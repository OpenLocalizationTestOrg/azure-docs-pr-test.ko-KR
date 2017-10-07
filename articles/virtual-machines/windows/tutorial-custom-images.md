---
title: "Azure PowerShell hello 사용 하 여 사용자 지정 VM 이미지를 aaaCreate | Microsoft Docs"
description: "자습서-hello Azure PowerShell을 사용 하 여 사용자 지정 VM 이미지를 만듭니다."
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
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 3a759fe1b7e7b72f531399b0f4a99e341713c6a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-powershell"></a>PowerShell을 사용하여 Azure VM의 사용자 지정 이미지 만들기

사용자 지정 이미지는 Marketplace 이미지와 같지만 직접 만듭니다. 사용자 지정 이미지에는 응용 프로그램, 응용 프로그램 구성 및 기타 운영 체제 구성을 미리 로드 하는 등 사용된 toobootstrap 구성 될 수 있습니다. 이 자습서에서는 Azure Virtual Machines의 사용자 지정 이미지를 만듭니다. 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * VM Sysprep 및 일반화
> * 사용자 지정 이미지 만들기
> * 사용자 지정 이미지에서 VM 만들기
> * 구독에서 모든 hello 이미지 나열
> * 이미지 삭제

이 자습서는 Azure PowerShell 모듈 버전 3.6 이상 hello가 필요합니다. 실행 ` Get-Module -ListAvailable AzureRM` toofind hello 버전입니다. Tooupgrade 필요한 경우 참조 [Azure PowerShell 설치 모듈](/powershell/azure/install-azurerm-ps)합니다.

## <a name="before-you-begin"></a>시작하기 전에

다음 hello 단계 tootake 기존 VM 및 설정에 재사용 가능한 사용자 지정 이미지를 toocreate 새 VM 인스턴스 사용 방법을 자세히 설명 합니다.

이 자습서에서는 toocomplete hello 예제에서는 기존 가상 컴퓨터 있어야 합니다. 필요한 경우 이 [스크립트 샘플](../scripts/virtual-machines-windows-powershell-sample-create-vm.md)을 사용하여 가상 컴퓨터를 만들 수 있습니다. Hello 자습서를 통해 작업 대체 필요한 경우 hello 리소스 그룹 및 VM 이름 합니다.

## <a name="prepare-vm"></a>VM 준비

가상 컴퓨터의 이미지 toocreate tooprepare hello VM 일반화 hello VM 할당 해제, 한 다음 Azure에서 일반화 된 것과 같이 VM hello 소스를 표시 하 여 필요 합니다.

### <a name="generalize-hello-windows-vm-using-sysprep"></a>일반화 hello Sysprep를 사용 하 여 Windows VM

Sysprep는 특히, 모든 개인 계정 정보를 제거 하 고 이미지 형식으로 사용 되는 hello 컴퓨터 toobe를 준비 합니다. Sysprep에 대 한 세부 정보를 참조 하십시오. [어떻게 tooUse Sysprep: 소개](http://technet.microsoft.com/library/bb457073.aspx)합니다.


1. Toohello 가상 컴퓨터를 연결 합니다.
2. Hello 명령 프롬프트 창을 관리자 권한으로 엽니다. Hello 디렉터리도 변경*%windir%\system32\sysprep*, 한 다음 실행 *sysprep.exe*합니다.
3. Hello에 **시스템 준비 도구** 대화 상자에서 *입력 시스템을 기본 OOBE (Experience)*, 해당 hello 있는지 확인 하 고 *일반화* 확인란을 선택 합니다.
4. **종료 옵션**에서 *종료*를 선택한 다음 **확인**을 클릭합니다.
5. Sysprep이 완료 된 hello 가상 컴퓨터를 종료 합니다. **Hello VM 다시 시작 하지 않으면**합니다.

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a>할당을 취소 하 고 hello VM 일반화 된 대로 표시

이미지 toocreate hello VM toobe 할당 취소 되 고 Azure에서 일반화 한 것으로 표시 해야 합니다.

사용 하 여 할당 취소 된 hello VM [중지 AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm)합니다.

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Force
```

Hello 가상 컴퓨터의 hello 상태를 너무 설정`-Generalized` 를 사용 하 여 [집합 AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm)합니다. 
   
```powershell
Set-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Generalized
```


## <a name="create-hello-image"></a>Hello 이미지 만들기

이제를 사용 하 여 hello VM의 이미지를 만들 수 [새로 AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) 및 [새로 AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage)합니다. hello 다음 예제에서는 명명 된 이미지 *myImage* 라는 VM에서 *myVM*합니다.

Hello 가상 컴퓨터를 가져옵니다. 

```powershell
$vm = Get-AzureRmVM -Name myVM -ResourceGroupName myResourceGroupImages
```

Hello 이미지 구성을 만듭니다.

```powershell
$image = New-AzureRmImageConfig -Location EastUS -SourceVirtualMachineId $vm.ID 
```

Hello 이미지를 만듭니다.

```powershell
New-AzureRmImage -Image $image -ImageName myImage -ResourceGroupName myResourceGroupImages
``` 

 
## <a name="create-vms-from-hello-image"></a>Hello 이미지에서 Vm 만들기

이미지를가지고 hello 이미지에서 하나 이상의 새 Vm을 만들 수 있습니다. 사용자 지정 이미지에서 VM 만들기는 매우 유사한 toocreating 마켓플레이스 이미지를 사용 하는 VM입니다. 마켓플레이스 이미지를 사용 하면 hello 이미지, 이미지 공급자, 제품, SKU 및 버전에 대 한 tooinformation을 해야 합니다. 사용자 지정 이미지를 사용 하기만 하면 hello 사용자 지정 이미지 리소스의 tooprovide hello ID입니다. 

다음 스크립트는 hello, 변수 만듭니다 *$image* toostore hello 사용자 지정 이미지를 사용 하는 방법은 [Get AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) 데 사용 되는 다음 [집합-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)hello를 사용 하 여 hello ID를 지정 하 고 *$image* 변수 방금 만든 합니다. 

hello 스크립트 라는 VM 만듭니다 *myVMfromImage* 라는 새 리소스 그룹에는 사용자 지정 이미지에서 *myResourceGroupFromImage* hello에 *West US* 위치 합니다.


```powershell
$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

New-AzureRmResourceGroup -Name myResourceGroupFromImage -Location EastUS

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name "mypublicdns$(Get-Random)" `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4

  $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

  $nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$vmConfig = New-AzureRmVMConfig `
    -VMName myVMfromImage `
    -VMSize Standard_D1 | Set-AzureRmVMOperatingSystem -Windows `
        -ComputerName myComputer `
        -Credential $cred 

# Here is where we create a variable toostore information about hello image 
$image = Get-AzureRmImage `
    -ImageName myImage `
    -ResourceGroupName myResourceGroupImages

# Here is where we specify that we want toocreate hello VM from and image and provide hello image ID
$vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -Id $image.Id

$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id

New-AzureRmVM `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -VM $vmConfig
```

## <a name="image-management"></a>이미지 관리 

다음은 일반 관리 이미지 작업의 몇 가지 예제와 방법을 toocomplete PowerShell을 사용 하 게 합니다.

이름별로 모든 이미지를 나열합니다.

```powershell
$images = Find-AzureRMResource -ResourceType Microsoft.Compute/images 
$images.name
```

이미지 삭제를 삭제합니다. 이 예에서는 삭제 hello 라는 이미지 *myOldImage* hello에서 *myResourceGroup*합니다.

```powershell
Remove-AzureRmImage `
    -ImageName myOldImage `
    -ResourceGroupName myResourceGroup
```

## <a name="next-steps"></a>다음 단계

이 자습서에서는 사용자 지정 VM 이미지를 만들었습니다. 다음 방법에 대해 알아보았습니다.

> [!div class="checklist"]
> * VM Sysprep 및 일반화
> * 사용자 지정 이미지 만들기
> * 사용자 지정 이미지에서 VM 만들기
> * 구독에서 모든 hello 이미지 나열
> * 이미지 삭제

어떻게 항상 사용 가능한 가상 컴퓨터에 대 한 다음 자습서 toolearn toohello를 진행 합니다.

> [!div class="nextstepaction"]
> [항상 사용 가능한 VM 만들기](tutorial-availability-sets.md)



