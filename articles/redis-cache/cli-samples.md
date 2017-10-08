---
title: "aaaAzure CLI Redis 캐시 샘플 | Microsoft Docs"
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
ms.openlocfilehash: a2eb6f7267951faca599a43ff29b46beb05fea6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-azure-redis-cache"></a><span data-ttu-id="012c7-103">Azure Redis Cache에 대한 Azure CLI 샘플</span><span class="sxs-lookup"><span data-stu-id="012c7-103">Azure CLI Samples for Azure Redis Cache</span></span>

<span data-ttu-id="012c7-104">hello 다음 표는 hello Azure CLI를 사용 하 여 빌드된 링크 toobash 스크립트.</span><span class="sxs-lookup"><span data-stu-id="012c7-104">hello following table includes links toobash scripts built using hello Azure CLI.</span></span>

| | |
|---|---|
|<span data-ttu-id="012c7-105">**캐시 만들기**</span><span class="sxs-lookup"><span data-stu-id="012c7-105">**Create cache**</span></span>||
| [<span data-ttu-id="012c7-106">캐시 만들기</span><span class="sxs-lookup"><span data-stu-id="012c7-106">Create a cache</span></span>](./scripts/create-cache.md) | <span data-ttu-id="012c7-107">리소스 그룹 및 기본 계층 Azure Redis Cache를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="012c7-107">Creates a resource group and a basic tier Azure Redis Cache.</span></span> |
| [<span data-ttu-id="012c7-108">클러스터링을 사용하여 프리미엄 캐시 만들기</span><span class="sxs-lookup"><span data-stu-id="012c7-108">Create a premium cache with clustering</span></span>](./scripts/create-premium-cache-cluster.md) | <span data-ttu-id="012c7-109">클러스터링을 사용하여 리소스 그룹 및 프리미엄 계층 캐시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="012c7-109">Creates a resource group and a premium tier cache with clustering enabled.</span></span>|
| [<span data-ttu-id="012c7-110">캐시 세부 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="012c7-110">Get cache details</span></span>](./scripts/show-cache.md) | <span data-ttu-id="012c7-111">프로비전 상태를 포함한 Azure Redis Cache 인스턴스의 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="012c7-111">Gets details of an Azure Redis Cache instance, including provisioning status.</span></span> |
| [<span data-ttu-id="012c7-112">Hello 호스트 이름, 포트 및 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="012c7-112">Get hello hostname, ports, and keys</span></span>](./scripts/cache-keys-ports.md) | <span data-ttu-id="012c7-113">Hello 호스트 이름, 포트 및 Azure Redis 캐시 인스턴스에 대 한 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="012c7-113">Gets hello hostname, ports, and keys for an Azure Redis Cache instance.</span></span> |
|<span data-ttu-id="012c7-114">**웹앱과 캐시**</span><span class="sxs-lookup"><span data-stu-id="012c7-114">**Web app plus cache**</span></span>||
| [<span data-ttu-id="012c7-115">웹 앱 tooa redis 캐시를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="012c7-115">Connect a web app tooa redis cache</span></span>](./../app-service-web/scripts/app-service-cli-app-service-redis.md) | <span data-ttu-id="012c7-116">Azure 웹 앱 및 redis 캐시 만듭니다 다음 hello redis 연결 세부 정보 toohello 응용 프로그램 설정을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="012c7-116">Creates an Azure web app and a redis cache, then adds hello redis connection details toohello app settings.</span></span> |
|<span data-ttu-id="012c7-117">**캐시 삭제**</span><span class="sxs-lookup"><span data-stu-id="012c7-117">**Delete cache**</span></span>||
| [<span data-ttu-id="012c7-118">캐시 삭제</span><span class="sxs-lookup"><span data-stu-id="012c7-118">Delete a cache</span></span>](./scripts/delete-cache.md) | <span data-ttu-id="012c7-119">Azure Redis Cache 인스턴스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="012c7-119">Deletes an Azure Redis Cache instance</span></span>  |
| | |

<span data-ttu-id="012c7-120">Azure CLI 2.0에 대한 자세한 내용은 [Azure CLI 2.0 설치](https://docs.microsoft.com/cli/azure/install-azure-cli) 및 [Azure CLI 2.0 시작](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="012c7-120">For more information about Azure CLI 2.0, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) and [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>