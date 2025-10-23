# Docker-Network --- Connection of a Two Tier Flask App

If we want to establish communication between our application container and our database container using container name then we create a custom bridge network and assign the same network to both containers.

# Step 1

```bash
git clone https://github.com/muhammadaliazhar/Docker-Network.git
```


# Step 2 --- Create a Custom bridge Network

```bash
docker network ls
docker network create two-tier-network
```
<img width="822" height="214" alt="image" src="https://github.com/user-attachments/assets/c1280205-fd72-4fbd-b205-7c55ac95c999" />



# Step 3  --- Create image of flask application

```bash
 cd Docker-Network
 docker build -t two-tier-app .
docker images
```

<img width="811" height="234" alt="image" src="https://github.com/user-attachments/assets/a458d355-3992-4080-8bca-09045f83d913" />



# Step 4 --- Run mysql container using custom bridge network

```bash
docker run -d --name mysql_container --network two-tier-network -e MYSQL_ROOT_PASSWORD=123 -e MYSQL_DATABASE=devops
docker ps
```

# Step 5 --- Run Flask app container using same custom bridge network

```bash
docker run -d --name two-tier-container -p 5000:5000 --network two-tier-network -e MYSQL_HOST=mysql_container -e MYSQL_PASSWORD=123 -e MYSQL_DB=devops two-tier-app
docker ps
```
<img width="1669" height="184" alt="image" src="https://github.com/user-attachments/assets/acd3842f-335b-46df-9829-250acfa3ffaa" />


# Step 6 --- Inspect conatiners in your custom bridge network

```bash
docker network inspect two-tier-network
```
<img width="1053" height="881" alt="image" src="https://github.com/user-attachments/assets/51788fca-8d79-4f52-b574-86ba5a550831" />

Open Port 5000 in firewall rule


# Stap 7 --- Access application on browser  public-ip:5000

<img width="1152" height="615" alt="image" src="https://github.com/user-attachments/assets/bfb6ecd0-93ed-4955-84a7-a14cbba02fff" />


# Step 8 --- Check database enteries in db table

```bash
docker exec -it <mysql-container-id> /bin/bash
mysql -u root -p
```

<img width="949" height="801" alt="image" src="https://github.com/user-attachments/assets/2bcc3098-df43-4c86-9e48-ea204bfda36d" />



