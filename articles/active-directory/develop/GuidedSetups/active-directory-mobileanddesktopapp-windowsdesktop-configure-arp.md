---
title: "AD aaaAzure v2 Windows 데스크톱 시작-Config | Microsoft Docs"
description: "Windows Desktop .NET(XAML) 응용 프로그램이 액세스 토큰을 얻고 Azure Active Directory v2 끝점으로 보호되는 API를 호출하는 방식"
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
ms.openlocfilehash: d96d9eded200824a6f7ee234009dd0bb11b18b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a>Hello 응용 프로그램의 등록 정보 tooyour 앱 추가
이 단계에서는 tooadd hello 응용 프로그램 Id tooyour 프로젝트가 필요합니다.

1.  열기 `App.xaml.cs` hello를 포함 하는 hello 줄 바꾸고 `ClientId` 사용:

```csharp
private static string ClientId = "[Enter hello application Id here]";
```

### <a name="what-is-next"></a>다음 내용

[테스트 및 유효성 검사](active-directory-mobileanddesktopapp-windowsdesktop-test.md)
