FROM node:18-alpine

WORKDIR /app

# Install frontend dependencies
COPY package*.json ./
RUN npm install

# Copy frontend source
COPY . .

# The Angular dev server will listen on 0.0.0.0 so it works in Docker
EXPOSE 4200

# Use existing start script, which should run ng serve with host 0.0.0.0 and port 4200
CMD ["npx", "ng", "serve", "--host", "0.0.0.0", "--port", "4200", "--disable-host-check"]
