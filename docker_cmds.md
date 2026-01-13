docker pull ubuntu

docker run -it ubuntu

docker build -t hello-docker .

docker images

docker run hello-docker

docker run -it hello-docker sh

docker ps

docker ps -a

docker stop c3d

docker container prune

docker rm aa7

docker rm aa7 --force

docker run -p 3000:5173 react-docker

docker run -p 3000:5173 -v "$(pwd):/app" -v /app/node_modules react-docker
docker run -p 3000:5173 -v ${PWD}:/app -v /app/node_modules react-docker
docker run -p 3000:5173 -v "%cd%:/app" -v /app/node_modules react-docker
docker run -e CHOKIDAR_USEPOLLING=true -p 3000:5173 -v "%cd%:/app" -v /app/node_modules react-docker npm run dev -- --host

docker login
docker tag react-docker <docker-username>/react-docker
docker push <docker-username>/react-docker
