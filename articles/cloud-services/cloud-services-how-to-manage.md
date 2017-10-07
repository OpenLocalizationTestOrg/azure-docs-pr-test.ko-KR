---
title: "aaaCommon 클라우드 서비스 관리 작업 (클래식) | Microsoft Docs"
description: "Hello Azure 클래식 포털에서에서 toomanage 클라우드 서비스 하는 방법에 대해 알아봅니다."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 41a30e50-067c-485b-96fd-434a6d057abc
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 03b1d632f1480d0f65c87b7f8ffc747417acf7b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-cloud-services"></a><span data-ttu-id="58e7a-103">TooManage 클라우드 서비스 하는 방법</span><span class="sxs-lookup"><span data-stu-id="58e7a-103">How tooManage Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="58e7a-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="58e7a-104">Azure portal</span></span>](cloud-services-how-to-manage-portal.md)
> * [<span data-ttu-id="58e7a-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="58e7a-105">Azure classic portal</span></span>](cloud-services-how-to-manage.md)
>
>

<span data-ttu-id="58e7a-106">Hello에 **클라우드 서비스** 부문의 문제 hello Azure 클래식 포털에서 있습니다 수 서비스 역할 또는 배포 업데이트, 준비 된 배포 tooproduction 승격, hello 리소스를 볼 수 있도록 리소스 tooyour 클라우드 서비스에 연결 종속성 및 배율에는 리소스를 함께 hello 및 클라우드 서비스 또는 배포를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-106">In hello **Cloud Services** area of hello Azure classic portal, you can update a service role or a deployment, promote a staged deployment tooproduction, link resources tooyour cloud service so that you can see hello resource dependencies and scale hello resources together, and delete a cloud service or a deployment.</span></span>

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a><span data-ttu-id="58e7a-107">방법: 클라우드 서비스 역할 또는 배포 업데이트</span><span class="sxs-lookup"><span data-stu-id="58e7a-107">How to: Update a cloud service role or deployment</span></span>
<span data-ttu-id="58e7a-108">클라우드 서비스에 대 한 tooupdate hello 응용 프로그램 코드를 필요 사용 **업데이트** hello 대시보드에서 **클라우드 서비스** 페이지 또는 **인스턴스** 페이지.</span><span class="sxs-lookup"><span data-stu-id="58e7a-108">If you need tooupdate hello application code for your cloud service, use **Update** on hello dashboard, **Cloud Services** page, or **Instances** page.</span></span> <span data-ttu-id="58e7a-109">단일 역할이나 모든 역할을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-109">You can update a single role or all roles.</span></span> <span data-ttu-id="58e7a-110">Tooupload 새 서비스 패키지 및 서비스 구성 파일이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-110">You'll need tooupload a new service package and service configuration file.</span></span>

1. <span data-ttu-id="58e7a-111">Hello에 [Azure 클래식 포털](https://manage.windowsazure.com/), hello 대시보드에서 **클라우드 서비스** 페이지 또는 **인스턴스** 페이지 **업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-111">In hello [Azure classic portal](https://manage.windowsazure.com/), on hello dashboard, **Cloud Services** page, or **Instances** page, click **Update**.</span></span>

    ![배포 업데이트](./media/cloud-services-how-to-manage/CloudServices_UpdateDeployment.png)

2. <span data-ttu-id="58e7a-113">**배포 레이블**, 이름 tooidentify hello 배포 (예를 들어 mycloudservice4)을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-113">In **Deployment label**, enter a name tooidentify hello deployment (for example, mycloudservice4).</span></span> <span data-ttu-id="58e7a-114">배포 레이블 hello 있습니다 **퀵 스타트** hello 대시보드에서.</span><span class="sxs-lookup"><span data-stu-id="58e7a-114">You'll find hello deployment label under **quick start** on hello dashboard.</span></span>
3. <span data-ttu-id="58e7a-115">**패키지**를 사용 하 여 **찾아보기** tooupload hello 서비스 패키지 파일 (.cspkg).</span><span class="sxs-lookup"><span data-stu-id="58e7a-115">In **Package**, use **Browse** tooupload hello service package file (.cspkg).</span></span>
4. <span data-ttu-id="58e7a-116">**구성**를 사용 하 여 **찾아보기** tooupload hello 서비스 구성 파일 (.cscfg).</span><span class="sxs-lookup"><span data-stu-id="58e7a-116">In **Configuration**, use **Browse** tooupload hello service configuration file (.cscfg).</span></span>
5. <span data-ttu-id="58e7a-117">**역할**선택, **모든** hello에 있는 모든 역할이 클라우드 서비스 tooupgrade 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="58e7a-117">In **Role**, select **All** if you want tooupgrade all roles in hello cloud service.</span></span> <span data-ttu-id="58e7a-118">tooperform 단일 역할 업데이트 tooupdate 선택 hello 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-118">tooperform a single role update, select hello role you want tooupdate.</span></span> <span data-ttu-id="58e7a-119">특정 역할 tooupdate 선택 하는 경우에 hello 업데이트 hello 서비스 구성 파일에는 적용 된 tooall 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-119">Even if you select a specific role tooupdate, hello updates in hello service configuration file are applied tooall roles.</span></span>
6. <span data-ttu-id="58e7a-120">Hello 업데이트 변경 내용을 모든 역할의 hello 크기나 역할 수가 hello, hello 선택 **역할 크기나 역할 수가 변경 되 면 업데이트의 허용** 확인란 tooenable hello 업데이트 tooproceed 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-120">If hello update changes hello number of roles or hello size of any role, select hello **Allow update if role sizes or number of roles changes** check box tooenable hello update tooproceed.</span></span>

    <span data-ttu-id="58e7a-121">업그레이드할 역할 (즉, 역할 인스턴스를 호스팅하는 가상 컴퓨터의 hello 크기)의 hello 크기를 변경 하거나 역할 수가 hello 경우 각 역할 인스턴스 (가상 컴퓨터)은 이미지로 다시 설치 된 있어야 합니다. 모든 로컬 데이터가 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-121">Be aware that if you change hello size of a role (that is, hello size of a virtual machine that hosts a role instance) or hello number of roles, each role instance (virtual machine) must be re-imaged, and any local data will be lost.</span></span>

7. <span data-ttu-id="58e7a-122">모든 서비스 역할이 역할 인스턴스가 하나만 있는 경우 선택 hello **하나 이상의 역할에는 단일 인스턴스 확인란이 포함 하는 경우에 업데이트** tooenable hello 업그레이드 tooproceed 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-122">If any service roles have only one role instance, select hello **Update even if one or more role contain a single instance check box** tooenable hello upgrade tooproceed.</span></span>

    <span data-ttu-id="58e7a-123">Azure는 각 역할에 둘 이상의 역할 인스턴스(가상 컴퓨터)가 있는 경우에만 클라우드 서비스 업데이트 중 99.95%의 서비스 가용성을 보장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-123">Azure can only guarantee 99.95 percent service availability during a cloud service update if each role has at least two role instances (virtual machines).</span></span> <span data-ttu-id="58e7a-124">수 있도록 하나 가상 컴퓨터 tooprocess 클라이언트 요청 다른 hello를 업데이트 하는 동안 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-124">That enables one virtual machine tooprocess client requests while hello other is being updated.</span></span>

8. <span data-ttu-id="58e7a-125">클릭 **확인** (확인 표시) toobegin hello 서비스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-125">Click **OK** (checkmark) toobegin updating hello service.</span></span>

## <a name="how-to-swap-deployments-toopromote-a-staged-deployment-tooproduction"></a><span data-ttu-id="58e7a-126">방법: 준비 된 배포 tooproduction 배포 toopromote 교체</span><span class="sxs-lookup"><span data-stu-id="58e7a-126">How to: Swap deployments toopromote a staged deployment tooproduction</span></span>
<span data-ttu-id="58e7a-127">사용 하 여 **교체** toopromote 클라우드 서비스 tooproduction의 스테이징 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-127">Use **Swap** toopromote a staging deployment of a cloud service tooproduction.</span></span> <span data-ttu-id="58e7a-128">Toodeploy 클라우드 서비스의 새 릴리스를 결정할 때 단계 하 고 고객이 프로덕션 환경에서 현재 릴리스 hello를 사용 하는 동안 클라우드 서비스가 스테이징 환경에 새 릴리스를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-128">When you decide toodeploy a new release of a cloud service, you can stage and test your new release in your cloud service staging environment while your customers are using hello current release in production.</span></span> <span data-ttu-id="58e7a-129">준비가 끝나면 toopromote 새 릴리스 tooproduction hello를 사용할 수 있습니다 **교체** tooswitch hello Url는 hello 하 여 두 배포의 주소로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-129">When you're ready toopromote hello new release tooproduction, you can use **Swap** tooswitch hello URLs by which hello two deployments are addressed.</span></span>

<span data-ttu-id="58e7a-130">Hello에서 배포를 스왑할 수 **클라우드 서비스** 페이지나 hello 대시보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-130">You can swap deployments from hello **Cloud Services** page or hello dashboard.</span></span>

1. <span data-ttu-id="58e7a-131">Hello에 [Azure 클래식 포털](https://manage.windowsazure.com/), 클릭 **클라우드 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-131">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**.</span></span>
2. <span data-ttu-id="58e7a-132">클라우드 서비스의 hello 목록에서 클릭 hello 클라우드 서비스 tooselect 것입니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-132">In hello list of cloud services, click hello cloud service tooselect it.</span></span>
3. <span data-ttu-id="58e7a-133">**교환**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-133">Click **Swap**.</span></span>

    <span data-ttu-id="58e7a-134">hello 다음과 같은 확인 프롬프트가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-134">hello following confirmation prompt opens.</span></span>

    ![클라우드 서비스 교환](./media/cloud-services-how-to-manage/CloudServices_Swap.png)

4. <span data-ttu-id="58e7a-136">Hello 배포 정보를 확인 한 후 클릭 **예** tooswap hello 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-136">After you verify hello deployment information, click **Yes** tooswap hello deployments.</span></span>

    <span data-ttu-id="58e7a-137">hello 배포 스왑 발생 신속 하 게 변경 하는 hello 유일한 항목은 hello 가상 IP 주소 (Vip) hello 배포에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-137">hello deployment swap happens quickly because hello only thing that changes is hello virtual IP addresses (VIPs) for hello deployments.</span></span>

    <span data-ttu-id="58e7a-138">toosave 계산 비용이 hello hello 새 프로덕션 배포 예상 대로 작동 확인 되 면 스테이징 환경에에서 hello 배포를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-138">toosave compute costs, you can delete hello deployment in hello staging environment when you're sure hello new production deployment is performing as expected.</span></span>

### <a name="common-questions-about-swapping-deployments"></a><span data-ttu-id="58e7a-139">배포 교환에 대한 일반적인 질문</span><span class="sxs-lookup"><span data-stu-id="58e7a-139">Common questions about swapping deployments</span></span>

<span data-ttu-id="58e7a-140">**Hello 필수 구성 요소 배포를 교환 하는 무엇입니까?**</span><span class="sxs-lookup"><span data-stu-id="58e7a-140">**What are hello prerequisites for swapping deployments?**</span></span>

<span data-ttu-id="58e7a-141">성공적인 배포 교환을 위한 2가지 핵심 필수 조건은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-141">There are two key prerequisites for a successful deployment swap:</span></span>

- <span data-ttu-id="58e7a-142">프로덕션 슬롯에 대 한 고정 IP 주소를 toouse 하려는 경우에 프로그램 스테이징 슬롯에 대 한를 예약 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-142">If you would like toouse a static IP address for your production slot, you must reserve one for your staging slot as well.</span></span> <span data-ttu-id="58e7a-143">그렇지 않으면 hello 스왑 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-143">Otherwise, hello swap will fail.</span></span>

- <span data-ttu-id="58e7a-144">Hello 교체를 수행 하기 전에 역할의 모든 인스턴스를 실행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-144">All instances of your roles must be running before you can perform hello swap.</span></span> <span data-ttu-id="58e7a-145">Hello Azure 클래식 포털에서에서 또는 사용 하 여 인스턴스의 hello 상태를 확인할 수 [Get-azurerole 명령을 Windows PowerShell의 hello](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0)합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-145">You can check hello status of your instances in hello Azure classic portal or by using [hello Get-AzureRole command in Windows PowerShell](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0).</span></span>

<span data-ttu-id="58e7a-146">게스트 OS 업데이트 및 서비스 작업을 복구 배포 발생할 수 있습니다 참고 toofail을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-146">Note that guest OS updates and service healing operations can also cause deployment swaps toofail.</span></span> <span data-ttu-id="58e7a-147">자세한 내용은 [클라우드 서비스 배포 문제 해결](cloud-services-troubleshoot-deployment-problems.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="58e7a-147">See [Troubleshoot cloud service deployment problems](cloud-services-troubleshoot-deployment-problems.md) for more details.</span></span>

<span data-ttu-id="58e7a-148">**교체 시 응용 프로그램 가동 중지가 발생할 수 있습니까? 어떻게 처리해야 합니까?**</span><span class="sxs-lookup"><span data-stu-id="58e7a-148">**Does a swap incur downtime for my application? How should I handle it?**</span></span>

<span data-ttu-id="58e7a-149">Hello 마지막 섹션에서 설명한 배포 스왑 일반적으로 매우 빠릅니다 hello Azure 부하 분산 장치에 구성 변경에 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-149">As described in hello last section, a deployment swap is typically very fast since it is just a configuration change in hello Azure load balancer.</span></span> <span data-ttu-id="58e7a-150">그러나 경우에 따라 10초 이상 걸리며 일시적인 연결 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-150">In some cases, however, it can take ten or more seconds and result in transient connection failures.</span></span> <span data-ttu-id="58e7a-151">toolimit 영향 tooyour 고객 구현을 고려할 [클라이언트 다시 시도 논리](../best-practices-retry-general.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-151">toolimit impact tooyour customers, consider implementing [client retry logic](../best-practices-retry-general.md).</span></span>

## <a name="how-to-link-a-resource-tooa-cloud-service"></a><span data-ttu-id="58e7a-152">방법: 리소스 tooa 클라우드 서비스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-152">How to: Link a resource tooa cloud service</span></span>
<span data-ttu-id="58e7a-153">tooshow 클라우드 서비스의 종속성 다른 리소스에 저장소 계정 toohello 클라우드 서비스 또는 Azure SQL 데이터베이스 인스턴스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-153">tooshow your cloud service's dependencies on other resources, you can link an Azure SQL Database instance or a storage account toohello cloud service.</span></span> <span data-ttu-id="58e7a-154">에 연결 하 고 hello에 리소스 연결을 해제 **연결 된 리소스** 페이지를 선택한 다음의 사용 현황을 hello 클라우드 서비스 대시보드에서 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-154">You can link and unlink resources on hello **Linked Resources** page, and then monitor their usage on hello cloud service dashboard.</span></span> <span data-ttu-id="58e7a-155">연결 된 저장소 계정에 설정 되어 모니터링 하는 경우에 hello 클라우드 서비스 대시보드에서 총 요청 수를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-155">If a linked storage account has monitoring turned on, you can monitor Total Requests on hello cloud service dashboard.</span></span>

<span data-ttu-id="58e7a-156">사용 하 여 **링크** toolink 기존 또는 새 SQL 데이터베이스 인스턴스나 저장소 계정 tooyour 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-156">Use **Link** toolink a new or existing SQL Database instance or storage account tooyour cloud service.</span></span> <span data-ttu-id="58e7a-157">hello를 사용 하는 hello 클라우드 서비스 역할과 함께 hello 데이터베이스를 확장할 수 있습니다 **배율** 페이지.</span><span class="sxs-lookup"><span data-stu-id="58e7a-157">You can then scale hello database along with hello cloud service role that is using it on hello **Scale** page.</span></span> <span data-ttu-id="58e7a-158">(저장소 계정은 사용량이 늘어나면 자동으로 확장됩니다.) 자세한 내용은 참조 [어떻게 tooScale 클라우드 서비스와 연결 된 리소스](cloud-services-how-to-scale.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-158">(A storage account scales automatically as usage increases.) For more information, see [How tooScale a Cloud Service and Linked Resources](cloud-services-how-to-scale.md).</span></span>

<span data-ttu-id="58e7a-159">모니터링, 관리 하 고 수도 있습니다 hello로 hello 데이터베이스 크기를 조정 **데이터베이스** hello Azure 클래식 포털의 노드.</span><span class="sxs-lookup"><span data-stu-id="58e7a-159">You also can monitor, manage, and scale hello database in hello **Databases** node of hello Azure classic portal.</span></span>

<span data-ttu-id="58e7a-160">이런이 의미에서 리소스를 "연결" 응용 프로그램 toohello 리소스를 연결 되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-160">"Linking" a resource in this sense doesn't connect your app toohello resource.</span></span> <span data-ttu-id="58e7a-161">사용 하 여 새 데이터베이스를 만드는 경우 **링크**, tooadd hello 연결 문자열 tooyour 응용 프로그램 코드와 다음 업그레이드 hello 클라우드 서비스가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-161">If you create a new database using **Link**, you'll need tooadd hello connection strings tooyour application code and then upgrade hello cloud service.</span></span> <span data-ttu-id="58e7a-162">응용 프로그램 연결 된 저장소 계정에 리소스를 사용 하는 경우에 tooadd 연결 문자열 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-162">You'll also need tooadd connection strings if your app uses resources in a linked storage account.</span></span>

<span data-ttu-id="58e7a-163">절차를 수행 하는 hello toolink 새 SQL 데이터베이스 인스턴스를 배포 방법 새 SQL 데이터베이스 서버, tooa 클라우드 서비스에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-163">hello following procedure describes how toolink a new SQL Database instance, deployed on a new SQL Database server, tooa cloud service.</span></span>

### <a name="toolink-a-sql-database-instance-tooa-cloud-service"></a><span data-ttu-id="58e7a-164">toolink SQL 데이터베이스 인스턴스 tooa 클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="58e7a-164">toolink a SQL Database instance tooa cloud service</span></span>
1. <span data-ttu-id="58e7a-165">Hello에 [Azure 클래식 포털](http://manage.windowsazure.com/), 클릭 **클라우드 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-165">In hello [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**.</span></span> <span data-ttu-id="58e7a-166">Hello 클라우드 서비스 tooopen hello 대시보드의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-166">Then click hello name of hello cloud service tooopen hello dashboard.</span></span>
2. <span data-ttu-id="58e7a-167">**연결된 리소스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-167">Click **Linked Resources**.</span></span>

    <span data-ttu-id="58e7a-168">hello **연결 된 리소스** 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-168">hello **Linked Resources** page opens.</span></span>

    ![연결된 리소스 페이지](./media/cloud-services-how-to-manage/CloudServices_LinkedResourcesPage.png)

3. <span data-ttu-id="58e7a-170">**연결된 리소스** 또는 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-170">Click either **Link a Resource** or **Link**.</span></span>

    <span data-ttu-id="58e7a-171">hello **링크 리소스** 마법사가 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-171">hello **Link Resource** wizard starts.</span></span>

    ![연결 페이지1](./media/cloud-services-how-to-manage/CloudServices_LinkedResources_LinkPage1.png)

4. <span data-ttu-id="58e7a-173">**새 리소스 만들기** 또는 **기존 리소스에 연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-173">Click **Create a new resource** or **Link an existing resource**.</span></span>
5. <span data-ttu-id="58e7a-174">리소스 toolink hello 형식을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-174">Choose hello type of resource toolink.</span></span> <span data-ttu-id="58e7a-175">Hello에 [Azure 클래식 포털](http://manage.windowsazure.com/), 클릭 **SQL 데이터베이스**합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-175">In hello [Azure classic portal](http://manage.windowsazure.com/), click **SQL Database**.</span></span> <span data-ttu-id="58e7a-176">(Hello Azure 클래식 포털 지원 저장소 계정 tooa 클라우드 서비스를 연결 합니다.)</span><span class="sxs-lookup"><span data-stu-id="58e7a-176">(Only hello Azure classic portal supports linking a storage account tooa cloud service.)</span></span>
6. <span data-ttu-id="58e7a-177">toocomplete hello 데이터베이스 구성이 hello에 대 한 도움말의 지침에 따라 **SQL 데이터베이스** hello Azure 클래식 포털의 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-177">toocomplete hello database configuration, follow instructions in help for hello **SQL Databases** area of hello Azure classic portal.</span></span>

    <span data-ttu-id="58e7a-178">Hello 연결 hello 메시지 영역에는 작업의 hello 진행률을 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-178">You can follow hello progress of hello linking operation in hello message area.</span></span>

    <span data-ttu-id="58e7a-179">연결 완료 되 면 hello 클라우드 서비스 대시보드에서 hello 연결 된 리소스의 hello 상태를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-179">When linking is complete, you can monitor hello status of hello linked resource on hello cloud service dashboard.</span></span> <span data-ttu-id="58e7a-180">연결 된 SQL 데이터베이스 확장에 대 한 정보를 참조 하십시오. [어떻게 tooScale 클라우드 서비스와 연결 된 리소스](cloud-services-how-to-scale.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-180">For information about scaling a linked SQL Database, see [How tooScale a Cloud Service and Linked Resources](cloud-services-how-to-scale.md).</span></span>

### <a name="toounlink-a-linked-resource"></a><span data-ttu-id="58e7a-181">toounlink 링크 된 리소스</span><span class="sxs-lookup"><span data-stu-id="58e7a-181">toounlink a linked resource</span></span>
1. <span data-ttu-id="58e7a-182">Hello에 [Azure 클래식 포털](http://manage.windowsazure.com/), 클릭 **클라우드 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-182">In hello [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**.</span></span> <span data-ttu-id="58e7a-183">Hello 클라우드 서비스 tooopen hello 대시보드의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-183">Then click hello name of hello cloud service tooopen hello dashboard.</span></span>
2. <span data-ttu-id="58e7a-184">클릭 **연결 된 리소스**, 한 다음 hello 리소스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-184">Click **Linked Resources**, and then select hello resource.</span></span>
3. <span data-ttu-id="58e7a-185">**연결 해제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-185">Click **Unlink**.</span></span> <span data-ttu-id="58e7a-186">클릭 **예** hello 명령 프롬프트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-186">Then click **Yes** at hello confirmation prompt.</span></span>

    <span data-ttu-id="58e7a-187">SQL 데이터베이스 연결을 해제 해도 hello 데이터베이스나 hello 응용 프로그램의 연결 toohello 데이터베이스에는 영향이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-187">Unlinking a SQL Database has no effect on hello database or hello application's connections toohello database.</span></span> <span data-ttu-id="58e7a-188">Hello에 hello 데이터베이스를 계속 관리할 수 있습니다 **SQL 데이터베이스** hello Azure 클래식 포털의 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-188">You can still manage hello database in hello **SQL Databases** area of hello Azure classic portal.</span></span>

## <a name="how-to-delete-deployments-and-a-cloud-service"></a><span data-ttu-id="58e7a-189">방법: 배포 및 클라우드 서비스 삭제</span><span class="sxs-lookup"><span data-stu-id="58e7a-189">How to: Delete deployments and a cloud service</span></span>
<span data-ttu-id="58e7a-190">클라우드 서비스를 삭제하려면 먼저 각각의 기존 배포를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-190">Before you can delete a cloud service, you must delete each existing deployment.</span></span>

<span data-ttu-id="58e7a-191">toosave 계산 비용이 프로덕션 배포 예상 대로 작동 하는지 확인 한 후 스테이징 배포를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-191">toosave compute costs, you can delete your staging deployment after you verify that your production deployment is working as expected.</span></span> <span data-ttu-id="58e7a-192">클라우드 서비스가 실행되고 있지 않은 경우에도 역할 인스턴스의 계산 비용이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-192">You are billed compute costs for role instances even if a cloud service is not running.</span></span>

<span data-ttu-id="58e7a-193">배포 또는 클라우드 서비스 프로시저 toodelete 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-193">Use hello following procedure toodelete a deployment or your cloud service.</span></span>

1. <span data-ttu-id="58e7a-194">Hello에 [Azure 클래식 포털](http://manage.windowsazure.com/), 클릭 **클라우드 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-194">In hello [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**.</span></span>
2. <span data-ttu-id="58e7a-195">Hello 클라우드 서비스를 선택한 다음 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-195">Select hello cloud service, and then click **Delete**.</span></span> <span data-ttu-id="58e7a-196">(tooselect hello 대시보드를 열지 않고 클라우드 서비스는 아무 곳 이나 클릭 hello 클라우드 서비스 항목에서 hello 이름을 제외 하 고 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="58e7a-196">(tooselect a cloud service without opening hello dashboard, click anywhere except hello name in hello cloud service entry.)</span></span>

    <span data-ttu-id="58e7a-197">스테이징 또는 프로덕션에 배포를 설정한 경우 비슷한 toohello hello hello 창 맨 아래에 하나를 선택 항목의 메뉴가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-197">If you have a deployment in staging or production, you will see a menu of choices similar toohello following one at hello bottom of hello window.</span></span> <span data-ttu-id="58e7a-198">Hello 클라우드 서비스를 삭제 하기 전에 모든 기존 배포를 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-198">Before you can delete hello cloud service, you must delete any existing deployments.</span></span>

    ![삭제 메뉴](./media/cloud-services-how-to-manage/CloudServices_DeleteMenu.png)

3. <span data-ttu-id="58e7a-200">toodelete 해당 배포를 클릭 하 여 **프로덕션 배포 삭제** 또는 **스테이징 배포 삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-200">toodelete a deployment, click **Delete production deployment** or **Delete staging deployment**.</span></span> <span data-ttu-id="58e7a-201">Hello 명령 프롬프트에서 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-201">Then, at hello confirmation prompt, click **Yes**.</span></span>
4. <span data-ttu-id="58e7a-202">Toodelete hello 클라우드 서비스를 계획 하는 경우 필요에 따라 toodelete 다른 배포 3 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-202">If you plan toodelete hello cloud service, repeat step 3, if needed, toodelete your other deployment.</span></span>
5. <span data-ttu-id="58e7a-203">toodelete hello 클라우드 서비스를 클릭 하 여 **삭제 클라우드 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-203">toodelete hello cloud service, click **Delete cloud service**.</span></span> <span data-ttu-id="58e7a-204">Hello 명령 프롬프트에서 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-204">Then, at hello confirmation prompt, click **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="58e7a-205">자세한 정보 표시 모니터링을 구성 된 경우 클라우드 서비스에 대 한 Azure hello hello 클라우드 서비스를 삭제 하면 모니터링 저장소 계정에서 데이터를 삭제 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-205">If verbose monitoring is configured for your cloud service, Azure does not delete hello monitoring data from your storage account when you delete hello cloud service.</span></span> <span data-ttu-id="58e7a-206">수동으로 toodelete hello 데이터가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-206">You will need toodelete hello data manually.</span></span> <span data-ttu-id="58e7a-207">여기서 toofind hello 메트릭 테이블에 대 한 정보를 참조 하십시오. "하는 방법: hello Azure 클래식 포털 외부 자세한 정보 표시 모니터링 데이터에 액세스"에서 [tooMonitor 클라우드 서비스 방법](cloud-services-how-to-monitor.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-207">For information about where toofind hello metrics tables, see "How to: Access verbose monitoring data outside hello Azure classic portal" in [How tooMonitor Cloud Services](cloud-services-how-to-monitor.md).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="58e7a-208">다음 단계</span><span class="sxs-lookup"><span data-stu-id="58e7a-208">Next steps</span></span>
* <span data-ttu-id="58e7a-209">[클라우드 서비스의 일반 구성](cloud-services-how-to-configure.md)</span><span class="sxs-lookup"><span data-stu-id="58e7a-209">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="58e7a-210">너무 방법에 대해 알아봅니다[클라우드 서비스 배포](cloud-services-how-to-create-deploy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="58e7a-210">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="58e7a-211">[사용자 지정 도메인 이름](cloud-services-custom-domain-name.md)구성</span><span class="sxs-lookup"><span data-stu-id="58e7a-211">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="58e7a-212">[SSL 인증서](cloud-services-configure-ssl-certificate.md)구성</span><span class="sxs-lookup"><span data-stu-id="58e7a-212">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span></span>
