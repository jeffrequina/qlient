# bords-utils
### _A set of utility/helper functions to speed up development_
### _These functions can be used in your React, Vue, Angular and Svelte Projects_


# Usage
## bordsFetch (methodType,apiUrl,authtoken,options) 
  ###### _Save hundred lines of code with this fully flexible promise base fetching method_
  ###### _No Request Headers and Authorization Headers boilerplates needed_
  ###### _just pass it as objects and just wait for the Promise response_
  
  - Shorthand fetch, Easy to call function, just pass in the needed arguments
  - Promise based HTTP client
  - Uses native Fetch API (https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
  - Uses Async/Await internally
  - Can be called anywhere
  - Supports additional Headers and Authentication
  - Supports abort signal/fetch request cancellation (AbortController)
  - No need for Promise chaining and nested fetch
  
  #### constants.js
  ```jsx
  const __GET         = 'GET'
  const __POST        = 'POST'
  const __DELETE      = 'DELETE'
  const __PUT         = 'PUT'
  const __API_HOST    = 'http://localhost:'
  const __API_PORT    = '3000'
  const __API_ROUTE   = '/api/'
  const __BEARER      = 'SecretBearer '
  ...
  ```
  #### your-component.js
  ```jsx
  // Sample Code in React JS
  import * as CONSTANT from 'constants'
  import {bordsFetch} from 'bords-utils'

  const [value,setValue] = useState({})
  useEffect(() => {
      //call with no options, just pass empty object {} to options
      bordsFetch(
        CONSTANT.__GET,
        `${__API_HOST+__API_PORT+__API_ROUTE}getCoffee`,
        `${__BEARER}<api-token>`,
        {},
      ).then(setValue)
  }, [])
  ```

  ```jsx
  //example body options
  const fetchOptions = {body:{
    userId:1,
    title: "foo",
    body: "bar"
    }
  }

  //example with body and headers options
  const fetchOptions = {
    headers:{'Custom-Header': 'hello bords'},
    body:{
      userId  : 1,
      title   : "foo",
      body    : "bar"
    }
  }

  //sample call with fetchOptions
  bordsFetch(
    CONSTANT.__POST,
    `${__API_HOST+__API_PORT+__API_ROUTE}your_api_endpoint`,
    `${__BEARER}<api-token>`,
    fetchOptions,
  )
  ```

  ```jsx
  //sample call with no token and no options
  bordsFetch(
    CONSTANT.__GET,
    `${__API_HOST+__API_PORT+__API_ROUTE}your_api_endpoint`,
    {},
    {},
  )
  ```
---
## getObj (object, array) 
  ###### useful when JSON response "keys" has special character property (eg. _text) which is difficult to navigate using dot notation.
  
  ```sh
  // Example JSON Response
  
  "EmpInfo": {
    "mobileNo": {
      "_text": "12345"
  }
  ```
  ```jsx
  const mobileNumber = getObj(empInfo, ['mobileNo', '_text'])
  ```
---
## getURLParams (props,name)
  ###### function to read URL Query parameters. 
  ###### argument props - is your browser's object that contains history and location.
  ###### argument name - is the URL key (eg. localhost/?Name=bords)
  
  ```jsx
  let queryURL = getURLParams(props,'Name') 
  ```
---
## arrRemove (arr, value)
---
## arrRemoveObj (arrObj,fprop,fval)
---
## arrReverse (arr)
  ###### Reverse array from ascending to descending and vice versa
  ###### Useful for reversing html list elements order inside Object .map

  ```jsx
    const bords = require('bords-utils')
    var arr = [1,2,3,4,5]
    console.log(bords.arrReverse(arr))
  ```
  OR
   ```jsx
    import {arrReverse} from 'bords-utils'
    console.log(arrReverse([1,2,3,4,5]))
  ```
---
## removeItemOnce (arr, value) 
---
## removeItemAll (arr, value)
---
## clearCacheData ()
  ```jsx
  //clears console logs, etc.
  clearCacheData()
  ```
---
## formatDate (date)
  ```jsx
  let today = new Date()
  formatDate(today)
  ```
---
## formateDate2 (datestring)
  ```jsx
  let today = new Date()
  formateDate2(today)
  ```
---
## formatDateMiddleEastern (date)
  ```jsx
  let today = new Date()
  formatDateMiddleEastern(today)

  const expirydate = formatDateMiddleEastern(getObj(data, ['expirydate', '_text']));
  ```
---
## getDayName (dateStr, locale)
  ```jsx
  let today = new Date()
  getDayName(today, 'en-US')
  ```
---
## counterAnimation (id, start, end, duration)
  ```jsx
  import counterAnimation from 'bords-utils'
  counterAnimation("count1", 0, data.total, 2000);

  <div>
    <span id="count1">{data.total}</span>
  </div>
  ```
---
## waitInSeconds (seconds)
  ###### delay timer sometimes comes in handy while processing something on the background

  ```jsx
  waitInSeconds(3000) //delay for 3 seconds
  ```
---

> More features will be added from time to time, please tune in!
