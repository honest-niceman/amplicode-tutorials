## Инициализация схемы БД

```bash
psql postgresql://root:root@localhost:5432/blog

CREATE TABLE posts (
  id BIGINT GENERATED BY DEFAULT AS IDENTITY NOT NULL,
   created_by VARCHAR(255),
   created_date TIMESTAMP WITHOUT TIME ZONE,
   last_modified_by VARCHAR(255),
   last_modified_date TIMESTAMP WITHOUT TIME ZONE,
   title VARCHAR(255) NOT NULL,
   text OID NOT NULL,
   published_at TIMESTAMP WITHOUT TIME ZONE,
   author_id BIGINT NOT NULL,
   CONSTRAINT pk_posts PRIMARY KEY (id)
);

CREATE TABLE users (
  id BIGINT GENERATED BY DEFAULT AS IDENTITY NOT NULL,
   created_by VARCHAR(255),
   created_date TIMESTAMP WITHOUT TIME ZONE,
   last_modified_by VARCHAR(255),
   last_modified_date TIMESTAMP WITHOUT TIME ZONE,
   first_name VARCHAR(255) NOT NULL,
   last_name VARCHAR(255) NOT NULL,
   CONSTRAINT pk_users PRIMARY KEY (id)
);

CREATE INDEX idx_user_names ON users(first_name, last_name);

ALTER TABLE posts ADD CONSTRAINT FK_POSTS_ON_AUTHOR FOREIGN KEY (author_id) REFERENCES users (id);

\q
```