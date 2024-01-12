```javascript
const fs = require('fs');

// 파일 읽기를 중첩된 콜백으로 처리하는 예시
fs.readFile('file1.txt', 'utf8', (err, data1) => {
    if (err) {
        console.error(err);
        return;
    }
    console.log(data1);

    fs.readFile('file2.txt', 'utf8', (err, data2) => {
        if (err) {
            console.error(err);
            return;
        }
        console.log(data2);

        fs.readFile('file3.txt', 'utf8', (err, data3) => {
            if (err) {
                console.error(err);
                return;
            }
            console.log(data3);
            // 더 많은 중첩된 콜백...
        });
    });
});

```

```javascript
  const fs = require('fs').promises;

// Promise를 사용하여 파일을 순차적으로 읽는 예시
const readFile = (fileName) => {
    return fs.readFile(fileName, 'utf8');
};

readFile('file1.txt')
    .then(data1 => {
        console.log(data1);
        return readFile('file2.txt');
    })
    .then(data2 => {
        console.log(data2);
        return readFile('file3.txt');
    })
    .then(data3 => {
        console.log(data3);
    })
    .catch(err => {
        console.error(err);
    });

```

```javascript
  const fs = require('fs').promises;

// async 함수를 사용하여 파일을 순차적으로 읽는 예시
const readFileAsync = async () => {
    try {
        const data1 = await fs.readFile('file1.txt', 'utf8');
        console.log(data1);

        const data2 = await fs.readFile('file2.txt', 'utf8');
        console.log(data2);

        const data3 = await fs.readFile('file3.txt', 'utf8');
        console.log(data3);
    } catch (err) {
        console.error(err);
    }
};

readFileAsync();
```
