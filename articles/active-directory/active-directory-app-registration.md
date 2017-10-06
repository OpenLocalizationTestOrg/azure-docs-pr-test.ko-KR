---
title: "Active Directory 응용 프로그램 등록 aaaAzure | Microsoft Docs"
description: "이 문서에서 설명 하는 방법을 toouse hello Azure 포털 tooregister Azure Active Directory와 응용 프로그램"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 7dc7b89f-653f-405a-b5f4-2c1288720c15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: priyamo
ms.reviewer: elisol
ms.openlocfilehash: 0134e299dcc53919a6f789a0878a1cf64a8e244d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="register-your-application-with-your-azure-active-directory-tenant"></a>Azure Active Directory 테넌트로 응용 프로그램 등록

Azure Active Directory (Azure AD) 테 넌 트와 Azure 포털 tooregister hello 응용 프로그램을 사용할 수 있습니다. Hello 응용 프로그램에 대 한 응용 프로그램 ID 만들고 tooreceive 토큰 수 있도록 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello hello 페이지의 맨 위 오른쪽 모서리에서 사용자 계정을 선택 하 여 Azure AD 테 넌 트를 선택 합니다.
3. Hello 왼쪽의 탐색 창에서 선택 **더 서비스**, 클릭 **앱 등록**를 클릭 하 고 **추가**합니다.
4. Hello 화면에 따라 수행 하 고 새 응용 프로그램을 만듭니다. 웹 응용 프로그램 또는 네이티브 응용 프로그램에 대한 구체적인 예제를 원하는 경우 [빠른 시작](active-directory-developers-guide.md)을 확인합니다.
  * 웹 응용 프로그램에서는 hello 제공 **로그온 URL**, hello 응용 프로그램의 기준 URL을 설정 하는 예: 사용자가 로그인이 변수인 `http://localhost:12345`합니다.
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * 네이티브 응용 프로그램에 제공 된 **리디렉션 URI**, tooreturn 토큰 응답을 사용 하 여 Azure AD는 합니다. 값 특정 tooyour 응용 프로그램을 입력 합니다. 예:`http://MyFirstAADApp`
5. Azure AD 할당 hello 응용 프로그램 id입니다. 고유한 클라이언트 식별자, 응용 프로그램 등록을 마친 후

## <a name="update-application-settings-from-hello-azure-portal"></a>Hello Azure 포털에서에서 응용 프로그램 설정 업데이트

Azure 포털 hello를 사용 하 여 기존 응용 프로그램의 설정을 쉽게 수정할 수 있습니다. 예를 들어 좋습니다 tooconfigure Azure AD 토큰 응답을 발급 하는 회신 URL. Tooconfigure 권한 tooother 응용 프로그램을 할 수 있습니다, 인스턴스 tooallow에 대 한 응용 프로그램 tooaccess hello Microsoft Graph API입니다. 이 모든 hello 응용 프로그램 설정 페이지를 통해 수행할 수 있습니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello hello 페이지의 맨 위 오른쪽 모서리에서 사용자 계정을 선택 하 여 Azure AD 테 넌 트를 선택 합니다.
3. Hello 왼쪽의 탐색 창에서 선택 **더 서비스**, 클릭 **앱 등록**, hello 목록에서 응용 프로그램을 선택 합니다.
4. 클릭 **설정을** tooopen hello 응용 프로그램에 대 한 hello 설정 페이지를 구성 합니다.
  * hello **속성** 페이지 hello hello 응용 프로그램에 대 한 일반 정보를 수정할 수 있습니다. Hello 응용 프로그램 이름, hello 로그온 URL 및 hello 로그 아웃 URL이 포함 됩니다.
  * hello **회신 Url** 페이지에서는 Azure AD 토큰 응답을 전송 하는 위치는 회신 URL을 tooadd 있습니다.
  * hello **소유자** 페이지에서는 tooadd 응용 프로그램 소유자가 있습니다.
  * hello **권한을** 페이지에서는 hello 앱에 대 한 권한을 tooconfigure 있습니다. 예를 들어 tooaccess hello Microsoft Graph API를 클릭 하 여 **추가** 선택 **Microsoft Graph** hello API 선택기에서 hello 권한이 필요한 경우 예를 들어 다음 선택 **디렉터리 데이터 읽기 **.
  * hello **키** 페이지에서는 tooadd 응용 프로그램 암호입니다. hello 비밀만 표시 한 번를 만든 후 즉시 있는지 toocopy를 수 있으므로 더 이상 사용 하기 위해.

## <a name="use-hello-inline-manifest-editor"></a>Hello 인라인 매니페스트 편집기를 사용 하 여

Hello 인라인 매니페스트 편집기 toomodify 특정 응용 프로그램 속성에 직접 노출 되지 않는 hello Azure 포털을 사용할 수 있습니다. 예를 들어 toomodify hello 응용 프로그램의 앱 ID URI를 사용할 수 있습니다 또는 tooenable hello oauth 2.0 암시적 흐름 대신 hello 기본 권한 부여 코드 흐름을 부여 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello hello 페이지의 맨 위 오른쪽 모서리에서 사용자 계정을 선택 하 여 Azure AD 테 넌 트를 선택 합니다.
3. Hello 왼쪽의 탐색 창에서 선택 **더 서비스**, 클릭 **앱 등록**, hello 목록에서 응용 프로그램을 선택 합니다.
4. 클릭 **매니페스트** hello 응용 프로그램 페이지 tooopen hello 인라인 매니페스트 편집기에서.
5. 변경 내용을 toohello 매니페스트 하 고 싶다면 저장 직접 만들 수 있습니다. 또는 hello 매니페스트 tooopen를 다운로드할 수 있습니다 프로그램 즐겨 찾는 편집기 및 업로드 hello에서 매니페스트를 업데이트 합니다.

## <a name="next-steps"></a>다음 단계

1. 체크 아웃 hello [퀵 스타트](active-directory-developers-guide.md) Azure AD를 사용 하 여 인증을 수행 하는 응용 프로그램의 자세한 연습에 대 한 합니다.
2. [GitHub](https://github.com/azure-samples)에서 코드 샘플에 대한 전체 목록을 확인합니다.
