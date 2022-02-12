# install the application dependencies in a full UBI Node docker image
FROM registry.access.redhat.com/ubi8/nodejs-16:latest as builder

# install pnpm app dependencies
RUN npm install -g pnpm

# copy everything excluding files/directories matching pattern in .dockerignore
COPY . .

# install 
RUN pnpm install
RUN pnpm build 

# prune e.g. devDependencies will be removed.
RUN pnpm prune --production

# copy the app along with production dependencies into a minimal Node.js image
FROM registry.access.redhat.com/ubi8/nodejs-16-minimal:latest

# copy node_modules, build and package.json
WORKDIR /opt/app-root/
COPY --from=builder /opt/app-root/src/node_modules ./node_modules
COPY --from=builder /opt/app-root/src/build ./app
COPY --from=builder /opt/app-root/src/package.json ./

ENV NODE_ENV production
ENV PORT 3000
EXPOSE 3000

CMD ["node", "app"]

ENV HOST=0.0.0.0
