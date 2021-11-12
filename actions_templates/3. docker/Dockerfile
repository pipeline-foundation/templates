# if JS
FROM node:16.11.1-alpine3.14

COPY dist dist

ENTRYPOINT [ "node", "/dist/index.js" ]

# if Bash
# # Container image that runs your code
# FROM alpine:3.14

# # Copies your code file from your action repository to the filesystem path `/` of the container
# COPY entrypoint.sh /entrypoint.sh

# # Code file to execute when the docker container starts up (`entrypoint.sh`)
# ENTRYPOINT ["/entrypoint.sh"]