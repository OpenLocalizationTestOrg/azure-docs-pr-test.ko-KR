---
title: "aaaUpgrade 백업 자격 증명 모음 tooa 복구 서비스 자격 증명 모음 (미리 보기) | Microsoft Docs"
description: "지침 및 지원 정보 tooupgrade Azure 백업 tooa 복구 서비스 자격 증명 모음 자격 증명 모음입니다."
services: backup
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
ms.assetid: 228fef19-2f6b-4067-acc3-fb6e501afb88
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/03/2017
ms.author: sogup;markgal;arunak
ms.openlocfilehash: 49062ca4556a009c82f143bb3a60ec71748bed01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-backup-vault-tooa-recovery-services-vault"></a>백업 자격 증명 모음 tooa 복구 서비스 자격 증명 모음 업그레이드

이 문서 방법을 tooupgrade 백업 자격 증명 모음 tooa 복구 서비스 자격 증명 모음에 대해 설명 합니다. hello 업그레이드 프로세스는 실행 중인 백업 작업에 영향을 주지 하 고 백업 데이터가 손실 됩니다. hello 기본 복구 서비스 자격 증명 모음에 백업 자격 증명 모음 tooa tooupgrade 이유:
- Recovery Services 자격 증명 모음에 백업 자격 증명 모음의 기능이 모두 유지됩니다.
- Recovery Services 자격 증명 모음은 보안 향상, 모니터링 통합, 빠른 복원 및 항목 수준의 복원을 포함하여 백업 자격 증명 모음보다 더 많은 기능을 제공합니다.
- 향상되고 간소화된 포털에서 백업 항목을 관리합니다.
- 새로운 기능 tooRecovery 서비스 자격 증명 모음을만 적용 됩니다.

## <a name="impact-toooperations-during-upgrade"></a>업그레이드 하는 동안 toooperations 영향

백업 자격 증명 모음 tooa 복구 서비스 자격 증명 모음으로 업그레이드할 때 아무 영향도 끼치지 않습니다 tooyour 데이터 평면 작업 합니다. 모든 백업 작업이 정상적으로 계속되고 모든 활성 복원 작업도 중단없이 계속됩니다. Hello 업그레이드 하는 동안 짧은 가동 중지 시간이 발생 하는 관리 작업 및 새 항목을 보호 하거나 임시 백업 작업을 만들 수 없습니다. IaaS Vm에 대 한 복원 작업이 hello 업그레이드 하는 동안 실행 되지 않습니다. 시간 toocomplete 아래 hello 자격 증명 모음 업그레이드가 됩니다. 완료 되 면 복구 서비스 자격 증명 모음 hello 백업 자격 증명 모음을 대체 합니다.

## <a name="changes-tooyour-automation-and-tool-after-upgrading"></a>업그레이드 한 후 tooyour 자동화 및 도구 변경

Hello 자격 증명 모음 업그레이드를 위한 인프라를 준비 하는 동안 기존 자동화를 업데이트 해야 하거나 tooensure tooling 한다는 계속 toowork hello 업그레이드 후 합니다.
Hello에 대 한 hello PowerShell cmdlet 참조를 참조 하십시오. [Service Manager 배포 모델](backup-client-automation-classic.md) 및 hello [리소스 관리자 배포 모델](backup-client-automation.md)합니다.


## <a name="before-you-upgrade"></a>업그레이드하기 전에

Hello 다음과 같은 문제 업그레이드 하기 전에 사용자 백업 자격 증명 모음은 tooRecovery 서비스 자격 증명 모음을 확인 합니다.

- **최소 에이전트 버전이**: tooupgrade 자격 증명 모음을 확인 했는지 hello Microsoft Azure 복구 서비스 (MARS) 에이전트는 적어도 2.0.9070.0 버전입니다. Hello MARS 에이전트 2.0.9070.0 지난 경우 hello 업그레이드 프로세스를 시작 하기 전에 hello 에이전트를 업데이트 합니다.
- **인스턴스 기반 청구 모델**: 복구 서비스 자격 증명 모음만 hello 인스턴스 기반 청구 모델을 지원 합니다. Hello 이전 저장소 기반 청구 모델을 사용 하는 백업 자격 증명 모음을 사용 하는 경우 업그레이드 하는 동안 hello 청구 모델을 변환 합니다.
- **진행 중인 백업 구성 작업이**: 액세스 toohello 관리 평면 업그레이드 하는 동안 제한 됩니다. 모든 관리 평면 동작을 완료 하 고 hello 업그레이드를 시작 합니다.

## <a name="using-powershell-scripts-tooupgrade-your-vaults"></a>PowerShell 스크립트 tooupgrade 사용자 자격 증명 모음 사용

PowerShell 스크립트 tooupgrade에서는 백업 tooRecovery 서비스 자격 증명 모음 자격 증명 모음입니다. Hello 있어야 하는 확인에는 PowerShell 구성 요소 tootrigger hello 자격 증명 모음 업그레이드가 필요 합니다. 백업 자격 증명 모음에 대한 PowerShell 스크립트는 Recovery Services 자격 증명 모음에서 작동하지 않습니다. 사용자 환경 tooupgrade hello 자격 증명 모음을 준비 합니다.

1. 설치 또는 업그레이드 [WMF Windows Management Framework () tooversion 5](https://www.microsoft.com/download/details.aspx?id=50395) 이상.
2. [Azure PowerShell MSI 설치](https://github.com/Azure/azure-powershell/releases/download/v3.8.0-April2017/azure-powershell.3.8.0.msi)
3. Hello 다운로드 [PowerShell 스크립트](https://aka.ms/vaultupgradescript2) tooupgrade 사용자 자격 증명 모음입니다.

### <a name="run-hello-powershell-script"></a>Hello PowerShell 스크립트 실행

다음 스크립트 tooupgrade hello 사용자 자격 증명 모음을 사용 합니다. 다음 샘플 스크립트는 hello hello 매개 변수에 대 한 정보에 있습니다.

RecoveryServicesVaultUpgrade-1.0.2.ps1 **-SubscriptionID** `<subscriptionID>` **-VaultName** `<vaultname>` **-Location** `<location>` **-ResourceType** `BackupVault` **-TargetResourceGroupName** `<rgname>`

**SubscriptionID** -hello hello 자격 증명 모음의 업그레이드 중인 구독 ID 번호.<br/>
**VaultName** -hello 업그레이드 중인 hello 백업 자격 증명 모음 이름입니다.<br/>
**위치** -업그레이드 중인 hello 자격 증명 모음의 위치입니다.<br/>
**ResourceType** - BackupVault를 사용합니다.<br/>
**TargetResourceGroupName** -이후 배포 업그레이드 하는 hello 자격 증명 모음 tooa 리소스 관리자 기반, 리소스 그룹을 지정 합니다. 기존 리소스 그룹을 사용하거나 새 이름을 제공하여 새 리소스 그룹을 만들 수 있습니다. 리소스 그룹의 hello 이름을 잘못 된 경우에 새 리소스 그룹을 만들 수 있습니다. 리소스 그룹에 대해 자세히 toolearn이 내용을 읽고 [리소스 그룹에 대 한 개요](../azure-resource-manager/resource-group-overview.md#resource-groups)합니다.

>[!NOTE]
> 리소스 그룹 이름에는 제약이 있습니다. 있는지 toofollow hello 지침; 수 따라서 실패 toodo 자격 증명 모음 업그레이드 toofail을 발생할 수 있습니다.
>
>

hello 다음 코드 조각은 예의 PowerShell 명령 어떤 같아야 합니다.

```
RecoveryServicesVaultUpgrade.ps1 -SubscriptionID 53a3c692-5283-4f0a-baf6-49412f5ebefe -VaultName "TestVault" -Location "Australia East" -ResourceType BackupVault -TargetResourceGroupName "ContosoRG"
```

매개 변수 없이 hello 스크립트를 실행할 수도 있습니다 및 모든 필수 매개 변수에 대해 tooprovide 입력을 요청 합니다.

PowerShell 스크립트 hello 메시지 있습니다 tooenter 자격 증명을 표시합니다. 자격 증명을 두 번 입력: hello Service Manager 계정 및 리소스 관리자 계정 hello에 대 한 두 번째 시간에 대해 한 번씩입니다.

### <a name="pre-requisites-checking"></a>필수 구성 요소 확인
Azure 자격 증명을 입력 하 고 나면 Azure는 환경이 hello 다음 필수 구성 요소를 충족 하는지 확인 합니다.

- **최소 에이전트 버전이** -업그레이드 백업 자격 증명 모음 tooRecovery 서비스 자격 증명 모음을 사용 하려면 hello MARS 에이전트 toobe 적어도 2.0.9070 버전입니다. 있는 경우 항목 에이전트 2.0.9070 보다 이전 tooa 백업 자격 증명 모음에 등록, hello 필수 구성 요소 검사에 실패 합니다. Hello 필수 구성 요소 확인이 실패 하면 hello 에이전트를 업데이트 하 고 tooupgrade hello 자격 증명 모음을 다시 시도 하십시오. Hello에서 hello 에이전트의 최신 버전을 다운로드할 수 있습니다 [http://download.microsoft.com/download/F/4/B/F4B06356-150F-4DB0-8AD8-95B4DB4BBF7C/MARSAgentInstaller.exe](http://download.microsoft.com/download/F/4/B/F4B06356-150F-4DB0-8AD8-95B4DB4BBF7C/MARSAgentInstaller.exe)합니다.
- **진행 중인 구성 작업이**: toobe 업그레이드 또는 항목 등록 백업 자격 증명 모음 설정에 대 한 작업 구성 하는 누군가가, 경우 hello 필수 구성 요소 검사에 실패 합니다. Hello 구성을 완료 하거나 hello 항목 등록을 완료 하 고 hello 자격 증명 모음에 대 한 업그레이드 프로세스를 시작 합니다.
- **저장소 기반 청구 모델**: 복구 서비스 자격 증명 모음 지원 hello 인스턴스 기반 청구 모델입니다. 사용 하 여 hello 저장소 기반 청구 모델, 입력 정보 요청된 tooupgrade는 백업 자격 증명 모음에 hello 자격 증명 모음 업그레이드를 실행 하는 경우 청구 모델 hello와 함께 자격 증명 모음입니다. 먼저, 청구 모델을 업데이트할 수는 그렇지 않은 경우 다음 hello 자격 증명 모음 업그레이드를 실행 합니다.
- Hello 복구 서비스 자격 증명 모음에 대 한 리소스 그룹을 식별 합니다. tootake 활용 hello 리소스 관리자 배포 기능, 리소스 그룹에 복구 서비스 자격 증명 모음을 설정 해야 합니다. 이름 및 hello에 대 한 업그레이드 프로세스를 제공 하는 리소스 그룹 toouse 알지 못하는 경우 hello 리소스 그룹을 만듭니다. hello 업그레이드 프로세스는 또한 hello 자격 증명 모음을 연결 된 hello 새 리소스 그룹입니다.

Hello 필수 조건 검사를 완료 하는 hello 업그레이드 프로세스, 나면 hello 프로세스 있습니다 toostart hello 자격 증명 모음 업그레이드 라는 메시지를 표시 합니다. 를 확인 한 후 hello 업그레이드 프로세스는 일반적으로 자격 증명 모음의 hello 크기에 따라 15 20 분 toocomplete 주위 걸립니다. 큰 자격 증명 모음이 업그레이드 too90 분 모두 사용할 수 있습니다.

## <a name="managing-your-recovery-services-vaults"></a>Recovery Services 자격 증명 모음 관리

hello 화면에 따라 새 복구 서비스 자격 증명 모음을 hello Azure 포털에서에서 백업 자격 증명 모음에서 업그레이드를 표시 합니다. 첫 번째 화면 hello hello 자격 증명 모음에 대 한 주요 엔터티를 표시 하는 hello 자격 증명 모음 대시보드를 보여 줍니다.

![백업 자격 증명 모음에서 업그레이드된 Recovery Services 자격 증명 모음의 예](./media/backup-azure-upgrade-backup-to-recovery-services/upgraded-rs-vault-in-dashboard.png)

hello 두 번째 화면 hello 도움말 링크를 사용할 수 있는 toohelp hello 복구 서비스를 사용 하 여 시작 하려면 자격 증명 모음에 표시 됩니다.

![도움말 hello 빠른 시작 블레이드 링크](./media/backup-azure-upgrade-backup-to-recovery-services/quick-start-w-help-links.png)

## <a name="post-upgrade-steps"></a>업그레이드 후 단계
Recovery Services 자격 증명 모음은 백업 정책에서 표준 시간대 정보를 지정하도록 지원합니다. 자격 증명 모음 성공적으로 업그레이드 되 면 자격 증명 모음 설정 메뉴에서 tooBackup 정책을 이동한 각 hello 자격 증명 모음에 구성 된 hello 정책에 대 한 hello 표준 시간대 정보를 업데이트 합니다. 이 여기서는 이미 지정 된 정책을 만든 경우 사용 되는 현지 표준 시간대 당 hello 백업 일정 시간을 표시 합니다. 

## <a name="enhanced-security"></a>향상된 보안

백업 자격 증명 모음 업그레이드 되 면 tooa 복구 서비스 자격 증명 모음, 해당 자격 증명 모음에 대 한 hello 보안 설정이 자동으로 켜져 있습니다. 암호를 변경 해야 하거나 때 hello 보안 설정은 백업을 삭제 하는 등 특정 작업에 대 한 [Azure Multi-factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) PIN입니다. Hello 강화 된 보안에 대 한 자세한 내용은 hello 문서 참조 [보안 기능이 tooprotect 하이브리드 백업을](backup-azure-security-feature.md)합니다. 

Hello 강화 된 보안 상태에서 데이터를 too14 일 hello 복구 지점 정보 hello 자격 증명 모음에서 삭제 한 후 유지 됩니다. 고객에게 이 보안 데이터의 저장에 대한 비용이 청구됩니다. 보안 데이터 보존 hello Azure 백업 에이전트, Azure 백업 서버 및 System Center Data Protection Manager에서 얻은 toorecovery 점수를 적용 합니다. 

## <a name="gather-data-on-your-vault"></a>자격 증명 모음에서 데이터 수집

Tooa 복구 서비스 자격 증명 모음을 업그레이드 하면 (IaaS Vm 및 Microsoft Azure 복구 서비스 MARS ())에 대 한 Azure 백업에 대 한 보고서를 구성 하 고 Power BI tooaccess hello 보고서를 사용 합니다. 데이터 수집에 대 한 자세한 내용은 hello 문서 참조 [Azure 백업 구성 보고](backup-azure-configure-reports.md)합니다.

## <a name="frequently-asked-questions"></a>질문과 대답

**업그레이드 계획 hello 진행 중인 동안 백업 영향은?**</br>
아니요. 진행 중인 백업은 업그레이드 전후에도 중단되지 않고 계속됩니다.

**곧 업그레이드 계획이 있나요, 어떻게 toomy 자격 증명 모음 됩니까?**</br>
새로운 기능을 모두 적용 tooRecovery 서비스 자격 증명 모음만, 있습니다 tooupgrade 사용자 자격 증명 모음 읽어보시기 합니다. Microsoft은 hello 클래식 포털 사용할 수 없게 결국 됩니다. 2017 년 9 월 1부터 Microsoft 자동 업그레이드 시작 됩니다 백업 tooRecovery 서비스 자격 증명 모음 자격 증명 모음입니다. 2017 년 11 월 1에서 Microsoft hello 업그레이드 프로세스를 완료 합니다. 자격 증명 모음은 9월 또는 10월 중에 언제든지 자동으로 업그레이드할 수 있습니다. 자격 증명 모음을 가능한 한 빨리 업그레이드하는 것이 좋습니다.

**이 업그레이드로 기존 도구는 어떻게 되나요?**</br>
도구 toohello 리소스 관리자 배포 모델을 업데이트 합니다. 복구 서비스 자격 증명 모음에 대해 생성 된 hello 리소스 관리자 배포 모델에서 사용 합니다. Hello 리소스 관리자 배포 모델에 대 한 계획 및 사용자 자격 증명 모음에 hello 차이 가정 하에 중요 합니다. 

**Hello 업그레이드 하는 동안는 작동 중단 시간 무엇입니까?**</br>
업그레이드 하는 리소스의 hello 수에 따라 다릅니다. 소규모 배포 (수십 보호 된 인스턴스)에 대 한 전체 업그레이드 hello 20 분 미만 취해야 합니다. 대규모 배포의 경우에 최대 1시간이 걸립니다.

**업그레이드한 후에 롤백할 수 있나요?**</br>
아니요. Hello 리소스 성공적으로 업그레이드 된 후에 롤백이 지원 되지 않습니다.

**있습니까 유효성을 검사할 수 내 구독 또는 리소스 toosee 업그레이드 수 있는 경우?**</br>
예. 업그레이드 중에 첫 번째 단계 hello hello 리소스 업그레이드 지원할 수 있는지 확인 합니다. 필수 hello 유효성 검사 실패 하는 경우 메시지가 모든 hello 이유로 hello 업그레이드를 완료할 수 없습니다.

**사용 권한은 해야 있습니까 tootrigger 자격 증명 모음 업그레이드?**</br>
tooperform hello 자격 증명 모음에 업그레이드 hello Azure 클래식 포털에서에서 구독 hello에 대 한 공동 관리자로 추가 해야 합니다. 사용자는 이미 hello Azure 포털에에서 소유자로 나열 되어 있는 경우에 이것이 필요 합니다. Hello 구독에 대 한 공동 관리자는 tooadd 아웃 Azure 클래식 포털 toofind에서 hello 구독에 대 한 공동 관리자를 시도 합니다. 공동 관리자 수 tooadd 없는 경우 공동 관리자로 추가할 수 있는 hello 구독에 대 한 서비스 관리자 또는 공동 관리자에 문의 합니다.

**CSP 기반 백업 자격 증명 모음을 업그레이드할 수 있나요?**</br>
번호 CSP 기반 백업 자격 증명 모음을 현재 업그레이드할 수 없습니다. 업그레이드 하는 hello 다음 릴리스에서 CSP 기반 백업 자격 증명 모음에 대 한 지원을 추가 합니다.

**클래식 자격 증명 모음을 업그레이드한 이후를 볼 수 있나요?**</br>
아니요. 클래식 자격 증명을 업그레이드한 이후를 보거나 관리할 수 없습니다. 수 toouse hello 새 Azure 포털 hello 자격 증명 모음에 있는 모든 관리 작업을 위해 수만 있습니다.

**내 업그레이드 실패 했지만 hello 에이전트 요구를 보유 하는 hello 컴퓨터를 더 이상 존재 하지를 업데이트 합니다. 이러한 경우 어떻게 해야 하나요?**</br>
Toouse hello 저장소 해야 할 경우 장기 보존을 위해이 컴퓨터의 백업을 hello 수 tooupgrade hello 자격 증명 모음 됩니다. 이후 릴리스에서 이러한 자격 증명 모음을 업그레이드하는 지원을 추가할 예정입니다.
이 컴퓨터의 toostore hello 백업이 필요 하지 않은 경우에 더 이상 다음 하십시오 hello 자격 증명 모음에서이 컴퓨터를 등록 취소 하 고 hello 업그레이드 다시 시도 합니다.

**표시 되지 않는 이유 hello 작업 정보 내 온-프레미스 리소스에 대 한 업그레이드 후**</br>
에 대 한 모니터링 온-프레미스 백업 (MARS 에이전트, DPM 및 Azure 백업 서버) 자격 증명 백업 자격 증명 모음 tooRecovery 서비스 모음을 업그레이드 하는 경우 얻을 수 있는 새로운 기능입니다. 정보를 모니터링 하는 hello hello 서비스와 too12 시간 toosync를 차지 합니다.

**문제를 보고하려면 어떻게 해야 하나요?**</br>
실패 hello 자격 증명 모음의 일부 업그레이드 참고 hello OperationId hello 오류에 나열 됩니다. Microsoft 기술 지원 서비스는 tooresolve hello 문제를 적극적으로 작동 합니다. TooSupport 연락 하거나 전자 메일을 보내 수 rsvaultupgrade@service.microsoft.com 는 구독 ID로, 자격 증명 모음 이름, OperationId 합니다. 최대한 빨리 tooresolve hello 문제를 시도할 예정입니다. Toodo 명시적으로 지시 하지 않으면 hello 작업을 다시 시도 하지 마세요 Microsoft에서 등입니다.


## <a name="next-steps"></a>다음 단계
다음 문서를 사용 하 여 hello:</br>
[IaaS VM 백업](backup-azure-arm-vms-prepare.md)</br>
[Azure Backup Server 백업](backup-azure-microsoft-azure-backup.md)</br>
[Windows Server 백업](backup-configure-vault.md)
