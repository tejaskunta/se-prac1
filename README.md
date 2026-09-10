. Important pom.xml

Remember these:

<groupId>com.lms</groupId>
<artifactId>LMSWEBP</artifactId>
<version>1.0</version>
<packaging>war</packaging>
Java version
<properties>
    <maven.compiler.source>17</maven.compiler.source>
    <maven.compiler.target>17</maven.compiler.target>
</properties>
Servlet dependency
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
    <version>4.0.1</version>
    <scope>provided</scope>
</dependency>
JUnit
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.13.2</version>
    <scope>test</scope>
</dependency>
WAR name
<build>
    <finalName>LMSWEBP</finalName>
</build>

So output becomes:

target/LMSWEBP.war
4. Maven Commands
Clean old files
mvn clean
Compile
mvn compile
Run tests
mvn test
Build WAR
mvn clean package

After this:

target/LMSWEBP.war
Main Maven lifecycle to remember
clean → compile → test → package
5. Maven Important Terms
.m2 repository

Maven stores downloaded dependencies here:

C:\Users\YOURNAME\.m2\repository
pom.xml

Contains:

project information
dependencies
plugins
build configuration
target

Contains generated files:

target/

Especially:

target/LMSWEBP.war
finalName

Controls the generated WAR/JAR name.

<finalName>LMSWEBP</finalName>
6. Git Setup

Inside your project folder:

git init

Set username:

git config --global user.name "Your Name"

Set email:

git config --global user.email "your@email.com"

Check:

git config --global user.name
git config --global user.email
7. First Git Commit

Check files:

git status

Add everything:

git add .

Commit:

git commit -m "first commit"

Check history:

git log
8. .gitignore

For Maven:

target/

Usually also:

.classpath
.project
.settings/

Then:

git add .
git commit -m "add gitignore"
9. Create GitHub Repository

Create repository on GitHub.

Then connect:

git remote add origin https://github.com/YOURUSERNAME/LMSWEBP.git

Check:

git remote -v

Rename branch to main:

git branch -M main

Push:

git push -u origin main

If remote already exists:

git remote set-url origin https://github.com/YOURUSERNAME/LMSWEBP.git
10. Git Branches

Create branch:

git branch feature

Switch:

git checkout feature

OR:

git switch feature

Create + switch:

git checkout -b feature

Check branches:

git branch

Switch back:

git checkout main
11. Git Merge

Suppose:

main
feature

First go to main:

git checkout main

Then merge:

git merge feature

Basic idea:

feature → main
12. Git Stash

Temporarily save unfinished changes:

git stash

See stashes:

git stash list

Bring back latest:

git stash pop

Apply without removing stash:

git stash apply

Delete stash:

git stash drop
Remember
stash = temporarily hide changes
pop = bring them back
13. Git Restore

Discard changes in a file:

git restore filename

Example:

git restore App.java

Unstage a file:

git restore --staged App.java
14. Git Revert

Undo a commit safely by creating a new commit:

git revert COMMIT_ID

Example:

git revert abc123
Remember
revert = undo commit safely
15. Git Reset

Move HEAD backward.

git reset --soft HEAD~1

Keeps changes staged.

git reset --mixed HEAD~1

Keeps changes but unstages them.

git reset --hard HEAD~1

Deletes the commit and changes.

Easy memory
soft   → keep staged
mixed  → keep files
hard   → delete changes
16. Git Clone

Copy a GitHub repository:

git clone https://github.com/USERNAME/REPO.git

Then:

cd REPO
17. Merge Conflict

If:

git merge feature

causes conflict:

<<<<<<< HEAD
main code
=======
feature code
>>>>>>> feature

Fix the file manually.

Then:

git add .
git commit -m "resolve merge conflict"
18. Dockerfile

Use this:

FROM tomcat:9.0

COPY target/*.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080

CMD ["catalina.sh", "run"]
Meaning
FROM     → base image
COPY     → copy WAR into Tomcat
EXPOSE   → container port
CMD      → start Tomcat
19. Build Docker Image

Make sure you are in the project folder:

docker build -t lmsimage .

Check images:

docker image ls
20. Run Container
docker run -d -p 7089:8080 --name lmcontainer lmsimage

Meaning:

7089 = your computer
8080 = container/Tomcat

Open:

http://localhost:7089/
21. Check Containers

Running containers:

docker ps

All containers:

docker ps -a

Stop:

docker stop lmcontainer

Start again:

docker start lmcontainer

Remove:

docker rm lmcontainer

Force remove:

docker rm -f lmcontainer
22. Docker Images

List images:

docker image ls

Remove image:

docker rmi lmsimage
23. Docker Login
docker login

Enter Docker Hub username/password.

24. Push Docker Image

Tag:

docker tag lmsimage YOURUSERNAME/lmsimage:latest

Push:

docker push YOURUSERNAME/lmsimage:latest
25. Pull Docker Image
docker pull YOURUSERNAME/lmsimage:latest

Run it:

docker run -d -p 7089:8080 --name lmcontainer YOURUSERNAME/lmsimage:latest
26. Ubuntu Docker Example

Pull Ubuntu:

docker pull ubuntu

Run interactively:

docker run -it ubuntu

Inside container:

ls

Exit:

exit
27. Most Important Git Commands

Memorize this table:

Question	Command
Create repo	git init
Check status	git status
Add files	git add .
Commit	git commit -m "message"
See commits	git log
Create branch	git branch feature
Switch branch	git checkout feature
Create + switch	git checkout -b feature
Merge	git merge feature
Clone	git clone URL
Temporarily save changes	git stash
Restore stash	git stash pop
Undo commit safely	git revert ID
Remove last commit	git reset HEAD~1
Discard file changes	git restore file
Unstage file	git restore --staged file
Add remote	git remote add origin URL
Push	git push -u origin main
See branches	git branch
28. Most Important Docker Commands
docker image ls
docker ps
docker ps -a
docker build -t lmsimage .
docker run -d -p 7089:8080 --name lmcontainer lmsimage
docker stop lmcontainer
docker start lmcontainer
docker rm lmcontainer
docker rmi lmsimage
docker login
docker tag lmsimage YOURUSERNAME/lmsimage:latest
docker push YOURUSERNAME/lmsimage:latest
docker pull YOURUSERNAME/lmsimage:latest
29. Full Exam Workflow

This is the main thing to memorize:

Step 1 — Maven
mvn clean
mvn compile
mvn test
mvn clean package

Check:

target/LMSWEBP.war
Step 2 — Git
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/YOURUSERNAME/LMSWEBP.git
git push -u origin main
Step 3 — Docker
docker build -t lmsimage .
docker run -d -p 7089:8080 --name lmcontainer lmsimage

Open:

http://localhost:7089/
Step 4 — Docker Hub
docker login
docker tag lmsimage YOURUSERNAME/lmsimage:latest
docker push YOURUSERNAME/lmsimage:latest
30. One-Line Mental Map


And the 3 commands you absolutely cannot forget:

mvn clean package
git add . && git commit -m "first commit"
docker run -d -p 7089:8080 --name lmcontainer lmsimage
