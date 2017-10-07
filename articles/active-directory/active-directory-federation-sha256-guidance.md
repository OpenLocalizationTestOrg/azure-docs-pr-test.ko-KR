---
title: "Office 365 신뢰 당사자 트러스트에 대 한 서명 해시 알고리즘 aaaChange | Microsoft Docs"
description: "이 페이지에서는 Office 365와의 페더레이션 트러스트에 대한 SHA 알고리즘을 변경하는 방법에 대한 지침을 제공합니다."
keywords: "SHA1,SHA256,O365,페더레이션,aadconnect,adfs,ad fs,sha 변경,페더레이션 트러스트,신뢰 당사자 트러스트"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: samueld
editor: 
ms.assetid: cf6880e2-af78-4cc9-91bc-b64de4428bbd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: anandy
ms.openlocfilehash: 3333d1384aff8bdf6b3bcc894f8c633fd9ccc3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="change-signature-hash-algorithm-for-office-365-relying-party-trust"></a>Office 365 신뢰 당사자 트러스트에 대한 서명 해시 알고리즘 변경
## <a name="overview"></a>개요
Active Directory Federation Services (AD FS) 변조 될 수 있는 해당 토큰 tooMicrosoft Azure Active Directory tooensure에 서명 합니다. 이 서명은 SHA1 또는 SHA256을 기반으로 할 수 있습니다. Azure Active Directory 이제는 s h a 256 알고리즘으로 서명 토큰을 지원 하 고 hello 토큰 서명 알고리즘 tooSHA256 hello 가장 높은 수준의 보안을 설정 하는 것이 좋습니다. 이 문서에서는 필요한 tooset hello 토큰 서명 알고리즘 toohello 보안 강화 SHA256 수준 hello 단계를 설명 합니다.

>[!NOTE]
>Microsoft는 s h a 1 보다 더 안전 하지만 SHA1 여전히 지원 되는 옵션으로 토큰을 서명 하는 것에 대 한 hello 알고리즘으로 s h a 256의 사용을 권장 합니다.

## <a name="change-hello-token-signing-algorithm"></a>Hello 토큰 서명 알고리즘 변경
아래 두 프로세스 hello 중 하나가 지정 된 hello 서명 알고리즘을 설정한 후 AD FS 신뢰 당사자 트러스트 SHA256와 Office 365에 대 한 hello 토큰에 서명 합니다. 추가 구성 변경 내용을 toomake 필요 하지 않습니다 되었으며이 변경 프로그램 기능 tooaccess Office 365 또는 다른 Azure AD 응용 프로그램에 영향을 주지 않습니다.

### <a name="ad-fs-management-console"></a>AD FS 관리 콘솔
1. Hello 기본 AD FS 서버에서 hello AD FS 관리 콘솔을 엽니다.
2. Hello AD FS 노드를 확장 하 고 클릭 **신뢰 당사자 트러스트**합니다.
3. Office 365/Azure 신뢰 당사자 트러스트를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.
4. 선택 hello **고급** 탭 및 선택 hello 보안 해시 알고리즘 s h a 256입니다.
5. **확인**을 클릭합니다.

![SHA256 서명 알고리즘--MMC](./media/active-directory-aadconnectfed-sha256guidance/mmc.png)

### <a name="ad-fs-powershell-cmdlets"></a>AD FS PowerShell cmdlet
1. AD FS 서버에서 관리자 권한으로 PowerShell을 엽니다.
2. Hello를 사용 하 여 hello 보안 해시 알고리즘 집합 **집합 AdfsRelyingPartyTrust** cmdlet.
   
   <code>Set-AdfsRelyingPartyTrust -TargetName 'Microsoft Office 365 Identity Platform' -SignatureAlgorithm 'http://www.w3.org/2001/04/xmldsig-more#rsa-sha256'</code>

## <a name="also-read"></a>참조 항목
* [Azure AD Connect를 사용하여 Office 365 트러스트 복구](connect/active-directory-aadconnect-federation-management.md#repairthetrust)

