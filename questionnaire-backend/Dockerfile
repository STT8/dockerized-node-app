#Build Stage
FROM docker.io/library/node:12-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
# Copy prod config
RUN cp src/environments/environment.prod.ts src/environments/environment.ts
RUN npm run build

#Prod stage
FROM docker.io/library/node:12-alpine
WORKDIR /app
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/package*.json ./
RUN npm install
EXPOSE 3000
CMD ["node", "dist/index.js"]
