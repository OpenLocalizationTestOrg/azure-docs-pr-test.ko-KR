---
title: "SQL Server 가상 컴퓨터 프로비전 | Microsoft Docs"
description: "포털을 사용하여 Azure에서 SQL Server 가상 컴퓨터를 만들고 연결하기. 이 자습서는 리소스 관리자 모드를 사용합니다."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 1aff691f-a40a-4de2-b6a0-def1384e086e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: jroth
ms.openlocfilehash: c923f9aae4c7a1b8bd4f5760d0ec4f33923b9321
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="provision-a-sql-server-virtual-machine-in-the-azure-portal"></a><span data-ttu-id="2ad41-104">Azure Portal에서 SQL Server 가상 컴퓨터 프로비저닝</span><span class="sxs-lookup"><span data-stu-id="2ad41-104">Provision a SQL Server virtual machine in the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2ad41-105">포털</span><span class="sxs-lookup"><span data-stu-id="2ad41-105">Portal</span></span>](virtual-machines-windows-portal-sql-server-provision.md)
> * [<span data-ttu-id="2ad41-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ad41-106">PowerShell</span></span>](virtual-machines-windows-ps-sql-create.md)
> 
> 

<span data-ttu-id="2ad41-107">이 종단간 자습서는 Azure Portal을 사용하여 SQL Server를 실행하는 가상 컴퓨터를 프로비전하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-107">This end-to-end tutorial shows you how to use the Azure portal to provision a virtual machine running SQL Server.</span></span>

<span data-ttu-id="2ad41-108">Azure 가상 컴퓨터(VM) 갤러리에는 Microsoft SQL Server가 포함된 몇 개의 이미지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-108">The Azure virtual machine (VM) gallery includes several images that contain Microsoft SQL Server.</span></span> <span data-ttu-id="2ad41-109">클릭 몇 번으로, 갤러리에서 SQL VM 이미지 중 하나를 선택하고 Azure 환경에 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-109">With a few clicks, you can select one of the SQL VM images from the gallery and provision it in your Azure environment.</span></span>

<span data-ttu-id="2ad41-110">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-110">In this tutorial, you will:</span></span>

* [<span data-ttu-id="2ad41-111">갤러리에서 SQL VM 이미지 선택</span><span class="sxs-lookup"><span data-stu-id="2ad41-111">Select a SQL VM image from the gallery</span></span>](#select-a-sql-vm-image-from-the-gallery)
* [<span data-ttu-id="2ad41-112">VM 구성 및 만들기</span><span class="sxs-lookup"><span data-stu-id="2ad41-112">Configure and create the VM</span></span>](#configure-the-vm)
* [<span data-ttu-id="2ad41-113">원격 데스크톱을 사용하여 VM 열기</span><span class="sxs-lookup"><span data-stu-id="2ad41-113">Open the VM with Remote Desktop</span></span>](#open-the-vm-with-remote-desktop)
* [<span data-ttu-id="2ad41-114">원격으로 SQL Server 연결</span><span class="sxs-lookup"><span data-stu-id="2ad41-114">Connect to SQL Server remotely</span></span>](#connect-to-sql-server-remotely)

## <a name="select-a-sql-vm-image-from-the-gallery"></a><span data-ttu-id="2ad41-115">갤러리에서 SQL VM 이미지 선택</span><span class="sxs-lookup"><span data-stu-id="2ad41-115">Select a SQL VM image from the gallery</span></span>

1. <span data-ttu-id="2ad41-116">사용자 계정을 사용하여 [Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-116">Log in to the [Azure portal](https://portal.azure.com) using your account.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2ad41-117">Azure 계정이 없는 경우 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)을 방문하십시오.</span><span class="sxs-lookup"><span data-stu-id="2ad41-117">If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

2. <span data-ttu-id="2ad41-118">Azure Portal에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-118">On the Azure portal, click **New**.</span></span> <span data-ttu-id="2ad41-119">포털에 **새** 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-119">The portal opens the **New** window.</span></span>

3. <span data-ttu-id="2ad41-120">**새로 만들기** 창에서 **Compute**를 클릭한 다음 **모두 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-120">In the **New** window, click **Compute** and then click **See all**.</span></span>

   ![새 계산 창](./media/virtual-machines-windows-portal-sql-server-provision/azure-new-compute-blade.png)

4. <span data-ttu-id="2ad41-122">검색 필드에 **SQL Server**를 입력하고 ENTER 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-122">In the search field, type **SQL Server**, and press ENTER.</span></span>

5. <span data-ttu-id="2ad41-123">그런 다음, **필터** 아이콘을 클릭하고 게시자로 **Microsoft**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-123">Then click the **Filter** icon and select **Microsoft** for the publisher.</span></span> <span data-ttu-id="2ad41-124">필터 창에서 **완료**를 클릭하여 결과를 Microsoft 게시 SQL Server 이미지로 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-124">Click **Done** on the filter window to filter the results to Microsoft published SQL Server images.</span></span>

   ![Azure Virtual Machines 창](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-blade2.png)

5. <span data-ttu-id="2ad41-126">사용 가능한 SQL Server 이미지를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-126">Review the available SQL Server images.</span></span> <span data-ttu-id="2ad41-127">각 이미지는 SQL Server 버전 및 운영 체제를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-127">Each image identifies a SQL Server version and an operating system.</span></span>

6. <span data-ttu-id="2ad41-128">**무료 라이선스: Windows Server 2016에서 SQL Server 2016 SP1 Developer**용 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-128">Select the image named **Free License: SQL Server 2016 SP1 Developer on Windows Server 2016**.</span></span>

   > [!TIP]
   > <span data-ttu-id="2ad41-129">Developer 버전은 개발 테스트 목적으로 무료로 제공되는 SQL Server의 모든 기능을 갖춘 버전이므로 이 자습서에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-129">The Developer edition is used in this tutorial because it is a full-featured edition of SQL Server that is free for development testing purposes.</span></span> <span data-ttu-id="2ad41-130">VM 실행 비용에 대해서만 비용을 지불합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-130">You pay only for the cost of running the VM.</span></span> <span data-ttu-id="2ad41-131">그러나 이 자습서에 사용할 이미지를 자유롭게 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-131">However, you are free to choose any of the images to use in this tutorial.</span></span>

   > [!TIP]
   > <span data-ttu-id="2ad41-132">SQL VM 이미지는 만든 VM의 분당 가격에 SQL Server에 대한 라이선스 비용을 포함합니다(Developer 및 Express 버전 제외).</span><span class="sxs-lookup"><span data-stu-id="2ad41-132">SQL VM images include the licensing costs for SQL Server into the per-minute pricing of the VM you create (except for the Developer and Express editions).</span></span> <span data-ttu-id="2ad41-133">SQL Server Developer는 개발/테스트(비 프로덕션)에 대해 무료이며 SQL Express는 간단한 작업(1GB 미만의 메모리, 10GB 미만의 저장소)에 대해 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-133">SQL Server Developer is free for development/testing (not production) and SQL Express is free for lightweight workloads (less than 1GB memory, less than 10 GB storage).</span></span> <span data-ttu-id="2ad41-134">BYOL(Bring Your Own License) 및 VM에 대해서만 지불에 대한 또 다른 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-134">There is another option to bring-your-own-license (BYOL) and pay only for the VM.</span></span> <span data-ttu-id="2ad41-135">이러한 이미지 이름에는 접두사 {BYOL}이 붙습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-135">Those image names are prefixed with {BYOL}.</span></span> 
   >
   > <span data-ttu-id="2ad41-136">이러한 옵션에 대한 자세한 내용은 [SQL Server Azure VM에 대한 가격 책정 지침](virtual-machines-windows-sql-server-pricing-guidance.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ad41-136">For more information on these options, see [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md).</span></span>

7. <span data-ttu-id="2ad41-137">**배포 모델 선택**에서 **리소스 관리자**가 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-137">Under **Select a deployment model**, verify that **Resource Manager** is selected.</span></span> <span data-ttu-id="2ad41-138">리소스 관리자는 새로운 가상 컴퓨터에 권장되는 배포 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-138">Resource Manager is the recommended deployment model for new virtual machines.</span></span> 

8. <span data-ttu-id="2ad41-139">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-139">Click **Create**.</span></span>

    ![리소스 관리자로 SQL VM 만들기](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-sql-deployment-model.png)

## <a name="configure-the-vm"></a><span data-ttu-id="2ad41-141">VM 구성</span><span class="sxs-lookup"><span data-stu-id="2ad41-141">Configure the VM</span></span>
<span data-ttu-id="2ad41-142">SQL Server 가상 컴퓨터를 구성하기 위한 5개의 창이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-142">There are five windows for configuring a SQL Server virtual machine.</span></span>

| <span data-ttu-id="2ad41-143">단계</span><span class="sxs-lookup"><span data-stu-id="2ad41-143">Step</span></span> | <span data-ttu-id="2ad41-144">설명</span><span class="sxs-lookup"><span data-stu-id="2ad41-144">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2ad41-145">**기본 사항**</span><span class="sxs-lookup"><span data-stu-id="2ad41-145">**Basics**</span></span> |[<span data-ttu-id="2ad41-146">기본 설정 구성</span><span class="sxs-lookup"><span data-stu-id="2ad41-146">Configure basic settings</span></span>](#1-configure-basic-settings) |
| <span data-ttu-id="2ad41-147">**크기**</span><span class="sxs-lookup"><span data-stu-id="2ad41-147">**Size**</span></span> |[<span data-ttu-id="2ad41-148">가상 컴퓨터 크기 선택</span><span class="sxs-lookup"><span data-stu-id="2ad41-148">Choose virtual machine size</span></span>](#2-choose-virtual-machine-size) |
| <span data-ttu-id="2ad41-149">**설정**</span><span class="sxs-lookup"><span data-stu-id="2ad41-149">**Settings**</span></span> |[<span data-ttu-id="2ad41-150">선택적 기능 구성</span><span class="sxs-lookup"><span data-stu-id="2ad41-150">Configure optional features</span></span>](#3-configure-optional-features) |
| <span data-ttu-id="2ad41-151">**SQL 서버 설정**</span><span class="sxs-lookup"><span data-stu-id="2ad41-151">**SQL Server settings**</span></span> |[<span data-ttu-id="2ad41-152">SQL Server 설정 구성</span><span class="sxs-lookup"><span data-stu-id="2ad41-152">Configure SQL server settings</span></span>](#4-configure-sql-server-settings) |
| <span data-ttu-id="2ad41-153">**요약**</span><span class="sxs-lookup"><span data-stu-id="2ad41-153">**Summary**</span></span> |[<span data-ttu-id="2ad41-154">요약 검토</span><span class="sxs-lookup"><span data-stu-id="2ad41-154">Review the summary</span></span>](#5-review-the-summary) |

## <a name="1-configure-basic-settings"></a><span data-ttu-id="2ad41-155">1. 기본 설정 구성</span><span class="sxs-lookup"><span data-stu-id="2ad41-155">1. Configure basic settings</span></span>

<span data-ttu-id="2ad41-156">**기본** 창에서 다음 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-156">On the **Basics** window, provide the following information:</span></span>

* <span data-ttu-id="2ad41-157">고유한 가상 컴퓨터 **이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-157">Enter a unique virtual machine **Name**.</span></span>

* <span data-ttu-id="2ad41-158">최적의 성능을 위해 VM 디스크 유형에 **SSD**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-158">Select **SSD** for VM disk type for optimal performance.</span></span>

* <span data-ttu-id="2ad41-159">VM의 로컬 관리자 계정에 대한 **사용자 이름**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-159">Specify a **User name** for the local administrator account on the VM.</span></span> <span data-ttu-id="2ad41-160">이 계정은 SQL Server **sysadmin** 고정 서버 역할에도 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-160">This account is also added to the SQL Server **sysadmin** fixed server role.</span></span>

* <span data-ttu-id="2ad41-161">강력한 **암호**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-161">Provide a strong **Password**.</span></span>

* <span data-ttu-id="2ad41-162">구독이 여러 개인 경우 구독이 새 VM에 대해 올바른지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-162">If you have multiple subscriptions, verify that the subscription is correct for the new VM.</span></span>

* <span data-ttu-id="2ad41-163">**리소스 그룹** 상자에 새 리소스 그룹의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-163">In the **Resource group** box, type a name for a new resource group.</span></span> <span data-ttu-id="2ad41-164">또는 기존 리소스 그룹을 사용하려면 **기존 항목 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-164">Alternatively, to use an existing resource group click **Use existing**.</span></span> <span data-ttu-id="2ad41-165">리소스 그룹은 Azure 내 관련 리소스의 컬렉션입니다(가상 컴퓨터, 저장소 계정, 가상 네트워크 등).</span><span class="sxs-lookup"><span data-stu-id="2ad41-165">A resource group is a collection of related resources in Azure (virtual machines, storage accounts, virtual networks, etc.).</span></span>

  > [!NOTE]
  > <span data-ttu-id="2ad41-166">새 리소스 그룹을 사용하면 Azure에서 SQL Server 배포를 테스트하거나 알아보는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-166">Using a new resource group is helpful if you are just testing or learning about SQL Server deployments in Azure.</span></span> <span data-ttu-id="2ad41-167">테스트를 완료한 후 리소스 그룹을 삭제하면 VM과 해당 리소스 그룹과 연결된 모든 리소스가 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-167">After you finish with your test, delete the resource group to automatically delete the VM and all resources associated with that resource group.</span></span> <span data-ttu-id="2ad41-168">리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../../../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ad41-168">For more information about resource groups, see [Azure Resource Manager Overview](../../../azure-resource-manager/resource-group-overview.md).</span></span>

* <span data-ttu-id="2ad41-169">이 배포를 호스팅할 Azure 지역에 **위치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-169">Select a **Location** for the Azure region that will host this deployment.</span></span>

* <span data-ttu-id="2ad41-170">**확인**을 클릭하여 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-170">Click **OK** to save the settings.</span></span>

    ![SQL 기본 창](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-basic.png)

## <a name="2-choose-virtual-machine-size"></a><span data-ttu-id="2ad41-172">2. 가상 컴퓨터 크기 선택</span><span class="sxs-lookup"><span data-stu-id="2ad41-172">2. Choose virtual machine size</span></span>

<span data-ttu-id="2ad41-173">**크기** 단계의 **크기 선택** 창에서 가상 컴퓨터 크기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-173">On the **Size** step, choose a virtual machine size in the **Choose a size** window.</span></span> <span data-ttu-id="2ad41-174">창은 선택한 이미지를 기반으로 권장되는 컴퓨터 크기를 처음에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-174">The window initially displays recommended machine sizes based on the image you selected.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2ad41-175">**크기 선택** 창에 표시된 월별 예상 비용에는 SQL Server 라이선스 비용이 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-175">The estimated monthly cost displayed on the **Choose a size** window does not include SQL Server licensing costs.</span></span> <span data-ttu-id="2ad41-176">이것은 VM만의 비용입니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-176">This is the cost of the VM alone.</span></span> <span data-ttu-id="2ad41-177">SQL Server의 Express 및 Developer 버전의 경우, 이것은 총 예상 비용입니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-177">For the Express and Developer editions of SQL Server, this is the total estimated cost.</span></span> <span data-ttu-id="2ad41-178">다른 버전의 경우 [Windows Virtual Machines 가격 책정 페이지](https://azure.microsoft.com/pricing/details/virtual-machines/windows/)를 참조하여 SQL Server의 대상 버전을 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="2ad41-178">For other editions, see the [Windows Virtual Machines pricing page](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) and select your target edition of SQL Server.</span></span> <span data-ttu-id="2ad41-179">또한 [SQL Server Azure VM에 대한 가격 책정 지침](virtual-machines-windows-sql-server-pricing-guidance.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ad41-179">Also see the [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md).</span></span>

![SQL VM 크기 옵션](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-choose-a-size.png)

<span data-ttu-id="2ad41-181">프로덕션 워크로드의 경우 [Azure Virtual Machines의 SQL Server에 대한 성능 모범 사례](virtual-machines-windows-sql-performance.md)에서 권장하는 컴퓨터 크기 및 구성을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ad41-181">For production workloads, see the recommended machine sizes and configuration in [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span></span> <span data-ttu-id="2ad41-182">나열되지 않은 컴퓨터 크기가 필요할 경우 **모든 보기** 단추를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="2ad41-182">If you need a machine size that is not listed, click the **View all** button.</span></span>

> [!NOTE]
> <span data-ttu-id="2ad41-183">가상 컴퓨터 크기에 대한 자세한 내용은 [가상 컴퓨터 크기](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ad41-183">For more information about virtual machine sizes see, [Sizes for virtual machines](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="2ad41-184">컴퓨터 크기를 선택한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-184">Choose your machine size, and then click **Select**.</span></span>

## <a name="3-configure-optional-features"></a><span data-ttu-id="2ad41-185">3. 선택적 기능 구성</span><span class="sxs-lookup"><span data-stu-id="2ad41-185">3. Configure optional features</span></span>

<span data-ttu-id="2ad41-186">**설정** 창에서 가상 컴퓨터용 Azure Storage, 네트워킹 및 모니터링을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-186">On the **Settings** window, configure Azure storage, networking, and monitoring for the virtual machine.</span></span>

* <span data-ttu-id="2ad41-187">**Storage**의 **Managed Disks**에서 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-187">Under **Storage**, select **Yes** under use **Managed Disks**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2ad41-188">SQL Server에 Managed Disks를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-188">Microsoft recommends Managed Disks for SQL Server.</span></span> <span data-ttu-id="2ad41-189">Managed Disks는 배후에서 저장소를 처리해줍니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-189">Managed Disks handles storage behind the scenes.</span></span> <span data-ttu-id="2ad41-190">또한 Managed Disks가 있는 가상 컴퓨터가 동일한 가용성 집합에 속할 경우 Azure는 저장소 리소스를 배포하여 적절한 중복성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-190">In addition, when virtual machines with Managed Disks are in the same availability set, Azure distributes the storage resources to provide appropriate redundancy.</span></span> <span data-ttu-id="2ad41-191">자세한 내용은 [Azure Managed Disks 개요](../../../storage/storage-managed-disks-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ad41-191">For additional information, see [Azure Managed Disks Overview](../../../storage/storage-managed-disks-overview.md).</span></span> <span data-ttu-id="2ad41-192">가용성 집합의 Managed Disks에 대한 구체적인 내용을 보려면 [가용성 집합에서 VM에 Managed Disks 사용](../manage-availability.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ad41-192">For specifics about managed disks in an availability set, see [Use managed disks for VMs in availability set](../manage-availability.md).</span></span>

* <span data-ttu-id="2ad41-193">**네트워크**아래에서 자동으로 채워진 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-193">Under **Network**, you can accept the automatically populated values.</span></span> <span data-ttu-id="2ad41-194">각 기능을 클릭하여 **가상 네트워크**, **서브넷**, **공용 IP 주소** 및 **네트워크 보안 그룹**을 수동으로 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-194">You can also click on each feature to manually configure the **Virtual network**, **Subnet**, **Public IP address**, and **Network Security Group**.</span></span> <span data-ttu-id="2ad41-195">이 자습서에서는 기본 값을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-195">For the purposes of this tutorial, keep the default values.</span></span>

* <span data-ttu-id="2ad41-196">Azure에서는 VM에 지정된 것과 동일한 저장소 계정을 통해 **모니터링**이 기본적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-196">Azure enables **Monitoring** by default with the same storage account designated for the VM.</span></span> <span data-ttu-id="2ad41-197">여기에서 이러한 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-197">You can change these settings here.</span></span>

* <span data-ttu-id="2ad41-198">**가용성 집합**에서 이 자습서에 대해 기본값을 **없음**으로 남겨둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-198">Under **Availability set**, you can leave the default of **none** for this tutorial.</span></span> <span data-ttu-id="2ad41-199">SQL AlwaysOn 가용성 그룹을 설정하려는 경우 가상 컴퓨터를 다시 만들지 않도록 가용성을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-199">If you plan to set up SQL AlwaysOn Availability Groups, configure the availability to avoid recreating the virtual machine.</span></span>  <span data-ttu-id="2ad41-200">자세한 내용은 [Virtual Machines의 가용성 관리](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ad41-200">For more information, see [Manage the Availability of Virtual Machines](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="2ad41-201">이러한 설정 구성을 완료한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-201">When you are done configuring these settings, click **OK**.</span></span>

## <a name="4-configure-sql-server-settings"></a><span data-ttu-id="2ad41-202">4. SQL Server 설정 구성</span><span class="sxs-lookup"><span data-stu-id="2ad41-202">4. Configure SQL server settings</span></span>
<span data-ttu-id="2ad41-203">**SQL Server 설정** 창에서 SQL Server에 대한 설정 및 최적화를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-203">On the **SQL Server settings** window, configure specific settings and optimizations for SQL Server.</span></span> <span data-ttu-id="2ad41-204">SQL Server에 대해 구성할 수 있는 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-204">The settings that you can configure for SQL Server include the following.</span></span>

| <span data-ttu-id="2ad41-205">설정</span><span class="sxs-lookup"><span data-stu-id="2ad41-205">Setting</span></span> |
| --- |
| [<span data-ttu-id="2ad41-206">연결</span><span class="sxs-lookup"><span data-stu-id="2ad41-206">Connectivity</span></span>](#connectivity) |
| [<span data-ttu-id="2ad41-207">인증</span><span class="sxs-lookup"><span data-stu-id="2ad41-207">Authentication</span></span>](#authentication) |
| [<span data-ttu-id="2ad41-208">Storage 구성</span><span class="sxs-lookup"><span data-stu-id="2ad41-208">Storage configuration</span></span>](#storage-configuration) |
| [<span data-ttu-id="2ad41-209">자동화된 패치</span><span class="sxs-lookup"><span data-stu-id="2ad41-209">Automated Patching</span></span>](#automated-patching) |
| [<span data-ttu-id="2ad41-210">자동화된 Backup</span><span class="sxs-lookup"><span data-stu-id="2ad41-210">Automated Backup</span></span>](#automated-backup) |
| [<span data-ttu-id="2ad41-211">Azure Key Vault 통합</span><span class="sxs-lookup"><span data-stu-id="2ad41-211">Azure Key Vault Integration</span></span>](#azure-key-vault-integration) |
| [<span data-ttu-id="2ad41-212">R 서비스</span><span class="sxs-lookup"><span data-stu-id="2ad41-212">R Services</span></span>](#r-services) |

### <a name="connectivity"></a><span data-ttu-id="2ad41-213">연결</span><span class="sxs-lookup"><span data-stu-id="2ad41-213">Connectivity</span></span>

<span data-ttu-id="2ad41-214">**SQL 연결**에서 VM의 SQL Server 인스턴스에 대해 원하는 액세스 유형을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-214">Under **SQL connectivity**, specify the type of access you want to the SQL Server instance on this VM.</span></span> <span data-ttu-id="2ad41-215">이 자습서에서는 **공개(인터넷)**를 지정하여 인터넷 상의 컴퓨터 또는 서비스에서 SQL Server로의 연결을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-215">For the purposes of this tutorial, select **Public (internet)** to allow connections to SQL Server from machines or services on the internet.</span></span> <span data-ttu-id="2ad41-216">이 옵션을 선택하면 Azure에서는 포트 1433에서 트래픽을 허용하도록 방화벽 및 네트워크 보안 그룹을 자동으로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-216">With this option selected, Azure automatically configures the firewall and the network security group to allow traffic on port 1433.</span></span>

![SQL 연결 옵션](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-connectivity-alt.png)

> [!TIP]
> <span data-ttu-id="2ad41-218">기본적으로 SQL Server는 잘 알려진 포트 **1433**에서 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-218">By default, SQL Server listens on a well-known port, **1433**.</span></span> <span data-ttu-id="2ad41-219">보안 향상을 위해 이전 대화 상자의 포트를 기본 이외 포트(예: 1401)를 수신하도록 변경하세요.</span><span class="sxs-lookup"><span data-stu-id="2ad41-219">For increased security, change the port in the previous dialog to listen on a non-default port, such as 1401.</span></span> <span data-ttu-id="2ad41-220">이 작업을 수행할 경우 SSMS와 같이 모든 클라이언트 도구의 해당 포트를 사용하여 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-220">If you do this, you must connect using that port from any client tools, such as SSMS.</span></span>

<span data-ttu-id="2ad41-221">인터넷을 통해 SQL Server에 연결하려면 SQL Server 인증을 사용하도록 설정해야 합니다. 이 내용은 다음 섹션에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-221">To connect to SQL Server via the internet, you also must enable SQL Server Authentication, which is described in the next section.</span></span>

<span data-ttu-id="2ad41-222">인터넷을 통해 데이터베이스 엔진에 대한 연결을 사용하도록 설정하지 않으려면 다음 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-222">If you would prefer to not enable connections to the Database Engine via the internet, choose one of the following options:</span></span>

* <span data-ttu-id="2ad41-223">**로컬(VM 내부만)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-223">**Local (inside VM only)** to allow connections to SQL Server only from within the VM.</span></span>
* <span data-ttu-id="2ad41-224">**사설(Virtual Network 내)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-224">**Private (within Virtual Network)** to allow connections to SQL Server from machines or services in the same virtual network.</span></span>

<span data-ttu-id="2ad41-225">일반적으로, 시나리오에 허용되는 가장 제한적인 연결을 선택하여 보안을 개선합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-225">In general, improve security by choosing the most restrictive connectivity that your scenario allows.</span></span> <span data-ttu-id="2ad41-226">하지만 모든 옵션은 네트워크 보안 그룹 및 SQL/Windows 인증을 통해 보안을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-226">But all the options are securable through Network Security Group rules and SQL/Windows Authentication.</span></span> <span data-ttu-id="2ad41-227">VM이 만들어진 후에 네트워크 보안 그룹을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-227">You can edit Network Security Group after the VM is created.</span></span> <span data-ttu-id="2ad41-228">자세한 내용은 [Azure Virtual Machines의 SQL Server에 대한 보안 고려 사항](virtual-machines-windows-sql-security.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ad41-228">For more information, see [Security Considerations for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-security.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2ad41-229">SQL Server Express Edition용 가상 컴퓨터 이미지는 자동으로 TCP/IP 프로토콜을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-229">The virtual machine image for SQL Server Express edition does not automatically enable the TCP/IP protocol.</span></span> <span data-ttu-id="2ad41-230">공용 및 개인 연결 옵션에 대해서도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-230">This is true even for the Public and  Private connectivity options.</span></span> <span data-ttu-id="2ad41-231">Express Edition의 경우 VM을 만든 후에 SQL Server 구성 관리자를 사용하여 [수동으로 TCP/IP 프로토콜을 사용](#configure-sql-server-to-listen-on-the-tcp-protocol) 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-231">For Express edition, you must use SQL Server Configuration Manager to [manually enable the TCP/IP protocol](#configure-sql-server-to-listen-on-the-tcp-protocol) after creating the VM.</span></span>

### <a name="authentication"></a><span data-ttu-id="2ad41-232">인증</span><span class="sxs-lookup"><span data-stu-id="2ad41-232">Authentication</span></span>

<span data-ttu-id="2ad41-233">SQL Server 인증이 필요하도록 지정하려면 **사용** under **사용**을 방문하십시오.</span><span class="sxs-lookup"><span data-stu-id="2ad41-233">If you require SQL Server Authentication, click **Enable** under **SQL authentication**.</span></span>

![SQL Server 인증](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-authentication.png)

> [!NOTE]
> <span data-ttu-id="2ad41-235">인터넷(즉, 공용 연결 옵션)을 통해 SQL Server에 액세스하려는 경우 여기에서 SQL 인증을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-235">If you plan to access SQL Server over the internet (i.e. the Public connectivity option), you must enable SQL authentication here.</span></span> <span data-ttu-id="2ad41-236">SQL Server에 대한 공용 액세스를 위해서는 SQL 인증을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-236">Public access to the SQL Server requires the use of SQL Authentication.</span></span>
> 
> 

<span data-ttu-id="2ad41-237">SQL Server 인증을 사용하도록 설정하는 경우 **로그인 이름** 및 **암호**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-237">If you enable SQL Server Authentication, specify a **Login name** and **Password**.</span></span> <span data-ttu-id="2ad41-238">이 사용자 이름은 SQL Server 인증 로그인 및 **sysadmin** 고정된 서버 역할의 구성원으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-238">This user name is configured as a SQL Server Authentication login and member of the **sysadmin** fixed server role.</span></span> <span data-ttu-id="2ad41-239">인증 모드에 대한 자세한 내용은 [인증 모드 선택](https://docs.microsoft.com/sql/relational-databases/security/choose-an-authentication-mode)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ad41-239">See [Choose an Authentication Mode](https://docs.microsoft.com/sql/relational-databases/security/choose-an-authentication-mode) for more information about Authentication Modes.</span></span>

<span data-ttu-id="2ad41-240">SQL Server 인증을 사용하도록 설정하지 않으면, VM의 로컬 관리자 계정을 사용하여 SQL Server 인스턴스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-240">If you do not enable SQL Server Authentication, then you can use the local Administrator account on the VM to connect to the SQL Server instance.</span></span>

### <a name="storage-configuration"></a><span data-ttu-id="2ad41-241">Storage 구성</span><span class="sxs-lookup"><span data-stu-id="2ad41-241">Storage configuration</span></span>

<span data-ttu-id="2ad41-242">저장소 요구 사항을 지정하려면 **Storage 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-242">Click **Storage configuration** to specify the storage requirements.</span></span>

![SQL Storage 구성](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-storage.png)

> [!NOTE]
> <span data-ttu-id="2ad41-244">표준 저장소를 사용하도록 VM을 수동으로 구성한 경우 이 옵션은 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-244">If you manually configured your VM to use standard storage, this option is not available.</span></span> <span data-ttu-id="2ad41-245">자동 저장소 최적화는 Premium Storage에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-245">Automatic storage optimization is available only for Premium Storage.</span></span>

> [!TIP]
> <span data-ttu-id="2ad41-246">정지 수와 각 슬라이더의 상한값은 사용자가 선택한 VM 크기에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-246">The number of stops and the upper limits of each slider is dependent on the size of VM you selected.</span></span> <span data-ttu-id="2ad41-247">더 크고 효율적인 VM이 추가 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-247">A larger and more powerful VM is able to scale up more.</span></span>

<span data-ttu-id="2ad41-248">초당 입/출력 작업(IOPs), 처리량(MB/s) 및 총 저장소 크기로 요구 사항을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-248">You can specify requirements as input/output operations per second (IOPs), throughput in MB/s, and total storage size.</span></span> <span data-ttu-id="2ad41-249">슬라이딩 규모를 사용하여 이 값을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-249">Configure these values by using the sliding scales.</span></span> <span data-ttu-id="2ad41-250">워크로드에 따라 이러한 저장소 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-250">You can change these storage settings based on workload.</span></span> <span data-ttu-id="2ad41-251">포털에는 이러한 요구 사항에 따라 장착 및 구성할 디스크 수를 자동으로 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-251">The portal automatically calculates the number of disks to attach and configure based on these requirements.</span></span>

<span data-ttu-id="2ad41-252">**다음에 대해 Storage 최적화**에서 다음 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-252">Under **Storage optimized for**, select one of the following options:</span></span>

* <span data-ttu-id="2ad41-253">**일반**은 기본 설정이며 대부분의 워크로드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-253">**General** is the default setting and supports most workloads.</span></span>
* <span data-ttu-id="2ad41-254">**트랜잭션** 처리는 기존의 데이터베이스 OLTP 워크로드용으로 저장소를 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-254">**Transactional** processing optimizes the storage for traditional database OLTP workloads.</span></span>
* <span data-ttu-id="2ad41-255">**데이터 웨어하우징**은 분석 및 보고 워크로드용으로 저장소를 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-255">**Data warehousing** optimizes the storage for analytic and reporting workloads.</span></span>

### <a name="automated-patching"></a><span data-ttu-id="2ad41-256">자동화된 패치</span><span class="sxs-lookup"><span data-stu-id="2ad41-256">Automated patching</span></span>

<span data-ttu-id="2ad41-257">**Automated patching**이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-257">**Automated patching** is enabled by default.</span></span> <span data-ttu-id="2ad41-258">Azure에서는 자동화된 패치를 통해 SQL Server와 운영 체제를 자동으로 패치합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-258">Automated patching allows Azure to automatically patch SQL Server and the operating system.</span></span> <span data-ttu-id="2ad41-259">요일, 시간 및 유지 관리 기간에 대한 날짜를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-259">Specify a day of the week, time, and duration for a maintenance window.</span></span> <span data-ttu-id="2ad41-260">Azure에서 유지 관리 기간에 패치를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-260">Azure performs patching in this maintenance window.</span></span> <span data-ttu-id="2ad41-261">유지 관리 기간 일정에서는 VM 로캘 시간을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-261">The maintenance window schedule uses the VM locale for time.</span></span> <span data-ttu-id="2ad41-262">Azure에서 SQL Server와 운영 체제를 자동으로 패치하지 않으려면 **사용 안 함**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-262">If you do not want Azure to automatically patch SQL Server and the operating system, click **Disable**.</span></span>  

![SQL 자동화된 패치](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-patching.png)

<span data-ttu-id="2ad41-264">자세한 내용은 [Azure Virtual Machines에서 SQL Server의 자동화된 패치](virtual-machines-windows-sql-automated-patching.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ad41-264">For more information, see [Automated Patching for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-automated-patching.md).</span></span>

### <a name="automated-backup"></a><span data-ttu-id="2ad41-265">자동화된 백업</span><span class="sxs-lookup"><span data-stu-id="2ad41-265">Automated backup</span></span>

<span data-ttu-id="2ad41-266">**자동화된 백업**에서 모든 데이터베이스에 대해 자동 데이터베이스 백업을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-266">Enable automatic database backups for all databases under **Automated backup**.</span></span> <span data-ttu-id="2ad41-267">자동화된 백업은 기본적으로 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-267">Automated backup is disabled by default.</span></span>

<span data-ttu-id="2ad41-268">SQL 자동화된 백업을 사용하면 다음을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-268">When you enable SQL automated backup, you can configure the following:</span></span>

* <span data-ttu-id="2ad41-269">백업에 대한 보존 기간(일)</span><span class="sxs-lookup"><span data-stu-id="2ad41-269">Retention period (days) for backups</span></span>
* <span data-ttu-id="2ad41-270">백업에 사용할 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="2ad41-270">Storage account to use for backups</span></span>
* <span data-ttu-id="2ad41-271">백업을 위한 암호화 옵션 및 암호</span><span class="sxs-lookup"><span data-stu-id="2ad41-271">Encryption option and password for backups</span></span>
* <span data-ttu-id="2ad41-272">시스템 데이터베이스 백업</span><span class="sxs-lookup"><span data-stu-id="2ad41-272">Backup system databases</span></span>
* <span data-ttu-id="2ad41-273">백업 일정 구성</span><span class="sxs-lookup"><span data-stu-id="2ad41-273">Configure backup schedule</span></span>

<span data-ttu-id="2ad41-274">백업을 암호화하려면 **사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-274">To encrypt the backup, click **Enable**.</span></span> <span data-ttu-id="2ad41-275">그 다음 **암호**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-275">Then specify the **Password**.</span></span> <span data-ttu-id="2ad41-276">Azure에서는 백업을 암호화할 인증서를 만들고 지정된 암호를 사용하여 인증서를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-276">Azure creates a certificate to encrypt the backups and uses the specified password to protect that certificate.</span></span>

![SQL 자동화된 Backup](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-autobackup2.png)

 <span data-ttu-id="2ad41-278">자세한 내용은 [Azure Virtual Machines에서 SQL Server에 대한 자동화된 Backup](virtual-machines-windows-sql-automated-backup.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ad41-278">For more information, see [Automated Backup for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).</span></span>

### <a name="azure-key-vault-integration"></a><span data-ttu-id="2ad41-279">Azure Key Vault 통합</span><span class="sxs-lookup"><span data-stu-id="2ad41-279">Azure Key Vault integration</span></span>

<span data-ttu-id="2ad41-280">Azure에서 암호화를 위한 보안 암호를 저장하려면 **Azure Key Vault 통합**을 클릭하고 **사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-280">To store security secrets in Azure for encryption, click **Azure key vault integration** and click **Enable**.</span></span>

![SQL Azure Key Vault 통합](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-akv.png)

<span data-ttu-id="2ad41-282">다음 표에서는 Azure Key Vault 통합을 구성하는 데 필요한 매개 변수를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-282">The following table lists the parameters required to configure Azure Key Vault Integration.</span></span>

| <span data-ttu-id="2ad41-283">매개 변수</span><span class="sxs-lookup"><span data-stu-id="2ad41-283">PARAMETER</span></span> | <span data-ttu-id="2ad41-284">설명</span><span class="sxs-lookup"><span data-stu-id="2ad41-284">DESCRIPTION</span></span> | <span data-ttu-id="2ad41-285">예제</span><span class="sxs-lookup"><span data-stu-id="2ad41-285">EXAMPLE</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2ad41-286">**주요 자격 증명 모음 URL**</span><span class="sxs-lookup"><span data-stu-id="2ad41-286">**Key Vault URL**</span></span> |<span data-ttu-id="2ad41-287">주요 자격 증명 모음의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-287">The location of the key vault.</span></span> |<span data-ttu-id="2ad41-288">https://contosokeyvault.vault.azure.net/</span><span class="sxs-lookup"><span data-stu-id="2ad41-288">https://contosokeyvault.vault.azure.net/</span></span> |
| <span data-ttu-id="2ad41-289">**주체 이름**</span><span class="sxs-lookup"><span data-stu-id="2ad41-289">**Principal name**</span></span> |<span data-ttu-id="2ad41-290">Azure Active Directory 서비스 주체 이름.</span><span class="sxs-lookup"><span data-stu-id="2ad41-290">Azure Active Directory service principal name.</span></span> <span data-ttu-id="2ad41-291">이 이름을 클라이언트 ID라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-291">This name is also referred to as the Client ID.</span></span> |<span data-ttu-id="2ad41-292">fde2b411-33d5-4e11-af04eb07b669ccf2</span><span class="sxs-lookup"><span data-stu-id="2ad41-292">fde2b411-33d5-4e11-af04eb07b669ccf2</span></span> |
| <span data-ttu-id="2ad41-293">**주체 암호**</span><span class="sxs-lookup"><span data-stu-id="2ad41-293">**Principal secret**</span></span> |<span data-ttu-id="2ad41-294">Azure Active Directory 서비스 주체 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-294">Azure Active Directory service principal secret.</span></span> <span data-ttu-id="2ad41-295">이 암호를 클라이언트 암호라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-295">This secret is also referred to as the Client Secret.</span></span> |<span data-ttu-id="2ad41-296">9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM=</span><span class="sxs-lookup"><span data-stu-id="2ad41-296">9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM=</span></span> |
| <span data-ttu-id="2ad41-297">**자격 증명 이름**</span><span class="sxs-lookup"><span data-stu-id="2ad41-297">**Credential name**</span></span> |<span data-ttu-id="2ad41-298">**자격 증명 이름**: AKV 통합은 VM이 주요 자격 증명 모음에 액세스할 수 있도록 SQL Server 내에 자격 증명을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-298">**Credential name**: AKV Integration creates a credential within SQL Server, allowing the VM to have access to the key vault.</span></span> <span data-ttu-id="2ad41-299">이 자격 증명의 이름을 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="2ad41-299">Choose a name for this credential.</span></span> |<span data-ttu-id="2ad41-300">mycred1</span><span class="sxs-lookup"><span data-stu-id="2ad41-300">mycred1</span></span> |

<span data-ttu-id="2ad41-301">자세한 내용은 [Azure VM에서 SQL Server에 대한 Azure Key Vault 통합 구성](virtual-machines-windows-ps-sql-keyvault.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ad41-301">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs](virtual-machines-windows-ps-sql-keyvault.md).</span></span>

### <a name="r-services"></a><span data-ttu-id="2ad41-302">R 서비스</span><span class="sxs-lookup"><span data-stu-id="2ad41-302">R services</span></span>

<span data-ttu-id="2ad41-303">[SQL Server R 서비스](https://msdn.microsoft.com/library/mt604845.aspx)를 사용하도록 설정하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-303">You have the option to enable [SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx).</span></span> <span data-ttu-id="2ad41-304">SQL Server 2016을 사용하여 고급 분석을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-304">This enables you to use advanced analytics with SQL Server 2016.</span></span> <span data-ttu-id="2ad41-305">**SQL Server 설정** 창에서 **사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-305">Click **Enable** on the **SQL Server Settings** window.</span></span>

> [!NOTE]
> <span data-ttu-id="2ad41-306">SQL Server 2016 Developer Edition의 경우 이 옵션이 포털에서 잘못 비활성화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-306">For SQL Server 2016 Developer Edition, this option is incorrectly disabled by the portal.</span></span> <span data-ttu-id="2ad41-307">Developer 버전의 경우 VM을 생성한 후 R 서비스를 수동으로 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-307">For Developer edition, you must enable R Services manually after creating your VM.</span></span>

![SQL Server R 서비스 사용](./media/virtual-machines-windows-portal-sql-server-provision/azure-vm-sql-server-r-services.png)

<span data-ttu-id="2ad41-309">SQL Server 설정 구성을 마치면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-309">When you are finished configuring SQL Server settings, click **OK**.</span></span>

## <a name="5-review-the-summary"></a><span data-ttu-id="2ad41-310">5. 요약 검토</span><span class="sxs-lookup"><span data-stu-id="2ad41-310">5. Review the summary</span></span>

<span data-ttu-id="2ad41-311">**요약** 창에서 요약을 검토하고 **구매**를 클릭하여 이 VM에 대해 지정된 SQL Server, 리소스 그룹 및 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-311">On the **Summary** window, review the summary and click **Purchase** to create SQL Server, resource group, and resources specified for this VM.</span></span>

<span data-ttu-id="2ad41-312">Azure Portal에서 배포를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-312">You can monitor the deployment from the Azure portal.</span></span> <span data-ttu-id="2ad41-313">화면 맨 위에 있는 **알림** 단추는 배포의 기본 상태를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-313">The **Notifications** button at the top of the screen shows basic status of the deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="2ad41-314">배포 시간에 대한 정보를 제공하기 위해 SQL VM을 미국 동부 지역에 기본 설정을 사용하여 배포해 두었습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-314">To provide you with an idea on deployment times, I deployed a SQL VM to the East US region with default settings.</span></span> <span data-ttu-id="2ad41-315">이 테스트 배포는 완료하기까지 총 26분이 소요되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-315">This test deployment took a total of 26 minutes to complete.</span></span> <span data-ttu-id="2ad41-316">사용자의 지역 및 선택한 설정에 따라서 배포 시간이 더 빠르거나 늦을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-316">But you might experience a faster or slower deployment time based on your region and selected settings.</span></span>

## <a name="open-the-vm-with-remote-desktop"></a><span data-ttu-id="2ad41-317">원격 데스크톱을 사용하여 VM 열기</span><span class="sxs-lookup"><span data-stu-id="2ad41-317">Open the VM with Remote Desktop</span></span>

<span data-ttu-id="2ad41-318">다음 단계를 사용하여 원격 데스크톱으로 SQL Server 가상 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-318">Use the following steps to connect to the SQL Server virtual machine with Remote Desktop:</span></span>

> [!INCLUDE [Connect to SQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

<span data-ttu-id="2ad41-319">SQL Server 가상 컴퓨터에 연결된 후에, SQL Server Management Studio를 시작하고 로컬 관리자 자격 증명을 사용하여 Windows 인증으로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-319">After you connect to the SQL Server virtual machine, you can launch SQL Server Management Studio and connect with Windows Authentication using your local administrator credentials.</span></span> <span data-ttu-id="2ad41-320">SQL Server 인증을 사용하도록 설정한 경우에는, 프로비전 중에 구성해 놓은 SQL 로그인 및 암호를 사용하여 SQL 인증에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-320">If you enabled SQL Server Authentication, you can also connect with SQL Authentication using the SQL login and password you configured during provisioning.</span></span>

<span data-ttu-id="2ad41-321">컴퓨터에 연결하면 요구 사항에 따라 컴퓨터와 SQL Server 설정을 직접 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-321">Access to the machine enables you to directly change machine and SQL Server settings based on your requirements.</span></span> <span data-ttu-id="2ad41-322">예를 들어, 방화벽 설정을 구성하거나 SQL Server 구성 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-322">For example, you could configure the firewall settings or change SQL Server configuration settings.</span></span>

## <a name="enable-tcpip-for-developer-and-express-editions"></a><span data-ttu-id="2ad41-323">개발자 및 Express 버전에 대해 TCP/IP 사용</span><span class="sxs-lookup"><span data-stu-id="2ad41-323">Enable TCP/IP for Developer and Express editions</span></span>

<span data-ttu-id="2ad41-324">새 SQL Server VM을 프로비전할 때 Azure는 SQL Server 개발자 및 Express 버전에 대해 TCP/IP 프로토콜을 자동으로 설정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-324">When provisioning a new SQL Server VM, Azure does not automatically enable the TCP/IP protocol for SQL Server Developer and Express editions.</span></span> <span data-ttu-id="2ad41-325">아래 단계에서는 IP 주소를 통해 원격으로 연결할 수 있도록 TCP/IP를 수동으로 사용하도록 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-325">The steps below explain how to manually enable TCP/IP so that you can connect remotely by IP address.</span></span>

<span data-ttu-id="2ad41-326">다음 단계에서는 **SQL Server 구성 관리자**를 사용하여 SQL Server 개발자 및 Express 버전에 대해 TCP/IP 프로토콜을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-326">The following steps use **SQL Server Configuration Manager** to enable the TCP/IP protocol for SQL Server Developer and Express editions.</span></span>

> [!INCLUDE [Connect to SQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-to-sql-server-remotely"></a><span data-ttu-id="2ad41-327">원격으로 SQL Server 연결</span><span class="sxs-lookup"><span data-stu-id="2ad41-327">Connect to SQL Server remotely</span></span>

<span data-ttu-id="2ad41-328">이 자습서에서는 가상 컴퓨터와 **SQL Server 인증**에 대해 **공용** 액세스를 선택했습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-328">In this tutorial, we selected **Public** access for the virtual machine and **SQL Server Authentication**.</span></span> <span data-ttu-id="2ad41-329">이러한 설정은 가상 컴퓨터가 인터넷을 통한 모든 클라이언트의 SQL Server 연결을 허용하도록 자동으로 구성합니다(올바른 SQL 로그인이 있다는 가정 하에).</span><span class="sxs-lookup"><span data-stu-id="2ad41-329">These settings automatically configured the virtual machine to allow SQL Server connections from any client over the internet (assuming they have the correct SQL login).</span></span>

> [!NOTE]
> <span data-ttu-id="2ad41-330">프로비전 중에 공용을 선택하지 않은 경우 프로비전 후 포털을 통해 SQL 연결 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-330">If you did not select Public during provisioning, then you can change your SQL connectivity settings through the portal after provisioning.</span></span> <span data-ttu-id="2ad41-331">자세한 내용은 [SQL 연결 설정 변경](virtual-machines-windows-sql-connect.md#change)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ad41-331">For more information, see  [Change your SQL connectivity settings](virtual-machines-windows-sql-connect.md#change).</span></span>

<span data-ttu-id="2ad41-332">다음 섹션은 인터넷 상의 다른 컴퓨터에서 VM의 SQL Server 인스턴스에 연결하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="2ad41-332">The following sections show how to connect to your SQL Server instance on your VM from a different computer over the internet.</span></span>

> [!INCLUDE [Connect to SQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="2ad41-333">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2ad41-333">Next Steps</span></span>

<span data-ttu-id="2ad41-334">Azure에서 SQL Server를 사용하는 방법에 대한 기타 정보는 [Azure Virtual Machines의 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md) 및 [질문과 대답](virtual-machines-windows-sql-server-iaas-faq.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ad41-334">For other information about using SQL Server in Azure, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md) and the [Frequently Asked Questions](virtual-machines-windows-sql-server-iaas-faq.md).</span></span>