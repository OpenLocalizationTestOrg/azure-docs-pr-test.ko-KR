---
title: "Azure Machine Learning FAQ(질문과 대답) | Microsoft Docs"
description: "Azure 기계 학습 소개: 간소화된 예측 모델링에 대한 클라우드 서비스의 요금 청구, 기능 및 제한 사항을 다루는 FAQ."
keywords: "기계 학습 소개, 예측 모델링, 기계 학습이란 무엇인가요"
services: machine-learning
documentationcenter: 
author: garyericson
manager: paulettm
editor: cgronlun
ms.assetid: a4a32a06-dbed-4727-a857-c10da774ce66
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/02/2017
ms.author: garye
ms.openlocfilehash: 0a1e23cd52ab5c10791a11d93753b54eb1c1b71a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-machine-learning-frequently-asked-questions-billing-capabilities-limitations-and-support"></a><span data-ttu-id="9cda6-104">Azure Machine Learning 질문과 대답: 대금 청구, 기능, 제한 사항 및 지원</span><span class="sxs-lookup"><span data-stu-id="9cda6-104">Azure Machine Learning frequently asked questions: Billing, capabilities, limitations, and support</span></span>
<span data-ttu-id="9cda6-105">Azure Machine Learning, 예측 모델 개발을 위한 클라우드 서비스 및 웹 서비스를 통한 운용성 솔루션에 대한 질문(FAQ)과 해당하는 대답입니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-105">Here are some frequently asked questions (FAQs) and corresponding answers about Azure Machine Learning, a cloud service for developing predictive models and operationalizing solutions through web services.</span></span> <span data-ttu-id="9cda6-106">이 FAQ는 청구 모델, 기능, 제한 및 지원을 포함한 서비스 사용 방법에 대한 질문을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-106">These FAQs provide questions about how to use the service, which includes the billing model, capabilities, limitations, and support.</span></span>

<span data-ttu-id="9cda6-107">**여기에서 찾을 수 없는 질문이 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-107">**Have a question you can't find here?**</span></span>

<span data-ttu-id="9cda6-108">Azure Machine Learning은 데이터 과학 커뮤니티의 멤버가 Azure Machine Learning에 대한 질문을 할 수 있는 MSDN 포럼을 운영합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-108">Azure Machine Learning has a forum on MSDN where members of the data science community can ask questions about Azure Machine Learning.</span></span> <span data-ttu-id="9cda6-109">Azure Machine Learning 팀에서 포럼을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-109">The Azure Machine Learning team monitors the forum.</span></span> <span data-ttu-id="9cda6-110">답변을 검색하거나 새로운 질문을 게시하려면 [Azure Machine Learning 포럼](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning)으로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-110">Go to the [Azure Machine Learning Forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) to search for answers or to post a new question of your own.</span></span>

## <a name="general-questions"></a><span data-ttu-id="9cda6-111">일반적인 질문</span><span class="sxs-lookup"><span data-stu-id="9cda6-111">General questions</span></span>
<span data-ttu-id="9cda6-112">**Azure 기계 학습이란 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-112">**What is Azure Machine Learning?**</span></span>

<span data-ttu-id="9cda6-113">Azure 기계 학습은 완벽하게 관리되는 서비스로, 이 서비스를 통해 클라우드에 예측 분석 솔루션을 만들고, 테스트하고, 운영하고, 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-113">Azure Machine Learning is a fully managed service that you can use to create, test, operate, and manage predictive analytic solutions in the cloud.</span></span> <span data-ttu-id="9cda6-114">브라우저만 있으면 로그인하고 데이터를 업로드하고 즉시 기계 학습 실험을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-114">With only a browser, you can sign in, upload data, and immediately start machine-learning experiments.</span></span> <span data-ttu-id="9cda6-115">끌어서 놓기 예측 모델링, 모듈의 대형 팔레트 및 시작 템플릿의 라이브러리를 활용하면 일반적인 기계 학습 작업을 간단히, 빠르게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-115">Drag-and-drop predictive modeling, a large pallet of modules, and a library of starting templates make common machine-learning tasks simple and quick.</span></span> <span data-ttu-id="9cda6-116">자세한 내용은 [Azure 기계 학습 서비스 개요](https://azure.microsoft.com/services/machine-learning/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-116">For more information, see the [Azure Machine Learning service overview](https://azure.microsoft.com/services/machine-learning/).</span></span> <span data-ttu-id="9cda6-117">주요 용어 및 개념을 설명하는 기계 학습 소개는 [Azure Machine Learning 소개](machine-learning-what-is-machine-learning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-117">For an introduction to machine learning that explains key terminology and concepts, see [Introduction to Azure Machine Learning](machine-learning-what-is-machine-learning.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="9cda6-118">**기계 학습 스튜디오란 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-118">**What is Machine Learning Studio?**</span></span>

<span data-ttu-id="9cda6-119">Machine Learning Studio는 웹 브라우저를 사용하여 액세스하는 워크벤치 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-119">Machine Learning Studio is a workbench environment that you access by using a web browser.</span></span> <span data-ttu-id="9cda6-120">Machine Learning Studio는 실험 형태의 종단 간 데이터 과학 워크플로를 구성할 수 있는 시각적 컴퍼지션 인터페이스로 모듈 팔레트를 호스트합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-120">Machine Learning Studio hosts a pallet of modules in a visual composition interface that helps you build an end-to-end, data-science workflow in the form of an experiment.</span></span>

<span data-ttu-id="9cda6-121">기계 학습 스튜디오에 대한 자세한 내용은 [기계 학습 스튜디오란 무엇인가요?](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="9cda6-121">For more information about Machine Learning Studio, see [What is Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>

<span data-ttu-id="9cda6-122">**Azure 기계 학습 API 서비스란 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-122">**What is the Machine Learning API service?**</span></span>

<span data-ttu-id="9cda6-123">Machine Learning API 서비스를 통해 Machine Learning Studio에 기본 제공되는 것과 같은 예측 모델을 확장성 있는 내결함성 웹 서비스로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-123">The Machine Learning API service enables you to deploy predictive models, like those that are built into Machine Learning Studio, as scalable, fault-tolerant, web services.</span></span> <span data-ttu-id="9cda6-124">Machine Learning API 서비스로 만든 웹 서비스는, 외부 응용 프로그램과 예측 분석 모델 간의 통신용 인터페이스를 제공하는 REST API입니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-124">The web services that the Machine Learning API service creates are REST APIs that provide an interface for communication between external applications and your predictive analytics models.</span></span>

<span data-ttu-id="9cda6-125">자세한 내용은 [Azure Machine Learning 웹 서비스 사용 방법](machine-learning-consume-web-services.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-125">For more information, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

<span data-ttu-id="9cda6-126">**내 클래식 웹 서비스는 어디에 나열되나요? 내 새 Azure Resource Manager 기반 웹 서비스는 어디에 나열되나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-126">**Where are my Classic web services listed? Where are my New (Azure Resource Manager-based) web services listed?**</span></span>

<span data-ttu-id="9cda6-127">클래식 배포 모델을 사용하여 만든 웹 서비스와 새로운 Azure Resource Manager 배포 모델을 사용하여 만든 웹 서비스가 [Microsoft Azure Machine Learning 웹 서비스](https://services.azureml.net/) 포털에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-127">Web services created using the Classic deployment model and web services created using the New Azure Resource Manager deployment model are listed in the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/) portal.</span></span>

<span data-ttu-id="9cda6-128">또한 클래식 웹 서비스는 **웹 서비스** 탭의 [Machine Learning Studio](http://studio.azureml.net)에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-128">Classic web services are also listed in [Machine Learning Studio](http://studio.azureml.net) on the **Web services** tab.</span></span>

## <a name="azure-machine-learning-questions"></a><span data-ttu-id="9cda6-129">Azure Machine Learning 질문</span><span class="sxs-lookup"><span data-stu-id="9cda6-129">Azure Machine Learning questions</span></span>
<span data-ttu-id="9cda6-130">**Azure Machine Learning 웹 서비스란?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-130">**What are Azure Machine Learning web services?**</span></span>

<span data-ttu-id="9cda6-131">Machine Learning 웹 서비스는 응용 프로그램과 Machine Learning 워크플로 점수 매기기 모델 간의 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-131">Machine Learning web services provide an interface between an application and a Machine Learning workflow scoring model.</span></span> <span data-ttu-id="9cda6-132">외부 응용 프로그램에서 Azure Machine Learning을 사용하여 Machine Learning 워크플로 점수 매기기 모델과 실시간으로 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-132">An external application can use Azure Machine Learning to communicate with a Machine Learning workflow scoring model in real time.</span></span> <span data-ttu-id="9cda6-133">Machine Learning 웹 서비스에 대한 호출은 외부 응용 프로그램에 예측 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-133">A call to a Machine Learning web service returns prediction results to an external application.</span></span> <span data-ttu-id="9cda6-134">웹 서비스를 호출하려면 웹 서비스를 배포할 때 만들어진 API 키를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-134">To make a call to a web service, you pass an API key that was created when you deployed the web service.</span></span> <span data-ttu-id="9cda6-135">Machine Learning 웹 서비스는 웹 프로그래밍 프로젝트에 일반적으로 사용되는 아키텍처인 REST를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-135">A Machine Learning web service is based on REST, a popular architecture choice for web programming projects.</span></span>

<span data-ttu-id="9cda6-136">Azure Machine Learning에는 다음 두 가지 유형의 웹 서비스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-136">Azure Machine Learning has two types of web services:</span></span>

* <span data-ttu-id="9cda6-137">RRS(요청-응답 서비스): 대기 시간이 짧고 확장성 있는 서비스로, Machine Learning Studio를 사용하여 생성 및 배포되는 상태 비저장 모델에 대한 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-137">Request-Response Service (RRS): A low latency, highly scalable service that provides an interface to the stateless models created and deployed by using Machine Learning Studio.</span></span>
* <span data-ttu-id="9cda6-138">BES(일괄 처리 실행 서비스): 데이터 레코드의 점수를 일괄적으로 매기는 비동기 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-138">Batch Execution Service (BES): An asynchronous service that scores a batch for data records.</span></span>

<span data-ttu-id="9cda6-139">REST API를 사용하고 웹 서비스에 액세스하는 여러 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-139">There are several ways to consume the REST API and access the web service.</span></span> <span data-ttu-id="9cda6-140">예를 들어, 웹 서비스를 배포할 때 생성된 샘플 코드를 사용하여 C#, R 또는 Python에서 응용 프로그램을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-140">For example, you can write an application in C#, R, or Python by using the sample code that's generated for you when you deployed the web service.</span></span>

<span data-ttu-id="9cda6-141">샘플 코드는 다음에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-141">The sample code is available on:</span></span>
- <span data-ttu-id="9cda6-142">Azure Machine Learning 웹 서비스 포털에서 웹 서비스에 대한 사용 페이지</span><span class="sxs-lookup"><span data-stu-id="9cda6-142">The Consume page for the web service in the Azure Machine Learning Web Services portal</span></span>
- <span data-ttu-id="9cda6-143">Machine Learning Studio에서 웹 서비스 대시보드에서 API 도움말 페이지</span><span class="sxs-lookup"><span data-stu-id="9cda6-143">The API Help Page in the web service dashboard in Machine Learning Studio</span></span>

<span data-ttu-id="9cda6-144">사용자용으로 만들고 Machine Learning Studio의 웹 서비스 대시보드에서 사용 가능한 샘플 Microsoft Excel 통합 문서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-144">You can also use the sample Microsoft Excel workbook that's created for you and is available in the web service dashboard in Machine Learning Studio.</span></span>

<span data-ttu-id="9cda6-145">**Azure Machine Learning에 대한 주요 업데이트는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-145">**What are the main updates to Azure Machine Learning?**</span></span>

<span data-ttu-id="9cda6-146">최신 업데이트는 [Azure Machine Learning의 새로운 기능](machine-learning-whats-new.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-146">For the latest updates, see [What's new in Azure Machine Learning](machine-learning-whats-new.md).</span></span>

## <a name="machine-learning-studio-questions"></a><span data-ttu-id="9cda6-147">기계 학습 스튜디오 질문</span><span class="sxs-lookup"><span data-stu-id="9cda6-147">Machine Learning Studio questions</span></span>
### <a name="import-and-export-data-for-machine-learning"></a><span data-ttu-id="9cda6-148">Machine Learning에 대한 데이터 가져오기 및 내보내기</span><span class="sxs-lookup"><span data-stu-id="9cda6-148">Import and export data for Machine Learning</span></span>
<span data-ttu-id="9cda6-149">**기계 학습에서 지원하는 데이터 원본은 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-149">**What data sources does Machine Learning support?**</span></span>

<span data-ttu-id="9cda6-150">세 가지 방법으로 Machine Learning Studio 실험으로 데이터를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-150">You can download data to a Machine Learning Studio experiment in three ways:</span></span>

- <span data-ttu-id="9cda6-151">데이터 집합으로 로컬 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="9cda6-151">Upload a local file as a dataset</span></span>
- <span data-ttu-id="9cda6-152">모듈을 사용하여 클라우드 데이터 서비스에서 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="9cda6-152">Use a module to import data from cloud data services</span></span>
- <span data-ttu-id="9cda6-153">다른 실험에서 저장된 데이터 집합 가져오기</span><span class="sxs-lookup"><span data-stu-id="9cda6-153">Import a dataset saved from another experiment</span></span>

<span data-ttu-id="9cda6-154">지원된 파일 형식에 대한 자세한 내용은 [Machine Learning Studio로 학습 데이터 가져오기](machine-learning-data-science-import-data.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-154">To learn more about supported file formats, see [Import training data into Machine Learning Studio](machine-learning-data-science-import-data.md).</span></span>

#### <span data-ttu-id="9cda6-155"><a id="ModuleLimit"></a>모듈에 대해 설정할 수 있는 데이터 집합의 크기는 어느 정도인가요?</span><span class="sxs-lookup"><span data-stu-id="9cda6-155"><a id="ModuleLimit"></a>How large can the data set be for my modules?</span></span>
<span data-ttu-id="9cda6-156">기계 학습 스튜디오의 모듈은 일반적인 사용 사례의 경우 최대 10GB 숫자 데이터의 데이터 집합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-156">Modules in Machine Learning Studio support datasets of up to 10 GB of dense numerical data for common use cases.</span></span> <span data-ttu-id="9cda6-157">모듈에서 둘 이상의 입력을 사용하는 경우에는 모든 입력 크기의 합계 값이 10GB입니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-157">If a module takes more than one input, the 10 GB value is the total of all input sizes.</span></span> <span data-ttu-id="9cda6-158">Hive 또는 Azure SQL Database 쿼리를 사용하여 더 큰 데이터 집합을 샘플링하거나 수집하기 전에 Learning by Counts 전처리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-158">You can also sample larger datasets by using queries from Hive or Azure SQL Database, or you can use Learning by Counts preprocessing before ingestion.</span></span>  

<span data-ttu-id="9cda6-159">다음 데이터 형식은 기능 정규화 중에 확장할 수 있으며 10GB 미만으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-159">The following types of data can expand to larger datasets during feature normalization and are limited to less than 10 GB:</span></span>

* <span data-ttu-id="9cda6-160">스파스</span><span class="sxs-lookup"><span data-stu-id="9cda6-160">Sparse</span></span>
* <span data-ttu-id="9cda6-161">범주</span><span class="sxs-lookup"><span data-stu-id="9cda6-161">Categorical</span></span>
* <span data-ttu-id="9cda6-162">문자열</span><span class="sxs-lookup"><span data-stu-id="9cda6-162">Strings</span></span>
* <span data-ttu-id="9cda6-163">이진 데이터</span><span class="sxs-lookup"><span data-stu-id="9cda6-163">Binary data</span></span>

<span data-ttu-id="9cda6-164">다음 모듈은 10GB 미만의 데이터 집합으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-164">The following modules are limited to datasets less than 10 GB:</span></span>

* <span data-ttu-id="9cda6-165">Recommender 모듈</span><span class="sxs-lookup"><span data-stu-id="9cda6-165">Recommender modules</span></span>
* <span data-ttu-id="9cda6-166">SMOTE(Synthetic Minority Oversampling Technique) 모듈</span><span class="sxs-lookup"><span data-stu-id="9cda6-166">Synthetic Minority Oversampling Technique (SMOTE) module</span></span>
* <span data-ttu-id="9cda6-167">Scripting 모듈: R, Python, SQL</span><span class="sxs-lookup"><span data-stu-id="9cda6-167">Scripting modules: R, Python, SQL</span></span>
* <span data-ttu-id="9cda6-168">출력 데이터 크기가 입력 데이터 크기보다 클 수 있는 모듈(예: Join 또는 Feature Hashing)</span><span class="sxs-lookup"><span data-stu-id="9cda6-168">Modules where the output data size can be larger than input data size, such as Join or Feature Hashing</span></span>
* <span data-ttu-id="9cda6-169">Cross-validation, Tune Model Hyperparameters, Ordinal Regression 및 One-vs-All Multiclass(반복 횟수가 매우 많은 경우)</span><span class="sxs-lookup"><span data-stu-id="9cda6-169">Cross-validation, Tune Model Hyperparameters, Ordinal Regression, and One-vs-All Multiclass, when the number of iterations is very large</span></span>

#### <span data-ttu-id="9cda6-170"><a id="UploadLimit"></a>데이터 업로드에 대한 제한 사항은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="9cda6-170"><a id="UploadLimit"></a>What are the limits for data upload?</span></span>
<span data-ttu-id="9cda6-171">몇 GB보다 큰 데이터 집합의 경우 로컬 파일에서 직접 업로드하지 않고 Azure Storage 또는 Azure SQL Database에 데이터를 업로드하거나 Azure HDInsight를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-171">For datasets that are larger than a couple GBs, upload data to Azure Storage or Azure SQL Database, or use Azure HDInsight rather than directly uploading from a local file.</span></span>

<span data-ttu-id="9cda6-172">**Amazon S3에서 데이터를 읽을 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-172">**Can I read data from Amazon S3?**</span></span>

<span data-ttu-id="9cda6-173">소량의 데이터를 HTTP URL을 통해 노출하려는 경우 [데이터 가져오기][import-data] 모듈을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-173">If you have a small amount of data and want to expose it via an HTTP URL, then you can use the [Import Data][import-data] module.</span></span> <span data-ttu-id="9cda6-174">전송할 데이터가 많은 경우에는 먼저 Azure Storage로 전송한 다음 [데이터 가져오기][import-data] 모듈을 사용하여 실험으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-174">For larger amounts of data, transfer it to Azure Storage first, and then use the [Import Data][import-data] module to bring it into your experiment.</span></span>
<!--

<SEE CLOUD DS PROCESS>
-->

<span data-ttu-id="9cda6-175">**기본 제공 이미지 입력 기능이 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-175">**Is there a built-in image input capability?**</span></span>

<span data-ttu-id="9cda6-176">이미지 입력 기능은 [이미지 가져오기][image-reader] 참조에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-176">You can learn about image input capability in the [Import Images][image-reader] reference.</span></span>

### <a name="modules"></a><span data-ttu-id="9cda6-177">모듈</span><span class="sxs-lookup"><span data-stu-id="9cda6-177">Modules</span></span>
<span data-ttu-id="9cda6-178">**원하는 알고리즘, 데이터 원본, 데이터 형식, 데이터 변환 작업이 Azure Machine Learning Studio에 없습니다. 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-178">**The algorithm, data source, data format, or data transformation operation that I am looking for isn't in Azure Machine Learning Studio. What are my options?**</span></span>

<span data-ttu-id="9cda6-179">[사용자 피드백 포럼](http://go.microsoft.com/fwlink/?LinkId=404231)으로 이동하여 Microsoft에서 추적 중인 기능 요청을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-179">You can go to the [user feedback forum](http://go.microsoft.com/fwlink/?LinkId=404231) to see feature requests that we are tracking.</span></span> <span data-ttu-id="9cda6-180">원하는 기능이 이미 요청된 경우 해당 요청에 투표할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-180">Add your vote to a request if a capability that you're looking for has already been requested.</span></span> <span data-ttu-id="9cda6-181">원하는 기능이 없는 경우 새로운 요청을 만드세요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-181">If the capability that you're looking for doesn't exist, create a new request.</span></span> <span data-ttu-id="9cda6-182">이 포럼에서 요청의 상태를 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-182">You can view the status of your request in this forum, too.</span></span> <span data-ttu-id="9cda6-183">Microsoft는 이 목록을 긴밀하게 추적하여 기능의 사용 가능성 상태를 자주 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-183">We track this list closely and update the status of feature availability frequently.</span></span> <span data-ttu-id="9cda6-184">R 및 Python에 대한 기본적인 지원 외에 필요에 따라 사용자 지정 변환을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-184">In addition, you can use the built-in support for R and Python to create custom transformations when needed.</span></span>

<span data-ttu-id="9cda6-185">**기존 코드를 기계 학습 스튜디오로 가져올 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-185">**Can I bring my existing code into Machine Learning Studio?**</span></span>

<span data-ttu-id="9cda6-186">예, 기계 학습 스튜디오로 기존 R 또는 Python 코드를 가져와서, Azure 기계 학습 학습자와 동일한 실험에서 실행하고 Azure 기계 학습을 통해 솔루션을 웹 서비스로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-186">Yes, you can bring your existing R or Python code into Machine Learning Studio, run it in the same experiment with Azure Machine Learning learners, and deploy the solution as a web service via Azure Machine Learning.</span></span> <span data-ttu-id="9cda6-187">자세한 내용은 [R을 사용하여 실험 확장](machine-learning-extend-your-experiment-with-r.md) 및 [Azure Machine Learning Studio에서 Python 기계 학습 스크립트 실행](machine-learning-execute-python-scripts.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-187">For more information, see [Extend your experiment with R](machine-learning-extend-your-experiment-with-r.md) and [Execute Python machine learning scripts in Azure Machine Learning Studio](machine-learning-execute-python-scripts.md).</span></span>

<span data-ttu-id="9cda6-188">**[PMML](http://en.wikipedia.org/wiki/Predictive_Model_Markup_Language)과 유사한 기능을 사용하여 모델을 정의할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-188">**Is it possible to use something like [PMML](http://en.wikipedia.org/wiki/Predictive_Model_Markup_Language) to define a model?**</span></span>

<span data-ttu-id="9cda6-189">아니요, PMML(Predictive Model Markup Language)은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-189">No, Predictive Model Markup Language (PMML) is not supported.</span></span> <span data-ttu-id="9cda6-190">모듈을 정의하려면 사용자 지정 R 및 Python 코드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-190">You can use custom R and Python code to define a module.</span></span>

<span data-ttu-id="9cda6-191">**실험에서 병렬로 실행할 수 있는 모듈은 몇 개인가요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-191">**How many modules can I execute in parallel in my experiment?**</span></span>  

<span data-ttu-id="9cda6-192">실험에서 동시에 최대 네 개의 모듈을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-192">You can execute up to four modules in parallel in an experiment.</span></span>

### <a name="data-processing"></a><span data-ttu-id="9cda6-193">데이터 처리</span><span class="sxs-lookup"><span data-stu-id="9cda6-193">Data processing</span></span>
<span data-ttu-id="9cda6-194">**실험 내에서 대화형으로 데이터를 시각화하는 기능(R 시각화 외)이 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-194">**Is there an ability to visualize data (beyond R visualizations) interactively within the experiment?**</span></span>

<span data-ttu-id="9cda6-195">모듈의 출력을 클릭하여 데이터를 시각화하고 통계를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-195">Click the output of a module to visualize the data and get statistics.</span></span>

<span data-ttu-id="9cda6-196">**브라우저에서 결과 또는 데이터를 미리 볼 때 행 및 열 수가 제한됩니다. 그 이유는 무엇일까요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-196">**When previewing results or data in a browser, the number of rows and columns is limited. Why?**</span></span>

<span data-ttu-id="9cda6-197">많은 양의 데이터를 브라우저에 전송할 수 있으므로 Machine Learning Studio의 속도 저하를 방지하기 위해 데이터 크기가 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-197">Because large amounts of data might be sent to a browser, data size is limited to prevent slowing down Machine Learning Studio.</span></span> <span data-ttu-id="9cda6-198">모든 데이터/결과를 시각화하려면, 데이터를 다운로드하고 Excel 또는 다른 도구를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-198">To visualize all the data/results, it's better to download the data and use Excel or another tool.</span></span>

### <a name="algorithms"></a><span data-ttu-id="9cda6-199">알고리즘</span><span class="sxs-lookup"><span data-stu-id="9cda6-199">Algorithms</span></span>
<span data-ttu-id="9cda6-200">**기계 학습 스튜디오에서 지원되는 기존 기계 학습 알고리즘은 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-200">**What existing algorithms are supported in Machine Learning Studio?**</span></span>

<span data-ttu-id="9cda6-201">Machine Learning Studio는 Microsoft Research에서 개발된 확장 가능한 고급 의사 결정 트리, Bayesian 권장 시스템, 심층적인 신경망, 의사 결정 정글 등 최신 알고리즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-201">Machine Learning Studio provides state-of-the-art algorithms, such as Scalable Boosted Decision trees, Bayesian Recommendation systems, Deep Neural Networks, and Decision Jungles developed at Microsoft Research.</span></span> <span data-ttu-id="9cda6-202">Vowpal Wabbit과 같은 확장성 있는 오픈 소스 기계 학습 패키지도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-202">Scalable open-source machine learning packages, like Vowpal Wabbit, are also included.</span></span> <span data-ttu-id="9cda6-203">기계 학습 스튜디오는 여러 클래스의 이진 분류, 회귀 및 클러스터링을 위한 기계 학습 알고리즘을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-203">Machine Learning Studio supports machine learning algorithms for multiclass and binary classification, regression, and clustering.</span></span> <span data-ttu-id="9cda6-204">전체 목록은 [Machine Learning 모듈][machine-learning-modules]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-204">See the complete list of [Machine Learning Modules][machine-learning-modules].</span></span>

<span data-ttu-id="9cda6-205">**데이터에 사용할 올바른 기계 학습 알고리즘이 자동으로 제안되나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-205">**Do you automatically suggest the right Machine Learning algorithm to use for my data?**</span></span>

<span data-ttu-id="9cda6-206">아니요, 그러나 Machine Learning Studio에서 각 알고리즘의 결과를 비교하여 문제에 적합한 알고리즘을 확인할 수 있는 다양한 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-206">No, but Machine Learning Studio has various ways to compare the results of each algorithm to determine the right one for your problem.</span></span>

<span data-ttu-id="9cda6-207">**제공된 알고리즘에서 적합한 알고리즘 하나를 선택하는 데 대한 지침이 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-207">**Do you have any guidelines on picking one algorithm over another for the provided algorithms?**</span></span>

<span data-ttu-id="9cda6-208">[알고리즘을 선택하는 방법](machine-learning-algorithm-choice.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-208">See [How to choose an algorithm](machine-learning-algorithm-choice.md).</span></span>

<span data-ttu-id="9cda6-209">**제공되는 알고리즘은 R 또는 Python으로 작성되었나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-209">**Are the provided algorithms written in R or Python?**</span></span>

<span data-ttu-id="9cda6-210">아니요, 이러한 알고리즘은 더 나은 성능을 제공하기 위해 주로 컴파일된 언어로 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-210">No, these algorithms are mostly written in compiled languages to provide better performance.</span></span>

<span data-ttu-id="9cda6-211">**제공되는 알고리즘에 대한 세부 정보가 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-211">**Are any details of the algorithms provided?**</span></span>

<span data-ttu-id="9cda6-212">설명서에는 알고리즘에 대한 일부 정보가 나와 있으며, 용도에 맞게 알고리즘을 최적화할 수 있도록 조정할 매개 변수에 대한 설명이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-212">The documentation provides some information about the algorithms and parameters for tuning are described to optimize the algorithm for your use.</span></span>  

<span data-ttu-id="9cda6-213">**온라인 학습을 지원하나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-213">**Is there any support for online learning?**</span></span>

<span data-ttu-id="9cda6-214">아니요, 현재는 프로그래밍 방식의 재학습만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-214">No, currently only programmatic retraining is supported.</span></span>

<span data-ttu-id="9cda6-215">**기본 제공 모듈을 사용하여 신경망 모델의 계층을 시각화할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-215">**Can I visualize the layers of a Neural Net Model by using the built-in module?**</span></span>

<span data-ttu-id="9cda6-216">아니요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-216">No.</span></span>

<span data-ttu-id="9cda6-217">**C# 또는 일부 다른 언어로 모듈을 만들 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-217">**Can I create my own modules in C# or some other language?**</span></span>

<span data-ttu-id="9cda6-218">현재는 R을 사용해서만 새 사용자 지정 모듈을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-218">Currently, you can only use R to create new custom modules.</span></span>

### <a name="r-module"></a><span data-ttu-id="9cda6-219">R 모듈</span><span class="sxs-lookup"><span data-stu-id="9cda6-219">R module</span></span>
<span data-ttu-id="9cda6-220">**기계 학습 스튜디오에서 사용 가능한 R 패키지는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-220">**What R packages are available in Machine Learning Studio?**</span></span>

<span data-ttu-id="9cda6-221">Machine Learning Studio는 현재 400개가 넘는 CRAN R 패키지를 지원하며 다음은 모든 포함된 패키지의 [현재 목록](http://az754797.vo.msecnd.net/docs/RPackages.xlsx) 입니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-221">Machine Learning Studio supports more than 400 CRAN R packages today, and here is the [current list](http://az754797.vo.msecnd.net/docs/RPackages.xlsx) of all included packages.</span></span> <span data-ttu-id="9cda6-222">이 목록을 직접 검색하는 방법에 대해 알아보려면 [R을 사용하여 실험 확장](machine-learning-extend-your-experiment-with-r.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-222">Also, see [Extend your experiment with R](machine-learning-extend-your-experiment-with-r.md) to learn how to retrieve this list yourself.</span></span> <span data-ttu-id="9cda6-223">원하는 패키지가 이 목록에 없는 경우 [사용자 피드백 포럼](http://go.microsoft.com/fwlink/?LinkId=404231)에서 패키지 이름을 제공해 주세요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-223">If the package that you want is not in this list, provide the name of the package at the [user feedback forum](http://go.microsoft.com/fwlink/?LinkId=404231).</span></span>

<span data-ttu-id="9cda6-224">**사용자 지정 R 모듈을 빌드할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-224">**Is it possible to build a custom R module?**</span></span>

<span data-ttu-id="9cda6-225">예, 자세한 내용은 [Azure 기계 학습에서 사용자 지정 R 모듈 작성](machine-learning-custom-r-modules.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-225">Yes, see [Author custom R modules in Azure Machine Learning](machine-learning-custom-r-modules.md) for more information.</span></span>

<span data-ttu-id="9cda6-226">**R에 대한 REPL 환경이 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-226">**Is there a REPL environment for R?**</span></span>

<span data-ttu-id="9cda6-227">아니요, R에 대한 REPL(Read-Eval-Print-Loop) 환경은 스튜디오에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-227">No, there is no Read-Eval-Print-Loop (REPL) environment for R in the studio.</span></span>

### <a name="python-module"></a><span data-ttu-id="9cda6-228">Python 모듈</span><span class="sxs-lookup"><span data-stu-id="9cda6-228">Python module</span></span>
<span data-ttu-id="9cda6-229">**사용자 지정 Python 모듈을 빌드할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-229">**Is it possible to build a custom Python module?**</span></span>

<span data-ttu-id="9cda6-230">현재는 안 되지만, 하나 이상의 [Python 스크립트 실행][python] 모듈을 사용하여 동일한 결과를 낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-230">Not currently, but you can use one or more [Execute Python Script][python] modules to get the same result.</span></span>

<span data-ttu-id="9cda6-231">**Python에 대한 REPL 환경이 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-231">**Is there a REPL environment for Python?**</span></span>

<span data-ttu-id="9cda6-232">기계 학습 스튜디오에서 Jupyter 노트북을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-232">You can use the Jupyter Notebooks in Machine Learning Studio.</span></span> <span data-ttu-id="9cda6-233">자세한 내용은 [Azure Machine Learning Studio에 Jupyter 노트북 도입](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-233">For more information, see [Introducing Jupyter Notebooks in Azure Machine Learning Studio](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span></span>

## <a name="web-service"></a><span data-ttu-id="9cda6-234">웹 서비스</span><span class="sxs-lookup"><span data-stu-id="9cda6-234">Web service</span></span>
### <a name="retrain"></a><span data-ttu-id="9cda6-235">다시 학습</span><span class="sxs-lookup"><span data-stu-id="9cda6-235">Retrain</span></span>
<span data-ttu-id="9cda6-236">**Azure Machine Learning 모델 프로그래밍 방식을 다시 학습하려면 어떻게 하나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-236">**How do I retrain Azure Machine Learning models programmatically?**</span></span>

<span data-ttu-id="9cda6-237">API 다시 학습을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-237">Use the retraining APIs.</span></span> <span data-ttu-id="9cda6-238">자세한 내용은 [프로그래밍 방식으로 기계 학습 모델 다시 학습](machine-learning-retrain-models-programmatically.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-238">For more information, see [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> <span data-ttu-id="9cda6-239">샘플 코드는 [Microsoft Azure Machine Learning 다시 학습 데모](https://azuremlretrain.codeplex.com/)에서도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-239">Sample code is also available in the [Microsoft Azure Machine Learning Retraining Demo](https://azuremlretrain.codeplex.com/).</span></span>

### <a name="create"></a><span data-ttu-id="9cda6-240">생성</span><span class="sxs-lookup"><span data-stu-id="9cda6-240">Create</span></span>
<span data-ttu-id="9cda6-241">**모델을 로컬로 배포하거나 인터넷에 연결하지 않고 응용 프로그램에서 배포할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-241">**Can I deploy the model locally or in an application that doesn't have an Internet connection?**</span></span>

<span data-ttu-id="9cda6-242">아니요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-242">No.</span></span>

<span data-ttu-id="9cda6-243">**모든 웹 서비스에 예상되는 기준 대기 시간이 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-243">**Is there a baseline latency that is expected for all web services?**</span></span>

<span data-ttu-id="9cda6-244">[Azure 구독 제한](../azure-subscription-service-limits.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-244">See the [Azure subscription limits](../azure-subscription-service-limits.md).</span></span>

### <a name="use"></a><span data-ttu-id="9cda6-245">사용</span><span class="sxs-lookup"><span data-stu-id="9cda6-245">Use</span></span>
<span data-ttu-id="9cda6-246">**어떤 경우에 내 예측 모델을 일괄 처리 실행 서비스로 실행하고 어떤 경우에 요청-응답 웹 서비스를 실행하나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-246">**When would I want to run my predictive model as a Batch Execution service versus a Request Response service?**</span></span>

<span data-ttu-id="9cda6-247">RRS(요청-응답 서비스)는 대기 시간이 짧고, 확장성이 높은 웹 서비스로, 실험 환경에서 생성하여 배포하는 상태 비저장 모델에 대한 인터페이스를 제공하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-247">The Request Response service (RRS) is a low-latency, high-scale web service that is used to provide an interface to stateless models that are created and deployed from the experimentation environment.</span></span> <span data-ttu-id="9cda6-248">BES(일괄 처리 실행 서비스)는 데이터 레코드의 배치에 대한 점수를 비동기적으로 계산하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-248">The Batch Execution service (BES) is a service that asynchronously scores a batch of data records.</span></span> <span data-ttu-id="9cda6-249">BES에 대한 입력은 RRS에서 사용하는 데이터 입력과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-249">The input for BES is like data input that RRS uses.</span></span> <span data-ttu-id="9cda6-250">가장 중요한 차이는 BES에서는 Azure Blob Storage 및 Azure Table Storage, Azure SQL Database, HDInsight(Hive 쿼리), HTTP 소스 등의 다양한 소스에서 레코드 블록을 읽는다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-250">The main difference is that BES reads a block of records from a variety of sources, such as Azure Blob storage, Azure Table storage, Azure SQL Database, HDInsight (hive query), and HTTP sources.</span></span> <span data-ttu-id="9cda6-251">자세한 내용은 [Azure Machine Learning 웹 서비스 사용 방법](machine-learning-consume-web-services.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-251">For more information, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

<span data-ttu-id="9cda6-252">**배포된 웹 서비스의 모델을 업데이트하려면 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-252">**How do I update the model for the deployed web service?**</span></span>

<span data-ttu-id="9cda6-253">이미 배포된 서비스의 예측 모델을 업데이트하려면 학습된 모델을 작성하여 저장하는 데 사용된 실험을 수정하고 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-253">To update a predictive model for an already deployed service, modify and rerun the experiment that you used to author and save the trained model.</span></span> <span data-ttu-id="9cda6-254">새 버전의 학습된 모델이 확보된 후에는, Machine Learning Studio에서 웹 서비스를 업데이트할지 여부를 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-254">After you have a new version of the trained model available, Machine Learning Studio asks you if you want to update your web service.</span></span> <span data-ttu-id="9cda6-255">배포된 웹 서비스를 업데이트하는 방법에 대한 자세한 내용은 [Machine Learning 웹 서비스 배포](machine-learning-publish-a-machine-learning-web-service.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-255">For details about how to update a deployed web service, see [Deploy a Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="9cda6-256">다시 학습 API도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-256">You can also use the Retraining APIs.</span></span>
<span data-ttu-id="9cda6-257">자세한 내용은 [프로그래밍 방식으로 기계 학습 모델 다시 학습](machine-learning-retrain-models-programmatically.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-257">For more information, see [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> <span data-ttu-id="9cda6-258">샘플 코드는 [Microsoft Azure Machine Learning 다시 학습 데모](https://azuremlretrain.codeplex.com/)에서도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-258">Sample code is also available in the [Microsoft Azure Machine Learning Retraining Demo](https://azuremlretrain.codeplex.com/).</span></span>

<span data-ttu-id="9cda6-259">**프로덕션에 배포된 웹 서비스를 모니터링하려면 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-259">**How do I monitor my web service deployed in production?**</span></span>

<span data-ttu-id="9cda6-260">예측 모델을 배포한 후에는 Azure 클래식 포털(기본 웹 서비스에만 해당) 또는 Azure Machine Learning 웹 서비스 포털에서 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-260">After you deploy a predictive model, you can monitor it from the Azure classic portal (Classic web services only) or the Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="9cda6-261">배포된 각 서비스에는 고유한 대시보드가 있어, 이 대시보드에서 해당 서비스에 대한 모니터링 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-261">Each deployed service has its own dashboard where you can see monitoring information for that service.</span></span> <span data-ttu-id="9cda6-262">배포된 웹 서비스를 관리하는 방법에 대한 자세한 내용은 [Azure Machine Learning 웹 서비스 포털을 사용하여 웹 서비스 관리](machine-learning-manage-new-webservice.md) 및 [Azure Machine Learning 작업 영역 관리](machine-learning-manage-workspace.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-262">For more information about how to manage your deployed web services, see [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md) and [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md).</span></span>

<span data-ttu-id="9cda6-263">**RRS/BES의 출력을 볼 수 있는 곳이 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-263">**Is there a place where I can see the output of my RRS/BES?**</span></span>

<span data-ttu-id="9cda6-264">RRS의 경우 웹 서비스 응답은 일반적으로 결과를 보는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-264">For RRS, the web service response is typically where you see the result.</span></span> <span data-ttu-id="9cda6-265">Azure Blob Storage에 기록도 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-265">You can also write it to Azure Blob storage.</span></span> <span data-ttu-id="9cda6-266">BES의 경우 기본적으로 출력은 Blob에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-266">For BES, the output is written to a blob by default.</span></span> <span data-ttu-id="9cda6-267">[데이터 내보내기][export-data] 모듈을 사용하여 출력을 데이터베이스 또는 테이블에 기록할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-267">You can also write the output to a database or table by using the [Export Data][export-data] module.</span></span>

<span data-ttu-id="9cda6-268">**Machine Learning Studio에서 만든 모델에서만 웹 서비스를 만들 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-268">**Can I create web services only from models that were created in Machine Learning Studio?**</span></span>

<span data-ttu-id="9cda6-269">아니요. Jupyter Notebook 및 RStudio를 사용하여 직접 웹 서비스를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-269">No, you can also create web services directly by using Jupyter Notebooks and RStudio.</span></span>

<span data-ttu-id="9cda6-270">**오류 코드에 대한 정보를 어디서 찾을 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-270">**Where can I find information about error codes?**</span></span>

<span data-ttu-id="9cda6-271">오류 코드 목록 및 설명은 [Machine Learning 모듈 오류 코드](https://msdn.microsoft.com/library/azure/dn905910.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-271">See [Machine Learning Module Error Codes](https://msdn.microsoft.com/library/azure/dn905910.aspx) for a list of error codes and descriptions.</span></span>

## <a name="scalability"></a><span data-ttu-id="9cda6-272">확장성</span><span class="sxs-lookup"><span data-stu-id="9cda6-272">Scalability</span></span>
<span data-ttu-id="9cda6-273">**웹 서비스의 확장성이란 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-273">**What is the scalability of the web service?**</span></span>

<span data-ttu-id="9cda6-274">현재 기본 끝점은 끝점당 20개의 동시 RRS 요청으로 프로비전됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-274">Currently, the default endpoint is provisioned with 20 concurrent RRS requests per endpoint.</span></span> <span data-ttu-id="9cda6-275">[웹 서비스 확장](machine-learning-scaling-webservice.md)에 설명된 것처럼 끝점당 동시 요청 수를 200개까지 확장할 수 있으며 웹 서비스당 10,000개 끝점으로 각 웹 서비스를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-275">You can scale this to 200 concurrent requests per endpoint, and you can scale each web service to 10,000 endpoints per web service as described in [Scaling a Web Service](machine-learning-scaling-webservice.md).</span></span> <span data-ttu-id="9cda6-276">BES의 경우 각 끝점은 한 번에 40개의 요청을 처리할 수 있으며 40개를 초과하는 추가 요청은 큐에 대기됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-276">For BES, each endpoint can process 40 requests at a time, and additional requests beyond 40 requests are queued.</span></span> <span data-ttu-id="9cda6-277">이러한 큐에 대기 중인 요청은 큐에서 나옴과 동시에 자동으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-277">These queued requests run automatically as the queue drains.</span></span>

<span data-ttu-id="9cda6-278">**R 작업은 노드 간에 분산되나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-278">**Are R jobs spread across nodes?**</span></span>

<span data-ttu-id="9cda6-279">번호</span><span class="sxs-lookup"><span data-stu-id="9cda6-279">No.</span></span>  

<span data-ttu-id="9cda6-280">**학습에 사용할 수 있는 데이터의 양은 얼마인가요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-280">**How much data can I use for training?**</span></span>

<span data-ttu-id="9cda6-281">기계 학습 스튜디오의 모듈은 일반적인 사용 사례의 경우 최대 10GB 숫자 데이터의 데이터 집합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-281">Modules in Machine Learning Studio support datasets of up to 10 GB of dense numerical data for common use cases.</span></span> <span data-ttu-id="9cda6-282">모듈에서 둘 이상의 입력을 사용하는 경우에는 모든 입력에 대한 총 크기가 10GB입니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-282">If a module takes more than one input, the total size for all inputs is 10 GB.</span></span> <span data-ttu-id="9cda6-283">Hive 쿼리 또는 Azure SQL Database 쿼리를 통하거나 수집 전에 [개수로 알아보기][counts] 모듈로 전처리하여 더 큰 데이터 집합을 샘플링할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-283">You can also sample larger datasets via Hive queries, via Azure SQL Database queries, or by preprocessing with [Learning with Counts][counts] modules before ingestion.</span></span>  

<span data-ttu-id="9cda6-284">다음 데이터 형식은 기능 정규화 중에 확장할 수 있으며 10GB 미만으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-284">The following types of data can expand to larger datasets during feature normalization and are limited to less than 10 GB:</span></span>

* <span data-ttu-id="9cda6-285">스파스</span><span class="sxs-lookup"><span data-stu-id="9cda6-285">Sparse</span></span>
* <span data-ttu-id="9cda6-286">범주</span><span class="sxs-lookup"><span data-stu-id="9cda6-286">Categorical</span></span>
* <span data-ttu-id="9cda6-287">문자열</span><span class="sxs-lookup"><span data-stu-id="9cda6-287">Strings</span></span>
* <span data-ttu-id="9cda6-288">이진 데이터</span><span class="sxs-lookup"><span data-stu-id="9cda6-288">Binary data</span></span>

<span data-ttu-id="9cda6-289">다음 모듈은 10GB 미만의 데이터 집합으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-289">The following modules are limited to datasets less than 10 GB:</span></span>

* <span data-ttu-id="9cda6-290">Recommender 모듈</span><span class="sxs-lookup"><span data-stu-id="9cda6-290">Recommender modules</span></span>
* <span data-ttu-id="9cda6-291">SMOTE(Synthetic Minority Oversampling Technique) 모듈</span><span class="sxs-lookup"><span data-stu-id="9cda6-291">Synthetic Minority Oversampling Technique (SMOTE) module</span></span>
* <span data-ttu-id="9cda6-292">Scripting 모듈: R, Python, SQL</span><span class="sxs-lookup"><span data-stu-id="9cda6-292">Scripting modules: R, Python, SQL</span></span>
* <span data-ttu-id="9cda6-293">출력 데이터 크기가 입력 데이터 크기보다 클 수 있는 모듈(예: Join 또는 Feature Hashing)</span><span class="sxs-lookup"><span data-stu-id="9cda6-293">Modules where the output data size can be larger than input data size, such as Join or Feature Hashing</span></span>
* <span data-ttu-id="9cda6-294">Cross-Validate, Tune Model Hyperparameters, Ordinal Regression 및 One-vs-All Multiclass(반복 횟수가 매우 많은 경우)</span><span class="sxs-lookup"><span data-stu-id="9cda6-294">Cross-Validate, Tune Model Hyperparameters, Ordinal Regression, and One-vs-All Multiclass, when number of iterations is very large</span></span>

<span data-ttu-id="9cda6-295">몇 GB보다 큰 데이터 집합의 경우 로컬 파일에서 직접 업로드하지 않고 Azure Storage 또는 Azure SQL Database에 데이터를 업로드하거나 HDInsight를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-295">For datasets that are larger than a few GBs, upload data to Azure Storage or Azure SQL Database, or use HDInsight rather than directly uploading from a local file.</span></span>

<span data-ttu-id="9cda6-296">**벡터 크기 제한이 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-296">**Are there any vector size limitations?**</span></span>

<span data-ttu-id="9cda6-297">행 및 열은 각각 .NET 제한인 Max Int: 2,147,483,647로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-297">Rows and columns are each limited to the .NET limitation of Max Int: 2,147,483,647.</span></span>

<span data-ttu-id="9cda6-298">**웹 서비스를 실행하는 가상 컴퓨터의 크기를 조정할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-298">**Can I adjust the size of the virtual machine that runs the web service?**</span></span>

<span data-ttu-id="9cda6-299">아니요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-299">No.</span></span>  

## <a name="security-and-availability"></a><span data-ttu-id="9cda6-300">보안 및 사용 가능성</span><span class="sxs-lookup"><span data-stu-id="9cda6-300">Security and availability</span></span>
<span data-ttu-id="9cda6-301">**웹 서비스에 대한 http 끝점에 기본적으로 액세스할 수 있는 사람은 누구인가요? 끝점에 대한 액세스는 어떻게 제한하나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-301">**Who can access the http endpoint for the web service by default? How do I restrict access to the endpoint?**</span></span>

<span data-ttu-id="9cda6-302">웹 서비스가 배포된 후 해당 서비스에 대한 기본 끝점이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-302">After a web service is deployed, a default endpoint is created for that service.</span></span> <span data-ttu-id="9cda6-303">기본 끝점은 API 키를 사용하여 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-303">The default endpoint can be called by using its API key.</span></span> <span data-ttu-id="9cda6-304">Azure 클래식 포털에서 또는 웹 서비스 관리 API를 사용하여 프로그래밍 방식으로 해당 고유 키로 끝점을 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-304">You can add more endpoints with their own keys from the Azure classic portal or programmatically by using the Web Service Management APIs.</span></span> <span data-ttu-id="9cda6-305">액세스 키는 웹 서비스를 호출하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-305">Access keys are needed to make calls to the web service.</span></span> <span data-ttu-id="9cda6-306">자세한 내용은 [Azure Machine Learning 웹 서비스 사용 방법](machine-learning-consume-web-services.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-306">For more information, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

<span data-ttu-id="9cda6-307">**내 Azure Storage 계정을 찾을 수 없는 경우 어떻게 되나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-307">**What happens if my Azure storage account can't be found?**</span></span>

<span data-ttu-id="9cda6-308">Machine Learning Studio는 워크플로를 실행할 때 사용자가 제공한 Azure Storage 계정을 기반으로 중간 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-308">Machine Learning Studio relies on a user-supplied Azure storage account to save intermediary data when it executes the workflow.</span></span> <span data-ttu-id="9cda6-309">이 저장소 계정은 작업 영역을 만들 때 Machine Learning Studio에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-309">This storage account is provided to Machine Learning Studio when a workspace is created.</span></span> <span data-ttu-id="9cda6-310">작업 영역을 만든 후 저장소 계정이 삭제되고 더 이상 찾을 수 없는 경우에는 해당 작업 영역의 작동이 중지되고 작업 영역의 모든 실험이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-310">After the workspace is created, if the storage account is deleted and can no longer be found, the workspace will stop functioning, and all experiments in that workspace will fail.</span></span>

<span data-ttu-id="9cda6-311">저장소 계정을 실수로 삭제한 경우 삭제한 저장소 계정과 동일한 지역과 동일한 이름으로 저장소 계정을 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-311">If you accidentally deleted the storage account, recreate the storage account with the same name in the same region as the deleted storage account.</span></span> <span data-ttu-id="9cda6-312">그 후 액세스 키를 다시 동기화하세요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-312">After that, resync the access key.</span></span>

<span data-ttu-id="9cda6-313">**저장소 계정 액세스 키가 동기화되지 않은 경우 어떻게 되나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-313">**What happens if my storage account access key is out of sync?**</span></span>

<span data-ttu-id="9cda6-314">Machine Learning Studio는 워크플로를 실행할 때 사용자가 제공한 Azure Storage 계정을 기반으로 중간 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-314">Machine Learning Studio relies on a user-supplied Azure storage account to store intermediary data when it executes the workflow.</span></span> <span data-ttu-id="9cda6-315">이 저장소 계정은 작업 영역을 만들 때 Machine Learning Studio에 제공되고 액세스 키가 해당 작업 영역과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-315">This storage account is provided to Machine Learning Studio when a workspace is created, and the access keys are associated with that workspace.</span></span> <span data-ttu-id="9cda6-316">액세스 키가 변경되면 작업 영역이 만들어진 후에 작업 영역은 저장소 계정에 더 이상 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-316">If the access keys are changed after the workspace is created, the workspace can no longer access the storage account.</span></span> <span data-ttu-id="9cda6-317">작동이 중지되고 해당 작업 영역의 모든 실험이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-317">It will stop functioning and all experiments in that workspace will fail.</span></span>

<span data-ttu-id="9cda6-318">저장소 계정 액세스 키를 변경한 경우에는, Azure 클래식 포털을 사용하여 작업 영역에서 액세스 키를 다시 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-318">If you changed storage account access keys, resync the access keys in the workspace by using the Azure classic portal.</span></span>  

## <a name="support-and-training"></a><span data-ttu-id="9cda6-319">지원 및 교육</span><span class="sxs-lookup"><span data-stu-id="9cda6-319">Support and training</span></span>
<span data-ttu-id="9cda6-320">**Azure 기계 학습에 대한 교육은 어디에서 받을 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-320">**Where can I get training for Azure Machine Learning?**</span></span>

<span data-ttu-id="9cda6-321">[Azure Machine Learning 설명서 센터](https://azure.microsoft.com/services/machine-learning/)에서 비디오 자습서와 방법 가이드를 호스트합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-321">The [Azure Machine Learning Documentation Center](https://azure.microsoft.com/services/machine-learning/) hosts video tutorials and how-to guides.</span></span> <span data-ttu-id="9cda6-322">이러한 단계별 가이드에서는 서비스를 소개하고, 데이터 가져오기, 데이터 정리, 예측 모델 구성, Azure Machine Learning을 사용하여 프로덕션에 배포의 데이터 과학 수명 주기 전체를 설명해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-322">These step-by-step guides introduce the services and explain the data science life cycle of importing data, cleaning data, building predictive models, and deploying them in production by using Azure Machine Learning.</span></span>

<span data-ttu-id="9cda6-323">Microsoft는 Machine Learning Center에 새로운 자료를 추가하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-323">We add new material to the Machine Learning Center on an ongoing basis.</span></span> <span data-ttu-id="9cda6-324">[사용자 피드백 포럼](https://windowsazure.uservoice.com/forums/257792-machine-learning)에서 기계 학습 센터의 추가 학습 자료에 대한 요청을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-324">You can submit requests for additional learning material on Machine Learning Center at the [user feedback forum](https://windowsazure.uservoice.com/forums/257792-machine-learning).</span></span>

<span data-ttu-id="9cda6-325">[Microsoft Virtual Academy](http://www.microsoftvirtualacademy.com/training-courses/getting-started-with-microsoft-azure-machine-learning)에서 교육을 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-325">You can also find training at [Microsoft Virtual Academy](http://www.microsoftvirtualacademy.com/training-courses/getting-started-with-microsoft-azure-machine-learning).</span></span>

<span data-ttu-id="9cda6-326">**Azure 기계 학습에 대한 지원을 받으려면 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-326">**How do I get support for Azure Machine Learning?**</span></span>

<span data-ttu-id="9cda6-327">Azure Machine Learning에 대한 기술 지원을 받으려면 [Azure 지원](/support/options/) 으로 이동하여 **기계 학습**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-327">To get technical support for Azure Machine Learning, go to [Azure Support](/support/options/), and select **Machine Learning**.</span></span>

<span data-ttu-id="9cda6-328">또한 Azure Machine Learning은 MSDN에 커뮤니티 포럼을 갖고 있으며, 여기에서 Azure 기계 학습 관련 질문을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-328">Azure Machine Learning also has a community forum on MSDN where you can ask questions about Azure Machine Learning.</span></span> <span data-ttu-id="9cda6-329">Azure Machine Learning 팀에서 포럼을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-329">The Azure Machine Learning team monitors the forum.</span></span> <span data-ttu-id="9cda6-330">[Azure 포럼](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning)으로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-330">Go to [Azure Forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning).</span></span>

## <a name="billing-questions"></a><span data-ttu-id="9cda6-331">대금 청구 관련 질문</span><span class="sxs-lookup"><span data-stu-id="9cda6-331">Billing questions</span></span>
<span data-ttu-id="9cda6-332">**기계 학습 결제는 어떤 방식으로 이루어지나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-332">**How does Machine Learning billing work?**</span></span>

<span data-ttu-id="9cda6-333">Azure Machine Learning은 Machine Learning Studio 및 Machine Learning 웹 서비스라는 두 구성 요소로 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-333">Azure Machine Learning has two components: Machine Learning Studio and Machine Learning web services.</span></span>

<span data-ttu-id="9cda6-334">Machine Learning Studio를 평가하는 동안 무료 청구 계층을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-334">While you are evaluating Machine Learning Studio, you can use the Free billing tier.</span></span> <span data-ttu-id="9cda6-335">무료 계층을 사용하면 제한된 용량으로 클래식 웹 서비스를 배포할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-335">The Free tier also lets you deploy a Classic web service that has limited capacity.</span></span>

<span data-ttu-id="9cda6-336">Azure Machine Learning이 필요를 충족한다고 결정했으면 표준 계층에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-336">If you decide that Azure Machine Learning meets your needs, you can sign up for the Standard tier.</span></span> <span data-ttu-id="9cda6-337">등록하려면 Microsoft Azure 구독이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-337">To sign up, you must have a Microsoft Azure subscription.</span></span>

<span data-ttu-id="9cda6-338">표준 계층에서는 Machine Learning Studio에서 정의하는 각 작업 영역에 대해 월별로 요금을 청구합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-338">In the Standard tier, you are billed monthly for each workspace that you define in Machine Learning Studio.</span></span> <span data-ttu-id="9cda6-339">스튜디오에서 실험을 실행하면 실험을 실행할 때 계산 리소스가 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-339">When you run an experiment in the studio, you are billed for compute resources when you are running an experiment.</span></span> <span data-ttu-id="9cda6-340">클래식 웹 서비스를 배포하는 경우 트랜잭션 및 계산 시간은 종량제 기준으로 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-340">When you deploy a Classic web service, transactions and compute hours are billed on the Pay As You Go basis.</span></span>

<span data-ttu-id="9cda6-341">새 Resource Manager 기반 웹 서비스는 비용을 예측할 수 있도록 청구 계획을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-341">New (Resource Manager-based) web services introduce billing plans that allow for more predictability in costs.</span></span> <span data-ttu-id="9cda6-342">계층화된 가격 책정은 많은 양의 용량을 필요로 하는 고객에게 할인된 요금을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-342">Tiered pricing offers discounted rates to customers who need a large amount of capacity.</span></span>

<span data-ttu-id="9cda6-343">계획을 만들 때 API 계산 시간 및 API 트랜잭션이 포함된 수량과 함께 제공되는 고정된 비용에 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-343">When you create a plan, you commit to a fixed cost that comes with an included quantity of API compute hours and API transactions.</span></span> <span data-ttu-id="9cda6-344">포함된 수량이 더 필요한 경우 계획에 인스턴스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-344">If you need more included quantities, you can add instances to your plan.</span></span> <span data-ttu-id="9cda6-345">포함된 수량이 더 많이 필요한 경우 포함된 수량을 훨씬 더 많이 제공하고 할인율이 더 나은 높은 계층 계획을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-345">If you need a lot more included quantities, you can choose a higher tier plan that provides considerably more included quantities and a better discounted rate.</span></span>

<span data-ttu-id="9cda6-346">기존 인스턴스에 포함된 수량을 모두 사용한 후에 추가 사용량은 청구 계획 계층과 연결된 초과 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-346">After the included quantities in existing instances are used up, additional usage is charged at the overage rate that's associated with the billing plan tier.</span></span>

> [!NOTE]
<span data-ttu-id="9cda6-347">포함된 수량은 30일마다 다시 할당되고 사용하지 않은 포함된 수량은 다음 기간에 롤오버되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-347">Included quantities are reallocated every 30 days, and unused included quantities do not roll over to the next period.</span></span>

<span data-ttu-id="9cda6-348">추가 대금 청구 및 가격 책정 정보는 [기계 학습 가격](https://azure.microsoft.com/pricing/details/machine-learning/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-348">For additional billing and pricing information, see [Machine Learning Pricing](https://azure.microsoft.com/pricing/details/machine-learning/).</span></span>

<span data-ttu-id="9cda6-349">**Azure 기계 학습의 무료 평가판이 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-349">**Does Machine Learning have a free trial?**</span></span>

 <span data-ttu-id="9cda6-350">Azure Machine Learning에는 무료 구독 옵션이 포함되며 이에 대한 내용은 [Machine Learning 가격 책정](https://azure.microsoft.com/pricing/details/machine-learning/)에 설명됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-350">Azure Machine Learning has a free subscription option that's explained in [Machine Learning Pricing](https://azure.microsoft.com/pricing/details/machine-learning/).</span></span> <span data-ttu-id="9cda6-351">Machine Learning Studio에는 [Machine Learning Studio](https://studio.azureml.net/?selectAccess=true&o=2)에 로그인할 때 사용 가능한 8시간의 빠른 평가판이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-351">Machine Learning Studio has an eight-hour quick evaluation trial that's available when you sign in to [Machine Learning Studio](https://studio.azureml.net/?selectAccess=true&o=2).</span></span>

 <span data-ttu-id="9cda6-352">또한 Azure 무료 평가판에 등록하면 한 달 동안 모든 Azure 서비스를 사용해볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-352">In addition, when you sign up for an Azure free trial, you can try any Azure services for a month.</span></span> <span data-ttu-id="9cda6-353">Azure 무료 평가판에 대한 자세한 내용을 보려면 [Azure 무료 평가판 FAQ](https://azure.microsoft.com/pricing/free-trial-faq/)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-353">To learn more about the Azure free trial, visit [Azure free trial FAQ](https://azure.microsoft.com/pricing/free-trial-faq/).</span></span>

<span data-ttu-id="9cda6-354">**트랜잭션이란?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-354">**What is a transaction?**</span></span>

<span data-ttu-id="9cda6-355">트랜잭션은 Azure Machine Learning이 응답하는 API 호출을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-355">A transaction represents an API call that Azure Machine Learning responds to.</span></span> <span data-ttu-id="9cda6-356">RRS(요청-응답 서비스) 및 BES(배치 실행 서비스) 호출에서 트랜잭션이 집계되고 청구 계획에 대한 요금으로 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-356">Transactions from Request-Response Service (RRS) and Batch Execution Service (BES) calls are aggregated and charged against your billing plan.</span></span>

<span data-ttu-id="9cda6-357">**RRS와 BES 트랜잭션 모두에 대한 계획에 포함된 트랜잭션 수량을 사용할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-357">**Can I use the included transaction quantities in a plan for both RRS and BES transactions?**</span></span>

<span data-ttu-id="9cda6-358">예, RRS와 BES에서 트랜잭션이 집계되고 청구 계획에 대한 요금으로 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-358">Yes, your transactions from your RRS and BES are aggregated and charged against your billing plan.</span></span>

<span data-ttu-id="9cda6-359">**API 계산 시간이란?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-359">**What is an API compute hour?**</span></span>

<span data-ttu-id="9cda6-360">API 계산 시간은 Machine Learning 계산 리소스를 사용하여 API 호출 실행에 소요되는 시간에 대한 청구 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-360">An API compute hour is the billing unit for the time that API calls take to run by using Machine Learning compute resources.</span></span> <span data-ttu-id="9cda6-361">모든 호출은 청구 목적으로 집계됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-361">All your calls are aggregated for billing purposes.</span></span>

<span data-ttu-id="9cda6-362">**일반 프로덕션 API 호출은 얼마나 걸리나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-362">**How long does a typical production API call take?**</span></span>

<span data-ttu-id="9cda6-363">일반적으로 프로덕션 API 호출 시간은 수백 밀리초에서 몇 초에 이르기까지 상당히 다양합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-363">Production API call times can vary significantly, generally ranging from hundreds of milliseconds to a few seconds.</span></span> <span data-ttu-id="9cda6-364">일부 API 호출은 데이터 처리 및 기계 학습 모델의 복잡도에 따라 몇 분이 필요할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-364">Some API calls might require minutes depending on the complexity of the data processing and machine-learning model.</span></span> <span data-ttu-id="9cda6-365">프로덕션 API 호출 시간을 예측하는 가장 좋은 방법은 기계 학습 서비스에서 모델을 벤치마킹하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-365">The best way to estimate production API call times is to benchmark a model on the Machine Learning service.</span></span>

<span data-ttu-id="9cda6-366">**스튜디오 계산 시간이란?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-366">**What is a Studio compute hour?**</span></span>

<span data-ttu-id="9cda6-367">스튜디오 계산 시간은 실험이 스튜디오에서 계산 리소스를 사용한 집계 시간에 대한 청구 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-367">A Studio compute hour is the billing unit for the aggregate time that your experiments use compute resources in studio.</span></span>

<span data-ttu-id="9cda6-368">**새 Azure Resource Manager 기반 웹 서비스에서 개발/테스트 계층의 용도는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-368">**In New (Azure Resource Manager-based) web services, what is the Dev/Test tier meant for?**</span></span>

<span data-ttu-id="9cda6-369">Resource Manager 기반 웹 서비스는 청구 계획을 프로비전하는 데 사용할 수 있는 여러 계층을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-369">Resource Manager-based web services provide multiple tiers that you can use to provision your billing plan.</span></span> <span data-ttu-id="9cda6-370">개발/테스트 가격 책정 계층은 별도의 비용 없이도 실험을 웹 서비스로 테스트할 수 있도록 제한된 만큼의 포함된 수량을 제공하는 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-370">The Dev/Test pricing tier provides limited, included quantities that allow you to test your experiment as a web service without incurring costs.</span></span> <span data-ttu-id="9cda6-371">이 계층의 작동 방식을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-371">You have the opportunity to see how it works.</span></span>

<span data-ttu-id="9cda6-372">**저장소 요금은 별도입니까?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-372">**Are there separate storage charges?**</span></span>

<span data-ttu-id="9cda6-373">Machine Learning 무료 계층은 별도의 저장소를 필요로 하지 않거나 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-373">The Machine Learning Free tier does not require or allow separate storage.</span></span> <span data-ttu-id="9cda6-374">기계 학습 표준 계층을 사용하려면 Azure 저장소 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-374">The Machine Learning Standard tier requires users to have an Azure storage account.</span></span> <span data-ttu-id="9cda6-375">Azure Storage는 [별도로 청구됩니다](https://azure.microsoft.com/pricing/details/storage/).</span><span class="sxs-lookup"><span data-stu-id="9cda6-375">Azure Storage is [billed separately](https://azure.microsoft.com/pricing/details/storage/).</span></span>

<span data-ttu-id="9cda6-376">**Machine Learning에서 고가용성 작업을 지원하나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-376">**Does Machine Learning support high availability?**</span></span>

<span data-ttu-id="9cda6-377">예.</span><span class="sxs-lookup"><span data-stu-id="9cda6-377">Yes.</span></span> <span data-ttu-id="9cda6-378">자세한 내용은 [Machine Learning 가격 책정](https://azure.microsoft.com/en-us/pricing/details/machine-learning/)에서 Service Level Agreement(서비스 수준 약정)에 대한 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-378">For details, see [Machine Learning Pricing](https://azure.microsoft.com/en-us/pricing/details/machine-learning/) for a description of the service level agreement (SLA).</span></span>

<span data-ttu-id="9cda6-379">**내 프로덕션 API 호출이 실행될 계산 리소스의 구체적인 종류는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-379">**What specific kind of compute resources will my production API calls be run on?**</span></span>

<span data-ttu-id="9cda6-380">Machine Learning 서비스는 다중 테넌트 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-380">The Machine Learning service is a multitenant service.</span></span> <span data-ttu-id="9cda6-381">백 엔드에서 사용되는 실제 계산 리소스는 다양하며 성능 및 예측성을 위해 최적화됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-381">Actual compute resources that are used on the back end vary and are optimized for performance and predictability.</span></span>

### <a name="management-of-new-resource-manager-based-web-services"></a><span data-ttu-id="9cda6-382">새 Resource Manager 기반 웹 서비스 관리</span><span class="sxs-lookup"><span data-stu-id="9cda6-382">Management of New (Resource Manager-based) web services</span></span>
<span data-ttu-id="9cda6-383">**계획을 삭제하면 어떻게 되나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-383">**What happens if I delete my plan?**</span></span>

<span data-ttu-id="9cda6-384">계획이 구독에서 제거되고 비례 청구된 사용량에 대한 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-384">The plan is removed from your subscription, and you are billed for prorated usage.</span></span>

> [!NOTE]
<span data-ttu-id="9cda6-385">웹 서비스에서 사용하는 계획을 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-385">You cannot delete a plan that a web service is using.</span></span> <span data-ttu-id="9cda6-386">계획을 삭제하려면 웹 서비스에 새 계획을 할당하거나 웹 서비스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-386">To delete the plan, you must either assign a new plan to the web service or delete the web service.</span></span>

<span data-ttu-id="9cda6-387">**계획 인스턴스란?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-387">**What is a plan instance?**</span></span>

<span data-ttu-id="9cda6-388">계획 인스턴스는 청구 계획에 추가할 수 있는 포함된 수량의 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-388">A plan instance is a unit of included quantities that you can add to your billing plan.</span></span> <span data-ttu-id="9cda6-389">청구 계획에 대한 청구 계층을 선택하면 인스턴스 하나와 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-389">When you select a billing tier for your billing plan, it comes with one instance.</span></span> <span data-ttu-id="9cda6-390">포함된 수량이 더 필요한 경우 계획에 선택한 청구 계층의 인스턴스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-390">If you need more included quantities, you can add instances of the selected billing tier to your plan.</span></span>

<span data-ttu-id="9cda6-391">**계획 인스턴스를 얼마나 추가할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-391">**How many plan instances can I add?**</span></span>

<span data-ttu-id="9cda6-392">구독에는 개발/테스트 가격 책정 계층의 인스턴스 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-392">You can have one instance of the Dev/Test pricing tier in a subscription.</span></span>

<span data-ttu-id="9cda6-393">표준 S1, 표준 S2, 표준 S3 계층의 경우 필요한 만큼을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-393">For Standard S1, Standard S2, and Standard S3 tiers, you can add as many as necessary.</span></span>

> [!NOTE]
<span data-ttu-id="9cda6-394">예상된 사용량에 따라 현재 계층에 인스턴스를 추가하는 대신 더 많이 포함된 수량으로 업그레이드하는 편이 보다 더 비용 효율적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-394">Depending on your anticipated usage, it might be more cost effective to upgrade to a tier that has more included quantities rather than add instances to the current tier.</span></span>

<span data-ttu-id="9cda6-395">**계획 계층을 변경(업그레이드/다운그레이드)하는 경우 어떻게 되나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-395">**What happens when I change plan tiers (upgrade / downgrade)?**</span></span>

<span data-ttu-id="9cda6-396">이전 계획은 삭제되고 현재 사용량은 비례적으로 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-396">The old plan is deleted and the current usage is billed on a prorated basis.</span></span> <span data-ttu-id="9cda6-397">업그레이드/다운그레이드된 계층의 전체 포함된 수량이 있는 새 계획이 나머지 기간 동안 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-397">A new plan with the full included quantities of the upgraded/downgraded tier is created for the rest of the period.</span></span>

> [!NOTE]
<span data-ttu-id="9cda6-398">포함된 수량은 기간당 할당되고 사용하지 않은 수량은 롤오버되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-398">Included quantities are allocated per period, and unused quantities do not roll over.</span></span>

<span data-ttu-id="9cda6-399">**계획의 인스턴스를 증가시키면 어떻게 되나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-399">**What happens when I increase the instances in a plan?**</span></span>

<span data-ttu-id="9cda6-400">수량은 비례적으로 포함되고 적용되는 데 24시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-400">Quantities are included on a prorated basis and may take 24 hours to be effective.</span></span>

<span data-ttu-id="9cda6-401">**계획의 인스턴스를 삭제하면 어떻게 되나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-401">**What happens when I delete an instance of a plan?**</span></span>

<span data-ttu-id="9cda6-402">인스턴스가 구독에서 제거되고 비례 청구된 사용량에 대한 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-402">The instance is removed from your subscription, and you are billed for prorated usage.</span></span>

### <a name="sign-up-for-new-resource-manager-based-web-services-plans"></a><span data-ttu-id="9cda6-403">새 Resource Manager 기반 웹 서비스 계획 등록</span><span class="sxs-lookup"><span data-stu-id="9cda6-403">Sign up for New (Resource Manager-based) web services plans</span></span>
<span data-ttu-id="9cda6-404">**계획에 어떻게 등록하나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-404">**How do I sign up for a plan?**</span></span>

<span data-ttu-id="9cda6-405">두 가지 방법으로 청구 계획을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-405">You have two ways to create billing plans.</span></span>

<span data-ttu-id="9cda6-406">Resource Manager 기반 웹 서비스를 처음 배포할 때 기존 계획을 선택하거나 새 계획을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-406">When you first deploy a Resource Manager-based web service, you can choose an existing plan or create a new plan.</span></span>

<span data-ttu-id="9cda6-407">이 방식으로 만든 계획은 기본 지역에 있으며 웹 서비스도 해당 지역에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-407">Plans that you create in this manner are in your default region, and your web service will be deployed to that region.</span></span>

<span data-ttu-id="9cda6-408">기본 지역이 아닌 지역에 서비스를 배포하려는 경우 서비스를 배포하기 전에 청구 계획을 정의하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-408">If you want to deploy services to regions other than your default region, you may want to define your billing plans before you deploy your service.</span></span>

<span data-ttu-id="9cda6-409">이 경우에 Azure Machine Learning 웹 서비스 포털에 로그인하여 계획 페이지로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-409">In that case, you can sign in to the Azure Machine Learning Web Services portal, and go to the Plans page.</span></span> <span data-ttu-id="9cda6-410">거기에서 계획을 추가하고 삭제할 수 있을 뿐만 아니라 기존 계획을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-410">From there, you can add plans, delete plans, and modify existing plans.</span></span>

<span data-ttu-id="9cda6-411">**처음에 어떤 계획부터 사용하는 게 좋을까요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-411">**Which plan should I choose to start off with?**</span></span>

<span data-ttu-id="9cda6-412">표준 S1 계층으로 시작해보고 서비스의 사용량을 모니터링하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-412">We recommend you that you start with the Standard S1 tier and monitor your service for usage.</span></span> <span data-ttu-id="9cda6-413">포함된 수량을 빠르게 사용할 경우 인스턴스를 추가하거나 더 높은 계층으로 이동하여 할인된 요금을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-413">If you find that you are using your included quantities rapidly, you can add instances or move to a higher tier and get better discounted rates.</span></span> <span data-ttu-id="9cda6-414">청구 주기 동안 필요에 따라 청구 계획을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-414">You can adjust your billing plan as needed throughout your billing cycle.</span></span>

<span data-ttu-id="9cda6-415">**새 계획을 사용할 수 있는 지역은 어디인가요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-415">**Which regions are the new plans available in?**</span></span>

<span data-ttu-id="9cda6-416">새 청구 계획은 새 웹 서비스가 지원되는 다음 세 곳의 프로덕션 지역에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-416">The new billing plans are available in the three production regions in which we support the new web services:</span></span>

* <span data-ttu-id="9cda6-417">미국 중남부</span><span class="sxs-lookup"><span data-stu-id="9cda6-417">South Central US</span></span>
* <span data-ttu-id="9cda6-418">서유럽</span><span class="sxs-lookup"><span data-stu-id="9cda6-418">West Europe</span></span>
* <span data-ttu-id="9cda6-419">동남아시아</span><span class="sxs-lookup"><span data-stu-id="9cda6-419">South East Asia</span></span>

<span data-ttu-id="9cda6-420">**여러 지역에서 웹 서비스를 사용합니다. 모든 지역에 대한 계획이 필요한가요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-420">**I have web services in multiple regions. Do I need a plan for every region?**</span></span>

<span data-ttu-id="9cda6-421">예.</span><span class="sxs-lookup"><span data-stu-id="9cda6-421">Yes.</span></span> <span data-ttu-id="9cda6-422">지역에 따라 계획 가격 책정이 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-422">Plan pricing varies by region.</span></span> <span data-ttu-id="9cda6-423">다른 지역에 웹 서비스를 배포하는 경우 해당 지역에 특정된 계획을 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-423">When you deploy a web service to another region, you need to assign it a plan that is specific to that region.</span></span> <span data-ttu-id="9cda6-424">자세한 내용은 [지역별 사용 가능한 제품]( https://azure.microsoft.com/regions/services/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-424">For more information, see [Products available by region]( https://azure.microsoft.com/regions/services/).</span></span>

### <a name="new-web-services-overages"></a><span data-ttu-id="9cda6-425">새 웹 서비스 - 초과분</span><span class="sxs-lookup"><span data-stu-id="9cda6-425">New web services: Overages</span></span>
<span data-ttu-id="9cda6-426">**내 웹 서비스 사용량을 초과했는지 어떻게 확인하나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-426">**How do I check if I exceeded my web service usage?**</span></span>

<span data-ttu-id="9cda6-427">Azure Machine Learning 웹 서비스 포털의 계획 페이지에서 모든 계획의 사용량을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-427">You can view the usage on all your plans on the Plans page in the Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="9cda6-428">포털에 로그인한 다음 **계획** 메뉴 옵션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-428">Sign in to the portal, and then click the **Plans** menu option.</span></span>

<span data-ttu-id="9cda6-429">테이블의 **트랜잭션** 및 **계산** 열에서 계획의 포함된 수량 및 사용된 백분율을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-429">In the **Transactions** and **Compute** columns of the table, you can see the included quantities of the plan and the percentage used.</span></span>

<span data-ttu-id="9cda6-430">**개발/테스트 가격 책정 계층에 포함된 수량을 모두 사용하면 어떻게 되나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-430">**What happens when I use up the include quantities in the Dev/Test pricing tier?**</span></span>

<span data-ttu-id="9cda6-431">개발/테스트 가격 책정 계층이 할당된 서비스가 다음 기간 또는 유료 계층으로 전환될 때까지 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-431">Services that have a Dev/Test pricing tier assigned to them are stopped until the next period or until you move them to a paid tier.</span></span>

<span data-ttu-id="9cda6-432">**클래식 웹 서비스 및 새 Resource Manager 기반 웹 서비스 초과분의 경우 RRS(요청 응답) 및 BES(배치) 워크로드에 대한 가격은 어떻게 계산되나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-432">**For Classic web services and overages of New (Resource Manager-based) web services, how are prices calculated for Request Response (RRS) and Batch (BES) workloads?**</span></span>

<span data-ttu-id="9cda6-433">RRS 워크로드의 경우 요청하신 모든 API 트랜잭션 호출 및 해당 요청과 연관된 계산 시간에 대한 비용이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-433">For an RRS workload, you are charged for every API transaction call that you make and for the compute time that's associated with those requests.</span></span> <span data-ttu-id="9cda6-434">RRS 프로덕션 API 트랜잭션 비용은 요청하신 총 API 호출 수에 트랜잭션 1,000개당 가격을 곱하여 계산됩니다(트랜잭션별 일할 계산).</span><span class="sxs-lookup"><span data-stu-id="9cda6-434">Your RRS production API transaction costs are calculated as the total number of API calls that you make multiplied by the price per 1,000 transactions (prorated by individual transaction).</span></span> <span data-ttu-id="9cda6-435">RRS API 프로덕션 API 계산 시간 비용은 각 API 호출 실행에 필요한 시간에 총 API 트랜잭션 수를 곱하고 프로덕션 API 계산 시간당 가격을 곱하여 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-435">Your RRS API production API compute hour costs are calculated as the amount of time required for each API call to run, multiplied by the total number of API transactions, multiplied by the price per production API compute hour.</span></span>

<span data-ttu-id="9cda6-436">예를 들어 표준 S1 초과분의 경우 한 번 실행하는 데 0.72초가 걸리는 API 트랜잭션이 1,000,000개 있다면 프로덕션 API 트랜잭션 비용은 $500(1,000,000 $0.50/1K API 트랜잭션)이고 프로덕션 API 계산 시간은 $400(1,000,000 0.72초 * $2/시간)로 총 $900의 금액이 산정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-436">For example, for Standard S1 overage, 1,000,000 API transactions that take 0.72 seconds each to run would result in (1,000,000 * $0.50/1K API transactions) in $500 in production API transaction costs and (1,000,000 * 0.72 sec * $2/hr) $400 in production API compute hours, for a total of $900.</span></span>

<span data-ttu-id="9cda6-437">BES 워크로드도 같은 방식으로 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-437">For a BES workload, you are charged in the same manner.</span></span> <span data-ttu-id="9cda6-438">하지만 API 트랜잭션 비용은 제출한 일괄 작업 수를, 계산 비용은 해당 일괄 작업과 연관된 계산 시간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-438">However, the API transaction costs represent the number of batch jobs that you submit, and the compute costs represent the compute time that's associated with those batch jobs.</span></span> <span data-ttu-id="9cda6-439">BES 프로덕션 API 트랜잭션 비용은 제출한 총 작업 수에 트랜잭션 1,000개당 가격을 곱하여 계산됩니다(트랜잭션별 일할 계산).</span><span class="sxs-lookup"><span data-stu-id="9cda6-439">Your BES production API transaction costs are calculated as the total number of jobs submitted multiplied by the price per 1,000 transactions (prorated by individual transaction).</span></span> <span data-ttu-id="9cda6-440">BES API 프로덕션 API 계산 시간 비용은 작업의 각 행 실행에 필요한 시간에 작업의 총 행 수, 총 작업 수, 프로덕션 API 계산 시간당 가격을 곱하여 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-440">Your BES API production API compute hour costs are calculated as the amount of time required for each row in your job to run multiplied by the total number of rows in your job multiplied by the total number of jobs multiplied by the price per production API compute hour.</span></span> <span data-ttu-id="9cda6-441">Machine Learning 계산기를 사용할 때 트랜잭션 미터는 제출하려는 작업 수를, 트랜잭션 필드당 시간은 각 작업의 모든 행을 실행하는 데 필요한 총 시간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-441">When you use the Machine Learning calculator, the transaction meter represents the number of jobs that you plan to submit, and the time-per-transaction field represents the combined time that's needed for all rows in each job to run.</span></span>

<span data-ttu-id="9cda6-442">예를 들어 표준 S1 초과분에 대해 각 0.72초가 필요한 행 500개로 구성된 각 작업을 하루에 100개 제출한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-442">For example, assume Standard S1 overage, and you submit 100 jobs per day that each consist of 500 rows that take 0.72 seconds each.</span></span> <span data-ttu-id="9cda6-443">월간 초과 비용은 프로덕션 API 트랜잭션 비용 $1.55(하루 100개 작업 = 3,100개 작업/1개월 $0.50/1K API 트랜잭션)이며 프로덕션 API 계산 시간은 $620(500행 0.72초 3,100개 작업 $2/시간)로 총 $621.55의 금액이 산정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-443">Your monthly overage costs would be (100 jobs per day = 3,100 jobs/mo * $0.50/1K API transactions) $1.55 in production API transaction costs and (500 rows * 0.72 sec * 3,100 Jobs * $2/hr) $620 in production API compute hours, for a total of $621.55.</span></span>

### <a name="azure-machine-learning-classic-web-services"></a><span data-ttu-id="9cda6-444">Azure Machine Learning 클래식 웹 서비스</span><span class="sxs-lookup"><span data-stu-id="9cda6-444">Azure Machine Learning Classic web services</span></span>
<span data-ttu-id="9cda6-445">**종량제를 계속 사용할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-445">**Is Pay As You Go still available?**</span></span>

<span data-ttu-id="9cda6-446">예, 기존 웹 서비스는 Azure Machine Learning에서 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-446">Yes, Classic web services are still available in Azure Machine Learning.</span></span>  

### <a name="azure-machine-learning-free-and-standard-tier"></a><span data-ttu-id="9cda6-447">Azure Machine Learning 무료 및 표준 계층</span><span class="sxs-lookup"><span data-stu-id="9cda6-447">Azure Machine Learning Free and Standard tier</span></span>
<span data-ttu-id="9cda6-448">**Azure 기계 학습 무료 계층에는 무엇이 포함되나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-448">**What is included in the Azure Machine Learning Free tier?**</span></span>

<span data-ttu-id="9cda6-449">Azure 기계 학습 무료 계층은 Azure 기계 학습 스튜디오를 자세히 소개하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-449">The Azure Machine Learning Free tier is intended to provide an in-depth introduction to the Azure Machine Learning Studio.</span></span> <span data-ttu-id="9cda6-450">Microsoft 계정을 등록하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-450">All you need is a Microsoft account to sign up.</span></span> <span data-ttu-id="9cda6-451">무료 계층에는 [Microsoft 계정](https://www.microsoft.com/account/default.aspx)당 하나의 Azure 기계 학습 스튜디오 작업 영역에 대한 무료 액세스 권한이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-451">The Free tier includes free access to one Azure Machine Learning Studio workspace per [Microsoft account](https://www.microsoft.com/account/default.aspx).</span></span> <span data-ttu-id="9cda6-452">이 계층에서 최대 10GB의 저장소를 사용하고 스테이징 API로서 모델을 운영할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-452">In this tier, you can use up to 10 GB of storage and operationalize models as staging APIs.</span></span> <span data-ttu-id="9cda6-453">무료 계층 작업은 SLA의 적용을 받지 않으며 개발 및 개인 용도로만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-453">Free tier workloads are not covered by an SLA and are intended for development and personal use only.</span></span> 

<span data-ttu-id="9cda6-454">무료 계층 작업 영역의 제한 사항:</span><span class="sxs-lookup"><span data-stu-id="9cda6-454">Free tier workspaces have the following limitations:</span></span>

* <span data-ttu-id="9cda6-455">워크로드가 SQL Server가 실행되는 온-프레미스 서버에 연결하여 데이터에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-455">Workloads can't access data by connecting to an on-premises server that runs SQL Server.</span></span>
* <span data-ttu-id="9cda6-456">새 리소스 관리자 기반 웹 서비스를 배포할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-456">You cannot deploy New Resource Manager base web services.</span></span>


<span data-ttu-id="9cda6-457">**Azure 기계 학습 표준 계층 및 계획에는 무엇이 포함됩니까?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-457">**What is included in the Azure Machine Learning Standard tier and plans?**</span></span>

<span data-ttu-id="9cda6-458">Azure 기계 학습 표준 계층은 Azure 기계 학습 스튜디오의 유료 프로덕션 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-458">The Azure Machine Learning Standard tier is a paid production version of Azure Machine Learning Studio.</span></span> <span data-ttu-id="9cda6-459">Azure Machine Learning Studio는 작업 영역별 및 월별 기준으로 요금이 청구되고 한 달이 안되는 경우 일할 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-459">The Azure Machine Learning Studio monthly fee is billed on a per workspace per month basis and prorated for partial months.</span></span> <span data-ttu-id="9cda6-460">Azure Machine Learning 스튜디오 실험 시간은 실제 실험의 계산 시간을 기준으로 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-460">Azure Machine Learning Studio experiment hours are billed per compute hour for active experimentation.</span></span> <span data-ttu-id="9cda6-461">요금은 부분 시간별로 일할 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-461">Billing is prorated for partial hours.</span></span>  

<span data-ttu-id="9cda6-462">Azure Machine Learning API 서비스는 클래식 웹 서비스 또는 새로운 Resource Manager 기반 웹 서비스인지에 따라 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-462">The Azure Machine Learning API service is billed depending on whether it's a Classic web service or a New (Resource Manager-based) web service.</span></span>

<span data-ttu-id="9cda6-463">다음 요금은 구독에 대해 작업 영역별로 집계됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-463">The following charges are aggregated per workspace for your subscription.</span></span>

* <span data-ttu-id="9cda6-464">Machine Learning 작업 영역 구독 - Machine Learning 작업 영역 구독은 Machine Learning Studio 작업 영역에 대한 액세스를 제공하는 월별 요금입니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-464">Machine Learning Workspace Subscription: The Machine Learning workspace subscription is a monthly fee that provides access to a Machine Learning Studio workspace.</span></span> <span data-ttu-id="9cda6-465">이 구독은 스튜디오에서 실행하고 프로덕션 API를 활용하는 실험에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-465">The subscription is required to run experiments in the studio and to utilize the production APIs.</span></span>
* <span data-ttu-id="9cda6-466">스튜디오 실험 시간 - 이 미터는 Machine Learning Studio에서 실행 중인 실험과 스테이징 환경에서 실행 중인 프로덕션 API 호출로 발생하는 모든 계산 요금을 집계합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-466">Studio Experiment hours: This meter aggregates all compute charges that are accrued by running experiments in Machine Learning Studio and running production API calls in the staging environment.</span></span>
* <span data-ttu-id="9cda6-467">교육 및 평가를 위해 모델에서 SQL Server를 실행하는 온-프레미스 서버에 연결하여 데이터에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-467">Access data by connecting to an on-premises server that runs SQL Server in your models for your training and scoring.</span></span>
* <span data-ttu-id="9cda6-468">클래식 웹 서비스의 경우:</span><span class="sxs-lookup"><span data-stu-id="9cda6-468">For Classic web services:</span></span>
  * <span data-ttu-id="9cda6-469">프로덕션 API 계산 시간: 이 미터에는 프로덕션에서 실행 중인 웹 서비스로 발생하는 계산 요금이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-469">Production API Compute Hours: This meter includes compute charges that are accrued by web services running in production.</span></span>
  * <span data-ttu-id="9cda6-470">프로덕션 API 트랜잭션(단위: 1000): 이 미터에는 프로덕션 웹 서비스 호출당 발생하는 요금이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-470">Production API Transactions (in 1000s): This meter includes charges that are accrued per call to your production web service.</span></span>

<span data-ttu-id="9cda6-471">Resource Manager 기반 웹 서비스의 경우 앞의 요금 외에도 선택한 계획에 대한 요금이 집계됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-471">Apart from the preceding charges, in the case of Resource Manager-based web service, charges are aggregated to the selected plan:</span></span>

* <span data-ttu-id="9cda6-472">표준 S1/S2/S3 API 계획(단위): 이 미터는 Resource Manager 기반 웹 서비스에 대해 선택한 인스턴스의 유형을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-472">Standard S1/S2/S3 API Plan (Units): This meter represents the type of instance that's selected for Resource Manager-based web services.</span></span>
* <span data-ttu-id="9cda6-473">표준 S1/S2/S3 초과 API 계산 시간: 이 미터는 기존 인스턴스의 포함된 수량을 모두 사용한 후에 프로덕션에서 실행되는 Resource Manager 기반 웹 서비스에서 발생한 계산 요금을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-473">Standard S1/S2/S3 Overage API Compute Hours: This meter includes compute charges that are accrued by Resource Manager-based web services that run in production after the included quantities in existing instances are used up.</span></span> <span data-ttu-id="9cda6-474">추가 사용량은 S1/S2/S3 계획 계층과 관련한 초과 요금으로 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-474">The additional usage is charged at the overate rate that's associated with S1/S2/S3 plan tier.</span></span>
* <span data-ttu-id="9cda6-475">표준 S1/S2/S3 초과 API 트랜잭션(단위: 1,000): 이 미터는 기존 인스턴스의 포함된 수량을 모두 사용한 후에 프로덕션 Resource Manager 기반 웹 서비스에 대한 호출당 발생하는 요금을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-475">Standard S1/S2/S3 Overage API Transactions (in 1,000s): This meter includes charges that are accrued per call to your production Resource Manager-based web service after the included quantities in existing instances are used up.</span></span> <span data-ttu-id="9cda6-476">추가 사용량은 S1/S2/S3 계획 계층과 관련한 초과 요금으로 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-476">The additional usage is charged at the overate rate associated with S1/S2/S3 plan tier.</span></span>
* <span data-ttu-id="9cda6-477">포함된 수량 API 계산 시간: 이 미터는 Resource Manager 기반 웹 서비스를 사용하여 API 계산 시간의 포함된 수량을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-477">Included Quantity API Compute Hours: With Resource Manager-based web services, this meter represents the included quantity of API compute hours.</span></span>
* <span data-ttu-id="9cda6-478">포함된 수량 API 트랜잭션(단위: 1,000): 이 미터는 Resource Manager 기반 웹 서비스를 사용하여 API 트랜잭션의 포함된 수량을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-478">Included Quantity API Transactions (in 1,000s): With Resource Manager-based web services, this meter represents the included quantity of API transactions.</span></span>

<span data-ttu-id="9cda6-479">**Azure Machine Learning 무료 계층에 등록하려면 어떻게 하나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-479">**How do I sign up for Azure Machine Learning Free tier?**</span></span>

<span data-ttu-id="9cda6-480">Microsoft 계정만 있으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-480">All you need is a Microsoft account.</span></span> <span data-ttu-id="9cda6-481">[Azure Machine Learning 홈](https://azure.microsoft.com/services/machine-learning/)으로 이동하고 **지금 시작**을 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-481">Go to [Azure Machine Learning home](https://azure.microsoft.com/services/machine-learning/), and then click **Start Now**.</span></span> <span data-ttu-id="9cda6-482">Microsoft 계정으로 로그인하면 무료 계층에 작업 영역이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-482">Sign in with your Microsoft account and a workspace in Free tier is created for you.</span></span> <span data-ttu-id="9cda6-483">기계 학습 실험을 바로 탐색하고 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-483">You can start to explore and create Machine Learning experiments right away.</span></span>

<span data-ttu-id="9cda6-484">**Azure Machine Learning 표준 계층에 등록하려면 어떻게 하나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-484">**How do I sign up for Azure Machine Learning Standard tier?**</span></span>

<span data-ttu-id="9cda6-485">표준 Machine Learning 작업 영역을 만들려면 먼저 Azure 구독에 대한 액세스 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-485">You must first have access to an Azure subscription to create a Standard Machine Learning workspace.</span></span> <span data-ttu-id="9cda6-486">30일 무료 평가판 Azure 구독에 등록하고 나중에 유료 Azure 구독으로 업그레이드하거나 유료 Azure 구독을 바로 구입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-486">You can sign up for a 30-day free trial Azure subscription and later upgrade to a paid Azure subscription, or you can purchase a paid Azure subscription outright.</span></span> <span data-ttu-id="9cda6-487">그런 다음 구독에 대한 액세스 권한을 받은 후 Microsoft Azure 클래식 포털에서 Machine Learning 작업 영역을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-487">You can then create a Machine Learning workspace from the Microsoft Azure classic portal after you gain access to the subscription.</span></span> <span data-ttu-id="9cda6-488">[단계별 지침](https://azure.microsoft.com/trial/get-started-machine-learning-b/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cda6-488">View the [step-by-step instructions](https://azure.microsoft.com/trial/get-started-machine-learning-b/).</span></span>

<span data-ttu-id="9cda6-489">또는 표준 Machine Learning 작업 영역 소유자에게 초대를 받아 소유자의 작업 영역에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-489">Alternatively, you can be invited by a Standard Machine Learning workspace owner to access the owner's workspace.</span></span>

<span data-ttu-id="9cda6-490">**무료 계층에서 사용하기 위해 고유한 Azure Blob Storage 계정을 지정할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-490">**Can I specify my own Azure Blob storage account to use with the Free tier?**</span></span>

<span data-ttu-id="9cda6-491">아니요, 표준 계층은 표준 계층이 도입되기 전에 이용 가능했던 기계 학습 서비스 버전과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-491">No, the Standard tier is equivalent to the version of the Machine Learning service that was available before the tiers were introduced.</span></span>

<span data-ttu-id="9cda6-492">**무료 계층에서 내 기계 학습 모델을 API로 배포할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-492">**Can I deploy my machine learning models as APIs in the Free tier?**</span></span>

<span data-ttu-id="9cda6-493">예, 무료 계층의 일부로서 스테이징 API 서비스에 기계 학습 모델을 운영할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-493">Yes, you can operationalize machine learning models to staging API services as part of the Free tier.</span></span> <span data-ttu-id="9cda6-494">스테이징 API 서비스를 프로덕션하고 운영 서비스에 대한 프로덕션 끝점을 가져오려면 표준 계층을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-494">To put the staging API service into production and get a production endpoint for the operationalized service, you must use the Standard tier.</span></span>

<span data-ttu-id="9cda6-495">**Azure 무료 평가판과 Azure Machine Learning 무료 계층의 차이점은 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-495">**What is the difference between Azure free trial and Azure Machine Learning Free tier?**</span></span>

<span data-ttu-id="9cda6-496">[Microsoft Azure 무료 평가판](https://azure.microsoft.com/free/)은 한 달 동안 모든 Azure 서비스에 적용할 수 있는 크레딧을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-496">The [Microsoft Azure free trial](https://azure.microsoft.com/free/) offers credits that you can apply to any Azure service for one month.</span></span> <span data-ttu-id="9cda6-497">Azure Machine Learning 무료 계층은 프로덕션 워크로드가 아닌 경우 Azure Machine Learning에 특별히 지속적인 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-497">The Azure Machine Learning Free tier offers continuous access specifically to Azure Machine Learning for non-production workloads.</span></span>

<span data-ttu-id="9cda6-498">**무료 계층에서 표준 계층으로 실험을 이동하려면 어떻게 하나요?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-498">**How do I move an experiment from the Free tier to the Standard tier?**</span></span>

<span data-ttu-id="9cda6-499">무료 계층에서 표준 계층으로 실험을 복사하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-499">To copy your experiments from the Free tier to the Standard tier:</span></span>

1. <span data-ttu-id="9cda6-500">Azure Machine Learning Studio에 로그인하고 맨 위 탐색 모음의 작업 영역 선택기에 무료 작업 영역과 표준 작업 영역이 모두 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-500">Sign in to Azure Machine Learning Studio, and make sure that you can see both the Free workspace and the Standard workspace in the workspace selector in the top navigation bar.</span></span>
2. <span data-ttu-id="9cda6-501">표준 작업 영역에 있는 경우 무료 작업 영역으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-501">Switch to Free workspace if you are in the Standard workspace.</span></span>
3. <span data-ttu-id="9cda6-502">실험 목록 보기에서 복사하려는 실험을 선택하고 **복사** 명령 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-502">In the experiment list view, select an experiment that you'd like to copy, and then click the **Copy** command button.</span></span>
4. <span data-ttu-id="9cda6-503">팝업 대화 상자에서 표준 작업 영역을 선택하고 **복사** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-503">Select the Standard workspace from the dialog box that opens, and then click the **Copy** button.</span></span>
   <span data-ttu-id="9cda6-504">연결된 데이터 집합, 학습한 모델 등이 모두 실험과 함께 표준 작업 영역에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-504">All the associated datasets, trained model, etc. are copied together with the experiment into the Standard workspace.</span></span>
5. <span data-ttu-id="9cda6-505">실험을 다시 실행하고 표준 작업 영역에 웹 서비스를 다시 게시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-505">You need to rerun the experiment and republish your web service in the Standard workspace.</span></span>

### <a name="studio-workspace"></a><span data-ttu-id="9cda6-506">스튜디오 작업 영역</span><span class="sxs-lookup"><span data-stu-id="9cda6-506">Studio workspace</span></span>
<span data-ttu-id="9cda6-507">**작업 영역마다 별도의 청구 내역을 볼 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-507">**Will I see different bills for different workspaces?**</span></span>

<span data-ttu-id="9cda6-508">작업 영역 요금은 단일 청구서에 해당하는 각 미터로 별도 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-508">Workspace charges are broken out separately for each applicable meter on a single bill.</span></span>

<span data-ttu-id="9cda6-509">**내 실험을 실행할 구체적인 계산 리소스 종류는 무엇입니까?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-509">**What specific kind of compute resources will my experiments be run on?**</span></span>

<span data-ttu-id="9cda6-510">Machine Learning 서비스는 다중 테넌트 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-510">The Machine Learning service is a multitenant service.</span></span> <span data-ttu-id="9cda6-511">백 엔드에서 사용되는 실제 계산 리소스는 다양하며 성능 및 예측성을 위해 최적화됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-511">Actual compute resources that are used on the back end vary and are optimized for performance and predictability.</span></span>

### <a name="guest-access"></a><span data-ttu-id="9cda6-512">게스트 액세스</span><span class="sxs-lookup"><span data-stu-id="9cda6-512">Guest Access</span></span>
<span data-ttu-id="9cda6-513">**Azure 기계 학습 스튜디오의 게스트 액세스란?**</span><span class="sxs-lookup"><span data-stu-id="9cda6-513">**What is Guest Access to Azure Machine Learning Studio?**</span></span>

<span data-ttu-id="9cda6-514">게스트 액세스는 제한적인 체험 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-514">Guest Access is a restricted trial experience.</span></span> <span data-ttu-id="9cda6-515">Azure Machine Learning Studio에서 인증 없이 무료로 실험을 만들어 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-515">You can create and run experiments in Azure Machine Learning Studio at no cost and without authentication.</span></span> <span data-ttu-id="9cda6-516">게스트 세션은 저장할 수 없으며 임시로 유지되고, 8시간으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-516">Guest sessions are non-persistent (cannot be saved) and limited to eight hours.</span></span> <span data-ttu-id="9cda6-517">또한 R 및 Python이 제대로 지원되지 않고 스테이징 API가 충분하지 않으며 데이터 집합 크기와 저장소 용량도 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-517">Other limitations include lack of support for R and Python, lack of staging APIs, and restricted dataset size and storage capacity.</span></span> <span data-ttu-id="9cda6-518">하지만 Microsoft 계정으로 로그인한 사용자는 저장이 가능한 작업 영역과 보다 포괄적인 기능이 포함되어 있는 이전에 설명된 Machine Learning Studio의 무료 계층에 모두 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-518">By comparison, users who choose to sign in with a Microsoft account have full access to the Free tier of Machine Learning Studio that's described previously, which includes a persistent workspace and more comprehensive capabilities.</span></span> <span data-ttu-id="9cda6-519">무료 Machine Learning 환경을 선택하려면 [https://studio.azureml.net](https://studio.azureml.net) 에서 **시작하기**를 클릭하고 **게스트 액세스**를 선택하거나 Microsoft 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9cda6-519">To choose your free Machine Learning experience, click **Get started** on [https://studio.azureml.net](https://studio.azureml.net), and then select **Guess Access** or sign in with a Microsoft account.</span></span>

<!-- Module References -->
[image-reader]: https://msdn.microsoft.com/library/azure/893f8c57-1d36-456d-a47b-d29ae67f5d84/
[join]: https://msdn.microsoft.com/library/azure/124865f7-e901-4656-adac-f4cb08248099/
[machine-learning-modules]: https://msdn.microsoft.com/library/azure/6d9e2516-1343-4859-a3dc-9673ccec9edc/
[partition-and-sample]: https://msdn.microsoft.com/library/azure/a8726e34-1b3e-4515-b59a-3e4a475654b8/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[export-data]: https://msdn.microsoft.com/library/azure/7A391181-B6A7-4AD4-B82D-E419C0D6522C
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[python]: https://msdn.microsoft.com/library/azure/CDB56F95-7F4C-404D-BDE7-5BB972E6F232
[counts]: https://msdn.microsoft.com/library/azure/dn913056.aspx
