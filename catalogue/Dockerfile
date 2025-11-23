FROM node:20
WORKDIR /app/server
COPY *.js /app/server/
COPY *.json /app/server/
RUN npm install
ENV mongo="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
# containers can access with their names
CMD [ "node","server.js" ]
    