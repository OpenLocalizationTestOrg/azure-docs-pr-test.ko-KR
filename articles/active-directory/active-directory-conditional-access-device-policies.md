---
title: "Office 365 서비스에 대 한 Active Directory 조건부 액세스 장치 정책을 aaaAzure | Microsoft Docs"
description: "조건부 액세스 장치 정책을 toohelp tooprovision 하도록 사용자 규정 준수 및 액세스 tooservices 유지 하면서 회사 리소스를 더 안전 하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8664c0bb-bba1-4012-b321-e9c8363080a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 38229a8d9766efbf0e6b17875b3018011c6b4ea3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="active-directory-conditional-access-device-policies-for-office-365-services"></a>Office 365 서비스에 대한 Active Directory 조건부 액세스 장치 정책

조건부 액세스에는 여러 조각 toowork가 필요합니다. 여기에는 다른 요인들 중에서도 다단계 인증 사용자, 인증된 장치 및 준수 장치가 포함됩니다. 이 문서에서 주로 살펴볼 조직 toohelp tooOffice 365 서비스 액세스 제어를 사용할 수 있는 장치 기반 조건에입니다. 

기업 사용자는 회사 또는 학교에서 개인 장치에서 Exchange 및 SharePoint Online와 같은 tooaccess Office 365 서비스를 원합니다. 원하는 hello 액세스 toobe 안전 합니다. 조건부 액세스 장치 정책을 toohelp 확인 회사 리소스 액세스 tooservices 규격 장치를 사용 하는 사용자에 대 한 승인 하는 동안 보다 안전한 프로 비전 할 수 있습니다. 조건부 액세스 정책을 tooOffice 365 hello Microsoft Intune 조건부 액세스 포털에서 설정할 수 있습니다.

Azure Active Directory (Azure AD)는 조건부 액세스 정책을 toohelp 보안 액세스 tooOffice 365 서비스를 적용 합니다. 비준수 장치 사용자가 Office 365 서비스에 액세스할 수 없도록 차단하는 조건부 액세스 정책을 만들 수 있습니다. hello 사용자 액세스 toohello 서비스 권한을 부여 하기 전에 toohello 회사의 장치 정책을 준수 해야 합니다. 또는 해당 장치 toogain 액세스 tooan Office 365 서비스 사용자가 tooenroll 요구 하는 정책을 만들 수 있습니다. 정책 적용된 tooall 사용자 조직에서 일 수 있습니다 또는 tooa 몇 개의 대상 그룹을 제한 합니다. 시간이 지남에 따라 자세한 대상 그룹 tooa 정책을 추가할 수 있습니다.

장치 정책 적용을 위한 필수 구성 요소가 사용자 hello Azure AD device registration service와 해당 장치를 등록 해야 합니다. Tooturn hello Azure AD 장치 등록 서비스를 등록 하는 장치에 대해 multi-factor authentication에서 선택할 수 있습니다. Multi-factor authentication hello Azure Active Directory 장치 등록 서비스에 대 한 것이 좋습니다. 다단계 인증 상태에서 2 단계 인증에 대 한 hello Azure AD 장치 등록 서비스와 해당 장치를 등록할 사용자 문제가 됩니다.

## <a name="how-does-a-conditional-access-policy-work"></a>조건부 액세스 정책의 작동 방식

지원 되는 장치 플랫폼에서 액세스 tooan Office 365 서비스를 요청 하는 사용자, Azure AD는 hello 사용자와 hello 장치를 인증 합니다. Azure AD 권한 부여 액세스 toohello 서비스 hello 사용자 hello 서비스에 대 한 설정 toohello 정책을 준수 하는 경우에 합니다. 등록 되지 않은 장치의 사용자에 게는 방법에 관한 지침이 제공 됩니다 tooenroll 규격 tooaccess 회사 Office 365 서비스 되 고 있습니다. IOS 및 Android 장치에서 사용자가 hello Intune 회사 포털 응용 프로그램을 사용 하 여 필요한 tooenroll 자신의 장치를 됩니다. 사용자는 장치를 등록, hello 장치가 Azure AD에 등록 하 고 장치 관리 및 규정 준수에 대 한 등록 합니다. Office 365 서비스에 대 한 모바일 장치 관리에 대 한 Microsoft Intune을 사용한 hello Azure AD 장치 등록 서비스를 사용 해야 합니다. 장치 등록은 장치 정책이 적용 될 때 사용자 tooaccess Office 365 서비스에 필요 합니다.

때 사용자 성공적으로 등록 하는 장치, hello 장치, 신뢰할 수 있는 됩니다. Azure AD 인증 hello 사용자 single sign-on 액세스 toocompany 응용 프로그램을 제공합니다. Azure AD는 조건부 액세스 정책 toogrant 액세스 tooa 서비스 hello hello 기존 사용자가에 대 한 액세스를 요청 뿐 아니라 모든 시간 hello 사용자 액세스에 대 한 요청 갱신 강제 적용 합니다. hello 사용자 로그인 자격 증명이 변경 된, hello 장치를 분실 하거나 도난당 한 경우 또는 갱신에 대 한 요청의 hello 시 hello 정책 hello 조건을 만족 하지 않을 때 액세스 tooservices를 거부 됩니다.

## <a name="deployment-considerations"></a>배포 고려 사항

Hello Azure AD 장치 등록 서비스 tooregister 장치를 사용 해야 합니다.

온-프레미스 사용자가 인증 되 면 toobe Active Directory Federation Services (AD FS)에 대 한 (버전 1.0 및 이상 버전)가 필요 합니다. 작업 공간 연결에 대해 multi-factor authentication hello id 공급자의 multi-factor authentication 수 없는 경우에 경우 실패 합니다. 예를 들어 AD FS 2.0에서는 다단계 인증을 사용할 수 없습니다. 해당 hello 온-프레미스 AD FS multi-factor authentication과 함께 작동 하 고 유효한 multi-factor authentication 방법 설정 되어 있는지 hello Azure AD 장치 등록 서비스에 대해 multi-factor authentication을 설정 하기 전에 확인 합니다. 예를 들어 Windows Server 2012 R2의 AD FS에는 다단계 인증 기능이 있습니다. 설정 해야 추가 유효한 인증 (multi-factor authentication) 방법 hello AD FS 서버의 hello Azure AD 장치 등록 서비스에 대해 multi-factor authentication을 설정 하기 전에. AD FS에서 지원되는 다단계 인증 방법에 대한 자세한 내용은 [AD FS에 대한 추가 인증 방법 구성](/windows-server/identity/ad-fs/operations/configure-additional-authentication-methods-for-ad-fs)을 참조하세요.

## <a name="next-steps"></a>다음 단계

*   대답 toocommon 질문에 대 한 참조 [Azure Active Directory의 조건부 액세스 Faq](active-directory-conditional-faqs.md)합니다.
