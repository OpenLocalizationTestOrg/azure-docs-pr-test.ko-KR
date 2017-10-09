---
title: "hello Azure CLI로 aaaManage Azure 디스크 | Microsoft Docs"
description: "자습서-Azure CLI hello로 Azure 디스크 관리"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ad29cfbec5f9738f47705b19d0450c9a2f555492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-hello-azure-cli"></a>Hello Azure CLI로 Azure 디스크 관리

Azure 가상 컴퓨터 디스크 toostore hello Vm 운영 체제, 응용 프로그램 및 데이터를 사용 합니다. VM을 만들 때 중요 한 toochoose 디스크 크기 및 구성 필요 합니다. 적절 한 toohello 작업 부하는 합니다. 이 자습서에서는 VM 디스크의 배포 및 관리에 대해 다룹니다. 다음에 대해 알아봅니다.

> [!div class="checklist"]
> * OS 디스크 및 임시 디스크
> * 데이터 디스크
> * 표준 및 프리미엄 디스크
> * 디스크 성능
> * 데이터 디스크 연결 및 준비
> * 디스크 크기 조정
> * 디스크 스냅숏


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 자습서를 사용 하려면 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

## <a name="default-azure-disks"></a>기본 Azure 디스크

Azure 가상 컴퓨터를 만들면 두 디스크는 자동으로 연결 된 toohello 가상 컴퓨터입니다. 

**운영 체제 디스크** -운영 체제 디스크를 too1 테라바이트 크기를 조정할 수 및 호스트 hello Vm 운영 체제입니다. hello OS 디스크 레이블이 */개발/sda* 기본적으로 합니다. hello 디스크 캐싱 구성 hello OS 디스크의 운영 체제 성능을 위해 최적화 되어 있습니다. 이 구성으로 인해 OS 디스크 hello **없는** 응용 프로그램이 나 데이터를 호스트 합니다. 응용 프로그램 및 데이터는 데이터 디스크를 사용하며 여기에 대해서는 이 문서의 뒷부분에서 자세히 설명합니다. 

**임시 디스크** -임시 디스크에 있는 반도체 드라이브를 사용 하 여 hello에 hello VM과 동일한 Azure 호스트 합니다. 임시 디스크는 성능이 높고 임시 데이터 처리 등의 작업에 사용할 수 있습니다. 그러나 이동된 tooa 새 호스트가 hello VM을 사용 하는 경우 임시 디스크에 저장 된 모든 데이터가 제거 됩니다. hello 임시 디스크의 hello 크기는 hello VM 크기에 따라 결정 됩니다. 임시 디스크는 */dev/sdb*로 레이블이 지정되고 탑재 지점은 */mnt*입니다.

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

프리미엄 디스크는 SSD 기반 고성능의 대기 시간이 짧은 디스크에서 지원합니다. 프로덕션 워크로드를 실행하는 VM에 완벽한 디스크입니다. Premium Storage는 DS 시리즈, DSv2 시리즈, GS 시리즈 및 FS 시리즈 VM을 지원합니다. 프리미엄 디스크 세 가지 유형 (P10, P20, P30)을 hello 디스크의 크기 hello hello 디스크 형식을 결정 됩니다. 선택 하 고, 디스크 크기 hello 값 toohello 다음 형식으로 반올림 됩니다. 예를 들어 hello 디스크 크기가 128 g B 미만인 경우 hello 디스크 유형 P10입니다. Hello 디스크 크기 129 GB와 512GB 사이 있으면 hello 크기는 P20는입니다. 아무 것도 512GB 넘는 hello 크기는는 P30 합니다.

### <a name="premium-disk-performance"></a>프리미엄 디스크 성능

|Premium Storage 디스크 유형 | P10 | P20 | P30 |
| --- | --- | --- | --- |
| 디스크 크기(반올림) | 128GB | 512GB | 1,024GB(1TB) |
| 디스크당 최대 IOPS | 500 | 2,300 | 5,000 |
디스크당 처리량 | 100MB/초 | 150MB/초 | 200MB/s |

테이블 위에 hello 디스크당 최대 IOPS를 식별 하는 동안에 더 높은 수준의 성능 여러 데이터 디스크를 스트라이프 하 여 구현할 수 있습니다. 예를 들어 Standard_GS5 VM은 최대 80,000 IOPS를 얻을 수 있습니다. VM당 최대 IOPS에 대한 자세한 내용은 [Linux VM 크기](sizes.md)를 참조하세요.

## <a name="create-and-attach-disks"></a>디스크 만들기 및 연결

데이터 디스크를 만들고 VM 생성 시간 또는 tooan 기존 VM에 연결 된 수 있습니다.

### <a name="attach-disk-at-vm-creation"></a>VM을 만들 때 디스크 연결

Hello로 리소스 그룹 만들기 [az 그룹 만들기](https://docs.microsoft.com/cli/azure/group#create) 명령입니다. 

```azurecli-interactive 
az group create --name myResourceGroupDisk --location eastus
```

Hello를 사용 하 여 VM 만들기 [az vm 만들기]( /cli/azure/vm#create) 명령입니다. hello `--datadisk-sizes-gb` 인수는 사용 되는 toospecify 추가 디스크는 만들어야 하며 toohello 가상 컴퓨터를 연결 합니다. toocreate 둘 이상의 디스크를 연결 하 고, 디스크 크기 값은 공백으로 구분 된 목록을 사용 하 여 합니다. 다음 예제는 hello, VM 두 개의 데이터 디스크를 모두 128GB 만들어집니다. Hello 디스크 크기는 128GB 이기 때문에 이러한 디스크 둘 다 P10s 500 최대 디스크 IOPS를 제공 하는로 구성 됩니다.

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupDisk \
  --name myVM \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --data-disk-sizes-gb 128 128 \
  --generate-ssh-keys
```

### <a name="attach-disk-tooexisting-vm"></a>디스크 tooexisting VM 연결

toocreate hello를 사용 하 여, 새 디스크 tooan 기존 가상 컴퓨터를 연결 하 고 [az vm 디스크를 연결](/cli/azure/vm/disk#attach) 명령입니다. hello 다음 예제에서는 128gb 크기에서 프리미엄 디스크를 만들고 toohello hello 마지막 단계에서 만든 VM에 연결 합니다.

```azurecli-interactive 
az vm disk attach --vm-name myVM --resource-group myResourceGroupDisk --disk myDataDisk --size-gb 128 --sku Premium_LRS --new 
```

## <a name="prepare-data-disks"></a>데이터 디스크 준비

디스크에 대 한 연결 된 toohello 가상 컴퓨터를 수행한 hello 운영 체제 구성 toobe toouse hello 디스크를 만들어야 합니다. 다음 예제는 hello toomanually 디스크를 구성 하는 방법을 보여 줍니다. 이 프로세스는 cloud-init를 사용하여 자동화할 수도 있으며 여기에 대해서는 [이후의 자습서](./tutorial-automate-vm-deployment.md)에서 다룹니다.

### <a name="manual-configuration"></a>수동 구성

Hello 가상 컴퓨터와 SSH 연결을 만듭니다. Hello hello 가상 컴퓨터의 공용 IP로 hello 예제 IP 주소를 대체 합니다.

```azurecli-interactive 
ssh 52.174.34.95
```

파티션에 hello 디스크 `fdisk`합니다.

```bash
(echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
```

Hello를 사용 하 여 파일 시스템 toohello 파티션을 작성 `mkfs` 명령입니다.

```bash
sudo mkfs -t ext4 /dev/sdc1
```

Hello 운영 체제에 액세스할 수 있도록 hello 새 디스크를 탑재 합니다.

```bash
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
```

hello를 통해 이제 hello 디스크에 액세스할 수 *datadrive* hello를 실행 하 여 확인할 수 있는 탑재 지점, `df -h` 명령입니다. 

```bash
df -h
```

hello 출력과 hello 새 드라이브에 탑재 된 */datadrive*합니다.

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G  1.4G   28G   5% /
/dev/sdb1       6.8G   16M  6.4G   1% /mnt
/dev/sdc1        50G   52M   47G   1% /datadrive
```

다시 부팅 한 후 다시 탑재 될 드라이브 hello tooensure, toohello 추가 해야 */등/fstab* 파일입니다. toodo hello로 hello hello 디스크의 UUID를 따라서가 `blkid` 유틸리티입니다.

```bash
sudo -i blkid
```

hello hello 드라이브의 UUID를 표시 하는 hello 출력 `/dev/sdc1` 이 경우.

```bash
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

Toohello 다음 줄 비슷한 toohello 추가 */등/fstab* 파일입니다. *barrier=0*을 사용하여 쓰기 장벽을 사용하지 않도록 설정할 수 있으며 이 구성으로 디스크 성능이 향상될 수 있습니다. 

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive  ext4    defaults,nofail,barrier=0   1  2
```

Hello 디스크에 구성 된 했으므로 hello SSH 세션을 닫습니다.

```bash
exit
```

## <a name="resize-vm-disk"></a>VM 디스크 크기 조정

VM이 배포 된 후 모든 연결 된 데이터 디스크 또는 hello 운영 체제 디스크 크기가 증가할 수 있습니다. 더 많은 저장 공간이 또는 더 높은 수준의 성능 (P10, P20, P30) 확장이 필요할 때 디스크의 hello 크기 증가 하는 것이 좋습니다. 디스크 크기를 줄일 수는 없습니다.

디스크 크기를 증가 하기 전에 Id hello 또는 hello 디스크의 이름이 필요 합니다. 사용 하 여 hello [az 디스크 목록](/cli/azure/vm/disk#list) 명령 tooreturn 모든 리소스 그룹의 디스크입니다. Hello 디스크 이름을 기록해 싶다는 의사를 tooresize 합니다.

```azurecli-interactive 
az disk list -g myResourceGroupDisk --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table
```

hello VM 할당이 해제 해야 합니다. 사용 하 여 hello [az vm 할당을 취소]( /cli/azure/vm#deallocate) toostop 명령 및 hello VM 할당을 취소 합니다.

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupDisk --name myVM
```

사용 하 여 hello [az 디스크 업데이트](/cli/azure/vm/disk#update) 명령 tooresize hello 디스크. 이 예제에서는 명명 된 디스크의 크기를 조정 *myDataDisk* too1 테라바이트 합니다.

```azurecli-interactive 
az disk update --name myDataDisk --resource-group myResourceGroupDisk --size-gb 1023
```

Hello 크기 조정 작업이 완료 되 면 hello VM을 시작 합니다.

```azurecli-interactive 
az vm start --resource-group myResourceGroupDisk --name myVM
```

Hello 운영 체제 디스크 크기를 조정 했습니다 hello 파티션이 자동으로 확장 됩니다. 현재 파티션에서 데이터 디스크 크기를 조정 했습니다 하면 toobe hello Vm 운영 체제에서 확장입니다.

## <a name="snapshot-azure-disks"></a>스냅숏 Azure 디스크

디스크 스냅숏을 만드는 hello 디스크의 읽기 전용, 지정 시간 복사본을 만듭니다. Azure VM 스냅숏은 구성을 변경 하기 전에 VM의 hello 상태를 신속 하 게 저장 하는 데 유용 합니다. Hello 이벤트에서 hello 구성 변경 내용을 증명 toobe 의도 하지 않은, hello 스냅숏을 사용 하 여 VM 상태를 복원할 수 있습니다. Hello와 독립적으로 각 디스크의 스냅숏을 VM에 하나 이상의 디스크가 있는 경우 다른 사용자입니다. 응용 프로그램 일치 백업을 만들도록, 디스크에 대 한 스냅숏을 하기 전에 hello VM을 중지 하는 것이 좋습니다. 또는 hello를 사용 하 여 [Azure 백업 서비스](/azure/backup/), 있습니다 tooperform 자동 백업 중 VM이 실행 되 고 hello 사용 합니다.

### <a name="create-snapshot"></a>스냅숏 만들기

가상 컴퓨터 디스크 스냅숏을 만들기 전에 hello Id 또는 hello 디스크의 이름이 필요 합니다. 사용 하 여 hello [az vm 표시](https://docs.microsoft.com/en-us/cli/azure/vm#show) 명령 tooreturn hello 디스크 id입니다. 이 예제에서는 hello 디스크 id는 이후 단계에서 사용할 수 있도록 변수에 저장 됩니다.

```azurecli-interactive 
osdiskid=$(az vm show -g myResourceGroupDisk -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```

Hello 가상 컴퓨터 디스크의 hello id를가지고 hello 다음 명령은 hello 디스크의 스냅숏을 합니다.

```azurcli
az snapshot create -g myResourceGroupDisk --source "$osdiskid" --name osDisk-backup
```

### <a name="create-disk-from-snapshot"></a>스냅숏에서 디스크 만들기

이 스냅숏은 사용 하는 toorecreate hello 가상 컴퓨터 하나일 수 있습니다를 디스크에 다음 변환할 수 있습니다.

```azurecli-interactive 
az disk create --resource-group myResourceGroupDisk --name mySnapshotDisk --source osDisk-backup
```

### <a name="restore-virtual-machine-from-snapshot"></a>스냅숏에서 가상 컴퓨터 복원

delete hello 기존 가상 컴퓨터 toodemonstrate 가상 컴퓨터 복구 합니다. 

```azurecli-interactive 
az vm delete --resource-group myResourceGroupDisk --name myVM
```

Hello 스냅숏 디스크에서 새 가상 컴퓨터를 만듭니다.

```azurecli-interactive 
az vm create --resource-group myResourceGroupDisk --name myVM --attach-os-disk mySnapshotDisk --os-type linux
```

### <a name="reattach-data-disk"></a>데이터 디스크 다시 연결

모든 데이터 디스크를 다시 연결 toobe toohello 가상 컴퓨터 필요 합니다.

먼저 hello를 사용 하 여 hello 데이터 디스크 이름의 찾을 [az 디스크 목록](https://docs.microsoft.com/cli/azure/disk#list) 명령입니다. 이 예에서는 위치 hello 라는 변수에 hello 디스크의 이름을 *datadisk*, hello 다음 단계에서 사용 되는 합니다.

```azurecli-interactive 
datadisk=$(az disk list -g myResourceGroupDisk --query "[?contains(name,'myVM')].[name]" -o tsv)
```

사용 하 여 hello [az vm 디스크를 연결](https://docs.microsoft.com/cli/azure/vm/disk#attach) 명령 tooattach hello 디스크.

```azurecli-interactive 
az vm disk attach –g myResourceGroupDisk –-vm-name myVM –-disk $datadisk
```

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음과 같은 VM 디스크 항목에 대해 알아보았습니다.

> [!div class="checklist"]
> * OS 디스크 및 임시 디스크
> * 데이터 디스크
> * 표준 및 프리미엄 디스크
> * 디스크 성능
> * 데이터 디스크 연결 및 준비
> * 디스크 크기 조정
> * 디스크 스냅숏

VM 구성을 자동화 하는 방법에 대 한 다음 자습서 toolearn toohello를 진행 합니다.

> [!div class="nextstepaction"]
> [VM 구성 자동화](./tutorial-automate-vm-deployment.md)
