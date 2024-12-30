# ---- Bases ----
FROM node:lts-alpine3.20 AS base
WORKDIR /app
COPY package.json ./
COPY pnpm-lock.yaml ./
RUN npm install -g pnpm

# ---- Dependencies ----
FROM base AS dependencies
RUN pnpm install --frozen-lockfile

# ---- Copy Files/Build ----
FROM dependencies AS build
COPY . .
# Use the build argument to run the specified build script
RUN pnpm prune --prod

# ---- Release ----
FROM node:lts-alpine3.20 AS release
#Release Workdir
WORKDIR /release
COPY --from=build /app .

CMD ["node", "index.js"]