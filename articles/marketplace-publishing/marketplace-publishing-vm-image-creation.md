---
title: "Azure Marketplace에 대한 가상 컴퓨터 이미지 만들기 | Microsoft Docs"
description: "Azure 마켓플레이스에서 다른 사용자가 구입할 수 있도록 가상 컴퓨터 이미지를 만드는 방법에 대한 자세한 지침입니다."
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 5c937b8e-e28d-4007-9fef-624046bca2ae
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 01/05/2017
ms.author: hascipio; v-divte
ms.openlocfilehash: 046ce7af40301014746c6aef07d08d81ab4adcc2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="guide-to-create-a-virtual-machine-image-for-the-azure-marketplace"></a><span data-ttu-id="c4e81-103">Azure 마켓플레이스에 대한 가상 컴퓨터 이미지 만들기 가이드</span><span class="sxs-lookup"><span data-stu-id="c4e81-103">Guide to create a virtual machine image for the Azure Marketplace</span></span>
<span data-ttu-id="c4e81-104">이 문서의 **2단계**에서는 Azure 마켓플레이스에 배포할 VHD(가상 하드 디스크)를 준비하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-104">This article, **Step 2**, walks you through preparing the virtual hard disks (VHDs) that you will deploy to the Azure Marketplace.</span></span> <span data-ttu-id="c4e81-105">VHD는 SKU의 기반입니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-105">Your VHDs are the foundation of your SKU.</span></span> <span data-ttu-id="c4e81-106">Linux 기반 SKU를 제공할지 Windows 기반 SKU를 제공할지 여부에 따라 프로세스는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-106">The process differs depending on whether you are providing a Linux-based or Windows-based SKU.</span></span> <span data-ttu-id="c4e81-107">이 문서에서는 두 시나리오를 모두 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-107">This article covers both scenarios.</span></span> <span data-ttu-id="c4e81-108">이 프로세스는 [계정 만들기 및 등록][link-acct-creation]과 함께 병렬로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-108">This process can be performed in parallel with [Account creation and registration][link-acct-creation].</span></span>

## <a name="1-define-offers-and-skus"></a><span data-ttu-id="c4e81-109">1. 제품 및 SKU 정의</span><span class="sxs-lookup"><span data-stu-id="c4e81-109">1. Define Offers and SKUs</span></span>
<span data-ttu-id="c4e81-110">이 섹션에서는 제품 및 관련 SKU 정의에 대해 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-110">In this section, you learn to define the offers and their associated SKUs.</span></span>

<span data-ttu-id="c4e81-111">제품은 모든 SKU의 "부모"입니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-111">An offer is a "parent" to all of its SKUs.</span></span> <span data-ttu-id="c4e81-112">제품을 여러 개 보유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-112">You can have multiple offers.</span></span> <span data-ttu-id="c4e81-113">제품을 구성하는 방법은 게시자가 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-113">How you decide to structure your offers is up to you.</span></span> <span data-ttu-id="c4e81-114">제품은 스테이징으로 푸시될 때 모든 SKU와 함께 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-114">When an offer is pushed to staging, it is pushed along with all of its SKUs.</span></span> <span data-ttu-id="c4e81-115">SKU 식별자는 URL에 표시되므로 신중하게 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="c4e81-115">Carefully consider your SKU identifiers, because they will be visible in the URL:</span></span>

* <span data-ttu-id="c4e81-116">Azure.com: http://azure.microsoft.com/marketplace/partners/{PartnerNamespace}/{OfferIdentifier}-{SKUidentifier}</span><span class="sxs-lookup"><span data-stu-id="c4e81-116">Azure.com: http://azure.microsoft.com/marketplace/partners/{PartnerNamespace}/{OfferIdentifier}-{SKUidentifier}</span></span>
* <span data-ttu-id="c4e81-117">Azure Preview 포털: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{SKUIDdentifier}</span><span class="sxs-lookup"><span data-stu-id="c4e81-117">Azure preview portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{SKUIDdentifier}</span></span>  

<span data-ttu-id="c4e81-118">SKU는 VM 이미지에 대한 상업용 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-118">A SKU is the commercial name for a VM image.</span></span> <span data-ttu-id="c4e81-119">VM 이미지에는 운영 체제 디스크 하나와 0개 이상의 데이터 디스크가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-119">A VM image contains one operating system disk and zero or more data disks.</span></span> <span data-ttu-id="c4e81-120">가상 컴퓨터에 대한 완벽한 저장소 프로필입니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-120">It is essentially the complete storage profile for a virtual machine.</span></span> <span data-ttu-id="c4e81-121">디스크당 VHD 하나가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-121">One VHD is needed per disk.</span></span> <span data-ttu-id="c4e81-122">데이터 디스크가 비어 있는 경우에도 VHD를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-122">Even blank data disks require a VHD to be created.</span></span>

<span data-ttu-id="c4e81-123">사용 중인 운영 체제에 상관없이 SKU에 필요한 최소 개수의 데이터 디스크만 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-123">Regardless of which operating system you use, add only the minimum number of data disks needed by the SKU.</span></span> <span data-ttu-id="c4e81-124">고객은 배포 시 이미지의 일부인 디스크를 제거할 수 없지만, 필요한 경우 배포 중이나 이후에 언제든지 디스크를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-124">Customers cannot remove disks that are part of an image at the time of deployment but can always add disks during or after deployment if they need them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c4e81-125">**새 이미지 버전에서 디스크 수를 변경하지 마세요.**</span><span class="sxs-lookup"><span data-stu-id="c4e81-125">**Do not change disk count in a new image version.**</span></span> <span data-ttu-id="c4e81-126">이미지에서 데이터 디스크를 다시 구성해야 하는 경우 새 SKU를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-126">If you must reconfigure Data disks in the image, define a new SKU.</span></span> <span data-ttu-id="c4e81-127">디스크 수가 다른 새 이미지 버전을 게시하면 자동 확장, ARM 템플릿을 통한 솔루션의 자동 배포 및 기타 시나리오에서 새 이미지 버전을 기반으로 새로운 배포를 포함할 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-127">Publishing a new image version with different disk counts will have the potential of breaking new deployment based on the new image version in cases of auto-scaling, automatic deployments of solutions through ARM templates and other scenarios.</span></span>
>
>

### <a name="11-add-an-offer"></a><span data-ttu-id="c4e81-128">1.1 제품 추가</span><span class="sxs-lookup"><span data-stu-id="c4e81-128">1.1 Add an offer</span></span>
1. <span data-ttu-id="c4e81-129">판매자 계정을 사용하여 [게시 포털][link-pubportal]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-129">Sign in to the [Publishing Portal][link-pubportal] by using your seller account.</span></span>
2. <span data-ttu-id="c4e81-130">게시 포털의 **가상 컴퓨터** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-130">Select the **Virtual Machines** tab of the Publishing Portal.</span></span> <span data-ttu-id="c4e81-131">표시된 입력 필드에 제품 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-131">In the prompted entry field, enter your offer name.</span></span> <span data-ttu-id="c4e81-132">제품 이름은 일반적으로 Azure 마켓플레이스에 판매할 계획인 제품 또는 서비스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-132">The offer name is typically the name of the product or service that you plan to sell in the Azure Marketplace.</span></span>
3. <span data-ttu-id="c4e81-133">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-133">Select **Create**.</span></span>

### <a name="12-define-a-sku"></a><span data-ttu-id="c4e81-134">1.2 SKU 정의</span><span class="sxs-lookup"><span data-stu-id="c4e81-134">1.2 Define a SKU</span></span>
<span data-ttu-id="c4e81-135">제품을 추가한 후 SKU를 정의 및 식별해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-135">After you have added an offer, you need to define and identify your SKUs.</span></span> <span data-ttu-id="c4e81-136">게시자는 제품을 여러 개 보유할 수 있으며 각 제품에는 그 아래 여러 개의 SKU를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-136">You can have multiple offers, and each offer can have multiple SKUs under it.</span></span> <span data-ttu-id="c4e81-137">제품은 스테이징으로 푸시될 때 모든 SKU와 함께 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-137">When an offer is pushed to staging, it is pushed along with all of its SKUs.</span></span>

1. <span data-ttu-id="c4e81-138">**SKU를 추가합니다.**</span><span class="sxs-lookup"><span data-stu-id="c4e81-138">**Add a SKU.**</span></span> <span data-ttu-id="c4e81-139">SKU는 URL에 사용되는 식별자가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-139">The SKU requires an identifier, which is used in the URL.</span></span> <span data-ttu-id="c4e81-140">이 식별자는 게시 프로필 내에서 공유해야 하지만, 식별자가 다른 게시자와 충돌할 위험은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-140">The identifier must be unique within your publishing profile, but there is no risk of identifier collision with other publishers.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c4e81-141">제품 및 SKU 식별자는 마켓플레이스의 제품 URL에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-141">The offer and SKU identifiers are displayed in the offer URL in the Marketplace.</span></span>
   >
   >
2. <span data-ttu-id="c4e81-142">**SKU에 대한 요약 설명을 추가합니다.**</span><span class="sxs-lookup"><span data-stu-id="c4e81-142">**Add a summary description for your SKU.**</span></span> <span data-ttu-id="c4e81-143">요약 설명은 고객에게 표시되므로 이해하기 쉽도록 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-143">Summary descriptions are visible to customers, so you should make them easily readable.</span></span> <span data-ttu-id="c4e81-144">이 정보는 "스테이징으로 푸시" 단계까지 잠글 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-144">This information does not need to be locked until the "Push to Staging" phase.</span></span> <span data-ttu-id="c4e81-145">그때까지 자유롭게 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-145">Until then, you are free to edit it.</span></span>
3. <span data-ttu-id="c4e81-146">Windows 기반 SKU를 사용할 경우 제안된 링크를 따라 Windows Server의 승인된 버전을 습득하세요.</span><span class="sxs-lookup"><span data-stu-id="c4e81-146">If you are using Windows-based SKUs, follow the suggested links to acquire the approved versions of Windows Server.</span></span>

## <a name="2-create-an-azure-compatible-vhd-linux-based"></a><span data-ttu-id="c4e81-147">2. Azure 호환 VHD 만들기(Linux 기반)</span><span class="sxs-lookup"><span data-stu-id="c4e81-147">2. Create an Azure-compatible VHD (Linux-based)</span></span>
<span data-ttu-id="c4e81-148">이 섹션에서는 Azure 마켓플레이스에 대한 Linux 기반 VM 이미지를 만드는 모범 사례를 중심으로 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-148">This section focuses on best practices for creating a Linux-based VM image for the Azure Marketplace.</span></span> <span data-ttu-id="c4e81-149">단계별 연습은 [Linux 운영 체제가 포함된 가상 하드 디스크 만들기 및 업로드](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4e81-149">For a step-by-step walkthrough, refer to the following documentation: [Creating and Uploading a Virtual Hard Disk that Contains the Linux Operating System](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

## <a name="3-create-an-azure-compatible-vhd-windows-based"></a><span data-ttu-id="c4e81-150">3. Azure 호환 VHD 만들기(Windows 기반)</span><span class="sxs-lookup"><span data-stu-id="c4e81-150">3. Create an Azure-compatible VHD (Windows-based)</span></span>
<span data-ttu-id="c4e81-151">이 섹션에서는 Azure 마켓플레이스에 대해 Windows Server 기반 SKU를 만드는 단계를 중심으로 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-151">This section focuses on the steps to create a SKU based on Windows Server for the Azure Marketplace.</span></span>

### <a name="31-ensure-that-you-are-using-the-correct-base-vhds"></a><span data-ttu-id="c4e81-152">3.1 올바른 기본 VHD를 사용 중인지 확인</span><span class="sxs-lookup"><span data-stu-id="c4e81-152">3.1 Ensure that you are using the correct base VHDs</span></span>
<span data-ttu-id="c4e81-153">VM 이미지용 운영 체제 VHD는 Windows Server 또는 SQL Server를 포함하는 Azure 승인 기본 이미지를 기반으로 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-153">The operating system VHD for your VM image must be based on an Azure-approved base image that contains Windows Server or SQL Server.</span></span>

<span data-ttu-id="c4e81-154">시작하려면 [Microsoft Azure Portal][link-azure-portal]에 있는 다음 이미지 중 하나에서 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-154">To begin, create a VM from one of the following images, located at the [Microsoft Azure portal][link-azure-portal]:</span></span>

* <span data-ttu-id="c4e81-155">Windows Server([2012 R2 Datacenter][link-datactr-2012-r2], [2012 Datacenter][link-datactr-2012], [2008 R2 SP1][link-datactr-2008-r2])</span><span class="sxs-lookup"><span data-stu-id="c4e81-155">Windows Server ([2012 R2 Datacenter][link-datactr-2012-r2], [2012 Datacenter][link-datactr-2012], [2008 R2 SP1][link-datactr-2008-r2])</span></span>
* <span data-ttu-id="c4e81-156">SQL Server 2014 ([Enterprise][link-sql-2014-ent], [Standard][link-sql-2014-std], [Web][link-sql-2014-web])</span><span class="sxs-lookup"><span data-stu-id="c4e81-156">SQL Server 2014 ([Enterprise][link-sql-2014-ent], [Standard][link-sql-2014-std], [Web][link-sql-2014-web])</span></span>
* <span data-ttu-id="c4e81-157">SQL Server 2012 SP2 ([Enterprise][link-sql-2012-ent], [Standard][link-sql-2012-std], [Web][link-sql-2012-web])</span><span class="sxs-lookup"><span data-stu-id="c4e81-157">SQL Server 2012 SP2 ([Enterprise][link-sql-2012-ent], [Standard][link-sql-2012-std], [Web][link-sql-2012-web])</span></span>

<span data-ttu-id="c4e81-158">이러한 링크는 게시 포털의 SKU 페이지 아래에도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-158">These links can also be found in the Publishing Portal under the SKU page.</span></span>

> [!TIP]
> <span data-ttu-id="c4e81-159">최신 Azure 포털 또는 PowerShell을 사용 중인 경우 2014년 9월 8일 이후에 게시된 Windows Server 이미지가 승인됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-159">If you are using the current Azure portal or PowerShell, Windows Server images published on September 8, 2014 and later are approved.</span></span>
>
>

### <a name="32-create-your-windows-based-vm"></a><span data-ttu-id="c4e81-160">3.2 Windows 기반 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="c4e81-160">3.2 Create your Windows-based VM</span></span>
<span data-ttu-id="c4e81-161">Microsoft Azure 포털에서 승인된 기본 이미지를 기반으로 VM을 간단히 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-161">From the Microsoft Azure portal, you can create your VM based on an approved base image in just a few simple steps.</span></span> <span data-ttu-id="c4e81-162">프로세스 개요는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-162">The following is an overview of the process:</span></span>

1. <span data-ttu-id="c4e81-163">기본 이미지 페이지에서 **가상 컴퓨터 만들기**를 선택합니다. 그러면 새 [Microsoft Azure Portal][link-azure-portal]로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-163">From the base image page, select **Create Virtual Machine** to be directed to the new [Microsoft Azure portal][link-azure-portal].</span></span>

    ![그리기][img-acom-1]
2. <span data-ttu-id="c4e81-165">사용할 Azure 구독에 대한 Microsoft 계정 및 암호를 사용하여 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-165">Sign in to the portal with the Microsoft account and password for the Azure subscription you want to use.</span></span>
3. <span data-ttu-id="c4e81-166">프롬프트에 따라 선택한 기본 이미지를 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-166">Follow the prompts to create a VM by using the base image you have selected.</span></span> <span data-ttu-id="c4e81-167">VM에 대한 호스트 이름(컴퓨터 이름), 사용자 이름(관리자로 등록됨) 및 암호를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-167">You need to provide a host name (name of the computer), user name (registered as an administrator), and password for the VM.</span></span>

    ![drawing][img-portal-vm-create]
4. <span data-ttu-id="c4e81-169">배포할 VM의 크기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-169">Select the size of the VM to deploy:</span></span>

    <span data-ttu-id="c4e81-170">a.</span><span class="sxs-lookup"><span data-stu-id="c4e81-170">a.</span></span>    <span data-ttu-id="c4e81-171">온-프레미스에서 VHD를 개발하려는 경우 크기는 중요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-171">If you plan to develop the VHD on-premises, the size does not matter.</span></span> <span data-ttu-id="c4e81-172">더 작은 VM 중 하나를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-172">Consider using one of the smaller VMs.</span></span>

    <span data-ttu-id="c4e81-173">b.</span><span class="sxs-lookup"><span data-stu-id="c4e81-173">b.</span></span>    <span data-ttu-id="c4e81-174">Azure에서 이미지를 개발하려는 경우 선택된 이미지에 대한 권장 VM 크기 중 하나를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-174">If you plan to develop the image in Azure, consider using one of the recommended VM sizes for the selected image.</span></span>

    <span data-ttu-id="c4e81-175">c.</span><span class="sxs-lookup"><span data-stu-id="c4e81-175">c.</span></span>    <span data-ttu-id="c4e81-176">가격 책정에 대한 자세한 내용은 포털에 표시되는 **권장 가격 책정 계층** 선택기를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4e81-176">For pricing information, refer to the **Recommended pricing tiers** selector displayed on the portal.</span></span> <span data-ttu-id="c4e81-177">게시자가 제공한 세 개의 권장 크기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-177">It will provide the three recommended sizes provided by the publisher.</span></span> <span data-ttu-id="c4e81-178">이 경우 게시자는 Microsoft입니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-178">(In this case, the publisher is Microsoft.)</span></span>

    ![drawing][img-portal-vm-size]
5. <span data-ttu-id="c4e81-180">속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-180">Set properties:</span></span>

    <span data-ttu-id="c4e81-181">a.</span><span class="sxs-lookup"><span data-stu-id="c4e81-181">a.</span></span>    <span data-ttu-id="c4e81-182">빠른 배포를 위해 **선택적 구성** 및 **리소스 그룹**에서 속성에 대한 기본값을 그대로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-182">For quick deployment, you can leave the default values for the properties under **Optional Configuration** and **Resource Group**.</span></span>

    <span data-ttu-id="c4e81-183">b.</span><span class="sxs-lookup"><span data-stu-id="c4e81-183">b.</span></span>    <span data-ttu-id="c4e81-184">필요에 따라 **저장소 계정**에서 운영 체제 VHD를 저장할 저장소 계정을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-184">Under **Storage Account**, you can optionally select the storage account in which the operating system VHD will be stored.</span></span>

    <span data-ttu-id="c4e81-185">c.</span><span class="sxs-lookup"><span data-stu-id="c4e81-185">c.</span></span>    <span data-ttu-id="c4e81-186">필요에 따라 **리소스 그룹**에서 VM을 배치할 논리 그룹을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-186">Under **Resource Group**, you can optionally select the logical group in which to place the VM.</span></span>
6. <span data-ttu-id="c4e81-187">배포를 위한 **위치** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-187">Select the **Location** for deployment:</span></span>

    <span data-ttu-id="c4e81-188">a.</span><span class="sxs-lookup"><span data-stu-id="c4e81-188">a.</span></span>    <span data-ttu-id="c4e81-189">온-프레미스에서 VHD를 개발하려면 나중에 이미지를 Azure에 업로드할 것이므로 위치는 중요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-189">If you plan to develop the VHD on-premises, the location does not matter because you will upload the image to Azure later.</span></span>

    <span data-ttu-id="c4e81-190">b.</span><span class="sxs-lookup"><span data-stu-id="c4e81-190">b.</span></span>    <span data-ttu-id="c4e81-191">Azure에서 이미지를 개발하려면 처음부터 미국 기반 Microsoft Azure 지역 중 하나를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-191">If you plan to develop the image in Azure, consider using one of the US-based Microsoft Azure regions from the beginning.</span></span> <span data-ttu-id="c4e81-192">그러면 개발자가 인증을 위해 이미지를 제출할 때 Microsoft에서 자동으로 수행되는 VHD 복사 프로세스가 단축됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-192">This speeds up the VHD copying process that Microsoft performs on your behalf when you submit your image for certification.</span></span>

    ![drawing][img-portal-vm-location]
7. <span data-ttu-id="c4e81-194">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-194">Click **Create**.</span></span> <span data-ttu-id="c4e81-195">VM 배포를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-195">The VM starts to deploy.</span></span> <span data-ttu-id="c4e81-196">몇 분 이내에 배포되고 SKU에 대한 이미지 만들기를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-196">Within minutes, you will have a successful deployment and can begin to create the image for your SKU.</span></span>

### <a name="33-develop-your-vhd-in-the-cloud"></a><span data-ttu-id="c4e81-197">3.3 클라우드에서 VHD 개발</span><span class="sxs-lookup"><span data-stu-id="c4e81-197">3.3 Develop your VHD in the cloud</span></span>
<span data-ttu-id="c4e81-198">RDP(원격 데스크톱 프로토콜)를 사용하여 클라우드에서 VHD를 개발하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-198">We strongly recommend that you develop your VHD in the cloud by using Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="c4e81-199">프로비전 중에 지정한 사용자 이름과 암호를 사용하여 RDP에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-199">You connect to RDP with the user name and password specified during provisioning.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c4e81-200">온-프레미스에서 VHD를 개발하는 경우(권장되지 않음) [온-프레미스에 가상 컴퓨터 이미지 만들기](marketplace-publishing-vm-image-creation-on-premise.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4e81-200">If you develop your VHD on-premises (which is not recommended), see [Creating a virtual machine image on-premises](marketplace-publishing-vm-image-creation-on-premise.md).</span></span> <span data-ttu-id="c4e81-201">클라우드에서 개발 중인 경우에는 VHD를 다운로드할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-201">Downloading your VHD is not necessary if you are developing in the cloud.</span></span>
>
>

<span data-ttu-id="c4e81-202">**[Microsoft Azure Portal][link-azure-portal]**을 사용하여 RDP를 통해 연결</span><span class="sxs-lookup"><span data-stu-id="c4e81-202">**Connect via RDP using the [Microsoft Azure portal][link-azure-portal]**</span></span>

1. <span data-ttu-id="c4e81-203">**찾아보기** > **VM**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-203">Select **Browse** > **VMs**.</span></span>
2. <span data-ttu-id="c4e81-204">가상 컴퓨터 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-204">The Virtual machines blade opens.</span></span> <span data-ttu-id="c4e81-205">연결하려는 VM이 실행 중인지 확인하고 배포된 VM 목록에서 해당 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-205">Ensure that the VM that you want to connect with is running, and then select it from the list of deployed VMs.</span></span>
3. <span data-ttu-id="c4e81-206">선택된 VM을 설명하는 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-206">A blade opens that describes the selected VM.</span></span> <span data-ttu-id="c4e81-207">맨 위에 있는 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-207">At the top, click **Connect**.</span></span>
4. <span data-ttu-id="c4e81-208">프로비전 중에 지정한 사용자 이름과 암호를 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-208">You are prompted to enter the user name and password that you specified during provisioning.</span></span>

<span data-ttu-id="c4e81-209">**PowerShell을 사용하여 RDP를 통해 연결**</span><span class="sxs-lookup"><span data-stu-id="c4e81-209">**Connect via RDP using PowerShell**</span></span>

<span data-ttu-id="c4e81-210">원격 데스크톱 파일을 로컬 컴퓨터에 다운로드하려면 [Get-AzureRemoteDesktopFile cmdlet][link-technet-2]을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-210">To download a remote desktop file to a local machine, use the [Get-AzureRemoteDesktopFile cmdlet][link-technet-2].</span></span> <span data-ttu-id="c4e81-211">이 cmdlet을 사용하려면 서비스 이름과 VM 이름을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-211">In order to use this cmdlet, you need to know the name of the service and name of the VM.</span></span> <span data-ttu-id="c4e81-212">[Microsoft Azure Portal][link-azure-portal]에서 VM을 만든 경우 VM 속성에서 이 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-212">If you created the VM from the [Microsoft Azure portal][link-azure-portal], you can find this information under VM properties:</span></span>

1. <span data-ttu-id="c4e81-213">Microsoft Azure Portal에서 **찾아보기** > **VM**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-213">In the Microsoft Azure portal, select **Browse** > **VMs**.</span></span>
2. <span data-ttu-id="c4e81-214">가상 컴퓨터 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-214">The Virtual machines blade opens.</span></span> <span data-ttu-id="c4e81-215">배포된 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-215">Select the VM that you deployed.</span></span>
3. <span data-ttu-id="c4e81-216">선택된 VM을 설명하는 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-216">A blade opens that describes the selected VM.</span></span>
4. <span data-ttu-id="c4e81-217">**속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-217">Click **Properties**.</span></span>
5. <span data-ttu-id="c4e81-218">도메인 이름의 첫 부분은 서비스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-218">The first portion of the domain name is the service name.</span></span> <span data-ttu-id="c4e81-219">호스트 이름은 VM 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-219">The host name is the VM name.</span></span>

    ![drawing][img-portal-vm-rdp]
6. <span data-ttu-id="c4e81-221">만든 VM에 대한 RDP 파일을 관리자의 로컬 데스크톱으로 다운로드하기 위한 cmdlet은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-221">The cmdlet to download the RDP file for the created VM to the administrator's local desktop is as follows.</span></span>

        Get‐AzureRemoteDesktopFile ‐ServiceName “baseimagevm‐6820cq00” ‐Name “BaseImageVM” –LocalPath “C:\Users\Administrator\Desktop\BaseImageVM.rdp”

<span data-ttu-id="c4e81-222">RDP에 대한 자세한 내용은 MSDN의 [RDP 또는 SSH를 사용하여 Azure VM에 연결](http://msdn.microsoft.com/library/azure/dn535788.aspx)(영문) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4e81-222">More information about RDP can be found on MSDN in the article [Connect to an Azure VM with RDP or SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx).</span></span>

<span data-ttu-id="c4e81-223">**VM 구성 및 SKU 만들기**</span><span class="sxs-lookup"><span data-stu-id="c4e81-223">**Configure a VM and create your SKU**</span></span>

<span data-ttu-id="c4e81-224">운영 체제 VHD를 다운로드한 후 Hyper­V를 사용하고 SKU 만들기를 시작하도록 VM을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-224">After the operating system VHD is downloaded, use Hyper­V and configure a VM to begin creating your SKU.</span></span> <span data-ttu-id="c4e81-225">세부 단계는 TechNet에서 [Hyper­V 설치 및 VM 구성](http://technet.microsoft.com/library/hh846766.aspx)링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4e81-225">Detailed steps can be found at the following TechNet link: [Install Hyper­V and Configure a VM](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="34-choose-the-correct-vhd-size"></a><span data-ttu-id="c4e81-226">3.4 올바른 VHD 크기 선택</span><span class="sxs-lookup"><span data-stu-id="c4e81-226">3.4 Choose the correct VHD size</span></span>
<span data-ttu-id="c4e81-227">VM 이미지의 Windows 운영 체제 VHD는 128GB 고정 형식 VHD로 만들어져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-227">The Windows operating system VHD in your VM image should be created as a 128-GB fixed-format VHD.</span></span>  

<span data-ttu-id="c4e81-228">물리적 크기가 128GB보다 작은 경우 VHD가 스파스여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-228">If the physical size is less than 128 GB, the VHD should be sparse.</span></span> <span data-ttu-id="c4e81-229">이미 제공된 기본 Windows 및 SQL Server 이미지는 이러한 요구 사항을 충족해야 하므로 가져온 VHD의 형식 또는 크기를 변경하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="c4e81-229">The base Windows and SQL Server images provided already meet these requirements, so do not change the format or the size of the VHD obtained.</span></span>  

<span data-ttu-id="c4e81-230">데이터 디스크는 1TB이하여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-230">Data disks can be as large as 1 TB.</span></span> <span data-ttu-id="c4e81-231">디스크 크기를 결정할 때 고객이 배포 시에 이미지 내에서 VHD 크기를 조정할 수 없음에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="c4e81-231">When deciding on the disk size, remember that customers cannot resize VHDs within an image at the time of deployment.</span></span> <span data-ttu-id="c4e81-232">데이터 디스크 VHD는 고정 형식 VHD로 작성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-232">Data disk VHDs should be created as a fixed-format VHD.</span></span> <span data-ttu-id="c4e81-233">또한 스파스여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-233">They should also be sparse.</span></span> <span data-ttu-id="c4e81-234">데이터 디스크는 비어 있거나 데이터를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-234">Data disks can be empty or contain data.</span></span>

### <a name="35-install-the-latest-windows-patches"></a><span data-ttu-id="c4e81-235">3.5 최신 Windows 패치 설치</span><span class="sxs-lookup"><span data-stu-id="c4e81-235">3.5 Install the latest Windows patches</span></span>
<span data-ttu-id="c4e81-236">기본 이미지에는 게시된 날짜까지의 최신 패치가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-236">The base images contain the latest patches up to their published date.</span></span> <span data-ttu-id="c4e81-237">만든 운영 체제 VHD를 게시하기 전에 Windows 업데이트가 실행되었고 모든 최신의 필수 및 중요 보안 패치를 설치했는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="c4e81-237">Before publishing the operating system VHD you have created, ensure that Windows Update has been run and that all the latest Critical and Important security updates have been installed.</span></span>

### <a name="36-perform-additional-configuration-and-schedule-tasks-as-necessary"></a><span data-ttu-id="c4e81-238">3.6 필요 시 추가 구성 수행 및 작업 예약</span><span class="sxs-lookup"><span data-stu-id="c4e81-238">3.6 Perform additional configuration and schedule tasks as necessary</span></span>
<span data-ttu-id="c4e81-239">추가 구성이 필요한 경우 시작 시 실행하도록 예약된 작업을 사용하여 배포된 VM을 최종적으로 변경하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-239">If additional configuration is needed, consider using a scheduled task that runs at startup to make any final changes to the VM after it has been deployed:</span></span>

* <span data-ttu-id="c4e81-240">작업이 성공적으로 실행된 후 해당 작업을 자동으로 삭제하는 것이 모범 사례입니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-240">It is a best practice to have the task delete itself upon successful execution.</span></span>
* <span data-ttu-id="c4e81-241">C 또는 D 드라이브는 항상 존재하므로 반드시 이 두 드라이브 중 하나를 사용하도록 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-241">No configuration should rely on drives other than drives C or D, because these are the only two drives that are always guaranteed to exist.</span></span> <span data-ttu-id="c4e81-242">C 드라이브는 운영 체제 디스크이고 D 드라이브는 임시 로컬 디스크입니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-242">Drive C is the operating system disk, and drive D is the temporary local disk.</span></span>

### <a name="37-generalize-the-image"></a><span data-ttu-id="c4e81-243">3.7 이미지 일반화</span><span class="sxs-lookup"><span data-stu-id="c4e81-243">3.7 Generalize the image</span></span>
<span data-ttu-id="c4e81-244">Azure 마켓플레이스의 모든 이미지는 일반적으로 다시 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-244">All images in the Azure Marketplace must be reusable in a generic fashion.</span></span> <span data-ttu-id="c4e81-245">즉, 운영 체제 VHD를 일반화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-245">In other words, the operating system VHD must be generalized:</span></span>

* <span data-ttu-id="c4e81-246">Windows의 경우 이미지에 "sysprep"을 실행해야 하므로 **sysprep** 명령을 지원하지 않도록 구성해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-246">For Windows, the image should be "sysprepped," and no configurations should be done that do not support the **sysprep** command.</span></span>
* <span data-ttu-id="c4e81-247">%windir%\System32\Sysprep 디렉터리에서 다음 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-247">You can run the following command from the directory %windir%\System32\Sysprep.</span></span>

        sysprep.exe /generalize /oobe /shutdown

  <span data-ttu-id="c4e81-248">운영 체제에 sysprep를 실행하는 방법은 MSDN 문서, [Windows Server VHD를 만들어서 Azure에 업로드](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)의 단계를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4e81-248">Guidance on how to sysprep the operating system is provided in Step of the following MSDN article: [Create and upload a Windows Server VHD to Azure](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="4-deploy-a-vm-from-your-vhds"></a><span data-ttu-id="c4e81-249">4. VHD에서 VM 배포</span><span class="sxs-lookup"><span data-stu-id="c4e81-249">4. Deploy a VM from your VHDs</span></span>
<span data-ttu-id="c4e81-250">VHD(일반화된 운영 체제 VHD 및 0개 이상의 데이터 디스크 VHD)가 Azure 저장소 계정에 업로드된 후에는 사용자 VM 이미지로 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-250">After you have uploaded your VHDs (the generalized operating system VHD and zero or more data disk VHDs) to an Azure storage account, you can register them as a user VM image.</span></span> <span data-ttu-id="c4e81-251">그런 다음 해당 이미지를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-251">Then you can test that image.</span></span> <span data-ttu-id="c4e81-252">운영 체제 VHD는 일반화되므로 VHD URL을 제공하여 VM을 직접 배포할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-252">Note that because your operating system VHD is generalized, you cannot directly deploy the VM by providing the VHD URL.</span></span>

<span data-ttu-id="c4e81-253">VM 이미지에 대해 자세히 알아보려면 다음 블로그 게시물을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4e81-253">To learn more about VM images, review the following blog posts:</span></span>

* [<span data-ttu-id="c4e81-254">VM 이미지</span><span class="sxs-lookup"><span data-stu-id="c4e81-254">VM Image</span></span>](https://azure.microsoft.com/blog/vm-image-blog-post/)
* [<span data-ttu-id="c4e81-255">VM 이미지 PowerShell 방법</span><span class="sxs-lookup"><span data-stu-id="c4e81-255">VM Image PowerShell How To</span></span>](https://azure.microsoft.com/blog/vm-image-powershell-how-to-blog-post/)
* [<span data-ttu-id="c4e81-256">Azure에서 VM 이미지 정보</span><span class="sxs-lookup"><span data-stu-id="c4e81-256">About VM images in Azure</span></span>](https://msdn.microsoft.com/library/azure/dn790290.aspx)

### <a name="set-up-the-necessary-tools-powershell-and-azure-cli"></a><span data-ttu-id="c4e81-257">필요한 도구, PowerShell 및 Azure CLI 설정</span><span class="sxs-lookup"><span data-stu-id="c4e81-257">Set up the necessary tools, PowerShell and Azure CLI</span></span>
* [<span data-ttu-id="c4e81-258">PowerShell을 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="c4e81-258">How to setup PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="c4e81-259">Azure CLI를 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="c4e81-259">How to setup Azure CLI</span></span>](../cli-install-nodejs.md)

### <a name="41-create-a-user-vm-image"></a><span data-ttu-id="c4e81-260">4.1 사용자 VM 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="c4e81-260">4.1 Create a user VM image</span></span>
#### <a name="capture-vm"></a><span data-ttu-id="c4e81-261">VM 캡처</span><span class="sxs-lookup"><span data-stu-id="c4e81-261">Capture VM</span></span>
<span data-ttu-id="c4e81-262">API/PowerShell/Azure CLI를 사용하여 VM을 캡처하는 방법에 대한 지침은 아래 제공된 링크를 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="c4e81-262">Please read the links given below for guidance on capturing the VM using API/PowerShell/Azure CLI.</span></span>

* [<span data-ttu-id="c4e81-263">API</span><span class="sxs-lookup"><span data-stu-id="c4e81-263">API</span></span>](https://msdn.microsoft.com/library/mt163560.aspx)
* [<span data-ttu-id="c4e81-264">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4e81-264">PowerShell</span></span>](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="c4e81-265">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c4e81-265">Azure CLI</span></span>](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="generalize-image"></a><span data-ttu-id="c4e81-266">이미지 일반화</span><span class="sxs-lookup"><span data-stu-id="c4e81-266">Generalize Image</span></span>
<span data-ttu-id="c4e81-267">API/PowerShell/Azure CLI를 사용하여 VM을 캡처하는 방법에 대한 지침은 아래 제공된 링크를 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="c4e81-267">Please read the links given below for guidance on capturing the VM using API/PowerShell/Azure CLI.</span></span>

* [<span data-ttu-id="c4e81-268">API</span><span class="sxs-lookup"><span data-stu-id="c4e81-268">API</span></span>](https://msdn.microsoft.com/library/mt269439.aspx)
* [<span data-ttu-id="c4e81-269">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4e81-269">PowerShell</span></span>](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="c4e81-270">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c4e81-270">Azure CLI</span></span>](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="42-deploy-a-vm-from-a-user-vm-image"></a><span data-ttu-id="c4e81-271">4.2 사용자 VM 이미지에서 VM 배포</span><span class="sxs-lookup"><span data-stu-id="c4e81-271">4.2 Deploy a VM from a user VM image</span></span>
<span data-ttu-id="c4e81-272">사용자 VM 이미지에서 VM을 배포하려면 최신 [Azure 포털](https://manage.windowsazure.com) 또는 PowerShell을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-272">To deploy a VM from a user VM image, you can use the current [Azure portal](https://manage.windowsazure.com) or PowerShell.</span></span>

<span data-ttu-id="c4e81-273">**최신 Azure 포털에서 VM 배포**</span><span class="sxs-lookup"><span data-stu-id="c4e81-273">**Deploy a VM from the current Azure portal**</span></span>

1. <span data-ttu-id="c4e81-274">**새로 만들기** > **계산** > **가상 컴퓨터** > **갤러리에서**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-274">Go to **New** > **Compute** > **Virtual machine** > **From gallery**.</span></span>

    ![drawing][img-manage-vm-new]
2. <span data-ttu-id="c4e81-276">**내 이미지**로 이동한 다음 VM을 배포할 VM 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-276">Go to **My images**, and then select the VM image from which to deploy a VM:</span></span>

   1. <span data-ttu-id="c4e81-277">**내 이미지** 보기에는 운영 체제 이미지와 VM 이미지가 모두 나열되므로 선택한 이미지에 주의하세요.</span><span class="sxs-lookup"><span data-stu-id="c4e81-277">Pay close attention to which image you select, because the **My images** view lists both operating system images and VM images.</span></span>
   2. <span data-ttu-id="c4e81-278">VM 이미지의 대부분은 디스크가 두 개 이상이므로 디스크 수를 조사하면 배포 중인 이미지의 형식을 결정하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-278">Looking at the number of disks can help determine what type of image you are deploying, because the majority of VM images have more than one disk.</span></span> <span data-ttu-id="c4e81-279">하지만 VM 이미지 중에도 운영 체제 디스크가 하나만 존재하여 **디스크 수** 가 1로 설정되는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-279">However, it is still possible to have a VM image with only a single operating system disk, which would then have **Number of disks** set to 1.</span></span>

      ![drawing][img-manage-vm-select]
3. <span data-ttu-id="c4e81-281">VM 만들기 마법사를 따라 VM 이름, VM 크기, 위치, 사용자 이름 및 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-281">Follow the VM creation wizard and specify the VM name, VM size, location, user name, and password.</span></span>

<span data-ttu-id="c4e81-282">**PowerShell에서 VM 배포**</span><span class="sxs-lookup"><span data-stu-id="c4e81-282">**Deploy a VM from PowerShell**</span></span>

<span data-ttu-id="c4e81-283">대형 VM을 배포하려면 방금 만든 일반화된 VM 이미지에서 다음 cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-283">To deploy a large VM from the generalized VM image just created, you can use the following cmdlets.</span></span>

    $img = Get-AzureVMImage -ImageName "myVMImage"
    $user = "user123"
    $pass = "adminPassword123"
    $myVM = New-AzureVMConfig -Name "VMImageVM" -InstanceSize "Large" -ImageName $img.ImageName | Add-AzureProvisioningConfig -Windows -AdminUsername $user -Password $pass
    New-AzureVM -ServiceName "VMImageCloudService" -VMs $myVM -Location "West US" -WaitForBoot

> [!IMPORTANT]
> <span data-ttu-id="c4e81-284">추가적인 도움이 필요하면 [VHD를 만드는 동안 발생하는 일반적인 문제 해결]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4e81-284">Please refer [Troubleshooting common issues encountered during VHD creation] for additional assistance.</span></span>
>
>

## <a name="5-obtain-certification-for-your-vm-image"></a><span data-ttu-id="c4e81-285">5. VM 이미지에 대한 인증받기</span><span class="sxs-lookup"><span data-stu-id="c4e81-285">5. Obtain certification for your VM image</span></span>
<span data-ttu-id="c4e81-286">Azure 마켓플레이스에 대한 VM 이미지 준비 과정의 다음 단계는 인증받기입니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-286">The next step in preparing your VM image for the Azure Marketplace is to have it certified.</span></span>

<span data-ttu-id="c4e81-287">이 프로세스는 특수 인증 도구 실행, VHD가 있는 Azure 컨테이너에 확인 결과 업로드, 제품 추가, SKU 정의, 인증을 위해 VM 이미지 제출 등으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-287">This process includes running a special certification tool, uploading the verification results to the Azure container where your VHDs reside, adding an offer, defining your SKU, and submitting your VM image for certification.</span></span>

### <a name="51-download-and-run-the-certification-test-tool-for-azure-certified"></a><span data-ttu-id="c4e81-288">5.1 Azure Certified용 인증 테스트 도구 다운로드 및 실행</span><span class="sxs-lookup"><span data-stu-id="c4e81-288">5.1 Download and run the Certification Test Tool for Azure Certified</span></span>
<span data-ttu-id="c4e81-289">인증 도구는 사용자 VM 이미지에서 프로비전된 실행 중인 VM에 대해 실행되어 VM 이미지가 Microsoft Azure와 호환되는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-289">The certification tool runs on a running VM, provisioned from your user VM image, to ensure that the VM image is compatible with Microsoft Azure.</span></span> <span data-ttu-id="c4e81-290">VHD 준비에 대한 지침과 요구 사항이 충족되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-290">It will verify that the guidance and requirements about preparing your VHD have been met.</span></span> <span data-ttu-id="c4e81-291">이 도구의 출력은 호환성 보고서로, 인증을 요청하는 동안 게시 포털에 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-291">The output of the tool is a compatibility report, which should be uploaded on the Publishing Portal while requesting certification.</span></span>

<span data-ttu-id="c4e81-292">인증 도구는 Windows VM과 Linux VM 모두에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-292">The certification tool can be used with both Windows and Linux VMs.</span></span> <span data-ttu-id="c4e81-293">PowerShell을 통해 Windows 기반 VM에 연결하고 SSH.Net을 통해 Linux VM에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-293">It connects to Windows-based VMs via PowerShell and connects to Linux VMs via SSH.Net:</span></span>

1. <span data-ttu-id="c4e81-294">먼저 [Microsoft 다운로드 사이트][link-msft-download]에서 인증 도구를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-294">First, download the certification tool at the [Microsoft download site][link-msft-download].</span></span>
2. <span data-ttu-id="c4e81-295">인증 도구를 연 후 **새 테스트 시작** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-295">Open the certification tool, and then click the **Start New Test** button.</span></span>
3. <span data-ttu-id="c4e81-296">**테스트 정보** 화면에서 테스트 실행에 대한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-296">From the **Test Information** screen, enter a name for the test run.</span></span>
4. <span data-ttu-id="c4e81-297">Linux VM인지 Windows VM인지 여부를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-297">Choose whether your VM is on Linux or Windows.</span></span> <span data-ttu-id="c4e81-298">선택에 따라 후속 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-298">Depending on which you choose, select the subsequent options.</span></span>

### <a name="connect-the-certification-tool-to-a-linux-vm-image"></a><span data-ttu-id="c4e81-299">**Linux VM 이미지에 인증 도구 연결**</span><span class="sxs-lookup"><span data-stu-id="c4e81-299">**Connect the certification tool to a Linux VM image**</span></span>
1. <span data-ttu-id="c4e81-300">SSH 인증 모드: 암호 또는 키 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-300">Select the SSH authentication mode: password or key file.</span></span>
2. <span data-ttu-id="c4e81-301">암호 기반 인증을 사용할 경우 DNS(도메인 이름 시스템) 이름, 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-301">If using password-­based authentication, enter the Domain Name System (DNS) name, user name, and password.</span></span>
3. <span data-ttu-id="c4e81-302">키 파일 인증을 사용할 경우 DNS 이름, 사용자 이름 및 개인 키 위치를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-302">If using key file authentication, enter the DNS name, user name, and private key location.</span></span>

   ![Linux VM 이미지의 암호 인증][img-cert-vm-pswd-lnx]

   ![Linux VM 이미지의 키 파일 인증][img-cert-vm-key-lnx]

### <a name="connect-the-certification-tool-to-a-windows-based-vm-image"></a><span data-ttu-id="c4e81-305">**Windows 기반 VM 이미지에 인증 도구 연결**</span><span class="sxs-lookup"><span data-stu-id="c4e81-305">**Connect the certification tool to a Windows-based VM image**</span></span>
1. <span data-ttu-id="c4e81-306">정규화된 VM DNS 이름을 입력합니다(예: MyVMName.Cloudapp.net).</span><span class="sxs-lookup"><span data-stu-id="c4e81-306">Enter the fully qualified VM DNS name (for example, MyVMName.Cloudapp.net).</span></span>
2. <span data-ttu-id="c4e81-307">사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-307">Enter the user name and password.</span></span>

   ![Windows VM 이미지의 암호 인증][img-cert-vm-pswd-win]

<span data-ttu-id="c4e81-309">Linux 또는 Windows 기반 VM 이미지에 대해 올바른 옵션을 선택한 경우 **연결 테스트** 를 선택하여 SSH.Net 또는 PowerShell에 테스트를 위한 유효한 연결이 있는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-309">After you have selected the correct options for your Linux or Windows-based VM image, select **Test Connection** to ensure that SSH.Net or PowerShell has a valid connection for testing purposes.</span></span> <span data-ttu-id="c4e81-310">연결이 설정되면 **다음** 을 선택하여 테스트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-310">After a connection is established, select **Next** to start the test.</span></span>

<span data-ttu-id="c4e81-311">테스트가 완료되면 각 테스트 요소에 대한 결과(통과/실패/경고)가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-311">When the test is complete, you will receive the results (Pass/Fail/Warning) for each test element.</span></span>

![Linux VM 이미지에 대한 테스트 사례][img-cert-vm-test-lnx]

![Windows VM 이미지에 대한 테스트 사례][img-cert-vm-test-win]

<span data-ttu-id="c4e81-314">테스트 중 하나라도 실패하면 이미지가 인증되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-314">If any of the tests fail, your image will not be certified.</span></span> <span data-ttu-id="c4e81-315">이 경우 요구 사항을 검토하고 필요한 변경 내용을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="c4e81-315">If this occurs, review the requirements and make any necessary changes.</span></span>

<span data-ttu-id="c4e81-316">자동화된 테스트 후에 질문서 화면을 통해 VM 이미지에 추가 입력을 제공하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-316">After the automated test, you are asked to provide additional input on your VM image via a questionnaire screen.</span></span>  <span data-ttu-id="c4e81-317">질문을 작성한 후 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-317">Complete the questions, and then select **Next**.</span></span>

![인증 도구 질문서][img-cert-vm-questionnaire]

![인증 도구 질문서][img-cert-vm-questionnaire-2]

<span data-ttu-id="c4e81-320">질문서를 완료하면 Linux VM 이미지에 대한 SSH 액세스 정보와 실패한 평가에 대한 설명 등의 추가 정보를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-320">After you have completed the questionnaire, you can provide additional information such as SSH access information for the Linux VM image and an explanation for any failed assessments.</span></span> <span data-ttu-id="c4e81-321">실행된 테스트 사례에 대한 테스트 결과 및 로그 파일과 질문서에 대한 답변을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-321">You can download the test results and log files for the executed test cases in addition to your answers to the questionnaire.</span></span> <span data-ttu-id="c4e81-322">VHD와 동일한 컨테이너에 결과를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-322">Save the results in the same container as your VHDs.</span></span>

![인증 테스트 결과 저장][img-cert-vm-results]

### <a name="52-get-the-shared-access-signature-uri-for-your-vm-images"></a><span data-ttu-id="c4e81-324">5.2 VM 이미지에 대한 공유 액세스 서명 URI 가져오기</span><span class="sxs-lookup"><span data-stu-id="c4e81-324">5.2 Get the shared access signature URI for your VM images</span></span>
<span data-ttu-id="c4e81-325">게시 프로세스 중에 SKU에 대해 만든 각 VHD로 안내하는 URI(Uniform Resource Identifier)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-325">During the publishing process, you specify the uniform resource identifiers (URIs) that lead to each of the VHDs you have created for your SKU.</span></span> <span data-ttu-id="c4e81-326">Microsoft는 인증 프로세스 중에 이러한 VHD에 액세스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-326">Microsoft needs access to these VHDs during the certification process.</span></span> <span data-ttu-id="c4e81-327">따라서 각 VHD에 대해 공유 액세스 서명 URI를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-327">Therefore, you need to create a shared access signature URI for each VHD.</span></span> <span data-ttu-id="c4e81-328">이 URI를 게시 포털의 **이미지** 탭에 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-328">This is the URI that should be entered in the **Images** tab in the Publishing Portal.</span></span>

<span data-ttu-id="c4e81-329">만든 공유 액세스 서명 URI는 다음 요구 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-329">The shared access signature URI created should adhere to the following requirements:</span></span>

* <span data-ttu-id="c4e81-330">VHD에 대한 공유 액세스 서명 URI를 생성할 때 나열 및 읽기 권한이면 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-330">When generating shared access signature URIs for your VHDs, List and Read­ permissions are sufficient.</span></span> <span data-ttu-id="c4e81-331">쓰기 또는 삭제 권한을 제공하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="c4e81-331">Do not provide Write or Delete access.</span></span>
* <span data-ttu-id="c4e81-332">액세스 기간은 공유 액세스 서명 URI가 만들어진 날로부터 3주 이상이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-332">The duration for access should be a minimum of three (3) weeks from when the shared access signature URI is created.</span></span>
* <span data-ttu-id="c4e81-333">UTC 시간을 보호하려면 현재 이전 날짜를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-333">To safeguard for UTC time, select the day before the current date.</span></span> <span data-ttu-id="c4e81-334">예를 들어, 현재 날짜가 2014년 10월 6일이면 2014년 10월 5일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-334">For example, if the current date is October 6, 2014, select 10/5/2014.</span></span>

<span data-ttu-id="c4e81-335">Azure Marketplace에 대한 VHD를 공유하는 여러 가지 방법으로 SAS URL을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-335">SAS URL can be generated in multiple ways to share your VHD for Azure Marketplace.</span></span>
<span data-ttu-id="c4e81-336">3가지 권장되는 도구는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-336">Following are the 3 recommended tools:</span></span>

1.  <span data-ttu-id="c4e81-337">Azure Storage 탐색기</span><span class="sxs-lookup"><span data-stu-id="c4e81-337">Azure Storage Explorer</span></span>
2.  <span data-ttu-id="c4e81-338">Microsoft Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="c4e81-338">Microsoft Storage Explorer</span></span>
3.  <span data-ttu-id="c4e81-339">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c4e81-339">Azure CLI</span></span>

<span data-ttu-id="c4e81-340">**Azure Storage Explorer(Windows 사용자에 대해 권장됨)**</span><span class="sxs-lookup"><span data-stu-id="c4e81-340">**Azure Storage Explorer (Recommended for Windows Users)**</span></span>

<span data-ttu-id="c4e81-341">Azure Storage Explorer를 사용하여 SAS URL을 생성하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-341">Following are the steps for generating SAS URL by using Azure Storage Explorer</span></span>

1. <span data-ttu-id="c4e81-342">CodePlex에서 [Azure Storage Explorer 6 미리 보기 3](https://azurestorageexplorer.codeplex.com/)을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-342">Download [Azure Storage Explorer 6 Preview 3](https://azurestorageexplorer.codeplex.com/) from CodePlex.</span></span> <span data-ttu-id="c4e81-343">[Azure Storage Explorer 6 미리 보기](https://azurestorageexplorer.codeplex.com/)로 이동하고 **"다운로드"**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-343">Go to [Azure Storage Explorer 6 Preview](https://azurestorageexplorer.codeplex.com/) and click **"Downloads"**.</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_01.png)

2. <span data-ttu-id="c4e81-345">[AzureStorageExplorer6Preview3.zip](https://azurestorageexplorer.codeplex.com/downloads/get/891668)을 다운로드하고 압축을 푼 후에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-345">Download [AzureStorageExplorer6Preview3.zip](https://azurestorageexplorer.codeplex.com/downloads/get/891668) and install after unzipping it.</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_02.png)

3. <span data-ttu-id="c4e81-347">설치한 후 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-347">After it is installed, open the application.</span></span>
4. <span data-ttu-id="c4e81-348">**계정 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-348">Click **Add Account**.</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_03.png)

5. <span data-ttu-id="c4e81-350">저장소 계정 이름, 저장소 계정 키 및 저장소 끝점 도메인을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-350">Specify the storage account name, storage account key, and storage endpoints domain.</span></span> <span data-ttu-id="c4e81-351">Azure Portal에 대한 VHD를 보관하는 Azure 구독의 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-351">This is the storage account in your Azure subscription where you have kept your VHD on Azure portal.</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_04.png)

6. <span data-ttu-id="c4e81-353">Azure Storage Explorer가 특정 저장소 계정에 연결되면 저장소 계정 내에 포함된 내용을 모두 보여 주기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-353">Once Azure Storage Explorer is connected to your specific storage account, it will start showing all of the contains within the storage account.</span></span> <span data-ttu-id="c4e81-354">운영 체제 디스크 VHD 파일(시나리오에 적용 가능한 경우 데이터 디스크도 해당)을 복사한 컨테이너를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-354">Select the container where you copied the operating system disk VHD file (also data disks if they are applicable for your scenario).</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_05.png)

7. <span data-ttu-id="c4e81-356">Blob 컨테이너를 선택하면 Azure 저장소 탐색기에서 컨테이너 내의 파일을 보여주기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-356">After selecting the blob container, Azure Storage Explorer starts showing the files within the container.</span></span> <span data-ttu-id="c4e81-357">제출해야 하는 이미지 파일(.vhd)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-357">Select the image file (.vhd) that needs to be submitted.</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_06.png)

8.  <span data-ttu-id="c4e81-359">컨테이너의 .vhd 파일을 선택한 후 **보안** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-359">After selecting the .vhd file in the container, click the **Security** tab.</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_07.png)

9.  <span data-ttu-id="c4e81-361">**Blob 컨테이너 보안** 대화 상자의 **액세스 수준** 탭에서 기본값을 그대로 두고 **공유 액세스 서명** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-361">In the **Blob Container Security** dialog box, leave the defaults on the **Access Level** tab, and then click **Shared Access Signatures** tab.</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_08.png)

10. <span data-ttu-id="c4e81-363">.vhd 이미지에 대한 공유 액세스 서명 URI를 생성하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="c4e81-363">Follow the steps below to generate a shared access signature URI for the .vhd image:</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_09.png)

    <span data-ttu-id="c4e81-365">a.</span><span class="sxs-lookup"><span data-stu-id="c4e81-365">a.</span></span> <span data-ttu-id="c4e81-366">**액세스 허용 시작**: UTC 시간에 대한 보호를 위해 현재 날짜 이전으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-366">**Access permitted from:** To safeguard for UTC time, select the day before the current date.</span></span> <span data-ttu-id="c4e81-367">예를 들어, 현재 날짜가 2014년 10월 6일이면 2014년 10월 5일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-367">For example, if the current date is October 6, 2014, select 10/5/2014.</span></span>

    <span data-ttu-id="c4e81-368">b.</span><span class="sxs-lookup"><span data-stu-id="c4e81-368">b.</span></span> <span data-ttu-id="c4e81-369">**액세스 허용 종료**: **액세스 허용 시작** 날짜로부터 3주 이상 지난 날짜를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-369">**Access permitted to:** Select a date that is at least 3 weeks after the **Access permitted from** date.</span></span>

    <span data-ttu-id="c4e81-370">c.</span><span class="sxs-lookup"><span data-stu-id="c4e81-370">c.</span></span> <span data-ttu-id="c4e81-371">**허용 동작**: **나열** 및 **읽기** 권한을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-371">**Actions permitted:** Select the **List** and **Read** permissions.</span></span>

    <span data-ttu-id="c4e81-372">d.</span><span class="sxs-lookup"><span data-stu-id="c4e81-372">d.</span></span> <span data-ttu-id="c4e81-373">vhd 파일을 올바르게 선택한 경우 **액세스할 Blob 이름** 에 확장명이 .vhd인 파일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-373">If you have selected your .vhd file correctly, then your file appears in **Blob name to access** with extension .vhd.</span></span>

    <span data-ttu-id="c4e81-374">e.</span><span class="sxs-lookup"><span data-stu-id="c4e81-374">e.</span></span> <span data-ttu-id="c4e81-375">**서명 생성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-375">Click **Generate Signature**.</span></span>

    <span data-ttu-id="c4e81-376">f.</span><span class="sxs-lookup"><span data-stu-id="c4e81-376">f.</span></span> <span data-ttu-id="c4e81-377">**이 컨테이너의 생성된 공유 액세스 서명 URI**에서 위에 강조 표시된 대로 다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-377">In **Generated Shared Access Signature URI of this container**, check for the following as highlighted above:</span></span>

       - <span data-ttu-id="c4e81-378">이미지 파일 이름과 **".vhd"**가 URI에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-378">Make sure that your image file name and **".vhd"** are in the URI.</span></span>
       - <span data-ttu-id="c4e81-379">서명 끝에 **"=rl"**이 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-379">At the end of the signature, make sure that **"=rl"** appears.</span></span> <span data-ttu-id="c4e81-380">이는 읽기 및 나열 액세스가 성공적으로 제공되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-380">This demonstrates that Read and List access was provided successfully.</span></span>
       - <span data-ttu-id="c4e81-381">서명 중간에 **"sr=c"**가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-381">In middle of the signature, make sure that **"sr=c"** appears.</span></span> <span data-ttu-id="c4e81-382">컨테이너 수준 액세스 권한이 있는지 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-382">This demonstrates that you have container level access</span></span>

11. <span data-ttu-id="c4e81-383">생성된 공유 액세스 서명 URI가 작동하는지 확인하려면 **Test in Browser(브라우저에서 테스트)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-383">To ensure that the generated shared access signature URI works, click **Test in Browser**.</span></span> <span data-ttu-id="c4e81-384">다운로드 프로세스가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-384">It should start the download process.</span></span>

12. <span data-ttu-id="c4e81-385">공유 액세스 서명 URI를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-385">Copy the shared access signature URI.</span></span> <span data-ttu-id="c4e81-386">이 URI는 게시 포털에 붙여넣을 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-386">This is the URI to paste into the Publishing Portal.</span></span>

13. <span data-ttu-id="c4e81-387">SKU에서 각 VHD에 대해 6~10단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-387">Repeat steps 6-10 for each VHD in the SKU.</span></span>

<span data-ttu-id="c4e81-388">**Microsoft Azure Storage Explorer(Windows/MAC/Linux)**</span><span class="sxs-lookup"><span data-stu-id="c4e81-388">**Microsoft Azure Storage Explorer (Windows/MAC/Linux)**</span></span>

<span data-ttu-id="c4e81-389">Microsoft Azure Storage Explorer를 사용하여 SAS URL을 생성하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-389">Following are the steps for generating SAS URL by using Microsoft Azure Storage Explorer</span></span>

1.  <span data-ttu-id="c4e81-390">[http://storageexplorer.com/](http://storageexplorer.com/) 웹 사이트에서 Microsoft Azure Storage Explorer를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-390">Download Microsoft Azure Storage Explorer form [http://storageexplorer.com/](http://storageexplorer.com/) website.</span></span> <span data-ttu-id="c4e81-391">[Microsoft Azure Storage Explorer](http://storageexplorer.com/releasenotes.html)로 이동하여 **"Windows용 다운로드"**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-391">Go to [Microsoft Azure Storage Explorer](http://storageexplorer.com/releasenotes.html) and click **“Download for Windows”**.</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_10.png)

2.  <span data-ttu-id="c4e81-393">설치한 후 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-393">After it is installed, open the application.</span></span>

3.  <span data-ttu-id="c4e81-394">**계정 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-394">Click **Add Account**.</span></span>

4.  <span data-ttu-id="c4e81-395">계정에 로그인하여 구독에 Microsoft Azure Storage Explorer를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-395">Configure Microsoft Azure Storage Explorer to your subscription by sign in to your account</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_11.png)

5.  <span data-ttu-id="c4e81-397">저장소 계정으로 이동하여 컨테이너를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-397">Go to storage account and select the Container</span></span>

6.  <span data-ttu-id="c4e81-398">**"공유 액세스 서명 가져오기"**를</span><span class="sxs-lookup"><span data-stu-id="c4e81-398">Select **“Get Share Access Signature..”**</span></span> <span data-ttu-id="c4e81-399">선택합니다(**컨테이너**를 마우스 오른쪽 버튼으로 클릭).</span><span class="sxs-lookup"><span data-stu-id="c4e81-399">by using Right Click of the **container**</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_12.png)

7.  <span data-ttu-id="c4e81-401">다음에 따른 업데이트 시작 시간, 만료 시간 및 사용 권한</span><span class="sxs-lookup"><span data-stu-id="c4e81-401">Update Start time, Expiry time and Permissions as per following</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_13.png)

    <span data-ttu-id="c4e81-403">a.</span><span class="sxs-lookup"><span data-stu-id="c4e81-403">a.</span></span>  <span data-ttu-id="c4e81-404">**시작 시간:** UTC 시간을 보호하려면 현재 이전 날짜를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-404">**Start Time:** To safeguard for UTC time, select the day before the current date.</span></span> <span data-ttu-id="c4e81-405">예를 들어, 현재 날짜가 2014년 10월 6일이면 2014년 10월 5일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-405">For example, if the current date is October 6, 2014, select 10/5/2014.</span></span>

    <span data-ttu-id="c4e81-406">b.</span><span class="sxs-lookup"><span data-stu-id="c4e81-406">b.</span></span>  <span data-ttu-id="c4e81-407">**만료 시간:** **시작 시간** 날짜 이후 3주 이상 지난 날짜를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-407">**Expiry Time:** Select a date that is at least 3 weeks after the **Start Time** date.</span></span>

    <span data-ttu-id="c4e81-408">c.</span><span class="sxs-lookup"><span data-stu-id="c4e81-408">c.</span></span>  <span data-ttu-id="c4e81-409">**사용 권한**: **나열** 및 **읽기** 권한을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-409">**Permissions:** Select the **List** and **Read** permissions</span></span>

8.  <span data-ttu-id="c4e81-410">컨테이너 공유 액세스 서명 URI를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-410">Copy Container shared access signature URI</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_14.png)

    <span data-ttu-id="c4e81-412">생성된 SAS URL은 컨테이너 수준에 적용되며 이제 여기에 VHD 이름을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-412">Generated SAS URL is for container Level and now we need to add VHD name in it.</span></span>

    <span data-ttu-id="c4e81-413">컨테이너 수준 SAS URL의 형식:`https://testrg009.blob.core.windows.net/vhds?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span><span class="sxs-lookup"><span data-stu-id="c4e81-413">Format of Container Level SAS URL: `https://testrg009.blob.core.windows.net/vhds?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span></span>

    <span data-ttu-id="c4e81-414">아래와 같이 SAS URL의 컨테이너 이름 뒤에 VHD 이름을 삽입합니다.`https://testrg009.blob.core.windows.net/vhds/<VHD NAME>?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span><span class="sxs-lookup"><span data-stu-id="c4e81-414">Insert VHD name after the container name in SAS URL as below `https://testrg009.blob.core.windows.net/vhds/<VHD NAME>?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span></span>

    <span data-ttu-id="c4e81-415">예제:</span><span class="sxs-lookup"><span data-stu-id="c4e81-415">Example:</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_15.png)

    <span data-ttu-id="c4e81-417">TestRGVM201631920152.vhd는 VHD 이름이고 VHD SAS URL은 `https://testrg009.blob.core.windows.net/vhds/TestRGVM201631920152.vhd?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`입니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-417">TestRGVM201631920152.vhd is the VHD Name then VHD SAS URL will be `https://testrg009.blob.core.windows.net/vhds/TestRGVM201631920152.vhd?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span></span>

    - <span data-ttu-id="c4e81-418">이미지 파일 이름과 **".vhd"**가 URI에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-418">Make sure that your image file name and **".vhd"** are in the URI.</span></span>
    - <span data-ttu-id="c4e81-419">서명 중간에 **"sp=rl"**이 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-419">In middle of the signature, make sure that **"sp=rl"** appears.</span></span> <span data-ttu-id="c4e81-420">이는 읽기 및 나열 액세스가 성공적으로 제공되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-420">This demonstrates that Read and List access was provided successfully.</span></span>
    - <span data-ttu-id="c4e81-421">서명 중간에 **"sr=c"**가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-421">In middle of the signature, make sure that **"sr=c"** appears.</span></span> <span data-ttu-id="c4e81-422">컨테이너 수준 액세스 권한이 있는지 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-422">This demonstrates that you have container level access</span></span>

9.  <span data-ttu-id="c4e81-423">생성된 공유 액세스 서명 URI가 작동하는지 확인하려면 브라우저에서 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-423">To ensure that the generated shared access signature URI works, test it in browser.</span></span> <span data-ttu-id="c4e81-424">다운로드 프로세스가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-424">It should start the download process</span></span>

10. <span data-ttu-id="c4e81-425">공유 액세스 서명 URI를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-425">Copy the shared access signature URI.</span></span> <span data-ttu-id="c4e81-426">이 URI는 게시 포털에 붙여넣을 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-426">This is the URI to paste into the Publishing Portal.</span></span>

11. <span data-ttu-id="c4e81-427">SKU에서 각 VHD에 대해 이 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-427">Repeat these steps for each VHD in the SKU.</span></span>

<span data-ttu-id="c4e81-428">**Azure CLI(Windows가 아닌 연속 통합에 권장됨)**</span><span class="sxs-lookup"><span data-stu-id="c4e81-428">**Azure CLI (Recommended for Non-Windows & Continuous Integration)**</span></span>

<span data-ttu-id="c4e81-429">Azure CLI를 사용하여 SAS URL을 생성하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-429">Following are the steps for generating SAS URL by using Azure CLI</span></span>

1.  <span data-ttu-id="c4e81-430">Microsoft Azure CLI를 [여기](https://azure.microsoft.com/en-in/documentation/articles/xplat-cli-install/)에서 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-430">Download Microsoft Azure CLI from [here](https://azure.microsoft.com/en-in/documentation/articles/xplat-cli-install/).</span></span> <span data-ttu-id="c4e81-431">**[Windows](http://aka.ms/webpi-azure-cli)** 및 **[MAC OS](http://aka.ms/mac-azure-cli)**에 대한 다양한 링크를 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-431">You can also find different links for **[Windows](http://aka.ms/webpi-azure-cli)** and **[MAC OS](http://aka.ms/mac-azure-cli)**.</span></span>

2.  <span data-ttu-id="c4e81-432">다운로드되면 설치하세요.</span><span class="sxs-lookup"><span data-stu-id="c4e81-432">Once it is downloaded, please install</span></span>

3.  <span data-ttu-id="c4e81-433">다음 코드를 사용하여 PowerShell 파일을 만들고 로컬에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-433">Create a PowerShell file with following code and save it in local</span></span>

          $conn="DefaultEndpointsProtocol=https;AccountName=<StorageAccountName>;AccountKey=<Storage Account Key>"
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl <Permission End Date> -c $conn --start <Permission Start Date>  

    <span data-ttu-id="c4e81-434">위에 있는 다음 매개 변수를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-434">Update the following parameters in above</span></span>

    <span data-ttu-id="c4e81-435">a.</span><span class="sxs-lookup"><span data-stu-id="c4e81-435">a.</span></span> <span data-ttu-id="c4e81-436">**`<StorageAccountName>`**: 저장소 계정 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-436">**`<StorageAccountName>`**: Give your storage account name</span></span>

    <span data-ttu-id="c4e81-437">b.</span><span class="sxs-lookup"><span data-stu-id="c4e81-437">b.</span></span> <span data-ttu-id="c4e81-438">**`<Storage Account Key>`**: 저장소 계정 키를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-438">**`<Storage Account Key>`**: Give your storage account key</span></span>

    <span data-ttu-id="c4e81-439">c.</span><span class="sxs-lookup"><span data-stu-id="c4e81-439">c.</span></span> <span data-ttu-id="c4e81-440">**`<Permission Start Date>`**: UTC 시간을 보호하려면 현재 이전 날짜를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-440">**`<Permission Start Date>`**: To safeguard for UTC time, select the day before the current date.</span></span> <span data-ttu-id="c4e81-441">예를 들어, 현재 날짜가 2016년 10월 26일이면 값은 2016/10/25입니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-441">For example, if the current date is October 26, 2016, then value should be 10/25/2016</span></span>

    <span data-ttu-id="c4e81-442">d.</span><span class="sxs-lookup"><span data-stu-id="c4e81-442">d.</span></span> <span data-ttu-id="c4e81-443">**`<Permission End Date>`**: **시작 날짜** 이후 3주 이상 지난 날짜를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-443">**`<Permission End Date>`**: Select a date that is at least 3 weeks after the **Start Date**.</span></span> <span data-ttu-id="c4e81-444">값은 **2016/11/02**이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-444">Then value should be **11/02/2016**.</span></span>

    <span data-ttu-id="c4e81-445">다음은 적절한 매개 변수를 업데이트한 후의 예제 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-445">Following is the example code after updating proper parameters</span></span>

          $conn="DefaultEndpointsProtocol=https;AccountName=st20151;AccountKey=TIQE5QWMKHpT5q2VnF1bb+NUV7NVMY2xmzVx1rdgIVsw7h0pcI5nMM6+DVFO65i4bQevx21dmrflA91r0Vh2Yw=="
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl 11/02/2016 -c $conn --start 10/25/2016  

4.  <span data-ttu-id="c4e81-446">"관리자 권한으로 실행" 모드로 Powershell 편집기를 열고 3단계에서 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-446">Open Powershell editor with “Run as Administrator” mode and open file in step #3.</span></span>

5.  <span data-ttu-id="c4e81-447">스크립트를 실행하면 컨테이너 수준 액세스에 대한 SAS URL을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-447">Run the script and it will provide you the SAS URL for container level access</span></span>

    <span data-ttu-id="c4e81-448">다음은 SAS 서명의 출력으로 메모장에서 강조 표시된 부분을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-448">Following will be the output of the SAS Signature and copy the highlighted part in a notepad</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_16.png)

6.  <span data-ttu-id="c4e81-450">이제 컨테이너 수준 SAS URL이 있으므로 여기에 VHD의 이름을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-450">Now you will get container level SAS URL and you need to add VHD name in it.</span></span>

    <span data-ttu-id="c4e81-451">컨테이너 수준 SAS URL #</span><span class="sxs-lookup"><span data-stu-id="c4e81-451">Container level SAS URL #</span></span>

    `https://st20151.blob.core.windows.net/vhds?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

7.  <span data-ttu-id="c4e81-452">아래 `https://st20151.blob.core.windows.net/vhds/<VHDName>?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`와 같이 SAS URL의 컨테이너 이름 뒤에 VHD 이름을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-452">Insert VHD name after the container name in SAS URL as shown below `https://st20151.blob.core.windows.net/vhds/<VHDName>?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`</span></span>

    <span data-ttu-id="c4e81-453">예제:</span><span class="sxs-lookup"><span data-stu-id="c4e81-453">Example:</span></span>

    <span data-ttu-id="c4e81-454">TestRGVM201631920152.vhd는 VHD 이름이고 VHD SAS URL은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-454">TestRGVM201631920152.vhd is the VHD Name then VHD SAS URL will be</span></span>

    `https://st20151.blob.core.windows.net/vhds/ TestRGVM201631920152.vhd?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

    - <span data-ttu-id="c4e81-455">이미지 파일 이름과 ".vhd"가 URI에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-455">Make sure that your image file name and ".vhd" are in the URI.</span></span>
    -   <span data-ttu-id="c4e81-456">서명 중간에 "sp=rl"이 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-456">In middle of the signature, make sure that "sp=rl" appears.</span></span> <span data-ttu-id="c4e81-457">이는 읽기 및 나열 액세스가 성공적으로 제공되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-457">This demonstrates that Read and List access was provided successfully.</span></span>
    -   <span data-ttu-id="c4e81-458">서명 중간에 "sr=c"가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-458">In middle of the signature, make sure that "sr=c" appears.</span></span> <span data-ttu-id="c4e81-459">컨테이너 수준 액세스 권한이 있는지 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-459">This demonstrates that you have container level access</span></span>

8.  <span data-ttu-id="c4e81-460">생성된 공유 액세스 서명 URI가 작동하는지 확인하려면 브라우저에서 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-460">To ensure that the generated shared access signature URI works, test it in browser.</span></span> <span data-ttu-id="c4e81-461">다운로드 프로세스가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-461">It should start the download process</span></span>

9.  <span data-ttu-id="c4e81-462">공유 액세스 서명 URI를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-462">Copy the shared access signature URI.</span></span> <span data-ttu-id="c4e81-463">이 URI는 게시 포털에 붙여넣을 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-463">This is the URI to paste into the Publishing Portal.</span></span>

10. <span data-ttu-id="c4e81-464">SKU에서 각 VHD에 대해 이 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-464">Repeat these steps for each VHD in the SKU.</span></span>


### <a name="53-provide-information-about-the-vm-image-and-request-certification-in-the-publishing-portal"></a><span data-ttu-id="c4e81-465">5.3 VM 이미지에 대한 정보를 제공하고 게시 포털에서 인증 요청</span><span class="sxs-lookup"><span data-stu-id="c4e81-465">5.3 Provide information about the VM image and request certification in the Publishing Portal</span></span>
<span data-ttu-id="c4e81-466">제품 및 SKU를 만든 후 해당 SKU에 연결되는 이미지 세부 정보를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-466">After you have created your offer and SKU, you should enter the image details associated with that SKU:</span></span>

1. <span data-ttu-id="c4e81-467">[게시 포털][link-pubportal]로 이동한 후 판매자 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-467">Go to the [Publishing Portal][link-pubportal], and then sign in with your seller account.</span></span>
2. <span data-ttu-id="c4e81-468">**VM 이미지** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-468">Select the **VM images** tab.</span></span>
3. <span data-ttu-id="c4e81-469">페이지의 맨 위에 나열된 식별자는 SKU 식별자가 아니고 실제 제품 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-469">The identifier listed at the top of the page is actually the offer identifier and not the SKU identifier.</span></span>
4. <span data-ttu-id="c4e81-470">**SKU** 섹션에 속성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-470">Fill out the properties under the **SKUs** section.</span></span>
5. <span data-ttu-id="c4e81-471">**운영 체제 제품군**에서 운영 체제 VHD에 연결된 운영 체제 유형을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-471">Under **Operating system family**, click the operating system type associated with the operating system VHD.</span></span>
6. <span data-ttu-id="c4e81-472">**운영 체제** 상자에서 운영 체제에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-472">In the **Operating system** box, describe the operating system.</span></span> <span data-ttu-id="c4e81-473">운영 체제 제품군, 유형, 버전, 업데이트 등과 같은 형식을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="c4e81-473">Consider a format such as operating system family, type, version, and updates.</span></span> <span data-ttu-id="c4e81-474">예를 들어 "Windows Server Datacenter 2014 R2"를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-474">An example is "Windows Server Datacenter 2014 R2."</span></span>
7. <span data-ttu-id="c4e81-475">권장된 가상 컴퓨터 크기를 최대 6개까지 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-475">Select up to six recommended virtual machine sizes.</span></span> <span data-ttu-id="c4e81-476">이는 이미지를 구입하여 배포하려는 경우에 Azure 포털에서 고객의 가격 책정 계층 블레이드에 표시되는 권장 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-476">These are recommendations that get displayed to the customer in the Pricing tier blade in the Azure Portal when they decide to purchase and deploy your image.</span></span> <span data-ttu-id="c4e81-477">**이는 유일한 권장 사항입니다. 고객은 이미지에 지정된 디스크에 적용되는 VM 크기를 선택할 수 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="c4e81-477">**These are only recommendations. The customer is able to select any VM size that accommodates the disks specified in your image.**</span></span>
8. <span data-ttu-id="c4e81-478">버전을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-478">Enter the version.</span></span> <span data-ttu-id="c4e81-479">버전 필드는 제품 및 해당 업데이트를 식별하는 의미 체계 버전을 캡슐화합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-479">The version field encapsulates a semantic version to identify the product and its updates:</span></span>
   * <span data-ttu-id="c4e81-480">버전은 X.Y.Z 형식이며, X, Y 및 Z는 정수여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-480">Versions should be of the form X.Y.Z, where X, Y, and Z are integers.</span></span>
   * <span data-ttu-id="c4e81-481">다른 SKU에서 이미지는 다른 주 버전과 부 버전을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-481">Images in different SKUs can have different major and minor versions.</span></span>
   * <span data-ttu-id="c4e81-482">SKU 내의 버전은 패치 버전이 증가(X.Y.Z에서 Z)하는 증분 변경이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-482">Versions within a SKU should only be incremental changes, which increase the patch version (Z from X.Y.Z).</span></span>
9. <span data-ttu-id="c4e81-483">**OS VHD URL** 상자에 운영 체제 VHD에 대해 만들어진 공유 액세스 서명 URI를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-483">In the **OS VHD URL** box, enter the shared access signature URI created for the operating system VHD.</span></span>
10. <span data-ttu-id="c4e81-484">이 SKU에 데이터 디스크가 연결되어 있는 경우 배포 시 이 데이터 디스크를 탑재할 LUN(논리 단위 번호)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-484">If there are data disks associated with this SKU, select the logical unit number (LUN) to which you would like this data disk to be mounted upon deployment.</span></span>
11. <span data-ttu-id="c4e81-485">**LUN X VHD URL** 상자에 첫 번째 데이터 VHD에 대해 만들어진 공유 액세스 서명 URI를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-485">In the **LUN X VHD URL** box, enter the shared access signature URI created for the first data VHD.</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-3.png)


## <a name="common-sas-url-issues--fixes"></a><span data-ttu-id="c4e81-487">일반적인 SAS URL 문제 및 해결</span><span class="sxs-lookup"><span data-stu-id="c4e81-487">Common SAS URL issues & fixes</span></span>

|<span data-ttu-id="c4e81-488">문제</span><span class="sxs-lookup"><span data-stu-id="c4e81-488">Issue</span></span>|<span data-ttu-id="c4e81-489">오류 메시지</span><span class="sxs-lookup"><span data-stu-id="c4e81-489">Failure Message</span></span>|<span data-ttu-id="c4e81-490">해결</span><span class="sxs-lookup"><span data-stu-id="c4e81-490">Fix</span></span>|<span data-ttu-id="c4e81-491">문서 링크</span><span class="sxs-lookup"><span data-stu-id="c4e81-491">Documentation Link</span></span>|
|---|---|---|---|
|<span data-ttu-id="c4e81-492">이미지 복사 중 오류 - "?"가 SAS URL에 없습니다</span><span class="sxs-lookup"><span data-stu-id="c4e81-492">Failure in copying images - "?" is not found in SAS url</span></span>|<span data-ttu-id="c4e81-493">오류: 이미지 복사</span><span class="sxs-lookup"><span data-stu-id="c4e81-493">Failure: Copying Images.</span></span> <span data-ttu-id="c4e81-494">제공된 SAS URI를 사용하여 Blob을 다운로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-494">Not able to download blob using provided SAS Uri.</span></span>|<span data-ttu-id="c4e81-495">권장 도구를 사용하여 SAS URL 업데이트</span><span class="sxs-lookup"><span data-stu-id="c4e81-495">Update the SAS Url using recommended tools</span></span>|[<span data-ttu-id="c4e81-496">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span><span class="sxs-lookup"><span data-stu-id="c4e81-496">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="c4e81-497">이미지 복사 중 오류 - "st" 및 "se" 매개 변수가 SAS URL에 없습니다</span><span class="sxs-lookup"><span data-stu-id="c4e81-497">Failure in copying images - “st” and “se” parameters not in SAS url</span></span>|<span data-ttu-id="c4e81-498">오류: 이미지 복사</span><span class="sxs-lookup"><span data-stu-id="c4e81-498">Failure: Copying Images.</span></span> <span data-ttu-id="c4e81-499">제공된 SAS URI를 사용하여 Blob을 다운로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-499">Not able to download blob using provided SAS Uri.</span></span>|<span data-ttu-id="c4e81-500">시작 및 종료 날짜로 SAS URL 업데이트</span><span class="sxs-lookup"><span data-stu-id="c4e81-500">Update the SAS Url with Start and End dates on it</span></span>|[<span data-ttu-id="c4e81-501">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span><span class="sxs-lookup"><span data-stu-id="c4e81-501">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="c4e81-502">이미지 복사 중 오류 - “sp=rl”이 SAS URL에 없습니다</span><span class="sxs-lookup"><span data-stu-id="c4e81-502">Failure in copying images - “sp=rl” not in SAS url</span></span>|<span data-ttu-id="c4e81-503">오류: 이미지 복사</span><span class="sxs-lookup"><span data-stu-id="c4e81-503">Failure: Copying Images.</span></span> <span data-ttu-id="c4e81-504">제공된 SAS URI를 사용하여 Blob을 다운로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-504">Not able to download blob using provided SAS Uri</span></span>|<span data-ttu-id="c4e81-505">"읽기" 및 "나열"로 설정된 사용 권한으로 SAS URL 업데이트</span><span class="sxs-lookup"><span data-stu-id="c4e81-505">Update the SAS Url with permissions set as “Read” & “List</span></span>|[<span data-ttu-id="c4e81-506">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span><span class="sxs-lookup"><span data-stu-id="c4e81-506">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="c4e81-507">이미지 복사 중 오류 - SAS URL은 VHD 이름에 공백을 포함합니다</span><span class="sxs-lookup"><span data-stu-id="c4e81-507">Failure in copying images - SAS url have white spaces in vhd name</span></span>|<span data-ttu-id="c4e81-508">오류: 이미지 복사</span><span class="sxs-lookup"><span data-stu-id="c4e81-508">Failure: Copying Images.</span></span> <span data-ttu-id="c4e81-509">제공된 SAS URI를 사용하여 Blob을 다운로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-509">Not able to download blob using provided SAS Uri.</span></span>|<span data-ttu-id="c4e81-510">공백 없이 SAS URL 업데이트</span><span class="sxs-lookup"><span data-stu-id="c4e81-510">Update the SAS Url without white spaces</span></span>|[<span data-ttu-id="c4e81-511">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span><span class="sxs-lookup"><span data-stu-id="c4e81-511">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="c4e81-512">이미지 복사 중 오류 – SAS URL 권한 부여 오류</span><span class="sxs-lookup"><span data-stu-id="c4e81-512">Failure in copying images – SAS Url Authorization error</span></span>|<span data-ttu-id="c4e81-513">오류: 이미지 복사</span><span class="sxs-lookup"><span data-stu-id="c4e81-513">Failure: Copying Images.</span></span> <span data-ttu-id="c4e81-514">권한 부여 오류로 인해 Blob을 다운로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-514">Not able to download blob due to authorization error</span></span>|<span data-ttu-id="c4e81-515">SAS URL 다시 생성</span><span class="sxs-lookup"><span data-stu-id="c4e81-515">Regenerate the SAS Url</span></span>|[<span data-ttu-id="c4e81-516">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span><span class="sxs-lookup"><span data-stu-id="c4e81-516">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|


## <a name="next-step"></a><span data-ttu-id="c4e81-517">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c4e81-517">Next step</span></span>
<span data-ttu-id="c4e81-518">SKU 세부 정보를 완료하면 [Azure Marketplace 마케팅 콘텐츠 가이드][link-pushstaging]를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-518">After you are done with the SKU details, you can move forward to the [Azure Marketplace marketing content guide][link-pushstaging].</span></span> <span data-ttu-id="c4e81-519">게시 프로세스의 해당 단계에서는 **3단계: 스테이징에서 VM 제품 테스트** 이전에 필요한 마케팅 콘텐츠, 가격 책정 및 기타 정보를 제공합니다. 여기에서 제품을 Azure Marketplace에 배포하여 일반에게 공개하고 판매하기 전에 다양한 사용 사례 시나리오를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c4e81-519">In that step of the publishing process, you provide the marketing content, pricing, and other information necessary prior to **Step 3: Testing your VM offer in staging**, where you test various use-case scenarios before deploying the offer to the Azure Marketplace for public visibility and purchase.</span></span>  

## <a name="see-also"></a><span data-ttu-id="c4e81-520">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c4e81-520">See also</span></span>
* [<span data-ttu-id="c4e81-521">시작: Azure 마켓플레이스에 제품을 게시하는 방법</span><span class="sxs-lookup"><span data-stu-id="c4e81-521">Getting started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

[img-acom-1]:media/marketplace-publishing-vm-image-creation/vm-image-acom-datacenter.png
[img-portal-vm-size]:media/marketplace-publishing-vm-image-creation/vm-image-portal-size.png
[img-portal-vm-create]:media/marketplace-publishing-vm-image-creation/vm-image-portal-create-vm.png
[img-portal-vm-location]:media/marketplace-publishing-vm-image-creation/vm-image-portal-location.png
[img-portal-vm-rdp]:media/marketplace-publishing-vm-image-creation/vm-image-portal-rdp.png
[img-azstg-add]:media/marketplace-publishing-vm-image-creation/vm-image-storage-add.png
[img-manage-vm-new]:media/marketplace-publishing-vm-image-creation/vm-image-manage-new.png
[img-manage-vm-select]:media/marketplace-publishing-vm-image-creation/vm-image-manage-select.png
[img-cert-vm-key-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-keyfile-linux.png
[img-cert-vm-pswd-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-linux.png
[img-cert-vm-pswd-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-win.png
[img-cert-vm-test-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-linux.png
[img-cert-vm-test-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-win.png
[img-cert-vm-results]:media/marketplace-publishing-vm-image-creation/vm-image-certification-results.png
[img-cert-vm-questionnaire]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire.png
[img-cert-vm-questionnaire-2]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire-2.png
[img-pubportal-vm-skus]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus.png
[img-pubportal-vm-skus-2]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-2.png

[link-pushstaging]:marketplace-publishing-push-to-staging.md
[link-github-waagent]:https://github.com/Azure/WALinuxAgent
[link-azure-codeplex]:https://azurestorageexplorer.codeplex.com/
[link-azure-2]:../storage/blobs/storage-dotnet-shared-access-signature-part-2.md
[link-azure-1]:../storage/common/storage-dotnet-shared-access-signature-part-1.md
[link-msft-download]:http://www.microsoft.com/download/details.aspx?id=44299
[link-technet-3]:https://technet.microsoft.com/library/hh846766.aspx
[link-technet-2]:https://msdn.microsoft.com/library/dn495261.aspx
[link-azure-portal]:https://portal.azure.com
[link-pubportal]:https://publish.windowsazure.com
[link-sql-2014-ent]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014enterprisewindowsserver2012r2/
[link-sql-2014-std]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014standardwindowsserver2012r2/
[link-sql-2014-web]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014webwindowsserver2012r2/
[link-sql-2012-ent]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2enterprisewindowsserver2012/
[link-sql-2012-std]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2standardwindowsserver2012/
[link-sql-2012-web]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2webwindowsserver2012/
[link-datactr-2012-r2]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2012r2datacenter/
[link-datactr-2012]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2012datacenter/
[link-datactr-2008-r2]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2008r2sp1/
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-technet-1]:https://technet.microsoft.com/library/hh848454.aspx
[link-azure-vm-2]:./virtual-machines-linux-agent-user-guide/
[link-openssl]:https://www.openssl.org/
[link-intsvc]:http://www.microsoft.com/download/details.aspx?id=41554
[link-python]:https://www.python.org/
