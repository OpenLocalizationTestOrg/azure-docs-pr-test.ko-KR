---
title: "PowerShell과 함께 새 Azure 기계 학습 웹 서비스 aaaRetrain | Microsoft Docs"
description: "Tooprogrammatically 모델과 hello 웹 서비스 toouse hello 새로 학습 된 모델 업데이트 hello 컴퓨터 학습 관리 PowerShell cmdlet을 사용 하 여 Azure 기계 학습에서를 재 연습 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 5b77fa82cfe17f0b4e90007ef81c506ab712475b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-new-resource-manager-based-web-service-using-hello-machine-learning-management-powershell-cmdlets"></a><span data-ttu-id="41b7e-103">Hello 컴퓨터 학습 관리 PowerShell cmdlet을 사용 하 여 새 리소스 관리자 기반 웹 서비스를 다시 학습</span><span class="sxs-lookup"><span data-stu-id="41b7e-103">Retrain a New Resource Manager based web service using hello Machine Learning Management PowerShell cmdlets</span></span>
<span data-ttu-id="41b7e-104">새 웹 서비스를 다시 학습 hello 예측 웹 서비스 정의 tooreference hello 새 학습 된 모델을 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41b7e-104">When you retrain a New web service, you update hello predictive web service definition tooreference hello new trained model.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="41b7e-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="41b7e-105">Prerequisites</span></span>
<span data-ttu-id="41b7e-106">학습 실험 및 예측 실험을 [프로그래밍 방식으로 Machine Learning 모델 재학습](machine-learning-retrain-models-programmatically.md)에서 보듯이 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b7e-106">You must set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="41b7e-107">hello 예측 실험으로는 Azure 리소스 관리자 (새) 기반으로 기계 학습 웹 서비스 배포 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b7e-107">hello predictive experiment must be deployed as an Azure Resource Manager (New) based machine learning web service.</span></span> <span data-ttu-id="41b7e-108">toodeploy 충분 한 권한이의 해야 hello 구독 toowhich hello 웹 서비스를 배포 하면 새 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="41b7e-108">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="41b7e-109">자세한 내용은 참조 [hello Azure 컴퓨터 학습 웹 서비스 포털을 사용 하 여 웹 서비스 관리](machine-learning-manage-new-webservice.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="41b7e-109">For more information, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="41b7e-110">웹 서비스 배포에 대한 자세한 내용은 [Azure Machine Learning 웹 서비스 배포](machine-learning-publish-a-machine-learning-web-service.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41b7e-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="41b7e-111">이 프로세스는 hello Azure 컴퓨터 학습 Cmdlet을 설치 했는지 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b7e-111">This process requires that you have installed hello Azure Machine Learning Cmdlets.</span></span> <span data-ttu-id="41b7e-112">Hello 기계 학습 cmdlet을 설치 하는 정보에 대 한 참조 hello [Azure 컴퓨터 학습 Cmdlet](https://msdn.microsoft.com/library/azure/mt767952.aspx) msdn 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b7e-112">For information installing hello Machine Learning cmdlets, see hello [Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN.</span></span>

<span data-ttu-id="41b7e-113">복사 된 hello 출력 재교육 hello에서 다음 정보:</span><span class="sxs-lookup"><span data-stu-id="41b7e-113">Copied hello following information from hello retraining output:</span></span>

* <span data-ttu-id="41b7e-114">BaseLocation</span><span class="sxs-lookup"><span data-stu-id="41b7e-114">BaseLocation</span></span>
* <span data-ttu-id="41b7e-115">RelativeLocation</span><span class="sxs-lookup"><span data-stu-id="41b7e-115">RelativeLocation</span></span>

<span data-ttu-id="41b7e-116">hello 단계를 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41b7e-116">hello steps you take are:</span></span>

1. <span data-ttu-id="41b7e-117">Tooyour Azure 리소스 관리자 계정에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b7e-117">Sign in tooyour Azure Resource Manager account.</span></span>
2. <span data-ttu-id="41b7e-118">Hello 웹 서비스 정의 가져오기</span><span class="sxs-lookup"><span data-stu-id="41b7e-118">Get hello web service definition</span></span>
3. <span data-ttu-id="41b7e-119">JSON으로 hello 웹 서비스 정의 내보내기</span><span class="sxs-lookup"><span data-stu-id="41b7e-119">Export hello Web Service Definition as JSON</span></span>
4. <span data-ttu-id="41b7e-120">Hello JSON hello 참조 toohello ilearner blob를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b7e-120">Update hello reference toohello ilearner blob in hello JSON.</span></span>
5. <span data-ttu-id="41b7e-121">웹 서비스 정의 hello JSON 가져오기</span><span class="sxs-lookup"><span data-stu-id="41b7e-121">Import hello JSON into a Web Service Definition</span></span>
6. <span data-ttu-id="41b7e-122">새 웹 서비스 정의 된 hello 웹 서비스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b7e-122">Update hello web service with new Web Service Definition</span></span>

## <a name="sign-in-tooyour-azure-resource-manager-account"></a><span data-ttu-id="41b7e-123">Tooyour Azure 리소스 관리자 계정에 로그인</span><span class="sxs-lookup"><span data-stu-id="41b7e-123">Sign in tooyour Azure Resource Manager account</span></span>
<span data-ttu-id="41b7e-124">먼저 tooyour hello를 사용 하 여 hello PowerShell 환경 내에서 Azure 계정에에서 로그인 해야 [추가 AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="41b7e-124">You must first sign in tooyour Azure account from within hello PowerShell environment using hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-hello-web-service-definition"></a><span data-ttu-id="41b7e-125">Hello 웹 서비스 정의 가져오기</span><span class="sxs-lookup"><span data-stu-id="41b7e-125">Get hello Web Service Definition</span></span>
<span data-ttu-id="41b7e-126">다음으로 hello 호출 하 여 hello 웹 서비스를 가져올 [Get AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="41b7e-126">Next, get hello Web Service by calling hello [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="41b7e-127">hello 웹 서비스 정의 hello 웹 서비스의 hello 학습 된 모델의 내부 표현 되며 직접 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="41b7e-127">hello Web Service Definition is an internal representation of hello trained model of hello web service and is not directly modifiable.</span></span> <span data-ttu-id="41b7e-128">예측 실험 및 하지 학습 실험에 대 한 웹 서비스 정의 hello 검색 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b7e-128">Make sure that you are retrieving hello Web Service Definition for your Predictive experiment and not your training experiment.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="41b7e-129">toodetermine hello 리소스 그룹의 이름 구독에서 모든 매개 변수 toodisplay hello 웹 서비스 없이 hello AzureRmMlWebService Get cmdlet을 실행 하는 기존 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="41b7e-129">toodetermine hello resource group name of an existing web service, run hello Get-AzureRmMlWebService cmdlet without any parameters toodisplay hello web services in your subscription.</span></span> <span data-ttu-id="41b7e-130">Hello 웹 서비스를 찾은 다음 웹 서비스 ID 확인</span><span class="sxs-lookup"><span data-stu-id="41b7e-130">Locate hello web service, and then look at its web service ID.</span></span> <span data-ttu-id="41b7e-131">hello hello 리소스 그룹 이름은 hello ID의 네 번째 요소 hello hello 직후 *resourceGroups* 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="41b7e-131">hello name of hello resource group is hello fourth element in hello ID, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="41b7e-132">다음 예제는 hello, hello 리소스 그룹 이름은 기본-MachineLearning-SouthCentralUS를입니다.</span><span class="sxs-lookup"><span data-stu-id="41b7e-132">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="41b7e-133">또는 toodetermine hello 리소스의 그룹 이름 기존 웹 서비스, toohello Microsoft Azure 컴퓨터 학습 웹 서비스 포털에 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b7e-133">Alternatively, toodetermine hello resource group name of an existing web service, log on toohello Microsoft Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="41b7e-134">Hello 웹 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b7e-134">Select hello web service.</span></span> <span data-ttu-id="41b7e-135">hello 리소스 그룹 이름은 hello 직후 hello 웹 서비스의 hello URL의 다섯 번째 요소 hello *resourceGroups* 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="41b7e-135">hello resource group name is hello fifth element of hello URL of hello web service, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="41b7e-136">다음 예제는 hello, hello 리소스 그룹 이름은 기본-MachineLearning-SouthCentralUS를입니다.</span><span class="sxs-lookup"><span data-stu-id="41b7e-136">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-as-json"></a><span data-ttu-id="41b7e-137">JSON으로 hello 웹 서비스 정의 내보내기</span><span class="sxs-lookup"><span data-stu-id="41b7e-137">Export hello Web Service Definition as JSON</span></span>
<span data-ttu-id="41b7e-138">toomodify hello 정의 toohello 학습 된 모델 toouse hello 새로 학습 된 모델, hello를 먼저 사용 해야 [내보내기 AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport 것 tooa JSON 형식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="41b7e-138">toomodify hello definition toohello trained model toouse hello newly Trained Model, you must first use hello [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport it tooa JSON format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob-in-hello-json"></a><span data-ttu-id="41b7e-139">Hello JSON hello 참조 toohello ilearner blob를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b7e-139">Update hello reference toohello ilearner blob in hello JSON.</span></span>
<span data-ttu-id="41b7e-140">Hello 자산에서 hello [학습 된 모델], 업데이트 hello 찾습니다 *uri* hello 값 *locationInfo* hello hello ilearner blob의 URI로 노드.</span><span class="sxs-lookup"><span data-stu-id="41b7e-140">In hello assets, locate hello [trained model], update hello *uri* value in hello *locationInfo* node with hello URI of hello ilearner blob.</span></span> <span data-ttu-id="41b7e-141">hello URI는 결합 하 여 생성 hello *BaseLocation* 및 hello *RelativeLocation* hello BES 재교육 호출의 hello 출력에서.</span><span class="sxs-lookup"><span data-stu-id="41b7e-141">hello URI is generated by combining hello *BaseLocation* and hello *RelativeLocation* from hello output of hello BES retraining call.</span></span> <span data-ttu-id="41b7e-142">Hello 경로 tooreference hello 새 학습 된 모델을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b7e-142">This updates hello path tooreference hello new trained model.</span></span>

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

## <a name="import-hello-json-into-a-web-service-definition"></a><span data-ttu-id="41b7e-143">웹 서비스 정의 hello JSON 가져오기</span><span class="sxs-lookup"><span data-stu-id="41b7e-143">Import hello JSON into a Web Service Definition</span></span>
<span data-ttu-id="41b7e-144">Hello를 사용 해야 [가져오기 AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello tooupdate hello 웹 서비스 정의 사용할 수 있는 웹 서비스 정의로 다시 JSON 파일을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b7e-144">You must use hello [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello modified JSON file back into a Web Service Definition that you can use tooupdate hello Web Service Definition.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service-with-new-web-service-definition"></a><span data-ttu-id="41b7e-145">새 웹 서비스 정의 된 hello 웹 서비스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b7e-145">Update hello web service with new Web Service Definition</span></span>
<span data-ttu-id="41b7e-146">사용 하는 마지막으로, [업데이트 AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello 웹 서비스 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b7e-146">Finally, you use [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello Web Service Definition.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'  -ServiceUpdates $wsd

## <a name="summary"></a><span data-ttu-id="41b7e-147">요약</span><span class="sxs-lookup"><span data-stu-id="41b7e-147">Summary</span></span>
<span data-ttu-id="41b7e-148">Hello 컴퓨터 학습 PowerShell 관리 cmdlet을 사용 하 여 예측 웹 서비스 같은 시나리오를 지원의 hello 학습 된 모델을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41b7e-148">Using hello Machine Learning PowerShell management cmdlets, you can update hello trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="41b7e-149">새 데이터를 사용하는 주기적 모델 재학습.</span><span class="sxs-lookup"><span data-stu-id="41b7e-149">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="41b7e-150">자신의 데이터를 사용 하 여 hello 모델을 보존 하기 위해 이러한의 hello 목표 모델 toocustomers의 분포를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b7e-150">Distribution of a model toocustomers with hello goal of letting them retrain hello model using their own data.</span></span>

