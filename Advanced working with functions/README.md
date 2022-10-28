# 과제

## 일초 간격으로 숫자 출력하기

from에 명시한 숫자부터 to에 명시한 숫자까지 출력해주는 함수 printNumbers(from, to)를 만들어보세요. 숫자는 일 초 간격으로 출력되어야 합니다.

두 가지 방법을 사용해 함수를 만드셔야 합니다.

1. setInterval을 이용한 방법
2. 중첩 setTimeout을 이용한 방법

<details>
<summary>해답</summary>

1. setInterval을 이용한 방법

   ```js
   function printNumbers(from, to) {
     let current = from;

     const timer = setInterval(function () {
       alert(current);
       if (current === to) {
         clearInterval(timer);
       }
       current++;
     }, 1000);
   }

   printNumbers(5, 10);
   ```

2. 중첩 setTimeout을 이용한 방법

   - #### 내 풀이 1

   ```js
   function printNumbers(from, to) {
     let current = from;

     setTimeout(function go() {
       const timer = setTimeout(go, 1000);
       alert(current);
       if (current === to) {
         clearTimeout(timer);
       }
       current++;
     }, 1000);
   }

   printNumbers(5, 10);
   ```

   - #### 내 풀이 2

   ```js
   function printNumbers(from, to) {
     let current = from;

     setTimeout(function go() {
       alert(current);
       if (current === to) {
         clearTimeout(timer);
       }
       current++;

       const timer = setTimeout(go, 1000);
     }, 1000);
   }

   printNumbers(5, 10);
   ```

   - #### 솔루션 A

   ```js
   function printNumbers(from, to) {
     let current = from;

     setTimeout(function go() {
       alert(current);
       if (current < to) {
         setTimeout(go, 1000);
       }
       current++;
     }, 1000);
   }

   printNumbers(5, 10);
   ```

   - #### 솔루션 B: 초기 지연시간 없이 함수를 바로 실행

   ```js
   function printNumbers(from, to) {
     let current = from;

     function go() {
       alert(current);
       if (current === to) {
         clearInterval(timerId);
       }
       current++;
     }

     go();
     const timerId = setInterval(go, 1000);
   }

   printNumbers(5, 10);
   ```

   </details>

## setTimeout 은 무엇을 보여줄까요?

아래 코드에선 setTimeout을 이용해 호출을 스케줄링하고 있습니다. 그런데 그 아래 코드에선 실행 시간이 100ms 이상 걸리는 무거운 작업을 하고 있네요.

이런 경우 setTimeout에 넘겨준 함수는 언제 실행될까요?

1. 반복문 실행 후
2. 반복문 실행 전
3. 반복문이 실행되는 시점

얼럿창엔 어떤 값이 출력될까요?

```js
let i = 0;

setTimeout(() => alert(i), 100); // ?

// 아래 반복문을 다 도는 데 100ms 이상의 시간이 걸린다고 가정합시다.
for (let j = 0; j < 100000000; j++) {
  i++;
}
```

<details>
<summary>해답</summary>

<!-- summary 아래 한칸 공백 두어야함 -->

setTimeout은 현재 실행 중인 코드의 실행이 종료되었을 때 실행됩니다.

반복문 실행이 종료되고 난 후 i는 100000000이 되므로, 얼럿창엔 100000000이 출력됩니다.

```js
let i = 0;

setTimeout(() => alert(i), 100); // 100000000이 출력됩니다.

// assume that the time to execute this function is >100ms
for (let j = 0; j < 100000000; j++) {
  i++;
}
```

</details>
