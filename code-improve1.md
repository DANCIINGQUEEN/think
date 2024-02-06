```js
const multiKill = (title) => {
    if (title.includes("쿼드라")) return "skyblue";
    else if (title.includes("펜타")) return "#FF0077FF";
    else return "rgba(0,0,0,0.02)";
};
```

개선 : else문 제거

```js
const multiKill = (title) => {
    if (title.includes("쿼드라")) return "skyblue";
    if (title.includes("펜타")) return "#FF0077FF";
    return "rgba(0,0,0,0.02)";
};
```
