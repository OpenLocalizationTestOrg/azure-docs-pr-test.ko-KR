---
title: "백업용 Azure 관리 디스크 복사 | Microsoft Docs"
description: "백업 또는 디스크 문제 해결에 사용할 수 있는 Azure 관리 디스크의 복사본을 만드는 방법을 알아봅니다."
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
ms.openlocfilehash: c91367ef11c9d531bebac7c069d2df586607ec29
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="940b0-103">관리 스냅숏을 사용하여 Azure 관리 디스크로 저장된 VHD 복사본 만들기</span><span class="sxs-lookup"><span data-stu-id="940b0-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="940b0-104">백업용 관리 디스크의 스냅숏을 만들거나 스냅숏으로 관리 디스크를 만들고 테스트 가상 컴퓨터에 연결하여 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="940b0-104">Take a snapshot of a Managed disk for backup or create a Managed Disk from the snapshot and attach it to a test virtual machine to troubleshoot.</span></span> <span data-ttu-id="940b0-105">관리 스냅숏은 VM 관리 디스크의 완전한 특정 시점 복사본입니다.</span><span class="sxs-lookup"><span data-stu-id="940b0-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="940b0-106">VHD의 읽기 전용 복사본을 만들어서 기본적으로 표준 관리 디스크로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="940b0-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> 

<span data-ttu-id="940b0-107">가격 책정에 대한 자세한 내용은 [Azure Storage 가격 책정](https://azure.microsoft.com/pricing/details/managed-disks/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="940b0-107">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> <!--Add link to topic or blog post that explains managed disks. -->

<span data-ttu-id="940b0-108">Azure Portal 또는 Azure CLI 2.0을 사용하여 Managed Disk 스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="940b0-108">Use either the Azure portal or the Azure CLI 2.0 to take a snapshot of the Managed Disk.</span></span>

## <a name="use-azure-cli-20-to-take-a-snapshot"></a><span data-ttu-id="940b0-109">Azure CLI 2.0을 사용하여 스냅숏 만들기</span><span class="sxs-lookup"><span data-stu-id="940b0-109">Use Azure CLI 2.0 to take a snapshot</span></span>

> [!NOTE] 
> <span data-ttu-id="940b0-110">다음 예제는 Azure CLI 2.0을 설치하고 Azure 계정에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="940b0-110">The following example requires the Azure CLI 2.0 installed and logged into your Azure account.</span></span>

<span data-ttu-id="940b0-111">다음 단계에서는 `az snapshot create` 명령과 `--source-disk` 매개 변수를 사용하여 관리 OS 디스크의 스냅숏을 가져오고 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="940b0-111">The following steps show how to obtain and take a snapshot of a managed OS disk using the `az snapshot create` command with the `--source-disk` parameter.</span></span> <span data-ttu-id="940b0-112">다음 예제는 `myResourceGroup` 리소스 그룹의 관리 OS 디스크로 만든 `myVM`이라는 VM이 있는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="940b0-112">The following example assumes that there is a VM called `myVM` created with a managed OS disk in the `myResourceGroup` resource group.</span></span>

```azure-cli
# take the disk id with which to create a snapshot
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create -g myResourceGroup --source "$osDiskId" --name osDisk-backup
```

<span data-ttu-id="940b0-113">다음과 비슷하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="940b0-113">The output should look something like:</span></span>

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

## <a name="use-azure-portal-to-take-a-snapshot"></a><span data-ttu-id="940b0-114">Azure Portal을 사용하여 스냅숏 만들기</span><span class="sxs-lookup"><span data-stu-id="940b0-114">Use Azure portal to take a snapshot</span></span> 

1. <span data-ttu-id="940b0-115">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="940b0-115">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="940b0-116">왼쪽 위에서 **새로 만들기**를 클릭하고 **스냅숏**을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="940b0-116">Starting in the upper-left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="940b0-117">스냅숏 블레이드에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="940b0-117">In the Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="940b0-118">스냅숏의 **이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="940b0-118">Enter a **Name** for the snapshot.</span></span>
5. <span data-ttu-id="940b0-119">기존 [리소스 그룹](../../azure-resource-manager/resource-group-overview.md#resource-groups)을 선택하거나 새 리소스 그룹의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="940b0-119">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type the name for a new one.</span></span> 
6. <span data-ttu-id="940b0-120">Azure 데이터 센터 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="940b0-120">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="940b0-121">**원본 디스크**에서 스냅숏을 만들 Managed Disk를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="940b0-121">For **Source disk**, select the Managed Disk to snapshot.</span></span>
8. <span data-ttu-id="940b0-122">스냅숏 저장에 사용할 **계정 유형**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="940b0-122">Select the **Account type** to use to store the snapshot.</span></span> <span data-ttu-id="940b0-123">고성능 디스크에 저장할 필요가 없다면 **Standard_LRS**를 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="940b0-123">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="940b0-124">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="940b0-124">Click **Create**.</span></span>

<span data-ttu-id="940b0-125">스냅숏을 사용하여 관리 디스크를 만들고 고성능이 필요한 VM에 스냅숏을 연결하려는 경우 `--sku Premium_LRS` 매개 변수와 `az snapshot create` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="940b0-125">If you plan to use the snapshot to create a Managed Disk and attach it a VM that needs to be high performing, use the parameter `--sku Premium_LRS` with the `az snapshot create` command.</span></span> <span data-ttu-id="940b0-126">그러면 프리미엄 관리 디스크로 저장되는 스냅숏이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="940b0-126">This creates the snapshot so that it is stored as a Premium Managed Disk.</span></span> <span data-ttu-id="940b0-127">프리미엄 Managed Disks는 SSD(반도체 드라이브)이기 때문에 성능이 우수하지만 표준 디스크(HDD)보다 가격이 비쌉니다.</span><span class="sxs-lookup"><span data-stu-id="940b0-127">Premium Managed Disks perform better because they are solid-state drives (SSDs), but cost more than Standard disks (HDDs).</span></span>


