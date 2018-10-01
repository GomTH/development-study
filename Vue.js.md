# Vue js

> Vue는 View의 발음에서 따온 것으로, 말 그대로 화면 작에서 최적화 된 자바스크립트 프레임워크이다.
>
> MVVM(Model - View - ViewModel) 패턴 기반으로 디자인되었고, 컴포넌트 기반으로 재사용 가능한 UI들을 조합하여 사용 할 수 있다. 

### 특징

- MVVM Pattern

  > Model - View - ViewModel의 줄임말로 로직과 UI의 분리를 위해 설계된 패턴이다.
  >
  > HTML, CSS가 View 역할을 하고, Javascript가 Model 역할을 한다.
  >
  > ViewModel이 없는 경우 DOM API를 이용해(getElementById) View와 Model을 직접 연결시켜야 하는데, 이런 경우 Javascript에서 컨트롤러 역할까지 하며 코드의 양이 증가한다.
  >
  > ViewModel이 중간에서 그 컨트롤러 역할을 하는 것이 MVVM 패턴이다. Vue.js가 담당하며, 미리 정의된 옵션들을 통해서 데이터의 변화를 감지하거나 이벤트를 등록한다.

  ![MVVM](./Images/MVVM.jpeg)

- Virtual Dom

  > Virtual Dom 즉 가상 Dom이란 DOM(Document Object Model)의 복사본을 메모리 내에 저장해서 사용하여, Javascript로 DOM을 조작하며 생긴 변경 사항을 가상의 위치에서 처리함으로, 실제 DOM의 렌더링을 최소화 하는 방식이다.(Virtual Dom을 사용한 예는 대표적으로 Vue, React등의 프레임워크들이 있다.)

  ![VirtualDom](./Images/VirtualDom.png)

- Component

  > 화면에 보여지는 페이지를 구성하는 요소를 쪼개서 재활용이 가능한 형태로 관리하는 것, 하나의 컴포넌트는 미리 정의된 옵션을 갖고 있는 Vue 인스턴스이다.
  >
  > 컴포넌트들을 조합하여 페이지를 구성할 수 있고, 이를 활용해 각 코드들의 의존도를 낮추고 재활용성을 높일 수 있다.
  >
  >  **("싱글 파일 컴포넌트 체계" 에서는 Template(HTML), Style(CSS), Script(JavaScript)로 구성되어있다.)**

---

### Vue Instance

> 뷰 인스턴스는 뷰로 화면을 개발하기 위해 필수적으로 생성해야 하는 기본 단위이다.
>
> 뷰 인스턴스를 생성할때는 데이터, 템플릿, 마운트할 엘리먼트, 메소드, 라이프사이클 콜백 등의 옵션을 포함 할 수있는 **options 객체**를 전달 해야한다.

```javascript
var vm = new Vue({
    // 옵션
})
```

##### Options

- data

  > 컴포넌트의 속성을 정의하는 객체.
  >
  > 뷰 인스턴스 내부에서 직접 이용되지 않고, 뷰 인스턴스와 data 옵션 사이에 **프록시**를 두어 처리한다.
  >
  > data 옵션은 뷰 인스턴스가 관찰하는 객체이므로 변경사항은 즉시 감지되어(반응형) 데이터가 변경되면 화면도 다시 렌더링된다.

  > 프록시란 ? 
  >
  > 대리인 이라는 뜻을 가지고 있다. 사용자가 직접 요청을 하기보다는 한 단계 앞에 프록시를 두어 간접적으로 접근하게 한다. 이를 흐름제어라 한다. 프록시를 사용하면, 잘못된 요청을 방지할 수 있다. 
  >
  > **중요한 것은, 흐름제어만 할 뿐 결과 값을 조작해서는 안 된다.**

  ```js
  var vm = new Vue({
          data: {
              name: 'choi',
              age: 25
          },
          created: function() { // 페이지 호출 및 data 등의 옵션 호출 완료 후
              console.log(this.name); // choi
          }
  })
  ```

- el

  > 뷰 인스턴스에 연결할 HTML DOM 요소를 지정한다.
  >
  > 한 개의 요소만 지정할 수 있다. 동적으로 지정할 수 있으나, 한 번 HTML 요소가 연결되면 도중에 연결된 요소를 변경할 수 없다. 따라서 도중 바뀔 일이 없으므로 최초 인스턴스 생성 시 el은 직접 지정하는 것이 좋다.

  ```html
  <div id="example">
      <h2>hi</h2>
  </div>
  <script type="text/javascript">
      var vm = new Vue({
          el: "#example"
      })
  </script>
  ```

- methods

  > 뷰 인스턴스에서 사용할 메서드들을 정의하는 객체.
  >
  > 정의(등록)된 메서드는 뷰 인스턴스 내에서 직접 호출할 수 있고, HTML에서는 뷰가 제공하는 디렉티브 표현식(v-model, v-click 등) 및 콧수염 표현식({{}})으로 호출할 수 있다.

  ```html
  <div id="example">
      <h1>{{ getAge() }}</h1> // 콧수염 표현식
      <h2 v-model="getAge()"></h2> // 디렉티브 표현식
  </div>
  <script type="text/javascript">
      var vm = new Vue({
          el: "#example",
          data: {
              name: 'choi',
              age: 25
          },
          methods: {
              getAge() {
                  console.log(this.age);
              },
              getGetAge() {
                  this.getAge(); // 인스턴스 내 호출
              }
          }
      })
  </script>
  ```

- watch

  > 계산형 속성과 같이 하나의 데이터를 기반으로 다른 데이터를 변경할 필요가 있을 때 사용한다. (주로 긴 처리 시간이 필요한 비동기 처리에 적합하다.)
  >
  > 속성 이름과 해당 속성 값이 변경되었을 때 호출할 함수를 등록한다 즉, 값이 바뀔 때마다 매번 함수가 호출된다.

  ```html
  <div id="app">
      x: <input type="text" v-model="x"><br>
      y: <input type="text" v-model="y"><br>
      덧셈 결과: {{ sum }}
  </div>
  <script type="text/javascript">
      var vm = new Vue({
          el: '#app',
          data: {
              x: 0,
              y: 0,
              sum: 0
          },
          watch: {
              x: function (n) {
                  console.log('x 변경');
                  var result = Number(n) + Number(this.y);
                  this.sum = result;
              },
              y: function (n) {
                  console.log('y 변경');
                  var result = Number(n) + Number(this.x);
                  this.sum = result;
              }
          }
      })
  </script>
  ```

---

### Lifecycle

Vue,js의 라이프 사이클은 크게 Creation, Mounting, Updating, Destruction으로 나눌 수 있다.

![Lifecycle](./Images/Lifecycle.png)

##### Creation: 컴포넌트 초기화 단계

> 라이프사이클 중에 가장 처음 실행되는 단계이다. 이 단계는 컴포넌트가 DOM에 추가되기 전이다.(서버 렌더링에서도 지원되는 훅) ***! 아직 컴포넌트가 DOM에 추가되기 전이기 때문에 DOM에 접근하거나 this.$el를 사용할 수 없다.***

- beforeCreate

  모든 훅 중에 가장 먼저 실행되는 훅이다. 아직 data와 events(on, once, off, emit 등)가 세팅되지 않은 시점이다.

  ```javascript
  <script>
    export default {
      data () {
        return {
          title: ''
        }
      },
  
      beforeCreate () {
        //can't use Data(this.title ...), events(vm.$on, vm.$once, vm.$off, vm.$emit)
      }
    }
  </script>
  ```

- created

  created 훅에서는 data와 events가 활성화 되어 접근이 가능하다. 하지만 template, Virtual DOM은 마운트 및 렌더링되지 않은 상태이다.

  ```html
  <script>
    export default {
      data () {
        return {
          title: ''
        }
      },
      computed: {
        titleComputed() {
          console.log('I change when this.property changes.')
          return this.property
        }
      },
      created () {
        //can use Data(this.title, this.titleComputed ...), events(vm.$on, vm.$once, vm.$off, vm.$emit)
        //don't use $el
      }
    }
  </script>
  ```

##### Mounting: DOM 삽입 단계

> Mounting 단계는 초기 렌더링 직전에 컴포넌트에 직접 접근이 가능하다. (서버 렌더링 에서는 지원하지 않는다.)

- beforeMount

  beforeMount 훅은 템플릿과 render함수들이 컴파일 된 후 첫 렌더링이 일어나기 직전에 실행된다. (대부분의 경우 사용하지 않는 것이 좋다. ~~사용하지도 않는다.~~)

- mounted

  mounted 훅에서는 컴포넌트, 템플릿, 렌더링된 돔에 접근할 수 있다.( **!** 모든 하위 컴포넌트가 마운트된 상태를 보장하지는 않는다.)

  ```html
  <script>
  export default {
    mounted() {
      console.log(this.$el.textContent) // can use $el
      this.$nextTick(function () {
        // 모든 화면이 렌더링된 후 실행됩니다.
      })
    }
  }
  </script>
  ```

  **!!!** mounted훅에서 유의할 점은, 부모와 자식 관계의 컴포넌트에서 mounted발생 순서가 **자식 -> 부모** 순서로 진행된다는 것이다.(당연히 부모 -> 자식 이라고 생각했을것이다.)

  ![Hookworkflow](./Images/Hookworkflow.png)

  위 그림처럼 Created훅은 **부모 -> 자식** 순서로 진행되지만 mounted는 그렇지 않은 것을 확인할 수 있다.(mounted 훅에서 부모는 자식의 훅이 끝나기를 기다린 후 진행됨을 알 수 있다.)

##### Updating: Diff 및 재 렌더링 단계

> 컴포넌트의 속성들이 변경되는 등의 이유로 재 렌더링이 발생되면 실행된다.(디버깅이나 프로파일링 등을 위해 컴포넌트 재 렌더링 시점을 알고 싶을때 사용할 수 있다.)

- beforeUpdate

  컴포넌트의 데이터가 변하여 업데이트 사이클이 시작될때 실행된다.(정확히는 DOM이 재 렌더링 되고 패치되기 직전에 실행된다.) 재 렌더링 전의 새 상태의 데이터를 얻을 수 있고 더 많은 변경이 가능하다.(이 변경으로 인한 재 렌더링은 트리거되지 않는다.)

- updated

  컴포넌트의 데이터가 변하여 재 렌더링이 일어난 후에 실행된다. DOM의 업데이트가 완료된 상태이므로 종속적인 연산이 가능하다.(그러나 여기서 상태를 변경하면 무한루프에 빠질 수 있다.)

  ```html
  <script>
  export default {
    updated() {
      this.$nextTick(function () {
        // 모든 화면이 렌더링된 후 실행됩니다.
      })
    }
  }
  </script>
  view raw
  ```

##### Destruction: 해체 단계

- beforeDestroy

   이 훅은 해체(뷰 인스턴스 제거)된 후에 호출된다. 뷰 인스턴스의 모든 디렉티브가 바인딩 해제되고, 모든 이벤트 리스너가 제거되며, 모든 하위 뷰 인스턴스도 삭제된다.(서버 렌더링시 호출되지 않는다.)

---

