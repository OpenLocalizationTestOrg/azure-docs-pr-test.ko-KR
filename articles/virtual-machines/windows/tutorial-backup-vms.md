---
title: Windows Azure Vm aaaBackup | Microsoft Docs
description: "Azure Backup을 통해 Windows VM을 백업하여 보호합니다."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 1cd3e1940a83aacd160cba3c8613b63b6f3c11d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-virtual-machines-in-azure"></a>Azure에서 Windows 가상 컴퓨터 백업

정기적으로 백업을 수행하여 데이터를 보호할 수 있습니다. Azure Backup은 지역 중복 복구 자격 증명 모음에 저장되는 복구 지점을 만듭니다. 복원할 수는 복구 지점에서 복원할 때는 전체 VM 또는 특정 파일 hello 합니다. 이 문서에서는 단일 toorestore tooa VM 파일 하는 방법을 설명 Windows 서버 및 IIS를 실행 합니다. VM toouse 없는 경우 하나를 만들 수 있습니다 hello를 사용 하 여 [Windows 퀵 스타트](quick-create-portal.md)합니다. 이 자습서에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * VM 백업 만들기
> * 매일 백업 예약
> * 백업에서 파일 복원




## <a name="backup-overview"></a>백업 개요

백업 작업을 시작 하는 hello Azure 백업 서비스 hello 예비 내선 번호 tootake를 지정 시간에 스냅숏으로 트리거합니다. Azure 백업 서비스 hello hello를 사용 하 여 _VMSnapshot_ 확장 합니다. hello 확장 hello VM을 실행 하는 경우 hello 첫 번째 VM 백업 하는 동안 설치 됩니다. Hello VM 실행 되지 않는 경우, hello 백업 서비스는 hello (응용 프로그램 쓰기가 수행 되지 hello VM을 중지 하는 동안) 이후 기본 저장소의 스냅숏을 만듭니다.

Windows Vm의 스냅숏을 만드는, hello 백업 서비스 hello 가상 컴퓨터의 디스크의 일관 된 스냅숏을 hello 볼륨 섀도 복사본 서비스 (VSS) tooget와 동등 합니다. Hello Azure 백업 서비스는 hello 스냅숏을, 되 면 hello 데이터는 전송 된 toohello 자격 증명 모음입니다. toomaximize 효율성 hello 서비스를 식별 하 고 hello 이전 백업 이후에 변경 된 데이터의 hello 블록만 전송 합니다.

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

## <a name="recover-a-file"></a>파일 복구

실수로 삭제 하거나 변경 tooa 파일 확인을 하는 경우에 백업 자격 증명 모음에서 파일 복구 toorecover hello 파일을 사용할 수 있습니다. 파일 복구 hello VM에서 실행 되는 스크립트를 사용 하 여 로컬 드라이브로 toomount hello 복구 지점입니다. 이러한 드라이브 남습니다 탑재 된 12 시간 동안 hello 복구 지점에서 파일을 복사 하 고 toohello VM을 복원할 수 있도록 합니다.  

이 예제에서는 toorecover IIS에 대 한 hello 기본 웹 페이지에 사용 되는 이미지 파일을 hello 하는 방법을 보여 줍니다. 

1. 브라우저를 열고 hello VM tooshow hello 기본 IIS 페이지의 toohello IP 주소를 연결 합니다.

    ![기본 IIS 웹 페이지](./media/tutorial-backup-vms/iis-working.png)

2. Toohello VM을 연결 합니다.
3. Hello VM에서 엽니다 **파일 탐색기** too\inetpub\wwwroot 이동 하 고 hello 파일을 삭제 하 고 **iisstart.png**합니다.
4. 로컬 컴퓨터의 이미지 hello 기본 IIS 페이지 hello 새로 고침 hello 브라우저 toosee 사라지게 됩니다.

    ![기본 IIS 웹 페이지](./media/tutorial-backup-vms/iis-broken.png)

5. 로컬 컴퓨터에를 열고 새 탭 이동 hello hello [Azure 포털](https://portal.azure.com)합니다.
6. Hello hello 왼쪽 메뉴에서 선택 **가상 컴퓨터** 및 선택 hello VM 양식 hello 목록입니다.
8. Hello에 hello VM 블레이드에서 **설정** 섹션에서 클릭 **백업**합니다. hello **백업** 블레이드를 엽니다. 
9. Hello hello 블레이드의 hello 위쪽 메뉴에서 선택 **파일 복구**합니다. hello **파일 복구** 블레이드를 엽니다.
10. **1 단계: 복구 지점을 선택**를 hello 드롭다운 목록에서 복구 지점을 선택 합니다.
11. **2 단계: 스크립트 toobrowse 다운로드 하 고 파일을 복구할**, hello 클릭 **실행 파일을 다운로드** 단추입니다. Hello 파일 tooyour 저장 **다운로드** 폴더입니다.
12. 로컬 컴퓨터에서 엽니다 **파일 탐색기** tooyour 이동 **다운로드** 폴더 및 복사 hello.exe 파일을 다운로드 합니다. VM 이름으로 접두사가 hello 파일 이름입니다. 
13. (RDP 연결 hello)를 통해 VM에 hello.exe 파일 toohello를 VM의 데스크톱에 붙여 넣습니다. 
14. VM의 toohello 데스크톱 이동한 hello.exe를 두 번 클릭 합니다. 명령 프롬프트를 시작 되 고 액세스할 수 있는 파일 공유로 복구 지점을 hello를 탑재 합니다. 완료 되 면 입력 hello 공유를 만들 **q** tooclose hello 명령 프롬프트입니다.
15. VM을 열고 **파일 탐색기** hello 파일 공유에 사용 된 toohello 드라이브 문자를 이동 합니다.
16. 복사 및 too\inetpub\wwwroot 탐색 **iisstart.png** hello 파일에서 공유 하 고 \inetpub\wwwroot에 붙여 넣습니다. 예를 들어 F:\inetpub\wwwroot\iisstart.png 복사한 c:\inetpub\wwwroot toorecover hello 파일에 붙여 넣습니다.
17. 로컬 컴퓨터에 연결 되어 있는 hello 브라우저 탭을 열고 toohello IP 주소를 hello VM hello IIS 기본 페이지를 표시 합니다. CTRL + f 5를 눌러 toorefresh hello 브라우저 페이지. 이제 해당 hello 표시 이미지 복원 되었습니다.
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









