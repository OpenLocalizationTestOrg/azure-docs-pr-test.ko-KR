---
title: "기존 예측 웹 서비스 재학습 | Microsoft Docs"
description: "Azure Machine Learning에서 모델을 다시 학습하고 새로 학습된 모델을 사용하도록 웹 서비스를 업데이트하는 방법을 알아봅니다."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: cc4c26a2-5672-4255-a767-cfd971e46775
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: v-donglo
ms.openlocfilehash: bdc994daf441d397157f8e6cbcf84d72584927f0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="retrain-an-existing-predictive-web-service"></a><span data-ttu-id="81137-103">기존 예측 웹 서비스 재학습</span><span class="sxs-lookup"><span data-stu-id="81137-103">Retrain an existing predictive web service</span></span>
<span data-ttu-id="81137-104">이 문서에서는 다음 시나리오에 대한 재학습 프로세스를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-104">This document describes the retraining process for the following scenario:</span></span>

* <span data-ttu-id="81137-105">조작 가능한 웹 서비스로 배포한 학습 실험 및 예측 실험이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81137-105">You have a training experiment and a predictive experiment that you have deployed as an operationalized web service.</span></span>
* <span data-ttu-id="81137-106">예측 웹 서비스가 점수 매기기를 수행하도록 하기 위해 사용할 새 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81137-106">You have new data that you want your predictive web service to use to perform its scoring.</span></span>

> [!NOTE] 
> <span data-ttu-id="81137-107">새 웹 서비스를 배포하려면 웹 서비스를 배포하려는 구독에 충분한 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-107">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="81137-108">자세한 내용은 [Azure Machine Learning 웹 서비스 포털에서 웹 서비스 관리](machine-learning-manage-new-webservice.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81137-108">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="81137-109">기존 웹 서비스 및 실험을 시작으로 다음 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-109">Starting with your existing web service and experiments, you need to follow these steps:</span></span>

1. <span data-ttu-id="81137-110">모델을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-110">Update the model.</span></span>
   1. <span data-ttu-id="81137-111">웹 서비스 입력 및 출력을 감안하도록 학습 실험을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-111">Modify your training experiment to allow for web service inputs and outputs.</span></span>
   2. <span data-ttu-id="81137-112">학습 실험을 재학습 웹 서비스로 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-112">Deploy the training experiment as a retraining web service.</span></span>
   3. <span data-ttu-id="81137-113">학습 실험의 BES(일괄 처리 실행 서비스)를 사용하여 모델을 다시 학습합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-113">Use the training experiment's Batch Execution Service (BES) to retrain the model.</span></span>
2. <span data-ttu-id="81137-114">Azure Machine Learning PowerShell cmdlet을 사용하여 예측 실험을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-114">Use the Azure Machine Learning PowerShell cmdlets to update the predictive experiment.</span></span>
   1. <span data-ttu-id="81137-115">Azure Resource Manager 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-115">Sign in to your Azure Resource Manager account.</span></span>
   2. <span data-ttu-id="81137-116">웹 서비스 정의를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="81137-116">Get the web service definition.</span></span>
   3. <span data-ttu-id="81137-117">JSON으로 웹 서비스 정의를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="81137-117">Export the web service definition as JSON.</span></span>
   4. <span data-ttu-id="81137-118">JSON에서 ilearner blob에 대한 참조를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-118">Update the reference to the ilearner blob in the JSON.</span></span>
   5. <span data-ttu-id="81137-119">JSON을 웹 서비스 정의로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="81137-119">Import the JSON into a web service definition.</span></span>
   6. <span data-ttu-id="81137-120">새 웹 서비스 정의를 사용해 웹 서비스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-120">Update the web service with a new web service definition.</span></span>

## <a name="deploy-the-training-experiment"></a><span data-ttu-id="81137-121">학습 실험 배포</span><span class="sxs-lookup"><span data-stu-id="81137-121">Deploy the training experiment</span></span>
<span data-ttu-id="81137-122">학습 실험을 재학습 웹 서비스로 배포하려면 웹 서비스 입력 및 출력을 모델에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-122">To deploy the training experiment as a retraining web service, you must add web service inputs and outputs to the model.</span></span> <span data-ttu-id="81137-123">*웹 서비스 출력* 모듈을 실험의 *[모델 학습][train-model]* 모듈에 연결하여 학습 실험이 예측 실험에 사용할 수 있는 학습된 모델을 새로 생성하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81137-123">By connecting a *Web Service Output* module to the experiment's *[Train Model][train-model]* module, you enable the training experiment to produce a new trained model that you can use in your predictive experiment.</span></span> <span data-ttu-id="81137-124">*모델 평가* 모듈이 있다면 또한 웹 서비스 출력을 연결하여 평가 결과를 출력으로 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81137-124">If you have an *Evaluate Model* module, you can also attach web service output to get the evaluation results as output.</span></span>

<span data-ttu-id="81137-125">학습 실험을 업데이트하려면:</span><span class="sxs-lookup"><span data-stu-id="81137-125">To update your training experiment:</span></span>

1. <span data-ttu-id="81137-126">*웹 서비스 입력* 모듈을 데이터 입력(예를 들어 *누락 데이터 정리* 모듈)에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-126">Connect a *Web Service Input* module to your data input (for example, a *Clean Missing Data* module).</span></span> <span data-ttu-id="81137-127">일반적으로 이 입력 데이터가 원래 학습 데이터와 동일한 방식으로 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-127">Typically, you want to ensure that your input data is processed in the same way as your original training data.</span></span>
2. <span data-ttu-id="81137-128">*웹 서비스 출력* 모듈을 *모델 학습* 모듈의 출력에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-128">Connect a *Web Service Output* module to the output of your *Train Model* module.</span></span>
3. <span data-ttu-id="81137-129">*모델 평가* 모듈이 있고 평가 결과를 출력하고자 할 경우, *웹 서비스 출력* 모듈을 *모델 평가* 모듈의 출력에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-129">If you have an *Evaluate Model* module and you want to output the evaluation results, connect a *Web Service Output* module to the output of your *Evaluate Model* module.</span></span>

<span data-ttu-id="81137-130">실험을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-130">Run your experiment.</span></span>

<span data-ttu-id="81137-131">다음으로 학습 실험을 학습된 모델 및 모델 평가 결과를 생성하는 웹 서비스로 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-131">Next, you must deploy the training experiment as a web service that produces a trained model and model evaluation results.</span></span>  

<span data-ttu-id="81137-132">실험 캔버스 맨 아래에서 **웹 서비스 설정**을 클릭한 다음 **웹 서비스[New] 배포**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-132">At the bottom of the experiment canvas, click **Set Up Web Service**, and then select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="81137-133">Azure Machine Learning Web Services 포털은 **웹 서비스 배포** 페이지에 열립니다.</span><span class="sxs-lookup"><span data-stu-id="81137-133">The Azure Machine Learning Web Services portal opens to the **Deploy Web Service** page.</span></span> <span data-ttu-id="81137-134">웹 서비스의 이름을 입력하고 결제 방식을 선택한 다음 **배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-134">Type a name for your web service, choose a payment plan, and then click **Deploy**.</span></span> <span data-ttu-id="81137-135">학습된 모델을 만들 때는 배치 실행 방법만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81137-135">You can only use the Batch Execution method for creating trained models.</span></span>

## <a name="retrain-the-model-with-new-data-by-using-bes"></a><span data-ttu-id="81137-136">BES를 사용하여 새 데이터로 모델 다시 학습</span><span class="sxs-lookup"><span data-stu-id="81137-136">Retrain the model with new data by using BES</span></span>
<span data-ttu-id="81137-137">이 예에서는 재학습 응용 프로그램을 만드는 데 C#을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-137">For this example, we're using C# to create the retraining application.</span></span> <span data-ttu-id="81137-138">또한 Python 또는 R 샘플 코드를 사용하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81137-138">You can also use Python or R sample code to accomplish this task.</span></span>

<span data-ttu-id="81137-139">재학습 API를 호출하려면:</span><span class="sxs-lookup"><span data-stu-id="81137-139">To call the retraining APIs:</span></span>

1. <span data-ttu-id="81137-140">Visual Studio(**새로 만들기** > **프로젝트** > **Visual C#** > **Windows 클래식 바탕 화면** > **콘솔 앱(.NET Framework)**)에서 C# 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81137-140">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="81137-141">Machine Learning Web Service 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-141">Sign in to the Machine Learning Web Services portal.</span></span>
3. <span data-ttu-id="81137-142">현재 작업 중인 웹 서비스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-142">Click the web service that you're working with.</span></span>
4. <span data-ttu-id="81137-143">**사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-143">Click **Consume**.</span></span>
5. <span data-ttu-id="81137-144">**사용** 페이지의 맨 아래에 있는 **샘플 코드** 섹션에서 **Batch**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-144">At the bottom of the **Consume** page, in the **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="81137-145">배치 실행을 위해 샘플 C# 코드를 복사한 다음 Program.cs 파일에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="81137-145">Copy the sample C# code for batch execution and paste it into the Program.cs file.</span></span> <span data-ttu-id="81137-146">네임스페이스를 그대로 유지하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-146">Make sure that the namespace remains intact.</span></span>

<span data-ttu-id="81137-147">설명에서 지정된 대로 NuGet 패키지인 Microsoft.AspNet.WebApi.Client를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-147">Add the NuGet package Microsoft.AspNet.WebApi.Client, as specified in the comments.</span></span> <span data-ttu-id="81137-148">Microsoft.WindowsAzure.Storage.dll에 참조를 추가하려면 우선 [Azure Storage 서비스용 클라이언트 라이브러리](https://www.nuget.org/packages/WindowsAzure.Storage)를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-148">To add the reference to Microsoft.WindowsAzure.Storage.dll, you might first need to install the [client library for Azure Storage services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

<span data-ttu-id="81137-149">다음 스크린 샷은 Azure Machine Learning Web Services 포털의 **사용** 페이지를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="81137-149">The following screenshot shows the **Consume** page in the Azure Machine Learning Web Services portal.</span></span>

![사용 페이지][1]

### <a name="update-the-apikey-declaration"></a><span data-ttu-id="81137-151">apikey 선언 업데이트</span><span class="sxs-lookup"><span data-stu-id="81137-151">Update the apikey declaration</span></span>
<span data-ttu-id="81137-152">**apikey** 선언을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="81137-152">Locate the **apikey** declaration:</span></span>

    const string apiKey = "abc123"; // Replace this with the API key for the web service

<span data-ttu-id="81137-153">**사용** 페이지의 **기본 사용량 정보** 섹션에서 기본 키를 찾아 **apikey** 선언으로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-153">In the **Basic consumption info** section of the **Consume** page, locate the primary key and copy it to the **apikey** declaration.</span></span>

### <a name="update-the-azure-storage-information"></a><span data-ttu-id="81137-154">Azure 저장소 정보 업데이트</span><span class="sxs-lookup"><span data-stu-id="81137-154">Update the Azure Storage information</span></span>
<span data-ttu-id="81137-155">BES 샘플 코드는 로컬 드라이브에서(예: "C:\temp\CensusIpnput.csv") Azure Storage로 파일을 업로드하고 이를 처리하고 결과를 Azure Storage에 다시 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-155">The BES sample code uploads a file from a local drive (for example, "C:\temp\CensusIpnput.csv") to Azure Storage, processes it, and writes the results back to Azure Storage.</span></span>  

<span data-ttu-id="81137-156">Azure Storage 정보를 업데이트하려면 Azure 클래식 포털에서 저장소 계정에 대한 저장소 계정 이름, 키 및 컨테이너 정보 검색한 다음 해당 값을 업데이트해야 합니다. 실험을 실행한 후 결과 워크플로가 다음과 유사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-156">To update the Azure Storage information, you must retrieve the storage account name, key, and container information for your storage account from the Azure classic portal, and then update the correspondi After running your experiment, the resulting workflow should be similar to the following:</span></span>

![실행 후 결과 워크플로][4]<span data-ttu-id="81137-158">코드에서 ng 값입니다.</span><span class="sxs-lookup"><span data-stu-id="81137-158">ng values in the code.</span></span>

1. <span data-ttu-id="81137-159">Azure 클래식 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-159">Sign in to the Azure classic portal.</span></span>
2. <span data-ttu-id="81137-160">왼쪽 탐색 열에서 **Storage**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-160">In the left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="81137-161">저장소 계정 목록에서 하나를 선택하여 재학습된 모델을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-161">From the list of storage accounts, select one to store the retrained model.</span></span>
4. <span data-ttu-id="81137-162">페이지 맨 아래에 있는 **액세스 키 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-162">At the bottom of the page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="81137-163">**기본 액세스 키**를 복사하여 저장한 후 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="81137-163">Copy and save the **Primary Access Key** and close the dialog.</span></span>
6. <span data-ttu-id="81137-164">페이지 위쪽에서 **컨테이너**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-164">At the top of the page, click **Containers**.</span></span>
7. <span data-ttu-id="81137-165">기존 컨테이너를 선택하거나 새 컨테이너를 만들어 이름을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-165">Select an existing container, or create a new one and save the name.</span></span>

<span data-ttu-id="81137-166">*StorageAccountName*, *StorageAccountKey* 및 *StorageContainerName* 선언을 찾아 클래식 포털에서 저장한 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-166">Locate the *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations, and update the values that you saved from the classic portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure storage account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage container name

<span data-ttu-id="81137-167">또한 코드에 지정한 위치에서 입력 파일을 사용할 수 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-167">You also must ensure that the input file is available at the location that you specify in the code.</span></span>

### <a name="specify-the-output-location"></a><span data-ttu-id="81137-168">출력 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-168">Specify the output location</span></span>
<span data-ttu-id="81137-169">요청 페이로드에서 출력 위치를 지정할 때 *RelativeLocation* 에서 지정된 파일의 확장명을 csv에서 `ilearner`으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-169">When you specify the output location in the Request Payload, the extension of the file that is specified in *RelativeLocation* must be specified as `ilearner`.</span></span> <span data-ttu-id="81137-170">다음 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81137-170">See the following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with the location you want to use for your output file and a valid file extension (usually .csv for scoring results or .ilearner for trained models)*/
            }
        },

<span data-ttu-id="81137-171">다음은 재학습 출력의 예입니다. ![재학습 출력][6]</span><span class="sxs-lookup"><span data-stu-id="81137-171">The following is an example of retraining output: ![Retraining output][6]</span></span>

## <a name="evaluate-the-retraining-results"></a><span data-ttu-id="81137-172">재학습 결과 평가</span><span class="sxs-lookup"><span data-stu-id="81137-172">Evaluate the retraining results</span></span>
<span data-ttu-id="81137-173">응용 프로그램을 실행할 때 출력은 평가 결과를 액세스하는 데 필요한 URL 및 공유 액세스 서명 토큰을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-173">When you run the application, the output includes the URL and shared access signatures token that are necessary to access the evaluation results.</span></span>

<span data-ttu-id="81137-174">*output2*에 대한 출력 결과의 *BaseLocation*, *RelativeLocation* 및 *SasBlobToken*을 조합하고(앞서 재학습 출력 이미지에 표시된 것처럼) 브라우저 주소 표시줄에 전체 URL을 붙여넣어 다시 학습된 모델의 성능 결과를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81137-174">You can see the performance results of the retrained model by combining the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results for *output2* (as shown in the preceding retraining output image) and pasting the complete URL into the browser address bar.</span></span>  

<span data-ttu-id="81137-175">새로 학습된 모델이 기존 모델을 대체할 만큼 성능이 뛰어난지 여부를 확인하도록 결과를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-175">Examine the results to determine whether the newly trained model performs well enough to replace the existing one.</span></span>

<span data-ttu-id="81137-176">출력 결과에서 *BaseLocation*, *RelativeLocation* 및 *SasBlobToken*을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-176">Copy the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results.</span></span>

## <a name="retrain-the-web-service"></a><span data-ttu-id="81137-177">웹 서비스 재학습</span><span class="sxs-lookup"><span data-stu-id="81137-177">Retrain the web service</span></span>
<span data-ttu-id="81137-178">새 웹 서비스를 다시 교육하는 경우 새로 학습된 모델을 참조하여 예측 웹 서비스 정의를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-178">When you retrain a new web service, you update the predictive web service definition to reference the new trained model.</span></span> <span data-ttu-id="81137-179">웹 서비스 정의는 웹 서비스 학습된 모델의 내부 표현이며 직접 수정할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="81137-179">The web service definition is an internal representation of the trained model of the web service and is not directly modifiable.</span></span> <span data-ttu-id="81137-180">학습 실험이 아닌 예측 실험에 대한 웹 서비스 정의를 검색하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-180">Make sure that you are retrieving the web service definition for your predictive experiment and not your training experiment.</span></span>

## <a name="sign-in-to-azure-resource-manager"></a><span data-ttu-id="81137-181">Azure Resource Manager로 로그인</span><span class="sxs-lookup"><span data-stu-id="81137-181">Sign in to Azure Resource Manager</span></span>
<span data-ttu-id="81137-182">먼저 [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet을 사용하여 PowerShell 환경 내에서 Azure 계정에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-182">You must first sign in to your Azure account from within the PowerShell environment by using the [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-the-web-service-definition-object"></a><span data-ttu-id="81137-183">웹 서비스 정의 개체 가져오기</span><span class="sxs-lookup"><span data-stu-id="81137-183">Get the Web Service Definition object</span></span>
<span data-ttu-id="81137-184">다음으로 [Get AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet을 호출하여 웹 서비스 정의 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="81137-184">Next, get the Web Service Definition object by calling the [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="81137-185">기존 웹 서비스의 리소스 그룹 이름을 결정하려면 구독 중인 웹 서비스를 표시하도록 매개 변수 없이 Get-AzureRmMlWebService cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-185">To determine the resource group name of an existing web service, run the Get-AzureRmMlWebService cmdlet without any parameters to display the web services in your subscription.</span></span> <span data-ttu-id="81137-186">웹 서비스를 찾은 다음 웹 서비스 ID를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="81137-186">Locate the web service, and then look at its web service ID.</span></span> <span data-ttu-id="81137-187">리소스 그룹 이름은 ID의 네 번째 요소로 *resourceGroups* 요소 바로 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81137-187">The name of the resource group is the fourth element in the ID, just after the *resourceGroups* element.</span></span> <span data-ttu-id="81137-188">다음 예제에서 리소스 그룹 이름은 Default-MachineLearning-SouthCentralUS입니다.</span><span class="sxs-lookup"><span data-stu-id="81137-188">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="81137-189">또는 기존 웹 서비스의 리소스 그룹 이름을 결정하려면 Azure Machine Learning Web Services 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-189">Alternatively, to determine the resource group name of an existing web service, sign in to the Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="81137-190">웹 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-190">Select the web service.</span></span> <span data-ttu-id="81137-191">리소스 그룹 이름은 웹 서비스 URL의 다섯 번째 요소로 *resourceGroups* 요소 바로 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81137-191">The resource group name is the fifth element of the URL of the web service, just after the *resourceGroups* element.</span></span> <span data-ttu-id="81137-192">다음 예제에서 리소스 그룹 이름은 Default-MachineLearning-SouthCentralUS입니다.</span><span class="sxs-lookup"><span data-stu-id="81137-192">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-the-web-service-definition-object-as-json"></a><span data-ttu-id="81137-193">JSON으로 웹 서비스 정의 개체 내보내기</span><span class="sxs-lookup"><span data-stu-id="81137-193">Export the Web Service Definition object as JSON</span></span>
<span data-ttu-id="81137-194">새로 학습된 모델을 사용하여 새로 학습된 모델에 대한 정의를 수정하려면 먼저 [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet을 사용하여 JSON 형식 파일에 내보내기해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-194">To modify the definition of the trained model to use the newly trained model, you must first use the [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet to export it to a JSON-format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-the-reference-to-the-ilearner-blob"></a><span data-ttu-id="81137-195">ilearner blob에 대한 참조 업데이트</span><span class="sxs-lookup"><span data-stu-id="81137-195">Update the reference to the ilearner blob</span></span>
<span data-ttu-id="81137-196">자산에서 [학습된 모델]을 찾아, ilearner Blob의 URI와 함께 *locationInfo* 노드의 *uri* 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-196">In the assets, locate the [trained model], update the *uri* value in the *locationInfo* node with the URI of the ilearner blob.</span></span> <span data-ttu-id="81137-197">URI는 BES 재학습 호출의 출력에서 *BaseLocation* 및 *RelativeLocation*을 조합하여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81137-197">The URI is generated by combining the *BaseLocation* and the *RelativeLocation* from the output of the BES retraining call.</span></span>

     "asset3": {
        "name": "Retrain Sample [trained model]",
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

## <a name="import-the-json-into-a-web-service-definition-object"></a><span data-ttu-id="81137-198">JSON을 웹 서비스 정의 개체로 가져오기</span><span class="sxs-lookup"><span data-stu-id="81137-198">Import the JSON into a Web Service Definition object</span></span>
<span data-ttu-id="81137-199">수정된 JSON 파일을 예측 실험을 업데이트하는 데 사용할 수 있는 웹 서비스 정의 개체로 변환하려면 [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-199">You must use the [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet to convert the modified JSON file back into a Web Service Definition object that you can use to update the predicative experiment.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-the-web-service"></a><span data-ttu-id="81137-200">웹 서비스 업데이트</span><span class="sxs-lookup"><span data-stu-id="81137-200">Update the web service</span></span>
<span data-ttu-id="81137-201">마지막으로, [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet를 사용하여 예측 실험을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="81137-201">Finally, use the [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet to update the predictive experiment.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

[1]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-consume-page.png
[4]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE04.png
[6]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE06.png

<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
