Key takeaways: 
==
**Stage 1**
- Multi-stage build → smaller, cleaner final image.
- Keeps final image small → no dev cache.
- Copy all raw materials (JS & JSON files).
- Install dependencies (npm install).
- Build the finished product.

**Stage 2**
- Copy only finished product from Stage 1

```
FROM node:20.19.5-alpine3.22 AS build
WORKDIR /opt/server
COPY *.js /opt/server/
COPY *.json /opt/server/
RUN npm install
```
***Explanation**

- FROM node:20.19.5-alpine3.22 AS build → “Use Node.js lightweight Alpine image for building the app and call this stage build”
- WORKDIR /opt/server → “Set working folder inside container”
- COPY *.js & COPY *.json → “Copy all JavaScript and JSON files to the container”
- RUN npm install → “Install all Node dependencies”
**Key point:** This stage is only for building the app. The final image won’t carry unnecessary files like node_modules cache from build tools unless needed.

```
FROM node:20.19.5-alpine3.22
WORKDIR /opt/server
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /opt/server
```
***COPY --from=build --chown=roboshop:roboshop /opt/server /opt/server**
- Copy the compiled code to the container.
```
EXPOSE 8080
LABEL com.project="roboshop" \
      components="catalogue" \
      created_by="chakra"
CMD [" server.js" ]
ENTRYPOINT [ "node" ]
```
***Explanation:** Start fresh lightweight Node image
- Create non-root user and group roboshop (good security practice)
- Change ownership of /opt/server → the app runs as roboshop, not root.
- “Don’t run your app as admin — make a dedicated user for safety.”
