---
title: "Azure Key Vault에 영향을 주는 Azure 서비스 중단 발생 시 수행할 작업 | Microsoft Docs"
description: "Azure Key Vault에 영향을 주는 Azure 서비스 중단 발생 시 수행할 작업에 대해 알아봅니다."
services: key-vault
documentationcenter: 
author: adamglick
manager: mbaldwin
editor: 
ms.assetid: 19a9af63-3032-447b-9d1a-b0125f384edb
ms.service: key-vault
ms.workload: key-vault
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: sumedhb;aglick
ms.openlocfilehash: 6419d54c54e7d19103419262b79e7a5268b2268c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-availability-and-redundancy"></a><span data-ttu-id="fa667-103">Azure 주요 자격 증명 모음 가용성 및 중복성</span><span class="sxs-lookup"><span data-stu-id="fa667-103">Azure Key Vault availability and redundancy</span></span>
<span data-ttu-id="fa667-104">Azure 주요 자격 증명 모음에는 서비스의 개별 구성 요소가 실패해도 응용 프로그램에서 키 및 암호를 사용할 수 있도록 해주는 여러 계층의 중복성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa667-104">Azure Key Vault features multiple layers of redundancy to make sure that your keys and secrets remain available to your application even if individual components of the service fail.</span></span>

<span data-ttu-id="fa667-105">주요 자격 증명 모음의 내용은 지역 내에는 물론 동일한 지리 내에 150마일 이상 떨어진 보조 지역에도 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa667-105">The contents of your key vault are replicated within the region and to a secondary region at least 150 miles away but within the same geography.</span></span> <span data-ttu-id="fa667-106">따라서 키와 암호의 내구성이 매우 높습니다.</span><span class="sxs-lookup"><span data-stu-id="fa667-106">This maintains high durability of your keys and secrets.</span></span> <span data-ttu-id="fa667-107">특정 지역 쌍에 대한 자세한 내용은 [Azure 쌍을 이루는 지역](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fa667-107">See the [Azure paired regions](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) document for details on specific region pairs.</span></span>

<span data-ttu-id="fa667-108">주요 자격 증명 모음 서비스 내에서 개별 구성 요소가 실패하면 기능이 저하되지 않도록 하기 위해 해당 지역 내의 대체 구성 요소가 요청을 처리하도록 개입됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa667-108">If individual components within the key vault service fail, alternate components within the region step in to serve your request to make sure that there is no degradation of functionality.</span></span> <span data-ttu-id="fa667-109">이 트리거에 어떤 조치도 취할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fa667-109">You do not need to take any action to trigger this.</span></span> <span data-ttu-id="fa667-110">자동으로 발생하고 투명하게 보일 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fa667-110">It happens automatically and will be transparent to you.</span></span>

<span data-ttu-id="fa667-111">전체 Azure 지역을 사용할 수 없는 드문 경우, 해당 지역에 Azure Key Vault를 활용하는 요청이 보조 지역으로 자동 라우팅(*장애 조치*)됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa667-111">In the rare event that an entire Azure region is unavailable, the requests that you make of Azure Key Vault in that region are automatically routed (*failed over*) to a secondary region.</span></span> <span data-ttu-id="fa667-112">기본 지역을 다시 사용할 수 있는 경우 요청은 주 지역으로 다시 라우팅(*장애 복구(failback)*)됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa667-112">When the primary region is available again, requests are routed back (*failed back*) to the primary region.</span></span> <span data-ttu-id="fa667-113">다시 한 번 말씀드리지만, 이 작업은 자동으로 이루어지므로 어떤 조치도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fa667-113">Again, you do not need to take any action because this happens automatically.</span></span>

<span data-ttu-id="fa667-114">알고 있어야 하는 몇 가지 주의 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa667-114">There are a few caveats to be aware of:</span></span>

* <span data-ttu-id="fa667-115">지역 장애 조치 시 서비스를 장애 조치하는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa667-115">In the event of a region failover, it may take a few minutes for the service to fail over.</span></span> <span data-ttu-id="fa667-116">이 시간 중에 이루어진 요청은 장애 조치가 완료될 때까지 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa667-116">Requests that are made during this time may fail until the failover completes.</span></span>
* <span data-ttu-id="fa667-117">장애 조치가 완료되면 주요 자격 증명 모음은 읽기 전용 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="fa667-117">After a failover is complete, your key vault is in read-only mode.</span></span> <span data-ttu-id="fa667-118">이 모드에서 지원되는 요청은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fa667-118">Requests that are supported in this mode are:</span></span>
  * <span data-ttu-id="fa667-119">주요 자격 증명 모음 나열</span><span class="sxs-lookup"><span data-stu-id="fa667-119">List key vaults</span></span>
  * <span data-ttu-id="fa667-120">주요 자격 증명 모음 속성 가져오기</span><span class="sxs-lookup"><span data-stu-id="fa667-120">Get properties of key vaults</span></span>
  * <span data-ttu-id="fa667-121">암호 나열</span><span class="sxs-lookup"><span data-stu-id="fa667-121">List secrets</span></span>
  * <span data-ttu-id="fa667-122">암호 가져오기</span><span class="sxs-lookup"><span data-stu-id="fa667-122">Get secrets</span></span>
  * <span data-ttu-id="fa667-123">키 나열</span><span class="sxs-lookup"><span data-stu-id="fa667-123">List keys</span></span>
  * <span data-ttu-id="fa667-124">키(키의 속성) 가져오기</span><span class="sxs-lookup"><span data-stu-id="fa667-124">Get (properties of) keys</span></span>
  * <span data-ttu-id="fa667-125">암호화</span><span class="sxs-lookup"><span data-stu-id="fa667-125">Encrypt</span></span>
  * <span data-ttu-id="fa667-126">암호 해독</span><span class="sxs-lookup"><span data-stu-id="fa667-126">Decrypt</span></span>
  * <span data-ttu-id="fa667-127">래핑</span><span class="sxs-lookup"><span data-stu-id="fa667-127">Wrap</span></span>
  * <span data-ttu-id="fa667-128">래핑 취소</span><span class="sxs-lookup"><span data-stu-id="fa667-128">Unwrap</span></span>
  * <span data-ttu-id="fa667-129">Verify</span><span class="sxs-lookup"><span data-stu-id="fa667-129">Verify</span></span>
  * <span data-ttu-id="fa667-130">로그인</span><span class="sxs-lookup"><span data-stu-id="fa667-130">Sign</span></span>
  * <span data-ttu-id="fa667-131">백업</span><span class="sxs-lookup"><span data-stu-id="fa667-131">Backup</span></span>
* <span data-ttu-id="fa667-132">장애 조치가 장애 복구되면 모든 요청 유형( 읽기 *및* 쓰기 요청 포함)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa667-132">After a failover is failed back, all request types (including read *and* write requests) are available.</span></span>

