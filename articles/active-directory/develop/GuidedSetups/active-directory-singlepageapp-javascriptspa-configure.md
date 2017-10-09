---
title: "aaaAzure AD v2 JS SPA 단계별 설치-구성 | Microsoft Docs"
description: "JavaScript SPA 응용 프로그램이 Azure Active Directory v2 끝점으로 보호되는 액세스 토큰을 필요로 하는 API를 호출하는 방식"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 1b93298d4bd4e17dd261dbb75502a122c30aac97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="register-your-application"></a>응용 프로그램 등록

여러 방법으로 toocreate 응용 프로그램, 그 중 하나를 선택 하십시오.

### <a name="option-1-register-your-application-express-mode"></a>옵션 1: 응용 프로그램 등록(기본 모드)
이제 tooregister hello에서 응용 프로그램 필요한 *Microsoft 응용 프로그램 등록 포털*:

1.  Hello 통해 응용 프로그램 등록 [Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)
2.  응용 프로그램 이름과 메일을 입력합니다.
3.  있는지 hello 옵션에 대 한 확인 *단계별 설치* 확인
4.  Hello 지침 tooobtain hello 응용 프로그램 ID를 따르고 코드에 붙여

### <a name="option-2-register-your-application-advanced-mode"></a>옵션 2: 응용 프로그램 등록(고급 모드)

1. Toohello 이동 [Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com/portal/register-app) tooregister 응용 프로그램
2. 응용 프로그램 이름과 메일을 입력합니다. 
3. 있는지 hello 옵션에 대 한 확인 *단계별 설치* 선택 하지 않으면
4.  `Add Platform`를 클릭한 다음 `Web`을 선택합니다.
5. Hello 추가 `Redirect URL` 해당 하는 웹 서버에 따라 toohello 응용 프로그램의 URL입니다. 방법에 대 한 지침은 아래 hello 섹션을 참조 하십시오. tooset / Visual Studio 및 Python에서 hello 리디렉션 URL을 검색 합니다.
6. 페이지 맨 아래에 있는 *저장*

> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a>리디렉션 URL을 얻기 위한 Visual Studio 지침
> Hello 지침 tooobtain 리디렉션 URL을 수행 합니다.
> 1.    *솔루션 탐색기*hello 프로젝트를 선택 하 고 hello를 살펴보고 `Properties` 창 (키를 눌러 속성 창을 보이지 않으면 `F4`)
> 2.    Hello 값에서 복사 `URL` toohello 클립보드:<br/> ![](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)<br />
> 3.    뒤로 toohello 전환 *응용 프로그램 등록 포털* hello 값으로 붙여는 `Redirect URL` '저장'를 클릭 합니다.

<p/>

> #### <a name="setting-redirect-url-for-python"></a>Python에 대한 리디렉션 URL 설정
> Python에 대 한 명령줄을 통해 hello 웹 서버 포트를 설정할 수 있습니다. 참조에 대 한 hello 포트 8080을 사용 하는이 단계별된 설치 하지만 사용 가능한 다른 포트 무료 toouse 느껴집니다. 어떤 경우 든, 아래 지침을 hello tooset hello 응용 프로그램 등록 정보에 리디렉션 URL 구성 합니다.<br/>
> - 뒤로 toohello 전환 *응용 프로그램 등록 포털* 설정 `http://localhost:8080/` 로 `Redirect URL`, 사용 또는 `http://localhost:[port]/` 사용자 지정 TCP 포트를 사용 하는 경우 (여기서 *[port]* 는 hello 사용자 지정 하는 TCP 포트 번호) '저장'를 클릭 합니다.


#### <a name="configure-your-javascript-spa"></a>JavaScript SPA 구성

1.  라는 파일을 만들어 `msalconfig.js` hello 응용 프로그램 등록 정보를 포함 합니다. Visual Studio, 선택 hello 프로젝트 (프로젝트 루트 폴더)를 사용 하는 인덱스를 마우스 오른쪽 단추로 클릭 하 고 선택: `Add`  >  `New Item`  >  `JavaScript File`합니다. 이름을 `msalconfig.js`로 지정합니다.
2.  다음 코드 tooyour hello 추가 `msalconfig.js` 파일:

```javascript
var msalconfig = {
    clientID: "Enter_the_Application_Id_here",
    redirectUri: location.origin
};
```
<ol start="3">
<li>
대체 <code>Enter_the_Application_Id_here</code> hello 방금 등록 한 응용 프로그램 Id로
</li>
</ol>
