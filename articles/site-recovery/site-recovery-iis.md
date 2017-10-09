---
title: "다중 계층 IIS aaaReplicate 기반 Azure Site Recovery를 사용 하 여 웹 응용 프로그램 | Microsoft Docs"
description: "이 문서에서는 어떻게 tooreplicate IIS 웹 팜 가상 컴퓨터를 Azure Site Recovery를 사용 하 여 설명 합니다."
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
ms.openlocfilehash: 1974265b3cb05f6dc57049876306d2e08424bb97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-iis-based-web-application-using-azure-site-recovery"></a><span data-ttu-id="c0448-103">Azure Site Recovery를 사용하여 다중 계층 IIS 기반 웹 응용 프로그램 복제</span><span class="sxs-lookup"><span data-stu-id="c0448-103">Replicate a multi-tier IIS based web application using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="c0448-104">개요</span><span class="sxs-lookup"><span data-stu-id="c0448-104">Overview</span></span>


<span data-ttu-id="c0448-105">응용 프로그램 소프트웨어는 조직에서 비즈니스 생산성 hello 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-105">Application software is hello engine of business productivity in an organization.</span></span> <span data-ttu-id="c0448-106">다양한 웹 응용 프로그램은 조직 내 여러 용도로 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-106">Various web applications can serve different purposes in an organization.</span></span> <span data-ttu-id="c0448-107">급여 처리, 금융 응용 프로그램 및 고객 연결 웹 사이트와 같은 일부 응용 프로그램은 조직에 매우 중요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-107">Some of these like payroll processing, financial applications and customer facing websites can be utmost critical for an organization.</span></span> <span data-ttu-id="c0448-108">것은 중요 한 hello 조직 toohave를 고 항상 tooprevent 생산성 저하 간격으로 실행 되 고 더 중요 한 것은 hello 조직의 손상 toohello 브랜드 이미지를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-108">It will be important for hello organization toohave them up and running at all times tooprevent loss of productivity and more importantly prevent any damage toohello brand image of hello organization.</span></span>

<span data-ttu-id="c0448-109">일반적으로 다양 한 계층에서 응용 프로그램, hello 웹 및 데이터베이스와 다중 계층 응용 프로그램으로 중요 한 웹 응용 프로그램 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-109">Critical web applications are typically set up as multi-tier applications with hello web, database and application on different tiers.</span></span> <span data-ttu-id="c0448-110">다양 한 계층에 분산 되 고, 이외 hello 응용 프로그램 사용할 수도 있습니다 여러 서버에서 각 계층 tooload hello 트래픽의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-110">Apart from being spread across various tiers, hello applications may also be using multiple servers in each tier tooload balance hello traffic.</span></span> <span data-ttu-id="c0448-111">또한 hello 매핑 다양 한 계층 간 및 hello 웹 서버에서 고정 IP 주소에 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-111">Moreover, hello mappings between various tiers and on hello web server may be based on static IP addresses.</span></span> <span data-ttu-id="c0448-112">장애 조치 시 hello 웹 서버에 구성 된 여러 웹 사이트를 설정한 경우, 특히 업데이트 toobe 이러한 매핑 중 일부를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-112">On failover, some of these mappings will need toobe updated, especially, if you have multiple websites configured on hello web server.</span></span> <span data-ttu-id="c0448-113">SSL을 사용 하는 웹 응용 프로그램의 경우 인증서 바인딩을 toobe 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-113">In case of web applications using SSL, certificate bindings will need toobe updated.</span></span>

<span data-ttu-id="c0448-114">다양 한 구성 파일, 레지스트리 설정, 바인딩, 사용자 지정 구성 요소 (COM 또는.NET), 콘텐츠 및 또한 인증서 및 일련의 수동 단계를 통해 복구 hello 파일의 백업을 포함 하는 기존의 비 복제 기반된 복구 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-114">Traditional non-replication based recovery methods involve backing up of various configuration files, registry settings, bindings, custom components (COM or .NET), content and also certificates and recovering hello files through a set of manual steps.</span></span> <span data-ttu-id="c0448-115">이러한 기술은 분명히 번거롭고, 오류가 발생하기 쉽고, 확장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-115">These techniques are clearly cumbersome, error prone and not scalable.</span></span> <span data-ttu-id="c0448-116">예를 들어, 쉽게 tooforget 인증서를 백업에 대 한 가능한 한 남겨둘 toobuy 없지만 선택 된 hello 서버에 대 한 인증서를 새 장애 조치 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-116">It is, for example, easily possible for you tooforget backing up certificates and be left with no choice but toobuy new certificates for hello server after failover.</span></span>

<span data-ttu-id="c0448-117">좋은 재해 복구 솔루션을 복잡 한 응용 프로그램 아키텍처 위에 hello 주위 복구 계획의 모델링을 허용 하 고 hello 기능 사용자 지정 tooadd 단계 toohandle 응용 프로그램 간의 매핑을 제공 되므로 다양 한 계층을 갖게 해야는 단일 클릭 했는지 tooa 선행 재해의 hello 이벤트에서 솔루션을 샷 RTO를 낮추면 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-117">A good disaster recovery solution, should allow modeling of recovery plans around hello above complex application architectures and also have hello ability tooadd customized steps toohandle application mappings between various tiers hence providing a single-click sure shot solution in hello event of a disaster leading tooa lower RTO.</span></span>


<span data-ttu-id="c0448-118">이 문서에서 설명 하는 IIS tooprotect 사용 하 여 웹 응용 프로그램 기반으로 한 [Azure Site Recovery](site-recovery-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-118">This article describes how tooprotect an IIS based web application using a [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="c0448-119">이 문서에서는 IIS 기반 웹 응용 프로그램 tooAzure, 재해 복구 훈련과 수행 하는 방법은 및 장애 조치 hello 응용 프로그램 tooAzure 하는 방법을 3 계층을 복제 하기 위한 모범 사례를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-119">This article will cover best practices for replicating a three tier IIS based web application tooAzure, how you can do a disaster recovery drill, and how you can failover hello application tooAzure.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="c0448-120">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c0448-120">Prerequisites</span></span>

<span data-ttu-id="c0448-121">시작 하기 전에 hello 다음 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-121">Before you start, make sure you understand hello following:</span></span>

1. [<span data-ttu-id="c0448-122">가상 컴퓨터 tooAzure 복제</span><span class="sxs-lookup"><span data-stu-id="c0448-122">Replicating a virtual machine tooAzure</span></span>](site-recovery-vmware-to-azure.md)
1. <span data-ttu-id="c0448-123">어떻게 너무[복구 네트워크 디자인](site-recovery-network-design.md)</span><span class="sxs-lookup"><span data-stu-id="c0448-123">How too[design a recovery network](site-recovery-network-design.md)</span></span>
1. [<span data-ttu-id="c0448-124">테스트 장애 조치 tooAzure 수행</span><span class="sxs-lookup"><span data-stu-id="c0448-124">Doing a test failover tooAzure</span></span>](./site-recovery-test-failover-to-azure.md)
1. [<span data-ttu-id="c0448-125">장애 조치 tooAzure 수행</span><span class="sxs-lookup"><span data-stu-id="c0448-125">Doing a failover tooAzure</span></span>](site-recovery-failover.md)
1. <span data-ttu-id="c0448-126">어떻게 너무[도메인 컨트롤러 복제](site-recovery-active-directory.md)</span><span class="sxs-lookup"><span data-stu-id="c0448-126">How too[replicate a domain controller](site-recovery-active-directory.md)</span></span>
1. <span data-ttu-id="c0448-127">어떻게 너무[SQL Server 복제](site-recovery-sql.md)</span><span class="sxs-lookup"><span data-stu-id="c0448-127">How too[replicate SQL Server](site-recovery-sql.md)</span></span>

## <a name="deployment-patterns"></a><span data-ttu-id="c0448-128">배포 패턴</span><span class="sxs-lookup"><span data-stu-id="c0448-128">Deployment patterns</span></span>
<span data-ttu-id="c0448-129">일반적으로 IIS 기반 웹 응용 프로그램의 배포 패턴을 따르는 hello 하나를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-129">An IIS based web application typically follows one of hello following deployment patterns:</span></span>

<span data-ttu-id="c0448-130">**배포 패턴 1** ARR(응용 프로그램 요청 라우팅), IIS 서버 및 Microsoft SQL Server를 사용하는 IIS 기반 웹 팜</span><span class="sxs-lookup"><span data-stu-id="c0448-130">**Deployment pattern 1 ** An IIS based web farm  with Application Request Routing(ARR), IIS Server and Microsoft SQL Server.</span></span>

![배포 패턴](./media/site-recovery-iis/deployment-pattern1.png)

<span data-ttu-id="c0448-132">**배포 패턴 2** ARR(응용 프로그램 요청 라우팅), IIS 서버, 응용 프로그램 서버 및 Microsoft SQL Server를 사용하는 IIS 기반 웹 팜</span><span class="sxs-lookup"><span data-stu-id="c0448-132">**Deployment pattern 2** An IIS based web farm with Application Request Routing(ARR), IIS Server, Application Server, and Microsoft SQL Server.</span></span>


![배포 패턴](./media/site-recovery-iis/deployment-pattern2.png)

## <a name="site-recovery-support"></a><span data-ttu-id="c0448-134">Site Recovery 지원</span><span class="sxs-lookup"><span data-stu-id="c0448-134">Site Recovery support</span></span>

<span data-ttu-id="c0448-135">IIS 서버에서 Windows Server 2012 R2 Enterprise 버전 7.5 사용 하 여이 문서 VMware 가상 컴퓨터를 만드는 hello 목적을 위해 사용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-135">For hello purpose of creating this article VMware virtual machines with IIS Server version 7.5 on Windows Server 2012 R2 Enterprise were used.</span></span> <span data-ttu-id="c0448-136">사이트 복구 복제는 응용 프로그램 알 hello 권장 사항을 제공도 다음과 같은 시나리오와 서로 다른 버전의 IIS에 대 한 예상된 toohold 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-136">As site recovery replication is application agnostic, hello recommendations provided here are expected toohold on following scenarios as well and for different version of IIS.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="c0448-137">원본 및 대상</span><span class="sxs-lookup"><span data-stu-id="c0448-137">Source and target</span></span>

<span data-ttu-id="c0448-138">**시나리오**</span><span class="sxs-lookup"><span data-stu-id="c0448-138">**Scenario**</span></span> | <span data-ttu-id="c0448-139">**tooa 보조 사이트**</span><span class="sxs-lookup"><span data-stu-id="c0448-139">**tooa secondary site**</span></span> | <span data-ttu-id="c0448-140">**tooAzure**</span><span class="sxs-lookup"><span data-stu-id="c0448-140">**tooAzure**</span></span>
--- | --- | ---
<span data-ttu-id="c0448-141">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="c0448-141">**Hyper-V**</span></span> | <span data-ttu-id="c0448-142">예</span><span class="sxs-lookup"><span data-stu-id="c0448-142">Yes</span></span> | <span data-ttu-id="c0448-143">예</span><span class="sxs-lookup"><span data-stu-id="c0448-143">Yes</span></span>
<span data-ttu-id="c0448-144">**VMware**</span><span class="sxs-lookup"><span data-stu-id="c0448-144">**VMware**</span></span> | <span data-ttu-id="c0448-145">예</span><span class="sxs-lookup"><span data-stu-id="c0448-145">Yes</span></span> | <span data-ttu-id="c0448-146">예</span><span class="sxs-lookup"><span data-stu-id="c0448-146">Yes</span></span>
<span data-ttu-id="c0448-147">**물리적 서버**</span><span class="sxs-lookup"><span data-stu-id="c0448-147">**Physical server**</span></span> | <span data-ttu-id="c0448-148">아니요</span><span class="sxs-lookup"><span data-stu-id="c0448-148">No</span></span> | <span data-ttu-id="c0448-149">예</span><span class="sxs-lookup"><span data-stu-id="c0448-149">Yes</span></span>

## <a name="replicate-virtual-machines"></a><span data-ttu-id="c0448-150">가상 컴퓨터 복제</span><span class="sxs-lookup"><span data-stu-id="c0448-150">Replicate virtual machines</span></span>

<span data-ttu-id="c0448-151">에 따라 [이 지침은](site-recovery-vmware-to-azure.md) toostart 모든 hello IIS 웹 팜 가상 컴퓨터 tooAzure를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-151">Follow [this guidance](site-recovery-vmware-to-azure.md) toostart replicating all hello IIS web farm virtual machines tooAzure.</span></span>

<span data-ttu-id="c0448-152">고정 IP를 사용 하는 다음 hello에 가상 컴퓨터 tootake hello 원하는 hello IP를 지정 하는 경우 [ **대상 IP** ](./site-recovery-replicate-vmware-to-azure.md#view-and-manage-vm-properties) 계산 및 네트워크 설정에서 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-152">If you are using a static IP then specify hello IP that you want hello virtual machine tootake in hello [**Target IP**](./site-recovery-replicate-vmware-to-azure.md#view-and-manage-vm-properties) setting in Compute and Network settings.</span></span>

![대상 IP](./media/site-recovery-active-directory/dns-target-ip.png)


## <a name="creating-a-recovery-plan"></a><span data-ttu-id="c0448-154">복구 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="c0448-154">Creating a recovery plan</span></span>

<span data-ttu-id="c0448-155">복구 계획을 나열 하는 응용 프로그램 일관성을 유지 하는 다중 계층 응용 프로그램, 따라서의 다양 한 계층의 hello 장애 조치 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-155">A recovery plan allows sequencing hello failover of various tiers in a multi-tier application, hence, maintaining application consistency.</span></span> <span data-ttu-id="c0448-156">다중 계층 웹 응용 프로그램에 대 한 복구 계획을 만드는 동안 hello 아래 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-156">Follow hello below steps while creating a recovery plan for a multi-tier web application.</span></span>  <span data-ttu-id="c0448-157">[복구 계획 만들기에 대한 자세한 정보](./site-recovery-create-recovery-plans.md)</span><span class="sxs-lookup"><span data-stu-id="c0448-157">[Learn more about creating a recovery plan](./site-recovery-create-recovery-plans.md).</span></span>

### <a name="adding-virtual-machines-toofailover-groups"></a><span data-ttu-id="c0448-158">가상 컴퓨터 toofailover 그룹 추가</span><span class="sxs-lookup"><span data-stu-id="c0448-158">Adding virtual machines toofailover groups</span></span>
<span data-ttu-id="c0448-159">SQL 가상 컴퓨터, IIS 서버를 구성 하는 hello 웹 계층 및 응용 프로그램 계층으로 데이터베이스 계층의 일반적인 다중 계층 IIS 웹 응용 프로그램으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-159">A typical multi-tier IIS web application will consist of a database tier with SQL virtual machines, hello web tier constituted by a IIS server and an application tier.</span></span> <span data-ttu-id="c0448-160">아래 계층에 따라 이러한 모든 가상 컴퓨터 toodifferent 그룹을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-160">Add all these virtual machines toodifferent group based on tier as below.</span></span> <span data-ttu-id="c0448-161">[복구 계획 사용자 지정에 대한 자세한 정보](site-recovery-runbook-automation.md#customize-the-recovery-plan)</span><span class="sxs-lookup"><span data-stu-id="c0448-161">[Learn more about customising recovery plan](site-recovery-runbook-automation.md#customize-the-recovery-plan).</span></span>

1. <span data-ttu-id="c0448-162">복구 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-162">Create a recovery plan.</span></span> <span data-ttu-id="c0448-163">그룹 1 tooensure은 종료 마지막를 먼저 가져온에서 hello 데이터베이스 계층 가상 컴퓨터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-163">Add hello database tier virtual machines under Group 1 tooensure that they are shutdown last and brought up first.</span></span>

1. <span data-ttu-id="c0448-164">Hello 데이터베이스 계층 제기 된 후 전환 하기 되도록 그룹 2에서 hello 응용 프로그램 계층 가상 컴퓨터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-164">Add hello application tier virtual machines under Group 2 such that they are brought up after hello database tier has been brought up.</span></span>

1. <span data-ttu-id="c0448-165">Hello 응용 프로그램 계층 제기 된 후 전환 하기 되도록 그룹 3의 hello 웹 계층 가상 컴퓨터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-165">Add hello web tier virtual machines in Group 3 such that they are brought up after hello application tier has been brought up.</span></span>

1. <span data-ttu-id="c0448-166">제기 된 hello 웹 계층 제기 된 후 해당 가상 컴퓨터 부하 분산: 그룹 4에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-166">Add load balance virtual machines in Group 4 such that they are brought up after hello web tier has been brought up.</span></span>


### <a name="adding-scripts-toohello-recovery-plan"></a><span data-ttu-id="c0448-167">Toohello 복구 계획 스크립트 추가</span><span class="sxs-lookup"><span data-stu-id="c0448-167">Adding scripts toohello recovery plan</span></span>
<span data-ttu-id="c0448-168">해야 toodo hello Azure 가상 컴퓨터 사후 장애 조치/테스트 장애 조치 toomake IIS 웹 팜 함수에 대 한 일부 작업 정확 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-168">You may need toodo some operations on hello Azure virtual machines post failover/Test failover toomake IIS web farm function correctly.</span></span> <span data-ttu-id="c0448-169">사이트 바인딩을 변경 DNS 항목을 업데이트와 같은 hello post 장애 조치 작업을 자동화, 아래와 같이 hello 복구 계획에서 해당 스크립트를 추가 하 여 연결 문자열에서 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-169">You can automate hello post failover operation like updating DNS entry, changing site binding, change  in connection string  by adding corresponding scripts in hello recovery plan as below.</span></span> <span data-ttu-id="c0448-170">[복구 계획에 스크립트 추가에 대한 자세한 정보](./site-recovery-create-recovery-plans.md#add-scripts)</span><span class="sxs-lookup"><span data-stu-id="c0448-170">[Learn more about add script recovery plan](./site-recovery-create-recovery-plans.md#add-scripts).</span></span>

#### <a name="dns-update"></a><span data-ttu-id="c0448-171">DNS 업데이트</span><span class="sxs-lookup"><span data-stu-id="c0448-171">DNS Update</span></span>
<span data-ttu-id="c0448-172">Hello DNS 동적 DNS 업데이트 한 후 가상 컴퓨터에 대 한 일반적으로 구성 된 경우는 시작 되 면 hello 새 ip hello DNS를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-172">If hello DNS is configured for dynamic DNS update then virtual machines usually update hello DNS with hello new IP once they start.</span></span> <span data-ttu-id="c0448-173">Tooadd 명시적 단계 tooupdate DNS hello로 새 hello 가상 컴퓨터의 Ip 다음 추가이 [DNS에 IP tooupdate 스크립트](https://aka.ms/asr-dns-update) 복구 계획 그룹에 대 한 게시 작업으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-173">If you want tooadd an explicit step tooupdate DNS with hello new IPs of hello virtual machines then add this [script tooupdate IP in DNS](https://aka.ms/asr-dns-update) as a post action on recovery plan groups.</span></span>  

#### <a name="connection-string-in-an-applications-webconfig"></a><span data-ttu-id="c0448-174">응용 프로그램의 web.config에 있는 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="c0448-174">Connection string in an application’s web.config</span></span>
<span data-ttu-id="c0448-175">연결 문자열 hello와 통신 하는 웹 사이트를 hello hello 데이터베이스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-175">hello connection string specifies hello database that hello web site communicates with.</span></span>

<span data-ttu-id="c0448-176">연결 문자열 hello hello 데이터베이스 가상 컴퓨터의 hello 이름, 추가 단계가 필요한 사후 장애 조치 됩니다 생기고 hello 응용 프로그램은 수 tooautomatically toohello DB 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-176">If hello connection string carries hello name of hello database virtual machine, no further steps will be needed post failover and hello application will be able tooautomatically communicate toohello DB.</span></span> <span data-ttu-id="c0448-177">또한 hello 데이터베이스 가상 컴퓨터에 대 한 IP 주소 hello 유지 되는지 않을 tooupdate hello 연결 문자열이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-177">Also, if hello IP address for hello database virtual machine is retained, it will not be needed tooupdate hello connection string.</span></span> <span data-ttu-id="c0448-178">Hello 연결 문자열은 toohello 데이터베이스 가상 컴퓨터 IP 주소를 사용 하 여을 참조 하는 경우 업데이트 toobe 사후 장애 조치를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-178">If hello connection string refers toohello database virtual machine using an IP address, it will need toobe updated post failover.</span></span> <span data-ttu-id="c0448-179">예:</span><span class="sxs-lookup"><span data-stu-id="c0448-179">E.g.</span></span> <span data-ttu-id="c0448-180">연결 문자열 아래 hello 가리키는 toohello ip 127.0.1.2 DB</span><span class="sxs-lookup"><span data-stu-id="c0448-180">hello below connection string points toohello DB with IP 127.0.1.2</span></span>

        <?xml version="1.0" encoding="utf-8"?>
        <configuration>
        <connectionStrings>
        <add name="ConnStringDb1" connectionString="Data Source= 127.0.1.2\SqlExpress; Initial Catalog=TestDB1;Integrated Security=False;" />
        </connectionStrings>
        </configuration>

<span data-ttu-id="c0448-181">추가 하 여 웹 계층의 hello 연결 문자열을 업데이트할 수 있습니다 [IIS 연결 업데이트 스크립트](https://aka.ms/asr-update-webtier-script-classic) hello 복구 계획에 그룹 3 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-181">You can update hello connection string in web tier by adding [IIS connection update script](https://aka.ms/asr-update-webtier-script-classic) after Group 3 in hello recovery plan.</span></span>

#### <a name="site-bindings-for-hello-application"></a><span data-ttu-id="c0448-182">Hello 응용 프로그램에 대 한 사이트 바인딩</span><span class="sxs-lookup"><span data-stu-id="c0448-182">Site bindings for hello application</span></span>
<span data-ttu-id="c0448-183">모든 사이트 hello 형식의 바인딩 포함 하는 정보, hello IP 주소는 hello IIS 서버 hello 사이트, hello 포트 번호 및 hello 사이트에 대 한 호스트 이름을 hello에 대 한 toohello 요청 수신 바인딩 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-183">Every site consists of binding information that includes hello type of binding, hello IP address at which hello IIS server listens toohello requests for hello site, hello port number and hello host names for hello site.</span></span> <span data-ttu-id="c0448-184">장애 조치의 hello 시 이러한 바인딩은 toobe 연관 hello IP 주소에 변경 될 경우 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-184">At hello time of a failover, these bindings might need toobe updated if there is a change in hello IP address associated with them.</span></span>

> [!NOTE]
>
> <span data-ttu-id="c0448-185">'All unassigned' hello 예제 아래와 같이 hello 사이트 바인딩에 대 한 표시 필요가 없습니다 tooupdate이 바인딩 사후 장애 조치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-185">If you have marked ‘all unassigned’ for hello site binding as in hello example below, you will not need tooupdate this binding post failover.</span></span> <span data-ttu-id="c0448-186">또한, 장애 조치 hello IP 주소는 사이트와 연결 된 후 변경 되지 않은 경우 hello 사이트 바인딩이 필요 업데이트할 수 (hello 네트워크 아키텍처에 따라 달라 집니다 hello IP 주소의 보존 및 서브넷 toohello 기본 및 복구 사이트를 할당 하 고 따라서 이거나 아닐 가능 하면 조직용.)</span><span class="sxs-lookup"><span data-stu-id="c0448-186">Also, if hello IP address associated with a site is not changed post failover, hello site binding need not be updated (Retention of hello IP address depends on hello network architecture and subnets assigned toohello primary and recovery sites and hence may or may not be feasible for your organization.)</span></span>

![SSL 바인딩](./media/site-recovery-iis/sslbinding.png)

<span data-ttu-id="c0448-188">사이트 hello IP 주소 연관 hello 새 IP 주소를 가진 모든 사이트 바인딩 tooupdate 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-188">If you have associated hello IP address with a site, you will need tooupdate all site bindings with hello new IP address.</span></span> <span data-ttu-id="c0448-189">추가할 수 있습니다 [IIS 웹 계층 업데이트 스크립트](https://aka.ms/asr-web-tier-update-runbook-classic) 후 복구 계획 toochange hello 사이트 바인딩에서 그룹 3입니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-189">You can add [IIS Web tier update script](https://aka.ms/asr-web-tier-update-runbook-classic) after Group 3 in recovery plan toochange hello site bindings.</span></span>


#### <a name="update-load-balancer-ip-address"></a><span data-ttu-id="c0448-190">부하 분산 장치 IP 주소 업데이트</span><span class="sxs-lookup"><span data-stu-id="c0448-190">Update load balancer IP address</span></span>
<span data-ttu-id="c0448-191">응용 프로그램 요청 라우팅 가상 컴퓨터를 사용 하는 경우 추가 [IIS ARR 장애 조치 스크립트](https://aka.ms/asr-iis-arrtier-failover-script-classic) 후: 그룹 4 tooupdate hello IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-191">If you have  Application Request Routing virtual machine, add [IIS ARR  failover script](https://aka.ms/asr-iis-arrtier-failover-script-classic) after Group 4 tooupdate hello IP address.</span></span>

#### <a name="hello-ssl-cert-binding-for-an-https-connection"></a><span data-ttu-id="c0448-192">https 연결에 대 한 hello SSL 인증서 바인딩</span><span class="sxs-lookup"><span data-stu-id="c0448-192">hello SSL cert binding for an https connection</span></span>
<span data-ttu-id="c0448-193">웹 사이트에서 웹 서버 hello hello 사용자의 브라우저 간의 보안 통신을 보장 하는 데 도움이 되는 관련된 SSL 인증서를 개뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-193">Websites can have an associated SSL certificate that helps in ensuring a secure communication between hello webserver and hello user’s browser.</span></span> <span data-ttu-id="c0448-194">Hello 웹 사이트에 https 연결 및 SSL 인증서 바인딩과 함께 hello IIS 서버의 연결된 https 사이트 바인딩 toohello IP 주소, 새 사이트 바인딩을 toobe hello IIS 가상 컴퓨터의 IP 사후 장애 조치 hello로 hello 인증서에 대 한 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-194">If hello website has an https connection and an associated https site binding toohello IP address of hello IIS server with an SSL cert binding, a new site binding will need toobe added for hello cert with hello IP of hello IIS virtual machine post failover.</span></span>

<span data-ttu-id="c0448-195">hello SSL 인증서에 대해 실행 될 수 있습니다-</span><span class="sxs-lookup"><span data-stu-id="c0448-195">hello SSL cert can be issued against-</span></span>

<span data-ttu-id="c0448-196">hello 웹 사이트의 a) hello 정규화 된 도메인 이름</span><span class="sxs-lookup"><span data-stu-id="c0448-196">a) hello fully qualified domain name of hello website</span></span><br>
<span data-ttu-id="c0448-197">hello 서버 b) hello 이름</span><span class="sxs-lookup"><span data-stu-id="c0448-197">b) hello name of hello server</span></span><br>
<span data-ttu-id="c0448-198">c) hello 도메인 이름에 대 한 와일드 카드 인증서</span><span class="sxs-lookup"><span data-stu-id="c0448-198">c) A wildcard certificate for hello domain name</span></span><br>
<span data-ttu-id="c0448-199">d)는 IP 주소-hello SSL 인증서의 hello IIS 서버 hello IP에 대해 실행 될 다른 SSL 인증서 요구 toobe hello Azure 사이트에서 IIS 서버 hello의 hello IP 주소에 대해 발급 하 고이 인증서에 대해 추가 SSL 바인딩을 만든 toobe 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-199">d) An IP address – If hello SSL cert is issued against hello IP of hello IIS server, another SSL cert needs toobe issued against hello IP address of hello IIS server on hello Azure site and an additional SSL binding for this certificate will need toobe created.</span></span> <span data-ttu-id="c0448-200">따라서, 좋습니다 toonot 사용 하 여 IP에 대해 발급 된 SSL 인증서를입니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-200">Hence, it is advisable toonot use an SSL cert issued against IP.</span></span> <span data-ttu-id="c0448-201">이는 널리 사용되지 않는 옵션이며, CA/브라우저 포럼의 새로운 변경 내용에 따라 곧 사용되지 않을 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-201">This is a less widely used option and will soon be deprecated as per new CA/browser forum changes.</span></span>

#### <a name="update-hello-dependency-between-hello-web-and-hello-application-tier"></a><span data-ttu-id="c0448-202">Hello 웹과 hello 응용 프로그램 계층 간 업데이트 hello 종속성</span><span class="sxs-lookup"><span data-stu-id="c0448-202">Update hello dependency between hello web and hello application tier</span></span>
<span data-ttu-id="c0448-203">Hello 가상 컴퓨터의 hello IP 주소에 따라 응용 프로그램 특정 종속성이 있으면이 종속성 사후 장애 조치 tooupdate 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-203">If you have an application specific dependency based on hello IP address of hello virtual machines, you need tooupdate this dependency post failover.</span></span>

## <a name="doing-a-test-failover"></a><span data-ttu-id="c0448-204">테스트 장애 조치 수행</span><span class="sxs-lookup"><span data-stu-id="c0448-204">Doing a test failover</span></span>
<span data-ttu-id="c0448-205">에 따라 [이 지침은](site-recovery-test-failover-to-azure.md) toodo 테스트 장애 조치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-205">Follow [this guidance](site-recovery-test-failover-to-azure.md) toodo a test failover.</span></span>

1.  <span data-ttu-id="c0448-206">TooAzure 포털 이동한 다음 복구 서비스 자격 증명 모음을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-206">Go tooAzure portal and select your Recovery Service vault.</span></span>
1.  <span data-ttu-id="c0448-207">IIS 웹 팜에 대해 만든 hello 복구 계획을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-207">Click on hello recovery plan created for IIS web farm.</span></span>
1.  <span data-ttu-id="c0448-208">'테스트 장애 조치'를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-208">Click on 'Test Failover'.</span></span>
1.  <span data-ttu-id="c0448-209">복구 지점 및 Azure 가상 네트워크 toostart hello 테스트 장애 조치 프로세스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-209">Select recovery point and Azure virtual network toostart hello test failover process.</span></span>
1.  <span data-ttu-id="c0448-210">Hello 보조 환경의 되 면 사용자 유효성 검사를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-210">Once hello secondary environment is up, you can perform your validations.</span></span>
1.  <span data-ttu-id="c0448-211">Hello 유효성 검사가 완료 되 면 유효성 검사 완료를 선택할 수 있습니다 및 hello 테스트 장애 조치 환경을 정리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-211">Once hello validations are complete, you can select ‘Validations complete’ and hello test failover environment will be cleaned.</span></span>

## <a name="doing-a-failover"></a><span data-ttu-id="c0448-212">장애 조치 수행</span><span class="sxs-lookup"><span data-stu-id="c0448-212">Doing a failover</span></span>
<span data-ttu-id="c0448-213">장애 조치를 수행할 때 [이 지침](site-recovery-failover.md)을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-213">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

1.  <span data-ttu-id="c0448-214">TooAzure 포털 이동한 다음 복구 서비스 자격 증명 모음을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-214">Go tooAzure portal and select your Recovery Service vault.</span></span>
1.  <span data-ttu-id="c0448-215">IIS 웹 팜에 대해 만든 hello 복구 계획을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-215">Click on hello recovery plan created for IIS web farm.</span></span>
1.  <span data-ttu-id="c0448-216">'장애 조치'를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-216">Click on 'Failover'.</span></span>
1.  <span data-ttu-id="c0448-217">복구 지점 toostart hello 장애 조치 프로세스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-217">Select recovery point toostart hello failover process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0448-218">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c0448-218">Next steps</span></span>
<span data-ttu-id="c0448-219">Site Recovery를 사용하여 [다른 응용 프로그램을 복제하는 방법](site-recovery-workload.md)에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0448-219">You can learn more about [replicate other applications](site-recovery-workload.md) using Site Recovery.</span></span>
