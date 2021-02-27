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
```SQL
