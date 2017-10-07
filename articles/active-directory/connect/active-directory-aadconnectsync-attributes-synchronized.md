---
title: "Azure AD Connect에서 동기화된 특성 | Microsoft Docs"
description: "목록 hello 특성을 tooAzure Active Directory를 동기화 합니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c2bb36e0-5205-454c-b9b6-f4990bcedf51
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: 2fe5b944a7fc832f245631416c265fb82eedeb15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-attributes-synchronized-tooazure-active-directory"></a>Azure AD Connect 동기화: tooAzure Active Directory 동기화 되는 특성
이 항목에는 Azure AD Connect 동기화를 통해 동기화 되는 hello 속성이 나열 됩니다.  
hello 특성은 그룹화 hello 관련 하 여 Azure AD 앱.

## <a name="attributes-toosynchronize"></a>특성 toosynchronize
일반적인 질문은 *hello 목록이 최소 특성이 toosynchronize 이란*합니다. hello 기본 및 권장 되는 방법이 tookeep hello 기본 특성에는 전체 GAL (전체 주소 목록)을 생성할 수 있도록 hello 클라우드와 tooget Office 365 작업에서 모든 기능입니다. 일부 경우에는 조직 하지 않으려고 동기화 된 toohello 클라우드 이러한 특성에 포함 되어 있으므로 중요 한 일부 특성이 또는이 예제에서와 같이 PII (개인 식별이 가능한 정보) 데이터:  
![잘못된 특성](./media/active-directory-aadconnectsync-attributes-synchronized/badextensionattribute.png)

이 경우이 항목에 특성 목록을 hello로 시작 하 고는 구분 또는 PII 데이터를 포함 하 고 동기화 할 수 없습니다는 해당 속성을 식별 합니다. 그런 다음 [Azure AD 앱 및 특성 필터링](active-directory-aadconnect-get-started-custom.md#azure-ad-app-and-attribute-filtering)을 사용하여 설치 중에 이러한 특성을 선택 취소합니다.

> [!WARNING]
> 특성을 선택 취소 하는 경우 주의 해야 하 고만 이러한 특성 수 없습니다. 절대 toosynchronize 선택 취소 해야 합니다. 다른 특성을 선택 취소하면 기능에 부정적인 영향을 미칠 수도 있습니다.
>
>

## <a name="office-365-proplus"></a>Office 365 ProPlus
| 특성 이름 | 사용자 | 주석 |
| --- |:---:| --- |
| accountEnabled |X |활성화된 계정을 정의합니다. |
| cn |X | |
| displayName |X | |
| objectSID |X |기계적 속성입니다. AD 사용자 id toomaintain 동기화 Azure 간에 사용 되는 AD와 AD 합니다. |
| pwdLastSet |X |기계적 속성입니다. 이미 발급 된 토큰 tooinvalidate 때 사용 되는 tooknow 합니다. 암호 동기화 및 페더레이션 모두 사용됩니다. |
| sourceAnchor |X |기계적 속성입니다. ADDS와 Azure AD 간의 toomaintain 관계를 변경할 수 없는 식별자입니다. |
| usageLocation |X |기계적 속성입니다. hello 사용자의 국가입니다. 라이선스 할당에 사용됩니다. |
| userPrincipalName |X |UPN은 hello 사용자에 대 한 hello 로그인 ID입니다. [Mail] 값과 같으며 hello 경우가 가장 많습니다. |

## <a name="exchange-online"></a>Exchange Online
| 특성 이름 | 사용자 | 연락처 | 그룹 | 주석 |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |활성화된 계정을 정의합니다. |
| 도우미 |X |X | | |
| altRecipient |X | | |Azure AD Connect 빌드 1.1.552.0 이상이 필요합니다. |
| authOrig |X |X |X | |
| C |X |X | | |
| cn |X | |X | |
| co |X |X | | |
| company |X |X | | |
| countryCode |X |X | | |
| department |X |X | | |
| description |X |X |X | |
| displayName |X |X |X | |
| dLMemRejectPerms |X |X |X | |
| dLMemSubmitPerms |X |X |X | |
| extensionAttribute1 |X |X |X | |
| extensionAttribute10 |X |X |X | |
| extensionAttribute11 |X |X |X | |
| extensionAttribute12 |X |X |X | |
| extensionAttribute13 |X |X |X | |
| extensionAttribute14 |X |X |X | |
| extensionAttribute15 |X |X |X | |
| extensionAttribute2 |X |X |X | |
| extensionAttribute3 |X |X |X | |
| extensionAttribute4 |X |X |X | |
| extensionAttribute5 |X |X |X | |
| extensionAttribute6 |X |X |X | |
| extensionAttribute7 |X |X |X | |
| extensionAttribute8 |X |X |X | |
| extensionAttribute9 |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| givenName |X |X | | |
| homePhone |X |X | | |
| info |X |X |X |이 특성은 현재 그룹에 사용되지 않습니다. |
| Initials |X |X | | |
| l |X |X | | |
| legacyExchangeDN |X |X |X | |
| mailNickname |X |X |X | |
| mangedBy | | |X | |
| manager |X |X | | |
| member | | |X | |
| mobile |X |X | | |
| maDS-HABSeniorityIndex |X |X |X | |
| msDS-PhoneticDisplayName |X |X |X | |
| msExchArchiveGUID |X | | | |
| msExchArchiveName |X | | | |
| msExchAssistantName |X |X | | |
| msExchAuditAdmin |X | | | |
| msExchAuditDelegate |X | | | |
| msExchAuditDelegateAdmin |X | | | |
| msExchAuditOwner |X | | | |
| msExchBlockedSendersHash |X |X | | |
| msExchBypassAudit |X | | | |
| msExchBypassModerationLink | | |X |Azure AD Connect 버전 1.1.524.0에서 사용 가능 |
| msExchCoManagedByLink | | |X | |
| msExchDelegateListLink |X | | | |
| msExchELCExpirySuspensionEnd |X | | | |
| msExchELCExpirySuspensionStart |X | | | |
| msExchELCMailboxFlags |X | | | |
| msExchEnableModeration |X | |X | |
| msExchExtensionCustomAttribute1 |X |X |X |이 특성은 현재 Exchange Online에 사용되지 않습니다. |
| msExchExtensionCustomAttribute2 |X |X |X |이 특성은 현재 Exchange Online에 사용되지 않습니다. |
| msExchExtensionCustomAttribute3 |X |X |X |이 특성은 현재 Exchange Online에 사용되지 않습니다. |
| msExchExtensionCustomAttribute4 |X |X |X |이 특성은 현재 Exchange Online에 사용되지 않습니다. |
| msExchExtensionCustomAttribute5 |X |X |X |이 특성은 현재 Exchange Online에 사용되지 않습니다. |
| msExchHideFromAddressLists |X |X |X | |
| msExchImmutableID |X | | | |
| msExchLitigationHoldDate |X |X |X | |
| msExchLitigationHoldOwner |X |X |X | |
| msExchMailboxAuditEnable |X | | | |
| msExchMailboxAuditLogAgeLimit |X | | | |
| msExchMailboxGuid |X | | | |
| msExchModeratedByLink |X |X |X | |
| msExchModerationFlags |X |X |X | |
| msExchRecipientDisplayType |X |X |X | |
| msExchRecipientTypeDetails |X |X |X | |
| msExchRemoteRecipientType |X | | | |
| msExchRequireAuthToSendTo |X |X |X | |
| msExchResourceCapacity |X | | | |
| msExchResourceDisplay |X | | | |
| msExchResourceMetaData |X | | | |
| msExchResourceSearchProperties |X | | | |
| msExchRetentionComment |X |X |X | |
| msExchRetentionURL |X |X |X | |
| msExchSafeRecipientsHash |X |X | | |
| msExchSafeSendersHash |X |X | | |
| msExchSenderHintTranslations |X |X |X | |
| msExchTeamMailboxExpiration |X | | | |
| msExchTeamMailboxOwners |X | | | |
| msExchTeamMailboxSharePointUrl |X | | | |
| msExchUserHoldPolicies |X | | | |
| msOrg IsOrganizational | | |X | |
| objectSID |X | |X |기계적 속성입니다. AD 사용자 id toomaintain 동기화 Azure 간에 사용 되는 AD와 AD 합니다. |
| oOFReplyToOriginator | | |X | |
| otherFacsimileTelephone |X |X | | |
| otherHomePhone |X |X | | |
| otherTelephone |X |X | | |
| pager |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| proxyAddresses |X |X |X | |
| publicDelegates |X |X |X | |
| pwdLastSet |X | | |기계적 속성입니다. 이미 발급 된 토큰 tooinvalidate 때 사용 되는 tooknow 합니다. 암호 동기화 및 페더레이션 모두 사용됩니다. |
| reportToOriginator | | |X | |
| reportToOwner | | |X | |
| securityEnabled | | |X |groupType에서 파생됩니다 |
| sn |X |X | | |
| sourceAnchor |X |X |X |기계적 속성입니다. ADDS와 Azure AD 간의 toomaintain 관계를 변경할 수 없는 식별자입니다. |
| st |X |X | | |
| streetAddress |X |X | | |
| targetAddress |X |X | | |
| telephoneAssistant |X |X | | |
| telephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| title |X |X | | |
| unauthOrig |X |X |X | |
| usageLocation |X | | |기계적 속성입니다. hello 사용자의 국가입니다. 라이선스 할당에 사용됩니다. |
| userCertificate |X |X | | |
| userPrincipalName |X | | |UPN은 hello 사용자에 대 한 hello 로그인 ID입니다. [Mail] 값과 같으며 hello 경우가 가장 많습니다. |
| userSMIMECertificates |X |X | | |
| wWWHomePage |X |X | | |

## <a name="sharepoint-online"></a>SharePoint Online
| 특성 이름 | 사용자 | 연락처 | 그룹 | 주석 |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |활성화된 계정을 정의합니다. |
| authOrig |X |X |X | |
| C |X |X | | |
| cn |X | |X | |
| co |X |X | | |
| company |X |X | | |
| countryCode |X |X | | |
| department |X |X | | |
| description |X |X |X | |
| displayName |X |X |X | |
| dLMemRejectPerms |X |X |X | |
| dLMemSubmitPerms |X |X |X | |
| extensionAttribute1 |X |X |X | |
| extensionAttribute10 |X |X |X | |
| extensionAttribute11 |X |X |X | |
| extensionAttribute12 |X |X |X | |
| extensionAttribute13 |X |X |X | |
| extensionAttribute14 |X |X |X | |
| extensionAttribute15 |X |X |X | |
| extensionAttribute2 |X |X |X | |
| extensionAttribute3 |X |X |X | |
| extensionAttribute4 |X |X |X | |
| extensionAttribute5 |X |X |X | |
| extensionAttribute6 |X |X |X | |
| extensionAttribute7 |X |X |X | |
| extensionAttribute8 |X |X |X | |
| extensionAttribute9 |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| givenName |X |X | | |
| hideDLMembership | | |X | |
| homePhone |X |X | | |
| info |X |X |X | |
| Initials |X |X | | |
| ipPhone |X |X | | |
| l |X |X | | |
| mail |X |X |X | |
| mailNickname |X |X |X | |
| managedBy | | |X | |
| manager |X |X | | |
| member | | |X | |
| middleName |X |X | | |
| mobile |X |X | | |
| msExchTeamMailboxExpiration |X | | | |
| msExchTeamMailboxOwners |X | | | |
| msExchTeamMailboxSharePointLinkedBy |X | | | |
| msExchTeamMailboxSharePointUrl |X | | | |
| objectSID |X | |X |기계적 속성입니다. AD 사용자 id toomaintain 동기화 Azure 간에 사용 되는 AD와 AD 합니다. |
| oOFReplyToOriginator | | |X | |
| otherFacsimileTelephone |X |X | | |
| otherHomePhone |X |X | | |
| otherIpPhone |X |X | | |
| otherMobile |X |X | | |
| otherPager |X |X | | |
| otherTelephone |X |X | | |
| pager |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| postOfficeBox |X |X | | |
| preferredLanguage |X | | | |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |기계적 속성입니다. 이미 발급 된 토큰 tooinvalidate 때 사용 되는 tooknow 합니다. 암호 동기화 및 페더레이션 모두 사용됩니다. |
| reportToOriginator | | |X | |
| reportToOwner | | |X | |
| securityEnabled | | |X |groupType에서 파생됩니다 |
| sn |X |X | | |
| sourceAnchor |X |X |X |기계적 속성입니다. ADDS와 Azure AD 간의 toomaintain 관계를 변경할 수 없는 식별자입니다. |
| st |X |X | | |
| streetAddress |X |X | | |
| targetAddress |X |X | | |
| telephoneAssistant |X |X | | |
| telephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| title |X |X | | |
| unauthOrig |X |X |X | |
| url |X |X | | |
| usageLocation |X | | |기계적 속성입니다. hello 사용자의 국가입니다. 라이선스 할당에 사용됩니다. |
| userPrincipalName |X | | |UPN은 hello 사용자에 대 한 hello 로그인 ID입니다. [Mail] 값과 같으며 hello 경우가 가장 많습니다. |
| wWWHomePage |X |X | | |

## <a name="lync-online"></a>Lync Online
| 특성 이름 | 사용자 | 연락처 | 그룹 | 주석 |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |활성화된 계정을 정의합니다. |
| C |X |X | | |
| cn |X | |X | |
| co |X |X | | |
| company |X |X | | |
| department |X |X | | |
| description |X |X |X | |
| displayName |X |X |X | |
| facsimiletelephonenumber |X |X |X | |
| givenName |X |X | | |
| homePhone |X |X | | |
| ipPhone |X |X | | |
| l |X |X | | |
| mail |X |X |X | |
| mailNickname |X |X |X | |
| managedBy | | |X | |
| manager |X |X | | |
| member | | |X | |
| mobile |X |X | | |
| msExchHideFromAddressLists |X |X |X | |
| msRTCSIP-ApplicationOptions |X | | | |
| msRTCSIP-DeploymentLocator |X |X | | |
| msRTCSIP-Line |X |X | | |
| msRTCSIP-OptionFlags |X |X | | |
| msRTCSIP-OwnerUrn |X | | | |
| msRTCSIP-PrimaryUserAddress |X |X | | |
| msRTCSIP-UserEnabled |X |X | | |
| objectSID |X | |X |기계적 속성입니다. AD 사용자 id toomaintain 동기화 Azure 간에 사용 되는 AD와 AD 합니다. |
| otherTelephone |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| preferredLanguage |X | | | |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |기계적 속성입니다. 이미 발급 된 토큰 tooinvalidate 때 사용 되는 tooknow 합니다. 암호 동기화 및 페더레이션 모두 사용됩니다. |
| securityEnabled | | |X |groupType에서 파생됩니다 |
| sn |X |X | | |
| sourceAnchor |X |X |X |기계적 속성입니다. ADDS와 Azure AD 간의 toomaintain 관계를 변경할 수 없는 식별자입니다. |
| st |X |X | | |
| streetAddress |X |X | | |
| telephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| title |X |X | | |
| usageLocation |X | | |기계적 속성입니다. hello 사용자의 국가입니다. 라이선스 할당에 사용됩니다. |
| userPrincipalName |X | | |UPN은 hello 사용자에 대 한 hello 로그인 ID입니다. [Mail] 값과 같으며 hello 경우가 가장 많습니다. |
| wWWHomePage |X |X | | |

## <a name="azure-rms"></a>Azure RMS
| 특성 이름 | 사용자 | 연락처 | 그룹 | 주석 |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |활성화된 계정을 정의합니다. |
| cn |X | |X |일반 이름 또는 별칭입니다. 가장 자주 hello의 접두사 [mail] 값입니다. |
| displayName |X |X |X |Hello 이름 (이름, 성)으로 자주 표시 되는 hello 이름을 나타내는 문자열입니다. |
| mail |X |X |X |메일 주소 전체입니다. |
| member | | |X | |
| objectSID |X | |X |기계적 속성입니다. AD 사용자 id toomaintain 동기화 Azure 간에 사용 되는 AD와 AD 합니다. |
| proxyAddresses |X |X |X |기계적 속성입니다. Azure AD에서 사용됩니다. Hello 사용자에 대 한 모든 보조 메일 주소를 포함합니다. |
| pwdLastSet |X | | |기계적 속성입니다. 이미 발급 된 토큰 tooinvalidate 때 사용 되는 tooknow 합니다. |
| securityEnabled | | |X |groupType에서 파생됩니다. |
| sourceAnchor |X |X |X |기계적 속성입니다. ADDS와 Azure AD 간의 toomaintain 관계를 변경할 수 없는 식별자입니다. |
| usageLocation |X | | |기계적 속성입니다. hello 사용자의 국가입니다. 라이선스 할당에 사용됩니다. |
| userPrincipalName |X | | |이 UPN은 hello 사용자에 대 한 hello 로그인 ID입니다. [Mail] 값과 같으며 hello 경우가 가장 많습니다. |

## <a name="intune"></a>Intune
| 특성 이름 | 사용자 | 연락처 | 그룹 | 주석 |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |활성화된 계정을 정의합니다. |
| C |X |X | | |
| cn |X | |X | |
| description |X |X |X | |
| displayName |X |X |X | |
| mail |X |X |X | |
| mailNickname |X |X |X | |
| member | | |X | |
| objectSID |X | |X |기계적 속성입니다. AD 사용자 id toomaintain 동기화 Azure 간에 사용 되는 AD와 AD 합니다. |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |기계적 속성입니다. 이미 발급 된 토큰 tooinvalidate 때 사용 되는 tooknow 합니다. 암호 동기화 및 페더레이션 모두 사용됩니다. |
| securityEnabled | | |X |groupType에서 파생됩니다 |
| sourceAnchor |X |X |X |기계적 속성입니다. ADDS와 Azure AD 간의 toomaintain 관계를 변경할 수 없는 식별자입니다. |
| usageLocation |X | | |기계적 속성입니다. hello 사용자의 국가입니다. 라이선스 할당에 사용됩니다. |
| userPrincipalName |X | | |UPN은 hello 사용자에 대 한 hello 로그인 ID입니다. [Mail] 값과 같으며 hello 경우가 가장 많습니다. |

## <a name="dynamics-crm"></a>Dynamics CRM
| 특성 이름 | 사용자 | 연락처 | 그룹 | 주석 |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |활성화된 계정을 정의합니다. |
| C |X |X | | |
| cn |X | |X | |
| co |X |X | | |
| company |X |X | | |
| countryCode |X |X | | |
| description |X |X |X | |
| displayName |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| givenName |X |X | | |
| l |X |X | | |
| managedBy | | |X | |
| manager |X |X | | |
| member | | |X | |
| mobile |X |X | | |
| objectSID |X | |X |기계적 속성입니다. AD 사용자 id toomaintain 동기화 Azure 간에 사용 되는 AD와 AD 합니다. |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| preferredLanguage |X | | | |
| pwdLastSet |X | | |기계적 속성입니다. 이미 발급 된 토큰 tooinvalidate 때 사용 되는 tooknow 합니다. 암호 동기화 및 페더레이션 모두 사용됩니다. |
| securityEnabled | | |X |groupType에서 파생됩니다 |
| sn |X |X | | |
| sourceAnchor |X |X |X |기계적 속성입니다. ADDS와 Azure AD 간의 toomaintain 관계를 변경할 수 없는 식별자입니다. |
| st |X |X | | |
| streetAddress |X |X | | |
| telephoneNumber |X |X | | |
| title |X |X | | |
| usageLocation |X | | |기계적 속성입니다. hello 사용자의 국가입니다. 라이선스 할당에 사용됩니다. |
| userPrincipalName |X | | |UPN은 hello 사용자에 대 한 hello 로그인 ID입니다. [Mail] 값과 같으며 hello 경우가 가장 많습니다. |

## <a name="3rd-party-applications"></a>타사 응용 프로그램
이 그룹은 hello 일반 작업 또는 응용 프로그램에 필요한 최소한의 특성으로 사용 되는 특성입니다. 다른 섹션에 나열되지 않은 워크로드 또는 타사 앱에 사용할 수 있습니다. Hello 다음에 대 한 명시적으로 사용 됩니다.

* Yammer(User만 사용됨)
* [SharePoint와 같은 리소스에서 제공하는 하이브리드 B2B 조직 간 공동 작업 시나리오](http://go.microsoft.com/fwlink/?LinkId=747036)

이 그룹은 toosupport Office 365, Dynamics, 또는 Intune을 사용 하는 hello Azure AD 디렉터리가 아닌 경우 사용할 수 있는 특성의 집합입니다. 코어 특성의 작은 집합이 있습니다.

| 특성 이름 | 사용자 | 연락처 | 그룹 | 주석 |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |활성화된 계정을 정의합니다. |
| cn |X | |X | |
| displayName |X |X |X | |
| givenName |X |X | | |
| mail |X | |X | |
| managedBy | | |X | |
| mailNickname |X |X |X | |
| member | | |X | |
| objectSID |X | | |기계적 속성입니다. AD 사용자 id toomaintain 동기화 Azure 간에 사용 되는 AD와 AD 합니다. |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |기계적 속성입니다. 이미 발급 된 토큰 tooinvalidate 때 사용 되는 tooknow 합니다. 암호 동기화 및 페더레이션 모두 사용됩니다. |
| sn |X |X | | |
| sourceAnchor |X |X |X |기계적 속성입니다. ADDS와 Azure AD 간의 toomaintain 관계를 변경할 수 없는 식별자입니다. |
| usageLocation |X | | |기계적 속성입니다. hello 사용자의 국가입니다. 라이선스 할당에 사용됩니다. |
| userPrincipalName |X | | |UPN은 hello 사용자에 대 한 hello 로그인 ID입니다. [Mail] 값과 같으며 hello 경우가 가장 많습니다. |

## <a name="windows-10"></a>Windows 10
Windows 10 도메인에 가입 된 computer(device) 일부 특성 tooAzure AD를 동기화합니다. Hello 시나리오에 대 한 자세한 내용은 참조 하십시오. [발생 하는 Windows 10에 대 한 AD 도메인에 가입 된 장치 tooAzure 연결](../active-directory-azureadjoin-devices-group-policy.md)합니다. 이 특성은 항상 동기화되며 Windows 10은 선택 취소할 수 있는 앱으로 표시되지 않습니다. Windows 10 도메인에 가입 된 컴퓨터는 hello 특성 userCertificate 채워진 것으로 식별 됩니다.

| 특성 이름 | 장치 | 주석 |
| --- |:---:| --- |
| accountEnabled |X | |
| deviceTrustType |X |도메인에 가입된 컴퓨터에 대해 하드 코딩된 값입니다. |
| displayName |X | |
| ms-DS-CreatorSID |X |registeredOwnerReference라고도 합니다. |
| objectGUID |X |deviceID라고도 합니다. |
| objectSID |X |onPremisesSecurityIdentifier라고도 합니다. |
| operatingSystem |X |deviceOSType이라고도 합니다. |
| operatingSystemVersion |X |deviceOSVersion이라고도 합니다. |
| userCertificate |X | |

이러한 특성에 대 한 **사용자** 는 또한 toohello 응용 프로그램을 선택 합니다.  

| 특성 이름 | 사용자 | 주석 |
| --- |:---:| --- |
| domainFQDN |X |dnsDomainName이라고도 합니다. 예를 들어 contoso.com입니다. |
| domainNetBios |X |netBiosName이라고도 합니다. 예를 들어 CONTOSO입니다. |

## <a name="exchange-hybrid-writeback"></a>Exchange 하이브리드 쓰기 저장
이러한 특성 다시 기록 되며 Azure AD tooon 온-프레미스 Active Directory에서에서 tooenable 선택 **Exchange 하이브리드**합니다. Exchange 버전에 따라 더 적은 특성을 동기화 할 수 있습니다.

| 특성 이름 | 사용자 | 연락처 | 그룹 | 주석 |
| --- |:---:|:---:|:---:| --- |
| msDS-ExternalDirectoryObjectID |X | | |Azure AD의 cloudAnchor에서 파생됩니다. 이 특성은 Exchange 2016 및 Windows Server 2016 AD의 새로운 기능입니다. |
| msExchArchiveStatus |X | | |온라인 보관: 고객 tooarchive 메일을 활성화합니다. |
| msExchBlockedSendersHash |X | | |필터링: 온-프레미스 필터링을 다시 쓰고 온라인 보관 및 보낸 사람의 데이터를 클라이어트로부터 차단합니다. |
| msExchSafeRecipientsHash |X | | |필터링: 온-프레미스 필터링을 다시 쓰고 온라인 보관 및 보낸 사람의 데이터를 클라이어트로부터 차단합니다. |
| msExchSafeSendersHash |X | | |필터링: 온-프레미스 필터링을 다시 쓰고 온라인 보관 및 보낸 사람의 데이터를 클라이어트로부터 차단합니다. |
| msExchUCVoiceMailSettings |X | | |통합 메시징 (UM)-온라인 음성 메일을 사용 하도록 설정: Microsoft Lync Server 통합 tooindicate tooLync에서 사용 하는 온-프레미스 서버는 hello 사용자가 음성 메일 온라인 서비스에 있습니다. |
| msExchUserHoldPolicies |X | | |소송 보류: 사용자가 소송 보유 하는 클라우드 서비스 toodetermine를 수 있습니다. |
| proxyAddresses |X |X |X |Exchange Online에서 x500 hello 주소에만 삽입 됩니다. |
| publicDelegates |X | | |Exchange Online 사서함 toobe는 온-프레미스 Exchange 사서함이 있는 SendOnBehalfTo 권한 toousers 부여 수 있습니다. Azure AD Connect 빌드 1.1.552.0 이상이 필요합니다. |

## <a name="exchange-mail-public-folder"></a>Exchange 메일 공용 폴더
이러한 특성은 온-프레미스 Active Directory tooAzure tooenable를 선택 하는 경우 AD에서에서 동기화 된 **Exchange 메일에 대 한 공용 폴더**합니다.

| 특성 이름 | PublicFolder | 주석 |
| --- | :---:| --- |
| displayName | X |  |
| mail | X |  |
| msExchRecipientTypeDetails | X |  |
| objectGUID | X |  |
| proxyAddresses | X |  |
| targetAddress | X |  |

## <a name="device-writeback"></a>장치 쓰기 저장
Active Directory에 장치 개체를 만듭니다. 이러한 개체는 장치 tooAzure AD 또는 도메인에 가입 된 Windows 10 컴퓨터를 조인할 수 있습니다.

| 특성 이름 | 장치 | 주석 |
| --- |:---:| --- |
| altSecurityIdentities |X | |
| displayName |X | |
| dn |X | |
| msDS-CloudAnchor |X | |
| msDS-DeviceID |X | |
| msDS-DeviceObjectVersion |X | |
| msDS-DeviceOSType |X | |
| msDS-DeviceOSVersion |X | |
| msDS-DevicePhysicalIDs |X | |
| msDS-KeyCredentialLink |X |Windows Server 2016 AD 스키마에서만 |
| msDS-IsCompliant |X | |
| msDS-IsEnabled |X | |
| msDS-IsManaged |X | |
| msDS-RegisteredOwner |X | |

## <a name="notes"></a>참고 사항
* 사용 하 여 대체 ID를 hello 온-프레미스 특성 userPrincipalName hello Azure AD 특성 onPremisesUserPrincipalName와 동기화 됩니다. 대체 ID 특성 hello, 예를 들어 메일, Azure AD 특성 userPrincipalName hello와 동기화 됩니다.
* Hello 목록 위의 개체 유형 hello **사용자** toohello 개체 형식에도 적용 됩니다 **iNetOrgPerson**합니다.

## <a name="next-steps"></a>다음 단계
Hello에 대 한 자세한 [Azure AD Connect 동기화](active-directory-aadconnectsync-whatis.md) 구성 합니다.

[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.
