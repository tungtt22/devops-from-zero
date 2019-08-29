create a project angular:

install node js
install ng:

npm install -g @angular/cli

* create new angular project:
ng new angular-test1

* create a dockerfile (
   *stage1*
FROM node:latest as node 

WORKDIR /hue

COPY . .

RUN npm install

RUN npm run build --prod

*stage2*

FROM nginx:latest

COPY --from=node /hue/dist/angular-test1 /usr/share/nginx/html 
)

* pull image:
    - docker pull node
    - docker pull nginx