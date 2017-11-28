---
title: "빠른 시작: Azure Virtual Machines에서 단일 인스턴스 SAP HANA 수동 설치 | Microsoft Docs"
description: "Azure Virtual Machines에서 단일 인스턴스 SAP HANA를 수동으로 설치하기 위한 빠른 시작 가이드입니다."
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: c51a2a06-6e97-429b-a346-b433a785c9f0
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 05fb31007e1e4c2243f93169129ec5b2c93099e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="quickstart-manual-installation-of-single-instance-sap-hana-on-azure-vms"></a><span data-ttu-id="19163-103">빠른 시작: Azure VMs에서 단일 인스턴스 SAP HANA 수동 설치</span><span class="sxs-lookup"><span data-stu-id="19163-103">Quickstart: Manual installation of single-instance SAP HANA on Azure VMs</span></span>
## <a name="introduction"></a><span data-ttu-id="19163-104">소개</span><span class="sxs-lookup"><span data-stu-id="19163-104">Introduction</span></span>
<span data-ttu-id="19163-105">이 가이드는 SAP NetWeaver 7.5 및 SAP HANA 1.0 SP12를 수동으로 설치할 때 Azure VM(가상 컴퓨터)에서 단일 인스턴스 SAP HANA를 설정하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-105">This guide helps you set up a single-instance SAP HANA on Azure virtual machines (VMs) when you install SAP NetWeaver 7.5 and SAP HANA 1.0 SP12 manually.</span></span> <span data-ttu-id="19163-106">따라서 SAP HANA를 Azure에 배포하는 데 중점을 두고 있으며,</span><span class="sxs-lookup"><span data-stu-id="19163-106">The focus of this guide is on deploying SAP HANA on Azure.</span></span> <span data-ttu-id="19163-107">SAP 설명서를 대체하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-107">It does not replace SAP documentation.</span></span> 

>[!Note]
><span data-ttu-id="19163-108">이 가이드에서는 Azure VM에 SAP HANA를 배포하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-108">This guide describes deployments of SAP HANA into Azure VMs.</span></span> <span data-ttu-id="19163-109">HANA 큰 인스턴스에 SAP HANA를 배포하는 방법에 대한 자세한 내용은 [Azure VM(가상 컴퓨터)에서 SAP 사용](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/get-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19163-109">For information on deploying SAP HANA into HANA large instances, see [Using SAP on Azure virtual machines (VMs)](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/get-started).</span></span>
 
## <a name="prerequisites"></a><span data-ttu-id="19163-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="19163-110">Prerequisites</span></span>
<span data-ttu-id="19163-111">여기서는 다음과 같은 IaaS(Infrastructure as a Service) 기본 사항에 대해 잘 알고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-111">This guide assumes that you are familiar with such infrastructure as a service (IaaS) basics as:</span></span>
 * <span data-ttu-id="19163-112">Azure Portal 또는 PowerShell을 통해 가상 컴퓨터 또는 가상 네트워크를 배포하는 방법</span><span class="sxs-lookup"><span data-stu-id="19163-112">How to deploy virtual machines or virtual networks via the Azure portal or PowerShell.</span></span>
 * <span data-ttu-id="19163-113">JSON(JavaScript Object Notification) 템플릿을 사용할 수 있는 옵션을 포함한 Azure 플랫폼 간 CLI(명령줄 인터페이스)</span><span class="sxs-lookup"><span data-stu-id="19163-113">The Azure cross-platform command-line interface (CLI), including the option to use JavaScript Object Notation (JSON) templates.</span></span>

<span data-ttu-id="19163-114">또한 다음에 대해서도 잘 알고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-114">This guide also assumes that you are familiar with:</span></span>
* <span data-ttu-id="19163-115">SAP HANA, SAP NetWeaver 및 온-프레미스에 설치하는 방법</span><span class="sxs-lookup"><span data-stu-id="19163-115">SAP HANA and SAP NetWeaver and how to install them on-premises.</span></span>
* <span data-ttu-id="19163-116">Azure에서 SAP HANA 및 SAP 응용 프로그램 인스턴스 설치 및 조작</span><span class="sxs-lookup"><span data-stu-id="19163-116">Installing and operating SAP HANA and SAP application instances on Azure.</span></span>
* <span data-ttu-id="19163-117">다음 개념 및 절차:</span><span class="sxs-lookup"><span data-stu-id="19163-117">The following concepts and procedures:</span></span>
   * <span data-ttu-id="19163-118">Azure에서의 SAP 배포 계획(Azure Virtual Network 계획 및 Azure Storage 사용 포함) -</span><span class="sxs-lookup"><span data-stu-id="19163-118">Planning for SAP deployment on Azure, including Azure Virtual Network  planning and Azure Storage usage.</span></span> <span data-ttu-id="19163-119">[Azure VMs(Virtual Machines)에서 SAP NetWeaver - 계획 및 구현 가이드](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/planning-guide) 참조</span><span class="sxs-lookup"><span data-stu-id="19163-119">See [SAP NetWeaver on Azure Virtual Machines (VMs) - Planning and implementation guide](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/planning-guide).</span></span>
   * <span data-ttu-id="19163-120">Azure에 VM을 배포하는 배포 원칙 및 방법 -</span><span class="sxs-lookup"><span data-stu-id="19163-120">Deployment principles and ways to deploy VMs in Azure.</span></span> <span data-ttu-id="19163-121">[SAP용 Azure Virtual Machines 배포](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/deployment-guide) 참조</span><span class="sxs-lookup"><span data-stu-id="19163-121">See [Azure Virtual Machines deployment for SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/deployment-guide).</span></span>
   * <span data-ttu-id="19163-122">Azure의 SAP NetWeaver ASCS(ABAP SAP Central Services), SCS(SAP Central Services) 및 ERS(입고 기준 자동 정산)에 대한 고가용성 -</span><span class="sxs-lookup"><span data-stu-id="19163-122">High availability for SAP NetWeaver ASCS (ABAP SAP Central Services), SCS (SAP Central Services), and ERS (Evaluated Receipt Settlement) on Azure.</span></span> <span data-ttu-id="19163-123">[Azure VM에서 SAP NetWeaver에 대한 고가용성](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide) 참조</span><span class="sxs-lookup"><span data-stu-id="19163-123">See [High availability for SAP NetWeaver on Azure VMs](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide).</span></span>
   * <span data-ttu-id="19163-124">Azure에서 ASCS/SCS의 다중 SID 설치를 활용하여 효율성을 향상시키는 방법에 대한 세부 정보 -</span><span class="sxs-lookup"><span data-stu-id="19163-124">Details on how to improve efficiency in leveraging a multi-SID installation of ASCS/SCS on Azure.</span></span> <span data-ttu-id="19163-125">[SAP NetWeaver 다중 SID 구성 만들기](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-multi-sid) 참조</span><span class="sxs-lookup"><span data-stu-id="19163-125">See [Create a SAP NetWeaver multi-SID configuration](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-multi-sid).</span></span> 
   * <span data-ttu-id="19163-126">Azure에서 Linux 기반 VM에 기반한 SAP NetWeaver 실행 원칙 -</span><span class="sxs-lookup"><span data-stu-id="19163-126">Principles of running SAP NetWeaver based on Linux-driven VMs in Azure.</span></span> <span data-ttu-id="19163-127">[Microsoft Azure SUSE Linux VM에서 SAP NetWeaver 실행](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/suse-quickstart) 참조.</span><span class="sxs-lookup"><span data-stu-id="19163-127">See [Running SAP NetWeaver on Microsoft Azure SUSE Linux VMs](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/suse-quickstart).</span></span> <span data-ttu-id="19163-128">이 가이드에서는 Azure VM의 Linux에 대한 특정 설정과 Linux VM에 Azure 저장소 디스크를 Linux VM에 올바르게 연결하는 방법에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-128">This guide provides specific settings for Linux in Azure VMs and details on how to properly attach Azure storage disks to Linux VMs.</span></span>

<span data-ttu-id="19163-129">현재 Azure VM은 SAP HANA 강화 구성에 대해서만 SAP에서 인증되었습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-129">At this time, Azure VMs are certified by SAP for SAP HANA scale-up configurations only.</span></span> <span data-ttu-id="19163-130">SAP HANA 워크로드를 포함한 스케일 아웃 구성은 아직 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-130">Scale-out configurations with SAP HANA workloads are not yet supported.</span></span> <span data-ttu-id="19163-131">강화 구성 시의 SAP HANA 고가용성은 [Azure VMs(Virtual Machines)의 SAP HANA 고가용성](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-high-availability)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19163-131">For SAP HANA high availability in cases of scale-up configurations, see [High availability of SAP HANA on Azure virtual machines (VMs)](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-high-availability).</span></span>

<span data-ttu-id="19163-132">SAP HANA 인스턴스 또는 S/4HANA 또는 BW/4HANA 시스템을 매우 빠른 시간 내에 배포하려는 경우 [SAP 클라우드 어플라이언스 라이브러리](http://cal.sap.com)를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-132">If you are seeking to get an SAP HANA instance or S/4HANA, or BW/4HANA system deployed in very fast time, you should consider the usage of [SAP Cloud Appliance Library](http://cal.sap.com).</span></span> <span data-ttu-id="19163-133">예를 들어 Azure에서 SAP CAL을 통해 S/4HANA 시스템을 배포하는 방법에 대한 설명서는 [이 가이드](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-133">You can find documentation about deploying, for example, an S/4HANA system through SAP CAL on Azure in [this guide](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h).</span></span> <span data-ttu-id="19163-134">SAP 클라우드 어플라이언스 라이브러리에 등록할 수 있는 Azure 구독 및 SAP 사용자만 있으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19163-134">All you need to have is an Azure subscription and an SAP user that can be registered with SAP Cloud Appliance Library.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="19163-135">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="19163-135">Additional resources</span></span>
### <a name="sap-hana-backup"></a><span data-ttu-id="19163-136">SAP HANA 백업</span><span class="sxs-lookup"><span data-stu-id="19163-136">SAP HANA backup</span></span>
<span data-ttu-id="19163-137">Azure VM에서 SAP HANA 데이터베이스를 백업하는 방법에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19163-137">For information on backing up SAP HANA databases on Azure VMs, see:</span></span>
* [<span data-ttu-id="19163-138">Azure Virtual Machines의 SAP HANA 백업 가이드</span><span class="sxs-lookup"><span data-stu-id="19163-138">Backup guide for SAP HANA on Azure Virtual Machines</span></span>](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-guide)
* [<span data-ttu-id="19163-139">파일 수준의 SAP HANA Azure 백업</span><span class="sxs-lookup"><span data-stu-id="19163-139">SAP HANA Azure Backup on file level</span></span>](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-file-level)
* [<span data-ttu-id="19163-140">저장소 스냅숏에 기반한 SAP HANA 백업</span><span class="sxs-lookup"><span data-stu-id="19163-140">SAP HANA backup based on storage snapshots</span></span>](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-storage-snapshots)

### <a name="sap-cloud-appliance-library"></a><span data-ttu-id="19163-141">SAP 클라우드 어플라이언스 라이브러리</span><span class="sxs-lookup"><span data-stu-id="19163-141">SAP Cloud Appliance Library</span></span>
<span data-ttu-id="19163-142">SAP 클라우드 어플라이언스 라이브러리를 사용하여 S/4HANA 또는 BW/4HANA를 배포하는 방법에 대한 내용은 [Microsoft Azure에서 SAP S/4HANA 또는 BW/4HANA 배포](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19163-142">For information on using SAP Cloud Appliance Library to deploy S/4HANA or BW/4HANA, see [Deploy SAP S/4HANA or BW/4HANA on Microsoft Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h).</span></span>

### <a name="sap-hana-supported-operating-systems"></a><span data-ttu-id="19163-143">SAP HANA 지원 운영 체제</span><span class="sxs-lookup"><span data-stu-id="19163-143">SAP HANA-supported operating systems</span></span>
<span data-ttu-id="19163-144">SAP HANA 지원 운영 체제에 대한 내용은 [SAP Support Note #2235581 - SAP HANA: 지원되는 운영 체제](https://launchpad.support.sap.com/#/notes/2235581/E)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19163-144">For information on SAP HANA-supported operating systems, see [SAP Support Note #2235581 - SAP HANA: Supported Operating Systems](https://launchpad.support.sap.com/#/notes/2235581/E).</span></span> <span data-ttu-id="19163-145">Azure VM은 이러한 운영 체제의 하위 집합만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-145">Azure VMs support only a subset of these operating systems.</span></span> <span data-ttu-id="19163-146">Azure에서 SAP HANA를 배포하는 데 지원되는 운영 체제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-146">The following operating systems are supported to deploy SAP HANA on Azure:</span></span> 

* <span data-ttu-id="19163-147">SUSE Linux Enterprise Server 12.x</span><span class="sxs-lookup"><span data-stu-id="19163-147">SUSE Linux Enterprise Server 12.x</span></span>
* <span data-ttu-id="19163-148">Red Hat Enterprise Linux 7.2</span><span class="sxs-lookup"><span data-stu-id="19163-148">Red Hat Enterprise Linux 7.2</span></span>

<span data-ttu-id="19163-149">SAP HANA 및 다른 Linux 운영 체제에 대한 SAP 추가 설명서는 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19163-149">For additional SAP documentation about SAP HANA and different Linux operating systems, see:</span></span>

* <span data-ttu-id="19163-150">[SAP Support Note #171356 – SAP Software on Linux: 일반 정보](https://launchpad.support.sap.com/#/notes/1984787)(영문)</span><span class="sxs-lookup"><span data-stu-id="19163-150">[SAP Support Note #171356 - SAP Software on Linux:  General Information](https://launchpad.support.sap.com/#/notes/1984787)</span></span>
* <span data-ttu-id="19163-151">[SAP Support Note #1944799 – SLES 운영 체제 설치를 위한 SAP HANA 지침](http://go.sap.com/documents/2016/05/e8705aae-717c-0010-82c7-eda71af511fa.html)(영문)</span><span class="sxs-lookup"><span data-stu-id="19163-151">[SAP Support Note #1944799 - SAP HANA Guidelines for SLES Operating System Installation](http://go.sap.com/documents/2016/05/e8705aae-717c-0010-82c7-eda71af511fa.html)</span></span>
* <span data-ttu-id="19163-152">[SAP Support Note #2205917 – SAP HANA DB: SLES 12 for SAP Applications를 위한 권장 OS 설정](https://launchpad.support.sap.com/#/notes/2205917/E)(영문)</span><span class="sxs-lookup"><span data-stu-id="19163-152">[SAP Support Note #2205917 - SAP HANA DB Recommended OS Settings for SLES 12 for SAP Applications](https://launchpad.support.sap.com/#/notes/2205917/E)</span></span>
* <span data-ttu-id="19163-153">[SAP Support Note #1984787 – SUSE Linux Enterprise Server 12: 설치 참고](https://launchpad.support.sap.com/#/notes/1984787)(영문)</span><span class="sxs-lookup"><span data-stu-id="19163-153">[SAP Support Note #1984787 - SUSE Linux Enterprise Server 12:  Installation Notes](https://launchpad.support.sap.com/#/notes/1984787)</span></span>
* <span data-ttu-id="19163-154">[SAP Support Note #1391070 – Linux UUID 솔루션](https://launchpad.support.sap.com/#/notes/1391070)(영문)</span><span class="sxs-lookup"><span data-stu-id="19163-154">[SAP Support Note #1391070 - Linux UUID Solutions](https://launchpad.support.sap.com/#/notes/1391070)</span></span>
* [<span data-ttu-id="19163-155">SAP Support Note #2009879 – RHEL(Red Hat Enterprise Linux) 운영 체제에 대한 SAP HANA 지침</span><span class="sxs-lookup"><span data-stu-id="19163-155">SAP Support Note #2009879 - SAP HANA Guidelines for Red Hat Enterprise Linux (RHEL) Operating System</span></span>](https://launchpad.support.sap.com/#/notes/2009879)
* [<span data-ttu-id="19163-156">2292690 - SAP HANA DB: RHEL 7에 대한 권장 OS 설정</span><span class="sxs-lookup"><span data-stu-id="19163-156">2292690 - SAP HANA DB: Recommended OS settings for RHEL 7</span></span>](https://launchpad.support.sap.com/#/notes/2292690/E)

### <a name="sap-monitoring-in-azure"></a><span data-ttu-id="19163-157">Azure에서 SAP 모니터링</span><span class="sxs-lookup"><span data-stu-id="19163-157">SAP monitoring in Azure</span></span>
<span data-ttu-id="19163-158">Azure에서 SAP를 모니터링하는 방법에 대한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19163-158">For information about SAP monitoring in Azure, see:</span></span>

* <span data-ttu-id="19163-159">[SAP Note 2191498](https://launchpad.support.sap.com/#/notes/2191498/E)(영문) -</span><span class="sxs-lookup"><span data-stu-id="19163-159">[SAP Note 2191498](https://launchpad.support.sap.com/#/notes/2191498/E).</span></span> <span data-ttu-id="19163-160">Azure에서 Linux VM을 사용한 SAP "고급 모니터링"에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-160">This note discusses SAP "enhanced monitoring" with Linux VMs on Azure.</span></span> 
* <span data-ttu-id="19163-161">[SAP Note 1102124](https://launchpad.support.sap.com/#/notes/1102124/E)(영문) -</span><span class="sxs-lookup"><span data-stu-id="19163-161">[SAP Note 1102124](https://launchpad.support.sap.com/#/notes/1102124/E).</span></span> <span data-ttu-id="19163-162">SAPOSCOL on Linux에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-162">This note discusses information about SAPOSCOL on Linux.</span></span> 
* <span data-ttu-id="19163-163">[SAP Note 2178632](https://launchpad.support.sap.com/#/notes/2178632/E)(영문) -</span><span class="sxs-lookup"><span data-stu-id="19163-163">[SAP Note 2178632](https://launchpad.support.sap.com/#/notes/2178632/E).</span></span> <span data-ttu-id="19163-164">Microsoft Azure의 SAP용 주요 모니터링 메트릭에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-164">This note discusses key monitoring metrics for SAP on Microsoft Azure.</span></span>

### <a name="azure-vm-types"></a><span data-ttu-id="19163-165">Azure VM 유형</span><span class="sxs-lookup"><span data-stu-id="19163-165">Azure VM types</span></span>
<span data-ttu-id="19163-166">SAP HANA와 함께 사용되는 Azure VM 유형 및 SAP 지원 워크로드 시나리오는 [SAP 인증 IaaS 플랫폼](https://www.sap.com/dmc/exp/2014-09-02-hana-hardware/enEN/iaas.html)(영문)에서 설명하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-166">Azure VM types and SAP-supported workload scenarios used with SAP HANA are documented in [SAP certified IaaS Platforms](https://www.sap.com/dmc/exp/2014-09-02-hana-hardware/enEN/iaas.html).</span></span> 

<span data-ttu-id="19163-167">SAP NetWeaver 또는 S/4HANA 응용 프로그램 계층에 대해 SAP에서 인증한 Azure VM 유형은 [SAP Note 1928533 - SAP Applications on Azure: 지원 제품 및 Azure VM 유형](https://launchpad.support.sap.com/#/notes/1928533/E)(영문)에서 설명하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-167">Azure VM types that are certified by SAP for SAP NetWeaver or the S/4HANA application layer are documented in [SAP Note 1928533 - SAP Applications on Azure: Supported Products and Azure VM types](https://launchpad.support.sap.com/#/notes/1928533/E).</span></span>

>[!Note]
><span data-ttu-id="19163-168">SAP-Linux-Azure 통합은 Azure Resource Manager에서만 지원하며, 클래식 배포 모델에서는 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-168">SAP-Linux-Azure integration is supported only on Azure Resource Manager and not the classic deployment model.</span></span> 

## <a name="manual-installation-of-sap-hana"></a><span data-ttu-id="19163-169">SAP HANA 수동 설치</span><span class="sxs-lookup"><span data-stu-id="19163-169">Manual installation of SAP HANA</span></span>
<span data-ttu-id="19163-170">이 가이드에서는 다음 두 가지 방법으로 Azure VM에 SAP HANA를 수동으로 설치하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-170">This guide describes how to manually install SAP HANA on Azure VMs in two different ways:</span></span>

* <span data-ttu-id="19163-171">"데이터베이스 인스턴스 설치" 단계에서 분산형 NetWeaver 설치의 일부로 SWPM(SAP Software Provisioning Manager) 사용</span><span class="sxs-lookup"><span data-stu-id="19163-171">By using SAP Software Provisioning Manager (SWPM) as part of a distributed NetWeaver installation in the "install database instance" step</span></span>
* <span data-ttu-id="19163-172">SAP HANA 데이터베이스 수명 주기 관리자 도구인 HDBLCM 사용 후 NetWeaver 설치</span><span class="sxs-lookup"><span data-stu-id="19163-172">By using the SAP HANA database lifecycle manager tool, HDBLCM, and then installing NetWeaver</span></span>

<span data-ttu-id="19163-173">또한 이 [SAP HANA 블로그 알림](https://blogs.saphana.com/2013/12/31/announcement-sap-hana-and-sap-netweaver-as-abap-deployed-on-one-server-is-generally-available/)에서 설명한 대로 SWPM을 사용하여 단일 VM에 모든 구성 요소(SAP HANA, SAP 응용 프로그램 서버 및 ASCS 인스턴스)를 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-173">You can also use SWPM to install all components (SAP HANA, the SAP application server, and the ASCS instance) in one single VM, as described in this [SAP HANA blog announcement](https://blogs.saphana.com/2013/12/31/announcement-sap-hana-and-sap-netweaver-as-abap-deployed-on-one-server-is-generally-available/).</span></span> <span data-ttu-id="19163-174">이 빠른 시작 가이드에서는 이 옵션을 설명하지 않지만 고려해야 하는 문제는 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-174">This option isn't described in this Quickstart guide, but the issues that you must take into consideration are the same.</span></span>

<span data-ttu-id="19163-175">설치를 시작하기 전에 이 안내서 뒷부분에 있는 "SAP HANA 수동 설치를 위한 Azure VM 준비" 섹션을 참조하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-175">Before you start an installation, we recommend that you read the "Preparing Azure VMs for manual installation of SAP HANA" section later in this guide.</span></span> <span data-ttu-id="19163-176">이렇게 하면 기본 Azure VM 구성만 사용할 때 발생할 수 있는 몇 가지 기본적인 실수를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-176">Doing so can help prevent several basic mistakes that might occur when you use only a default Azure VM configuration.</span></span>

## <a name="key-steps-for-sap-hana-installation-when-you-use-sap-swpm"></a><span data-ttu-id="19163-177">SAP SWPM 사용 시 SAP HANA 설치를 위한 주요 단계</span><span class="sxs-lookup"><span data-stu-id="19163-177">Key steps for SAP HANA installation when you use SAP SWPM</span></span>
<span data-ttu-id="19163-178">이 섹션에서는 SAP SWPM을 사용하여 분산형 SAP NetWeaver 7.5를 설치할 때의 단일 인스턴스 SAP HANA 수동 설치의 주요 단계를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-178">This section lists the key steps for a manual, single-instance SAP HANA installation when you use SAP SWPM to perform a distributed SAP NetWeaver 7.5 installation.</span></span> <span data-ttu-id="19163-179">개별 단계는 이 가이드의 뒷부분에 나오는 스크린샷에서 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-179">The individual steps are explained in more detail in screenshots later in this guide.</span></span>

1. <span data-ttu-id="19163-180">2개 테스트 VM이 포함된 Azure 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="19163-180">Create an Azure virtual network that includes two test VMs.</span></span>
2. <span data-ttu-id="19163-181">Azure Resource Manager 모델에 따라 운영 체제(이 예제에서는 SLES(SUSE Linux Enterprise Server) 및 SLES for SAP Applications 12 SP1)가 포함된 2개의 Azure VM을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-181">Deploy the two Azure VMs with operating systems (in our example, SUSE Linux Enterprise Server (SLES) and SLES for SAP Applications 12 SP1), according to the Azure Resource Manager model.</span></span>
3. <span data-ttu-id="19163-182">응용 프로그램 서버 VM에 2개의 Azure 표준 또는 프리미엄 저장소 디스크(예: 75GB 및 500GB 디스크)를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-182">Attach two Azure standard or premium storage disks (for example, 75-GB or 500-GB disks) to the application server VM.</span></span>
4. <span data-ttu-id="19163-183">HANA DB 서버 VM에 프리미엄 저장소 디스크를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-183">Attach premium storage disks to the HANA DB server VM.</span></span> <span data-ttu-id="19163-184">자세한 내용은 이 설명서의 뒷부분에 나오는 "디스크 설정" 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19163-184">For details, see the "Disk setup" section later in this guide.</span></span>
5. <span data-ttu-id="19163-185">크기 또는 처리량 요구 사항에 따라 여러 디스크를 연결한 다음 VM 내부의 OS 수준에서 논리 볼륨 관리 또는 MDADM(다중 장치 관리 도구)을 사용하여 스트라이프 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="19163-185">Depending on size or throughput requirements, attach multiple disks, and then create striped volumes by using either logical volume management or a multiple-devices administration tool (MDADM) at the OS level inside the VM.</span></span>
6. <span data-ttu-id="19163-186">연결된 디스크 또는 논리 볼륨에 XFS 파일 시스템을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="19163-186">Create XFS file systems on the attached disks or logical volumes.</span></span>
7. <span data-ttu-id="19163-187">새 XFS 파일 시스템을 OS 수준에서 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-187">Mount the new XFS file systems at the OS level.</span></span> <span data-ttu-id="19163-188">모든 SAP 소프트웨어에 대해 하나의 파일 시스템을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-188">Use one file system for all the SAP software.</span></span> <span data-ttu-id="19163-189">다른 소프트웨어(예: /sapmnt 디렉터리 및 백업)에는 다른 파일 시스템을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-189">Use the other file system for the /sapmnt directory and backups, for example.</span></span> <span data-ttu-id="19163-190">SAP HANA DB 서버에서 XFS 파일 시스템을 프리미엄 저장소 디스크(예: /hana 및 /usr/sap)에 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-190">On the SAP HANA DB server, mount the XFS file systems on the premium storage disks as /hana and /usr/sap.</span></span> <span data-ttu-id="19163-191">이 프로세스는 Linux Azure VM에서 크지 않은 루트 파일 시스템이 가득 차지 않도록 방지하기 위해 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-191">This process is necessary to prevent the root file system, which isn't large on Linux Azure VMs, from filling up.</span></span>
8. <span data-ttu-id="19163-192">/etc/hosts 파일에 테스트 VM의 로컬 IP 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-192">Enter the local IP addresses of the test VMs in the /etc/hosts file.</span></span>
9. <span data-ttu-id="19163-193">/etc/fstab 파일에 **nofail** 매개 변수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-193">Enter the **nofail** parameter in the /etc/fstab file.</span></span>
10. <span data-ttu-id="19163-194">사용 중인 Linux OS 릴리스에 따라 Linux 커널 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-194">Set Linux kernel parameters according to the Linux OS release you are using.</span></span> <span data-ttu-id="19163-195">자세한 내용은 HANA에 대해 설명하는 해당 SAP Note 및 이 가이드의 "커널 매개 변수" 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19163-195">For more information, see the appropriate SAP notes that discuss HANA and the "Kernel parameters" section in this guide.</span></span>
11. <span data-ttu-id="19163-196">교환 공간 추가</span><span class="sxs-lookup"><span data-stu-id="19163-196">Add swap space.</span></span>
12. <span data-ttu-id="19163-197">선택적으로 테스트 VM에 그래픽 데스크톱 설치,</span><span class="sxs-lookup"><span data-stu-id="19163-197">Optionally, install a graphical desktop on the test VMs.</span></span> <span data-ttu-id="19163-198">그렇지 않은 경우 원격 SAPinst 설치 사용</span><span class="sxs-lookup"><span data-stu-id="19163-198">Otherwise, use a remote SAPinst installation.</span></span>
13. <span data-ttu-id="19163-199">SAP Service Marketplace에서 SAP 소프트웨어를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-199">Download the SAP software from the SAP Service Marketplace.</span></span>
14. <span data-ttu-id="19163-200">앱 서버 VM에 SAP ASCS 인스턴스 설치</span><span class="sxs-lookup"><span data-stu-id="19163-200">Install the SAP ASCS instance on the app server VM.</span></span>
15. <span data-ttu-id="19163-201">NFS를 사용하여 테스트 VM 간에 /sapmnt 디렉터리 공유 -</span><span class="sxs-lookup"><span data-stu-id="19163-201">Share the /sapmnt directory among the test VMs by using NFS.</span></span> <span data-ttu-id="19163-202">응용 프로그램 서버 VM은 NFS 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="19163-202">The application server VM is the NFS server.</span></span>
16. <span data-ttu-id="19163-203">DB 서버 VM에서 SWPM을 사용하여 HANA를 포함한 데이터베이스 인스턴스 설치</span><span class="sxs-lookup"><span data-stu-id="19163-203">Install the database instance, including HANA, by using SWPM on the DB server VM.</span></span>
17. <span data-ttu-id="19163-204">응용 프로그램 서버 VM에 PAS(기본 응용 프로그램 서버)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-204">Install the primary application server (PAS) on the application server VM.</span></span>
18. <span data-ttu-id="19163-205">SAP MC(SAP 관리 콘솔)를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-205">Start SAP Management Console (SAP MC).</span></span> <span data-ttu-id="19163-206">예를 들어 SAP GUI 또는 HANA Studio와 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-206">Connect with SAP GUI or HANA Studio, for example.</span></span>

## <a name="key-steps-for-sap-hana-installation-when-you-use-hdblcm"></a><span data-ttu-id="19163-207">HDBLCM 사용 시 SAP HANA 설치를 위한 주요 단계</span><span class="sxs-lookup"><span data-stu-id="19163-207">Key steps for SAP HANA installation when you use HDBLCM</span></span>
<span data-ttu-id="19163-208">이 섹션에서는 SAP HDBLCM을 사용하여 분산형 SAP NetWeaver 7.5를 설치할 때의 단일 인스턴스 SAP HANA 수동 설치의 주요 단계를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-208">This section lists the key steps for a manual, single-instance SAP HANA installation when you use SAP HDBLCM to perform a distributed SAP NetWeaver 7.5 installation.</span></span> <span data-ttu-id="19163-209">개별 단계는 이 가이드의 스크린샷에서 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-209">The individual steps are explained in more detail in screenshots throughout this guide.</span></span>

1. <span data-ttu-id="19163-210">2개 테스트 VM이 포함된 Azure 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="19163-210">Create an Azure virtual network that includes two test VMs.</span></span>
2. <span data-ttu-id="19163-211">Azure Resource Manager 모델에 따라 운영 체제(이 예제에서는 SLES 및 SLES for SAP Applications 12 SP1)가 포함된 2개의 Azure VM을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-211">Deploy two Azure VMs with operating systems (in our example, SLES and SLES for SAP Applications 12 SP1) according to the Azure Resource Manager model.</span></span>
3. <span data-ttu-id="19163-212">앱 서버 VM에 2개의 Azure 표준 또는 프리미엄 저장소 디스크(예: 75GB 및 500GB 디스크)를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-212">Attach two Azure standard or premium storage disks (for example, 75-GB or 500-GB disks) to the app server VM.</span></span>
4. <span data-ttu-id="19163-213">HANA DB 서버 VM에 프리미엄 저장소 디스크를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-213">Attach premium storage disks to the HANA DB server VM.</span></span> <span data-ttu-id="19163-214">자세한 내용은 이 설명서의 뒷부분에 나오는 "디스크 설정" 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19163-214">For details, see the "Disk setup" section later in this guide.</span></span>
5. <span data-ttu-id="19163-215">크기 또는 처리량 요구 사항에 따라 여러 디스크를 연결하고 VM 내부의 OS 수준에서 LVM(논리 볼륨 관리) 또는 MDADM(다중 장치 관리 도구)을 사용하여 스트라이프 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="19163-215">Depending on size or throughput requirements, attach multiple disks and create striped volumes by using either logical volume management or a multiple-devices administration tool (MDADM) at the OS level inside the VM.</span></span>
6. <span data-ttu-id="19163-216">연결된 디스크 또는 논리 볼륨에 XFS 파일 시스템을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="19163-216">Create XFS file systems on the attached disks or logical volumes.</span></span>
7. <span data-ttu-id="19163-217">새 XFS 파일 시스템을 OS 수준에서 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-217">Mount the new XFS file systems at the OS level.</span></span> <span data-ttu-id="19163-218">모든 SAP 소프트웨어에 대해 하나의 파일 시스템을 사용하고, 다른 소프트웨어(예: /sapmnt 디렉터리 및 백업)에는 다른 파일 시스템을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-218">Use one file system for all the SAP software, and use the other one for the /sapmnt directory and backups, for example.</span></span> <span data-ttu-id="19163-219">SAP HANA DB 서버에서 XFS 파일 시스템을 프리미엄 저장소 디스크(예: /hana 및 /usr/sap)에 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-219">On the SAP HANA DB server, mount the XFS file systems on the premium storage disks as /hana and /usr/sap.</span></span> <span data-ttu-id="19163-220">이 프로세스는 Linux Azure VM에서 크지 않은 루트 파일 시스템이 가득 차지 않도록 방지하기 위해 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-220">This process is necessary to help prevent the root file system, which isn't large on Linux Azure VMs, from filling up.</span></span>
8. <span data-ttu-id="19163-221">/etc/hosts 파일에 테스트 VM의 로컬 IP 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-221">Enter the local IP addresses of the test VMs in the /etc/hosts file.</span></span>
9. <span data-ttu-id="19163-222">/etc/fstab 파일에 **nofail** 매개 변수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-222">Enter the **nofail** parameter in the /etc/fstab file.</span></span>
10. <span data-ttu-id="19163-223">사용 중인 Linux OS 릴리스에 따라 커널 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-223">Set kernel parameters according to the Linux OS release you are using.</span></span> <span data-ttu-id="19163-224">자세한 내용은 HANA에 대해 설명하는 해당 SAP Note 및 이 가이드의 "커널 매개 변수" 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19163-224">For more information, see the appropriate SAP notes that discuss HANA and the "Kernel parameters" section in this guide.</span></span>
11. <span data-ttu-id="19163-225">교환 공간 추가</span><span class="sxs-lookup"><span data-stu-id="19163-225">Add swap space.</span></span>
12. <span data-ttu-id="19163-226">선택적으로 테스트 VM에 그래픽 데스크톱 설치,</span><span class="sxs-lookup"><span data-stu-id="19163-226">Optionally, install a graphical desktop on the test VMs.</span></span> <span data-ttu-id="19163-227">그렇지 않은 경우 원격 SAPinst 설치 사용</span><span class="sxs-lookup"><span data-stu-id="19163-227">Otherwise, use a remote SAPinst installation.</span></span>
13. <span data-ttu-id="19163-228">SAP Service Marketplace에서 SAP 소프트웨어를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-228">Download the SAP software from the SAP Service Marketplace.</span></span>
14. <span data-ttu-id="19163-229">HANA DB 서버 VM에 그룹 ID가 1001인 sapsys 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="19163-229">Create a group, sapsys, with group ID 1001, on the HANA DB server VM.</span></span>
15. <span data-ttu-id="19163-230">HDBLCM(HANA 데이터베이스 수명 주기 관리자)을 사용하여 DB 서버 VM에 SAP HANA를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-230">Install SAP HANA on the DB server VM by using HANA Database Lifecycle Manager (HDBLCM).</span></span>
16. <span data-ttu-id="19163-231">앱 서버 VM에 SAP ASCS 인스턴스 설치</span><span class="sxs-lookup"><span data-stu-id="19163-231">Install the SAP ASCS instance on the app server VM.</span></span>
17. <span data-ttu-id="19163-232">NFS를 사용하여 테스트 VM 간에 /sapmnt 디렉터리 공유 -</span><span class="sxs-lookup"><span data-stu-id="19163-232">Share the /sapmnt directory among the test VMs by using NFS.</span></span> <span data-ttu-id="19163-233">응용 프로그램 서버 VM은 NFS 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="19163-233">The application server VM is the NFS server.</span></span>
18. <span data-ttu-id="19163-234">HANA DB 서버 VM에 SWPM을 통해 HANA를 포함한 데이터베이스 인스턴스 설치</span><span class="sxs-lookup"><span data-stu-id="19163-234">Install the database instance, including HANA, by using SWPM on the HANA DB server VM.</span></span>
19. <span data-ttu-id="19163-235">응용 프로그램 서버 VM에 PAS(기본 응용 프로그램 서버)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-235">Install the primary application server (PAS) on the application server VM.</span></span>
20. <span data-ttu-id="19163-236">SAP MC를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-236">Start SAP MC.</span></span> <span data-ttu-id="19163-237">SAP GUI 또는 HANA Studio를 통해 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-237">Connect through SAP GUI or HANA Studio.</span></span>

## <a name="preparing-azure-vms-for-a-manual-installation-of-sap-hana"></a><span data-ttu-id="19163-238">SAP HANA 수동 설치를 위한 Azure VM 준비</span><span class="sxs-lookup"><span data-stu-id="19163-238">Preparing Azure VMs for a manual installation of SAP HANA</span></span>
<span data-ttu-id="19163-239">이 섹션에서는 다음 항목을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="19163-239">This section covers the following topics:</span></span>

* <span data-ttu-id="19163-240">OS 업데이트</span><span class="sxs-lookup"><span data-stu-id="19163-240">OS updates</span></span>
* <span data-ttu-id="19163-241">디스크 설정</span><span class="sxs-lookup"><span data-stu-id="19163-241">Disk setup</span></span>
* <span data-ttu-id="19163-242">커널 매개 변수</span><span class="sxs-lookup"><span data-stu-id="19163-242">Kernel parameters</span></span>
* <span data-ttu-id="19163-243">파일 시스템</span><span class="sxs-lookup"><span data-stu-id="19163-243">File systems</span></span>
* <span data-ttu-id="19163-244">/etc/hosts 파일</span><span class="sxs-lookup"><span data-stu-id="19163-244">The /etc/hosts file</span></span>
* <span data-ttu-id="19163-245">/etc/fstab 파일</span><span class="sxs-lookup"><span data-stu-id="19163-245">The /etc/fstab file</span></span>

### <a name="os-updates"></a><span data-ttu-id="19163-246">OS 업데이트</span><span class="sxs-lookup"><span data-stu-id="19163-246">OS updates</span></span>
<span data-ttu-id="19163-247">추가 소프트웨어를 설치하기 전에 먼저 Linux OS 업데이트 및 픽스가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-247">Check for Linux OS updates and fixes before installing additional software.</span></span> <span data-ttu-id="19163-248">패치를 설치하면 지원 센터에 문의할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-248">By installing a patch, you might be able to avoid a call to the support desk.</span></span>

<span data-ttu-id="19163-249">다음을 사용하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-249">Make sure that you are using:</span></span>
* <span data-ttu-id="19163-250">SUSE Linux Enterprise Server for SAP Applications</span><span class="sxs-lookup"><span data-stu-id="19163-250">SUSE Linux Enterprise Server for SAP Applications.</span></span>
* <span data-ttu-id="19163-251">Red Hat Enterprise Linux for SAP Applications 또는 Red Hat Enterprise Linux for SAP HANA</span><span class="sxs-lookup"><span data-stu-id="19163-251">Red Hat Enterprise Linux for SAP Applications or Red Hat Enterprise Linux for SAP HANA.</span></span> 

<span data-ttu-id="19163-252">아직 등록하지 않은 경우 Linux 공급업체의 Linux 구독으로 OS 배포를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-252">If you haven't already, register the OS deployment with your Linux subscription from the Linux vendor.</span></span> <span data-ttu-id="19163-253">SUSE에는 이미 서비스를 포함하고 있고 자동으로 등록되는 SAP 응용 프로그램용 OS 이미지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-253">Note that SUSE has OS images for SAP applications that already include services and which are registered automatically.</span></span>

<span data-ttu-id="19163-254">다음은 **zypper** 명령을 사용하여 SUSE Linux에 사용할 수 있는 패치를 확인하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="19163-254">Here is an example of checking for available patches for SUSE Linux by using the **zypper** command:</span></span>

 `sudo zypper list-patches`

<span data-ttu-id="19163-255">문제의 종류에 따라 패치는 범주 및 심각도별로 분류됩니다.</span><span class="sxs-lookup"><span data-stu-id="19163-255">Depending on the kind of issue, patches are classified by category and severity.</span></span> <span data-ttu-id="19163-256">범주에 일반적으로 사용되는 값은 **security**, **recommended**, **optional**, **feature**, **document** 또는 **yast**입니다.</span><span class="sxs-lookup"><span data-stu-id="19163-256">Commonly used values for category are: **security**, **recommended**, **optional**, **feature**, **document**, or **yast**.</span></span>
<span data-ttu-id="19163-257">심각도에 일반적으로 사용되는 값은 **critical**, **important**, **moderate**, **low** 또는 **unspecified**입니다.</span><span class="sxs-lookup"><span data-stu-id="19163-257">Commonly used values for severity are: **critical**, **important**, **moderate**, **low**, or **unspecified**.</span></span>

<span data-ttu-id="19163-258">**zypper** 명령은 설치된 패키지에 필요한 업데이트만 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-258">The **zypper** command looks only for the updates that your installed packages need.</span></span> <span data-ttu-id="19163-259">예를 들어 다음 명령은 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-259">For example, you could use this command:</span></span>

`sudo zypper patch  --category=security,recommended --severity=critical,important`

<span data-ttu-id="19163-260">실제로 시스템을 업데이트하지 않고 `--dry-run` 매개 변수를 추가하여 해당 업데이트를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-260">You can add the parameter `--dry-run` to test the update without actually updating the system.</span></span>


### <a name="disk-setup"></a><span data-ttu-id="19163-261">디스크 설정</span><span class="sxs-lookup"><span data-stu-id="19163-261">Disk setup</span></span>
<span data-ttu-id="19163-262">Azure에서 Linux VM의 루트 파일 시스템의 크기는 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="19163-262">The root file system in a Linux VM on Azure has a size limitation.</span></span> <span data-ttu-id="19163-263">따라서 SAP를 실행하기 위한 추가 디스크 공간을 Azure VM에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-263">Therefore, it's necessary to attach additional disk space to an Azure VM for running SAP.</span></span> <span data-ttu-id="19163-264">SAP 응용 프로그램 서버 Azure VM의 경우 Azure 표준 저장소 디스크로도 충분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-264">For SAP application server Azure VMs, the use of Azure standard storage disks might be sufficient.</span></span> <span data-ttu-id="19163-265">그러나 SAP HANA DBMS Azure VM의 경우 프로덕션 및 비 프로덕션 구현에 대해 Azure Premium Storage 디스크를 반드시 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-265">However, for SAP HANA DBMS Azure VMs, the use of Azure Premium Storage disks for production and non-production implementations is mandatory.</span></span>

<span data-ttu-id="19163-266">[SAP HANA TDI 저장소 요구 사항](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html)(영문)에 따라 다음과 같은 Azure Premium Storage 저장소 구성이 제안됩니다.</span><span class="sxs-lookup"><span data-stu-id="19163-266">Based on the [SAP HANA TDI Storage Requirements](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html), the following Azure Premium Storage configuration is suggested:</span></span> 

| <span data-ttu-id="19163-267">VM SKU</span><span class="sxs-lookup"><span data-stu-id="19163-267">VM SKU</span></span> | <span data-ttu-id="19163-268">RAM</span><span class="sxs-lookup"><span data-stu-id="19163-268">RAM</span></span> |  <span data-ttu-id="19163-269">/hana/data 및 /hana/log</span><span class="sxs-lookup"><span data-stu-id="19163-269">/hana/data and /hana/log</span></span> <br /> <span data-ttu-id="19163-270">(LVM 또는 MDADM으로 스트라이프됨)</span><span class="sxs-lookup"><span data-stu-id="19163-270">striped with LVM or MDADM</span></span> | <span data-ttu-id="19163-271">/hana/shared</span><span class="sxs-lookup"><span data-stu-id="19163-271">/hana/shared</span></span> | <span data-ttu-id="19163-272">/root 볼륨</span><span class="sxs-lookup"><span data-stu-id="19163-272">/root volume</span></span> | <span data-ttu-id="19163-273">/usr/sap</span><span class="sxs-lookup"><span data-stu-id="19163-273">/usr/sap</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="19163-274">GS5</span><span class="sxs-lookup"><span data-stu-id="19163-274">GS5</span></span> | <span data-ttu-id="19163-275">448GB</span><span class="sxs-lookup"><span data-stu-id="19163-275">448 GB</span></span> | <span data-ttu-id="19163-276">2 x P30</span><span class="sxs-lookup"><span data-stu-id="19163-276">2 x P30</span></span> | <span data-ttu-id="19163-277">1 x P20</span><span class="sxs-lookup"><span data-stu-id="19163-277">1 x P20</span></span> | <span data-ttu-id="19163-278">1 x P10</span><span class="sxs-lookup"><span data-stu-id="19163-278">1 x P10</span></span> | <span data-ttu-id="19163-279">1 x P10</span><span class="sxs-lookup"><span data-stu-id="19163-279">1 x P10</span></span> | 

<span data-ttu-id="19163-280">제안된 디스크 구성에서 HANA 데이터 볼륨 및 로그 볼륨은 LVM 또는 MDADM으로 스트라이프된 Azure Premium Storage 디스크의 동일한 집합에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="19163-280">In the suggested disk configuration, the HANA data volume and log volume are placed on the same set of Azure premium storage disks that are striped with LVM or MDADM.</span></span> <span data-ttu-id="19163-281">Azure Premium Storage는 중복성을 위해 세 개의 디스크 이미지를 유지하므로 RAID 중복성 수준을 정의할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-281">It is not necessary to define any RAID redundancy level because Azure Premium Storage keeps three images of the disks for redundancy.</span></span> <span data-ttu-id="19163-282">충분한 저장소를 구성하려면 [SAP HANA TDI 저장소 요구 사항](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html)(영문) 및 [SAP HANA 서버 설치 및 업데이트 가이드](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19163-282">To make sure that you configure enough storage, consult the [SAP HANA TDI Storage Requirements](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) and [SAP HANA Server Installation and Update Guide](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm).</span></span> <span data-ttu-id="19163-283">또한 [VM의 고성능 Premium Storage 및 관리 디스크](https://docs.microsoft.com/azure/storage/storage-premium-storage)에서 설명한 대로 다른 Azure Premium Storage 디스크의 다른 VHD(가상 하드 디스크) 처리량도 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="19163-283">Also consider the different virtual hard disk (VHD) throughput volumes of the different Azure premium storage disks as documented in [High-performance Premium Storage and managed disks for VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage).</span></span> 

<span data-ttu-id="19163-284">HANA DBMS VM에 추가 Premium Storage 디스크를 추가하여 데이터베이스 또는 트랜잭션 로그 백업을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-284">You can add more premium storage disks to the HANA DBMS VMs for storing database or transaction log backups.</span></span>

<span data-ttu-id="19163-285">스트라이핑 구성에 사용되는 두 가지 주요 도구에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19163-285">For more information about the two main tools used to configure striping, see the following articles:</span></span>

* [<span data-ttu-id="19163-286">Linux에서 소프트웨어 RAID 구성</span><span class="sxs-lookup"><span data-stu-id="19163-286">Configure software RAID on Linux</span></span>](../../linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="19163-287">Azure에서 Linux VM에 LVM 구성</span><span class="sxs-lookup"><span data-stu-id="19163-287">Configure LVM on a Linux VM in Azure</span></span>](../../linux/configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="19163-288">Linux를 게스트 OS로 실행하는 Azure VM에 디스크를 연결하는 방법에 대한 자세한 내용은 [Linux VM에 디스크 추가](../../linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19163-288">For more information on attaching disks to Azure VMs running Linux as a guest OS, see [Add a disk to a Linux VM](../../linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="19163-289">Azure Premium Storage에서는 디스크 캐싱 모드를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-289">Azure Premium Storage allows you to define disk caching modes.</span></span> <span data-ttu-id="19163-290">/hana/data 및 /hana/log를 보유하는 스트라이프 집합의 경우 디스크 캐싱을 비활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-290">For the striped set holding /hana/data and /hana/log, disk caching should be disabled.</span></span> <span data-ttu-id="19163-291">다른 볼륨(디스크)의 경우 캐싱 모드를 **ReadOnly**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-291">For the other volumes (disks), the caching mode should be set to **ReadOnly**.</span></span>

<span data-ttu-id="19163-292">자세한 내용은 [Premium Storage: Azure Virtual Machine 워크로드를 위한 고성능 저장소](../../../storage/common/storage-premium-storage.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19163-292">For more information, see [Premium Storage: High-performance storage for Azure Virtual Machine workloads](../../../storage/common/storage-premium-storage.md).</span></span>

<span data-ttu-id="19163-293">VM 만들기를 위한 샘플 JSON 템플릿을 찾으려면 [Azure 빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-293">To find sample JSON templates for creating VMs, go to [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
<span data-ttu-id="19163-294">vm-simple-sles 템플릿은 기본 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="19163-294">The vm-simple-sles template is a basic template.</span></span> <span data-ttu-id="19163-295">여기에는 100GB 추가 데이터 디스크가 포함된 저장소 섹션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-295">It includes a storage section, with an additional 100-GB data disk.</span></span> <span data-ttu-id="19163-296">이 템플릿을 기반으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-296">This template can be used as a base.</span></span> <span data-ttu-id="19163-297">특정 구성에 맞게 템플릿을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-297">You can adapt the template to your specific configuration.</span></span>

>[!Note]
><span data-ttu-id="19163-298">[Microsoft Azure SUSE Linux VM에서 SAP NetWeaver 실행](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 설명한 대로 UUID를 사용하여 Azure 저장소 디스크를 연결하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-298">It is important to attach the Azure storage disk by using a UUID as documented in [Running SAP NetWeaver on Microsoft Azure SUSE Linux VMs](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="19163-299">테스트 환경에서 다음 스크린샷과 같이 2개 Azure 표준 저장소 디스크가 SAP 앱 서버 VM에 연결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-299">In the test environment, two Azure standard storage disks were attached to the SAP app server VM, as shown in the following screenshot.</span></span> <span data-ttu-id="19163-300">한 디스크에서는 설치를 위한 모든 SAP 소프트웨어(NetWeaver 7.5, SAP GUI 및 SAP HANA 포함)를 저장했습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-300">One disk stored all the SAP software (including NetWeaver 7.5, SAP GUI, and SAP HANA) for installation.</span></span> <span data-ttu-id="19163-301">다른 한 디스크에서는 추가 요구 사항(예: 백업 및 테스트 데이터)에 대비하여 충분한 여유 공간을 확보하고, 동일한 SAP 환경에 속한 모든 VM 간에 /sapmnt 디렉터리(즉 SAP 프로필)를 공유할 수 있도록 했습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-301">The second disk ensured that enough free space would be available for additional requirements (for example, backup and test data) and for the /sapmnt directory (that is, SAP profiles) to be shared among all VMs that belong to the same SAP landscape.</span></span>

![2개 데이터 디스크 및 해당 크기를 보여 주는 SAP HANA 앱 서버 디스크 창](./media/hana-get-started/image003.jpg)


### <a name="kernel-parameters"></a><span data-ttu-id="19163-303">커널 매개 변수</span><span class="sxs-lookup"><span data-stu-id="19163-303">Kernel parameters</span></span>
<span data-ttu-id="19163-304">SAP HANA에는 표준 Azure 갤러리 이미지의 일부가 아닌 특정 Linux 커널 설정이 필요하며, 수동으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-304">SAP HANA requires specific Linux kernel settings, which are not part of the standard Azure gallery images and must be set manually.</span></span> <span data-ttu-id="19163-305">SUSE 또는 Red Hat의 사용 여부에 따라 매개 변수가 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-305">Depending on whether you use SUSE or Red Hat, the parameters might be different.</span></span> <span data-ttu-id="19163-306">앞에서 나열한 SAP Note에서 이러한 매개 변수에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-306">The SAP Notes listed earlier give information about those parameters.</span></span> <span data-ttu-id="19163-307">표시된 스크린샷에서 SUSE Linux 12 SP1이 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-307">In the screenshots shown, SUSE Linux 12 SP1 was used.</span></span> 

<span data-ttu-id="19163-308">SLES for SAP Applications 12 GA 및 SLES for SAP Applications 12 SP1에는 이전 **sapconf** 유틸리티를 대체하는 새로운 **tuned-adm** 도구가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-308">SLES for SAP Applications 12 GA and SLES for SAP Applications 12 SP1 have a new tool, **tuned-adm**, that replaces the old **sapconf** tool.</span></span> <span data-ttu-id="19163-309">**tuned-adm**에 대한 특별한 SAP HANA 프로필을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-309">A special SAP HANA profile is available for **tuned-adm**.</span></span> <span data-ttu-id="19163-310">SAP HANA에 맞게 시스템을 튜닝하려면 루트 사용자로서 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-310">To tune the system for SAP HANA, enter the following as a root user:</span></span>

   `tuned-adm profile sap-hana`

<span data-ttu-id="19163-311">**tuned-adm**에 대한 자세한 내용은 [tuned-adm 관련 SUSE 설명서](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19163-311">For more information about **tuned-adm**, see the [SUSE documentation about tuned-adm](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip).</span></span>

<span data-ttu-id="19163-312">다음 스크린샷에서는 필요한 SAP HANA 설정에 따라 **tuned-adm**에서 `transparent_hugepage` 및 `numa_balancing` 값을 변경한 방식을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-312">In the following screenshot, you can see how **tuned-adm** changed the `transparent_hugepage` and `numa_balancing` values, according to the required SAP HANA settings.</span></span>

![tuned-adm 도구는 필수 SAP HANA 설정에 따라 값을 변경합니다.](./media/hana-get-started/image005.jpg)

<span data-ttu-id="19163-314">SAP HANA 커널을 영구적으로 설정하려면 SLES 12에서 **grub2**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-314">To make the SAP HANA kernel settings permanent, use **grub2** on SLES 12.</span></span> <span data-ttu-id="19163-315">**grub2**에 대한 자세한 내용은 SUSE 설명서의 [구성 파일 구조](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip)(영문) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19163-315">For more information about **grub2**, go to the [Configuration File Structure](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip) section of the SUSE documentation.</span></span>

<span data-ttu-id="19163-316">다음 스크린샷에서는 구성 파일에서 커널 설정을 변경한 다음 **grub2-mkconfig**를 사용하여 컴파일한 방식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="19163-316">The following screenshot shows how the kernel settings were changed in the configuration file and then compiled by using **grub2-mkconfig**:</span></span>

![구성 파일에서 변경된 커널 설정 및 grub2-mkconfig를 통한 컴파일](./media/hana-get-started/image006.jpg)

<span data-ttu-id="19163-318">또 다른 옵션은 YaST 및 **부팅 로더** > **커널 매개 변수** 설정을 사용하여 커널 설정을 변경하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="19163-318">Another option is to change the settings by using YaST and the **Boot Loader** > **Kernel Parameters** settings:</span></span>

![YaST 부팅 로더의 커널 매개 변수 설정 탭](./media/hana-get-started/image007.jpg)

### <a name="file-systems"></a><span data-ttu-id="19163-320">파일 시스템</span><span class="sxs-lookup"><span data-stu-id="19163-320">File systems</span></span>
<span data-ttu-id="19163-321">다음 스크린샷에서는 2개 Azure 표준 저장소 디스크에 연결된 SAP 앱 서버 VM에 만들어진 2개 파일 시스템을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="19163-321">The following screenshot shows two file systems that were created on the SAP app server VM on top of the two attached Azure standard storage disks.</span></span> <span data-ttu-id="19163-322">두 파일 시스템은 모두 XFS 형식이며 /sapdata 및 /sapsoftware에 탑재됩니다.</span><span class="sxs-lookup"><span data-stu-id="19163-322">Both file systems are of type XFS and are mounted to /sapdata and /sapsoftware.</span></span>

<span data-ttu-id="19163-323">파일 시스템을 반드시 이 방식으로 구조화하는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="19163-323">It is not mandatory to structure your file systems in this way.</span></span> <span data-ttu-id="19163-324">디스크 공간을 구조화하기 위한 다른 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-324">You have other options for structuring the disk space.</span></span> <span data-ttu-id="19163-325">가장 중요한 고려 사항은 루트 파일 시스템의 여유 공간이 부족하지 않도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="19163-325">The most important consideration is to prevent the root file system from running out of free space.</span></span>

![SAP 앱 서버 VM에 만든 2개 파일 시스템](./media/hana-get-started/image008.jpg)

<span data-ttu-id="19163-327">SAP HANA DB VM과 관련하여 데이터베이스 설치 중에 SAPinst(SWPM) 및 **일반** 설치 옵션을 사용하면 모든 항목이 /hana 및 /usr/sap 아래에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="19163-327">Regarding the SAP HANA DB VM, during a database installation, when you use SAPinst (SWPM) and the **typical** installation option, everything is installed under /hana and /usr/sap.</span></span> <span data-ttu-id="19163-328">SAP HANA 로그 백업의 기본 위치는 /usr/sap 아래입니다.</span><span class="sxs-lookup"><span data-stu-id="19163-328">The default location for the SAP HANA log backup is under /usr/sap.</span></span> <span data-ttu-id="19163-329">즉 루트 파일 시스템의 저장소 공간이 부족하지 않도록 하는 것이 중요하기 때문에 SWPM을 사용하여 SAP HANA를 설치하기 전에 /hana 및 /usr/sap 아래에 충분한 여유 공간이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-329">Again, because it's important to prevent the root file system from running out of storage space, make sure that there is enough free space under /hana and /usr/sap before you install SAP HANA by using SWPM.</span></span>

<span data-ttu-id="19163-330">SAP HANA의 표준 파일 시스템 레이아웃에 대한 설명은 [SAP HANA 서버 설치 및 업데이트 가이드](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19163-330">For a description of the standard file-system layout of SAP HANA, see the [SAP HANA Server Installation and Update Guide](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm).</span></span>

![SAP 앱 서버 VM에 만든 추가 파일 시스템](./media/hana-get-started/image009.jpg)

<span data-ttu-id="19163-332">표준 SLES/SLES for SAP Applications 12에 SAP NetWeaver를 설치하면 다음 스크린샷과 같이 스왑 공간이 없다는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="19163-332">When you install SAP NetWeaver on a standard SLES/SLES for SAP Applications 12 Azure gallery image, a message is displayed that says  there is no swap space, as shown in the following screenshot.</span></span> <span data-ttu-id="19163-333">이 메시지를 해제하려면 **dd**, **mkswap** 및 **swapon**을 사용하여 스왑 파일을 수동으로 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19163-333">To dismiss this message, you can manually add a swap file by using **dd**, **mkswap**, and **swapon**.</span></span> <span data-ttu-id="19163-334">자세한 내용은 SUSE 설명서의 [YaST Partitioner 사용](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip)(영문) 섹션에서 "수동으로 스왑 파일 추가"를 검색해 보세요.</span><span class="sxs-lookup"><span data-stu-id="19163-334">To learn how, search for "Adding a swap file manually" in the [Using the YaST Partitioner](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip) section of the SUSE documentation.</span></span>

<span data-ttu-id="19163-335">또 다른 옵션은 Linux VM 에이전트를 사용하여 교환 공간을 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="19163-335">Another option is to configure swap space by using the Linux VM agent.</span></span> <span data-ttu-id="19163-336">자세한 내용은 [Azure Linux 에이전트 사용자 가이드](../../linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19163-336">For more information, see the [Azure Linux Agent User Guide](../../linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

![교환 공간이 부족하다고 알리는 팝업 메시지](./media/hana-get-started/image010.jpg)


### <a name="the-etchosts-file"></a><span data-ttu-id="19163-338">/etc/hosts 파일</span><span class="sxs-lookup"><span data-stu-id="19163-338">The /etc/hosts file</span></span>
<span data-ttu-id="19163-339">SAP 설치를 시작하기 전에 먼저 SAP VM의 호스트 이름과 IP 주소를 /etc/hosts 파일에 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-339">Before you start to install SAP, make sure you include the host names and IP addresses of the SAP VMs in the /etc/hosts file.</span></span> <span data-ttu-id="19163-340">하나의 Azure 가상 네트워크 내에 모든 SAP VM을 배포한 다음 아래와 같은 내부 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-340">Deploy all the SAP VMs within one Azure virtual network, and then use the internal IP addresses, as shown here:</span></span>

![/etc/hosts 파일에 나열된 SAP VM의 호스트 이름 및 IP 주소](./media/hana-get-started/image011.jpg)

### <a name="the-etcfstab-file"></a><span data-ttu-id="19163-342">/etc/fstab 파일</span><span class="sxs-lookup"><span data-stu-id="19163-342">The /etc/fstab file</span></span>

<span data-ttu-id="19163-343">fstab 파일에 **nofail** 매개 변수를 추가하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-343">It is helpful to add the **nofail** parameter to the fstab file.</span></span> <span data-ttu-id="19163-344">이렇게 하면 디스크에 오류가 발생하더라도 VM이 부팅 프로세스에서 중단되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-344">This way, if something goes wrong with the disks, the VM does not hang in the boot process.</span></span> <span data-ttu-id="19163-345">그러나 추가 디스크 공간을 사용할 수 없으며 프로세스가 루트 파일 시스템을 가득 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-345">But remember that additional disk space might not be available, and processes might fill up the root file system.</span></span> <span data-ttu-id="19163-346">/hana가 누락되면 SAP HANA가 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-346">If /hana is missing, SAP HANA won't start.</span></span>

![fstab 파일에 nofail 매개 변수 추가](./media/hana-get-started/image000c.jpg)

## <a name="graphical-gnome-desktop-on-sles-12sles-for-sap-applications-12"></a><span data-ttu-id="19163-348">SLES 12/SLES for SAP Applications 12의 그래픽 GNOME 데스크톱</span><span class="sxs-lookup"><span data-stu-id="19163-348">Graphical GNOME desktop on SLES 12/SLES for SAP Applications 12</span></span>
<span data-ttu-id="19163-349">이 섹션에서는 다음 항목을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="19163-349">This section covers the following topics:</span></span>

* <span data-ttu-id="19163-350">SLES 12/SLES-for-SAP 응용 프로그램 12에 GNOME 데스크톱 및 xrdp 설치</span><span class="sxs-lookup"><span data-stu-id="19163-350">Installing the GNOME desktop and xrdp on SLES 12/SLES for SAP Applications 12</span></span>
* <span data-ttu-id="19163-351">SLES 12/SLES for SAP Applications 12에서 Firefox를 사용하여 Java 기반 SAP MC 실행</span><span class="sxs-lookup"><span data-stu-id="19163-351">Running Java-based SAP MC by using Firefox on SLES 12/SLES for SAP Applications 12</span></span>

<span data-ttu-id="19163-352">Xterminal 또는 VNC와 같은 대안을 사용할 수도 있습니다(여기서는 설명하지 않음).</span><span class="sxs-lookup"><span data-stu-id="19163-352">You can also use alternatives such as Xterminal or VNC (not described in this guide).</span></span>

### <a name="installing-the-gnome-desktop-and-xrdp-on-sles-12sles-for-sap-applications-12"></a><span data-ttu-id="19163-353">SLES 12/SLES-for-SAP 응용 프로그램 12에 GNOME 데스크톱 및 xrdp 설치</span><span class="sxs-lookup"><span data-stu-id="19163-353">Installing the GNOME desktop and xrdp on SLES 12/SLES for SAP Applications 12</span></span>
<span data-ttu-id="19163-354">Windows 백그라운드에 있으면 SAP Linux VM 내에서 그래픽 데스크톱을 직접 사용하여, Firefox, SAPinst, SAP GUI, SAP MC 또는 HANA Studio를 실행하고, Windows 컴퓨터에서 RDP(원격 데스크톱 프로토콜)를 통해 VM에 연결할 수 있습니다 .</span><span class="sxs-lookup"><span data-stu-id="19163-354">If you have a Windows background, you can easily use a graphical desktop directly within the SAP Linux VMs to run Firefox, SAPinst, SAP GUI, SAP MC, or HANA Studio, and connect to the VM through the Remote Desktop Protocol (RDP) from a Windows computer.</span></span> <span data-ttu-id="19163-355">프로덕션 및 비프로덕션 Linux 기반 시스템에 그래픽 사용자 인터페이스를 추가하는 것과 관련된 회사 정책에 따라 서버에 GNOME을 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-355">Dependent on your company policies about adding graphical user interfaces to production and non-production Linux based systems, you might want to install GNOME on your server.</span></span> <span data-ttu-id="19163-356">Azure SLES 12/SLES for SAP Applications 12 VM에 GNOME 데스크톱을 설치하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-356">To install the GNOME desktop on an Azure SLES 12/SLES for SAP Applications 12 VM:</span></span>

1. <span data-ttu-id="19163-357">다음 명령을 입력하여 GNOME 데스크톱을 설치합니다(예: PuTTY 창에서).</span><span class="sxs-lookup"><span data-stu-id="19163-357">Install the GNOME desktop by entering the following command (for example, in a PuTTY window):</span></span>

   `zypper in -t pattern gnome-basic`

2. <span data-ttu-id="19163-358">xrdp를 설치하여 RDP를 통해 VM에 연결할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-358">Install xrdp to allow a connection to the VM through RDP:</span></span>

   `zypper in xrdp`

3. <span data-ttu-id="19163-359">/etc/sysconfig/windowmanager를 편집하고 기본 창 관리자를 GNOME으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-359">Edit /etc/sysconfig/windowmanager, and set the default window manager to GNOME:</span></span>

   `DEFAULT_WM="gnome"`

4. <span data-ttu-id="19163-360">**chkconfig**를 실행하여 다시 부팅한 후 xrdp가 자동으로 시작되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-360">Run **chkconfig** to make sure that xrdp starts automatically after a reboot:</span></span>

   `chkconfig -level 3 xrdp on`

5. <span data-ttu-id="19163-361">RDP 연결에 문제가 있으면 다시 시작합니다(예: PuTTY 창에서).</span><span class="sxs-lookup"><span data-stu-id="19163-361">If you have an issue with the RDP connection, try to restart (from a PuTTY window, for example):</span></span>

   `/etc/xrdp/xrdp.sh restart`

6. <span data-ttu-id="19163-362">이전 단계에서 언급한 xrdp 다시 시작이 작동하지 않으면 .pid 파일을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-362">If an xrdp restart mentioned in the previous step doesn't work, check for a .pid file:</span></span>

   `check /var/run` 

   <span data-ttu-id="19163-363">`xrdp.pid`를 찾아보세요.</span><span class="sxs-lookup"><span data-stu-id="19163-363">Look for `xrdp.pid`.</span></span> <span data-ttu-id="19163-364">찾은 다음 제거하고 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-364">If you find it, remove it, and try to restart again.</span></span>

### <a name="starting-sap-mc"></a><span data-ttu-id="19163-365">SAP MC 시작</span><span class="sxs-lookup"><span data-stu-id="19163-365">Starting SAP MC</span></span>
<span data-ttu-id="19163-366">GNOME 데스크톱을 설치한 후 Azure SLES 12/SLES for SAP Applications 12 VM에서 실행되는 Firefox에서 그래픽 Java 기반 SAP MC를 시작하면 누락된 Java 브라우저 플러그 인으로 인해 오류가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-366">After you install the GNOME desktop, starting the graphical Java-based SAP MC from Firefox while running in an Azure SLES 12/SLES for SAP Applications 12 VM might display an error because of the missing Java-browser plug-in.</span></span>

<span data-ttu-id="19163-367">SAP MC를 시작할 URL은 `<server>:5<instance_number>13`입니다.</span><span class="sxs-lookup"><span data-stu-id="19163-367">The URL to start the SAP MC is `<server>:5<instance_number>13`.</span></span>

<span data-ttu-id="19163-368">자세한 내용은 [웹 기반 SAP 관리 콘솔 시작](https://help.sap.com/saphelp_nwce10/helpdata/en/48/6b7c6178dc4f93e10000000a42189d/frameset.htm)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19163-368">For more information, see [Starting the Web-Based SAP Management Console](https://help.sap.com/saphelp_nwce10/helpdata/en/48/6b7c6178dc4f93e10000000a42189d/frameset.htm).</span></span>

<span data-ttu-id="19163-369">다음 스크린샷에서는 Java 브라우저 플러그 인이 없는 경우 표시되는 오류 메시지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="19163-369">The following screenshot shows the error message that is displayed when the Java-browser plug-in is missing:</span></span>

![누락된 Java 브라우저 플러그 인을 나타내는 오류 메시지](./media/hana-get-started/image013.jpg)

<span data-ttu-id="19163-371">이 문제를 해결하는 한 가지 방법은 다음 스크린샷과 같이 YaST를 사용하여 누락된 플러그 인을 설치하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="19163-371">One way to solve the problem is to install the missing plug-in by using YaST, as shown in the following screenshot:</span></span>

![YaST를 사용하여 누락된 플러그 인 설치](./media/hana-get-started/image014.jpg)

<span data-ttu-id="19163-373">SAP 관리 콘솔 URL을 다시 입력하면 플러그 인을 활성화하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="19163-373">When you re-enter the SAP Management Console URL, a message appears asking you to activate the plug-in:</span></span>

![플러그 인 활성화를 요청하는 대화 상자](./media/hana-get-started/image015.jpg)

<span data-ttu-id="19163-375">누락된 javafx.properties 파일에 대한 오류 메시지가 표시될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-375">You might also receive an error message about a missing file, javafx.properties.</span></span> <span data-ttu-id="19163-376">이 항목은 SAP GUI 7.4용 Oracle Java 1.8의 요구 사항과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-376">This is related to the requirement of Oracle Java 1.8 for SAP GUI 7.4.</span></span> <span data-ttu-id="19163-377">([SAP Note 2059429](https://launchpad.support.sap.com/#/notes/2059424) 참조) SLES/SLES for SAP Applications 12와 함께 제공되는 IBM Java 버전 또는 openjdk 패키지에는 필요한 javafx.propertie파일이 포함되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-377">(See [SAP Note 2059429](https://launchpad.support.sap.com/#/notes/2059424).) Neither the IBM Java version nor the openjdk package delivered with SLES/SLES for SAP Applications 12 includes the needed javafx.properties file.</span></span> <span data-ttu-id="19163-378">따라서 Oracle에서 Java SE 8를 다운로드하고 설치하여 이 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-378">The solution is to download and install Java SE 8 from Oracle.</span></span>

<span data-ttu-id="19163-379">openSUSE에서 openjdk와 비슷한 문제에 대한 내용은 [SAPGui 7.4 Java for openSUSE 42.1 Leap](https://scn.sap.com/thread/3908306)(영문) 토론 스레드를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19163-379">For information about a similar issue with openjdk on openSUSE, see the discussion thread [SAPGui 7.4 Java for openSUSE 42.1 Leap](https://scn.sap.com/thread/3908306).</span></span>

## <a name="manual-installation-of-sap-hana-swpm"></a><span data-ttu-id="19163-380">SAP HANA 수동 설치: SWPM</span><span class="sxs-lookup"><span data-stu-id="19163-380">Manual installation of SAP HANA: SWPM</span></span>
<span data-ttu-id="19163-381">이 섹션에서 보여 주는 일련의 스크린샷은 SWPM(SAPinst)을 사용할 때 SAP NetWeaver 7.5 및 SAP HANA SP12를 설치하기 위한 주요 단계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="19163-381">The series of screenshots in this section shows the key steps for installing SAP NetWeaver 7.5 and SAP HANA SP12 when you use SWPM (SAPinst).</span></span> <span data-ttu-id="19163-382">NetWeaver 7.5 설치의 일부로 SWPM은 HANA 데이터베이스를 단일 인스턴스로 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-382">As part of a NetWeaver 7.5 installation, SWPM can also install the HANA database as a single instance.</span></span>

<span data-ttu-id="19163-383">샘플 테스트 환경에서는 ABAP(Advanced Business Application Programming) 앱 서버 하나만 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-383">In a sample test environment, we installed just one Advanced Business Application Programming (ABAP) app server.</span></span> <span data-ttu-id="19163-384">다음 스크린샷에서는 **분산 시스템** 옵션을 사용하여 하나의 Azure VM에는 ASCS 및 기본 응용 프로그램 서버 인스턴스를, 다른 하나의 Azure VM에는 데이터베이스 시스템으로 SAP HANA를 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-384">As shown in the following screenshot, we used the **Distributed System** option to install the ASCS and primary application server instances in one Azure VM and SAP HANA as the database system in another Azure VM.</span></span>

![[분산 시스템] 옵션으로 설치된 ASCS 및 기본 응용 프로그램 서버 인스턴스](./media/hana-get-started/image012.jpg)

<span data-ttu-id="19163-386">ASCS 인스턴스를 앱 서버 VM에 설치하고 SAP 관리 콘솔에서 "녹색"으로 설정한 후에는 SAP 프로필 디렉터리를 포함한 /sapmnt 디렉터리를 SAP HANA DB 서버 VM과 공유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-386">After the ASCS instance is installed on the app server VM and is set to "green" in the SAP Management Console (shown in the following screenshot), the /sapmnt directory (including the SAP profile directory) must be shared with the SAP HANA DB server VM.</span></span> <span data-ttu-id="19163-387">DB 설치 단계에서 이 정보에 액세스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-387">The DB installation step needs access to this information.</span></span> <span data-ttu-id="19163-388">액세스를 제공하는 가장 좋은 방법은 YaST를 사용하여 구성할 수 있는 NFS를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="19163-388">The best way to provide access is to use NFS, which can be configured by using YaST.</span></span>

![앱 서버 VM에 설치하되 "녹색"으로 설정된 ASCS 인스턴스를 보여 주는 SAP 관리 콘솔](./media/hana-get-started/image016.jpg)

<span data-ttu-id="19163-390">앱 서버 VM에서 /sapmnt 디렉터리는 **rw** 및 **no_root_squash** 옵션을 사용하여 NFS를 통해 공유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-390">On the app server VM, the /sapmnt directory should be shared via NFS by using the **rw** and **no_root_squash** options.</span></span> <span data-ttu-id="19163-391">기본값은 **ro** 및 **root_squash**이며, 데이터베이스 인스턴스를 설치할 때 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-391">The defaults are **ro** and **root_squash**, which might lead to problems when you install the database instance.</span></span>

!["rw" 및 "no_root_squash" 옵션을 사용하여 NFS를 통해 /sapmnt 디렉터리 공유](./media/hana-get-started/image017b.jpg)

<span data-ttu-id="19163-393">다음 스크린샷과 같이 **NFS 클라이언트**(및 YaST)를 사용하여 SAP HANA DB 서버 VM에 앱 서버 VM의 /sapmnt 공유를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-393">As the next screenshot shows, the /sapmnt share from the app server VM must be configured on the SAP HANA DB server VM by using **NFS Client** (and YaST).</span></span>

![NFS 클라이언트를 사용하여 구성된 /sapmnt 공유](./media/hana-get-started/image018b.jpg)

<span data-ttu-id="19163-395">다음 스크린샷과 같이 분산형 NetWeaver 7.5 설치(**데이터베이스 인스턴스**)를 수행하려면 SAP HANA DB 서버 VM에 로그인하고 SWPM을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-395">To perform a distributed NetWeaver 7.5 installation (**Database Instance**), as shown in the following screenshot, sign in to the SAP HANA DB server VM and start SWPM.</span></span>

![SAP HANA DB 서버 VM에 로그인하고 SWPM을 시작하여 데이터베이스 인스턴스 설치](./media/hana-get-started/image019.jpg)

<span data-ttu-id="19163-397">**일반** 설치 및 설치 미디어 경로를 선택한 다음 DB SID, 호스트 이름, 인스턴스 번호 및 DB 시스템 관리자 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-397">After you select **typical** installation and the path to the installation media, enter a DB SID, the host name, the instance number, and the DB system administrator password.</span></span>

![SAP HANA 데이터베이스 시스템 관리자 로그인 페이지](./media/hana-get-started/image035b.jpg)

<span data-ttu-id="19163-399">DBACOCKPIT 스키마의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-399">Enter the password for the DBACOCKPIT schema:</span></span>

![DBACOCKPIT 스키마의 암호 입력 상자](./media/hana-get-started/image036b.jpg)

<span data-ttu-id="19163-401">SAPABAP1 스키마 암호에 대한 질문을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-401">Enter a question for the SAPABAP1 schema password:</span></span>

![SAPABAP1 스키마 암호에 대한 질문 입력](./media/hana-get-started/image037b.jpg)

<span data-ttu-id="19163-403">각 작업이 완료되면 DB 설치 프로세스의 각 단계 옆에 녹색 확인 표시가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="19163-403">After each task is completed, a green check mark is displayed next to each phase of the DB installation process.</span></span> <span data-ttu-id="19163-404">메시지 "데이터베이스... 인스턴스의 실행이 완료되었습니다."가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="19163-404">The message "Execution of ... Database Instance has completed" is displayed.</span></span>

![확인 메시지가 표시된 작업 완료 창](./media/hana-get-started/image023.jpg)

<span data-ttu-id="19163-406">성공적으로 설치되면 SAP 관리 콘솔에서 DB 인스턴스를 "녹색"으로 표시하고, SAP HANA 프로세스의 전체 목록(hdbindexserver, hdbcompileserver 등)도 표시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-406">After successful installation, the SAP Management Console should also show the DB instance as "green" and display the full list of SAP HANA processes (hdbindexserver, hdbcompileserver, and so forth).</span></span>

![SAP HANA 프로세스 목록을 보여 주는 SAP 관리 콘솔 창](./media/hana-get-started/image024.jpg)

<span data-ttu-id="19163-408">다음 스크린샷에서는 HANA 설치 중에 SWPM에서 만든 /hana/shared 디렉터리 아래의 파일 구조 일부를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="19163-408">The following screenshot shows the parts of the file structure under the /hana/shared directory that SWPM created during the HANA installation.</span></span> <span data-ttu-id="19163-409">다른 경로를 지정하는 옵션이 없으므로 SWPM을 사용하여 SAP HANA를 설치하기 전에 먼저 /hana 디렉터리 아래에 추가 디스크 공간을 탑재해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-409">Because there is no option to specify a different path, it's important to mount additional disk space under the /hana directory before the SAP HANA installation by using SWPM.</span></span> <span data-ttu-id="19163-410">이렇게 하면 루트 파일 시스템의 여유 공간이 부족하지 않도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-410">This prevents the root file system from running out of free space.</span></span>

![HANA 설치 중에 만든 /hana/shared 디렉터리 파일 구조](./media/hana-get-started/image025.jpg)

<span data-ttu-id="19163-412">다음 스크린샷에서는 /usr/sap 디렉터리의 파일 구조를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="19163-412">This screenshot shows the file structure of the /usr/sap directory:</span></span>

![/usr/sap 디렉터리 파일 구조](./media/hana-get-started/image026.jpg)

<span data-ttu-id="19163-414">분산형 ABAP 설치의 마지막 단계는 기본 응용 프로그램 서버 인스턴스를 설치하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="19163-414">The last step of the distributed ABAP installation is to install the primary application server instance:</span></span>

![마지막 단계로 기본 응용 프로그램 서버 인스턴스를 보여 주는 ABAP 설치](./media/hana-get-started/image027b.jpg)

<span data-ttu-id="19163-416">기본 응용 프로그램 서버 인스턴스 및 SAP GUI를 설치한 후에는 **DBA Cockpit** 트랜잭션을 사용하여 SAP HANA 설치가 올바르게 완료되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-416">After the primary application server instance and SAP GUI are installed, use the **DBA Cockpit** transaction to confirm that the SAP HANA installation has finished correctly:</span></span>

![성공적인 설치를 확인하는 DBA Cockpit 창](./media/hana-get-started/image028b.jpg)

<span data-ttu-id="19163-418">마지막 단계로 HANA Studio를 SAP 앱 서버 VM에 설치한 다음 DB 서버 VM에서 실행 중인 SAP HANA 인스턴스에 연결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-418">As a final step, you might want to first install HANA Studio in the SAP app server VM, and then connect to the SAP HANA instance that's running on the DB server VM:</span></span>

![SAP 앱 서버 VM에 SAP HANA Studio 설치](./media/hana-get-started/image038b.jpg)

## <a name="manual-installation-of-sap-hana-hdblcm"></a><span data-ttu-id="19163-420">SAP HANA 수동 설치: HDBLCM</span><span class="sxs-lookup"><span data-stu-id="19163-420">Manual installation of SAP HANA: HDBLCM</span></span>
<span data-ttu-id="19163-421">SWPM을 사용하여 분산 설치의 일부로 SAP HANA를 설치하는 것 외에도 먼저 HDBLCM을 사용하여 독립 실행형 HANA를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-421">In addition to installing SAP HANA as part of a distributed installation by using SWPM, you can install the HANA standalone first, by using HDBLCM.</span></span> <span data-ttu-id="19163-422">예를 들어 SAP NetWeaver 7.5를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-422">You can then install SAP NetWeaver 7.5, for example.</span></span> <span data-ttu-id="19163-423">이 섹션의 스크린샷에서는 이 프로세스가 작동하는 방식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="19163-423">The screenshots in this section show how this process works.</span></span>

<span data-ttu-id="19163-424">HANA HDBLCM 도구에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19163-424">For more information about the HANA HDBLCM tool, see:</span></span>

* [<span data-ttu-id="19163-425">Choosing the Correct SAP HANA HDBLCM for Your Task(작업을 위해 올바른 SAP HANA HDBLCM 선택)</span><span class="sxs-lookup"><span data-stu-id="19163-425">Choosing the Correct SAP HANA HDBLCM for Your Task</span></span>](https://help.sap.com/saphelp_hanaplatform/helpdata/en/68/5cff570bb745d48c0ab6d50123ca60/content.htm)
* [<span data-ttu-id="19163-426">SAP HANA Lifecycle Management Tools(SAP HANA 수명 주기 관리 도구)</span><span class="sxs-lookup"><span data-stu-id="19163-426">SAP HANA Lifecycle Management Tools</span></span>](http://saphanatutorial.com/sap-hana-lifecycle-management-tools/)
* [<span data-ttu-id="19163-427">SAP HANA Server Installation and Update Guide(SAP HANA 서버 설치 및 업데이트 가이드)</span><span class="sxs-lookup"><span data-stu-id="19163-427">SAP HANA Server Installation and Update Guide</span></span>](http://help.sap.com/hana/SAP_HANA_Server_Installation_Guide_en.pdf)

<span data-ttu-id="19163-428">HDBLCM 도구로 만든 `\<HANA SID\>adm user`에 대한 기본 그룹 ID 설정에 문제가 발생하지 않도록 HDBLCM을 통해 SAP HANA를 설치하기 전에 `1001` 그룹 ID를 사용하여 `sapsys`라는 새 그룹을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-428">To avoid problems with a default group ID setting for the `\<HANA SID\>adm user` (created by the HDBLCM tool), define a new group called `sapsys` by using group ID `1001` before you install SAP HANA via HDBLCM:</span></span>

![1001 그룹 ID를 사용하여 정의한 새로운 "sapsys" 그룹](./media/hana-get-started/image030.jpg)

<span data-ttu-id="19163-430">HDBLCM을 처음으로 시작하면 간단한 시작 메뉴가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="19163-430">When you start HDBLCM the first time, a simple start menu is displayed.</span></span> <span data-ttu-id="19163-431">다음 스크린샷과 같이 항목 1 **새 시스템 설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-431">Select item 1, **Install new system**, as shown in the following screenshot:</span></span>

![HDBLCM 시작 창의 "새 시스템 설치" 옵션](./media/hana-get-started/image031.jpg)

<span data-ttu-id="19163-433">다음 스크린샷에서는 이전에 선택한 주요 옵션을 모두 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="19163-433">The following screenshot displays all the key options that you selected previously.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="19163-434">HANA 로그 및 데이터 볼륨뿐만 아니라 설치 경로(이 샘플의 경우 /hana/shared) 및 /usr/sap의 이름이 지정된 디렉터리는 루트 파일 시스템의 일부가 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-434">Directories that are named for HANA log and data volumes, as well as the installation path (/hana/shared in this sample) and /usr/sap, should not be part of the root file system.</span></span> <span data-ttu-id="19163-435">이러한 디렉터리는 "디스크 설정" 섹션에서 설명한 대로 VM에 연결된 Azure 데이터 디스크에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-435">These directories belong to the Azure data disks that were attached to the VM (described in the "Disk setup" section).</span></span> <span data-ttu-id="19163-436">이 방법은 루트 파일 시스템의 공간이 부족하지 않도록 방지하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-436">This approach helps prevent the root file system from running out of space.</span></span> <span data-ttu-id="19163-437">다음 스크린샷에서 HANA 시스템 관리자는 사용자 ID가 `1005`이고 설치하기 전에 정의한 `sapsys` 그룹(ID `1001`)에 속해 있음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-437">In the following screenshot, you can see that the HANA system administrator has user ID `1005` and is part of the `sapsys` group (ID `1001`) that was defined before the installation.</span></span>

![이전에 선택한 주요 SAP HANA 구성 요소 전체 목록](./media/hana-get-started/image032.jpg)

<span data-ttu-id="19163-439">/etc/passwd 디렉터리에서 `\<HANA SID\>adm user`(다음 스크린샷의 `azdadm`) 세부 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-439">You can check the `\<HANA SID\>adm user` (`azdadm` in the following screenshot) details in the /etc/passwd directory:</span></span>

![/etc/passwd 디렉터리에 나열된 HANA \<HANA SID\>adm 사용자 세부 정보](./media/hana-get-started/image033.jpg)

<span data-ttu-id="19163-441">HDBLCM을 사용하여 SAP HANA를 설치하면 다음 스크린샷과 같이 SAP HANA Studio에서 파일 구조를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-441">After you install SAP HANA by using HDBLCM, you can see the file structure in SAP HANA Studio, as shown in the following screenshot.</span></span> <span data-ttu-id="19163-442">모든 SAP NetWeaver 테이블을 포함하는 SAPABAP1 스키마는 아직 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-442">The SAPABAP1 schema, which includes all the SAP NetWeaver tables, isn't available yet.</span></span>

![SAP HANA Studio의 SAP HANA 파일 구조](./media/hana-get-started/image034.jpg)

<span data-ttu-id="19163-444">SAP HANA를 설치한 후에는 이를 기반으로 하여 SAP NetWeaver를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-444">After you install SAP HANA, you can install SAP NetWeaver on top of it.</span></span> <span data-ttu-id="19163-445">다음 스크린샷과 같이 이전 섹션에서 설명한 대로 SWPM을 사용하여 "분산 설치"로 수행되었습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-445">As shown in the following screenshot, the installation was performed as a distributed installation by using SWPM (as described in the previous section).</span></span> <span data-ttu-id="19163-446">SWPM을 사용하여 데이터베이스 인스턴스를 설치하는 경우 HDBLCM을 사용하여 동일한 데이터(예: 호스트 이름, HANA SID 및 인스턴스 번호)를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-446">When you install the database instance by using SWPM, you enter the same data by using HDBLCM (for example, host name, HANA SID, and instance number).</span></span> <span data-ttu-id="19163-447">그러면 SWPM에서 기존 HANA 설치를 사용하고 더 많은 스키마를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-447">SWPM then uses the existing HANA installation and adds more schemas.</span></span>

![SWPM을 사용하여 수행한 분산 설치](./media/hana-get-started/image035b.jpg)

<span data-ttu-id="19163-449">다음 스크린샷에서는 DBACOCKPIT 스키마에 대한 데이터를 입력하는 SWPM 설치 단계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="19163-449">The following screenshot shows the SWPM installation step where you enter data about the DBACOCKPIT schema:</span></span>

![DBACOCKPIT 스키마 데이터를 입력하는 SWPM 설치 단계](./media/hana-get-started/image036b.jpg)

<span data-ttu-id="19163-451">SAPABAP1 스키마에 대한 데이터를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="19163-451">Enter data about the SAPABAP1 schema:</span></span>

![SAPABAP1 스키마에 대한 데이터 입력](./media/hana-get-started/image037b.jpg)

<span data-ttu-id="19163-453">SWPM 데이터베이스 인스턴스 설치가 완료되면 SAP HANA Studio에서 SAPABAP1 스키마를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-453">After the SWPM database instance installation is completed, you can see the SAPABAP1 schema in SAP HANA Studio:</span></span>

![SAP HANA Studio의 SAPABAP1 스키마](./media/hana-get-started/image038b.jpg)

<span data-ttu-id="19163-455">마지막으로 SAP 앱 서버 및 SAP GUI 설치가 완료되면 **DBA Cockpit** 트랜잭션을 사용하여 HANA DB 인스턴스를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-455">Finally, after the SAP app server and SAP GUI installations are completed, you can verify the HANA DB instance by using the **DBA Cockpit** transaction:</span></span>

![DBA Cockpit 트랜잭션으로 확인된 HANA DB 인스턴스](./media/hana-get-started/image039b.jpg)


## <a name="sap-software-downloads"></a><span data-ttu-id="19163-457">SAP 소프트웨어 다운로드</span><span class="sxs-lookup"><span data-stu-id="19163-457">SAP software downloads</span></span>
<span data-ttu-id="19163-458">다음 스크린샷과 같이 SAP Service Marketplace에서 소프트웨어를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19163-458">You can download software from the SAP Service Marketplace, as shown in the following screenshots.</span></span>

<span data-ttu-id="19163-459">Linux/HANA용 NetWeaver 7.5 다운로드:</span><span class="sxs-lookup"><span data-stu-id="19163-459">Download NetWeaver 7.5 for Linux/HANA:</span></span>

 ![NetWeaver 7.5를 다운로드하기 위한 SAP 서비스 설치 및 업그레이드 창](./media/hana-get-started/image001.jpg)

<span data-ttu-id="19163-461">HANA SP12 Platform Edition 다운로드:</span><span class="sxs-lookup"><span data-stu-id="19163-461">Download HANA SP12 Platform Edition:</span></span>

 ![HANA SP12 Platform Edition을 다운로드하기 위한 SAP 서비스 설치 및 업그레이드 창](./media/hana-get-started/image002.jpg)

