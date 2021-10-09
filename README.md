# bords-utils
## _A set of utility/helper functions to speed up development_

## Function Reference

- getObj (object, array)
- getURLParams (props,name)
- arrRemove (arr, value)
- arrRemoveObj (arrObj,fprop,fval)
- arrReverse (arr)
- clearCacheData ()
- formatDate (date)
- formateDate2 (datestring)
- formatDateMiddleEastern (date)
- getDayName (dateStr, locale)
- counterAnimation (id, start, end, duration)
- waitInSeconds (seconds)
- removeItemOnce (arr, value) 
- removeItemAll (arr, value)

## Usage


```sh
const bords = require('bords-utils')
var arr = [1,2,3,4,5]
var date = new Date()
console.log(bords.arrReverse(arr))
console.log(bords.formatDate(date))
```

> More functions will be added in the next release
> including a generic async fetch function that accepts
> generic request headers with authentication token
> and returns a promise.
