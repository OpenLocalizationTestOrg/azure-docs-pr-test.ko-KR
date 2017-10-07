---
title: "aaaPrerequisites tooaccess hello Azure AD 보고 API입니다. | Microsoft Docs"
description: "Hello 필수 구성 요소 tooaccess hello Azure AD 보고 API에 대 한 자세한 내용은"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: e9d7ceaedb07d18fbd75b70d68b5cfbebc756c36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a>필수 구성 요소 tooaccess hello Azure AD 보고 API
hello [Azure AD reporting Api](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) REST 기반 Api 집합을 통해 toohello 데이터에 프로그래밍 방식 액세스를 제공 합니다. 다양한 프로그래밍 언어 및 도구에서 이러한 API를 호출할 수 있습니다.

API가 사용을 보고 하는 hello [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize toohello web Api에 액세스 합니다. 

tooprepare 보고 API 사용자 액세스 toohello를 수행 해야 합니다.

1. Azure AD 테넌트에서 응용 프로그램 만들기 
2. Grant hello 응용 프로그램 적절 한 사용 권한을 tooaccess hello Azure AD 데이터
3. 디렉터리에서 구성 설정 수집

질문, 문제 또는 피드백은 [AAD Reporting 도움말](mailto:aadreportinghelp@microsoft.com)에 문의하세요.

## <a name="create-an-azure-ad-application"></a>Azure AD 응용 프로그램 만들기
tooconfigure 디렉터리 tooaccess hello Azure AD 보고 API에 로그인 해야 toohello hello Azure AD 테 넌 트 전역 관리자 디렉터리 역할의 멤버 이기도 있는 Azure 구독 관리자 계정으로 Azure 클래식 포털입니다.

> [!IMPORTANT]
> 다음과 같이 "admin" 권한이 있는 자격 증명으로 실행 중인 응용 프로그램은 매우 강력 할 수 하므로 보안 있는지 tookeep hello 응용 프로그램의 ID/암호 자격 증명 해야 합니다.
> 
> 

1. Hello에 [Azure 클래식 포털](https://manage.windowsazure.com), 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Hello에서 **active directory** 목록에서 디렉터리를 선택 합니다.
3. Hello 메뉴에서 hello 위에 표시를 클릭 **응용 프로그램**합니다.
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Hello 아래쪽 막대에서 클릭 **추가**합니다.
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/03.png) 
5. Hello에 **하 신 toodo 원하는?** 대화 상자에서 클릭 **조직에서 개발 중인 응용 프로그램 추가**합니다. 
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/04.png) 
6. Hello에 **응용 프로그램에 대해 알리기** 대화 상자에서 hello 다음 단계를 수행 합니다. 
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    a. Hello에 **이름** 텍스트 상자에 이름 (예:: Reporting API 응용 프로그램).
   
    b. **웹 응용 프로그램 및/또는 Web API**를 선택합니다.
   
    c. **다음**을 누릅니다.
7. Hello에 **앱 속성** 대화 상자에서 hello 다음 단계를 수행 합니다. 
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    a. Hello에 **로그온 URL** 텍스트 상자에 `https://localhost`합니다.
   
    b. Hello에 **앱 ID URI** 텍스트 상자에 ```https://localhost/ReportingApiApp```합니다.
   
    c. 페이지 맨 아래에 있는 **완료**을 참조하세요.

## <a name="grant-your-application-permission-toouse-hello-api"></a>응용 프로그램 권한 toouse hello API를 부여 합니다.
1. Hello에 [Azure 클래식 포털](https://manage.windowsazure.com/), 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Hello에서 **active directory** 목록에서 디렉터리를 선택 합니다.
3. Hello 메뉴에서 hello 위에 표시를 클릭 **응용 프로그램**합니다.
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/02.png)
4. Hello 응용 프로그램 목록에서 새로 만든된 응용 프로그램을 선택 합니다.
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/07.png)
5. Hello 메뉴에서 hello 위에 표시를 클릭 **구성**합니다.
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/08.png)
6. Hello에 **tooother 응용 프로그램 사용 권한** hello에 대 한 섹션 **Azure Active Directory** 리소스를 hello 클릭 **응용 프로그램 사용 권한** 드롭 다운 목록 및 선택 **디렉터리 데이터 읽기**합니다.
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/09.png)
7. Hello 아래쪽 막대에서 클릭 **저장**합니다.
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a>디렉터리에서 구성 설정 수집
이 섹션에서는 디렉터리에서 설정을 다음 tooget hello:

* 도메인 이름
* 클라이언트 ID
* 클라이언트 암호

호출 toohello 보고 API를 구성할 때 이러한 값이 있어야 합니다. 

### <a name="get-your-domain-name"></a>도메인 이름 가져오기
1. Hello에 [Azure 클래식 포털](https://manage.windowsazure.com), 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Hello에서 **active directory** 목록에서 디렉터리를 선택 합니다.
3. Hello 메뉴에서 hello 위에 표시를 클릭 **도메인**합니다.
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/11.png) 
4. Hello에 **도메인 이름** 열에서 도메인 이름을 복사 합니다.
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-hello-applications-client-id"></a>Hello 응용 프로그램의 클라이언트 ID 가져오기
1. Hello에 [Azure 클래식 포털](https://manage.windowsazure.com), 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Hello에서 **active directory** 목록에서 디렉터리를 선택 합니다.
3. Hello 메뉴에서 hello 위에 표시를 클릭 **응용 프로그램**합니다.
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Hello 응용 프로그램 목록에서 새로 만든된 응용 프로그램을 선택 합니다.
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/07.png)
5. Hello 메뉴에서 hello 위에 표시를 클릭 **구성**합니다.
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/08.png)
6. **클라이언트 ID**를 복사합니다.
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-hello-applications-client-secret"></a>Hello 응용 프로그램 클라이언트 암호를 받을
tooget 응용 프로그램의 클라이언트 비밀을 toocreate 새 키 및 해야 나중에 더 이상 가능한 tooretrieve 없기 때문에 hello 새 키를 저장할 때 해당 값이이 값을 저장 합니다.

1. Hello에 [Azure 클래식 포털](https://manage.windowsazure.com), 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Hello에서 **active directory** 목록에서 디렉터리를 선택 합니다.
3. Hello 메뉴에서 hello 위에 표시를 클릭 **응용 프로그램**합니다.
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Hello 응용 프로그램 목록에서 새로 만든된 응용 프로그램을 선택 합니다.
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/07.png)
5. Hello 메뉴에서 hello 위에 표시를 클릭 **구성**합니다.
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/08.png)
6. Hello에 **키** 섹션를 hello 다음 단계를 수행 합니다. 
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/14.png)
   
    a. Hello 기간 목록에서 기간을 선택
   
    b. Hello 아래쪽 막대에서 클릭 **저장**합니다.
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/10.png)
   
    c. Hello 키 값을 복사 합니다.

## <a name="next-steps"></a>다음 단계
* API는 프로그래밍 방식으로 보고는 tooaccess hello hello Azure AD의에서 데이터와 같은 있습니다? 체크 아웃 [hello Azure Active Directory 보고 API 시작](active-directory-reporting-api-getting-started.md)합니다.
* Azure Active Directory 보고에 대 한 자세한 내용을 toofind 싶으시면 참조 hello [Azure Active Directory Reporting 가이드](active-directory-reporting-guide.md)합니다.  

