FROM node:lts

# ENV NODE_ENV=production
# ENV HOST 0.0.0.0

RUN mkdir -p /app
COPY ./app /app
WORKDIR /app

EXPOSE 3000

RUN yarn install
RUN yarn build

CMD ["yarn", "start"]