---
title: "여러 서브넷이 있는 Azure Virtual Network 만들기 | Microsoft 문서"
description: "Azure에서 여러 서브넷이 있는 가상 네트워크를 만드는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: a31f0524a6fa1de45498f340a27b863a3c627e04
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-virtual-network-with-multiple-subnets"></a><span data-ttu-id="f7a6b-103">여러 서브넷이 있는 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="f7a6b-103">Create a virtual network with multiple subnets</span></span>

<span data-ttu-id="f7a6b-104">이 자습서에서는 별도의 공용 및 개인 서브넷이 있는 기본 Azure Virtual Network를 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-104">In this tutorial, learn how to create a basic Azure virtual network that has separate public and private subnets.</span></span> <span data-ttu-id="f7a6b-105">가상 컴퓨터, App Service Environment, Virtual Machine Scale Sets, Azure HDInsight 및 서브넷의 클라우드 서비스와 같은 Azure 리소스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-105">You can create Azure resources, like Virtual machines, App Service environments, Virtual machine scale sets, Azure HDInsight, and Cloud services in a subnet.</span></span> <span data-ttu-id="f7a6b-106">가상 네트워크의 리소스는 서로 간에 통신할 수 있으며 가상 네트워크에 연결된 다른 네트워크의 리소스와도 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-106">Resources in virtual networks can communicate with each other and with resources in other networks connected to a virtual network.</span></span>

<span data-ttu-id="f7a6b-107">다음 섹션에서는 [Azure Portal](#portal), Azure 명령줄 인터페이스([Azure CLI](#azure-cli)), [Azure PowerShell](#powershell) 및 [Azure Resource Manager 템플릿](#resource-manager-template)을 사용하여 가상 네트워크를 만들 수 있는 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-107">The following sections include steps that you can take to create a virtual network by using the [Azure portal](#portal), the Azure command-line interface ([Azure CLI](#azure-cli)), [Azure PowerShell](#powershell), and an [Azure Resource Manager template](#resource-manager-template).</span></span> <span data-ttu-id="f7a6b-108">가상 네트워크를 만드는 데 어떤 도구를 선택하든지 간에 결과는 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-108">The result is the same, regardless of which tool you use to create the virtual network.</span></span> <span data-ttu-id="f7a6b-109">도구 링크를 클릭하면 자습서의 해당 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-109">Click a tool link to go to that section of the tutorial.</span></span> <span data-ttu-id="f7a6b-110">해당 섹션에서 모든 [가상 네트워크](virtual-network-manage-network.md) 및 [서브넷](virtual-network-manage-subnet.md) 설정에 대해 자세히 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-110">Learn more about all [virtual network](virtual-network-manage-network.md) and [subnet](virtual-network-manage-subnet.md) settings.</span></span>

<span data-ttu-id="f7a6b-111">이 문서에서는 새 가상 네트워크를 만들 때 사용하는 것이 좋은 배포 모델인 Resource Manager 배포 모델을 통해 가상 네트워크를 만드는 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-111">This article provides steps to create a virtual network through the Resource Manager deployment model, which is the deployment model we recommend using when creating new virtual networks.</span></span> <span data-ttu-id="f7a6b-112">가상 네트워크(클래식)를 만들어야 할 경우 [가상 네트워크(클래식) 만들기](create-virtual-network-classic.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-112">If you need to create a virtual network (classic), see [Create a virtual network (classic)](create-virtual-network-classic.md).</span></span> <span data-ttu-id="f7a6b-113">Azure 배포 모델에 대해 잘 모르는 경우에는 [Azure 배포 모델 이해](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-113">If you're not familiar with Azure's deployment models, see [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>

## <span data-ttu-id="f7a6b-114"><a name="portal"></a>Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f7a6b-114"><a name="portal"></a>Azure portal</span></span>

1. <span data-ttu-id="f7a6b-115">인터넷 브라우저에서 [Azure Portal](https://portal.azure.com)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-115">In an Internet browser, go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f7a6b-116">[Azure 계정](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-116">Log in using your [Azure account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="f7a6b-117">Azure 계정이 없으면 [평가판](https://azure.microsoft.com/offers/ms-azr-0044p)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-117">If you don't have an Azure account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="f7a6b-118">포털에서 **+새로 만들기** > **네트워킹** > **가상 네트워크**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-118">In the portal, click **+New** > **Networking** > **Virtual network**.</span></span>
3. <span data-ttu-id="f7a6b-119">**가상 네트워크 만들기** 블레이드에서 다음 값을 입력한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-119">On the **Create virtual network** blade, enter the following values, and then click **Create**:</span></span>

    |<span data-ttu-id="f7a6b-120">설정</span><span class="sxs-lookup"><span data-stu-id="f7a6b-120">Setting</span></span>|<span data-ttu-id="f7a6b-121">값</span><span class="sxs-lookup"><span data-stu-id="f7a6b-121">Value</span></span>|
    |---|---|
    |<span data-ttu-id="f7a6b-122">이름</span><span class="sxs-lookup"><span data-stu-id="f7a6b-122">Name</span></span>|<span data-ttu-id="f7a6b-123">myVnet</span><span class="sxs-lookup"><span data-stu-id="f7a6b-123">myVnet</span></span>|
    |<span data-ttu-id="f7a6b-124">주소 공간</span><span class="sxs-lookup"><span data-stu-id="f7a6b-124">Address space</span></span>|<span data-ttu-id="f7a6b-125">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="f7a6b-125">10.0.0.0/16</span></span>|
    |<span data-ttu-id="f7a6b-126">서브넷 이름</span><span class="sxs-lookup"><span data-stu-id="f7a6b-126">Subnet name</span></span>|<span data-ttu-id="f7a6b-127">공용</span><span class="sxs-lookup"><span data-stu-id="f7a6b-127">Public</span></span>|
    |<span data-ttu-id="f7a6b-128">서브넷 주소 범위</span><span class="sxs-lookup"><span data-stu-id="f7a6b-128">Subnet address range</span></span>|<span data-ttu-id="f7a6b-129">10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="f7a6b-129">10.0.0.0/24</span></span>|
    |<span data-ttu-id="f7a6b-130">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="f7a6b-130">Resource group</span></span>|<span data-ttu-id="f7a6b-131">**새로 만들기**를 선택한 채로 두고 **myResourceGroup**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-131">Leave **Create new** selected, and then enter **myResourceGroup**.</span></span>|
    |<span data-ttu-id="f7a6b-132">구독 및 위치</span><span class="sxs-lookup"><span data-stu-id="f7a6b-132">Subscription and location</span></span>|<span data-ttu-id="f7a6b-133">구독 및 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-133">Select your subscription and location.</span></span>

    <span data-ttu-id="f7a6b-134">Azure를 처음 사용하는 경우 [리소스 그룹](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [구독](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) 및 [위치](https://azure.microsoft.com/regions)(*지역*이라고도 함)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-134">If you're new to Azure, learn more about [resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (also referred to as *regions*).</span></span>
4. <span data-ttu-id="f7a6b-135">포털에서 가상 네트워크를 만들 때 서브넷을 하나만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-135">In the portal, you can create only one subnet when you create a virtual network.</span></span> <span data-ttu-id="f7a6b-136">이 자습서에서는 가상 네트워크를 만든 후 두 번째 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-136">In this tutorial, you create a second subnet after you create the virtual network.</span></span> <span data-ttu-id="f7a6b-137">나중에 인터넷에서 액세스할 수 있는 리소스를 **공용** 서브넷에 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-137">You might later create Internet-accessible resources in the **Public** subnet.</span></span> <span data-ttu-id="f7a6b-138">또한 **개인** 서브넷에는 인터넷에서 액세스할 수 없는 리소스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-138">You also might create resources that aren't accessible from the Internet in the **Private** subnet.</span></span> <span data-ttu-id="f7a6b-139">두 번째 서브넷을 만들려면 페이지 위쪽의 **리소스 검색** 상자에 **myVnet**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-139">To create the second subnet, in the **Search resources** box at the top of the page, enter **myVnet**.</span></span> <span data-ttu-id="f7a6b-140">검색 결과에서 **myVnet**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-140">In the search results, click **myVnet**.</span></span> <span data-ttu-id="f7a6b-141">구독에 동일한 이름을 가진 여러 가상 네트워크가 있는 경우 각 가상 네트워크 아래에 나열된 리소스 그룹을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-141">If you have multiple virtual networks with the same name in your subscription, check the resource groups that are listed under each virtual network.</span></span> <span data-ttu-id="f7a6b-142">**myResourceGroup** 리소스 그룹이 있는 **myVnet** 검색 결과를 클릭해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-142">Ensure that you click the **myVnet** search result that has the resource group **myResourceGroup**.</span></span>
5. <span data-ttu-id="f7a6b-143">**myVnet** 블레이드의 **설정**에서 **서브넷**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-143">On the **myVnet** blade, under **SETTINGS**, click **Subnets**.</span></span>
6. <span data-ttu-id="f7a6b-144">**myVnet - 서브넷** 블레이드에서 **+서브넷**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-144">On the **myVnet - Subnets** blade, click **+Subnet**.</span></span>
7. <span data-ttu-id="f7a6b-145">**서브넷 추가** 블레이드에서 **이름**에 **개인**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-145">On the **Add subnet** blade, for **Name**, enter **Private**.</span></span> <span data-ttu-id="f7a6b-146">**주소 범위**에 **10.0.1.0/24**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-146">For **Address range**, enter **10.0.1.0/24**.</span></span>  <span data-ttu-id="f7a6b-147">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-147">Click **OK**.</span></span>
8. <span data-ttu-id="f7a6b-148">**myVnet - 서브넷** 블레이드에서 서브넷을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-148">On the **myVnet - Subnets** blade, review the subnets.</span></span> <span data-ttu-id="f7a6b-149">만든 **공용** 및 **개인** 서브넷을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-149">You can see the **Public** and **Private** subnets that you created.</span></span>
9. <span data-ttu-id="f7a6b-150">**선택 사항**: 이 자습서에서 만든 리소스를 삭제하려면 이 문서의 [리소스 삭제](#delete-portal)에서 설명하는 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-150">**Optional:** To delete the resources that you create in this tutorial, complete the steps in [Delete resources](#delete-portal) in this article.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="f7a6b-151">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f7a6b-151">Azure CLI</span></span>

<span data-ttu-id="f7a6b-152">Azure CLI 명령은 Windows, Linux 또는 macOS에서 실행하는지 여부에 상관없이 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-152">Azure CLI commands are the same, whether you execute the commands from Windows, Linux, or macOS.</span></span> <span data-ttu-id="f7a6b-153">그러나 운영 체제 셸 간에 스크립팅 차이는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-153">However, there are scripting differences between operating system shells.</span></span> <span data-ttu-id="f7a6b-154">다음 단계의 스크립트는 Bash 셸에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-154">The script in the following steps executes in a Bash shell.</span></span> 

1. <span data-ttu-id="f7a6b-155">[Azure CLI를 설치 및 구성합니다](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f7a6b-155">[Install and configure the Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="f7a6b-156">최신 버전의 Azure CLI를 설치했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-156">Ensure you have the most recent version of the Azure CLI installed.</span></span> <span data-ttu-id="f7a6b-157">CLI 명령에 대한 도움말을 보려면 `az <command> --help`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-157">To get help for CLI commands, type `az <command> --help`.</span></span> <span data-ttu-id="f7a6b-158">CLI 및 해당 필수 구성 요소를 설치하는 대신 Azure Cloud Shell을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-158">Rather than installing the CLI and its pre-requisites, you can use the Azure Cloud Shell.</span></span> <span data-ttu-id="f7a6b-159">Azure Cloud Shell은 Azure Portal에서 직접 실행할 수 있는 평가판 Bash 셸입니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-159">The Azure Cloud Shell is a free Bash shell that you can run directly within the Azure portal.</span></span> <span data-ttu-id="f7a6b-160">Cloud Shell에는 Azure CLI가 사전 설치되어 계정에서 사용하도록 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-160">The Cloud Shell has the Azure CLI preinstalled and configured to use with your account.</span></span> <span data-ttu-id="f7a6b-161">Cloud Shell을 사용하려면 [Portal](https://portal.azure.com) 위쪽의 Cloud Shell(**>_**) 단추를 클릭하거나 이어지는 단계에서 *사용해 보세요.* 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-161">To use the Cloud Shell, click the Cloud Shell (**>_**) button at the top of the [portal](https://portal.azure.com) or just click the *Try it* button in the steps that follow.</span></span> 
2. <span data-ttu-id="f7a6b-162">CLI를 로컬로 실행하는 경우 `az login` 명령을 사용하여 Azure에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-162">If running the CLI locally, log in to Azure with the `az login` command.</span></span> <span data-ttu-id="f7a6b-163">Cloud Shell을 사용하는 경우에는 이미 로그인된 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-163">If using the Cloud Shell, you're already logged in.</span></span>
3. <span data-ttu-id="f7a6b-164">다음 스크립트와 해당 주석을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-164">Review the following script and its comments.</span></span> <span data-ttu-id="f7a6b-165">브라우저에서 스크립트를 복사하여 CLI 세션에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-165">In your browser, copy the script and paste it into your CLI session:</span></span>

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
    
    # Create an additional subnet named Private in the virtual network.
    az network vnet subnet create \
      --name Private \
      --address-prefix 10.0.1.0/24 \
      --vnet-name myVnet \
      --resource-group myResourceGroup
    ```
    
4. <span data-ttu-id="f7a6b-166">스크립트 실행이 완료되면 가상 네트워크의 서브넷을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-166">When the script is finished running, review the subnets for the virtual network.</span></span> <span data-ttu-id="f7a6b-167">다음 명령을 복사하여 CLI 세션에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-167">Copy the following command, and then paste it into your CLI session:</span></span>

    ```azurecli
    az network vnet subnet list --resource-group myResourceGroup --vnet-name myVnet --output table
    ```

5. <span data-ttu-id="f7a6b-168">**선택 사항**: 이 자습서에서 만든 리소스를 삭제하려면 이 문서의 [리소스 삭제](#delete-cli)에서 설명하는 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-168">**Optional**: To delete the resources that you create in this tutorial, complete the steps in [Delete resources](#delete-cli) in this article.</span></span>

## <a name="powershell"></a><span data-ttu-id="f7a6b-169">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7a6b-169">PowerShell</span></span>

1. <span data-ttu-id="f7a6b-170">최신 버전의 PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-170">Install the latest version of the PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="f7a6b-171">Azure PowerShell을 처음 사용하는 경우 [Azure PowerShell 개요](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-171">If you're new to Azure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="f7a6b-172">PowerShell 세션에서 `login-azurermaccount` 명령을 사용하여 [Azure 계정](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)으로 Azure에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-172">In a PowerShell session, log in to Azure with your [Azure account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) using the `login-azurermaccount` command.</span></span>

3. <span data-ttu-id="f7a6b-173">다음 스크립트와 해당 주석을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-173">Review the following script and its comments.</span></span> <span data-ttu-id="f7a6b-174">브라우저에서 스크립트를 복사하여 PowerShell 세션에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-174">In your browser, copy the script and paste it into your PowerShell session:</span></span>

    ```powershell
    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name myResourceGroup `
      -Location eastus
    
    # Create the public and private subnets.
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

4. <span data-ttu-id="f7a6b-175">가상 네트워크의 서브넷을 검토하려면 다음 명령을 복사한 다음 PowerShell 세션에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-175">To review the subnets for the virtual network, copy the following command, and then paste it into your PowerShell session:</span></span>

    ```powershell
    $Vnet.subnets | Format-Table Name, AddressPrefix
    ```

5. <span data-ttu-id="f7a6b-176">**선택 사항**: 이 자습서에서 만든 리소스를 삭제하려면 이 문서의 [리소스 삭제](#delete-powershell)에서 설명하는 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-176">**Optional**: To delete the resources that you create in this tutorial, complete the steps in [Delete resources](#delete-powershell) in this article.</span></span>

## <a name="resource-manager-template"></a><span data-ttu-id="f7a6b-177">Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="f7a6b-177">Resource Manager template</span></span>

<span data-ttu-id="f7a6b-178">Azure Resource Manager 템플릿을 사용하여 가상 네트워크를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-178">You can deploy a virtual network by using an Azure Resource Manager template.</span></span> <span data-ttu-id="f7a6b-179">템플릿에 대한 자세한 내용은 [Resource Manager란?](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#template-deployment)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-179">To learn more about templates, see [What is Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#template-deployment).</span></span> <span data-ttu-id="f7a6b-180">템플릿에 액세스하여 해당 매개 변수에 대해 알아보려면 [두 서브넷이 있는 가상 네트워크 만들기](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) 템플릿을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-180">To access the template and to learn about its parameters, see the [Create a virtual network with two subnets](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) template.</span></span> <span data-ttu-id="f7a6b-181">[포털](#template-portal), [Azure CLI](#template-cli) 또는 [PowerShell](#template-powershell)을 사용하여 템플릿을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-181">You can deploy the template by using the [portal](#template-portal), [Azure CLI](#template-cli), or [PowerShell](#template-powershell).</span></span>

<span data-ttu-id="f7a6b-182">**선택 사항**: 이 자습서에서 만든 리소스를 삭제하려면 이 문서의 [리소스 삭제](#delete) 하위 섹션에서 설명하는 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-182">**Optional:** To delete the resources that you create in this tutorial, complete the steps in any subsections of [Delete resources](#delete) in this article.</span></span>

### <span data-ttu-id="f7a6b-183"><a name="template-portal"></a>Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f7a6b-183"><a name="template-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="f7a6b-184">브라우저에서 [템플릿 페이지](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-184">In your browser, open the [template page](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets).</span></span>
2. <span data-ttu-id="f7a6b-185">**Azure에 배포** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-185">Click the **Deploy to Azure** button.</span></span> <span data-ttu-id="f7a6b-186">Azure에 아직 로그인하지 않은 경우 표시되는 Azure Portal 로그인 화면에서 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-186">If you're not already logged in to Azure, log in on the Azure portal login screen that appears.</span></span>
3. <span data-ttu-id="f7a6b-187">[Azure 계정](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)을 사용하여 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-187">Sign in to the portal by using your [Azure account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="f7a6b-188">Azure 계정이 없으면 [평가판](https://azure.microsoft.com/offers/ms-azr-0044p)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-188">If you don't have an Azure account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="f7a6b-189">매개 변수에 대해 다음 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-189">Enter the following values for the parameters:</span></span>

    |<span data-ttu-id="f7a6b-190">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-190">Parameter</span></span>|<span data-ttu-id="f7a6b-191">값</span><span class="sxs-lookup"><span data-stu-id="f7a6b-191">Value</span></span>|
    |---|---|
    |<span data-ttu-id="f7a6b-192">구독</span><span class="sxs-lookup"><span data-stu-id="f7a6b-192">Subscription</span></span>|<span data-ttu-id="f7a6b-193">구독 선택</span><span class="sxs-lookup"><span data-stu-id="f7a6b-193">Select your subscription</span></span>|
    |<span data-ttu-id="f7a6b-194">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="f7a6b-194">Resource group</span></span>|<span data-ttu-id="f7a6b-195">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f7a6b-195">myResourceGroup</span></span>|
    |<span data-ttu-id="f7a6b-196">위치</span><span class="sxs-lookup"><span data-stu-id="f7a6b-196">Location</span></span>|<span data-ttu-id="f7a6b-197">위치 선택</span><span class="sxs-lookup"><span data-stu-id="f7a6b-197">Select a location</span></span>|
    |<span data-ttu-id="f7a6b-198">VNet 이름</span><span class="sxs-lookup"><span data-stu-id="f7a6b-198">Vnet Name</span></span>|<span data-ttu-id="f7a6b-199">myVnet</span><span class="sxs-lookup"><span data-stu-id="f7a6b-199">myVnet</span></span>|
    |<span data-ttu-id="f7a6b-200">VNet 주소 접두사</span><span class="sxs-lookup"><span data-stu-id="f7a6b-200">Vnet Address Prefix</span></span>|<span data-ttu-id="f7a6b-201">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="f7a6b-201">10.0.0.0/16</span></span>|
    |<span data-ttu-id="f7a6b-202">Subnet1Prefix</span><span class="sxs-lookup"><span data-stu-id="f7a6b-202">Subnet1Prefix</span></span>|<span data-ttu-id="f7a6b-203">10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="f7a6b-203">10.0.0.0/24</span></span>|
    |<span data-ttu-id="f7a6b-204">Subnet1Name</span><span class="sxs-lookup"><span data-stu-id="f7a6b-204">Subnet1Name</span></span>|<span data-ttu-id="f7a6b-205">공용</span><span class="sxs-lookup"><span data-stu-id="f7a6b-205">Public</span></span>|
    |<span data-ttu-id="f7a6b-206">Subnet2Prefix</span><span class="sxs-lookup"><span data-stu-id="f7a6b-206">Subnet2Prefix</span></span>|<span data-ttu-id="f7a6b-207">10.0.1.0/24</span><span class="sxs-lookup"><span data-stu-id="f7a6b-207">10.0.1.0/24</span></span>|
    |<span data-ttu-id="f7a6b-208">Subnet2Name</span><span class="sxs-lookup"><span data-stu-id="f7a6b-208">Subnet2Name</span></span>|<span data-ttu-id="f7a6b-209">개인</span><span class="sxs-lookup"><span data-stu-id="f7a6b-209">Private</span></span>|

5. <span data-ttu-id="f7a6b-210">사용 약관에 동의한 다음 **구매**를 클릭하여 가상 네트워크를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-210">Agree to the terms and conditions, and then click **Purchase** to deploy the virtual network.</span></span>

### <span data-ttu-id="f7a6b-211"><a name="template-cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f7a6b-211"><a name="template-cli"></a>Azure CLI</span></span>

1. <span data-ttu-id="f7a6b-212">[Azure CLI를 설치 및 구성합니다](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f7a6b-212">[Install and configure the Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="f7a6b-213">최신 버전의 Azure CLI를 설치했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-213">Ensure you have the most recent version of the Azure CLI installed.</span></span> <span data-ttu-id="f7a6b-214">CLI 명령에 대한 도움말을 보려면 `az <command> --help`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-214">To get help for CLI commands, type `az <command> --help`.</span></span> <span data-ttu-id="f7a6b-215">CLI 및 해당 필수 구성 요소를 설치하는 대신 Azure Cloud Shell을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-215">Rather than installing the CLI and its pre-requisites, you can use the Azure Cloud Shell.</span></span> <span data-ttu-id="f7a6b-216">Azure Cloud Shell은 Azure Portal에서 직접 실행할 수 있는 평가판 Bash 셸입니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-216">The Azure Cloud Shell is a free Bash shell that you can run directly within the Azure portal.</span></span> <span data-ttu-id="f7a6b-217">Cloud Shell에는 Azure CLI가 사전 설치되어 계정에서 사용하도록 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-217">The Cloud Shell has the Azure CLI preinstalled and configured to use with your account.</span></span> <span data-ttu-id="f7a6b-218">Cloud Shell을 사용하려면 [Portal](https://portal.azure.com) 위쪽의 Cloud Shell **>_** 단추를 클릭하거나 이어지는 단계에서 **사용해 보세요.** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-218">To use the Cloud Shell, click the Cloud Shell **>_** button at the top of the [portal](https://portal.azure.com), or just click the **Try it** button in the steps that follow.</span></span> 
2. <span data-ttu-id="f7a6b-219">CLI를 로컬로 실행하는 경우 `az login` 명령을 사용하여 Azure에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-219">If running the CLI locally, log in to Azure with the `az login` command.</span></span> <span data-ttu-id="f7a6b-220">Cloud Shell을 사용하는 경우에는 이미 로그인된 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-220">If using the Cloud Shell, you're already logged in.</span></span>
3. <span data-ttu-id="f7a6b-221">가상 네트워크에 대한 리소스 그룹을 만들려면 다음 명령을 복사하여 CLI 세션에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-221">To create a resource group for the virtual network, copy the following command and paste it into your CLI session:</span></span>

    ```azurecli-interactive
    az group create --name myResourceGroup --location eastus
    ```
    
4. <span data-ttu-id="f7a6b-222">다음 매개 변수 옵션 중 하나를 사용하여 템플릿을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-222">You can deploy the template by using one of the following parameters options:</span></span>
    - <span data-ttu-id="f7a6b-223">**기본 매개 변수 값**.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-223">**Default parameter values**.</span></span> <span data-ttu-id="f7a6b-224">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-224">Enter the following command:</span></span>
    
        ```azurecli-interactive
        az group deployment create --resource-group myResourceGroup --name VnetTutorial --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vnet-two-subnets/azuredeploy.json`
        ```
    - <span data-ttu-id="f7a6b-225">**사용자 지정 매개 변수 값**.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-225">**Custom parameter values**.</span></span> <span data-ttu-id="f7a6b-226">템플릿을 다운로드하여 수정한 후 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-226">Download and modify the template before you deploy the template.</span></span> <span data-ttu-id="f7a6b-227">또한 명령줄에서 매개 변수를 사용하여 템플릿을 배포하거나, 별도의 매개 변수 파일을 사용하여 템플릿을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-227">You also can deploy the template by using parameters at the command line, or deploy the template with a separate parameters file.</span></span> <span data-ttu-id="f7a6b-228">템플릿 및 매개 변수 파일을 다운로드하려면 [두 서브넷이 있는 VNet 만들기](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) 템플릿 페이지에서 **GitHub에서 찾아보기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-228">To download the template and parameters files, click the **Browse on GitHub** button on the [Create a virtual network with two subnets](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) template page.</span></span> <span data-ttu-id="f7a6b-229">GitHub에서 **azuredeploy.parameters.json** 또는 **azuredeploy.json** 파일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-229">In GitHub, click the **azuredeploy.parameters.json** or **azuredeploy.json** file.</span></span> <span data-ttu-id="f7a6b-230">그런 다음 **원시** 단추를 클릭하여 파일을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-230">Then, click the **Raw** button to display the file.</span></span> <span data-ttu-id="f7a6b-231">브라우저에서 파일 내용을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-231">In your browser, copy the contents of the file.</span></span> <span data-ttu-id="f7a6b-232">사용자 컴퓨터에 있는 파일에 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-232">Save the contents to a file on your computer.</span></span> <span data-ttu-id="f7a6b-233">템플릿에서 매개 변수 값을 수정하거나 별도의 매개 변수 파일을 통해 템플릿을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-233">You can modify the parameter values in the template, or deploy the template with a separate parameters file.</span></span>  

    <span data-ttu-id="f7a6b-234">이러한 방법을 사용하여 템플릿을 배포하는 방법에 대해 자세히 알아보려면 `az group deployment create --help`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-234">To learn more about how to deploy templates by using these methods, type `az group deployment create --help`.</span></span>

### <span data-ttu-id="f7a6b-235"><a name="template-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7a6b-235"><a name="template-powershell"></a>PowerShell</span></span>

1. <span data-ttu-id="f7a6b-236">최신 버전의 PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-236">Install the latest version of the PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="f7a6b-237">Azure PowerShell을 처음 사용하는 경우 [Azure PowerShell 개요](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-237">If you're new to Azure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="f7a6b-238">PowerShell 세션에서 [Azure 계정](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)으로 로그인하려면 `login-azurermaccount`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-238">In a PowerShell session, to sign in with your [Azure account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account), enter `login-azurermaccount`.</span></span>
3. <span data-ttu-id="f7a6b-239">가상 네트워크에 대한 리소스 그룹을 만들려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-239">To create a resource group for the virtual network, enter the following command:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
    ```
    
4. <span data-ttu-id="f7a6b-240">다음 매개 변수 옵션 중 하나를 사용하여 템플릿을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-240">You can deploy the template by using one of the following parameters options:</span></span>
    - <span data-ttu-id="f7a6b-241">**기본 매개 변수 값**.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-241">**Default parameter values**.</span></span> <span data-ttu-id="f7a6b-242">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-242">Enter the following command:</span></span>
    
        ```powershell
        New-AzureRmResourceGroupDeployment -Name VnetTutorial -ResourceGroupName myResourceGroup -TemplateUri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vnet-two-subnets/azuredeploy.json
        ```
        
    - <span data-ttu-id="f7a6b-243">**사용자 지정 매개 변수 값**.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-243">**Custom parameter values**.</span></span> <span data-ttu-id="f7a6b-244">템플릿을 다운로드하여 수정한 후 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-244">Download and modify the template before you deploy it.</span></span> <span data-ttu-id="f7a6b-245">또한 명령줄에서 매개 변수를 사용하여 템플릿을 배포하거나, 별도의 매개 변수 파일을 사용하여 템플릿을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-245">You also can deploy the template by using parameters at the command line, or deploy the template with a separate parameters file.</span></span> <span data-ttu-id="f7a6b-246">템플릿 및 매개 변수 파일을 다운로드하려면 [두 서브넷이 있는 VNet 만들기](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) 템플릿 페이지에서 **GitHub에서 찾아보기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-246">To download the template and parameters files, click the **Browse on GitHub** button on the [Create a virtual network with two subnets](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) template page.</span></span> <span data-ttu-id="f7a6b-247">GitHub에서 **azuredeploy.parameters.json** 또는 **azuredeploy.json** 파일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-247">In GitHub, click the **azuredeploy.parameters.json**  or **azuredeploy.json** file.</span></span> <span data-ttu-id="f7a6b-248">그런 다음 **원시** 단추를 클릭하여 파일을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-248">Then, click the **Raw** button to display the file.</span></span> <span data-ttu-id="f7a6b-249">브라우저에서 파일 내용을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-249">In your browser, copy the contents of the file.</span></span> <span data-ttu-id="f7a6b-250">사용자 컴퓨터에 있는 파일에 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-250">Save the contents to a file on your computer.</span></span> <span data-ttu-id="f7a6b-251">템플릿에서 매개 변수 값을 수정하거나 별도의 매개 변수 파일을 통해 템플릿을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-251">You can modify the parameter values in the template, or deploy the template with a separate parameters file.</span></span>  

    <span data-ttu-id="f7a6b-252">이러한 방법을 사용하여 템플릿을 배포하는 방법에 대해 자세히 알아보려면 `Get-Help New-AzureRmResourceGroupDeployment`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-252">To learn more about how to deploy templates by using these methods, type `Get-Help New-AzureRmResourceGroupDeployment`.</span></span> 

## <span data-ttu-id="f7a6b-253"><a name="delete"></a>리소스 삭제</span><span class="sxs-lookup"><span data-stu-id="f7a6b-253"><a name="delete"></a>Delete resources</span></span>

<span data-ttu-id="f7a6b-254">이 자습서를 마친 후에는 사용 요금이 발생하지 않도록 작성했던 리소스를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-254">When you finish this tutorial, you might want to delete the resources that you created, so that you don't incur usage charges.</span></span> <span data-ttu-id="f7a6b-255">리소스 그룹을 삭제하면 리소스 그룹에 있는 리소스도 모두 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-255">Deleting a resource group also deletes all resources that are in the resource group.</span></span>

### <span data-ttu-id="f7a6b-256"><a name="delete-portal"></a>Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f7a6b-256"><a name="delete-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="f7a6b-257">포털 검색 상자에 **myResourceGroup**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-257">In the portal search box, enter **myResourceGroup**.</span></span> <span data-ttu-id="f7a6b-258">검색 결과에서 **myResourceGroup**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-258">In the search results, click **myResourceGroup**.</span></span>
2. <span data-ttu-id="f7a6b-259">**myResourceGroup** 블레이드에서 **삭제** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-259">On the **myResourceGroup** blade, click the **Delete** icon.</span></span>
3. <span data-ttu-id="f7a6b-260">삭제를 확인하려면 **리소스 그룹 이름 입력** 상자에 **myResourceGroup**을 입력한 다음 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-260">To confirm the deletion, in the **TYPE THE RESOURCE GROUP NAME** box, enter **myResourceGroup**, and then click **Delete**.</span></span>

### <span data-ttu-id="f7a6b-261"><a name="delete-cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f7a6b-261"><a name="delete-cli"></a>Azure CLI</span></span>

<span data-ttu-id="f7a6b-262">CLI 세션에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-262">In a CLI session, enter the following command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <span data-ttu-id="f7a6b-263"><a name="delete-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7a6b-263"><a name="delete-powershell"></a>PowerShell</span></span>

<span data-ttu-id="f7a6b-264">PowerShell 세션에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-264">In a PowerShell session, enter the following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="next-steps"></a><span data-ttu-id="f7a6b-265">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f7a6b-265">Next steps</span></span>

- <span data-ttu-id="f7a6b-266">모든 가상 네트워크 및 서브넷 설정에 대해 알아보려면 [가상 네트워크 관리](virtual-network-manage-network.md#view-vnet) 및 [가상 네트워크 서브넷 관리](virtual-network-manage-subnet.md#create-subnet)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-266">To learn about all virtual network and subnet settings, see [Manage virtual networks](virtual-network-manage-network.md#view-vnet) and [Manage virtual network subnets](virtual-network-manage-subnet.md#create-subnet).</span></span> <span data-ttu-id="f7a6b-267">프로덕션 환경에서 가상 네트워크 및 서브넷을 사용할 때 다양한 요구 사항을 충족하기 위한 여러 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-267">You have various options for using virtual networks and subnets in a production environment to meet different requirements.</span></span>
- <span data-ttu-id="f7a6b-268">인바운드 및 아웃바운드 서브넷 트래픽을 필터링하려면 [네트워크 보안 그룹](virtual-networks-nsg.md)을 만들고 서브넷에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-268">To filter inbound and outbound subnet traffic, create and apply [network security groups](virtual-networks-nsg.md) to subnets.</span></span>
- <span data-ttu-id="f7a6b-269">[Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 또는 [Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 가상 컴퓨터를 만든 다음, 기존 가상 네트워크에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-269">Create a [Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or a [Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) virtual machine, and then connect it to an existing virtual network.</span></span>
- <span data-ttu-id="f7a6b-270">같은 Azure 위치의 두 가상 네트워크를 연결하려면 가상 네트워크 간에 [가상 네트워크 피어링](virtual-network-peering-overview.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-270">To connect two virtual networks in the same Azure location, create a  [virtual network peering](virtual-network-peering-overview.md) between the virtual networks.</span></span>
- <span data-ttu-id="f7a6b-271">[VPN Gateway](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 또는 [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 회로를 사용하여 가상 네트워크를 온-프레미스 네트워크에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-271">Connect the virtual network to an on-premises network by using a [VPN Gateway](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuit.</span></span>
