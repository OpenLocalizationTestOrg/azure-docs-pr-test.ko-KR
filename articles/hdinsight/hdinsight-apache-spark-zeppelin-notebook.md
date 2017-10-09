---
title: "Azure HDInsight의 Apache Spark와 함께 aaaUse 선을 전자 필기장 클러스터 | Microsoft Docs"
description: "Azure HDInsight의 Apache Spark와 함께 toouse 선을 전자 필기장 클러스터 하는 방법에 대해 단계별로 설명 합니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: df489d70-7788-4efa-a089-e5e5006421e2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 3ab479cfccc7fd38a9bf6a9fb4f5928beec8ff7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a><span data-ttu-id="c3b82-103">Azure HDInsight에서 Apache Spark 클러스터와 함께 Zeppelin Notebook 사용</span><span class="sxs-lookup"><span data-stu-id="c3b82-103">Use Zeppelin notebooks with Apache Spark cluster on Azure HDInsight</span></span>

<span data-ttu-id="c3b82-104">HDInsight Spark 클러스터 toorun Spark 작업을 사용할 수 있는 선을 전자 필기장 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-104">HDInsight Spark clusters include Zeppelin notebooks that you can use toorun Spark jobs.</span></span> <span data-ttu-id="c3b82-105">이 문서에서는 toouse HDInsight 클러스터에서 선을 노트북 hello 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-105">In this article, you learn how toouse hello Zeppelin notebook on an HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="c3b82-106">Zeppelin Notebook은 HDInsight 3.5의 Spark 1.6.3 및 HDInsight 3.6의 Spark 2.1.0에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-106">Zeppelin notebooks are available only for Spark 1.6.3 on HDInsight 3.5 and Spark 2.1.0 on HDInsight 3.6.</span></span>
>

<span data-ttu-id="c3b82-107">**필수 조건:**</span><span class="sxs-lookup"><span data-stu-id="c3b82-107">**Prerequisites:**</span></span>

* <span data-ttu-id="c3b82-108">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="c3b82-108">An Azure subscription.</span></span> <span data-ttu-id="c3b82-109">[Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3b82-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="c3b82-110">HDInsight의 Apache Spark 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-110">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="c3b82-111">자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3b82-111">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="launch-a-zeppelin-notebook"></a><span data-ttu-id="c3b82-112">Zeppelin Notebook 시작</span><span class="sxs-lookup"><span data-stu-id="c3b82-112">Launch a Zeppelin notebook</span></span>
1. <span data-ttu-id="c3b82-113">Hello Spark 클러스터 블레이드에서 클릭 **클러스터 대시보드**, 클릭 하 고 **선을 노트북**합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-113">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Zeppelin Notebook**.</span></span> <span data-ttu-id="c3b82-114">메시지가 표시 되 면 hello 클러스터에 대 한 hello 관리자 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-114">If prompted, enter hello admin credentials for hello cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c3b82-115">또한 열어 hello URL을 브라우저에서 다음을 통해 클러스터에 대 한 hello 선을 노트북에 도달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-115">You may also reach hello Zeppelin Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="c3b82-116">대체 **CLUSTERNAME** 클러스터의 hello 이름의:</span><span class="sxs-lookup"><span data-stu-id="c3b82-116">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. <span data-ttu-id="c3b82-117">새 Notebook을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-117">Create a new notebook.</span></span> <span data-ttu-id="c3b82-118">Hello 헤더 창에서 클릭 **노트북**, 클릭 하 고 **만들 새 메모**합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-118">From hello header pane, click **Notebook**, and then click **Create New Note**.</span></span>
   
    <span data-ttu-id="c3b82-119">![새 Zeppelin Notebook 만들기](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "새 Zeppelin Notebook 만들기")</span><span class="sxs-lookup"><span data-stu-id="c3b82-119">![Create a new Zeppelin notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Create a new Zeppelin notebook")</span></span>
   
    <span data-ttu-id="c3b82-120">Hello 전자 필기장에 대 한 이름을 입력 한 다음 클릭 **만들 참고**합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-120">Enter a name for hello notebook, and then click **Create Note**.</span></span>
3. <span data-ttu-id="c3b82-121">연결 된 상태를 표시 하는 hello 노트북 헤더 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-121">Also, make sure hello notebook header shows a connected status.</span></span> <span data-ttu-id="c3b82-122">녹색 점 hello 오른쪽 위 모서리에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-122">It is denoted by a green dot in hello top-right corner.</span></span>
   
    <span data-ttu-id="c3b82-123">![Zeppelin Notebook 상태](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin Notebook 상태")</span><span class="sxs-lookup"><span data-stu-id="c3b82-123">![Zeppelin notebook status](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin notebook status")</span></span>
4. <span data-ttu-id="c3b82-124">샘플 데이터를 임시 테이블에 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-124">Load sample data into a temporary table.</span></span> <span data-ttu-id="c3b82-125">Hello 예제 데이터 파일, HDInsight의 Spark 클러스터를 만들 때 **hvac.csv**, 복사한 toohello 연결 된 저장소 계정에는 **\HdiSamples\SensorSampleData\hvac**합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-125">When you create a Spark cluster in HDInsight, hello sample data file, **hvac.csv**, is copied toohello associated storage account under **\HdiSamples\SensorSampleData\hvac**.</span></span>
   
    <span data-ttu-id="c3b82-126">기본적으로 새 전자 필기장 hello에에서 만들어지는 빈 단락 hello에서 다음 코드 조각 hello를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-126">In hello empty paragraph that is created by default in hello new notebook, paste hello following snippet.</span></span>
   
        %livy.spark
        //hello above magic instructs Zeppelin toouse hello Livy Scala interpreter
   
        // Create an RDD using hello default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map hello values in hello .csv file toohello schema
        val hvac = hvacText.map(s => s.split(",")).filter(s => s(0) != "Date").map(
            s => Hvac(s(0), 
                    s(1),
                    s(2).toInt,
                    s(3).toInt,
                    s(6)
            )
        ).toDF()
   
        // Register as a temporary table called "hvac"
        hvac.registerTempTable("hvac")
   
    <span data-ttu-id="c3b82-127">키를 눌러 **SHIFT + ENTER** hello 키를 누르거나 **재생** hello 단락 toorun hello 조각에 대 한 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-127">Press **SHIFT + ENTER** or click hello **Play** button for hello paragraph toorun hello snippet.</span></span> <span data-ttu-id="c3b82-128">hello 단락의 hello 오른쪽 모서리에서 hello 상태 보류 중, 실행 tooFINISHED 준비에서 진행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-128">hello status on hello right-corner of hello paragraph should progress from READY, PENDING, RUNNING tooFINISHED.</span></span> <span data-ttu-id="c3b82-129">hello 출력에 hello hello 맨 아래에 참석 같은 단락 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-129">hello output shows up at hello bottom of hello same paragraph.</span></span> <span data-ttu-id="c3b82-130">hello 스크린 샷 hello 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-130">hello screenshot looks like hello following:</span></span>
   
    <span data-ttu-id="c3b82-131">![원시 데이터에서 임시 테이블 만들기](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "원시 데이터에서 임시 테이블 만들기")</span><span class="sxs-lookup"><span data-stu-id="c3b82-131">![Create a temporary table from raw data](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Create a temporary table from raw data")</span></span>
   
    <span data-ttu-id="c3b82-132">또한 제목 tooeach 단락을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-132">You can also provide a title tooeach paragraph.</span></span> <span data-ttu-id="c3b82-133">Hello 오른쪽 모서리에서 클릭 hello **설정** 아이콘을 클릭 한 다음 **제목 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-133">From hello right-hand corner, click hello **Settings** icon, and then click **Show title**.</span></span>
5. <span data-ttu-id="c3b82-134">Hello에 이제 Spark SQL 문을 실행할 수 있습니다 **hvac** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-134">You can now run Spark SQL statements on hello **hvac** table.</span></span> <span data-ttu-id="c3b82-135">Hello를 다음 새 단락에서 쿼리를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-135">Paste hello following query in a new paragraph.</span></span> <span data-ttu-id="c3b82-136">hello 쿼리 hello 차이 hello 대상과 특정된 날짜에 각 빌드에 대 한 실제 온도 및 hello 건물 ID를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-136">hello query retrieves hello building ID and hello difference between hello target and actual temperatures for each building on a given date.</span></span> <span data-ttu-id="c3b82-137">**Shift + Enter**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-137">Press **SHIFT + ENTER**.</span></span>
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    <span data-ttu-id="c3b82-138">hello **%sql** hello 시작 부분에는 문을 hello 노트북 toouse hello 리비 Scala 인터프리터를 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-138">hello **%sql** statement at hello beginning tells hello notebook toouse hello Livy Scala interpreter.</span></span>
   
    <span data-ttu-id="c3b82-139">hello 다음 스크린 샷에서 hello 출력이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-139">hello following screenshot shows hello output.</span></span>
   
    <span data-ttu-id="c3b82-140">![Hello 노트북을 사용 하 여 Spark SQL 문을 실행](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "hello 노트북을 사용 하 여 Spark SQL 문 실행")</span><span class="sxs-lookup"><span data-stu-id="c3b82-140">![Run a Spark SQL statement using hello notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "Run a Spark SQL statement using hello notebook")</span></span>
   
     <span data-ttu-id="c3b82-141">Hello에 대 한 다른 표현 간의 hello 표시 옵션 (에 강조 표시 된 사각형) tooswitch 클릭 동일한 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-141">Click hello display options (highlighted in rectangle) tooswitch between different representations for hello same output.</span></span> <span data-ttu-id="c3b82-142">클릭 **설정을** toochoose 어떤 consitutes hello 키와 hello 출력에는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-142">Click **Settings** toochoose what consitutes hello key and values in hello output.</span></span> <span data-ttu-id="c3b82-143">사용 하 여 위에 화면 캡처 hello **buildingID** hello 키와의 hello 평균 **temp_diff** hello 값으로.</span><span class="sxs-lookup"><span data-stu-id="c3b82-143">hello screen capture above uses **buildingID** as hello key and hello average of **temp_diff** as hello value.</span></span>
6. <span data-ttu-id="c3b82-144">또한 hello 쿼리에서 변수를 사용 하 여 Spark SQL 문을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-144">You can also run Spark SQL statements using variables in hello query.</span></span> <span data-ttu-id="c3b82-145">다음 조각과 hello 방법을 toodefine 변수에 **Temp**와 tooquery 원하는 hello 가능한 값을 사용 하 여 hello 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-145">hello next snippet shows how toodefine a variable, **Temp**, in hello query with hello possible values you want tooquery with.</span></span> <span data-ttu-id="c3b82-146">Hello 쿼리를 처음 실행 하면 드롭 다운 hello hello 변수에 대해 지정한 값이 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-146">When you first run hello query, a drop-down is automatically populated with hello values you specified for hello variable.</span></span>
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    <span data-ttu-id="c3b82-147">새 단락에 이 코드 조각을 붙여넣고 **Shift + Enter**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-147">Paste this snippet in a new paragraph and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="c3b82-148">hello 다음 스크린 샷에서 hello 출력이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-148">hello following screenshot shows hello output.</span></span>
   
    <span data-ttu-id="c3b82-149">![Hello 노트북을 사용 하 여 Spark SQL 문을 실행](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "hello 노트북을 사용 하 여 Spark SQL 문 실행")</span><span class="sxs-lookup"><span data-stu-id="c3b82-149">![Run a Spark SQL statement using hello notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "Run a Spark SQL statement using hello notebook")</span></span>
   
    <span data-ttu-id="c3b82-150">후속 쿼리에 대 한 hello 드롭다운 목록에서 새 값을 선택 하 고 hello 쿼리를 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-150">For subsequent queries, you can select a new value from hello drop-down and run hello query again.</span></span> <span data-ttu-id="c3b82-151">클릭 **설정을** toochoose 어떤 consitutes hello 키와 hello 출력에는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-151">Click **Settings** toochoose what consitutes hello key and values in hello output.</span></span> <span data-ttu-id="c3b82-152">사용 하 여 위에 화면 캡처 hello **buildingID** hello 키로의 평균 hello **temp_diff** hello 값으로 및 **targettemp** hello 그룹으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-152">hello screen capture above uses **buildingID** as hello key, hello average of **temp_diff** as hello value, and **targettemp** as hello group.</span></span>
7. <span data-ttu-id="c3b82-153">Hello 리비 인터프리터 tooexit hello 응용 프로그램을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-153">Restart hello Livy interpreter tooexit hello application.</span></span> <span data-ttu-id="c3b82-154">toodo 인터프리터 설정을 hello 오른쪽 위 모서리에서 사용자 이름에 기록 하는 hello를 클릭 하 여 열고 클릭 **인터프리터**합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-154">toodo so, open interpreter settings by clicking hello logged in user name from hello top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="c3b82-155">![인터프리터 시작](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive 출력")</span><span class="sxs-lookup"><span data-stu-id="c3b82-155">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
8. <span data-ttu-id="c3b82-156">TooLivy 인터프리터 설정을 스크롤한 다음 클릭 **다시 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-156">Scroll tooLivy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="c3b82-157">![리비 intepreter hello를 다시 시작](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "hello 선을 intepreter를 다시 시작")</span><span class="sxs-lookup"><span data-stu-id="c3b82-157">![Restart hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart hello Zeppelin intepreter")</span></span>

## <a name="how-do-i-use-external-packages-with-hello-notebook"></a><span data-ttu-id="c3b82-158">외부 패키지 hello 노트북으로 사용 하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="c3b82-158">How do I use external packages with hello notebook?</span></span>
<span data-ttu-id="c3b82-159">Hello 선을 노트북에 HDInsight (Linux) toouse 외부, 커뮤니티 제공 하지 않은 패키지를 포함된-의-즉시 hello 클러스터의 Apache Spark 클러스터에서 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-159">You can configure hello Zeppelin notebook in Apache Spark cluster on HDInsight (Linux) toouse external, community-contributed packages that are not included out-of-the-box in hello cluster.</span></span> <span data-ttu-id="c3b82-160">Hello를 검색할 수 있습니다 [Maven 리포지토리](http://search.maven.org/) 사용할 수 있는 패키지의 전체 목록은 hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-160">You can search hello [Maven repository](http://search.maven.org/) for hello complete list of packages that are available.</span></span> <span data-ttu-id="c3b82-161">다른 소스에서 사용 가능한 패키지 목록을 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-161">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="c3b82-162">예를 들어 커뮤니티 제공 패키지의 전체 목록은 [Spark 패키지](http://spark-packages.org/)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-162">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="c3b82-163">이 문서에서 볼 수 있습니다 어떻게 toouse hello [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) hello Jupyter 노트북을 사용 하 여 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-163">In this article, you will see how toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with hello Jupyter notebook.</span></span>

1. <span data-ttu-id="c3b82-164">인터프리터 설정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-164">Open interpreter settings.</span></span> <span data-ttu-id="c3b82-165">Hello 오른쪽 위 모서리에서 사용자 이름에 기록 하는 hello를 클릭 한 다음 클릭 **인터프리터**합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-165">From hello top-right corner, click hello logged in user name, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="c3b82-166">![인터프리터 시작](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive 출력")</span><span class="sxs-lookup"><span data-stu-id="c3b82-166">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="c3b82-167">TooLivy 인터프리터 설정을 스크롤한 다음 클릭 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-167">Scroll tooLivy interpreter settings and then click **Edit**.</span></span>
   
    <span data-ttu-id="c3b82-168">![인터프리터 설정 변경](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "인터프리터 설정 변경")</span><span class="sxs-lookup"><span data-stu-id="c3b82-168">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Change interpreter settings")</span></span>
3. <span data-ttu-id="c3b82-169">새 키를 추가 호출 **livy.spark.jars.packages** hello 형식에서 값을 설정 하 고 `group:id:version`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-169">Add a new key, called **livy.spark.jars.packages** and set its value in hello format `group:id:version`.</span></span> <span data-ttu-id="c3b82-170">따라서 toouse hello를 원하는 경우 [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) 패키지 hello hello 키 값을 너무 설정 해야`com.databricks:spark-csv_2.10:1.4.0`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-170">So, if you want toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package, you must set hello value of hello key too`com.databricks:spark-csv_2.10:1.4.0`.</span></span>
   
    <span data-ttu-id="c3b82-171">![인터프리터 설정 변경](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "인터프리터 설정 변경")</span><span class="sxs-lookup"><span data-stu-id="c3b82-171">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Change interpreter settings")</span></span>
   
    <span data-ttu-id="c3b82-172">클릭 **저장** 고 hello 리비 인터프리터를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-172">Click **Save** and then restart hello Livy interpreter.</span></span>
4. <span data-ttu-id="c3b82-173">**팁**: 원하는 toounderstand hello hello 키 값에 tooarrive 여기의 위에 입력 되는 한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-173">**Tip**: If you want toounderstand how tooarrive at hello value of hello key entered above, here's how.</span></span>
   
    <span data-ttu-id="c3b82-174">a.</span><span class="sxs-lookup"><span data-stu-id="c3b82-174">a.</span></span> <span data-ttu-id="c3b82-175">Maven 리포지토리 hello hello 패키지를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-175">Locate hello package in hello Maven Repository.</span></span> <span data-ttu-id="c3b82-176">이 자습서에서는 [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar)를 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-176">For this tutorial, we used [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="c3b82-177">b.</span><span class="sxs-lookup"><span data-stu-id="c3b82-177">b.</span></span> <span data-ttu-id="c3b82-178">에 대 한 hello 값을 수집 hello 리포지토리에서 **GroupId**, **의 ArtifactId**, 및 **버전**합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-178">From hello repository, gather hello values for **GroupId**, **ArtifactId**, and **Version**.</span></span>
   
    <span data-ttu-id="c3b82-179">![Jupyter Notebook에서 외부 패키지 사용](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Jupyter Notebook에서 외부 패키지 사용")</span><span class="sxs-lookup"><span data-stu-id="c3b82-179">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="c3b82-180">c.</span><span class="sxs-lookup"><span data-stu-id="c3b82-180">c.</span></span> <span data-ttu-id="c3b82-181">콜론으로 구분 하는 hello 3 값 연결 (**:**).</span><span class="sxs-lookup"><span data-stu-id="c3b82-181">Concatenate hello three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-hello-zeppelin-notebooks-saved"></a><span data-ttu-id="c3b82-182">어디 hello를 저장 하는 선을 전자 필기장 입니까?</span><span class="sxs-lookup"><span data-stu-id="c3b82-182">Where are hello Zeppelin notebooks saved?</span></span>
<span data-ttu-id="c3b82-183">hello 선을 전자 필기장 toohello 클러스터 headnodes를 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-183">hello Zeppelin notebooks are saved toohello cluster headnodes.</span></span> <span data-ttu-id="c3b82-184">따라서 hello 클러스터를 삭제 하면 hello 전자 필기장도 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-184">So, if you delete hello cluster, hello notebooks will be deleted as well.</span></span> <span data-ttu-id="c3b82-185">다른 클러스터에 나중에 사용할 전자 필기장 toopreserve 않으려면 hello 작업 실행을 완료 한 후 내보낼 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-185">If you want toopreserve your notebooks for later use on other clusters, you must export them after you have finished running hello jobs.</span></span> <span data-ttu-id="c3b82-186">노트북, tooexport 클릭 hello **내보내기** hello 이미지 아래에 나와 있는 것 처럼 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-186">tooexport a notebook, click hello **Export** icon as shown in hello image below.</span></span>

<span data-ttu-id="c3b82-187">![노트북 다운로드](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "다운로드 hello 노트북")</span><span class="sxs-lookup"><span data-stu-id="c3b82-187">![Download notebook](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Download hello notebook")</span></span>

<span data-ttu-id="c3b82-188">이렇게 하면 hello 노트북 JSON 파일로 다운로드 위치에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-188">This saves hello notebook as a JSON file in your download location.</span></span>

## <a name="livy-session-management"></a><span data-ttu-id="c3b82-189">Livy 세션 관리</span><span class="sxs-lookup"><span data-stu-id="c3b82-189">Livy session management</span></span>
<span data-ttu-id="c3b82-190">선 노트북에서 첫 번째 코드 단락 hello를 실행할 때 새 리비 세션 HDInsight Spark 클러스터에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-190">When you run hello first code paragraph in your Zeppelin notebook, a new Livy session is created in your HDInsight Spark cluster.</span></span> <span data-ttu-id="c3b82-191">이 세션은 이후에 만드는 모든 Zeppelin Notebook에서 공유됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-191">This session is shared across all Zeppelin notebooks that you subsequently create.</span></span> <span data-ttu-id="c3b82-192">몇 가지 이유 hello에 대 한 경우 세션은 리비 종료 (클러스터 다시 부팅 등), hello 선 전자 필기장에서 수 toorun 작업 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-192">If for some reason hello Livy session is killed (cluster reboot, etc.), you will not be able toorun jobs from hello Zeppelin notebook.</span></span>

<span data-ttu-id="c3b82-193">이러한 경우 hello 선 전자 필기장에서 실행 중인 작업을 시작 하기 전에 다음 단계를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-193">In such a case, you must perform hello following steps before you can start running jobs from a Zeppelin notebook.</span></span> 

1. <span data-ttu-id="c3b82-194">Hello hello 선 전자 필기장에서 리비 인터프리터를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-194">Restart hello Livy interpreter from hello Zeppelin notebook.</span></span> <span data-ttu-id="c3b82-195">toodo 인터프리터 설정을 hello 오른쪽 위 모서리에서 사용자 이름에 기록 하는 hello를 클릭 하 여 열고 클릭 **인터프리터**합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-195">toodo so, open interpreter settings by clicking hello logged in user name from hello top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="c3b82-196">![인터프리터 시작](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive 출력")</span><span class="sxs-lookup"><span data-stu-id="c3b82-196">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="c3b82-197">TooLivy 인터프리터 설정을 스크롤한 다음 클릭 **다시 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-197">Scroll tooLivy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="c3b82-198">![리비 intepreter hello를 다시 시작](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "hello 선을 intepreter를 다시 시작")</span><span class="sxs-lookup"><span data-stu-id="c3b82-198">![Restart hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart hello Zeppelin intepreter")</span></span>
3. <span data-ttu-id="c3b82-199">기존 Zeppelin Notebook에서 코드 셀을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-199">Run a code cell from an existing Zeppelin notebook.</span></span> <span data-ttu-id="c3b82-200">Hello HDInsight 클러스터에 새 리비 세션을 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-200">This creates a new Livy session in hello HDInsight cluster.</span></span>

## <span data-ttu-id="c3b82-201"><a name="seealso"></a>참고 항목</span><span class="sxs-lookup"><span data-stu-id="c3b82-201"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="c3b82-202">개요: Azure HDInsight에서 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="c3b82-202">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="c3b82-203">시나리오</span><span class="sxs-lookup"><span data-stu-id="c3b82-203">Scenarios</span></span>
* [<span data-ttu-id="c3b82-204">BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행</span><span class="sxs-lookup"><span data-stu-id="c3b82-204">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="c3b82-205">기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="c3b82-205">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="c3b82-206">Spark와 기계 학습: HDInsight toopredict 음식 검사 결과에 사용 하 여 Spark</span><span class="sxs-lookup"><span data-stu-id="c3b82-206">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="c3b82-207">Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="c3b82-207">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="c3b82-208">HDInsight의 Spark를 사용하여 웹 사이트 로그 분석</span><span class="sxs-lookup"><span data-stu-id="c3b82-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="c3b82-209">응용 프로그램 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="c3b82-209">Create and run applications</span></span>
* [<span data-ttu-id="c3b82-210">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="c3b82-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="c3b82-211">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="c3b82-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="c3b82-212">도구 및 확장</span><span class="sxs-lookup"><span data-stu-id="c3b82-212">Tools and extensions</span></span>
* [<span data-ttu-id="c3b82-213">IntelliJ 아이디어 toocreate에 대 한 HDInsight 도구 플러그 인을 사용 하 고 스파크 Scala 개 제출</span><span class="sxs-lookup"><span data-stu-id="c3b82-213">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="c3b82-214">IntelliJ 아이디어 toodebug Spark 응용 프로그램에 대 한 HDInsight 도구 플러그 인을 원격으로 사용</span><span class="sxs-lookup"><span data-stu-id="c3b82-214">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="c3b82-215">HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널</span><span class="sxs-lookup"><span data-stu-id="c3b82-215">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="c3b82-216">Jupyter 노트북에서 외부 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="c3b82-216">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="c3b82-217">Jupyter 사용자 컴퓨터에 설치 하 고 tooan HDInsight Spark 클러스터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-217">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="c3b82-218">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="c3b82-218">Manage resources</span></span>
* [<span data-ttu-id="c3b82-219">Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b82-219">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="c3b82-220">HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그</span><span class="sxs-lookup"><span data-stu-id="c3b82-220">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md 







