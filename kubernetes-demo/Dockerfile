# use a small base3 image
FROM node:18-alpine AS base3
WORKDIR /app

# Install deps separately for caching
COPY package.json package-lock.json* ./
RUN npm ci --omit=dev

# Copy app source
COPY . .

# Run as non-root (alpine node image includes user "node")
USER node
EXPOSE 3000
ENV NODE_ENV=production
CMD ["npm","start"]