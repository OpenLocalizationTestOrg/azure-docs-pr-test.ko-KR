---
title: "Azure AD 응용 프로그램 프록시를 사용 하 여 게시 된 앱에 대 한 사용자 지정 홈 페이지 aaaSet | Microsoft Docs"
description: "Azure AD 응용 프로그램 프록시 커넥터에 대 한 hello 기본 사항 설명"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5bb695e904d285c3b440520f107c7bf63ba5cac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a>Azure AD 응용 프로그램 프록시를 사용하여 게시된 앱에 대해 사용자 지정 홈 페이지 설정

이 문서에서는 어떻게 tooconfigure 앱 toodirect 사용자 tooa 사용자 지정 홈 페이지입니다. 응용 프로그램 프록시 응용 프로그램을 게시할 때 내부 URL을 설정 하면 사용할 수 있지만 때로는 hello 페이지를 사용자가 먼저 표시 됩니다. 사용자가 Azure Active Directory 액세스 패널 hello 또는 hello Office 365 앱 시작 관리자에서 hello 앱에 액세스할 때 toohello 오른쪽 페이지 이동 되도록 사용자 지정 홈 페이지를 설정 합니다.

Hello 앱을 시작 하는 사용자가 hello 게시 된 앱에 대 한 기본 toohello 루트 도메인 URL로 이동 하는. hello 방문 페이지는 일반적으로 hello 홈 페이지 URL로 설정 됩니다. Hello Azure AD PowerShell 모듈 toodefine 사용자 지정 홈 페이지 Url을 사용 하 여 hello 앱 내에서 특정 페이지에 응용 프로그램 사용자 tooland 하려는 경우. 

예:
- 회사 네트워크 내 사용자가 이동 너무*https://ExpenseApp/login/login.aspx* toosign에 응용 프로그램에 액세스 하 고 있습니다.
- Hello 앱을 게시 하는 응용 프로그램 프록시 tooaccess hello 폴더 구조의 최상위 hello에 필요한 이미지와 같은 다른 자산을 가지기 때문에 *https://ExpenseApp* 내부 URL hello으로 합니다.
- 기본 외부 URL은 hello *https://ExpenseApp-contoso.msappproxy.net*, 페이지에서 사용자가 toohello 기호를 사용 하지 않습니다입니다.  
- 설정 *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* 사용자가 홈 페이지 URL toogive hello으로 원활 합니다. 

>[!NOTE]
>Hello 앱 hello에 표시 됩니다 toopublished 앱 사용자가 액세스를 부여 하면 [Azure AD 액세스 패널](active-directory-saas-access-panel-introduction.md) 및 hello [Office 365 앱 시작 관리자](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher)합니다.

## <a name="before-you-start"></a>시작하기 전에

Hello 홈 페이지 URL을 설정 하기 전에 염두 hello 요구 사항에 유의 하십시오.

* 사용자가 지정한 해당 hello 경로 hello 루트 도메인 URL의 하위 도메인 경로 확인 합니다.

  Hello 루트 도메인 URL이 인 경우 예를 들어 https://apps.contoso.com/app1/, 구성 하는 hello 홈 페이지 URL 이니셜라이저에서 https://apps.contoso.com/app1/ 합니다.

* 변경 하는 경우 toohello 앱 게시, hello 변경 hello 홈 페이지 URL의 hello 값을 다시 설정 될 수 있습니다. 향후 hello에서 hello 응용 프로그램을 업데이트할 때 다시 검사를, 필요한 경우 hello 홈 페이지 URL을 업데이트 합니다.

## <a name="change-hello-home-page-in-hello-azure-portal"></a>Hello Azure 포털에서에서 변경 hello 홈 페이지

1. Toohello 로그인 [Azure 포털](https://portal.azure.com) 관리자 권한으로 합니다.
2. 너무 이동**Azure Active Directory** > **앱 등록** hello 목록에서 응용 프로그램을 선택 합니다. 
3. 선택 **속성** hello 설정에서 합니다.
4. 업데이트 hello **홈 페이지 URL** 새 경로 있는 필드입니다. 

   ![새 홈페이지 URL 제공](./media/application-proxy-office365-app-launcher/homepage.png)

5. **저장**을 선택합니다.

## <a name="change-hello-home-page-with-powershell"></a>PowerShell과 함께 변경 hello 홈 페이지

### <a name="install-hello-azure-ad-powershell-module"></a>Hello Azure AD PowerShell 모듈 설치

PowerShell을 사용 하 여 사용자 지정 홈 페이지 URL을 정의 하기 전에 hello Azure AD PowerShell 모듈을 설치 합니다. Hello에서 hello 패키지를 다운로드할 수 있습니다 [PowerShell 갤러리](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131)는, 사용 하 여 hello Graph API 끝점. 

tooinstall hello 패키지에서 다음이 단계를 수행 합니다.

1. 표준 PowerShell 창을 열고 hello 다음 명령을 실행 합니다.

    ```
     Install-Module -Name AzureAD
    ```
    Hello를 사용 하 여 hello 명령 비관리자를 실행 하는 경우 `-scope currentuser` 옵션입니다.
2. Hello 설치 하는 동안 선택 **Y** tooinstall 두 Nuget.org를 패키지 합니다. 두 개의 패키지가 모두 필요합니다. 

### <a name="find-hello-objectid-of-hello-app"></a>Hello hello 응용 프로그램의 개체 Id

Hello hello 응용 프로그램의 개체 Id를 받으며 hello 앱에 대 한 홈 페이지에서 다음 검색 합니다.

1. PowerShell을 열고 hello Azure AD 모듈을 가져옵니다.

    ```
    Import-Module AzureAD
    ```

2. 테 넌 트 관리자에 게로 Azure AD 모듈 toohello에 로그인 합니다.

    ```
    Connect-AzureAD
    ```
3. 홈 페이지 URL에 따라 hello 앱을 찾습니다. 너무 이동 하 여 hello URL hello 포털에서 찾을 수 있습니다**Azure Active Directory** > **엔터프라이즈 응용 프로그램** > **모든 응용 프로그램**합니다. 이 예제에서는 *sharepoint-iddemo*를 사용합니다.

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. 여기에 표시 된 하나 비슷한 toohello 않는 결과 가져와야 합니다. Hello ObjectID GUID toouse hello 다음 섹션에 복사 합니다.

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-hello-home-page-url"></a>업데이트 hello 홈 페이지 URL

Hello에서 1 단계에 사용한 동일한 PowerShell 모듈 hello 다음 단계를 수행 합니다.

1. 응용 프로그램, 수정 및 바꾸기 hello 있는지 확인 *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* hello hello 앞 단계에서에서 복사한 ObjectID로 합니다.

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 Hello 앱을 확인 한 했으므로 준비 tooupdate hello 홈 페이지에서 다음과 같이 것입니다.

2. 새 응용 프로그램 개체 toohold toomake hello 변경을 만듭니다. 이 변수는 tooupdate hello 값을 보유 합니다. 이 단계에서는 아무 것도 만들어지지 않습니다.

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. Hello 홈 페이지 URL toohello 원하는 값을 설정 합니다. hello 값 hello 게시 된 앱의 하위 경로 여야 합니다. 예를 들어 변경 하는 경우 홈 페이지 URL에서 hello *https://sharepoint-iddemo.msappproxy.net/* 너무*https://sharepoint-iddemo.msappproxy.net/hybrid/*, 앱 사용자가 직접 전환 toohello 사용자 지정 홈 페이지입니다.

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. 복사한 GUID (ObjectID) hello를 사용 하 여 업데이트를 hello 확인 "1 단계: 찾기 hello hello 응용 프로그램의 개체 Id입니다."

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. hello 변경 성공적으로 수행 되었는지 tooconfirm hello 앱을 다시 시작 합니다.

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
>Toohello 앱 수행한 변경 내용 hello 홈 페이지 URL을 재설정 수 있습니다. 홈페이지 URL이 다시 설정되면 2단계를 반복합니다.

## <a name="next-steps"></a>다음 단계

- [원격 액세스 tooSharePoint Azure AD 응용 프로그램 프록시를 사용 하도록 설정](application-proxy-enable-remote-access-sharepoint.md)
- [Hello Azure 포털에서에서 응용 프로그램 프록시를 사용 하도록 설정](active-directory-application-proxy-enable.md)
