# Stage 1: Build
FROM node:16-alpine AS build-stage
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Stage 2: Serve với Nginx (Ex-3.4 Optimize size)
FROM nginx:alpine
# FIX: Cập nhật hệ thống để vá các lỗ hổng bảo mật
RUN apk update && apk upgrade

WORKDIR /usr/share/nginx/html
COPY --from=build-stage /app/build .

# Ex-1.12: Cấu hình Nginx lắng nghe port 5000 thay vì 80 mặc định
RUN sed -i 's/listen 80;/listen 5000;/g' /etc/nginx/conf.d/default.conf

# Ex-3.3: Bảo mật - Chạy với user nginx (non-root)
RUN touch /var/run/nginx.pid && \
    chown -R nginx:nginx /var/run/nginx.pid /var/cache/nginx /var/log/nginx /etc/nginx/conf.d
USER nginx

EXPOSE 5000
CMD ["nginx", "-g", "daemon off;"]