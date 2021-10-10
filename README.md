# bords-utils
## _A set of utility/helper functions to speed up development_

## Function Reference

##### _These functions can be used in your React, Vue, Angular and Svelte Projects_

###### bordsFetch (methodType,apiUrl,authtoken,options) 
  - Fully flexible promise base fetching method

  ```jsx
  constants.js
  const __GET         = 'GET'
  const __POST        = 'POST'
  const __DELETE      = 'DELETE'
  const __PUT         = 'PUT'
  const __API_HOST    = 'http://localhost:'
  const __API_PORT    = '3000'
  const __API_ROUTE   = '/api/'
  const __BEARER      = 'SecretBearer '
  ...

  // Sample Code in React
  import * as CONSTANT from 'constants'
  import {bordsFetch} from 'bords-utils'

  const [value,setValue] = useState({})
  useEffect(() => {
      //call with no options, just pass {}
      bordsFetch(
        CONSTANT.__GET,
        `${__API_HOST+__API_PORT+__API_ROUTE}getCoffee`,
        `${__BEARER}<api-token>`,
        {},
      ).then(setValue)
  }, [])

  //sample call with options
  const fetchOptions = {body:{id,variance},};
  bordsFetch(
    CONSTANT.__POST,
    `${__API_HOST+__API_PORT+__API_ROUTE}your_api_endpoint`,
    `${__BEARER}<api-token>`,
    fetchOptions,
  )
  
  //sample call with no token
  bordsFetch(
    CONSTANT.__GET,
    `${__API_HOST+__API_PORT+__API_ROUTE}your_api_endpoint`,
    {},
    {},
  )
  ```

###### getObj (object, array) 
  - useful when JSON response "keys" has special character property (eg. _text) which is difficult to navigate using dot notation. 
  
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
###### getURLParams (props,name)
  - function to read URL Query parameters. 
  - props argument is your browser's object that contains history and location.
  - name argument is the URL key (eg. localhost/?Name=bords)
  
  ```jsx
  let queryURL = getURLParams(props,'Name') 
  ```
---
###### arrRemove (arr, value)
---
###### arrRemoveObj (arrObj,fprop,fval)
---
###### arrReverse (arr)
  - Reverse array from ascending to descending and vice versa
  - Useful for reversing html list elements order inside Object .map
---
###### removeItemOnce (arr, value) 
---
###### removeItemAll (arr, value)
---
###### clearCacheData ()
  ```jsx
  //clears console logs, etc.
  clearCacheData()
  ```
---
###### formatDate (date)
  ```jsx
  let today = new Date()
  formatDate(today)
  ```
---
###### formateDate2 (datestring)
  ```jsx
  let today = new Date()
  formateDate2(today)
  ```
---
###### formatDateMiddleEastern (date)
  ```jsx
  let today = new Date()
  formatDateMiddleEastern(today)

  const expirydate = formatDateMiddleEastern(getObj(data, ['expirydate', '_text']));
  ```
---
###### getDayName (dateStr, locale)
  ```jsx
  let today = new Date()
  getDayName(today, 'en-US')
  ```
---
###### counterAnimation (id, start, end, duration)
  ```jsx
  import counterAnimation from 'bords-utils'
  counterAnimation("count1", 0, data.total, 2000);

  <div>
    <span id="count1">{data.total}</span>
  </div>
  ```
---
###### waitInSeconds (seconds)
    - delay timer sometimes comes in handy while processing something on the background
---
## Usage
  ```jsx
  const bords = require('bords-utils')
  var arr = [1,2,3,4,5]
  var date = new Date()
  console.log(bords.arrReverse(arr))
  console.log(bords.formatDate(date))
  ```
  OR
  ```jsx
  import {arrReverse} from 'bords-utils'
  console.log(arrReverse([1,2,3,4,5]))
  ```
---
> More functions will be added in the next release
> including a generic async fetch function that accepts
> generic request headers with authentication token
> and returns a promise.
