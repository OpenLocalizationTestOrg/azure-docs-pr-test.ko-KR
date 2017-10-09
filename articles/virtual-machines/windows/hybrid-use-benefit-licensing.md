---
title: "Windows Server 및 Windows 클라이언트에 대 한 하이브리드 사용 혜택 aaaAzure | Microsoft Docs"
description: "어떻게 toomaximize Windows Software Assurance 혜택 toobring 온-프레미스에 알아봅니다 tooAzure 라이선스"
services: virtual-machines-windows
documentationcenter: 
author: kmouss
manager: timlt
editor: 
ms.assetid: 332583b6-15a3-4efb-80c3-9082587828b0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 5/26/2017
ms.author: xujing
ms.openlocfilehash: f24487320a60132aaf766a31f3e6f3726d4a3bd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-hybrid-use-benefit-for-windows-server-and-windows-client"></a>Window Server 및 Windows 클라이언트에 대한 Azure 하이브리드 사용 혜택
Software Assurance와 함께 고객에 대 한 Azure 하이브리드 사용 혜택 사용 하면 toouse 온-프레미스 Windows Server 및 Windows 클라이언트 라이선스 및 저렴된 한 비용에 Azure에서 실행된 Windows 가상 컴퓨터. Windows Server에 대한 Azure 하이브리드 사용 혜택에는 Windows Server 2008R2, Windows Server 2012, Windows Server 2012R2 및 Windows Server 2016이 포함됩니다. Windows 클라이언트에 대한 Azure 하이브리드 사용 혜택에는 Windows 10이 포함됩니다. 자세한 내용은 hello를 참조 하십시오 [Azure 하이브리드 사용 혜택 라이선스 페이지](https://azure.microsoft.com/pricing/hybrid-use-benefit/)합니다.

>[!IMPORTANT]
>Azure 하이브리드 사용 이점에 대 한 Windows 클라이언트는 현재 미리 보기로 hello Windows 10 이미지를 사용 하 여 hello Azure Marketplace에서. 사용자별 Windows 10 Enterprise E3/E5 또는 사용자별 Windows VDA(사용자 구독 라이선스 또는 추가 기능 사용자 구독 라이선스)를 보유한 엔터프라이즈 고객("적격 라이선스")만 혜택을 누릴 수 있습니다.
>
>

## <a name="ways-toouse-azure-hybrid-use-benefit"></a>같은 방법으로 toouse Azure 하이브리드 사용 이점
Azure 하이브리드 사용 혜택 hello로 다양 한 방법 toodeploy Windows Vm의 두 가지가 있습니다.

1. Azure 하이브리드 사용 혜택을 이용하여 미리 구성된 [특정 Marketplace 이미지](#deploy-a-vm-using-the-azure-marketplace)(Windows Server 2016, Windows Server 2012R2, Windows Server 2012 및 Windows Server 2008SP1)에서 VM을 배포할 수 있습니다.
2. [사용자 지정 VM을 업로드](#upload-a-windows-vhd)하거나 [Resource Manager 템플릿](#deploy-a-vm-via-resource-manager) 또는 [Azure PowerShell을 사용하여 배포](#detailed-powershell-deployment-walkthrough)할 수 있습니다.

## <a name="deploy-a-vm-using-hello-azure-marketplace"></a>Hello Azure Marketplace를 사용 하 여 VM 배포
다음 이미지는 hello Azure 하이브리드 사용 혜택으로 미리 구성 하는 Marketplace에서에서 사용할 수 있습니다.: Windows Server 2016, Windows Server 2012 r 2, Windows Server 2012 및 Windows Server 2008SP1 합니다. 이러한 이미지는 Azure 포털 hello, 리소스 관리자 템플릿 또는 Azure PowerShell에서 직접 배포할 수 있습니다.

Hello Azure 포털에서 직접 이러한 이미지를 배포할 수 있습니다. 리소스 관리자 템플릿을 Azure PowerShell을 사용 하 여 사용 하기 위해 볼 hello 이미지 목록이 방법은 다음과 같습니다.

Windows Server:
```powershell
Get-AzureRmVMImagesku -Location westus -PublisherName MicrosoftWindowsServer -Offer WindowsServer
```
- 2016-Datacenter 버전 2016.127.20170406 이상

- 2012-R2-Datacenter 버전 4.127.20170406 이상

- 2012-Datacenter 버전 3.127.20170406 이상

- 2008-R2-SP1 버전 2.127.20170406 이상

Windows 클라이언트:
```powershell
Get-AzureRMVMImageSku -Location "West US" -Publisher "MicrosoftWindowsServer" `
    -Offer "Windows-HUB"
```

## <a name="upload-a-windows-server-vhd"></a>Windows Server VHD 업로드
Azure에서 Windows Server VM toodeploy 먼저 toocreate 기본 Windows 빌드를 포함 하는 VHD입니다. TooAzure 업로드 하기 전에이 VHD Sysprep을 통해 적절 하 게 준비 해야 합니다. 있습니다 수 [hello VHD 요구 사항 및 Sysprep 프로세스에 대 한 자세한](upload-generalized-managed.md) 및 [서버 역할에 대 한 Sysprep 지원](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)합니다. Sysprep를 실행 하기 전에 hello VM 백업 합니다. 

있는지 [최신 Azure PowerShell 설치 및 구성 된 hello](/powershell/azure/overview)합니다. VHD를 준비 했으면, 업로드 hello를 사용 하 여 hello VHD tooyour Azure 저장소 계정을 `Add-AzureRmVhd` 다음과 같이 cmdlet:

```powershell
Add-AzureRmVhd -ResourceGroupName "myResourceGroup" -LocalFilePath "C:\Path\To\myvhd.vhd" `
    -Destination "https://mystorageaccount.blob.core.windows.net/vhds/myvhd.vhd"
```

> [!NOTE]
> Microsoft SQL Server, SharePoint 서버 및 Dynamics는 또한 Software Assurance 라이선스를 활용할 수 있습니다. 응용 프로그램 구성 요소를 설치 하 고 라이선스 키를 적절 하 게 제공 다음 hello 디스크 이미지 tooAzure 업로드 하 여 tooprepare hello Windows Server 이미지를 여전히 필요 합니다. Hello와 같은 응용 프로그램에 Sysprep를 실행 하기 위한 적절 한 설명서를 검토 [Sysprep를 사용 하 여 SQL Server 설치를 위한 고려 사항](https://msdn.microsoft.com/library/ee210754.aspx) 또는 [(Sysprep)SharePointServer2016참조이미지만들기](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).
>
>

또한 자세한 방법에 대 한 [hello VHD tooAzure 프로세스를 업로드 하는 중](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)


## <a name="deploy-a-vm-via-resource-manager-template"></a>Resource Manager 템플릿을 통해 VM 배포
Resource Manager 템플릿 내에서 `licenseType` 에 대한 추가 매개 변수를 지정할 수 있습니다. [Azure Resource Manager 템플릿 작성](../../resource-group-authoring-templates.md)에 대해 자세히 알아볼 수 있습니다. VHD 업로드 tooAzure를 만든 후 편집 하면 리소스 관리자 템플릿 tooinclude hello 라이선스 유형 hello의 일부 공급자를 계산 하 고 일반적인 방법으로 템플릿을 배포 합니다.

Windows Server:
```json
"properties": {  
   "licenseType": "Windows_Server",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

Windows 클라이언트 toouse Azure 마켓플레이스 이미지와만에 대 한:
```json
"properties": {  
   "licenseType": "Windows_Client",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

## <a name="deploy-a-vm-via-powershell-quickstart"></a>PowerShell 빠른 시작을 통해 VM 배포
PowerShell을 통해 Windows Server VM을 배포할 때는 `-LicenseType`에 대한 추가 매개 변수가 있습니다. 사용 하 여 VM을 만들 VHD 업로드 tooAzure를 만든 후 `New-AzureRmVM` hello 라이선스 유형을 다음과 같이 지정 합니다.

Windows Server:
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Server"
```

Windows 클라이언트 toouse Azure 마켓플레이스 이미지와만에 대 한:
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Client"
```

할 수 있습니다 [PowerShell 통해 Azure에서 VM 배포에 보다 자세한 연습 읽을](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) 에 보다 설명적인 가이드 hello 너무 다른 단계가 아래 또는 읽기[리소스 관리자 및 PowerShell를사용하여WindowsVM을만들](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


## <a name="verify-your-vm-is-utilizing-hello-licensing-benefit"></a>VM hello 라이선스 혜택을 활용 하는 확인
Hello PowerShell 또는 리소스 관리자 배포 방법 중 하나를 통해 VM을 배포한 후 확인 된 hello 라이선스 유형을 `Get-AzureRmVM` 다음과 같습니다.

```powershell
Get-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
```

hello는 비슷한 toohello 다음 예제에서는 Windows Server에 대 한 출력:

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              : Windows_Server
```

이 출력 다음 VM hello Azure 갤러리에서 직접 배포 된 VM과 같은 Azure 하이브리드 사용 혜택 라이선스 없이 배포 된 hello와 대조 합니다.

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              :
```

## <a name="detailed-powershell-deployment-walkthrough"></a>자세한 PowerShell 배포 연습
hello 다음 PowerShell 단계 표시 VM의 전체 배포를 자세히 설명합니다. Toohello 실제 cmdlet에서 생성 되 고 다른 구성 요소와 더 많은 컨텍스트를 읽을 수 [리소스 관리자 및 PowerShell을 사용 하 여 Windows VM을 만들](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. 단계별로 리소스 그룹, 저장소 계정 및 가상 네트워킹을 만든 다음 VM을 정의하고 마지막으로 VM을 만듭니다.

먼저 안전하게 자격 증명을 얻고, 위치를 설정하고, 리소스 그룹 이름을 지정합니다.

```powershell
$cred = Get-Credential
$location = "West US"
$resourceGroupName = "myResourceGroup"
```

공용 IP 만들기:

```powershell
$publicIPName = "myPublicIP"
$publicIP = New-AzureRmPublicIpAddress -Name $publicIPName -ResourceGroupName $resourceGroupName `
    -Location $location -AllocationMethod "Dynamic"
```

서브넷, NIC 및 VNET을 정의합니다.

```powershell
$subnetName = "mySubnet"
$nicName = "myNIC"
$vnetName = "myVnet"
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/8
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location `
    -AddressPrefix 10.0.0.0/8 -Subnet $subnetconfig
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $resourceGroupName -Location $location `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $publicIP.Id
```

VM 이름을 지정하고 VM 구성을 만듭니다.

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A1"
```

OS 정의:

```powershell
$computerName = "myVM"
$vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

프로그램 NIC toohello VM을 추가 합니다.

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

저장소 계정 toouse hello를 정의 합니다.

```powershell
$storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -AccountName mystorageaccount
```

적절 하 게 준비 된 VHD를 업로드 하 고 사용 하기 위해 VM tooyour 연결:

```powershell
$osDiskName = "licensing.vhd"
$osDiskUri = '{0}vhds/{1}{2}.vhd' -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/vhd/myvhd.vhd"
$vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption FromImage `
    -SourceImageUri $urlOfUploadedImageVhd -Windows
```

마지막으로, VM 만들고 형식 tooutilize Azure 하이브리드 사용 혜택 라이선스 hello 정의:

Windows Server:
```powershell
New-AzureRmVM -ResourceGroupName $resourceGroupName -Location $location -VM $vm -LicenseType "Windows_Server"
```

## <a name="deploy-a-virtual-machine-scale-set-via-resource-manager-template"></a>Resource Manager 템플릿을 사용하여 가상 컴퓨터 크기 집합 배포
VMSS Resource Manager 템플릿 내에서 `licenseType` 에 대한 추가 매개 변수를 지정해야 합니다. [Azure Resource Manager 템플릿 작성](../../resource-group-authoring-templates.md)에 대해 자세히 알아볼 수 있습니다. Hello 크기 집합 virtualMachineProfile의 일환으로 리소스 관리자 템플릿 tooinclude hello licenseType 속성을 편집 하 고 일반적인 방법으로 템플릿을 배포-2016 Windows Server 이미지를 사용 하 여 아래 예제를 참조 하십시오.


```json
"virtualMachineProfile": {
    "storageProfile": {
        "osDisk": {
            "createOption": "FromImage"
        },
        "imageReference": {
            "publisher": "MicrosoftWindowsServer",
            "offer": "WindowsServer",
            "sku": "2016-Datacenter",
            "version": "latest"
        }
    },
    "licenseType": "Windows_Server",
    "osProfile": {
            "computerNamePrefix": "[parameters('vmssName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
    }
```

> [!NOTE]
> PowerShell 및 다른 SDK 도구를 통해 AHUB 기능을 활용하여 가상 컴퓨터 확장 집합을 배포하는 방식은 곧 지원될 예정입니다.
>

## <a name="next-steps"></a>다음 단계
자세한 내용은 [Azure 하이브리드 사용 혜택 라이선싱](https://azure.microsoft.com/pricing/hybrid-use-benefit/)을 참조하세요.

[Resource Manager 템플릿 사용](../../azure-resource-manager/resource-group-overview.md)에 대해 자세히 알아봅니다.

에 대 한 자세한 내용은 [Azure 하이브리드 사용 이점 및 Azure 사이트 복구 확인 마이그레이션 응용 프로그램 tooAzure 훨씬 더 비용 효율적인](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/)합니다.
