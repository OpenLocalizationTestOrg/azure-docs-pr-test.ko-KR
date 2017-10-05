---
title: "Azure Virtual Network 게이트웨이 및 연결 문제 해결 - PowerShell | Microsoft Docs"
description: "이 페이지에서는 Azure Network Watcher 문제 해결 PowerShell cmdlet을 사용하는 방법을 설명합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: f6f0a813-38b6-4a1f-8cfc-1dfdf979f595
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: 0bdffbac18d1d236b7674feed4dbc784e50e0ea8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="84b1b-103">Azure Network Watcher PowerShell을 사용하여 Virtual Network 게이트웨이 및 연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="84b1b-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="84b1b-104">포털</span><span class="sxs-lookup"><span data-stu-id="84b1b-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="84b1b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="84b1b-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="84b1b-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="84b1b-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="84b1b-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="84b1b-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="84b1b-108">REST API</span><span class="sxs-lookup"><span data-stu-id="84b1b-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="84b1b-109">Network Watcher는 Azure에서 네트워크 리소스를 이해하는 데 관련된 다양한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="84b1b-109">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="84b1b-110">이러한 기능 중 하나는 리소스 문제 해결입니다.</span><span class="sxs-lookup"><span data-stu-id="84b1b-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="84b1b-111">리소스 문제 해결은 포털, PowerShell, CLI 또는 REST API를 통해 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b1b-111">Resource troubleshooting can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="84b1b-112">Network Watcher가 호출되면 Virtual Network 게이트웨이 또는 연결의 상태를 검사하거나 해당 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="84b1b-112">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="84b1b-113">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="84b1b-113">Before you begin</span></span>

<span data-ttu-id="84b1b-114">이 시나리오에서는 사용자가 Network Watcher를 만드는 [Network Watcher 만들기](network-watcher-create.md)의 단계를 이미 수행했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="84b1b-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

<span data-ttu-id="84b1b-115">지원되는 게이트웨이 유형 목록을 보려면 [지원되는 게이트웨이 유형](network-watcher-troubleshoot-overview.md#supported-gateway-types)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="84b1b-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="84b1b-116">개요</span><span class="sxs-lookup"><span data-stu-id="84b1b-116">Overview</span></span>

<span data-ttu-id="84b1b-117">리소스 문제 해결은 Virtual Network 게이트웨이 및 연결에 발생한 문제를 해결하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="84b1b-117">Resource troubleshooting provides the ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="84b1b-118">리소스 문제 해결을 요청하는 경우 로그를 쿼리하고 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="84b1b-118">When a request is made to resource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="84b1b-119">검사가 완료되면 결과가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b1b-119">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="84b1b-120">리소스 문제 해결 요청은 장기 실행 요청이며 결과를 반환하는 데 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b1b-120">Resource troubleshooting requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="84b1b-121">문제를 해결하는 로그는 지정된 저장소 계정의 컨테이너에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b1b-121">The logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="84b1b-122">Network Watcher 검색</span><span class="sxs-lookup"><span data-stu-id="84b1b-122">Retrieve Network Watcher</span></span>

<span data-ttu-id="84b1b-123">첫 번째 단계는 Network Watcher 인스턴스를 검색하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="84b1b-123">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="84b1b-124">`$networkWatcher` 변수는 4단계에서 `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b1b-124">The `$networkWatcher` variable is passed to the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="84b1b-125">Virtual Network 게이트웨이 연결 검색</span><span class="sxs-lookup"><span data-stu-id="84b1b-125">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="84b1b-126">이 예제에서 리소스 문제 해결은 연결에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b1b-126">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="84b1b-127">Virtual Network 게이트웨이를 전달할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b1b-127">You can also pass it a Virtual Network Gateway.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "2to3" -ResourceGroupName "testrg"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="84b1b-128">저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="84b1b-128">Create a storage account</span></span>

<span data-ttu-id="84b1b-129">리소스 문제 해결은 리소스의 상태에 대한 데이터를 반환하고 검토할 저장소 계정에 로그를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="84b1b-129">Resource troubleshooting returns data about the health of the resource, it also saves logs to a storage account to be reviewed.</span></span> <span data-ttu-id="84b1b-130">이 단계에서는 저장소 계정을 만듭니다. 기존 저장소 계정이 있는 경우 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b1b-130">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

```powershell
$sa = New-AzureRmStorageAccount -Name "contosoexamplesa" -SKU "Standard_LRS" -ResourceGroupName "testrg" -Location "WestCentralUS"
Set-AzureRmCurrentStorageAccount -ResourceGroupName $sa.ResourceGroupName -Name $sa.StorageAccountName
$sc = New-AzureStorageContainer -Name logs
```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="84b1b-131">Network Watcher 리소스 문제 해결 실행</span><span class="sxs-lookup"><span data-stu-id="84b1b-131">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="84b1b-132">`Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet을 사용하여 리소스의 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="84b1b-132">You troubleshoot resources with the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet.</span></span> <span data-ttu-id="84b1b-133">Network Watcher 개체, 연결 또는 Virtual Network 게이트웨이 ID, 저장소 계정의 ID 및 결과를 저장할 경로에 cmdlet을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="84b1b-133">We pass the cmdlet the Network Watcher object, the Id of the Connection or Virtual Network Gateway, the storage account id, and the path to store the results.</span></span>

> [!NOTE]
> <span data-ttu-id="84b1b-134">`Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet은 장기 실행되며 완료하는 데 몇 분이 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b1b-134">The `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet is long running and may take a few minutes to complete.</span></span>

```powershell
Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath "$($sa.PrimaryEndpoints.Blob)$($sc.name)"
```

<span data-ttu-id="84b1b-135">cmdlet을 실행하면 Network Watcher는 리소스를 검토하여 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="84b1b-135">Once you run the cmdlet, Network Watcher reviews the resource to verify the health.</span></span> <span data-ttu-id="84b1b-136">셸에 결과를 반환하고 지정된 저장소 계정에 결과 로그를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="84b1b-136">It returns the results to the shell and stores logs of the results in the storage account specified.</span></span>

## <a name="understanding-the-results"></a><span data-ttu-id="84b1b-137">결과 이해</span><span class="sxs-lookup"><span data-stu-id="84b1b-137">Understanding the results</span></span>

<span data-ttu-id="84b1b-138">작업 텍스트에서는 문제를 해결하는 방법에 대한 일반적인 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="84b1b-138">The action text provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="84b1b-139">문제에 대한 조치를 취할 수 있는 경우 링크는 추가 설명서와 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b1b-139">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="84b1b-140">추가 지침이 없는 경우에 응답은 지원 사례를 열 URL을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="84b1b-140">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="84b1b-141">응답의 속성 및 포함된 항목에 대한 자세한 내용은 [Network Watcher 문제 해결 개요](network-watcher-troubleshoot-overview.md)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="84b1b-141">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="84b1b-142">Azure Storage 계정에서 파일을 다운로드하는 방법에 대한 지침은 [.NET을 사용하여 Azure Blob Storage 시작](../storage/blobs/storage-dotnet-how-to-use-blobs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="84b1b-142">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="84b1b-143">사용할 수 있는 다른 도구는 저장소 탐색기입니다.</span><span class="sxs-lookup"><span data-stu-id="84b1b-143">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="84b1b-144">저장소 탐색기에 대한 자세한 내용은 여기에 있는 [저장소 탐색기](http://storageexplorer.com/) 링크에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b1b-144">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="84b1b-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="84b1b-145">Next steps</span></span>

<span data-ttu-id="84b1b-146">VPN 연결을 중지하도록 설정이 변경된 경우 [네트워크 보안 그룹 관리](../virtual-network/virtual-network-manage-nsg-arm-portal.md)를 참조하여 문제가 될 수 있는 네트워크 보안 그룹 및 보안 규칙을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="84b1b-146">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>
