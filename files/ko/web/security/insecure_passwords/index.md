---
title: 안전하지 않은 비밀번호
slug: Web/Security/Insecure_passwords
translation_of: Web/Security/Insecure_passwords
---

HTTP를 통한 로그인 양식은 특히 사용자의 비밀번호를 추출하는데 사용할 수 있는 다양한 종류의 공격으로 인해 위험합니다. 네트워크 도청자는 네트워크를 스니핑하거나 전송되는 페이지를 수정하여 사용자의 비밀번호를 도용할 수 있습니다. 이 페이지는 안전하지 않은 비밀번호와 비밀번호 도용을 둘러싼 위험을 사용자와 개발자에게 경고하기 위해 Firefox가 마련한 보안 메커니즘에 대해 자세히 설명합니다.

[HTTPS](insecure_page2_with_arrows_cropped.jpeg) 프로토콜은 사용자 데이터를 도청(기밀성)하거나 네트워크에 수정(무결성)을 가하는 것으로부터 보호하도록 설계되었습니다. 사용자 데이터를 처리하는 웹사이트는 HTTPS를 사용하여 공격자로부터 사용자를 보호해야 합니다. 웹사이트에서 HTTP 대신 HTTPS를 사용하는 경우 사용자 정보(예 : 로그인 자격 증명)를 훔치는 일은 쉽지 않습니다. 이것은 [Firesheep](https://codebutler.github.io/firesheep/)에 의해 유명하게 시연되었습니다.

이 문제를 해결하려면 서버에 SSL/TLS 인증서를 설치하고 구성하십시오. 무료 및 유료 인증서를 제공하는 다양한 공급 업체가 있습니다. 클라우드 플랫폼을 사용하는 경우 HTTPS를 사용하는 고유한 방법이 있을 수 있습니다.

## Firefox 비밀번호 보안 표시기

위에서 설명한 위협을 알리기 위해서, Firefox는 많은 경고 메커니즘을 구현합니다.

1. Firefox 51버전부터는 로그인 페이지에 보안 연결이 없는 경우, 아래와 보이는 것과 같은 주소 표시줄에 빨간색으로 취소 표시가 있는 잠금 아이콘을 표시합니다.

    ![Lock Icon](https://support.cdn.mozilla.net/media/uploads/gallery/images/2015-11-17-12-13-18-2faa61.png)

2. Firefox 52버전부터는 URL 표시줄과 안전하지 않은 양식의 선택된 비밀번호 필드 아래에 명확한 경고를 표시합니다.

    ![Warning](https://support.cdn.mozilla.net/media/uploads/gallery/images/2017-04-21-23-52-53-ba340d.png)

3. Firefox 52버전부터는 안전하지 않은 로그인 양식에 대한 자동 채우기도 비활성화했습니다. 사용자는 저장된 로그인 정보를 드롭다운 목록에서 수동으로 완료할 수 있습니다.
4. 안전하지 않은 로그인 양식에 대한 경고는 다음 섹션에서 설명하는 것처럼 모든 Firefox 릴리스의 개발자 콘솔 보안창에서 찾을 수 있습니다.

## 웹 콘솔 메시지

이 섹션에서는 안전하지 않은 비밀번호에 대한 응답으로 Firefox DevTools의 개발자 콘솔에 표시되는 보안 메시지에 대해 설명합니다.

### HTTP를 통한 로그인 양식 제공

Form action이 HTTPS URL 인 경우에도 공격자는 사용자가 받을 페이지에 수정을 가할 수 있으므로 사용자의 로그인 양식이 보호되지 않습니다 (예 : 공격자가 form의 목적지를 변경하여 중요한 데이터를 공격자가 제어하는 서버로 보내거나, 사용자가 비밀번호를 입력할 때 비밀번호를 도용하는 키로깅 스크립트를 삽입할 수 있습니다). 웹 콘솔의 보안 탭은 개발자와 사용자에게 보안 문제에 대해 경고합니다.

![Insecure login form shown with the Web Console and contextual warning on the password field.](insecure_password_console_contextual_sm.png)

> **참고:** **주의** : HTTP 문서에 HTTPS 로그인 페이지를 포함시키는 것도 안전하지 않습니다. 공격자는 악의적인 사이트를 가리키도록 프레임 URL을 변경할 수 있습니다.

### Form action 에 HTTP URL 사용

이 경우 사용자가 입력하는 모든 데이터는 네트워크를 통해 일반 텍스트로 전송됩니다. 사용자의 비밀번호가 사용자의 컴퓨터를 떠나서 웹사이트의 서버에 도달할 때까지 네트워크를 스니핑하는 누구든 사용자의 비밀번호를 볼 수 있습니다.

![Insecure login form action shown with the Web Console and contextual warning on the password field.](insecure_action_password_console_contextual_sm.png)

## 비밀번호 재사용에 대한 주의사항

가끔씩 웹사이트는 사용자이름과 비밀번호를 요구하지만 실제로는 매우 민감한 데이터는 저장하지 않습니다. 예를 들어, 뉴스 사이트는 사용자가 돌아가서 읽고 싶어하는 뉴스 기사를 저장할 수 있지만 사용자에 대한 다른 데이터는 저장하지 않을 수 있습니다. 뉴스 사이트의 웹 개발자는 자신의 사이트와 사용자 자격 증명을 확보하려는 동기가 적을 수 있습니다.

불행하게도 [비밀번호 재사용은 큰 문제입니다.](https://www.lightbluetouchpaper.org/2011/02/09/measuring-password-re-use-empirically/) 사용자는 여러 사이트(뉴스 웹사이트, 소셜 네트워크, 이메일 제공 업체, 은행)에서 동일한 비밀번호를 사용합니다. 따라서 사용자이름과 비밀번호로 사이트에 접근하는 것이 큰 위험으로 보이지 않더라도 동일한 사용자이름과 비밀번호를 사용하여 은행 계좌에 로그인한 사용자에게는 큰 위험이 따릅니다. 공격자가 점점 더 똑똑해지고 있습니다. 그들은 한 사이트에서 사용자이름/암호 쌍을 훔친 다음 더 수익성있는 사이트에서 다시 사용하려고 시도합니다.

## See also

- [HTTP를 통한 비밀번호는 더 이상 안됩니다, 제발!](https://blog.mozilla.org/tanvi/2016/01/28/no-more-passwords-over-http-please/) — 더 자세한 정보와 FAQ를 가진 블로그.

{{QuickLinksWithSubpages("/en-US/docs/Web/Security")}}
