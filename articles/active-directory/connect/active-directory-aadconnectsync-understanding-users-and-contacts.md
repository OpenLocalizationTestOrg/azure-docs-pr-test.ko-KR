---
title: "Azure AD Connect 동기화: 사용자 및 연락처 이해 | Microsoft Docs"
description: "Azure AD Connect 동기화의 사용자 및 연락처에 대해 설명합니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8d204647-213a-4519-bd62-49563c421602
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi;andkjell
ms.openlocfilehash: 4d80648c53a2981eb2626338913ed2282423f183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-users-and-contacts"></a>Azure AD Connect Sync: 사용자 및 연락처 이해
여러 Active Directory 포리스트를 가져야 하는 이유와 배포 토폴로지는 여러 가지가 있습니다. 일반적인 모델에는 합병 & 인수 후 계정 리소스 배포 및 GAL 동기화 포리스트가 포함됩니다. 하지만 순수 모델이 있어도 하이브리드 모델도 일반적입니다. Azure AD Connect 동기화의 기본 구성에서는 hello 특정 모델을 가정 하지 않습니다 되지만 어떻게 사용자 일치에서 선택한 hello 설치 가이드를 따라 다른 동작을 관찰할 수 있습니다.

이 항목에서는 특정 토폴로지에서 hello 기본 구성 동작 하는 방식을 살펴보겠습니다. Hello 구성 살펴보겠습니다 및 동기화 규칙 편집기 hello hello 구성에 사용 되는 toolook 될 수 있습니다.

Hello 구성 것으로 가정 하는 일반적인 규칙 몇 가지가 있습니다.

* Hello 소스 현재 디렉터리에서에서 가져올, 순서에 관계 없이 hello 최종 결과 항상 될 hello 동일한 합니다.
* 활성 계정은 항상 **userPrincipalName** 및**sourceAnchor**를 포함한 로그인 정보를 제공합니다.
* 사용할 수 없는 계정을 주지 userPrincipalName 및 sourceanchor를 제공 하지 않은 경우 연결 된 사서함을 찾을 수 없는 현재 계정 toobe 없을 경우.
* 연결된 사서함이 있는 계정은 userPrincipalName 및 sourceAnchor에 대 해 사용되지 않습니다. 활성 계정이 나중에 검색되는 것으로 가정합니다.
* 사용자 또는 연락처 연락처 개체 프로 비전 된 tooAzure AD을 수 있습니다. 모든 원본 Active Directory 포리스트가 처리 될 때까지 실제로 알지 못합니다.

## <a name="contacts"></a>연락처
연락처가 다른 포리스트의 사용자를 나타내게 하는 것은 GALSync 솔루션이 둘 이상의 Exchange 포리스트 사이를 연결하는 M&A 후에 일반적입니다. hello에 연락처 개체는 항상 hello 커넥터 공간 toohello 메타 버스 hello 메일 특성을 사용 하 여에서 조인 됩니다. 이미 있는 경우 동일한 메일 주소는 연락처 개체나 사용자 개체가 hello로, hello 개체가 함께 조인 됩니다. Hello 규칙에 구성 됨 **에서 from AD – Contact Join**합니다. 규칙은 또한 **에서 from AD – Contact Common** 특성 흐름 toohello 메타 버스 특성을 가진 **sourceObjectType** hello 상수와 **연락처**합니다. 이 규칙에 우선 순위가 매우 낮으므로 사용자 개체가 조인된 toohello는 경우 동일한 메타 버스 개체가 다음 hello 규칙 **에서 from AD – User Common** 주지 hello 값 사용자 toothis 특성입니다. 이 규칙을 사용할 경우이 특성이 없는 사용자가 조인 하는 경우에 게 문의 하 고 하나 이상의 사용자를 찾을 수 없으면 값 사용자 hello hello 값을 갖습니다.

개체 tooAzure AD 프로 비전에 아웃 바운드 규칙 hello **tooAAD – Join 문의 아웃** 경우 hello 연락처 개체를 만듭니다 메타 버스 특성 **sourceObjectType** 너무 설정**문의** . 이 특성은 너무 설정 하는 경우**사용자**, 다음 hello 규칙 **tooAAD – User Join 아웃** 대신 사용자 개체를 만듭니다.
있기 소스 현재 디렉터리를 가져오고 동기화 하는 경우 개체에서 연락처 tooUser 승격 됩니다.

예를 들어 GALSync 토폴로지에서 살펴보면 연락처 개체 모두를 위한 두 번째 포리스트의 hello hello 첫 번째 포리스트를 가져올 때. 이 새 연락처 개체가 AAD 커넥터 hello에 스테이징 됩니다. 나중에 가져올 고 두 번째 포리스트의 hello 동기화, 때는 실제 사용자에 게 hello 찾을 하 고 toohello 기존 메타 버스 개체에 테이블을 조인 합니다. 그런 다음 hello AAD에서 연락처 개체를 삭제 하 고 새 사용자 개체를 대신 만들어야 합니다.

사용자가 연락처로 표시 되는 위치는 토폴로지를 사용 하도록 설정한 경우 hello 설치 가이드에서 toomatch hello 메일 특성에 있는 사용자를 선택 했는지 확인 합니다. 다른 옵션을 선택하면 주문에 종속된 구성이 만들어집니다. 연락처 개체는 항상 hello 메일 특성에 조인 하지만 사용자 개체 hello 설치 가이드에서이 옵션을 선택한 경우에 hello 메일 특성에 조인 됩니다. 될 수 있습니다 다음 hello로 hello 메타 버스의 두 개의 서로 다른 개체와 동일한 메일 특성 hello 사용자 개체 보다 먼저 hello 연락처 개체를 가져온 경우. 내보내기 tooAzure 광고 하는 동안 오류가 throw 됩니다. 이 동작은 설계 된 잘못 된 데이터 477860 또는 hello 설치 하는 동안 해당 hello 토폴로지가 올바로 식별 되지 않았음을 합니다.

## <a name="disabled-accounts"></a>비활성화된 계정
비활성된 계정은 AD tooAzure도 동기화 됩니다. 사용 하지 않는 계정을 exchange에서 예를 들어 회의실 일반적인 toorepresent 리소스입니다. hello 예외; 연결 된 사서함이 있는 사용자는 위에서 언급 한 대로이 프로 비전 하지 않습니다 계정 tooAzure AD 합니다.

hello 이라고 가정 하는 사용 하지 않는 사용자 계정이 발견 되 면 찾지 않으며 다른 활성 계정을 나중에 고 hello 개체는 hello userPrincipalName 및 sourceAnchor를 찾을 수 있는 프로 비전 된 tooAzure AD 합니다. 경우에 다른 활성 계정이 toohello 사용한 다음의 userPrincipalName 및 sourceAnchor 동일한 메타 버스 개체에 연결 됩니다.

## <a name="changing-sourceanchor"></a>sourceAnchor 변경
개체에 내보낸 tooAzure AD 이면 경우 허용된 toochange hello sourceAnchor 더 이상 있습니다. Hello 개체에 내보낸된 hello 메타 버스 특성을 수행한 경우 **cloudSourceAnchor** hello로 설정 되어 **sourceAnchor** Azure AD에 의해 허용 되는 값입니다. 경우 **sourceAnchor** 변경 되 고 일치 하지 **cloudSourceAnchor**, hello 규칙 **tooAAD – User Join 아웃** hello 오류를 발생 시킵니다 **sourceAnchor 특성 변경 된**합니다. Hello 구성 또는 데이터를 수정 해야 경우에 동일 하므로 hello sourceAnchor가 다시 hello 메타 버스의 전에 hello 개체를 다시 동기화 할 수 있습니다.

## <a name="additional-resources"></a>추가 리소스
* [Azure AD Connect Sync: 사용자 지정 동기화 옵션](active-directory-aadconnectsync-whatis.md)
* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)

