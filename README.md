# nginx-reverse-proxy
Nginx reverse proxy setup with Let's Encrypt for https support and docker-compose for easy deployment

As the title says, with this repository you can quickly spin up an nginx reverse proxy that uses https with combination of Let's Encrypt and Certbot.

Certificate renewal is taken care of with Certbot. 

Prerequisites:
- Docker and docker-compose installed
- Valid domain name either free or paid
- Server with public ip address that can be setup with domain, or server which has a dynamic-dns setup
- Domain and server ip connected and working (A Record)

In order to run it you have to follow these steps:
- Clone the repository
- Replace all the occurrences of change-me.org with your domain
- Replace '<address and port of your service>' with the docker container name of your service and internal docker port (not the exposed one to the host)
- Your service needs to run inside dockernet network in order to be visible by the proxy!
- If your service is running outside of docker uncomment bridge mode in the docker-compose.yml and comment out the networks sections

After that you will need to change permissions for the init.sh with
```bash
sudo chmod +x init.sh
```

And execute it with
```bash
sudo ./init.sh
```

Follow the process and after it is finished run
```bash
docker-compose up -d
```

To start the docker containers. You will have working proxy with ssh support and automatic renewal of certificates! 

If you want to run more services behind the proxy, you can adjust the app.conf file add more location blocks and point them to your services. 

In that case you can't serve it from root of the server, but every service would need to have a separate path like
```
location /service1 {
  ...
}

location /service2 {
  ...
}

```

Happy hacking!
OctaCode Team
