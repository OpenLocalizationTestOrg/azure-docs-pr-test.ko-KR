---
title: "AD aaaAzure.NET 프로토콜 개요 | Microsoft Docs"
description: "어떻게 toouse HTTP 메시지 tooauthorize tooweb 응용 프로그램 및 Azure AD를 사용 하 여 테 넌 트의 웹 Api에 액세스 합니다."
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/21/2016
ms.author: priyamo
ms.openlocfilehash: 5bd54af028c445afd3f35d67d47d7c84b476c757
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## AD 테넌트에 응용 프로그램 등록
먼저 tooregister 응용 프로그램이 Azure Active Directory (Azure AD) 테 넌 트와 합니다. 이 응용 프로그램에 대 한 응용 프로그램 ID를 제공 뿐만 tooreceive 토큰을 사용 합니다.

* Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
* Hello hello 페이지의 맨 위 오른쪽 모서리에 있는 사용자 계정을 클릭 하 여 Azure AD 테 넌 트를 선택 합니다.
* Hello 왼쪽 탐색 창에서 클릭 **Azure Active Directory**합니다.
* **앱 등록**을 클릭하고 **추가**를 클릭합니다.
* Hello 화면에 따라 수행 하 고 새 응용 프로그램을 만듭니다. 이 자습서에서는 웹 응용 프로그램이든지 네이티브 응용 프로그램이든지 상관 없지만 웹 응용 프로그램 또는 네이티브 응용 프로그램에 대한 특정 예제가 필요한 경우 [빠른 시작](../articles/active-directory/develop/active-directory-developers-guide.md)을 확인하세요.
  * 웹 응용 프로그램에서는 hello 제공 **로그온 URL** hello 응용 프로그램의 기준 URL을 설정 하는 예: 사용자가 로그인이 변수인 `http://localhost:12345`합니다.
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * 네이티브 응용 프로그램에 대 한 제공는 **리디렉션 URI**, Azure AD는 tooreturn 토큰 응답을 사용 합니다. 값 특정 tooyour 응용 프로그램을 입력 합니다. 예:`http://MyFirstAADApp`
* Azure AD 응용 프로그램을 고유한 클라이언트 식별자 할당 되 면 응용 프로그램 id. hello 등록을 마친 후 이 값이 필요 합니다 hello 다음 섹션의 하므로에서 복사 hello 응용 프로그램 페이지.
