# Deployment Steps for Dockerized Web Application
This document provides the full deployment process for setting up a Dockerized multi-container voting application on an AWS EC2 instance. Follow the steps in order to install dependencies, build Docker images, deploy services using Docker Compose, and verify the application.

---

## 1. Create the Environment in N. Virginia (us-east-1)

### Launch EC2 Instance
- Name: `docker-compose`
- AMI: `Amazon Linux 2023 (Kernel 6.12)`
- Instance Type: `t3.small`
- Key pair: `mykey`
- Auto assign public IP: enabled
- Security group: allow all traffic(for demo purpose)

---

## 2. Connect to the EC2 Instance

### Login to Server
$ sudo su -

### Install Docker
$ yum install docker -y
$ systemctl start docker
$ systemctl status docker

### Install Git
$ yum install git -y
$ git --version

## 3. Clone the Application Repository

### Fork Repository
$ https://github.com/<username>/docker-voting-app-new.git

### Clone Repository on EC2
$ git clone https://github.com/<your-username>/docker-voting-app-new.git
$ cd docker-voting-app-new

---

## 4. Build Docker Images

### Build Vote Service Image
$ cd vote
$ docker build -t vote .
$ cd ..

### Build Result Service Image
$ cd result
$ docker build -t result .
$ cd ..

### Build Worker Service Image
$ cd worker
$ docker build -t worker .
$ cd ..

---

### Verify Docker Images
$ docker images

## 5. Create Docker Compose File

### Create docker-compose.yml
$ vi docker-compose.yml
```
version: "3"

services:
  redis:
    image: redis

  db:
    image: postgres
    ports:
      - "2345:5432"
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres

  vote:
    image: vote
    ports:
      - "1000:80"
    links:
      - redis

  worker:
    image: worker
    links:
      - redis
      - db

  result:
    image: result
    ports:
      - "1001:80"
    links:
      - db
```
## 6. Deploy the Application

### Start All Services
$ docker-compose up -d

### Verify Running Containers
$ docker-compose ps

## 7. Verify Application Access

### Open in Browser

- Voting Application:
  http://<EC2-Public-IP>:1000

- Result Application:
  http://<EC2-Public-IP>:1001

If the setup is correct, the voting page and live results page will load successfully.

---
