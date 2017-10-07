---
title: "어떻게 toomanage AzureML 웹 서비스 API 관리를 사용 하 여 aaaLearn | Microsoft Docs"
description: "API 관리를 사용 하 여 toomanage AzureML 웹을 서비스 하는 방법을 보여 주는 가이드입니다."
keywords: "기계 학습, api 관리"
services: machine-learning
documentationcenter: 
author: roalexan
manager: jhubbard
editor: 
ms.assetid: 05150ae1-5b6a-4d25-ac67-fb2f24a68e8d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/19/2017
ms.author: roalexan
ms.openlocfilehash: 6e764fbfd71be6cc908a1c8d3d8889969fc651a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-how-toomanage-azureml-web-services-using-api-management"></a><span data-ttu-id="20034-104">API 관리를 사용 하 여 toomanage AzureML 웹을 서비스 하는 방법에 대해 알아봅니다</span><span class="sxs-lookup"><span data-stu-id="20034-104">Learn how toomanage AzureML web services using API Management</span></span>
## <a name="overview"></a><span data-ttu-id="20034-105">개요</span><span class="sxs-lookup"><span data-stu-id="20034-105">Overview</span></span>
<span data-ttu-id="20034-106">이 가이드에서는 tooquickly AzureML 웹 서비스 API 관리 toomanage를 사용 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-106">This guide shows you how tooquickly get started using API Management toomanage your AzureML web services.</span></span>

## <a name="what-is-azure-api-management"></a><span data-ttu-id="20034-107">Azure API 관리란?</span><span class="sxs-lookup"><span data-stu-id="20034-107">What is Azure API Management?</span></span>
<span data-ttu-id="20034-108">Azure API 관리는 사용자 액세스, 사용 제한 및 대시보드 모니터링을 정의하여 REST API 끝점을 관리할 수 있는 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="20034-108">Azure API Management is an Azure service that lets you manage your REST API endpoints by defining user access, usage throttling, and dashboard monitoring.</span></span> <span data-ttu-id="20034-109">Azure API 관리에 대한 자세한 내용은 [여기](https://azure.microsoft.com/services/api-management/) 를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="20034-109">Click [here](https://azure.microsoft.com/services/api-management/) for details on Azure API Management.</span></span> <span data-ttu-id="20034-110">클릭 [여기](../api-management/api-management-get-started.md) tooget Azure API 관리 시작 하는 방법에 대 한 지침에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-110">Click [here](../api-management/api-management-get-started.md) for a guide on how tooget started with Azure API Management.</span></span> <span data-ttu-id="20034-111">이 가이드를 기반으로 하는 이 다른 가이드에서는 알림 구성, 가격 책정 계층, 응답 처리, 사용자 인증, 제품 생산, 개발자 구독 및 사용량 대시보딩을 포함하는 다양한 주제를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="20034-111">This other guide, which this guide is based on, covers more topics, including notification configurations, tier pricing, response handling, user authentication, creating products, developer subscriptions, and usage dashboarding.</span></span>

## <a name="what-is-azureml"></a><span data-ttu-id="20034-112">AzureML이란?</span><span class="sxs-lookup"><span data-stu-id="20034-112">What is AzureML?</span></span>
<span data-ttu-id="20034-113">AzureML는 tooeasily 빌드 수 있도록 하는 기계 학습에 대 한 Azure 서비스, 배포 및 고급 분석 솔루션 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-113">AzureML is an Azure service for machine learning that enables you tooeasily build, deploy, and share advanced analytics solutions.</span></span> <span data-ttu-id="20034-114">AzureML에 대한 자세한 내용은 [여기](https://azure.microsoft.com/services/machine-learning/) 를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="20034-114">Click [here](https://azure.microsoft.com/services/machine-learning/) for details on AzureML.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20034-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="20034-115">Prerequisites</span></span>
<span data-ttu-id="20034-116">toocomplete 해야이 가이드:</span><span class="sxs-lookup"><span data-stu-id="20034-116">toocomplete this guide, you need:</span></span>

* <span data-ttu-id="20034-117">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="20034-117">An Azure account.</span></span> <span data-ttu-id="20034-118">Azure 계정이 없으면 클릭 [여기](https://azure.microsoft.com/pricing/free-trial/) 방법에 대 한 자세한 내용은 toocreate 무료 평가판 계정 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-118">If you don’t have an Azure account, click [here](https://azure.microsoft.com/pricing/free-trial/) for details on how toocreate a free trial account.</span></span>
* <span data-ttu-id="20034-119">AzureML 계정.</span><span class="sxs-lookup"><span data-stu-id="20034-119">An AzureML account.</span></span> <span data-ttu-id="20034-120">AzureML 계정이 없으면 클릭 [여기](https://studio.azureml.net/) 방법에 대 한 자세한 내용은 toocreate 무료 평가판 계정 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-120">If you don’t have an AzureML account, click [here](https://studio.azureml.net/) for details on how toocreate a free trial account.</span></span>
* <span data-ttu-id="20034-121">hello 작업 영역, 서비스 및 웹 서비스로 배포 AzureML 실험에 api_key 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-121">hello workspace, service, and api_key for an AzureML experiment deployed as a web service.</span></span> <span data-ttu-id="20034-122">클릭 [여기](machine-learning-create-experiment.md) toocreate는 AzureML 실험 하는 방법에 대 한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-122">Click [here](machine-learning-create-experiment.md) for details on how toocreate an AzureML experiment.</span></span> <span data-ttu-id="20034-123">클릭 [여기](machine-learning-publish-a-machine-learning-web-service.md) 웹 서비스로 toodeploy는 AzureML 실험 하는 방법에 대 한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-123">Click [here](machine-learning-publish-a-machine-learning-web-service.md) for details on how toodeploy an AzureML experiment as a web service.</span></span> <span data-ttu-id="20034-124">또는 부록 A toocreate 및 간단한 AzureML 테스트 실험 하 고 웹 서비스로 배포 방법에 대 한 지침에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20034-124">Alternately, Appendix A has instructions for how toocreate and test a simple AzureML experiment and deploy it as a web service.</span></span>

## <a name="create-an-api-management-instance"></a><span data-ttu-id="20034-125">API 관리 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="20034-125">Create an API Management instance</span></span>
<span data-ttu-id="20034-126">AzureML 웹 서비스 API 관리 toomanage를 사용 하 여 hello 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="20034-126">Below are hello steps for using API Management toomanage your AzureML web service.</span></span> <span data-ttu-id="20034-127">먼저 서비스 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="20034-127">First create a service instance.</span></span> <span data-ttu-id="20034-128">Toohello 로그인 [클래식 포털](https://manage.windowsazure.com/) 클릭 **새로** > **응용 프로그램 서비스** > **API 관리**  >  **만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-128">Log in toohello [Classic Portal](https://manage.windowsazure.com/) and click **New** > **App Services** > **API Management** > **Create**.</span></span>

![create-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-instance.png)

<span data-ttu-id="20034-130">고유한 **URL**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-130">Specify a unique **URL**.</span></span> <span data-ttu-id="20034-131">이 가이드에서는 **demoazureml** – 해야 toochoose 서로 다른 무엇 인가입니다.</span><span class="sxs-lookup"><span data-stu-id="20034-131">This guide uses **demoazureml** – you will need toochoose something different.</span></span> <span data-ttu-id="20034-132">원하는 hello 선택 **구독** 및 **지역** 서비스 인스턴스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-132">Choose hello desired **Subscription** and **Region** for your service instance.</span></span> <span data-ttu-id="20034-133">선택 항목에 확인 한 후 hello 다음 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-133">After making your selections, click hello next button.</span></span>

![create-service-1](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-1.png)

<span data-ttu-id="20034-135">Hello에 대 한 값을 지정 **조직 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-135">Specify a value for hello **Organization Name**.</span></span> <span data-ttu-id="20034-136">이 가이드에서는 **demoazureml** – 해야 toochoose 서로 다른 무엇 인가입니다.</span><span class="sxs-lookup"><span data-stu-id="20034-136">This guide uses **demoazureml** – you will need toochoose something different.</span></span> <span data-ttu-id="20034-137">Hello에 전자 메일 주소를 입력 **관리자 전자 메일** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="20034-137">Enter your email address in hello **administrator e-mail** field.</span></span> <span data-ttu-id="20034-138">이 전자 메일 주소는 hello API 관리 시스템에서에서 알림에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="20034-138">This email address is used for notifications from hello API Management system.</span></span>

![create-service-2](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-2.png)

<span data-ttu-id="20034-140">Hello 확인란 toocreate 서비스 인스턴스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-140">Click hello check box toocreate your service instance.</span></span> <span data-ttu-id="20034-141">*만든 새 서비스 toobe toothirty 분 차지*합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-141">*It takes up toothirty minutes for a new service toobe created*.</span></span>

## <a name="create-hello-api"></a><span data-ttu-id="20034-142">Hello API 만들기</span><span class="sxs-lookup"><span data-stu-id="20034-142">Create hello API</span></span>
<span data-ttu-id="20034-143">Hello 서비스 인스턴스를 만든 후 hello 다음 단계는 toocreate hello API입니다.</span><span class="sxs-lookup"><span data-stu-id="20034-143">Once hello service instance is created, hello next step is toocreate hello API.</span></span> <span data-ttu-id="20034-144">API는 클라이언트 응용 프로그램에서 호출할 수 있는 작업 집합으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="20034-144">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="20034-145">API 작업은 웹 서비스 프록시 tooexisting입니다.</span><span class="sxs-lookup"><span data-stu-id="20034-145">API operations are proxied tooexisting web services.</span></span> <span data-ttu-id="20034-146">이 가이드는 기존 AzureML RR 및 BES 웹 서비스 프록시 toohello 해당 Api를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="20034-146">This guide creates APIs that proxy toohello existing AzureML RRS and BES web services.</span></span>

<span data-ttu-id="20034-147">Api 생성 및 hello Azure 클래식 포털을 통해 액세스할 수 있는 hello API 게시자 포털에서 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="20034-147">APIs are created and configured from hello API publisher portal, which is accessed through hello Azure Classic Portal.</span></span> <span data-ttu-id="20034-148">tooreach는 서비스 인스턴스를 게시자 포털에서 선택 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-148">tooreach hello publisher portal, select your service instance.</span></span>

![select-service-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-service-instance.png)

<span data-ttu-id="20034-150">클릭 **관리** API 관리 서비스에 대 한 hello Azure 클래식 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="20034-150">Click **Manage** in hello Azure Classic Portal for your API Management service.</span></span>

![manage-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/manage-service.png)

<span data-ttu-id="20034-152">클릭 **Api** hello에서 **API 관리** 를 hello 왼쪽, 클릭 한 다음 메뉴 **추가 API**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-152">Click **APIs** from hello **API Management** menu on hello left, and then click **Add API**.</span></span>

![api-management-menu](./media/machine-learning-manage-web-service-endpoints-using-api-management/api-management-menu.png)

<span data-ttu-id="20034-154">형식 **AzureML 데모 API** hello로 **웹 API 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-154">Type **AzureML Demo API** as hello **Web API name**.</span></span> <span data-ttu-id="20034-155">형식 **https://ussouthcentral.services.azureml.net** hello로 **웹 서비스 URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-155">Type **https://ussouthcentral.services.azureml.net** as hello **Web service URL**.</span></span> <span data-ttu-id="20034-156">형식 **azureml 데모** hello로 **웹 API URL 접미사**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-156">Type **azureml-demo** as hello **Web API URL suffix**.</span></span> <span data-ttu-id="20034-157">확인 **HTTPS** hello로 **웹 API URL** 구성표입니다.</span><span class="sxs-lookup"><span data-stu-id="20034-157">Check **HTTPS** as hello **Web API URL** scheme.</span></span> <span data-ttu-id="20034-158">**시작**을 **제품**으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-158">Select **Starter** as **Products**.</span></span> <span data-ttu-id="20034-159">완료 되 면 클릭 **저장** toocreate hello API입니다.</span><span class="sxs-lookup"><span data-stu-id="20034-159">When finished, click **Save** toocreate hello API.</span></span>

![add-new-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-new-api.png)

## <a name="add-hello-operations"></a><span data-ttu-id="20034-161">Hello 작업 추가</span><span class="sxs-lookup"><span data-stu-id="20034-161">Add hello operations</span></span>
<span data-ttu-id="20034-162">클릭 **추가 작업이** tooadd operations toothis API입니다.</span><span class="sxs-lookup"><span data-stu-id="20034-162">Click **Add operation** tooadd operations toothis API.</span></span>

![add-operation](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-operation.png)

<span data-ttu-id="20034-164">hello **새 작업** 창이 표시 되 고 hello **서명** 탭이 기본적으로 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="20034-164">hello **New operation** window will be displayed and hello **Signature** tab will be selected by default.</span></span>

## <a name="add-rrs-operation"></a><span data-ttu-id="20034-165">RRS 작업 추가</span><span class="sxs-lookup"><span data-stu-id="20034-165">Add RRS Operation</span></span>
<span data-ttu-id="20034-166">먼저 hello AzureML RR 서비스에 대 한 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="20034-166">First create an operation for hello AzureML RRS service.</span></span> <span data-ttu-id="20034-167">선택 **POST** hello로 **HTTP 동사**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-167">Select **POST** as hello **HTTP verb**.</span></span> <span data-ttu-id="20034-168">형식 **/workspaces/ {작업 영역} /services/ {서비스} / 실행? api 버전 {apiversion} = & 세부 정보 = {자세히}** hello로 **URL 템플릿**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-168">Type **/workspaces/{workspace}/services/{service}/execute?api-version={apiversion}&details={details}** as hello **URL template**.</span></span> <span data-ttu-id="20034-169">형식 **RR 실행** hello로 **표시 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-169">Type **RRS Execute** as hello **Display name**.</span></span>

![add-rrs-operation-signature](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

<span data-ttu-id="20034-171">클릭 **응답** > **추가** 왼쪽과 선택 hello에 **200 확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-171">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="20034-172">클릭 **저장** toosave이이 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-172">Click **Save** toosave this operation.</span></span>

![add-rrs-operation-response](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a><span data-ttu-id="20034-174">BES 작업 추가</span><span class="sxs-lookup"><span data-stu-id="20034-174">Add BES Operations</span></span>
<span data-ttu-id="20034-175">스크린 샷을 대 한 포함 되지 않습니다. hello RR 작업을 추가 하기 위한 매우 유사한 toothose 멤버인 BES 작업 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-175">Screenshots are not included for hello BES operations as they are very similar toothose for adding hello RRS operation.</span></span>

### <a name="submit-but-not-start-a-batch-execution-job"></a><span data-ttu-id="20034-176">일괄 처리 실행 작업 제출(시작하지는 않음)</span><span class="sxs-lookup"><span data-stu-id="20034-176">Submit (but not start) a Batch Execution job</span></span>
<span data-ttu-id="20034-177">클릭 **추가 작업이** tooadd hello AzureML BES 작업 toohello API입니다.</span><span class="sxs-lookup"><span data-stu-id="20034-177">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="20034-178">선택 **POST** hello에 대 한 **HTTP 동사**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-178">Select **POST** for hello **HTTP verb**.</span></span> <span data-ttu-id="20034-179">형식 **/workspaces/ {작업 영역} /services/ {서비스 (를) 작업 /? api 버전 {apiversion} =** hello에 대 한 **URL 템플릿**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-179">Type **/workspaces/{workspace}/services/{service}/jobs?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="20034-180">형식 **BES 제출** hello에 대 한 **표시 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-180">Type **BES Submit** for hello **Display name**.</span></span> <span data-ttu-id="20034-181">클릭 **응답** > **추가** 왼쪽과 선택 hello에 **200 확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-181">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="20034-182">클릭 **저장** toosave이이 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-182">Click **Save** toosave this operation.</span></span>

### <a name="start-a-batch-execution-job"></a><span data-ttu-id="20034-183">일괄 처리 실행 작업 시작</span><span class="sxs-lookup"><span data-stu-id="20034-183">Start a Batch Execution job</span></span>
<span data-ttu-id="20034-184">클릭 **추가 작업이** tooadd hello AzureML BES 작업 toohello API입니다.</span><span class="sxs-lookup"><span data-stu-id="20034-184">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="20034-185">선택 **POST** hello에 대 한 **HTTP 동사**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-185">Select **POST** for hello **HTTP verb**.</span></span> <span data-ttu-id="20034-186">형식 **/workspaces/ {작업 영역} {서비스} /services/ /jobs/ {jobid} / 시작? api 버전 {apiversion} =** hello에 대 한 **URL 템플릿**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-186">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}/start?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="20034-187">형식 **BES 시작** hello에 대 한 **표시 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-187">Type **BES Start** for hello **Display name**.</span></span> <span data-ttu-id="20034-188">클릭 **응답** > **추가** 왼쪽과 선택 hello에 **200 확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-188">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="20034-189">클릭 **저장** toosave이이 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-189">Click **Save** toosave this operation.</span></span>

### <a name="get-hello-status-or-result-of-a-batch-execution-job"></a><span data-ttu-id="20034-190">Hello 상태 또는 일괄 처리 실행 작업의 결과 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="20034-190">Get hello status or result of a Batch Execution job</span></span>
<span data-ttu-id="20034-191">클릭 **추가 작업이** tooadd hello AzureML BES 작업 toohello API입니다.</span><span class="sxs-lookup"><span data-stu-id="20034-191">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="20034-192">선택 **가져오기** hello에 대 한 **HTTP 동사**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-192">Select **GET** for hello **HTTP verb**.</span></span> <span data-ttu-id="20034-193">형식 **/workspaces/ {작업 영역} {서비스} /services/ /jobs/ {jobid}? api 버전 {apiversion} =** hello에 대 한 **URL 템플릿**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-193">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="20034-194">형식 **BES 상태** hello에 대 한 **표시 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-194">Type **BES Status** for hello **Display name**.</span></span> <span data-ttu-id="20034-195">클릭 **응답** > **추가** 왼쪽과 선택 hello에 **200 확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-195">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="20034-196">클릭 **저장** toosave이이 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-196">Click **Save** toosave this operation.</span></span>

### <a name="delete-a-batch-execution-job"></a><span data-ttu-id="20034-197">일괄 처리 실행 작업 삭제</span><span class="sxs-lookup"><span data-stu-id="20034-197">Delete a Batch Execution job</span></span>
<span data-ttu-id="20034-198">클릭 **추가 작업이** tooadd hello AzureML BES 작업 toohello API입니다.</span><span class="sxs-lookup"><span data-stu-id="20034-198">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="20034-199">선택 **삭제** hello에 대 한 **HTTP 동사**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-199">Select **DELETE** for hello **HTTP verb**.</span></span> <span data-ttu-id="20034-200">형식 **/workspaces/ {작업 영역} {서비스} /services/ /jobs/ {jobid}? api 버전 {apiversion} =** hello에 대 한 **URL 템플릿**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-200">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="20034-201">형식 **BES 삭제** hello에 대 한 **표시 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-201">Type **BES Delete** for hello **Display name**.</span></span> <span data-ttu-id="20034-202">클릭 **응답** > **추가** 왼쪽과 선택 hello에 **200 확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-202">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="20034-203">클릭 **저장** toosave이이 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-203">Click **Save** toosave this operation.</span></span>

## <a name="call-an-operation-from-hello-developer-portal"></a><span data-ttu-id="20034-204">Hello 개발자 포털에서에서 작업 호출</span><span class="sxs-lookup"><span data-stu-id="20034-204">Call an operation from hello Developer Portal</span></span>
<span data-ttu-id="20034-205">작업 편리 tooview 제공 하는 hello 개발자 포털에서 직접 호출할 수 있습니다 및 API의 hello 작동을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-205">Operations can be called directly from hello Developer portal, which provides a convenient way tooview and test hello operations of an API.</span></span> <span data-ttu-id="20034-206">호출 하 게이 가이드 단계에서는 hello **RR 실행** toohello 추가 된 메서드가 **AzureML 데모 API**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-206">In this guide step you will call hello **RRS Execute** method that was added toohello **AzureML Demo API**.</span></span> <span data-ttu-id="20034-207">클릭 **개발자 포털** hello에 hello 메뉴에서 hello 클래식 포털의 오른쪽 위에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20034-207">Click **Developer portal** from hello menu at hello top right of hello Classic Portal.</span></span>

![developer-portal](./media/machine-learning-manage-web-service-endpoints-using-api-management/developer-portal.png)

<span data-ttu-id="20034-209">클릭 **Api** hello 상단 메뉴에서 **AzureML 데모 API** toosee hello 작업의 상태를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20034-209">Click **APIs** from hello top menu, and then click **AzureML Demo API** toosee hello operations available.</span></span>

![demoazureml-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/demoazureml-api.png)

<span data-ttu-id="20034-211">선택 **RR 실행** hello 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-211">Select **RRS Execute** for hello operation.</span></span> <span data-ttu-id="20034-212">**사용해 보세요.**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-212">Click **Try It**.</span></span>

![try-it](./media/machine-learning-manage-web-service-endpoints-using-api-management/try-it.png)

<span data-ttu-id="20034-214">요청 매개 변수를 입력 하면 **작업 영역**, **서비스**, **2.0** hello에 대 한 **apiversion**, 및 **true**hello에 대 한 **세부 정보**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-214">For Request parameters, type your **workspace**,  **service**, **2.0** for hello **apiversion**, and  **true** for hello **details**.</span></span> <span data-ttu-id="20034-215">찾을 수 있습니다 프로그램 **작업 영역** 및 **서비스** hello AzureML 웹 서비스 대시보드에서 (참조 **hello 웹 서비스를 테스트할** 부록 A).</span><span class="sxs-lookup"><span data-stu-id="20034-215">You can find your **workspace** and **service** in hello AzureML web service dashboard (see **Test hello web service** in Appendix A).</span></span>

<span data-ttu-id="20034-216">요청 헤더로는 **헤더 추가**를 클릭하고 **콘텐츠 유형** 및 **application/json**을 입력하고 나서, **헤더 추가**를 클릭하고 **자동화** 및 **전달자<YOUR AZUREML SERVICE API-KEY>**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-216">For Request headers, click **Add header** and type **Content-Type** and **application/json**, then click **Add header** and type **Authorization** and **Bearer <YOUR AZUREML SERVICE API-KEY>**.</span></span> <span data-ttu-id="20034-217">찾을 수 있습니다 프로그램 **api 키** hello AzureML 웹 서비스 대시보드에서 (참조 **hello 웹 서비스를 테스트할** 부록 A).</span><span class="sxs-lookup"><span data-stu-id="20034-217">You can find your **api key** in hello AzureML web service dashboard (see **Test hello web service** in Appendix A).</span></span>

<span data-ttu-id="20034-218">형식 **{"입력": {"input1": {"ColumnNames": "값" ["Col2"]: [["이것이 좋은 하루"]]}}, "GlobalParameters": {}}** hello 요청 본문에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-218">Type **{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": [["This is a good day"]]}}, "GlobalParameters": {}}** for hello request body.</span></span>

![azureml-demo-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

<span data-ttu-id="20034-220">**보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-220">Click **Send**.</span></span>

![보내기](./media/machine-learning-manage-web-service-endpoints-using-api-management/send.png)

<span data-ttu-id="20034-222">작업이 호출 hello 개발자 포털 hello 표시 **요청 URL** hello 백 엔드 서비스에서 hello **응답 상태**, hello **응답 헤더**, 임의의 **응답 콘텐츠**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-222">After an operation is invoked, hello developer portal displays hello **Requested URL** from hello back-end service, hello **Response status**, hello **Response headers**, and any **Response content**.</span></span>

![response-status](./media/machine-learning-manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a><span data-ttu-id="20034-224">부록 A - 간단한 AzureML 웹 서비스 만들기 및 테스트</span><span class="sxs-lookup"><span data-stu-id="20034-224">Appendix A - Creating and testing a simple AzureML web service</span></span>
### <a name="creating-hello-experiment"></a><span data-ttu-id="20034-225">Hello 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="20034-225">Creating hello experiment</span></span>
<span data-ttu-id="20034-226">간단한 AzureML 실험을 만들어 웹 서비스로 배포 하기 위한 hello 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="20034-226">Below are hello steps for creating a simple AzureML experiment and deploying it as a web service.</span></span> <span data-ttu-id="20034-227">임의의 텍스트 열을 입력으로 웹 서비스는 hello 하 고 정수로 표시 되는 기능 집합을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-227">hello web service takes as input a column of arbitrary text and returns a set of features represented as integers.</span></span> <span data-ttu-id="20034-228">예:</span><span class="sxs-lookup"><span data-stu-id="20034-228">For example:</span></span>

| <span data-ttu-id="20034-229">텍스트</span><span class="sxs-lookup"><span data-stu-id="20034-229">Text</span></span> | <span data-ttu-id="20034-230">해시된 텍스트</span><span class="sxs-lookup"><span data-stu-id="20034-230">Hashed Text</span></span> |
| --- | --- |
| <span data-ttu-id="20034-231">This is a good day</span><span class="sxs-lookup"><span data-stu-id="20034-231">This is a good day</span></span> |<span data-ttu-id="20034-232">1 1 2 2 0 2 0 1</span><span class="sxs-lookup"><span data-stu-id="20034-232">1 1 2 2 0 2 0 1</span></span> |

<span data-ttu-id="20034-233">첫째, 원하는 브라우저를 사용 하 여를 이동: [https://studio.azureml.net/](https://studio.azureml.net/) 사용자 자격 증명 toolog에를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-233">First, using a browser of your choice, navigate to: [https://studio.azureml.net/](https://studio.azureml.net/) and enter your credentials toolog in.</span></span> <span data-ttu-id="20034-234">그리고 새 실험을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="20034-234">Next, create a new blank experiment.</span></span>

![search-experiment-templates](./media/machine-learning-manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

<span data-ttu-id="20034-236">너무 이름 바꾸기**SimpleFeatureHashingExperiment**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-236">Rename it too**SimpleFeatureHashingExperiment**.</span></span> <span data-ttu-id="20034-237">**저장된 데이터 집합**을 확장하고 **Amazon의 도서 리뷰**를 실험으로 끌어서 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="20034-237">Expand **Saved Datasets** and drag **Book Reviews from Amazon** onto your experiment.</span></span>

![simple-feature-hashing-experiment](./media/machine-learning-manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

<span data-ttu-id="20034-239">**데이터 변환** 및 **조작**을 확장하고 **데이터 집합의 열 선택**을 실험으로 끌어서 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="20034-239">Expand **Data Transformation** and **Manipulation** and drag **Select Columns in Dataset** onto your experiment.</span></span> <span data-ttu-id="20034-240">연결 **Amazon에서 책 검토** 너무**데이터 집합의 열 선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-240">Connect **Book Reviews from Amazon** too**Select Columns in Dataset**.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/project-columns.png)

<span data-ttu-id="20034-242">**데이터 집합의 열 선택**, **열 선택기 시작**을 차례로 클릭하고 **Col2**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-242">Click **Select Columns in Dataset** and then click **Launch column selector** and select **Col2**.</span></span> <span data-ttu-id="20034-243">이러한 변경 내용을 확인 표시 tooapply hello를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-243">Click hello checkmark tooapply these changes.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-columns.png)

<span data-ttu-id="20034-245">확장 **텍스트 분석** 끌어서 **기능 해시** hello 실험에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20034-245">Expand **Text Analytics** and drag **Feature Hashing** onto hello experiment.</span></span> <span data-ttu-id="20034-246">연결 **데이터 집합의 열 선택** 너무**기능 해시**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-246">Connect **Select Columns in Dataset** too**Feature Hashing**.</span></span>

![connect-project-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/connect-project-columns.png)

<span data-ttu-id="20034-248">형식 **3** hello에 대 한 **해시 비트 크기**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-248">Type **3** for hello **Hashing bitsize**.</span></span> <span data-ttu-id="20034-249">8(23)개 열이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="20034-249">This will create 8 (23) columns.</span></span>

![hashing-bitsize](./media/machine-learning-manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

<span data-ttu-id="20034-251">이 시점에서 tooclick 경우가 **실행** tootest hello 실험 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-251">At this point, you may want tooclick **Run** tootest hello experiment.</span></span>

![실행](./media/machine-learning-manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a><span data-ttu-id="20034-253">웹 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="20034-253">Create a web service</span></span>
<span data-ttu-id="20034-254">이제 웹 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="20034-254">Now create a web service.</span></span> <span data-ttu-id="20034-255">**웹 서비스**를 확장하고 **입력**을 실험으로 끌어서 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="20034-255">Expand **Web Service** and drag **Input** onto your experiment.</span></span> <span data-ttu-id="20034-256">연결 **입력** 너무**기능 해시**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-256">Connect **Input** too**Feature Hashing**.</span></span> <span data-ttu-id="20034-257">**출력** 을 실험으로 끌어서 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="20034-257">Also drag **output** onto your experiment.</span></span> <span data-ttu-id="20034-258">연결 **출력** 너무**기능 해시**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-258">Connect **Output** too**Feature Hashing**.</span></span>

![output-to-feature-hashing](./media/machine-learning-manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

<span data-ttu-id="20034-260">**웹 서비스 게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-260">Click **Publish web service**.</span></span>

![publish-web-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/publish-web-service.png)

<span data-ttu-id="20034-262">클릭 **예** toopublish hello 실험 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-262">Click **Yes** toopublish hello experiment.</span></span>

![yes-to-publish](./media/machine-learning-manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-hello-web-service"></a><span data-ttu-id="20034-264">Hello 웹 서비스 테스트</span><span class="sxs-lookup"><span data-stu-id="20034-264">Test hello web service</span></span>
<span data-ttu-id="20034-265">AzureML 웹 서비스는 RSS(요청/응답 서비스) 및 BES(일괄 처리 실행 서비스) 끝점으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="20034-265">An AzureML web service consists of RSS (request/response service) and BES (batch execution service) endpoints.</span></span> <span data-ttu-id="20034-266">RSS는 동기 실행에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="20034-266">RSS is for synchronous execution.</span></span> <span data-ttu-id="20034-267">BES는 비동기 작업 실행에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="20034-267">BES is for asynchronous job execution.</span></span> <span data-ttu-id="20034-268">tootest hello 샘플 Python 소스 아래와 웹 서비스를 할 수 있습니다 toodownload 및 설치 hello Azure SDK for Python (참조: [어떻게 tooinstall Python](../python-how-to-install.md)).</span><span class="sxs-lookup"><span data-stu-id="20034-268">tootest your web service with hello sample Python source below, you may need toodownload and install hello Azure SDK for Python (see: [How tooinstall Python](../python-how-to-install.md)).</span></span>

<span data-ttu-id="20034-269">Hello 만들어야 **작업 영역**, **서비스**, 및 **api_key** hello 샘플 소스 아래에 대 한 실험의 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-269">You will also need hello **workspace**, **service**, and **api_key** of your experiment for hello sample source below.</span></span> <span data-ttu-id="20034-270">클릭 하 여 hello 작업 영역 및 서비스를 찾을 수 있습니다 **요청/응답** 또는 **일괄 처리 실행** hello 웹 서비스 대시보드를 사용 하 여 실험에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-270">You can find hello workspace and service by clicking either **Request/Response** or **Batch Execution** for your experiment in hello web service dashboard.</span></span>

![find-workspace-and-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

<span data-ttu-id="20034-272">Hello를 찾을 수 있습니다 **api_key** hello 웹 서비스 대시보드를 사용 하 여 실험을 클릭 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-272">You can find hello **api_key** by clicking your experiment in hello web service dashboard.</span></span>

![find-api-key](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a><span data-ttu-id="20034-274">RRS 끝점 테스트</span><span class="sxs-lookup"><span data-stu-id="20034-274">Test RRS endpoint</span></span>
##### <a name="test-button"></a><span data-ttu-id="20034-275">테스트 단추</span><span class="sxs-lookup"><span data-stu-id="20034-275">Test button</span></span>
<span data-ttu-id="20034-276">쉽게 tootest hello RR 끝점은 tooclick **테스트** hello 웹 서비스 대시보드에서.</span><span class="sxs-lookup"><span data-stu-id="20034-276">An easy way tootest hello RRS endpoint is tooclick **Test** on hello web service dashboard.</span></span>

![test](./media/machine-learning-manage-web-service-endpoints-using-api-management/test.png)

<span data-ttu-id="20034-278">**col2**로 **This is a good day**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-278">Type **This is a good day** for **col2**.</span></span> <span data-ttu-id="20034-279">Hello 확인 표시를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-279">Click hello checkmark.</span></span>

![enter-data](./media/machine-learning-manage-web-service-endpoints-using-api-management/enter-data.png)

<span data-ttu-id="20034-281">다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="20034-281">You will see something like</span></span>

![sample-output](./media/machine-learning-manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a><span data-ttu-id="20034-283">샘플 코드</span><span class="sxs-lookup"><span data-stu-id="20034-283">Sample Code</span></span>
<span data-ttu-id="20034-284">또 다른 방법은 tootest 프로그램 RR 클라이언트 코드에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="20034-284">Another way tootest your RRS is from your client code.</span></span> <span data-ttu-id="20034-285">클릭 하면 **요청/응답** hello 대시보드 및 스크롤 toohello 아래쪽에 C#, Python 및 오른쪽에 대 한 샘플 코드를 표시 됩니다 Hello 요청 URI, 헤더 및 본문을 포함 하 여 hello RR 요청의 hello 구문이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="20034-285">If you click **Request/response** on hello dashboard and scroll toohello bottom, you will see sample code for C#, Python, and R. You will also see hello syntax of hello RRS request, including hello request URI, headers, and body.</span></span>

<span data-ttu-id="20034-286">이 가이드에서는 작동하는 Python 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="20034-286">This guide shows a working Python example.</span></span> <span data-ttu-id="20034-287">Toomodify 해야 hello와 **작업 영역**, **서비스**, 및 **api_key** 실험의 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-287">You will need toomodify it with hello **workspace**, **service**, and **api_key** of your experiment.</span></span>

    import urllib2
    import json
    workspace = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE WORKSPACE ID>"
    service = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE SERVICE ID>"
    api_key = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE API KEY>"
    data = {
    "Inputs": {
        "input1": {
            "ColumnNames": ["Col2"],
            "Values": [ [ "This is a good day" ] ]
        },
    },
    "GlobalParameters": { }
    }
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace + "/services/" + service + "/execute?api-version=2.0&details=true"
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}
    body = str.encode(json.dumps(data))
    try:
        req = urllib2.Request(url, body, headers)
        response = urllib2.urlopen(req)
        result = response.read()
        print "result:" + result
            except urllib2.HTTPError, error:
        print("hello request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a><span data-ttu-id="20034-288">BES 끝점 테스트</span><span class="sxs-lookup"><span data-stu-id="20034-288">Test BES endpoint</span></span>
<span data-ttu-id="20034-289">클릭 **일괄 처리 실행** hello 대시보드 및 스크롤 toohello 아래쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20034-289">Click **Batch execution** on hello dashboard and scroll toohello bottom.</span></span> <span data-ttu-id="20034-290">C#, Python 및 오른쪽에 대 한 샘플 코드에 표시 됩니다. Hello 구문을 hello BES 요청 toosubmit 작업, 작업 시작, hello 상태 또는 작업의 결과 및 작업 삭제도 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="20034-290">You will see sample code for C#, Python, and R. You will also see hello syntax of hello BES requests toosubmit a job, start a job, get hello status or results of a job, and delete a job.</span></span>

<span data-ttu-id="20034-291">이 가이드에서는 작동하는 Python 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="20034-291">This guide shows a working Python example.</span></span> <span data-ttu-id="20034-292">Toomodify 필요한 hello와 **작업 영역**, **서비스**, 및 **api_key** 실험의 합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-292">You need toomodify it with hello **workspace**, **service**, and **api_key** of your experiment.</span></span> <span data-ttu-id="20034-293">또한 toomodify hello를 할 **저장소 계정 이름**, **저장소 계정 키**, 및 **저장소 컨테이너 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-293">Additionally, you need toomodify hello **storage account name**, **storage account key**, and **storage container name**.</span></span> <span data-ttu-id="20034-294">마지막으로, 해야 toomodify hello 위치의 hello **입력된 파일** 및 hello의 hello 위치 **출력 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="20034-294">Lastly, you will need toomodify hello location of hello **input file** and hello location of hello **output file**.</span></span>

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH hello API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH hello LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH hello LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("hello request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading hello result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written toohello file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("hello results for " + outputName + " are available at hello following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "hello results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading hello input tooblob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded hello input tooblob storage"
    input_blob_path = "/" + storage_container_name + "/" + input_blob_name
    connection_string = "DefaultEndpointsProtocol=https;AccountName=" + storage_account_name + ";AccountKey=" + storage_account_key
    payload =  {
        "Input": {
            "ConnectionString": connection_string,
            "RelativeLocation": input_blob_path
        },
        "Outputs": {
            "output1": { "ConnectionString": connection_string, "RelativeLocation": "/" + storage_container_name + "/" + output_blob_name },
        },
        "GlobalParameters": {
        }
    }
        body = str.encode(json.dumps(payload))
    headers = { "Content-Type":"application/json", "Authorization":("Bearer " + api_key)}
    print("Submitting hello job...")
    # submit hello job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove hello enclosing double-quotes
    print("Job ID: " + job_id)
    # start hello job
    print("Starting hello job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking hello job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in hello follwing code
        req = urllib2.Request(url2, headers = { "Authorization":("Bearer " + api_key) })
        try:
            response = urllib2.urlopen(req)
        except urllib2.HTTPError, error:
            printHttpError(error)
            return
        result = json.loads(response.read())
        status = result["StatusCode"]
        print "status:" + status
        if (status == 0 or status == "NotStarted"):
            print("Job " + job_id + " not yet started...")
        elif (status == 1 or status == "Running"):
            print("Job " + job_id + " running...")
        elif (status == 2 or status == "Failed"):
            print("Job " + job_id + " failed!")
            print("Error details: " + result["Details"])
            break
        elif (status == 3 or status == "Cancelled"):
            print("Job " + job_id + " cancelled!")
            break
        elif (status == 4 or status == "Finished"):
            print("Job " + job_id + " finished!")
            processResults(result)
            break
        time.sleep(1) # wait one second
    return
    invokeBatchExecutionService()
