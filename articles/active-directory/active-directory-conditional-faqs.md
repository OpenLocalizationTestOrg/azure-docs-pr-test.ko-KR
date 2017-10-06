---
title: "Active Directory의 조건부 액세스 Faq aaaAzure | Microsoft Docs"
description: "Azure Active Directory의 조건부 액세스에 대 한 질문과 대답 toofrequently를 가져옵니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 14f7fc83-f4bb-41bf-b6f1-a9bb97717c34
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: d23acbb01217d7e9717d1a43de1b46a929404118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-faqs"></a>Azure Active Directory 조건부 액세스 FAQ

## <a name="which-applications-work-with-conditional-access-policies"></a>조건부 액세스 정책이 적용되는 응용 프로그램은 무엇입니까?

조건부 액세스 정책과 함께 작동하는 응용 프로그램에 대한 자세한 내용은 [Azure Active Directory에서 조건부 액세스 규칙을 사용하는 응용 프로그램 및 브라우저](active-directory-conditional-access-supported-apps.md)를 참조하세요.

## <a name="are-conditional-access-policies-enforced-for-b2b-collaboration-and-guest-users"></a>B2B 공동 작업과 게스트 사용자에게 조건부 액세스 정책이 적용됩니까?

B2B(Business-to-Business) 공동 작업 사용자에 대한 정책이 적용됩니다. 그러나 경우에 따라 사용자 아닐 수 toosatisfy hello 정책 요구 사항. 예를 들어 게스트 사용자의 조직이 다단계 인증을 지원하지 않는 경우가 있습니다. 



## <a name="does-a-sharepoint-online-policy-also-apply-tooonedrive-for-business"></a>SharePoint Online 정책도 해당 tooOneDrive 비즈니스에 대 한?

예. SharePoint Online 정책 비즈니스용 tooOneDrive도 적용 됩니다.


## <a name="why-cant-i-set-a-policy-on-client-apps-like-word-or-outlook"></a>Word나 Outlook 등의 클라이언트 앱에 정책을 설정할 수 없는 이유는 무엇입니까?

조건부 액세스 정책은 서비스 액세스 요구 사항을 설정하고, 인증 toothat 서비스 발생할 때 적용 됩니다. 클라이언트 응용 프로그램에서 직접 hello 정책 설정 되지 않았습니다. 클라이언트가 서비스를 호출할 때 적용됩니다. 예를 들어 SharePoint에서 설정한 정책 적용 tooclients SharePoint 호출 됩니다. Exchange에서 설정한 정책 tooOutlook 적용 됩니다.

## <a name="does-a-conditional-access-policy-apply-tooservice-accounts"></a>조건부 액세스 정책 tooservice 계정을 해당?

조건부 액세스 정책은 tooall 사용자 계정을 적용 됩니다. 여기에는 서비스 계정으로 사용되는 사용자 계정이 포함됩니다. 종종 무인 모드로 실행 되는 서비스 계정에는 조건부 액세스 정책 hello 요구 사항을 만족할 수 없습니다. 예를 들어 다단계 인증이 필요할 수 있습니다. 조건부 액세스 정책 관리 설정을 사용하여 서비스 계정을 정책에서 제외할 수 있습니다. 

## <a name="are-graph-apis-available-for-configuring-conditional-access-policies"></a>조건부 액세스 정책을 구성하는 데 Graph API를 사용할 수 있나요?

현재는 사용할 수 없습니다. 

## <a name="what-is-hello-default-exclusion-policy-for-unsupported-device-platforms"></a>지원 되지 않는 장치 플랫폼에 대 한 hello 기본 제외 정책 이란?

현재 iOS 및 Android 장치의 사용자에 대해 선택적으로 조건부 액세스 정책이 적용됩니다. 다른 장치 플랫폼에서 응용 프로그램을 기본적으로 영향을 받지 않습니다 iOS 및 Android 장치에 대 한 hello 조건부 액세스 정책. 테 넌 트 관리자는 지원 되지 않는 플랫폼에서 toooverride hello 글로벌 정책 toodisallow 액세스 toousers를 선택할 수 있습니다.


## <a name="how-do-conditional-access-policies-work-for-microsoft-teams"></a>Microsoft Teams에 대해 조건부 액세스 정책이 어떻게 작동하나요?  

Microsoft Teams는 모임, 일정, 파일 공유 등의 핵심 생산성 시나리오를 위해 Exchange Online 및 SharePoint Online을 많이 사용합니다. 이러한 클라우드 앱에 대해 설정 된 조건부 액세스 정책은 사용자가 로그인 할 때 tooMicrosoft 팀을 적용 합니다.

Microsoft Teams는 Azure Active Directory 조건부 액세스 정책에서 별도의 클라우드 앱으로도 지원됩니다. 클라우드 앱에 대해 설정 된 인증서 기관 정책은 사용자가 로그인 할 때 tooMicrosoft 팀을 적용 합니다.

Windows 및 Mac용 Microsoft Teams 데스크톱 클라이언트는 최신 인증을 지원합니다. 최신 인증 로그인에 플랫폼 간에 hello Azure Active Directory 인증 라이브러리 (ADAL) tooMicrosoft Office 클라이언트 응용 프로그램에 따라 제공 합니다. 
