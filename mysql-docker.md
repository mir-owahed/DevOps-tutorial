
### Here’s the rewritten docker-compose.yml without the auto-load schema and data moun
...yaml
version: "3.9"

services:
  db:
    image: mysql:8.0
    container_name: mysql_db
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: rootpass      # root password
      MYSQL_DATABASE: sakila             # default database
      MYSQL_USER: admin                  # extra user (optional)
      MYSQL_PASSWORD: admin123           # password for admin
    ports:
      - "3306:3306"
    volumes:
      - mysql_data:/var/lib/mysql

  phpmyadmin:
    image: phpmyadmin:latest
    container_name: pma
    restart: always
    environment:
      PMA_HOST: db             # connect phpMyAdmin to the "db" service
      UPLOAD_LIMIT: 64M        # raise SQL upload limit (default is only 2M)
    ports:
      - "8080:80"
    depends_on:
      - db

volumes:
  mysql_data:
```
```
Now it will only create the MySQL container with the **sakila** database initialized, but without auto-importing schema/data SQL files.

👉 Do you want me to also add a **persistent named volume** for phpMyAdmin sessions/configs, or just keep it stateless (default)?

docker compose up -d

Perfect 🚀 glad you got logged in!

Here’s how you can upload the **Sakila schema + data** using the **phpMyAdmin UI**:

---

### ✅ Steps in phpMyAdmin

1. Open phpMyAdmin in your browser → [http://localhost:8080](http://localhost:8080/).
2. On the **left sidebar**, click on the database `sakila` (which you created via `docker-compose`).
3. At the top, click the **Import** tab.
4. Under **File to Import**:
    - Click **Choose File**.
    - Select your **`sakila-schema.sql`** file first.
    - Leave other options as default (character set: `utf-8`, format: SQL).
5. Scroll down and click **Go**.
    - This will create all the tables, views, and relationships.
6. Repeat the same steps for **`sakila-data.sql`**.
    - This will insert all the sample data (actors, films, rentals, etc.).
```
