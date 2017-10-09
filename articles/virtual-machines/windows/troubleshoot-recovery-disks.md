---
title: "windows Azure PowerShell을 사용 하 여 VM을 문제 해결 aaaUse | Microsoft Docs"
description: "Windows VM tootroubleshoot Azure의 hello OS 디스크 tooa 복구 Azure PowerShell을 사용 하 여 VM을 연결 하 여 발급 하는 방법을 알아봅니다"
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
ms.openlocfilehash: 7a6a76f64824fe5d06dc4286cb1d87ab8bb794e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-azure-powershell"></a>Windows VM hello OS 디스크 tooa 복구 Azure PowerShell을 사용 하 여 VM을 연결 하 여 문제 해결
Azure에서 Windows 가상 컴퓨터 (VM) 부팅 또는 디스크 오류가 발생 하는 경우 문제 해결 단계는 자체 hello 가상 하드 디스크에서 tooperform을 할 수 있습니다. 일반적인 예로 hello VM 수 tooboot 성공적으로 않도록 방지 하는 실패 한 응용 프로그램 업데이트는 것입니다. 이 세부 정보를 어떻게 문서 toouse Azure PowerShell tooconnect에 가상 하드 디스크 tooanother Windows VM toofix 오류를 다시 만들어야 원래 VM입니다.


## <a name="recovery-process-overview"></a>복구 프로세스 개요
hello 문제 해결 과정은 다음과 같습니다.

1. Hello VM 발생 문제, 유지 hello 가상 하드 디스크를 삭제 합니다.
2. 첨부 하 고 문제 해결을 위해 hello 가상 하드 디스크 tooanother Windows VM에 탑재 합니다.
3. Toohello VM 문제 해결을 연결 합니다. 파일을 편집 하거나 hello 원래 가상 하드 디스크에서 다양 한 도구 toofix 문제를 실행 합니다.
4. 탑재 해제 하 고 VM의 문제를 해결 하는 hello에서 hello 가상 하드 디스크를 분리 합니다.
5. Hello 원래 가상 하드 디스크를 사용 하는 VM을 만듭니다.

확인 했는지 [최신 Azure PowerShell hello](/powershell/azure/overview) 설치 하 고 tooyour 구독에 기록:

```powershell
Login-AzureRMAccount
```

Hello 다음 예에서는 매개 변수 이름은 고유한 값으로 대체 합니다. 예제 매개 변수 이름에 `myResourceGroup`, `mystorageaccount` 및 `myVM`이 포함됩니다.


## <a name="determine-boot-issues"></a>부팅 문제 확인
Azure에서 VM의 스크린샷을 볼 수 있습니다 toohelp 부팅 문제를 해결 합니다. 이 스크린 샷 VM tooboot 실패 이유를 파악 하는 데 도움이 됩니다. hello 다음 예제에서는 가져옵니다 hello 스크린 샷 hello 라는 Windows VM에서에서 `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`:

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup `
    -Name myVM -Windows -LocalPath C:\Users\ops\
```

Hello 스크린 샷 toodetermine hello VM tooboot를 실패 한 이유를 검토 합니다. 제공된 특정 오류 메시지 또는 오류 코드를 기록해 둡니다.


## <a name="view-existing-virtual-hard-disk-details"></a>기존 가상 하드 디스크 세부 정보 보기
가상 하드 디스크 tooanother VM에 연결할 수 있습니다, 전에 hello 가상 하드 디스크 (VHD)의 tooidentify hello 이름이 필요 합니다.

hello 다음 예제에서는 가져옵니다 hello 라는 VM에 대 한 정보 `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`:

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

검색할 `Vhd URI` hello 내 `StorageProfile` hello 출력에서 hello 명령 앞의 섹션입니다. hello 다음 잘린된 예제는 출력 hello `Vhd URI` hello 코드 블록의 hello 끝 쪽으로:

```powershell
RequestId                     : 8a134642-2f01-4e08-bb12-d89b5b81a0a0
StatusCode                    : OK
ResourceGroupName             : myResourceGroup
Id                            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM
Name                          : myVM
Type                          : Microsoft.Compute/virtualMachines
...
StorageProfile                :
  ImageReference              :
    Publisher                 : MicrosoftWindowsServer
    Offer                     : WindowsServer
    Sku                       : 2016-Datacenter
    Version                   : latest
  OsDisk                      :
    OsType                    : Windows
    Name                      : myVM
    Vhd                       :
      Uri                     : https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    Caching                   : ReadWrite
    CreateOption              : FromImage
```


## <a name="delete-existing-vm"></a>기존 VM 삭제
가상 하드 디스크와 VM은 Azure의 두 가지 별개의 리소스입니다. 가상 하드 디스크는 자체 hello 운영 체제, 응용 프로그램 및 구성 저장 됩니다. hello VM 자체 hello 크기 또는 위치를 정의 하 고 가상 하드 디스크 또는 가상 네트워크 인터페이스 카드 (NIC) 등의 리소스를 참조 하는 메타 데이터 일 뿐입니다. 각 가상 하드 디스크에 연결 되어 있을 때 할당 한 임 대권을 tooa VM입니다. 데이터 디스크를 연결 하 고 hello VM에서 실행 중인 동안에 분리 수, 있지만 hello VM 리소스는 삭제 하지 않는 한 hello OS 디스크를 분리할 수 없습니다. hello 임대는 해당 VM 중지 및 할당 취소 된 상태에 있을 경우에 tooassociate hello OS 디스크는 VM으로 계속 됩니다.

첫 번째 단계 toorecover hello VM은 자체 toodelete hello VM 리소스입니다. VM 삭제 hello 저장소 계정의 hello 가상 하드 디스크를 유지합니다. VM을 삭제 하는 hello, 후 hello 가상 하드 디스크 tooanother VM tootroubleshoot 첨부 고 hello 오류를 해결 합니다.

다음 예에서는 삭제 하는 hello hello 라는 VM `myVM` 이라는 hello 리소스 그룹에서 `myResourceGroup`:

```powershell
Remove-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

Hello VM가 hello 가상 하드 디스크 tooanother VM을 연결 하기 전에 삭제를 마치기 때까지 기다립니다. hello 임대 VM hello로 연결 하는 hello 가상 하드 디스크에 toobe hello 가상 하드 디스크 tooanother VM을 연결 하기 전에 해제 해야 합니다.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>기존 가상 하드 디스크 tooanother VM 연결
에 대 한 hello 다음 몇 단계 문제 해결을 위해 다른 VM을 사용 합니다. Hello 기존 가상 하드 디스크 toothis VM toobrowse 문제 해결을 첨부 하 고이 정보를 hello 디스크의 콘텐츠를 편집 합니다. 이 프로세스 toocorrect를 통해 모든 구성 오류 또는 추가 응용 프로그램을 확인 또는 로그 파일, 예를 들어 시스템. 선택 하거나 문제 해결을 위해 다른 VM toouse 만듭니다.

Hello 기존 가상 하드 디스크를 연결할 경우 hello 앞에서 만든 hello URL toohello 디스크 지정 `Get-AzureRmVM` 명령입니다. hello 다음 예제에서는 연결 가상 컴퓨터 V 문제를 해결 하는 기존 가상 하드 디스크 toohello `myVMRecovery` 이라는 hello 리소스 그룹에 `myResourceGroup`:

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
Add-AzureRmVMDataDisk -VM $myVM -CreateOption "Attach" -Name "DataDisk" -DiskSizeInGB $null `
    -VhdUri "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

> [!NOTE]
> 디스크 추가 hello 디스크의 toospecify hello 크기가 필요 합니다. 기존 디스크를 연결 했습니다 hello `-DiskSizeInGB` 로 지정 된 `$null`합니다. 이 값을 입력 하면 hello 데이터 디스크가 올바르게 연결 되었는지, 및 hello 하지 않고 필요한 toodetermine hello 데이터 디스크의 실제 크기입니다.


## <a name="mount-hello-attached-data-disk"></a>Hello 연결 된 데이터 디스크를 탑재

1. RDP tooyour hello 적절 한 자격 증명을 사용 하 여 VM의 문제를 해결 합니다. hello 다음 예제에서는 다운로드 hello 라는 VM에 대 한 RDP 연결 파일 hello `myVMRecovery` 이라는 hello 리소스 그룹에 `myResourceGroup`, 너무 다운로드`C:\Users\ops\Documents`"

    ```powershell
    Get-AzureRMRemoteDesktopFile -ResourceGroupName "myResourceGroup" -Name "myVMRecovery" `
        -LocalPath "C:\Users\ops\Documents\myVMRecovery.rdp"
    ```

2. hello 데이터 디스크가 자동으로 감지 되 고 연결 합니다. 다음과 같이 hello 목록은 연결 된 볼륨이 toodetermine hello 드라이브 문자를 보려면:

    ```powershell
    Get-Disk
    ```

    다음 예제 출력 hello hello 가상 하드 디스크는 디스크를 연결 표시 **2**합니다. (사용할 수 있습니다 `Get-Volume` tooview hello 드라이브 문자):

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Online       127 GB MBR
    ```

## <a name="fix-issues-on-original-virtual-hard-disk"></a>원래 가상 하드 디스크의 문제 해결
이제 hello 기존 가상 하드 디스크를 탑재, 모든 유지 관리 및 문제 해결 단계는 필요에 따라 수행할 수 있습니다. Hello 문제를 해결 한 후 단계를 수행 하는 hello로 계속 합니다.


## <a name="unmount-and-detach-original-virtual-hard-disk"></a>원래 가상 하드 디스크의 탑재 해제 및 분리
프로그램 오류가 해결 되 면 분리 하 고 문제 해결 VM에서 hello 기존 가상 하드 디스크를 분리 합니다. VM의 문제를 해결 하는 hello 가상 하드 디스크 toohello 연결 hello 임대가 해제 될 때까지 다른 VM과 가상 하드 디스크를 사용할 수 없습니다.

1. RDP 세션에서 복구 VM에 hello 데이터 디스크를 분리 하십시오. 이전 hello에서 hello 디스크 번호를 필요한 `Get-Disk` cmdlet. 다음을 사용 하 여 `Set-Disk` 오프 라인으로 tooset hello 디스크:

    ```powershell
    Set-Disk -Number 2 -IsOffline $True
    ```

    이제 hello 디스크 사용 하 여 오프 라인으로 설정 확인 `Get-Disk` 다시 합니다. hello 다음 예제 출력과 hello 디스크 이제 오프 라인으로 설정:

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Offline      127 GB MBR
    ```

2. RDP 세션을 종료합니다. Azure PowerShell 세션에서 VM의 문제를 해결 하는 hello에서 hello 가상 하드 디스크를 제거 합니다.

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
    Remove-AzureRmVMDataDisk -VM $myVM -Name "DataDisk"
    Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
    ```


## <a name="create-vm-from-original-hard-disk"></a>원래 하드 디스크에서 VM 만들기
원래 가상 하드 디스크에서 VM에서 사용할 toocreate [이 Azure 리소스 관리자 템플릿을](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet)합니다. 실제 JSON 템플릿 hello 링크 hello에 됩니다.

- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json

hello에서 VHD URL hello를 사용 하 여 기존 가상 네트워크를으로 VM을 배포 하는 hello 템플릿 이전 명령입니다. hello 다음 예제에서는 배포 이라는 hello 템플릿 toohello 리소스 그룹 `myResourceGroup`:

```powershell
New-AzureRmResourceGroupDeployment -Name myDeployment -ResourceGroupName myResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json
```

VM 이름, 운영 체제 유형 및 v M 크기와 같은 hello 서식 파일에 대 한 응답 hello 메시지 표시합니다. hello `osDiskVhdUri` hello 기존 가상 하드 디스크 toohello VM 문제 해결을 연결할 때 이전에 사용 되는 동일한 hello 됩니다.


## <a name="re-enable-boot-diagnostics"></a>부트 진단 다시 사용

Hello 기존 가상 하드 디스크에서 VM을 만들 때 부트 진단이 자동으로 사용할 수 없습니다. hello 다음 예에서는 가상 컴퓨터 V hello에 진단 확장 hello `myVMDeployed` 이라는 hello 리소스 그룹에 `myResourceGroup`:

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMDeployed"
Set-AzureRmVMBootDiagnostics -ResourceGroupName myResourceGroup -VM $myVM -enable
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

## <a name="next-steps"></a>다음 단계
Tooyour VM을 연결 하는 데 문제가 있는 경우 참조 [문제를 해결 하는 RDP 연결 tooan Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. VM에서 실행 중인 응용 프로그램에 액세스하는 데 문제가 있는 경우 [Windows VM에서 응용 프로그램 연결 문제 해결](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.

Resource Manager를 사용하는 방법에 대한 자세한 내용은 [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.
