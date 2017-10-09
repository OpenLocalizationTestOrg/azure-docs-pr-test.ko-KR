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
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="a84b7-103">관리 스냅숏을 사용하여 Azure Managed Disk로 저장된 VHD 복사본 만들기</span><span class="sxs-lookup"><span data-stu-id="a84b7-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="a84b7-104">백업에 대 한 관리 되는 디스크의 스냅숏을 또는 hello 스냅숏에서 관리 되는 디스크를 만들어 tooa 테스트 가상 컴퓨터 tootroubleshoot를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a84b7-104">Take a snapshot of a Managed disk for backup or create a Managed Disk from hello snapshot and attach it tooa test virtual machine tootroubleshoot.</span></span> <span data-ttu-id="a84b7-105">관리 스냅숏은 VM Managed Disk의 특정 시점 전체 복사본입니다.</span><span class="sxs-lookup"><span data-stu-id="a84b7-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="a84b7-106">VHD의 읽기 전용 복사본을 만들어서 기본적으로 표준 관리 디스크로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a84b7-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> 

<span data-ttu-id="a84b7-107">가격 책정에 대한 자세한 내용은 [Azure Storage 가격 책정](https://azure.microsoft.com/pricing/details/managed-disks/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a84b7-107">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> <!--Add link tootopic or blog post that explains managed disks. -->

<span data-ttu-id="a84b7-108">Azure 포털 또는 hello Azure CLI 2.0 tootake 어느 hello hello 관리 되는 디스크의 스냅숏을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a84b7-108">Use either hello Azure portal or hello Azure CLI 2.0 tootake a snapshot of hello Managed Disk.</span></span>

## <a name="use-azure-cli-20-tootake-a-snapshot"></a><span data-ttu-id="a84b7-109">Azure CLI 2.0 tootake 스냅숏을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="a84b7-109">Use Azure CLI 2.0 tootake a snapshot</span></span>

> [!NOTE] 
> <span data-ttu-id="a84b7-110">hello 다음 예제에서는 hello Azure CLI 2.0 설치 하 고 Azure 계정에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a84b7-110">hello following example requires hello Azure CLI 2.0 installed and logged into your Azure account.</span></span>

<span data-ttu-id="a84b7-111">hello 다음 단계 표시 방법을 tooobtain 및 관리 되는 운영 체제에 대 한 스냅숏을 사용 하 여 디스크로 hello `az snapshot create` hello로 명령을 `--source-disk` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="a84b7-111">hello following steps show how tooobtain and take a snapshot of a managed OS disk using hello `az snapshot create` command with hello `--source-disk` parameter.</span></span> <span data-ttu-id="a84b7-112">hello 다음 예제에서는 라고 가정 라는 VM `myVM` hello에서 관리 되는 운영 체제 디스크를 사용 하 여 만든 `myResourceGroup` 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="a84b7-112">hello following example assumes that there is a VM called `myVM` created with a managed OS disk in hello `myResourceGroup` resource group.</span></span>

```azure-cli
# take hello disk id with which toocreate a snapshot
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create -g myResourceGroup --source "$osDiskId" --name osDisk-backup
```

<span data-ttu-id="a84b7-113">hello 출력에는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a84b7-113">hello output should look something like:</span></span>

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

## <a name="use-azure-portal-tootake-a-snapshot"></a><span data-ttu-id="a84b7-114">Azure 포털 tootake 스냅숏을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="a84b7-114">Use Azure portal tootake a snapshot</span></span> 

1. <span data-ttu-id="a84b7-115">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="a84b7-115">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a84b7-116">클릭 하 여 hello 왼쪽 위 년부터 **새로** 검색 한 **스냅숏**합니다.</span><span class="sxs-lookup"><span data-stu-id="a84b7-116">Starting in hello upper-left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="a84b7-117">Hello 스냅숏 블레이드에서 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="a84b7-117">In hello Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="a84b7-118">입력 한 **이름** hello 스냅숏에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a84b7-118">Enter a **Name** for hello snapshot.</span></span>
5. <span data-ttu-id="a84b7-119">기존 선택 [리소스 그룹](../../azure-resource-manager/resource-group-overview.md#resource-groups) 또는 새 유형 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a84b7-119">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span> 
6. <span data-ttu-id="a84b7-120">Azure 데이터 센터 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a84b7-120">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="a84b7-121">에 대 한 **원본 디스크**, 선택 hello toosnapshot 디스크 관리.</span><span class="sxs-lookup"><span data-stu-id="a84b7-121">For **Source disk**, select hello Managed Disk toosnapshot.</span></span>
8. <span data-ttu-id="a84b7-122">선택 hello **계정 유형** toouse toostore hello 스냅숏 합니다.</span><span class="sxs-lookup"><span data-stu-id="a84b7-122">Select hello **Account type** toouse toostore hello snapshot.</span></span> <span data-ttu-id="a84b7-123">고성능 디스크에 저장할 필요가 없다면 **Standard_LRS**를 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="a84b7-123">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="a84b7-124">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a84b7-124">Click **Create**.</span></span>

<span data-ttu-id="a84b7-125">Hello 매개 변수를 사용 하 여 관리 되는 디스크 toouse hello 스냅숏 toocreate를 계획 하 고 toobe 높은 수행 해야 하는 VM을 연결 하는 경우 `--sku Premium_LRS` hello로 `az snapshot create` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="a84b7-125">If you plan toouse hello snapshot toocreate a Managed Disk and attach it a VM that needs toobe high performing, use hello parameter `--sku Premium_LRS` with hello `az snapshot create` command.</span></span> <span data-ttu-id="a84b7-126">그러면 프리미엄 관리 되는 디스크에 저장 되도록 hello 스냅숏이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a84b7-126">This creates hello snapshot so that it is stored as a Premium Managed Disk.</span></span> <span data-ttu-id="a84b7-127">프리미엄 Managed Disks는 SSD(반도체 드라이브)이기 때문에 성능이 우수하지만 표준 디스크(HDD)보다 가격이 비쌉니다.</span><span class="sxs-lookup"><span data-stu-id="a84b7-127">Premium Managed Disks perform better because they are solid-state drives (SSDs), but cost more than Standard disks (HDDs).</span></span>


