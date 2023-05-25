# # Stage 1: Build the application
# FROM node:alpine3.17 as build

# # Set the working directory to /app
# WORKDIR /app

# # Copy only the package.json and package-lock.json
# COPY package*.json ./

# # Install production dependencies
# RUN npm ci --only=production

# # Stage 2: Create the production image
# FROM node:alpine3.17

# # Set the working directory to /app
# WORKDIR /app

# # Copy the built application from the previous stage
# COPY --from=build /app .

# # Set the command to run the application
# CMD ["npm", "start"]

FROM node:alpine3.16 As build
WORKDIR /client
COPY . .
RUN npm install
RUN npm run build

FROM nginx:1.19.0 As run
COPY --from=build /client/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
