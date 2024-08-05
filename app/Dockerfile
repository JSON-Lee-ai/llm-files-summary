# Stage 1: Build the SvelteKit application
FROM node:18 AS builder

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json (if available)
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application files
COPY . .

# Build the SvelteKit application
RUN npm run build

# Stage 2: Serve the application
FROM node:18-slim AS runner

# Set the working directory in the container
WORKDIR /app

# Copy only the necessary files from the build stage
COPY --from=builder /app/package*.json ./
COPY --from=builder /app/build ./build

# Install production dependencies only
RUN npm install --production

# Expose the port the app runs on
EXPOSE 3000

# Set environment variable to use the correct adapter
ENV PORT 3000
ENV NODE_ENV production

# Command to run the application
CMD ["node", "build"]

