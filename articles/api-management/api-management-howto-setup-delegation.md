---
title: "aaaHow toodelegate 사용자 등록 및 제품 구독"
description: "어떻게 toodelegate 사용자 등록 및 제품 구독 tooa 하는 타사 Azure API 관리에 알아봅니다."
services: api-management
documentationcenter: 
author: antonba
manager: erikre
editor: 
ms.assetid: 8b7ad5ee-a873-4966-a400-7e508bbbe158
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 406648db2d2f37c4dcda466294726d331cc0551b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodelegate-user-registration-and-product-subscription"></a>어떻게 toodelegate 사용자 등록 및 제품 구독
위임을 사용 하면 toouse 개발자 로그인-에/등록 및 구독 tooproducts로 처리 하기 위한 기존 웹 사이트 대신 toousing hello hello 개발자 포털에서 기본 제공 기능입니다. 웹 사이트 tooown hello 사용자 데이터를 사용 하도록 설정 하 고 사용자 지정 방식으로 이러한 단계의 hello 유효성 검사를 수행 합니다.

## <a name="delegate-signin-up"> </a>개발자 로그인 및 등록 위임
toodelegate 개발자 로그인 및 등록 tooyour 기존 웹 사이트 hello hello API 관리 개발자 포털에서 시작 된 이러한 모든 요청에 대 한 진입점으로 사용 하는 사이트에 특별 한 위임 끝점 toocreate 필요 합니다.

hello 최종 워크플로 다음과 같이 됩니다.

1. Hello API 관리 개발자 포털에 로그인 하거나 등록 링크 hello에 대 한 개발자 클릭
2. 브라우저는 리디렉션된 toohello 위임 끝점
3. 위임 끝점 반환 tooor 표시 합니다. UI 묻는 사용자를 리디렉션합니다 toosign 기능 또는 등록
4. 성공 시 hello 사용자가 리디렉션된 백 toohello API 관리 개발자 포털 페이지에서 시작

이제 첫 번째 설치 API 관리 tooroute toobegin, 위임 끝점을 통해 요청합니다. Hello API 관리 게시자 포털에서 클릭 **보안** hello를 클릭 한 다음 **위임** 탭 합니다. Hello 확인란 tooenable 'Delegate 등록 및 로그인'를 클릭 합니다.

![위임 페이지][api-management-delegation-signin-up]

* 어떤 특별 한 위임 끝점의 URL hello 되며 hello에 입력 결정 **위임 끝점 URL** 필드입니다. 
* Hello 내 **위임 인증 키** 필드 사용된 toocompute 요청 hello 확인 tooensure에 대 한 제공 된 서명 tooyou는 실제로 Azure API 관리에서 제공 되는 암호를 입력 합니다. Hello를 클릭할 수 있는 **생성** 단추 toohave API 관리 사용자에 대 한 키를 임의로 생성 합니다.

이제 toocreate hello 필요한 **위임 끝점**합니다. 몇 가지 작업 tooperform 했습니다.

1. 요청 hello 다음 폼에에서 나타납니다.
   
   > *http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={원본 페이지의 URL}&salt={문자열}&sig={문자열}*
   > 
   > 
   
    Hello 로그인 / 등록 사례에 대 한 쿼리 매개 변수:
   
   * **operation**: 위임 요청의 유형을 식별합니다. 이 경우 **SignIn**만 가능합니다.
   * **returnUrl**: hello hello 사용자 로그인 하거나 등록 링크를 클릭 하는 hello 페이지의 URL
   * **salt**: 보안 해시를 계산하는 데 사용되는 특수 salt 문자열입니다.
   * **sig**: 비교 tooyour 자체에 사용 되는 계산 된 보안 해시 toobe 계산 된 해시
2. 해당 hello 요청이 (선택 사항 이지만 보안에 대 한 권장 사항임) Azure API 관리에서 오는지 확인 합니다.
   
   * Hello를 기반으로 문자열의 한 hmac-sha512 해시 계산 **returnUrl** 및 **솔트** 쿼리 매개 변수 ([아래에 제공 된 예제 코드]):
     
     > HMAC(**salt** + '\n' + **returnUrl**)
     > 
     > 
   * Hello의 hello 위에서 계산 된 해시 toohello 값 비교 **sig** 쿼리 매개 변수입니다. Hello 두 해시가 일치 하는 경우 toohello 다음 단계에서 이동, 그렇지 않으면 hello 요청을 거부 합니다.
3. Sign / / 기호 위쪽에 대 한 요청을 받고 있는지 확인: hello **작업** 쿼리 매개 변수를 설정할 너무 "**SignIn**"입니다.
4. Hello 사용자 toosign 옵트인 하거나 등록 하는 UI 제공
5. Hello 사용자가 등록 해 있으면 toocreate 해당 계정에 대 한 API 관리에서입니다. [사용자 만들기] hello API 관리 REST API로 합니다. 이렇게 할 경우 사용자 저장소에 같거나 tooan ID 있습니다 수에 추적 하는 사용자 ID toohello hello를 설정 했는지 확인 합니다.
6. Hello 사용자가 성공적으로 인증 하면:
   
   * [single sign-on (SSO) 토큰을 요청] hello API 관리 REST API를 통해
   * returnUrl 쿼리 매개 변수 toohello 위의 hello API 호출 로부터 받은 SSO URL을 추가 합니다.
     
     > 예: https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url 
     > 
     > 
   * 리디렉션 hello 사용자 toohello 위의 URL 생성

또한 toohello에서 **SignIn** 작업을 수행할 수도 있습니다 계정 관리 hello 이전 단계를 수행 하 고 작업을 수행 하는 hello 중 하나를 사용 하 여 합니다.

* **ChangePassword**
* **ChangeProfile**
* **CloseAccount**

계정 관리 작업에 대 한 쿼리 매개 변수 뒤 hello를 통과 해야 합니다.

* **operation**: 위임 요청의 유형을 식별합니다(ChangePassword, ChangeProfile 또는 CloseAccount).
* **userId**: hello 계정 toomanage의 hello 사용자 id
* **salt**: 보안 해시를 계산하는 데 사용되는 특수 salt 문자열입니다.
* **sig**: 비교 tooyour 자체에 사용 되는 계산 된 보안 해시 toobe 계산 된 해시

## <a name="delegate-product-subscription"> </a>제품 구독 위임
제품 구독을 위임 toodelegating 사용자 로그인/접속 유사 하 게 작동 합니다. hello 최종 워크플로 다음과 같이 합니다.

1. 개발자는 hello API 관리 개발자 포털에서 제품을 선택 하 고 hello 가입 단추를 클릭
2. 브라우저는 리디렉션된 toohello 위임 끝점
3. 필요한 제품 구독 단계를 수행 하는 위임 끝점-tooyou 위로 이므로 리디렉션 tooanother 페이지 toorequest 결제 정보, 추가 질문 또는 단순히 hello 정보를 저장 하 고 사용자 개입을 필요로 하지 않는 수반 될 수 있습니다.

hello에 tooenable hello 기능 **위임** 페이지 **제품 구독을 위임**합니다.

그런 다음 hello 위임 끝점 hello 다음 작업을 수행 해야 합니다.

1. 요청 hello 다음 폼에에서 나타납니다.
   
   > *{작업이} http://www.yourwebsite.com/apimdelegation?operation= & productId = {에 제품 toosubscribe} & userId = {사용자 요청을 만드는} 솔트 & = {string} & sig = {string}*
   > 
   > 
   
    Hello 제품 구독 사례에 대 한 쿼리 매개 변수:
   
   * **operation**: 위임 요청 유형을 식별합니다. 제품 구독에 대 한 요청 hello 유효한 옵션은:
     * "구독": 인 제품을 지정 된 요청 toosubscribe hello 사용자 tooa 제공 ID (아래 참조)
     * "구독을 취소할": 요청 toounsubscribe 제품에서 사용자
     * "갱신": 요청이 toorenew 하는 구독 (예: 만료 될 수)
   * **productId**: hello 제품 hello 사용자의 hello ID 요청에 toosubscribe
   * **userId**: hello에 hello 요청이 hello 사용자의 ID
   * **salt**: 보안 해시를 계산하는 데 사용되는 특수 salt 문자열입니다.
   * **sig**: 비교 tooyour 자체에 사용 되는 계산 된 보안 해시 toobe 계산 된 해시
2. 해당 hello 요청이 (선택 사항 이지만 보안에 대 한 권장 사항임) Azure API 관리에서 오는지 확인 합니다.
   
   * Hello를 기반으로 문자열의 HMAC SHA512 계산 **productId**, **userId** 및 **솔트** 쿼리 매개 변수:
     
     > HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)
     > 
     > 
   * Hello의 hello 위에서 계산 된 해시 toohello 값 비교 **sig** 쿼리 매개 변수입니다. Hello 두 해시가 일치 하는 경우 toohello 다음 단계에서 이동, 그렇지 않으면 hello 요청을 거부 합니다.
3. 요청 된 작업의 hello 형식을 기반으로 제품 구독 처리를 수행 **작업** -질문 등 추가 예: 대금 청구, 합니다.
4. 편이 hello 사용자 toohello 제품, 구독에 가입 하 여 hello 사용자 toohello API 관리 제품 [제품 구독에 대 한 REST API 호출 hello]합니다.

## <a name="delegate-example-code"> </a> 예제 코드
샘플 표시 방식을 코드 이러한 tootake hello *위임 유효성 검사 키*, hello 게시자 포털의 hello 위임 화면에 설정 된,이 HMAC toocreate toovalidate hello 서명, hello의 hello 유효성을 증명 사용 전달 된 returnUrl 합니다. hello hello productId 및 약간의 수정 하지 않고도 사용자 Id에 대 한 동일한 코드가 작동 합니다.

**ReturnUrl의 C# 코드 toogenerate 해시**

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature toosig query parameter
}
```

**ReturnUrl의 NodeJS 코드 toogenerate 해시**

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature toosig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a>다음 단계
위임에 대 한 자세한 내용은 hello 다음 비디오를 참조 하세요.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
[single sign-on (SSO) 토큰을 요청]: http://go.microsoft.com/fwlink/?LinkId=507409
[사용자를 만듭니다]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser
[제품 구독에 대 한 REST API 호출 hello]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO
[Next steps]: #next-steps
[아래에 제공 된 예제 코드]: #delegate-example-code

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 
