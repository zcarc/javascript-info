### 상속 클래스, 부모 클래스에서 this

```js
class Animal {
  constructor(name) {
    this.name = "test";
    this.speed = 0;
    console.log("animal constructor... this: ", this);
    console.log("animal constructor... name: ", name);
  }

  getAimalName() {
    console.log("animal this.name: ", this.name);
  }
}

class Rabbit extends Animal {
  constructor(name, earLength) {
    super(name);
    this.name = name;
    this.earLength = earLength;
    console.log("rabbit constructor... this: ", this);
  }
  showName() {
    console.log("rabbit");
  }
}

const rabbit = new Rabbit("흰 토끼", 10);
```

### 기본적으로 상속 클래스에 생성자가 정의되지 않았다면 다음과 같이 생성자가 암시적으로 생성되어 부모 생성자를 호출합니다.

```js
constructor(…args) {
    super(…args)
}
```

만약 상속 클래스의 생성자가 정의되고 ‘super’ 함수를 호출하지 않는다면, Rabbit에서 ‘this’를 사용하려고 하면 에러가 발생합니다. <br />
그 이유는 상속 클래스의 생성자에서 빈 객체를 만들고 ‘this’에 이 객체를 할당하는 일을 부모 클래스의 생성자가 처리해주기를 기대합니다. <br />
그래서 자식 클래스에서 ‘this’를 사용한다면 부모 생성자 함수(constructor)를 실행해야하므로 ‘super’ 함수를 호출해서 부모 생성자를 실행해줘야합니다. <br />
그렇지 않으면 ‘this’가 될 객체가 만들어지지 않아 에러가 발생합니다. <br />
부모의 ‘this’ 객체는 상속 클래스 생성자 함수에서 만들어진 빈 객체를 가리키고 <br />
부모 클래스의 생성자에서 this로 접근하여 할당한 속성들은 상속 클래스의 this와 같은 객체를 가리키게 됩니다. <br />
‘super’ 의 호출로 부모 생성자의 로직이 종료되고 나서 ‘super’ 호출부 이후의 로직이 진행됩니다. <br />
만약 부모 생성자와 자식 생성자에서 ‘this’ 객체에 동일한 프로퍼티에 값을 할당한다면 자식 생성자 로직이 나중에 진행되므로 해당 프로퍼티의 값은 자식 생성자에서 할당한 값이 됩니다. <br />
