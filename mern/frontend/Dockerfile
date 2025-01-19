#stage01 
FROM node:18.9.1 AS frontend-builder 
WORKDIR /app 
COPY package*.json .  
RUN npm install 
COPY . . 

#stage02 
FROM node:18-slim 
WORKDIR /app 
COPY --from=frontend-builder /app . 
EXPOSE 5173 
CMD ["npm", "run", "dev"]
