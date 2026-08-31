# Stage 1: Build the Angular application
FROM node:22-alpine AS build

WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm ci

# Copy source code
COPY . .

# Build Angular application
RUN npm run build

# Stage 2: Run the Angular SSR application
FROM node:22-alpine

WORKDIR /app

# Copy package files
COPY package*.json ./

# Install only production dependencies
RUN npm ci --omit=dev

# Copy the built Angular application
COPY --from=build /app/dist ./dist

# Angular SSR default port
EXPOSE 4000

# Start the SSR server
CMD ["node", "dist/angular-app/server/server.mjs"]
