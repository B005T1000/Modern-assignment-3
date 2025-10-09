FROM node:18-bullseye-slim AS build
WORKDIR /app

# Accept build-time API URL so Vite can bake it into the static build
ARG VITE_API_URL=http://localhost:5000
ENV VITE_API_URL=${VITE_API_URL}

COPY package*.json ./
RUN npm install

COPY . .
# Build the production static assets (Vite will read VITE_API_URL at build time)
RUN npm run build

FROM node:18-bullseye-slim AS runtime
WORKDIR /app

# Install a small static server
RUN npm install -g serve@14

COPY --from=build /app/dist ./dist

EXPOSE 3000

ENV PORT=3000
CMD ["serve", "-s", "dist", "-l", "3000"]
