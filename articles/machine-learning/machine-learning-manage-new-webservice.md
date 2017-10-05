---
title: "Azure Machine Learning 웹 서비스 포털 사용 | Microsoft Docs"
description: "Azure 기계 학습 작업 영역에 대한 액세스를 관리하고, ML API 웹 서비스를 배포 및 관리합니다."
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
ms.openlocfilehash: ad1314aa4b504bd2cb3285789073d4f1de1f545d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-web-service-using-the-azure-machine-learning-web-services-portal"></a><span data-ttu-id="b07d0-103">Azure Machine Learning 웹 서비스 포털에서 웹 서비스 관리</span><span class="sxs-lookup"><span data-stu-id="b07d0-103">Manage a Web service using the Azure Machine Learning Web Services portal</span></span>
<span data-ttu-id="b07d0-104">Microsoft Azure Machine Learning 웹 서비스 포털을 사용하여 Machine Learning 새 웹 서비스 및 기존 웹 서비스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-104">You can manage your Machine Learning New and Classic Web services using the Microsoft Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="b07d0-105">기존 웹 서비스와 새 웹 서비스는 서로 다른 기본 기술에 기반하고 있으므로 서비스 각각에는 약간씩 다른 관리 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-105">Since Classic Web services and New Web services are based on different underlying technologies, you have slightly different management capabilities for each of them.</span></span>

<span data-ttu-id="b07d0-106">Machine Learning 웹 서비스 포털에서 수행할 수 있는 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-106">In the Machine Learning Web Services portal you can:</span></span>

* <span data-ttu-id="b07d0-107">웹 서비스가 사용되는 방식을 모니터링합니다</span><span class="sxs-lookup"><span data-stu-id="b07d0-107">Monitor how the web service is being used.</span></span>
* <span data-ttu-id="b07d0-108">설명을 구성하고, 웹 서비스 키 및 저장소 계정 키를 업데이트하며(새 서비스에만 해당), 로깅을 사용하도록 설정하고, 샘플 데이터를 사용하거나 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-108">Configure the description, update the keys for the web service (New only), update your storage account key (New only), enable logging, and enable or disable sample data.</span></span>
* <span data-ttu-id="b07d0-109">웹 서비스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-109">Delete the web service.</span></span>
* <span data-ttu-id="b07d0-110">청구 계획을 만들거나 삭제하거나 업데이트합니다(새 서비스에만 해당).</span><span class="sxs-lookup"><span data-stu-id="b07d0-110">Create, delete, or update billing plans (New only).</span></span>
* <span data-ttu-id="b07d0-111">끝점을 추가하거나 삭제 합니다(기존 서비스에만 해당).</span><span class="sxs-lookup"><span data-stu-id="b07d0-111">Add and delete endpoints (Classic only)</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="permissions-to-manage-new-resources-manager-based-web-services"></a><span data-ttu-id="b07d0-112">새 Resources Manager 기반 웹 서비스를 관리하기 위한 권한</span><span class="sxs-lookup"><span data-stu-id="b07d0-112">Permissions to manage New Resources Manager based web services</span></span>

<span data-ttu-id="b07d0-113">새 웹 서비스는 Azure 리소스로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-113">New web services are deployed as Azure resources.</span></span> <span data-ttu-id="b07d0-114">따라서 새 웹 서비스를 배포하고 관리하기 위한 올바른 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-114">As such, you must have the correct permissions to deploy and manage New web services.</span></span>  <span data-ttu-id="b07d0-115">새로운 웹 서비스를 배포 또는 관리하려면 웹 서비스가 배포된 구독에 대한 참여자 또는 관리자 역할을 할당받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-115">To deploy or manage New web services you must be assigned a contributor or administrator role on the subscription to which the web service is deployed.</span></span> <span data-ttu-id="b07d0-116">Machine Learning 작업 영역에 다른 사용자를 초대하는 경우 구독에 대한 참여자 또는 관리자 역할을 할당해야 해당 사용자가 웹 서비스를 배포하거나 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-116">If you invite another user to a machine learning workspace, you must assign them to a contributor or administrator role on the subscription before they can deploy or manage web services.</span></span> 

<span data-ttu-id="b07d0-117">사용자에게 Azure Machine Learning 웹 서비스 포털에서 리소스에 액세스할 수 있는 올바른 권한이 없으면 웹 서비스를 배포하려고 할 때 다음과 같은 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-117">If the user does not have the correct permissions to access resources in the Azure Machine Learning Web Services portal, they will receive the following error when trying to deploy a web service:</span></span>

<span data-ttu-id="b07d0-118">*웹 서비스 배포에 실패했습니다. 이 계정은 작업 영역을 포함하는 Azure 구독에 대한 충분한 액세스 권한이 없습니다. 웹 서비스를 Azure에 배포하려면 같은 계정을 작업 영역에 초대하여 작업 영역을 포함하는 Azure 구독에 액세스할 권한이 이 계정에 제공되어야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="b07d0-118">*Web Service deployment failed. This account does not have sufficient access to the Azure subscription that contains the Workspace. In order to deploy a Web Service to Azure, the same account must be invited to the Workspace and be given access to the Azure subscription that contains the Workspace.*</span></span>

<span data-ttu-id="b07d0-119">작업 영역을 만드는 방법에 대한 자세한 내용은 [Azure Machine Learning 작업 영역 만들기 및 공유](machine-learning-create-workspace.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b07d0-119">For more information on creating a workspace, see [Create and share an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

<span data-ttu-id="b07d0-120">액세스 권한 설정에 대한 자세한 내용은 [Azure Portal에서 사용자 및 그룹에 대한 액세스 권한 할당 보기 - 공개 미리 보기](../active-directory/role-based-access-control-manage-assignments.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b07d0-120">For more information on setting access permissions, see [View access assignments for users and groups in the Azure portal - Public preview](../active-directory/role-based-access-control-manage-assignments.md).</span></span>


## <a name="manage-new-web-services"></a><span data-ttu-id="b07d0-121">새 웹 서비스 관리</span><span class="sxs-lookup"><span data-stu-id="b07d0-121">Manage New Web services</span></span>
<span data-ttu-id="b07d0-122">새 웹 서비스를 관리하려면</span><span class="sxs-lookup"><span data-stu-id="b07d0-122">To manage your New Web services:</span></span>

1. <span data-ttu-id="b07d0-123">Microsoft Azure 계정을 사용하여 [Microsoft Azure Machine Learning 웹 서비스 ](https://services.azureml.net/quickstart) 포털에 로그인합니다. Azure 구독에 연결된 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-123">Sign in to the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal using your Microsoft Azure account - use the account that's associated with the Azure subscription.</span></span>
2. <span data-ttu-id="b07d0-124">메뉴에서 **웹 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-124">On the menu, click **Web Services**.</span></span>

<span data-ttu-id="b07d0-125">그러면 구독에 배포된 웹 서비스의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-125">This displays a list of deployed Web services for your subscription.</span></span> 

<span data-ttu-id="b07d0-126">웹 서비스를 관리하려면 해당 웹 서비스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-126">To manage a Web service, click Web Services.</span></span> <span data-ttu-id="b07d0-127">웹 서비스 페이지에서 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-127">From the Web Services page you can:</span></span>

* <span data-ttu-id="b07d0-128">웹 서비스를 클릭하여 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-128">Click the web service to manage it.</span></span>
* <span data-ttu-id="b07d0-129">웹 서비스에 대한 청구 계획을 클릭하여 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-129">Click the Billing Plan for the web service to update it.</span></span>
* <span data-ttu-id="b07d0-130">웹 서비스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-130">Delete a web service.</span></span>
* <span data-ttu-id="b07d0-131">웹 서비스를 복사하고 다른 지역에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-131">Copy a web service and deploy it to another region.</span></span>

<span data-ttu-id="b07d0-132">웹 서비스를 클릭하면 웹 서비스 빠른 시작 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-132">When you click a web service, the web service Quickstart page opens.</span></span> <span data-ttu-id="b07d0-133">웹 서비스 빠른 시작 페이지에는 다음과 같이 웹 서비스를 관리할 수 있는 두 개의 메뉴 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-133">The web service Quickstart page has two menu options that allow you to manage your web service:</span></span>

* <span data-ttu-id="b07d0-134">**대시보드** - 웹 서비스 사용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-134">**DASHBOARD** - Allows you to view Web service usage.</span></span>
* <span data-ttu-id="b07d0-135">**구성** - 설명 텍스트를 추가하고, 웹 서비스와 연결된 저장소 계정 키를 업데이트하고, 샘플 데이터를 사용하거나 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-135">**CONFIGURE** - Allows you to add descriptive text, update the key for the storage account associated with the Web service, and enable or disable sample data.</span></span>

### <a name="monitoring-how-the-web-service-is-being-used"></a><span data-ttu-id="b07d0-136">웹 서비스가 사용되는 방식 모니터링</span><span class="sxs-lookup"><span data-stu-id="b07d0-136">Monitoring how the web service is being used</span></span>
<span data-ttu-id="b07d0-137">**대시보드 탭** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-137">Click the **DASHBOARD** tab.</span></span>

<span data-ttu-id="b07d0-138">대시보드에서 일정 시간의 웹 서비스 전체 사용량을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-138">From the dashboard, you can view overall usage of your Web service over a period of time.</span></span> <span data-ttu-id="b07d0-139">사용량 차트의 오른쪽 위에 있는 기간 드롭다운 메뉴에서 보려는 기간을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-139">You can select the period to view from the Period dropdown menu in the upper right of the usage charts.</span></span> <span data-ttu-id="b07d0-140">대시보드에서는 다음 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-140">The dashboard shows the following information:</span></span>

* <span data-ttu-id="b07d0-141">**시간에 따른 요청** 은 선택한 기간 동안 요청 수의 단계 그래프를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-141">**Requests Over Time** displays a step graph of the number of requests over the selected time period.</span></span> <span data-ttu-id="b07d0-142">사용량이 급증하는 경우에 식별할 수 있도록 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-142">It can help identify if you are experiencing spikes in usage.</span></span>
* <span data-ttu-id="b07d0-143">**요청-응답 요청** 은 선택한 기간 동안 서비스가 수신한 요청-응답 호출의 총 횟수 및 그 중 실패한 횟수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-143">**Request-Response Requests** displays the total number of Request-Response calls the service has received over the selected time period and how many of them failed.</span></span>
* <span data-ttu-id="b07d0-144">**평균 요청-응답 계산 시간** 은 수신된 요청을 실행하는 데 필요한 시간의 평균을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-144">**Average Request-Response Compute Time** displays an average of the time needed to execute the received requests.</span></span>
* <span data-ttu-id="b07d0-145">**배치 요청** 은 선택한 기간 동안 서비스가 수신한 배치 요청의 총 횟수 및 그 중 실패한 횟수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-145">**Batch Requests** displays the total number of Batch Requests the service has received over the selected time period and how many of them failed.</span></span>
* <span data-ttu-id="b07d0-146">**평균 작업 대기** 는 수신된 요청을 실행하는 데 필요한 시간의 평균을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-146">**Average Job Latency** displays an average of the time needed to execute the received requests.</span></span>
* <span data-ttu-id="b07d0-147">**오류** 웹 서비스 호출에서 발생한 오류의 집계 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-147">**Errors** displays the aggregate number of errors that have occurred on calls to the web service.</span></span>
* <span data-ttu-id="b07d0-148">**서비스 비용** 은 서비스와 연결된 청구 계획에 대한 요금을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-148">**Services Costs** displays the charges for the billing plan associated with the service.</span></span>

### <a name="configuring-the-web-service"></a><span data-ttu-id="b07d0-149">웹 서비스 구성</span><span class="sxs-lookup"><span data-stu-id="b07d0-149">Configuring the web service</span></span>
<span data-ttu-id="b07d0-150">**구성** 메뉴 옵션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-150">Click the **CONFIGURE** menu option.</span></span>

<span data-ttu-id="b07d0-151">다음 속성을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-151">You can update the following properties:</span></span>

* <span data-ttu-id="b07d0-152">**설명** 웹 서비스에 대한 설명을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-152">**Description** allows you to enter a description for the Web service.</span></span>
* <span data-ttu-id="b07d0-153">**제목** 웹 서비스에 대한 제목을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-153">**Title** allows you to enter a title for the Web service</span></span>
* <span data-ttu-id="b07d0-154">**키** 를 사용하면 기본 API 키와 보조 API 키를 회전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-154">**Keys** allows you to rotate your primary and secondary API keys.</span></span>
* <span data-ttu-id="b07d0-155">**저장소 계정 키** 웹 서비스 변경 내용과 연결된 저장소 계정 키를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-155">**Storage account key** allows you to update the key for the storage account associated with the Web service changes.</span></span> 
* <span data-ttu-id="b07d0-156">**샘플 데이터 사용** 요청-응답 서비스 테스트에 사용할 수 있는 샘플 데이터를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-156">**Enable Sample data** allows you to provide sample data that you can use to test the Request-Response service.</span></span> <span data-ttu-id="b07d0-157">기계 학습 스튜디오에서 웹 서비스를 만든 경우 샘플 데이터는 모델을 학습하는 데 사용된 데이터에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-157">If you created the web service in Machine Learning Studio, the sample data is taken from the data your used to train your model.</span></span> <span data-ttu-id="b07d0-158">서비스를 프로그래밍 방식으로 만들 경우 JSON 패키지의 일부로 제공된 예제 데이터에서 가져온 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-158">If you created the service programmatically, the data is taken from the example data you provided as part of the JSON package.</span></span>

### <a name="managing-billing-plans"></a><span data-ttu-id="b07d0-159">청구 계획 관리</span><span class="sxs-lookup"><span data-stu-id="b07d0-159">Managing billing plans</span></span>
<span data-ttu-id="b07d0-160">웹 서비스 빠른 시작 페이지에서 **계획** 메뉴 옵션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-160">Click the **Plans** menu option from the web services Quickstart page.</span></span> <span data-ttu-id="b07d0-161">특정 웹 서비스와 연결된 계획을 선택하면 해당 계획을 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-161">You can also click the plan associated with specific Web service to manage that plan.</span></span>

* <span data-ttu-id="b07d0-162">**새로 만들기** 를 사용하면 새 계획을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-162">**New** allows you to create a new plan.</span></span>
* <span data-ttu-id="b07d0-163">**계획 인스턴스 추가/제거** 를 사용하면 기존 계획을 "확장"하여 용량을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-163">**Add/Remove Plan instance** allows you to "scale out" an existing plan to add capacity.</span></span>
* <span data-ttu-id="b07d0-164">**업그레이드/다운그레이드** 를 사용하면 기존 계획을 "강화"하여 용량을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-164">**Upgrade/DownGrade** allows you to "scale up" an existing plan to add capacity.</span></span>
* <span data-ttu-id="b07d0-165">**삭제** 를 사용하면 계획을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-165">**Delete** allows you to delete a plan.</span></span>

<span data-ttu-id="b07d0-166">계획을 클릭하면 해당 대시보드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-166">Click a plan to view its dashboard.</span></span> <span data-ttu-id="b07d0-167">대시보드는 선택한 기간 동안 스냅숏 또는 계획 사용량을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-167">The dashboard gives you snapshot or plan usage over a selected period of time.</span></span> <span data-ttu-id="b07d0-168">기간을 선택하려면 대시보드 오른쪽 위의 **기간** 드롭다운을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-168">To select the time period to view, click the **Period** dropdown at the upper right of dashboard.</span></span> 

<span data-ttu-id="b07d0-169">계획 대시보드에서는 다음 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-169">The plan dashboard provides the following information:</span></span>

* <span data-ttu-id="b07d0-170">**계획 설명** 은 계획과 관련된 비용 및 용량에 대한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-170">**Plan Description** displays information about the costs and capacity associated with the plan.</span></span>
* <span data-ttu-id="b07d0-171">**계획 사용량** 은 계획에 대한 요금이 청구된 트랜잭션 및 계산 시간 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-171">**Plan Usage** displays the number of transactions and compute hours that have been charged against the plan.</span></span>
* <span data-ttu-id="b07d0-172">**웹 서비스** 해당 계획을 사용하는 웹 서비스의 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-172">**Web Services** displays the number of Web services that are using this plan.</span></span>
* <span data-ttu-id="b07d0-173">**호출별 최상위 웹 서비스** 계획과 대조하여 요금이 청구되는 호출을 발생시키는 최상위 4개 웹 서비스를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-173">**Top Web Service By Calls** displays the top four Web services that are making calls that are charged against the plan.</span></span>
* <span data-ttu-id="b07d0-174">**계산 시간별 최상위 웹 서비스** 계획과 대조하여 요금이 청구되는 계산 리소스를 사용하는 최상위 4개 웹 서비스를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-174">**Top Web Services by Compute Hrs** displays the top four Web services that are using compute resources that are charged against the plan.</span></span>

## <a name="manage-classic-web-services"></a><span data-ttu-id="b07d0-175">기존 웹 서비스 관리</span><span class="sxs-lookup"><span data-stu-id="b07d0-175">Manage Classic Web Services</span></span>
> [!NOTE]
> <span data-ttu-id="b07d0-176">이 섹션의 절차는 Azure Machine Learning 웹 서비스 포털을 통해 기본 웹 서비스를 관리하는 것과 관련됩니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-176">The procedures in this section are relevant to managing Classic web services through the Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="b07d0-177">Machine Learning Studio 및 Azure 클래식 포털을 통한 기존 웹 서비스 관리에 대한 내용은 [Azure Machine Learning 작업 영역 관리](machine-learning-manage-workspace.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b07d0-177">For information on managing Classic Web services through the Machine Learning Studio and the Azure classic portal, see [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md).</span></span>
> 
> 

<span data-ttu-id="b07d0-178">기존 웹 서비스를 관리하려면</span><span class="sxs-lookup"><span data-stu-id="b07d0-178">To manage your Classic Web services:</span></span>

1. <span data-ttu-id="b07d0-179">Microsoft Azure 계정을 사용하여 [Microsoft Azure Machine Learning 웹 서비스 ](https://services.azureml.net/quickstart) 포털에 로그인합니다. Azure 구독에 연결된 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-179">Sign in to the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal using your Microsoft Azure account - use the account that's associated with the Azure subscription.</span></span>
2. <span data-ttu-id="b07d0-180">메뉴에서 **기존 웹 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-180">On the menu, click **Classic Web Services**.</span></span>

<span data-ttu-id="b07d0-181">**기존 웹 서비스**를 클릭하면 해당 웹 서비스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-181">To manage a Classic Web Service, click **Classic Web Services**.</span></span> <span data-ttu-id="b07d0-182">기존 웹 서비스 페이지에서 수행할 수 있는 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-182">From the Classic Web Services page you can:</span></span>

* <span data-ttu-id="b07d0-183">웹 서비스를 클릭하여 연결된 끝점을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-183">Click the web service to view the associated endpoints.</span></span>
* <span data-ttu-id="b07d0-184">웹 서비스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-184">Delete a web service.</span></span>

<span data-ttu-id="b07d0-185">기존 웹 서비스를 관리하는 경우 각 끝점을 개별적으로 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-185">When you manage a Classic Web service, you manage each of the endpoints separately.</span></span> <span data-ttu-id="b07d0-186">웹 서비스 페이지에서 웹 서비스를 클릭하면 서비스에 연결된 끝점들의 목록이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-186">When you click a web service in the Web Services page, the list of endpoints associated with the service opens.</span></span> 

<span data-ttu-id="b07d0-187">기존 웹 서비스 끝점 페이지에서 서비스의 끝점을 추가하거나 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-187">On the Classic Web Service endpoint page, you can add and delete endpoints on the service.</span></span> <span data-ttu-id="b07d0-188">끝점 추가에 대한 자세한 내용은 [끝점 만들기](machine-learning-create-endpoint.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b07d0-188">For more information on adding endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span>

<span data-ttu-id="b07d0-189">끝점 중 하나를 클릭하면 웹 서비스 빠른 시작 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-189">Click one of the endpoints to open the web service Quickstart page.</span></span> <span data-ttu-id="b07d0-190">웹 서비스 빠른 시작 페이지에는 다음과 같이 웹 서비스를 관리할 수 있는 두 개의 메뉴 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-190">On the Quickstart page, there are two menu options that allow you to manage your web service:</span></span>

* <span data-ttu-id="b07d0-191">**대시보드** - 웹 서비스 사용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-191">**DASHBOARD** - Allows you to view Web service usage.</span></span>
* <span data-ttu-id="b07d0-192">**구성** - 설명 텍스트를 추가하고, 오류 로깅을 설정 및 해제하며, 웹 서비스와 연결된 저장소 계정 키를 업데이트하고, 샘플 데이터를 사용하거나 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-192">**CONFIGURE** - Allows you to add descriptive text, turn error logging on and off, update the key for the storage account associated with the Web service, and enable and disable sample data.</span></span>

### <a name="monitoring-how-the-web-service-is-being-used"></a><span data-ttu-id="b07d0-193">웹 서비스가 사용되는 방식 모니터링</span><span class="sxs-lookup"><span data-stu-id="b07d0-193">Monitoring how the web service is being used</span></span>
<span data-ttu-id="b07d0-194">**대시보드 탭** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-194">Click the **DASHBOARD** tab.</span></span>

<span data-ttu-id="b07d0-195">대시보드에서 일정 시간의 웹 서비스 전체 사용량을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-195">From the dashboard, you can view overall usage of your Web service over a period of time.</span></span> <span data-ttu-id="b07d0-196">사용량 차트의 오른쪽 위에 있는 기간 드롭다운 메뉴에서 보려는 기간을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-196">You can select the period to view from the Period dropdown menu in the upper right of the usage charts.</span></span> <span data-ttu-id="b07d0-197">대시보드에서는 다음 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-197">The dashboard shows the following information:</span></span>

* <span data-ttu-id="b07d0-198">**시간에 따른 요청** 은 선택한 기간 동안 요청 수의 단계 그래프를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-198">**Requests Over Time** displays a step graph of the number of requests over the selected time period.</span></span> <span data-ttu-id="b07d0-199">사용량이 급증하는 경우에 식별할 수 있도록 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-199">It can help identify if you are experiencing spikes in usage.</span></span>
* <span data-ttu-id="b07d0-200">**요청-응답 요청** 은 선택한 기간 동안 서비스가 수신한 요청-응답 호출의 총 횟수 및 그 중 실패한 횟수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-200">**Request-Response Requests** displays the total number of Request-Response calls the service has received over the selected time period and how many of them failed.</span></span>
* <span data-ttu-id="b07d0-201">**평균 요청-응답 계산 시간** 은 수신된 요청을 실행하는 데 필요한 시간의 평균을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-201">**Average Request-Response Compute Time** displays an average of the time needed to execute the received requests.</span></span>
* <span data-ttu-id="b07d0-202">**배치 요청** 은 선택한 기간 동안 서비스가 수신한 배치 요청의 총 횟수 및 그 중 실패한 횟수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-202">**Batch Requests** displays the total number of Batch Requests the service has received over the selected time period and how many of them failed.</span></span>
* <span data-ttu-id="b07d0-203">**평균 작업 대기** 는 수신된 요청을 실행하는 데 필요한 시간의 평균을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-203">**Average Job Latency** displays an average of the time needed to execute the received requests.</span></span>
* <span data-ttu-id="b07d0-204">**오류** 웹 서비스 호출에서 발생한 오류의 집계 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-204">**Errors** displays the aggregate number of errors that have occurred on calls to the web service.</span></span>
* <span data-ttu-id="b07d0-205">**서비스 비용** 은 서비스와 연결된 청구 계획에 대한 요금을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-205">**Services Costs** displays the charges for the billing plan associated with the service.</span></span>

### <a name="configuring-the-web-service"></a><span data-ttu-id="b07d0-206">웹 서비스 구성</span><span class="sxs-lookup"><span data-stu-id="b07d0-206">Configuring the web service</span></span>
<span data-ttu-id="b07d0-207">**구성** 메뉴 옵션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-207">Click the **CONFIGURE** menu option.</span></span>

<span data-ttu-id="b07d0-208">다음 속성을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-208">You can update the following properties:</span></span>

* <span data-ttu-id="b07d0-209">**설명** 웹 서비스에 대한 설명을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-209">**Description** allows you to enter a description for the Web service.</span></span> <span data-ttu-id="b07d0-210">설명은 필수 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-210">Description is a required field.</span></span>
* <span data-ttu-id="b07d0-211">**로깅** 오류 끝점에 대한 로깅을 사용하거나 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-211">**Logging** allows you to enable or disable error logging on the endpoint.</span></span> <span data-ttu-id="b07d0-212">로깅에 대한 자세한 내용은 [Machine Learning 웹 서비스에 대한 로깅 사용](machine-learning-web-services-logging.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b07d0-212">For more information on Logging, see Enable [logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>
* <span data-ttu-id="b07d0-213">**샘플 데이터 사용** 요청-응답 서비스 테스트에 사용할 수 있는 샘플 데이터를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-213">**Enable Sample data** allows you to provide sample data that you can use to test the Request-Response service.</span></span> <span data-ttu-id="b07d0-214">기계 학습 스튜디오에서 웹 서비스를 만든 경우 샘플 데이터는 모델을 학습하는 데 사용된 데이터에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-214">If you created the web service in Machine Learning Studio, the sample data is taken from the data your used to train your model.</span></span> <span data-ttu-id="b07d0-215">서비스를 프로그래밍 방식으로 만들 경우 JSON 패키지의 일부로 제공된 예제 데이터에서 가져온 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-215">If you created the service programmatically, the data is taken from the example data you provided as part of the JSON package.</span></span>

## <a name="grant-or-suspend-access-to-web-services-for-users-in-the-portal"></a><span data-ttu-id="b07d0-216">포털에서 사용자의 웹 서비스 액세스 허용 또는 일시 중단</span><span class="sxs-lookup"><span data-stu-id="b07d0-216">Grant or suspend access to Web services for users in the portal</span></span>
<span data-ttu-id="b07d0-217">Azure 클래식 포털에서 특정 사용자의 액세스를 허용하거나 거부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-217">Using the Azure classic portal, you can allow or deny access to specific users.</span></span>

### <a name="access-for-users-of-new-web-services"></a><span data-ttu-id="b07d0-218">새 웹 서비스 사용자의 액세스</span><span class="sxs-lookup"><span data-stu-id="b07d0-218">Access for users of New Web services</span></span>
<span data-ttu-id="b07d0-219">다른 사용자가 Azure Machine Learning 웹 서비스 포털의 웹 서비스를 사용하려면 Azure 구독에 해당 사용자를 공동 관리자로 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-219">To enable other users to work with your Web services in the Azure Machine Learning Web Services portal, you must add them as co-adminstrators on your Azure subscription.</span></span>

<span data-ttu-id="b07d0-220">Microsoft Azure 계정을 사용하여 [Azure 클래식 포털](https://manage.windowsazure.com/)에 로그인합니다. Azure 구독에 연결된 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-220">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) using your Microsoft Azure account - use the account that's associated with the Azure subscription.</span></span>

1. <span data-ttu-id="b07d0-221">탐색 창에서 **설정**, **관리자**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-221">In the navigation pane, click **Settings**, then click **Administrators**.</span></span>
2. <span data-ttu-id="b07d0-222">창 아래에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-222">At the bottom of the window, click **Add**.</span></span> 
3. <span data-ttu-id="b07d0-223">공동 관리자 추가 대화 상자에서 공동 관리자로 추가할 사람의 메일 주소를 입력한 다음 공동 관리자가 액세스하려는 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-223">In the ADD A CO-ADMINISTRATOR dialog, type the email address of the person you want to add as Co-administrator and then select the subscription that you want the Co-administrator to access.</span></span>
4. <span data-ttu-id="b07d0-224">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-224">Click **Save**.</span></span>

### <a name="access-for-users-of-classic-web-services"></a><span data-ttu-id="b07d0-225">기존 웹 서비스 사용자의 액세스</span><span class="sxs-lookup"><span data-stu-id="b07d0-225">Access for users of Classic Web services</span></span>
<span data-ttu-id="b07d0-226">작업 영역을 관리하려면</span><span class="sxs-lookup"><span data-stu-id="b07d0-226">To manage a workspace:</span></span>

<span data-ttu-id="b07d0-227">Microsoft Azure 계정을 사용하여 [Azure 클래식 포털](https://manage.windowsazure.com/)에 로그인합니다. Azure 구독에 연결된 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-227">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) using your Microsoft Azure account - use the account that's associated with the Azure subscription.</span></span>

1. <span data-ttu-id="b07d0-228">Microsoft Azure 서비스 패널에서 **기계 학습**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-228">In the Microsoft Azure services panel, click **MACHINE LEARNING**.</span></span>
2. <span data-ttu-id="b07d0-229">관리하려는 작업 영역을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-229">Click the workspace you want to manage.</span></span>
3. <span data-ttu-id="b07d0-230">**구성** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-230">Click the **CONFIGURE** tab.</span></span>

<span data-ttu-id="b07d0-231">구성 탭에서 **거부**를 클릭하면 Machine Learning 작업 영역에 대한 액세스를 일시 중단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-231">From the configuration tab, you can suspend access to the Machine Learning workspace by clicking **DENY**.</span></span> <span data-ttu-id="b07d0-232">사용자는 더 이상 기계 학습 스튜디오에서 작업 영역을 열 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-232">Users will no longer be able to open the workspace in Machine Learning Studio.</span></span> <span data-ttu-id="b07d0-233">액세스를 복원하려면 **허용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-233">To restore access, click **ALLOW**.</span></span>

<span data-ttu-id="b07d0-234">특정 사용자의 경우</span><span class="sxs-lookup"><span data-stu-id="b07d0-234">To specific users:</span></span>

<span data-ttu-id="b07d0-235">Machine Learning Studio의 작업 영역에 액세스할 수 있는 계정을 추가로 관리하려면 **대시보드** 탭에서 **ML Studio에 로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-235">To manage additional accounts who have access to the workspace in Machine Learning Studio, click **Sign-in to ML Studio** in the **DASHBOARD** tab.</span></span> <span data-ttu-id="b07d0-236">그러면 작업 영역에서 기계 학습 스튜디오가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-236">This opens the workspace in Machine Learning Studio.</span></span> <span data-ttu-id="b07d0-237">여기서 **설정** 탭을 클릭한 다음 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-237">From here, click the **SETTINGS** tab and then **USERS**.</span></span> <span data-ttu-id="b07d0-238">**더 많은 사용자 초대**를 클릭하여 사용자에게 작업 영역에 대한 액세스 권한을 부여하거나 사용자를 선택하고 **제거**를 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-238">You can click **INVITE MORE USERS** to give users access to the workspace, or select a user and click **REMOVE**.</span></span>

> [!NOTE]
> <span data-ttu-id="b07d0-239">**ML 스튜디오에 로그인** 링크를 클릭하면 현재 로그인된 Microsoft 계정을 사용하여 기계 학습 스튜디오가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-239">The **Sign-in to ML Studio** link opens Machine Learning Studio using the Microsoft Account you are currently signed into.</span></span> <span data-ttu-id="b07d0-240">Azure 클래식 포털에 로그인하여 작업 영역을 만드는 데 사용한 Microsoft 계정에는 해당 작업 영역을 열 수 있는 권한이 자동으로 부여되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-240">The Microsoft Account you used to sign in to the Azure classic portal to create a workspace does not automatically have permission to open that workspace.</span></span> <span data-ttu-id="b07d0-241">작업 영역을 열려면 작업 영역의 소유자로 정의된 Microsoft 계정으로 로그인하거나 작업 공간 소유자의 참가 초대를 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b07d0-241">To open a workspace, you must be signed in to the Microsoft Account that was defined as the owner of the workspace, or you need to receive an invitation from the owner to join the workspace.</span></span>
> 
> 

