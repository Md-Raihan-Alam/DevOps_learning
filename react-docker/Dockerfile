# set the base iamge to create the image for react app
FROM node:20-alpine

# create auser with permissions to run the app
# -S -> create a system user
# -G -> add the user to a group
# This is done to avoid running the app as root
# If the app is run as roon, any vulnerability in the app can be exploited to gain 
# access to the host system
# It's a good practice to run the app as a non-root user
RUN addgroup -S app && adduser -S -G app app

# set the working directory to /app
WORKDIR /app

# copy package.json and package-lock.json to the working directory
# this si done before copying the rest of hte files to take advantage of Docker's cashe
# if the packet.json and packet-lock.json files haven't change . Docker
# will use hte cached dependencies
COPY package*.json ./

# sometimes the ownership of the fiels in working direcotory is changed to root
# and thus the app can't access the fiels and throws an error -> EACCESS: permission denied
# to avoid this, change the ownership of the fiels to the root user
USER root

# change the ownershi of the /app director to the app user
# chown -R <user>:group <directory>
# chown command changes the user and/or group ownership of for given file
RUN chown -R app:app /app

# change the user back to the app user
USER app

# install dependencies
RUN npm install

# copy the rest of fieli to the working directory
COPY . .

# expose port 5173 to tell Docker that container listens on the specified network
# ports at runtime
EXPOSE 5173

# command to run the app
CMD ["npm", "run", "dev"]
