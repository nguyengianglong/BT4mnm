-Thiết lập file docker compose:

services:
  mariadb:
    image: mariadb:latest
    container_name: mariadb
    restart: always
    environment:
      TZ: "Asia/Ho_Chi_Minh"
      MARIADB_ROOT_PASSWORD: root123
      MARIADB_DATABASE: wordpress
      MARIADB_USER: wpuser
      MARIADB_PASSWORD: wp123
    volumes:
      - mariadb_data:/var/lib/mysql
    networks:
      - wp-network

  phpmyadmin:
    image: phpmyadmin:latest
    container_name: phpmyadmin
    restart: always
    ports:
      - "8080:80"
    environment:
      PMA_HOST: mariadb
      PMA_ARBITRARY: 1
    depends_on:
      - mariadb
    networks:
      - wp-network

  wordpress:
    image: wordpress:latest
    container_name: wordpress
    restart: always
    ports:
      - "8000:80"
    environment:
      WORDPRESS_DB_HOST: mariadb
      WORDPRESS_DB_NAME: wordpress
      WORDPRESS_DB_USER: wpuser
      WORDPRESS_DB_PASSWORD: wp123
    depends_on:
      - mariadb
    volumes:
      - wordpress_data:/var/www/html
    networks:
      - wp-network

  n8n:
    image: n8nio/n8n:latest
    container_name: n8n
    restart: always
    ports:
      - "5678:5678"
    environment:
      TZ: "Asia/Ho_Chi_Minh"
      WEBHOOK_URL: "http://n8n.nguyengianglong.io.vn/"
    volumes:
      - n8n_data:/home/node/.n8n
    networks:
      - wp-network

  cloudflared:
    image: cloudflare/cloudflared:latest
    container_name: cloudflared
    restart: always
    command: tunnel run
    environment:
      - TUNNEL_TOKEN=PASTE_TUNNEL_TOKEN_HERE
    networks:
      - wp-network

volumes:
  mariadb_data:
  wordpress_data:
  n8n_data:

networks:
  wp-network:

-cài đặt các img mới:
-Route các service:

<img width="1268" height="164" alt="image" src="https://github.com/user-attachments/assets/d8ad2dc9-d610-4a5e-9212-69a3db8b1700" />

Thêm id tunnel vào config.yml

<img width="1920" height="291" alt="image" src="https://github.com/user-attachments/assets/db60ae31-a9fd-426c-bf26-e027012a9c54" />

Cấu hình lại cloudflared trong docker compose.yml

<img width="636" height="226" alt="image" src="https://github.com/user-attachments/assets/1c6fa288-5db9-4832-a592-fc882f9af41e" />

Cấp quyền cho config:

<img width="696" height="31" alt="image" src="https://github.com/user-attachments/assets/a461ffe0-2064-4a14-b28a-f7372d37877b" />

Pull cái image và run:

<img width="1530" height="476" alt="image" src="https://github.com/user-attachments/assets/6309c9cc-20e1-47ff-a35f-6a0e8c5c5a55" />

Test: 

<img width="1920" height="877" alt="image" src="https://github.com/user-attachments/assets/38aad476-eba3-4296-b235-40cd3d413f46" />

<img width="1920" height="746" alt="image" src="https://github.com/user-attachments/assets/313825fe-d0c2-43c9-938d-ebdf4ecfaf28" />

<img width="1920" height="891" alt="image" src="https://github.com/user-attachments/assets/20c5e621-f93d-40e9-95b4-51a81599c66f" />

