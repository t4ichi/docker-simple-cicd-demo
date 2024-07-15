FROM node:18 AS base

CMD [ "bash" ]

# build
FROM base As test-and-build
COPY . /workspace
WORKDIR /workspace
ARG REACT_APP_API_SERVER
RUN npm ci && npm RUN test && RUN npm run build

# hosting in nginx
FROM nginx:latest AS production
COPY --from=build /workspace/build /var/www
COPY nginx.conf /etc/nginx/conf.d/default.conf
