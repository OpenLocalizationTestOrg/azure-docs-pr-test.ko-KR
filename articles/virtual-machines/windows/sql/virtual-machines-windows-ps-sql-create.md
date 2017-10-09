---
title: "Azure PowerShell (리소스 관리자)에서 SQL Server 가상 컴퓨터 aaaCreate | Microsoft Docs"
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
ms.openlocfilehash: 2b8cb8f69ff9894a95eab617816a60c8674eeefa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-resource-manager"></a><span data-ttu-id="f3680-103">Azure PowerShell(리소스 관리자)을 사용하여 SQL Server 가상 컴퓨터 프로비전</span><span class="sxs-lookup"><span data-stu-id="f3680-103">Provision a SQL Server virtual machine using Azure PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f3680-104">포털</span><span class="sxs-lookup"><span data-stu-id="f3680-104">Portal</span></span>](virtual-machines-windows-portal-sql-server-provision.md)
> * [<span data-ttu-id="f3680-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f3680-105">PowerShell</span></span>](virtual-machines-windows-ps-sql-create.md)
>
>

## <a name="overview"></a><span data-ttu-id="f3680-106">개요</span><span class="sxs-lookup"><span data-stu-id="f3680-106">Overview</span></span>
<span data-ttu-id="f3680-107">이 자습서에서는 방법을 사용 하 여 Azure 가상 컴퓨터를 단일 toocreate hello **Azure 리소스 관리자** Azure PowerShell cmdlet을 사용 하 여 배포 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-107">This tutorial shows you how toocreate a single Azure virtual machine using hello **Azure Resource Manager** deployment model using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="f3680-108">이 자습서에서는 hello SQL 갤러리에서에서 이미지에서 단일 디스크 드라이브를 사용 하 여 단일 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-108">In this tutorial, we will create a single virtual machine using a single disk drive from an image in hello SQL Gallery.</span></span> <span data-ttu-id="f3680-109">Hello 저장소, 네트워크 및 hello 가상 컴퓨터에서 사용할 수 있는 계산 리소스에 대 한 새 공급자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-109">We will create new providers for hello storage, network, and compute resources that will be used by hello virtual machine.</span></span> <span data-ttu-id="f3680-110">이러한 리소스에 대한 기존 공급자가 있는 경우 대신 이러한 공급자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-110">If you have existing providers for any of these resources, you can use those providers instead.</span></span>

<span data-ttu-id="f3680-111">이 항목의 클래식 버전 hello 필요, 참조 [Azure PowerShell 클래식을 사용 하 여 SQL Server 가상 컴퓨터를 프로 비전](../classic/ps-sql-create.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-111">If you need hello classic version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Classic](../classic/ps-sql-create.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3680-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f3680-112">Prerequisites</span></span>
<span data-ttu-id="f3680-113">이 자습서에는 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-113">For this tutorial you'll need:</span></span>

* <span data-ttu-id="f3680-114">시작하기 전에 Azure 계정 및 구독.</span><span class="sxs-lookup"><span data-stu-id="f3680-114">An Azure account and subscription before you start.</span></span> <span data-ttu-id="f3680-115">없는 경우 지금 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)에 등록하세요.</span><span class="sxs-lookup"><span data-stu-id="f3680-115">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f3680-116">[Azure PowerShell](/powershell/azure/overview), 최소 버전 1.4.0 이상(이 자습서는 1.5.0 버전을 사용하여 작성)</span><span class="sxs-lookup"><span data-stu-id="f3680-116">[Azure PowerShell)](/powershell/azure/overview), minimum version of 1.4.0 or later (this tutorial written using version 1.5.0).</span></span>
  * <span data-ttu-id="f3680-117">tooretrieve 버전, 형식 **Azure Get-module-ListAvailable**합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-117">tooretrieve your version, type **Get-Module Azure -ListAvailable**.</span></span>

## <a name="configure-your-subscription"></a><span data-ttu-id="f3680-118">구독 구성</span><span class="sxs-lookup"><span data-stu-id="f3680-118">Configure your subscription</span></span>
<span data-ttu-id="f3680-119">Windows PowerShell을 열고 Azure 계정 액세스 tooyour hello 다음 cmdlet을 실행 하 여 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-119">Open Windows PowerShell and establish access tooyour Azure account by running hello following cmdlet.</span></span> <span data-ttu-id="f3680-120">나타납니다 화면 tooenter 로그인과 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-120">You will be presented with a sign in screen tooenter your credentials.</span></span> <span data-ttu-id="f3680-121">사용 하 여 hello 동일한 전자 메일 및 toosign toohello Azure 포털에서에서 사용 하는 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-121">Use hello same email and password that you use toosign in toohello Azure portal.</span></span>

    Add-AzureRmAccount

<span data-ttu-id="f3680-122">성공적으로 로그인 한 후에 로그인 하는 hello 구독 Id를 포함 하는 화면에 일부 정보가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-122">After successfully signing in you will see some information on screen that includes hello SubscriptionId with which you signed in.</span></span> <span data-ttu-id="f3680-123">이 자습서에 대 한 hello 리소스 생성 시 사용할 tooa 다른 구독을 변경 하지 않는 한 hello 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-123">This is hello subscription in which hello resources for this tutorial will be created unless you change tooa different subscription.</span></span> <span data-ttu-id="f3680-124">여러 SubscriptionIds를 설정한 경우 모든 사용자 SubscriptionIds의 목록을 hello cmdlet tooreturn 다음 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-124">If you have multiple SubscriptionIds, run hello following cmdlet tooreturn a list of all of your SubscriptionIds:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="f3680-125">toochange tooanother SubscriptionID, hello 뒤에 원하는 구독 Id 사용 하 여 cmdlet을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-125">toochange tooanother SubscriptionID, run hello following cmdlet with your desired SubscriptionId.</span></span>

    Select-AzureRmSubscription -SubscriptionId xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## <a name="define-image-variables"></a><span data-ttu-id="f3680-126">이미지 변수 정의</span><span class="sxs-lookup"><span data-stu-id="f3680-126">Define image variables</span></span>
<span data-ttu-id="f3680-127">toosimplify 유용성 및 이해가이 자습서를 완료 하는 hello 스크립트의 여러 가지 변수를 정의 하 여 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-127">toosimplify usability and understanding of hello completed script from this tutorial, we will start by defining a number of variables.</span></span> <span data-ttu-id="f3680-128">나타나며, 하지만 제공 된 hello 값을 수정 하는 경우에는 명명 제한 관련된 tooname 길이 및 특수 문자에 유의 hello 매개 변수 값을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-128">Change hello parameter values as you see fit, but beware of naming restrictions related tooname lengths and special characters when modifying hello values provided.</span></span>

### <a name="location-and-resource-group"></a><span data-ttu-id="f3680-129">위치 및 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="f3680-129">Location and Resource Group</span></span>
<span data-ttu-id="f3680-130">두 개의 변수 toodefine hello 데이터 영역과 hello 리소스 그룹을 만들게 됩니다 hello hello 가상 컴퓨터에 대 한 기타 리소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-130">Use two variables toodefine hello data region and hello resource group into which you will create hello other resources for hello virtual machine.</span></span>

<span data-ttu-id="f3680-131">원하는 대로 수정 하 고 hello cmdlet tooinitialize 다음 이러한 변수를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-131">Modify as desired and then execute hello following cmdlets tooinitialize these variables.</span></span>

    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"

### <a name="storage-properties"></a><span data-ttu-id="f3680-132">저장소 속성</span><span class="sxs-lookup"><span data-stu-id="f3680-132">Storage properties</span></span>
<span data-ttu-id="f3680-133">다음 변수 toodefine hello 저장소 계정 및 hello 유형의 저장소 toobe hello 가상 컴퓨터에서 사용 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-133">Use hello following variables toodefine hello storage account and hello type of storage toobe used by hello virtual machine.</span></span>

<span data-ttu-id="f3680-134">원하는 대로 수정 하 고 hello cmdlet tooinitialize 다음 이러한 변수를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-134">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span> <span data-ttu-id="f3680-135">이 예제에서는 프로덕션 워크로드에 권장되는 [프리미엄 저장소](../../../storage/common/storage-premium-storage.md)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-135">Note that in this example, we are using [Premium Storage](../../../storage/common/storage-premium-storage.md), which is recommended for production workloads.</span></span> <span data-ttu-id="f3680-136">이 참고 자료 및 기타 권장 사항에 대한 세부 정보는 [Azure 가상 컴퓨터의 SQL Server에 대한 성능 모범 사례](virtual-machines-windows-sql-performance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f3680-136">For details on this guidance and other recommendations, see [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span></span>

    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

### <a name="network-properties"></a><span data-ttu-id="f3680-137">네트워크 속성</span><span class="sxs-lookup"><span data-stu-id="f3680-137">Network properties</span></span>
<span data-ttu-id="f3680-138">Hello 다음 변수 toodefine hello 네트워크 인터페이스, hello TCP/IP 할당 방법, hello 가상 네트워크 이름, hello 가상 서브넷 이름, hello 가상 네트워크에 대 한 hello 범위의 IP 주소, 서브넷 hello 및 hello에 대 한 hello 범위의 IP 주소를 사용 하 여 공용 도메인 이름 레이블 toobe hello 가상 컴퓨터의 hello 네트워크에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-138">Use hello following variables toodefine hello network interface, hello TCP/IP allocation method, hello virtual network name, hello virtual subnet name, hello range of IP addresses for hello virtual network, hello range of IP addresses for hello subnet, and hello public domain name label toobe used by hello network in hello virtual machine.</span></span>

<span data-ttu-id="f3680-139">원하는 대로 수정 하 고 hello cmdlet tooinitialize 다음 이러한 변수를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-139">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $TCPIPAllocationMethod = "Dynamic"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $DomainName = "sqlvm1"

### <a name="virtual-machine-properties"></a><span data-ttu-id="f3680-140">가상 컴퓨터 속성</span><span class="sxs-lookup"><span data-stu-id="f3680-140">Virtual machine properties</span></span>
<span data-ttu-id="f3680-141">다음 변수 toodefine hello 가상 컴퓨터 이름 "," hello 컴퓨터 이름 "," hello 가상 컴퓨터 크기 "및" hello 가상 컴퓨터에 대 한 hello 운영 체제 디스크 이름을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-141">Use hello following variables toodefine hello virtual machine name, hello computer name, hello virtual machine size, and hello operating system disk name for hello virtual machine.</span></span>

<span data-ttu-id="f3680-142">원하는 대로 수정 하 고 hello cmdlet tooinitialize 다음 이러한 변수를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-142">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

### <a name="image-properties"></a><span data-ttu-id="f3680-143">이미지 속성</span><span class="sxs-lookup"><span data-stu-id="f3680-143">Image properties</span></span>
<span data-ttu-id="f3680-144">다음 변수 toodefine hello 이미지 toouse hello 가상 컴퓨터에 대 한 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-144">Use hello following variables toodefine hello image toouse for hello virtual machine.</span></span> <span data-ttu-id="f3680-145">이 예제에서는 hello SQL Server 2016 Enterprise 이미지가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-145">In this example, hello SQL Server 2016 Enterprise image is used.</span></span>

<span data-ttu-id="f3680-146">원하는 대로 수정 하 고 hello cmdlet tooinitialize 다음 이러한 변수를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-146">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

<span data-ttu-id="f3680-147">Note hello Get AzureRmVMImageOffer 명령 사용 하 여 SQL Server 이미지 제품의 전체 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-147">Note that you can get a full list of SQL Server image offerings with hello Get-AzureRmVMImageOffer command:</span></span>

    Get-AzureRmVMImageOffer -Location 'East US' -Publisher 'MicrosoftSQLServer'

<span data-ttu-id="f3680-148">및 hello hello Get AzureRmVMImageSku 명령 사용 하 여 제공에 대 한 사용 가능한 Sku를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-148">And you can see hello Skus available for an offering with hello Get-AzureRmVMImageSku command.</span></span> <span data-ttu-id="f3680-149">hello 다음 명령을 표시 hello에 사용할 수 있는 모든 Sku **SQL2014SP1 WS2012R2** 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-149">hello following command shows all Skus available for hello **SQL2014SP1-WS2012R2** offer.</span></span>

    Get-AzureRmVMImageSku -Location 'East US' -Publisher 'MicrosoftSQLServer' -Offer 'SQL2014SP1-WS2012R2' | Select Skus

## <a name="create-a-resource-group"></a><span data-ttu-id="f3680-150">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="f3680-150">Create a resource group</span></span>
<span data-ttu-id="f3680-151">Hello 리소스 관리자 배포 모델을 만드는 첫 번째 개체를 hello은 hello 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-151">With hello Resource Manager deployment model, hello first object that you create is hello resource group.</span></span> <span data-ttu-id="f3680-152">Hello 사용 하 여 [새로 AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet toocreate Azure 리소스 그룹 및 hello 리소스를 사용 하 여 해당 리소스 그룹 이름 및 이전에 초기화 hello 변수에 의해 정의 된 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-152">We will use hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet toocreate an Azure resource group and its resources with hello resource group name and location defined by hello variables that you previously initialized.</span></span>

<span data-ttu-id="f3680-153">다음 cmdlet toocreate hello 새 리소스 그룹을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-153">Execute hello following cmdlet toocreate your new resource group.</span></span>

    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

## <a name="create-a-storage-account"></a><span data-ttu-id="f3680-154">저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="f3680-154">Create a storage account</span></span>
<span data-ttu-id="f3680-155">hello 가상 컴퓨터는 hello 운영 체제 디스크 및 hello SQL Server 데이터 및 로그 파일에 대 한 저장소 리소스를 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-155">hello virtual machine requires storage resources for hello operating system disk and for hello SQL Server data and log files.</span></span> <span data-ttu-id="f3680-156">간단히 하기 위해 둘 다에 대한 단일 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-156">For simplicity, we will create a single disk for both.</span></span> <span data-ttu-id="f3680-157">Hello를 사용 하 여 나중에 추가 디스크를 연결 하면 [추가 Azure 디스크](/powershell/module/azure/add-azuredisk) cmdlet에 주문 tooplace SQL Server 데이터 및 로그 파일은 전용된 디스크에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-157">You can attach additional disks later using hello [Add-Azure Disk](/powershell/module/azure/add-azuredisk) cmdlet in order tooplace your SQL Server data and log files on dedicated disks.</span></span> <span data-ttu-id="f3680-158">Hello 사용 하 여 [새로 AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet toocreate 표준 저장소 계정을 hello 저장소 계정 이름, 저장소 Sku 이름 및 hello 변수를 사용 하 여 정의 된 위치와 새 리소스 그룹 이전에 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-158">We will use hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet toocreate a standard storage account in your new resource group and with hello storage account name, storage Sku name, and location defined using hello variables that you previously initialized.</span></span>

<span data-ttu-id="f3680-159">새 저장소 계정의 hello cmdlet toocreate 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-159">Execute hello following cmdlet toocreate your new storage account.</span></span>

    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

## <a name="create-network-resources"></a><span data-ttu-id="f3680-160">네트워크 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="f3680-160">Create network resources</span></span>
<span data-ttu-id="f3680-161">hello 가상 컴퓨터는 네트워크 연결을 위한 다양 한 네트워크 리소스를 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-161">hello virtual machine requires a number of network resources for network connectivity.</span></span>

* <span data-ttu-id="f3680-162">각 가상 컴퓨터에 가상 네트워크가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-162">Each virtual machine requires a virtual network.</span></span>
* <span data-ttu-id="f3680-163">가상 네트워크에는 하나 이상의 서브넷이 정의되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-163">A virtual network must have at least one subnet defined.</span></span>
* <span data-ttu-id="f3680-164">네트워크 인터페이스가 공용 또는 개인 IP 주소 중 하나로 정의되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-164">A network interface must be defined with either a public or a private IP address.</span></span>

### <a name="create-a-virtual-network-subnet-configuration"></a><span data-ttu-id="f3680-165">가상 네트워크 서브넷 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="f3680-165">Create a virtual network subnet configuration</span></span>
<span data-ttu-id="f3680-166">가상 네트워크에 대한 서브넷 구성을 만들어 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-166">We will start by creating a subnet configuration for our virtual network.</span></span> <span data-ttu-id="f3680-167">이 자습서에 대 한 hello를 사용 하 여 기본 서브넷 만듭니다 [새로 AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f3680-167">For our tutorial, we will create a default subnet using hello [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet.</span></span> <span data-ttu-id="f3680-168">이 가상 네트워크 서브넷 configuration hello 서브넷 이름 및 주소 접두사는 이전에 초기화 hello 변수를 사용 하 여 정의를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-168">We will create our virtual network subnet configuration with hello subnet name and address prefix defined using hello variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="f3680-169">이 cmdlet을 사용 하 여 hello 가상 네트워크 서브넷 구성의 추가 속성을 정의할 수 있지만이 자습서의 hello 범위를 벗어납니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-169">You can define additional properties of hello virtual network subnet configuration using this cmdlet, but that is beyond hello scope of this tutorial.</span></span>
>
>

<span data-ttu-id="f3680-170">가상 서브넷 configuration hello cmdlet toocreate 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-170">Execute hello following cmdlet toocreate your virtual subnet configuration.</span></span>

    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix

### <a name="create-a-virtual-network"></a><span data-ttu-id="f3680-171">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="f3680-171">Create a virtual network</span></span>
<span data-ttu-id="f3680-172">다음으로 hello를 사용 하는 가상 네트워크를 만들겠습니다 [새로 AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f3680-172">Next, we will create our virtual network using hello [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet.</span></span> <span data-ttu-id="f3680-173">주소 접두사 정의 이전에 초기화 된 hello 변수를 사용 하 고 hello 이전 단계에서 정의 된 hello 서브넷 configuration을 사용 하 여 hello 이름, 위치와 새 리소스 그룹에는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-173">We will create our virtual network in your new resource group, with hello name, location, and address prefix defined using hello variables that you previously initialized, and using hello subnet configuration that you defined in hello previous step.</span></span>

<span data-ttu-id="f3680-174">가상 네트워크가 hello cmdlet toocreate 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-174">Execute hello following cmdlet toocreate your virtual network.</span></span>

    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig

### <a name="create-hello-public-ip-address"></a><span data-ttu-id="f3680-175">Hello 공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="f3680-175">Create hello public IP address</span></span>
<span data-ttu-id="f3680-176">이제는 가상 네트워크를 정의 했으므로 연결 toohello 가상 컴퓨터에 대 한 tooconfigure IP 주소가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-176">Now that we have our virtual network defined, we need tooconfigure an IP address for connectivity toohello virtual machine.</span></span> <span data-ttu-id="f3680-177">이 자습서에서는 toosupport 인터넷 연결 주소를 지정 하는 동적 IP를 사용 하 여 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-177">For this tutorial, we will create a public IP address using dynamic IP addressing toosupport Internet connectivity.</span></span> <span data-ttu-id="f3680-178">Hello 사용 하 여 [새로 AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet toocreate hello 공용 IP 주소 hello 리소스 그룹을 만들었습니다 prevously 고 hello 이름, 위치, 할당 방법 및 hello를 사용 하 여 정의 하는 DNS 도메인 이름 레이블 이전에 초기화는 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-178">We will use hello [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet toocreate hello public IP address in hello resource group created prevously and with hello name, location, allocation method, and DNS domain name label defined using hello variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="f3680-179">추가 속성을이 cmdlet을 사용 하 여 hello 공용 IP 주소를 정의할 수 있지만 초기이 자습서의 hello 범위를 벗어납니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-179">You can define additional properties of hello public IP address using this cmdlet, but that is beyond hello scope of this initial tutorial.</span></span> <span data-ttu-id="f3680-180">고정 주소를 갖는 개인 주소 또는 주소를 만들 수도 수 있지만이 자습서의 hello 범위를 벗어나 그것도입니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-180">You could also create a private address or an address with a static address, but that is also beyond hello scope of this tutorial.</span></span>
>
>

<span data-ttu-id="f3680-181">공용 IP 주소가 hello cmdlet toocreate 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-181">Execute hello following cmdlet toocreate your public IP address.</span></span>

    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName

### <a name="create-hello-network-interface"></a><span data-ttu-id="f3680-182">Hello 네트워크 인터페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="f3680-182">Create hello network interface</span></span>
<span data-ttu-id="f3680-183">가상 컴퓨터에서 사용할 준비 toocreate hello 네트워크 인터페이스는 이제입니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-183">We are now ready toocreate hello network interface that our virtual machine will use.</span></span> <span data-ttu-id="f3680-184">Hello 사용 하 여 [새로 AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet toocreate hello 이름, 위치, 서브넷 및 공용 IP 주소 앞에서 만든 hello 리소스 그룹에이 네트워크 인터페이스는 이전에 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-184">We will use hello [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet toocreate our network interface in hello resource group created earlier and with hello name, location, subnet and public IP address previously defined.</span></span>

<span data-ttu-id="f3680-185">다음 cmdlet toocreate hello 해당 네트워크 인터페이스를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-185">Execute hello following cmdlet toocreate your network interface.</span></span>

    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

## <a name="configure-a-vm-object"></a><span data-ttu-id="f3680-186">VM 개체 구성</span><span class="sxs-lookup"><span data-stu-id="f3680-186">Configure a VM object</span></span>
<span data-ttu-id="f3680-187">이제 저장소 및 네트워크 리소스를 정의 했으므로 hello 가상 컴퓨터에 대 한 준비 toodefine 계산 리소스는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-187">Now that we have storage and network resources defined, we are ready toodefine compute resources for hello virtual machine.</span></span> <span data-ttu-id="f3680-188">이 자습서에 대 한 hello 가상 컴퓨터 크기와 다양 한 운영 체제 속성 지정, 이전에 만든 hello 네트워크 인터페이스 지정, blob 저장소를 정의 하 고 합니다 hello 운영 체제 디스크를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-188">For our tutorial, we will specify hello virtual machine size and various operating system properties, specify hello network interface that we previously created, define blob storage, and then specify hello operating system disk.</span></span>

### <a name="create-hello-vm-object"></a><span data-ttu-id="f3680-189">Hello VM 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="f3680-189">Create hello VM object</span></span>
<span data-ttu-id="f3680-190">Hello 가상 컴퓨터 크기를 지정 하 여 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-190">We will start by specifying hello virtual machine size.</span></span> <span data-ttu-id="f3680-191">이 자습서의 경우 DS13을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-191">For this tutorial, we are specifying a DS13.</span></span> <span data-ttu-id="f3680-192">Hello 사용 하 여 [새로 AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet toocreate 구성 가능한 가상 컴퓨터 개체에 hello 이름 및 크기를 이전에 초기화 하는 hello 변수를 사용 하 여 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-192">We will use hello [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet toocreate a configurable virtual machine object with hello name and size defined using hello variables that you previously initialized.</span></span>

<span data-ttu-id="f3680-193">Hello cmdlet toocreate hello 가상 컴퓨터 개체를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-193">Execute hello following cmdlet toocreate hello virtual machine object.</span></span>

    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize

### <a name="create-a-credential-object-toohold-hello-name-and-password-for-hello-local-administrator-credentials"></a><span data-ttu-id="f3680-194">자격 증명 개체 toohold hello 이름 및 암호 hello 로컬 관리자 자격 증명 만들기</span><span class="sxs-lookup"><span data-stu-id="f3680-194">Create a credential object toohold hello name and password for hello local administrator credentials</span></span>
<span data-ttu-id="f3680-195">Hello 가상 컴퓨터에 대 한 hello 운영 체제 속성을 설정할 수 있습니다, 전에 toosupply hello 자격 증명이 필요 hello 로컬 관리자 계정에 대 한 보안 문자열로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-195">Before we can set hello operating system properties for hello virtual machine, we need toosupply hello credentials for hello local administrator account as a secure string.</span></span> <span data-ttu-id="f3680-196">tooaccomplish이 hello 사용 하 여 [Get-credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f3680-196">tooaccomplish this, we will use hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

<span data-ttu-id="f3680-197">Hello 다음 cmdlet을 실행 하 고 hello Windows PowerShell 자격 증명 요청 창에서 이름 및 암호 toouse hello Windows 가상 컴퓨터에서 로컬 관리자 계정 hello에 대 한 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-197">Execute hello following cmdlet and, in hello Windows PowerShell credential request window, type hello name and password toouse for hello local administrator account in hello Windows virtual machine.</span></span>

    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."

### <a name="set-hello-operating-system-properties-for-hello-virtual-machine"></a><span data-ttu-id="f3680-198">Hello 가상 컴퓨터에 대 한 hello 운영 체제 속성 설정</span><span class="sxs-lookup"><span data-stu-id="f3680-198">Set hello operating system properties for hello virtual machine</span></span>
<span data-ttu-id="f3680-199">이제는 준비 tooset hello 가상 컴퓨터의 운영 체제 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-199">Now we are ready tooset hello virtual machine's operating system properties.</span></span> <span data-ttu-id="f3680-200">Hello 사용 하 여 [집합 AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) cmdlet tooset hello Windows 운영 체제 유형을 hello [가상 컴퓨터 에이전트](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) 설치 toobe 해당 hello cmdlet을 사용 하면 자동 지정 업데이트 하 고 hello 가상 컴퓨터 이름, hello 컴퓨터 이름 및 이전에 초기화 하는 hello 변수를 사용 하 여 hello 자격 증명을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-200">We will use hello [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) cmdlet tooset hello type of operating system as Windows, require hello [virtual machine agent](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toobe installed, specify that hello cmdlet enables auto update and set hello virtual machine name, hello computer name, and hello credential using hello variables that you previously initialized.</span></span>

<span data-ttu-id="f3680-201">다음과 같은 가상 컴퓨터에 대 한 cmdlet tooset hello 운영 체제 속성 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-201">Execute hello following cmdlet tooset hello operating system properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate

### <a name="add-hello-network-interface-toohello-virtual-machine"></a><span data-ttu-id="f3680-202">Hello 네트워크 인터페이스 toohello 가상 컴퓨터 추가</span><span class="sxs-lookup"><span data-stu-id="f3680-202">Add hello network interface toohello virtual machine</span></span>
<span data-ttu-id="f3680-203">다음으로 hello 네트워크 인터페이스는 앞서 만든 toohello 가상 컴퓨터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-203">Next, we will add hello network interface that we created previously toohello virtual machine.</span></span> <span data-ttu-id="f3680-204">Hello 사용 하 여 [추가 AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) 앞에서 정의한 hello 네트워크 인터페이스 변수를 사용 하 여 cmdlet tooadd hello 네트워크 인터페이스.</span><span class="sxs-lookup"><span data-stu-id="f3680-204">We will use hello [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) cmdlet tooadd hello network interface using hello network interface variable that you defined earlier.</span></span>

<span data-ttu-id="f3680-205">가상 컴퓨터에 대 한 cmdlet tooset hello 네트워크 인터페이스를 수행 하는 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-205">Execute hello following cmdlet tooset hello network interface for your virtual machine.</span></span>

    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id

### <a name="set-hello-blob-storage-location-for-hello-disk-toobe-used-by-hello-virtual-machine"></a><span data-ttu-id="f3680-206">Hello 디스크 toobe hello 가상 컴퓨터에서 사용에 대 한 hello blob 저장소 위치 설정</span><span class="sxs-lookup"><span data-stu-id="f3680-206">Set hello blob storage location for hello disk toobe used by hello virtual machine</span></span>
<span data-ttu-id="f3680-207">다음으로, 앞에서 정의한 hello 변수를 사용 하 여 hello 가상 컴퓨터에서 사용 하는 hello 디스크 toobe에 대 한 hello blob 저장소 위치를 설정 해 드립니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-207">Next, we will set hello blob storage location for hello disk toobe used by hello virtual machine using hello variables that you defined earlier.</span></span>

<span data-ttu-id="f3680-208">Hello 수정할 수 있는 cmdlet tooset hello blob 저장소 위치를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-208">Execute hello following cmdlet tooset hello blob storage location.</span></span>

    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"

### <a name="set-hello-operating-system-disk-properties-for-hello-virtual-machine"></a><span data-ttu-id="f3680-209">Hello 운영 체제 디스크 속성 hello 가상 컴퓨터에 대 한 설정</span><span class="sxs-lookup"><span data-stu-id="f3680-209">Set hello operating system disk properties for hello virtual machine</span></span>
<span data-ttu-id="f3680-210">다음으로 설정 해 드립니다 hello 운영 체제 디스크 속성 hello 가상 컴퓨터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-210">Next, we will set hello operating system disk properties for hello virtual machine.</span></span> <span data-ttu-id="f3680-211">Hello를 사용 합니다 [집합 AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) hello 가상 컴퓨터용 운영 체제 hello cmdlet toospecify 이미지로 tooset tooread만 캐시에서 제공 됩니다 (hello에 SQL Server를 설치 하기 때문에 동일한 디스크) 및 정의 hello 가상 컴퓨터 이름과 hello 운영 체제 디스크는 앞에서 정의한 hello 변수를 사용 하 여 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-211">We will use hello [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) cmdlet toospecify that hello operating system for hello virtual machine will come from an image, tooset caching tooread only (because SQL Server is being installed on hello same disk) and define hello virtual machine name and hello operating system disk defined using hello variables that we defined earlier.</span></span>

<span data-ttu-id="f3680-212">다음과 같은 가상 컴퓨터에 대 한 cmdlet tooset hello 운영 체제 디스크 속성 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-212">Execute hello following cmdlet tooset hello operating system disk properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

### <a name="specify-hello-platform-image-for-hello-virtual-machine"></a><span data-ttu-id="f3680-213">Hello 가상 컴퓨터에 대 한 hello 플랫폼 이미지를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-213">Specify hello platform image for hello virtual machine</span></span>
<span data-ttu-id="f3680-214">수행할 마지막 구성 단계는 가상 컴퓨터에 대 한 toospecify hello 플랫폼 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-214">Our last configuration step is toospecify hello platform image for our virtual machine.</span></span> <span data-ttu-id="f3680-215">이 자습서에 대 한 hello 최신 SQL Server 2016 CTP 이미지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-215">For our tutorial, we are using hello latest SQL Server 2016 CTP image.</span></span> <span data-ttu-id="f3680-216">Hello 사용 하 여 [집합 AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet toouse 앞에서 정의한 hello 변수에 의해 정의 된 대로이 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-216">We will use hello [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet toouse this image as defined by hello variables that you defined earlier.</span></span>

<span data-ttu-id="f3680-217">가상 컴퓨터에 대 한 cmdlet toospecify hello 플랫폼 이미지를 수행 하는 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-217">Execute hello following cmdlet toospecify hello platform image for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

## <a name="create-hello-sql-vm"></a><span data-ttu-id="f3680-218">Hello SQL VM 만들기</span><span class="sxs-lookup"><span data-stu-id="f3680-218">Create hello SQL VM</span></span>
<span data-ttu-id="f3680-219">이제 hello 구성 단계를 완료 했으면 준비 toocreate hello 가상 컴퓨터는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-219">Now that you have finished hello configuration steps, you are ready toocreate hello virtual machine.</span></span> <span data-ttu-id="f3680-220">Hello 사용 하 여 [새로 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) 정의한 hello 변수를 사용 하 여 cmdlet toocreate hello 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="f3680-220">We will use hello [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) cmdlet toocreate hello virtual machine using hello variables that we have defined.</span></span>

<span data-ttu-id="f3680-221">다음 cmdlet toocreate hello 가상 컴퓨터를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-221">Execute hello following cmdlet toocreate your virtual machine.</span></span>

    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

<span data-ttu-id="f3680-222">hello 가상 컴퓨터가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-222">hello virtual machine is created.</span></span> <span data-ttu-id="f3680-223">공지 hello hello 가상 컴퓨터의 디스크에 대 한 저장소 계정을 지정 하기 때문에 부팅 진단에 대 한 표준 저장소 계정이 만들어졌는지 프리미엄 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-223">Notice that a standard storage account is created for boot diagnostics because hello specified storage account for hello virtual machine's disk is a premium storage account.</span></span>

<span data-ttu-id="f3680-224">이제 hello Azure 포털 toosee에서이 컴퓨터를 볼 수 있습니다 [공용 IP 주소 및 정규화 된 도메인 이름](virtual-machines-windows-portal-sql-server-provision.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-224">You can now view this machine in hello Azure Portal toosee [its public IP address and its fully qualified domain name](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="example-script"></a><span data-ttu-id="f3680-225">예제 스크립트</span><span class="sxs-lookup"><span data-stu-id="f3680-225">Example script</span></span>
<span data-ttu-id="f3680-226">hello 다음 스크립트 hello 전체 PowerShell 스크립트를 포함이 자습서에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-226">hello following script contains hello complete PowerShell script for this tutorial.</span></span> <span data-ttu-id="f3680-227">이 있다고 가정 이미 hello로 설치 hello Azure 구독 toouse **추가 AzureRmAccount** 및 **선택 AzureRmSubscription** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-227">It assumes that you have already setup hello Azure subscription toouse with hello **Add-AzureRmAccount** and **Select-AzureRmSubscription** commands.</span></span>

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
    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."
    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate #-TimeZone = $TimeZone
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

    # Image
    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

    ## Create hello VM in Azure
    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

## <a name="next-steps"></a><span data-ttu-id="f3680-228">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f3680-228">Next steps</span></span>
<span data-ttu-id="f3680-229">Hello 가상 컴퓨터를 만든 후에 설치 프로그램 및 RDP 연결을 사용 하 여 준비 tooconnect toohello 가상 컴퓨터는.</span><span class="sxs-lookup"><span data-stu-id="f3680-229">After hello virtual machine is created, you are ready tooconnect toohello virtual machine using RDP and setup connectivity.</span></span> <span data-ttu-id="f3680-230">자세한 내용은 참조 [tooa (리소스 관리자) Azure에서 SQL Server 가상 컴퓨터를 연결](virtual-machines-windows-sql-connect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f3680-230">For more information, see [Connect tooa SQL Server Virtual Machine on Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).</span></span>

