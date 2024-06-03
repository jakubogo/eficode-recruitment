FROM node:16

WORKDIR /frontend

COPY package.json .
COPY package-lock.json .
COPY webpack.config.js .

RUN npm install 

COPY . .

EXPOSE 8000

CMD [ "npm" , "run", "start-watch"]
