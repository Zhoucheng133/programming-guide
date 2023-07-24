# String与JSON

## 为何需要这样处理？

  很多时候需要存储或者传递JSON的时候无法直接传递，只能通过将其转换为String后再转换

## 将JSON转换为String

  ```js
  // 假设jsonObj为JSON
  var jsonStr = JSON.stringify(jsonObj);
  // ...
  ```

## 将String转换为JSON

  ```js
  var jsonObj = JSON.parse(jsonStr);
  ```

  