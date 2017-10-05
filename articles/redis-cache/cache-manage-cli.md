---
title: "Azure CLI를 사용하여 Azure Redis Cache 관리 | Microsoft Docs"
description: "모든 플랫폼에서 Azure CLI를 설치하고, Azure CLI를 사용하여 Azure 계정에 연결하고, Azure CLI에서 Redis cache를 만들고 관리하는 방법에 대해 알아봅니다."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 964ff245-859d-4bc1-bccf-62e4b3c1169f
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: ba078a870a3998568170cc197bd6698b97b7fadb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-manage-azure-redis-cache-using-the-azure-command-line-interface-azure-cli"></a><span data-ttu-id="9b850-103">Azure 명령줄 인터페이스(Azure CLI)를 사용하여 Azure Redis Cache를 만들고 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="9b850-103">How to create and manage Azure Redis Cache using the Azure Command-Line Interface (Azure CLI)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9b850-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b850-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="9b850-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9b850-105">Azure CLI</span></span>](cache-manage-cli.md)
>
>

<span data-ttu-id="9b850-106">Azure CLI를 사용하면 어떤 플랫폼에서나 Azure 인프라를 효율적으로 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-106">The Azure CLI is a great way to manage your Azure infrastructure from any platform.</span></span> <span data-ttu-id="9b850-107">이 문서에서는 Azure CLI를 사용하여 Azure Redis Cache 인스턴스를 만들고 관리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-107">This article shows you how to create and manage your Azure Redis Cache instances using the Azure CLI.</span></span>

> [!NOTE]
> <span data-ttu-id="9b850-108">이 문서는 이전 버전의 Azure CLI에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-108">This article applies to a previous version of Azure CLI.</span></span> <span data-ttu-id="9b850-109">최신 Azure CLI 2.0 샘플 스크립트에 대해서는 [Azure CLI Redis Cache 샘플](cli-samples.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9b850-109">For the latest Azure CLI 2.0 sample scripts, see [Azure CLI Redis cache samples](cli-samples.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="9b850-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9b850-110">Prerequisites</span></span>
<span data-ttu-id="9b850-111">Azure CLI를 사용하여 Azure Redis Cache 인스턴스를 만들고 관리하려면 다음 단계를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-111">To create and manage Azure Redis Cache instances using Azure CLI, you must complete the following steps.</span></span>

* <span data-ttu-id="9b850-112">Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-112">You must have an Azure account.</span></span> <span data-ttu-id="9b850-113">계정이 없는 경우 몇 분 만에 [무료 계정](https://azure.microsoft.com/pricing/free-trial/) 을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-113">If you don't have one, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a few moments.</span></span>
* <span data-ttu-id="9b850-114">[Azure CLI를 설치합니다](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="9b850-114">[Install the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="9b850-115">Azure CLI 설치를 개인 Azure 계정이나 회사 또는 학교 Azure 계정에 연결하고 `azure login` 명령을 사용하여 Azure CLI에서 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-115">Connect your Azure CLI installation with a personal Azure account, or with a work or school Azure account, and log in from the Azure CLI using the `azure login` command.</span></span> <span data-ttu-id="9b850-116">차이점을 이해하고 선택하려면 [Azure CLI(Azure 명령줄 인터페이스)에서 Azure 구독 연결](../xplat-cli-connect.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9b850-116">To understand the differences and choose, see [Connect to an Azure subscription from the Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="9b850-117">다음 명령 중 하나를 실행하기 전에 `azure config mode arm` 명령을 실행하여 Azure CLI를 리소스 관리자 모드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-117">Before running any of the following commands, switch the Azure CLI into Resource Manager mode by running the `azure config mode arm` command.</span></span> <span data-ttu-id="9b850-118">자세한 내용은 [Azure 리소스 및 리소스 그룹 관리를 위해 Azure CLI 사용](../xplat-cli-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9b850-118">For more information, see [Use the Azure CLI to manage Azure resources and resource groups](../xplat-cli-azure-resource-manager.md).</span></span>

## <a name="redis-cache-properties"></a><span data-ttu-id="9b850-119">Redis Cache 속성</span><span class="sxs-lookup"><span data-stu-id="9b850-119">Redis Cache properties</span></span>
<span data-ttu-id="9b850-120">Redis Cache 인스턴스를 만들고 업데이트하는 경우에 다음 속성이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-120">The following properties are used when creating and updating Redis Cache instances.</span></span>

| <span data-ttu-id="9b850-121">속성</span><span class="sxs-lookup"><span data-stu-id="9b850-121">Property</span></span> | <span data-ttu-id="9b850-122">Switch</span><span class="sxs-lookup"><span data-stu-id="9b850-122">Switch</span></span> | <span data-ttu-id="9b850-123">설명</span><span class="sxs-lookup"><span data-stu-id="9b850-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9b850-124">name</span><span class="sxs-lookup"><span data-stu-id="9b850-124">name</span></span> |<span data-ttu-id="9b850-125">-n, --name</span><span class="sxs-lookup"><span data-stu-id="9b850-125">-n, --name</span></span> |<span data-ttu-id="9b850-126">Redis Cache의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-126">Name of the Redis Cache.</span></span> |
| <span data-ttu-id="9b850-127">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="9b850-127">resource group</span></span> |<span data-ttu-id="9b850-128">-g, --resource-group</span><span class="sxs-lookup"><span data-stu-id="9b850-128">-g, --resource-group</span></span> |<span data-ttu-id="9b850-129">리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-129">Name of the Resource Group.</span></span> |
| <span data-ttu-id="9b850-130">location</span><span class="sxs-lookup"><span data-stu-id="9b850-130">location</span></span> |<span data-ttu-id="9b850-131">-l, --location</span><span class="sxs-lookup"><span data-stu-id="9b850-131">-l, --location</span></span> |<span data-ttu-id="9b850-132">캐시를 만드는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-132">Location to create cache.</span></span> |
| <span data-ttu-id="9b850-133">size</span><span class="sxs-lookup"><span data-stu-id="9b850-133">size</span></span> |<span data-ttu-id="9b850-134">-z, --size</span><span class="sxs-lookup"><span data-stu-id="9b850-134">-z, --size</span></span> |<span data-ttu-id="9b850-135">Redis Cache의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-135">Size of the Redis Cache.</span></span> <span data-ttu-id="9b850-136">유효한 값: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span><span class="sxs-lookup"><span data-stu-id="9b850-136">Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span></span> |
| <span data-ttu-id="9b850-137">sku</span><span class="sxs-lookup"><span data-stu-id="9b850-137">sku</span></span> |<span data-ttu-id="9b850-138">-x, --sku</span><span class="sxs-lookup"><span data-stu-id="9b850-138">-x, --sku</span></span> |<span data-ttu-id="9b850-139">Redis SKU입니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-139">Redis SKU.</span></span> <span data-ttu-id="9b850-140">다음 중 하나여야 합니다. [기본, 표준, 프리미엄]</span><span class="sxs-lookup"><span data-stu-id="9b850-140">Should be one of : [Basic, Standard, Premium]</span></span> |
| <span data-ttu-id="9b850-141">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="9b850-141">EnableNonSslPort</span></span> |<span data-ttu-id="9b850-142">-e, --enable-non-ssl-port</span><span class="sxs-lookup"><span data-stu-id="9b850-142">-e, --enable-non-ssl-port</span></span> |<span data-ttu-id="9b850-143">Redis Cache의 EnableNonSslPort 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-143">EnableNonSslPort property of the Redis Cache.</span></span> <span data-ttu-id="9b850-144">캐시에 대해 비 SSL 포트를 사용하도록 설정하려는 경우 이 플래그를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-144">Add this flag if you want to enable the Non SSL Port for your cache</span></span> |
| <span data-ttu-id="9b850-145">Redis 구성</span><span class="sxs-lookup"><span data-stu-id="9b850-145">Redis Configuration</span></span> |<span data-ttu-id="9b850-146">-c, --redis-configuration</span><span class="sxs-lookup"><span data-stu-id="9b850-146">-c, --redis-configuration</span></span> |<span data-ttu-id="9b850-147">Redis 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-147">Redis Configuration.</span></span> <span data-ttu-id="9b850-148">구성 키 및 값의 JSON 형식 문자열을 여기에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-148">Enter a JSON formatted string of configuration keys and values here.</span></span> <span data-ttu-id="9b850-149">형식:"{"":"","":""}"</span><span class="sxs-lookup"><span data-stu-id="9b850-149">Format:"{"":"","":""}"</span></span> |
| <span data-ttu-id="9b850-150">Redis 구성</span><span class="sxs-lookup"><span data-stu-id="9b850-150">Redis Configuration</span></span> |<span data-ttu-id="9b850-151">-f, --redis-configuration-file</span><span class="sxs-lookup"><span data-stu-id="9b850-151">-f, --redis-configuration-file</span></span> |<span data-ttu-id="9b850-152">Redis 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-152">Redis Configuration.</span></span> <span data-ttu-id="9b850-153">구성 키 및 값이 있는 파일의 경로를 여기에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-153">Enter the path of a file containing configuration keys and values here.</span></span> <span data-ttu-id="9b850-154">파일 항목에 대한 형식: {"":"","":""}</span><span class="sxs-lookup"><span data-stu-id="9b850-154">Format for the file entry: {"":"","":""}</span></span> |
| <span data-ttu-id="9b850-155">분할된 데이터베이스 수</span><span class="sxs-lookup"><span data-stu-id="9b850-155">Shard Count</span></span> |<span data-ttu-id="9b850-156">-r, --shard-count</span><span class="sxs-lookup"><span data-stu-id="9b850-156">-r, --shard-count</span></span> |<span data-ttu-id="9b850-157">클러스터링을 사용하는 프리미엄 클러스터 캐시에서 만드는 분할된 데이터베이스 수입니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-157">Number of Shards to create on a Premium Cluster Cache with clustering.</span></span> |
| <span data-ttu-id="9b850-158">가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="9b850-158">Virtual Network</span></span> |<span data-ttu-id="9b850-159">-v, --virtual-network</span><span class="sxs-lookup"><span data-stu-id="9b850-159">-v, --virtual-network</span></span> |<span data-ttu-id="9b850-160">VNET에서 캐시를 호스트하는 경우 Redis Cache를 배포하는 가상 네트워크의 정확한 ARM 리소스 ID를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-160">When hosting your cache in a VNET, specifies the exact ARM resource ID of the virtual network to deploy the redis cache in.</span></span> <span data-ttu-id="9b850-161">형식 예: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="9b850-161">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="9b850-162">키 유형</span><span class="sxs-lookup"><span data-stu-id="9b850-162">key type</span></span> |<span data-ttu-id="9b850-163">-t, --key-type</span><span class="sxs-lookup"><span data-stu-id="9b850-163">-t, --key-type</span></span> |<span data-ttu-id="9b850-164">갱신하는 키의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-164">Type of key to renew.</span></span> <span data-ttu-id="9b850-165">유효한 값: [주, 보조]</span><span class="sxs-lookup"><span data-stu-id="9b850-165">Valid values: [Primary, Secondary]</span></span> |
| <span data-ttu-id="9b850-166">StaticIP</span><span class="sxs-lookup"><span data-stu-id="9b850-166">StaticIP</span></span> |<span data-ttu-id="9b850-167">-p, --static-ip <static-ip></span><span class="sxs-lookup"><span data-stu-id="9b850-167">-p, --static-ip <static-ip></span></span> |<span data-ttu-id="9b850-168">VNET에서 캐시를 호스팅하는 경우 서브넷에서 캐시에 대한 고유 IP 주소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-168">When hosting your cache in a VNET, specifies a unique IP address in the subnet for the cache.</span></span> <span data-ttu-id="9b850-169">제공되지 않으면 하나의 IP 주소가 서브넷에서 자동으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-169">If not provided, one is chosen for you from the subnet.</span></span> |
| <span data-ttu-id="9b850-170">서브넷</span><span class="sxs-lookup"><span data-stu-id="9b850-170">Subnet</span></span> |<span data-ttu-id="9b850-171">t, --subnet <subnet></span><span class="sxs-lookup"><span data-stu-id="9b850-171">t, --subnet <subnet></span></span> |<span data-ttu-id="9b850-172">VNET에서 캐시를 호스팅하는 경우에 캐시를 배포할 서브넷의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-172">When hosting your cache in a VNET, specifies the name of the subnet in which to deploy the cache.</span></span> |
| <span data-ttu-id="9b850-173">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="9b850-173">VirtualNetwork</span></span> |<span data-ttu-id="9b850-174">-v, --virtual-network <virtual-network></span><span class="sxs-lookup"><span data-stu-id="9b850-174">-v, --virtual-network <virtual-network></span></span> |<span data-ttu-id="9b850-175">VNET에서 캐시를 호스트하는 경우 Redis Cache를 배포하는 가상 네트워크의 정확한 ARM 리소스 ID를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-175">When hosting your cache in a VNET, specifies the exact ARM resource ID of the virtual network to deploy the redis cache in.</span></span> <span data-ttu-id="9b850-176">형식 예: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="9b850-176">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="9b850-177">구독</span><span class="sxs-lookup"><span data-stu-id="9b850-177">Subscription</span></span> |<span data-ttu-id="9b850-178">-s, --subscription</span><span class="sxs-lookup"><span data-stu-id="9b850-178">-s, --subscription</span></span> |<span data-ttu-id="9b850-179">구독 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-179">The subscription identifier.</span></span> |

## <a name="see-all-redis-cache-commands"></a><span data-ttu-id="9b850-180">모든 Redis Cache 명령 참조</span><span class="sxs-lookup"><span data-stu-id="9b850-180">See all Redis Cache commands</span></span>
<span data-ttu-id="9b850-181">모든 Redis Cache 명령 및 매개 변수를 보려면 `azure rediscache -h` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-181">To see all Redis Cache commands and their parameters, use the `azure rediscache -h` command.</span></span>

    C:\>azure rediscache -h
    help:    Commands to manage your Azure Redis Cache(s)
    help:
    help:    Create a Redis Cache
    help:      rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Delete an existing Redis Cache
    help:      rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    List all Redis Caches within your Subscription or Resource Group
    help:      rediscache list [options]
    help:
    help:    Show properties of an existing Redis Cache
    help:      rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Change settings of an existing Redis Cache
    help:      rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Renew the authentication key for an existing Redis Cache
    help:      rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:      rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help  output usage information
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="create-a-redis-cache"></a><span data-ttu-id="9b850-182">Redis Cache 만들기</span><span class="sxs-lookup"><span data-stu-id="9b850-182">Create a Redis Cache</span></span>
<span data-ttu-id="9b850-183">Redis Cache를 만들려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-183">To create a Redis Cache, use the following command:</span></span>

    azure rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]

<span data-ttu-id="9b850-184">이 명령에 대한 자세한 내용은 `azure rediscache create -h` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-184">For more information about this command, run the `azure rediscache create -h` command.</span></span>

    C:\>azure rediscache create -h
    help:    Create a Redis Cache
    help:
    help:    Usage: rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of the Resource Group
    help:      -l, --location <location>                                Location to create cache.
    help:      -z, --size <size>                                        Size of the Redis Cache. Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]
    help:      -x, --sku <sku>                                          Redis SKU. Should be one of : [Basic, Standard, Premium]
    help:      -e, --enable-non-ssl-port                                EnableNonSslPort property of the Redis Cache. Add this flag if you want to enable the Non SSL Port for your cache
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here. Format:"{"<key1>":"<value1>","<key2>":"<value2>"}"
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter the path of a file containing configuration keys and values here. Format for the file entry: {"<key1>":"<value1>","<key2>":"<value2>"}
    help:      -r, --shard-count <shard-count>                          Number of Shards to create on a Premium Cluster Cache
    help:      -v, --virtual-network <virtual-network>                  The exact ARM resource ID of the virtual network to deploy the redis cache in. Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1
    help:      -t, --subnet <subnet>                                    Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -p, --static-ip <static-ip>                              Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -s, --subscription <id>                                  the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="delete-an-existing-redis-cache"></a><span data-ttu-id="9b850-185">기존 Redis Cache 삭제</span><span class="sxs-lookup"><span data-stu-id="9b850-185">Delete an existing Redis Cache</span></span>
<span data-ttu-id="9b850-186">Redis Cache를 삭제하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-186">To delete a Redis Cache, use the following command:</span></span>

    azure rediscache delete [--name <name> --resource-group <resource-group> ]

<span data-ttu-id="9b850-187">이 명령에 대한 자세한 내용은 `azure rediscache delete -h` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-187">For more information about this command, run the `azure rediscache delete -h` command.</span></span>

    C:\>azure rediscache delete -h
    help:    Delete an existing Redis Cache
    help:
    help:    Usage: rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group under which the cache exists
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-all-redis-caches-within-your-subscription-or-resource-group"></a><span data-ttu-id="9b850-188">구독 또는 리소스 그룹 내 모든 Redis Cache 나열</span><span class="sxs-lookup"><span data-stu-id="9b850-188">List all Redis Caches within your Subscription or Resource Group</span></span>
<span data-ttu-id="9b850-189">구독 또는 리소스 그룹 내 모든 Redis Cache를 나열하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-189">To list all Redis Caches within your Subscription or Resource Group, use the following command:</span></span>

    azure rediscache list [options]

<span data-ttu-id="9b850-190">이 명령에 대한 자세한 내용은 `azure rediscache list -h` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-190">For more information about this command, run the `azure rediscache list -h` command.</span></span>

    C:\>azure rediscache list -h
    help:    List all Redis Caches within your Subscription or Resource Group
    help:
    help:    Usage: rediscache list [options]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -g, --resource-group <resource-group>  Name of the Resource Group
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="show-properties-of-an-existing-redis-cache"></a><span data-ttu-id="9b850-191">기존 Redis Cache의 속성 표시</span><span class="sxs-lookup"><span data-stu-id="9b850-191">Show properties of an existing Redis Cache</span></span>
<span data-ttu-id="9b850-192">기존 Redis Cache의 속성을 표시하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-192">To show properties of an existing Redis Cache, use the following command:</span></span>

    azure rediscache show [--name <name> --resource-group <resource-group>]

<span data-ttu-id="9b850-193">이 명령에 대한 자세한 내용은 `azure rediscache show -h` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-193">For more information about this command, run the `azure rediscache show -h` command.</span></span>

    C:\>azure rediscache show -h
    help:    Show properties of an existing Redis Cache
    help:
    help:    Usage: rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

<a name="scale"></a>

## <a name="change-settings-of-an-existing-redis-cache"></a><span data-ttu-id="9b850-194">기존 Redis Cache의 설정 변경</span><span class="sxs-lookup"><span data-stu-id="9b850-194">Change settings of an existing Redis Cache</span></span>
<span data-ttu-id="9b850-195">기존 Redis Cache의 설정을 변경하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-195">To change settings of an existing Redis Cache, use the following command:</span></span>

    azure rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]

<span data-ttu-id="9b850-196">이 명령에 대한 자세한 내용은 `azure rediscache set -h` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-196">For more information about this command, run the `azure rediscache set -h` command.</span></span>

    C:\>azure rediscache set -h
    help:    Change settings of an existing Redis Cache
    help:
    help:    Usage: rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of the Resource Group
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here.
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter the path of a file containing configuration keys and values here.
    help:      -s, --subscription <subscription>                        the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="renew-the-authentication-key-for-an-existing-redis-cache"></a><span data-ttu-id="9b850-197">기존 Redis Cache에 대한 인증 키 갱신</span><span class="sxs-lookup"><span data-stu-id="9b850-197">Renew the authentication key for an existing Redis Cache</span></span>
<span data-ttu-id="9b850-198">기존 Redis Cache에 대한 인증 키를 갱신하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-198">To renew the authentication key for an existing Redis Cache, use the following command:</span></span>

    azure rediscache renew-key [--name <name> --resource-group <resource-group> --key-type <key-type>]

<span data-ttu-id="9b850-199">`key-type`에 대해 `Primary` 또는 `Secondary`를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-199">Specify `Primary` or `Secondary` for `key-type`.</span></span>

<span data-ttu-id="9b850-200">이 명령에 대한 자세한 내용은 `azure rediscache renew-key -h` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-200">For more information about this command, run the `azure rediscache renew-key -h` command.</span></span>

    C:\>azure rediscache renew-key -h
    help:    Renew the authentication key for an existing Redis Cache
    help:
    help:    Usage: rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group under which cache exists
    help:      -t, --key-type <key-type>              type of key to renew. Valid values are: 'Primary', 'Secondary'.
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-primary-and-secondary-keys-of-an-existing-redis-cache"></a><span data-ttu-id="9b850-201">기존 Redis Cache의 주 및 보조 키 나열</span><span class="sxs-lookup"><span data-stu-id="9b850-201">List Primary and Secondary keys of an existing Redis Cache</span></span>
<span data-ttu-id="9b850-202">기존 Redis Cache의 주 및 보조 키를 나열하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-202">To list Primary and Secondary keys of an existing Redis Cache, use the following command:</span></span>

    azure rediscache list-keys [--name <name> --resource-group <resource-group>]

<span data-ttu-id="9b850-203">이 명령에 대한 자세한 내용은 `azure rediscache list-keys -h` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9b850-203">For more information about this command, run the `azure rediscache list-keys -h` command.</span></span>

    C:\>azure rediscache list-keys -h
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:
    help:    Usage: rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group under which Cache exists
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)
