FROM node:14.14.0-alpine as builder
WORKDIR '/usr/app'
COPY ./package.json ./
RUN npm install
COPY . .
RUN npm run build

# Phase 2
FROM nginx
# Below instruction is useless for our locals, but for EBS it uses this as the port for incoming traffic
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/build /usr/share/nginx/html
