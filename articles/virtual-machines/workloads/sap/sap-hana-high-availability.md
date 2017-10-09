---
title: "aaaHigh 가용성의 SAP HANA Azure 가상 컴퓨터 (Vm)에서 | Microsoft Docs"
description: "Azure VM(Virtual Machines)에서 SAP HANA 고가용성을 설정합니다."
services: virtual-machines-linux
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: sedusch
ms.openlocfilehash: dcb9bb70594f9d97f8a888cec76300bcbe0bf1ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-sap-hana-on-azure-virtual-machines-vms"></a><span data-ttu-id="fff98-103">Azure VM(Virtual Machines)의 SAP HANA 고가용성</span><span class="sxs-lookup"><span data-stu-id="fff98-103">High Availability of SAP HANA on Azure Virtual Machines (VMs)</span></span>

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

[2205917]:https://launchpad.support.sap.com/#/notes/2205917
[1944799]:https://launchpad.support.sap.com/#/notes/1944799
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351

[hana-ha-guide-replication]:sap-hana-high-availability.md#14c19f65-b5aa-4856-9594-b81c7e4df73d
[hana-ha-guide-shared-storage]:sap-hana-high-availability.md#498de331-fa04-490b-997c-b078de457c9d

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[sap-swcenter]:https://launchpad.support.sap.com/#/softwarecenter
[template-multisid-db]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged%2Fazuredeploy.json

<span data-ttu-id="fff98-113">온-프레미스에 두 HANA 시스템 복제를 사용 하거나 SAP HANA에 대 한 공유 저장소 tooestablish 고가용성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-113">On-premises, you can use either HANA System Replication or use shared storage tooestablish high availability for SAP HANA.</span></span>
<span data-ttu-id="fff98-114">현재로서는 Azure에서 HANA 시스템 복제 설정만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-114">We currently only support setting up HANA System Replication on Azure.</span></span> <span data-ttu-id="fff98-115">SAP HANA 복제는 하나의 마스터 노드와 하나 이상의 슬레이브 노드로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-115">SAP HANA Replication consists of one master node and at least one slave node.</span></span> <span data-ttu-id="fff98-116">변경 내용을 toohello hello 마스터 노드는 데이터는 동기적 또는 비동기적으로 toohello 슬레이브 노드를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-116">Changes toohello data on hello master node are replicated toohello slave nodes synchronously or asynchronously.</span></span>

<span data-ttu-id="fff98-117">이 문서에서는 어떻게 toodeploy hello 가상 컴퓨터 hello 가상 컴퓨터 구성, hello 클러스터 프레임 워크를 설치, 설치 및 구성 SAP HANA 시스템 복제 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-117">This article describes how toodeploy hello virtual machines, configure hello virtual machines, install hello cluster framework, install and configure SAP HANA System Replication.</span></span>
<span data-ttu-id="fff98-118">Hello 예제 구성에서는 설치 등 인스턴스 번호 03 명령과 HANA 시스템 ID HDB 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-118">In hello example configurations, installation commands etc. instance number 03 and HANA System ID HDB is used.</span></span>

<span data-ttu-id="fff98-119">SAP Note와 문서를 먼저 다음 읽기 hello</span><span class="sxs-lookup"><span data-stu-id="fff98-119">Read hello following SAP Notes and papers first</span></span>

* <span data-ttu-id="fff98-120">SAP Note [1928533], 다음 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-120">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="fff98-121">Hello SAP 소프트웨어 배포에 지원 되는 Azure VM 크기의 목록</span><span class="sxs-lookup"><span data-stu-id="fff98-121">List of Azure VM sizes that are supported for hello deployment of SAP software</span></span>
  * <span data-ttu-id="fff98-122">Azure VM 크기에 대한 중요한 용량 정보</span><span class="sxs-lookup"><span data-stu-id="fff98-122">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="fff98-123">지원되는 SAP 소프트웨어 및 운영 체제(OS)와 데이터베이스 조합</span><span class="sxs-lookup"><span data-stu-id="fff98-123">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="fff98-124">Microsoft Azure에서 Windows 및 Linux에 필요한 SAP 커널 버전</span><span class="sxs-lookup"><span data-stu-id="fff98-124">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>
* <span data-ttu-id="fff98-125">SAP Note [2015553]는 Azure에서 SAP을 지원하는 SAP 소프트웨어 배포에 대한 필수 구성 요소를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-125">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="fff98-126">SAP Note [2205917]에는 SAP 응용 프로그램용 SUSE Linux Enterprise Server에 권장되는 OS 설정이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-126">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="fff98-127">SAP Note [1944799]에는 SAP 응용 프로그램용 SUSE Linux Enterprise Server에 대한 SAP HANA 지침이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-127">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="fff98-128">SAP Note [2178632]는 Azure에서 SAP에 대해 보고된 모든 모니터링 메트릭에 대한 자세한 정보를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-128">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="fff98-129">SAP Note [2191498] hello 필요한 SAP 호스트 에이전트 버전 Azure에서 Linux에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-129">SAP Note [2191498] has hello required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="fff98-130">SAP Note [2243692]는 Azure에서 Linux의 SAP 라이선스에 대한 정보를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-130">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="fff98-131">SAP Note [1984787]은 SUSE LINUX Enterprise Server 12에 대한 일반 정보를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-131">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="fff98-132">SAP Note [1999351] Azure 고급 모니터링 확장의 SAP 용 hello에 대 한 추가 문제 해결 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-132">SAP Note [1999351] has additional troubleshooting information for hello Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="fff98-133">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes)는 Linux에 필요한 모든 SAP Note를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-133">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="fff98-134">[Linux에서 SAP용 Azure Virtual Machines 계획 및 구현][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="fff98-134">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="fff98-135">[Linux에서 SAP용 Azure Virtual Machines 배포(이 문서)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="fff98-135">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="fff98-136">[Linux에서 SAP용 Azure Virtual Machines DBMS 배포][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="fff98-136">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="fff98-137">[SAP HANA SR 성능에 최적화 된 시나리오] [ suse-hana-ha-guide] 온-프레미스 SAP HANA 시스템 복제를 모든 필요한 정보 tooset hello 가이드에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-137">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide] hello guide contains all required information tooset up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="fff98-138">이 가이드를 기준으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-138">Use this guide as a baseline.</span></span>

## <a name="deploying-linux"></a><span data-ttu-id="fff98-139">Linux 배포</span><span class="sxs-lookup"><span data-stu-id="fff98-139">Deploying Linux</span></span>

<span data-ttu-id="fff98-140">SAP HANA에 대 한 hello 리소스 에이전트는 SAP 응용 프로그램에 대 한 SUSE Linux Enterprise Server에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-140">hello resource agent for SAP HANA is included in SUSE Linux Enterprise Server for SAP Applications.</span></span>
<span data-ttu-id="fff98-141">Azure 마켓플레이스 hello BYOS (Bring Your 자신의 구독의) toodeploy 새 가상 컴퓨터를 사용할 수 있는 경우 SAP 응용 프로그램 12에 대 한 SUSE Linux Enterprise Server에 대 한 이미지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-141">hello Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 with BYOS (Bring Your Own Subscription) that you can use toodeploy new virtual machines.</span></span>

### <a name="manual-deployment"></a><span data-ttu-id="fff98-142">수동 배포</span><span class="sxs-lookup"><span data-stu-id="fff98-142">Manual Deployment</span></span>

1. <span data-ttu-id="fff98-143">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="fff98-143">Create a Resource Group</span></span>
1. <span data-ttu-id="fff98-144">Virtual Network 만들기</span><span class="sxs-lookup"><span data-stu-id="fff98-144">Create a Virtual Network</span></span>
1. <span data-ttu-id="fff98-145">두 개의 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="fff98-145">Create two Storage Accounts</span></span>
1. <span data-ttu-id="fff98-146">가용성 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="fff98-146">Create an Availability Set</span></span>  
   <span data-ttu-id="fff98-147">최대 업데이트 도메인 설정</span><span class="sxs-lookup"><span data-stu-id="fff98-147">Set max update domain</span></span>
1. <span data-ttu-id="fff98-148">부하 분산 장치(내부) 만들기</span><span class="sxs-lookup"><span data-stu-id="fff98-148">Create a Load Balancer (internal)</span></span>  
   <span data-ttu-id="fff98-149">위의 VNET 단계 선택</span><span class="sxs-lookup"><span data-stu-id="fff98-149">Select VNET of step above</span></span>
1. <span data-ttu-id="fff98-150">가상 컴퓨터 1 만들기</span><span class="sxs-lookup"><span data-stu-id="fff98-150">Create Virtual Machine 1</span></span>  
   <span data-ttu-id="fff98-151">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span><span class="sxs-lookup"><span data-stu-id="fff98-151">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="fff98-152">SAP 응용 프로그램 12 SP1용 SLES(BYOS)</span><span class="sxs-lookup"><span data-stu-id="fff98-152">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="fff98-153">저장소 계정 1 선택</span><span class="sxs-lookup"><span data-stu-id="fff98-153">Select Storage Account 1</span></span>  
   <span data-ttu-id="fff98-154">가용성 집합 선택</span><span class="sxs-lookup"><span data-stu-id="fff98-154">Select Availability Set</span></span>  
1. <span data-ttu-id="fff98-155">가상 컴퓨터 2 만들기</span><span class="sxs-lookup"><span data-stu-id="fff98-155">Create Virtual Machine 2</span></span>  
   <span data-ttu-id="fff98-156">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span><span class="sxs-lookup"><span data-stu-id="fff98-156">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="fff98-157">SAP 응용 프로그램 12 SP1용 SLES(BYOS)</span><span class="sxs-lookup"><span data-stu-id="fff98-157">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="fff98-158">저장소 계정 2 선택</span><span class="sxs-lookup"><span data-stu-id="fff98-158">Select Storage Account 2</span></span>   
   <span data-ttu-id="fff98-159">가용성 집합 선택</span><span class="sxs-lookup"><span data-stu-id="fff98-159">Select Availability Set</span></span>  
1. <span data-ttu-id="fff98-160">데이터 디스크 추가</span><span class="sxs-lookup"><span data-stu-id="fff98-160">Add Data Disks</span></span>
1. <span data-ttu-id="fff98-161">Hello 부하 분산 장치 구성</span><span class="sxs-lookup"><span data-stu-id="fff98-161">Configure hello load balancer</span></span>
    1. <span data-ttu-id="fff98-162">프런트 엔드 IP 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="fff98-162">Create a frontend IP pool</span></span>
        1. <span data-ttu-id="fff98-163">열기 hello 부하 분산 장치 프런트 엔드 IP 풀을 선택 하 고 추가 클릭</span><span class="sxs-lookup"><span data-stu-id="fff98-163">Open hello load balancer, select frontend IP pool and click Add</span></span>
        1. <span data-ttu-id="fff98-164">Hello 새 프런트 엔드 IP 풀 (예를 들어 hana-프런트 엔드) hello 이름 입력</span><span class="sxs-lookup"><span data-stu-id="fff98-164">Enter hello name of hello new frontend IP pool (for example hana-frontend)</span></span>
       1. <span data-ttu-id="fff98-165">확인 클릭</span><span class="sxs-lookup"><span data-stu-id="fff98-165">Click OK</span></span>
        1. <span data-ttu-id="fff98-166">Hello 새 프런트 엔드 IP 풀을 만든 후 해당 IP 주소를 적어 둡니다</span><span class="sxs-lookup"><span data-stu-id="fff98-166">After hello new frontend IP pool is created, write down its IP address</span></span>
    1. <span data-ttu-id="fff98-167">백 엔드 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="fff98-167">Create a backend pool</span></span>
        1. <span data-ttu-id="fff98-168">열기 hello 부하 분산 장치 백 엔드 풀을 선택 하 고 추가 클릭</span><span class="sxs-lookup"><span data-stu-id="fff98-168">Open hello load balancer, select backend pools and click Add</span></span>
        1. <span data-ttu-id="fff98-169">Hello 새 백 엔드 풀 (예를 들어 hana-백 엔드) hello 이름 입력</span><span class="sxs-lookup"><span data-stu-id="fff98-169">Enter hello name of hello new backend pool (for example hana-backend)</span></span>
        1. <span data-ttu-id="fff98-170">가상 컴퓨터 추가 클릭</span><span class="sxs-lookup"><span data-stu-id="fff98-170">Click Add a virtual machine</span></span>
        1. <span data-ttu-id="fff98-171">Hello 앞에서 만든 가용성 집합 선택</span><span class="sxs-lookup"><span data-stu-id="fff98-171">Select hello Availability Set you created earlier</span></span>
        1. <span data-ttu-id="fff98-172">Hello SAP HANA 클러스터의 hello 가상 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-172">Select hello virtual machines of hello SAP HANA cluster</span></span>
        1. <span data-ttu-id="fff98-173">확인 클릭</span><span class="sxs-lookup"><span data-stu-id="fff98-173">Click OK</span></span>
    1. <span data-ttu-id="fff98-174">상태 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="fff98-174">Create a health probe</span></span>
       1. <span data-ttu-id="fff98-175">열기 hello 부하 분산 장치 상태 프로브를 선택 하 고 추가 클릭</span><span class="sxs-lookup"><span data-stu-id="fff98-175">Open hello load balancer, select health probes and click Add</span></span>
        1. <span data-ttu-id="fff98-176">Hello 새 상태 프로브 (예: hana-hp) hello 이름 입력</span><span class="sxs-lookup"><span data-stu-id="fff98-176">Enter hello name of hello new health probe (for example hana-hp)</span></span>
        1. <span data-ttu-id="fff98-177">프로토콜로 TCP를 선택하고 포트 625**03**을 선택한 다음 간격은 5, 비정상 임계값은 2로 유지</span><span class="sxs-lookup"><span data-stu-id="fff98-177">Select TCP as protocol, port 625**03**, keep Interval 5 and Unhealthy threshold 2</span></span>
        1. <span data-ttu-id="fff98-178">확인 클릭</span><span class="sxs-lookup"><span data-stu-id="fff98-178">Click OK</span></span>
    1. <span data-ttu-id="fff98-179">부하 분산 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="fff98-179">Create load balancing rules</span></span>
        1. <span data-ttu-id="fff98-180">Hello 부하 분산 장치 부하 분산 규칙 찾아서 추가 클릭</span><span class="sxs-lookup"><span data-stu-id="fff98-180">Open hello load balancer, select load balancing rules and click Add</span></span>
        1. <span data-ttu-id="fff98-181">Hello hello 새 부하 분산 장치 규칙 이름 입력 (예: hana-lb-3**03**15)</span><span class="sxs-lookup"><span data-stu-id="fff98-181">Enter hello name of hello new load balancer rule (for example hana-lb-3**03**15)</span></span>
        1. <span data-ttu-id="fff98-182">선택 hello 프런트 엔드 IP 주소, 백 엔드 풀 및 상태 프로브 하면 이전에 만든 (예를 들어 hana-프런트 엔드)</span><span class="sxs-lookup"><span data-stu-id="fff98-182">Select hello frontend IP address, backend pool and health probe you created earlier (for example hana-frontend)</span></span>
        1. <span data-ttu-id="fff98-183">프로토콜 TCP를 유지하고 포트 3**03**15 입력</span><span class="sxs-lookup"><span data-stu-id="fff98-183">Keep protocol TCP, enter port 3**03**15</span></span>
        1. <span data-ttu-id="fff98-184">Too30 분 유휴 시간 제한 증가</span><span class="sxs-lookup"><span data-stu-id="fff98-184">Increase idle timeout too30 minutes</span></span>
       1. <span data-ttu-id="fff98-185">**Tooenable 있는지를 확인 합니다. 부동 IP**</span><span class="sxs-lookup"><span data-stu-id="fff98-185">**Make sure tooenable Floating IP**</span></span>
        1. <span data-ttu-id="fff98-186">확인 클릭</span><span class="sxs-lookup"><span data-stu-id="fff98-186">Click OK</span></span>
        1. <span data-ttu-id="fff98-187">포트 3에 대 한 위의 hello 단계를 반복**03**17</span><span class="sxs-lookup"><span data-stu-id="fff98-187">Repeat hello steps above for port 3**03**17</span></span>

### <a name="deploy-with-template"></a><span data-ttu-id="fff98-188">템플릿을 사용하여 배포</span><span class="sxs-lookup"><span data-stu-id="fff98-188">Deploy with template</span></span>
<span data-ttu-id="fff98-189">사용할 수 있습니다 hello 빠른 시작 템플릿 중 하나에 github toodeploy 필요한 모든 리소스.</span><span class="sxs-lookup"><span data-stu-id="fff98-189">You can use one of hello quick start templates on github toodeploy all required resources.</span></span> <span data-ttu-id="fff98-190">hello 템플릿 hello 가상 컴퓨터, hello 부하 분산 장치, 가용성 집합 등을 배포 합니다. 이러한 단계 toodeploy hello 서식 파일을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-190">hello template deploys hello virtual machines, hello load balancer, availability set etc. Follow these steps toodeploy hello template:</span></span>

1. <span data-ttu-id="fff98-191">열기 hello [데이터베이스 템플릿을] [ template-multisid-db] 또는 hello [템플릿 수렴] [ template-converged] hello Azure 포털에 hello 데이터베이스 템플릿은 만듭니다 hello 데이터베이스에 대 한 부하 분산 규칙 hello 수렴 형된 템플릿도 만듭니다. 반면 hello 부하 분산 규칙 ASCS/SCS 및 호출자 (Linux에만 해당) 인스턴스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-191">Open hello [database template][template-multisid-db] or hello [converged template][template-converged] on hello Azure Portal hello database template only creates hello load-balancing rules for a database whereas hello converged template also creates hello load-balancing rules for an ASCS/SCS and ERS (Linux only) instance.</span></span> <span data-ttu-id="fff98-192">Tooinstall SAP NetWeaver 기반 시스템을 계획 하 고 싶다면 tooinstall hello ASCS/SCS 인스턴스에 경우 hello에 동일한 컴퓨터를 사용 하 여 hello [템플릿 수렴 형][template-converged]합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-192">If you plan tooinstall an SAP NetWeaver based system and you also want tooinstall hello ASCS/SCS instance on hello same machines, use hello [converged template][template-converged].</span></span>
1. <span data-ttu-id="fff98-193">Hello 매개 변수 뒤에 입력</span><span class="sxs-lookup"><span data-stu-id="fff98-193">Enter hello following parameters</span></span>
    1. <span data-ttu-id="fff98-194">SAP 시스템 ID -</span><span class="sxs-lookup"><span data-stu-id="fff98-194">Sap System Id</span></span>  
       <span data-ttu-id="fff98-195">Hello tooinstall 원하는 SAP 시스템의 hello SAP 시스템 Id를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-195">Enter hello SAP system Id of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="fff98-196">hello Id는 배포 된 hello 리소스에 대 한 접두사로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-196">hello Id will be used as a prefix for hello resources that are deployed.</span></span>
    1. <span data-ttu-id="fff98-197">스택 형식 (hello 수렴 형된 서식 파일을 사용 하는 경우에 해당)</span><span class="sxs-lookup"><span data-stu-id="fff98-197">Stack Type (only applicable if you use hello converged template)</span></span>  
       <span data-ttu-id="fff98-198">Hello SAP NetWeaver 스택 유형 선택</span><span class="sxs-lookup"><span data-stu-id="fff98-198">Select hello SAP NetWeaver stack type</span></span>
    1. <span data-ttu-id="fff98-199">OS 종류 -</span><span class="sxs-lookup"><span data-stu-id="fff98-199">Os Type</span></span>  
       <span data-ttu-id="fff98-200">Hello Linux 배포 사항 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-200">Select one of hello Linux distributions.</span></span> <span data-ttu-id="fff98-201">이 예에서는 SLES 12 BYOS 선택</span><span class="sxs-lookup"><span data-stu-id="fff98-201">For this example, select SLES 12 BYOS</span></span>
    1. <span data-ttu-id="fff98-202">Db 형식</span><span class="sxs-lookup"><span data-stu-id="fff98-202">Db Type</span></span>  
       <span data-ttu-id="fff98-203">HANA 선택</span><span class="sxs-lookup"><span data-stu-id="fff98-203">Select HANA</span></span>
    1. <span data-ttu-id="fff98-204">SAP 시스템 크기 -</span><span class="sxs-lookup"><span data-stu-id="fff98-204">Sap System Size</span></span>  
       <span data-ttu-id="fff98-205">hello 양을 SAPS hello 새 시스템을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-205">hello amount of SAPS hello new system will provide.</span></span> <span data-ttu-id="fff98-206">SAP 기술 파트너 나 시스템 통합 업체에 문의 개수 SAPS hello 시스템 내용의 확실 하지 않은 경우</span><span class="sxs-lookup"><span data-stu-id="fff98-206">If you are not sure how many SAPS hello system will require, please ask your SAP Technology Partner or System Integrator</span></span>
    1. <span data-ttu-id="fff98-207">시스템 가용성 -</span><span class="sxs-lookup"><span data-stu-id="fff98-207">System Availability</span></span>  
       <span data-ttu-id="fff98-208">HA를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-208">Select HA</span></span>
    1. <span data-ttu-id="fff98-209">관리자 사용자 이름 및 관리자 암호 -</span><span class="sxs-lookup"><span data-stu-id="fff98-209">Admin Username and Admin Password</span></span>  
       <span data-ttu-id="fff98-210">새 사용자를 만들가 toohello 컴퓨터에서 사용 되는 toolog 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-210">A new user is created that can be used toolog on toohello machine.</span></span>
    1. <span data-ttu-id="fff98-211">기존 또는 새 서브넷 -</span><span class="sxs-lookup"><span data-stu-id="fff98-211">New Or Existing Subnet</span></span>  
       <span data-ttu-id="fff98-212">새 가상 네트워크와 서브넷을 만들어야 하는지 또는 기존 서브넷을 사용해야 하는지 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-212">Determines whether a new virtual network and subnet should be created or an existing subnet should be used.</span></span> <span data-ttu-id="fff98-213">가상 네트워크는 연결 된 tooyour 온-프레미스 네트워크를 이미 있는 경우 기존 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-213">If you already have a virtual network that is connected tooyour on-premises network, select existing.</span></span>
    1. <span data-ttu-id="fff98-214">서브넷 ID -</span><span class="sxs-lookup"><span data-stu-id="fff98-214">Subnet Id</span></span>  
    <span data-ttu-id="fff98-215">hello 서브넷 toowhich hello 가상 컴퓨터의 hello ID에 연결 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-215">hello ID of hello subnet toowhich hello virtual machines should be connected to.</span></span> <span data-ttu-id="fff98-216">VPN 또는 Express 경로 가상 네트워크 tooconnect hello 가상 컴퓨터 tooyour 온-프레미스 네트워크의 서브넷을 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-216">Select hello subnet of your VPN or Express Route virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="fff98-217">hello ID는 일반적으로 /subscriptions/ 처럼 보이는`<subscription id`> /resourceGroups/`<resource group name`> /providers/Microsoft.Network/virtualNetworks/`<virtual network name`> /subnets/`<subnet name`></span><span class="sxs-lookup"><span data-stu-id="fff98-217">hello ID usually looks like /subscriptions/`<subscription id`>/resourceGroups/`<resource group name`>/providers/Microsoft.Network/virtualNetworks/`<virtual network name`>/subnets/`<subnet name`></span></span>

## <a name="setting-up-linux-ha"></a><span data-ttu-id="fff98-218">Linux HA 설정</span><span class="sxs-lookup"><span data-stu-id="fff98-218">Setting up Linux HA</span></span>

<span data-ttu-id="fff98-219">다음 항목 hello에 대 한 접두사로 사용 하거나 [A]-[1]-1 또는 [2]에 적용할 수 toonode-에 적용할 수 toonode 2, 해당 tooall 노드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-219">hello following items are prefixed with either [A] - applicable tooall nodes, [1] - only applicable toonode 1 or [2] - only applicable toonode 2.</span></span>

1. <span data-ttu-id="fff98-220">[A] SLES SAP BYOS 전용-등록 SLES toobe 수 toouse hello 저장소에 대 한</span><span class="sxs-lookup"><span data-stu-id="fff98-220">[A] SLES for SAP BYOS only - Register SLES toobe able toouse hello repositories</span></span>
1. <span data-ttu-id="fff98-221">[A] SLES for SAP BYOS 전용 - 공개 클라우드 모듈 추가</span><span class="sxs-lookup"><span data-stu-id="fff98-221">[A] SLES for SAP BYOS only - Add public-cloud module</span></span>
1. <span data-ttu-id="fff98-222">[A] SLES 업데이트</span><span class="sxs-lookup"><span data-stu-id="fff98-222">[A] Update SLES</span></span>
    ```bash
    sudo zypper update

    ```

1. <span data-ttu-id="fff98-223">[1] ssh 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="fff98-223">[1] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key
    sudo cat /root/.ssh/id_dsa.pub
    ```

2. <span data-ttu-id="fff98-224">[2] ssh 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="fff98-224">[2] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa

    # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
    sudo vi /root/.ssh/authorized_keys
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key    
    sudo cat /root/.ssh/id_dsa.pub
    ```

1. <span data-ttu-id="fff98-225">[1] ssh 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="fff98-225">[1] Enable ssh access</span></span>
    ```bash
    # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
    sudo vi /root/.ssh/authorized_keys
    
    ```

1. <span data-ttu-id="fff98-226">[A] HA 확장 설치</span><span class="sxs-lookup"><span data-stu-id="fff98-226">[A] Install HA extension</span></span>
    ```bash
    sudo zypper install sle-ha-release fence-agents
    
    ```

1. <span data-ttu-id="fff98-227">[A] 설치 디스크 레이아웃</span><span class="sxs-lookup"><span data-stu-id="fff98-227">[A] Setup disk layout</span></span>
    1. <span data-ttu-id="fff98-228">LVM</span><span class="sxs-lookup"><span data-stu-id="fff98-228">LVM</span></span>  
    <span data-ttu-id="fff98-229">일반적으로 로그 파일 및 데이터를 저장 하는 볼륨에 대 한 LVM toouse를 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-229">We generally recommend toouse LVM for volumes that store data and log files.</span></span> <span data-ttu-id="fff98-230">아래 예제에서는 hello 하려면 네 개의 연결 된 데이터 디스크 두 개의 볼륨을 사용 하는 toocreate 되어야 하는 hello 가상 컴퓨터에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-230">hello example below assumes that hello virtual machines have four data disks attached that should be used toocreate two volumes.</span></span>
        * <span data-ttu-id="fff98-231">Toouse 되도록 하는 모든 디스크에 대 한 실제 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-231">Create physical volumes for all disks that you want toouse.</span></span>
    <pre><code>
    sudo pvcreate /dev/sdc
    sudo pvcreate /dev/sdd
    sudo pvcreate /dev/sde
    sudo pvcreate /dev/sdf
    </code></pre>
        * <span data-ttu-id="fff98-232">Hello 데이터 파일에 대 한 볼륨 그룹, hello 로그 파일에 대 한 하나의 볼륨 그룹 및 SAP HANA의 hello 공유 디렉터리에 대 한 만들기</span><span class="sxs-lookup"><span data-stu-id="fff98-232">Create a volume group for hello data files, one volume group for hello log files and one for hello shared directory of SAP HANA</span></span>
    <pre><code>
    sudo vgcreate vg_hana_data /dev/sdc /dev/sdd
    sudo vgcreate vg_hana_log /dev/sde
    sudo vgcreate vg_hana_shared /dev/sdf
    </code></pre>
        * <span data-ttu-id="fff98-233">Hello 논리 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-233">Create hello logical volumes</span></span>
    <pre><code>
    sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
    sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
    sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
    sudo mkfs.xfs /dev/vg_hana_data/hana_data
    sudo mkfs.xfs /dev/vg_hana_log/hana_log
    sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
    </code></pre>
        * <span data-ttu-id="fff98-234">Hello 탑재 디렉터리를 만들고 hello 모든 논리 볼륨의 UUID를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-234">Create hello mount directories and copy hello UUID of all logical volumes</span></span>
    <pre><code>
    sudo mkdir -p /hana/data
    sudo mkdir -p /hana/log
    sudo mkdir -p /hana/shared
    # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
    sudo blkid
    </code></pre>
        * <span data-ttu-id="fff98-235">논리 볼륨이 3 개씩 hello에 대 한 fstab 항목 만들기</span><span class="sxs-lookup"><span data-stu-id="fff98-235">Create fstab entries for hello three logical volumes</span></span>
    <pre><code>
    sudo vi /etc/fstab
    </code></pre>
    <span data-ttu-id="fff98-236">이 줄 너무/등/fstab 삽입</span><span class="sxs-lookup"><span data-stu-id="fff98-236">Insert this line too/etc/fstab</span></span>
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b> /hana/data xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b> /hana/log xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b> /hana/shared xfs  defaults,nofail  0  2
    </code></pre>
        * <span data-ttu-id="fff98-237">Hello 새 볼륨을 탑재</span><span class="sxs-lookup"><span data-stu-id="fff98-237">Mount hello new volumes</span></span>
    <pre><code>
    sudo mount -a
    </code></pre>
    1. <span data-ttu-id="fff98-238">일반 디스크</span><span class="sxs-lookup"><span data-stu-id="fff98-238">Plain Disks</span></span>  
       <span data-ttu-id="fff98-239">소규모 또는 데모 시스템용으로 한 디스크에 HANA 데이터와 로그 파일을 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-239">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="fff98-240">hello 다음 /dev/sdc에 파티션을 만들고 명령과 xfs로 포맷 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-240">hello following commands create a partition on /dev/sdc and format it with xfs.</span></span>
    ```bash
    sudo fdisk /dev/sdc
    sudo mkfs.xfs /dev/sdc1
    
    # <a name="write-down-hello-id-of-devsdc1"></a><span data-ttu-id="fff98-241">/dev/sdc1의 hello id 기록</span><span class="sxs-lookup"><span data-stu-id="fff98-241">write down hello id of /dev/sdc1</span></span>
    <span data-ttu-id="fff98-242">sudo /sbin/blkid  sudo vi /etc/fstab</span><span class="sxs-lookup"><span data-stu-id="fff98-242">sudo /sbin/blkid  sudo vi /etc/fstab</span></span>
    ```

    Insert this line too/etc/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID&gt;</b> /hana xfs  defaults,nofail  0  2
    </code></pre>

    Create hello target directory and mount hello disk.

    ```bash
    sudo mkdir /hana
    sudo mount -a
    ```

1. <span data-ttu-id="fff98-243">[A] 모든 호스트의 호스트 이름 확인 설정</span><span class="sxs-lookup"><span data-stu-id="fff98-243">[A] Setup host name resolution for all hosts</span></span>  
    <span data-ttu-id="fff98-244">DNS 서버를 사용 하거나 모든 노드에서 hello /etc/hosts 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-244">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="fff98-245">이 예제에서는 toouse /etc/hosts 파일 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-245">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="fff98-246">Hello IP 주소와 hello 명령 뒤에 hello 호스트 이름 바꾸기</span><span class="sxs-lookup"><span data-stu-id="fff98-246">Replace hello IP address and hello hostname in hello following commands</span></span>
    ```bash
    sudo vi /etc/hosts
    ```
    <span data-ttu-id="fff98-247">다음 줄 너무/등/호스트 hello를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-247">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="fff98-248">IP 주소 및 호스트 이름 toomatch hello 환경 변경</span><span class="sxs-lookup"><span data-stu-id="fff98-248">Change hello IP address and hostname toomatch your environment</span></span>    
    
    <pre><code>
    <b>&lt;IP address of host 1&gt; &lt;hostname of host 1&gt;</b>
    <b>&lt;IP address of host 2&gt; &lt;hostname of host 2&gt;</b>
    </code></pre>

1. <span data-ttu-id="fff98-249">[1] 클러스터 설치</span><span class="sxs-lookup"><span data-stu-id="fff98-249">[1] Install Cluster</span></span>
    ```bash
    sudo ha-cluster-init
    
    # Do you want toocontinue anyway? [y/N] -> y
    # Network address toobind too(e.g.: 192.168.1.0) [10.79.227.0] -> ENTER
    # Multicast address (e.g.: 239.x.x.x) [239.174.218.125] -> ENTER
    # Multicast port [5405] -> ENTER
    # Do you wish toouse SBD? [y/N] -> N
    # Do you wish tooconfigure an administration IP? [y/N] -> N
    ```
        
1. <span data-ttu-id="fff98-250">[2] toocluster 노드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-250">[2] Add node toocluster</span></span>
    ```bash
    sudo ha-cluster-join
        
    # WARNING: NTP is not configured toostart at system boot.
    # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
    # Do you want toocontinue anyway? [y/N] -> y
    # IP address or hostname of existing node (e.g.: 192.168.1.1) [] -> IP address of node 1 e.g. 10.0.0.5
    # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
    ```

1. <span data-ttu-id="fff98-251">[A] 변경 hacluster 암호 toohello 동일한 암호</span><span class="sxs-lookup"><span data-stu-id="fff98-251">[A] Change hacluster password toohello same password</span></span>
    ```bash
    sudo passwd hacluster
    
    ```

1. <span data-ttu-id="fff98-252">[A] corosync toouse 다른 전송을 구성 하 고 nodelist를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-252">[A] Configure corosync toouse other transport and add nodelist.</span></span> <span data-ttu-id="fff98-253">그렇지 않으면 클러스터가 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-253">Cluster will not work otherwise.</span></span>
    ```bash
    sudo vi /etc/corosync/corosync.conf    
    
    ```

    <span data-ttu-id="fff98-254">Hello 다음 콘텐츠 toohello 굵게 표시 된 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-254">Add hello following bold content toohello file.</span></span>
    
    <pre><code> 
    [...]
      interface { 
          [...] 
      }
      <b>transport:      udpu</b>
    } 
    <b>nodelist {
      node {
        ring0_addr:     < ip address of node 1 >
      }
      node {
        ring0_addr:     < ip address of node 2 > 
      } 
    }</b>
    logging {
      [...]
    </code></pre>

    <span data-ttu-id="fff98-255">다음 hello corosync 서비스 다시 시작</span><span class="sxs-lookup"><span data-stu-id="fff98-255">Then restart hello corosync service</span></span>

    ```bash
    sudo service corosync restart
    
    ```

1. <span data-ttu-id="fff98-256">[A] HANA HA 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="fff98-256">[A] Install HANA HA packages</span></span>  
    ```bash
    sudo zypper install SAPHanaSR
    
    ```

## <a name="installing-sap-hana"></a><span data-ttu-id="fff98-257">SAP HANA 설치</span><span class="sxs-lookup"><span data-stu-id="fff98-257">Installing SAP HANA</span></span>

<span data-ttu-id="fff98-258">장을 참조 4의 hello [SAP HANA SR 성능에 최적화 된 시나리오 가이드] [ suse-hana-ha-guide] tooinstall SAP HANA 시스템 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-258">Follow chapter 4 of hello [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] tooinstall SAP HANA System Replication.</span></span>

1. <span data-ttu-id="fff98-259">[A] hello HANA DVD에서에서 hdblcm을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-259">[A] Run hdblcm from hello HANA DVD</span></span>
    * <span data-ttu-id="fff98-260">설치 선택 -> 1</span><span class="sxs-lookup"><span data-stu-id="fff98-260">Choose installation -> 1</span></span>
    * <span data-ttu-id="fff98-261">설치할 추가 구성 요소 선택 -> 1</span><span class="sxs-lookup"><span data-stu-id="fff98-261">Select additional components for installation -> 1</span></span>
    * <span data-ttu-id="fff98-262">설치 경로 [/hana/shared] 입력: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="fff98-262">Enter Installation Path [/hana/shared]: -> ENTER</span></span>
    * <span data-ttu-id="fff98-263">로컬 호스트 이름 입력 [..]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="fff98-263">Enter Local Host Name [..]: -> ENTER</span></span>
    * <span data-ttu-id="fff98-264">Tooadd 추가 호스트 toohello 시스템 하 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="fff98-264">Do you want tooadd additional hosts toohello system?</span></span> <span data-ttu-id="fff98-265">(y/n) [n]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="fff98-265">(y/n) [n]: -> ENTER</span></span>
    * <span data-ttu-id="fff98-266">SAP HANA 시스템 ID 입력: <SID of HANA e.g. HDB></span><span class="sxs-lookup"><span data-stu-id="fff98-266">Enter SAP HANA System ID: <SID of HANA e.g. HDB></span></span>
    * <span data-ttu-id="fff98-267">인스턴스 번호 [00] 입력:</span><span class="sxs-lookup"><span data-stu-id="fff98-267">Enter Instance Number [00]:</span></span>   
  <span data-ttu-id="fff98-268">HANA 인스턴스 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-268">HANA Instance number.</span></span> <span data-ttu-id="fff98-269">위의 hello 예제 뒤 또는 hello Azure 템플릿을 사용한 경우 03를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="fff98-269">Use 03 if you used hello Azure Template or followed hello example above</span></span>
    * <span data-ttu-id="fff98-270">데이터베이스 모드 선택 / 인덱스 [1] 입력: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="fff98-270">Select Database Mode / Enter Index [1]: -> ENTER</span></span>
    * <span data-ttu-id="fff98-271">시스템 사용량 선택 / 인덱스 [4] 입력:</span><span class="sxs-lookup"><span data-stu-id="fff98-271">Select System Usage / Enter Index [4]:</span></span>  
  <span data-ttu-id="fff98-272">Hello 시스템 사용을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-272">Select hello system Usage</span></span>
    * <span data-ttu-id="fff98-273">데이터 볼륨의 위치 [/hana/data/HDB] 입력: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="fff98-273">Enter Location of Data Volumes [/hana/data/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="fff98-274">로그 볼륨의 위치 [/hana/log/HDB] 입력: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="fff98-274">Enter Location of Log Volumes [/hana/log/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="fff98-275">최대 메모리 할당 제한?</span><span class="sxs-lookup"><span data-stu-id="fff98-275">Restrict maximum memory allocation?</span></span> <span data-ttu-id="fff98-276">[n]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="fff98-276">[n]: -> ENTER</span></span>
    * <span data-ttu-id="fff98-277">'...' 호스트에 대 한 인증서 호스트 이름 입력 [...]: ENTER-></span><span class="sxs-lookup"><span data-stu-id="fff98-277">Enter Certificate Host Name For Host '...' [...]: -> ENTER</span></span>
    * <span data-ttu-id="fff98-278">SAP 호스트 에이전트 사용자(sapadm) 암호 입력:</span><span class="sxs-lookup"><span data-stu-id="fff98-278">Enter SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="fff98-279">SAP 호스트 에이전트 사용자(sapadm) 암호 확인:</span><span class="sxs-lookup"><span data-stu-id="fff98-279">Confirm SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="fff98-280">시스템 관리자(hdbadm) 암호 입력:</span><span class="sxs-lookup"><span data-stu-id="fff98-280">Enter System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="fff98-281">시스템 관리자(hdbadm) 암호 확인:</span><span class="sxs-lookup"><span data-stu-id="fff98-281">Confirm System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="fff98-282">시스템 관리자 홈 디렉터리 [/usr/sap/HDB/home] 입력: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="fff98-282">Enter System Administrator Home Directory [/usr/sap/HDB/home]: -> ENTER</span></span>
    * <span data-ttu-id="fff98-283">시스템 관리자 로그인 셸 [/bin/sh] 입력: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="fff98-283">Enter System Administrator Login Shell [/bin/sh]: -> ENTER</span></span>
    * <span data-ttu-id="fff98-284">시스템 관리자 사용자 ID [1001] 입력: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="fff98-284">Enter System Administrator User ID [1001]: -> ENTER</span></span>
    * <span data-ttu-id="fff98-285">사용자 그룹 ID(sapsys) [79] 입력: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="fff98-285">Enter ID of User Group (sapsys) [79]: -> ENTER</span></span>
    * <span data-ttu-id="fff98-286">데이터베이스 사용자(SYSTEM) 암호 입력:</span><span class="sxs-lookup"><span data-stu-id="fff98-286">Enter Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="fff98-287">데이터베이스 사용자(SYSTEM) 암호 확인:</span><span class="sxs-lookup"><span data-stu-id="fff98-287">Confirm Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="fff98-288">컴퓨터를 다시 부팅한 다음 시스템 다시 시작?</span><span class="sxs-lookup"><span data-stu-id="fff98-288">Restart system after machine reboot?</span></span> <span data-ttu-id="fff98-289">[n]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="fff98-289">[n]: -> ENTER</span></span>
    * <span data-ttu-id="fff98-290">Toocontinue 하 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="fff98-290">Do you want toocontinue?</span></span> <span data-ttu-id="fff98-291">(y/n):</span><span class="sxs-lookup"><span data-stu-id="fff98-291">(y/n):</span></span>  
  <span data-ttu-id="fff98-292">Hello 요약의 유효성을 검사 하 고 y toocontinue 입력</span><span class="sxs-lookup"><span data-stu-id="fff98-292">Validate hello summary and enter y toocontinue</span></span>
1. <span data-ttu-id="fff98-293">[A] SAP 호스트 에이전트 업그레이드</span><span class="sxs-lookup"><span data-stu-id="fff98-293">[A] Upgrade SAP Host Agent</span></span>  
  <span data-ttu-id="fff98-294">Hello에서 hello 최신 SAP 호스트 에이전트 아카이브 다운로드 [SAP Softwarecenter] [ sap-swcenter] 하 고 실행할 hello 명령 tooupgrade hello 에이전트 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-294">Download hello latest SAP Host Agent archive from hello [SAP Softwarecenter][sap-swcenter] and run hello following command tooupgrade hello agent.</span></span> <span data-ttu-id="fff98-295">Hello 경로 toohello 보관 toopoint toohello 다운로드 한 파일을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-295">Replace hello path toohello archive toopoint toohello file you downloaded.</span></span>
    ```bash
    sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <path tooSAP Host Agent SAR>
    ```

1. <span data-ttu-id="fff98-296">[1] 루트로 HANA 복제 만들기</span><span class="sxs-lookup"><span data-stu-id="fff98-296">[1] Create HANA replication (as root)</span></span>  
    <span data-ttu-id="fff98-297">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-297">Run hello following command.</span></span> <span data-ttu-id="fff98-298">SAP HANA 설치의 hello 값을 사용 하 여 있는지 tooreplace 굵게 표시 된 문자열 (HANA 시스템 ID HDB 및 인스턴스 번호 03)를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-298">Make sure tooreplace bold strings (HANA System ID HDB and instance number 03) with hello values of your SAP HANA installation.</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
    hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
    hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
    </code></pre>

1. <span data-ttu-id="fff98-299">[A] 루트로 키 저장소 항목 만들기</span><span class="sxs-lookup"><span data-stu-id="fff98-299">[A] Create keystore entry (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>passwd</b>
    </code></pre>
1. <span data-ttu-id="fff98-300">[1] 루트로 데이터베이스 백업</span><span class="sxs-lookup"><span data-stu-id="fff98-300">[1] Backup database (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
    </code></pre>
1. <span data-ttu-id="fff98-301">[1] toohello sapsid 사용자 (예: hdbadm) 전환 하 고 hello 기본 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-301">[1] Switch toohello sapsid user (for example hdbadm) and create hello primary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    hdbnsutil -sr_enable –-name=<b>SITE1</b>
    </code></pre>
1. <span data-ttu-id="fff98-302">[2] toohello sapsid 사용자 (예: hdbadm) 전환한 hello 보조 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-302">[2] Switch toohello sapsid user (for example hdbadm) and create hello secondary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    sapcontrol -nr <b>03</b> -function StopWait 600 10
    hdbnsutil -sr_register --remoteHost=<b>saphanavm1</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
    </code></pre>

## <a name="configure-cluster-framework"></a><span data-ttu-id="fff98-303">클러스터 프레임워크 구성</span><span class="sxs-lookup"><span data-stu-id="fff98-303">Configure Cluster Framework</span></span>

<span data-ttu-id="fff98-304">Hello 기본 설정 변경</span><span class="sxs-lookup"><span data-stu-id="fff98-304">Change hello default settings</span></span>

<pre>
sudo vi crm-defaults.txt
# enter hello following toocrm-defaults.txt
<code>
property $id="cib-bootstrap-options" \
  no-quorum-policy="ignore" \
  stonith-enabled="true" \
  stonith-action="reboot" \
  stonith-timeout="150s"
rsc_defaults $id="rsc-options" \
  resource-stickiness="1000" \
  migration-threshold="5000"
op_defaults $id="op-options" \
  timeout="600"
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="fff98-305">이제 hello 파일 toohello 클러스터 로드</span><span class="sxs-lookup"><span data-stu-id="fff98-305">now we load hello file toohello cluster</span></span>
<span data-ttu-id="fff98-306">sudo crm configure load update crm-defaults.txt</span><span class="sxs-lookup"><span data-stu-id="fff98-306">sudo crm configure load update crm-defaults.txt</span></span>
</pre>

### <a name="create-stonith-device"></a><span data-ttu-id="fff98-307">STONITH 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="fff98-307">Create STONITH device</span></span>

<span data-ttu-id="fff98-308">hello STONITH 장치는 Microsoft Azure에 대 한 서비스 사용자 tooauthorize를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-308">hello STONITH device uses a Service Principal tooauthorize against Microsoft Azure.</span></span> <span data-ttu-id="fff98-309">이러한 단계 toocreate 서비스 사용자를 수행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="fff98-309">Please follow these steps toocreate a Service Principal.</span></span>

1. <span data-ttu-id="fff98-310">너무 이동<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="fff98-310">Go too<https://portal.azure.com></span></span>
1. <span data-ttu-id="fff98-311">Azure Active Directory 블레이드 열기 hello</span><span class="sxs-lookup"><span data-stu-id="fff98-311">Open hello Azure Active Directory blade</span></span>  
   <span data-ttu-id="fff98-312">TooProperties 이동한 적어 둡니다 hello 디렉터리 id입니다. 이 hello **테 넌 트 id**합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-312">Go tooProperties and write down hello Directory Id. This is hello **tenant id**.</span></span>
1. <span data-ttu-id="fff98-313">앱 등록 클릭</span><span class="sxs-lookup"><span data-stu-id="fff98-313">Click App registrations</span></span>
1. <span data-ttu-id="fff98-314">추가를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-314">Click Add</span></span>
1. <span data-ttu-id="fff98-315">이름을 입력하고 응용 프로그램 유형 "Web app/API"를 선택한 다음 로그온 URL(예: http://localhost )을 입력하고 만들기를 클릭</span><span class="sxs-lookup"><span data-stu-id="fff98-315">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="fff98-316">hello 로그온 URL은 사용 되지 않으며 유효한 URL이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-316">hello sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="fff98-317">선택 hello 새 앱 hello 설정 탭의 키 클릭</span><span class="sxs-lookup"><span data-stu-id="fff98-317">Select hello new App and click Keys in hello Settings tab</span></span>
1. <span data-ttu-id="fff98-318">새 키의 설명을 입력하고 “만료되지 않음”을 선택한 다음 저장을 클릭</span><span class="sxs-lookup"><span data-stu-id="fff98-318">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="fff98-319">Hello 값 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-319">Write down hello Value.</span></span> <span data-ttu-id="fff98-320">Hello로 사용 **암호** hello 서비스 사용자에 대 한</span><span class="sxs-lookup"><span data-stu-id="fff98-320">It is used as hello **password** for hello Service Principal</span></span>
1. <span data-ttu-id="fff98-321">적어 둡니다 hello 응용 프로그램 id입니다. Hello 사용자 이름으로 사용 됩니다 (**로그인 id** hello 단계 아래에) hello 서비스 사용자의</span><span class="sxs-lookup"><span data-stu-id="fff98-321">Write down hello Application Id. It is used as hello username (**login id** in hello steps below) of hello Service Principal</span></span>

<span data-ttu-id="fff98-322">hello 서비스 사용자에 없는 사용 권한을 tooaccess Azure 리소스 기본적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-322">hello Service Principal does not have permissions tooaccess your Azure resources by default.</span></span> <span data-ttu-id="fff98-323">Toogive hello 서비스 보안 주체 사용 권한 toostart 필요 하 고 중지 (할당 취소) hello 클러스터의 모든 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="fff98-323">You need toogive hello Service Principal permissions toostart and stop (deallocate) all virtual machines of hello cluster.</span></span>

1. <span data-ttu-id="fff98-324">Toohttps://portal.azure.com 이동</span><span class="sxs-lookup"><span data-stu-id="fff98-324">Go toohttps://portal.azure.com</span></span>
1. <span data-ttu-id="fff98-325">모든 리소스 블레이드를 hello 열기</span><span class="sxs-lookup"><span data-stu-id="fff98-325">Open hello All resources blade</span></span>
1. <span data-ttu-id="fff98-326">Hello 가상 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-326">Select hello virtual machine</span></span>
1. <span data-ttu-id="fff98-327">액세스 제어(IAM) 클릭</span><span class="sxs-lookup"><span data-stu-id="fff98-327">Click Access control (IAM)</span></span>
1. <span data-ttu-id="fff98-328">추가를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-328">Click Add</span></span>
1. <span data-ttu-id="fff98-329">Hello 역할 소유자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-329">Select hello role Owner</span></span>
1. <span data-ttu-id="fff98-330">위에서 만든 hello 응용 프로그램의 hello 이름 입력</span><span class="sxs-lookup"><span data-stu-id="fff98-330">Enter hello name of hello application you created above</span></span>
1. <span data-ttu-id="fff98-331">확인 클릭</span><span class="sxs-lookup"><span data-stu-id="fff98-331">Click OK</span></span>

<span data-ttu-id="fff98-332">Hello 가상 컴퓨터에 대 한 hello 권한의 편집한 후에 hello 클러스터의 hello STONITH 장치를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-332">After you edited hello permissions for hello virtual machines, you can configure hello STONITH devices in hello cluster.</span></span>

<pre>
sudo vi crm-fencing.txt
# enter hello following toocrm-fencing.txt
# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password
<code>
primitive rsc_st_azure_1 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

primitive rsc_st_azure_2 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="fff98-333">이제 hello 파일 toohello 클러스터 로드</span><span class="sxs-lookup"><span data-stu-id="fff98-333">now we load hello file toohello cluster</span></span>
<span data-ttu-id="fff98-334">sudo crm configure load update crm-fencing.txt</span><span class="sxs-lookup"><span data-stu-id="fff98-334">sudo crm configure load update crm-fencing.txt</span></span>
</pre>

### <a name="create-sap-hana-resources"></a><span data-ttu-id="fff98-335">SAP HANA 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="fff98-335">Create SAP HANA resources</span></span>

<pre>
sudo vi crm-saphanatop.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number and HANA system id
<code>
primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHanaTopology \
    operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
    op monitor interval="10" timeout="600" \
    op start interval="0" timeout="600" \
    op stop interval="0" timeout="300" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"

clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="fff98-336">이제 hello 파일 toohello 클러스터 로드</span><span class="sxs-lookup"><span data-stu-id="fff98-336">now we load hello file toohello cluster</span></span>
<span data-ttu-id="fff98-337">sudo crm configure load update crm-saphanatop.txt</span><span class="sxs-lookup"><span data-stu-id="fff98-337">sudo crm configure load update crm-saphanatop.txt</span></span>
</pre>

<pre>
sudo vi crm-saphana.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
<code>
primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
    operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
    op start interval="0" timeout="3600" \
    op stop interval="0" timeout="3600" \
    op promote interval="0" timeout="3600" \
    op monitor interval="60" role="Master" timeout="700" \
    op monitor interval="61" role="Slave" timeout="700" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
    DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"

ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
    target-role="Started" interleave="true"

primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
    meta target-role="Started" is-managed="true" \ 
    operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
    op monitor interval="10s" timeout="20s" \ 
    params ip="<b>10.0.0.21</b>" 
primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
    params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
    op monitor timeout=20s interval=10 depth=0 
group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
 
colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  
order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="fff98-338">이제 hello 파일 toohello 클러스터 로드</span><span class="sxs-lookup"><span data-stu-id="fff98-338">now we load hello file toohello cluster</span></span>
<span data-ttu-id="fff98-339">sudo crm configure load update crm-saphana.txt</span><span class="sxs-lookup"><span data-stu-id="fff98-339">sudo crm configure load update crm-saphana.txt</span></span>
</pre>

### <a name="test-cluster-setup"></a><span data-ttu-id="fff98-340">클러스터 설정 테스트</span><span class="sxs-lookup"><span data-stu-id="fff98-340">Test cluster setup</span></span>
<span data-ttu-id="fff98-341">hello 장 다음 설치 프로그램을 테스트 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-341">hello following chapter describe how you can test your setup.</span></span> <span data-ttu-id="fff98-342">모든 테스트 루트는 hello SAP HANA 마스터 hello 가상 컴퓨터 saphanavm1에서 실행 되 고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-342">Every test assumes that you are root and hello SAP HANA master is running on hello virtual machine saphanavm1.</span></span>

#### <a name="fencing-test"></a><span data-ttu-id="fff98-343">펜싱 테스트</span><span class="sxs-lookup"><span data-stu-id="fff98-343">Fencing Test</span></span>

<span data-ttu-id="fff98-344">네트워크 인터페이스 노드 saphanavm1에 hello를 사용 하지 않도록 설정 하 여 hello 펜스 에이전트의 hello 설치 프로그램을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-344">You can test hello setup of hello fencing agent by disabling hello network interface on node saphanavm1.</span></span>

<pre><code>
sudo ifdown eth0
</code></pre>

<span data-ttu-id="fff98-345">hello 가상 컴퓨터 가져오기 지금 다시 시작 하거나 클러스터 구성에 따라 중지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-345">hello virtual machine should now get restarted or stopped depending on your cluster configuration.</span></span>
<span data-ttu-id="fff98-346">Hello stonith 작업 toooff로 설정 하면 hello 가상 컴퓨터가 중지 되 고 hello 리소스는 가상 컴퓨터를 실행 하는 마이그레이션된 toohello 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-346">If you set hello stonith-action toooff, hello virtual machine will be stopped and hello resources are migrated toohello running virtual machine.</span></span>

<span data-ttu-id="fff98-347">Hello 가상 컴퓨터를 다시 시작 되 면 hello SAP HANA 리소스 못합니다 toostart 보조 데이터베이스로 AUTOMATED_REGISTER를 설정한 경우 = "false"입니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-347">Once you start hello virtual machine again, hello SAP HANA resource will fail toostart as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="fff98-348">이 경우 hello 다음 명령을 실행 하 여 보조로 tooconfigure hello HANA 인스턴스가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-348">In this case, you need tooconfigure hello HANA instance as secondary by executing hello following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b>

# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-manual-failover"></a><span data-ttu-id="fff98-349">수동 장애 조치 테스트</span><span class="sxs-lookup"><span data-stu-id="fff98-349">Testing a manual failover</span></span>

<span data-ttu-id="fff98-350">수동 장애 조치 노드 saphanavm1에 hello pacemaker 서비스를 중지 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-350">You can test a manual failover by stopping hello pacemaker service on node saphanavm1.</span></span>
<pre><code>
service pacemaker stop
</code></pre>

<span data-ttu-id="fff98-351">Hello 장애 조치 후 hello 서비스를 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-351">After hello failover, you can start hello service again.</span></span> <span data-ttu-id="fff98-352">hello saphanavm1에 SAP HANA 리소스 못합니다 toostart 보조 데이터베이스로 AUTOMATED_REGISTER를 설정한 경우 = "false"입니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-352">hello SAP HANA resource on saphanavm1 will fail toostart as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="fff98-353">이 경우 hello 다음 명령을 실행 하 여 보조로 tooconfigure hello HANA 인스턴스가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-353">In this case, you need tooconfigure hello HANA instance as secondary by executing hello following command:</span></span>

<pre><code>
service pacemaker start
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 


# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-migration"></a><span data-ttu-id="fff98-354">마이그레이션 테스트</span><span class="sxs-lookup"><span data-stu-id="fff98-354">Testing a migration</span></span>

<span data-ttu-id="fff98-355">Hello 다음 명령을 실행 하 여 hello SAP HANA 마스터 노드를 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-355">You can migrate hello SAP HANA master node by executing hello following command</span></span>
<pre><code>
crm resource migrate msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
crm resource migrate g_ip_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="fff98-356">Hello SAP HANA 마스터 노드 및 가상 IP 주소 toosaphanavm2 hello를 포함 하는 hello 그룹 마이그레이션해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-356">This should migrate hello SAP HANA master node and hello group that contains hello virtual IP address toosaphanavm2.</span></span>
<span data-ttu-id="fff98-357">hello saphanavm1에 SAP HANA 리소스 못합니다 toostart 보조 데이터베이스로 AUTOMATED_REGISTER를 설정한 경우 = "false"입니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-357">hello SAP HANA resource on saphanavm1 will fail toostart as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="fff98-358">이 경우 hello 다음 명령을 실행 하 여 보조로 tooconfigure hello HANA 인스턴스가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-358">In this case, you need tooconfigure hello HANA instance as secondary by executing hello following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 
</code></pre>

<span data-ttu-id="fff98-359">hello 마이그레이션은 toobe 다시 삭제 해야 하는 위치 제약 조건을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-359">hello migration creates location contraints that need toobe deleted again.</span></span>

<pre><code>
crm configure edited

# delete location contraints that are named like hello following contraint. You should have two contraints, one for hello SAP HANA resource and one for hello IP address group.
location cli-prefer-g_ip_<b>HDB</b>_HDB<b>03</b> g_ip_<b>HDB</b>_HDB<b>03</b> role=Started inf: <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="fff98-360">또한 hello 보조 노드에 리소스의 toocleanup hello 상태 해야</span><span class="sxs-lookup"><span data-stu-id="fff98-360">You also need toocleanup hello state of hello secondary node resource</span></span>

<pre><code>
# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

## <a name="next-steps"></a><span data-ttu-id="fff98-361">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fff98-361">Next steps</span></span>
* <span data-ttu-id="fff98-362">[SAP용 Azure Virtual Machines 계획 및 구현][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="fff98-362">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="fff98-363">[SAP용 Azure Virtual Machines 배포][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="fff98-363">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="fff98-364">[SAP용 Azure Virtual Machines DBMS 배포][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="fff98-364">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="fff98-365">tooestablish 고가용성 및 (대형 인스턴스) Azure에서 SAP HANA의 재해 복구 계획의 참조 toolearn [SAP HANA (대형 인스턴스) 고가용성 및 재해 복구 Azure에서](hana-overview-high-availability-disaster-recovery.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fff98-365">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span> 
