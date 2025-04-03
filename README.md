# Nginx Docker Container with Custom HTML

This project demonstrates how to run an Nginx Docker container with a custom `index.html` file mounted from the host machine. The goal is to serve a simple HTML page via Nginx, exposed on port `8080`, and allow real-time updates to the content.

![overview](https://github.com/user-attachments/assets/13103f15-5506-475e-95f8-455b4c80df0a)


## 🎯 Objective

1. Create a host directory to store the HTML file.
2. Create an `index.html` file inside this directory.
3. Run an Nginx container, mounting the host directory and exposing it on port `8080`.
4. Access the container from a browser and observe real-time updates when the HTML file is modified.

---

## 🚀 Steps

### 1. Create a Host Directory
First, create a directory on your host machine to store the HTML file.

```bash
mkdir website
cd website
```
![1](https://github.com/user-attachments/assets/9250e99b-4abd-4d11-9aa8-16c3ede03388)


### 2. Create an `index.html` File
Create an `index.html` file inside the `website` directory.

![2](https://github.com/user-attachments/assets/8bd01baa-dd05-4b04-a6ce-c594ad305397)


You can use any text editor (e.g., `vim`, `nano`, or VS Code) to create and edit this file.

### 3. Run the Nginx Container
Run an Nginx container with the following command:

```bash
docker run -it -d --name web -p 8080:80 -v ~/website:/usr/share/nginx/html nginx
```
![3](https://github.com/user-attachments/assets/7ef53db1-7df8-492d-bdd8-e3f84cd82c28)


#### Explanation of Flags:
- `-it`: Run the container interactively (though `-d` detaches it).
- `-d`: Run the container in detached mode (background).
- `--name web`: Assign the name `web` to the container.
- `-p 8080:80`: Map port `8080` on the host to port `80` in the container (Nginx's default port).
- `-v ~/website:/usr/share/nginx/html`: Mount the host directory `~/website` to `/usr/share/nginx/html` (Nginx's default web root).
- `nginx`: Use the official Nginx Docker image.

### 4. Access the Container from a Browser
Open your browser and navigate to:
```
http://localhost:8080
```

You should see the HTML page you created.

![4](https://github.com/user-attachments/assets/b351891b-ed54-44a0-b9fe-bced81c8d135)


### 5. Real-Time Updates
Modify the `index.html` file on your host machine (e.g., change the text or add new elements). 

![5](https://github.com/user-attachments/assets/30a5ee35-34fa-40c5-9da8-8d8b9c59dcf3)

Refresh the browser to see the changes **immediately** without restarting the container.

![6](https://github.com/user-attachments/assets/e4931f09-61f2-4dbc-90ce-f2e2688e128d)

---

## 🔧 Troubleshooting

### Common Issues:
1. **Port Conflict**: If port `8080` is already in use, choose another port (e.g., `-p 8081:80`).
2. **Permission Issues**: Ensure the host directory (`~/website`) has read permissions for the Nginx process inside the container.
3. **Container Not Starting**: Check logs with:
   ```bash
   docker logs web
   ```

### Stop and Remove the Container:
```bash
docker stop web
docker rm web
```

---

## 📌 Notes
- Nginx serves files from `/usr/share/nginx/html` by default. Mounting a host directory here replaces the default Nginx welcome page.
- Changes to `index.html` are reflected instantly because the host directory is bind-mounted into the container.

---
