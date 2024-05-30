FROM node:16
WORKDIR /app
COPY . .
RUN npm install
CMD ["iconic", "server"]
api: {
    url: 'http://localhost:8000/', <-- server URL
    mapKey: '', <-- Leaflet map key,
    googleAuthClientId: '', <-- google Auth CLient ID for Social signin
    webSocketUrl: 'ws://localhost:8000/websocket' <-- websocket URL
  }
EXPOSE 80
