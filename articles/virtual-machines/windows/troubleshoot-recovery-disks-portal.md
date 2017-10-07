---
title: "windows hello Azure 포털에서에서 VM을 문제 해결 aaaUse | Microsoft Docs"
description: "어떻게 연결 hello OS 디스크 tooa 복구 VM 사용 하 여 tootroubleshoot Windows 가상 컴퓨터 문제 Azure의 hello Azure 포털에 알아봅니다"
services: virtual-machines-windows
documentationCenter: 
authors: genlin
manager: timlt
editor: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 396f70338fa39f80bb9adcb9244d3c83f2a233eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-portal"></a>Windows VM hello OS 디스크 tooa 복구 VM을 연결 하 여 문제 해결 Azure 포털 hello를 사용 하 여
Azure에서 Windows 가상 컴퓨터 (VM) 부팅 또는 디스크 오류가 발생 하는 경우 문제 해결 단계는 자체 hello 가상 하드 디스크에서 tooperform을 할 수 있습니다. 일반적인 예로 hello VM 수 tooboot 성공적으로 않도록 방지 하는 실패 한 응용 프로그램 업데이트는 것입니다. 이 문서에 자세히 설명 방법 toouse hello Azure 포털 tooconnect 가상 하드 디스크 tooanother Windows VM toofix 오류를 다음 다시 원래 VM를 만듭니다.

## <a name="recovery-process-overview"></a>복구 프로세스 개요
hello 문제 해결 과정은 다음과 같습니다.

1. Hello VM 발생 문제, 유지 hello 가상 하드 디스크를 삭제 합니다.
2. 첨부 하 고 문제 해결을 위해 hello 가상 하드 디스크 tooanother Windows VM에 탑재 합니다.
3. Toohello VM 문제 해결을 연결 합니다. 파일을 편집 하거나 hello 원래 가상 하드 디스크에서 다양 한 도구 toofix 문제를 실행 합니다.
4. 탑재 해제 하 고 VM의 문제를 해결 하는 hello에서 hello 가상 하드 디스크를 분리 합니다.
5. Hello 원래 가상 하드 디스크를 사용 하는 VM을 만듭니다.


## <a name="determine-boot-issues"></a>부팅 문제 확인
VM 없는 이유 수 tooboot 올바르게 toodetermine hello 부트 진단이 VM 스크린샷을 검사 합니다. 일반적인 예로는 응용 프로그램 업데이트가 실패하거나 기본 가상 하드 디스크를 삭제 또는 이동하는 것입니다.

Hello 포털에서 VM을 선택 하 고 다음 toohello 아래쪽으로 스크롤하여 **지원 + 문제 해결** 섹션. 클릭 **진단 부팅** tooview hello 스크린 샷 합니다. 특정 오류 메시지 또는 오류 코드에 유의 toohelp hello VM 문제 발생 이유를 확인 합니다. hello 다음 예제에서 서비스를 중지 대기 VM:

![VM 부팅 진단 콘솔 로그 보기](./media/troubleshoot-recovery-disks-portal/screenshot-error.png)

클릭할 수도 있습니다 **스크린 샷** toodownload hello VM 스크린 샷 캡처.


## <a name="view-existing-virtual-hard-disk-details"></a>기존 가상 하드 디스크 세부 정보 보기
가상 하드 디스크 tooanother VM에 연결할 수 있습니다, 전에 hello 가상 하드 디스크 (VHD)의 tooidentify hello 이름이 필요 합니다. 

Hello 포털에서 리소스 그룹을 선택 하 고 저장소 계정을 선택 합니다. 클릭 **Blob**와 같이, 다음 예제는 hello:

![저장소 Blob 선택](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

일반적으로 가상 하드 디스크를 저장하는 **vhd**로 명명된 컨테이너가 있습니다. Hello 컨테이너 tooview 가상 하드 디스크의 목록을 선택 합니다. VHD의 참고 hello 이름 (hello 접두사는 일반적으로 hello 이름 VM의):

![저장소 컨테이너에서 VHD 식별](./media/troubleshoot-recovery-disks-portal/storage-container.png)

Hello 목록에서 기존 가상 하드 디스크를 선택 하 고 단계를 수행 하는 hello에 사용 하기 위해 hello URL을 복사 합니다.

![기존 가상 하드 디스크 URL 복사](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a>기존 VM 삭제
가상 하드 디스크와 VM은 Azure의 두 가지 별개의 리소스입니다. 가상 하드 디스크는 자체 hello 운영 체제, 응용 프로그램 및 구성 저장 됩니다. hello VM 자체 hello 크기 또는 위치를 정의 하 고 가상 하드 디스크 또는 가상 네트워크 인터페이스 카드 (NIC) 등의 리소스를 참조 하는 메타 데이터 일 뿐입니다. 각 가상 하드 디스크에 연결 되어 있을 때 할당 한 임 대권을 tooa VM입니다. 데이터 디스크를 연결 하 고 hello VM에서 실행 중인 동안에 분리 수, 있지만 hello VM 리소스는 삭제 하지 않는 한 hello OS 디스크를 분리할 수 없습니다. hello 임대는 해당 VM 중지 및 할당 취소 된 상태에 있을 경우에 tooassociate hello OS 디스크는 VM으로 계속 됩니다.

첫 번째 단계 toorecover hello VM은 자체 toodelete hello VM 리소스입니다. VM 삭제 hello 저장소 계정의 hello 가상 하드 디스크를 유지합니다. VM을 삭제 하는 hello, 후 hello 가상 하드 디스크 tooanother VM tootroubleshoot 첨부 고 hello 오류를 해결 합니다.

Hello 포털에서 VM을 선택한 다음 클릭 **삭제**:

![부팅 오류를 보여 주는 VM 부팅 진단 스크린샷](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

Hello VM가 hello 가상 하드 디스크 tooanother VM을 연결 하기 전에 삭제를 마치기 때까지 기다립니다. hello 임대 VM hello로 연결 하는 hello 가상 하드 디스크에 toobe hello 가상 하드 디스크 tooanother VM을 연결 하기 전에 해제 해야 합니다.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>기존 가상 하드 디스크 tooanother VM 연결
에 대 한 hello 다음 몇 단계 문제 해결을 위해 다른 VM을 사용 합니다. Hello 기존 가상 하드 디스크 toothis VM toobe 수 toobrowse 문제 해결을 첨부 하 고이 정보를 hello 디스크의 콘텐츠를 편집 합니다. 이 프로세스 toocorrect를 통해 모든 구성 오류 또는 추가 응용 프로그램을 확인 또는 로그 파일, 예를 들어 시스템. 선택 하거나 문제 해결을 위해 다른 VM toouse 만듭니다.

1. Hello 포털에서 리소스 그룹을 선택 하 고 문제 해결 VM을 선택 합니다. **디스크**를 선택한 다음 **기존 연결**을 클릭합니다.

    ![Hello 포털에서 기존 디스크 연결](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. tooselect 기존 가상 하드 디스크를 클릭 **VHD 파일**:

    ![기존 VHD 찾아보기](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. 저장소 계정 및 컨테이너를 선택한 다음 기존 VHD를 클릭합니다. Hello 클릭 **선택** tooconfirm 선택한 단추:

    ![기존 VHD 선택](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. 이제 선택한 VHD를 클릭 **확인** tooattach hello 기존 가상 하드 디스크:

    ![기존 가상 하드 디스크 연결 확인](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. 몇 초 후 hello **디스크** VM에 대 한 창에 데이터 디스크로 연결 된 기존 가상 하드 디스크를 나열 합니다.

    ![데이터 디스크로 연결된 기존 가상 하드 디스크](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-hello-attached-data-disk"></a>Hello 연결 된 데이터 디스크를 탑재

1. 원격 데스크톱 연결 tooyour VM을 엽니다. Hello 포털에서 VM을 선택 하 고 클릭 **연결**합니다. 다운로드 하 고 hello RDP 연결 파일을 엽니다. 자격 증명 toolog tooyour VM에에서 다음과 같이 입력 합니다.

    ![Tooyour 원격 데스크톱을 사용 하 여 VM에 로그인](./media/troubleshoot-recovery-disks-portal/open-remote-desktop.png)

2. **서버 관리자**를 연 다음 **파일 및 저장소 서비스**를 선택합니다. 

    ![서버 관리자에서 파일 및 저장소 서비스 선택](./media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

3. hello 데이터 디스크가 자동으로 감지 되 고 연결 합니다. 연결 된 디스크, 선택 toosee hello 목록이 **디스크**합니다. 사용자 데이터 디스크 tooview 볼륨 정보를 hello 드라이브 문자를 포함 하 여 선택할 수 있습니다. 다음 예제에서는 연결 된 데이터 디스크를 hello 및 사용 하 여 hello **f:**:

    ![서버 관리자의 연결된 디스크 및 볼륨 정보](./media/troubleshoot-recovery-disks-portal/server-manager-disk-attached.png)


## <a name="fix-issues-on-original-virtual-hard-disk"></a>원래 가상 하드 디스크의 문제 해결
이제 hello 기존 가상 하드 디스크를 탑재, 모든 유지 관리 및 문제 해결 단계는 필요에 따라 수행할 수 있습니다. Hello 문제를 해결 한 후 단계를 수행 하는 hello로 계속 합니다.


## <a name="unmount-and-detach-original-virtual-hard-disk"></a>원래 가상 하드 디스크의 탑재 해제 및 분리
프로그램 오류가 해결 되 면 hello 기존 가상 하드 디스크 문제 해결 VM에서 분리 합니다. VM의 문제를 해결 하는 hello 가상 하드 디스크 toohello 연결 hello 임대가 해제 될 때까지 다른 VM과 가상 하드 디스크를 사용할 수 없습니다.

1. Hello RDP 세션 tooyour VM에서에서 열고 **서버 관리자**을 선택한 후 **파일 및 저장소 서비스**:

    ![서버 관리자에서 파일 및 저장소 서비스 선택](./media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

2. **디스크**를 선택한 다음 데이터 디스크를 선택합니다. 데이터 디스크를 마우스 오른쪽 단추로 클릭하고 **오프라인 상태로 전환**을 선택합니다.

    ![서버 관리자에서 오프 라인으로 hello 데이터 디스크 설정](./media/troubleshoot-recovery-disks-portal/server-manager-set-disk-offline.png)

3. 이제 hello hello VM에서에서 가상 하드 디스크를 분리 합니다. Hello Azure 포털에서에서 VM을 선택 하 고 클릭 **디스크**합니다. 기존 가상 하드 디스크를 선택한 다음 **분리**를 클릭합니다.

    ![기존 가상 하드 디스크 분리](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    계속 하기 전에 VM hello hello 데이터 디스크를 성공적으로 분리 된 때까지 기다립니다.

## <a name="create-vm-from-original-hard-disk"></a>원래 하드 디스크에서 VM 만들기
원래 가상 하드 디스크에서 VM에서 사용할 toocreate [이 Azure 리소스 관리자 템플릿을](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet)합니다. hello에서 VHD URL hello를 사용 하 여 기존 가상 네트워크를으로 VM을 배포 하는 hello 템플릿 이전 명령입니다. Hello 클릭 **tooAzure 배포** 다음과 같이 단추:

![GitHub의 템플릿에서 VM 배포](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

hello 템플릿 배포에 대 한 Azure 포털 hello에 로드 됩니다. 새 VM 및 기존 Azure 리소스에 대 한 hello 이름을 입력 하 고 hello URL tooyour 기존 가상 하드 디스크를 붙여 넣습니다. toobegin hello 배포 클릭 **구매**:

![템플릿에서 VM 배포](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a>부트 진단 다시 사용
Hello 기존 가상 하드 디스크에서 VM을 만들 때 부트 진단이 자동으로 사용할 수 없습니다. toocheck 부트 진단의 상태를 hello 및 hello 포털에서 VM을 선택 합니다. 필요한 경우 설정 합니다. **모니터링**에서 **진단 설정**을 클릭합니다. Hello 상태는 확인 **에**, 너무 확인 표시를 다음 hello 및**진단 부팅** 을 선택 합니다. 항목을 변경하려면 **저장**을 클릭합니다.

![부팅 진단 설정 업데이트](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a>다음 단계
Tooyour VM을 연결 하는 데 문제가 있는 경우 참조 [문제를 해결 하는 RDP 연결 tooan Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. VM에서 실행 중인 응용 프로그램에 액세스하는 데 문제가 있는 경우 [Windows VM에서 응용 프로그램 연결 문제 해결](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.

Resource Manager를 사용하는 방법에 대한 자세한 내용은 [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.