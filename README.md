### _Promise based HTTP Client for all your API invocation needs_
### _Use this in your React, Vue, Angular, Solid, Svelte or any Javascript Projects_

# Installation
```jsx
  npm i qlient
```

## qlient( methodType, apiUrl, bearerName?, authtoken?, options?, signal? )   
  
  ### _More Cleaner, More Modern & Concise Fetch! NO BOILERPLATE NEEDED!_
  ### _(Lightweight) 100% native Fetch — dependency FREE!_
  ### _Production Grade API Query Client a.k.a qlient_
  
  #### Key Features
  - Save hundred lines of code setting up fetching method boilerplates
  - Easy to use Promise based HTTP client, shorthand fetch
  - Uses native Fetch API (https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
  - Invoke anywhere (eg. handlers, external helpers, components and state manager)
  - Supports additional arguments for Headers and Authentication
  - Supports abort signal/fetch request cancellation (AbortController) so you can cancel the request when the component is unmounted
  - Supports all standard HTTP methods
  - Supports Promise chaining or nested fetch
  - Auto-detects responses between json and plain text
  - Fully typed methods and responses
  - Cookies included in every request

  ### Basic Usage (using only required parameters `methodType` `apiUrl`)
  ```tsx
    // constants.ts
    const GET = "GET"
    
    // your endpoint URL
    const apiUrl = getEndpointURL()

    // invoke an API call
    const fetchPost = async () => {
      const res = await qlient({
        methodType: GET,
        apiUrl,
      })
      console.log({ res })
    }

    // Or if you prefer chaining
    qlient({ methodType: GET, apiUrl })
    .then(res => console.log({res}))
  ```

  ### Advance Usage (using parameters `bearerName` `authtoken` `options`)
  ```tsx
    export const addPost = async () => {
      const methodType = HTTP_METHODS.POST
      const bearerName = getYourBearerNameHere()
      const apiUrl = getEndpointURL()
      const authtoken = getYourTokenFromHere()
      const options = {
        body: {
          userId: 1,
          title: "foo",
          body: "bar",
        },
      }

      return await qlient({
        methodType,
        apiUrl,
        bearerName,
        authtoken,
        options,
      })
    }
  ```

  #### Other example usage
  ```tsx
  //example with body and extra custom header
  const options = {
    headers:{'Custom-Header': 'your_string_value_here'},
    body:{
      userId  : 1,
      title   : "foo",
      body    : "bar"
    }
  }

  // sample with Query Parameters
  const options = {
    queryParams: {
        user_id: userId,
        order_id: orderID,
    },
  }

  //sample call with custom options
  let res = await qlient({
    methodType: HTTP_METHODS.POST,
    apiUrl,
    bearerName,
    authtoken,
    options, // pass options here
  })

  console.log({ res })
  ```

  ### Usage with Signals (cancel pending queries when component unmounts)
  ```tsx
    // Docs: ( https://developer.mozilla.org/en-US/docs/Web/API/AbortController )
    // Initialize controller for aborting pending requests
    const controller = new AbortController()
    const signal = controller.signal
    ...
    qlient({ methodType: GET, apiUrl, signal })
    ...
    //calling abort() cancels the fetch request
    controller.abort() 
  ```


> More features will be added from time to time, please tune in!
* Automatic retry logic
* Timeout feature (request automatically aborts after 10 seconds?)
* Easy integration with React Query for caching and background refetching
* Interceptors
