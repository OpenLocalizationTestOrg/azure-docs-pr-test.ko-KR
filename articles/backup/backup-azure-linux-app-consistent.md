---
title: "Azure Backup: Linux VM의 응용 프로그램 일치 백업 | Microsoft Docs"
description: "Linux 가상 컴퓨터에 대 한 스크립트 tooguarantee 응용 프로그램에 일관 된 백업을 tooAzure를 사용 합니다. hello 스크립트 리소스 관리자 배포; tooLinux Vm에만 적용 hello 스크립트 tooWindows Vm 또는 서비스 관리자 배포 적용 되지 않습니다. 이 문서에서는 hello hello 스크립트, 문제 해결을 포함 하 여를 구성 하는 단계를 안내 합니다."
services: backup
documentationcenter: dev-center-name
author: anuragmehrotra
manager: shivamg
keywords: "앱 일치 백업, 응용 프로그램 일치 Azure VM 백업, Linux VM 백업, Azure Backup"
ms.assetid: bbb99cf2-d8c7-4b3d-8b29-eadc0fed3bef
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 4/12/2017
ms.author: anuragm;markgal
ms.openlocfilehash: d557dd973364d79bb4d8ce954f648de835dd345f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-consistent-backup-of-azure-linux-vms-preview"></a>Azure Linux VM의 응용 프로그램 일치 백업(미리 보기)

이 문서 hello Linux 전 스크립트와 사후 스크립트 프레임 워크 및 Azure Linux Vm의 응용 프로그램에 일관 된 백업을 사용 하는 tootake 수 있는 방법에 대해 소개 합니다.

> [!Note]
> hello 전 스크립트와 사후 스크립트 framework Azure 리소스 관리자를 통해 배포 된 Linux 가상 컴퓨터에 대해서만 지원 됩니다. Service Manager 배포 가상 컴퓨터 또는 Windows 가상 컴퓨터에는 응용 프로그램 일관성 스크립트가 지원되지 않습니다.
>

## <a name="how-hello-framework-works"></a>Hello 프레임 워크의 작동 원리

hello 프레임 워크에는 후 VM의 스냅숏을 수행 하는 동안 스크립트 및 사용자 지정 사전 스크립트 옵션 toorun를 제공 합니다. 바로 전에 hello VM 스냅샷 걸리고 hello VM 스냅샷을 수행한 후에 즉시 후 스크립트가 실행 전 스크립트 실행 됩니다. 이렇게 하면 있습니다 hello 유연성 toocontrol 응용 프로그램 및 환경 VM의 스냅숏을 수행 하는 동안 됩니다.

이 시나리오에서는 것은 중요 한 tooensure 응용 프로그램에 일관 된 VM 백업입니다. hello 전 스크립트는 응용 프로그램-네이티브 Api tooquiesce hello IOs를 호출 하 고 메모리 콘텐츠 toohello 디스크 플러시 수입니다. 이렇게 하면 해당 hello 스냅숏을 응용 프로그램에 일관 된 (면 hello 응용 프로그램을 제공 하는, 즉 부팅 되는 VM hello 복원 후). 이후 스크립트에 사용 되는 toothaw hello IOs 될 수 있습니다. 정상 작업 게시물 VM 스냅샷 hello 응용 프로그램을 다시 시작할 수 있도록 응용 프로그램-네이티브 Api를 사용 하 여 수행 합니다.

## <a name="steps-tooconfigure-pre-script-and-post-script"></a>이전 스크립트와 사후 단계 tooconfigure

1. Hello 루트 사용자 toohello tooback를 원하는 Linux VM에 로그인 합니다.

2. 다운로드 **VMSnapshotScriptPluginConfig.json** 에서 [GitHub](https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig), toohello 복사 **/등/azure** 를 tooback 거 인 모든 hello Vm에서 폴더입니다. Hello 만들기 **/등/azure** 이미 존재 하지 않는 경우 디렉터리입니다.

3. Hello 전 스크립트와 tooback를 계획 하는 모든 hello Vm에서 응용 프로그램에 대 한 후 스크립트를 복사 합니다. Hello 스크립트 tooany 위치 hello VM에 복사할 수 있습니다. Hello에서 스크립트 파일의 hello 있는지 tooupdate hello 전체 경로 수 **VMSnapshotScriptPluginConfig.json** 파일입니다.

4. Hello 다음 이러한 파일에 대 한 권한을 확인 합니다.

   - **VMSnapshotScriptPluginConfig.json**: 권한 "600" 예를 들어 "root" 사용자만 "읽기" 및 "쓰기" 사용 권한 toothis 파일이 있어야 합니다. 및 사용자를 "실행" 권한이 있어야 합니다.

   - **사전 스크립트 파일**: 권한 “700”  "Root" 사용자만 있어야 예를 들어 "읽기", "쓰기" 및 "실행" 권한 toothis 파일입니다.
  
   - **사후 스크립트**: 권한 “700” "Root" 사용자만 있어야 예를 들어 "읽기", "쓰기" 및 "실행" 권한 toothis 파일입니다.

   > [!Important]
   > hello 프레임 워크는 사용자에 게 강력한 기능을 제공 합니다. 안전 하 고 "root" 사용자의 액세스 toocritical JSON와 스크립트 파일이 유용 합니다.
   > Hello 이전 요구 사항이 충족 되지 않으면 hello 스크립트가 실행 되지 않습니다. 이로 인해 파일 시스템/충돌 일치 백업이 생성됩니다.
   >

5. 다음에 설명된 대로 **VMSnapshotScriptPluginConfig.json**을 구성합니다.
    - **pluginName**: 이 필드를 있는 그대로 둡니다. 그렇지 않으면 스크립트가 예상대로 작동하지 않을 수 있습니다.

    - **preScriptLocation**: hello는 진행 중인 toobe 백업 하는 VM에 hello hello 전 스크립트의 전체 경로 제공 합니다.

    - **postScriptLocation**: hello는 진행 중인 toobe 백업 하는 VM에 hello hello 후 스크립트의 전체 경로 제공 합니다.

    - **preScriptParams**: toobe toohello 전 스크립트를 전달 해야 하는 hello 선택적 매개 변수를 제공 합니다. 모든 매개 변수는 큰따옴표로 묶어야 하며 여러 개의 매개 변수는 쉼표로 구분해야 합니다.

    - **postScriptParams**: toobe toohello 후 스크립트를 전달 해야 하는 hello 선택적 매개 변수를 제공 합니다. 모든 매개 변수는 큰따옴표로 묶어야 하며 여러 개의 매개 변수는 쉼표로 구분해야 합니다.

    - **preScriptNoOfRetries**: hello 횟수 설정 hello 사전 스크립트 종료 하기 전에 오류가 발견 되는 경우 다시 시도 하십시오. 0은 한 번의 시도를 의미하고 실패의 경우 시도 없음을 의미합니다.

    - **postScriptNoOfRetries**: hello 횟수 설정 종료 하기 전에 오류가 발견 되 면 hello 후 스크립트 다시 시도해 야 합니다. 0은 한 번의 시도를 의미하고 실패의 경우 시도 없음을 의미합니다.
    
    - **timeoutInSeconds**: hello 전 스크립트와 사후 스크립트 hello에 대 한 개별 시간 제한을 지정 합니다.

    - **continueBackupOnFailure**:이 값을 너무 설정**true** 사전 스크립트 하는 경우 Azure 백업 toofall 백 tooa 파일 시스템 일관성/크래시 일관성 백업을 원하는 경우 또는 실패 후 스크립팅 합니다. 이 너무 설정**false** 실패 hello (있는 경우 단일 디스크 VM이이 설정에 관계 없이 해당 위치 합니다. 다시 일관 된 toocrash 백업) 제외 스크립트 오류가 발생 한 경우 백업 합니다.

    - **fsFreezeEnabled**: hello VM 스냅샷 tooensure 파일 시스템 일관성을 수행 하는 동안 Linux fsfreeze 호출할 수 있는지 여부를 지정 합니다. 도이 설정을 유지 하는 것이 좋습니다**true** 응용 프로그램에 fsfreeze 비활성화에 대 한 종속성입니다.

6. 이제 hello 스크립트 프레임 워크 구성 됩니다. Hello VM 백업이 이미 구성 되어 있으면 다음 백업 hello hello 스크립트를 호출 하 고 응용 프로그램 일치 백업을 트리거합니다. Hello VM 백업이 구성 되지 않은 경우 사용 하 여 구성 [tooRecovery 서비스 자격 증명 모음 Azure 가상 컴퓨터를 백업 합니다.](https://docs.microsoft.com/azure/backup/backup-azure-vms-first-look-arm)

## <a name="troubleshooting"></a>문제 해결

이전 스크립트와 사후 스크립트를 작성 하는 동안 적절 한 로깅 추가 하 고 스크립트 로그 toofix 스크립트 문제를 검토 해야 합니다. 여전히 스크립트를 실행 하는 문제가 있으면 toohello 테이블에 대 한 자세한 내용은 다음을 참조 하십시오.

| 오류 | 오류 메시지 | 권장 작업 |
| ------------------------ | -------------- | ------------------ |
| Pre-ScriptExecutionFailed |hello 사전 스크립트 백업 응용 프로그램 일치 되지에서 오류를 반환 합니다. | 스크립트 toofix hello 문제에 대 한 hello 오류 로그를 검토 합니다.|  
|   Post-ScriptExecutionFailed |    hello 사후 스크립트 응용 프로그램 상태에 영향을 줄 수 있는 오류를 반환 합니다. |  스크립트 toofix hello 문제에 대 한 hello 오류 로그와 hello 응용 프로그램 상태를 확인 하십시오. |
| Pre-ScriptNotFound |  hello 사전 스크립트 찾을 수 없습니다 hello에 지정 된 hello 위치의 **VMSnapshotScriptPluginConfig.json** 구성 파일입니다. | 확인 있는지를 사전 스크립트가 hello tooensure 응용 프로그램 일치 백업 구성 파일에에서 지정 된 hello 경로 앞에 있어야 합니다.|
| Post-ScriptNotFound | hello 사후 스크립트 되지 않은 위치에서 찾을 hello hello에 지정 된 **VMSnapshotScriptPluginConfig.json** 구성 파일입니다. | 확인 되었는지는 이후 스크립트가 hello tooensure 응용 프로그램 일치 백업 구성 파일에에서 지정 된 hello 경로 앞에 있어야 합니다.|
| IncorrectPluginhostFile | hello **Pluginhost** hello VmSnapshotLinux 확장에 오는 파일 손상 하므로 이전 스크립트와 이후 스크립트를 실행할 수 없습니다 하 고 hello 백업 응용 프로그램 일치 되지 않습니다.   | Hello 제거 **VmSnapshotLinux** , 확장명을 사용 하며 자동으로 다시 설치 됩니다 hello 다음 백업 toofix hello 문제입니다. |
| IncorrectJSONConfigFile | hello **VMSnapshotScriptPluginConfig.json** 파일은 잘못 되었거나, 하므로 이전 스크립트와 사후 스크립트를 실행할 수 없습니다 및 hello 백업 응용 프로그램 일치 되지 않습니다. | hello 복사본 다운로드 [GitHub](https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig) 다시 구성 합니다. |
| InsufficientPermissionforPre-Script | Hello 파일 "700" 권한이 있어야 및 스크립트를 실행 하는 것에 대 한 "root" 사용자 hello 파일의 hello 소유자 여야 합니다 (즉, "소유자"만 가져야 합니다 "읽기", "쓰기" 및 "실행" 권한). | "Root" 사용자는 hello 스크립트 파일의 "소유자" hello 있고 "소유자"만 "읽기", "쓰기" 및 "실행" 권한이 있는지 확인 합니다. |
| InsufficientPermissionforPost-Script | Hello 파일 "700" 권한이 있어야 하 고 스크립트를 실행 하는 것에 대 한 루트 사용자 hello 파일의 hello 소유자 여야 합니다 (즉, "소유자"만 가져야 합니다 "읽기", "쓰기" 및 "실행" 권한). | "Root" 사용자는 hello 스크립트 파일의 "소유자" hello 있고 "소유자"만 "읽기", "쓰기" 및 "실행" 권한이 있는지 확인 합니다. |
| Pre-ScriptTimeout | hello hello 응용 프로그램 일치 백업 전 스크립트 실행 시간 초과 합니다. | Hello 스크립트를 확인 하 고 hello에 hello 시간 제한을 늘릴 **VMSnapshotScriptPluginConfig.json** 에 있는 파일을 **/등/azure**합니다. |
| Post-ScriptTimeout | hello hello 응용 프로그램 일치 백업 후 스크립트 실행 제한 시간이 초과 되었습니다. | Hello 스크립트를 확인 하 고 hello에 hello 시간 제한을 늘릴 **VMSnapshotScriptPluginConfig.json** 에 있는 파일을 **/등/azure**합니다. |

## <a name="next-steps"></a>다음 단계
[VM 백업 tooa 복구 서비스 자격 증명 모음 구성](https://docs.microsoft.com/azure/backup/backup-azure-arm-vms)
