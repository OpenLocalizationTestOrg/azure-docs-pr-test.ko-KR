---
title: "Azure DevTest Lab 정보 | Microsoft Docs"
description: "DevTest Lab에서 Azure 가상 컴퓨터를 쉽게 만들고 관리하고 모니터링할 수 있는 방법 알아보기"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 1b9eed3b-c69a-4c49-a36e-f388efea6f39
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 62e2d214d6d685c7f27c8c45cae161eb25ed1cbd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="about-azure-devtest-labs"></a><span data-ttu-id="241d5-103">Azure DevTest Labs 정보</span><span class="sxs-lookup"><span data-stu-id="241d5-103">About Azure DevTest Labs</span></span>
## <a name="overview"></a><span data-ttu-id="241d5-104">개요</span><span class="sxs-lookup"><span data-stu-id="241d5-104">Overview</span></span>
<span data-ttu-id="241d5-105">개발자와 테스터는 클라우드로 이동하여 해당 환경을 만들고 관리하면서 발생하는 지연을 해결할 방법을 찾고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="241d5-105">Developers and testers are looking to solve the delays in creating and managing their environments by going to the cloud.</span></span>  <span data-ttu-id="241d5-106">Azure에서는 환경 지연 문제가 해결되고 비용 효율적인 새 구조 안에서 셀프 서비스가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="241d5-106">Azure solves the problem of environment delays and allows self-service within a new cost efficient structure.</span></span>  <span data-ttu-id="241d5-107">하지만 개발자와 테스터는 셀프 서비스되는 환경을 구성하기 위해 여전히 상당한 시간을 소비해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="241d5-107">However, developers and testers still need to spend considerable time configuring their self-served environments.</span></span> <span data-ttu-id="241d5-108">또한 의사 결정자는 너무 많은 프로세스 오버헤드를 추가하지 않으면서 클라우드를 활용하여 비용 절감을 최대화하는 방법을 잘 모르고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="241d5-108">Also, decision makers are uncertain about how to leverage the cloud to maximize their cost savings without adding too much process overhead.</span></span>

<span data-ttu-id="241d5-109">Azure DevTest Lab은 개발자와 테스터가 낭비를 최소화하고 비용을 제어하면서 Azure에서 빠르게 환경을 만들 수 있도록 돕는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="241d5-109">Azure DevTest Labs is a service that helps developers and testers quickly create environments in Azure while minimizing waste and controlling cost.</span></span> <span data-ttu-id="241d5-110">재사용이 가능한 템플릿과 아티팩트를 사용하여 Windows와 Linux 환경을 빠르게 프로비전함으로써 최신 버전의 응용 프로그램을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="241d5-110">You can test the latest version of your application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span></span> <span data-ttu-id="241d5-111">배포 파이프라인과 DevTest Lab을 쉽게 통합하여 주문형 환경으로 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="241d5-111">Easily integrate your deployment pipeline with DevTest Labs to provision on-demand environments.</span></span> <span data-ttu-id="241d5-112">여러 개의 테스트 에이전트를 프로비전하여 부하 테스트를 확장하고 교육 및 데모를 위해 미리 프로비전된 환경을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="241d5-112">Scale up your load testing by provisioning multiple test agents, and create pre-provisioned environments for training and demos.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/What-is-Azure-DevTest-Labs/player]
> 
> 

<span data-ttu-id="241d5-113">DevTest Lab은 클라우드에서 개발자 및 테스트 환경을 만들고 구성하고 관리하는 데 다음과 같은 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="241d5-113">DevTest Labs provides the following benefits in creating, configuring, and managing developer and test environments in the cloud</span></span>

## <a name="worry-free-self-service"></a><span data-ttu-id="241d5-114">걱정할 필요가 없는 셀프 서비스</span><span class="sxs-lookup"><span data-stu-id="241d5-114">Worry-free self-service</span></span>
<span data-ttu-id="241d5-115">DevTest Lab을 사용하면 사용자당 VM 수(가상 컴퓨터) 및 랩당 VM 수와 같은 정책을 랩에서 설정할 수 있기 때문에 더 쉽게 비용을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="241d5-115">DevTest Labs makes it easier to control costs by allowing you to set policies on your lab - such as number of virtual machines (VM) per user and number of VMs per lab.</span></span> <span data-ttu-id="241d5-116">또한 DevTest Lab을 사용하면 VM을 자동으로 종료하거나 시작하는 정책을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="241d5-116">DevTest Labs also enables you to create policies to automatically shut down and start VMs.</span></span>

## <a name="quickly-get-to-ready-to-test"></a><span data-ttu-id="241d5-117">빠른 테스트 준비</span><span class="sxs-lookup"><span data-stu-id="241d5-117">Quickly get to ready-to-test</span></span>
<span data-ttu-id="241d5-118">DevTest Lab을 사용하면 팀에서 응용 프로그램 개발 및 테스트를 시작하는 데 필요한 모든 사항이 미리 프로비전된 환경을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="241d5-118">DevTest Labs enables you to create pre-provisioned environments with everything your team needs to start developing and testing applications.</span></span> <span data-ttu-id="241d5-119">응용 프로그램의 마지막 빌드가 설치된 환경을 클레임하고 바로 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="241d5-119">Simply claim the environments where the last good build of your application is installed and get working right away.</span></span> <span data-ttu-id="241d5-120">또는 더 빠르고 간결한 환경을 만들기 위해 컨테이너를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="241d5-120">Or, use containers for even faster and leaner environment creation.</span></span>

## <a name="create-once-use-everywhere"></a><span data-ttu-id="241d5-121">한 번 만들어서 어디에나 사용</span><span class="sxs-lookup"><span data-stu-id="241d5-121">Create once, use everywhere</span></span>
<span data-ttu-id="241d5-122">팀 또는 조직 내에서 환경 템플릿 및 아티팩트(모두 원본 컨트롤에 있음)를 캡처하고 공유하여 개발자 환경 및 테스트 환경을 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="241d5-122">Capture and share environment templates and artifacts within your team or organization - all in source control - to create developer and test environments easily.</span></span>

## <a name="integrates-with-your-existing-toolchain"></a><span data-ttu-id="241d5-123">기존 도구 체인과 통합</span><span class="sxs-lookup"><span data-stu-id="241d5-123">Integrates with your existing toolchain</span></span>
<span data-ttu-id="241d5-124">미리 만들어져 있는 플러그 인 또는 Microsoft의 API를 활용하여 원하는 CI(지속적인 통합) 도구, IDE(통합 개발 환경) 또는 자동화된 릴리스 파이프라인에서 직접 개발/테스트 환경을 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="241d5-124">Leverage pre-made plug-ins or our API to provision Dev/Test environments directly from your preferred continuous integration (CI) tool, integrated development environment (IDE), or automated release pipeline.</span></span> <span data-ttu-id="241d5-125">Microsoft의 포괄적인 명령줄 도구를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="241d5-125">You can also use our comprehensive command-line tool.</span></span>


[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="241d5-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="241d5-126">Next steps</span></span>
[<span data-ttu-id="241d5-127">DevTest Lab 개념</span><span class="sxs-lookup"><span data-stu-id="241d5-127">DevTest Labs concepts</span></span>](devtest-lab-concepts.md)

