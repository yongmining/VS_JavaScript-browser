# 2-4. Event (이벤트 기본 동작)

## 2-4-1. prevent browser action (브라우저 기본 동작 중단)
- 이벤트 객체의 preventDefault 메서드는 DOM 요소의 기본 동작을 중단시킨다. 
  - 예를 들어 a 요소를 클릭하면 href 어트리뷰트에 지정 된 링크로 이동하고, checkbox 또는 radio 요소를 클릭하면 체크 또는 해제되는 것 등을 기본 동작이라고 한다. 

```html
<a href="https://www.google.com">클릭해도 절대 이동할 수 없는 a태그</a>
<input type="checkbox">클릭해도 절대 체크되지 않는 체크박스 
```

```js
document.querySelector('a').addEventListener('click', e => {
    e.preventDefault();
});
document.querySelector('input[type=checkbox]').addEventListener('click', e => {
    e.preventDefault();
});
```

## 2-4-2. stop event propagation (이벤트 전파 방지)
- 이벤트 객체의 stopPropagation 메서드는 이벤트 전파를 중지 시킨다.
```html
<ul id="drink">
    <li>커피</li>
    <li>콜라</li>
    <li>우유</li>
</ul>
```

```js
const $drink = document.getElementById('drink');

// 이벤트 위임 - 클릭 된 하위 li 요소의 color 변경
$drink.addEventListener('click', e => {
    if(e.target.matches('li'))
        e.target.style.color = 'red';
});

// 첫번째 li를 대상으로 color 변경 
document.querySelector('li').addEventListener('click', e => {
    e.stopPropagation();    // 이벤트 전파 중단으로 red로 변경되지 않음
    e.target.style.color = 'blue';
});
```