---
title: "(사용되지 않음) Machine Learning 웹 서비스를 Azure Marketplace에 게시 | Microsoft Docs"
description: "(사용되지 않음) Azure Marketplace에 Azure Machine Learning 웹 서비스를 게시하는 방법"
services: machine-learning
documentationcenter: 
author: BharathS
manager: jhubbard
editor: cgronlun
ms.assetid: 68e908be-3a99-4cd7-9517-e2b5f2f341b8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: machine-learning-gallery-experiments
redirect_document_id: TRUE
ms.openlocfilehash: 3e3420872f0c604e027d1f309a6de6f52a5a788c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-publish-azure-machine-learning-web-service-to-the-azure-marketplace"></a><span data-ttu-id="604cb-103">(사용되지 않음) Azure Marketplace에 Azure Machine Learning 웹 서비스 게시</span><span class="sxs-lookup"><span data-stu-id="604cb-103">(deprecated) Publish Azure Machine Learning Web Service to the Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="604cb-104">DataMarket 및 Data Services는 종료되며 기존 구독은 2017년 3월 31일부터 종료 및 취소됩니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span></span> <span data-ttu-id="604cb-105">결과적으로,이 문서는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-105">As a result, this article is being deprecated.</span></span> 
> 
> <span data-ttu-id="604cb-106">대안으로, 데이터 과학 커뮤니티를 위하여 [Cortana Intelligence 갤러리](https://gallery.cortanaintelligence.com/)에 Machine Learning 실험을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-106">As an alternative, you can publish your Machine Learning experiments to the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for the benefit of the data science community.</span></span> <span data-ttu-id="604cb-107">자세한 내용은 [Cortana Intelligence 갤러리에서 리소스 공유 및 검색](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="604cb-107">For more information, see [Share and discover resources in the Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span></span>

<span data-ttu-id="604cb-108">Azure 마켓플레이스에서는 외부 고객이 사용하도록 유료 또는 무료 서비스로 Azure 기계 학습 웹 서비스를 게시하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-108">The Azure Marketplace provides the ability to publish Azure Machine Learning web services as paid or free services for consumption by external customers.</span></span> <span data-ttu-id="604cb-109">이 문서에서는 시작 지침에 대한 링크와 함께 프로세스의 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-109">This article provides an overview of that process with links to guidelines to get you started.</span></span> <span data-ttu-id="604cb-110">이 프로세스를 사용하여 다른 개발자가 응용 프로그램에서 사용할 수 있도록 웹 서비스를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-110">By using this process, you can make your web services available for other developers to consume in their applications.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-the-publishing-process"></a><span data-ttu-id="604cb-111">게시 프로세스 개요</span><span class="sxs-lookup"><span data-stu-id="604cb-111">Overview of the publishing process</span></span>
<span data-ttu-id="604cb-112">Azure 기계 학습 웹 서비스를 Azure 마켓플레이스에 게시하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-112">The following are the steps for publishing an Azure Machine Learning web service to Azure Marketplace:</span></span>

1. <span data-ttu-id="604cb-113">기계 학습 요청-응답 서비스(RR)를 만들어서 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-113">Create and publish a Machine Learning Request-Response service (RRS)</span></span>
2. <span data-ttu-id="604cb-114">서비스를 프로덕션 환경에 배포하고 API 키 및 OData 끝점 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-114">Deploy the service to production, and obtain the API Key and OData endpoint information.</span></span>
3. <span data-ttu-id="604cb-115">게시된 웹 서비스의 URL을 사용하여 [Azure 마켓플레이스(데이터 마켓)](https://publish.windowsazure.com/workspace/)</span><span class="sxs-lookup"><span data-stu-id="604cb-115">Use the URL of the published web service to publish to [Azure Marketplace (Data Market)](https://publish.windowsazure.com/workspace/)</span></span> 
4. <span data-ttu-id="604cb-116">제출된 제품은 검토되고 고객이 구매를 시작하기 전에 승인되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-116">Once submitted, your offer is reviewed and needs to be approved before your customers can start purchasing it.</span></span> <span data-ttu-id="604cb-117">게시 프로세스는 영업일 기준 몇 일이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-117">The publishing process can take a few business days.</span></span> 

## <a name="walk-through"></a><span data-ttu-id="604cb-118">방법 설명</span><span class="sxs-lookup"><span data-stu-id="604cb-118">Walk through</span></span>
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a><span data-ttu-id="604cb-119">1단계: 기계 학습 요청-응답 서비스(RR)를 만들어서 게시</span><span class="sxs-lookup"><span data-stu-id="604cb-119">Step 1: Create and publish a Machine Learning Request-Response service (RRS)</span></span>
 <span data-ttu-id="604cb-120">아직 게시하지 않은 분은 이 [방법 설명](machine-learning-walkthrough-5-publish-web-service.md)을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="604cb-120">If you have not done this already, please take a look at this [walk through](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

### <a name="step-2-deploy-the-service-to-production-and-obtain-the-api-key-and-odata-endpoint-information"></a><span data-ttu-id="604cb-121">2단계: 서비스를 프로덕션 환경에 배포하고 API 키 및 OData 끝점 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="604cb-121">Step 2: Deploy the service to production, and obtain the API Key and OData endpoint information</span></span>
1. <span data-ttu-id="604cb-122">[Azure 클래식 포털](http://manage.windowsazure.com)에서,왼쪽에 있는 탐색 모음에서 **기계 학습** 옵션을 선택하고 작업 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-122">From the [Azure Classic Portal](http://manage.windowsazure.com), select the **MACHINE LEARNING** option from the left navigation bar, and select your workspace.</span></span> 
2. <span data-ttu-id="604cb-123">**웹 서비스** 탭을 클릭하고 마켓플레이스에 게시할 웹 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-123">Click on the **WEB SERVICES** tab, and select the web service you would like to publish to the marketplace.</span></span>
   
    ![Azure 마켓플레이스][workspace]
3. <span data-ttu-id="604cb-125">마켓플레이스에서 사용되기를 원하는 끝점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-125">Select the endpoint you would like to have the marketplace consume.</span></span> <span data-ttu-id="604cb-126">추가 끝점을 하나도 만들지 않은 경우 **기본** 끝점을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-126">If you have not created any additional endpoints, you can select the **Default** endpoint.</span></span>
4. <span data-ttu-id="604cb-127">끝점에서 클릭하면 **API 키**가 보일 것입니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-127">Once you have clicked on the endpoint, you will be able to see the **API KEY**.</span></span> <span data-ttu-id="604cb-128">3단계에서 이 정보가 필요하므로 키를 복사해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-128">You will need this piece of information later on in Step 3, so make a copy of it.</span></span>
   
    ![Azure 마켓플레이스][apikey]
5. <span data-ttu-id="604cb-130">**REQUEST/RESPONSE** 메서드를 클릭합니다. 현재는 마켓플레이스에 Batch 실행 서비스를 게시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-130">Click on the **REQUEST/RESPONSE** method, at this point we do not support publishing batch execution services to the marketplace.</span></span> <span data-ttu-id="604cb-131">Request/Response 메서드에 대한 API 도움말 페이지로 이동될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-131">That will take you to the API help page for the Request/Response method.</span></span>
6. <span data-ttu-id="604cb-132">**OData 끝점 주소**를 복사합니다. 3단계에서 이 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-132">Copy the **OData Endpoint Address**, you will need this information later on in Step 3.</span></span>
   
    ![Azure 마켓플레이스][odata]

<span data-ttu-id="604cb-134">프로덕션 환경에 서비스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-134">deploy the service into production.</span></span>

### <a name="step-3-use-the-url-of-the-published-web-service-to-publish-to-azure-marketplace-datamarket"></a><span data-ttu-id="604cb-135">3단계: 게시된 웹 서비스의 URL을 사용하여 Azure 마켓플레이스(데이터 마켓)에 게시</span><span class="sxs-lookup"><span data-stu-id="604cb-135">Step 3: Use the URL of the published web service to publish to Azure Marketplace (DataMarket)</span></span>
1. <span data-ttu-id="604cb-136">[Azure 마켓플레이스(데이터 마켓)](http://datamarket.azure.com/home)</span><span class="sxs-lookup"><span data-stu-id="604cb-136">Navigate to [Azure Marketplace (Data Market)](http://datamarket.azure.com/home)</span></span> 
2. <span data-ttu-id="604cb-137">페이지 상단의 **게시** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-137">Click on the **Publish** link at the top of the page.</span></span> <span data-ttu-id="604cb-138">[Microsoft Azure 게시 포털](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="604cb-138">This will take you to the [Microsoft Azure Publishing Portal](https://publish.windowsazure.com)</span></span>
3. <span data-ttu-id="604cb-139">**게시자** 섹션을 클릭하여 게시자로 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-139">Click on the **publishers** section to register as a publisher.</span></span>
4. <span data-ttu-id="604cb-140">새 제품을 만들 때 **Data Services**를 선택하고 **새 Data Service 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-140">When creating a new offer, select **Data Services**, then click **Create a New Data Service**.</span></span> 
   
   ![Azure 마켓플레이스][image1]
   
   <br />
5. <span data-ttu-id="604cb-142">**요금제** 아래에서 가격 요금제를 포함하여 제품에 대한 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-142">Under **Plans** provide information on your offering, including a pricing plan.</span></span> <span data-ttu-id="604cb-143">무료 또는 유료 서비스를 제공할지 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-143">Decide if you will offer a free or paid service.</span></span> <span data-ttu-id="604cb-144">유료로 제공하려면 은행 및 세금 정보와 같은 결제 정보를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-144">To get paid, provide payment information such as your bank and tax information.</span></span>
6. <span data-ttu-id="604cb-145">**마케팅** 아래에서 제목, 제품에 대한 설명 등 제품 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-145">Under **Marketing** provide information about your offer, such as the title and description for your offer.</span></span>
7. <span data-ttu-id="604cb-146">**요금제** 아래에서 특정 국가에 대한 요금제 가격을 설정하거나 시스템에서 제품 가격을 "자동 설정"하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-146">Under **Pricing** you can set the price for your plans for specific countries, or let the system "autoprice" your offer.</span></span>
8. <span data-ttu-id="604cb-147">**데이터 서비스** 탭에서 **데이터 원본**으로 **웹 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-147">On the **Data Service** tab, click **Web Service** as the **Data Source**.</span></span>
   
    ![Azure 마켓플레이스][image2]
9. <span data-ttu-id="604cb-149">위의 2단계에서 설명한 대로 Azure 클래식 포털에서 웹 서비스 URL 및 API 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-149">Get the web service URL and API key from the Azure Classic Portal, as explained in step 2 above.</span></span>
10. <span data-ttu-id="604cb-150">마켓플레이스 데이터 서비스 설정 대화 상자에서 OData 끝점 주소를 **서비스 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-150">In the Marketplace Data Service setup dialog box, paste the OData endpoint address into the **Service URL** text box.</span></span>
11. <span data-ttu-id="604cb-151">**인증**에 대해 **헤더**를 **인증 체계**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-151">For **Authentication**, choose **Header** as the **Authentication Scheme**.</span></span>
    
    * <span data-ttu-id="604cb-152">**헤더 이름**.으로 "권한 부여"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-152">Enter "Authorization" for the **Header Name**.</span></span>
    * <span data-ttu-id="604cb-153">**헤더 값**에 대해 "Bearer"(따옴표 제외)를 입력하고, **스페이스** 바를 클릭한 다음 API 키를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-153">For the **Header Value**, enter "Bearer" (without the quotation marks), click the **Space** bar, and then paste the API key.</span></span>
    * <span data-ttu-id="604cb-154">**This Service is OData(이 서비스는 OData입니다.)** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-154">Select the **This Service is OData** check box.</span></span>
    * <span data-ttu-id="604cb-155">**연결 테스트** 를 클릭하여 연결을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-155">Click **Test Connection** to test the connection.</span></span>
12. <span data-ttu-id="604cb-156">**범주** 아래에서 **Machine Learning**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-156">Under **Categories**, ensure **Machine Learning** is selected.</span></span>
13. <span data-ttu-id="604cb-157">제품에 대한 모든 메타데이터를 입력했으면 **게시**를 클릭한 다음 **스테이징 환경으로 푸시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-157">When you are done entering all the metadata about your offer, click on **Publish**, and then **Push to Staging**.</span></span> <span data-ttu-id="604cb-158">이 시점에서 수정이 필요한 나머지 문제에 대한 알림이 제공될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-158">At this point, you will be notified of any remaining issues that you need to fix.</span></span>
14. <span data-ttu-id="604cb-159">모든 미해결 문제를 해결한 후 **프로덕션 환경으로 푸시하도록 승인 요청**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-159">After you have ensured completion of all the outstanding issues, click on **Request approval to push to Production**.</span></span> <span data-ttu-id="604cb-160">게시 프로세스는 영업일 기준 몇 일이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="604cb-160">The publishing process can take a few business days.</span></span> 

[image1]:./media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:./media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:./media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:./media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:./media/machine-learning-publish-web-service-to-azure-marketplace/odata.png

