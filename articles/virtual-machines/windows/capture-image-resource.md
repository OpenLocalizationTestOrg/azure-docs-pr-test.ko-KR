---
title: "Azure에서 관리 되는 이미지 aaaCreate | Microsoft Docs"
description: "Azure에서 일반화된 VM 또는 VHD의 관리 이미지를 만듭니다. 이미지 toocreate 사용 되는 관리 되는 디스크를 사용 하는 여러 Vm 수 있습니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: cynthn
ms.openlocfilehash: d8cd6c2ce8c5d704de2c845abced85139944d682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-image-of-a-generalized-vm-in-azure"></a>Azure에서 일반화된 VM의 관리 이미지 만들기

저장소 계정에 관리 디스크 또는 비관리 디스크로 저장되는 일반화된 VM으로 관리 이미지 리소스를 만들 수 있습니다. 이미지 수를 hello 다음 toocreate 사용 되는 여러 Vm 수 있습니다. 


## <a name="generalize-hello-windows-vm-using-sysprep"></a>일반화 hello Sysprep를 사용 하 여 Windows VM

Sysprep는 특히, 모든 개인 계정 정보를 제거 하 고 이미지 형식으로 사용 되는 hello 컴퓨터 toobe를 준비 합니다. Sysprep에 대 한 세부 정보를 참조 하십시오. [어떻게 tooUse Sysprep: 소개](http://technet.microsoft.com/library/bb457073.aspx)합니다.

Hello 컴퓨터에서 실행 되는 hello 서버 역할과 Sysprep에서 사용할 수 있는지 확인 합니다. 자세한 내용은 [서버 역할에 대한 Sysprep 지원](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

> [!IMPORTANT]
> 를 사용 하 여 VHD tooAzure hello에 대 한 처음으로 업로드 하기 전에 Sysprep를 실행 하는 경우 했는지 확인 [VM 준비](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Sysprep를 실행 하기 전에. 
> 
> 

1. Windows 가상 컴퓨터 toohello에 로그인 합니다.
2. Hello 명령 프롬프트 창을 관리자 권한으로 엽니다. Hello 디렉터리도 변경**%windir%\system32\sysprep**, 한 다음 실행 `sysprep.exe`합니다.
3. Hello에 **시스템 준비 도구** 대화 상자에서 **입력 시스템을 기본 OOBE (Experience)**, 해당 hello 있는지 확인 하 고 **일반화** 확인란을 선택 합니다.
4. **종료 옵션**에서 **종료**를 선택합니다.
5. **확인**을 클릭합니다.
   
    ![Sysprep 시작](./media/upload-generalized-managed/sysprepgeneral.png)
6. Sysprep이 완료 된 hello 가상 컴퓨터를 종료 합니다. Hello VM을 다시 시작 하지 않습니다.


## <a name="create-a-managed-image-in-hello-portal"></a>Hello 포털에서 관리 되는 이미지 만들기 

1. 열기 hello [포털](https://portal.azure.com)합니다.
2. 클릭 하 여 새 리소스를 더하기 기호 toocreate hello 합니다.
3. Hello 필터 검색 입력 **이미지**합니다.
4. 선택 **이미지** hello 결과에서 합니다.
5. Hello에 **이미지** 블레이드에서 클릭 **만들기**합니다.
6. **이름**를 hello 이미지에 대 한 이름을 입력 합니다.
7. 선택 hello hello에서 올바른 이름이 둘 이상의 구독이 있으면 **구독** 드롭 다운 합니다.
7. **리소스 그룹** 선택 하거나 **새로 만들기** 이름을 입력 하거나 선택 하 고 **기존 계획에서** 리소스 그룹 toouse hello 드롭 다운 목록에서 선택 합니다.
8. **위치**, 리소스 그룹의 hello 위치를 선택 합니다.
9. **OS 유형이** hello 유형의 Windows 또는 Linux 운영 체제를 선택 합니다.
11. **저장소 blob**, 클릭 **찾아보기** toolook Azure 저장소에 VHD hello에 대 한 합니다.
12. **계정 유형**에서 Standard_LRS 또는 Premium_LRS를 선택합니다. 표준은 하드 디스크 드라이브를 사용하고 프리미엄은 반도체 드라이브를 사용합니다. 둘 다 로컬 중복 저장소를 사용합니다.
13. **디스크 캐싱** 선택 hello 적합 한 디스크 캐싱 옵션입니다. hello 옵션은 **None**, **읽기 전용** 및 **읽기/쓰기**합니다.
14. 선택 사항: 추가할 수 있습니다도 기존 데이터 디스크 toohello 이미지를 클릭 하 여 **+ 추가 데이터 디스크**합니다.  
15. 선택을 마치면 **만들기**를 클릭합니다.
16. Hello 이미지를 만든 후 나타납니다로 **이미지** hello 선택한 hello 리소스 그룹의 리소스 목록에는 리소스입니다.



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a>Powershell을 사용하여 VM 관리 이미지 만들기

VM hello 이미지를 사용 하면 hello에서 직접 이미지를 만들기 hello hello OS 디스크 및 데이터 디스크를 포함 하 여 VM과 연결 된 hello 디스크를 모두 포함 됩니다.


시작 하기 전에 hello hello AzureRM.Compute PowerShell 모듈의 최신 버전이 있는지 확인 합니다. 실행 명령 tooinstall 다음 hello 합니다.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
자세한 내용은 [Azure PowerShell 버전 관리](/powershell/azure/overview)를 참조하세요.


1. 일부 변수를 만듭니다.

    ```powershell
    $vmName = "myVM"
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $imageName = "myImage"
    ```
2. VM 할당 취소 되어 있는지 hello를 확인 합니다.

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. Hello 가상 컴퓨터의 hello 상태를 너무 설정**일반화 됨으로**합니다. 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. Hello 가상 컴퓨터를 가져옵니다. 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. Hello 이미지 구성을 만듭니다.

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. Hello 이미지를 만듭니다.

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a>PowerShell에서 VHD 관리 이미지 만들기

일반화된 OS VHD를 사용하여 관리 이미지를 만듭니다.


1.  먼저, hello 공통 매개 변수를 설정 합니다.

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. Step\deallocate hello VM입니다.

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. Hello 일반화 된 것과 같이 VM을 표시 합니다.

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  일반화 된 운영 체제 VHD를 사용 하 여 hello 이미지를 만듭니다.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a>Powershell을 사용하여 스냅숏으로 관리 이미지 만들기

Hello 일반화 된 VM에서 VHD의 스냅샷을에서 관리 되는 이미지를 만들 수도 있습니다.

    
1. 일부 변수를 만듭니다. 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. Hello 스냅숏을 가져옵니다.

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. Hello 이미지 구성을 만듭니다.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. Hello 이미지를 만듭니다.

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a>다음 단계
- 이제 [일반화 hello 관리 되는 이미지에서 VM을 만들](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.    

