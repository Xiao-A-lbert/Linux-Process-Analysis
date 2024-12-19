# Linux Process Analysis

<h2>Description</h2>
In this Linux Process Analysis task, I used various command lines to observe the processes, process tree, top command, and lsof to observe the notmalware.elf process even after deleting it. 

<h2>Languages and Utilities Used</h2>

- <b>Linux CLI</b>

<h2>Environments Used</h2>

- <b>Ubuntu</b>

<br />
<br />
I used "sudo ps -AFH | less" to show a detailed, hierarchical view of all processes running on the system, including those owned by other users. Here's a breakdown of what this command does:
sudo: Executes the command with superuser privileges, 
ps -AFH: Lists all processes with extended information, 
-A: Shows all processes,
-F: Displays full-format listing,
-H: Shows a process hierarchy (tree structure),
| less: Pipes the output to the less command, allowing you to scroll through the results page by page.

![1) sudo ps -AFH to show parent process id of notmalware](https://github.com/user-attachments/assets/ea7b731a-acff-4d3a-85ab-e09efd6922e3)

<br />
<br />
I used "pstree -p -s 3115" to display a process tree showing the parent processes of the process with PID 3115, including process IDs. Here's what each part of the command does:
pstree: Displays running processes as a tree,
-p: Shows process IDs (PIDs) in parentheses after each process name,
-s: Shows parent processes of the specified PID,
3115: The specific process ID for which we want to see the parent hierarchy.

![2) process tree](https://github.com/user-attachments/assets/f8f5e073-7fe0-4273-ab89-77e0eb00bb48)

<br />
<br />  
I used "sudo top -u albert -c" to provide a real-time, dynamic view of the system, focusing on processes owned by albert. -c: Displays the absolute path of running processes.

![3) sudo top -u albert -c ](https://github.com/user-attachments/assets/6830dc60-4040-45aa-a94b-cfa173f226b7)

<br />
<br />
Using "sudo top -u albert -c -o -TIME+" similar above but to sort the list by most recent process time.  

![4) -TIME+ sorts time column most recent first](https://github.com/user-attachments/assets/337705b4-5065-4f35-b56e-aefea03b9900)

<br />
<br />
Changing direcetory to /proc/3115 and cat the cmdline will show the command line used to execute PID 3115 of notmalware.elf

![5) proc pid3115 cat cmdline](https://github.com/user-attachments/assets/dc58cb85-ffe8-47e0-bec0-2756e0d3546c)

<br />
<br />
ls -al cwd will list the current working directory of the PID 3115 notmalware.elf

![6) shows current working directory of notmalware](https://github.com/user-attachments/assets/a7f85a8f-45bd-4a27-9a99-8dce80b8b06c)

<br />
<br />
Making a backup and deleting notmalware.elf, I ran "sudo lsof -p 3115" to show that the notmalware.elf process is still running even though it was deleted. 

![7) deleting malware  run lsof shows process still running](https://github.com/user-attachments/assets/f5fd06b0-005c-40d8-b1ce-b015b255c8b9)

<br />
<br />
I used "lsof +L1" to display information about deleted files that are still being held open by processes12. Here's what this command does:
It lists all open files that have a link count (number of hard links) less than 1.
This typically indicates files that have been unlinked (deleted) from the filesystem but are still being held open by one or more processes.

![8) lsof +L1, ls al exe shows file process ](https://github.com/user-attachments/assets/e9b07855-8eac-4d26-8733-b765d9c62043)

<br />
<br />
