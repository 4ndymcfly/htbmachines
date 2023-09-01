# Hack The Box Machine Finder
### Hack The Box search engine based on the machines solved by @S4vitar (Hack4you Academy Practice)
--- 
**htbmachines** is a bash script that allows you to search for HTB machines by filtering by name, operating system, skill, certification, difficulty and their corresponding Youtube link.

Usage:
```bash
./htbmachines [OPTION]

		-The options -o (OS) and -d (DIFFICULTY) can be concatenated. 
		Example: ./htbmachines -o Linux -d Insane

		-The options -c (CERTIFICATION) and -d (DIFFICULTY) can be concatenated. 
		Example: ./htbmachines -c OSCP -d Easy

Options: 

	-u,	Update/Download DB of machines.
	-m,	Search by machine name.
	-i,	Search by machine IP.
	-o,	Search by machine Operating System (Windows, Linux).
	-s,	Search machines with the indicated Skill.
	-c,	Search machines by the indicated certification (OSCP, eJPT, etc).
	-d,	List available machines according to their difficulty (Easy, Medium, Hard, Insane).
	-y,	Get YouTube URL of the machine resolution.
	-h,	Show this help panel.
```
