FROM node:18
WORKDIR /app
COPY package* ./
RUN npm install
COPY . .
RUN npm run build
EXPOSE 80


FROM nginx:alpine
COPY --from=build /app /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g","daeamon off;"]
