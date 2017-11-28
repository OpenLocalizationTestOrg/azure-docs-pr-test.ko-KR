---
title: "Azure Site Recovery를 사용하여 다중 계층 IIS 기반 웹 응용 프로그램 복제 | Microsoft Docs"
description: "이 문서에서는 Azure Site Recovery를 사용하여 IIS 웹 팜 가상 컴퓨터를 복제하는 방법에 대해 설명합니다."
services: site-recovery
documentationcenter: 
author: nsoneji
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: nisoneji
ms.openlocfilehash: 4ac79df703de00ac009d9845772d8be740e74f29
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="replicate-a-multi-tier-iis-based-web-application-using-azure-site-recovery"></a><span data-ttu-id="4b130-103">Azure Site Recovery를 사용하여 다중 계층 IIS 기반 웹 응용 프로그램 복제</span><span class="sxs-lookup"><span data-stu-id="4b130-103">Replicate a multi-tier IIS based web application using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="4b130-104">개요</span><span class="sxs-lookup"><span data-stu-id="4b130-104">Overview</span></span>


<span data-ttu-id="4b130-105">응용 프로그램 소프트웨어는 조직에서 비즈니스 생산성의 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-105">Application software is the engine of business productivity in an organization.</span></span> <span data-ttu-id="4b130-106">다양한 웹 응용 프로그램은 조직 내 여러 용도로 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-106">Various web applications can serve different purposes in an organization.</span></span> <span data-ttu-id="4b130-107">급여 처리, 금융 응용 프로그램 및 고객 연결 웹 사이트와 같은 일부 응용 프로그램은 조직에 매우 중요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-107">Some of these like payroll processing, financial applications and customer facing websites can be utmost critical for an organization.</span></span> <span data-ttu-id="4b130-108">조직 내 생산성의 손실, 더 나아가 브랜드 이미지 손상을 방지하기 위해 이러한 웹 응용 프로그램이 항상 정상적으로 실행되도록 하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-108">It will be important for the organization to have them up and running at all times to prevent loss of productivity and more importantly prevent any damage to the brand image of the organization.</span></span>

<span data-ttu-id="4b130-109">중요한 웹 응용 프로그램은 일반적으로 웹, 데이터베이스 및 응용 프로그램이 서로 다른 계층에 있는 다중 계층 응용 프로그램으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-109">Critical web applications are typically set up as multi-tier applications with the web, database and application on different tiers.</span></span> <span data-ttu-id="4b130-110">여러 계층으로 분산하는 것 외에도 각 계층에 여러 서버를 사용하여 트래픽 부하를 분산할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-110">Apart from being spread across various tiers, the applications may also be using multiple servers in each tier to load balance the traffic.</span></span> <span data-ttu-id="4b130-111">또한 다양한 계층 간 그리고 웹 서버 상의 매핑은 고정 IP 주소를 기반으로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-111">Moreover, the mappings between various tiers and on the web server may be based on static IP addresses.</span></span> <span data-ttu-id="4b130-112">장애 조치에서, 특히 웹 서버에 구성된 웹 사이트가 여러 개 있는 경우 이러한 매핑 중 일부를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-112">On failover, some of these mappings will need to be updated, especially, if you have multiple websites configured on the web server.</span></span> <span data-ttu-id="4b130-113">SSL을 사용하는 웹 응용 프로그램의 경우 인증서 바인딩을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-113">In case of web applications using SSL, certificate bindings will need to be updated.</span></span>

<span data-ttu-id="4b130-114">기존의 비복제 기반 복구 방법에는 다양한 구성 파일, 레지스트리 설정, 바인딩, 사용자 지정 구성 요소(COM 또는 .NET), 콘텐츠 및 인증서를 백업하고, 일단의 수동 단계를 통해 파일을 복구하는 작업이 필연적으로 수반됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-114">Traditional non-replication based recovery methods involve backing up of various configuration files, registry settings, bindings, custom components (COM or .NET), content and also certificates and recovering the files through a set of manual steps.</span></span> <span data-ttu-id="4b130-115">이러한 기술은 분명히 번거롭고, 오류가 발생하기 쉽고, 확장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-115">These techniques are clearly cumbersome, error prone and not scalable.</span></span> <span data-ttu-id="4b130-116">예를 들어 인증서를 백업하는 것을 쉽게 잊어버릴 수 있으며, 장애 조치 후에 서버에 대한 새 인증서를 구입할 수 밖에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-116">It is, for example, easily possible for you to forget backing up certificates and be left with no choice but to buy new certificates for the server after failover.</span></span>

<span data-ttu-id="4b130-117">훌륭한 재해 복구 솔루션에서는 위의 복잡한 응용 프로그램 아키텍처에 기반하여 복구 계획을 모델링할 수 있어야 하며, 다양한 계층 간의 응용 프로그램 매핑을 처리하기 위한 사용자 지정 단계를 추가할 수 있어야 합니다. 이에 따라 재해 발생시 한 번의 클릭으로 RTO(복구 시간 목표)를 낮추는 확실한 솔루션을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-117">A good disaster recovery solution, should allow modeling of recovery plans around the above complex application architectures and also have the ability to add customized steps to handle application mappings between various tiers hence providing a single-click sure shot solution in the event of a disaster leading to a lower RTO.</span></span>


<span data-ttu-id="4b130-118">이 문서에서는 [Azure Site Recovery](site-recovery-overview.md)를 사용하여 IIS 기반 웹 응용 프로그램을 보호하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-118">This article describes how to protect an IIS based web application using a [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="4b130-119">그리고 3계층 IIS 기반 웹 응용 프로그램을 Azure로 복제하는 방법, 재해 복구 연습을 수행하는 방법 및 응용 프로그램을 Azure로 장애 조치하는 방법에 대한 모범 사례를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-119">This article will cover best practices for replicating a three tier IIS based web application to Azure, how you can do a disaster recovery drill, and how you can failover the application to Azure.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="4b130-120">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4b130-120">Prerequisites</span></span>

<span data-ttu-id="4b130-121">시작하기 전에 다음 항목을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-121">Before you start, make sure you understand the following:</span></span>

1. [<span data-ttu-id="4b130-122">Azure에 가상 컴퓨터 복제</span><span class="sxs-lookup"><span data-stu-id="4b130-122">Replicating a virtual machine to Azure</span></span>](site-recovery-vmware-to-azure.md)
1. <span data-ttu-id="4b130-123">방법: [복구 네트워크 디자인](site-recovery-network-design.md)</span><span class="sxs-lookup"><span data-stu-id="4b130-123">How to [design a recovery network](site-recovery-network-design.md)</span></span>
1. [<span data-ttu-id="4b130-124">Azure로 테스트 장애 조치 수행</span><span class="sxs-lookup"><span data-stu-id="4b130-124">Doing a test failover to Azure</span></span>](./site-recovery-test-failover-to-azure.md)
1. [<span data-ttu-id="4b130-125">Azure로 장애 조치 수행</span><span class="sxs-lookup"><span data-stu-id="4b130-125">Doing a failover to Azure</span></span>](site-recovery-failover.md)
1. <span data-ttu-id="4b130-126">방법: [도메인 컨트롤러 복제](site-recovery-active-directory.md)</span><span class="sxs-lookup"><span data-stu-id="4b130-126">How to [replicate a domain controller](site-recovery-active-directory.md)</span></span>
1. <span data-ttu-id="4b130-127">방법: [SQL Server 복제](site-recovery-sql.md)</span><span class="sxs-lookup"><span data-stu-id="4b130-127">How to [replicate SQL Server](site-recovery-sql.md)</span></span>

## <a name="deployment-patterns"></a><span data-ttu-id="4b130-128">배포 패턴</span><span class="sxs-lookup"><span data-stu-id="4b130-128">Deployment patterns</span></span>
<span data-ttu-id="4b130-129">IIS 기반 웹 응용 프로그램은 일반적으로 다음 배포 패턴 중 하나를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-129">An IIS based web application typically follows one of the following deployment patterns:</span></span>

<span data-ttu-id="4b130-130">**배포 패턴 1** ARR(응용 프로그램 요청 라우팅), IIS 서버 및 Microsoft SQL Server를 사용하는 IIS 기반 웹 팜</span><span class="sxs-lookup"><span data-stu-id="4b130-130">**Deployment pattern 1 ** An IIS based web farm  with Application Request Routing(ARR), IIS Server and Microsoft SQL Server.</span></span>

![배포 패턴](./media/site-recovery-iis/deployment-pattern1.png)

<span data-ttu-id="4b130-132">**배포 패턴 2** ARR(응용 프로그램 요청 라우팅), IIS 서버, 응용 프로그램 서버 및 Microsoft SQL Server를 사용하는 IIS 기반 웹 팜</span><span class="sxs-lookup"><span data-stu-id="4b130-132">**Deployment pattern 2** An IIS based web farm with Application Request Routing(ARR), IIS Server, Application Server, and Microsoft SQL Server.</span></span>


![배포 패턴](./media/site-recovery-iis/deployment-pattern2.png)

## <a name="site-recovery-support"></a><span data-ttu-id="4b130-134">Site Recovery 지원</span><span class="sxs-lookup"><span data-stu-id="4b130-134">Site Recovery support</span></span>

<span data-ttu-id="4b130-135">이 문서를 작성하기 위해 Windows Server 2012 R2 Enterprise에 IIS 서버 버전 7.5가 있는 VMware 가상 컴퓨터가 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-135">For the purpose of creating this article VMware virtual machines with IIS Server version 7.5 on Windows Server 2012 R2 Enterprise were used.</span></span> <span data-ttu-id="4b130-136">사이트 복구 복제는 응용 프로그램을 제한하지 않으므로 여기서 제시하는 권장 사항은 다음 시나리오뿐만 아니라 다른 버전의 IIS에서도 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-136">As site recovery replication is application agnostic, the recommendations provided here are expected to hold on following scenarios as well and for different version of IIS.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="4b130-137">원본 및 대상</span><span class="sxs-lookup"><span data-stu-id="4b130-137">Source and target</span></span>

<span data-ttu-id="4b130-138">**시나리오**</span><span class="sxs-lookup"><span data-stu-id="4b130-138">**Scenario**</span></span> | <span data-ttu-id="4b130-139">**보조 사이트로**</span><span class="sxs-lookup"><span data-stu-id="4b130-139">**To a secondary site**</span></span> | <span data-ttu-id="4b130-140">**Azure로**</span><span class="sxs-lookup"><span data-stu-id="4b130-140">**To Azure**</span></span>
--- | --- | ---
<span data-ttu-id="4b130-141">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="4b130-141">**Hyper-V**</span></span> | <span data-ttu-id="4b130-142">예</span><span class="sxs-lookup"><span data-stu-id="4b130-142">Yes</span></span> | <span data-ttu-id="4b130-143">예</span><span class="sxs-lookup"><span data-stu-id="4b130-143">Yes</span></span>
<span data-ttu-id="4b130-144">**VMware**</span><span class="sxs-lookup"><span data-stu-id="4b130-144">**VMware**</span></span> | <span data-ttu-id="4b130-145">예</span><span class="sxs-lookup"><span data-stu-id="4b130-145">Yes</span></span> | <span data-ttu-id="4b130-146">예</span><span class="sxs-lookup"><span data-stu-id="4b130-146">Yes</span></span>
<span data-ttu-id="4b130-147">**물리적 서버**</span><span class="sxs-lookup"><span data-stu-id="4b130-147">**Physical server**</span></span> | <span data-ttu-id="4b130-148">아니요</span><span class="sxs-lookup"><span data-stu-id="4b130-148">No</span></span> | <span data-ttu-id="4b130-149">예</span><span class="sxs-lookup"><span data-stu-id="4b130-149">Yes</span></span>

## <a name="replicate-virtual-machines"></a><span data-ttu-id="4b130-150">가상 컴퓨터 복제</span><span class="sxs-lookup"><span data-stu-id="4b130-150">Replicate virtual machines</span></span>

<span data-ttu-id="4b130-151">[이 지침](site-recovery-vmware-to-azure.md)에 따라 모든 IIS 웹 팜 가상 컴퓨터를 Azure로 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-151">Follow [this guidance](site-recovery-vmware-to-azure.md) to start replicating all the IIS web farm virtual machines to Azure.</span></span>

<span data-ttu-id="4b130-152">고정 IP를 사용하는 경우 계산 및 네트워크 설정의 [**대상 IP**](./site-recovery-replicate-vmware-to-azure.md#view-and-manage-vm-properties) 설정에 가상 컴퓨터에서 사용할 IP를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-152">If you are using a static IP then specify the IP that you want the virtual machine to take in the [**Target IP**](./site-recovery-replicate-vmware-to-azure.md#view-and-manage-vm-properties) setting in Compute and Network settings.</span></span>

![대상 IP](./media/site-recovery-active-directory/dns-target-ip.png)


## <a name="creating-a-recovery-plan"></a><span data-ttu-id="4b130-154">복구 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="4b130-154">Creating a recovery plan</span></span>

<span data-ttu-id="4b130-155">복구 계획을 사용하면 다중 계층 응용 프로그램에서 다양한 계층의 장애 조치를 시퀀싱하여 응용 프로그램의 일관성을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-155">A recovery plan allows sequencing the failover of various tiers in a multi-tier application, hence, maintaining application consistency.</span></span> <span data-ttu-id="4b130-156">다중 계층 웹 응용 프로그램에 대한 복구 계획을 만드는 동안 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-156">Follow the below steps while creating a recovery plan for a multi-tier web application.</span></span>  <span data-ttu-id="4b130-157">[복구 계획 만들기에 대한 자세한 정보](./site-recovery-create-recovery-plans.md)</span><span class="sxs-lookup"><span data-stu-id="4b130-157">[Learn more about creating a recovery plan](./site-recovery-create-recovery-plans.md).</span></span>

### <a name="adding-virtual-machines-to-failover-groups"></a><span data-ttu-id="4b130-158">장애 조치 그룹에 가상 컴퓨터 추가</span><span class="sxs-lookup"><span data-stu-id="4b130-158">Adding virtual machines to failover groups</span></span>
<span data-ttu-id="4b130-159">일반적인 다중 계층 IIS 웹 응용 프로그램은 SQL 가상 컴퓨터가 있는 데이터베이스 계층 및 IIS 서버와 응용 프로그램 계층으로 구성된 웹 계층으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-159">A typical multi-tier IIS web application will consist of a database tier with SQL virtual machines, the web tier constituted by a IIS server and an application tier.</span></span> <span data-ttu-id="4b130-160">아래와 같이 계층을 기반으로 하여 서로 다른 그룹에 이러한 모든 가상 컴퓨터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-160">Add all these virtual machines to different group based on tier as below.</span></span> <span data-ttu-id="4b130-161">[복구 계획 사용자 지정에 대한 자세한 정보](site-recovery-runbook-automation.md#customize-the-recovery-plan)</span><span class="sxs-lookup"><span data-stu-id="4b130-161">[Learn more about customising recovery plan](site-recovery-runbook-automation.md#customize-the-recovery-plan).</span></span>

1. <span data-ttu-id="4b130-162">복구 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-162">Create a recovery plan.</span></span> <span data-ttu-id="4b130-163">맨 마지막으로 종료하고 맨 먼저 작동하도록 그룹 1에 데이터베이스 계층 가상 컴퓨터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-163">Add the database tier virtual machines under Group 1 to ensure that they are shutdown last and brought up first.</span></span>

1. <span data-ttu-id="4b130-164">데이터베이스 계층을 작동한 후에 작동하도록 그룹 2에 응용 프로그램 계층 가상 컴퓨터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-164">Add the application tier virtual machines under Group 2 such that they are brought up after the database tier has been brought up.</span></span>

1. <span data-ttu-id="4b130-165">응용 프로그램 계층을 작동한 후에 작동하도록 그룹 3에 웹 계층 가상 컴퓨터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-165">Add the web tier virtual machines in Group 3 such that they are brought up after the application tier has been brought up.</span></span>

1. <span data-ttu-id="4b130-166">웹 계층을 작동한 후에 작동하도록 그룹 4에 부하 분산 가상 컴퓨터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-166">Add load balance virtual machines in Group 4 such that they are brought up after the web tier has been brought up.</span></span>


### <a name="adding-scripts-to-the-recovery-plan"></a><span data-ttu-id="4b130-167">복구 계획에 스크립트 추가</span><span class="sxs-lookup"><span data-stu-id="4b130-167">Adding scripts to the recovery plan</span></span>
<span data-ttu-id="4b130-168">장애 조치/테스트 장애 조치 후에 IIS 웹 팜 기능이 올바르게 작동하도록 Azure 가상 컴퓨터에서 일부 작업을 수행해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-168">You may need to do some operations on the Azure virtual machines post failover/Test failover to make IIS web farm function correctly.</span></span> <span data-ttu-id="4b130-169">아래와 같이 복구 계획에 해당 스크립트를 추가하여 DNS 항목 업데이트, 사이트 바인딩 변경, 연결 문자열 변경 등과 같은 사후 장애 조치 작업을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-169">You can automate the post failover operation like updating DNS entry, changing site binding, change  in connection string  by adding corresponding scripts in the recovery plan as below.</span></span> <span data-ttu-id="4b130-170">[복구 계획에 스크립트 추가에 대한 자세한 정보](./site-recovery-create-recovery-plans.md#add-scripts)</span><span class="sxs-lookup"><span data-stu-id="4b130-170">[Learn more about add script recovery plan](./site-recovery-create-recovery-plans.md#add-scripts).</span></span>

#### <a name="dns-update"></a><span data-ttu-id="4b130-171">DNS 업데이트</span><span class="sxs-lookup"><span data-stu-id="4b130-171">DNS Update</span></span>
<span data-ttu-id="4b130-172">DNS가 동적 DNS 업데이트를 위해 구성된 경우 일반적으로 가상 컴퓨터를 시작할 때 새 IP로 DNS를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-172">If the DNS is configured for dynamic DNS update then virtual machines usually update the DNS with the new IP once they start.</span></span> <span data-ttu-id="4b130-173">가상 컴퓨터의 새 IP로 DNS를 업데이트하는 명시적인 단계를 추가하려면 복구 계획 그룹의 사후 작업으로 [DNS의 IP를 업데이트하는 스크립트](https://aka.ms/asr-dns-update)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-173">If you want to add an explicit step to update DNS with the new IPs of the virtual machines then add this [script to update IP in DNS](https://aka.ms/asr-dns-update) as a post action on recovery plan groups.</span></span>  

#### <a name="connection-string-in-an-applications-webconfig"></a><span data-ttu-id="4b130-174">응용 프로그램의 web.config에 있는 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="4b130-174">Connection string in an application’s web.config</span></span>
<span data-ttu-id="4b130-175">연결 문자열은 웹 사이트에서 통신하는 데이터베이스를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-175">The connection string specifies the database that the web site communicates with.</span></span>

<span data-ttu-id="4b130-176">연결 문자열에 데이터베이스 가상 컴퓨터의 이름이 있으면 장애 조치 후의 추가 단계가 필요하지 않고 응용 프로그램에서 DB와 자동으로 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-176">If the connection string carries the name of the database virtual machine, no further steps will be needed post failover and the application will be able to automatically communicate to the DB.</span></span> <span data-ttu-id="4b130-177">또한 데이터베이스 가상 컴퓨터의 IP 주소가 유지되면 연결 문자열을 업데이트할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-177">Also, if the IP address for the database virtual machine is retained, it will not be needed to update the connection string.</span></span> <span data-ttu-id="4b130-178">연결 문자열에서 IP 주소를 사용하는 데이터베이스 가상 컴퓨터를 참조하는 경우 장애 조치 후 해당 IP를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-178">If the connection string refers to the database virtual machine using an IP address, it will need to be updated post failover.</span></span> <span data-ttu-id="4b130-179">예:</span><span class="sxs-lookup"><span data-stu-id="4b130-179">E.g.</span></span> <span data-ttu-id="4b130-180">아래 연결 문자열은 127.0.1.2 IP를 사용하는 DB를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-180">the below connection string points to the DB with IP 127.0.1.2</span></span>

        <?xml version="1.0" encoding="utf-8"?>
        <configuration>
        <connectionStrings>
        <add name="ConnStringDb1" connectionString="Data Source= 127.0.1.2\SqlExpress; Initial Catalog=TestDB1;Integrated Security=False;" />
        </connectionStrings>
        </configuration>

<span data-ttu-id="4b130-181">복구 계획에서 그룹 3 뒤에 [IIS 연결 업데이트 스크립트](https://aka.ms/asr-update-webtier-script-classic)를 추가하여 웹 계층의 연결 문자열을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-181">You can update the connection string in web tier by adding [IIS connection update script](https://aka.ms/asr-update-webtier-script-classic) after Group 3 in the recovery plan.</span></span>

#### <a name="site-bindings-for-the-application"></a><span data-ttu-id="4b130-182">응용 프로그램에 대한 사이트 바인딩</span><span class="sxs-lookup"><span data-stu-id="4b130-182">Site bindings for the application</span></span>
<span data-ttu-id="4b130-183">모든 사이트는 바인딩 형식, IIS 서버에서 사이트 요청을 수신 대기하는 IP 주소, 포트 번호 및 사이트의 호스트 이름을 포함하는 바인딩 정보로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-183">Every site consists of binding information that includes the type of binding, the IP address at which the IIS server listens to the requests for the site, the port number and the host names for the site.</span></span> <span data-ttu-id="4b130-184">장애 조치 시 연결되는 IP 주소가 변경된 경우 이러한 바인딩을 업데이트해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-184">At the time of a failover, these bindings might need to be updated if there is a change in the IP address associated with them.</span></span>

> [!NOTE]
>
> <span data-ttu-id="4b130-185">아래 예제와 같이 사이트 바인딩에 대해 '모두 할당되지 않음'으로 표시했으면 장애 조치 후에 이 바인딩을 업데이트할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-185">If you have marked ‘all unassigned’ for the site binding as in the example below, you will not need to update this binding post failover.</span></span> <span data-ttu-id="4b130-186">또한 사이트와 연결된 IP 주소가 장애 조치 후에 변경되지 않으면 사이트 바인딩을 업데이트할 필요가 없습니다. (IP 주소의 보존은 기본 사이트와 복구 사이트에 할당된 네트워크 아키텍처 및 서브넷에 따라 달라지므로 조직에 적합하거나 적합하지 않을 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="4b130-186">Also, if the IP address associated with a site is not changed post failover, the site binding need not be updated (Retention of the IP address depends on the network architecture and subnets assigned to the primary and recovery sites and hence may or may not be feasible for your organization.)</span></span>

![SSL 바인딩](./media/site-recovery-iis/sslbinding.png)

<span data-ttu-id="4b130-188">IP 주소를 사이트와 연결한 경우 모든 사이트 바인딩을 새 IP 주소로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-188">If you have associated the IP address with a site, you will need to update all site bindings with the new IP address.</span></span> <span data-ttu-id="4b130-189">복구 계획에서 그룹 3 뒤에 [IIS 웹 계층 업데이트 스크립트](https://aka.ms/asr-web-tier-update-runbook-classic)를 추가하여 사이트 바인딩을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-189">You can add [IIS Web tier update script](https://aka.ms/asr-web-tier-update-runbook-classic) after Group 3 in recovery plan to change the site bindings.</span></span>


#### <a name="update-load-balancer-ip-address"></a><span data-ttu-id="4b130-190">부하 분산 장치 IP 주소 업데이트</span><span class="sxs-lookup"><span data-stu-id="4b130-190">Update load balancer IP address</span></span>
<span data-ttu-id="4b130-191">ARR(응용 프로그램 요청 라우팅) 가상 컴퓨터가 있는 경우 그룹 4 뒤에 [IIS ARR 장애 조치 스크립트](https://aka.ms/asr-iis-arrtier-failover-script-classic)를 추가하여 IP 주소를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-191">If you have  Application Request Routing virtual machine, add [IIS ARR  failover script](https://aka.ms/asr-iis-arrtier-failover-script-classic) after Group 4 to update the IP address.</span></span>

#### <a name="the-ssl-cert-binding-for-an-https-connection"></a><span data-ttu-id="4b130-192">https 연결을 위한 SSL 인증서 바인딩</span><span class="sxs-lookup"><span data-stu-id="4b130-192">The SSL cert binding for an https connection</span></span>
<span data-ttu-id="4b130-193">웹 사이트에는 웹 서버와 사용자의 브라우저 사이의 보안 통신을 보장하는 데 도움이 되는 연결된 SSL 인증서가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-193">Websites can have an associated SSL certificate that helps in ensuring a secure communication between the webserver and the user’s browser.</span></span> <span data-ttu-id="4b130-194">웹 사이트에 SSL 인증서 바인딩과 함께 IIS 서버의 IP 주소에 대한 https 연결 및 연결된 https 사이트 바인딩이 있는 경우 장애 조치 후에 IIS 가상 컴퓨터의 IP를 사용하여 인증서에 대한 새 사이트 바인딩을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-194">If the website has an https connection and an associated https site binding to the IP address of the IIS server with an SSL cert binding, a new site binding will need to be added for the cert with the IP of the IIS virtual machine post failover.</span></span>

<span data-ttu-id="4b130-195">SSL 인증서는 다음 항목에 대해 발급될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-195">The SSL cert can be issued against-</span></span>

<span data-ttu-id="4b130-196">a) 웹 사이트의 정규화된 도메인 이름</span><span class="sxs-lookup"><span data-stu-id="4b130-196">a) The fully qualified domain name of the website</span></span><br>
<span data-ttu-id="4b130-197">b) 서버의 이름</span><span class="sxs-lookup"><span data-stu-id="4b130-197">b) The name of the server</span></span><br>
<span data-ttu-id="4b130-198">c) 도메인 이름에 대한 와일드카드 인증서</span><span class="sxs-lookup"><span data-stu-id="4b130-198">c) A wildcard certificate for the domain name</span></span><br>
<span data-ttu-id="4b130-199">d) IP 주소 - SSL 서버 인증서가 IIS 서버의 IP에 대해 발급되면, Azure 사이트에 있는 IIS 서버의 IP 주소에 대해 다른 SSL 인증서를 발급해야 하며 이 인증서에 대한 추가 SSL 바인딩을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-199">d) An IP address – If the SSL cert is issued against the IP of the IIS server, another SSL cert needs to be issued against the IP address of the IIS server on the Azure site and an additional SSL binding for this certificate will need to be created.</span></span> <span data-ttu-id="4b130-200">따라서 IP에 대해 발급된 SSL 인증서는 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-200">Hence, it is advisable to not use an SSL cert issued against IP.</span></span> <span data-ttu-id="4b130-201">이는 널리 사용되지 않는 옵션이며, CA/브라우저 포럼의 새로운 변경 내용에 따라 곧 사용되지 않을 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-201">This is a less widely used option and will soon be deprecated as per new CA/browser forum changes.</span></span>

#### <a name="update-the-dependency-between-the-web-and-the-application-tier"></a><span data-ttu-id="4b130-202">웹과 응용 프로그램 계층 간 종속성 업데이트</span><span class="sxs-lookup"><span data-stu-id="4b130-202">Update the dependency between the web and the application tier</span></span>
<span data-ttu-id="4b130-203">가상 컴퓨터의 IP 주소를 기반으로 하는 응용 프로그램 특정 종속성이 있는 경우 장애 조치 후에 이 종속성을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-203">If you have an application specific dependency based on the IP address of the virtual machines, you need to update this dependency post failover.</span></span>

## <a name="doing-a-test-failover"></a><span data-ttu-id="4b130-204">테스트 장애 조치 수행</span><span class="sxs-lookup"><span data-stu-id="4b130-204">Doing a test failover</span></span>
<span data-ttu-id="4b130-205">[이 지침](site-recovery-test-failover-to-azure.md)에 따라 테스트 장애 조치를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-205">Follow [this guidance](site-recovery-test-failover-to-azure.md) to do a test failover.</span></span>

1.  <span data-ttu-id="4b130-206">Azure Portal로 이동하여 Recovery Service 자격 증명 모음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-206">Go to Azure portal and select your Recovery Service vault.</span></span>
1.  <span data-ttu-id="4b130-207">IIS 웹 팜에 대해 만든 복구 계획을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-207">Click on the recovery plan created for IIS web farm.</span></span>
1.  <span data-ttu-id="4b130-208">'테스트 장애 조치'를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-208">Click on 'Test Failover'.</span></span>
1.  <span data-ttu-id="4b130-209">복구 지점 및 Azure 가상 네트워크를 선택하여 테스트 장애 조치 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-209">Select recovery point and Azure virtual network to start the test failover process.</span></span>
1.  <span data-ttu-id="4b130-210">보조 환경이 가동 중이면 유효성 검사를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-210">Once the secondary environment is up, you can perform your validations.</span></span>
1.  <span data-ttu-id="4b130-211">유효성 검사가 완료되면 '유효성 검사 완료'를 선택할 수 있으며 테스트 장애 조치 환경이 정리됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-211">Once the validations are complete, you can select ‘Validations complete’ and the test failover environment will be cleaned.</span></span>

## <a name="doing-a-failover"></a><span data-ttu-id="4b130-212">장애 조치 수행</span><span class="sxs-lookup"><span data-stu-id="4b130-212">Doing a failover</span></span>
<span data-ttu-id="4b130-213">장애 조치를 수행할 때 [이 지침](site-recovery-failover.md)을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-213">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

1.  <span data-ttu-id="4b130-214">Azure Portal로 이동하여 Recovery Service 자격 증명 모음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-214">Go to Azure portal and select your Recovery Service vault.</span></span>
1.  <span data-ttu-id="4b130-215">IIS 웹 팜에 대해 만든 복구 계획을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-215">Click on the recovery plan created for IIS web farm.</span></span>
1.  <span data-ttu-id="4b130-216">'장애 조치'를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-216">Click on 'Failover'.</span></span>
1.  <span data-ttu-id="4b130-217">복구 지점을 선택하여 장애 조치 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-217">Select recovery point to start the failover process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b130-218">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4b130-218">Next steps</span></span>
<span data-ttu-id="4b130-219">Site Recovery를 사용하여 [다른 응용 프로그램을 복제하는 방법](site-recovery-workload.md)에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b130-219">You can learn more about [replicate other applications](site-recovery-workload.md) using Site Recovery.</span></span>
