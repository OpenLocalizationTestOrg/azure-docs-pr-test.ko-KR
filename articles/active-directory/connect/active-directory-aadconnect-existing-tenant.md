---
title: "Azure AD Connect: Azure AD가 이미 있는 경우 | Microsoft Docs"
description: "이 항목에서는 toouse 연결 하는 경우는 방법을 설명 기존 Azure AD 테 넌 트가 있습니다."
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
ms.openlocfilehash: f7b166e9e85c1f03330e8e0074d4afa4036738c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-when-you-have-an-existent-tenant"></a>Azure AD Connect: 기존 테넌트가 있는 경우
대부분 toouse Azure AD Connect 가정 하 하는 방법에 대 한 hello 항목의 시작 새 azure AD 테 넌 트 및 사용자가 또는 다른 개체에 있습니다. 사용자 및 기타 개체를 제공을 toouse 연결을 할 수 있지만 Azure AD 테 넌 트 사용을 시작 하는 경우 다음이 항목은 합니다.

## <a name="hello-basics"></a>hello 기본 사항
Azure AD의 개체는 하거나 hello 클라우드 (Azure AD) 또는 온-프레미스에서 마스터 됩니다. 단일 개체의 경우 온-프레미스의 일부 특성과 Azure AD의 다른 일부 특성은 관리할 수 없습니다. 각 개체에 hello 개체가 관리 되는 위치를 나타내는 플래그입니다.

일부 사용자가 온-프레미스 및 기타 hello 클라우드에서 관리할 수 있습니다. 이 구성의 일반적인 시나리오는 회계 직원과 판매 직원이 혼합된 조직입니다. hello 회계 직원 들은 온-프레미스 AD 계정 하지만 hello 판매 직원은 그렇지 않습니다, Azure AD의 계정을 갖습니다. 온-프레미스의 일부 사용자와 Azure AD의 일부 사용자를 관리합니다.

Toomanage 사용자가 시작한 경우에 있는 Azure AD에서 온-프레미스 AD 있는데 나중에 toouse Connect tooconsider 필요한 몇 가지 추가 문제가 다음 합니다.

## <a name="sync-with-existing-users-in-azure-ad"></a>Azure AD의 기존 사용자와 동기화
Azure AD Connect를 설치 하는 경우 동기화를 시작 하기 hello Azure AD 동기화 서비스 (Azure AD)는 모든 새 개체에 검사를 시도 기존 개체 toomatch toofind. 이 프로세스에는 **userPrincipalName**, **proxyAddresses** 및 **sourceAnchor**/**immutableID**의 세 가지 특성이 사용됩니다. **userPrincipalName** 및 **proxyAddresses**에 대한 일치를 **소프트 일치**라고 하며, **sourceAnchor**에 대한 일치는 **하드 일치**라고 합니다. Hello에 대 한 **proxyAddresses** 특성으로 hello 값만 **SMTP:**, 하는 hello 기본 전자 메일 주소, hello 평가에 사용 됩니다.

연결에서 생성 된 새 개체에 hello 일치만 계산 됩니다. 이러한 특성 중 하나와 일치하도록 기존 개체를 변경하는 경우 오류가 대신 표시됩니다.

Azure AD hello 특성에 값이 hello 개체를 찾습니다. 오는 개체에 대 한 동일한 연결에서 이미 있는 Azure ad에서는 다음 hello Azure AD의 개체는 프로세스에 의해 처리 연결 합니다. hello 이전에 클라우드 관리 개체도 플래그가 지정 되어 온-프레미스 관리 합니다. 모든 특성 값이 온-프레미스에 있는 Azure AD에서 AD hello 온-프레미스 값으로 덮어쓰여집니다. hello 예외는 특성에 있는 경우는 **NULL** 온-프레미스 값입니다. 이 경우 Azure AD는 남아 있지만 있습니다 hello 값도 변경할 수 다른 온-프레미스 toosomething 합니다.

> [!WARNING]
> Azure AD의 모든 특성이 hello 온-프레미스 값 덮어쓰기 toobe 것 이며, 이후 적절 한 데이터 온-프레미스 있는지 확인 합니다. 예를 들어 Office 365에서만 전자 메일 주소를 관리하고 온-프레미스 AD DS에서 전자 메일 주소를 업데이트하지 않은 경우 AD DS에 없는 Azure AD/Office 365의 값을 잃게 됩니다.

> [!IMPORTANT]
> 하는 경우 항상 기본 설정으로 사용 되는 암호 동기화를 사용 하 고 hello 암호가 온-프레미스에서 Azure AD에 hello 암호 덮어쓰기 AD 합니다. 경우 tooinform 해야 사용자가 사용 되는 toomanage 다른 암호를 사용 해야 하는 연결을 설치한 후 온-프레미스 암호를 hello 합니다.

이전 섹션 hello 및 경고를 계획할 고려 되어야 합니다. 에 반영 되지 않고 Azure AD에서 많은 변경이 변경한 경우 온-프레미스 AD DS와 Azure AD Connect 사용 하 여 개체를 동기화 하기 전에 AD DS hello로 toopopulate 값을 업데이트 하는 방법에 대 한 tooplan 해야 합니다.

소프트-일치 하는 사용 하 여 개체, 일치 하는 경우 다음 hello **sourceAnchor** 하드 일치 항목을 나중에 사용할 수 있도록 Azure AD에서 toohello 개체가 추가 됩니다.

### <a name="hard-match-vs-soft-match"></a>하드 일치 및 소프트 일치
Connect를 새로 설치하는 경우 소프트 일치와 하드 일치 사이에 실질적인 차이가 없습니다. hello 차이점은 재해 복구 상황입니다. Azure AD Connect를 사용하여 서버를 잃어버린 경우 데이터 손실 없이 새 인스턴스를 다시 설치할 수 있습니다. SourceAnchor 가진 개체가 초기 설치 중 tooConnect 전송 됩니다. hello 일치 다음 평가할 수 이렇게 하면 보다 훨씬 빠릅니다 hello 클라이언트 (Azure AD Connect)에 의해 Azure AD에서 hello 동일 합니다. 하드 일치는 Connect와 Azure AD 모두에서 평가되지만, 소프트 일치는 Azure AD에서만 평가됩니다.

### <a name="other-objects-than-users"></a>사용자 이외의 다른 개체
사용자가 주로 userPrincipalName 및 proxyAddresses, 모두 hello 일치 항목을 쉽게 합니다. 그러나 보안 그룹과 같은 다른 개체에는 이러한 특성이 없습니다. 이 경우 hello sourceAnchor를 사용 하 여 하드 일치에만 연결할 수 있습니다. hello sourceAnchor가 항상 Base64 변환 hello **objectGUID** 온-프레미스에 있으므로 두 개의 개체 toomatch 중지 해야 하는 Azure AD의 hello 값을 업데이트 해야 합니다. hello sourceAnchor/immutableID powershell를 사용 하 여 hello 포털에만 업데이트할 수 있습니다.

## <a name="create-a-new-on-premises-active-directory-from-data-in-azure-ad"></a>Azure AD의 데이터에서 새로운 온-프레미스 Active Directory 만들기
일부 고객은 Azure AD를 사용하는 클라우드 전용 솔루션으로 시작하고 온-프레미스 AD를 사용하지 않습니다. 나중에 tooconsume 온-프레미스 리소스를 않고자 toobuild 온-프레미스 AD 데이터를 기반으로 Azure AD. 이 시나리오에서는 Azure AD Connect가 도움이 되지 않습니다. 사용자가 온-프레미스를 생성 하지 않습니다 하 고 모든 기능 tooset hello 암호가 온-프레미스 toohello 없는 Azure AD와 같습니다.

Hello tooadd를 계획 하는 이유는 유일한 이유 온-프레미스 AD는 toosupport Lob (기간 업무 앱) 이면 toouse 고려해 야 있을 경우 [Azure AD 도메인 서비스](../../active-directory-domain-services/index.md) 대신 합니다.

## <a name="next-steps"></a>다음 단계
[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.
