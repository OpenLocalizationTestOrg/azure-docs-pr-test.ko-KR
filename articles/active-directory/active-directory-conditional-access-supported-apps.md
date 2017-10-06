---
title: "aaaApplications 및 Azure Active Directory의 조건부 액세스 규칙을 사용 하는 브라우저 | Microsoft Docs"
description: "조건부 액세스 제어를 사용한 hello 사용자 및 tooallow 응용 프로그램 액세스를 인증 하는 경우 특정 조건에 대 한 Azure Active Directory 확인 합니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 62349fba-3cc0-4ab5-babe-372b3389eff6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: ca20853bb9f4b22d0b88ddd2f051d658e0d88cf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="applications-and-browsers-that-use-conditional-access-rules-in-azure-active-directory"></a>Azure Active Directory에서 조건부 액세스 규칙을 사용하는 응용 프로그램 및 브라우저

조건부 액세스 규칙은 Azure AD(Azure Active Directory) 연결 응용 프로그램, 페더레이션된 사전 통합 SaaS(Software as a Service) 응용 프로그램, 암호 SSO(Single Sign-On)를 사용하는 프로그램, LOB(기간 업무) 응용 프로그램 및 Azure AD 응용 프로그램 프록시를 사용하는 응용 프로그램에서 지원합니다. 조건부 액세스를 사용할 수 있는 응용 프로그램의 자세한 목록은 [조건부 액세스로 설정된 서비스](active-directory-conditional-access-technical-reference.md)를 참조하세요. 조건부 액세스는 최신 인증을 사용하는 모바일과 데스크톱 응용 프로그램 모두에서 작동합니다. 이 문서에서는 모바일 및 데스크톱 앱에서 조건부 액세스가 작동되는 방법에 대해 설명합니다.

최신 인증을 사용하는 응용 프로그램에서 Azure AD 로그인 페이지를 사용할 수 있습니다. 로그인 페이지에서는 사용자에게 다단계 인증을 요구하는 메시지가 표시됩니다. Hello 사용자의 액세스가 차단 되는 경우 메시지가 표시 됩니다. 최신 인증은 Azure AD에 장치 tooauthenticate hello에 대 한 필요한 되므로 장치 기반 조건부 액세스 정책은 평가 됩니다.

것이 중요 한 tooknow 응용 프로그램을 조건부 액세스 규칙을 사용할 수 있으며이 필요할 수 있습니다 tootake toosecure 다른 응용 프로그램 진입점 단계 hello 합니다.

## <a name="applications-that-use-modern-authentication"></a>최신 인증을 사용하는 응용 프로그램
> [!NOTE]
> Azure AD에 Office 365와 대등한 조건부 액세스 정책이 있는 경우 두 조건부 액세스 정책을 모두 구성합니다. 이 적용, 예를 들어 Exchange Online 또는 SharePoint Online에 대 한 액세스 정책을 tooconditional.
>
>

hello 다음 응용 프로그램 조건부 액세스를 위한 지원 Office 365 및 기타 Azure AD에 연결 된 서비스 응용 프로그램:


| 대상 서비스| 플랫폼| 응용 프로그램 |
| --- | --- | --- |
| 모든 My Apps 앱 서비스| Android 및 iOS| 앱에 대한 MFA 및 위치 정책입니다. 장치 기반 정책은 지원되지 않습니다.|
| Azure 원격 앱 서비스| Windows 10, Windows 8.1, Windows 7, iOS, Android 및 Mac OS X| Azure 원격 앱|
| Dynamics CRM| Windows 10, Windows 8.1, Windows 7, iOS 및 Android| Dynamics CRM 앱|
| Microsoft 팀| Windows 10, Windows 8.1, Windows 7, iOS/Android 및 MAC OSX| Microsoft Teams Services - Microsoft Teams 및 모든 클라이언트 앱(Windows 데스크톱, MAC OS X, iOS, Android, WP, 웹 클라이언트)을 지원하는 서비스를 모두 제어합니다.|
| Office 365 Exchange Online| Windows 10| 메일/달력/인물 정보 앱, Outlook 2016, Outlook 2013(최신 인증 사용), 비즈니스용 Skype(최신 인증 사용)|
| Office 365 Exchange Online| Windows 8.1, Windows 7| Outlook 2016, Outlook 2013(최신 인증 사용), 비즈니스용 Skype(최신 인증 사용)|
| Office 365 Exchange Online| iOS| Outlook 모바일 앱|
| Office 365 Exchange Online| Mac OS X| Outlook 2016(macOS용 Office)|
| Office 365 SharePoint Online| Windows 10| Office 2016 응용 프로그램, 유니버설 Office 앱, Office 2013 최신 인증의 경우) (포함 OneDrive 동기화 클라이언트 (참조 [노트](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e)), 이후 hello에 대 한 향후 hello에 대 한 계획 된 Office 그룹 지원, SharePoint 응용 프로그램 지원 계획|
| Office 365 SharePoint Online| Windows 8.1, Windows 7| Office 2016 앱, Office 2013(최신 인증 사용), OneDrive 동기화 클라이언트([참고](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e) 참조)|
| Office 365 SharePoint Online| iOS, Android| Office 모바일 앱|
| Office 365 SharePoint Online| Mac OS X| macOS용 Office 2016(Word, Excel, PowerPoint, OneNote만 해당) OneDrive에 비즈니스 지원 이후 hello에 대 한 계획|
| Office 365 Yammer| Windows 10, iOS, Android| Office Yammer 앱|
| PowerBI 서비스| Windows 10, Windows 8.1, Windows 7 및 iOS| PowerBI 앱. Android 용 hello Power BI 앱은 장치 기반 조건부 액세스를 현재 지원 하지 않습니다.|
| Visual Studio Team Services| Windows 10, Windows 8.1, Windows 7, iOS 및 Android| Visual Studio Team Services 앱|








## <a name="applications-that-do-not-use-modern-authentication"></a>최신 인증을 사용하지 않는 응용 프로그램
현재, 최신 인증을 사용 하지 않는 다른 메서드 tooblock 액세스 tooapps를 사용 해야 합니다. 최신 인증을 사용하지 않는 앱에 대한 액세스 규칙이 조건부 액세스를 통해 강제로 적용되지 않기 때문입니다. 이는 기본적으로 Exchange 및 SharePoint에 대한 액세스를 위한 고려 사항입니다. 이전 버전의 앱은 대부분 이전 액세스 제어 프로토콜을 사용합니다.

### <a name="control-access-in-office-365-sharepoint-online"></a>Office 365 SharePoint Online 액세스 제어
Hello 집합 SPOTenant cmdlet을 사용 하 여 SharePoint 액세스에 대 한 레거시 프로토콜을 비활성화할 수 있습니다. SharePoint Online 리소스에 액세스 하지 못하도록 최신이 아닌 인증 인증 프로토콜을 사용 하는이 cmdlet tooprevent Office 클라이언트를 사용 합니다.

**예제 명령**: `Set-SPOTenant -LegacyAuthProtocolsEnabled $false`

### <a name="control-access-in-office-365-exchange-online"></a>Office 365 Exchange Online 액세스 제어
Exchange에서는 중요한 두 가지 범주의 프로토콜을 제공합니다. Hello 다음 옵션을 검토 하 고 조직에 적합 한 hello 정책을 선택 합니다.

* **Exchange ActiveSync** - 기본적으로 다단계 인증 및 위치에 대한 조건부 액세스 정책은 Exchange ActiveSync에 강제로 적용되지 않습니다. 해야 tooprotect 액세스 toothese 서비스 Exchange ActiveSync 정책을 직접 구성 하거나 Active Directory Federation Services (AD FS) 규칙을 사용 하 여 Exchange ActiveSync를 차단 합니다.
* **레거시 프로토콜** - AD FS를 사용하면 레거시 프로토콜을 차단할 수 있습니다. Office 2013 최신 인증을 사용 하도록 설정 하 고 이전 버전의 Office 없이 같은 액세스 tooolder Office 클라이언트를 차단 합니다.

### <a name="use-ad-fs-tooblock-legacy-protocol"></a>AD FS tooblock 레거시 프로토콜을 사용 하 여
다음 예에서는 발급 권한 부여 규칙 tooblock 레거시 프로토콜 수준에서 액세스 hello AD FS hello를 사용할 수 있습니다. 일반적인 두 가지 구성에서 선택합니다.

#### <a name="option-1-allow-exchange-activesync-and-allow-legacy-apps-but-only-on-hello-intranet"></a>옵션 1: Exchange ActiveSync를 허용 하 고 hello 인트라넷에만 레거시 앱을 허용 합니다.
다음 세 가지 규칙 toohello hello를 적용 하 여 Microsoft Office 365 Id 플랫폼, Exchange ActiveSync 트래픽에 대 한 AD FS 신뢰 당사자 트러스트와 브라우저 및 최신 인증 트래픽을 액세스할 수 있습니다. 레거시 앱 hello 엑스트라넷에서 차단 됩니다.

##### <a name="rule-1"></a>규칙 1
    @RuleName = "Allow all intranet traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "true"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

##### <a name="rule-2"></a>규칙 2
    @RuleName = "Allow Exchange ActiveSync"
    c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value == "Microsoft.Exchange.ActiveSync"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

##### <a name="rule-3"></a>규칙 3
    @RuleName = "Allow extranet browser and browser dialog traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

#### <a name="option-2-allow-exchange-activesync-and-block-legacy-apps"></a>옵션 2: Exchange ActiveSync 허용 및 레거시 앱 차단
다음 세 가지 규칙 toohello hello를 적용 하 여 Microsoft Office 365 Id 플랫폼, Exchange ActiveSync 트래픽에 대 한 AD FS 신뢰 당사자 트러스트와 브라우저 및 최신 인증 트래픽을 액세스할 수 있습니다. 레거시 앱은 모든 위치에서 차단됩니다.

##### <a name="rule-1"></a>규칙 1
    @RuleName = "Allow all intranet traffic only for browser and modern authentication clients"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "true"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


##### <a name="rule-2"></a>규칙 2
    @RuleName = "Allow Exchange ActiveSync"
    c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value == "Microsoft.Exchange.ActiveSync"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


##### <a name="rule-3"></a>규칙 3
    @RuleName = "Allow extranet browser and browser dialog traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


## <a name="supported-browsers-for-device-based-policies"></a>장치 기반 정책에 대해 지원되는 브라우저 

Azure AD를 식별 하 고 hello 장치를 인증 하는 경우 장치 규정 준수 및 도메인 가입에 대 한 확인 하는 기반으로 하는 장치 정책에 대 한 액세스를 가져올 수 있습니다. 대부분의 장치 및 브라우저에서 MFA 작업 위치 등의 대부분 검사 하는 동안 장치 정책 hello OS 버전 및 아래에 나열 된 브라우저의 필요 합니다. 장치 정책은 지원 되지 않는 브라우저 또는 hello 운영 체제에서 사용자에 대 한 액세스가 차단 됩니다. 

| OS                     | 브라우저                 | 지원     |
| :--                    | :--                      | :-:         |
| Win 10                 | IE, Edge                 | ![확인][1] |
| Win 10                 | Chrome                   | 미리 보기     |
| Win 8 / 8.1            | IE, Chrome               | ![확인][1] |
| Win 7                  | IE, Chrome               | ![확인][1] |
| iOS                    | Safari                   | ![확인][1] |
| Android                | Chrome                   | ![확인][1] |
| Windows Phone          | IE, Edge                 | ![확인][1] |
| Windows Server 2016    | IE, Edge                 | ![확인][1] |
| Windows Server 2016    | Chrome                   | 서비스 예정 |
| Windows Server 2012 R2 | IE, Chrome               | ![확인][1] |
| Windows Server 2008 R2 | IE, Chrome               | ![확인][1] |
| Mac OS                 | Safari                   | ![확인][1] |
| Mac OS                 | Chrome                   | 곧 출시됩니다 |

> [!NOTE]
> 크롬 지원을 위해 사용 해야 하 고 Windows 10 작성자가 업데이트 설치 hello 확장을 찾을 수 [여기](https://chrome.google.com/webstore/detail/windows-10-accounts/ppnbnpeolgkicgegkbkbjmhlideopiji)합니다.
>
>

## <a name="next-steps"></a>다음 단계

자세한 내용은 [Azure Active Directory 조건부 액세스](active-directory-conditional-access.md)를 참조하세요.




<!--Image references-->
[1]: ./media/active-directory-conditional-access-supported-apps/ic195031.png


