```js
const multiKill = (title) => {
    if (title.includes("쿼드라")) return "skyblue";
    else if (title.includes("펜타")) return "#FF0077FF";
    else return "rgba(0,0,0,0.02)";
};
```

개선 : `else if`, `else` 제거

```js
const multiKill = (title) => {
    if (title.includes("쿼드라")) return "skyblue";
    if (title.includes("펜타")) return "#FF0077FF";
    return "rgba(0,0,0,0.02)";
};
```

=========================================================

```js
const date = playlist[1].date
const id = playlist[1]._id
```
개선 : 구조 분해 할당(destructuring)

```js
const { date, _id: id } = playlist[1]
```


=========================================================
