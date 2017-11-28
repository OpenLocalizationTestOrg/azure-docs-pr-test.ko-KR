---
title: "SQL Server 가상 컴퓨터 aaaProvision | Microsoft Docs"
description: "만들고 hello 포털을 사용 하 여 Azure에서 tooa SQL Server 가상 컴퓨터를 연결 합니다. 이 자습서에서는 hello Resource Manager 모드를 사용 합니다."
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
ms.openlocfilehash: aaad422d6ed47f5ca00b1ef484ac270a58e24f99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-in-hello-azure-portal"></a><span data-ttu-id="136b8-104">Hello Azure 포털에서에서 SQL Server 가상 컴퓨터를 프로 비전</span><span class="sxs-lookup"><span data-stu-id="136b8-104">Provision a SQL Server virtual machine in hello Azure Portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="136b8-105">포털</span><span class="sxs-lookup"><span data-stu-id="136b8-105">Portal</span></span>](virtual-machines-windows-portal-sql-server-provision.md)
> * [<span data-ttu-id="136b8-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="136b8-106">PowerShell</span></span>](virtual-machines-windows-ps-sql-create.md)
> 
> 

<span data-ttu-id="136b8-107">이 종단 간 자습서에서는 어떻게 toouse hello Azure 포털 tooprovision SQL Server를 실행 하는 가상 컴퓨터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-107">This end-to-end tutorial shows you how toouse hello Azure Portal tooprovision a virtual machine running SQL Server.</span></span>

<span data-ttu-id="136b8-108">hello (VM) Azure 가상 컴퓨터 갤러리에 Microsoft SQL Server가 포함 된 몇 가지 이미지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-108">hello Azure virtual machine (VM) gallery includes several images that contain Microsoft SQL Server.</span></span> <span data-ttu-id="136b8-109">몇 번의 클릭 hello hello 갤러리에서 SQL VM 이미지 중 하나를 선택 하 고 프로 비전 할 Azure 환경에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-109">With a few clicks, you can select one of hello SQL VM images from hello gallery and provision it in your Azure environment.</span></span>

<span data-ttu-id="136b8-110">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-110">In this tutorial, you will:</span></span>

* [<span data-ttu-id="136b8-111">Hello 갤러리에서 SQL VM 이미지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-111">Select a SQL VM image from hello gallery</span></span>](#select-a-sql-vm-image-from-the-gallery)
* [<span data-ttu-id="136b8-112">구성 및 hello VM 만들기</span><span class="sxs-lookup"><span data-stu-id="136b8-112">Configure and create hello VM</span></span>](#configure-the-vm)
* [<span data-ttu-id="136b8-113">원격 데스크톱으로 hello VM을 열으십시오</span><span class="sxs-lookup"><span data-stu-id="136b8-113">Open hello VM with Remote Desktop</span></span>](#open-the-vm-with-remote-desktop)
* [<span data-ttu-id="136b8-114">TooSQL 서버를 원격으로 연결</span><span class="sxs-lookup"><span data-stu-id="136b8-114">Connect tooSQL Server remotely</span></span>](#connect-to-sql-server-remotely)

## <a name="select-a-sql-vm-image-from-hello-gallery"></a><span data-ttu-id="136b8-115">Hello 갤러리에서 SQL VM 이미지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-115">Select a SQL VM image from hello gallery</span></span>
1. <span data-ttu-id="136b8-116">Toohello 로그인 [Azure 포털](https://portal.azure.com) 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-116">Log in toohello [Azure portal](https://portal.azure.com) using your account.</span></span>

   > [!NOTE]
   > <span data-ttu-id="136b8-117">Azure 계정이 없는 경우 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)을 방문하십시오.</span><span class="sxs-lookup"><span data-stu-id="136b8-117">If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

2. <span data-ttu-id="136b8-118">Hello Azure 포털에서 클릭 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-118">On hello Azure portal, click **New**.</span></span> <span data-ttu-id="136b8-119">hello 포털이 열립니다 hello **새로** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-119">hello portal opens hello **New** blade.</span></span> <span data-ttu-id="136b8-120">hello SQL Server VM 리소스는 hello에서 **계산** hello Marketplace의 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-120">hello SQL Server VM resources are in hello **Compute** group of hello Marketplace.</span></span>
3. <span data-ttu-id="136b8-121">Hello에 **새로** 블레이드에서 클릭 **계산** 클릭 하 고 **스크롤하게**합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-121">In hello **New** blade, click **Compute** and then click **See all**.</span></span>
4. <span data-ttu-id="136b8-122">Hello에 **필터** 텍스트 상자에 SQL Server를 입력 하 고 hello ENTER 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-122">In hello **Filter** text box type SQL Server, and press hello ENTER key.</span></span>

   ![Azure Virtual Machines 블레이드](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-blade2.png)

5. <span data-ttu-id="136b8-124">Hello 제공 되는 SQL Server 이미지를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-124">Review hello available SQL Server images.</span></span> <span data-ttu-id="136b8-125">각 이미지는 SQL Server 버전 및 운영 체제를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-125">Each image identifies a SQL Server version and an operating system.</span></span> 
6. <span data-ttu-id="136b8-126">Windows Server 2016에서 SQL Server 2016 SP1 개발자에 대 한 hello 이미지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-126">Select hello image for SQL Server 2016 SP1 Developer on Windows Server 2016.</span></span>

   > [!TIP]
   > <span data-ttu-id="136b8-127">hello Developer edition은 테스트 목적으로 개발에 대 한 무료 SQL Server의 모든 기능을 갖춘 버전 이기 때문에이 자습서에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-127">hello Developer edition is used in this tutorial because it is a full-featured edition of SQL Server that is free for development testing purposes.</span></span> <span data-ttu-id="136b8-128">Hello 실행 비용을 hello VM에 대해서만 지불 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-128">You pay only for hello cost of running hello VM.</span></span>

   > [!NOTE]
   > <span data-ttu-id="136b8-129">SQL VM 이미지 SQL Server 라이선스 비용 hello hello hello 개발자 및 Express 버전만) (제외 만드는 VM의 hello 분 당 가격에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-129">SQL VM images include hello licensing costs for SQL Server into hello per-minute pricing of hello VM you create (except for hello Developer and Express editions).</span></span> <span data-ttu-id="136b8-130">SQL Server Developer는 개발/테스트(비 프로덕션)를 위한 평가판이며, SQL Express는 간단한 워크로드(1GB 미만 메모리, 10GB 미만 저장소)를 위한 평가판입니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-130">SQL Server Developer is free for development/testing (not production) and SQL Express is free for lightweight workloads (less than 1 GB memory, less than 10-GB storage).</span></span>
   > <span data-ttu-id="136b8-131">다른 옵션 toobring your-소유-라이선스 (BYOL) 고 hello VM에 대해서만 지불 됩니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-131">There is another option toobring-your-own-license (BYOL) and pay only for hello VM.</span></span> <span data-ttu-id="136b8-132">이러한 이미지 이름에는 접두사 {BYOL}이 붙습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-132">Those image names are prefixed with {BYOL}.</span></span> <span data-ttu-id="136b8-133">이러한 옵션에 대한 자세한 내용은 [SQL Server Azure VM에 대한 가격 책정 지침](virtual-machines-windows-sql-server-pricing-guidance.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="136b8-133">For more information on these options, see [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md).</span></span>

7. <span data-ttu-id="136b8-134">**배포 모델 선택**에서 **리소스 관리자**가 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-134">Under **Select a deployment model**, verify that **Resource Manager** is selected.</span></span> <span data-ttu-id="136b8-135">리소스 관리자는 새 가상 컴퓨터에 대 한 배포 모델을 권장 하는 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-135">Resource Manager is hello recommended deployment model for new virtual machines.</span></span> <span data-ttu-id="136b8-136">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-136">Click **Create**.</span></span>

    ![리소스 관리자로 SQL VM 만들기](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-sql-deployment-model.png)

## <a name="configure-hello-vm"></a><span data-ttu-id="136b8-138">Hello VM 구성</span><span class="sxs-lookup"><span data-stu-id="136b8-138">Configure hello VM</span></span>
<span data-ttu-id="136b8-139">SQL Server 가상 컴퓨터를 구성하기 위한 5개의 블레이드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-139">There are five blades for configuring a SQL Server virtual machine.</span></span>

| <span data-ttu-id="136b8-140">단계</span><span class="sxs-lookup"><span data-stu-id="136b8-140">Step</span></span> | <span data-ttu-id="136b8-141">설명</span><span class="sxs-lookup"><span data-stu-id="136b8-141">Description</span></span> |
| --- | --- |
| <span data-ttu-id="136b8-142">**기본 사항**</span><span class="sxs-lookup"><span data-stu-id="136b8-142">**Basics**</span></span> |[<span data-ttu-id="136b8-143">기본 설정 구성</span><span class="sxs-lookup"><span data-stu-id="136b8-143">Configure basic settings</span></span>](#1-configure-basic-settings) |
| <span data-ttu-id="136b8-144">**크기**</span><span class="sxs-lookup"><span data-stu-id="136b8-144">**Size**</span></span> |[<span data-ttu-id="136b8-145">가상 컴퓨터 크기 선택</span><span class="sxs-lookup"><span data-stu-id="136b8-145">Choose virtual machine size</span></span>](#2-choose-virtual-machine-size) |
| <span data-ttu-id="136b8-146">**설정**</span><span class="sxs-lookup"><span data-stu-id="136b8-146">**Settings**</span></span> |[<span data-ttu-id="136b8-147">선택적 기능 구성</span><span class="sxs-lookup"><span data-stu-id="136b8-147">Configure optional features</span></span>](#3-configure-optional-features) |
| <span data-ttu-id="136b8-148">**SQL 서버 설정**</span><span class="sxs-lookup"><span data-stu-id="136b8-148">**SQL Server settings**</span></span> |[<span data-ttu-id="136b8-149">SQL Server 설정 구성</span><span class="sxs-lookup"><span data-stu-id="136b8-149">Configure SQL server settings</span></span>](#4-configure-sql-server-settings) |
| <span data-ttu-id="136b8-150">**요약**</span><span class="sxs-lookup"><span data-stu-id="136b8-150">**Summary**</span></span> |[<span data-ttu-id="136b8-151">요약 검토 hello</span><span class="sxs-lookup"><span data-stu-id="136b8-151">Review hello summary</span></span>](#5-review-the-summary) |

## <a name="1-configure-basic-settings"></a><span data-ttu-id="136b8-152">1. 기본 설정 구성</span><span class="sxs-lookup"><span data-stu-id="136b8-152">1. Configure basic settings</span></span>
<span data-ttu-id="136b8-153">Hello에 **기본 사항** 블레이드에서 hello 다음 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-153">On hello **Basics** blade, provide hello following information:</span></span>

* <span data-ttu-id="136b8-154">고유한 가상 컴퓨터 **이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-154">Enter a unique virtual machine **Name**.</span></span>
* <span data-ttu-id="136b8-155">지정 된 **사용자 이름** hello hello VM 로컬 관리자 계정에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-155">Specify a **User name** for hello local administrator account on hello VM.</span></span> <span data-ttu-id="136b8-156">이 계정은 SQL Server toohello도 추가 **sysadmin** 고정된 서버 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-156">This account is also added toohello SQL Server **sysadmin** fixed server role.</span></span>
* <span data-ttu-id="136b8-157">강력한 **암호**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-157">Provide a strong **Password**.</span></span>
* <span data-ttu-id="136b8-158">Hello 구독에 대해 올바른지 확인 하는 여러 구독이 있는 경우에 새 VM hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-158">If you have multiple subscriptions, verify that hello subscription is correct for hello new VM.</span></span>
* <span data-ttu-id="136b8-159">Hello에 **리소스 그룹** 상자에 새 리소스 그룹에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-159">In hello **Resource group** box, type a name for a new resource group.</span></span> <span data-ttu-id="136b8-160">또는 toouse 기존 리소스 그룹 클릭 **기존 항목 사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-160">Alternatively, toouse an existing resource group click **Use existing**.</span></span> <span data-ttu-id="136b8-161">리소스 그룹은 Azure 내 관련 리소스의 컬렉션입니다(가상 컴퓨터, 저장소 계정, 가상 네트워크 등).</span><span class="sxs-lookup"><span data-stu-id="136b8-161">A resource group is a collection of related resources in Azure (virtual machines, storage accounts, virtual networks, etc.).</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="136b8-162">새 리소스 그룹을 사용하면 Azure에서 SQL Server 배포를 테스트하거나 알아보는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-162">Using a new resource group is helpful if you are just testing or learning about SQL Server deployments in Azure.</span></span> <span data-ttu-id="136b8-163">테스트와 완료 된 후 hello 리소스 그룹 tooautomatically delete hello VM 및 해당 리소스 그룹에 연결 된 모든 리소스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-163">After you finish with your test, delete hello resource group tooautomatically delete hello VM and all resources associated with that resource group.</span></span> <span data-ttu-id="136b8-164">리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../../../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="136b8-164">For more information about resource groups, see [Azure Resource Manager Overview](../../../azure-resource-manager/resource-group-overview.md).</span></span>
  > 
  > 
* <span data-ttu-id="136b8-165">이 배포의 **위치** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-165">Select a **Location** for this deployment.</span></span>
* <span data-ttu-id="136b8-166">클릭 **확인** toosave hello 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-166">Click **OK** toosave hello settings.</span></span>
  
    ![SQL 기본 블레이드](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-basic.png)

## <a name="2-choose-virtual-machine-size"></a><span data-ttu-id="136b8-168">2. 가상 컴퓨터 크기 선택</span><span class="sxs-lookup"><span data-stu-id="136b8-168">2. Choose virtual machine size</span></span>
<span data-ttu-id="136b8-169">Hello에 **크기** 단계, hello에 가상 컴퓨터 크기 선택 **크기 선택** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-169">On hello **Size** step, choose a virtual machine size in hello **Choose a size** blade.</span></span> <span data-ttu-id="136b8-170">hello 블레이드는 처음 선택한 hello 이미지에 따라 권장된 컴퓨터 크기를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-170">hello blade initially displays recommended machine sizes based on hello image you selected.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="136b8-171">hello 예상 hello에 표시 되는 월별 비용 **크기 선택** 블레이드 SQL Server 라이선스 비용을 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-171">hello estimated monthly cost displayed on hello **Choose a size** blade does not include SQL Server licensing costs.</span></span> <span data-ttu-id="136b8-172">이 예상된 월별 비용 hello 단독 VM의 hello 비용이입니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-172">This estimated monthly cost is hello cost of hello VM alone.</span></span> <span data-ttu-id="136b8-173">SQL Server의 hello Express 및 Developer 버전에서 hello 총 예상된 비용입니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-173">For hello Express and Developer editions of SQL Server, this is hello total estimated cost.</span></span> <span data-ttu-id="136b8-174">다른 버전에 대 한 참조 hello [Windows 가상 컴퓨터 가격 책정 페이지](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) 하 고 SQL Server의 대상 버전을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-174">For other editions, see hello [Windows Virtual Machines pricing page](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) and select your target edition of SQL Server.</span></span> <span data-ttu-id="136b8-175">또한 hello 참조 [SQL Server Azure Vm에 대 한 지침을 가격](virtual-machines-windows-sql-server-pricing-guidance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-175">Also see hello [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md).</span></span>

![SQL VM 크기 옵션](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-choose-a-size.png)

<span data-ttu-id="136b8-177">프로덕션 워크로드에는, [Premium Storage](../../../storage/storage-premium-storage.md)를 지원하는 가상 컴퓨터 크기를 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-177">For production workloads, we recommend selecting a virtual machine size that supports [Premium Storage](../../../storage/storage-premium-storage.md).</span></span> <span data-ttu-id="136b8-178">Hello를 사용 하 여 해당 수준의 성능 필요 하지 않은 경우 **모든 보기** 단추를 모든 컴퓨터 크기 옵션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-178">If you do not require that level of performance, use hello **View all** button, which shows all machine size options.</span></span> <span data-ttu-id="136b8-179">예를 들어, 개발 또는 테스트 환경을 위해 더 작은 컴퓨터 크기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-179">For example, you might use a smaller machine size for a development or test environment.</span></span>

> [!NOTE]
> <span data-ttu-id="136b8-180">가상 컴퓨터 크기에 대한 자세한 내용은 [가상 컴퓨터 크기](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="136b8-180">For more information about virtual machine sizes, [Sizes for virtual machines](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="136b8-181">SQL Server VM 크기에 대한 고려 사항은 [Azure Virtual Machines의 SQL Server에 대한 성능 모범 사례](virtual-machines-windows-sql-performance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="136b8-181">For considerations about SQL Server VM sizes, see [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span></span>

<span data-ttu-id="136b8-182">컴퓨터 크기를 선택한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-182">Choose your machine size, and then click **Select**.</span></span>

## <a name="3-configure-optional-features"></a><span data-ttu-id="136b8-183">3. 선택적 기능 구성</span><span class="sxs-lookup"><span data-stu-id="136b8-183">3. Configure optional features</span></span>
<span data-ttu-id="136b8-184">Hello에 **설정을** 블레이드를 Azure 저장소, 네트워킹, 및 hello 가상 컴퓨터에 대 한 모니터링을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-184">On hello **Settings** blade, configure Azure storage, networking, and monitoring for hello virtual machine.</span></span>

* <span data-ttu-id="136b8-185">**Storage**에서 **디스크 유형**으로 표준 또는 프리미엄(SSD)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-185">Under **Storage**, specify a **Disk type** of either Standard or Premium (SSD).</span></span> <span data-ttu-id="136b8-186">프리미엄 저장소는 프로덕션 워크로드용으로 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-186">Premium storage is recommended for production workloads.</span></span>

> [!NOTE]
> <span data-ttu-id="136b8-187">Premium Storage를 지원하지 않는 컴퓨터 크기에 대해 프리미엄(SSD)을 선택하면, 컴퓨터 크기가 자동으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-187">If you select Premium (SSD) for a machine size that does not support Premium Storage, your machine size changes automatically.</span></span>  
> 
> 

* <span data-ttu-id="136b8-188">아래 **저장소 계정**, hello 자동으로 프로 비전 된 저장소 계정 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-188">Under **Storage account**, you can accept hello automatically provisioned storage account name.</span></span> <span data-ttu-id="136b8-189">또한 클릭할 수 **저장소 계정** toochoose 기존 계정 및 hello 저장소 계정 유형을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-189">You can also click on **Storage account** toochoose an existing account and configure hello storage account type.</span></span> <span data-ttu-id="136b8-190">기본적으로 Azure에서는 로컬 중복 저장소로 새 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-190">By default, Azure creates a new storage account with locally redundant storage.</span></span> <span data-ttu-id="136b8-191">저장소 옵션에 대한 자세한 내용은 [Azure Storage 복제](../../../storage/storage-redundancy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="136b8-191">For more information about storage options, see [Azure Storage replication](../../../storage/storage-redundancy.md).</span></span>
* <span data-ttu-id="136b8-192">아래 **네트워크**를 자동으로 채울 hello 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-192">Under **Network**, you can accept hello automatically populated values.</span></span> <span data-ttu-id="136b8-193">각 기능을 클릭할 수도 있습니다 toomanually hello 구성 **가상 네트워크**, **서브넷**, **공용 IP 주소**, 및 **네트워크보안그룹**.</span><span class="sxs-lookup"><span data-stu-id="136b8-193">You can also click on each feature toomanually configure hello **Virtual network**, **Subnet**, **Public IP address**, and **Network Security Group**.</span></span> <span data-ttu-id="136b8-194">이 자습서의 hello 위해 hello 기본값을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-194">For hello purposes of this tutorial, keep hello default values.</span></span>
* <span data-ttu-id="136b8-195">Azure 사용 **모니터링** hello VM에 대해 동일한 저장소 계정을 지정 하는 hello로 기본적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-195">Azure enables **Monitoring** by default with hello same storage account designated for hello VM.</span></span> <span data-ttu-id="136b8-196">여기에서 이러한 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-196">You can change these settings here.</span></span>
* <span data-ttu-id="136b8-197">**가용성 집합**아래에서 가용성 집합을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-197">Under **Availability set**, specify an availability set.</span></span> <span data-ttu-id="136b8-198">이 자습서의 hello 위해 선택할 수 있습니다 **none**합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-198">For hello purposes of this tutorial, you can select **none**.</span></span> <span data-ttu-id="136b8-199">SQL AlwaysOn 가용성 그룹을 tooset 하려는 경우 hello 가용성 tooavoid 다시 만들고 hello 가상 컴퓨터를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-199">If you plan tooset up SQL AlwaysOn Availability Groups, configure hello availability tooavoid recreating hello virtual machine.</span></span>  <span data-ttu-id="136b8-200">자세한 내용은 참조 [가상 컴퓨터의 가용성 관리 hello](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-200">For more information, see [Manage hello Availability of Virtual Machines](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="136b8-201">이러한 설정 구성을 완료한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-201">When you are done configuring these settings, click **OK**.</span></span>

## <a name="4-configure-sql-server-settings"></a><span data-ttu-id="136b8-202">4. SQL Server 설정 구성</span><span class="sxs-lookup"><span data-stu-id="136b8-202">4. Configure SQL server settings</span></span>
<span data-ttu-id="136b8-203">Hello에 **SQL Server 설정을** 블레이드에서 특정 설정 및 SQL Server에 대 한 최적화를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-203">On hello **SQL Server settings** blade, configure specific settings and optimizations for SQL Server.</span></span> <span data-ttu-id="136b8-204">SQL Server에 대해 구성할 수 있는 hello 설정 hello 설정을 다음을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-204">hello settings that you can configure for SQL Server include hello following settings.</span></span>

| <span data-ttu-id="136b8-205">설정</span><span class="sxs-lookup"><span data-stu-id="136b8-205">Setting</span></span> |
| --- |
| [<span data-ttu-id="136b8-206">연결</span><span class="sxs-lookup"><span data-stu-id="136b8-206">Connectivity</span></span>](#connectivity) |
| [<span data-ttu-id="136b8-207">인증</span><span class="sxs-lookup"><span data-stu-id="136b8-207">Authentication</span></span>](#authentication) |
| [<span data-ttu-id="136b8-208">Storage 구성</span><span class="sxs-lookup"><span data-stu-id="136b8-208">Storage configuration</span></span>](#storage-configuration) |
| [<span data-ttu-id="136b8-209">자동화된 패치</span><span class="sxs-lookup"><span data-stu-id="136b8-209">Automated Patching</span></span>](#automated-patching) |
| [<span data-ttu-id="136b8-210">자동화된 Backup</span><span class="sxs-lookup"><span data-stu-id="136b8-210">Automated Backup</span></span>](#automated-backup) |
| [<span data-ttu-id="136b8-211">Azure Key Vault 통합</span><span class="sxs-lookup"><span data-stu-id="136b8-211">Azure Key Vault Integration</span></span>](#azure-key-vault-integration) |
| [<span data-ttu-id="136b8-212">R 서비스</span><span class="sxs-lookup"><span data-stu-id="136b8-212">R Services</span></span>](#r-services) |

### <a name="connectivity"></a><span data-ttu-id="136b8-213">연결</span><span class="sxs-lookup"><span data-stu-id="136b8-213">Connectivity</span></span>
<span data-ttu-id="136b8-214">**SQL 연결**, hello 유형을 지정 하려는이 VM의 SQL Server 인스턴스에 toohello 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-214">Under **SQL connectivity**, specify hello type of access you want toohello SQL Server instance on this VM.</span></span> <span data-ttu-id="136b8-215">이 자습서의 hello 위해서 선택 **공개 (인터넷)** tooallow 연결 tooSQL 서버 컴퓨터 또는 서비스를 통해 인터넷 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-215">For hello purposes of this tutorial, select **Public (internet)** tooallow connections tooSQL Server from machines or services on hello internet.</span></span> <span data-ttu-id="136b8-216">이 옵션을 선택 하면 Azure에서 자동으로 구성 hello 방화벽 및 네트워크 보안 그룹 tooallow 트래픽 hello 포트 1433입니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-216">With this option selected, Azure automatically configures hello firewall and hello network security group tooallow traffic on port 1433.</span></span>  

![SQL 연결 옵션](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-connectivity-alt.png)

<span data-ttu-id="136b8-218">tooconnect tooSQL 서버 hello 통해 인터넷을도 인증을 활성화 해야 SQL Server, hello 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-218">tooconnect tooSQL Server via hello internet, you also must enable SQL Server Authentication, which is described in hello next section.</span></span>

> [!NOTE]
> <span data-ttu-id="136b8-219">것은 가능한 tooadd hello 네트워크 통신 tooyour SQL Server VM에 대 한 더 많은 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-219">It is possible tooadd more restrictions for hello network communications tooyour SQL Server VM.</span></span> <span data-ttu-id="136b8-220">Hello VM을 만든 후 더 많은 제한이 편집 hello 네트워크 보안 그룹으로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-220">You can add more restrictions by editing hello Network Security Group after hello VM is created.</span></span> <span data-ttu-id="136b8-221">자세한 내용은 [NSG(네트워크 보안 그룹)란?](../../../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="136b8-221">For more information, see [What is a Network Security Group (NSG)?](../../../virtual-network/virtual-networks-nsg.md)</span></span>
> 
> 

<span data-ttu-id="136b8-222">Toonot enable 연결 toohello 데이터베이스 엔진을 사용 하도록 하려는 경우를 통해 인터넷 hello, hello 다음 옵션 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-222">If you would prefer toonot enable connections toohello Database Engine via hello internet, choose one of hello following options:</span></span>

* <span data-ttu-id="136b8-223">**VM에만 해당) (내 로컬** tooallow 연결 tooSQL 에서만 서버 hello VM 내에서.</span><span class="sxs-lookup"><span data-stu-id="136b8-223">**Local (inside VM only)** tooallow connections tooSQL Server only from within hello VM.</span></span>
* <span data-ttu-id="136b8-224">**(가상 네트워크 내에서) 개인** tooallow 연결 tooSQL 서버 hello의 서비스 또는 컴퓨터에서 동일한 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-224">**Private (within Virtual Network)** tooallow connections tooSQL Server from machines or services in hello same virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="136b8-225">SQL Server Express edition에 대 한 가상 컴퓨터 이미지 hello hello TCP/IP 프로토콜을 자동으로 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-225">hello virtual machine image for SQL Server Express edition does not automatically enable hello TCP/IP protocol.</span></span> <span data-ttu-id="136b8-226">이 hello 공용 및 전용 연결에도 적용 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-226">This is true even for hello Public and  Private connectivity options.</span></span> <span data-ttu-id="136b8-227">Express edition을 사용 해야 SQL Server 구성 관리자 너무[수동으로 hello TCP/IP 프로토콜을 사용 하도록 설정](#configure-sql-server-to-listen-on-the-tcp-protocol) hello VM을 만든 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-227">For Express edition, you must use SQL Server Configuration Manager too[manually enable hello TCP/IP protocol](#configure-sql-server-to-listen-on-the-tcp-protocol) after creating hello VM.</span></span>
> 
> 

<span data-ttu-id="136b8-228">일반적으로 시나리오에서 허용 하는 hello 가장 제한적인 연결을 선택 하 여 보안을 향상 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-228">In general, improve security by choosing hello most restrictive connectivity that your scenario allows.</span></span> <span data-ttu-id="136b8-229">하지만 모든 hello 옵션은 네트워크 보안 그룹 규칙 및 SQL/Windows 인증을 통해 보안 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-229">But all hello options are securable through Network Security Group rules and SQL/Windows Authentication.</span></span>

<span data-ttu-id="136b8-230">**포트** too1433 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-230">**Port** defaults too1433.</span></span> <span data-ttu-id="136b8-231">다른 포트 번호를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-231">You can specify a different port number.</span></span>
<span data-ttu-id="136b8-232">자세한 내용은 참조 [tooa SQL Server 가상 컴퓨터 (리소스 관리자)에 연결 | Microsoft Azure](virtual-machines-windows-sql-connect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-232">For more information, see [Connect tooa SQL Server Virtual Machine (Resource Manager) | Microsoft Azure](virtual-machines-windows-sql-connect.md).</span></span>

### <a name="authentication"></a><span data-ttu-id="136b8-233">인증</span><span class="sxs-lookup"><span data-stu-id="136b8-233">Authentication</span></span>
<span data-ttu-id="136b8-234">SQL Server 인증이 필요하도록 지정하려면 **사용** under **사용**을 방문하십시오.</span><span class="sxs-lookup"><span data-stu-id="136b8-234">If you require SQL Server Authentication, click **Enable** under **SQL authentication**.</span></span>

![SQL Server 인증](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-authentication.png)

> [!NOTE]
> <span data-ttu-id="136b8-236">통해 tooaccess SQL Server를 계획 하는 경우 hello 인터넷 (즉, hello 공용 연결 옵션), 여기에 SQL 인증을 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-236">If you plan tooaccess SQL Server over hello internet (that is, hello Public connectivity option), you must enable SQL authentication here.</span></span> <span data-ttu-id="136b8-237">공용 액세스 toohello SQL Server에는 SQL 인증 hello 사용을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-237">Public access toohello SQL Server requires hello use of SQL Authentication.</span></span>
> 
> 

<span data-ttu-id="136b8-238">SQL Server 인증을 사용하도록 설정하는 경우 **로그인 이름** 및 **암호**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-238">If you enable SQL Server Authentication, specify a **Login name** and **Password**.</span></span> <span data-ttu-id="136b8-239">이 사용자 이름은 SQL Server 인증 로그인 및 hello의 구성원으로 구성 된 **sysadmin** 고정된 서버 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-239">This user name is configured as a SQL Server Authentication login and member of hello **sysadmin** fixed server role.</span></span> <span data-ttu-id="136b8-240">인증 모드에 대한 자세한 내용은 [인증 모드 선택](http://msdn.microsoft.com/library/ms144284.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="136b8-240">For more information about Authentication Modes, see [Choose an Authentication Mode](http://msdn.microsoft.com/library/ms144284.aspx).</span></span>

<span data-ttu-id="136b8-241">SQL Server 인증을 사용 하지 않도록 하는 경우 로컬 관리자 계정을 hello hello VM tooconnect toohello SQL Server 인스턴스에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-241">If you do not enable SQL Server Authentication, then you can use hello local Administrator account on hello VM tooconnect toohello SQL Server instance.</span></span>

### <a name="storage-configuration"></a><span data-ttu-id="136b8-242">Storage 구성</span><span class="sxs-lookup"><span data-stu-id="136b8-242">Storage configuration</span></span>
<span data-ttu-id="136b8-243">클릭 **저장소 구성** toospecify hello에 대 한 저장소 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-243">Click **Storage configuration** toospecify hello storage requirements.</span></span>

![SQL Storage 구성](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-storage.png)

> [!NOTE]
> <span data-ttu-id="136b8-245">표준 저장소를 선택하면, 이 옵션을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-245">If you select Standard storage, this option is not available.</span></span> <span data-ttu-id="136b8-246">자동 저장소 최적화는 Premium Storage에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-246">Automatic storage optimization is available only for Premium Storage.</span></span>
> 
> 

<span data-ttu-id="136b8-247">초당 입/출력 작업(IOPs), 처리량(MB/s) 및 총 저장소 크기로 요구 사항을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-247">You can specify requirements as input/output operations per second (IOPs), throughput in MB/s, and total storage size.</span></span> <span data-ttu-id="136b8-248">Hello 슬라이딩 눈금을 사용 하 여 이러한 값을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-248">Configure these values by using hello sliding scales.</span></span> <span data-ttu-id="136b8-249">hello 포털 hello 수의 이러한 요구 사항에 따라 디스크를 자동으로 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-249">hello portal automatically calculates hello number of disks based on these requirements.</span></span>

<span data-ttu-id="136b8-250">기본적으로 Azure 5,000 IOPs, 200mb의 디스크 및 저장소 공간의 1TB hello 저장소를 최적화 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-250">By default, Azure optimizes hello storage for 5000 IOPs, 200 MBs, and 1 TB of storage space.</span></span> <span data-ttu-id="136b8-251">워크로드에 따라 이러한 저장소 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-251">You can change these storage settings based on workload.</span></span> <span data-ttu-id="136b8-252">아래 **저장소에 대 한 액세스에 최적화 된**, hello 다음 옵션 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-252">Under **Storage optimized for**, select one of hello following options:</span></span>

* <span data-ttu-id="136b8-253">**일반** hello 기본 설정 이며 대부분의 워크 로드를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-253">**General** is hello default setting and supports most workloads.</span></span>
* <span data-ttu-id="136b8-254">**트랜잭션** 처리 일반 데이터베이스 OLTP 워크 로드에 대 한 hello 저장소를 최적화 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-254">**Transactional** processing optimizes hello storage for traditional database OLTP workloads.</span></span>
* <span data-ttu-id="136b8-255">**데이터 웨어하우징** 분석 및 보고 작업에 대 한 hello 저장소를 최적화 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-255">**Data warehousing** optimizes hello storage for analytic and reporting workloads.</span></span>

> [!NOTE]
> <span data-ttu-id="136b8-256">hello 상한값 hello 슬라이더에서 선택한 가상 컴퓨터 크기에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-256">hello upper limits on hello sliders vary depending on your selected virtual machine size.</span></span>
> 
> 

### <a name="automated-patching"></a><span data-ttu-id="136b8-257">자동화된 패치</span><span class="sxs-lookup"><span data-stu-id="136b8-257">Automated patching</span></span>
<span data-ttu-id="136b8-258">**Automated patching**이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-258">**Automated patching** is enabled by default.</span></span> <span data-ttu-id="136b8-259">자동화 된 패치 적용 Azure tooautomatically 패치 hello 및 SQL Server 운영 체제 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-259">Automated patching allows Azure tooautomatically patch SQL Server and hello operating system.</span></span> <span data-ttu-id="136b8-260">요일을 한 hello 주, 시간 및 유지 관리 기간에 대 한 기간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-260">Specify a day of hello week, time, and duration for a maintenance window.</span></span> <span data-ttu-id="136b8-261">Azure에서 유지 관리 기간에 패치를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-261">Azure performs patching in this maintenance window.</span></span> <span data-ttu-id="136b8-262">hello 유지 관리 창 일정 시간에 대 한 hello VM 로캘을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-262">hello maintenance window schedule uses hello VM locale for time.</span></span> <span data-ttu-id="136b8-263">Azure tooautomatically 패치 hello 및 SQL Server 운영 체제 하지 않으려면 클릭 **사용 하지 않도록 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-263">If you do not want Azure tooautomatically patch SQL Server and hello operating system, click **Disable**.</span></span>  

![SQL 자동화된 패치](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-patching.png)

<span data-ttu-id="136b8-265">자세한 내용은 [Azure Virtual Machines에서 SQL Server의 자동화된 패치](virtual-machines-windows-sql-automated-patching.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="136b8-265">For more information, see [Automated Patching for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-automated-patching.md).</span></span>

### <a name="automated-backup"></a><span data-ttu-id="136b8-266">자동화된 백업</span><span class="sxs-lookup"><span data-stu-id="136b8-266">Automated backup</span></span>
<span data-ttu-id="136b8-267">**자동화된 백업**에서 모든 데이터베이스에 대해 자동 데이터베이스 백업을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-267">Enable automatic database backups for all databases under **Automated backup**.</span></span> <span data-ttu-id="136b8-268">자동화된 백업은 기본적으로 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-268">Automated backup is disabled by default.</span></span>

<span data-ttu-id="136b8-269">SQL 자동화 된 백업을 사용 하도록 설정 하면 hello 다음 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-269">When you enable SQL automated backup, you can configure hello following settings:</span></span>

* <span data-ttu-id="136b8-270">백업에 대한 보존 기간(일)</span><span class="sxs-lookup"><span data-stu-id="136b8-270">Retention period (days) for backups</span></span>
* <span data-ttu-id="136b8-271">백업에 대 한 저장소 계정 toouse</span><span class="sxs-lookup"><span data-stu-id="136b8-271">Storage account toouse for backups</span></span>
* <span data-ttu-id="136b8-272">백업을 위한 암호화 옵션 및 암호</span><span class="sxs-lookup"><span data-stu-id="136b8-272">Encryption option and password for backups</span></span>
* <span data-ttu-id="136b8-273">시스템 데이터베이스 백업</span><span class="sxs-lookup"><span data-stu-id="136b8-273">Backup system databases</span></span>
* <span data-ttu-id="136b8-274">백업 일정 구성</span><span class="sxs-lookup"><span data-stu-id="136b8-274">Configure backup schedule</span></span>

<span data-ttu-id="136b8-275">tooencrypt hello 백업, 클릭 **사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-275">tooencrypt hello backup, click **Enable**.</span></span> <span data-ttu-id="136b8-276">그런 다음 hello 지정 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-276">Then specify hello **Password**.</span></span> <span data-ttu-id="136b8-277">Azure 인증서 tooencrypt hello 백업을 만들고 사용 하 여 hello 암호 tooprotect 해당 인증서를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-277">Azure creates a certificate tooencrypt hello backups and uses hello specified password tooprotect that certificate.</span></span>

![SQL 자동화된 Backup](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-autobackup2.png)

 <span data-ttu-id="136b8-279">자세한 내용은 [Azure Virtual Machines에서 SQL Server에 대한 자동화된 Backup](virtual-machines-windows-sql-automated-backup.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="136b8-279">For more information, see [Automated Backup for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).</span></span>

### <a name="azure-key-vault-integration"></a><span data-ttu-id="136b8-280">Azure Key Vault 통합</span><span class="sxs-lookup"><span data-stu-id="136b8-280">Azure Key Vault integration</span></span>
<span data-ttu-id="136b8-281">암호화를 위해 Azure의 보안 암호 toostore 클릭 **Azure 키 자격 증명 모음 통합** 클릭 **사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-281">toostore security secrets in Azure for encryption, click **Azure key vault integration** and click **Enable**.</span></span>

![SQL Azure Key Vault 통합](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-akv.png)

<span data-ttu-id="136b8-283">hello 다음 표에 나열 hello 매개 변수가 필요한 tooconfigure Azure 키 자격 증명 모음 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-283">hello following table lists hello parameters required tooconfigure Azure Key Vault Integration.</span></span>

| <span data-ttu-id="136b8-284">매개 변수</span><span class="sxs-lookup"><span data-stu-id="136b8-284">PARAMETER</span></span> | <span data-ttu-id="136b8-285">설명</span><span class="sxs-lookup"><span data-stu-id="136b8-285">DESCRIPTION</span></span> | <span data-ttu-id="136b8-286">예제</span><span class="sxs-lookup"><span data-stu-id="136b8-286">EXAMPLE</span></span> |
| --- | --- | --- |
| <span data-ttu-id="136b8-287">**주요 자격 증명 모음 URL**</span><span class="sxs-lookup"><span data-stu-id="136b8-287">**Key Vault URL**</span></span> |<span data-ttu-id="136b8-288">hello 위치 hello 주요 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-288">hello location of hello key vault.</span></span> |<span data-ttu-id="136b8-289">https://contosokeyvault.vault.azure.net/</span><span class="sxs-lookup"><span data-stu-id="136b8-289">https://contosokeyvault.vault.azure.net/</span></span> |
| <span data-ttu-id="136b8-290">**주체 이름**</span><span class="sxs-lookup"><span data-stu-id="136b8-290">**Principal name**</span></span> |<span data-ttu-id="136b8-291">Azure Active Directory 서비스 주체 이름.</span><span class="sxs-lookup"><span data-stu-id="136b8-291">Azure Active Directory service principal name.</span></span> <span data-ttu-id="136b8-292">이 이름은 이기도 하며 tooas hello 클라이언트 id입니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-292">This name is also referred tooas hello Client ID.</span></span> |<span data-ttu-id="136b8-293">fde2b411-33d5-4e11-af04eb07b669ccf2</span><span class="sxs-lookup"><span data-stu-id="136b8-293">fde2b411-33d5-4e11-af04eb07b669ccf2</span></span> |
| <span data-ttu-id="136b8-294">**주체 암호**</span><span class="sxs-lookup"><span data-stu-id="136b8-294">**Principal secret**</span></span> |<span data-ttu-id="136b8-295">Azure Active Directory 서비스 주체 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-295">Azure Active Directory service principal secret.</span></span> <span data-ttu-id="136b8-296">이 암호는 또한 참조 tooas hello 클라이언트 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-296">This secret is also referred tooas hello Client Secret.</span></span> |<span data-ttu-id="136b8-297">9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM=</span><span class="sxs-lookup"><span data-stu-id="136b8-297">9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM=</span></span> |
| <span data-ttu-id="136b8-298">**자격 증명 이름**</span><span class="sxs-lookup"><span data-stu-id="136b8-298">**Credential name**</span></span> |<span data-ttu-id="136b8-299">**자격 증명 이름**: AKV 통합 hello VM toohave 액세스 toohello 주요 자격 증명 모음을 허용 하는 SQL Server 내에서 자격 증명을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-299">**Credential name**: AKV Integration creates a credential within SQL Server, allowing hello VM toohave access toohello key vault.</span></span> <span data-ttu-id="136b8-300">이 자격 증명의 이름을 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="136b8-300">Choose a name for this credential.</span></span> |<span data-ttu-id="136b8-301">mycred1</span><span class="sxs-lookup"><span data-stu-id="136b8-301">mycred1</span></span> |

<span data-ttu-id="136b8-302">자세한 내용은 [Azure VM에서 SQL Server에 대한 Azure Key Vault 통합 구성](virtual-machines-windows-ps-sql-keyvault.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="136b8-302">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs](virtual-machines-windows-ps-sql-keyvault.md).</span></span>

<span data-ttu-id="136b8-303">SQL Server 설정 구성을 마치면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-303">When you are finished configuring SQL Server settings, click **OK**.</span></span>

### <a name="r-services"></a><span data-ttu-id="136b8-304">R 서비스</span><span class="sxs-lookup"><span data-stu-id="136b8-304">R services</span></span>
<span data-ttu-id="136b8-305">[SQL Server R 서비스](https://msdn.microsoft.com/library/mt604845.aspx)를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-305">You can enable [SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx).</span></span> <span data-ttu-id="136b8-306">SQL Server R Services는 SQL Server 2016으로 고급 toouse 분석이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-306">SQL Server R Services enables you toouse advanced analytics with SQL Server 2016.</span></span> <span data-ttu-id="136b8-307">클릭 **사용** hello에 **SQL Server 설정** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-307">Click **Enable** on hello **SQL Server Settings** blade.</span></span>

![SQL Server R 서비스 사용](./media/virtual-machines-windows-portal-sql-server-provision/azure-vm-sql-server-r-services.png)


## <a name="5-review-hello-summary"></a><span data-ttu-id="136b8-309">5. 요약 검토 hello</span><span class="sxs-lookup"><span data-stu-id="136b8-309">5. Review hello summary</span></span>
<span data-ttu-id="136b8-310">Hello에 **요약** 블레이드에서 검토 hello 요약 하 고 클릭 **확인** 이 VM에 대해 지정 된 SQL Server toocreate, 리소스 그룹 및 리소스.</span><span class="sxs-lookup"><span data-stu-id="136b8-310">On hello **Summary** blade, review hello summary and click **OK** toocreate SQL Server, resource group, and resources specified for this VM.</span></span>

<span data-ttu-id="136b8-311">Hello azure 포털에서 hello 배포를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-311">You can monitor hello deployment from hello azure portal.</span></span> <span data-ttu-id="136b8-312">hello **알림** hello hello 화면 위쪽에 단추를 클릭 hello 배포의 기본 상태를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-312">hello **Notifications** button at hello top of hello screen shows basic status of hello deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="136b8-313">tooprovide 시간이 배포에 대해 예측 하기 SQL VM toohello 미국 동부 지역 기본 설정으로 배포 하려면.</span><span class="sxs-lookup"><span data-stu-id="136b8-313">tooprovide you with an idea on deployment times, I deployed a SQL VM toohello East US region with default settings.</span></span> <span data-ttu-id="136b8-314">이 테스트 배포 환경에서는 총 26 분 toocomplete의 걸렸습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-314">This test deployment took a total of 26 minutes toocomplete.</span></span> <span data-ttu-id="136b8-315">사용자의 지역 및 선택한 설정에 따라서 배포 시간이 더 빠르거나 늦을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-315">But you might experience a faster or slower deployment time based on your region and selected settings.</span></span>
> 
> 

## <a name="open-hello-vm-with-remote-desktop"></a><span data-ttu-id="136b8-316">원격 데스크톱으로 hello VM을 열으십시오</span><span class="sxs-lookup"><span data-stu-id="136b8-316">Open hello VM with Remote Desktop</span></span>
<span data-ttu-id="136b8-317">다음 단계 tooconnect toohello 가상 컴퓨터 원격 데스크톱을 사용 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-317">Use hello following steps tooconnect toohello virtual machine with Remote Desktop:</span></span>

1. <span data-ttu-id="136b8-318">Hello Azure VM 작성 되 면 hello에 대 한 hello 아이콘 후 VM에서 Azure 대시보드에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-318">After hello Azure VM is built, hello icon for hello VM appears on your Azure dashboard.</span></span> <span data-ttu-id="136b8-319">기존 가상 컴퓨터를 검색하여 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-319">You can also find it by browsing your existing virtual machines.</span></span> <span data-ttu-id="136b8-320">새 SQL 가상 컴퓨터를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-320">Click on your new SQL virtual machine.</span></span> <span data-ttu-id="136b8-321">**가상 컴퓨터** 블레이드에 가상 컴퓨터 세부 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-321">A **Virtual machine** blade displays your virtual machine details.</span></span>
2. <span data-ttu-id="136b8-322">Hello의 hello 위쪽 **가상 컴퓨터** 블레이드에서 클릭 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-322">At hello top of hello **Virtual machine** blade, click **Connect**.</span></span>
3. <span data-ttu-id="136b8-323">hello 브라우저 hello VM에 대 한 RDP 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-323">hello browser downloads an RDP file for hello VM.</span></span> <span data-ttu-id="136b8-324">열기 hello RDP 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-324">Open hello RDP file.</span></span>
    <span data-ttu-id="136b8-325">![원격 데스크톱 tooSQL VM](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-remote-desktop.png)</span><span class="sxs-lookup"><span data-stu-id="136b8-325">![Remote Desktop tooSQL VM](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-remote-desktop.png)</span></span>
4. <span data-ttu-id="136b8-326">원격 데스크톱 연결 hello가 알려줍니다 해당 hello이 원격 연결의 게시자를 식별할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-326">hello Remote Desktop Connection notifies you that hello publisher of this remote connection cannot be identified.</span></span> <span data-ttu-id="136b8-327">클릭 **연결** toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-327">Click **Connect** toocontinue.</span></span>
5. <span data-ttu-id="136b8-328">Hello에 **Windows 보안** 대화 상자를 클릭 하 여 **다른 계정을 사용 하 여**합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-328">In hello **Windows Security** dialog, click **Use another account**.</span></span>
6. <span data-ttu-id="136b8-329">에 대 한 **사용자 이름** 형식  **\<사용자 이름 >**여기서 <user name> hello VM을 구성할 때 지정한 hello 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-329">For **User name** type **\<user name>**, where <user name> is hello user name that you specified when you configured hello VM.</span></span> <span data-ttu-id="136b8-330">Tooadd hello 이름 앞에 초기 백슬래시를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-330">You have tooadd an initial backslash before hello name.</span></span>
7. <span data-ttu-id="136b8-331">형식 hello **암호** 이전에이 vm을 구성을 클릭 한 다음 **확인** tooconnect 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-331">Type hello **Password** that you previously configured for this VM, and then click **OK** tooconnect.</span></span>
8. <span data-ttu-id="136b8-332">다른 경우 **원격 데스크톱 연결** 대화 묻는 여부 tooconnect, 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-332">If another **Remote Desktop Connection** dialog asks you whether tooconnect, click **Yes**.</span></span>

<span data-ttu-id="136b8-333">Toohello SQL Server 가상 컴퓨터를 연결한 후에 SQL Server Management Studio 실행 수 있으며 로컬 관리자 자격 증명을 사용 하 여 Windows 인증을 사용 하 여 연결 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-333">After you connect toohello SQL Server virtual machine, you can launch SQL Server Management Studio and connect with Windows Authentication using your local administrator credentials.</span></span> <span data-ttu-id="136b8-334">SQL Server 인증을 설정한 경우 SQL 인증 hello SQL 로그인 및 프로 비전 하는 동안 구성 된 암호를 사용 하 여 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-334">If you enabled SQL Server Authentication, you can also connect with SQL Authentication using hello SQL login and password you configured during provisioning.</span></span>

<span data-ttu-id="136b8-335">액세스 toohello 컴퓨터 toodirectly 변경 컴퓨터 및 요구 사항에 따라 SQL Server 설정을 사용 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-335">Access toohello machine enables you toodirectly change machine and SQL Server settings based on your requirements.</span></span> <span data-ttu-id="136b8-336">예를 들어 hello 방화벽 설정을 구성 하거나 SQL Server 구성 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-336">For example, you could configure hello firewall settings or change SQL Server configuration settings.</span></span>

## <a name="connect-toosql-server-remotely"></a><span data-ttu-id="136b8-337">TooSQL 서버를 원격으로 연결</span><span class="sxs-lookup"><span data-stu-id="136b8-337">Connect tooSQL Server remotely</span></span>
<span data-ttu-id="136b8-338">이 자습서에서는 선택한 **공용** hello 가상 컴퓨터에 대 한 액세스 및 **SQL Server 인증**합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-338">In this tutorial, we selected **Public** access for hello virtual machine and **SQL Server Authentication**.</span></span> <span data-ttu-id="136b8-339">이러한 설정을 자동으로 구성 된 hello 가상 컴퓨터 tooallow SQL Server 연결을 통해 모든 클라이언트에서 hello 인터넷 (hello 올바른 SQL 로그인에 게 이러한 가정).</span><span class="sxs-lookup"><span data-stu-id="136b8-339">These settings automatically configured hello virtual machine tooallow SQL Server connections from any client over hello internet (assuming they have hello correct SQL login).</span></span>

> [!NOTE]
> <span data-ttu-id="136b8-340">선택 하지 않은 Public이 프로 비전 하는 동안 추가 단계는 필요한 tooaccess를 통해 SQL Server 인스턴스 하는 경우 인터넷 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-340">If you did not select Public during provisioning, then extra steps are required tooaccess your SQL Server instance over hello internet.</span></span> <span data-ttu-id="136b8-341">자세한 내용은 참조 [tooa SQL Server 가상 컴퓨터를 연결](virtual-machines-windows-sql-connect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-341">For more information, see  [Connect tooa SQL Server Virtual Machine](virtual-machines-windows-sql-connect.md).</span></span>
> 
> 

<span data-ttu-id="136b8-342">다음 섹션 hello tooconnect tooyour SQL Server 인스턴스를 통해 다른 컴퓨터에서 VM에 인터넷 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-342">hello following sections show how tooconnect tooyour SQL Server instance on your VM from a different computer over hello internet.</span></span>

> [!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="136b8-343">다음 단계</span><span class="sxs-lookup"><span data-stu-id="136b8-343">Next Steps</span></span>
<span data-ttu-id="136b8-344">Azure에서 SQL Server를 사용 하는 방법에 대 한 기타 정보를 참조 하십시오. [Azure 가상 컴퓨터에 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md) 및 hello [질문과 대답](virtual-machines-windows-sql-server-iaas-faq.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-344">For other information about using SQL Server in Azure, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md) and hello [Frequently Asked Questions](virtual-machines-windows-sql-server-iaas-faq.md).</span></span>

<span data-ttu-id="136b8-345">SQL Server를 Azure 가상 컴퓨터의 비디오 개요를 감시 [Azure VM은 SQL Server 2016 용 hello 기능이 뛰어난](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016)합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-345">For a video overview of SQL Server on Azure Virtual Machines, watch [Azure VM is hello best platform for SQL Server 2016](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016).</span></span>

<span data-ttu-id="136b8-346">[Hello 학습 경로 탐색](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) Azure 가상 컴퓨터에 SQL Server에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="136b8-346">[Explore hello Learning Path](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) for SQL Server on Azure virtual machines.</span></span>

