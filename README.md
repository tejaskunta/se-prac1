
---

# 2. Import Maven Project in Eclipse

```text
File
→ Import
→ Git
→ Projects from Git (with smart import)
→ Clone URI
```

Enter GitHub repository URL.

Then:

```text
Finish
```

If creating/importing a local Maven project:

```text
File
→ Import
→ Maven
→ Existing Maven Projects
```

---

# 3. Important `pom.xml`

Remember these:

```xml
<groupId>com.lms</groupId>
<artifactId>LMSWEBP</artifactId>
<version>1.0</version>
<packaging>war</packaging>
```

### Java version

```xml
<properties>
    <maven.compiler.source>17</maven.compiler.source>
    <maven.compiler.target>17</maven.compiler.target>
</properties>
```

### Servlet dependency

```xml
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
    <version>4.0.1</version>
    <scope>provided</scope>
</dependency>
```

### JUnit

```xml
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.13.2</version>
    <scope>test</scope>
</dependency>
```

### WAR name

```xml
<build>
    <finalName>LMSWEBP</finalName>
</build>
```

So output becomes:

```text
target/LMSWEBP.war
```

---

# 4. Maven Commands

### Clean old files

```bash
mvn clean
```

### Compile

```bash
mvn compile
```

### Run tests

```bash
mvn test
```

### Build WAR

```bash
mvn clean package
```

After this:

```text
target/LMSWEBP.war
```

### Main Maven lifecycle to remember

```text
clean → compile → test → package
```

---

# 5. Maven Important Terms

### `.m2` repository

Maven stores downloaded dependencies here:

```text
C:\Users\YOURNAME\.m2\repository
```

### `pom.xml`

Contains:

* project information
* dependencies
* plugins
* build configuration

### `target`

Contains generated files:

```text
target/
```

Especially:

```text
target/LMSWEBP.war
```

### `finalName`

Controls the generated WAR/JAR name.

```xml
<finalName>LMSWEBP</finalName>
```

---

# 6. Git Setup

Inside your project folder:

```bash
git init
```

Set username:

```bash
git config --global user.name "Your Name"
```

Set email:

```bash
git config --global user.email "your@email.com"
```

Check:

```bash
git config --global user.name
git config --global user.email
```

---

# 7. First Git Commit

Check files:

```bash
git status
```

Add everything:

```bash
git add .
```

Commit:

```bash
git commit -m "first commit"
```

Check history:

```bash
git log
```

---

# 8. `.gitignore`

For Maven:

```text
target/
```

Usually also:

```text
.classpath
.project
.settings/
```

Then:

```bash
git add .
git commit -m "add gitignore"
```

---

# 9. Create GitHub Repository

Create repository on GitHub.

Then connect:

```bash
git remote add origin https://github.com/YOURUSERNAME/LMSWEBP.git
```

Check:

```bash
git remote -v
```

Rename branch to main:

```bash
git branch -M main
```

Push:

```bash
git push -u origin main
```

If remote already exists:

```bash
git remote set-url origin https://github.com/YOURUSERNAME/LMSWEBP.git
```

---

# 10. Git Branches

Create branch:

```bash
git branch feature
```

Switch:

```bash
git checkout feature
```

OR:

```bash
git switch feature
```

Create + switch:

```bash
git checkout -b feature
```

Check branches:

```bash
git branch
```

Switch back:

```bash
git checkout main
```

---

# 11. Git Merge

Suppose:

```text
main
feature
```

First go to main:

```bash
git checkout main
```

Then merge:

```bash
git merge feature
```

Basic idea:

```text
feature → main
```

---

# 12. Git Stash

Temporarily save unfinished changes:

```bash
git stash
```

See stashes:

```bash
git stash list
```

Bring back latest:

```bash
git stash pop
```

Apply without removing stash:

```bash
git stash apply
```

Delete stash:

```bash
git stash drop
```

### Remember

```text
stash = temporarily hide changes
pop = bring them back
```

---

# 13. Git Restore

Discard changes in a file:

```bash
git restore filename
```

Example:

```bash
git restore App.java
```

Unstage a file:

```bash
git restore --staged App.java
```

---

# 14. Git Revert

Undo a commit **safely** by creating a new commit:

```bash
git revert COMMIT_ID
```

Example:

```bash
git revert abc123
```

### Remember

```text
revert = undo commit safely
```

---

# 15. Git Reset

Move HEAD backward.

```bash
git reset --soft HEAD~1
```

Keeps changes staged.

```bash
git reset --mixed HEAD~1
```

Keeps changes but unstages them.

```bash
git reset --hard HEAD~1
```

Deletes the commit and changes.

### Easy memory

```text
soft   → keep staged
mixed  → keep files
hard   → delete changes
```

---

# 16. Git Clone

Copy a GitHub repository:

```bash
git clone https://github.com/USERNAME/REPO.git
```

Then:

```bash
cd REPO
```

---

# 17. Merge Conflict

If:

```bash
git merge feature
```

causes conflict:

```text
<<<<<<< HEAD
main code
=======
feature code
>>>>>>> feature
```

Fix the file manually.

Then:

```bash
git add .
```

```bash
git commit -m "resolve merge conflict"
```

---

# 18. Dockerfile

Use this:

```dockerfile
FROM tomcat:9.0

COPY target/*.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080

CMD ["catalina.sh", "run"]
```

### Meaning

```text
FROM     → base image
COPY     → copy WAR into Tomcat
EXPOSE   → container port
CMD      → start Tomcat
```

---

# 19. Build Docker Image

Make sure you are in the project folder:

```bash
docker build -t lmsimage .
```

Check images:

```bash
docker image ls
```

---

# 20. Run Container

```bash
docker run -d -p 7089:8080 --name lmcontainer lmsimage
```

Meaning:

```text
7089 = your computer
8080 = container/Tomcat
```

Open:

```text
http://localhost:7089/
```

---

# 21. Check Containers

Running containers:

```bash
docker ps
```

All containers:

```bash
docker ps -a
```

Stop:

```bash
docker stop lmcontainer
```

Start again:

```bash
docker start lmcontainer
```

Remove:

```bash
docker rm lmcontainer
```

Force remove:

```bash
docker rm -f lmcontainer
```

---

# 22. Docker Images

List images:

```bash
docker image ls
```

Remove image:

```bash
docker rmi lmsimage
```

---

# 23. Docker Login

```bash
docker login
```

Enter Docker Hub username/password.

---

# 24. Push Docker Image

Tag:

```bash
docker tag lmsimage YOURUSERNAME/lmsimage:latest
```

Push:

```bash
docker push YOURUSERNAME/lmsimage:latest
```

---

# 25. Pull Docker Image

```bash
docker pull YOURUSERNAME/lmsimage:latest
```

Run it:

```bash
docker run -d -p 7089:8080 --name lmcontainer YOURUSERNAME/lmsimage:latest
```

---

# 26. Ubuntu Docker Example

Pull Ubuntu:

```bash
docker pull ubuntu
```

Run interactively:

```bash
docker run -it ubuntu
```

Inside container:

```bash
ls
```

Exit:

```bash
exit
```

---

# 27. Most Important Git Commands

Memorize this table:

| Question                 | Command                     |
| ------------------------ | --------------------------- |
| Create repo              | `git init`                  |
| Check status             | `git status`                |
| Add files                | `git add .`                 |
| Commit                   | `git commit -m "message"`   |
| See commits              | `git log`                   |
| Create branch            | `git branch feature`        |
| Switch branch            | `git checkout feature`      |
| Create + switch          | `git checkout -b feature`   |
| Merge                    | `git merge feature`         |
| Clone                    | `git clone URL`             |
| Temporarily save changes | `git stash`                 |
| Restore stash            | `git stash pop`             |
| Undo commit safely       | `git revert ID`             |
| Remove last commit       | `git reset HEAD~1`          |
| Discard file changes     | `git restore file`          |
| Unstage file             | `git restore --staged file` |
| Add remote               | `git remote add origin URL` |
| Push                     | `git push -u origin main`   |
| See branches             | `git branch`                |

---

# 28. Most Important Docker Commands

```bash
docker image ls
```

```bash
docker ps
```

```bash
docker ps -a
```

```bash
docker build -t lmsimage .
```

```bash
docker run -d -p 7089:8080 --name lmcontainer lmsimage
```

```bash
docker stop lmcontainer
```

```bash
docker start lmcontainer
```

```bash
docker rm lmcontainer
```

```bash
docker rmi lmsimage
```

```bash
docker login
```

```bash
docker tag lmsimage YOURUSERNAME/lmsimage:latest
```

```bash
docker push YOURUSERNAME/lmsimage:latest
```

```bash
docker pull YOURUSERNAME/lmsimage:latest
```

---

# 29. Full Exam Workflow

This is the **main thing to memorize**:

### Step 1 — Maven

```bash
mvn clean
mvn compile
mvn test
mvn clean package
```

Check:

```text
target/LMSWEBP.war
```

### Step 2 — Git

```bash
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/YOURUSERNAME/LMSWEBP.git
git push -u origin main
```

### Step 3 — Docker

```bash
docker build -t lmsimage .
```

```bash
docker run -d -p 7089:8080 --name lmcontainer lmsimage
```

Open:

```text
http://localhost:7089/
```

### Step 4 — Docker Hub

```bash
docker login
```

```bash
docker tag lmsimage YOURUSERNAME/lmsimage:latest
```

```bash
docker push YOURUSERNAME/lmsimage:latest
```

---

# 30. One-Line Mental Map

Memorize this:

```text
CODE
 ↓
MAVEN
 ↓
WAR
 ↓
GIT
 ↓
GITHUB
 ↓
DOCKER IMAGE
 ↓
CONTAINER
 ↓
localhost:7089
```

And the **3 commands you absolutely cannot forget**:

```bash
mvn clean package
```

```bash
git add . && git commit -m "first commit"
```

```bash
docker run -d -p 7089:8080 --name lmcontainer lmsimage
```
