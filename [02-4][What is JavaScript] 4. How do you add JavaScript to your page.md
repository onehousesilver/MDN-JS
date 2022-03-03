## What is JavaScript?

> 출처: https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/What_is_JavaScript


### How do you add JavaScript to your page?
>  웹 페이지에 JavaScript를 어떻게 넣나요?

자바스크립트는 CSS와 같은 방식으로 HTML 페이지에 적용됩니다. CSS는 외부의 스타일시트를 적용하기 위해 `<link>`를 사용하거나 내부의 스타일시트를 적용하기 위해 `<style>` 요소를 사용하는 반면,자바스크립트는 HTML상에서 오직 `<script>` 태그만으로 사용이 가능합니다. 어떻게 작동되는지 한번 살펴봅시다.



### Internal JavaScript
> HTML 내부의 자바스크립트

html 파일에서 `</body>` 태그 직전에 코드를 추가합니다.

```JS
<script>

  // JavaScript goes here

</script>
```



### External JavaScript

> 외부의 자바스크립트

만약에 외부 파일로 자바스크립트를 위치시키고 싶다면 어떻게 할까요? 이에 대해서 알아봅니다.

먼저, HTML 파일이 있는 디렉토리에 `script.js`라는 새로운 파일을 만듭니다. 
파일의 확장자가 `.js`이면 그 파일이 `자바스크립트`로 이루어져 있음을 뜻합니다.

아래의 태그를 HTML 코드에 붙여넣기 한 후 저장합니다.

```JS
<script src="script.js" defer></script>
```

자바스크립트 파일을 외부에 생성해서 불러오는걸 더 권장합니다.



### Inline JavaScript handlers
> 인라인 JavaScript 처리기

실제 HTML 속에 포함된 자바스크립트코드를 함께 쓸 수 있습니다. 이는 다음과 같으니 참고해보세요.

```JS
function createParagraph() {
  let para = document.createElement('p');
  para.textContent = 'You clicked the button!';
  document.body.appendChild(para);
}
//HTML 내의 <scirpt>태그 내부에 작성
```

```html
<button onclick="createParagraph()">Click me!</button>
```
이는 다음과 같은 예제로 볼 수 있습니다.


이 데모 예제는 `<button>`태그에 `onclick`속성에 대한 값을 함수이름으로 넣어 버튼이 클릭될 때마다 함수가 실행되도록 작성하였습니다.

하지만, **이 방법은 효율적이지 않습니다.**  이는 자바스크립트와 함께 HTML 소스를 복잡하게 할 수 있습니다. 또한 함수를 만들기 위한 모든 버튼 마다 `onclick="createParagraph()"` 속성을 포함해야합니다.



### Using addEventListener instead
> `addEventListener`의 사용

JavaScript 코드만으로도 모든 버튼에 함수를 연결할 수 있습니다. 위의 내용을 의도한대로 수정한다면 다음과 같습니다.

HTML에 JavaScript를 포함하는 대신 순수 JavaScript 구조를 사용합니다. `querySelectorAll()` 기능을 사용하면 페이지의 모든 버튼을 선택할 수 있습니다. 그런 다음 버튼을 반복하여 `addEventListener()`를 사용하여 각각에 대해 이벤트를 할당할 수 있습니다. 이에 대한 코드는 다음과 같습니다.

이 코드는 onclick 속성 코드 보다 조금 길어보이지만, 페이지가 많든, 버튼의 수가 많든 적든 상관없이**모든 버튼들이 같은 기능을 할 수 있도록 합니다.** 물론 자바스크립트 코드를 변경할 필요가 없습니다.

```JS
const buttons = document.querySelectorAll('button');
//모든 <button>태그를 List 형태로 buttons 변수에 저장한다.

for (let i = 0; i < buttons.length ; i++) {
  buttons[i].addEventListener('click', createParagraph);
}
//복수이기 때문에 for를 사용해 루프를 돌린다.
```



### Script loading strategies

> 스크립트의 로딩 방법

작성된 스크립트를 브라우저가 적절한 때에 로딩하는것에 대해 몇가지 이슈가 있습니다. 중요한 것은 모든 HTML 요소는 **순서대로 페이지에 로드**된다는 것입니다. 만약 당신이 자바스크립트를 이용해 HTML 요소를 조작할 경우(정확하게는 DOM), 자바스크립트 코드가 조작 대상인 HTML 요소보다 먼저 실행된다면 조작할 요소가 존재하지 않는 상태이기 때문에 제대로 동작하지 않을 것입니다.

위의 코드 예제에서, 내부와 외부의 자바스크립트는 HTML Document의 `body`가 해석되기 전인 `head` 부분에 로드되고 실행되었습니다. **이는 에러를 일으킬 수 있습니다.** 그래서 여기에 사용되는 몇가지 해결방법들이 있습니다.

내부 자바스크립트 예제에서는 다음과 같이 구성하면 됩니다.

```JS
document.addEventListener("DOMContentLoaded", function() {
  ...
});
```

이 이벤트리스너는 `"DOMContentLoad" 이벤트`가 발생되었을 때 `function()`을 실행한다는 의미입니다. `"DOMContentLoad" 이벤트`는 브라우저가 완전히 로드되고 해석될때 발생됩니다. function(){} 내부의 자바스크립트 구문은 **이벤트가 발생되기 전까지는 실행되지 않습니다.** 따라서 모든 body태그의 요소가 로드된 이후 자바스크립트 코드가 실행되도록 만들어 에러를 피할 수 있습니다.

외부 자바스크립트 예제에서는 좀더 최신의 자바스크립트 문법인 `async` 속성을 사용하게 됩니다. 일반적으로 HTML요소를 로딩하는 중 `<scirpt>`태그를 만나면 JavaScript의 내용이 모두 다운될 때까지 HTML로딩은 멈추게 되는데, `async`요소는 `비동기방식`으로 `<script>`태그에 도달했을 때 브라우저에게 HTML 요소를 멈추지 않고 다운받도록 유지시킵니다.

```JS
<script src="script.js" async></script>
```
이 경우 `script`와 `HTML`은 모두 동시에 로드되고 작동할 것입니다.

> Note: 외부 스크립트 경우 async 속성을 사용하면 되기 때문에 내부 스크립트처럼 DOMContentLoaded이벤트를 사용할 필요가 없습니다. 하지만 async속성은 외부 스크립트의 경우만 동작합니다.

예전 방식은 `scirpt` 요소를 `body`태그의 맨 끝에 넣는 방법이었습니다(`</body>` 바로 위에). 이 방식을 사용해도 `body`태그가 모두 로드된 이후 `scirpt`가 실행되게 만들 수 있습니다. 문제는 이 방법과` DOMContentLoaded`를 이용한 방법 모두 **HTML DOM이 로드되기 전까지 script의 로딩과 파싱이 완전히 차단된다는 것입니다.** 이는 많은 자바스크립트 코드를 다루는 규모가 큰 사이트의 경우 사이트를 느리게 만드는 중요한 성능 문제를 야기할 수 있습니다. 이것이 `async 속성을 사용해야 하는 이유`입니다!

> Note: 자바스크립트의 비동기 개념은 이해하는데 시간이 오래 걸리기 때문에, 지금 이해되지 않는다면 현재 단계에선 외부 스크립트 방식만 사용하고 넘어가도 무방합니다.



### async & defer

더 깊게 들어가보면 이러한 코드문제를 해결하기 위한 방법은 실제로 두가지가 있습니다.
async 와defer 입니다. 두 가지의 차이를 봅시다.

`async` 스크립트는 **페이지 렌더링의 중단 없이 스크립트를 다운로드 하고, 또한 스크립트의 다운로드가 끝나자 마자 이를 실행시킵니다.** `async`는 외부 스크립트끼리의 구체적인 실행 순서는 보장하지 않고, 단지 나머지 페이지가 나타나는 동안 스크립트가 비동기방식으로 다운로드 되어 **중단되지 않는다는 것만 보장**합니다. async는 각각의 스크립트가 독립적으로, 서로에게 의존하지 않는 관계일 때 적절합니다.

아래의 예제를 보시죠.

```JS
<script async src="js/vendor/jquery.js"></script>

<script async src="js/script2.js"></script>

<script async src="js/script3.js"></script>
```
3개의 스크립트를 로딩하지만 **이들의 순서는 보장할 수 없습니다.** 이는 `script2.js`나 `script3.js`에 있는 함수가 `jquery.js`의 함수를 사용한다면 에러를 발생될 수 있다는 것을 의미합니다.

Defer는 이와 다르게 순서대로 다운로드 한 후 모든 스크립트와 내용이 다운로드 되었을 때 실행됩니다.

```JS
<script defer src="js/vendor/jquery.js"></script>

<script defer src="js/script2.js"></script>

<script defer src="js/script3.js"></script>
```
따라서 위의 예제의 경우에는 `jquery.js -> script2.js -> script3.js` 의 **순서가 보장됩니다.**

📢 **요약**

만약 `scirpt`들이 각각의 스크립트에 의존하지 않고 독립적으로 파싱되도 상관없다면, `async`를 사용합니다.
먄약 `sciprt`들이 의존하고 하나의 스크립트가 파싱될때까지 기다려야 한다면, `defer` 를 사용하고 각각의 `<script>` 태그들을 실행되길 원하는 순서대로 작성합니다.