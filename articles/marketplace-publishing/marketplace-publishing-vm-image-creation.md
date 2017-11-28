---
title: "Azure 마켓플레이스 hello에 대 한 가상 컴퓨터 이미지 aaaCreating | Microsoft Docs"
description: "어떻게 toocreate 가상 컴퓨터 이미지 hello Azure Marketplace에 대 한 다른 사용자에 대 한 toopurchase 대 한 자세한 설명입니다."
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
ms.openlocfilehash: 65e1c0530bb050fb379a52544e36c55faacd84df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toocreate-a-virtual-machine-image-for-hello-azure-marketplace"></a><span data-ttu-id="8b37e-103">가이드 toocreate hello Azure Marketplace에 대 한 가상 컴퓨터 이미지</span><span class="sxs-lookup"><span data-stu-id="8b37e-103">Guide toocreate a virtual machine image for hello Azure Marketplace</span></span>
<span data-ttu-id="8b37e-104">이 문서에서는 **2 단계**, hello 가상 하드 디스크 (Vhd)가 Azure 마켓플레이스 toohello 배포한를 준비 하는 것을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-104">This article, **Step 2**, walks you through preparing hello virtual hard disks (VHDs) that you will deploy toohello Azure Marketplace.</span></span> <span data-ttu-id="8b37e-105">Vhd 프로그램 SKU의 hello 기초가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-105">Your VHDs are hello foundation of your SKU.</span></span> <span data-ttu-id="8b37e-106">hello 프로세스는 Windows 기반 또는 Linux 기반 SKU를 제공 하 고 있는지 여부에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-106">hello process differs depending on whether you are providing a Linux-based or Windows-based SKU.</span></span> <span data-ttu-id="8b37e-107">이 문서에서는 두 시나리오를 모두 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-107">This article covers both scenarios.</span></span> <span data-ttu-id="8b37e-108">이 프로세스는 [계정 만들기 및 등록][link-acct-creation]과 함께 병렬로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-108">This process can be performed in parallel with [Account creation and registration][link-acct-creation].</span></span>

## <a name="1-define-offers-and-skus"></a><span data-ttu-id="8b37e-109">1. 제품 및 SKU 정의</span><span class="sxs-lookup"><span data-stu-id="8b37e-109">1. Define Offers and SKUs</span></span>
<span data-ttu-id="8b37e-110">이 섹션에서는 toodefine hello 행사와 관련 된 각각의 Sku를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-110">In this section, you learn toodefine hello offers and their associated SKUs.</span></span>

<span data-ttu-id="8b37e-111">제품의 Sku의 "부모" tooall입니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-111">An offer is a "parent" tooall of its SKUs.</span></span> <span data-ttu-id="8b37e-112">제품을 여러 개 보유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-112">You can have multiple offers.</span></span> <span data-ttu-id="8b37e-113">Toostructure를 결정 하는 방법은 해당 제공 tooyou를입니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-113">How you decide toostructure your offers is up tooyou.</span></span> <span data-ttu-id="8b37e-114">제안을 toostaging 푸시됩니다와 Sku를 모두 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-114">When an offer is pushed toostaging, it is pushed along with all of its SKUs.</span></span> <span data-ttu-id="8b37e-115">Hello URL에 표시 될 있으므로 SKU 식별자를를 신중 하 게 고려:</span><span class="sxs-lookup"><span data-stu-id="8b37e-115">Carefully consider your SKU identifiers, because they will be visible in hello URL:</span></span>

* <span data-ttu-id="8b37e-116">Azure.com: http://azure.microsoft.com/marketplace/partners/{PartnerNamespace}/{OfferIdentifier}-{SKUidentifier}</span><span class="sxs-lookup"><span data-stu-id="8b37e-116">Azure.com: http://azure.microsoft.com/marketplace/partners/{PartnerNamespace}/{OfferIdentifier}-{SKUidentifier}</span></span>
* <span data-ttu-id="8b37e-117">Azure Preview 포털: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{SKUIDdentifier}</span><span class="sxs-lookup"><span data-stu-id="8b37e-117">Azure preview portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{SKUIDdentifier}</span></span>  

<span data-ttu-id="8b37e-118">SKU에는 VM 이미지에 대 한 hello 상용 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-118">A SKU is hello commercial name for a VM image.</span></span> <span data-ttu-id="8b37e-119">VM 이미지에는 운영 체제 디스크 하나와 0개 이상의 데이터 디스크가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-119">A VM image contains one operating system disk and zero or more data disks.</span></span> <span data-ttu-id="8b37e-120">가상 컴퓨터에 대 한 전체 저장소 프로필 기본적으로 hello 이며</span><span class="sxs-lookup"><span data-stu-id="8b37e-120">It is essentially hello complete storage profile for a virtual machine.</span></span> <span data-ttu-id="8b37e-121">디스크당 VHD 하나가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-121">One VHD is needed per disk.</span></span> <span data-ttu-id="8b37e-122">빈 데이터 디스크에 만든 VHD toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-122">Even blank data disks require a VHD toobe created.</span></span>

<span data-ttu-id="8b37e-123">사용 하는 운영 체제에 관계 없이 hello 최소 개수의 hello SKU에 필요한 데이터 디스크를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-123">Regardless of which operating system you use, add only hello minimum number of data disks needed by hello SKU.</span></span> <span data-ttu-id="8b37e-124">고객 배포의 hello 시간에 있는 이미지의 일부 디스크를 제거할 수 없습니다 있지만 항상 디스크 추가할 수 중 이나 개발 후가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-124">Customers cannot remove disks that are part of an image at hello time of deployment but can always add disks during or after deployment if they need them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b37e-125">**새 이미지 버전에서 디스크 수를 변경하지 마세요.**</span><span class="sxs-lookup"><span data-stu-id="8b37e-125">**Do not change disk count in a new image version.**</span></span> <span data-ttu-id="8b37e-126">Hello 이미지에 데이터 디스크를 다시 구성 해야 하는 경우 새로운 SKU를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-126">If you must reconfigure Data disks in hello image, define a new SKU.</span></span> <span data-ttu-id="8b37e-127">다른 디스크 개수로 새 이미지 버전 게시 주요 hello ARM 템플릿 및 기타 시나리오를 통해 솔루션의 자동 크기 조정, 자동 배포의 경우에 새 이미지 버전에 따라 새 배포의 hello 잠재력을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-127">Publishing a new image version with different disk counts will have hello potential of breaking new deployment based on hello new image version in cases of auto-scaling, automatic deployments of solutions through ARM templates and other scenarios.</span></span>
>
>

### <a name="11-add-an-offer"></a><span data-ttu-id="8b37e-128">1.1 제품 추가</span><span class="sxs-lookup"><span data-stu-id="8b37e-128">1.1 Add an offer</span></span>
1. <span data-ttu-id="8b37e-129">Toohello 로그인 [게시 포털] [ link-pubportal] 판매자 계정을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-129">Sign in toohello [Publishing Portal][link-pubportal] by using your seller account.</span></span>
2. <span data-ttu-id="8b37e-130">선택 hello **가상 컴퓨터** hello 게시 포털을 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-130">Select hello **Virtual Machines** tab of hello Publishing Portal.</span></span> <span data-ttu-id="8b37e-131">Hello 메시지 표시 입력 필드에 제품 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-131">In hello prompted entry field, enter your offer name.</span></span> <span data-ttu-id="8b37e-132">hello 제공 이름은 일반적으로 hello 이름에 hello 제품이 나 서비스 toosell hello Azure Marketplace에서에서 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-132">hello offer name is typically hello name of hello product or service that you plan toosell in hello Azure Marketplace.</span></span>
3. <span data-ttu-id="8b37e-133">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-133">Select **Create**.</span></span>

### <a name="12-define-a-sku"></a><span data-ttu-id="8b37e-134">1.2 SKU 정의</span><span class="sxs-lookup"><span data-stu-id="8b37e-134">1.2 Define a SKU</span></span>
<span data-ttu-id="8b37e-135">제공 하는 서비스를 추가한 후 toodefine 필요 하 고 프로그램 Sku를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-135">After you have added an offer, you need toodefine and identify your SKUs.</span></span> <span data-ttu-id="8b37e-136">게시자는 제품을 여러 개 보유할 수 있으며 각 제품에는 그 아래 여러 개의 SKU를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-136">You can have multiple offers, and each offer can have multiple SKUs under it.</span></span> <span data-ttu-id="8b37e-137">제안을 toostaging 푸시됩니다와 Sku를 모두 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-137">When an offer is pushed toostaging, it is pushed along with all of its SKUs.</span></span>

1. <span data-ttu-id="8b37e-138">**SKU를 추가합니다.**</span><span class="sxs-lookup"><span data-stu-id="8b37e-138">**Add a SKU.**</span></span> <span data-ttu-id="8b37e-139">hello SKU hello URL에 사용 되는 식별자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-139">hello SKU requires an identifier, which is used in hello URL.</span></span> <span data-ttu-id="8b37e-140">hello 식별자 게시 프로필 내에서 고유 해야 하지만 다른 게시자와 식별 충돌의 위험이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-140">hello identifier must be unique within your publishing profile, but there is no risk of identifier collision with other publishers.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8b37e-141">hello에서 제공 하 고 SKU 식별자 hello Marketplace에에서 hello 제공 URL에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-141">hello offer and SKU identifiers are displayed in hello offer URL in hello Marketplace.</span></span>
   >
   >
2. <span data-ttu-id="8b37e-142">**SKU에 대한 요약 설명을 추가합니다.**</span><span class="sxs-lookup"><span data-stu-id="8b37e-142">**Add a summary description for your SKU.**</span></span> <span data-ttu-id="8b37e-143">요약 설명이 표시 toocustomers 않으므로으로 설정 해야 쉽게 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-143">Summary descriptions are visible toocustomers, so you should make them easily readable.</span></span> <span data-ttu-id="8b37e-144">이 정보는 hello "푸시 tooStaging" 단계까지 잠긴 toobe가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-144">This information does not need toobe locked until hello "Push tooStaging" phase.</span></span> <span data-ttu-id="8b37e-145">그때 까지는 무료 tooedit는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-145">Until then, you are free tooedit it.</span></span>
3. <span data-ttu-id="8b37e-146">Windows 기반 Sku를 사용 하는 경우의 권장 링크 hello tooacquire hello 버전의 Windows Server를 승인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-146">If you are using Windows-based SKUs, follow hello suggested links tooacquire hello approved versions of Windows Server.</span></span>

## <a name="2-create-an-azure-compatible-vhd-linux-based"></a><span data-ttu-id="8b37e-147">2. Azure 호환 VHD 만들기(Linux 기반)</span><span class="sxs-lookup"><span data-stu-id="8b37e-147">2. Create an Azure-compatible VHD (Linux-based)</span></span>
<span data-ttu-id="8b37e-148">이 섹션 hello Azure Marketplace에 대 한 Linux 기반 VM 이미지를 만들기 위한 최선의 방법에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-148">This section focuses on best practices for creating a Linux-based VM image for hello Azure Marketplace.</span></span> <span data-ttu-id="8b37e-149">단계별 연습은 toohello 설명서 참조: [만들어 포함 된 가상 하드 디스크를 업로드 하는 hello Linux 운영 체제](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="8b37e-149">For a step-by-step walkthrough, refer toohello following documentation: [Creating and Uploading a Virtual Hard Disk that Contains hello Linux Operating System](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

## <a name="3-create-an-azure-compatible-vhd-windows-based"></a><span data-ttu-id="8b37e-150">3. Azure 호환 VHD 만들기(Windows 기반)</span><span class="sxs-lookup"><span data-stu-id="8b37e-150">3. Create an Azure-compatible VHD (Windows-based)</span></span>
<span data-ttu-id="8b37e-151">이 섹션으로 hello Azure Marketplace에 대 한 Windows Server에 기반 하는 SKU hello 단계 toocreate 집중 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-151">This section focuses on hello steps toocreate a SKU based on Windows Server for hello Azure Marketplace.</span></span>

### <a name="31-ensure-that-you-are-using-hello-correct-base-vhds"></a><span data-ttu-id="8b37e-152">기본 Vhd를 수정 하는 hello를 사용 하 고 있는지 확인 합니다. 3.1</span><span class="sxs-lookup"><span data-stu-id="8b37e-152">3.1 Ensure that you are using hello correct base VHDs</span></span>
<span data-ttu-id="8b37e-153">VM 이미지에 대 한 hello 운영 체제 VHD Windows Server 또는 SQL Server에 포함 된 Azure 승인 기본 이미지를 기반으로 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-153">hello operating system VHD for your VM image must be based on an Azure-approved base image that contains Windows Server or SQL Server.</span></span>

<span data-ttu-id="8b37e-154">toobegin, hello hello에 있는 이미지를 다음 중 하나에서 VM을 만들 [Microsoft Azure 포털][link-azure-portal]:</span><span class="sxs-lookup"><span data-stu-id="8b37e-154">toobegin, create a VM from one of hello following images, located at hello [Microsoft Azure portal][link-azure-portal]:</span></span>

* <span data-ttu-id="8b37e-155">Windows Server([2012 R2 Datacenter][link-datactr-2012-r2], [2012 Datacenter][link-datactr-2012], [2008 R2 SP1][link-datactr-2008-r2])</span><span class="sxs-lookup"><span data-stu-id="8b37e-155">Windows Server ([2012 R2 Datacenter][link-datactr-2012-r2], [2012 Datacenter][link-datactr-2012], [2008 R2 SP1][link-datactr-2008-r2])</span></span>
* <span data-ttu-id="8b37e-156">SQL Server 2014 ([Enterprise][link-sql-2014-ent], [Standard][link-sql-2014-std], [Web][link-sql-2014-web])</span><span class="sxs-lookup"><span data-stu-id="8b37e-156">SQL Server 2014 ([Enterprise][link-sql-2014-ent], [Standard][link-sql-2014-std], [Web][link-sql-2014-web])</span></span>
* <span data-ttu-id="8b37e-157">SQL Server 2012 SP2 ([Enterprise][link-sql-2012-ent], [Standard][link-sql-2012-std], [Web][link-sql-2012-web])</span><span class="sxs-lookup"><span data-stu-id="8b37e-157">SQL Server 2012 SP2 ([Enterprise][link-sql-2012-ent], [Standard][link-sql-2012-std], [Web][link-sql-2012-web])</span></span>

<span data-ttu-id="8b37e-158">Hello 게시 포털 hello SKU 페이지 아래에서 이러한 링크를 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-158">These links can also be found in hello Publishing Portal under hello SKU page.</span></span>

> [!TIP]
> <span data-ttu-id="8b37e-159">Hello 현재 Azure 포털 또는 PowerShell을 사용 하는 경우 2014 년 9 월 8 일에 게시 된 및 이후 버전의 Windows Server 이미지 승인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-159">If you are using hello current Azure portal or PowerShell, Windows Server images published on September 8, 2014 and later are approved.</span></span>
>
>

### <a name="32-create-your-windows-based-vm"></a><span data-ttu-id="8b37e-160">3.2 Windows 기반 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="8b37e-160">3.2 Create your Windows-based VM</span></span>
<span data-ttu-id="8b37e-161">Hello Microsoft Azure 포털에서 몇 가지 간단한 단계만 거치면에서 승인 된 기본 이미지에 따라 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-161">From hello Microsoft Azure portal, you can create your VM based on an approved base image in just a few simple steps.</span></span> <span data-ttu-id="8b37e-162">hello 다음은 hello 프로세스의 개요입니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-162">hello following is an overview of hello process:</span></span>

1. <span data-ttu-id="8b37e-163">Hello 기본 이미지 페이지에서 선택 **가상 컴퓨터 만들기** toobe toohello 새 전송 [Microsoft Azure 포털][link-azure-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-163">From hello base image page, select **Create Virtual Machine** toobe directed toohello new [Microsoft Azure portal][link-azure-portal].</span></span>

    ![drawing][img-acom-1]
2. <span data-ttu-id="8b37e-165">Microsoft 계정 hello로 toohello 포털 및 Azure 구독 toouse hello에 대 한 암호를 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-165">Sign in toohello portal with hello Microsoft account and password for hello Azure subscription you want toouse.</span></span>
3. <span data-ttu-id="8b37e-166">선택한 hello 기본 이미지를 사용 하 여 hello 프롬프트 toocreate VM을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-166">Follow hello prompts toocreate a VM by using hello base image you have selected.</span></span> <span data-ttu-id="8b37e-167">Tooprovide 호스트 이름 (hello 컴퓨터의 이름), (관리자 권한으로 등록 됨) 사용자 이름 및 암호에 필요한 VM hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-167">You need tooprovide a host name (name of hello computer), user name (registered as an administrator), and password for hello VM.</span></span>

    ![drawing][img-portal-vm-create]
4. <span data-ttu-id="8b37e-169">Hello VM toodeploy의 hello 크기를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-169">Select hello size of hello VM toodeploy:</span></span>

    <span data-ttu-id="8b37e-170">a.</span><span class="sxs-lookup"><span data-stu-id="8b37e-170">a.</span></span>    <span data-ttu-id="8b37e-171">Toodevelop hello VHD 온-프레미스를 계획 하는 경우에 hello 크기 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-171">If you plan toodevelop hello VHD on-premises, hello size does not matter.</span></span> <span data-ttu-id="8b37e-172">Hello 중 하나를 사용 하는 것이 좋습니다. 더 작은 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-172">Consider using one of hello smaller VMs.</span></span>

    <span data-ttu-id="8b37e-173">b.</span><span class="sxs-lookup"><span data-stu-id="8b37e-173">b.</span></span>    <span data-ttu-id="8b37e-174">Azure의 hello 이미지 toodevelop 하려는 경우에 hello 중 하나를 사용 하 여 hello 선택한 이미지에 대 한 VM 크기를 권장 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-174">If you plan toodevelop hello image in Azure, consider using one of hello recommended VM sizes for hello selected image.</span></span>

    <span data-ttu-id="8b37e-175">c.</span><span class="sxs-lookup"><span data-stu-id="8b37e-175">c.</span></span>    <span data-ttu-id="8b37e-176">가격 책정 정보에 대 한 참조 toohello **가격 책정 계층을 권장** hello 포털에 표시 되는 선택기입니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-176">For pricing information, refer toohello **Recommended pricing tiers** selector displayed on hello portal.</span></span> <span data-ttu-id="8b37e-177">Hello hello 게시자에서 제공 하는 세 가지 권장된 크기를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-177">It will provide hello three recommended sizes provided by hello publisher.</span></span> <span data-ttu-id="8b37e-178">(이 경우 hello 게시자는 Microsoft입니다.)</span><span class="sxs-lookup"><span data-stu-id="8b37e-178">(In this case, hello publisher is Microsoft.)</span></span>

    ![drawing][img-portal-vm-size]
5. <span data-ttu-id="8b37e-180">속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-180">Set properties:</span></span>

    <span data-ttu-id="8b37e-181">a.</span><span class="sxs-lookup"><span data-stu-id="8b37e-181">a.</span></span>    <span data-ttu-id="8b37e-182">빠른 배포를 위해 그대로 두면 hello 아래의 hello 속성에 대 한 기본값 **옵션 구성** 및 **리소스 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-182">For quick deployment, you can leave hello default values for hello properties under **Optional Configuration** and **Resource Group**.</span></span>

    <span data-ttu-id="8b37e-183">b.</span><span class="sxs-lookup"><span data-stu-id="8b37e-183">b.</span></span>    <span data-ttu-id="8b37e-184">아래 **저장소 계정**, hello 저장소 계정 운영 체제는 hello에서 VHD를 저장할 필요에 따라 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-184">Under **Storage Account**, you can optionally select hello storage account in which hello operating system VHD will be stored.</span></span>

    <span data-ttu-id="8b37e-185">c.</span><span class="sxs-lookup"><span data-stu-id="8b37e-185">c.</span></span>    <span data-ttu-id="8b37e-186">아래 **리소스 그룹**, 필요에 따라 어떤 tooplace에 VM을 hello hello 논리 그룹을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-186">Under **Resource Group**, you can optionally select hello logical group in which tooplace hello VM.</span></span>
6. <span data-ttu-id="8b37e-187">선택 hello **위치** 배포:</span><span class="sxs-lookup"><span data-stu-id="8b37e-187">Select hello **Location** for deployment:</span></span>

    <span data-ttu-id="8b37e-188">a.</span><span class="sxs-lookup"><span data-stu-id="8b37e-188">a.</span></span>    <span data-ttu-id="8b37e-189">Toodevelop hello VHD 온-프레미스 하려는 경우 hello 위치 hello 이미지 tooAzure 나중에 업로드할 때문에 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-189">If you plan toodevelop hello VHD on-premises, hello location does not matter because you will upload hello image tooAzure later.</span></span>

    <span data-ttu-id="8b37e-190">b.</span><span class="sxs-lookup"><span data-stu-id="8b37e-190">b.</span></span>    <span data-ttu-id="8b37e-191">Azure의 hello 이미지 toodevelop 하려는 경우 hello 처음부터 hello 미국 기반 Microsoft Azure 지역 중 하나를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-191">If you plan toodevelop hello image in Azure, consider using one of hello US-based Microsoft Azure regions from hello beginning.</span></span> <span data-ttu-id="8b37e-192">인증에 대 한 이미지를 제출 하면 Microsoft에서 사용자 대신 수행 하는 hello VHD 복사 프로세스 속도가 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-192">This speeds up hello VHD copying process that Microsoft performs on your behalf when you submit your image for certification.</span></span>

    ![drawing][img-portal-vm-location]
7. <span data-ttu-id="8b37e-194">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-194">Click **Create**.</span></span> <span data-ttu-id="8b37e-195">hello VM toodeploy를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-195">hello VM starts toodeploy.</span></span> <span data-ttu-id="8b37e-196">분 안에 문자열 성공적인 배포를가지고 있으며 사용자 SKU에 대 한 toocreate hello 이미지를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-196">Within minutes, you will have a successful deployment and can begin toocreate hello image for your SKU.</span></span>

### <a name="33-develop-your-vhd-in-hello-cloud"></a><span data-ttu-id="8b37e-197">3.3 개발 hello 클라우드에서 VHD</span><span class="sxs-lookup"><span data-stu-id="8b37e-197">3.3 Develop your VHD in hello cloud</span></span>
<span data-ttu-id="8b37e-198">프로토콜 RDP (원격 데스크톱)를 사용 하 여 hello 클라우드에서 VHD를 개발 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-198">We strongly recommend that you develop your VHD in hello cloud by using Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="8b37e-199">Hello 사용자 이름 및 암호를 구축 하는 동안 지정 tooRDP를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-199">You connect tooRDP with hello user name and password specified during provisioning.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b37e-200">온-프레미스에서 VHD를 개발하는 경우(권장되지 않음) [온-프레미스에 가상 컴퓨터 이미지 만들기](marketplace-publishing-vm-image-creation-on-premise.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b37e-200">If you develop your VHD on-premises (which is not recommended), see [Creating a virtual machine image on-premises](marketplace-publishing-vm-image-creation-on-premise.md).</span></span> <span data-ttu-id="8b37e-201">VHD 다운로드 hello 클라우드 개발 하는 경우에 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-201">Downloading your VHD is not necessary if you are developing in hello cloud.</span></span>
>
>

<span data-ttu-id="8b37e-202">**Hello를 사용 하 여 RDP를 통해 연결 [Microsoft Azure 포털][link-azure-portal]**</span><span class="sxs-lookup"><span data-stu-id="8b37e-202">**Connect via RDP using hello [Microsoft Azure portal][link-azure-portal]**</span></span>

1. <span data-ttu-id="8b37e-203">**찾아보기** > **VM**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-203">Select **Browse** > **VMs**.</span></span>
2. <span data-ttu-id="8b37e-204">hello 가상 컴퓨터 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-204">hello Virtual machines blade opens.</span></span> <span data-ttu-id="8b37e-205">해당 hello와 tooconnect 원하는 VM 실행 되 고 다음 배포 된 Vm의 hello 목록에서 선택 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-205">Ensure that hello VM that you want tooconnect with is running, and then select it from hello list of deployed VMs.</span></span>
3. <span data-ttu-id="8b37e-206">선택한 VM으로 hello를 설명 하는 블레이드에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-206">A blade opens that describes hello selected VM.</span></span> <span data-ttu-id="8b37e-207">Hello 위쪽 클릭 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-207">At hello top, click **Connect**.</span></span>
4. <span data-ttu-id="8b37e-208">입력 정보 요청된 tooenter hello 사용자 이름 및 암호 프로 비전 중에 지정 된 경우</span><span class="sxs-lookup"><span data-stu-id="8b37e-208">You are prompted tooenter hello user name and password that you specified during provisioning.</span></span>

<span data-ttu-id="8b37e-209">**PowerShell을 사용하여 RDP를 통해 연결**</span><span class="sxs-lookup"><span data-stu-id="8b37e-209">**Connect via RDP using PowerShell**</span></span>

<span data-ttu-id="8b37e-210">원격 데스크톱 파일 tooa 로컬 컴퓨터, toodownload hello를 사용 하 여 [Get-azureremotedesktopfile cmdlet][link-technet-2]합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-210">toodownload a remote desktop file tooa local machine, use hello [Get-AzureRemoteDesktopFile cmdlet][link-technet-2].</span></span> <span data-ttu-id="8b37e-211">toouse이이 cmdlet을 순서, tooknow hello hello 서비스의 이름과 hello VM의 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-211">In order toouse this cmdlet, you need tooknow hello name of hello service and name of hello VM.</span></span> <span data-ttu-id="8b37e-212">Hello에서 hello VM을 만든 경우 [Microsoft Azure 포털][link-azure-portal], VM 속성에서이 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-212">If you created hello VM from hello [Microsoft Azure portal][link-azure-portal], you can find this information under VM properties:</span></span>

1. <span data-ttu-id="8b37e-213">Hello Microsoft Azure 포털에서 선택 **찾아보기** > **Vm**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-213">In hello Microsoft Azure portal, select **Browse** > **VMs**.</span></span>
2. <span data-ttu-id="8b37e-214">hello 가상 컴퓨터 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-214">hello Virtual machines blade opens.</span></span> <span data-ttu-id="8b37e-215">Hello 배포 된 VM을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-215">Select hello VM that you deployed.</span></span>
3. <span data-ttu-id="8b37e-216">선택한 VM으로 hello를 설명 하는 블레이드에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-216">A blade opens that describes hello selected VM.</span></span>
4. <span data-ttu-id="8b37e-217">**속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-217">Click **Properties**.</span></span>
5. <span data-ttu-id="8b37e-218">hello hello 도메인 이름의 첫 부분에는 hello 서비스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-218">hello first portion of hello domain name is hello service name.</span></span> <span data-ttu-id="8b37e-219">hello 호스트 이름은 hello VM 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-219">hello host name is hello VM name.</span></span>

    ![drawing][img-portal-vm-rdp]
6. <span data-ttu-id="8b37e-221">만든 hello VM toohello 관리자의 로컬 데스크톱에 대 한 hello cmdlet toodownload hello RDP 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-221">hello cmdlet toodownload hello RDP file for hello created VM toohello administrator's local desktop is as follows.</span></span>

        Get‐AzureRemoteDesktopFile ‐ServiceName “baseimagevm‐6820cq00” ‐Name “BaseImageVM” –LocalPath “C:\Users\Administrator\Desktop\BaseImageVM.rdp”

<span data-ttu-id="8b37e-222">Hello 문서에서 RDP에 대 한 자세한 내용은 MSDN에서 확인할 수 있습니다 [RDP 또는 SSH를 사용 하 여 Azure VM tooan 연결](http://msdn.microsoft.com/library/azure/dn535788.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-222">More information about RDP can be found on MSDN in hello article [Connect tooan Azure VM with RDP or SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx).</span></span>

<span data-ttu-id="8b37e-223">**VM 구성 및 SKU 만들기**</span><span class="sxs-lookup"><span data-stu-id="8b37e-223">**Configure a VM and create your SKU**</span></span>

<span data-ttu-id="8b37e-224">Hello 운영 체제 VHD를 다운로드 한 후 HyperV를 사용 하 고 사용자 SKU 만드는 VM toobegin를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-224">After hello operating system VHD is downloaded, use Hyper­V and configure a VM toobegin creating your SKU.</span></span> <span data-ttu-id="8b37e-225">자세한 단계는 hello TechNet 링크에서 찾을 수 있습니다: [HyperV 설치 및 구성의 VM](http://technet.microsoft.com/library/hh846766.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-225">Detailed steps can be found at hello following TechNet link: [Install Hyper­V and Configure a VM](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="34-choose-hello-correct-vhd-size"></a><span data-ttu-id="8b37e-226">3.4 hello 올바른 VHD 크기 선택</span><span class="sxs-lookup"><span data-stu-id="8b37e-226">3.4 Choose hello correct VHD size</span></span>
<span data-ttu-id="8b37e-227">VM 이미지의 hello Windows 운영 체제 VHD 128 GB 고정 형식 VHD로 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-227">hello Windows operating system VHD in your VM image should be created as a 128-GB fixed-format VHD.</span></span>  

<span data-ttu-id="8b37e-228">Hello 실제 크기는 128GB 보다 작거나, VHD hello 스파스 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-228">If hello physical size is less than 128 GB, hello VHD should be sparse.</span></span> <span data-ttu-id="8b37e-229">제공 된 기본 Windows 및 SQL Server 이미지 hello 이러한 요구 사항을 이미 충족, 따라서 hello 얻을 VHD의 hello hello 또는 형식 크기를 변경 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="8b37e-229">hello base Windows and SQL Server images provided already meet these requirements, so do not change hello format or hello size of hello VHD obtained.</span></span>  

<span data-ttu-id="8b37e-230">데이터 디스크는 1TB이하여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-230">Data disks can be as large as 1 TB.</span></span> <span data-ttu-id="8b37e-231">Hello 디스크 크기를 결정할 때는 고객 수 없는 크기가 조정 된다는 Vhd 이미지 내에서 배포의 hello 시 기억해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-231">When deciding on hello disk size, remember that customers cannot resize VHDs within an image at hello time of deployment.</span></span> <span data-ttu-id="8b37e-232">데이터 디스크 VHD는 고정 형식 VHD로 작성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-232">Data disk VHDs should be created as a fixed-format VHD.</span></span> <span data-ttu-id="8b37e-233">또한 스파스여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-233">They should also be sparse.</span></span> <span data-ttu-id="8b37e-234">데이터 디스크는 비어 있거나 데이터를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-234">Data disks can be empty or contain data.</span></span>

### <a name="35-install-hello-latest-windows-patches"></a><span data-ttu-id="8b37e-235">3.5 hello 최신 Windows 패치를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-235">3.5 Install hello latest Windows patches</span></span>
<span data-ttu-id="8b37e-236">hello 기본 이미지에 포함 되어 hello 최신 패치를 tootheir 게시 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-236">hello base images contain hello latest patches up tootheir published date.</span></span> <span data-ttu-id="8b37e-237">Hello 운영 체제 만든 VHD를 게시 하기 전에 Windows 업데이트 실행 되 고 모든 hello 최신 위험 및 중요 한 보안 업데이트가 설치 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-237">Before publishing hello operating system VHD you have created, ensure that Windows Update has been run and that all hello latest Critical and Important security updates have been installed.</span></span>

### <a name="36-perform-additional-configuration-and-schedule-tasks-as-necessary"></a><span data-ttu-id="8b37e-238">3.6 필요 시 추가 구성 수행 및 작업 예약</span><span class="sxs-lookup"><span data-stu-id="8b37e-238">3.6 Perform additional configuration and schedule tasks as necessary</span></span>
<span data-ttu-id="8b37e-239">추가 구성이 필요 하며, 경우에 실행 시작 toomake에 모든 변경 내용이 최종 toohello VM을 배포한 후 예약된 된 작업을 사용 하 여 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-239">If additional configuration is needed, consider using a scheduled task that runs at startup toomake any final changes toohello VM after it has been deployed:</span></span>

* <span data-ttu-id="8b37e-240">것이 모범 사례 toohave hello 작업 실행이 완료 되 자체를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-240">It is a best practice toohave hello task delete itself upon successful execution.</span></span>
* <span data-ttu-id="8b37e-241">구성 없이 tooexist 항상 표시할 수 있는 두 개의 드라이브 hello 가지 때문에 C 또는 D 드라이브 이외의 드라이브에 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-241">No configuration should rely on drives other than drives C or D, because these are hello only two drives that are always guaranteed tooexist.</span></span> <span data-ttu-id="8b37e-242">C 드라이브 hello 운영 체제 디스크가 고 D 드라이브 hello 임시 로컬 디스크.</span><span class="sxs-lookup"><span data-stu-id="8b37e-242">Drive C is hello operating system disk, and drive D is hello temporary local disk.</span></span>

### <a name="37-generalize-hello-image"></a><span data-ttu-id="8b37e-243">3.7 hello 이미지를 일반화 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-243">3.7 Generalize hello image</span></span>
<span data-ttu-id="8b37e-244">Azure 마켓플레이스 hello에서 모든 이미지는 일반적인 방법으로 다시 사용할 수 있는 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-244">All images in hello Azure Marketplace must be reusable in a generic fashion.</span></span> <span data-ttu-id="8b37e-245">즉, VHD hello 운영 체제를 일반화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-245">In other words, hello operating system VHD must be generalized:</span></span>

* <span data-ttu-id="8b37e-246">Windows hello 이미지 "sysprepped" 수 있어야 하 고 구성이 hello를 지원 하지 않는 **sysprep** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-246">For Windows, hello image should be "sysprepped," and no configurations should be done that do not support hello **sysprep** command.</span></span>
* <span data-ttu-id="8b37e-247">Hello hello 디렉터리 windir%\System32\Sysprep에서 다음 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-247">You can run hello following command from hello directory %windir%\System32\Sysprep.</span></span>

        sysprep.exe /generalize /oobe /shutdown

  <span data-ttu-id="8b37e-248">다음 MSDN 문서 hello의 단계에서 toosysprep hello 운영 시스템을 제공 하는 방법에 대 한 지침: [만들기 및 업로드 Windows Server VHD tooAzure](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-248">Guidance on how toosysprep hello operating system is provided in Step of hello following MSDN article: [Create and upload a Windows Server VHD tooAzure](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="4-deploy-a-vm-from-your-vhds"></a><span data-ttu-id="8b37e-249">4. VHD에서 VM 배포</span><span class="sxs-lookup"><span data-stu-id="8b37e-249">4. Deploy a VM from your VHDs</span></span>
<span data-ttu-id="8b37e-250">(Hello 일반화 된 운영 체제 VHD와 0 개 이상의 데이터 디스크 Vhd) Vhd를 업로드 한 후 tooan Azure 저장소 계정 수에 등록 하면 사용자 VM 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-250">After you have uploaded your VHDs (hello generalized operating system VHD and zero or more data disk VHDs) tooan Azure storage account, you can register them as a user VM image.</span></span> <span data-ttu-id="8b37e-251">그런 다음 해당 이미지를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-251">Then you can test that image.</span></span> <span data-ttu-id="8b37e-252">운영 체제 VHD을 일반화 하기 때문에 배포할 수 없다는 직접 VM hello hello VHD URL을 제공 하 여 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-252">Note that because your operating system VHD is generalized, you cannot directly deploy hello VM by providing hello VHD URL.</span></span>

<span data-ttu-id="8b37e-253">toolearn VM 이미지에 대 한 자세한 검토 hello 다음 블로그 게시물:</span><span class="sxs-lookup"><span data-stu-id="8b37e-253">toolearn more about VM images, review hello following blog posts:</span></span>

* [<span data-ttu-id="8b37e-254">VM 이미지</span><span class="sxs-lookup"><span data-stu-id="8b37e-254">VM Image</span></span>](https://azure.microsoft.com/blog/vm-image-blog-post/)
* [<span data-ttu-id="8b37e-255">VM 이미지 PowerShell 방법</span><span class="sxs-lookup"><span data-stu-id="8b37e-255">VM Image PowerShell How To</span></span>](https://azure.microsoft.com/blog/vm-image-powershell-how-to-blog-post/)
* [<span data-ttu-id="8b37e-256">Azure에서 VM 이미지 정보</span><span class="sxs-lookup"><span data-stu-id="8b37e-256">About VM images in Azure</span></span>](https://msdn.microsoft.com/library/azure/dn790290.aspx)

### <a name="set-up-hello-necessary-tools-powershell-and-azure-cli"></a><span data-ttu-id="8b37e-257">Hello 필요한 도구, PowerShell 및 Azure CLI 설정</span><span class="sxs-lookup"><span data-stu-id="8b37e-257">Set up hello necessary tools, PowerShell and Azure CLI</span></span>
* [<span data-ttu-id="8b37e-258">어떻게 toosetup PowerShell</span><span class="sxs-lookup"><span data-stu-id="8b37e-258">How toosetup PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="8b37e-259">어떻게 toosetup Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8b37e-259">How toosetup Azure CLI</span></span>](../cli-install-nodejs.md)

### <a name="41-create-a-user-vm-image"></a><span data-ttu-id="8b37e-260">4.1 사용자 VM 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="8b37e-260">4.1 Create a user VM image</span></span>
#### <a name="capture-vm"></a><span data-ttu-id="8b37e-261">VM 캡처</span><span class="sxs-lookup"><span data-stu-id="8b37e-261">Capture VM</span></span>
<span data-ttu-id="8b37e-262">Azure PowerShell/API/CLI를 사용 하 여 VM hello 캡처에 대 한 지침은 아래 제공 된 hello 링크를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="8b37e-262">Please read hello links given below for guidance on capturing hello VM using API/PowerShell/Azure CLI.</span></span>

* [<span data-ttu-id="8b37e-263">API</span><span class="sxs-lookup"><span data-stu-id="8b37e-263">API</span></span>](https://msdn.microsoft.com/library/mt163560.aspx)
* [<span data-ttu-id="8b37e-264">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8b37e-264">PowerShell</span></span>](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="8b37e-265">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8b37e-265">Azure CLI</span></span>](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="generalize-image"></a><span data-ttu-id="8b37e-266">이미지 일반화</span><span class="sxs-lookup"><span data-stu-id="8b37e-266">Generalize Image</span></span>
<span data-ttu-id="8b37e-267">Azure PowerShell/API/CLI를 사용 하 여 VM hello 캡처에 대 한 지침은 아래 제공 된 hello 링크를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="8b37e-267">Please read hello links given below for guidance on capturing hello VM using API/PowerShell/Azure CLI.</span></span>

* [<span data-ttu-id="8b37e-268">API</span><span class="sxs-lookup"><span data-stu-id="8b37e-268">API</span></span>](https://msdn.microsoft.com/library/mt269439.aspx)
* [<span data-ttu-id="8b37e-269">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8b37e-269">PowerShell</span></span>](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="8b37e-270">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8b37e-270">Azure CLI</span></span>](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="42-deploy-a-vm-from-a-user-vm-image"></a><span data-ttu-id="8b37e-271">4.2 사용자 VM 이미지에서 VM 배포</span><span class="sxs-lookup"><span data-stu-id="8b37e-271">4.2 Deploy a VM from a user VM image</span></span>
<span data-ttu-id="8b37e-272">사용자 VM 이미지에서 VM toodeploy hello 현재 사용할 수 있습니다 [Azure 포털](https://manage.windowsazure.com) 또는 PowerShell입니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-272">toodeploy a VM from a user VM image, you can use hello current [Azure portal](https://manage.windowsazure.com) or PowerShell.</span></span>

<span data-ttu-id="8b37e-273">**Hello 현재 Azure 포털에서 VM 배포**</span><span class="sxs-lookup"><span data-stu-id="8b37e-273">**Deploy a VM from hello current Azure portal**</span></span>

1. <span data-ttu-id="8b37e-274">너무 이동**새로** > **계산** > **가상 컴퓨터** > **갤러리에서**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-274">Go too**New** > **Compute** > **Virtual machine** > **From gallery**.</span></span>

    ![drawing][img-manage-vm-new]
2. <span data-ttu-id="8b37e-276">너무 이동**내 이미지**을 다음 선택 hello 어떤 toodeploy에서 VM 이미지는 VM 및:</span><span class="sxs-lookup"><span data-stu-id="8b37e-276">Go too**My images**, and then select hello VM image from which toodeploy a VM:</span></span>

   1. <span data-ttu-id="8b37e-277">사용량 기준 과금 주의 기울여야 toowhich 이미지 때문에 선택 hello **내 이미지** 보기는 운영 체제 이미지와 VM 이미지를 모두 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-277">Pay close attention toowhich image you select, because hello **My images** view lists both operating system images and VM images.</span></span>
   2. <span data-ttu-id="8b37e-278">Hello 디스크 수를 보면 hello 대부분 VM 이미지의 둘 이상의 디스크가 있어야 하기 때문에 어떤 유형의 이미지를 배포 하는 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-278">Looking at hello number of disks can help determine what type of image you are deploying, because hello majority of VM images have more than one disk.</span></span> <span data-ttu-id="8b37e-279">그러나 여전히 가능한 toohave 그러면는 단일 운영 체제 디스크가 하나만 있는 VM 이미지는 **디스크 수가** too1를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-279">However, it is still possible toohave a VM image with only a single operating system disk, which would then have **Number of disks** set too1.</span></span>

      ![drawing][img-manage-vm-select]
3. <span data-ttu-id="8b37e-281">Hello VM 만들기 마법사를 수행 하 고 hello VM 이름, VM 크기, 위치, 사용자 이름 및 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-281">Follow hello VM creation wizard and specify hello VM name, VM size, location, user name, and password.</span></span>

<span data-ttu-id="8b37e-282">**PowerShell에서 VM 배포**</span><span class="sxs-lookup"><span data-stu-id="8b37e-282">**Deploy a VM from PowerShell**</span></span>

<span data-ttu-id="8b37e-283">toodeploy hello에서 큰 VM 일반화 방금 만든 VM 이미지를 hello 다음 cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-283">toodeploy a large VM from hello generalized VM image just created, you can use hello following cmdlets.</span></span>

    $img = Get-AzureVMImage -ImageName "myVMImage"
    $user = "user123"
    $pass = "adminPassword123"
    $myVM = New-AzureVMConfig -Name "VMImageVM" -InstanceSize "Large" -ImageName $img.ImageName | Add-AzureProvisioningConfig -Windows -AdminUsername $user -Password $pass
    New-AzureVM -ServiceName "VMImageCloudService" -VMs $myVM -Location "West US" -WaitForBoot

> [!IMPORTANT]
> <span data-ttu-id="8b37e-284">추가적인 도움이 필요하면 [VHD를 만드는 동안 발생하는 일반적인 문제 해결]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b37e-284">Please refer [Troubleshooting common issues encountered during VHD creation] for additional assistance.</span></span>
>
>

## <a name="5-obtain-certification-for-your-vm-image"></a><span data-ttu-id="8b37e-285">5. VM 이미지에 대한 인증받기</span><span class="sxs-lookup"><span data-stu-id="8b37e-285">5. Obtain certification for your VM image</span></span>
<span data-ttu-id="8b37e-286">Azure 마켓플레이스 hello에 대 한 VM 이미지를 준비 hello 다음 단계에는 toohave 인증 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-286">hello next step in preparing your VM image for hello Azure Marketplace is toohave it certified.</span></span>

<span data-ttu-id="8b37e-287">Hello 확인 결과 toohello 업로드 Vhd가 있는 Azure 컨테이너 추가 제안을, SKU, 정의 하 고, 제출 하는 VM 이미지 인증에 대 한,이 프로세스는 특별 한 인증 도구를 실행 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-287">This process includes running a special certification tool, uploading hello verification results toohello Azure container where your VHDs reside, adding an offer, defining your SKU, and submitting your VM image for certification.</span></span>

### <a name="51-download-and-run-hello-certification-test-tool-for-azure-certified"></a><span data-ttu-id="8b37e-288">5.1 다운로드 하 여 Azure 인증에 대 한 hello 인증 테스트 도구 실행</span><span class="sxs-lookup"><span data-stu-id="8b37e-288">5.1 Download and run hello Certification Test Tool for Azure Certified</span></span>
<span data-ttu-id="8b37e-289">hello 인증 도구는 사용자 VM 이미지에서 사용자를 프로 비전 하는 실행 중인 VM에서 실행, VM 이미지 hello tooensure Microsoft Azure와 호환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-289">hello certification tool runs on a running VM, provisioned from your user VM image, tooensure that hello VM image is compatible with Microsoft Azure.</span></span> <span data-ttu-id="8b37e-290">Hello 지침과 VHD를 준비 하는 방법에 대 한 요구 사항을 충족 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-290">It will verify that hello guidance and requirements about preparing your VHD have been met.</span></span> <span data-ttu-id="8b37e-291">hello 도구의 hello 출력 요청 인증 하는 동안 hello 게시 포털에 업로드 해야 하는 호환성 보고서를 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-291">hello output of hello tool is a compatibility report, which should be uploaded on hello Publishing Portal while requesting certification.</span></span>

<span data-ttu-id="8b37e-292">Windows와 Linux Vm의 경우와 hello 인증 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-292">hello certification tool can be used with both Windows and Linux VMs.</span></span> <span data-ttu-id="8b37e-293">PowerShell 통해 tooWindows 기반 Vm에 연결 하 고 SSH.Net 통해 tooLinux Vm을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-293">It connects tooWindows-based VMs via PowerShell and connects tooLinux VMs via SSH.Net:</span></span>

1. <span data-ttu-id="8b37e-294">먼저, hello에 hello 인증 도구를 다운로드 [Microsoft 다운로드 사이트][link-msft-download]합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-294">First, download hello certification tool at hello [Microsoft download site][link-msft-download].</span></span>
2. <span data-ttu-id="8b37e-295">Hello 인증 도구를 열고 클릭 다음 hello **새 테스트 시작** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-295">Open hello certification tool, and then click hello **Start New Test** button.</span></span>
3. <span data-ttu-id="8b37e-296">Hello에서 **테스트 정보** 화면 hello 테스트 실행에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-296">From hello **Test Information** screen, enter a name for hello test run.</span></span>
4. <span data-ttu-id="8b37e-297">Linux VM인지 Windows VM인지 여부를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-297">Choose whether your VM is on Linux or Windows.</span></span> <span data-ttu-id="8b37e-298">선택한 있는 따라 hello 후속 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-298">Depending on which you choose, select hello subsequent options.</span></span>

### <a name="connect-hello-certification-tool-tooa-linux-vm-image"></a><span data-ttu-id="8b37e-299">**Hello 인증 도구 tooa Linux VM 이미지를 연결 합니다.**</span><span class="sxs-lookup"><span data-stu-id="8b37e-299">**Connect hello certification tool tooa Linux VM image**</span></span>
1. <span data-ttu-id="8b37e-300">SSH 인증 모드 선택 hello: 암호 또는 키 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-300">Select hello SSH authentication mode: password or key file.</span></span>
2. <span data-ttu-id="8b37e-301">암호 기반 인증을 사용 하는 경우 hello 도메인 이름 (DNS System) 이름, 사용자 이름 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-301">If using password-­based authentication, enter hello Domain Name System (DNS) name, user name, and password.</span></span>
3. <span data-ttu-id="8b37e-302">인증 키 파일을 사용 하는 경우 hello DNS 이름, 사용자 이름 및 개인 키 위치를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-302">If using key file authentication, enter hello DNS name, user name, and private key location.</span></span>

   ![Linux VM 이미지의 암호 인증][img-cert-vm-pswd-lnx]

   ![Linux VM 이미지의 키 파일 인증][img-cert-vm-key-lnx]

### <a name="connect-hello-certification-tool-tooa-windows-based-vm-image"></a><span data-ttu-id="8b37e-305">**Hello 인증 도구 tooa Windows 기반 VM 이미지를 연결 합니다.**</span><span class="sxs-lookup"><span data-stu-id="8b37e-305">**Connect hello certification tool tooa Windows-based VM image**</span></span>
1. <span data-ttu-id="8b37e-306">정규화 된 hello VM DNS 이름 (예를 들어 MyVMName.Cloudapp.net)을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-306">Enter hello fully qualified VM DNS name (for example, MyVMName.Cloudapp.net).</span></span>
2. <span data-ttu-id="8b37e-307">Hello 사용자 이름 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-307">Enter hello user name and password.</span></span>

   ![Windows VM 이미지의 암호 인증][img-cert-vm-pswd-win]

<span data-ttu-id="8b37e-309">Linux 또는 Windows 기반 VM 이미지에 대 한 hello 적절 한 옵션을 선택한 후 선택 **연결 테스트** SSH.Net 또는 PowerShell에 테스트용으로 유효한 연결이 있는지 tooensure 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-309">After you have selected hello correct options for your Linux or Windows-based VM image, select **Test Connection** tooensure that SSH.Net or PowerShell has a valid connection for testing purposes.</span></span> <span data-ttu-id="8b37e-310">연결 된 후에 선택 **다음** toostart hello 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-310">After a connection is established, select **Next** toostart hello test.</span></span>

<span data-ttu-id="8b37e-311">Hello 테스트가 완료 되 면 각 테스트 요소에 대 한 hello 결과 (성공/실패/경고) 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-311">When hello test is complete, you will receive hello results (Pass/Fail/Warning) for each test element.</span></span>

![Linux VM 이미지에 대한 테스트 사례][img-cert-vm-test-lnx]

![Windows VM 이미지에 대한 테스트 사례][img-cert-vm-test-win]

<span data-ttu-id="8b37e-314">Hello 테스트 중 하나라도 실패할 경우 이미지는 보증 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-314">If any of hello tests fail, your image will not be certified.</span></span> <span data-ttu-id="8b37e-315">이 경우 hello 요구 사항을 검토 하 고 필요한 변경을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-315">If this occurs, review hello requirements and make any necessary changes.</span></span>

<span data-ttu-id="8b37e-316">테스트를 자동화 하는 hello 후 추가 입력이 tooprovide 설문지 화면을 통해 VM 이미지에 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-316">After hello automated test, you are asked tooprovide additional input on your VM image via a questionnaire screen.</span></span>  <span data-ttu-id="8b37e-317">Hello 질문을 완료 한 후 선택 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-317">Complete hello questions, and then select **Next**.</span></span>

![인증 도구 질문서][img-cert-vm-questionnaire]

![인증 도구 질문서][img-cert-vm-questionnaire-2]

<span data-ttu-id="8b37e-320">Hello 질문을 완료 한 후에 hello Linux VM 이미지에 대 한 SSH 액세스 정보 같은 추가 정보 및 모든 실패 한 평가 대 한 설명을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-320">After you have completed hello questionnaire, you can provide additional information such as SSH access information for hello Linux VM image and an explanation for any failed assessments.</span></span> <span data-ttu-id="8b37e-321">Hello 테스트 결과 다운로드 하 고 실행 하는 hello 테스트 사례에 대 한 파일 추가 tooyour 답변 toohello 설문지 로그인 수입니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-321">You can download hello test results and log files for hello executed test cases in addition tooyour answers toohello questionnaire.</span></span> <span data-ttu-id="8b37e-322">Hello에 hello 결과 저장 Vhd와 동일한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-322">Save hello results in hello same container as your VHDs.</span></span>

![인증 테스트 결과 저장][img-cert-vm-results]

### <a name="52-get-hello-shared-access-signature-uri-for-your-vm-images"></a><span data-ttu-id="8b37e-324">5.2 VM 이미지에 대 한 hello 공유 액세스 서명 URI 가져오기</span><span class="sxs-lookup"><span data-stu-id="8b37e-324">5.2 Get hello shared access signature URI for your VM images</span></span>
<span data-ttu-id="8b37e-325">게시 프로세스는 hello, 하는 동안 hello 만든 프로그램 SKU에 대 한 Vhd의 tooeach 이어지는 hello uniform resource identifier (Uri)를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-325">During hello publishing process, you specify hello uniform resource identifiers (URIs) that lead tooeach of hello VHDs you have created for your SKU.</span></span> <span data-ttu-id="8b37e-326">Microsoft은 hello 인증 프로세스 중 액세스 toothese Vhd 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-326">Microsoft needs access toothese VHDs during hello certification process.</span></span> <span data-ttu-id="8b37e-327">따라서 각 VHD에 대 한 공유 액세스 서명 URI toocreate 필요.</span><span class="sxs-lookup"><span data-stu-id="8b37e-327">Therefore, you need toocreate a shared access signature URI for each VHD.</span></span> <span data-ttu-id="8b37e-328">이 hello에 입력 해야 하는 URI는 **이미지** hello 게시 포털에서에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-328">This is hello URI that should be entered in the **Images** tab in hello Publishing Portal.</span></span>

<span data-ttu-id="8b37e-329">hello 공유 액세스 서명 URI 생성 toohello 요구 사항 준수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-329">hello shared access signature URI created should adhere toohello following requirements:</span></span>

* <span data-ttu-id="8b37e-330">VHD에 대한 공유 액세스 서명 URI를 생성할 때 나열 및 읽기 권한이면 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-330">When generating shared access signature URIs for your VHDs, List and Read­ permissions are sufficient.</span></span> <span data-ttu-id="8b37e-331">쓰기 또는 삭제 권한을 제공하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="8b37e-331">Do not provide Write or Delete access.</span></span>
* <span data-ttu-id="8b37e-332">액세스에 대 한 hello 기간 hello 공유 액세스 서명 URI를 만들 때 최소 3 주 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-332">hello duration for access should be a minimum of three (3) weeks from when hello shared access signature URI is created.</span></span>
* <span data-ttu-id="8b37e-333">UTC 시간, hello 현재 날짜를 전날 선택 hello에 대 한 toosafeguard 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-333">toosafeguard for UTC time, select hello day before hello current date.</span></span> <span data-ttu-id="8b37e-334">예를 들어 hello 현재 날짜는 2014 년 10 월 6 일 경우 2014 년 10 월 5를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-334">For example, if hello current date is October 6, 2014, select 10/5/2014.</span></span>

<span data-ttu-id="8b37e-335">SAS URL이 될 수 있습니다 여러 방법으로 tooshare VHD에 대해 생성 된 Azure Marketplace 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-335">SAS URL can be generated in multiple ways tooshare your VHD for Azure Marketplace.</span></span>
<span data-ttu-id="8b37e-336">다음 3 권장된 도구 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-336">Following are hello 3 recommended tools:</span></span>

1.  <span data-ttu-id="8b37e-337">Azure Storage 탐색기</span><span class="sxs-lookup"><span data-stu-id="8b37e-337">Azure Storage Explorer</span></span>
2.  <span data-ttu-id="8b37e-338">Microsoft Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="8b37e-338">Microsoft Storage Explorer</span></span>
3.  <span data-ttu-id="8b37e-339">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8b37e-339">Azure CLI</span></span>

<span data-ttu-id="8b37e-340">**Azure Storage Explorer(Windows 사용자에 대해 권장됨)**</span><span class="sxs-lookup"><span data-stu-id="8b37e-340">**Azure Storage Explorer (Recommended for Windows Users)**</span></span>

<span data-ttu-id="8b37e-341">다음은 Azure 저장소 탐색기를 사용 하 여 SAS URL을 생성 하기 위한 hello 단계</span><span class="sxs-lookup"><span data-stu-id="8b37e-341">Following are hello steps for generating SAS URL by using Azure Storage Explorer</span></span>

1. <span data-ttu-id="8b37e-342">CodePlex에서 [Azure Storage Explorer 6 미리 보기 3](https://azurestorageexplorer.codeplex.com/)을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-342">Download [Azure Storage Explorer 6 Preview 3](https://azurestorageexplorer.codeplex.com/) from CodePlex.</span></span> <span data-ttu-id="8b37e-343">너무 이동[Azure 저장소 탐색기 6 미리 보기](https://azurestorageexplorer.codeplex.com/) 클릭 **"다운로드"**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-343">Go too[Azure Storage Explorer 6 Preview](https://azurestorageexplorer.codeplex.com/) and click **"Downloads"**.</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_01.png)

2. <span data-ttu-id="8b37e-345">[AzureStorageExplorer6Preview3.zip](https://azurestorageexplorer.codeplex.com/downloads/get/891668)을 다운로드하고 압축을 푼 후에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-345">Download [AzureStorageExplorer6Preview3.zip](https://azurestorageexplorer.codeplex.com/downloads/get/891668) and install after unzipping it.</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_02.png)

3. <span data-ttu-id="8b37e-347">설치 된 후 hello 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-347">After it is installed, open hello application.</span></span>
4. <span data-ttu-id="8b37e-348">**계정 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-348">Click **Add Account**.</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_03.png)

5. <span data-ttu-id="8b37e-350">Hello 저장소 계정 이름, 저장소 계정 키 및 저장소 끝점 도메인을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-350">Specify hello storage account name, storage account key, and storage endpoints domain.</span></span> <span data-ttu-id="8b37e-351">Azure 포털에서 VHD를 유지 한 있는 Azure 구독에서 hello 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-351">This is hello storage account in your Azure subscription where you have kept your VHD on Azure portal.</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_04.png)

6. <span data-ttu-id="8b37e-353">Azure 저장소 탐색기 연결 tooyour 특정 저장소 계정을 보여 주는 hello 저장소 계정 내에서 포함 된 모든 hello 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-353">Once Azure Storage Explorer is connected tooyour specific storage account, it will start showing all of hello contains within hello storage account.</span></span> <span data-ttu-id="8b37e-354">Hello 운영 체제 디스크 VHD 파일 (또한 데이터 디스크 시나리오에 적용할 수 있는 경우)를 복사 했던 hello 컨테이너를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-354">Select hello container where you copied hello operating system disk VHD file (also data disks if they are applicable for your scenario).</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_05.png)

7. <span data-ttu-id="8b37e-356">Hello blob 컨테이너를 선택한 후 Azure 저장소 탐색기는 hello 컨테이너 내에서 표시 된 hello 파일을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-356">After selecting hello blob container, Azure Storage Explorer starts showing hello files within hello container.</span></span> <span data-ttu-id="8b37e-357">제출 된 toobe 필요한 hello 이미지 파일 (.vhd)를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-357">Select hello image file (.vhd) that needs toobe submitted.</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_06.png)

8.  <span data-ttu-id="8b37e-359">Hello 컨테이너에서 hello.vhd 파일을 선택한 다음 클릭 hello **보안** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-359">After selecting hello .vhd file in hello container, click hello **Security** tab.</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_07.png)

9.  <span data-ttu-id="8b37e-361">Hello에 **Blob 컨테이너 보안** 대화 상자, hello에서 leave hello 기본값 **액세스 수준을** 탭을 클릭 한 다음 **공유 액세스 서명** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-361">In hello **Blob Container Security** dialog box, leave hello defaults on hello **Access Level** tab, and then click **Shared Access Signatures** tab.</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_08.png)

10. <span data-ttu-id="8b37e-363">Toogenerate hello.vhd 이미지에 대 한 공유 액세스 서명 URI 아래 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-363">Follow hello steps below toogenerate a shared access signature URI for hello .vhd image:</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_09.png)

    <span data-ttu-id="8b37e-365">a.</span><span class="sxs-lookup"><span data-stu-id="8b37e-365">a.</span></span> <span data-ttu-id="8b37e-366">**액세스를 허용:** toosafeguard UTC 시간은 선택 hello 전날 hello 현재 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-366">**Access permitted from:** toosafeguard for UTC time, select hello day before hello current date.</span></span> <span data-ttu-id="8b37e-367">예를 들어 hello 현재 날짜는 2014 년 10 월 6 일 경우 2014 년 10 월 5를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-367">For example, if hello current date is October 6, 2014, select 10/5/2014.</span></span>

    <span data-ttu-id="8b37e-368">b.</span><span class="sxs-lookup"><span data-stu-id="8b37e-368">b.</span></span> <span data-ttu-id="8b37e-369">**에 대 한 액세스가 허용:** hello 후 3 주 이상 된 날짜를 선택 **에서 액세스를 허용** 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-369">**Access permitted to:** Select a date that is at least 3 weeks after hello **Access permitted from** date.</span></span>

    <span data-ttu-id="8b37e-370">c.</span><span class="sxs-lookup"><span data-stu-id="8b37e-370">c.</span></span> <span data-ttu-id="8b37e-371">**허용 된 작업:** 선택 hello **목록** 및 **읽기** 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="8b37e-371">**Actions permitted:** Select hello **List** and **Read** permissions.</span></span>

    <span data-ttu-id="8b37e-372">d.</span><span class="sxs-lookup"><span data-stu-id="8b37e-372">d.</span></span> <span data-ttu-id="8b37e-373">.Vhd 파일 올바르게를 선택한 경우에 프로그램 파일이 나타납니다 **Blob 이름 tooaccess** 확장.vhd를 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-373">If you have selected your .vhd file correctly, then your file appears in **Blob name tooaccess** with extension .vhd.</span></span>

    <span data-ttu-id="8b37e-374">e.</span><span class="sxs-lookup"><span data-stu-id="8b37e-374">e.</span></span> <span data-ttu-id="8b37e-375">**서명 생성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-375">Click **Generate Signature**.</span></span>

    <span data-ttu-id="8b37e-376">f.</span><span class="sxs-lookup"><span data-stu-id="8b37e-376">f.</span></span> <span data-ttu-id="8b37e-377">**생성 된 공유 액세스 서명 URI이이 컨테이너의**, 위에 강조 표시 된 대로 다음 hello에 대 한 확인:</span><span class="sxs-lookup"><span data-stu-id="8b37e-377">In **Generated Shared Access Signature URI of this container**, check for hello following as highlighted above:</span></span>

       - <span data-ttu-id="8b37e-378">이미지 파일 이름 있는지 확인 하 고 **".vhd"** hello URI에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-378">Make sure that your image file name and **".vhd"** are in hello URI.</span></span>
       - <span data-ttu-id="8b37e-379">Hello 서명의 hello 끝에 있는지 확인 하는 **"rl ="** 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-379">At hello end of hello signature, make sure that **"=rl"** appears.</span></span> <span data-ttu-id="8b37e-380">이는 읽기 및 나열 액세스가 성공적으로 제공되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-380">This demonstrates that Read and List access was provided successfully.</span></span>
       - <span data-ttu-id="8b37e-381">Hello 서명의 중간 되는지 확인 **"sr = c"** 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-381">In middle of hello signature, make sure that **"sr=c"** appears.</span></span> <span data-ttu-id="8b37e-382">컨테이너 수준 액세스 권한이 있는지 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-382">This demonstrates that you have container level access</span></span>

11. <span data-ttu-id="8b37e-383">생성 된 hello tooensure 공유 액세스 서명 URI works, 클릭 **브라우저에서 테스트**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-383">tooensure that hello generated shared access signature URI works, click **Test in Browser**.</span></span> <span data-ttu-id="8b37e-384">그 hello 다운로드 프로세스를 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-384">It should start hello download process.</span></span>

12. <span data-ttu-id="8b37e-385">Hello 공유 액세스 서명 URI를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-385">Copy hello shared access signature URI.</span></span> <span data-ttu-id="8b37e-386">이 hello 게시 포털에 hello URI toopaste입니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-386">This is hello URI toopaste into hello Publishing Portal.</span></span>

13. <span data-ttu-id="8b37e-387">Hello SKU의에서 각 VHD에 대 한 6-10 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-387">Repeat steps 6-10 for each VHD in hello SKU.</span></span>

<span data-ttu-id="8b37e-388">**Microsoft Azure Storage Explorer(Windows/MAC/Linux)**</span><span class="sxs-lookup"><span data-stu-id="8b37e-388">**Microsoft Azure Storage Explorer (Windows/MAC/Linux)**</span></span>

<span data-ttu-id="8b37e-389">다음은 Microsoft Azure 저장소 탐색기를 사용 하 여 SAS URL을 생성 하기 위한 hello 단계</span><span class="sxs-lookup"><span data-stu-id="8b37e-389">Following are hello steps for generating SAS URL by using Microsoft Azure Storage Explorer</span></span>

1.  <span data-ttu-id="8b37e-390">[http://storageexplorer.com/](http://storageexplorer.com/) 웹 사이트에서 Microsoft Azure Storage Explorer를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-390">Download Microsoft Azure Storage Explorer form [http://storageexplorer.com/](http://storageexplorer.com/) website.</span></span> <span data-ttu-id="8b37e-391">너무 이동[Microsoft Azure 저장소 탐색기](http://storageexplorer.com/releasenotes.html) 클릭 **"Windows 용 다운로드"**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-391">Go too[Microsoft Azure Storage Explorer](http://storageexplorer.com/releasenotes.html) and click **“Download for Windows”**.</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_10.png)

2.  <span data-ttu-id="8b37e-393">설치 된 후 hello 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-393">After it is installed, open hello application.</span></span>

3.  <span data-ttu-id="8b37e-394">**계정 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-394">Click **Add Account**.</span></span>

4.  <span data-ttu-id="8b37e-395">Tooyour 계정에 로그인 하 여 Microsoft Azure 저장소 탐색기 tooyour 구독 구성</span><span class="sxs-lookup"><span data-stu-id="8b37e-395">Configure Microsoft Azure Storage Explorer tooyour subscription by sign in tooyour account</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_11.png)

5.  <span data-ttu-id="8b37e-397">Toostorage 계정을 이동 하 고 hello 컨테이너를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-397">Go toostorage account and select hello Container</span></span>

6.  <span data-ttu-id="8b37e-398">**"공유 액세스 서명 가져오기"**를</span><span class="sxs-lookup"><span data-stu-id="8b37e-398">Select **“Get Share Access Signature..”**</span></span> <span data-ttu-id="8b37e-399">마우스 오른쪽 단추로 클릭의 hello 사용 하 여 **컨테이너**</span><span class="sxs-lookup"><span data-stu-id="8b37e-399">by using Right Click of hello **container**</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_12.png)

7.  <span data-ttu-id="8b37e-401">다음에 따른 업데이트 시작 시간, 만료 시간 및 사용 권한</span><span class="sxs-lookup"><span data-stu-id="8b37e-401">Update Start time, Expiry time and Permissions as per following</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_13.png)

    <span data-ttu-id="8b37e-403">a.</span><span class="sxs-lookup"><span data-stu-id="8b37e-403">a.</span></span>  <span data-ttu-id="8b37e-404">**시작 시간:** toosafeguard UTC 시간은 선택 hello 전날 hello 현재 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-404">**Start Time:** toosafeguard for UTC time, select hello day before hello current date.</span></span> <span data-ttu-id="8b37e-405">예를 들어 hello 현재 날짜는 2014 년 10 월 6 일 경우 2014 년 10 월 5를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-405">For example, if hello current date is October 6, 2014, select 10/5/2014.</span></span>

    <span data-ttu-id="8b37e-406">b.</span><span class="sxs-lookup"><span data-stu-id="8b37e-406">b.</span></span>  <span data-ttu-id="8b37e-407">**만료 시간:** hello 후 3 주 이상 된 날짜를 선택 **시작 시간** 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-407">**Expiry Time:** Select a date that is at least 3 weeks after hello **Start Time** date.</span></span>

    <span data-ttu-id="8b37e-408">c.</span><span class="sxs-lookup"><span data-stu-id="8b37e-408">c.</span></span>  <span data-ttu-id="8b37e-409">**사용 권한:** 선택 hello **목록** 및 **읽기** 사용 권한</span><span class="sxs-lookup"><span data-stu-id="8b37e-409">**Permissions:** Select hello **List** and **Read** permissions</span></span>

8.  <span data-ttu-id="8b37e-410">컨테이너 공유 액세스 서명 URI를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-410">Copy Container shared access signature URI</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_14.png)

    <span data-ttu-id="8b37e-412">컨테이너 수준에 대 한 생성 된 SAS URL 이며 이제 내부에 tooadd VHD 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-412">Generated SAS URL is for container Level and now we need tooadd VHD name in it.</span></span>

    <span data-ttu-id="8b37e-413">컨테이너 수준 SAS URL의 형식:`https://testrg009.blob.core.windows.net/vhds?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span><span class="sxs-lookup"><span data-stu-id="8b37e-413">Format of Container Level SAS URL: `https://testrg009.blob.core.windows.net/vhds?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span></span>

    <span data-ttu-id="8b37e-414">아래와 같이 SAS URL에 hello 컨테이너 이름 뒤에 오는 VHD 이름 삽입`https://testrg009.blob.core.windows.net/vhds/<VHD NAME>?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span><span class="sxs-lookup"><span data-stu-id="8b37e-414">Insert VHD name after hello container name in SAS URL as below `https://testrg009.blob.core.windows.net/vhds/<VHD NAME>?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span></span>

    <span data-ttu-id="8b37e-415">예제:</span><span class="sxs-lookup"><span data-stu-id="8b37e-415">Example:</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_15.png)

    <span data-ttu-id="8b37e-417">VHD SAS URL이 됩니다 TestRGVM201631920152.vhd는 hello VHD 이름`https://testrg009.blob.core.windows.net/vhds/TestRGVM201631920152.vhd?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span><span class="sxs-lookup"><span data-stu-id="8b37e-417">TestRGVM201631920152.vhd is hello VHD Name then VHD SAS URL will be `https://testrg009.blob.core.windows.net/vhds/TestRGVM201631920152.vhd?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span></span>

    - <span data-ttu-id="8b37e-418">이미지 파일 이름 있는지 확인 하 고 **".vhd"** hello URI에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-418">Make sure that your image file name and **".vhd"** are in hello URI.</span></span>
    - <span data-ttu-id="8b37e-419">Hello 서명의 중간 되는지 확인 **"sp = rl"** 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-419">In middle of hello signature, make sure that **"sp=rl"** appears.</span></span> <span data-ttu-id="8b37e-420">이는 읽기 및 나열 액세스가 성공적으로 제공되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-420">This demonstrates that Read and List access was provided successfully.</span></span>
    - <span data-ttu-id="8b37e-421">Hello 서명의 중간 되는지 확인 **"sr = c"** 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-421">In middle of hello signature, make sure that **"sr=c"** appears.</span></span> <span data-ttu-id="8b37e-422">컨테이너 수준 액세스 권한이 있는지 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-422">This demonstrates that you have container level access</span></span>

9.  <span data-ttu-id="8b37e-423">생성 된 공유 액세스 서명 URI works hello tooensure 브라우저에서 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-423">tooensure that hello generated shared access signature URI works, test it in browser.</span></span> <span data-ttu-id="8b37e-424">Hello 다운로드 프로세스를 시작 해야</span><span class="sxs-lookup"><span data-stu-id="8b37e-424">It should start hello download process</span></span>

10. <span data-ttu-id="8b37e-425">Hello 공유 액세스 서명 URI를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-425">Copy hello shared access signature URI.</span></span> <span data-ttu-id="8b37e-426">이 hello 게시 포털에 hello URI toopaste입니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-426">This is hello URI toopaste into hello Publishing Portal.</span></span>

11. <span data-ttu-id="8b37e-427">Hello SKU의에서 각 VHD에 대 한 이러한 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-427">Repeat these steps for each VHD in hello SKU.</span></span>

<span data-ttu-id="8b37e-428">**Azure CLI(Windows가 아닌 연속 통합에 권장됨)**</span><span class="sxs-lookup"><span data-stu-id="8b37e-428">**Azure CLI (Recommended for Non-Windows & Continuous Integration)**</span></span>

<span data-ttu-id="8b37e-429">다음은 Azure CLI를 사용 하 여 SAS URL을 생성 하기 위한 hello 단계</span><span class="sxs-lookup"><span data-stu-id="8b37e-429">Following are hello steps for generating SAS URL by using Azure CLI</span></span>

1.  <span data-ttu-id="8b37e-430">Microsoft Azure CLI를 [여기](https://azure.microsoft.com/en-in/documentation/articles/xplat-cli-install/)에서 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-430">Download Microsoft Azure CLI from [here](https://azure.microsoft.com/en-in/documentation/articles/xplat-cli-install/).</span></span> <span data-ttu-id="8b37e-431">**[Windows](http://aka.ms/webpi-azure-cli)** 및 **[MAC OS](http://aka.ms/mac-azure-cli)**에 대한 다양한 링크를 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-431">You can also find different links for **[Windows](http://aka.ms/webpi-azure-cli)** and **[MAC OS](http://aka.ms/mac-azure-cli)**.</span></span>

2.  <span data-ttu-id="8b37e-432">다운로드되면 설치하세요.</span><span class="sxs-lookup"><span data-stu-id="8b37e-432">Once it is downloaded, please install</span></span>

3.  <span data-ttu-id="8b37e-433">다음 코드를 사용하여 PowerShell 파일을 만들고 로컬에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-433">Create a PowerShell file with following code and save it in local</span></span>

          $conn="DefaultEndpointsProtocol=https;AccountName=<StorageAccountName>;AccountKey=<Storage Account Key>"
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl <Permission End Date> -c $conn --start <Permission Start Date>  

    <span data-ttu-id="8b37e-434">Hello 다음 업데이트에서 매개 변수 위에</span><span class="sxs-lookup"><span data-stu-id="8b37e-434">Update hello following parameters in above</span></span>

    <span data-ttu-id="8b37e-435">a.</span><span class="sxs-lookup"><span data-stu-id="8b37e-435">a.</span></span> <span data-ttu-id="8b37e-436">**`<StorageAccountName>`**: 저장소 계정 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-436">**`<StorageAccountName>`**: Give your storage account name</span></span>

    <span data-ttu-id="8b37e-437">b.</span><span class="sxs-lookup"><span data-stu-id="8b37e-437">b.</span></span> <span data-ttu-id="8b37e-438">**`<Storage Account Key>`**: 저장소 계정 키를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-438">**`<Storage Account Key>`**: Give your storage account key</span></span>

    <span data-ttu-id="8b37e-439">c.</span><span class="sxs-lookup"><span data-stu-id="8b37e-439">c.</span></span> <span data-ttu-id="8b37e-440">**`<Permission Start Date>`**: toosafeguard UTC 시간은 선택 hello 전날 hello 현재 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-440">**`<Permission Start Date>`**: toosafeguard for UTC time, select hello day before hello current date.</span></span> <span data-ttu-id="8b37e-441">예를 들어 hello 현재 날짜가 2016 년 10 월 26 일 경우 값은 여야 2016 년 10 월 25 일</span><span class="sxs-lookup"><span data-stu-id="8b37e-441">For example, if hello current date is October 26, 2016, then value should be 10/25/2016</span></span>

    <span data-ttu-id="8b37e-442">d.</span><span class="sxs-lookup"><span data-stu-id="8b37e-442">d.</span></span> <span data-ttu-id="8b37e-443">**`<Permission End Date>`**: Hello 후 3 주까지 이상 되는 날짜를 선택 합니다. **시작 날짜**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-443">**`<Permission End Date>`**: Select a date that is at least 3 weeks after hello **Start Date**.</span></span> <span data-ttu-id="8b37e-444">값은 **2016/11/02**이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-444">Then value should be **11/02/2016**.</span></span>

    <span data-ttu-id="8b37e-445">다음은 적절 한 매개 변수를 업데이트 한 후 hello 예제 코드</span><span class="sxs-lookup"><span data-stu-id="8b37e-445">Following is hello example code after updating proper parameters</span></span>

          $conn="DefaultEndpointsProtocol=https;AccountName=st20151;AccountKey=TIQE5QWMKHpT5q2VnF1bb+NUV7NVMY2xmzVx1rdgIVsw7h0pcI5nMM6+DVFO65i4bQevx21dmrflA91r0Vh2Yw=="
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl 11/02/2016 -c $conn --start 10/25/2016  

4.  <span data-ttu-id="8b37e-446">"관리자 권한으로 실행" 모드로 Powershell 편집기를 열고 3단계에서 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-446">Open Powershell editor with “Run as Administrator” mode and open file in step #3.</span></span>

5.  <span data-ttu-id="8b37e-447">실행된 hello 스크립트와 해당 컨테이너 수준 액세스에 대 한 SAS URL을 hello 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-447">Run hello script and it will provide you hello SAS URL for container level access</span></span>

    <span data-ttu-id="8b37e-448">다음과 같은 hello SAS 서명 및 복사 강조 표시 하는 hello-메모장에서의 hello 출력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-448">Following will be hello output of hello SAS Signature and copy hello highlighted part in a notepad</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/img5.2_16.png)

6.  <span data-ttu-id="8b37e-450">컨테이너 수준 SAS URL을 이제 얻게 됩니다 및 그 안에 tooadd VHD 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-450">Now you will get container level SAS URL and you need tooadd VHD name in it.</span></span>

    <span data-ttu-id="8b37e-451">컨테이너 수준 SAS URL #</span><span class="sxs-lookup"><span data-stu-id="8b37e-451">Container level SAS URL #</span></span>

    `https://st20151.blob.core.windows.net/vhds?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

7.  <span data-ttu-id="8b37e-452">아래 표시 된 대로 SAS URL에 hello 컨테이너 이름 뒤에 오는 VHD 이름 삽입`https://st20151.blob.core.windows.net/vhds/<VHDName>?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`</span><span class="sxs-lookup"><span data-stu-id="8b37e-452">Insert VHD name after hello container name in SAS URL as shown below `https://st20151.blob.core.windows.net/vhds/<VHDName>?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`</span></span>

    <span data-ttu-id="8b37e-453">예제:</span><span class="sxs-lookup"><span data-stu-id="8b37e-453">Example:</span></span>

    <span data-ttu-id="8b37e-454">VHD SAS URL이 됩니다 TestRGVM201631920152.vhd는 hello VHD 이름</span><span class="sxs-lookup"><span data-stu-id="8b37e-454">TestRGVM201631920152.vhd is hello VHD Name then VHD SAS URL will be</span></span>

    `https://st20151.blob.core.windows.net/vhds/ TestRGVM201631920152.vhd?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

    - <span data-ttu-id="8b37e-455">이미지 파일 이름 및 ".vhd" hello URI에에서 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-455">Make sure that your image file name and ".vhd" are in hello URI.</span></span>
    -   <span data-ttu-id="8b37e-456">Hello 서명의 중간에 있는지 확인 하는 "sp = rl" 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-456">In middle of hello signature, make sure that "sp=rl" appears.</span></span> <span data-ttu-id="8b37e-457">이는 읽기 및 나열 액세스가 성공적으로 제공되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-457">This demonstrates that Read and List access was provided successfully.</span></span>
    -   <span data-ttu-id="8b37e-458">Hello 서명의 중간에 있는지 확인 하는 "s r c =" 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-458">In middle of hello signature, make sure that "sr=c" appears.</span></span> <span data-ttu-id="8b37e-459">컨테이너 수준 액세스 권한이 있는지 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-459">This demonstrates that you have container level access</span></span>

8.  <span data-ttu-id="8b37e-460">생성 된 공유 액세스 서명 URI works hello tooensure 브라우저에서 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-460">tooensure that hello generated shared access signature URI works, test it in browser.</span></span> <span data-ttu-id="8b37e-461">Hello 다운로드 프로세스를 시작 해야</span><span class="sxs-lookup"><span data-stu-id="8b37e-461">It should start hello download process</span></span>

9.  <span data-ttu-id="8b37e-462">Hello 공유 액세스 서명 URI를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-462">Copy hello shared access signature URI.</span></span> <span data-ttu-id="8b37e-463">이 hello 게시 포털에 hello URI toopaste입니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-463">This is hello URI toopaste into hello Publishing Portal.</span></span>

10. <span data-ttu-id="8b37e-464">Hello SKU의에서 각 VHD에 대 한 이러한 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-464">Repeat these steps for each VHD in hello SKU.</span></span>


### <a name="53-provide-information-about-hello-vm-image-and-request-certification-in-hello-publishing-portal"></a><span data-ttu-id="8b37e-465">5.3 hello VM 이미지에 대 한 정보를 제공 하 고 hello 게시 포털에서에서 인증 요청</span><span class="sxs-lookup"><span data-stu-id="8b37e-465">5.3 Provide information about hello VM image and request certification in hello Publishing Portal</span></span>
<span data-ttu-id="8b37e-466">제안 및 SKU를 만든 후 해당 SKU와 연결 된 hello 이미지 세부 정보를 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-466">After you have created your offer and SKU, you should enter hello image details associated with that SKU:</span></span>

1. <span data-ttu-id="8b37e-467">Toohello 이동 [게시 포털][link-pubportal], 한 다음 판매자 계정으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-467">Go toohello [Publishing Portal][link-pubportal], and then sign in with your seller account.</span></span>
2. <span data-ttu-id="8b37e-468">선택 hello **VM 이미지** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-468">Select hello **VM images** tab.</span></span>
3. <span data-ttu-id="8b37e-469">hello hello 페이지 위쪽에 나열 된 hello 식별자가 실제로 hello 제품 식별자 및 hello SKU 식별자가 아닌 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-469">hello identifier listed at hello top of hello page is actually hello offer identifier and not hello SKU identifier.</span></span>
4. <span data-ttu-id="8b37e-470">Hello 아래의 hello 속성을 채울 **Sku** 섹션.</span><span class="sxs-lookup"><span data-stu-id="8b37e-470">Fill out hello properties under hello **SKUs** section.</span></span>
5. <span data-ttu-id="8b37e-471">아래 **운영 체제 제품군**, hello 운영 체제 VHD와 연결 된 hello 운영 체제 유형을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-471">Under **Operating system family**, click hello operating system type associated with hello operating system VHD.</span></span>
6. <span data-ttu-id="8b37e-472">Hello에 **운영 체제** hello 운영 체제를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-472">In hello **Operating system** box, describe hello operating system.</span></span> <span data-ttu-id="8b37e-473">운영 체제 제품군, 유형, 버전, 업데이트 등과 같은 형식을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="8b37e-473">Consider a format such as operating system family, type, version, and updates.</span></span> <span data-ttu-id="8b37e-474">예를 들어 "Windows Server Datacenter 2014 R2"를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-474">An example is "Windows Server Datacenter 2014 R2."</span></span>
7. <span data-ttu-id="8b37e-475">가상 컴퓨터 크기를 권장 toosix를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-475">Select up toosix recommended virtual machine sizes.</span></span> <span data-ttu-id="8b37e-476">이들은 toopurchase 결정 하 고 사용자 이미지를 배포할 때 hello 가격 책정 계층 블레이드 hello Azure 포털에에서 표시 된 toohello 고객을 방해 하는 권장 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-476">These are recommendations that get displayed toohello customer in hello Pricing tier blade in hello Azure Portal when they decide toopurchase and deploy your image.</span></span> <span data-ttu-id="8b37e-477">**이들은 권장 사항일 뿐입니다. hello 고객 수 tooselect 이미지에 지정 된 hello 디스크를 제공 하는 모든 VM 크기입니다.**</span><span class="sxs-lookup"><span data-stu-id="8b37e-477">**These are only recommendations. hello customer is able tooselect any VM size that accommodates hello disks specified in your image.**</span></span>
8. <span data-ttu-id="8b37e-478">Hello 버전을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-478">Enter hello version.</span></span> <span data-ttu-id="8b37e-479">hello 버전 필드에 의미 체계의 버전 tooidentify hello 제품과 해당 업데이트가 캡슐화합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-479">hello version field encapsulates a semantic version tooidentify hello product and its updates:</span></span>
   * <span data-ttu-id="8b37e-480">버전은 hello x.y.z 형식이 며, X, Y 및 Z는 정수 형식 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-480">Versions should be of hello form X.Y.Z, where X, Y, and Z are integers.</span></span>
   * <span data-ttu-id="8b37e-481">다른 SKU에서 이미지는 다른 주 버전과 부 버전을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-481">Images in different SKUs can have different major and minor versions.</span></span>
   * <span data-ttu-id="8b37e-482">SKU에서 버전 hello 패치 버전 (Z x.y.z 형식이 며에서)를 늘리는 증분 변경만 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-482">Versions within a SKU should only be incremental changes, which increase hello patch version (Z from X.Y.Z).</span></span>
9. <span data-ttu-id="8b37e-483">Hello에 **OS VHD URL** 상자 hello 운영 체제 VHD에 대 한 URI를 만들 hello 공유 액세스 서명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-483">In hello **OS VHD URL** box, enter hello shared access signature URI created for hello operating system VHD.</span></span>
10. <span data-ttu-id="8b37e-484">이 SKU와 연결 된 데이터 디스크에 있는 경우 hello 논리 단위 번호 (LUN) toowhich 배포 시 탑재이 데이터 디스크 toobe 원하는 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-484">If there are data disks associated with this SKU, select hello logical unit number (LUN) toowhich you would like this data disk toobe mounted upon deployment.</span></span>
11. <span data-ttu-id="8b37e-485">Hello에 **LUN X VHD URL** 상자 hello 첫 번째 데이터 VHD에 대 한 URI를 만들 hello 공유 액세스 서명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-485">In hello **LUN X VHD URL** box, enter hello shared access signature URI created for hello first data VHD.</span></span>

    ![drawing](media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-3.png)


## <a name="common-sas-url-issues--fixes"></a><span data-ttu-id="8b37e-487">일반적인 SAS URL 문제 및 해결</span><span class="sxs-lookup"><span data-stu-id="8b37e-487">Common SAS URL issues & fixes</span></span>

|<span data-ttu-id="8b37e-488">문제</span><span class="sxs-lookup"><span data-stu-id="8b37e-488">Issue</span></span>|<span data-ttu-id="8b37e-489">오류 메시지</span><span class="sxs-lookup"><span data-stu-id="8b37e-489">Failure Message</span></span>|<span data-ttu-id="8b37e-490">해결</span><span class="sxs-lookup"><span data-stu-id="8b37e-490">Fix</span></span>|<span data-ttu-id="8b37e-491">문서 링크</span><span class="sxs-lookup"><span data-stu-id="8b37e-491">Documentation Link</span></span>|
|---|---|---|---|
|<span data-ttu-id="8b37e-492">이미지 복사 중 오류 - "?"가 SAS URL에 없습니다</span><span class="sxs-lookup"><span data-stu-id="8b37e-492">Failure in copying images - "?" is not found in SAS url</span></span>|<span data-ttu-id="8b37e-493">오류: 이미지 복사</span><span class="sxs-lookup"><span data-stu-id="8b37e-493">Failure: Copying Images.</span></span> <span data-ttu-id="8b37e-494">사용 하 여 수 없습니다. toodownload blob SAS Uri를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-494">Not able toodownload blob using provided SAS Uri.</span></span>|<span data-ttu-id="8b37e-495">도구를 사용 하 여 업데이트 hello SAS Url 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-495">Update hello SAS Url using recommended tools</span></span>|[<span data-ttu-id="8b37e-496">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span><span class="sxs-lookup"><span data-stu-id="8b37e-496">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="8b37e-497">이미지 복사 중 오류 - "st" 및 "se" 매개 변수가 SAS URL에 없습니다</span><span class="sxs-lookup"><span data-stu-id="8b37e-497">Failure in copying images - “st” and “se” parameters not in SAS url</span></span>|<span data-ttu-id="8b37e-498">오류: 이미지 복사</span><span class="sxs-lookup"><span data-stu-id="8b37e-498">Failure: Copying Images.</span></span> <span data-ttu-id="8b37e-499">사용 하 여 수 없습니다. toodownload blob SAS Uri를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-499">Not able toodownload blob using provided SAS Uri.</span></span>|<span data-ttu-id="8b37e-500">에 시작 및 끝 날짜가 hello SAS Url 업데이트</span><span class="sxs-lookup"><span data-stu-id="8b37e-500">Update hello SAS Url with Start and End dates on it</span></span>|[<span data-ttu-id="8b37e-501">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span><span class="sxs-lookup"><span data-stu-id="8b37e-501">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="8b37e-502">이미지 복사 중 오류 - “sp=rl”이 SAS URL에 없습니다</span><span class="sxs-lookup"><span data-stu-id="8b37e-502">Failure in copying images - “sp=rl” not in SAS url</span></span>|<span data-ttu-id="8b37e-503">오류: 이미지 복사</span><span class="sxs-lookup"><span data-stu-id="8b37e-503">Failure: Copying Images.</span></span> <span data-ttu-id="8b37e-504">제공 된 SAS Uri를 사용 하 여 toodownload 수 없습니다. blob</span><span class="sxs-lookup"><span data-stu-id="8b37e-504">Not able toodownload blob using provided SAS Uri</span></span>|<span data-ttu-id="8b37e-505">"읽기" 및 "목록으로 설정 하는 권한이 있는 hello SAS Url을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-505">Update hello SAS Url with permissions set as “Read” & “List</span></span>|[<span data-ttu-id="8b37e-506">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span><span class="sxs-lookup"><span data-stu-id="8b37e-506">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="8b37e-507">이미지 복사 중 오류 - SAS URL은 VHD 이름에 공백을 포함합니다</span><span class="sxs-lookup"><span data-stu-id="8b37e-507">Failure in copying images - SAS url have white spaces in vhd name</span></span>|<span data-ttu-id="8b37e-508">오류: 이미지 복사</span><span class="sxs-lookup"><span data-stu-id="8b37e-508">Failure: Copying Images.</span></span> <span data-ttu-id="8b37e-509">사용 하 여 수 없습니다. toodownload blob SAS Uri를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-509">Not able toodownload blob using provided SAS Uri.</span></span>|<span data-ttu-id="8b37e-510">공백 없이 hello SAS Url을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-510">Update hello SAS Url without white spaces</span></span>|[<span data-ttu-id="8b37e-511">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span><span class="sxs-lookup"><span data-stu-id="8b37e-511">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="8b37e-512">이미지 복사 중 오류 – SAS URL 권한 부여 오류</span><span class="sxs-lookup"><span data-stu-id="8b37e-512">Failure in copying images – SAS Url Authorization error</span></span>|<span data-ttu-id="8b37e-513">오류: 이미지 복사</span><span class="sxs-lookup"><span data-stu-id="8b37e-513">Failure: Copying Images.</span></span> <span data-ttu-id="8b37e-514">Tooauthorization 오류 인해 수 없습니다. toodownload blob</span><span class="sxs-lookup"><span data-stu-id="8b37e-514">Not able toodownload blob due tooauthorization error</span></span>|<span data-ttu-id="8b37e-515">Hello SAS Url을 다시 생성</span><span class="sxs-lookup"><span data-stu-id="8b37e-515">Regenerate hello SAS Url</span></span>|[<span data-ttu-id="8b37e-516">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span><span class="sxs-lookup"><span data-stu-id="8b37e-516">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|


## <a name="next-step"></a><span data-ttu-id="8b37e-517">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8b37e-517">Next step</span></span>
<span data-ttu-id="8b37e-518">Hello SKU 세부 정보를 완료 한 후에 앞으로 toohello을 이동할 수 있습니다 [Azure 마켓플레이스 마케팅 콘텐츠 가이드][link-pushstaging]합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-518">After you are done with hello SKU details, you can move forward toohello [Azure Marketplace marketing content guide][link-pushstaging].</span></span> <span data-ttu-id="8b37e-519">콘텐츠, 가격 및 기타 정보 필요한 전에 너무 마케팅 hello hello 게시 프로세스의 해당 단계에서 제공한**3 단계: 준비 단계에 제공 VM 테스트**배포 하기 전에 다양 한 사용 사례 시나리오를 테스트할 있습니다, 공용 표시 여부에 대 한 제안을 toohello Azure 마켓플레이스 hello 및 구매 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b37e-519">In that step of hello publishing process, you provide hello marketing content, pricing, and other information necessary prior too**Step 3: Testing your VM offer in staging**, where you test various use-case scenarios before deploying hello offer toohello Azure Marketplace for public visibility and purchase.</span></span>  

## <a name="see-also"></a><span data-ttu-id="8b37e-520">참고 항목</span><span class="sxs-lookup"><span data-stu-id="8b37e-520">See also</span></span>
* [<span data-ttu-id="8b37e-521">시작 하기: 어떻게 toopublish 제안 toohello Azure 마켓플레이스</span><span class="sxs-lookup"><span data-stu-id="8b37e-521">Getting started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

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
