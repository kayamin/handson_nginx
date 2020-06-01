FROM centos:centos7

COPY ./nginx.repo /etc/yum.repos.d/nginx.repo

# docker では firewalld で設定しても意味は無さそう
RUN yum install -y nginx tree net-tools

# nginx で使用する 80, 443 ポートを開けておく
EXPOSE 80
EXPOSE 443

# Docker image のビルドの際にキャッシュが効くように，頻繁に変更する設定ファイルは後に持ってくる
COPY ./nginx.conf /etc/nginx/nginx.conf

# nginx を systemd を用いず直接起動，設定ファイルを指定，フォアグラウンドで起動するための オプションを付与
# docker コンテナは フォアグラウンドでプロセスが起動していないと停止してしまう
CMD ["/usr/sbin/nginx", "-c", "/etc/nginx/nginx.conf", "-g", "daemon off;"]

# 内部で systemctl コマンドを使うために docker-compose.yml の privileged: true に加えて以下を実行
#CMD /sbin/init