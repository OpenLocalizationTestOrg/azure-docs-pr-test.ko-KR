---
title: "hello 팀 데이터 과학 프로세스에 대 한 aaaCustomize Hadoop 클러스터 | Microsoft Docs"
description: "일반적인 Python 모듈을 사용자 지정 Azure HDInsight Hadoop 클러스터에서 사용할 수 있습니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0c115dca-2565-4e7a-9536-6002af5c786a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: e192542dd39f71bccbb5163382b4050d0f12ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-azure-hdinsight-hadoop-clusters-for-hello-team-data-science-process"></a><span data-ttu-id="7ad9b-103">Hello 팀 데이터 과학 프로세스에 대 한 Azure HDInsight Hadoop 클러스터를 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="7ad9b-103">Customize Azure HDInsight Hadoop clusters for hello Team Data Science Process</span></span>
<span data-ttu-id="7ad9b-104">이 문서에서는 64 비트 Anaconda (Python 2.7)를 설치 하 여 toocustomize HDInsight Hadoop 클러스터 방법을 각 노드에서 hello 클러스터는 HDInsight 서비스로 프로 비전 될 때</span><span class="sxs-lookup"><span data-stu-id="7ad9b-104">This article describes how toocustomize an HDInsight Hadoop cluster by installing 64-bit Anaconda (Python 2.7) on each node when hello cluster is provisioned as an HDInsight service.</span></span> <span data-ttu-id="7ad9b-105">또한 tooaccess toosubmit 사용자 지정 작업 toohello 클러스터 헤드 노드에 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-105">It also shows how tooaccess hello headnode toosubmit custom jobs toohello cluster.</span></span> <span data-ttu-id="7ad9b-106">이 사용자 지정 여러 인기 있는 Python 모듈, Anaconda에 포함 된으로 편리 하 게에 사용할 수 있는 사용자 정의 함수 (Udf)를 tooprocess hello 클러스터의 Hive 레코드 설계 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-106">This customization makes many popular Python modules, that are included in Anaconda, conveniently available for use in user defined functions (UDFs) that are designed tooprocess Hive records in hello cluster.</span></span> <span data-ttu-id="7ad9b-107">이 시나리오에서 사용 하는 hello 프로시저에 대 한 자세한 내용은 참조 하십시오. [어떻게 toosubmit 하이브 쿼리](machine-learning-data-science-move-hive-tables.md#submit)합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-107">For instructions on hello procedures used in this scenario, see [How toosubmit Hive queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

<span data-ttu-id="7ad9b-108">hello 다음과 같은 메뉴가 링크 tooset hello 다양 한 데이터 과학 환경에서 어떻게 사용 hello를 설명 하는 tootopics [팀 데이터 과학 프로세스 (TDSP)](data-science-process-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-108">hello following menu links tootopics that describe how tooset up hello various data science environments used by hello [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

## <span data-ttu-id="7ad9b-109"><a name="customize"></a>Azure HDInsight Hadoop 클러스터 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="7ad9b-109"><a name="customize"></a>Customize Azure HDInsight Hadoop Cluster</span></span>
<span data-ttu-id="7ad9b-110">사용자 지정 된 HDInsight Hadoop 클러스터 toocreate 너무 로그온 하 여 시작[**Azure 클래식 포털**](https://manage.windowsazure.com/), 클릭 **새로** hello 왼쪽에 아래 모퉁이 한 다음 데이터 서비스를 선택 HDINSIGHT->-> **사용자 지정 만들기** hello toobring **클러스터 세부 정보** 창.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-110">toocreate a customized HDInsight Hadoop cluster, start by logging on too[**Azure classic portal**](https://manage.windowsazure.com/), click **New** at hello left bottom corner, and then select DATA SERVICES -> HDINSIGHT -> **CUSTOM CREATE** toobring up hello **Cluster Details** window.</span></span> 

![작업 영역 만들기](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="7ad9b-112">1, 구성 페이지에서 만든 hello 클러스터 toobe의 hello 이름을 입력 하 고 다른 필드 hello에 대 한 기본값을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-112">Input hello name of hello cluster toobe created on configuration page 1, and accept default values for hello other fields.</span></span> <span data-ttu-id="7ad9b-113">Hello 화살표 toogo toohello 다음 구성 페이지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-113">Click hello arrow toogo toohello next configuration page.</span></span> 

![작업 영역 만들기](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="7ad9b-115">구성 페이지 2의 hello 수를 입력 **데이터 노드**선택, hello **지역/가상 네트워크**의 hello hello 크기를 선택 하 고 **헤드 노드** 및 hello **데이터 노드**합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-115">On configuration page 2, input hello number of **DATA NODES**, select hello **REGION/VIRTUAL NETWORK**, and select hello sizes of hello **HEAD NODE** and hello **DATA NODE**.</span></span> <span data-ttu-id="7ad9b-116">Hello 화살표 toogo toohello 다음 구성 페이지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-116">Click hello arrow toogo toohello next configuration page.</span></span>

> [!NOTE]
> <span data-ttu-id="7ad9b-117">hello **지역/가상 네트워크** toobe toobe hello HDInsight Hadoop 클러스터에 사용 되는 이동 하는 hello 저장소 계정의 hello 영역으로 hello 동일 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-117">hello **REGION/VIRTUAL NETWORK** has toobe hello same as hello region of hello storage account that is going toobe used for hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="7ad9b-118">그렇지 않으면 hello 네 번째 구성 페이지에서 hello 저장소 계정에 표시 되지 것입니다 hello 드롭다운 목록이 **계정 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-118">Otherwise, in hello fourth configuration page, hello storage account will not appear on hello dropdown list of **ACCOUNT NAME**.</span></span>
> 
> 

![작업 영역 만들기](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img3.png)

<span data-ttu-id="7ad9b-120">구성 페이지 3 hello HDInsight Hadoop 클러스터에 대 한 사용자 이름 및 암호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-120">On configuration page 3, provide a user name and password for hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="7ad9b-121">**없는** 선택 hello *Enter hello Hive/Oozie Metastore*합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-121">**Do not** select hello *Enter hello Hive/Oozie Metastore*.</span></span> <span data-ttu-id="7ad9b-122">그런 다음 hello 화살표 toogo toohello 다음 구성 페이지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-122">Then, click hello arrow toogo toohello next configuration page.</span></span> 

![작업 영역 만들기](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img4.png)

<span data-ttu-id="7ad9b-124">구성 페이지 4 hello 저장소 계정 이름, hello HDInsight Hadoop 클러스터의 hello 기본 컨테이너를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-124">On configuration page 4, specify hello storage account name, hello default container of hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="7ad9b-125">선택 하는 경우 *기본 컨테이너 만들기* hello에 **기본 컨테이너** 드롭다운 목록, hello 사용 하 여 컨테이너 이름과 같은 이름을 hello 클러스터를 만들 때.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-125">If you select *Create default container* in hello **DEFAULT CONTAINER** dropdown list, a container with hello same name as hello cluster will be created.</span></span> <span data-ttu-id="7ad9b-126">Hello 화살표 toogo toohello 마지막 구성 페이지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-126">Click hello arrow toogo toohello last configuration page.</span></span>

![작업 영역 만들기](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img5.png)

<span data-ttu-id="7ad9b-128">최종 hello에 **스크립트 동작** 구성 페이지에서 클릭 **스크립트 동작 추가** 단추를 클릭 한 다음 값에는 hello로 hello 텍스트 필드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-128">On hello final **Script Actions** configuration page, click **add script action** button, and fill hello text fields with hello following values.</span></span>

* <span data-ttu-id="7ad9b-129">**이름** -hello 이름과이 스크립트 동작의 모든 문자열</span><span class="sxs-lookup"><span data-stu-id="7ad9b-129">**NAME** - any string as hello name of this script action</span></span>
* <span data-ttu-id="7ad9b-130">**노드 유형** - **모든 노드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-130">**NODE TYPE** - select **All nodes**</span></span>
* <span data-ttu-id="7ad9b-131">**스크립트 URI** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span><span class="sxs-lookup"><span data-stu-id="7ad9b-131">**SCRIPT URI** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span></span> 
  * <span data-ttu-id="7ad9b-132">*publicscripts* 은 hello 저장소 계정에서 공용 컨테이너</span><span class="sxs-lookup"><span data-stu-id="7ad9b-132">*publicscripts* is a public container in hello storage account</span></span> 
  * <span data-ttu-id="7ad9b-133">*getgoing* tooshare PowerShell 스크립트 파일 toofacilitate 사용자 작업 사용 하 여 Azure에서</span><span class="sxs-lookup"><span data-stu-id="7ad9b-133">*getgoing* we use tooshare PowerShell script files toofacilitate users' work in Azure</span></span>
* <span data-ttu-id="7ad9b-134">**매개 변수** - 비어 있는 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-134">**PARAMETERS** - (leave blank)</span></span>

<span data-ttu-id="7ad9b-135">마지막으로, 사용자 지정 하는 hello HDInsight Hadoop 클러스터 hello 확인 표시가 toostart hello 만들기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-135">Finally, click hello check mark toostart hello creation of hello customized HDInsight Hadoop cluster.</span></span> 

![작업 영역 만들기](./media/machine-learning-data-science-customize-hadoop-cluster/script-actions.png)

## <span data-ttu-id="7ad9b-137"><a name="headnode"></a>액세스 hello Hadoop 클러스터의 헤드 노드</span><span class="sxs-lookup"><span data-stu-id="7ad9b-137"><a name="headnode"></a> Access hello Head Node of Hadoop Cluster</span></span>
<span data-ttu-id="7ad9b-138">RDP를 통해 hello Hadoop 클러스터의 헤드 노드 hello에 액세스 하려면 먼저 Azure에서 원격 액세스 toohello Hadoop 클러스터를 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-138">You must enable remote access toohello Hadoop cluster in Azure before you can access hello head node of hello Hadoop cluster through RDP.</span></span> 

1. <span data-ttu-id="7ad9b-139">Toohello 로그인 [ **Azure 클래식 포털**](https://manage.windowsazure.com/)선택, **HDInsight** hello 왼쪽에 클러스터의 hello 목록에서 Hadoop 클러스터를 선택, hello  **구성** 탭을 클릭 한 다음 hello **원격 사용** hello hello 페이지 맨 위에 있는 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-139">Log in toohello [**Azure classic portal**](https://manage.windowsazure.com/), select **HDInsight** on hello left, select your Hadoop cluster from hello list of clusters, click hello **CONFIGURATION** tab, and then click hello **ENABLE REMOTE** icon at hello bottom of hello page.</span></span>
   
    ![작업 영역 만들기](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-1.png)
2. <span data-ttu-id="7ad9b-141">Hello에 **원격 데스크톱 구성** 창 hello 사용자 이름 및 암호 필드를 입력 하 고 원격 액세스를 위한 hello 만료 날짜를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-141">In hello **Configure Remote Desktop** window, enter hello USER NAME and PASSWORD fields, and select hello expiration date for remote access.</span></span> <span data-ttu-id="7ad9b-142">Hello 확인 표시가 tooenable hello 원격 액세스 toohello 클러스터의 헤드 노드 hello Hadoop 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-142">Then click hello check mark tooenable hello remote access toohello head node of hello Hadoop cluster.</span></span>
   
    ![작업 영역 만들기](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-2.png)

> [!NOTE]
> <span data-ttu-id="7ad9b-144">hello 사용자 이름 및 원격 액세스 hello에 대 한 암호 없는 hello 사용자 이름 및 암호를 hello Hadoop 클러스터를 만들 때 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-144">hello user name and password for hello remote access are not hello user name and password that you use when you created hello Hadoop cluster.</span></span> <span data-ttu-id="7ad9b-145">이는 별도의 자격 증명 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-145">This is a separate set of credentials.</span></span> <span data-ttu-id="7ad9b-146">또한 hello 원격 액세스의 hello 만료 날짜는 현재 날짜 로부터 hello 7 일 이내 toobe 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-146">Also, hello expiration date of hello remote access has toobe within 7 days from hello current date.</span></span>
> 
> 

<span data-ttu-id="7ad9b-147">원격 액세스를 사용 하도록 설정한 후 클릭 **연결** hello 헤드 노드로 hello 페이지 tooremote hello 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-147">After remote access is enabled, click **CONNECT** at hello bottom of hello page tooremote into hello head node.</span></span> <span data-ttu-id="7ad9b-148">이전에 지정한 hello 원격 액세스 사용자에 대 한 hello 자격 증명을 입력 하 여 hello Hadoop 클러스터의 헤드 노드 toohello에 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-148">You log on toohello head node of hello Hadoop cluster by entering hello credentials for hello remote access user that you specified earlier.</span></span>

![작업 영역 만들기](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-3.png)

<span data-ttu-id="7ad9b-150">hello hello 고급 분석 프로세스의에서 다음 단계에에서 매핑된 hello [팀 데이터 과학 프로세스 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) 처리 하 고 hello 데이터 로부터 학습을 위한 준비 과정에서 샘플링 하는 것이 있으면 HDInsight에 테이블로 데이터를 이동 하는 단계를 포함할 수 있습니다 와 Azure 기계 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-150">hello next steps in hello advanced analytics process are mapped in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into HDInsight, then process and sample it there in preparation for learning from hello data with Azure Machine Learning.</span></span>

<span data-ttu-id="7ad9b-151">참조 [어떻게 toosubmit 하이브 쿼리](machine-learning-data-science-move-hive-tables.md#submit) tooaccess hello 사용자 정의 함수 (Udf) 사용 하는 tooprocess 있는 클러스터의 헤드 노드에서 hello Anaconda에 포함 된 Python 모듈 hello 하는 방법에 대 한 지침은 하이브 저장 된 레코드 hello 클러스터에서.</span><span class="sxs-lookup"><span data-stu-id="7ad9b-151">See [How toosubmit Hive queries](machine-learning-data-science-move-hive-tables.md#submit) for instructions on how tooaccess hello Python modules that are included in Anaconda from hello head node of hello cluster in user-defined functions (UDFs) that are used tooprocess Hive records stored in hello cluster.</span></span>

