---
title: "6 단계: hello 컴퓨터 학습 웹 서비스에 액세스 | Microsoft Docs"
description: "예측 솔루션 연습을 개발 하는 hello의 6 단계: 활성 Azure 컴퓨터 학습 웹 서비스에 액세스 합니다."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a65c89a-40ab-4673-8dd8-8eee0a150e3b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 211de0294092c6a6b5e6eb608d5d3b88107674c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-6-access-hello-azure-machine-learning-web-service"></a><span data-ttu-id="fbecc-103">6 단계를 연습: hello Azure 기계 학습 웹 서비스에 액세스</span><span class="sxs-lookup"><span data-stu-id="fbecc-103">Walkthrough Step 6: Access hello Azure Machine Learning web service</span></span>

<span data-ttu-id="fbecc-104">이 hello 연습의 마지막 단계 hello [Azure 기계 학습에서 예측 분석 솔루션을 개발 합니다.](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="fbecc-104">This is hello last step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="fbecc-105">기계 학습 작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="fbecc-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="fbecc-106">기존 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="fbecc-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="fbecc-107">새 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="fbecc-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="fbecc-108">학습 하 고 hello 모델 평가</span><span class="sxs-lookup"><span data-stu-id="fbecc-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="fbecc-109">Hello 웹 서비스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbecc-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. <span data-ttu-id="fbecc-110">**Hello 웹 서비스에 액세스**</span><span class="sxs-lookup"><span data-stu-id="fbecc-110">**Access hello Web service**</span></span>

- - -
<span data-ttu-id="fbecc-111">이 연습에서는 hello 이전 단계에서 예제의 신용 위험 예측 모델을 사용 하는 웹 서비스를 배포 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fbecc-111">In hello previous step in this walkthrough we deployed a web service that uses our credit risk prediction model.</span></span> <span data-ttu-id="fbecc-112">이제 사용자의 수 toosend 데이터 tooit 및 결과 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbecc-112">Now users are able toosend data tooit and receive results.</span></span> 

<span data-ttu-id="fbecc-113">hello 웹 서비스는 Azure 웹 서비스 수신 하 고 REST Api를 사용 하 여 두 가지 방법 중 하나에서 데이터를 반환할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="fbecc-113">hello Web service is an Azure web service that can receive and return data using REST APIs in one of two ways:</span></span>  

* <span data-ttu-id="fbecc-114">**요청/응답** -hello 사용자 전송 하나 또는 신용 데이터 toohello 개 이상의 행 서비스는 HTTP 프로토콜을 사용 하 여 하나 이상의 결과 집합으로 서비스 응답 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbecc-114">**Request/Response** - hello user sends one or more rows of credit data toohello service by using an HTTP protocol, and hello service responds with one or more sets of results.</span></span>
* <span data-ttu-id="fbecc-115">**일괄 처리 실행** -hello 사용자 하나를 저장 하거나 Azure의 신용 데이터의 행을 더 blob hello blob 위치 toohello 서비스를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbecc-115">**Batch Execution** - hello user stores one or more rows of credit data in an Azure blob and then sends hello blob location toohello service.</span></span> <span data-ttu-id="fbecc-116">데이터 행을 모두 hello hello 서비스 점수 hello 입력된 blob, 저장소 hello 다른 blob에 대 한 결과 및 반환 hello 해당 컨테이너의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="fbecc-116">hello service scores all hello rows of data in hello input blob, stores hello results in another blob, and returns hello URL of that container.</span></span>  

<span data-ttu-id="fbecc-117">기본 웹 서비스는 hello를 통해 쉽고 빠르게 tooaccess hello [Azure ML 요청 응답 서비스 웹 앱](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) 또는 [Azure ML 일괄 처리 실행 서비스 웹 응용 프로그램 템플릿](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)합니다.</span><span class="sxs-lookup"><span data-stu-id="fbecc-117">hello quickest and easiest way tooaccess a Classic web service is through hello [Azure ML Request-Response Service Web App](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) or [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span></span>

<span data-ttu-id="fbecc-118">이러한 웹앱 템플릿은 웹 서비스의 입력 데이터 및 예상 결과를 알고 있는 사용자 지정 웹앱을 구축할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbecc-118">These web app templates can build a custom web app that knows your web service's input data and what it will return.</span></span> <span data-ttu-id="fbecc-119">하기만 하면 toodo 액세스 tooyour 웹 서비스 및 데이터를 제공 되며 hello 템플릿 rest hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fbecc-119">All you need toodo is provide access tooyour web service and data, and hello template does hello rest.</span></span>

<span data-ttu-id="fbecc-120">Hello 웹 응용 프로그램 템플릿을 사용 하 여에 대 한 자세한 내용은 참조 하십시오. [는 Azure 컴퓨터 학습 웹 서비스 웹 앱 템플릿 사용 하 여 사용할](machine-learning-consume-web-service-with-web-app-template.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fbecc-120">For more information on using hello web app templates, see [Consume an Azure Machine Learning Web service with a web app template](machine-learning-consume-web-service-with-web-app-template.md).</span></span>

<span data-ttu-id="fbecc-121">또한 R, C#, 및 Python 프로그래밍 언어에서 제공 하는 시작 코드를 사용 하 여 사용자 지정 응용 프로그램 tooaccess hello 웹 서비스를 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbecc-121">You can also develop a custom application tooaccess hello web service using starter code provided for you in R, C#, and Python programming languages.</span></span>

<span data-ttu-id="fbecc-122">전체 세부 정보를 찾을 수 있습니다 [어떻게 tooconsume Azure 컴퓨터 학습 웹 서비스](machine-learning-consume-web-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fbecc-122">You can find complete details in [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

