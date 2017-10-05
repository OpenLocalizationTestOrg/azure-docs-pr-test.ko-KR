---
title: "Machine Learning 웹 서비스에 대한 로깅 | Microsoft Docs"
description: "기계 학습 웹 서비스에 대해 로깅을 사용하도록 설정하는 방법을 알아봅니다. 로깅은 API 문제를 해결하는 데 도움이 되는 추가 정보를 제공합니다."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c54d41e1-0300-46ef-bbfc-d6f7dca85086
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: raymondl;garye
ms.openlocfilehash: 7d0b2db01427430d6b0a317cdfefc265dd4b06e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-logging-for-machine-learning-web-services"></a><span data-ttu-id="2f3b6-104">기계 학습 웹 서비스에 대해 로깅 사용</span><span class="sxs-lookup"><span data-stu-id="2f3b6-104">Enable logging for Machine Learning web services</span></span>
<span data-ttu-id="2f3b6-105">이 문서에서는 Machine Learning 웹 서비스의 로깅 기능을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-105">This document provides information on the logging capability of Machine Learning web services.</span></span> <span data-ttu-id="2f3b6-106">로깅은 오류 번호 및 메시지 외에 Machine Learning API 호출 문제를 해결하는 데 유용한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-106">Logging provides additional information, beyond just an error number and a message, that can help you troubleshoot your calls to the Machine Learning APIs.</span></span>  

## <a name="how-to-enable-logging-for-a-web-service"></a><span data-ttu-id="2f3b6-107">웹 서비스에서 로깅을 사용하도록 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="2f3b6-107">How to enable logging for a Web service</span></span>

<span data-ttu-id="2f3b6-108">[Azure Machine Learning 웹 서비스](https://services.azureml.net) 포털에서 로깅을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-108">You enable logging from the [Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span> 

1. <span data-ttu-id="2f3b6-109">[https://services.azureml.net](https://services.azureml.net)에서 Azure Machine Learning 웹 서비스 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-109">Sign in to the Azure Machine Learning Web Services portal at [https://services.azureml.net](https://services.azureml.net).</span></span> <span data-ttu-id="2f3b6-110">클래식 웹 서비스의 경우 Machine Learning 스튜디오에서 Machine Learning 웹 서비스 페이지에 있는 **새 웹 서비스 환경**을 클릭하여 포털로 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-110">For a Classic web service, you can also get to the portal by clicking **New Web Services Experience** on the Machine Learning Web Services page in Machine Learning Studio.</span></span>

   ![새 웹 서비스 환경 링크](media/machine-learning-web-services-logging/new-web-services-experience-link.png)

2. <span data-ttu-id="2f3b6-112">상단 메뉴 모음에서 새 웹 서비스에 대한 **웹 서비스**를 클릭하거나 클래식 웹 서비스에 대한 **클래식 웹 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-112">On the top menu bar, click **Web Services** for a New web service, or click **Classic Web Services** for a Classic web service.</span></span>

   ![새로운 또는 클래식 웹 서비스 선택](media/machine-learning-web-services-logging/select-web-service.png)

3. <span data-ttu-id="2f3b6-114">새 웹 서비스의 경우 웹 서비스 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-114">For a New web service, click the web service name.</span></span> <span data-ttu-id="2f3b6-115">클래식 웹 서비스의 경우 웹 서비스 이름을 클릭하고, 다음 페이지에서 적절한 끝점을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-115">For a Classic web service, click the web service name and then on the next page click the appropriate endpoint.</span></span>

4. <span data-ttu-id="2f3b6-116">최상위 메뉴 모음에서 **구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-116">On the top menu bar, click **Configure**.</span></span>

5. <span data-ttu-id="2f3b6-117">**로깅 사용** 옵션을 *오류*(오류만 로그) 또는 *모두*(전체 로깅의 경우)로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-117">Set the **Enable Logging** option to *Error* (to log only errors) or *All* (for full logging).</span></span>

   ![로깅 수준 선택](media/machine-learning-web-services-logging/enable-logging.png)

6. <span data-ttu-id="2f3b6-119">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-119">Click **Save**.</span></span>

7. <span data-ttu-id="2f3b6-120">클래식 웹 서비스의 경우 **ml-diagnostics** 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-120">For Classic web services, create the **ml-diagnostics** container.</span></span>

   <span data-ttu-id="2f3b6-121">모든 웹 서비스 로그는 웹 서비스와 연결된 저장소 계정에 있는 **ml-diagnostics**이라는 blob 컨테이너에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-121">All web service logs are kept in a blob container named **ml-diagnostics** in the storage account associated with the web service.</span></span> <span data-ttu-id="2f3b6-122">새 웹 서비스의 경우 이 컨테이너는 처음 웹 서비스에 액세스할 때 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-122">For New web services, this container is created the first time you access the web service.</span></span> <span data-ttu-id="2f3b6-123">클래식 웹 서비스의 경우 이 컨테이너가 없는 경우 하나 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-123">For Classic web services, you need to create the container if it doesn't already exist.</span></span> 

   1. <span data-ttu-id="2f3b6-124">[Azure Portal](https://portal.azure.com)에서 웹 서비스와 연결된 저장소 계정으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-124">In the [Azure portal](https://portal.azure.com), go to the storage account associated with the web service.</span></span>

   2. <span data-ttu-id="2f3b6-125">**Blob Service**에서 **컨테이너**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-125">Under **Blob Service**, click **Containers**.</span></span>

   3. <span data-ttu-id="2f3b6-126">컨테이너 **ml-diagnostics**가 없는 경우 **+컨테이너**를 클릭하여 컨테이너 이름을 “ml-diagnostics”로 지정하고, **액세스 형식**을 “Blob”으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-126">If the container **ml-diagnostics** doesn't exist, click **+Container**, give the container the name "ml-diagnostics", and select the **Access type** as "Blob".</span></span> <span data-ttu-id="2f3b6-127">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-127">Click **OK**.</span></span>

      ![로깅 수준 선택](media/machine-learning-web-services-logging/create-ml-diagnostics-container.png)

> [!TIP]
>
> <span data-ttu-id="2f3b6-129">클래식 웹 서비스의 경우 Machine Learning Studio에서 웹 서비스 대시보드는 로깅을 사용하도록 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-129">For a Classic web service, the Web Services Dashboard in Machine Learning Studio also has a switch to enable logging.</span></span> <span data-ttu-id="2f3b6-130">그러나 이제 로깅은 웹 서비스 포털을 통해 관리되므로 이 문서에 설명된 대로 포털을 통해 로깅을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-130">However, because logging is now managed through the Web Services portal, you need to enable logging through the portal as described in this article.</span></span> <span data-ttu-id="2f3b6-131">이미 Studio에서 로그인을 사용하도록 설정한 경우 웹 서비스 포털에서 로깅을 사용하지 않도록 설정하고 다시 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-131">If you already enabled logging in Studio, then in the Web Services Portal, disable logging and enable it again.</span></span>


## <a name="the-effects-of-enabling-logging"></a><span data-ttu-id="2f3b6-132">로깅 활성화의 효과</span><span class="sxs-lookup"><span data-stu-id="2f3b6-132">The effects of enabling logging</span></span>
<span data-ttu-id="2f3b6-133">로깅을 사용하도록 설정하면 웹 서비스 끝점의 진단 및 오류가 사용자 작업 영역과 연결된 Azure Storage 계정의 **ml-diagnostics** blob 컨테이너에 로깅됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-133">When logging is enabled, the diagnostics and errors from the web service endpoint are logged in the **ml-diagnostics** blob container in the Azure Storage Account linked with the user’s workspace.</span></span> <span data-ttu-id="2f3b6-134">이 컨테이너는 이 저장소 계정과 연결된 모든 작업 영역의 모든 웹 서비스 끝점에 대한 모든 진단 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-134">This container holds all the diagnostics information for all the web service endpoints for all the workspaces associated with this storage account.</span></span>

<span data-ttu-id="2f3b6-135">Azure Storage 계정을 탐색하는 데 사용할 수 있는 여러 도구 중 하나를 통해 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-135">The logs can be viewed using any of the several tools available to explore an Azure Storage Account.</span></span> <span data-ttu-id="2f3b6-136">가장 쉬운 방법은 Azure Portal에서 저장소 계정으로 이동한 다음, **컨테이너**를 클릭하고 컨테이너 **ml-diagnostics**를 클릭하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-136">The easiest may be to navigate to the storage account in the Azure portal, click **Containers**, and then click the container **ml-diagnostics**.</span></span>  

## <a name="log-blob-detail-information"></a><span data-ttu-id="2f3b6-137">Blob 세부 정보 기록</span><span class="sxs-lookup"><span data-stu-id="2f3b6-137">Log blob detail information</span></span>
<span data-ttu-id="2f3b6-138">컨테이너의 각 blob은 정확히 다음 작업 중 하나에 대한 진단 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-138">Each blob in the container holds the diagnostics information for exactly one of the following actions:</span></span>

* <span data-ttu-id="2f3b6-139">일괄 처리 실행 메서드 실행</span><span class="sxs-lookup"><span data-stu-id="2f3b6-139">An execution of the Batch-Execution method</span></span>  
* <span data-ttu-id="2f3b6-140">요청-응답 메서드 실행</span><span class="sxs-lookup"><span data-stu-id="2f3b6-140">An execution of the Request-Response method</span></span>  
* <span data-ttu-id="2f3b6-141">요청-응답 컨테이너 초기화</span><span class="sxs-lookup"><span data-stu-id="2f3b6-141">Initialization of a Request-Response container</span></span>

<span data-ttu-id="2f3b6-142">각 Blob의 이름에는 다음과 같은 형식의 접두사가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-142">The name of each blob has a prefix of the following form:</span></span> 


`{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}`


<span data-ttu-id="2f3b6-143">_로그 형식_은 다음 값 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-143">Where _Log type_ is one of the following values:</span></span>  

* <span data-ttu-id="2f3b6-144">일괄 처리</span><span class="sxs-lookup"><span data-stu-id="2f3b6-144">batch</span></span>  
* <span data-ttu-id="2f3b6-145">score/requests</span><span class="sxs-lookup"><span data-stu-id="2f3b6-145">score/requests</span></span>  
* <span data-ttu-id="2f3b6-146">score/init</span><span class="sxs-lookup"><span data-stu-id="2f3b6-146">score/init</span></span>  

