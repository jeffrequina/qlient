### _A set of utility/helper functions to speed up development_
### _Use this in your React, Vue, Angular, Solid, & Svelte Projects_

# Installation
```jsx
  npm i bords-utils
```

## bordsFetch ( methodType, apiUrl, authtoken, options, signal )   
  
  ### _More Cleaner, More Modern & Concise Fetch! NO BOILERPLATE NEEDED!_
  
  #### Key Features
  - Save hundred lines of code setting up fetching method boilerplates
  - Easy to use Promise based HTTP client, shorthand fetch
  - Uses native Fetch API (https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
  - Uses Async/Await internally
  - Can be called anywhere (eg. helpers, components and state manager)
  - Supports additional arguments for Headers and Authentication
  - Supports abort signal/fetch request cancellation (AbortController)
  - Supports Promise chaining or nested fetch
  - Auto-detects API response between json and plain text

  ### Basic Usage
  ```jsx
    bordsFetch('GET','https://jsonplaceholder.typicode.com/posts/1',{},{},{})
    .then(res => console.log(res))

    // OR Async/Await below:

    const fetchData = async () => {
      let result = await bordsFetch('GET','https://jsonplaceholder.typicode.com/posts/1',{},{},{})
      console.log({result})
    }
  ```

  ### Advance Usage
  #### constants.js
  ```jsx
    export const __API_ROUTE   = 'http://localhost:3000/api'
    export const __BEARER      = 'SecretBearer '
    ...
  ```
  #### your-component.js
  ```jsx
    // Sample Code in React JS
    import * as CONSTANT from 'constants'
    import { bordsFetch } from 'bords-utils'

    const [value,setValue] = useState({})
    useEffect(() => {
        //call with no options, just pass empty object {} to token, options & signal
        bordsFetch(
          'GET',                                // request method
          `${CONSTANT.__API_ROUTE}/gettodos`,   // api URL
          `${CONSTANT.__BEARER}<api-token>`,    // Bearer Token
          {},                                   // fetch options, body AND/OR headers
          {}                                    // signal
        ).then(setValue)
    }, [])
  ```

  #### Other example usage:
  ```jsx
  //example body options
  const fetchOptions = {
    body:{
      userId  : 1,
      title   : "foo",
      body    : "bar"
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
    'POST',
    `${CONSTANT.__API_ROUTE}/your_api_endpoint`,
    `${CONSTANT.__BEARER}<api-token>`,
    fetchOptions,
    {}).then(...)
  ```

  ```jsx
  //sample call with no token, no options, & no signal
  bordsFetch('GET',`${CONSTANT.__API_ROUTE}/your_api_endpoint`,{},{},{}).then(...)
  ```

  ```jsx
  //sample call for Request Cancellation or Aborting Signal
  const controller = new AbortController()
  const signal = controller.signal
  ...
  bordsFetch('GET',`${CONSTANT.__API_ROUTE}/your_api_endpoint`,{},{},{signal}).then(...)
  ...
  //calling abort() cancels the fetch request
  controller.abort() 
  ```

  #### helper-sample.js
  ```jsx
  //sample call inside an external helper
  export const fetchDDLOptions = async (authToken) => {  
    try {   
      let ddlOptions = [];    

      bordsFetch(
        'POST', 
        `${CONSTANT.__API_ROUTE}/your_api_endpoint`, 
        `${CONSTANT.__BEARER}${authToken}`, 
        {},
        {}).then(items=> {      
              items.forEach(element => {
                let ddlList = { value: element["id"], label: element["description"] }
                ddlOptions.push(ddlList)          
              });
            }) 
      return ddlOptions

    } catch (err) { console.log(err) }
  }
  ```

  #### async-helper-sample.js
  ```jsx
  //sample call inside an external helper with async/await function
  export const fetchUserCount = async (authToken, userID, userName) => {  
    try {   
      const fetchOptions = {body: {userID,userName},};

      let result = await bordsFetch(
        'POST', 
        `${CONSTANT.__API_ROUTE}/your_api_endpoint`, 
        `${CONSTANT.__BEARER}${authToken}`, 
        fetchOptions,
        {})

      return result[0]

    } catch (bords_err) { console.log(bords_err) }
  }
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
###### Remove a value in an array.
---
## arrRemoveObj (arrObj,fprop,fval)
###### Remove a value in an array object base of prop and value
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
## toggleInt (int)
  ```jsx
    toggleInt(1) //returns 0
    toggleInt(0) //returns 1
  ```
---
## toggleBoolean (bool)
  ```jsx
    toggleBoolean(false) //returns true
    toggleBoolean(true) //returns false
  ```
---
## capitalizeFirstLetter (stringVal)
  ```jsx
    capitalizeFirstLetter('THE QUICK BROWN FOX') //returns 'The Quick Brown Fox'
    capitalizeFirstLetter('the quick brown fox') //returns 'The Quick Brown Fox'
  ```
---
## extractTime (timeStamp)
  ```jsx
    extractTime("2021-11-01T11:33:29.320+04:00") //returns 11:33:29 AM
  ```
---
## calcPercOnNum (x,y)
  ```jsx
    calcPercOnNum(10,10) returns 100
    calcPercOnNum(50,100) returns 50
  ```
---
## getTotalSecondsByTimeDiff (startTime, endTime)
  ```jsx
    let inTime = "06:30:04"
    let outTime = "16:04:14"
    getTotalSecondsByTimeDiff(inTime,outTime)

    //1 day is to 86400 seconds
    //8 Hours of work is to 28800 seconds
    calcPercOnNum(getTotalSecondsByTimeDiff(inTime, outTime), 28800).toFixed(0) + '%' //returns 120%
  ```
---

> More features will be added from time to time, please tune in!
