# flask-tutorial-corey-schafer

I'm using this repo as a place to store my code as I work through the Corey Schafer Flask tutorial on YouTube. Mostly for my own reference in the future.

## Tutorials I've Worked Through

- Part 1 - Getting Started: https://www.youtube.com/watch?v=MwZwr5Tvyxo
- Part 2 - Templates: https://www.youtube.com/watch?v=QnDWIZuWYW0
- Part 3 - Forms and User Input: https://www.youtube.com/watch?v=UIJKdCIEXUQ
- Part 4 - Database with Flask-SQLAlchemy: https://www.youtube.com/watch?v=cYWiDiIUxQc

## Testing the DB in Part 4

Adding data in `python` repl:

```
from flask_app import db
db.create_all()
from flask_app import User, Post
user_1 = User(username='Corey', email='C@demo.com', password='password')
db.session.add(user_1)
user_2 = User(username='JohnDoe', email='jd@demo.com', password='password')
db.session.add(user_2)
db.session.commit()
```

```
user = User.query.get(1)
post_1 = Post(title='Blog 1', content='First Post Content!', user_id=user.id)
post_2 = Post(title='Blog 2', content='Second Post Content!', user_id=user.id)
db.session.add(post_1)
db.session.add(post_2)
db.session.commit()
```

Querying the seeded data (again in `python` repl):

```
User.query.all()
-> [User('Corey', 'C@demo.com', 'default.jpg'), User('JohnDoe', 'jd@demo.com', 'default.jpg')]
```

```
User.query.first()
-> User('Corey', 'C@demo.com', 'default.jpg')
```

```
User.query.filter_by(username='Corey').all()
-> [User('Corey', 'C@demo.com', 'default.jpg')]
```

```
User.query.filter_by(username='Corey').first()
-> User('Corey', 'C@demo.com', 'default.jpg')
```

```
user = User.query.filter_by(username='Corey').first()
user
-> User('Corey', 'C@demo.com', 'default.jpg')

user.id
-> 1
```

```
user = User.query.get(1)
user
-> User('Corey', 'C@demo.com', 'default.jpg')

user.posts    # before seeding the post data (above)
-> []     

user.posts    # after seeding the post data (above)
-> [Post('Blog 1', '2022-03-02 09:13:37.712607'), Post('Blog 2', '2022-03-02 09:13:37.719281')]
```

```
post = Post.query.first()
post.author
-> User('Corey', 'C@demo.com', 'default.jpg')
```

Tidying up, dropping the test data and re-creating the tables:

```
db.drop_all()
db.create_all()
```