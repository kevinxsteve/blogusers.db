# blogusers.db
A database of Entities Posts, Author, Tags, Tagsposts for a Blog
User Blog

- Name, Email, Creator | Author
- Title, CreatedAt, Tags

## ER

where to do it:
https://mermaid-js.github.io/mermaid-live-editor/#/

```ER
erDiagram
Author |{--o{ Post: has    
Post |{--o{ Tag: may_have    
    Author{
        string name
        string email
    }
    Post{
    string title
    int createdAt
    }
    Tag{
    string tagname
    }
 ```
    
    
[![](https://mermaid.ink/img/eyJjb2RlIjoiZXJEaWFncmFtXG5BdXRob3IgfHstLW97IFBvc3Q6aGFzICAgIFxuUG9zdCB8ey0tb3sgVGFnOiBtYXlfaGF2ZSAgICBcbiAgICBBdXRob3J7XG4gICAgICAgIHN0cmluZyBuYW1lXG4gICAgICAgIHN0cmluZyBlbWFpbFxuICAgIH1cbiAgICBQb3N0e1xuICAgIHN0cmluZyB0aXRsZVxuICAgIGludCBjcmVhdGVkQXRcbiAgICB9XG4gICAgVGFne1xuICAgIHN0cmluZyB0YWduYW1lXG4gICAgfSIsIm1lcm1haWQiOnt9LCJ1cGRhdGVFZGl0b3IiOmZhbHNlfQ)](https://mermaid-js.github.io/mermaid-live-editor/#/edit/eyJjb2RlIjoiZXJEaWFncmFtXG5BdXRob3IgfHstLW97IFBvc3Q6aGFzICAgIFxuUG9zdCB8ey0tb3sgVGFnOiBtYXlfaGF2ZSAgICBcbiAgICBBdXRob3J7XG4gICAgICAgIHN0cmluZyBuYW1lXG4gICAgICAgIHN0cmluZyBlbWFpbFxuICAgIH1cbiAgICBQb3N0e1xuICAgIHN0cmluZyB0aXRsZVxuICAgIGludCBjcmVhdGVkQXRcbiAgICB9XG4gICAgVGFne1xuICAgIHN0cmluZyB0YWduYW1lXG4gICAgfSIsIm1lcm1haWQiOnt9LCJ1cGRhdGVFZGl0b3IiOmZhbHNlfQ)

## SQL Model

Single SQL file




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
# Querying the title, created_at, name, tagname
```SQL
SELECT title, created_at, name, tagname FROM posts
INNER JOIN authors ON posts.author_id = authors.author_id
INNER JOIN tagsposts ON tagsposts.post_id = posts.post_id
INNER JOIN tags ON tagsposts.tag_id = tags.tag_id;
```
or another way would be
```SQL
select title, tagname, name, created_at from tagsposts
inner join tags on tagsposts.tag_id = tags.tag_id
join posts on tagsposts.post_id = posts.post_id
join authors on posts.author_id = authors.author_id;
```
or an easier way would be
```SQL
SELECT title, created_at, name, tagname FROM posts
JOIN authors using (author_id)
JOIN tagsposts using (post_id)
JOIN tags using (tag_id);
```
# Querying the title, tagname
```SQL
select title,tagname from tagsposts
join tags using (tag_id)
join posts using (post_id);
```
or another way
```SQL
select title, tagname from tagsposts
inner join tags on tagsposts.tag_id = tags.tag_id
join posts on tagsposts.post_id = posts.post_id;
```

