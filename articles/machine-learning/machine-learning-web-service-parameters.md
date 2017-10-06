---
title: "Azure 컴퓨터 학습 웹 서비스 매개 변수가 aaaUse | Microsoft Docs"
description: "어떻게 toouse Azure 컴퓨터 학습 웹 서비스 매개 변수가 toomodify hello hello 웹 서비스에 액세스할 때 모델의 동작입니다."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c49187db-b976-4731-89d6-11a0bf653db1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2017
ms.author: raymondl;garye
ms.openlocfilehash: 214711eb819a6cea34db905abdf015da11e846d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-web-service-parameters"></a><span data-ttu-id="9a315-103">Azure 기계 학습 웹 서비스 매개 변수 사용</span><span class="sxs-lookup"><span data-stu-id="9a315-103">Use Azure Machine Learning Web Service Parameters</span></span>
<span data-ttu-id="9a315-104">Azure 기계 학습 웹 서비스는 구성 가능한 매개 변수로 모듈이 포함된 실험을 게시하여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-104">An Azure Machine Learning web service is created by publishing an experiment that contains modules with configurable parameters.</span></span> <span data-ttu-id="9a315-105">경우에 따라 hello 웹 서비스가 실행 중인 동안 toochange hello 모듈 동작을 원하는 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-105">In some cases, you may want toochange hello module behavior while hello web service is running.</span></span> <span data-ttu-id="9a315-106">*웹 서비스 매개 변수* toodo 사용 하면이 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-106">*Web Service Parameters* allow you toodo this task.</span></span> 

<span data-ttu-id="9a315-107">일반적인 예로 hello를 설정 하 고 [데이터 가져오기] [ reader] 모듈의 hello 해당 hello 사용자 웹 서비스 게시 hello 웹 서비스에 액세스할 때 다른 데이터 원본을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-107">A common example is setting up hello [Import Data][reader] module so that hello user of hello published web service can specify a different data source when hello web service is accessed.</span></span> <span data-ttu-id="9a315-108">Hello 구성 또는 [데이터 내보내기] [ writer] 모듈 다른 위치를 지정할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-108">Or configuring hello [Export Data][writer] module so that a different destination can be specified.</span></span> <span data-ttu-id="9a315-109">다른 몇 가지 예를 들어 hello hello에 대 한 비트 수를 변경 [기능 해시] [ feature-hashing] hello에 대 한 원하는 기능의 수를 모듈 또는 hello [필터 기반 기능 선택] [ filter-based-feature-selection] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-109">Some other examples include changing hello number of bits for hello [Feature Hashing][feature-hashing] module or hello number of desired features for hello [Filter-Based Feature Selection][filter-based-feature-selection] module.</span></span> 

<span data-ttu-id="9a315-110">실험에서 웹 서비스 매개 변수를 설정하여 하나 이상의 모듈 매개 변수와 연결하고 이러한 매개 변수가 필수인지 또는 선택 사항인지 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-110">You can set Web Service Parameters and associate them with one or more module parameters in your experiment, and you can specify whether they are required or optional.</span></span> <span data-ttu-id="9a315-111">다음 hello 웹 서비스의 hello 사용자 hello 웹 서비스를 호출할 때 이러한 매개 변수에 대해 값을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-111">hello user of hello web service can then provide values for these parameters when they call hello web service.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-tooset-and-use-web-service-parameters"></a><span data-ttu-id="9a315-112">어떻게 tooset 및 사용 하 여 웹 서비스 매개 변수</span><span class="sxs-lookup"><span data-stu-id="9a315-112">How tooset and use Web Service Parameters</span></span>
<span data-ttu-id="9a315-113">Hello 아이콘 다음 toohello 매개 변수는 모듈에 대 한 "웹 서비스 매개 변수로 설정"을 선택 하 여 웹 서비스 매개 변수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-113">You define a Web Service Parameter by clicking hello icon next toohello parameter for a module and selecting "Set as web service parameter".</span></span> <span data-ttu-id="9a315-114">이렇게 하면 새 웹 서비스 매개 변수를 만들고이 toothat: 모듈 매개 변수를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-114">This creates a new Web Service Parameter and connects it toothat module parameter.</span></span> <span data-ttu-id="9a315-115">그런 다음 hello 웹 서비스에 액세스 하는 hello 사용자는 웹 서비스 매개 변수 hello에 대 한 값을 지정할 수 있습니다 및 적용 된 toohello 모듈 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-115">Then, when hello web service is accessed, hello user can specify a value for hello Web Service Parameter and it is applied toohello module parameter.</span></span>

<span data-ttu-id="9a315-116">사용 가능한 tooany는 웹 서비스 매개 변수를 정의한 다음 다른: hello 실험에서 모듈 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-116">Once you define a Web Service Parameter, it's available tooany other module parameter in hello experiment.</span></span> <span data-ttu-id="9a315-117">동일한 웹 서비스 매개 변수가 hello 매개 변수 예상 값 같은 유형의으로 hello로 하나의 모듈에 대 한 매개 변수와 연결 된 웹 서비스 매개 변수를 정의 하는 경우, 다른 모듈에 대 한 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-117">If you define a Web Service Parameter associated with a parameter for one module, you can use that same Web Service Parameter for any other module, as long as hello parameter expects hello same type of value.</span></span> <span data-ttu-id="9a315-118">예를 들어 hello 웹 서비스 매개 변수는 숫자 값 이면 다음만 사용할 수 있습니다에 대 한 숫자 값을 예상 하는 모듈 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-118">For example, if hello Web Service Parameter is a numeric value, then it can only be used for module parameters that expect a numeric value.</span></span> <span data-ttu-id="9a315-119">Hello 사용자 웹 서비스 매개 변수 hello에 대 한 값을 설정 하는 경우 관련 된 적용된 tooall 모듈 매개 변수를 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-119">When hello user sets a value for hello Web Service Parameter, it will be applied tooall associated module parameters.</span></span>

<span data-ttu-id="9a315-120">결정할 수 tooprovide 기본 hello 웹 서비스 매개 변수 값 여부.</span><span class="sxs-lookup"><span data-stu-id="9a315-120">You can decide whether tooprovide a default value for hello Web Service Parameter.</span></span> <span data-ttu-id="9a315-121">다음 hello를 매개 변수는 hello 웹 서비스의 hello 사용자에 대 한 선택 사항.</span><span class="sxs-lookup"><span data-stu-id="9a315-121">If you do, then hello parameter is optional for hello user of hello web service.</span></span> <span data-ttu-id="9a315-122">기본값을 제공 하지 않으면, 다음 hello 사용자가 필요한 tooenter 값 hello 웹 서비스에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-122">If you don't provide a default value, then hello user is required tooenter a value when hello web service is accessed.</span></span>

<span data-ttu-id="9a315-123">hello hello 웹 서비스에 대 한 API 설명서에는 어떻게 toospecify hello 웹 서비스 매개 변수 프로그래밍 방식으로 hello 웹 서비스에 액세스할 때에 hello 웹 서비스 사용자에 대 한 정보가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-123">hello API documentation for hello web service includes information for hello web service user on how toospecify hello Web Service Parameter programmatically when accessing hello web service.</span></span>

> [!NOTE]
> <span data-ttu-id="9a315-124">클래식 웹 서비스는 hello를 통해 제공 됩니다에 대 한 API 설명서 hello **API 도움말 페이지** hello 웹 서비스에서 링크 **대시보드** 기계 학습 스튜디오에서.</span><span class="sxs-lookup"><span data-stu-id="9a315-124">hello API documentation for a classic web service is provided through hello **API help page** link in hello web service **DASHBOARD** in Machine Learning Studio.</span></span> <span data-ttu-id="9a315-125">새 웹 서비스는 hello를 통해 제공 됩니다에 대 한 API 설명서 hello [Azure 컴퓨터 학습 웹 서비스](https://services.azureml.net/Quickstart) hello에 포털 **사용** 및 **Swagger API** 페이지에 대 한 사용자 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-125">hello API documentation for a new web service is provided through hello [Azure Machine Learning Web Services](https://services.azureml.net/Quickstart) portal on hello **Consume** and **Swagger API** pages for your web service.</span></span>
> 
> 

## <a name="example"></a><span data-ttu-id="9a315-126">예제</span><span class="sxs-lookup"><span data-stu-id="9a315-126">Example</span></span>
<span data-ttu-id="9a315-127">예를 들어 있다고 가정해를 실험 한 [데이터 내보내기] [ writer] 정보 tooAzure blob 저장소에서 전송 하는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-127">As an example, let's assume we have an experiment with an [Export Data][writer] module that sends information tooAzure blob storage.</span></span> <span data-ttu-id="9a315-128">여기서 "Blob 경로" 라는 웹 서비스 매개 변수는 hello 서비스에 액세스할 때 hello 웹 서비스 사용자 toochange hello 경로 toohello blob 저장소 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-128">We'll define a Web Service Parameter named "Blob path" that allows hello web service user toochange hello path toohello blob storage when hello service is accessed.</span></span>

1. <span data-ttu-id="9a315-129">기계 학습 스튜디오에서 클릭 hello [데이터 내보내기] [ writer] 모듈 tooselect 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-129">In Machine Learning Studio, click hello [Export Data][writer] module tooselect it.</span></span> <span data-ttu-id="9a315-130">해당 속성이 hello 속성 창 toohello hello 실험 캔버스의 오른쪽에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-130">Its properties are shown in hello Properties pane toohello right of hello experiment canvas.</span></span>
2. <span data-ttu-id="9a315-131">Hello 저장소 유형을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-131">Specify hello storage type:</span></span>
   
   * <span data-ttu-id="9a315-132">**데이터 대상 지정**에서 "Azure Blob 저장소"를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-132">Under **Please specify data destination**, select "Azure Blob Storage".</span></span>
   * <span data-ttu-id="9a315-133">**인증 유형 지정**에서 "계정"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-133">Under **Please specify authentication type**, select "Account".</span></span>
   * <span data-ttu-id="9a315-134">Hello Azure blob 저장소에 대 한 hello 계정 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-134">Enter hello account information for hello Azure blob storage.</span></span> 
     <p /><span data-ttu-id="9a315-135">
3.Hello 아이콘 toohello hello의 오른쪽 클릭 **tooblob 컨테이너 매개 변수와 함께 시작 하는 경로**합니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-135">
3. Click hello icon toohello right of hello **Path tooblob beginning with container parameter**.</span></span> <span data-ttu-id="9a315-136">다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-136">It looks like this:</span></span>
   
   ![웹 서비스 매개 변수 아이콘][icon]
   
   <span data-ttu-id="9a315-138">"웹 서비스 매개 변수로 설정"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-138">Select "Set as web service parameter".</span></span>
   
   <span data-ttu-id="9a315-139">아래 항목에 추가 되 **웹 서비스 매개 변수가** hello hello 이름 "경로 tooblob 시작으로 컨테이너" hello 속성 창 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-139">An entry is added under **Web Service Parameters** at hello bottom of hello Properties pane with hello name "Path tooblob beginning with container".</span></span> <span data-ttu-id="9a315-140">이것은 웹 서비스 매개 변수는 이제를 hello와 연결 된 [데이터 내보내기] [ writer] : 모듈 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-140">This is hello Web Service Parameter that is now associated with this [Export Data][writer] module parameter.</span></span>
4. <span data-ttu-id="9a315-141">toorename 웹 서비스 매개 변수를 hello hello 이름, "Blob 경로"를 입력을 hello 키를 누릅니다 **Enter** 키입니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-141">toorename hello Web Service Parameter, click hello name, enter "Blob path", and press hello **Enter** key.</span></span> 
5. <span data-ttu-id="9a315-142">tooprovide hello 웹 서비스 매개 변수 기본값을 클릭 hello 아이콘 toohello hello 이름 오른쪽의 "기본값을 제공 합니다.", "(예:" container1/output1.csv), 값을 입력 하 고 선택한 hello 키를 누릅니다 **Enter** 키입니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-142">tooprovide a default value for hello Web Service Parameter, click hello icon toohello right of hello name, select "Provide default value", enter a value (for example, "container1/output1.csv"), and press hello **Enter** key.</span></span>
   
   ![웹 서비스 매개 변수][parameter]
6. <span data-ttu-id="9a315-144">**실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-144">Click **Run**.</span></span> 
7. <span data-ttu-id="9a315-145">클릭 **웹 서비스 배포** 선택 **웹 서비스 배포 [기본]** 또는 **웹 서비스 배포 [New]** toodeploy hello 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-145">Click **Deploy Web Service** and select **Deploy Web Service [Classic]** or **Deploy Web Service [New]** toodeploy hello web service.</span></span>

> [!NOTE] 
> <span data-ttu-id="9a315-146">toodeploy 충분 한 권한이의 해야 hello 구독 toowhich hello 웹 서비스를 배포 하면 새 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-146">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="9a315-147">자세한 내용은 참조 하십시오 [hello Azure 컴퓨터 학습 웹 서비스 포털을 사용 하 여 웹 서비스 관리](machine-learning-manage-new-webservice.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-147">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="9a315-148">hello 웹 서비스의 hello 사용자 hello에 대 한 새 대상을 지정할 수 [데이터 내보내기] [ writer] hello 웹 서비스에 액세스할 때 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-148">hello user of hello web service can now specify a new destination for hello [Export Data][writer] module when accessing hello web service.</span></span>

## <a name="more-information"></a><span data-ttu-id="9a315-149">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="9a315-149">More information</span></span>
<span data-ttu-id="9a315-150">더 자세한 예제를 보려면 hello [웹 서비스 매개 변수가](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) hello에 항목 [기계 학습 블로그](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-150">For a more detailed example, see hello [Web Service Parameters](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) entry in hello [Machine Learning Blog](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx).</span></span>

<span data-ttu-id="9a315-151">기계 학습 웹 서비스 액세스에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooconsume Azure 컴퓨터 학습 웹 서비스](machine-learning-consume-web-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9a315-151">For more information on accessing a Machine Learning web service, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

<!-- Images -->
[icon]: ./media/machine-learning-web-service-parameters/icon.png
[parameter]: ./media/machine-learning-web-service-parameters/parameter.png


<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[reader]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[writer]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/

