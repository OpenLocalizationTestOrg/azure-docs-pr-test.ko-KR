---
title: "SAP 응용 프로그램용 SUSE Linux Enterprise Server의 SAP NetWeaver에 대한 Azure Virtual Machines 고가용성 | Microsoft 문서"
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
ms.openlocfilehash: 16e09797926f29bc18cb05671c986c74f9c2d4f8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms-on-suse-linux-enterprise-server-for-sap-applications"></a><span data-ttu-id="33635-103">SAP 응용 프로그램용 SUSE Linux Enterprise Server의 Azure VM에 있는 SAP NetWeaver에 대한 고가용성</span><span class="sxs-lookup"><span data-stu-id="33635-103">High availability for SAP NetWeaver on Azure VMs on SUSE Linux Enterprise Server for SAP applications</span></span>

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

<span data-ttu-id="33635-104">[2205917]:https://launchpad.support.sap.com/#/notes/2205917</span><span class="sxs-lookup"><span data-stu-id="33635-104">[2205917]:https://launchpad.support.sap.com/#/notes/2205917</span></span>
<span data-ttu-id="33635-105">[1944799]:https://launchpad.support.sap.com/#/notes/1944799</span><span class="sxs-lookup"><span data-stu-id="33635-105">[1944799]:https://launchpad.support.sap.com/#/notes/1944799</span></span>
<span data-ttu-id="33635-106">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span><span class="sxs-lookup"><span data-stu-id="33635-106">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span></span>
<span data-ttu-id="33635-107">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span><span class="sxs-lookup"><span data-stu-id="33635-107">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span></span>
<span data-ttu-id="33635-108">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span><span class="sxs-lookup"><span data-stu-id="33635-108">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span></span>
<span data-ttu-id="33635-109">[2191498]:https://launchpad.support.sap.com/#/notes/2191498</span><span class="sxs-lookup"><span data-stu-id="33635-109">[2191498]:https://launchpad.support.sap.com/#/notes/2191498</span></span>
<span data-ttu-id="33635-110">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span><span class="sxs-lookup"><span data-stu-id="33635-110">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span></span>
<span data-ttu-id="33635-111">[1984787]:https://launchpad.support.sap.com/#/notes/1984787</span><span class="sxs-lookup"><span data-stu-id="33635-111">[1984787]:https://launchpad.support.sap.com/#/notes/1984787</span></span>
<span data-ttu-id="33635-112">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span><span class="sxs-lookup"><span data-stu-id="33635-112">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span></span>
[1410736]:https://launchpad.support.sap.com/#/notes/1410736

[sap-swcenter]:https://support.sap.com/en/my-support/software-downloads.html

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[suse-drbd-guide]:https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha_techguides/book_sleha_techguides.html

[template-multisid-xscs]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged-md%2Fazuredeploy.json
[template-file-server]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-file-server-md%2Fazuredeploy.json

[sap-hana-ha]:sap-hana-high-availability.md

<span data-ttu-id="33635-113">이 문서에서는 가상 컴퓨터를 배포 및 구성하고 클러스터 프레임워크 및 고가용성 SAP NetWeaver 7.50 시스템을 설치하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-113">This article describes how to deploy the virtual machines, configure the virtual machines, install the cluster framework and install a highly available SAP NetWeaver 7.50 system.</span></span>
<span data-ttu-id="33635-114">그리고 예제 구성, 설치 명령 등을 소개합니다. 여기서는 ASCS 인스턴스 번호 00, ERS 인스턴스 번호 02 및 SAP 시스템 ID NWS를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-114">In the example configurations, installation commands etc. ASCS instance number 00, ERS instance number 02 and SAP System ID NWS is used.</span></span> <span data-ttu-id="33635-115">예제에 포함된 가상 컴퓨터, 가상 네트워크 등의 리소스 이름은 SAP 시스템 ID가 NWS인 [수렴형 템플릿][template-converged]을 사용하여 리소스를 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-115">The names of the resources (for example virtual machines, virtual networks) in the example assume that you have used the [converged template][template-converged] with SAP system ID NWS to create the resources.</span></span>

<span data-ttu-id="33635-116">먼저 다음 SAP 참고와 문서 읽기</span><span class="sxs-lookup"><span data-stu-id="33635-116">Read the following SAP Notes and papers first</span></span>

* <span data-ttu-id="33635-117">SAP Note [1928533], 다음 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-117">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="33635-118">SAP 소프트웨어 배포에 지원되는 Azure VM 크기 목록</span><span class="sxs-lookup"><span data-stu-id="33635-118">List of Azure VM sizes that are supported for the deployment of SAP software</span></span>
  * <span data-ttu-id="33635-119">Azure VM 크기에 대한 중요한 용량 정보</span><span class="sxs-lookup"><span data-stu-id="33635-119">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="33635-120">지원되는 SAP 소프트웨어 및 운영 체제(OS)와 데이터베이스 조합</span><span class="sxs-lookup"><span data-stu-id="33635-120">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="33635-121">Microsoft Azure에서 Windows 및 Linux에 필요한 SAP 커널 버전</span><span class="sxs-lookup"><span data-stu-id="33635-121">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>

* <span data-ttu-id="33635-122">SAP Note [2015553]는 Azure에서 SAP을 지원하는 SAP 소프트웨어 배포에 대한 필수 구성 요소를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-122">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="33635-123">SAP Note [2205917]에는 SAP 응용 프로그램용 SUSE Linux Enterprise Server에 권장되는 OS 설정이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-123">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="33635-124">SAP Note [1944799]에는 SAP 응용 프로그램용 SUSE Linux Enterprise Server에 대한 SAP HANA 지침이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-124">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="33635-125">SAP Note [2178632]는 Azure에서 SAP에 대해 보고된 모든 모니터링 메트릭에 대한 자세한 정보를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-125">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="33635-126">SAP Note [2191498]는 Azure에서 Linux에 필요한 SAP Host Agent 버전을 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-126">SAP Note [2191498] has the required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="33635-127">SAP Note [2243692]는 Azure에서 Linux의 SAP 라이선스에 대한 정보를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-127">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="33635-128">SAP Note [1984787]은 SUSE LINUX Enterprise Server 12에 대한 일반 정보를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-128">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="33635-129">SAP Note [1999351]은 SAP용 Azure 고급 모니터링 확장을 위한 추가 문제 해결 정보를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-129">SAP Note [1999351] has additional troubleshooting information for the Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="33635-130">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes)는 Linux에 필요한 모든 SAP Note를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-130">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="33635-131">[Linux에서 SAP용 Azure Virtual Machines 계획 및 구현][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="33635-131">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="33635-132">[Linux에서 SAP용 Azure Virtual Machines 배포(이 문서)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="33635-132">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="33635-133">[Linux에서 SAP용 Azure Virtual Machines DBMS 배포][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="33635-133">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="33635-134">[SAP HANA SR 성능 최적화된 시나리오][suse-hana-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="33635-134">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide]</span></span>  
  <span data-ttu-id="33635-135">이 가이드에는 온-프레미스에 SAP HANA 시스템 복제를 설정하는 데 필요한 모든 정보가 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-135">The guide contains all required information to set up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="33635-136">이 가이드를 기준으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-136">Use this guide as a baseline.</span></span>
* <span data-ttu-id="33635-137">[DRBD 및 Pacemaker를 사용하는 고가용성 NFS 저장소][suse-drbd-guide] 이 가이드에는 고가용성 NFS 서버를 설정하는 데 필요한 모든 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-137">[Highly Available NFS Storage with DRBD and Pacemaker][suse-drbd-guide] The guide contains all required information to set up a highly available NFS server.</span></span> <span data-ttu-id="33635-138">이 가이드를 기준으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-138">Use this guide as a baseline.</span></span>


## <a name="overview"></a><span data-ttu-id="33635-139">개요</span><span class="sxs-lookup"><span data-stu-id="33635-139">Overview</span></span>

<span data-ttu-id="33635-140">SAP NetWeaver의 가용성을 높이려면 NFS 서버가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-140">To achieve high availability, SAP NetWeaver requires an NFS server.</span></span> <span data-ttu-id="33635-141">NFS 서버는 별도의 클러스터에서 구성되며, 여러 SAP 시스템에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-141">The NFS server is configured in a separate cluster and can be used by multiple SAP systems.</span></span>

![SAP NetWeaver 고가용성 개요](./media/high-availability-guide-suse/img_001.png)

<span data-ttu-id="33635-143">NFS 서버, SAP NetWeaver ASCS, SAP NetWeaver SCS, SAP NetWeaver ERS 및 SAP HANA 데이터베이스는 가상 호스트 이름 및 가상 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-143">The NFS server, SAP NetWeaver ASCS, SAP NetWeaver SCS, SAP NetWeaver ERS and the SAP HANA database use virtual hostname and virtual IP addresses.</span></span> <span data-ttu-id="33635-144">Azure에서는 가상 IP 주소를 사용하려면 부하 분산 장치가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-144">On Azure, a load balancer is required to use a virtual IP address.</span></span> <span data-ttu-id="33635-145">아래 목록에는 부하 분산 장치 구성이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-145">The following list shows the configuration of the load balancer.</span></span>

### <a name="nfs-server"></a><span data-ttu-id="33635-146">NFS 서버</span><span class="sxs-lookup"><span data-stu-id="33635-146">NFS Server</span></span>
* <span data-ttu-id="33635-147">프런트 엔드 구성</span><span class="sxs-lookup"><span data-stu-id="33635-147">Frontend configuration</span></span>
  * <span data-ttu-id="33635-148">IP 주소 10.0.0.4</span><span class="sxs-lookup"><span data-stu-id="33635-148">IP address 10.0.0.4</span></span>
* <span data-ttu-id="33635-149">백 엔드 구성</span><span class="sxs-lookup"><span data-stu-id="33635-149">Backend configuration</span></span>
  * <span data-ttu-id="33635-150">NFS 클러스터의 일부분이어야 하는 모든 가상 컴퓨터의 주 네트워크 인터페이스에 연결됨</span><span class="sxs-lookup"><span data-stu-id="33635-150">Connected to primary network interfaces of all virtual machines that should be part of the NFS cluster</span></span>
* <span data-ttu-id="33635-151">프로브 포트</span><span class="sxs-lookup"><span data-stu-id="33635-151">Probe Port</span></span>
  * <span data-ttu-id="33635-152">포트 61000</span><span class="sxs-lookup"><span data-stu-id="33635-152">Port 61000</span></span>
* <span data-ttu-id="33635-153">부하 분산 규칙</span><span class="sxs-lookup"><span data-stu-id="33635-153">Loadbalancing rules</span></span>
  * <span data-ttu-id="33635-154">2049 TCP</span><span class="sxs-lookup"><span data-stu-id="33635-154">2049 TCP</span></span> 
  * <span data-ttu-id="33635-155">2049 UDP</span><span class="sxs-lookup"><span data-stu-id="33635-155">2049 UDP</span></span>

### <a name="ascs"></a><span data-ttu-id="33635-156">(A)SCS</span><span class="sxs-lookup"><span data-stu-id="33635-156">(A)SCS</span></span>
* <span data-ttu-id="33635-157">프런트 엔드 구성</span><span class="sxs-lookup"><span data-stu-id="33635-157">Frontend configuration</span></span>
  * <span data-ttu-id="33635-158">IP 주소 10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="33635-158">IP address 10.0.0.10</span></span>
* <span data-ttu-id="33635-159">백 엔드 구성</span><span class="sxs-lookup"><span data-stu-id="33635-159">Backend configuration</span></span>
  * <span data-ttu-id="33635-160">(A)SCS/ERS 클러스터의 일부분이어야 하는 모든 가상 컴퓨터의 주 네트워크 인터페이스에 연결됨</span><span class="sxs-lookup"><span data-stu-id="33635-160">Connected to primary network interfaces of all virtual machines that should be part of the (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="33635-161">프로브 포트</span><span class="sxs-lookup"><span data-stu-id="33635-161">Probe Port</span></span>
  * <span data-ttu-id="33635-162">포트 620**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="33635-162">Port 620**&lt;nr&gt;**</span></span>
* <span data-ttu-id="33635-163">부하 분산 규칙</span><span class="sxs-lookup"><span data-stu-id="33635-163">Loadbalancing rules</span></span>
  * <span data-ttu-id="33635-164">32**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="33635-164">32**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="33635-165">36**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="33635-165">36**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="33635-166">39**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="33635-166">39**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="33635-167">81**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="33635-167">81**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="33635-168">5**&lt;nr&gt;**13 TCP</span><span class="sxs-lookup"><span data-stu-id="33635-168">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="33635-169">5**&lt;nr&gt;**14 TCP</span><span class="sxs-lookup"><span data-stu-id="33635-169">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="33635-170">5**&lt;nr&gt;**16 TCP</span><span class="sxs-lookup"><span data-stu-id="33635-170">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="ers"></a><span data-ttu-id="33635-171">ERS</span><span class="sxs-lookup"><span data-stu-id="33635-171">ERS</span></span>
* <span data-ttu-id="33635-172">프런트 엔드 구성</span><span class="sxs-lookup"><span data-stu-id="33635-172">Frontend configuration</span></span>
  * <span data-ttu-id="33635-173">IP 주소 10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="33635-173">IP address 10.0.0.11</span></span>
* <span data-ttu-id="33635-174">백 엔드 구성</span><span class="sxs-lookup"><span data-stu-id="33635-174">Backend configuration</span></span>
  * <span data-ttu-id="33635-175">(A)SCS/ERS 클러스터의 일부분이어야 하는 모든 가상 컴퓨터의 주 네트워크 인터페이스에 연결됨</span><span class="sxs-lookup"><span data-stu-id="33635-175">Connected to primary network interfaces of all virtual machines that should be part of the (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="33635-176">프로브 포트</span><span class="sxs-lookup"><span data-stu-id="33635-176">Probe Port</span></span>
  * <span data-ttu-id="33635-177">포트 621**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="33635-177">Port 621**&lt;nr&gt;**</span></span>
* <span data-ttu-id="33635-178">부하 분산 규칙</span><span class="sxs-lookup"><span data-stu-id="33635-178">Loadbalancing rules</span></span>
  * <span data-ttu-id="33635-179">33**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="33635-179">33**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="33635-180">5**&lt;nr&gt;**13 TCP</span><span class="sxs-lookup"><span data-stu-id="33635-180">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="33635-181">5**&lt;nr&gt;**14 TCP</span><span class="sxs-lookup"><span data-stu-id="33635-181">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="33635-182">5**&lt;nr&gt;**16 TCP</span><span class="sxs-lookup"><span data-stu-id="33635-182">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="sap-hana"></a><span data-ttu-id="33635-183">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="33635-183">SAP HANA</span></span>
* <span data-ttu-id="33635-184">프런트 엔드 구성</span><span class="sxs-lookup"><span data-stu-id="33635-184">Frontend configuration</span></span>
  * <span data-ttu-id="33635-185">IP 주소 10.0.0.12</span><span class="sxs-lookup"><span data-stu-id="33635-185">IP address 10.0.0.12</span></span>
* <span data-ttu-id="33635-186">백 엔드 구성</span><span class="sxs-lookup"><span data-stu-id="33635-186">Backend configuration</span></span>
  * <span data-ttu-id="33635-187">HANA 클러스터의 일부분이어야 하는 모든 가상 컴퓨터의 주 네트워크 인터페이스에 연결됨</span><span class="sxs-lookup"><span data-stu-id="33635-187">Connected to primary network interfaces of all virtual machines that should be part of the HANA cluster</span></span>
* <span data-ttu-id="33635-188">프로브 포트</span><span class="sxs-lookup"><span data-stu-id="33635-188">Probe Port</span></span>
  * <span data-ttu-id="33635-189">포트 625**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="33635-189">Port 625**&lt;nr&gt;**</span></span>
* <span data-ttu-id="33635-190">부하 분산 규칙</span><span class="sxs-lookup"><span data-stu-id="33635-190">Loadbalancing rules</span></span>
  * <span data-ttu-id="33635-191">3**&lt;nr&gt;**15 TCP</span><span class="sxs-lookup"><span data-stu-id="33635-191">3**&lt;nr&gt;**15 TCP</span></span>
  * <span data-ttu-id="33635-192">3**&lt;nr&gt;**17 TCP</span><span class="sxs-lookup"><span data-stu-id="33635-192">3**&lt;nr&gt;**17 TCP</span></span>

## <a name="setting-up-a-highly-available-nfs-server"></a><span data-ttu-id="33635-193">고가용성 NFS 서버 설정</span><span class="sxs-lookup"><span data-stu-id="33635-193">Setting up a highly available NFS server</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="33635-194">Linux 배포</span><span class="sxs-lookup"><span data-stu-id="33635-194">Deploying Linux</span></span>

<span data-ttu-id="33635-195">Azure Marketplace에는 새 가상 컴퓨터를 배포하는 데 사용할 수 있는 SAP Applications 12용 SUSE Linux Enterprise Server의 이미지가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-195">The Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use to deploy new virtual machines.</span></span>
<span data-ttu-id="33635-196">Github에서 빠른 시작 템플릿 중 하나를 사용하여 필요한 모든 리소스를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-196">You can use one of the quick start templates on github to deploy all required resources.</span></span> <span data-ttu-id="33635-197">템플릿에서 가상 컴퓨터, 부하 분산 장치, 가용성 집합 등을 배포합니다. 다음 단계를 따라 템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-197">The template deploys the virtual machines, the load balancer, availability set etc. Follow these steps to deploy the template:</span></span>

1. <span data-ttu-id="33635-198">Azure Portal에서 [SAP 파일 서버 템플릿][template-file-server]을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="33635-198">Open the [SAP file server template][template-file-server] in the Azure portal</span></span>   
1. <span data-ttu-id="33635-199">다음 매개 변수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-199">Enter the following parameters</span></span>
   1. <span data-ttu-id="33635-200">리소스 접두사 -</span><span class="sxs-lookup"><span data-stu-id="33635-200">Resource Prefix</span></span>  
      <span data-ttu-id="33635-201">사용할 접두사를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-201">Enter the prefix you want to use.</span></span> <span data-ttu-id="33635-202">이 값은 배포되는 리소스의 접두사로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="33635-202">The value is used as a prefix for the resources that are deployed.</span></span>
   2. <span data-ttu-id="33635-203">OS 종류 -</span><span class="sxs-lookup"><span data-stu-id="33635-203">Os Type</span></span>  
      <span data-ttu-id="33635-204">Linux 배포판 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-204">Select one of the Linux distributions.</span></span> <span data-ttu-id="33635-205">이 예제에서는 SLES 12를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-205">For this example, select SLES 12</span></span>
   3. <span data-ttu-id="33635-206">관리자 사용자 이름 및 관리자 암호 -</span><span class="sxs-lookup"><span data-stu-id="33635-206">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="33635-207">컴퓨터에 로그온하는 데 사용할 수 있게 만들어진 새 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="33635-207">A new user is created that can be used to log on to the machine.</span></span>
   4. <span data-ttu-id="33635-208">서브넷 ID -</span><span class="sxs-lookup"><span data-stu-id="33635-208">Subnet Id</span></span>  
      <span data-ttu-id="33635-209">가상 컴퓨터를 연결해야 하는 서브넷의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="33635-209">The ID of the subnet to which the virtual machines should be connected to.</span></span> <span data-ttu-id="33635-210">새 가상 네트워크를 만들려는 경우 비워 두거나, 가상 컴퓨터를 온-프레미스 네트워크에 연결하려는 경우 VPN 또는 ExpressRoute 가상 네트워크의 서브넷을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-210">Leave empty if you want to create a new virtual network or select the subnet of your VPN or Express Route virtual network to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="33635-211">ID는 대개 /subscriptions/**&lt;구독 ID&gt;**/resourceGroups/**&lt;리소스 그룹 이름&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;가상 네트워크 이름&gt;**/subnets/**&lt;서브넷 이름&gt;**과 같은 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="33635-211">The ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="33635-212">설치</span><span class="sxs-lookup"><span data-stu-id="33635-212">Installation</span></span>

<span data-ttu-id="33635-213">다음 항목에는 접두사 **[A]**(모든 노드에 적용됨), **[1]**(노드 1에만 적용됨), **[2]**(노드 2에만 적용됨) 접두사가 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-213">The following items are prefixed with either **[A]** - applicable to all nodes, **[1]** - only applicable to node 1 or **[2]** - only applicable to node 2.</span></span>

1. <span data-ttu-id="33635-214">**[A]** SLES 업데이트</span><span class="sxs-lookup"><span data-stu-id="33635-214">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="33635-215">**[1]** ssh 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="33635-215">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy the public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="33635-216">**[2]** ssh 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="33635-216">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert the public key you copied in the last step into the authorized keys file on the second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy the public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="33635-217">**[1]** ssh 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="33635-217">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert the public key you copied in the last step into the authorized keys file on the first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="33635-218">**[A]** HA 확장 설치</span><span class="sxs-lookup"><span data-stu-id="33635-218">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="33635-219">**[A]** 호스트 이름 확인 설정</span><span class="sxs-lookup"><span data-stu-id="33635-219">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="33635-220">DNS 서버를 사용하거나 모든 노드의 /etc/hosts를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-220">You can either use a DNS server or modify the /etc/hosts on all nodes.</span></span> <span data-ttu-id="33635-221">이 예에서는 /etc/hosts 파일 사용 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="33635-221">This example shows how to use the /etc/hosts file.</span></span>
   <span data-ttu-id="33635-222">다음 명령에서 IP 주소와 호스트 이름 바꾸기</span><span class="sxs-lookup"><span data-stu-id="33635-222">Replace the IP address and the hostname in the following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="33635-223">다음 줄을 /etc/hosts에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-223">Insert the following lines to /etc/hosts.</span></span> <span data-ttu-id="33635-224">환경에 맞게 IP 주소와 호스트 이름 변경</span><span class="sxs-lookup"><span data-stu-id="33635-224">Change the IP address and hostname to match your environment</span></span>   
   
   <pre><code>
   # IP address of the load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   </code></pre>

1. <span data-ttu-id="33635-225">**[1]** 클러스터 설치</span><span class="sxs-lookup"><span data-stu-id="33635-225">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want to continue anyway? [y/N] -> y
   # Network address to bind to (for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish to use SBD? [y/N] -> N
   # Do you wish to configure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="33635-226">**[2]** 클러스터에 노드 추가</span><span class="sxs-lookup"><span data-stu-id="33635-226">**[2]** Add node to cluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured to start at system boot.
   # WARNING: No watchdog device found. If SBD is used, the cluster will be unable to start without a watchdog.
   # Do you want to continue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="33635-227">**[A]** hacluster 암호를 동일한 암호로 변경</span><span class="sxs-lookup"><span data-stu-id="33635-227">**[A]** Change hacluster password to the same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="33635-228">**[A]** 다른 전송을 사용하고 nodelist를 추가하도록 corosync 구성.</span><span class="sxs-lookup"><span data-stu-id="33635-228">**[A]** Configure corosync to use other transport and add nodelist.</span></span> <span data-ttu-id="33635-229">그렇지 않으면 클러스터가 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-229">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="33635-230">굵은체로 된 다음 콘텐츠를 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-230">Add the following bold content to the file.</span></span>
   
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

   <span data-ttu-id="33635-231">그런 다음 corosync 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-231">Then restart the corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="33635-232">**[A]** drbd 구성 요소 설치</span><span class="sxs-lookup"><span data-stu-id="33635-232">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="33635-233">**[A]** drbd 장치용 파티션 만들기</span><span class="sxs-lookup"><span data-stu-id="33635-233">**[A]** Create a partition for the drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="33635-234">**[A]** LVM 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="33635-234">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_NFS /dev/sdc1
   sudo lvcreate -l 100%FREE -n <b>NWS</b> vg_NFS
   </code></pre>

1. <span data-ttu-id="33635-235">**[A]** NFS drbd 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="33635-235">**[A]** Create the NFS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_nfs.res
   </code></pre>

   <span data-ttu-id="33635-236">새 drbd 장치용 구성을 삽입하고 명령을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-236">Insert the configuration for the new drbd device and exit</span></span>

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

   <span data-ttu-id="33635-237">drbd 장치를 만들어 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-237">Create the drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_nfs
   sudo drbdadm up <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="33635-238">**[1]** 초기 동기화 건너뛰기</span><span class="sxs-lookup"><span data-stu-id="33635-238">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="33635-239">**[1]** 주 노드 설정</span><span class="sxs-lookup"><span data-stu-id="33635-239">**[1]** Set the primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="33635-240">**[1]** 새 drbd 장치가 동기화될 때까지 대기</span><span class="sxs-lookup"><span data-stu-id="33635-240">**[1]** Wait until the new drbd devices are synchronized</span></span>

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:Connected ro:Primary/Secondary ds:UpToDate/UpToDate C r-----
   #    ns:0 nr:0 dw:0 dr:912 al:8 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. <span data-ttu-id="33635-241">**[1]** drbd 장치에서 파일 시스템 만들기</span><span class="sxs-lookup"><span data-stu-id="33635-241">**[1]** Create file systems on the drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="33635-242">클러스터 프레임워크 구성</span><span class="sxs-lookup"><span data-stu-id="33635-242">Configure Cluster Framework</span></span>

1. <span data-ttu-id="33635-243">**[1]** 기본 설정 변경</span><span class="sxs-lookup"><span data-stu-id="33635-243">**[1]** Change the default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="33635-244">**[1]** 클러스터 구성에 NFS drbd 장치 추가</span><span class="sxs-lookup"><span data-stu-id="33635-244">**[1]** Add the NFS drbd device to the cluster configuration</span></span>

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

1. <span data-ttu-id="33635-245">**[1]** NFS 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="33635-245">**[1]** Create the NFS server</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive nfsserver \
     systemd:nfs-server \
     op monitor interval="30s"

   crm(live)configure# clone cl-nfsserver nfsserver interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="33635-246">**[1]** NFS 파일 시스템 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="33635-246">**[1]** Create the NFS File System resources</span></span>

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

1. <span data-ttu-id="33635-247">**[1]** NFS 내보내기 만들기</span><span class="sxs-lookup"><span data-stu-id="33635-247">**[1]** Create the NFS exports</span></span>

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

1. <span data-ttu-id="33635-248">**[1]** 내부 부하 분산 장치용 가상 IP 리소스 및 상태 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="33635-248">**[1]** Create a virtual IP resource and health-probe for the internal load balancer</span></span>

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

### <a name="create-stonith-device"></a><span data-ttu-id="33635-249">STONITH 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="33635-249">Create STONITH device</span></span>

<span data-ttu-id="33635-250">STONITH 장치에서는 서비스 주체를 사용하여 Microsoft Azure에 대해 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-250">The STONITH device uses a Service Principal to authorize against Microsoft Azure.</span></span> <span data-ttu-id="33635-251">다음 단계에 따라 서비스 주체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33635-251">Follow these steps to create a Service Principal.</span></span>

1. <span data-ttu-id="33635-252"><https://portal.azure.com>으로 이동</span><span class="sxs-lookup"><span data-stu-id="33635-252">Go to <https://portal.azure.com></span></span>
1. <span data-ttu-id="33635-253">Azure Active Directory 블레이드 열기</span><span class="sxs-lookup"><span data-stu-id="33635-253">Open the Azure Active Directory blade</span></span>  
   <span data-ttu-id="33635-254">속성으로 이동하여 Directory ID 기록</span><span class="sxs-lookup"><span data-stu-id="33635-254">Go to Properties and write down the Directory Id.</span></span> <span data-ttu-id="33635-255">이 ID는 **테넌트 ID**입니다.</span><span class="sxs-lookup"><span data-stu-id="33635-255">This is the **tenant id**.</span></span>
1. <span data-ttu-id="33635-256">앱 등록 클릭</span><span class="sxs-lookup"><span data-stu-id="33635-256">Click App registrations</span></span>
1. <span data-ttu-id="33635-257">추가를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-257">Click Add</span></span>
1. <span data-ttu-id="33635-258">이름을 입력하고 응용 프로그램 유형 "Web app/API"를 선택한 다음 로그온 URL(예: http://localhost )을 입력하고 만들기를 클릭</span><span class="sxs-lookup"><span data-stu-id="33635-258">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="33635-259">로그온 URL이 사용되지 않으며, 이 URL은 임의의 올바른 URL이 될 수 있음</span><span class="sxs-lookup"><span data-stu-id="33635-259">The sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="33635-260">새 앱을 선택하고 설정 탭에서 키 클릭</span><span class="sxs-lookup"><span data-stu-id="33635-260">Select the new App and click Keys in the Settings tab</span></span>
1. <span data-ttu-id="33635-261">새 키의 설명을 입력하고 “만료되지 않음”을 선택한 다음 저장을 클릭</span><span class="sxs-lookup"><span data-stu-id="33635-261">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="33635-262">값을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="33635-262">Write down the Value.</span></span> <span data-ttu-id="33635-263">서비스 주체의 **암호**로 사용됨</span><span class="sxs-lookup"><span data-stu-id="33635-263">It is used as the **password** for the Service Principal</span></span>
1. <span data-ttu-id="33635-264">응용 프로그램 ID를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="33635-264">Write down the Application Id.</span></span> <span data-ttu-id="33635-265">서비스 주체의 사용자 이름(아래 단계의 **로그인 id**)으로 사용됨</span><span class="sxs-lookup"><span data-stu-id="33635-265">It is used as the username (**login id** in the steps below) of the Service Principal</span></span>

<span data-ttu-id="33635-266">서비스 주체에는 기본적으로 Azure 리소스에 액세스할 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-266">The Service Principal does not have permissions to access your Azure resources by default.</span></span> <span data-ttu-id="33635-267">서비스 주체에 클러스터의 모든 가상 컴퓨터를 시작 및 중지(할당 취소)하기 위한 권한을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-267">You need to give the Service Principal permissions to start and stop (deallocate) all virtual machines of the cluster.</span></span>

1. <span data-ttu-id="33635-268">https://portal.azure.com으로 이동</span><span class="sxs-lookup"><span data-stu-id="33635-268">Go to https://portal.azure.com</span></span>
1. <span data-ttu-id="33635-269">모든 리소스 블레이드 열기</span><span class="sxs-lookup"><span data-stu-id="33635-269">Open the All resources blade</span></span>
1. <span data-ttu-id="33635-270">가상 컴퓨터 선택</span><span class="sxs-lookup"><span data-stu-id="33635-270">Select the virtual machine</span></span>
1. <span data-ttu-id="33635-271">액세스 제어(IAM) 클릭</span><span class="sxs-lookup"><span data-stu-id="33635-271">Click Access control (IAM)</span></span>
1. <span data-ttu-id="33635-272">추가를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-272">Click Add</span></span>
1. <span data-ttu-id="33635-273">소유자 역할 선택</span><span class="sxs-lookup"><span data-stu-id="33635-273">Select the role Owner</span></span>
1. <span data-ttu-id="33635-274">위에서 만든 응용 프로그램의 이름 입력</span><span class="sxs-lookup"><span data-stu-id="33635-274">Enter the name of the application you created above</span></span>
1. <span data-ttu-id="33635-275">확인 클릭</span><span class="sxs-lookup"><span data-stu-id="33635-275">Click OK</span></span>

#### <a name="1-create-the-stonith-devices"></a><span data-ttu-id="33635-276">**[1]** STONITH 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="33635-276">**[1]** Create the STONITH devices</span></span>

<span data-ttu-id="33635-277">가상 컴퓨터의 권한을 편집하고 나면 클러스터의 STONITH 장치를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-277">After you edited the permissions for the virtual machines, you can configure the STONITH devices in the cluster.</span></span>

<pre><code>
sudo crm configure

# replace the bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-the-use-of-a-stonith-device"></a><span data-ttu-id="33635-278">**[1]** STONITH 장치를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="33635-278">**[1]** Enable the use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="setting-up-ascs"></a><span data-ttu-id="33635-279">(A)SCS 설정</span><span class="sxs-lookup"><span data-stu-id="33635-279">Setting up (A)SCS</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="33635-280">Linux 배포</span><span class="sxs-lookup"><span data-stu-id="33635-280">Deploying Linux</span></span>

<span data-ttu-id="33635-281">Azure Marketplace에는 새 가상 컴퓨터를 배포하는 데 사용할 수 있는 SAP Applications 12용 SUSE Linux Enterprise Server의 이미지가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-281">The Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use to deploy new virtual machines.</span></span> <span data-ttu-id="33635-282">Marketplace 이미지는 SAP NetWeaver용 리소스 에이전트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-282">The marketplace image contains the resource agent for SAP NetWeaver.</span></span>

<span data-ttu-id="33635-283">Github에서 빠른 시작 템플릿 중 하나를 사용하여 필요한 모든 리소스를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-283">You can use one of the quick start templates on github to deploy all required resources.</span></span> <span data-ttu-id="33635-284">템플릿에서 가상 컴퓨터, 부하 분산 장치, 가용성 집합 등을 배포합니다. 다음 단계를 따라 템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-284">The template deploys the virtual machines, the load balancer, availability set etc. Follow these steps to deploy the template:</span></span>

1. <span data-ttu-id="33635-285">Azure Portal에서 [ASCS/SCS 다중 SID 템플릿][template-multisid-xscs] 또는 [수렴형 템플릿][template-converged]을 엽니다. ASCS/SCS 템플릿은 SAP NetWeaver ASCS/SCS 및 ERS(Linux에만 해당)용 부하 분산 규칙만 만드는 반면, 수렴형 템플릿은 데이터베이스(예: Microsoft SQL Server 또는 SAP HANA)용 부하 분산 규칙도 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33635-285">Open the [ASCS/SCS Multi SID template][template-multisid-xscs] or the [converged template][template-converged] on the Azure portal The ASCS/SCS template only creates the load-balancing rules for the SAP NetWeaver ASCS/SCS and ERS (Linux only) instances whereas the converged template also creates the load-balancing rules for a database (for example Microsoft SQL Server or SAP HANA).</span></span> <span data-ttu-id="33635-286">SAP NetWeaver 기반 시스템을 설치할 계획이며 동일한 컴퓨터에 데이터베이스도 설치하려는 경우에는 [수렴형 템플릿][template-converged]을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-286">If you plan to install an SAP NetWeaver based system and you also want to install the database on the same machines, use the [converged template][template-converged].</span></span>
1. <span data-ttu-id="33635-287">다음 매개 변수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-287">Enter the following parameters</span></span>
   1. <span data-ttu-id="33635-288">리소스 접두사(ASCS/SCS 다중 SID 템플릿에만 해당)</span><span class="sxs-lookup"><span data-stu-id="33635-288">Resource Prefix (ASCS/SCS Multi SID template only)</span></span>  
      <span data-ttu-id="33635-289">사용할 접두사를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-289">Enter the prefix you want to use.</span></span> <span data-ttu-id="33635-290">이 값은 배포되는 리소스의 접두사로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="33635-290">The value is used as a prefix for the resources that are deployed.</span></span>
   3. <span data-ttu-id="33635-291">SAP 시스템 ID(수렴형 템플릿에만 해당)</span><span class="sxs-lookup"><span data-stu-id="33635-291">Sap System Id (converged template only)</span></span>  
      <span data-ttu-id="33635-292">설치하려는 SAP 시스템의 SAP 시스템 ID를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-292">Enter the SAP system Id of the SAP system you want to install.</span></span> <span data-ttu-id="33635-293">이 ID는 배포되는 리소스의 접두사로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="33635-293">The Id is used as a prefix for the resources that are deployed.</span></span>
   4. <span data-ttu-id="33635-294">스택 유형 -</span><span class="sxs-lookup"><span data-stu-id="33635-294">Stack Type</span></span>  
      <span data-ttu-id="33635-295">SAP NetWeaver 스택 유형 선택</span><span class="sxs-lookup"><span data-stu-id="33635-295">Select the SAP NetWeaver stack type</span></span>
   5. <span data-ttu-id="33635-296">OS 종류 -</span><span class="sxs-lookup"><span data-stu-id="33635-296">Os Type</span></span>  
      <span data-ttu-id="33635-297">Linux 배포판 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-297">Select one of the Linux distributions.</span></span> <span data-ttu-id="33635-298">이 예에서는 SLES 12 BYOS 선택</span><span class="sxs-lookup"><span data-stu-id="33635-298">For this example, select SLES 12 BYOS</span></span>
   6. <span data-ttu-id="33635-299">Db 형식</span><span class="sxs-lookup"><span data-stu-id="33635-299">Db Type</span></span>  
      <span data-ttu-id="33635-300">HANA 선택</span><span class="sxs-lookup"><span data-stu-id="33635-300">Select HANA</span></span>
   7. <span data-ttu-id="33635-301">SAP 시스템 크기 -</span><span class="sxs-lookup"><span data-stu-id="33635-301">Sap System Size</span></span>  
      <span data-ttu-id="33635-302">새 시스템에서 제공하는 SAP의 양입니다.</span><span class="sxs-lookup"><span data-stu-id="33635-302">The amount of SAPS the new system provides.</span></span> <span data-ttu-id="33635-303">시스템에 필요한 SAP의 수를 모를 경우 SAP 기술 파트너 또는 시스템 통합자에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="33635-303">If you are not sure how many SAPS the system requires, please ask your SAP Technology Partner or System Integrator</span></span>
   8. <span data-ttu-id="33635-304">시스템 가용성 -</span><span class="sxs-lookup"><span data-stu-id="33635-304">System Availability</span></span>  
      <span data-ttu-id="33635-305">HA를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-305">Select HA</span></span>
   9. <span data-ttu-id="33635-306">관리자 사용자 이름 및 관리자 암호 -</span><span class="sxs-lookup"><span data-stu-id="33635-306">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="33635-307">컴퓨터에 로그온하는 데 사용할 수 있게 만들어진 새 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="33635-307">A new user is created that can be used to log on to the machine.</span></span>
   10. <span data-ttu-id="33635-308">서브넷 ID -</span><span class="sxs-lookup"><span data-stu-id="33635-308">Subnet Id</span></span>  
   <span data-ttu-id="33635-309">가상 컴퓨터를 연결해야 하는 서브넷의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="33635-309">The ID of the subnet to which the virtual machines should be connected to.</span></span>  <span data-ttu-id="33635-310">새 가상 네트워크를 만들려는 경우 비워 두거나, NFS 서버 배포의 일부분으로 사용했거나 만든 것과 같은 서브넷을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-310">Leave empty if you want to create a new virtual network or select the same subnet that you used or created as part of the NFS server deployment.</span></span> <span data-ttu-id="33635-311">ID는 대개 /subscriptions/**&lt;구독 ID&gt;**/resourceGroups/**&lt;리소스 그룹 이름&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;가상 네트워크 이름&gt;**/subnets/**&lt;서브넷 이름&gt;**과 같은 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="33635-311">The ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="33635-312">설치</span><span class="sxs-lookup"><span data-stu-id="33635-312">Installation</span></span>

<span data-ttu-id="33635-313">다음 항목에는 접두사 **[A]**(모든 노드에 적용됨), **[1]**(노드 1에만 적용됨), **[2]**(노드 2에만 적용됨) 접두사가 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-313">The following items are prefixed with either **[A]** - applicable to all nodes, **[1]** - only applicable to node 1 or **[2]** - only applicable to node 2.</span></span>

1. <span data-ttu-id="33635-314">**[A]** SLES 업데이트</span><span class="sxs-lookup"><span data-stu-id="33635-314">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="33635-315">**[1]** ssh 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="33635-315">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy the public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="33635-316">**[2]** ssh 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="33635-316">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert the public key you copied in the last step into the authorized keys file on the second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy the public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="33635-317">**[1]** ssh 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="33635-317">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert the public key you copied in the last step into the authorized keys file on the first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="33635-318">**[A]** HA 확장 설치</span><span class="sxs-lookup"><span data-stu-id="33635-318">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="33635-319">**[A]** SAP 리소스 에이전트 업데이트</span><span class="sxs-lookup"><span data-stu-id="33635-319">**[A]** Update SAP resource agents</span></span>  
   
   <span data-ttu-id="33635-320">이 문서에서 설명하는 새 구성을 사용하려면 리소스 에이전트 패키지용 패치가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-320">A patch for the resource-agents package is required to use the new configuration, that is described in this article.</span></span> <span data-ttu-id="33635-321">다음 명령을 사용하여 패치가 이미 설치되었는지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-321">You can check, if the patch is already installed with the following command</span></span>

   <pre><code>
   sudo grep 'parameter name="IS_ERS"' /usr/lib/ocf/resource.d/heartbeat/SAPInstance
   </code></pre>

   <span data-ttu-id="33635-322">다음과 같은 출력이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-322">The output should be similar to</span></span>

   <pre><code>
   &lt;parameter name="IS_ERS" unique="0" required="0"&gt;
   </code></pre>

   <span data-ttu-id="33635-323">grep 명령을 실행하여 IS_ERS 매개 변수를 찾을 수 없는 경우에는 [SUSE 다운로드 페이지](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)에 나와 있는 패치를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-323">If the grep command does not find the IS_ERS parameter, you need to install the patch listed on [the SUSE download page](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)</span></span>

   <pre><code>
   # example for patch for SLES 12 SP1
   sudo zypper in -t patch SUSE-SLE-HA-12-SP1-2017-885=1
   # example for patch for SLES 12 SP2
   sudo zypper in -t patch SUSE-SLE-HA-12-SP2-2017-886=1
   </code></pre>

1. <span data-ttu-id="33635-324">**[A]** 호스트 이름 확인 설정</span><span class="sxs-lookup"><span data-stu-id="33635-324">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="33635-325">DNS 서버를 사용하거나 모든 노드의 /etc/hosts를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-325">You can either use a DNS server or modify the /etc/hosts on all nodes.</span></span> <span data-ttu-id="33635-326">이 예에서는 /etc/hosts 파일 사용 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="33635-326">This example shows how to use the /etc/hosts file.</span></span>
   <span data-ttu-id="33635-327">다음 명령에서 IP 주소와 호스트 이름 바꾸기</span><span class="sxs-lookup"><span data-stu-id="33635-327">Replace the IP address and the hostname in the following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="33635-328">다음 줄을 /etc/hosts에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-328">Insert the following lines to /etc/hosts.</span></span> <span data-ttu-id="33635-329">환경에 맞게 IP 주소와 호스트 이름 변경</span><span class="sxs-lookup"><span data-stu-id="33635-329">Change the IP address and hostname to match your environment</span></span>   
   
   <pre><code>
   # IP address of the load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of the load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of the load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of the load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   </code></pre>

1. <span data-ttu-id="33635-330">**[1]** 클러스터 설치</span><span class="sxs-lookup"><span data-stu-id="33635-330">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want to continue anyway? [y/N] -> y
   # Network address to bind to (for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish to use SBD? [y/N] -> N
   # Do you wish to configure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="33635-331">**[2]** 클러스터에 노드 추가</span><span class="sxs-lookup"><span data-stu-id="33635-331">**[2]** Add node to cluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured to start at system boot.
   # WARNING: No watchdog device found. If SBD is used, the cluster will be unable to start without a watchdog.
   # Do you want to continue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="33635-332">**[A]** hacluster 암호를 동일한 암호로 변경</span><span class="sxs-lookup"><span data-stu-id="33635-332">**[A]** Change hacluster password to the same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="33635-333">**[A]** 다른 전송을 사용하고 nodelist를 추가하도록 corosync 구성.</span><span class="sxs-lookup"><span data-stu-id="33635-333">**[A]** Configure corosync to use other transport and add nodelist.</span></span> <span data-ttu-id="33635-334">그렇지 않으면 클러스터가 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-334">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="33635-335">굵은체로 된 다음 콘텐츠를 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-335">Add the following bold content to the file.</span></span>
   
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

   <span data-ttu-id="33635-336">그런 다음 corosync 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-336">Then restart the corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="33635-337">**[A]** drbd 구성 요소 설치</span><span class="sxs-lookup"><span data-stu-id="33635-337">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="33635-338">**[A]** drbd 장치용 파티션 만들기</span><span class="sxs-lookup"><span data-stu-id="33635-338">**[A]** Create a partition for the drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="33635-339">**[A]** LVM 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="33635-339">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_<b>NWS</b> /dev/sdc1
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ASCS vg_<b>NWS</b>
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ERS vg_<b>NWS</b>
   </code></pre>

1. <span data-ttu-id="33635-340">**[A]** SCS drbd 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="33635-340">**[A]** Create the SCS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ascs.res
   </code></pre>

   <span data-ttu-id="33635-341">새 drbd 장치용 구성을 삽입하고 명령을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-341">Insert the configuration for the new drbd device and exit</span></span>

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

   <span data-ttu-id="33635-342">drbd 장치를 만들어 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-342">Create the drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ascs
   sudo drbdadm up <b>NWS</b>_ascs
   </code></pre>

1. <span data-ttu-id="33635-343">**[A]** ERS drbd 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="33635-343">**[A]** Create the ERS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ers.res
   </code></pre>

   <span data-ttu-id="33635-344">새 drbd 장치용 구성을 삽입하고 명령을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-344">Insert the configuration for the new drbd device and exit</span></span>

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

   <span data-ttu-id="33635-345">drbd 장치를 만들어 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-345">Create the drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ers
   sudo drbdadm up <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="33635-346">**[1]** 초기 동기화 건너뛰기</span><span class="sxs-lookup"><span data-stu-id="33635-346">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ascs
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="33635-347">**[1]** 주 노드 설정</span><span class="sxs-lookup"><span data-stu-id="33635-347">**[1]** Set the primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_ascs
   sudo drbdadm primary --force <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="33635-348">**[1]** 새 drbd 장치가 동기화될 때까지 대기</span><span class="sxs-lookup"><span data-stu-id="33635-348">**[1]** Wait until the new drbd devices are synchronized</span></span>

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

1. <span data-ttu-id="33635-349">**[1]** drbd 장치에서 파일 시스템 만들기</span><span class="sxs-lookup"><span data-stu-id="33635-349">**[1]** Create file systems on the drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   sudo mkfs.xfs /dev/drbd1
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="33635-350">클러스터 프레임워크 구성</span><span class="sxs-lookup"><span data-stu-id="33635-350">Configure Cluster Framework</span></span>

<span data-ttu-id="33635-351">**[1]** 기본 설정 변경</span><span class="sxs-lookup"><span data-stu-id="33635-351">**[1]** Change the default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

## <a name="prepare-for-sap-netweaver-installation"></a><span data-ttu-id="33635-352">SAP NetWeaver 설치 준비</span><span class="sxs-lookup"><span data-stu-id="33635-352">Prepare for SAP NetWeaver installation</span></span>

1. <span data-ttu-id="33635-353">**[A]** 공유 디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="33635-353">**[A]** Create the shared directories</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans
   sudo mkdir -p /usr/sap/<b>NWS</b>/SYS

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   sudo chattr +i /usr/sap/<b>NWS</b>/SYS
   </code></pre>

1. <span data-ttu-id="33635-354">**[A]** autofs 구성</span><span class="sxs-lookup"><span data-stu-id="33635-354">**[A]** Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add the following line to the file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="33635-355">아래 코드를 사용하여 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33635-355">Create a file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add the following lines to the file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   /usr/sap/<b>NWS</b>/SYS -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sidsys
   </code></pre>

   <span data-ttu-id="33635-356">autofs를 다시 시작하여 새 공유를 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-356">Restart autofs to mount the new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="33635-357">**[A]** 스왑 파일 구성</span><span class="sxs-lookup"><span data-stu-id="33635-357">**[A]** Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set the property ResourceDisk.EnableSwap to y
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set the size of the SWAP file with property ResourceDisk.SwapSizeMB
   # The free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check the SWAP space with command swapon
   # Size of the swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="33635-358">에이전트를 다시 시작하여 변경 내용을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-358">Restart the Agent to activate the change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

### <a name="installing-sap-netweaver-ascsers"></a><span data-ttu-id="33635-359">SAP NetWeaver ASCS/ERS 설치</span><span class="sxs-lookup"><span data-stu-id="33635-359">Installing SAP NetWeaver ASCS/ERS</span></span>

1. <span data-ttu-id="33635-360">**[1]** 내부 부하 분산 장치용 가상 IP 리소스 및 상태 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="33635-360">**[1]** Create a virtual IP resource and health-probe for the internal load balancer</span></span>

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

   <span data-ttu-id="33635-361">클러스터 상태가 정상이며 모든 리소스가 시작되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-361">Make sure that the cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="33635-362">리소스가 실행되는 노드는 중요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-362">It is not important on which node the resources are running.</span></span>

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

1. <span data-ttu-id="33635-363">**[1]** SAP NetWeaver ASCS 설치</span><span class="sxs-lookup"><span data-stu-id="33635-363">**[1]** Install SAP NetWeaver ASCS</span></span>  

   <span data-ttu-id="33635-364">ASCS용 부하 분산 장치 프런트 엔드 구성의 IP 주소에 매핑되는 가상 호스트 이름(예: <b>nws-ascs</b>, <b>10.0.0.10</b>)과 부하 분산 장치의 프로브에 사용했던 인스턴스 번호(예: <b>00</b>)를 사용하여 첫 번째 노드에 루트로 SAP NetWeaver ASCS를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-364">Install SAP NetWeaver ASCS as root on the first node using a virtual hostname that maps to the IP address of the load balancer frontend configuration for the ASCS for example <b>nws-ascs</b>, <b>10.0.0.10</b> and the instance number that you used for the probe of the load balancer for example <b>00</b>.</span></span>

   <span data-ttu-id="33635-365">sapinst 매개 변수 SAPINST_REMOTE_ACCESS_USER를 사용하면 루트 권한이 없는 사용자의 sapinst 연결을 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-365">You can use the sapinst parameter SAPINST_REMOTE_ACCESS_USER to allow a non-root user to connect to sapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="33635-366">**[1]** 내부 부하 분산 장치용 가상 IP 리소스 및 상태 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="33635-366">**[1]** Create a virtual IP resource and health-probe for the internal load balancer</span></span>

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
   # Do you still want to commit (y/n)? y

   crm(live)configure# exit
   
   </code></pre>
 
   <span data-ttu-id="33635-367">클러스터 상태가 정상이며 모든 리소스가 시작되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-367">Make sure that the cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="33635-368">리소스가 실행되는 노드는 중요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-368">It is not important on which node the resources are running.</span></span>

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

1. <span data-ttu-id="33635-369">**[2]** SAP NetWeaver ERS 설치</span><span class="sxs-lookup"><span data-stu-id="33635-369">**[2]** Install SAP NetWeaver ERS</span></span>  

   <span data-ttu-id="33635-370">ERS용 부하 분산 장치 프런트 엔드 구성의 IP 주소에 매핑되는 가상 호스트 이름(예: <b>nws-ers</b>, <b>10.0.0.11</b>)과 부하 분산 장치의 프로브에 사용했던 인스턴스 번호(예: <b>02</b>)를 사용하여 두 번째 노드에 루트로 SAP NetWeaver ERS를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-370">Install SAP NetWeaver ERS as root on the second node using a virtual hostname that maps to the IP address of the load balancer frontend configuration for the ERS for example <b>nws-ers</b>, <b>10.0.0.11</b> and the instance number that you used for the probe of the load balancer for example <b>02</b>.</span></span>

   <span data-ttu-id="33635-371">sapinst 매개 변수 SAPINST_REMOTE_ACCESS_USER를 사용하면 루트 권한이 없는 사용자의 sapinst 연결을 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-371">You can use the sapinst parameter SAPINST_REMOTE_ACCESS_USER to allow a non-root user to connect to sapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

   > [!NOTE]
   > <span data-ttu-id="33635-372">SWPM SP 20 PL 05 이상을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="33635-372">Please use SWPM SP 20 PL 05 or higher.</span></span> <span data-ttu-id="33635-373">그 이전 버전은 권한을 올바르게 설정하지 않으므로 설치가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-373">Lower versions do not set the permissions correctly and the installation will fail.</span></span>
   > 

1. <span data-ttu-id="33635-374">**[1]** ASCS/SCS 및 ERS 인스턴스 프로필 조정</span><span class="sxs-lookup"><span data-stu-id="33635-374">**[1]** Adapt the ASCS/SCS and ERS instance profiles</span></span>
 
   * <span data-ttu-id="33635-375">ASCS/SCS 프로필</span><span class="sxs-lookup"><span data-stu-id="33635-375">ASCS/SCS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_<b>ASCS00</b>_<b>nws-ascs</b>

   # Change the restart command to a start command
   #Restart_Program_01 = local $(_EN) pf=$(_PF)
   Start_Program_01 = local $(_EN) pf=$(_PF)

   # Add the following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector

   # Add the keep alive parameter
   enque/encni/set_so_keepalive = true
   </code></pre>

   * <span data-ttu-id="33635-376">ERS 프로필</span><span class="sxs-lookup"><span data-stu-id="33635-376">ERS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>

   # Add the following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector
   </code></pre>


1. <span data-ttu-id="33635-377">**[A]** 연결 유지 구성</span><span class="sxs-lookup"><span data-stu-id="33635-377">**[A]** Configure Keep Alive</span></span>

   <span data-ttu-id="33635-378">SAP NetWeaver 응용 프로그램 서버와 ASCS/SCS 간의 통신은 소프트웨어 부하 분산 장치를 통해 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="33635-378">The communication between the SAP NetWeaver application server and the ASCS/SCS is routed through a software load balancer.</span></span> <span data-ttu-id="33635-379">부하 분산 장치는 구성 가능한 시간 제한이 지나면 비활성 연결을 끊습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-379">The load balancer disconnects inactive connections after a configurable timeout.</span></span> <span data-ttu-id="33635-380">이 연결 끊김을 방지하려면 SAP NetWeaver ASCS/SCS 프로필에서 매개 변수를 설정하고 Linux 시스템 설정을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-380">To prevent this you need to set a parameter in the SAP NetWeaver ASCS/SCS profile and change the Linux system settings.</span></span> <span data-ttu-id="33635-381">자세한 내용은 [SAP Note 1410736][1410736]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33635-381">Please read [SAP Note 1410736][1410736] for more information.</span></span>
   
   <span data-ttu-id="33635-382">ASCS/SCS profile 매개 변수 enque/encni/set_so_keepalive는 마지막 단계에서 이미 추가된 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="33635-382">The ASCS/SCS profile parameter enque/encni/set_so_keepalive was already added in the last step.</span></span>

   <pre><code> 
   # Change the Linux system configuration
   sudo sysctl net.ipv4.tcp_keepalive_time=120
   </code></pre>

1. <span data-ttu-id="33635-383">**[A]** 설치 후 SAP 사용자 구성</span><span class="sxs-lookup"><span data-stu-id="33635-383">**[A]** Configure the SAP users after the installation</span></span>
 
   <pre><code>
   # Add sidadm to the haclient group
   sudo usermod -aG haclient <b>nws</b>adm   
   </code></pre>

1. <span data-ttu-id="33635-384">**[1]** sapservice 파일에 ASCS 및 ERS SAP 서비스 추가</span><span class="sxs-lookup"><span data-stu-id="33635-384">**[1]** Add the ASCS and ERS SAP services to the sapservice file</span></span>

   <span data-ttu-id="33635-385">ASCS 서비스 항목을 두 번째 노드에 추가하고 ERS 서비스 항목을 첫 번째 노드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-385">Add the ASCS service entry to the second node and copy the ERS service entry to the first node.</span></span>

   <pre><code>
   cat /usr/sap/sapservices | grep ASCS<b>00</b> | sudo ssh <b>nws-cl-1</b> "cat >>/usr/sap/sapservices"
   sudo ssh <b>nws-cl-1</b> "cat /usr/sap/sapservices" | grep ERS<b>02</b> | sudo tee -a /usr/sap/sapservices
   </code></pre>

1. <span data-ttu-id="33635-386">**[1]** SAP 클러스터 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="33635-386">**[1]** Create the SAP cluster resources</span></span>

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

   <span data-ttu-id="33635-387">클러스터 상태가 정상이며 모든 리소스가 시작되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-387">Make sure that the cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="33635-388">리소스가 실행되는 노드는 중요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-388">It is not important on which node the resources are running.</span></span>

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

### <a name="create-stonith-device"></a><span data-ttu-id="33635-389">STONITH 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="33635-389">Create STONITH device</span></span>

<span data-ttu-id="33635-390">STONITH 장치에서는 서비스 주체를 사용하여 Microsoft Azure에 대해 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-390">The STONITH device uses a Service Principal to authorize against Microsoft Azure.</span></span> <span data-ttu-id="33635-391">다음 단계에 따라 서비스 주체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33635-391">Follow these steps to create a Service Principal.</span></span>

1. <span data-ttu-id="33635-392"><https://portal.azure.com>으로 이동</span><span class="sxs-lookup"><span data-stu-id="33635-392">Go to <https://portal.azure.com></span></span>
1. <span data-ttu-id="33635-393">Azure Active Directory 블레이드 열기</span><span class="sxs-lookup"><span data-stu-id="33635-393">Open the Azure Active Directory blade</span></span>  
   <span data-ttu-id="33635-394">속성으로 이동하여 Directory ID 기록</span><span class="sxs-lookup"><span data-stu-id="33635-394">Go to Properties and write down the Directory Id.</span></span> <span data-ttu-id="33635-395">이 ID는 **테넌트 ID**입니다.</span><span class="sxs-lookup"><span data-stu-id="33635-395">This is the **tenant id**.</span></span>
1. <span data-ttu-id="33635-396">앱 등록 클릭</span><span class="sxs-lookup"><span data-stu-id="33635-396">Click App registrations</span></span>
1. <span data-ttu-id="33635-397">추가를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-397">Click Add</span></span>
1. <span data-ttu-id="33635-398">이름을 입력하고 응용 프로그램 유형 "Web app/API"를 선택한 다음 로그온 URL(예: http://localhost )을 입력하고 만들기를 클릭</span><span class="sxs-lookup"><span data-stu-id="33635-398">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="33635-399">로그온 URL이 사용되지 않으며, 이 URL은 임의의 올바른 URL이 될 수 있음</span><span class="sxs-lookup"><span data-stu-id="33635-399">The sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="33635-400">새 앱을 선택하고 설정 탭에서 키 클릭</span><span class="sxs-lookup"><span data-stu-id="33635-400">Select the new App and click Keys in the Settings tab</span></span>
1. <span data-ttu-id="33635-401">새 키의 설명을 입력하고 “만료되지 않음”을 선택한 다음 저장을 클릭</span><span class="sxs-lookup"><span data-stu-id="33635-401">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="33635-402">값을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="33635-402">Write down the Value.</span></span> <span data-ttu-id="33635-403">서비스 주체의 **암호**로 사용됨</span><span class="sxs-lookup"><span data-stu-id="33635-403">It is used as the **password** for the Service Principal</span></span>
1. <span data-ttu-id="33635-404">응용 프로그램 ID를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="33635-404">Write down the Application Id.</span></span> <span data-ttu-id="33635-405">서비스 주체의 사용자 이름(아래 단계의 **로그인 id**)으로 사용됨</span><span class="sxs-lookup"><span data-stu-id="33635-405">It is used as the username (**login id** in the steps below) of the Service Principal</span></span>

<span data-ttu-id="33635-406">서비스 주체에는 기본적으로 Azure 리소스에 액세스할 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-406">The Service Principal does not have permissions to access your Azure resources by default.</span></span> <span data-ttu-id="33635-407">서비스 주체에 클러스터의 모든 가상 컴퓨터를 시작 및 중지(할당 취소)하기 위한 권한을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-407">You need to give the Service Principal permissions to start and stop (deallocate) all virtual machines of the cluster.</span></span>

1. <span data-ttu-id="33635-408">https://portal.azure.com으로 이동</span><span class="sxs-lookup"><span data-stu-id="33635-408">Go to https://portal.azure.com</span></span>
1. <span data-ttu-id="33635-409">모든 리소스 블레이드 열기</span><span class="sxs-lookup"><span data-stu-id="33635-409">Open the All resources blade</span></span>
1. <span data-ttu-id="33635-410">가상 컴퓨터 선택</span><span class="sxs-lookup"><span data-stu-id="33635-410">Select the virtual machine</span></span>
1. <span data-ttu-id="33635-411">액세스 제어(IAM) 클릭</span><span class="sxs-lookup"><span data-stu-id="33635-411">Click Access control (IAM)</span></span>
1. <span data-ttu-id="33635-412">추가를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-412">Click Add</span></span>
1. <span data-ttu-id="33635-413">소유자 역할 선택</span><span class="sxs-lookup"><span data-stu-id="33635-413">Select the role Owner</span></span>
1. <span data-ttu-id="33635-414">위에서 만든 응용 프로그램의 이름 입력</span><span class="sxs-lookup"><span data-stu-id="33635-414">Enter the name of the application you created above</span></span>
1. <span data-ttu-id="33635-415">확인 클릭</span><span class="sxs-lookup"><span data-stu-id="33635-415">Click OK</span></span>

#### <a name="1-create-the-stonith-devices"></a><span data-ttu-id="33635-416">**[1]** STONITH 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="33635-416">**[1]** Create the STONITH devices</span></span>

<span data-ttu-id="33635-417">가상 컴퓨터의 권한을 편집하고 나면 클러스터의 STONITH 장치를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-417">After you edited the permissions for the virtual machines, you can configure the STONITH devices in the cluster.</span></span>

<pre><code>
sudo crm configure

# replace the bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-the-use-of-a-stonith-device"></a><span data-ttu-id="33635-418">**[1]** STONITH 장치를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="33635-418">**[1]** Enable the use of a STONITH device</span></span>

<span data-ttu-id="33635-419">STONITH 장치를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="33635-419">Enable the use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="install-database"></a><span data-ttu-id="33635-420">데이터베이스 설치</span><span class="sxs-lookup"><span data-stu-id="33635-420">Install database</span></span>

<span data-ttu-id="33635-421">이 예제에서 SAP HANA System Replication을 설치 및 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-421">In this example an SAP HANA System Replication is installed and configured.</span></span> <span data-ttu-id="33635-422">SAP HANA는 SAP NetWeaver ASCS/SCS 및 ERS와 같은 클러스터에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="33635-422">SAP HANA will run in the same cluster as the SAP NetWeaver ASCS/SCS and ERS.</span></span> <span data-ttu-id="33635-423">전용 클러스터에 SAP HANA를 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-423">You can also install SAP HANA on a dedicated cluster.</span></span> <span data-ttu-id="33635-424">자세한 내용은 [Azure VM(Virtual Machines)의 SAP HANA 고가용성][sap-hana-ha]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33635-424">See [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha] for more information.</span></span>

### <a name="prepare-for-sap-hana-installation"></a><span data-ttu-id="33635-425">SAP HANA 설치 준비</span><span class="sxs-lookup"><span data-stu-id="33635-425">Prepare for SAP HANA installation</span></span>

<span data-ttu-id="33635-426">일반적으로는 데이터와 로그 파일을 저장하는 볼륨의 LVM을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-426">We generally recommend using LVM for volumes that store data and log files.</span></span> <span data-ttu-id="33635-427">테스트의 경우에는 데이터와 로그 파일을 일반 디스크에 직접 저장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-427">For testing purposes, you can also choose to store the data and log file directly on a plain disk.</span></span>

1. <span data-ttu-id="33635-428">**[A]** LVM</span><span class="sxs-lookup"><span data-stu-id="33635-428">**[A]** LVM</span></span>  
   <span data-ttu-id="33635-429">아래 예에서는 가상 컴퓨터에 두 개의 볼륨을 만드는 데 사용해야 하는 4개의 데이터 디스크가 연결되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-429">The example below assumes that the virtual machines have four data disks attached that should be used to create two volumes.</span></span>
   
   <span data-ttu-id="33635-430">사용하려는 모든 디스크의 물리적 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33635-430">Create physical volumes for all disks that you want to use.</span></span>
   
   <pre><code>
   sudo pvcreate /dev/sdd
   sudo pvcreate /dev/sde
   sudo pvcreate /dev/sdf
   sudo pvcreate /dev/sdg
   </code></pre>
   
   <span data-ttu-id="33635-431">데이터 파일에 대한 볼륨 그룹, 로그 파일에 대해 한 볼륨 그룹 및 SAP HANA의 공유 디렉터리에 대해 한 볼륨 만들기</span><span class="sxs-lookup"><span data-stu-id="33635-431">Create a volume group for the data files, one volume group for the log files and one for the shared directory of SAP HANA</span></span>
   
   <pre><code>
   sudo vgcreate vg_hana_data /dev/sdd /dev/sde
   sudo vgcreate vg_hana_log /dev/sdf
   sudo vgcreate vg_hana_shared /dev/sdg
   </code></pre>
   
   <span data-ttu-id="33635-432">논리 볼륨 만들기</span><span class="sxs-lookup"><span data-stu-id="33635-432">Create the logical volumes</span></span>
   
   <pre><code>
   sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
   sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
   sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
   sudo mkfs.xfs /dev/vg_hana_data/hana_data
   sudo mkfs.xfs /dev/vg_hana_log/hana_log
   sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
   </code></pre>
   
   <span data-ttu-id="33635-433">탑재 디렉터리를 만들고 모든 논리 볼륨의 UUID 복사</span><span class="sxs-lookup"><span data-stu-id="33635-433">Create the mount directories and copy the UUID of all logical volumes</span></span>
   
   <pre><code>
   sudo mkdir -p /hana/data
   sudo mkdir -p /hana/log
   sudo mkdir -p /hana/shared
   sudo chattr +i /hana/data
   sudo chattr +i /hana/log
   sudo chattr +i /hana/shared
   # write down the id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
   sudo blkid
   </code></pre>
   
   <span data-ttu-id="33635-434">세 개의 논리 볼륨에 대한 autofs 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33635-434">Create autofs entries for the three logical volumes</span></span>
   
   <pre><code>
   sudo vi /etc/auto.direct
   </code></pre>
   
   <span data-ttu-id="33635-435">sudo vi /etc/auto.direct에 아래 줄을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-435">Insert this line to sudo vi /etc/auto.direct</span></span>
   
   <pre><code>
   /hana/data -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b>
   /hana/log -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b>
   /hana/shared -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b>
   </code></pre>
   
   <span data-ttu-id="33635-436">새 볼륨 탑재</span><span class="sxs-lookup"><span data-stu-id="33635-436">Mount the new volumes</span></span>
   
   <pre><code>
   sudo service autofs restart 
   </code></pre>

1. <span data-ttu-id="33635-437">**[A]** 일반 디스크</span><span class="sxs-lookup"><span data-stu-id="33635-437">**[A]** Plain Disks</span></span>  

   <span data-ttu-id="33635-438">소규모 또는 데모 시스템용으로 한 디스크에 HANA 데이터와 로그 파일을 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-438">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="33635-439">다음 명령은 /dev/sdc에 패턴을 만들고 xfs로 서식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-439">The following commands create a partition on /dev/sdc and format it with xfs.</span></span>
   ```bash
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdd'
   sudo mkfs.xfs /dev/sdd1
   
   # write down the id of /dev/sdd1
   sudo /sbin/blkid
   sudo vi /etc/auto.direct
   ```
   
   <span data-ttu-id="33635-440">/etc/auto.direct에 아래 줄을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-440">Insert this line to /etc/auto.direct</span></span>
   <pre><code>
   /hana -fstype=xfs :UUID=<b>&lt;UUID&gt;</b>
   </code></pre>
   
   <span data-ttu-id="33635-441">대상 디렉터리를 만들고 디스크를 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-441">Create the target directory and mount the disk.</span></span>
   
   <pre><code>
   sudo mkdir /hana
   sudo chattr +i /hana
   sudo service autofs restart
   </code></pre>

### <a name="installing-sap-hana"></a><span data-ttu-id="33635-442">SAP HANA 설치</span><span class="sxs-lookup"><span data-stu-id="33635-442">Installing SAP HANA</span></span>

<span data-ttu-id="33635-443">다음 단계에서는 [SAP HANA SR 성능 최적화 시나리오 가이드][suse-hana-ha-guide]의 4장에 따라 SAP HANA System Replication을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-443">The following steps are based on chapter 4 of the [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] to install SAP HANA System Replication.</span></span> <span data-ttu-id="33635-444">설치를 계속하기 전에 해당 내용을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="33635-444">Please read it before you continue the installation.</span></span>

1. <span data-ttu-id="33635-445">**[A]** HANA DVD에서 hdblcm 실행</span><span class="sxs-lookup"><span data-stu-id="33635-445">**[A]** Run hdblcm from the HANA DVD</span></span>
   
   <pre><code>
   sudo hdblcm --sid=<b>HDB</b> --number=<b>03</b> --action=install --batch --password=<b>&lt;password&gt;</b> --system_user_password=<b>&lt;password for system user&gt;</b>

   sudo /hana/shared/<b>HDB</b>/hdblcm/hdblcm --action=configure_internal_network --listen_interface=internal --internal_network=<b>10.0.0/24</b> --password=<b>&lt;password for system user&gt;</b> --batch
   </code></pre>

1. <span data-ttu-id="33635-446">**[A]** SAP 호스트 에이전트 업그레이드</span><span class="sxs-lookup"><span data-stu-id="33635-446">**[A]** Upgrade SAP Host Agent</span></span>

   <span data-ttu-id="33635-447">[SAP Softwarecenter][sap-swcenter]에서 최신 SAP 호스트 에이전트 아카이브를 다운로드하고 다음 명령을 실행하여 에이전트를 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-447">Download the latest SAP Host Agent archive from the [SAP Softwarecenter][sap-swcenter] and run the following command to upgrade the agent.</span></span> <span data-ttu-id="33635-448">다운로드한 파일을 가리키도록 아카이브의 경로를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="33635-448">Replace the path to the archive to point to the file you downloaded.</span></span>
   <pre><code>
   sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <b>&lt;path to SAP Host Agent SAR&gt;</b> 
   </code></pre>

1. <span data-ttu-id="33635-449">**[1]** 루트로 HANA 복제 만들기</span><span class="sxs-lookup"><span data-stu-id="33635-449">**[1]** Create HANA replication (as root)</span></span>  

   <span data-ttu-id="33635-450">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-450">Run the following command.</span></span> <span data-ttu-id="33635-451">굵은체로 된 문자열(HANA 시스템 ID HDB 및 인스턴스 번호 03)을 SAP HANA 설치의 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="33635-451">Make sure to replace bold strings (HANA System ID HDB and instance number 03) with the values of your SAP HANA installation.</span></span>
   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
   hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN TO <b>hdb</b>hasync' 
   hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
   </code></pre>

1. <span data-ttu-id="33635-452">**[A]** 루트로 키 저장소 항목 만들기</span><span class="sxs-lookup"><span data-stu-id="33635-452">**[A]** Create keystore entry (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>&lt;passwd&gt;</b>
   </code></pre>

1. <span data-ttu-id="33635-453">**[1]** 루트로 데이터베이스 백업</span><span class="sxs-lookup"><span data-stu-id="33635-453">**[1]** Backup database (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
   </code></pre>

1. <span data-ttu-id="33635-454">**[1]** HANA sapsid 사용자로 전환하여 기본 사이트 만들기</span><span class="sxs-lookup"><span data-stu-id="33635-454">**[1]** Switch to the HANA sapsid user and create the primary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   hdbnsutil -sr_enable –-name=<b>SITE1</b>
   </code></pre>

1. <span data-ttu-id="33635-455">**[2]** HANA sapsid 사용자로 전환하여 보조 사이트 만들기</span><span class="sxs-lookup"><span data-stu-id="33635-455">**[2]** Switch to the HANA sapsid user and create the secondary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   sapcontrol -nr <b>03</b> -function StopWait 600 10
   hdbnsutil -sr_register --remoteHost=<b>nws-cl-0</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
   </code></pre>

1. <span data-ttu-id="33635-456">**[1]** SAP HANA 클러스터 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="33635-456">**[1]** Create SAP HANA cluster resources</span></span>

   <span data-ttu-id="33635-457">먼저 토폴로지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33635-457">First, create the topology.</span></span>
   
   <pre><code>
   sudo crm configure

   # replace the bold string with your instance number and HANA system id
   
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
   
   <span data-ttu-id="33635-458">다음으로 HANA 리소스를 만듭니다</span><span class="sxs-lookup"><span data-stu-id="33635-458">Next, create the HANA resources</span></span>
   
   <pre><code>
   sudo crm configure

   # replace the bold string with your instance number, HANA system id and the frontend IP address of the Azure load balancer. 
    
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

   <span data-ttu-id="33635-459">클러스터 상태가 정상이며 모든 리소스가 시작되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-459">Make sure that the cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="33635-460">리소스가 실행되는 노드는 중요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-460">It is not important on which node the resources are running.</span></span>

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

1. <span data-ttu-id="33635-461">**[1]** SAP NetWeaver 데이터베이스 인스턴스 설치</span><span class="sxs-lookup"><span data-stu-id="33635-461">**[1]** Install the SAP NetWeaver database instance</span></span>

   <span data-ttu-id="33635-462">데이터베이스용 부하 분산 장치 프런트 엔드 구성의 IP 주소에 매핑되는 가상 호스트 이름(예: <b>nws-db</b> 및 <b>10.0.0.12</b>)을 사용하여 루트로 SAP NetWeaver 데이터베이스 인스턴스를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-462">Install the SAP NetWeaver database instance as root using a virtual hostname that maps to the IP address of the load balancer frontend configuration for the database for example <b>nws-db</b> and <b>10.0.0.12</b>.</span></span>

   <span data-ttu-id="33635-463">sapinst 매개 변수 SAPINST_REMOTE_ACCESS_USER를 사용하면 루트 권한이 없는 사용자의 sapinst 연결을 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-463">You can use the sapinst parameter SAPINST_REMOTE_ACCESS_USER to allow a non-root user to connect to sapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

## <a name="sap-netweaver-application-server-installation"></a><span data-ttu-id="33635-464">SAP NetWeaver 응용 프로그램 서버 설치</span><span class="sxs-lookup"><span data-stu-id="33635-464">SAP NetWeaver application server installation</span></span>

<span data-ttu-id="33635-465">다음 단계에 따라 SAP 응용 프로그램 서버를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-465">Follow these steps to install an SAP application server.</span></span> <span data-ttu-id="33635-466">아래 단계에서는 ASCS/SCS 및 HANA 서버와 다른 서버에 응용 프로그램 서버를 설치한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-466">The steps bellow assume that you install the application server on a server different from the ASCS/SCS and HANA servers.</span></span> <span data-ttu-id="33635-467">그 외의 경우에는 호스트 이름 확인을 구성하는 단계 등 아래의 일부 단계를 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-467">Otherwise some of the steps below (like configuring host name resolution) are not needed.</span></span>

1. <span data-ttu-id="33635-468">호스트 이름 확인 설정</span><span class="sxs-lookup"><span data-stu-id="33635-468">Setup host name resolution</span></span>    
   <span data-ttu-id="33635-469">DNS 서버를 사용하거나 모든 노드의 /etc/hosts를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-469">You can either use a DNS server or modify the /etc/hosts on all nodes.</span></span> <span data-ttu-id="33635-470">이 예에서는 /etc/hosts 파일 사용 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="33635-470">This example shows how to use the /etc/hosts file.</span></span>
   <span data-ttu-id="33635-471">다음 명령에서 IP 주소와 호스트 이름 바꾸기</span><span class="sxs-lookup"><span data-stu-id="33635-471">Replace the IP address and the hostname in the following commands</span></span>
   ```bash
   sudo vi /etc/hosts
   ```
   <span data-ttu-id="33635-472">다음 줄을 /etc/hosts에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-472">Insert the following lines to /etc/hosts.</span></span> <span data-ttu-id="33635-473">환경에 맞게 IP 주소와 호스트 이름 변경</span><span class="sxs-lookup"><span data-stu-id="33635-473">Change the IP address and hostname to match your environment</span></span>    
    
   <pre><code>
   # IP address of the load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of the load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of the load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of the load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   # IP address of the application server
   <b>10.0.0.8 nws-di-0</b>
   </code></pre>

1. <span data-ttu-id="33635-474">sapmnt 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33635-474">Create the sapmnt directory</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   </code></pre>

1. <span data-ttu-id="33635-475">autofs를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-475">Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add the following line to the file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="33635-476">다음 코드를 사용하여 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33635-476">Create a new file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add the following lines to the file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   </code></pre>

   <span data-ttu-id="33635-477">autofs를 다시 시작하여 새 공유를 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-477">Restart autofs to mount the new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="33635-478">스왑 파일을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-478">Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set the property ResourceDisk.EnableSwap to y
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set the size of the SWAP file with property ResourceDisk.SwapSizeMB
   # The free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check the SWAP space with command swapon
   # Size of the swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="33635-479">에이전트를 다시 시작하여 변경 내용을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-479">Restart the Agent to activate the change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

1. <span data-ttu-id="33635-480">SAP NetWeaver 응용 프로그램 서버 설치</span><span class="sxs-lookup"><span data-stu-id="33635-480">Install SAP NetWeaver application server</span></span>

   <span data-ttu-id="33635-481">기본 또는 추가 SAP NetWeaver 응용 프로그램 서버를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-481">Install a primary or additional SAP NetWeaver applications server.</span></span>

   <span data-ttu-id="33635-482">sapinst 매개 변수 SAPINST_REMOTE_ACCESS_USER를 사용하면 루트 권한이 없는 사용자의 sapinst 연결을 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33635-482">You can use the sapinst parameter SAPINST_REMOTE_ACCESS_USER to allow a non-root user to connect to sapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="33635-483">SAP HANA 보안 저장소 업데이트</span><span class="sxs-lookup"><span data-stu-id="33635-483">Update SAP HANA secure store</span></span>

   <span data-ttu-id="33635-484">설치한 SAP HANA System Replication의 가상 이름을 가리키도록 SAP HANA 보안 저장소를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="33635-484">Update the SAP HANA secure store to point to the virtual name of the SAP HANA System Replication setup.</span></span>
   <pre><code>
   su - <b>nws</b>adm
   hdbuserstore SET DEFAULT <b>nws-db</b>:3<b>03</b>15 <b>SAPABAP1</b> <b>&lt;password of ABAP schema&gt;</b>
   </code></pre>

## <a name="next-steps"></a><span data-ttu-id="33635-485">다음 단계</span><span class="sxs-lookup"><span data-stu-id="33635-485">Next steps</span></span>
* <span data-ttu-id="33635-486">[SAP용 Azure Virtual Machines 계획 및 구현][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="33635-486">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="33635-487">[SAP용 Azure Virtual Machines 배포][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="33635-487">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="33635-488">[SAP용 Azure Virtual Machines DBMS 배포][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="33635-488">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="33635-489">[Azure의 SAP HANA(큰 인스턴스) 고가용성 및 재해 복구](hana-overview-high-availability-disaster-recovery.md) - Azure의 SAP HANA(큰 인스턴스)에 대한 고가용성 및 재해 복구 계획을 설정하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="33635-489">To learn how to establish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span>
* <span data-ttu-id="33635-490">Azure VM에서 SAP HANA의 재해 복구를 계획하고 고가용성을 설정하는 방법을 알아보려면 [Azure VM(Virtual Machines)의 SAP HANA 고가용성][sap-hana-ha]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33635-490">To learn how to establish high availability and plan for disaster recovery of SAP HANA on Azure VMs, see [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha]</span></span>