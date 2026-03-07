FROM node:18-alpine

WORKDIR /app

# Install backend dependencies
COPY package*.json ./
RUN npm install --only=production

# Copy backend source
COPY . .

# Environment and port
ENV PORT=8080
EXPOSE 8080

# Use the existing start script from package.json
CMD ["npm", "start"]