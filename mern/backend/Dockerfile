# Stage01
FROM node:18.9.1 AS backend-builder 
WORKDIR /app 
COPY package*.json .      
RUN npm install 
COPY . . 

# Stage02 
FROM node:18-slim 
WORKDIR /app 
COPY --from=backend-builder /app . 
EXPOSE 5050 
CMD ["npm", "start"]
