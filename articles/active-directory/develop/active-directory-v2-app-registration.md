---
title: "aaaRegister hello 포털을 사용 하 여 Azure AD hello v2.0 끝점으로 응용 프로그램 | Microsoft Docs"
description: "Hello v2.0 끝점을 사용 하 여 tooregister Microsoft에서 로그인을 사용 하도록 설정 하 고 Microsoft에 액세스를 사용 하 여 앱을 서비스 하는 방법"
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: 
ms.assetid: bb2f701f-3bc3-4759-94a5-8b9d53a8a0b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: lenalepa
ms.custom: aaddev
ms.openlocfilehash: c56c98906656062435516e820cb318a04c03149c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooregister-an-app-with-hello-v20-endpoint"></a>어떻게 tooregister hello v2.0 끝점을 사용 하 여 앱
toobuild MSA 및 Azure AD를 모두 허용 하는 응용 프로그램 로그인을 처음 해야 tooregister Microsoft와 응용 프로그램입니다.  지금은 없습니다 수 toouse Azure AD와 모든 기존 앱 수 또는 MSA-toocreate 브랜드 새 필요 합니다.

> [!NOTE]
> 모든 Azure Active Directory 시나리오 및 기능 hello v2.0 끝점에서 사용할 수 있습니다.  에 대해 알아보세요 hello v2.0 끝점을 사용 해야 하는 경우 toodetermine [v2.0 제한](active-directory-v2-limitations.md)합니다.
> 
> 

## <a name="visit-hello-microsoft-app-registration-portal"></a>Hello Microsoft 응용 프로그램 등록 포털을 방문
중요 한 정보는 처음-너무 이동[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)합니다.  이곳은 Microsoft 앱을 관리할 수 있는 새로운 앱 등록 포털입니다.

개인, 직장 또는 학교 Microsoft 계정 중 하나로 로그인 합니다.  계정이 하나라도 없다면, 새로운 개인 계정을 등록합니다. 그렇게 오래 걸리지 않으니 등록하세요 - 기다리겠습니다.

등록했나요? 아마도 비어있을 Microsoft 앱의 목록을 보고 있을 것입니다.  변경을 시작해봅시다.

**앱 추가**를 클릭하여 이름을 지정합니다.  hello 포털 앱 코드에서 사용할는 전역적으로 고유한 응용 프로그램 Id를 할당 합니다.  Api 호출에 대 한 액세스 토큰 해야 하는 응용 프로그램 서버 측 구성 요소를 포함 하는 경우 (생각: Office, Azure 또는 고유한 web API)를 toocreate 합니다는 **응용 프로그램 암호** 여기에도 합니다.

Hello 플랫폼 앱에서 사용할 다음을 추가 합니다.

* 웹 기반 앱의 경우 로그인 메시지를 보낼 수 있는 **리디렉션 URI** 를 제공합니다.
* 모바일 앱에 대 한 hello 기본 아래로 복사 리디렉션 자동으로 생성 하는 uri입니다.

필요에 따라 hello 프로필 섹션에서에서 로그인 페이지의 hello 모양과 느낌을 사용자 지정할 수 있습니다.  있는지 tooclick 확인 **저장** 넘어가기 전에 합니다.

> [!NOTE]
> 사용 하 여 응용 프로그램을 만들 때 [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), toosign hello 포털을 사용 하는 hello 계정의 hello 홈 테 넌 트에서 hello 응용 프로그램 등록 됩니다.  즉, 개인 Microsoft 계정을 사용하여 Azure AD 테넌트에 응용 프로그램을 등록할 수 없습니다.  명시적으로 원할 경우 tooregister 응용 프로그램 특정 테 넌 트에 해당 테 넌 트에서 만든 원래 계정으로 로그인 합니다.
> 
> 

## <a name="build-a-quick-start-app"></a>빠른 시작 앱 빌드하기
이제 Microsoft 앱을 가지고 있으므로 v2.0 빠른 시작 자습서 중 하나를 완료할 수 있습니다.  몇가지 권장 사항입니다.

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

