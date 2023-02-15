# This dockerfile must be built with the monorepo root directory as cwd
FROM node:lts-alpine

# RUN npm i -g pnpm@latest

# all files needed for the build
COPY package.json .
COPY package-lock.json .
# COPY tsconfig.json .
COPY svelte.config.js .
COPY vite.config.js .

# all folders needed for the build
COPY src src/
COPY static static/

RUN npm install --frozen-lockfile

RUN npm run build

EXPOSE 8080

CMD ["node", "build"]
