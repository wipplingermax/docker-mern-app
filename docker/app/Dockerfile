FROM node:latest

RUN mkdir -p /home/app
WORKDIR /home/app

RUN npm install -g --silent --force yarn

RUN alias yarn='node /usr/local/bin/yarn'

RUN yarn global add nodemon

COPY ./start.sh /home/start.sh

CMD bash /home/start.sh