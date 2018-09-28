# Vue js

> Vue는 View의 발음에서 따온 것으로, 말 그대로 화면 작에서 최적화 된 자바스크립트 프레임워크이다.
>
> MVVM(Model - View - ViewModel) 패턴 기반으로 디자인되었고, 컴포넌트 기반으로 재사용 가능한 UI들을 조합하여 사용 할 수 있다. 

#### 특징

- MVVM Pattern

  > Model - View - ViewModel의 줄임말로 로직과 UI의 분리를 위해 설계된 패턴이다.
  >
  > HTML, CSS가 View 역할을 하고, Javascript가 Model 역할을 한다.
  >
  > ViewModel이 없는 경우 DOM API를 이용해(getElementById) View와 Model을 직접 연결시켜야 하는데, 이런 경우 Javascript에서 컨트롤러 역할까지 하며 코드의 양이 증가한다.
  >
  > ViewModel이 중간에서 그 컨트롤러 역할을 하는 것이 MVVM 패턴이다. Vue.js가 담당하며, 미리 정의된 옵션들을 통해서 데이터의 변화를 감지하거나 이벤트를 등록한다.

  ![MVVM](/Users/paul/Documents/web-development-study/Images/MVVM.jpeg)

- Virtual Dom

  > Virtual Dom 즉 가상 Dom이란 DOM(Document Object Model)의 복사본을 메모리 내에 저장해서 사용하여, Javascript로 DOM을 조작하며 생긴 변경 사항을 가상의 위치에서 처리함으로, 실제 DOM의 렌더링을 최소화 하는 방식이다.(Virtual Dom을 사용한 예는 대표적으로 Vue, React등의 프레임워크들이 있다.)

  ![VirtualDom](/Users/paul/Documents/web-development-study/Images/VirtualDom.png)

- Component

  > 화면에 보여지는 페이지를 구성하는 요소를 쪼개서 재활용이 가능한 형태로 관리하는 것, 하나의 컴포넌트는 미리 정의된 옵션을 갖고 있는 Vue 인스턴스이다.
  >
  > 컴포넌트들을 조합하여 페이지를 구성할 수 있고, 이를 활용해 각 코드들의 의존도를 낮추고 재활용성을 높일 수 있다 **("싱글 파일 컴포넌트 체계" 에서는 Template(HTML), Style(CSS), Script(JavaScript)로 구성되어있다.)**

  ---
