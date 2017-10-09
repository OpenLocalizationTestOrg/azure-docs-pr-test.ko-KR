---
title: "aaaUse hello Azure 컴퓨터 학습 웹 서비스 포털 | Microsoft Docs"
description: "액세스 tooAzure 기계 학습 작업 영역, 관리 및 배포 하 고 기계 학습 API 웹 서비스 관리"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: jhubbard
editor: cgronlun
ms.assetid: b62cf2ca-dd2a-4a83-bb54-469f948fb026
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: v-donglo
ms.openlocfilehash: 04b49027fc0ab227382b320310088bb66aafacc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-service-using-hello-azure-machine-learning-web-services-portal"></a><span data-ttu-id="c9e15-103">Hello Azure 컴퓨터 학습 웹 서비스 포털을 사용 하 여 웹 서비스 관리</span><span class="sxs-lookup"><span data-stu-id="c9e15-103">Manage a Web service using hello Azure Machine Learning Web Services portal</span></span>
<span data-ttu-id="c9e15-104">Hello Microsoft Azure 컴퓨터 학습 웹 서비스 포털을 사용 하 여 컴퓨터 학습 새로 추가 되거나 기존의 웹 서비스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-104">You can manage your Machine Learning New and Classic Web services using hello Microsoft Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="c9e15-105">기존 웹 서비스와 새 웹 서비스는 서로 다른 기본 기술에 기반하고 있으므로 서비스 각각에는 약간씩 다른 관리 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-105">Since Classic Web services and New Web services are based on different underlying technologies, you have slightly different management capabilities for each of them.</span></span>

<span data-ttu-id="c9e15-106">Hello 컴퓨터 학습 웹 서비스 포털에서 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-106">In hello Machine Learning Web Services portal you can:</span></span>

* <span data-ttu-id="c9e15-107">Hello 웹 서비스 사용 되는 방식을 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-107">Monitor how hello web service is being used.</span></span>
* <span data-ttu-id="c9e15-108">Hello 설명 구성 hello 웹에 대 한 hello 키를 업데이트 합니다 (새로만 해당) 서비스, 사용자 저장소 계정 키 (새로만 해당), 로깅 사용, 업데이트 및 사용 하도록 설정 또는 샘플 데이터를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-108">Configure hello description, update hello keys for hello web service (New only), update your storage account key (New only), enable logging, and enable or disable sample data.</span></span>
* <span data-ttu-id="c9e15-109">Hello 웹 서비스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-109">Delete hello web service.</span></span>
* <span data-ttu-id="c9e15-110">청구 계획을 만들거나 삭제하거나 업데이트합니다(새 서비스에만 해당).</span><span class="sxs-lookup"><span data-stu-id="c9e15-110">Create, delete, or update billing plans (New only).</span></span>
* <span data-ttu-id="c9e15-111">끝점을 추가하거나 삭제 합니다(기존 서비스에만 해당).</span><span class="sxs-lookup"><span data-stu-id="c9e15-111">Add and delete endpoints (Classic only)</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="permissions-toomanage-new-resources-manager-based-web-services"></a><span data-ttu-id="c9e15-112">사용 권한 toomanage 새 리소스 관리자 기반 웹 서비스</span><span class="sxs-lookup"><span data-stu-id="c9e15-112">Permissions toomanage New Resources Manager based web services</span></span>

<span data-ttu-id="c9e15-113">새 웹 서비스는 Azure 리소스로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-113">New web services are deployed as Azure resources.</span></span> <span data-ttu-id="c9e15-114">이와 같이 hello 올바른 사용 권한이 toodeploy 고 해야 새 웹 서비스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-114">As such, you must have hello correct permissions toodeploy and manage New web services.</span></span>  <span data-ttu-id="c9e15-115">toodeploy 참가자를 할당 해야 하는 새 웹 서비스를 관리 또는 hello 구독 toowhich hello 웹 서비스에 대 한 관리자 역할을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-115">toodeploy or manage New web services you must be assigned a contributor or administrator role on hello subscription toowhich hello web service is deployed.</span></span> <span data-ttu-id="c9e15-116">다른 사용자 tooa 기계 학습 작업 영역을 초대 배포 하거나 웹 서비스를 관리 하려면 해당를 tooa 참가자 또는 관리자 역할 hello 구독에 할당 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-116">If you invite another user tooa machine learning workspace, you must assign them tooa contributor or administrator role on hello subscription before they can deploy or manage web services.</span></span> 

<span data-ttu-id="c9e15-117">Hello 사용자 hello Azure 컴퓨터 학습 웹 서비스 포털에서 사용 권한을 tooaccess 리소스를 수정 하는 hello 없으면 toodeploy 웹 서비스는 동안 다음 오류가 hello를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-117">If hello user does not have hello correct permissions tooaccess resources in hello Azure Machine Learning Web Services portal, they will receive hello following error when trying toodeploy a web service:</span></span>

<span data-ttu-id="c9e15-118">*웹 서비스 배포에 실패했습니다. 이 계정에는 충분 한 액세스 toohello hello 작업 영역을 포함 하는 Azure 구독이 없습니다. 순서 대로 toodeploy 웹 서비스 tooAzure, 동일한 계정 이어야 합니다 hello toohello 작업 영역을 초대 그리고 hello 작업 영역 포함 된 지정 된 액세스 toohello Azure 구독 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="c9e15-118">*Web Service deployment failed. This account does not have sufficient access toohello Azure subscription that contains hello Workspace. In order toodeploy a Web Service tooAzure, hello same account must be invited toohello Workspace and be given access toohello Azure subscription that contains hello Workspace.*</span></span>

<span data-ttu-id="c9e15-119">작업 영역을 만드는 방법에 대한 자세한 내용은 [Azure Machine Learning 작업 영역 만들기 및 공유](machine-learning-create-workspace.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9e15-119">For more information on creating a workspace, see [Create and share an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

<span data-ttu-id="c9e15-120">액세스 권한 설정에 대 한 자세한 내용은 참조 하십시오. [hello Azure 포털-공개 미리 보기의에서 사용자 및 그룹에 대 한 보기 액세스 할당](../active-directory/role-based-access-control-manage-assignments.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-120">For more information on setting access permissions, see [View access assignments for users and groups in hello Azure portal - Public preview](../active-directory/role-based-access-control-manage-assignments.md).</span></span>


## <a name="manage-new-web-services"></a><span data-ttu-id="c9e15-121">새 웹 서비스 관리</span><span class="sxs-lookup"><span data-stu-id="c9e15-121">Manage New Web services</span></span>
<span data-ttu-id="c9e15-122">toomanage 새 웹 서비스:</span><span class="sxs-lookup"><span data-stu-id="c9e15-122">toomanage your New Web services:</span></span>

1. <span data-ttu-id="c9e15-123">Toohello 로그인 [Microsoft Azure 컴퓨터 학습 웹 서비스](https://services.azureml.net/quickstart) Microsoft Azure 계정-연결 된 hello 계정 사용을 사용 하 여 포털 hello Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="c9e15-123">Sign in toohello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal using your Microsoft Azure account - use hello account that's associated with hello Azure subscription.</span></span>
2. <span data-ttu-id="c9e15-124">Hello 메뉴를 클릭 **웹 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-124">On hello menu, click **Web Services**.</span></span>

<span data-ttu-id="c9e15-125">그러면 구독에 배포된 웹 서비스의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-125">This displays a list of deployed Web services for your subscription.</span></span> 

<span data-ttu-id="c9e15-126">toomanage 웹 서비스를 웹 서비스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-126">toomanage a Web service, click Web Services.</span></span> <span data-ttu-id="c9e15-127">Hello 웹 서비스 페이지에서 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-127">From hello Web Services page you can:</span></span>

* <span data-ttu-id="c9e15-128">Hello 웹 서비스 toomanage 클릭 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-128">Click hello web service toomanage it.</span></span>
* <span data-ttu-id="c9e15-129">웹 서비스 tooupdate hello에 대 한 대금 청구 계획 hello 클릭 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-129">Click hello Billing Plan for hello web service tooupdate it.</span></span>
* <span data-ttu-id="c9e15-130">웹 서비스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-130">Delete a web service.</span></span>
* <span data-ttu-id="c9e15-131">웹 서비스 복사한 tooanother 영역을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-131">Copy a web service and deploy it tooanother region.</span></span>

<span data-ttu-id="c9e15-132">웹 서비스를 클릭 하면 hello 웹 서비스 빠른 시작 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-132">When you click a web service, hello web service Quickstart page opens.</span></span> <span data-ttu-id="c9e15-133">hello 웹 서비스 빠른 시작 페이지에는 웹 서비스 toomanage를 허용 하는 두 가지 메뉴 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-133">hello web service Quickstart page has two menu options that allow you toomanage your web service:</span></span>

* <span data-ttu-id="c9e15-134">**대시보드** -tooview 웹 서비스 사용을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-134">**DASHBOARD** - Allows you tooview Web service usage.</span></span>
* <span data-ttu-id="c9e15-135">**구성** -웹 서비스 hello와 연결 된 hello 저장소 계정에 대 한 업데이트 hello 키 tooadd 설명 텍스트를 허용 하 고 사용 하도록 설정 하거나 예제 데이터를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-135">**CONFIGURE** - Allows you tooadd descriptive text, update hello key for hello storage account associated with hello Web service, and enable or disable sample data.</span></span>

### <a name="monitoring-how-hello-web-service-is-being-used"></a><span data-ttu-id="c9e15-136">Hello 웹 서비스 사용 되는 방식을 모니터링</span><span class="sxs-lookup"><span data-stu-id="c9e15-136">Monitoring how hello web service is being used</span></span>
<span data-ttu-id="c9e15-137">Hello 클릭 **대시보드** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-137">Click hello **DASHBOARD** tab.</span></span>

<span data-ttu-id="c9e15-138">Hello 대시보드에서 시간 동안 웹 서비스의 전반적인 사용량을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-138">From hello dashboard, you can view overall usage of your Web service over a period of time.</span></span> <span data-ttu-id="c9e15-139">Hello 기간 tooview hello hello 사용 현황 차트의 오른쪽 위에 있는 hello 기간 드롭다운 메뉴에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-139">You can select hello period tooview from hello Period dropdown menu in hello upper right of hello usage charts.</span></span> <span data-ttu-id="c9e15-140">hello 대시보드 hello 다음 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-140">hello dashboard shows hello following information:</span></span>

* <span data-ttu-id="c9e15-141">**시간에 따른 요청** hello 특정 기간을 통해 요청 hello 수 단계 그래프를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-141">**Requests Over Time** displays a step graph of hello number of requests over hello selected time period.</span></span> <span data-ttu-id="c9e15-142">사용량이 급증하는 경우에 식별할 수 있도록 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-142">It can help identify if you are experiencing spikes in usage.</span></span>
* <span data-ttu-id="c9e15-143">**요청-응답 요청** hello hello 서비스 hello 선택한 기간 및 그 중 실패 한를 통해 수신한 요청-응답 호출의 총 수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-143">**Request-Response Requests** displays hello total number of Request-Response calls hello service has received over hello selected time period and how many of them failed.</span></span>
* <span data-ttu-id="c9e15-144">**평균 시간을 계산 하는 요청-응답** hello 시간의 평균을 표시 tooexecute hello 받은 요청 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-144">**Average Request-Response Compute Time** displays an average of hello time needed tooexecute hello received requests.</span></span>
* <span data-ttu-id="c9e15-145">**일괄 처리 요청** 표시 hello의 총 일괄 처리 요청 hello 서비스 기간을 선택 하는 hello를 통해을 얼마나 많이 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-145">**Batch Requests** displays hello total number of Batch Requests hello service has received over hello selected time period and how many of them failed.</span></span>
* <span data-ttu-id="c9e15-146">**평균 작업 대기 시간** hello 시간의 평균을 표시 tooexecute hello 받은 요청 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-146">**Average Job Latency** displays an average of hello time needed tooexecute hello received requests.</span></span>
* <span data-ttu-id="c9e15-147">**오류** toohello 웹 서비스 호출에서 발생 한 오류를 hello 집계 수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-147">**Errors** displays hello aggregate number of errors that have occurred on calls toohello web service.</span></span>
* <span data-ttu-id="c9e15-148">**서비스 비용** hello 서비스와 연결 된 hello 청구 계획에 대 한 hello 요금을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-148">**Services Costs** displays hello charges for hello billing plan associated with hello service.</span></span>

### <a name="configuring-hello-web-service"></a><span data-ttu-id="c9e15-149">Hello 웹 서비스 구성</span><span class="sxs-lookup"><span data-stu-id="c9e15-149">Configuring hello web service</span></span>
<span data-ttu-id="c9e15-150">Hello 클릭 **구성** 메뉴 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-150">Click hello **CONFIGURE** menu option.</span></span>

<span data-ttu-id="c9e15-151">Hello 다음과 같은 속성을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-151">You can update hello following properties:</span></span>

* <span data-ttu-id="c9e15-152">**설명** tooenter hello 웹 서비스에 대 한 설명이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-152">**Description** allows you tooenter a description for hello Web service.</span></span>
* <span data-ttu-id="c9e15-153">**제목** tooenter hello 웹 서비스에 대 한 title 있습니다</span><span class="sxs-lookup"><span data-stu-id="c9e15-153">**Title** allows you tooenter a title for hello Web service</span></span>
* <span data-ttu-id="c9e15-154">**키** toorotate 사용 하면 기본 및 보조 API 키입니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-154">**Keys** allows you toorotate your primary and secondary API keys.</span></span>
* <span data-ttu-id="c9e15-155">**저장소 계정 키** hello 웹 서비스 변경과 관련 된 hello 저장소 계정에 대 한 tooupdate hello 키 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-155">**Storage account key** allows you tooupdate hello key for hello storage account associated with hello Web service changes.</span></span> 
* <span data-ttu-id="c9e15-156">**예제 데이터 사용** tooprovide 예제 데이터 tootest hello 요청 응답 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-156">**Enable Sample data** allows you tooprovide sample data that you can use tootest hello Request-Response service.</span></span> <span data-ttu-id="c9e15-157">기계 학습 스튜디오에서 hello 웹 서비스를 만든 경우 hello 예제 데이터에서에서 가져온 것 hello 데이터에 사용 되는 tootrain 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-157">If you created hello web service in Machine Learning Studio, hello sample data is taken from hello data your used tootrain your model.</span></span> <span data-ttu-id="c9e15-158">Hello 서비스를 프로그래밍 방식으로 만든 경우 hello 데이터 hello JSON 패키지의 일부로 제공 하는 hello 예제 데이터에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-158">If you created hello service programmatically, hello data is taken from hello example data you provided as part of hello JSON package.</span></span>

### <a name="managing-billing-plans"></a><span data-ttu-id="c9e15-159">청구 계획 관리</span><span class="sxs-lookup"><span data-stu-id="c9e15-159">Managing billing plans</span></span>
<span data-ttu-id="c9e15-160">Hello 클릭 **계획** hello 웹 서비스 빠른 시작 페이지에서 메뉴 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-160">Click hello **Plans** menu option from hello web services Quickstart page.</span></span> <span data-ttu-id="c9e15-161">계획 하는 특정 웹 서비스 toomanage와 연결 된 hello 계획을 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-161">You can also click hello plan associated with specific Web service toomanage that plan.</span></span>

* <span data-ttu-id="c9e15-162">**새** toocreate 새 계획을 사용 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-162">**New** allows you toocreate a new plan.</span></span>
* <span data-ttu-id="c9e15-163">**추가/제거 계획 인스턴스** 사용 하면 너무 "확장" 하 여 기존 계획 tooadd 용량이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-163">**Add/Remove Plan instance** allows you too"scale out" an existing plan tooadd capacity.</span></span>
* <span data-ttu-id="c9e15-164">**업그레이드/다운 그레이드** 사용 하면 너무 "확장" 하 여 기존 계획 tooadd 용량이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-164">**Upgrade/DownGrade** allows you too"scale up" an existing plan tooadd capacity.</span></span>
* <span data-ttu-id="c9e15-165">**삭제** toodelete 계획 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-165">**Delete** allows you toodelete a plan.</span></span>

<span data-ttu-id="c9e15-166">계획 tooview 대시보드를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-166">Click a plan tooview its dashboard.</span></span> <span data-ttu-id="c9e15-167">hello 대시보드에서 선택한 기간 동안 스냅숏 또는 계획 사용량을 보이도록합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-167">hello dashboard gives you snapshot or plan usage over a selected period of time.</span></span> <span data-ttu-id="c9e15-168">tooselect 시간 기간 tooview hello, hello 클릭 **기간** hello 대시보드의 오른쪽 위에서 드롭다운에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-168">tooselect hello time period tooview, click hello **Period** dropdown at hello upper right of dashboard.</span></span> 

<span data-ttu-id="c9e15-169">계획 대시보드 hello hello를 다음 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-169">hello plan dashboard provides hello following information:</span></span>

* <span data-ttu-id="c9e15-170">**계획 설명** hello 비용과 hello 계획과 연결 된 용량에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-170">**Plan Description** displays information about hello costs and capacity associated with hello plan.</span></span>
* <span data-ttu-id="c9e15-171">**사용을 계획** hello 트랜잭션과 hello 계획에 따라 요금이 청구 되었다는 계산 시간 수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-171">**Plan Usage** displays hello number of transactions and compute hours that have been charged against hello plan.</span></span>
* <span data-ttu-id="c9e15-172">**웹 서비스** 이 계획을 사용 하는 웹 서비스의 hello 수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-172">**Web Services** displays hello number of Web services that are using this plan.</span></span>
* <span data-ttu-id="c9e15-173">**웹 서비스 호출 하 여 상위** hello 계획에 따라 부과 된 호출 하는 hello 상위 4 개 웹 서비스를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-173">**Top Web Service By Calls** displays hello top four Web services that are making calls that are charged against hello plan.</span></span>
* <span data-ttu-id="c9e15-174">**계산 시간 기준으로 웹 서비스를 상위** hello 계획에 따라 요금이 청구 되는 계산 리소스를 사용 하는 hello 상위 4 개 웹 서비스를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-174">**Top Web Services by Compute Hrs** displays hello top four Web services that are using compute resources that are charged against hello plan.</span></span>

## <a name="manage-classic-web-services"></a><span data-ttu-id="c9e15-175">기존 웹 서비스 관리</span><span class="sxs-lookup"><span data-stu-id="c9e15-175">Manage Classic Web Services</span></span>
> [!NOTE]
> <span data-ttu-id="c9e15-176">이 섹션의 절차에서는 hello는 hello Azure 컴퓨터 학습 웹 서비스 포털을 통해 관련 toomanaging 클래식 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-176">hello procedures in this section are relevant toomanaging Classic web services through hello Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="c9e15-177">클래식 웹 관리에 대 한 내용은 서비스를 통해 기계 학습 스튜디오 hello 및 hello Azure 클래식 포털에서 참조 [는 Azure 기계 학습 작업 영역을 관리](machine-learning-manage-workspace.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-177">For information on managing Classic Web services through hello Machine Learning Studio and hello Azure classic portal, see [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md).</span></span>
> 
> 

<span data-ttu-id="c9e15-178">toomanage 클래식 웹 서비스:</span><span class="sxs-lookup"><span data-stu-id="c9e15-178">toomanage your Classic Web services:</span></span>

1. <span data-ttu-id="c9e15-179">Toohello 로그인 [Microsoft Azure 컴퓨터 학습 웹 서비스](https://services.azureml.net/quickstart) Microsoft Azure 계정-연결 된 hello 계정 사용을 사용 하 여 포털 hello Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="c9e15-179">Sign in toohello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal using your Microsoft Azure account - use hello account that's associated with hello Azure subscription.</span></span>
2. <span data-ttu-id="c9e15-180">Hello 메뉴를 클릭 **웹 서비스를 클래식**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-180">On hello menu, click **Classic Web Services**.</span></span>

<span data-ttu-id="c9e15-181">웹 서비스를 클래식 toomanage 클릭 **웹 서비스를 클래식**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-181">toomanage a Classic Web Service, click **Classic Web Services**.</span></span> <span data-ttu-id="c9e15-182">Hello 클래식 웹 서비스 페이지에서 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-182">From hello Classic Web Services page you can:</span></span>

* <span data-ttu-id="c9e15-183">Hello 웹 서비스 tooview hello 연결 된 끝점을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-183">Click hello web service tooview hello associated endpoints.</span></span>
* <span data-ttu-id="c9e15-184">웹 서비스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-184">Delete a web service.</span></span>

<span data-ttu-id="c9e15-185">기존의 웹 서비스를 관리 하는 경우 사용 하면 각 hello 끝점 별도로 관리할 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-185">When you manage a Classic Web service, you manage each of hello endpoints separately.</span></span> <span data-ttu-id="c9e15-186">Hello 웹 서비스 페이지에서 웹 서비스를 클릭 하면 hello hello 서비스와 연결 된 끝점 목록이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-186">When you click a web service in hello Web Services page, hello list of endpoints associated with hello service opens.</span></span> 

<span data-ttu-id="c9e15-187">Hello 클래식 웹 서비스 끝점 페이지에 추가 하 고 hello 서비스에 끝점을 삭제할 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-187">On hello Classic Web Service endpoint page, you can add and delete endpoints on hello service.</span></span> <span data-ttu-id="c9e15-188">끝점 추가에 대한 자세한 내용은 [끝점 만들기](machine-learning-create-endpoint.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9e15-188">For more information on adding endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span>

<span data-ttu-id="c9e15-189">Hello 끝점 tooopen hello 웹 서비스 빠른 시작 페이지 중 하나를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-189">Click one of hello endpoints tooopen hello web service Quickstart page.</span></span> <span data-ttu-id="c9e15-190">Hello 빠른 시작 페이지에서 옵션에는 두 가지 메뉴 toomanage 수 있는 웹 서비스</span><span class="sxs-lookup"><span data-stu-id="c9e15-190">On hello Quickstart page, there are two menu options that allow you toomanage your web service:</span></span>

* <span data-ttu-id="c9e15-191">**대시보드** -tooview 웹 서비스 사용을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-191">**DASHBOARD** - Allows you tooview Web service usage.</span></span>
* <span data-ttu-id="c9e15-192">**구성** -tooadd 설명 텍스트를 사용 하면 오류 로깅을 켜고, 업데이트 hello 키 웹 서비스 hello와 관련 된 hello 저장소 계정에 대해 사용 하도록 설정 하 고 예제 데이터를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-192">**CONFIGURE** - Allows you tooadd descriptive text, turn error logging on and off, update hello key for hello storage account associated with hello Web service, and enable and disable sample data.</span></span>

### <a name="monitoring-how-hello-web-service-is-being-used"></a><span data-ttu-id="c9e15-193">Hello 웹 서비스 사용 되는 방식을 모니터링</span><span class="sxs-lookup"><span data-stu-id="c9e15-193">Monitoring how hello web service is being used</span></span>
<span data-ttu-id="c9e15-194">Hello 클릭 **대시보드** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-194">Click hello **DASHBOARD** tab.</span></span>

<span data-ttu-id="c9e15-195">Hello 대시보드에서 시간 동안 웹 서비스의 전반적인 사용량을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-195">From hello dashboard, you can view overall usage of your Web service over a period of time.</span></span> <span data-ttu-id="c9e15-196">Hello 기간 tooview hello hello 사용 현황 차트의 오른쪽 위에 있는 hello 기간 드롭다운 메뉴에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-196">You can select hello period tooview from hello Period dropdown menu in hello upper right of hello usage charts.</span></span> <span data-ttu-id="c9e15-197">hello 대시보드 hello 다음 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-197">hello dashboard shows hello following information:</span></span>

* <span data-ttu-id="c9e15-198">**시간에 따른 요청** hello 특정 기간을 통해 요청 hello 수 단계 그래프를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-198">**Requests Over Time** displays a step graph of hello number of requests over hello selected time period.</span></span> <span data-ttu-id="c9e15-199">사용량이 급증하는 경우에 식별할 수 있도록 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-199">It can help identify if you are experiencing spikes in usage.</span></span>
* <span data-ttu-id="c9e15-200">**요청-응답 요청** hello hello 서비스 hello 선택한 기간 및 그 중 실패 한를 통해 수신한 요청-응답 호출의 총 수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-200">**Request-Response Requests** displays hello total number of Request-Response calls hello service has received over hello selected time period and how many of them failed.</span></span>
* <span data-ttu-id="c9e15-201">**평균 시간을 계산 하는 요청-응답** hello 시간의 평균을 표시 tooexecute hello 받은 요청 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-201">**Average Request-Response Compute Time** displays an average of hello time needed tooexecute hello received requests.</span></span>
* <span data-ttu-id="c9e15-202">**일괄 처리 요청** 표시 hello의 총 일괄 처리 요청 hello 서비스 기간을 선택 하는 hello를 통해을 얼마나 많이 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-202">**Batch Requests** displays hello total number of Batch Requests hello service has received over hello selected time period and how many of them failed.</span></span>
* <span data-ttu-id="c9e15-203">**평균 작업 대기 시간** hello 시간의 평균을 표시 tooexecute hello 받은 요청 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-203">**Average Job Latency** displays an average of hello time needed tooexecute hello received requests.</span></span>
* <span data-ttu-id="c9e15-204">**오류** toohello 웹 서비스 호출에서 발생 한 오류를 hello 집계 수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-204">**Errors** displays hello aggregate number of errors that have occurred on calls toohello web service.</span></span>
* <span data-ttu-id="c9e15-205">**서비스 비용** hello 서비스와 연결 된 hello 청구 계획에 대 한 hello 요금을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-205">**Services Costs** displays hello charges for hello billing plan associated with hello service.</span></span>

### <a name="configuring-hello-web-service"></a><span data-ttu-id="c9e15-206">Hello 웹 서비스 구성</span><span class="sxs-lookup"><span data-stu-id="c9e15-206">Configuring hello web service</span></span>
<span data-ttu-id="c9e15-207">Hello 클릭 **구성** 메뉴 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-207">Click hello **CONFIGURE** menu option.</span></span>

<span data-ttu-id="c9e15-208">Hello 다음과 같은 속성을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-208">You can update hello following properties:</span></span>

* <span data-ttu-id="c9e15-209">**설명** tooenter hello 웹 서비스에 대 한 설명이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-209">**Description** allows you tooenter a description for hello Web service.</span></span> <span data-ttu-id="c9e15-210">설명은 필수 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-210">Description is a required field.</span></span>
* <span data-ttu-id="c9e15-211">**로깅** hello 끝점에 대 한 로깅을 tooenable 또는 사용 안 함 오류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-211">**Logging** allows you tooenable or disable error logging on hello endpoint.</span></span> <span data-ttu-id="c9e15-212">로깅에 대한 자세한 내용은 [Machine Learning 웹 서비스에 대한 로깅 사용](machine-learning-web-services-logging.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9e15-212">For more information on Logging, see Enable [logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>
* <span data-ttu-id="c9e15-213">**예제 데이터 사용** tooprovide 예제 데이터 tootest hello 요청 응답 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-213">**Enable Sample data** allows you tooprovide sample data that you can use tootest hello Request-Response service.</span></span> <span data-ttu-id="c9e15-214">기계 학습 스튜디오에서 hello 웹 서비스를 만든 경우 hello 예제 데이터에서에서 가져온 것 hello 데이터에 사용 되는 tootrain 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-214">If you created hello web service in Machine Learning Studio, hello sample data is taken from hello data your used tootrain your model.</span></span> <span data-ttu-id="c9e15-215">Hello 서비스를 프로그래밍 방식으로 만든 경우 hello 데이터 hello JSON 패키지의 일부로 제공 하는 hello 예제 데이터에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-215">If you created hello service programmatically, hello data is taken from hello example data you provided as part of hello JSON package.</span></span>

## <a name="grant-or-suspend-access-tooweb-services-for-users-in-hello-portal"></a><span data-ttu-id="c9e15-216">허용 또는 hello 포털에서 사용자에 대 한 액세스 tooWeb 서비스를 일시 중단</span><span class="sxs-lookup"><span data-stu-id="c9e15-216">Grant or suspend access tooWeb services for users in hello portal</span></span>
<span data-ttu-id="c9e15-217">Hello Azure 클래식 포털을 사용 하 여, 허용 하거나 toospecific 사용자 액세스를 거부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-217">Using hello Azure classic portal, you can allow or deny access toospecific users.</span></span>

### <a name="access-for-users-of-new-web-services"></a><span data-ttu-id="c9e15-218">새 웹 서비스 사용자의 액세스</span><span class="sxs-lookup"><span data-stu-id="c9e15-218">Access for users of New Web services</span></span>
<span data-ttu-id="c9e15-219">tooenable hello Azure 컴퓨터 학습 웹 서비스 포털에서 웹 서비스와 다른 사용자가 toowork에 추가 해야 공동 관리자와 Azure 구독에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-219">tooenable other users toowork with your Web services in hello Azure Machine Learning Web Services portal, you must add them as co-adminstrators on your Azure subscription.</span></span>

<span data-ttu-id="c9e15-220">Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com/) Microsoft Azure를 사용 하 여 계정-Azure 구독 hello와 관련 된 hello 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-220">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) using your Microsoft Azure account - use hello account that's associated with hello Azure subscription.</span></span>

1. <span data-ttu-id="c9e15-221">Hello 탐색 창에서 클릭 **설정**, 클릭 **관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-221">In hello navigation pane, click **Settings**, then click **Administrators**.</span></span>
2. <span data-ttu-id="c9e15-222">Hello hello 창의 아래쪽에 있는 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-222">At hello bottom of hello window, click **Add**.</span></span> 
3. <span data-ttu-id="c9e15-223">Hello A 공동 관리자 추가 대화 상자, 공동 관리자 및 공동 관리자 tooaccess hello를 선택한 후 hello 구독으로 tooadd 원하는 hello 사람의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-223">In hello ADD A CO-ADMINISTRATOR dialog, type hello email address of hello person you want tooadd as Co-administrator and then select hello subscription that you want hello Co-administrator tooaccess.</span></span>
4. <span data-ttu-id="c9e15-224">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-224">Click **Save**.</span></span>

### <a name="access-for-users-of-classic-web-services"></a><span data-ttu-id="c9e15-225">기존 웹 서비스 사용자의 액세스</span><span class="sxs-lookup"><span data-stu-id="c9e15-225">Access for users of Classic Web services</span></span>
<span data-ttu-id="c9e15-226">작업 영역 toomanage:</span><span class="sxs-lookup"><span data-stu-id="c9e15-226">toomanage a workspace:</span></span>

<span data-ttu-id="c9e15-227">Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com/) Microsoft Azure를 사용 하 여 계정-Azure 구독 hello와 관련 된 hello 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-227">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) using your Microsoft Azure account - use hello account that's associated with hello Azure subscription.</span></span>

1. <span data-ttu-id="c9e15-228">Hello Microsoft Azure 서비스 패널에서 **기계 학습**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-228">In hello Microsoft Azure services panel, click **MACHINE LEARNING**.</span></span>
2. <span data-ttu-id="c9e15-229">원하는 toomanage hello 작업 영역을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-229">Click hello workspace you want toomanage.</span></span>
3. <span data-ttu-id="c9e15-230">Hello 클릭 **구성** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-230">Click hello **CONFIGURE** tab.</span></span>

<span data-ttu-id="c9e15-231">Hello 구성 탭에서 일시 중지할 수 있습니다 액세스 toohello 기계 학습 작업 영역을 클릭 하 여 **DENY**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-231">From hello configuration tab, you can suspend access toohello Machine Learning workspace by clicking **DENY**.</span></span> <span data-ttu-id="c9e15-232">사용자가 더 이상 기계 학습 스튜디오에서 수 tooopen hello 작업 영역 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-232">Users will no longer be able tooopen hello workspace in Machine Learning Studio.</span></span> <span data-ttu-id="c9e15-233">toorestore 액세스 클릭 **허용**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-233">toorestore access, click **ALLOW**.</span></span>

<span data-ttu-id="c9e15-234">toospecific 사용자:</span><span class="sxs-lookup"><span data-stu-id="c9e15-234">toospecific users:</span></span>

<span data-ttu-id="c9e15-235">기계 학습 스튜디오에서 작업 한 toohello 영역 액세스 권한이 있는 toomanage 추가 계정을 클릭 **로그인 tooML Studio** hello에 **대시보드** 탭 합니다. 작업 영역을 hello 기계 학습 스튜디오에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-235">toomanage additional accounts who have access toohello workspace in Machine Learning Studio, click **Sign-in tooML Studio** in hello **DASHBOARD** tab. This opens hello workspace in Machine Learning Studio.</span></span> <span data-ttu-id="c9e15-236">여기에서 클릭 hello **설정** 탭 한 다음 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-236">From here, click hello **SETTINGS** tab and then **USERS**.</span></span> <span data-ttu-id="c9e15-237">클릭할 수 있는 **더 사용자 초대** toogive 사용자 toohello 작업 영역 액세스 또는 사용자 선택 하 고 클릭 **제거**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-237">You can click **INVITE MORE USERS** toogive users access toohello workspace, or select a user and click **REMOVE**.</span></span>

> [!NOTE]
> <span data-ttu-id="c9e15-238">hello **로그인 tooML Studio** 링크 hello 현재 로그인 하는 Microsoft 계정을 사용 하 여 기계 학습 스튜디오를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-238">hello **Sign-in tooML Studio** link opens Machine Learning Studio using hello Microsoft Account you are currently signed into.</span></span> <span data-ttu-id="c9e15-239">hello toosign toohello Azure 클래식 포털 toocreate 작업 영역에서에서 사용한 Microsoft 계정에 자동으로 없는 권한 tooopen 작업 영역을 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-239">hello Microsoft Account you used toosign in toohello Azure classic portal toocreate a workspace does not automatically have permission tooopen that workspace.</span></span> <span data-ttu-id="c9e15-240">작업 영역에서 tooopen toohello hello 영역의 hello 소유자로 정의 된 Microsoft 계정에에서 서명 해야 하거나 tooreceive hello 소유자 toojoin hello 작업 영역에서 초대장이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e15-240">tooopen a workspace, you must be signed in toohello Microsoft Account that was defined as hello owner of hello workspace, or you need tooreceive an invitation from hello owner toojoin hello workspace.</span></span>
> 
> 

