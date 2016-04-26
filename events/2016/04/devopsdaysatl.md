Devopsdaysatl
-------------
######Tue Apr 27 2016

http://www.devopsdays.org/events/2016-atlanta/program/

Opening welcome
---------------
- Make new friends
- Come back next year


Putting the Service in Microservices
------------------------------------
Jeff Sussna @jeffsussna
- DevOps is Conway's Law
- "The shape of your organization drives the shape of your application."
- Every project has to be broken down into parts.
- One must consider the look and interactions of each part.
- "Your microservice teams are service providers."
- "This is what I do - > this is how I help."


Enterprise Application as a 12 Factor App
-----------------------------------------
*Developing and Operating an Enterprise Application as a 12Factor App using Docker and Amazon Web Services*
Kartik Pandya kpandya@manh.com
- Enterprise app:
  - upgradable with zero downtime
  - scalable
  - Able to deliver changes quickly
  - low op-ex and cap-ex
- He couldn't think of any enterprise apps that are 12 factor
- "New functionality trumps architectural improvements" thus none
- Must Cs
  - Componentization
  - Containerization
  - Continuous Integration
  - Cloud-awareness
- 2 service discovery
- 3 Externalize Configuration
- 4 Take backwards compatibility seriously
  - Version 1.x can have deprecation warnings
- 5 Make your components disposable
- 6 Containerize
- 7 Decouple your code from deploys
  -  don't hardcode RDS in your code
  - environment variables
- 8 Simplify your logs with log aggregator
  - Components should log to stdout
  - Something like LogSpout gathers stdout and publishes to ELK
- 9 Focus on CI
  - Int, QA, Sim Prod, UA, Prod
- 10 Gateways
  - pull code, tag as IRON
  - integration pulls IRON, tags as a BRONZE when passing
  - upgrade runway gathers from many QAs and publishes to one sim prod
- 11 Use Container Management
- 12 Distinguish pets from Cattle
  - Database, No-SQL, cache, messaging provider are pets
  - pets are named and at known locations
  - pets exist before cattle


Frameworks for Feedback
-----------------------
Rebecca Miller-Webster @rmillerwebster
- Having another human look at your code is the best way to reduce bugs
- 1:1s are feedbacks, need to be more between peers
- The goal of feedback is to build a better relationship
- Situation, Behavior, Impact, Recommendation
- Negative feedback weighs more than positive. 3:1
- Receiving feedback: Listen, Ask questions, Thank you & Follow up
- need to get quotes about mirroring from the slides
  - "I hear you saying..."
- Get better empathy by listening and summarizing
- Regular requests are more likely to illicit feedback
- What should I Start/Stop/Continue doing?
- Good feedback is Actionable, Specific, and Kind
- Review results
- Look up "feeling wheels"



Closing Keynote - Burnout
-------------------------
John Willis
- made a blog post about burnout, need to read on itrevolution.com
- karojatu "death by overwork
- burnout.io
- Higher performers are more likely to burnout
- B-DOC: Burnout During Organization Change
- 3 dimensions: Exhaustion, Cynicism, Efficacy
- Ship Show has an episode with Maslach
- Maslach Burnout Inventory Survey
- Maslach also has an Areas of Worklife Survey
- Netflix has a culture deck
- Pushing the DevOps Survey


Lunch Questions
---------------
- Terraform can keep state in an S3 bucket, where else?
- Does a test servEr exist insuch to keep track of which tests fail the most frequent?