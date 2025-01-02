# Linux/Bash questions

## Question 1
How do you change the ownership of a file named `data.txt` to a user named `researcher` and a group named `research_team`?

## Question 2
What command would you use to add a new group called `bioinformatics` and then assign a user named `alex` to this group?

## Question 3
You need to transfer a file named `data.csv` from your local machine to a remote server located at `192.168.1.100`, placing it under the `/home/user/files/` directory. What command would you use and how?

## Question 4
You want to identify and delete all files named `temp.txt` in the `/tmp` directory and its subdirectories. What command would you run to accomplish this?

## Question 5
A file `script.sh` has `-rw-r--r--` permissions. You want to make it executable by the file's owner. What command would you run?

## Question 6
Describe the purpose of the following command and what its output represents:

```bash
df -h
```

## Question 7
You are tasked with archiving and compressing a directory `/project/data` into a file named `data_backup.tar.gz`. Write the command you would use.

## Question 8
You are notified by the IT team that you are taking up way too much storage space, and so you need to delete some unused data.  
You have several projects, and you decide to check the storage usage ***per project*** to prioritise which project to clean up first. Below is the directory tree of your projects:
```bash
/shared/user/john-doe
├── project_A
├── project_B
└── group
    ├── project_C
    └── project_D
```
How can you get a concise report of the storage usage per project?


## Question 9
You want to find all files in the `/home/research/` directory that were modified in the last 7 days. What command would you use?


## Question 10
You are tasked with copying the contents of `/var/www/html/` from a local machine to a remote server at `backup.example.com:/var/backups/html/`. How would you ensure that all permissions, timestamps, and symbolic links are preserved, and verify the integrity of the files after copying?


## Question 11
A user reports that they cannot connect to the server via SSH. You shared this information with your colleague and he/she mentions that they recently changed some SSH configurations.

- Where would you find the main configuration file for the SSH service?
- After reverting your colleague's change, how do you restart the SSH service?


## Question 12
A colleague requests help because they can't clone a repository from GitHub.

- How would you check if GitHub is reachable over the network?
- How would you verify that port 443 (used for HTTPS) is open for connections to `github.com`?


## Question 13
A colleague on an Ubuntu system reports the following error while trying to install a package:

```bash
Command 'yum' not found
```

- What is the issue with their command?
- What command should they use to install a package on Ubuntu?


## Question 14
A colleague has installed a custom version of Python in `/opt/python3.9/bin`, but when they type `python3` in the terminal, it still uses the system's default version located in `/usr/bin/python3`.

- Why is this happening?
- How would you modify the environment to make `/opt/python3.9/bin/python3` the default python3 executable?
- How can you verify which version of python3 is being used after the change?