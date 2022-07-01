FROM node:lts-alpine3.14
ENV DIR=/usr/src/dehub-gui
RUN apk update && apk upgrade && apk add git python3 build-base
RUN git clone https://github.com/mig-frankfurt/dataelementhub.gui.git $DIR
WORKDIR $DIR
RUN git checkout develop
RUN yarn && yarn build
EXPOSE 3000
ENV NUXT_HOST=0.0.0.0
ENV NUXT_PORT=3000
CMD [ "npm", "run", "dev" ]