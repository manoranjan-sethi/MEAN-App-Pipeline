FROM node:20-slim AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci

FROM node:20-slim
RUN apt-get update && apt-get install -y --no-install-recommends dumb-init \
    && rm -rf /var/lib/apt/lists/*
WORKDIR /app
COPY --from=builder /app/node_modules ./node_modules
COPY . .

EXPOSE 8080
CMD ["dumb-init", "node", "server.js"]