---
title: "Azure 키 자격 증명 모음에 영향을 주는 Azure 서비스 중단의 hello 이벤트에서 aaaWhat toodo | Microsoft Docs"
description: "어떤 toodo hello Azure 키 자격 증명 모음에 영향을 주는 Azure 서비스 중단 이벤트에 알아봅니다."
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
ms.openlocfilehash: 88eec82ada401a28323b3eea126168185ba4cdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-availability-and-redundancy"></a><span data-ttu-id="83082-103">Azure 주요 자격 증명 모음 가용성 및 중복성</span><span class="sxs-lookup"><span data-stu-id="83082-103">Azure Key Vault availability and redundancy</span></span>
<span data-ttu-id="83082-104">Azure 주요 자격 증명의 여러 계층의 중복 toomake 키와 암호 남아 있는지 사용할 수 있는 tooyour 응용 프로그램 hello의 개별 구성 요소 실패를 서비스 하는 경우에 있는지 기능 합니다.</span><span class="sxs-lookup"><span data-stu-id="83082-104">Azure Key Vault features multiple layers of redundancy toomake sure that your keys and secrets remain available tooyour application even if individual components of hello service fail.</span></span>

<span data-ttu-id="83082-105">hello 내용의 주요 자격 증명 모음 내에서 복제 됩니다 hello 지역과 보조 지역 tooa 150 마일 이상 떨어져 있지만 hello 내 동일한 지리적 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="83082-105">hello contents of your key vault are replicated within hello region and tooa secondary region at least 150 miles away but within hello same geography.</span></span> <span data-ttu-id="83082-106">따라서 키와 암호의 내구성이 매우 높습니다.</span><span class="sxs-lookup"><span data-stu-id="83082-106">This maintains high durability of your keys and secrets.</span></span> <span data-ttu-id="83082-107">Hello 참조 [Azure 지역 쌍이](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) 특정 지역 쌍에 대 한 자세한 내용은 문서.</span><span class="sxs-lookup"><span data-stu-id="83082-107">See hello [Azure paired regions](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) document for details on specific region pairs.</span></span>

<span data-ttu-id="83082-108">Hello 주요 자격 증명 모음 서비스 내에서 개별 구성 요소 실패 hello 지역 내의 다른 구성 요소 단계 tooserve 기능 저하 없이 인지 사용자 요청 toomake입니다.</span><span class="sxs-lookup"><span data-stu-id="83082-108">If individual components within hello key vault service fail, alternate components within hello region step in tooserve your request toomake sure that there is no degradation of functionality.</span></span> <span data-ttu-id="83082-109">모든 작업 tootrigger tootake를 불필요이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83082-109">You do not need tootake any action tootrigger this.</span></span> <span data-ttu-id="83082-110">자동으로 발생 하 고 투명 하 게 tooyou 됩니다.</span><span class="sxs-lookup"><span data-stu-id="83082-110">It happens automatically and will be transparent tooyou.</span></span>

<span data-ttu-id="83082-111">해당 지역에서 Azure 키 자격 증명 모음 구성 하는 hello 요청은 자동으로 hello 드문 경우에는 전체 Azure 지역을 사용할 수 없다는 라우팅됩니다 (*장애 조치*) tooa 보조 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="83082-111">In hello rare event that an entire Azure region is unavailable, hello requests that you make of Azure Key Vault in that region are automatically routed (*failed over*) tooa secondary region.</span></span> <span data-ttu-id="83082-112">요청은 다시 라우팅됩니다 hello 기본 지역을 사용할 수 있는 다시 (*다시 실패*) toohello 기본 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="83082-112">When hello primary region is available again, requests are routed back (*failed back*) toohello primary region.</span></span> <span data-ttu-id="83082-113">다시 않아도 tootake 조치가 자동으로 수행 하기 때문에 합니다.</span><span class="sxs-lookup"><span data-stu-id="83082-113">Again, you do not need tootake any action because this happens automatically.</span></span>

<span data-ttu-id="83082-114">몇 가지 주의 사항이 toobe 인식</span><span class="sxs-lookup"><span data-stu-id="83082-114">There are a few caveats toobe aware of:</span></span>

* <span data-ttu-id="83082-115">지역 장애 조치의 hello 이벤트를 hello 서비스 toofail 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83082-115">In hello event of a region failover, it may take a few minutes for hello service toofail over.</span></span> <span data-ttu-id="83082-116">이 시간 동안 만들어진 요청 hello 장애 조치가 완료 될 때까지 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83082-116">Requests that are made during this time may fail until hello failover completes.</span></span>
* <span data-ttu-id="83082-117">장애 조치가 완료되면 주요 자격 증명 모음은 읽기 전용 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="83082-117">After a failover is complete, your key vault is in read-only mode.</span></span> <span data-ttu-id="83082-118">이 모드에서 지원되는 요청은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="83082-118">Requests that are supported in this mode are:</span></span>
  * <span data-ttu-id="83082-119">주요 자격 증명 모음 나열</span><span class="sxs-lookup"><span data-stu-id="83082-119">List key vaults</span></span>
  * <span data-ttu-id="83082-120">주요 자격 증명 모음 속성 가져오기</span><span class="sxs-lookup"><span data-stu-id="83082-120">Get properties of key vaults</span></span>
  * <span data-ttu-id="83082-121">암호 나열</span><span class="sxs-lookup"><span data-stu-id="83082-121">List secrets</span></span>
  * <span data-ttu-id="83082-122">암호 가져오기</span><span class="sxs-lookup"><span data-stu-id="83082-122">Get secrets</span></span>
  * <span data-ttu-id="83082-123">키 나열</span><span class="sxs-lookup"><span data-stu-id="83082-123">List keys</span></span>
  * <span data-ttu-id="83082-124">키(키의 속성) 가져오기</span><span class="sxs-lookup"><span data-stu-id="83082-124">Get (properties of) keys</span></span>
  * <span data-ttu-id="83082-125">암호화</span><span class="sxs-lookup"><span data-stu-id="83082-125">Encrypt</span></span>
  * <span data-ttu-id="83082-126">암호 해독</span><span class="sxs-lookup"><span data-stu-id="83082-126">Decrypt</span></span>
  * <span data-ttu-id="83082-127">래핑</span><span class="sxs-lookup"><span data-stu-id="83082-127">Wrap</span></span>
  * <span data-ttu-id="83082-128">래핑 취소</span><span class="sxs-lookup"><span data-stu-id="83082-128">Unwrap</span></span>
  * <span data-ttu-id="83082-129">Verify</span><span class="sxs-lookup"><span data-stu-id="83082-129">Verify</span></span>
  * <span data-ttu-id="83082-130">로그인</span><span class="sxs-lookup"><span data-stu-id="83082-130">Sign</span></span>
  * <span data-ttu-id="83082-131">백업</span><span class="sxs-lookup"><span data-stu-id="83082-131">Backup</span></span>
* <span data-ttu-id="83082-132">장애 조치가 장애 복구되면 모든 요청 유형( 읽기 *및* 쓰기 요청 포함)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83082-132">After a failover is failed back, all request types (including read *and* write requests) are available.</span></span>

