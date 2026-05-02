FROM node:22-alpine AS builder

WORKDIR /app

COPY package*.json ./
COPY backend/package*.json ./backend/

RUN npm install --workspace backend --legacy-peer-deps

COPY backend/ ./backend/

RUN npm run build:backend

FROM node:22-alpine

WORKDIR /app

COPY --from=builder /app/package*.json ./
COPY --from=builder /app/backend/package*.json ./backend/
COPY --from=builder /app/backend/dist ./backend/dist

RUN npm install --workspace backend --omit=dev --legacy-peer-deps

EXPOSE 5000

CMD ["node", "backend/dist/server.js"]