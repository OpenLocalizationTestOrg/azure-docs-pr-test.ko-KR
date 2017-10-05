---
title: "Azure Machine Learning 웹 서비스: 배포 및 사용 | Microsoft Docs"
description: "웹 서비스 배포 및 사용을 위한 리소스입니다."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: 47635376-d1f4-4ea4-a6af-bd1f99f69a69
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 18edabe267ec06c08074d7a7a6d71435cedc8489
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a><span data-ttu-id="51ed1-103">Azure 기계 학습 웹 서비스: 배포 및 사용</span><span class="sxs-lookup"><span data-stu-id="51ed1-103">Azure Machine Learning Web Services: Deployment and consumption</span></span>
<span data-ttu-id="51ed1-104">Azure 기계 학습을 통해 웹 서비스로 기계 학습 워크플로 및 모델을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ed1-104">You can use Azure Machine Learning to deploy machine-learning workflows and models as web services.</span></span> <span data-ttu-id="51ed1-105">그런 다음 이러한 웹 서비스를 실시간으로 또는 배치 모드로 예측을 수행하도록 인터넷을 통해 응용 프로그램에서 기계 학습 모델을 호출하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ed1-105">These web services can then be used to call the machine-learning models from applications over the Internet to do predictions in real time or in batch mode.</span></span> <span data-ttu-id="51ed1-106">웹 서비스는 RESTFul이므로 .NET 및 Java와 같은 다양한 프로그래밍 언어 및 플랫폼과 Excel과 같은 응용 프로그램에서 호출될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ed1-106">Because the web services are RESTful, you can call them from various programming languages and platforms, such as .NET and Java, and from applications, such as Excel.</span></span>

<span data-ttu-id="51ed1-107">다음 섹션에서는 시작하는 데 도움이 되는 연습, 코드 및 설명서에 대한 링크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="51ed1-107">The next sections provide links to walkthroughs, code, and documentation to help get you started.</span></span>

## <a name="deploy-a-web-service"></a><span data-ttu-id="51ed1-108">웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="51ed1-108">Deploy a web service</span></span>
### <a name="with-azure-machine-learning-studio"></a><span data-ttu-id="51ed1-109">Azure 기계 학습 스튜디오 사용</span><span class="sxs-lookup"><span data-stu-id="51ed1-109">With Azure Machine Learning Studio</span></span>
<span data-ttu-id="51ed1-110">기계 학습 스튜디오 및 Microsoft Azure 기계 학습 웹 서비스 포털은 코드를 작성할 필요 없이 웹 서비스를 배포 및 관리하도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="51ed1-110">Machine Learning Studio and the Microsoft Azure Machine Learning Web Services portal help you deploy and manage a web service without writing code.</span></span>

<span data-ttu-id="51ed1-111">다음 링크는 새 웹 서비스를 배포하는 방법에 대한 일반 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="51ed1-111">The following links provide general Information about how to deploy a new web service:</span></span>

* <span data-ttu-id="51ed1-112">Azure Resource Manager를 기준으로 하는 새 웹 서비스를 배포하는 방법에 대한 개요는 [새 웹 서비스 배포](machine-learning-webservice-deploy-a-web-service.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51ed1-112">For an overview about how to deploy a new web service that's based on Azure Resource Manager, see [Deploy a new web service](machine-learning-webservice-deploy-a-web-service.md).</span></span>
* <span data-ttu-id="51ed1-113">웹 서비스를 배포하는 방법에 대한 연습은 [Azure 기계 학습 웹 서비스 배포](machine-learning-publish-a-machine-learning-web-service.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51ed1-113">For a walkthrough about how to deploy a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="51ed1-114">웹 서비스를 만들고 배포하는 방법에 대한 전체 연습은 [연습 1 단계: 기계 학습 작업 영역 만들기](machine-learning-walkthrough-1-create-ml-workspace.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51ed1-114">For a full walkthrough about how to create and deploy a web service, see [Walkthrough Step 1: Create a Machine Learning workspace](machine-learning-walkthrough-1-create-ml-workspace.md).</span></span>
* <span data-ttu-id="51ed1-115">웹 서비스 배포의 특정 예제는 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51ed1-115">For specific examples that deploy a web service, see:</span></span>

  * [<span data-ttu-id="51ed1-116">연습 5단계: Azure 기계 학습 웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="51ed1-116">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
  * [<span data-ttu-id="51ed1-117">여러 지역에 웹 서비스를 배포하는 방법</span><span class="sxs-lookup"><span data-stu-id="51ed1-117">How to deploy a web service to multiple regions</span></span>](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a><span data-ttu-id="51ed1-118">웹 서비스 리소스 공급자 API(Azure Resource Manager API) 사용</span><span class="sxs-lookup"><span data-stu-id="51ed1-118">With web services resource provider APIs (Azure Resource Manager APIs)</span></span>
<span data-ttu-id="51ed1-119">웹 서비스에 대한 Azure 기계 학습 리소스 공급자는 REST API 호출을 사용하여 웹 서비스의 배포 및 관리를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="51ed1-119">The Azure Machine Learning resource provider for web services enables deployment and management of web services by using REST API calls.</span></span> <span data-ttu-id="51ed1-120">자세한 내용은 MSDN의 [Machine Learning 웹 서비스(REST)](/rest/api/machinelearning/index) 참조를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51ed1-120">For additional details, see the [Machine Learning Web Service (REST)](/rest/api/machinelearning/index) reference.</span></span>

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a><span data-ttu-id="51ed1-121">PowerShell cmdlet 사용</span><span class="sxs-lookup"><span data-stu-id="51ed1-121">With PowerShell cmdlets</span></span>
<span data-ttu-id="51ed1-122">웹 서비스에 대한 Azure 기계 학습 리소스 공급자는 PowerShell cmdlet을 사용하여 웹 서비스의 배포 및 관리를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="51ed1-122">Azure Machine Learning resource provider for web services enables deployment and management of web services by using PowerShell cmdlets.</span></span>

<span data-ttu-id="51ed1-123">cmdlet을 사용하려면 먼저 [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet을 사용하여 PowerShell 환경 내에서 Azure 계정에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ed1-123">To use the cmdlets, you must first sign in to your Azure account from within the PowerShell environment by using the [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="51ed1-124">Resource Manager를 기준으로 하는 PowerShell 명령을 호출하는 방법에 익숙하지 않은 경우 [Azure Resource Manager로 Azure PowerShell 사용](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51ed1-124">If you are unfamiliar with how to call PowerShell commands that are based on Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span></span>

<span data-ttu-id="51ed1-125">예측 실험을 내보내려면 이 [샘플 코드](https://github.com/ritwik20/AzureML-WebServices)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="51ed1-125">To export your predictive experiment, use [this sample code](https://github.com/ritwik20/AzureML-WebServices).</span></span> <span data-ttu-id="51ed1-126">코드에서 .exe 파일을 만든 후 다음을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ed1-126">After you create the .exe file from the code, you can type:</span></span>

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

<span data-ttu-id="51ed1-127">응용 프로그램을 실행하면 웹 서비스 JSON 템플릿이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="51ed1-127">Running the application creates a web service JSON template.</span></span> <span data-ttu-id="51ed1-128">웹 서비스를 배포하는 데 템플릿을 사용하려면 다음 정보를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ed1-128">To use the template to deploy a web service, you must add the following information:</span></span>

* <span data-ttu-id="51ed1-129">저장소 계정 이름 및 키</span><span class="sxs-lookup"><span data-stu-id="51ed1-129">Storage account name and key</span></span>

    <span data-ttu-id="51ed1-130">[Azure Portal](https://portal.azure.com/) 또는 [Azure 클래식 포털](http://manage.windowsazure.com/)에서 저장소 계정 이름 및 키를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ed1-130">You can get the storage account name and key from either the [Azure portal](https://portal.azure.com/) or the [Azure classic portal](http://manage.windowsazure.com/).</span></span>
* <span data-ttu-id="51ed1-131">약정 계획 ID</span><span class="sxs-lookup"><span data-stu-id="51ed1-131">Commitment plan ID</span></span>

    <span data-ttu-id="51ed1-132">로그인하고 계획 이름을 클릭하여 [Azure 기계 학습 웹 서비스](https://services.azureml.net) 포털에서 계획 ID를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ed1-132">You can get the plan ID from the [Azure Machine Learning Web Services](https://services.azureml.net) portal by signing in and clicking a plan name.</span></span>

<span data-ttu-id="51ed1-133">*MachineLearningWorkspace* 노드와 동일한 수준에서 *Properties* 노드의 자식으로 JSON 템플릿에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="51ed1-133">Add them to the JSON template as children of the *Properties* node at the same level as the *MachineLearningWorkspace* node.</span></span>

<span data-ttu-id="51ed1-134">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="51ed1-134">Here's an example:</span></span>

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

<span data-ttu-id="51ed1-135">추가 세부 정보는 다음 문서 및 샘플 코드를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51ed1-135">See the following articles and sample code for additional details:</span></span>

* <span data-ttu-id="51ed1-136">[Azure 기계 학습 Cmdlet](https://msdn.microsoft.com/library/azure/mt767952.aspx) 참조</span><span class="sxs-lookup"><span data-stu-id="51ed1-136">[Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN</span></span>
* <span data-ttu-id="51ed1-137">GitHub의 샘플 [연습](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt)</span><span class="sxs-lookup"><span data-stu-id="51ed1-137">Sample [walkthrough](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) on GitHub</span></span>

## <a name="consume-the-web-services"></a><span data-ttu-id="51ed1-138">웹 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="51ed1-138">Consume the web services</span></span>
### <a name="from-the-azure-machine-learning-web-services-ui-testing"></a><span data-ttu-id="51ed1-139">Azure 기계 학습 웹 서비스 UI에서(테스트)</span><span class="sxs-lookup"><span data-stu-id="51ed1-139">From the Azure Machine Learning Web Services UI (Testing)</span></span>
<span data-ttu-id="51ed1-140">Azure 기계 학습 웹 서비스 포털에서 웹 서비스를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ed1-140">You can test your web service from the Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="51ed1-141">여기에는 RR(요청-응답 서비스) 및 BES(일괄 처리 실행 서비스) 인터페이스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="51ed1-141">This includes testing the Request-Response service (RRS) and Batch Execution service (BES) interfaces.</span></span>

* [<span data-ttu-id="51ed1-142">새 웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="51ed1-142">Deploy a new web service</span></span>](machine-learning-webservice-deploy-a-web-service.md)
* [<span data-ttu-id="51ed1-143">Azure 기계 학습 웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="51ed1-143">Deploy an Azure Machine Learning web service</span></span>](machine-learning-publish-a-machine-learning-web-service.md)
* [<span data-ttu-id="51ed1-144">연습 5단계: Azure 기계 학습 웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="51ed1-144">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a><span data-ttu-id="51ed1-145">엑셀에서</span><span class="sxs-lookup"><span data-stu-id="51ed1-145">From Excel</span></span>
<span data-ttu-id="51ed1-146">웹 서비스를 사용하는 Excel 템플릿을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ed1-146">You can download an Excel template that consumes the web service:</span></span>

* [<span data-ttu-id="51ed1-147">Excel에서 Azure 기계 학습 웹 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="51ed1-147">Consuming an Azure Machine Learning web service from Excel</span></span>](machine-learning-consuming-from-excel.md)
* [<span data-ttu-id="51ed1-148">Azure 기계 학습 웹 서비스용 Excel 추가 기능</span><span class="sxs-lookup"><span data-stu-id="51ed1-148">Excel add-in for Azure Machine Learning Web Services</span></span>](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a><span data-ttu-id="51ed1-149">REST 기반 클라이언트에서</span><span class="sxs-lookup"><span data-stu-id="51ed1-149">From a REST-based client</span></span>
<span data-ttu-id="51ed1-150">Azure 기계 학습 웹 서비스는 RESTful API입니다.</span><span class="sxs-lookup"><span data-stu-id="51ed1-150">Azure Machine Learning Web Services are RESTful APIs.</span></span> <span data-ttu-id="51ed1-151">.NET, Python, R, Java 등과 같은 다양한 플랫폼에서 이러한 API를 사용할 수 있습니다. [Microsoft Azure Machine Learning 웹 서비스 포털](https://services.azureml.net)의 웹 서비스에 대한 **사용** 페이지에는 시작하는 데 도움을 줄 수 있는 샘플 코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ed1-151">You can consume these APIs from various platforms, such as .NET, Python, R, Java, etc. The **Consume** page for your web service on the [Microsoft Azure Machine Learning Web Services portal](https://services.azureml.net) has sample code that can help you get started.</span></span> <span data-ttu-id="51ed1-152">자세한 내용은 [Azure Machine Learning 웹 서비스 사용 방법](machine-learning-consume-web-services.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51ed1-152">For more information, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>
