---
title: What is a URL?
slug: Learn/Common_questions/What_is_a_URL
---
이 글은 Uniform Resource Locators (URLs) 를 설명한다. 또한, URL이 무엇이고 어떻게 구성되어 있는 지도 설명한다.

<table class="learn-box standard-table">
  <tbody>
    <tr>
      <th scope="row">선수지식:</th>
      <td>
        <a href="/en-US/docs/Learn/How_the_Internet_works"
          >인터넷이 작동하는 법</a
        >,
        <a href="/en-US/docs/Learn/What_is_a_Web_server">웹서버가 무엇인가</a>
        그리고
        <a href="/en-US/docs/Learn/Understanding_links_on_the_web"
          >웹상의 링크 속에 있는 개념</a
        >에 대해 먼저 알아야 한다.
      </td>
    </tr>
    <tr>
      <th scope="row">목적:</th>
      <td>URL을 배울 것이고, 웹에서 어떻게 URL이 작동하는 지 배운다.</td>
    </tr>
  </tbody>
</table>

## 요약

{{Glossary("Hypertext")}} 와 {{Glossary("HTTP")}} 함께, **_URL_** 은 웹에서 중요한 개념 중 하나이다. URL은 웹에 게시된 어떤 자원을 찾기 위해서 {{Glossary("Browser","browsers")}}에 의해 사용되는 메카니즘이다 .

**URL** 은 _Uniform Resource Locator_(인터넷에서 자원 위치)을 나타낸다. URL은 웹에서 정해진 유일한 자원의 주소일 뿐이다. 이론적으로, 각각의 유일한 URL은 유일한 자원을 가리킨다. 그런 자원은 HTML 페이지, CSS 문서, 이미지 등이 될 수 있다. 실제로, 여러 예외가 있는데, 가장 흔한 URL은 더 이상 존재하지 않는 자원이나 옮겨진 자원을 가리키는 것이다. URL에 의해 표현된 자원과 URL 자체는 웹서버에 의해 다루어지기 때문에, 자원과 관련 URL을 주의 깊게 관리하기 위해서 웹서버의 소유자에게 달려있다..

## Active Learning(능동 학습)

_아직 이용 가능한 능동학습이 없습니다. [Please, consider contributing](/ko/docs/MDN/Getting_started)._

## 깊게 들어가기

### 기본: URL의 구조

여기에 URL의 예제들이 있습니다:

```
https://developer.mozilla.org
https://developer.mozilla.org/en-US/docs/Learn/
https://developer.mozilla.org/en-US/search?q=URL
```

관련 페이지를 불러오기 위해서, 저 URL들 중 어떤 것이든 주소 창에 적을 수 있습니다. (자원).

URL 은 다른 파트들과, 몇몇의 의무와 선택사항들로 구성됩니다. 다음 URL을 사용하여 가장 중요한 부분을 봅시다:

```
http://www.example.com:80/path/to/myfile.html?key1=value1&key2=value2#SomewhereInTheDocument
```

- ![Protocol](https://mdn.mozillademos.org/files/15766/mdn-url-protocol@x2_update.png)
  - : `http` 는 프로토콜(규약)입니다. URL의 첫 파트는 브라우저가 어떤 규약을 사용해야 하는 지를 나타냅니다. 프로토콜은 컴퓨터 네트워크에서 데이터를 교환하거나 전송하기 위한 방법들의 세트입니다. 보통 웹사이트들을 위해, 이것은 HTTP 프로토콜이나 HTTP 프로토콜의 보안 버전입니다. 웹은 이 두 가지 중 하나를 요구합니다, 그러나 브라우저는 `mailto:` (메일 클라이언트를 열기 위한) 또는 파일을 전송하기 위해 `ftp:` 와 같은 다른 프로토콜들을 다루는 법 또한 알고 있습니다, 그러므로 만약 이런 프로토콜들을 보더라도 놀라지 마십시오.
- ![Domaine Name](mdn-url-domain@x2.png)
  - : `www.example.com` 은 도메인 이름입니다. 이것은 어떤 웹 서버가 요구되는 것인 지를 가리킵니다. 대안으로, 직접 {{Glossary("IP address")}}를 사용하는 것도 가능합니다, 그러나 덜 편리하기 때문에, 그것은 웹에서 주로 사용되지는 않습니다.
- ![Port](mdn-url-port@x2.png)
  - : `:80` 은 포트입니다. 이것은 기술적으로 웹서버에서 자원을 접근하기 위해 사용하는 "관문(gate)"을 가리킵니다. 만약 웹서버가 자원의 접근 하기 위해 표준 HTTP 포트 (HTTP를 위한 80, HTTPS를 위한 443)를 사용한다면, 포트 번호는 보통 생략합니다. 그렇지 않으면 포트 번호는 필수입니다.
- ![Path to the file](https://mdn.mozillademos.org/files/8019/mdn-url-path@x2.png)
  - : `/path/to/myfile.html` 은 웹서버에서 자원에 대한 경로입니다. 초기의 웹에서는, 웹서버상에서 물리적 파일 위치를 나타냈습니다. 요즘에는, 실제 물리적 경로를 나타내지 않고, 웹 서버에서 추상화하여 보여줍니다.
- ![Parameters](https://mdn.mozillademos.org/files/8021/mdn-url-parameters@x2.png)
  - : `?key1=value1&key2=value2` 는 웹서버에 제공하는 추가 파라미터입니다. 이 파라미터들은 `&` 기호로 구분된 키/값으로 짝을 이룬 리스트입니다. 웹 서버는 자원을 반환하기 전에 추가적인 작업을 위해 이런 파라미터들을 사용할 수 있습니다. 각각의 웹서버는 파라미터들을 언급하는 자신의 규칙을 갖고 있습니다. 그리고, 특정한 웹서버가 파라미터를 다루는 지 알기 위한 유일한 방법은 웹서버 소유자에게 묻는 것입니다.
- ![Anchor](https://mdn.mozillademos.org/files/8023/mdn-url-anchor@x2.png)
  - : `#SomewhereInTheDocument` 는 자원 자체의 다른 부분에 대한 anchor(닻) 입니다. An anchor 는 일종의 자원 안에서 "bookmark" 입니다. 즉, "bookmarked" 지점에 위치된 내용을 보여주기 위해 브라우저에게 방향을 알려줍니다. 예를 들어, HTML 문서에서 브라우저는 anchor가 정의한 곳의 점을 스크롤할 것입니다; 비디오나 오디오 문서에서, 브라우저는 앵커가 나타내는 시간을 찾으려 할 것입니다. **#**뒤에 오는 부분은 가치가 없습니다. 또한,_ **fragment identifier(부분 식별자)** 라고 알려져, 요청이 서버에 절대 보내지지 않습니다._

> **참고:** URLs을 말하면 [몇몇의 추가적인 부분과 규칙](http://en.wikipedia.org/wiki/Uniform_Resource_Locator)이 있다, 그러나 그것들은 일반적인 유저와 웹 개발자들에게 상관이 없다. 이것에 대해 걱정하지 말고, 완전한 기능적인 URLs를 구축하고 사용하기 위해 알 필요는 없다.

당신은 일반적인 우편 메일 주소처럼 URL을 생각할 것이다: *프로토콜*은 사용하고 싶은 우편 서비스다, *도메인 이름*은 도시나 마을이다, 그리고 _포트_ 우편 번호이다; *경로*는 메일이 전달되어야 하는 건물을 나타낸다; *파라미터*는 건물 번호와 같은 정보를 나타낸다; 그리고, 마지막으로, *anchor(앵커)*는 메일을 받는 실제 사람을 나타낸다.

### URLs 을 사용하는 법

어떤 URL이든 자원을 얻기 위해 브라우저의 주소창에 올바르게 적으면 된다!

{{Glossary("HTML")}} 언어 — [나중에 이야기할 것](/ko/docs/Learn/HTML/HTML_tags) — 가 URLs을 광범위하게 사용하게 만들었다:

- {{HTMLElement("a")}} 요소로 다른 문서와의 링크를 만들기 위해;
- {{HTMLElement("link")}} 또는 {{HTMLElement("script")}}처럼 다양한 요소를 통해서 관련된 자원을 가진 문서를 연결시키기 위해;
- 이미지 ({{HTMLElement("img")}} 요소), 비디오 ({{HTMLElement("video")}} 요소), 소리 또는 음악 ({{HTMLElement("audio")}} 요소), 등과 같은 미디어를 보여주기 위해;
- {{HTMLElement("iframe")}} 요소를 다른 HTML 문서에 보여주기 위해.

> **참고:** 한 페이지의 일부로서, 자원을 불러오기 위해 URLs 특정할 때, (`<script>`, `<audio>`, `<img>`, `<video>`, 와 같은 것을 사용할 때 처럼), 오직 HTTP와 HTTPS URL을 사용해야만 한다. 예를 들어, FTP를 사용하는 것은 부분적으로 안전하지 않고, 더 이상 많은 브라우저에서 지원하지 않는다.

{{Glossary("CSS")}} 또는 {{Glossary("JavaScript")}}와 같은 다른 기술들은 URLs를 광범위하게 사용한다 그리고, 이런 것들이 정말로 웹의 심장이다.

### 절대 URLs vs 상대 URLs

우리가 위에서 얘기한 것은 _절대 URL_ 이다. 그러나 또한 *상대 URL*도 있다. 그 차이가 의미하는 것을 더 자세히 알아봅시다.

요구한 부분의 URL은 URL이 사용되는 문맥에서 크게 의존한다. 브라우저의 주소바에서, URL은 어떤 문맥도 가지고 있지 않다, 그래서 위에서 본 것 처럼 전체 (또는 _절대_) URL을 제공해야 한다. 프로토콜(브라우저는 기본적으로 HTTP 를 사용한다)또는 포트(해당 웹서버가 몇몇의 흔치 않은 포트를 사용할 때만 요구한다.)를 포함할 필요는 없다. 그러나, URL의 모든 다른 부분(part)은 필요하다.

URL이 HTML 페이지와 같은 문서 내에서 사용될 때는 조금 다르다. 왜냐하면, 브라우저는 이미 문서의 자체 URL을 갖고 있기 때문에, 문서 내에서 이용가능한 어떤 URL의 잃어버린 부분(part)에 정보를 채우기 위해 사용한다. 오직 URL의 _path_ 부분을 보면, *절대 URL*과 *상대 URL*을 구별할 수 있다. 만약 URL의 경로 부분이 `"/`" 문자로 시작한다면, 그 브라우저는 현재 문서에서 주어진 문맥에서 참조없이, 서버의 루트(top root)에서 자원을 가지고 올 것이다.

더 분명하게 알기 위해 예제를 봅시다.

#### 절대 URLs의 예

- 전체 URL (이전에 사용한 것과 같은)

  - :

    ```
    https://developer.mozilla.org/en-US/docs/Learn
    ```

- 내포된 프로토콜

  - :

    ```
    //developer.mozilla.org/en-US/docs/Learn
    ```

    이 경우에, 브라우저는 URL을 호스팅한 문서를 불러오기 위해 사용한 것과 같은 프로토콜을 가진 URL을 부를 것이다.

- 내포된 도메인명

  - :

    ```
    /en-US/docs/Learn
    ```

    이것은 HTML 문서 내에서 절대 URL을 위한 가장 흔한 사용법이다. 브라우저는 같은 프로토콜과 그 URL을 호스팅한 문서를 불러오기 위해 사용한 것과 같은 도메인명을 사용할 것이다. **Note:** _프로토콜을 생략하는 것 없이, 도메인명을 생략하는 것을 가능하지 않다_.

#### 상대 URLs의 예

다음의 예를 더 잘 이해하기 위해, URL은 다음의 URL이 위치한 문서 내에서 불린다고 가정해봅시다: `https://developer.mozilla.org/en-US/docs/Learn`

- Sub-resources

  - :

    ```
    Skills/Infrastructure/Understanding_URLs
    ```

    URL이 `/`로 시작하지 않기 때문에, 브라우저는 현재 자원을 포함하는 서브 디렉토리에 있는 문서를 찾으려 할 것이다. 그래서 예를 들어, 이 URL에 도달하길 원하는 것이다: `https://developer.mozilla.org/en-US/docs/Learn/Skills/Infrastructure/Understanding_URLs`

- 디렉토리 트리에서 뒤로 가기

  - :

    ```
    ../CSS/display
    ```

    이 경우에, `../` 를 쓰는 것을 관례로 사용한다 — UNIX 파일 시스템에서 유래했다 — 브라우저에게 한 디렉토리에서 상위로 가고 싶다고 말하는 것이다. 여기서, 이 URL에 도달하고 싶은 것이다: `https://developer.mozilla.org/en-US/docs/Learn/../CSS/display`, 이렇게 단순화 된다: `https://developer.mozilla.org/en-US/docs/CSS/display`

### Semantic(의미있는) URLs

매우 기술적인 것에도 불구하고, URLs은 웹 사이트를 위한 인간이 읽을 수 있는 시작점을 나타낸다. URL은 저장될 수 있고, 누군가가 URL을 주소바에 기입할 수 있다. 사람들이 웹에 핵심에 있다. 그리고, [_semantic URLs_](http://en.wikipedia.org/wiki/Semantic_URL)이라 불리는 것을 구축하기 위해 최선을 고려한다. Semantic URLs은 기술적인 노하우와 상관없이 누구나 이해할 수 있게 하는 의미로 단어들을 사용한다.

언어학적 의미론(Semantics)은 컴퓨터와 상관없는 코스다. 아마도 자주 임의의 문자들의 조합처럼 보이는 URL을 봤을 것이다. 그러나 인간이 읽을 수 있는 URL들을 만드는 것에는 많은 장점이 있다:

- 당신이 URL을 조작하기 쉽게 한다.
- 어디에 있고, 무엇을 하고, 무엇을 읽거나 웹에서 상호작용하는 지에 대해 유저들에게 분명히 알려준다.
- 몇몇의 검색엔진은 관련 페이지들을 잘 분류하기 위해 이런 의미론을 사용할 수 있다.

## 다음 단계

- [도메인 명 이해하기](/ko/docs/Learn/Understanding_domain_names)
