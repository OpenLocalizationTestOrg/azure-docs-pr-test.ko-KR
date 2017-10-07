---
title: "Azure AD Connect: 지원되는 토폴로지 | Microsoft Docs"
description: "이 항목은 Azure AD Connect에 대해 지원되고 지원되지 않는 토폴로지에 대해 자세히 설명합니다."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 1034c000-59f2-4fc8-8137-2416fa5e4bfe
ms.service: active-directory
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: identity
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 41632a54e8e85492fbf1a751ef4e618c8870abe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="topologies-for-azure-ad-connect"></a>Azure AD Connect에 대한 토폴로지
이 문서에서는 다양 한 온-프레미스와 Azure AD Connect 동기화를 사용 하 여 hello 주요 통합 솔루션으로 Azure Active Directory (Azure AD) 토폴로지를 설명 합니다. 이 문서에는 지원되는 구성과 지원되지 않는 구성이 포함되어 있습니다.

Hello 범례에서 나오는 그림 hello 문서에는 다음과 같습니다.

| 설명 | 기호 |
| --- | --- |
| 온-프레미스 Active Directory 포리스트 |![온-프레미스 Active Directory 포리스트](./media/active-directory-aadconnect-topologies/LegendAD1.png) |
| 필터링된 가져오기를 사용한 온-프레미스 Active Directory |![필터링된 가져오기를 사용한 Active Directory](./media/active-directory-aadconnect-topologies/LegendAD2.png) |
| Azure AD Connect Sync 서버 |![Azure AD Connect Sync 서버](./media/active-directory-aadconnect-topologies/LegendSync1.png) |
| Azure AD Connect Sync 서버 “스테이징 모드” |![Azure AD Connect Sync 서버 “스테이징 모드”](./media/active-directory-aadconnect-topologies/LegendSync2.png) |
| FIM(Forefront Identity Manager) 2010 또는 MIM(Microsoft Identity Manager) 2016을 사용하는 GALSync |![FIM 2010 또는 MIM 2016을 사용하는 GALSync](./media/active-directory-aadconnect-topologies/LegendSync3.png) |
| Azure AD Connect Sync 서버, 자세히 설명됨 |![Azure AD Connect Sync 서버, 자세히 설명됨](./media/active-directory-aadconnect-topologies/LegendSync4.png) |
| Azure AD |![Azure Active Directory](./media/active-directory-aadconnect-topologies/LegendAAD.png) |
| 지원되지 않는 시나리오 |![지원되지 않는 시나리오](./media/active-directory-aadconnect-topologies/LegendUnsupported.png) |

## <a name="single-forest-single-azure-ad-tenant"></a>단일 포리스트, 단일 Azure AD 테넌트
![단일 포리스트 및 단일 테넌트에 대한 토폴로지](./media/active-directory-aadconnect-topologies/SingleForestSingleDirectory.png)

hello 가장 일반적인 토폴로지에서 단일 온-프레미스 포리스트, 하나 또는 여러 도메인과 단일 Azure AD 테 넌 트입니다. Azure AD 인증을 위해 암호 동기화가 사용됩니다. Azure AD Connect의 hello 빠른 설치에는이 토폴로지에 지원합니다.

### <a name="single-forest-multiple-sync-servers-tooone-azure-ad-tenant"></a>단일 포리스트, 여러 동기화 서버 tooone Azure AD 테 넌
![단일 포리스트에 지원되지 않는 필터링된 토폴로지](./media/active-directory-aadconnect-topologies/SingleForestFilteredUnsupported.png)

에 대 한 제외를 여러 Azure AD Connect 동기화 서버를 연결 된 toohello 동일한 Azure AD 테 넌 트 지원 되지 않습니다는 데는 [서버를 준비 하](#staging-server)합니다. 이러한 서버는 구성 된 toosynchronize 상호 배타적인 개체 집합이 있는 경우에 지원 되지 않는 있습니다. 수 고려이 토폴로지는 단일 서버에서 hello 포리스트의 모든 도메인에에서 연결할 수 없는 경우 또는 여러 서버 toodistribute 부하를 사용 하려는 경우.

## <a name="multiple-forests-single-azure-ad-tenant"></a>여러 포리스트, 단일 Azure AD 테넌트
![여러 포리스트 및 단일 테넌트에 대한 토폴로지](./media/active-directory-aadconnect-topologies/MultiForestSingleDirectory.png)

많은 조직에는 다중 온-프레미스 Active Directory 포리스트가 있는 환경이 있습니다. 둘 이상의 온-프레미스 Active Directory 포리스트가 있는 이유는 여러 가지가 있습니다. 일반적인 예로 계정-리소스 포리스트 및 hello 결과 합병 이나 인수를 사용 하 여 설계는 있습니다.

포리스트가 여러 개인 경우 단일 Azure AD Connect Sync 서버에서 모든 포리스트에 연결할 수 있어야 합니다. Toojoin hello 서버 tooa 도메인이 필요는 없습니다. 하는 경우 필요한 tooreach 모든 포리스트에 hello 서버 경계 네트워크 (DMZ, 완충 지역 및 라고도 스크린 된 서브넷)에 배치할 수 있습니다.

hello Azure AD Connect 설치 마법사는 여러 옵션 tooconsolidate 사용자가 여러 포리스트에 표시를 제공 합니다. hello ֲ 사용자 Azure AD에서 한 번만 표시 됩니다. Hello 설치 마법사의 사용자 지정 설치 경로 hello에 구성할 수 있는 몇 가지 일반적인 토폴로지에 있습니다. Hello에 **고유 하 게 식별 하는 사용자가** 토폴로지에 나타내는 선택 hello 해당 옵션 페이지입니다. hello 통합 사용자에 대해서만 구성 됩니다. 중복 된 그룹 hello 기본 구성으로 통합 되지 됩니다.

에 대 한 일반적인 토폴로지에 hello 섹션에서 설명 [토폴로지 분리](#multiple-forests-separate-topologies), [메시 전체](#multiple-forests-full-mesh-with-optional-galsync), 및 [계정-리소스 토폴로지 hello](#multiple-forests-account-resource-forest)합니다.

Azure AD Connect 동기화의 기본 구성에서는 hello 가정합니다.

* 각 사용자에 게 하나만 활성화 된 계정이 되며이 계정은 위치한 hello 포리스트 사용 되는 tooauthenticate hello 사용자입니다. 이 가정은 암호 동기화 및 페더레이션에 모두 적용됩니다. UserPrincipalName 및 sourceAnchor/immutableID는 이 포리스트에서 제공됩니다.
* 사용자마다 사서함이 하나씩만 제공됩니다.
* 사용자에 대 한 hello 사서함을 호스트 하는 hello 포리스트의 hello Exchange GAL 주소 목록 ()에 표시 되는 특성에 대 한 최상의 데이터 품질 hello에 있습니다. 모든 포리스트에 사용된 toocontribute 수 hello 사용자에 대 한 사서함 이면 이러한 특성 값입니다.
* 연결된 사서함이 있으면 로그인에 사용되는 다른 포리스트에도 계정이 있습니다.

사용자 환경에서 이러한 가정와 일치 하지 않는 경우 hello 다음 작업이 수행 됩니다.

* 둘 이상의 활성 계정 또는 둘 이상의 사서함 있다면 hello 동기화 엔진이 하나를 선택 하 고 다른 hello를 무시 합니다.
* 다른 활성 계정이 없으면를 사용 하 여 연결 된 사서함 내보낸된 tooAzure AD 아닙니다. 모든 그룹의 구성원으로 hello 사용자 계정이 표시 되지 않습니다. DirSync에 있는 연결된 사서함은 항상 일반 사서함으로 표시됩니다. 이 변경은 의도적으로 다른 동작이 toobetter 지원 다중 포리스트 시나리오입니다.

자세한 정보를 찾을 수 있습니다 [hello 기본 구성 이해](active-directory-aadconnectsync-understanding-default-configuration.md)합니다.

### <a name="multiple-forests-multiple-sync-servers-tooone-azure-ad-tenant"></a>다중 포리스트, 여러 동기화 서버 tooone Azure AD 테 넌
![다중 포리스트 및 다중 동기화 서버에 지원되지 않는 토폴로지](./media/active-directory-aadconnect-topologies/MultiForestMultiSyncUnsupported.png)

단일 Azure AD 테 넌 트 둘 이상의 Azure AD Connect 동기화 연결 된 서버 tooa 것은 지원 되지 않습니다. hello 예외는 hello 사용은 [서버를 준비 하](#staging-server)합니다.

### <a name="multiple-forests-separate-topologies"></a>다중 포리스트, 별도의 토폴로지
![모든 디렉터리에서 사용자를 한 번만 표시하는 옵션](./media/active-directory-aadconnect-topologies/MultiForestUsersOnce.png)

![다중 포리스트 및 별도의 토폴로지에 대한 설명](./media/active-directory-aadconnect-topologies/MultiForestSeperateTopologies.png)

이 환경에서는 모든 온-프레미스 포리스트가 별도의 엔터티로 처리됩니다. 사용자가 다른 포리스트에 표시되지 않습니다. 각 포리스트에 자체 Exchange 조직을 않았으며 hello 포리스트 간에 GALSync 없음이 됩니다. 이 토폴로지 hello 상황 인수 및 합병 후 또는 조직에 있는 각 사업 부서가 무관 하 게 작동 될 수 있습니다. Azure AD의 동일한 조직 hello 고 통합된 GAL와 함께이 포리스트는에 있습니다. 앞 그림 hello, 모든 포리스트에 있는 각 개체 hello 메타 버스에서 한 번만 표시 하 고 hello 대상 Azure AD 테 넌 트에 집계 됩니다.

### <a name="multiple-forests-match-users"></a>다중 포리스트, 사용자 일치
일반적인 tooall 이러한 시나리오는 해당 배포 및 보안 그룹에는 다양 한 사용자, 연락처 및 (Fsp)에 외부 보안 주체 포함 될 수 있습니다. Fsp 보안 그룹의 다른 포리스트의 Active Directory 도메인 서비스 (AD DS) toorepresent 멤버에 사용 됩니다. 모든 Fsp 해결된 toohello 실제 개체가 Azure AD는 있습니다.

### <a name="multiple-forests-full-mesh-with-optional-galsync"></a>다중 포리스트: GALSync 선택 사항이 제공되는 전체 메시
![사용자 id가 여러 디렉터리 때 일치 하는 hello 메일 특성을 사용 하기 위한 옵션](./media/active-directory-aadconnect-topologies/MultiForestUsersMail.png)

![다중 포리스트를 위한 전체 메시 토폴로지](./media/active-directory-aadconnect-topologies/MultiForestFullMesh.png)

풀 메시 토폴로지 사용자와 리소스 toobe 원하는 포리스트에 배치할 수 있습니다. 일반적으로 hello 포리스트 간에 양방향 트러스트 됩니다.

둘 이상의 포리스트에 Exchange가 있으면 온-프레미스 GALSync 솔루션이 선택적으로 제공될 수 있습니다. 그러면 모든 사용자는 그 외의 모든 포리스트에 연락처로 표시됩니다. GALSync는 일반적으로 FIM 2010 또는 MIM 2016을 통해 구현됩니다. Azure AD Connect를 온-프레미스 GALSync에 사용할 수 없습니다.

이 시나리오에서는 id 개체 hello 메일 특성을 통해 조인 됩니다. Hello에 hello 연락처 조인 하나의 포리스트에 사서함을 가진 사용자가 다른 포리스트의 합니다.

### <a name="multiple-forests-account-resource-forest"></a>다중 포리스트: 계정 리소스 포리스트
![Id가 여러 디렉터리 때 일치 하는 hello ObjectSID 및 msExchMasterAccountSID 특성 사용에 대 한 옵션](./media/active-directory-aadconnect-topologies/MultiForestUsersObjectSID.png)

![다중 포리스트를 위한 계정 리소스 포리스트 토폴로지](./media/active-directory-aadconnect-topologies/MultiForestAccountResource.png)

계정 리소스 포리스트 토폴로지에는 활성 사용자 계정이 있는 하나 이상의 *계정* 포리스트가 있습니다. 또한 계정이 비활성화된 하나 이상의 *리소스* 포리스트가 있습니다.

이 시나리오에서는 하나 이상의 리소스 포리스트가 모든 계정 포리스트를 신뢰합니다. hello 리소스 포리스트는 일반적으로 Exchange 및 Lync와 확장된 된 Active Directory 스키마를 있습니다. 다른 공유 서비스는 물론이고 모든 Exchange 및 Lync 서비스도 이 포리스트에 배치됩니다. 사용자가 사용할 수 없는 사용자 계정이이 포리스트에 및 연결 된 hello 사서함 toohello 계정 포리스트 합니다.

## <a name="office-365-and-topology-considerations"></a>Office 365 및 토폴로지 고려 사항
일부 Office 365 워크로드의 경우 지원되는 토폴로지에 약간의 제한이 있습니다.

| 워크로드 | 제한 |
--------- | ---------
| Exchange Online | 둘 이상의 온-프레미스 Exchange 조직의 경우 (즉, Exchange에 배포 된 toomore 한 포리스트의 보다)를 수행한 Exchange 2013 s p 1을 사용 해야 이상. 자세한 내용은 [여러 Active Directory 포리스트가 있는 하이브리드 배포](https://technet.microsoft.com/library/jj873754.aspx)를 참조하세요. |
| 비즈니스용 Skype | 여러 온-프레미스 포리스트를 사용 하는 경우에 hello 계정-리소스 포리스트 토폴로지는 지원 됩니다. 자세한 내용은 [Business Server 2015용 Skype에 대한 환경 요구 사항](https://technet.microsoft.com/library/dn933910.aspx)을 참조하세요. |


## <a name="staging-server"></a>스테이징 서버
![토폴로지의 준비 서버](./media/active-directory-aadconnect-topologies/MultiForestStaging.png)

Azure AD Connect는 *준비 모드*에서 두 번째 서버의 설치를 지원합니다. 이 모드의 서버에에서 연결 된 모든 디렉터리에서 데이터를 읽고 하지만 tooconnected 디렉터리 작성지 않습니다 아무 것도 합니다. Hello 기본적인 동기화 주기를 사용 하며 따라서 hello id 데이터의 업데이트 된 복사본을 포함.

Hello 주 서버 실패 하면 재해 서버를 준비 하는 toohello 조치할 수 있습니다. Hello Azure AD Connect 마법사에서이 작업을 수행 합니다. 이 두 번째 서버 hello 주 서버와 공유 인프라가 없는 다른 데이터 센터에 있을 수 있습니다. 두 번째 서버를 toohello hello 주 서버에서 구성 변경 내용을 수동으로 복사 해야 합니다.

준비 서버 tootest 새 사용자 지정 구성 및 hello 되는 효과이 데이터에 사용할 수 있습니다. Hello 변경 내용을 미리 볼 수 있으며 hello 구성을 조정할 수 있습니다. Hello 새 구성을 사용 하 여 만족 했으면 hello 서버 hello 활성 서버를 준비 하 고 hello 오래 된 활성 서버 toostaging 모드를 설정할 수 있습니다.

이 메서드 tooreplace hello active sync 서버를 사용할 수 있습니다. Hello 새 서버를 준비 하 고 toostaging 모드를 설정 합니다. 준비 모드 (활성화 될 때 해당), 사용 안 함 라는 상태가 정상 인지 확인 한 hello 현재 활성 서버를 종료 합니다.

다른 데이터 센터에서 여러 백업 toohave를 사용할 때 스테이징 서버를 하나 이상 가능한 toohave입니다.

## <a name="multiple-azure-ad-tenants"></a>여러 Azure AD 테넌트
조직의 Azure AD에 테넌트를 하나만 보유할 것을 권장합니다.
여러 Azure AD 테 넌 트 toouse를 계획 하기 전에 hello 문서 참조 [Azure AD의 관리 단위 관리](../active-directory-administrative-units-management.md)합니다. 단일 테넌트를 사용할 수 있는 일반적인 시나리오에 대해 설명되어 있습니다.

![다중 포리스트 및 다중 테넌트를 위한 토폴로지](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectory.png)

Azure AD Connect Sync 서버와 Azure AD 테넌트가 1:1 관계입니다. 각 Azure AD 테넌트에 하나의 Azure AD Connect 동기화 서버 설치가 필요합니다. hello Azure AD 테 넌 트 인스턴스 설계와 격리 됩니다. 즉, 한 테 넌 트의 사용자가 hello에 대 한 사용자가 다른 테 넌 트를 볼 수 없습니다. 이러한 격리를 원하는 경우 이 구성이 지원됩니다. Hello를 사용 해야 하는 그렇지 않은 경우 Azure AD 테 넌 트 모델을 단일 합니다.

### <a name="each-object-only-once-in-an-azure-ad-tenant"></a>Azure AD 테넌트에서 각 개체가 한 번만
![단일 포리스트에 대한 필터링된 토폴로지](./media/active-directory-aadconnect-topologies/SingleForestFiltered.png)

이 토폴로지의 경우 하나의 Azure AD Connect 동기화 서버는 연결 된 tooeach Azure AD 테 넌 트입니다. 각 보안 개체 toooperate의 상호 배타적인 집합 있도록 hello Azure AD Connect 동기화 서버를 필터링에 대 한 구성 되어야 합니다. 예를 들어, 각 서버 tooa 특정 도메인 또는 조직 구성 단위 범위 수 있습니다.

DNS 도메인은 단일 Azure AD 테넌트에만 등록할 수 있습니다. hello hello 온-프레미스 Active Directory 인스턴스에서 hello 사용자의 Upn 별도 네임 스페이스를 사용 해야 합니다. 예를 들어 hello 앞 그림에 세 개의 별도 UPN 접미사에에서 등록 되어 있는 hello 온-프레미스 Active Directory 인스턴스에: contoso.com, fabrikam.com을 및 부모입니다. hello 사용자가 각 온-프레미스 Active Directory 도메인에 다른 네임 스페이스를 사용 합니다.

Hello Azure AD 테 넌 트 인스턴스 간에 GALSync 없는 경우 사용자에 게 hello 동일한 테 넌 트에만 비즈니스 표시에 대 한 Exchange Online 및 Skype에서 주소록을 hello 합니다.

이 토폴로지는 hello 다음 다른 방법에 대 한 제한 지원 되는 시나리오:

* Hello Azure AD 테 넌 트 중 하나에만 hello 온-프레미스 Active Directory 인스턴스와 Exchange 하이브리드 사용 가능 합니다.
* Windows 10 장치는 하나의 Azure AD 테넌트에만 연결할 수 있습니다.
* hello single sign-on (SSO) 옵션 암호 동기화 및 통과 인증을 위해 Azure AD 테 넌 트를 하나만 사용할 수 있습니다.

개체의 상호 배타적인 집합에 대 한 hello 요구 사항에는 toowriteback도 적용 됩니다. 이 토폴로지는 단일 온-프레미스 구성을 전제로 하기 때문에 일부 쓰기 저장 기능이 지원되지 않습니다. 이러한 기능으로는 다음이 포함됩니다.

* 기본 구성으로 쓰기 저장 그룹화.
* 장치 쓰기 저장.

### <a name="each-object-multiple-times-in-an-azure-ad-tenant"></a>Azure AD 테넌트에서 각 개체가 여러 번
![단일 포리스트 및 다중 테넌트를 지원하지 않는 토폴로지](./media/active-directory-aadconnect-topologies/SingleForestMultiDirectoryUnsupported.png) ![단일 포리스트 및 다중 커넥터를 지원하지 않는 토폴로지](./media/active-directory-aadconnect-topologies/SingleForestMultiConnectorsUnsupported.png)

다음 작업은 지원되지 않습니다.

* 동기화 hello 동일 사용자 toomultiple Azure AD 테 넌 트입니다.
* 한 Azure AD 테넌트의 사용자가 다른 Azure AD 테넌트에 연락처로 표시되도록 구성 변경.
* Azure AD Connect 동기화 tooconnect toomultiple Azure AD 테 넌 트를 수정 합니다.

### <a name="galsync-by-using-writeback"></a>쓰기 저장을 사용한 GALSync
![다중 포리스트 및 다중 디렉터리를 지원하지 않는 토폴로지, Azure AD에 집중하는 GALSync 사용](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync1Unsupported.png) ![다중 포리스트 및 다중 디렉터리를 지원하지 않는 토폴로지, 온-프레미스 Active Directory에 집중하는 GALSync 사용](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync2Unsupported.png)

Azure AD 테넌트는 서로 격리되도록 설계되었습니다. 다음 작업은 지원되지 않습니다.

* 다른 Azure AD 테 넌 트의 Azure AD Connect 동기화 tooread 데이터의 변경 hello 구성입니다.
* Azure AD Connect 동기화를 사용 하 여 연락처 tooanother 온-프레미스 Active Directory 인스턴스와 사용자가 내보냅니다.

### <a name="galsync-with-on-premises-sync-server"></a>온-프레미스 동기화 서버로 GALSync
![다중 포리스트 및 다중 디렉터리를 위한 토폴로지의 GALSync](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync.png)

FIM 2010 또는 MIM 2016 온-프레미스 toosync 사용자 (GALSync)를 통해 두 Exchange 조직 간에 사용할 수 있습니다. 한 조직의 hello 사용자가 다른 조직의 hello 외래 사용자/연락처에 표시 합니다. 이러한 여러 온-프레미스 Active Directory 인스턴스를 각각 자체 Azure AD 테넌트와 동기화할 수 있습니다.

## <a name="next-steps"></a>다음 단계
이러한 시나리오에 대 한 Azure AD Connect tooinstall 참조 toolearn [Azure AD Connect의 사용자 지정 설치](active-directory-aadconnect-get-started-custom.md)합니다.

Hello에 대 한 자세한 [Azure AD Connect 동기화](active-directory-aadconnectsync-whatis.md) 구성 합니다.

[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.
