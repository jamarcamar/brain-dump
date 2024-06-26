
| **Command**                                                                                                                                                    | **Description**                                        | **Remarks**                                                                                        |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------ | -------------------------------------------------------------------------------------------------- |
| `pwd`                                                                                                                                                          | Print working directory.                               |                                                                                                    |
| `ls`<br>`ls -a`                                                                                                                                                | List directory contents.<br>Include hidden files.      |                                                                                                    |
| `cd <directory>`<br>                                                                                                                                           | Change directory.                                      |                                                                                                    |
| `nano <filename>`                                                                                                                                              | Use to delete, add, or change the contents of a file.  | `Ctrl + O` to save changes.<br>`Ctrl + X `to exit the editor.                                      |
| `echo`                                                                                                                                                         | Create or edit a file.                                 | `echo "This is the content." > filename.md`<br>`echo "This is additional content." >> filename.md` |
| `git --version`                                                                                                                                                | Check version of Git.                                  |                                                                                                    |
| `git status`                                                                                                                                                   | Check the status of files.                             |                                                                                                    |
| `git add <filename>`<br>`git add .`                                                                                                                            | Add a file to staging.<br>Add all files to staging.    |                                                                                                    |
| `git commit -m "Commit message"`                                                                                                                               | Commit changes.                                        |                                                                                                    |
| `git diff <filename>`<br>`git diff -r HEAD`<br>`git diff -r HEAD <filename>`<br>`git diff -r HEAD~1`<br>`git diff <hash1> <hash2>`<br>`git diff HEAD~3 HEAD~2` | Compare unstaged file with the last committed version. | `git diff -r HEAD` won't work without the `HEAD`                                                   |
| `git log`<br>`git log -3`<br>`git log -3 <filename>`<br>`git log --since='Month Day Year'`<br>`git log --since='Month Day Year' --until='Month Day Year'`      | Show commit logs.                                      | `Space` to show more recent commits.<br>`Q` to quit the log and return to the terminal.            |
| `git show <hash>`<br>`git show HEAD~1`                                                                                                                         | Show a particular commit.                              |                                                                                                    |
| `git annotate <filename>`                                                                                                                                      | Show changes per document line.                        |                                                                                                    |
| `git reset HEAD <filename>`<br>`git reset HEAD`                                                                                                                | Unstaging a file in Git.                               |                                                                                                    |
| `git checkout -- <filename>`<br>`git checkout .`<br>`git checkout <hash> <filename>`<br>`git checkout HEAD~1 <filename>`<br>`git checkout <hash>`              | Undo changes to an unstaged files.                     |                                                                                                    |
| `git clean -n`                                                                                                                                                 | See untracked files.                                   |                                                                                                    |
| `git clean -f`                                                                                                                                                 | Delete untracked files.                                | This cannot be undone.                                                                             |
| `git config --list`                                                                                                                                            | To show list of settings.                              | `--local`<br>`--global`<br>`--system`                                                              |
|                                                                                                                                                                |                                                        |                                                                                                    |
|                                                                                                                                                                |                                                        |                                                                                                    |
|                                                                                                                                                                |                                                        |                                                                                                    |
### Git Workflow
1. Modify a file
2. Save the draft
3. Commit the updated file
4. Repeat

### Git Structure
1. Commit - contains the metadata.
2. Tree - tracks the names and locations in the repo.
3. Blob - binary large object | may contain any type of data | compressed snapshot of a file's data.
![[Commit structure.png]]

### Configuring Git

#### Levels of settings
`git config --list`

- Three levels of settings
	1. `--local` : settings for one specific project
	2. `--global` : settings for all of our projects
	3. `--system` : settings for every users on this computer
- Changing settings
		`git config --global setting value`
		example: `git config --global user.email camarjamar@gmail.com`

#### Using alias
- Used to shorten a command.
- example: `git config --global alias.ci 'commit -m'`
- example: `git config --global alias.unstage 'reset HEAD'`
- tracking aliases: `git config --global --list`

#### Ignoring specific files
- `nano .gitignore`
- `*.log`


### Branches
![[Merging report to main.png]]


#### Codes
- `git branch`
- Create a new branch: `git checkout -b <branch name>`
- Difference between branches: `git diff <branch1> <branch2>`
- Switch branch: `git checkout <branch>`
- To merge: `git merge <source> <destination>`


### Creating Repos
 
`git init <repo>`

To convert a directory into a repo
`git init`

### Working with remotes
#### Cloning locally
`git clone <path to project directory> <repo name>`

#### Cloning a remote
`git clone <URL>`

To know where the original was
`git remote`
To know more information such as remote's URL
`git remote -v`

#### Creating a remote
`git remote add <name> <URL>`

### Gathering from a remote
 
 `git fetch <name of the remote> <local branch to fetch into>`
`git fetch origin main`


To synchronize contents
`git merge origin main`


To simplify `fetch` and `merge`
`git pull origin main`

To push
`git push remote local_branch`

