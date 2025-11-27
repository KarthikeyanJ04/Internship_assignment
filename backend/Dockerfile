# Use a lightweight Node.js image
FROM node:18-alpine

# Create app directory inside container
WORKDIR /app

# Copy package files first (for better caching)
COPY package*.json ./

# Install only production dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Expose the backend API port
EXPOSE 8080

# Set environment variable for production
ENV NODE_ENV=production

# Start the server
CMD ["node", "server.js"]
