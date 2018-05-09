## Reference
    - A Guide For Building A React Redux CRUD App
    

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
Redux provides a function called __"dispatch"__ which allows us to pass the “Action” JSON object to all other components. Dispatching an Action means simply calling the dispatch function w/ the action JSON object.

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
    - "FETCH_OBJ”(for loading)"
    - "FETCH_OBJ_SUCCESS"" 
    - "FETCH_OBJ_FAILURE" 
    - "OBJ_RESET"(to cleanup dirty previous state).