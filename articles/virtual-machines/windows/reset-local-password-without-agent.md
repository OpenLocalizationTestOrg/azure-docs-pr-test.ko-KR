---
title: "Azure 에이전트 없이 로컬 Windows 암호 aaaReset | Microsoft Docs"
description: "Hello Azure 게스트 에이전트가 설치 되어 있지 않거나 VM에서 올바르게 작동 하는 경우 로컬 Windows 사용자 계정의 암호 tooreset hello 하는 방법"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf353dd3-89c9-47f6-a449-f874f0957013
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/07/2017
ms.author: iainfou
ms.openlocfilehash: c559c31ea142f9cf50d2c5b6182c5355fec9bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-windows-password-for-azure-vm"></a>어떻게 tooreset Azure VM에 대 한 로컬 Windows 암호
Hello hello를 사용 하 여 Azure에서 VM의 로컬 Windows 암호를 다시 설정할 수 있습니다 [Azure 포털 또는 Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello Azure 게스트 에이전트가 설치 되어 제공 합니다. 이 메서드는 기본 방법 tooreset hello Azure VM에 대 한 암호입니다. Hello Azure 게스트 에이전트가 응답 하지 않거나 사용자 지정 이미지를 업로드 한 후 tooinstall 실패 된 문제를 발생 하는 경우 Windows 암호를 수동으로 다시 설정할 수 있습니다. 이 문서 tooreset 로컬 계정 암호를 연결 하 여 운영 체제 원본 가상 디스크 tooanother VM hello 하는 방법을 설명 합니다. 

> [!WARNING]
> 이 프로세스는 마지막 수단으로만 사용합니다. 항상 tooreset hello를 사용 하 여 암호를 시도 [Azure 포털 또는 Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 첫 번째입니다.
> 
> 

## <a name="overview-of-hello-process"></a>Hello 프로세스의 개요
로컬 암호 액세스 toohello Azure 게스트 에이전트가 때 Azure에서 Windows VM에 대 한 재설정을 수행 하기 위한 hello 핵심 단계는 다음과 같습니다.

* Hello 원본 VM을 삭제 합니다. hello 가상 디스크에 그대로 유지 됩니다.
* Hello에 hello 소스 VM의 OS 디스크 tooanother VM 연결 Azure 구독 내에서 같은 위치입니다. 이 VM은 참조 tooas hello VM 문제를 해결 합니다.
* VM의 문제를 해결 하는 hello를 사용 하 여 hello 소스 VM의 OS 디스크에 일부 구성 파일을 만듭니다.
* VM의 문제를 해결 하는 hello에서 hello VM의 OS 디스크를 분리 합니다.
* 리소스 관리자 템플릿 toocreate hello 원래 가상 디스크를 사용 하 여 VM을 사용 합니다.
* Hello 새 VM 부팅을 hello config 파일 때 필요한 hello 사용자의 hello 암호를 업데이트를 만듭니다.

## <a name="detailed-steps"></a>자세한 단계
항상 tooreset hello를 사용 하 여 암호를 시도 [Azure 포털 또는 Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello 다음 단계를 시도 하기 전에. 시작하기 전에 VM을 백업했는지 확인합니다. 

1. 삭제 hello Azure 포털에서 VM의 영향을 합니다. VM 삭제 hello만 hello Azure 내에서 VM의 hello 참조 hello 메타 데이터를 삭제합니다. hello 가상 디스크는 hello VM 삭제 될 때 유지 됩니다.
   
   * Hello Azure 포털에에서 선택 hello VM 클릭 *삭제*:
     
     ![기존 VM 삭제](./media/reset-local-password-without-agent/delete_vm.png)
2. Hello 소스 VM의 OS 디스크 toohello VM 문제 해결을 연결 합니다. VM의 문제를 해결 하는 hello hello에 있어야 합니다. hello 소스 VM의 OS 디스크와 동일한 지역 (예: `West US`):
   
   * Hello hello Azure 포털에서에서 VM을 문제 해결을 선택 합니다. *디스크* | *기존 연결*을 클릭합니다.
     
     ![기존 디스크 연결](./media/reset-local-password-without-agent/disks_attach_existing.png)
     
     선택 *VHD 파일* 한 후 원본 VM을 포함 하는 hello 저장소 계정을 선택 합니다.
     
     ![저장소 계정 선택](./media/reset-local-password-without-agent/disks_select_storageaccount.PNG)
     
     Hello 소스 컨테이너를 선택 합니다. hello 원본 컨테이너는 일반적으로 *vhd*:
     
     ![저장소 컨테이너 선택](./media/reset-local-password-without-agent/disks_select_container.png)
     
     운영 체제 vhd tooattach hello를 선택 합니다. 클릭 *선택* toocomplete hello 프로세스:
     
     ![원본 가상 디스크 선택](./media/reset-local-password-without-agent/disks_select_source_vhd.png)
3. 원격 데스크톱을 사용 하 여 VM을 문제 해결 toohello를 연결 하 고 hello 소스 VM의 OS 디스크가 표시:
   
   * Hello hello Azure 포털에서에서 VM을 문제 해결을 선택 하 고 클릭 *연결*합니다.
   * 다운로드 하는 hello RDP 파일을 엽니다. Hello 사용자 이름 및 VM 문제를 해결 하는 hello의 암호를 입력 합니다.
   * 파일 탐색기에서 연결 하는 hello 데이터 디스크를 찾습니다. Hello VM의 VHD가 소스 hello VM 문제를 해결 하는 유일한 데이터 연결 된 디스크 toohello, hello f: 드라이브가 상태 여야 합니다.
     
     ![연결된 데이터 디스크 보기](./media/reset-local-password-without-agent/troubleshooting_vm_fileexplorer.png)
4. 만들 `gpt.ini` 에 `\Windows\System32\GroupPolicy` hello 소스 VM의 드라이브에 있음 (gpt.ini 있으면 이름을 toogpt.ini.bak):
   
   > [!WARNING]
   > 않는 실수로 C:\Windows에 있는 파일을 다음 hello 만들 하 hello hello VM 문제 해결에 대 한 운영 체제 드라이브에 있는지 확인 합니다. Hello 다음 원본에 데이터 디스크로 연결 된 VM에 대 한 hello 운영 체제 드라이브에 파일을 만듭니다.
   > 
   > 
   
   * Hello에 줄을 다음 hello 추가 `gpt.ini` 만든 파일:
     
     ```
     [General]
     gPCFunctionalityVersion=2
     gPCMachineExtensionNames=[{42B5FAAE-6536-11D2-AE5A-0000F87571E3}{40B6664F-4972-11D1-A7CA-0000F87571E3}]
     Version=1
     ```
     
     ![gpt.ini 만들기](./media/reset-local-password-without-agent/create_gpt_ini.png)
5. `\Windows\System32\GroupPolicy\Machine\Scripts`에 `scripts.ini`를 만듭니다. 숨겨진 폴더가 표시되어 있는지 확인합니다. 필요한 경우 만들 hello `Machine` 또는 `Scripts` 폴더입니다.
   
   * 다음 줄 hello hello 추가 `scripts.ini` 만든 파일:
     
     ```
     [Startup]
     0CmdLine=C:\Windows\System32\FixAzureVM.cmd
     0Parameters=
     ```
     
     ![scripts.ini 만들기](./media/reset-local-password-without-agent/create_scripts_ini.png)
6. 만들기 `FixAzureVM.cmd` 에 `\Windows\System32` 내용 뒤, 대체 hello로 `<username>` 및 `<newpassword>` 고유한 값으로.
   
    ```
    net user <username> <newpassword> /add
    net localgroup administrators <username> /add
    net localgroup "remote desktop users" <username> /add

    ```

    ![FixAzureVM.cmd 만들기](./media/reset-local-password-without-agent/create_fixazure_cmd.png)
   
    Hello 새 암호를 정의 하는 경우에 VM에 대 한 암호 복잡성 요구 사항을 구성 하는 hello를 충족 해야 합니다.
7. Azure 포털에서 VM의 문제를 해결 하는 hello에서 hello 디스크를 분리 합니다.
   
   * Hello Azure 포털에서에서 VM 문제를 해결 하는 hello 선택를 클릭 *디스크*합니다.
   * 2 단계에서 연결 된 선택 hello 데이터 디스크를 클릭 *분리*:
     
     ![디스크 분리](./media/reset-local-password-without-agent/detach_disk.png)
8. VM을 만들기 전에 hello URI tooyour 소스 OS 디스크를 가져옵니다.
   
   * Hello Azure 포털에서에서 저장소 계정을 선택 hello 클릭 *Blob*합니다.
   * Hello 컨테이너를 선택 합니다. hello 원본 컨테이너는 일반적으로 *vhd*:
     
     ![저장소 계정 Blob 선택](./media/reset-local-password-without-agent/select_storage_details.png)
     
     소스 VM OS VHD를 선택 하 고 hello 클릭 *복사* 단추 다음 toohello *URL* 이름:
     
     ![디스크 URI 복사](./media/reset-local-password-without-agent/copy_source_vhd_uri.png)
9. Hello 소스 VM의 OS 디스크에서 VM을 만듭니다.
   
   * 사용 하 여 [이 Azure 리소스 관리자 템플릿을](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate 특수 VHD에서 VM입니다. Hello 클릭 `Deploy tooAzure` 단추 tooopen hello Azure 포털 hello 템플릿 기반 세부 정보가 채워집니다.
   * Hello VM에 대 한 모든 hello 이전 설정을 tooretain 하려는 경우 선택 *템플릿 편집* tooprovide 기존 VNet, 서브넷, 네트워크 어댑터 또는 공용 IP입니다.
   * Hello에 `OSDISKVHDURI` 매개 변수 텍스트 상자, 붙여넣기 hello hello 앞 단계에서에서 원본 VHD의 URI를 가져올:
     
     ![템플릿에서 VM 만들기](./media/reset-local-password-without-agent/create_new_vm_from_template.png)
10. 새 VM에서 실행 되 고 hello, 후 toohello hello 새 암호로 hello에 지정 된 원격 데스크톱을 사용 하 여 VM을 연결 `FixAzureVM.cmd` 스크립트입니다.
11. 원격 세션 toohello에서 새 VM을 따라 제거 hello hello 환 tooclean 파일:
    
    * %windir%\System32에서
      * FixAzureVM.cmd 제거
    * %windir%\System32\GroupPolicy\Machine\에서
      * scripts.ini 제거
    * %windir%\System32\GroupPolicy에서
      * (gpt.ini, 전에 있으며 toogpt.ini.bak, 이름 바꾸기 hello.bak 파일 백 toogpt.ini 바꾼) 경우 gpt.ini 제거

## <a name="next-steps"></a>다음 단계
원격 데스크톱을 사용 하 여 계속 연결할 수 없는 경우 참조 hello [RDP 문제 해결 가이드](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. hello [자세한 문제 해결 가이드 RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 특정 단계를 사용 하지 않고 메서드 문제 해결을 살펴봅니다. 직접적인 도움을 위해 [Azure 지원 요청](https://azure.microsoft.com/support/options/)을 개설할 수도 있습니다.

