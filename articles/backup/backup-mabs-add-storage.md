---
title: "Azure 백업 서버 v 2와 함께 최신 백업 저장소 aaaUse | Microsoft Docs"
description: "Hello Azure 백업 서버 v 2의 새로운 기능에 알아봅니다. 이 문서에서는 설명 방법을 tooupgrade 백업 서버 설치 합니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: b2a1ed27a6a682bd611fea1d2df9ef93314404e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-storage-tooazure-backup-server-v2"></a>저장소 tooAzure v2 백업 서버를 추가 합니다.

Azure Backup Server v2에는 System Center 2016 Data Protection Manager Modern Backup Storage가 함께 제공됩니다. Modern Backup Storage를 사용하면 저장소를 50% 절약할 수 있고, 백업이 3배 더 빨라지고, 저장소를 더 효율적으로 사용할 수 있습니다. 저장소에서 워크로드를 인식할 수도 있습니다. 

> [!NOTE]
> 최신 백업 저장소 toouse Windows Server 2016의 백업 서버 v 2를 실행 해야 합니다. Backup Server v2를 이전 버전의 Windows Server에서 실행하면 Azure Backup Server는 Modern Backup Storage를 사용할 수 없습니다. 대신에 Backup Server v1에서 보호하는 것처럼 워크로드를 보호합니다. 자세한 내용은 hello 백업 서버 버전을 참조 하십시오. [보호 매트릭스](backup-mabs-protection-matrix.md)합니다.

## <a name="volumes-in-backup-server-v2"></a>Backup Server v2의 볼륨

Backup Server v2는 저장소 볼륨을 허용합니다. 볼륨을 추가 하는 경우 백업 서버 hello 볼륨 tooResilient ReFS 파일 시스템 ()을 최신 백업 저장소에서 사용 하는 형식을 지정 합니다. tooadd, 볼륨 및 tooexpand 나중 해야 할 경우이 워크플로 사용 하는 것이 좋습니다.

1.  VM에 Backup Server v2를 설치합니다.
2.  저장소 풀의 가상 디스크에 볼륨을 만듭니다.
    1.  디스크 tooa 저장소 풀을 추가 하 고 단순 레이아웃으로 가상 디스크를 만듭니다.
    2.  추가 디스크를 추가 하 고 hello 가상 디스크를 확장 합니다.
    3.  Hello 가상 디스크에 볼륨을 만듭니다.
3.  Hello 볼륨 tooBackup 서버를 추가 합니다.
4.  워크로드 인식 저장소를 구성합니다.

## <a name="create-a-volume-for-modern-backup-storage"></a>Modern Backup Storage에 대한 볼륨 만들기

볼륨이 포함된 Backup Server v2를 디스크 저장소로 사용하면 저장소를 지속적으로 제어할 수 있습니다. 볼륨은 단일 디스크일 수 있습니다. 그러나 hello에 tooextend 저장소를 지정 하지 않고 향후 하려는 경우 저장소 공간을 사용 하 여 만든 디스크 공간 부족 볼륨을 만듭니다. 백업 저장을 위해 tooexpand hello 볼륨을 하려는 경우 유용 합니다. 이 섹션에서는 이 설정을 통해 볼륨을 만드는 모범 사례를 제공합니다.

1. 서버 관리자에서 **파일 및 저장소 서비스** > **볼륨** > **저장소 풀**을 선택합니다. **실제 디스크**에서 **새 저장소 풀**을 선택합니다. 

    ![새 저장소 풀 만들기](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. Hello에 **작업** 드롭다운 상자 **새 가상 디스크**합니다.

    ![가상 디스크 추가](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. Hello 저장소 풀을 선택한 다음 선택 **실제 디스크 추가**합니다.

    ![실제 디스크 추가](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. Hello 실제 디스크를 선택한 다음 선택 **가상 디스크 확장**합니다.

    ![Hello 가상 디스크를 확장 합니다.](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. Hello 가상 디스크를 선택한 다음 선택 **새 볼륨**합니다.

    ![새 볼륨 만들기](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. Hello에 **hello 서버 및 디스크 선택** 대화 상자, 선택 hello 서버 및 hello 새 디스크. 그다음에 **다음**을 선택합니다.

    ![Hello 서버 및 디스크 선택](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-toobackup-server-disk-storage"></a>볼륨 tooBackup 서버 디스크 저장소를 추가 합니다.

hello에 볼륨 tooBackup 서버 tooadd **관리** hello 저장소 다시 검사 하 고 다음을 선택 하는 창 **추가**합니다. 모든 hello 볼륨 사용 가능한 toobe 서버는 백업 저장소에 대 한 추가 목록이 표시 됩니다. 사용할 수 있는 볼륨 선택한 볼륨의 toohello 목록에 추가 된 후 관리 하는 이름 toohelp을 제공할 수 있습니다. 이러한 볼륨 tooReFS 백업 서버 hello 이점의 최신 백업 저장소를 사용할 수 있도록 선택 tooformat **확인**합니다.

![사용 가능한 볼륨 추가](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a>워크로드 인식 저장소 설정

작업량 감지 저장소 우선적으로 특정 종류의 작업 부하를 저장 하는 hello 볼륨을 선택할 수 있습니다. 예를 들어 비용이 많이 드는 볼륨을 지 원하는 많은 수의 두 번째 (IOPS) toostore 전용 hello 작업 자주, 대용량 백업 해야 하는 초당 입력/출력 작업을 설정할 수 있습니다. 예를 들어 트랜잭션 로그가 포함된 SQL Server가 있습니다. Vm의 경우와 같은 덜를 자주 백업 되는 다른 워크 로드 toolow 비용 볼륨을 백업할 수 있습니다.

### <a name="update-dpmdiskstorage"></a>Update-DPMDiskStorage

Data Protection Manager 서버의 hello 저장소 풀에 볼륨의 hello 속성을 업데이트 하는 업데이트-DPMDiskStorage hello PowerShell cmdlet을 사용 하 여 작업 부하 인식 저장소를 설정할 수 있습니다.

구문

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
hello 다음 스크린샷은 hello 업데이트 DPMDiskStorage cmdlet hello PowerShell 창에서.

![hello hello PowerShell 창에서 업데이트 DPMDiskStorage 명령](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

PowerShell을 사용 하 여 hello 변경 hello 백업 서버 관리자 콘솔에에서 반영 됩니다.

![Hello 관리자 콘솔의에서 디스크와 볼륨](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a>다음 단계
백업 서버를 설치한 후에 대해 알아봅니다 어떻게 tooprepare 서버의 작업 보호를 시작 또는 합니다.

- [Backup Server 워크로드 준비](backup-azure-microsoft-azure-backup.md)
- [백업 서버 tooback VMware 서버를 사용 하 여](backup-azure-backup-server-vmware.md)
- [SQL Server를 tooback 백업 서버를 사용 하 여](backup-azure-sql-mabs.md)

