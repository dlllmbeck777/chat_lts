FROM node:18-alpine

WORKDIR /usr/src/app

# We will install packages inside the container for initialization later, or mount them.
# The entrypoint can be generic for now.
CMD ["sh", "-c", "npm install && npm run start:dev"]