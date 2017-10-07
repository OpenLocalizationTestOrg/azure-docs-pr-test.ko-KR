---
title: "AD aaaAzure v2 ASP.NET 웹 서버 시작-테스트 | Microsoft Docs"
description: "OpenID Connect 표준을 사용하여 기존 웹 브라우저 기반 응용 프로그램을 사용하는 ASP.NET 솔루션에서 Microsoft 로그인 구현"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 99c7525b9146605142180962fc2a61b3c953c064
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>코드 테스트

키를 눌러 `F5` toorun Visual Studio에서 프로젝트. hello 브라우저가 열리고 너무 데이터 웨어하우스가*http://localhost: {port}* hello를 볼 수 있는 *इ न क Microsoft* 단추입니다. 계속 해 toosign에서을 클릭 합니다.

준비 tootest를 사용 하 여 회사 또는 학교 (Azure Active Directory) 또는 개인 (live.com, outlook.com) 계정에 toosign 라인인 경우입니다. 

![Microsoft로 로그인 브라우저 창](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin.png)

![Microsoft로 로그인 브라우저 창](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin2.png)

#### <a name="expected-results"></a>예상 결과
로그인 한 후 hello 사용자는 hello hello Microsoft 응용 프로그램 등록 포털에서에서 응용 프로그램 등록 정보에 지정 된 HTTPS URL 인 웹 사이트의 리디렉션된 toohello 홈 페이지입니다. 이 페이지에 이제 표시 *Hello {User}* 는 링크 toosign 출력 및 링크 toohello Authorize 컨트롤러인 링크 toosee hello 사용자의 클레임 – 앞에서 만든 합니다.

### <a name="see-users-claims"></a>사용자의 클레임 보기
Hello 하이퍼링크 toosee hello 사용자 클레임을 선택 합니다. 이 안내 toohello 컨트롤러와 뷰를 사용할 수 있는 toousers 인증 된만 합니다.

#### <a name="expected-results"></a>예상 결과
 Hello hello 로그온 한 사용자의 기본 속성을 포함 하는 테이블을 표시 되어야 합니다.

| 속성 | 값 | 설명|
|---|---|---|
| 이름 | {User Full Name} | hello 사용자 ् य ा च े ं
|사용자 이름 | <span>user@domain.com</span>| tooidentify hello 로그온 한 사용자를 사용 하는 hello 사용자 이름
| 제목| {Subject}|문자열 toouniquely hello 웹 간에 hello 사용자 로그온 식별|
| 테넌트 ID| {Guid}| A *guid* toouniquely hello 사용자의 Azure Active Directory 조직을 나타냅니다.|

또한 인증 요청에 포함된 모든 사용자 클레임을 포함하는 표가 표시됩니다. 모든 클레임과 ID 토큰 및 설명 목록은 이 [문서](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "ID 토큰의 클레임 목록")을 참조하세요.


### <a name="test-accessing-a-method-that-has-an-authorize-attribute-optional"></a>*[Authorize]* 특성이 있는 메서드 액세스 테스트(선택 사항)
이 단계에서는 익명 사용자로 액세스 hello 인증 된 컨트롤러를 테스트 합니다.<br/>
Toosign 아웃 hello 사용자를 연결 하는 hello 및 전체 hello 로그 아웃 프로세스를 선택 합니다.<br/>
이제 브라우저에 http://localhost를 입력: {port} / tooaccess hello로 보호 되는 컨트롤러 인증 `[Authorize]` 특성

#### <a name="expected-results"></a>예상 결과
Tooauthenticate toosee hello 보기를 요구 하는 hello 프롬프트를 받아야 합니다.

## <a name="additional-information"></a>추가 정보

<!--start-collapse-->
### <a name="protect-your-entire-web-site"></a>전체 웹 사이트 보호
tooprotect 전체 웹 사이트 추가 hello `AuthorizeAttribute` 너무`GlobalFilters` 에 `Global.asax` `Application_Start` 메서드:

```csharp
GlobalFilters.Filters.Add(new AuthorizeAttribute());
```
<!--end-collapse-->

<div></div>
<br/>

> [!NOTE]
> **어떻게 toorestrict 하나만 조직 toosign tooyour 응용 프로그램에서 사용자가**

> 기본적으로 모든 회사 또는 조직에서 Azure Active Directory와 통합 하는 회사 및 학교 계정 뿐만 아니라 개인 계정 (포함 하 여 outlook.com, live.com, 등)에 로그인 tooyour 응용 프로그램입니다. 

> 사용자 응용 프로그램 tooaccept 로그인만 한 Azure Active Directory 조직에서 사용할 경우 교체 hello `Tenant` 매개 변수에서 *web.config* 에서 `Common` hello 조직의 – toohello 테 넌 트 이름 예제에서는 *contoso.onmicrosoft.com*합니다. 그 후 변경 hello `ValidateIssuer` 인수에 프로그램 *OWIN 시작 클래스* 너무`true`합니다.

> tooallow 사용자가 특정 조직과 목록만 설정 `ValidateIssuer` tootrue 및 사용 하 여 hello `ValidIssuers` 매개 변수 toospecify 조직 목록입니다.

> 또 다른 옵션은 사용자 지정 메서드 tooimplement toovalidate hello 발급자 IssuerValidator 매개 변수를 사용 하 여 합니다. `TokenValidationParameters`에 대한 자세한 내용은 [이](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters MSDN 문서") MSDN 문서를 참조하세요.

