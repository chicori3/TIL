## 4. 클로저

### 4-1. 클로저의 개념

```javascript
function outerFunc() {
  var x = 10;
  var innerFunc = function () {
    console.log(x);
    return innerFunc;
  };
}

var inner = outerFunc();
inner(); // 10
```
