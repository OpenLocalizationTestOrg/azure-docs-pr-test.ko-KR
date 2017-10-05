---
title: "SQL Server 가상 컴퓨터 프로비전 | Microsoft Docs"
description: "포털을 사용하여 Azure에서 SQL Server 가상 컴퓨터를 만들고 연결하기. 이 자습서는 리소스 관리자 모드를 사용합니다."
services: virtual-machines-windows
documentationcenter: na
author: rothja
editor: 
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 1aff691f-a40a-4de2-b6a0-def1384e086e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: jroth
experimental_id: a641df96-f27d-40
ms.openlocfilehash: c51908058bb785cb33da21de76ba3c956b6b9f1f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="provision-a-sql-server-virtual-machine-in-the-azure-portal"></a><span data-ttu-id="ae8f8-104">Azure 포털에서 SQL Server 가상 컴퓨터 프로비전</span><span class="sxs-lookup"><span data-stu-id="ae8f8-104">Provision a SQL Server virtual machine in the Azure Portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ae8f8-105">포털</span><span class="sxs-lookup"><span data-stu-id="ae8f8-105">Portal</span></span>](virtual-machines-windows-portal-sql-server-provision.md)
> * [<span data-ttu-id="ae8f8-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae8f8-106">PowerShell</span></span>](virtual-machines-windows-ps-sql-create.md)
> 
> 

<span data-ttu-id="ae8f8-107">이 종단간 자습서는 Azure 포털을 사용하여 SQL Server를 실행하는 가상 컴퓨터를 프로비전하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-107">This end-to-end tutorial shows you how to use the Azure Portal to provision a virtual machine running SQL Server.</span></span>

<span data-ttu-id="ae8f8-108">Azure 가상 컴퓨터(VM) 갤러리에는 Microsoft SQL Server가 포함된 몇 개의 이미지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-108">The Azure virtual machine (VM) gallery includes several images that contain Microsoft SQL Server.</span></span> <span data-ttu-id="ae8f8-109">클릭 몇 번으로, 갤러리에서 SQL VM 이미지 중 하나를 선택하고 Azure 환경에 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-109">With a few clicks, you can select one of the SQL VM images from the gallery and provision it in your Azure environment.</span></span>

<span data-ttu-id="ae8f8-110">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-110">In this tutorial, you will:</span></span>

* [<span data-ttu-id="ae8f8-111">갤러리에서 SQL VM 이미지 선택</span><span class="sxs-lookup"><span data-stu-id="ae8f8-111">Select a SQL VM image from the gallery</span></span>](#select-a-sql-vm-image-from-the-gallery)
* [<span data-ttu-id="ae8f8-112">VM 구성 및 만들기</span><span class="sxs-lookup"><span data-stu-id="ae8f8-112">Configure and create the VM</span></span>](#configure-the-vm)
* [<span data-ttu-id="ae8f8-113">원격 데스크톱을 사용하여 VM 열기</span><span class="sxs-lookup"><span data-stu-id="ae8f8-113">Open the VM with Remote Desktop</span></span>](#open-the-vm-with-remote-desktop)
* [<span data-ttu-id="ae8f8-114">원격으로 SQL Server 연결</span><span class="sxs-lookup"><span data-stu-id="ae8f8-114">Connect to SQL Server remotely</span></span>](#connect-to-sql-server-remotely)

## <a name="select-a-sql-vm-image-from-the-gallery"></a><span data-ttu-id="ae8f8-115">갤러리에서 SQL VM 이미지 선택</span><span class="sxs-lookup"><span data-stu-id="ae8f8-115">Select a SQL VM image from the gallery</span></span>
1. <span data-ttu-id="ae8f8-116">사용자 계정을 사용하여 [Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-116">Log in to the [Azure portal](https://portal.azure.com) using your account.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ae8f8-117">Azure 계정이 없는 경우 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)을 방문하십시오.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-117">If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

2. <span data-ttu-id="ae8f8-118">Azure Portal에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-118">On the Azure portal, click **New**.</span></span> <span data-ttu-id="ae8f8-119">포털에 **새** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-119">The portal opens the **New** blade.</span></span> <span data-ttu-id="ae8f8-120">SQL Server VM 리소스는 Marketplace의 **계산** 그룹에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-120">The SQL Server VM resources are in the **Compute** group of the Marketplace.</span></span>
3. <span data-ttu-id="ae8f8-121">**새로 만들기** 블레이드에서 **계산**을 클릭한 다음 **모두 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-121">In the **New** blade, click **Compute** and then click **See all**.</span></span>
4. <span data-ttu-id="ae8f8-122">**필터** 텍스트 상자에서 SQL Server를 입력하고 ENTER 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-122">In the **Filter** text box type SQL Server, and press the ENTER key.</span></span>

   ![Azure Virtual Machines 블레이드](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-blade2.png)

5. <span data-ttu-id="ae8f8-124">사용 가능한 SQL Server 이미지를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-124">Review the available SQL Server images.</span></span> <span data-ttu-id="ae8f8-125">각 이미지는 SQL Server 버전 및 운영 체제를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-125">Each image identifies a SQL Server version and an operating system.</span></span> 
6. <span data-ttu-id="ae8f8-126">Windows Server 2016에서 SQL Server 2016 SP1 Developer용 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-126">Select the image for SQL Server 2016 SP1 Developer on Windows Server 2016.</span></span>

   > [!TIP]
   > <span data-ttu-id="ae8f8-127">Developer 버전은 개발 테스트 목적으로 무료로 제공되는 SQL Server의 모든 기능을 갖춘 버전이므로 이 자습서에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-127">The Developer edition is used in this tutorial because it is a full-featured edition of SQL Server that is free for development testing purposes.</span></span> <span data-ttu-id="ae8f8-128">VM 실행 비용에 대해서만 비용을 지불합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-128">You pay only for the cost of running the VM.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ae8f8-129">SQL VM 이미지는 만든 VM의 분당 가격에 SQL Server에 대한 라이선스 비용을 포함합니다(Developer 및 Express 버전 제외).</span><span class="sxs-lookup"><span data-stu-id="ae8f8-129">SQL VM images include the licensing costs for SQL Server into the per-minute pricing of the VM you create (except for the Developer and Express editions).</span></span> <span data-ttu-id="ae8f8-130">SQL Server Developer는 개발/테스트(비 프로덕션)를 위한 평가판이며, SQL Express는 간단한 워크로드(1GB 미만 메모리, 10GB 미만 저장소)를 위한 평가판입니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-130">SQL Server Developer is free for development/testing (not production) and SQL Express is free for lightweight workloads (less than 1 GB memory, less than 10-GB storage).</span></span>
   > <span data-ttu-id="ae8f8-131">BYOL(Bring Your Own License) 및 VM에 대해서만 지불에 대한 또 다른 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-131">There is another option to bring-your-own-license (BYOL) and pay only for the VM.</span></span> <span data-ttu-id="ae8f8-132">이러한 이미지 이름에는 접두사 {BYOL}이 붙습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-132">Those image names are prefixed with {BYOL}.</span></span> <span data-ttu-id="ae8f8-133">이러한 옵션에 대한 자세한 내용은 [SQL Server Azure VM에 대한 가격 책정 지침](virtual-machines-windows-sql-server-pricing-guidance.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-133">For more information on these options, see [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md).</span></span>

7. <span data-ttu-id="ae8f8-134">**배포 모델 선택**에서 **리소스 관리자**가 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-134">Under **Select a deployment model**, verify that **Resource Manager** is selected.</span></span> <span data-ttu-id="ae8f8-135">리소스 관리자는 새로운 가상 컴퓨터에 권장되는 배포 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-135">Resource Manager is the recommended deployment model for new virtual machines.</span></span> <span data-ttu-id="ae8f8-136">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-136">Click **Create**.</span></span>

    ![리소스 관리자로 SQL VM 만들기](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-sql-deployment-model.png)

## <a name="configure-the-vm"></a><span data-ttu-id="ae8f8-138">VM 구성</span><span class="sxs-lookup"><span data-stu-id="ae8f8-138">Configure the VM</span></span>
<span data-ttu-id="ae8f8-139">SQL Server 가상 컴퓨터를 구성하기 위한 5개의 블레이드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-139">There are five blades for configuring a SQL Server virtual machine.</span></span>

| <span data-ttu-id="ae8f8-140">단계</span><span class="sxs-lookup"><span data-stu-id="ae8f8-140">Step</span></span> | <span data-ttu-id="ae8f8-141">설명</span><span class="sxs-lookup"><span data-stu-id="ae8f8-141">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ae8f8-142">**기본 사항**</span><span class="sxs-lookup"><span data-stu-id="ae8f8-142">**Basics**</span></span> |[<span data-ttu-id="ae8f8-143">기본 설정 구성</span><span class="sxs-lookup"><span data-stu-id="ae8f8-143">Configure basic settings</span></span>](#1-configure-basic-settings) |
| <span data-ttu-id="ae8f8-144">**크기**</span><span class="sxs-lookup"><span data-stu-id="ae8f8-144">**Size**</span></span> |[<span data-ttu-id="ae8f8-145">가상 컴퓨터 크기 선택</span><span class="sxs-lookup"><span data-stu-id="ae8f8-145">Choose virtual machine size</span></span>](#2-choose-virtual-machine-size) |
| <span data-ttu-id="ae8f8-146">**설정**</span><span class="sxs-lookup"><span data-stu-id="ae8f8-146">**Settings**</span></span> |[<span data-ttu-id="ae8f8-147">선택적 기능 구성</span><span class="sxs-lookup"><span data-stu-id="ae8f8-147">Configure optional features</span></span>](#3-configure-optional-features) |
| <span data-ttu-id="ae8f8-148">**SQL 서버 설정**</span><span class="sxs-lookup"><span data-stu-id="ae8f8-148">**SQL Server settings**</span></span> |[<span data-ttu-id="ae8f8-149">SQL Server 설정 구성</span><span class="sxs-lookup"><span data-stu-id="ae8f8-149">Configure SQL server settings</span></span>](#4-configure-sql-server-settings) |
| <span data-ttu-id="ae8f8-150">**요약**</span><span class="sxs-lookup"><span data-stu-id="ae8f8-150">**Summary**</span></span> |[<span data-ttu-id="ae8f8-151">요약 검토</span><span class="sxs-lookup"><span data-stu-id="ae8f8-151">Review the summary</span></span>](#5-review-the-summary) |

## <a name="1-configure-basic-settings"></a><span data-ttu-id="ae8f8-152">1. 기본 설정 구성</span><span class="sxs-lookup"><span data-stu-id="ae8f8-152">1. Configure basic settings</span></span>
<span data-ttu-id="ae8f8-153">**기본** 블레이드에서 다음 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-153">On the **Basics** blade, provide the following information:</span></span>

* <span data-ttu-id="ae8f8-154">고유한 가상 컴퓨터 **이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-154">Enter a unique virtual machine **Name**.</span></span>
* <span data-ttu-id="ae8f8-155">VM의 로컬 관리자 계정에 대한 **사용자 이름** 을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-155">Specify a **User name** for the local administrator account on the VM.</span></span> <span data-ttu-id="ae8f8-156">이 계정은 SQL Server **sysadmin** 고정 서버 역할에도 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-156">This account is also added to the SQL Server **sysadmin** fixed server role.</span></span>
* <span data-ttu-id="ae8f8-157">강력한 **암호**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-157">Provide a strong **Password**.</span></span>
* <span data-ttu-id="ae8f8-158">구독이 여러 개인 경우 구독이 새 VM에 대해 올바른지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-158">If you have multiple subscriptions, verify that the subscription is correct for the new VM.</span></span>
* <span data-ttu-id="ae8f8-159">**리소스 그룹** 상자에 새 리소스 그룹의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-159">In the **Resource group** box, type a name for a new resource group.</span></span> <span data-ttu-id="ae8f8-160">또는 기존 리소스 그룹을 사용하려면 **기존 항목 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-160">Alternatively, to use an existing resource group click **Use existing**.</span></span> <span data-ttu-id="ae8f8-161">리소스 그룹은 Azure 내 관련 리소스의 컬렉션입니다(가상 컴퓨터, 저장소 계정, 가상 네트워크 등).</span><span class="sxs-lookup"><span data-stu-id="ae8f8-161">A resource group is a collection of related resources in Azure (virtual machines, storage accounts, virtual networks, etc.).</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="ae8f8-162">새 리소스 그룹을 사용하면 Azure에서 SQL Server 배포를 테스트하거나 알아보는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-162">Using a new resource group is helpful if you are just testing or learning about SQL Server deployments in Azure.</span></span> <span data-ttu-id="ae8f8-163">테스트를 완료한 후 리소스 그룹을 삭제하면 VM과 해당 리소스 그룹과 연결된 모든 리소스가 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-163">After you finish with your test, delete the resource group to automatically delete the VM and all resources associated with that resource group.</span></span> <span data-ttu-id="ae8f8-164">리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../../../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-164">For more information about resource groups, see [Azure Resource Manager Overview](../../../azure-resource-manager/resource-group-overview.md).</span></span>
  > 
  > 
* <span data-ttu-id="ae8f8-165">이 배포의 **위치** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-165">Select a **Location** for this deployment.</span></span>
* <span data-ttu-id="ae8f8-166">**확인** 을 클릭하여 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-166">Click **OK** to save the settings.</span></span>
  
    ![SQL 기본 블레이드](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-basic.png)

## <a name="2-choose-virtual-machine-size"></a><span data-ttu-id="ae8f8-168">2. 가상 컴퓨터 크기 선택</span><span class="sxs-lookup"><span data-stu-id="ae8f8-168">2. Choose virtual machine size</span></span>
<span data-ttu-id="ae8f8-169">**크기** 단계의 **크기 선택** 블레이드에서 가상 컴퓨터 크기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-169">On the **Size** step, choose a virtual machine size in the **Choose a size** blade.</span></span> <span data-ttu-id="ae8f8-170">블레이드는 선택한 이미지를 기반으로 권장되는 컴퓨터 크기를 처음에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-170">The blade initially displays recommended machine sizes based on the image you selected.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ae8f8-171">**크기 선택** 블레이드에 표시된 월별 예상 비용에는 SQL Server 라이선스 비용이 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-171">The estimated monthly cost displayed on the **Choose a size** blade does not include SQL Server licensing costs.</span></span> <span data-ttu-id="ae8f8-172">이 월별 예상 비용은 VM에만 해당하는 비용입니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-172">This estimated monthly cost is the cost of the VM alone.</span></span> <span data-ttu-id="ae8f8-173">SQL Server의 Express 및 Developer 버전의 경우, 이것은 총 예상 비용입니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-173">For the Express and Developer editions of SQL Server, this is the total estimated cost.</span></span> <span data-ttu-id="ae8f8-174">다른 버전의 경우 [Windows Virtual Machines 가격 책정 페이지](https://azure.microsoft.com/pricing/details/virtual-machines/windows/)를 참조하여 SQL Server의 대상 버전을 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-174">For other editions, see the [Windows Virtual Machines pricing page](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) and select your target edition of SQL Server.</span></span> <span data-ttu-id="ae8f8-175">또한 [SQL Server Azure VM에 대한 가격 책정 지침](virtual-machines-windows-sql-server-pricing-guidance.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-175">Also see the [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md).</span></span>

![SQL VM 크기 옵션](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-choose-a-size.png)

<span data-ttu-id="ae8f8-177">프로덕션 워크로드에는, [Premium Storage](../../../storage/storage-premium-storage.md)를 지원하는 가상 컴퓨터 크기를 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-177">For production workloads, we recommend selecting a virtual machine size that supports [Premium Storage](../../../storage/storage-premium-storage.md).</span></span> <span data-ttu-id="ae8f8-178">그러한 수준의 성능이 필요하지 않으면, **모두 보기** 단추를 사용하여 모든 컴퓨터 크기 옵션을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-178">If you do not require that level of performance, use the **View all** button, which shows all machine size options.</span></span> <span data-ttu-id="ae8f8-179">예를 들어, 개발 또는 테스트 환경을 위해 더 작은 컴퓨터 크기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-179">For example, you might use a smaller machine size for a development or test environment.</span></span>

> [!NOTE]
> <span data-ttu-id="ae8f8-180">가상 컴퓨터 크기에 대한 자세한 내용은 [가상 컴퓨터 크기](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-180">For more information about virtual machine sizes, [Sizes for virtual machines](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="ae8f8-181">SQL Server VM 크기에 대한 고려 사항은 [Azure Virtual Machines의 SQL Server에 대한 성능 모범 사례](virtual-machines-windows-sql-performance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-181">For considerations about SQL Server VM sizes, see [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span></span>

<span data-ttu-id="ae8f8-182">컴퓨터 크기를 선택한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-182">Choose your machine size, and then click **Select**.</span></span>

## <a name="3-configure-optional-features"></a><span data-ttu-id="ae8f8-183">3. 선택적 기능 구성</span><span class="sxs-lookup"><span data-stu-id="ae8f8-183">3. Configure optional features</span></span>
<span data-ttu-id="ae8f8-184">**설정** 블레이드에서 가상 컴퓨터용 Azure Storage, 네트워킹 및 모니터링을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-184">On the **Settings** blade, configure Azure storage, networking, and monitoring for the virtual machine.</span></span>

* <span data-ttu-id="ae8f8-185">**Storage**에서 **디스크 유형**으로 표준 또는 프리미엄(SSD)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-185">Under **Storage**, specify a **Disk type** of either Standard or Premium (SSD).</span></span> <span data-ttu-id="ae8f8-186">프리미엄 저장소는 프로덕션 워크로드용으로 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-186">Premium storage is recommended for production workloads.</span></span>

> [!NOTE]
> <span data-ttu-id="ae8f8-187">Premium Storage를 지원하지 않는 컴퓨터 크기에 대해 프리미엄(SSD)을 선택하면, 컴퓨터 크기가 자동으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-187">If you select Premium (SSD) for a machine size that does not support Premium Storage, your machine size changes automatically.</span></span>  
> 
> 

* <span data-ttu-id="ae8f8-188">**저장소 계정**아래에서 자동으로 프로비전된 저장소 계정 이름을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-188">Under **Storage account**, you can accept the automatically provisioned storage account name.</span></span> <span data-ttu-id="ae8f8-189">또한 **저장소 계정** 을 클릭하여 기존 계정을 선택하고 저장소 계정 유형을 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-189">You can also click on **Storage account** to choose an existing account and configure the storage account type.</span></span> <span data-ttu-id="ae8f8-190">기본적으로 Azure에서는 로컬 중복 저장소로 새 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-190">By default, Azure creates a new storage account with locally redundant storage.</span></span> <span data-ttu-id="ae8f8-191">저장소 옵션에 대한 자세한 내용은 [Azure Storage 복제](../../../storage/storage-redundancy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-191">For more information about storage options, see [Azure Storage replication](../../../storage/storage-redundancy.md).</span></span>
* <span data-ttu-id="ae8f8-192">**네트워크**아래에서 자동으로 채워진 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-192">Under **Network**, you can accept the automatically populated values.</span></span> <span data-ttu-id="ae8f8-193">각 기능을 클릭하여 **가상 네트워크**, **서브넷**, **공용 IP 주소** 및 **네트워크 보안 그룹**을 수동으로 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-193">You can also click on each feature to manually configure the **Virtual network**, **Subnet**, **Public IP address**, and **Network Security Group**.</span></span> <span data-ttu-id="ae8f8-194">이 자습서에서는 기본 값을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-194">For the purposes of this tutorial, keep the default values.</span></span>
* <span data-ttu-id="ae8f8-195">Azure에서는 VM에 지정된 것과 동일한 저장소 계정을 통해 **모니터링**이 기본적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-195">Azure enables **Monitoring** by default with the same storage account designated for the VM.</span></span> <span data-ttu-id="ae8f8-196">여기에서 이러한 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-196">You can change these settings here.</span></span>
* <span data-ttu-id="ae8f8-197">**가용성 집합**아래에서 가용성 집합을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-197">Under **Availability set**, specify an availability set.</span></span> <span data-ttu-id="ae8f8-198">이 자습서에서는 **없음**을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-198">For the purposes of this tutorial, you can select **none**.</span></span> <span data-ttu-id="ae8f8-199">SQL AlwaysOn 가용성 그룹을 설정하려는 경우 가상 컴퓨터를 다시 만들지 않도록 가용성을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-199">If you plan to set up SQL AlwaysOn Availability Groups, configure the availability to avoid recreating the virtual machine.</span></span>  <span data-ttu-id="ae8f8-200">자세한 내용은 [Virtual Machines의 가용성 관리](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-200">For more information, see [Manage the Availability of Virtual Machines](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="ae8f8-201">이러한 설정 구성을 완료한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-201">When you are done configuring these settings, click **OK**.</span></span>

## <a name="4-configure-sql-server-settings"></a><span data-ttu-id="ae8f8-202">4. SQL Server 설정 구성</span><span class="sxs-lookup"><span data-stu-id="ae8f8-202">4. Configure SQL server settings</span></span>
<span data-ttu-id="ae8f8-203">**SQL Server 설정** 블레이드에서 SQL Server에 대한 설정 및 최적화를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-203">On the **SQL Server settings** blade, configure specific settings and optimizations for SQL Server.</span></span> <span data-ttu-id="ae8f8-204">SQL Server에 대해 구성할 수 있는 설정에는 다음과 같은 설정이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-204">The settings that you can configure for SQL Server include the following settings.</span></span>

| <span data-ttu-id="ae8f8-205">설정</span><span class="sxs-lookup"><span data-stu-id="ae8f8-205">Setting</span></span> |
| --- |
| [<span data-ttu-id="ae8f8-206">연결</span><span class="sxs-lookup"><span data-stu-id="ae8f8-206">Connectivity</span></span>](#connectivity) |
| [<span data-ttu-id="ae8f8-207">인증</span><span class="sxs-lookup"><span data-stu-id="ae8f8-207">Authentication</span></span>](#authentication) |
| [<span data-ttu-id="ae8f8-208">Storage 구성</span><span class="sxs-lookup"><span data-stu-id="ae8f8-208">Storage configuration</span></span>](#storage-configuration) |
| [<span data-ttu-id="ae8f8-209">자동화된 패치</span><span class="sxs-lookup"><span data-stu-id="ae8f8-209">Automated Patching</span></span>](#automated-patching) |
| [<span data-ttu-id="ae8f8-210">자동화된 Backup</span><span class="sxs-lookup"><span data-stu-id="ae8f8-210">Automated Backup</span></span>](#automated-backup) |
| [<span data-ttu-id="ae8f8-211">Azure Key Vault 통합</span><span class="sxs-lookup"><span data-stu-id="ae8f8-211">Azure Key Vault Integration</span></span>](#azure-key-vault-integration) |
| [<span data-ttu-id="ae8f8-212">R 서비스</span><span class="sxs-lookup"><span data-stu-id="ae8f8-212">R Services</span></span>](#r-services) |

### <a name="connectivity"></a><span data-ttu-id="ae8f8-213">연결</span><span class="sxs-lookup"><span data-stu-id="ae8f8-213">Connectivity</span></span>
<span data-ttu-id="ae8f8-214">**SQL 연결**에서 VM의 SQL Server 인스턴스에 대해 원하는 액세스 유형을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-214">Under **SQL connectivity**, specify the type of access you want to the SQL Server instance on this VM.</span></span> <span data-ttu-id="ae8f8-215">이 자습서에서는 **공개(인터넷)**를 지정하여 인터넷 상의 컴퓨터 또는 서비스에서 SQL Server로의 연결을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-215">For the purposes of this tutorial, select **Public (internet)** to allow connections to SQL Server from machines or services on the internet.</span></span> <span data-ttu-id="ae8f8-216">이 옵션을 선택하면 Azure에서는 포트 1433에서 트래픽을 허용하도록 방화벽 및 네트워크 보안 그룹을 자동으로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-216">With this option selected, Azure automatically configures the firewall and the network security group to allow traffic on port 1433.</span></span>  

![SQL 연결 옵션](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-connectivity-alt.png)

<span data-ttu-id="ae8f8-218">인터넷을 통해 SQL Server에 연결하려면 SQL Server 인증을 사용하도록 설정해야 합니다. 이 내용은 다음 섹션에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-218">To connect to SQL Server via the internet, you also must enable SQL Server Authentication, which is described in the next section.</span></span>

> [!NOTE]
> <span data-ttu-id="ae8f8-219">네트워크 통신에 대한 추가 제한을 SQL Server VM에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-219">It is possible to add more restrictions for the network communications to your SQL Server VM.</span></span> <span data-ttu-id="ae8f8-220">VM을 만든 후에 네트워크 보안 그룹을 편집하여 더 많은 제한을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-220">You can add more restrictions by editing the Network Security Group after the VM is created.</span></span> <span data-ttu-id="ae8f8-221">자세한 내용은 [NSG(네트워크 보안 그룹)란?](../../../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="ae8f8-221">For more information, see [What is a Network Security Group (NSG)?](../../../virtual-network/virtual-networks-nsg.md)</span></span>
> 
> 

<span data-ttu-id="ae8f8-222">인터넷을 통해 데이터베이스 엔진에 대한 연결을 사용하도록 설정하지 않으려면 다음 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-222">If you would prefer to not enable connections to the Database Engine via the internet, choose one of the following options:</span></span>

* <span data-ttu-id="ae8f8-223">**로컬(VM 내부만)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-223">**Local (inside VM only)** to allow connections to SQL Server only from within the VM.</span></span>
* <span data-ttu-id="ae8f8-224">**사설(Virtual Network 내)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-224">**Private (within Virtual Network)** to allow connections to SQL Server from machines or services in the same virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="ae8f8-225">SQL Server Express Edition용 가상 컴퓨터 이미지는 자동으로 TCP/IP 프로토콜을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-225">The virtual machine image for SQL Server Express edition does not automatically enable the TCP/IP protocol.</span></span> <span data-ttu-id="ae8f8-226">공용 및 개인 연결 옵션에 대해서도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-226">This is true even for the Public and  Private connectivity options.</span></span> <span data-ttu-id="ae8f8-227">Express Edition의 경우 VM을 만든 후에 SQL Server 구성 관리자를 사용하여 [수동으로 TCP/IP 프로토콜을 사용](#configure-sql-server-to-listen-on-the-tcp-protocol) 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-227">For Express edition, you must use SQL Server Configuration Manager to [manually enable the TCP/IP protocol](#configure-sql-server-to-listen-on-the-tcp-protocol) after creating the VM.</span></span>
> 
> 

<span data-ttu-id="ae8f8-228">일반적으로, 시나리오에 허용되는 가장 제한적인 연결을 선택하여 보안을 개선합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-228">In general, improve security by choosing the most restrictive connectivity that your scenario allows.</span></span> <span data-ttu-id="ae8f8-229">하지만 모든 옵션은 네트워크 보안 그룹 및 SQL/Windows 인증을 통해 보안을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-229">But all the options are securable through Network Security Group rules and SQL/Windows Authentication.</span></span>

<span data-ttu-id="ae8f8-230">**포트** 기본값은 1433입니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-230">**Port** defaults to 1433.</span></span> <span data-ttu-id="ae8f8-231">다른 포트 번호를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-231">You can specify a different port number.</span></span>
<span data-ttu-id="ae8f8-232">자세한 내용은 [SQL Server Virtual Machine에 연결(Resource Manager) | Microsoft Azure](virtual-machines-windows-sql-connect.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-232">For more information, see [Connect to a SQL Server Virtual Machine (Resource Manager) | Microsoft Azure](virtual-machines-windows-sql-connect.md).</span></span>

### <a name="authentication"></a><span data-ttu-id="ae8f8-233">인증</span><span class="sxs-lookup"><span data-stu-id="ae8f8-233">Authentication</span></span>
<span data-ttu-id="ae8f8-234">SQL Server 인증이 필요하도록 지정하려면 **사용** under **사용**을 방문하십시오.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-234">If you require SQL Server Authentication, click **Enable** under **SQL authentication**.</span></span>

![공개](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-authentication.png)

> [!NOTE]
> <span data-ttu-id="ae8f8-236">인터넷(즉, 공용 연결 옵션)을 통해 SQL Server에 액세스하려면 여기서 SQL 인증을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-236">If you plan to access SQL Server over the internet (that is, the Public connectivity option), you must enable SQL authentication here.</span></span> <span data-ttu-id="ae8f8-237">SQL Server에 대한 공용 액세스를 위해서는 SQL 인증을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-237">Public access to the SQL Server requires the use of SQL Authentication.</span></span>
> 
> 

<span data-ttu-id="ae8f8-238">SQL Server 인증을 사용하도록 설정하는 경우 **로그인 이름** 및 **암호**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-238">If you enable SQL Server Authentication, specify a **Login name** and **Password**.</span></span> <span data-ttu-id="ae8f8-239">이 사용자 이름은 SQL Server 인증 로그인 및 **sysadmin** 고정된 서버 역할의 구성원으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-239">This user name is configured as a SQL Server Authentication login and member of the **sysadmin** fixed server role.</span></span> <span data-ttu-id="ae8f8-240">인증 모드에 대한 자세한 내용은 [인증 모드 선택](http://msdn.microsoft.com/library/ms144284.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-240">For more information about Authentication Modes, see [Choose an Authentication Mode](http://msdn.microsoft.com/library/ms144284.aspx).</span></span>

<span data-ttu-id="ae8f8-241">SQL Server 인증을 사용하도록 설정하지 않으면, VM의 로컬 관리자 계정을 사용하여 SQL Server 인스턴스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-241">If you do not enable SQL Server Authentication, then you can use the local Administrator account on the VM to connect to the SQL Server instance.</span></span>

### <a name="storage-configuration"></a><span data-ttu-id="ae8f8-242">Storage 구성</span><span class="sxs-lookup"><span data-stu-id="ae8f8-242">Storage configuration</span></span>
<span data-ttu-id="ae8f8-243">저장소 요구 사항을 지정하려면 **Storage 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-243">Click **Storage configuration** to specify the storage requirements.</span></span>

![SQL 저장소 구성](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-storage.png)

> [!NOTE]
> <span data-ttu-id="ae8f8-245">표준 저장소를 선택하면, 이 옵션을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-245">If you select Standard storage, this option is not available.</span></span> <span data-ttu-id="ae8f8-246">자동 저장소 최적화는 Premium Storage에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-246">Automatic storage optimization is available only for Premium Storage.</span></span>
> 
> 

<span data-ttu-id="ae8f8-247">초당 입/출력 작업(IOPs), 처리량(MB/s) 및 총 저장소 크기로 요구 사항을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-247">You can specify requirements as input/output operations per second (IOPs), throughput in MB/s, and total storage size.</span></span> <span data-ttu-id="ae8f8-248">슬라이딩 규모를 사용하여 이 값을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-248">Configure these values by using the sliding scales.</span></span> <span data-ttu-id="ae8f8-249">포털에는 이러한 요구 사항에 따라 디스크 수를 자동으로 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-249">The portal automatically calculates the number of disks based on these requirements.</span></span>

<span data-ttu-id="ae8f8-250">기본적으로 Azure에서는 5000 IOPs, 200MBs 및 1TB의 저장소 공간에 대해 저장소를 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-250">By default, Azure optimizes the storage for 5000 IOPs, 200 MBs, and 1 TB of storage space.</span></span> <span data-ttu-id="ae8f8-251">워크로드에 따라 이러한 저장소 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-251">You can change these storage settings based on workload.</span></span> <span data-ttu-id="ae8f8-252">**다음에 대해 저장소 최적화**에서 다음 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-252">Under **Storage optimized for**, select one of the following options:</span></span>

* <span data-ttu-id="ae8f8-253">**일반**은 기본 설정이며 대부분의 워크로드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-253">**General** is the default setting and supports most workloads.</span></span>
* <span data-ttu-id="ae8f8-254">**트랜잭션** 처리는 기존의 데이터베이스 OLTP 워크로드용으로 저장소를 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-254">**Transactional** processing optimizes the storage for traditional database OLTP workloads.</span></span>
* <span data-ttu-id="ae8f8-255">**데이터 웨어하우징** 은 분석 및 보고 워크로드용으로 저장소를 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-255">**Data warehousing** optimizes the storage for analytic and reporting workloads.</span></span>

> [!NOTE]
> <span data-ttu-id="ae8f8-256">슬라이더에 대한 상한값은 선택한 가상 컴퓨터 크기에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-256">The upper limits on the sliders vary depending on your selected virtual machine size.</span></span>
> 
> 

### <a name="automated-patching"></a><span data-ttu-id="ae8f8-257">자동화된 패치</span><span class="sxs-lookup"><span data-stu-id="ae8f8-257">Automated patching</span></span>
<span data-ttu-id="ae8f8-258">**Automated patching**이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-258">**Automated patching** is enabled by default.</span></span> <span data-ttu-id="ae8f8-259">Azure에서는 자동화된 패치를 통해 SQL Server와 운영 체제를 자동으로 패치합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-259">Automated patching allows Azure to automatically patch SQL Server and the operating system.</span></span> <span data-ttu-id="ae8f8-260">요일, 시간 및 유지 관리 기간에 대한 날짜를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-260">Specify a day of the week, time, and duration for a maintenance window.</span></span> <span data-ttu-id="ae8f8-261">Azure에서 유지 관리 기간에 패치를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-261">Azure performs patching in this maintenance window.</span></span> <span data-ttu-id="ae8f8-262">유지 관리 기간 일정에서는 VM 로캘 시간을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-262">The maintenance window schedule uses the VM locale for time.</span></span> <span data-ttu-id="ae8f8-263">Azure에서 SQL Server와 운영 체제를 자동으로 패치하지 않으려면 **사용 안 함**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-263">If you do not want Azure to automatically patch SQL Server and the operating system, click **Disable**.</span></span>  

![SQL 자동화된 패치](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-patching.png)

<span data-ttu-id="ae8f8-265">자세한 내용은 [Azure Virtual Machines에서 SQL Server의 자동화된 패치](virtual-machines-windows-sql-automated-patching.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-265">For more information, see [Automated Patching for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-automated-patching.md).</span></span>

### <a name="automated-backup"></a><span data-ttu-id="ae8f8-266">자동화된 백업</span><span class="sxs-lookup"><span data-stu-id="ae8f8-266">Automated backup</span></span>
<span data-ttu-id="ae8f8-267">**자동화된 백업**에서 모든 데이터베이스에 대해 자동 데이터베이스 백업을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-267">Enable automatic database backups for all databases under **Automated backup**.</span></span> <span data-ttu-id="ae8f8-268">자동화된 백업은 기본적으로 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-268">Automated backup is disabled by default.</span></span>

<span data-ttu-id="ae8f8-269">SQL 자동화된 백업을 사용하도록 설정하면 다음 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-269">When you enable SQL automated backup, you can configure the following settings:</span></span>

* <span data-ttu-id="ae8f8-270">백업에 대한 보존 기간(일)</span><span class="sxs-lookup"><span data-stu-id="ae8f8-270">Retention period (days) for backups</span></span>
* <span data-ttu-id="ae8f8-271">백업에 사용할 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="ae8f8-271">Storage account to use for backups</span></span>
* <span data-ttu-id="ae8f8-272">백업을 위한 암호화 옵션 및 암호</span><span class="sxs-lookup"><span data-stu-id="ae8f8-272">Encryption option and password for backups</span></span>
* <span data-ttu-id="ae8f8-273">시스템 데이터베이스 백업</span><span class="sxs-lookup"><span data-stu-id="ae8f8-273">Backup system databases</span></span>
* <span data-ttu-id="ae8f8-274">백업 일정 구성</span><span class="sxs-lookup"><span data-stu-id="ae8f8-274">Configure backup schedule</span></span>

<span data-ttu-id="ae8f8-275">백업을 암호화하려면 **사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-275">To encrypt the backup, click **Enable**.</span></span> <span data-ttu-id="ae8f8-276">그 다음 **암호**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-276">Then specify the **Password**.</span></span> <span data-ttu-id="ae8f8-277">Azure에서는 백업을 암호화할 인증서를 만들고 지정된 암호를 사용하여 인증서를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-277">Azure creates a certificate to encrypt the backups and uses the specified password to protect that certificate.</span></span>

![SQL 자동화된 Backup](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-autobackup2.png)

 <span data-ttu-id="ae8f8-279">자세한 내용은 [Azure Virtual Machines에서 SQL Server에 대한 자동화된 Backup](virtual-machines-windows-sql-automated-backup.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-279">For more information, see [Automated Backup for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).</span></span>

### <a name="azure-key-vault-integration"></a><span data-ttu-id="ae8f8-280">Azure Key Vault 통합</span><span class="sxs-lookup"><span data-stu-id="ae8f8-280">Azure Key Vault integration</span></span>
<span data-ttu-id="ae8f8-281">Azure에서 암호화를 위한 보안 암호를 저장하려면 **Azure Key Vault 통합**을 클릭하고 **사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-281">To store security secrets in Azure for encryption, click **Azure key vault integration** and click **Enable**.</span></span>

![SQL Azure Key Vault 통합](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-akv.png)

<span data-ttu-id="ae8f8-283">다음 표에서는 Azure Key Vault 통합을 구성하는 데 필요한 매개 변수를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-283">The following table lists the parameters required to configure Azure Key Vault Integration.</span></span>

| <span data-ttu-id="ae8f8-284">매개 변수</span><span class="sxs-lookup"><span data-stu-id="ae8f8-284">PARAMETER</span></span> | <span data-ttu-id="ae8f8-285">설명</span><span class="sxs-lookup"><span data-stu-id="ae8f8-285">DESCRIPTION</span></span> | <span data-ttu-id="ae8f8-286">예제</span><span class="sxs-lookup"><span data-stu-id="ae8f8-286">EXAMPLE</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ae8f8-287">**주요 자격 증명 모음 URL**</span><span class="sxs-lookup"><span data-stu-id="ae8f8-287">**Key Vault URL**</span></span> |<span data-ttu-id="ae8f8-288">주요 자격 증명 모음의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-288">The location of the key vault.</span></span> |<span data-ttu-id="ae8f8-289">https://contosokeyvault.vault.azure.net/</span><span class="sxs-lookup"><span data-stu-id="ae8f8-289">https://contosokeyvault.vault.azure.net/</span></span> |
| <span data-ttu-id="ae8f8-290">**주체 이름**</span><span class="sxs-lookup"><span data-stu-id="ae8f8-290">**Principal name**</span></span> |<span data-ttu-id="ae8f8-291">Azure Active Directory 서비스 주체 이름.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-291">Azure Active Directory service principal name.</span></span> <span data-ttu-id="ae8f8-292">이 이름을 클라이언트 ID라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-292">This name is also referred to as the Client ID.</span></span> |<span data-ttu-id="ae8f8-293">fde2b411-33d5-4e11-af04eb07b669ccf2</span><span class="sxs-lookup"><span data-stu-id="ae8f8-293">fde2b411-33d5-4e11-af04eb07b669ccf2</span></span> |
| <span data-ttu-id="ae8f8-294">**주체 암호**</span><span class="sxs-lookup"><span data-stu-id="ae8f8-294">**Principal secret**</span></span> |<span data-ttu-id="ae8f8-295">Azure Active Directory 서비스 주체 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-295">Azure Active Directory service principal secret.</span></span> <span data-ttu-id="ae8f8-296">이 암호를 클라이언트 암호라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-296">This secret is also referred to as the Client Secret.</span></span> |<span data-ttu-id="ae8f8-297">9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM=</span><span class="sxs-lookup"><span data-stu-id="ae8f8-297">9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM=</span></span> |
| <span data-ttu-id="ae8f8-298">**자격 증명 이름**</span><span class="sxs-lookup"><span data-stu-id="ae8f8-298">**Credential name**</span></span> |<span data-ttu-id="ae8f8-299">**자격 증명 이름**: AKV 통합은 VM이 주요 자격 증명 모음에 액세스할 수 있도록 SQL Server 내에 자격 증명을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-299">**Credential name**: AKV Integration creates a credential within SQL Server, allowing the VM to have access to the key vault.</span></span> <span data-ttu-id="ae8f8-300">이 자격 증명의 이름을 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-300">Choose a name for this credential.</span></span> |<span data-ttu-id="ae8f8-301">mycred1</span><span class="sxs-lookup"><span data-stu-id="ae8f8-301">mycred1</span></span> |

<span data-ttu-id="ae8f8-302">자세한 내용은 [Azure VM에서 SQL Server에 대한 Azure Key Vault 통합 구성](virtual-machines-windows-ps-sql-keyvault.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-302">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs](virtual-machines-windows-ps-sql-keyvault.md).</span></span>

<span data-ttu-id="ae8f8-303">SQL Server 설정 구성을 마치면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-303">When you are finished configuring SQL Server settings, click **OK**.</span></span>

### <a name="r-services"></a><span data-ttu-id="ae8f8-304">R 서비스</span><span class="sxs-lookup"><span data-stu-id="ae8f8-304">R services</span></span>
<span data-ttu-id="ae8f8-305">[SQL Server R 서비스](https://msdn.microsoft.com/library/mt604845.aspx)를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-305">You can enable [SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx).</span></span> <span data-ttu-id="ae8f8-306">SQL Server R 서비스를 사용하면 SQL Server 2016에서 고급 분석을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-306">SQL Server R Services enables you to use advanced analytics with SQL Server 2016.</span></span> <span data-ttu-id="ae8f8-307">**사용** on the **SQL Server Settings** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-307">Click **Enable** on the **SQL Server Settings** blade.</span></span>

![SQL Server R 서비스 사용](./media/virtual-machines-windows-portal-sql-server-provision/azure-vm-sql-server-r-services.png)


## <a name="5-review-the-summary"></a><span data-ttu-id="ae8f8-309">5. 요약 검토</span><span class="sxs-lookup"><span data-stu-id="ae8f8-309">5. Review the summary</span></span>
<span data-ttu-id="ae8f8-310">**요약** 블레이드에서 요약을 검토하고 **확인**을 클릭하여 이 VM에 대해 지정된 SQL Server, 리소스 그룹 및 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-310">On the **Summary** blade, review the summary and click **OK** to create SQL Server, resource group, and resources specified for this VM.</span></span>

<span data-ttu-id="ae8f8-311">Azure 포털에서 배포를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-311">You can monitor the deployment from the azure portal.</span></span> <span data-ttu-id="ae8f8-312">화면 맨 위에 있는 **알림** 단추는 배포의 기본 상태를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-312">The **Notifications** button at the top of the screen shows basic status of the deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="ae8f8-313">배포 시간에 대한 정보를 제공하기 위해 SQL VM을 미국 동부 지역에 기본 설정을 사용하여 배포해 두었습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-313">To provide you with an idea on deployment times, I deployed a SQL VM to the East US region with default settings.</span></span> <span data-ttu-id="ae8f8-314">이 테스트 배포는 완료하기까지 총 26분이 소요되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-314">This test deployment took a total of 26 minutes to complete.</span></span> <span data-ttu-id="ae8f8-315">사용자의 지역 및 선택한 설정에 따라서 배포 시간이 더 빠르거나 늦을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-315">But you might experience a faster or slower deployment time based on your region and selected settings.</span></span>
> 
> 

## <a name="open-the-vm-with-remote-desktop"></a><span data-ttu-id="ae8f8-316">원격 데스크톱을 사용하여 VM 열기</span><span class="sxs-lookup"><span data-stu-id="ae8f8-316">Open the VM with Remote Desktop</span></span>
<span data-ttu-id="ae8f8-317">다음 단계를 사용하여 원격 데스크톱으로 가상 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-317">Use the following steps to connect to the virtual machine with Remote Desktop:</span></span>

1. <span data-ttu-id="ae8f8-318">Azure VM이 작성되면, VM에 대한 아이콘이 Azure 대시보드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-318">After the Azure VM is built, the icon for the VM appears on your Azure dashboard.</span></span> <span data-ttu-id="ae8f8-319">기존 가상 컴퓨터를 검색하여 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-319">You can also find it by browsing your existing virtual machines.</span></span> <span data-ttu-id="ae8f8-320">새 SQL 가상 컴퓨터를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-320">Click on your new SQL virtual machine.</span></span> <span data-ttu-id="ae8f8-321">**가상 컴퓨터** 블레이드에 가상 컴퓨터 세부 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-321">A **Virtual machine** blade displays your virtual machine details.</span></span>
2. <span data-ttu-id="ae8f8-322">**가상 컴퓨터** 블레이드 위에 있는 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-322">At the top of the **Virtual machine** blade, click **Connect**.</span></span>
3. <span data-ttu-id="ae8f8-323">브라우저가 VM에 대한 RDP 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-323">The browser downloads an RDP file for the VM.</span></span> <span data-ttu-id="ae8f8-324">RDP 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-324">Open the RDP file.</span></span>
    <span data-ttu-id="ae8f8-325">![SQL VM에 원격 데스크톱 연결](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-remote-desktop.png)</span><span class="sxs-lookup"><span data-stu-id="ae8f8-325">![Remote Desktop to SQL VM](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-remote-desktop.png)</span></span>
4. <span data-ttu-id="ae8f8-326">원격 데스크톱 연결이 이 원격 연결의 게시자를 식별할 수 없다고 알립니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-326">The Remote Desktop Connection notifies you that the publisher of this remote connection cannot be identified.</span></span> <span data-ttu-id="ae8f8-327">**연결** 을 클릭하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-327">Click **Connect** to continue.</span></span>
5. <span data-ttu-id="ae8f8-328">**Windows 보안** 대화 상자에서 **다른 계정 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-328">In the **Windows Security** dialog, click **Use another account**.</span></span>
6. <span data-ttu-id="ae8f8-329">**사용자 이름**에 **\<user name>**을 입력합니다. 여기서 <user name>은(는) VM을 구성할 때 지정한 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-329">For **User name** type **\<user name>**, where <user name> is the user name that you specified when you configured the VM.</span></span> <span data-ttu-id="ae8f8-330">이름 앞에 초기 백슬래시를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-330">You have to add an initial backslash before the name.</span></span>
7. <span data-ttu-id="ae8f8-331">이전에 구성한 이 VM의 **암호**를 입력한 다음 **확인**을 클릭하여 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-331">Type the **Password** that you previously configured for this VM, and then click **OK** to connect.</span></span>
8. <span data-ttu-id="ae8f8-332">다른 **원격 데스크톱 연결** 대화 상자가 연결 여부를 물어보면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-332">If another **Remote Desktop Connection** dialog asks you whether to connect, click **Yes**.</span></span>

<span data-ttu-id="ae8f8-333">SQL Server 가상 컴퓨터에 연결된 후에, SQL Server Management Studio를 시작하고 로컬 관리자 자격 증명을 사용하여 Windows 인증으로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-333">After you connect to the SQL Server virtual machine, you can launch SQL Server Management Studio and connect with Windows Authentication using your local administrator credentials.</span></span> <span data-ttu-id="ae8f8-334">SQL Server 인증을 사용하도록 설정한 경우에는, 프로비전 중에 구성해 놓은 SQL 로그인 및 암호를 사용하여 SQL 인증에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-334">If you enabled SQL Server Authentication, you can also connect with SQL Authentication using the SQL login and password you configured during provisioning.</span></span>

<span data-ttu-id="ae8f8-335">컴퓨터에 연결하면 요구 사항에 따라 컴퓨터와 SQL Server 설정을 직접 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-335">Access to the machine enables you to directly change machine and SQL Server settings based on your requirements.</span></span> <span data-ttu-id="ae8f8-336">예를 들어, 방화벽 설정을 구성하거나 SQL Server 구성 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-336">For example, you could configure the firewall settings or change SQL Server configuration settings.</span></span>

## <a name="connect-to-sql-server-remotely"></a><span data-ttu-id="ae8f8-337">원격으로 SQL Server 연결</span><span class="sxs-lookup"><span data-stu-id="ae8f8-337">Connect to SQL Server remotely</span></span>
<span data-ttu-id="ae8f8-338">이 자습서에서는 가상 컴퓨터와 **SQL Server 인증**에 대해 **공용** 액세스를 선택했습니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-338">In this tutorial, we selected **Public** access for the virtual machine and **SQL Server Authentication**.</span></span> <span data-ttu-id="ae8f8-339">이러한 설정은 가상 컴퓨터가 인터넷을 통한 모든 클라이언트의 SQL Server 연결을 허용하도록 자동으로 구성합니다(올바른 SQL 로그인이 있다는 가정 하에).</span><span class="sxs-lookup"><span data-stu-id="ae8f8-339">These settings automatically configured the virtual machine to allow SQL Server connections from any client over the internet (assuming they have the correct SQL login).</span></span>

> [!NOTE]
> <span data-ttu-id="ae8f8-340">프로비전 중에 공용을 선택하지 않은 경우 인터넷을 통한 SQL Server 인스턴스 액세스에 추가 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-340">If you did not select Public during provisioning, then extra steps are required to access your SQL Server instance over the internet.</span></span> <span data-ttu-id="ae8f8-341">자세한 내용은 [SQL Server 가상 컴퓨터에 연결](virtual-machines-windows-sql-connect.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-341">For more information, see  [Connect to a SQL Server Virtual Machine](virtual-machines-windows-sql-connect.md).</span></span>
> 
> 

<span data-ttu-id="ae8f8-342">다음 섹션은 인터넷 상의 다른 컴퓨터에서 VM의 SQL Server 인스턴스에 연결하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-342">The following sections show how to connect to your SQL Server instance on your VM from a different computer over the internet.</span></span>

> [!INCLUDE [Connect to SQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ae8f8-343">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ae8f8-343">Next Steps</span></span>
<span data-ttu-id="ae8f8-344">Azure에서 SQL Server를 사용하는 방법에 대한 기타 정보는 [Azure Virtual Machines의 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md) 및 [질문과 대답](virtual-machines-windows-sql-server-iaas-faq.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-344">For other information about using SQL Server in Azure, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md) and the [Frequently Asked Questions](virtual-machines-windows-sql-server-iaas-faq.md).</span></span>

<span data-ttu-id="ae8f8-345">Azure Virtual Machines의 SQL Server에 대한 비디오 개요는 [Azure VM은 SQL Server 2016에 가장 적합한 플랫폼입니다.](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016)를 시청하세요.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-345">For a video overview of SQL Server on Azure Virtual Machines, watch [Azure VM is the best platform for SQL Server 2016](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016).</span></span>

<span data-ttu-id="ae8f8-346">Azure Virtual Machines에서 SQL Server용 [학습 경로를 탐색](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae8f8-346">[Explore the Learning Path](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) for SQL Server on Azure virtual machines.</span></span>

