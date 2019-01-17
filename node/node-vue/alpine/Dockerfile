FROM node:alpine

RUN apk update && \
    apk add --no-cache tzdata make gcc g++ python bash && \
    cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    echo "Asia/Shanghai" >  /etc/timezone && \
    date

RUN mkdir -p /app

WORKDIR /app

ONBUILD ADD ["package.json", "/tmp/"]

ONBUILD RUN cd /tmp && \
    npm install --silent --production && \
    npm install chalk

ONBUILD RUN mv /tmp/node_modules /app

ONBUILD ADD . .

ONBUILD RUN npm run build && rm -rf /app/client

ONBUILD RUN apk del make gcc g++ python tzdata

CMD ["npm", "start"]
