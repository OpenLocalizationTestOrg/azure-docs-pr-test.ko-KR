---
title: "aaaTroubleshoot Azure 가상 네트워크 게이트웨이 및 연결-PowerShell | Microsoft Docs"
description: "이 페이지에서는 toouse hello Azure 네트워크 감시자 PowerShell cmdlet을 해결 하는 방법을 설명 합니다."
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
ms.openlocfilehash: b7dbe6e44e0fa1ea0481223a84098d7a57c068a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="a7fa8-103">Azure Network Watcher PowerShell을 사용하여 Virtual Network 게이트웨이 및 연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="a7fa8-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="a7fa8-104">포털</span><span class="sxs-lookup"><span data-stu-id="a7fa8-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="a7fa8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a7fa8-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="a7fa8-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a7fa8-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="a7fa8-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a7fa8-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="a7fa8-108">REST API</span><span class="sxs-lookup"><span data-stu-id="a7fa8-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="a7fa8-109">네트워크 감시자 toounderstanding Azure의 네트워크 리소스 관련해 서 다양 한 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7fa8-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="a7fa8-110">이러한 기능 중 하나는 리소스 문제 해결입니다.</span><span class="sxs-lookup"><span data-stu-id="a7fa8-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="a7fa8-111">리소스 문제를 해결 하는 hello 포털, PowerShell, CLI 또는 REST API를 통해 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7fa8-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="a7fa8-112">호출 되 면 네트워크 감시자 가상 네트워크 게이트웨이 또는 연결의 hello 상태를 검사 하 고 해당 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7fa8-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a7fa8-113">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="a7fa8-113">Before you begin</span></span>

<span data-ttu-id="a7fa8-114">이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7fa8-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="a7fa8-115">지원되는 게이트웨이 유형 목록을 보려면 [지원되는 게이트웨이 유형](network-watcher-troubleshoot-overview.md#supported-gateway-types)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="a7fa8-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="a7fa8-116">개요</span><span class="sxs-lookup"><span data-stu-id="a7fa8-116">Overview</span></span>

<span data-ttu-id="a7fa8-117">Hello 기능을 제공 리소스 문제 해결 가상 네트워크 게이트웨이 및 연결 때 발생 하는 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7fa8-117">Resource troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="a7fa8-118">요청이 이루어지면 tooresource 문제 해결 로그 되는 쿼리 및 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7fa8-118">When a request is made tooresource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="a7fa8-119">검사 완료 되 면 hello 결과가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7fa8-119">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="a7fa8-120">결과 여러 분 tooreturn를 수행할 수 있는 리소스 문제 해결 요청은 장기 실행 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7fa8-120">Resource troubleshooting requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="a7fa8-121">문제 해결에서 hello 로그에 지정 된 저장소 계정에 대 한 컨테이너에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7fa8-121">hello logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="a7fa8-122">Network Watcher 검색</span><span class="sxs-lookup"><span data-stu-id="a7fa8-122">Retrieve Network Watcher</span></span>

<span data-ttu-id="a7fa8-123">hello 첫 번째 단계는 tooretrieve hello 네트워크 감시자 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="a7fa8-123">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="a7fa8-124">hello `$networkWatcher` 변수 toohello 전달 `Start-AzureRmNetworkWatcherResourceTroubleshooting` 4 단계에서 cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a7fa8-124">hello `$networkWatcher` variable is passed toohello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="a7fa8-125">Virtual Network 게이트웨이 연결 검색</span><span class="sxs-lookup"><span data-stu-id="a7fa8-125">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="a7fa8-126">이 예제에서 리소스 문제 해결은 연결에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7fa8-126">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="a7fa8-127">Virtual Network 게이트웨이를 전달할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7fa8-127">You can also pass it a Virtual Network Gateway.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "2to3" -ResourceGroupName "testrg"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="a7fa8-128">저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="a7fa8-128">Create a storage account</span></span>

<span data-ttu-id="a7fa8-129">Hello 리소스의 hello 상태에 대 한 데이터를 반환 리소스 문제 해결, 로그 tooa 저장소 계정 toobe 검토를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7fa8-129">Resource troubleshooting returns data about hello health of hello resource, it also saves logs tooa storage account toobe reviewed.</span></span> <span data-ttu-id="a7fa8-130">이 단계에서는 저장소 계정을 만듭니다. 기존 저장소 계정이 있는 경우 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7fa8-130">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

```powershell
$sa = New-AzureRmStorageAccount -Name "contosoexamplesa" -SKU "Standard_LRS" -ResourceGroupName "testrg" -Location "WestCentralUS"
Set-AzureRmCurrentStorageAccount -ResourceGroupName $sa.ResourceGroupName -Name $sa.StorageAccountName
$sc = New-AzureStorageContainer -Name logs
```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="a7fa8-131">Network Watcher 리소스 문제 해결 실행</span><span class="sxs-lookup"><span data-stu-id="a7fa8-131">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="a7fa8-132">Hello 사용 하 여 리소스 문제를 해결 `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a7fa8-132">You troubleshoot resources with hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet.</span></span> <span data-ttu-id="a7fa8-133">Hello cmdlet hello 네트워크 감시자 개체, hello hello 연결의 Id 또는 가상 네트워크 게이트웨이, hello 저장소 계정 id 및 hello 경로 toostore hello 결과 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="a7fa8-133">We pass hello cmdlet hello Network Watcher object, hello Id of hello Connection or Virtual Network Gateway, hello storage account id, and hello path toostore hello results.</span></span>

> [!NOTE]
> <span data-ttu-id="a7fa8-134">hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet 오래 실행 되 고 몇 분 toocomplete 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7fa8-134">hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet is long running and may take a few minutes toocomplete.</span></span>

```powershell
Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath "$($sa.PrimaryEndpoints.Blob)$($sc.name)"
```

<span data-ttu-id="a7fa8-135">Hello cmdlet을 실행 한 후 네트워크 감시자 hello 리소스 tooverify hello 상태를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7fa8-135">Once you run hello cmdlet, Network Watcher reviews hello resource tooverify hello health.</span></span> <span data-ttu-id="a7fa8-136">Toohello 셸 hello 결과 반환 합니다. 지정 된 hello 저장소 계정에 hello 결과의 로그를 보관 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7fa8-136">It returns hello results toohello shell and stores logs of hello results in hello storage account specified.</span></span>

## <a name="understanding-hello-results"></a><span data-ttu-id="a7fa8-137">Hello 결과 이해</span><span class="sxs-lookup"><span data-stu-id="a7fa8-137">Understanding hello results</span></span>

<span data-ttu-id="a7fa8-138">hello 동작 텍스트 tooresolve 문제 hello 하는 방법에 대 한 일반적인 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7fa8-138">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="a7fa8-139">Hello 문제에 대 한 작업을 수행할 수, 링크를 추가 하는 지침과 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7fa8-139">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="a7fa8-140">Hello 경우에서 hello 응답을 자세한 지침은 없으며가 있는 hello url tooopen 지원 사례를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7fa8-140">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="a7fa8-141">Hello 응답 및 포함 된 항목의 hello 속성에 대 한 자세한 내용은 방문 [네트워크 감시자 문제 해결 개요](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a7fa8-141">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="a7fa8-142">Azure 저장소 계정에서 파일을 다운로드 하는 방법은 참조 너무[.NET을 사용 하 여 Azure Blob 저장소 시작](../storage/blobs/storage-dotnet-how-to-use-blobs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a7fa8-142">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="a7fa8-143">사용할 수 있는 다른 도구는 저장소 탐색기입니다.</span><span class="sxs-lookup"><span data-stu-id="a7fa8-143">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="a7fa8-144">저장소 탐색기에 대 한 자세한 내용은 여기에 있습니다 링크 hello: [저장소 탐색기](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="a7fa8-144">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7fa8-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a7fa8-145">Next steps</span></span>

<span data-ttu-id="a7fa8-146">해당 중지 VPN 연결 설정이 변경 되었으며, 참조 [네트워크 보안 그룹 관리](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack 아래로 hello 네트워크 보안 그룹 및 보안 규칙을 문제가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7fa8-146">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
