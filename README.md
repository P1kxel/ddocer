apt-get update && apt-get install -y docker-engine
systemctl enable --now docker.service
docker run -d -p 5000:5000 --restart=always --name DockerRegistry registry:2

vim Dockerfile

FROM nginx:alpine
COPY index.html /usr/share/nginx/html

vim index.html(содрежимое на листе с заданием, просто перепеши оттуда)
docker build -t localhost:5000/web:1.0 .

docker push localhost:5000/web:1.0
docker pull localhost:5000/web:1.0
docker run -d -p 80:80 --restart=always --name web localhost:5000/web:1.0
