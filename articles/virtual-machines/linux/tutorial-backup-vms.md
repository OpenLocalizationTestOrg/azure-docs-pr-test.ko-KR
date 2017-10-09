---
title: "Azure Linux VM 백업 | Microsoft Docs"
description: "Azure Backup을 통해 Linux VM을 백업하여 보호합니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 7c00392d5185a2f067f2ee2717529dcbde1e71f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-linux--virtual-machines-in-azure"></a>Azure에서 Linux 가상 컴퓨터 백업

정기적으로 백업을 수행하여 데이터를 보호할 수 있습니다. Azure Backup은 지역 중복 복구 자격 증명 모음에 저장되는 복구 지점을 만듭니다. 복원할 수는 복구 지점에서 복원할 때는 전체 VM 또는 특정 파일 hello 합니다. 이 문서에서는 toorestore 단일 tooa Linux VM 실행 중인 nginx 파일 하는 방법을 설명 합니다. VM toouse 없는 경우 하나를 만들 수 있습니다 hello를 사용 하 여 [Linux 퀵 스타트](quick-create-cli.md)합니다. 이 자습서에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * VM 백업 만들기
> * 매일 백업 예약
> * 백업에서 파일 복원



## <a name="backup-overview"></a>백업 개요

백업을 시작 하는 hello Azure 백업 서비스를 hello 예비 내선 번호 tootake를 지정 시간에 스냅숏으로 트리거합니다. Azure 백업 서비스 hello hello를 사용 하 여 _VMSnapshotLinux_ Linux에서 확장 합니다. hello 확장 hello VM을 실행 하는 경우 hello 첫 번째 VM 백업 하는 동안 설치 됩니다. Hello VM 실행 되지 않는 경우, hello 백업 서비스는 hello (응용 프로그램 쓰기가 수행 되지 hello VM을 중지 하는 동안) 이후 기본 저장소의 스냅숏을 만듭니다.

기본적으로 Azure 백업에서는 파일 시스템 일관성 백업을 Linux VM에 대 한 구성된 tootake 수 없지만 [전 스크립트와 사후 스크립트 프레임 워크를 사용 하 여 응용 프로그램 일치 백업을](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent)합니다. Hello Azure 백업 서비스는 hello 스냅숏을, 되 면 hello 데이터는 전송 된 toohello 자격 증명 모음입니다. toomaximize 효율성 hello 서비스를 식별 하 고 hello 이전 백업 이후에 변경 된 데이터의 hello 블록만 전송 합니다.

Hello 데이터 전송이 완료 되 면 hello 스냅숏을 제거 되 고 복구 지점이 생성 됩니다.


## <a name="create-a-backup"></a>백업 만들기
간단한 예약 된 매일 백업 tooa 복구 서비스 자격 증명 모음을 만듭니다. 

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. Hello hello 왼쪽 메뉴에서 선택 **가상 컴퓨터**합니다. 
3. Hello 목록에서 VM tooback를 선택 합니다.
4. Hello에 hello VM 블레이드에서 **설정** 섹션에서 클릭 **백업**합니다. hello **백업 사용** 블레이드를 엽니다.
5. **복구 서비스 자격 증명 모음**, 클릭 **새로 만들기** hello hello 새 자격 증명 모음 이름을 제공 합니다. 새 자격 증명 모음에서에서 만든 hello 동일한 리소스 그룹 및 hello 가상 컴퓨터로 위치입니다.
6. **백업 정책**을 클릭합니다. 이 예에서는 hello 기본값을 유지 하 고 클릭 **확인**합니다.
7. Hello에 **백업 사용** 블레이드에서 클릭 **백업 사용**합니다. 이렇게 하면 hello 기본 일정에 따라 매일 백업을 만들어집니다.
10. 초기 복구 지점 hello에 toocreate **백업** 블레이드 클릭 **지금 백업**합니다.
11. Hello에 **지금 백업** 블레이드에서 hello 달력 아이콘을 hello 달력 컨트롤 tooselect hello 마지막 날이 복구 지점을 유지 하 고 클릭을 사용 하 여 **백업**합니다.
12. Hello에 **백업** 블레이드에서 VM에 대 한 완료 된 복구 지점 hello 수가 표시 됩니다.

    ![복구 지점](./media/tutorial-backup-vms/backup-complete.png)

hello 첫 번째 백업에는 20 분 정도 걸립니다. 백업이 완료 된 후 toohello이이 자습서의 다음 단계를 진행 합니다.

## <a name="restore-a-file"></a>파일 복원

실수로 삭제 하거나 변경 tooa 파일 확인을 하는 경우에 백업 자격 증명 모음에서 파일 복구 toorecover hello 파일을 사용할 수 있습니다. 파일 복구 hello VM에서 실행 되는 스크립트를 사용 하 여 로컬 드라이브로 toomount hello 복구 지점입니다. 이러한 드라이브 남습니다 탑재 된 12 시간 동안 hello 복구 지점에서 파일을 복사 하 고 toohello VM을 복원할 수 있도록 합니다.  

이 예제에서는 toorecover 기본 nginx 웹 페이지 /var/www/html/index.nginx-debian.html hello 하는 방법을 보여 줍니다. 이 예에서 VM의 공용 IP 주소 hello는 *13.69.75.209*합니다. 사용 하 여 vm의 hello IP 주소를 찾을 수 있습니다.

 ```bash 
 az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
 ```

 
1. 로컬 컴퓨터의 VM toosee hello 기본 nginx 웹 페이지의 hello 공용 IP 주소에서 유형과 브라우저를 엽니다.

    ![기본 nginx 웹 페이지](./media/tutorial-backup-vms/nginx-working.png)

1. VM에 SSH를 수행합니다

    ```bash
    ssh 13.69.75.209
    ```
2. /var/www/html/index.nginx-debian.html을 삭제합니다.

    ```bash
    sudo rm /var/www/html/index.nginx-debian.html
    ```
    
4. 로컬 컴퓨터에서 CTRL 키를 눌러 hello 브라우저를 새로 고치려면 + 기본 nginx 페이지 F5 toosee는 사라집니다.

    ![기본 nginx 웹 페이지](./media/tutorial-backup-vms/nginx-broken.png)
    
1. 로컬 컴퓨터에서 toohello에 로그인 [Azure 포털](https://portal.azure.com/)합니다.
6. Hello hello 왼쪽 메뉴에서 선택 **가상 컴퓨터**합니다. 
7. Hello 목록에서 hello VM을 선택 합니다.
8. Hello에 hello VM 블레이드에서 **설정** 섹션에서 클릭 **백업**합니다. hello **백업** 블레이드를 엽니다. 
9. Hello hello 블레이드의 hello 위쪽 메뉴에서 선택 **파일 복구**합니다. hello **파일 복구** 블레이드를 엽니다.
10. **1 단계: 복구 지점을 선택**를 hello 드롭다운 목록에서 복구 지점을 선택 합니다.
11. **2 단계: 스크립트 toobrowse 다운로드 하 고 파일을 복구할**, hello 클릭 **실행 파일을 다운로드** 단추입니다. 로컬 컴퓨터를 tooyour hello 다운로드 한 파일을 저장 합니다.
7. 클릭 **스크립트 다운로드** toodownload hello 스크립트 파일을 로컬입니다.
8. Bash 프롬프트 유형과 hello 뒤, 대체 열고 *Linux_myVM_05-05-2017.sh* hello 경로 파일 이름을 다운로드 한 hello 스크립트에 대 한 올바른 *azureuser* hello VM에 대 한 hello 사용자 이름으로 및 *13.69.75.209* hello VM에 대 한 공용 IP 주소와 합니다.
    
    ```bash
    scp Linux_myVM_05-05-2017.sh azureuser@13.69.75.209:
    ```
    
9. 로컬 컴퓨터에서 SSH 연결 toohello VM을 엽니다.

    ```bash
    ssh 13.69.75.209
    ```
    
10. VM에서 추가 권한 toohello 스크립트 파일을 실행 합니다.

    ```bash
    chmod +x Linux_myVM_05-05-2017.sh
    ```
    
11. VM에서 hello 스크립트 toomount hello 복구 지점 파일 시스템으로 실행 합니다.

    ```bash
    ./Linux_myVM_05-05-2017.sh
    ```
    
12. hello는 hello 탑재 지점에 대 한 경로 hello hello 스크립트 제공에서 출력입니다. hello 출력은 유사한 toothis 합니다.

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
                          
    Connecting toorecovery point using ISCSI service...
    
    Connection succeeded!
    
    Please wait while we attach volumes of hello recovery point toothis machine...
                         
    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath 

    1)  | /dev/sdc  |  /dev/sdc1  |  /home/azureuser/myVM-20170505191055/Volume1

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

12. VM을 복사 hello nginx 기본 웹 페이지 hello 파일 hello 탑재 지점 백 toowhere에서 삭제 합니다.

    ```bash
    sudo cp ~/myVM-20170505191055/Volume1/var/www/html/index.nginx-debian.html /var/www/html/
    ```
    
17. 로컬 컴퓨터에 연결 되어 있는 hello 브라우저 탭을 열고 toohello IP 주소를 hello VM hello nginx 기본 페이지를 표시 합니다. CTRL + f 5를 눌러 toorefresh hello 브라우저 페이지. 이제 해당 hello 표시 기본 페이지가 다시 작동 합니다.

    ![기본 nginx 웹 페이지](./media/tutorial-backup-vms/nginx-working.png)

18. 로컬 컴퓨터에 돌아가서 toohello 브라우저 탭과 hello Azure 포털에 대 한 **3 단계: 복구 후 hello 디스크를 마운트 해제** hello 클릭 **디스크 분리** 단추입니다. 이 단계를 toodo을 잊은 경우 hello 연결 toohello "탑재 지점" 닫혀 자동으로 12 시간 후입니다. 이러한 12 시간 후 새 스크립트 toocreate 새 "탑재 지점" toodownload를 해야합니다.


## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음 방법에 대해 알아보았습니다.

> [!div class="checklist"]
> * VM 백업 만들기
> * 매일 백업 예약
> * 백업에서 파일 복원

가상 컴퓨터를 모니터링 하는 방법에 대 한 다음 자습서 toolearn toohello를 진행 합니다.

> [!div class="nextstepaction"]
> [가상 컴퓨터 모니터링](tutorial-monitoring.md)

