---
title: "SQL Server VM에 대한 저장소 구성 | Microsoft Docs"
description: "이 항목에서는 Azure가 프로비전하는 동안 SQL Server VM에 대한 저장소를 구성하는 방법을 설명합니다(Resource Manager 배포 모델). 또한 기존 SQL Server VM에 대한 저장소를 구성하는 방법을 설명합니다."
services: virtual-machines-windows
documentationcenter: na
author: ninarn
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 169fc765-3269-48fa-83f1-9fe3e4e40947
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: ninarn
ms.openlocfilehash: f10bac1189c94a581487d19fc0cc129acec6a636
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="storage-configuration-for-sql-server-vms"></a><span data-ttu-id="3b1d9-104">SQL Server VM에 대한 저장소 구성</span><span class="sxs-lookup"><span data-stu-id="3b1d9-104">Storage configuration for SQL Server VMs</span></span>
<span data-ttu-id="3b1d9-105">Azure에서 SQL Server 가상 컴퓨터 이미지를 구성하는 경우 포털에서는 저장소 구성을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-105">When you configure a SQL Server virtual machine image in Azure, the Portal helps to automate your storage configuration.</span></span> <span data-ttu-id="3b1d9-106">저장소를 VM에 연결하고 해당 저장소를 SQL Server에 액세스할 수 있도록 하고 구성하여 특정 성능 요구 사항에 최적화하는 작업을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-106">This includes attaching storage to the VM, making that storage accessible to SQL Server, and configuring it to optimize for your specific performance requirements.</span></span>

<span data-ttu-id="3b1d9-107">이 항목에서는 Azure에서 프로비전 중 저장소 SQL Server VM 및 기존 VM에 대한 저장소를 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-107">This topic explains how Azure configures storage for your SQL Server VMs both during provisioning and for existing VMs.</span></span> <span data-ttu-id="3b1d9-108">이 구성은 SQL Server를 실행하는 Azure VM의 [성능 모범 사례](virtual-machines-windows-sql-performance.md) 에 기반합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-108">This configuration is based on the [performance best practices](virtual-machines-windows-sql-performance.md) for Azure VMs running SQL Server.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="3b1d9-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3b1d9-109">Prerequisites</span></span>
<span data-ttu-id="3b1d9-110">자동화된 저장소 구성 설정을 사용하려면 가상 컴퓨터에는 다음과 같은 특성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-110">To use the automated storage configuration settings, your virtual machine requires the following characteristics:</span></span>

* <span data-ttu-id="3b1d9-111">[SQL Server 갤러리 이미지](virtual-machines-windows-sql-server-iaas-overview.md#option-1-create-a-sql-vm-with-per-minute-licensing)로 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-111">Provisioned with a [SQL Server gallery image](virtual-machines-windows-sql-server-iaas-overview.md#option-1-create-a-sql-vm-with-per-minute-licensing).</span></span>
* <span data-ttu-id="3b1d9-112">[Resource Manager 배포 모델](../../../azure-resource-manager/resource-manager-deployment-model.md)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-112">Uses the [Resource Manager deployment model](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
* <span data-ttu-id="3b1d9-113">[프리미엄 저장소](../../../storage/common/storage-premium-storage.md)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-113">Uses [Premium Storage](../../../storage/common/storage-premium-storage.md).</span></span>

## <a name="new-vms"></a><span data-ttu-id="3b1d9-114">새 VM</span><span class="sxs-lookup"><span data-stu-id="3b1d9-114">New VMs</span></span>
<span data-ttu-id="3b1d9-115">다음 섹션에서는 새 SQL Server 가상 컴퓨터에 대한 저장소를 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-115">The following sections describe how to configure storage for new SQL Server virtual machines.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="3b1d9-116">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="3b1d9-116">Azure Portal</span></span>
<span data-ttu-id="3b1d9-117">SQL Server 갤러리 이미지를 사용하여 Azure VM을 프로비전할 경우 새 VM에 대한 저장소를 자동으로 구성하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-117">When provisioning an Azure VM using a SQL Server gallery image, you can choose to automatically configure the storage for your new VM.</span></span> <span data-ttu-id="3b1d9-118">저장소 크기, 성능 제한 및 워크로드 유형을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-118">You specify the storage size, performance limits, and workload type.</span></span> <span data-ttu-id="3b1d9-119">다음 스크린샷에서는 SQL VM을 프로비전하는 동안 사용된 저장소 구성 블레이드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-119">The following screenshot shows the Storage configuration blade used during SQL VM provisioning.</span></span>

![프로비전하는 동안 SQL Server VM 저장소 구성](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-provisioning.png)

<span data-ttu-id="3b1d9-121">선택을 기반으로 Azure는 VM을 만든 후에 다음과 같은 저장소 구성 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-121">Based on your choices, Azure performs the following storage configuration tasks after creating the VM:</span></span>

* <span data-ttu-id="3b1d9-122">프리미엄 저장소 데이터 디스크를 만들고 가상 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-122">Creates and attaches premium storage data disks to the virtual machine.</span></span>
* <span data-ttu-id="3b1d9-123">SQL Server에 액세스할 수 있도록 데이터 디스크를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-123">Configures the data disks to be accessible to SQL Server.</span></span>
* <span data-ttu-id="3b1d9-124">지정된 크기와 성능(IOPS 및 처리량) 요구 사항에 따라 저장소 풀에 데이터 디스크를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-124">Configures the data disks into a storage pool based on the specified size and performance (IOPS and throughput) requirements.</span></span>
* <span data-ttu-id="3b1d9-125">가상 컴퓨터에 새 드라이브와 저장소 풀을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-125">Associates the storage pool with a new drive on the virtual machine.</span></span>
* <span data-ttu-id="3b1d9-126">지정한 워크로드 유형(데이터 웨어하우징, 트랜잭션 처리 또는 일반)에 따라 새 드라이브를 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-126">Optimizes this new drive based on your specified workload type (Data warehousing, Transactional processing, or General).</span></span>

<span data-ttu-id="3b1d9-127">Azure에서 저장소 설정을 구성하는 방법에 대한 자세한 내용은 [저장소 구성 섹션](#storage-configuration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-127">For further details on how Azure configures storage settings, see the [Storage configuration section](#storage-configuration).</span></span> <span data-ttu-id="3b1d9-128">Azure 포털에서 SQL Server VM을 만드는 방법의 전체 연습은 [프로비전 자습서](virtual-machines-windows-portal-sql-server-provision.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-128">For a full walkthrough of how to create a SQL Server VM in the Azure Portal, see [the provisioning tutorial](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="resource-manage-templates"></a><span data-ttu-id="3b1d9-129">Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="3b1d9-129">Resource Manage templates</span></span>
<span data-ttu-id="3b1d9-130">다음 Resource Manager 템플릿을 사용하는 경우 두 개의 프리미엄 데이터 디스크는 저장소 풀 구성 없이 기본적으로 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-130">If you use the following Resource Manager templates, two premium data disks are attached by default, with no storage pool configuration.</span></span> <span data-ttu-id="3b1d9-131">그러나 이러한 템플릿을 사용자 지정하여 가상 컴퓨터에 연결된 프리미엄 데이터 디스크의 수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-131">However, you can customize these templates to change the number of premium data disks that are attached to the virtual machine.</span></span>

* [<span data-ttu-id="3b1d9-132">자동화된 백업을 사용하여 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="3b1d9-132">Create VM with Automated Backup</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-autobackup)
* [<span data-ttu-id="3b1d9-133">자동화된 패치를 사용하여 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="3b1d9-133">Create VM with Automated Patching</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-autopatching)
* [<span data-ttu-id="3b1d9-134">AKV 통합을 사용하여 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="3b1d9-134">Create VM with AKV Integration</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-keyvault)

## <a name="existing-vms"></a><span data-ttu-id="3b1d9-135">기존 VM</span><span class="sxs-lookup"><span data-stu-id="3b1d9-135">Existing VMs</span></span>
<span data-ttu-id="3b1d9-136">기존 SQL Server VM의 경우 Azure 포털에서 일부 저장소 설정을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-136">For existing SQL Server VMs, you can modify some storage settings in the Azure portal.</span></span> <span data-ttu-id="3b1d9-137">VM을 선택하고 설정 영역으로 이동하며 SQL Server 구성을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-137">Select your VM, go to the Settings area, and then select SQL Server Configuration.</span></span> <span data-ttu-id="3b1d9-138">SQL Server 구성 블레이드에서는 VM의 현재 저장소 사용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-138">The SQL Server Configuration blade shows the current storage usage of your VM.</span></span> <span data-ttu-id="3b1d9-139">VM에 있는 모든 드라이브는 이 차트에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-139">All drives that exist on your VM are displayed in this chart.</span></span> <span data-ttu-id="3b1d9-140">각 드라이브의 경우 저장 공간은 네 개의 섹션에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-140">For each drive, the storage space displays in four sections:</span></span>

* <span data-ttu-id="3b1d9-141">SQL 데이터</span><span class="sxs-lookup"><span data-stu-id="3b1d9-141">SQL data</span></span>
* <span data-ttu-id="3b1d9-142">SQL 로그</span><span class="sxs-lookup"><span data-stu-id="3b1d9-142">SQL log</span></span>
* <span data-ttu-id="3b1d9-143">기타(비 SQL 저장소)</span><span class="sxs-lookup"><span data-stu-id="3b1d9-143">Other (non-SQL storage)</span></span>
* <span data-ttu-id="3b1d9-144">사용 가능</span><span class="sxs-lookup"><span data-stu-id="3b1d9-144">Available</span></span>

![기존 SQL Server VM에 대한 저장소 구성](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-existing.png)

<span data-ttu-id="3b1d9-146">새 드라이브를 추가하거나 기존 드라이브를 확장하도록 저장소를 구성하려면 차트 위의 편집 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-146">To configure the storage to add a new drive or extend an existing drive, click the Edit link above the chart.</span></span>

<span data-ttu-id="3b1d9-147">표시된 구성 옵션은 전에 이 기능을 사용했는지 여부에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-147">The configuration options that you see varies depending on whether you have used this feature before.</span></span> <span data-ttu-id="3b1d9-148">처음으로 사용하는 경우 새 드라이브에 대한 저장소 요구 사항을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-148">When using for the first time, you can specify your storage requirements for a new drive.</span></span> <span data-ttu-id="3b1d9-149">이전에 이 기능을 사용하여 드라이브를 만든 경우 해당 드라이브의 저장소를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-149">If you previously used this feature to create a drive, you can choose to extend that drive’s storage.</span></span>

### <a name="use-for-the-first-time"></a><span data-ttu-id="3b1d9-150">처음으로 사용</span><span class="sxs-lookup"><span data-stu-id="3b1d9-150">Use for the first time</span></span>
<span data-ttu-id="3b1d9-151">이 기능을 처음으로 사용하는 경우 새 드라이브에 대한 저장소 크기와 성능 제한을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-151">If it is your first time using this feature, you can specify the storage size and performance limits for a new drive.</span></span> <span data-ttu-id="3b1d9-152">이러한 환경은 프로비전 시 표시되는 것과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-152">This experience is similar to what you would see at provisioning time.</span></span> <span data-ttu-id="3b1d9-153">주요 차이점은 워크로드 유형을 지정하도록 허용되지 않았다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-153">The main difference is that you are not permitted to specify the workload type.</span></span> <span data-ttu-id="3b1d9-154">이 제한은 가상 컴퓨터에서 기존 SQL Server 구성을 중단하지 않도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-154">This restriction prevents disrupting any existing SQL Server configurations on the virtual machine.</span></span>

![SQL Server 저장소 슬라이더 구성](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-usage-sliders.png)

<span data-ttu-id="3b1d9-156">Azure는 사양에 따라 새 드라이브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-156">Azure creates a new drive based on your specifications.</span></span> <span data-ttu-id="3b1d9-157">이 시나리오에서 Azure는 다음과 같은 저장소 구성 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-157">In this scenario, Azure performs the following storage configuration tasks:</span></span>

* <span data-ttu-id="3b1d9-158">프리미엄 저장소 데이터 디스크를 만들고 가상 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-158">Creates and attaches premium storage data disks to the virtual machine.</span></span>
* <span data-ttu-id="3b1d9-159">SQL Server에 액세스할 수 있도록 데이터 디스크를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-159">Configures the data disks to be accessible to SQL Server.</span></span>
* <span data-ttu-id="3b1d9-160">지정된 크기와 성능(IOPS 및 처리량) 요구 사항에 따라 저장소 풀에 데이터 디스크를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-160">Configures the data disks into a storage pool based on the specified size and performance (IOPS and throughput) requirements.</span></span>
* <span data-ttu-id="3b1d9-161">가상 컴퓨터에 새 드라이브와 저장소 풀을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-161">Associates the storage pool with a new drive on the virtual machine.</span></span>

<span data-ttu-id="3b1d9-162">Azure에서 저장소 설정을 구성하는 방법에 대한 자세한 내용은 [저장소 구성 섹션](#storage-configuration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-162">For further details on how Azure configures storage settings, see the [Storage configuration section](#storage-configuration).</span></span>

### <a name="add-a-new-drive"></a><span data-ttu-id="3b1d9-163">새 드라이브 추가</span><span class="sxs-lookup"><span data-stu-id="3b1d9-163">Add a new drive</span></span>
<span data-ttu-id="3b1d9-164">SQL Server VM에 이미 저장소를 구성한 경우 저장소를 확장하면 두 가지 새로운 옵션을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-164">If you have already configured storage on your SQL Server VM, expanding storage brings up two new options.</span></span> <span data-ttu-id="3b1d9-165">첫 번째는 새 드라이브를 추가하는 옵션으로 VM의 성능 수준을 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-165">The first option is to add a new drive, which can increase the performance level of your VM.</span></span>

![SQL VM에 새 드라이브 추가](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-add-new-drive.png)

<span data-ttu-id="3b1d9-167">그러나 드라이브를 추가한 후에 성능 향상을 달성하기 위해 몇 가지 추가 수동 구성을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-167">However, after adding the drive, you must perform some extra manual configuration to achieve the performance increase.</span></span>

### <a name="extend-the-drive"></a><span data-ttu-id="3b1d9-168">드라이브 확장</span><span class="sxs-lookup"><span data-stu-id="3b1d9-168">Extend the drive</span></span>
<span data-ttu-id="3b1d9-169">저장소 확장을 위한 다른 옵션은 기존 드라이브를 확장하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-169">The other option for expanding storage is to extend the existing drive.</span></span> <span data-ttu-id="3b1d9-170">이 옵션으로 사용자의 드라이브에 사용 가능한 저장소가 증가하지만 성능은 증가하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-170">This option increases the available storage for your drive, but it does not increase performance.</span></span> <span data-ttu-id="3b1d9-171">저장소 풀을 만든 후에 저장소 풀을 사용해서 열 수를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-171">With storage pools, you cannot alter the number of columns after the storage pool is created.</span></span> <span data-ttu-id="3b1d9-172">열 수는 병렬 쓰기 수를 결정하며 이는 데이터 디스크에 걸쳐 스트라이프될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-172">The number of columns determines the number of parallel writes, which can be striped across the data disks.</span></span> <span data-ttu-id="3b1d9-173">따라서 추가 데이터 디스크는 성능을 향상시킬 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-173">Therefore, any added data disks cannot increase performance.</span></span> <span data-ttu-id="3b1d9-174">쓰여지는 데이터에 더 많은 저장 공간을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-174">They can only provide more storage for the data being written.</span></span> <span data-ttu-id="3b1d9-175">즉, 이 제한으로 드라이브를 확장할 때 열 수는 추가할 수 있는 데이터 디스크의 최소 수를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-175">This limitation also means that, when extending the drive, the number of columns determines the minimum number of data disks that you can add.</span></span> <span data-ttu-id="3b1d9-176">따라서 4개의 데이터 디스크가 있는 저장소 풀을 만드는 경우 열 수도 4개가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-176">So if you create a storage pool with four data disks, the number of columns is also four.</span></span> <span data-ttu-id="3b1d9-177">저장소를 확장하면 4개 이상의 데이터 디스크도 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-177">Any time you extend the storage, you must add at least four data disks.</span></span>

![SQL VM에 대한 드라이브 확장](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-extend-a-drive.png)

## <a name="storage-configuration"></a><span data-ttu-id="3b1d9-179">저장소 구성</span><span class="sxs-lookup"><span data-stu-id="3b1d9-179">Storage configuration</span></span>
<span data-ttu-id="3b1d9-180">이 섹션에서는 Azure가 SQL VM을 프로비전하거나 Azure 포털에서 구성하는 동안 자동으로 수행하는 저장소 구성 변경에 대한 참조를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-180">This section provides a reference for the storage configuration changes that Azure automatically performs during SQL VM provisioning or configuration in the Azure Portal.</span></span>

* <span data-ttu-id="3b1d9-181">VM에 대한 2TB 미만의 저장소를 선택한 경우 Azure는 저장소 풀을 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-181">If you have selected fewer than two TBs of storage for your VM, Azure does not create a storage pool.</span></span>
* <span data-ttu-id="3b1d9-182">VM에 대한 2TB 이상의 저장소를 선택한 경우 Azure는 저장소 풀을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-182">If you have selected at least two TBs of storage for your VM, Azure configures a storage pool.</span></span> <span data-ttu-id="3b1d9-183">이 항목의 다음 섹션에서는 저장소 풀 구성의 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-183">The next section of this topic provides the details of the storage pool configuration.</span></span>
* <span data-ttu-id="3b1d9-184">자동 저장소 구성은 항상 [프리미엄 저장소](../../../storage/common/storage-premium-storage.md) P30 데이터 디스크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-184">Automatic storage configuration always uses [premium storage](../../../storage/common/storage-premium-storage.md) P30 data disks.</span></span> <span data-ttu-id="3b1d9-185">따라서 선택한 테라바이트 수와 VM에 연결된 데이터 디스크의 수 간에 1:1 매핑이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-185">Consequently, there is a 1:1 mapping between your selected number of Terabytes and the number of data disks attached to your VM.</span></span>

<span data-ttu-id="3b1d9-186">가격 책정 정보는 [디스크 저장소](https://azure.microsoft.com/pricing/details/storage) 탭의 **저장소 가격 책정** 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-186">For pricing information, see the [Storage pricing](https://azure.microsoft.com/pricing/details/storage) page on the **Disk Storage** tab.</span></span>

### <a name="creation-of-the-storage-pool"></a><span data-ttu-id="3b1d9-187">저장소 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="3b1d9-187">Creation of the storage pool</span></span>
<span data-ttu-id="3b1d9-188">Azure는 다음 설정을 사용하여 SQL Server VM에 저장소 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-188">Azure uses the following settings to create the storage pool on SQL Server VMs.</span></span>

| <span data-ttu-id="3b1d9-189">설정</span><span class="sxs-lookup"><span data-stu-id="3b1d9-189">Setting</span></span> | <span data-ttu-id="3b1d9-190">값</span><span class="sxs-lookup"><span data-stu-id="3b1d9-190">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3b1d9-191">스트라이프 크기</span><span class="sxs-lookup"><span data-stu-id="3b1d9-191">Stripe size</span></span> |<span data-ttu-id="3b1d9-192">256KB(데이터 웨어하우징); 64KB(트랜잭션)</span><span class="sxs-lookup"><span data-stu-id="3b1d9-192">256 KB (Data warehousing); 64 KB (Transactional)</span></span> |
| <span data-ttu-id="3b1d9-193">디스크 크기</span><span class="sxs-lookup"><span data-stu-id="3b1d9-193">Disk sizes</span></span> |<span data-ttu-id="3b1d9-194">각각 1TB</span><span class="sxs-lookup"><span data-stu-id="3b1d9-194">1 TB each</span></span> |
| <span data-ttu-id="3b1d9-195">캐시</span><span class="sxs-lookup"><span data-stu-id="3b1d9-195">Cache</span></span> |<span data-ttu-id="3b1d9-196">읽기</span><span class="sxs-lookup"><span data-stu-id="3b1d9-196">Read</span></span> |
| <span data-ttu-id="3b1d9-197">할당 크기</span><span class="sxs-lookup"><span data-stu-id="3b1d9-197">Allocation size</span></span> |<span data-ttu-id="3b1d9-198">64KB NTFS 할당 단위 크기</span><span class="sxs-lookup"><span data-stu-id="3b1d9-198">64 KB NTFS allocation unit size</span></span> |
| <span data-ttu-id="3b1d9-199">즉시 파일 초기화</span><span class="sxs-lookup"><span data-stu-id="3b1d9-199">Instant file initialization</span></span> |<span data-ttu-id="3b1d9-200">사용</span><span class="sxs-lookup"><span data-stu-id="3b1d9-200">Enabled</span></span> |
| <span data-ttu-id="3b1d9-201">메모리 내 페이지 잠금</span><span class="sxs-lookup"><span data-stu-id="3b1d9-201">Lock pages in memory</span></span> |<span data-ttu-id="3b1d9-202">사용</span><span class="sxs-lookup"><span data-stu-id="3b1d9-202">Enabled</span></span> |
| <span data-ttu-id="3b1d9-203">복구</span><span class="sxs-lookup"><span data-stu-id="3b1d9-203">Recovery</span></span> |<span data-ttu-id="3b1d9-204">단순 복구(복원력 없음)</span><span class="sxs-lookup"><span data-stu-id="3b1d9-204">Simple recovery (no resiliency)</span></span> |
| <span data-ttu-id="3b1d9-205">열 수</span><span class="sxs-lookup"><span data-stu-id="3b1d9-205">Number of columns</span></span> |<span data-ttu-id="3b1d9-206">데이터 디스크 수<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="3b1d9-206">Number of data disks<sup>1</sup></span></span> |
| <span data-ttu-id="3b1d9-207">TempDB 위치</span><span class="sxs-lookup"><span data-stu-id="3b1d9-207">TempDB location</span></span> |<span data-ttu-id="3b1d9-208">데이터 디스크에 저장됨<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="3b1d9-208">Stored on data disks<sup>2</sup></span></span> |

<span data-ttu-id="3b1d9-209"><sup>1</sup> 저장소 풀을 만든 후에 저장소 풀에서 열 수를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-209"><sup>1</sup> After the storage pool is created, you cannot alter the number of columns in the storage pool.</span></span>

<span data-ttu-id="3b1d9-210"><sup>2</sup> 이 설정은 저장소 구성 기능을 사용하는 첫 번째 드라이브에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-210"><sup>2</sup> This setting only applies to the first drive you create using the storage configuration feature.</span></span>

## <a name="workload-optimization-settings"></a><span data-ttu-id="3b1d9-211">워크로드 최적화 설정</span><span class="sxs-lookup"><span data-stu-id="3b1d9-211">Workload optimization settings</span></span>
<span data-ttu-id="3b1d9-212">다음 테이블에서는 사용할 수 있는 세 가지 워크로드 유형 옵션 및 이에 해당하는 최적화를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-212">The following table describes the three workload type options available and their corresponding optimizations:</span></span>

| <span data-ttu-id="3b1d9-213">워크로드 유형</span><span class="sxs-lookup"><span data-stu-id="3b1d9-213">Workload type</span></span> | <span data-ttu-id="3b1d9-214">설명</span><span class="sxs-lookup"><span data-stu-id="3b1d9-214">Description</span></span> | <span data-ttu-id="3b1d9-215">최적화</span><span class="sxs-lookup"><span data-stu-id="3b1d9-215">Optimizations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b1d9-216">**일반**</span><span class="sxs-lookup"><span data-stu-id="3b1d9-216">**General**</span></span> |<span data-ttu-id="3b1d9-217">대부분의 워크로드를 지원하는 기본 설정</span><span class="sxs-lookup"><span data-stu-id="3b1d9-217">Default setting that supports most workloads</span></span> |<span data-ttu-id="3b1d9-218">없음</span><span class="sxs-lookup"><span data-stu-id="3b1d9-218">None</span></span> |
| <span data-ttu-id="3b1d9-219">**트랜잭션 처리**</span><span class="sxs-lookup"><span data-stu-id="3b1d9-219">**Transactional processing**</span></span> |<span data-ttu-id="3b1d9-220">기존의 데이터베이스 OLTP 워크로드용으로 저장소를 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-220">Optimizes the storage for traditional database OLTP workloads</span></span> |<span data-ttu-id="3b1d9-221">추적 플래그 1117</span><span class="sxs-lookup"><span data-stu-id="3b1d9-221">Trace Flag 1117</span></span><br/><span data-ttu-id="3b1d9-222">추적 플래그 1118</span><span class="sxs-lookup"><span data-stu-id="3b1d9-222">Trace Flag 1118</span></span> |
| <span data-ttu-id="3b1d9-223">**데이터 웨어하우징**</span><span class="sxs-lookup"><span data-stu-id="3b1d9-223">**Data warehousing**</span></span> |<span data-ttu-id="3b1d9-224">분석 및 보고 워크로드용으로 저장소를 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-224">Optimizes the storage for analytic and reporting workloads</span></span> |<span data-ttu-id="3b1d9-225">추적 플래그 610</span><span class="sxs-lookup"><span data-stu-id="3b1d9-225">Trace Flag 610</span></span><br/><span data-ttu-id="3b1d9-226">추적 플래그 1117</span><span class="sxs-lookup"><span data-stu-id="3b1d9-226">Trace Flag 1117</span></span> |

> [!NOTE]
> <span data-ttu-id="3b1d9-227">SQL 가상 컴퓨터를 프로비전할 때 저장소 구성 단계에서 워크로드 유형을 선택하여 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-227">You can only specify the workload type when you provision a SQL virtual machine by selecting it in the storage configuration step.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="3b1d9-228">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3b1d9-228">Next steps</span></span>
<span data-ttu-id="3b1d9-229">Azure VM에서의 SQL Server 실행에 관한 다른 항목은 [Azure 가상 컴퓨터의 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b1d9-229">For other topics related to running SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
