FROM node:18-bullseye-slim

WORKDIR /app

# Install minimal build tools to ensure native modules (sqlite3) can be built if needed
RUN apt-get update \
  && apt-get install -y --no-install-recommends python3 make g++ \
  && rm -rf /var/lib/apt/lists/*

COPY package*.json ./

# Install production dependencies
RUN npm install --production

# Copy app sources
COPY . .

# Expose the port the app listens on
EXPOSE 5000

ENV PORT=5000

CMD ["npm", "start"]
