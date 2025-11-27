# Stage 1: Build
FROM node:18-alpine as build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build --prod

# Stage 2: Serve
FROM nginx:alpine

# DELETE the default Nginx config
RUN rm /etc/nginx/conf.d/default.conf

# COPY your new custom config
COPY nginx.conf /etc/nginx/conf.d/default.conf

# COPY the Angular files (Use the path you found earlier)
COPY --from=build /app/dist/angular-15-crud /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
