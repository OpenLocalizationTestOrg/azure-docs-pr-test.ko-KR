---
title: "Azure 로그 분석에서 모니터링 솔루션 aaaContainer | Microsoft Docs"
description: "로그 분석에서 솔루션 컨테이너 모니터링 hello를 사용 하면 Docker 및 Windows 보기 및 관리를 단일 위치에서 컨테이너 호스트입니다."
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
ms.openlocfilehash: 2eed1dd81c22faef78a375fca3ebece9e5300c09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="container-monitoring-solution-in-log-analytics"></a><span data-ttu-id="24ab8-103">Log Analytics의 컨테이너 모니터링 솔루션</span><span class="sxs-lookup"><span data-stu-id="24ab8-103">Container Monitoring solution in Log Analytics</span></span>

![컨테이너 기호](./media/log-analytics-containers/containers-symbol.png)

<span data-ttu-id="24ab8-105">이 문서에서 설명 하는 방법을 tooset를 사용 하 여 hello Docker 및 Windows 보기 및 관리 하는 데 도움이 되는 로그 분석에서 컨테이너 모니터링 솔루션을 한 위치에 컨테이너 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-105">This article describes how tooset up and use hello Container Monitoring solution in Log Analytics, which helps you view and manage your Docker and Windows container hosts in a single location.</span></span> <span data-ttu-id="24ab8-106">소프트웨어 배포 tootheir IT 자동화 하는 toocreate 컨테이너를 사용 하는 소프트웨어 가상화 시스템으로 한 docker는 인프라입니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-106">Docker is a software virtualization system used toocreate containers that automate software deployment tootheir IT infrastructure.</span></span>

<span data-ttu-id="24ab8-107">솔루션에서는 컨테이너는 실행 되는 어떤 컨테이너 이미지를 실행 중인 hello 및 컨테이너를 실행 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-107">hello solution shows which containers are running, what container image they’re running, and where containers are running.</span></span> <span data-ttu-id="24ab8-108">컨테이너에 사용하는 명령을 표시하는 상세한 감사 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-108">You can view detailed audit information showing commands used with containers.</span></span> <span data-ttu-id="24ab8-109">및 보기 tooremotely 보기 Docker 또는 Windows 호스트 필요 없이 중앙 집중화 된 로그를 검색 하 여 컨테이너의 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-109">And, you can troubleshoot containers by viewing and searching centralized logs without having tooremotely view Docker or Windows hosts.</span></span> <span data-ttu-id="24ab8-110">호스트에서 성가시고 과도한 리소스를 소모하는 컨테이너를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-110">You can find containers that may be noisy and consuming excess resources on a host.</span></span> <span data-ttu-id="24ab8-111">또한 컨테이너에 대해 중앙화된 CPU 메모리, 저장소, 네트워크 사용 및 성능 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-111">And, you can view centralized CPU, memory, storage, and network usage and performance information for containers.</span></span> <span data-ttu-id="24ab8-112">Windows를 실행하는 컴퓨터에서 Windows Server, Hyper-V, Docker 컨테이너에서 로그를 중앙 집중화 및 비교할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-112">On computers running Windows, you can centralize and compare logs from Windows Server, Hyper-V, and Docker containers.</span></span> <span data-ttu-id="24ab8-113">hello 솔루션 컨테이너 orchestrators 다음 hello를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-113">hello solution supports hello following container orchestrators:</span></span>

- <span data-ttu-id="24ab8-114">Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="24ab8-114">Docker Swarm</span></span>
- <span data-ttu-id="24ab8-115">DC/OS</span><span class="sxs-lookup"><span data-stu-id="24ab8-115">DC/OS</span></span>
- <span data-ttu-id="24ab8-116">kubernetes</span><span class="sxs-lookup"><span data-stu-id="24ab8-116">Kubernetes</span></span>
- <span data-ttu-id="24ab8-117">서비스 패브릭</span><span class="sxs-lookup"><span data-stu-id="24ab8-117">Service Fabric</span></span>
- <span data-ttu-id="24ab8-118">Red Hat OpenShift</span><span class="sxs-lookup"><span data-stu-id="24ab8-118">Red Hat OpenShift</span></span>


<span data-ttu-id="24ab8-119">hello 다음 다이어그램 관계를 보여 hello 다양 한 컨테이너 호스트와 에이전트가 OMS와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-119">hello following diagram shows hello relationships between various container hosts and agents with OMS.</span></span>

![컨테이너 다이어그램](./media/log-analytics-containers/containers-diagram.png)

## <a name="system-requirements"></a><span data-ttu-id="24ab8-121">시스템 요구 사항</span><span class="sxs-lookup"><span data-stu-id="24ab8-121">System requirements</span></span>

<span data-ttu-id="24ab8-122">을 시작 하기 전에 다음 세부 정보 tooverify hello 필수 조건을 충족 하는 hello를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-122">Before starting, review hello following details tooverify you meet hello prerequisites.</span></span>

### <a name="container-monitoring-solution-support-for-docker-orchestrator-and-os-platform"></a><span data-ttu-id="24ab8-123">Docker Orchestrator 및 OS 플랫폼에 대한 컨테이너 모니터링 솔루션 지원</span><span class="sxs-lookup"><span data-stu-id="24ab8-123">Container monitoring solution support for Docker Orchestrator and OS platform</span></span>
<span data-ttu-id="24ab8-124">hello 다음 표에 정리 되어 hello Docker 오케스트레이션 및 운영 체제 지원 컨테이너 인벤토리, 성능 및 로그 분석을 사용 하 여 로그를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-124">hello following table outlines hello Docker orchestration and operating system monitoring support of container inventory, performance, and logs with Log Analytics.</span></span>   

| | <span data-ttu-id="24ab8-125">ACS</span><span class="sxs-lookup"><span data-stu-id="24ab8-125">ACS</span></span> | <span data-ttu-id="24ab8-126">Linux</span><span class="sxs-lookup"><span data-stu-id="24ab8-126">Linux</span></span> | <span data-ttu-id="24ab8-127">Windows</span><span class="sxs-lookup"><span data-stu-id="24ab8-127">Windows</span></span> | <span data-ttu-id="24ab8-128">컨테이너</span><span class="sxs-lookup"><span data-stu-id="24ab8-128">Container</span></span><br><span data-ttu-id="24ab8-129">인벤토리</span><span class="sxs-lookup"><span data-stu-id="24ab8-129">Inventory</span></span> | <span data-ttu-id="24ab8-130">이미지</span><span class="sxs-lookup"><span data-stu-id="24ab8-130">Image</span></span><br><span data-ttu-id="24ab8-131">인벤토리</span><span class="sxs-lookup"><span data-stu-id="24ab8-131">Inventory</span></span> | <span data-ttu-id="24ab8-132">노드</span><span class="sxs-lookup"><span data-stu-id="24ab8-132">Node</span></span><br><span data-ttu-id="24ab8-133">인벤토리</span><span class="sxs-lookup"><span data-stu-id="24ab8-133">Inventory</span></span> | <span data-ttu-id="24ab8-134">컨테이너</span><span class="sxs-lookup"><span data-stu-id="24ab8-134">Container</span></span><br><span data-ttu-id="24ab8-135">성능</span><span class="sxs-lookup"><span data-stu-id="24ab8-135">Performance</span></span> | <span data-ttu-id="24ab8-136">컨테이너</span><span class="sxs-lookup"><span data-stu-id="24ab8-136">Container</span></span><br><span data-ttu-id="24ab8-137">이벤트</span><span class="sxs-lookup"><span data-stu-id="24ab8-137">Event</span></span> | <span data-ttu-id="24ab8-138">이벤트</span><span class="sxs-lookup"><span data-stu-id="24ab8-138">Event</span></span><br><span data-ttu-id="24ab8-139">로그</span><span class="sxs-lookup"><span data-stu-id="24ab8-139">Log</span></span> | <span data-ttu-id="24ab8-140">컨테이너</span><span class="sxs-lookup"><span data-stu-id="24ab8-140">Container</span></span><br><span data-ttu-id="24ab8-141">로그</span><span class="sxs-lookup"><span data-stu-id="24ab8-141">Log</span></span> |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| <span data-ttu-id="24ab8-142">kubernetes</span><span class="sxs-lookup"><span data-stu-id="24ab8-142">Kubernetes</span></span> | <span data-ttu-id="24ab8-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-143">&#8226;</span></span> | <span data-ttu-id="24ab8-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-144">&#8226;</span></span> | | <span data-ttu-id="24ab8-145">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-145">&#8226;</span></span> | <span data-ttu-id="24ab8-146">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-146">&#8226;</span></span> | <span data-ttu-id="24ab8-147">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-147">&#8226;</span></span> | <span data-ttu-id="24ab8-148">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-148">&#8226;</span></span> | <span data-ttu-id="24ab8-149">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-149">&#8226;</span></span> | <span data-ttu-id="24ab8-150">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-150">&#8226;</span></span> | <span data-ttu-id="24ab8-151">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-151">&#8226;</span></span> |
| <span data-ttu-id="24ab8-152">Mesosphere</span><span class="sxs-lookup"><span data-stu-id="24ab8-152">Mesosphere</span></span><br><span data-ttu-id="24ab8-153">DC/OS</span><span class="sxs-lookup"><span data-stu-id="24ab8-153">DC/OS</span></span> | <span data-ttu-id="24ab8-154">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-154">&#8226;</span></span> | <span data-ttu-id="24ab8-155">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-155">&#8226;</span></span> | | <span data-ttu-id="24ab8-156">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-156">&#8226;</span></span> | <span data-ttu-id="24ab8-157">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-157">&#8226;</span></span> | <span data-ttu-id="24ab8-158">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-158">&#8226;</span></span> | <span data-ttu-id="24ab8-159">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-159">&#8226;</span></span>| <span data-ttu-id="24ab8-160">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-160">&#8226;</span></span> | <span data-ttu-id="24ab8-161">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-161">&#8226;</span></span> | <span data-ttu-id="24ab8-162">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-162">&#8226;</span></span> |
| <span data-ttu-id="24ab8-163">Docker</span><span class="sxs-lookup"><span data-stu-id="24ab8-163">Docker</span></span><br><span data-ttu-id="24ab8-164">Swarm</span><span class="sxs-lookup"><span data-stu-id="24ab8-164">Swarm</span></span> | <span data-ttu-id="24ab8-165">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-165">&#8226;</span></span> | <span data-ttu-id="24ab8-166">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-166">&#8226;</span></span> | <span data-ttu-id="24ab8-167">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-167">&#8226;</span></span> | <span data-ttu-id="24ab8-168">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-168">&#8226;</span></span> | <span data-ttu-id="24ab8-169">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-169">&#8226;</span></span> | <span data-ttu-id="24ab8-170">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-170">&#8226;</span></span> | <span data-ttu-id="24ab8-171">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-171">&#8226;</span></span> | <span data-ttu-id="24ab8-172">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-172">&#8226;</span></span> | | <span data-ttu-id="24ab8-173">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-173">&#8226;</span></span> |
| <span data-ttu-id="24ab8-174">부여</span><span class="sxs-lookup"><span data-stu-id="24ab8-174">Service</span></span><br><span data-ttu-id="24ab8-175">Fabric</span><span class="sxs-lookup"><span data-stu-id="24ab8-175">Fabric</span></span> | | | <span data-ttu-id="24ab8-176">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-176">&#8226;</span></span> | <span data-ttu-id="24ab8-177">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-177">&#8226;</span></span> | <span data-ttu-id="24ab8-178">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-178">&#8226;</span></span> | <span data-ttu-id="24ab8-179">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-179">&#8226;</span></span> | <span data-ttu-id="24ab8-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-180">&#8226;</span></span> | <span data-ttu-id="24ab8-181">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-181">&#8226;</span></span> | <span data-ttu-id="24ab8-182">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-182">&#8226;</span></span> | <span data-ttu-id="24ab8-183">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-183">&#8226;</span></span> |
| <span data-ttu-id="24ab8-184">Red Hat Open</span><span class="sxs-lookup"><span data-stu-id="24ab8-184">Red Hat Open</span></span><br><span data-ttu-id="24ab8-185">Shift</span><span class="sxs-lookup"><span data-stu-id="24ab8-185">Shift</span></span> | | <span data-ttu-id="24ab8-186">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-186">&#8226;</span></span> | | <span data-ttu-id="24ab8-187">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-187">&#8226;</span></span> | <span data-ttu-id="24ab8-188">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-188">&#8226;</span></span>| <span data-ttu-id="24ab8-189">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-189">&#8226;</span></span> | <span data-ttu-id="24ab8-190">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-190">&#8226;</span></span> | <span data-ttu-id="24ab8-191">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-191">&#8226;</span></span> | | <span data-ttu-id="24ab8-192">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-192">&#8226;</span></span> |
| <span data-ttu-id="24ab8-193">Windows Server</span><span class="sxs-lookup"><span data-stu-id="24ab8-193">Windows Server</span></span><br><span data-ttu-id="24ab8-194">(독립 실행형)</span><span class="sxs-lookup"><span data-stu-id="24ab8-194">(standalone)</span></span> | | | <span data-ttu-id="24ab8-195">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-195">&#8226;</span></span> | <span data-ttu-id="24ab8-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-196">&#8226;</span></span> | <span data-ttu-id="24ab8-197">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-197">&#8226;</span></span> | <span data-ttu-id="24ab8-198">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-198">&#8226;</span></span> | <span data-ttu-id="24ab8-199">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-199">&#8226;</span></span> | <span data-ttu-id="24ab8-200">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-200">&#8226;</span></span> | | <span data-ttu-id="24ab8-201">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-201">&#8226;</span></span> |
| <span data-ttu-id="24ab8-202">Linux 서버</span><span class="sxs-lookup"><span data-stu-id="24ab8-202">Linux Server</span></span><br><span data-ttu-id="24ab8-203">(독립 실행형)</span><span class="sxs-lookup"><span data-stu-id="24ab8-203">(standalone)</span></span> | | <span data-ttu-id="24ab8-204">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-204">&#8226;</span></span> | | <span data-ttu-id="24ab8-205">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-205">&#8226;</span></span> | <span data-ttu-id="24ab8-206">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-206">&#8226;</span></span> | <span data-ttu-id="24ab8-207">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-207">&#8226;</span></span> | <span data-ttu-id="24ab8-208">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-208">&#8226;</span></span> | <span data-ttu-id="24ab8-209">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-209">&#8226;</span></span> | | <span data-ttu-id="24ab8-210">&#8226;</span><span class="sxs-lookup"><span data-stu-id="24ab8-210">&#8226;</span></span> |


### <a name="docker-versions-supported-on-linux"></a><span data-ttu-id="24ab8-211">Linux에서 지원되는 Docker 버전</span><span class="sxs-lookup"><span data-stu-id="24ab8-211">Docker versions supported on Linux</span></span>

- <span data-ttu-id="24ab8-212">Docker 1.11 too1.13</span><span class="sxs-lookup"><span data-stu-id="24ab8-212">Docker 1.11 too1.13</span></span>
- <span data-ttu-id="24ab8-213">Docker CE 및 EE v17.06</span><span class="sxs-lookup"><span data-stu-id="24ab8-213">Docker CE and EE v17.06</span></span>

### <a name="x64-linux-distributions-supported-as-container-hosts"></a><span data-ttu-id="24ab8-214">컨테이너 호스트로 지원되는 x64 Linux 배포</span><span class="sxs-lookup"><span data-stu-id="24ab8-214">x64 Linux distributions supported as container hosts</span></span>

- <span data-ttu-id="24ab8-215">Ubuntu 14.04 LTS 및 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="24ab8-215">Ubuntu 14.04 LTS and 16.04 LTS</span></span>
- <span data-ttu-id="24ab8-216">CoreOS(stable)</span><span class="sxs-lookup"><span data-stu-id="24ab8-216">CoreOS(stable)</span></span>
- <span data-ttu-id="24ab8-217">Amazon Linux 2016.09.0</span><span class="sxs-lookup"><span data-stu-id="24ab8-217">Amazon Linux 2016.09.0</span></span>
- <span data-ttu-id="24ab8-218">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="24ab8-218">openSUSE 13.2</span></span>
- <span data-ttu-id="24ab8-219">openSUSE LEAP 42.2</span><span class="sxs-lookup"><span data-stu-id="24ab8-219">openSUSE LEAP 42.2</span></span>
- <span data-ttu-id="24ab8-220">CentOS 7.2 및 7.3</span><span class="sxs-lookup"><span data-stu-id="24ab8-220">CentOS 7.2 and 7.3</span></span>
- <span data-ttu-id="24ab8-221">SLES 12</span><span class="sxs-lookup"><span data-stu-id="24ab8-221">SLES 12</span></span>
- <span data-ttu-id="24ab8-222">RHEL 7.2 및 7.3</span><span class="sxs-lookup"><span data-stu-id="24ab8-222">RHEL 7.2 and 7.3</span></span>
- <span data-ttu-id="24ab8-223">Red Hat OCP(OpenShift Container Platform) 3.4 및 3.5</span><span class="sxs-lookup"><span data-stu-id="24ab8-223">Red Hat OpenShift Container Platform (OCP) 3.4 and 3.5</span></span>
- <span data-ttu-id="24ab8-224">ACS Mesosphere DC/OS 1.7.3 too1.8.8</span><span class="sxs-lookup"><span data-stu-id="24ab8-224">ACS Mesosphere DC/OS 1.7.3 too1.8.8</span></span>
- <span data-ttu-id="24ab8-225">ACS Kubernetes 1.4.5 too1.6</span><span class="sxs-lookup"><span data-stu-id="24ab8-225">ACS Kubernetes 1.4.5 too1.6</span></span>
- <span data-ttu-id="24ab8-226">ACS Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="24ab8-226">ACS Docker Swarm</span></span>

### <a name="supported-windows-operating-system"></a><span data-ttu-id="24ab8-227">지원되는 Windows 운영 체제</span><span class="sxs-lookup"><span data-stu-id="24ab8-227">Supported Windows operating system</span></span>

- <span data-ttu-id="24ab8-228">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="24ab8-228">Windows Server 2016</span></span>
- <span data-ttu-id="24ab8-229">Windows 10 1주년 버전(Professional 또는 Enterprise)</span><span class="sxs-lookup"><span data-stu-id="24ab8-229">Windows 10 Anniversary Edition (Professional or Enterprise)</span></span>

### <a name="docker-versions-supported-on-windows"></a><span data-ttu-id="24ab8-230">Windows에서 지원되는 Docker 버전</span><span class="sxs-lookup"><span data-stu-id="24ab8-230">Docker versions supported on Windows</span></span>

- <span data-ttu-id="24ab8-231">Docker 1.12 - 1.13</span><span class="sxs-lookup"><span data-stu-id="24ab8-231">Docker 1.12 and 1.13</span></span>
- <span data-ttu-id="24ab8-232">Docker 17.03.0 이상</span><span class="sxs-lookup"><span data-stu-id="24ab8-232">Docker 17.03.0 and later</span></span>

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="24ab8-233">설치 하 고 hello 솔루션 구성</span><span class="sxs-lookup"><span data-stu-id="24ab8-233">Installing and configuring hello solution</span></span>
<span data-ttu-id="24ab8-234">다음 정보 tooinstall hello를 사용 하 고 hello 솔루션을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-234">Use hello following information tooinstall and configure hello solution.</span></span>

1. <span data-ttu-id="24ab8-235">Hello 컨테이너 모니터링 솔루션 tooyour OMS 작업 영역에서 추가 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) 또는에 설명 된 hello 프로세스를 사용 하 여 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-235">Add hello Container Monitoring solution tooyour OMS workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>

2. <span data-ttu-id="24ab8-236">OMS 에이전트를 사용하여 Docker를 설치 및 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-236">Install and use Docker with an OMS agent.</span></span>  <span data-ttu-id="24ab8-237">운영 체제에 따라 hello 메서드를 다음에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-237">Based on your operating system, you can choose from hello following methods:</span></span>

  * <span data-ttu-id="24ab8-238">지원 되는 Linux 운영 체제에 설치 및 Docker를 실행 하 고 하 고 다음을 설치 하 고 hello 구성 [Linux 용 OMS 에이전트](log-analytics-agent-linux.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-238">On supported Linux operating systems, install and run Docker and then install and configure hello [OMS Agent for Linux](log-analytics-agent-linux.md).</span></span>  
  * <span data-ttu-id="24ab8-239">CoreOS에 Linux 용 OMS 에이전트 hello를 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-239">On CoreOS, you cannot run hello OMS Agent for Linux.</span></span> <span data-ttu-id="24ab8-240">대신, Linux에 대 한 컨테이너 화 된 버전의 hello OMS 에이전트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-240">Instead, you run a containerized version of hello OMS Agent for Linux.</span></span> <span data-ttu-id="24ab8-241">Azure Government 클라우드에서 컨테이너를 사용하는 경우 [CoreOS를 포함한 Linux 컨테이너 호스트](#for-all-linux-container-hosts-including-coreos) 또는 [CoreOS을 포함한 Azure Government Linux 컨테이너 호스트](#for-all-azure-government-linux-container-hosts-including-coreos)를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="24ab8-241">Review [Linux container hosts including CoreOS](#for-all-linux-container-hosts-including-coreos) or [Azure Government Linux container hosts including CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) if you are working with containers in Azure Government Cloud.</span></span>
  * <span data-ttu-id="24ab8-242">Windows Server 2016 및 Windows 10에서 hello Docker 엔진 및 클라이언트를 설치 후 에이전트 toogather 정보를 연결 하 고 tooLog 분석을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-242">On Windows Server 2016 and Windows 10, install hello Docker Engine and client then connect an agent toogather information and send it tooLog Analytics.</span></span>  

### <a name="container-services"></a><span data-ttu-id="24ab8-243">Container Service</span><span class="sxs-lookup"><span data-stu-id="24ab8-243">Container services</span></span>

- <span data-ttu-id="24ab8-244">Red Hat OpenShift 환경인 경우 [Red Hat OpenShift용 OMS 에이전트 구성](#configure-an-oms-agent-for-red-hat-openshift)을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="24ab8-244">If you have a Red Hat OpenShift environment, review [Configure an OMS agent for Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span></span>
- <span data-ttu-id="24ab8-245">Hello Azure 컨테이너 서비스를 사용 하는 Kubernetes 클러스터를 설정한 경우 검토 [Azure 컨테이너 서비스 클러스터 Microsoft 작업 관리 도구 모음 (OMS)으로 모니터링](../container-service/kubernetes/container-service-kubernetes-oms.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-245">If you have a Kubernetes cluster using hello Azure Container Service, review [Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span></span>
- <span data-ttu-id="24ab8-246">Azure Container Service DC/OS 클러스터가 있는 경우 [Operations Management Suite를 사용하여 Azure Container Service DC/OS 클러스터 모니터링](../container-service/dcos-swarm/container-service-monitoring-oms.md)에서 자세한 내용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24ab8-246">If you have an Azure Container Service DC/OS cluster, learn more at [Monitor an Azure Container Service DC/OS cluster with Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).</span></span>
- <span data-ttu-id="24ab8-247">Docker Swarm 모드 환경에 있는 경우 [Docker Swarm용 OMS 에이전트 구성](#configure-an-oms-agent-for-docker-swarm)에서 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="24ab8-247">If you have a Docker Swarm mode environment, learn more at [Configure an OMS agent for Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span></span>
- <span data-ttu-id="24ab8-248">Service Fabric과 함께 컨테이너를 사용하는 경우 [Azure Service Fabric의 개요](../service-fabric/service-fabric-overview.md)에서 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="24ab8-248">If you use containers with Service Fabric, learn more at [Overview of Azure Service Fabric](../service-fabric/service-fabric-overview.md).</span></span>
- <span data-ttu-id="24ab8-249">검토 hello [Windows에서 Docker 엔진](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) 방법에 대 한 자세한 내용은 문서 tooinstall 하 고 Windows를 실행 하는 컴퓨터에 Docker 엔진을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-249">Review hello [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) article for additional information about how tooinstall and configure your Docker Engines on computers running Windows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="24ab8-250">Docker 실행 중 이어야 합니다 **전에** hello 설치 [Linux 용 OMS 에이전트](log-analytics-agent-linux.md) 컨테이너 호스트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-250">Docker must be running **before** you install hello [OMS Agent for Linux](log-analytics-agent-linux.md) on your container hosts.</span></span> <span data-ttu-id="24ab8-251">Docker를 설치 하기 전에 hello 에이전트를 이미 설치한 경우 Linux 용 OMS 에이전트 tooreinstall hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-251">If you've already installed hello agent before installing Docker, you need tooreinstall hello OMS Agent for Linux.</span></span> <span data-ttu-id="24ab8-252">Docker에 대 한 자세한 내용은 참조 hello [Docker 웹 사이트](https://www.docker.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-252">For more information about Docker, see hello [Docker website](https://www.docker.com).</span></span>


## <a name="linux-container-hosts"></a><span data-ttu-id="24ab8-253">Linux 컨테이너 호스트</span><span class="sxs-lookup"><span data-stu-id="24ab8-253">Linux container hosts</span></span>

<span data-ttu-id="24ab8-254">Docker를 설치 하 고 나면 다음 Docker와 함께 사용할 컨테이너 호스트 tooconfigure hello 에이전트에 대 한 설정을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-254">After you've installed Docker, use hello following settings for your container host tooconfigure hello agent for use with Docker.</span></span> <span data-ttu-id="24ab8-255">먼저 OMS 작업 영역 ID 및 키 hello Azure 포털에서에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-255">First you need your OMS workspace ID and key, which you can find in hello Azure portal.</span></span> <span data-ttu-id="24ab8-256">작업 영역에서 클릭 **빠른 시작** > **컴퓨터** tooview 프로그램 **작업 영역 ID** 및 **기본 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-256">In your workspace, click **Quick Start** > **Computers** tooview your **Workspace ID** and **Primary Key**.</span></span>  <span data-ttu-id="24ab8-257">두 항목을 복사하여 선호하는 편집기에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-257">Copy and paste both into your favorite editor.</span></span>

### <a name="for-all-linux-container-hosts-except-coreos"></a><span data-ttu-id="24ab8-258">CoreOS를 제외한 모든 Linux 컨테이너 호스트의 경우</span><span class="sxs-lookup"><span data-stu-id="24ab8-258">For all Linux container hosts except CoreOS</span></span>

- <span data-ttu-id="24ab8-259">자세한 내용 및 단계 tooinstall Linux 용 OMS 에이전트를 hello 하는 방법에 대 한 참조 [프로그램 Linux 컴퓨터 tooOperations Management Suite (OMS) 연결](log-analytics-agent-linux.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-259">For more information and steps on how tooinstall hello OMS Agent for Linux, see [Connect your Linux Computers tooOperations Management Suite (OMS)](log-analytics-agent-linux.md).</span></span>

### <a name="for-all-linux-container-hosts-including-coreos"></a><span data-ttu-id="24ab8-260">CoreOS를 포함한 모든 Linux 컨테이너 호스트의 경우</span><span class="sxs-lookup"><span data-stu-id="24ab8-260">For all Linux container hosts including CoreOS</span></span>

<span data-ttu-id="24ab8-261">원하는 toomonitor hello OMS 컨테이너를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-261">Start hello OMS container that you want toomonitor.</span></span> <span data-ttu-id="24ab8-262">수정 하 고 다음 예제는 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="24ab8-262">Modify and use hello following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -e WSID="your workspace id" -e KEY="your key" -h=`hostname` -p 127.0.0.1:25225:25225 --name="omsagent" --restart=always microsoft/oms
```

### <a name="for-all-azure-government-linux-container-hosts-including-coreos"></a><span data-ttu-id="24ab8-263">CoreOS를 포함한 모든 Azure Government Linux 컨테이너 호스트의 경우</span><span class="sxs-lookup"><span data-stu-id="24ab8-263">For all Azure Government Linux container hosts including CoreOS</span></span>

<span data-ttu-id="24ab8-264">원하는 toomonitor hello OMS 컨테이너를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-264">Start hello OMS container that you want toomonitor.</span></span> <span data-ttu-id="24ab8-265">수정 하 고 다음 예제는 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="24ab8-265">Modify and use hello following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/log:/var/log -e WSID="your workspace id" -e KEY="your key" -e DOMAIN="opinsights.azure.us" -p 127.0.0.1:25225:25225 -p 127.0.0.1:25224:25224/udp --name="omsagent" -h=`hostname` --restart=always microsoft/oms
```

### <a name="switching-from-using-an-installed-linux-agent-tooone-in-a-container"></a><span data-ttu-id="24ab8-266">컨테이너에는 설치 된 Linux 에이전트 tooone를 사용 하 여에서 전환</span><span class="sxs-lookup"><span data-stu-id="24ab8-266">Switching from using an installed Linux agent tooone in a container</span></span>
<span data-ttu-id="24ab8-267">이전에 에이전트를 직접 설치 하는 hello를 사용 하 고 원하는 경우 tooinstead 컨테이너에서 실행 중인 에이전트를 먼저 사용 하 여 Linux 용 OMS 에이전트 hello를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-267">If you previously used hello directly-installed agent and want tooinstead use an agent running in a container, you must first remove hello OMS Agent for Linux.</span></span> <span data-ttu-id="24ab8-268">참조 [Linux 용 OMS 에이전트 제거 시 hello](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) toosuccessfully 제거 하는 방법을 toounderstand hello 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-268">See [Uninstalling hello OMS Agent for Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) toounderstand how toosuccessfully uninstall hello agent.</span></span>  

### <a name="configure-an-oms-agent-for-docker-swarm"></a><span data-ttu-id="24ab8-269">Docker Swarm용 OMS 에이전트 구성</span><span class="sxs-lookup"><span data-stu-id="24ab8-269">Configure an OMS agent for Docker Swarm</span></span>

<span data-ttu-id="24ab8-270">Docker는 Docker Swarm에서 글로벌 서비스 hello OMS 에이전트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-270">You can run hello OMS Agent as a global service on Docker Swarm.</span></span> <span data-ttu-id="24ab8-271">다음 정보 toocreate OMS 에이전트 서비스는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-271">Use hello following information toocreate an OMS Agent service.</span></span> <span data-ttu-id="24ab8-272">OMS 작업 영역 ID와 기본 키 tooinsert 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-272">You need tooinsert your OMS Workspace ID and Primary Key.</span></span>

- <span data-ttu-id="24ab8-273">Hello 다음 hello 마스터 노드에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-273">Run hello following on hello master node.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock  -e WSID="<WORKSPACE ID>" -e KEY="<PRIMARY KEY>" -p 25225:25225 -p 25224:25224/udp  --restart-condition=on-failure microsoft/oms
    ```

### <a name="configure-an-oms-agent-for-red-hat-openshift"></a><span data-ttu-id="24ab8-274">Red Hat OpenShift용 OMS 에이전트 구성</span><span class="sxs-lookup"><span data-stu-id="24ab8-274">Configure an OMS Agent for Red Hat OpenShift</span></span>
<span data-ttu-id="24ab8-275">세 가지 방법으로 tooadd hello OMS 에이전트 tooRed Hat OpenShift toostart 컨테이너 모니터링 데이터를 수집할 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-275">There are three ways tooadd hello OMS Agent tooRed Hat OpenShift toostart collecting container monitoring data.</span></span>

* <span data-ttu-id="24ab8-276">[Linux 용 OMS 에이전트 hello 설치](log-analytics-agent-linux.md) 각 OpenShift 노드에서 직접</span><span class="sxs-lookup"><span data-stu-id="24ab8-276">[Install hello OMS Agent for Linux](log-analytics-agent-linux.md) directly on each OpenShift node</span></span>  
* <span data-ttu-id="24ab8-277">Azure에 있는 각 OpenShift 노드에서 [Log Analytics VM 확장을 사용하도록 설정](log-analytics-azure-vm-extension.md)</span><span class="sxs-lookup"><span data-stu-id="24ab8-277">[Enable Log Analytics VM Extension](log-analytics-azure-vm-extension.md) on each OpenShift node residing in Azure</span></span>  
* <span data-ttu-id="24ab8-278">OpenShift 데몬 집합으로 hello OMS 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-278">Install hello OMS Agent as a OpenShift daemon-set</span></span>  

<span data-ttu-id="24ab8-279">이 섹션에서는 OpenShift 데몬 집합으로 hello 단계 필요한 tooinstall hello OMS 에이전트를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-279">In this section we cover hello steps required tooinstall hello OMS Agent as an OpenShift daemon-set.</span></span>  

1. <span data-ttu-id="24ab8-280">Toohello OpenShift 마스터 노드 및 복사 hello yaml 파일 로그온 [ocp omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) GitHub에서 tooyour 노드를 마스터 및 hello 값 OMS 작업 영역 ID와 기본 키를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-280">Sign on toohello OpenShift master node and copy hello yaml file [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) from GitHub tooyour master node and modify hello value with your OMS Workspace ID and with your Primary Key.</span></span>
2. <span data-ttu-id="24ab8-281">OMS에 대 한 hello 명령을 toocreate 다음 프로젝트를 실행 하 고 hello 사용자 계정을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-281">Run hello following commands toocreate a project for OMS and set hello user account.</span></span>

    ```
    oadm new-project omslogging --node-selector='zone=default'
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="24ab8-282">toodeploy hello 데몬 집합 hello 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-282">toodeploy hello daemon-set, run hello following:</span></span>

    `oc create -f ocp-omsagent.yaml`

5. <span data-ttu-id="24ab8-283">tooverify 구성 되어 있으며 제대로 작동 hello 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-283">tooverify it is configured and working correctly, type hello following:</span></span>

    `oc describe daemonset omsagent`  

    <span data-ttu-id="24ab8-284">및 hello 출력와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-284">and hello output should resemble:</span></span>

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

<span data-ttu-id="24ab8-285">원할 경우 toouse 비밀 toosecure OMS 작업 영역 ID와 기본 키 hello OMS 에이전트 데몬 집합 yaml 파일을 사용 하는 경우 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-285">If you want toouse secrets toosecure your OMS Workspace ID and Primary Key when using hello OMS Agent daemon-set yaml file, perform hello following steps.</span></span>

1. <span data-ttu-id="24ab8-286">Toohello OpenShift 마스터 노드 및 복사 hello yaml 파일 로그온 [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) 및 스크립트를 생성 하는 암호 [ocp secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) GitHub에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-286">Sign on toohello OpenShift master node and copy hello yaml file [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) and secret generating script [ocp-secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) from GitHub.</span></span>  <span data-ttu-id="24ab8-287">이 스크립트는 hello 비밀 yaml 파일 toosecure OMS 작업 영역 ID와 기본 키를 생성 하는 사용자 정보를 분입니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-287">This script will generate hello secrets yaml file for OMS Workspace ID and Primary Key toosecure your secrete information.</span></span>  
2. <span data-ttu-id="24ab8-288">OMS에 대 한 hello 명령을 toocreate 다음 프로젝트를 실행 하 고 hello 사용자 계정을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-288">Run hello following commands toocreate a project for OMS and set hello user account.</span></span> <span data-ttu-id="24ab8-289">OMS 작업 영역 ID에 대 한 스크립트를 생성 하는 hello 비밀 요청 <WSID> 와 기본 키 <KEY> 완료 되 면 hello ocp secret.yaml 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-289">hello secret generating script asks for your OMS Workspace ID <WSID> and Primary Key <KEY> and upon completion, it creates hello ocp-secret.yaml file.</span></span>  

    ```
    oadm new-project omslogging --node-selector='zone=default'  
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="24ab8-290">Hello 다음을 실행 하 여 hello 보안 파일을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-290">Deploy hello secret file by running hello following:</span></span>

    `oc create -f ocp-secret.yaml`

5. <span data-ttu-id="24ab8-291">Hello 다음을 실행 하 여 배포를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-291">Verify deployment by running hello following:</span></span>

    `oc describe secret omsagent-secret`  

    <span data-ttu-id="24ab8-292">및 hello 출력와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-292">and hello  output should resemble:</span></span>  

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

6. <span data-ttu-id="24ab8-293">Hello 다음을 실행 하 여 hello OMS 에이전트 데몬 집합 yaml 파일을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-293">Deploy hello OMS Agent daemon-set yaml file by running hello following:</span></span>

    `oc create -f ocp-ds-omsagent.yaml`  

7. <span data-ttu-id="24ab8-294">Hello 다음을 실행 하 여 배포를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-294">Verify deployment by running hello following:</span></span>

    `oc describe ds oms`

    <span data-ttu-id="24ab8-295">및 hello 출력와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-295">and hello output should resemble:</span></span>

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

### <a name="secure-your-secret-information-for-docker-swarm-and-kubernetes"></a><span data-ttu-id="24ab8-296">Docker Swarm 및 Kubernetes에 대한 비밀 정보를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-296">Secure your secret information for Docker Swarm and Kubernetes</span></span>

<span data-ttu-id="24ab8-297">Docker Swarm 및 Kubernetes 컨테이너 서비스에 대한 비밀 OMS 작업 영역 ID 및 기본 키를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-297">You can secure your secret OMS Workspace ID and Primary Keys for Docker Swarm and Kubernetes container services.</span></span>

#### <a name="secure-secrets-for-docker-swarm"></a><span data-ttu-id="24ab8-298">Docker Swarm에 대한 비밀 보호</span><span class="sxs-lookup"><span data-stu-id="24ab8-298">Secure secrets for Docker Swarm</span></span>

<span data-ttu-id="24ab8-299">Docker는 Docker Swarm 작업 영역 ID와 기본 키에 대 한 hello 암호를 만든 후 실행 하면 hello OMSagent 용 hello Docker 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-299">For Docker Swarm, once hello secret for Workspace ID and Primary Key is created, you can run hello create hello Docker service for OMSagent.</span></span> <span data-ttu-id="24ab8-300">다음 정보 toocreate hello 비밀 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-300">Use hello following information toocreate your secret information.</span></span>

1. <span data-ttu-id="24ab8-301">Hello 다음 hello 마스터 노드에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-301">Run hello following on hello master node.</span></span>

    ```
    echo "WSID" | docker secret create WSID -
    echo "KEY" | docker secret create KEY -
    ```

2. <span data-ttu-id="24ab8-302">비밀이 제대로 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-302">Verify that secrets were created properly.</span></span>

    ```
    keiko@swarmm-master-13957614-0:/run# sudo docker secret ls
    ```

    ```
    ID                          NAME                CREATED             UPDATED
    j2fj153zxy91j8zbcitnjxjiv   WSID                43 minutes ago      43 minutes ago
    l9rh3n987g9c45zffuxdxetd9   KEY                 38 minutes ago      38 minutes ago
    ```

3. <span data-ttu-id="24ab8-303">다음 명령은 toomount hello 비밀 toohello 실행된 hello OMS 에이전트 컨테이너 화 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-303">Run hello following command toomount hello secrets toohello containerized OMS Agent.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock --secret source=WSID,target=WSID --secret source=KEY,target=KEY  -p 25225:25225 -p 25224:25224/udp --restart-condition=on-failure microsoft/oms
    ```

#### <a name="secure-secrets-for-kubernetes-with-yaml-files"></a><span data-ttu-id="24ab8-304">yaml 파일로 Kubernetes에 대한 비밀 보호</span><span class="sxs-lookup"><span data-stu-id="24ab8-304">Secure secrets for Kubernetes with yaml files</span></span>

<span data-ttu-id="24ab8-305">Kubernetes, 작업 영역 ID와 기본 키에 대 한 스크립트 toogenerate hello 비밀 yaml 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-305">For Kubernetes, you use a script toogenerate hello secrets yaml file for your Workspace ID and Primary Key.</span></span> <span data-ttu-id="24ab8-306">Hello에 [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) 페이지에 상관 없이 사용자의 비밀 정보를 사용할 수 있는 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-306">At hello [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) page, there are files that you can use with or without your secret information.</span></span>

- <span data-ttu-id="24ab8-307">기본 OMS 에이전트 DaemonSet hello 비밀 정보 (omsagent.yaml)가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-307">hello Default OMS Agent DaemonSet does not have secret information (omsagent.yaml)</span></span>
- <span data-ttu-id="24ab8-308">hello OMS 에이전트 DaemonSet yaml 파일 비밀 생성 스크립트 toogenerate hello 비밀 yaml (omsagentsecret.yaml) 파일이 있는 비밀 정보 (omsagent ds secrets.yaml)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-308">hello OMS Agent DaemonSet yaml file uses secret information (omsagent-ds-secrets.yaml) with secret generation scripts toogenerate hello secrets yaml (omsagentsecret.yaml) file.</span></span>

<span data-ttu-id="24ab8-309">Toocreate omsagent DaemonSets 상관 없이 암호를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-309">You can choose toocreate omsagent DaemonSets with or without secrets.</span></span>

##### <a name="default-omsagent-daemonset-yaml-file-without-secrets"></a><span data-ttu-id="24ab8-310">비밀이 없는 기본 OMSagent DaemonSet yaml 파일</span><span class="sxs-lookup"><span data-stu-id="24ab8-310">Default OMSagent DaemonSet yaml file without secrets</span></span>

- <span data-ttu-id="24ab8-311">Hello 기본 OMS 에이전트 DaemonSet yaml 파일에 대 한 대체 hello `<WSID>` 및 `<KEY>` tooyour WSID 및 키입니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-311">For hello default OMS Agent DaemonSet yaml file, replace hello `<WSID>` and `<KEY>` tooyour WSID and KEY.</span></span> <span data-ttu-id="24ab8-312">Hello 파일 tooyour 마스터 노드 및 실행된 hello 다음 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-312">Copy hello file tooyour master node and run hello following:</span></span>

    ```
    sudo kubectl create -f omsagent.yaml
    ```

##### <a name="default-omsagent-daemonset-yaml-file-with-secrets"></a><span data-ttu-id="24ab8-313">비밀이 있는 기본 OMSagent DaemonSet yaml 파일</span><span class="sxs-lookup"><span data-stu-id="24ab8-313">Default OMSagent DaemonSet yaml file with secrets</span></span>

1. <span data-ttu-id="24ab8-314">toouse 비밀 정보를 사용 하 여 OMS 에이전트 DaemonSet hello 비밀을 먼저 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-314">toouse OMS Agent DaemonSet using secret information, create hello secrets first.</span></span>
    1. <span data-ttu-id="24ab8-315">Hello 스크립트 및 비밀 템플릿 파일을 복사 하 고 hello에 있는지 확인 동일한 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-315">Copy hello script and secret template file and make sure they are on hello same directory.</span></span>
        - <span data-ttu-id="24ab8-316">비밀 생성 스크립트 - secret-gen.sh</span><span class="sxs-lookup"><span data-stu-id="24ab8-316">Secret generating script - secret-gen.sh</span></span>
        - <span data-ttu-id="24ab8-317">비밀 템플릿 - secret-template.yaml</span><span class="sxs-lookup"><span data-stu-id="24ab8-317">secret template - secret-template.yaml</span></span>
    2. <span data-ttu-id="24ab8-318">다음 예제는 hello 같은 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-318">Run hello script, like hello following example.</span></span> <span data-ttu-id="24ab8-319">OMS 작업 영역 ID와 기본 키 hello 스크립트 hello에 대 한 요청에 입력 한 후 hello 스크립트 파일을 만듭니다 비밀 yaml 실행할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-319">hello script asks for hello OMS Workspace ID and Primary Key and after you enter them, hello script creates a secret yaml file so you can run it.</span></span>   

        ```
        #> sudo bash ./secret-gen.sh
        ```

    3. <span data-ttu-id="24ab8-320">Hello 비밀 pod를 hello 다음을 실행 하 여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-320">Create hello secrets pod by running hello following:</span></span>
        ```
        sudo kubectl create -f omsagentsecret.yaml
        ```

    4. <span data-ttu-id="24ab8-321">tooverify hello 다음 실행:</span><span class="sxs-lookup"><span data-stu-id="24ab8-321">tooverify, run hello following:</span></span>

        ```
        keiko@ubuntu16-13db:~# sudo kubectl get secrets
        ```

        <span data-ttu-id="24ab8-322">출력은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-322">Output should resemble:</span></span>

        ```
        NAME                  TYPE                                  DATA      AGE
        default-token-gvl91   kubernetes.io/service-account-token   3         50d
        omsagent-secret       Opaque                                2         1d
        ```

        ```
        keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
        ```

        <span data-ttu-id="24ab8-323">출력은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-323">Output should resemble:</span></span>

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

    5. <span data-ttu-id="24ab8-324">``` sudo kubectl create -f omsagent-ds-secrets.yaml ```을 실행하여 omsagent daemon-set 만들기</span><span class="sxs-lookup"><span data-stu-id="24ab8-324">Create your omsagent daemon-set by running ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

2. <span data-ttu-id="24ab8-325">해당 hello OMS 에이전트 DaemonSet 실행 중인 비슷한 toohello 다음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-325">Verify that hello OMS Agent DaemonSet is running, similar toohello following:</span></span>

    ```
    keiko@ubuntu16-13db:~# sudo kubectl get ds omsagent
    ```

    ```
    NAME       DESIRED   CURRENT   NODE-SELECTOR   AGE
    omsagent   3         3         <none>          1h
    ```


<span data-ttu-id="24ab8-326">Kubernetes에 대 한 작업 영역 ID와 기본 키에 대 한 스크립트 toogenerate hello 비밀 yaml 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-326">For Kubernetes, use a script toogenerate hello secrets yaml file for Workspace ID and Primary Key.</span></span> <span data-ttu-id="24ab8-327">다음 예에서는 정보 hello로 사용 하 여 hello [omsagent yaml 파일](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) toosecure 비밀 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-327">Use hello following example information with hello [omsagent yaml file](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) toosecure your secret information.</span></span>

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

## <a name="windows-container-hosts"></a><span data-ttu-id="24ab8-328">Windows 컨테이너 호스트</span><span class="sxs-lookup"><span data-stu-id="24ab8-328">Windows container hosts</span></span>

### <a name="preparation-before-installing-windows-agents"></a><span data-ttu-id="24ab8-329">Windows 에이전트 설치 전 준비</span><span class="sxs-lookup"><span data-stu-id="24ab8-329">Preparation before installing Windows agents</span></span>

<span data-ttu-id="24ab8-330">Windows를 실행 하는 컴퓨터에 에이전트를 설치 하기 전에 tooconfigure hello Docker 서비스가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-330">Before you install agents on computers running Windows, you need tooconfigure hello Docker service.</span></span> <span data-ttu-id="24ab8-331">hello 구성은 모니터링에 대 한 hello Windows 에이전트 또는 hello 로그 분석 가상 컴퓨터 확장 toouse hello hello 에이전트 hello Docker 디먼에 원격으로 액세스할 수 있도록 Docker TCP 소켓 및 toocapture 데이터를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-331">hello configuration allows hello Windows agent or hello Log Analytics virtual machine extension toouse hello Docker TCP socket so that hello agents can access hello Docker daemon remotely and toocapture data for monitoring.</span></span>

#### <a name="toostart-docker-and-verify-its-configuration"></a><span data-ttu-id="24ab8-332">Docker toostart 하 고 해당 구성을 확인</span><span class="sxs-lookup"><span data-stu-id="24ab8-332">toostart Docker and verify its configuration</span></span>

<span data-ttu-id="24ab8-333">Windows Server에 대 한 명명 된 파이프 TCP 필요한 단계 tooset 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-333">There are steps needed tooset up TCP named pipe for Windows Server:</span></span>

1. <span data-ttu-id="24ab8-334">Windows PowerShell에서 TCP 파이프 및 명명된 파이프를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-334">In Windows PowerShell, enable TCP pipe and named pipe.</span></span>

    ```
    Stop-Service docker
    dockerd --unregister-service
    dockerd --register-service -H npipe:// -H 0.0.0.0:2375  
    Start-Service docker
    ```

2. <span data-ttu-id="24ab8-335">명명 된 파이프 및 TCP 파이프에 대 한 hello 구성 파일을 사용 하 여 Docker를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-335">Configure Docker with hello configuration file for TCP pipe and named pipe.</span></span> <span data-ttu-id="24ab8-336">hello 구성 파일은 C:\ProgramData\docker\config\daemon.json에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-336">hello configuration file is located at C:\ProgramData\docker\config\daemon.json.</span></span>

    <span data-ttu-id="24ab8-337">Hello daemon.json 파일에 hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-337">In hello daemon.json file, you will need hello following:</span></span>

    ```
    {
    "hosts": ["tcp://0.0.0.0:2375", "npipe://"]
    }
    ```

<span data-ttu-id="24ab8-338">Windows 컨테이너와 함께 사용 하는 hello Docker 디먼 구성에 대 한 자세한 내용은 참조 [Windows에서 Docker 엔진](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon)합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-338">For more information about hello Docker daemon configuration used with Windows Containers, see [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span></span>


### <a name="install-windows-agents"></a><span data-ttu-id="24ab8-339">Windows 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="24ab8-339">Install Windows agents</span></span>

<span data-ttu-id="24ab8-340">Windows tooenable 및 모니터링, Hyper-v 컨테이너는 컨테이너 호스트 하는 Windows 컴퓨터에서 Microsoft Monitoring Agent (MMA) hello를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-340">tooenable Windows and Hyper-V container monitoring, install hello Microsoft Monitoring Agent (MMA) on Windows computers that are container hosts.</span></span> <span data-ttu-id="24ab8-341">온-프레미스 환경에서 Windows를 실행 하는 컴퓨터에 대 한 참조 [연결 Windows 컴퓨터 tooLog 분석](log-analytics-windows-agents.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-341">For computers running Windows in your on-premises environment, see [Connect Windows computers tooLog Analytics](log-analytics-windows-agents.md).</span></span> <span data-ttu-id="24ab8-342">가상 컴퓨터에 대 한 Azure에서 실행에 연결 분석 tooLog hello를 사용 하 여 [가상 컴퓨터 확장](log-analytics-azure-vm-extension.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-342">For virtual machines running in Azure, connect them tooLog Analytics using hello [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="24ab8-343">Service Fabric에서 실행 중인 Windows 컨테이너를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-343">You can monitor Windows containers running on Service Fabric.</span></span> <span data-ttu-id="24ab8-344">그러나 [Azure에서 실행 중인 가상 컴퓨터](log-analytics-azure-vm-extension.md) 및 [온-프레미스 환경에서 Windows를 실행하는 컴퓨터](log-analytics-windows-agents.md)만 현재 Service Fabric에 대해 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-344">However, only [virtual machines running in Azure](log-analytics-azure-vm-extension.md) and [computers running Windows in your on-premises environment](log-analytics-windows-agents.md) are currently supported for Service Fabric.</span></span>

<span data-ttu-id="24ab8-345">Windows에 대 한 해당 hello 솔루션 컨테이너 모니터링이 올바르게 설정 되어 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-345">You can verify that hello Container Monitoring solution is set correctly for Windows.</span></span> <span data-ttu-id="24ab8-346">에 대 한 확인 여부에 관계 없이 hello 관리 팩 다운로드 제대로 toocheck *ContainerManagement.xxx*합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-346">toocheck whether hello management pack was download properly, look for *ContainerManagement.xxx*.</span></span> <span data-ttu-id="24ab8-347">hello 파일 hello C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs 폴더에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-347">hello files should be in hello C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs folder.</span></span>


## <a name="solution-components"></a><span data-ttu-id="24ab8-348">솔루션 구성 요소</span><span class="sxs-lookup"><span data-stu-id="24ab8-348">Solution components</span></span>

<span data-ttu-id="24ab8-349">Windows 에이전트를 사용 하는 경우 다음 hello 다음 관리 팩은 각 컴퓨터에 설치 에이전트가이 솔루션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-349">If you are using Windows agents, then hello following management pack is installed on each computer with an agent when you add this solution.</span></span> <span data-ttu-id="24ab8-350">구성 또는 유지 관리 없습니다 hello 관리 팩에 대 한 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-350">No configuration or maintenance is required for hello management pack.</span></span>

- <span data-ttu-id="24ab8-351">C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs에 설치된 *ContainerManagement.xxx*</span><span class="sxs-lookup"><span data-stu-id="24ab8-351">*ContainerManagement.xxx* installed in C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs</span></span>

## <a name="container-data-collection-details"></a><span data-ttu-id="24ab8-352">컨테이너 데이터 컬렉션 세부 정보</span><span class="sxs-lookup"><span data-stu-id="24ab8-352">Container data collection details</span></span>
<span data-ttu-id="24ab8-353">컨테이너 모니터링 솔루션 hello 컨테이너 호스트 및 사용 하도록 설정 하면 에이전트를 사용 하 여 컨테이너에서 다양 한 성능 메트릭 및 로그 데이터를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-353">hello Container Monitoring solution collects various performance metrics and log data from container hosts and containers using agents that you enable.</span></span>

<span data-ttu-id="24ab8-354">데이터 수집 3 분 마다 에이전트 유형만 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-354">Data is collected every three minutes by hello following agent types.</span></span>

- [<span data-ttu-id="24ab8-355">OMS Agent for Linux</span><span class="sxs-lookup"><span data-stu-id="24ab8-355">OMS Agent for Linux</span></span>](log-analytics-linux-agents.md)
- [<span data-ttu-id="24ab8-356">Windows 에이전트</span><span class="sxs-lookup"><span data-stu-id="24ab8-356">Windows agent</span></span>](log-analytics-windows-agents.md)
- [<span data-ttu-id="24ab8-357">Log Analytics VM 확장</span><span class="sxs-lookup"><span data-stu-id="24ab8-357">Log Analytics VM extension</span></span>](log-analytics-azure-vm-extension.md)


### <a name="container-records"></a><span data-ttu-id="24ab8-358">컨테이너 레코드</span><span class="sxs-lookup"><span data-stu-id="24ab8-358">Container records</span></span>

<span data-ttu-id="24ab8-359">hello 다음 표에서 hello 컨테이너 모니터링 솔루션 및 로그 검색 결과에 표시 되는 hello 데이터 형식에 의해 수집 된 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-359">hello following table shows examples of records collected by hello Container Monitoring solution and hello data types that appear in log search results.</span></span>

| <span data-ttu-id="24ab8-360">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="24ab8-360">Data type</span></span> | <span data-ttu-id="24ab8-361">로그 검색의 데이터 유형</span><span class="sxs-lookup"><span data-stu-id="24ab8-361">Data type in Log Search</span></span> | <span data-ttu-id="24ab8-362">필드</span><span class="sxs-lookup"><span data-stu-id="24ab8-362">Fields</span></span> |
| --- | --- | --- |
| <span data-ttu-id="24ab8-363">호스트 및 컨테이너에 대한 성능</span><span class="sxs-lookup"><span data-stu-id="24ab8-363">Performance for hosts and containers</span></span> | `Type=Perf` | <span data-ttu-id="24ab8-364">컴퓨터, ObjectName, CounterName &#40;%프로세서 시간, 디스크 읽기 MB, 디스크 쓰기 MB, 메모리 사용 MB, 네트워크 수신 바이트, 네트워크 송신 바이트, 프로세서 사용 초, 네트워크&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="24ab8-364">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span></span> |
| <span data-ttu-id="24ab8-365">컨테이너 인벤토리</span><span class="sxs-lookup"><span data-stu-id="24ab8-365">Container inventory</span></span> | `Type=ContainerInventory` | <span data-ttu-id="24ab8-366">TimeGenerated, 컴퓨터, 컨테이너 이름, ContainerHostname, 이미지, ImageTag, ContainerState, ExitCode, EnvironmentVar, 명령, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span><span class="sxs-lookup"><span data-stu-id="24ab8-366">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span></span> |
| <span data-ttu-id="24ab8-367">컨테이너 이미지 인벤토리</span><span class="sxs-lookup"><span data-stu-id="24ab8-367">Container image inventory</span></span> | `Type=ContainerImageInventory` | <span data-ttu-id="24ab8-368">TimeGenerated, 컴퓨터, 이미지, ImageTag, ImageSize, VirtualSize, 실행 중, 일시 중지됨, 중지됨, 실패, SourceSystem, ImageID, TotalContainer</span><span class="sxs-lookup"><span data-stu-id="24ab8-368">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span></span> |
| <span data-ttu-id="24ab8-369">컨테이너 로그</span><span class="sxs-lookup"><span data-stu-id="24ab8-369">Container log</span></span> | `Type=ContainerLog` | <span data-ttu-id="24ab8-370">TimeGenerated, 컴퓨터, 이미지 ID, 컨테이너 이름, LogEntrySource, LogEntry, SourceSystem, ContainerID</span><span class="sxs-lookup"><span data-stu-id="24ab8-370">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="24ab8-371">컨테이너 서비스 로그</span><span class="sxs-lookup"><span data-stu-id="24ab8-371">Container service log</span></span> | `Type=ContainerServiceLog`  | <span data-ttu-id="24ab8-372">TimeGenerated, 컴퓨터, TimeOfCommand, 이미지, 명령, SourceSystem, ContainerID</span><span class="sxs-lookup"><span data-stu-id="24ab8-372">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="24ab8-373">컨테이너 노드 인벤토리</span><span class="sxs-lookup"><span data-stu-id="24ab8-373">Container node inventory</span></span> | `Type=ContainerNodeInventory_CL`| <span data-ttu-id="24ab8-374">TimeGenerated, 컴퓨터, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="24ab8-374">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span></span>|
| <span data-ttu-id="24ab8-375">Kubernetes 인벤토리</span><span class="sxs-lookup"><span data-stu-id="24ab8-375">Kubernetes inventory</span></span> | `Type=KubePodInventory_CL` | <span data-ttu-id="24ab8-376">TimeGenerated, 컴퓨터, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="24ab8-376">TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span></span> |
| <span data-ttu-id="24ab8-377">컨테이너 프로세스</span><span class="sxs-lookup"><span data-stu-id="24ab8-377">Container process</span></span> | `Type=ContainerProcess_CL` | <span data-ttu-id="24ab8-378">TimeGenerated, 컴퓨터, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="24ab8-378">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span></span> |
| <span data-ttu-id="24ab8-379">kubernetes 이벤트</span><span class="sxs-lookup"><span data-stu-id="24ab8-379">Kubernetes events</span></span> | `Type=KubeEvents_CL` | <span data-ttu-id="24ab8-380">TimeGenerated, 컴퓨터, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, 메시지</span><span class="sxs-lookup"><span data-stu-id="24ab8-380">TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message</span></span> |

<span data-ttu-id="24ab8-381">레이블 추가 너무*PodLabel* 데이터 유형은 사용자 지정 레이블을 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-381">Labels appended too*PodLabel* data types are your own custom labels.</span></span> <span data-ttu-id="24ab8-382">hello hello 테이블에 표시 되는 추가 된 PodLabel 레이블을 예입니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-382">hello appended PodLabel labels shown in hello table are examples.</span></span> <span data-ttu-id="24ab8-383">따라서 `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s`는 사용자 환경의 데이터 집합에 따라 달라지며 일반적으로 `PodLabel_yourlabel_s`와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-383">So, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` will differ in your environment's data set and generically resemble `PodLabel_yourlabel_s`.</span></span>


## <a name="monitor-containers"></a><span data-ttu-id="24ab8-384">모니터 컨테이너</span><span class="sxs-lookup"><span data-stu-id="24ab8-384">Monitor containers</span></span>
<span data-ttu-id="24ab8-385">Hello OMS 포털에서 사용 하도록 설정 하는 hello 솔루션을 사용 하는 다음 hello **컨테이너** 타일 컨테이너 호스트와 호스트에서 실행 되는 hello 컨테이너에 대 한 요약 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-385">After you have hello solution enabled in hello OMS portal, hello **Containers** tile shows summary information about your container hosts and hello containers running in hosts.</span></span>

![컨테이너 타일](./media/log-analytics-containers/containers-title.png)

<span data-ttu-id="24ab8-387">hello 타일 실행 중 또는 중지 된 hello 환경 및 실패 하는 여부에 있는 개수 컨테이너의 개요를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-387">hello tile shows an overview of how many containers you have in hello environment and whether they're failed, running, or stopped.</span></span>

### <a name="using-hello-containers-dashboard"></a><span data-ttu-id="24ab8-388">Hello 컨테이너 대시보드를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="24ab8-388">Using hello Containers dashboard</span></span>
<span data-ttu-id="24ab8-389">Hello 클릭 **컨테이너** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-389">Click hello **Containers** tile.</span></span> <span data-ttu-id="24ab8-390">여기에서는 다음에 따라 구성된 보기를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-390">From there you'll see views organized by:</span></span>

- <span data-ttu-id="24ab8-391">**컨테이너 이벤트** - 컨테이너 상태 및 실패한 컨테이너가 있는 컴퓨터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-391">**Container Events** - Shows container status and computers with failed containers.</span></span>
- <span data-ttu-id="24ab8-392">**컨테이너 로그** -로그 파일의 가장 높은 수 hello 사용 하 여 시간에 따른 컴퓨터의 목록을 생성 하는 컨테이너 로그 파일의 차트를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-392">**Container Logs** - Shows a chart of container log files generated over time and a list of computers with hello highest number of log files.</span></span>
- <span data-ttu-id="24ab8-393">**Kubernetes 이벤트** -시간 hello 원인은 포드 hello 이벤트를 생성 하는 원인에 따라 생성 된 Kubernetes 이벤트의 차트를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-393">**Kubernetes Events** - Shows a chart of Kubernetes events generated over time and a list of hello reasons why pods generated hello events.</span></span> <span data-ttu-id="24ab8-394">*이 데이터 집합은 Linux 환경에만 사용됩니다.*</span><span class="sxs-lookup"><span data-stu-id="24ab8-394">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="24ab8-395">**Kubernetes Namespace 인벤토리** -네임 스페이스 및 포드 hello 수를 표시 하 고 해당 계층을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-395">**Kubernetes Namespace Inventory** - Shows hello number of namespaces and pods and shows their hierarchy.</span></span> <span data-ttu-id="24ab8-396">*이 데이터 집합은 Linux 환경에만 사용됩니다.*</span><span class="sxs-lookup"><span data-stu-id="24ab8-396">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="24ab8-397">**컨테이너 노드 인벤토리** -컨테이너 노드/호스트에서 사용 되는 오케스트레이션 형식의 hello 수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-397">**Container Node Inventory** - Shows hello number of orchestration types used on container nodes/hosts.</span></span> <span data-ttu-id="24ab8-398">컨테이너의 hello 번호로 hello 컴퓨터 노드/호스트도 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-398">hello computer nodes/hosts are also listed by hello number of containers.</span></span> <span data-ttu-id="24ab8-399">*이 데이터 집합은 Linux 환경에만 사용됩니다.*</span><span class="sxs-lookup"><span data-stu-id="24ab8-399">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="24ab8-400">**컨테이너 이미지 인벤토리** -hello 사용 되는 컨테이너 이미지의 총 수와 이미지 형식의 수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-400">**Container Images Inventory** - Shows hello total number of container images used and number of image types.</span></span> <span data-ttu-id="24ab8-401">이미지의 hello 수 hello 이미지 태그로 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-401">hello number of images are also listed by hello image tag.</span></span>
- <span data-ttu-id="24ab8-402">**컨테이너 상태** -노드/호스트 컴퓨터를 실행 중인 컨테이너 hello 컨테이너의 총 수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-402">**Containers Status** - Shows hello total number of container nodes/host computers that have running containers.</span></span> <span data-ttu-id="24ab8-403">호스트를 실행 중인 hello 번호로 컴퓨터도 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-403">Computers are also listed by hello number of running hosts.</span></span>
- <span data-ttu-id="24ab8-404">**컨테이너 프로세스** - 시간에 따른 실행 중인 컨테이너 프로세스의 꺾은선형 차트를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-404">**Container Process** - Shows a line chart of container processes running over time.</span></span> <span data-ttu-id="24ab8-405">컨테이너는 컨테이너 내 실행 중인 명령/프로세스를 기준으로 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-405">Containers are also listed by running command/process within containers.</span></span> <span data-ttu-id="24ab8-406">*이 데이터 집합은 Linux 환경에만 사용됩니다.*</span><span class="sxs-lookup"><span data-stu-id="24ab8-406">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="24ab8-407">**컨테이너 CPU 성능** -hello 컴퓨터 노드/호스트에 대 한 시간에 따라 평균 CPU 사용률의 꺾은선형 차트를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-407">**Container CPU Performance** - Shows a line chart of hello average CPU utilization over time for computer nodes/hosts.</span></span> <span data-ttu-id="24ab8-408">또한 목록 hello 컴퓨터 노드/호스트 기반 평균 CPU 사용률입니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-408">Also lists hello computer nodes/hosts based on average CPU utilization.</span></span>
- <span data-ttu-id="24ab8-409">**컨테이너 메모리 성능** - 시간에 따른 메모리 사용량의 꺾은선형 차트를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-409">**Container Memory Performance** - Shows a line chart of memory usage over time.</span></span> <span data-ttu-id="24ab8-410">또한 인스턴스 이름을 기준으로 컴퓨터 메모리 사용률을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-410">Also lists computer memory utilization based on instance name.</span></span>
- <span data-ttu-id="24ab8-411">**컴퓨터 성능** -시간대 시간에 따른 CPU 성능의 hello % 꺾은선형 차트의 여유 디스크 공간이 메가바이트 고 시간에 따라 메모리 사용 백분율을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-411">**Computer Performance** - Shows line charts of hello percent of CPU performance over time, percent of memory usage over time, and megabytes of free disk space over time.</span></span> <span data-ttu-id="24ab8-412">자세한 내용을 보려면 차트 tooview에서 해당 줄 위로 가져가면 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-412">You can hover over any line in a chart tooview more details.</span></span>


<span data-ttu-id="24ab8-413">Hello 대시보드의 각 영역에 수집 된 데이터에서 실행 되는 검색의 시각적 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-413">Each area of hello dashboard is a visual representation of a search that is run on collected data.</span></span>

![컨테이너 대시보드 ](./media/log-analytics-containers/containers-dash01.png)

![컨테이너 대시보드 ](./media/log-analytics-containers/containers-dash02.png)

<span data-ttu-id="24ab8-416">Hello에 **컨테이너 상태** 영역에서 아래와 같이 hello 위쪽 영역을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-416">In hello **Container Status** area, click hello top area, as shown below.</span></span>

![컨테이너 상태](./media/log-analytics-containers/containers-status.png)

<span data-ttu-id="24ab8-418">사용자 컨테이너의 hello 상태에 관한 정보 표시 로그 검색이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-418">Log Search opens, displaying information about hello state of your containers.</span></span>

![컨테이너에 대한 로그 검색](./media/log-analytics-containers/containers-log-search.png)

<span data-ttu-id="24ab8-420">여기에서는 hello 검색 쿼리 toomodify를 편집할 수 있습니다이 toofind hello 특정 정보에 관심이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-420">From here, you can edit hello search query toomodify it toofind hello specific information you're interested in.</span></span> <span data-ttu-id="24ab8-421">로그 검색에 대한 자세한 내용은 [Log Analytics의 로그 검색](log-analytics-log-searches.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24ab8-421">For more information about Log Searches, see [Log searches in Log Analytics](log-analytics-log-searches.md).</span></span>

## <a name="troubleshoot-by-finding-a-failed-container"></a><span data-ttu-id="24ab8-422">실패한 컨테이너를 검색하여 문제 해결</span><span class="sxs-lookup"><span data-stu-id="24ab8-422">Troubleshoot by finding a failed container</span></span>

<span data-ttu-id="24ab8-423">0이 아닌 종료 코드로 종료된 경우 Log Analytics는 이 컨테이너를 **Failed**로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-423">Log Analytics marks a container as **Failed** if it has exited with a non-zero exit code.</span></span> <span data-ttu-id="24ab8-424">Hello 오류 및 실패 hello에 hello 환경에 대 한 개요를 확인할 수 있습니다 **실패 컨테이너** 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-424">You can see an overview of hello errors and failures in hello environment in hello **Failed Containers** area.</span></span>

### <a name="toofind-failed-containers"></a><span data-ttu-id="24ab8-425">toofind 컨테이너를 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-425">toofind failed containers</span></span>
1. <span data-ttu-id="24ab8-426">Hello 클릭 **컨테이너 상태** 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-426">Click hello **Container Status** area.</span></span>  
   <span data-ttu-id="24ab8-427">![컨테이너 상태](./media/log-analytics-containers/containers-status.png)</span><span class="sxs-lookup"><span data-stu-id="24ab8-427">![containers status](./media/log-analytics-containers/containers-status.png)</span></span>
2. <span data-ttu-id="24ab8-428">로그 검색 열리고 다음 유사한 toohello 컨테이너의 hello 상태가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-428">Log Search opens and displays hello state of your containers, similar toohello following.</span></span>  
   ![컨테이너 상태](./media/log-analytics-containers/containers-log-search.png)
3. <span data-ttu-id="24ab8-430">다음으로 실패 한 컨테이너 tooview 추가 정보의 hello 집계 값을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-430">Next, click hello aggregated value of failed containers tooview additional information.</span></span> <span data-ttu-id="24ab8-431">확장 **자세히 표시** tooview hello 이미지 id입니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-431">Expand **show more** tooview hello image ID.</span></span>  
   <span data-ttu-id="24ab8-432">![실패한 컨테이너](./media/log-analytics-containers/containers-state-failed.png)</span><span class="sxs-lookup"><span data-stu-id="24ab8-432">![failed containers](./media/log-analytics-containers/containers-state-failed.png)</span></span>  
4. <span data-ttu-id="24ab8-433">그런 다음 hello 검색 쿼리에서 hello 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-433">Next, type hello following in hello search query.</span></span> <span data-ttu-id="24ab8-434">`Type=ContainerInventory <ImageID>`중지 되 고 실패 한 이미지의 이미지 크기와 수 같은 hello 이미지에 대 한 세부 정보를 toosee 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-434">`Type=ContainerInventory <ImageID>` toosee details about hello image such as image size and number of stopped and failed images.</span></span>  
   <span data-ttu-id="24ab8-435">![실패한 컨테이너](./media/log-analytics-containers/containers-failed04.png)</span><span class="sxs-lookup"><span data-stu-id="24ab8-435">![failed containers](./media/log-analytics-containers/containers-failed04.png)</span></span>

## <a name="search-logs-for-container-data"></a><span data-ttu-id="24ab8-436">컨테이너 데이터에 대한 로그 검색</span><span class="sxs-lookup"><span data-stu-id="24ab8-436">Search logs for container data</span></span>
<span data-ttu-id="24ab8-437">특정 오류 문제를 해결 하는 경우 사용자 환경에서 발생 하는 toosee를 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-437">When you're troubleshooting a specific error, it can help toosee where it is occurring in your environment.</span></span> <span data-ttu-id="24ab8-438">로그 유형만 hello는 원하는 tooreturn hello 정보 쿼리를 작성 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-438">hello following log types will help you create queries tooreturn hello information you want.</span></span>


- <span data-ttu-id="24ab8-439">**ContainerImageInventory** – 이미지 Id 또는 크기와 같은 이미지와 tooview 이미지 정보로 구성 된 toofind 정보를 시도 하는 경우이 유형을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-439">**ContainerImageInventory** – Use this type when you're trying toofind information organized by image and tooview image information such as image IDs or sizes.</span></span>
- <span data-ttu-id="24ab8-440">**ContainerInventory** – 컨테이너 위치, 해당 컨테이너 이름, 실행 중인 이미지에 대한 정보가 필요할 때 이 유형을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-440">**ContainerInventory** – Use this type when you want information about container location, what their names are, and what images they're running.</span></span>
- <span data-ttu-id="24ab8-441">**ContainerLog** – toofind 특정 오류 로그 정보 및 항목을 원하는 경우이 유형을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-441">**ContainerLog** – Use this type when you want toofind specific error log information and entries.</span></span>
- <span data-ttu-id="24ab8-442">**ContainerNodeInventory_CL** 이 유형을 사용 호스트/노드에 대 한 hello 정보를 원하는 컨테이너 있는 됩니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-442">**ContainerNodeInventory_CL**  Use this type when you want hello information about host/node where containers are residing.</span></span> <span data-ttu-id="24ab8-443">Docker 버전, 오케스트레이션 형식, 저장소 및 네트워크 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-443">It provides you Docker version, orchestration type, storage, and network information.</span></span>
- <span data-ttu-id="24ab8-444">**ContainerProcess_CL** 사용 하 여가 형식 tooquickly hello 컨테이너 내에서 실행 하는 hello 프로세스를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="24ab8-444">**ContainerProcess_CL** Use this type tooquickly see hello process running within hello container.</span></span>
- <span data-ttu-id="24ab8-445">**ContainerServiceLog** – hello Docker 디먼을 시작, 예: 중지, 삭제 또는 끌어오기 명령에 대 한 toofind 감사 추적 정보를 시도 하는 경우이 유형을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-445">**ContainerServiceLog** – Use this type when you're trying toofind audit trail information for hello Docker daemon, such as start, stop, delete, or pull commands.</span></span>
- <span data-ttu-id="24ab8-446">**KubeEvents_CL** 이 형식의 toosee hello Kubernetes 이벤트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-446">**KubeEvents_CL**  Use this type toosee hello Kubernetes events.</span></span>
- <span data-ttu-id="24ab8-447">**KubePodInventory_CL** toounderstand hello 클러스터 계층 구조 정보를 원하는 경우이 유형을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-447">**KubePodInventory_CL**  Use this type when you want toounderstand hello cluster hierarchy information.</span></span>


### <a name="toosearch-logs-for-container-data"></a><span data-ttu-id="24ab8-448">컨테이너 데이터에 대 한 toosearch 로그</span><span class="sxs-lookup"><span data-stu-id="24ab8-448">toosearch logs for container data</span></span>
* <span data-ttu-id="24ab8-449">사용자가 알고 있는 이미지 최근에 실패 했습니다 및 hello 오류 로그에 대 한 찾기 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-449">Choose an image that you know has failed recently and find hello error logs for it.</span></span> <span data-ttu-id="24ab8-450">**ContainerInventory** 검색을 통해 해당 이미지를 실행 중인 컨테이너 이름부터 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-450">Start by finding a container name that is running that image with a **ContainerInventory** search.</span></span> <span data-ttu-id="24ab8-451">예를 들어, `Type=ContainerInventory ubuntu Failed`를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-451">For example, search for `Type=ContainerInventory ubuntu Failed`</span></span>  
    <span data-ttu-id="24ab8-452">![Ubuntu 컨테이너에 대한 검색](./media/log-analytics-containers/search-ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="24ab8-452">![Search for Ubuntu containers](./media/log-analytics-containers/search-ubuntu.png)</span></span>

  <span data-ttu-id="24ab8-453">hello 컨테이너의 이름 옆 너무 hello**이름**, 이러한 로그를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-453">hello name of hello container next too**Name**, and search for those logs.</span></span> <span data-ttu-id="24ab8-454">이 예제에서는 `Type=ContainerLog cranky_stonebreaker`입니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-454">In this example, it is `Type=ContainerLog cranky_stonebreaker`.</span></span>

<span data-ttu-id="24ab8-455">**성능 정보 보기**</span><span class="sxs-lookup"><span data-stu-id="24ab8-455">**View performance information**</span></span>

<span data-ttu-id="24ab8-456">Tooconstruct 쿼리를 시작 하는 경우 손쉽게 toosee 먼저 가능한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-456">When you're beginning tooconstruct queries, it can help toosee what's possible first.</span></span> <span data-ttu-id="24ab8-457">예를 들어 toosee 모든 성능 데이터, 시도 광범위 한 쿼리를 입력 하 여 hello 다음 검색 쿼리.</span><span class="sxs-lookup"><span data-stu-id="24ab8-457">For example, toosee all performance data, try a broad query by typing hello following search query.</span></span>

```
Type=Perf
```

![컨테이너 성능](./media/log-analytics-containers/containers-perf01.png)

<span data-ttu-id="24ab8-459">표시 되는 tooa 특정 컨테이너의 hello 이름을 입력 하 여 쿼리의 오른쪽 toohello hello 성능 데이터 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-459">You can scope hello performance data you're seeing tooa specific container by typing hello name of it toohello right of your query.</span></span>

```
Type=Perf <containerName>
```

<span data-ttu-id="24ab8-460">개별 컨테이너에 대해 수집 되는 성능 메트릭에 hello 목록을 표시를 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-460">That shows hello list of performance metrics that are collected for an individual container.</span></span>

![컨테이너 성능](./media/log-analytics-containers/containers-perf03.png)

## <a name="example-log-search-queries"></a><span data-ttu-id="24ab8-462">로그 검색 쿼리 예제</span><span class="sxs-lookup"><span data-stu-id="24ab8-462">Example log search queries</span></span>
<span data-ttu-id="24ab8-463">종종 유용한 toobuild 사용자 환경 또는 예 2부터 다음 toofit 수정 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-463">It's often useful toobuild queries starting with an example or two and then modifying them toofit your environment.</span></span> <span data-ttu-id="24ab8-464">시작 지점으로 hello로 실험 **샘플 쿼리** 영역 toohelp 보다 고급 수준의 쿼리를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-464">As a starting point, you can experiment with hello **Sample Queries** area toohelp you build more advanced queries.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![컨테이너 쿼리](./media/log-analytics-containers/containers-queries.png)


## <a name="saving-log-search-queries"></a><span data-ttu-id="24ab8-466">로그 검색 쿼리 저장</span><span class="sxs-lookup"><span data-stu-id="24ab8-466">Saving log search queries</span></span>
<span data-ttu-id="24ab8-467">쿼리 저장은 Log Analytics의 표준 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-467">Saving queries is a standard feature in Log Analytics.</span></span> <span data-ttu-id="24ab8-468">이를 저장해 두면 향후 유용하게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-468">By saving them, you'll have those that you've found useful handy for future use.</span></span>

<span data-ttu-id="24ab8-469">유용한 쿼리를 만든 후 클릭 하 여 저장 **즐겨찾기** hello hello 로그 검색 페이지 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-469">After you create a query that you find useful, save it by clicking **Favorites** at hello top of hello Log Search page.</span></span> <span data-ttu-id="24ab8-470">쉽게 액세스할 수 나중 hello에서 다음 **내 대시보드** 페이지.</span><span class="sxs-lookup"><span data-stu-id="24ab8-470">Then you can easily access it later from hello **My Dashboard** page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24ab8-471">다음 단계</span><span class="sxs-lookup"><span data-stu-id="24ab8-471">Next steps</span></span>
* <span data-ttu-id="24ab8-472">[로그 검색](log-analytics-log-searches.md) tooview 컨테이너 데이터 레코드를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="24ab8-472">[Search logs](log-analytics-log-searches.md) tooview detailed container data records.</span></span>
