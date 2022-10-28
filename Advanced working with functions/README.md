# 과제

일초 간격으로 숫자 출력하기

from에 명시한 숫자부터 to에 명시한 숫자까지 출력해주는 함수 printNumbers(from, to)를 만들어보세요. 숫자는 일 초 간격으로 출력되어야 합니다.

두 가지 방법을 사용해 함수를 만드셔야 합니다.

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

   ```js
   // 내가 풀이한 방법 1
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

   ```js
   // 내가 풀이한 방법 2
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

   ```js
   // 솔루션 A
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

   ```js
   // 솔루션 B: 초기 지연시간 없이 함수를 바로 실행
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
