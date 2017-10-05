---
title: "Azure PowerShell(리소스 관리자)에서 SQL Server 가상 컴퓨터 만들기 | Microsoft Docs"
description: "SQL Server 가상 컴퓨터 갤러리 이미지를 사용하여 Azure VM을 만드는 단계 및 PowerShell 스크립트를 제공합니다."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 98d50dd8-48ad-444f-9031-5378d8270d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/17/2017
ms.author: jroth
ms.openlocfilehash: aa90a1d017af5f477407ab33f0580904472f412b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-resource-manager"></a><span data-ttu-id="29fc1-103">Azure PowerShell(리소스 관리자)을 사용하여 SQL Server 가상 컴퓨터 프로비전</span><span class="sxs-lookup"><span data-stu-id="29fc1-103">Provision a SQL Server virtual machine using Azure PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="29fc1-104">포털</span><span class="sxs-lookup"><span data-stu-id="29fc1-104">Portal</span></span>](virtual-machines-windows-portal-sql-server-provision.md)
> * [<span data-ttu-id="29fc1-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="29fc1-105">PowerShell</span></span>](virtual-machines-windows-ps-sql-create.md)
>
>

## <a name="overview"></a><span data-ttu-id="29fc1-106">개요</span><span class="sxs-lookup"><span data-stu-id="29fc1-106">Overview</span></span>
<span data-ttu-id="29fc1-107">이 자습서에서는 Azure PowerShell cmdlet을 사용하여 **Azure Resource Manager** 배포 모델을 사용하는 단일 Azure 가상 컴퓨터를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-107">This tutorial shows you how to create a single Azure virtual machine using the **Azure Resource Manager** deployment model using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="29fc1-108">이 자습서에서는 SQL 갤러리의 이미지에서 단일 디스크 드라이브를 사용하여 단일 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-108">In this tutorial, we will create a single virtual machine using a single disk drive from an image in the SQL Gallery.</span></span> <span data-ttu-id="29fc1-109">가상 컴퓨터에서 사용할 저장소, 네트워크 및 계산 리소스에 대한 새 공급자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-109">We will create new providers for the storage, network, and compute resources that will be used by the virtual machine.</span></span> <span data-ttu-id="29fc1-110">이러한 리소스에 대한 기존 공급자가 있는 경우 대신 이러한 공급자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-110">If you have existing providers for any of these resources, you can use those providers instead.</span></span>

<span data-ttu-id="29fc1-111">이 항목의 클래식 버전이 필요한 경우 [Azure PowerShell 클래식을 사용하여 SQL Server 가상 컴퓨터 프로비전](../classic/ps-sql-create.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29fc1-111">If you need the classic version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Classic](../classic/ps-sql-create.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29fc1-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="29fc1-112">Prerequisites</span></span>
<span data-ttu-id="29fc1-113">이 자습서에는 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-113">For this tutorial you'll need:</span></span>

* <span data-ttu-id="29fc1-114">시작하기 전에 Azure 계정 및 구독.</span><span class="sxs-lookup"><span data-stu-id="29fc1-114">An Azure account and subscription before you start.</span></span> <span data-ttu-id="29fc1-115">없는 경우 지금 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)에 등록하세요.</span><span class="sxs-lookup"><span data-stu-id="29fc1-115">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="29fc1-116">[Azure PowerShell](/powershell/azure/overview), 최소 버전 1.4.0 이상(이 자습서는 1.5.0 버전을 사용하여 작성)</span><span class="sxs-lookup"><span data-stu-id="29fc1-116">[Azure PowerShell)](/powershell/azure/overview), minimum version of 1.4.0 or later (this tutorial written using version 1.5.0).</span></span>
  * <span data-ttu-id="29fc1-117">버전을 검색하려면 **Get-Module Azure -ListAvailable**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-117">To retrieve your version, type **Get-Module Azure -ListAvailable**.</span></span>

## <a name="configure-your-subscription"></a><span data-ttu-id="29fc1-118">구독 구성</span><span class="sxs-lookup"><span data-stu-id="29fc1-118">Configure your subscription</span></span>
<span data-ttu-id="29fc1-119">Windows PowerShell을 열고 다음 cmdlet을 실행하여 Azure 계정에 대한 액세스를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-119">Open Windows PowerShell and establish access to your Azure account by running the following cmdlet.</span></span> <span data-ttu-id="29fc1-120">자격 증명을 입력할 수 있는 로그인 화면이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-120">You will be presented with a sign in screen to enter your credentials.</span></span> <span data-ttu-id="29fc1-121">Azure 포털에 로그인할 때 사용한 것과 동일한 메일과 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-121">Use the same email and password that you use to sign in to the Azure portal.</span></span>

    Add-AzureRmAccount

<span data-ttu-id="29fc1-122">로그인에 성공하면 로그인에 사용한 SubscriptionId를 포함하는 화면에 일부 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-122">After successfully signing in you will see some information on screen that includes the SubscriptionId with which you signed in.</span></span> <span data-ttu-id="29fc1-123">이는 다른 구독으로 변경하지 않는 경우 이 자습서에 대한 리소스가 만들어지는 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-123">This is the subscription in which the resources for this tutorial will be created unless you change to a different subscription.</span></span> <span data-ttu-id="29fc1-124">여러 SubscriptionId가 있는 경우 다음 cmdlet을 실행하여 모든 SubscriptionId 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-124">If you have multiple SubscriptionIds, run the following cmdlet to return a list of all of your SubscriptionIds:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="29fc1-125">다른 SubscriptionID로 변경하려면 원하는 SubscriptionId를 사용하여 다음 cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-125">To change to another SubscriptionID, run the following cmdlet with your desired SubscriptionId.</span></span>

    Select-AzureRmSubscription -SubscriptionId xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## <a name="define-image-variables"></a><span data-ttu-id="29fc1-126">이미지 변수 정의</span><span class="sxs-lookup"><span data-stu-id="29fc1-126">Define image variables</span></span>
<span data-ttu-id="29fc1-127">이 자습서에서 완료된 스크립트를 간단히 이해하고 사용하기 위해 여러 가지 변수를 정의하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-127">To simplify usability and understanding of the completed script from this tutorial, we will start by defining a number of variables.</span></span> <span data-ttu-id="29fc1-128">적절하다고 판단되면 매개 변수 값을 변경하지만, 제공된 값을 수정할 때 이름 길이 및 특수 문자와 관련된 명명 제한 사항에 주의하세요.</span><span class="sxs-lookup"><span data-stu-id="29fc1-128">Change the parameter values as you see fit, but beware of naming restrictions related to name lengths and special characters when modifying the values provided.</span></span>

### <a name="location-and-resource-group"></a><span data-ttu-id="29fc1-129">위치 및 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="29fc1-129">Location and Resource Group</span></span>
<span data-ttu-id="29fc1-130">두 변수를 사용하여 가상 컴퓨터에 대한 다른 리소스를 만들 리소스 그룹 및 데이터 영역을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-130">Use two variables to define the data region and the resource group into which you will create the other resources for the virtual machine.</span></span>

<span data-ttu-id="29fc1-131">원하는 대로 수정하고 다음 cmdlet을 실행하여 이러한 변수를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-131">Modify as desired and then execute the following cmdlets to initialize these variables.</span></span>

    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"

### <a name="storage-properties"></a><span data-ttu-id="29fc1-132">저장소 속성</span><span class="sxs-lookup"><span data-stu-id="29fc1-132">Storage properties</span></span>
<span data-ttu-id="29fc1-133">다음 변수를 사용하여 가상 컴퓨터에서 사용할 저장소 계정 및 저장소 유형을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-133">Use the following variables to define the storage account and the type of storage to be used by the virtual machine.</span></span>

<span data-ttu-id="29fc1-134">원하는 대로 수정하고 다음 cmdlet을 실행하여 이러한 변수를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-134">Modify as desired and then execute the following cmdlet to initialize these variables.</span></span> <span data-ttu-id="29fc1-135">이 예제에서는 프로덕션 워크로드에 권장되는 [프리미엄 저장소](../../../storage/common/storage-premium-storage.md)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-135">Note that in this example, we are using [Premium Storage](../../../storage/common/storage-premium-storage.md), which is recommended for production workloads.</span></span> <span data-ttu-id="29fc1-136">이 참고 자료 및 기타 권장 사항에 대한 세부 정보는 [Azure 가상 컴퓨터의 SQL Server에 대한 성능 모범 사례](virtual-machines-windows-sql-performance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29fc1-136">For details on this guidance and other recommendations, see [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span></span>

    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

### <a name="network-properties"></a><span data-ttu-id="29fc1-137">네트워크 속성</span><span class="sxs-lookup"><span data-stu-id="29fc1-137">Network properties</span></span>
<span data-ttu-id="29fc1-138">다음 변수를 사용하여 가상 컴퓨터의 네트워크에서 사용할 네트워크 인터페이스, TCP/IP 할당 방법, 가상 네트워크 이름, 가상 서브넷 이름, 가상 네트워크용 IP 주소 범위, 서브넷용 IP 주소 범위 및 공용 도메인 이름 레이블을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-138">Use the following variables to define the network interface, the TCP/IP allocation method, the virtual network name, the virtual subnet name, the range of IP addresses for the virtual network, the range of IP addresses for the subnet, and the public domain name label to be used by the network in the virtual machine.</span></span>

<span data-ttu-id="29fc1-139">원하는 대로 수정하고 다음 cmdlet을 실행하여 이러한 변수를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-139">Modify as desired and then execute the following cmdlet to initialize these variables.</span></span>

    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $TCPIPAllocationMethod = "Dynamic"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $DomainName = "sqlvm1"

### <a name="virtual-machine-properties"></a><span data-ttu-id="29fc1-140">가상 컴퓨터 속성</span><span class="sxs-lookup"><span data-stu-id="29fc1-140">Virtual machine properties</span></span>
<span data-ttu-id="29fc1-141">다음 변수를 사용하여 가상 컴퓨터에 대한 가상 컴퓨터 이름, 컴퓨터 이름, 가상 컴퓨터 크기 및 운영 체제 디스크 이름을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-141">Use the following variables to define the virtual machine name, the computer name, the virtual machine size, and the operating system disk name for the virtual machine.</span></span>

<span data-ttu-id="29fc1-142">원하는 대로 수정하고 다음 cmdlet을 실행하여 이러한 변수를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-142">Modify as desired and then execute the following cmdlet to initialize these variables.</span></span>

    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

### <a name="image-properties"></a><span data-ttu-id="29fc1-143">이미지 속성</span><span class="sxs-lookup"><span data-stu-id="29fc1-143">Image properties</span></span>
<span data-ttu-id="29fc1-144">다음 변수를 사용하여 가상 컴퓨터에 사용할 이미지를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-144">Use the following variables to define the image to use for the virtual machine.</span></span> <span data-ttu-id="29fc1-145">이 예제에서는 SQL Server 2016 Enterprise 이미지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-145">In this example, the SQL Server 2016 Enterprise image is used.</span></span>

<span data-ttu-id="29fc1-146">원하는 대로 수정하고 다음 cmdlet을 실행하여 이러한 변수를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-146">Modify as desired and then execute the following cmdlet to initialize these variables.</span></span>

    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

<span data-ttu-id="29fc1-147">Get-AzureRmVMImageOffer 명령을 사용하여 SQL Server 이미지 제품의 전체 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-147">Note that you can get a full list of SQL Server image offerings with the Get-AzureRmVMImageOffer command:</span></span>

    Get-AzureRmVMImageOffer -Location 'East US' -Publisher 'MicrosoftSQLServer'

<span data-ttu-id="29fc1-148">Get-AzureRmVMImageSku 명령을 사용하여 제품에 사용 가능한 Sku를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-148">And you can see the Skus available for an offering with the Get-AzureRmVMImageSku command.</span></span> <span data-ttu-id="29fc1-149">다음 명령을 사용하여 **SQL2014SP1 WS2012R2** 제품에 사용 가능한 모든 Sku를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-149">The following command shows all Skus available for the **SQL2014SP1-WS2012R2** offer.</span></span>

    Get-AzureRmVMImageSku -Location 'East US' -Publisher 'MicrosoftSQLServer' -Offer 'SQL2014SP1-WS2012R2' | Select Skus

## <a name="create-a-resource-group"></a><span data-ttu-id="29fc1-150">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="29fc1-150">Create a resource group</span></span>
<span data-ttu-id="29fc1-151">리소스 관리자 배포 모델을 사용하여 만드는 첫 번째 개체는 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-151">With the Resource Manager deployment model, the first object that you create is the resource group.</span></span> <span data-ttu-id="29fc1-152">[New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet을 사용하여 이전에 초기화한 변수로 정의된 리소스 그룹 이름 및 위치로 Azure 리소스 그룹 및 해당 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-152">We will use the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet to create an Azure resource group and its resources with the resource group name and location defined by the variables that you previously initialized.</span></span>

<span data-ttu-id="29fc1-153">다음 cmdlet을 실행하여 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-153">Execute the following cmdlet to create your new resource group.</span></span>

    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

## <a name="create-a-storage-account"></a><span data-ttu-id="29fc1-154">저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="29fc1-154">Create a storage account</span></span>
<span data-ttu-id="29fc1-155">가상 컴퓨터에 운영 체제 디스크와 SQL Server 데이터 및 로그 파일에 대한 저장소 리소스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-155">The virtual machine requires storage resources for the operating system disk and for the SQL Server data and log files.</span></span> <span data-ttu-id="29fc1-156">간단히 하기 위해 둘 다에 대한 단일 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-156">For simplicity, we will create a single disk for both.</span></span> <span data-ttu-id="29fc1-157">SQL Server 데이터와 로그 파일을 전용 디스크에 배치하기 위해 [Add-Azure Disk](/powershell/module/azure/add-azuredisk) cmdlet을 사용하여 나중에 추가 디스크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-157">You can attach additional disks later using the [Add-Azure Disk](/powershell/module/azure/add-azuredisk) cmdlet in order to place your SQL Server data and log files on dedicated disks.</span></span> <span data-ttu-id="29fc1-158">[New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet을 사용하여 이전에 초기화한 변수로 정의된 저장소 계정 이름, 저장소 SKU 이름 및 위치로 새 리소스 그룹에서 표준 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-158">We will use the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet to create a standard storage account in your new resource group and with the storage account name, storage Sku name, and location defined using the variables that you previously initialized.</span></span>

<span data-ttu-id="29fc1-159">다음 cmdlet을 실행하여 새 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-159">Execute the following cmdlet to create your new storage account.</span></span>

    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

## <a name="create-network-resources"></a><span data-ttu-id="29fc1-160">네트워크 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="29fc1-160">Create network resources</span></span>
<span data-ttu-id="29fc1-161">가상 컴퓨터에 네트워크 연결을 위해 여러 네트워크 리소스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-161">The virtual machine requires a number of network resources for network connectivity.</span></span>

* <span data-ttu-id="29fc1-162">각 가상 컴퓨터에 가상 네트워크가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-162">Each virtual machine requires a virtual network.</span></span>
* <span data-ttu-id="29fc1-163">가상 네트워크에는 하나 이상의 서브넷이 정의되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-163">A virtual network must have at least one subnet defined.</span></span>
* <span data-ttu-id="29fc1-164">네트워크 인터페이스가 공용 또는 개인 IP 주소 중 하나로 정의되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-164">A network interface must be defined with either a public or a private IP address.</span></span>

### <a name="create-a-virtual-network-subnet-configuration"></a><span data-ttu-id="29fc1-165">가상 네트워크 서브넷 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="29fc1-165">Create a virtual network subnet configuration</span></span>
<span data-ttu-id="29fc1-166">가상 네트워크에 대한 서브넷 구성을 만들어 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-166">We will start by creating a subnet configuration for our virtual network.</span></span> <span data-ttu-id="29fc1-167">이 자습서의 경우 [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet을 사용하여 기본 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-167">For our tutorial, we will create a default subnet using the [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet.</span></span> <span data-ttu-id="29fc1-168">이전에 초기화한 변수를 사용하여 정의된 서브넷 이름 및 주소 접두사로 가상 네트워크 서브넷 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-168">We will create our virtual network subnet configuration with the subnet name and address prefix defined using the variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="29fc1-169">이 cmdlet을 사용하여 가상 네트워크 서브넷 구성의 추가 속성을 정의할 수 있지만, 이 내용은 이 자습서에서 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-169">You can define additional properties of the virtual network subnet configuration using this cmdlet, but that is beyond the scope of this tutorial.</span></span>
>
>

<span data-ttu-id="29fc1-170">다음 cmdlet을 실행하여 가상 서브넷 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-170">Execute the following cmdlet to create your virtual subnet configuration.</span></span>

    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix

### <a name="create-a-virtual-network"></a><span data-ttu-id="29fc1-171">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="29fc1-171">Create a virtual network</span></span>
<span data-ttu-id="29fc1-172">다음으로 [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet을 사용하여 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-172">Next, we will create our virtual network using the [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet.</span></span> <span data-ttu-id="29fc1-173">이전 단계에서 정의된 서브넷 구성을 사용하고 이전에 초기화한 변수를 사용하여 정의된 이름, 위치 및 주소 접두사로 새 리소스 그룹에서 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-173">We will create our virtual network in your new resource group, with the name, location, and address prefix defined using the variables that you previously initialized, and using the subnet configuration that you defined in the previous step.</span></span>

<span data-ttu-id="29fc1-174">다음 cmdlet을 실행하여 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-174">Execute the following cmdlet to create your virtual network.</span></span>

    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig

### <a name="create-the-public-ip-address"></a><span data-ttu-id="29fc1-175">공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="29fc1-175">Create the public IP address</span></span>
<span data-ttu-id="29fc1-176">이제 가상 네트워크를 정의했으므로 가상 컴퓨터에 연결하려면 IP 주소를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-176">Now that we have our virtual network defined, we need to configure an IP address for connectivity to the virtual machine.</span></span> <span data-ttu-id="29fc1-177">이 자습서의 경우 인터넷 연결을 지원하도록 동적 IP 주소 지정을 사용하여 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-177">For this tutorial, we will create a public IP address using dynamic IP addressing to support Internet connectivity.</span></span> <span data-ttu-id="29fc1-178">[New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet을 사용하여 이전에 초기화한 변수로 정의된 이름, 위치, 할당 방법 및 DNS 도메인 이름 레이블로 이전에 만든 리소스 그룹에서 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-178">We will use the [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet to create the public IP address in the resource group created prevously and with the name, location, allocation method, and DNS domain name label defined using the variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="29fc1-179">이 cmdlet을 사용하여 공용 IP 주소의 추가 속성을 정의할 수 있지만, 이 내용은 이 초기 자습서에서 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-179">You can define additional properties of the public IP address using this cmdlet, but that is beyond the scope of this initial tutorial.</span></span> <span data-ttu-id="29fc1-180">또한 고정 주소로 개인 주소 또는 주소도 만들 수 있지만, 이 내용도 이 자습서에서 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-180">You could also create a private address or an address with a static address, but that is also beyond the scope of this tutorial.</span></span>
>
>

<span data-ttu-id="29fc1-181">다음 cmdlet을 실행하여 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-181">Execute the following cmdlet to create your public IP address.</span></span>

    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName

### <a name="create-the-network-interface"></a><span data-ttu-id="29fc1-182">네트워크 인터페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="29fc1-182">Create the network interface</span></span>
<span data-ttu-id="29fc1-183">이제 가상 컴퓨터에서 사용할 네트워크 인터페이스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-183">We are now ready to create the network interface that our virtual machine will use.</span></span> <span data-ttu-id="29fc1-184">[New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet을 사용하여 이전에 정의된 이름, 위치, 서브넷 및 공용 IP 주소로 이전에 만든 리소스 그룹에서 네트워크 인터페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-184">We will use the [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet to create our network interface in the resource group created earlier and with the name, location, subnet and public IP address previously defined.</span></span>

<span data-ttu-id="29fc1-185">다음 cmdlet을 실행하여 네트워크 인터페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-185">Execute the following cmdlet to create your network interface.</span></span>

    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

## <a name="configure-a-vm-object"></a><span data-ttu-id="29fc1-186">VM 개체 구성</span><span class="sxs-lookup"><span data-stu-id="29fc1-186">Configure a VM object</span></span>
<span data-ttu-id="29fc1-187">이제 저장소 및 네트워크 리소스를 정의했으므로 가상 컴퓨터에 대한 계산 리소스를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-187">Now that we have storage and network resources defined, we are ready to define compute resources for the virtual machine.</span></span> <span data-ttu-id="29fc1-188">이 자습서의 경우, 가상 컴퓨터 크기 및 다양한 운영 체제 속성을 지정하고, 이전에 만든 네트워크 인터페이스를 지정하고, Blob 저장소를 정의한 다음 운영 체제 디스크를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-188">For our tutorial, we will specify the virtual machine size and various operating system properties, specify the network interface that we previously created, define blob storage, and then specify the operating system disk.</span></span>

### <a name="create-the-vm-object"></a><span data-ttu-id="29fc1-189">VM 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="29fc1-189">Create the VM object</span></span>
<span data-ttu-id="29fc1-190">가상 컴퓨터 크기를 지정하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-190">We will start by specifying the virtual machine size.</span></span> <span data-ttu-id="29fc1-191">이 자습서의 경우 DS13을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-191">For this tutorial, we are specifying a DS13.</span></span> <span data-ttu-id="29fc1-192">[New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet을 사용하여 이전에 초기화한 변수로 정의된 이름 및 크기로 구성 가능한 가상 컴퓨터 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-192">We will use the [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet to create a configurable virtual machine object with the name and size defined using the variables that you previously initialized.</span></span>

<span data-ttu-id="29fc1-193">다음 cmdlet을 실행하여 가상 컴퓨터 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-193">Execute the following cmdlet to create the virtual machine object.</span></span>

    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize

### <a name="create-a-credential-object-to-hold-the-name-and-password-for-the-local-administrator-credentials"></a><span data-ttu-id="29fc1-194">로컬 관리자 자격 증명에 대한 이름 및 암호를 저장하도록 자격 증명 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="29fc1-194">Create a credential object to hold the name and password for the local administrator credentials</span></span>
<span data-ttu-id="29fc1-195">가상 컴퓨터에 대한 운영 체제 속성을 설정하려면 먼저 보안 문자열로 로컬 관리자 계정의 자격 증명을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-195">Before we can set the operating system properties for the virtual machine, we need to supply the credentials for the local administrator account as a secure string.</span></span> <span data-ttu-id="29fc1-196">이렇게 하려면 [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-196">To accomplish this, we will use the [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

<span data-ttu-id="29fc1-197">다음 cmdlet을 실행하고 Windows PowerShell 자격 증명 요청 창에서 Windows 가상 컴퓨터의 로컬 관리자 계정에 사용할 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-197">Execute the following cmdlet and, in the Windows PowerShell credential request window, type the name and password to use for the local administrator account in the Windows virtual machine.</span></span>

    $Credential = Get-Credential -Message "Type the name and password of the local administrator account."

### <a name="set-the-operating-system-properties-for-the-virtual-machine"></a><span data-ttu-id="29fc1-198">가상 컴퓨터에 대한 운영 체제 속성 설정</span><span class="sxs-lookup"><span data-stu-id="29fc1-198">Set the operating system properties for the virtual machine</span></span>
<span data-ttu-id="29fc1-199">이제 가상 컴퓨터의 운영 체제 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-199">Now we are ready to set the virtual machine's operating system properties.</span></span> <span data-ttu-id="29fc1-200">[Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) cmdlet을 사용하여 운영 체제 유형을 Windows로 설정하고, [가상 컴퓨터 에이전트](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)를 설치하도록 요구하고, cmdlet이 자동 업데이트를 사용하도록 지정하고, 이전에 초기화한 변수로 가상 컴퓨터 이름, 컴퓨터 이름 및 자격 증명을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-200">We will use the [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) cmdlet to set the type of operating system as Windows, require the [virtual machine agent](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) to be installed, specify that the cmdlet enables auto update and set the virtual machine name, the computer name, and the credential using the variables that you previously initialized.</span></span>

<span data-ttu-id="29fc1-201">다음 cmdlet을 실행하여 가상 컴퓨터에 대한 운영 체제 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-201">Execute the following cmdlet to set the operating system properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate

### <a name="add-the-network-interface-to-the-virtual-machine"></a><span data-ttu-id="29fc1-202">가상 컴퓨터에 네트워크 인터페이스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-202">Add the network interface to the virtual machine</span></span>
<span data-ttu-id="29fc1-203">다음으로 가상 컴퓨터에 이전에 만든 네트워크 인터페이스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-203">Next, we will add the network interface that we created previously to the virtual machine.</span></span> <span data-ttu-id="29fc1-204">[Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) cmdlet을 사용하여 이전에 정의한 네트워크 인터페이스 변수를 사용하는 네트워크 인터페이스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-204">We will use the [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) cmdlet to add the network interface using the network interface variable that you defined earlier.</span></span>

<span data-ttu-id="29fc1-205">다음 cmdlet을 실행하여 가상 컴퓨터에 대한 네트워크 인터페이스를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-205">Execute the following cmdlet to set the network interface for your virtual machine.</span></span>

    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id

### <a name="set-the-blob-storage-location-for-the-disk-to-be-used-by-the-virtual-machine"></a><span data-ttu-id="29fc1-206">가상 컴퓨터에서 사용할 디스크에 대한 Blob 저장소 위치를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-206">Set the blob storage location for the disk to be used by the virtual machine</span></span>
<span data-ttu-id="29fc1-207">다음으로 이전에 정의한 변수를 사용하여 가상 컴퓨터에서 사용할 디스크에 대한 Blob 저장소 위치를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-207">Next, we will set the blob storage location for the disk to be used by the virtual machine using the variables that you defined earlier.</span></span>

<span data-ttu-id="29fc1-208">다음 cmdlet을 실행하여 Blob 저장소 위치를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-208">Execute the following cmdlet to set the blob storage location.</span></span>

    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"

### <a name="set-the-operating-system-disk-properties-for-the-virtual-machine"></a><span data-ttu-id="29fc1-209">가상 컴퓨터에 대한 운영 체제 디스크 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-209">Set the operating system disk properties for the virtual machine</span></span>
<span data-ttu-id="29fc1-210">다음으로 가상 컴퓨터에 대한 운영 체제 디스크 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-210">Next, we will set the operating system disk properties for the virtual machine.</span></span> <span data-ttu-id="29fc1-211">[Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) cmdlet을 사용하여 가상 컴퓨터의 운영 체제를 이미지에서 구성하도록 지정하고 캐싱을 SQL Server가 같은 디스크에 설치되는 중이므로 읽기 전용으로 설정하며 이전에 정의한 변수로 정의된 가상 컴퓨터 이름 및 운영 체제 디스크를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-211">We will use the [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) cmdlet to specify that the operating system for the virtual machine will come from an image, to set caching to read only (because SQL Server is being installed on the same disk) and define the virtual machine name and the operating system disk defined using the variables that we defined earlier.</span></span>

<span data-ttu-id="29fc1-212">다음 cmdlet을 실행하여 가상 컴퓨터에 대한 운영 체제 디스크 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-212">Execute the following cmdlet to set the operating system disk properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

### <a name="specify-the-platform-image-for-the-virtual-machine"></a><span data-ttu-id="29fc1-213">가상 컴퓨터에 대한 플랫폼 이미지 지정</span><span class="sxs-lookup"><span data-stu-id="29fc1-213">Specify the platform image for the virtual machine</span></span>
<span data-ttu-id="29fc1-214">마지막 구성 단계는 가상 컴퓨터에 대한 플랫폼 이미지를 지정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-214">Our last configuration step is to specify the platform image for our virtual machine.</span></span> <span data-ttu-id="29fc1-215">이 자습서의 경우 최신 SQL Server 2016 CTP 이미지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-215">For our tutorial, we are using the latest SQL Server 2016 CTP image.</span></span> <span data-ttu-id="29fc1-216">[Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet을 사용하여 이전에 정의한 변수에서 정의된 대로 이 이미지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-216">We will use the [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet to use this image as defined by the variables that you defined earlier.</span></span>

<span data-ttu-id="29fc1-217">다음 cmdlet을 실행하여 가상 컴퓨터에 대한 플랫폼 이미지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-217">Execute the following cmdlet to specify the platform image for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

## <a name="create-the-sql-vm"></a><span data-ttu-id="29fc1-218">SQL VM 만들기</span><span class="sxs-lookup"><span data-stu-id="29fc1-218">Create the SQL VM</span></span>
<span data-ttu-id="29fc1-219">이제 구성 단계를 완료했으므로 가상 컴퓨터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-219">Now that you have finished the configuration steps, you are ready to create the virtual machine.</span></span> <span data-ttu-id="29fc1-220">[New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) cmdlet을 사용하여 정의한 변수로 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-220">We will use the [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) cmdlet to create the virtual machine using the variables that we have defined.</span></span>

<span data-ttu-id="29fc1-221">다음 cmdlet을 실행하여 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-221">Execute the following cmdlet to create your virtual machine.</span></span>

    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

<span data-ttu-id="29fc1-222">가상 컴퓨터가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-222">The virtual machine is created.</span></span> <span data-ttu-id="29fc1-223">가상 컴퓨터의 디스크에 대해 지정된 저장소 계정은 프리미엄 저장소 계정이므로 표준 저장소 계정이 부팅 진단에 대해 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-223">Notice that a standard storage account is created for boot diagnostics because the specified storage account for the virtual machine's disk is a premium storage account.</span></span>

<span data-ttu-id="29fc1-224">이제 Azure 포털에서 이 컴퓨터를 보고 [해당 공용 IP 주소 및 정규화된 도메인 이름](virtual-machines-windows-portal-sql-server-provision.md)을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-224">You can now view this machine in the Azure Portal to see [its public IP address and its fully qualified domain name](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="example-script"></a><span data-ttu-id="29fc1-225">예제 스크립트</span><span class="sxs-lookup"><span data-stu-id="29fc1-225">Example script</span></span>
<span data-ttu-id="29fc1-226">다음 스크립트에는 이 자습서에 대한 전체 PowerShell 스크립트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-226">The following script contains the complete PowerShell script for this tutorial.</span></span> <span data-ttu-id="29fc1-227">**Add-AzureRmAccount** 및 **Select-AzureRmSubscription** 명령을 사용하도록 이미 Azure 구독을 설정한 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-227">It assumes that you have already setup the Azure subscription to use with the **Add-AzureRmAccount** and **Select-AzureRmSubscription** commands.</span></span>

    # Variables
    ## Global
    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"
    ## Storage
    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

    ## Network
    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $TCPIPAllocationMethod = "Dynamic"
    $DomainName = "sqlvm1"

    ##Compute
    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

    ##Image
    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

    # Resource Group
    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

    # Storage
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

    # Network
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix
    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig
    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName
    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

    # Compute
    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize
    $Credential = Get-Credential -Message "Type the name and password of the local administrator account."
    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate #-TimeZone = $TimeZone
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

    # Image
    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

    ## Create the VM in Azure
    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

## <a name="next-steps"></a><span data-ttu-id="29fc1-228">다음 단계</span><span class="sxs-lookup"><span data-stu-id="29fc1-228">Next steps</span></span>
<span data-ttu-id="29fc1-229">가상 컴퓨터가 만들어지면 RDP를 사용하여 가상 컴퓨터에 연결하고 연결을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29fc1-229">After the virtual machine is created, you are ready to connect to the virtual machine using RDP and setup connectivity.</span></span> <span data-ttu-id="29fc1-230">자세한 내용은 [Azure(리소스 관리자)에서 SQL Server 가상 컴퓨터에 연결](virtual-machines-windows-sql-connect.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29fc1-230">For more information, see [Connect to a SQL Server Virtual Machine on Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).</span></span>

