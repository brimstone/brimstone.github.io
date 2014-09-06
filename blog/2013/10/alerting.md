Alerting
--------
######Wed Oct 23 22:43:02 EDT 2013

This is a post about alertting. I think this schedule is usable, but it requires more thought:

<table>
	<tr>
		<th>Severity</th>
		<th>Frequency</th>
		<th>Example</th>
	</tr>
	<tr>
		<td>Disaster</td>
		<td>5 minutes</td>
		<td>Server offline, disk free < 10%, Load > # cpus</td>
	</tr>
	<tr>
		<td>High</td>
		<td>10 minutes</td>
		<td>Load > 2</td>
	</tr>
	<tr>
		<td>Warning</td>
		<td>20 minutes</td>
		<td>??</td>
	</tr>
	<tr>
		<td>Average</td>
		<td>30 minutes</td>
		<td>Disk < 20%, swap < 20%</td>
	</tr>
	<tr>
		<td>Information</td>
		<td>1 hour</td>
		<td>Software version changed, file changed</td>
	</tr>
</table>
