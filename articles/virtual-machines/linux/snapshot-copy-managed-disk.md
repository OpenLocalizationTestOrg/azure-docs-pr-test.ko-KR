---
title: "백업에는 Azure 관리 되는 디스크 aaaCopy | Microsoft Docs"
description: "위쪽 또는 문제 해결을 다시 디스크는 Azure 관리 되는 디스크 toouse의 복사본을 발급 하는 toocreate 방법에 대해 알아봅니다."
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 2/6/2017
ms.author: rasquill
ms.openlocfilehash: 41b91c2d68eb5be9c493a66be5f7d085a70450d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a>관리 스냅숏을 사용하여 Azure Managed Disk로 저장된 VHD 복사본 만들기
백업에 대 한 관리 되는 디스크의 스냅숏을 또는 hello 스냅숏에서 관리 되는 디스크를 만들어 tooa 테스트 가상 컴퓨터 tootroubleshoot를 연결 합니다. 관리 스냅숏은 VM Managed Disk의 특정 시점 전체 복사본입니다. VHD의 읽기 전용 복사본을 만들어서 기본적으로 표준 관리 디스크로 저장합니다. 

가격 책정에 대한 자세한 내용은 [Azure Storage 가격 책정](https://azure.microsoft.com/pricing/details/managed-disks/)을 참조하세요. <!--Add link tootopic or blog post that explains managed disks. -->

Azure 포털 또는 hello Azure CLI 2.0 tootake 어느 hello hello 관리 되는 디스크의 스냅숏을 사용 합니다.

## <a name="use-azure-cli-20-tootake-a-snapshot"></a>Azure CLI 2.0 tootake 스냅숏을 사용 하 여

> [!NOTE] 
> hello 다음 예제에서는 hello Azure CLI 2.0 설치 하 고 Azure 계정에 로그인 합니다.

hello 다음 단계 표시 방법을 tooobtain 및 관리 되는 운영 체제에 대 한 스냅숏을 사용 하 여 디스크로 hello `az snapshot create` hello로 명령을 `--source-disk` 매개 변수입니다. hello 다음 예제에서는 라고 가정 라는 VM `myVM` hello에서 관리 되는 운영 체제 디스크를 사용 하 여 만든 `myResourceGroup` 리소스 그룹입니다.

```azure-cli
# take hello disk id with which toocreate a snapshot
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create -g myResourceGroup --source "$osDiskId" --name osDisk-backup
```

hello 출력에는 다음과 같이 표시 됩니다.

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Copy",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/disks/osdisk_6NexYgkFQU",
    "storageAccountId": null
  },
  "diskSizeGb": 30,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/snapshots/osDisk-backup",
  "location": "westus",
  "name": "osDisk-backup",
  "osType": "Linux",
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-06T21:27:10.172980+00:00",
  "type": "Microsoft.Compute/snapshots"
}
```

## <a name="use-azure-portal-tootake-a-snapshot"></a>Azure 포털 tootake 스냅숏을 사용 하 여 

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. 클릭 하 여 hello 왼쪽 위 년부터 **새로** 검색 한 **스냅숏**합니다.
3. Hello 스냅숏 블레이드에서 클릭 **만들기**합니다.
4. 입력 한 **이름** hello 스냅숏에 대 한 합니다.
5. 기존 선택 [리소스 그룹](../../azure-resource-manager/resource-group-overview.md#resource-groups) 또는 새 유형 hello 이름입니다. 
6. Azure 데이터 센터 위치를 선택합니다.  
7. 에 대 한 **원본 디스크**, 선택 hello toosnapshot 디스크 관리.
8. 선택 hello **계정 유형** toouse toostore hello 스냅숏 합니다. 고성능 디스크에 저장할 필요가 없다면 **Standard_LRS**를 권장합니다.
9. **만들기**를 클릭합니다.

Hello 매개 변수를 사용 하 여 관리 되는 디스크 toouse hello 스냅숏 toocreate를 계획 하 고 toobe 높은 수행 해야 하는 VM을 연결 하는 경우 `--sku Premium_LRS` hello로 `az snapshot create` 명령입니다. 그러면 프리미엄 관리 되는 디스크에 저장 되도록 hello 스냅숏이 만들어집니다. 프리미엄 Managed Disks는 SSD(반도체 드라이브)이기 때문에 성능이 우수하지만 표준 디스크(HDD)보다 가격이 비쌉니다.


