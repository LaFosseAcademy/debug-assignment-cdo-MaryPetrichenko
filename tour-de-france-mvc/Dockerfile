FROM node:16
WORKDIR /app
COPY package*.json /app
RUN npm install
COPY . /app
ENV PORT=3000
# The default value of a user when creating a postgreSQL DB
ENV DB_USER=postgres
# The value of the service name which is used in the 'docker-compose.yml' file
ENV DB_HOST=tour-de-france-db
# The name of the database we assigned in the microservice
ENV DB_NAME=tour-de-france
# The value of the password we assigned in the microservice
ENV DB_PASSWORD=docker
# The default port when creating a postgreSQL DB
ENV DB_PORT=5432
EXPOSE 3000
CMD ["node", "index.js"]