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
ms.openlocfilehash: badc47e131290a56a507592f944a0fc7093260a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="configure-your-aspnet-web-app-with-hello-applications-registration-information"></a>ASP.NET 웹 앱 hello 응용 프로그램의 등록 정보로 구성

이 단계에서는 프로그램 프로젝트 toouse SSL을 구성 하 고 hello SSL URL tooconfigure 응용 프로그램의 등록 정보를 사용 합니다. 그러면 hello 응용 프로그램을 추가 '를 통해 등록 정보 tooyour 솔루션 *web.config*합니다.

1.  솔루션 탐색기에서 hello 프로젝트를 선택 하 고 hello를 살펴보고 `Properties` 창 (F4 키를 눌러 속성 창을 표시 되지 않는) 하는 경우
2.  변경 `SSL Enabled` 너무`True`
3.  Hello 값에서 복사 `SSL URL` 위에 hello에 붙여 넣을 `Redirect URL` 필드 hello이이 페이지 위쪽에 클릭 *업데이트*:<br/><br/>![](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
4.  Hello 다음에서 추가 `web.config` 섹션에서 루트의 폴더에 있는 파일 `configuration\appSettings`:

```xml
<add key="ClientId" value="[Enter hello application Id here]" />
<add key="RedirectUri" value="[Enter hello Redirect URL here]" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
