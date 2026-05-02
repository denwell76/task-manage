FROM node:22-alpine AS builder

WORKDIR /app

COPY package*.json ./
COPY frontend/package*.json ./frontend/

RUN npm install --workspace frontend --legacy-peer-deps

COPY frontend/ ./frontend/

ARG VITE_API_URL
ENV VITE_API_URL=$VITE_API_URL

RUN npm run build:frontend

FROM nginx:alpine

COPY --from=builder /app/frontend/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]