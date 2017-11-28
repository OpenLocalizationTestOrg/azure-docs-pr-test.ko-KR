---
title: "aaaCommon 클라우드 서비스 관리 작업 | Microsoft Docs"
description: "Hello Azure 포털에서에서 toomanage 클라우드 서비스 하는 방법에 대해 알아봅니다. 이러한 예제는 hello Azure 포털을 사용합니다."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: cb218ad9-77d4-4149-83db-71159c00767e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: ade8a18a7754edbaae4903230c26c009fef63ed7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-cloud-services"></a><span data-ttu-id="e1f07-104">TooManage 클라우드 서비스 하는 방법</span><span class="sxs-lookup"><span data-stu-id="e1f07-104">How tooManage Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e1f07-105">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="e1f07-105">Azure portal</span></span>](cloud-services-how-to-manage-portal.md)
> * [<span data-ttu-id="e1f07-106">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="e1f07-106">Azure classic portal</span></span>](cloud-services-how-to-manage.md)
>
>

<span data-ttu-id="e1f07-107">Hello에 **클라우드 서비스 (클래식)** 부문의 문제 hello Azure 포털에서 있습니다 수 서비스 역할 또는 배포 업데이트, 준비 된 배포 tooproduction 승격, hello 리소스를 볼 수 있도록 리소스 tooyour 클라우드 서비스에 연결 종속성 및 배율에는 리소스를 함께 hello 및 클라우드 서비스 또는 배포를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-107">In hello **Cloud Services (classic)** area of hello Azure portal, you can update a service role or a deployment, promote a staged deployment tooproduction, link resources tooyour cloud service so that you can see hello resource dependencies and scale hello resources together, and delete a cloud service or a deployment.</span></span>

<span data-ttu-id="e1f07-108">어떻게 tooscale 클라우드 서비스를 사용할 수에 대 한 자세한 내용은 [여기](cloud-services-how-to-scale-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-108">More information about how tooscale your cloud service is available [here](cloud-services-how-to-scale-portal.md).</span></span>

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a><span data-ttu-id="e1f07-109">방법: 클라우드 서비스 역할 또는 배포 업데이트</span><span class="sxs-lookup"><span data-stu-id="e1f07-109">How to: Update a cloud service role or deployment</span></span>
<span data-ttu-id="e1f07-110">클라우드 서비스에 대 한 tooupdate hello 응용 프로그램 코드를 필요 사용 **업데이트** hello 클라우드 서비스 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-110">If you need tooupdate hello application code for your cloud service, use **Update** on hello cloud service blade.</span></span> <span data-ttu-id="e1f07-111">단일 역할이나 모든 역할을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-111">You can update a single role or all roles.</span></span> <span data-ttu-id="e1f07-112">tooupdate, 서비스 구성 파일 또는 새 서비스 패키지를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-112">tooupdate, you can upload a new service package or service configuration file.</span></span>

1. <span data-ttu-id="e1f07-113">Hello에 [Azure 포털][Azure portal], tooupdate 원하는 hello 클라우드 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-113">In hello [Azure portal][Azure portal], select hello cloud service you want tooupdate.</span></span> <span data-ttu-id="e1f07-114">이 단계는 hello 클라우드 서비스 인스턴스 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-114">This step opens hello cloud service instance blade.</span></span>
2. <span data-ttu-id="e1f07-115">Hello 블레이드에서 hello 클릭 **업데이트** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-115">In hello blade, click hello **Update** button.</span></span>

    ![업데이트 단추](./media/cloud-services-how-to-manage-portal/update-button.png)

3. <span data-ttu-id="e1f07-117">새 서비스 패키지 파일 (.cspkg) 및 서비스 구성 파일 (.cscfg) 사용 하 여 hello 배포를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-117">Update hello deployment with a new service package file (.cspkg) and service configuration file (.cscfg).</span></span>

    ![배포 업데이트](./media/cloud-services-how-to-manage-portal/update-blade.png)

4. <span data-ttu-id="e1f07-119">**필요에 따라** hello 배포 레이블 및 hello 저장소 계정을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-119">**Optionally** update hello deployment label and hello storage account.</span></span>
5. <span data-ttu-id="e1f07-120">모든 역할 역할 인스턴스를 하나만 있는 경우 선택 hello **하나 이상의 역할 단일 인스턴스가 포함 된 경우에 배포** tooenable hello 업그레이드 tooproceed 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-120">If any roles have only one role instance, select hello **Deploy even if one or more roles contain a single instance** tooenable hello upgrade tooproceed.</span></span>

    <span data-ttu-id="e1f07-121">Azure는 각 역할에 둘 이상의 역할 인스턴스(가상 컴퓨터)가 있는 경우에만 클라우드 서비스 업데이트 중 99.95%의 서비스 가용성을 보장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-121">Azure can only guarantee 99.95 percent service availability during a cloud service update if each role has at least two role instances (virtual machines).</span></span> <span data-ttu-id="e1f07-122">두 개의 역할 인스턴스와 하나의 가상 컴퓨터 hello 다른 업데이트에 클라이언트 요청을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-122">With two role instances, one virtual machine processes client requests while hello other is updated.</span></span>

6. <span data-ttu-id="e1f07-123">확인 **배포 시작** toohave hello 업데이트 hello 패키지의 hello 업로드가 완료 된 후에 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-123">Check **Start deployment** toohave hello update applied after hello upload of hello package has finished.</span></span>
7. <span data-ttu-id="e1f07-124">클릭 **확인** toobegin hello 서비스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-124">Click **OK** toobegin updating hello service.</span></span>

## <a name="how-to-swap-deployments-toopromote-a-staged-deployment-tooproduction"></a><span data-ttu-id="e1f07-125">방법: 준비 된 배포 tooproduction 배포 toopromote 교체</span><span class="sxs-lookup"><span data-stu-id="e1f07-125">How to: Swap deployments toopromote a staged deployment tooproduction</span></span>
<span data-ttu-id="e1f07-126">단계는 클라우드 서비스의 새로운 릴리스가 toodeploy 결정 및 클라우드 서비스 스테이징 환경에서 새 릴리스를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-126">When you decide toodeploy a new release of a cloud service, stage and test your new release in your cloud service staging environment.</span></span> <span data-ttu-id="e1f07-127">사용 하 여 **교체** tooswitch hello Url는 hello 하 여 두 개의 배포 사항은 및 새 릴리스 tooproduction 승격 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-127">Use **Swap** tooswitch hello URLs by which hello two deployments are addressed and promote a new release tooproduction.</span></span>

<span data-ttu-id="e1f07-128">Hello에서 배포를 스왑할 수 **클라우드 서비스** 페이지나 hello 대시보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-128">You can swap deployments from hello **Cloud Services** page or hello dashboard.</span></span>

1. <span data-ttu-id="e1f07-129">Hello에 [Azure 포털][Azure portal], tooupdate 원하는 hello 클라우드 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-129">In hello [Azure portal][Azure portal], select hello cloud service you want tooupdate.</span></span> <span data-ttu-id="e1f07-130">이 단계는 hello 클라우드 서비스 인스턴스 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-130">This step opens hello cloud service instance blade.</span></span>
2. <span data-ttu-id="e1f07-131">Hello 블레이드에서 hello 클릭 **교체** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-131">In hello blade, click hello **Swap** button.</span></span>

    ![클라우드 서비스 교환](./media/cloud-services-how-to-manage-portal/swap-button.png)

3. <span data-ttu-id="e1f07-133">hello 다음과 같은 확인 프롬프트가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-133">hello following confirmation prompt opens.</span></span>

    ![클라우드 서비스 교환](./media/cloud-services-how-to-manage-portal/swap-prompt.png)

4. <span data-ttu-id="e1f07-135">Hello 배포 정보를 확인 한 후 클릭 **확인** tooswap hello 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-135">After you verify hello deployment information, click **OK** tooswap hello deployments.</span></span>

    <span data-ttu-id="e1f07-136">hello 배포 스왑 발생 신속 하 게 변경 하는 hello 유일한 항목은 hello 가상 IP 주소 (Vip) hello 배포에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-136">hello deployment swap happens quickly because hello only thing that changes is hello virtual IP addresses (VIPs) for hello deployments.</span></span>

    <span data-ttu-id="e1f07-137">toosave 계산 비용이 hello 프로덕션 배포 예상 대로 작동 하는지 확인 한 후에 스테이징 배포를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-137">toosave compute costs, you can delete hello staging deployment after you verify that your production deployment is working as expected.</span></span>

### <a name="common-questions-about-swapping-deployments"></a><span data-ttu-id="e1f07-138">배포 교환에 대한 일반적인 질문</span><span class="sxs-lookup"><span data-stu-id="e1f07-138">Common questions about swapping deployments</span></span>

<span data-ttu-id="e1f07-139">**Hello 필수 구성 요소 배포를 교환 하는 무엇입니까?**</span><span class="sxs-lookup"><span data-stu-id="e1f07-139">**What are hello prerequisites for swapping deployments?**</span></span>

<span data-ttu-id="e1f07-140">성공적인 배포 교환을 위한 2가지 핵심 필수 조건은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-140">There are two key prerequisites for a successful deployment swap:</span></span>

- <span data-ttu-id="e1f07-141">프로덕션 슬롯에 대 한 고정 IP 주소를 toouse 하려는 경우에 프로그램 스테이징 슬롯에 대 한를 예약 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-141">If you would like toouse a static IP address for your production slot, you must reserve one for your staging slot as well.</span></span> <span data-ttu-id="e1f07-142">그렇지 않으면 hello 스왑 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-142">Otherwise, hello swap fails.</span></span>

- <span data-ttu-id="e1f07-143">Hello 교체를 수행 하기 전에 역할의 모든 인스턴스를 실행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-143">All instances of your roles must be running before you can perform hello swap.</span></span> <span data-ttu-id="e1f07-144">Hello Azure 포털의 hello 개요 블레이드에에서 인스턴스의 hello 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-144">You can check hello status of your instances in hello overview blade of hello Azure portal.</span></span> <span data-ttu-id="e1f07-145">Hello 또는 사용할 수 있습니다 [Get-azurerole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) Windows PowerShell에서 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-145">Alternatively, you can use hello [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) command in Windows PowerShell.</span></span>

<span data-ttu-id="e1f07-146">게스트 OS 업데이트 및 서비스 작업을 복구 배포에도 발생할 수 있습니다 toofail을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-146">Note that Guest OS updates and service healing operations can also cause deployment swaps toofail.</span></span> <span data-ttu-id="e1f07-147">자세한 내용은 [클라우드 서비스 배포 문제 해결](cloud-services-troubleshoot-deployment-problems.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1f07-147">For more information, see [Troubleshoot cloud service deployment problems](cloud-services-troubleshoot-deployment-problems.md).</span></span>

<span data-ttu-id="e1f07-148">**교체 시 응용 프로그램 가동 중지가 발생할 수 있습니까? 어떻게 처리해야 합니까?**</span><span class="sxs-lookup"><span data-stu-id="e1f07-148">**Does a swap incur downtime for my application? How should I handle it?**</span></span>

<span data-ttu-id="e1f07-149">Hello 마지막 섹션에서 설명한 배포 스왑은 hello Azure 부하 분산 장치에 구성 변경에 있기 때문에 일반적으로 속도가 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-149">As described in hello last section, a deployment swap is typically fast since it is just a configuration change in hello Azure load balancer.</span></span> <span data-ttu-id="e1f07-150">그러나 경우에 따라 10초 이상 걸리며 일시적인 연결 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-150">In some cases, however, it can take ten or more seconds and result in transient connection failures.</span></span> <span data-ttu-id="e1f07-151">toolimit 영향 tooyour 고객 구현을 고려할 [클라이언트 다시 시도 논리](../best-practices-retry-general.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-151">toolimit impact tooyour customers, consider implementing [client retry logic](../best-practices-retry-general.md).</span></span>

## <a name="how-to-link-a-resource-tooa-cloud-service"></a><span data-ttu-id="e1f07-152">방법: 리소스 tooa 클라우드 서비스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-152">How to: Link a resource tooa cloud service</span></span>
<span data-ttu-id="e1f07-153">Azure 포털 hello hello 현재 Azure 클래식 포털 같이 함께 리소스를 연결 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-153">hello Azure portal does not link resources together like hello current Azure classic portal does.</span></span> <span data-ttu-id="e1f07-154">대신, 추가 리소스 toohello 배포 hello 클라우드 서비스에서 사용 중인 동일한 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-154">Instead, deploy additional resources toohello same resource group being used by hello Cloud Service.</span></span>

## <a name="how-to-delete-deployments-and-a-cloud-service"></a><span data-ttu-id="e1f07-155">방법: 배포 및 클라우드 서비스 삭제</span><span class="sxs-lookup"><span data-stu-id="e1f07-155">How to: Delete deployments and a cloud service</span></span>
<span data-ttu-id="e1f07-156">클라우드 서비스를 삭제하려면 먼저 각각의 기존 배포를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-156">Before you can delete a cloud service, you must delete each existing deployment.</span></span>

<span data-ttu-id="e1f07-157">toosave 계산 비용이 hello 프로덕션 배포 예상 대로 작동 하는지 확인 한 후에 스테이징 배포를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-157">toosave compute costs, you can delete hello staging deployment after you verify that your production deployment is working as expected.</span></span> <span data-ttu-id="e1f07-158">중지된 배포된 역할 인스턴스의 계산 비용이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-158">You are billed for compute costs for deployed role instances that are stopped.</span></span>

<span data-ttu-id="e1f07-159">배포 또는 클라우드 서비스 프로시저 toodelete 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-159">Use hello following procedure toodelete a deployment or your cloud service.</span></span>

1. <span data-ttu-id="e1f07-160">Hello에 [Azure 포털][Azure portal], toodelete 원하는 hello 클라우드 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-160">In hello [Azure portal][Azure portal], select hello cloud service you want toodelete.</span></span> <span data-ttu-id="e1f07-161">이 단계는 hello 클라우드 서비스 인스턴스 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-161">This step opens hello cloud service instance blade.</span></span>
2. <span data-ttu-id="e1f07-162">Hello 블레이드에서 hello 클릭 **삭제** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-162">In hello blade, click hello **Delete** button.</span></span>

    ![클라우드 서비스 교환](./media/cloud-services-how-to-manage-portal/delete-button.png)

3. <span data-ttu-id="e1f07-164">확인 하 여 hello 전체 클라우드 서비스를 삭제 하려면 **클라우드 서비스 및 해당 배포** hello 중 하나를 선택 하거나 **프로덕션 배포** 또는 hello **스테이징 배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-164">You can delete hello entire cloud service by checking **Cloud service and its deployments** or choose either hello **Production deployment** or hello **Staging deployment**.</span></span>

    ![클라우드 서비스 교환](./media/cloud-services-how-to-manage-portal/delete-blade.png)

4. <span data-ttu-id="e1f07-166">Hello 클릭 **삭제** hello 아래쪽 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-166">Click hello **Delete** button at hello bottom.</span></span>
5. <span data-ttu-id="e1f07-167">toodelete hello 클라우드 서비스를 클릭 하 여 **삭제 클라우드 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-167">toodelete hello cloud service, click **Delete cloud service**.</span></span> <span data-ttu-id="e1f07-168">Hello 명령 프롬프트에서 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-168">Then, at hello confirmation prompt, click **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="e1f07-169">클라우드 서비스가 삭제 되 고 구성 되는 자세한 정보 표시 모니터링 하는 경우 저장소 계정에서 hello 데이터를 수동으로 삭제 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-169">When a cloud service is deleted, and verbose monitoring is configured, you must delete hello data manually from your storage account.</span></span> <span data-ttu-id="e1f07-170">여기서 toofind hello 메트릭 테이블에 대 한 정보를 참조 하십시오. [이](cloud-services-how-to-monitor.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="e1f07-170">For information about where toofind hello metrics tables, see [this](cloud-services-how-to-monitor.md) article.</span></span>


## <a name="how-to-find-more-information-about-failed-deployments"></a><span data-ttu-id="e1f07-171">방법: 실패한 배포에 대한 자세한 정보 보기</span><span class="sxs-lookup"><span data-stu-id="e1f07-171">How to: Find more information about failed deployments</span></span>
<span data-ttu-id="e1f07-172">hello **개요** 블레이드 상태 표시줄이 hello 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-172">hello **Overview** blade has a status bar at hello top.</span></span> <span data-ttu-id="e1f07-173">Hello 막대를 클릭 하면는 새 블레이드가 열리고 모든 오류 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-173">When you click hello bar, a new blade opens and displays any error information.</span></span> <span data-ttu-id="e1f07-174">Hello 배포에 포함 된 오류가 hello 정보 블레이드에서 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-174">If hello deployment does not contain any errors, hello information blade is blank.</span></span>

![클라우드 서비스 교환](./media/cloud-services-how-to-manage-portal/status-info.png)



[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="e1f07-176">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e1f07-176">Next steps</span></span>
* <span data-ttu-id="e1f07-177">[클라우드 서비스의 일반 구성](cloud-services-how-to-configure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="e1f07-177">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="e1f07-178">너무 방법에 대해 알아봅니다[클라우드 서비스 배포](cloud-services-how-to-create-deploy-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f07-178">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="e1f07-179">[사용자 지정 도메인 이름](cloud-services-custom-domain-name-portal.md)구성</span><span class="sxs-lookup"><span data-stu-id="e1f07-179">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="e1f07-180">[SSL 인증서](cloud-services-configure-ssl-certificate-portal.md)구성</span><span class="sxs-lookup"><span data-stu-id="e1f07-180">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
