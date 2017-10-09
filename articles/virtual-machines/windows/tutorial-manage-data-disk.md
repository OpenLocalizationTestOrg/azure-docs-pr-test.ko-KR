---
title: "Azure PowerShell hello로 aaaManage Azure 디스크 | Microsoft Docs"
description: "자습서-hello Azure PowerShell로 Azure 디스크 관리"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 2f61ad18bc94bab527d7ae593da603c6073adc89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-powershell"></a>PowerShell을 사용하여 Azure 디스크 관리

Azure 가상 컴퓨터 디스크 toostore hello Vm 운영 체제, 응용 프로그램 및 데이터를 사용 합니다. VM을 만들 때 중요 한 toochoose 디스크 크기 및 구성 필요 합니다. 적절 한 toohello 작업 부하는 합니다. 이 자습서에서는 VM 디스크의 배포 및 관리에 대해 다룹니다. 다음에 대해 알아봅니다.

> [!div class="checklist"]
> * OS 디스크 및 임시 디스크
> * 데이터 디스크
> * 표준 및 프리미엄 디스크
> * 디스크 성능
> * 데이터 디스크 연결 및 준비

이 자습서는 Azure PowerShell 모듈 버전 3.6 이상 hello가 필요합니다. 실행 ` Get-Module -ListAvailable AzureRM` toofind hello 버전입니다. Tooupgrade 필요한 경우 참조 [Azure PowerShell 설치 모듈](/powershell/azure/install-azurerm-ps)합니다.

## <a name="default-azure-disks"></a>기본 Azure 디스크

Azure 가상 컴퓨터를 만들면 두 디스크는 자동으로 연결 된 toohello 가상 컴퓨터입니다. 

**운영 체제 디스크** -운영 체제 디스크를 too1 테라바이트 크기를 조정할 수 및 호스트 hello Vm 운영 체제입니다.  hello OS 디스크의 드라이브 문자 할당 *c:* 기본적으로 합니다. hello 디스크 캐싱 구성 hello OS 디스크의 운영 체제 성능을 위해 최적화 되어 있습니다. hello OS 디스크 **없는** 응용 프로그램이 나 데이터를 호스트 합니다. 응용 프로그램 및 데이터는 데이터 디스크를 사용하며 여기에 대해서는 이 문서의 뒷부분에서 자세히 설명합니다.

**임시 디스크** -임시 디스크에 있는 반도체 드라이브를 사용 하 여 hello에 hello VM과 동일한 Azure 호스트 합니다. 임시 디스크는 성능이 높고 임시 데이터 처리 등의 작업에 사용할 수 있습니다. 그러나 이동된 tooa 새 호스트가 hello VM을 사용 하는 경우 임시 디스크에 저장 된 모든 데이터가 제거 됩니다. hello 임시 디스크의 hello 크기는 hello VM 크기에 따라 결정 됩니다. 임시 디스크는 기본적으로 *d:* 드라이브 문자가 할당됩니다.

### <a name="temporary-disk-sizes"></a>임시 디스크 크기

| 형식 | VM 크기 | 최대 임시 디스크 크기(GB) |
|----|----|----|
| [범용](sizes-general.md) | A 및 D 시리즈 | 800 |
| [Compute에 최적화](sizes-compute.md) | F 시리즈 | 800 |
| [메모리에 최적화](../virtual-machines-windows-sizes-memory.md) | D 및 G 시리즈 | 6144 |
| [Storage에 최적화](../virtual-machines-windows-sizes-storage.md) | L 시리즈 | 5630 |
| [GPU](sizes-gpu.md) | N 시리즈 | 1,440 |
| [고성능](sizes-hpc.md) | A 및 H 시리즈 | 2000 |

## <a name="azure-data-disks"></a>Azure 데이터 디스크

응용 프로그램을 설치하고 데이터를 저장하기 위해 데이터 디스크를 더 추가할 수 있습니다. 데이터 디스크는 지속형 및 반응형 데이터 저장소가 필요한 상황에 사용해야 합니다. 각 데이터 디스크의 최대 용량은 1테라바이트입니다. hello 크기 hello 가상 컴퓨터의 데이터 디스크 수는 연결 된 tooa VM 수를 결정 합니다. 각 VM 코어에 대해 두 개의 데이터 디스크를 연결할 수 있습니다. 

### <a name="max-data-disks-per-vm"></a>VM당 최대 데이터 디스크 수

| 형식 | VM 크기 | VM당 최대 데이터 디스크 수 |
|----|----|----|
| [범용](sizes-general.md) | A 및 D 시리즈 | 32 |
| [Compute에 최적화](sizes-compute.md) | F 시리즈 | 32 |
| [메모리에 최적화](../virtual-machines-windows-sizes-memory.md) | D 및 G 시리즈 | 64 |
| [Storage에 최적화](../virtual-machines-windows-sizes-storage.md) | L 시리즈 | 64 |
| [GPU](sizes-gpu.md) | N 시리즈 | 48 |
| [고성능](sizes-hpc.md) | A 및 H 시리즈 | 32 |

## <a name="vm-disk-types"></a>VM 디스크 유형

Azure는 두 가지 유형의 디스크를 제공합니다.

### <a name="standard-disk"></a>표준 디스크

Standard Storage는 HDD에 의해 지원되며 성능은 그대로이면서 비용 효율적인 저장소를 제공합니다. 표준 디스크는 비용 효율적인 개발 및 테스트 워크로드에 적합합니다.

### <a name="premium-disk"></a>프리미엄 디스크

프리미엄 디스크는 SSD 기반 고성능의 대기 시간이 짧은 디스크에서 지원합니다. 프로덕션 워크로드를 실행하는 VM에 완벽한 디스크입니다. Premium Storage는 DS 시리즈, DSv2 시리즈, GS 시리즈 및 FS 시리즈 VM을 지원합니다. 프리미엄 디스크 세 가지 유형 (P10, P20, P30)을 hello 디스크의 크기 hello hello 디스크 형식을 결정 됩니다. 선택 하 고, 디스크 크기 hello 값 toohello 다음 형식으로 반올림 됩니다. 예를 들어 hello 크기는 128GB hello 디스크 유형 아래 됩니다 P10, 129 및 512 P20, 사이의 P30 512 개. 

### <a name="premium-disk-performance"></a>프리미엄 디스크 성능

|Premium Storage 디스크 유형 | P10 | P20 | P30 |
| --- | --- | --- | --- |
| 디스크 크기(반올림) | 128GB | 512GB | 1,024GB(1TB) |
| 디스크당 IOPS | 500 | 2,300 | 5,000 |
디스크당 처리량 | 100MB/초 | 150MB/초 | 200MB/s |

테이블 위에 hello 디스크당 최대 IOPS를 식별 하는 동안에 더 높은 수준의 성능 여러 데이터 디스크를 스트라이프 하 여 구현할 수 있습니다. 예를 들어, 64 데이터 디스크 수 tooStandard_GS5 VM을 연결 합니다. 이러한 각 디스크는 P30에 해당하는 크기이며 최대 80,000 IOPS를 얻을 수 있습니다. VM당 최대 IOPS에 대한 자세한 내용은 [Linux VM 크기](./sizes.md)를 참조하세요.

## <a name="create-and-attach-disks"></a>디스크 만들기 및 연결

이 자습서에서는 toocomplete hello 예제에서는 기존 가상 컴퓨터 있어야 합니다. 필요한 경우 이 [스크립트 샘플](../scripts/virtual-machines-windows-powershell-sample-create-vm.md)을 사용하여 가상 컴퓨터를 만들 수 있습니다. Hello 자습서를 통해 작업 대체 필요한 경우 hello 리소스 그룹 및 VM 이름 합니다.

Hello와 초기 구성 만들기 [새로 AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig)합니다. 다음 예에서는 hello 디스크 128 기가바이트 크기를 구성 합니다.

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

Hello로 hello 데이터 디스크를 만들 [새로 AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) 명령입니다.

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

Get hello 가상 컴퓨터가 원하는 tooadd hello 데이터 디스크 toowith hello [Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) 명령입니다.

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

추가 hello 데이터 디스크 toohello 인 가상 컴퓨터 구성 hello [추가 AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) 명령입니다.

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

Hello로 hello 가상 컴퓨터를 업데이트 [업데이트 AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) 명령입니다.

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a>데이터 디스크 준비

디스크에 대 한 연결 된 toohello 가상 컴퓨터를 수행한 hello 운영 체제 구성 toobe toouse hello 디스크를 만들어야 합니다. hello 다음 예제에서는 toomanually 추가 hello 첫 번째 디스크를 구성 하는 방법 toohello VM입니다. Hello를 사용 하 여이 프로세스 자동화할 수도 있습니다 [사용자 지정 스크립트 확장](./tutorial-automate-vm-deployment.md)합니다.

### <a name="manual-configuration"></a>수동 구성

Hello 가상 컴퓨터에 대 한 RDP 연결을 만듭니다. PowerShell을 열고 이 스크립트를 실행합니다.

```powershell
Get-Disk | Where partitionstyle -eq 'raw' | `
Initialize-Disk -PartitionStyle MBR -PassThru | `
New-Partition -AssignDriveLetter -UseMaximumSize | `
Format-Volume -FileSystem NTFS -NewFileSystemLabel "myDataDisk" -Confirm:$false
```

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음과 같은 VM 디스크 항목에 대해 알아보았습니다.

> [!div class="checklist"]
> * OS 디스크 및 임시 디스크
> * 데이터 디스크
> * 표준 및 프리미엄 디스크
> * 디스크 성능
> * 데이터 디스크 연결 및 준비

VM 구성을 자동화 하는 방법에 대 한 다음 자습서 toolearn toohello를 진행 합니다.

> [!div class="nextstepaction"]
> [VM 구성 자동화](./tutorial-automate-vm-deployment.md)
