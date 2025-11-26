FROM node:20.19.5-alpine3.22 AS build
WORKDIR /opt/server
COPY *.js /opt/server/
COPY *.json /opt/server/
RUN npm install
ENV mongo="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
CMD [ "node","server.js" ]

FROM node:20.19.5-alpine3.22
# create a group and user
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
WORKDIR /opt/server
RUN chown -R roboshop:roboshop /opt/server
EXPOSE 8080
LABEL com.project="roboshop" \
      components="catalogue" \
      created_by="chakra"
ENV mongo="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
COPY --from=build /opt/server /opt/server
USER roboshop
CMD [ "server.js" ]
ENTRYPOINT [ "node" ]