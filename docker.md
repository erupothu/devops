
# window machine

#### create VM in virtual box  
> download centos iso image and run the server in VM  
> setup network to access system internet  
> Login with username and password  
> add ip to check the public ip ( we can connect form putty through ssh centos@public_ip_address  

#### install Docker in VM  
> sudo yum install -y yum-utils  
> sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo  
> sudo yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin  
> sudo systemctl start docker  
> sudo docker run hello-world  

#### Docker commands  
> docker version  
> docker images  
> docker ps (container)  
> docker ps -a (running containers)  
> docker build image_name [path_to_code] or docker build -f [path_to_mydockerfile.dockerfile] image_name [path_to_code]  
> docker run -p target_port:acutal_port image_name  --name container_name  
> docker kill container_name  
> docker rm container_name  
> docker rmi image_name  

#### Custom Docker file
```index.html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Docker Nginx</title>
</head>
<body>
  <h2>Hello from Nginx container</h2>
</body>
</html>
```

```Dockerfile
FROM nginx:latest
COPY ./index.html /usr/share/nginx/html/index.html
```

> docker build -t webserver .   
> docker run -it --rm -d -p 8080:80 --name web webserver  

#### Docker Registry  

1. Create docker hub account  
2. In account security generate token and save  

> docker login -u [username]  
> [password/generated_token]  
>
> docker image tag cust_nginx harishe/cust_nginx:web  
> docker push harishe/cust_nginx:web  
