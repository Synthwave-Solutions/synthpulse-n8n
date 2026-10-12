FROM node:24.18.0-bookworm-slim
RUN apt-get update && apt-get install -y --no-install-recommends python3 make g++ tini ca-certificates && rm -rf /var/lib/apt/lists/*
COPY compiled /usr/local/lib/node_modules/n8n
WORKDIR /usr/local/lib/node_modules/n8n
RUN npm rebuild sqlite3 isolated-vm && ln -s /usr/local/lib/node_modules/n8n/bin/n8n /usr/local/bin/n8n
RUN mkdir -p /home/node/.n8n && chown -R node:node /home/node/.n8n
USER node
WORKDIR /home/node
ENV NODE_ENV=production
EXPOSE 5678
ENTRYPOINT ["tini", "--", "n8n"]
