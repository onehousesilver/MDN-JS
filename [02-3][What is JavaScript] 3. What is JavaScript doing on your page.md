# What is JavaScript?

> 출처: https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/What_is_JavaScript



### What is JavaScript doing on your page?

> 웹 페이지에서 JavaScript는 어떤 일을 하나요?

여기서 몇가지 코드를 실제로 살펴보고, 페이지에서 자바스크립트가 언제 어떻게 작동하는지 알아 볼 것입니다.

브라우저에서 웹페이지를 불러올 때 어떤 일이 발생하는지 생각해봅시다. 브라우저에서 웹페이지를 불러올 때, 실행 환경(브라우저 탭)안에서 HTML, CSS, Javascript 코드가 실행됩니다. 이는 마치 공장에서 원재료(코드)가 일련의 과정을 거쳐 제품(웹페이지)으로 탄생되는 것과 같습니다.![img](https://media.vlpt.us/images/onehousesilver/post/42b94373-cd85-4986-bce5-17c1ae6b8767/image.png)

자바스크립트는 HTML과 CSS가 결합되고 웹페이지 상에서 올려진 후, 브라우저의 자바스크립트 엔진에 의해 실행됩니다. 이는 페이지의 구조와 스타일등을 정해놓고, 자바스크립트가 실행된다는 것과 같은 의미입니다.
동적으로 사용자 인터페이스를 업데이트하는 자바스크립트의 사용은 Document Object Model API를 통해 HTML과 CSS를 수정하는 것으로 좋은 현상입니다. **만약 자바 스크립트가 HTML과 CSS 전에 실행되었다면 문제가 분명 발생할 것입니다.**



### Browser security

> 브라우저 보안성

각각의 브라우저 탭들은 코드가 실행되는 개별적인 구성(실행 환경)입니다. 이는 각 탭의 대부분의 경우는 완전히 독립적이고, 하나의 탭의 코드는 다른 탭이나 웹사이트에 직접적으로 영향을 줄 수 없다는 의미입니다. 보안성에 좋은 방법입니다. 만약 이러한 부분이 없다면, 해커들이 다른 웹사이트로 부터 정보를 가로채는 등 나쁜 짓을 할 수 있습니다.

```markdown
Note: 물론 코드나 정보를 동떨어진 웹사이트나 탭으로 전송할 수 있는 안전한 방식이 존재합니다. 하지만 지금 과정과는 거리가 멀기 때문에 여기서는 다루지 않도록 하겠습니다.
```



### JavaScript running order

> 자바스크립트 실행 순서

브라우저에서 자바스크립트를 만났을 때 일반적으로는 위에서 아래 순서대로 실행됩니다. 이는 순서에 주의해서 코드를 작성해야한다는 의미입니다. 예를 들어, 아래의 첫번째 예제를 통해 자바스크립트 블록을 반환해봅시다.

```JavaScript
const para = document.querySelector('p');
//HTML 요소 중 p태그를 선택

para.addEventListener('click', updateName);
//para에 저장된 객체가 클릭되었을 때 updateName 함수를 실행

function updateName() {
  let name = prompt('Enter a new name');
  //'Enter a new name'과 입력란 출력하여 입력받은 값을 name에 저장
  para.textContent = 'Player 1: ' + name;
  //papa(p태그)에 새로운 문자열 저장
}
```

1. 먼저 p태그의 요소를 para변수에 저장합니다(1번줄).
2. 그리고 `event listener`를 붙여(3번줄) p태그가 `클릭`되었을 때, `updateName()`코드 블록(중괄호로 묶여있는 부분)이 (5-8번줄) 실행되도록 합니다.
   `updateName()` 코드 블록(이렇게 계속적으로 사용할 수 있는 코드 블럭을 함수라고 합니다.).
3. 사용자로 하여금 새로운 이름을 입력받기를 요청하고, 사용자가 이름을 입력하면 화면에 출력하게 됩니다.

만약 1번줄과 3번줄을 바꿨다면 코드는 실행되지 않을 것입니다. 대신 브라우저의 개발자 콘솔창에 다음과 같은 에러 알림이 뜰 것입니다. — `TypeError: para is undefined.` 이는 para라는 객체가 아직 존재하지 않는다는 뜻으로, para라는 변수에 event listener는 추가할 수 없습니다.



### Interpreted versus compiled code

> 해석형 언어 VS 컴파일러형 언어

프로그래밍을 하는 입장에서 **interpreted** (인터프리트)와 **compiled**(컴파일)이라는 개념에 대해서는 들어보았을 것입니다. 자바스크립트는 해석형 언어입니다. **따라서 코드가 위에서 아래로 순차적으로 실행되고 그 즉시 결과가 반환됩니다.** 브라우저에서 동작하기 전에 다른 방식으로 코드를 변환할 필요가 없습니다.

반면에 컴파일러형 언어는 컴퓨터에 의해 동작되기전 다른 형식으로 변환하는 언어입니다. 예를 들면 C/C++과 같은 언어는 어셈블리어로 컴파일되어 동작됩니다.

이 둘의 관점은 각각의 장점을 가지고 있으니 다음장 부터 한번 알아봅시다.



### Server-side versus client-side code

> 서버측 코드 VS 클라이언트측 코드

웹 개발 맥락에서 **server-side** (서버측)과 **client-side** (클라이언트측) 코드에 대해 들어보았을 것입니다. 클라이언트측 코드란 사용자의 컴퓨터에서 작동되는 코드입니다. 만약 웹페이지를 보고자 한다면, 클라이언트측 코드가 사용자의 컴퓨터로 다운로드되고 브라우저가 이를 표시합니다. 이러한 자바스크립트 모듈을 정확히는 **클라이언트측 자바스크립트**라고 합니다.

반면 서버측 코드는 서버에서 작동되고, 그 결과가 사용자의 브라우저에 넘어가 표시됩니다. PHP, Python, Ruby, ASP.NET등이 서버측 웹 언어의 대표적 예라고 볼 수 있습니다. 물론 자바스크립트도 가능합니다! 유명한 Node.js란 환경을 통해 서버측에서도 자바스크립트가 사용 가능합니다.



### Dynamic versus static code

> 동적 VS 정적 코드

"동적"이라는 말은 클라이언트측 서버측 언어 모두를 가르킵니다. 이는 각기 다른 상황에서 적절한 정보가 보이고, 컨텐츠를 웹페이지나 앱 상에 계속적으로 노출시키는 역할을 합니다. 서버측 코드는 데이터베이스로 부터 데이터를 던지는 등 동적으로 새로운 컨텐츠들을 만듭니다. 반면에, 클라이언트측 자바스크립트는 새로운 HTML 표를 만들어 서버에서 요청한 데이터를 뿌려 사용자에게 보이는 등 동적으로 브라우저 안에서 작동됩니다. 이 둘 사이는 서로 미묘한 차이가 있지만, 서로 연관되어 있고 서버측 클라이언트측의 관계와 접근에 대해 알 필요가 있습니다.

동적으로 바뀌지 않는 페이지를 "정적"페이지라고 합니다. (항상 같은 콘텐츠를 보여줍니다.)