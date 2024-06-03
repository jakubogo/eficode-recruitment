FROM node:latest

WORKDIR /backend

COPY package.json .
COPY package-lock.json .

RUN npm install

COPY . .

EXPOSE 9000

CMD [ "npm" , "run", "start-watch"]
