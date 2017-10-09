---
title: "웹 서비스 tooAzure 마켓플레이스 학습 aaa(deprecated) 게시 컴퓨터 | Microsoft Docs"
description: "(사용 되지 않음) 어떻게 toopublish 하면 Azure 기계 학습 웹 서비스 toohello Azure 마켓플레이스"
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
redirect_document_id: True
ms.openlocfilehash: 149abc3df9b79c1b37d233d5e85e803592ff1020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-publish-azure-machine-learning-web-service-toohello-azure-marketplace"></a><span data-ttu-id="1c800-103">(사용 되지 않음) Azure 기계 학습 웹 서비스 toohello Azure 마켓플레이스에서 게시</span><span class="sxs-lookup"><span data-stu-id="1c800-103">(deprecated) Publish Azure Machine Learning Web Service toohello Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="1c800-104">DataMarket 및 Data Services는 종료되며 기존 구독은 2017년 3월 31일부터 종료 및 취소됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span></span> <span data-ttu-id="1c800-105">결과적으로,이 문서는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-105">As a result, this article is being deprecated.</span></span> 
> 
> <span data-ttu-id="1c800-106">기계 학습 실험 toohello를 게시할 수 있습니다 [Cortana 인텔리전스 갤러리](https://gallery.cortanaintelligence.com/) hello hello 데이터 과학 커뮤니티의 혜택을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-106">As an alternative, you can publish your Machine Learning experiments toohello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for hello benefit of hello data science community.</span></span> <span data-ttu-id="1c800-107">자세한 내용은 참조 [공유 hello Cortana Intelligence 갤러리 리소스를 검색 하 고](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish)합니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-107">For more information, see [Share and discover resources in hello Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span></span>

<span data-ttu-id="1c800-108">hello Azure 마켓플레이스 지불 된 hello 기능 toopublish Azure 기계 학습 웹 서비스를 제공 하거나 외부 고객에 의해 소비에 대 한 서비스를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-108">hello Azure Marketplace provides hello ability toopublish Azure Machine Learning web services as paid or free services for consumption by external customers.</span></span> <span data-ttu-id="1c800-109">이 문서에서는 링크 tooguidelines tooget 했는지와 해당 프로세스의 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-109">This article provides an overview of that process with links tooguidelines tooget you started.</span></span> <span data-ttu-id="1c800-110">이 프로세스를 사용 하 여 가능 웹 서비스에 다른 개발자가 tooconsume에 사용할 수 있는 응용 프로그램에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-110">By using this process, you can make your web services available for other developers tooconsume in their applications.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-hello-publishing-process"></a><span data-ttu-id="1c800-111">Hello 게시 프로세스의 개요</span><span class="sxs-lookup"><span data-stu-id="1c800-111">Overview of hello publishing process</span></span>
<span data-ttu-id="1c800-112">Azure 기계 학습 웹 서비스 tooAzure 마켓플레이스를 게시 하기 위한 hello 단계는 hello 다음과가 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-112">hello following are hello steps for publishing an Azure Machine Learning web service tooAzure Marketplace:</span></span>

1. <span data-ttu-id="1c800-113">기계 학습 요청-응답 서비스(RR)를 만들어서 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-113">Create and publish a Machine Learning Request-Response service (RRS)</span></span>
2. <span data-ttu-id="1c800-114">Hello 서비스 tooproduction를 배포 하 고 hello API 키와 OData 끝점 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-114">Deploy hello service tooproduction, and obtain hello API Key and OData endpoint information.</span></span>
3. <span data-ttu-id="1c800-115">Hello의 hello URL을 사용 하 여 게시 웹 서비스 toopublish 너무[Azure 마켓플레이스 (데이터 마켓)](https://publish.windowsazure.com/workspace/)</span><span class="sxs-lookup"><span data-stu-id="1c800-115">Use hello URL of hello published web service toopublish too[Azure Marketplace (Data Market)](https://publish.windowsazure.com/workspace/)</span></span> 
4. <span data-ttu-id="1c800-116">제출 된 제안을 검토 하 고 필요한 전에 고객 승인 toobe 구입 해야 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-116">Once submitted, your offer is reviewed and needs toobe approved before your customers can start purchasing it.</span></span> <span data-ttu-id="1c800-117">hello 게시 프로세스에 비즈니스 며칠 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-117">hello publishing process can take a few business days.</span></span> 

## <a name="walk-through"></a><span data-ttu-id="1c800-118">방법 설명</span><span class="sxs-lookup"><span data-stu-id="1c800-118">Walk through</span></span>
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a><span data-ttu-id="1c800-119">1단계: 기계 학습 요청-응답 서비스(RR)를 만들어서 게시</span><span class="sxs-lookup"><span data-stu-id="1c800-119">Step 1: Create and publish a Machine Learning Request-Response service (RRS)</span></span>
 <span data-ttu-id="1c800-120">아직 게시하지 않은 분은 이 [방법 설명](machine-learning-walkthrough-5-publish-web-service.md)을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="1c800-120">If you have not done this already, please take a look at this [walk through](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

### <a name="step-2-deploy-hello-service-tooproduction-and-obtain-hello-api-key-and-odata-endpoint-information"></a><span data-ttu-id="1c800-121">2 단계: hello 서비스 tooproduction를 배포 하 고 hello API 키와 OData 끝점 정보를 가져오려면</span><span class="sxs-lookup"><span data-stu-id="1c800-121">Step 2: Deploy hello service tooproduction, and obtain hello API Key and OData endpoint information</span></span>
1. <span data-ttu-id="1c800-122">Hello에서 [Azure 클래식 포털](http://manage.windowsazure.com)선택, hello **기계 학습** hello 왼쪽된 탐색 모음에서 옵션 및 작업 영역을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-122">From hello [Azure Classic Portal](http://manage.windowsazure.com), select hello **MACHINE LEARNING** option from hello left navigation bar, and select your workspace.</span></span> 
2. <span data-ttu-id="1c800-123">Hello 클릭 **웹 서비스** 탭 및 선택 hello 웹 서비스 toopublish toohello 마켓플레이스를 원할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-123">Click on hello **WEB SERVICES** tab, and select hello web service you would like toopublish toohello marketplace.</span></span>
   
    ![Azure 마켓플레이스][workspace]
3. <span data-ttu-id="1c800-125">Hello 끝점은 toohave hello 마켓플레이스와 같은 사용을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-125">Select hello endpoint you would like toohave hello marketplace consume.</span></span> <span data-ttu-id="1c800-126">모든 추가 끝점을 만들지 않은 경우에 hello을 선택할 수 있습니다 **기본** 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-126">If you have not created any additional endpoints, you can select hello **Default** endpoint.</span></span>
4. <span data-ttu-id="1c800-127">Hello 끝점을 클릭 하면 수 toosee hello 수 **API 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-127">Once you have clicked on hello endpoint, you will be able toosee hello **API KEY**.</span></span> <span data-ttu-id="1c800-128">3단계에서 이 정보가 필요하므로 키를 복사해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-128">You will need this piece of information later on in Step 3, so make a copy of it.</span></span>
   
    ![Azure 마켓플레이스][apikey]
5. <span data-ttu-id="1c800-130">Hello 클릭 **요청/응답** 게시 일괄 처리 모드 실행 지원 하지 않습니다는이 시점 메서드 toohello 마켓플레이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-130">Click on hello **REQUEST/RESPONSE** method, at this point we do not support publishing batch execution services toohello marketplace.</span></span> <span data-ttu-id="1c800-131">요청/응답 메서드 hello에 대 한 toohello API 도움말 페이지를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-131">That will take you toohello API help page for hello Request/Response method.</span></span>
6. <span data-ttu-id="1c800-132">복사 hello **OData 끝점 주소**, 3 단계에서 나중에이 정보가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-132">Copy hello **OData Endpoint Address**, you will need this information later on in Step 3.</span></span>
   
    ![Azure 마켓플레이스][odata]

<span data-ttu-id="1c800-134">프로덕션 환경에 hello 서비스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-134">deploy hello service into production.</span></span>

### <a name="step-3-use-hello-url-of-hello-published-web-service-toopublish-tooazure-marketplace-datamarket"></a><span data-ttu-id="1c800-135">3 단계: hello의 hello URL을 사용 하 여 게시 된 웹 서비스 toopublish tooAzure 마켓플레이스 (DataMarket)</span><span class="sxs-lookup"><span data-stu-id="1c800-135">Step 3: Use hello URL of hello published web service toopublish tooAzure Marketplace (DataMarket)</span></span>
1. <span data-ttu-id="1c800-136">너무 이동[Azure 마켓플레이스 (데이터 마켓)](http://datamarket.azure.com/home)</span><span class="sxs-lookup"><span data-stu-id="1c800-136">Navigate too[Azure Marketplace (Data Market)](http://datamarket.azure.com/home)</span></span> 
2. <span data-ttu-id="1c800-137">Hello 클릭 **게시** hello hello 페이지 맨 아래에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-137">Click on hello **Publish** link at hello top of hello page.</span></span> <span data-ttu-id="1c800-138">그러면 toohello [Microsoft Azure 게시 포털](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="1c800-138">This will take you toohello [Microsoft Azure Publishing Portal](https://publish.windowsazure.com)</span></span>
3. <span data-ttu-id="1c800-139">Hello 클릭 **게시자** 를 게시자로 섹션 tooregister 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-139">Click on hello **publishers** section tooregister as a publisher.</span></span>
4. <span data-ttu-id="1c800-140">새 제품을 만들 때 **Data Services**를 선택하고 **새 Data Service 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-140">When creating a new offer, select **Data Services**, then click **Create a New Data Service**.</span></span> 
   
   ![Azure 마켓플레이스][image1]
   
   <br />
5. <span data-ttu-id="1c800-142">**요금제** 아래에서 가격 요금제를 포함하여 제품에 대한 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-142">Under **Plans** provide information on your offering, including a pricing plan.</span></span> <span data-ttu-id="1c800-143">무료 또는 유료 서비스를 제공할지 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-143">Decide if you will offer a free or paid service.</span></span> <span data-ttu-id="1c800-144">유료, tooget 은행 및 세금 정보 등 결제 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-144">tooget paid, provide payment information such as your bank and tax information.</span></span>
6. <span data-ttu-id="1c800-145">아래 **마케팅** hello 제목 및 제안에 대 한 설명 등 자신의 구독에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-145">Under **Marketing** provide information about your offer, such as hello title and description for your offer.</span></span>
7. <span data-ttu-id="1c800-146">아래 **가격 책정** 특정 국가 대 한 계획에 대 한 hello 가격을 설정 하거나 제안을 hello 시스템에서 "autoprice" 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-146">Under **Pricing** you can set hello price for your plans for specific countries, or let hello system "autoprice" your offer.</span></span>
8. <span data-ttu-id="1c800-147">Hello에 **데이터 서비스** 탭을 클릭 **웹 서비스** hello로 **데이터 소스**합니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-147">On hello **Data Service** tab, click **Web Service** as hello **Data Source**.</span></span>
   
    ![Azure 마켓플레이스][image2]
9. <span data-ttu-id="1c800-149">위의 2 단계에서 설명한 것 처럼 hello Azure 클래식 포털에서에서 hello 웹 서비스 URL 및 API 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-149">Get hello web service URL and API key from hello Azure Classic Portal, as explained in step 2 above.</span></span>
10. <span data-ttu-id="1c800-150">Hello 마켓플레이스 데이터 서비스 설정 대화 상자에 붙여 넣습니다 hello OData 끝점 주소 hello **서비스 URL** 입력란.</span><span class="sxs-lookup"><span data-stu-id="1c800-150">In hello Marketplace Data Service setup dialog box, paste hello OData endpoint address into hello **Service URL** text box.</span></span>
11. <span data-ttu-id="1c800-151">에 대 한 **인증**, 선택 **헤더** hello로 **인증 체계**합니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-151">For **Authentication**, choose **Header** as hello **Authentication Scheme**.</span></span>
    
    * <span data-ttu-id="1c800-152">Hello에 대 한 "인증"을 입력 **헤더 이름을**합니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-152">Enter "Authorization" for hello **Header Name**.</span></span>
    * <span data-ttu-id="1c800-153">Hello에 대 한 **헤더 값**, "Bearer" (인용 부호 hello) 없이 입력, 클릭 hello **공간** , 가로 막대형 차트 및 hello API 키를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-153">For hello **Header Value**, enter "Bearer" (without hello quotation marks), click hello **Space** bar, and then paste hello API key.</span></span>
    * <span data-ttu-id="1c800-154">선택 hello **이 서비스는 OData** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-154">Select hello **This Service is OData** check box.</span></span>
    * <span data-ttu-id="1c800-155">클릭 **연결 테스트** tootest hello 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-155">Click **Test Connection** tootest hello connection.</span></span>
12. <span data-ttu-id="1c800-156">**범주** 아래에서 **Machine Learning**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-156">Under **Categories**, ensure **Machine Learning** is selected.</span></span>
13. <span data-ttu-id="1c800-157">완료 되 면 메타 데이터를 hello 모든 입력 자신의 구독에 대 한 클릭 **게시**, 차례로 **tooStaging 푸시**합니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-157">When you are done entering all hello metadata about your offer, click on **Publish**, and then **Push tooStaging**.</span></span> <span data-ttu-id="1c800-158">이 시점에서 알려의 나머지 문제 toofix 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-158">At this point, you will be notified of any remaining issues that you need toofix.</span></span>
14. <span data-ttu-id="1c800-159">Hello 미해결 문제를 모두 완료 했을 후 클릭 **요청 승인 toopush tooProduction**합니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-159">After you have ensured completion of all hello outstanding issues, click on **Request approval toopush tooProduction**.</span></span> <span data-ttu-id="1c800-160">hello 게시 프로세스에 비즈니스 며칠 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c800-160">hello publishing process can take a few business days.</span></span> 

[image1]:./media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:./media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:./media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:./media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:./media/machine-learning-publish-web-service-to-azure-marketplace/odata.png

