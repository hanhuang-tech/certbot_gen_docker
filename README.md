# certgen_docker
- Creates a container for certbot and executes certbot commands on a mounted container.  
  
To use:  
1. docker build -t cert_gen .    #generates cert_gen docker image from Dockerfile  
2. bash cert_gen.sh    #starts new container using docker image cert_gen, runs bash inside container  
3. bash certbot_web.sh    #inside docker image > bash this shell script to generate new certbot certificate  
***
**Dockerfile**  
From an alpine image, copy across certbot_dns.sh to root inside the created container.  
Run below required instructions:  
- copy certbot_dns.sh to root (see below)
- apk upgrade  
- add certbot  
- add bash  
- expose port 2000  
  
**cert_gen.sh**  
docker run: Creates a container called cert_gen that is interactive in terminal.  
Mounts on host a directory called "certs" onto target /etc/letsencrypt in the container.  
Starts a bash session within this container.  
By running certbot_dns.sh, generates TLS certificates via certbot to /etc/letsencrypt  
Host will parallel TLS certificates generated by above process.  
  
**certbot_web.sh**  
certbot certonly: Bash shell script to generate TLS certificate usng TXT record for hanhuang.tech.  
use webroot authentication on path /.well-known/acme-challenge/
