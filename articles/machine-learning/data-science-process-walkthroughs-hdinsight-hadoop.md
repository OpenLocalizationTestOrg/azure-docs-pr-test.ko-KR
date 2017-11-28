---
title: "Azure에서 Hive를 사용하여 HDInsight Hadoop 데이터 과학 연습 | Microsoft Docs"
description: "예측 분석을 수행하기 위해 Azure HDInsight Hadoop에서 Hive 사용을 보여 주는 Team Data Science Process의 예제입니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev
ms.openlocfilehash: fb06c3c1b1ae30d970a2e4d45a49e22e9d78b876
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="hdinsight-hadoop-data-science-walkthroughs-using-hive-on-azure"></a><span data-ttu-id="c6961-103">Azure에서 Hive를 사용하여 HDInsight Hadoop 데이터 과학 연습</span><span class="sxs-lookup"><span data-stu-id="c6961-103">HDInsight Hadoop data science walkthroughs using Hive on Azure</span></span> 

<span data-ttu-id="c6961-104">이 연습에서는 HDInsight Hadoop 클러스터와 Hive를 사용하여 예측 분석을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c6961-104">These walkthroughs use Hive with an HDInsight Hadoop cluster to do predictive analytics.</span></span> <span data-ttu-id="c6961-105">Team Data Science Process에 설명된 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c6961-105">They follow the steps outlined in the Team Data Science Process.</span></span> <span data-ttu-id="c6961-106">Team Data Science Process의 개요는 [데이터 과학 프로세스](data-science-process-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c6961-106">For an overview of the Team Data Science Process, see [Data Science Process](data-science-process-overview.md).</span></span> <span data-ttu-id="c6961-107">Azure HDInsight에 대한 소개는 [Azure HDInsight, Hadoop 기술 스택 및 Hadoop 클러스터에 대한 소개](../hdinsight/hdinsight-hadoop-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c6961-107">For an introduction to Azure HDInsight, see [Introduction to Azure HDInsight, the Hadoop technology stack, and Hadoop clusters](../hdinsight/hdinsight-hadoop-introduction.md).</span></span>

<span data-ttu-id="c6961-108">Team Data Science Process를 실행하는 추가 데이터 과학 연습은 사용하는 **플랫폼**에 따라 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6961-108">Additional data science walkthroughs that execute the Team Data Science Process are grouped by the **platform** that they use:</span></span> 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]


## <a name="predict-taxi-tips-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="c6961-109">HDInsight Hadoop와 함께 Hive를 사용하여 택시 팁 예측</span><span class="sxs-lookup"><span data-stu-id="c6961-109">Predict taxi tips using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="c6961-110">[HDInsight Hadoop 클러스터 사용](machine-learning-data-science-process-hive-walkthrough.md) 연습은 뉴욕 택시에서 데이터를 사용하여 다음을 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="c6961-110">The [Use HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) walkthrough uses data from New York taxis to predict:</span></span> 

- <span data-ttu-id="c6961-111">팁 지불 여부</span><span class="sxs-lookup"><span data-stu-id="c6961-111">Whether a tip is paid</span></span> 
- <span data-ttu-id="c6961-112">팁 금액의 분포</span><span class="sxs-lookup"><span data-stu-id="c6961-112">The distribution of tip amounts</span></span>

<span data-ttu-id="c6961-113">시나리오는 [Azure HDInsight Hadoop 클러스터](https://azure.microsoft.com/services/hdinsight/)와 함께 Hive를 사용하여 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6961-113">The scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/).</span></span> <span data-ttu-id="c6961-114">공개적으로 사용할 수 있는 NYC Taxi Trip 및 요금 데이터 집합에서 데이터를 저장, 탐색 및 기능 엔지니어링하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="c6961-114">You learn how to store, explore, and feature engineer data from a publicly available NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="c6961-115">또한 Azure Machine Learning을 사용하여 모델을 빌드 및 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6961-115">You also use Azure Machine Learning to build and deploy the models.</span></span>

## <a name="predict-advertisement-clicks-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="c6961-116">HDInsight Hadoop와 함께 Hive를 사용하여 광고 클릭 예측</span><span class="sxs-lookup"><span data-stu-id="c6961-116">Predict advertisement clicks using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="c6961-117">[1TB 데이터 집합에서 Azure HDInsight Hadoop 클러스터 사용](machine-learning-data-science-process-hive-criteo-walkthrough.md) 연습에서는 공개적으로 사용할 수 있는 [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) 클릭 데이터 집합을 사용하여 팁 지불 여부와 예상하는 금액 범위를 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="c6961-117">The [Use Azure HDInsight Hadoop Clusters on a 1-TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md) walkthrough uses a publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) click dataset to predict whether a tip is paid and the range of amounts expected.</span></span> <span data-ttu-id="c6961-118">시나리오는 샘플 데이터를 저장, 탐색, 기능 엔지니어링 및 다운하기 위해 [Azure HDInsight Hadoop 클러스터](https://azure.microsoft.com/services/hdinsight/)와 함께 Hive를 사용하여 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6961-118">The scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore, feature engineer, and down sample data.</span></span> <span data-ttu-id="c6961-119">Azure Machine Learning을 사용하여 광고에 대한 사용자 클릭 여부를 예측하는 이진 분류 모델을 빌드, 학습 및 점수 매깁니다.</span><span class="sxs-lookup"><span data-stu-id="c6961-119">It uses Azure Machine Learning to build, train, and score a binary classification model predicting whether a user clicks on an advertisement.</span></span> <span data-ttu-id="c6961-120">연습은 이러한 모델 중 하나를 웹 서비스로 게시하는 방법을 보여 주는 것으로 마칩니다.</span><span class="sxs-lookup"><span data-stu-id="c6961-120">The walkthrough concludes showing how to publish one of these models as a Web service.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c6961-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c6961-121">Next steps</span></span>

<span data-ttu-id="c6961-122">Team Data Science Process를 구성하는 주요 구성의 논의는 [Team Data Science Process 개요](data-science-process-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c6961-122">For a discussion of the key components that comprise the Team Data Science Process, see [Team Data Science Process overview](data-science-process-overview.md).</span></span>

<span data-ttu-id="c6961-123">데이터 과학 프로젝트를 구성하는 데 사용할 수 있는 Team Data Science Process 수명 주기의 논의는 [Team Data Science Process 수명 주기](data-science-process-lifecycle.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c6961-123">For a discussion of the Team Data Science Process lifecycle that you can use to structure your data science projects, see [Team Data Science Process lifecycle](data-science-process-lifecycle.md).</span></span> <span data-ttu-id="c6961-124">수명 주기는 일반적으로 프로젝트가 실행될 때 시작부터 끝까지 따라야 하는 단계를 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c6961-124">The lifecycle outlines the steps, from start to finish, that projects usually follow when they are executed.</span></span> 

