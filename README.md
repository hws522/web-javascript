# Web Browser control with JavaScript

<br>
<br>

### **HTML에서 JavaScript 로드**
---
JavaScript로 웹페이지를 제어하기 위해서는 JavaScript를 로드해야 한다.



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

`script 파일은 head 태그 보다 페이지의 하단에 위치시키는 것이 더 좋은 방법이다. `

