---
title: "일반화 된 온-프레미스 VHD에서 관리 되는 Azure VM aaaCreate | Microsoft Docs"
description: "일반화 된 VHD tooAzure 업로드 하 고 toocreate 사용 hello 리소스 관리자 배포 모델에서 새 Vm입니다."
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
ms.date: 05/19/2017
ms.author: cynthn
ms.openlocfilehash: 2fd0c0eec922e6ca8af4e712c1bceb1f9466105c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-and-use-it-toocreate-new-vms-in-azure"></a>일반화 된 VHD를 업로드 하 고 toocreate를 사용 하 여 Azure에서 새 Vm

이 항목에서는 PowerShell tooupload를 사용 하 여 일반화 된 VM tooAzure의 VHD, hello VHD에서에서 이미지 만들기 및 해당 이미지에서 새 VM을 만듭니다. 다른 클라우드 또는 온-프레미스 가상화 도구에서 내보낸 VHD를 업로드할 수 있습니다. 사용 하 여 [관리 하는 디스크](managed-disks-overview.md) hello에 대 한 새 VM hello VM 관리를 단순화 하 고 hello VM은 가용성 집합에 배치 하는 경우 더 나은 가용성을 제공 합니다. 

샘플 스크립트 toouse 참조 [스크립트 tooupload VHD tooAzure 샘플링 및 새 VM 만들기](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)

## <a name="before-you-begin"></a>시작하기 전에

- 모든 VHD tooAzure를 업로드 하기 전에 따라야 [Windows VHD 또는 VHDX tooupload tooAzure 준비](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
- 검토 [hello 마이그레이션 계획 tooManaged 디스크](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) 너무 마이그레이션을 시작 하기 전에[관리 하는 디스크](managed-disks-overview.md)합니다.
- Hello hello AzureRM.Compute PowerShell 모듈의 최신 버전이 있는지 확인 합니다. 실행 명령 tooinstall 다음 hello 합니다.

    ```powershell
    Install-Module AzureRM.Compute -RequiredVersion 2.6.0
    ```
    자세한 내용은 [Azure PowerShell 버전 관리](/powershell/azure/overview)를 참조하세요.


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



## <a name="log-in-tooazure"></a>TooAzure 로그인
PowerShell 버전 1.4가 없는 이상 읽기 설치 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

1. Azure PowerShell을 열고 tooyour Azure 계정에에서 로그인 합니다. Azure 계정 자격을 증명 tooenter 있습니다에 대 한 팝업 창이 열립니다.
   
    ```powershell
    Login-AzureRmAccount
    ```
2. 사용 가능한 구독에 대 한 hello 구독을 Id를 가져옵니다.
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. Hello 구독 id입니다.를 사용 하 여 hello 올바른 구독 설정 대체  *<subscriptionID>*  hello hello ID로 구독을 수정 합니다.
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="get-hello-storage-account"></a>Hello 저장소 계정 가져오기
Azure toostore 업로드 hello VM 이미지에 저장소 계정이 필요합니다. 기존 저장소 계정을 사용하거나 새 계정을 만들 수 있습니다. 

사용 하려는 hello VHD toocreate 관리 디스크 vm의 경우, hello 저장소 계정 위치 hello VM 만들어야 하는 동일한 hello 위치를 이어야 합니다.

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

    리소스 그룹 이름이 toocreate **myResourceGroup** hello에 **미국 동부** 지역, 유형:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "East US"
    ```

2. 라는 저장소 계정 만들기 **mystorageaccount** hello를 사용 하 여이 리소스 그룹에 [새로 AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "East US"`
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
    -SkuName에 대한 유효한 값은 다음과 같습니다.
   
   * **Standard_LRS** - 로컬 중복 저장소 
   * **Standard_ZRS** - 영역 중복 저장소
   * **Standard_GRS** - 지역 중복 저장소 
   * **Standard_RAGRS** - 읽기 액세스 지역 중복 저장소 
   * **Premium_LRS** - 프리미엄 로컬 중복 저장소 

## <a name="upload-hello-vhd-tooyour-storage-account"></a>Hello VHD tooyour 저장소 계정에 업로드

사용 하 여 hello [추가 AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) 저장소 계정의 cmdlet tooupload hello VHD tooa 컨테이너입니다. 이 예에서는 업로드 파일 hello *myVHD.vhd* 에서 *"C:\Users\Public\Documents\Virtual 하드 디스크\"*  tooa 저장소 계정인 *mystorageaccount*hello에 *myResourceGroup* 리소스 그룹입니다. hello 파일 라는 hello 컨테이너에 배치 됨 *mycontainer* hello 새 파일 이름이 됩니다 *myUploadedVHD.vhd*합니다.

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

이 명령은 네트워크 연결 및 VHD 파일의 hello 크기에 따라 시간이 걸릴 수 있습니다 toocomplete

Hello 저장 **대상 URI** 경로 toouse hello를 사용 하 여 새 VM에 VHD 업로드 또는 관리 되는 디스크 toocreate 하려는 경우 이후입니다.

### <a name="other-options-for-uploading-a-vhd"></a>VHD를 업로드하기 위한 기타 옵션
 
 
Hello 다음 중 하나를 사용 하 여 VHD tooyour 저장소 계정을 업로드할 수 있습니다.

- [AZCopy](http://aka.ms/downloadazcopy)
- [Azure 저장소 Blob 복사 API](https://msdn.microsoft.com/library/azure/dd894037.aspx)
- [Azure Storage 탐색기 Blob 업로드](https://azurestorageexplorer.codeplex.com/)
- [저장소 가져오기/내보내기 서비스 REST API 참조](https://msdn.microsoft.com/library/dn529096.aspx)
-   예상 업로드 시간이 7일보다 긴 경우 가져오기/내보내기 서비스를 사용하는 것이 좋습니다. 사용할 수 있습니다 [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) 데이터 크기와 전송 단위에서 tooestimate hello 시간입니다. 
    가져오기/내보내기 수 toocopy tooa 표준 저장소 계정을 사용 합니다. AzCopy와 같은 도구를 사용 하 여 표준 저장소 toopremium 저장소 계정에서 toocopy가 필요 합니다.


## <a name="create-a-managed-image-from-hello-uploaded-vhd"></a>관리 되는 만들기 hello에서 이미지에 VHD 업로드 

일반화된 OS VHD를 사용하여 관리 이미지를 만듭니다. 사용자의 정보로 hello 값을 대체 합니다.


1.  먼저, hello 공통 매개 변수를 설정 합니다.

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    $vmSize = "Standard_DS1_v2"
    $location = "East US" 
    $imageName = "yourImageName"
    ```

4.  일반화 된 운영 체제 VHD를 사용 하 여 hello 이미지를 만듭니다.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $urlOfUploadedImageVhd
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```

## <a name="create-a-virtual-network"></a>가상 네트워크 만들기
Hello vNet 및 hello의 서브넷을 만들 [가상 네트워크](../../virtual-network/virtual-networks-overview.md)합니다.

1. Hello 서브넷을 만듭니다. 이 예에서는 이라는 서브넷을 만듭니다 *mySubnet* hello 주소 접두사와 *10.0.0.0/24*합니다.  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Hello 가상 네트워크를 만듭니다. 이 예제에서는 명명 된 가상 네트워크를 만들어 *myVnet* hello 주소 접두사와 *10.0.0.0/16*합니다.  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a>공용 IP 주소 및 네트워크 인터페이스 만들기

필요한 tooenable hello 가상 네트워크의 hello 가상 컴퓨터와의 통신을는 [공용 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) 및 네트워크 인터페이스.

1. 공용 IP 주소 만들기. 이 예에서는 *myPip*라는 공용 IP 주소를 만듭니다. 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. Hello NIC. 만들기 이 예에서는 **myNic**라는 NIC를 만듭니다. 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Hello 네트워크 보안 그룹 및 RDP 규칙 만들기

toobe 수 toolog tooyour에서 RDP를 사용 하 여 VM을 toohave RDP 포트 3389에 대 한 액세스를 허용 하는 네트워크 보안 규칙 (NSG) 필요 합니다. 

이 예에서는 포트 3389를 통한 RDP 트래픽을 허용하는 *myRdpRule*이라는 규칙을 포함하는 *myNsg*로 명명된 NSG를 만듭니다. Nsg에 대 한 자세한 내용은 참조 [PowerShell을 사용 하 여 Azure에서 VM 포트 tooa 여](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-hello-virtual-network"></a>Hello 가상 네트워크에 대 한 변수 만들기

가상 네트워크를 완료 하는 hello에 대 한 변수를 만듭니다. 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a>Hello VM에 대 한 hello 자격 증명 가져오기

hello 다음 cmdlet이 열립니다 입력할 수 있는 새 사용자 이름 및 암호 toouse hello 로컬 관리자 계정으로 원격으로 hello VM에 액세스 하기 위한 창. 

```powershell
$cred = Get-Credential
```

## <a name="add-hello-vm-name-and-size-toohello-vm-configuration"></a>Hello VM 이름 및 크기 toohello VM 구성에 추가 합니다.

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a>Hello에 대 한 원본 이미지로 집합 hello VM 이미지 새 VM

관리 되는 hello VM 이미지의 hello ID를 사용 하 여 hello 소스 이미지를 설정 합니다.

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a>운영 체제 구성 hello를 설정 하 고 hello NIC. 추가

Hello 저장소 유형 (PremiumLRS 또는 StandardLRS)와 hello OS 디스크의 hello 크기를 입력 합니다. 이 예에서는 설정 hello 계정 유형 너무*PremiumLRS*, 디스크 크기를 너무 hello*128GB* 및 디스크 캐싱에 너무*ReadWrite*합니다.

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a>Hello VM 만들기

Hello hello에 저장 된 hello 구성을 사용 하 여 새 VM 만들기 **$vm** 변수입니다.

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a>VM이 생성 되었고 해당 hello를 확인 합니다.
새로 만든 VM의 hello hello 나타나야 완료 되 면 [Azure 포털](https://portal.azure.com) 아래 **찾아보기** > **가상 컴퓨터**, 또는 hello 다음을 사용 하 여 PowerShell 명령:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>다음 단계

tooyour 새 가상 컴퓨터, hello에 찾아보기 toohello VM에에서 toosign [포털](https://portal.azure.com), 클릭 **연결**, 및 열기 hello RDP 원격 데스크톱 파일입니다. Tooyour 새 가상 컴퓨터에 프로그램 원래 가상 컴퓨터 toosign의 hello 계정 자격 증명을 사용 합니다. 자세한 내용은 참조 [어떻게 tooconnect 로그온 tooan Azure 가상 컴퓨터 및 Windows를 실행](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. 

