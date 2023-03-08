FROM node:15 as builder

WORKDIR /usr/src/app

COPY ./app .

RUN npm install

FROM node:15-alpine

WORKDIR /usr/src/app

RUN rm -rf /usr/src/app/*.*

COPY --from=builder /usr/src/app .

# TODO Is this working?
RUN apk add --no-cache wget
ENV DOCKERIZE_VERSION v0.6.1
RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && rm dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz

CMD ["node","index.js"]