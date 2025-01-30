# Linux/Bash questions

## Question 1
How do you change the ownership of a file named `data.txt` to a user named `researcher` and a group named `research_team`?
> chown researcher:research_team data.txt

## Question 2
What command would you use to add a new group called `bioinformatics` and then assign a user named `alex` to this group?
> sudo groupadd bioinformatics

> sudo usermod -aG bioinformatics alex

## Question 3
You need to transfer a file named `data.csv` from your local machine to a remote server located at `192.168.1.100`, placing it under the `/home/user/files/` directory. What command would you use and how?
> rsync -avP data.csv user@192.168.1.100:/home/user/files/

## Question 4
You want to identify and delete all files named `temp.txt` in the `/tmp` directory and its subdirectories. What command would you run to accomplish this?
> find /tmp -type f -name 'temp.txt' -delete

> find /tmp -type f -name 'temp.txt' -exec rm {} +

## Question 5
A file `script.sh` has `-rw-r--r--` permissions. You want to make it executable by the file's owner. What command would you run?
> chmod u+x script.sh

## Question 6
Describe the purpose of the following command and what its output represents:

```bash
df -h
```
> It reports the disk space usage in human-readable format, i.e. 100.4G, 23.9M

## Question 7
You are tasked with archiving and compressing a directory `/project/data` into a file named `data_backup.tar.gz`. Write the command you would use.
> tar -czvf /project/data_backup.tar.gz -C /project data

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
> du -h --max-depth=2 /shared/user/john-doe/ | sort -hr

## Question 9
You want to find all files in the `/home/research/` directory that were modified in the last 7 days. What command would you use?
> find /home/research/ -type f -mtime -7 -exec ls -ltr {} +

## Question 10
You are tasked with copying the contents of `/var/www/html/` from a local machine to a remote server at `backup.example.com:/var/backups/html/`. How would you ensure that all permissions, timestamps, and symbolic links are preserved, and verify the integrity of the files after copying?
> rsync -avP --checksum /var/www/html/ backup.example.com:/var/backups/html/

## Question 11
A user reports that they cannot connect to the server via SSH. You shared this information with your colleague and he/she mentions that they recently changed some SSH configurations.

- Where would you find the main configuration file for the SSH service?
- After reverting your colleague's change, how do you restart the SSH service?


## Question 12
A colleague requests help because they can't clone a repository from GitHub.

- How would you check if GitHub is reachable over the network?
- > ping www.github.com
- How would you verify that port 443 (used for HTTPS) is open for connections to `github.com`?
- > nc -zv github.com 443

## Question 13
A colleague on an Ubuntu system reports the following error while trying to install a package:

```bash
Command 'yum' not found
```

- What is the issue with their command?
- > `yum` is not installed as default package manager in Ubuntu
- What command should they use to install a package on Ubuntu?
- > They should use `apt-get install` or `apt install`

## Question 14
A colleague has installed a custom version of Python in `/opt/python3.9/bin`, but when they type `python3` in the terminal, it still uses the system's default version located in `/usr/bin/python3`.

- Why is this happening?
- > The /opt/python3.9/bin directory is not in PATH, or it is lower in priority than /usr/bin
- How would you modify the environment to make `/opt/python3.9/bin/python3` the default python3 executable?
- > The colleague needs to add the `/opt/python3.9/bin` to the path variable (in the beginning) in `.bashrc` and source it. Eg. 'export PATH=/opt/python3.9/bin:$PATH'
- How can you verify which version of python3 is being used after the change?
- > By executing `which python3`
