# docker-compose

建立yml檔後，到檔案的目錄執行
```
docker-compose up -d
```
開始yml檔裡的配置建置docker並在後台執行(-d, detached mode)

docker-compose的指令類似docker
常用指令


| 用途               | 指令              | 常用可選參數 | 類似指令   |
| ------------------ | ----------------- | ------------ | ---------- |
| 建立並前景執行容器 | docker-compose up | -d、-f | docker run |
| 查看容器運作 | docker-compose up | -f | docker ps |
| 執行容器 | docker-compose start | -f | docker ps |
| 停止容器 | docker-compose stop | -f | docker stop |
| 刪除容器 | docker-compose down | -f | docker rm |
| 印出log | docker-compose logs | -f | docker logs |
| 進入容器 | docker-compose exec <service> bash | -f | docker exec -it <id or container-name> bash |

yml範例(PostgreSQL 13 + pgadmin 4)：
```yaml=
# 使用 3.8 版的設定檔，通常新版本會有新的功能，並支援新的設定參數
version: "3.8"

# 定義 service 的區塊，一個 service 設定可以用來啟動多個 container
services:
  # 定義 service
    postgres:
      container_name: postgresql13
      image: arm64v8/postgres:13
      environment:
        POSTGRES_USER: pg13
        POSTGRES_PASSWORD: pg13
      volumes:
        - postgres13:/Users/sam/DockerVolumes/postgresql/pgsql13
      ports:
        - "5432:5432"
      networks:
        - pgsql13
      restart: unless-stopped

    pgadmin:
      container_name: pgadmin4
      image: dpage/pgadmin4:eb05dedcba82f77440d164ea327bb3f5837213673e451260d14e225afbaa8364
 # latest linux/arm64/v8
      environment:
        PGADMIN_DEFAULT_EMAIL: sam2010mn32@gmail.com
        PGADMIN_DEFAULT_PASSWORD: sam2010mn32@gmail.com
      volumes:
        - pgadmin4:/Users/sam/DockerVolumes/postgresql/pgadmin4
      ports:
        - "9000:80"
      networks:
        - pgsql13
      restart: unless-stopped

networks:
  pgsql13:
    driver: bridge

volumes:
  postgres13:
  pgadmin4:
```

###### tags: `Docker`