---
title: HTTP 메시지
slug: Web/HTTP/Messages
tags:
  - Guide
  - HTTP
  - HTTP/1.1
  - HTTP/2
  - Response
  - request
translation_of: Web/HTTP/Messages
---
{{HTTPSidebar}}

HTTP 메시지는 서버와 클라이언트 간에 데이터가 교환되는 방식입니다. 메시지 타입은 두 가지가 있습니다. 요청(_request)은_ 클라이언트가 서버로 전달해서 서버의 액션이 일어나게끔 하는 메시지고, 응답(*response)은 요청*에 대한 서버의 답변입니다.

HTTP 메시지는 ASCII로 인코딩된 텍스트 정보이며 여러 줄로 되어 있습니다. HTTP 프로토콜 초기 버전과 HTTP/1.1에서는 클라이언트와 서버 사이의 연결을 통해 공개적으로 전달되었습니다. 이렇게 한 때 사람이 읽을 수 있었던 메시지는 HTTP/2에서는 최적화와 성능 향상을 위해 HTTP 프레임으로 나누어집니다.

웹 개발자, 또는 웹 마스터가 손수 HTTP 메시지를 텍스트로 작성하는 경우는 드뭅니다. 대신에 소프트웨어, 브라우저, 프록시, 또는 웹 서버가 그 일을 합니다. HTTP 메시지는 설정 파일(프록시 혹은 서버의 경우), API(브라우저의 경우), 혹은 다른 인터페이스를 통해 제공됩니다.

![From a user-, script-, or server- generated event, an HTTP/1.x msg is generated, and if HTTP/2 is in use, it is binary framed into an HTTP/2 stream, then sent.](https://mdn.mozillademos.org/files/13825/HTTPMsg2.png)

HTTP/2의 이진 프레이밍 메커니즘(binary framing mechanism)은 사용 중인 API나 설정 파일 등을 변경하지 않아도 되도록 설계 되었기 때문에, 사용자가 보고 이해하기 쉽습니다.

HTTP 요청과 응답의 구조는 서로 닮았으며, 그 구조는 다음과 같습니다.

1. 시작 줄(start-line)에는 실행되어야 할 요청, 또은 요청 수행에 대한 성공 또는 실패가 기록되어 있습니다. 이 줄은 항상 한 줄로 끝납니다.
2. 옵션으로 HTTP 헤더 세트가 들어갑니다. 여기에는 요청에 대한 설명, 혹은 메시지 본문에 대한 설명이 들어갑니다.
3. 요청에 대한 모든 메타 정보가 전송되었음을 알리는 빈 줄(blank line)이 삽입됩니다.
4. 요청과 관련된 내용(HTML 폼 콘텐츠 등)이 옵션으로 들어가거나, 응답과 관련된 문서(document)가 들어갑니다. 본문의 존재 유무 및 크기는 첫 줄과 HTTP 헤더에 명시됩니다.

HTTP 메시지의 시작 줄과 HTTP 헤더를 묶어서 요청 _헤드(head)라고 부르며_, 이와 반대로 HTTP 메시지의 페이로드는 *본문(body)*이라고 합니다.

![Requests and responses share a common structure in HTTP](https://mdn.mozillademos.org/files/13827/HTTPMsgStructure2.png)

## HTTP 요청

### 시작 줄

HTTP 요청은 서버가 특정 동작을 취하게끔 만들기 위해 클라이언트에서 전송하는 메시지입니다. 시작 줄은 다음과 같이 세 가지 요소로 이루어져 있습니다.

1. 첫번째는 _[HTTP 메서드](/ko/docs/Web/HTTP/Methods)로_, 영어 동사({{HTTPMethod("GET")}}, {{HTTPMethod("PUT")}},{{HTTPMethod("POST")}}) 혹은 명사({{HTTPMethod("HEAD")}}, {{HTTPMethod("OPTIONS")}})를 사용해 서버가 수행해야 할 동작을 나타냅니다. 예를 들어, `GET`은 리소스를 클라이언트로 가져다 달라는 것을 뜻하며, `POST`는 데이터가 서버로 들어가야 함을 의미(리소스를 새로 만들거나 수정하기 위해, 또는 클라이언트로 돌려 보낼 임시 문서를 생성하기 위해)합니다.
2. 두번째로 오는 요청 타겟은 주로 {{glossary("URL")}}, 또는 프로토콜, 포트, 도메인의 절대 경로로 나타낼 수도 있으며 이들은 요청 컨텍스트에 의해 특정지어 집니다. 요청 타겟 포맷은 HTTP 메소드에 따라 달라집니다. 포맷에는 다음과 같은 것들이 있습니다.

    - origin 형식: 끝에 `'?'`와 쿼리 문자열이 붙는 절대 경로입니다. 이는 가장 일반적인 형식이며, `GET`, `POST`, `HEAD`, `OPTIONS` 메서드와 함께 사용합니다.
      `POST / HTTP 1.1 GET /background.png HTTP/1.0 HEAD /test.html?query=alibaba HTTP/1.1 OPTIONS /anypage.html HTTP/1.0`
    - _absolute 형식: 완전한 URL 형식입니다._ 프록시에 연결하는 경우 대부분 `GET`과 함께 사용됩니다.
      `GET http://developer.mozilla.org/en-US/docs/Web/HTTP/Messages HTTP/1.1`
    - _authority 형식:_ 도메인 이름 및 옵션 포트(`':'`가 앞에 붙습니다)로 이루어진 URL의 authority component 입니다.​​​​ HTTP 터널을 구축하는 경우에만 `CONNECT`와 함께 사용할 수 있습니다.
      `CONNECT developer.mozilla.org:80 HTTP/1.1`
    - _asterisk 형식:_ `OPTIONS`와 함께 별표(`'*'`) 하나로 간단하게 서버 전체를 나타냅니다. ​​​​​
      `OPTIONS * HTTP/1.1`

3. 마지막으로 ​​​​*HTTP 버전이 들어갑니다. 메시지의 남은* 구조를 결정하기 때문에, 응답 메시지에서 써야 할 HTTP 버전을 알려주는 역할을 합니다.

### 헤더

요청에 들어가는 [HTTP 헤더](/ko/docs/Web/HTTP/Headers)는 HTTP 헤더의 기본 구조를 따릅니다. 대소문자 구분없는 문자열 다음에 콜론(`':'`)이 붙으며, 그 뒤에 오는 값은 헤더에 따라 달라집니다. 헤더는 값까지 포함해 한 줄로 구성되지만 꽤 길어질 수 있습니다.

다양한 종류의 요청 헤더가 있는데, 이들은 다음과 같이 몇몇 그룹으로 나눌 수 있습니다.

- General 헤더: {{HTTPHeader("Via")}}와 같은 _헤더는_ 메시지 전체에 적용됩니다.
- Request 헤더: {{HTTPHeader("User-Agent")}}, {{HTTPHeader("Accept-Type")}}와 같은 헤더는 요청의 내용을 좀 더 구체화 시키고({{HTTPHeader("Accept-Language")}}), 컨텍스를 제공하기도 하며({{HTTPHeader("Referer")}}), 조건에 따른 제약 사항을 가하기도 하면서({{HTTPHeader("If-None")}}) 요청 내용을 수정합니다.
- Entity 헤더: {{HTTPHeader("Content-Length")}}와 같은 헤더는 요청 본문에 적용됩니다. 당연히 요청 내에 본문이 없는 경우 entity 헤더는 전송되지 않습니다.

![Example of headers in an HTTP request](http_request_headers2.png)

### 본문

본문은 요청의 마지막 부분에 들어갑니다. 모든 요청에 본문이 들어가지는 않습니다. `GET`, `HEAD`, `DELETE` , `OPTIONS`처럼 리소스를 가져오는 요청은 보통 본문이 필요가 없습니다. 일부 요청은 업데이트를 하기 위해 서버에 데이터를 전송합니다. 보통 (HTML 폼 데이터를 포함하는) `POST` 요청일 경우에 그렇습니다.

넓게 보면 본문은 두가지 종류로 나뉩니다.

- 단일-리소스 본문(single-resource bodies): 헤더 두 개({{HTTPHeader("Content-Type")}}와 {{HTTPHeader("Content-Length")}})로 정의된 단일 파일로 구성됩니다.
- 다중-리소스 본문(multiple-resource bodies): 멀티파트 본문으로 구성되는 [다중 리소스 본문](/ko/docs/Web/HTTP/Basics_of_HTTP/MIME_types#multipartform-data)에서는 파트마다 다른 정보를 지니게 됩니다. 보통 [HTML 폼](/ko/docs/Web/Guide/HTML/Forms)과 관련이 있습니다.

## HTTP 응답

### 상태 줄

HTTP 응답의 시작 줄은 *상태 줄(status line)*이라고 불리며, 다음과 같은 정보를 가지고 있습니다.

1. _프로토콜 버전:_ 보통 `HTTP/1.1`입니다.
2. 상태 코드: 요청의 성공 여부를 나타냅니다. {{HTTPStatus("200")}}, {{HTTPStatus("404")}} 혹은 {{HTTPStatus("302")}}입니다.
3. 상태 텍스트: 짧고 간결하게 상태 코드에 대한 설명을 글로 나타내어 사람들이 HTTP 메시지를 이해할 때 도움이 됩니다.

상태 줄은 일반적으로 `HTTP/1.1 404 Not Found.` 같이 생겼습니다.

### 헤더

응답에 들어가는 [HTTP 헤더](/ko/docs/Web/HTTP/Headers)는 다른 헤더와 동일한 구조를 따릅니다. 대소문자를 구분하지 않는 문자열 다음에 콜론(`':'`)이 오며, 그 뒤에 오는 값은 구조가 헤더에 따라 달라집니다. 헤더는 값을 포함해 전체를 한 줄로 표시합니다.

다양한 종류의 응답 헤더가 있는데, 이들은 다음과 같이 몇몇 그룹으로 나눌 수 있습니다.

- General 헤더: {{HTTPHeader("Via")}}와 같은 _헤더는_ 메시지 전체에 적용됩니다.
- Response 헤더: {{HTTPHeader("Vary")}}와 {{HTTPHeader("Accept-Ranges")}}와 같은 헤더는 상태 줄에 미처 들어가지 못했던 서버에 대한 추가 정보를 제공합니다.
- Entity 헤더: {{HTTPHeader("Content-Length")}}와 같은 헤더는 요청 본문에 적용됩니다. 당연히 요청 내에 본문이 없는 경우 entity 헤더는 전송되지 않습니다.

![Example of headers in an HTTP response](http_response_headers2.png)

### 본문

본문은 응답의 마지막 부분에 들어갑니다. 모든 응답에 본문이 들어가지는 않습니다. {{HTTPStatus("201")}}, {{HTTPStatus("204")}}과 같은 상태 코드를 가진 응답에는 보통 본문이 없습니다.

넓게 보면 본문은 세가지 종류로 나뉩니다.

- 이미 길이가 알려진 단일 파일로 구성된 단일-리소스 본문: 헤더 두개({{HTTPHeader("Content-Type")}}와 {{HTTPHeader("Content-Length")}})로 정의 합니다.
- 길이를 모르는 단일 파일로 구성된 단일-리소스 본문: {{HTTPHeader("Transfer-Encoding")}}가 `chunked`로 설정되어 있으며, 파일은 청크로 나뉘어 인코딩 되어 있습니다.
- 서로 다른 정보를 담고 있는 멀티파트로 이루어진 [다중 리소스 본문](/ko/docs/Web/HTTP/Basics_of_HTTP/MIME_types#multipartform-data): 이 경우는 상대적으로 위의 두 경우에 비해 보기 힘듭니다.

## HTTP/2 프레임

HTTP/1.x 메시지는 성능상의 결함을 몇가지 내포하고 있습니다.

- 본문은 압축이 되지만 헤더는 압축이 되지 않습니다.
- 연속된 메시지들은 비슷한 헤더 구조를 띄기 마련인데, 그럼에도 불구하고 메시지마다 반복되어 전송되고 있습니다.
- 다중전송(multiplexing)이 불가능합니다. 서버 하나에 연결을 여러개 열어야 합니다. 적극적인(warm) TCP 연결이 소극적인(cold) TCP 연결보다 효율적인데 말이죠.

HTTP/2에서는 추가적인 단계가 도입되었습니다. HTTP/1.x 메시지를 프레임으로 나누어 스트림에 끼워 넣는 것입니다. 데이터와 헤더 프레임이 분리 되었기 때문에 헤더를 압축할 수 있습니다. 스트림 여러개를 하나로 묶을 수 있어서(이러한 과정을 멀티플렉싱이라 합니다), 기저에서 수행되는 TCP 연결이 좀 더 효율적이게 이루어집니다.

![HTTP/2 modify the HTTP message to divide them in frames (part of a single stream), allowing for more optimization.](https://mdn.mozillademos.org/files/13819/Binary_framing2.png)

이제 웹 개발자 입장에서는 HTTP 프레임을 매우 쉽게 살펴볼 수 있게 되었습니다. HTTP 프레임은 HTTP/2에서 추가된 단계이며, HTTP/1.1 메시지와 그 기저를 이루는 전송 프로토콜 사이를 메워주는 존재입니다. 그렇다고 해서 HTTP 프레임 때문에 개발자들이 API를 바꿔야 할 필요는 없습니다. 브라우저와 서버 둘 다 모두 HTTP 프레임을 받아 들일 수 있다면, HTTP/2가 활성화 된 후에 사용될 것입니다.

## 결론

HTTP 메시지는 HTTP에서 핵심적인 역할을 합니다. 메시지 구조는 단순하게 이루어져 있으며, 확장성도 매우 좋습니다. HTTP/2 프레이밍 메커니즘 덕분에 HTTP/1.x 구문과 기저가 되는 전송 프로토콜 사이에 새로운 중간 단계가 추가 되었습니다. 프로토콜을 자체적으로 수정하지 않고 이미 입증된 메커니즘을 바탕으로 이뤄낸 것입니다.
