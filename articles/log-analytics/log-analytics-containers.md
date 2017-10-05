---
title: "Azure Log Analytics의 컨테이너 모니터링 솔루션 | Microsoft Docs"
description: "Log Analytics의 컨테이너 모니터링 솔루션을 사용하여 단일 위치에서 Docker 및 Windows 컨테이너 호스트를 보고 관리할 수 있습니다."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e1e4b52b-92d5-4bfa-8a09-ff8c6b5a9f78
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte;banders
ms.openlocfilehash: b2e03531ee401f4552198e5dd50fbfe1d970f0e5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="container-monitoring-solution-in-log-analytics"></a><span data-ttu-id="5f4d7-103">Log Analytics의 컨테이너 모니터링 솔루션</span><span class="sxs-lookup"><span data-stu-id="5f4d7-103">Container Monitoring solution in Log Analytics</span></span>

![컨테이너 기호](./media/log-analytics-containers/containers-symbol.png)

<span data-ttu-id="5f4d7-105">이 문서에서는 단일 위치에서 Docker 및 Windows 컨테이너 호스트를 보고 관리할 수 있게 Log Analytics의 컨테이너 모니터링 솔루션을 설정 및 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-105">This article describes how to set up and use the Container Monitoring solution in Log Analytics, which helps you view and manage your Docker and Windows container hosts in a single location.</span></span> <span data-ttu-id="5f4d7-106">Docker는 IT 인프라에 대한 소프트웨어 배포를 자동화하는 컨테이너를 만드는 데 사용되는 소프트웨어 가상화 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-106">Docker is a software virtualization system used to create containers that automate software deployment to their IT infrastructure.</span></span>

<span data-ttu-id="5f4d7-107">솔루션은 어떤 컨테이너가 실행 중인지, 실행 중인 컨테이너 이미지 및 컨테이너가 실행 중인 위치를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-107">The solution shows which containers are running, what container image they’re running, and where containers are running.</span></span> <span data-ttu-id="5f4d7-108">컨테이너에 사용하는 명령을 표시하는 상세한 감사 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-108">You can view detailed audit information showing commands used with containers.</span></span> <span data-ttu-id="5f4d7-109">또한 중앙화된 로그를 보고 검색하면 원격으로 Docker 또는 Windows 호스트를 보지 않고도 컨테이너의 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-109">And, you can troubleshoot containers by viewing and searching centralized logs without having to remotely view Docker or Windows hosts.</span></span> <span data-ttu-id="5f4d7-110">호스트에서 성가시고 과도한 리소스를 소모하는 컨테이너를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-110">You can find containers that may be noisy and consuming excess resources on a host.</span></span> <span data-ttu-id="5f4d7-111">또한 컨테이너에 대해 중앙화된 CPU 메모리, 저장소, 네트워크 사용 및 성능 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-111">And, you can view centralized CPU, memory, storage, and network usage and performance information for containers.</span></span> <span data-ttu-id="5f4d7-112">Windows를 실행하는 컴퓨터에서 Windows Server, Hyper-V, Docker 컨테이너에서 로그를 중앙 집중화 및 비교할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-112">On computers running Windows, you can centralize and compare logs from Windows Server, Hyper-V, and Docker containers.</span></span> <span data-ttu-id="5f4d7-113">솔루션은 다음과 같은 컨테이너 오케스트레이터를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-113">The solution supports the following container orchestrators:</span></span>

- <span data-ttu-id="5f4d7-114">Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="5f4d7-114">Docker Swarm</span></span>
- <span data-ttu-id="5f4d7-115">DC/OS</span><span class="sxs-lookup"><span data-stu-id="5f4d7-115">DC/OS</span></span>
- <span data-ttu-id="5f4d7-116">kubernetes</span><span class="sxs-lookup"><span data-stu-id="5f4d7-116">Kubernetes</span></span>
- <span data-ttu-id="5f4d7-117">서비스 패브릭</span><span class="sxs-lookup"><span data-stu-id="5f4d7-117">Service Fabric</span></span>
- <span data-ttu-id="5f4d7-118">Red Hat OpenShift</span><span class="sxs-lookup"><span data-stu-id="5f4d7-118">Red Hat OpenShift</span></span>


<span data-ttu-id="5f4d7-119">다음 다이어그램에서는 OMS에서 다양한 컨테이너 호스트와 에이전트 간의 관계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-119">The following diagram shows the relationships between various container hosts and agents with OMS.</span></span>

![컨테이너 다이어그램](./media/log-analytics-containers/containers-diagram.png)

## <a name="system-requirements"></a><span data-ttu-id="5f4d7-121">시스템 요구 사항</span><span class="sxs-lookup"><span data-stu-id="5f4d7-121">System requirements</span></span>

<span data-ttu-id="5f4d7-122">시작하기 전에 다음 세부 정보를 검토하여 필수 구성 요소를 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-122">Before starting, review the following details to verify you meet the prerequisites.</span></span>

### <a name="container-monitoring-solution-support-for-docker-orchestrator-and-os-platform"></a><span data-ttu-id="5f4d7-123">Docker Orchestrator 및 OS 플랫폼에 대한 컨테이너 모니터링 솔루션 지원</span><span class="sxs-lookup"><span data-stu-id="5f4d7-123">Container monitoring solution support for Docker Orchestrator and OS platform</span></span>
<span data-ttu-id="5f4d7-124">아래 표에는 Log Analytics를 통한 컨테이너 인벤토리/성능/로그의 Docker 오케스트레이션 및 운영 체제 모니터링 지원에 대한 설명이 요약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-124">The following table outlines the Docker orchestration and operating system monitoring support of container inventory, performance, and logs with Log Analytics.</span></span>   

| | <span data-ttu-id="5f4d7-125">ACS</span><span class="sxs-lookup"><span data-stu-id="5f4d7-125">ACS</span></span> | <span data-ttu-id="5f4d7-126">Linux</span><span class="sxs-lookup"><span data-stu-id="5f4d7-126">Linux</span></span> | <span data-ttu-id="5f4d7-127">Windows</span><span class="sxs-lookup"><span data-stu-id="5f4d7-127">Windows</span></span> | <span data-ttu-id="5f4d7-128">컨테이너</span><span class="sxs-lookup"><span data-stu-id="5f4d7-128">Container</span></span><br><span data-ttu-id="5f4d7-129">인벤토리</span><span class="sxs-lookup"><span data-stu-id="5f4d7-129">Inventory</span></span> | <span data-ttu-id="5f4d7-130">이미지</span><span class="sxs-lookup"><span data-stu-id="5f4d7-130">Image</span></span><br><span data-ttu-id="5f4d7-131">인벤토리</span><span class="sxs-lookup"><span data-stu-id="5f4d7-131">Inventory</span></span> | <span data-ttu-id="5f4d7-132">노드</span><span class="sxs-lookup"><span data-stu-id="5f4d7-132">Node</span></span><br><span data-ttu-id="5f4d7-133">인벤토리</span><span class="sxs-lookup"><span data-stu-id="5f4d7-133">Inventory</span></span> | <span data-ttu-id="5f4d7-134">컨테이너</span><span class="sxs-lookup"><span data-stu-id="5f4d7-134">Container</span></span><br><span data-ttu-id="5f4d7-135">성능</span><span class="sxs-lookup"><span data-stu-id="5f4d7-135">Performance</span></span> | <span data-ttu-id="5f4d7-136">컨테이너</span><span class="sxs-lookup"><span data-stu-id="5f4d7-136">Container</span></span><br><span data-ttu-id="5f4d7-137">이벤트</span><span class="sxs-lookup"><span data-stu-id="5f4d7-137">Event</span></span> | <span data-ttu-id="5f4d7-138">이벤트</span><span class="sxs-lookup"><span data-stu-id="5f4d7-138">Event</span></span><br><span data-ttu-id="5f4d7-139">로그</span><span class="sxs-lookup"><span data-stu-id="5f4d7-139">Log</span></span> | <span data-ttu-id="5f4d7-140">컨테이너</span><span class="sxs-lookup"><span data-stu-id="5f4d7-140">Container</span></span><br><span data-ttu-id="5f4d7-141">로그</span><span class="sxs-lookup"><span data-stu-id="5f4d7-141">Log</span></span> |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| <span data-ttu-id="5f4d7-142">kubernetes</span><span class="sxs-lookup"><span data-stu-id="5f4d7-142">Kubernetes</span></span> | <span data-ttu-id="5f4d7-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-143">&#8226;</span></span> | <span data-ttu-id="5f4d7-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-144">&#8226;</span></span> | | <span data-ttu-id="5f4d7-145">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-145">&#8226;</span></span> | <span data-ttu-id="5f4d7-146">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-146">&#8226;</span></span> | <span data-ttu-id="5f4d7-147">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-147">&#8226;</span></span> | <span data-ttu-id="5f4d7-148">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-148">&#8226;</span></span> | <span data-ttu-id="5f4d7-149">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-149">&#8226;</span></span> | <span data-ttu-id="5f4d7-150">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-150">&#8226;</span></span> | <span data-ttu-id="5f4d7-151">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-151">&#8226;</span></span> |
| <span data-ttu-id="5f4d7-152">Mesosphere</span><span class="sxs-lookup"><span data-stu-id="5f4d7-152">Mesosphere</span></span><br><span data-ttu-id="5f4d7-153">DC/OS</span><span class="sxs-lookup"><span data-stu-id="5f4d7-153">DC/OS</span></span> | <span data-ttu-id="5f4d7-154">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-154">&#8226;</span></span> | <span data-ttu-id="5f4d7-155">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-155">&#8226;</span></span> | | <span data-ttu-id="5f4d7-156">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-156">&#8226;</span></span> | <span data-ttu-id="5f4d7-157">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-157">&#8226;</span></span> | <span data-ttu-id="5f4d7-158">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-158">&#8226;</span></span> | <span data-ttu-id="5f4d7-159">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-159">&#8226;</span></span>| <span data-ttu-id="5f4d7-160">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-160">&#8226;</span></span> | <span data-ttu-id="5f4d7-161">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-161">&#8226;</span></span> | <span data-ttu-id="5f4d7-162">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-162">&#8226;</span></span> |
| <span data-ttu-id="5f4d7-163">Docker</span><span class="sxs-lookup"><span data-stu-id="5f4d7-163">Docker</span></span><br><span data-ttu-id="5f4d7-164">Swarm</span><span class="sxs-lookup"><span data-stu-id="5f4d7-164">Swarm</span></span> | <span data-ttu-id="5f4d7-165">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-165">&#8226;</span></span> | <span data-ttu-id="5f4d7-166">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-166">&#8226;</span></span> | <span data-ttu-id="5f4d7-167">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-167">&#8226;</span></span> | <span data-ttu-id="5f4d7-168">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-168">&#8226;</span></span> | <span data-ttu-id="5f4d7-169">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-169">&#8226;</span></span> | <span data-ttu-id="5f4d7-170">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-170">&#8226;</span></span> | <span data-ttu-id="5f4d7-171">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-171">&#8226;</span></span> | <span data-ttu-id="5f4d7-172">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-172">&#8226;</span></span> | | <span data-ttu-id="5f4d7-173">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-173">&#8226;</span></span> |
| <span data-ttu-id="5f4d7-174">부여</span><span class="sxs-lookup"><span data-stu-id="5f4d7-174">Service</span></span><br><span data-ttu-id="5f4d7-175">Fabric</span><span class="sxs-lookup"><span data-stu-id="5f4d7-175">Fabric</span></span> | | | <span data-ttu-id="5f4d7-176">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-176">&#8226;</span></span> | <span data-ttu-id="5f4d7-177">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-177">&#8226;</span></span> | <span data-ttu-id="5f4d7-178">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-178">&#8226;</span></span> | <span data-ttu-id="5f4d7-179">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-179">&#8226;</span></span> | <span data-ttu-id="5f4d7-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-180">&#8226;</span></span> | <span data-ttu-id="5f4d7-181">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-181">&#8226;</span></span> | <span data-ttu-id="5f4d7-182">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-182">&#8226;</span></span> | <span data-ttu-id="5f4d7-183">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-183">&#8226;</span></span> |
| <span data-ttu-id="5f4d7-184">Red Hat Open</span><span class="sxs-lookup"><span data-stu-id="5f4d7-184">Red Hat Open</span></span><br><span data-ttu-id="5f4d7-185">Shift</span><span class="sxs-lookup"><span data-stu-id="5f4d7-185">Shift</span></span> | | <span data-ttu-id="5f4d7-186">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-186">&#8226;</span></span> | | <span data-ttu-id="5f4d7-187">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-187">&#8226;</span></span> | <span data-ttu-id="5f4d7-188">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-188">&#8226;</span></span>| <span data-ttu-id="5f4d7-189">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-189">&#8226;</span></span> | <span data-ttu-id="5f4d7-190">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-190">&#8226;</span></span> | <span data-ttu-id="5f4d7-191">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-191">&#8226;</span></span> | | <span data-ttu-id="5f4d7-192">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-192">&#8226;</span></span> |
| <span data-ttu-id="5f4d7-193">Windows Server</span><span class="sxs-lookup"><span data-stu-id="5f4d7-193">Windows Server</span></span><br><span data-ttu-id="5f4d7-194">(독립 실행형)</span><span class="sxs-lookup"><span data-stu-id="5f4d7-194">(standalone)</span></span> | | | <span data-ttu-id="5f4d7-195">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-195">&#8226;</span></span> | <span data-ttu-id="5f4d7-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-196">&#8226;</span></span> | <span data-ttu-id="5f4d7-197">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-197">&#8226;</span></span> | <span data-ttu-id="5f4d7-198">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-198">&#8226;</span></span> | <span data-ttu-id="5f4d7-199">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-199">&#8226;</span></span> | <span data-ttu-id="5f4d7-200">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-200">&#8226;</span></span> | | <span data-ttu-id="5f4d7-201">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-201">&#8226;</span></span> |
| <span data-ttu-id="5f4d7-202">Linux 서버</span><span class="sxs-lookup"><span data-stu-id="5f4d7-202">Linux Server</span></span><br><span data-ttu-id="5f4d7-203">(독립 실행형)</span><span class="sxs-lookup"><span data-stu-id="5f4d7-203">(standalone)</span></span> | | <span data-ttu-id="5f4d7-204">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-204">&#8226;</span></span> | | <span data-ttu-id="5f4d7-205">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-205">&#8226;</span></span> | <span data-ttu-id="5f4d7-206">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-206">&#8226;</span></span> | <span data-ttu-id="5f4d7-207">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-207">&#8226;</span></span> | <span data-ttu-id="5f4d7-208">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-208">&#8226;</span></span> | <span data-ttu-id="5f4d7-209">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-209">&#8226;</span></span> | | <span data-ttu-id="5f4d7-210">&#8226;</span><span class="sxs-lookup"><span data-stu-id="5f4d7-210">&#8226;</span></span> |


### <a name="docker-versions-supported-on-linux"></a><span data-ttu-id="5f4d7-211">Linux에서 지원되는 Docker 버전</span><span class="sxs-lookup"><span data-stu-id="5f4d7-211">Docker versions supported on Linux</span></span>

- <span data-ttu-id="5f4d7-212">Docker 1.11 - 1.13</span><span class="sxs-lookup"><span data-stu-id="5f4d7-212">Docker 1.11 to 1.13</span></span>
- <span data-ttu-id="5f4d7-213">Docker CE 및 EE v17.06</span><span class="sxs-lookup"><span data-stu-id="5f4d7-213">Docker CE and EE v17.06</span></span>

### <a name="x64-linux-distributions-supported-as-container-hosts"></a><span data-ttu-id="5f4d7-214">컨테이너 호스트로 지원되는 x64 Linux 배포</span><span class="sxs-lookup"><span data-stu-id="5f4d7-214">x64 Linux distributions supported as container hosts</span></span>

- <span data-ttu-id="5f4d7-215">Ubuntu 14.04 LTS 및 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="5f4d7-215">Ubuntu 14.04 LTS and 16.04 LTS</span></span>
- <span data-ttu-id="5f4d7-216">CoreOS(stable)</span><span class="sxs-lookup"><span data-stu-id="5f4d7-216">CoreOS(stable)</span></span>
- <span data-ttu-id="5f4d7-217">Amazon Linux 2016.09.0</span><span class="sxs-lookup"><span data-stu-id="5f4d7-217">Amazon Linux 2016.09.0</span></span>
- <span data-ttu-id="5f4d7-218">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="5f4d7-218">openSUSE 13.2</span></span>
- <span data-ttu-id="5f4d7-219">openSUSE LEAP 42.2</span><span class="sxs-lookup"><span data-stu-id="5f4d7-219">openSUSE LEAP 42.2</span></span>
- <span data-ttu-id="5f4d7-220">CentOS 7.2 및 7.3</span><span class="sxs-lookup"><span data-stu-id="5f4d7-220">CentOS 7.2 and 7.3</span></span>
- <span data-ttu-id="5f4d7-221">SLES 12</span><span class="sxs-lookup"><span data-stu-id="5f4d7-221">SLES 12</span></span>
- <span data-ttu-id="5f4d7-222">RHEL 7.2 및 7.3</span><span class="sxs-lookup"><span data-stu-id="5f4d7-222">RHEL 7.2 and 7.3</span></span>
- <span data-ttu-id="5f4d7-223">Red Hat OCP(OpenShift Container Platform) 3.4 및 3.5</span><span class="sxs-lookup"><span data-stu-id="5f4d7-223">Red Hat OpenShift Container Platform (OCP) 3.4 and 3.5</span></span>
- <span data-ttu-id="5f4d7-224">ACS Mesosphere DC/OS 1.7.3 - 1.8.8</span><span class="sxs-lookup"><span data-stu-id="5f4d7-224">ACS Mesosphere DC/OS 1.7.3 to 1.8.8</span></span>
- <span data-ttu-id="5f4d7-225">ACS Kubernetes 1.4.5 - 1.6</span><span class="sxs-lookup"><span data-stu-id="5f4d7-225">ACS Kubernetes 1.4.5 to 1.6</span></span>
- <span data-ttu-id="5f4d7-226">ACS Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="5f4d7-226">ACS Docker Swarm</span></span>

### <a name="supported-windows-operating-system"></a><span data-ttu-id="5f4d7-227">지원되는 Windows 운영 체제</span><span class="sxs-lookup"><span data-stu-id="5f4d7-227">Supported Windows operating system</span></span>

- <span data-ttu-id="5f4d7-228">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="5f4d7-228">Windows Server 2016</span></span>
- <span data-ttu-id="5f4d7-229">Windows 10 1주년 버전(Professional 또는 Enterprise)</span><span class="sxs-lookup"><span data-stu-id="5f4d7-229">Windows 10 Anniversary Edition (Professional or Enterprise)</span></span>

### <a name="docker-versions-supported-on-windows"></a><span data-ttu-id="5f4d7-230">Windows에서 지원되는 Docker 버전</span><span class="sxs-lookup"><span data-stu-id="5f4d7-230">Docker versions supported on Windows</span></span>

- <span data-ttu-id="5f4d7-231">Docker 1.12 - 1.13</span><span class="sxs-lookup"><span data-stu-id="5f4d7-231">Docker 1.12 and 1.13</span></span>
- <span data-ttu-id="5f4d7-232">Docker 17.03.0 이상</span><span class="sxs-lookup"><span data-stu-id="5f4d7-232">Docker 17.03.0 and later</span></span>

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="5f4d7-233">솔루션 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="5f4d7-233">Installing and configuring the solution</span></span>
<span data-ttu-id="5f4d7-234">다음 정보를 사용하여 솔루션을 설치하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-234">Use the following information to install and configure the solution.</span></span>

1. <span data-ttu-id="5f4d7-235">[Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview)에서 또는 [솔루션 갤러리에서 Log Analytics 솔루션 추가](log-analytics-add-solutions.md)에서 설명하는 프로세스를 사용하여 OMS 작업 영역에 컨테이너 모니터링 솔루션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-235">Add the Container Monitoring solution to your OMS workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>

2. <span data-ttu-id="5f4d7-236">OMS 에이전트를 사용하여 Docker를 설치 및 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-236">Install and use Docker with an OMS agent.</span></span>  <span data-ttu-id="5f4d7-237">운영 체제에 따라 다음 방법 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-237">Based on your operating system, you can choose from the following methods:</span></span>

  * <span data-ttu-id="5f4d7-238">지원되는 Linux 운영 체제에서 Docker를 설치 및 실행한 다음 [Linux용 OMS 에이전트](log-analytics-agent-linux.md)를 설치 및 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-238">On supported Linux operating systems, install and run Docker and then install and configure the [OMS Agent for Linux](log-analytics-agent-linux.md).</span></span>  
  * <span data-ttu-id="5f4d7-239">CoreOS에서는 Linux 용 OMS 에이전트를 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-239">On CoreOS, you cannot run the OMS Agent for Linux.</span></span> <span data-ttu-id="5f4d7-240">대신 컨테이너화된 Linux 용 OMS 에이전트 버전을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-240">Instead, you run a containerized version of the OMS Agent for Linux.</span></span> <span data-ttu-id="5f4d7-241">Azure Government 클라우드에서 컨테이너를 사용하는 경우 [CoreOS를 포함한 Linux 컨테이너 호스트](#for-all-linux-container-hosts-including-coreos) 또는 [CoreOS을 포함한 Azure Government Linux 컨테이너 호스트](#for-all-azure-government-linux-container-hosts-including-coreos)를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-241">Review [Linux container hosts including CoreOS](#for-all-linux-container-hosts-including-coreos) or [Azure Government Linux container hosts including CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) if you are working with containers in Azure Government Cloud.</span></span>
  * <span data-ttu-id="5f4d7-242">Windows Server 2016 및 Windows 10에서 Docker 엔진 및 클라이언트를 설치한 후 에이전트를 연결하여 정보를 수집하고 Log Analytics에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-242">On Windows Server 2016 and Windows 10, install the Docker Engine and client then connect an agent to gather information and send it to Log Analytics.</span></span>  

### <a name="container-services"></a><span data-ttu-id="5f4d7-243">Container Service</span><span class="sxs-lookup"><span data-stu-id="5f4d7-243">Container services</span></span>

- <span data-ttu-id="5f4d7-244">Red Hat OpenShift 환경인 경우 [Red Hat OpenShift용 OMS 에이전트 구성](#configure-an-oms-agent-for-red-hat-openshift)을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-244">If you have a Red Hat OpenShift environment, review [Configure an OMS agent for Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span></span>
- <span data-ttu-id="5f4d7-245">Azure Container Service를 사용하는 Kubernetes 클러스터가 있는 경우 [Microsoft OMS(Operations Management Suite)를 사용하여 Azure Container Service 클러스터 모니터링](../container-service/kubernetes/container-service-kubernetes-oms.md)을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-245">If you have a Kubernetes cluster using the Azure Container Service, review [Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span></span>
- <span data-ttu-id="5f4d7-246">Azure Container Service DC/OS 클러스터가 있는 경우 [Operations Management Suite를 사용하여 Azure Container Service DC/OS 클러스터 모니터링](../container-service/dcos-swarm/container-service-monitoring-oms.md)에서 자세한 내용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-246">If you have an Azure Container Service DC/OS cluster, learn more at [Monitor an Azure Container Service DC/OS cluster with Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).</span></span>
- <span data-ttu-id="5f4d7-247">Docker Swarm 모드 환경에 있는 경우 [Docker Swarm용 OMS 에이전트 구성](#configure-an-oms-agent-for-docker-swarm)에서 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-247">If you have a Docker Swarm mode environment, learn more at [Configure an OMS agent for Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span></span>
- <span data-ttu-id="5f4d7-248">Service Fabric과 함께 컨테이너를 사용하는 경우 [Azure Service Fabric의 개요](../service-fabric/service-fabric-overview.md)에서 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-248">If you use containers with Service Fabric, learn more at [Overview of Azure Service Fabric](../service-fabric/service-fabric-overview.md).</span></span>
- <span data-ttu-id="5f4d7-249">[Windows에서 Docker 엔진](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) 문서에서 Windows를 실행하는 컴퓨터에서 Docker 엔진을 설치하고 구성하는 방법에 대한 추가 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-249">Review the [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) article for additional information about how to install and configure your Docker Engines on computers running Windows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5f4d7-250">Docker는 컨테이너 호스트에 [OMS Agent for Linux](log-analytics-agent-linux.md)를 설치하기 **전에** 실행해야 합니다. </span><span class="sxs-lookup"><span data-stu-id="5f4d7-250">Docker must be running **before** you install the [OMS Agent for Linux](log-analytics-agent-linux.md) on your container hosts.</span></span> <span data-ttu-id="5f4d7-251">Docker 설치에 앞서 에이전트를 설치한 경우 Linux용 OMS 에이전트를 다시 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-251">If you've already installed the agent before installing Docker, you need to reinstall the OMS Agent for Linux.</span></span> <span data-ttu-id="5f4d7-252">Docker에 대한 자세한 내용은 [Docker 웹 사이트](https://www.docker.com)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-252">For more information about Docker, see the [Docker website](https://www.docker.com).</span></span>


## <a name="linux-container-hosts"></a><span data-ttu-id="5f4d7-253">Linux 컨테이너 호스트</span><span class="sxs-lookup"><span data-stu-id="5f4d7-253">Linux container hosts</span></span>

<span data-ttu-id="5f4d7-254">Docker를 설치한 후 컨테이너 호스트에 다음 설정을 사용하여 Docker에 사용할 에이전트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-254">After you've installed Docker, use the following settings for your container host to configure the agent for use with Docker.</span></span> <span data-ttu-id="5f4d7-255">Azure Portal에서 찾을 수 있는 OMS 작업 영역 ID 및 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-255">First you need your OMS workspace ID and key, which you can find in the Azure portal.</span></span> <span data-ttu-id="5f4d7-256">작업 영역에서 **빠른 시작** > **컴퓨터**를 클릭하여 **작업 영역 ID** 및 **기본 키**를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-256">In your workspace, click **Quick Start** > **Computers** to view your **Workspace ID** and **Primary Key**.</span></span>  <span data-ttu-id="5f4d7-257">두 항목을 복사하여 선호하는 편집기에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-257">Copy and paste both into your favorite editor.</span></span>

### <a name="for-all-linux-container-hosts-except-coreos"></a><span data-ttu-id="5f4d7-258">CoreOS를 제외한 모든 Linux 컨테이너 호스트의 경우</span><span class="sxs-lookup"><span data-stu-id="5f4d7-258">For all Linux container hosts except CoreOS</span></span>

- <span data-ttu-id="5f4d7-259">Linux용 OMS 에이전트를 설치하는 방법에 대한 자세한 내용과 해당 단계는 [OMS(Operations Management Suite)에 Linux 컴퓨터 연결](log-analytics-agent-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-259">For more information and steps on how to install the OMS Agent for Linux, see [Connect your Linux Computers to Operations Management Suite (OMS)](log-analytics-agent-linux.md).</span></span>

### <a name="for-all-linux-container-hosts-including-coreos"></a><span data-ttu-id="5f4d7-260">CoreOS를 포함한 모든 Linux 컨테이너 호스트의 경우</span><span class="sxs-lookup"><span data-stu-id="5f4d7-260">For all Linux container hosts including CoreOS</span></span>

<span data-ttu-id="5f4d7-261">모니터링하려는 OMS 컨테이너를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-261">Start the OMS container that you want to monitor.</span></span> <span data-ttu-id="5f4d7-262">다음 예제를 수정하여 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-262">Modify and use the following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -e WSID="your workspace id" -e KEY="your key" -h=`hostname` -p 127.0.0.1:25225:25225 --name="omsagent" --restart=always microsoft/oms
```

### <a name="for-all-azure-government-linux-container-hosts-including-coreos"></a><span data-ttu-id="5f4d7-263">CoreOS를 포함한 모든 Azure Government Linux 컨테이너 호스트의 경우</span><span class="sxs-lookup"><span data-stu-id="5f4d7-263">For all Azure Government Linux container hosts including CoreOS</span></span>

<span data-ttu-id="5f4d7-264">모니터링하려는 OMS 컨테이너를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-264">Start the OMS container that you want to monitor.</span></span> <span data-ttu-id="5f4d7-265">다음 예제를 수정하여 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-265">Modify and use the following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/log:/var/log -e WSID="your workspace id" -e KEY="your key" -e DOMAIN="opinsights.azure.us" -p 127.0.0.1:25225:25225 -p 127.0.0.1:25224:25224/udp --name="omsagent" -h=`hostname` --restart=always microsoft/oms
```

### <a name="switching-from-using-an-installed-linux-agent-to-one-in-a-container"></a><span data-ttu-id="5f4d7-266">설치된 Linux 에이전트에서 컨테이너의 다른 에이전트로 전환</span><span class="sxs-lookup"><span data-stu-id="5f4d7-266">Switching from using an installed Linux agent to one in a container</span></span>
<span data-ttu-id="5f4d7-267">이전에 직접 설치한 에이전트를 사용하였고 이제 실행 중인 에이전트를 사용하려는 경우 먼저 Linux용 OMS 에이전트를 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-267">If you previously used the directly-installed agent and want to instead use an agent running in a container, you must first remove the OMS Agent for Linux.</span></span> <span data-ttu-id="5f4d7-268">[Linux용 OMS 에이전트 제거](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux)를 참조하여 성공적으로 에이전트를 제거하는 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-268">See [Uninstalling the OMS Agent for Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) to understand how to successfully uninstall the agent.</span></span>  

### <a name="configure-an-oms-agent-for-docker-swarm"></a><span data-ttu-id="5f4d7-269">Docker Swarm용 OMS 에이전트 구성</span><span class="sxs-lookup"><span data-stu-id="5f4d7-269">Configure an OMS agent for Docker Swarm</span></span>

<span data-ttu-id="5f4d7-270">Docker Swarm에서 전역 서비스로 OMS 에이전트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-270">You can run the OMS Agent as a global service on Docker Swarm.</span></span> <span data-ttu-id="5f4d7-271">다음 정보를 사용하여 OMS 에이전트 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-271">Use the following information to create an OMS Agent service.</span></span> <span data-ttu-id="5f4d7-272">OMS 작업 영역 ID 및 기본 키를 삽입해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-272">You need to insert your OMS Workspace ID and Primary Key.</span></span>

- <span data-ttu-id="5f4d7-273">마스터 노드에서 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-273">Run the following on the master node.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock  -e WSID="<WORKSPACE ID>" -e KEY="<PRIMARY KEY>" -p 25225:25225 -p 25224:25224/udp  --restart-condition=on-failure microsoft/oms
    ```

### <a name="configure-an-oms-agent-for-red-hat-openshift"></a><span data-ttu-id="5f4d7-274">Red Hat OpenShift용 OMS 에이전트 구성</span><span class="sxs-lookup"><span data-stu-id="5f4d7-274">Configure an OMS Agent for Red Hat OpenShift</span></span>
<span data-ttu-id="5f4d7-275">컨테이너 모니터링 데이터 수집을 시작하기 위해 Red Hat OpenShift에 OMS 에이전트를 추가하는 방법에는 세 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-275">There are three ways to add the OMS Agent to Red Hat OpenShift to start collecting container monitoring data.</span></span>

* <span data-ttu-id="5f4d7-276">각 OpenShift 노드에서 직접 [Linux용 OMS 에이전트를 설치](log-analytics-agent-linux.md)</span><span class="sxs-lookup"><span data-stu-id="5f4d7-276">[Install the OMS Agent for Linux](log-analytics-agent-linux.md) directly on each OpenShift node</span></span>  
* <span data-ttu-id="5f4d7-277">Azure에 있는 각 OpenShift 노드에서 [Log Analytics VM 확장을 사용하도록 설정](log-analytics-azure-vm-extension.md)</span><span class="sxs-lookup"><span data-stu-id="5f4d7-277">[Enable Log Analytics VM Extension](log-analytics-azure-vm-extension.md) on each OpenShift node residing in Azure</span></span>  
* <span data-ttu-id="5f4d7-278">OpenShift 디먼 집합으로 OMS 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="5f4d7-278">Install the OMS Agent as a OpenShift daemon-set</span></span>  

<span data-ttu-id="5f4d7-279">이 섹션에서는 OpenShift 디먼 집합으로 OMS 에이전트를 설치하는 데 필요한 단계를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-279">In this section we cover the steps required to install the OMS Agent as an OpenShift daemon-set.</span></span>  

1. <span data-ttu-id="5f4d7-280">OpenShift 마스터 노드에 로그온하고, GitHub에서 마스터 노드로 yaml 파일 [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml)을 복사하고, OMS 작업 영역 ID와 기본 키로 값을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-280">Sign on to the OpenShift master node and copy the yaml file [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) from GitHub to your master node and modify the value with your OMS Workspace ID and with your Primary Key.</span></span>
2. <span data-ttu-id="5f4d7-281">다음 명령을 실행하여 OMS에 대한 프로젝트를 만들고 사용자 계정을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-281">Run the following commands to create a project for OMS and set the user account.</span></span>

    ```
    oadm new-project omslogging --node-selector='zone=default'
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="5f4d7-282">디먼 집합을 배포하려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-282">To deploy the daemon-set, run the following:</span></span>

    `oc create -f ocp-omsagent.yaml`

5. <span data-ttu-id="5f4d7-283">올바르게 구성되어 있고 작동하는지 확인하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-283">To verify it is configured and working correctly, type the following:</span></span>

    `oc describe daemonset omsagent`  

    <span data-ttu-id="5f4d7-284">출력은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-284">and the output should resemble:</span></span>

    ```
    [ocpadmin@khm-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

<span data-ttu-id="5f4d7-285">OMS 에이전트 디먼 집합 yaml 파일을 사용하는 경우 OMS 작업 영역 ID와 기본 키를 보호하기 위해 비밀을 사용하려는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-285">If you want to use secrets to secure your OMS Workspace ID and Primary Key when using the OMS Agent daemon-set yaml file, perform the following steps.</span></span>

1. <span data-ttu-id="5f4d7-286">OpenShift 마스터 노드에 로그온하고 GitHub에서 yaml 파일 [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) 및 비밀 생성 스크립트 [ocp-secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh)를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-286">Sign on to the OpenShift master node and copy the yaml file [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) and secret generating script [ocp-secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) from GitHub.</span></span>  <span data-ttu-id="5f4d7-287">이 스크립트는 비밀 정보를 보호하기 위해 OMS 작업 영역 ID와 기본 키에 대한 비밀 yaml 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-287">This script will generate the secrets yaml file for OMS Workspace ID and Primary Key to secure your secrete information.</span></span>  
2. <span data-ttu-id="5f4d7-288">다음 명령을 실행하여 OMS에 대한 프로젝트를 만들고 사용자 계정을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-288">Run the following commands to create a project for OMS and set the user account.</span></span> <span data-ttu-id="5f4d7-289">비밀 생성 스크립트는 OMS 작업 영역 ID<WSID> 및 기본 키<KEY>를 요청하고, 완료되면 ocp-secret.yaml 파일이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-289">The secret generating script asks for your OMS Workspace ID <WSID> and Primary Key <KEY> and upon completion, it creates the ocp-secret.yaml file.</span></span>  

    ```
    oadm new-project omslogging --node-selector='zone=default'  
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="5f4d7-290">다음을 실행하여 비밀 파일을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-290">Deploy the secret file by running the following:</span></span>

    `oc create -f ocp-secret.yaml`

5. <span data-ttu-id="5f4d7-291">다음을 실행하여 배포를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-291">Verify deployment by running the following:</span></span>

    `oc describe secret omsagent-secret`  

    <span data-ttu-id="5f4d7-292">출력은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-292">and the  output should resemble:</span></span>  

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

6. <span data-ttu-id="5f4d7-293">다음을 실행하여 OMS 에이전트 디먼 집합 yaml 파일을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-293">Deploy the OMS Agent daemon-set yaml file by running the following:</span></span>

    `oc create -f ocp-ds-omsagent.yaml`  

7. <span data-ttu-id="5f4d7-294">다음을 실행하여 배포를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-294">Verify deployment by running the following:</span></span>

    `oc describe ds oms`

    <span data-ttu-id="5f4d7-295">출력은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-295">and the output should resemble:</span></span>

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe secret omsagent-secret  
    Name:           omsagent-secret  
    Namespace:      omslogging  
    Labels:         <none>  
    Annotations:    <none>  

    Type:   Opaque  

     Data  
     ====  
     KEY:    89 bytes  
     WSID:   37 bytes  
    ```

### <a name="secure-your-secret-information-for-docker-swarm-and-kubernetes"></a><span data-ttu-id="5f4d7-296">Docker Swarm 및 Kubernetes에 대한 비밀 정보를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-296">Secure your secret information for Docker Swarm and Kubernetes</span></span>

<span data-ttu-id="5f4d7-297">Docker Swarm 및 Kubernetes 컨테이너 서비스에 대한 비밀 OMS 작업 영역 ID 및 기본 키를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-297">You can secure your secret OMS Workspace ID and Primary Keys for Docker Swarm and Kubernetes container services.</span></span>

#### <a name="secure-secrets-for-docker-swarm"></a><span data-ttu-id="5f4d7-298">Docker Swarm에 대한 비밀 보호</span><span class="sxs-lookup"><span data-stu-id="5f4d7-298">Secure secrets for Docker Swarm</span></span>

<span data-ttu-id="5f4d7-299">Docker Swarm의 경우 작업 영역 ID 및 기본 키에 대한 비밀이 생성되면 OMSagent에 대한 Docker 서비스 만들기를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-299">For Docker Swarm, once the secret for Workspace ID and Primary Key is created, you can run the create the Docker service for OMSagent.</span></span> <span data-ttu-id="5f4d7-300">다음 정보를 사용하여 비밀 정보를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-300">Use the following information to create your secret information.</span></span>

1. <span data-ttu-id="5f4d7-301">마스터 노드에서 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-301">Run the following on the master node.</span></span>

    ```
    echo "WSID" | docker secret create WSID -
    echo "KEY" | docker secret create KEY -
    ```

2. <span data-ttu-id="5f4d7-302">비밀이 제대로 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-302">Verify that secrets were created properly.</span></span>

    ```
    keiko@swarmm-master-13957614-0:/run# sudo docker secret ls
    ```

    ```
    ID                          NAME                CREATED             UPDATED
    j2fj153zxy91j8zbcitnjxjiv   WSID                43 minutes ago      43 minutes ago
    l9rh3n987g9c45zffuxdxetd9   KEY                 38 minutes ago      38 minutes ago
    ```

3. <span data-ttu-id="5f4d7-303">다음 명령을 실행하여 비밀을 컨테이너화된 OMS 에이전트에 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-303">Run the following command to mount the secrets to the containerized OMS Agent.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock --secret source=WSID,target=WSID --secret source=KEY,target=KEY  -p 25225:25225 -p 25224:25224/udp --restart-condition=on-failure microsoft/oms
    ```

#### <a name="secure-secrets-for-kubernetes-with-yaml-files"></a><span data-ttu-id="5f4d7-304">yaml 파일로 Kubernetes에 대한 비밀 보호</span><span class="sxs-lookup"><span data-stu-id="5f4d7-304">Secure secrets for Kubernetes with yaml files</span></span>

<span data-ttu-id="5f4d7-305">Kubernetes의 경우 스크립트를 사용하여 작업 영역 ID 및 기본 키에 대한 비밀 yaml 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-305">For Kubernetes, you use a script to generate the secrets yaml file for your Workspace ID and Primary Key.</span></span> <span data-ttu-id="5f4d7-306">[OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) 페이지에는 비밀 정보를 포함 또는 포함하지 않고 사용할 수 있는 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-306">At the [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) page, there are files that you can use with or without your secret information.</span></span>

- <span data-ttu-id="5f4d7-307">비밀 정보(omsagent.yaml)가 없는 기본 OMS 에이전트 DaemonSet</span><span class="sxs-lookup"><span data-stu-id="5f4d7-307">The Default OMS Agent DaemonSet does not have secret information (omsagent.yaml)</span></span>
- <span data-ttu-id="5f4d7-308">비밀 yaml(omsagentsecret.yaml) 파일을 생성하는 비밀 생성 스크립트를 통해 비밀 정보(omsagent-ds-secrets.yaml)를 사용하는 OMS 에이전트 DaemonSet yaml 파일.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-308">The OMS Agent DaemonSet yaml file uses secret information (omsagent-ds-secrets.yaml) with secret generation scripts to generate the secrets yaml (omsagentsecret.yaml) file.</span></span>

<span data-ttu-id="5f4d7-309">비밀을 포함 또는 포함하지 않고 omsagent DaemonSet를 만들도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-309">You can choose to create omsagent DaemonSets with or without secrets.</span></span>

##### <a name="default-omsagent-daemonset-yaml-file-without-secrets"></a><span data-ttu-id="5f4d7-310">비밀이 없는 기본 OMSagent DaemonSet yaml 파일</span><span class="sxs-lookup"><span data-stu-id="5f4d7-310">Default OMSagent DaemonSet yaml file without secrets</span></span>

- <span data-ttu-id="5f4d7-311">기본 OMS Agent DaemonSet yaml 파일에서 `<WSID>` 및 `<KEY>`를 사용자의 WSID 및 KEY로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-311">For the default OMS Agent DaemonSet yaml file, replace the `<WSID>` and `<KEY>` to your WSID and KEY.</span></span> <span data-ttu-id="5f4d7-312">파일을 마스터 노드에 복사하고 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-312">Copy the file to your master node and run the following:</span></span>

    ```
    sudo kubectl create -f omsagent.yaml
    ```

##### <a name="default-omsagent-daemonset-yaml-file-with-secrets"></a><span data-ttu-id="5f4d7-313">비밀이 있는 기본 OMSagent DaemonSet yaml 파일</span><span class="sxs-lookup"><span data-stu-id="5f4d7-313">Default OMSagent DaemonSet yaml file with secrets</span></span>

1. <span data-ttu-id="5f4d7-314">비밀 정보를 사용하여 OMS 에이전트 DaemonSet을 사용하려면 먼저 비밀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-314">To use OMS Agent DaemonSet using secret information, create the secrets first.</span></span>
    1. <span data-ttu-id="5f4d7-315">스크립트 및 비밀 템플릿 파일을 복사하고 이들이 같은 디렉터리에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-315">Copy the script and secret template file and make sure they are on the same directory.</span></span>
        - <span data-ttu-id="5f4d7-316">비밀 생성 스크립트 - secret-gen.sh</span><span class="sxs-lookup"><span data-stu-id="5f4d7-316">Secret generating script - secret-gen.sh</span></span>
        - <span data-ttu-id="5f4d7-317">비밀 템플릿 - secret-template.yaml</span><span class="sxs-lookup"><span data-stu-id="5f4d7-317">secret template - secret-template.yaml</span></span>
    2. <span data-ttu-id="5f4d7-318">다음 예제와 같이 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-318">Run the script, like the following example.</span></span> <span data-ttu-id="5f4d7-319">스크립트에서 OMS 작업 영역 ID 및 기본 키를 요청하고 사용자가 이를 입력하면 스크립트에서 비밀 yaml 파일을 생성하며 사용자가 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-319">The script asks for the OMS Workspace ID and Primary Key and after you enter them, the script creates a secret yaml file so you can run it.</span></span>   

        ```
        #> sudo bash ./secret-gen.sh
        ```

    3. <span data-ttu-id="5f4d7-320">다음을 실행하여 비밀 Pod를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-320">Create the secrets pod by running the following:</span></span>
        ```
        sudo kubectl create -f omsagentsecret.yaml
        ```

    4. <span data-ttu-id="5f4d7-321">확인하려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-321">To verify, run the following:</span></span>

        ```
        keiko@ubuntu16-13db:~# sudo kubectl get secrets
        ```

        <span data-ttu-id="5f4d7-322">출력은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-322">Output should resemble:</span></span>

        ```
        NAME                  TYPE                                  DATA      AGE
        default-token-gvl91   kubernetes.io/service-account-token   3         50d
        omsagent-secret       Opaque                                2         1d
        ```

        ```
        keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
        ```

        <span data-ttu-id="5f4d7-323">출력은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-323">Output should resemble:</span></span>

        ```
        Name:           omsagent-secret
        Namespace:      default
        Labels:         <none>
        Annotations:    <none>

        Type:   Opaque

        Data
        ====
        WSID:   36 bytes
        KEY:    88 bytes
        ```

    5. <span data-ttu-id="5f4d7-324">``` sudo kubectl create -f omsagent-ds-secrets.yaml ```을 실행하여 omsagent daemon-set 만들기</span><span class="sxs-lookup"><span data-stu-id="5f4d7-324">Create your omsagent daemon-set by running ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

2. <span data-ttu-id="5f4d7-325">OMS 에이전트 DaemonSet가 다음과 같이 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-325">Verify that the OMS Agent DaemonSet is running, similar to the following:</span></span>

    ```
    keiko@ubuntu16-13db:~# sudo kubectl get ds omsagent
    ```

    ```
    NAME       DESIRED   CURRENT   NODE-SELECTOR   AGE
    omsagent   3         3         <none>          1h
    ```


<span data-ttu-id="5f4d7-326">Kubernetes의 경우 스크립트를 사용하여 작업 영역 ID 및 기본 키에 대한 비밀 yaml 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-326">For Kubernetes, use a script to generate the secrets yaml file for Workspace ID and Primary Key.</span></span> <span data-ttu-id="5f4d7-327">[omsagent yaml 파일](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml)에 다음 예제 정보를 사용하여 비밀 정보를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-327">Use the following example information with the [omsagent yaml file](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) to secure your secret information.</span></span>

```
keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
Name:           omsagent-secret
Namespace:      default
Labels:         <none>
Annotations:    <none>

Type:   Opaque

Data
====
WSID:   36 bytes
KEY:    88 bytes
```

## <a name="windows-container-hosts"></a><span data-ttu-id="5f4d7-328">Windows 컨테이너 호스트</span><span class="sxs-lookup"><span data-stu-id="5f4d7-328">Windows container hosts</span></span>

### <a name="preparation-before-installing-windows-agents"></a><span data-ttu-id="5f4d7-329">Windows 에이전트 설치 전 준비</span><span class="sxs-lookup"><span data-stu-id="5f4d7-329">Preparation before installing Windows agents</span></span>

<span data-ttu-id="5f4d7-330">Windows를 실행하는 컴퓨터에 에이전트를 설치하기 전에 Docker 서비스를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-330">Before you install agents on computers running Windows, you need to configure the Docker service.</span></span> <span data-ttu-id="5f4d7-331">구성을 통해 Windows 에이전트 또는 Log Analytics 가상 컴퓨터 확장에서 Docker TCP 소켓을 사용하도록 하여 에이전트가 Docker 데몬에 원격으로 액세스하고 모니터링할 데이터를 캡처하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-331">The configuration allows the Windows agent or the Log Analytics virtual machine extension to use the Docker TCP socket so that the agents can access the Docker daemon remotely and to capture data for monitoring.</span></span>

#### <a name="to-start-docker-and-verify-its-configuration"></a><span data-ttu-id="5f4d7-332">Docker를 시작하고 구성을 확인하려면</span><span class="sxs-lookup"><span data-stu-id="5f4d7-332">To start Docker and verify its configuration</span></span>

<span data-ttu-id="5f4d7-333">Windows 서버에 대한 TCP 명명된 파이프를 설정하는 데 필요한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-333">There are steps needed to set up TCP named pipe for Windows Server:</span></span>

1. <span data-ttu-id="5f4d7-334">Windows PowerShell에서 TCP 파이프 및 명명된 파이프를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-334">In Windows PowerShell, enable TCP pipe and named pipe.</span></span>

    ```
    Stop-Service docker
    dockerd --unregister-service
    dockerd --register-service -H npipe:// -H 0.0.0.0:2375  
    Start-Service docker
    ```

2. <span data-ttu-id="5f4d7-335">TCP 파이프 및 명명된 파이프에 대한 구성 파일로 Docker를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-335">Configure Docker with the configuration file for TCP pipe and named pipe.</span></span> <span data-ttu-id="5f4d7-336">구성 파일은 C:\ProgramData\docker\config\daemon.json에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-336">The configuration file is located at C:\ProgramData\docker\config\daemon.json.</span></span>

    <span data-ttu-id="5f4d7-337">daemon.json 파일에서 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-337">In the daemon.json file, you will need the following:</span></span>

    ```
    {
    "hosts": ["tcp://0.0.0.0:2375", "npipe://"]
    }
    ```

<span data-ttu-id="5f4d7-338">Windows 컨테이너에서 사용하는 Docker 데몬 구성에 대한 자세한 내용은 [Windows에서 Docker 엔진](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-338">For more information about the Docker daemon configuration used with Windows Containers, see [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span></span>


### <a name="install-windows-agents"></a><span data-ttu-id="5f4d7-339">Windows 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="5f4d7-339">Install Windows agents</span></span>

<span data-ttu-id="5f4d7-340">Windows 및 Hyper-V 컨테이너 모니터링을 사용하도록 설정하려면 컨테이너 호스트인 Windows 컴퓨터에 MMA(Microsoft Monitoring Agent)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-340">To enable Windows and Hyper-V container monitoring, install the Microsoft Monitoring Agent (MMA) on Windows computers that are container hosts.</span></span> <span data-ttu-id="5f4d7-341">온-프레미스 환경에서 Windows를 실행하는 컴퓨터는 [Log Analytics에 Windows 컴퓨터 연결](log-analytics-windows-agents.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-341">For computers running Windows in your on-premises environment, see [Connect Windows computers to Log Analytics](log-analytics-windows-agents.md).</span></span> <span data-ttu-id="5f4d7-342">Azure에서 실행되는 가상 컴퓨터의 경우 [가상 컴퓨터 확장](log-analytics-azure-vm-extension.md)을 사용하여 Log Analytics에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-342">For virtual machines running in Azure, connect them to Log Analytics using the [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="5f4d7-343">Service Fabric에서 실행 중인 Windows 컨테이너를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-343">You can monitor Windows containers running on Service Fabric.</span></span> <span data-ttu-id="5f4d7-344">그러나 [Azure에서 실행 중인 가상 컴퓨터](log-analytics-azure-vm-extension.md) 및 [온-프레미스 환경에서 Windows를 실행하는 컴퓨터](log-analytics-windows-agents.md)만 현재 Service Fabric에 대해 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-344">However, only [virtual machines running in Azure](log-analytics-azure-vm-extension.md) and [computers running Windows in your on-premises environment](log-analytics-windows-agents.md) are currently supported for Service Fabric.</span></span>

<span data-ttu-id="5f4d7-345">컨테이너 모니터링 솔루션이 Windows에 대해 올바르게 설정되어 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-345">You can verify that the Container Monitoring solution is set correctly for Windows.</span></span> <span data-ttu-id="5f4d7-346">관리 팩이 제대로 다운로드되었는지 확인하려면 *ContainerManagement.xxx*를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-346">To check whether the management pack was download properly, look for *ContainerManagement.xxx*.</span></span> <span data-ttu-id="5f4d7-347">파일은 C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs 폴더에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-347">The files should be in the C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs folder.</span></span>


## <a name="solution-components"></a><span data-ttu-id="5f4d7-348">솔루션 구성 요소</span><span class="sxs-lookup"><span data-stu-id="5f4d7-348">Solution components</span></span>

<span data-ttu-id="5f4d7-349">Windows 에이전트를 사용하는 경우 이 솔루션을 추가할 때 에이전트와 함께 다음 관리 팩이 각 컴퓨터에 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-349">If you are using Windows agents, then the following management pack is installed on each computer with an agent when you add this solution.</span></span> <span data-ttu-id="5f4d7-350">관리 팩에는 구성 또는 유지 관리가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-350">No configuration or maintenance is required for the management pack.</span></span>

- <span data-ttu-id="5f4d7-351">C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs에 설치된 *ContainerManagement.xxx*</span><span class="sxs-lookup"><span data-stu-id="5f4d7-351">*ContainerManagement.xxx* installed in C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs</span></span>

## <a name="container-data-collection-details"></a><span data-ttu-id="5f4d7-352">컨테이너 데이터 컬렉션 세부 정보</span><span class="sxs-lookup"><span data-stu-id="5f4d7-352">Container data collection details</span></span>
<span data-ttu-id="5f4d7-353">컨테이너 모니터링 솔루션은 사용자가 활성화한 에이전트를 사용하여 컨테이너 호스트 및 컨테이너로부터 다양한 성능 메트릭과 로그 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-353">The Container Monitoring solution collects various performance metrics and log data from container hosts and containers using agents that you enable.</span></span>

<span data-ttu-id="5f4d7-354">데이터는 다음 에이전트 형식으로 3분마다 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-354">Data is collected every three minutes by the following agent types.</span></span>

- [<span data-ttu-id="5f4d7-355">OMS Agent for Linux</span><span class="sxs-lookup"><span data-stu-id="5f4d7-355">OMS Agent for Linux</span></span>](log-analytics-linux-agents.md)
- [<span data-ttu-id="5f4d7-356">Windows 에이전트</span><span class="sxs-lookup"><span data-stu-id="5f4d7-356">Windows agent</span></span>](log-analytics-windows-agents.md)
- [<span data-ttu-id="5f4d7-357">Log Analytics VM 확장</span><span class="sxs-lookup"><span data-stu-id="5f4d7-357">Log Analytics VM extension</span></span>](log-analytics-azure-vm-extension.md)


### <a name="container-records"></a><span data-ttu-id="5f4d7-358">컨테이너 레코드</span><span class="sxs-lookup"><span data-stu-id="5f4d7-358">Container records</span></span>

<span data-ttu-id="5f4d7-359">다음 테이블은 컨테이너 모니터링 솔루션에 의해 수집된 레코드 및 로그 검색 결과에 표시된 데이터 형식의 예를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-359">The following table shows examples of records collected by the Container Monitoring solution and the data types that appear in log search results.</span></span>

| <span data-ttu-id="5f4d7-360">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="5f4d7-360">Data type</span></span> | <span data-ttu-id="5f4d7-361">로그 검색의 데이터 유형</span><span class="sxs-lookup"><span data-stu-id="5f4d7-361">Data type in Log Search</span></span> | <span data-ttu-id="5f4d7-362">필드</span><span class="sxs-lookup"><span data-stu-id="5f4d7-362">Fields</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5f4d7-363">호스트 및 컨테이너에 대한 성능</span><span class="sxs-lookup"><span data-stu-id="5f4d7-363">Performance for hosts and containers</span></span> | `Type=Perf` | <span data-ttu-id="5f4d7-364">컴퓨터, ObjectName, CounterName &#40;%프로세서 시간, 디스크 읽기 MB, 디스크 쓰기 MB, 메모리 사용 MB, 네트워크 수신 바이트, 네트워크 송신 바이트, 프로세서 사용 초, 네트워크&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="5f4d7-364">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span></span> |
| <span data-ttu-id="5f4d7-365">컨테이너 인벤토리</span><span class="sxs-lookup"><span data-stu-id="5f4d7-365">Container inventory</span></span> | `Type=ContainerInventory` | <span data-ttu-id="5f4d7-366">TimeGenerated, 컴퓨터, 컨테이너 이름, ContainerHostname, 이미지, ImageTag, ContainerState, ExitCode, EnvironmentVar, 명령, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span><span class="sxs-lookup"><span data-stu-id="5f4d7-366">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span></span> |
| <span data-ttu-id="5f4d7-367">컨테이너 이미지 인벤토리</span><span class="sxs-lookup"><span data-stu-id="5f4d7-367">Container image inventory</span></span> | `Type=ContainerImageInventory` | <span data-ttu-id="5f4d7-368">TimeGenerated, 컴퓨터, 이미지, ImageTag, ImageSize, VirtualSize, 실행 중, 일시 중지됨, 중지됨, 실패, SourceSystem, ImageID, TotalContainer</span><span class="sxs-lookup"><span data-stu-id="5f4d7-368">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span></span> |
| <span data-ttu-id="5f4d7-369">컨테이너 로그</span><span class="sxs-lookup"><span data-stu-id="5f4d7-369">Container log</span></span> | `Type=ContainerLog` | <span data-ttu-id="5f4d7-370">TimeGenerated, 컴퓨터, 이미지 ID, 컨테이너 이름, LogEntrySource, LogEntry, SourceSystem, ContainerID</span><span class="sxs-lookup"><span data-stu-id="5f4d7-370">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="5f4d7-371">컨테이너 서비스 로그</span><span class="sxs-lookup"><span data-stu-id="5f4d7-371">Container service log</span></span> | `Type=ContainerServiceLog`  | <span data-ttu-id="5f4d7-372">TimeGenerated, 컴퓨터, TimeOfCommand, 이미지, 명령, SourceSystem, ContainerID</span><span class="sxs-lookup"><span data-stu-id="5f4d7-372">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="5f4d7-373">컨테이너 노드 인벤토리</span><span class="sxs-lookup"><span data-stu-id="5f4d7-373">Container node inventory</span></span> | `Type=ContainerNodeInventory_CL`| <span data-ttu-id="5f4d7-374">TimeGenerated, 컴퓨터, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="5f4d7-374">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span></span>|
| <span data-ttu-id="5f4d7-375">Kubernetes 인벤토리</span><span class="sxs-lookup"><span data-stu-id="5f4d7-375">Kubernetes inventory</span></span> | `Type=KubePodInventory_CL` | <span data-ttu-id="5f4d7-376">TimeGenerated, 컴퓨터, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="5f4d7-376">TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span></span> |
| <span data-ttu-id="5f4d7-377">컨테이너 프로세스</span><span class="sxs-lookup"><span data-stu-id="5f4d7-377">Container process</span></span> | `Type=ContainerProcess_CL` | <span data-ttu-id="5f4d7-378">TimeGenerated, 컴퓨터, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="5f4d7-378">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span></span> |
| <span data-ttu-id="5f4d7-379">kubernetes 이벤트</span><span class="sxs-lookup"><span data-stu-id="5f4d7-379">Kubernetes events</span></span> | `Type=KubeEvents_CL` | <span data-ttu-id="5f4d7-380">TimeGenerated, 컴퓨터, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, 메시지</span><span class="sxs-lookup"><span data-stu-id="5f4d7-380">TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message</span></span> |

<span data-ttu-id="5f4d7-381">*PodLabel* 데이터 형식에 추가된 레이블은 사용자 고유의 사용자 지정 레이블입니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-381">Labels appended to *PodLabel* data types are your own custom labels.</span></span> <span data-ttu-id="5f4d7-382">테이블에 표시된 추가된 PodLabel 레이블은 예입니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-382">The appended PodLabel labels shown in the table are examples.</span></span> <span data-ttu-id="5f4d7-383">따라서 `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s`는 사용자 환경의 데이터 집합에 따라 달라지며 일반적으로 `PodLabel_yourlabel_s`와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-383">So, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` will differ in your environment's data set and generically resemble `PodLabel_yourlabel_s`.</span></span>


## <a name="monitor-containers"></a><span data-ttu-id="5f4d7-384">모니터 컨테이너</span><span class="sxs-lookup"><span data-stu-id="5f4d7-384">Monitor containers</span></span>
<span data-ttu-id="5f4d7-385">OMS 포털에서 솔루션을 사용하도록 설정한 후에는 **컨테이너** 타일에 컨테이너 호스트와 호스트에서 실행 중인 컨테이너에 대한 요약 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-385">After you have the solution enabled in the OMS portal, the **Containers** tile shows summary information about your container hosts and the containers running in hosts.</span></span>

![컨테이너 타일](./media/log-analytics-containers/containers-title.png)

<span data-ttu-id="5f4d7-387">타일은 환경에 있는 컨테이너의 수와, 해당 컨테이너의 실패, 실행 중 또는 중지 여부를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-387">The tile shows an overview of how many containers you have in the environment and whether they're failed, running, or stopped.</span></span>

### <a name="using-the-containers-dashboard"></a><span data-ttu-id="5f4d7-388">컨테이너 대시보드 사용</span><span class="sxs-lookup"><span data-stu-id="5f4d7-388">Using the Containers dashboard</span></span>
<span data-ttu-id="5f4d7-389">**컨테이너** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-389">Click the **Containers** tile.</span></span> <span data-ttu-id="5f4d7-390">여기에서는 다음에 따라 구성된 보기를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-390">From there you'll see views organized by:</span></span>

- <span data-ttu-id="5f4d7-391">**컨테이너 이벤트** - 컨테이너 상태 및 실패한 컨테이너가 있는 컴퓨터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-391">**Container Events** - Shows container status and computers with failed containers.</span></span>
- <span data-ttu-id="5f4d7-392">**컨테이너 로그** - 시간에 따라 생성되는 컨테이너 로그 파일의 차트 및 로그 파일 수가 가장 높은 컴퓨터의 목록을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-392">**Container Logs** - Shows a chart of container log files generated over time and a list of computers with the highest number of log files.</span></span>
- <span data-ttu-id="5f4d7-393">**Kubernetes 이벤트** - 시간에 따라 생성되는 Kubernetes 이벤트의 차트 및 Pod가 이벤트를 생성하는 이유에 대한 목록을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-393">**Kubernetes Events** - Shows a chart of Kubernetes events generated over time and a list of the reasons why pods generated the events.</span></span> <span data-ttu-id="5f4d7-394">*이 데이터 집합은 Linux 환경에만 사용됩니다.*</span><span class="sxs-lookup"><span data-stu-id="5f4d7-394">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="5f4d7-395">**Kubernetes 네임스페이스 인벤토리** - 네임스페이스 및 Pod의 수를 표시하고 해당 계층을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-395">**Kubernetes Namespace Inventory** - Shows the number of namespaces and pods and shows their hierarchy.</span></span> <span data-ttu-id="5f4d7-396">*이 데이터 집합은 Linux 환경에만 사용됩니다.*</span><span class="sxs-lookup"><span data-stu-id="5f4d7-396">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="5f4d7-397">**컨테이너 노드 인벤토리** - 컨테이너 노드/호스트에서 사용되는 오케스트레이션 형식의 수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-397">**Container Node Inventory** - Shows the number of orchestration types used on container nodes/hosts.</span></span> <span data-ttu-id="5f4d7-398">컴퓨터 노드/호스트가 컨테이너의 수를 기준으로 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-398">The computer nodes/hosts are also listed by the number of containers.</span></span> <span data-ttu-id="5f4d7-399">*이 데이터 집합은 Linux 환경에만 사용됩니다.*</span><span class="sxs-lookup"><span data-stu-id="5f4d7-399">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="5f4d7-400">**컨테이너 이미지 인벤토리** - 사용된 총 컨테이너 이미지 수 및 이미지 형식의 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-400">**Container Images Inventory** - Shows the total number of container images used and number of image types.</span></span> <span data-ttu-id="5f4d7-401">이미지 수는 이미지 태그를 기준으로 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-401">The number of images are also listed by the image tag.</span></span>
- <span data-ttu-id="5f4d7-402">**컨테이너 상태** - 컨테이너를 실행 중인 총 컨테이너 노드/호스트 컴퓨터 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-402">**Containers Status** - Shows the total number of container nodes/host computers that have running containers.</span></span> <span data-ttu-id="5f4d7-403">컴퓨터는 실행 중인 호스트 수를 기준으로 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-403">Computers are also listed by the number of running hosts.</span></span>
- <span data-ttu-id="5f4d7-404">**컨테이너 프로세스** - 시간에 따른 실행 중인 컨테이너 프로세스의 꺾은선형 차트를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-404">**Container Process** - Shows a line chart of container processes running over time.</span></span> <span data-ttu-id="5f4d7-405">컨테이너는 컨테이너 내 실행 중인 명령/프로세스를 기준으로 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-405">Containers are also listed by running command/process within containers.</span></span> <span data-ttu-id="5f4d7-406">*이 데이터 집합은 Linux 환경에만 사용됩니다.*</span><span class="sxs-lookup"><span data-stu-id="5f4d7-406">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="5f4d7-407">**컨테이너 CPU 성능** - 컴퓨터 노드/호스트에 대한 시간에 따른 평균 CPU 사용률의 꺾은선형 차트를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-407">**Container CPU Performance** - Shows a line chart of the average CPU utilization over time for computer nodes/hosts.</span></span> <span data-ttu-id="5f4d7-408">또한 평균 CPU 사용률을 기준으로 컴퓨터 노드/호스트를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-408">Also lists the computer nodes/hosts based on average CPU utilization.</span></span>
- <span data-ttu-id="5f4d7-409">**컨테이너 메모리 성능** - 시간에 따른 메모리 사용량의 꺾은선형 차트를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-409">**Container Memory Performance** - Shows a line chart of memory usage over time.</span></span> <span data-ttu-id="5f4d7-410">또한 인스턴스 이름을 기준으로 컴퓨터 메모리 사용률을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-410">Also lists computer memory utilization based on instance name.</span></span>
- <span data-ttu-id="5f4d7-411">**컴퓨터 성능** - 시간에 따른 CPU 성능의 백분율, 시간에 따른 메모리 사용량의 백분율 및 시간에 따른 사용 가능한 디스크 공간의 메가바이트를 꺾은 선형 차트로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-411">**Computer Performance** - Shows line charts of the percent of CPU performance over time, percent of memory usage over time, and megabytes of free disk space over time.</span></span> <span data-ttu-id="5f4d7-412">차트에서 해당 줄 위로 마우스를 이동하면 자세한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-412">You can hover over any line in a chart to view more details.</span></span>


<span data-ttu-id="5f4d7-413">대시보드의 각 영역은 수집된 데이터에서 실행되는 검색을 시각적으로 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-413">Each area of the dashboard is a visual representation of a search that is run on collected data.</span></span>

![컨테이너 대시보드 ](./media/log-analytics-containers/containers-dash01.png)

![컨테이너 대시보드 ](./media/log-analytics-containers/containers-dash02.png)

<span data-ttu-id="5f4d7-416">**컨테이너 상태** 영역에서 아래 그림과 같이 위쪽 영역을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-416">In the **Container Status** area, click the top area, as shown below.</span></span>

![컨테이너 상태](./media/log-analytics-containers/containers-status.png)

<span data-ttu-id="5f4d7-418">로그 검색이 열리고 컨테이너 상태에 대한 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-418">Log Search opens, displaying information about the state of your containers.</span></span>

![컨테이너에 대한 로그 검색](./media/log-analytics-containers/containers-log-search.png)

<span data-ttu-id="5f4d7-420">여기에서 검색 쿼리를 편집 수정하여 관심 있는 특정 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-420">From here, you can edit the search query to modify it to find the specific information you're interested in.</span></span> <span data-ttu-id="5f4d7-421">로그 검색에 대한 자세한 내용은 [Log Analytics의 로그 검색](log-analytics-log-searches.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-421">For more information about Log Searches, see [Log searches in Log Analytics](log-analytics-log-searches.md).</span></span>

## <a name="troubleshoot-by-finding-a-failed-container"></a><span data-ttu-id="5f4d7-422">실패한 컨테이너를 검색하여 문제 해결</span><span class="sxs-lookup"><span data-stu-id="5f4d7-422">Troubleshoot by finding a failed container</span></span>

<span data-ttu-id="5f4d7-423">0이 아닌 종료 코드로 종료된 경우 Log Analytics는 이 컨테이너를 **Failed**로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-423">Log Analytics marks a container as **Failed** if it has exited with a non-zero exit code.</span></span> <span data-ttu-id="5f4d7-424">**실패한 컨테이너** 영역에서 환경의 오류 및 실패 개요를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-424">You can see an overview of the errors and failures in the environment in the **Failed Containers** area.</span></span>

### <a name="to-find-failed-containers"></a><span data-ttu-id="5f4d7-425">실패한 컨테이너 찾기</span><span class="sxs-lookup"><span data-stu-id="5f4d7-425">To find failed containers</span></span>
1. <span data-ttu-id="5f4d7-426">**컨테이너 상태** 영역을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-426">Click the **Container Status** area.</span></span>  
   <span data-ttu-id="5f4d7-427">![컨테이너 상태](./media/log-analytics-containers/containers-status.png)</span><span class="sxs-lookup"><span data-stu-id="5f4d7-427">![containers status](./media/log-analytics-containers/containers-status.png)</span></span>
2. <span data-ttu-id="5f4d7-428">로그 검색이 열리고 다음과 유사한 컨테이너 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-428">Log Search opens and displays the state of your containers, similar to the following.</span></span>  
   ![컨테이너 상태](./media/log-analytics-containers/containers-log-search.png)
3. <span data-ttu-id="5f4d7-430">추가 정보를 보려면 실패한 컨테이너의 집계 값을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-430">Next, click the aggregated value of failed containers to view additional information.</span></span> <span data-ttu-id="5f4d7-431">**자세히 표시**를 확장하여 이미지 ID를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-431">Expand **show more** to view the image ID.</span></span>  
   <span data-ttu-id="5f4d7-432">![실패한 컨테이너](./media/log-analytics-containers/containers-state-failed.png)</span><span class="sxs-lookup"><span data-stu-id="5f4d7-432">![failed containers](./media/log-analytics-containers/containers-state-failed.png)</span></span>  
4. <span data-ttu-id="5f4d7-433">검색 쿼리에</span><span class="sxs-lookup"><span data-stu-id="5f4d7-433">Next, type the following in the search query.</span></span> <span data-ttu-id="5f4d7-434">`Type=ContainerInventory <ImageID>`를 입력하여 이미지 크기 및 중지되고 실패한 이미지 수와 같은 이미지에 대한 세부 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-434">`Type=ContainerInventory <ImageID>` to see details about the image such as image size and number of stopped and failed images.</span></span>  
   <span data-ttu-id="5f4d7-435">![실패한 컨테이너](./media/log-analytics-containers/containers-failed04.png)</span><span class="sxs-lookup"><span data-stu-id="5f4d7-435">![failed containers](./media/log-analytics-containers/containers-failed04.png)</span></span>

## <a name="search-logs-for-container-data"></a><span data-ttu-id="5f4d7-436">컨테이너 데이터에 대한 로그 검색</span><span class="sxs-lookup"><span data-stu-id="5f4d7-436">Search logs for container data</span></span>
<span data-ttu-id="5f4d7-437">특정 오류 문제를 해결할 때는 환경 내 발생 위치를 확인하는 것이 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-437">When you're troubleshooting a specific error, it can help to see where it is occurring in your environment.</span></span> <span data-ttu-id="5f4d7-438">다음 로그 유형은 원하는 정보를 반환하는 쿼리를 만드는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-438">The following log types will help you create queries to return the information you want.</span></span>


- <span data-ttu-id="5f4d7-439">**ContainerImageInventory** – 이미지별로 정리하여 정보를 찾고 이미지 ID나 크기 같은 이미지 정보를 보려는 경우 이 유형을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-439">**ContainerImageInventory** – Use this type when you're trying to find information organized by image and to view image information such as image IDs or sizes.</span></span>
- <span data-ttu-id="5f4d7-440">**ContainerInventory** – 컨테이너 위치, 해당 컨테이너 이름, 실행 중인 이미지에 대한 정보가 필요할 때 이 유형을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-440">**ContainerInventory** – Use this type when you want information about container location, what their names are, and what images they're running.</span></span>
- <span data-ttu-id="5f4d7-441">**ContainerLog** – 특정 오류 로그 정보와 항목을 찾으려 할 때 이 유형을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-441">**ContainerLog** – Use this type when you want to find specific error log information and entries.</span></span>
- <span data-ttu-id="5f4d7-442">**ContainerNodeInventory_CL** 컨테이너가 상주하는 호스트/노드에 대한 정보를 얻으려면 이 유형을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-442">**ContainerNodeInventory_CL**  Use this type when you want the information about host/node where containers are residing.</span></span> <span data-ttu-id="5f4d7-443">Docker 버전, 오케스트레이션 형식, 저장소 및 네트워크 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-443">It provides you Docker version, orchestration type, storage, and network information.</span></span>
- <span data-ttu-id="5f4d7-444">**ContainerProcess_CL** 컨테이너 내에서 실행 중인 프로세스를 신속하게 확인하려면 이 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-444">**ContainerProcess_CL** Use this type to quickly see the process running within the container.</span></span>
- <span data-ttu-id="5f4d7-445">**ContainerServiceLog** – 시작, 중지, 삭제, 끌어오기 명령 등과 같이 Docker 데몬의 감사 추적 정보를 찾으려 할 때 이 유형을 사용합니다. </span><span class="sxs-lookup"><span data-stu-id="5f4d7-445">**ContainerServiceLog** – Use this type when you're trying to find audit trail information for the Docker daemon, such as start, stop, delete, or pull commands.</span></span>
- <span data-ttu-id="5f4d7-446">**KubeEvents_CL** Kubernetes 이벤트를 확인하려면 이 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-446">**KubeEvents_CL**  Use this type to see the Kubernetes events.</span></span>
- <span data-ttu-id="5f4d7-447">**KubePodInventory_CL** 클러스터 계층 구조 정보를 이해하려면 이 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-447">**KubePodInventory_CL**  Use this type when you want to understand the cluster hierarchy information.</span></span>


### <a name="to-search-logs-for-container-data"></a><span data-ttu-id="5f4d7-448">컨테이너 데이터에 대한 로그 검색</span><span class="sxs-lookup"><span data-stu-id="5f4d7-448">To search logs for container data</span></span>
* <span data-ttu-id="5f4d7-449">최근에 실패했다고 알고 있는 이미지를 선택하고 그에 대한 오류 로그를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-449">Choose an image that you know has failed recently and find the error logs for it.</span></span> <span data-ttu-id="5f4d7-450">**ContainerInventory** 검색을 통해 해당 이미지를 실행 중인 컨테이너 이름부터 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-450">Start by finding a container name that is running that image with a **ContainerInventory** search.</span></span> <span data-ttu-id="5f4d7-451">예를 들어, `Type=ContainerInventory ubuntu Failed`를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-451">For example, search for `Type=ContainerInventory ubuntu Failed`</span></span>  
    <span data-ttu-id="5f4d7-452">![Ubuntu 컨테이너에 대한 검색](./media/log-analytics-containers/search-ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="5f4d7-452">![Search for Ubuntu containers](./media/log-analytics-containers/search-ubuntu.png)</span></span>

  <span data-ttu-id="5f4d7-453">**이름** 옆에 컨테이너 이름을 확인하고 해당 로그를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-453">The name of the container next to **Name**, and search for those logs.</span></span> <span data-ttu-id="5f4d7-454">이 예제에서는 `Type=ContainerLog cranky_stonebreaker`입니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-454">In this example, it is `Type=ContainerLog cranky_stonebreaker`.</span></span>

<span data-ttu-id="5f4d7-455">**성능 정보 보기**</span><span class="sxs-lookup"><span data-stu-id="5f4d7-455">**View performance information**</span></span>

<span data-ttu-id="5f4d7-456">쿼리 작성을 시작할 때는 먼저 가능한 항목을 확인하는 것이 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-456">When you're beginning to construct queries, it can help to see what's possible first.</span></span> <span data-ttu-id="5f4d7-457">예를 들어, 모든 성능 데이터를 보려면 다음 검색 쿼리를 입력하여 광범위 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-457">For example, to see all performance data, try a broad query by typing the following search query.</span></span>

```
Type=Perf
```

![컨테이너 성능](./media/log-analytics-containers/containers-perf01.png)

<span data-ttu-id="5f4d7-459">쿼리 오른쪽에 이름을 입력하여 확인하는 성능 데이터의 범위를 특정 데이터로 한정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-459">You can scope the performance data you're seeing to a specific container by typing the name of it to the right of your query.</span></span>

```
Type=Perf <containerName>
```

<span data-ttu-id="5f4d7-460">그러면 개별 컨테이너에 대해 수집된 성능 메트릭 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-460">That shows the list of performance metrics that are collected for an individual container.</span></span>

![컨테이너 성능](./media/log-analytics-containers/containers-perf03.png)

## <a name="example-log-search-queries"></a><span data-ttu-id="5f4d7-462">로그 검색 쿼리 예제</span><span class="sxs-lookup"><span data-stu-id="5f4d7-462">Example log search queries</span></span>
<span data-ttu-id="5f4d7-463">한두 가지 예제로 쿼리 구성을 시작한 다음 환경에 맞게 수정하는 것이 유용한 경우가 종종 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-463">It's often useful to build queries starting with an example or two and then modifying them to fit your environment.</span></span> <span data-ttu-id="5f4d7-464">먼저 **샘플 쿼리** 영역에서 테스트하면 고급 쿼리를 빌드하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-464">As a starting point, you can experiment with the **Sample Queries** area to help you build more advanced queries.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![컨테이너 쿼리](./media/log-analytics-containers/containers-queries.png)


## <a name="saving-log-search-queries"></a><span data-ttu-id="5f4d7-466">로그 검색 쿼리 저장</span><span class="sxs-lookup"><span data-stu-id="5f4d7-466">Saving log search queries</span></span>
<span data-ttu-id="5f4d7-467">쿼리 저장은 Log Analytics의 표준 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-467">Saving queries is a standard feature in Log Analytics.</span></span> <span data-ttu-id="5f4d7-468">이를 저장해 두면 향후 유용하게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-468">By saving them, you'll have those that you've found useful handy for future use.</span></span>

<span data-ttu-id="5f4d7-469">만든 쿼리가 유용하다고 생각되면 로그 검색 페이지 위쪽의 **즐겨찾기**를 클릭하여 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-469">After you create a query that you find useful, save it by clicking **Favorites** at the top of the Log Search page.</span></span> <span data-ttu-id="5f4d7-470">그러면 나중에 **내 대시보드** 페이지에서 간편하게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-470">Then you can easily access it later from the **My Dashboard** page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f4d7-471">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5f4d7-471">Next steps</span></span>
* <span data-ttu-id="5f4d7-472">[로그를 검색](log-analytics-log-searches.md) 하여 자세한 컨테이너 데이터 레코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4d7-472">[Search logs](log-analytics-log-searches.md) to view detailed container data records.</span></span>
