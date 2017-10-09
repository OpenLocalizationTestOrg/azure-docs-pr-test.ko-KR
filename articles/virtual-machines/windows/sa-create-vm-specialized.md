---
title: "Azure에서 특수 한 디스크에서 VM aaaCreate | Microsoft Docs"
description: "Hello 리소스 관리자 배포 모델에서 관리 되지 않는 특수 한 디스크를 연결 하 여 새 VM을 만듭니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3b7d3cd5-e3d7-4041-a2a7-0290447458ea
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: c88f213b6629a6c1d6ff5845e76c2f7719672714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-specialized-vhd-in-a-storage-account"></a>저장소 계정의 특수한 VHD에서 VM 만들기

Powershell을 사용 하 여 hello 운영 체제 디스크와 관리 되지 않는 특수 한 디스크를 연결 하 여 새 VM을 만듭니다. 특수 한 디스크는 hello 사용자 계정, 응용 프로그램 및 원래 VM에서 다른 상태 데이터를 유지 하는 기존 VM에서 VHD의 복사본입니다. 

다음 두 가지 옵션을 사용할 수 있습니다.
* [VHD 업로드](create-vm-specialized.md#option-1-upload-a-specialized-vhd)
* [Hello 기존 Azure VM의 VHD를 복사 합니다.](create-vm-specialized.md#option-2-copy-an-existing-azure-vm)

## <a name="before-you-begin"></a>시작하기 전에
PowerShell을 사용 하는 경우 hello hello AzureRM.Compute PowerShell 모듈의 최신 버전이 있는지 확인 합니다. 실행 명령 tooinstall 다음 hello 합니다.

```powershell
Install-Module AzureRM.Compute 
```
자세한 내용은 [Azure PowerShell 버전 관리](/powershell/azure/overview)를 참조하세요.


## <a name="option-1-upload-a-specialized-vhd"></a>옵션 1: 특수한 VHD 업로드

Hello 하이퍼-V 또는 VM 사설 클라우드에서 다른 클라우드에서 내보낼 처럼 온-프레미스 가상화 도구를 사용 하 여 만든 특수 한 VM에서 VHD를 업로드할 수 있습니다.

### <a name="prepare-hello-vm"></a>Hello VM 준비
온-프레미스 VM을 사용하여 만든 특수한 VHD 또는 다른 클라우드에서 내보낸 VHD를 업로드할 수 있습니다. 특수화 된 VHD hello 사용자 계정, 응용 프로그램 및 원래 VM에서 다른 상태 데이터를 유지 관리합니다. Toouse를 가져오려는 경우 VHD로 hello-toocreate 새 VM은 hello 다음 단계를 완료 합니다. 
  
  * [Windows VHD tooupload tooAzure 준비](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. **없는** 일반화 Sysprep를 사용 하 여 VM hello 합니다.
  * 모든 게스트 가상화 도구와 hello (즉, VMware 도구)를 VM에 설치 된 에이전트를 제거 합니다.
  * Hello VM 확인 해당 IP 주소 및 DNS 설정이 DHCP 통해 구성 된 toopull 됩니다. 이렇게 하면 해당 hello 서버를 시작할 때 hello VNet 내에서 IP 주소를 가져옵니다. 


### <a name="get-hello-storage-account"></a>Hello 저장소 계정 가져오기
Azure toostore 업로드 hello VM 이미지에 저장소 계정이 필요합니다. 기존 저장소 계정을 사용하거나 새 계정을 만들 수 있습니다. 

tooshow hello 사용 가능한 저장소 계정을 입력 합니다.

```powershell
Get-AzureRmStorageAccount
```

Toouse 기존 저장소 계정을 사용할 경우 진행 toohello [hello VM 이미지 업로드](#upload-the-vm-vhd-to-your-storage-account) 섹션.

저장소 계정 toocreate 해야 할 경우 다음이 단계를 따르십시오.

1. Hello 저장소 계정을 만들어야 하는 hello 리소스 그룹의 hello 이름이 필요 합니다. 구독을 형식에 있는 모든 hello 리소스 그룹 아웃 toofind:
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    리소스 그룹 이름이 toocreate **myResourceGroup** hello에 **미국 서 부** 지역, 유형:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. 라는 저장소 계정 만들기 **mystorageaccount** hello를 사용 하 여이 리소스 그룹에 [새로 AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
### <a name="upload-hello-vhd-tooyour-storage-account"></a>Hello VHD tooyour 저장소 계정에 업로드
사용 하 여 hello [추가 AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) 저장소 계정의 cmdlet tooupload hello 이미지 tooa 컨테이너입니다. 이 예에서는 업로드 파일 hello **myVHD.vhd** 에서 `"C:\Users\Public\Documents\Virtual hard disks\"` tooa 저장소 계정인 **mystorageaccount** hello에 **myResourceGroup** 리소스 그룹입니다. hello 파일 라는 hello 컨테이너에 배치 됨 **mycontainer** hello 새 파일 이름이 됩니다 **myUploadedVHD.vhd**합니다.

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


성공 하면 다음과 비슷한 toothis 응답 가져오기:

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

이 명령은 네트워크 연결 및 VHD 파일의 hello 크기에 따라 시간이 걸릴 수 있습니다 toocomplete 합니다.


## <a name="option-2-copy-hello-vhd-from-an-existing-azure-vm"></a>옵션 2: 기존 Azure VM에서 hello VHD를 복사 합니다.

새, 중복 된 VM을 만들 때 VHD tooanother 저장소 계정 toouse를 복사할 수 있습니다.

### <a name="before-you-begin"></a>시작하기 전에
다음 사항을 확인합니다.

* Hello에 대 한 정보가 **원본 및 대상 저장소 계정**합니다. Hello 원본 VM toohave hello 저장소 계정 및 컨테이너 이름이 필요합니다. Hello 컨테이너 이름이 됩니다 일반적으로 **vhd**합니다. 대상 저장소 계정 toohave를 해야합니다. 아직 없는 하나, 각 hello 포털을 사용 하 여 하나를 만들 수 있습니다 (**더 서비스** > 저장소 계정 > 추가) 또는 hello를 사용 하 여 [새로 AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet. 
* 다운로드 하 고 hello 설치한 [AzCopy tool](../../storage/common/storage-use-azcopy.md)합니다. 

### <a name="deallocate-hello-vm"></a>Hello VM 할당 취소
Hello 복사 hello VHD toobe 확보 하는 VM 할당이 취소 되었습니다. 

* **포털**: **가상 컴퓨터** > **myVM** > 중지를 클릭합니다.
* **Powershell**: 사용 [중지 AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) toostop (할당 취소) 가상 컴퓨터 V hello **myVM** 리소스 그룹에 **myResourceGroup**합니다.

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

hello **상태** hello Azure에에서 VM hello에 대 한 포털에서 변경 **Stopped** 너무**중지 됨 (할당 취소 됨)**합니다.

### <a name="get-hello-storage-account-urls"></a>Hello 저장소 계정 Url 가져오기
Hello Url의 hello 원본 및 대상 저장소 계정이 필요합니다. hello Url 같이: `https://<storageaccount>.blob.core.windows.net/<containerName>/`합니다. Hello 저장소 계정 및 컨테이너 이름을 알고 있는 경우 hello 대괄호 toocreate 간에 hello 정보를 URL만 바꿀 수 있습니다. 

Hello Azure 포털 또는 Azure Powershell tooget hello URL을 사용할 수 있습니다.

* **포털**: hello 클릭  **>**  에 대 한 **더 많은 서비스** > **저장소 계정은**  >   *저장소 계정* > **Blob** 원본 VHD 파일 hello 되었 및 **vhd** 컨테이너입니다. 클릭 **속성** hello 컨테이너 및 hello 텍스트 레이블이 지정 된 복사에 대 한 **URL**합니다. 원본과 대상 모두 hello 컨테이너의 hello Url 필요 합니다. 
* **Powershell**: 사용 [Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) 이라는 VM에 대 한 tooget hello 정보 **myVM** hello 리소스 그룹에 **myResourceGroup**합니다. Hello 찾는 위치 hello 결과에 **저장소 프로필** hello에 대 한 섹션 **Vhd Uri**합니다. hello Uri의 첫 번째 부분 hello hello URL toohello 컨테이너 고 hello 마지막 부분은 hello hello VM에 대 한 운영 체제 VHD 이름입니다.

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
``` 

## <a name="get-hello-storage-access-keys"></a>Hello 저장소 액세스 키 가져오기
원본 및 대상 저장소 계정이 hello에 대 한 hello 선택 키를 찾습니다. 액세스 키에 대한 자세한 내용은 [Azure 저장소 계정 방법](../../storage/common/storage-create-storage-account.md)을 참조하세요.

* **포털**: **추가 서비스** > **저장소 계정** > *저장소 계정* > **액세스 키**를 클릭합니다. 로 표시 된 hello 키 복사 **key1**합니다.
* **Powershell**: 사용 [Get AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) tooget hello 저장소 계정에 대 한 저장소 키를 hello **mystorageaccount** hello 리소스 그룹에  **myResourceGroup**합니다. 레이블이 지정 된 hello 키 복사 **key1**합니다.

```powershell
Get-AzureRmStorageAccountKey -Name mystorageaccount -ResourceGroupName myResourceGroup
```

### <a name="copy-hello-vhd"></a>Hello VHD 복사
AzCopy를 사용하여 저장소 계정 간에 파일을 복사할 수 있습니다. Hello 대상 컨테이너에 대 한 지정 된 컨테이너 hello 존재 하지 않으면 자동으로 만들어집니다 드립니다. 

toouse AzCopy 로컬 컴퓨터에서 명령 프롬프트를 열고 AzCopy를 설치한 toohello 폴더를 이동 합니다. 너무 비슷한 됩니다*C:\Program Files (x86) \Microsoft SDKs\Azure\AzCopy*합니다. 

hello를 사용 하면 toocopy hello의 모든 컨테이너 내에서 파일을 **/S** 전환 합니다. 이 사용 되는 toocopy hello OS VHD 수와 동일한 컨테이너 hello 모든 hello 데이터 디스크에 있는 경우에 합니다. 이 예에서는 어떻게 hello 컨테이너의 모든 hello 파일 toocopy **mysourcecontainer** 저장소 계정에 **mysourcestorageaccount** toohello 컨테이너 **mydestinationcontainer**  hello에 **mydestinationstorageaccount** 저장소 계정입니다. 사용자의 정보로 hello hello 저장소 계정 이름 및 컨테이너를 대체 합니다. `<sourceStorageAccountKey1>` 및 `<destinationStorageAccountKey1>`을 사용자 고유 키로 바꿉니다.

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
    /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
    /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> /S
```

여러 파일 toocopy 컨테이너에서 특정 VHD만 하려는 경우 또한 hello /Pattern 스위치를 사용 하 여 hello 파일 이름을 지정할 수 있습니다. 이 예제에서는 라는 파일만 hello **myFileName.vhd** 복사 됩니다.

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
  /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
  /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> `
  /Pattern:myFileName.vhd
```


완료되면 다음과 유사한 메시지를 받게 됩니다.

```
Finished 2 of total 2 file(s).
[2016/10/07 17:37:41] Transfer summary:
-----------------
Total files transferred: 2
Transfer successfully:   2
Transfer skipped:        0
Transfer failed:         0
Elapsed time:            00.00:13:07
```

### <a name="troubleshooting"></a>문제 해결
* 를 사용 하면 AZCopy hello 오류가 나타나는 경우 "tooauthenticate hello 요청 하지 못했습니다 서버" 올바르게 hello 서명을 포함 하 여 hello hello 권한 부여 헤더 값의 형식이 설정 되어 있는지 확인 합니다. 키 2 또는 hello 보조 저장소 키를 사용 하는 경우 hello 주 또는 1 일 저장소 키를 사용해 보세요.

## <a name="create-hello-new-vm"></a>만들 새 VM hello 

Toocreate 네트워킹 및 hello에서 사용 하는 다른 VM 리소스 toobe 해야 새 VM입니다.

### <a name="create-hello-subnet-and-vnet"></a>Hello 서브넷 및 vNet 만들기

Hello vNet 및 hello의 서브넷을 만들 [가상 네트워크](../../virtual-network/virtual-networks-overview.md)합니다.

1. Hello 서브넷을 만듭니다. 이 예에서는 이라는 서브넷을 만듭니다 **mySubNet**, hello 리소스 그룹에 **myResourceGroup**, 집합 서브넷 주소 접두사를 너무 hello 및**10.0.0.0/24**합니다.
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubNet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Hello vNet을 만듭니다. 이 예제에서는 집합에 가상 네트워크 이름 toobe hello **myVnetName**, 위치를 너무 hello**미국 서 부**, hello 가상 네트워크에 대 한 주소 접두사를 너무 hello 및**10.0.0.0/16**합니다. 
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnetName"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-nic"></a>공용 IP 주소 및 NIC 만들기
필요한 tooenable hello 가상 네트워크의 hello 가상 컴퓨터와의 통신을는 [공용 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) 및 네트워크 인터페이스.

1. Hello 공용 IP를 만듭니다. 이 예제에서는 hello 공용 IP 주소 이름이 설정 되어 너무**myIP**합니다.
   
    ```powershell
    $ipName = "myIP"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. Hello NIC. 만들기 이 예제에서는 hello NIC 이름이 설정 되어 너무**myNicName**합니다.
   
    ```powershell
    $nicName = "myNicName"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Hello 네트워크 보안 그룹 및 RDP 규칙 만들기
toobe 수 toolog tooyour에서 RDP를 사용 하 여 VM을 toohave RDP 포트 3389에 대 한 액세스를 허용 하는 보안 규칙이 필요 합니다. 기존에서 새 VM을 만든 hello에 대 한 VHD hello 특수화 되므로 VM, 있습니다 hello VM 만들어진 후 hello 원본 가상 컴퓨터에 RDP를 사용 하 여 권한 toolog에서 기존 계정을 사용할 수 있습니다.
이 예제에서는 집합 hello NSG 이름을 너무**myNsg** 너무 hello RDP 규칙 이름 및**myRdpRule**합니다.

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

끝점 및 NSG 규칙에 대 한 자세한 내용은 참조 [PowerShell을 사용 하 여 Azure에서 VM 포트 tooa 여](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

### <a name="set-hello-vm-name-and-size"></a>Hello VM 이름 및 크기를 설정 합니다.

이 예제에서는 집합에 VM 이름 hello 너무 "myVM" 및 hello VM 크기가 너무 "Standard_A2"입니다.
```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a>Hello NIC를 추가 합니다.
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    
    
### <a name="configure-hello-os-disk"></a>Hello OS 디스크 구성

1. Hello 업로드 또는 복사 된 VHD에 대 한 hello URI를 설정 합니다. 이 예제에서는 명명 된 VHD 파일을 hello **myOsDisk.vhd** 라는 저장소 계정에 유지 되는 **myStorageAccount** 라는 컨테이너에 **myContainer**합니다.

    ```powershell
    $osDiskUri = "https://myStorageAccount.blob.core.windows.net/myContainer/myOsDisk.vhd"
    ```
2. Hello OS 디스크를 추가 합니다. 이 예제에서는 hello OS 디스크를 만들면 osDisk"hello 용어" appened toohello VM 이름 toocreate hello OS 디스크 이름입니다. 또한이 Windows 기반 VHD 연결된 toohello hello OS 디스크로 VM 되어야 함을 지정 합니다.
    
    ```powershell
    $osDiskName = $vmName + "osDisk"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption attach -Windows
    ```

선택 사항: 데이터 디스크가 있는 경우 해당 필요 toobe 연결 된 VM toohello hello 데이터 디스크를 사용 하 여 hello 데이터 Vhd의 Url 및 적절 한 논리 단위 번호 (Lun) hello를 추가 하세요.

```powershell
$dataDiskName = $vmName + "dataDisk"
$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -VhdUri $dataDiskUri -Lun 1 -CreateOption attach
```

저장소 계정을 사용할 경우, hello 데이터 및 운영 체제 디스크 Url이 다음과 같은: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`합니다. Hello 운영 체제 또는 데이터 복사 된 VHD 클릭 하면 toohello 대상 저장소 컨테이너를 찾아보고 다음 hello URL의 hello 내용을 복사 하 여 hello 포털에서 찾을 수 있습니다.


### <a name="complete-hello-vm"></a>전체 hello VM 

만들 방금 만든 hello 구성을 사용 하 여 VM hello 합니다.

```powershell
#Create hello new VM
New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

이 명령에 성공할 경우 다음과 유사한 출력이 표시됩니다.

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a>VM이 생성 되었고 해당 hello를 확인 합니다.
Hello 새로 만든 VM hello에 표시 되어야 [Azure 포털](https://portal.azure.com)아래 **찾아보기** > **가상 컴퓨터**, 또는 다음 PowerShell hello를 사용 하 여 명령:

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $rgName
$vmList.Name
```

## <a name="next-steps"></a>다음 단계
tooyour 새 가상 컴퓨터, hello에 찾아보기 toohello VM에에서 toosign [포털](https://portal.azure.com), 클릭 **연결**, 및 열기 hello RDP 원격 데스크톱 파일입니다. Tooyour 새 가상 컴퓨터에 프로그램 원래 가상 컴퓨터 toosign의 hello 계정 자격 증명을 사용 합니다. 자세한 내용은 참조 [어떻게 tooconnect 로그온 tooan Azure 가상 컴퓨터 및 Windows를 실행](connect-logon.md)합니다.

