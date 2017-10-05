---
title: "Stream Analytics의 Machine Learning 끝점 사용 | Microsoft Docs"
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
ms.openlocfilehash: d3a46190dd802bf31ea03ef38304d58e6e63b66d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="machine-learning-integration-in-stream-analytics"></a><span data-ttu-id="a123c-103">Stream Analytics의 Machine Learning 통합</span><span class="sxs-lookup"><span data-stu-id="a123c-103">Machine Learning integration in Stream Analytics</span></span>
<span data-ttu-id="a123c-104">Stream Analytics는 Azure Machine Learning 끝점을 호출하는 사용자 정의 함수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-104">Stream Analytics supports user-defined functions that call out to Azure Machine Learning endpoints.</span></span> <span data-ttu-id="a123c-105">이 기능에 대한 REST API 지원은 [Stream Analytics REST API 라이브러리](https://msdn.microsoft.com/library/azure/dn835031.aspx)에 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-105">REST API support for this feature is detailed in the [Stream Analytics REST API library](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span></span> <span data-ttu-id="a123c-106">이 문서에서는 Stream Analytics에서 이 기능을 성공적으로 구현하기 위해 필요한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-106">This article provides supplemental information needed for successful implementation of this capability in Stream Analytics.</span></span> <span data-ttu-id="a123c-107">자습서도 게시되어 있으며 [여기](stream-analytics-machine-learning-integration-tutorial.md)서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-107">A tutorial has also been posted and is available [here](stream-analytics-machine-learning-integration-tutorial.md).</span></span>

## <a name="overview-azure-machine-learning-terminology"></a><span data-ttu-id="a123c-108">개요: Azure Machine Learning 용어</span><span class="sxs-lookup"><span data-stu-id="a123c-108">Overview: Azure Machine Learning terminology</span></span>
<span data-ttu-id="a123c-109">Microsoft Azure Machine Learning은 데이터에 대한 예측 분석 솔루션을 빌드, 테스트, 배포할 수 있는 공동 끌어서 놓기 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-109">Microsoft Azure Machine Learning provides a collaborative, drag-and-drop tool you can use to build, test, and deploy predictive analytics solutions on your data.</span></span> <span data-ttu-id="a123c-110">이 도구를 *Azure Machine Learning 스튜디오*라고 부릅니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-110">This tool is called the *Azure Machine Learning Studio*.</span></span> <span data-ttu-id="a123c-111">이 스튜디오는 Machine Learning 리소스와 상호 작용하고 설계를 간편하게 빌드, 테스트 및 반복하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-111">The studio is used to interact with the Machine Learning resources and easily build, test, and iterate on your design.</span></span> <span data-ttu-id="a123c-112">이러한 리소스 및 해당 정의는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-112">These resources and their definitions are below.</span></span>

* <span data-ttu-id="a123c-113">**작업 영역**: *작업 영역* 은 관리 및 제어를 위해 다른 모든 Machine Learning 리소스를 함께 보관하는 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-113">**Workspace**: The *workspace* is a container that holds all other Machine Learning resources together in a container for management and control.</span></span>
* <span data-ttu-id="a123c-114">**실험**: 데이터 과학자가 데이터 집합을 활용하고 Machine Learning 모델을 교육하기 위해 *실험* 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-114">**Experiment**: *Experiments* are created by data scientists to utilize datasets and train a machine learning model.</span></span>
* <span data-ttu-id="a123c-115">**끝점**: *끝점* 은 입력으로 기능을 가져오고, 지정된 Machine Learning 모델을 적용하고, 점수가 매겨진 출력을 반환하는 데 사용되는 Azure Machine Learning 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-115">**Endpoint**: *Endpoints* are the Azure Machine Learning object used to take features as input, apply a specified machine learning model and return scored output.</span></span>
* <span data-ttu-id="a123c-116">**점수 매기기 웹 서비스**: *점수 매기기 웹 서비스* 는 위에서 언급한 대로 끝점 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-116">**Scoring Webservice**: A *scoring webservice* is a collection of endpoints as mentioned above.</span></span>

<span data-ttu-id="a123c-117">각 끝점에는 배치 실행 및 동기 실행을 위한 API가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-117">Each endpoint has apis for batch execution and synchronous execution.</span></span> <span data-ttu-id="a123c-118">Stream Analytics은 동기 실행을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-118">Stream Analytics uses synchronous execution.</span></span> <span data-ttu-id="a123c-119">특정 서비스는 AzureML 스튜디오에 있는 [Request/Response Service](../machine-learning/machine-learning-consume-web-services.md) 라는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-119">The specific service is named a [Request/Response Service](../machine-learning/machine-learning-consume-web-services.md) in AzureML studio.</span></span>

## <a name="machine-learning-resources-needed-for-stream-analytics-jobs"></a><span data-ttu-id="a123c-120">Stream Analytics 작업에 필요한 Machine Learning 리소스</span><span class="sxs-lookup"><span data-stu-id="a123c-120">Machine Learning resources needed for Stream Analytics jobs</span></span>
<span data-ttu-id="a123c-121">Stream Analytics 작업을 처리하려면 요청/응답 끝점, [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md)및 swagger 정의가 모두 있어야 성공적으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-121">For the purposes of Stream Analytics job processing, a Request/Response endpoint, an [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), and a swagger definition are all necessary for successful execution.</span></span> <span data-ttu-id="a123c-122">Stream Analytics에는 swagger 끝점에 대한 url을 생성하고, 인터페이스를 조회하고, 사용자에게 기본 UDF 정의를 반환하는 추가 끝점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-122">Stream Analytics has an additional endpoint that constructs the url for swagger endpoint, looks up the interface and returns a default UDF definition to the user.</span></span>

## <a name="configure-a-stream-analytics-and-machine-learning-udf-via-rest-api"></a><span data-ttu-id="a123c-123">REST API를 통해 Stream Analytics 및 Machine Learning UDF 구성</span><span class="sxs-lookup"><span data-stu-id="a123c-123">Configure a Stream Analytics and Machine Learning UDF via REST API</span></span>
<span data-ttu-id="a123c-124">REST API를 사용하여 Azure 기계 언어 함수를 호출하는 작업을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-124">By using REST APIs you may configure your job to call Azure Machine Language functions.</span></span> <span data-ttu-id="a123c-125">단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-125">The steps are as follows:</span></span>

1. <span data-ttu-id="a123c-126">Stream Analytics 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="a123c-126">Create a Stream Analytics job</span></span>
2. <span data-ttu-id="a123c-127">입력 정의</span><span class="sxs-lookup"><span data-stu-id="a123c-127">Define an input</span></span>
3. <span data-ttu-id="a123c-128">출력 정의</span><span class="sxs-lookup"><span data-stu-id="a123c-128">Define an output</span></span>
4. <span data-ttu-id="a123c-129">UDF(사용자 정의 함수) 만들기</span><span class="sxs-lookup"><span data-stu-id="a123c-129">Create a user-defined function (UDF)</span></span>
5. <span data-ttu-id="a123c-130">UDF를 호출하는 Stream Analytics 변환 작성</span><span class="sxs-lookup"><span data-stu-id="a123c-130">Write a Stream Analytics transformation that calls the UDF</span></span>
6. <span data-ttu-id="a123c-131">작업 시작</span><span class="sxs-lookup"><span data-stu-id="a123c-131">Start the job</span></span>

## <a name="creating-a-udf-with-basic-properties"></a><span data-ttu-id="a123c-132">기본 속성을 사용하여 UDF 만들기</span><span class="sxs-lookup"><span data-stu-id="a123c-132">Creating a UDF with basic properties</span></span>
<span data-ttu-id="a123c-133">예를 들어 다음 샘플 코드는 Azure Machine Learning 끝점에 바인딩되는 *newudf* 라고 하는 스칼라 UDF를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-133">As an example, the following sample code creates a scalar UDF named *newudf* that binds to an Azure Machine Learning endpoint.</span></span> <span data-ttu-id="a123c-134">*끝점*(서비스 URI)은 선택한 서비스에 대한 API 도움말 페이지에서 찾을 수 있고 *apiKey*는 서비스 기본 페이지에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-134">Note that the *endpoint* (service URI) can be found on the API help page for the chosen service and the *apiKey* can be found on the Services main page.</span></span>

````
    PUT : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>  
````

<span data-ttu-id="a123c-135">요청 본문 예제:</span><span class="sxs-lookup"><span data-stu-id="a123c-135">Example request body:</span></span>  

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

## <a name="call-retrievedefaultdefinition-endpoint-for-default-udf"></a><span data-ttu-id="a123c-136">기본 UDF에 대한 RetrieveDefaultDefinition 끝점 호출</span><span class="sxs-lookup"><span data-stu-id="a123c-136">Call RetrieveDefaultDefinition endpoint for default UDF</span></span>
<span data-ttu-id="a123c-137">기초 UDF를 만든 후에는 완전한 UDF 정의가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-137">Once the skeleton UDF is created the complete definition of the UDF is needed.</span></span> <span data-ttu-id="a123c-138">RetreiveDefaultDefinition 끝점은 Azure Machine Learning 끝점에 바인딩된 스칼라 함수의 기본 정의를 가져오는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-138">The RetreiveDefaultDefinition endpoint helps you get the default definition for a scalar function that is bound to an Azure Machine Learning endpoint.</span></span> <span data-ttu-id="a123c-139">아래 페이로드는 Azure Machine Learning 끝점에 바인딩된 스칼라 함수의 기본 UDF 정의를 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-139">The payload below requires you to get the default UDF definition for a scalar function that is bound to an Azure Machine Learning endpoint.</span></span> <span data-ttu-id="a123c-140">PUT 요청 동안 이미 끝점이 제공되었기 때문에 실제 끝점을 지정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-140">It doesn’t specify the actual endpoint as it has already been provided during PUT request.</span></span> <span data-ttu-id="a123c-141">끝점이 명시적으로 제공되면 Stream Analytics는 요청에 제공된 끝점을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-141">Stream Analytics calls the endpoint provided in the request if it is provided explicitly.</span></span> <span data-ttu-id="a123c-142">그렇지 않으면 원래 참조하던 끝점을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-142">Otherwise it uses the one originally referenced.</span></span> <span data-ttu-id="a123c-143">다음 UDF는 단일 문자열 매개 변수(문장)를 가져와서 해당 문장에 대한 “sentiment” 레이블의 단일 문자열 형식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-143">Here the UDF takes a single string parameter (a sentence) and returns a single output of type string which indicates the “sentiment” label for that sentence.</span></span>

````
POST : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>/RetrieveDefaultDefinition?api-version=<apiVersion>
````

<span data-ttu-id="a123c-144">요청 본문 예제:</span><span class="sxs-lookup"><span data-stu-id="a123c-144">Example request body:</span></span>  

````
    {
        "bindingType": "Microsoft.MachineLearning/WebService",
        "bindingRetrievalProperties": {
            "executeEndpoint": null,
            "udfType": "Scalar"
        }
    }
````

<span data-ttu-id="a123c-145">이 샘플 출력은 아래와 비슷하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-145">A sample output of this would look something like below.</span></span>  

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

## <a name="patch-udf-with-the-response"></a><span data-ttu-id="a123c-146">응답과 함께 UDF 패치</span><span class="sxs-lookup"><span data-stu-id="a123c-146">Patch UDF with the response</span></span>
<span data-ttu-id="a123c-147">이제 아래와 같이 이전 응답과 함께 UDF를 패치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-147">Now the UDF must be patched with the previous response, as shown below.</span></span>

````
PATCH : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>
````

<span data-ttu-id="a123c-148">요청 본문(RetrieveDefaultDefinition):</span><span class="sxs-lookup"><span data-stu-id="a123c-148">Request Body (Output from RetrieveDefaultDefinition):</span></span>

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

## <a name="implement-stream-analytics-transformation-to-call-the-udf"></a><span data-ttu-id="a123c-149">UDF를 호출하는 Stream Analytics 변환 구현</span><span class="sxs-lookup"><span data-stu-id="a123c-149">Implement Stream Analytics transformation to call the UDF</span></span>
<span data-ttu-id="a123c-150">이제 모든 입력 이벤트에 대해 UDF(여기서는 scoreTweet)를 쿼리하고 해당 이벤트에 대한 응답을 출력으로 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123c-150">Now query the UDF (here named scoreTweet) for every input event and write a response for that event to an output.</span></span>  

````
    {
        "name": "transformation",
        "properties": {
            "streamingUnits": null,
            "query": "select *,scoreTweet(Tweet) TweetSentiment into blobOutput from blobInput"
        }
    }
````


## <a name="get-help"></a><span data-ttu-id="a123c-151">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="a123c-151">Get help</span></span>
<span data-ttu-id="a123c-152">추가 지원이 필요할 경우 [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="a123c-152">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="a123c-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a123c-153">Next steps</span></span>
* [<span data-ttu-id="a123c-154">Azure Stream Analytics 소개</span><span class="sxs-lookup"><span data-stu-id="a123c-154">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="a123c-155">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="a123c-155">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="a123c-156">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="a123c-156">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="a123c-157">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="a123c-157">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="a123c-158">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="a123c-158">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
