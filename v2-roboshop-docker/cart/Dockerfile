FROM node:20
WORKDIR /app/server
COPY *.js .
COPY *.json .
RUN npm install 
ENV REDIS_HOST="redis" \
    CATALOGUE_HOST="catalogue" \
    CATALOGUE_PORT="8080"
EXPOSE 8080
CMD [ "node","server.js" ]