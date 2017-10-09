---
title: "가상 컴퓨터에 대 한 고가용성 SUSE Linux Enterprise Server에서의 SAP NetWeaver SAP 응용 프로그램에 대 한 aaaAzure | Microsoft Docs"
description: "SAP 응용 프로그램용 SUSE Linux Enterprise Server의 SAP NetWeaver에 대한 고가용성 가이드"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: mssedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: sedusch
ms.openlocfilehash: e944103df92d5ffec9196189f138e25972bea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms-on-suse-linux-enterprise-server-for-sap-applications"></a><span data-ttu-id="f7c63-103">SAP 응용 프로그램용 SUSE Linux Enterprise Server의 Azure VM에 있는 SAP NetWeaver에 대한 고가용성</span><span class="sxs-lookup"><span data-stu-id="f7c63-103">High availability for SAP NetWeaver on Azure VMs on SUSE Linux Enterprise Server for SAP applications</span></span>

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
[1410736]:https://launchpad.support.sap.com/#/notes/1410736

[sap-swcenter]:https://support.sap.com/en/my-support/software-downloads.html

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[suse-drbd-guide]:https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha_techguides/book_sleha_techguides.html

[template-multisid-xscs]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged-md%2Fazuredeploy.json
[template-file-server]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-file-server-md%2Fazuredeploy.json

[sap-hana-ha]:sap-hana-high-availability.md

<span data-ttu-id="f7c63-113">이 문서 toodeploy hello 가상 컴퓨터를 hello 가상 컴퓨터 구성, hello 클러스터 프레임 워크를 설치 및 항상 사용 가능한 SAP NetWeaver 7.50 시스템 설치 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-113">This article describes how toodeploy hello virtual machines, configure hello virtual machines, install hello cluster framework and install a highly available SAP NetWeaver 7.50 system.</span></span>
<span data-ttu-id="f7c63-114">Hello 예제 구성에서는 설치 명령이 등입니다. 여기서는 ASCS 인스턴스 번호 00, ERS 인스턴스 번호 02 및 SAP 시스템 ID NWS를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-114">In hello example configurations, installation commands etc. ASCS instance number 00, ERS instance number 02 and SAP System ID NWS is used.</span></span> <span data-ttu-id="f7c63-115">hello hello 예제에서 hello 리소스 (예: 가상 컴퓨터, 가상 네트워크) 이름을 가정 hello를 사용한 [템플릿 수렴] [ template-converged] SAP 시스템 ID NWS toocreate hello 리소스와 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-115">hello names of hello resources (for example virtual machines, virtual networks) in hello example assume that you have used hello [converged template][template-converged] with SAP system ID NWS toocreate hello resources.</span></span>

<span data-ttu-id="f7c63-116">SAP Note와 문서를 먼저 다음 읽기 hello</span><span class="sxs-lookup"><span data-stu-id="f7c63-116">Read hello following SAP Notes and papers first</span></span>

* <span data-ttu-id="f7c63-117">SAP Note [1928533], 다음 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-117">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="f7c63-118">Hello SAP 소프트웨어 배포에 지원 되는 Azure VM 크기의 목록</span><span class="sxs-lookup"><span data-stu-id="f7c63-118">List of Azure VM sizes that are supported for hello deployment of SAP software</span></span>
  * <span data-ttu-id="f7c63-119">Azure VM 크기에 대한 중요한 용량 정보</span><span class="sxs-lookup"><span data-stu-id="f7c63-119">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="f7c63-120">지원되는 SAP 소프트웨어 및 운영 체제(OS)와 데이터베이스 조합</span><span class="sxs-lookup"><span data-stu-id="f7c63-120">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="f7c63-121">Microsoft Azure에서 Windows 및 Linux에 필요한 SAP 커널 버전</span><span class="sxs-lookup"><span data-stu-id="f7c63-121">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>

* <span data-ttu-id="f7c63-122">SAP Note [2015553]는 Azure에서 SAP을 지원하는 SAP 소프트웨어 배포에 대한 필수 구성 요소를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-122">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="f7c63-123">SAP Note [2205917]에는 SAP 응용 프로그램용 SUSE Linux Enterprise Server에 권장되는 OS 설정이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-123">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="f7c63-124">SAP Note [1944799]에는 SAP 응용 프로그램용 SUSE Linux Enterprise Server에 대한 SAP HANA 지침이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-124">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="f7c63-125">SAP Note [2178632]는 Azure에서 SAP에 대해 보고된 모든 모니터링 메트릭에 대한 자세한 정보를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-125">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="f7c63-126">SAP Note [2191498] hello 필요한 SAP 호스트 에이전트 버전 Azure에서 Linux에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-126">SAP Note [2191498] has hello required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="f7c63-127">SAP Note [2243692]는 Azure에서 Linux의 SAP 라이선스에 대한 정보를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-127">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="f7c63-128">SAP Note [1984787]은 SUSE LINUX Enterprise Server 12에 대한 일반 정보를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-128">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="f7c63-129">SAP Note [1999351] Azure 고급 모니터링 확장의 SAP 용 hello에 대 한 추가 문제 해결 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-129">SAP Note [1999351] has additional troubleshooting information for hello Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="f7c63-130">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes)는 Linux에 필요한 모든 SAP Note를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-130">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="f7c63-131">[Linux에서 SAP용 Azure Virtual Machines 계획 및 구현][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="f7c63-131">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="f7c63-132">[Linux에서 SAP용 Azure Virtual Machines 배포(이 문서)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="f7c63-132">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="f7c63-133">[Linux에서 SAP용 Azure Virtual Machines DBMS 배포][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="f7c63-133">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="f7c63-134">[SAP HANA SR 성능 최적화된 시나리오][suse-hana-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="f7c63-134">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide]</span></span>  
  <span data-ttu-id="f7c63-135">hello 가이드에서는 온-프레미스 SAP HANA 시스템 복제를 모든 필요한 정보 tooset 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-135">hello guide contains all required information tooset up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="f7c63-136">이 가이드를 기준으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-136">Use this guide as a baseline.</span></span>
* <span data-ttu-id="f7c63-137">[DRBD Pacemaker와 항상 사용 가능한 NFS 저장소] [ suse-drbd-guide] hello 가이드 모든 필요한 정보 tooset 항상 사용 가능한 NFS 서버를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-137">[Highly Available NFS Storage with DRBD and Pacemaker][suse-drbd-guide] hello guide contains all required information tooset up a highly available NFS server.</span></span> <span data-ttu-id="f7c63-138">이 가이드를 기준으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-138">Use this guide as a baseline.</span></span>


## <a name="overview"></a><span data-ttu-id="f7c63-139">개요</span><span class="sxs-lookup"><span data-stu-id="f7c63-139">Overview</span></span>

<span data-ttu-id="f7c63-140">tooachieve 높은 가용성, SAP NetWeaver NFS 서버가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-140">tooachieve high availability, SAP NetWeaver requires an NFS server.</span></span> <span data-ttu-id="f7c63-141">NFS 서버 hello 별도 클러스터에 구성 되 고 여러 SAP 시스템에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-141">hello NFS server is configured in a separate cluster and can be used by multiple SAP systems.</span></span>

![SAP NetWeaver 고가용성 개요](./media/high-availability-guide-suse/img_001.png)

<span data-ttu-id="f7c63-143">SAP NetWeaver ASCS, SAP NetWeaver SCS, SAP NetWeaver 호출자 및 SAP HANA 데이터베이스 hello NFS 서버 hello 가상 호스트 이름 및 가상 IP 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-143">hello NFS server, SAP NetWeaver ASCS, SAP NetWeaver SCS, SAP NetWeaver ERS and hello SAP HANA database use virtual hostname and virtual IP addresses.</span></span> <span data-ttu-id="f7c63-144">Azure 부하 분산 장치는 필요한 toouse 가상 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-144">On Azure, a load balancer is required toouse a virtual IP address.</span></span> <span data-ttu-id="f7c63-145">hello 다음 목록은 hello hello 부하 분산 장치 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-145">hello following list shows hello configuration of hello load balancer.</span></span>

### <a name="nfs-server"></a><span data-ttu-id="f7c63-146">NFS 서버</span><span class="sxs-lookup"><span data-stu-id="f7c63-146">NFS Server</span></span>
* <span data-ttu-id="f7c63-147">프런트 엔드 구성</span><span class="sxs-lookup"><span data-stu-id="f7c63-147">Frontend configuration</span></span>
  * <span data-ttu-id="f7c63-148">IP 주소 10.0.0.4</span><span class="sxs-lookup"><span data-stu-id="f7c63-148">IP address 10.0.0.4</span></span>
* <span data-ttu-id="f7c63-149">백 엔드 구성</span><span class="sxs-lookup"><span data-stu-id="f7c63-149">Backend configuration</span></span>
  * <span data-ttu-id="f7c63-150">Hello NFS 클러스터의 일부 여야 하는 모든 가상 컴퓨터의 네트워크 인터페이스 tooprimary 연결</span><span class="sxs-lookup"><span data-stu-id="f7c63-150">Connected tooprimary network interfaces of all virtual machines that should be part of hello NFS cluster</span></span>
* <span data-ttu-id="f7c63-151">프로브 포트</span><span class="sxs-lookup"><span data-stu-id="f7c63-151">Probe Port</span></span>
  * <span data-ttu-id="f7c63-152">포트 61000</span><span class="sxs-lookup"><span data-stu-id="f7c63-152">Port 61000</span></span>
* <span data-ttu-id="f7c63-153">부하 분산 규칙</span><span class="sxs-lookup"><span data-stu-id="f7c63-153">Loadbalancing rules</span></span>
  * <span data-ttu-id="f7c63-154">2049 TCP</span><span class="sxs-lookup"><span data-stu-id="f7c63-154">2049 TCP</span></span> 
  * <span data-ttu-id="f7c63-155">2049 UDP</span><span class="sxs-lookup"><span data-stu-id="f7c63-155">2049 UDP</span></span>

### <a name="ascs"></a><span data-ttu-id="f7c63-156">(A)SCS</span><span class="sxs-lookup"><span data-stu-id="f7c63-156">(A)SCS</span></span>
* <span data-ttu-id="f7c63-157">프런트 엔드 구성</span><span class="sxs-lookup"><span data-stu-id="f7c63-157">Frontend configuration</span></span>
  * <span data-ttu-id="f7c63-158">IP 주소 10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="f7c63-158">IP address 10.0.0.10</span></span>
* <span data-ttu-id="f7c63-159">백 엔드 구성</span><span class="sxs-lookup"><span data-stu-id="f7c63-159">Backend configuration</span></span>
  * <span data-ttu-id="f7c63-160">Hello (A) SCS/호출자 클러스터의 일부 여야 하는 모든 가상 컴퓨터의 연결 된 tooprimary 네트워크 인터페이스</span><span class="sxs-lookup"><span data-stu-id="f7c63-160">Connected tooprimary network interfaces of all virtual machines that should be part of hello (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="f7c63-161">프로브 포트</span><span class="sxs-lookup"><span data-stu-id="f7c63-161">Probe Port</span></span>
  * <span data-ttu-id="f7c63-162">포트 620**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="f7c63-162">Port 620**&lt;nr&gt;**</span></span>
* <span data-ttu-id="f7c63-163">부하 분산 규칙</span><span class="sxs-lookup"><span data-stu-id="f7c63-163">Loadbalancing rules</span></span>
  * <span data-ttu-id="f7c63-164">32**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="f7c63-164">32**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="f7c63-165">36**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="f7c63-165">36**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="f7c63-166">39**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="f7c63-166">39**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="f7c63-167">81**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="f7c63-167">81**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="f7c63-168">5**&lt;nr&gt;**13 TCP</span><span class="sxs-lookup"><span data-stu-id="f7c63-168">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="f7c63-169">5**&lt;nr&gt;**14 TCP</span><span class="sxs-lookup"><span data-stu-id="f7c63-169">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="f7c63-170">5**&lt;nr&gt;**16 TCP</span><span class="sxs-lookup"><span data-stu-id="f7c63-170">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="ers"></a><span data-ttu-id="f7c63-171">ERS</span><span class="sxs-lookup"><span data-stu-id="f7c63-171">ERS</span></span>
* <span data-ttu-id="f7c63-172">프런트 엔드 구성</span><span class="sxs-lookup"><span data-stu-id="f7c63-172">Frontend configuration</span></span>
  * <span data-ttu-id="f7c63-173">IP 주소 10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="f7c63-173">IP address 10.0.0.11</span></span>
* <span data-ttu-id="f7c63-174">백 엔드 구성</span><span class="sxs-lookup"><span data-stu-id="f7c63-174">Backend configuration</span></span>
  * <span data-ttu-id="f7c63-175">Hello (A) SCS/호출자 클러스터의 일부 여야 하는 모든 가상 컴퓨터의 연결 된 tooprimary 네트워크 인터페이스</span><span class="sxs-lookup"><span data-stu-id="f7c63-175">Connected tooprimary network interfaces of all virtual machines that should be part of hello (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="f7c63-176">프로브 포트</span><span class="sxs-lookup"><span data-stu-id="f7c63-176">Probe Port</span></span>
  * <span data-ttu-id="f7c63-177">포트 621**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="f7c63-177">Port 621**&lt;nr&gt;**</span></span>
* <span data-ttu-id="f7c63-178">부하 분산 규칙</span><span class="sxs-lookup"><span data-stu-id="f7c63-178">Loadbalancing rules</span></span>
  * <span data-ttu-id="f7c63-179">33**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="f7c63-179">33**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="f7c63-180">5**&lt;nr&gt;**13 TCP</span><span class="sxs-lookup"><span data-stu-id="f7c63-180">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="f7c63-181">5**&lt;nr&gt;**14 TCP</span><span class="sxs-lookup"><span data-stu-id="f7c63-181">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="f7c63-182">5**&lt;nr&gt;**16 TCP</span><span class="sxs-lookup"><span data-stu-id="f7c63-182">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="sap-hana"></a><span data-ttu-id="f7c63-183">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="f7c63-183">SAP HANA</span></span>
* <span data-ttu-id="f7c63-184">프런트 엔드 구성</span><span class="sxs-lookup"><span data-stu-id="f7c63-184">Frontend configuration</span></span>
  * <span data-ttu-id="f7c63-185">IP 주소 10.0.0.12</span><span class="sxs-lookup"><span data-stu-id="f7c63-185">IP address 10.0.0.12</span></span>
* <span data-ttu-id="f7c63-186">백 엔드 구성</span><span class="sxs-lookup"><span data-stu-id="f7c63-186">Backend configuration</span></span>
  * <span data-ttu-id="f7c63-187">Hello HANA 클러스터의 일부 여야 하는 모든 가상 컴퓨터의 네트워크 인터페이스 tooprimary 연결</span><span class="sxs-lookup"><span data-stu-id="f7c63-187">Connected tooprimary network interfaces of all virtual machines that should be part of hello HANA cluster</span></span>
* <span data-ttu-id="f7c63-188">프로브 포트</span><span class="sxs-lookup"><span data-stu-id="f7c63-188">Probe Port</span></span>
  * <span data-ttu-id="f7c63-189">포트 625**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="f7c63-189">Port 625**&lt;nr&gt;**</span></span>
* <span data-ttu-id="f7c63-190">부하 분산 규칙</span><span class="sxs-lookup"><span data-stu-id="f7c63-190">Loadbalancing rules</span></span>
  * <span data-ttu-id="f7c63-191">3**&lt;nr&gt;**15 TCP</span><span class="sxs-lookup"><span data-stu-id="f7c63-191">3**&lt;nr&gt;**15 TCP</span></span>
  * <span data-ttu-id="f7c63-192">3**&lt;nr&gt;**17 TCP</span><span class="sxs-lookup"><span data-stu-id="f7c63-192">3**&lt;nr&gt;**17 TCP</span></span>

## <a name="setting-up-a-highly-available-nfs-server"></a><span data-ttu-id="f7c63-193">고가용성 NFS 서버 설정</span><span class="sxs-lookup"><span data-stu-id="f7c63-193">Setting up a highly available NFS server</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="f7c63-194">Linux 배포</span><span class="sxs-lookup"><span data-stu-id="f7c63-194">Deploying Linux</span></span>

<span data-ttu-id="f7c63-195">Azure 마켓플레이스 hello toodeploy 새 가상 컴퓨터를 사용할 수 있는 SAP 응용 프로그램 12에 대 한 SUSE Linux Enterprise Server에 대 한 이미지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-195">hello Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use toodeploy new virtual machines.</span></span>
<span data-ttu-id="f7c63-196">사용할 수 있습니다 hello 빠른 시작 템플릿 중 하나에 github toodeploy 필요한 모든 리소스.</span><span class="sxs-lookup"><span data-stu-id="f7c63-196">You can use one of hello quick start templates on github toodeploy all required resources.</span></span> <span data-ttu-id="f7c63-197">hello 템플릿 hello 가상 컴퓨터, hello 부하 분산 장치, 가용성 집합 등을 배포 합니다. 이러한 단계 toodeploy hello 서식 파일을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-197">hello template deploys hello virtual machines, hello load balancer, availability set etc. Follow these steps toodeploy hello template:</span></span>

1. <span data-ttu-id="f7c63-198">열기 hello [SAP 파일 서버 템플릿] [ template-file-server] hello Azure 포털에서</span><span class="sxs-lookup"><span data-stu-id="f7c63-198">Open hello [SAP file server template][template-file-server] in hello Azure portal</span></span>   
1. <span data-ttu-id="f7c63-199">Hello 매개 변수 뒤에 입력</span><span class="sxs-lookup"><span data-stu-id="f7c63-199">Enter hello following parameters</span></span>
   1. <span data-ttu-id="f7c63-200">리소스 접두사 -</span><span class="sxs-lookup"><span data-stu-id="f7c63-200">Resource Prefix</span></span>  
      <span data-ttu-id="f7c63-201">원하는 toouse hello 접두사를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-201">Enter hello prefix you want toouse.</span></span> <span data-ttu-id="f7c63-202">hello 값은 배포 된 hello 리소스에 대 한 접두사로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-202">hello value is used as a prefix for hello resources that are deployed.</span></span>
   2. <span data-ttu-id="f7c63-203">OS 종류 -</span><span class="sxs-lookup"><span data-stu-id="f7c63-203">Os Type</span></span>  
      <span data-ttu-id="f7c63-204">Hello Linux 배포 사항 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-204">Select one of hello Linux distributions.</span></span> <span data-ttu-id="f7c63-205">이 예제에서는 SLES 12를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-205">For this example, select SLES 12</span></span>
   3. <span data-ttu-id="f7c63-206">관리자 사용자 이름 및 관리자 암호 -</span><span class="sxs-lookup"><span data-stu-id="f7c63-206">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="f7c63-207">새 사용자를 만들가 toohello 컴퓨터에서 사용 되는 toolog 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-207">A new user is created that can be used toolog on toohello machine.</span></span>
   4. <span data-ttu-id="f7c63-208">서브넷 ID -</span><span class="sxs-lookup"><span data-stu-id="f7c63-208">Subnet Id</span></span>  
      <span data-ttu-id="f7c63-209">hello 서브넷 toowhich hello 가상 컴퓨터의 hello ID에 연결 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-209">hello ID of hello subnet toowhich hello virtual machines should be connected to.</span></span> <span data-ttu-id="f7c63-210">원하는 toocreate 새 가상 네트워크 또는 VPN 또는 Express 경로 가상 네트워크 tooconnect hello 가상 컴퓨터 tooyour 온-프레미스 네트워크의 hello 서브넷을 선택 하는 경우 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-210">Leave empty if you want toocreate a new virtual network or select hello subnet of your VPN or Express Route virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="f7c63-211">hello ID는 일반적으로 /subscriptions/ 처럼 보이는**&lt;구독 id&gt;**/resourceGroups/**&lt;리소스 그룹 이름은&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;가상 네트워크 이름&gt;**/subnets/**&lt;서브넷 이름입니다.&gt;**</span><span class="sxs-lookup"><span data-stu-id="f7c63-211">hello ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="f7c63-212">설치</span><span class="sxs-lookup"><span data-stu-id="f7c63-212">Installation</span></span>

<span data-ttu-id="f7c63-213">hello 다음 항목은 접두사가 사용 하 여 **[A]** -해당 tooall 노드 **[1]** -해당 toonode 1 또는 **[2]** -해당 toonode 2입니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-213">hello following items are prefixed with either **[A]** - applicable tooall nodes, **[1]** - only applicable toonode 1 or **[2]** - only applicable toonode 2.</span></span>

1. <span data-ttu-id="f7c63-214">**[A]** SLES 업데이트</span><span class="sxs-lookup"><span data-stu-id="f7c63-214">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="f7c63-215">**[1]** ssh 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="f7c63-215">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="f7c63-216">**[2]** ssh 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="f7c63-216">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="f7c63-217">**[1]** ssh 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="f7c63-217">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="f7c63-218">**[A]** HA 확장 설치</span><span class="sxs-lookup"><span data-stu-id="f7c63-218">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="f7c63-219">**[A]** 호스트 이름 확인 설정</span><span class="sxs-lookup"><span data-stu-id="f7c63-219">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="f7c63-220">DNS 서버를 사용 하거나 모든 노드에서 hello /etc/hosts 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-220">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="f7c63-221">이 예제에서는 toouse /etc/hosts 파일 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-221">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="f7c63-222">Hello IP 주소와 hello 명령 뒤에 hello 호스트 이름 바꾸기</span><span class="sxs-lookup"><span data-stu-id="f7c63-222">Replace hello IP address and hello hostname in hello following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="f7c63-223">다음 줄 너무/등/호스트 hello를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-223">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="f7c63-224">IP 주소 및 호스트 이름 toomatch hello 환경 변경</span><span class="sxs-lookup"><span data-stu-id="f7c63-224">Change hello IP address and hostname toomatch your environment</span></span>   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   </code></pre>

1. <span data-ttu-id="f7c63-225">**[1]** 클러스터 설치</span><span class="sxs-lookup"><span data-stu-id="f7c63-225">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="f7c63-226">**[2]**  Toocluster 노드 추가</span><span class="sxs-lookup"><span data-stu-id="f7c63-226">**[2]** Add node toocluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="f7c63-227">**[A]**  변경 hacluster 암호 toohello 동일한 암호</span><span class="sxs-lookup"><span data-stu-id="f7c63-227">**[A]** Change hacluster password toohello same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="f7c63-228">**[A]**  다른 전송을 corosync toouse를 구성 하 고 nodelist를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-228">**[A]** Configure corosync toouse other transport and add nodelist.</span></span> <span data-ttu-id="f7c63-229">그렇지 않으면 클러스터가 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-229">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="f7c63-230">Hello 다음 콘텐츠 toohello 굵게 표시 된 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-230">Add hello following bold content toohello file.</span></span>
   
   <pre><code> 
   [...]
     interface { 
        [...] 
     }
     <b>transport:      udpu</b>
   } 
   <b>nodelist {
     node {
      # IP address of <b>prod-nfs-0</b>
      ring0_addr:10.0.0.5
     }
     node {
      # IP address of <b>prod-nfs-1</b>
      ring0_addr:10.0.0.6
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   <span data-ttu-id="f7c63-231">다음 hello corosync 서비스 다시 시작</span><span class="sxs-lookup"><span data-stu-id="f7c63-231">Then restart hello corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="f7c63-232">**[A]** drbd 구성 요소 설치</span><span class="sxs-lookup"><span data-stu-id="f7c63-232">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="f7c63-233">**[A]**  Hello drbd 장치에 대 한 파티션을 만들려면</span><span class="sxs-lookup"><span data-stu-id="f7c63-233">**[A]** Create a partition for hello drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="f7c63-234">**[A]** LVM 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="f7c63-234">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_NFS /dev/sdc1
   sudo lvcreate -l 100%FREE -n <b>NWS</b> vg_NFS
   </code></pre>

1. <span data-ttu-id="f7c63-235">**[A]**  Hello NFS drbd 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="f7c63-235">**[A]** Create hello NFS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_nfs.res
   </code></pre>

   <span data-ttu-id="f7c63-236">새 drbd 장치 hello 및 종료에 대 한 hello 구성 삽입</span><span class="sxs-lookup"><span data-stu-id="f7c63-236">Insert hello configuration for hello new drbd device and exit</span></span>

   <pre><code>
   resource <b>NWS</b>_nfs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>prod-nfs-0</b> {
         address   <b>10.0.0.5</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
      on <b>prod-nfs-1</b> {
         address   <b>10.0.0.6</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
   }
   </code></pre>

   <span data-ttu-id="f7c63-237">Hello drbd 장치 만들기 및 시작</span><span class="sxs-lookup"><span data-stu-id="f7c63-237">Create hello drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_nfs
   sudo drbdadm up <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="f7c63-238">**[1]** 초기 동기화 건너뛰기</span><span class="sxs-lookup"><span data-stu-id="f7c63-238">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="f7c63-239">**[1]**  집합 hello 주 노드</span><span class="sxs-lookup"><span data-stu-id="f7c63-239">**[1]** Set hello primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="f7c63-240">**[1]**  Hello 새 drbd 장치가 동기화 될 때까지 대기</span><span class="sxs-lookup"><span data-stu-id="f7c63-240">**[1]** Wait until hello new drbd devices are synchronized</span></span>

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:Connected ro:Primary/Secondary ds:UpToDate/UpToDate C r-----
   #    ns:0 nr:0 dw:0 dr:912 al:8 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. <span data-ttu-id="f7c63-241">**[1]**  Drbd 장치 hello에 파일 시스템을 만들</span><span class="sxs-lookup"><span data-stu-id="f7c63-241">**[1]** Create file systems on hello drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="f7c63-242">클러스터 프레임워크 구성</span><span class="sxs-lookup"><span data-stu-id="f7c63-242">Configure Cluster Framework</span></span>

1. <span data-ttu-id="f7c63-243">**[1]**  Hello 기본 설정 변경</span><span class="sxs-lookup"><span data-stu-id="f7c63-243">**[1]** Change hello default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="f7c63-244">**[1]**  추가 hello NFS drbd 장치 toohello 클러스터 구성</span><span class="sxs-lookup"><span data-stu-id="f7c63-244">**[1]** Add hello NFS drbd device toohello cluster configuration</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_nfs \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_nfs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_nfs drbd_<b>NWS</b>_nfs \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="f7c63-245">**[1]**  만들기 hello NFS 서버</span><span class="sxs-lookup"><span data-stu-id="f7c63-245">**[1]** Create hello NFS server</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive nfsserver \
     systemd:nfs-server \
     op monitor interval="30s"

   crm(live)configure# clone cl-nfsserver nfsserver interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="f7c63-246">**[1]**  Hello NFS 파일 시스템 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="f7c63-246">**[1]** Create hello NFS File System resources</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive fs_<b>NWS</b>_sapmnt \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/srv/nfs/<b>NWS</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# group g-<b>NWS</b>_nfs fs_<b>NWS</b>_sapmnt

   crm(live)configure# order o-<b>NWS</b>_drbd_before_nfs inf: \
     ms-drbd_<b>NWS</b>_nfs:promote g-<b>NWS</b>_nfs:start
   
   crm(live)configure# colocation col-<b>NWS</b>_nfs_on_drbd inf: \
     g-<b>NWS</b>_nfs ms-drbd_<b>NWS</b>_nfs:Master

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="f7c63-247">**[1]**  Hello NFS 내보내기 만들기</span><span class="sxs-lookup"><span data-stu-id="f7c63-247">**[1]** Create hello NFS exports</span></span>

   <pre><code>
   sudo mkdir /srv/nfs/<b>NWS</b>/sidsys
   sudo mkdir /srv/nfs/<b>NWS</b>/sapmntsid
   sudo mkdir /srv/nfs/<b>NWS</b>/trans

   sudo crm configure

   crm(live)configure# primitive exportfs_<b>NWS</b> \
     ocf:heartbeat:exportfs \
     params directory="/srv/nfs/<b>NWS</b>" \
     options="rw,no_root_squash" \
     clientspec="*" fsid=0 \
     wait_for_leasetime_on_stop=true \
     op monitor interval="30s"

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add exportfs_<b>NWS</b>

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="f7c63-248">**[1]**  가상 IP 리소스 및 hello 내부 부하 분산 장치에 대 한 상태 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="f7c63-248">**[1]** Create a virtual IP resource and health-probe for hello internal load balancer</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive vip_<b>NWS</b>_nfs IPaddr2 \
     params ip=<b>10.0.0.4</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_nfs anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 610<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add nc_<b>NWS</b>_nfs
   crm(live)configure# modgroup g-<b>NWS</b>_nfs add vip_<b>NWS</b>_nfs

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

### <a name="create-stonith-device"></a><span data-ttu-id="f7c63-249">STONITH 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="f7c63-249">Create STONITH device</span></span>

<span data-ttu-id="f7c63-250">hello STONITH 장치는 Microsoft Azure에 대 한 서비스 사용자 tooauthorize를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-250">hello STONITH device uses a Service Principal tooauthorize against Microsoft Azure.</span></span> <span data-ttu-id="f7c63-251">이러한 단계 toocreate 서비스 사용자를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-251">Follow these steps toocreate a Service Principal.</span></span>

1. <span data-ttu-id="f7c63-252">너무 이동<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="f7c63-252">Go too<https://portal.azure.com></span></span>
1. <span data-ttu-id="f7c63-253">Azure Active Directory 블레이드 열기 hello</span><span class="sxs-lookup"><span data-stu-id="f7c63-253">Open hello Azure Active Directory blade</span></span>  
   <span data-ttu-id="f7c63-254">TooProperties 이동한 적어 둡니다 hello 디렉터리 id입니다. 이 hello **테 넌 트 id**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-254">Go tooProperties and write down hello Directory Id. This is hello **tenant id**.</span></span>
1. <span data-ttu-id="f7c63-255">앱 등록 클릭</span><span class="sxs-lookup"><span data-stu-id="f7c63-255">Click App registrations</span></span>
1. <span data-ttu-id="f7c63-256">추가를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-256">Click Add</span></span>
1. <span data-ttu-id="f7c63-257">이름을 입력하고 응용 프로그램 유형 "Web app/API"를 선택한 다음 로그온 URL(예: http://localhost )을 입력하고 만들기를 클릭</span><span class="sxs-lookup"><span data-stu-id="f7c63-257">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="f7c63-258">hello 로그온 URL은 사용 되지 않으며 유효한 URL이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-258">hello sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="f7c63-259">선택 hello 새 앱 hello 설정 탭의 키 클릭</span><span class="sxs-lookup"><span data-stu-id="f7c63-259">Select hello new App and click Keys in hello Settings tab</span></span>
1. <span data-ttu-id="f7c63-260">새 키의 설명을 입력하고 “만료되지 않음”을 선택한 다음 저장을 클릭</span><span class="sxs-lookup"><span data-stu-id="f7c63-260">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="f7c63-261">Hello 값 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-261">Write down hello Value.</span></span> <span data-ttu-id="f7c63-262">Hello로 사용 **암호** hello 서비스 사용자에 대 한</span><span class="sxs-lookup"><span data-stu-id="f7c63-262">It is used as hello **password** for hello Service Principal</span></span>
1. <span data-ttu-id="f7c63-263">적어 둡니다 hello 응용 프로그램 id입니다. Hello 사용자 이름으로 사용 됩니다 (**로그인 id** hello 단계 아래에) hello 서비스 사용자의</span><span class="sxs-lookup"><span data-stu-id="f7c63-263">Write down hello Application Id. It is used as hello username (**login id** in hello steps below) of hello Service Principal</span></span>

<span data-ttu-id="f7c63-264">hello 서비스 사용자에 없는 사용 권한을 tooaccess Azure 리소스 기본적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-264">hello Service Principal does not have permissions tooaccess your Azure resources by default.</span></span> <span data-ttu-id="f7c63-265">Toogive hello 서비스 보안 주체 사용 권한 toostart 필요 하 고 중지 (할당 취소) hello 클러스터의 모든 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="f7c63-265">You need toogive hello Service Principal permissions toostart and stop (deallocate) all virtual machines of hello cluster.</span></span>

1. <span data-ttu-id="f7c63-266">Toohttps://portal.azure.com 이동</span><span class="sxs-lookup"><span data-stu-id="f7c63-266">Go toohttps://portal.azure.com</span></span>
1. <span data-ttu-id="f7c63-267">모든 리소스 블레이드를 hello 열기</span><span class="sxs-lookup"><span data-stu-id="f7c63-267">Open hello All resources blade</span></span>
1. <span data-ttu-id="f7c63-268">Hello 가상 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-268">Select hello virtual machine</span></span>
1. <span data-ttu-id="f7c63-269">액세스 제어(IAM) 클릭</span><span class="sxs-lookup"><span data-stu-id="f7c63-269">Click Access control (IAM)</span></span>
1. <span data-ttu-id="f7c63-270">추가를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-270">Click Add</span></span>
1. <span data-ttu-id="f7c63-271">Hello 역할 소유자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-271">Select hello role Owner</span></span>
1. <span data-ttu-id="f7c63-272">위에서 만든 hello 응용 프로그램의 hello 이름 입력</span><span class="sxs-lookup"><span data-stu-id="f7c63-272">Enter hello name of hello application you created above</span></span>
1. <span data-ttu-id="f7c63-273">확인 클릭</span><span class="sxs-lookup"><span data-stu-id="f7c63-273">Click OK</span></span>

#### <a name="1-create-hello-stonith-devices"></a><span data-ttu-id="f7c63-274">**[1]**  Hello STONITH 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="f7c63-274">**[1]** Create hello STONITH devices</span></span>

<span data-ttu-id="f7c63-275">Hello 가상 컴퓨터에 대 한 hello 권한의 편집한 후에 hello 클러스터의 hello STONITH 장치를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-275">After you edited hello permissions for hello virtual machines, you can configure hello STONITH devices in hello cluster.</span></span>

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a><span data-ttu-id="f7c63-276">**[1]**  STONITH 장치 hello 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="f7c63-276">**[1]** Enable hello use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="setting-up-ascs"></a><span data-ttu-id="f7c63-277">(A)SCS 설정</span><span class="sxs-lookup"><span data-stu-id="f7c63-277">Setting up (A)SCS</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="f7c63-278">Linux 배포</span><span class="sxs-lookup"><span data-stu-id="f7c63-278">Deploying Linux</span></span>

<span data-ttu-id="f7c63-279">Azure 마켓플레이스 hello toodeploy 새 가상 컴퓨터를 사용할 수 있는 SAP 응용 프로그램 12에 대 한 SUSE Linux Enterprise Server에 대 한 이미지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-279">hello Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use toodeploy new virtual machines.</span></span> <span data-ttu-id="f7c63-280">hello 마켓플레이스 이미지는 SAP NetWeaver 용 hello 리소스 에이전트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-280">hello marketplace image contains hello resource agent for SAP NetWeaver.</span></span>

<span data-ttu-id="f7c63-281">사용할 수 있습니다 hello 빠른 시작 템플릿 중 하나에 github toodeploy 필요한 모든 리소스.</span><span class="sxs-lookup"><span data-stu-id="f7c63-281">You can use one of hello quick start templates on github toodeploy all required resources.</span></span> <span data-ttu-id="f7c63-282">hello 템플릿 hello 가상 컴퓨터, hello 부하 분산 장치, 가용성 집합 등을 배포 합니다. 이러한 단계 toodeploy hello 서식 파일을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-282">hello template deploys hello virtual machines, hello load balancer, availability set etc. Follow these steps toodeploy hello template:</span></span>

1. <span data-ttu-id="f7c63-283">열기 hello [ASCS/SCS 다중 SID 템플릿] [ template-multisid-xscs] 또는 hello [템플릿 수렴] [ template-converged] hello Azure 포털 hello ASCS/SCS 서식 파일에만 만듭니다 (예: Microsoft SQL Server 또는 SAP HANA) 데이터베이스에 대 한 부하 분산 규칙 hello hello 수렴 형된 템플릿 반면 SAP NetWeaver ASCS/SCS hello 및 호출자 (Linux에만 해당) 인스턴스에 대 한 hello 부하 분산 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-283">Open hello [ASCS/SCS Multi SID template][template-multisid-xscs] or hello [converged template][template-converged] on hello Azure portal hello ASCS/SCS template only creates hello load-balancing rules for hello SAP NetWeaver ASCS/SCS and ERS (Linux only) instances whereas hello converged template also creates hello load-balancing rules for a database (for example Microsoft SQL Server or SAP HANA).</span></span> <span data-ttu-id="f7c63-284">Tooinstall SAP NetWeaver 기반 시스템을 계획 하 고 싶다면 tooinstall hello 데이터베이스 경우 같은 컴퓨터 hello, hello를 사용 하 여 [템플릿 수렴][template-converged]합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-284">If you plan tooinstall an SAP NetWeaver based system and you also want tooinstall hello database on hello same machines, use hello [converged template][template-converged].</span></span>
1. <span data-ttu-id="f7c63-285">Hello 매개 변수 뒤에 입력</span><span class="sxs-lookup"><span data-stu-id="f7c63-285">Enter hello following parameters</span></span>
   1. <span data-ttu-id="f7c63-286">리소스 접두사(ASCS/SCS 다중 SID 템플릿에만 해당)</span><span class="sxs-lookup"><span data-stu-id="f7c63-286">Resource Prefix (ASCS/SCS Multi SID template only)</span></span>  
      <span data-ttu-id="f7c63-287">원하는 toouse hello 접두사를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-287">Enter hello prefix you want toouse.</span></span> <span data-ttu-id="f7c63-288">hello 값은 배포 된 hello 리소스에 대 한 접두사로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-288">hello value is used as a prefix for hello resources that are deployed.</span></span>
   3. <span data-ttu-id="f7c63-289">SAP 시스템 ID(수렴형 템플릿에만 해당)</span><span class="sxs-lookup"><span data-stu-id="f7c63-289">Sap System Id (converged template only)</span></span>  
      <span data-ttu-id="f7c63-290">Hello tooinstall 원하는 SAP 시스템의 hello SAP 시스템 Id를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-290">Enter hello SAP system Id of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="f7c63-291">hello Id는 배포 된 hello 리소스에 대 한 접두사로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-291">hello Id is used as a prefix for hello resources that are deployed.</span></span>
   4. <span data-ttu-id="f7c63-292">스택 유형 -</span><span class="sxs-lookup"><span data-stu-id="f7c63-292">Stack Type</span></span>  
      <span data-ttu-id="f7c63-293">Hello SAP NetWeaver 스택 유형 선택</span><span class="sxs-lookup"><span data-stu-id="f7c63-293">Select hello SAP NetWeaver stack type</span></span>
   5. <span data-ttu-id="f7c63-294">OS 종류 -</span><span class="sxs-lookup"><span data-stu-id="f7c63-294">Os Type</span></span>  
      <span data-ttu-id="f7c63-295">Hello Linux 배포 사항 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-295">Select one of hello Linux distributions.</span></span> <span data-ttu-id="f7c63-296">이 예에서는 SLES 12 BYOS 선택</span><span class="sxs-lookup"><span data-stu-id="f7c63-296">For this example, select SLES 12 BYOS</span></span>
   6. <span data-ttu-id="f7c63-297">Db 형식</span><span class="sxs-lookup"><span data-stu-id="f7c63-297">Db Type</span></span>  
      <span data-ttu-id="f7c63-298">HANA 선택</span><span class="sxs-lookup"><span data-stu-id="f7c63-298">Select HANA</span></span>
   7. <span data-ttu-id="f7c63-299">SAP 시스템 크기 -</span><span class="sxs-lookup"><span data-stu-id="f7c63-299">Sap System Size</span></span>  
      <span data-ttu-id="f7c63-300">hello 양을 SAPS hello 새 시스템을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-300">hello amount of SAPS hello new system provides.</span></span> <span data-ttu-id="f7c63-301">SAP 기술 파트너 나 시스템 통합 업체에 문의 개수 SAPS hello 시스템을 사용 하려면 확실 하지 않은 경우</span><span class="sxs-lookup"><span data-stu-id="f7c63-301">If you are not sure how many SAPS hello system requires, please ask your SAP Technology Partner or System Integrator</span></span>
   8. <span data-ttu-id="f7c63-302">시스템 가용성 -</span><span class="sxs-lookup"><span data-stu-id="f7c63-302">System Availability</span></span>  
      <span data-ttu-id="f7c63-303">HA를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-303">Select HA</span></span>
   9. <span data-ttu-id="f7c63-304">관리자 사용자 이름 및 관리자 암호 -</span><span class="sxs-lookup"><span data-stu-id="f7c63-304">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="f7c63-305">새 사용자를 만들가 toohello 컴퓨터에서 사용 되는 toolog 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-305">A new user is created that can be used toolog on toohello machine.</span></span>
   10. <span data-ttu-id="f7c63-306">서브넷 ID -</span><span class="sxs-lookup"><span data-stu-id="f7c63-306">Subnet Id</span></span>  
   <span data-ttu-id="f7c63-307">hello 서브넷 toowhich hello 가상 컴퓨터의 hello ID에 연결 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-307">hello ID of hello subnet toowhich hello virtual machines should be connected to.</span></span>  <span data-ttu-id="f7c63-308">선택 사용 하거나 hello NFS 서버 배포의 일부로 만든 동일한 서브넷 hello 또는 toocreate 새 가상 네트워크를 예약할 경우 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-308">Leave empty if you want toocreate a new virtual network or select hello same subnet that you used or created as part of hello NFS server deployment.</span></span> <span data-ttu-id="f7c63-309">hello ID는 일반적으로 /subscriptions/ 처럼 보이는**&lt;구독 id&gt;**/resourceGroups/**&lt;리소스 그룹 이름은&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;가상 네트워크 이름&gt;**/subnets/**&lt;서브넷 이름입니다.&gt;**</span><span class="sxs-lookup"><span data-stu-id="f7c63-309">hello ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="f7c63-310">설치</span><span class="sxs-lookup"><span data-stu-id="f7c63-310">Installation</span></span>

<span data-ttu-id="f7c63-311">hello 다음 항목은 접두사가 사용 하 여 **[A]** -해당 tooall 노드 **[1]** -해당 toonode 1 또는 **[2]** -해당 toonode 2입니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-311">hello following items are prefixed with either **[A]** - applicable tooall nodes, **[1]** - only applicable toonode 1 or **[2]** - only applicable toonode 2.</span></span>

1. <span data-ttu-id="f7c63-312">**[A]** SLES 업데이트</span><span class="sxs-lookup"><span data-stu-id="f7c63-312">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="f7c63-313">**[1]** ssh 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="f7c63-313">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="f7c63-314">**[2]** ssh 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="f7c63-314">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="f7c63-315">**[1]** ssh 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="f7c63-315">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="f7c63-316">**[A]** HA 확장 설치</span><span class="sxs-lookup"><span data-stu-id="f7c63-316">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="f7c63-317">**[A]** SAP 리소스 에이전트 업데이트</span><span class="sxs-lookup"><span data-stu-id="f7c63-317">**[A]** Update SAP resource agents</span></span>  
   
   <span data-ttu-id="f7c63-318">Hello 리소스 에이전트 패키지에 대 한 패치는 필요한 toouse hello 새 구성,이 문서에 설명 되어 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-318">A patch for hello resource-agents package is required toouse hello new configuration, that is described in this article.</span></span> <span data-ttu-id="f7c63-319">다음 명령을 hello로 hello 패치를 이미 설치한 경우 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-319">You can check, if hello patch is already installed with hello following command</span></span>

   <pre><code>
   sudo grep 'parameter name="IS_ERS"' /usr/lib/ocf/resource.d/heartbeat/SAPInstance
   </code></pre>

   <span data-ttu-id="f7c63-320">hello 출력와 유사 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-320">hello output should be similar to</span></span>

   <pre><code>
   &lt;parameter name="IS_ERS" unique="0" required="0"&gt;
   </code></pre>

   <span data-ttu-id="f7c63-321">에 나열 된 tooinstall hello 패치 hello grep 명령 hello IS_ERS 매개 변수를 찾지 못하면 경우 해야 [hello SUSE 다운로드 페이지](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)</span><span class="sxs-lookup"><span data-stu-id="f7c63-321">If hello grep command does not find hello IS_ERS parameter, you need tooinstall hello patch listed on [hello SUSE download page](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)</span></span>

   <pre><code>
   # example for patch for SLES 12 SP1
   sudo zypper in -t patch SUSE-SLE-HA-12-SP1-2017-885=1
   # example for patch for SLES 12 SP2
   sudo zypper in -t patch SUSE-SLE-HA-12-SP2-2017-886=1
   </code></pre>

1. <span data-ttu-id="f7c63-322">**[A]** 호스트 이름 확인 설정</span><span class="sxs-lookup"><span data-stu-id="f7c63-322">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="f7c63-323">DNS 서버를 사용 하거나 모든 노드에서 hello /etc/hosts 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-323">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="f7c63-324">이 예제에서는 toouse /etc/hosts 파일 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-324">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="f7c63-325">Hello IP 주소와 hello 명령 뒤에 hello 호스트 이름 바꾸기</span><span class="sxs-lookup"><span data-stu-id="f7c63-325">Replace hello IP address and hello hostname in hello following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="f7c63-326">다음 줄 너무/등/호스트 hello를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-326">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="f7c63-327">IP 주소 및 호스트 이름 toomatch hello 환경 변경</span><span class="sxs-lookup"><span data-stu-id="f7c63-327">Change hello IP address and hostname toomatch your environment</span></span>   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   </code></pre>

1. <span data-ttu-id="f7c63-328">**[1]** 클러스터 설치</span><span class="sxs-lookup"><span data-stu-id="f7c63-328">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="f7c63-329">**[2]**  Toocluster 노드 추가</span><span class="sxs-lookup"><span data-stu-id="f7c63-329">**[2]** Add node toocluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="f7c63-330">**[A]**  변경 hacluster 암호 toohello 동일한 암호</span><span class="sxs-lookup"><span data-stu-id="f7c63-330">**[A]** Change hacluster password toohello same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="f7c63-331">**[A]**  다른 전송을 corosync toouse를 구성 하 고 nodelist를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-331">**[A]** Configure corosync toouse other transport and add nodelist.</span></span> <span data-ttu-id="f7c63-332">그렇지 않으면 클러스터가 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-332">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="f7c63-333">Hello 다음 콘텐츠 toohello 굵게 표시 된 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-333">Add hello following bold content toohello file.</span></span>
   
   <pre><code> 
   [...]
     interface { 
        [...] 
     }
     <b>transport:      udpu</b>
   } 
   <b>nodelist {
     node {
      # IP address of <b>nws-cl-0</b>
      ring0_addr:     10.0.0.14
     }
     node {
      # IP address of <b>nws-cl-1</b>
      ring0_addr:     10.0.0.13
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   <span data-ttu-id="f7c63-334">다음 hello corosync 서비스 다시 시작</span><span class="sxs-lookup"><span data-stu-id="f7c63-334">Then restart hello corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="f7c63-335">**[A]** drbd 구성 요소 설치</span><span class="sxs-lookup"><span data-stu-id="f7c63-335">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="f7c63-336">**[A]**  Hello drbd 장치에 대 한 파티션을 만들려면</span><span class="sxs-lookup"><span data-stu-id="f7c63-336">**[A]** Create a partition for hello drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="f7c63-337">**[A]** LVM 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="f7c63-337">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_<b>NWS</b> /dev/sdc1
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ASCS vg_<b>NWS</b>
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ERS vg_<b>NWS</b>
   </code></pre>

1. <span data-ttu-id="f7c63-338">**[A]**  Hello SCS drbd 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="f7c63-338">**[A]** Create hello SCS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ascs.res
   </code></pre>

   <span data-ttu-id="f7c63-339">새 drbd 장치 hello 및 종료에 대 한 hello 구성 삽입</span><span class="sxs-lookup"><span data-stu-id="f7c63-339">Insert hello configuration for hello new drbd device and exit</span></span>

   <pre><code>
   resource <b>NWS</b>_ascs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
   }
   </code></pre>

   <span data-ttu-id="f7c63-340">Hello drbd 장치 만들기 및 시작</span><span class="sxs-lookup"><span data-stu-id="f7c63-340">Create hello drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ascs
   sudo drbdadm up <b>NWS</b>_ascs
   </code></pre>

1. <span data-ttu-id="f7c63-341">**[A]**  Hello 호출자 drbd 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="f7c63-341">**[A]** Create hello ERS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ers.res
   </code></pre>

   <span data-ttu-id="f7c63-342">새 drbd 장치 hello 및 종료에 대 한 hello 구성 삽입</span><span class="sxs-lookup"><span data-stu-id="f7c63-342">Insert hello configuration for hello new drbd device and exit</span></span>

   <pre><code>
   resource <b>NWS</b>_ers {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
   }
   </code></pre>

   <span data-ttu-id="f7c63-343">Hello drbd 장치 만들기 및 시작</span><span class="sxs-lookup"><span data-stu-id="f7c63-343">Create hello drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ers
   sudo drbdadm up <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="f7c63-344">**[1]** 초기 동기화 건너뛰기</span><span class="sxs-lookup"><span data-stu-id="f7c63-344">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ascs
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="f7c63-345">**[1]**  집합 hello 주 노드</span><span class="sxs-lookup"><span data-stu-id="f7c63-345">**[1]** Set hello primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_ascs
   sudo drbdadm primary --force <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="f7c63-346">**[1]**  Hello 새 drbd 장치가 동기화 될 때까지 대기</span><span class="sxs-lookup"><span data-stu-id="f7c63-346">**[1]** Wait until hello new drbd devices are synchronized</span></span>

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:93991268 nr:0 dw:93991268 dr:93944920 al:383 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 1: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:6047920 nr:0 dw:6047920 dr:6039112 al:34 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 2: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:5142732 nr:0 dw:5142732 dr:5133924 al:30 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. <span data-ttu-id="f7c63-347">**[1]**  Drbd 장치 hello에 파일 시스템을 만들</span><span class="sxs-lookup"><span data-stu-id="f7c63-347">**[1]** Create file systems on hello drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   sudo mkfs.xfs /dev/drbd1
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="f7c63-348">클러스터 프레임워크 구성</span><span class="sxs-lookup"><span data-stu-id="f7c63-348">Configure Cluster Framework</span></span>

<span data-ttu-id="f7c63-349">**[1]**  Hello 기본 설정 변경</span><span class="sxs-lookup"><span data-stu-id="f7c63-349">**[1]** Change hello default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

## <a name="prepare-for-sap-netweaver-installation"></a><span data-ttu-id="f7c63-350">SAP NetWeaver 설치 준비</span><span class="sxs-lookup"><span data-stu-id="f7c63-350">Prepare for SAP NetWeaver installation</span></span>

1. <span data-ttu-id="f7c63-351">**[A]**  만들기 hello 공유 디렉터리</span><span class="sxs-lookup"><span data-stu-id="f7c63-351">**[A]** Create hello shared directories</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans
   sudo mkdir -p /usr/sap/<b>NWS</b>/SYS

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   sudo chattr +i /usr/sap/<b>NWS</b>/SYS
   </code></pre>

1. <span data-ttu-id="f7c63-352">**[A]** autofs 구성</span><span class="sxs-lookup"><span data-stu-id="f7c63-352">**[A]** Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="f7c63-353">아래 코드를 사용하여 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-353">Create a file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   /usr/sap/<b>NWS</b>/SYS -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sidsys
   </code></pre>

   <span data-ttu-id="f7c63-354">Autofs toomount hello 새 공유를 다시 시작</span><span class="sxs-lookup"><span data-stu-id="f7c63-354">Restart autofs toomount hello new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="f7c63-355">**[A]** 스왑 파일 구성</span><span class="sxs-lookup"><span data-stu-id="f7c63-355">**[A]** Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="f7c63-356">Hello 에이전트 tooactivate hello 변경 다시 시작</span><span class="sxs-lookup"><span data-stu-id="f7c63-356">Restart hello Agent tooactivate hello change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

### <a name="installing-sap-netweaver-ascsers"></a><span data-ttu-id="f7c63-357">SAP NetWeaver ASCS/ERS 설치</span><span class="sxs-lookup"><span data-stu-id="f7c63-357">Installing SAP NetWeaver ASCS/ERS</span></span>

1. <span data-ttu-id="f7c63-358">**[1]**  가상 IP 리소스 및 hello 내부 부하 분산 장치에 대 한 상태 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="f7c63-358">**[1]** Create a virtual IP resource and health-probe for hello internal load balancer</span></span>

   <pre><code>
   sudo crm node standby <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ASCS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ascs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ASCS drbd_<b>NWS</b>_ASCS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ASCS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/usr/sap/<b>NWS</b>/ASCS<b>00</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ASCS IPaddr2 \
     params ip=<b>10.0.0.10</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ASCS anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 620<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0
   
   crm(live)configure# group g-<b>NWS</b>_ASCS nc_<b>NWS</b>_ASCS vip_<b>NWS</b>_ASCS fs_<b>NWS</b>_ASCS \
      meta resource-stickiness=3000

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ASCS inf: \
     ms-drbd_<b>NWS</b>_ASCS:promote g-<b>NWS</b>_ASCS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ASCS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ASCS:Master g-<b>NWS</b>_ASCS
   
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   <span data-ttu-id="f7c63-359">Hello 클러스터 상태가 정상 인지 하며 리소스를 모두 시작 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-359">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="f7c63-360">노드 hello 리소스의 실행에 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-360">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # Node nws-cl-1: standby
   # <b>Online: [ nws-cl-0 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      Stopped: [ nws-cl-1 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   </code></pre>

1. <span data-ttu-id="f7c63-361">**[1]** SAP NetWeaver ASCS 설치</span><span class="sxs-lookup"><span data-stu-id="f7c63-361">**[1]** Install SAP NetWeaver ASCS</span></span>  

   <span data-ttu-id="f7c63-362">예를 들어 hello ASCS hello에 대 한 부하 분산 장치 프런트 엔드 구성의 toohello IP 주소를 매핑하는 가상 호스트 이름을 사용 하는 hello 첫 번째 노드에서 루트로 SAP NetWeaver ASCS 설치 <b>nws ascs</b>, <b>10.0.0.10</b>hello 부하 분산 장치 프로브 hello에 대 한 예를 사용 하는 인스턴스 번호를 hello <b>00</b>합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-362">Install SAP NetWeaver ASCS as root on hello first node using a virtual hostname that maps toohello IP address of hello load balancer frontend configuration for hello ASCS for example <b>nws-ascs</b>, <b>10.0.0.10</b> and hello instance number that you used for hello probe of hello load balancer for example <b>00</b>.</span></span>

   <span data-ttu-id="f7c63-363">Hello sapinst 매개 변수 SAPINST_REMOTE_ACCESS_USER tooallow 루트가 아닌 사용자 tooconnect toosapinst를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-363">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="f7c63-364">**[1]**  가상 IP 리소스 및 hello 내부 부하 분산 장치에 대 한 상태 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="f7c63-364">**[1]** Create a virtual IP resource and health-probe for hello internal load balancer</span></span>

   <pre><code>
   sudo crm node standby <b>nws-cl-0</b>
   sudo crm node online <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ERS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ers" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ERS drbd_<b>NWS</b>_ERS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ERS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd1 \
     directory=/usr/sap/<b>NWS</b>/ERS<b>02</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ERS IPaddr2 \
     params ip=<b>10.0.0.11</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ERS anything \
    params binfile="/usr/bin/nc" cmdline_options="-l -k 621<b>02</b>" \
    op monitor timeout=20s interval=10 depth=0

   crm(live)configure# group g-<b>NWS</b>_ERS nc_<b>NWS</b>_ERS vip_<b>NWS</b>_ERS fs_<b>NWS</b>_ERS

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ERS inf: \
     ms-drbd_<b>NWS</b>_ERS:promote g-<b>NWS</b>_ERS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ERS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ERS:Master g-<b>NWS</b>_ERS
   
   crm(live)configure# commit
   # WARNING: Resources nc_NWS_ASCS,nc_NWS_ERS,nc_NWS_nfs violate uniqueness for parameter "binfile": "/usr/bin/nc"
   # Do you still want toocommit (y/n)? y

   crm(live)configure# exit
   
   </code></pre>
 
   <span data-ttu-id="f7c63-365">Hello 클러스터 상태가 정상 인지 하며 리소스를 모두 시작 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-365">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="f7c63-366">노드 hello 리소스의 실행에 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-366">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # Node <b>nws-cl-0: standby</b>
   # <b>Online: [ nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   </code></pre>

1. <span data-ttu-id="f7c63-367">**[2]** SAP NetWeaver ERS 설치</span><span class="sxs-lookup"><span data-stu-id="f7c63-367">**[2]** Install SAP NetWeaver ERS</span></span>  

   <span data-ttu-id="f7c63-368">예를 들어 hello hello 호출자에 대 한 부하 분산 장치 프런트 엔드 구성의 toohello IP 주소를 매핑하는 가상 호스트 이름을 사용 하 여 hello 두 번째 노드는 루트로 SAP NetWeaver 호출자 설치 <b>nws 호출자</b>, <b>10.0.0.11</b> 예를 들어 hello 부하 분산 장치 프로브 hello에 대 한 사용 하는 인스턴스 번호를 hello <b>02</b>합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-368">Install SAP NetWeaver ERS as root on hello second node using a virtual hostname that maps toohello IP address of hello load balancer frontend configuration for hello ERS for example <b>nws-ers</b>, <b>10.0.0.11</b> and hello instance number that you used for hello probe of hello load balancer for example <b>02</b>.</span></span>

   <span data-ttu-id="f7c63-369">Hello sapinst 매개 변수 SAPINST_REMOTE_ACCESS_USER tooallow 루트가 아닌 사용자 tooconnect toosapinst를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-369">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

   > [!NOTE]
   > <span data-ttu-id="f7c63-370">SWPM SP 20 PL 05 이상을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="f7c63-370">Please use SWPM SP 20 PL 05 or higher.</span></span> <span data-ttu-id="f7c63-371">더 낮은 버전 hello 사용 권한을 올바르게 설정 하지 않으면 및 hello 설치가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-371">Lower versions do not set hello permissions correctly and hello installation will fail.</span></span>
   > 

1. <span data-ttu-id="f7c63-372">**[1]**  Hello ASCS/SCS 및 호출자 인스턴스 프로필 적용</span><span class="sxs-lookup"><span data-stu-id="f7c63-372">**[1]** Adapt hello ASCS/SCS and ERS instance profiles</span></span>
 
   * <span data-ttu-id="f7c63-373">ASCS/SCS 프로필</span><span class="sxs-lookup"><span data-stu-id="f7c63-373">ASCS/SCS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_<b>ASCS00</b>_<b>nws-ascs</b>

   # Change hello restart command tooa start command
   #Restart_Program_01 = local $(_EN) pf=$(_PF)
   Start_Program_01 = local $(_EN) pf=$(_PF)

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector

   # Add hello keep alive parameter
   enque/encni/set_so_keepalive = true
   </code></pre>

   * <span data-ttu-id="f7c63-374">ERS 프로필</span><span class="sxs-lookup"><span data-stu-id="f7c63-374">ERS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector
   </code></pre>


1. <span data-ttu-id="f7c63-375">**[A]** 연결 유지 구성</span><span class="sxs-lookup"><span data-stu-id="f7c63-375">**[A]** Configure Keep Alive</span></span>

   <span data-ttu-id="f7c63-376">hello SAP NetWeaver 응용 프로그램 서버와 hello ASCS/SCS 간의 hello 통신 소프트웨어 부하 분산 장치를 통해 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-376">hello communication between hello SAP NetWeaver application server and hello ASCS/SCS is routed through a software load balancer.</span></span> <span data-ttu-id="f7c63-377">hello 부하 분산 장치 구성 가능한 시간 초과 이후 비활성 연결을 끊습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-377">hello load balancer disconnects inactive connections after a configurable timeout.</span></span> <span data-ttu-id="f7c63-378">tooprevent이 tooset hello SAP NetWeaver ASCS/SCS 프로필의에서 매개 변수를 필요 하 고 hello Linux 시스템 설정을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-378">tooprevent this you need tooset a parameter in hello SAP NetWeaver ASCS/SCS profile and change hello Linux system settings.</span></span> <span data-ttu-id="f7c63-379">자세한 내용은 [SAP Note 1410736][1410736]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7c63-379">Please read [SAP Note 1410736][1410736] for more information.</span></span>
   
   <span data-ttu-id="f7c63-380">hello ASCS/SCS 프로필 매개 변수 큐에 넣지/encni/set_so_keepalive hello 마지막 단계에서 이미 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-380">hello ASCS/SCS profile parameter enque/encni/set_so_keepalive was already added in hello last step.</span></span>

   <pre><code> 
   # Change hello Linux system configuration
   sudo sysctl net.ipv4.tcp_keepalive_time=120
   </code></pre>

1. <span data-ttu-id="f7c63-381">**[A]**  Hello SAP 사용자 hello 설치 후 구성</span><span class="sxs-lookup"><span data-stu-id="f7c63-381">**[A]** Configure hello SAP users after hello installation</span></span>
 
   <pre><code>
   # Add sidadm toohello haclient group
   sudo usermod -aG haclient <b>nws</b>adm   
   </code></pre>

1. <span data-ttu-id="f7c63-382">**[1]**  Hello ASCS 및 호출자 SAP 서비스 toohello sapservice 파일 추가</span><span class="sxs-lookup"><span data-stu-id="f7c63-382">**[1]** Add hello ASCS and ERS SAP services toohello sapservice file</span></span>

   <span data-ttu-id="f7c63-383">Hello ASCS 서비스 항목 toohello 두 번째 노드 및 복사 hello 호출자 서비스 항목 toohello 첫 번째 노드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-383">Add hello ASCS service entry toohello second node and copy hello ERS service entry toohello first node.</span></span>

   <pre><code>
   cat /usr/sap/sapservices | grep ASCS<b>00</b> | sudo ssh <b>nws-cl-1</b> "cat >>/usr/sap/sapservices"
   sudo ssh <b>nws-cl-1</b> "cat /usr/sap/sapservices" | grep ERS<b>02</b> | sudo tee -a /usr/sap/sapservices
   </code></pre>

1. <span data-ttu-id="f7c63-384">**[1]**  Hello SAP 클러스터 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="f7c63-384">**[1]** Create hello SAP cluster resources</span></span>

   <pre><code>
   sudo crm configure property maintenance-mode="true"

   sudo crm configure

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ASCS<b>00</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ASCS<b>00</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b>" \
    AUTOMATIC_RECOVER=false \
    meta resource-stickiness=5000 failure-timeout=60 migration-threshold=1 priority=10

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ERS<b>02</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ERS<b>02</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>" AUTOMATIC_RECOVER=false IS_ERS=true \
    meta priority=1000

   crm(live)configure# modgroup g-<b>NWS</b>_ASCS add rsc_sap_<b>NWS</b>_ASCS<b>00</b>
   crm(live)configure# modgroup g-<b>NWS</b>_ERS add rsc_sap_<b>NWS</b>_ERS<b>02</b>

   crm(live)configure# colocation col_sap_<b>NWS</b>_no_both -5000: g-<b>NWS</b>_ERS g-<b>NWS</b>_ASCS
   crm(live)configure# location loc_sap_<b>NWS</b>_failover_to_ers rsc_sap_<b>NWS</b>_ASCS<b>00</b> rule 2000: runs_ers_<b>NWS</b> eq 1
   crm(live)configure# order ord_sap_<b>NWS</b>_first_start_ascs Optional: rsc_sap_<b>NWS</b>_ASCS<b>00</b>:start rsc_sap_<b>NWS</b>_ERS<b>02</b>:stop symmetrical=false

   crm(live)configure# commit
   crm(live)configure# exit

   sudo crm configure property maintenance-mode="false"
   sudo crm node online <b>nws-cl-0</b>
   </code></pre>

   <span data-ttu-id="f7c63-385">Hello 클러스터 상태가 정상 인지 하며 리소스를 모두 시작 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-385">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="f7c63-386">노드 hello 리소스의 실행에 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-386">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # Online: <b>[ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   </code></pre>

### <a name="create-stonith-device"></a><span data-ttu-id="f7c63-387">STONITH 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="f7c63-387">Create STONITH device</span></span>

<span data-ttu-id="f7c63-388">hello STONITH 장치는 Microsoft Azure에 대 한 서비스 사용자 tooauthorize를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-388">hello STONITH device uses a Service Principal tooauthorize against Microsoft Azure.</span></span> <span data-ttu-id="f7c63-389">이러한 단계 toocreate 서비스 사용자를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-389">Follow these steps toocreate a Service Principal.</span></span>

1. <span data-ttu-id="f7c63-390">너무 이동<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="f7c63-390">Go too<https://portal.azure.com></span></span>
1. <span data-ttu-id="f7c63-391">Azure Active Directory 블레이드 열기 hello</span><span class="sxs-lookup"><span data-stu-id="f7c63-391">Open hello Azure Active Directory blade</span></span>  
   <span data-ttu-id="f7c63-392">TooProperties 이동한 적어 둡니다 hello 디렉터리 id입니다. 이 hello **테 넌 트 id**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-392">Go tooProperties and write down hello Directory Id. This is hello **tenant id**.</span></span>
1. <span data-ttu-id="f7c63-393">앱 등록 클릭</span><span class="sxs-lookup"><span data-stu-id="f7c63-393">Click App registrations</span></span>
1. <span data-ttu-id="f7c63-394">추가를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-394">Click Add</span></span>
1. <span data-ttu-id="f7c63-395">이름을 입력하고 응용 프로그램 유형 "Web app/API"를 선택한 다음 로그온 URL(예: http://localhost )을 입력하고 만들기를 클릭</span><span class="sxs-lookup"><span data-stu-id="f7c63-395">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="f7c63-396">hello 로그온 URL은 사용 되지 않으며 유효한 URL이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-396">hello sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="f7c63-397">선택 hello 새 앱 hello 설정 탭의 키 클릭</span><span class="sxs-lookup"><span data-stu-id="f7c63-397">Select hello new App and click Keys in hello Settings tab</span></span>
1. <span data-ttu-id="f7c63-398">새 키의 설명을 입력하고 “만료되지 않음”을 선택한 다음 저장을 클릭</span><span class="sxs-lookup"><span data-stu-id="f7c63-398">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="f7c63-399">Hello 값 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-399">Write down hello Value.</span></span> <span data-ttu-id="f7c63-400">Hello로 사용 **암호** hello 서비스 사용자에 대 한</span><span class="sxs-lookup"><span data-stu-id="f7c63-400">It is used as hello **password** for hello Service Principal</span></span>
1. <span data-ttu-id="f7c63-401">적어 둡니다 hello 응용 프로그램 id입니다. Hello 사용자 이름으로 사용 됩니다 (**로그인 id** hello 단계 아래에) hello 서비스 사용자의</span><span class="sxs-lookup"><span data-stu-id="f7c63-401">Write down hello Application Id. It is used as hello username (**login id** in hello steps below) of hello Service Principal</span></span>

<span data-ttu-id="f7c63-402">hello 서비스 사용자에 없는 사용 권한을 tooaccess Azure 리소스 기본적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-402">hello Service Principal does not have permissions tooaccess your Azure resources by default.</span></span> <span data-ttu-id="f7c63-403">Toogive hello 서비스 보안 주체 사용 권한 toostart 필요 하 고 중지 (할당 취소) hello 클러스터의 모든 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="f7c63-403">You need toogive hello Service Principal permissions toostart and stop (deallocate) all virtual machines of hello cluster.</span></span>

1. <span data-ttu-id="f7c63-404">Toohttps://portal.azure.com 이동</span><span class="sxs-lookup"><span data-stu-id="f7c63-404">Go toohttps://portal.azure.com</span></span>
1. <span data-ttu-id="f7c63-405">모든 리소스 블레이드를 hello 열기</span><span class="sxs-lookup"><span data-stu-id="f7c63-405">Open hello All resources blade</span></span>
1. <span data-ttu-id="f7c63-406">Hello 가상 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-406">Select hello virtual machine</span></span>
1. <span data-ttu-id="f7c63-407">액세스 제어(IAM) 클릭</span><span class="sxs-lookup"><span data-stu-id="f7c63-407">Click Access control (IAM)</span></span>
1. <span data-ttu-id="f7c63-408">추가를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-408">Click Add</span></span>
1. <span data-ttu-id="f7c63-409">Hello 역할 소유자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-409">Select hello role Owner</span></span>
1. <span data-ttu-id="f7c63-410">위에서 만든 hello 응용 프로그램의 hello 이름 입력</span><span class="sxs-lookup"><span data-stu-id="f7c63-410">Enter hello name of hello application you created above</span></span>
1. <span data-ttu-id="f7c63-411">확인 클릭</span><span class="sxs-lookup"><span data-stu-id="f7c63-411">Click OK</span></span>

#### <a name="1-create-hello-stonith-devices"></a><span data-ttu-id="f7c63-412">**[1]**  Hello STONITH 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="f7c63-412">**[1]** Create hello STONITH devices</span></span>

<span data-ttu-id="f7c63-413">Hello 가상 컴퓨터에 대 한 hello 권한의 편집한 후에 hello 클러스터의 hello STONITH 장치를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-413">After you edited hello permissions for hello virtual machines, you can configure hello STONITH devices in hello cluster.</span></span>

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a><span data-ttu-id="f7c63-414">**[1]**  STONITH 장치 hello 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="f7c63-414">**[1]** Enable hello use of a STONITH device</span></span>

<span data-ttu-id="f7c63-415">Hello STONITH 장치를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="f7c63-415">Enable hello use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="install-database"></a><span data-ttu-id="f7c63-416">데이터베이스 설치</span><span class="sxs-lookup"><span data-stu-id="f7c63-416">Install database</span></span>

<span data-ttu-id="f7c63-417">이 예제에서 SAP HANA System Replication을 설치 및 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-417">In this example an SAP HANA System Replication is installed and configured.</span></span> <span data-ttu-id="f7c63-418">SAP HANA hello hello SAP NetWeaver ASCS/SCS와 호출자와 동일한 클러스터에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-418">SAP HANA will run in hello same cluster as hello SAP NetWeaver ASCS/SCS and ERS.</span></span> <span data-ttu-id="f7c63-419">전용 클러스터에 SAP HANA를 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-419">You can also install SAP HANA on a dedicated cluster.</span></span> <span data-ttu-id="f7c63-420">자세한 내용은 [Azure VM(Virtual Machines)의 SAP HANA 고가용성][sap-hana-ha]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7c63-420">See [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha] for more information.</span></span>

### <a name="prepare-for-sap-hana-installation"></a><span data-ttu-id="f7c63-421">SAP HANA 설치 준비</span><span class="sxs-lookup"><span data-stu-id="f7c63-421">Prepare for SAP HANA installation</span></span>

<span data-ttu-id="f7c63-422">일반적으로는 데이터와 로그 파일을 저장하는 볼륨의 LVM을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-422">We generally recommend using LVM for volumes that store data and log files.</span></span> <span data-ttu-id="f7c63-423">테스트를 위해 toostore 일반 디스크에 직접 데이터 및 로그 파일 hello를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-423">For testing purposes, you can also choose toostore hello data and log file directly on a plain disk.</span></span>

1. <span data-ttu-id="f7c63-424">**[A]** LVM</span><span class="sxs-lookup"><span data-stu-id="f7c63-424">**[A]** LVM</span></span>  
   <span data-ttu-id="f7c63-425">아래 예제에서는 hello 하려면 네 개의 연결 된 데이터 디스크 두 개의 볼륨을 사용 하는 toocreate 되어야 하는 hello 가상 컴퓨터에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-425">hello example below assumes that hello virtual machines have four data disks attached that should be used toocreate two volumes.</span></span>
   
   <span data-ttu-id="f7c63-426">Toouse 되도록 하는 모든 디스크에 대 한 실제 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-426">Create physical volumes for all disks that you want toouse.</span></span>
   
   <pre><code>
   sudo pvcreate /dev/sdd
   sudo pvcreate /dev/sde
   sudo pvcreate /dev/sdf
   sudo pvcreate /dev/sdg
   </code></pre>
   
   <span data-ttu-id="f7c63-427">Hello 데이터 파일에 대 한 볼륨 그룹, hello 로그 파일에 대 한 하나의 볼륨 그룹 및 SAP HANA의 hello 공유 디렉터리에 대 한 만들기</span><span class="sxs-lookup"><span data-stu-id="f7c63-427">Create a volume group for hello data files, one volume group for hello log files and one for hello shared directory of SAP HANA</span></span>
   
   <pre><code>
   sudo vgcreate vg_hana_data /dev/sdd /dev/sde
   sudo vgcreate vg_hana_log /dev/sdf
   sudo vgcreate vg_hana_shared /dev/sdg
   </code></pre>
   
   <span data-ttu-id="f7c63-428">Hello 논리 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-428">Create hello logical volumes</span></span>
   
   <pre><code>
   sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
   sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
   sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
   sudo mkfs.xfs /dev/vg_hana_data/hana_data
   sudo mkfs.xfs /dev/vg_hana_log/hana_log
   sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
   </code></pre>
   
   <span data-ttu-id="f7c63-429">Hello 탑재 디렉터리를 만들고 hello 모든 논리 볼륨의 UUID를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-429">Create hello mount directories and copy hello UUID of all logical volumes</span></span>
   
   <pre><code>
   sudo mkdir -p /hana/data
   sudo mkdir -p /hana/log
   sudo mkdir -p /hana/shared
   sudo chattr +i /hana/data
   sudo chattr +i /hana/log
   sudo chattr +i /hana/shared
   # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
   sudo blkid
   </code></pre>
   
   <span data-ttu-id="f7c63-430">논리 볼륨이 3 개씩 hello에 대 한 autofs 항목 만들기</span><span class="sxs-lookup"><span data-stu-id="f7c63-430">Create autofs entries for hello three logical volumes</span></span>
   
   <pre><code>
   sudo vi /etc/auto.direct
   </code></pre>
   
   <span data-ttu-id="f7c63-431">이 줄 toosudo vi /etc/auto.direct 삽입</span><span class="sxs-lookup"><span data-stu-id="f7c63-431">Insert this line toosudo vi /etc/auto.direct</span></span>
   
   <pre><code>
   /hana/data -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b>
   /hana/log -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b>
   /hana/shared -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b>
   </code></pre>
   
   <span data-ttu-id="f7c63-432">Hello 새 볼륨을 탑재</span><span class="sxs-lookup"><span data-stu-id="f7c63-432">Mount hello new volumes</span></span>
   
   <pre><code>
   sudo service autofs restart 
   </code></pre>

1. <span data-ttu-id="f7c63-433">**[A]** 일반 디스크</span><span class="sxs-lookup"><span data-stu-id="f7c63-433">**[A]** Plain Disks</span></span>  

   <span data-ttu-id="f7c63-434">소규모 또는 데모 시스템용으로 한 디스크에 HANA 데이터와 로그 파일을 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-434">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="f7c63-435">hello 다음 /dev/sdc에 파티션을 만들고 명령과 xfs로 포맷 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-435">hello following commands create a partition on /dev/sdc and format it with xfs.</span></span>
   ```bash
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdd'
   sudo mkfs.xfs /dev/sdd1
   
   # write down hello id of /dev/sdd1
   sudo /sbin/blkid
   sudo vi /etc/auto.direct
   ```
   
   <span data-ttu-id="f7c63-436">이 줄 too/etc/auto.direct 삽입</span><span class="sxs-lookup"><span data-stu-id="f7c63-436">Insert this line too/etc/auto.direct</span></span>
   <pre><code>
   /hana -fstype=xfs :UUID=<b>&lt;UUID&gt;</b>
   </code></pre>
   
   <span data-ttu-id="f7c63-437">Hello 대상 디렉터리를 만들고 hello 디스크를 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-437">Create hello target directory and mount hello disk.</span></span>
   
   <pre><code>
   sudo mkdir /hana
   sudo chattr +i /hana
   sudo service autofs restart
   </code></pre>

### <a name="installing-sap-hana"></a><span data-ttu-id="f7c63-438">SAP HANA 설치</span><span class="sxs-lookup"><span data-stu-id="f7c63-438">Installing SAP HANA</span></span>

<span data-ttu-id="f7c63-439">hello 다음 단계에 기반 hello의 4 장을 [SAP HANA SR 성능에 최적화 된 시나리오 가이드] [ suse-hana-ha-guide] tooinstall SAP HANA 시스템 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-439">hello following steps are based on chapter 4 of hello [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] tooinstall SAP HANA System Replication.</span></span> <span data-ttu-id="f7c63-440">읽어 보십시오 hello 설치를 계속 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="f7c63-440">Please read it before you continue hello installation.</span></span>

1. <span data-ttu-id="f7c63-441">**[A]**  Hdblcm hello HANA DVD에서에서 실행</span><span class="sxs-lookup"><span data-stu-id="f7c63-441">**[A]** Run hdblcm from hello HANA DVD</span></span>
   
   <pre><code>
   sudo hdblcm --sid=<b>HDB</b> --number=<b>03</b> --action=install --batch --password=<b>&lt;password&gt;</b> --system_user_password=<b>&lt;password for system user&gt;</b>

   sudo /hana/shared/<b>HDB</b>/hdblcm/hdblcm --action=configure_internal_network --listen_interface=internal --internal_network=<b>10.0.0/24</b> --password=<b>&lt;password for system user&gt;</b> --batch
   </code></pre>

1. <span data-ttu-id="f7c63-442">**[A]** SAP 호스트 에이전트 업그레이드</span><span class="sxs-lookup"><span data-stu-id="f7c63-442">**[A]** Upgrade SAP Host Agent</span></span>

   <span data-ttu-id="f7c63-443">Hello에서 hello 최신 SAP 호스트 에이전트 아카이브 다운로드 [SAP Softwarecenter] [ sap-swcenter] 하 고 실행할 hello 명령 tooupgrade hello 에이전트 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-443">Download hello latest SAP Host Agent archive from hello [SAP Softwarecenter][sap-swcenter] and run hello following command tooupgrade hello agent.</span></span> <span data-ttu-id="f7c63-444">Hello 경로 toohello 보관 toopoint toohello 다운로드 한 파일을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-444">Replace hello path toohello archive toopoint toohello file you downloaded.</span></span>
   <pre><code>
   sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <b>&lt;path tooSAP Host Agent SAR&gt;</b> 
   </code></pre>

1. <span data-ttu-id="f7c63-445">**[1]** 루트로 HANA 복제 만들기</span><span class="sxs-lookup"><span data-stu-id="f7c63-445">**[1]** Create HANA replication (as root)</span></span>  

   <span data-ttu-id="f7c63-446">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-446">Run hello following command.</span></span> <span data-ttu-id="f7c63-447">SAP HANA 설치의 hello 값을 사용 하 여 있는지 tooreplace 굵게 표시 된 문자열 (HANA 시스템 ID HDB 및 인스턴스 번호 03)를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-447">Make sure tooreplace bold strings (HANA System ID HDB and instance number 03) with hello values of your SAP HANA installation.</span></span>
   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
   hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
   hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
   </code></pre>

1. <span data-ttu-id="f7c63-448">**[A]** 루트로 키 저장소 항목 만들기</span><span class="sxs-lookup"><span data-stu-id="f7c63-448">**[A]** Create keystore entry (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>&lt;passwd&gt;</b>
   </code></pre>

1. <span data-ttu-id="f7c63-449">**[1]** 루트로 데이터베이스 백업</span><span class="sxs-lookup"><span data-stu-id="f7c63-449">**[1]** Backup database (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
   </code></pre>

1. <span data-ttu-id="f7c63-450">**[1]**  Toohello HANA sapsid 사용자를 전환 하 고 hello 주 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-450">**[1]** Switch toohello HANA sapsid user and create hello primary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   hdbnsutil -sr_enable –-name=<b>SITE1</b>
   </code></pre>

1. <span data-ttu-id="f7c63-451">**[2]**  Toohello HANA sapsid 사용자를 전환 하 고 hello 보조 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-451">**[2]** Switch toohello HANA sapsid user and create hello secondary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   sapcontrol -nr <b>03</b> -function StopWait 600 10
   hdbnsutil -sr_register --remoteHost=<b>nws-cl-0</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
   </code></pre>

1. <span data-ttu-id="f7c63-452">**[1]** SAP HANA 클러스터 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="f7c63-452">**[1]** Create SAP HANA cluster resources</span></span>

   <span data-ttu-id="f7c63-453">먼저 hello 토폴로지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-453">First, create hello topology.</span></span>
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number and HANA system id
   
   crm(live)configure# primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b>   ocf:suse:SAPHanaTopology \
     operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
     op monitor interval="10" timeout="600" \
     op start interval="0" timeout="600" \
     op stop interval="0" timeout="300" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"
    
   crm(live)configure# clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>
   
   <span data-ttu-id="f7c63-454">다음으로 hello을 HANA 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="f7c63-454">Next, create hello HANA resources</span></span>
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
    
   crm(live)configure# primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
     operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
     op start interval="0" timeout="3600" \
     op stop interval="0" timeout="3600" \
     op promote interval="0" timeout="3600" \
     op monitor interval="60" role="Master" timeout="700" \
     op monitor interval="61" role="Slave" timeout="700" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
     DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"
    
   crm(live)configure# ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
     target-role="Started" interleave="true"
    
   crm(live)configure# primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
     meta target-role="Started" is-managed="true" \ 
     operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
     op monitor interval="10s" timeout="20s" \ 
     params ip="<b>10.0.0.12</b>" 

   crm(live)configure# primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
     params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
     op monitor timeout=20s interval=10 depth=0 

   crm(live)configure# group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  

   crm(live)configure# order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   <span data-ttu-id="f7c63-455">Hello 클러스터 상태가 정상 인지 하며 리소스를 모두 시작 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-455">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="f7c63-456">노드 hello 리소스의 실행에 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-456">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # <b>Online: [ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Clone Set: cln_SAPHanaTopology_HDB_HDB03 [rsc_SAPHanaTopology_HDB_HDB03]
   #      <b>Started: [ nws-cl-0 nws-cl-1 ]</b>
   #  Master/Slave Set: msl_SAPHana_HDB_HDB03 [rsc_SAPHana_HDB_HDB03]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g_ip_HDB_HDB03
   #      rsc_ip_HDB_HDB03   (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      rsc_nc_HDB_HDB03   (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   # rsc_st_azure_1  (stonith:fence_azure_arm):      <b>Started nws-cl-0</b>
   # rsc_st_azure_2  (stonith:fence_azure_arm):      <b>Started nws-cl-1</b>
   </code></pre>

1. <span data-ttu-id="f7c63-457">**[1]**  설치 hello SAP NetWeaver 데이터베이스 인스턴스</span><span class="sxs-lookup"><span data-stu-id="f7c63-457">**[1]** Install hello SAP NetWeaver database instance</span></span>

   <span data-ttu-id="f7c63-458">예를 들어 hello hello 데이터베이스에 대 한 부하 분산 장치 프런트 엔드 구성의 toohello IP 주소를 매핑하는 가상 호스트 이름을 사용 하 여 루트로 설치 hello SAP NetWeaver 데이터베이스 인스턴스 <b>nws db</b> 및 <b>10.0.0.12</b>.</span><span class="sxs-lookup"><span data-stu-id="f7c63-458">Install hello SAP NetWeaver database instance as root using a virtual hostname that maps toohello IP address of hello load balancer frontend configuration for hello database for example <b>nws-db</b> and <b>10.0.0.12</b>.</span></span>

   <span data-ttu-id="f7c63-459">Hello sapinst 매개 변수 SAPINST_REMOTE_ACCESS_USER tooallow 루트가 아닌 사용자 tooconnect toosapinst를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-459">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

## <a name="sap-netweaver-application-server-installation"></a><span data-ttu-id="f7c63-460">SAP NetWeaver 응용 프로그램 서버 설치</span><span class="sxs-lookup"><span data-stu-id="f7c63-460">SAP NetWeaver application server installation</span></span>

<span data-ttu-id="f7c63-461">이러한 단계 tooinstall SAP 응용 프로그램 서버를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-461">Follow these steps tooinstall an SAP application server.</span></span> <span data-ttu-id="f7c63-462">hello 단계 아래 hello ASCS/SCS와에서 다른 서버에 응용 프로그램 서버 hello 및 HANA 서버 설치 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-462">hello steps bellow assume that you install hello application server on a server different from hello ASCS/SCS and HANA servers.</span></span> <span data-ttu-id="f7c63-463">그렇지 않은 경우 (예: 호스트 이름 확인 구성)는 다음 hello 단계 중 일부는 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-463">Otherwise some of hello steps below (like configuring host name resolution) are not needed.</span></span>

1. <span data-ttu-id="f7c63-464">호스트 이름 확인 설정</span><span class="sxs-lookup"><span data-stu-id="f7c63-464">Setup host name resolution</span></span>    
   <span data-ttu-id="f7c63-465">DNS 서버를 사용 하거나 모든 노드에서 hello /etc/hosts 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-465">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="f7c63-466">이 예제에서는 toouse /etc/hosts 파일 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-466">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="f7c63-467">Hello IP 주소와 hello 명령 뒤에 hello 호스트 이름 바꾸기</span><span class="sxs-lookup"><span data-stu-id="f7c63-467">Replace hello IP address and hello hostname in hello following commands</span></span>
   ```bash
   sudo vi /etc/hosts
   ```
   <span data-ttu-id="f7c63-468">다음 줄 너무/등/호스트 hello를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-468">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="f7c63-469">IP 주소 및 호스트 이름 toomatch hello 환경 변경</span><span class="sxs-lookup"><span data-stu-id="f7c63-469">Change hello IP address and hostname toomatch your environment</span></span>    
    
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   # IP address of hello application server
   <b>10.0.0.8 nws-di-0</b>
   </code></pre>

1. <span data-ttu-id="f7c63-470">Hello sapmnt 디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="f7c63-470">Create hello sapmnt directory</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   </code></pre>

1. <span data-ttu-id="f7c63-471">autofs를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-471">Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="f7c63-472">다음 코드를 사용하여 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-472">Create a new file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   </code></pre>

   <span data-ttu-id="f7c63-473">Autofs toomount hello 새 공유를 다시 시작</span><span class="sxs-lookup"><span data-stu-id="f7c63-473">Restart autofs toomount hello new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="f7c63-474">스왑 파일을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-474">Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="f7c63-475">Hello 에이전트 tooactivate hello 변경 다시 시작</span><span class="sxs-lookup"><span data-stu-id="f7c63-475">Restart hello Agent tooactivate hello change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

1. <span data-ttu-id="f7c63-476">SAP NetWeaver 응용 프로그램 서버 설치</span><span class="sxs-lookup"><span data-stu-id="f7c63-476">Install SAP NetWeaver application server</span></span>

   <span data-ttu-id="f7c63-477">기본 또는 추가 SAP NetWeaver 응용 프로그램 서버를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-477">Install a primary or additional SAP NetWeaver applications server.</span></span>

   <span data-ttu-id="f7c63-478">Hello sapinst 매개 변수 SAPINST_REMOTE_ACCESS_USER tooallow 루트가 아닌 사용자 tooconnect toosapinst를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-478">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="f7c63-479">SAP HANA 보안 저장소 업데이트</span><span class="sxs-lookup"><span data-stu-id="f7c63-479">Update SAP HANA secure store</span></span>

   <span data-ttu-id="f7c63-480">SAP HANA 보안 업데이트 hello toopoint toohello hello SAP HANA 시스템 복제 설치 프로그램의 가상 이름을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-480">Update hello SAP HANA secure store toopoint toohello virtual name of hello SAP HANA System Replication setup.</span></span>
   <pre><code>
   su - <b>nws</b>adm
   hdbuserstore SET DEFAULT <b>nws-db</b>:3<b>03</b>15 <b>SAPABAP1</b> <b>&lt;password of ABAP schema&gt;</b>
   </code></pre>

## <a name="next-steps"></a><span data-ttu-id="f7c63-481">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f7c63-481">Next steps</span></span>
* <span data-ttu-id="f7c63-482">[SAP용 Azure Virtual Machines 계획 및 구현][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="f7c63-482">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="f7c63-483">[SAP용 Azure Virtual Machines 배포][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="f7c63-483">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="f7c63-484">[SAP용 Azure Virtual Machines DBMS 배포][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="f7c63-484">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="f7c63-485">tooestablish 고가용성 및 (대형 인스턴스) Azure에서 SAP HANA의 재해 복구 계획의 참조 toolearn [SAP HANA (대형 인스턴스) 고가용성 및 재해 복구 Azure에서](hana-overview-high-availability-disaster-recovery.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c63-485">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span>
* <span data-ttu-id="f7c63-486">tooestablish 고가용성 및 Azure Vm에서 SAP HANA의 재해 복구 계획의 참조 toolearn [SAP HANA의 높은 가용성 Azure 가상 컴퓨터 (Vm)에서][sap-hana-ha]</span><span class="sxs-lookup"><span data-stu-id="f7c63-486">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure VMs, see [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha]</span></span>
