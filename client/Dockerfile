# Install dep and build app
FROM node:alpine as builder
WORKDIR '/app'
COPY ./package.json .
RUN npm install
COPY . .
RUN npm run build

# what we care about /app/build

# Run phase - this automatically stops previous stage (ie, the builder) once docker sees a "FROM"
# this ONLY has the build artifacts
FROM nginx
EXPOSE 3000
# copy over something from the other phase (see documentation on nginx - https://hub.docker.com/_/nginx)
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPy --from=builder /app/build  /usr/share/nginx/html
