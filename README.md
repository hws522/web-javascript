# Web Browser control with JavaScript

<br>
<br>

### **HTML에서 JavaScript 로드**
---
JavaScript로 웹페이지를 제어하기 위해서는 JavaScript를 로드해야 한다.

<br>


**Inline**

inline 방식은 태그에 직접 자바스크립트를 기술하는 방식이다. 장점은 태그에 연관된 스크립트가 분명하게 드러난다는 점이다. 하지만 정보와 제어가 섞여 있기 때문에 정보로서의 가치가 떨어진다.

```
<!DOCTYPE html>
<html>
<body>
    <input type="button" onclick="alert('Hello world')" value="Hello world" />
</body>
</html>
```

**script**

`<script></script>` 태그를 만들어서 여기에 자바스크립트 코드를 삽입하는 방식이다. 장점은 html 태그와 js 코드를 분리할 수 있다는 점이다. 

```
<!DOCTYPE html>
<html>
<body>
    <input type="button" id="hw" value="Hello world" />
    <script type="text/javascript">
        var hw = document.getElementById('hw');
        hw.addEventListener('click', function(){
            alert('Hello world');
        })
    </script>
</body>
</html>
```

**외부 파일로 분리**

js를 별도의 파일로 분리할 수도 있다. 장점은 보다 엄격하게 정보와 제어를 분리할 수 있다. 하나의 js 파일을 여러 웹페이지에서 로드함으로서 js의 재활용성을 높일 수 있다. 캐쉬를 통해서 속도의 향상, 전송량의 경량화를 도모할 수 있다.

```
<!DOCTYPE html>
<html>
<body>
    <input type="button" id="hw" value="Hello world" />
    <script type="text/javascript" src="script2.js"></script>
</body>
</html>
```

```
// script2.js

var hw = document.getElementById('hw');
hw.addEventListener('click', function(){
    alert('Hello world');
})
```

script를 head 태그에 위치시킬 수도 있다. 하지만 이 경우는 오류가 발생한다.

```
<!DOCTYPE html>
<html>
<head>
    <script src="script2.js"></script>
</head>
<body>
    <input type="button" id="hw" value="Hello world" />
</body>
</html>
```

아래와 같이 script2.js의 코드를 수정해야 한다.

```
window.onload = function(){
    var hw = document.getElementById('hw');
    hw.addEventListener('click', function(){
        alert('Hello world');
    })
}
```

window.onload = function(){} 함수는 웹브라우저의 모든 구성요소에 대한 로드가 끝났을 때 브라우저에 의해서 호출되는 함수다. 이러한 것을 이벤트라고 한다.

`script 파일은 head 태그보다 페이지의 하단에 위치시키는 것이 더 좋은 방법이다. `

<br>

### **Object Model**
---

웹브라우저의 구성요소들은 하나하나가 객체화되어 있다. 자바스크립트로 이 객체를 제어해서 웹브라우저를 제어할 수 있게 된다. 이 객체들은 서로 계층적인 관계로 구조화되어 있다. BOM과 DOM은 이 구조를 구성하고 있는 가장 큰 틀의 분류라고 할 수 있다.

<br>


**JavaScript Core**

JavaScript 언어 자체에 정의되어 있는 객체들. 

**BOM**

Browser Object Model. 웹페이지의 내용을 제외한 브라우저의 각종 요소들을 객체화시킨 것이다. 전역객체 Window의 프로퍼티에 속한 객체들이 이에 속한다. 

```
<!DOCTYPE html>
<html>
<body>
    <input type="button" onclick="alert(window.location)" value="alert(window.location)" />
    <input type="button" onclick="window.open('bom.html')" value="window.open('bom.html')" />
</body>
</html>
```

**DOM**

Document Object Model. 웹페이지의 내용을 제어한다. window의 프로퍼티인 document 프로퍼터에 할당된 Document 객체가 이러한 작업을 담당한다. 

Document 객체의 프로퍼티는 문서 내의 주요 엘리먼트에 접근할 수 있는 객체를 제공한다.

```
<!DOCTYPE html>
<html>
<body>
    <img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/course/94.png" />
    <img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/course/94.png" />
    <img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/course/94.png" />
    <img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/course/94.png" />
    <img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/course/94.png" />
    <script>
        // body 객체
        console.log(document.body);
        // 이미지 객체들의 리스트
        console.log(document.images);
    </script>
</body>
</html>
```

또한 특정한 엘러먼트의 객체를 획득할 수 있는 메소드도 제공한다. 

```
<!DOCTYPE html>
<html>
<body>
    <img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/course/94.png" />
    <img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/course/94.png" />
    <img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/course/94.png" />
    <img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/course/94.png" />
    <img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/course/94.png" />
    <script type="text/javascript">
        // body 객체
        console.log(document.getElementsByTagName('body')[0]);
        // 이미지 객체들의 리스트
        console.log(document.getElementsByTagName('body'));
    </script>
</body>
</html>
```

<br>

### **Window 객체**
---
Window 객체는 모든 객체가 소속된 객체이고, 전역객체이면서, 창이나 프레임을 의미한다. 

<br>

**전역객체**

Window 객체는 식별자 window를 통해서 얻을 수 있다. 또한 생략 가능하다. Window 객체의 메소드인 alert을 호출하는 방법은 아래와 같다.

```
<!DOCTYPE html>
<html>
<script>
    alert('Hello world');
    window.alert('Hello world');
</script>
<body>
 
</body>
</html>
```

아래는 전역변수 a에 접근하는 방법이다.  

```
<!DOCTYPE html>
<html>
<script>
    var a = 1;
    alert(a);
    alert(window.a);
</script>
<body>
 
</body>
</html>
```

객체를 만든다는 것은 결국 window 객체의 프로퍼티를 만드는 것과 같다.

```
<!DOCTYPE html>
<html>
<script>
    var a = {id:1};
    alert(a.id);
    alert(window.a.id);
</script>
<body>
 
</body>
</html>
```

예제를 통해서 알 수 있는 것은 전역변수와 함수가 사실은 window 객체의 프로퍼티와 메소드라는 것이다. 또한 모든 객체는 사실 window에 소속되어 있다는 것도 알 수 있다. 이러한 특성을 ECMAScript에서는 Global 객체라고 부른다. ECMAScript의 Global 객체는 호스트 환경에 따라서 이름이 다르고 하는 역할이 조금씩 다르다. 웹브라우저 자바스크립트에서 Window 객체는 ECMAScript의 전역객체이면서 동시에 웹브라우저의 창이나 프레임을 제어하는 역할을 한다.

<br>

### **사용자와의 커뮤니케이션**
---

HTML은 form을 통해서 사용자와 커뮤니케이션할 수 있는 기능을 제공한다. 자바스크립트에는 사용자와 정보를 주고 받을 수 있는 간편한 수단을 제공한다.

<br>


**alert**

경고창이라고 부른다. 사용자에게 정보를 제공하거나 디버깅등의 용도로 많이 사용한다. 최근에는 개발자도구의 console.log를 주로 사용함.

```
<!DOCTYPE html>
<html>
    <body>
        <input type="button" value="alert" onclick="alert('hello world');" />
    </body>
</html>
```

**confirm**

확인을 누르면 true, 취소를 누르면 false를 리턴한다.

```
<!DOCTYPE html>
<html>
    <body>
        <input type="button" value="confirm" onclick="func_confirm()" />
        <script>
            function func_confirm(){
                if(confirm('ok?')){
                    alert('ok');
                } else {
                    alert('cancel');
                }
            }
        </script>
    </body>
</html>
```

**prompt**

입력값이 같으면 true, 다르면 false를 리턴한다.

```
<!DOCTYPE html>
<html>
    <body>
        <input type="button" value="prompt" onclick="func_prompt()" />
        <script>
            function func_prompt(){
                if(prompt('id?') === 'egoing'){
                    alert('welcome');
                } else {
                    alert('fail');
                }
            }
        </script>
    </body>
</html>
```

<br>

### **Location 객체**
---

Location 객체는 문서의 주소와 관련된 객체로 Window 객체의 프로퍼티다. 이 객체를 이용해서 윈도우의 문서 URL을 변경할 수 있고, 문서의 위치와 관련해서 다양한 정보를 얻을 수 있다.


<br>


**현재 window의 URL 알아내기**

아래는 현재 윈도우의 문서가 위치하는 URL을 알아내는 방법이다. `location.href`가 더 선호되는 방법이다.

```
console.log(location.toString(), location.href);
```

**URL Parsing**

location 객체는 URL을 의미에 따라서 별도의 프로퍼티로 제공하고 있다.

```
console.log(location.protocol, location.host, location.port, location.pathname, location.search, location.hash);
```

**URL 변경하기**

아래 코드는 현재 문서를 `http://seo.net`으로 이동한다.

```
location.href = "http://seo.net";
```

아래와 같은 방법도 같은 효과를 낸다. 하지만 `location.href`가 더 명시적이다.

```
location = "http://seo.net";
```

아래는 현재 문서를 리로드하는 간편한 방법을 제공한다.

```
location.reload();
```




