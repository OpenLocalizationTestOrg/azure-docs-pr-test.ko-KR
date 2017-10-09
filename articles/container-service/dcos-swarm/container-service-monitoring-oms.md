---
title: "aaaMonitor Azure DC/OS 클러스터 운영 관리 | Microsoft Docs"
description: "Microsoft Operations Management Suite를 사용하여 Azure Container Service DC/OS 클러스터를 모니터링합니다."
services: container-service
documentationcenter: 
author: keikhara
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 11/17/2016
ms.author: keikhara
ms.custom: mvc
ms.openlocfilehash: 0ebfa3ba3cef8f0205b15731b0e91f5b304bc8fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-operations-management-suite"></a><span data-ttu-id="ae1ab-103">Operations Management Suite를 사용하여 Azure Container Service DC/OS 클러스터 모니터링</span><span class="sxs-lookup"><span data-stu-id="ae1ab-103">Monitor an Azure Container Service DC/OS cluster with Operations Management Suite</span></span>

<span data-ttu-id="ae1ab-104">OMS(Microsoft Operations Management Suite)는 온-프레미스 및 클라우드 인프라를 관리 및 보호하도록 도와주는 Microsoft의 클라우드 기반 IT 관리 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-104">Microsoft Operations Management Suite (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="ae1ab-105">컨테이너에서 hello 컨테이너 인벤토리 보기, 성능 및 단일 위치에 있는 로그를 사용 하면 OMS 로그 분석 솔루션을 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-105">Container Solution is a solution in OMS Log Analytics, which helps you view hello container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="ae1ab-106">감사, 중앙된 위치에 hello 로그를 확인 하 여 컨테이너 문제 해결 및 사용 과다 컨테이너 호스트에 잡음이 있는 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-106">You can audit, troubleshoot containers by viewing hello logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="ae1ab-107">컨테이너 솔루션에 대 한 자세한 내용은 읽어보십시오 toothe [컨테이너, 로그 분석 솔루션](../../log-analytics/log-analytics-containers.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-107">For more information about Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="setting-up-oms-from-hello-dcos-universe"></a><span data-ttu-id="ae1ab-108">Hello DC/OS universe에서 OMS를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-108">Setting up OMS from hello DC/OS universe</span></span>


<span data-ttu-id="ae1ab-109">이 문서에서는 DC/OS를 설정 하 고 간단한 웹 컨테이너 응용 프로그램에서는 hello 클러스터에 배포 하는 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-109">This article assumes that you have set up an DC/OS and have deployed simple web container applications on hello cluster.</span></span>

### <a name="pre-requisite"></a><span data-ttu-id="ae1ab-110">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="ae1ab-110">Pre-requisite</span></span>
- <span data-ttu-id="ae1ab-111">[Microsoft Azure 구독](https://azure.microsoft.com/free/) - 무료로 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-111">[Microsoft Azure Subscription](https://azure.microsoft.com/free/) - You can get this for free.</span></span>  
- <span data-ttu-id="ae1ab-112">Microsoft OMS 작업 영역 설치 - 아래 "3단계" 참조</span><span class="sxs-lookup"><span data-stu-id="ae1ab-112">Microsoft OMS Workspace Setup - see "Step 3" below</span></span>
- <span data-ttu-id="ae1ab-113">[DC/OS CLI](https://dcos.io/docs/1.8/usage/cli/install/) 설치</span><span class="sxs-lookup"><span data-stu-id="ae1ab-113">[DC/OS CLI](https://dcos.io/docs/1.8/usage/cli/install/) installed.</span></span>

1. <span data-ttu-id="ae1ab-114">Hello DC/OS 대시보드에서 Universe 및 아래와 같이 'OMS'에 대 한 검색을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-114">In hello DC/OS dashboard, click on Universe and search for ‘OMS’ as shown below.</span></span>

![](media/container-service-monitoring-oms/image2.png)

2. <span data-ttu-id="ae1ab-115">**Install**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-115">Click **Install**.</span></span> <span data-ttu-id="ae1ab-116">Pop를 hello OMS 버전 정보와 함께 표시 됩니다는 및 **패키지 설치** 또는 **고급 설치** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-116">You will see a pop up with hello OMS version information and an **Install Package** or **Advanced Installation** button.</span></span> <span data-ttu-id="ae1ab-117">클릭할 때 **고급 설치**, toohello 안내는 **OMS 어댑터별 구성 속성** 페이지.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-117">When you click **Advanced Installation**, which leads you toohello **OMS specific configuration properties** page.</span></span>

![](media/container-service-monitoring-oms/image3.png)

![](media/container-service-monitoring-oms/image4.png)

3. <span data-ttu-id="ae1ab-118">여기에서는 묻는 tooenter hello `wsid` (hello OMS 작업 영역 ID) 및 `wskey` (hello OMS 기본 키 hello 작업 영역 id에 대 한).</span><span class="sxs-lookup"><span data-stu-id="ae1ab-118">Here, you will be asked tooenter hello `wsid` (hello OMS workspace ID) and `wskey` (hello OMS primary key for hello workspace id).</span></span> <span data-ttu-id="ae1ab-119">두 tooget `wsid` 및 `wskey` toocreate OMS 계정에 필요한 <https://mms.microsoft.com>합니다. Hello 단계 toocreate 계정을 수행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-119">tooget both `wsid` and `wskey` you need toocreate an OMS account at <https://mms.microsoft.com>. Please follow hello steps toocreate an account.</span></span> <span data-ttu-id="ae1ab-120">Tooobtain hello 계정 만들기를 완료 해야 사용자 `wsid` 및 `wskey` 클릭 하 여 **설정**, 다음 **연결 된 원본**, 차례로 **Linux 서버** 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-120">Once you are done creating hello account, you need tooobtain your `wsid` and `wskey` by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

4. <span data-ttu-id="ae1ab-121">인스턴스를 선택 hello 숫자 하면 OMS 고 hello '검토 하 고 설치' 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-121">Select hello number you OMS instances that you want and click hello ‘Review and Install’ button.</span></span> <span data-ttu-id="ae1ab-122">일반적으로 toohave hello 수가 VM 에이전트 클러스터에 있는 수가 인스턴스 같은 toohello OMS 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-122">Typically, you will want toohave hello number of OMS instances equal toohello number of VM’s you have in your agent cluster.</span></span> <span data-ttu-id="ae1ab-123">Linux 용 OMS 에이전트 toocollect 모니터링 정보와 로깅 정보 브로드캐스트하며 각 VM에서 개별 컨테이너로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-123">OMS Agent for Linux is installs as individual containers on each VM that it wants toocollect information for monitoring and logging information.</span></span>

## <a name="setting-up-a-simple-oms-dashboard"></a><span data-ttu-id="ae1ab-124">간단한 OMS 대시보드 설정</span><span class="sxs-lookup"><span data-stu-id="ae1ab-124">Setting up a simple OMS dashboard</span></span>

<span data-ttu-id="ae1ab-125">Hello Vm에 Linux 용 OMS 에이전트 hello를 설치한 후 다음 단계를 OMS 대시보드에 hello tooset입니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-125">Once you have installed hello OMS Agent for Linux on hello VMs, next step is tooset up hello OMS dashboard.</span></span> <span data-ttu-id="ae1ab-126">두 가지 방법으로 toodo이: OMS 포털 또는 Azure 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-126">There are two ways toodo this: OMS Portal or Azure Portal.</span></span>

### <a name="oms-portal"></a><span data-ttu-id="ae1ab-127">OMS 포털</span><span class="sxs-lookup"><span data-stu-id="ae1ab-127">OMS Portal</span></span> 

<span data-ttu-id="ae1ab-128">Toohello OMS 포털에 로그인 (<https://mms.microsoft.com>) toohello 이동 **솔루션 갤러리**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-128">Log in toohello OMS portal (<https://mms.microsoft.com>) and go toohello **Solution Gallery**.</span></span>

![](media/container-service-monitoring-oms/image6.png)

<span data-ttu-id="ae1ab-129">Hello에 있는 경우 **솔루션 갤러리**선택, **컨테이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-129">Once you are in hello **Solution Gallery**, select **Containers**.</span></span>

![](media/container-service-monitoring-oms/image7.png)

<span data-ttu-id="ae1ab-130">Hello 컨테이너 솔루션을 선택한 후 hello 타일 hello OMS 개요 대시보드 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-130">Once you’ve selected hello Container Solution, you will see hello tile on hello OMS Overview Dashboard page.</span></span> <span data-ttu-id="ae1ab-131">수집 된 hello 컨테이너 데이터는 인덱싱된 나타납니다 hello 타일 솔루션 보기 타일에 대 한 정보로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-131">Once hello ingested container data is indexed, you will see hello tile populated with information on the solution view tiles.</span></span>

![](media/container-service-monitoring-oms/image8.png)

### <a name="azure-portal"></a><span data-ttu-id="ae1ab-132">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="ae1ab-132">Azure Portal</span></span> 

<span data-ttu-id="ae1ab-133">TooAzure 포털에 로그인 <https://portal.microsoft.com/>합니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-133">Login tooAzure portal at <https://portal.microsoft.com/>.</span></span> <span data-ttu-id="ae1ab-134">**마켓플레이스**로 이동하고 **모니터링 + 관리**를 선택한 다음 **모두 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-134">Go to **Marketplace**, select **Monitoring + management** and click **See All**.</span></span> <span data-ttu-id="ae1ab-135">그런 다음 검색 상자에서 `containers`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-135">Then Type `containers` in search.</span></span> <span data-ttu-id="ae1ab-136">"컨테이너" hello 검색 결과에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-136">You will see "containers" in hello search results.</span></span> <span data-ttu-id="ae1ab-137">**컨테이너**를 선택하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-137">Select **Containers** and click **Create**.</span></span>

![](media/container-service-monitoring-oms/image9.png)

<span data-ttu-id="ae1ab-138">**만들기**를 클릭하면 작업 영역을 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-138">Once you click **Create**, it will ask you for your workspace.</span></span> <span data-ttu-id="ae1ab-139">작업 영역을 선택하거나 작업 영역이 없는 경우 새 작업 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-139">Select your workspace or if you do not have one, create a new workspace.</span></span>

![](media/container-service-monitoring-oms/image10.PNG)

<span data-ttu-id="ae1ab-140">작업 영역을 선택했으면 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-140">Once you’ve selected your workspace, click **Create**.</span></span>

![](media/container-service-monitoring-oms/image11.png)

<span data-ttu-id="ae1ab-141">Hello OMS 컨테이너 솔루션에 대 한 자세한 내용은 읽어보십시오 toothe [컨테이너, 로그 분석 솔루션](../../log-analytics/log-analytics-containers.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-141">For more information about hello OMS Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

### <a name="how-tooscale-oms-agent-with-acs-dcos"></a><span data-ttu-id="ae1ab-142">어떻게 tooscale OMS 에이전트와 ACS DC/OS</span><span class="sxs-lookup"><span data-stu-id="ae1ab-142">How tooscale OMS Agent with ACS DC/OS</span></span> 

<span data-ttu-id="ae1ab-143">Hello 실제 노드 수 부족 toohave 설치 된 OMS 에이전트 필요 하거나 더 많은 VM을 추가 하 여 VMSS를 크기 조정, 후 그렇게 hello를 확장 하 여 `msoms` 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-143">In case you need toohave installed OMS agent short of hello actual node count or you are scaling up VMSS by adding more VM, you can do so by scaling hello `msoms` service.</span></span>

<span data-ttu-id="ae1ab-144">TooMarathon 또는 hello DC/o S I c e s 탭으로 이동 수 있으며 노드 수를 확장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-144">You can either go tooMarathon or hello DC/OS UI Services tab and scale up your node count.</span></span>

![](media/container-service-monitoring-oms/image12.PNG)

<span data-ttu-id="ae1ab-145">Hello OMS 에이전트를 아직 배포 하지 않은 tooother 노드인을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-145">This will deploy tooother nodes which have not yet deployed hello OMS agent.</span></span>

## <a name="uninstall-ms-oms"></a><span data-ttu-id="ae1ab-146">MS OMS 제거</span><span class="sxs-lookup"><span data-stu-id="ae1ab-146">Uninstall MS OMS</span></span>

<span data-ttu-id="ae1ab-147">MS OMS toouninstall hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-147">toouninstall MS OMS enter hello following command:</span></span>

```bash
$ dcos package uninstall msoms
```

## <a name="let-us-know"></a><span data-ttu-id="ae1ab-148">알려주세요!!!</span><span class="sxs-lookup"><span data-stu-id="ae1ab-148">Let us know!!!</span></span>
<span data-ttu-id="ae1ab-149">무슨 일입니까?</span><span class="sxs-lookup"><span data-stu-id="ae1ab-149">What works?</span></span> <span data-ttu-id="ae1ab-150">무엇이 필요합니까?</span><span class="sxs-lookup"><span data-stu-id="ae1ab-150">What is missing?</span></span> <span data-ttu-id="ae1ab-151">다른 작업 필요 한가요이 toobe에 대 한 유용한 드립니다?</span><span class="sxs-lookup"><span data-stu-id="ae1ab-151">What else do you need for this toobe useful for you?</span></span> <span data-ttu-id="ae1ab-152"><a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>에 알려주세요.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-152">Let us know at <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae1ab-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ae1ab-153">Next steps</span></span>

 <span data-ttu-id="ae1ab-154">설정한 후 OMS toomonitor 컨테이너, 했으므로[컨테이너 대시보드](../../log-analytics/log-analytics-containers.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae1ab-154">Now that you have set up OMS toomonitor your containers,[see your container dashboard](../../log-analytics/log-analytics-containers.md).</span></span>
