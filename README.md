# use cases:

signup, login, logout, **create post**, delete post, **play video in posts**, comment, like, repost, share, **follow**, **unfollow**, message, for you(recommendation), nearby posts, my following, my followers, search for posts/users, activate, inactivate

sorted by priority:

1. create post, follow, unfollow, play video in posts, delete posts
2. signup, login, logout, my following, followers
3. comment, like, repost, share
4. posts recommendation, nearby posts

# API Design

## 1. Posts

### 1.1 creat a post

> POST	/v1/posts/{post_id}/create

create a post with a specific id

*Path Parameters:*

- post_id: id of the new post

*Request Body:*

- user_id(string)
- message(string): the text message of the new post
- lat(double): latitude of the current login user
- lon(double): longitude of the current login user

*Sample Request:*

```json
curl -v -X POST https://api.MyTwitter.com/v1/posts/{post_id}/create \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <Access-Token>" \
-d '{
    "user_id" : xxxx
    "message" : Hello World
    "lat" : 127.8
    "lon" : 280.3
}'
```

*Response：*

A successful request returns the HTTP *201 Created* status code

### 1.2 delete a post

> DELETE	/v1/posts/{post_id}

delete a post with a specific id

*Path Parameters:*

- post_id: id of the post to be deleted

*Sample Request:*

```json
curl -v -X  https://api.MyTwitter.com/v1/posts/{post_id} \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <Access-Token>" \
```

*Response:*

A successful request returns the HTTP *204 No Content* status code

### 1.3 comment

> POST	/v1/posts/{post_id}/comment

write comments to a specific post

*Path Parameters:*

- post_id: id of the post to be commented

*Requst Body:*

- user_id(string): id of the user that's performing the 'comment' action
- comment(string): content of the comment
- lat(double): latitude of the current commenting user
- lon(double): longitude of the current commenting user

*Sample Requst:*

```json
curl -v -X POST https://api.MyTwitter.com/v1/posts/{post_id}/comment \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <Access-Token>" \
-d '{
    "user_id" : xxxx
    "comment" : I really like the content
    "lat" : 127.8
    "lon" : 280.3
}'
```

*Response:*

A successful request returns the HTTP *204 No Content* status code

### 1.4 like

> POST	/v1/posts/{post_id}/like

mark a specific post as my like

### 1.5 repost

> POST	/v1/posts/{post_id}/repost

repost a specific post

### 1.6 share

> POST	/v1/posts/{post_id}/share

share a specific post to a social media platform

### 1.7 play video in posts

> POST	/v1/posts/{post_id}/play

play the video in a specific post

Response:

```json
{
    "url" : "xxxxxx.com"
}
```

A successful request returns the url of the actual video and the user side makes another request to the video url.

## 2. Users

### 2.1  signup

> POST	/v1/users/signup

signup

### 2.2 login

> POST	/v1/users/login

### 2.3 logout

> POST	/v1/users/logout

### 2.4 my following

> GET	/v1/users/{user_id}/following

get a list of the users that the specific user is following

### 2.5 followers

> GET	/v1/users/{user_id}/followers

get a list of the users that are following the specific user

### 2.6 follow

> POST	/v1/users/{user_id}/followers

follow a user

*Path Parameters:*

- user_id(string): the user that is performing the 'follow' action

*Request Body:*

- target_user_id(string): the id of the target user to be followed

*Sample Request:*

```json
curl -v -X POST https://api.MyTwitter.com/POST/v1/users/{user_id}/followers \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <Access-Token>" \
-d '{
	"target_user_id" : xxxxx
}'
```

*Response:*

- following(boolean) : represents whether the follow action is successful, true for successful

*Sample Response-successful:*

```json
{
	"following" : true
}
```



### 2.7 unfollow

> DELETE	/v1/users/{user_id}/followers

unfollow a user

*Path Parameters:*

- user_id(string): the user that is performing the 'unfollow' action

*Request Body:*

- target_user_id(string): the id of the target user to be unfollowed

*Sample Request:*

```json
curl -v -X POST https://api.MyTwitter.com/DELETE/v1/users/{user_id}/followers \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <Access-Token>" \
-d '{
	"target_user_id" : xxxxx
}'
```

*Response:*

- following(boolean) : represents whether the unfollow action is successful, false for successful

*Sample Response-successful:*

```json
{
	"following" : false
}
```

