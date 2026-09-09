# LMSWEBP - Maven Practice Project

This is an intentionally incomplete Maven Java Web project for lab/exam practice.

## Tasks to complete

1. Complete/fix `pom.xml`
2. Add required Maven dependencies
3. Configure WAR packaging
4. Add Maven build plugins
5. Complete the Java Servlet/application
6. Run Maven commands
7. Generate the WAR in `target/`
8. Complete the Dockerfile
9. Build a Docker image
10. Run the container
11. Push the project to GitHub

## Maven commands to practice

mvn clean
mvn compile
mvn test
mvn package
mvn clean package

## Docker commands to practice

docker image ls
docker ps -a
docker build -t lmsimage .
docker run -d -p 7089:8080 --name lmcontainer lmsimage
docker stop lmcontainer
docker start lmcontainer
docker rm lmcontainer
docker login
docker push <username>/lmsimage:latest

## Git commands to practice

git init
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/LMSWEBP.git
git push -u origin main
# se-prac1
