
Name: Thuong Pham

Student ID: 1002155359

---

# Project 1: Docker

## Question 1: About Docker Tutorial

- link to Q1 shared image: [https://hub.docker.com/r/lucypham951/getting-started/tags](https://hub.docker.com/r/lucypham951/getting-started/tags)

---
### Build Image and Run Container
<details><summary>view record</summary>
- After write the Dockerfile, we build an image based on it

```
$ date; whoami; docker build -t getting-started .
Mon Feb 12 19:24:02 CST 2024
lucypham
[+] Building 0.6s (12/12) FINISHED                                 docker:desktop-linux
 => [internal] load build definition from Dockerfile                               0.0s
 => => transferring dockerfile: 258B                                               0.0s
 => resolve image config for docker.io/docker/dockerfile:1                         0.4s
 => CACHED docker-image://docker.io/docker/dockerfile:1@sha256:ac85f380a63b13dfce  0.0s
 => [internal] load metadata for docker.io/library/node:18-alpine                  0.0s
 => [internal] load .dockerignore                                                  0.0s
 => => transferring context: 52B                                                   0.0s
 => [1/5] FROM docker.io/library/node:18-alpine                                    0.0s
 => [internal] load build context                                                  0.0s
 => => transferring context: 4.60kB                                                0.0s
 => CACHED [2/5] WORKDIR /app                                                      0.0s
 => CACHED [3/5] COPY package.json yarn.lock ./                                    0.0s
 => CACHED [4/5] RUN yarn install --production                                     0.0s
 => CACHED [5/5] COPY . .                                                          0.0s
 => exporting to image                                                             0.0s
 => => exporting layers                                                            0.0s
 => => writing image sha256:0cba7957d22a7494b13e2496887a8a5fa502562cf93c826366201  0.0s
 => => naming to docker.io/library/getting-started                                 0.0s

View build details: docker-desktop://dashboard/build/desktop-linux/desktop-linux/14uc4um9w1f3px28xbkgy066n

What's Next?
  View a summary of image vulnerabilities and recommendations → docker scout quickview
```


- start a container with the constructed image
```
$ date; whoami; docker run -dp 127.0.0.1:3000:3000 getting-started
Mon Feb 12 19:25:24 CST 2024
lucypham
0b4d0e1d4daf5d2331c2de4b6c2ce020562ee96ee3e503002119aa6fce85dc35
```

- track status of running containers

```
date; whoami; docker ps                                          
Mon Feb 12 19:25:51 CST 2024
lucypham
CONTAINER ID   IMAGE             COMMAND                  CREATED          STATUS          PORTS                      NAMES
0b4d0e1d4daf   getting-started   "docker-entrypoint.s…"   27 seconds ago   Up 26 seconds   127.0.0.1:3000->3000/tcp   suspicious_faraday
```
![](<screenshots/Screenshot 2024-02-11 at 10.30.15 PM.png>)

</details>


### Update Docker Application

<details><summary>view record</summary>

- After modify the content of the application (change printout), we close old container; rebuild image and run new container

```
# delete old container
$ docker rm -f 0b4d0e1d4daf;
0b4d0e1d4daf

# rebuild image and rerun container
$  date; whoami; docker build -t getting-started . ; docker run -dp 127.0.0.1:3000:3000 getting-started
Mon Feb 12 19:28:08 CST 2024
lucypham
[+] Building 0.9s (13/13) FINISHED                                 docker:desktop-linux
 => [internal] load build definition from Dockerfile                               0.0s
 => => transferring dockerfile: 258B                                               0.0s
 => resolve image config for docker.io/docker/dockerfile:1                         0.8s
 => [auth] docker/dockerfile:pull token for registry-1.docker.io                   0.0s
 => CACHED docker-image://docker.io/docker/dockerfile:1@sha256:ac85f380a63b13dfce  0.0s
 => [internal] load metadata for docker.io/library/node:18-alpine                  0.0s
 => [internal] load .dockerignore                                                  0.0s
 => => transferring context: 52B                                                   0.0s
 => [1/5] FROM docker.io/library/node:18-alpine                                    0.0s
 => [internal] load build context                                                  0.0s
 => => transferring context: 4.60kB                                                0.0s
 => CACHED [2/5] WORKDIR /app                                                      0.0s
 => CACHED [3/5] COPY package.json yarn.lock ./                                    0.0s
 => CACHED [4/5] RUN yarn install --production                                     0.0s
 => CACHED [5/5] COPY . .                                                          0.0s
 => exporting to image                                                             0.0s
 => => exporting layers                                                            0.0s
 => => writing image sha256:0cba7957d22a7494b13e2496887a8a5fa502562cf93c826366201  0.0s
 => => naming to docker.io/library/getting-started                                 0.0s

View build details: docker-desktop://dashboard/build/desktop-linux/desktop-linux/5whkafhv43iltoh64pq0x0daq

What's Next?
  View a summary of image vulnerabilities and recommendations → docker scout quickview
385838ddb14556debfe6cb87f61453ca9b2ee14db9722dbc8c528f411974ddf8
```
![No item yet--> You have no todo items yet](<screenshots/Screenshot 2024-02-11 at 10.40.29 PM.png>)

- close the container
```
date; whoami; docker rm -f 385838ddb145
Mon Feb 12 19:35:35 CST 2024
lucypham
385838ddb145
```
</details>

### Share an application

<details><summary>view record</summary>

- tag the current image to be the repository image, then push the image to the public repository

```
$ docker login -u lucypham951                                                                            Password: 
Login Succeeded

$ docker tag getting-started lucypham951/getting-started

$ docker push lucypham951/getting-started

```

- build a new image based on the old one but able to run on different platform: Linux AMD64

```
$ date; whoami; docker build --platform linux/amd64 -t lucypham951/getting-started .
Mon Feb 12 19:42:02 CST 2024
lucypham
[+] Building 17.4s (14/14) FINISHED                                docker:desktop-linux
 => [internal] load build definition from Dockerfile                               0.0s
 => => transferring dockerfile: 258B                                               0.0s
 => resolve image config for docker.io/docker/dockerfile:1                         0.6s
 => [auth] docker/dockerfile:pull token for registry-1.docker.io                   0.0s
 => CACHED docker-image://docker.io/docker/dockerfile:1@sha256:ac85f380a63b13dfce  0.0s
 => [internal] load metadata for docker.io/library/node:18-alpine                  0.5s
 => [auth] library/node:pull token for registry-1.docker.io                        0.0s
 => [internal] load .dockerignore                                                  0.0s
 => => transferring context: 52B                                                   0.0s
 => [1/5] FROM docker.io/library/node:18-alpine@sha256:0085670310d2879621f96a4216  0.0s
 => [internal] load build context                                                  0.0s
 => => transferring context: 4.60kB                                                0.0s
 => CACHED [2/5] WORKDIR /app                                                      0.0s
 => [3/5] COPY package.json yarn.lock ./                                           0.0s
 => [4/5] RUN yarn install --production                                           15.4s
 => [5/5] COPY . .                                                                 0.0s 
 => exporting to image                                                             0.7s 
 => => exporting layers                                                            0.7s 
 => => writing image sha256:fc9ad607dab4cd9ff2ee22c15fb67df4cf914f90638d20ec16ded  0.0s 
 => => naming to docker.io/lucypham951/getting-started                             0.0s 
                                                                                        
View build details: docker-desktop://dashboard/build/desktop-linux/desktop-linux/qw21r6q4dslswiiwt9uk5aed7

What's Next?
  View a summary of image vulnerabilities and recommendations → docker scout quickview
```

- push the new image to the Docker repository so we can share to different device

```
$ date; whoami; docker push lucypham951/getting-started 
Mon Feb 12 19:43:45 CST 2024
lucypham
Using default tag: latest
The push refers to repository [docker.io/lucypham951/getting-started]
e052abc78ba6: Pushed 
32c9c7bc2b58: Pushed 
574afb127953: Pushed 
686c8b2b7170: Layer already exists 
b325b33b9813: Layer already exists 
4a0d315ad53e: Layer already exists 
29e213bad130: Layer already exists 
d4fc045c9e3a: Layer already exists 
latest: digest: sha256:ac4abfcc13a11a158b1c832d117f546154bdc9d1b08a00f82bba988bcc860851 size: 1996
```

- open "Play with Docker", create a instance to interact with this image
```
# in the AMD64 instance, build a container base on the shared image
$ docker run -dp 0.0.0.0:3000:3000 lucypham951/getting-started

# then open port 3000 to see the front end of the running container
```
![Play with Docker's instance](<screenshots/Screenshot 2024-02-11 at 10.57.22 PM.png>)

![Play with Docker's deployed frontend](<screenshots/image.png>)

- close session afterward

</details>

### Shared Database: Persist mount

<details><summary>view record</summary>

- Start an ubuntu container that will create a file named /data.txt with a random number between 1 and 10000.

```
$ docker run -d ubuntu bash -c "shuf -i 1-10000 -n 1 -o /data.txt && tail -f /dev/null"
ed6ac95af796ddf51c62c6d8e9875d50446ad7ab66d0b954415a8ff1990b3ea7
```

- check status of container(s)
```
docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS     NAMES
ed6ac95af796   ubuntu    "bash -c 'shuf -i 1-…"   49 seconds ago   Up 48 seconds             sleepy_keldysh
```

- Look at the data.txt file created inside that container (return a random number)

```
docker exec ed6ac95af796 cat /data.txt
8182
```

- Create a new interactive ubuntu container to confirm that we cannot not see that /data.txt file since they are isolated environment

```
docker run -it ubuntu ls /
bin  boot  dev  etc  home  lib  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
# no data.txt found --> confirmed
```

- close container
```
$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS     NAMES
ed6ac95af796   ubuntu    "bash -c 'shuf -i 1-…"   4 minutes ago   Up 4 minutes             sleepy_keldysh

$ docker rm -f ed6ac95af796
```

- Now, we create a shared volume on host

```
$ docker volume create todo-db
todo-db
```

- run a container that is linked to the shared volume

```
$ docker run -dp 127.0.0.1:3000:3000 --mount type=volume,src=todo-db,target=/etc/todos getting-started
dedc04a4960142abdcec7fd2a1eb2d2eaa0211ccaade5a2d7637db007af4a251
```

- After adding some items in the todo list, kill the running container
```
$ docker rm -f dedc04a49601
dedc04a49601
```

- We expect the changes is saved in the shared volume even after the container is killed. Hence starting another container still see the those changes.

```
$ docker run -dp 127.0.0.1:3000:3000 --mount type=volume,src=todo-db,target=/etc/todos getting-started
b412807478805d07f0cecfacbcd7932ac3bcd81fcbbc2e0d61d84b4ef33e6c53
```

- Open port 3000, same as where we left off. Also confirming by inspecting the volume

```
We can also check what is saved in the volume todo-db
» docker volume inspect todo-db                                                                               1 ↵
[
    {
        "CreatedAt": "2024-02-12T05:15:27Z",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/todo-db/_data",
        "Name": "todo-db",
        "Options": null,
        "Scope": "local"
    }
]
```

</details>

### Shared Database: bind mounts

<details><summary>view record</summary>

- start an interactive bash in ubuntu with bind mount at location: /src

```
$ docker run -it --mount type=bind,src="$(pwd)",target=/src ubuntu bash
root@ea424dd803f8:/# pwd
/
root@ea424dd803f8:/# ls
bin  boot  dev  etc  home  lib  media  mnt  opt  proc  root  run  sbin  src  srv  sys  tmp  usr  var
```

- In the container: cd to the mounted target and make change so that we can observe the corresponding change in the host

```
root@ea424dd803f8:/# cd /src
root@ea424dd803f8:/src# ls
Dockerfile  README.md  package.json  spec  src  yarn.lock
root@ea424dd803f8:/src# touch myfile.txt
```

- In the host, we found the file that we created inside container

```
$ ls -rlth
total 312
-rw-r--r--  1 lucypham  staff   269B Feb 11 22:17 README.md
-rw-r--r--  1 lucypham  staff   648B Feb 11 22:17 package.json
-rw-r--r--  1 lucypham  staff   144K Feb 11 22:17 yarn.lock
drwxr-xr-x  4 lucypham  staff   128B Feb 11 22:18 spec
-rw-r--r--  1 lucypham  staff   142B Feb 11 22:20 Dockerfile
drwxr-xr-x  6 lucypham  staff   192B Feb 11 22:36 src
-rw-r--r--  1 lucypham  staff     0B Feb 12 00:04 myfile.txt
```
- Delete that file and close container

```
$ rm myfile.txt

$ docker ps
CONTAINER ID   IMAGE             COMMAND                  CREATED          STATUS          PORTS                      NAMES
b41280747880   getting-started   "docker-entrypoint.s…"   48 minutes ago   Up 48 minutes   127.0.0.1:3000->3000/tcp   xenodochial_khorana

$ docker rm -f b41280747880
```

- After experiment with bind mount, we can run our Node app and see if the app change when the shared database is updated

```
# run a container, with bind mount, from image node:18-alpine (pull from docker library since we don't have it locally) and execute shell commands 
$ docker run -dp 127.0.0.1:3000:3000 \
    -w /app --mount type=bind,src="$(pwd)",target=/app \
    node:18-alpine \
    sh -c "yarn install && yarn run dev"
Unable to find image 'node:18-alpine' locally
18-alpine: Pulling from library/node
bca4290a9639: Already exists 
f1740a8d9e06: Already exists 
cc243ad803dd: Already exists 
7fc23bc03008: Already exists 
Digest: sha256:0085670310d2879621f96a4216c893f92e2ded827e9e6ef8437672e1bd72f437
Status: Downloaded newer image for node:18-alpine
d2d84e4e455412b0b0eb1edd32a14892dd5ec6bdd372bb3b61f569c4ec0d935b

# change button name from host's app.js and reload the host without restarting container to see immediate change (thanks for bind mount) --> confirmed button label change from 'Add Item' to 'Add'

```

- finished with bind mount, close container

```
$ docker ps
CONTAINER ID   IMAGE            COMMAND                  CREATED         STATUS         PORTS                      NAMES
d2d84e4e4554   node:18-alpine   "docker-entrypoint.s…"   7 minutes ago   Up 7 minutes   127.0.0.1:3000->3000/tcp   condescending_lalande

$ docker rm -f d2d84e4e4554
d2d84e4e4554
```
</details>

### Run App on multi-containers with SQL

<details><summary>view record</summary>

- create a network to overcome isolation between containers

```
$ docker network create todo-app
e104c990d7beb31fe548eae0b53207dca6bc77b3e7c3c2ed94e51f20ba853b8c
```

- run container 1: MySQL that is linked to todo-app network

```
$ docker run -d \
    --network todo-app --network-alias mysql \
    -v todo-mysql-data:/var/lib/mysql \
    -e MYSQL_ROOT_PASSWORD=secret \
    -e MYSQL_DATABASE=todos \
    mysql:8.0


Unable to find image 'mysql:8.0' locally
8.0: Pulling from library/mysql
0647c03756d6: Pull complete 
7c571053c52e: Pull complete 
d6453741958d: Pull complete 
03e97ad7011a: Pull complete 
65f90da87686: Pull complete 
e34bc5fd6dca: Pull complete 
1aabd0ea8416: Pull complete 
8c7cac6c965c: Pull complete 
0c3b88eb4e54: Pull complete 
21716a23f73a: Pull complete 
275e4950a203: Pull complete 
Digest: sha256:d848240fd25e2bc1c4f1f3a1f0a0f32582871feb0373dfb8203a52f390120e6f
Status: Downloaded newer image for mysql:8.0
5cf9265e050d9c8727b952d88dc18850fb7ed1c44806cb7917508e291e6909c4
```

- check if the container is successfully running by open interactive CLI

```
$docker exec -it 5cf9265e050d mysql -u root -p
Enter password: 

# inside mysql container

Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 8
Server version: 8.0.36 MySQL Community Server - GPL

Copyright (c) 2000, 2024, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| todos              |
+--------------------+
5 rows in set (0.02 sec)

mysql> exit
Bye
```

- Run a second container (interactive) and connect it to the same network. Then check if 2 containers can communicate.

```
$ docker run -it --network todo-app nicolaka/netshoot
Unable to find image 'nicolaka/netshoot:latest' locally
latest: Pulling from nicolaka/netshoot
08409d417260: Pull complete 
ac33bad4dbc8: Pull complete 
923c486e8fbf: Pull complete 
47fe9363a92a: Pull complete 
42db5be59d6c: Pull complete 
15d2d99713c2: Pull complete 
e75fe07ab2d6: Pull complete 
4f4fb700ef54: Pull complete 
aa1e8a00074d: Pull complete 
b13a35cd3e60: Pull complete 
70b9b37f0442: Pull complete 
df18fbfdedba: Pull complete 
aebbe40f073b: Pull complete 
05af46097b85: Pull complete 
404981eb2565: Pull complete 
Digest: sha256:a7c92e1a2fb9287576a16e107166fee7f9925e15d2c1a683dbb1f4370ba9bfe8

...
#
# inside Netshoot container
#

 4b33c7b9755d  ~  dig mysql

; <<>> DiG 9.18.13 <<>> mysql
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 65492
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;mysql.                         IN      A

;; ANSWER SECTION:
mysql.                  600     IN      A       172.18.0.2

;; Query time: 11 msec
;; SERVER: 127.0.0.11#53(127.0.0.11) (UDP)
;; WHEN: Mon Feb 12 06:31:13 UTC 2024
;; MSG SIZE  rcvd: 44
 4b33c7b9755d  ~  exit

```

- Run another second container for the app that link to the mySQL via todo network
``` 
$ docker run -dp 127.0.0.1:3000:3000 \
  -w /app -v "$(pwd):/app" \
  --network todo-app \
  -e MYSQL_HOST=mysql \
  -e MYSQL_USER=root \
  -e MYSQL_PASSWORD=secret \
  -e MYSQL_DB=todos \
  node:18-alpine \
  sh -c "yarn install && yarn run dev"
e6d911df3e3f43b801476e975080a97014699435e7bc046e6badd3314c6a8710
```

- Now modifying the todo list will result in changes in SQL database. Check by open an interactive terminal inside mysql container:

```
$ docker exec -it 0c9b3e1da0f3 mysql -p todos                                                                 1 ↵
Enter password: 
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 12
Server version: 8.0.36 MySQL Community Server - GPL

Copyright (c) 2000, 2024, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> select * from todo_items;
+--------------------------------------+---------+-----------+
| id                                   | name    | completed |
+--------------------------------------+---------+-----------+
| 0d8ee79b-bf82-43a8-b362-8ce297365a48 | hello   |         1 |
| b35a3d0b-4d2f-43ad-8145-d930d52b4b45 | from    |         1 |
| 9a88239f-9934-46c1-b30e-48ad2c96df7f | the     |         0 |
| e750cf6f-9fff-4f7d-a4b6-a095918733cd | darkest |         0 |
| be632b01-c51a-4c56-8932-db4ad238e619 | side    |         0 |
+--------------------------------------+---------+-----------+
5 rows in set (0.00 sec)

```

- finish with bind mount, close containers

``` 
$ docker rm -f 0045df5e156c 0c9b3e1da0f3
0045df5e156c
0c9b3e1da0f3
```

</details>

### Docker Compose: building stack of application

<details><summary>view record</summary>

- Create the compose.yaml file that list all the containers and volumes we want to run. Then compose the stack in the background:

```
$ docker compose up -d
[+] Running 2/4
 ⠼ Network getting-started-app_default           Created                                                                                                                               0.4s 
 ⠸ Volume "getting-started-app_todo-mysql-data"  Created                                                                                                                               0.3s 
 ✔ Container getting-started-app-mysql-1         Started                                                                                                                               0.3s 
 ✔ Container getting-started-app-app-1           Started 
```

- Open port and check if app successfully deployed --> confirm.

- close the running containers and volumes by tear down the composed stack:

```
$ docker compose down --volumes
[+] Running 4/2
 ✔ Container getting-started-app-app-1         Removed                                                                                                                                 0.2s 
 ✔ Container getting-started-app-mysql-1       Removed                                                                                                                                 3.0s 
 ✔ Volume getting-started-app_todo-mysql-data  Removed                                                                                                                                 0.0s 
 ✔ Network getting-started-app_default         Removed 
```

</details>

### Image-building best practices

<details><summary>view record</summary>

- Here's how to check layers of the built image:

```
$ docker image history getting-started
IMAGE          CREATED        CREATED BY                                      SIZE      COMMENT
2a5c1a5593bf   11 hours ago   EXPOSE map[3000/tcp:{}]                         0B        buildkit.dockerfile.v0
<missing>      11 hours ago   CMD ["node" "src/index.js"]                     0B        buildkit.dockerfile.v0
<missing>      11 hours ago   RUN /bin/sh -c yarn install --production # b…   85.2MB    buildkit.dockerfile.v0
<missing>      11 hours ago   COPY . . # buildkit                             6.46MB    buildkit.dockerfile.v0
<missing>      11 hours ago   WORKDIR /app                                    0B        buildkit.dockerfile.v0
<missing>      2 weeks ago    /bin/sh -c #(nop)  CMD ["node"]                 0B        
<missing>      2 weeks ago    /bin/sh -c #(nop)  ENTRYPOINT ["docker-entry…   0B        
<missing>      2 weeks ago    /bin/sh -c #(nop) COPY file:4d192565a7220e13…   388B      
<missing>      2 weeks ago    /bin/sh -c apk add --no-cache --virtual .bui…   7.77MB    
<missing>      2 weeks ago    /bin/sh -c #(nop)  ENV YARN_VERSION=1.22.19     0B        
<missing>      2 weeks ago    /bin/sh -c addgroup -g 1000 node     && addu…   114MB     
<missing>      2 weeks ago    /bin/sh -c #(nop)  ENV NODE_VERSION=18.19.0     0B        
<missing>      2 weeks ago    /bin/sh -c #(nop)  CMD ["/bin/sh"]              0B        
<missing>      2 weeks ago    /bin/sh -c #(nop) ADD file:d0764a717d1e9d0af…   7.73MB 
```

- Now we cache the consistent layers to save building time. This is done by copy package.json before install dependencies to only get neccessary packages. Here is the comparison of before and after doing layer cache:

```
# Before: 8.6 seconds
$ docker build -t getting-started .
[+] Building 8.6s (13/13) FINISHED                                                                                                ...

# After: 0.7 seconds --> much faster
$ docker build -t getting-started .
[+] Building 0.7s (12/12) FINISHED      
...
```

-- Finished Question 1. --


</details>

## Question 2: Building a Python Application


- link for GitHub: [https://github.com/lucypham951/Docker-HW.git](https://github.com/lucypham951/Docker-HW.git)

- link for DockerHub: [https://hub.docker.com/r/lucypham951/docker-hw/tags](https://hub.docker.com/r/lucypham951/docker-hw/tags)

---

### Run Application locally

<details><summary>view record</summary>

- We are given an app.py and a file of dependency requirements. First we create docker related files quickly like this:

```
$ docker init              

Welcome to the Docker Init CLI!

This utility will walk you through creating the following files with sensible defaults for your project:
  - .dockerignore
  - Dockerfile
  - compose.yaml
  - README.Docker.md

Let's get started!

? What application platform does your project use? Python
? What version of Python do you want to use? 3.9.6
? What port do you want your app to listen on? 5000
? What is the command you use to run your app? python3 -m flask run --host=0.0.0.0

CREATED: .dockerignore
CREATED: Dockerfile
CREATED: compose.yaml
CREATED: README.Docker.md

✔ Your Docker files are ready!

Take a moment to review them and tailor them to your application.

When you're ready, start your application by running: docker compose up --build

Your application will be available at http://localhost:5000

Consult README.Docker.md for more information about using the generated files.

```

- <u>Note:</u> My device has port 5000 as system port, hence we need to redirect the port to 3000 instead. This is done by modify the compse.yaml's port from 5000:5000 to 3000:5000.

- Now we build image and compose the stack 

```
docker compose up --build                                                                                        130 ↵
[+] Building 0.8s (12/12) FINISHED                                                                                                                                     docker:desktop-linux
 => [server internal] load build definition from Dockerfile                                                                                                                            0.0s
 => => transferring dockerfile: 1.68kB                                                                                                                                                 0.0s
 => [server] resolve image config for docker.io/docker/dockerfile:1                                                                                                                    0.4s
 => CACHED [server] docker-image://docker.io/docker/dockerfile:1@sha256:ac85f380a63b13dfcefa89046420e1781752bab202122f8f50032edf31be0021                                               0.0s
 => [server internal] load metadata for docker.io/library/python:3.9.6-slim                                                                                                            0.2s
 => [server internal] load .dockerignore                                                                                                                                               0.0s
 => => transferring context: 667B                                                                                                                                                      0.0s
 => [server base 1/5] FROM docker.io/library/python:3.9.6-slim@sha256:4115592fd02679fb3d9e8c513cae33ad3fdd64747b64d32b504419d7118bcd7c                                                 0.0s
 => [server internal] load build context                                                                                                                                               0.0s
 => => transferring context: 98B                                                                                                                                                       0.0s
 => CACHED [server base 2/5] WORKDIR /app                                                                                                                                              0.0s
 => CACHED [server base 3/5] RUN adduser     --disabled-password     --gecos ""     --home "/nonexistent"     --shell "/sbin/nologin"     --no-create-home     --uid "10001"     appu  0.0s
 => CACHED [server base 4/5] RUN --mount=type=cache,target=/root/.cache/pip     --mount=type=bind,source=requirements.txt,target=requirements.txt     python -m pip install -r requir  0.0s
 => CACHED [server base 5/5] COPY . .                                                                                                                                                  0.0s
 => [server] exporting to image                                                                                                                                                        0.0s
 => => exporting layers                                                                                                                                                                0.0s
 => => writing image sha256:b34c324666a801b893625848401493a54bb21af5d35dbc9d2a1f7feec2ebd563                                                                                           0.0s
 => => naming to docker.io/library/python-docker-server                                                                                                                                0.0s
[+] Running 1/1
 ✔ Container python-docker-server-1  Recreated                                                                                                                                         0.1s 
Attaching to server-1
server-1  |  * Debug mode: off
server-1  | WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
server-1  |  * Running on all addresses (0.0.0.0)
server-1  |  * Running on http://127.0.0.1:5000
server-1  |  * Running on http://172.19.0.2:5000
server-1  | Press CTRL+C to quit
```

- Here is the example display of the container:
![Display of Python App](<screenshots/Screenshot 2024-02-12 at 8.55.11 PM.png>)

</details>

### Add local database with volume

<details><summary>view record</summary>

- After we modify compose.yaml to have volume instructions, and have a password.txt file containing key, we compose the stack:

```
$ docker compose up --build -d
[+] Building 1.0s (12/12) FINISHED                                                                                                                                     docker:desktop-linux
 => [server internal] load build definition from Dockerfile                                                                                                                            0.0s
 => => transferring dockerfile: 1.68kB                                                                                                                                                 0.0s
 => [server] resolve image config for docker.io/docker/dockerfile:1                                                                                                                    0.5s
 => CACHED [server] docker-image://docker.io/docker/dockerfile:1@sha256:ac85f380a63b13dfcefa89046420e1781752bab202122f8f50032edf31be0021                                               0.0s
 => [server internal] load metadata for docker.io/library/python:3.9.6-slim                                                                                                            0.3s
 => [server internal] load .dockerignore                                                                                                                                               0.0s
 => => transferring context: 667B                                                                                                                                                      0.0s
 => [server base 1/5] FROM docker.io/library/python:3.9.6-slim@sha256:4115592fd02679fb3d9e8c513cae33ad3fdd64747b64d32b504419d7118bcd7c                                                 0.0s
 => [server internal] load build context                                                                                                                                               0.0s
 => => transferring context: 154B                                                                                                                                                      0.0s
 => CACHED [server base 2/5] WORKDIR /app                                                                                                                                              0.0s
 => CACHED [server base 3/5] RUN adduser     --disabled-password     --gecos ""     --home "/nonexistent"     --shell "/sbin/nologin"     --no-create-home     --uid "10001"     appu  0.0s
 => CACHED [server base 4/5] RUN --mount=type=cache,target=/root/.cache/pip     --mount=type=bind,source=requirements.txt,target=requirements.txt     python -m pip install -r requir  0.0s
 => CACHED [server base 5/5] COPY . .                                                                                                                                                  0.0s
 => [server] exporting to image                                                                                                                                                        0.0s
 => => exporting layers                                                                                                                                                                0.0s
 => => writing image sha256:54609bcba0c8780988d30a00560520df0972937b43c044b2a7bb28a964a335ec                                                                                           0.0s
 => => naming to docker.io/library/python-docker-server                                                                                                                                0.0s
[+] Running 2/2
 ✔ Container python-docker-db-1      Healthy                                                                                                                                           0.0s 
 ✔ Container python-docker-server-1  Started 
```

- It is run successfully. Now we implement docker watch so that any change in script is automatically updated to the container.

```
# Compose with watch
$ docker compose watch
[+] Building 1.1s (14/14) FINISHED                                                                                                                                     docker:desktop-linux
 => [server internal] load build definition from Dockerfile                                                                                                                            0.0s
 => => transferring dockerfile: 1.68kB                                                                                                                                                 0.0s
 => [server] resolve image config for docker.io/docker/dockerfile:1                                                                                                                    0.5s
 => [server auth] docker/dockerfile:pull token for registry-1.docker.io                                                                                                                0.0s
 => CACHED [server] docker-image://docker.io/docker/dockerfile:1@sha256:ac85f380a63b13dfcefa89046420e1781752bab202122f8f50032edf31be0021                                               0.0s
 => [server internal] load metadata for docker.io/library/python:3.9.6-slim                                                                                                            0.4s
 => [server auth] library/python:pull token for registry-1.docker.io                                                                                                                   0.0s
 => [server internal] load .dockerignore                                                                                                                                               0.0s
 => => transferring context: 667B                                                                                                                                                      0.0s
 => [server base 1/5] FROM docker.io/library/python:3.9.6-slim@sha256:4115592fd02679fb3d9e8c513cae33ad3fdd64747b64d32b504419d7118bcd7c                                                 0.0s
 => [server internal] load build context                                                                                                                                               0.0s
 => => transferring context: 154B                                                                                                                                                      0.0s
 => CACHED [server base 2/5] WORKDIR /app                                                                                                                                              0.0s
 => CACHED [server base 3/5] RUN adduser     --disabled-password     --gecos ""     --home "/nonexistent"     --shell "/sbin/nologin"     --no-create-home     --uid "10001"     appu  0.0s
 => CACHED [server base 4/5] RUN --mount=type=cache,target=/root/.cache/pip     --mount=type=bind,source=requirements.txt,target=requirements.txt     python -m pip install -r requir  0.0s
 => CACHED [server base 5/5] COPY . .                                                                                                                                                  0.0s
 => [server] exporting to image                                                                                                                                                        0.0s
 => => exporting layers                                                                                                                                                                0.0s
 => => writing image sha256:54609bcba0c8780988d30a00560520df0972937b43c044b2a7bb28a964a335ec                                                                                           0.0s
 => => naming to docker.io/library/python-docker-server                                                                                                                                0.0s
[+] Running 2/3
 ⠋ Network python-docker_default     Created                                                                                                                                          11.0s 
 ✔ Container python-docker-db-1      Healthy                                                                                                                                          10.8s 
 ✔ Container python-docker-server-1  Started                                                                                                                                          10.9s 
Watch configuration for service "server":
  - Action rebuild for path "/Users/lucypham/Desktop/Docker-Project-1/python-docker"

```
- As we change the print from "Hello, Docker!" to "Hello, Lucy!", the docker updated the server accordingly.

![Changed Display from Python App](<screenshots/Screenshot 2024-02-12 at 9.01.27 PM.png>)

- close stack with Ctrl-C

</details>

### Implement Github Action for CI/CD

<details><summary>view record</summary>

- After we create a github with corresponding DOCKER_USERNAME and DOCKERHUB_TOKEN, we push our docker app to the github. Then we create Action workflow so that everytime the code is commited, The updated image is build and run.

![success commit build](<screenshots/Screenshot 2024-02-12 at 6.50.21 PM.png>)

- To check the running build, we use Kuberbetes as our deployment software. We write the docker-python-kubernetes.yaml and run it:

```
$ kubectl.docker apply -f docker-python-kubernetes.yaml     
deployment.apps/docker-python-demo unchanged
service/service-entrypoint created
```

- Checking the deployment and service status:

```
$ kubectl.docker get deployments
NAME                 READY   UP-TO-DATE   AVAILABLE   AGE
docker-python-demo   0/1     1            0           2m37s
# check online service
$ kubectl.docker get services 
NAME                 TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
kubernetes           ClusterIP   10.96.0.1       <none>        443/TCP          7m2s
service-entrypoint   NodePort    10.105.230.15   <none>        3000:30001/TCP   99s
```

- Now we check the connection by request the service via curl

```
$ curl "http://localhost:3000/"
Hello, Lucy!
```

- Confirmed that we has successfully implement CI/CD deployment. Now tear down the application:

```
$ kubectl delete -f docker-python-kubernetes.yaml
deployment.apps "docker-python-demo" deleted
service "service-entrypoint" deleted
```

</details>

--- finished Question 2 ---
