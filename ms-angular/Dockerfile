FROM node:alpine AS builder
WORKDIR /app
COPY . .
RUN npm install && \
    npm run build
echo "build completed"
#FROM nginx:alpine
#COPY --from=builder /app/dist/ng-ms /usr/share/nginx/html/
