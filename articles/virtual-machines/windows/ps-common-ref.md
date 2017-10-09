---
title: "aaaCommon PowerShell 명령에 대 한 Azure 가상 컴퓨터 | Microsoft Docs"
description: "만들기 및 관리 Windows Azure 내 Vm의에서 일반적인 PowerShell 명령을 tooget 시작 합니다."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ba3839a2-f3d5-4e19-a5de-95bfb1c0e61e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: 3de9bd4d20259ced2c0aa8ef7a3f7d9520a071d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="common-powershell-commands-for-creating-and-managing-azure-virtual-machines"></a>Azure Virtual Machines를 만들고 관리하기 위한 공통 PowerShell 명령

이 문서에서는 hello toocreate를 사용 하 고 Azure 구독에서 가상 컴퓨터를 관리할 수 있는 Azure PowerShell 명령 중 일부에 대해 설명 합니다.  특정 명령줄 스위치 및 옵션에 대해 자세한 도움이 필요할 경우 **Get-Help** *명령*을 사용할 수 있습니다.

참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) hello 최신 버전의 Azure PowerShell을 설치, 구독을 선택 하 고 tooyour 계정에 로그인 하는 방법에 대 한 정보에 대 한 합니다.

이 문서에 둘 이상의 hello 명령을 실행 하는 경우 이러한 변수 두면 유용할 수 있습니다.

- $location-hello 가상 컴퓨터의 hello 위치입니다. 사용할 수 있습니다 [Get AzureRmLocation](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermlocation) toofind는 [지리적 지역의](https://azure.microsoft.com/regions/) 있는 주시기 바랍니다.
- $myResourceGroup-hello 가상 컴퓨터가 포함 된 hello 리소스 그룹의 hello 이름입니다.
- $myVM-hello 가상 컴퓨터의 hello 이름입니다.

## <a name="create-a-vm"></a>VM 만들기

| 작업 | 명령 |
| ---- | ------- |
| VM 구성 만들기 |$vm = [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvmconfig) -VMName $myVM -VMSize "Standard_D1_v1"<BR></BR><BR></BR>hello VM 구성은 hello VM에 대 한 toodefine 또는 업데이트 설정이 사용된 합니다. hello 구성의 VM hello hello 이름으로 초기화 됩니다 및 해당 [크기](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. |
| 구성 설정 추가 |$vm = [Set-AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) -VM $vm -Windows -ComputerName $myVM -Credential $cred -ProvisionVMAgent -EnableAutoUpdate<BR></BR><BR></BR>운영 체제 설정을 포함 하 여 [자격 증명](https://technet.microsoft.com/library/hh849815.aspx) AzureRmVMConfig 새로 만들기를 사용 하 여 이전에 만든 toohello 구성 개체에 추가 됩니다. |
| 네트워크 인터페이스 추가 |$vm = [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/Add-AzureRmVMNetworkInterface) -VM $vm -Id $nic.Id<BR></BR><BR></BR>VM 있어야는 [네트워크 인터페이스](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toocommunicate 가상 네트워크에 있습니다. 사용할 수도 있습니다 [Get AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) tooretrieve 기존 네트워크 인터페이스 개체입니다. |
| 플랫폼 이미지 지정 |$vm = [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmsourceimage) -VM $vm -PublisherName "publisher_name" -Offer "publisher_offer" -Skus "product_sku" -Version "latest"<BR></BR><BR></BR>[이미지 정보](cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) AzureRmVMConfig 새로 만들기를 사용 하 여 이전에 만든 toohello 구성 개체에 추가 됩니다. 이 명령에서 반환 하는 hello 개체 hello OS 디스크 toouse 플랫폼 이미지를 설정 하는 경우에 사용 됩니다. |
| OS 디스크 toouse 플랫폼 이미지 설정 |$vm = [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmosdisk) -VM $vm -Name "myOSDisk" -VhdUri "http://mystore1.blob.core.windows.net/vhds/myOSDisk.vhd" -CreateOption FromImage<BR></BR><BR></BR>hello 운영 체제 디스크 및 해당 위치에서의 hello 이름 [저장소](../../storage/common/storage-powershell-guide-full.md) 이전에 만든 toohello 구성 개체에 추가 됩니다. |
| 이미지를 일반화 된 운영 체제 디스크 toouse 설정 |$vm = Set-AzureRmVMOSDisk -VM $vm -Name "myOSDisk" -SourceImageUri "https://mystore1.blob.core.windows.net/system/Microsoft.Compute/Images/myimages/myprefix-osDisk.{guid}.vhd" -VhdUri "https://mystore1.blob.core.windows.net/vhds/disk_name.vhd" -CreateOption FromImage -Windows<BR></BR><BR></BR>hello 이름 hello 운영 체제 디스크, hello 원본 이미지의 hello 위치 및 hello 디스크의 위치에 [저장소](../../storage/common/storage-powershell-guide-full.md) toohello 구성 개체에 추가 됩니다. |
| OS 디스크 toouse 특수 이미지 설정 |$vm = Set-AzureRmVMOSDisk -VM $vm -Name "myOSDisk" -VhdUri "http://mystore1.blob.core.windows.net/vhds/" -CreateOption Attach -Windows |
| VM 만들기 |[New-AzureRmVM]() -ResourceGroupName $myResourceGroup -Location $location -VM $vm<BR></BR><BR></BR>모든 리소스는 [리소스 그룹](../../azure-resource-manager/powershell-azure-resource-manager.md)에서 생성됩니다. 이 명령을 실행하기 전에, New-AzureRmVMConfig, Set-AzureRmVMOperatingSystem, Set-AzureRmVMSourceImage, Add-AzureRmVMNetworkInterface, and Set-AzureRmVMOSDisk을 실행합니다. |

## <a name="get-information-about-vms"></a>VM에 대한 정보 가져오기

| 작업 | 명령 |
| ---- | ------- |
| 구독에서 Vm 나열 |[Get AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvm) |
| 리소스 그룹에서 Vm 나열 |Get-AzureRmVM -ResourceGroupName $myResourceGroup<BR></BR><BR></BR>구독에서 tooget 리소스의 목록을 그룹, 사용 하 여 [Get AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermresourcegroup)합니다. |
| VM 관련 정보 가져오기 |Get-AzureRmVM -ResourceGroupName $myResourceGroup -Name $myVM |

## <a name="manage-vms"></a>VM 관리
| 작업 | 명령 |
| --- | --- |
| VM 시작 |[Start-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/start-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM |
| VM 중지 |[Stop-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/stop-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM |
| 실행 중인 VM 다시 시작 |[Restart-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/restart-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM |
| VM 삭제 |[Remove-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM |
| VM 일반화 |[Set-AzureRmVm](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM -Generalized<BR></BR><BR></BR>이 명령을 Save-AzureRmVMImage를 실행하기 전에 실행합니다. |
| VM 캡처 |[Save-AzureRmVMImage](https://docs.microsoft.com/powershell/module/azurerm.compute/save-azurermvmimage) -ResourceGroupName $myResourceGroup -VMName $myVM -DestinationContainerName "myImageContainer" -VHDNamePrefix "myImagePrefix" -Path "C:\filepath\filename.json"<BR></BR><BR></BR>가상 컴퓨터가 있어야 [준비, 종료 및 일반화](prepare-for-upload-vhd-image.md) 사용 toobe toocreate 이미지입니다. 이 명령을 실행하기 전에 Set-AzureRmVm을 실행합니다. |
| VM 업데이트 |[Update-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/update-azurermvm) -ResourceGroupName $myResourceGroup -VM $vm<BR></BR><BR></BR>Get AzureRmVM를 사용 하 여 hello 현재 VM 구성을 가져오고 hello VM 개체의 구성 설정을 변경 후이 명령을 실행 합니다. |
| 데이터 디스크 tooa VM 추가 |[Add-AzureRmVMDataDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvmdatadisk) -VM $vm -Name "myDataDisk" -VhdUri "https://mystore1.blob.core.windows.net/vhds/myDataDisk.vhd" -LUN # -Caching ReadWrite -DiskSizeinGB # -CreateOption Empty<BR></BR><BR></BR>Get AzureRmVM tooget hello VM 개체를 사용 합니다. Hello LUN 수 및 hello hello 디스크 크기를 지정 합니다. 업데이트 AzureRmVM tooapply hello 구성 변경 내용을 toohello VM을 실행 합니다. 추가 하는 hello 디스크 초기화 되지 않았습니다. |
| VM에서 데이터 디스크 제거 |[Remove-AzureRmVMDataDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvmdatadisk) -VM $vm -Name "myDataDisk"<BR></BR><BR></BR>Get AzureRmVM tooget hello VM 개체를 사용 합니다. 업데이트 AzureRmVM tooapply hello 구성 변경 내용을 toohello VM을 실행 합니다. |
| 확장 tooa VM 추가 |[Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) -ResourceGroupName $myResourceGroup -Location $location -VMName $myVM -Name "extensionName" -Publisher "publisherName" -Type "extensionType" -TypeHandlerVersion "#.#" -Settings $Settings -ProtectedSettings $ProtectedSettings<BR></BR><BR></BR>이 명령을 실행 하 여 적절 한 hello로 [구성 정보](template-description.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#extensions) tooinstall hello 확장명에 대 한 합니다. |
| VM 확장 제거 |[Remove-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvmextension) -ResourceGroupName $myResourceGroup -Name "extensionName" -VMName $myVM |

## <a name="next-steps"></a>다음 단계
* Hello에 가상 컴퓨터를 만들기 위한 기본 단계를 참조 [리소스 관리자 및 PowerShell을 사용 하 여 Windows VM을 만들](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

