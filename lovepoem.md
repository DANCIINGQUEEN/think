```js
// 단어와 구절 라이브러리
const words = ["사랑", "마음", "영원", "열정"];
const phrases = ["별빛 아래에서", "너의 눈빛 속에서", "끝없는 꿈 속에서", "시간을 거슬러"];

// 랜덤 선택 함수
function randomChoice(list) {
    return list[Math.floor(Math.random() * list.length)];
}

// 시 형식 정의
const numLines = 4;
const numStanzas = 3;

// 시 생성
let poem = "";
for (let stanza = 0; stanza < numStanzas; stanza++) {
    for (let line = 0; line < numLines; line++) {
        // 단어 또는 구절 무작위 선택
        poem += Math.random() < 0.5 ? randomChoice(words) + " " : randomChoice(phrases) + " ";
    }
    poem += "\n";
}

console.log(poem);
```

```js
// 단어와 구절 라이브러리
const emotions = {
  happy: {
    words: ["행복", "즐거움", "웃음"],
    phrases: ["태양 아래 뛰노는", "꽃들 사이를 거니는", "맑은 하늘 아래서"]
  },
  sad: {
    words: ["슬픔", "고독", "그리움"],
    phrases: ["비 내리는 창가에서", "어두운 밤을 걷는", "잊혀진 시간 속에서"]
  }
  // 여기에 더 많은 감정 카테고리 추가 가능
};

// 랜덤 선택 함수
function randomChoice(list) {
    return list[Math.floor(Math.random() * list.length)];
}

// 시 생성 로직
function generatePoem(emotion) {
  const word = randomChoice(emotions[emotion].words);
  const phrase = randomChoice(emotions[emotion].phrases);
  return `사랑은 ${word}, ${phrase}.`;
}

// 사용자의 감정 선택에 반응하는 이벤트 리스너
document.getElementById('emotion').addEventListener('change', function() {
  const selectedEmotion = this.value;
  const poem = generatePoem(selectedEmotion);
  console.log(poem); // 또는 웹 페이지에 표시
});

```

```js
// 배열 정의
const emotions = ["행복한", "슬픈", "그리워하는", "열정적인"];
const places = ["해변에서", "산속에서", "도시의 거리에서", "고요한 밤에"];
const actions = ["춤추는", "노래하는", "생각에 잠긴", "하늘을 바라보는"];

// 랜덤 선택 함수
function randomChoice(list) {
    return list[Math.floor(Math.random() * list.length)];
}

// 시 생성 로직
function generatePoem(numLines) {
    let poem = "";
    for (let i = 0; i < numLines; i++) {
        const emotion = randomChoice(emotions);
        const place = randomChoice(places);
        const action = randomChoice(actions);
        poem += `사랑은 ${emotion}, ${place} ${action}.\n`;
    }
    return poem;
}

// 시 생성 및 콘솔에 출력
const poem = generatePoem(4); // 4줄짜리 시 생성
console.log(poem);

```
