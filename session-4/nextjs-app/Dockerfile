# Stage number 1
# Install dependencies
FROM node:20 AS deps

WORKDIR /app

COPY package*.json ./

RUN npm install

#Stage number 2 
#build and compile the application

FROM node:20-alpine AS builder

WORKDIR /app

COPY --from=deps /app/node_modules ./node_modules

COPY . .

RUN npm run build

#Stage number 3
#Final stage has everything we need for the runtime.

FROM node:20-alpine AS final

WORKDIR /app

COPY --from=deps /app/node_modules ./node_modules
COPY --from=builder /app/.next ./.next
COPY --from=builder /app/public ./public
COPY --from=builder /app/next.config.js ./

RUN chown -R node:node /app
USER node
EXPOSE 3000

CMD ["npm", "start"]