
| **Command**                                                                   | **Description**                                        | **Remarks**                                                                                    |
| ----------------------------------------------------------------------------- | ------------------------------------------------------ | ---------------------------------------------------------------------------------------------- |
| `pwd`                                                                         | Print working directory.                               |                                                                                                |
| `ls`<br>`ls -a`                                                               | List directory contents.<br>Include hidden files.      |                                                                                                |
| `cd <directory>`<br>                                                          | Change directory.                                      |                                                                                                |
| `nano <filename>`                                                             | Use to delete, add, or change the contents of a file.  | Ctrl + O to save changes.<br>Ctrl + X to exit the editor.                                      |
| `echo`                                                                        | Create or edit a file.                                 | echo "This is the content." > filename.md<br>echo "This is additional content." >> filename.md |
| `git --version`                                                               | Check version of Git.                                  |                                                                                                |
| `git status`                                                                  | Check the status of files.                             |                                                                                                |
| `git add <filename>`<br>`git add .`                                           | Add a file to staging.<br>Add all files to staging.    |                                                                                                |
| `git commit -m "Commit message"`                                              | Commit changes.                                        |                                                                                                |
| `git diff <filename>`<br>`git diff -r HEAD `<br>`git diff -r HEAD <filename>` | Compare unstaged file with the last committed version. | `git diff -r HEAD` won't work without the `HEAD`                                               |
### Git Workflow
1. Modify a file
2. Save the draft
3. Commit the updated file
4. Repeat

### Git Structure
1. Commit - contains the metadata.
2. Tree - tracks the names and locations in the repo.
3. Blob - binary large object | may contain any type of data | compressed snapshot of a file's data.
![[Commit Structure.png]]