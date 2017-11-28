---
title: "Machine Learning에서 웹 서비스 끝점 만들기 | Microsoft Docs"
description: "Azure Machine Learning에서 웹 서비스 끝점 만들기"
services: machine-learning
documentationcenter: 
author: hiteshmadan
manager: padou
editor: cgronlun
ms.assetid: 4657fc1b-5228-4950-a29e-bc709259f728
ms.service: machine-learning
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 10/04/2016
ms.author: himad
ms.openlocfilehash: 9f83ffc9cf7dbe37c1ce9980fd7f5b9133fe78f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-endpoints"></a><span data-ttu-id="e4506-103">끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="e4506-103">Creating Endpoints</span></span>
> [!NOTE]
>  <span data-ttu-id="e4506-104">이 항목에서는 **기존** Machine Learning 웹 서비스에 적용되는 기술을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-104">This topic describes techniques applicable to a **Classic** Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="e4506-105">고객에게 판매할 웹 서비스를 만들 때는 웹 서비스를 만든 실험에 아직 연결되어 있는 각 고객에게 학습된 모델을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-105">When you create Web services that you sell forward to your customers, you need to provide trained models to each customer that are still linked to the experiment from which the Web service was created.</span></span> <span data-ttu-id="e4506-106">또한 사용자 지정을 덮어쓰지 않고 실험의 모든 업데이트를 끝점에 선택적으로 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-106">In addition, any updates to the experiment should be applied selectively to an endpoint without overwriting the customizations.</span></span>

<span data-ttu-id="e4506-107">이를 위해 Azure Machine Learning을 사용하면 배포된 웹 서비스에 대한 여러 끝점을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-107">To accomplish this, Azure Machine Learning allows you to create multiple endpoints for a deployed Web service.</span></span> <span data-ttu-id="e4506-108">웹 서비스의 각 끝점은 독립적으로 처리, 제한 및 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-108">Each endpoint in the Web service is independently addressed, throttled, and managed.</span></span> <span data-ttu-id="e4506-109">각 끝점에는 고객에게 배포할 수 있는 고유한 URL 및 권한 부여 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-109">Each endpoint is a unique URL and authorization key that you can distribute to your customers.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-to-a-web-service"></a><span data-ttu-id="e4506-110">웹 서비스에 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="e4506-110">Adding endpoints to a Web service</span></span>
<span data-ttu-id="e4506-111">웹 서비스에 끝점을 추가하는 방법은 세 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-111">There are three ways to add an endpoint to a Web service.</span></span>

* <span data-ttu-id="e4506-112">프로그래밍 방식</span><span class="sxs-lookup"><span data-stu-id="e4506-112">Programmatically</span></span>
* <span data-ttu-id="e4506-113">Azure Machine Learning 웹 서비스 포털을 통해</span><span class="sxs-lookup"><span data-stu-id="e4506-113">Through the Azure Machine Learning Web Services portal</span></span>
* <span data-ttu-id="e4506-114">Azure 클래식 포털을 통해</span><span class="sxs-lookup"><span data-stu-id="e4506-114">Though the Azure classic portal</span></span>

<span data-ttu-id="e4506-115">끝점이 만들어지면 동기 API, 일괄 처리 API 및 Excel 워크시트를 통해 끝점을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-115">Once the endpoint is created, you can consume it through synchronous APIs, batch APIs, and excel worksheets.</span></span> <span data-ttu-id="e4506-116">또한 이 UI 통해 끝점을 추가하는 것 외에도 끝점 관리 API를 사용하여 프로그래밍 방식으로 끝점을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-116">In addition to adding endpoints through this UI, you can also use the Endpoint Management APIs to programmatically add endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="e4506-117">웹 서비스에 끝점을 더 추가한 경우 기본 끝점은 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-117">If you have added additional endpoints to the Web service, you cannot delete the default endpoint.</span></span>
> 
> 

## <a name="adding-an-endpoint-programmatically"></a><span data-ttu-id="e4506-118">프로그래밍 방식으로 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="e4506-118">Adding an endpoint programmatically</span></span>
<span data-ttu-id="e4506-119">[AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) 샘플 코드를 사용하여 프로그래밍 방식으로 웹 서비스에 끝점을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-119">You can add an endpoint to your Web service programmatically using the [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>

## <a name="adding-an-endpoint-using-the-azure-machine-learning-web-services-portal"></a><span data-ttu-id="e4506-120">Azure Machine Learning 웹 서비스 포털을 사용하여 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="e4506-120">Adding an endpoint using the Azure Machine Learning Web Services portal</span></span>
1. <span data-ttu-id="e4506-121">Machine Learning Studio의 왼쪽 탐색 열에서 Web Services를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-121">In Machine Learning Studio, on the left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="e4506-122">웹 서비스 대시보드 아래쪽에서 **끝점 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-122">At the bottom of the Web service dashboard, click **Manage endpoints**.</span></span> <span data-ttu-id="e4506-123">Azure Machine Learning 웹 서비스 포털에 웹 서비스 끝점 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-123">The Azure Machine Learning Web Services portal opens to the endpoints page for the Web service.</span></span>
3. <span data-ttu-id="e4506-124">**새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-124">Click **New**.</span></span>
4. <span data-ttu-id="e4506-125">새 끝점에 대한 이름 및 설명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-125">Type a name and description for the new endpoint.</span></span> <span data-ttu-id="e4506-126">끝점 이름은 길이가 24자 이하이고 알파벳 소문자 또는 숫자로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-126">Endpoint names must be 24 character or less in length, and must be made up of lower-case alphabets or numbers.</span></span> <span data-ttu-id="e4506-127">로깅 수준 및 예제 데이터 사용 여부를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-127">Select the logging level and whether sample data is enabled.</span></span> <span data-ttu-id="e4506-128">로깅에 대한 자세한 내용은 [Machine Learning 웹 서비스에 대한 로깅 사용](machine-learning-web-services-logging.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4506-128">For more information on logging, see [Enable logging for Machine Learning Web services](machine-learning-web-services-logging.md).</span></span>

## <a name="adding-an-endpoint-using-the-azure-classic-portal"></a><span data-ttu-id="e4506-129">Azure 클래식 포털을 사용하여 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="e4506-129">Adding an endpoint using the Azure classic portal</span></span>
1. <span data-ttu-id="e4506-130">[Azure 클래식 포털](http://manage.windowsazure.com)에 로그인한 후 왼쪽 열에서 **Machine Learning**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-130">Sign in to the [Azure classic portal](http://manage.windowsazure.com), click **Machine Learning** in the left column.</span></span> <span data-ttu-id="e4506-131">관심 있는 웹 서비스가 포함되어 있는 작업 영역을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-131">Click the workspace which contains the Web service in which you are interested.</span></span>
   
    ![작업 영역으로 이동](./media/machine-learning-create-endpoint/figure-1.png)
2. <span data-ttu-id="e4506-133">**웹 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-133">Click **Web Services**.</span></span>
   
    ![웹 서비스로 이동](./media/machine-learning-create-endpoint/figure-2.png)
3. <span data-ttu-id="e4506-135">사용 가능한 끝점 목록을 확인할 웹 서비스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-135">Click the Web service you're interested in to see the list of available endpoints.</span></span>
   
    ![끝점으로 이동](./media/machine-learning-create-endpoint/figure-3.png)
4. <span data-ttu-id="e4506-137">페이지 맨 아래에 있는 **끝점 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-137">At the bottom of the page, click **Add Endpoint**.</span></span> <span data-ttu-id="e4506-138">이름 및 설명을 입력하고 이 웹 서비스에 같은 이름의 다른 끝점이 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-138">Type a name and description, ensure there are no other endpoints with the same name in this Web service.</span></span> <span data-ttu-id="e4506-139">특별한 요구 사항이 없는 경우 제한 수준을 해당 기본값으로 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e4506-139">Leave the throttle level with its default value unless you have special requirements.</span></span> <span data-ttu-id="e4506-140">제한에 대해 자세히 알아보려면 [API 끝점 확장](machine-learning-scaling-webservice.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4506-140">To learn more about throttling, see [Scaling API Endpoints](machine-learning-scaling-webservice.md).</span></span>
   
    ![끝점 만들기](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a><span data-ttu-id="e4506-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e4506-142">Next Steps</span></span>
<span data-ttu-id="e4506-143">[Azure Machine Learning 웹 서비스 사용 방법](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="e4506-143">[How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

