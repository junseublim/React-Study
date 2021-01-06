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

## Chapter 4

### 리액트의 이벤트 시스템

#### 주의사항
1. 이벤트 이름은 카멜 표기법으로 (ex. onClick)
2. 이벤트에 실행할 자바스크립트 코드가 아니라 함수 형태의 값을 전달해야 한다.
3. DOM 요소에반 이벤트 설정할 수 있다.
    - 직접 만든 컴포넌트에는 이벤트를 자체적으로 설정할 수 없다.

#### 임의 메서드 만들기
이벤트에 실행할 함수 형태의 값을 전달할때 미리 메서드로 작성해서 넘겨 줄 수있다.
클래스형 컴포넌트에서 클래스 내에서 함수를 정의하고 생성자에서 바인딩 해줘야 한다.
```javascript
class MyComponent extends Component {
    constructor(props) {
        this.handler = this.handler.bind(this);
    }
    handler(e) {
        alert(e.target.value);
    }
}
```
혹은 바벨의 transform-class-properties 문법을 사용하여 화살표 함수 형태로 메서드를 정의해도 된다.
```javascript
class MyComponent extends Component {
    handler = (e) => {
        alert(e.target.value);
    }
}
```
## Chapter 5
일반 HTML에서 DOM 요소에 이름을 달때는 id를 사용한다. 이처럼 리액트에서는 ref를 사용하여 DOM 요소에 이름을 단다. 리액트 컴포넌트에서도 id를 사용할 수 있지만 권장하지 않는다. 컴포넌트를 여러번 재사용하면 동일한 id를 가진 DOM이 여러개 생길 수 있다. ref는 전역적으로 작동하지 않고 컴포넌트 내부에서만 작동하기 때문에 이런 문제가 생기지 않는다. 

### ref의 사용
ref는 DOM을 꼭 직접적으로 건드려야 할 떄 사용한다.
- 특정 input에 포커스 주기
- 스크롤 박스 조작하기
- Canvas 요서에 그림그리기

### ref의 사용 방법
두가지 방법이 있다. 

1. 콜백 함수를 통한 ref 설정
ref를 달고자 하는 요소에 ref라는 콜백 함수를 props로 전달.
```javascript
<input ref={(ref) => {this.input=ref}}>
```
이렇게 하면 앞으로 this.input은 input 요소의 DOM을 가르킨다.

2. createRef를 통한 ref 설정
```javascript
class RefSample extends Component {
    input = React.createRef();
    handleFocus = () => {
        this.input.current.focus();
    }
    render () {
        return (
            <div>
                <input ref={this.input}/>
            </div>
        );
    }
}
```
콜백 함수에 다르게 사용할 떄는 .current를 넣어줘야 한다.

### 컴포너트에 ref 달기

내부에 있는 DOM을 컴포넌트 외부에서 사용할 떄 쓴다.
```javascript
<MyComponent
    ref={(ref) => {this.myComponent = ref}}
>
```
이렇게 하면 MyComponent 내부의 메서드 및 멤버 변수에도 접근할 수 있다. 즉 내부의 ref에도 점근 할 수 있다.


## Chapter 6
반복적인 내용을 효율적으로 보여주고 관리

### 자바스크립트 배열의 map() 함수

#### 문법
```javascript
arr.map(callback, [thisArg])
```
- callback : 새로운 배열의 요소를 생성하는 함수로 파라미터는 3가지이다
    - currentValue: 현재 처리하고 있는 요소
    - index : 현재 처리하고 있는 요소의 index
    - array : 현재 처리하고 있는 원본 배열
- thisArg: callback 함수 내부에서 사용할 this 레퍼런스

### key
리액트에서 key는 컴포넌트 배열을 렌더링 했을 떄 어떤 원소에 변동이 있었는지 알아내기 위해 사용한다. key 값은 유일해야 한다.

#### index를 key값으로?
warning은 없앨 수 있으나 배열 변경시 효율적으로 리렌더링 하지 못한다.

## Chapter 7

### 라이프사이클
라이프사이클은 크게 마운트, 업데이트, 언마운트 카테고리로 나뉜다.

1. **마운트** : DOM이 생성되고 웹 브라우저상에 나타나는 것을 마운트라고 한다. 이떄 호출 하는 메서드들은 다음과 같다.
    1. constructor : 컴포넌트를 새로 만들때 호출되는 생성자
    2. getDerivedStateFromProps : props에 있는 값을 state에 넣는 메서드
    3. render : UI 렌더링 메서드
    4. componentDidMount: 컴포넌트가 웹 브라우저상에 나타난 후 호출되는 메서드
2. **업데이트** : 컴포넌트는 다음 네가지 경우에 업데이트 한다.
    - props가 변경 될 때
    - state가 변경 될 떄
    - 부모 컴포넌트가 리렌더링될 때
    - this.forceUpdate로 강제로 렌더링을 트리거할 때
    
    업데이트할 때 호출하는 메서드는 다음과 같다. 
    1. getDerivedStateFromProps : props에 변화에 따라 state 값에도 변화를 주고 싶을떄 사용
    2. shouldComponentUpdate: 컴포넌트가 리렌더링 할지 말지 결정하는 메서드. true 반환시 렌더
    3. render : 리렌더링 하는 메서드
    4. getSnapShotBeforeUpdate : 컴포넌트 변화를 DOM에 반영하기 직전에 호출하는 메서드. 
    5. componentDidUpdate : 컴포넌트의 업데이트 작업이 끝난 후 호출하는 메서드.
3. **언마운트** : 마운트의 반대과정, 컴포넌트를 DOM에서 제거하는 작업
    1. componentWillUnmoint : 컴포넌트가 웹 브라우저상에서 사라지기 전에 호출.


### 라이프사이클 메서드 살펴보기

1. render()

컴포넌트의 모양새를 정의한다. this.props, this.state에 접근할 수 있으며, 리액트 요소를 반환한다. 
**이 메서드 안에서는 이벤트 설정이 아닌 곳에서 setState를 사용하거나 DOM에 접근하면 안된다.** 이는 componentDidMount에서 처리해야 한다.

2. getDerivedStateFromProps()
props로 받아 온 값을 state에 동기화시키는 용도로 사용된다. 
```javascript
static getDerivedStateFromProps(nextProps, prevState) {
    if (nextProps.value != prevState.value) {
        return { value : nextProps.value};
    }
    return null;
}
```

3. componentDidMount()

다른 자바스크립트 라이브러리, 프레임워크의 함수를 호출하거나, 이벤트 등록, setTimeout 등 비동기 작업 처리를 하면 된다.

4. shouldComponentUpdate()

props 또는 state를 변경했을 때, 리렌더링을 할지 여부를 지정하는 메서드. 따로 생성하지 않으면 true를 반환.
this.props, this.state로 현재 props와 state 접근 가능하고, 새로 설정될 props, state 는 nextProps 또는 nextState로 접근 가능하다.

5. getSnapshotBeforeUpdate()

render에서 만들어진 결과물이 브라우저에 실제로 반영되기 직전에 호출된다. 이 메서드에서 반환하는 값은 componentDidUpdate에서 세 번째 파라미터인 snapshot 값으로 전달 받을 수 있는데 이는 주로 업데이트하기 직전의 값을 참고할 일이 있을 때 활용된다. (예. 스크롤바 위치 유지)

6. componentDidUpdate()

DOM관련 처리 하기 위해서 사용한다. prevState, prevProps를 통해 컴포넌트가 이전에 가졌던 데이터에 접근할 수 있다. 또 snapshot 값을 전달 받을 수 있다. 

7. componentWillUnmount()

 컴포넌트를 DOM에서 제거할 때 실행.

 8. componentDidCatch()

 컴포넌트 렌더링 중 에러가 발생했을 떄 오류 UI를 보여준다. 


## Chapter 8

### useState

함수형 컴포넌트에서 가변적이 ㄴ상태를 지닐 수 있게 해준다. 
```javascript
const [value, setValue] = useState(0);
```

### useEffect
리액트 컴포넌트가 렌더링될 때마다 특정 작업을 수행하도록 설정할 수 잇는 hookd이다. componentDidMount, componentDidUpdate를 합친 형태로 보아도 무방하다.

1. 마운트 시에만 실행하고 싶을 때 : 빈 배열을 넣어주면 된다.
```javascript
useEffect(() => {
    console.log('마운트 시에만');
}, [])
```

2. 특정 값이 업데이트될 때만 실행하고 싶을 때 : 배열안에 값을 넣어주면 된다. 
```javascript
useEffect(() => {
    console.log('name');
}, [name])
```

3. 뒷정리 할 댸 : 컴포넌트가 언마운트, 업데이트 되기 직전에 어떤 작업을 수행하고 싶다면 뒷정리 함수를 반환하면 된다.

```javascript
useEffect(() => {
    return () => {
        console.log('cleanup');
    }
})
```
```javascript
//오직 언마운트시에만 호출 하고싶다면 빈배열을 두번째 파라미터로
useEffect(() => {
    return () => {
        console.log('cleanup');
    }
}, [])
```

### UseReducer

useReducer는 useState 보다 더 다양한 컴포넌트 상화에 따라 다양한 상태를 다른 값으로 업데이트 해주고 싶을 떄 사용하는 hook.

Reducer는 현재 상태, 그리고 업데이트를 위해 필요한 정보를 담은 액션 값을 전달받아 새로운 상태를 반환하는 함수이다. Reducer에서 새로운 상태를 만들 때는 반드시 불변성을 지켜 줘야 한다.

```javascript

function reducer(state, action) {
    switch(action.type) {
        case 'INCREMENT' : 
            return {value: state.value + 1};
        case 'DECREMENT' :
            return {value: state.value - 1};
        default : 
            return state;
    }
}

const Counter = () => {
    const [state, dispatch] = useReducer(reducer, {value: 0});
    return (
        <div>
            <p>Current number is {state.value}</p>
            <button onClick={() => {dispatch({type: 'INCREMENT'})}}>+1</button>
            <button onClick={() => {dispatch({type: 'DECREMENT'})}}>-1</button>
        </div>
    )
}
```
useReducer 첫번째 파라미터는 reducer 함수이며, 두 번째 파라미터는 해당 리듀서의 기본 값.

reducer의 장점은 컴포넌트 업데이트 로직을 컴포넌트 바깥으로 빼낼 수 있다는 것이다.

### useMemo

useMemo 사용시 함수형 컴포넌트 내부에서 발생하는 연산을 최적화할 수 있다.
렌더링 과정에서 특정 값이 바뀌었을 겨웅에만 연산을 실행하고 원하는 값이 바뀌지 않았다면 이전에 연산했던 결과를 다시 사용하는 방식이다.

```javascript
const avg = useMemo(() => getAverage(list), [list]);
```
이는 list 배열의 내용이 바뀔 때만 getAverage 함수가 호출 된다.

### useCallback

useMemo에 유사하게 주로 런데링 성능을 최적화해야 하는 상황에서 사용한다. 컴포넌트에서는 사용할 함수들을 생성해야 하는데 먼역 컴포넌트의 렌더링이 자주 발생하거나 렌더링해야 할 컴포넌트의 개수가 많아지면 이부분을 최적화해 주는 것이 좋다. 
```js
const onChange = useCallback(e => {
    setNumber(e.target.value);
}, []); //컴포넌트가 처음 렌더링될 때만 함수 생성
const onInsert = useCallback((val) => {
    const nextList = [...list, number];
    setList(nextList);
}, [number, list]); //number, list가 바뀌었을 때만 함수 생성
```
함수 내부에서 상태 값에 의존해야 할 때는 반드시 그 값을 두 번째 파라미터 안에 포함시켜 줘야 한다.

### useRef

useRef는 함수형 컴포넌트에서 ref를 쉽게 사용할 수 있도록 해준다. 또한 컴포넌트 로컬 변수를 사용해야 할 때도 활용할 수 있다. 
```javascript
const Focus = () => {
    const inputEl = useRef(null);
    const onClick = () => {
        inputEl.current.focus();
    }

    return ( 
        <div>
            <input ref={inputEl} />
            <button onClick={onClick}>Click</button>
        </div>
    )
}
```
```javascript
const Ref = () => {
    const id = useRef(1);
    const setId = (n) => {
        id.current = n;
    }
    const printId = () => {
        console.log(id.current);
    }
    return ( 
        <div>
            refSample
        </div>
    )
}
```
ref안의 값이 바뀌어도 컴포넌트가 렌더링 되지 않는다.
