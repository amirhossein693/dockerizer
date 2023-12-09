FROM node:18-alpine AS deps
WORKDIR /app
COPY package.json package-lock.json* ./

FROM deps as runner
WORKDIR /app
COPY . .
RUN npm install
RUN npm run build
EXPOSE 3000
ENV NODE_ENV production
CMD ["npm", "start"]
