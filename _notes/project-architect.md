## Reference
- A Guide For Building A React Redux CRUD App
    - https://medium.com/@rajaraodv/a-guide-for-building-a-react-redux-crud-app-7fe0b8943d0f

## Steps
- STEP 1 — Write Detailed Mocks For Each Page And Phases.
- STEP 2 — Divide Each Page Into Components
- STEP 3 — List State and Actions For Each Component (AND For Each Phase)
- STEP 4 — Create Action Creators For Each Action
- STEP 5 — Write Reducers For Each Action
- STEP 6 — Implement Every Presentational Component
- STEP 7 — Create Container Component For Some/All Presentational Component
- STEP 8 — Finally Bring Them All Together

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