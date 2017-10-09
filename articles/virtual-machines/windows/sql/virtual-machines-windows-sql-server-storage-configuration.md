---
title: "SQL Server Vm에 대 한 aaaStorage 구성 | Microsoft Docs"
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
ms.openlocfilehash: b50dbd698828780cfc044fa0966e8f4e2f3bb6c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="storage-configuration-for-sql-server-vms"></a><span data-ttu-id="fefbf-104">SQL Server VM에 대한 저장소 구성</span><span class="sxs-lookup"><span data-stu-id="fefbf-104">Storage configuration for SQL Server VMs</span></span>
<span data-ttu-id="fefbf-105">Azure에서 SQL Server 가상 컴퓨터 이미지를 구성 hello 포털 저장소 구성이 tooautomate 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-105">When you configure a SQL Server virtual machine image in Azure, hello Portal helps tooautomate your storage configuration.</span></span> <span data-ttu-id="fefbf-106">여기에 연결 하는 저장소 toohello VM을 해당 저장소 액세스할 수 있는 tooSQL 서버를 만들고이 toooptimize 특정 성능 요구 사항에 맞게 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-106">This includes attaching storage toohello VM, making that storage accessible tooSQL Server, and configuring it toooptimize for your specific performance requirements.</span></span>

<span data-ttu-id="fefbf-107">이 항목에서는 Azure에서 프로비전 중 저장소 SQL Server VM 및 기존 VM에 대한 저장소를 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-107">This topic explains how Azure configures storage for your SQL Server VMs both during provisioning and for existing VMs.</span></span> <span data-ttu-id="fefbf-108">이 구성은 hello 기초로 [성능 모범 사례](virtual-machines-windows-sql-performance.md) Azure vm의 SQL Server를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-108">This configuration is based on hello [performance best practices](virtual-machines-windows-sql-performance.md) for Azure VMs running SQL Server.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="fefbf-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fefbf-109">Prerequisites</span></span>
<span data-ttu-id="fefbf-110">toouse hello 자동 저장소 구성 설정, 가상 컴퓨터 특성에 따라 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="fefbf-110">toouse hello automated storage configuration settings, your virtual machine requires hello following characteristics:</span></span>

* <span data-ttu-id="fefbf-111">[SQL Server 갤러리 이미지](virtual-machines-windows-sql-server-iaas-overview.md#option-1-create-a-sql-vm-with-per-minute-licensing)로 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-111">Provisioned with a [SQL Server gallery image](virtual-machines-windows-sql-server-iaas-overview.md#option-1-create-a-sql-vm-with-per-minute-licensing).</span></span>
* <span data-ttu-id="fefbf-112">사용 하 여 hello [리소스 관리자 배포 모델](../../../azure-resource-manager/resource-manager-deployment-model.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-112">Uses hello [Resource Manager deployment model](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
* <span data-ttu-id="fefbf-113">[프리미엄 저장소](../../../storage/common/storage-premium-storage.md)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-113">Uses [Premium Storage](../../../storage/common/storage-premium-storage.md).</span></span>

## <a name="new-vms"></a><span data-ttu-id="fefbf-114">새 VM</span><span class="sxs-lookup"><span data-stu-id="fefbf-114">New VMs</span></span>
<span data-ttu-id="fefbf-115">hello 다음 섹션에서는 설명 방법을 새 SQL Server 가상 컴퓨터에 대 한 tooconfigure 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-115">hello following sections describe how tooconfigure storage for new SQL Server virtual machines.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="fefbf-116">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="fefbf-116">Azure Portal</span></span>
<span data-ttu-id="fefbf-117">SQL Server 갤러리 이미지를 사용 하 여 Azure VM을 프로 비전 하는 경우 선택할 수 있습니다 tooautomatically 새 VM에 대 한 hello 저장소를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-117">When provisioning an Azure VM using a SQL Server gallery image, you can choose tooautomatically configure hello storage for your new VM.</span></span> <span data-ttu-id="fefbf-118">Hello 저장소 크기, 성능 제한 및 작업 유형을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-118">You specify hello storage size, performance limits, and workload type.</span></span> <span data-ttu-id="fefbf-119">hello 다음 스크린샷은 SQL VM 중에 사용 하는 hello 저장소 구성 블레이드 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-119">hello following screenshot shows hello Storage configuration blade used during SQL VM provisioning.</span></span>

![프로비전하는 동안 SQL Server VM 저장소 구성](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-provisioning.png)

<span data-ttu-id="fefbf-121">선택한 설정에 따라 Azure hello 저장소 구성 작업 hello VM을 만든 후 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-121">Based on your choices, Azure performs hello following storage configuration tasks after creating hello VM:</span></span>

* <span data-ttu-id="fefbf-122">에서는 프리미엄 저장소 데이터 디스크 toohello 가상 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-122">Creates and attaches premium storage data disks toohello virtual machine.</span></span>
* <span data-ttu-id="fefbf-123">Hello 데이터 디스크 toobe 액세스할 수 있는 tooSQL 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-123">Configures hello data disks toobe accessible tooSQL Server.</span></span>
* <span data-ttu-id="fefbf-124">Hello 데이터 디스크를 저장소로 구성 hello에 따라 풀 크기와 성능 (IOPS 및 처리량) 요구 사항을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-124">Configures hello data disks into a storage pool based on hello specified size and performance (IOPS and throughput) requirements.</span></span>
* <span data-ttu-id="fefbf-125">Hello 가상 컴퓨터를 새 드라이브로 hello 저장소 풀을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-125">Associates hello storage pool with a new drive on hello virtual machine.</span></span>
* <span data-ttu-id="fefbf-126">지정한 워크로드 유형(데이터 웨어하우징, 트랜잭션 처리 또는 일반)에 따라 새 드라이브를 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-126">Optimizes this new drive based on your specified workload type (Data warehousing, Transactional processing, or General).</span></span>

<span data-ttu-id="fefbf-127">Azure 저장소의 설정을 구성 하는 방법에 자세한 내용은 참조 hello [저장소 구성 섹션](#storage-configuration)합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-127">For further details on how Azure configures storage settings, see hello [Storage configuration section](#storage-configuration).</span></span> <span data-ttu-id="fefbf-128">Toocreate hello Azure 포털에서에서 SQL Server VM 확인 하려면 어떻게 해야 하는 전체 연습은 [자습서를 프로 비전 하는 hello](virtual-machines-windows-portal-sql-server-provision.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-128">For a full walkthrough of how toocreate a SQL Server VM in hello Azure Portal, see [hello provisioning tutorial](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="resource-manage-templates"></a><span data-ttu-id="fefbf-129">Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="fefbf-129">Resource Manage templates</span></span>
<span data-ttu-id="fefbf-130">리소스 관리자 템플릿을 다음 hello를 사용 하는 경우 기본적으로 저장소 풀 구성 하지 않고도 두 개의 프리미엄 데이터 디스크가 연결 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-130">If you use hello following Resource Manager templates, two premium data disks are attached by default, with no storage pool configuration.</span></span> <span data-ttu-id="fefbf-131">그러나 이러한 템플릿을 toochange hello 수가 toohello 연결 된 가상 컴퓨터는 프리미엄 데이터 디스크를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-131">However, you can customize these templates toochange hello number of premium data disks that are attached toohello virtual machine.</span></span>

* [<span data-ttu-id="fefbf-132">자동화된 백업을 사용하여 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="fefbf-132">Create VM with Automated Backup</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-autobackup)
* [<span data-ttu-id="fefbf-133">자동화된 패치를 사용하여 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="fefbf-133">Create VM with Automated Patching</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-autopatching)
* [<span data-ttu-id="fefbf-134">AKV 통합을 사용하여 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="fefbf-134">Create VM with AKV Integration</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-keyvault)

## <a name="existing-vms"></a><span data-ttu-id="fefbf-135">기존 VM</span><span class="sxs-lookup"><span data-stu-id="fefbf-135">Existing VMs</span></span>
<span data-ttu-id="fefbf-136">기존 SQL Server Vm에 대 한 hello Azure 포털에서에서 일부 저장소 설정을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-136">For existing SQL Server VMs, you can modify some storage settings in hello Azure portal.</span></span> <span data-ttu-id="fefbf-137">VM을 선택, toohello 설정 영역을 이동 하 고 SQL Server 구성을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-137">Select your VM, go toohello Settings area, and then select SQL Server Configuration.</span></span> <span data-ttu-id="fefbf-138">SQL Server 구성 블레이드 hello VM의 hello 현재 저장소 사용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-138">hello SQL Server Configuration blade shows hello current storage usage of your VM.</span></span> <span data-ttu-id="fefbf-139">VM에 있는 모든 드라이브는 이 차트에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-139">All drives that exist on your VM are displayed in this chart.</span></span> <span data-ttu-id="fefbf-140">각 드라이브에 대 한 hello 저장 공간 4 개의 섹션에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-140">For each drive, hello storage space displays in four sections:</span></span>

* <span data-ttu-id="fefbf-141">SQL 데이터</span><span class="sxs-lookup"><span data-stu-id="fefbf-141">SQL data</span></span>
* <span data-ttu-id="fefbf-142">SQL 로그</span><span class="sxs-lookup"><span data-stu-id="fefbf-142">SQL log</span></span>
* <span data-ttu-id="fefbf-143">기타(비 SQL 저장소)</span><span class="sxs-lookup"><span data-stu-id="fefbf-143">Other (non-SQL storage)</span></span>
* <span data-ttu-id="fefbf-144">사용 가능</span><span class="sxs-lookup"><span data-stu-id="fefbf-144">Available</span></span>

![기존 SQL Server VM에 대한 저장소 구성](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-existing.png)

<span data-ttu-id="fefbf-146">tooconfigure hello 저장소 tooadd 새 드라이브 또는 기존 드라이브를 확장, hello 차트 위 hello 편집 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-146">tooconfigure hello storage tooadd a new drive or extend an existing drive, click hello Edit link above hello chart.</span></span>

<span data-ttu-id="fefbf-147">볼 수 있는 hello 구성 옵션 하기 전에이 기능 사용 여부에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-147">hello configuration options that you see varies depending on whether you have used this feature before.</span></span> <span data-ttu-id="fefbf-148">처음으로 hello에 대 한 사용 하 여, 새 드라이브에 대 한 저장소 요구 사항을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-148">When using for hello first time, you can specify your storage requirements for a new drive.</span></span> <span data-ttu-id="fefbf-149">이 기능은 toocreate 드라이브를 이전에 사용한 경우 해당 드라이브의 저장소 tooextend를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-149">If you previously used this feature toocreate a drive, you can choose tooextend that drive’s storage.</span></span>

### <a name="use-for-hello-first-time"></a><span data-ttu-id="fefbf-150">처음으로 hello에 대 한 사용</span><span class="sxs-lookup"><span data-stu-id="fefbf-150">Use for hello first time</span></span>
<span data-ttu-id="fefbf-151">지정할 수는 경우에이 기능을 사용 하 여 처음으로, 새 드라이브에 대 한 저장소 크기와 성능 제한 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-151">If it is your first time using this feature, you can specify hello storage size and performance limits for a new drive.</span></span> <span data-ttu-id="fefbf-152">이 환경은 비슷한 toowhat 시간 프로 비전에 표시 되는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-152">This experience is similar toowhat you would see at provisioning time.</span></span> <span data-ttu-id="fefbf-153">hello 주요 차이점은 toospecify hello 작업 부하 유형이 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-153">hello main difference is that you are not permitted toospecify hello workload type.</span></span> <span data-ttu-id="fefbf-154">이 제한 사항은 hello 가상 컴퓨터에 모든 기존 SQL Server 구성을 중단을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-154">This restriction prevents disrupting any existing SQL Server configurations on hello virtual machine.</span></span>

![SQL Server 저장소 슬라이더 구성](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-usage-sliders.png)

<span data-ttu-id="fefbf-156">Azure는 사양에 따라 새 드라이브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-156">Azure creates a new drive based on your specifications.</span></span> <span data-ttu-id="fefbf-157">이 시나리오에서는 Azure 저장소 구성 작업을 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-157">In this scenario, Azure performs hello following storage configuration tasks:</span></span>

* <span data-ttu-id="fefbf-158">에서는 프리미엄 저장소 데이터 디스크 toohello 가상 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-158">Creates and attaches premium storage data disks toohello virtual machine.</span></span>
* <span data-ttu-id="fefbf-159">Hello 데이터 디스크 toobe 액세스할 수 있는 tooSQL 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-159">Configures hello data disks toobe accessible tooSQL Server.</span></span>
* <span data-ttu-id="fefbf-160">Hello 데이터 디스크를 저장소로 구성 hello에 따라 풀 크기와 성능 (IOPS 및 처리량) 요구 사항을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-160">Configures hello data disks into a storage pool based on hello specified size and performance (IOPS and throughput) requirements.</span></span>
* <span data-ttu-id="fefbf-161">Hello 가상 컴퓨터를 새 드라이브로 hello 저장소 풀을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-161">Associates hello storage pool with a new drive on hello virtual machine.</span></span>

<span data-ttu-id="fefbf-162">Azure 저장소의 설정을 구성 하는 방법에 자세한 내용은 참조 hello [저장소 구성 섹션](#storage-configuration)합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-162">For further details on how Azure configures storage settings, see hello [Storage configuration section](#storage-configuration).</span></span>

### <a name="add-a-new-drive"></a><span data-ttu-id="fefbf-163">새 드라이브 추가</span><span class="sxs-lookup"><span data-stu-id="fefbf-163">Add a new drive</span></span>
<span data-ttu-id="fefbf-164">SQL Server VM에 이미 저장소를 구성한 경우 저장소를 확장하면 두 가지 새로운 옵션을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-164">If you have already configured storage on your SQL Server VM, expanding storage brings up two new options.</span></span> <span data-ttu-id="fefbf-165">hello 첫 번째 옵션은 tooadd는 새 드라이브를 VM의 hello 성능 수준을 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-165">hello first option is tooadd a new drive, which can increase hello performance level of your VM.</span></span>

![새 드라이브 tooa SQL VM 추가](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-add-new-drive.png)

<span data-ttu-id="fefbf-167">그러나 hello 드라이브를 추가한 후 몇 가지 추가 수동 구성 tooachieve hello 성능 향상을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-167">However, after adding hello drive, you must perform some extra manual configuration tooachieve hello performance increase.</span></span>

### <a name="extend-hello-drive"></a><span data-ttu-id="fefbf-168">Hello 드라이브를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-168">Extend hello drive</span></span>
<span data-ttu-id="fefbf-169">hello 저장소 확장을 위한 다른 옵션은 tooextend hello 기존 드라이브입니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-169">hello other option for expanding storage is tooextend hello existing drive.</span></span> <span data-ttu-id="fefbf-170">이 옵션을 사용 하면 사용자의 드라이브에 대 한 사용 가능한 저장소 hello 있지만 성능을 증가 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-170">This option increases hello available storage for your drive, but it does not increase performance.</span></span> <span data-ttu-id="fefbf-171">저장소 풀과 hello 저장소 풀이 만들어진 후 hello 열 수를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-171">With storage pools, you cannot alter hello number of columns after hello storage pool is created.</span></span> <span data-ttu-id="fefbf-172">열 수가 hello hello 데이터 디스크 스트라이프 수는 병렬 쓰기 hello 수를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-172">hello number of columns determines hello number of parallel writes, which can be striped across hello data disks.</span></span> <span data-ttu-id="fefbf-173">따라서 추가 데이터 디스크는 성능을 향상시킬 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-173">Therefore, any added data disks cannot increase performance.</span></span> <span data-ttu-id="fefbf-174">만 쓰여지는 hello 데이터에 대 한 더 많은 저장 공간을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-174">They can only provide more storage for hello data being written.</span></span> <span data-ttu-id="fefbf-175">이 제한 사항은 hello 드라이브를 확장 하는 경우 열 수가 hello 추가할 수 있는 데이터 디스크의 hello 최소 수를 결정 한다는 의미 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-175">This limitation also means that, when extending hello drive, hello number of columns determines hello minimum number of data disks that you can add.</span></span> <span data-ttu-id="fefbf-176">따라서 4 개의 데이터 디스크와 저장소 풀을 만드는 경우 열의 hello 수는 또한 4 개입니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-176">So if you create a storage pool with four data disks, hello number of columns is also four.</span></span> <span data-ttu-id="fefbf-177">Hello 저장소를 확장 하 든 지 4 개 이상의 데이터 디스크를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-177">Any time you extend hello storage, you must add at least four data disks.</span></span>

![SQL VM에 대한 드라이브 확장](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-extend-a-drive.png)

## <a name="storage-configuration"></a><span data-ttu-id="fefbf-179">Storage 구성</span><span class="sxs-lookup"><span data-stu-id="fefbf-179">Storage configuration</span></span>
<span data-ttu-id="fefbf-180">이 섹션에서는 Azure SQL VM 프로 비전 또는 hello Azure 포털에서에서 구성 하는 동안 자동으로 수행 하는 hello 저장소 구성 변경에 대 한 대 한 참조를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-180">This section provides a reference for hello storage configuration changes that Azure automatically performs during SQL VM provisioning or configuration in hello Azure Portal.</span></span>

* <span data-ttu-id="fefbf-181">VM에 대한 2TB 미만의 저장소를 선택한 경우 Azure는 저장소 풀을 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-181">If you have selected fewer than two TBs of storage for your VM, Azure does not create a storage pool.</span></span>
* <span data-ttu-id="fefbf-182">VM에 대한 2TB 이상의 저장소를 선택한 경우 Azure는 저장소 풀을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-182">If you have selected at least two TBs of storage for your VM, Azure configures a storage pool.</span></span> <span data-ttu-id="fefbf-183">이 항목의 다음 섹션 hello hello 저장소 풀 구성의 hello 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-183">hello next section of this topic provides hello details of hello storage pool configuration.</span></span>
* <span data-ttu-id="fefbf-184">자동 저장소 구성은 항상 [프리미엄 저장소](../../../storage/common/storage-premium-storage.md) P30 데이터 디스크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-184">Automatic storage configuration always uses [premium storage](../../../storage/common/storage-premium-storage.md) P30 data disks.</span></span> <span data-ttu-id="fefbf-185">따라서 선택한 수가 테라바이트 간에 1:1 매핑 않으며 tooyour VM을 첨부 하는 데이터 디스크의 hello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-185">Consequently, there is a 1:1 mapping between your selected number of Terabytes and hello number of data disks attached tooyour VM.</span></span>

<span data-ttu-id="fefbf-186">가격 책정 정보 참조 hello [저장소 가격](https://azure.microsoft.com/pricing/details/storage) hello에 대 한 페이지 **디스크 저장소** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-186">For pricing information, see hello [Storage pricing](https://azure.microsoft.com/pricing/details/storage) page on hello **Disk Storage** tab.</span></span>

### <a name="creation-of-hello-storage-pool"></a><span data-ttu-id="fefbf-187">Hello 저장소 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="fefbf-187">Creation of hello storage pool</span></span>
<span data-ttu-id="fefbf-188">Azure는 SQL Server Vm에 설정을 toocreate hello 저장소 풀을 다음과 같은 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-188">Azure uses hello following settings toocreate hello storage pool on SQL Server VMs.</span></span>

| <span data-ttu-id="fefbf-189">설정</span><span class="sxs-lookup"><span data-stu-id="fefbf-189">Setting</span></span> | <span data-ttu-id="fefbf-190">값</span><span class="sxs-lookup"><span data-stu-id="fefbf-190">Value</span></span> |
| --- | --- |
| <span data-ttu-id="fefbf-191">스트라이프 크기</span><span class="sxs-lookup"><span data-stu-id="fefbf-191">Stripe size</span></span> |<span data-ttu-id="fefbf-192">256KB(데이터 웨어하우징); 64KB(트랜잭션)</span><span class="sxs-lookup"><span data-stu-id="fefbf-192">256 KB (Data warehousing); 64 KB (Transactional)</span></span> |
| <span data-ttu-id="fefbf-193">디스크 크기</span><span class="sxs-lookup"><span data-stu-id="fefbf-193">Disk sizes</span></span> |<span data-ttu-id="fefbf-194">각각 1TB</span><span class="sxs-lookup"><span data-stu-id="fefbf-194">1 TB each</span></span> |
| <span data-ttu-id="fefbf-195">캐시</span><span class="sxs-lookup"><span data-stu-id="fefbf-195">Cache</span></span> |<span data-ttu-id="fefbf-196">읽기</span><span class="sxs-lookup"><span data-stu-id="fefbf-196">Read</span></span> |
| <span data-ttu-id="fefbf-197">할당 크기</span><span class="sxs-lookup"><span data-stu-id="fefbf-197">Allocation size</span></span> |<span data-ttu-id="fefbf-198">64KB NTFS 할당 단위 크기</span><span class="sxs-lookup"><span data-stu-id="fefbf-198">64 KB NTFS allocation unit size</span></span> |
| <span data-ttu-id="fefbf-199">즉시 파일 초기화</span><span class="sxs-lookup"><span data-stu-id="fefbf-199">Instant file initialization</span></span> |<span data-ttu-id="fefbf-200">사용</span><span class="sxs-lookup"><span data-stu-id="fefbf-200">Enabled</span></span> |
| <span data-ttu-id="fefbf-201">메모리 내 페이지 잠금</span><span class="sxs-lookup"><span data-stu-id="fefbf-201">Lock pages in memory</span></span> |<span data-ttu-id="fefbf-202">사용</span><span class="sxs-lookup"><span data-stu-id="fefbf-202">Enabled</span></span> |
| <span data-ttu-id="fefbf-203">복구</span><span class="sxs-lookup"><span data-stu-id="fefbf-203">Recovery</span></span> |<span data-ttu-id="fefbf-204">단순 복구(복원력 없음)</span><span class="sxs-lookup"><span data-stu-id="fefbf-204">Simple recovery (no resiliency)</span></span> |
| <span data-ttu-id="fefbf-205">열 수</span><span class="sxs-lookup"><span data-stu-id="fefbf-205">Number of columns</span></span> |<span data-ttu-id="fefbf-206">데이터 디스크 수<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="fefbf-206">Number of data disks<sup>1</sup></span></span> |
| <span data-ttu-id="fefbf-207">TempDB 위치</span><span class="sxs-lookup"><span data-stu-id="fefbf-207">TempDB location</span></span> |<span data-ttu-id="fefbf-208">데이터 디스크에 저장됨<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="fefbf-208">Stored on data disks<sup>2</sup></span></span> |

<span data-ttu-id="fefbf-209"><sup>1</sup> hello 저장소 풀을 만든 후 hello hello 저장소 풀의 열 수를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-209"><sup>1</sup> After hello storage pool is created, you cannot alter hello number of columns in hello storage pool.</span></span>

<span data-ttu-id="fefbf-210"><sup>2</sup> 이 설정은 hello 저장소 구성 기능을 사용 하 여 만드는 toohello 첫 번째 드라이브에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-210"><sup>2</sup> This setting only applies toohello first drive you create using hello storage configuration feature.</span></span>

## <a name="workload-optimization-settings"></a><span data-ttu-id="fefbf-211">워크로드 최적화 설정</span><span class="sxs-lookup"><span data-stu-id="fefbf-211">Workload optimization settings</span></span>
<span data-ttu-id="fefbf-212">hello 다음 표에서 hello 세 가지 작업 유형 사용 가능한 옵션 및 해당 해당 최적화.</span><span class="sxs-lookup"><span data-stu-id="fefbf-212">hello following table describes hello three workload type options available and their corresponding optimizations:</span></span>

| <span data-ttu-id="fefbf-213">워크로드 유형</span><span class="sxs-lookup"><span data-stu-id="fefbf-213">Workload type</span></span> | <span data-ttu-id="fefbf-214">설명</span><span class="sxs-lookup"><span data-stu-id="fefbf-214">Description</span></span> | <span data-ttu-id="fefbf-215">최적화</span><span class="sxs-lookup"><span data-stu-id="fefbf-215">Optimizations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fefbf-216">**일반**</span><span class="sxs-lookup"><span data-stu-id="fefbf-216">**General**</span></span> |<span data-ttu-id="fefbf-217">대부분의 워크로드를 지원하는 기본 설정</span><span class="sxs-lookup"><span data-stu-id="fefbf-217">Default setting that supports most workloads</span></span> |<span data-ttu-id="fefbf-218">없음</span><span class="sxs-lookup"><span data-stu-id="fefbf-218">None</span></span> |
| <span data-ttu-id="fefbf-219">**트랜잭션 처리**</span><span class="sxs-lookup"><span data-stu-id="fefbf-219">**Transactional processing**</span></span> |<span data-ttu-id="fefbf-220">일반 데이터베이스 OLTP 워크 로드에 대 한 hello 저장소를 최적화</span><span class="sxs-lookup"><span data-stu-id="fefbf-220">Optimizes hello storage for traditional database OLTP workloads</span></span> |<span data-ttu-id="fefbf-221">추적 플래그 1117</span><span class="sxs-lookup"><span data-stu-id="fefbf-221">Trace Flag 1117</span></span><br/><span data-ttu-id="fefbf-222">추적 플래그 1118</span><span class="sxs-lookup"><span data-stu-id="fefbf-222">Trace Flag 1118</span></span> |
| <span data-ttu-id="fefbf-223">**데이터 웨어하우징**</span><span class="sxs-lookup"><span data-stu-id="fefbf-223">**Data warehousing**</span></span> |<span data-ttu-id="fefbf-224">분석 및 보고 작업에 대 한 hello 저장소를 최적화</span><span class="sxs-lookup"><span data-stu-id="fefbf-224">Optimizes hello storage for analytic and reporting workloads</span></span> |<span data-ttu-id="fefbf-225">추적 플래그 610</span><span class="sxs-lookup"><span data-stu-id="fefbf-225">Trace Flag 610</span></span><br/><span data-ttu-id="fefbf-226">추적 플래그 1117</span><span class="sxs-lookup"><span data-stu-id="fefbf-226">Trace Flag 1117</span></span> |

> [!NOTE]
> <span data-ttu-id="fefbf-227">Hello 저장소 구성 단계에서 선택 하 여 SQL 가상 컴퓨터를 프로 비전 할 때에 hello 작업 유형을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-227">You can only specify hello workload type when you provision a SQL virtual machine by selecting it in hello storage configuration step.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="fefbf-228">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fefbf-228">Next steps</span></span>
<span data-ttu-id="fefbf-229">다른 항목은 서로 관련 toorunning Azure Vm에서 SQL Server에 대 한 참조 [Azure 가상 컴퓨터에 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fefbf-229">For other topics related toorunning SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
