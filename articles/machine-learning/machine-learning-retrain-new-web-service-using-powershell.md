---
title: "PowerShell을 사용하여 새 Azure Machine Learning 웹 서비스 다시 학습 | Microsoft Docs"
description: "Machine Learning Management PowerShell cmdlet를 사용하여 Azure Machine Learning에서 프로그래밍 방식으로 모델을 다시 학습하고 새로 학습된 모델을 사용하도록 웹 서비스를 업데이트하는 방법을 알아봅니다."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3953a398-6174-4d2d-8bbd-e55cf1639415
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 804dd59e62f38ee1878045d93211ee18e0d5bfce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="retrain-a-new-resource-manager-based-web-service-using-the-machine-learning-management-powershell-cmdlets"></a><span data-ttu-id="7f9ec-103">Machine Learning 관리 PowerShell cmdlet을 사용하여 새 리소스 관리자 기반 웹 서비스를 다시 학습</span><span class="sxs-lookup"><span data-stu-id="7f9ec-103">Retrain a New Resource Manager based web service using the Machine Learning Management PowerShell cmdlets</span></span>
<span data-ttu-id="7f9ec-104">새 웹 서비스를 다시 교육하는 경우 새로 학습된 모델을 참조하여 예측 웹 서비스 정의를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-104">When you retrain a New web service, you update the predictive web service definition to reference the new trained model.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="7f9ec-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7f9ec-105">Prerequisites</span></span>
<span data-ttu-id="7f9ec-106">학습 실험 및 예측 실험을 [프로그래밍 방식으로 Machine Learning 모델 재학습](machine-learning-retrain-models-programmatically.md)에서 보듯이 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-106">You must set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="7f9ec-107">예측 실험을 Azure Resource Manager(신규) 기반 Machine Learning 웹 서비스로 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-107">The predictive experiment must be deployed as an Azure Resource Manager (New) based machine learning web service.</span></span> <span data-ttu-id="7f9ec-108">새 웹 서비스를 배포하려면 웹 서비스를 배포하려는 구독에 충분한 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-108">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="7f9ec-109">자세한 내용은 [Azure Machine Learning 웹 서비스 포털에서 웹 서비스 관리](machine-learning-manage-new-webservice.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-109">For more information, see [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="7f9ec-110">웹 서비스 배포에 대한 자세한 내용은 [Azure Machine Learning 웹 서비스 배포](machine-learning-publish-a-machine-learning-web-service.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="7f9ec-111">이 프로세스는 Azure Machine Learning Cmdlets 설치가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-111">This process requires that you have installed the Azure Machine Learning Cmdlets.</span></span> <span data-ttu-id="7f9ec-112">Machine Learning cmdlet 설치에 관한 정보는 MSDN의 [Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) 참조를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-112">For information installing the Machine Learning cmdlets, see the [Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN.</span></span>

<span data-ttu-id="7f9ec-113">다음 정보를 재학습 출력에서 복사했습니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-113">Copied the following information from the retraining output:</span></span>

* <span data-ttu-id="7f9ec-114">BaseLocation</span><span class="sxs-lookup"><span data-stu-id="7f9ec-114">BaseLocation</span></span>
* <span data-ttu-id="7f9ec-115">RelativeLocation</span><span class="sxs-lookup"><span data-stu-id="7f9ec-115">RelativeLocation</span></span>

<span data-ttu-id="7f9ec-116">수행할 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-116">The steps you take are:</span></span>

1. <span data-ttu-id="7f9ec-117">Azure Resource Manager 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-117">Sign in to your Azure Resource Manager account.</span></span>
2. <span data-ttu-id="7f9ec-118">웹 서비스 정의 가져오기</span><span class="sxs-lookup"><span data-stu-id="7f9ec-118">Get the web service definition</span></span>
3. <span data-ttu-id="7f9ec-119">JSON으로 웹 서비스 정의 내보내기</span><span class="sxs-lookup"><span data-stu-id="7f9ec-119">Export the Web Service Definition as JSON</span></span>
4. <span data-ttu-id="7f9ec-120">JSON에서 ilearner blob에 대한 참조를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-120">Update the reference to the ilearner blob in the JSON.</span></span>
5. <span data-ttu-id="7f9ec-121">JSON을 웹 서비스 정의로 가져오기</span><span class="sxs-lookup"><span data-stu-id="7f9ec-121">Import the JSON into a Web Service Definition</span></span>
6. <span data-ttu-id="7f9ec-122">웹 서비스를 새 웹 서비스 정의로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-122">Update the web service with new Web Service Definition</span></span>

## <a name="sign-in-to-your-azure-resource-manager-account"></a><span data-ttu-id="7f9ec-123">Azure Resource Manager 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-123">Sign in to your Azure Resource Manager account</span></span>
<span data-ttu-id="7f9ec-124">먼저 [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet을 사용하여 PowerShell 환경 내에서 Azure 계정에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-124">You must first sign in to your Azure account from within the PowerShell environment using the [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-the-web-service-definition"></a><span data-ttu-id="7f9ec-125">웹 서비스 정의 가져오기</span><span class="sxs-lookup"><span data-stu-id="7f9ec-125">Get the Web Service Definition</span></span>
<span data-ttu-id="7f9ec-126">다음으로 [Get AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet을 호출하여 웹 서비스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-126">Next, get the Web Service by calling the [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="7f9ec-127">웹 서비스 정의는 웹 서비스 학습된 모델의 내부 표현이며 직접 수정할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-127">The Web Service Definition is an internal representation of the trained model of the web service and is not directly modifiable.</span></span> <span data-ttu-id="7f9ec-128">학습 실험이 아닌 예측 실험에 대한 웹 서비스 정의를 검색하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-128">Make sure that you are retrieving the Web Service Definition for your Predictive experiment and not your training experiment.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="7f9ec-129">기존 웹 서비스의 리소스 그룹 이름을 결정하려면 구독 중인 웹 서비스를 표시하도록 매개 변수 없이 Get-AzureRmMlWebService cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-129">To determine the resource group name of an existing web service, run the Get-AzureRmMlWebService cmdlet without any parameters to display the web services in your subscription.</span></span> <span data-ttu-id="7f9ec-130">웹 서비스를 찾은 다음 웹 서비스 ID를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-130">Locate the web service, and then look at its web service ID.</span></span> <span data-ttu-id="7f9ec-131">리소스 그룹 이름은 ID의 네 번째 요소로 *resourceGroups* 요소 바로 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-131">The name of the resource group is the fourth element in the ID, just after the *resourceGroups* element.</span></span> <span data-ttu-id="7f9ec-132">다음 예제에서 리소스 그룹 이름은 Default-MachineLearning-SouthCentralUS입니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-132">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="7f9ec-133">또는 기존 웹 서비스의 리소스 그룹 이름을 결정하려면 Microsoft Azure Machine Learning Web Services 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-133">Alternatively, to determine the resource group name of an existing web service, log on to the Microsoft Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="7f9ec-134">웹 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-134">Select the web service.</span></span> <span data-ttu-id="7f9ec-135">리소스 그룹 이름은 웹 서비스 URL의 다섯 번째 요소로 *resourceGroups* 요소 바로 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-135">The resource group name is the fifth element of the URL of the web service, just after the *resourceGroups* element.</span></span> <span data-ttu-id="7f9ec-136">다음 예제에서 리소스 그룹 이름은 Default-MachineLearning-SouthCentralUS입니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-136">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-the-web-service-definition-as-json"></a><span data-ttu-id="7f9ec-137">JSON으로 웹 서비스 정의 내보내기</span><span class="sxs-lookup"><span data-stu-id="7f9ec-137">Export the Web Service Definition as JSON</span></span>
<span data-ttu-id="7f9ec-138">새로 Trained Model을 사용하여 새로 학습된 모델에 대한 정의를 수정하려면 먼저 [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet을 사용하여 JSON 형식 파일에 내보내기해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-138">To modify the definition to the trained model to use the newly Trained Model, you must first use the [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet to export it to a JSON format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-the-reference-to-the-ilearner-blob-in-the-json"></a><span data-ttu-id="7f9ec-139">JSON에서 ilearner blob에 대한 참조를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-139">Update the reference to the ilearner blob in the JSON.</span></span>
<span data-ttu-id="7f9ec-140">자산에서 [학습된 모델]을 찾아, ilearner Blob의 URI와 함께 *locationInfo* 노드의 *uri* 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-140">In the assets, locate the [trained model], update the *uri* value in the *locationInfo* node with the URI of the ilearner blob.</span></span> <span data-ttu-id="7f9ec-141">URI는 BES 재학습 호출의 출력에서 *BaseLocation* 및 *RelativeLocation*을 조합하여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-141">The URI is generated by combining the *BaseLocation* and the *RelativeLocation* from the output of the BES retraining call.</span></span> <span data-ttu-id="7f9ec-142">이렇게 새로 학습된 모델을 참조하는 경로를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-142">This updates the path to reference the new trained model.</span></span>

     "asset3": {
        "name": "Retrain Samp.le [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-the-json-into-a-web-service-definition"></a><span data-ttu-id="7f9ec-143">JSON을 웹 서비스 정의로 가져오기</span><span class="sxs-lookup"><span data-stu-id="7f9ec-143">Import the JSON into a Web Service Definition</span></span>
<span data-ttu-id="7f9ec-144">수정된 JSON 파일을 웹 서비스 정의를 업데이트하는 데 사용할 수 있는 웹 서비스 정의로 변환하려면 [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-144">You must use the [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet to convert the modified JSON file back into a Web Service Definition that you can use to update the Web Service Definition.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-the-web-service-with-new-web-service-definition"></a><span data-ttu-id="7f9ec-145">웹 서비스를 새 웹 서비스 정의로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-145">Update the web service with new Web Service Definition</span></span>
<span data-ttu-id="7f9ec-146">마지막으로, [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet를 사용하여 웹 서비스 정의를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-146">Finally, you use [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet to update the Web Service Definition.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'  -ServiceUpdates $wsd

## <a name="summary"></a><span data-ttu-id="7f9ec-147">요약</span><span class="sxs-lookup"><span data-stu-id="7f9ec-147">Summary</span></span>
<span data-ttu-id="7f9ec-148">Machine Learning PowerShell Management cmdlet을 사용하여 다음과 같은 시나리오를 활성화하는 예측 웹 서비스의 학습된 모델을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-148">Using the Machine Learning PowerShell management cmdlets, you can update the trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="7f9ec-149">새 데이터를 사용하는 주기적 모델 재학습.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-149">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="7f9ec-150">자신의 데이터를 사용하여 모델을 다시 학습할 수 있도록 하는 것을 목표로 고객에게 모델 배포.</span><span class="sxs-lookup"><span data-stu-id="7f9ec-150">Distribution of a model to customers with the goal of letting them retrain the model using their own data.</span></span>

