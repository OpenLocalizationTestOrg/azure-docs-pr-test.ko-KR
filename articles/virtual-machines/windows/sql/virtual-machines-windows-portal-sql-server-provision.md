---
title: "SQL Server 가상 컴퓨터 aaaProvision | Microsoft Docs"
description: "만들고 hello 포털을 사용 하 여 Azure에서 tooa SQL Server 가상 컴퓨터를 연결 합니다. 이 자습서에서는 hello Resource Manager 모드를 사용 합니다."
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
ms.openlocfilehash: acb52b180103d83715b51b46e2519211c8f0e362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-in-hello-azure-portal"></a><span data-ttu-id="a160b-104">Hello Azure 포털에서에서 SQL Server 가상 컴퓨터를 프로 비전</span><span class="sxs-lookup"><span data-stu-id="a160b-104">Provision a SQL Server virtual machine in hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a160b-105">포털</span><span class="sxs-lookup"><span data-stu-id="a160b-105">Portal</span></span>](virtual-machines-windows-portal-sql-server-provision.md)
> * [<span data-ttu-id="a160b-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a160b-106">PowerShell</span></span>](virtual-machines-windows-ps-sql-create.md)
> 
> 

<span data-ttu-id="a160b-107">이 종단 간 자습서에서는 어떻게 toouse hello Azure 포털 tooprovision SQL Server를 실행 하는 가상 컴퓨터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-107">This end-to-end tutorial shows you how toouse hello Azure portal tooprovision a virtual machine running SQL Server.</span></span>

<span data-ttu-id="a160b-108">hello (VM) Azure 가상 컴퓨터 갤러리에 Microsoft SQL Server가 포함 된 몇 가지 이미지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-108">hello Azure virtual machine (VM) gallery includes several images that contain Microsoft SQL Server.</span></span> <span data-ttu-id="a160b-109">몇 번의 클릭 hello hello 갤러리에서 SQL VM 이미지 중 하나를 선택 하 고 프로 비전 할 Azure 환경에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-109">With a few clicks, you can select one of hello SQL VM images from hello gallery and provision it in your Azure environment.</span></span>

<span data-ttu-id="a160b-110">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-110">In this tutorial, you will:</span></span>

* [<span data-ttu-id="a160b-111">Hello 갤러리에서 SQL VM 이미지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-111">Select a SQL VM image from hello gallery</span></span>](#select-a-sql-vm-image-from-the-gallery)
* [<span data-ttu-id="a160b-112">구성 및 hello VM 만들기</span><span class="sxs-lookup"><span data-stu-id="a160b-112">Configure and create hello VM</span></span>](#configure-the-vm)
* [<span data-ttu-id="a160b-113">원격 데스크톱으로 hello VM을 열으십시오</span><span class="sxs-lookup"><span data-stu-id="a160b-113">Open hello VM with Remote Desktop</span></span>](#open-the-vm-with-remote-desktop)
* [<span data-ttu-id="a160b-114">TooSQL 서버를 원격으로 연결</span><span class="sxs-lookup"><span data-stu-id="a160b-114">Connect tooSQL Server remotely</span></span>](#connect-to-sql-server-remotely)

## <a name="select-a-sql-vm-image-from-hello-gallery"></a><span data-ttu-id="a160b-115">Hello 갤러리에서 SQL VM 이미지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-115">Select a SQL VM image from hello gallery</span></span>

1. <span data-ttu-id="a160b-116">Toohello 로그인 [Azure 포털](https://portal.azure.com) 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-116">Log in toohello [Azure portal](https://portal.azure.com) using your account.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a160b-117">Azure 계정이 없는 경우 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)을 방문하십시오.</span><span class="sxs-lookup"><span data-stu-id="a160b-117">If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

2. <span data-ttu-id="a160b-118">Hello Azure 포털에서 클릭 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-118">On hello Azure portal, click **New**.</span></span> <span data-ttu-id="a160b-119">hello 포털이 열립니다 hello **새로** 창.</span><span class="sxs-lookup"><span data-stu-id="a160b-119">hello portal opens hello **New** window.</span></span>

3. <span data-ttu-id="a160b-120">Hello에 **새로** 창 클릭 **계산** 클릭 하 고 **스크롤하게**합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-120">In hello **New** window, click **Compute** and then click **See all**.</span></span>

   ![새 계산 창](./media/virtual-machines-windows-portal-sql-server-provision/azure-new-compute-blade.png)

4. <span data-ttu-id="a160b-122">Hello 검색 필드에 입력 **SQL Server**, ENTER 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-122">In hello search field, type **SQL Server**, and press ENTER.</span></span>

5. <span data-ttu-id="a160b-123">Hello 클릭 **필터** 아이콘과 선택 **Microsoft** hello 게시자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-123">Then click hello **Filter** icon and select **Microsoft** for hello publisher.</span></span> <span data-ttu-id="a160b-124">클릭 **수행** tooMicrosoft hello 필터 toofilter hello 결과 창에 SQL Server 이미지를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-124">Click **Done** on hello filter window toofilter hello results tooMicrosoft published SQL Server images.</span></span>

   ![Azure Virtual Machines 창](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-blade2.png)

5. <span data-ttu-id="a160b-126">Hello 제공 되는 SQL Server 이미지를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-126">Review hello available SQL Server images.</span></span> <span data-ttu-id="a160b-127">각 이미지는 SQL Server 버전 및 운영 체제를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-127">Each image identifies a SQL Server version and an operating system.</span></span>

6. <span data-ttu-id="a160b-128">라는 선택 hello 이미지 **무료 라이선스: Windows Server 2016에서 SQL Server 2016 SP1 Developer**합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-128">Select hello image named **Free License: SQL Server 2016 SP1 Developer on Windows Server 2016**.</span></span>

   > [!TIP]
   > <span data-ttu-id="a160b-129">hello Developer edition은 테스트 목적으로 개발에 대 한 무료 SQL Server의 모든 기능을 갖춘 버전 이기 때문에이 자습서에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-129">hello Developer edition is used in this tutorial because it is a full-featured edition of SQL Server that is free for development testing purposes.</span></span> <span data-ttu-id="a160b-130">Hello 실행 비용을 hello VM에 대해서만 지불 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-130">You pay only for hello cost of running hello VM.</span></span> <span data-ttu-id="a160b-131">하지만 무료 toochoose는이 자습서에서는 hello 이미지 toouse 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-131">However, you are free toochoose any of hello images toouse in this tutorial.</span></span>

   > [!TIP]
   > <span data-ttu-id="a160b-132">SQL VM 이미지 SQL Server 라이선스 비용 hello hello hello 개발자 및 Express 버전만) (제외 만드는 VM의 hello 분 당 가격에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-132">SQL VM images include hello licensing costs for SQL Server into hello per-minute pricing of hello VM you create (except for hello Developer and Express editions).</span></span> <span data-ttu-id="a160b-133">SQL Server Developer는 개발/테스트(비 프로덕션)에 대해 무료이며 SQL Express는 간단한 작업(1GB 미만의 메모리, 10GB 미만의 저장소)에 대해 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-133">SQL Server Developer is free for development/testing (not production) and SQL Express is free for lightweight workloads (less than 1GB memory, less than 10 GB storage).</span></span> <span data-ttu-id="a160b-134">다른 옵션 toobring your-소유-라이선스 (BYOL) 고 hello VM에 대해서만 지불 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-134">There is another option toobring-your-own-license (BYOL) and pay only for hello VM.</span></span> <span data-ttu-id="a160b-135">이러한 이미지 이름에는 접두사 {BYOL}이 붙습니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-135">Those image names are prefixed with {BYOL}.</span></span> 
   >
   > <span data-ttu-id="a160b-136">이러한 옵션에 대한 자세한 내용은 [SQL Server Azure VM에 대한 가격 책정 지침](virtual-machines-windows-sql-server-pricing-guidance.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a160b-136">For more information on these options, see [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md).</span></span>

7. <span data-ttu-id="a160b-137">**배포 모델 선택**에서 **리소스 관리자**가 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-137">Under **Select a deployment model**, verify that **Resource Manager** is selected.</span></span> <span data-ttu-id="a160b-138">리소스 관리자는 새 가상 컴퓨터에 대 한 배포 모델을 권장 하는 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-138">Resource Manager is hello recommended deployment model for new virtual machines.</span></span> 

8. <span data-ttu-id="a160b-139">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-139">Click **Create**.</span></span>

    ![리소스 관리자로 SQL VM 만들기](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-sql-deployment-model.png)

## <a name="configure-hello-vm"></a><span data-ttu-id="a160b-141">Hello VM 구성</span><span class="sxs-lookup"><span data-stu-id="a160b-141">Configure hello VM</span></span>
<span data-ttu-id="a160b-142">SQL Server 가상 컴퓨터를 구성하기 위한 5개의 창이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-142">There are five windows for configuring a SQL Server virtual machine.</span></span>

| <span data-ttu-id="a160b-143">단계</span><span class="sxs-lookup"><span data-stu-id="a160b-143">Step</span></span> | <span data-ttu-id="a160b-144">설명</span><span class="sxs-lookup"><span data-stu-id="a160b-144">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a160b-145">**기본 사항**</span><span class="sxs-lookup"><span data-stu-id="a160b-145">**Basics**</span></span> |[<span data-ttu-id="a160b-146">기본 설정 구성</span><span class="sxs-lookup"><span data-stu-id="a160b-146">Configure basic settings</span></span>](#1-configure-basic-settings) |
| <span data-ttu-id="a160b-147">**크기**</span><span class="sxs-lookup"><span data-stu-id="a160b-147">**Size**</span></span> |[<span data-ttu-id="a160b-148">가상 컴퓨터 크기 선택</span><span class="sxs-lookup"><span data-stu-id="a160b-148">Choose virtual machine size</span></span>](#2-choose-virtual-machine-size) |
| <span data-ttu-id="a160b-149">**설정**</span><span class="sxs-lookup"><span data-stu-id="a160b-149">**Settings**</span></span> |[<span data-ttu-id="a160b-150">선택적 기능 구성</span><span class="sxs-lookup"><span data-stu-id="a160b-150">Configure optional features</span></span>](#3-configure-optional-features) |
| <span data-ttu-id="a160b-151">**SQL 서버 설정**</span><span class="sxs-lookup"><span data-stu-id="a160b-151">**SQL Server settings**</span></span> |[<span data-ttu-id="a160b-152">SQL Server 설정 구성</span><span class="sxs-lookup"><span data-stu-id="a160b-152">Configure SQL server settings</span></span>](#4-configure-sql-server-settings) |
| <span data-ttu-id="a160b-153">**요약**</span><span class="sxs-lookup"><span data-stu-id="a160b-153">**Summary**</span></span> |[<span data-ttu-id="a160b-154">요약 검토 hello</span><span class="sxs-lookup"><span data-stu-id="a160b-154">Review hello summary</span></span>](#5-review-the-summary) |

## <a name="1-configure-basic-settings"></a><span data-ttu-id="a160b-155">1. 기본 설정 구성</span><span class="sxs-lookup"><span data-stu-id="a160b-155">1. Configure basic settings</span></span>

<span data-ttu-id="a160b-156">Hello에 **기본 사항** 창의 hello 다음 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-156">On hello **Basics** window, provide hello following information:</span></span>

* <span data-ttu-id="a160b-157">고유한 가상 컴퓨터 **이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-157">Enter a unique virtual machine **Name**.</span></span>

* <span data-ttu-id="a160b-158">최적의 성능을 위해 VM 디스크 유형에 **SSD**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-158">Select **SSD** for VM disk type for optimal performance.</span></span>

* <span data-ttu-id="a160b-159">지정 된 **사용자 이름** hello hello VM 로컬 관리자 계정에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-159">Specify a **User name** for hello local administrator account on hello VM.</span></span> <span data-ttu-id="a160b-160">이 계정은 SQL Server toohello도 추가 **sysadmin** 고정된 서버 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-160">This account is also added toohello SQL Server **sysadmin** fixed server role.</span></span>

* <span data-ttu-id="a160b-161">강력한 **암호**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-161">Provide a strong **Password**.</span></span>

* <span data-ttu-id="a160b-162">Hello 구독에 대해 올바른지 확인 하는 여러 구독이 있는 경우에 새 VM hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-162">If you have multiple subscriptions, verify that hello subscription is correct for hello new VM.</span></span>

* <span data-ttu-id="a160b-163">Hello에 **리소스 그룹** 상자에 새 리소스 그룹에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-163">In hello **Resource group** box, type a name for a new resource group.</span></span> <span data-ttu-id="a160b-164">또는 toouse 기존 리소스 그룹 클릭 **기존 항목 사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-164">Alternatively, toouse an existing resource group click **Use existing**.</span></span> <span data-ttu-id="a160b-165">리소스 그룹은 Azure 내 관련 리소스의 컬렉션입니다(가상 컴퓨터, 저장소 계정, 가상 네트워크 등).</span><span class="sxs-lookup"><span data-stu-id="a160b-165">A resource group is a collection of related resources in Azure (virtual machines, storage accounts, virtual networks, etc.).</span></span>

  > [!NOTE]
  > <span data-ttu-id="a160b-166">새 리소스 그룹을 사용하면 Azure에서 SQL Server 배포를 테스트하거나 알아보는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-166">Using a new resource group is helpful if you are just testing or learning about SQL Server deployments in Azure.</span></span> <span data-ttu-id="a160b-167">테스트와 완료 된 후 hello 리소스 그룹 tooautomatically delete hello VM 및 해당 리소스 그룹에 연결 된 모든 리소스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-167">After you finish with your test, delete hello resource group tooautomatically delete hello VM and all resources associated with that resource group.</span></span> <span data-ttu-id="a160b-168">리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../../../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a160b-168">For more information about resource groups, see [Azure Resource Manager Overview](../../../azure-resource-manager/resource-group-overview.md).</span></span>

* <span data-ttu-id="a160b-169">선택 된 **위치** hello이이 배포를 호스팅하는 Azure 지역에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-169">Select a **Location** for hello Azure region that will host this deployment.</span></span>

* <span data-ttu-id="a160b-170">클릭 **확인** toosave hello 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-170">Click **OK** toosave hello settings.</span></span>

    ![SQL 기본 창](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-basic.png)

## <a name="2-choose-virtual-machine-size"></a><span data-ttu-id="a160b-172">2. 가상 컴퓨터 크기 선택</span><span class="sxs-lookup"><span data-stu-id="a160b-172">2. Choose virtual machine size</span></span>

<span data-ttu-id="a160b-173">Hello에 **크기** 단계, hello에 가상 컴퓨터 크기 선택 **크기 선택** 창.</span><span class="sxs-lookup"><span data-stu-id="a160b-173">On hello **Size** step, choose a virtual machine size in hello **Choose a size** window.</span></span> <span data-ttu-id="a160b-174">hello 창은 선택한 hello 이미지에 따라 권장된 컴퓨터 크기를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-174">hello window initially displays recommended machine sizes based on hello image you selected.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a160b-175">hello 예상 hello에 표시 되는 월별 비용 **크기를 선택** 창에 SQL Server 라이선스 비용 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-175">hello estimated monthly cost displayed on hello **Choose a size** window does not include SQL Server licensing costs.</span></span> <span data-ttu-id="a160b-176">이 hello 단독 VM의 hello 비용입니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-176">This is hello cost of hello VM alone.</span></span> <span data-ttu-id="a160b-177">SQL Server의 hello Express 및 Developer 버전에서 hello 총 예상된 비용입니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-177">For hello Express and Developer editions of SQL Server, this is hello total estimated cost.</span></span> <span data-ttu-id="a160b-178">다른 버전에 대 한 참조 hello [Windows 가상 컴퓨터 가격 책정 페이지](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) 하 고 SQL Server의 대상 버전을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-178">For other editions, see hello [Windows Virtual Machines pricing page](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) and select your target edition of SQL Server.</span></span> <span data-ttu-id="a160b-179">또한 hello 참조 [SQL Server Azure Vm에 대 한 지침을 가격](virtual-machines-windows-sql-server-pricing-guidance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-179">Also see hello [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md).</span></span>

![SQL VM 크기 옵션](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-choose-a-size.png)

<span data-ttu-id="a160b-181">프로덕션 작업에 대 한 hello 컴퓨터 크기 및 구성에서 권장을 보려면 [Azure 가상 컴퓨터의 SQL Server에 대 한 성능 모범 사례](virtual-machines-windows-sql-performance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-181">For production workloads, see hello recommended machine sizes and configuration in [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span></span> <span data-ttu-id="a160b-182">나열 되지 않은 컴퓨터 크기를 해야 하는 경우 클릭 hello **모든 보기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-182">If you need a machine size that is not listed, click hello **View all** button.</span></span>

> [!NOTE]
> <span data-ttu-id="a160b-183">가상 컴퓨터 크기에 대한 자세한 내용은 [가상 컴퓨터 크기](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a160b-183">For more information about virtual machine sizes see, [Sizes for virtual machines](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="a160b-184">컴퓨터 크기를 선택한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-184">Choose your machine size, and then click **Select**.</span></span>

## <a name="3-configure-optional-features"></a><span data-ttu-id="a160b-185">3. 선택적 기능 구성</span><span class="sxs-lookup"><span data-stu-id="a160b-185">3. Configure optional features</span></span>

<span data-ttu-id="a160b-186">Hello에 **설정을** 창에서 Azure 저장소, 네트워킹, 및 hello 가상 컴퓨터에 대 한 모니터링을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-186">On hello **Settings** window, configure Azure storage, networking, and monitoring for hello virtual machine.</span></span>

* <span data-ttu-id="a160b-187">**Storage**의 **Managed Disks**에서 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-187">Under **Storage**, select **Yes** under use **Managed Disks**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a160b-188">SQL Server에 Managed Disks를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-188">Microsoft recommends Managed Disks for SQL Server.</span></span> <span data-ttu-id="a160b-189">Hello 백그라운드 핸들 저장소 디스크를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-189">Managed Disks handles storage behind hello scenes.</span></span> <span data-ttu-id="a160b-190">또한 관리 되는 디스크와 가상 컴퓨터에에서 있는 경우 hello 동일한 가용성 집합에 Azure hello 저장소 리소스 tooprovide 적절 한 중복 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-190">In addition, when virtual machines with Managed Disks are in hello same availability set, Azure distributes hello storage resources tooprovide appropriate redundancy.</span></span> <span data-ttu-id="a160b-191">자세한 내용은 [Azure Managed Disks 개요](../../../storage/storage-managed-disks-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a160b-191">For additional information, see [Azure Managed Disks Overview](../../../storage/storage-managed-disks-overview.md).</span></span> <span data-ttu-id="a160b-192">가용성 집합의 Managed Disks에 대한 구체적인 내용을 보려면 [가용성 집합에서 VM에 Managed Disks 사용](../manage-availability.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a160b-192">For specifics about managed disks in an availability set, see [Use managed disks for VMs in availability set](../manage-availability.md).</span></span>

* <span data-ttu-id="a160b-193">아래 **네트워크**를 자동으로 채울 hello 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-193">Under **Network**, you can accept hello automatically populated values.</span></span> <span data-ttu-id="a160b-194">각 기능을 클릭할 수도 있습니다 toomanually hello 구성 **가상 네트워크**, **서브넷**, **공용 IP 주소**, 및 **네트워크보안그룹**.</span><span class="sxs-lookup"><span data-stu-id="a160b-194">You can also click on each feature toomanually configure hello **Virtual network**, **Subnet**, **Public IP address**, and **Network Security Group**.</span></span> <span data-ttu-id="a160b-195">이 자습서의 hello 위해 hello 기본값을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-195">For hello purposes of this tutorial, keep hello default values.</span></span>

* <span data-ttu-id="a160b-196">Azure 사용 **모니터링** hello VM에 대해 동일한 저장소 계정을 지정 하는 hello로 기본적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-196">Azure enables **Monitoring** by default with hello same storage account designated for hello VM.</span></span> <span data-ttu-id="a160b-197">여기에서 이러한 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-197">You can change these settings here.</span></span>

* <span data-ttu-id="a160b-198">아래 **가용성 집합**, hello 기본값은 그대로 두면 **none** 이 자습서에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-198">Under **Availability set**, you can leave hello default of **none** for this tutorial.</span></span> <span data-ttu-id="a160b-199">SQL AlwaysOn 가용성 그룹을 tooset 하려는 경우 hello 가용성 tooavoid 다시 만들고 hello 가상 컴퓨터를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-199">If you plan tooset up SQL AlwaysOn Availability Groups, configure hello availability tooavoid recreating hello virtual machine.</span></span>  <span data-ttu-id="a160b-200">자세한 내용은 참조 [가상 컴퓨터의 가용성 관리 hello](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-200">For more information, see [Manage hello Availability of Virtual Machines](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="a160b-201">이러한 설정 구성을 완료한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-201">When you are done configuring these settings, click **OK**.</span></span>

## <a name="4-configure-sql-server-settings"></a><span data-ttu-id="a160b-202">4. SQL Server 설정 구성</span><span class="sxs-lookup"><span data-stu-id="a160b-202">4. Configure SQL server settings</span></span>
<span data-ttu-id="a160b-203">Hello에 **SQL Server 설정을** 창에서 특정 설정 및 SQL Server에 대 한 최적화를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-203">On hello **SQL Server settings** window, configure specific settings and optimizations for SQL Server.</span></span> <span data-ttu-id="a160b-204">SQL Server에 대해 구성할 수 있는 hello 설정을 hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-204">hello settings that you can configure for SQL Server include hello following.</span></span>

| <span data-ttu-id="a160b-205">설정</span><span class="sxs-lookup"><span data-stu-id="a160b-205">Setting</span></span> |
| --- |
| [<span data-ttu-id="a160b-206">연결</span><span class="sxs-lookup"><span data-stu-id="a160b-206">Connectivity</span></span>](#connectivity) |
| [<span data-ttu-id="a160b-207">인증</span><span class="sxs-lookup"><span data-stu-id="a160b-207">Authentication</span></span>](#authentication) |
| [<span data-ttu-id="a160b-208">Storage 구성</span><span class="sxs-lookup"><span data-stu-id="a160b-208">Storage configuration</span></span>](#storage-configuration) |
| [<span data-ttu-id="a160b-209">자동화된 패치</span><span class="sxs-lookup"><span data-stu-id="a160b-209">Automated Patching</span></span>](#automated-patching) |
| [<span data-ttu-id="a160b-210">자동화된 Backup</span><span class="sxs-lookup"><span data-stu-id="a160b-210">Automated Backup</span></span>](#automated-backup) |
| [<span data-ttu-id="a160b-211">Azure Key Vault 통합</span><span class="sxs-lookup"><span data-stu-id="a160b-211">Azure Key Vault Integration</span></span>](#azure-key-vault-integration) |
| [<span data-ttu-id="a160b-212">R 서비스</span><span class="sxs-lookup"><span data-stu-id="a160b-212">R Services</span></span>](#r-services) |

### <a name="connectivity"></a><span data-ttu-id="a160b-213">연결</span><span class="sxs-lookup"><span data-stu-id="a160b-213">Connectivity</span></span>

<span data-ttu-id="a160b-214">**SQL 연결**, hello 유형을 지정 하려는이 VM의 SQL Server 인스턴스에 toohello 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-214">Under **SQL connectivity**, specify hello type of access you want toohello SQL Server instance on this VM.</span></span> <span data-ttu-id="a160b-215">이 자습서의 hello 위해서 선택 **공개 (인터넷)** tooallow 연결 tooSQL 서버 컴퓨터 또는 서비스를 통해 인터넷 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-215">For hello purposes of this tutorial, select **Public (internet)** tooallow connections tooSQL Server from machines or services on hello internet.</span></span> <span data-ttu-id="a160b-216">이 옵션을 선택 하면 Azure에서 자동으로 구성 hello 방화벽 및 네트워크 보안 그룹 tooallow 트래픽 hello 포트 1433입니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-216">With this option selected, Azure automatically configures hello firewall and hello network security group tooallow traffic on port 1433.</span></span>

![SQL 연결 옵션](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-connectivity-alt.png)

> [!TIP]
> <span data-ttu-id="a160b-218">기본적으로 SQL Server는 잘 알려진 포트 **1433**에서 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-218">By default, SQL Server listens on a well-known port, **1433**.</span></span> <span data-ttu-id="a160b-219">보안 향상된을 위해 1401 등의 기본이 아닌 포트에서 이전 대화 toolisten hello에에서 hello 포트를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-219">For increased security, change hello port in hello previous dialog toolisten on a non-default port, such as 1401.</span></span> <span data-ttu-id="a160b-220">이 작업을 수행할 경우 SSMS와 같이 모든 클라이언트 도구의 해당 포트를 사용하여 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-220">If you do this, you must connect using that port from any client tools, such as SSMS.</span></span>

<span data-ttu-id="a160b-221">tooconnect tooSQL 서버 hello 통해 인터넷을도 인증을 활성화 해야 SQL Server, hello 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-221">tooconnect tooSQL Server via hello internet, you also must enable SQL Server Authentication, which is described in hello next section.</span></span>

<span data-ttu-id="a160b-222">Toonot enable 연결 toohello 데이터베이스 엔진을 사용 하도록 하려는 경우를 통해 인터넷 hello, hello 다음 옵션 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-222">If you would prefer toonot enable connections toohello Database Engine via hello internet, choose one of hello following options:</span></span>

* <span data-ttu-id="a160b-223">**VM에만 해당) (내 로컬** tooallow 연결 tooSQL 에서만 서버 hello VM 내에서.</span><span class="sxs-lookup"><span data-stu-id="a160b-223">**Local (inside VM only)** tooallow connections tooSQL Server only from within hello VM.</span></span>
* <span data-ttu-id="a160b-224">**(가상 네트워크 내에서) 개인** tooallow 연결 tooSQL 서버 hello의 서비스 또는 컴퓨터에서 동일한 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-224">**Private (within Virtual Network)** tooallow connections tooSQL Server from machines or services in hello same virtual network.</span></span>

<span data-ttu-id="a160b-225">일반적으로 시나리오에서 허용 하는 hello 가장 제한적인 연결을 선택 하 여 보안을 향상 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-225">In general, improve security by choosing hello most restrictive connectivity that your scenario allows.</span></span> <span data-ttu-id="a160b-226">하지만 모든 hello 옵션은 네트워크 보안 그룹 규칙 및 SQL/Windows 인증을 통해 보안 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-226">But all hello options are securable through Network Security Group rules and SQL/Windows Authentication.</span></span> <span data-ttu-id="a160b-227">Hello VM이 생성 한 후 네트워크 보안 그룹을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-227">You can edit Network Security Group after hello VM is created.</span></span> <span data-ttu-id="a160b-228">자세한 내용은 [Azure Virtual Machines의 SQL Server에 대한 보안 고려 사항](virtual-machines-windows-sql-security.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a160b-228">For more information, see [Security Considerations for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-security.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a160b-229">SQL Server Express edition에 대 한 가상 컴퓨터 이미지 hello hello TCP/IP 프로토콜을 자동으로 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-229">hello virtual machine image for SQL Server Express edition does not automatically enable hello TCP/IP protocol.</span></span> <span data-ttu-id="a160b-230">이 hello 공용 및 전용 연결에도 적용 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-230">This is true even for hello Public and  Private connectivity options.</span></span> <span data-ttu-id="a160b-231">Express edition을 사용 해야 SQL Server 구성 관리자 너무[수동으로 hello TCP/IP 프로토콜을 사용 하도록 설정](#configure-sql-server-to-listen-on-the-tcp-protocol) hello VM을 만든 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-231">For Express edition, you must use SQL Server Configuration Manager too[manually enable hello TCP/IP protocol](#configure-sql-server-to-listen-on-the-tcp-protocol) after creating hello VM.</span></span>

### <a name="authentication"></a><span data-ttu-id="a160b-232">인증</span><span class="sxs-lookup"><span data-stu-id="a160b-232">Authentication</span></span>

<span data-ttu-id="a160b-233">SQL Server 인증이 필요하도록 지정하려면 **사용** under **사용**을 방문하십시오.</span><span class="sxs-lookup"><span data-stu-id="a160b-233">If you require SQL Server Authentication, click **Enable** under **SQL authentication**.</span></span>

![SQL Server 인증](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-authentication.png)

> [!NOTE]
> <span data-ttu-id="a160b-235">통해 tooaccess SQL Server를 계획 하는 경우 hello 인터넷 (예: hello 공용 연결 옵션), 여기에 SQL 인증을 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-235">If you plan tooaccess SQL Server over hello internet (i.e. hello Public connectivity option), you must enable SQL authentication here.</span></span> <span data-ttu-id="a160b-236">공용 액세스 toohello SQL Server에는 SQL 인증 hello 사용을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-236">Public access toohello SQL Server requires hello use of SQL Authentication.</span></span>
> 
> 

<span data-ttu-id="a160b-237">SQL Server 인증을 사용하도록 설정하는 경우 **로그인 이름** 및 **암호**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-237">If you enable SQL Server Authentication, specify a **Login name** and **Password**.</span></span> <span data-ttu-id="a160b-238">이 사용자 이름은 SQL Server 인증 로그인 및 hello의 구성원으로 구성 된 **sysadmin** 고정된 서버 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-238">This user name is configured as a SQL Server Authentication login and member of hello **sysadmin** fixed server role.</span></span> <span data-ttu-id="a160b-239">인증 모드에 대한 자세한 내용은 [인증 모드 선택](https://docs.microsoft.com/sql/relational-databases/security/choose-an-authentication-mode)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a160b-239">See [Choose an Authentication Mode](https://docs.microsoft.com/sql/relational-databases/security/choose-an-authentication-mode) for more information about Authentication Modes.</span></span>

<span data-ttu-id="a160b-240">SQL Server 인증을 사용 하지 않도록 하는 경우 로컬 관리자 계정을 hello hello VM tooconnect toohello SQL Server 인스턴스에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-240">If you do not enable SQL Server Authentication, then you can use hello local Administrator account on hello VM tooconnect toohello SQL Server instance.</span></span>

### <a name="storage-configuration"></a><span data-ttu-id="a160b-241">Storage 구성</span><span class="sxs-lookup"><span data-stu-id="a160b-241">Storage configuration</span></span>

<span data-ttu-id="a160b-242">클릭 **저장소 구성** toospecify hello에 대 한 저장소 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-242">Click **Storage configuration** toospecify hello storage requirements.</span></span>

![SQL Storage 구성](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-storage.png)

> [!NOTE]
> <span data-ttu-id="a160b-244">VM toouse 표준 저장소를 수동으로 구성한 경우이 옵션은 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-244">If you manually configured your VM toouse standard storage, this option is not available.</span></span> <span data-ttu-id="a160b-245">자동 저장소 최적화는 Premium Storage에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-245">Automatic storage optimization is available only for Premium Storage.</span></span>

> [!TIP]
> <span data-ttu-id="a160b-246">위치의 hello 수 및 각 슬라이더의 상한값 hello 선택한 VM의 hello 크기에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-246">hello number of stops and hello upper limits of each slider is dependent on hello size of VM you selected.</span></span> <span data-ttu-id="a160b-247">더 큰 효율적이 고 VM이 더 수 tooscale 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-247">A larger and more powerful VM is able tooscale up more.</span></span>

<span data-ttu-id="a160b-248">초당 입/출력 작업(IOPs), 처리량(MB/s) 및 총 저장소 크기로 요구 사항을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-248">You can specify requirements as input/output operations per second (IOPs), throughput in MB/s, and total storage size.</span></span> <span data-ttu-id="a160b-249">Hello 슬라이딩 눈금을 사용 하 여 이러한 값을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-249">Configure these values by using hello sliding scales.</span></span> <span data-ttu-id="a160b-250">워크로드에 따라 이러한 저장소 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-250">You can change these storage settings based on workload.</span></span> <span data-ttu-id="a160b-251">디스크 tooattach 수가 hello 및 구성에 자동으로 hello 포털 계산 이러한 요구 사항을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-251">hello portal automatically calculates hello number of disks tooattach and configure based on these requirements.</span></span>

<span data-ttu-id="a160b-252">아래 **저장소에 대 한 액세스에 최적화 된**, hello 다음 옵션 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-252">Under **Storage optimized for**, select one of hello following options:</span></span>

* <span data-ttu-id="a160b-253">**일반** hello 기본 설정 이며 대부분의 워크 로드를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-253">**General** is hello default setting and supports most workloads.</span></span>
* <span data-ttu-id="a160b-254">**트랜잭션** 처리 일반 데이터베이스 OLTP 워크 로드에 대 한 hello 저장소를 최적화 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-254">**Transactional** processing optimizes hello storage for traditional database OLTP workloads.</span></span>
* <span data-ttu-id="a160b-255">**데이터 웨어하우징** 분석 및 보고 작업에 대 한 hello 저장소를 최적화 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-255">**Data warehousing** optimizes hello storage for analytic and reporting workloads.</span></span>

### <a name="automated-patching"></a><span data-ttu-id="a160b-256">자동화된 패치</span><span class="sxs-lookup"><span data-stu-id="a160b-256">Automated patching</span></span>

<span data-ttu-id="a160b-257">**Automated patching**이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-257">**Automated patching** is enabled by default.</span></span> <span data-ttu-id="a160b-258">자동화 된 패치 적용 Azure tooautomatically 패치 hello 및 SQL Server 운영 체제 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-258">Automated patching allows Azure tooautomatically patch SQL Server and hello operating system.</span></span> <span data-ttu-id="a160b-259">요일을 한 hello 주, 시간 및 유지 관리 기간에 대 한 기간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-259">Specify a day of hello week, time, and duration for a maintenance window.</span></span> <span data-ttu-id="a160b-260">Azure에서 유지 관리 기간에 패치를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-260">Azure performs patching in this maintenance window.</span></span> <span data-ttu-id="a160b-261">hello 유지 관리 창 일정 시간에 대 한 hello VM 로캘을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-261">hello maintenance window schedule uses hello VM locale for time.</span></span> <span data-ttu-id="a160b-262">Azure tooautomatically 패치 hello 및 SQL Server 운영 체제 하지 않으려면 클릭 **사용 하지 않도록 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-262">If you do not want Azure tooautomatically patch SQL Server and hello operating system, click **Disable**.</span></span>  

![SQL 자동화된 패치](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-patching.png)

<span data-ttu-id="a160b-264">자세한 내용은 [Azure Virtual Machines에서 SQL Server의 자동화된 패치](virtual-machines-windows-sql-automated-patching.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a160b-264">For more information, see [Automated Patching for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-automated-patching.md).</span></span>

### <a name="automated-backup"></a><span data-ttu-id="a160b-265">자동화된 백업</span><span class="sxs-lookup"><span data-stu-id="a160b-265">Automated backup</span></span>

<span data-ttu-id="a160b-266">**자동화된 백업**에서 모든 데이터베이스에 대해 자동 데이터베이스 백업을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-266">Enable automatic database backups for all databases under **Automated backup**.</span></span> <span data-ttu-id="a160b-267">자동화된 백업은 기본적으로 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-267">Automated backup is disabled by default.</span></span>

<span data-ttu-id="a160b-268">SQL 자동화 된 백업을 사용 하도록 설정 하면 hello 다음을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-268">When you enable SQL automated backup, you can configure hello following:</span></span>

* <span data-ttu-id="a160b-269">백업에 대한 보존 기간(일)</span><span class="sxs-lookup"><span data-stu-id="a160b-269">Retention period (days) for backups</span></span>
* <span data-ttu-id="a160b-270">백업에 대 한 저장소 계정 toouse</span><span class="sxs-lookup"><span data-stu-id="a160b-270">Storage account toouse for backups</span></span>
* <span data-ttu-id="a160b-271">백업을 위한 암호화 옵션 및 암호</span><span class="sxs-lookup"><span data-stu-id="a160b-271">Encryption option and password for backups</span></span>
* <span data-ttu-id="a160b-272">시스템 데이터베이스 백업</span><span class="sxs-lookup"><span data-stu-id="a160b-272">Backup system databases</span></span>
* <span data-ttu-id="a160b-273">백업 일정 구성</span><span class="sxs-lookup"><span data-stu-id="a160b-273">Configure backup schedule</span></span>

<span data-ttu-id="a160b-274">tooencrypt hello 백업, 클릭 **사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-274">tooencrypt hello backup, click **Enable**.</span></span> <span data-ttu-id="a160b-275">그런 다음 hello 지정 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-275">Then specify hello **Password**.</span></span> <span data-ttu-id="a160b-276">Azure 인증서 tooencrypt hello 백업을 만들고 사용 하 여 hello 암호 tooprotect 해당 인증서를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-276">Azure creates a certificate tooencrypt hello backups and uses hello specified password tooprotect that certificate.</span></span>

![SQL 자동화된 Backup](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-autobackup2.png)

 <span data-ttu-id="a160b-278">자세한 내용은 [Azure Virtual Machines에서 SQL Server에 대한 자동화된 Backup](virtual-machines-windows-sql-automated-backup.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a160b-278">For more information, see [Automated Backup for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).</span></span>

### <a name="azure-key-vault-integration"></a><span data-ttu-id="a160b-279">Azure Key Vault 통합</span><span class="sxs-lookup"><span data-stu-id="a160b-279">Azure Key Vault integration</span></span>

<span data-ttu-id="a160b-280">암호화를 위해 Azure의 보안 암호 toostore 클릭 **Azure 키 자격 증명 모음 통합** 클릭 **사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-280">toostore security secrets in Azure for encryption, click **Azure key vault integration** and click **Enable**.</span></span>

![SQL Azure Key Vault 통합](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-akv.png)

<span data-ttu-id="a160b-282">hello 다음 표에 나열 hello 매개 변수가 필요한 tooconfigure Azure 키 자격 증명 모음 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-282">hello following table lists hello parameters required tooconfigure Azure Key Vault Integration.</span></span>

| <span data-ttu-id="a160b-283">매개 변수</span><span class="sxs-lookup"><span data-stu-id="a160b-283">PARAMETER</span></span> | <span data-ttu-id="a160b-284">설명</span><span class="sxs-lookup"><span data-stu-id="a160b-284">DESCRIPTION</span></span> | <span data-ttu-id="a160b-285">예제</span><span class="sxs-lookup"><span data-stu-id="a160b-285">EXAMPLE</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a160b-286">**주요 자격 증명 모음 URL**</span><span class="sxs-lookup"><span data-stu-id="a160b-286">**Key Vault URL**</span></span> |<span data-ttu-id="a160b-287">hello 위치 hello 주요 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-287">hello location of hello key vault.</span></span> |<span data-ttu-id="a160b-288">https://contosokeyvault.vault.azure.net/</span><span class="sxs-lookup"><span data-stu-id="a160b-288">https://contosokeyvault.vault.azure.net/</span></span> |
| <span data-ttu-id="a160b-289">**주체 이름**</span><span class="sxs-lookup"><span data-stu-id="a160b-289">**Principal name**</span></span> |<span data-ttu-id="a160b-290">Azure Active Directory 서비스 주체 이름.</span><span class="sxs-lookup"><span data-stu-id="a160b-290">Azure Active Directory service principal name.</span></span> <span data-ttu-id="a160b-291">이 이름은 이기도 하며 tooas hello 클라이언트 id입니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-291">This name is also referred tooas hello Client ID.</span></span> |<span data-ttu-id="a160b-292">fde2b411-33d5-4e11-af04eb07b669ccf2</span><span class="sxs-lookup"><span data-stu-id="a160b-292">fde2b411-33d5-4e11-af04eb07b669ccf2</span></span> |
| <span data-ttu-id="a160b-293">**주체 암호**</span><span class="sxs-lookup"><span data-stu-id="a160b-293">**Principal secret**</span></span> |<span data-ttu-id="a160b-294">Azure Active Directory 서비스 주체 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-294">Azure Active Directory service principal secret.</span></span> <span data-ttu-id="a160b-295">이 암호는 또한 참조 tooas hello 클라이언트 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-295">This secret is also referred tooas hello Client Secret.</span></span> |<span data-ttu-id="a160b-296">9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM=</span><span class="sxs-lookup"><span data-stu-id="a160b-296">9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM=</span></span> |
| <span data-ttu-id="a160b-297">**자격 증명 이름**</span><span class="sxs-lookup"><span data-stu-id="a160b-297">**Credential name**</span></span> |<span data-ttu-id="a160b-298">**자격 증명 이름**: AKV 통합 hello VM toohave 액세스 toohello 주요 자격 증명 모음을 허용 하는 SQL Server 내에서 자격 증명을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-298">**Credential name**: AKV Integration creates a credential within SQL Server, allowing hello VM toohave access toohello key vault.</span></span> <span data-ttu-id="a160b-299">이 자격 증명의 이름을 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="a160b-299">Choose a name for this credential.</span></span> |<span data-ttu-id="a160b-300">mycred1</span><span class="sxs-lookup"><span data-stu-id="a160b-300">mycred1</span></span> |

<span data-ttu-id="a160b-301">자세한 내용은 [Azure VM에서 SQL Server에 대한 Azure Key Vault 통합 구성](virtual-machines-windows-ps-sql-keyvault.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a160b-301">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs](virtual-machines-windows-ps-sql-keyvault.md).</span></span>

### <a name="r-services"></a><span data-ttu-id="a160b-302">R 서비스</span><span class="sxs-lookup"><span data-stu-id="a160b-302">R services</span></span>

<span data-ttu-id="a160b-303">Hello 옵션 tooenable 있는 [SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-303">You have hello option tooenable [SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx).</span></span> <span data-ttu-id="a160b-304">이렇게 하면 SQL Server 2016 toouse 고급 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-304">This enables you toouse advanced analytics with SQL Server 2016.</span></span> <span data-ttu-id="a160b-305">클릭 **사용** hello에 **SQL Server 설정** 창.</span><span class="sxs-lookup"><span data-stu-id="a160b-305">Click **Enable** on hello **SQL Server Settings** window.</span></span>

> [!NOTE]
> <span data-ttu-id="a160b-306">SQL Server 2016 Developer Edition에 대 한이 옵션은 hello 포털에서 하지 사용할 정확 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-306">For SQL Server 2016 Developer Edition, this option is incorrectly disabled by hello portal.</span></span> <span data-ttu-id="a160b-307">Developer 버전의 경우 VM을 생성한 후 R 서비스를 수동으로 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-307">For Developer edition, you must enable R Services manually after creating your VM.</span></span>

![SQL Server R 서비스 사용](./media/virtual-machines-windows-portal-sql-server-provision/azure-vm-sql-server-r-services.png)

<span data-ttu-id="a160b-309">SQL Server 설정 구성을 마치면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-309">When you are finished configuring SQL Server settings, click **OK**.</span></span>

## <a name="5-review-hello-summary"></a><span data-ttu-id="a160b-310">5. 요약 검토 hello</span><span class="sxs-lookup"><span data-stu-id="a160b-310">5. Review hello summary</span></span>

<span data-ttu-id="a160b-311">Hello에 **요약** 검토 요약 hello 창과 클릭 **구매** 이 VM에 대해 지정 된 SQL Server toocreate, 리소스 그룹 및 리소스.</span><span class="sxs-lookup"><span data-stu-id="a160b-311">On hello **Summary** window, review hello summary and click **Purchase** toocreate SQL Server, resource group, and resources specified for this VM.</span></span>

<span data-ttu-id="a160b-312">Hello Azure 포털에서에서 hello 배포를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-312">You can monitor hello deployment from hello Azure portal.</span></span> <span data-ttu-id="a160b-313">hello **알림** hello hello 화면 위쪽에 단추를 클릭 hello 배포의 기본 상태를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-313">hello **Notifications** button at hello top of hello screen shows basic status of hello deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="a160b-314">tooprovide 시간이 배포에 대해 예측 하기 SQL VM toohello 미국 동부 지역 기본 설정으로 배포 하려면.</span><span class="sxs-lookup"><span data-stu-id="a160b-314">tooprovide you with an idea on deployment times, I deployed a SQL VM toohello East US region with default settings.</span></span> <span data-ttu-id="a160b-315">이 테스트 배포 환경에서는 총 26 분 toocomplete의 걸렸습니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-315">This test deployment took a total of 26 minutes toocomplete.</span></span> <span data-ttu-id="a160b-316">사용자의 지역 및 선택한 설정에 따라서 배포 시간이 더 빠르거나 늦을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-316">But you might experience a faster or slower deployment time based on your region and selected settings.</span></span>

## <a name="open-hello-vm-with-remote-desktop"></a><span data-ttu-id="a160b-317">원격 데스크톱으로 hello VM을 열으십시오</span><span class="sxs-lookup"><span data-stu-id="a160b-317">Open hello VM with Remote Desktop</span></span>

<span data-ttu-id="a160b-318">다음 단계 tooconnect toohello SQL Server 가상 컴퓨터 원격 데스크톱을 사용 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-318">Use hello following steps tooconnect toohello SQL Server virtual machine with Remote Desktop:</span></span>

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

<span data-ttu-id="a160b-319">Toohello SQL Server 가상 컴퓨터를 연결한 후에 SQL Server Management Studio 실행 수 있으며 로컬 관리자 자격 증명을 사용 하 여 Windows 인증을 사용 하 여 연결 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-319">After you connect toohello SQL Server virtual machine, you can launch SQL Server Management Studio and connect with Windows Authentication using your local administrator credentials.</span></span> <span data-ttu-id="a160b-320">SQL Server 인증을 설정한 경우 SQL 인증 hello SQL 로그인 및 프로 비전 하는 동안 구성 된 암호를 사용 하 여 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-320">If you enabled SQL Server Authentication, you can also connect with SQL Authentication using hello SQL login and password you configured during provisioning.</span></span>

<span data-ttu-id="a160b-321">액세스 toohello 컴퓨터 toodirectly 변경 컴퓨터 및 요구 사항에 따라 SQL Server 설정을 사용 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-321">Access toohello machine enables you toodirectly change machine and SQL Server settings based on your requirements.</span></span> <span data-ttu-id="a160b-322">예를 들어 hello 방화벽 설정을 구성 하거나 SQL Server 구성 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-322">For example, you could configure hello firewall settings or change SQL Server configuration settings.</span></span>

## <a name="enable-tcpip-for-developer-and-express-editions"></a><span data-ttu-id="a160b-323">개발자 및 Express 버전에 대해 TCP/IP 사용</span><span class="sxs-lookup"><span data-stu-id="a160b-323">Enable TCP/IP for Developer and Express editions</span></span>

<span data-ttu-id="a160b-324">새 SQL Server VM을 프로 비전 할 때 Azure는 자동으로 사용 되지 hello TCP/IP 프로토콜 SQL Server Developer 및 Express 버전에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-324">When provisioning a new SQL Server VM, Azure does not automatically enable hello TCP/IP protocol for SQL Server Developer and Express editions.</span></span> <span data-ttu-id="a160b-325">다음 hello 단계 IP 주소를 통해 원격으로 연결할 수 있도록 toomanually TCP/IP를 설정 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-325">hello steps below explain how toomanually enable TCP/IP so that you can connect remotely by IP address.</span></span>

<span data-ttu-id="a160b-326">다음 단계 사용 하 여 hello **SQL Server 구성 관리자** SQL Server Developer 및 Express 버전에 대 한 tooenable hello TCP/IP 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-326">hello following steps use **SQL Server Configuration Manager** tooenable hello TCP/IP protocol for SQL Server Developer and Express editions.</span></span>

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-toosql-server-remotely"></a><span data-ttu-id="a160b-327">TooSQL 서버를 원격으로 연결</span><span class="sxs-lookup"><span data-stu-id="a160b-327">Connect tooSQL Server remotely</span></span>

<span data-ttu-id="a160b-328">이 자습서에서는 선택한 **공용** hello 가상 컴퓨터에 대 한 액세스 및 **SQL Server 인증**합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-328">In this tutorial, we selected **Public** access for hello virtual machine and **SQL Server Authentication**.</span></span> <span data-ttu-id="a160b-329">이러한 설정을 자동으로 구성 된 hello 가상 컴퓨터 tooallow SQL Server 연결을 통해 모든 클라이언트에서 hello 인터넷 (hello 올바른 SQL 로그인에 게 이러한 가정).</span><span class="sxs-lookup"><span data-stu-id="a160b-329">These settings automatically configured hello virtual machine tooallow SQL Server connections from any client over hello internet (assuming they have hello correct SQL login).</span></span>

> [!NOTE]
> <span data-ttu-id="a160b-330">프로 비전 중에 공용을 선택 하지 않은 hello 포털을 통해 SQL 연결 설정을 프로 비전 한 후 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-330">If you did not select Public during provisioning, then you can change your SQL connectivity settings through hello portal after provisioning.</span></span> <span data-ttu-id="a160b-331">자세한 내용은 [SQL 연결 설정 변경](virtual-machines-windows-sql-connect.md#change)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a160b-331">For more information, see  [Change your SQL connectivity settings](virtual-machines-windows-sql-connect.md#change).</span></span>

<span data-ttu-id="a160b-332">다음 섹션 hello tooconnect tooyour SQL Server 인스턴스를 통해 다른 컴퓨터에서 VM에 인터넷 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-332">hello following sections show how tooconnect tooyour SQL Server instance on your VM from a different computer over hello internet.</span></span>

> [!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="a160b-333">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a160b-333">Next Steps</span></span>

<span data-ttu-id="a160b-334">Azure에서 SQL Server를 사용 하는 방법에 대 한 기타 정보를 참조 하십시오. [Azure 가상 컴퓨터에 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md) 및 hello [질문과 대답](virtual-machines-windows-sql-server-iaas-faq.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a160b-334">For other information about using SQL Server in Azure, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md) and hello [Frequently Asked Questions](virtual-machines-windows-sql-server-iaas-faq.md).</span></span>
