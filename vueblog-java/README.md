# 后台打包
mvn clean package -Dmaven.test.skip=true

# 服务启动
docker-compose up -d

# 服务重启
docker-compose restart