---
title: "Azure CLI Redis Cache 샘플 | Microsoft Docs"
description: "Azure Redis Cache에 대한 Azure CLI 샘플입니다."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 8d2de145-50c0-4f76-bf8f-fdf679f03698
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: a3debf3380b57faa5b7b30f612698fe6de5b7067
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cli-samples-for-azure-redis-cache"></a><span data-ttu-id="e82b2-103">Azure Redis Cache에 대한 Azure CLI 샘플</span><span class="sxs-lookup"><span data-stu-id="e82b2-103">Azure CLI Samples for Azure Redis Cache</span></span>

<span data-ttu-id="e82b2-104">다음 테이블은 Azure CLI를 사용하여 빌드된 bash 셸에 대한 링크를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e82b2-104">The following table includes links to bash scripts built using the Azure CLI.</span></span>

| | |
|---|---|
|<span data-ttu-id="e82b2-105">**캐시 만들기**</span><span class="sxs-lookup"><span data-stu-id="e82b2-105">**Create cache**</span></span>||
| [<span data-ttu-id="e82b2-106">캐시 만들기</span><span class="sxs-lookup"><span data-stu-id="e82b2-106">Create a cache</span></span>](./scripts/create-cache.md) | <span data-ttu-id="e82b2-107">리소스 그룹 및 기본 계층 Azure Redis Cache를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e82b2-107">Creates a resource group and a basic tier Azure Redis Cache.</span></span> |
| [<span data-ttu-id="e82b2-108">클러스터링을 사용하여 프리미엄 캐시 만들기</span><span class="sxs-lookup"><span data-stu-id="e82b2-108">Create a premium cache with clustering</span></span>](./scripts/create-premium-cache-cluster.md) | <span data-ttu-id="e82b2-109">클러스터링을 사용하여 리소스 그룹 및 프리미엄 계층 캐시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e82b2-109">Creates a resource group and a premium tier cache with clustering enabled.</span></span>|
| [<span data-ttu-id="e82b2-110">캐시 세부 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="e82b2-110">Get cache details</span></span>](./scripts/show-cache.md) | <span data-ttu-id="e82b2-111">프로비전 상태를 포함한 Azure Redis Cache 인스턴스의 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e82b2-111">Gets details of an Azure Redis Cache instance, including provisioning status.</span></span> |
| [<span data-ttu-id="e82b2-112">호스트 이름, 포트 및 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="e82b2-112">Get the hostname, ports, and keys</span></span>](./scripts/cache-keys-ports.md) | <span data-ttu-id="e82b2-113">Azure Redis Cache 인스턴스의 호스트 이름, 포트 및 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e82b2-113">Gets the hostname, ports, and keys for an Azure Redis Cache instance.</span></span> |
|<span data-ttu-id="e82b2-114">**웹앱과 캐시**</span><span class="sxs-lookup"><span data-stu-id="e82b2-114">**Web app plus cache**</span></span>||
| [<span data-ttu-id="e82b2-115">Redis Cache에 웹앱 연결</span><span class="sxs-lookup"><span data-stu-id="e82b2-115">Connect a web app to a redis cache</span></span>](./../app-service-web/scripts/app-service-cli-app-service-redis.md) | <span data-ttu-id="e82b2-116">Azure 웹앱 및 Redis Cache를 만들고 앱 설정에 Redis 연결 세부 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e82b2-116">Creates an Azure web app and a redis cache, then adds the redis connection details to the app settings.</span></span> |
|<span data-ttu-id="e82b2-117">**캐시 삭제**</span><span class="sxs-lookup"><span data-stu-id="e82b2-117">**Delete cache**</span></span>||
| [<span data-ttu-id="e82b2-118">캐시 삭제</span><span class="sxs-lookup"><span data-stu-id="e82b2-118">Delete a cache</span></span>](./scripts/delete-cache.md) | <span data-ttu-id="e82b2-119">Azure Redis Cache 인스턴스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="e82b2-119">Deletes an Azure Redis Cache instance</span></span>  |
| | |

<span data-ttu-id="e82b2-120">Azure CLI 2.0에 대한 자세한 내용은 [Azure CLI 2.0 설치](https://docs.microsoft.com/cli/azure/install-azure-cli) 및 [Azure CLI 2.0 시작](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e82b2-120">For more information about Azure CLI 2.0, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) and [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>