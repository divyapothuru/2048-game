CREATE A GAME 2048 USING DOCKER AND DEPLOY IN AWS:

WE NEED TO CREATE A DOCKER FILE(Here we used already existed github repo "Game repository https://github.com/gabrielecirulli/2048")
FROM ubuntu:22.04

#installing and updating required commands
RUN apt-get update
RUN apt-get install -y nginx zip curl

RUN echo "daemon off;" >>/etc/nginx/nginx.conf
#you dont need to clone this repo just by using this we can zip all this in a master.zip folder
RUN curl -o /var/www/html/master.zip -L https://codeload.github.com/gabrielecirulli/2048/zip/master
#unzip the code which was zipped in the folder and also delete the existed folder.
RUN cd /var/www/html/ && unzip master.zip && mv 2048-master/* . && rm -rf 2048-master master.zip

EXPOSE 80

CMD ["/usr/sbin/nginx", "-c","/etc/nginx/nginx.conf"]

-->docker build -t <image-name> .
-->docker images-to list all images
-->docker run -d -p 80:80 (imagename/imageid)
we can see the output in localhost:80
![image](https://github.com/divyapothuru/2048-game/assets/36921186/228cb3d1-def6-4562-9278-a5d21ee5f161)
we need to create the aws elastic bean stack application where we deploy this application.
After launching in aws
http://new-game-env.eba-7w5sqsj4.us-east-1.elasticbeanstalk.com/
![image](https://github.com/divyapothuru/2048-game/assets/36921186/cdc5cb3b-cd36-430a-a46f-40a0a44c2078)




