# GIT TUTORIAL

## 1. Configuring GIT

### 1.1. Settings:

- Name
- Email
- Default editor
- Line ending.

#### 1.2. Levels:

- System: All users.
- Global: All repositories of the current user.
- Local: The current repository.

##### 1.2.1 Configuration of global:

Use the **git config -- global** comand.

To configure user information:
git config --global **user.name "<<name>>"**
git config --global **user.email email@something.com**

Default editor is vim, nevertheless the instructor recommends Visual Studio Code editor.
To config VS, you can add this line to de global configuration.
git config --global **core.editor "code --wait"**
*In this computer, default coder is __nano__*

All configurations are stored in a text document. To access it:
**git config --global -e**
config document is **.gitconfig**

##### 1.2.2. Configuration of end-of-line

Super important, because we can work from different Operative Systems. In _Windows_, the EOLs are **\n (Line Feed)** and **\r (Carriage Return)**, while for Linux and MacOS are just **\n**.
To config:
_For Windows:_
    git config --global **core.autocrlf true**
_Linux and MacOS:_
    git config --global **core.autocrlf input**

With this configuration, we make sure that unify criteria when a file is synchronized.

## 2. Getting help

### 2.1. Using **man**:

**man** git-config
You can also find the information in the Web.
###2.2. Cheat sheet:
It's supposed to be en my email.

## 3. Creating snapshots:

### 3.1. Initializing a **Repository**:

1. Create a directory:
    mkdir <<NameOfTheProject>>
    cd <<NameofTheProject>>
2. Initialize the Repository:
    git **init**
    A *.git* directory will be created. It must not be touched.
    Can be viewed with ls -al
    Writing **open** .git will show the directory content in file viewer.

## 4. Git Workflow:

### 4.1. What is a workflow?

1. A file or a group of files could be modified.
2. When finished, this new versions we'll be called **snapshots**.
3. When a snapshot is created, it goes through the **Staging Area** (also called **Index**).
    The Staging Area reviews the file and, if everything is ok, then makes a **commit**.
4. When changes are committed, new versions are stored in the GIT repository database (which is in the subdirectories of <<Project>>/.git

### 4.2. The workflow:

WORKING DIRECTORY -> STAGING AREA -> GIT REPOSITORY

### 4.3. The Staging area:

Staging area review the work before recording a snapshot. If it's wrong, it can be **uncommitted** and be committed in a future snapshot.

### 4.4. Let's do a real-life example.

1. Create two files.
    touch file1.txt
    touch file2.txt
    *If you want to create a file with data, you can use vi or nano instead of touch*.
2. git **add** file1.txt file2.txt
    This is weird but good to know. **add** is used to synchronize a deletion.
3. git **commit** -m "Initial commit."
    The commit is done.
    The argument -m includes a message. In this case "Initial commit."
        [master (commit-raíz) 91e51a0] Initial commit.
         2 files changed, 5 insertions(+)
         create mode 100644 file1.txt
         create mode 100644 file2.txt
    The **-m message** is super important, because its a description of the changes made in that commit.
3. When committing, Staging area is not empty, but keeps the commited documents. Having a reflection of the _production_ files or the _next version_ that is going to production.
Each commit has the followign data:
    ID | Message | Date/time | Author | Complete snapshot

***Really good to know:*** 
- Git doesn't use a lot of space, because all the content is **compressed** and never **duplicated**.
- Every commit contains a complete snapshot of the project.

## 5. Staging files:

git **status** give the information of the git local repository.
Good to find that it says **On branch master**. Remember this because it will be important.

git add can be used as follows:
- git add file1 to add only file1
- git add file1, file 2, ..., to add only the files defined.
- git add \*.txt adds all files with extension txt.
- git add . add all files in the directory.

## 6. Committing changes:

git **commit** -m "Description message!!!"
git **commit** will open the /.git/COMMIT_EDITMSG file, where you have to write the message for the commit. This is useful when the message must be larger.

### 6.1. Best practices for committing

1. Commit size matters:
    It's not worthy to commit too small changes or too large changes. The idea is to find a midpoint where you can have good checkpoints.
2. Commit often:
    Try to commit when you have reached a state you want to record.
3. Word convention:
    To make sure that everybody understand.
    Instructor recommends to always write in simple present.

### 6.2. Skipping the Staging Area:

Just do it if you are **totally sure** that your work is correct and there is no need to review.

git commit -am "Commit skipping the Staging Area."

The **-a** argument commits all files

## 7. Removing files:

**git ls-files** list the files in the Staging area.
Remember, Staging Area doesn't necessarely have the files latest version.

**rm <<file>>** remove files from the working directory (this is a Linux command).
**git add <<file>>** will remove the deleted file from the Staging Area.
**git commit -m "Removing file"** updates the repository, without the file.

### 7.1. Removing using GIT:

It's easier to use **git rm <<file1>> <<file1>>*** to delete using git.
git rm \*.ext to delete all files with extension \*.ext
git rm . to delete all files in directory.
git rm --cached remove files **only for the Staging Area**, and leaves the working directory untouched.
git rm -r allow recursive removal (good for directories).

**git rm --cached -r** directoryToBeDeleted/ will remove directory and it's content.

## 8. Renaming or moving files:

**mv** source.ext dest.ext rename files.
**mv** /from/this/dir/source.ext /to/this/dir/dest.ext moves the file and changes it's name.
Git understand that the source.ext file was deleted and dest.ext file has been created.
mv source.ext dest.ext
git add dest.ext
git status -> Will find that the file was renamed.

### 8.1. Renaming using GIT:

git mv source.ext dest.ext
git commit -m "A file has been renamed."

## 9. Ignoring files:

Sometimes is useful to ignore some files. For this manual, is useful to ignore **git-tutorial.md-swp** because is a temporal file.

To ignore a document, a file called **.gitignore** must be created. No name, just extension.
echo logs/ > .gitignore
vi ./gitignore
add the file or extensions that you want to ignore.
Save the document (for vi, must write :wq).
git add .gitignore
git commit -m "Adding ignore file."

The .gitignore document can be #commented.

## 10. Short status:

git **status -s** return the short status.
StagingArea | WorkingSpace FileName
M  file1.ext - Is in Staging area.
 M file2.ext - Is in working space.
?? file3.ext - Is a new file.

M is for Modified.
A is for Added.

## 11. Viewing the Staged and Unstaged Changes:

A good practice is to always review the code before committing.
git diff --staged

_**diff --git a/file1.txt b/file1.txt**_
**a/file1.txt** is the older copy
**b/file1.txt** is the newer copy
index b0d03a1..3ba6c5a 100644
--- a/file1.txt
+++ b/file1.txt
--- Changes made to older copy.
+++ Changes made to newer copy.
@@ -3,3 +3,5 @@ Hicimos un cambio a este documento
**-3,3** lines in older copy.
**+3,5** lines in newer copy.
 Hicimos dos cambios a este documento
 CAMBIO IMPORTANTÍSIMO
 CAMBIO PARA HACER UN COMMIT SIN PASAR POR EL STAGING AREA.
//THE CHANGES ARE IN HERE
+ADDING A NEW LINE FOR GIT STATUS -S EXAMPLE
+Experiment

### 11.1. Visual Diff Tools:

Just is you are using a visual tool.
For VSCode
git config --global **diff.tool vscode**
git config --global difftoo.vscode.cmd "code --wait --diff $LOCAL $REMOTE"

## 12. Watching the log:

**git log** display the historic of commits from last to first

**ATTENTION:** At first line, you will find HEAD -> master. This is the **BRANCH**.
Remember, because it's going to be important.
Head -> Current branch.

git log **--oneline** Short log.
git log **--reverse** swap the story from first to last.

### 12.1. Viewing a commit:

git **show** id - Display the information of the commit.
git show BRANCH~number of lines before.
git show BRANCH~number:<fileToReview>

git ls-tree the information is represented as a tree.
blob - File
tree - Directory

## 13. Unstaging files:

Always review the Staging Area before committing.

git **restore** --staged file.ext | \*.ext | .
Remove the selected file(s) from the Staging Area.

### 13.1. Discarding local changes:

git **restore** file.ext | \*.ext | .
Restores the selected files in the Working Directory.

git **clean** delete all files in Working Directory.
View the man page: man git-clean

### 13.2. Restoring a file to an earlier version:

git restore **--source**=HEAD~1 <file.ext>
