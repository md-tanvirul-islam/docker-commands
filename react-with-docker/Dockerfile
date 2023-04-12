FROM node:14.16.0-alpine3.13
RUN addgroup app && adduser -S -G app app
WORKDIR /app
COPY . .
RUN npm install
ENV API_URL=http://www.something.com
EXPOSE 3000
CMD ["npm" "start"]
