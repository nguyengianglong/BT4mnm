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
    vo
    lumes:
    
      - mariadb_data:/var/lib/mysql
    ne
    tworks:
    
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

-truy cập sub-domain nhưng do e đang sử dụng từ bài cũ luôn nên wordpress đã được cài đặt:

<img width="1920" height="745" alt="image" src="https://github.com/user-attachments/assets/885927fd-a175-4527-95a8-603bbe4e721e" />

-Tạo bài viết tổng kết những gì đã học trong môn học Phát triển chương trình với mã nguồn mở:

<img width="1920" height="927" alt="image" src="https://github.com/user-attachments/assets/21febfa8-e90a-4555-b8b8-f5b32bec4fef" />

-tạo tk n8n

<img width="1920" height="692" alt="image" src="https://github.com/user-attachments/assets/862bf39a-87c2-446a-ab06-5f8cab7d2e73" />

-Gửi lincense key:

<img width="659" height="571" alt="image" src="https://github.com/user-attachments/assets/e74ab4e5-e534-4c1a-b343-6d946716548f" />

-check mail lấy license key:

<img width="890" height="537" alt="image" src="https://github.com/user-attachments/assets/f490f48a-e87f-4b8a-9056-0fd4a466677d" />

-Vào usage and plan, nhập key:

<img width="1916" height="643" alt="image" src="https://github.com/user-attachments/assets/fa9f9207-0a18-4cda-bba0-7d49bb7f8830" />

-Tạo workflow mới + telegram trigger

<img width="1920" height="724" alt="image" src="https://github.com/user-attachments/assets/04db3140-cf86-42e8-ab85-b41e36d3da1d" />

-Tạo bot lấy token:

<img width="858" height="1908" alt="image" src="https://github.com/user-attachments/assets/7ee66531-c8d5-4076-a666-001a784e5cff" />

-Nhập token mới nhận:

<img width="1920" height="932" alt="image" src="https://github.com/user-attachments/assets/506cf906-8d40-432f-a464-80214c8193b3" />

-Chat với bot mới:

<img width="858" height="1908" alt="image" src="https://github.com/user-attachments/assets/e8c2ec1f-e2bd-415f-8f7a-ac4f7672ebf8" />

<img width="1914" height="532" alt="image" src="https://github.com/user-attachments/assets/77509b3b-21b2-479b-9caa-32ee4849efb9" />

-Add (nối tiếp vào sau node Telegram Trigger) node: AI Google Gemini => Message a model => Set up Credential => cần Nhập API KEY

<img width="1920" height="368" alt="image" src="https://github.com/user-attachments/assets/45f8d86d-3f29-4de5-a257-7a42a540e4f7" />


<img width="846" height="184" alt="image" src="https://github.com/user-attachments/assets/8ce15b46-b03d-41c2-b405-c27fce59118f" />

<img width="1215" height="758" alt="image" src="https://github.com/user-attachments/assets/36cd2c5a-4b34-41c9-b23f-73051eb23d0d" />

-Kéo phần text đã nhắn với bot từ trước, sau đó thêm lệnh+ bật Output Content as JSON để kết quả trả về JSON + có thể thêm option cho nó chuyên nghiệp

<img width="1853" height="801" alt="image" src="https://github.com/user-attachments/assets/30feb0d4-377e-49f3-a211-f68277f4c97d" />

<img width="1920" height="935" alt="image" src="https://github.com/user-attachments/assets/4d83a84f-c9f8-4b32-b624-89d661e30dc0" />

-Thêm node code javacript 

<img width="1920" height="940" alt="image" src="https://github.com/user-attachments/assets/844b8b88-f2a0-460c-b449-84c55d47e4c3" />

-Thêm node wordpress create a post-lấy mk ứng dụng ở trong wordpress

<img width="397" height="839" alt="image" src="https://github.com/user-attachments/assets/c01f259f-804e-4908-8287-52ec912faee9" />

<img width="1196" height="756" alt="image" src="https://github.com/user-attachments/assets/04b309ed-5aaa-46ad-a9be-9c3116d9687c" />

- Cấu hình kéo các tp cần thiết vào ô như tittle+ content+ status thì chọn publish

<img width="1870" height="934" alt="image" src="https://github.com/user-attachments/assets/a400f32c-340e-430f-9413-83b8bf54f8e0" />

-Publish + execute node và ta sẽ thấy bài viết trên wordpress

<img width="1920" height="992" alt="image" src="https://github.com/user-attachments/assets/7be06890-879b-4622-98d1-82b4c4703017" />

-Node n8n 

<img width="1253" height="307" alt="image" src="https://github.com/user-attachments/assets/ad52b472-52e4-46e3-b6c6-54709fa20379" />

#Nhận xét: Bài làm hay nhất ( do bài này e làm ít lỗi nhất hehe). Theo e thì bài này giúp e học stack các service open source + tự động hóa quy trình. Cũng như hệ thống hoạt động khá ổn và mượt 
