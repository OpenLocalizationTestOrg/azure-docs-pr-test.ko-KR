---
title: "Azure 가상 네트워크 (클래식)를 여러 서브넷 aaaCreate | Microsoft Docs"
description: "자세한 내용은 방법 toocreate Azure에서 다중 서브넷 가상 네트워크 (클래식)."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: cc7b9ad08d5c26dba09584762bedf614d2847032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-classic-with-multiple-subnets"></a><span data-ttu-id="dfe54-103">여러 서브넷이 있는 가상 네트워크(클래식) 만들기</span><span class="sxs-lookup"><span data-stu-id="dfe54-103">Create a virtual network (classic) with multiple subnets</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dfe54-104">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-104">Azure has two [different deployment models](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) for creating and working with resources: Resource Manager and classic.</span></span> <span data-ttu-id="dfe54-105">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="dfe54-106">Hello 통해 대부분 새 가상 네트워크를 만드는 것이 좋습니다 [리소스 관리자](virtual-networks-create-vnet-arm-pportal.md) 배포 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-106">Microsoft recommends creating most new virtual networks through hello [Resource Manager](virtual-networks-create-vnet-arm-pportal.md) deployment model.</span></span>

<span data-ttu-id="dfe54-107">이 자습서에서는 toocreate 기본 Azure 가상 네트워크 (클래식)가 공용 및 개인 서브넷을 분리 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-107">In this tutorial, learn how toocreate a basic Azure virtual network (classic) that has separate public and private subnets.</span></span> <span data-ttu-id="dfe54-108">Virtual Machines 및 서브넷에 있는 Cloud Services와 같은 Azure 리소스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-108">You can create Azure resources, like Virtual machines and Cloud services in a subnet.</span></span> <span data-ttu-id="dfe54-109">가상 네트워크 (클래식)에서 생성 된 리소스는 서로 다른 네트워크 연결 된 tooa 가상 네트워크의 리소스와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-109">Resources created in virtual networks (classic) can communicate with each other, and with resources in other networks connected tooa virtual network.</span></span>

<span data-ttu-id="dfe54-110">모든 [가상 네트워크](virtual-network-manage-network.md) 및 [서브넷](virtual-network-manage-subnet.md) 설정에 대해 자세히 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="dfe54-110">Learn more about all [virtual network](virtual-network-manage-network.md) and [subnet](virtual-network-manage-subnet.md) settings.</span></span>

> [!WARNING]
> <span data-ttu-id="dfe54-111">[구독이 비활성화되는](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit) 경우 Azure에서 가상 네트워크(클래식)가 즉시 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-111">Virtual networks (classic) are immediately deleted by Azure when a [subscription is disabled](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit).</span></span> <span data-ttu-id="dfe54-112">가상 네트워크 (클래식) 리소스는 hello 가상 네트워크에 존재 하는지 여부에 관계 없이 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-112">Virtual networks (classic) are deleted regardless of whether resources exist in hello virtual network.</span></span> <span data-ttu-id="dfe54-113">나중에 다시 사용 하면 hello 구독, hello 가상 네트워크에 존재 하는 리소스를 다시 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-113">If you later re-enable hello subscription, resources that existed in hello virtual network must be recreated.</span></span>

<span data-ttu-id="dfe54-114">Hello를 사용 하 여 가상 네트워크 (클래식)를 만들 수 있습니다 [Azure 포털](#portal), hello [Azure CLI (명령줄 인터페이스) 1.0](#azure-cli), 또는 [PowerShell](#powershell)합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-114">You can create a virtual network (classic) by using hello [Azure portal](#portal), hello [Azure command-line interface (CLI) 1.0](#azure-cli), or [PowerShell](#powershell).</span></span>

## <a name="portal"></a><span data-ttu-id="dfe54-115">포털</span><span class="sxs-lookup"><span data-stu-id="dfe54-115">Portal</span></span>

1. <span data-ttu-id="dfe54-116">인터넷 브라우저를 이동 toohello [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-116">In an Internet browser, go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="dfe54-117">[Azure 계정](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-117">Log in using your [Azure account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="dfe54-118">Azure 계정이 없으면 [무료 평가판](https://azure.microsoft.com/offers/ms-azr-0044p)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-118">If you don't have an Azure account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="dfe54-119">클릭 **+ 새로 만들기** hello 포털에서입니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-119">Click **+New** in hello portal.</span></span>
3. <span data-ttu-id="dfe54-120">입력 *가상 네트워크* hello에 **검색 hello 마켓플레이스** hello의 hello 상단 상자 **새로 만들기** 블레이드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-120">Enter *Virtual network* in hello **Search hello Marketplace** box at hello top of hello **New** blade that appears.</span></span>  <span data-ttu-id="dfe54-121">클릭 **가상 네트워크** hello 검색 결과에 표시 되 면입니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-121">Click **Virtual network** when it appears in hello search results.</span></span>
4. <span data-ttu-id="dfe54-122">선택 **클래식** hello에 **배포 모델 선택** 상자 hello에 **가상 네트워크** 블레이드를 놓고 클릭 한 다음 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-122">Select **Classic** in hello **Select a deployment model** box in hello **Virtual Network** blade that appears, then click **Create**.</span></span> 
5. <span data-ttu-id="dfe54-123">입력 값에 나오는 hello에 hello **가상 네트워크 만들기 (클래식)** 블레이드에 대 한 클릭 **만들기**:</span><span class="sxs-lookup"><span data-stu-id="dfe54-123">Enter hello following values on hello **Create virtual network (classic)** blade and then click **Create**:</span></span>

    |<span data-ttu-id="dfe54-124">설정</span><span class="sxs-lookup"><span data-stu-id="dfe54-124">Setting</span></span>|<span data-ttu-id="dfe54-125">값</span><span class="sxs-lookup"><span data-stu-id="dfe54-125">Value</span></span>|
    |---|---|
    |<span data-ttu-id="dfe54-126">이름</span><span class="sxs-lookup"><span data-stu-id="dfe54-126">Name</span></span>|<span data-ttu-id="dfe54-127">myVnet</span><span class="sxs-lookup"><span data-stu-id="dfe54-127">myVnet</span></span>|
    |<span data-ttu-id="dfe54-128">주소 공간</span><span class="sxs-lookup"><span data-stu-id="dfe54-128">Address space</span></span>|<span data-ttu-id="dfe54-129">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="dfe54-129">10.0.0.0/16</span></span>|
    |<span data-ttu-id="dfe54-130">서브넷 이름</span><span class="sxs-lookup"><span data-stu-id="dfe54-130">Subnet name</span></span>|<span data-ttu-id="dfe54-131">공용</span><span class="sxs-lookup"><span data-stu-id="dfe54-131">Public</span></span>|
    |<span data-ttu-id="dfe54-132">서브넷 주소 범위</span><span class="sxs-lookup"><span data-stu-id="dfe54-132">Subnet address range</span></span>|<span data-ttu-id="dfe54-133">10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="dfe54-133">10.0.0.0/24</span></span>|
    |<span data-ttu-id="dfe54-134">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="dfe54-134">Resource group</span></span>|<span data-ttu-id="dfe54-135">**새로 만들기**를 선택한 채로 두고 **myResourceGroup**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-135">Leave **Create new** selected, and then enter **myResourceGroup**.</span></span>|
    |<span data-ttu-id="dfe54-136">구독 및 위치</span><span class="sxs-lookup"><span data-stu-id="dfe54-136">Subscription and location</span></span>|<span data-ttu-id="dfe54-137">구독 및 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-137">Select your subscription and location.</span></span>

    <span data-ttu-id="dfe54-138">새 tooAzure 인 경우에 대해 자세히 알아보세요 [리소스 그룹](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [구독](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), 및 [위치](https://azure.microsoft.com/regions) (tooas 라고도 *영역*).</span><span class="sxs-lookup"><span data-stu-id="dfe54-138">If you're new tooAzure, learn more about [resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (also referred tooas *regions*).</span></span>
4. <span data-ttu-id="dfe54-139">Hello 포털에서 가상 네트워크를 만들 때 서브넷이 하나만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-139">In hello portal, you can create only one subnet when you create a virtual network.</span></span> <span data-ttu-id="dfe54-140">이 자습서에서는 hello 가상 네트워크를 만든 후 두 번째 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-140">In this tutorial, you create a second subnet after you create hello virtual network.</span></span> <span data-ttu-id="dfe54-141">인터넷에서 액세스할 수 있는 리소스 hello 나중에 만들 수 있습니다 **공용** 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-141">You might later create Internet-accessible resources in hello **Public** subnet.</span></span> <span data-ttu-id="dfe54-142">또한 hello에 hello 인터넷에서에서 액세스할 수 없는 리소스를 만들 수 있습니다 **개인** 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-142">You also might create resources that aren't accessible from hello Internet in hello **Private** subnet.</span></span> <span data-ttu-id="dfe54-143">toocreate hello 두 번째 서브넷을 입력 **myVnet** hello에 **리소스 검색** hello hello 페이지 위쪽에 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-143">toocreate hello second subnet, enter **myVnet** in hello **Search resources** box at hello top of hello page.</span></span> <span data-ttu-id="dfe54-144">클릭 **myVnet** hello 검색 결과에 표시 되 면입니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-144">Click **myVnet** when it appears in hello search results.</span></span>
5. <span data-ttu-id="dfe54-145">클릭 **서브넷** (hello에 **설정** 섹션) hello에 **가상 네트워크 만들기 (클래식)** 블레이드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-145">Click **Subnets** (in hello **SETTINGS** section) on hello **Create virtual network (classic)** blade that appears.</span></span>
6. <span data-ttu-id="dfe54-146">클릭 **+ 추가** hello에 **myVnet-서브넷** 블레이드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-146">Click **+Add** on hello **myVnet - Subnets** blade that appears.</span></span>
7. <span data-ttu-id="dfe54-147">입력 **개인** 에 대 한 **이름** hello에 **서브넷 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-147">Enter **Private** for **Name** on hello **Add subnet** blade.</span></span> <span data-ttu-id="dfe54-148">**주소 범위**에 **10.0.1.0/24**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-148">Enter **10.0.1.0/24** for **Address range**.</span></span>  <span data-ttu-id="dfe54-149">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-149">Click **OK**.</span></span>
8. <span data-ttu-id="dfe54-150">Hello에 **myVnet-서브넷** 블레이드에서 hello를 볼 수 있습니다 **공용** 및 **개인** 만든 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-150">On hello **myVnet - Subnets** blade, you can see hello **Public** and **Private** subnets that you created.</span></span>
9. <span data-ttu-id="dfe54-151">**선택적**:이 자습서를 완료 하면 사용 요금을 발생 하지 않습니다 수 있도록 사용자가 만든 toodelete hello 리소스 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-151">**Optional**: When you finish this tutorial, you might want toodelete hello resources that you created, so that you don't incur usage charges:</span></span>
    - <span data-ttu-id="dfe54-152">클릭 **개요** hello에 **myVnet** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-152">Click **Overview** on hello **myVnet** blade.</span></span>
    - <span data-ttu-id="dfe54-153">Hello 클릭 **삭제** hello에 아이콘 **myVnet** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-153">Click hello **Delete** icon on hello **myVnet** blade.</span></span>
    - <span data-ttu-id="dfe54-154">tooconfirm hello 삭제 클릭 **예** hello에 **가상 네트워크 삭제** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-154">tooconfirm hello deletion, click **Yes** in hello **Delete virtual network** box.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="dfe54-155">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="dfe54-155">Azure CLI</span></span>

1. <span data-ttu-id="dfe54-156">유지할 수 있습니다 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), 하거나 hello Azure 클라우드 셸 내에서 CLI hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-156">You can either [install and configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), or use hello CLI within hello Azure Cloud Shell.</span></span> <span data-ttu-id="dfe54-157">Azure 클라우드 셸 hello hello Azure 포털 내에서 직접 실행할 수 있는 무료 Bash 셸의입니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-157">hello Azure Cloud Shell is a free Bash shell that you can run directly within hello Azure portal.</span></span> <span data-ttu-id="dfe54-158">Hello Azure CLI 사전 설치 및 toouse 사용자 계정으로 구성 된이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-158">It has hello Azure CLI preinstalled and configured toouse with your account.</span></span> <span data-ttu-id="dfe54-159">CLI 명령에 대 한 도움말 tooget 입력 `azure <command> --help`합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-159">tooget help for CLI commands, type `azure <command> --help`.</span></span> 
2. <span data-ttu-id="dfe54-160">CLI 세션에서 tooAzure 뒤에 오는 hello 명령 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-160">In a CLI session, log in tooAzure with hello command that follows.</span></span> <span data-ttu-id="dfe54-161">클릭 하면 **실습** hello 상자 아래에 클라우드 셸 열립니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-161">If you click **Try it** in hello box below, a Cloud Shell opens.</span></span> <span data-ttu-id="dfe54-162">Hello 다음 명령을 입력 하지 않고 tooyour Azure 구독에 로그인 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-162">You can log in tooyour Azure subscription, without entering hello following command:</span></span>

    ```azurecli-interactive
    azure login
    ```

3. <span data-ttu-id="dfe54-163">서비스 관리 모드에서 CLI는 tooensure hello hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-163">tooensure hello CLI is in Service Management mode, enter hello following command:</span></span>

    ```azurecli-interactive
    azure config mode asm
    ```

4. <span data-ttu-id="dfe54-164">개인 서브넷을 사용하는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-164">Create a virtual network with a private subnet:</span></span>

    ```azurecli-interactive
    azure network vnet create --vnet myVnet --address-space 10.0.0.0 --cidr 16  --subnet-name Private --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --location "East US"
    ```

5. <span data-ttu-id="dfe54-165">Hello 가상 네트워크 내에 있는 공용 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-165">Create a public subnet within hello virtual network:</span></span>

    ```azurecli-interactive
    azure network vnet subnet create --name Public --vnet-name myVnet --address-prefix 10.0.1.0/24
    ```    
    
6. <span data-ttu-id="dfe54-166">Hello 가상 네트워크 및 서브넷을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-166">Review hello virtual network and subnets:</span></span>

    ```azurecli-interactive
    azure network vnet show --vnet myVnet
    ```

7. <span data-ttu-id="dfe54-167">**선택적**: toodelete hello 리소스 사용량에 따른 요금을 발생 하지 않습니다 있도록이 자습서를 완료 하면 만든를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-167">**Optional**: You might want toodelete hello resources that you created when you finish this tutorial, so that you don't incur usage charges:</span></span>

    ```azurecli-interactive
    azure network vnet delete --vnet myVnet --quiet
    ```

> [!NOTE]
> <span data-ttu-id="dfe54-168">Azure 리소스 그룹에 hello 가상 네트워크를 만듭니다 hello CLI를 사용 하 여 리소스 그룹 toocreate 가상 네트워크 (클래식)를 지정할 수 없습니다, 있지만 *기본 네트워킹*합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-168">Though you can't specify a resource group toocreate a virtual network (classic) in using hello CLI, Azure creates hello virtual network in a resource group named *Default-Networking*.</span></span>

## <a name="powershell"></a><span data-ttu-id="dfe54-169">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dfe54-169">PowerShell</span></span>

1. <span data-ttu-id="dfe54-170">Hello hello PowerShell의 최신 버전을 설치 [Azure](https://www.powershellgallery.com/packages/Azure) 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-170">Install hello latest version of hello PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) module.</span></span> <span data-ttu-id="dfe54-171">새 tooAzure PowerShell 인 경우 참조 [Azure PowerShell 개요](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-171">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="dfe54-172">PowerShell 세션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-172">Start a PowerShell session.</span></span>
3. <span data-ttu-id="dfe54-173">PowerShell에서 로그인 tooAzure hello를 입력 하 여 `Add-AzureAccount` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-173">In PowerShell, log in tooAzure by entering hello `Add-AzureAccount` command.</span></span>
4. <span data-ttu-id="dfe54-174">변경 hello 다음 경로 파일 이름을 적절 하 게는 다음 기존 네트워크 구성 파일을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-174">Change hello following path and filename, as appropriate, then export your existing network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
    ```

5. <span data-ttu-id="dfe54-175">toocreate 공용 및 개인 서브넷과 가상 네트워크를 사용 하 여 모든 텍스트 편집기 tooadd hello **VirtualNetworkSite** toohello 네트워크 구성 파일에 나타나는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-175">toocreate a virtual network with public and private subnets, use any text editor tooadd hello **VirtualNetworkSite** element that follows toohello network configuration file.</span></span>

    ```xml
    <VirtualNetworkSite name="myVnet" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Private">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Public">
            <AddressPrefix>10.0.1.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    ```

    <span data-ttu-id="dfe54-176">전체 검토 hello [네트워크 구성 파일 스키마](https://msdn.microsoft.com/library/azure/jj157100.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-176">Review hello full [network configuration file schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

6. <span data-ttu-id="dfe54-177">Hello 네트워크 구성 파일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-177">Import hello network configuration file:</span></span>

    ```powershell
    Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
    ```

    > [!WARNING]
    > <span data-ttu-id="dfe54-178">변경 된 네트워크 구성 파일을 가져오는 변경 될 수 tooexisting 가상 네트워크 (클래식)를 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-178">Importing a changed network configuration file can cause changes tooexisting virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="dfe54-179">만 hello 이전 가상 네트워크를 추가 하 고 변경 하거나 구독에서 기존 가상 네트워크를 제거 하지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-179">Ensure you only add hello previous virtual network and that you don't change or remove any existing virtual networks from your subscription.</span></span> 

7. <span data-ttu-id="dfe54-180">Hello 가상 네트워크 및 서브넷을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-180">Review hello virtual network and subnets:</span></span>

    ```powershell
    Get-AzureVNetSite -VNetName "myVnet"
    ```

8. <span data-ttu-id="dfe54-181">**선택적**: toodelete hello 리소스 사용량에 따른 요금을 발생 하지 않습니다 있도록이 자습서를 완료 하면 만든를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-181">**Optional**: You might want toodelete hello resources that you created when you finish this tutorial, so that you don't incur usage charges.</span></span> <span data-ttu-id="dfe54-182">toodelete hello 가상 네트워크를 전체 4-6 단계를 다시이 시간 제거 hello **VirtualNetworkSite** 5 단계에서 추가 된 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-182">toodelete hello virtual network, complete steps 4-6 again, this time removing hello **VirtualNetworkSite** element you added in step 5.</span></span>
 
> [!NOTE]
> <span data-ttu-id="dfe54-183">Azure 리소스 그룹에 hello 가상 네트워크를 만듭니다 PowerShell을 사용 하 여 리소스 그룹 toocreate 가상 네트워크 (클래식)를 지정할 수 없습니다, 있지만 *기본 네트워킹*합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-183">Though you can't specify a resource group toocreate a virtual network (classic) in using PowerShell, Azure creates hello virtual network in a resource group named *Default-Networking*.</span></span>

---

## <a name="next-steps"></a><span data-ttu-id="dfe54-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dfe54-184">Next steps</span></span>

- <span data-ttu-id="dfe54-185">모든 가상 네트워크 및 서브넷 설정 하는 방법에 대 한 toolearn 참조 [가상 네트워크를 관리](virtual-network-manage-network.md) 및 [관리 가상 네트워크 서브넷](virtual-network-manage-subnet.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-185">toolearn about all virtual network and subnet settings, see [Manage virtual networks](virtual-network-manage-network.md) and [Manage virtual network subnets](virtual-network-manage-subnet.md).</span></span> <span data-ttu-id="dfe54-186">가상 네트워크 및 서브넷을 사용 하 여 프로덕션 환경 toomeet 다른 요구에 대 한 다양 한 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-186">You have various options for using virtual networks and subnets in a production environment toomeet different requirements.</span></span>
- <span data-ttu-id="dfe54-187">인바운드 및 아웃 바운드 toofilter 서브넷 간의 트래픽은 만들기 및 적용 [네트워크 보안 그룹](virtual-networks-nsg.md) toosubnets 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-187">toofilter inbound and outbound subnet traffic, create and apply [network security groups](virtual-networks-nsg.md) toosubnets.</span></span>
- <span data-ttu-id="dfe54-188">만들기는 [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 또는 [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 가상 컴퓨터를 다음 tooan 기존 가상 네트워크 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-188">Create a [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or a [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) virtual machine, and then connect it tooan existing virtual network.</span></span>
- <span data-ttu-id="dfe54-189">tooconnect 두 가상 네트워크에서 동일한 Azure 위치 hello 하 만들기는 [가상 네트워크 피어 링](create-peering-different-deployment-models.md) hello 가상 네트워크 간의 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-189">tooconnect two virtual networks in hello same Azure location, create a  [virtual network peering](create-peering-different-deployment-models.md) between hello virtual networks.</span></span> <span data-ttu-id="dfe54-190">가상 네트워크 (리소스 관리자) tooa 가상 네트워크 (클래식) 피어 링 할 수 있지만 두 가상 네트워크 (클래식) 간의 피어 링을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-190">You can peer a virtual network (Resource Manager) tooa virtual network (classic), but you cannot create a peering between two virtual networks (classic).</span></span>
- <span data-ttu-id="dfe54-191">사용 하 여 hello 가상 네트워크 tooan 온-프레미스 네트워크에 연결 된 [VPN 게이트웨이](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 또는 [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 회로 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfe54-191">Connect hello virtual network tooan on-premises network by using a [VPN Gateway](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuit.</span></span>
