---
title: "Azure Linux VM에서 데이터 디스크 aaaDetach | Microsoft Docs"
description: "Toodetach CLI 2.0 또는 hello Azure 포털을 사용 하 여 Azure에서 가상 컴퓨터에서 데이터 디스크에 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: azurecli
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: 1c6145fc97f13179457225e93e0fb7adc261a65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-linux-virtual-machine"></a>Linux 가상 컴퓨터에서 toodetach 데이터 디스크 하는 방법

연결 된 tooa 가상 컴퓨터가 있는 데이터 디스크를 더 이상 해야 하는 경우 쉽게 분리할 수 없습니다. 이 hello 디스크 hello 가상 컴퓨터에서 제거 하지만 저장소에서 제거 되지 않습니다. 

> [!WARNING]
> 디스크를 분리해도 자동으로 삭제되지 않습니다. TooPremium 저장소를 구독 하는 경우에 hello 디스크에 대 한 저장소 비용은 tooincur 계속 됩니다. 자세한 내용은 참조 너무[가격 및 프리미엄 저장소를 사용 하는 경우 청구](../../storage/common/storage-premium-storage.md#pricing-and-billing)합니다. 
> 
> 

Hello toouse hello 디스크에 기존 데이터를 다시 선택 하면 다시 연결할 수 toohello 동일한 가상 컴퓨터 이거나 다른 컴퓨터입니다.  

## <a name="detach-a-data-disk-using-cli-20"></a>CLI 2.0을 사용하여 데이터 디스크 분리

```azurecli
az vm disk detach -g myResourceGroup --vm-name myVm -n myDataDisk
```

hello 디스크 저장소에 남아 있지만 더 이상 연결 된 tooa 가상 컴퓨터.


## <a name="detach-a-data-disk-using-hello-portal"></a>Hello 포털을 사용 하 여 데이터 디스크를 분리
1. Hello 포털 허브에서 선택 **가상 컴퓨터**합니다.
2. Hello 가상 컴퓨터를 누르고 원하는 toodetach hello 데이터 디스크 선택 **중지** toodeallocate hello VM입니다.
3. Hello 가상 컴퓨터 블레이드 선택 **디스크**합니다.
4. Hello의 hello 위쪽 **디스크** 블레이드를 **편집**합니다.
5. Hello에 **디스크** 블레이드에서 toohello 싶다는 의사를 toodetach, hello 데이터 디스크의 맨 오른쪽 클릭 hello ![분리 단추 이미지](./media/detach-disk/detach.png) 단추를 분리 합니다.
5. Hello 디스크를 제거한 후 hello 블레이드 맨 hello에서 저장을 클릭 합니다.
6. Hello 가상 컴퓨터 블레이드 클릭 **개요** hello를 클릭 한 다음 **시작** hello 블레이드 toorestart hello VM hello 위쪽에 단추입니다.

hello 디스크 저장소에 남아 있지만 더 이상 연결 된 tooa 가상 컴퓨터.








## <a name="next-steps"></a>다음 단계
Tooreuse hello 데이터 디스크를 사용 하도록 하려는 경우 수 방금 [tooanother VM 연결](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

