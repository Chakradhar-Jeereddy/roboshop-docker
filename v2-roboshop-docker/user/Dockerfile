FROM node:20.19.5-alpine3.22 AS build
WORKDIR /opt/server
COPY *.js /opt/server/
COPY *.json /opt/server/
RUN npm install


FROM node:20.19.5-alpine3.22
# create a group and user
WORKDIR /opt/server
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /opt/server
EXPOSE 8080
LABEL com.project="roboshop" \
      components="catalogue" \
      created_by="chakra"
ENV MONGO="true" \
    REDIS_URL="redis://redis:6379" \
    MONGO_URL="mongodb://mongodb:27017/user"
COPY --from=build --chown=roboshop:roboshop /opt/server /opt/server
USER roboshop
CMD [ "server.js" ]
ENTRYPOINT [ "node" ]



# FROM node:20
# WORKDIR /app/server
# COPY *.js .
# COPY *.json .
# RUN npm install 
# ENV MONGO="true" \
#     REDIS_URL="redis://redis:6379" \
#     MONGO_URL="mongodb://mongodb:27017/user"
# EXPOSE 8080
# CMD [ "node","server.js" ]

