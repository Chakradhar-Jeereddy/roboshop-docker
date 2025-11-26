FROM node:20
WORKDIR /app/server
COPY *.js /app/server/
COPY *.json /app/server/
RUN npm install
ENV mongo="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
# containers can access with their names
CMD [ "node","server.js" ]


## Run and rest
 # docker build --no-cache --progress=plain -t catalogue:v1 catalogue/.
 # docker run -d --name=catalogue f7efa194d4a4
 # curl http://localhost:8080/health
 # {"app":"OK","mongo":false}