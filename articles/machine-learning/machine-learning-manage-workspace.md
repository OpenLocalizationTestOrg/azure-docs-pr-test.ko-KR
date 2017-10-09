---
title: "기계 학습 작업 영역 aaaManage | Microsoft Docs"
description: "액세스 tooAzure 기계 학습 작업 영역, 관리 및 배포 하 고 기계 학습 API 웹 서비스 관리"
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
ms.openlocfilehash: 7bd378d82aa46f4340ca974c7dc5a612c089cdca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-machine-learning-workspace"></a><span data-ttu-id="f8af7-103">Azure 기계 학습 작업 영역 관리</span><span class="sxs-lookup"><span data-stu-id="f8af7-103">Manage an Azure Machine Learning workspace</span></span>

> [!NOTE]
> <span data-ttu-id="f8af7-104">Hello 컴퓨터 학습 웹 서비스 포털에서 웹 서비스 관리에 대 한 자세한 내용은 참조 하십시오. [hello Azure 컴퓨터 학습 웹 서비스 포털을 사용 하 여 웹 서비스 관리](machine-learning-manage-new-webservice.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-104">For information on managing Web services in hello Machine Learning Web Services portal, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span>
> 
> 

<span data-ttu-id="f8af7-105">기계 학습 작업 영역 중 하나가 hello Azure 포털에서에서 관리 또는 Azure 클래식 포털 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-105">You can manage Machine Learning workspaces in either hello Azure portal or hello Azure classic portal.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="use-hello-azure-portal"></a><span data-ttu-id="f8af7-106">Hello Azure 포털을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="f8af7-106">Use hello Azure portal</span></span>

<span data-ttu-id="f8af7-107">toomanage hello Azure 포털에서에서 작업 영역:</span><span class="sxs-lookup"><span data-stu-id="f8af7-107">toomanage a workspace in hello Azure portal:</span></span>

1. <span data-ttu-id="f8af7-108">Toohello 로그인 [Azure 포털](https://portal.azure.com/) Azure 구독 관리자 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-108">Sign in toohello [Azure portal](https://portal.azure.com/) using an Azure subscription administrator account.</span></span>
2. <span data-ttu-id="f8af7-109">Hello hello 페이지 위쪽에 hello 검색 상자에 "기계 학습 작업 영역"을 입력 한 다음 선택 **기계 학습 작업 영역**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-109">In hello search box at hello top of hello page, enter "machine learning workspaces" and then select **Machine Learning Workspaces**.</span></span>
3. <span data-ttu-id="f8af7-110">원하는 toomanage hello 작업 영역을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-110">Click hello workspace you want toomanage.</span></span>

<span data-ttu-id="f8af7-111">또한 toohello 표준 리소스 관리 정보 및 사용할 수 있는 옵션을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-111">In addition toohello standard resource management information and options available, you can:</span></span>

- <span data-ttu-id="f8af7-112">보기 **속성** -이 페이지는 hello 작업 영역 및 리소스 정보를 표시 하 고 hello 구독 및 리소스 그룹에이 작업 영역 연결을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-112">View **Properties** - This page displays hello workspace and resource information, and you can change hello subscription and resource group that this workspace is connected with.</span></span>
- <span data-ttu-id="f8af7-113">**저장소 키를 다시 동기화** -hello 작업 영역 toohello 저장소 계정 키를 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-113">**Resync Storage Keys** - hello workspace maintains keys toohello storage account.</span></span> <span data-ttu-id="f8af7-114">Hello 저장소 계정 키를 변경 하는 경우 다음 클릭할 수 있는 **키를 다시 동기화** hello 작업 영역과 toosynchronize hello 키입니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-114">If hello storage account changes keys, then you can click **Resync keys** toosynchronize hello keys with hello workspace.</span></span>

<span data-ttu-id="f8af7-115">이 작업 영역과 연결 된 toomanage hello 웹 서비스는 hello 컴퓨터 학습 웹 서비스 포털을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-115">toomanage hello web services associated with this workspace, use hello Machine Learning Web Services portal.</span></span> <span data-ttu-id="f8af7-116">참조 [hello Azure 컴퓨터 학습 웹 서비스 포털을 사용 하 여 웹 서비스 관리](machine-learning-manage-new-webservice.md) 완전 한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-116">See [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md) for complete information.</span></span>

> [!NOTE]
> <span data-ttu-id="f8af7-117">toodeploy 참가자를 할당 해야 하는 새 웹 서비스를 관리 또는 hello 구독 toowhich hello 웹 서비스에 대 한 관리자 역할을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-117">toodeploy or manage New web services you must be assigned a contributor or administrator role on hello subscription toowhich hello web service is deployed.</span></span> <span data-ttu-id="f8af7-118">다른 사용자 tooa 기계 학습 작업 영역을 초대 배포 하거나 웹 서비스를 관리 하려면 해당를 tooa 참가자 또는 관리자 역할 hello 구독에 할당 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-118">If you invite another user tooa machine learning workspace, you must assign them tooa contributor or administrator role on hello subscription before they can deploy or manage web services.</span></span> 
> 
><span data-ttu-id="f8af7-119">액세스 권한 설정에 대 한 자세한 내용은 참조 하십시오. [hello Azure 포털-공개 미리 보기의에서 사용자 및 그룹에 대 한 보기 액세스 할당](../active-directory/role-based-access-control-manage-assignments.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-119">For more information on setting access permissions, see [View access assignments for users and groups in hello Azure portal - Public preview](../active-directory/role-based-access-control-manage-assignments.md).</span></span>

## <a name="use-hello-azure-classic-portal"></a><span data-ttu-id="f8af7-120">Hello Azure 클래식 포털을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="f8af7-120">Use hello Azure classic portal</span></span>

<span data-ttu-id="f8af7-121">Hello Azure 클래식 포털을 사용 하 여 기계 학습 작업 영역을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-121">Using hello Azure classic portal, you can manage your Machine Learning workspaces to:</span></span>

* <span data-ttu-id="f8af7-122">Hello 작업 영역 사용 되는 방식을 모니터링합니다</span><span class="sxs-lookup"><span data-stu-id="f8af7-122">Monitor how hello workspace is being used</span></span>
* <span data-ttu-id="f8af7-123">작업 영역 tooallow hello 구성 또는 액세스 거부</span><span class="sxs-lookup"><span data-stu-id="f8af7-123">Configure hello workspace tooallow or deny access</span></span>
* <span data-ttu-id="f8af7-124">Hello 작업 영역에서 만든 웹 서비스 관리</span><span class="sxs-lookup"><span data-stu-id="f8af7-124">Manage Web services created in hello workspace</span></span>
* <span data-ttu-id="f8af7-125">Hello 작업 영역 삭제</span><span class="sxs-lookup"><span data-stu-id="f8af7-125">Delete hello workspace</span></span>

<span data-ttu-id="f8af7-126">또한 hello 대시보드 탭 작업 영역 사용의 개요 및 작업 영역 정보의 빠른 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-126">In addition, hello dashboard tab provides an overview of your workspace usage and a quick glance of your workspace information.</span></span>  

> [!TIP]
> <span data-ttu-id="f8af7-127">Hello, Azure 기계 학습 스튜디오에서 **웹 서비스** 탭에 추가 하려면 업데이트 또는 컴퓨터 학습 웹 서비스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-127">In Azure Machine Learning Studio, on hello **WEB SERVICES** tab, you can add, update, or delete a Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="f8af7-128">toomanage hello Azure 클래식 포털에서에서 작업 영역:</span><span class="sxs-lookup"><span data-stu-id="f8af7-128">toomanage a workspace in hello Azure classic portal:</span></span>

1. <span data-ttu-id="f8af7-129">Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com/) Microsoft Azure를 사용 하 여 계정-Azure 구독 hello와 관련 된 hello 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-129">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) using your Microsoft Azure account - use hello account that's associated with hello Azure subscription.</span></span>
2. <span data-ttu-id="f8af7-130">Hello Microsoft Azure 서비스 패널에서 **기계 학습**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-130">In hello Microsoft Azure services panel, click **MACHINE LEARNING**.</span></span>
3. <span data-ttu-id="f8af7-131">원하는 toomanage hello 작업 영역을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-131">Click hello workspace you want toomanage.</span></span>

<span data-ttu-id="f8af7-132">hello 작업 영역 페이지는 세 개의 탭:</span><span class="sxs-lookup"><span data-stu-id="f8af7-132">hello workspace page has three tabs:</span></span>

* <span data-ttu-id="f8af7-133">**대시보드** -있습니다 tooview 작업 영역 사용 및 정보</span><span class="sxs-lookup"><span data-stu-id="f8af7-133">**DASHBOARD** - Allows you tooview workspace usage and information</span></span>
* <span data-ttu-id="f8af7-134">**구성** -toomanage access toohello 작업 영역 사용 하면</span><span class="sxs-lookup"><span data-stu-id="f8af7-134">**CONFIGURE** - Allows you toomanage access toohello workspace</span></span>
* <span data-ttu-id="f8af7-135">**웹 서비스** -이 작업 영역에서 게시 된 웹 서비스를 toomanage 있습니다</span><span class="sxs-lookup"><span data-stu-id="f8af7-135">**WEB SERVICES** - Allows you toomanage Web services that have been published from this workspace</span></span>

### <a name="toomonitor-how-hello-workspace-is-being-used"></a><span data-ttu-id="f8af7-136">toomonitor hello 작업 영역 사용 방법</span><span class="sxs-lookup"><span data-stu-id="f8af7-136">toomonitor how hello workspace is being used</span></span>
<span data-ttu-id="f8af7-137">Hello 클릭 **대시보드** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-137">Click hello **DASHBOARD** tab.</span></span>

<span data-ttu-id="f8af7-138">Hello 대시보드에서 작업 영역의 전체 사용량을 볼 수 있으며 작업 영역 정보 빠르게 확인할 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-138">From hello dashboard, you can view overall usage of your workspace and get a quick glance of workspace information.</span></span>

* <span data-ttu-id="f8af7-139">hello **계산** 차트 hello 작업 영역에서 사용 되 고 hello 계산 리소스를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-139">hello **COMPUTE** chart shows hello compute resources being used by hello workspace.</span></span> <span data-ttu-id="f8af7-140">Hello 보기 toodisplay 상대 또는 절대 값을 변경할 수 있습니다 및 hello 차트에 표시 된 hello 시간을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-140">You can change hello view toodisplay relative or absolute values, and you can change hello timeframe displayed in hello chart.</span></span>
* <span data-ttu-id="f8af7-141">**사용 개요** hello 작업 영역에서 사용 중인 Azure 저장소가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-141">**Usage overview** displays Azure storage being used by hello workspace.</span></span>
* <span data-ttu-id="f8af7-142">**빠른 보기** 는 작업 영역 정보 및 유용한 링크의 요약 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-142">**Quick glance** provides a summary of workspace information and useful links.</span></span>

> [!NOTE]
> <span data-ttu-id="f8af7-143">hello **로그인 tooML Studio** 링크 hello 현재 로그인 하는 Microsoft 계정을 사용 하 여 기계 학습 스튜디오를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-143">hello **Sign-in tooML Studio** link opens Machine Learning Studio using hello Microsoft Account you are currently signed into.</span></span> <span data-ttu-id="f8af7-144">hello toosign toohello Azure 클래식 포털 toocreate 작업 영역에서에서 사용한 Microsoft 계정에 자동으로 없는 권한 tooopen 작업 영역을 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-144">hello Microsoft Account you used toosign in toohello Azure classic portal toocreate a workspace does not automatically have permission tooopen that workspace.</span></span> <span data-ttu-id="f8af7-145">작업 영역에서 tooopen toohello hello 영역의 hello 소유자로 정의 된 Microsoft 계정에에서 서명 해야 하거나 tooreceive hello 소유자 toojoin hello 작업 영역에서 초대장이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-145">tooopen a workspace, you must be signed in toohello Microsoft Account that was defined as hello owner of hello workspace, or you need tooreceive an invitation from hello owner toojoin hello workspace.</span></span>
> 
> 

### <a name="toogrant-or-suspend-access-for-users"></a><span data-ttu-id="f8af7-146">toogrant 또는 사용자에 대 한 액세스를 일시 중단</span><span class="sxs-lookup"><span data-stu-id="f8af7-146">toogrant or suspend access for users</span></span>
<span data-ttu-id="f8af7-147">Hello 클릭 **구성** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-147">Click hello **CONFIGURE** tab.</span></span>

<span data-ttu-id="f8af7-148">Hello 구성 탭에서 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-148">From hello configuration tab you can:</span></span>

* <span data-ttu-id="f8af7-149">Toohello 기계 학습 작업 영역 액세스 거부를 클릭 하 여 일시 중단 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-149">Suspend access toohello Machine Learning workspace by clicking DENY.</span></span> <span data-ttu-id="f8af7-150">사용자가 더 이상 기계 학습 스튜디오에서 수 tooopen hello 작업 영역 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-150">Users will no longer be able tooopen hello workspace in Machine Learning Studio.</span></span> <span data-ttu-id="f8af7-151">toorestore 액세스 허용을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-151">toorestore access, click ALLOW.</span></span>

<span data-ttu-id="f8af7-152">기계 학습 스튜디오에서 작업 한 toohello 영역 액세스 권한이 있는 toomanage 추가 계정을 클릭 **로그인 tooML Studio** hello에 **대시보드** 탭 (hello 앞에 오는 참고 참조에 대 한  **Studio tooML Sign-in**).</span><span class="sxs-lookup"><span data-stu-id="f8af7-152">toomanage additional accounts who have access toohello workspace in Machine Learning Studio, click **Sign-in tooML Studio** in hello **DASHBOARD** tab (see hello preceeding note regarding **Sign-in tooML Studio**).</span></span> <span data-ttu-id="f8af7-153">작업 영역을 hello 기계 학습 스튜디오에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-153">This opens hello workspace in Machine Learning Studio.</span></span> <span data-ttu-id="f8af7-154">여기에서 클릭 hello **설정** 탭 한 다음 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-154">From here, click hello **SETTINGS** tab and then **USERS**.</span></span> <span data-ttu-id="f8af7-155">클릭할 수 있는 **더 사용자 초대** toogive 사용자 toohello 작업 영역 액세스 또는 사용자 선택 하 고 클릭 **제거**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-155">You can click **INVITE MORE USERS** toogive users access toohello workspace, or select a user and click **REMOVE**.</span></span>

### <a name="toomanage-web-services-in-this-workspace"></a><span data-ttu-id="f8af7-156">이 작업 영역에서 toomanage 웹 서비스</span><span class="sxs-lookup"><span data-stu-id="f8af7-156">toomanage web services in this workspace</span></span>
<span data-ttu-id="f8af7-157">Hello 클릭 **웹 서비스** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-157">Click hello **WEB SERVICES** tab.</span></span>

<span data-ttu-id="f8af7-158">이 작업 영역에서 게시된 웹 서비스의 목록이 표시될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-158">This displays a list of web services published from this workspace.</span></span>
<span data-ttu-id="f8af7-159">toomanage 웹 서비스에는 hello 목록 tooopen hello 웹 서비스 페이지에 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-159">toomanage a web service, click hello name in hello list tooopen hello Web service page.</span></span>

<span data-ttu-id="f8af7-160">웹 서비스에 정의된 끝점이 하나 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-160">A Web service may have one or more endpoints defined.</span></span>

* <span data-ttu-id="f8af7-161">또한 toohello "Default" 끝점에서 더 많은 끝점을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-161">You can define more endpoints in addition toohello "Default" endpoint.</span></span> <span data-ttu-id="f8af7-162">tooadd 끝점 hello, 클릭 **관리 끝점** hello hello 대시보드 tooopen hello Azure 컴퓨터 학습 웹 서비스 포털 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-162">tooadd hello endpoint, click **Manage Endpoints** at hello bottom of hello dashboard tooopen hello Azure Machine Learning Web Services portal.</span></span>
* <span data-ttu-id="f8af7-163">toodelete (hello "Default" 끝점을 삭제할 수 없음) 끝점을 hello 끝점 행 hello 시작 시 hello 확인란을 클릭 하 고 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-163">toodelete an endpoint (you cannot delete hello "Default" endpoint), click hello check box at hello beginning of hello endpoint row, and click **DELETE**.</span></span> <span data-ttu-id="f8af7-164">이렇게 하면 hello 끝점 hello 웹 서비스에서에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-164">This removes hello endpoint from hello Web service.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="f8af7-165">Hello 끝점 삭제 될 때 응용 프로그램에서 hello 웹 서비스 끝점을 사용 하는, 다음 번 tooaccess hello 서비스 시도 hello 응용 프로그램 오류 hello를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-165">If an application is using hello web service endpoint when hello endpoint is deleted, hello application will receive an error hello next time it tries tooaccess hello service.</span></span>
  > 
  > 

<span data-ttu-id="f8af7-166">웹 서비스 끝점 tooopen의 hello 이름을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-166">Click hello name of a Web service endpoint tooopen it.</span></span> 

<span data-ttu-id="f8af7-167">Hello 대시보드에서 시간 동안 웹 서비스의 전반적인 사용량을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-167">From hello dashboard, you can view overall usage of your Web service over a period of time.</span></span> <span data-ttu-id="f8af7-168">Hello 기간 tooview hello hello 사용 현황 차트의 오른쪽 위에 있는 hello 기간 드롭다운 메뉴에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-168">You can select hello period tooview from hello Period dropdown menu in hello upper right of hello usage charts.</span></span> <span data-ttu-id="f8af7-169">hello 대시보드 hello 다음 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-169">hello dashboard shows hello following information:</span></span>

* <span data-ttu-id="f8af7-170">**시간에 따른 요청** hello 특정 기간을 통해 요청 hello 수 단계 그래프를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-170">**Requests Over Time** displays a step graph of hello number of requests over hello selected time period.</span></span> <span data-ttu-id="f8af7-171">사용량이 급증하는 경우에 식별할 수 있도록 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-171">It can help identify if you are experiencing spikes in usage.</span></span>
* <span data-ttu-id="f8af7-172">**요청-응답 요청** hello hello 서비스 hello 선택한 기간 및 그 중 실패 한를 통해 수신한 요청-응답 호출의 총 수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-172">**Request-Response Requests** displays hello total number of Request-Response calls hello service has received over hello selected time period and how many of them failed.</span></span>
* <span data-ttu-id="f8af7-173">**평균 시간을 계산 하는 요청-응답** hello 시간의 평균을 표시 tooexecute hello 받은 요청 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-173">**Average Request-Response Compute Time** displays an average of hello time needed tooexecute hello received requests.</span></span>
* <span data-ttu-id="f8af7-174">**일괄 처리 요청** 표시 hello의 총 일괄 처리 요청 hello 서비스 기간을 선택 하는 hello를 통해을 얼마나 많이 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-174">**Batch Requests** displays hello total number of Batch Requests hello service has received over hello selected time period and how many of them failed.</span></span>
* <span data-ttu-id="f8af7-175">**평균 작업 대기 시간** hello 시간의 평균을 표시 tooexecute hello 받은 요청 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-175">**Average Job Latency** displays an average of hello time needed tooexecute hello received requests.</span></span>
* <span data-ttu-id="f8af7-176">**오류** toohello 웹 서비스 호출에서 발생 한 오류를 hello 집계 수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-176">**Errors** displays hello aggregate number of errors that have occurred on calls toohello web service.</span></span>
* <span data-ttu-id="f8af7-177">**서비스 비용** hello 서비스와 연결 된 hello 청구 계획에 대 한 hello 요금을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-177">**Services Costs** displays hello charges for hello billing plan associated with hello service.</span></span>

<span data-ttu-id="f8af7-178">Hello 구성 페이지에서 다음과 같은 속성 hello를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-178">From hello Configure page, you can update hello following properties:</span></span>

* <span data-ttu-id="f8af7-179">**설명** tooenter hello 웹 서비스에 대 한 설명이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-179">**Description** allows you tooenter a description for hello Web service.</span></span> <span data-ttu-id="f8af7-180">설명은 필수 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-180">Description is a required field.</span></span>
* <span data-ttu-id="f8af7-181">**로깅** hello 끝점에 대 한 로깅을 tooenable 또는 사용 안 함 오류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-181">**Logging** allows you tooenable or disable error logging on hello endpoint.</span></span> <span data-ttu-id="f8af7-182">로깅에 대한 자세한 내용은 [Machine Learning 웹 서비스에 대한 로깅 사용](machine-learning-web-services-logging.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f8af7-182">For more information on Logging, see Enable [logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>
* <span data-ttu-id="f8af7-183">**예제 데이터 사용** tooprovide 예제 데이터 tootest hello 요청 응답 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-183">**Enable Sample data** allows you tooprovide sample data that you can use tootest hello Request-Response service.</span></span> <span data-ttu-id="f8af7-184">기계 학습 스튜디오에서 hello 웹 서비스를 만든 경우 hello 예제 데이터에서에서 가져온 것 hello 데이터에 사용 되는 tootrain 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-184">If you created hello web service in Machine Learning Studio, hello sample data is taken from hello data your used tootrain your model.</span></span> <span data-ttu-id="f8af7-185">Hello 서비스를 프로그래밍 방식으로 만든 경우 hello 데이터 hello JSON 패키지의 일부로 제공 하는 hello 예제 데이터에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f8af7-185">If you created hello service programmatically, hello data is taken from hello example data you provided as part of hello JSON package.</span></span>

