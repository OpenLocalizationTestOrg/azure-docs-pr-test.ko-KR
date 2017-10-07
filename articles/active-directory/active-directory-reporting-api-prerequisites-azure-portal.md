---
title: "aaaPrerequisites tooaccess hello Azure AD 보고 API | Microsoft Docs"
description: "Hello 필수 구성 요소 tooaccess hello Azure AD 보고 API에 대 한 자세한 내용은"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: ec28a7530f341dda31268a978754b615c727d66f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a>필수 구성 요소 tooaccess hello Azure AD 보고 API

hello [Azure AD reporting Api](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) REST 기반 Api 집합을 통해 toohello 데이터에 프로그래밍 방식 액세스를 제공 합니다. 다양한 프로그래밍 언어 및 도구에서 이러한 API를 호출할 수 있습니다.

API가 사용을 보고 하는 hello [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize toohello web Api에 액세스 합니다. 

tooget hello API를 통해 toohello 보고 데이터에 액세스, toohave hello 할당 된 역할을 다음 중 하나가 필요 합니다.

- 보안 판독기
- 보안 관리자
- 전역 관리자


tooprepare 보고 API 사용자 액세스 toohello를 수행 해야 합니다.

1. 응용 프로그램 등록 
2. 권한 부여 
3. 구성 설정 수집 

질문, 문제 또는 피드백은 [지원 티켓을 파일로 저장하세요](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).

## <a name="register-an-azure-active-directory-application"></a>Azure Active Directory 응용 프로그램 등록

Hello 보고 스크립트를 사용 하는 API에 액세스 하는 경우에 앱 tooregister를 해야 합니다. 이렇게 하면는 **응용 프로그램 ID**, 권한 부여 호출에 대 한 필요한 및 코드 tooreceive 토큰 수 있습니다.

tooconfigure 디렉터리 tooaccess hello Azure AD 보고 API에 로그인 해야 toohello hello의 구성원 이기도 Azure 관리자 계정으로 Azure 포털 **전역 관리자** Azure AD 테 넌 트의 디렉터리 역할 .

> [!IMPORTANT]
> 다음과 같이 "admin" 권한이 있는 자격 증명으로 실행 중인 응용 프로그램은 매우 강력 할 수 하므로 보안 있는지 tookeep hello 응용 프로그램의 ID/암호 자격 증명 해야 합니다.
> 


**tooregister Azure Active Directory 응용 프로그램:**

1. Hello에 [Azure 포털](https://portal.azure.com), 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. Hello에 **Azure Active Directory** 블레이드에서 클릭 **앱 등록**합니다.

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/02.png) 

3. Hello에 **앱 등록** 블레이드 hello 바탕 화면에서 hello 도구 모음에서 클릭 **새 응용 프로그램 등록**합니다.

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/03.png)

4. Hello에 **만들기** 블레이드에서 hello 다음 단계를 수행 합니다.

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/04.png)

    a. Hello에 **이름** 텍스트 상자에 `Reporting API application`합니다.

    b. **응용 프로그램 형식**으로 **웹앱/API**를 선택합니다.

    c. Hello에 **로그온 URL** 텍스트 상자에 `https://localhost`합니다.

    d. **만들기**를 클릭합니다. 


## <a name="grant-permissions"></a>권한 부여 

이 단계의 목표 hello toogrant 응용 프로그램은 **디렉터리 데이터 읽기** 권한 toohello **Windows Azure Active Directory** API입니다.

![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/16.png)
 

**toogrant 응용 프로그램 권한 toouse hello API:**

1. Hello에 **앱 등록** 블레이드 hello 앱 목록에서 클릭 **Reporting API 응용 프로그램**합니다.

2. Hello에 **Reporting API 응용 프로그램** 블레이드 hello 바탕 화면에서 hello 도구 모음에서 클릭 **설정을**합니다. 

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

3. Hello에 **설정** 블레이드에서 클릭 **필요한 권한**합니다. 

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/06.png)

4. Hello에 **필요한 권한** 블레이드 hello **API** 목록에서 클릭 **Windows Azure Active Directory**합니다. 

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/07.png)

5. Hello에 **액세스 가능** 블레이드를 **디렉터리 데이터 읽기**합니다. 

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/08.png)

6. 도구 모음의 hello hello 위쪽에 클릭 **저장**합니다.

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/15.png)

## <a name="gather-configuration-settings"></a>구성 설정 수집 
이 섹션에서는 디렉터리에서 설정을 다음 tooget hello:

* 도메인 이름
* 클라이언트 ID
* 클라이언트 암호

호출 toohello 보고 API를 구성할 때 이러한 값이 있어야 합니다. 

### <a name="get-your-domain-name"></a>도메인 이름 가져오기

**tooget 도메인 이름:**

1. Hello에 [Azure 포털](https://portal.azure.com), 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. Hello에 **Azure Active Directory** 블레이드에서 클릭 **도메인 이름**합니다.

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/09.png) 

3. Hello 도메인 목록에서 도메인 이름을 복사 합니다.


### <a name="get-your-applications-client-id"></a>응용 프로그램의 클라이언트 ID 가져오기

**tooget 응용 프로그램의 클라이언트 ID:**

1. Hello에 [Azure 포털](https://portal.azure.com), 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. Hello에 **앱 등록** 블레이드 hello 앱 목록에서 클릭 **Reporting API 응용 프로그램**합니다.

3. Hello에 **Reporting API 응용 프로그램** hello에 블레이드 **응용 프로그램 ID**, 클릭 **toocopy 클릭**합니다.

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/11.png) 



### <a name="get-your-applications-client-secret"></a>응용 프로그램의 클라이언트 비밀 가져오기
tooget 응용 프로그램의 클라이언트 비밀을 toocreate 새 키 및 해야 나중에 더 이상 가능한 tooretrieve 없기 때문에 hello 새 키를 저장할 때 해당 값이이 값을 저장 합니다.

**tooget 응용 프로그램의 클라이언트 암호:**

1. Hello에 [Azure 포털](https://portal.azure.com), 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. Hello에 **앱 등록** 블레이드 hello 앱 목록에서 클릭 **Reporting API 응용 프로그램**합니다.


3. Hello에 **Reporting API 응용 프로그램** 블레이드 hello 바탕 화면에서 hello 도구 모음에서 클릭 **설정을**합니다. 

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

4. Hello에 **설정** 블레이드 hello **APIR 액세스** 섹션에서 클릭 **키**합니다. 

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/12.png)


5. Hello에 **키** 블레이드에서 hello 다음 단계를 수행 합니다.

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/14.png)

    a. Hello에 **설명** 텍스트 상자에 `Reporting API`합니다.

    b. **만료**로 **In 2 years**(2년)를 선택합니다.

    c. **Save**를 클릭합니다.

    d. Hello 키 값을 복사 합니다.


## <a name="next-steps"></a>다음 단계
* API는 프로그래밍 방식으로 보고는 tooaccess hello hello Azure AD의에서 데이터와 같은 있습니다? 체크 아웃 [hello Azure Active Directory 보고 API 시작](active-directory-reporting-api-getting-started.md)합니다.
* Azure Active Directory 보고에 대 한 자세한 내용을 toofind 싶으시면 참조 hello [Azure Active Directory Reporting 가이드](active-directory-reporting-guide.md)합니다.  

