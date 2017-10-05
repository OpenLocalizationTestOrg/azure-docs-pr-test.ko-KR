---
title: "팀 데이터 과학 프로세스용 Hadoop 클러스터 사용자 지정 | Microsoft Docs"
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
ms.openlocfilehash: 53ff04ee66b08ae36f3550536c659a547c658fd9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="customize-azure-hdinsight-hadoop-clusters-for-the-team-data-science-process"></a><span data-ttu-id="1f577-103">팀 데이터 과학 프로세스용 Azure HDInsight Hadoop 클러스터 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="1f577-103">Customize Azure HDInsight Hadoop clusters for the Team Data Science Process</span></span>
<span data-ttu-id="1f577-104">이 문서에서는 HDInsight 서비스로 클러스터를 프로비전할 때 64비트 Anaconda(Python 2.7)를 각 노드에 설치하여 HDInsight Hadoop 클러스터를 사용자 지정하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-104">This article describes how to customize an HDInsight Hadoop cluster by installing 64-bit Anaconda (Python 2.7) on each node when the cluster is provisioned as an HDInsight service.</span></span> <span data-ttu-id="1f577-105">또한 헤드 노드에 액세스하여 사용자 지정 작업을 클러스터에 제출하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-105">It also shows how to access the headnode to submit custom jobs to the cluster.</span></span> <span data-ttu-id="1f577-106">이 사용자 지정을 통해 클러스터에서 Hive 레코드를 처리하도록 설계된 UDF(사용자 정의 함수)에서 Anaconda에 포함된 널리 사용되는 많은 Python 모듈을 편리하게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-106">This customization makes many popular Python modules, that are included in Anaconda, conveniently available for use in user defined functions (UDFs) that are designed to process Hive records in the cluster.</span></span> <span data-ttu-id="1f577-107">이 시나리오에 사용되는 프로시저에 대한 지침은 [Hive 쿼리를 제출하는 방법](machine-learning-data-science-move-hive-tables.md#submit)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f577-107">For instructions on the procedures used in this scenario, see [How to submit Hive queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

<span data-ttu-id="1f577-108">다음 메뉴는 [TDSP(팀 데이터 과학 프로세스)](data-science-process-overview.md)에서 사용되는 다양한 데이터 과학 환경의 설정 방법을 설명하는 항목에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-108">The following menu links to topics that describe how to set up the various data science environments used by the [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

## <span data-ttu-id="1f577-109"><a name="customize"></a>Azure HDInsight Hadoop 클러스터 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="1f577-109"><a name="customize"></a>Customize Azure HDInsight Hadoop Cluster</span></span>
<span data-ttu-id="1f577-110">사용자 지정 HDInsight Hadoop 클러스터를 만들려면 [**Azure 클래식 포털**](https://manage.windowsazure.com/)에 로그온한 후 왼쪽 아래에서 **새로 만들기**를 클릭한 다음 Data Services -> HDINSIGHT -> **사용자 지정 만들기**를 선택하여 **클러스터 세부 정보** 창을 불러와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-110">To create a customized HDInsight Hadoop cluster, start by logging on to [**Azure classic portal**](https://manage.windowsazure.com/), click **New** at the left bottom corner, and then select DATA SERVICES -> HDINSIGHT -> **CUSTOM CREATE** to bring up the **Cluster Details** window.</span></span> 

![작업 영역 만들기](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="1f577-112">구성 페이지 1에서 만들려는 클러스터의 이름을 입력하고 나머지 필드에서는 기본값을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-112">Input the name of the cluster to be created on configuration page 1, and accept default values for the other fields.</span></span> <span data-ttu-id="1f577-113">화살표를 클릭하여 다음 구성 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-113">Click the arrow to go to the next configuration page.</span></span> 

![작업 영역 만들기](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="1f577-115">구성 페이지 2에서 **데이터 노드** 수를 입력하고 **지역/가상 네트워크**를 선택한 다음 **헤드 노드** 및 **데이터 노드**의 크기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-115">On configuration page 2, input the number of **DATA NODES**, select the **REGION/VIRTUAL NETWORK**, and select the sizes of the **HEAD NODE** and the **DATA NODE**.</span></span> <span data-ttu-id="1f577-116">화살표를 클릭하여 다음 구성 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-116">Click the arrow to go to the next configuration page.</span></span>

> [!NOTE]
> <span data-ttu-id="1f577-117">**지역/가상 네트워크** 는 HDInsight Hadoop 클러스터에 사용할 저장소 계정의 지역과 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-117">The **REGION/VIRTUAL NETWORK** has to be the same as the region of the storage account that is going to be used for the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="1f577-118">그렇지 않으면 네 번째 구성 페이지에서 저장소 계정이 **계정 이름** 드롭다운 목록에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-118">Otherwise, in the fourth configuration page, the storage account will not appear on the dropdown list of **ACCOUNT NAME**.</span></span>
> 
> 

![작업 영역 만들기](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img3.png)

<span data-ttu-id="1f577-120">구성 페이지 3에서 HDInsight Hadoop 클러스터의 사용자 이름 및 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-120">On configuration page 3, provide a user name and password for the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="1f577-121">*Hive/Oozie Metastore 입력*은 선택하지 **마세요**.</span><span class="sxs-lookup"><span data-stu-id="1f577-121">**Do not** select the *Enter the Hive/Oozie Metastore*.</span></span> <span data-ttu-id="1f577-122">그런 다음 화살표를 클릭하여 다음 구성 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-122">Then, click the arrow to go to the next configuration page.</span></span> 

![작업 영역 만들기](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img4.png)

<span data-ttu-id="1f577-124">구성 페이지 4에서 HDInsight Hadoop 클러스터의 기본 컨테이너인 저장소 계정 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-124">On configuration page 4, specify the storage account name, the default container of the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="1f577-125">**기본 컨테이너** 드롭다운 목록에서 *기본 컨테이너 만들기*를 선택한 경우 클러스터와 이름이 같은 컨테이너가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-125">If you select *Create default container* in the **DEFAULT CONTAINER** dropdown list, a container with the same name as the cluster will be created.</span></span> <span data-ttu-id="1f577-126">화살표를 클릭하여 마지막 구성 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-126">Click the arrow to go to the last configuration page.</span></span>

![작업 영역 만들기](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img5.png)

<span data-ttu-id="1f577-128">마지막 **스크립트 동작** 구성 페이지에서 **스크립트 동작 추가** 단추를 클릭하고 텍스트 필드를 다음 값으로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-128">On the final **Script Actions** configuration page, click **add script action** button, and fill the text fields with the following values.</span></span>

* <span data-ttu-id="1f577-129">**이름** - 이 스크립트 동작의 이름인 모든 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-129">**NAME** - any string as the name of this script action</span></span>
* <span data-ttu-id="1f577-130">**노드 유형** - **모든 노드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-130">**NODE TYPE** - select **All nodes**</span></span>
* <span data-ttu-id="1f577-131">**스크립트 URI** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span><span class="sxs-lookup"><span data-stu-id="1f577-131">**SCRIPT URI** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span></span> 
  * <span data-ttu-id="1f577-132">*publicscripts*는 저장소 계정의 공용 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-132">*publicscripts* is a public container in the storage account</span></span> 
  * <span data-ttu-id="1f577-133">*getgoing*은 Azure에서 사용자의 작업을 용이하게 하기 위해 PowerShell 스크립트 파일을 공유하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-133">*getgoing* we use to share PowerShell script files to facilitate users' work in Azure</span></span>
* <span data-ttu-id="1f577-134">**매개 변수** - 비어 있는 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-134">**PARAMETERS** - (leave blank)</span></span>

<span data-ttu-id="1f577-135">마지막으로 확인 표시를 클릭하여 사용자 지정 HDInsight Hadoop 클러스터 만들기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-135">Finally, click the check mark to start the creation of the customized HDInsight Hadoop cluster.</span></span> 

![작업 영역 만들기](./media/machine-learning-data-science-customize-hadoop-cluster/script-actions.png)

## <span data-ttu-id="1f577-137"><a name="headnode"></a> Hadoop 클러스터의 헤드 노드 액세스</span><span class="sxs-lookup"><span data-stu-id="1f577-137"><a name="headnode"></a> Access the Head Node of Hadoop Cluster</span></span>
<span data-ttu-id="1f577-138">RDP를 통해 Hadoop 클러스터의 헤드 노드에 액세스하려면 먼저 Azure에서 Hadoop 클러스터에 대한 원격 액세스를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-138">You must enable remote access to the Hadoop cluster in Azure before you can access the head node of the Hadoop cluster through RDP.</span></span> 

1. <span data-ttu-id="1f577-139">[**Azure 클래식 포털**](https://manage.windowsazure.com/)에 로그인하여 왼쪽에서 **HDInsight**를 선택하고 클러스터 목록에서 Hadoop 클러스터를 선택한 후 **구성** 탭을 클릭하고 페이지 아래쪽에서 **원격 사용** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-139">Log in to the [**Azure classic portal**](https://manage.windowsazure.com/), select **HDInsight** on the left, select your Hadoop cluster from the list of clusters, click the **CONFIGURATION** tab, and then click the **ENABLE REMOTE** icon at the bottom of the page.</span></span>
   
    ![작업 영역 만들기](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-1.png)
2. <span data-ttu-id="1f577-141">**원격 데스크톱 구성** 창에서 사용자 이름 및 암호 필드를 입력하고 원격 액세스의 만료 날짜를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-141">In the **Configure Remote Desktop** window, enter the USER NAME and PASSWORD fields, and select the expiration date for remote access.</span></span> <span data-ttu-id="1f577-142">그런 다음 확인 표시를 클릭하여 Hadoop 클러스터의 헤드 노드에 대한 원격 액세스를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-142">Then click the check mark to enable the remote access to the head node of the Hadoop cluster.</span></span>
   
    ![작업 영역 만들기](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-2.png)

> [!NOTE]
> <span data-ttu-id="1f577-144">원격 액세스용 사용자 이름 및 암호는 Hadoop 클러스터를 만들 때 사용하는 사용자 이름 및 암호가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-144">The user name and password for the remote access are not the user name and password that you use when you created the Hadoop cluster.</span></span> <span data-ttu-id="1f577-145">이는 별도의 자격 증명 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-145">This is a separate set of credentials.</span></span> <span data-ttu-id="1f577-146">또한 원격 액세스의 만료 날짜는 현재 날짜로부터 7일 이내여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-146">Also, the expiration date of the remote access has to be within 7 days from the current date.</span></span>
> 
> 

<span data-ttu-id="1f577-147">원격 액세스를 설정한 후에는 페이지 아래쪽에서 **연결** 을 클릭하여 헤드 노드로 원격 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-147">After remote access is enabled, click **CONNECT** at the bottom of the page to remote into the head node.</span></span> <span data-ttu-id="1f577-148">이전에 지정한 원격 액세스 사용자의 자격 증명을 입력하여 Hadoop 클러스터의 헤드 노드에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-148">You log on to the head node of the Hadoop cluster by entering the credentials for the remote access user that you specified earlier.</span></span>

![작업 영역 만들기](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-3.png)

<span data-ttu-id="1f577-150">고급 분석 프로세스의 다음 단계는 [TDSP(팀 데이터 과학 프로세스)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)에서 매핑되며, 데이터를 HDInsight로 이동한 후 Azure Machine Learning에서 데이터를 통해 학습할 준비를 수행하면서 데이터를 처리 및 샘플링하는 단계를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f577-150">The next steps in the advanced analytics process are mapped in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into HDInsight, then process and sample it there in preparation for learning from the data with Azure Machine Learning.</span></span>

<span data-ttu-id="1f577-151">클러스터에 저장된 Hive 레코드를 처리하는 데 사용된 UDF(사용자 정의 함수)의 클러스터 헤드 노드에서 Anaconda에 포함된 Python 모듈에 액세스하는 방법에 대한 지침은 [Hive 쿼리를 제출하는 방법](machine-learning-data-science-move-hive-tables.md#submit)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f577-151">See [How to submit Hive queries](machine-learning-data-science-move-hive-tables.md#submit) for instructions on how to access the Python modules that are included in Anaconda from the head node of the cluster in user-defined functions (UDFs) that are used to process Hive records stored in the cluster.</span></span>

