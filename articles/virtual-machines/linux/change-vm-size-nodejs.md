---
title: "aaaHow tooresize hello Azure CLI 1.0을 사용 하 여 Linux VM | Microsoft Docs"
description: "어떻게를 tooscale 또는 비율을 변경 하 여 Linux 가상 컴퓨터를 hello VM 크기입니다."
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/16/2016
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 43dd955dc2f2dd9d1b2da07ecbfbf2459bcaa4d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-vm-with-azure-cli-10"></a>Azure CLI 1.0을 사용하여 Linux VM의 크기 조정

## <a name="overview"></a>개요

가상 컴퓨터 (VM)를 프로 비전 한 후 확장할 수 있습니다 hello VM 위로 또는 아래로 hello를 변경 하 여 [VM 크기][vm-sizes]합니다. 경우에 따라 할당을 취소 해야 hello VM 먼저 합니다. 이 새 크기 hello hello VM을 호스팅하는 hello 하드웨어 클러스터에 사용할 수 없는 경우 발생할 수 있습니다.

이 문서에서는 어떻게 hello를 사용 하 여 Linux VM a tooresize [Azure CLI][azure-cli]합니다.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a>CLI 버전 toocomplete hello 작업
Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.

- [Azure CLI 1.0](#resize-a-linux-vm) – 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)
- [Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한


## <a name="resize-a-linux-vm"></a>Linux VM 크기 조정
VM을 tooresize hello 다음 단계를 수행 합니다.

1. Hello 다음 CLI 명령을 실행 합니다. 이 명령은 hello VM 호스팅되는 hello 하드웨어 클러스터에서 사용할 수 있는 hello VM 크기를 나열 합니다.
   
    ```azurecli
    azure vm sizes -g myResourceGroup --vm-name myVM
    ```
2. Hello 원하는 크기 나열 된 경우 다음 명령을 tooresize hello VM hello를 실행 합니다.
   
    ```azurecli
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM  \
        --enable-boot-diagnostics
        --boot-diagnostics-storage-uri https://mystorageaccount.blob.core.windows.net/ 
    ```
   
    이 프로세스 동안 hello VM 다시 시작 됩니다. Hello 다시 시작한 후 기존 OS 및 데이터 디스크 다시 매핑됩니다. Hello 임시 디스크에 있는 모든 내용을 손실 됩니다.
   
    사용 하 여 hello `--enable-boot-diagnostics` 옵션을 사용 하면 [진단 부팅][boot-diagnostics], toolog 모든 오류 관련된 toostartup 합니다.
3. 그렇지 않으면 hello 크기 나열 되지 않으면 원하는 경우 hello 다음 명령을 toodeallocate hello VM 크기를 변경 하 고 hello VM을 다시 실행 합니다.
   
    ```azurecli
    azure vm deallocate -g myResourceGroup myVM
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM \
        --enable-boot-diagnostics --boot-diagnostics-storage-uri \
        https://mystorageaccount.blob.core.windows.net/ 
    azure vm start -g myResourceGroup myVM
    ```
   
   > [!WARNING]
   > 또한 할당 해제 hello VM toohello VM을 할당 하는 동적 IP 주소를 해제 합니다. hello OS 및 데이터 디스크 영향을 받지 않습니다.
   > 
   > 

## <a name="next-steps"></a>다음 단계
확장성을 높이기 위해서는 여러 VM 인스턴스를 실행하고 규모를 확장합니다. 자세한 내용은 [가상 컴퓨터 확장 집합에서 Linux 컴퓨터 자동 확장][scale-set]을 참조하세요. 

<!-- links -->

[azure-cli]:../../cli-install-nodejs.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
