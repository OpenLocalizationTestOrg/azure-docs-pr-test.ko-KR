---
title: "Azure Active Directory 조건부 액세스 기술 참조 | Microsoft Docs"
description: "Azure Active Directory에서 조건부 액세스 제어가 작동하는 방식을 알아봅니다. 응용 프로그램에 대해 사용자를 인증하고 액세스를 제어하기 위한 조건을 지정합니다. 지정된 조건이 충족되면 사용자를 인증하고 응용 프로그램에 대한 액세스를 부여합니다."
services: active-directory.
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 56a5bade-7dcc-4dcf-8092-a7d4bf5df3c1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 09/01/2017
ms.author: markvi
ms.reviewer: spunukol
ms.openlocfilehash: 27ace4e9bc4a1626059fba657dce0c629d52f32d
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a>Azure Active Directory 조건부 액세스 기술 참조

[Azure AD(Azure Active Directory) 조건부 액세스](active-directory-conditional-access-azure-portal.md)를 사용하여 권한 있는 사용자가 리소스를 액세스하는 방법을 미세 조정할 수 있습니다.  

이 토픽에서는 조건부 액세스 정책의 다음 구성 옵션에 대한 지원 정보를 제공합니다. 

- 클라우드 응용 프로그램 할당

- 장치 플랫폼 조건 

- 클라이언트 응용 프로그램 조건

- 승인된 클라이언트 응용 프로그램 요구 사항



## <a name="cloud-apps-assignments"></a>클라우드 앱 할당

조건부 액세스 정책을 구성할 경우 [정책을 사용할 클라우드 앱](active-directory-conditional-access-azure-portal.md#who)을 선택해야 합니다. 

![정책에 대한 클라우드 앱 선택](./media/active-directory-conditional-access-technical-reference/09.png)


### <a name="microsoft-cloud-applications"></a>Microsoft 클라우드 응용 프로그램

Microsoft의 다음 클라우드 앱에 조건부 액세스 정책을 할당할 수 있습니다.

- Azure RemoteApp

- Microsoft Dynamics 365

- Microsoft Office 365 Yammer

- Microsoft Office 365 Exchange Online

- Microsoft Office 365 SharePoint Online(비즈니스용 OneDrive 포함)

- Microsoft Power BI 

- Microsoft Visual Studio Team Services

- Microsoft 팀


### <a name="other-applications"></a>다른 응용 프로그램 

Microsoft 클라우드 앱 외에도 다음과 같은 형식의 클라우드 앱에 조건부 액세스 정책을 할당할 수 있습니다.

- Azure AD에 연결된 응용 프로그램

- 사전 통합되고 페더레이션된 SaaS(software as a service) 응용 프로그램

- 암호 SSO(Single Sign-On)를 사용하는 응용 프로그램

- 기간 업무 응용 프로그램

- Azure AD 응용 프로그램 프록시를 사용하는 응용 프로그램


## <a name="device-platform-condition"></a>장치 플랫폼 조건

조건부 액세스 정책에서 정책을 클라이언트의 운영 체제에 연결하는 장치 플랫폼 조건을 구성할 수 있습니다.

![클라이언트 OS에 액세스 정책 연결](./media/active-directory-conditional-access-technical-reference/41.png)

Azure AD 조건부 액세스에서는 다음과 같은 장치 플랫폼을 지원합니다.

- Android

- iOS

- Windows Phone

- Windows

- macOS(미리 보기)



## <a name="client-apps-condition"></a>클라이언트 앱 조건 

조건부 액세스 정책을 구성할 경우 클라이언트 앱 조건에 대해 [클라이언트 앱](active-directory-conditional-access-azure-portal.md#client-apps)을 선택할 수 있습니다. 다음과 같은 종류의 클라이언트 앱에서 액세스를 시도할 때 액세스를 차단하거나 부여하는 클라이언트 앱 조건을 설정합니다.

- 브라우저
- 모바일 앱 및 데스크톱 앱

![클라이언트 앱에 대한 액세스 제어](./media/active-directory-conditional-access-technical-reference/03.png)

### <a name="supported-browsers"></a>지원되는 브라우저 

조건부 액세스 정책에서 **브라우저** 옵션을 사용하여 브라우저 액세스를 제어합니다. 지원되는 브라우저에서 액세스를 시도해야만 액세스가 부여됩니다. 지원되지 않는 브라우저에서 액세스하는 경우 시도가 차단됩니다.

![지원되는 브라우저의 액세스 제어](./media/active-directory-conditional-access-technical-reference/05.png)

조건부 액세스 정책에서 다음 브라우저가 지원됩니다. 


| OS                     | 브라우저                    | 지원     |
| :--                    | :--                         | :-:         |
| Windows 10             | Internet Explorer, Edge     | ![확인][1] |
| Windows 10             | Chrome                      | ![확인][1] |
| Windows 8 / 8.1        | Internet Explorer, 크롬   | ![확인][1] |
| Windows 7              | Internet Explorer, 크롬   | ![확인][1] |
| iOS                    | Safari, Intune Managed Browser                      | ![확인][1] |
| Android                | 크롬, Intune Managed Browser                      | ![확인][1] |
| Windows Phone          | Internet Explorer, Edge     | ![확인][1] |
| Windows Server 2016    | Internet Explorer, Edge     | ![확인][1] |
| Windows Server 2016    | Chrome                      | 서비스 예정 |
| Windows Server 2012 R2 | Internet Explorer, 크롬   | ![확인][1] |
| Windows Server 2008 R2 | Internet Explorer, 크롬   | ![확인][1] |
| macOS                  | Safari                      | ![확인][1] |
| macOS                  | Chrome                      | 곧 출시됩니다 |

> [!NOTE]
> 크롬 지원의 경우 Windows 10 Creators 업데이트(버전 1703) 이상을 사용해야 합니다.<br>
> [이 확장](https://chrome.google.com/webstore/detail/windows-10-accounts/ppnbnpeolgkicgegkbkbjmhlideopiji)을 설치할 수 있습니다.

### <a name="supported-mobile-applications-and-desktop-clients"></a>지원되는 모바일 응용 프로그램 및 데스크톱 클라이언트

조건부 액세스 정책의 **모바일 앱 및 데스크톱 클라이언트** 옵션을 사용하여 앱 및 클라이언트 액세스를 제어합니다. 지원되는 모바일 앱 또는 데스크톱 클라이언트에서 액세스를 시도해야만 액세스가 부여됩니다. 지원되지 않는 앱이나 클라이언트에서 액세스하는 경우 시도가 차단됩니다.

![지원되는 모바일 앱 또는 데스크톱 클라이언트에 대한 액세스 제어](./media/active-directory-conditional-access-technical-reference/06.png)

Office 365 및 기타 Azure AD 연결 서비스 응용 프로그램에 대한 조건부 액세스를 지원하는 모바일 앱 및 데스크톱 클라이언트는 다음과 같습니다.


| 클라이언트 응용 프로그램| 대상 서비스| 플랫폼 |
| --- | --- | --- |
| 앱에 대한 Azure Multi-Factor Authentication 및 위치 정책(장치 기반 정책 지원 안 함)| 모든 My Apps 앱 서비스| Android, iOS|
| Azure RemoteApp| Azure RemoteApp 서비스| Windows 10, Windows 8.1, Windows 7, iOS, Android, macOS|
| Dynamics 365 앱| Dynamics 365| Windows 10, Windows 8.1, Windows 7, iOS, Android|
| Microsoft Office 365 Teams(Windows Desktop, iOS, Android, Windows Phone, 웹 클라이언트 등, Microsoft Teams과 모든 해당 앱을 지원하는 모든 서비스 제어)| Microsoft 팀| Windows 10, Windows 8.1, Windows 7, iOS, Android|
| 메일/달력/인물 정보 앱, Outlook 2016, Outlook 2013(최신 인증 사용), 비즈니스용 Skype(최신 인증 사용)| Office 365 Exchange Online| Windows 10|
| Outlook 2016, Outlook 2013(최신 인증 사용), 비즈니스용 Skype(최신 인증 사용)| Office 365 Exchange Online| Windows 8.1, Windows 7|
| Outlook 모바일 앱| Office 365 Exchange Online| iOS|
| Outlook 2016(macOS용 Office)| Office 365 Exchange Online| macOS|
| Office 2016 앱, Universal Office 앱, Office 2013(최신 인증 사용), [OneDrive](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e) 동기화 클라이언트, 향후 Office Groups 및 SharePoint 앱 지원 예정| Office 365 SharePoint Online| Windows 10|
| Office 2016 앱, Office 2013(최신 인증 사용), [OneDrive](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e) 동기화 클라이언트| Office 365 SharePoint Online| Windows 8.1, Windows 7|
| Office 모바일 앱| Office 365 SharePoint Online| iOS, Android|
| macOS용 Office 2016(Word, Excel, PowerPoint, OneNote만 지원), 향후 OneDrive for Business 지원 예정| Office 365 SharePoint Online| macOS|
| Office Yammer 앱| Office 365 Yammer| Windows 10, iOS, Android|
| PowerBI 앱(현재 Android에서 지원되지 않음)| PowerBI 서비스| Windows 10, Windows 8.1, Windows 7 및 iOS|
| Visual Studio Team Services 앱| Visual Studio Team Services| Windows 10, Windows 8.1, Windows 7, iOS, Android|



## <a name="approved-client-app-requirement"></a>승인된 클라이언트 앱 요구 사항 

조건부 액세스 정책에서 **승인된 클라이언트 앱 필요** 옵션을 사용하여 클라이언트 연결을 제어합니다. 승인된 클라이언트 앱으로 연결하는 경우에만 액세스가 부여됩니다.

![승인된 클라이언트 앱에 대한 액세스 제어](./media/active-directory-conditional-access-technical-reference/21.png)

승인된 클라이언트 응용 프로그램 요구 사항에 다음 클라이언트 앱을 사용할 수 있습니다.

- Microsoft Excel

- Microsoft OneDrive

- Microsoft Outlook

- Microsoft OneNote

- Microsoft PowerPoint

- Microsoft SharePoint

- 비즈니스용 Microsoft Skype

- Microsoft 팀

- Microsoft Visio

- Microsoft Word


**설명**

- 승인된 클라이언트 앱은 Intune 모바일 응용 프로그램 관리 기능을 지원합니다.

- **승인된 클라이언트 앱 필요** 요구 사항:

    - [장치 플랫폼 조건](#device-platforms-condition)에서는 iOS 및 Android만 지원됩니다.

    - [클라이언트 앱 조건](#supported-browsers)에서는 **브라우저** 옵션을 지원하지 않습니다.
    
    - 이 옵션을 선택하면 **모바일 앱 및 데스크톱 클라이언트** 옵션이 [클라이언트 앱 조건](#supported-mobile-apps-and-desktop-clients)을 대체합니다.


## <a name="next-steps"></a>다음 단계

- 조건부 액세스에 대한 개요는 [Azure Active Directory의 조건부 액세스](active-directory-conditional-access-azure-portal.md)를 참조하세요.
- 사용자 환경에서 조건부 액세스 정책을 구성할 준비가 완료된 경우 [Azure Active Directory의 조건부 액세스 권장 사례](active-directory-conditional-access-best-practices.md)를 참조하세요.



<!--Image references-->
[1]: ./media/active-directory-conditional-access-technical-reference/01.png


