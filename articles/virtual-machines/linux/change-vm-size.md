---
title: "aaaHow tooresize hello Azure CLI 2.0을 사용 하 여 Linux VM | Microsoft Docs"
description: "어떻게를 tooscale 또는 비율을 변경 하 여 Linux 가상 컴퓨터를 hello VM 크기입니다."
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: e163f878-b919-45c5-9f5a-75a64f3b14a0
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2017
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e8fba485b5bcc7824f546de5cf3df77624a28008
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-virtual-machine-using-cli-20"></a>CLI 2.0을 사용하여 Linux 가상 컴퓨터 크기 조정

가상 컴퓨터 (VM)를 프로 비전 한 후 확장할 수 있습니다 hello VM 위로 또는 아래로 hello를 변경 하 여 [VM 크기][vm-sizes]합니다. 경우에 따라 할당을 취소 해야 hello VM 먼저 합니다. Hello hello VM을 호스팅하는 hello 하드웨어 클러스터에 사용할 수 없는 크기 원하는 toodeallocate hello VM 필요 합니다. 이 문서를 사용 하 여 Linux VM tooresize Azure CLI 2.0 hello 하는 방법을 자세히 설명 합니다. Hello로 다음이 단계를 수행할 수도 있습니다 [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

## <a name="resize-a-vm"></a>VM 크기 조정
VM tooresize 필요한 hello 최신 [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치 하 고 사용 하 여 Azure 계정 tooan [az 로그인](/cli/azure/#login)합니다.

1. Hello 하드웨어 클러스터 VM hello로 호스트 되는 위치에서 사용 가능한 VM hello 목록 보기의 크기를 조정 [az vm 목록-vm-크기 조정-옵션](/cli/azure/vm#list-vm-resize-options)합니다. hello 다음 예에서는 나열 hello 라는 VM에 대 한 VM 크기 `myVM` hello 리소스 그룹에 `myResourceGroup` 영역:
   
    ```azurecli
    az vm list-vm-resize-options --resource-group myResourceGroup --name myVM --output table
    ```

2. VM 크기 나열 된 hello 필요한 경우 크기 조정의 VM hello [az vm 크기를 조정](/cli/azure/vm#resize)합니다. 다음 예제에서는 크기가 조정 되어 hello hello 라는 VM `myVM` toohello `Standard_DS3_v2` 크기:
   
    ```azurecli
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    ```
   
    이 프로세스 동안 hello VM 다시 시작합니다. Hello 다시 시작한 후 기존 OS 및 데이터 디스크는 다시 매핑됩니다. Hello 임시 디스크에 있는 모든 내용을 손실 됩니다.

3. Toofirst hello VM 크기 나열 되지 않으면 원하는 경우 해야 할당을 취소의 VM hello [az vm 할당을 취소](/cli/azure/vm#deallocate)합니다. 이 프로세스 영역에서는 hello 및 후에 시작 하는 크기가 조정 된 tooany 크기로 사용할 수 있는 hello VM toothen을 수 있습니다. hello 다음 단계 할당 해제, 크기 조정 및 다음 hello 라는 VM을 시작 `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`:
   
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    az vm start --resource-group myResourceGroup --name myVM
    ```
   
   > [!WARNING]
   > 또한 할당 해제 hello VM toohello VM을 할당 하는 동적 IP 주소를 해제 합니다. hello OS 및 데이터 디스크 영향을 받지 않습니다.

## <a name="next-steps"></a>다음 단계
확장성을 높이기 위해서는 여러 VM 인스턴스를 실행하고 규모를 확장합니다. 자세한 내용은 [가상 컴퓨터 확장 집합에서 Linux 컴퓨터 자동 확장][scale-set]을 참조하세요. 

<!-- links -->
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
