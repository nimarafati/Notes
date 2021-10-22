This is summary of course that Mahesh Binzer-Panchal presented at NBIS.

# FastQC

running the image or owork with image interactively

    docker run --name fqc -it quay.io/biocontainers/fastqc:0.11.9--0 bash

Or just run a command

    docker run --name fqc -it quay.io/biocontainers/fastqc:0.11.9--0 bash --version

Removing the image

    docker rm fqc

# BWA

    docker pull biocontainers/bwa:v0.7.17_cv1

List running dockers/images

    docker ps -a

# R instance

Running docker with `-rm` it removes the image instance. The container
exist s but not the run instance.

    docker run --rm rocker/verse:4.1.1

This command pulls the image and then you can open the image after
finding the name by `docker ps`.  
Running R

Mapping outside to inside  
First run `docker os` to find the image name.

    docker run --rm -p 8787:8787 -v $HOME/Documents:/home/rstudio -e PASSWORD=Takenoko3 rocker/verse

You may also want to consider using eg docker run -p 127.0.0.1:8787:8787
… to ensure your container services are only accessible from your own
computer, and not by others on the network/internet (unless you made the
container image yourself, or are otherwise very certain that it is
secure)  
**It is very important to provide a password otherwise everyone can
access your local files!**

Then open a browser to open rstudio by `localhost:8787`then provide user
**rstudio** and password is what you provided in previous command.

You can create a yml file so that you can directly open the Rstudio

    # docker-compose.yml:
    version: "3.9"
    services:
      rstudio:
        image: 'rocker/verse:4.1.1'
        ports:
          - 8787:8787
        environment:
          - 'DISABLE_AUTH=true'
        volumes:
          - "$PWD:/home/rstudio"
        working_dir: /home/rstudio
        #user: "${UID, eval = F}:${GID, eval = F}"

To start the image then you can open the rStudio session through web
browser.

    docker compose -f docker-compose.yml up -d

To stop it run the following command:

    docker compose down  

CLeaning all of the images

    docker container prune  

# Create your own image

    # Dockerfile:

Push the image to github

    export GHCR=My_Token
    own_image % echo "$GHCR" | docker login ghcr.io -u nimarafati --password-stdin 
    own_image % docker build -t gchr.io/nimarafati/docker_demo/spade:1.0 .

# Singluarity

\*\* Difference between singularity and docker is that docker needs root
access \*\*
