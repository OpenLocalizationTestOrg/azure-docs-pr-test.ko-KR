---
title: "aaaExcel 추가 기능에서 컴퓨터 학습 웹 서비스에 대 한 | Microsoft Docs"
description: "어떻게 toouse Azure 컴퓨터 학습 웹 서비스 Excel에서 직접 코드를 작성 합니다."
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
ms.openlocfilehash: c52f40d33c9907f284e4750afe47181dc3365fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="excel-add-in-for-azure-machine-learning-web-services"></a><span data-ttu-id="fa687-103">Azure 기계 학습 웹 서비스용 Excel 추가 기능</span><span class="sxs-lookup"><span data-stu-id="fa687-103">Excel Add-in for Azure Machine Learning web services</span></span>
<span data-ttu-id="fa687-104">Excel 하면 쉽게 toocall 웹 서비스 직접 hello toowrite 모든 코드가 필요 하지 않고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-104">Excel makes it easy toocall web services directly without hello need toowrite any code.</span></span>

## <a name="steps-toouse-an-existing-web-service-in-hello-workbook"></a><span data-ttu-id="fa687-105">단계 tooUse hello 통합 문서에에서는 기존 웹 서비스</span><span class="sxs-lookup"><span data-stu-id="fa687-105">Steps tooUse an Existing web service in hello Workbook</span></span>

1. <span data-ttu-id="fa687-106">열기 hello [샘플 Excel 파일](http://aka.ms/amlexcel-sample-2)hello Excel 추가 기능에 포함 되어 있지 않으며 승객에 대 한 데이터 hello Titanic 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-106">Open hello [sample Excel file](http://aka.ms/amlexcel-sample-2), which contains hello Excel add-in and data about passengers on hello Titanic.</span></span>
2. <span data-ttu-id="fa687-107">클릭 하 여 hello 웹 서비스 선택-"모아 만든 Survivor 예측 (Excel 추가 기능 샘플) [점수]"이 예에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-107">Choose hello web service by clicking it - "Titanic Survivor Predictor (Excel Add-in Sample) [Score]" in this example.</span></span>
   
    ![웹 서비스 선택][01]
3. <span data-ttu-id="fa687-109">이렇게 하면 toohello **Predict** 섹션.</span><span class="sxs-lookup"><span data-stu-id="fa687-109">This takes you toohello **Predict** section.</span></span>  <span data-ttu-id="fa687-110">이 통합 문서에는 이미 샘플 데이터가 포함되어 있지만 통합 문서가 비어 있는 경우에는 Excel에서 셀 하나를 선택하고 **샘플 데이터 사용**을 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-110">This workbook already contains sample data, but for a blank workbook you can select a cell in Excel and click **Use sample data**.</span></span>
4. <span data-ttu-id="fa687-111">헤더를 사용 하 여 hello 데이터를 선택 하 고 hello 입력된 데이터 범위 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-111">Select hello data with headers and click hello input data range icon.</span></span>  <span data-ttu-id="fa687-112">Hello "내 데이터에 머리글" 확인란을 선택 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-112">Make sure hello "My data has headers" box is checked.</span></span>
5. <span data-ttu-id="fa687-113">아래 **출력**를 저장할 출력 toobe, 예를 들어 "H1" 여기 hello hello 셀 번호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-113">Under **Output**, enter hello cell number where you want hello output toobe, for example "H1" here.</span></span>
6. <span data-ttu-id="fa687-114">**Predict**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-114">Click **Predict**.</span></span>
   
    ![Predict 섹션][02]

<span data-ttu-id="fa687-116">웹 서비스를 배포하거나 기존 웹 서비스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-116">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="fa687-117">웹 서비스를 배포 하는 방법에 대 한 자세한 내용은 참조 하십시오. [연습 5 단계: hello Azure 컴퓨터 학습 웹 서비스를 배포](machine-learning-walkthrough-5-publish-web-service.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-117">For more information on deploying a web service, see [Walkthrough Step 5: Deploy hello Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

<span data-ttu-id="fa687-118">웹 서비스에 대 한 hello API 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-118">Get hello API key for your web service.</span></span> <span data-ttu-id="fa687-119">새 Machine Learning 웹 서비스의 기존 Machine Learning 웹 서비스를 게시했는지 여부에 따라 이 작업을 수행하는 위치가 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-119">Where you perform this action depends on whether you published a Classic Machine Learning web service of a New Machine Learning web service.</span></span>

<span data-ttu-id="fa687-120">**기존 웹 서비스 사용**</span><span class="sxs-lookup"><span data-stu-id="fa687-120">**Use a Classic web service**</span></span> 

1. <span data-ttu-id="fa687-121">기계 학습 스튜디오에서 클릭 hello **웹 서비스** hello 왼쪽된 창에서 섹션 및 다음 hello 웹 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-121">In Machine Learning Studio, click hello **WEB SERVICES** section in hello left pane, and then select hello web service.</span></span>
   
    ![Studio 웹 서비스 선택][04]
2. <span data-ttu-id="fa687-123">Hello 웹 서비스에 대 한 hello API 키를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-123">Copy hello API key for hello web service.</span></span>
   
    ![Studio API 키][05]
3. <span data-ttu-id="fa687-125">Hello에 **대시보드** hello 웹 서비스에 대 한 탭에서 hello **요청/응답** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-125">On hello **DASHBOARD** tab for hello web service, click hello **REQUEST/RESPONSE** link.</span></span>
4. <span data-ttu-id="fa687-126">Hello에 대 한 확인 **요청 URI** 섹션.</span><span class="sxs-lookup"><span data-stu-id="fa687-126">Look for hello **Request URI** section.</span></span>  <span data-ttu-id="fa687-127">복사 하 고 hello URL을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-127">Copy and save hello URL.</span></span>

> [!NOTE]
> <span data-ttu-id="fa687-128">이제는 hello에 가능한 toosign [Azure 컴퓨터 학습 웹 서비스](https://services.azureml.net) 클래식 기계 학습 웹 서비스에 대 한 포털 tooobtain hello API 키입니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-128">It is now possible toosign into hello [Azure Machine Learning Web Services](https://services.azureml.net) portal tooobtain hello API key for a Classic Machine Learning web service.</span></span>
> 
> 

<span data-ttu-id="fa687-129">**새 웹 서비스 사용**</span><span class="sxs-lookup"><span data-stu-id="fa687-129">**Use a New web service**</span></span>

1. <span data-ttu-id="fa687-130">Hello에 [Azure 컴퓨터 학습 웹 서비스](https://services.azureml.net) 포털 **웹 서비스**, 웹 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-130">In hello [Azure Machine Learning Web Services](https://services.azureml.net) portal, click **Web Services**, then select your web service.</span></span> 
2. <span data-ttu-id="fa687-131">**사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-131">Click **Consume**.</span></span>
3. <span data-ttu-id="fa687-132">Hello에 대 한 확인 **기본 소비 정보** 섹션.</span><span class="sxs-lookup"><span data-stu-id="fa687-132">Look for hello **Basic consumption info** section.</span></span> <span data-ttu-id="fa687-133">복사 하 고 hello 저장 **기본 키** 및 hello **요청-응답** URL입니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-133">Copy and save hello **Primary Key** and hello **Request-Response** URL.</span></span>

## <a name="steps-tooadd-a-new-web-service"></a><span data-ttu-id="fa687-134">단계 tooAdd 새 웹 서비스</span><span class="sxs-lookup"><span data-stu-id="fa687-134">Steps tooAdd a New web service</span></span>

1. <span data-ttu-id="fa687-135">웹 서비스를 배포하거나 기존 웹 서비스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-135">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="fa687-136">웹 서비스를 배포 하는 방법에 대 한 자세한 내용은 참조 하십시오. [연습 5 단계: hello Azure 컴퓨터 학습 웹 서비스를 배포](machine-learning-walkthrough-5-publish-web-service.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-136">For more information on deploying a web service, see [Walkthrough Step 5: Deploy hello Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
2. <span data-ttu-id="fa687-137">**사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-137">Click **Consume**.</span></span>
3. <span data-ttu-id="fa687-138">Hello에 대 한 확인 **기본 소비 정보** 섹션.</span><span class="sxs-lookup"><span data-stu-id="fa687-138">Look for hello **Basic consumption info** section.</span></span> <span data-ttu-id="fa687-139">복사 하 고 hello 저장 **기본 키** 및 hello **요청-응답** URL입니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-139">Copy and save hello **Primary Key** and hello **Request-Response** URL.</span></span>
4. <span data-ttu-id="fa687-140">Excel에서 toohello 이동 **웹 서비스** 섹션 (hello에 있는 경우 **Predict** 섹션에서 웹 서비스의 hello toogo toohello 목록을 뒤로 화살표를 클릭).</span><span class="sxs-lookup"><span data-stu-id="fa687-140">In Excel, go toohello **Web Services** section (if you are in hello **Predict** section, click hello back arrow toogo toohello list of web services).</span></span>
   
    ![이동 tooWeb 서비스 선택][03]
5. <span data-ttu-id="fa687-142">**Add Web Service**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-142">Click **Add Web Service**.</span></span>
6. <span data-ttu-id="fa687-143">Excel 추가 기능에서 텍스트 상자에 레이블이 지정 된 hello hello URL을 붙여 **URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-143">Paste hello URL into hello Excel add-in text box labeled **URL**.</span></span>
7. <span data-ttu-id="fa687-144">레이블이 지정 된 hello 텍스트 상자로 붙여넣기 hello API/기본 키 **API 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-144">Paste hello API/Primary key into hello text box labeled **API key**.</span></span>
8. <span data-ttu-id="fa687-145">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-145">Click **Add**.</span></span>
   
    ![기존 웹 서비스에 대한 URL 및 API 키.][06]
9. <span data-ttu-id="fa687-147">toouse hello 웹 서비스는 hello 앞 방향에 따라, "단계 tooUse 기존 웹 서비스입니다."</span><span class="sxs-lookup"><span data-stu-id="fa687-147">toouse hello web service, follow hello preceding directions, "Steps tooUse an Existing web Service."</span></span>

## <a name="sharing-your-workbook"></a><span data-ttu-id="fa687-148">통합 문서 공유</span><span class="sxs-lookup"><span data-stu-id="fa687-148">Sharing Your Workbook</span></span>
<span data-ttu-id="fa687-149">통합 문서를 저장 하는 경우 추가 했으면 hello 웹 서비스에 대 한 hello API/기본 키도 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-149">If you save your workbook, then hello API/Primary key for hello web services you have added is also saved.</span></span> <span data-ttu-id="fa687-150">즉, 신뢰할 수 개인과 hello 통합 문서를 공유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-150">That means you should only share hello workbook with individuals you trust.</span></span>

<span data-ttu-id="fa687-151">다음 설명 섹션 또는 hello에서 모든 질문 하기 우리의 [포럼](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa687-151">Ask any questions in hello following comment section or on our [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span></span>

[01]: ./media/machine-learning-excel-add-in-for-web-services/image1.png
[02]: ./media/machine-learning-excel-add-in-for-web-services/image2.png
[03]: ./media/machine-learning-excel-add-in-for-web-services/image3.png
[04]: ./media/machine-learning-excel-add-in-for-web-services/image4.png
[05]: ./media/machine-learning-excel-add-in-for-web-services/image5.png
[06]: ./media/machine-learning-excel-add-in-for-web-services/image6.png
