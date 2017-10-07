---
title: "Azure Active Directory Domain Services: 관리되는 도메인에서의 동기화 | Microsoft Docs"
description: "Azure Active Directory Domain Services 관리되는 도메인에서의 동기화를 이해합니다."
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 57cbf436-fc1d-4bab-b991-7d25b6e987ef
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 9be25b61823a6b031906f3576395782e73831fc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="synchronization-in-an-azure-ad-domain-services-managed-domain"></a>Azure AD 도메인 서비스 관리되는 도메인에서 동기화
hello 다음 다이어그램에서는 동기화 작동 방식 Azure AD 도메인 서비스에서 관리 되는 도메인입니다.

![Azure AD Domain Services의 동기화 토폴로지](./media/active-directory-domain-services-design-guide/sync-topology.png)

## <a name="synchronization-from-your-on-premises-directory-tooyour-azure-ad-tenant"></a>온-프레미스 디렉터리 tooyour Azure AD 테 넌 트에서 동기화
Azure AD Connect 동기화 toosynchronize 사용 되는 사용자 계정, 그룹 멤버 자격 및 자격 증명 해시 tooyour Azure AD 테 넌 트 됩니다. 사용자의 속성 hello UPN 같은 계정 및 온-프레미스 SID (보안 식별자)가 동기화 됩니다. Azure AD 도메인 서비스를 사용 하면 NTLM 및 Kerberos 인증에 필요한 레거시 자격 증명 해시가 동기화 된 tooyour Azure AD 테 넌 트도 있습니다.

쓰기 저장을 구성한 경우 Azure AD 디렉터리에서 변경 되는 백 tooyour 온-프레미스 Active Directory 동기화 됩니다. Hello 변경 된 암호가 온-프레미스에서 업데이트는 Azure AD의 셀프 서비스 암호 변경 기능을 사용 하 여 암호를 변경 하는 경우에 예를 들어 AD 도메인입니다.

> [!NOTE]
> 항상 hello 최신 버전을 사용 하 여 Azure AD Connect tooensure의 알려진된 버그를 모두에 대 한 수정 해야 합니다.
>
>

## <a name="synchronization-from-your-azure-ad-tenant-tooyour-managed-domain"></a>도메인을 관리 되는 Azure AD 테 넌 트 tooyour에서 동기화
사용자 계정, 그룹 멤버 자격 및 자격 증명 해시가 Azure AD 테 넌 트 tooyour 관리 되는 도메인을 Azure AD 도메인 서비스에서에서 동기화 됩니다. 이 동기화 프로세스는 자동입니다. 않아도 tooconfigure, 모니터링 또는이 동기화 프로세스를 관리 합니다. 디렉터리의 hello 일회성 초기 동기화 완료 되 면 일반적으로 Azure AD toobe에서 변경 될 때까지 20 분 정도 걸립니다 반영 관리 되는 도메인 내에서. 이 동기화 간격 toopassword 변경 내용을 적용 하거나 Azure AD에서 tooattributes를 변경 합니다.

hello 동기화 프로세스 한 / 단방향/단방향 본질적으로 이기도합니다. 관리되는 도메인은 사용자가 만든 사용자 지정 OU를 제외하고는 대부분 읽기 전용입니다. 따라서 hello 관리 되는 도메인 내에서 변경 내용 toouser 특성, 사용자 암호 또는 그룹 멤버 자격을 만들 수 없습니다. 결과적으로, 관리 되는 도메인 백 tooyour Azure AD 테 넌 트 로부터 변경 내용 역방향 동기화가 있습니다.

## <a name="synchronization-from-a-multi-forest-on-premises-environment"></a>다중 포리스트 온-프레미스 환경에서의 동기화
많은 조직에는 여러 계정 포리스트로 구성된 매우 복잡한 온-프레미스 ID 인프라가 있습니다. Azure AD Connect 동기화 사용자, 그룹 및 다중 포리스트 환경 tooyour Azure AD 테 넌 트의 자격 증명 해시를 지원합니다.

반면, Azure AD 테넌트는 훨씬 간단한 단일 구조 네임스페이스입니다. tooenable 사용자 tooreliably access 응용 프로그램에서는 Azure AD에서 보호 다른 포리스트의 사용자 계정 간에 UPN 충돌을 해결 합니다. 색상 Azure AD 도메인 서비스 관리 되는 도메인의 곰은 tooyour Azure AD 테 넌 트를 닫습니다. 따라서 관리되는 도메인의 OU 구조는 단일 구조입니다. 모든 사용자 및 그룹 hello 온-프레미스 도메인 이나 포리스트에 있는 동기화 된에 관계 없이 hello ' AADDC Users' 컨테이너 내에 저장 됩니다. 사용자가 온-프레미스에 계층형 OU 구조를 구성했을 수도 있지만 이 경우에도 관리되는 도메인은 단순한 단일 OU 구조를 유지합니다.

## <a name="exclusions---what-isnt-synchronized-tooyour-managed-domain"></a>그렇지 않은 제외-동기화 tooyour 관리 되는 도메인
hello 다음 개체 또는 특성 없는 tooyour 관리 되는 도메인 또는 동기화 된 tooyour Azure AD 테 넌 트:

* **특성을 제외:** Azure AD Connect를 사용 하 여 온-프레미스 도메인의 테 넌 트 tooyour Azure AD 동기화에서 tooexclude 특정 특성을 선택할 수 있습니다. 이러한 제외된 특성은 관리되는 도메인에서 사용할 수 없습니다.
* **그룹 정책:** 온-프레미스 도메인에 구성 된 그룹 정책이 관리 되는 도메인 동기화 된 tooyour 되지 않습니다.
* **SYSVOL 공유:** 마찬가지로 hello hello 온-프레미스 도메인의 SYSVOL 공유의 내용이 동기화 된 tooyour 관리 되는 도메인입니다.
* **컴퓨터 개체:** 컴퓨터 조인된 tooyour 온-프레미스 도메인에 대 한 컴퓨터 개체는 동기화 된 tooyour 관리 되는 도메인입니다. 이러한 컴퓨터는 관리 되는 도메인 트러스트 관계가 설정 되어 하지 않으며 tooyour 온-프레미스 도메인에만 속해야 합니다. 관리 되는 도메인에 도메인을 관리 되는 toohello 명시적으로 도메인에 가입 되어 있는 컴퓨터에 대해서만 컴퓨터 개체를 찾는 합니다.
* **사용자 및 그룹에 대 한 SidHistory 특성:** hello 기본 사용자 및 기본 그룹에서 온-프레미스 도메인 Sid는 tooyour 동기화 된 관리 되는 도메인입니다. 그러나 사용자 및 그룹에 대 한 SidHistory 특성을 기존 온-프레미스 도메인 tooyour 관리 되는 도메인에서 동기화 되지 않습니다.
* **조직 단위 (OU) 구조:** 온-프레미스 도메인에 정의 된 조직 구성 단위 tooyour 관리 되는 도메인을 동기화 하지 않습니다. 관리되는 도메인에는 두 개의 기본 제공 OU가 있습니다. 기본적으로 관리되는 도메인은 단일 OU 구조를 가집니다. 그러나 시켜야 너무[관리 되는 도메인의 사용자 지정 OU를 만드는](active-directory-ds-admin-guide-create-ou.md)합니다.

## <a name="how-specific-attributes-are-synchronized-tooyour-managed-domain"></a>특정 특성을 동기화 된 tooyour 관리 되는 도메인 관계
다음 표에 hello 몇 가지 일반적인 특성을 나열 하 고 동기화 된 tooyour 관리 되는 도메인 하는 방법을 설명 합니다.

| 관리되는 도메인의 특성 | 원본 | 참고 사항 |
|:--- |:--- |:--- |
| UPN |Azure AD 테넌트의 사용자 UPN 특성 |Azure AD 테 넌 트에서 hello UPN 특성 tooyour 관리 되는 도메인은 동기화 됩니다. 따라서 hello 가장 신뢰할 수 있는 방식으로 toosign tooyour 관리 되는 도메인에는 UPN을 사용 합니다. |
| SAMAccountName |Azure AD 테넌트에서 사용되거나 자동 생성된 사용자의 mailNickname |hello SAMAccountName 특성은 Azure AD 테 넌 트에 hello mailNickname 특성에서 제공 됩니다. 여러 사용자 계정이 hello hello SAMAccountName 동일한 mailNickname 특성은 자동 생성 된 경우. 이면 hello 사용자의 mailNickname 또는 UPN 접두사 20 자 보다 긴 hello SAMAccountName SAMAccountName 특성에서 자동으로 생성 된 toosatisfy hello 20 자 제한 됩니다. |
| 암호 |Azure AD 테넌트의 사용자 암호 |Kerberos 인증에 필요한 자격 증명 해시(보조 자격 증명이라고도 함)는 Azure AD 테넌트에서 동기화됩니다. Azure AD 테넌트가 동기화된 테넌트인 경우 이러한 자격 증명은 온-프레미스 도메인에서 제공됩니다. |
| 기본 사용자/그룹 SID |자동 생성 |관리 되는 도메인 사용자/그룹 계정에 대 한 hello 주 SID는 자동으로 생성 합니다. 이 특성이 hello 기본 사용자/그룹 온-프레미스에 hello 개체의 SID를 일치 하지 않습니다 AD 도메인입니다. 이 불일치는 hello 관리 되는 도메인에 다른 SID 네임 스페이스가 온-프레미스 도메인 보다 때문입니다. |
| 사용자 및 그룹에 대한 SID 기록 |온-프레미스 기본 사용자 및 그룹 SID |관리 되는 도메인의 사용자 및 그룹에 대 한 SidHistory 특성 hello는 온-프레미스 도메인에 toomatch hello 해당 기본 사용자 또는 그룹 SID 설정 됩니다. 이 기능 사용 확인 리프트 및-시프트의 온-프레미스 응용 프로그램 toohello 관리 되는 도메인을 보다 쉽게 하므로 리소스의 ACL을 toore 필요가 없습니다. |

> [!NOTE]
> **Hello UPN 형식을 사용 하 여 toohello 관리 되는 도메인에 로그인:** hello SAMAccountName 특성은 관리 되는 도메인의 일부 사용자 계정에 대해 자동으로 생성 된 수 있습니다. 여러 사용자가 hello 동일한 mailNickname 특성 또는 사용자 접두사가 지나치게 긴 UPN, 이러한 사용자에 대 한 hello SAMAccountName 자동-발생할 수 있습니다. 따라서 hello SAMAccountName (예를 들어 ' CONTOSO100\joeuser') 형식이 항상 toohello 도메인에서 신뢰할 수 있는 방법은 toosign입니다. 자동 생성된 사용자의 SAMAccountName은 UPN 접두사와 다를 수 있습니다. 사용 하 여 hello UPN 형식 (예를 들어 'joeuser@contoso100.com') toosign toohello에 도메인을 안정적으로 관리 합니다.
>
>

### <a name="attribute-mapping-for-user-accounts"></a>사용자 계정에 대한 특성 매핑
다음 표에서 hello Azure AD 테 넌 트의 사용자 개체는 관리 되는 도메인 내에서 동기화 된 toocorresponding 특성에 대 한 특정 특성을 보여 줍니다.

| Azure AD 테넌트의 사용자 특성 | 관리되는 도메인의 사용자 특성 |
|:--- |:--- |
| accountEnabled |userAccountControl (설정 또는 비트 ACCOUNT_DISABLED hello 지웁니다) |
| city |l |
| country |co |
| department |department |
| displayName |displayName |
| facsimileTelephoneNumber |facsimileTelephoneNumber |
| givenName |givenName |
| jobTitle |title |
| mail |mail |
| mailNickname |msDS-AzureADMailNickname |
| mailNickname |SAMAccountName(자동 생성되는 경우도 있음) |
| mobile |mobile |
| objectId |msDS-AzureADObjectId |
| onPremiseSecurityIdentifier |sidHistory |
| passwordPolicies |userAccountControl (설정 또는 비트 DONT_EXPIRE_PASSWORD hello 지웁니다) |
| physicalDeliveryOfficeName |physicalDeliveryOfficeName |
| postalCode |postalCode |
| preferredLanguage |preferredLanguage |
| state |st |
| streetAddress |streetAddress |
| surname |sn |
| telephoneNumber |telephoneNumber |
| userPrincipalName |userPrincipalName |

### <a name="attribute-mapping-for-groups"></a>그룹에 대한 특성 매핑
다음 표에서 hello Azure AD 테 넌 트에 그룹 개체는 관리 되는 도메인 내에서 동기화 된 toocorresponding 특성에 대 한 특정 특성을 보여 줍니다.

| Azure AD 테넌트의 그룹 특성 | 관리되는 도메인의 그룹 특성 |
|:--- |:--- |
| displayName |displayName |
| displayName |SAMAccountName(자동 생성되는 경우도 있음) |
| mail |mail |
| mailNickname |msDS-AzureADMailNickname |
| objectId |msDS-AzureADObjectId |
| onPremiseSecurityIdentifier |sidHistory |
| securityEnabled |groupType |

## <a name="objects-that-are-not-synchronized-tooyour-azure-ad-tenant-from-your-managed-domain"></a>관리 되는 도메인에서 tooyour Azure AD 테 넌 트를 동기화 하는 되지 않는 개체
이 문서의 이전 섹션에 표시 된 것과 같이 관리 되는 도메인 백 tooyour Azure AD 테 넌 트에서에서 동기화가 있습니다. 너무 선택할 수 있습니다[는 사용자 지정 조직 구성 단위 (OU)를 만들](active-directory-ds-admin-guide-create-ou.md) 관리 되는 도메인에 있습니다. 또한 이러한 사용자 지정 OU 내에서 다른 OU, 사용자, 그룹 또는 서비스 계정을 만들 수 있습니다. 사용자 지정 Ou 내에서 생성 된 hello 개체 중 뒤로 tooyour Azure AD 테 넌 트를 동기화 됩니다. 이러한 개체는 관리되는 도메인 내에서만 사용할 수 있습니다. 따라서 이러한 개체 또는 Azure AD PowerShell cmdlet, Azure AD Graph API를 사용 하 여 hello Azure AD 관리 UI에 표시 되지 않습니다.

## <a name="related-content"></a>관련 콘텐츠
* [기능 - Azure AD Domain Services](active-directory-ds-features.md)
* [배포 시나리오 - Azure AD Domain Services](active-directory-ds-scenarios.md)
* [Azure AD 도메인 서비스에 대한 네트워킹 고려 사항](active-directory-ds-networking.md)
* [Azure AD 도메인 서비스 시작](active-directory-ds-getting-started.md)
