---
title: "Azure Virtual Network 게이트웨이 및 연결 문제 해결 - Azure CLI 1.0 | Microsoft Docs"
description: "이 페이지에서는 Azure Network Watcher 문제 해결 Azure CLI 1.0을 사용하는 방법을 설명합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2838bc61-b182-4da8-8533-27db8fdbd177
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: 9de4b2a0bdda7ffbd269883877a708d67312092f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-10"></a><span data-ttu-id="f1b9e-103">Azure Network Watcher Azure CLI 1.0을 사용하여 Virtual Network 게이트웨이 및 연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="f1b9e-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="f1b9e-104">포털</span><span class="sxs-lookup"><span data-stu-id="f1b9e-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="f1b9e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1b9e-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="f1b9e-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f1b9e-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="f1b9e-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f1b9e-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="f1b9e-108">REST API</span><span class="sxs-lookup"><span data-stu-id="f1b9e-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="f1b9e-109">Network Watcher는 Azure에서 네트워크 리소스를 이해하는 데 관련된 다양한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-109">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="f1b9e-110">이러한 기능 중 하나는 리소스 문제 해결입니다.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="f1b9e-111">리소스 문제 해결은 포털, PowerShell, CLI 또는 REST API를 통해 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-111">Resource troubleshooting can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="f1b9e-112">Network Watcher가 호출되면 Virtual Network 게이트웨이 또는 연결의 상태를 검사하거나 해당 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-112">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="f1b9e-113">이 문서에서는 Windows, Mac 및 Linux에 사용할 수 있는 플랫폼 간 Azure CLI 1.0을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-113">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="f1b9e-114">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="f1b9e-114">Before you begin</span></span>

<span data-ttu-id="f1b9e-115">이 시나리오에서는 사용자가 Network Watcher를 만드는 [Network Watcher 만들기](network-watcher-create.md)의 단계를 이미 수행했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

<span data-ttu-id="f1b9e-116">지원되는 게이트웨이 유형 목록을 보려면 [지원되는 게이트웨이 유형](/network-watcher-troubleshoot-overview.md#supported-gateway-types)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-116">For a list of supported gateway types visit, [Supported Gateway types](/network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="f1b9e-117">개요</span><span class="sxs-lookup"><span data-stu-id="f1b9e-117">Overview</span></span>

<span data-ttu-id="f1b9e-118">리소스 문제 해결은 Virtual Network 게이트웨이 및 연결에 발생한 문제를 해결하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-118">Resource troubleshooting provides the ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="f1b9e-119">리소스 문제 해결을 요청하는 경우 로그를 쿼리하고 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-119">When a request is made to resource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="f1b9e-120">검사가 완료되면 결과가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-120">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="f1b9e-121">리소스 문제 해결 요청은 장기 실행 요청이며 결과를 반환하는 데 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-121">Resource troubleshooting requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="f1b9e-122">문제를 해결하는 로그는 지정된 저장소 계정의 컨테이너에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-122">The logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="f1b9e-123">Virtual Network 게이트웨이 연결 검색</span><span class="sxs-lookup"><span data-stu-id="f1b9e-123">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="f1b9e-124">이 예제에서 리소스 문제 해결은 연결에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-124">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="f1b9e-125">Virtual Network 게이트웨이를 전달할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-125">You can also pass it a Virtual Network Gateway.</span></span> <span data-ttu-id="f1b9e-126">다음 cmdlet은 리소스 그룹에서 VPN 연결을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-126">The following cmdlet lists the vpn-connections in a resource group.</span></span>

```azurecli
azure network vpn-connection list -g resourceGroupName
```

<span data-ttu-id="f1b9e-127">구독에서 연결을 참조하는 명령을 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-127">You can also run the command to see the connections in a subscription.</span></span>

```azurecli
azure network vpn-connection list -s subscription
```

<span data-ttu-id="f1b9e-128">연결의 이름이 있으면 해당 리소스 ID를 가져오기 위해 이 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-128">Once you have the name of the connection, you can run this command to get its resource Id:</span></span>

```azurecli
azure network vpn-connection show -g resourceGroupName -n connectionName
```

## <a name="create-a-storage-account"></a><span data-ttu-id="f1b9e-129">저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="f1b9e-129">Create a storage account</span></span>

<span data-ttu-id="f1b9e-130">리소스 문제 해결은 리소스의 상태에 대한 데이터를 반환하고 검토할 저장소 계정에 로그를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-130">Resource troubleshooting returns data about the health of the resource, it also saves logs to a storage account to be reviewed.</span></span> <span data-ttu-id="f1b9e-131">이 단계에서는 저장소 계정을 만듭니다. 기존 저장소 계정이 있는 경우 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-131">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

1. <span data-ttu-id="f1b9e-132">저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="f1b9e-132">Create the storage account</span></span>

    ```azurecli
    azure storage account create -n storageAccountName -l location -g resourceGroupName
    ```

1. <span data-ttu-id="f1b9e-133">저장소 계정 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="f1b9e-133">Get the storage account keys</span></span>

    ```azurecli
    azure storage account keys list storageAccountName -g resourcegroupName
    ```

1. <span data-ttu-id="f1b9e-134">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="f1b9e-134">Create the container</span></span>

    ```azurecli
    azure storage container create --account-name storageAccountName -g resourcegroupName --account-key {storageAccountKey} --container logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="f1b9e-135">Network Watcher 리소스 문제 해결 실행</span><span class="sxs-lookup"><span data-stu-id="f1b9e-135">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="f1b9e-136">`network watcher troubleshoot` cmdlet을 사용하여 리소스의 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-136">You troubleshoot resources with the `network watcher troubleshoot` cmdlet.</span></span> <span data-ttu-id="f1b9e-137">리소스 그룹, Network Watcher의 이름, 연결의 ID, 저장소 계정의 ID 및 Blob에 대한 경로에 cmdlet을 전달하여 문제 해결 결과를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-137">We pass the cmdlet the resource group, the name of the Network Watcher, the Id of the connection, the Id of the storage account, and the path to the blob to store the troubleshoot results in.</span></span>

```azurecli
azure network watcher troubleshoot -g resourceGroupName -n networkWatcherName -t connectionId -i storageId -p storagePath
```

<span data-ttu-id="f1b9e-138">cmdlet을 실행하면 Network Watcher는 리소스를 검토하여 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-138">Once you run the cmdlet, Network Watcher reviews the resource to verify the health.</span></span> <span data-ttu-id="f1b9e-139">셸에 결과를 반환하고 지정된 저장소 계정에 결과 로그를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-139">It returns the results to the shell and stores logs of the results in the storage account specified.</span></span>

## <a name="understanding-the-results"></a><span data-ttu-id="f1b9e-140">결과 이해</span><span class="sxs-lookup"><span data-stu-id="f1b9e-140">Understanding the results</span></span>

<span data-ttu-id="f1b9e-141">작업 텍스트에서는 문제를 해결하는 방법에 대한 일반적인 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-141">The action text provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="f1b9e-142">문제에 대한 조치를 취할 수 있는 경우 링크는 추가 설명서와 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-142">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="f1b9e-143">추가 지침이 없는 경우에 응답은 지원 사례를 열 URL을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-143">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="f1b9e-144">응답의 속성 및 포함된 항목에 대한 자세한 내용은 [Network Watcher 문제 해결 개요](network-watcher-troubleshoot-overview.md)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-144">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="f1b9e-145">Azure Storage 계정에서 파일을 다운로드하는 방법에 대한 지침은 [.NET을 사용하여 Azure Blob Storage 시작](../storage/blobs/storage-dotnet-how-to-use-blobs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-145">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="f1b9e-146">사용할 수 있는 다른 도구는 저장소 탐색기입니다.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-146">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="f1b9e-147">저장소 탐색기에 대한 자세한 내용은 여기에 있는 [저장소 탐색기](http://storageexplorer.com/) 링크에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-147">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1b9e-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f1b9e-148">Next steps</span></span>

<span data-ttu-id="f1b9e-149">VPN 연결을 중지하도록 설정이 변경된 경우 [네트워크 보안 그룹 관리](../virtual-network/virtual-network-manage-nsg-arm-portal.md)를 참조하여 문제가 될 수 있는 네트워크 보안 그룹 및 보안 규칙을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b9e-149">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>
