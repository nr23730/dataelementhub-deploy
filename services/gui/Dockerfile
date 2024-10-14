FROM node:lts-alpine
ENV DIR=/usr/src/dehub-gui
RUN apk update && apk upgrade && apk add git python3 build-base
RUN git clone https://github.com/imi-frankfurt/dataelementhub.gui.git $DIR
WORKDIR $DIR
RUN git checkout 1b7e1badf9db2e4dbdf5ff839baf120a0822de2b
RUN yarn && yarn build
EXPOSE 3000
ENV NUXT_HOST=0.0.0.0
ENV NUXT_PORT=3000
CMD [ "npm", "run", "dev" ]
