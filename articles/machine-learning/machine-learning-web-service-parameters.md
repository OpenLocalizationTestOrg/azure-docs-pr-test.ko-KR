---
title: "Azure Machine Learning 웹 서비스 매개 변수 사용 | Microsoft Docs"
description: "Azure 기계 학습 웹 서비스 매개 변수를 사용하여 웹 서비스에 액세스할 때 모델의 동작을 수정하는 방법입니다."
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
ms.openlocfilehash: 482726c1dae5385964e08b720e529817d5907537
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-machine-learning-web-service-parameters"></a><span data-ttu-id="d9e76-103">Azure 기계 학습 웹 서비스 매개 변수 사용</span><span class="sxs-lookup"><span data-stu-id="d9e76-103">Use Azure Machine Learning Web Service Parameters</span></span>
<span data-ttu-id="d9e76-104">Azure 기계 학습 웹 서비스는 구성 가능한 매개 변수로 모듈이 포함된 실험을 게시하여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-104">An Azure Machine Learning web service is created by publishing an experiment that contains modules with configurable parameters.</span></span> <span data-ttu-id="d9e76-105">경우에 따라 웹 서비스가 실행되는 동안 모듈 동작을 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-105">In some cases, you may want to change the module behavior while the web service is running.</span></span> <span data-ttu-id="d9e76-106">*웹 서비스 매개 변수*를 통해 이 태스크를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-106">*Web Service Parameters* allow you to do this task.</span></span> 

<span data-ttu-id="d9e76-107">일반적인 예는 게시된 웹 서비스의 사용자가 웹 서비스에 액세스할 때 다른 데이터 원본을 지정할 수 있도록 [데이터 가져오기][reader] 모듈을 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-107">A common example is setting up the [Import Data][reader] module so that the user of the published web service can specify a different data source when the web service is accessed.</span></span> <span data-ttu-id="d9e76-108">또는 다른 대상을 지정할 수 있도록 [데이터 내보내기][writer] 모듈을 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-108">Or configuring the [Export Data][writer] module so that a different destination can be specified.</span></span> <span data-ttu-id="d9e76-109">다른 예로는 [기능 해싱][feature-hashing] 모듈에 대한 비트 수 변경 또는 [필터 기반 기능 선택][filter-based-feature-selection] 모듈에 대한 원하는 기능 수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-109">Some other examples include changing the number of bits for the [Feature Hashing][feature-hashing] module or the number of desired features for the [Filter-Based Feature Selection][filter-based-feature-selection] module.</span></span> 

<span data-ttu-id="d9e76-110">실험에서 웹 서비스 매개 변수를 설정하여 하나 이상의 모듈 매개 변수와 연결하고 이러한 매개 변수가 필수인지 또는 선택 사항인지 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-110">You can set Web Service Parameters and associate them with one or more module parameters in your experiment, and you can specify whether they are required or optional.</span></span> <span data-ttu-id="d9e76-111">그러면 웹 서비스 사용자는 웹 서비스를 호출할 때 이러한 매개 변수에 대한 값을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-111">The user of the web service can then provide values for these parameters when they call the web service.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-to-set-and-use-web-service-parameters"></a><span data-ttu-id="d9e76-112">웹 서비스 매개 변수를 설정 및 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="d9e76-112">How to set and use Web Service Parameters</span></span>
<span data-ttu-id="d9e76-113">모듈 매개 변수 옆에 있는 아이콘을 클릭하고 "웹 서비스 매개 변수로 설정"을 선택하여 웹 서비스 매개 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-113">You define a Web Service Parameter by clicking the icon next to the parameter for a module and selecting "Set as web service parameter".</span></span> <span data-ttu-id="d9e76-114">새로운 웹 서비스 매개 변수가 만들어지고 해당 모듈 매개 변수에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-114">This creates a new Web Service Parameter and connects it to that module parameter.</span></span> <span data-ttu-id="d9e76-115">그런 다음 웹 서비스에 액세스할 때 사용자가 웹 서비스 매개 변수의 값을 지정할 수 있으며, 모듈 매개 변수에 값이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-115">Then, when the web service is accessed, the user can specify a value for the Web Service Parameter and it is applied to the module parameter.</span></span>

<span data-ttu-id="d9e76-116">웹 서비스 매개 변수를 정의하고 나면 실험의 다른 모든 모듈에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-116">Once you define a Web Service Parameter, it's available to any other module parameter in the experiment.</span></span> <span data-ttu-id="d9e76-117">한 모듈의 매개 변수와 연결된 웹 서비스 매개 변수를 정의하는 경우 매개 변수에 동일한 형식의 값이 예상되는 한 동일한 웹 서비스 매개 변수를 다른 모든 모듈에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-117">If you define a Web Service Parameter associated with a parameter for one module, you can use that same Web Service Parameter for any other module, as long as the parameter expects the same type of value.</span></span> <span data-ttu-id="d9e76-118">예를 들어 웹 서비스 매개 변수가 숫자 값인 경우 숫자 값이 필요한 모듈 매개 변수에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-118">For example, if the Web Service Parameter is a numeric value, then it can only be used for module parameters that expect a numeric value.</span></span> <span data-ttu-id="d9e76-119">사용자가 웹 서비스 매개 변수의 값을 설정하는 경우 연결된 모든 모듈 매개 변수에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-119">When the user sets a value for the Web Service Parameter, it will be applied to all associated module parameters.</span></span>

<span data-ttu-id="d9e76-120">웹 서비스 매개 변수에 대한 기본값을 제공할지 여부를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-120">You can decide whether to provide a default value for the Web Service Parameter.</span></span> <span data-ttu-id="d9e76-121">제공하는 경우 매개 변수는 웹 서비스 사용자에게 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-121">If you do, then the parameter is optional for the user of the web service.</span></span> <span data-ttu-id="d9e76-122">기본값을 제공하지 않는 경우 사용자가 웹 서비스에 액세스할 때 값을 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-122">If you don't provide a default value, then the user is required to enter a value when the web service is accessed.</span></span>

<span data-ttu-id="d9e76-123">웹 서비스에 대한 API 설명서에는 웹 서비스에 액세스할 때 프로그래밍 방식으로 웹 서비스 매개 변수를 지정하는 방법과 관련해서 웹 서비스 사용자를 위한 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-123">The API documentation for the web service includes information for the web service user on how to specify the Web Service Parameter programmatically when accessing the web service.</span></span>

> [!NOTE]
> <span data-ttu-id="d9e76-124">기존 웹 서비스에 대한 API 설명서는 Machine Learning 스튜디오에서 웹 서비스 **대시보드**의 **API 도움말 페이지** 링크를 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-124">The API documentation for a classic web service is provided through the **API help page** link in the web service **DASHBOARD** in Machine Learning Studio.</span></span> <span data-ttu-id="d9e76-125">새 웹 서비스에 대한 API 설명서는 웹 서비스에 대한 **사용** 및 **Swagger API** 페이지의 [Azure Machine Learning 웹 서비스](https://services.azureml.net/Quickstart) 포털을 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-125">The API documentation for a new web service is provided through the [Azure Machine Learning Web Services](https://services.azureml.net/Quickstart) portal on the **Consume** and **Swagger API** pages for your web service.</span></span>
> 
> 

## <a name="example"></a><span data-ttu-id="d9e76-126">예</span><span class="sxs-lookup"><span data-stu-id="d9e76-126">Example</span></span>
<span data-ttu-id="d9e76-127">예를 들어 Azure Blob Storage로 정보를 전송하는 [데이터 내보내기][writer] 모듈이 포함된 실험이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-127">As an example, let's assume we have an experiment with an [Export Data][writer] module that sends information to Azure blob storage.</span></span> <span data-ttu-id="d9e76-128">웹 서비스 사용자가 서비스에 액세스할 때 Blob 저장소 경로를 변경할 수 있게 해주는 "Blob 경로"라는 웹 서비스 매개 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-128">We'll define a Web Service Parameter named "Blob path" that allows the web service user to change the path to the blob storage when the service is accessed.</span></span>

1. <span data-ttu-id="d9e76-129">Machine Learning 스튜디오에서 [데이터 내보내기][writer] 모듈을 클릭하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-129">In Machine Learning Studio, click the [Export Data][writer] module to select it.</span></span> <span data-ttu-id="d9e76-130">실험 캔버스 오른쪽에 있는 속성 창에 해당 속성이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-130">Its properties are shown in the Properties pane to the right of the experiment canvas.</span></span>
2. <span data-ttu-id="d9e76-131">저장소 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-131">Specify the storage type:</span></span>
   
   * <span data-ttu-id="d9e76-132">**데이터 대상 지정**에서 "Azure Blob 저장소"를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-132">Under **Please specify data destination**, select "Azure Blob Storage".</span></span>
   * <span data-ttu-id="d9e76-133">**인증 유형 지정**에서 "계정"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-133">Under **Please specify authentication type**, select "Account".</span></span>
   * <span data-ttu-id="d9e76-134">Azure Blob 저장소에 대한 계정 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-134">Enter the account information for the Azure blob storage.</span></span> 
     <p /><span data-ttu-id="d9e76-135">
3. **컨테이너 매개 변수로 시작하는 blob에 대한 경로**의 오른쪽에 있는 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-135">
3. Click the icon to the right of the **Path to blob beginning with container parameter**.</span></span> <span data-ttu-id="d9e76-136">다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-136">It looks like this:</span></span>
   
   ![웹 서비스 매개 변수 아이콘][icon]
   
   <span data-ttu-id="d9e76-138">"웹 서비스 매개 변수로 설정"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-138">Select "Set as web service parameter".</span></span>
   
   <span data-ttu-id="d9e76-139">속성 창 맨 아래의 **웹 서비스 매개 변수** 에 "컨테이너로 시작하는 Blob 경로”라는 이름으로 항목이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-139">An entry is added under **Web Service Parameters** at the bottom of the Properties pane with the name "Path to blob beginning with container".</span></span> <span data-ttu-id="d9e76-140">이제 이 웹 서비스 매개 변수가 이 [데이터 내보내기][writer] 모듈 매개 변수와 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-140">This is the Web Service Parameter that is now associated with this [Export Data][writer] module parameter.</span></span>
4. <span data-ttu-id="d9e76-141">웹 서비스 매개 변수의 이름을 바꾸려면 이름을 클릭하고 "Blob 경로"를 입력한 다음 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-141">To rename the Web Service Parameter, click the name, enter "Blob path", and press the **Enter** key.</span></span> 
5. <span data-ttu-id="d9e76-142">웹 서비스 매개 변수에 대한 기본값을 제공하려면 이름 오른쪽에 있는 아이콘을 클릭하고 "기본값 제공"을 선택한 다음 값(예: "container1/output1.csv")을 입력하고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-142">To provide a default value for the Web Service Parameter, click the icon to the right of the name, select "Provide default value", enter a value (for example, "container1/output1.csv"), and press the **Enter** key.</span></span>
   
   ![웹 서비스 매개 변수][parameter]
6. <span data-ttu-id="d9e76-144">**실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-144">Click **Run**.</span></span> 
7. <span data-ttu-id="d9e76-145">**웹 서비스 배포**를 클릭하고 **웹 서비스 배포[클래식]** 또는 **웹 서비스 배포[신규]**를 선택하여 웹 서비스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-145">Click **Deploy Web Service** and select **Deploy Web Service [Classic]** or **Deploy Web Service [New]** to deploy the web service.</span></span>

> [!NOTE] 
> <span data-ttu-id="d9e76-146">새 웹 서비스를 배포하려면 웹 서비스를 배포하려는 구독에 충분한 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-146">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="d9e76-147">자세한 내용은 [Azure Machine Learning 웹 서비스 포털에서 웹 서비스 관리](machine-learning-manage-new-webservice.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9e76-147">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="d9e76-148">이제 웹 서비스 사용자가 웹 서비스에 액세스할 때 [데이터 내보내기][writer] 모듈에 대한 새 대상을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9e76-148">The user of the web service can now specify a new destination for the [Export Data][writer] module when accessing the web service.</span></span>

## <a name="more-information"></a><span data-ttu-id="d9e76-149">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="d9e76-149">More information</span></span>
<span data-ttu-id="d9e76-150">자세한 예제는 [Machine Learning 블로그](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx)의 [웹 서비스 매개 변수](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9e76-150">For a more detailed example, see the [Web Service Parameters](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) entry in the [Machine Learning Blog](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx).</span></span>

<span data-ttu-id="d9e76-151">Machine Learning 웹 서비스 액세스에 대한 자세한 내용은 [Azure Machine Learning 웹 서비스를 사용하는 방법](machine-learning-consume-web-services.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9e76-151">For more information on accessing a Machine Learning web service, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

<!-- Images -->
[icon]: ./media/machine-learning-web-service-parameters/icon.png
[parameter]: ./media/machine-learning-web-service-parameters/parameter.png


<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[reader]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[writer]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/

