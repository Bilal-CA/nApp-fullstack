# Official Node.js Image
FROM node:18

# Set working directory
WORKDIR /usr/src/app

# Set environment 
ENV NODE_ENV=production

# Copy package.json and package-lock.json files (if any)
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy rest of the app files
COPY . .

# Expose app port
EXPOSE 3000

# Start app
CMD ["node", "app.js"]
