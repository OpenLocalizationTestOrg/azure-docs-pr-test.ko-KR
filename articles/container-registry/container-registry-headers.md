---
title: "Azure 컨테이너 레지스트리 리포지토리 | Microsoft Docs"
description: "Docker 이미지에 Azure 컨테이너 레지스트리 리포지토리를 사용하는 방법"
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
ms.openlocfilehash: dd4feff057269ed7106990bb63eed7fcffa2dbec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="21f90-103">Azure 컨테이너 레지스트리 리포지토리</span><span class="sxs-lookup"><span data-stu-id="21f90-103">Azure container registry repositories</span></span>

<span data-ttu-id="21f90-104">Azure Container Registry는 다양한 서비스 및 오케스트레이터와 호환됩니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-104">Azure Container Registries are compatible with a multitude of services and orchestrators.</span></span> <span data-ttu-id="21f90-105">ACR을 사용하는 소스 서비스 및 에이전트를 쉽게 추적하기 위해 Docker.config 파일에서 Docker 헤더 필드를 사용하기 시작했습니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-105">To make it easier to track the source services and agents from which ACR is used, we have started using the Docker header field in the Docker.config file.</span></span>



## <a name="viewing-repositories-in-the-portal"></a><span data-ttu-id="21f90-106">포털에서 리포지토리 보기</span><span class="sxs-lookup"><span data-stu-id="21f90-106">Viewing repositories in the Portal</span></span>

<span data-ttu-id="21f90-107">ACR 헤더는 다음과 같은 형식을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-107">The ACR headers follow the format:</span></span>
```
X-Meta-Source-Client: <cloud>/<service>/<optionalservicename>
```

* <span data-ttu-id="21f90-108">Cloud: Azure, Azure Stack 또는 기타 정부 또는 국가별 Azure 클라우드입니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-108">Cloud: Azure, Azure Stack, or other government or country-specific Azure clouds.</span></span> <span data-ttu-id="21f90-109">Azure Stack 및 정부 클라우드가 현재 지원되지 않지만 이 매개 변수는 앞으로 지원될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-109">Although Azure Stack and government clouds are not currently supported, this parameter enables future support.</span></span>
* <span data-ttu-id="21f90-110">Service: 서비스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-110">Service: name of the service.</span></span>
* <span data-ttu-id="21f90-111">Optionalservicename: 하위 서비스를 포함하거나 SKU를 지정하는 서비스의 선택적 매개 변수입니다(예: Azure/app-service/web-apps에 해당하는 웹앱).</span><span class="sxs-lookup"><span data-stu-id="21f90-111">Optionalservicename: optional parameter for services with subservices, or to specify a SKU (ex: web apps correspond with Azure/app-service/web-apps).</span></span>

<span data-ttu-id="21f90-112">파트너 서비스 및 오케스트레이터는 원격 분석에 도움이 되도록 특정 헤더 값을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-112">Partner services and orchestrators are encouraged to use specific header values to help with our telemetry.</span></span> <span data-ttu-id="21f90-113">사용자가 원하는 경우 헤더에 전달된 값을 수정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-113">Users can also modify the value passed to the header if they so desire.</span></span>

<span data-ttu-id="21f90-114">ACR 파트너에서 "X-Meta-Source-Client" 필드를 채우는 데 사용하려는 값은 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="21f90-114">The values we want ACR partners to use to populate the "X-Meta-Source-Client" field are below:</span></span>

| <span data-ttu-id="21f90-115">서비스 이름</span><span class="sxs-lookup"><span data-stu-id="21f90-115">Service Name</span></span>              | <span data-ttu-id="21f90-116">헤더</span><span class="sxs-lookup"><span data-stu-id="21f90-116">Header</span></span>                                |
| ------------------------- | ------------------------------------- |
| <span data-ttu-id="21f90-117">Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="21f90-117">Azure Container Service</span></span>   | <span data-ttu-id="21f90-118">azure/compute/azure-container-service</span><span class="sxs-lookup"><span data-stu-id="21f90-118">azure/compute/azure-container-service</span></span> |
| <span data-ttu-id="21f90-119">App Service - Web Apps</span><span class="sxs-lookup"><span data-stu-id="21f90-119">App Service - Web Apps</span></span>    | <span data-ttu-id="21f90-120">azure/app-service/web-apps</span><span class="sxs-lookup"><span data-stu-id="21f90-120">azure/app-service/web-apps</span></span>            |
| <span data-ttu-id="21f90-121">App Service - Logic Apps</span><span class="sxs-lookup"><span data-stu-id="21f90-121">App Service - Logic Apps</span></span>  | <span data-ttu-id="21f90-122">azure/app-service/logic-apps</span><span class="sxs-lookup"><span data-stu-id="21f90-122">azure/app-service/logic-apps</span></span>          |
| <span data-ttu-id="21f90-123">배치</span><span class="sxs-lookup"><span data-stu-id="21f90-123">Batch</span></span>                     | <span data-ttu-id="21f90-124">azure/compute/batch</span><span class="sxs-lookup"><span data-stu-id="21f90-124">azure/compute/batch</span></span>                   |
| <span data-ttu-id="21f90-125">클라우드 콘솔</span><span class="sxs-lookup"><span data-stu-id="21f90-125">Cloud Console</span></span>             | <span data-ttu-id="21f90-126">azure/cloud-console</span><span class="sxs-lookup"><span data-stu-id="21f90-126">azure/cloud-console</span></span>                   |
| <span data-ttu-id="21f90-127">함수</span><span class="sxs-lookup"><span data-stu-id="21f90-127">Functions</span></span>                 | <span data-ttu-id="21f90-128">azure/compute/functions</span><span class="sxs-lookup"><span data-stu-id="21f90-128">azure/compute/functions</span></span>               |
| <span data-ttu-id="21f90-129">IoT(사물 인터넷) - 허브</span><span class="sxs-lookup"><span data-stu-id="21f90-129">Internet of Things - Hub</span></span>  | <span data-ttu-id="21f90-130">azure/iot/hub</span><span class="sxs-lookup"><span data-stu-id="21f90-130">azure/iot/hub</span></span>                         |
| <span data-ttu-id="21f90-131">HDInsight</span><span class="sxs-lookup"><span data-stu-id="21f90-131">HDInsight</span></span>                 | <span data-ttu-id="21f90-132">azure/data/hdinsight</span><span class="sxs-lookup"><span data-stu-id="21f90-132">azure/data/hdinsight</span></span>                  |
| <span data-ttu-id="21f90-133">Jenkins</span><span class="sxs-lookup"><span data-stu-id="21f90-133">Jenkins</span></span>                   | <span data-ttu-id="21f90-134">azure/jenkins</span><span class="sxs-lookup"><span data-stu-id="21f90-134">azure/jenkins</span></span>                         |
| <span data-ttu-id="21f90-135">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="21f90-135">Machine Learning</span></span>          | <span data-ttu-id="21f90-136">azure/data/machile-learning</span><span class="sxs-lookup"><span data-stu-id="21f90-136">azure/data/machile-learning</span></span>           |
| <span data-ttu-id="21f90-137">서비스 패브릭</span><span class="sxs-lookup"><span data-stu-id="21f90-137">Service Fabric</span></span>            | <span data-ttu-id="21f90-138">azure/compute/service-fabric</span><span class="sxs-lookup"><span data-stu-id="21f90-138">azure/compute/service-fabric</span></span>          |
| <span data-ttu-id="21f90-139">VSTS</span><span class="sxs-lookup"><span data-stu-id="21f90-139">VSTS</span></span>                      | <span data-ttu-id="21f90-140">azure/vsts</span><span class="sxs-lookup"><span data-stu-id="21f90-140">azure/vsts</span></span>                            |


## <a name="next-steps"></a><span data-ttu-id="21f90-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="21f90-141">Next steps</span></span>
[<span data-ttu-id="21f90-142">레지스트리 및 지원되는 서비스와 오케스트레이터에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="21f90-142">Learn more about registries and the supported services and orchestrators</span></span>](container-registry-intro.md)
