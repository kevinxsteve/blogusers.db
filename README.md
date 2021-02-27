# blogusers.db
A database of Entities Posts, Author, Tags, Tagsposts for a Blog
```SQL
CREATE TABLE authors (
  author_id INTEGER PRIMARY KEY, name TEXT NOT NULL, 
  email TEXT UNIQUE NOT NULL
);
CREATE TABLE posts(
  post_id INTEGER PRIMARY KEY, 
  title TEXT UNIQUE NOT NULL, 
  created_at DATE NOT NULL, 
  author_id INTEGER NOT NULL, 
  FOREIGN KEY(author_id) REFERENCES authors(author_id)
);
CREATE TABLE tags(
  tag_id INTEGER PRIMARY KEY, tagname TEXT UNIQUE NOT NULL
);
CREATE TABLE tagsposts (
  tagsposts_id INTEGER PRIMARY KEY, 
  tag_id INTEGER NOT NULL, 
  post_id INTEGER NOT NULL, 
  FOREIGN KEY (tag_id) REFERENCES tags(tag_id), 
  FOREIGN KEY (post_id) REFERENCES posts(post_id)
);
```
```SQL
INSERT INTO authors (name, email) VALUES ("Henri", "henri@hello.de"), ("Adrian", "adrian@hello.de"), ("Filippo", "filippo@hello.de"), ("Nick", "nick@hello.de");
INSERT INTO posts (title, created_at, author_id) VALUES ("Lorem", Date("now"), 1), ("Ipsum", Date("now"), 2), ("Sit", Date("now"), 3), ("Dolor", Date("now"), 4);
INSERT INTO tags(tagname) VALUES ("DYI"), ("LOL"), ("Cooking"), ("Selfmade");
INSERT INTO tagsposts (tag_id, post_id) VALUES (1,1), (2,1), (1,2), (3,2), (3,3), (4,4);
```

```SQL
SELECT title, created_at, name, tagname FROM posts
INNER JOIN authors ON posts.author_id = authors.author_id
INNER JOIN tagsposts ON tagsposts.post_id = posts.post_id
INNER JOIN tags ON tagsposts.tag_id = tags.tag_id;
```
