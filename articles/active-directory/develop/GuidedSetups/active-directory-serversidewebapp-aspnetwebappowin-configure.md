---
title: "AD aaaAzure v2 ASP.NET 웹 서버 시작-Config | Microsoft Docs"
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
ms.openlocfilehash: e666be4622ad30aaa1e12e49ae56bbe1e129b2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>응용 프로그램(Express) 만들기
이제 tooregister hello에서 응용 프로그램 필요한 *Microsoft 응용 프로그램 등록 포털*:
1. Hello 통해 응용 프로그램 등록 [Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)
2.  응용 프로그램 이름과 메일을 입력합니다.
3.  설치 문제 해결에 대 한 hello 옵션을 선택 했는지 확인
4.  Hello 지침 tooadd 리디렉션 URL tooyour 응용 프로그램에 따라

## <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>추가 응용 프로그램 등록 정보 tooyour 솔루션 (고급)
이제 tooregister hello에서 응용 프로그램 필요한 *Microsoft 응용 프로그램 등록 포털*:
1. Toohello 이동 [Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com/portal/register-app) tooregister 응용 프로그램
2. 응용 프로그램 이름과 메일을 입력합니다. 
3.  설치 문제 해결에 대 한 hello 옵션을 선택 하지 않았는지 확인
4.  `Add Platform`를 클릭한 다음 `Web`을 선택합니다.
5.  Studio tooVisual 돌아가서, 솔루션 탐색기에서 선택 hello 프로젝트 하 고 (보이지 않는 경우 속성 창, F4 키를 눌러) hello 속성 창을 확인합니다
6.  SSL 설정도 변경`True`
7.  Hello SSL URL을 복사 하 고이 URL toohello 목록 리디렉션 Url의 리디렉션 Url의 hello 등록 포털 목록에 추가 합니다.<br/><br/>![프로젝트 속성](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
8.  Hello 다음에서 추가 `web.config` hello 섹션 아래의 hello 루트 폴더에 있는 `configuration\appSettings`:

```xml
<add key="ClientId" value="Enter_the_Application_Id_here" />
<add key="redirectUri" value="Enter_the_Redirect_URL_here" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
<!-- Workaround for Docs conversion bug -->
<ol start="9">
<li>
대체 `ClientId` hello 방금 등록 한 응용 프로그램 Id로
</li>
<li>
대체 `redirectUri` hello 프로젝트의 SSL URL로
</li>
</ol>
<!-- End Docs -->
