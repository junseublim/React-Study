# React
"리액트를 다루는 기술" (저자: 김민준)을 기반으로 한 React 학습<br>

[자바스크립트 문법 학습 노트](javascript_study.md)
## Chapter 1

### 리액트란
리액트는 다른 프론트엔드 프레임워크와는 다르게 오직 뷰만 신경 쓰는 라이브러리이다. 리액트는 어떻게 하면 렌더링하면서 성능을 아끼고 사용자들에게 최적의 경험을 제공하기 위한 라이브러리이다. 

- 초기 렌더링 : 리액트에선 초기 화면을 렌더링 하기 위해 render 함수를 사용한다. 렌더링하여 HTML 마크업을 만들고 이를 실제 페이지의 DOM 요소안에 주입한다.
- 조화 과정 : 리액트에서 데이터의 변화가 있을 경우 새로운 요소로 갈아끼우는 행위를 조화라고 한다. 새로운 데이터를 가지고 render 함수를 호출하고, 결과를 이전 컴포넌트와 비교한다. 그 후 최소의 차이를 알아내 DOM 트리를 업데이트 하는 것이다.

### 리액트의 특징

1. Virtual DOM : 리액트는 Virtual DOM을 사용한다. 리액트에선 DOM을 업데이트 할때 먼저 Virtual Dom에 리렌더링하고 이전 Virtual DOM에 있던 내용과 현재 내용을 비교한 후 바뀐 내용만 실제 DOM에 적용한다. 
    - **지속적으로 데이터가 변화하는 대규모 애플리케이션 구축하기**
    - 간결성, 빠른 업데이트 속도

2. 리액트는 프레임워크가 아니라 라이브러리이다. 오직 View에 관련된 기능들만 제공한다.
    - 다른 기능들은 직접 구현 혹은 외부 라이브러리를 사용해야 한다.
    - 또한 다른 웹 프레임워크나 라이브러리와 혼용할 수 있다.

## Chapter 2

### Webpack
웹팩은 번들러의 일종으로, 파일들을 묶듯이 연결해준다. 번들러 도구를 사용하면 import(또는 require)로 모듈을 불러왔을 때 불러온 모듈을 모두 합쳐서 하나의 파일을 생성해준다. 또 최적화 과정에서 여러 개의 파일로 분리될 수도 있다. 

### JSX
jsx란 자바스크립트의 확장 문법으로 XML과 유사하게 생겼다. JSX 코드는 번들링되는 과정에서 바벨을 사용하여 일반 자바스크립트 형태의 문법으로 변환된다. 

#### JSX 장점
- 보기 쉽고 익숙하다.
- 활용도가 높다. JSX로 작성된 컴포넌트는 일반 html 태그처럼 사용할 수 있다.

#### JSX 문법
- 컴포넌트안에 여러 개의 요소가 있을 경우 하나의 부모요소로 감사야 한다.
    - div, Fragment 혹은 \<>로 감싸면 된다.
- 자바스크립트 표현을 사용하기 위해선 { }로 감싸면 된다.
- If 문 대신 삼항 연산자를 사용한다.
- AND(&&)를 이용해 조건부 렌더링이 가능하다. 
- undefinde를 반환하여 렌더링하는 상황을 만들면 안된다. 
    - undefinde일 수 있을 경우 OR(||) 연산자로 사용할 값을 지정해줘야 한다.
- 인라인 스타일링시 객체 형태로 스타일을 넣어주어야 한다.
    - 카멜표기법으로 이름을 표현한다. ex) backgroundColor
- 클래스 사용할 때는 class 가 아닌 className으로 설정.
- 주석은 {/* 주석 내용 */}으로 작성


## Chapter 3

### Component
컴포넌트는 크게 함수형, 클래스형 컴포넌트 두가지로 나뉜다. 둘의 차이는 클래스형 컴포넌트의 경우 
1. state 기능을 사용할 수 있으며
2. 라이프사이클 기능을 사용할 수 있고
3.  임의 메서드를 정의할 수 있다.

함수형 컴포넌트의 경우
1. 선언하기 훨씬 편하고
2. 메모리 자원도 클래스형 컴포넌트보다 작다.
3. Hooks를 통해 state와 라이프사이클 API를 사용할 수 있다.

리액트 공식 매뉴얼에서는 컴포넌트를 새로 작성할 때 함수형 컴포넌트를 권장한다.

### Props
컴포넌트의 속성을 설정할 때 사용하는 요소이며, 부모 컴포넌트에서 설정 가능하다.

1. props 사용법
```javascript
// 부모 Component
const App = () => {
    return <MyComponent name="React"/>;
}
```
```javascript
// 자식 Component
const MyComponent = props => {
    return <div>The name is {props.name}</div>;
}
```
2. props 기본값 설정: defaultProps
```javascript
// 부모 Component
const App = () => {
    return <MyComponent/>;
}
```
```javascript
// 자식 Component
const MyComponent = props => {
    return <div>The name is {props.name}</div>;
}
MyComponent.defaultProps = {
    name: '기본 이름'
};
```

3. 태그 사이의 내용을 보여주는 Children
```javascript
// 부모 Component
const App = () => {
    return <MyComponent>리액트</MyComponent>;
}
```
```javascript
// 자식 Component
const MyComponent = props => {
    return <div>The Children is {props.children}</div>;
}
```

4. propTypes를 통한 props 검증

컴포넌트의 타입을 지정할 때 사용. 타입이 다를 경우 Warning.
```javascript
// 부모 Component
const App = () => {
    return <MyComponent name="React"/>;
}
```
```javascript
// 자식 Component
const MyComponent = props => {
    return <div>The prop is {props.name}</div>;
}
MyComponent.propTypes = {
    name : PropTypes.string
}
```
5. isRequired

필수적인 prop 지정. 없을 경우 Warning.
```javascript
// 부모 Component
const App = () => {
    return <MyComponent name="React"/>;
}
```
```javascript
// 자식 Component
const MyComponent = props => {
    return <div>The prop is {props.name}</div>;
}
MyComponent.propTypes = {
    name : PropTypes.string.isRequired
}
```

#### 클래스형 컴포넌트에서 props 사용하기

render() 함수에서 this.props를 조회하면 된다. defaultProps, propTypes는 똑같은 방식으로 하거나, class 내부에서 지정하는 방식으로도 가능하다.

```javascript 
class MyComponent extends Component {
    static defaultProps = {
        name: '기본 이름'
    }
    static propTypes = {
        name: PropTypes.string,
        favoriteNumber: PropTypes.number.isRequired
    }
    render() {
        const {name, favoriteNumber, children} = this.props; //비구조화 할당
        return (<div>The prop is {name}</div>;)
    }
}
```

### State

state란 컴포넌트 내부에서 바뀔 수 있는 값을 의미. props는 컴포넌트가 사용되는 과정에서 부모 컴포넌트가 설정하는 값이며, 컴포넌트 자신은 해당 props을 읽기 전용으로만 사용할 수 있다. 반면 state는 직접 변경할 수 있다.

#### 클래스형 컴포넌트의 state

1. constructor에서 작성
```javascript
class MyComponent extends Component {
    constructor(props) {
        super(props);
        this.state = {
            number : 0
        };
    } 
    render () {
        const {number} = this.state;
    }
}
```
2. constructor 밖에서 작성
```javascript
class MyComponent extends Component {
    state = {
        number : 0
    }
    render () {
        const {number} = this.state;
    }
}
```

#### setState
setState 는 비동기적으로 업데이트 된다. 따라서 두번 연속으로 호출하려면 setState에 객체 대신에 함수를 인자로 넣어줘야 한다.
```javascript
this.setState((prevState, props) => {
    return {
        //업데이트 하고 싶은 내용
    }
})

```

#### setState 콜백 함수
setState 끝난 후에 특정 작업을 하려면 콜백 함수를 등록하면 된다.
```javascript
this.setState({
    number: number + 1
}, () => {
    console.log('callBack');
})
```

#### 함수형 컴포넌트에서 state
Hooks의 useState를 사용하여 state를 사용할 수 있다.
```javascript
const MyComponent () => {
    const [message, setMessage] = useState('');
    
    return (...);
}
```
useState 함수의 인자에는 초깃값을 넣어준다. 반드시 객체가 아니어도 된다. 반환 값의 두번째 원소는 setter 함수이다.