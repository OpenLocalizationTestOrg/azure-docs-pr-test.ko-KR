---
title: "Azure 가상 네트워크 서브넷이 여러 개를 aaaCreate | Microsoft Docs"
description: "자세한 내용은 방법 toocreate Azure에서 여러 서브넷을 사용 하 여 가상 네트워크입니다."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ad679a4-a959-4e48-a317-d9f5655a442b
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: 0f56fa6ac24537d33b8e217f5b03f387826ab487
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-multiple-subnets"></a><span data-ttu-id="884db-103">여러 서브넷이 있는 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="884db-103">Create a virtual network with multiple subnets</span></span>

<span data-ttu-id="884db-104">이 자습서에서는 toocreate 기본 Azure 가상 네트워크를 가진 공용 및 개인 서브넷을 구분 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="884db-104">In this tutorial, learn how toocreate a basic Azure virtual network that has separate public and private subnets.</span></span> <span data-ttu-id="884db-105">가상 컴퓨터, App Service Environment, Virtual Machine Scale Sets, Azure HDInsight 및 서브넷의 클라우드 서비스와 같은 Azure 리소스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="884db-105">You can create Azure resources, like Virtual machines, App Service environments, Virtual machine scale sets, Azure HDInsight, and Cloud services in a subnet.</span></span> <span data-ttu-id="884db-106">가상 네트워크의 리소스는 서로 다른 네트워크 연결 된 tooa 가상 네트워크의 리소스와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="884db-106">Resources in virtual networks can communicate with each other and with resources in other networks connected tooa virtual network.</span></span>

<span data-ttu-id="884db-107">hello 다음 섹션에서는 단계를 수행할 수 있는 toocreate 가상 네트워크 hello를 사용 하 여 [Azure 포털](#portal), hello Azure 명령줄 인터페이스 ([Azure CLI](#azure-cli)), [Azure PowerShell ](#powershell), 및 [Azure 리소스 관리자 템플릿](#resource-manager-template)합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-107">hello following sections include steps that you can take toocreate a virtual network by using hello [Azure portal](#portal), hello Azure command-line interface ([Azure CLI](#azure-cli)), [Azure PowerShell](#powershell), and an [Azure Resource Manager template](#resource-manager-template).</span></span> <span data-ttu-id="884db-108">hello 결과 hello에 관계 없이 동일한 toocreate hello 가상 네트워크를 사용 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="884db-108">hello result is hello same, regardless of which tool you use toocreate hello virtual network.</span></span> <span data-ttu-id="884db-109">Hello 자습서의 도구 링크 toogo toothat 섹션을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-109">Click a tool link toogo toothat section of hello tutorial.</span></span> <span data-ttu-id="884db-110">모든 [가상 네트워크](virtual-network-manage-network.md) 및 [서브넷](virtual-network-manage-subnet.md) 설정에 대해 자세히 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="884db-110">Learn more about all [virtual network](virtual-network-manage-network.md) and [subnet](virtual-network-manage-subnet.md) settings.</span></span>

<span data-ttu-id="884db-111">이 문서에서는 단계 toocreate hello 리소스 관리자 배포 모델을 사용할 수 있는 새 가상 네트워크를 만들 때 권장 하는 hello 배포 모델을 통해 가상 네트워크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-111">This article provides steps toocreate a virtual network through hello Resource Manager deployment model, which is hello deployment model we recommend using when creating new virtual networks.</span></span> <span data-ttu-id="884db-112">가상 네트워크 (클래식) toocreate 필요한 경우 참조 [가상 네트워크 (클래식)를 만들고](create-virtual-network-classic.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-112">If you need toocreate a virtual network (classic), see [Create a virtual network (classic)](create-virtual-network-classic.md).</span></span> <span data-ttu-id="884db-113">Azure 배포 모델에 대해 잘 모르는 경우에는 [Azure 배포 모델 이해](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="884db-113">If you're not familiar with Azure's deployment models, see [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>

## <span data-ttu-id="884db-114"><a name="portal"></a>Azure Portal</span><span class="sxs-lookup"><span data-stu-id="884db-114"><a name="portal"></a>Azure portal</span></span>

1. <span data-ttu-id="884db-115">인터넷 브라우저를 이동 toohello [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-115">In an Internet browser, go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="884db-116">[Azure 계정](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-116">Log in using your [Azure account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="884db-117">Azure 계정이 없으면 [무료 평가판](https://azure.microsoft.com/offers/ms-azr-0044p)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="884db-117">If you don't have an Azure account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="884db-118">Hello 포털에서 클릭 **+ 새로 만들기** > **네트워킹** > **가상 네트워크**합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-118">In hello portal, click **+New** > **Networking** > **Virtual network**.</span></span>
3. <span data-ttu-id="884db-119">Hello에 **가상 네트워크 만들기** 블레이드에서 hello 다음 값을 입력 하 고 클릭 **만들기**:</span><span class="sxs-lookup"><span data-stu-id="884db-119">On hello **Create virtual network** blade, enter hello following values, and then click **Create**:</span></span>

    |<span data-ttu-id="884db-120">설정</span><span class="sxs-lookup"><span data-stu-id="884db-120">Setting</span></span>|<span data-ttu-id="884db-121">값</span><span class="sxs-lookup"><span data-stu-id="884db-121">Value</span></span>|
    |---|---|
    |<span data-ttu-id="884db-122">이름</span><span class="sxs-lookup"><span data-stu-id="884db-122">Name</span></span>|<span data-ttu-id="884db-123">myVnet</span><span class="sxs-lookup"><span data-stu-id="884db-123">myVnet</span></span>|
    |<span data-ttu-id="884db-124">주소 공간</span><span class="sxs-lookup"><span data-stu-id="884db-124">Address space</span></span>|<span data-ttu-id="884db-125">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="884db-125">10.0.0.0/16</span></span>|
    |<span data-ttu-id="884db-126">서브넷 이름</span><span class="sxs-lookup"><span data-stu-id="884db-126">Subnet name</span></span>|<span data-ttu-id="884db-127">공용</span><span class="sxs-lookup"><span data-stu-id="884db-127">Public</span></span>|
    |<span data-ttu-id="884db-128">서브넷 주소 범위</span><span class="sxs-lookup"><span data-stu-id="884db-128">Subnet address range</span></span>|<span data-ttu-id="884db-129">10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="884db-129">10.0.0.0/24</span></span>|
    |<span data-ttu-id="884db-130">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="884db-130">Resource group</span></span>|<span data-ttu-id="884db-131">**새로 만들기**를 선택한 채로 두고 **myResourceGroup**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-131">Leave **Create new** selected, and then enter **myResourceGroup**.</span></span>|
    |<span data-ttu-id="884db-132">구독 및 위치</span><span class="sxs-lookup"><span data-stu-id="884db-132">Subscription and location</span></span>|<span data-ttu-id="884db-133">구독 및 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-133">Select your subscription and location.</span></span>

    <span data-ttu-id="884db-134">새 tooAzure 인 경우에 대해 자세히 알아보세요 [리소스 그룹](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [구독](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), 및 [위치](https://azure.microsoft.com/regions) (tooas 라고도 *영역*).</span><span class="sxs-lookup"><span data-stu-id="884db-134">If you're new tooAzure, learn more about [resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (also referred tooas *regions*).</span></span>
4. <span data-ttu-id="884db-135">Hello 포털에서 가상 네트워크를 만들 때 서브넷이 하나만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="884db-135">In hello portal, you can create only one subnet when you create a virtual network.</span></span> <span data-ttu-id="884db-136">이 자습서에서는 hello 가상 네트워크를 만든 후 두 번째 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="884db-136">In this tutorial, you create a second subnet after you create hello virtual network.</span></span> <span data-ttu-id="884db-137">인터넷에서 액세스할 수 있는 리소스 hello 나중에 만들 수 있습니다 **공용** 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="884db-137">You might later create Internet-accessible resources in hello **Public** subnet.</span></span> <span data-ttu-id="884db-138">또한 hello에 hello 인터넷에서에서 액세스할 수 없는 리소스를 만들 수 있습니다 **개인** 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="884db-138">You also might create resources that aren't accessible from hello Internet in hello **Private** subnet.</span></span> <span data-ttu-id="884db-139">hello에 toocreate hello 두 번째 서브넷에 **리소스 검색** hello hello 페이지 위쪽에 상자에 입력 **myVnet**합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-139">toocreate hello second subnet, in hello **Search resources** box at hello top of hello page, enter **myVnet**.</span></span> <span data-ttu-id="884db-140">Hello 검색 결과에서 클릭 **myVnet**합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-140">In hello search results, click **myVnet**.</span></span> <span data-ttu-id="884db-141">가상 네트워크가 여러 구독에서 이름이 같은 hello, 각 가상 네트워크에 나열 된 hello 리소스 그룹을 확인 있는 경우 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-141">If you have multiple virtual networks with hello same name in your subscription, check hello resource groups that are listed under each virtual network.</span></span> <span data-ttu-id="884db-142">Hello를 클릭 하면 확인 **myVnet** 검색 hello 리소스 그룹이 들어 있는 결과 **myResourceGroup**합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-142">Ensure that you click hello **myVnet** search result that has hello resource group **myResourceGroup**.</span></span>
5. <span data-ttu-id="884db-143">Hello에 **myVnet** 블레이드 아래 **설정**, 클릭 **서브넷**합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-143">On hello **myVnet** blade, under **SETTINGS**, click **Subnets**.</span></span>
6. <span data-ttu-id="884db-144">Hello에 **myVnet-서브넷** 블레이드에서 클릭 **+ 서브넷**합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-144">On hello **myVnet - Subnets** blade, click **+Subnet**.</span></span>
7. <span data-ttu-id="884db-145">Hello에 **서브넷 추가** 블레이드에서 대 한 **이름**, 입력 **개인**합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-145">On hello **Add subnet** blade, for **Name**, enter **Private**.</span></span> <span data-ttu-id="884db-146">**주소 범위**에 **10.0.1.0/24**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-146">For **Address range**, enter **10.0.1.0/24**.</span></span>  <span data-ttu-id="884db-147">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-147">Click **OK**.</span></span>
8. <span data-ttu-id="884db-148">Hello에 **myVnet-서브넷** 블레이드, 검토 hello 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="884db-148">On hello **myVnet - Subnets** blade, review hello subnets.</span></span> <span data-ttu-id="884db-149">Hello를 볼 수 있습니다 **공용** 및 **개인** 만든 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="884db-149">You can see hello **Public** and **Private** subnets that you created.</span></span>
9. <span data-ttu-id="884db-150">**선택 사항:** 이 자습서에서 만드는 toodelete hello 리소스의 단계를 완료 hello [리소스를 삭제](#delete-portal) 이 문서의 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="884db-150">**Optional:** toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-portal) in this article.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="884db-151">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="884db-151">Azure CLI</span></span>

<span data-ttu-id="884db-152">Azure CLI 명령을 경우 동일 hello Windows, Linux 또는 macOS에서 hello 명령을 실행 하는지 여부</span><span class="sxs-lookup"><span data-stu-id="884db-152">Azure CLI commands are hello same, whether you execute hello commands from Windows, Linux, or macOS.</span></span> <span data-ttu-id="884db-153">그러나 운영 체제 셸 간에 스크립팅 차이는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="884db-153">However, there are scripting differences between operating system shells.</span></span> <span data-ttu-id="884db-154">Bash 셸의 단계를 수행 하는 hello에 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-154">hello script in hello following steps executes in a Bash shell.</span></span> 

1. <span data-ttu-id="884db-155">[설치 및 구성 hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-155">[Install and configure hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="884db-156">Hello 최신 버전의 hello Azure CLI 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-156">Ensure you have hello most recent version of hello Azure CLI installed.</span></span> <span data-ttu-id="884db-157">CLI 명령에 대 한 도움말 tooget 입력 `az <command> --help`합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-157">tooget help for CLI commands, type `az <command> --help`.</span></span> <span data-ttu-id="884db-158">설치 hello CLI 및 해당 필수 구성 요소는 대신 Azure 클라우드 셸 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="884db-158">Rather than installing hello CLI and its pre-requisites, you can use hello Azure Cloud Shell.</span></span> <span data-ttu-id="884db-159">Azure 클라우드 셸 hello hello Azure 포털 내에서 직접 실행할 수 있는 무료 Bash 셸의입니다.</span><span class="sxs-lookup"><span data-stu-id="884db-159">hello Azure Cloud Shell is a free Bash shell that you can run directly within hello Azure portal.</span></span> <span data-ttu-id="884db-160">클라우드 셸 hello에 hello Azure CLI 사전 설치 및 toouse 계정으로 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="884db-160">hello Cloud Shell has hello Azure CLI preinstalled and configured toouse with your account.</span></span> <span data-ttu-id="884db-161">toouse hello 클라우드 셸 hello 클라우드 셸 클릭 (**> _**) hello hello 위쪽에 단추 [포털](https://portal.azure.com) hello 클릭 또는 *실습* 수행 하는 hello 단계에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="884db-161">toouse hello Cloud Shell, click hello Cloud Shell (**>_**) button at hello top of hello [portal](https://portal.azure.com) or just click hello *Try it* button in hello steps that follow.</span></span> 
2. <span data-ttu-id="884db-162">Hello로 tooAzure hello CLI를 로컬로 실행 하는 경우 로그인 `az login` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="884db-162">If running hello CLI locally, log in tooAzure with hello `az login` command.</span></span> <span data-ttu-id="884db-163">클라우드 셸 hello를 사용 하는 경우 이미 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-163">If using hello Cloud Shell, you're already logged in.</span></span>
3. <span data-ttu-id="884db-164">검토 hello 다음 스크립트와 해당 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-164">Review hello following script and its comments.</span></span> <span data-ttu-id="884db-165">브라우저에서 hello 스크립트 복사한 CLI 세션에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="884db-165">In your browser, copy hello script and paste it into your CLI session:</span></span>

    ```azurecli-interactive
    #!/bin/bash
    
    # Create a resource group.
    az group create \
      --name myResourceGroup \
      --location eastus
    
    # Create a virtual network with one subnet named Public.
    az network vnet create \
      --name myVnet \
      --resource-group myResourceGroup \
      --subnet-name Public
    
    # Create an additional subnet named Private in hello virtual network.
    az network vnet subnet create \
      --name Private \
      --address-prefix 10.0.1.0/24 \
      --vnet-name myVnet \
      --resource-group myResourceGroup
    ```
    
4. <span data-ttu-id="884db-166">Hello 스크립트가 완료 되 면 hello 가상 네트워크에 대 한 hello 서브넷 검토를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-166">When hello script is finished running, review hello subnets for hello virtual network.</span></span> <span data-ttu-id="884db-167">다음 명령을, hello 복사한 CLI 세션에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="884db-167">Copy hello following command, and then paste it into your CLI session:</span></span>

    ```azurecli
    az network vnet subnet list --resource-group myResourceGroup --vnet-name myVnet --output table
    ```

5. <span data-ttu-id="884db-168">**선택적**:이 자습서에서 만드는 toodelete hello 리소스의 단계를 완료 hello [리소스를 삭제](#delete-cli) 이 문서의 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="884db-168">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-cli) in this article.</span></span>

## <a name="powershell"></a><span data-ttu-id="884db-169">PowerShell</span><span class="sxs-lookup"><span data-stu-id="884db-169">PowerShell</span></span>

1. <span data-ttu-id="884db-170">Hello hello PowerShell의 최신 버전을 설치 [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="884db-170">Install hello latest version of hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="884db-171">새 tooAzure PowerShell 인 경우 참조 [Azure PowerShell 개요](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-171">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="884db-172">와 tooAzure PowerShell 세션에서 로그인 하면 [Azure 계정](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) hello를 사용 하 여 `login-azurermaccount` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="884db-172">In a PowerShell session, log in tooAzure with your [Azure account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) using hello `login-azurermaccount` command.</span></span>

3. <span data-ttu-id="884db-173">검토 hello 다음 스크립트와 해당 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-173">Review hello following script and its comments.</span></span> <span data-ttu-id="884db-174">브라우저에서 hello 스크립트를 복사 하 여 PowerShell 세션에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="884db-174">In your browser, copy hello script and paste it into your PowerShell session:</span></span>

    ```powershell
    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name myResourceGroup `
      -Location eastus
    
    # Create hello public and private subnets.
    $Subnet1 = New-AzureRmVirtualNetworkSubnetConfig `
      -Name Public `
      -AddressPrefix 10.0.0.0/24
    $Subnet2 = New-AzureRmVirtualNetworkSubnetConfig `
      -Name Private `
      -AddressPrefix 10.0.1.0/24
    
    # Create a virtual network.
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName myResourceGroup `
      -Location eastus `
      -Name myVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet1,$Subnet2
    ```

4. <span data-ttu-id="884db-175">hello 가상 네트워크에 대 한 tooreview hello 서브넷 다음 명령을, hello를 복사 하 여 PowerShell 세션에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="884db-175">tooreview hello subnets for hello virtual network, copy hello following command, and then paste it into your PowerShell session:</span></span>

    ```powershell
    $Vnet.subnets | Format-Table Name, AddressPrefix
    ```

5. <span data-ttu-id="884db-176">**선택적**:이 자습서에서 만드는 toodelete hello 리소스의 단계를 완료 hello [리소스를 삭제](#delete-powershell) 이 문서의 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="884db-176">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-powershell) in this article.</span></span>

## <a name="resource-manager-template"></a><span data-ttu-id="884db-177">Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="884db-177">Resource Manager template</span></span>

<span data-ttu-id="884db-178">Azure Resource Manager 템플릿을 사용하여 가상 네트워크를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="884db-178">You can deploy a virtual network by using an Azure Resource Manager template.</span></span> <span data-ttu-id="884db-179">서식 파일에 대해 자세히 toolearn 참조 [리소스 관리자란](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#template-deployment)합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-179">toolearn more about templates, see [What is Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#template-deployment).</span></span> <span data-ttu-id="884db-180">tooaccess hello 템플릿 및 해당 매개 변수에 대 한 toolearn 참조 hello [두 서브넷과 가상 네트워크 만들기](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) 템플릿.</span><span class="sxs-lookup"><span data-stu-id="884db-180">tooaccess hello template and toolearn about its parameters, see hello [Create a virtual network with two subnets](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) template.</span></span> <span data-ttu-id="884db-181">Hello를 사용 하 여 hello 서식 파일을 배포할 수 있습니다 [포털](#template-portal), [Azure CLI](#template-cli), 또는 [PowerShell](#template-powershell)합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-181">You can deploy hello template by using hello [portal](#template-portal), [Azure CLI](#template-cli), or [PowerShell](#template-powershell).</span></span>

<span data-ttu-id="884db-182">**선택 사항:** 이 자습서에서 만드는 toodelete hello 리소스의 모든 하위 섹션에서 단계를 완료 hello [리소스를 삭제](#delete) 이 문서의 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="884db-182">**Optional:** toodelete hello resources that you create in this tutorial, complete hello steps in any subsections of [Delete resources](#delete) in this article.</span></span>

### <span data-ttu-id="884db-183"><a name="template-portal"></a>Azure Portal</span><span class="sxs-lookup"><span data-stu-id="884db-183"><a name="template-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="884db-184">브라우저를 열고 hello [템플릿 페이지](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets)합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-184">In your browser, open hello [template page](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets).</span></span>
2. <span data-ttu-id="884db-185">Hello 클릭 **tooAzure 배포** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="884db-185">Click hello **Deploy tooAzure** button.</span></span> <span data-ttu-id="884db-186">표시 된 hello Azure 포털 로그인 화면에 tooAzure에 로그인 되어 있지 하는 경우에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-186">If you're not already logged in tooAzure, log in on hello Azure portal login screen that appears.</span></span>
3. <span data-ttu-id="884db-187">사용 하 여 toohello 포털에 로그인 하면 [Azure 계정](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-187">Sign in toohello portal by using your [Azure account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="884db-188">Azure 계정이 없으면 [무료 평가판](https://azure.microsoft.com/offers/ms-azr-0044p)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="884db-188">If you don't have an Azure account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="884db-189">Hello 다음 hello 매개 변수에 대 한 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-189">Enter hello following values for hello parameters:</span></span>

    |<span data-ttu-id="884db-190">매개 변수</span><span class="sxs-lookup"><span data-stu-id="884db-190">Parameter</span></span>|<span data-ttu-id="884db-191">값</span><span class="sxs-lookup"><span data-stu-id="884db-191">Value</span></span>|
    |---|---|
    |<span data-ttu-id="884db-192">구독</span><span class="sxs-lookup"><span data-stu-id="884db-192">Subscription</span></span>|<span data-ttu-id="884db-193">구독 선택</span><span class="sxs-lookup"><span data-stu-id="884db-193">Select your subscription</span></span>|
    |<span data-ttu-id="884db-194">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="884db-194">Resource group</span></span>|<span data-ttu-id="884db-195">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="884db-195">myResourceGroup</span></span>|
    |<span data-ttu-id="884db-196">위치</span><span class="sxs-lookup"><span data-stu-id="884db-196">Location</span></span>|<span data-ttu-id="884db-197">위치 선택</span><span class="sxs-lookup"><span data-stu-id="884db-197">Select a location</span></span>|
    |<span data-ttu-id="884db-198">VNet 이름</span><span class="sxs-lookup"><span data-stu-id="884db-198">Vnet Name</span></span>|<span data-ttu-id="884db-199">myVnet</span><span class="sxs-lookup"><span data-stu-id="884db-199">myVnet</span></span>|
    |<span data-ttu-id="884db-200">VNet 주소 접두사</span><span class="sxs-lookup"><span data-stu-id="884db-200">Vnet Address Prefix</span></span>|<span data-ttu-id="884db-201">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="884db-201">10.0.0.0/16</span></span>|
    |<span data-ttu-id="884db-202">Subnet1Prefix</span><span class="sxs-lookup"><span data-stu-id="884db-202">Subnet1Prefix</span></span>|<span data-ttu-id="884db-203">10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="884db-203">10.0.0.0/24</span></span>|
    |<span data-ttu-id="884db-204">Subnet1Name</span><span class="sxs-lookup"><span data-stu-id="884db-204">Subnet1Name</span></span>|<span data-ttu-id="884db-205">공용</span><span class="sxs-lookup"><span data-stu-id="884db-205">Public</span></span>|
    |<span data-ttu-id="884db-206">Subnet2Prefix</span><span class="sxs-lookup"><span data-stu-id="884db-206">Subnet2Prefix</span></span>|<span data-ttu-id="884db-207">10.0.1.0/24</span><span class="sxs-lookup"><span data-stu-id="884db-207">10.0.1.0/24</span></span>|
    |<span data-ttu-id="884db-208">Subnet2Name</span><span class="sxs-lookup"><span data-stu-id="884db-208">Subnet2Name</span></span>|<span data-ttu-id="884db-209">개인</span><span class="sxs-lookup"><span data-stu-id="884db-209">Private</span></span>|

5. <span data-ttu-id="884db-210">Toohello 사용 약관을 동의 하 고 클릭 **구매** toodeploy hello 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="884db-210">Agree toohello terms and conditions, and then click **Purchase** toodeploy hello virtual network.</span></span>

### <span data-ttu-id="884db-211"><a name="template-cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="884db-211"><a name="template-cli"></a>Azure CLI</span></span>

1. <span data-ttu-id="884db-212">[설치 및 구성 hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-212">[Install and configure hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="884db-213">Hello 최신 버전의 hello Azure CLI 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-213">Ensure you have hello most recent version of hello Azure CLI installed.</span></span> <span data-ttu-id="884db-214">CLI 명령에 대 한 도움말 tooget 입력 `az <command> --help`합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-214">tooget help for CLI commands, type `az <command> --help`.</span></span> <span data-ttu-id="884db-215">설치 hello CLI 및 해당 필수 구성 요소는 대신 Azure 클라우드 셸 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="884db-215">Rather than installing hello CLI and its pre-requisites, you can use hello Azure Cloud Shell.</span></span> <span data-ttu-id="884db-216">Azure 클라우드 셸 hello hello Azure 포털 내에서 직접 실행할 수 있는 무료 Bash 셸의입니다.</span><span class="sxs-lookup"><span data-stu-id="884db-216">hello Azure Cloud Shell is a free Bash shell that you can run directly within hello Azure portal.</span></span> <span data-ttu-id="884db-217">클라우드 셸 hello에 hello Azure CLI 사전 설치 및 toouse 계정으로 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="884db-217">hello Cloud Shell has hello Azure CLI preinstalled and configured toouse with your account.</span></span> <span data-ttu-id="884db-218">toouse hello 클라우드 셸 클릭 hello 클라우드 셸 **> _** hello hello 위쪽에 단추 [포털](https://portal.azure.com), 또는 hello 클릭할 **실습** 수행 하는 hello 단계에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="884db-218">toouse hello Cloud Shell, click hello Cloud Shell **>_** button at hello top of hello [portal](https://portal.azure.com), or just click hello **Try it** button in hello steps that follow.</span></span> 
2. <span data-ttu-id="884db-219">Hello로 tooAzure hello CLI를 로컬로 실행 하는 경우 로그인 `az login` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="884db-219">If running hello CLI locally, log in tooAzure with hello `az login` command.</span></span> <span data-ttu-id="884db-220">클라우드 셸 hello를 사용 하는 경우 이미 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-220">If using hello Cloud Shell, you're already logged in.</span></span>
3. <span data-ttu-id="884db-221">toocreate hello 가상 네트워크에 대 한 리소스 그룹 복사 hello 다음 명령 및 CLI 세션에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="884db-221">toocreate a resource group for hello virtual network, copy hello following command and paste it into your CLI session:</span></span>

    ```azurecli-interactive
    az group create --name myResourceGroup --location eastus
    ```
    
4. <span data-ttu-id="884db-222">Hello 다음 매개 변수 옵션 중 하나를 사용 하 여 hello 서식 파일을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="884db-222">You can deploy hello template by using one of hello following parameters options:</span></span>
    - <span data-ttu-id="884db-223">**기본 매개 변수 값**.</span><span class="sxs-lookup"><span data-stu-id="884db-223">**Default parameter values**.</span></span> <span data-ttu-id="884db-224">Hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-224">Enter hello following command:</span></span>
    
        ```azurecli-interactive
        az group deployment create --resource-group myResourceGroup --name VnetTutorial --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vnet-two-subnets/azuredeploy.json`
        ```
    - <span data-ttu-id="884db-225">**사용자 지정 매개 변수 값**.</span><span class="sxs-lookup"><span data-stu-id="884db-225">**Custom parameter values**.</span></span> <span data-ttu-id="884db-226">다운로드 하 고 hello 서식 파일을 배포 하기 전에 hello 서식 파일을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-226">Download and modify hello template before you deploy hello template.</span></span> <span data-ttu-id="884db-227">또한 수 hello 명령줄에서 매개 변수를 사용 하 여 hello 서식 파일을 배포 또는 별도 매개 변수 파일이 있는 hello 서식 파일을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-227">You also can deploy hello template by using parameters at hello command line, or deploy hello template with a separate parameters file.</span></span> <span data-ttu-id="884db-228">toodownload hello 템플릿 및 매개 변수 파일을 클릭 하 여 hello **GitHub에서 찾아보기** hello 단추 [두 서브넷과 가상 네트워크 만들기](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) 템플릿 페이지.</span><span class="sxs-lookup"><span data-stu-id="884db-228">toodownload hello template and parameters files, click hello **Browse on GitHub** button on hello [Create a virtual network with two subnets](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) template page.</span></span> <span data-ttu-id="884db-229">GitHub에서 클릭 hello **azuredeploy.parameters.json** 또는 **azuredeploy.json** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="884db-229">In GitHub, click hello **azuredeploy.parameters.json** or **azuredeploy.json** file.</span></span> <span data-ttu-id="884db-230">클릭 hello **Raw** 단추 toodisplay hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="884db-230">Then, click hello **Raw** button toodisplay hello file.</span></span> <span data-ttu-id="884db-231">브라우저에서 hello 내용 hello 파일을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-231">In your browser, copy hello contents of hello file.</span></span> <span data-ttu-id="884db-232">Hello 내용을 tooa 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-232">Save hello contents tooa file on your computer.</span></span> <span data-ttu-id="884db-233">Hello 템플릿의 hello 매개 변수 값을 수정 하거나 별도 매개 변수 파일을 사용 하 여 hello 서식 파일을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="884db-233">You can modify hello parameter values in hello template, or deploy hello template with a separate parameters file.</span></span>  

    <span data-ttu-id="884db-234">이러한 메서드를 사용 하 여 toodeploy 템플릿 입력 하는 방법에 대해 더 알아봅니다을 toolearn `az group deployment create --help`합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-234">toolearn more about how toodeploy templates by using these methods, type `az group deployment create --help`.</span></span>

### <span data-ttu-id="884db-235"><a name="template-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="884db-235"><a name="template-powershell"></a>PowerShell</span></span>

1. <span data-ttu-id="884db-236">Hello hello PowerShell의 최신 버전을 설치 [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="884db-236">Install hello latest version of hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="884db-237">새 tooAzure PowerShell 인 경우 참조 [Azure PowerShell 개요](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-237">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="884db-238">PowerShell 세션에서 사용 하 여 toosign 프로그램 [Azure 계정](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account), 입력 `login-azurermaccount`합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-238">In a PowerShell session, toosign in with your [Azure account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account), enter `login-azurermaccount`.</span></span>
3. <span data-ttu-id="884db-239">hello 가상 네트워크에 대 한 리소스 그룹 toocreate hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-239">toocreate a resource group for hello virtual network, enter hello following command:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
    ```
    
4. <span data-ttu-id="884db-240">Hello 다음 매개 변수 옵션 중 하나를 사용 하 여 hello 서식 파일을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="884db-240">You can deploy hello template by using one of hello following parameters options:</span></span>
    - <span data-ttu-id="884db-241">**기본 매개 변수 값**.</span><span class="sxs-lookup"><span data-stu-id="884db-241">**Default parameter values**.</span></span> <span data-ttu-id="884db-242">Hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-242">Enter hello following command:</span></span>
    
        ```powershell
        New-AzureRmResourceGroupDeployment -Name VnetTutorial -ResourceGroupName myResourceGroup -TemplateUri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vnet-two-subnets/azuredeploy.json
        ```
        
    - <span data-ttu-id="884db-243">**사용자 지정 매개 변수 값**.</span><span class="sxs-lookup"><span data-stu-id="884db-243">**Custom parameter values**.</span></span> <span data-ttu-id="884db-244">다운로드 하 고 배포 하기 전에 hello 서식 파일을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-244">Download and modify hello template before you deploy it.</span></span> <span data-ttu-id="884db-245">또한 수 hello 명령줄에서 매개 변수를 사용 하 여 hello 서식 파일을 배포 또는 별도 매개 변수 파일이 있는 hello 서식 파일을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-245">You also can deploy hello template by using parameters at hello command line, or deploy hello template with a separate parameters file.</span></span> <span data-ttu-id="884db-246">toodownload hello 템플릿 및 매개 변수 파일을 클릭 하 여 hello **GitHub에서 찾아보기** hello 단추 [두 서브넷과 가상 네트워크 만들기](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) 템플릿 페이지.</span><span class="sxs-lookup"><span data-stu-id="884db-246">toodownload hello template and parameters files, click hello **Browse on GitHub** button on hello [Create a virtual network with two subnets](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) template page.</span></span> <span data-ttu-id="884db-247">GitHub에서 클릭 hello **azuredeploy.parameters.json** 또는 **azuredeploy.json** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="884db-247">In GitHub, click hello **azuredeploy.parameters.json**  or **azuredeploy.json** file.</span></span> <span data-ttu-id="884db-248">클릭 hello **Raw** 단추 toodisplay hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="884db-248">Then, click hello **Raw** button toodisplay hello file.</span></span> <span data-ttu-id="884db-249">브라우저에서 hello 내용 hello 파일을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-249">In your browser, copy hello contents of hello file.</span></span> <span data-ttu-id="884db-250">Hello 내용을 tooa 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-250">Save hello contents tooa file on your computer.</span></span> <span data-ttu-id="884db-251">Hello 템플릿의 hello 매개 변수 값을 수정 하거나 별도 매개 변수 파일을 사용 하 여 hello 서식 파일을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="884db-251">You can modify hello parameter values in hello template, or deploy hello template with a separate parameters file.</span></span>  

    <span data-ttu-id="884db-252">이러한 메서드를 사용 하 여 toodeploy 템플릿 입력 하는 방법에 대해 더 알아봅니다을 toolearn `Get-Help New-AzureRmResourceGroupDeployment`합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-252">toolearn more about how toodeploy templates by using these methods, type `Get-Help New-AzureRmResourceGroupDeployment`.</span></span> 

## <span data-ttu-id="884db-253"><a name="delete"></a>리소스 삭제</span><span class="sxs-lookup"><span data-stu-id="884db-253"><a name="delete"></a>Delete resources</span></span>

<span data-ttu-id="884db-254">이 자습서를 완료 하면 사용 요금을 발생 하지 않습니다 수 있도록 사용자가 만든 toodelete hello 리소스를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="884db-254">When you finish this tutorial, you might want toodelete hello resources that you created, so that you don't incur usage charges.</span></span> <span data-ttu-id="884db-255">리소스 그룹을 삭제 하면 hello 리소스 그룹에는 모든 리소스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-255">Deleting a resource group also deletes all resources that are in hello resource group.</span></span>

### <span data-ttu-id="884db-256"><a name="delete-portal"></a>Azure Portal</span><span class="sxs-lookup"><span data-stu-id="884db-256"><a name="delete-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="884db-257">Hello 포털 검색 상자에 입력 **myResourceGroup**합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-257">In hello portal search box, enter **myResourceGroup**.</span></span> <span data-ttu-id="884db-258">Hello 검색 결과에서 클릭 **myResourceGroup**합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-258">In hello search results, click **myResourceGroup**.</span></span>
2. <span data-ttu-id="884db-259">Hello에 **myResourceGroup** 블레이드에서 hello 클릭 **삭제** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="884db-259">On hello **myResourceGroup** blade, click hello **Delete** icon.</span></span>
3. <span data-ttu-id="884db-260">hello에 tooconfirm hello 삭제 **형식 hello 리소스 그룹 이름은** 상자에 입력 **myResourceGroup**, 클릭 하 고 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-260">tooconfirm hello deletion, in hello **TYPE hello RESOURCE GROUP NAME** box, enter **myResourceGroup**, and then click **Delete**.</span></span>

### <span data-ttu-id="884db-261"><a name="delete-cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="884db-261"><a name="delete-cli"></a>Azure CLI</span></span>

<span data-ttu-id="884db-262">CLI 세션 hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-262">In a CLI session, enter hello following command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <span data-ttu-id="884db-263"><a name="delete-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="884db-263"><a name="delete-powershell"></a>PowerShell</span></span>

<span data-ttu-id="884db-264">PowerShell 세션에서 다음 명령을 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-264">In a PowerShell session, enter hello following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="next-steps"></a><span data-ttu-id="884db-265">다음 단계</span><span class="sxs-lookup"><span data-stu-id="884db-265">Next steps</span></span>

- <span data-ttu-id="884db-266">모든 가상 네트워크 및 서브넷 설정 하는 방법에 대 한 toolearn 참조 [가상 네트워크를 관리](virtual-network-manage-network.md#view-vnet) 및 [관리 가상 네트워크 서브넷](virtual-network-manage-subnet.md#create-subnet)합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-266">toolearn about all virtual network and subnet settings, see [Manage virtual networks](virtual-network-manage-network.md#view-vnet) and [Manage virtual network subnets](virtual-network-manage-subnet.md#create-subnet).</span></span> <span data-ttu-id="884db-267">가상 네트워크 및 서브넷을 사용 하 여 프로덕션 환경 toomeet 다른 요구에 대 한 다양 한 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="884db-267">You have various options for using virtual networks and subnets in a production environment toomeet different requirements.</span></span>
- <span data-ttu-id="884db-268">인바운드 및 아웃 바운드 toofilter 서브넷 간의 트래픽은 만들기 및 적용 [네트워크 보안 그룹](virtual-networks-nsg.md) toosubnets 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-268">toofilter inbound and outbound subnet traffic, create and apply [network security groups](virtual-networks-nsg.md) toosubnets.</span></span>
- <span data-ttu-id="884db-269">만들기는 [Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 또는 [Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 가상 컴퓨터를 다음 tooan 기존 가상 네트워크 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-269">Create a [Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or a [Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) virtual machine, and then connect it tooan existing virtual network.</span></span>
- <span data-ttu-id="884db-270">tooconnect 두 가상 네트워크에서 동일한 Azure 위치 hello 하 만들기는 [가상 네트워크 피어 링](virtual-network-peering-overview.md) hello 가상 네트워크 간의 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-270">tooconnect two virtual networks in hello same Azure location, create a  [virtual network peering](virtual-network-peering-overview.md) between hello virtual networks.</span></span>
- <span data-ttu-id="884db-271">사용 하 여 hello 가상 네트워크 tooan 온-프레미스 네트워크에 연결 된 [VPN 게이트웨이](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 또는 [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 회로 합니다.</span><span class="sxs-lookup"><span data-stu-id="884db-271">Connect hello virtual network tooan on-premises network by using a [VPN Gateway](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuit.</span></span>
