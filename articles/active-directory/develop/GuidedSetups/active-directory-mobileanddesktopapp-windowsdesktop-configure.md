---
title: "AD aaaAzure v2 Windows 데스크톱 시작-Config | Microsoft Docs"
description: "Windows Desktop .NET(XAML) 응용 프로그램이 액세스 토큰을 얻고 Azure Active Directory v2 끝점으로 보호되는 API를 호출하는 방식 | Microsoft Azure | Microsoft Azure"
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
ms.openlocfilehash: 39c257e3e0cb09491f6fe005877601bd46824d12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>응용 프로그램(Express) 만들기
이제 tooregister hello에서 응용 프로그램 필요한 *Microsoft 응용 프로그램 등록 포털*:
1. Hello 통해 응용 프로그램 등록 [Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)
2.  응용 프로그램 이름과 메일을 입력합니다.
3.  설치 문제 해결에 대 한 hello 옵션을 선택 했는지 확인
4.  Hello 지침 tooobtain hello 응용 프로그램 ID를 따르고 코드에 붙여

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>추가 응용 프로그램 등록 정보 tooyour 솔루션 (고급)
이제 tooregister hello에서 응용 프로그램 필요한 *Microsoft 응용 프로그램 등록 포털*:
1. Toohello 이동 [Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com/portal/register-app) tooregister 응용 프로그램
2. 응용 프로그램 이름과 메일을 입력합니다. 
3. 설치 문제 해결에 대 한 hello 옵션을 선택 하지 않았는지 확인
4. `Add Platform`를 클릭한 다음 `Native Application`을 선택하고 [저장]을 누릅니다.
5. 응용 프로그램 ID에 hello GUID를 복사, tooVisual Studio에서 열기 돌아가서 `App.xaml.cs` 바꾸고 `your_client_id_here` hello 방금 등록 한 응용 프로그램 ID로:

```csharp
private static string ClientId = "your_application_id_here";
```
