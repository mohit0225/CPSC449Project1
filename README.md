
# CPSC 449 Web Backend Engineering
## Project-1
### Project Members:
*  (@csu.fullerton.ed) | Role: Ops
* Mohit Kumar (mohit_kumar@csu.fullerton.edu) | Role: Dev
* Emily Pham (tpham523@csu.fullerton.edu) | Role: SDET

Installations:pip3 install flask, sudo apt install --yes gunicorn3


#### ---------------------------------- Dev Ops-------------------------------------------
1) Use this code for generating 3 instance of foreman in a terminal
```
foreman start -m post=3,vote=3
```

2) In separate terminal run
```
ulimit -n 8192 && caddy
```

3) Then go to localhost:2015/posts or localhost:2015/votes
ex: to get all post in Database run
http://localhost:2015/posts/filter

#### ---------------------------------- Post API-------------------------------------------
1. Create a new post: Send a POST request to route of create_post() fn
> 
```
Example request:
curl -i -X POST -H 'Content-Type:application/json' -d '{"title":"Test post", "description":"This is a test post", "username":"some_guy_or_gal", "community_name":"449"}' http://localhost:2015/posts/create;
```

2. Delete an existing post: Send a GET request to route of delete_post() fn
```
Example request:
curl -i -X DELETE http://localhost:2015/posts/delete?post_id=4;
```

3. Retrieve an existing post: Send a GET request to route of get_post() fn
```
Example request:
curl -i http://localhost:2015/posts/get?post_id=2;
```

4. List the n most recent posts to a particular community: Send a GET request to route of get_posts_filter() fn with args (community_name and n)
```
Example request:
curl -i http://localhost:2015/posts/filter?n=2&community_name=calculus;
```

5. List the n most recent posts to any community: Send a GET request to route of get_posts_filter() fn with args (n)
```
Example request:
curl -i http://localhost:2015/posts/filter?n=2;
```

#### ---------------------------------- Vote API-------------------------------------------



1) Upvote a post:
```
Example request:
curl -i -X POST -H "Content-Type: application/json" -d '{"vote_id":"2"}' 'http://127.0.0.1:5000/upvotes'
```

2) Downvote a post:
```
Example request:
curl -i -X POST -H "Content-Type: application/json" -d '{"vote_id":"2"}' 'http://127.0.0.1:5000/downvotes'
```

3) Report the number of upvotes and downvotes for a post:
```
Example request:
curl -i 'http://localhost:2015/votes/get?vote_id=2';
```

4) List the n top-scoring posts to any community:
```
Example request:
curl -i 'http://localhost:2015/votes/getTop?n=3';
```

5) Given a list of post identifiers, return the list sorted by score.:
```
Example request:
curl -i -X POST -H "Content-Type: application/json" -d '{"post_ids":["1","3"]}' 'http://127.0.0.1:5000/getList'
```

#### ---------------------------------- TESTING -------------------------------------------

#### ---------------------------------- UNIT TESTING --------------------------------------
We use Tavern to test each service. Test files are located under 'tests'

1) How to install Tavern
```
pip3 install tavern[pytest]
```

2) How to run test

```
py.test test_posting.tavern.yaml
py.test test_voting.tavern.yaml
```
 
#### ---------------------------------- Load Testing -------------------------------------------

We use a framework called Locust to perform load test.
We also use faker package to generate fake data for random testing.

1) How to install faker
```
pip3 install faker
```

2) How to install locust
```
pip3 install locustio
```

3) How to run test
####  ----- Post API -----
```
locust -f tests/postLocustFile.py --host=http://localhost:2015/posts --no-web -c 100 -r 10

# -c 100: # of users to be simulated. Here, it's 100 users
# -r 50: the rate of # users spawned per second. Here, it's 50 users per second.
```

#### ----- Vote API -----

```
locust -f tests/voteLocustFile.py --host=http://localhost:2015/votes --no-web -c 100 -r 10
```
