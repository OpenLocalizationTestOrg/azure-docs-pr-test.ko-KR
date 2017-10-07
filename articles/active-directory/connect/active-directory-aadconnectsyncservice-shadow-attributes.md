---
title: "aaaAzure AD Connect 동기화 서비스 섀도 특성 | Microsoft Docs"
description: "Azure AD Connect 동기화 서비스에서 섀도 특성이 작동하는 방식을 설명합니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1b8665e7488c6078b655f8a3e35519145bacd898
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-shadow-attributes"></a>Azure AD Connect 동기화 서비스 섀도 특성
대부분의 특성에 표시 되는 동일한 방식으로 hello Azure AD 온-프레미스 Active Directory에 있는 것 처럼 합니다. 하지만 일부 특성은 몇 가지 특수 한 처리 및 Azure AD에서 특성 값 hello Azure AD Connect 동기화 하는 기능 보다 다를 수 있습니다.

## <a name="introducing-shadow-attributes"></a>섀도 특성 소개
일부 특성은 Azure AD에서 두 가지로 표현됩니다. Hello 온-프레미스 값과 계산된 된 값이 저장 됩니다. 이러한 추가 특성을 섀도 특성이라고 합니다. 이 문제를 표시 하는 hello 두 가장 일반적인 특성은 **userPrincipalName** 및 **/ / proxyAddress**합니다. 특성 값의 변경 내용이 hello 검증 되지 않은 도메인을 나타내는 이러한 특성에 값이 있을 때 발생 합니다. 하지만 hello 동기화 엔진 연결에 값을 읽습니다 hello hello 그림자 특성에 있으므로 해당 관점에서 hello 특성이 확인 해야 합니다.

Hello Azure 포털 또는 PowerShell을 사용 하 여 hello 그림자 특성을 볼 수 없습니다. 않지만 hello 개념 이해 도움이 됩니다 있습니다 tootroubleshoot 특정 시나리오 hello 특성에 값이 다른 온-프레미스와 클라우드 hello.

toobetter는 hello 동작 이해를 Fabrikam에서이 예제를 확인 합니다.  
![도메인](./media/active-directory-aadconnectsyncservice-shadow-attributes/domains.png)  
온-프레미스 Active Directory에 UPN 접미사가 여러 개 있지만 확인된 것은 하나뿐입니다.

### <a name="userprincipalname"></a>userPrincipalName
사용자가 다음 검증 되지 않은 도메인의 특성 값에는 hello:

| 특성 | 값 |
| --- | --- |
| 온-프레미스 userPrincipalName | lee.sperry@fabrikam.com |
| Azure AD shadowUserPrincipalName | lee.sperry@fabrikam.com |
| Azure AD userPrincipalName | lee.sperry@fabrikam.onmicrosoft.com |

hello userPrincipalName 특성은 PowerShell을 사용 하는 경우 참조 하는 hello 값입니다.

Hello 실제 온-프레미스 특성 값은 hello fabrikam.com 도메인을 확인 하기는 경우 Azure AD에 저장 되므로 Azure AD는 hello userPrincipalName 특성 hello shadowUserPrincipalName의 hello 값으로 업데이트 합니다. 없는 toosynchronize 이러한 값 toobe 업데이트에 대 한 Azure AD Connect의 변경 내용을 합니다.

### <a name="proxyaddresses"></a>proxyAddresses
hello 일부 추가 논리가 하면서도 proxyAddresses에 대 한 동일한 프로세스만 확인 된 도메인을 포함 하는 데에 발생 합니다. 사서함 사용자에 대 한 확인 된 도메인에 대 한 hello 확인만 발생합니다. 메일 사용이 가능한 사용자 또는 연락처 Exchange 조직의 다른 사용자 나타내고 proxyAddresses toothese 개체의 모든 값을 추가할 수 있습니다.

사서함 사용자의 경우 온-프레미스 또는 Exchange Online에서 확인된 도메인의 값만 표시됩니다. 다음과 같이 표시될 수 있습니다.

| 특성 | 값 |
| --- | --- |
| 온-프레미스 proxyAddresses | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie.spencer@fabrikam.com</br>smtp:abbie@fabrikamonline.com |
| Exchange Online proxyAddresses | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie@fabrikamonline.com</br>SIP:abbie.spencer@fabrikamonline.com |

이 경우 해당 도메인이 확인되지 않았기 때문에 **smtp:abbie.spencer@fabrikam.com**이 제거되었습니다. 하지만 Exchange가 **SIP:abbie.spencer@fabrikamonline.com**을 추가했습니다. Fabrikam은 Lync/Skype 온-프레미스를 사용하지 않지만 Azure AD와 Exchange Online은 그에 대한 준비를 합니다.

ProxyAddresses에 대 한이 논리는 참조 된 tooas **ProxyCalc**합니다. 다음과 같은 경우 사용자에 대한 모든 변경 내용과 함께 ProxyCalc가 호출됩니다.

- hello 사용자 hello 사용자가 Exchange에 사용 허가 되지 않더라도 Exchange Online을 포함 하는 서비스 계획을 할당 되었습니다. 예를 들어 hello 사용자가 할당 하는 경우 Office E3 SKU hello 있지만 SharePoint Online 할당만 합니다. 사서함이 계속 온-프레미스에 있는 경우에도 마찬가지입니다.
- hello 특성 msExchRecipientTypeDetails 값을 갖습니다.
- 변경 tooproxyAddresses 또는 userPrincipalName 하면 됩니다.

ProxyCalc는 사용자에 몇 시간 tooprocess 변경 걸릴 수 있습니다 하 고 hello Azure AD Connect 내보내기 프로세스 동기화 되지 않습니다.

> [!NOTE]
> hello ProxyCalc 논리는이 항목에서 설명 하지는 고급 시나리오에 대 한 몇 가지 추가적인 동작에 있습니다. 이 항목에는 toounderstand hello 동작을 위해 모든 내부 논리를 설명 하지 제공 됩니다.

### <a name="quarantined-attribute-values"></a>격리된 특성 값
중복된 특성 값이 있는 경우에도 섀도 특성이 사용됩니다. 자세한 내용은 참조 [중복 특성 복원력](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)을 참조하세요.

## <a name="see-also"></a>참고 항목
* [Azure AD Connect 동기화](active-directory-aadconnectsync-whatis.md)
* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)
