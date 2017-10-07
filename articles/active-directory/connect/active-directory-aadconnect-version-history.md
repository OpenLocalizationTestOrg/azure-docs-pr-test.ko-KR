---
title: "Azure AD Connect: 버전 릴리스 내역 | Microsoft Docs"
description: "이 문서에는 Azure AD Connect 및 Azure AD Sync의 모든 릴리스가 나열되어 있습니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: ef2797d7-d440-4a9a-a648-db32ad137494
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b55e0f2d426e34ceef9869d5a6d1b0956d8bd076
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-version-release-history"></a>Azure AD Connect: 버전 릴리스 내역
hello Azure Active Directory (Azure AD) 팀은 정기적으로 새로운 특징과 기능으로 Azure AD Connect를 업데이트합니다. 적용 가능한 tooall 대상은 일부 추가 있습니다.

이 문서는 디자인 된 toohelp 출시 된 hello 버전의 추적할 수 및 toounderstand tooupdate toohello 최신 버전이 필요 여부.

다음은 관련 항목 목록입니다.


항목 |  세부 정보
--------- | --------- |
Azure AD Connect에서 단계 tooupgrade | 다양 한 방법을 너무[는 이전 버전 toohello 최신 버전에서 업그레이드](active-directory-aadconnect-upgrade-previous-version.md) Azure AD Connect 릴리스 합니다.
필요한 사용 권한 | 사용 권한 업데이트 tooapply를 필요한 참조 [계정 및 권한](./active-directory-aadconnect-accounts-permissions.md#upgrade)합니다.
다운로드| [Azure AD Connect 다운로드](http://go.microsoft.com/fwlink/?LinkId=615771).

## <a name="115610"></a>1.1.561.0
상태: 2017년 7월 23일

### <a name="azure-ad-connect"></a>Azure AD Connect

#### <a name="fixed-issue"></a>해결된 문제

* 기본 제공 동기화 규칙 hello를 발생 시킨 문제가 해결 되었습니다. "Out tooAD-사용자 ImmutableId" toobe 제거:

  * Azure AD Connect를 업그레이드 하는 경우 hello 문제가 발생 또는 때 작업 옵션을 환영 *업데이트 동기화 구성은* hello Azure AD Connect에서에서 마법사가 사용 되는 tooupdate Azure AD Connect 동기화 구성.
  
  * 이 동기화 규칙은 적용 가능한 toocustomers hello 설정한 [원본 앵커 기능으로 게스트가 ConsistencyGuid](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor)합니다. 이 기능은 1.1.524.0 이후 버전에서 도입되었습니다. Azure AD Connect는 온-프레미스 hello 동기화 규칙을 제거할 때 채울 더 이상 수 hello ObjectGuid 특성 값을 사용 하 여 AD ms-DS-ConsistencyGuid 특성입니다. 새 사용자가 Azure AD에 프로비전되지 않도록 방지하지 않습니다.
  
  * hello 수정 hello 기능이 사용 하도록 설정으로 해당 hello 동기화 규칙이 업그레이드 하는 동안 또는 구성 변경 중에 더 이상 제거할 수를 확인 합니다. 이 문제의 영향을 받은 사용자는 기존 고객에 대 한 hello 수정 갖는지도 toothis 버전의 Azure AD Connect 업그레이드 한 후 다시 해당 hello 동기화 규칙이 추가 됩니다.

* 기본 제공 동기화 규칙으로 인해가 100 보다 작은 toohave 우선 순위 값 하는 문제가 수정 되었습니다.

  * 일반적으로 사용자 지정 동기화 규칙에 대한 우선 순위 값은 0	~99로 예약됩니다. 업그레이드 하는 동안 기본 제공 동기화 규칙에 대 한 hello 우선 순위 값에는 업데이트 된 tooaccommodate 동기화 규칙이 변경 되더라도입니다. Toothis 문제로 인해 기본 제공 동기화 규칙 우선 순위 값을 100 보다 작은 할당할 수 있습니다.
  
  * 업그레이드 하는 동안 발생 hello 문제를 방지 하는 hello 수정 합니다. 그러나 hello 문제의 영향을 받은 기존 고객에 대 한 hello 우선 순위 값 복원 하지 않습니다. 별도 수정으로 hello 복원 이후 toohelp hello에에서 제공 됩니다.

* 문제가 해결 되었습니다. 여기서 hello [도메인 및 OU 필터링 화면](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) hello Azure AD Connect 마법사 표시 되어 *모든 도메인 및 Ou를 동기화* OU 기반 필터링을 사용 하는 경우에, 선택 된 것으로 옵션입니다.

*   문제가 해결 되었습니다. 해당 않아 hello [디렉터리 파티션 구성 화면](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) hello 동기화 서비스 관리자 tooreturn 오류가 경우 hello에 *새로 고침* 단추를 클릭 합니다. hello 오류 메시지는 *"도메인을 새로 고치는 동안 오류가 발생 했습니다: 'System.Collections.ArrayList' tootype 형식의 수 없습니다 toocast 개체 ' Microsoft.DirectoryServices.MetadirectoryServices.UI.PropertySheetBase.MaPropertyPages.PartitionObject입니다. "* hello 때 오류가 발생 새 AD 도메인 tooan 기존 AD 포리스트에 추가 되 고 고치려는 tooupdate Azure AD Connect를 사용 하 여 새로 고침 단추를 hello 합니다.

#### <a name="new-features-and-improvements"></a>새로운 기능 및 향상 기능

* [자동 업그레이드 기능](active-directory-aadconnect-feature-automatic-upgrade.md) 하는 구성을 따르고 hello로 확장된 toosupport 고객 되었습니다:
  * Hello 장치 쓰기 저장 기능을 사용 하도록 설정한 합니다.
  * Hello 그룹 쓰기 저장 기능을 사용 하도록 설정한 합니다.
  * hello 설치가 기본 설정을 또는 DirSync 업그레이드 되지 않습니다.
  * Hello 메타 버스의 100, 000 개 이상의 개체를가지고 있습니다.
  * 한 포리스트의 보다 toomore를 연결 됩니다. 빠른 설치만 tooone 포리스트를 연결 합니다.
  * AD 커넥터 계정 hello hello 기본 MSOL_ 계정 더 이상입니다.
  * hello 서버 준비 모드 toobe를 설정 되어 있습니다.
  * Hello 사용자 쓰기 저장 기능을 사용 하도록 설정한 합니다.
  
  >[!NOTE]
  >자동 업그레이드 기능 hello hello 범위 확장 후 Azure AD Connect 빌드 1.1.105.0와 고객을 영향을 줍니다. Azure AD Connect 서버에서 다음 cmdlet 실행 해야 하는 경우 자동으로 업그레이드 하 여 Azure AD Connect 서버 toobe 하지 않으려면: `Set-ADSyncAutoUpgrade -AutoUpgradeState disabled`합니다. 설정/해제 자동 업그레이드 하는 방법에 대 한 자세한 내용은 참조 tooarticle [Azure AD Connect: 자동 업그레이드](active-directory-aadconnect-feature-automatic-upgrade.md)합니다.

## <a name="115580"></a>1.1.558.0
상태: 릴리스되지 않았습니다. 이 빌드의 변경 내용은 1.1.561.0 버전에 포함됩니다.

### <a name="azure-ad-connect"></a>Azure AD Connect

#### <a name="fixed-issue"></a>해결된 문제

* Hello 기본 제공 동기화 규칙 "아웃 tooAD-사용자 ImmutableId"를 발생 시킨 문제가 해결 되었습니다. toobe 될 때 제거 OU 기반 필터링 구성 업데이트 됩니다. 이 동기화 규칙은 hello에 대 한 필수 [원본 앵커 기능으로 게스트가 ConsistencyGuid](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor)합니다.

* 문제가 해결 되었습니다. 여기서 hello [도메인 및 OU 필터링 화면](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) hello Azure AD Connect 마법사 표시 되어 *모든 도메인 및 Ou를 동기화* OU 기반 필터링을 사용 하는 경우에, 선택 된 것으로 옵션입니다.

*   문제가 해결 되었습니다. 해당 않아 hello [디렉터리 파티션 구성 화면](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) hello 동기화 서비스 관리자 tooreturn 오류가 경우 hello에 *새로 고침* 단추를 클릭 합니다. hello 오류 메시지는 *"도메인을 새로 고치는 동안 오류가 발생 했습니다: 'System.Collections.ArrayList' tootype 형식의 수 없습니다 toocast 개체 ' Microsoft.DirectoryServices.MetadirectoryServices.UI.PropertySheetBase.MaPropertyPages.PartitionObject입니다. "* hello 때 오류가 발생 새 AD 도메인 tooan 기존 AD 포리스트에 추가 되 고 고치려는 tooupdate Azure AD Connect를 사용 하 여 새로 고침 단추를 hello 합니다.

#### <a name="new-features-and-improvements"></a>새로운 기능 및 향상 기능

* [자동 업그레이드 기능](active-directory-aadconnect-feature-automatic-upgrade.md) 하는 구성을 따르고 hello로 확장된 toosupport 고객 되었습니다:
  * Hello 장치 쓰기 저장 기능을 사용 하도록 설정한 합니다.
  * Hello 그룹 쓰기 저장 기능을 사용 하도록 설정한 합니다.
  * hello 설치가 기본 설정을 또는 DirSync 업그레이드 되지 않습니다.
  * Hello 메타 버스의 100, 000 개 이상의 개체를가지고 있습니다.
  * 한 포리스트의 보다 toomore를 연결 됩니다. 빠른 설치만 tooone 포리스트를 연결 합니다.
  * AD 커넥터 계정 hello hello 기본 MSOL_ 계정 더 이상입니다.
  * hello 서버 준비 모드 toobe를 설정 되어 있습니다.
  * Hello 사용자 쓰기 저장 기능을 사용 하도록 설정한 합니다.
  
  >[!NOTE]
  >자동 업그레이드 기능 hello hello 범위 확장 후 Azure AD Connect 빌드 1.1.105.0와 고객을 영향을 줍니다. Azure AD Connect 서버에서 다음 cmdlet 실행 해야 하는 경우 자동으로 업그레이드 하 여 Azure AD Connect 서버 toobe 하지 않으려면: `Set-ADSyncAutoUpgrade -AutoUpgradeState disabled`합니다. 설정/해제 자동 업그레이드 하는 방법에 대 한 자세한 내용은 참조 tooarticle [Azure AD Connect: 자동 업그레이드](active-directory-aadconnect-feature-automatic-upgrade.md)합니다.

## <a name="115570"></a>1.1.557.0
상태: 2017년 7월

>[!NOTE]
>이 빌드 hello Azure AD 연결 자동 업그레이드 기능을 통해 사용할 수 있는 toocustomers 아닙니다.

### <a name="azure-ad-connect"></a>Azure AD Connect

#### <a name="fixed-issue"></a>해결된 문제
* Initialize ADSyncDomainJoinedComputerSync hello cmdlet hello 기존 서비스 연결 지점 개체 toobe 변경할 경우에 여전히 유효한 도메인에 구성 된 hello 확인 된 도메인이 발생 시킨 문제가 해결 되었습니다. 이 문제는 Azure AD 테 넌 트 hello 서비스 연결 지점을 구성 하는 데 사용할 수 있는 둘 이상의 확인 된 도메인에 있을 때 발생 합니다.

#### <a name="new-features-and-improvements"></a>새로운 기능 및 향상 기능
* 이제 비밀번호 쓰기 저장이 Microsoft Azure Government 클라우드 및 Microsoft Cloud Germany에서 미리 보기로 제공됩니다. 다른 서비스 인스턴스로 hello에 대 한 Azure AD Connect 지원에 대 한 자세한 내용은 참조 tooarticle [Azure AD Connect:에 대 한 특별 고려 사항 인스턴스](active-directory-aadconnect-instances.md)합니다.

* Initialize ADSyncDomainJoinedComputerSync hello cmdlet에는 이제 AzureADDomain 라는 새로운 선택적 매개 변수는에 있습니다. 이 매개 변수를 사용 하면 도메인 toobe hello 서비스 연결 지점을 구성 하는 데 사용 되는 확인 하 지정할 수 있습니다.

### <a name="pass-through-authentication"></a>통과 인증

#### <a name="new-features-and-improvements"></a>새로운 기능 및 향상 기능
* hello 에이전트에서 변경 된 통과 인증에 필요한 hello 이름 *Microsoft Azure AD 응용 프로그램 프록시 커넥터* 너무*Microsoft Azure AD Connect 인증 Agent*합니다.

* 통과 인증을 사용하도록 설정하면 기본적으로 암호 해시 동기화가 더 이상 활성화되지 않습니다.


## <a name="115530"></a>1.1.553.0
상태: 2017년 6월

> [!IMPORTANT]
> 이 빌드에서는 스키마 및 동기화 규칙이 변경되었습니다. Azure AD Connect 동기화 서비스는 업그레이드 후에 전체 가져오기 및 전체 동기화 단계를 트리거합니다. Hello 변경 내용의 세부 정보에 대 한 설명은 다음과 같습니다. tootemporarily 업그레이드 후 전체 가져오기 및 전체 동기화 단계 연기, tooarticle 참조 [어떻게 toodefer 전체 업그레이드 후 동기화](active-directory-aadconnect-upgrade-previous-version.md#how-to-defer-full-synchronization-after-upgrade)합니다.
>
>

### <a name="azure-ad-connect-sync"></a>Azure AD Connect 동기화

#### <a name="known-issue"></a>알려진 문제
* Azure AD Connect 동기화와 함께 [OU 기반 필터링](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering)을 사용하는 고객에게 영향을 주는 문제가 있습니다. Toohello를 탐색 하는 경우 [도메인 및 OU 필터링 페이지](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) hello Azure AD Connect 마법사의 동작을 수행 하는 hello 사용할 수 있습니다.
  * OU 기반 필터링을 사용 하는 경우 hello **선택한 도메인 및 Ou 동기화** 옵션을 선택 합니다.
  * 그렇지 않으면 hello **모든 도메인 및 Ou 동기화** 옵션을 선택 합니다.

hello 발생 하는 문제는 해당 hello **모든 도메인 및 Ou 옵션 동기화** hello 마법사를 실행할 때 항상 선택 됩니다.  이 문제는 OU 기반 필터링이 이전에 구성된 경우에도 발생합니다. AAD Connect 구성 변경 내용을 저장 하기 전에 hello 있는지를 확인 **Ou 옵션을 선택 및 선택한 도메인 동기화** toosynchronize 해야 하는 모든 Ou 다시 설정 되어 있는지 확인 합니다. 그렇지 않으면 OU 기반 필터링이 비활성화됩니다.

#### <a name="fixed-issues"></a>해결된 문제

* 문제가 해결 되었습니다. 암호 쓰기 저장 온-프레미스의 hello 암호는 Azure AD 관리자 tooreset 수 있도록와 AD 권한 있는 사용자 계정입니다. Azure AD Connect hello 특권 계정을 hello 암호 재설정 권한이 부여 된 hello 문제가 발생 합니다. hello 문제는이 버전의 Azure AD Connect 임의의 온-프레미스의 hello 암호는 Azure AD 관리자 tooreset를 허용 하지 않음으로써 AD 권한 있는 사용자 계정 관리자에 게는 해당 계정의 hello 소유자 하지 않는 한 합니다. 자세한 내용은 참조 너무[보안 권고 4033453](https://technet.microsoft.com/library/security/4033453)합니다.

* 관련 된 문제가 해결 되었습니다. toohello [원본 앵커로 게스트가 ConsistencyGuid](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor) 기능은 Azure AD Connect가 쓰기 저장 tooon-프레미스가 아니라 AD 게스트가 ConsistencyGuid 특성입니다. hello 문제가 있을 때 발생 여러 온-프레미스 AD 포리스트 추가 tooAzure AD 연결 및 hello *사용자 id가 여러 디렉터리 옵션* 을 선택 합니다. 이러한 구성을 사용 하면 hello 결과 동기화 규칙은 hello sourceAnchorBinary 특성 hello 메타 버스에에서 채우지 않습니다. hello sourceAnchorBinary 특성 게스트가 ConsistencyGuid 특성에 대 한 hello 원본 특성으로 사용 됩니다. 결과적으로, 쓰기 저장 toohello ms DSConsistencyGuid 특성 발생 하지 않습니다. 다음 동기화 규칙이 toofix hello 문제 hello sourceAnchorBinary 특성 메타 버스 항상 채워진 hello에 업데이트 된 tooensure 되었습니다.
  * In from AD - InetOrgPerson AccountEnabled.xml
  * In from AD - InetOrgPerson Common.xml
  * In from AD - User AccountEnabled.xml
  * In from AD - User Common.xml
  * In from AD - User Join SOAInAAD.xml

* 포함 하 여 이전에 경우 hello [원본 앵커로 게스트가 ConsistencyGuid](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor) 기능을 활성화 하지 않으면 hello tooAD 사용자 ImmutableId"Out" 동기화 규칙은 AD tooAzure 추가 여전히 연결 합니다. hello 효과 심각 하지는 및 게스트가 ConsistencyGuid 특성 toooccur의 쓰기 저장이 발생 하지 않습니다. tooavoid 혼동 동기화 규칙 hello tooensure hello 기능이 설정 된 경우에 추가 됩니다 논리가 추가 되었습니다.

* 암호 해시 동기화 toofail 611 오류 이벤트를 발생 시킨 문제를 해결 합니다. 이 문제는 온-프레미스 AD에서 하나 이상의 도메인 컨트롤러가 제거된 후에 발생합니다. 각 암호 동기화 주기 hello 끝 hello 동기화 쿠키를 발급 하 여 온-프레미스 AD USN (업데이트 시퀀스 번호) 값이 0 인 제거 hello 도메인 컨트롤러의 호출 Id를 포함 합니다. hello 암호 동기화 관리자 0 없습니다 toopersist 동기화 쿠키 포함 USN 값 이며 611 오류 이벤트와 함께 실패 합니다. Hello 다음 동기화 중 주기, 암호 동기화 관리자 다시 사용 hello 마지막 지속형된 동기화 쿠키의 USN 값이 0 포함 하지 않는 hello 합니다. 이 인해 hello 동일 하 게 암호 변경 toobe 다시 동기화 합니다. 이 수정 프로그램을 암호 동기화 관리자 hello 올바르게 동기화 쿠키의 hello를 유지합니다.

* 이전에 자동 업그레이드 해제 된 hello 집합 ADSyncAutoUpgrade cmdlet을 사용 하는 경우에 자동 업그레이드 프로세스 hello toocheck 업그레이드에 대 한 정기적으로, 계속 및 hello 다운로드 한 설치 관리자 toohonor 사용할 수 없는 상태에 의존 합니다. 이 해결 방법을 hello 자동 업그레이드 프로세스가 더 이상 업그레이드에 대 한 주기적으로 검사 합니다. hello 수정이 Azure AD Connect 버전에 대 한 업그레이드 설치 관리자를 한 번 실행 될 때 자동으로 적용 됩니다.

#### <a name="new-features-and-improvements"></a>새로운 기능 및 향상 기능

* 이전에 hello [원본 앵커로 게스트가 ConsistencyGuid](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor) 기능을 사용할 수 있는 toonew 배포만 합니다. 이제, 사용 가능한 tooexisting 배포입니다. 더 구체적으로 살펴보면 다음과 같습니다.
  * tooaccess 기능 hello hello Azure AD Connect 마법사를 시작 하 고 hello 선택 *업데이트 원본 앵커* 옵션입니다.
  * 이 옵션은 objectGuid sourceAnchor 특성으로 사용 하는 표시 tooexisting 배포만 있습니다.
  * Hello 옵션을 구성할 때 hello 마법사는 온-프레미스 Active Directory에 hello 게스트가 ConsistencyGuid 특성의 hello 상태를 확인 합니다. Hello 디렉터리에서 사용자 개체에 hello 특성이 구성 되지 않으면 hello 마법사 hello 게스트가 ConsistencyGuid hello sourceAnchor 특성으로 사용 합니다. Hello 디렉터리에 하나 이상의 사용자 개체에 hello 특성은 구성 된 경우 다른 응용 프로그램에서 사용 되 고 및 sourceAnchor 특성으로 적합 하지 않은 고 hello 원본 앵커 변경 tooproceed를 허용 하지 않는 hello 특성 hello 마법사 완료 됩니다. 인 경우 해당 hello 특성은 기존 응용 프로그램에 사용 되지 않는 특정 toosuppress 오류 hello 하는 방법에 대 한 내용은 toocontact 지원 해야 합니다.

* 특정 너무**userCertificate** 인증서 값에 필요한 장치 개체, Azure AD Connect 이제 특성 찾습니다 [연결 Windows 10 경험에 대 한 AD 도메인에 가입 된 장치 tooAzure](https://docs.microsoft.com/azure/active-directory/active-directory-azureadjoin-devices-group-policy) 및 hello rest tooAzure AD를 동기화 하기 전에 필터링 합니다. tooenable이이 동작을 "tooAAD-Out 장치 Join SOAInAD" hello 기본 제공 동기화 규칙 업데이트 되었습니다.

* Exchange Online의 azure AD Connect 지금은 지원 writeback **cloudPublicDelegates** 특성 tooon 온-프레미스 AD **publicDelegates** 특성입니다. 따라서 여기서는 Exchange Online 사서함 부여할 수 온-프레미스 Exchange 사서함이 있는 SendOnBehalfTo 권한 toousers hello 시나리오를 수 있습니다. toosupport이이 기능, tooAD Exchange 하이브리드 PublicDelegates 사용자 쓰기 저장"Out" 새 기본 제공 동기화 규칙 추가 되었습니다. 이 동기화 규칙은 AD tooAzure 추가 Exchange 하이브리드 기능을 사용할 수 있는 경우 연결 합니다.

*   Azure AD Connect에서 지 원하는 hello 동기화 **altRecipient** Azure AD에서 특성입니다. 기본 제공 동기화 규칙에 따라이 변경 된 toosupport tooinclude hello 필요한 특성 흐름 업데이트:
  * AD에서 들어오기 – 사용자 Exchange
  * TooAAD – 사용자 ExchangeOnline 아웃
  
* hello **cloudSOAExchMailbox** hello 메타 버스 특성 지정된 된 사용자 또는 Exchange Online 사서함에 있는지 여부를 나타냅니다. 정의 업데이트 tooinclude 되었으면 이러한 장비 및 회의실 사서함으로 Exchange Online RecipientDisplayTypes 추가 합니다. tooenable이이 변경의 기본 제공 동기화 규칙 "에서 AAD – 사용자 Exchange 하이브리드", 아래에서 액세스할 수 있는 hello cloudSOAExchMailbox 특성의 hello 정의에서 업데이트 되었습니다.

```
CBool(IIF(IsNullOrEmpty([cloudMSExchRecipientDisplayType]),NULL,BitAnd([cloudMSExchRecipientDisplayType],&amp;HFF) = 0))
```

... toohello 다음:

```
CBool(
  IIF(IsPresent([cloudMSExchRecipientDisplayType]),(
    IIF([cloudMSExchRecipientDisplayType]=0,True,(
      IIF([cloudMSExchRecipientDisplayType]=2,True,(
        IIF([cloudMSExchRecipientDisplayType]=7,True,(
          IIF([cloudMSExchRecipientDisplayType]=8,True,(
            IIF([cloudMSExchRecipientDisplayType]=10,True,(
              IIF([cloudMSExchRecipientDisplayType]=16,True,(
                IIF([cloudMSExchRecipientDisplayType]=17,True,(
                  IIF([cloudMSExchRecipientDisplayType]=18,True,(
                    IIF([cloudMSExchRecipientDisplayType]=1073741824,True,(
                       IF([cloudMSExchRecipientDisplayType]=1073741840,True,False)))))))))))))))))))),False))

```

* 추가 된 hello 다음 X509Certificate2 호환 함수 hello userCertificate 특성 동기화 규칙 식 toohandle 인증서 값을 만들기 위한 설정 합니다.

    ||||
    | --- | --- | --- |
    |CertSubject|CertIssuer|CertKeyAlgorithm|
    |CertSubjectNameDN|CertIssuerOid|CertNameInfo|
    |CertSubjectNameOid|CertIssuerDN|IsCert|
    |CertFriendlyName|CertThumbprint|CertExtensionOids|
    |CertFormat|CertNotAfter|CertPublicKeyOid|
    |CertSerialNumber|CertNotBefore|CertPublicKeyParametersOid|
    |CertVersion|CertSignatureAlgorithmOid|여기서|
    |CertKeyAlgorithmParams|CertHashString|Where|
    |||With|

* 다음 스키마 변경 내용이 도입 된 tooallow 고객 toocreate 사용자 지정 동기화 규칙 tooflow sAMAccountName, domainNetBios, 및 그룹 개체에 대 한 domainFQDN와 사용자 개체에 대 한 고유 이름 되었습니다.

  * 다음과 같은 특성이 tooMV 스키마를 추가 되었습니다.
    * 그룹: AccountName
    * 그룹: domainNetBios
    * 그룹: domainFQDN
    * 사용자: distinguishedName

  * AD 커넥터 스키마 tooAzure 다음과 같은 특성이 추가 되었습니다.
    * 그룹: OnPremisesSamAccountName
    * 그룹: NetBiosName
    * 그룹: DnsDomainName
    * 사용자: OnPremisesDistinguishedName

* hello ADSyncDomainJoinedComputerSync cmdlet 스크립트 AzureEnvironment 라는 새로운 선택적 매개 변수가 되었습니다. hello 매개 변수는 사용 되는 toospecify 어떤 영역 hello 해당 Azure Active Directory 테 넌 트에 호스팅됩니다. 유효한 값은 다음과 같습니다.
  * AzureCloud(기본값)
  * AzureChinaCloud
  * AzureGermanyCloud
  * USGovernment
 
* 업데이트 된 동기화 규칙 편집기 toouse (준비) 하는 대신 동기화 규칙을 만드는 중 연결 형식의 hello 기본값 조인 합니다.

### <a name="ad-fs-management"></a>AD FS 관리

#### <a name="issues-fixed"></a>해결된 문제

* Url 다음 Azure AD tooimprove 시에도 인증 중단으로 인해 새 Ws-federation 끝점 하며 추가 tooon 온-프레미스 AD FS 신뢰 당사자 구성이 회신:
  * https://ests.login.microsoftonline.com/login.srf
  * https://stamp2.login.microsoftonline.com/login.srf
  * https://ccs.login.microsoftonline.com/login.srf
  * https://ccs-sdf.login.microsoftonline.com/login.srf
  
* IssuerID에 대 한 AD FS toogenerate 잘못 된 클레임 값 발생 시킨 문제를 해결 합니다. hello 문제 발생 hello Azure AD 테 넌 트 및 hello userPrincipalName 특성을 사용한 toogenerate hello 도메인 접미사가 확인 된 도메인을 여러 개 있는 경우 클레임은 적어도 IssuerID hello 3-수준 전체 (예를 들어 johndoe@us.contoso.com). hello 클레임 규칙에서 사용 하는 hello regex를 업데이트 하 여 hello 문제가 해결 됩니다.

#### <a name="new-features-and-improvements"></a>새로운 기능 및 향상 기능
* 이전에 Azure AD Connect에서 제공 하는 hello ADFS 인증서 관리 기능의와 Azure AD Connect를 통해 관리 되는 ad FS 팜만 사용할 수 있습니다. 이제 Azure AD Connect를 사용 하 여 관리 되지 않는 ad FS 팜 사용 hello 기능을 사용할 수 있습니다.

## <a name="115240"></a>1.1.524.0
릴리스 날짜: 2017년 5월

> [!IMPORTANT]
> 이 빌드에서는 스키마 및 동기화 규칙이 변경되었습니다. Azure AD Connect 동기화 서비스는 업그레이드 후에 전체 가져오기 및 전체 동기화 단계를 트리거합니다. Hello 변경 내용의 세부 정보에 대 한 설명은 다음과 같습니다.
>
>

**수정된 문제:**

Azure AD Connect 동기화

* 고객 hello 집합 ADSyncAutoUpgrade cmdlet를 사용 하 여 hello 기능을 비활성화 한 경우에 Azure AD Connect 서버 hello에 toooccur 자동 업그레이드를 수행 하는 문제가 해결 되었습니다. 이 해결 방법을 hello hello 서버에 자동 업그레이드 프로세스 계속 확인 업그레이드 정기적으로, 하지만 hello 다운로드 한 설치 관리자 인식 hello 자동 업그레이드 구성 합니다.
* Azure AD Connect 디렉터리 동기화 전체 업그레이드 하는 동안 hello Azure AD 커넥터에서 Azure AD와 동기화 하는 데 사용 되는 Azure AD 서비스 계정 toobe를 만듭니다. Hello 계정을 만든 후 Azure AD Connect hello 계정을 사용 하 여 Azure AD에 인증 합니다. 경우에 따라 인증 실패 시 일시적인 문제 때문에 오류와 함께 DirSync 내부 업그레이드 toofail에 이르게 *"ए 실행 중인 구성 AAD 동기화 작업: AADSTS50034: hello 계정이 응용이 프로그램에 toosign 추가 해야 toohello xxx.onmicrosoft.com 디렉터리. "* 디렉터리 동기화 업그레이드 tooimprove hello 복원 력, Azure AD Connect hello 인증 단계를 지금 다시 시도합니다.
* 디렉터리 동기화 전체 업그레이드 toosucceed 시키는 443 빌드와 문제가 발생 했습니다. 하지만 디렉터리 동기화에 필요한 실행된 프로필 생성 되지 않습니다. 이 문제를 해결하는 논리가 Azure AD Connect의 이 빌드에 포함되었습니다. 고객 toothis 빌드를 업그레이드 하는 경우 Azure AD Connect 없습니다. 실행된 프로필을 검색 하 고으로 만듭니다.
* 암호 동기화 프로세스 toofail toostart 이벤트 ID 6900 및 오류를 발생 시키는 문제가 해결 되었습니다. *"hello 이미 추가 된 동일한 키를 가진 항목이"*합니다. 이 문제는 필터링 구성을 tooinclude AD 구성 파티션에 OU를 업데이트 하는 경우에 발생 합니다. AD 도메인 파티션만의 암호 변경을 동기화 하는 toofix 지금 암호 동기화이 문제를 처리 합니다. 구성 파티션과 같은 비도메인 파티션은 건너뜁니다.
* 빠른 설치 하는 동안 Azure AD Connect 만듭니다 온-프레미스 AD DS 계정 toobe hello AD 커넥터 toocommunicate 온-프레미스에서 사용 하는 AD 합니다. 이전에 hello 계정은 hello PASSWD_NOTREQD 플래그가 hello 사용자 계정 제어 특성에 설정 하 고 임의의 암호가 hello 계정에 설정 됩니다. 이제 Azure AD Connect 명시적으로 hello PASSWD_NOTREQD 플래그 후 제거 hello 암호가 hello 계정을 설정 합니다.
* 오류와 함께 DirSync 업그레이드 toofail를 발생 시키는 문제가 해결 되었습니다. *"는 교착 상태가 발생 한 sql server에 있는 동안 tooacquire 응용 프로그램 잠금을"* hello mailNickname 특성 hello에 있을 때 온-프레미스 AD 스키마 되지 않은 toohello AD 사용자 개체 클래스를 제한 합니다.
* 장치 쓰기 저장 기능 tooautomatically 되는 문제를 관리자가 Azure AD Connect 마법사를 사용 하 여 Azure AD Connect 동기화 구성을 업데이트할 때 사용할 고정 합니다. Hello 기존 장치 쓰기 저장 구성에서 온-프레미스 AD와 hello 확인이 실패에 대 한 hello 마법사 수행 필수 구성 요소 검사를 통해 원인입니다. 장치 쓰기 저장은 이미 사용 하도록 설정한 경우 이전에 hello 수정이 되었습니다 tooskip hello 확인 합니다.
* OU 필터링 hello Azure AD Connect 마법사를 사용 하거나 동기화 서비스 관리자 hello tooconfigure 합니다. 이전에 hello Azure AD Connect 마법사 tooconfigure OU 필터링을 사용 하면 만든 새 Ou 나중에 포함 되어 디렉터리 동기화 합니다. 새 Ou toobe 포함 하지 않으려면 OU를 구성 해야 동기화 서비스 관리자 hello를 사용 하 여 필터링 합니다. 이제이 가능 hello Azure AD Connect 마법사를 사용 하 여 동일한 동작입니다.
* Azure AD Connect toobe hello dbo 스키마에서 대신 관리자를 설치 하는 hello의 hello 스키마 아래에 생성에 필요한 저장된 프로시저는 문제를 수정 했습니다.
* Azure AD toobe hello AAD 연결 서버 이벤트 로그에 의해 반환 된 hello TrackingId 특성이 되는 문제를 수정 했습니다. hello 문제는 Azure AD에서 리디렉션 메시지를 수신 하는 Azure AD Connect 및 Azure AD Connect는 없습니다 tooconnect toohello 끝점을 제공 하는 경우에 발생 합니다. 서비스 쪽 로그가 포함 된 지원 엔지니어 toocorrelate hello TrackingId 문제를 해결 하는 동안 사용 됩니다.
* Azure AD에서 LargeObject 오류를 수신 하는 Azure AD Connect를 하는 경우 Azure AD Connect EventID 6941와 메시지를 사용 하 여 이벤트를 생성 하는 *"hello 프로 비전 된 개체가 너무 큽니다. 트리밍 특성 값이이 개체에 hello 수입니다. "* Hello에서 동일한 시간, Azure AD Connect도 EventID 6900 및 메시지와 함께 잘못 된 이벤트를 생성할 *"Microsoft.Online.Coexistence.ProvisionRetryException: Windows hello로 없습니다 toocommunicate Azure Active Directory 서비스입니다."* toominimize 혼동을 Azure AD Connect를 더 이상 LargeObject 오류가 수신 되 면 hello 후자 이벤트를 생성 합니다.
* 일반 LDAP 커넥터에 대 한 tooupdate hello 구성 하려고 할 때 응답 하지 않는 동기화 서비스 관리자 toobecome hello를 야기 하는 문제를 수정 했습니다.

**새 기능/향상된 기능:**

Azure AD Connect 동기화
* 동기화 규칙 변경 내용 – 변경을 구현한 동기화 규칙을 따르는 hello:
  * 업데이트 된 기본 동기화 규칙 집합 toonot 내보내기 특성 **userCertificate** 및 **userSMIMECertificate** hello 특성 15 개 이상의 값이 있는 경우.
  * AD 특성 **employeeID** 및 **msExchBypassModerationLink** 이제 hello 기본 동기화 규칙 집합에 포함 되어 있습니다.
  * **photo** AD 특성은 기본 동기화 규칙 집합에서 제거되었습니다.
  * 추가 **preferredDataLocation** toohello 메타 버스 스키마 및 AAD 커넥터 스키마입니다. 사용자가 Azure AD의 특성 중 하나를 구현할 수 tooupdate 사용자 지정 규칙 toodo를 지금 동기화 합니다. hello 특성에 대 한 자세한 내용을 toofind tooarticle 섹션을 참조 하십시오. [Azure AD Connect 동기화: 어떻게 변경 toohello toomake 기본 구성-Enable PreferredDataLocation 동기화](active-directory-aadconnectsync-change-the-configuration.md#enable-synchronization-of-preferreddatalocation)합니다.
  * 추가 **userType** toohello 메타 버스 스키마 및 AAD 커넥터 스키마입니다. 사용자가 Azure AD의 특성 중 하나를 구현할 수 tooupdate 사용자 지정 규칙 toodo를 지금 동기화 합니다.

* Azure AD Connect 이제 자동으로 ConsistencyGuid 특성에 대 한 hello 원본 앵커 특성으로 사용 하도록 설정 hello 사용 온-프레미스 AD 개체입니다. 그 뿐만 아니라 Azure AD Connect가 비어 있으면 hello objectGuid 특성 값을 사용 하 여 hello ConsistencyGuid 특성을 채웁니다. 이 기능은 해당 toonew 배포만 있습니다. 이 기능에 대 한 자세한 내용을 toofind tooarticle 섹션을 참조 하십시오. [Azure AD Connect: 개념-게스트가 ConsistencyGuid sourceAnchor로 사용 하 여 디자인](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor)합니다.
* 추가 된 toohelp 진단 암호 해시 동기화 새 cmdlet Invoke ADSyncDiagnostics 되었습니다. 문제 해결 관련 문제입니다. Hello cmdlet을 사용 하는 방법에 대 한 정보를 참조 tooarticle [Azure AD Connect 동기화로 암호 동기화 문제를 해결](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-troubleshoot-password-synchronization)합니다.
* Azure AD Connect에서 개체를 지 원하는 메일 사용이 가능한 공용 폴더를 동기화 하는 이제 온-프레미스 AD tooAzure AD. 선택적 기능에서 Azure AD Connect 마법사를 사용 하 여 hello 기능을 사용할 수 있습니다. 이 기능에 대 한 자세한 내용을 toofind 참조 tooarticle [온-프레미스 메일 사용 가능 공용 폴더에 대 한 지원 Office 365 디렉터리 기반 가장자리 차단](https://blogs.technet.microsoft.com/exchange/2017/05/19/office-365-directory-based-edge-blocking-support-for-on-premises-mail-enabled-public-folders)합니다.
* Azure AD Connect는 온-프레미스에서 AD DS 계정 toosynchronize는 필요한 AD 합니다. 이전에 Azure AD Connect를 설치 하는 경우 hello Express 모드를 사용 하 여 hello 엔터프라이즈 관리자 계정의 자격 증명을 제공할 수 있습니다 만들고 Azure AD Connect는 hello AD DS 계정이 필요 합니다. 그러나 사용자 지정 설치 및 추가 포리스트 tooan 기존 배포에 대 한 있었습니다. 필요한 tooprovide hello AD DS 계정 대신입니다. 이제도 hello 옵션 tooprovide 사용자 지정 설치 중에 엔터프라이즈 관리자 계정의 자격 증명을 hello 및 Azure AD Connect 필요한 AD DS hello 계정을 만들 수 있도록 준비 합니다.
* Azure AD Connect는 이제 SQL AOA를 지원합니다. Azure AD Connect를 설치하기 전에 SQL AOA를 사용하도록 설정해야 합니다. Azure AD Connect를 설치 하는 동안 SQL AOA에 대 한 제공 된 hello SQL 인스턴스 사용 되는지 여부를 검색 합니다. SQL AOA 사용 하는 경우 Azure AD Connect를 더 이상를 알아 SQL AOA 구성된 toouse 동기 복제 또는 비동기 복제 인지 합니다. Hello 가용성 그룹 수신기를 설정할 때는 hello RegisterAllProvidersIP 속성 too0를 설정 하는 것이 좋습니다. 이 SQL Native Client tooconnect tooSQL에 현재 사용 하 여 Azure AD Connect SQL Native Client MultiSubNetFailover 속성의 hello 사용을 지원 하지 않는 때문입니다.
* 사용 하는 LocalDB hello 데이터베이스와 Azure AD Connect 서버에 대 한 10GB 크기 제한에 도달 하는 경우 더 이상 hello 동기화 서비스를 시작 합니다. 이전에 필요 tooperform ShrinkDatabase 연산을 hello LocalDB tooreclaim DB 공간이 hello 동기화 서비스 toostart 합니다. 후 which, 있습니다 사용할 hello toodelete 동기화 서비스 관리자를 실행할 수 기록 tooreclaim DB 공간입니다. 이제 시작 ADSyncPurgeRunHistory cmdlet toopurge LocalDB tooreclaim DB 공간에서 실행 되는 기록 데이터를 사용할 수 있습니다. 또한이 cmdlet에는 오프 라인 모드를 지원 (지정 하 여 hello-offline 매개 변수) 실행 하지 않는 경우 사용된 hello 동기화 서비스 일 수 있습니다. 참고: hello 사용 되는 데이터베이스가 LocalDB 및 hello 동기화 서비스가 실행 되지 않는 경우 hello 오프 라인 모드 사용할만 있습니다.
* Azure AD Connect LocalDB/SQL 데이터베이스에 저장 하기 전에 동기화 오류 세부 정보를 이제 압축 tooreduce hello 양을 저장 공간이 필요 합니다. 이전 버전의 Azure AD Connect toothis 버전에서 업그레이드 하는 경우 Azure AD Connect 동기화 오류 세부 정보를 기존에 일회성 압축을 수행 합니다.
* 이전에 필터링 구성 하는 OU를 업데이트 한 후 있습니다 수동으로 실행 해야 합니다. 전체 가져오기 tooensure 기존 개체는 올바르게 포함/제외 디렉터리 동기화에서입니다. 이제 Azure AD Connect 전체 가져오기를 자동으로 트리거합니다 hello 다음 동기화 하는 동안 순환 합니다. 그 뿐만 아니라 전체 가져오기는 적용 된 toohello AD 커넥터 hello 업데이트의 영향을 수 있습니다. 참고: 이러한 향상은 적용 가능한 tooOU만 hello Azure AD Connect 마법사를 사용 하 여 수행 되는 업데이트를 필터링 합니다. 적용 가능한 tooOU hello 동기화 서비스 관리자를 사용 하 여 업데이트를 필터링 하지 않습니다.
* 이전에는 그룹 기반 필터링에서 Users, Groups 및 Contact 개체만 지원합니다. 이제는 그룹 기반 필터링에서 Computer 개체도 지원합니다.
* 이전에는 Azure AD Connect 동기화 스케줄러를 사용하여 커넥터 공간 데이터를 삭제할 수 있었습니다. 이제 hello Synchronization Service Manager 커넥터 공간 데이터의 hello 삭제를 차단 해당 hello 스케줄러 발견 되 면 활성화 됩니다. 또한 경고 hello 커넥터 공간 데이터는 삭제 하는 경우 잠재적 데이터 손실에 대 한 tooinform 고객 반환 됩니다.
* 이전에 Azure AD Connect 마법사 toorun에 대 한 PowerShell 기록이 올바르게 해제 해야 합니다. 이 문제는 부분적으로 해결되었습니다. Azure AD Connect 마법사 toomanage 동기화 구성을 사용 하는 경우 PowerShell 기록이 사용할 수 있습니다. Azure AD Connect 마법사 toomanage ADFS 구성을 사용 하는 경우에 PowerShell 기록이 해제 해야 합니다.



## <a name="114860"></a>1.1.486.0
릴리스 날짜: 2017년 4월

**수정된 문제:**
* 여기서 Azure AD Connect에 설치 되지 않음 성공적으로 지역화 된 버전의 Windows Server hello 문제가 해결 되었습니다.

## <a name="114840"></a>1.1.484.0
릴리스 날짜: 2017년 4월

**알려진 문제:**

* 이 버전의 Azure AD Connect hello 다음 조건이 모두 참인 경우에 제대로 설치 되지 않습니다.
   1. DirSync 전체 업그레이드 또는 Azure AD Connect 새로 설치를 수행하고 있습니다.
   2. 지역화 된 버전의 Windows Server를 hello 서버에서 기본 제공 관리자 그룹의 hello 이름은 "Administrators"이 아닙니다 사용 하는.
   3. Hello 기본 전체 SQL 제공 하는 대신 Azure AD Connect와 함께 설치 하는 SQL Server 2012 Express LocalDB를 사용 하는 합니다.

**수정된 문제:**

Azure AD Connect 동기화
* 하나 이상의 커넥터가 해당 동기화 단계에 대 한 실행된 프로필에 누락 된 경우 hello 동기화 스케줄러 hello 전체 동기화 단계를 건너뛰고는 여기서 문제를 해결 합니다. 예를 들어 실행 프로필에 대 한 델타 가져오기 작업을 만들지 않고 hello 동기화 서비스 관리자를 사용 하 여 커넥터 수동으로 추가 합니다. 이 문제를이 수정 해당 hello 동기화 스케줄러 다른 커넥터에 대 한 델타 가져오기 toorun 계속 되도록 합니다.
* 문제가 해결 되었습니다. 여기서 hello 동기화 서비스를 즉시 중지 실행된 프로필을 처리 되었을 때 문제가 발생 하 여는 hello 실행 단계 중 하나를 사용 합니다. 이 문제를이 수정 단계를 실행 하 고 계속 tooprocess hello 나머지를 건너뜁니다. 동기화 서비스는 hello를 보장 합니다. 예를 들어 여러 실행 단계가 포함된 AD Connector에 대한 델타 가져오기 실행 프로필이 있습니다(각 온-프레미스 AD 도메인에 하나씩). hello 동기화 서비스가 실행 됩니다 델타 가져오기 hello로 다른 AD 도메인 중 하나에 네트워크 연결 문제가 있는 경우에 합니다.
* 자동 업그레이드 중에 건너뜁니다 hello Azure AD 커넥터 업데이트 toobe 되는 문제를 수정 했습니다.
* 해당 원인을 Azure AD Connect tooincorrectly을 문제가 해결 되었습니다. 설정 하면 디렉터리 동기화에서에서 toofail 업그레이드를 설치 하는 동안 hello 서버는 도메인 컨트롤러 인지 확인 합니다.
* 내부 업그레이드 toonot 만들 모든 디렉터리 동기화 문제 실행 프로필 hello Azure AD 커넥터에 대 한 고정 합니다.
* Tooconfigure 일반 LDAP 커넥터 하려고 할 때 hello 동기화 서비스 관리자 사용자 인터페이스가 응답 하지 않는 수 없는 문제를 해결 합니다.

AD FS 관리
* Hello AD FS에 대 한 주 노드 이동된 tooanother 서버 되었으면 hello Azure AD Connect 마법사가 실패 하는 위치는 문제가 해결 되었습니다.

데스크톱 SSO
* 여기서 hello 로그인 화면 수는 없습니다을 새로 설치 하는 동안 로그인 옵션으로 암호 동기화를 선택 하는 경우 데스크톱 SSO 기능을 사용 하도록 설정 hello Azure AD Connect 마법사에서 문제를 해결 합니다.

**새 기능/향상된 기능:**

Azure AD Connect 동기화
* 이제 azure AD 연결 동기화 서비스 계정으로 가상 서비스 계정, 관리 서비스 계정 및 그룹 관리 서비스 계정을의 hello 사용을 지원합니다. 이 Azure AD Connect 설치를 toonew 적용 됩니다. Azure AD Connect를 설치할 경우:
    * 기본적으로 Azure AD Connect 마법사는 가상 서비스 계정을 만들고 이를 서비스 계정으로 사용합니다.
    * 도메인 컨트롤러에 설치 하는 경우 Azure AD Connect를 대신 tooprevious 동작은 도메인 사용자 계정을 만듭니다 하 고 대신 해당 서비스 계정으로 사용 합니다.
    * Hello 다음 중 하나를 제공 하 여 hello 기본 동작을 재정의할 수 있습니다.
      * 그룹 관리 서비스 계정
      * 관리 서비스 계정
      * 도메인 사용자 계정
      * 로컬 사용자 계정
* 이전에 포함 된 Azure AD Connect의 tooa 새 빌드를 업그레이드 하는 경우 커넥터를 업데이트 또는 Azure AD Connect 동기화 규칙이 변경 되더라도 전체 동기화 주기를 트리거합니다. 이제 Azure AD Connect는 선택적으로 업데이트가 있는 커넥터에 대해서만 전체 가져오기 단계를 트리거하고 동기화 규칙 변경 내용이 있는 커넥터에 대해서만 전체 동기화 단계를 트리거합니다.
* 이전에 hello 내보내기 삭제 임계값 hello 동기화 스케줄러를 통해 트리거되는 tooexports만 적용 됩니다. 이제 hello 기능을 수동으로 hello 동기화 서비스 관리자를 사용 하 여 hello 고객에 의해 트리거되는 tooinclude 내보내기를 확장 합니다.
* Azure AD 테넌트에는 테넌트에 대해 암호 동기화 기능을 사용할지 여부를 나타내는 서비스 구성이 있습니다. 이전에 hello 서비스 구성 toobe 잘못 구성 된 Azure AD Connect에서 활성 및 스테이징 서버에 대 한 쉽습니다. Azure AD Connect가 tookeep hello 서비스 구성 활성와 일치를 시도 하는 이제 Azure AD Connect 서버 전용입니다.
* Azure AD Connect 마법사는 이제 온-프레미스 AD에서 AD 휴지통이 사용되지 않는 경우 경고를 감지하고 반환합니다.
* 이전에 AD 제한 시간이 초과 되며 hello hello 일괄 처리의 hello 개체의 크기를 결합 하는 경우 실패 내보내기 tooAzure 특정 임계값을 초과 합니다. 이제 동기화 서비스 hello hello 문제가 발생 하는 경우 tooresend hello 개체를 별도, 더 작은 일괄 후 다시 시도 합니다.
* 동기화 서비스 키 관리 응용 프로그램 hello Windows 시작 메뉴에서 제거 되었습니다. 암호화 키의 관리 miiskmu.exe를 사용 하 여 명령줄 인터페이스를 통해 지원 toobe를 계속 됩니다. 암호화 키를 관리 하는 방법에 대 한 정보를 참조 tooarticle [Abandoning hello Azure AD Sync 연결 암호화 키](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-change-serviceacct-pass#abandoning-the-azure-ad-connect-sync-encryption-key)합니다.
* 이전에 hello Azure AD Connect 동기화 서비스 계정 암호를 변경 하면 hello 동기화 서비스 됩니다 수 시작 올바르게 hello 암호화 키를 중단 하 고 hello Azure AD Connect 동기화 서비스 계정 암호를 다시 초기화 될 때까지 합니다. 이제 이 내용은 더 이상 필요하지 않습니다.

데스크톱 SSO

* Azure AD Connect 마법사 포트 9090 toobe 통과 인증 및 데스크톱 SSO를 구성할 때 hello 네트워크에서 열을 더 이상 필요 합니다. 포트 443만 필요합니다. 

## <a name="114430"></a>1.1.443.0
릴리스 날짜: 2017년 3월

**수정된 문제:**

Azure AD Connect 동기화
* Hello Azure AD 커넥터의 표시 이름을 hello hello 초기 onmicrosoft.com 도메인 할당 toohello Azure AD 테 넌 트 포함 되어 있지 않으면 Azure AD Connect 마법사 toofail를 일으키는 문제를 해결 합니다.
* Azure AD Connect 마법사 toofail 아포스트로피, 콜론 및 공간 등의 특수 문자를 포함 하는 hello 암호 동기화 서비스 계정 hello의 tooSQL 데이터베이스 연결을 설정 하는 동안 발생 하는 문제가 해결 되었습니다.
* 그러면 hello 오류 toooccur "hello dimage hello 이미지 보다 다른 앵커에 대 한" 준비 모드에서 Azure AD Connect 서버에는 문제가 해결, 후 일시적으로 제외한 온-프레미스 AD에서 동기화 하는 개체를 포함 한 다음 다시 동기화 하는 중입니다.
* 그러면 hello 오류 toooccur "hello DN에서 찾은 개체가 팬텀" 준비 모드에서 Azure AD Connect 서버에는 문제가 해결, 후 일시적으로 제외한 온-프레미스 AD 동기화에서 개체를 동기화 하는 옵션과 다시 포함 합니다.

AD FS 관리
* Azure AD Connect 마법사가 되지 AD FS 구성을 업데이트 하 고 설정이 없는 hello 오른쪽 클레임 hello 대체 로그인 ID를 구성한 후에 신뢰 당사자 트러스트에 문제가 해결 되었습니다.
* 여기서 Azure AD Connect 마법사는 userPrincipalName 형식을 sAMAccountName 형식 대신 사용 하 여 구성 된 서비스 계정의 수 없습니다 toocorrectly 핸들 AD FS 서버 문제를 해결 합니다.

통과 인증
* 인증을 통해 전달 선택 되어 있지만 해당 커넥터의 등록에 실패 하는 경우 Azure AD Connect 마법사 toofail를 일으키는 문제를 해결 합니다.
* Azure AD Connect 마법사 toobypass 유효성을 검사 로그인 방법을 선택한 데스크톱 SSO 기능이 설정 된 경우에 문제가 해결 되었습니다.

암호 재설정
* Hello Azure AAD Connect 서버 toonot 시도 toore 수 있는 문제가 해결 되었습니다.-hello 연결 방화벽 또는 프록시에 의해 중단 된 경우에 연결 합니다.

**새 기능/향상된 기능:**

Azure AD Connect 동기화
* 이제 Get-ADSyncScheduler cmdlet은 SyncCycleInProgress라는 새 부울 속성을 반환합니다. Hello 반환 값이 true 인 경우, 진행 중인 예약 된 동기화 주기 있다는 것을 의미 합니다.
* Azure AD Connect 설치 및 설치 로그를 저장 하기 위한 대상 폴더 %localappdata%\AADConnect too%programdata%\AADConnect tooimprove 내게 필요한 옵션 toohello 로그 파일에서 이동 되었습니다.

AD FS 관리
* AD FS 팜 SSL 인증서를 업데이트하기 위한 지원이 추가되었습니다.
* AD FS 2016을 관리하기 위한 지원이 추가되었습니다.
* 이제 AD FS를 설치하는 동안 기존 gMSA(그룹 관리 서비스 계정)를 지정할 수 있습니다.
* 이제 Azure AD 신뢰 당사자 트러스트에 대 한 hello 서명 해시 알고리즘으로 s h A-256을 구성할 수 있습니다.

암호 재설정
* 향상 된 기능 tooallow hello 제품 toofunction을 더 엄격한 방화벽 규칙을 사용 하 여 환경에 도입 되었습니다.
* 향상 된 연결 안정성 tooAzure 서비스 버스

## <a name="113800"></a>1.1.380.0
릴리스 날짜: 2016년 12월

**해결된 문제:**

* Hello issuerid Active Directory Federation Services (AD FS)에 대 한 규칙을 클레임 고정된 hello 문제는이 빌드에 없습니다.

>[!NOTE]
>이 빌드 hello Azure AD 연결 자동 업그레이드 기능을 통해 사용할 수 있는 toocustomers 아닙니다.

## <a name="113710"></a>1.1.371.0
릴리스 날짜: 2016년 12월

**알려진 문제:**

* AD FS에 대 한 hello issuerid 클레임 규칙은이 빌드에 없습니다. hello issuerid 클레임 규칙은 Azure Active directory (Azure AD) 여러 도메인을 페더레이션 하는 경우 필수입니다. 온-프레미스 Azure AD Connect toomanage 사용 중인 경우 toothis 빌드를 업그레이드 하는 AD FS 배포에서 AD FS 구성을 hello 기존 issuerid 클레임 규칙을 제거 합니다. Hello 설치/업그레이드 후 hello issuerid 클레임 규칙을 추가 하 여 hello 문제를 해결할 수 있습니다. Hello issuerid 추가 대 한 내용은 클레임 규칙에 대 한 대 toothis 문서 참조 [Azure AD와 페더레이션에 대 한 여러 도메인 지원](active-directory-aadconnect-multiple-domains.md)합니다.

**해결된 문제:**

* 포트 9090 hello 아웃 바운드 연결에 대 한 열려 있지 않으면 hello Azure AD Connect 설치 또는 업그레이드 실패 합니다.

>[!NOTE]
>이 빌드 hello Azure AD 연결 자동 업그레이드 기능을 통해 사용할 수 있는 toocustomers 아닙니다.

## <a name="113700"></a>1.1.370.0
릴리스 날짜: 2016년 12월

**알려진 문제:**

* AD FS에 대 한 hello issuerid 클레임 규칙은이 빌드에 없습니다. 여러 도메인을 Azure AD와 페더레이션 hello issuerid 클레임 규칙이 필요 합니다. 온-프레미스 Azure AD Connect toomanage 사용 중인 경우 toothis 빌드를 업그레이드 하는 AD FS 배포에서 AD FS 구성을 hello 기존 issuerid 클레임 규칙을 제거 합니다. 설치/업그레이드 후 hello issuerid 클레임 규칙을 추가 하 여 hello 문제를 해결할 수 있습니다. 에 issuerid 추가 대 한 내용은 클레임 규칙에 대 한 참조 toothis 문서 [Azure AD와 페더레이션에 대 한 여러 도메인 지원](active-directory-aadconnect-multiple-domains.md)합니다.
* 포트 9090 열려 아웃 바운드 toocomplete 설치 해야 합니다.

**새로운 기능:**

* 통과 인증(미리 보기)

>[!NOTE]
>이 빌드 hello Azure AD 연결 자동 업그레이드 기능을 통해 사용할 수 있는 toocustomers 아닙니다.

## <a name="113430"></a>1.1.343.0
릴리스 날짜: 2016년 11월

**알려진 문제:**

* AD FS에 대 한 hello issuerid 클레임 규칙은이 빌드에 없습니다. 여러 도메인을 Azure AD와 페더레이션 hello issuerid 클레임 규칙이 필요 합니다. 온-프레미스 Azure AD Connect toomanage 사용 중인 경우 toothis 빌드를 업그레이드 하는 AD FS 배포에서 AD FS 구성을 hello 기존 issuerid 클레임 규칙을 제거 합니다. 설치/업그레이드 후 hello issuerid 클레임 규칙을 추가 하 여 hello 문제를 해결할 수 있습니다. 에 issuerid 추가 대 한 내용은 클레임 규칙에 대 한 참조 toothis 문서 [Azure AD와 페더레이션에 대 한 여러 도메인 지원](active-directory-aadconnect-multiple-domains.md)합니다.

**수정된 문제:**

* 암호 복잡성이 hello 조직의 암호 정책에 지정 된 hello 수준을 충족 하는 로컬 서비스 계정 수 없습니다 toocreate 있기 때문에 경우에 따라 실패 Azure AD Connect를 설치 합니다.
* 문제가 해결 되었습니다. 여기서 조인 규칙이 다시 평가 되지 hello 커넥터 공간에서 개체는 동시에 범위를 벗어난 되 면 하나에 대 한 규칙을 조인 하 고 범위에 있을 다른 합니다. 이런 상황은 조인 조건이 서로 배타적인 조인 규칙이 둘 이상인 경우 발생할 수 있습니다.
* 조인 규칙을 포함하지 않는 인바운드 동기화 규칙(Azure AD의)이 조인 규칙을 포함하는 규칙보다 낮은 우선 순위 값을 갖는 경우 처리되지 않는 문제가 해결되었습니다.

**향상된 기능:**

* Windows Server 2016 Standard 이상에 Azure AD Connect를 설치할 수 있도록 지원이 추가되었습니다.
* Hello 원격 데이터베이스와 SQL Server 2016을 사용 하 여 Azure AD Connect에 대 한 지원이 추가 되었습니다.

## <a name="112810"></a>1.1.281.0
릴리스 날짜: 2016년 8월

**수정된 문제:**

* 완료 된 다음 동기화 주기 후 hello 때까지 변경 내용을 toosync 간격 수행 되지 않습니다.
* Azure AD Connect 마법사는 사용자 이름이 밑줄(\_)로 시작하는 Azure AD 계정을 허용하지 않습니다.
* Azure AD Connect 마법사 hello 계정 암호에 특수 문자가 너무 많습니다. 포함 된 경우 tooauthenticate hello Azure AD 계정의 실패 합니다. 오류 메시지 "toovalidate 수 없습니다 자격 증명입니다. 예기치 않은 오류가 발생했습니다." 가 반환됩니다.
* 서버를 준비 하 제거 하는 Azure AD 테 넌 트의 암호 동기화를 해제 하 고 활성 서버 암호 동기화 toofail 되 면 합니다.
* 암호 동기화 사용자 hello에 저장 된 암호 해시 없는 경우 특수 한 경우 실패 합니다.
* Azure AD Connect 서버가 준비 모드에서 활성화된 경우 비밀번호 쓰기 저장은 일시적으로 비활성화되지 않습니다.
* Azure AD Connect 마법사 서버가 준비 모드에 있을 때 hello 실제 암호 동기화 및 암호 쓰기 저장 구성을 표시 되지 않습니다. 항상 비활성화로 표시합니다.
* 구성 변경 내용 toopassword 동기화 및 암호 쓰기 저장 유지 되지 않습니다 Azure AD Connect 마법사에 의해 서버가 준비 모드에 있을 때.

**향상된 기능:**

* 인지 것 수 toosuccessfully 시작 새 동기화 주기가 시작 ADSyncSyncCycle hello cmdlet tooindicate를 업데이트 합니다.
* 추가 된 hello 중지 ADSyncSyncCycle cmdlet tooterminate 동기화 주기와 작업을 현재 진행 중인입니다.
* 업데이트 된 hello 중지 ADSyncScheduler cmdlet tooterminate 동기화 주기와 작업을 현재 진행 중인입니다.
* 구성할 때 [디렉터리 확장](active-directory-aadconnectsync-feature-directory-extensions.md) 에 Azure AD Connect 마법사 "Teletex 문자열" 형식의 hello Azure AD 특성 이제 선택할 수 있습니다.

## <a name="111890"></a>1.1.189.0
릴리스 날짜: 2016년 6월

**수정된 문제 및 향상된 기능:**

* 이제 Azure AD Connect를 FIPS 규격 서버에 설치할 수 있습니다.
  * 암호 동기화에 대해서는 [암호 동기화 및 FIPS](active-directory-aadconnectsync-implement-password-synchronization.md#password-synchronization-and-fips)를 참조하세요.
* NetBIOS 이름 수 없는 해결된 toohello FQDN hello Active Directory Connector에서에서 문제를 해결 합니다.

## <a name="111800"></a>1.1.180.0
릴리스 날짜: 2016년 5월

**새로운 기능:**

* 사용자가 Azure AD Connect를 실행하기 전에 도메인을 확인하지 않았으면 사용자에게 그 사실을 알리고 확인할 수 있도록 도와줍니다.
* [Microsoft Cloud 독일](active-directory-aadconnect-instances.md#microsoft-cloud-germany)에 대한 지원을 추가했습니다.
* 최신 hello에 대 한 지원을 추가 [Microsoft Azure Government 클라우드](active-directory-aadconnect-instances.md#microsoft-azure-government-cloud) 인프라를 새 URL 요구 사항입니다.

**수정된 문제 및 향상된 기능:**

* 추가 된 필터링 toohello 동기화 규칙 편집기 toomake 하기 쉬운 toofind 동기화 규칙입니다.
* 커넥터 공간을 삭제할 경우 성능이 향상되었습니다.
* 동일한 개체 모두 삭제 되었고에 추가 된 hello hello 동일한 (호출 delete/추가)를 실행 하는 경우 문제가 해결 되었습니다.
* 비활성화된 동기화 규칙은 더 이상 업그레이드 또는 디렉터리 스키마 새로 고침 시 포함된 개체 및 특성을 다시 활성화하지 않습니다.

## <a name="111300"></a>1.1.130.0
릴리스 날짜: 2016년 4월

**새로운 기능:**

* 너무 다중값된 특성에 대 한 지원을 추가[디렉터리 확장](active-directory-aadconnectsync-feature-directory-extensions.md)합니다.
* 에 대 한 자세한 구성 변형에 대 한 지원 추가 [자동 업그레이드](active-directory-aadconnect-feature-automatic-upgrade.md) toobe 업그레이드 가능 것으로 간주 합니다.
* [사용자 지정 스케줄러](active-directory-aadconnectsync-feature-scheduler.md#custom-scheduler)에 대한 일부 cmdlet이 추가되었습니다.

## <a name="111190"></a>1.1.119.0
릴리스 날짜: 2016년 3월

**수정된 문제:**

* Windows Server 2008(R2 이전 버전)에는 암호 동기화가 지원되지 않기 때문에 이 운영 체제에서는 빠른 설치를 사용할 수 없습니다.
* 사용자 지정 필터가 구성된 Dirsync에서 업그레이드가 예상대로 작동하지 않습니다.
* Tooa 최신 릴리스로 업그레이드 하는 경우 변경 내용을 toohello 구성이 없는 가지, 전체 가져오기/동기화 작업이 예약 되지 않도록 합니다.

## <a name="111100"></a>1.1.110.0
릴리스 날짜: 2016년 2월

**수정된 문제:**

* Hello 설치 hello 기본 C:\Program Files 폴더에 없는 경우에 이전 버전에서 업그레이드 작동 하지 않습니다.
* 설치 하 고 선택을 취소 하면 **hello 동기화 프로세스를 시작** hello 설치 마법사의 hello 끝 실행 중인 hello 설치 마법사를 두 번째로 사용 하지 않습니다 hello 스케줄러입니다.
* hello 스케줄러 작동 하지 않는 위치 hello 영어 날짜/시간 형식이 사용 되지 않음을 서버에서 예상 대로 합니다. 또한 프로그램이 `Get-ADSyncScheduler` tooreturn 올바른 시간입니다.
* 를 설치한 경우 이전 버전의 Azure AD Connect 및 AD FS 로그인 옵션 및 업그레이드 hello으로 hello 설치 마법사를 다시 실행할 수 없습니다.

## <a name="111050"></a>1.1.105.0
릴리스 날짜: 2016년 2월

**새로운 기능:**

* [Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) 기능
* Hello 설치 마법사에서 Azure Multi-factor Authentication 및 Privileged Identity Management를 사용 하 여 전역 admin 님 안녕하세요 지원 합니다.
  * Tooallow 해야 Multi-factor Authentication을 사용 하는 경우 프록시 tooalso 트래픽 toohttps://secure.aadcdn.microsoftonline-p.com를 허용 합니다.
  * Multi-factor Authentication tooproperly 작업 tooadd https://secure.aadcdn.microsoftonline-p.com tooyour 신뢰할 수 있는 사이트 목록이 필요합니다.
* 초기 설치 후 hello 사용자의 로그인 메서드를 변경할 수 있습니다.
* 허용 [도메인 및 OU 필터링](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) hello 설치 마법사에 있습니다. 또한 모든 도메인을 사용할 수 있는 tooforests 연결할 수 있습니다.
* [스케줄러](active-directory-aadconnectsync-feature-scheduler.md) toohello 동기화 엔진에 작성 됩니다.

**미리 보기 tooGA에서 승격 된 기능은 다음과 같습니다.**

* [장치 쓰기 저장](active-directory-aadconnect-feature-device-writeback.md)
* [디렉터리 확장](active-directory-aadconnectsync-feature-directory-extensions.md)

**새로운 미리 보기 기능:**

* hello 새 기본 동기화 주기 간격은 30 분입니다. 모든 이전 버전에 대 한 toobe 3 시간을 사용 합니다. 추가 지원 toochange hello [스케줄러](active-directory-aadconnectsync-feature-scheduler.md) 동작 합니다.

**수정된 문제:**

* hello는 DNS 도메인 페이지 hello 도메인을 항상 인식 하지 못했습니다. 확인 합니다.
* AD FS를 구성할 때 도메인 관리자 자격 증명을 묻는 메시지가 표시됩니다.
* hello 온-프레미스 AD 계정을 hello 루트 도메인 보다 다른 DNS 트리를 사용 하 여 도메인에 있는 경우 hello 설치 마법사에 의해 인식 되지 않습니다.

## <a name="1091310"></a>1.0.9131.0
릴리스 날짜: 2015년 12월

**수정된 문제:**

* AD DS(Active Directory Domain Services)에서 암호를 변경할 때는 암호 동기화가 작동하지 않을 수도 있지만 암호를 설정할 때는 작동합니다.
* Hello 구성 페이지에서 업그레이드 하는 경우 또는 프록시 서버를 인증 tooAzure AD 설치 하는 동안 실패할 수 있는 경우 취소 됩니다.
* SQL Server SA(시스템 관리자)가 아닌 경우 전체 SQL Server 인스턴스를 사용하여 Azure AD Connect 이전 릴리스를 업데이트하면 업데이트가 실패합니다.
* 원격 SQL Server와 Azure AD Connect의 이전 릴리스에서 업데이트 hello "없습니다 tooaccess ADSync SQL 데이터베이스를 hello" 오류를 보여 줍니다.

## <a name="1091250"></a>1.0.9125.0
릴리스 날짜: 2015년 11월

**새로운 기능:**

* AD FS tooAzure AD 트러스트를 다시 구성할 수 있습니다.
* 수 hello Active Directory 스키마를 새로 고치고 동기화 규칙을 다시 생성 합니다.
* 동기화 규칙을 사용하지 않도록 설정할 수 있습니다.
* 동기화 규칙에서 새 리터럴로 "AuthoritativeNull"을 정의할 수 있습니다.

**새로운 미리 보기 기능:**

* [동기화를 위한 Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).
* [Azure AD 도메인 서비스](../active-directory-passwords-update-your-own-password.md) 암호 동기화를 지원합니다.

**지원되는 새 시나리오:**

* 여러 온-프레미스 Exchange 조직을 지원합니다. 자세한 내용은 [여러 Active Directory 포리스트가 있는 하이브리드 배포](https://technet.microsoft.com/library/jj873754.aspx)를 참조하세요.

**수정된 문제:**

* 암호 동기화 문제:
  * 범위를 벗어난 tooin 범위에서 이동 하는 개체 동기화 된 암호를 갖지 않습니다. 여기에는 OU와 특성 필터링이 모두 포함됩니다.
  * 새 OU tooinclude 동기화를 선택 하면 전체 암호 동기화는 필요 하지 않습니다.
  * 사용할 수 없는 사용자가 설정 된 경우 hello 암호 동기화 하지는 않습니다.
  * hello 암호 재시도 큐는 무한대 및 사용 중지 하는 5, 000 개체 toobe의 hello 이전 제한이 제거 되었습니다.
* 포리스트 기능 수준이 Windows Server 2016 수 없습니다. tooconnect tooActive 디렉터리입니다.
* Hello 초기 설치 후 그룹 필터링에 사용 되는 수 없습니다. toochange hello 그룹입니다.
* 더 이상 사용 하도록 설정 하는 암호 쓰기 저장을 사용 하 여 암호 변경을 수행 하는 모든 사용자에 대해 Azure AD Connect 서버 hello에 새 사용자 프로필을 만듭니다.
* 수 없습니다. toouse 정수 (Long) 값은 동기화 규칙 범위.
* hello 확인란 "장치 쓰기 저장" 연결할 수 없는 도메인 컨트롤러가 있는 경우 사용할 수 없는 상태로 유지 됩니다.

## <a name="1086670"></a>1.0.8667.0
릴리스 날짜: 2015년 8월

**새로운 기능:**

* 설치 마법사는 이제 Azure AD Connect hello tooall Windows Server 언어 지역화 됩니다.
* Azure AD 암호 관리 사용 시 계정 잠금 해제에 대한 지원이 추가되었습니다.

**수정된 문제:**

* Azure AD Connect 설치 마법사는 다른 사용자를 먼저 hello 설치를 시작한 hello 사용자 대신 설치 계속 되 면 충돌 합니다.
* Azure AD Connect 제거 하는 이전 toouninstall Azure AD Connect 동기화를 완전히 실패할 경우 가능한 tooreinstall 않습니다.
* Hello 사용자 hello hello 포리스트의 루트 도메인에 없는 경우 또는 Active Directory의 영어 이외의 버전을 사용 하는 경우에 빠른 설치를 사용 하 여 Azure AD Connect를 설치할 수 없습니다.
* Hello hello Active Directory 사용자 계정의 FQDN을 확인할 수 없으면 "Failed toocommit hello 스키마"에 잘못 된 오류 메시지가 표시 됩니다.
* Hello 마법사 외부 hello Active Directory Connector에 사용 되는 hello 계정을 변경 하는 경우 다음 번에 실행 hello 마법사가 실패 합니다.
* Azure AD Connect tooinstall 도메인 컨트롤러에 실패합니다.
* 확장 특성을 추가하지 않은 경우 “스테이징 모드"를 활성화 및 비활성화할 수 없습니다.
* 암호 쓰기 저장 hello Active Directory Connector에서 잘못 된 암호 때문에 일부 구성에 실패합니다.
* 특성 필터링에 DN(고유 이름)이 사용되는 경우 DirSync를 업그레이드할 수 없습니다.
* 암호 재설정을 사용할 경우 CPU가 과도하게 사용됩니다.

**제거된 미리 보기 기능:**

* hello 미리 보기 기능 [사용자 쓰기 저장](active-directory-aadconnect-feature-preview.md#user-writeback) 미리 보기 고객의에서 의견에 따라 일시적으로 제거 되었습니다. 피드백을 제공 하는 hello 해결 해 왔습니다 후 나중에 다시 추가할 수 됩니다.

## <a name="1086410"></a>1.0.8641.0
릴리스 날짜: 2015년 6월

**Azure AD Connect의 초기 릴리스입니다.**

Azure AD Sync tooAzure AD에서에서 변경 된 이름을 연결 합니다.

**새로운 기능:**

* [Express 설정](active-directory-aadconnect-get-started-express.md) 설치
* [AD FS 구성](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs) 가능
* [DirSync에서 업그레이드](active-directory-aadconnect-dirsync-upgrade-get-started.md) 가능
* [실수로 인한 삭제 방지](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)
* [스테이징 모드](active-directory-aadconnectsync-operations.md#staging-mode)

**새로운 미리 보기 기능:**

* [사용자 쓰기 저장](active-directory-aadconnect-feature-preview.md#user-writeback)
* [그룹 쓰기 저장](active-directory-aadconnect-feature-preview.md#group-writeback)
* [장치 쓰기 저장](active-directory-aadconnect-feature-device-writeback.md)
* [디렉터리 확장](active-directory-aadconnect-feature-preview.md)

## <a name="104940501"></a>1.0.494.0501
릴리스 날짜: 2015년 5월

**새로운 요구 사항:**

* Azure AD Sync hello.NET Framework 버전 4.5.1 toobe 설치 해야 합니다.

**수정된 문제:**

* Azure Service Bus 연결 오류와 함께 Azure AD에서 비밀번호 쓰기 저장이 실패합니다.

## <a name="104910413"></a>1.0.491.0413
릴리스 날짜: 2015년 4월

**수정된 문제 및 향상된 기능:**

* hello 휴지통 사용 되 고 hello 포리스트에 여러 도메인이 있는 경우 Active Directory Connector hello 삭제를 올바르게 처리 하지 않습니다.
* Azure Active Directory Connector hello에 대 한 가져오기 작업의 hello 성능이 향상 되었습니다.
* 그룹 hello 구성원 한도 초과 했습니다 때 (기본적으로 hello 제한 설정 too50, 000 개체), hello 그룹이 Azure Active Directory에서 삭제 되었습니다. Hello 새 동작으로 hello 그룹이 삭제 되지 않습니다, 예외가 발생 및 새로운 구성원 변경 내용이 내보내지 않습니다.
* 동일한 DN이 이미 hello 가진 스테이징된 된 삭제가 커넥터 공간 hello에에서 제공 하는 경우 새 개체를 프로비저닝할 수 없습니다.
* 일부 개체는 hello 개체에 위치 하는 변경 되지 않은 경우에 델타 동기화 하는 동안 동기화에 표시 됩니다.
* 암호 동기화를 강제로 hello 기본 설정 DC 목록도 제거 됩니다.
* CSExportAnalyzer에 일부 개체 상태에 문제가 있습니다.

**새로운 기능:**

* 조인을 너무 ""에서 해당 개체 유형 hello MV 이제 연결할 수 있습니다.

## <a name="104850222"></a>1.0.485.0222
릴리스 날짜: 2015년 2월

**향상된 기능:**

* 가져오기 성능이 향상되었습니다.

**수정된 문제:**

* 암호 동기화 특성을 필터링 하 여 사용 되는 hello cloudFiltered 특성을 준수 합니다. 필터링된 개체는 더 이상 암호 동기화 범위에 속하지 않습니다.
* 드물지만 hello 토폴로지 많은 도메인 컨트롤러에 암호 동기화 작동 하지 않습니다.
* Azure AD/Intune에서 "stopped-server" hello Azure AD 커넥터에서에서 장치 관리 한 후 가져올 때 설정 되었습니다.
* 동일한 포리스트 내 여러 도메인으로부터 외부 보안 주체(FSP)를 조인하면 모호한 오류가 발생합니다.

## <a name="104751202"></a>1.0.475.1202
릴리스 날짜: 2014년 12월

**새로운 기능:**

* 이제 특성 기반 필터링을 사용하는 암호 동기화가 지원됩니다. 자세한 내용은 [필터링으로 암호 동기화](active-directory-aadconnectsync-configure-filtering.md)를 참조하세요.
* hello Msds-externaldirectoryobjectid 특성 tooActive 디렉터리 다시 기록 됩니다. 이 기능을 통해 Office 365 응용 프로그램에 대한 지원이 추가됩니다. OAuth2 tooaccess 하이브리드 Exchange 배포의 온라인 및 온-프레미스 사서함을 사용합니다.

**수정된 업그레이드 문제:**

* Hello 로그인 도우미 새 버전이 hello 서버에서 사용할 수 있습니다.
* 사용자 지정 설치 경로 사용 하는 Azure AD Sync tooinstall 했습니다.
* 잘못 된 사용자 지정 조인 조건 블록 hello 업그레이드입니다.

**기타 수정 사항:**

* Office Pro Plus에 대 한 고정된 hello 템플릿입니다.
* 대시로 시작하는 사용자 이름에 의해 발생한 설치 문제가 수정되었습니다.
* Hello 설치 마법사를 두 번 실행 하는 경우 무시 되 hello sourceAnchor 설정을 수정 했습니다.
* 암호 동기화를 위한 ETW 추적이 수정되었습니다.

## <a name="104701023"></a>1.0.470.1023
릴리스 날짜: 2014년 10월

**새로운 기능:**

* 암호 동기화 여러에서 온-프레미스 Active Directory tooAzure AD.
* 지역화 된 설치 UI tooall Windows Server 언어입니다.

**AADSync 1.0 GA에서 업그레이드**

설치 된 Azure AD Sync를 이미 있는 경우 한 단계 hello 기본 제공 동기화 규칙을 하나라도 변경한 경우 tootake가 있습니다. 1.0.470.1023 toohello 릴리스를 업그레이드 한 후 수정한 hello 동기화 규칙이 복제 됩니다. 각 수정 된 동기화 규칙에 대해 수행 hello 다음:

1.  Hello 동기화 규칙을 수정한 다음 hello 변경 내용을 기록를 찾습니다.
* Hello 동기화 규칙을 삭제 합니다.
* Azure AD Sync에 의해 만들어진 hello 새 동기화 규칙을 찾은 다음 hello 변경 내용을 다시 적용 합니다.

**Hello Active Directory 계정에 대 한 사용 권한**

Active Directory 계정 hello는 Active Directory에서 추가 사용 권한을 toobe 수 tooread hello 암호 해시 부여 되어야 합니다. hello 권한을 toogrant "디렉터리 변경 복제" 라고 하 고 "디렉터리 변경 모두 복제 합니다." 두 사용 권한이 필요한 toobe 수 tooread hello 암호 해시를 않습니다.

## <a name="104190911"></a>1.0.419.0911
릴리스 날짜: 2014년 9월

**Azure AD Sync의 초기 릴리스**

## <a name="next-steps"></a>다음 단계
[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.
