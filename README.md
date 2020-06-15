
# ✨ Building Microservice for Apache Cassandra™ ✨

[![Gitpod ready-to-code](https://img.shields.io/badge/Gitpod-ready--to--code-blue?logo=gitpod)](https://gitpod.io/#https://github.com/DataStax-Academy/microservices-java-workshop-online) 
[![License Apache2](https://img.shields.io/hexpm/l/plug.svg)](http://www.apache.org/licenses/LICENSE-2.0)
[![Discord](https://img.shields.io/discord/685554030159593522)](https://discord.com/widget?id=685554030159593522&theme=dark)

*"In this repository, you'll find everything you need related to the **Cassandra Developer Workshop Build Java Microservices for Apache Cassandra**. [The first live stream will be June 17th](https://www.youtube.com/watch?v=KAcZg6l9QTw). Past this date the `README.MD` will be updated with the recording. Feel free to bookmark this page for future reference, Enjoy"!* - The Developer Advocates Team.

![SplashScreen](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/splash.png?raw=true)

`Cassandra Developer Workshorp` are an interactive experiences. Advocates share some knowledge about  Apache Cassandra™ database and you can interact with them through chats *([youtube](https://www.youtube.com/channel/UCAIQY251avaMv7bBv5PCo-A) and [discord](https://discord.com/widget?id=685554030159593522&theme=dark))*, quizzes (menti.com), and  exercises.

We will create a 

# Table of Content
For simplicity all exercises instructions are listed in a single `README.MD` document. As it is quite long we provide you a table of content is provided and after each chapter you can go back to it.

| Sections  | Material Description
|---|---|
| **Slide deck** | [Slidedeck for the workshop](4-materials/presentation.pdf) |
| **1. Bootstrapping** | [Setup your environment](4-materials/presentation.pdf) |
| **2. Run the Todo Application** | [Exercise 2](#exercise-1---create-your-astra-instance) |
| **3. Create your Astra instance** | [Exercise 3](#exercise-2----create-the-data-model) |
| **4. Connectivity to Astra** | [Connectivity to Cassandra](#exercise-3----connectivity-to-cassandra) |
| **5. CRUD Repository** | [Implement CRUD Repository](#exercise-4----implement-crud-repository) |
| **5. CRUD Repository Object Mapper** | [Run and Test the API](#exercise-5---run-and-test-the-api) |
| **6. CRUD Repository Spring Data** | [Spring DATA](#exercise-6---spring-data) |
| **7. Going Reactive** | [Spring Webflux](#exercise-7---spring-webflux) |

## 1. Bootstrapping

There are 2 ways to do the exercises, **locally** on your computer and with a **cloud-based IDE named Gitpod.** We recommend you to use your laptop in order to save code modifications and come back later. In both cases you should start by cloning the repository and download everything (including slides).

### Option A - Work with a 100% Cloud-based Environment ☁️

**✅ Open gitpod** : [Gitpod](https://www.gitpod.io/) is an IDE 100% online based on Eclipse Theia. To initialize your environment simply click on the button below.

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/DataStax-Academy/microservices-java-workshop-online)

A new tab opens in your browser at  `https://<your_uid>.<your_region>.gitpod.io/#/workspace/microservices-java-workshop-online`. Those URL are dynamic and we cannot provide clickable links in advance. You should copy-paste `<your_uid>.<your_region>` as we will insert them in each URL  during the exercises.

**👁️ Expected output**
![SplashScreen](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/gitpod-home.png?raw=true)

**That's it.** Gitpod provides all tools we will need for today including `Maven` and exporting port `8080`. At initialization of the workspace we schedule a `mvn clean install` to download dependencies. You can still download the repository and bookmark it as all materials including slides are part of it.

### Option B - Work with Local Environment 💻

This part is dedicated to people will to run the exercises on their laptop. You can skip it and directly go to [2. Run the Todo Application](#) if you want to work with gitpod.

**✅ Clone the repository :** : With `git` or through the web UI clone the repo
```bash
# Clone the current repository
git clone https://github.com/DataStax-Academy/microservices-java-workshop-online.git

# Access the proper folder
cd microservices-java-workshop-online
```

**✅ Install Java (JDK8+)** Pick the proper infos based on your operating system
- ![Windows](https://github.com/DataStax-Academy/kubernetes-workshop-online/blob/master/4-materials/images/windows32.png?raw=true) Please use the following tutorial [Installation of the JDK on Microsoft Windows Platforms](https://docs.oracle.com/en/java/javase/11/install/installation-jdk-microsoft-windows-platforms.html#GUID-A7E27B90-A28D-4237-9383-A58B416071CA)
- ![linux](https://github.com/DataStax-Academy/kubernetes-workshop-online/blob/master/4-materials/images/linux32.png?raw=true) Please use the following tutorial [Installation of the JDK on Linux Platform Platforms](https://docs.oracle.com/en/java/javase/11/install/installation-jdk-linux-platforms.html#GUID-737A84E4-2EFF-4D38-8E60-3E29D1B884B8)
- ![osx](https://github.com/DataStax-Academy/kubernetes-workshop-online/blob/master/4-materials/images/mac32.png?raw=true) Please use the following tutorial [Installation of the JDK on MACOS Platforms](https://docs.oracle.com/en/java/javase/11/install/installation-jdk-macos.html#GUID-2FE451B0-9572-4E38-A1A5-568B77B146DE) or with [homebrew](https://docs.brew.sh/Installation):
```bash
brew cask install java
```

**✅ Install Maven**
- ![Windows](https://github.com/DataStax-Academy/kubernetes-workshop-online/blob/master/4-materials/images/windows32.png?raw=true) Please use the following tutorial [How to install Maven on Windows](#https://mkyong.com/maven/how-to-install-maven-in-windows/)
- ![linux](https://github.com/DataStax-Academy/kubernetes-workshop-online/blob/master/4-materials/images/linux32.png?raw=true). For CentOS you can use: `sudo yum install maven`
- ![osx](https://github.com/DataStax-Academy/kubernetes-workshop-online/blob/master/4-materials/images/mac32.png?raw=true) For MacOS you can use `brew install maven`

Validate installation
```bash
mvn -v
```

**👁️ Expected output**
```bash
Apache Maven 3.6.0 (97c98ec64a1fdfee7767ce5ffb20918da4f719f3; 2018-10-24T20:41:47+02:00)
Maven home: /usr/local/Cellar/maven/3.6.0/libexec
Java version: 12, vendor: Oracle Corporation, runtime: /Library/Java/JavaVirtualMachines/openjdk-12.jdk/Contents/Home
Default locale: en_FR, platform encoding: UTF-8
OS name: "mac os x", version: "10.15.3", arch: "x86_64", family: "mac"
```

**✅ Install an IDE**

Pick and install your favourite Java IDE. Here are some propositions without preference order.

| Tools  | Download link
|---|---|
| **Eclipse STS** | 📥[Download Eclipse Spring Tools Suite](https://spring.io/tools#main)
| **Jetbrains IntelliJ** | 📥[Download IntelliJ](https://www.jetbrains.com/idea/download/index.html)
| **Core Eclipse** | 📥[Download Eclipse](https://www.eclipse.org/downloads/)
| **Visual Studio Code** | 📥[Downlowd Visual Code](https://code.visualstudio.com/Download)

**✅ Install Docker** (=not for today, to run Cassandra Locally)

Docker is an open-source project that automates the deployment of software applications inside containers by providing an additional layer of abstraction and automation of OS-level virtualization on Linux.

- ![Windows](https://github.com/DataStax-Academy/kubernetes-workshop-online/blob/master/4-materials/images/windows32.png?raw=true) : To install on **windows** please use the following installer [Docker Dekstop for Windows Installer](https://download.docker.com/win/stable/Docker%20Desktop%20Installer.exe)

- ![osx](https://github.com/DataStax-Academy/kubernetes-workshop-online/blob/master/4-materials/images/mac32.png?raw=true) : To install on **MAC OS**  use [Docker Dekstop for MAC Installer](https://download.docker.com/mac/stable/Docker.dmg) or [homebrew](https://docs.brew.sh/Installation) with following commands:
```bash
# Fetch latest version of homebrew and formula.
brew update              
# Tap the Caskroom/Cask repository from Github using HTTPS.
brew tap caskroom/cask                
# Searches all known Casks for a partial or exact match.
brew search docker                    
# Displays information about the given Cask
brew cask info docker
# Install the given cask.
brew cask install docker              
# Remove any older versions from the cellar.
brew cleanup
# Validate installation
docker -v
```

- ![linux](https://github.com/DataStax-Academy/kubernetes-workshop-online/blob/master/4-materials/images/linux32.png?raw=true) : To install on linux (centOS) you can use the following commands
```bash
# Remove if already install
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
# Utils
sudo yum install -y yum-utils

# Add docker-ce repo
sudo dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo
# Install
sudo dnf -y  install docker-ce --nobest
# Enable service
sudo systemctl enable --now docker
# Get Status
systemctl status  docker

# Logout....Lougin
exit
# Create user
sudo usermod -aG docker $USER
newgrp docker

# Validation
docker images
docker run hello-world
docker -v
```

**✅ Install Docker Compose** (=not for today, to run Cassandra Locally)

Docker Compose is a tool for defining and running multi-container Docker applications. It uses YAML files to configure the application's services and performs the creation and start-up process of all the containers with a single command. The `docker-compose` CLI utility allows users to run commands on multiple containers at once, for example, building images, scaling containers, running containers that were stopped, and more. Please refer to [Reference Documentation](https://docs.docker.com/compose/install/) if you have for more detailed instructions.

- ![Windows](https://github.com/DataStax-Academy/kubernetes-workshop-online/blob/master/4-materials/images/windows32.png?raw=true) : Already **included** in the previous package *Docker for Windows*

- ![osx](https://github.com/DataStax-Academy/kubernetes-workshop-online/blob/master/4-materials/images/mac32.png?raw=true) : Already **included** in the previous package *Docker for Mac*

- ![linux](https://github.com/DataStax-Academy/kubernetes-workshop-online/blob/master/4-materials/images/linux32.png?raw=true) : To install on linux (centOS) you can use the following commands

```bash
# Download deliverable and move to target location
sudo curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

# Allow execution
sudo chmod +x /usr/local/bin/docker-compose
```

[🏠back to table of content](#table-of-content)

## 2. Run the Todo Application

**TodoMVC** is a fabulous community contribution that helps developers compare frameworks on the basis of actual project code, not just claims and anecdotes. Michael Mahemoff. TodoMVC is an immensely valuable attempt at a difficult problem - providing a structured way of comparing JS libraries and frameworks.

![TodoMVC](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/todomvc.png?raw=true)

**✅ Test todoMVC application** : Access the [http://todomvc.com/](http://todomvc.com/) website and test one application with the framework of your choice.

**Todo-Backend** is a shared example to showcase backend tech stacks. The Todo-Backend project defines a simple web API spec - for managing a todo list. Contributors implement that spec using various tech stacks. Those implementations are cataloged below. A spec runner verifies that each contribution implements the exact same API, by running an automated test suite which defines the API.

![TodoBackend](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/todobackend.png?raw=true)

There are multiple free implementations available already. Some implementations provide endpoints to be tested in `heroku`. [Heroku provide free hosting for a Java application but this is on-demand](https://devcenter.heroku.com/articles/deploying-spring-boot-apps-to-heroku). With `Heroku` The application will be sleeping until you access the endpoint. So it will take 30s for the first person to have the application running. Among the available free endpoints we can list:
- `Endpoint#1` : [https://todo-back-springboot220-java12.herokuapp.com/todos](https://todo-back-springboot220-java12.herokuapp.com/todos)
- `Endpoint#2` : [https://todo-quarkus.herokuapp.com/todos](https://todo-quarkus.herokuapp.com/todos)
- `Endpoint#3` : [https://todo-backend-micronaut.herokuapp.com/todos](https://todo-backend-micronaut.herokuapp.com/todos)

**TodoBackend.com** provides a we bUI [spec runner](https://www.todobackend.com/specs/index.html) to test APIs against specifications. 

**✅ Test TodoBackEnd Spec Runner** : Use one of the `endpoints` decribed below to evaluate if the API matchs the requirements and `Run Tests`

![TodoBackendTest](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/todobackend-runtest.png?raw=true)

**👁️ Expected output**

![TodoBackendOuput](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/todobackend-output-host.png?raw=true)

**Note:** *During the live stream you will be hundreds testing the same endpoints so - maybe - we could hit some issues = race conditions.*

**✅ Test TodoBackEnd SCClient** : todoBackend.com provides a [client](https://www.todobackend.com/client/index.html) to work with the API. As before pick one of the `endpoints` listed before and try the client.

![TodoBackendClient](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/todobackend-runclient.png?raw=true)

**👁️ Expected output**

![TodoBackendClient](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/todobackend-output-client.png?raw=true)

Our mission withing the next hour is to implement the *backend API* and store  data into Apache Cassandra™. We have you covered by providing the skeleton of the application.

**✅ Start Backend API** : By using a maven command or run application in your IDE

```bash
# Build the project without tests (you did not implemented them yet TDD baby !)
mvn clean install -Dmaven.test.skip=true

# Navigate to the proper folder
cd wkshop-microservice-2-spring-boot/

# Start the backend API
mvn spring-boot:run
```

**👁️ Expected output**

```bash
[...]
INFO] ------------------------------------------------------------------------
[INFO] Reactor Summary for Spring microservices with Apache Cassandra 1.0-SNAPSHOT:
[INFO] 
[INFO] Spring microservices with Apache Cassandra ......... SUCCESS [  4.115 s]
[INFO] + microservice-1-common ............................ SUCCESS [  8.893 s]
[INFO] + microservice-2-spring-boot ....................... SUCCESS [  3.504 s]
[INFO] + microservice-3-spring-data ....................... SUCCESS [  1.369 s]
[INFO] + microservice-4-spring-webflux .................... SUCCESS [  0.311 s]
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  18.701 s
[INFO] Finished at: 2020-06-15T13:08:57Z
[INFO] ------------------------------------------------------------------------
```

```bash
 ________                __      __ __           .__                   
 \______ \   _______  __/  \    /  \  | __  _____|  |__   ____ ______  
  |    |  \_/ __ \  \/ /\   \/\/   /  |/ / /  ___/  |  \ /  _ \\____ \ 
  |    `   \  ___/\   /  \        /|    <  \___ \|   Y  (  <_> )  |_> >
 /_______  /\___  >\_/    \__/\  / |__|_ \/____  >___|  /\____/|   __/ 
         \/     \/             \/       \/     \/     \/       |__|    

 Backend API implementation of todobackend.com
 We are using SpringBoot and Apache Cassandra
 The application is started at http://localhost:8080  

14:54:54.773 INFO  com.datastax.sample.TodoBackendApplication         : Starting TodoBackendApplication on clunhost with PID 75757 (/Users/cedricklunven/dev/WORKSPACES/DATASTAX/microservices-java-workshop-online/wkshop-microservice-2-spring-boot/target/classes started by cedricklunven in /Users/cedricklunven/dev/WORKSPACES/DATASTAX/microservices-java-workshop-online/wkshop-microservice-2-spring-boot)
14:54:54.775 INFO  com.datastax.sample.TodoBackendApplication         : No active profile set, falling back to default profiles: default
14:55:03.604 INFO  com.datastax.sample.TodoBackendApplication         : Started TodoBackendApplication in 1.075 seconds (JVM running for 1.492)
```

**✅ Show Api Documentation** : through your browser

- 💻 If you are on your **laptop** : open a browser and navigate to [http://localhost:8080](http://localhost:8080)

- ☁️ If you are on **gitpod** : a popup may show up and redirect you to `https://8080-<your_id>.<>your_region.gitpod.io` as you can see this an alias for port `8080`.

**📗 Expected output**

![TodoBackendClient](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/backend-doc.png?raw=true)

You can open the `GET` command `/api/v1/todos` and execute `Try Out` to test the API live and get the result.

📘 **Execute tests against the API**

This REST API works **In memory** but is 100% valid. We can be sure of it by running the same test suite as before.

- If you are on your **laptop** open a browser and navigate to [https://www.todobackend.com/specs/index.html?http://localhost:8080/api/v1/todos](https://www.todobackend.com/specs/index.html?http://localhost:8080/api/v1/todos)
- If you are on **gitpod** : a popup may show up and redirect you to `https://8080-<your_id>.<>your_region.gitpod.io/api/v1/todos`.

**📗 Expected output**

![TodoBackendClient](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/realbackend-test.png?raw=true)

📘 **All together**

Back the client UI change the URL to match you backend URL :
- If your work locally : [https://www.todobackend.com/client/index.html?http://localhost:8080/api/v1/todos](https://www.todobackend.com/client/index.html?http://localhost:8080/api/v1/todos)
- If you are using gitpod `https://www.todobackend.com/client/index.html?https://8080-<your_id>.<your_region>-eu01.gitpod.io/api/v1/todos`

**📗 Expected output**

![TodoBackendClient](https://github.com/DataStax-Academy/microservices-java-workshop-online/blob/master/z-materials/images/backend-ok.png?raw=true)

*Ok I changed a little bit the values but now this is working. This is neat, the client and spec runner both work even with URL like localhost because this is javascript code executed at client side.* 

[🏠back to table of content](#table-of-content)

## 3. Create your Astra instance

[🏠back to table of content](#table-of-content)

## 4. Connectivity to Astra

[🏠back to table of content](#table-of-content)

## 5. CRUD Repository

[🏠back to table of content](#table-of-content)

## 6. CRUD Repository with Object Mapper
 
[🏠back to table of content](#table-of-content)

## 7. CRUD Repository with Spring Data

[🏠back to table of content](#table-of-content)

## 8. Going Reactive

```
XXX
```

[🏠back to table of content](#table-of-content)

## Exercise 3 -  Connectivity to Cassandra

Do X Y Z

```
XXX
```

[🏠back to table of content](#table-of-content)

## Exercise 4 -  Implement CRUD Repository

Do X Y Z

```
XXX
```

[🏠back to table of content](#table-of-content)

## Exercise 5 - Run and Test the API

Do X Y Z

```
XXX
```

[🏠back to table of content](#table-of-content)

## Exercise 6 - Spring DATA

Do X Y Z

```
XXX
```

[🏠back to table of content](#table-of-content)

## Exercise 7 - Spring Webflux

Do X Y Z

```
XXX
```

[🏠back to table of content](#table-of-content)


THE END.





