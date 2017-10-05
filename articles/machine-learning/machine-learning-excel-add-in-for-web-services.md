---
title: "Machine Learning 웹 서비스용 Excel 추가 기능 | Microsoft Docs"
description: "코드를 작성하지 않고 Excel에서 직접 Azure Machine Learning 웹 서비스를 사용하는 방법입니다."
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 9618079d-502f-4974-a3e2-8f924042a23f
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/14/2017
ms.author: tedway;garye
ms.openlocfilehash: 0d60dd87bbdd4d3eafac0f8876cc9e41412a53ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="excel-add-in-for-azure-machine-learning-web-services"></a><span data-ttu-id="f912e-103">Azure 기계 학습 웹 서비스용 Excel 추가 기능</span><span class="sxs-lookup"><span data-stu-id="f912e-103">Excel Add-in for Azure Machine Learning web services</span></span>
<span data-ttu-id="f912e-104">Excel을 사용하면 코드를 작성할 필요 없이 쉽게 직접 웹 서비스를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-104">Excel makes it easy to call web services directly without the need to write any code.</span></span>

## <a name="steps-to-use-an-existing-web-service-in-the-workbook"></a><span data-ttu-id="f912e-105">통합 문서에서 기존 웹 서비스를 사용하는 단계</span><span class="sxs-lookup"><span data-stu-id="f912e-105">Steps to Use an Existing web service in the Workbook</span></span>

1. <span data-ttu-id="f912e-106">타이타닉호의 승객에 대한 데이터와 Excel 추가 기능이 들어 있는 [샘플 Excel 파일](http://aka.ms/amlexcel-sample-2)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-106">Open the [sample Excel file](http://aka.ms/amlexcel-sample-2), which contains the Excel add-in and data about passengers on the Titanic.</span></span>
2. <span data-ttu-id="f912e-107">웹 서비스를 클릭하여 선택합니다(이 예제의 경우 "Titanic Survivor Predictor (Excel Add-in Sample) [Score]").</span><span class="sxs-lookup"><span data-stu-id="f912e-107">Choose the web service by clicking it - "Titanic Survivor Predictor (Excel Add-in Sample) [Score]" in this example.</span></span>
   
    ![웹 서비스 선택][01]
3. <span data-ttu-id="f912e-109">이렇게 하면 **Predict** 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-109">This takes you to the **Predict** section.</span></span>  <span data-ttu-id="f912e-110">이 통합 문서에는 이미 샘플 데이터가 포함되어 있지만 통합 문서가 비어 있는 경우에는 Excel에서 셀 하나를 선택하고 **샘플 데이터 사용**을 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-110">This workbook already contains sample data, but for a blank workbook you can select a cell in Excel and click **Use sample data**.</span></span>
4. <span data-ttu-id="f912e-111">머리글이 있는 데이터를 선택하고 입력 데이터 범위 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-111">Select the data with headers and click the input data range icon.</span></span>  <span data-ttu-id="f912e-112">"My data has headers" 상자가 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-112">Make sure the "My data has headers" box is checked.</span></span>
5. <span data-ttu-id="f912e-113">**Output** 아래에 출력을 배치할 셀 번호를 입력합니다(여기서는 "H1").</span><span class="sxs-lookup"><span data-stu-id="f912e-113">Under **Output**, enter the cell number where you want the output to be, for example "H1" here.</span></span>
6. <span data-ttu-id="f912e-114">**Predict**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-114">Click **Predict**.</span></span>
   
    ![Predict 섹션][02]

<span data-ttu-id="f912e-116">웹 서비스를 배포하거나 기존 웹 서비스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-116">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="f912e-117">웹 서비스 배포에 대한 자세한 내용은 [연습 5 단계: Azure Machine Learning 웹 서비스 배포](machine-learning-walkthrough-5-publish-web-service.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f912e-117">For more information on deploying a web service, see [Walkthrough Step 5: Deploy the Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

<span data-ttu-id="f912e-118">웹 서비스에 대한 API 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-118">Get the API key for your web service.</span></span> <span data-ttu-id="f912e-119">새 Machine Learning 웹 서비스의 기존 Machine Learning 웹 서비스를 게시했는지 여부에 따라 이 작업을 수행하는 위치가 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-119">Where you perform this action depends on whether you published a Classic Machine Learning web service of a New Machine Learning web service.</span></span>

<span data-ttu-id="f912e-120">**기존 웹 서비스 사용**</span><span class="sxs-lookup"><span data-stu-id="f912e-120">**Use a Classic web service**</span></span> 

1. <span data-ttu-id="f912e-121">기계 학습 스튜디오에서 왼쪽 창의 **WEB SERVICES** 섹션을 클릭한 다음 웹 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-121">In Machine Learning Studio, click the **WEB SERVICES** section in the left pane, and then select the web service.</span></span>
   
    ![Studio 웹 서비스 선택][04]
2. <span data-ttu-id="f912e-123">웹 서비스에 대한 API 키를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-123">Copy the API key for the web service.</span></span>
   
    ![Studio API 키][05]
3. <span data-ttu-id="f912e-125">웹 서비스의 **DASHBOARD** 탭에서 **REQUEST/RESPONSE** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-125">On the **DASHBOARD** tab for the web service, click the **REQUEST/RESPONSE** link.</span></span>
4. <span data-ttu-id="f912e-126">**요청 URI** 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-126">Look for the **Request URI** section.</span></span>  <span data-ttu-id="f912e-127">URL을 복사하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-127">Copy and save the URL.</span></span>

> [!NOTE]
> <span data-ttu-id="f912e-128">이제 [Azure Machine Learning 웹 서비스](https://services.azureml.net) 포털에 로그인하여 기존 Machine Learning 웹 서비스에 대한 API 키를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-128">It is now possible to sign into the [Azure Machine Learning Web Services](https://services.azureml.net) portal to obtain the API key for a Classic Machine Learning web service.</span></span>
> 
> 

<span data-ttu-id="f912e-129">**새 웹 서비스 사용**</span><span class="sxs-lookup"><span data-stu-id="f912e-129">**Use a New web service**</span></span>

1. <span data-ttu-id="f912e-130">[Azure Machine Learning 웹 서비스](https://services.azureml.net) 포털에서 **웹 서비스**를 클릭한 다음 웹 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-130">In the [Azure Machine Learning Web Services](https://services.azureml.net) portal, click **Web Services**, then select your web service.</span></span> 
2. <span data-ttu-id="f912e-131">**사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-131">Click **Consume**.</span></span>
3. <span data-ttu-id="f912e-132">**기본 사용량 정보** 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-132">Look for the **Basic consumption info** section.</span></span> <span data-ttu-id="f912e-133">**기본 키** 및 **요청-응답** URL을 복사하여 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-133">Copy and save the **Primary Key** and the **Request-Response** URL.</span></span>

## <a name="steps-to-add-a-new-web-service"></a><span data-ttu-id="f912e-134">새 웹 서비스 추가 단계</span><span class="sxs-lookup"><span data-stu-id="f912e-134">Steps to Add a New web service</span></span>

1. <span data-ttu-id="f912e-135">웹 서비스를 배포하거나 기존 웹 서비스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-135">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="f912e-136">웹 서비스 배포에 대한 자세한 내용은 [연습 5 단계: Azure Machine Learning 웹 서비스 배포](machine-learning-walkthrough-5-publish-web-service.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f912e-136">For more information on deploying a web service, see [Walkthrough Step 5: Deploy the Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
2. <span data-ttu-id="f912e-137">**사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-137">Click **Consume**.</span></span>
3. <span data-ttu-id="f912e-138">**기본 사용량 정보** 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-138">Look for the **Basic consumption info** section.</span></span> <span data-ttu-id="f912e-139">**기본 키** 및 **요청-응답** URL을 복사하여 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-139">Copy and save the **Primary Key** and the **Request-Response** URL.</span></span>
4. <span data-ttu-id="f912e-140">Excel에서 **웹 서비스** 섹션으로 이동합니다(**Predict** 섹션에 있는 경우 뒤로 화살표를 클릭하여 웹 서비스 목록으로 이동).</span><span class="sxs-lookup"><span data-stu-id="f912e-140">In Excel, go to the **Web Services** section (if you are in the **Predict** section, click the back arrow to go to the list of web services).</span></span>
   
    ![웹 서비스 선택으로 이동][03]
5. <span data-ttu-id="f912e-142">**Add Web Service**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-142">Click **Add Web Service**.</span></span>
6. <span data-ttu-id="f912e-143">URL을 **URL**이라고 레이블이 지정된 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-143">Paste the URL into the Excel add-in text box labeled **URL**.</span></span>
7. <span data-ttu-id="f912e-144">API/기본 키를 **API 키**텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-144">Paste the API/Primary key into the text box labeled **API key**.</span></span>
8. <span data-ttu-id="f912e-145">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-145">Click **Add**.</span></span>
   
    ![기존 웹 서비스에 대한 URL 및 API 키.][06]
9. <span data-ttu-id="f912e-147">웹 서비스를 사용하려면 위의 지침 "기존 웹 서비스를 사용하는 단계"를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-147">To use the web service, follow the preceding directions, "Steps to Use an Existing web Service."</span></span>

## <a name="sharing-your-workbook"></a><span data-ttu-id="f912e-148">통합 문서 공유</span><span class="sxs-lookup"><span data-stu-id="f912e-148">Sharing Your Workbook</span></span>
<span data-ttu-id="f912e-149">통합 문서를 저장하면 추가한 웹 서비스의 API/기본 키도 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-149">If you save your workbook, then the API/Primary key for the web services you have added is also saved.</span></span> <span data-ttu-id="f912e-150">즉, 신뢰할 수 있는 사용자와만 통합 문서를 공유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-150">That means you should only share the workbook with individuals you trust.</span></span>

<span data-ttu-id="f912e-151">다음 설명 섹션 또는 [포럼](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409)에서 질문을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f912e-151">Ask any questions in the following comment section or on our [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span></span>

[01]: ./media/machine-learning-excel-add-in-for-web-services/image1.png
[02]: ./media/machine-learning-excel-add-in-for-web-services/image2.png
[03]: ./media/machine-learning-excel-add-in-for-web-services/image3.png
[04]: ./media/machine-learning-excel-add-in-for-web-services/image4.png
[05]: ./media/machine-learning-excel-add-in-for-web-services/image5.png
[06]: ./media/machine-learning-excel-add-in-for-web-services/image6.png
