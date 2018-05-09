## Reference
- Securing React Redux Apps With JWT Tokens
- A Guide For Building A React Redux CRUD App


## Project Structure
There are 3 pages in application : 
    - An Index page that shows a list of Posts, has route:"/"
    - a Post details page, has route:"/postId"
    - a New Post page, has route:"/new"

Each page has "Success", "Loading" and "Error" phases because they all make AJAX calls to load/delete posts

Divide Each Page Into Components for success phase:
- Index page: PostList, Header
- Post details page: PostDetails, Header
- New post page: PostForm, Header 

for loading phase, no more components, just displaying "loading..."
for error phase, no more components, just displaying error message box.


