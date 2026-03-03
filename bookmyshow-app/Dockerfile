# -------------------------------
# Stage 1: Build React App
# -------------------------------
FROM node:20 AS build

WORKDIR /app

# Fix OpenSSL issue
ENV NODE_OPTIONS=--openssl-legacy-provider

COPY package*.json ./
RUN npm install --legacy-peer-deps

COPY . .
RUN npm run build


# -------------------------------
# Stage 2: Production Server
# -------------------------------
FROM node:20-slim

WORKDIR /app

RUN npm install -g serve

COPY --from=build /app/build ./build

EXPOSE 3000

CMD ["serve", "-s", "build", "-l", "3000"]
