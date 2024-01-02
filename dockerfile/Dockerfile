ARG BASE_PRIVATE_REGISTRY=""
FROM ${BASE_PRIVATE_REGISTRY}node:14.5.0 as install
ADD ./package-lock.json ./package.json /distributedkube/simulator/
WORKDIR //simulator
RUN npm ci --production

ARG BASE_PRIVATE_REGISTRY=""
FROM ${BASE_PRIVATE_REGISTRY}/base-node:v1.2.0
LABEL maintainer="danielpickens@gmail.com"
COPY ./package.json ./package-lock.json /distributedkube/simulator/
COPY build //simulator/build
COPY server //simulator/server
COPY --from=install /distributedkube/simulator/node_modules /distributedkube/simulator/node_modules
WORKDIR /distributedkube/simulator
CMD ["npm", "run", "start:server"]
