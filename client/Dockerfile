FROM node:alpine as builder
WORKDIR '/app'
COPY ./package.json ./
RUN npm install
COPY . .
# No need for volumes here since this is production
RUN npm run build

# /app/build <--- that's where all the final built app content will be

FROM nginx
# AWS will look for this EXPOSE instruction
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
# copy contents from the first phase:
COPY --from=builder /app/build /usr/share/nginx/html
# the default command of the nginx container is to start the server. No need for the CMD.