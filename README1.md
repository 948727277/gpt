# dev-ops
[README.md](README.md)
docker run \
--restart always \
--name Nginx \
-d \
-p 80:80 \
nginx

mkdir -p /data/nginx/conf
mkdir -p /data/nginx/html

docker container cp Nginx:/etc/nginx/nginx.conf /home/fzx/gpt/dev-ops/nginx/conf
docker container cp Nginx:/etc/nginx/conf.d/default.conf /home/fzx/gpt/dev-ops/nginx/conf/conf.d/default.conf
docker container cp Nginx:/usr/share/nginx/html/index.html /home/fzx/gpt/dev-ops/nginx/html

docker run \
--name Nginx \
-p 80:80 \
-v /home/fzx/gpt/dev-ops/nginx/logs:/var/log/nginx \
-v /home/fzx/gpt/dev-ops/nginx/html:/usr/share/nginx/html \
-v /home/fzx/gpt/dev-ops/nginx/conf/nginx.conf:/etc/nginx/nginx.conf \
-v /home/fzx/gpt/dev-ops/nginx/conf/conf.d:/etc/nginx/conf.d \
-v /home/fzx/gpt/dev-ops/nginx/ssl:/etc/nginx/ssl/  \
--privileged=true -d --restart=always nginx