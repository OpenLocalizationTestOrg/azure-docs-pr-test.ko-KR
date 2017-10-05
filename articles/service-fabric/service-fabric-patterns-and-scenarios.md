---
title: "Azure Service Fabric 패턴 및 시나리오 | Microsoft Docs"
description: "Service Fabric에서 마이크로 서비스를 개발, 디자인 및 운영하기 위한 모범 사례와 검증된 재사용 가능한 패턴에 대해 알아봅니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: d5aa75ff-98b9-4573-a2e5-7f5ab288157a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: fb2fa495758433e357722427b1c162420935955d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="service-fabric-patterns-and-scenarios"></a><span data-ttu-id="7917e-103">Service Fabric 패턴 및 시나리오</span><span class="sxs-lookup"><span data-stu-id="7917e-103">Service Fabric patterns and scenarios</span></span>
<span data-ttu-id="7917e-104">Azure Service Fabric을 사용하여 대규모 마이크로 서비스를 빌드하려면 PaaS(platform as a service)를 디자인하고 빌드한 전문가에게 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7917e-104">If you’re looking at building large-scale microservices using Azure Service Fabric, learn from the experts who designed and built this platform as a service (PaaS).</span></span> <span data-ttu-id="7917e-105">적절한 아키텍처를 시작한 다음 응용 프로그램에 대한 리소스를 최적화하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7917e-105">Get started with proper architecture, and then learn how to optimize resources for your application.</span></span> <span data-ttu-id="7917e-106">[Service Fabric 패턴 및 사례](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) 과정에서는 Service Fabric 시나리오 및 응용 프로그램 영역에 대해 실제 고객이 가장 자주 묻는 질문에 답변합니다.</span><span class="sxs-lookup"><span data-stu-id="7917e-106">The [Service Fabric Patterns and Practices](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) course answers the questions most often asked by real-world customers about Service Fabric scenarios and application areas.</span></span>
 
<span data-ttu-id="7917e-107">모범 사례 및 검증된 재사용 가능한 패턴을 사용하여 Service Fabric에서 마이크로 서비스를 디자인, 개발 및 운영하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7917e-107">Find out how to design, develop, and operate your microservices on Service Fabric using best practices and proven, reusable patterns.</span></span> <span data-ttu-id="7917e-108">Service Fabric의 개요를 살펴본 다음 클러스터 최적화 및 보안, 마이그레이션 레거시 앱, 대규모 IoT, 호스팅 게임 엔진 등을 다루는 항목에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7917e-108">Get an overview of Service Fabric and then dive deep into topics that cover cluster optimization and security, migrating legacy apps, IoT at scale, hosting game engines, and more.</span></span> <span data-ttu-id="7917e-109">다양한 워크로드에 대한 지속적인 업데이트와 Linux Support 및 컨테이너에 대한 자세한 내용도 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="7917e-109">Look at continuous delivery for various workloads, and even get the details on Linux support and containers.</span></span> 

## <a name="introduction"></a><span data-ttu-id="7917e-110">소개</span><span class="sxs-lookup"><span data-stu-id="7917e-110">Introduction</span></span>
<span data-ttu-id="7917e-111">모범 사례를 탐색하고 IaaS(서비스 제공 인프라)를 통한 PaaS(Platform as a Service) over 선택에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7917e-111">Explore best practices, and learn about choosing platform as a service (PaaS) over infrastructure as a service (IaaS).</span></span> <span data-ttu-id="7917e-112">다음과 같은 검증된 응용 프로그램 디자인 원칙에 대한 자세한 내용을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7917e-112">Get the details on following proven application design principles.</span></span>

<table><tr><th><span data-ttu-id="7917e-113">비디오</span><span class="sxs-lookup"><span data-stu-id="7917e-113">Video</span></span></th><th><span data-ttu-id="7917e-114">PowerPoint 데크</span><span class="sxs-lookup"><span data-stu-id="7917e-114">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=N2KwbbSGD_6405167344">
<img src="./media/service-fabric-patterns-and-scenarios/intro.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="7917e-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Service Fabric 소개</a></span><span class="sxs-lookup"><span data-stu-id="7917e-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Introduction to Service Fabric</a></span></span></td></tr>
</table>

## <a name="cluster-planning-and-management"></a><span data-ttu-id="7917e-116">클러스터 계획 및 관리</span><span class="sxs-lookup"><span data-stu-id="7917e-116">Cluster planning and management</span></span>
<span data-ttu-id="7917e-117">Azure Service Fabric에 있어서 용량 계획, 클러스터 최적화 및 클러스터 보안에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7917e-117">Learn about capacity planning, cluster optimization, and cluster security, in this look at Azure Service Fabric.</span></span>

<table><tr><th><span data-ttu-id="7917e-118">비디오</span><span class="sxs-lookup"><span data-stu-id="7917e-118">Video</span></span></th><th><span data-ttu-id="7917e-119">PowerPoint 데크</span><span class="sxs-lookup"><span data-stu-id="7917e-119">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=cyDYZcSGD_2805167344">
<img src="./media/service-fabric-patterns-and-scenarios/cluster.png" WIDTH="360" HEIGHT="244">
</a></td><td> <span data-ttu-id="7917e-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">클러스터 계획 및 관리</a></span><span class="sxs-lookup"><span data-stu-id="7917e-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Cluster Planning and Management</a></span></span></td></tr>
</table>

## <a name="hyper-scale-web"></a><span data-ttu-id="7917e-121">초대형 웹</span><span class="sxs-lookup"><span data-stu-id="7917e-121">Hyper-scale web</span></span>
<span data-ttu-id="7917e-122">가용성과 안정성, 초대형 및 상태 관리를 비롯한 초대형 웹 관련 개념을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="7917e-122">Review concepts around hyper-scale web, including availability and reliability, hyper-scale, and state management.</span></span>

<table><tr><th><span data-ttu-id="7917e-123">비디오</span><span class="sxs-lookup"><span data-stu-id="7917e-123">Video</span></span></th><th><span data-ttu-id="7917e-124">PowerPoint 데크</span><span class="sxs-lookup"><span data-stu-id="7917e-124">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=NgldAdSGD_405167344">
<img src="./media/service-fabric-patterns-and-scenarios/hyperscaleweb.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="7917e-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">하이퍼스케일(hyper-scale) 웹</a></span><span class="sxs-lookup"><span data-stu-id="7917e-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Hyper-scale web</a></span></span></td></tr>
</table>

## <a name="iot"></a><span data-ttu-id="7917e-126">IoT</span><span class="sxs-lookup"><span data-stu-id="7917e-126">IoT</span></span>
<span data-ttu-id="7917e-127">Azure IoT 파이프라인, 다중 테넌트 지원 및 대규모 IoT를 비롯하여 Azure Service Fabric의 컨텍스트에서 IoT(사물 인터넷)를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="7917e-127">Explore the Internet of Things (IoT) in the context of Azure Service Fabric, including the Azure IoT pipeline, multi-tenancy, and IoT at scale.</span></span>

<table><tr><th><span data-ttu-id="7917e-128">비디오</span><span class="sxs-lookup"><span data-stu-id="7917e-128">Video</span></span></th><th><span data-ttu-id="7917e-129">PowerPoint 데크</span><span class="sxs-lookup"><span data-stu-id="7917e-129">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=naFUVeSGD_1505167344">
<img src="./media/service-fabric-patterns-and-scenarios/iot.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="7917e-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span><span class="sxs-lookup"><span data-stu-id="7917e-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span></span></td></tr>
</table>

## <a name="gaming"></a><span data-ttu-id="7917e-131">게임</span><span class="sxs-lookup"><span data-stu-id="7917e-131">Gaming</span></span>
<span data-ttu-id="7917e-132">턴 기반 게임, 대화형 게임 및 기존 게임 엔진 호스팅에 대해 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="7917e-132">Look at turn-based games, interactive games, and hosting existing game engines.</span></span>

<table><tr><th><span data-ttu-id="7917e-133">비디오</span><span class="sxs-lookup"><span data-stu-id="7917e-133">Video</span></span></th><th><span data-ttu-id="7917e-134">PowerPoint 데크</span><span class="sxs-lookup"><span data-stu-id="7917e-134">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=6wECzeSGD_3805167344">
<img src="./media/service-fabric-patterns-and-scenarios/gaming.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="7917e-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">게임</a></span><span class="sxs-lookup"><span data-stu-id="7917e-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Gaming</a></span></span></td></tr>
</table>

## <a name="continuous-delivery"></a><span data-ttu-id="7917e-136">지속적인 업데이트</span><span class="sxs-lookup"><span data-stu-id="7917e-136">Continuous delivery</span></span>
<span data-ttu-id="7917e-137">Visual Studio Team Services를 통한 지속적인 통합/지속적인 업데이트, 워크플로 빌드/패키지/게시, 다중 환경 설치 및 서비스 패키지/공유를 포함한 개념을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="7917e-137">Explore concepts, including continuous integration/continuous delivery with Visual Studio Team Services, build/package/publish workflow, multi-environment setup, and service package/share.</span></span>

<table><tr><th><span data-ttu-id="7917e-138">비디오</span><span class="sxs-lookup"><span data-stu-id="7917e-138">Video</span></span></th><th><span data-ttu-id="7917e-139">PowerPoint 데크</span><span class="sxs-lookup"><span data-stu-id="7917e-139">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=78h5ofSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/cd.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="7917e-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">지속적인 업데이트</a></span><span class="sxs-lookup"><span data-stu-id="7917e-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Continuous delivery</a></span></span></td></tr>
</table>

## <a name="migration"></a><span data-ttu-id="7917e-141">마이그레이션</span><span class="sxs-lookup"><span data-stu-id="7917e-141">Migration</span></span>
<span data-ttu-id="7917e-142">레거시 앱의 마이그레이션 및 클라우드 서비스에서의 마이그레이션에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7917e-142">Learn about migrating from a cloud service, in addition to migration of legacy apps.</span></span>

<table><tr><th><span data-ttu-id="7917e-143">비디오</span><span class="sxs-lookup"><span data-stu-id="7917e-143">Video</span></span></th><th><span data-ttu-id="7917e-144">PowerPoint 데크</span><span class="sxs-lookup"><span data-stu-id="7917e-144">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=hd1cMgSGD_5605167344">
<img src="./media/service-fabric-patterns-and-scenarios/migration.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="7917e-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">마이그레이션</a></span><span class="sxs-lookup"><span data-stu-id="7917e-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Migration</a></span></span></td></tr>
</table>

## <a name="containers-and-linux-support"></a><span data-ttu-id="7917e-146">컨테이너 및 Linux Support</span><span class="sxs-lookup"><span data-stu-id="7917e-146">Containers and Linux support</span></span>
<span data-ttu-id="7917e-147">"컨테이너의 필요성"에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7917e-147">Get the answer to the question, "Why containers?"</span></span> <span data-ttu-id="7917e-148">Windows 컨테이너, Linux Support 및 Linux 컨테이너 오케스트레이션에 대한 미리 보기에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7917e-148">Learn about the preview for Windows containers, Linux supports, and Linux containers orchestration.</span></span> <span data-ttu-id="7917e-149">.NET Core 앱을 Linux로 마이그레이션하는 방법도 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7917e-149">Plus, find out how to migrate .NET Core apps to Linux.</span></span>

<table><tr><th><span data-ttu-id="7917e-150">비디오</span><span class="sxs-lookup"><span data-stu-id="7917e-150">Video</span></span></th><th><span data-ttu-id="7917e-151">PowerPoint 데크</span><span class="sxs-lookup"><span data-stu-id="7917e-151">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=V1ERJhSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/containers.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="7917e-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">컨테이너 및 Linux 지원</a></span><span class="sxs-lookup"><span data-stu-id="7917e-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Containers and Linux support</a></span></span></td></tr>
</table>

## <a name="next-steps"></a><span data-ttu-id="7917e-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7917e-153">Next steps</span></span>
<span data-ttu-id="7917e-154">지금까지 Service Fabric 패턴 및 시나리오에 대해 배웠습니다. 이제 [클러스터 만들기 및 관리](service-fabric-deploy-anywhere.md), [Cloud Services 앱을 Service Fabric으로 마이그레이션](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [지속적인 업데이트 설정](service-fabric-set-up-continuous-integration.md) 및 [컨테이너 배포](service-fabric-containers-overview.md) 방법에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7917e-154">Now that you've learned about Service Fabric patterns and scenarios, read more about how to [create and manage clusters](service-fabric-deploy-anywhere.md), [migrate Cloud Services apps to Service Fabric](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [set up continuous delivery](service-fabric-set-up-continuous-integration.md), and [deploy containers](service-fabric-containers-overview.md).</span></span>
