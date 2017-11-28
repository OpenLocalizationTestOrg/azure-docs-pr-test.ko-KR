---
title: "Machine Learning 작업 영역 관리 | Microsoft Docs"
description: "Azure 기계 학습 작업 영역에 대한 액세스를 관리하고, ML API 웹 서비스를 배포 및 관리합니다."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: daf3d413-7a77-4beb-9a7a-6b4bdf717719
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye
ms.openlocfilehash: 94800f51baf83311c33490cada5f991ff2101da9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-an-azure-machine-learning-workspace"></a><span data-ttu-id="58134-103">Azure 기계 학습 작업 영역 관리</span><span class="sxs-lookup"><span data-stu-id="58134-103">Manage an Azure Machine Learning workspace</span></span>

> [!NOTE]
> <span data-ttu-id="58134-104">Machine Learning 웹 서비스 포털의 웹 서비스 관리에 대한 자세한 내용은 [Azure Machine Learning 웹 서비스 포털에서 웹 서비스 관리](machine-learning-manage-new-webservice.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="58134-104">For information on managing Web services in the Machine Learning Web Services portal, see [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span>
> 
> 

<span data-ttu-id="58134-105">Azure Portal 또는 Azure 클래식 포털에서 Machine Learning 작업 영역을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58134-105">You can manage Machine Learning workspaces in either the Azure portal or the Azure classic portal.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="use-the-azure-portal"></a><span data-ttu-id="58134-106">Azure 포털 사용</span><span class="sxs-lookup"><span data-stu-id="58134-106">Use the Azure portal</span></span>

<span data-ttu-id="58134-107">Azure Portal에서 작업 영역을 관리하려면:</span><span class="sxs-lookup"><span data-stu-id="58134-107">To manage a workspace in the Azure portal:</span></span>

1. <span data-ttu-id="58134-108">Azure 구독 관리자 계정을 사용하여 [Azure Portal](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="58134-108">Sign in to the [Azure portal](https://portal.azure.com/) using an Azure subscription administrator account.</span></span>
2. <span data-ttu-id="58134-109">페이지 맨 위에 있는 검색 상자에 "machine learning 작업 영역"을 입력한 다음 선택 **Machine Learning 작업 영역**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58134-109">In the search box at the top of the page, enter "machine learning workspaces" and then select **Machine Learning Workspaces**.</span></span>
3. <span data-ttu-id="58134-110">관리하려는 작업 영역을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58134-110">Click the workspace you want to manage.</span></span>

<span data-ttu-id="58134-111">표준 리소스 관리 정보 및 사용할 수 있는 옵션 외에 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58134-111">In addition to the standard resource management information and options available, you can:</span></span>

- <span data-ttu-id="58134-112">**속성** 보기 - 이 페이지에는 작업 영역 및 리소스 정보가 표시됩니다. 이 작업 영역이 연결된 구독 및 리소스 그룹을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58134-112">View **Properties** - This page displays the workspace and resource information, and you can change the subscription and resource group that this workspace is connected with.</span></span>
- <span data-ttu-id="58134-113">**저장소 키 다시 동기화** - 이 작업 영역은 저장소 계정에 대한 키를 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="58134-113">**Resync Storage Keys** - The workspace maintains keys to the storage account.</span></span> <span data-ttu-id="58134-114">저장소 계정이 키를 변경하면 **키 다시 동기화**를 클릭하여 작업 영역과 키를 동기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58134-114">If the storage account changes keys, then you can click **Resync keys** to synchronize the keys with the workspace.</span></span>

<span data-ttu-id="58134-115">이 작업 영역과 연결된 웹 서비스를 관리하려면 Machine Learning 웹 서비스 포털을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="58134-115">To manage the web services associated with this workspace, use the Machine Learning Web Services portal.</span></span> <span data-ttu-id="58134-116">자세한 내용은 [Azure Machine Learning 웹 서비스 포털에서 웹 서비스 관리](machine-learning-manage-new-webservice.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="58134-116">See [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md) for complete information.</span></span>

> [!NOTE]
> <span data-ttu-id="58134-117">새로운 웹 서비스를 배포 또는 관리하려면 웹 서비스가 배포된 구독에 대한 참여자 또는 관리자 역할을 할당받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58134-117">To deploy or manage New web services you must be assigned a contributor or administrator role on the subscription to which the web service is deployed.</span></span> <span data-ttu-id="58134-118">Machine Learning 작업 영역에 다른 사용자를 초대하는 경우 구독에 대한 참여자 또는 관리자 역할을 할당해야 해당 사용자가 웹 서비스를 배포하거나 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58134-118">If you invite another user to a machine learning workspace, you must assign them to a contributor or administrator role on the subscription before they can deploy or manage web services.</span></span> 
> 
><span data-ttu-id="58134-119">액세스 권한 설정에 대한 자세한 내용은 [Azure Portal에서 사용자 및 그룹에 대한 액세스 권한 할당 보기 - 공개 미리 보기](../active-directory/role-based-access-control-manage-assignments.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="58134-119">For more information on setting access permissions, see [View access assignments for users and groups in the Azure portal - Public preview](../active-directory/role-based-access-control-manage-assignments.md).</span></span>

## <a name="use-the-azure-classic-portal"></a><span data-ttu-id="58134-120">Azure 클래식 포털 사용</span><span class="sxs-lookup"><span data-stu-id="58134-120">Use the Azure classic portal</span></span>

<span data-ttu-id="58134-121">Azure 클래식 포털을 사용하여 기계 학습 작업 영역을 관리하면 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58134-121">Using the Azure classic portal, you can manage your Machine Learning workspaces to:</span></span>

* <span data-ttu-id="58134-122">작업 영역이 사용되는 방식을 모니터링합니다</span><span class="sxs-lookup"><span data-stu-id="58134-122">Monitor how the workspace is being used</span></span>
* <span data-ttu-id="58134-123">액세스를 허용 또는 거부하도록 작업 영역 구성</span><span class="sxs-lookup"><span data-stu-id="58134-123">Configure the workspace to allow or deny access</span></span>
* <span data-ttu-id="58134-124">작업 영역에서 만든 웹 서비스 관리</span><span class="sxs-lookup"><span data-stu-id="58134-124">Manage Web services created in the workspace</span></span>
* <span data-ttu-id="58134-125">작업 영역 삭제</span><span class="sxs-lookup"><span data-stu-id="58134-125">Delete the workspace</span></span>

<span data-ttu-id="58134-126">또한 대시보드 탭은 작업 영역 사용 개요 및 작업 영역 정보의 간략 상태를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="58134-126">In addition, the dashboard tab provides an overview of your workspace usage and a quick glance of your workspace information.</span></span>  

> [!TIP]
> <span data-ttu-id="58134-127">Azure Machine Learning Studio의 **웹 서비스** 탭에서 Machine Learning 웹 서비스를 추가, 업데이트 또는 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58134-127">In Azure Machine Learning Studio, on the **WEB SERVICES** tab, you can add, update, or delete a Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="58134-128">Azure 클래식 포털에서 작업 영역을 관리하려면:</span><span class="sxs-lookup"><span data-stu-id="58134-128">To manage a workspace in the Azure classic portal:</span></span>

1. <span data-ttu-id="58134-129">Microsoft Azure 계정을 사용하여 [Azure 클래식 포털](https://manage.windowsazure.com/)에 로그인합니다. Azure 구독에 연결된 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="58134-129">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) using your Microsoft Azure account - use the account that's associated with the Azure subscription.</span></span>
2. <span data-ttu-id="58134-130">Microsoft Azure 서비스 패널에서 **기계 학습**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58134-130">In the Microsoft Azure services panel, click **MACHINE LEARNING**.</span></span>
3. <span data-ttu-id="58134-131">관리하려는 작업 영역을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58134-131">Click the workspace you want to manage.</span></span>

<span data-ttu-id="58134-132">작업 영역 페이지에는 다음 세 개의 탭이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58134-132">The workspace page has three tabs:</span></span>

* <span data-ttu-id="58134-133">**대시보드** - 작업 영역 사용 현황 및 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58134-133">**DASHBOARD** - Allows you to view workspace usage and information</span></span>
* <span data-ttu-id="58134-134">**구성** - 작업 영역에 대한 액세스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58134-134">**CONFIGURE** - Allows you to manage access to the workspace</span></span>
* <span data-ttu-id="58134-135">**웹 서비스** - 이 작업 영역에서 게시된 웹 서비스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58134-135">**WEB SERVICES** - Allows you to manage Web services that have been published from this workspace</span></span>

### <a name="to-monitor-how-the-workspace-is-being-used"></a><span data-ttu-id="58134-136">작업 영역이 사용되는 방식을 모니터링하려면</span><span class="sxs-lookup"><span data-stu-id="58134-136">To monitor how the workspace is being used</span></span>
<span data-ttu-id="58134-137">**대시보드 탭** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58134-137">Click the **DASHBOARD** tab.</span></span>

<span data-ttu-id="58134-138">대시보드에서 작업 영역의 전체 사용 현황을 살펴보고 작업 영역에 대한 개략적인 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58134-138">From the dashboard, you can view overall usage of your workspace and get a quick glance of workspace information.</span></span>

* <span data-ttu-id="58134-139">**계산** 차트는 작업 영역에서 사용되는 계산 리소스를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="58134-139">The **COMPUTE** chart shows the compute resources being used by the workspace.</span></span> <span data-ttu-id="58134-140">상대 값 또는 절대 값을 표시하도록 뷰를 변경하고 차트에 표시되는 기간을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58134-140">You can change the view to display relative or absolute values, and you can change the timeframe displayed in the chart.</span></span>
* <span data-ttu-id="58134-141">**사용 개요** 는 작업 영역에서 사용 중인 저장소를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="58134-141">**Usage overview** displays Azure storage being used by the workspace.</span></span>
* <span data-ttu-id="58134-142">**빠른 보기** 는 작업 영역 정보 및 유용한 링크의 요약 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="58134-142">**Quick glance** provides a summary of workspace information and useful links.</span></span>

> [!NOTE]
> <span data-ttu-id="58134-143">**ML 스튜디오에 로그인** 링크를 클릭하면 현재 로그인된 Microsoft 계정을 사용하여 기계 학습 스튜디오가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="58134-143">The **Sign-in to ML Studio** link opens Machine Learning Studio using the Microsoft Account you are currently signed into.</span></span> <span data-ttu-id="58134-144">Azure 클래식 포털에 로그인하여 작업 영역을 만드는 데 사용한 Microsoft 계정에는 해당 작업 영역을 열 수 있는 권한이 자동으로 부여되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="58134-144">The Microsoft Account you used to sign in to the Azure classic portal to create a workspace does not automatically have permission to open that workspace.</span></span> <span data-ttu-id="58134-145">작업 영역을 열려면 작업 영역의 소유자로 정의된 Microsoft 계정으로 로그인하거나 작업 공간 소유자의 참가 초대를 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58134-145">To open a workspace, you must be signed in to the Microsoft Account that was defined as the owner of the workspace, or you need to receive an invitation from the owner to join the workspace.</span></span>
> 
> 

### <a name="to-grant-or-suspend-access-for-users"></a><span data-ttu-id="58134-146">사용자에 대한 액세스 권한을 부여하거나 일시 중단하려면</span><span class="sxs-lookup"><span data-stu-id="58134-146">To grant or suspend access for users</span></span>
<span data-ttu-id="58134-147">**구성** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58134-147">Click the **CONFIGURE** tab.</span></span>

<span data-ttu-id="58134-148">구성 탭에서 수행할 수 있는 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="58134-148">From the configuration tab you can:</span></span>

* <span data-ttu-id="58134-149">거부를 클릭하여 기계 학습 작업 영역에 대한 액세스를 일시 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="58134-149">Suspend access to the Machine Learning workspace by clicking DENY.</span></span> <span data-ttu-id="58134-150">사용자는 더 이상 기계 학습 스튜디오에서 작업 영역을 열 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="58134-150">Users will no longer be able to open the workspace in Machine Learning Studio.</span></span> <span data-ttu-id="58134-151">액세스를 복원하려면 허용을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58134-151">To restore access, click ALLOW.</span></span>

<span data-ttu-id="58134-152">Machine Learning Studio의 작업 영역에 액세스할 수 있는 계정을 추가로 관리하려면 **대시보드** 탭에서 **ML Studio에 로그인**을 클릭합니다.(**ML Studio에 로그인**과 관련된 위 참고 사항 참조).</span><span class="sxs-lookup"><span data-stu-id="58134-152">To manage additional accounts who have access to the workspace in Machine Learning Studio, click **Sign-in to ML Studio** in the **DASHBOARD** tab (see the preceeding note regarding **Sign-in to ML Studio**).</span></span> <span data-ttu-id="58134-153">그러면 작업 영역에서 기계 학습 스튜디오가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="58134-153">This opens the workspace in Machine Learning Studio.</span></span> <span data-ttu-id="58134-154">여기서 **설정** 탭을 클릭한 다음 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58134-154">From here, click the **SETTINGS** tab and then **USERS**.</span></span> <span data-ttu-id="58134-155">**더 많은 사용자 초대**를 클릭하여 사용자에게 작업 영역에 대한 액세스 권한을 부여하거나 사용자를 선택하고 **제거**를 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58134-155">You can click **INVITE MORE USERS** to give users access to the workspace, or select a user and click **REMOVE**.</span></span>

### <a name="to-manage-web-services-in-this-workspace"></a><span data-ttu-id="58134-156">이 작업 영역에서 웹 서비스를 관리하려면</span><span class="sxs-lookup"><span data-stu-id="58134-156">To manage web services in this workspace</span></span>
<span data-ttu-id="58134-157">**웹 서비스** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58134-157">Click the **WEB SERVICES** tab.</span></span>

<span data-ttu-id="58134-158">이 작업 영역에서 게시된 웹 서비스의 목록이 표시될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="58134-158">This displays a list of web services published from this workspace.</span></span>
<span data-ttu-id="58134-159">웹 서비스를 관리하려면 목록에서 이름을 클릭하여 해당 웹 서비스 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="58134-159">To manage a web service, click the name in the list to open the Web service page.</span></span>

<span data-ttu-id="58134-160">웹 서비스에 정의된 끝점이 하나 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58134-160">A Web service may have one or more endpoints defined.</span></span>

* <span data-ttu-id="58134-161">"기본" 끝점 외에도 더 많은 끝점을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58134-161">You can define more endpoints in addition to the "Default" endpoint.</span></span> <span data-ttu-id="58134-162">끝점을 추가하려면 대시보드 아래에서 **끝점 관리**를 클릭하여 Azure Machine Learning 웹 서비스 포털을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="58134-162">To add the endpoint, click **Manage Endpoints** at the bottom of the dashboard to open the Azure Machine Learning Web Services portal.</span></span>
* <span data-ttu-id="58134-163">끝점을 삭제하려면 끝점 행의 시작 부분에 있는 확인란을 클릭한 다음 **삭제** 를 클릭합니다("기본" 끝점은 삭제할 수 없음).</span><span class="sxs-lookup"><span data-stu-id="58134-163">To delete an endpoint (you cannot delete the "Default" endpoint), click the check box at the beginning of the endpoint row, and click **DELETE**.</span></span> <span data-ttu-id="58134-164">그러면 웹 서비스에서 끝점을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="58134-164">This removes the endpoint from the Web service.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="58134-165">웹 서비스 끝점이 삭제될 때 응용 프로그램에서 웹 서비스 끝점을 사용 중이면 해당 응용 프로그램이 다음에 서비스에 액세스하려고 시도할 때 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="58134-165">If an application is using the web service endpoint when the endpoint is deleted, the application will receive an error the next time it tries to access the service.</span></span>
  > 
  > 

<span data-ttu-id="58134-166">웹 서비스 끝점의 이름을 클릭하여 해당 웹 서비스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="58134-166">Click the name of a Web service endpoint to open it.</span></span> 

<span data-ttu-id="58134-167">대시보드에서 일정 시간의 웹 서비스 전체 사용량을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58134-167">From the dashboard, you can view overall usage of your Web service over a period of time.</span></span> <span data-ttu-id="58134-168">사용량 차트의 오른쪽 위에 있는 기간 드롭다운 메뉴에서 보려는 기간을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58134-168">You can select the period to view from the Period dropdown menu in the upper right of the usage charts.</span></span> <span data-ttu-id="58134-169">대시보드에서는 다음 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="58134-169">The dashboard shows the following information:</span></span>

* <span data-ttu-id="58134-170">**시간에 따른 요청** 은 선택한 기간 동안 요청 수의 단계 그래프를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="58134-170">**Requests Over Time** displays a step graph of the number of requests over the selected time period.</span></span> <span data-ttu-id="58134-171">사용량이 급증하는 경우에 식별할 수 있도록 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="58134-171">It can help identify if you are experiencing spikes in usage.</span></span>
* <span data-ttu-id="58134-172">**요청-응답 요청** 은 선택한 기간 동안 서비스가 수신한 요청-응답 호출의 총 횟수 및 그 중 실패한 횟수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="58134-172">**Request-Response Requests** displays the total number of Request-Response calls the service has received over the selected time period and how many of them failed.</span></span>
* <span data-ttu-id="58134-173">**평균 요청-응답 계산 시간** 은 수신된 요청을 실행하는 데 필요한 시간의 평균을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="58134-173">**Average Request-Response Compute Time** displays an average of the time needed to execute the received requests.</span></span>
* <span data-ttu-id="58134-174">**배치 요청** 은 선택한 기간 동안 서비스가 수신한 배치 요청의 총 횟수 및 그 중 실패한 횟수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="58134-174">**Batch Requests** displays the total number of Batch Requests the service has received over the selected time period and how many of them failed.</span></span>
* <span data-ttu-id="58134-175">**평균 작업 대기** 는 수신된 요청을 실행하는 데 필요한 시간의 평균을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="58134-175">**Average Job Latency** displays an average of the time needed to execute the received requests.</span></span>
* <span data-ttu-id="58134-176">**오류** 웹 서비스 호출에서 발생한 오류의 집계 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="58134-176">**Errors** displays the aggregate number of errors that have occurred on calls to the web service.</span></span>
* <span data-ttu-id="58134-177">**서비스 비용** 은 서비스와 연결된 청구 계획에 대한 요금을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="58134-177">**Services Costs** displays the charges for the billing plan associated with the service.</span></span>

<span data-ttu-id="58134-178">구성 페이지에서 업데이트할 수 있는 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="58134-178">From the Configure page, you can update the following properties:</span></span>

* <span data-ttu-id="58134-179">**설명** 웹 서비스에 대한 설명을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58134-179">**Description** allows you to enter a description for the Web service.</span></span> <span data-ttu-id="58134-180">설명은 필수 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="58134-180">Description is a required field.</span></span>
* <span data-ttu-id="58134-181">**로깅** 오류 끝점에 대한 로깅을 사용하거나 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58134-181">**Logging** allows you to enable or disable error logging on the endpoint.</span></span> <span data-ttu-id="58134-182">로깅에 대한 자세한 내용은 [Machine Learning 웹 서비스에 대한 로깅 사용](machine-learning-web-services-logging.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="58134-182">For more information on Logging, see Enable [logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>
* <span data-ttu-id="58134-183">**샘플 데이터 사용** 요청-응답 서비스 테스트에 사용할 수 있는 샘플 데이터를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58134-183">**Enable Sample data** allows you to provide sample data that you can use to test the Request-Response service.</span></span> <span data-ttu-id="58134-184">기계 학습 스튜디오에서 웹 서비스를 만든 경우 샘플 데이터는 모델을 학습하는 데 사용된 데이터에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="58134-184">If you created the web service in Machine Learning Studio, the sample data is taken from the data your used to train your model.</span></span> <span data-ttu-id="58134-185">서비스를 프로그래밍 방식으로 만들 경우 JSON 패키지의 일부로 제공된 예제 데이터에서 가져온 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="58134-185">If you created the service programmatically, the data is taken from the example data you provided as part of the JSON package.</span></span>

