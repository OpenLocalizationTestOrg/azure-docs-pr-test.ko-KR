---
title: "웹 서비스에는 기존 예측 aaaRetrain | Microsoft Docs"
description: "Tooretrain 모델 및 update hello 웹 서비스 toouse hello 새로 학습 된 모델에 Azure 기계 학습 방법에 대해 알아봅니다."
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
ms.openlocfilehash: fb0760d0a2adc34fc5f3df1ae41bdac075f91bf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-an-existing-predictive-web-service"></a><span data-ttu-id="d412c-103">기존 예측 웹 서비스 재학습</span><span class="sxs-lookup"><span data-stu-id="d412c-103">Retrain an existing predictive web service</span></span>
<span data-ttu-id="d412c-104">이 문서에서는 hello를 재교육 시나리오를 따르는 hello에 대 한 프로세스를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-104">This document describes hello retraining process for hello following scenario:</span></span>

* <span data-ttu-id="d412c-105">조작 가능한 웹 서비스로 배포한 학습 실험 및 예측 실험이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-105">You have a training experiment and a predictive experiment that you have deployed as an operationalized web service.</span></span>
* <span data-ttu-id="d412c-106">새 데이터를 지정 하 여 예측 웹 서비스 toouse tooperform 해당 점수 매기기 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-106">You have new data that you want your predictive web service toouse tooperform its scoring.</span></span>

> [!NOTE] 
> <span data-ttu-id="d412c-107">toodeploy 충분 한 권한이의 해야 hello 구독 toowhich hello 웹 서비스를 배포 하면 새 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-107">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="d412c-108">자세한 내용은 참조 하십시오 [hello Azure 컴퓨터 학습 웹 서비스 포털을 사용 하 여 웹 서비스 관리](machine-learning-manage-new-webservice.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-108">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="d412c-109">기존 웹 서비스 및 실험 부터는 필요한 toofollow 다음이 단계:</span><span class="sxs-lookup"><span data-stu-id="d412c-109">Starting with your existing web service and experiments, you need toofollow these steps:</span></span>

1. <span data-ttu-id="d412c-110">Hello 모델을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-110">Update hello model.</span></span>
   1. <span data-ttu-id="d412c-111">웹 서비스 입력 및 출력에 대 한 학습 실험 tooallow 프로그램을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-111">Modify your training experiment tooallow for web service inputs and outputs.</span></span>
   2. <span data-ttu-id="d412c-112">Hello 학습 실험 재교육 웹 서비스로 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-112">Deploy hello training experiment as a retraining web service.</span></span>
   3. <span data-ttu-id="d412c-113">Hello 학습 실험 일괄 처리 실행 서비스 (BES) tooretrain hello 모델을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-113">Use hello training experiment's Batch Execution Service (BES) tooretrain hello model.</span></span>
2. <span data-ttu-id="d412c-114">Hello Azure 컴퓨터 학습 PowerShell cmdlet tooupdate hello 예측 실험을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-114">Use hello Azure Machine Learning PowerShell cmdlets tooupdate hello predictive experiment.</span></span>
   1. <span data-ttu-id="d412c-115">Tooyour Azure 리소스 관리자 계정에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-115">Sign in tooyour Azure Resource Manager account.</span></span>
   2. <span data-ttu-id="d412c-116">Hello 웹 서비스 정을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-116">Get hello web service definition.</span></span>
   3. <span data-ttu-id="d412c-117">JSON으로 hello 웹 서비스 정을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-117">Export hello web service definition as JSON.</span></span>
   4. <span data-ttu-id="d412c-118">Hello JSON hello 참조 toohello ilearner blob를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-118">Update hello reference toohello ilearner blob in hello JSON.</span></span>
   5. <span data-ttu-id="d412c-119">웹 서비스 정의로 hello를 JSON을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-119">Import hello JSON into a web service definition.</span></span>
   6. <span data-ttu-id="d412c-120">새 웹 서비스 정의로 hello 웹 서비스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-120">Update hello web service with a new web service definition.</span></span>

## <a name="deploy-hello-training-experiment"></a><span data-ttu-id="d412c-121">Hello 학습 실험 배포</span><span class="sxs-lookup"><span data-stu-id="d412c-121">Deploy hello training experiment</span></span>
<span data-ttu-id="d412c-122">재교육 웹 서비스로 toodeploy hello 학습 실험을 웹 서비스 입력 및 출력 toohello 모델을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-122">toodeploy hello training experiment as a retraining web service, you must add web service inputs and outputs toohello model.</span></span> <span data-ttu-id="d412c-123">연결 하 여 한 *웹 서비스 출력* 모듈 toohello 실험  *[모델 학습] [ train-model]*  학습 실험 hello를 사용 하면 모듈을 tooproduce 새 학습 된 모델을 예측 하 여 실험에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-123">By connecting a *Web Service Output* module toohello experiment's *[Train Model][train-model]* module, you enable hello training experiment tooproduce a new trained model that you can use in your predictive experiment.</span></span> <span data-ttu-id="d412c-124">있는 경우는 *모델 평가* 모듈을 출력으로 웹 서비스 출력 tooget hello 평가 결과 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-124">If you have an *Evaluate Model* module, you can also attach web service output tooget hello evaluation results as output.</span></span>

<span data-ttu-id="d412c-125">tooupdate 학습 실험:</span><span class="sxs-lookup"><span data-stu-id="d412c-125">tooupdate your training experiment:</span></span>

1. <span data-ttu-id="d412c-126">연결 된 *웹 서비스 입력* 모듈 tooyour 데이터 입력 (예를 들어 한 *누락 데이터 정리* 모듈).</span><span class="sxs-lookup"><span data-stu-id="d412c-126">Connect a *Web Service Input* module tooyour data input (for example, a *Clean Missing Data* module).</span></span> <span data-ttu-id="d412c-127">일반적으로 입력된 데이터에서 처리 되는 tooensure 원하는 hello 동일한 방식으로 원래 학습 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-127">Typically, you want tooensure that your input data is processed in hello same way as your original training data.</span></span>
2. <span data-ttu-id="d412c-128">연결 된 *웹 서비스 출력* 모듈 toohello 출력의 프로그램 *모델 학습* 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-128">Connect a *Web Service Output* module toohello output of your *Train Model* module.</span></span>
3. <span data-ttu-id="d412c-129">있는 경우는 *모델 평가* toooutput hello 평가 결과 원하는 모듈 하 고, 연결 된 *웹 서비스 출력* 모듈 toohello 출력의 프로그램 *모델 평가* 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-129">If you have an *Evaluate Model* module and you want toooutput hello evaluation results, connect a *Web Service Output* module toohello output of your *Evaluate Model* module.</span></span>

<span data-ttu-id="d412c-130">실험을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-130">Run your experiment.</span></span>

<span data-ttu-id="d412c-131">다음으로 hello 학습 실험 학습된 된 모델 및 모델 평가 결과 생성 하는 웹 서비스로 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-131">Next, you must deploy hello training experiment as a web service that produces a trained model and model evaluation results.</span></span>  

<span data-ttu-id="d412c-132">Hello 실험 캔버스의 hello 아래쪽 클릭 **웹 서비스 설정**를 선택한 후 **웹 서비스 배포 [New]**합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-132">At hello bottom of hello experiment canvas, click **Set Up Web Service**, and then select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="d412c-133">hello Azure 컴퓨터 학습 웹 서비스 포털도 열립니다 toohello **웹 서비스 배포** 페이지.</span><span class="sxs-lookup"><span data-stu-id="d412c-133">hello Azure Machine Learning Web Services portal opens toohello **Deploy Web Service** page.</span></span> <span data-ttu-id="d412c-134">웹 서비스의 이름을 입력하고 결제 방식을 선택한 다음 **배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-134">Type a name for your web service, choose a payment plan, and then click **Deploy**.</span></span> <span data-ttu-id="d412c-135">학습 된 모델을 만들기 위한 hello 일괄 처리 실행 방법만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-135">You can only use hello Batch Execution method for creating trained models.</span></span>

## <a name="retrain-hello-model-with-new-data-by-using-bes"></a><span data-ttu-id="d412c-136">BES를 사용 하 여 새 데이터를 사용 하 여 hello 모델을 다시 학습</span><span class="sxs-lookup"><span data-stu-id="d412c-136">Retrain hello model with new data by using BES</span></span>
<span data-ttu-id="d412c-137">이 예제에서는 C# toocreate hello 재교육 응용 프로그램 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-137">For this example, we're using C# toocreate hello retraining application.</span></span> <span data-ttu-id="d412c-138">또한이 작업 Python 또는 R 샘플 코드 tooaccomplish를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-138">You can also use Python or R sample code tooaccomplish this task.</span></span>

<span data-ttu-id="d412c-139">Api 재교육 toocall hello:</span><span class="sxs-lookup"><span data-stu-id="d412c-139">toocall hello retraining APIs:</span></span>

1. <span data-ttu-id="d412c-140">Visual Studio(**새로 만들기** > **프로젝트** > **Visual C#** > **Windows 클래식 바탕 화면** > **콘솔 앱(.NET Framework)**)에서 C# 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-140">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="d412c-141">시스템 학습 웹 서비스 포털 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-141">Sign in toohello Machine Learning Web Services portal.</span></span>
3. <span data-ttu-id="d412c-142">작업 하는 hello 웹 서비스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-142">Click hello web service that you're working with.</span></span>
4. <span data-ttu-id="d412c-143">**사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-143">Click **Consume**.</span></span>
5. <span data-ttu-id="d412c-144">Hello hello 맨 아래에 **사용** 페이지 hello **샘플 코드** 섹션에서 클릭 **일괄 처리**합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-144">At hello bottom of hello **Consume** page, in hello **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="d412c-145">일괄 처리 실행에 대 한 hello 샘플 C# 코드를 복사 하 고 hello Program.cs 파일에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-145">Copy hello sample C# code for batch execution and paste it into hello Program.cs file.</span></span> <span data-ttu-id="d412c-146">해당 hello 네임 스페이스는 그대로 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-146">Make sure that hello namespace remains intact.</span></span>

<span data-ttu-id="d412c-147">Hello 설명에 지정 된 대로 Microsoft.AspNet.WebApi.Client, hello NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-147">Add hello NuGet package Microsoft.AspNet.WebApi.Client, as specified in hello comments.</span></span> <span data-ttu-id="d412c-148">tooadd hello 참조 tooMicrosoft.WindowsAzure.Storage.dll 먼저 해야 tooinstall hello [Azure 저장소 서비스에 대 한 클라이언트 라이브러리](https://www.nuget.org/packages/WindowsAzure.Storage)합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-148">tooadd hello reference tooMicrosoft.WindowsAzure.Storage.dll, you might first need tooinstall hello [client library for Azure Storage services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

<span data-ttu-id="d412c-149">hello 다음 스크린샷은 hello **사용** hello Azure 컴퓨터 학습 웹 서비스 포털의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-149">hello following screenshot shows hello **Consume** page in hello Azure Machine Learning Web Services portal.</span></span>

![사용 페이지][1]

### <a name="update-hello-apikey-declaration"></a><span data-ttu-id="d412c-151">Hello apikey 선언 업데이트</span><span class="sxs-lookup"><span data-stu-id="d412c-151">Update hello apikey declaration</span></span>
<span data-ttu-id="d412c-152">Hello 찾을 **apikey** 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-152">Locate hello **apikey** declaration:</span></span>

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

<span data-ttu-id="d412c-153">Hello에 **기본 소비 정보** hello 섹션 **사용** 페이지 hello 기본 키 찾아 toohello 복사 **apikey** 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-153">In hello **Basic consumption info** section of hello **Consume** page, locate hello primary key and copy it toohello **apikey** declaration.</span></span>

### <a name="update-hello-azure-storage-information"></a><span data-ttu-id="d412c-154">Hello Azure 저장소 정보를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-154">Update hello Azure Storage information</span></span>
<span data-ttu-id="d412c-155">hello BES 샘플 코드는 로컬 드라이브 (예: "C:\temp\CensusIpnput.csv") tooAzure 저장소에서에서 파일을 업로드 하 고 처리 한 hello 결과 백 tooAzure 저장소를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-155">hello BES sample code uploads a file from a local drive (for example, "C:\temp\CensusIpnput.csv") tooAzure Storage, processes it, and writes hello results back tooAzure Storage.</span></span>  

<span data-ttu-id="d412c-156">hello 저장소 계정 이름, 키 및 컨테이너 hello Azure 클래식 포털에서에서 저장소 계정에 대 한 정보와 다음 실험을 실행 한 후 업데이트 hello correspondi hello 결과 검색 해야 tooupdate hello Azure 저장소 정보 워크플로 비슷한 toohello 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-156">tooupdate hello Azure Storage information, you must retrieve hello storage account name, key, and container information for your storage account from hello Azure classic portal, and then update hello correspondi After running your experiment, hello resulting workflow should be similar toohello following:</span></span>

![실행 후 결과 워크플로][4]<span data-ttu-id="d412c-158">hello 코드의 ng 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-158">ng values in hello code.</span></span>

1. <span data-ttu-id="d412c-159">Azure 클래식 포털 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-159">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="d412c-160">Hello 왼쪽된 탐색 열에서 클릭 **저장소**합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-160">In hello left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="d412c-161">Hello 저장소 계정 목록에서 선택 하나 toostore hello 모델을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-161">From hello list of storage accounts, select one toostore hello retrained model.</span></span>
4. <span data-ttu-id="d412c-162">Hello hello 페이지의 아래쪽에 있는 클릭 **액세스 키 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-162">At hello bottom of hello page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="d412c-163">복사 하 고 hello 저장 **기본 액세스 키** 및 닫기 hello 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="d412c-163">Copy and save hello **Primary Access Key** and close hello dialog.</span></span>
6. <span data-ttu-id="d412c-164">Hello hello 페이지의 위쪽에 클릭 **컨테이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-164">At hello top of hello page, click **Containers**.</span></span>
7. <span data-ttu-id="d412c-165">기존 컨테이너를 선택 하거나 새 만들고 hello 이름을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-165">Select an existing container, or create a new one and save hello name.</span></span>

<span data-ttu-id="d412c-166">Hello 찾을 *StorageAccountName*, *StorageAccountKey*, 및 *StorageContainerName* 선언 및 hello 클래식 포털에 저장 된 hello 값 업데이트 .</span><span class="sxs-lookup"><span data-stu-id="d412c-166">Locate hello *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations, and update hello values that you saved from hello classic portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure storage account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage container name

<span data-ttu-id="d412c-167">또한 hello이 입력된 파일은 hello 코드에서 지정 된 hello 위치에서 사용할 수 있는 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-167">You also must ensure that hello input file is available at hello location that you specify in hello code.</span></span>

### <a name="specify-hello-output-location"></a><span data-ttu-id="d412c-168">Hello 출력 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-168">Specify hello output location</span></span>
<span data-ttu-id="d412c-169">Hello 요청 페이로드를 hello 출력 위치를 지정 하는 경우에 지정 된 hello 파일의 확장명 hello *RelativeLocation* 로 지정 해야 `ilearner`합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-169">When you specify hello output location in hello Request Payload, hello extension of hello file that is specified in *RelativeLocation* must be specified as `ilearner`.</span></span> <span data-ttu-id="d412c-170">다음 예제는 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d412c-170">See hello following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you want toouse for your output file and a valid file extension (usually .csv for scoring results or .ilearner for trained models)*/
            }
        },

<span data-ttu-id="d412c-171">hello 다음은 출력 재교육의 예: ![재교육 출력][6]</span><span class="sxs-lookup"><span data-stu-id="d412c-171">hello following is an example of retraining output: ![Retraining output][6]</span></span>

## <a name="evaluate-hello-retraining-results"></a><span data-ttu-id="d412c-172">Hello 재교육 결과 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-172">Evaluate hello retraining results</span></span>
<span data-ttu-id="d412c-173">Hello 응용 프로그램을 실행 하면 hello 출력 hello URL 및 필요한 tooaccess hello 평가 결과 해당 하는 공유 액세스 서명 토큰을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-173">When you run hello application, hello output includes hello URL and shared access signatures token that are necessary tooaccess hello evaluation results.</span></span>

<span data-ttu-id="d412c-174">Hello를 결합 하 여 hello 다시 학습 되도록 모델의 hello 성능 결과 볼 수 있습니다 *BaseLocation*, *RelativeLocation*, 및 *SasBlobToken* hello 출력 결과에서 에 대 한 *output2* (에서처럼 hello 재교육 출력 이미지 이전) 및 hello 브라우저 주소 표시줄에 hello 전체 URL 붙여넣기 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-174">You can see hello performance results of hello retrained model by combining hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results for *output2* (as shown in hello preceding retraining output image) and pasting hello complete URL into hello browser address bar.</span></span>  

<span data-ttu-id="d412c-175">Hello 새로 학습 된 모델 하나 기존 tooreplace hello 충분히 잘 수행 하는지 여부 hello 결과 toodetermine를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-175">Examine hello results toodetermine whether hello newly trained model performs well enough tooreplace hello existing one.</span></span>

<span data-ttu-id="d412c-176">복사 hello *BaseLocation*, *RelativeLocation*, 및 *SasBlobToken* hello 출력 결과에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-176">Copy hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results.</span></span>

## <a name="retrain-hello-web-service"></a><span data-ttu-id="d412c-177">Hello 웹 서비스를 다시 학습</span><span class="sxs-lookup"><span data-stu-id="d412c-177">Retrain hello web service</span></span>
<span data-ttu-id="d412c-178">새 웹 서비스를 다시 학습 hello 예측 웹 서비스 정의 tooreference hello 새 학습 된 모델을 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-178">When you retrain a new web service, you update hello predictive web service definition tooreference hello new trained model.</span></span> <span data-ttu-id="d412c-179">hello 웹 서비스 정의 hello 웹 서비스의 hello 학습 된 모델의 내부 표현 되며 직접 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-179">hello web service definition is an internal representation of hello trained model of hello web service and is not directly modifiable.</span></span> <span data-ttu-id="d412c-180">예측 실험 및 하지 학습 실험에 대 한 hello 웹 서비스 정의 검색 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-180">Make sure that you are retrieving hello web service definition for your predictive experiment and not your training experiment.</span></span>

## <a name="sign-in-tooazure-resource-manager"></a><span data-ttu-id="d412c-181">리소스 관리자 tooAzure에 로그인</span><span class="sxs-lookup"><span data-stu-id="d412c-181">Sign in tooAzure Resource Manager</span></span>
<span data-ttu-id="d412c-182">먼저 hello를 사용 하 여 tooyour hello PowerShell 환경 내에서 Azure 계정에에서 로그인 해야 [추가 AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d412c-182">You must first sign in tooyour Azure account from within hello PowerShell environment by using hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-hello-web-service-definition-object"></a><span data-ttu-id="d412c-183">Hello 웹 서비스 정의 개체 가져오기</span><span class="sxs-lookup"><span data-stu-id="d412c-183">Get hello Web Service Definition object</span></span>
<span data-ttu-id="d412c-184">다음으로 호출 hello 여 hello 웹 서비스 정의 개체를 가져올 [Get AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d412c-184">Next, get hello Web Service Definition object by calling hello [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="d412c-185">toodetermine hello 리소스 그룹의 이름 구독에서 모든 매개 변수 toodisplay hello 웹 서비스 없이 hello AzureRmMlWebService Get cmdlet을 실행 하는 기존 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-185">toodetermine hello resource group name of an existing web service, run hello Get-AzureRmMlWebService cmdlet without any parameters toodisplay hello web services in your subscription.</span></span> <span data-ttu-id="d412c-186">Hello 웹 서비스를 찾은 다음 웹 서비스 ID 확인</span><span class="sxs-lookup"><span data-stu-id="d412c-186">Locate hello web service, and then look at its web service ID.</span></span> <span data-ttu-id="d412c-187">hello hello 리소스 그룹 이름은 hello ID의 네 번째 요소 hello hello 직후 *resourceGroups* 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-187">hello name of hello resource group is hello fourth element in hello ID, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="d412c-188">다음 예제는 hello, hello 리소스 그룹 이름은 기본-MachineLearning-SouthCentralUS를입니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-188">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="d412c-189">또는 toodetermine hello 리소스 그룹 이름은 기존 웹 서비스, toohello Azure 컴퓨터 학습 웹 서비스 포털에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-189">Alternatively, toodetermine hello resource group name of an existing web service, sign in toohello Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="d412c-190">Hello 웹 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-190">Select hello web service.</span></span> <span data-ttu-id="d412c-191">hello 리소스 그룹 이름은 hello 직후 hello 웹 서비스의 hello URL의 다섯 번째 요소 hello *resourceGroups* 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-191">hello resource group name is hello fifth element of hello URL of hello web service, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="d412c-192">다음 예제는 hello, hello 리소스 그룹 이름은 기본-MachineLearning-SouthCentralUS를입니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-192">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-object-as-json"></a><span data-ttu-id="d412c-193">Hello 웹 서비스 정의 개체를 JSON으로 내보내기</span><span class="sxs-lookup"><span data-stu-id="d412c-193">Export hello Web Service Definition object as JSON</span></span>
<span data-ttu-id="d412c-194">새로 학습 된 모델의 학습 된 모델 toouse hello hello toomodify hello 정의 hello를 먼저 사용 해야 [내보내기 AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport 것 tooa JSON 형식의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-194">toomodify hello definition of hello trained model toouse hello newly trained model, you must first use hello [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport it tooa JSON-format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob"></a><span data-ttu-id="d412c-195">Hello 참조 toohello ilearner blob를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-195">Update hello reference toohello ilearner blob</span></span>
<span data-ttu-id="d412c-196">Hello 자산에서 hello [학습 된 모델], 업데이트 hello 찾습니다 *uri* hello 값 *locationInfo* hello hello ilearner blob의 URI로 노드.</span><span class="sxs-lookup"><span data-stu-id="d412c-196">In hello assets, locate hello [trained model], update hello *uri* value in hello *locationInfo* node with hello URI of hello ilearner blob.</span></span> <span data-ttu-id="d412c-197">hello URI는 결합 하 여 생성 hello *BaseLocation* 및 hello *RelativeLocation* hello BES 재교육 호출의 hello 출력에서.</span><span class="sxs-lookup"><span data-stu-id="d412c-197">hello URI is generated by combining hello *BaseLocation* and hello *RelativeLocation* from hello output of hello BES retraining call.</span></span>

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

## <a name="import-hello-json-into-a-web-service-definition-object"></a><span data-ttu-id="d412c-198">웹 서비스 정의 개체에 hello JSON 가져오기</span><span class="sxs-lookup"><span data-stu-id="d412c-198">Import hello JSON into a Web Service Definition object</span></span>
<span data-ttu-id="d412c-199">Hello를 사용 해야 [가져오기 AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello tooupdate hello predicative 실험에 사용할 수 있는 웹 서비스 정의 개체에 다시 JSON 파일을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-199">You must use hello [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello modified JSON file back into a Web Service Definition object that you can use tooupdate hello predicative experiment.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service"></a><span data-ttu-id="d412c-200">Hello 웹 서비스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-200">Update hello web service</span></span>
<span data-ttu-id="d412c-201">마지막으로 hello를 사용 하 여 [업데이트 AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello 실험 예측 합니다.</span><span class="sxs-lookup"><span data-stu-id="d412c-201">Finally, use hello [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello predictive experiment.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

[1]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-consume-page.png
[4]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE04.png
[6]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE06.png

<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
