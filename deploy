echo "==============开始安装qBittorrent=================="
apt install -y docker.io docker-compose
mkdir /qbt/
mkdir /qbt/config
mkdir /qbt/downloads
mkdir /qbt/docker && cd /qbt/docker
cat >docker-compose.yml<<EOF
version: "3.7"
services:
  qbittorrent:
    image: linuxserver/qbittorrent:14.3.9.99202110311443-7435-01519b5e7ubuntu20.04.1-ls166
    container_name: qbt_qbittorrent
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Stockholm
      - UMASK_SET=022
      - WEBUI_PORT=58180
    ports:
      - 50282:50282
      - 50282:50282/udp
      - 58180:58180
    volumes:
      - /qbt/config:/config
      - /qbt/downloads:/downloads
    restart: always
EOF
docker-compose pull 
docker-compose up -d 
sleep 10
docker-compose down
mv /qbt/config/qBittorrent/qBittorrent.conf /qbt/config/qBittorrent/qBittorrent.conf.bak
sed -i "s/PortRangeMin=30282/PortRangeMin=50282/"  /qbt/config/qBittorrent/qBittorrent.conf
docker-compose up -d 
echo "==============qBittorrent安装完成=================="
echo "==============qBittorrent账号信息=================="
ip=$(curl ip.sb)
echo "web地址: http://"$ip":58180"
echo "默认账号: admin"
echo "默认密码: adminadmin"
echo "=================qBittorrent======================"
