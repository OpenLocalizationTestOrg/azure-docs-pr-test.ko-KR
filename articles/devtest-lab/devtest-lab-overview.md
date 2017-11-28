---
title: Azure DevTest Labs aaaAbout | Microsoft Docs
description: "DevTest Labs 수 쉽게 toocreate 확인, 관리 및 Azure 가상 컴퓨터를 모니터링 하는 방법에 대해 알아봅니다"
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
ms.openlocfilehash: 5e5aa683f80144a2f6872c7fa328016120ea6253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="about-azure-devtest-labs"></a><span data-ttu-id="6b9ee-103">Azure DevTest Labs 정보</span><span class="sxs-lookup"><span data-stu-id="6b9ee-103">About Azure DevTest Labs</span></span>
## <a name="overview"></a><span data-ttu-id="6b9ee-104">개요</span><span class="sxs-lookup"><span data-stu-id="6b9ee-104">Overview</span></span>
<span data-ttu-id="6b9ee-105">개발자와 테스터 환경 만들기 및 관리의 toohello 클라우드를 이동 하 여 toosolve hello 지연 보고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b9ee-105">Developers and testers are looking toosolve hello delays in creating and managing their environments by going toohello cloud.</span></span>  <span data-ttu-id="6b9ee-106">Azure 환경 지연의 hello 문제를 해결 하 고 새 비용 효율적인 구조 내에서 셀프 서비스를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9ee-106">Azure solves hello problem of environment delays and allows self-service within a new cost efficient structure.</span></span>  <span data-ttu-id="6b9ee-107">개발자와 테스터 자신의 셀프 서비스 제공된 하는 환경 구성 toospend 데 상당한 시간이 여전히 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9ee-107">However, developers and testers still need toospend considerable time configuring their self-served environments.</span></span> <span data-ttu-id="6b9ee-108">또한 의사 결정권자는 tooleverage hello 클라우드 toomaximize 추가 하지 않고 해당 비용을 절감할 너무 많이 처리 하는 방법을 오버 헤드에 대 한 확실 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6b9ee-108">Also, decision makers are uncertain about how tooleverage hello cloud toomaximize their cost savings without adding too much process overhead.</span></span>

<span data-ttu-id="6b9ee-109">Azure DevTest Lab은 개발자와 테스터가 낭비를 최소화하고 비용을 제어하면서 Azure에서 빠르게 환경을 만들 수 있도록 돕는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="6b9ee-109">Azure DevTest Labs is a service that helps developers and testers quickly create environments in Azure while minimizing waste and controlling cost.</span></span> <span data-ttu-id="6b9ee-110">신속 하 게 다시 사용할 수 있는 템플릿 및 아티팩트를 사용 하 여 Windows 및 Linux 환경 프로 비전 하 여 hello 최신 버전의 응용 프로그램을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b9ee-110">You can test hello latest version of your application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span></span> <span data-ttu-id="6b9ee-111">DevTest Labs tooprovision 주문형 환경을 사용 하 여 쉽게 배포 파이프라인을 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9ee-111">Easily integrate your deployment pipeline with DevTest Labs tooprovision on-demand environments.</span></span> <span data-ttu-id="6b9ee-112">여러 개의 테스트 에이전트를 프로비전하여 부하 테스트를 확장하고 교육 및 데모를 위해 미리 프로비전된 환경을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b9ee-112">Scale up your load testing by provisioning multiple test agents, and create pre-provisioned environments for training and demos.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/What-is-Azure-DevTest-Labs/player]
> 
> 

<span data-ttu-id="6b9ee-113">DevTest Labs 이점을 만들기, 구성 및 관리 hello 클라우드에서 개발자 및 테스트 환경에 따라 hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9ee-113">DevTest Labs provides hello following benefits in creating, configuring, and managing developer and test environments in hello cloud</span></span>

## <a name="worry-free-self-service"></a><span data-ttu-id="6b9ee-114">걱정할 필요가 없는 셀프 서비스</span><span class="sxs-lookup"><span data-stu-id="6b9ee-114">Worry-free self-service</span></span>
<span data-ttu-id="6b9ee-115">DevTest Labs 하면 보다 쉽게 toocontrol 비용 랩-가상 컴퓨터 (VM)의 수와 같은 tooset 정책을 허용 하 여 사용자 및 랩 당 Vm 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b9ee-115">DevTest Labs makes it easier toocontrol costs by allowing you tooset policies on your lab - such as number of virtual machines (VM) per user and number of VMs per lab.</span></span> <span data-ttu-id="6b9ee-116">또한 DevTest Labs 있습니다 toocreate 정책 tooautomatically 종료를 사용 하도록 설정 하 고 Vm을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9ee-116">DevTest Labs also enables you toocreate policies tooautomatically shut down and start VMs.</span></span>

## <a name="quickly-get-tooready-to-test"></a><span data-ttu-id="6b9ee-117">빠르게 tooready-테스트 시작</span><span class="sxs-lookup"><span data-stu-id="6b9ee-117">Quickly get tooready-to-test</span></span>
<span data-ttu-id="6b9ee-118">DevTest Labs toocreate 미리 프로 비전된 환경을 팀 개발 하 고 응용 프로그램을 테스트 toostart 필요한 모든 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b9ee-118">DevTest Labs enables you toocreate pre-provisioned environments with everything your team needs toostart developing and testing applications.</span></span> <span data-ttu-id="6b9ee-119">단순히 hello 정상적인 최신 빌드가 응용 프로그램의 설치 되어 있는 hello 환경 클레임 하 고 바로 작업을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6b9ee-119">Simply claim hello environments where hello last good build of your application is installed and get working right away.</span></span> <span data-ttu-id="6b9ee-120">또는 더 빠르고 간결한 환경을 만들기 위해 컨테이너를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9ee-120">Or, use containers for even faster and leaner environment creation.</span></span>

## <a name="create-once-use-everywhere"></a><span data-ttu-id="6b9ee-121">한 번 만들어서 어디에나 사용</span><span class="sxs-lookup"><span data-stu-id="6b9ee-121">Create once, use everywhere</span></span>
<span data-ttu-id="6b9ee-122">캡처 toocreate 개발자 환경 템플릿 및 내 팀 또는 조직--소스 제어에서 모든 아티팩트를 공유 하 고 테스트 환경을 쉽게 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9ee-122">Capture and share environment templates and artifacts within your team or organization - all in source control - toocreate developer and test environments easily.</span></span>

## <a name="integrates-with-your-existing-toolchain"></a><span data-ttu-id="6b9ee-123">기존 도구 체인과 통합</span><span class="sxs-lookup"><span data-stu-id="6b9ee-123">Integrates with your existing toolchain</span></span>
<span data-ttu-id="6b9ee-124">미리 만든된 플러그 인을 활용 또는 우리의 API tooprovision 개발/테스트 환경 직접 자신의 기본 CI (연속 통합) 도구에서 통합 개발 환경 (IDE) 또는 릴리스 파이프라인을 자동화 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9ee-124">Leverage pre-made plug-ins or our API tooprovision Dev/Test environments directly from your preferred continuous integration (CI) tool, integrated development environment (IDE), or automated release pipeline.</span></span> <span data-ttu-id="6b9ee-125">Microsoft의 포괄적인 명령줄 도구를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b9ee-125">You can also use our comprehensive command-line tool.</span></span>


[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="6b9ee-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6b9ee-126">Next steps</span></span>
[<span data-ttu-id="6b9ee-127">DevTest Lab 개념</span><span class="sxs-lookup"><span data-stu-id="6b9ee-127">DevTest Labs concepts</span></span>](devtest-lab-concepts.md)

