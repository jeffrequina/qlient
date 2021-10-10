# bords-utils
## _A set of utility/helper functions to speed up development_

## Function Reference

##### _These functions can be used in your React, Vue, Angular and Svelte Projects_

###### getObj (object, array) 
  - useful when JSON response "key" has special character property (eg. _text) which is difficult to navigate using dot notation. 
  
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
###### arrRemove (arr, value)
###### arrRemoveObj (arrObj,fprop,fval)
###### arrReverse (arr)
  - Reverse array from ascending to descending and vice versa
  - Useful for reversing html list elements order inside Object .map
###### removeItemOnce (arr, value) 
###### removeItemAll (arr, value)
###### clearCacheData ()
  ```jsx
  //clears console logs, etc.
  clearCacheData()
  ```
###### formatDate (date)
  ```jsx
  let today = new Date()
  formatDate(today)
  ```
###### formateDate2 (datestring)
  ```jsx
  let today = new Date()
  formateDate2(today)
  ```
###### formatDateMiddleEastern (date)
  ```jsx
  let today = new Date()
  formatDateMiddleEastern(today)

  const expirydate = formatDateMiddleEastern(getObj(data, ['expirydate', '_text']));
  ```
###### getDayName (dateStr, locale)
  ```jsx
  let today = new Date()
  getDayName(today, 'en-US')
  ```
###### counterAnimation (id, start, end, duration)
  ```jsx

  ```
###### waitInSeconds (seconds)
    - delay timer sometimes comes in handy while processing something on the background

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

> More functions will be added in the next release
> including a generic async fetch function that accepts
> generic request headers with authentication token
> and returns a promise.
