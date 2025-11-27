# Use Node for Angular dev server
FROM node:18-alpine

# Set working directory
WORKDIR /app

# Copy package files first for caching
COPY package*.json ./

# Install Angular CLI globally
RUN npm install -g @angular/cli

# Install dependencies
RUN npm install

# Copy rest of the frontend code
COPY . .

# Expose Angular dev server port
EXPOSE 8081

# Default command to run Angular dev server
CMD ["ng", "serve", "--host", "0.0.0.0", "--port", "8081"]
