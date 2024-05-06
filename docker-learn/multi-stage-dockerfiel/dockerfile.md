```
# Use a base image with Node.js installed
FROM node:14-alpine

# Set the working directory
WORKDIR /app

# Copy application files
COPY package.json .
COPY index.js .

# Install dependencies
RUN npm install --production

# Expose port 3000
EXPOSE 3000

# Start the application
CMD ["node", "index.js"]
```

