## Reference
    - A Guide For Building A React Redux CRUD App
        - https://medium.com/@rajaraodv/a-guide-for-building-a-react-redux-crud-app-7fe0b8943d0f

## Key points
    - Reducers
    - Actions
    - Middlewares
    - Stores
    - Making async requests and handling responses


Every component does two things:
1. Listen to the user and server events and send them to JS functions. In Redux, events are represented as a JSON object called __"Actions"__.
```
    {"type": "FETCH_POST", "id": 1234} // <-- Action
```

2. Render DOM based on some data. This data is called a __"state"__, which is also a JSON object.
```
    {"post": {"id": 1234, "title": "My Redux Post"}} // <-- state
```

These are functions that listen to DOM or server events and return formal JSON __"Action"__ object.
```
    function fetchPost(id) {
        return {
            type: FETCH_POST,
            result: makeServerRequest("http://postsServer.com/api/id")
        };
    }
```
Redux provides a function called __"dispatch"__ which allows us to pass the "Action" JSON object to all other components. Dispatching an Action means simply calling the dispatch function w/ the action JSON object.

```
    // Call the "Action Creator" and then use it's return value (Action JSON object) to finally dispatch it to "reducers"
    dispatch(fetchPost(id)) 
    or 
    dispatch({type:"FETCH_POST", id:1234})

```

__Reducers__ are functions that take an Action and the current state that was sent to them via "dispatch", apply action to the current state and return a new state. And Redux re-renders all components whenever there is a new state.

```
    //If the action is FETCH_POST_SUCCESS, return a new "activePost" state with new post)
    case FETCH_POST_SUCCESS:
    return {activePost: {post: action.payload.data, error:null,     
                        loading: false}};
```
        
## Dealing With Async Actions
If component is loading an object(e.g. list of Posts) via AJAX call to the server, that object’s state should keep track of all the potential states. Initial state for such objects should look like: 
```
    {
        objName: 
        {
            obj:null, loading: false, error:null
        }
    }
```
Further, such components should dispatch up to 4 actions such as 
    - "FETCH_OBJ"(for loading)"
    - "FETCH_OBJ_SUCCESS"" 
    - "FETCH_OBJ_FAILURE" 
    - "OBJ_RESET"(to cleanup dirty previous state).

Sample of postlist:
    - FETCH_POSTS
```
    export function fetchPosts() {
        const request = axios.get(`${ROOT_URL}/posts`);
        return {
            type: FETCH_POSTS,
            payload: request
        };
    }
```
    - FETCH_POSTS_SUCCESS
```
    export function fetchPostsSuccess(posts) {
        return {
            type: FETCH_POSTS_SUCCESS,
            payload: posts
        };
    }
``` 
    - FETCH_POSTS_FAILURE
```
    export function fetchPostsFailure(error) {
        return {
            type: FETCH_POSTS_FAILURE,
            payload: error
            };
    }
```

## "Presentational" and "Container" Components
Reducers are functions that take "state" from Redux and "action" JSON object and returns a new "state" to be stored back in Redux.
1. Reducer functions are called by the "Container" containers when there is a user or server action.
2. If the reducer changes the state, Redux passes the new state to each component and React re-renders each component

Keeping React and Redux logic inside each component can make it messy, so Redux recommends creating a dummy presentation only component called "Presentational" component and a parent wrapper component called "Container" component that deals with Redux, dispatch "Actions" and more. 
 
The parent Container then passes the data to the presentational component, handle events, deal with React on behalf of Presentational component.

Take the PostsListContainer as a sample, 
```
const mapStateToProps = (state) => {
  return { 
    posts: state.posts.postsList.posts,
  };
}

const mapDispatchToProps = (dispatch) => {
  return {
    fetchPosts: () => {
      dispatch(fetchPosts()).then((response) => {
            !response.error ? dispatch(fetchPostsSuccess(response.payload.data)) : dispatch(fetchPostsFailure(response.payload.data));
          });
    }
  }
}

export default connect(mapStateToProps, mapDispatchToProps)(PostsList);
```
PostsListContainer keeps track of "postList" global Redux state and passes "post" and "loading" to presentational.
