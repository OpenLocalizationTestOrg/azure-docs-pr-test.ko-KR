---
title: "Azure AD Connect: 이전 버전에서 업그레이드 | Microsoft Docs"
description: "Hello 다양 한 방법을 tooupgrade toohello 최신 버전의 Azure Active Directory Connect를 전체 업그레이드 및 회전 마이그레이션을 포함 하 여 설명 합니다."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 31f084d8-2b89-478c-9079-76cf92e6618f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 57bd5b094654e4983cafa303b6f3daecadafb01c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-upgrade-from-a-previous-version-toohello-latest"></a>이전 버전 toohello 최신 버전에서 azure AD Connect: 업그레이드
이 항목에서는 hello 사용할 수 있는 tooupgrade Azure Active Directory (Azure AD) Connect 설치 toohello 최신 릴리스에 여러 가지 방법을 설명 합니다. 유지 하는 사용자가 직접 Azure AD Connect의 hello 릴리스와의 현재 하는 것이 좋습니다. Hello에 hello 단계를 사용할 수도 [마이그레이션 돌려](#swing-migration) 상당한 구성을 변경 하는 경우 섹션.

DirSync에서 tooupgrade 참조 [Azure AD 동기화 도구 (DirSync)에서 업그레이드](active-directory-aadconnect-dirsync-upgrade-get-started.md) 대신 합니다.

몇 가지 전략 tooupgrade Azure AD Connect를 사용할 수 있습니다.

| 메서드 | 설명 |
| --- | --- |
| [자동 업그레이드](active-directory-aadconnect-feature-automatic-upgrade.md) |빠른 설치를 사용 하는 고객에 대 한 hello 가장 쉬운 방법입니다. |
| [전체 업그레이드](#in-place-upgrade) |에 내부에서 hello 설치를 업그레이드할 수는 단일 서버를 설정한 경우 같은 서버 hello 합니다. |
| [스윙 마이그레이션](#swing-migration) |두 명의 서버와 hello 새 릴리스 또는 구성, hello 서버 중 하나를 준비 하 고 준비가 hello 활성 서버를 변경할 수 있습니다. |

사용 권한 정보에 대 한 참조 hello [업그레이드에 필요한 사용 권한을](active-directory-aadconnect-accounts-permissions.md#upgrade)합니다.

> [!NOTE]
> 에 새 Azure AD Connect 서버 toostart 동기화 중 변경 내용을 tooAzure AD를 사용 하도록 설정한 후 하지 롤백해야 toousing DirSync 또는 Azure AD Sync 합니다. 디렉터리 동기화 및 Azure AD Sync를 포함 하 여 Azure AD Connect toolegacy 클라이언트로부터 다운 그레이드이 지원 되지 않으며 Azure AD에서 tooissues 데이터 손실 될 수 있습니다.

## <a name="in-place-upgrade"></a>전체 업그레이드
전체 업그레이드는 Azure AD Sync 또는 Azure AD Connect에서 이동하는 경우에 작동합니다. FIM(Forefront Identity Manager) + Azure AD 커넥터를 사용하는 솔루션이거나 DirSync에서 이동하는 경우에는 작동하지 않습니다.

이 방법은 단일 서버가 있고 개체 수가 100,000개 미만인 경우에 사용하는 것이 좋습니다. Toohello 기본 제공 동기화 규칙에 변경한 경우 전체 가져오기 및 전체 동기화 hello 업그레이드 후에 발생 합니다. 이 방법을 사용 하면 해당 hello 새 구성이 적용된 tooall 기존 개체 hello 시스템에 있습니다. 이 실행 hello hello 동기화 엔진의 범위에 있는 개체 수에 따라 몇 시간이 걸릴 수 있습니다. hello 일반 델타 동기화 스케줄러 (기본적으로 30 분 마다 동기화)를 일시 중단 되지만 암호 동기화가 계속 됩니다. 주말과 hello 전체 업그레이드를 수행 하는 것이 좋습니다. Hello 새 Azure AD Connect 릴리스마다 변경 toohello 기본적으로 구성 없이 있는 경우 다음 일반 델타 가져오기/동기화 시작 대신 합니다.  
![전체 업그레이드](./media/active-directory-aadconnect-upgrade-previous-version/inplaceupgrade.png)

변경 내용을 toohello 기본 제공 동기화 규칙을 만든 경우 다음 이러한 규칙은 다시 설정 toohello 기본 구성 업그레이드 시. toomake 간의 업그레이드, 구성에 유지 되도록 확인을에서 설명 하는 대로 변경 하 [hello 기본 구성 변경에 대 한 유용한](active-directory-aadconnectsync-best-practices-changing-default-configuration.md)합니다.

현재 위치 업그레이드 하는 동안 있을 수 있습니다 특정 동기화 (전체 가져오기 단계와 완전히 동기화 단계 포함) 활동 toobe 업그레이드가 완료 된 후 실행 해야 하는 변경 내용이 도입 되었습니다. toodefer 등의 작업 참조 toosection [어떻게 toodefer 전체 업그레이드 후 동기화](#how-to-defer-full-synchronization-after-upgrade)합니다.

## <a name="swing-migration"></a>스윙 마이그레이션
복잡 한 배포 또는 여러 개체를 설정한 경우에 비현실적 toodo hello 라이브 시스템에서의 전체 업그레이드가 수 있습니다. 일부 고객의 경우 처리하는 데 며칠이 걸리고 이 시간 동안 델타 변경이 처리되지 않습니다. Toomake 변경이 tooyour 구성을 계획 하 고 tootry 하려고 할 때이 메서드를 사용할 수도 toohello 클라우드를 푸시되는 전에 아웃 합니다.

이러한 시나리오에 대 한 메서드를 권장 하는 hello toouse 회전 마이그레이션입니다. 활성 서버 하나와 스테이징 서버 하나, (적어도) 두 개의 서버가 필요합니다. hello 활성 서버 (다음 그림 hello에서 파란색 실선으로 표시)는 hello 활성 프로덕션 부하에 대 한 합니다. 새 릴리스 hello 또는 구성 (자주색 파선으로 표시) 서버를 준비 하는 hello 준비가 되어 있습니다. 완벽하게 준비되면 이 서버가 활성 상태가 됩니다. hello 이전 활성 서버에 이제 hello 이전 버전 또는 설치 된 구성, 서버를 준비 하는 hello로 만들어질 및 업그레이드 됩니다.

hello 두 서버는 서로 다른 버전을 사용할 수 있습니다. 예를 들어 toodecommission 계획 hello 활성 서버에는 Azure AD Sync를 사용 하 여 및 hello 새 스테이징 서버에서 Azure AD Connect를 사용할 수 있습니다. 회전 마이그레이션 toodevelop를 사용 하는 경우 새 구성 하는 것이 좋습니다 toohave에 동일한 버전 hello 두 대의 서버 hello 합니다.  
![스테이징 서버](./media/active-directory-aadconnect-upgrade-previous-version/stagingserver1.png)

> [!NOTE]
> 일부 고객이이 시나리오에 대 한 3 또는 4 toohave 서버를 선호합니다. 에 대 한 백업 서버 없는 서버를 준비 하는 hello를 업그레이드할 경우 [재해 복구](active-directory-aadconnectsync-operations.md#disaster-recovery)합니다. 3 ~ 4 개의 서버와 하나의 주/대기 서버는 항상 준비 tootake 스타일러스가 준비 서버를 보장 하는 hello 새 버전으로 집합을 준비할 수 있습니다.

이러한 단계는 Azure AD Sync 또는 FIM + Azure AD 커넥터를 사용 하 여 솔루션에서 toomove 에서도 작동 합니다. 이러한 단계는 디렉터리 동기화 작업 하지는 않지만 동일한 회전 마이그레이션 방법 (병렬 배포 라고도 함)와 디렉터리 동기화에 대 한 단계 hello 중인 [업그레이드 Azure Active Directory로 동기화 (DirSync)](active-directory-aadconnect-dirsync-upgrade-get-started.md)합니다.

### <a name="use-a-swing-migration-tooupgrade"></a>회전 마이그레이션 tooupgrade를 사용 하 여
1. 서버와 계획 tooonly 사항을 구성 변경에 Azure AD Connect를 사용 하면 현재 서버와 준비 서버는 해야 모두 동일한 버전 hello를 사용 하 여 합니다. 따라서 보다 쉽게 toocompare 차이점 나중 합니다. Azure AD Sync에서 업그레이드하는 경우 두 서버는 서로 다른 버전을 사용하게 됩니다. Azure AD Connect의 이전 버전에서에서 업그레이드 하는 경우 hello 두 서버를 사용 하는 것이 좋습니다 toostart 동일한 버전을 hello를 사용 하 여 하지만 필요는 없습니다.
2. 사용자 지정 구성을 변경한 경우 스테이징 서버에 없는 경우 그 hello 단계를 따릅니다 [사용자 지정 구성에서 서버를 준비 하는 hello 활성 서버 toohello 이동](#move-custom-configuration-from-active-to-staging-server)합니다.
3. Azure AD Connect의 이전 버전에서에서 업그레이드 하는 경우 서버 toohello 최신 버전을 준비 하는 hello를 업그레이드 합니다. Azure AD Sync에서 전환하는 경우 스테이징 서버에 Azure AD Connect를 설치합니다.
4. Hello 동기화 엔진 실행에 대 한 전체 가져오기 및 준비 서버에서 전체 동기화를 사용 합니다.
5. 해당 hello 새 구성 하지 않은 변경 예기치 않은 hello "확인" 아래에 있는 단계를 사용 하 여 확인 [서버 hello 구성 확인](active-directory-aadconnectsync-operations.md#verify-the-configuration-of-a-server)합니다. 예상한 대로, 올바른 문제가 없는 경우 hello 가져오기 및 동기화를 실행, 고 hello 단계를 수행 하 여 적절 한 경우 표시 될 때까지 hello 데이터를 확인 합니다.
6. 서버 toobe hello 활성 서버를 준비 하는 hello를 전환 합니다. 이것이 hello 최종 단계 "스위치 active server" [서버 hello 구성 확인](active-directory-aadconnectsync-operations.md#verify-the-configuration-of-a-server)합니다.
7. Azure AD Connect를 업그레이드 하는 경우에 준비 단계 모드 toohello 최신 릴리스 이제 hello 서버를 업그레이드 합니다. Hello tooget hello 데이터와 구성 업그레이드 이전과 마찬가지로 동일한 단계를 따릅니다. Azure AD Sync에서 업그레이드 한 경우, 이제 이전 서버를 끄고 서비스 해제를 할 수 있습니다.

### <a name="move-a-custom-configuration-from-hello-active-server-toohello-staging-server"></a>사용자 지정 구성을 hello 활성 서버 toohello 스테이징 서버에서 이동
구성 변경 내용을 toohello 활성 서버를 변경한 경우 필요한 toomake 있는지 동일 hello 하는 변경 내용이 적용 된 toohello 서버를 준비 합니다. 이 toohelp 이동 hello를 사용할 수 있습니다 [Azure AD Connect 구성 데이터베이스 구조](https://github.com/Microsoft/AADConnectConfigDocumenter)합니다.

PowerShell을 사용 하 여 만든 hello 사용자 지정 동기화 규칙을 이동할 수 있습니다. 다른 변경 내용을 hello를 적용 해야 시스템 모두에서 있습니다 동일한 방식으로 hello 변경 내용을 마이그레이션할 수 없습니다. hello [구성 데이터베이스 구조](https://github.com/Microsoft/AADConnectConfigDocumenter) hello 두 시스템 toomake 증명이 동일한 지 비교 하는 데 도움이 됩니다. 이 섹션에서 제공 하는 hello 단계를 자동화 hello 도구 유용할 수 있습니다.

Tooconfigure hello 다음 필요한 작업 hello 동일한 방식으로 두 서버 모두에서:

* 연결 toohello 동일한 포리스트
* 모든 도메인 및 OU 필터링
* 암호 동기화 및 암호 쓰기 저장 등의 같은 선택적인 기능이 hello

**사용자 지정 동기화 규칙 이동**  
toomove 사용자 지정 동기화 규칙을 따르는 hello지 않습니다.

1. 활성 서버에서 **동기화 규칙 편집기** 를 엽니다.
2. 사용자 지정 규칙을 선택합니다. **내보내기**를 클릭합니다. 그러면 메모장 창이 열립니다. PS1 확장명으로 hello 임시 파일을 저장 합니다. 이렇게하면 PowerShell 스크립트가 됩니다. 서버를 준비 하는 hello PS1 파일 toohello를 복사 합니다.  
   ![동기화 규칙 내보내기](./media/active-directory-aadconnect-upgrade-previous-version/exportrule.png)
3. 서버를 준비 하는 hello 달라 지는 hello 커넥터 GUID 및 변경 해야 합니다. tooget hello GUID, 시작 **동기화 규칙 편집기**, 동일 시스템을 연결 하 고 클릭 하 여 해당 나타내는 hello hello 기본적으로 규칙 중 하나를 선택 **내보내기**합니다. 서버를 준비 하는 hello에서 GUID hello로 hello PS1 파일의 GUID를 대체 합니다.
4. PowerShell 프롬프트에서 hello PS1 파일을 실행 합니다. 서버를 준비 하는 hello에 hello 사용자 지정 동기화 규칙을 만듭니다.
5. 모든 사용자 지정 규칙에 대해 이 단계를 반복합니다.

## <a name="how-toodefer-full-synchronization-after-upgrade"></a>Toodefer는 업그레이드 후 동기화를 완전 하는 방법
현재 위치 업그레이드 하는 동안 있을 수 있습니다 특정 동기화 (전체 가져오기 단계와 완전히 동기화 단계 포함) 활동 toobe 실행 해야 하는 변경 내용이 도입 되었습니다. 커넥터 스키마 변경 해야 하는 예를 들어 **전체 가져오기** 단계 및 기본 제공 동기화 규칙 변경 필요 **전체 동기화** 단계 toobe 영향 받는 커넥터를 실행 합니다. 업그레이드 중 Azure AD Connect는 필요한 동기화 작업을 확인하고 *재정의*로 기록합니다. 다음 동기화 주기 hello, hello 동기화 스케줄러 이러한 재정의를 선택 하 고 실행 합니다. 재정의는 성공적으로 실행된 후 제거됩니다.

여기서 하지 않으려면 이러한 재정의 tootake 현재 위치 업그레이드 직후 경우가 있습니다. 예를 들어 다양 한 동기화 된 개체가 있고 원하는 이러한 동기화 단계 toooccur 업무 시간 이후입니다. 이러한 재정의 tooremove:

1. 업그레이드 하는 동안 **의 선택을 취소** 옵션 hello **구성이 완료 되 면 hello 동기화 프로세스를 시작**합니다. 이 hello 동기화 스케줄러를 사용 하지 않도록 설정 되며 못하도록 동기화 주기 수행 하 고 자동으로 hello 재정의가 제거 되기 전에 합니다.

   ![DisableFullSyncAfterUpgrade](./media/active-directory-aadconnect-upgrade-previous-version/disablefullsync01.png)

2. 업그레이드가 완료 된 후 어떤 재정의 추가 된 out cmdlet toofind 다음 hello를 실행 합니다.`Get-ADSyncSchedulerConnectorOverride | fl`

   >[!NOTE]
   > hello 재정의 커넥터 마다 다릅니다. Hello 다음 예제에서는, 전체 가져오기 단계와 완전히 동기화 단계 추가 되었습니다 tooboth hello 온-프레미스 AD 커넥터 및 Azure AD 커넥터입니다.

   ![DisableFullSyncAfterUpgrade](./media/active-directory-aadconnect-upgrade-previous-version/disablefullsync02.png)

3. Hello 기존 다운 참고에 추가 된 재정의 합니다.
   
4. 전체 가져오기 및 hello 다음 cmdlet을 실행 하는 임의 커넥터에서 전체 동기화를 둘 다에 대해 재정의 tooremove hello:`Set-ADSyncSchedulerConnectorOverride -ConnectorIdentifier <Guid-of-ConnectorIdentifier> -FullImportRequired $false -FullSyncRequired $false`

   PowerShell 스크립트 뒤 hello를 실행 하는 모든 커넥터에 tooremove hello 재정의 합니다.

   ```
   foreach ($connectorOverride in Get-ADSyncSchedulerConnectorOverride)
   {
       Set-ADSyncSchedulerConnectorOverride -ConnectorIdentifier $connectorOverride.ConnectorIdentifier.Guid -FullSyncRequired $false -FullImportRequired $false
   }
   ```

5. tooresume hello 스케줄러를 hello 다음 cmdlet을 실행 합니다.`Set-ADSyncScheduler -SyncCycleEnabled $true`

   >[!IMPORTANT]
   > 가능한 빨리 tooexecute 필요한 hello 동기화 단계를 기억 합니다. 수동으로 hello 동기화 서비스 관리자를 사용 하 여 다음이 단계를 실행 하거나 hello 집합 ADSyncSchedulerConnectorOverride cmdlet를 사용 하 여 hello 재정의 추가 합니다.

전체 가져오기 및 hello 다음 cmdlet을 실행 하는 임의 커넥터에서 전체 동기화를 둘 다에 대해 재정의 tooadd hello:`Set-ADSyncSchedulerConnectorOverride -ConnectorIdentifier <Guid> -FullImportRequired $true -FullSyncRequired $true`

## <a name="next-steps"></a>다음 단계
[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.
