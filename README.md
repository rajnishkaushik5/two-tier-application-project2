#...........................................................
# Project 2: Containerization of a Two-Tier Application using Docker, Docker Compose, and Image Scanning with Docker Scout

Tools Required:
Docker: For creating and managing containers.
Docker Compose: For defining and running multi-container Docker applications.
Docker Scout: For Scanning Docker images for vulnerabilities.
Any code editor (like Visual Studio Code, Atom, etc.)
Access to a basic two-tier application source code (e.g., a simple web app with a database backend).
Overview/Description:
This project involves containerizing a two-tier application (such as a web application with a database) using Docker and orchestrating the containers using Docker Compose. The project will also include using Docker Scout to scan the created Docker images for security vulnerabilities. 
This will give practical experience in containerization, orchestration, and security aspects of Dockerized applications.
Code Repository:
Repository Platform: GitHub
Repository Link: https://github.com/rajnishkaushik5/two-tier-application-project2.git
Access Instructions: Clone the repository to your local machine using Git. Instructions on cloning a repository can be found on GitHub's help pages.
Requirements:
Functional Requirements:
Containerize each component of the two-tier application using Docker.
Use Docker Compose to define and run the multi-container application.
Ensure network communication between containers (e.g., web app container communicating with the database container).
Scan the Docker images with Docker Scout and address any reported vulnerabilities.
Non-Functional Requirements:
Performance: The containers should be optimized for performance, considering aspects like image size and startup time.
Security: Implement best practices for Docker security, including managing secrets and using least privilege principles.
Documentation: Provided steps into this README file with clear instructions on how to build, run, and scan the application.
In this Project, I Successfully containerised a two-tier application using Docker and orchestrated the deployment with Docker Compose. 
Gained expertise in Docker image creation, and management, and performed vulnerability scanning using Docker Scout. 
This project enhanced my understanding of containerization, network communication between containers, and security practices in Docker environments.

#....................................................................

step 1:
*launch an EC2 instance --> t2.micro, ami:ubuntu, security group rules:22,80,5000
* ssh into instance

step 2:
update system packages and install docker.io in home dir
commands:
$sudo apt-get update
$sudo apt-get install docker.io

step 3:
get access to docker daemon by user
$sudo chown $USER /var/run/docker.sock

step 4:
install docker-compose tool
$sudo apt  install docker-compose 

step 5:
clone repo into local dir "my-project"
$git clone <url of repo>

step 6:
write a Dockerfile for backend;
no need to write a Dockerfile for mysql database instead use its base image "mysql:5.7"

step 7:
write a docker-compose.yml file to run both services(2-containers one for backend
and another for database)simultaneously,
to create a common network,and to mount a volume to database;
command:
$docker-compose up -d (it created 2-containers in one shot; d=detached mode) 
$docker ps (show both containers)
$docker network ls (show all network)
$docker volume ls  (show a volume created by docker-compose locally)

step 8 :
go to google ---> search "localhost:5000"
it show your web frontend+backend with live database;

step 9:
enter into container,command is
$docker exec -it <container id> bash
$ls --> show "docker-entrypoint-initdb.d/message.sql" dir in which my sql script is run

step 10:
enter into mysql container,the command is,
$mysql -u root -p
enter password : root

$show databases;
$use KYC;  --> KYC is my database created by user in which all data is stored from web
$show tables;  ---> its shows table name "messages"
$SHOW COLUMNS from messages; ---> show name of row and columns
$select * from messages; ---> shows all entry made to web 
$insert into messages (message) value ("enter any value")--> add a new entry into db shows at web

*any entry add to web shows in db and any entry add to db it show on web
 
step 11:
install docker scout in home dir to scan images for vulnerability:
a)1st go home dir
b)$mkdir .docker   ---> create a hidden dir
c)cd .docker/
d)$mkdir cli-plugins/
e)cd cli-plugins/
f)curl -sSfL https://raw.githubusercontent.com/docker/scout-cli/main/install.sh | sh -s --
g)/home/ubuntu/.docker/cli-plugins/docker-scout  --> path of docker-scout
i) $docker scout version

step 12:
inorder to use docker scout, 1st you have to login into your dockerHub account
$docker login
> username:
> password:
"login succeeded"

step 13:
command: to scan image
$docker scout quickview <image:tag>
$docker scout cves <image:tag>
$docker scout cves -o <image:tag>  ---> create a report of your scan 


step 14:
deleted resources:
$docker-compose down       ----> it remove all resources created by docker-compose.yml

$docker-compose up -d      ----> resources are created again

*terminate EC2 instance

# ..............................................



