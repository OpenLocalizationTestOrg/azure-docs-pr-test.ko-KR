---
title: "Azure CLI를 사용 하 여 Azure Redis 캐시 aaaManage | Microsoft Docs"
description: "어떻게 tooinstall hello Azure CLI 모든 플랫폼에서 방법에 대해 알아봅니다 toouse 것 tooconnect tooyour Azure 계정 및 방법을 toocreate hello Azure CLI에서에서 Redis 캐시를 관리 하 고 있습니다."
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
ms.openlocfilehash: e8ee30090133e6b4edea93dcd13fd171e75989bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-azure-redis-cache-using-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="884e0-103">어떻게 toocreate hello Azure 명령줄 인터페이스 (Azure CLI)를 사용 하 여 Azure Redis 캐시를 관리 하 고</span><span class="sxs-lookup"><span data-stu-id="884e0-103">How toocreate and manage Azure Redis Cache using hello Azure Command-Line Interface (Azure CLI)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="884e0-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="884e0-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="884e0-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="884e0-105">Azure CLI</span></span>](cache-manage-cli.md)
>
>

<span data-ttu-id="884e0-106">hello Azure CLI는 좋은 방법 toomanage 모든 플랫폼에서 Azure 인프라입니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-106">hello Azure CLI is a great way toomanage your Azure infrastructure from any platform.</span></span> <span data-ttu-id="884e0-107">이 문서에서는 어떻게 toocreate hello Azure CLI를 사용 하 여 Azure Redis 캐시 인스턴스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-107">This article shows you how toocreate and manage your Azure Redis Cache instances using hello Azure CLI.</span></span>

> [!NOTE]
> <span data-ttu-id="884e0-108">이 문서 tooa 이전 버전을 Azure CLI 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-108">This article applies tooa previous version of Azure CLI.</span></span> <span data-ttu-id="884e0-109">Hello 최신 Azure CLI 2.0 예제 스크립트에 대 한 참조 [Azure CLI Redis 캐시 샘플](cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-109">For hello latest Azure CLI 2.0 sample scripts, see [Azure CLI Redis cache samples](cli-samples.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="884e0-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="884e0-110">Prerequisites</span></span>
<span data-ttu-id="884e0-111">toocreate 및 Azure CLI를 사용 하 여 Azure Redis 캐시 인스턴스를 관리 hello 다음 단계를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-111">toocreate and manage Azure Redis Cache instances using Azure CLI, you must complete hello following steps.</span></span>

* <span data-ttu-id="884e0-112">Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-112">You must have an Azure account.</span></span> <span data-ttu-id="884e0-113">계정이 없는 경우 몇 분 만에 [무료 계정](https://azure.microsoft.com/pricing/free-trial/) 을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-113">If you don't have one, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a few moments.</span></span>
* <span data-ttu-id="884e0-114">[Hello Azure CLI 설치](../cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-114">[Install hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="884e0-115">회사 또는 개인 Azure 계정으로 Azure CLI를 설치 하 여 연결 하거나 학교 Azure 계정 및 로그인 hello에서 hello를 사용 하 여 Azure CLI `azure login` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-115">Connect your Azure CLI installation with a personal Azure account, or with a work or school Azure account, and log in from hello Azure CLI using hello `azure login` command.</span></span> <span data-ttu-id="884e0-116">toounderstand 차이 hello 및 선택, 참조 [hello Azure CLI (명령줄 인터페이스 Azure)에서 tooan Azure 구독 연결](../xplat-cli-connect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-116">toounderstand hello differences and choose, see [Connect tooan Azure subscription from hello Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="884e0-117">Hello 다음 명령 중 하나를 실행 하기 전에 hello를 실행 하 여 hello Azure CLI 리소스 관리자 모드로 전환 `azure config mode arm` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-117">Before running any of hello following commands, switch hello Azure CLI into Resource Manager mode by running hello `azure config mode arm` command.</span></span> <span data-ttu-id="884e0-118">자세한 내용은 참조 [hello Azure CLI toomanage Azure를 사용 하 여 리소스 및 리소스 그룹](../xplat-cli-azure-resource-manager.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-118">For more information, see [Use hello Azure CLI toomanage Azure resources and resource groups](../xplat-cli-azure-resource-manager.md).</span></span>

## <a name="redis-cache-properties"></a><span data-ttu-id="884e0-119">Redis Cache 속성</span><span class="sxs-lookup"><span data-stu-id="884e0-119">Redis Cache properties</span></span>
<span data-ttu-id="884e0-120">hello 다음 속성이 사용 됩니다 생성 및 Redis 캐시 인스턴스를 업데이트 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="884e0-120">hello following properties are used when creating and updating Redis Cache instances.</span></span>

| <span data-ttu-id="884e0-121">속성</span><span class="sxs-lookup"><span data-stu-id="884e0-121">Property</span></span> | <span data-ttu-id="884e0-122">Switch</span><span class="sxs-lookup"><span data-stu-id="884e0-122">Switch</span></span> | <span data-ttu-id="884e0-123">설명</span><span class="sxs-lookup"><span data-stu-id="884e0-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="884e0-124">name</span><span class="sxs-lookup"><span data-stu-id="884e0-124">name</span></span> |<span data-ttu-id="884e0-125">-n, --name</span><span class="sxs-lookup"><span data-stu-id="884e0-125">-n, --name</span></span> |<span data-ttu-id="884e0-126">Hello Redis 캐시의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-126">Name of hello Redis Cache.</span></span> |
| <span data-ttu-id="884e0-127">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="884e0-127">resource group</span></span> |<span data-ttu-id="884e0-128">-g, --resource-group</span><span class="sxs-lookup"><span data-stu-id="884e0-128">-g, --resource-group</span></span> |<span data-ttu-id="884e0-129">Hello 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-129">Name of hello Resource Group.</span></span> |
| <span data-ttu-id="884e0-130">location</span><span class="sxs-lookup"><span data-stu-id="884e0-130">location</span></span> |<span data-ttu-id="884e0-131">-l, --location</span><span class="sxs-lookup"><span data-stu-id="884e0-131">-l, --location</span></span> |<span data-ttu-id="884e0-132">위치 toocreate 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-132">Location toocreate cache.</span></span> |
| <span data-ttu-id="884e0-133">size</span><span class="sxs-lookup"><span data-stu-id="884e0-133">size</span></span> |<span data-ttu-id="884e0-134">-z, --size</span><span class="sxs-lookup"><span data-stu-id="884e0-134">-z, --size</span></span> |<span data-ttu-id="884e0-135">Hello Redis 캐시의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-135">Size of hello Redis Cache.</span></span> <span data-ttu-id="884e0-136">유효한 값: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span><span class="sxs-lookup"><span data-stu-id="884e0-136">Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span></span> |
| <span data-ttu-id="884e0-137">sku</span><span class="sxs-lookup"><span data-stu-id="884e0-137">sku</span></span> |<span data-ttu-id="884e0-138">-x, --sku</span><span class="sxs-lookup"><span data-stu-id="884e0-138">-x, --sku</span></span> |<span data-ttu-id="884e0-139">Redis SKU입니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-139">Redis SKU.</span></span> <span data-ttu-id="884e0-140">다음 중 하나여야 합니다. [기본, 표준, 프리미엄]</span><span class="sxs-lookup"><span data-stu-id="884e0-140">Should be one of : [Basic, Standard, Premium]</span></span> |
| <span data-ttu-id="884e0-141">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="884e0-141">EnableNonSslPort</span></span> |<span data-ttu-id="884e0-142">-e, --enable-non-ssl-port</span><span class="sxs-lookup"><span data-stu-id="884e0-142">-e, --enable-non-ssl-port</span></span> |<span data-ttu-id="884e0-143">Hello Redis Cache의 EnableNonSslPort 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-143">EnableNonSslPort property of hello Redis Cache.</span></span> <span data-ttu-id="884e0-144">캐시에 대 한 tooenable hello 비 SSL 포트를 사용 하려는 경우이 플래그를 추가</span><span class="sxs-lookup"><span data-stu-id="884e0-144">Add this flag if you want tooenable hello Non SSL Port for your cache</span></span> |
| <span data-ttu-id="884e0-145">Redis 구성</span><span class="sxs-lookup"><span data-stu-id="884e0-145">Redis Configuration</span></span> |<span data-ttu-id="884e0-146">-c, --redis-configuration</span><span class="sxs-lookup"><span data-stu-id="884e0-146">-c, --redis-configuration</span></span> |<span data-ttu-id="884e0-147">Redis 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-147">Redis Configuration.</span></span> <span data-ttu-id="884e0-148">구성 키 및 값의 JSON 형식 문자열을 여기에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-148">Enter a JSON formatted string of configuration keys and values here.</span></span> <span data-ttu-id="884e0-149">형식:"{"":"","":""}"</span><span class="sxs-lookup"><span data-stu-id="884e0-149">Format:"{"":"","":""}"</span></span> |
| <span data-ttu-id="884e0-150">Redis 구성</span><span class="sxs-lookup"><span data-stu-id="884e0-150">Redis Configuration</span></span> |<span data-ttu-id="884e0-151">-f, --redis-configuration-file</span><span class="sxs-lookup"><span data-stu-id="884e0-151">-f, --redis-configuration-file</span></span> |<span data-ttu-id="884e0-152">Redis 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-152">Redis Configuration.</span></span> <span data-ttu-id="884e0-153">구성 키 및 여기에 값을 포함 하는 파일의 hello 경로 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-153">Enter hello path of a file containing configuration keys and values here.</span></span> <span data-ttu-id="884e0-154">Hello 파일 항목에 대 한 형식: {"": "","": ""}</span><span class="sxs-lookup"><span data-stu-id="884e0-154">Format for hello file entry: {"":"","":""}</span></span> |
| <span data-ttu-id="884e0-155">분할된 데이터베이스 수</span><span class="sxs-lookup"><span data-stu-id="884e0-155">Shard Count</span></span> |<span data-ttu-id="884e0-156">-r, --shard-count</span><span class="sxs-lookup"><span data-stu-id="884e0-156">-r, --shard-count</span></span> |<span data-ttu-id="884e0-157">분할 된 데이터베이스 toocreate 클러스터링과 함께 Premium 클러스터 캐시에서의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-157">Number of Shards toocreate on a Premium Cluster Cache with clustering.</span></span> |
| <span data-ttu-id="884e0-158">가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="884e0-158">Virtual Network</span></span> |<span data-ttu-id="884e0-159">-v, --virtual-network</span><span class="sxs-lookup"><span data-stu-id="884e0-159">-v, --virtual-network</span></span> |<span data-ttu-id="884e0-160">지정 된 VNET에서 캐시를 호스팅하는 경우 hello 정확한 ARM 리소스 ID의 가상 네트워크 toodeploy hello hello redis 캐시에는 합니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-160">When hosting your cache in a VNET, specifies hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in.</span></span> <span data-ttu-id="884e0-161">형식 예: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="884e0-161">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="884e0-162">키 유형</span><span class="sxs-lookup"><span data-stu-id="884e0-162">key type</span></span> |<span data-ttu-id="884e0-163">-t, --key-type</span><span class="sxs-lookup"><span data-stu-id="884e0-163">-t, --key-type</span></span> |<span data-ttu-id="884e0-164">키 toorenew의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-164">Type of key toorenew.</span></span> <span data-ttu-id="884e0-165">유효한 값: [주, 보조]</span><span class="sxs-lookup"><span data-stu-id="884e0-165">Valid values: [Primary, Secondary]</span></span> |
| <span data-ttu-id="884e0-166">StaticIP</span><span class="sxs-lookup"><span data-stu-id="884e0-166">StaticIP</span></span> |<span data-ttu-id="884e0-167">-p, --static-ip <static-ip></span><span class="sxs-lookup"><span data-stu-id="884e0-167">-p, --static-ip <static-ip></span></span> |<span data-ttu-id="884e0-168">VNET에서 캐시를 호스팅하는 경우 hello 캐시에 대 한 hello 서브넷에 고유한 IP 주소를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-168">When hosting your cache in a VNET, specifies a unique IP address in hello subnet for hello cache.</span></span> <span data-ttu-id="884e0-169">을 지정 하지 않으면 하나는 선택 됩니다 hello 서브넷에서.</span><span class="sxs-lookup"><span data-stu-id="884e0-169">If not provided, one is chosen for you from hello subnet.</span></span> |
| <span data-ttu-id="884e0-170">서브넷</span><span class="sxs-lookup"><span data-stu-id="884e0-170">Subnet</span></span> |<span data-ttu-id="884e0-171">t, --subnet <subnet></span><span class="sxs-lookup"><span data-stu-id="884e0-171">t, --subnet <subnet></span></span> |<span data-ttu-id="884e0-172">VNET에서 캐시를 호스팅하는 경우 어떤 toodeploy hello 캐시 hello hello 서브넷 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-172">When hosting your cache in a VNET, specifies hello name of hello subnet in which toodeploy hello cache.</span></span> |
| <span data-ttu-id="884e0-173">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="884e0-173">VirtualNetwork</span></span> |<span data-ttu-id="884e0-174">-v, --virtual-network <virtual-network></span><span class="sxs-lookup"><span data-stu-id="884e0-174">-v, --virtual-network <virtual-network></span></span> |<span data-ttu-id="884e0-175">지정 된 VNET에서 캐시를 호스팅하는 경우 hello 정확한 ARM 리소스 ID의 가상 네트워크 toodeploy hello hello redis 캐시에는 합니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-175">When hosting your cache in a VNET, specifies hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in.</span></span> <span data-ttu-id="884e0-176">형식 예: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="884e0-176">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="884e0-177">구독</span><span class="sxs-lookup"><span data-stu-id="884e0-177">Subscription</span></span> |<span data-ttu-id="884e0-178">-s, --subscription</span><span class="sxs-lookup"><span data-stu-id="884e0-178">-s, --subscription</span></span> |<span data-ttu-id="884e0-179">hello 구독 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-179">hello subscription identifier.</span></span> |

## <a name="see-all-redis-cache-commands"></a><span data-ttu-id="884e0-180">모든 Redis Cache 명령 참조</span><span class="sxs-lookup"><span data-stu-id="884e0-180">See all Redis Cache commands</span></span>
<span data-ttu-id="884e0-181">toosee 모든 Redis Cache 명령 및 매개 변수를 사용 하 여 hello `azure rediscache -h` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-181">toosee all Redis Cache commands and their parameters, use hello `azure rediscache -h` command.</span></span>

    C:\>azure rediscache -h
    help:    Commands toomanage your Azure Redis Cache(s)
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
    help:    Renew hello authentication key for an existing Redis Cache
    help:      rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:      rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help  output usage information
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="create-a-redis-cache"></a><span data-ttu-id="884e0-182">Redis Cache 만들기</span><span class="sxs-lookup"><span data-stu-id="884e0-182">Create a Redis Cache</span></span>
<span data-ttu-id="884e0-183">Redis Cache toocreate hello 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-183">toocreate a Redis Cache, use hello following command:</span></span>

    azure rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]

<span data-ttu-id="884e0-184">이 명령에 대 한 자세한 내용은 실행 hello `azure rediscache create -h` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-184">For more information about this command, run hello `azure rediscache create -h` command.</span></span>

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
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -l, --location <location>                                Location toocreate cache.
    help:      -z, --size <size>                                        Size of hello Redis Cache. Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]
    help:      -x, --sku <sku>                                          Redis SKU. Should be one of : [Basic, Standard, Premium]
    help:      -e, --enable-non-ssl-port                                EnableNonSslPort property of hello Redis Cache. Add this flag if you want tooenable hello Non SSL Port for your cache
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here. Format:"{"<key1>":"<value1>","<key2>":"<value2>"}"
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here. Format for hello file entry: {"<key1>":"<value1>","<key2>":"<value2>"}
    help:      -r, --shard-count <shard-count>                          Number of Shards toocreate on a Premium Cluster Cache
    help:      -v, --virtual-network <virtual-network>                  hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1
    help:      -t, --subnet <subnet>                                    Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -p, --static-ip <static-ip>                              Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -s, --subscription <id>                                  hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="delete-an-existing-redis-cache"></a><span data-ttu-id="884e0-185">기존 Redis Cache 삭제</span><span class="sxs-lookup"><span data-stu-id="884e0-185">Delete an existing Redis Cache</span></span>
<span data-ttu-id="884e0-186">Redis Cache toodelete hello 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-186">toodelete a Redis Cache, use hello following command:</span></span>

    azure rediscache delete [--name <name> --resource-group <resource-group> ]

<span data-ttu-id="884e0-187">이 명령에 대 한 자세한 내용은 실행 hello `azure rediscache delete -h` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-187">For more information about this command, run hello `azure rediscache delete -h` command.</span></span>

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
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which hello cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-all-redis-caches-within-your-subscription-or-resource-group"></a><span data-ttu-id="884e0-188">구독 또는 리소스 그룹 내 모든 Redis Cache 나열</span><span class="sxs-lookup"><span data-stu-id="884e0-188">List all Redis Caches within your Subscription or Resource Group</span></span>
<span data-ttu-id="884e0-189">toolist 구독 또는 리소스 그룹 내에서 모든 Redis 캐시 사용 하 여 다음 명령을 hello:</span><span class="sxs-lookup"><span data-stu-id="884e0-189">toolist all Redis Caches within your Subscription or Resource Group, use hello following command:</span></span>

    azure rediscache list [options]

<span data-ttu-id="884e0-190">이 명령에 대 한 자세한 내용은 실행 hello `azure rediscache list -h` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-190">For more information about this command, run hello `azure rediscache list -h` command.</span></span>

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
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="show-properties-of-an-existing-redis-cache"></a><span data-ttu-id="884e0-191">기존 Redis Cache의 속성 표시</span><span class="sxs-lookup"><span data-stu-id="884e0-191">Show properties of an existing Redis Cache</span></span>
<span data-ttu-id="884e0-192">다음 명령을 hello를 사용 하는 기존 Redis 캐시의 tooshow 속성:</span><span class="sxs-lookup"><span data-stu-id="884e0-192">tooshow properties of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache show [--name <name> --resource-group <resource-group>]

<span data-ttu-id="884e0-193">이 명령에 대 한 자세한 내용은 실행 hello `azure rediscache show -h` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-193">For more information about this command, run hello `azure rediscache show -h` command.</span></span>

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
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

<a name="scale"></a>

## <a name="change-settings-of-an-existing-redis-cache"></a><span data-ttu-id="884e0-194">기존 Redis Cache의 설정 변경</span><span class="sxs-lookup"><span data-stu-id="884e0-194">Change settings of an existing Redis Cache</span></span>
<span data-ttu-id="884e0-195">기존 Redis Cache의 설정 toochange hello 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-195">toochange settings of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]

<span data-ttu-id="884e0-196">이 명령에 대 한 자세한 내용은 실행 hello `azure rediscache set -h` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-196">For more information about this command, run hello `azure rediscache set -h` command.</span></span>

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
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here.
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here.
    help:      -s, --subscription <subscription>                        hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="renew-hello-authentication-key-for-an-existing-redis-cache"></a><span data-ttu-id="884e0-197">기존 Redis 캐시에 대 한 hello 인증 키를 갱신 합니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-197">Renew hello authentication key for an existing Redis Cache</span></span>
<span data-ttu-id="884e0-198">기존 Redis 캐시에서 다음 명령을 사용 하 여 hello toorenew hello 인증 키:</span><span class="sxs-lookup"><span data-stu-id="884e0-198">toorenew hello authentication key for an existing Redis Cache, use hello following command:</span></span>

    azure rediscache renew-key [--name <name> --resource-group <resource-group> --key-type <key-type>]

<span data-ttu-id="884e0-199">`key-type`에 대해 `Primary` 또는 `Secondary`를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-199">Specify `Primary` or `Secondary` for `key-type`.</span></span>

<span data-ttu-id="884e0-200">이 명령에 대 한 자세한 내용은 실행 hello `azure rediscache renew-key -h` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-200">For more information about this command, run hello `azure rediscache renew-key -h` command.</span></span>

    C:\>azure rediscache renew-key -h
    help:    Renew hello authentication key for an existing Redis Cache
    help:
    help:    Usage: rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which cache exists
    help:      -t, --key-type <key-type>              type of key toorenew. Valid values are: 'Primary', 'Secondary'.
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-primary-and-secondary-keys-of-an-existing-redis-cache"></a><span data-ttu-id="884e0-201">기존 Redis Cache의 주 및 보조 키 나열</span><span class="sxs-lookup"><span data-stu-id="884e0-201">List Primary and Secondary keys of an existing Redis Cache</span></span>
<span data-ttu-id="884e0-202">기존 Redis 캐시의 기본 및 보조 키 toolist hello 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-202">toolist Primary and Secondary keys of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache list-keys [--name <name> --resource-group <resource-group>]

<span data-ttu-id="884e0-203">이 명령에 대 한 자세한 내용은 실행 hello `azure rediscache list-keys -h` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="884e0-203">For more information about this command, run hello `azure rediscache list-keys -h` command.</span></span>

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
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which Cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)
