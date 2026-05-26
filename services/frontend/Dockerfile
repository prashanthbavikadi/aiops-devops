# # Frontend Dockerfile
# FROM node:20-alpine

# WORKDIR /app

# # Copy package files
# COPY package*.json ./
# RUN npm install --production=false

# # Copy source code
# COPY . .

# # Build the app
# RUN npm run build

# # Install serve globally
# RUN npm install -g serve

# EXPOSE 3000

# # Use serve to host the static files
# CMD ["serve", "-s", "build", "-l", "3000", "--single"]



# =========================
# Stage 1: Build Stage
# =========================
FROM node:20-alpine AS builder

WORKDIR /app

# Copy package files first
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy source code
COPY . .

# Build frontend
RUN npm run build

# =========================
# Stage 2: Production Stage
# =========================
FROM nginx:alpine

# Remove default nginx files
RUN rm -rf /usr/share/nginx/html/*

# Copy only build output
COPY --from=builder /app/dist /usr/share/nginx/html

# Expose port
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]