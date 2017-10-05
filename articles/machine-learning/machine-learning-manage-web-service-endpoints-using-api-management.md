---
title: "API Management를 사용하여 Azure ML 웹 서비스를 관리하는 방법 알아보기 | Microsoft Docs"
description: "API 관리를 사용하여 AzureML 웹 서비스를 관리하는 방법에 대한 가이드입니다."
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
ms.openlocfilehash: 65eff3f4971f79886a840bb19bf76aaab48878de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="learn-how-to-manage-azureml-web-services-using-api-management"></a><span data-ttu-id="0ac8e-104">API 관리를 사용하여 AzureML 웹 서비스를 관리하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-104">Learn how to manage AzureML web services using API Management</span></span>
## <a name="overview"></a><span data-ttu-id="0ac8e-105">개요</span><span class="sxs-lookup"><span data-stu-id="0ac8e-105">Overview</span></span>
<span data-ttu-id="0ac8e-106">이 가이드에서는 API 관리를 빠르게 시작하여 AzureML 웹 서비스를 관리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-106">This guide shows you how to quickly get started using API Management to manage your AzureML web services.</span></span>

## <a name="what-is-azure-api-management"></a><span data-ttu-id="0ac8e-107">Azure API 관리란?</span><span class="sxs-lookup"><span data-stu-id="0ac8e-107">What is Azure API Management?</span></span>
<span data-ttu-id="0ac8e-108">Azure API 관리는 사용자 액세스, 사용 제한 및 대시보드 모니터링을 정의하여 REST API 끝점을 관리할 수 있는 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-108">Azure API Management is an Azure service that lets you manage your REST API endpoints by defining user access, usage throttling, and dashboard monitoring.</span></span> <span data-ttu-id="0ac8e-109">Azure API 관리에 대한 자세한 내용은 [여기](https://azure.microsoft.com/services/api-management/) 를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-109">Click [here](https://azure.microsoft.com/services/api-management/) for details on Azure API Management.</span></span> <span data-ttu-id="0ac8e-110">Azure API 관리를 시작하는 방법에 대한 설명은 [여기](../api-management/api-management-get-started.md) 를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-110">Click [here](../api-management/api-management-get-started.md) for a guide on how to get started with Azure API Management.</span></span> <span data-ttu-id="0ac8e-111">이 가이드를 기반으로 하는 이 다른 가이드에서는 알림 구성, 가격 책정 계층, 응답 처리, 사용자 인증, 제품 생산, 개발자 구독 및 사용량 대시보딩을 포함하는 다양한 주제를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-111">This other guide, which this guide is based on, covers more topics, including notification configurations, tier pricing, response handling, user authentication, creating products, developer subscriptions, and usage dashboarding.</span></span>

## <a name="what-is-azureml"></a><span data-ttu-id="0ac8e-112">AzureML이란?</span><span class="sxs-lookup"><span data-stu-id="0ac8e-112">What is AzureML?</span></span>
<span data-ttu-id="0ac8e-113">AzureML은 고급 분석 솔루션을 손쉽게 빌드, 배포 및 공유할 수 있도록 하는 기계 학습을 위한 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-113">AzureML is an Azure service for machine learning that enables you to easily build, deploy, and share advanced analytics solutions.</span></span> <span data-ttu-id="0ac8e-114">AzureML에 대한 자세한 내용은 [여기](https://azure.microsoft.com/services/machine-learning/) 를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-114">Click [here](https://azure.microsoft.com/services/machine-learning/) for details on AzureML.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ac8e-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0ac8e-115">Prerequisites</span></span>
<span data-ttu-id="0ac8e-116">이 가이드를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-116">To complete this guide, you need:</span></span>

* <span data-ttu-id="0ac8e-117">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-117">An Azure account.</span></span> <span data-ttu-id="0ac8e-118">Azure 계정이 없는 경우 무료 평가판 계정을 만드는 방법에 대한 자세한 내용은 [여기](https://azure.microsoft.com/pricing/free-trial/) 를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-118">If you don’t have an Azure account, click [here](https://azure.microsoft.com/pricing/free-trial/) for details on how to create a free trial account.</span></span>
* <span data-ttu-id="0ac8e-119">AzureML 계정.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-119">An AzureML account.</span></span> <span data-ttu-id="0ac8e-120">AzureML 계정이 없는 경우 무료 평가판 계정을 만드는 방법에 대한 자세한 내용은 [여기](https://studio.azureml.net/) 를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-120">If you don’t have an AzureML account, click [here](https://studio.azureml.net/) for details on how to create a free trial account.</span></span>
* <span data-ttu-id="0ac8e-121">AzureML 실험에 대한 작업 영역, 서비스 및 api_key는 웹 서비스로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-121">The workspace, service, and api_key for an AzureML experiment deployed as a web service.</span></span> <span data-ttu-id="0ac8e-122">AzureML 실험을 만드는 방법에 대한 자세한 내용은 [여기](machine-learning-create-experiment.md) 를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-122">Click [here](machine-learning-create-experiment.md) for details on how to create an AzureML experiment.</span></span> <span data-ttu-id="0ac8e-123">AzureML 실험을 웹 서비스로 배포하는 방법에 대한 자세한 내용은 [여기](machine-learning-publish-a-machine-learning-web-service.md) 를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-123">Click [here](machine-learning-publish-a-machine-learning-web-service.md) for details on how to deploy an AzureML experiment as a web service.</span></span> <span data-ttu-id="0ac8e-124">또는 간단한 AzureML 실험을 만들고 테스트하고 이를 웹 서비스로 배포하는 방법에 대한 지침이 부록 A에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-124">Alternately, Appendix A has instructions for how to create and test a simple AzureML experiment and deploy it as a web service.</span></span>

## <a name="create-an-api-management-instance"></a><span data-ttu-id="0ac8e-125">API 관리 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="0ac8e-125">Create an API Management instance</span></span>
<span data-ttu-id="0ac8e-126">API 관리를 사용하여 AzureML 웹 서비스를 관리하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-126">Below are the steps for using API Management to manage your AzureML web service.</span></span> <span data-ttu-id="0ac8e-127">먼저 서비스 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-127">First create a service instance.</span></span> <span data-ttu-id="0ac8e-128">[클래식 포털](https://manage.windowsazure.com/)에 로그인하고 **새로 만들기** > **App Services** > **API Management** > **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-128">Log in to the [Classic Portal](https://manage.windowsazure.com/) and click **New** > **App Services** > **API Management** > **Create**.</span></span>

![create-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-instance.png)

<span data-ttu-id="0ac8e-130">고유한 **URL**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-130">Specify a unique **URL**.</span></span> <span data-ttu-id="0ac8e-131">이 가이드에서는 **demoazureml**을 사용합니다. – 다른 방법을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-131">This guide uses **demoazureml** – you will need to choose something different.</span></span> <span data-ttu-id="0ac8e-132">서비스 인스턴스에 대해 원하는 **구독** 및 **지역**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-132">Choose the desired **Subscription** and **Region** for your service instance.</span></span> <span data-ttu-id="0ac8e-133">선택한 후에 다음 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-133">After making your selections, click the next button.</span></span>

![create-service-1](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-1.png)

<span data-ttu-id="0ac8e-135">**조직 이름**에 대한 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-135">Specify a value for the **Organization Name**.</span></span> <span data-ttu-id="0ac8e-136">이 가이드에서는 **demoazureml**을 사용합니다. – 다른 방법을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-136">This guide uses **demoazureml** – you will need to choose something different.</span></span> <span data-ttu-id="0ac8e-137">**관리자 메일** 필드에 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-137">Enter your email address in the **administrator e-mail** field.</span></span> <span data-ttu-id="0ac8e-138">이 전자 메일 주소는 API 관리 시스템에서 알림을 보내는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-138">This email address is used for notifications from the API Management system.</span></span>

![create-service-2](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-2.png)

<span data-ttu-id="0ac8e-140">확인란을 클릭하여 서비스 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-140">Click the check box to create your service instance.</span></span> <span data-ttu-id="0ac8e-141">*새로운 서비스를 만드는 데 최대 30분이 걸립니다*.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-141">*It takes up to thirty minutes for a new service to be created*.</span></span>

## <a name="create-the-api"></a><span data-ttu-id="0ac8e-142">API 만들기</span><span class="sxs-lookup"><span data-stu-id="0ac8e-142">Create the API</span></span>
<span data-ttu-id="0ac8e-143">서비스 인스턴스를 만든 후 다음 단계는 API를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-143">Once the service instance is created, the next step is to create the API.</span></span> <span data-ttu-id="0ac8e-144">API는 클라이언트 응용 프로그램에서 호출할 수 있는 작업 집합으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-144">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="0ac8e-145">API 작업은 기존 웹 서비스로 프록시 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-145">API operations are proxied to existing web services.</span></span> <span data-ttu-id="0ac8e-146">이 가이드는 기존 AzureML RRS 및 BES 웹 서비스에 대한 프록시인 API를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-146">This guide creates APIs that proxy to the existing AzureML RRS and BES web services.</span></span>

<span data-ttu-id="0ac8e-147">API는 Azure 클래식 포털을 통해 액세스할 수 있는 API 게시자 포털에서 생성 및 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-147">APIs are created and configured from the API publisher portal, which is accessed through the Azure Classic Portal.</span></span> <span data-ttu-id="0ac8e-148">게시자 포털에 연결하려면 서비스 인스턴스를 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-148">To reach the publisher portal, select your service instance.</span></span>

![select-service-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-service-instance.png)

<span data-ttu-id="0ac8e-150">API 관리 서비스에 대해 Azure 클래식 포털에서 **관리** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-150">Click **Manage** in the Azure Classic Portal for your API Management service.</span></span>

![manage-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/manage-service.png)

<span data-ttu-id="0ac8e-152">왼쪽의 **API Management** 메뉴에서 **API**를 클릭한 다음 **API 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-152">Click **APIs** from the **API Management** menu on the left, and then click **Add API**.</span></span>

![api-management-menu](./media/machine-learning-manage-web-service-endpoints-using-api-management/api-management-menu.png)

<span data-ttu-id="0ac8e-154">**Web API 이름**으로 **AzureML 데모 API**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-154">Type **AzureML Demo API** as the **Web API name**.</span></span> <span data-ttu-id="0ac8e-155">**https://ussouthcentral.services.azureml.net**을 **웹 서비스 URL**로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-155">Type **https://ussouthcentral.services.azureml.net** as the **Web service URL**.</span></span> <span data-ttu-id="0ac8e-156">**azureml-demo**를 **Web API URL 접미사**로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-156">Type **azureml-demo** as the **Web API URL suffix**.</span></span> <span data-ttu-id="0ac8e-157">**HTTPS**를 **Web API URL** 체계로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-157">Check **HTTPS** as the **Web API URL** scheme.</span></span> <span data-ttu-id="0ac8e-158">**시작**을 **제품**으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-158">Select **Starter** as **Products**.</span></span> <span data-ttu-id="0ac8e-159">완료되면 **저장**을 클릭하여 API를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-159">When finished, click **Save** to create the API.</span></span>

![add-new-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-new-api.png)

## <a name="add-the-operations"></a><span data-ttu-id="0ac8e-161">작업 추가</span><span class="sxs-lookup"><span data-stu-id="0ac8e-161">Add the operations</span></span>
<span data-ttu-id="0ac8e-162">해당 API에 새 작업을 추가하려면 **작업 추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-162">Click **Add operation** to add operations to this API.</span></span>

![add-operation](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-operation.png)

<span data-ttu-id="0ac8e-164">**새 작업** 창이 표시되고 **서명** 탭이 기본으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-164">The **New operation** window will be displayed and the **Signature** tab will be selected by default.</span></span>

## <a name="add-rrs-operation"></a><span data-ttu-id="0ac8e-165">RRS 작업 추가</span><span class="sxs-lookup"><span data-stu-id="0ac8e-165">Add RRS Operation</span></span>
<span data-ttu-id="0ac8e-166">먼저 AzureML RRS 서비스에 대한 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-166">First create an operation for the AzureML RRS service.</span></span> <span data-ttu-id="0ac8e-167">**게시**를 **HTTP 동사**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-167">Select **POST** as the **HTTP verb**.</span></span> <span data-ttu-id="0ac8e-168">**/workspaces/{workspace}/services/{service}/execute?api-version={apiversion}&details={details}**를 **URL 템플릿**으로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-168">Type **/workspaces/{workspace}/services/{service}/execute?api-version={apiversion}&details={details}** as the **URL template**.</span></span> <span data-ttu-id="0ac8e-169">**RRS 실행**을 **표시 이름**으로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-169">Type **RRS Execute** as the **Display name**.</span></span>

![add-rrs-operation-signature](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

<span data-ttu-id="0ac8e-171">왼쪽의 **응답** > **추가**를 클릭하여 **200 확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-171">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="0ac8e-172">**저장** 을 클릭하여 이 작업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-172">Click **Save** to save this operation.</span></span>

![add-rrs-operation-response](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a><span data-ttu-id="0ac8e-174">BES 작업 추가</span><span class="sxs-lookup"><span data-stu-id="0ac8e-174">Add BES Operations</span></span>
<span data-ttu-id="0ac8e-175">BES 작업에 대한 스크린샷은 RRS 작업을 추가하는 스크린샷과 매우 유사하므로 포함되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-175">Screenshots are not included for the BES operations as they are very similar to those for adding the RRS operation.</span></span>

### <a name="submit-but-not-start-a-batch-execution-job"></a><span data-ttu-id="0ac8e-176">일괄 처리 실행 작업 제출(시작하지는 않음)</span><span class="sxs-lookup"><span data-stu-id="0ac8e-176">Submit (but not start) a Batch Execution job</span></span>
<span data-ttu-id="0ac8e-177">API에 AzureML BES 작업을 추가하려면 **작업 추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-177">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="0ac8e-178">**게시**를 **HTTP 동사**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-178">Select **POST** for the **HTTP verb**.</span></span> <span data-ttu-id="0ac8e-179">**URL 템플릿**에 **/workspaces/{workspace}/services/{service}/jobs?api-version={apiversion}**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-179">Type **/workspaces/{workspace}/services/{service}/jobs?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="0ac8e-180">**표시 이름**에 **BES 제출**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-180">Type **BES Submit** for the **Display name**.</span></span> <span data-ttu-id="0ac8e-181">왼쪽의 **응답** > **추가**를 클릭하여 **200 확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-181">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="0ac8e-182">**저장** 을 클릭하여 이 작업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-182">Click **Save** to save this operation.</span></span>

### <a name="start-a-batch-execution-job"></a><span data-ttu-id="0ac8e-183">일괄 처리 실행 작업 시작</span><span class="sxs-lookup"><span data-stu-id="0ac8e-183">Start a Batch Execution job</span></span>
<span data-ttu-id="0ac8e-184">API에 AzureML BES 작업을 추가하려면 **작업 추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-184">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="0ac8e-185">**게시**를 **HTTP 동사**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-185">Select **POST** for the **HTTP verb**.</span></span> <span data-ttu-id="0ac8e-186">**URL 템플릿**에 **/workspaces/{workspace}/services/{service}/jobs/{jobid}/start?api-version={apiversion}**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-186">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}/start?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="0ac8e-187">**표시 이름**에 **BES 시작**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-187">Type **BES Start** for the **Display name**.</span></span> <span data-ttu-id="0ac8e-188">왼쪽의 **응답** > **추가**를 클릭하여 **200 확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-188">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="0ac8e-189">**저장** 을 클릭하여 이 작업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-189">Click **Save** to save this operation.</span></span>

### <a name="get-the-status-or-result-of-a-batch-execution-job"></a><span data-ttu-id="0ac8e-190">일괄 처리 실행 작업의 상태 또는 결과 가져오기</span><span class="sxs-lookup"><span data-stu-id="0ac8e-190">Get the status or result of a Batch Execution job</span></span>
<span data-ttu-id="0ac8e-191">API에 AzureML BES 작업을 추가하려면 **작업 추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-191">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="0ac8e-192">**가져오기**를 **HTTP 동사**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-192">Select **GET** for the **HTTP verb**.</span></span> <span data-ttu-id="0ac8e-193">**URL 템플릿**에 **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-193">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="0ac8e-194">**표시 이름**에 **BES 상태**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-194">Type **BES Status** for the **Display name**.</span></span> <span data-ttu-id="0ac8e-195">왼쪽의 **응답** > **추가**를 클릭하여 **200 확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-195">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="0ac8e-196">**저장** 을 클릭하여 이 작업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-196">Click **Save** to save this operation.</span></span>

### <a name="delete-a-batch-execution-job"></a><span data-ttu-id="0ac8e-197">일괄 처리 실행 작업 삭제</span><span class="sxs-lookup"><span data-stu-id="0ac8e-197">Delete a Batch Execution job</span></span>
<span data-ttu-id="0ac8e-198">API에 AzureML BES 작업을 추가하려면 **작업 추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-198">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="0ac8e-199">**삭제**를 **HTTP 동사**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-199">Select **DELETE** for the **HTTP verb**.</span></span> <span data-ttu-id="0ac8e-200">**URL 템플릿**에 **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-200">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="0ac8e-201">**표시 이름**에 **BES 삭제**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-201">Type **BES Delete** for the **Display name**.</span></span> <span data-ttu-id="0ac8e-202">왼쪽의 **응답** > **추가**를 클릭하여 **200 확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-202">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="0ac8e-203">**저장** 을 클릭하여 이 작업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-203">Click **Save** to save this operation.</span></span>

## <a name="call-an-operation-from-the-developer-portal"></a><span data-ttu-id="0ac8e-204">개발자 포털에서 작업 호출</span><span class="sxs-lookup"><span data-stu-id="0ac8e-204">Call an operation from the Developer Portal</span></span>
<span data-ttu-id="0ac8e-205">개발자 포털에서 직접 작업을 호출할 수 있으며, 이 포털을 사용하면 편리한 방법으로 API의 작업을 보고 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-205">Operations can be called directly from the Developer portal, which provides a convenient way to view and test the operations of an API.</span></span> <span data-ttu-id="0ac8e-206">이 가이드의 단계에서 **AzureML 데모 API**에 추가된 **RRS 실행** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-206">In this guide step you will call the **RRS Execute** method that was added to the **AzureML Demo API**.</span></span> <span data-ttu-id="0ac8e-207">클래식 포털의 오른쪽 위에 있는 메뉴에서 **개발자 포털** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-207">Click **Developer portal** from the menu at the top right of the Classic Portal.</span></span>

![developer-portal](./media/machine-learning-manage-web-service-endpoints-using-api-management/developer-portal.png)

<span data-ttu-id="0ac8e-209">맨 위 메뉴에서 **API**를 클릭하고 **AzureML 데모 API**를 클릭하여 사용 가능한 작업을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-209">Click **APIs** from the top menu, and then click **AzureML Demo API** to see the operations available.</span></span>

![demoazureml-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/demoazureml-api.png)

<span data-ttu-id="0ac8e-211">작업에 대해 **RRS 실행** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-211">Select **RRS Execute** for the operation.</span></span> <span data-ttu-id="0ac8e-212">**사용해 보세요.**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-212">Click **Try It**.</span></span>

![try-it](./media/machine-learning-manage-web-service-endpoints-using-api-management/try-it.png)

<span data-ttu-id="0ac8e-214">요청 매개 변수로는 **apiversion**에 **workspace**, **service**, **2.0**을 입력하고, **details**에 **true**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-214">For Request parameters, type your **workspace**,  **service**, **2.0** for the **apiversion**, and  **true** for the **details**.</span></span> <span data-ttu-id="0ac8e-215">AzureML 웹 서비스 대시보드에서 **작업 영역** 및 **서비스**를 찾을 수 있습니다(부록 A에서 **웹 서비스 테스트** 참조).</span><span class="sxs-lookup"><span data-stu-id="0ac8e-215">You can find your **workspace** and **service** in the AzureML web service dashboard (see **Test the web service** in Appendix A).</span></span>

<span data-ttu-id="0ac8e-216">요청 헤더로는 **헤더 추가**를 클릭하고 **콘텐츠 유형** 및 **application/json**을 입력하고 나서, **헤더 추가**를 클릭하고 **자동화** 및 **전달자<YOUR AZUREML SERVICE API-KEY>**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-216">For Request headers, click **Add header** and type **Content-Type** and **application/json**, then click **Add header** and type **Authorization** and **Bearer <YOUR AZUREML SERVICE API-KEY>**.</span></span> <span data-ttu-id="0ac8e-217">AzureML 웹 서비스 대시보드에서 **API 키**를 찾을 수 있습니다(부록 A에서 **웹 서비스 테스트** 참조).</span><span class="sxs-lookup"><span data-stu-id="0ac8e-217">You can find your **api key** in the AzureML web service dashboard (see **Test the web service** in Appendix A).</span></span>

<span data-ttu-id="0ac8e-218">요청 본문으로 **{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": [["This is a good day"]]}}, "GlobalParameters": {}}**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-218">Type **{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": [["This is a good day"]]}}, "GlobalParameters": {}}** for the request body.</span></span>

![azureml-demo-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

<span data-ttu-id="0ac8e-220">**보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-220">Click **Send**.</span></span>

![보내기](./media/machine-learning-manage-web-service-endpoints-using-api-management/send.png)

<span data-ttu-id="0ac8e-222">작업 호출 후에는 개발자 포털에 백 엔드 서비스의 **요청된 URL** 및 **응답 상태**, **응답 헤더**, **응답 콘텐츠**가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-222">After an operation is invoked, the developer portal displays the **Requested URL** from the back-end service, the **Response status**, the **Response headers**, and any **Response content**.</span></span>

![response-status](./media/machine-learning-manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a><span data-ttu-id="0ac8e-224">부록 A - 간단한 AzureML 웹 서비스 만들기 및 테스트</span><span class="sxs-lookup"><span data-stu-id="0ac8e-224">Appendix A - Creating and testing a simple AzureML web service</span></span>
### <a name="creating-the-experiment"></a><span data-ttu-id="0ac8e-225">실험 만들기</span><span class="sxs-lookup"><span data-stu-id="0ac8e-225">Creating the experiment</span></span>
<span data-ttu-id="0ac8e-226">간단한 AzureML 실험을 만들고 웹 서비스로 배포하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-226">Below are the steps for creating a simple AzureML experiment and deploying it as a web service.</span></span> <span data-ttu-id="0ac8e-227">웹 서비스에서는 임의 텍스트 열을 입력으로 사용하고 정수로 표시되는 기능 집합을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-227">The web service takes as input a column of arbitrary text and returns a set of features represented as integers.</span></span> <span data-ttu-id="0ac8e-228">예:</span><span class="sxs-lookup"><span data-stu-id="0ac8e-228">For example:</span></span>

| <span data-ttu-id="0ac8e-229">텍스트</span><span class="sxs-lookup"><span data-stu-id="0ac8e-229">Text</span></span> | <span data-ttu-id="0ac8e-230">해시된 텍스트</span><span class="sxs-lookup"><span data-stu-id="0ac8e-230">Hashed Text</span></span> |
| --- | --- |
| <span data-ttu-id="0ac8e-231">This is a good day</span><span class="sxs-lookup"><span data-stu-id="0ac8e-231">This is a good day</span></span> |<span data-ttu-id="0ac8e-232">1 1 2 2 0 2 0 1</span><span class="sxs-lookup"><span data-stu-id="0ac8e-232">1 1 2 2 0 2 0 1</span></span> |

<span data-ttu-id="0ac8e-233">먼저 선택한 브라우저를 사용하여 [https://studio.azureml.net/](https://studio.azureml.net/) 으로 이동하고 자격 증명을 입력하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-233">First, using a browser of your choice, navigate to: [https://studio.azureml.net/](https://studio.azureml.net/) and enter your credentials to log in.</span></span> <span data-ttu-id="0ac8e-234">그리고 새 실험을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-234">Next, create a new blank experiment.</span></span>

![search-experiment-templates](./media/machine-learning-manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

<span data-ttu-id="0ac8e-236">실험 이름을 **SimpleFeatureHashingExperiment**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-236">Rename it to **SimpleFeatureHashingExperiment**.</span></span> <span data-ttu-id="0ac8e-237">**저장된 데이터 집합**을 확장하고 **Amazon의 도서 리뷰**를 실험으로 끌어서 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-237">Expand **Saved Datasets** and drag **Book Reviews from Amazon** onto your experiment.</span></span>

![simple-feature-hashing-experiment](./media/machine-learning-manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

<span data-ttu-id="0ac8e-239">**데이터 변환** 및 **조작**을 확장하고 **데이터 집합의 열 선택**을 실험으로 끌어서 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-239">Expand **Data Transformation** and **Manipulation** and drag **Select Columns in Dataset** onto your experiment.</span></span> <span data-ttu-id="0ac8e-240">**Amazon의 도서 리뷰**를 **데이터 집합의 열 선택**에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-240">Connect **Book Reviews from Amazon** to **Select Columns in Dataset**.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/project-columns.png)

<span data-ttu-id="0ac8e-242">**데이터 집합의 열 선택**, **열 선택기 시작**을 차례로 클릭하고 **Col2**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-242">Click **Select Columns in Dataset** and then click **Launch column selector** and select **Col2**.</span></span> <span data-ttu-id="0ac8e-243">확인 표시를 클릭하여 변경 내용을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-243">Click the checkmark to apply these changes.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-columns.png)

<span data-ttu-id="0ac8e-245">**텍스트 분석**을 확장하고 **기능 해싱**을 실험으로 끌어서 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-245">Expand **Text Analytics** and drag **Feature Hashing** onto the experiment.</span></span> <span data-ttu-id="0ac8e-246">**데이터 집합의 열 선택**을 **기능 해싱**에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-246">Connect **Select Columns in Dataset** to **Feature Hashing**.</span></span>

![connect-project-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/connect-project-columns.png)

<span data-ttu-id="0ac8e-248">**해싱 비트 크기**로 **3**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-248">Type **3** for the **Hashing bitsize**.</span></span> <span data-ttu-id="0ac8e-249">8(23)개 열이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-249">This will create 8 (23) columns.</span></span>

![hashing-bitsize](./media/machine-learning-manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

<span data-ttu-id="0ac8e-251">이때 **실행** 을 클릭하여 실험을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-251">At this point, you may want to click **Run** to test the experiment.</span></span>

![실행](./media/machine-learning-manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a><span data-ttu-id="0ac8e-253">웹 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="0ac8e-253">Create a web service</span></span>
<span data-ttu-id="0ac8e-254">이제 웹 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-254">Now create a web service.</span></span> <span data-ttu-id="0ac8e-255">**웹 서비스**를 확장하고 **입력**을 실험으로 끌어서 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-255">Expand **Web Service** and drag **Input** onto your experiment.</span></span> <span data-ttu-id="0ac8e-256">**입력**을 **기능 해싱**에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-256">Connect **Input** to **Feature Hashing**.</span></span> <span data-ttu-id="0ac8e-257">**출력** 을 실험으로 끌어서 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-257">Also drag **output** onto your experiment.</span></span> <span data-ttu-id="0ac8e-258">**출력**을 **기능 해싱**에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-258">Connect **Output** to **Feature Hashing**.</span></span>

![output-to-feature-hashing](./media/machine-learning-manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

<span data-ttu-id="0ac8e-260">**웹 서비스 게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-260">Click **Publish web service**.</span></span>

![publish-web-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/publish-web-service.png)

<span data-ttu-id="0ac8e-262">**예** 를 클릭하여 실험을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-262">Click **Yes** to publish the experiment.</span></span>

![yes-to-publish](./media/machine-learning-manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-the-web-service"></a><span data-ttu-id="0ac8e-264">웹 서비스 테스트</span><span class="sxs-lookup"><span data-stu-id="0ac8e-264">Test the web service</span></span>
<span data-ttu-id="0ac8e-265">AzureML 웹 서비스는 RSS(요청/응답 서비스) 및 BES(일괄 처리 실행 서비스) 끝점으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-265">An AzureML web service consists of RSS (request/response service) and BES (batch execution service) endpoints.</span></span> <span data-ttu-id="0ac8e-266">RSS는 동기 실행에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-266">RSS is for synchronous execution.</span></span> <span data-ttu-id="0ac8e-267">BES는 비동기 작업 실행에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-267">BES is for asynchronous job execution.</span></span> <span data-ttu-id="0ac8e-268">다음 샘플 Python 소스로 웹 서비스를 테스트하려면 Python용 Azure SDK를 다운로드해야 할 수 있습니다( [Python을 설치하는 방법](../python-how-to-install.md)참조).</span><span class="sxs-lookup"><span data-stu-id="0ac8e-268">To test your web service with the sample Python source below, you may need to download and install the Azure SDK for Python (see: [How to install Python](../python-how-to-install.md)).</span></span>

<span data-ttu-id="0ac8e-269">또한 다음 샘플 원본에 대한 실험의 **workspace**, **service** 및 **api_key**가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-269">You will also need the **workspace**, **service**, and **api_key** of your experiment for the sample source below.</span></span> <span data-ttu-id="0ac8e-270">웹 서비스 대시보드에서 실험의 **요청/응답** 또는 **Batch 실행**을 클릭하여 workspace 및 service를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-270">You can find the workspace and service by clicking either **Request/Response** or **Batch Execution** for your experiment in the web service dashboard.</span></span>

![find-workspace-and-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

<span data-ttu-id="0ac8e-272">웹 서비스 대시보드에서 실험을 클릭하여 **api_key**를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-272">You can find the **api_key** by clicking your experiment in the web service dashboard.</span></span>

![find-api-key](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a><span data-ttu-id="0ac8e-274">RRS 끝점 테스트</span><span class="sxs-lookup"><span data-stu-id="0ac8e-274">Test RRS endpoint</span></span>
##### <a name="test-button"></a><span data-ttu-id="0ac8e-275">테스트 단추</span><span class="sxs-lookup"><span data-stu-id="0ac8e-275">Test button</span></span>
<span data-ttu-id="0ac8e-276">RRS 끝점을 테스트하는 간편한 방법은 웹 서비스 대시보드에서 **테스트** 를 클릭하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-276">An easy way to test the RRS endpoint is to click **Test** on the web service dashboard.</span></span>

![test](./media/machine-learning-manage-web-service-endpoints-using-api-management/test.png)

<span data-ttu-id="0ac8e-278">**col2**로 **This is a good day**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-278">Type **This is a good day** for **col2**.</span></span> <span data-ttu-id="0ac8e-279">확인 표시를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-279">Click the checkmark.</span></span>

![enter-data](./media/machine-learning-manage-web-service-endpoints-using-api-management/enter-data.png)

<span data-ttu-id="0ac8e-281">다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-281">You will see something like</span></span>

![sample-output](./media/machine-learning-manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a><span data-ttu-id="0ac8e-283">샘플 코드</span><span class="sxs-lookup"><span data-stu-id="0ac8e-283">Sample Code</span></span>
<span data-ttu-id="0ac8e-284">RRS를 테스트하는 또 다른 방법은 클라이언트 코드를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-284">Another way to test your RRS is from your client code.</span></span> <span data-ttu-id="0ac8e-285">대시보드에서 **요청/응답**을 클릭하고 아래쪽으로 스크롤하면 C#, Python 및 R에 대한 샘플 코드가 표시됩니다. 요청 URI, 헤더 및 본문을 포함한 RRS 요청 구문도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-285">If you click **Request/response** on the dashboard and scroll to the bottom, you will see sample code for C#, Python, and R. You will also see the syntax of the RRS request, including the request URI, headers, and body.</span></span>

<span data-ttu-id="0ac8e-286">이 가이드에서는 작동하는 Python 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-286">This guide shows a working Python example.</span></span> <span data-ttu-id="0ac8e-287">실험의 **workspace**, **service** 및 **api_key**를 사용하여 예제를 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-287">You will need to modify it with the **workspace**, **service**, and **api_key** of your experiment.</span></span>

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
        print("The request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a><span data-ttu-id="0ac8e-288">BES 끝점 테스트</span><span class="sxs-lookup"><span data-stu-id="0ac8e-288">Test BES endpoint</span></span>
<span data-ttu-id="0ac8e-289">대시보드에서 **Batch 실행**을 클릭하고 아래쪽으로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-289">Click **Batch execution** on the dashboard and scroll to the bottom.</span></span> <span data-ttu-id="0ac8e-290">C#, Python 및 R에 대한 샘플 코드가 표시됩니다. 작업을 제출하고, 작업을 시작하고, 작업의 상태나 결과를 가져오고, 작업을 삭제하기 위한 BES 요청 구문도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-290">You will see sample code for C#, Python, and R. You will also see the syntax of the BES requests to submit a job, start a job, get the status or results of a job, and delete a job.</span></span>

<span data-ttu-id="0ac8e-291">이 가이드에서는 작동하는 Python 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-291">This guide shows a working Python example.</span></span> <span data-ttu-id="0ac8e-292">실험의 **workspace**, **service** 및 **api_key**를 사용하여 예제를 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-292">You need to modify it with the **workspace**, **service**, and **api_key** of your experiment.</span></span> <span data-ttu-id="0ac8e-293">또한 **저장소 계정 이름**, **저장소 계정 키** 및 **저장소 컨테이너 이름**을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-293">Additionally, you need to modify the **storage account name**, **storage account key**, and **storage container name**.</span></span> <span data-ttu-id="0ac8e-294">마지막으로 **입력 파일**의 위치와 **출력 파일**의 위치를 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ac8e-294">Lastly, you will need to modify the location of the **input file** and the location of the **output file**.</span></span>

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH THE API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH THE LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH THE LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("The request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading the result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written to the file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("The results for " + outputName + " are available at the following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "The results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading the input to blob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded the input to blob storage"
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
    print("Submitting the job...")
    # submit the job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove the enclosing double-quotes
    print("Job ID: " + job_id)
    # start the job
    print("Starting the job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking the job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in the follwing code
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
