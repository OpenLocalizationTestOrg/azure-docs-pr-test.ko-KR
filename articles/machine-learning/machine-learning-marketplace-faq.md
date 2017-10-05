---
title: "(사용되지 않음) FAQ: Azure Marketplace에서 Machine Learning 앱 게시 및 사용 | Microsoft Docs"
description: "(사용되지 않음) Azure Marketplace에서 Machine Learning 앱 게시에 관한 FAQ"
services: machine-learning
documentationcenter: 
author: bharaths
manager: jhubbard
editor: cgronlun
ms.assetid: 26b3a1e7-8b9a-4004-98bc-17456d4c25e8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: a4631dfeb2f817b3a3c612a8f6af48398e4f2ab9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-publishing-and-using-machine-learning-apps-in-the-azure-marketplace-faq"></a><span data-ttu-id="e7450-103">(사용되지 않음) Azure Marketplace에서 Machine Learning 앱 게시 및 사용: FAQ</span><span class="sxs-lookup"><span data-stu-id="e7450-103">(deprecated) Publishing and using Machine Learning apps in the Azure Marketplace: FAQ</span></span>

> [!NOTE]
> <span data-ttu-id="e7450-104">DataMarket 및 Data Services는 종료되며 기존 구독은 2017년 3월 31일부터 종료 및 취소됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7450-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span></span> <span data-ttu-id="e7450-105">결과적으로,이 문서는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e7450-105">As a result, this article is being deprecated.</span></span> 
> 
> <span data-ttu-id="e7450-106">대안으로, 데이터 과학 커뮤니티를 위하여 [Cortana Intelligence 갤러리](https://gallery.cortanaintelligence.com/)에 Machine Learning 실험을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7450-106">As an alternative, you can publish your Machine Learning experiments to the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for the benefit of the data science community.</span></span> <span data-ttu-id="e7450-107">자세한 내용은 [Cortana Intelligence 갤러리에서 리소스 공유 및 검색](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="e7450-107">For more information, see [Share and discover resources in the Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span></span>


## <a name="questions-about-consuming-from-marketplace"></a><span data-ttu-id="e7450-108">마켓플레이스에서의 사용 관련 질문</span><span class="sxs-lookup"><span data-stu-id="e7450-108">Questions about consuming from Marketplace</span></span>
<span data-ttu-id="e7450-109">**1. 웹 서비스에 입력한 후에 다음과 같은 오류 메시지가 표시되는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="e7450-109">**1. Why do I get the following error message after I enter input for the web service:**</span></span>

<span data-ttu-id="e7450-110">**요청으로 인해 백 엔드 시간 초과 또는 백 엔드 오류가 발생했습니다. 해당 팀에서 이 문제를 조사하고 있습니다. 불편을 드려 죄송합니다. (500)**</span><span class="sxs-lookup"><span data-stu-id="e7450-110">**The request resulted in a back-end time out or back-end error. The team is investigating the issue. We are sorry for the inconvenience. (500)**</span></span>

<span data-ttu-id="e7450-111">입력 매개 변수가 특정 웹 서비스에 필요한 형식을 준수하지 않은 것일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7450-111">Your input parameter(s) may not conform to the required format for the specific web service.</span></span> <span data-ttu-id="e7450-112">이 웹 서비스의 입력 매개 변수에 대한 올바른 형식 및 제한을 찾으려면 해당 설명서 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7450-112">Please refer to the corresponding documentation link to find the correct format for input parameters and the limitations of this web service.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="e7450-113">**2. “이 데이터 집합 탐색” 페이지에 표시된 웹 서비스의 API 링크를 복사하여 다른 브라우저 창에 붙여 넣는 경우 결과에 액세스하는 데 사용해야 하는 자격 증명은 무엇이며, 결과를 보는 방법은 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="e7450-113">**2. If I copy the API link for the web service that I see on the "Explore this dataset" page and paste it into another browser window, what credentials should I use to access the results, and how do I see them?**</span></span>

<span data-ttu-id="e7450-114">마켓플레이스 계정을 사용자 이름으로 사용하고 기본 계정 키를 암호로 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7450-114">You should use your Marketplace account as the username and the primary account key as the password.</span></span> <span data-ttu-id="e7450-115">기본 계정 키는 **이 데이터 집합 탐색** 페이지의 웹 서비스 설명에서 찾을 수 있습니다(**표시** 단추 클릭).</span><span class="sxs-lookup"><span data-stu-id="e7450-115">The primary account key can be found on the **Explore this dataset** page under the description of the web service (click the **show** button).</span></span> <span data-ttu-id="e7450-116">사용 중인 브라우저에 따라 결과가 브라우저에 표시되거나 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7450-116">The result may display in the browser or it may be available to  download, depending on which browser you are using.</span></span>

<span data-ttu-id="e7450-117">**3. 웹 서비스의 “이 데이터 집합 탐색" 페이지에 입력한 후에 다음과 같은 오류 메시지가 표시되는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="e7450-117">**3. Why do I get the following error message after I enter the input for the web service on the "Explore this dataset" page:**</span></span> 

<span data-ttu-id="e7450-118">**요청을 처리하는 동안 예기치 않은 오류가 발생했습니다. 나중에 다시 시도하세요.**</span><span class="sxs-lookup"><span data-stu-id="e7450-118">**An unexpected error occurred while processing your request. Please try again.**</span></span>

<span data-ttu-id="e7450-119">마켓플레이스 **이 데이터 집합 탐색** 페이지에서 웹 서비스를 사용할 때 웹 서비스의 하나 이상의 입력 매개 변수가 길이 제한을 초과했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7450-119">One or more input parameters of your web service may have exceeded the length limit when consuming the web service on the marketplace **Explore this dataset** page.</span></span> <span data-ttu-id="e7450-120">HTTP POST 메서드를 사용하여 좀 더 길게 입력하여 서비스를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7450-120">The services can be called with a longer input length by using HTTP POST methods.</span></span> <span data-ttu-id="e7450-121">예제를 보려면 [기계 학습에서 R을 사용하고 마켓플레이스에 게시되는 샘플 솔루션](machine-learning-r-csharp-web-service-examples.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7450-121">For examples, see [Sample solutions using R on Machine Learning and published to Marketplace](machine-learning-r-csharp-web-service-examples.md).</span></span>

<span data-ttu-id="e7450-122">**4. Azure 클래식 포털의 스토어에서 "API 탐색기" 탭에 아무 내용도 표시되지 않는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="e7450-122">**4. Why do I not see anything in the "API EXPLORER" tab int the Store in the Azure Classic Portal?**</span></span> 

<span data-ttu-id="e7450-123">이것은 Azure 클래식 포털 마켓플레이스의 알려진 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="e7450-123">This is a known issue with the Azure Classic Portal Marketplace.</span></span> <span data-ttu-id="e7450-124">이 문제 해결을 위한 작업이 진행되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7450-124">The team is working to resolve this issue.</span></span> 

## <a name="questions-about-publishing-from-azure-machine-learning-on-marketplace"></a><span data-ttu-id="e7450-125">마켓플레이스에 있는 Azure 기계 학습에서의 게시에 대한 질문</span><span class="sxs-lookup"><span data-stu-id="e7450-125">Questions about publishing from Azure Machine Learning on Marketplace</span></span>
<span data-ttu-id="e7450-126">**1. 내 웹 서비스에 대해 내 로고 또는 이미지 트랜잭션 수가 새로 고쳐지지 않는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="e7450-126">**1. Why are my transactions of logos or images not refreshing for my web service?**</span></span> 

<span data-ttu-id="e7450-127">로고 및 이미지는 게시 포털에 캐싱되며 포털에서 새 로고 또는 이미지가 업데이트되기까지 최대 10일이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7450-127">Logos and images are cached in the publishing portal, and it may take up to 10 days for the new logo or image to update on the portal.</span></span>

<span data-ttu-id="e7450-128">**2. 마켓플레이스에서 내 웹 서비스의 "세부 정보" 탭에 오류 메시지가 표시되는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="e7450-128">**2. Why is the “Detail" tab of my web service on Marketplace showing an error message?**</span></span>

<span data-ttu-id="e7450-129">서비스 세부 정보를 확인하기 위해 Azure 기계 학습에 연결할 때 알려진 마켓플레이스 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7450-129">There is a known Marketplace issue when connecting to Azure Machine Learning for service details.</span></span> <span data-ttu-id="e7450-130">이 문제 해결을 위한 작업이 진행되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7450-130">The team is working to resolve this issue.</span></span>

<span data-ttu-id="e7450-131">**3. Azure 기계 학습 웹 서비스의 R 샘플 코드가 마켓플레이스에서의 웹 서비스 사용에 대해 작동하지 않는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="e7450-131">**3. Why does the R sample code in the Azure Machine Learning web services not work for consuming the web services in Marketplace?**</span></span>

<span data-ttu-id="e7450-132">Azure 기계 학습 웹 서비스에 직접 연결하는 경우와 마켓플레이스를 통해 이러한 웹 서비스에 연결하는 경우의 인증 시스템이 서로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="e7450-132">The authentication systems are different when connecting to Azure Machine Learning web services directly compared to connecting to these web services through the Marketplace.</span></span> <span data-ttu-id="e7450-133">마켓플레이스의 서비스는 OData 서비스이며 GET 또는 POST 메서드를 사용하여 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7450-133">The services in Marketplace are OData services, and they can be called with GET or POST methods.</span></span> 

<span data-ttu-id="e7450-134">**4. 내 웹 서비스 제품의 지원 링크가 일부 내 제품에 대해 올바르게 업데이트되지 않는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="e7450-134">**4. Why are the support links of my web service offers not updating correctly for some of my offers?**</span></span>

<span data-ttu-id="e7450-135">지원 링크는 제품당 전역이 아니라 게시자당 전역입니다.</span><span class="sxs-lookup"><span data-stu-id="e7450-135">The support links are global per publisher, not per offer.</span></span> 

<span data-ttu-id="e7450-136">**5. 마켓플레이스에서 일괄 처리 입력 모드를 통해 웹 서비스를 게시하는 방법은 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="e7450-136">**5. How do I publish a web service with batch input mode in Marketplace?**</span></span>

<span data-ttu-id="e7450-137">현재 마켓플레이스 웹 서비스에서는 일괄 처리 입력 모드가 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e7450-137">The batch input mode is currently not supported in Marketplace web services.</span></span>

<span data-ttu-id="e7450-138">**6. 데이터 게시자가 되는 것에 대한 질문이 있거나 게시 중에 문제가 있는 경우 도움을 얻기 위해 문의해야 하는 사람은 누구인가요?**</span><span class="sxs-lookup"><span data-stu-id="e7450-138">**6. Who should I contact to get help if I have questions about becoming a data publisher, or if I have issues during publishing?**</span></span>

<span data-ttu-id="e7450-139">자세한 내용은 <mailto:datamarketbd@microsoft.com>에서 Azure Marketplace 팀에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="e7450-139">Please contact the Azure Marketplace team at <mailto:datamarketbd@microsoft.com> for more information.</span></span>

