---
title: "Azure AD Connect: 자동 업그레이드 | Microsoft Docs"
description: "이 항목에서는 hello 기본 제공 자동 업그레이드 기능에 Azure AD Connect 동기화에 설명 합니다."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b395e8f-fa3c-4e55-be54-392dd303c472
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 70d15eb3adf7758d8a43d278157daa504e059a98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-automatic-upgrade"></a>Azure AD Connect: 자동 업그레이드
이 기능은 빌드 1.1.105.0(2016년 2월에 발표됨)에서 도입되었습니다.

## <a name="overview"></a>개요
Azure AD Connect 설치 toodate를 항상는 쉬워졌습니다 hello로 **자동 업그레이드** 기능입니다. 이 기능은 Express 설치 및 DirSync 업그레이드에 대해 기본적으로 사용되도록 설정되어 있습니다. 새 버전이 출시되면 설치가 자동으로 업그레이드됩니다.

자동 업그레이드는 hello 다음에 대 한 기본적으로 사용 됩니다.

* Express 설정 설치 및 DirSync 업그레이드
* SQL Express LocalDB(Express 설정에서 항상 사용)를 사용하는 경우 SQL Express를 사용한 DirSync에도 LocalDB가 사용됩니다.
* hello AD 계정에는 기본 설정 및 DirSync에서 만든 하는 hello 기본 MSOL_ 계정입니다.
* Hello 메타 버스에서 100, 000 보다 작은 개체 있어야 합니다.

hello PowerShell cmdlet과 hello 자동 업그레이드의 현재 상태를 볼 수 있습니다 `Get-ADSyncAutoUpgrade`합니다. 여기에 hello 상태 뒤에 있습니다.

| 시스템 상태 | 주석 |
| --- | --- |
| 사용 |자동 업그레이드를 사용할 수 있습니다. |
| 일시 중단 |Hello 체제별 설정 합니다. hello 시스템은 더 이상 적합 tooreceive 자동 업그레이드 합니다. |
| 사용 안 함 |자동 업그레이드를 사용할 수 없습니다. |

`Set-ADSyncAutoUpgrade`(으)로 **사용**과 **사용 안 함** 사이를 전환할 수 있습니다. Hello 시스템 hello 상태를 설정 해야 하는 전용 **Suspended**합니다.

자동 업그레이드는 hello 업그레이드 인프라에 대 한 Azure AD Connect Health를 사용 합니다. 자동 업그레이드 toowork 해야 hello Url에 대 한 프록시 서버에서 연 **Azure AD Connect Health** 에 설명 된 대로 [Office 365 Url 및 IP 주소 범위](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)합니다.

경우 hello **동기화 서비스 관리자** hello 업그레이드 일시 중단 hello UI를 닫을 때까지 다음 UI hello 서버에서 실행 됩니다.

## <a name="troubleshooting"></a>문제 해결
연결 설치 업그레이드 되지 않습니다. 자체 예상 대로, 이러한 단계 toofind 잘못 일 아웃을 수행 합니다.

첫째, 예상할 수 없습니다 hello 시도 하는 자동 업그레이드 toobe hello 새 버전이 출시 되는 첫 번째 날입니다. 업그레이드를 시도하기 전에 의도적인 임의성이 있으므로 설치가 즉시 업그레이드되지 않더라도 경고가 표시되지 않습니다.

무언가 적절 하지 않은 경우 다음 먼저 실행 `Get-ADSyncAutoUpgrade` tooensure 자동 업그레이드가 설정 되어 있습니다.

그런 다음 필요한 hello Url 프록시 또는 방화벽에서 연 해야 합니다. 자동 업데이트는 hello에 설명 된 대로 Azure AD Connect Health를 사용 중인 [개요](#overview)합니다. 프록시를 사용 하는 경우 상태에는 구성 된 toouse 되어 있는지 확인 한 [프록시 서버](../connect-health/active-directory-aadconnect-health-agent-install.md#configure-azure-ad-connect-health-agents-to-use-http-proxy)합니다. 또한 hello 테스트 [상태 연결](../connect-health/active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service) tooAzure AD 합니다.

AD 확인 하는 hello 연결 tooAzure은 시간 toolook hello에 대 한 이벤트 로그에 있습니다. Hello 이벤트 뷰어를 시작 하 고 hello 찾는 위치 **응용 프로그램** eventlog 합니다. Hello 원본에 대 한 이벤트 로그 필터를 추가할 **Azure AD 업그레이드 연결** hello 이벤트 id 범위 및 **300 399**합니다.  
![자동 업그레이드에 대한 이벤트 로그 필터](./media/active-directory-aadconnect-feature-automatic-upgrade/eventlogfilter.png)  

이제 자동 업그레이드에 대 한 hello 상태와 관련 된 hello 대 한 이벤트 로그를 볼 수 있습니다.  
![자동 업그레이드에 대한 이벤트 로그 필터](./media/active-directory-aadconnect-feature-automatic-upgrade/eventlogresult.png)  

hello 결과 코드 hello 상태에 대 한 개요와 접두사를 있습니다.

| 결과 코드 접두사 | 설명 |
| --- | --- |
| 성공 |hello 설치를 업그레이드 했습니다. |
| UpgradeAborted |일시적인 현상일 hello 업그레이드를 중지 합니다. 다시 시도 하 고 나중에 성공 했는지 hello 예상 됩니다. |
| UpgradeNotSupported |hello 시스템에 자동으로 업그레이드 되지 않도록 hello 시스템을 차단 하는 구성이 있습니다. Hello 상태가 변경 되 하지만 hello expectation hello 시스템을 수동으로 업그레이드 해야 하는 경우 toosee 더 시도 됩니다. |

찾았으면 hello 가장 일반적인 메시지 목록은 다음과 같습니다. Hello 결과 메시지는 hello 문제 이용해 수 있지만 모든, 표시 되지 않습니다.

| 결과 메시지 | 설명 |
| --- | --- |
| **UpgradeAborted** | |
| UpgradeAbortedCouldNotSetUpgradeMarker |Toohello 레지스트리를 쓸 수 없습니다. |
| UpgradeAbortedInsufficientDatabasePermissions |hello 기본 제공 administrators 그룹에는 사용 권한을 toohello 데이터베이스 없습니다. Azure AD Connect tooaddress의 최신 버전 toohello이이 문제를 수동으로 업그레이드 합니다. |
| UpgradeAbortedInsufficientDiskSpace |업그레이드는 디스크 공간 toosupport 충분 하지 않습니다. |
| UpgradeAbortedSecurityGroupsNotPresent |찾기 및 hello 동기화 엔진에 의해 사용 되는 모든 보안 그룹을 확인 하지 수 없습니다. |
| UpgradeAbortedServiceCanNotBeStarted |NT 서비스 hello **Microsoft Azure AD Sync** toostart 실패 했습니다. |
| UpgradeAbortedServiceCanNotBeStopped |NT 서비스 hello **Microsoft Azure AD Sync** toostop 실패 했습니다. |
| UpgradeAbortedServiceIsNotRunning |NT 서비스 hello **Microsoft Azure AD Sync** 실행 중이 아닙니다. |
| UpgradeAbortedSyncCycleDisabled |hello에 SyncCycle 옵션 hello [스케줄러](active-directory-aadconnectsync-feature-scheduler.md) 비활성화 되었습니다. |
| UpgradeAbortedSyncExeInUse |hello [동기화 서비스 관리자 UI](active-directory-aadconnectsync-service-manager-ui.md) hello 서버에서 열려 있습니다. |
| UpgradeAbortedSyncOrConfigurationInProgress |hello 설치 마법사가 실행 중 또는 hello 스케줄러 외부 동기화를 예약 합니다. |
| **UpgradeNotSupported** | |
| UpgradeNotSupportedCustomizedSyncRules |사용자 고유의 사용자 지정 규칙 toohello 구성을 추가 했습니다. |
| UpgradeNotSupportedDeviceWritebackEnabled |Hello 사용 하도록 설정한 [장치 쓰기 저장](active-directory-aadconnect-feature-device-writeback.md) 기능입니다. |
| UpgradeNotSupportedGroupWritebackEnabled |Hello 사용 하도록 설정한 [그룹 쓰기 저장](active-directory-aadconnect-feature-preview.md#group-writeback) 기능입니다. |
| UpgradeNotSupportedInvalidPersistedState |hello 설치가 기본 설정을 또는 DirSync 업그레이드 되지 않습니다. |
| UpgradeNotSupportedMetaverseSizeExceeeded |Hello 메타 버스의 100, 000 개 이상의 개체를가지고 있습니다. |
| UpgradeNotSupportedMultiForestSetup |한 포리스트의 보다 toomore를 연결 됩니다. 빠른 설치만 tooone 포리스트를 연결 합니다. |
| UpgradeNotSupportedNonLocalDbInstall |SQL Server Express LocalDB 데이터베이스를 사용하고 있지 않습니다. |
| UpgradeNotSupportedNonMsolAccount |hello [AD 커넥터 계정](active-directory-aadconnect-accounts-permissions.md#active-directory-account) hello 기본 MSOL_ 계정이 더 이상 아닙니다. |
| UpgradeNotSupportedStagingModeEnabled |서버 hello에 toobe 설정 되어 [준비 모드](active-directory-aadconnectsync-operations.md#staging-mode)합니다. |
| UpgradeNotSupportedUserWritebackEnabled |Hello 사용 하도록 설정한 [사용자 쓰기 저장](active-directory-aadconnect-feature-preview.md#user-writeback) 기능입니다. |

## <a name="next-steps"></a>다음 단계
[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.
