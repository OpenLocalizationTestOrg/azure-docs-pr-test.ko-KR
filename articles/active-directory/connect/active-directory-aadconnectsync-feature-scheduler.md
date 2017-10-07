---
title: "Azure AD Connect 동기화: 스케줄러 | Microsoft Docs"
description: "이 항목에서는 Azure AD Connect 동기화의 기본 제공 스케줄러 기능을 hello 설명 합니다."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b1a598f-89c0-4244-9b20-f4aaad5233cf
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: c587039cc68d305862a07beff364894b6f74cd2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-scheduler"></a>Azure AD Connect 동기화: 스케줄러
이 항목에서는 Azure AD Connect 동기화의 기본 제공 스케줄러 hello (규칙 하위 설명 설명합니다.

이 기능은 빌드 1.1.105.0(2016년 2월에 발표됨)에서 도입되었습니다.

## <a name="overview"></a>개요
Azure AD Connect 동기화는 스케줄러를 사용하여 온-프레미스 디렉터리에서 발생하는 변경 내용을 동기화합니다. 두 개의 스케줄러 프로세스가 있으며, 하나는 암호 동기화용이고 다른 하나는 개체/특성 동기화 및 유지 관리 작업용입니다. 이 항목에서는 hello 후자를 다룹니다.

이전 릴리스에서 개체와 특성에 대 한 hello 스케줄러 외부 toohello 동기화 엔진이 했습니다. Windows 작업 스케줄러 또는 별도 Windows 서비스 tootrigger hello 동기화 프로세스를 사용. 1.1 릴리스에 기본 제공 toohello 동기화 엔진이 hello를 일부 사용자 지정을 허용지 않습니다 hello 스케줄러와는 합니다. hello 새 기본 동기화 빈도 30 분입니다.

hello 스케줄러는 두 가지 작업을 담당 합니다.

* **동기화 주기**. hello 프로세스 tooimport, 동기화 및 내보내기 변경.
* **유지 관리 작업**. 암호 재설정 및 DRS(장치 등록 서비스)에 대한 키와 인증서를 갱신합니다. Hello 작업 로그에서 이전 항목을 제거 합니다.

자체 hello 스케줄러가 실행 되 고 항상 이지만 하나 또는 이러한 작업을 실행 하는 구성 된 tooonly 수 있습니다. 예를 들어 사용자가 소유한 동기화 주기 프로세스 toohave 해야 할 경우 hello 스케줄러에서는이 작업이 있지만 여전히 실행된 hello 유지 관리 작업 비활성화할 수 있습니다.

## <a name="scheduler-configuration"></a>스케줄러 구성
toosee 현재 구성 설정, tooPowerShell 돌아가서 실행 `Get-ADSyncScheduler`합니다. 아래 그림과 같이 표시됩니다.

![GetSyncScheduler](./media/active-directory-aadconnectsync-feature-scheduler/getsynccyclesettings2016.png)

표시 되 면 **hello 동기화 명령 또는 cmdlet를 사용할 수 없습니다** 이 cmdlet을 실행 하면 다음 hello PowerShell 모듈이 로드 되지 않았습니다. 이 문제는 도메인 컨트롤러 또는 hello 기본 설정 보다 더 높은 PowerShell 제한 수준 사용 하 여 서버에서 Azure AD Connect를 실행 하는 경우에 발생할 수 있습니다. 이 오류를 표시 하는 경우 다음 실행 `Import-Module ADSync` toomake hello cmdlet 사용 가능 합니다.

* **AllowedSyncCycleInterval**. hello 가장 짧은 시간 간격 Azure AD에서 허용 하는 동기화 주기 사이입니다. 이 설정보다 더 자주 동기화할 수 없으며 계속 지원됩니다.
* **CurrentlyEffectiveSyncCycleInterval**. hello 일정 현재 적용에서 합니다. Hello CustomizedSyncInterval과 같은 값인 있기 (하는 경우 설정) AllowedSyncInterval 보다 더 잦은 빈도로 없는 경우. 1.1.281 이전 빌드를 사용하고 CustomizedSyncCycleInterval을 변경한 경우 이 변경 내용은 다음 동기화 주기 후에 적용됩니다. 1.1.281 빌드에서 hello 변경 즉시 적용이 됩니다.
* **CustomizedSyncCycleInterval**. 30 분 hello 기본값과 빈도로 hello 스케줄러 toorun 하려는 경우이 설정을 구성 합니다. 위의 hello 그림에서 hello 스케줄러 설정한 toorun 매시간 대신 합니다. 이 설정은 tooa 값을 설정 하면 AllowedSyncInterval 보다 낮은 경우 후자 hello 사용 됩니다.
* **NextSyncCyclePolicyType**. 델타 또는 초기입니다. 다음 실행 하는 hello 프로세스 델타 변경 내용만 해야 하거나 hello 다음 실행 작업을 수행 해야 전체 정의 가져오기 및 동기화 합니다. 후자의 hello 또한 새롭거나 변경 된 모든 규칙을 다시 처리 것입니다.
* **NextSyncCycleStartTimeInUTC**. 다음 번 hello 스케줄러 시작 hello 다음 동기화 주기 합니다.
* **PurgeRunHistoryInterval**. hello 시간 작업 로그를 유지 해야 합니다. 이러한 로그는 hello 동기화 서비스 관리자에서 검토할 수 있습니다. 기본 hello 7 일 동안 tookeep 이러한 로그 됩니다.
* **SyncCycleEnabled**. 경우 hello 스케줄러가 실행 되 고 hello 가져오기, 동기화 및 내보내기 프로세스는 작업의 일부로 나타냅니다.
* **MaintenanceEnabled**. Hello 유지 관리 프로세스를 사용 하는 경우를 보여 줍니다. Hello 인증서/키를 업데이트 하 고 제거 작업 로그 hello 키를 누릅니다.
* **StagingModeEnabled**. [스테이징 모드](active-directory-aadconnectsync-operations.md#staging-mode)를 사용할 수 있는지 표시합니다. 이 설정을 사용 하는 경우 다음 표시 되지 않도록 hello 내보내기 실행에서 되지만 여전히 가져오기 및 동기화를 실행 합니다.
* **SchedulerSuspended**. 실행에서 하는 동안 업그레이드 tootemporarily 블록 hello 스케줄러 연결 하 여 설정 합니다.

`Set-ADSyncScheduler`(으)로 이러한 모든 설정 중 일부를 변경할 수 있습니다. hello 매개 변수 뒤에 수정할 수 있습니다.

* CustomizedSyncCycleInterval
* NextSyncCyclePolicyType
* PurgeRunHistoryInterval
* SyncCycleEnabled
* MaintenanceEnabled

Azure AD Connect의 이전 빌드에서 **isStagingModeEnabled**는 Set-ADSyncScheduler에서 노출되었습니다. **지원 되지 않는** tooset이이 속성입니다. 속성을 hello **SchedulerSuspended** connect 수정 되어야 합니다. **지원 되지 않는** tooset 직접 powershell이 있습니다.

hello 스케줄러 구성은 Azure AD에 저장 됩니다. 준비 서버를 설정한 경우 hello 주 서버의 모든 변경 (제외 IsStagingModeEnabled) 서버를 준비 하는 hello도 적용 됩니다.

### <a name="customizedsynccycleinterval"></a>CustomizedSyncCycleInterval
구문: `Set-ADSyncScheduler -CustomizedSyncCycleInterval d.HH:mm:ss`  
d -일, HH - 시간, mm - 분, ss - 초

예: `Set-ADSyncScheduler -CustomizedSyncCycleInterval 03:00:00`  
스케줄러 toorun 3 시간 마다 hello 하는 변경 합니다.

예: `Set-ADSyncScheduler -CustomizedSyncCycleInterval 1.0:0:0`  
변경은 hello 스케줄러 toorun를 매일 변경 됩니다.

### <a name="disable-hello-scheduler"></a>Hello 스케줄러를 사용 하지 않도록 설정  
Toomake 구성을 변경 해야 할 경우 toodisable hello 스케줄러를 할 수 있습니다. 예를 들어 있습니다 [필터링을 구성](active-directory-aadconnectsync-configure-filtering.md) 또는 [변경할 toosynchronization 규칙](active-directory-aadconnectsync-change-the-configuration.md)합니다.

실행 되는 toodisable hello 스케줄러 `Set-ADSyncScheduler -SyncCycleEnabled $false`합니다.

![Hello 스케줄러를 사용 하지 않도록 설정](./media/active-directory-aadconnectsync-change-the-configuration/schedulerdisable.png)

변경 내용을 수행 했으면를 사용 하 여 다시 tooenable hello 스케줄러 잊지 마십시오 `Set-ADSyncScheduler -SyncCycleEnabled $true`합니다.

## <a name="start-hello-scheduler"></a>Hello 스케줄러를 시작 합니다.
hello 스케줄러는 기본적으로 30 분 마다 실행 합니다. 경우에 따라 동기화 주기 사이 hello toorun 주기를 예약 또는 toorun 다른 종류를 만들어야 할 수 있습니다.

**델타 동기화 주기**  
델타 동기화 주기 단계를 수행 하는 hello를 포함 되어 있습니다.

* 모든 커넥터에서 델타 가져오기
* 모든 커넥터에서 델타 동기화
* 모든 커넥터에서 내보내기

긴급 한 있다고 것 toomanually는 이유는 즉시 동기화 할 변경 주기를 실행 합니다. Toomanually 해야 할 경우 주기를 실행 하는 PowerShell에서 다음 실행 `Start-ADSyncSyncCycle -PolicyType Delta`합니다.

**전체 동기화 주기**  
Hello 구성 변경 내용이 다음 중 하나를 수행 해야 전체 동기화 주기 toorun (규칙 하위 합니다.

* 원본 디렉터리에서 가져온 더 많은 개체 또는 특성 toobe 추가
* 변경 toohello 동기화 규칙
* 다른 수의 개체가 포함되도록 [필터링](active-directory-aadconnectsync-configure-filtering.md) 변경

이러한 변경 중 하나를 수행 해야 toorun 전체 동기화 주기 hello 동기화 엔진이 hello 기회 tooreconsolidate hello 커넥터 공간을 가집니다. 전체 동기화 주기 단계를 수행 하는 hello를 포함 되어 있습니다.

* 모든 커넥터에서 전체 가져오기
* 모든 커넥터에서 전체 동기화
* 모든 커넥터에서 내보내기

전체 동기화 주기 tooinitiate 실행 `Start-ADSyncSyncCycle -PolicyType Initial` PowerShell 프롬프트에서 합니다. 이 명령은 전체 동기화 주기를 시작합니다.

## <a name="stop-hello-scheduler"></a>Hello 스케줄러를 중지 합니다.
Toostop hello 스케줄러 동기화 주기 현재 실행 중인 경우 필요할 것입니다. 예를 들어 hello 설치 마법사를 시작 하 고이 오류가 발생할 경우:

![SyncCycleRunningError](./media/active-directory-aadconnectsync-feature-scheduler/synccyclerunningerror.png)

동기화 주기를 실행 중일 때 구성을 변경할 수 없습니다. Hello 스케줄러 hello 프로세스 완료 되지만 변경 내용을 즉시 확인할 수 있도록 또한 중지할 수 있습니다 때까지 기다릴 수 있습니다. 현재 주기 hello 중지 유해한 아니며 보류 중인 변경 내용이 처리 된 다음 실행 합니다.

1. 현재 hello 스케줄러 toostop 알림으로써 시작 hello PowerShell cmdlet과 주기 `Stop-ADSyncSyncCycle`합니다.
2. 경우 1.1.281, 전에 빌드를 사용 하 고 hello 스케줄러를 중지 해도 hello 현재는 현재 작업에서 커넥터입니다. tooforce 커넥터 toostop hello, 수행할 작업을 수행 하는 hello: ![StopAConnector](./media/active-directory-aadconnectsync-feature-scheduler/stopaconnector.png)
   * 시작 **동기화 서비스** hello 시작 메뉴에서 합니다. 너무 이동**커넥터**, hello 커넥터 hello 상태로 강조 표시 **실행**를 선택 하 고 **중지** hello 동작에서에서 합니다.

hello 스케줄러 아직 활성 상태 이며 다음 기회에 다시 시작 합니다.

## <a name="custom-scheduler"></a>사용자 지정 스케줄러
hello이 섹션에 설명 된 cmdlet만에서 사용할 수 있는 빌드 [1.1.130.0](active-directory-aadconnect-version-history.md#111300) 이상.

기본 제공 스케줄러 hello 요구 사항을 충족 하지 않으면, PowerShell을 사용 하 여 hello 커넥터를 예약할 수 있습니다.

### <a name="invoke-adsyncrunprofile"></a>Invoke-ADSyncRunProfile
다음과 같이 커넥터에 대한 프로필을 시작할 수 있습니다.

```
Invoke-ADSyncRunProfile -ConnectorName "name of connector" -RunProfileName "name of profile"
```

에 대 한 hello 이름 toouse [커넥터 이름](active-directory-aadconnectsync-service-manager-ui-connectors.md) 및 [실행 프로필 이름은](active-directory-aadconnectsync-service-manager-ui-connectors.md#configure-run-profiles) hello에서 찾을 수 [동기화 서비스 관리자 UI](active-directory-aadconnectsync-service-manager-ui.md)합니다.

![실행 프로필 호출](./media/active-directory-aadconnectsync-feature-scheduler/invokerunprofile.png)  

hello `Invoke-ADSyncRunProfile` cmdlet은 동기, 즉, 돌아가지 않습니다 제어 성공적으로 또는 오류가 발생 하 여 hello 커넥터 hello 작업을 완료할 때까지 합니다.

커넥터를 예약할 때 hello 좋습니다 tooschedule 순서에 따라 hello에서 해당:

1. (전체/델타) Active Directory와 같은 온-프레미스 디렉터리에서 가져오기
2. (전체/델타) Azure AD에서 가져오기
3. (전체/델타) Active Directory와 같은 온-프레미스 디렉터리에서 동기화
4. (전체/델타) Azure AD에서 동기화
5. TooAzure AD 내보내기
6. 내보내기 tooon 온-프레미스 디렉터리를 Active Directory와 같은

이 순서는 기본 제공 스케줄러 hello hello 커넥터를 실행 하는 방법.

### <a name="get-adsyncconnectorrunstatus"></a>Get-ADSyncConnectorRunStatus
또한 사용 중인지 또는 유휴 상태 이면 hello 동기화 엔진 toosee를 모니터링할 수 있습니다. 이 cmdlet는 동기화 엔진 hello 유휴 상태이 고 커넥터를 실행 되지 않는 경우 빈 결과 반환 합니다. 커넥터를 실행 중인 경우 hello 커넥터의 hello 이름을 반환 합니다.

```
Get-ADSyncConnectorRunStatus
```

![커넥터 실행 상태](./media/active-directory-aadconnectsync-feature-scheduler/getconnectorrunstatus.png)  
위의 hello 그림에서 hello 첫 번째 줄은 hello 동기화 엔진은 유휴 상태에서입니다. hello hello Azure AD 커넥터를 실행 중인 경우에서 두 번째 줄.

## <a name="scheduler-and-installation-wizard"></a>스케줄러 및 설치 마법사
Hello 설치 마법사를 시작 하는 경우 hello 스케줄러 일시적으로 중단 됩니다. 이 동작은 간주 되므로 구성을 변경 하 고 hello 동기화 엔진을 실행 하는 경우에 이러한 설정을 적용할 수 없습니다. 이러한 이유로 두지 마십시오 hello 설치 마법사 열기 이후 모든 동기화 작업을 수행 하는 hello 동기화 엔진이 중지 합니다.

## <a name="next-steps"></a>다음 단계
Hello에 대 한 자세한 [Azure AD Connect 동기화](active-directory-aadconnectsync-whatis.md) 구성 합니다.

[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.
