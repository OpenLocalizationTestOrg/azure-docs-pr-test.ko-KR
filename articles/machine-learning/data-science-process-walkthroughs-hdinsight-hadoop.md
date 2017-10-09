---
title: "하이브를 사용 하 여 Azure에서 aaaHDInsight Hadoop 데이터 과학 연습 | Microsoft Docs"
description: "Azure HDInsight Hadoop toodo 예측 분석에서 하이브 hello 사용 안내는 hello 팀 데이터 과학 프로세스의 예제입니다."
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
ms.openlocfilehash: 77efbe4ea6377f309987849d9f44e8b2b859ae9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="hdinsight-hadoop-data-science-walkthroughs-using-hive-on-azure"></a><span data-ttu-id="7b00b-103">Azure에서 Hive를 사용하여 HDInsight Hadoop 데이터 과학 연습</span><span class="sxs-lookup"><span data-stu-id="7b00b-103">HDInsight Hadoop data science walkthroughs using Hive on Azure</span></span> 

<span data-ttu-id="7b00b-104">이 연습에서는 HDInsight Hadoop 클러스터 toodo 예측 분석으로 하이브를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b00b-104">These walkthroughs use Hive with an HDInsight Hadoop cluster toodo predictive analytics.</span></span> <span data-ttu-id="7b00b-105">Hello 팀 데이터 과학 프로세스에에서 설명 된 hello 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="7b00b-105">They follow hello steps outlined in hello Team Data Science Process.</span></span> <span data-ttu-id="7b00b-106">Hello 팀 데이터 과학 프로세스의 개요를 참조 하십시오. [데이터 과학 프로세스](data-science-process-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b00b-106">For an overview of hello Team Data Science Process, see [Data Science Process](data-science-process-overview.md).</span></span> <span data-ttu-id="7b00b-107">HDInsight는 소개 tooAzure 참조 [소개 tooAzure HDInsight Hadoop 클러스터 및 Hadoop 기술 스택에서 hello](../hdinsight/hdinsight-hadoop-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b00b-107">For an introduction tooAzure HDInsight, see [Introduction tooAzure HDInsight, hello Hadoop technology stack, and Hadoop clusters](../hdinsight/hdinsight-hadoop-introduction.md).</span></span>

<span data-ttu-id="7b00b-108">Hello 팀 데이터 과학 프로세스를 실행 하는 추가 데이터 과학 연습 hello 별로 그룹화 되어 **플랫폼** 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b00b-108">Additional data science walkthroughs that execute hello Team Data Science Process are grouped by hello **platform** that they use:</span></span> 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]


## <a name="predict-taxi-tips-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="7b00b-109">HDInsight Hadoop와 함께 Hive를 사용하여 택시 팁 예측</span><span class="sxs-lookup"><span data-stu-id="7b00b-109">Predict taxi tips using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="7b00b-110">hello [사용할 HDInsight Hadoop 클러스터](machine-learning-data-science-process-hive-walkthrough.md) 연습 뉴욕 택시 toopredict의 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b00b-110">hello [Use HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) walkthrough uses data from New York taxis toopredict:</span></span> 

- <span data-ttu-id="7b00b-111">팁 지불 여부</span><span class="sxs-lookup"><span data-stu-id="7b00b-111">Whether a tip is paid</span></span> 
- <span data-ttu-id="7b00b-112">포함 된 팁 hello 배포</span><span class="sxs-lookup"><span data-stu-id="7b00b-112">hello distribution of tip amounts</span></span>

<span data-ttu-id="7b00b-113">hello 시나리오가 Hive 사용를 사용 하 여 구현 되는 [Azure HDInsight Hadoop 클러스터](https://azure.microsoft.com/services/hdinsight/)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b00b-113">hello scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/).</span></span> <span data-ttu-id="7b00b-114">Toostore를 탐색 및 기능에서 사용 가능한 공개 NYC 택시 여행 엔지니어 데이터 및 데이터 집합이 있어 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="7b00b-114">You learn how toostore, explore, and feature engineer data from a publicly available NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="7b00b-115">또한 Azure 기계 학습 toobuild를 사용 하 고 hello 모델을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b00b-115">You also use Azure Machine Learning toobuild and deploy hello models.</span></span>

## <a name="predict-advertisement-clicks-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="7b00b-116">HDInsight Hadoop와 함께 Hive를 사용하여 광고 클릭 예측</span><span class="sxs-lookup"><span data-stu-id="7b00b-116">Predict advertisement clicks using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="7b00b-117">hello [1TB 데이터 집합에서 사용 하 여 Azure HDInsight Hadoop 클러스터](machine-learning-data-science-process-hive-criteo-walkthrough.md) 연습에서는 공개적으로 사용할 수 있는 사용 [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) 팁을 지불 하 고 포함 된 예상 범위 hello 여부를 데이터 집합 toopredict를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b00b-117">hello [Use Azure HDInsight Hadoop Clusters on a 1-TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md) walkthrough uses a publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) click dataset toopredict whether a tip is paid and hello range of amounts expected.</span></span> <span data-ttu-id="7b00b-118">hello 시나리오가 Hive 사용를 사용 하 여 구현 되는 [Azure HDInsight Hadoop 클러스터](https://azure.microsoft.com/services/hdinsight/) toostore, 탐색, 엔지니어, 기능 및 예제 데이터를 아래쪽입니다.</span><span class="sxs-lookup"><span data-stu-id="7b00b-118">hello scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) toostore, explore, feature engineer, and down sample data.</span></span> <span data-ttu-id="7b00b-119">Azure 기계 학습 toobuild 사용 하 여, 학습 및 점수 사용자 광고를 클릭할 수 있는지 여부를 예측 하는 이진 분류 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="7b00b-119">It uses Azure Machine Learning toobuild, train, and score a binary classification model predicting whether a user clicks on an advertisement.</span></span> <span data-ttu-id="7b00b-120">hello 연습으로 어떻게 toopublish 다음 중 하나를 모델링 웹 서비스로 표시를 마칩니다.</span><span class="sxs-lookup"><span data-stu-id="7b00b-120">hello walkthrough concludes showing how toopublish one of these models as a Web service.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7b00b-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7b00b-121">Next steps</span></span>

<span data-ttu-id="7b00b-122">Hello 팀 데이터 과학 프로세스를 구성 하는 hello 주요 구성 요소의 논의 알려면 [팀 데이터 과학 프로세스 개요](data-science-process-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b00b-122">For a discussion of hello key components that comprise hello Team Data Science Process, see [Team Data Science Process overview](data-science-process-overview.md).</span></span>

<span data-ttu-id="7b00b-123">데이터 과학 프로젝트, 참조에 대 한 설명은 한 toostructure를 사용할 수 있는 hello 팀 데이터 과학 프로세스 수명 주기 [팀 데이터 과학 프로세스 수명 주기](data-science-process-lifecycle.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b00b-123">For a discussion of hello Team Data Science Process lifecycle that you can use toostructure your data science projects, see [Team Data Science Process lifecycle](data-science-process-lifecycle.md).</span></span> <span data-ttu-id="7b00b-124">hello 수명 주기에서 다음에 나오는 프로젝트 일반적으로 실행 될 때 시작 toofinish hello 단계를 간략하게 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b00b-124">hello lifecycle outlines hello steps, from start toofinish, that projects usually follow when they are executed.</span></span> 

