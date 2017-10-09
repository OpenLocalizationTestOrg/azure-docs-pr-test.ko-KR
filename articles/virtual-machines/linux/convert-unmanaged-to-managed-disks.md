---
title: "Azure에서 Linux 가상 컴퓨터를 관리 되지 않는 aaaConvert toomanaged 디스크-Azure 관리 되는 디스크 디스크 | Microsoft Docs"
description: "Linux VM에서 관리 되지 않는 디스크 toomanaged tooconvert hello 리소스 관리자 배포 모델에서 Azure CLI 2.0을 사용 하 여 디스크 방법"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 1b94da11deab46f344e28ab4491cf220506b6347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a>관리 되지 않는 디스크 toomanaged 디스크에서 Linux 가상 컴퓨터 변환

기존 Linux 가상 컴퓨터 (Vm) 관리 되지 않는 디스크를 사용 하는 경우 hello 통해 hello Vm toouse 관리 되는 디스크를 변환할 수 있습니다 [Azure 관리 되는 디스크](../windows/managed-disks-overview.md) 서비스입니다. 이 프로세스는 hello OS 디스크 및 연결 된 데이터 디스크를 모두 변환합니다.

이 문서를 사용 하 여 Vm tooconvert Azure CLI hello 하는 방법을 보여 줍니다. Tooinstall 필요 하거나 업그레이드할 참조 [Azure CLI 2.0 설치](/cli/azure/install-azure-cli)합니다. 

## <a name="before-you-begin"></a>시작하기 전에

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a>단일 인스턴스 VM 변환
이 섹션에서는 tooconvert 단일 인스턴스 Azure Vm에서 관리 되지 않는 toomanaged 디스크 디스크 하는 방법을 설명 합니다. (Vm 가용성 집합에 있는 경우 hello 다음 섹션 참조 합니다.) 이 프로세스 tooconvert hello Vm (HDD) 표준 또는 프리미엄 (SSD) 관리 되지 않는 디스크 toopremium 관리 되는 디스크에서 관리 되지 않는 디스크 toostandard 관리 되는 디스크를 사용할 수 있습니다.

1. VM hello를 사용 하 여 할당 취소 [az vm 할당을 취소](/cli/azure/vm#deallocate)합니다. hello 다음 예제에서는 할당 취소 hello 라는 VM `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. 사용 하 여 hello VM toomanaged 디스크 변환 [az vm 변환](/cli/azure/vm#convert)합니다. 변환 프로세스를 수행 하는 hello hello 라는 VM `myVM`hello OS 디스크 및 모든 데이터 디스크를 포함 하 여:

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. 사용 하 여 hello 변환 toomanaged 디스크 후 hello VM 시작 [az vm 시작](/cli/azure/vm#start)합니다. 다음 예에서는 시작 하는 hello hello 라는 VM `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`합니다.

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a>가용성 집합의 VM 변환

경우 tooconvert toomanaged 디스크 가용성 집합에는 원하는 hello Vm을 먼저 tooconvert hello 가용성 집합 tooa 관리 되는 가용성 집합입니다.

Hello 가용성 집합을 변환 하기 전에 hello 가용성 집합에 있는 모든 Vm은 해제 해야 합니다. 모든 Vm toomanaged 디스크 hello 공급 후 자체적으로 설정 하는 계획 tooconvert 가용성 집합 관리 되는 변환 된 tooa 되었습니다. 그런 다음, 모든 hello Vm을 시작 하 고 계속 정상적으로 작동 합니다.

1. [az vm availability-set list](/cli/azure/vm/availability-set#list)를 사용하여 가용성 집합의 모든 VM을 나열합니다. hello 다음 예에서는 나열 모든 Vm hello 가용성 명명 된 집합의 `myAvailabilitySet` 이라는 hello 리소스 그룹에 `myResourceGroup`:

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. 사용 하 여 모든 hello Vm 할당을 취소 [az vm 할당을 취소](/cli/azure/vm#deallocate)합니다. hello 다음 예제에서는 할당 취소 hello 라는 VM `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. 사용 하 여 설정 하는 hello 가용성 변환 [az vm 가용성 집합 convert](/cli/azure/vm/availability-set#convert)합니다. hello 다음 예제에서는 변환 hello 가용성 명명 된 집합 `myAvailabilitySet` 이라는 hello 리소스 그룹에 `myResourceGroup`:

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. 사용 하 여 모든 hello Vm toomanaged 디스크 변환 [az vm 변환](/cli/azure/vm#convert)합니다. 변환 프로세스를 수행 하는 hello hello 라는 VM `myVM`hello OS 디스크 및 모든 데이터 디스크를 포함 하 여:

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. 사용 하 여 hello 변환 toomanaged 디스크 후 모든 hello Vm 시작 [az vm 시작](/cli/azure/vm#start)합니다. 다음 예에서는 시작 하는 hello hello 라는 VM `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`:

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a>다음 단계
저장소 옵션에 대한 자세한 내용은 [Azure Managed Disks 개요](../windows/managed-disks-overview.md)를 참조하세요.
