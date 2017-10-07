---
title: "Azure AD Connect 동기화: hello 기본 구성 이해 | Microsoft Docs"
description: "이 문서에서는 Azure AD Connect 동기화의 기본 구성에서는 hello를 설명 합니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: ed876f22-6892-4b9d-acbe-6a2d112f1cd1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1cf95759af913cad8a1393839d3a836434e7c9bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-hello-default-configuration"></a>Azure AD Connect 동기화: hello 기본 구성 이해
이 문서는 hello의 기본 구성 규칙을 설명합니다. Hello 규칙 및 이러한 규칙 hello 구성에 미치는 영향를 문서화 합니다. 또한 안내 합니다 hello 기본 구성의 Azure AD Connect 동기화 합니다. hello 목표 hello 판독기 hello 구성 모델, 명명 된 선언적 프로비저닝이 실제 예에서 작동 방법을 파악 하는입니다. 이 문서에서는 이미 설치 되어 있는 hello 설치 마법사를 사용 하 여 Azure AD Connect 동기화를 구성 하는 가정 합니다.

hello 구성 모델을 읽을의 toounderstand hello 세부 사항을 [이해 선언적 프로비저닝이](active-directory-aadconnectsync-understanding-declarative-provisioning.md)합니다.

## <a name="out-of-box-rules-from-on-premises-tooazure-ad"></a>온-프레미스 tooAzure AD에서에서의 기본 규칙
hello 다음 식에에서 있습니다 hello 기본적으로 구성 합니다.

### <a name="user-out-of-box-rules"></a>사용자 기본 규칙
이러한 규칙에는 또한 toohello iNetOrgPerson 개체 유형에 적용 됩니다.

사용자 개체 toobe 동기화를 수행 하는 hello를 충족 해야 합니다.

* sourceAnchor가 있어야 합니다.
* Hello 후 개체가 생성 되었음을 Azure AD에서 후 sourceAnchor를 변경할 수 없습니다. Hello 값이 변경 된 온-프레미스 인 경우 hello 개체 중지 동기화 hello sourceAnchor 백 tooits 이전 값을 변경 될 때까지 합니다.
* 가 hello accountEnabled (userAccountControl) 특성 입력 해야 합니다. 온-프레미스 Active Directory를 통해 이 특성은 항상 존재하고 채워집니다.

다음 사용자 개체는 hello는 **하지** tooAzure AD 동기화:

* `IsPresent([isCriticalSystemObject])` Hello 기본 제공 관리자 계정과 같은 Active Directory의 많은 기본 제공 개체 확인, 동기화 되지 않습니다.
* `IsPresent([sAMAccountName]) = False` sAMAccountName 특성이 없는 사용자 개체가 동기화되지 않도록 합니다. 이 경우는 실질적으로 NT4에서 업그레이드된 도메인에 발생합니다.
* `Left([sAMAccountName], 4) = "AAD_"`, `Left([sAMAccountName], 5) = "MSOL_"`. Azure AD Connect 동기화 및 그 이전 버전에서 사용 하는 hello 서비스 계정에 동기화 되지 않습니다.
* Exchange Online에서 작동하지 않는 Exchange 계정을 동기화하지 않습니다.
  * `[sAMAccountName] = "SUPPORT_388945a0"`
  * `Left([mailNickname], 14) = "SystemMailbox{"`
  * `(Left([mailNickname], 4) = "CAS_" && (InStr([mailNickname], "}") > 0))`
  * `(Left([sAMAccountName], 4) = "CAS_" && (InStr([sAMAccountName], "}")> 0))`
* Exchange Online에서 작동하지 않는 개체를 동기화하지 않습니다.
  `CBool(IIF(IsPresent([msExchRecipientTypeDetails]),BitAnd([msExchRecipientTypeDetails],&H21C07000) > 0,NULL))`  
  이 비트 마스크 (& H21C07000)은 다음 개체는 hello 아웃 필터링:
  * 메일 사용 공용 폴더
  * 시스템 도우미 사서함
  * 사서함 데이터베이스 사서함(시스템 사서함)
  * 유니버설 보안 그룹(사용자에 대해 적용하지 않지만 레거시를 지원하기 위해 존재합니다)
  * 비유니버설 그룹(사용자에 대해 적용하지 않지만 레거시를 지원하기 위해 존재합니다)
  * 사서함 계획
  * 검색 사서함
* `CBool(InStr(DNComponent(CRef([dn]),1),"\\0ACNF:")>0)`. 복제 피해 개체를 동기화하지 않습니다.

hello 특성 규칙에 따라 적용 됩니다.

* `sourceAnchor <- IIF([msExchRecipientTypeDetails]=2,NULL,..)` hello sourceAnchor 특성이 연결된 된 사서함에서 제공 되지 않습니다. 연결된 된 사서함을 발견 하는 경우 실제 계정 hello 나중에 가입 되었는지 간주 됩니다.
* Exchange 관련 특성은만 경우 동기화 hello 특성 **mailNickName** 값입니다.
* 여러 포리스트에 사용자가 경우에 특성 순서에 따라 hello에 소비 되며:
  1. Toosign에 관련 된 특성 (예 userPrincipalName)에 대 한 활성화 된 계정으로 hello 포리스트에서 기여 하 합니다.
  2. Exchange 사서함이 있는 hello 포리스트에서 Exchange GAL (전체 주소 목록)에서 찾을 수 있는 특성 기여 하 합니다.
  3. 사서함이 없는 경우 이러한 특성은 포리스트에서 가져올 수 있습니다.
  4. Exchange 관련 특성 (GAL hello에서는 표시 되지 않고 기술 특성) hello 포리스트에서 기여 하 여기서 `mailNickname ISNOTNULL`합니다.
  5. 이러한 규칙 중 하나를 만족 하는 다음 hello 포리스트가 여러 개인 경우 만들기 (날짜/시간) hello 커넥터 (포리스트)의 순서가 사용된 toodetermine 포리스트 hello 특성을 적용 합니다.

### <a name="contact-out-of-box-rules"></a>연락처 기본 규칙
연락처 개체는 다음 동기화 toobe hello를 충족 해야 합니다.

* hello 연락처 메일 사용 가능 해야 합니다. 규칙에 따라 hello로 확인 합니다.
  * `IsPresent([proxyAddresses]) = True)` hello / / proxyAddresses 특성을 채워야 합니다.
  * 기본 전자 메일 주소는 hello / / proxyAddresses 특성 또는 hello 메일 특성에 있습니다. hello의 존재는 @ hello 콘텐츠인지 전자 메일 주소를 사용 하는 tooverify는 합니다. 이 두 가지 규칙 중 하나는 평가 tooTrue 이어야 합니다.
    * `(Contains([proxyAddresses], "SMTP:") > 0) && (InStr(Item([proxyAddresses], Contains([proxyAddresses], "SMTP:")), "@") > 0))` 포함 된 항목을 "SMTP:"가 수 및는 @ hello 문자열에서 찾을 수 있습니까?
    * `(IsPresent([mail]) = True && (InStr([mail], "@") > 0)` 채워진 메일 특성 hello 이며 인 경우이 수는 @ hello 문자열에서 찾을 수 있습니까?

hello 다음 연락처 개체는 **하지** tooAzure AD 동기화:

* `IsPresent([isCriticalSystemObject])` 중요로 표시된 연락처 개체가 동기화되지 않도록 합니다. 기본 구성을 사용하지 않아야 합니다.
* `((InStr([displayName], "(MSOL)") > 0) && (CBool([msExchHideFromAddressLists])))`.
* `(Left([mailNickname], 4) = "CAS_" && (InStr([mailNickname], "}") > 0))`. 해당 개체는 Exchange Online에서 작동하지 않습니다.
* `CBool(InStr(DNComponent(CRef([dn]),1),"\\0ACNF:")>0)`. 복제 피해 개체를 동기화하지 않습니다.

### <a name="group-out-of-box-rules"></a>그룹 기본 규칙
그룹 개체에는 다음 동기화 toobe hello를 충족 해야 합니다.

* 50,000명 미만의 멤버가 있어야 합니다. 이 개수는 hello hello 온-프레미스 그룹의 멤버 수입니다.
  * 가 더 많은 멤버 동기화 hello를 처음으로 시작 하기 전에 hello 그룹 동기화 되지 않습니다.
  * 멤버 수가 hello 처음 만들 때, 다음 중지 될 때까지 hello 구성원 수가 50, 000 보다 낮은 다시 동기화 하는 50, 000 멤버에 도달할 때에서 커지면 합니다.
  * 참고: hello 50000 구성원 수는 또한 Azure AD에 의해 적용 됩니다. 수정 하거나이 규칙을 제거 하는 경우에 더 많은 멤버가 포함 된 그룹 수 toosynchronize 없는 합니다.
* Hello 그룹의 경우는 **메일 그룹**, 메일을 사용할 수 있어야 합니다. 이러한 규칙이 적용되는 데 대해 [연락처 기본 규칙](#contact-out-of-box-rules)을 참조하세요.

다음 그룹 개체는 hello는 **하지** tooAzure AD 동기화:

* `IsPresent([isCriticalSystemObject])` Hello 기본 제공 administrators 그룹과 같은 Active Directory의 많은 기본 제공 개체 확인, 동기화 되지 않습니다.
* `[sAMAccountName] = "MSOL_AD_Sync_RichCoexistence"` DirSync에서 사용하는 레거시 그룹입니다.
* `BitAnd([msExchRecipientTypeDetails],&amp;H40000000)`. 역할 그룹입니다.
* `CBool(InStr(DNComponent(CRef([dn]),1),"\\0ACNF:")>0)`. 복제 피해 개체를 동기화하지 않습니다.

### <a name="foreignsecurityprincipal-out-of-box-rules"></a>ForeignSecurityPrincipal 기본 규칙
Fsp 너무 "any" 조인 된 (\*) hello 메타 버스의 개체입니다. 실제로 이 조인은 사용자 및 보안 그룹의 경우에만 발생합니다. 이 구성을 통해 포리스트 간 멤버 자격을 확인하고 Azure AD에 올바르게 표시합니다.

### <a name="computer-out-of-box-rules"></a>컴퓨터 기본 규칙
컴퓨터 개체는 다음 동기화 toobe hello를 충족 해야 합니다.

* `userCertificate ISNOTNULL` Windows 10 컴퓨터만이 이 특성을 채웁니다. 이 특성의 값을 가진 컴퓨터 개체를 모두 동기화합니다.

## <a name="understanding-hello-out-of-box-rules-scenario"></a>Hello 기본적으로 규칙 시나리오를 이해
이 예제에서 계정 포리스트(A), 리소스 포리스트(R) 및 Azure AD 디렉터리가 각각 하나씩 포함된 배포를 사용합니다.

![시나리오 설명이 있는 그림](./media/active-directory-aadconnectsync-understanding-default-configuration/scenario.png)

이 구성에서는 계정 포리스트 hello에에서 활성화 된 계정이 및 연결 된 사서함이 있는 hello 리소스 포리스트에서 사용할 수 없는 계정을 가정 합니다.

Hello 기본 구성 사용 하 여이 목표가입니다.

* 특성에 대 한 toosign 관련 사용 하도록 설정 하는 hello 계정과 hello 포리스트 로부터 동기화 됩니다.
* Hello GAL (전체 주소 목록)에서 찾을 수 있는 특성 hello 사서함이 있는 hello 포리스트 로부터 동기화 됩니다. 사서함을 찾을 수 없는 경우 다른 포리스트가 사용됩니다.
* 연결된 된 사서함이 없으면 hello 연결 된 계정은 사용 하도록 설정된 해야 찾을 수 hello 개체 내보낸 toobe tooAzure AD.

### <a name="synchronization-rule-editor"></a>동기화 규칙 편집기
hello 구성 확인 및 동기화 규칙 편집기 (SRE) hello 도구를 사용 하 여 변경할 수 및 바로 가기 tooit hello 시작 메뉴에서 찾을 수 있습니다.

![동기화 규칙 편집기 아이콘](./media/active-directory-aadconnectsync-understanding-default-configuration/sre.png)

hello SRE는 리소스 키트 도구와 Azure AD Connect 동기화와 함께 설치 됩니다. toobe 수 toostart, hello ADSyncAdmins 그룹의 구성원 이어야 합니다. 시작할 때 다음과 같이 표시됩니다.

![동기화 규칙 인바운드](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulesinbound.png)

이 창에서 사용자의 구성을 위해 만든 모든 동기화 규칙을 보게 됩니다. Hello 테이블의 각 줄은 하나의 동기화 규칙입니다. 규칙 유형, 두 가지 유형 hello 아래 왼쪽 toohello: 인바운드 및 아웃 바운드. 인바운드 및 아웃 바운드는 hello 메타 버스의 hello 보기. Hello에 진행 중인 toofocus 주로 인바운드이 개요에는 규칙입니다. 동기화 규칙의 실제 목록을 hello AD hello 검색 스키마에 따라 다릅니다. 위 hello 그림에 이러한 서비스에 대 한 hello 계정 포리스트 (fabrikamonline.com) Exchange 및 Lync, 그리고 동기화 규칙 없이 서비스를 모두 만들었습니다. 그러나 hello 리소스 포리스트 (res.fabrikamonline.com)에서 찾았으면 동기화 규칙 이러한 서비스에 대 한 합니다. hello 규칙의 hello 콘텐츠는 검색 hello 버전에 따라 달라 집니다. 예를 들어 Exchange 2013를 사용한 배포에서는 Exchange 2010/2007에서 보다 자세한 특성 흐름이 구성되었습니다.

### <a name="synchronization-rule"></a>동기화 규칙
동기화 규칙은 조건을 만족할 때 흐르는 특성 집합이 포함된 구성 개체입니다. 커넥터 공간에는 개체는 라고 hello 메타 버스의 관련된 tooan 개체 방법을 사용 하는 toodescribe 이기도 **조인** 또는 **일치**합니다. hello 동기화 규칙 tooeach 다른 관계를 나타내는 우선 순위 값이 있어야 합니다. 동기화 규칙에 숫자 값이 낮은 높은 우선 순위의 및 특성 흐름 충돌 하면 더 높은 우선 순위 wins hello 충돌 해결 합니다.

예를 들어 hello 동기화 규칙 확인 **에서 from AD – User AccountEnabled**합니다. Hello SRE에서에서이 줄을 표시 하 고 선택 **편집**합니다.

이 규칙은 기본적으로 규칙 이후에 hello 규칙을 열 때 경고를 받게 됩니다. 확인 해야 [기본 tooout 규칙 변경](active-directory-aadconnectsync-best-practices-changing-default-configuration.md)이므로 의도도 표시할 이란 요청 합니다. 이 경우에 원하는 tooview hello 규칙입니다. **아니오**를 선택합니다.

![동기화 규칙 경고](./media/active-directory-aadconnectsync-understanding-default-configuration/warningeditrule.png)

동기화 규칙에는 설명, 범위 지정 필터, 조인 규칙 및 변환의 네 가지 구성 섹션이 있습니다.

#### <a name="description"></a>설명
hello 첫 번째 섹션 이름, 설명과 같은 기본 정보를 제공 합니다.

![동기화 규칙 편집기의 설명 탭 ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncruledescription.png)

정보에 대 한 개체 유형 hello에는이 규칙은 관련이 있는 연결 된 시스템에 적용 되는 시스템을 연결 및 메타 버스 개체 형식 hello 찾을 수도 있습니다. hello 메타 버스 개체 형식은 hello 소스 개체 유형이 사용자, iNetOrgPerson 또는 연락처 때 사람 관계 없이 항상입니다. hello 메타 버스 개체 형식 때문에 제네릭 형식으로 생성은 변경 하면 안 됩니다. 링크 형식이 hello tooJoin, 스 티 키 조인, 또는 프로 비전 설정할 수 있습니다. 이 설정은 hello 조인 규칙 섹션과 함께 작동 하 고 나중에 적용 됩니다.

또한 이 동기화 규칙이 암호 동기화에 사용됨을 확인할 수 있습니다. 사용자는이 동기화 규칙에 대 한 범위에 있으면 hello 암호가 온-프레미스 toocloud (hello 암호 동기화 기능을 사용 하도록 설정한 경우)에서 동기화 됩니다.

#### <a name="scoping-filter"></a>범위 지정 필터
범위 지정 필터 섹션 hello 사용 되는 tooconfigure 때 동기화 규칙을 적용 해야 합니다. 활성화 된 사용자에 적용 해야 표시 하는 hello 보고 있는 동기화 규칙의 hello 이름, 되므로 hello 범위가 구성 되어 너무 hello AD 특성 **userAccountControl** 해야 하지 hello 비트가 2 설정 합니다. AD에서 사용자를 찾습니다. hello 동기화 엔진을이 동기화 숨겨지거나 표시 규칙 **userAccountControl** 512 (활성화 된 일반 사용자) toohello 10 진수 값으로 설정 되어 있습니다. Hello 사용자에 게 경우 hello 규칙 적용 되지 않습니다 **userAccountControl** too514 설정 (비활성화 된 일반 사용자).

![동기화 규칙 편집기의 범위 지정 탭 ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulescopingfilter.png)

hello 범위 지정 필터에 그룹 및 절을 중첩 될 수 있습니다. 동기화 규칙 tooapply 그룹 내의 모든 절을 충족 합니다. 여러 그룹이 정의 되어 있는 경우 규칙 tooapply hello에 대 한 그룹을 하나 이상 충족 되어야 합니다. 즉, 논리 OR은 그룹들 간에 평가되며 논리 AND는 하나의 그룹 내에서 평가됩니다. 이 구성의 예는 hello에서 확인할 수 있습니다 아웃 바운드 동기화 규칙 **tooAAD – Group Join 아웃**합니다. 예를 들어 몇 가지 동기화 필터 그룹, 보안 그룹에 대한 하나의 필터 그룹(`securityEnabled EQUAL True`) 및 배포 그룹에 대한 하나의 필터 그룹(`securityEnabled EQUAL False`)이 있습니다.

![동기화 규칙 편집기의 범위 지정 탭 ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulescopingfilterout.png)

이 규칙은 사용 되는 toodefine 그룹에 프로 비전 된 tooAzure AD 있어야 합니다. 메일 그룹 메일 사용 가능 toobe Azure AD와 동기화 해야 합니다. 하지만 보안 그룹 메일 필요 하지 않습니다.

#### <a name="join-rules"></a>조인 규칙
hello 세 번째 섹션은 사용 되는 tooconfigure hello 커넥터 공간에 개체 tooobjects hello 메타 버스에 연결 되는 방식입니다. hello 규칙 이전에 보지 못했이 없는 조인 규칙에 대 한 모든 구성을 대신에서 진행 중인 toolook는 **에서 from AD – User Join**합니다.

![동기화 규칙 편집기의 조인 규칙 탭 ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulejoinrules.png)

hello 조인 규칙의 hello 콘텐츠 hello 일치 hello 설치 마법사에서 선택한 옵션에 따라 달라 집니다. 인바운드 규칙에 대 한 hello 평가 hello 원본 커넥터 공간의 개체로 시작 하 고 각 그룹 hello 조인 규칙의 순서 대로 평가 됩니다. 경우 원본 개체는 평가 toomatch 정확히 하나의 개체에 메타 버스 hello 조인 규칙 중 하나를 사용 하 여 hello, hello 개체가 조인 됩니다. 모든 규칙이 평가 되었고 일치 하는 경우 hello 설명 페이지 hello 링크 형식이 사용 됩니다. 이 구성은 너무 설정 되어 있으면**프로 비전**, hello 대상, hello 메타 버스에에서 새 개체가 만들어집니다. 새 개체 toohello 메타 버스는 라고도 너무 tooprovision**프로젝트** 개체 toohello 메타 버스는 합니다.

hello 조인 규칙은 한 번만 계산 됩니다. 커넥터 공간 개체와 메타 버스 개체가 조인 되는 경우은 조인 된 상태로 유지 hello 동기화 규칙의 범위는 hello 계속 충족 됩니다.

동기화 규칙을 평가할 때 정의된 조인 규칙이 포함된 동기화 규칙 하나만이 범위 내에 있어야 합니다. 조인 규칙이 포함된 여러 동기화 규칙이 하나의 개체에 대해 발견되면 오류가 발생합니다. 이러한 이유로 hello 것이 좋습니다 toohave join과 함께 하나의 동기화 규칙 개체에 대 한 범위 내에 동기화 규칙이 여러 개 있는 경우를 정의 합니다. Azure AD Connect 동기화에 대 한 hello의 기본 구성에서는 이러한 규칙 hello 이름을 확인 하 여 찾을 수 하 고 찾을 수 있는 hello 단어 **조인** hello hello 이름 끝에 있습니다. 조인 규칙이 정의 없이 동기화 규칙 다른 동기화 규칙 hello 개체를 함께 조인 또는 hello 대상에서 새 개체를 프로 비전 하는 경우 hello 특성 흐름을 적용 합니다.

위 hello 그림을 보면 해당 hello 규칙 toojoin 시도 볼 수 있습니다 **objectSID** 와 **msExchMasterAccountSid** (교환) 및 **msRTCSIP OriginatorSid** 드 ( Lync). 즉, 계정-리소스 포리스트 토폴로지에서 기대한 것입니다. Hello 찾을 포리스트 전반에 동일한 규칙입니다. hello 가정은 모든 포리스트에 계정 또는 리소스 포리스트를 수입니다. 이 구성 하는 단일 포리스트에 거주 하 고 toobe 가입 하지 않은 경우에 작동 합니다.

#### <a name="transformations"></a>변환
hello 변환 섹션 hello 개체를 조인 하 고 충족 하는 hello 범위 필터가 때 toohello 대상 개체를 적용 하는 모든 특성 흐름을 정의 합니다. Toohello를 다시 살펴보자면 **에서 from AD – User AccountEnabled** 변환을 수행 하는 hello 찾을 동기화 규칙:

![동기화 규칙 편집기의 변환 탭 ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncruletransformations.png)

tooput Exchange 및 Lync 설정을 사용 하 여 계정 포리스트 hello에에서 활성화 된 계정이 및 hello 리소스에서 사용할 수 없는 계정 포리스트 예상된 toofind 것이 컨텍스트에 계정-리소스 포리스트 배포에서이 구성 합니다. 로그인에 필요한 hello 특성을 포함 하는 동기화 규칙에서 원하는 hello 및 hello 포리스트에서 이러한 특성이 흘러 야 활성화 된 계정이 있는 합니다. 이러한 모든 특성 흐름은 하나의 동기화 규칙에 함께 배치됩니다.

변환은 다른 형식을 가질 수 있습니다: 상수, 직접 및 식.

* 일정한 흐름은 항상 하드 코딩된 값을 전달합니다. 위의 hello 경우 항상로 설정 hello 값 **True** 라는 hello 메타 버스 특성에 **accountEnabled**합니다.
* 직접 흐름은 항상 hello hello 소스 toohello 대상 특성으로 hello 특성 값을 전달-됩니다.
* hello 세 번째 흐름 형식은 식이 며 고급 구성에 대 한 허용 합니다.

hello 식 언어는 VBA (Visual Basic의 경우 응용 프로그램에 대 한) 이므로 Microsoft Office를 사용한 경험이 있는 사용자 또는 VBScript hello 형식을 인식 하는입니다. 특성은 대괄호로 묶입니다(예: [attributeName]). 특성 이름과 함수 이름은 대/소문자, 하지만 hello 동기화 규칙 편집기 hello 식을 계산 하 고 hello 식이 유효 하지 않을 경우 경고를 제공 합니다. 모든 표현식은 함수가 중첩된 단일 행으로 표현됩니다. tooshow hello 전원 hello 구성 언어의 흐름은 다음과 같습니다 hello pwdlastset, 하지만 추가 주석이 삽입:

```
// If-then-else
IIF(
// (hello evaluation for IIF) Is hello attribute pwdLastSet present in AD?
IsPresent([pwdLastSet]),
// (hello True part of IIF) If it is, then from right tooleft, convert hello AD time format tooa .Net datetime, change it toohello time format used by Azure AD, and finally convert it tooa string.
CStr(FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")),
// (hello False part of IIF) Nothing toocontribute
NULL
)
```

참조 [선언적 프로비저닝 식 이해](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) hello 식 언어 특성 흐름에 대 한 자세한 내용은 합니다.

### <a name="precedence"></a>우선 순위
이제 몇 가지 개별 동기화 규칙에 보지 못했을 있습니다 하지만 hello 규칙 hello 구성에서 함께 작동 합니다. 경우에 따라 특성 값에서 여러 동기화 규칙 toohello 제공 동일한 대상 특성입니다. 이 경우 특성 우선 순위에는 사용 되는 toodetermine wins는 특성입니다. 예를 들어 hello 특성 sourceAnchor를 살펴봅니다. 이 특성은 tooAzure AD에에서는 중요 한 특성 toobe 수 toosign입니다. **AD에서 들어오기 – 사용자 AccountEnabled** 및 **AD에서 들어오기 – 사용자 공통**이라는 다른 두 가지 동기화 규칙에서 이 특성에 대한 특성 흐름에 찾을 수 있습니다. TooSynchronization 규칙 우선 순위 인해 hello sourceAnchor 특성이 제공 활성화 된 계정으로 hello 포리스트에서 먼저 여러 개체에 가입된 toohello 메타 버스 개체에 있는 경우. 활성화 된 계정이 없으면 있으면 hello 동기화 엔진이 사용 하는 포괄적인 동기화 규칙 hello **에서 from AD – User Common**합니다. 이 구성은 비활성화된 계정에 대해서도 여전히 sourceAnchor가 있다는 것을 확인합니다.

![동기화 규칙 인바운드](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulesinbound.png)

동기화 규칙에 대 한 hello 우선 순위는 hello 설치 마법사가 그룹에서 설정 됩니다. 모든 규칙 그룹에 있는 hello 있지만 이름이 같은 연결 된 toodifferent 연결 된 디렉터리입니다. hello 설치 마법사는 hello 규칙을 제공 **에서 from AD – User Join** 가장 높은 우선 순위 이므로 모든 조치 연결 AD 디렉터리 반복 합니다. 그런 다음 hello 다음 규칙 그룹에 미리 정의 된 순서에 따라 계속 됩니다. 그룹 내의 hello 규칙 커넥터 hello 마법사에서 추가 된 hello 순서 hello에 추가 됩니다. 다른 커넥터 hello 마법사를 통해 추가 되 면 hello 동기화 규칙은 다시 정렬 하 고 hello 새 커넥터의 규칙이 각 그룹의 마지막 삽입 됩니다.

### <a name="putting-it-all-together"></a>모든 항목 요약
동기화 규칙 toobe 수 toounderstand hello 구성 hello 작동 하는 방법에 대해 충분히 알고 이제 다른 동기화 규칙입니다. 보면 특성을 한 사용자 및 hello toohello 메타 버스를 제공, hello 규칙 hello 순서에 따라 적용 됩니다.

| 이름 | 주석 |
|:--- |:--- |
| AD에서 들어오기 – 사용자 조인 |메타버스를 사용하여 커넥터 공간 개체에 조인시키기 위한 규칙. |
| AD에서 들어오기 – 사용하도록 설정된 UserAccount |로그인 tooAzure AD 및 Office 365에 대 한 필수 특성입니다. 이러한 특성을 사용 하도록 설정 하는 hello 계정에서 사용 하는 것이 좋습니다. |
| AD에서 들어오기 – Exchange에서 사용자 공통 |Hello 전체 주소 목록에서에서 발견 된 특성입니다. Hello 사용자의 사서함을 발견 하는 hello 포리스트에 hello 데이터 품질은 가장 가정 합니다. |
| AD에서 들어오기 – 사용자 공통 |Hello 전체 주소 목록에서에서 발견 된 특성입니다. 사서함을 발견 하지 않은 경우 조인 된 다른 개체가 hello 특성 값을 제공할 수 있습니다. |
| AD에서 들어오기 – 사용자 Exchange |Exchange가 감지되는 경우에만 존재합니다. 인프라 Exchange 특성을 전송합니다. |
| AD에서 들어오기 – 사용자 Lync |Lync가 감지되는 경우에만 존재합니다. 모든 인프라 Lync 특성을 전송합니다. |

## <a name="next-steps"></a>다음 단계
* Hello 구성 모델에 대해 자세히 읽어보세요 [이해 선언적 프로비저닝이](active-directory-aadconnectsync-understanding-declarative-provisioning.md)합니다.
* Hello 식 언어에 대 한 자세한 설명 [선언적 프로비저닝 식 이해](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)합니다.
* Hello의 기본 구성에서 작동 하는 방법을 읽고 [사용자 및 연락처 이해](active-directory-aadconnectsync-understanding-users-and-contacts.md)
* 선언적 프로비저닝을 사용 하 여 실제 toomake을 변경 하는 방법을 확인할 [어떻게 변경 toohello toomake 기본 구성을](active-directory-aadconnectsync-change-the-configuration.md)합니다.

**개요 항목**

* [Azure AD Connect 동기화: 동기화의 이해 및 사용자 지정](active-directory-aadconnectsync-whatis.md)
* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)

