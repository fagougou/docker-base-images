FROM node:latest

RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    echo "Asia/Shanghai" > /etc/timezone

RUN mkdir -p /app

WORKDIR /app

ONBUILD ADD ["package.json", "package-lock.json", "/tmp/"]

ONBUILD RUN cd /tmp && \
    npm install --production --silent && \
    npm install chalk

ONBUILD RUN mv /tmp/node_modules /app/

ONBUILD ADD . .

ONBUILD RUN npm run build && rm -rf /app/client

CMD ["npm", "start"]
