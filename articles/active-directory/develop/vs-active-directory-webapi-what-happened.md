---
title: "만든 aaaChanges tooa WebApi 프로젝트 tooAzure 광고를 연결 하는 경우 | Microsoft Docs"
description: "Visual Studio를 사용 하 여 AD tooAzure를 연결할 때 tooyour WebApi 프로젝트 결과 설명 합니다."
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 57630aee-26a2-4326-9dbb-ea2a66daa8b0
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 1ea77b6c75b2dc273219fa6c43f02c7a7c5312ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-webapi-project-visual-studio-azure-active-directory-connected-service"></a>어떤 발생 했습니다 toomy WebApi 프로젝트 (Visual Studio의 Azure Active Directory 서비스를 연결 하는 데 사용)
> [!div class="op_single_selector"]
> * [시작](vs-active-directory-webapi-getting-started.md)
> * [변경된 내용](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a>참조가 추가됨
### <a name="nuget-package-references"></a>NuGet 패키지 참조
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a>.NET 참조
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a>코드 변경 내용
### <a name="code-files-were-added-tooyour-project"></a>Tooyour 프로젝트에 추가 된 코드 파일이
인증 시작 클래스, **App_Start/Startup.Auth.cs** Azure AD 인증에 대 한 시작 논리를 포함 하는 tooyour 프로젝트에 추가 되었습니다.

### <a name="startup-code-was-added-tooyour-project"></a>시작 코드 tooyour 프로젝트에 추가 된
프로젝트에서 시작 클래스 이미 설치한 경우 hello **구성** 메서드가 업데이트 된 tooinclude 호출 너무`ConfigureAuth(app)`합니다. 그렇지 않은 경우 시작 클래스 tooyour 프로젝트를 추가 되었습니다.

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a>app.config 또는 web.config 파일에 새 구성 값이 추가됨
구성 항목을 다음 hello 추가 되었습니다.

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="hello App ID Uri from hello wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a>Azure AD 앱이 만들어짐
Azure AD 응용 프로그램은 hello 마법사에서 선택한 hello 디렉터리에서 만들어졌습니다.

[Azure Active Directory에 대한 자세한 정보](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a>검사 하는 경우 *개별 사용자 계정 인증을 사용 하지 않도록 설정*, 추가 변경 내용을 toomy 프로젝트?
NuGet 패키지 참조가 제거되고 파일이 제거 및 백업되었습니다. 프로젝트의 hello 상태에 따라 toomanually 추가 참조 또는 파일을 제거 하거나 적절 하 게 코드를 수정 해야 합니다.

### <a name="nuget-package-references-removed-for-those-present"></a>NuGet 패키지 참조가 제거됨(해당되는 경우)
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a>코드 파일이 백업 및 제거됨(해당되는 경우)
다음 파일의 각 백업 하 고 hello 프로젝트에서 제거 되었습니다. 백업 파일은 hello hello 프로젝트의 디렉터리 루트에 '백업' 폴더에 있습니다.

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a>코드 파일이 백업됨(해당되는 경우)
교체 전에 다음 파일이 각각 백업되었습니다. 백업 파일은 hello hello 프로젝트의 디렉터리 루트에 '백업' 폴더에 있습니다.

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a>검사 하는 경우 *디렉터리 데이터 읽기*, 추가 변경 내용을 toomy 프로젝트?
### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a>Tooyour app.config 또는 web.config에 추가 변경 내용이 적용 된
hello 다음과 같은 추가 구성 항목 추가 되었습니다.

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a>Azure Active Directory 앱이 업데이트됨
Azure Active Directory 앱이 업데이트 된 tooinclude hello *디렉터리 데이터 읽기* hello로 다음 사용 권한 및 추가 키를 만든 *ida: 암호* hello에 `web.config` 파일입니다.

## <a name="next-steps"></a>다음 단계
- [Azure Active Directory에 대한 자세한 정보](https://azure.microsoft.com/services/active-directory/)

