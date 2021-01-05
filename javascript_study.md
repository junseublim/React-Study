# 자바스크립트 문법 노트

## ES6 const & let
- 기존 var : scope가 함수 단위.
- let : scope가 블록 단위인 변수
- const: scope가 블록 단위인 상수

## ES6 Arrow Function
**기존 함수와 다른점**: 기존 함수는 자신이 종속된 객체를 this로 가르키며, arrow function은 자신이 종속된 인스턴스를 가르킨다.

- 기존 함수
```javascript
function BlackDog() {
    this.name = '흰둥이'
    return {
        name : '검둥이',
        bark : function() {
            console.log(this.name + ' : 멍멍!' );
        }
    }
}
// 검둥이 : 멍멍!
```
- 화살표 함수
```javascript
function WhiteDog() {
    this.name = '흰둥이'
    return {
        name : '검둥이',
        bark : () => {
            console.log(this.name + ' : 멍멍!' );
        }
    }
}
// 흰둥이 : 멍멍!
```