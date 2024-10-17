# development stage
FROM node:18-alpine AS development

WORKDIR /usr/src/app

# Copy package.json and package-lock.json
COPY package.json package-lock.json ./

# Install dependencies
RUN npm ci

COPY . .

RUN npm run build

# production stage
FROM node:18-alpine AS production

WORKDIR /usr/src/app

# Copy package.json and package-lock.json
COPY package.json package-lock.json ./

RUN npm ci --prod

COPY --from=development /usr/src/app/dist ./dist

CMD ["node", "./dist/main.js"]
