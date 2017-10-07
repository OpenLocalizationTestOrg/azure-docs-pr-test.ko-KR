---
title: "aaaPrivileged Id 관리 구독-Azure | Microsoft Docs"
description: "Hello 구독 및 라이선스 관리 및 테 넌 트의 Azure AD Privileged Identity Management를 사용 하 여 요구 사항 설명"
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: mwahl
ms.assetid: 34367721-8b42-4fab-a443-a2e55cdbf33d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: 2639d13c250a582fdcf0b277c9bab37fdfcabcb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-privileged-identity-management-subscription-requirements"></a>Azure Active Directory Privileged Identity Management 구독 요구 사항

Azure AD Privileged Identity Management는 사용할 수 있는 Azure AD Premium P2 hello 버전의 일환으로 합니다. P2 및 tooPremium P1 비교의 다른 기능을 hello에 대 한 자세한 내용은 다음을 참조 합니다. [Azure Active Directory 버전](../active-directory-editions.md)합니다.

>[!NOTE]
미리 보기에서 Azure Active Directory (Azure AD) Privileged Identity Management 때 테 넌 트 tootry hello 서비스에 대 한 라이선스 검사 했습니다.  Azure AD Privileged Identity Management 일반 가용성에 도달 했으므로 평가판 또는 유료 구독에 대 한 Privileged Identity Management를 사용 하 여 2016 년 12 월 이후 hello 테 넌 트 toocontinue 있어야 합니다.
  

## <a name="confirm-your-trial-or-paid-subscription"></a>평가판 또는 유료 구독 확인

확실 하지 않은 여부 조직에는 평가판 구독을 구매 하거나, Azure Active Directory 모듈에 대 한 Windows PowerShell v 1에 포함 된 hello 명령을 사용 하 여 테 넌 트의 구독 인지 확인할 수 합니다. 
1. PowerShell 창을 엽니다.
2. 입력 `Connect-MsolService` tooauthenticate 테 넌 트에 사용자로 합니다.
3. `Get-MsolSubscription | ft SkuPartNumber,IsTrial,Status`을 입력합니다.

이 명령은 테 넌 트의 hello 구독의 목록을 검색합니다. 가 없을 경우 줄이 더 반환 된 Azure AD Premium P2 tooobtain 평가판 해야 Azure AD Premium P2 구독 또는 EMS E5 구독 toouse Azure AD Privileged Identity Management 구입 합니다.  tooget 평가판 및 Azure AD Privileged Identity Management를 사용 하 여 시작 읽기 [Azure AD Privileged Identity Management 시작](../active-directory-privileged-identity-management-getting-started.md)합니다.

이 명령은 한 줄에 반환 하는 경우 어떤 SkuPartNumber "AAD_PREMIUM_P2" 또는 "EMSPREMIUM" 하며 IsTrial은 "True",이 Azure AD Premium P2 평가판 hello 테 넌 트에 있는지 나타냅니다.  Hello 구독 상태를 사용 하지 않는 경우는 P2 Azure AD Premium 또는 EMS E5 구독 구매 없는 다음 구입 해야 Azure AD Premium P2 구독 또는 Azure AD Privileged Identity Management를 사용 하 여 EMS E5 구독 toocontinue 합니다.

Azure AD Premium P2을 통해 제공 되는 [Microsoft 기업 계약](https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx), hello [열려 있는 볼륨 라이선스 프로그램](https://www.microsoft.com/en-us/licensing/licensing-programs/open-license.aspx), 및 hello [클라우드 솔루션 공급자 프로그램](https://partner.microsoft.com/en-US/cloud-solution-provider)합니다. 또한 Azure 및 Office 365 구독자는 Azure AD Premium P2를 온라인으로 구입할 수도 있습니다.  자세한 내용은 Azure AD Premium 가격 및 tooorder 온라인에서 찾을 수 있습니다 어떻게 [Azure Active Directory 가격](https://azure.microsoft.com/en-us/pricing/details/active-directory/)합니다.

## <a name="azure-ad-privileged-identity-management-is-not-available-in-tenant"></a>Azure AD Privileged Identity Management를 테넌트에서 사용할 수 없음

다음과 같은 경우 Azure AD Privileged Identity Management를 테넌트에서 더 이상 사용할 수 없습니다.
- 조직이 미리 보기 상태이며 Azure AD Premium P2 구독 또는 EMS E5 구독을 구입하지 않은 상태에서 Azure AD Privileged Identity Management를 사용하고 있었습니다.
- 조직이 만료된 Azure AD Premium P2 또는 EMS E5 평가판을 보유하고 있습니다.
- 조직이 구입한 구독이 만료되었습니다.

Azure AD Premium P2 구독 또는 EMS E5 구독이 만료되거나 미리 보기의 Azure AD Privileged Identity Management를 사용하던 조직이 Azure AD Premium P2 또는 EMS E5 구독을 구입하지 않았습니다.

- 영구 역할 할당 tooAzure AD 역할 영향을 받지 것입니다.
- hello hello Azure 포털에서에서 Azure AD Privileged Identity Management 확장으로 hello Graph API cmdlet 및 Azure AD Privileged Identity Management의 PowerShell 인터페이스는 더 이상 사용자 tooactivate 권한 있는 역할에 대 한 사용 가능, 관리 특권 수준의 액세스, 또는 권한 있는 역할의 액세스 검토를 수행 합니다.
- 사용자가 내용이 수 tooactivate 권한 있는 역할 되므로 더 이상 Azure AD 역할의 적합 한 역할 할당 제거 됩니다.
- Azure AD 역할에 대해 진행 중인 모든 액세스 검토가 종료되고 Azure AD Privileged Identity Management 구성 설정이 제거됩니다.
- Azure AD Privileged Identity Management는 더 이상 역할 할당 변경에 대한 전자 메일을 전송하지 않습니다.

## <a name="next-steps"></a>다음 단계

- [Azure AD Privileged Identity Management 시작](../active-directory-privileged-identity-management-getting-started.md)
- [Azure AD Privileged Identity Management의 역할](../active-directory-privileged-identity-management-roles.md)
