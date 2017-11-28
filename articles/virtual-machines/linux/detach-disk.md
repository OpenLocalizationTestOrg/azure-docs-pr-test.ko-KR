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
# <a name="how-toodetach-a-data-disk-from-a-linux-virtual-machine"></a><span data-ttu-id="fad27-103">Linux 가상 컴퓨터에서 toodetach 데이터 디스크 하는 방법</span><span class="sxs-lookup"><span data-stu-id="fad27-103">How toodetach a data disk from a Linux virtual machine</span></span>

<span data-ttu-id="fad27-104">연결 된 tooa 가상 컴퓨터가 있는 데이터 디스크를 더 이상 해야 하는 경우 쉽게 분리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fad27-104">When you no longer need a data disk that's attached tooa virtual machine, you can easily detach it.</span></span> <span data-ttu-id="fad27-105">이 hello 디스크 hello 가상 컴퓨터에서 제거 하지만 저장소에서 제거 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fad27-105">This removes hello disk from hello virtual machine, but doesn't remove it from storage.</span></span> 

> [!WARNING]
> <span data-ttu-id="fad27-106">디스크를 분리해도 자동으로 삭제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fad27-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="fad27-107">TooPremium 저장소를 구독 하는 경우에 hello 디스크에 대 한 저장소 비용은 tooincur 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fad27-107">If you have subscribed tooPremium storage, you will continue tooincur storage charges for hello disk.</span></span> <span data-ttu-id="fad27-108">자세한 내용은 참조 너무[가격 및 프리미엄 저장소를 사용 하는 경우 청구](../../storage/common/storage-premium-storage.md#pricing-and-billing)합니다.</span><span class="sxs-lookup"><span data-stu-id="fad27-108">For more information refer too[Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span> 
> 
> 

<span data-ttu-id="fad27-109">Hello toouse hello 디스크에 기존 데이터를 다시 선택 하면 다시 연결할 수 toohello 동일한 가상 컴퓨터 이거나 다른 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="fad27-109">If you want toouse hello existing data on hello disk again, you can reattach it toohello same virtual machine, or another one.</span></span>  

## <a name="detach-a-data-disk-using-cli-20"></a><span data-ttu-id="fad27-110">CLI 2.0을 사용하여 데이터 디스크 분리</span><span class="sxs-lookup"><span data-stu-id="fad27-110">Detach a data disk using CLI 2.0</span></span>

```azurecli
az vm disk detach -g myResourceGroup --vm-name myVm -n myDataDisk
```

<span data-ttu-id="fad27-111">hello 디스크 저장소에 남아 있지만 더 이상 연결 된 tooa 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="fad27-111">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>


## <a name="detach-a-data-disk-using-hello-portal"></a><span data-ttu-id="fad27-112">Hello 포털을 사용 하 여 데이터 디스크를 분리</span><span class="sxs-lookup"><span data-stu-id="fad27-112">Detach a data disk using hello portal</span></span>
1. <span data-ttu-id="fad27-113">Hello 포털 허브에서 선택 **가상 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="fad27-113">In hello portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="fad27-114">Hello 가상 컴퓨터를 누르고 원하는 toodetach hello 데이터 디스크 선택 **중지** toodeallocate hello VM입니다.</span><span class="sxs-lookup"><span data-stu-id="fad27-114">Select hello virtual machine that has hello data disk you want toodetach and click **Stop** toodeallocate hello VM.</span></span>
3. <span data-ttu-id="fad27-115">Hello 가상 컴퓨터 블레이드 선택 **디스크**합니다.</span><span class="sxs-lookup"><span data-stu-id="fad27-115">In hello virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="fad27-116">Hello의 hello 위쪽 **디스크** 블레이드를 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="fad27-116">At hello top of hello **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="fad27-117">Hello에 **디스크** 블레이드에서 toohello 싶다는 의사를 toodetach, hello 데이터 디스크의 맨 오른쪽 클릭 hello ![분리 단추 이미지](./media/detach-disk/detach.png) 단추를 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad27-117">In hello **Disks** blade, toohello far right of hello data disk that you would like toodetach, click hello ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="fad27-118">Hello 디스크를 제거한 후 hello 블레이드 맨 hello에서 저장을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad27-118">After hello disk has been removed, click Save on hello top of hello blade.</span></span>
6. <span data-ttu-id="fad27-119">Hello 가상 컴퓨터 블레이드 클릭 **개요** hello를 클릭 한 다음 **시작** hello 블레이드 toorestart hello VM hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="fad27-119">In hello virtual machine blade, click **Overview** and then click hello **Start** button at hello top of hello blade toorestart hello VM.</span></span>

<span data-ttu-id="fad27-120">hello 디스크 저장소에 남아 있지만 더 이상 연결 된 tooa 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="fad27-120">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>








## <a name="next-steps"></a><span data-ttu-id="fad27-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fad27-121">Next steps</span></span>
<span data-ttu-id="fad27-122">Tooreuse hello 데이터 디스크를 사용 하도록 하려는 경우 수 방금 [tooanother VM 연결](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="fad27-122">If you want tooreuse hello data disk, you can just [attach it tooanother VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

