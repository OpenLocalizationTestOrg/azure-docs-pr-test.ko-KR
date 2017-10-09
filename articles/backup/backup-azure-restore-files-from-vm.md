---
title: "Azure 백업: Azure VM 백업에서 파일 및 폴더 복구 | Microsoft Docs"
description: "Azure 가상 컴퓨터 복구 지점에서 파일 복구"
services: backup
documentationcenter: dev-center-name
author: pvrk
manager: shivamg
keywords: "항목 수준 복구, Azure 백업에서 파일 복구, Azure VM에서 파일 복원"
ms.assetid: f1c067a2-4826-4da4-b97a-c5fd6c189a77
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/20/2017
ms.author: pullabhk;markgal
ms.openlocfilehash: 1a62a0ed83d61272c032ac0377a54099ed118db4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="recover-files-from-azure-virtual-machine-backup"></a>Azure Virtual Machine 백업에서 파일 복구

Azure 백업 기능은 hello 기능 toorestore [Azure Vm 및 디스크](./backup-azure-arm-restore-vms.md) Azure VM 백업에서 합니다. 이제 이 문서에서는 Azure VM 백업에서 파일 및 폴더와 같은 항목을 어떻게 복구할 수 있는지 설명합니다.

> [!Note]
> 이 기능은 hello 리소스 관리자 모델 및 보호 된 tooa 복구 서비스 자격 증명 모음을 사용 하 여 배포 하는 Azure Vm에 사용할 수 있습니다.
> 암호화된 VM 백업으로부터 파일 복구는 지원되지 않습니다.
>

## <a name="mount-hello-volume-and-copy-files"></a>Hello 볼륨 및 복사 파일 탑재

1. Hello에 로그인 [Azure 포털](http://portal.Azure.com)합니다. Hello 관련 복구 서비스 자격 증명 모음 및 백업 hello 필요한 항목을 찾습니다.

2. Hello 백업 항목 블레이드에서 클릭 **파일 복구**

    ![Recovery Services 자격 증명 모음 백업 항목 열기](./media/backup-azure-restore-files-from-vm/open-vault-item.png)

    hello **파일 복구** 블레이드를 엽니다.

    ![파일 복구 블레이드](./media/backup-azure-restore-files-from-vm/file-recovery-blade.png)

3. Hello에서 **복구 지점을 선택** 원하는 hello 파일이 포함 된 select hello 복구 지점, 드롭 다운 메뉴. 기본적으로 이미 hello 최신 복구 지점을 선택 됩니다.

4. 클릭 **실행 파일을 다운로드** (용 Windows Azure VM의 경우) 또는 **스크립트 다운로드** (Azure Linux VM)에 대 한 toodownload hello 소프트웨어 hello 복구 지점에서 toocopy 파일을 사용 합니다.

  hello 실행/스크립팅 간의 연결을 만듭니다 hello 로컬 컴퓨터와 hello 지정 된 복구 지점입니다.

5. 암호 toorun hello 다운로드 한 스크립트/실행 파일이 필요합니다. 생성 된 hello 암호 옆에 있는 hello 복사 단추를 사용 하 여 hello 포털에서 hello 암호를 복사할 수 있습니다.

    ![생성된 암호](./media/backup-azure-restore-files-from-vm/generated-pswd.png)

6. Hello toorecover hello 파일을 컴퓨터에서 실행 hello 실행/스크립팅 합니다. 관리자 자격 증명으로 실행해야 합니다. 제한 된 액세스 된 컴퓨터에 hello 스크립트를 실행 하는 경우에 액세스할 수 있는지 확인:

    - download.microsoft.com
    - Azure VM 백업에 사용된 Azure 끝점
    - 아웃바운드 포트 3260

   Linux 용 hello 스크립트에 필요한 ' 오픈 iscsi' 및 'lshw' 구성 요소 tooconnect toohello 복구 지점입니다. 된 hello 컴퓨터 실행 되는 위치에 존재 하지 않는 경우 권한 tooinstall hello 관련 구성 요소를 요청 하 고 승인 시이 설치 합니다.
   
   메시지가 표시 되 면 hello 포털에서 복사 하는 hello 암호를 입력 합니다. Hello 유효한 암호를 입력 한 후 hello 스크립트 toohello 복구 지점을 연결 합니다.
      
    ![파일 복구 블레이드](./media/backup-azure-restore-files-from-vm/executable-output.png)
    
   
   Hello 백업 VM으로 동일한 (또는 호환) hello 운영 체제는 모든 컴퓨터에 hello 스크립트를 실행할 수 있습니다. Hello 참조 [호환 OS 테이블](backup-azure-restore-files-from-vm.md#compatible-os) 호환 되는 운영 체제에 대 한 합니다. 이면 hello 보호 Azure 가상 컴퓨터 사용 (Windows Azure Vm)에 대 한 Windows 저장소 공간 또는 LVM/RAID Arrays(for Linux VMs) 하면에서 hello 실행 파일/스크립트를 실행할 수 없습니다 hello 동일한 가상 컴퓨터. 대신, 호환되는 운영 체제로 다른 컴퓨터에서 실행합니다.

### <a name="compatible-os"></a>호환되는 OS

#### <a name="for-windows"></a>Windows의 경우

테이블 표시 hello 호환성 서버와 컴퓨터 운영 체제 간의 다음 번호입니다. 파일을 복구할 경우 호환되지 않는 운영 체제 간에는 파일을 복원할 수 없습니다.

|서버 OS | 호환되는 클라이언트 OS  |
| --------------- | ---- |
| Windows Server 2012 R2 | Windows 8.1 |
| Windows Server 2012    | Windows 8  |
| Windows Server 2008 R2 | 윈도우 7   |

#### <a name="for-linux"></a>Linux의 경우

Linux에서 hello 기본 요구 사항은 hello 파일 시스템을 지원 해야 하는 hello 스크립트가 실행 되는 hello 컴퓨터의 해당 hello 운영 체제의 hello hello에 있는 파일 백업 Linux VM입니다. 컴퓨터 toorun hello 스크립트를 선택 하는 동안 hello 테이블 아래에 설명 된 대로 hello 호환 되는 OS 및 hello 버전을에 있는지 확인 하십시오.

|Linux OS | 버전  |
| --------------- | ---- |
| Ubuntu | 12.04 이상 |
| CentOS | 6.5 이상  |
| RHEL | 6.7 이상 |
| Debian | 7 이상 |
| Oracle Linux | 6.4 이상 |

hello 스크립트도 필요 python 및 구성 요소 tooexecute를 이용한 적 하 고 toohello 복구 지점에 안전 하 게 연결 합니다.

|구성 요소 | 버전  |
| --------------- | ---- |
| bash | 4 이상 |
| python | 2.6.6 이상  |


### <a name="identifying-volumes"></a>볼륨 식별

#### <a name="for-windows"></a>Windows의 경우

Hello 사용 하 여 실행을 실행 하면 hello 운영 체제 hello 새 볼륨을 탑재 하 고 드라이브 문자를 할당 합니다. Windows 탐색기 또는 파일 탐색기 toobrowse 해당 드라이브를 사용할 수 있습니다. 그러나 hello toohello 볼륨에 할당 된 드라이브 문자 아닐 수도 있습니다 hello 동일한 문자 hello 원래 가상 컴퓨터 hello 볼륨 이름으로 유지 됩니다. 예를 들어 hello 볼륨 hello 원래 가상 컴퓨터에이 경우 "데이터 디스크 (e:\)", 볼륨으로 연결할 수 있습니다 "데이터 디스크 ('사용 가능한 드라이브 문자는 ':\) hello 로컬 컴퓨터에 있습니다. 파일/폴더를 찾을 때까지 hello 스크립트 출력에 언급 된 모든 볼륨을 찾아봅니다.  
       
   ![파일 복구 블레이드](./media/backup-azure-restore-files-from-vm/volumes-attached.png)
           
#### <a name="for-linux"></a>Linux의 경우

Linux에서 hello 복구 지점의 hello 볼륨에 탑재 된 toohello 폴더 hello 스크립트가 실행 되는. hello 연결 된 디스크, 볼륨 및 hello 해당 탑재 경로 적절 하 게 표시 됩니다. 이러한 탑재 경로 표시 toousers 루트 수준 액세스 됩니다. Hello 스크립트 출력에서 언급 한 hello 볼륨을 찾아봅니다.

  ![Linux 파일 복구 블레이드](./media/backup-azure-restore-files-from-vm/linux-mount-paths.png)
  

## <a name="closing-hello-connection"></a>Hello 연결을 닫는 중

Hello 파일을 확인 하 고 tooa 로컬 저장소 위치를 복사, 제거 또는 분리 hello 추가 드라이브. hello에 toounmount hello 드라이브 **파일 복구** 블레이드 hello Azure 포털에서에서 클릭 **디스크 분리**합니다.

![디스크 분리](./media/backup-azure-restore-files-from-vm/unmount-disks3.png)

Hello 디스크 탑재 되지 않은, 되 면 성공 했는지 알려주는 메시지가 나타납니다. Hello 디스크를 제거할 수 있도록 hello 연결 toorefresh 몇 분 정도 걸릴 수 있습니다.

Linux에서 끊어지면 hello 연결점 toohello 복구 후 hello OS 제거 되지 않습니다 탑재 경로 해당 하는 hello 자동으로. 이러한 메서드는 "분리" 볼륨으로 존재 하 고 때 하면 액세스/쓰기 hello 파일 오류를 throw 되지만 표시 됩니다. 수동으로 제거할 수도 있습니다. 모든 이전 복구 지점에서 기존 이러한 볼륨을 식별 하 고 승인 시 정리 하는 hello 스크립트를 실행 합니다.

## <a name="special-configurations"></a>특수 구성

### <a name="dynamic-disks"></a>동적 디스크

다음에서 hello 실행 스크립트를 실행할 수 없습니다 hello 백업 된 Azure VM에 볼륨이 여러 디스크 (스팬 및 스트라이프 볼륨) 및/또는 동적 디스크에 내결함성 (미러된 및 raid-5 볼륨) 볼륨에 걸쳐 있는 경우 동일한 VM hello 합니다. 대신, 호환 되는 운영 체제를 사용 하 여 다른 컴퓨터에서 hello 실행 스크립트를 실행 합니다.

### <a name="windows-storage-spaces"></a>Windows 저장소 공간

Windows 저장소 공간에 toovirtualize 저장소를 사용 하면 Windows 저장소에 기술입니다. Windows 저장소 공간 사용 업계 표준 디스크를 저장소 풀으로 그룹화 하 고 해당 저장소 풀의 사용 가능한 공간 hello에서에서 저장소 공간 이라는 가상 디스크를 만들 수 있습니다.

Hello 백업 된 Azure VM hello 실행 스크립트를 실행할 수 없습니다 Windows 저장소 공간을 사용 하는 경우 동일한 VM hello 합니다. 대신, 호환 되는 운영 체제를 사용 하 여 다른 컴퓨터에서 hello 실행 스크립트를 실행 합니다.

### <a name="lvmraid-arrays"></a>LVM/RAID 배열

Linux, 논리 볼륨 관리자 (LVM) 및/또는 소프트웨어에 RAID 배열은 여러 디스크에 걸쳐 사용 되는 toomanage 논리 볼륨을 됩니다. Hello에서 hello 스크립트를 실행할 수 없습니다 Linux VM을 백업 하는 hello LVM 및/또는 RAID 배열을 사용 하는 경우 동일한 VM입니다. 대신 호환 가능한 운영 체제를 사용 하 여 다른 컴퓨터에서 hello 스크립트를 실행 하 고 VM을 백업 하는 hello의 파일 시스템을 지 원하는 합니다.

hello 스크립트 출력 LVM hello 및/또는 RAID 배열 디스크와 hello 볼륨 아래와 같이 hello 파티션 형식으로 표시 됩니다.

   ![Linux LVM 출력 블레이드](./media/backup-azure-restore-files-from-vm/linux-LVMOutput.png)
   
다음 hello toobe 실행 hello 사용자 toobring 하 여 이러한 파티션을 온라인 명령입니다. 

**LVM 파티션의 경우**

```
$ pvs <volume name as shown above in hello script output> 
```
이 실제 볼륨에 hello 볼륨 그룹 이름을 나열합니다.

```
$ lvdisplay <volume-group-name from hello pvs command’s results> 
```
볼륨 그룹에 모든 논리 볼륨, 이름 및 해당 경로를 나열합니다.

```
$ mount <LV path> </mountpath>
```
hello 논리 볼륨 toohello 경로 선택한 toomount 하 고 있습니다.


**RAID 배열의 경우**

```
$ mdadm –detail –scan
```
모든 raid 디스크에 대한 세부 정보를 표시합니다. hello 관련 RAID 디스크도 표시 됩니다.`/dev/mdm/<RAID array name in hello backed up VM>`

Hello RAID 디스크에 실제 볼륨 경우 hello mount 명령을 사용 합니다.
```
$ mount [RAID Disk Path] [/mounthpath]
```

따라야 합니다 LVM 파티션에 대 한 hello RAID 디스크 이름 되 고 hello 볼륨 이름으로 위에서 설명한 것과 동일한 절차 hello이 RAID 디스크의 다른 LVM 여기에 구성 된 경우

## <a name="troubleshooting"></a>문제 해결

Hello 가상 컴퓨터에서 파일을 복구 하는 동안 문제가 되 면 hello 다음 추가 정보에 대 한 표를 확인 합니다.

| 오류 메시지/시나리오 | 가능한 원인 | 권장 작업 |
| ------------------------ | -------------- | ------------------ |
| Exe 출력: *toohello 대상 연결 예외* |스크립트는 수 tooaccess hello 복구 지점 | Hello 컴퓨터 위에서 언급 한 hello 액세스 요구 사항을 충족 하는지 여부를 확인 하십시오.|  
|   Exe 출력: *hello 대상에 이미 로그인 ISCSI 세션을 통해.* |   동일한 컴퓨터와 hello 드라이브가 첨부 된 hello에서 이미 실행 된 hello 스크립트 |   hello 복구 지점 볼륨 hello가 이미 연결 되었습니다. 같은 드라이브 문자를 hello로 탑재 되지 않을 수 있습니다 원본 VM hello 합니다. Hello 사용 가능한 모든 볼륨에 파일에 대 한 hello 파일 탐색기에서 탐색 |
| Exe 출력: *포털/초과 hello 12 시간 제한을 통해 hello 디스크 분리 되어 있으므로이 스크립트 올바르지 않습니다. Hello 포털에서 새 스크립트를 다운로드 하십시오.* |    hello 디스크 hello 포털 또는 hello 12 시간 제한 초과에서 분리 되어 |  이 특정 exe는 현재 유효하지 않고 실행할 수 없습니다. Tooaccess hello 해당 복구 지점 시간의 파일을 원하는 경우 새 exe에 대 한 hello 포털을 방문 합니다.|
| Hello 컴퓨터 hello exe 실행 되는 위치에: hello 새 볼륨 hello 분리 단추를 클릭 한 후 분리 되지 않습니다 |    hello 컴퓨터 hello ISCSI 초기자는 하지 응답/연결 toohello 목표를 새로 고치고 hello 캐시를 유지 관리 |    Hello 분리 단추를 누른 후 몇 분까지 기다립니다. 새 볼륨 hello 여전히 분리 되지 경우 모든 hello 볼륨을 찾으십시오. 사용할 수 없으면 디스크 hello이 강제로 오류 메시지와 함께 hello는 시작자 toorefresh hello 연결과 hello 볼륨이 분리 되었습니다.|
| Exe 출력: 스크립트가 성공적으로 실행 되지만 "새 볼륨이 연결 되어" hello 스크립트 출력에 표시 되지 않으면 |   일시적인 오류입니다.   | hello 볼륨 이미 연결 합니다. 탐색기 toobrowse를 엽니다. 동일 컴퓨터 hello 스크립트 때마다 실행을 사용 하는 경우에 hello 후속 exe 실행에 표시 되어야 hello 목록과 hello 컴퓨터를 다시 시작 하는 것이 좋습니다. |
| Linux 특정: 수 없습니다. tooview hello 필요한 볼륨 | hello 스크립트가 실행 되는 hello 컴퓨터의 운영 체제 hello의 VM을 백업 하는 hello hello 기본 파일 시스템을 인식 하지 못할 수 없습니다. | Hello 복구 지점 수 있는지 여부를 확인은 크래시 일관성이 또는 파일에 일관적인 됩니다. 해당 OS hello를 인식 하는 다른 컴퓨터에서 일관 되 고 실행 hello 스크립트 파일 VM의 파일 시스템 백업 |
| Windows 특정: 수 없습니다. tooview hello 필요한 볼륨 | hello 디스크가 연결 되어 있지만 hello 볼륨 구성 되지 않은 | Hello 디스크 관리 화면에서 hello 추가 디스크 관련된 toohello 복구 지점을 식별 합니다. 이러한 디스크 없는 오프 라인 상태 시도 온라인 hello 디스크를 마우스 오른쪽 단추로 클릭 하 고 '온라인 ' 상태를 클릭 합니다.|
