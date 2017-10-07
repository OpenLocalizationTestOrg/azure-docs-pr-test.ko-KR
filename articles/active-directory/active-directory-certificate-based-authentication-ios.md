---
title: "iOS에서 aaaAzure Active Directory 인증서 기반 인증 | Microsoft Docs"
description: "Hello 지원 시나리오와 iOS 장치와 솔루션에서 인증서 기반 인증을 구성 하는 hello 요구 사항"
services: active-directory
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: 26a6fc54-0153-44fb-b970-9b432c99e9f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 4486ff5239c2897b3bc187053f31d74807430301
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-ios"></a>iOS에서 Azure Active Directory 인증서 기반 인증

인증서 기반 인증 (CBA)에 Exchange online 계정을 연결할 때 Windows, Android 또는 iOS 장치에 클라이언트 인증서와 함께 Azure Active Directory에 의해 인증 toobe가 있습니다. 

* Microsoft Outlook 및 Microsoft Word와 같은 Office 모바일 응용 프로그램   
* EAS(Exchange ActiveSync) 클라이언트 

Hello 필요 tooenter 사용자 이름 및 암호 조합을 특정 메일 및 모바일 장치에서 Microsoft Office 응용 프로그램에이 기능을 구성을 제거 합니다. 

이 항목에서는 hello 요구 사항 및 지원 hello 시나리오 CBA Office 365 Enterprise, Business, 교육, 미국 정부, 중국, 테 넌 트의 사용자에 대해 iOS(Android) 장치에서 구성 하기 위한 하 및 독일 계획 합니다.

이 기능은 Office 365 미국 국방부 및 연방 정부 계획에서 미리 보기 상태로 제공됩니다.




## <a name="office-mobile-applications-support"></a>Office 모바일 응용 프로그램 지원

| 앱 | 지원 |
| --- | --- |
| Azure Information Protection 앱 |![확인][1] |
| Microsoft 팀 |![확인][1] |
| OneNote |![확인][1] |
| OneDrive |![확인][1] |
| Outlook |![확인][1] |
| Power BI 모바일 앱 |![확인][1] |
| 비즈니스용 Skype |![확인][1] |
| Word / Excel / PowerPoint |![확인][1] |
| Yammer |![확인][1] |


## <a name="requirements"></a>요구 사항 

hello 장치 OS 버전 이어야 iOS 9 이상 

페더레이션 서버가 구성되어야 합니다.  

Microsoft Authenticator는 iOS의 Office 응용 프로그램에 필요합니다.  

Azure Active Directory toorevoke 클라이언트 인증서에 대 한 클레임을 따라 hello hello ADFS 토큰에 있어야 합니다.  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  (hello 클라이언트 인증서의 hello 일련 번호) 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  (hello 클라이언트 인증서의 발급자 hello에 대 한 hello 문자열) 

Azure Active Directory hello ADFS 토큰 (또는 다른 SAML 토큰)에서 사용할 수 있는 경우 이러한 클레임 toohello 새로 고침 토큰을 추가 합니다. Hello 새로 고침 토큰 toobe 유효성을 검사 하면이 정보에 사용 되는 toocheck hello 해지 됩니다. 

모범 사례로, hello 다음과 같이 hello ADFS 오류 페이지를 업데이트 해야 합니다.

* iOS에 hello Microsoft Authenticator를 설치 하기 위한 hello 요구 사항
* 방법은 tooget 사용자 인증서입니다. 

자세한 내용은 참조 하십시오. [hello AD FS 로그인 페이지 사용자 지정](https://technet.microsoft.com/library/dn280950.aspx)합니다.

일부 Office 앱 (최신 인증을 사용 하도록 설정)을 보낼 '*= 프롬프트 로그인*' 요청에 tooAzure AD 합니다. 기본적으로 Azure AD 만큼 변환 hello 요청 tooADFS에 너무 '*wauth usernamepassworduri =*' (ADFS toodo P U/auth 요청) 및 '*wfresh = 0*' (ADFS tooignore SSO 상태를 요청 및 새로운 인증 수행) . 이러한 앱에 대 한 tooenable 인증서 기반 인증을 사용 하도록 하려는 경우 toomodify hello 기본 Azure AD 동작을 해야 합니다. 방금 집합 hello '*PromptLoginBehavior*' 페더레이션된 도메인 설정에 너무 '*비활성화*'. Hello를 사용할 수 있습니다 [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) tooperform cmdlet이이 작업:

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`
  

## <a name="exchange-activesync-clients-support"></a>Exchange ActiveSync 클라이언트 지원
Ios 9 이상, hello 기본 iOS 메일 클라이언트 지원 됩니다. 다른 모든 Exchange ActiveSync 응용 프로그램, toodetermine이이 기능이 지원 되는지 문의 응용 프로그램 개발자.  


## <a name="next-steps"></a>다음 단계

사용자 환경에서 tooconfigure 인증서 기반 인증을 원하는 경우 참조 [Android에서 인증서 기반 인증 시작](active-directory-certificate-based-authentication-get-started.md) 지침에 대 한 합니다.


<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-ios/ic195031.png
