---
title: "컨테이너 레지스트리 리포지토리 aaaAzure | Microsoft Docs"
description: "어떻게 Docker 이미지에 대 한 toouse Azure 컨테이너 레지스트리 리포지토리"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: cristyg
ms.openlocfilehash: 06172a63465838a78a607f268da116d8158789ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="f2424-103">Azure 컨테이너 레지스트리 리포지토리</span><span class="sxs-lookup"><span data-stu-id="f2424-103">Azure container registry repositories</span></span>

<span data-ttu-id="f2424-104">Azure Container Registry는 다양한 서비스 및 오케스트레이터와 호환됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2424-104">Azure Container Registries are compatible with a multitude of services and orchestrators.</span></span> <span data-ttu-id="f2424-105">toomake 것 보다 쉽게 tootrack hello 소스 서비스 및 있는 ACR 사용 되는 에이전트 우리 시작 hello Docker 헤더 필드를 사용 하 여 hello Docker.config 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2424-105">toomake it easier tootrack hello source services and agents from which ACR is used, we have started using hello Docker header field in hello Docker.config file.</span></span>



## <a name="viewing-repositories-in-hello-portal"></a><span data-ttu-id="f2424-106">Hello 포털에서에서 저장소 보기</span><span class="sxs-lookup"><span data-stu-id="f2424-106">Viewing repositories in hello Portal</span></span>

<span data-ttu-id="f2424-107">hello ACR 헤더 hello 형식을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f2424-107">hello ACR headers follow hello format:</span></span>
```
X-Meta-Source-Client: <cloud>/<service>/<optionalservicename>
```

* <span data-ttu-id="f2424-108">Cloud: Azure, Azure Stack 또는 기타 정부 또는 국가별 Azure 클라우드입니다.</span><span class="sxs-lookup"><span data-stu-id="f2424-108">Cloud: Azure, Azure Stack, or other government or country-specific Azure clouds.</span></span> <span data-ttu-id="f2424-109">Azure Stack 및 정부 클라우드가 현재 지원되지 않지만 이 매개 변수는 앞으로 지원될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2424-109">Although Azure Stack and government clouds are not currently supported, this parameter enables future support.</span></span>
* <span data-ttu-id="f2424-110">Hello 서비스의 서비스: 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f2424-110">Service: name of hello service.</span></span>
* <span data-ttu-id="f2424-111">Optionalservicename: 하위 서비스, 또는 toospecify SKU 사용 하 여 서비스에 대 한 선택적 매개 변수 (예: 웹 응용 프로그램 Azure/앱-서비스/웹-앱에 해당).</span><span class="sxs-lookup"><span data-stu-id="f2424-111">Optionalservicename: optional parameter for services with subservices, or toospecify a SKU (ex: web apps correspond with Azure/app-service/web-apps).</span></span>

<span data-ttu-id="f2424-112">파트너 서비스 및 orchestrators 것이 좋습니다 toouse 특정 헤더 값 toohelp 된 우리의 원격 분석은입니다.</span><span class="sxs-lookup"><span data-stu-id="f2424-112">Partner services and orchestrators are encouraged toouse specific header values toohelp with our telemetry.</span></span> <span data-ttu-id="f2424-113">원하는 경우 toohello 헤더를 전달 하는 hello 값도 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2424-113">Users can also modify hello value passed toohello header if they so desire.</span></span>

<span data-ttu-id="f2424-114">hello 값을 원하는 ACR 파트너 toouse toopopulate hello "X-메타-소스-클라이언트" 필드 아래 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2424-114">hello values we want ACR partners toouse toopopulate hello "X-Meta-Source-Client" field are below:</span></span>

| <span data-ttu-id="f2424-115">서비스 이름</span><span class="sxs-lookup"><span data-stu-id="f2424-115">Service Name</span></span>              | <span data-ttu-id="f2424-116">헤더</span><span class="sxs-lookup"><span data-stu-id="f2424-116">Header</span></span>                                |
| ------------------------- | ------------------------------------- |
| <span data-ttu-id="f2424-117">Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="f2424-117">Azure Container Service</span></span>   | <span data-ttu-id="f2424-118">azure/compute/azure-container-service</span><span class="sxs-lookup"><span data-stu-id="f2424-118">azure/compute/azure-container-service</span></span> |
| <span data-ttu-id="f2424-119">App Service - Web Apps</span><span class="sxs-lookup"><span data-stu-id="f2424-119">App Service - Web Apps</span></span>    | <span data-ttu-id="f2424-120">azure/app-service/web-apps</span><span class="sxs-lookup"><span data-stu-id="f2424-120">azure/app-service/web-apps</span></span>            |
| <span data-ttu-id="f2424-121">App Service - Logic Apps</span><span class="sxs-lookup"><span data-stu-id="f2424-121">App Service - Logic Apps</span></span>  | <span data-ttu-id="f2424-122">azure/app-service/logic-apps</span><span class="sxs-lookup"><span data-stu-id="f2424-122">azure/app-service/logic-apps</span></span>          |
| <span data-ttu-id="f2424-123">배치</span><span class="sxs-lookup"><span data-stu-id="f2424-123">Batch</span></span>                     | <span data-ttu-id="f2424-124">azure/compute/batch</span><span class="sxs-lookup"><span data-stu-id="f2424-124">azure/compute/batch</span></span>                   |
| <span data-ttu-id="f2424-125">클라우드 콘솔</span><span class="sxs-lookup"><span data-stu-id="f2424-125">Cloud Console</span></span>             | <span data-ttu-id="f2424-126">azure/cloud-console</span><span class="sxs-lookup"><span data-stu-id="f2424-126">azure/cloud-console</span></span>                   |
| <span data-ttu-id="f2424-127">함수</span><span class="sxs-lookup"><span data-stu-id="f2424-127">Functions</span></span>                 | <span data-ttu-id="f2424-128">azure/compute/functions</span><span class="sxs-lookup"><span data-stu-id="f2424-128">azure/compute/functions</span></span>               |
| <span data-ttu-id="f2424-129">IoT(사물 인터넷) - 허브</span><span class="sxs-lookup"><span data-stu-id="f2424-129">Internet of Things - Hub</span></span>  | <span data-ttu-id="f2424-130">azure/iot/hub</span><span class="sxs-lookup"><span data-stu-id="f2424-130">azure/iot/hub</span></span>                         |
| <span data-ttu-id="f2424-131">HDInsight</span><span class="sxs-lookup"><span data-stu-id="f2424-131">HDInsight</span></span>                 | <span data-ttu-id="f2424-132">azure/data/hdinsight</span><span class="sxs-lookup"><span data-stu-id="f2424-132">azure/data/hdinsight</span></span>                  |
| <span data-ttu-id="f2424-133">Jenkins</span><span class="sxs-lookup"><span data-stu-id="f2424-133">Jenkins</span></span>                   | <span data-ttu-id="f2424-134">azure/jenkins</span><span class="sxs-lookup"><span data-stu-id="f2424-134">azure/jenkins</span></span>                         |
| <span data-ttu-id="f2424-135">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f2424-135">Machine Learning</span></span>          | <span data-ttu-id="f2424-136">azure/data/machile-learning</span><span class="sxs-lookup"><span data-stu-id="f2424-136">azure/data/machile-learning</span></span>           |
| <span data-ttu-id="f2424-137">서비스 패브릭</span><span class="sxs-lookup"><span data-stu-id="f2424-137">Service Fabric</span></span>            | <span data-ttu-id="f2424-138">azure/compute/service-fabric</span><span class="sxs-lookup"><span data-stu-id="f2424-138">azure/compute/service-fabric</span></span>          |
| <span data-ttu-id="f2424-139">VSTS</span><span class="sxs-lookup"><span data-stu-id="f2424-139">VSTS</span></span>                      | <span data-ttu-id="f2424-140">azure/vsts</span><span class="sxs-lookup"><span data-stu-id="f2424-140">azure/vsts</span></span>                            |


## <a name="next-steps"></a><span data-ttu-id="f2424-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f2424-141">Next steps</span></span>
[<span data-ttu-id="f2424-142">Orchestrators 레지스트리 및 hello 지원 서비스에 대 한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="f2424-142">Learn more about registries and hello supported services and orchestrators</span></span>](container-registry-intro.md)
