# Workflow

## Coding
Work items are containers for tasks if a change can't be defined in a single task.
A task is a clearly scoped change that doesn't need further definitions. Usually a task can be used when fixing minor bugs, removing a small portion of obsolete code or a simple feature addition.

**Note that a description can be added to a task as guidance. But as soon as the description results into a TODO list a work item would be smarter to use.**

Another guidance to decide which one to choose is the time to implement a change. A task is 
usually implemented in a couple of minutes to half a day. Everything above this timespan should result into a work item to ensure keeping track of everything.

**Examples for a chat app:**

<table>
<tr><th>Task</th><td>Fix typo</td></tr>
<tr><th>Task</th><td>Fix remove debug</td></tr>
<tr><th>Task</th><td>Add long message collapse</td></tr>
<tr><th>Task</th><td>Add file message preview</td></tr>

<tr><th>Work Item</th><td>Add pdf support (File upload, PDF preview)</td></tr>
<tr><th>Work Item</th><td>Add read state (Read receipt, Received and read event, Realtime update)</td></tr>
</table>

### Work item
1. Define Tasks
	-  Clear uncertainties
	-  Create tasks in timesheet
2. Create branch
3. Implement changes
4. Create pull request
5. Review code and add comments
6. Iterate step 3-5 until satisfied
7. Merge branch

### Task
1. Define Task
	-  Clear uncertainties
	-  Create tasks in timesheet
2. Implement changes
3. Merge branch

## Incorporate new employee
1. Add employee to timesheet
2. Install timesheet on iPhone
3. Install vscode
4. Install vscode extensions
	- GitLens
	- Git Graph
	- Code Spell Checker
	- German - Code Spell Checker
5. Add vpn
6. Read wiki
7. Introduce into acryps fullstack
	- vldom
	- vlserver
	- vlquery
	- vldeploy
	- vlcluster
	- ...