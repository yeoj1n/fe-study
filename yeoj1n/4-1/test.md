
## 오브젝트 속성이나 배열 항목을 반복할 때 사용하는 언어 구문은 무엇인가요?

### 오브젝트
- for in
- Object.keys(), Object.getOwnPropertyNames()
```
const obj = {a:1, b:2};
for (let property in obj) {
    console.log(property);
}

Object.keys(obj);
Object.getOwnPropertyNames(obj);

```

### 배열
- for 
- forEach
- for of
```
const arr = [1,2,3,4,5];

for (let i; i<arr.length; i++) {
    console.log(arr[i]);
}

arr.forEach((item, idx) => console.log(item));

for(let item of arr) {
    console.log(item);
}

for (let [item, idx] of arr.entries()) {
    console.log(`idx: ${idx}, item: ${item}`);
}
```
