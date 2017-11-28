---
title: "스트림 분석에서 aaaUse Azure 기계 학습 끝점 | Microsoft Docs"
description: "Stream Analytics의 기계 언어 사용자 정의 함수"
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 406b258f-b8c2-4e55-953c-b7f84e8e5354
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 013b841ee85b1e0b6d8139a9ba0dde88fc3f8ad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-integration-in-stream-analytics"></a><span data-ttu-id="e0161-103">Stream Analytics의 Machine Learning 통합</span><span class="sxs-lookup"><span data-stu-id="e0161-103">Machine Learning integration in Stream Analytics</span></span>
<span data-ttu-id="e0161-104">스트림 분석 tooAzure 기계 학습 끝점을 호출 하는 사용자 정의 함수를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-104">Stream Analytics supports user-defined functions that call out tooAzure Machine Learning endpoints.</span></span> <span data-ttu-id="e0161-105">이 기능에 대 한 REST API 지원 hello에 자세히 설명 되어 [스트림 분석 REST API 라이브러리](https://msdn.microsoft.com/library/azure/dn835031.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-105">REST API support for this feature is detailed in hello [Stream Analytics REST API library](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span></span> <span data-ttu-id="e0161-106">이 문서에서는 Stream Analytics에서 이 기능을 성공적으로 구현하기 위해 필요한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-106">This article provides supplemental information needed for successful implementation of this capability in Stream Analytics.</span></span> <span data-ttu-id="e0161-107">자습서도 게시되어 있으며 [여기](stream-analytics-machine-learning-integration-tutorial.md)서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-107">A tutorial has also been posted and is available [here](stream-analytics-machine-learning-integration-tutorial.md).</span></span>

## <a name="overview-azure-machine-learning-terminology"></a><span data-ttu-id="e0161-108">개요: Azure Machine Learning 용어</span><span class="sxs-lookup"><span data-stu-id="e0161-108">Overview: Azure Machine Learning terminology</span></span>
<span data-ttu-id="e0161-109">사용할 수 있는 공동 작업, 끌어서 놓기 도구를 제공 하는 Microsoft Azure 기계 학습 toobuild, 테스트 및 사용자 데이터에 대 한 예측 분석 솔루션을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-109">Microsoft Azure Machine Learning provides a collaborative, drag-and-drop tool you can use toobuild, test, and deploy predictive analytics solutions on your data.</span></span> <span data-ttu-id="e0161-110">이 도구는 hello 라고 *Azure 기계 학습 스튜디오*합니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-110">This tool is called hello *Azure Machine Learning Studio*.</span></span> <span data-ttu-id="e0161-111">hello studio hello로 사용 되는 toointeract 기계 학습 리소스는 및 쉽게 빌드, 테스트 및 디자인을 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-111">hello studio is used toointeract with hello Machine Learning resources and easily build, test, and iterate on your design.</span></span> <span data-ttu-id="e0161-112">이러한 리소스 및 해당 정의는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-112">These resources and their definitions are below.</span></span>

* <span data-ttu-id="e0161-113">**작업 영역**: hello *작업 영역* 관리 및 제어에 대 한 컨테이너에서 함께 다른 모든 기계 학습 리소스를 보유 하는 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-113">**Workspace**: hello *workspace* is a container that holds all other Machine Learning resources together in a container for management and control.</span></span>
* <span data-ttu-id="e0161-114">**실험**: *실험* 기계 학습 모델을 학습 하 고 데이터 과학자 tooutilize 데이터 집합에 의해 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-114">**Experiment**: *Experiments* are created by data scientists tooutilize datasets and train a machine learning model.</span></span>
* <span data-ttu-id="e0161-115">**끝점**: *끝점* 은 입력으로 사용 되는 개체 tootake 기능 Azure 기계 학습 hello, 지정 된 기계 학습 모델을 적용 및 점수가 매겨진된 출력도 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-115">**Endpoint**: *Endpoints* are hello Azure Machine Learning object used tootake features as input, apply a specified machine learning model and return scored output.</span></span>
* <span data-ttu-id="e0161-116">**점수 매기기 웹 서비스**: *점수 매기기 웹 서비스* 는 위에서 언급한 대로 끝점 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-116">**Scoring Webservice**: A *scoring webservice* is a collection of endpoints as mentioned above.</span></span>

<span data-ttu-id="e0161-117">각 끝점에는 배치 실행 및 동기 실행을 위한 API가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-117">Each endpoint has apis for batch execution and synchronous execution.</span></span> <span data-ttu-id="e0161-118">Stream Analytics은 동기 실행을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-118">Stream Analytics uses synchronous execution.</span></span> <span data-ttu-id="e0161-119">hello 특정 서비스는 이름이 [요청/응답 서비스](../machine-learning/machine-learning-consume-web-services.md) AzureML studio에서.</span><span class="sxs-lookup"><span data-stu-id="e0161-119">hello specific service is named a [Request/Response Service](../machine-learning/machine-learning-consume-web-services.md) in AzureML studio.</span></span>

## <a name="machine-learning-resources-needed-for-stream-analytics-jobs"></a><span data-ttu-id="e0161-120">Stream Analytics 작업에 필요한 Machine Learning 리소스</span><span class="sxs-lookup"><span data-stu-id="e0161-120">Machine Learning resources needed for Stream Analytics jobs</span></span>
<span data-ttu-id="e0161-121">스트림 분석의 hello 목적을 위해 처리, 요청/응답 끝점 작업는 [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), swagger 정의 및 실행 하는 데에 대 한 모든 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-121">For hello purposes of Stream Analytics job processing, a Request/Response endpoint, an [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), and a swagger definition are all necessary for successful execution.</span></span> <span data-ttu-id="e0161-122">스트림 분석에 swagger 끝점에 대 한 hello url을 생성 하 고, hello 인터페이스를 조회 한 다음 기본 UDF 정의 toohello 사용자를 반환 하는 추가 끝점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-122">Stream Analytics has an additional endpoint that constructs hello url for swagger endpoint, looks up hello interface and returns a default UDF definition toohello user.</span></span>

## <a name="configure-a-stream-analytics-and-machine-learning-udf-via-rest-api"></a><span data-ttu-id="e0161-123">REST API를 통해 Stream Analytics 및 Machine Learning UDF 구성</span><span class="sxs-lookup"><span data-stu-id="e0161-123">Configure a Stream Analytics and Machine Learning UDF via REST API</span></span>
<span data-ttu-id="e0161-124">REST Api를 사용 하 여 사용자 작업 toocall Azure 컴퓨터 언어 기능을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-124">By using REST APIs you may configure your job toocall Azure Machine Language functions.</span></span> <span data-ttu-id="e0161-125">hello 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-125">hello steps are as follows:</span></span>

1. <span data-ttu-id="e0161-126">Stream Analytics 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="e0161-126">Create a Stream Analytics job</span></span>
2. <span data-ttu-id="e0161-127">입력 정의</span><span class="sxs-lookup"><span data-stu-id="e0161-127">Define an input</span></span>
3. <span data-ttu-id="e0161-128">출력 정의</span><span class="sxs-lookup"><span data-stu-id="e0161-128">Define an output</span></span>
4. <span data-ttu-id="e0161-129">UDF(사용자 정의 함수) 만들기</span><span class="sxs-lookup"><span data-stu-id="e0161-129">Create a user-defined function (UDF)</span></span>
5. <span data-ttu-id="e0161-130">Hello UDF를 호출 하는 스트림 분석 변환을 작성합니다</span><span class="sxs-lookup"><span data-stu-id="e0161-130">Write a Stream Analytics transformation that calls hello UDF</span></span>
6. <span data-ttu-id="e0161-131">Hello 작업 시작</span><span class="sxs-lookup"><span data-stu-id="e0161-131">Start hello job</span></span>

## <a name="creating-a-udf-with-basic-properties"></a><span data-ttu-id="e0161-132">기본 속성을 사용하여 UDF 만들기</span><span class="sxs-lookup"><span data-stu-id="e0161-132">Creating a UDF with basic properties</span></span>
<span data-ttu-id="e0161-133">예를 들어, 다음 샘플 코드는 hello 라는 스칼라 UDF를 만듭니다 *newudf* tooan Azure 기계 학습 끝점을 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-133">As an example, hello following sample code creates a scalar UDF named *newudf* that binds tooan Azure Machine Learning endpoint.</span></span> <span data-ttu-id="e0161-134">해당 hello 참고 *끝점* hello 및 서비스를 선택 하는 hello에 대 한 hello API 도움말 페이지 (서비스 URI)를 찾을 수 *apiKey* hello 서비스 기본 페이지에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-134">Note that hello *endpoint* (service URI) can be found on hello API help page for hello chosen service and hello *apiKey* can be found on hello Services main page.</span></span>

````
    PUT : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>  
````

<span data-ttu-id="e0161-135">요청 본문 예제:</span><span class="sxs-lookup"><span data-stu-id="e0161-135">Example request body:</span></span>  

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77fb4b46bf2a30c63c078dca/services/b7be5e40fd194258796fb402c1958eaf/execute ",
                        "apiKey": "replacekeyhere"
                    }
                }
            }
        }
    }
````

## <a name="call-retrievedefaultdefinition-endpoint-for-default-udf"></a><span data-ttu-id="e0161-136">기본 UDF에 대한 RetrieveDefaultDefinition 끝점 호출</span><span class="sxs-lookup"><span data-stu-id="e0161-136">Call RetrieveDefaultDefinition endpoint for default UDF</span></span>
<span data-ttu-id="e0161-137">한 번 hello UDF를 hello UDF 필요한 hello의 전체 정의 생성 하는 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-137">Once hello skeleton UDF is created hello complete definition of hello UDF is needed.</span></span> <span data-ttu-id="e0161-138">hello RetreiveDefaultDefinition 끝점 스칼라 함수는 바인딩된 tooan Azure 기계 학습 끝점에 대 한 hello default 정의 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-138">hello RetreiveDefaultDefinition endpoint helps you get hello default definition for a scalar function that is bound tooan Azure Machine Learning endpoint.</span></span> <span data-ttu-id="e0161-139">아래 hello 페이로드 스칼라 함수는 바인딩된 tooan Azure 기계 학습 끝점에 대 한 tooget hello 기본 UDF 정의가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-139">hello payload below requires you tooget hello default UDF definition for a scalar function that is bound tooan Azure Machine Learning endpoint.</span></span> <span data-ttu-id="e0161-140">PUT 요청 중에 제공한 이미 hello 실제 끝점을 지정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-140">It doesn’t specify hello actual endpoint as it has already been provided during PUT request.</span></span> <span data-ttu-id="e0161-141">명시적으로 제공 되는 경우 hello 요청에 제공 된 hello 끝점을 호출 하는 스트림 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-141">Stream Analytics calls hello endpoint provided in hello request if it is provided explicitly.</span></span> <span data-ttu-id="e0161-142">그렇지 않은 경우 원래 참조 하나 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-142">Otherwise it uses hello one originally referenced.</span></span> <span data-ttu-id="e0161-143">여기 hello UDF 하나는 단일 문자열을 해당 문장에 대 한 hello "정서" 레이블을 나타내는 문자열 형식의 단일 출력 매개 변수 (문장) 및 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-143">Here hello UDF takes a single string parameter (a sentence) and returns a single output of type string which indicates hello “sentiment” label for that sentence.</span></span>

````
POST : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>/RetrieveDefaultDefinition?api-version=<apiVersion>
````

<span data-ttu-id="e0161-144">요청 본문 예제:</span><span class="sxs-lookup"><span data-stu-id="e0161-144">Example request body:</span></span>  

````
    {
        "bindingType": "Microsoft.MachineLearning/WebService",
        "bindingRetrievalProperties": {
            "executeEndpoint": null,
            "udfType": "Scalar"
        }
    }
````

<span data-ttu-id="e0161-145">이 샘플 출력은 아래와 비슷하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-145">A sample output of this would look something like below.</span></span>  

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "inputs": [{
                    "dataType": "nvarchar(max)",
                    "isConfigurationParameter": null
                }],
                "output": {
                    "dataType": "nvarchar(max)"
                },
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77ga4a4bbf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",
                        "apiKey": null,
                        "inputs": {
                            "name": "input1",
                            "columnNames": [{
                                "name": "tweet",
                                "dataType": "string",
                                "mapTo": 0
                            }]
                        },
                        "outputs": [{
                            "name": "Sentiment",
                            "dataType": "string"
                        }],
                        "batchSize": 10
                    }
                }
            }
        }
    }
````

## <a name="patch-udf-with-hello-response"></a><span data-ttu-id="e0161-146">Hello 응답과 함께 패치 UDF</span><span class="sxs-lookup"><span data-stu-id="e0161-146">Patch UDF with hello response</span></span>
<span data-ttu-id="e0161-147">이제 hello UDF 패치해야 hello 이전 응답으로 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-147">Now hello UDF must be patched with hello previous response, as shown below.</span></span>

````
PATCH : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>
````

<span data-ttu-id="e0161-148">요청 본문(RetrieveDefaultDefinition):</span><span class="sxs-lookup"><span data-stu-id="e0161-148">Request Body (Output from RetrieveDefaultDefinition):</span></span>

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "inputs": [{
                    "dataType": "nvarchar(max)",
                    "isConfigurationParameter": null
                }],
                "output": {
                    "dataType": "nvarchar(max)"
                },
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77ga4a4bbf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",
                        "apiKey": null,
                        "inputs": {
                            "name": "input1",
                            "columnNames": [{
                                "name": "tweet",
                                "dataType": "string",
                                "mapTo": 0
                            }]
                        },
                        "outputs": [{
                            "name": "Sentiment",
                            "dataType": "string"
                        }],
                        "batchSize": 10
                    }
                }
            }
        }
    }
````

## <a name="implement-stream-analytics-transformation-toocall-hello-udf"></a><span data-ttu-id="e0161-149">스트림 분석 변환 toocall hello UDF를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-149">Implement Stream Analytics transformation toocall hello UDF</span></span>
<span data-ttu-id="e0161-150">이제 hello UDF (여기 scoreTweet 라고 함)을 입력된 모든 이벤트에 대해 쿼리하고 해당 이벤트 tooan 출력에 대 한 응답을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0161-150">Now query hello UDF (here named scoreTweet) for every input event and write a response for that event tooan output.</span></span>  

````
    {
        "name": "transformation",
        "properties": {
            "streamingUnits": null,
            "query": "select *,scoreTweet(Tweet) TweetSentiment into blobOutput from blobInput"
        }
    }
````


## <a name="get-help"></a><span data-ttu-id="e0161-151">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="e0161-151">Get help</span></span>
<span data-ttu-id="e0161-152">추가 지원이 필요할 경우 [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="e0161-152">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0161-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e0161-153">Next steps</span></span>
* [<span data-ttu-id="e0161-154">스트림 분석 소개 tooAzure</span><span class="sxs-lookup"><span data-stu-id="e0161-154">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="e0161-155">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="e0161-155">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="e0161-156">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="e0161-156">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="e0161-157">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="e0161-157">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="e0161-158">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="e0161-158">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
