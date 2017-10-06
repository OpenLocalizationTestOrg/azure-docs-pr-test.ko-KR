---
title: "Azure HDInsight linux 기능 클러스터 aaaInstall | Microsoft Docs"
description: "어떻게 tooinstall 기능 및 Linux 기반 HDInsight Hadoop에서 Airpal 클러스터 스크립트 동작을 사용 하 여에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: nitinme
ms.openlocfilehash: 5d54d0efc3e5fdc6f5a8d3a94ad2f61d16df24c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-presto-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="535ea-103">HDInsight Hadoop 클러스터에 Presto 설치 및 사용</span><span class="sxs-lookup"><span data-stu-id="535ea-103">Install and use Presto on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="535ea-104">이 항목에서는 스크립트를 사용 하 여 tooinstall 기능 HDInsight Hadoop에 클러스터 되는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-104">In this topic, you learn how tooinstall Presto on HDInsight Hadoop clusters by using Script Action.</span></span> <span data-ttu-id="535ea-105">또한 학습 방법을 tooinstall Airpal 기존 새 HDInsight 클러스터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-105">You also learn how tooinstall Airpal on an existing Presto HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="535ea-106">hello이 문서의 단계를 수행 하려면는 **3.5 HDInsight Hadoop 클러스터** Linux를 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-106">hello steps in this document require an **HDInsight 3.5 Hadoop cluster** that uses Linux.</span></span> <span data-ttu-id="535ea-107">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="535ea-108">자세한 내용은 [HDInsight 버전](hdinsight-component-versioning.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="535ea-108">For more information, see [HDInsight versions](hdinsight-component-versioning.md).</span></span>

## <a name="what-is-presto"></a><span data-ttu-id="535ea-109">Presto란?</span><span class="sxs-lookup"><span data-stu-id="535ea-109">What is Presto?</span></span>
<span data-ttu-id="535ea-110">[Presto](https://prestodb.io/overview.html)는 빅 데이터에 대한 빠른 분산된 SQL 쿼리 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-110">[Presto](https://prestodb.io/overview.html) is a fast distributed SQL query engine for big data.</span></span> <span data-ttu-id="535ea-111">Presto는 페타바이트의 데이터를 대화형으로 쿼리하는 데 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-111">Presto is suitable for interactive querying of petabytes of data.</span></span> <span data-ttu-id="535ea-112">기능 및 함께 작동 하는 방법을 hello 구성 요소에 자세한 내용은 참조 [Presto 개념](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst)합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-112">For more information on hello components of Presto and how they work together, see [Presto concepts](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span></span>

> [!WARNING]
> <span data-ttu-id="535ea-113">Hello HDInsight 클러스터와 함께 제공 되는 구성 요소 완벽 하 게 지원를 Microsoft 지원 tooisolate는 데 도움이 되며 관련된 toothese 구성 요소 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-113">Components provided with hello HDInsight cluster are fully supported and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>
> 
> <span data-ttu-id="535ea-114">사용자 지정 구성 요소, 기능, 예: 수신 상업적으로 적절 한 지원 toohelp 있습니다 toofurther hello 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-114">Custom components, such as Presto, receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="535ea-115">이 hello 문제를 해결 하거나 hello에 대 한 사용 가능한 채널 tooengage 열면 해당 기술에 대 한 심층 전문 지식이 있는 소스 기술을 요청 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-115">This might result in resolving hello issue OR asking you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="535ea-116">예를 들어 [HDInsight에 대한 MSDN 포럼](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com)과 같은 여러 커뮤니티 사이트를 사용할 수 있습니다. Apache 프로젝트는 [http://apache.org](http://apache.org)에 프로젝트 사이트가 있습니다(예: [Hadoop](http://hadoop.apache.org/)).</span><span class="sxs-lookup"><span data-stu-id="535ea-116">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>
> 
> 


## <a name="install-presto-using-script-action"></a><span data-ttu-id="535ea-117">스크립트 작업을 사용하여 Presto 설치</span><span class="sxs-lookup"><span data-stu-id="535ea-117">Install Presto using script action</span></span>

<span data-ttu-id="535ea-118">이 섹션 toouse hello 샘플 스크립트를 사용 하 여 새 클러스터를 만들 때 Azure 포털을 hello 하는 방법에 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-118">This section provides instructions on how toouse hello sample script when creating a new cluster by using hello Azure portal.</span></span> 

1. <span data-ttu-id="535ea-119">hello 단계를 사용 하 여 클러스터를 프로 비전 시작 [프로 비전 Linux 기반 HDInsight 클러스터](hdinsight-hadoop-create-linux-clusters-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-119">Start provisioning a cluster by using hello steps in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span> <span data-ttu-id="535ea-120">Hello를 사용 하 여 hello 클러스터를 만들고 있는지 확인 **사용자 지정** 클러스터 만들기 흐름.</span><span class="sxs-lookup"><span data-stu-id="535ea-120">Make sure you create hello cluster using hello **Custom** cluster creation flow.</span></span> <span data-ttu-id="535ea-121">만들면 해당 hello 클러스터 hello 요구 사항을 준수를 충족 하는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-121">You must ensure that hello cluster you create meets hello following requirements.</span></span>

    <span data-ttu-id="535ea-122">a.</span><span class="sxs-lookup"><span data-stu-id="535ea-122">a.</span></span> <span data-ttu-id="535ea-123">HDInsight 버전 3.5를 사용하는 Hadoop 클러스터여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-123">It must be a Hadoop cluster with HDInsight version 3.5.</span></span>

    <span data-ttu-id="535ea-124">b.</span><span class="sxs-lookup"><span data-stu-id="535ea-124">b.</span></span> <span data-ttu-id="535ea-125">Hello 데이터 저장소와 Azure 저장소를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-125">It must use Azure Storage as hello data store.</span></span> <span data-ttu-id="535ea-126">Hello 저장소 옵션으로 Azure 데이터 레이크 저장소를 사용 하는 클러스터에서 새를 사용 하 여 아직 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-126">Using Presto on a cluster that uses Azure Data Lake Store as hello storage option is not yet supported.</span></span> 

    ![사용자 지정 옵션을 사용하여 HDInsight 클러스터 만들기](./media/hdinsight-hadoop-install-presto/hdinsight-install-custom.png)

2. <span data-ttu-id="535ea-128">Hello에 **고급 설정** 블레이드를 **스크립트 동작**, 아래 hello 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-128">On hello **Advanced settings** blade, select **Script Actions**, and provide hello information below:</span></span>
   
   * <span data-ttu-id="535ea-129">**이름**: hello 스크립트 동작에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-129">**NAME**: Enter a friendly name for hello script action.</span></span>
   * <span data-ttu-id="535ea-130">**Bash 스크립트 URI**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span><span class="sxs-lookup"><span data-stu-id="535ea-130">**Bash script URI**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span></span>
   * <span data-ttu-id="535ea-131">**HEAD**: 이 옵션 선택</span><span class="sxs-lookup"><span data-stu-id="535ea-131">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="535ea-132">**WORKER**: 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-132">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="535ea-133">**ZOOKEEPER**: 이 확인란의 선택 취소</span><span class="sxs-lookup"><span data-stu-id="535ea-133">**ZOOKEEPER**: Clear this check box</span></span>
   * <span data-ttu-id="535ea-134">**PARAMETERS**: 이 필드는 공백으로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-134">**PARAMETERS**: Leave this field blank</span></span>


3. <span data-ttu-id="535ea-135">Hello hello 맨 아래에 **스크립트 동작** 블레이드에서 hello 클릭 **선택** 단추 toosave hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-135">At hello bottom of hello **Script Actions** blade, click hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="535ea-136">마지막 hello를 클릭 하 여 **선택** hello 아래쪽 hello의 단추 **고급 설정** 블레이드 toosave hello 구성 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-136">Finally, click  hello **Select** button at hello bottom of hello **Advanced Settings** blade toosave hello configuration information.</span></span>

4. <span data-ttu-id="535ea-137">에 설명 된 대로 hello 클러스터를 프로 비전 계속 [프로 비전 Linux 기반 HDInsight 클러스터](hdinsight-hadoop-create-linux-clusters-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-137">Continue provisioning hello cluster as described in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="535ea-138">Azure PowerShell, hello Azure CLI, hello HDInsight.NET SDK 또는 Azure 리소스 관리자 템플릿을 사용 하는 tooapply 스크립트 동작 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-138">Azure PowerShell, hello Azure CLI, hello HDInsight .NET SDK, or Azure Resource Manager templates can also be used tooapply script actions.</span></span> <span data-ttu-id="535ea-139">클러스터를 실행 하는 스크립트 작업 tooalready를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-139">You can also apply script actions tooalready running clusters.</span></span> <span data-ttu-id="535ea-140">자세한 내용은 [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="535ea-140">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
    > 
    > 

## <a name="use-presto-with-hdinsight"></a><span data-ttu-id="535ea-141">HDInsight와 함께 Presto 사용</span><span class="sxs-lookup"><span data-stu-id="535ea-141">Use Presto with HDInsight</span></span>

<span data-ttu-id="535ea-142">Hello 위에서 설명한 hello 단계를 사용 하 여 설치 후 단계 toouse 기능 하는 HDInsight 클러스터에서 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-142">Perform hello following steps toouse Presto in an HDInsight cluster after you have installed it using hello steps described above.</span></span>

1. <span data-ttu-id="535ea-143">SSH를 사용 하 여 toohello HDInsight 클러스터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-143">Connect toohello HDInsight cluster using SSH:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="535ea-144">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="535ea-144">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
     

2. <span data-ttu-id="535ea-145">다음 명령을 hello를 사용 하 여 hello Presto 셸을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-145">Start hello Presto shell using hello following command.</span></span>
   
        presto --schema default

3. <span data-ttu-id="535ea-146">모든 HDInsight 클러스터에서 기본으로 사용할 수 있는 **hivesampletable** 샘플 테이블에서 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-146">Run a query on a sample table, **hivesampletable**, which is available on all HDInsight clusters by default.</span></span>
   
        select count (*) from hivesampletable;
   
    <span data-ttu-id="535ea-147">기본적으로 Presto에 대한 [Hive](https://prestodb.io/docs/current/connector/hive.html) 및 [TPCH](https://prestodb.io/docs/current/connector/tpch.html) 커넥터는 이미 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-147">By default, [Hive](https://prestodb.io/docs/current/connector/hive.html) and [TPCH](https://prestodb.io/docs/current/connector/tpch.html) connectors for Presto are already configured.</span></span> <span data-ttu-id="535ea-148">하이브 커넥터 구성된 toouse hello 설치 기본 하이브 설치 이므로 하이브에서 모든 hello 테이블 기능에 자동으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-148">Hive connector is configured toouse hello default installed Hive installation, so all hello tables from Hive will be automatically visible in Presto.</span></span>

    <span data-ttu-id="535ea-149">Presto를 사용하는 방법에 대한 자세한 설명은 [Presto 설명서](https://prestodb.io/docs/current/index.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="535ea-149">For a detailed description on how you can use Presto, see [Presto documentation](https://prestodb.io/docs/current/index.html).</span></span>

## <a name="use-airpal-with-presto"></a><span data-ttu-id="535ea-150">Presto와 함께 Airpal 사용</span><span class="sxs-lookup"><span data-stu-id="535ea-150">Use Airpal with Presto</span></span>

<span data-ttu-id="535ea-151">[Airpal](https://github.com/airbnb/airpal#airpal)은 Presto에 대한 오픈 소스 웹 기반 쿼리 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-151">[Airpal](https://github.com/airbnb/airpal#airpal) is an open-source web-based query interface for Presto.</span></span> <span data-ttu-id="535ea-152">Airpal에 대한 자세한 내용은 [Airpal 설명서](https://github.com/airbnb/airpal#airpal)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="535ea-152">For more information on Airpal, see [Airpal documentation](https://github.com/airbnb/airpal#airpal).</span></span>

<span data-ttu-id="535ea-153">이 섹션에서는 보면 hello 단계 너무**hello edgenode에 Airpal 설치** HDInsight Hadoop 클러스터의 기능에 이미 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-153">In this section, we look at hello steps too**install Airpal on hello edgenode** of an HDInsight Hadoop cluster, that already has Presto installed.</span></span> <span data-ttu-id="535ea-154">이렇게 하면 해당 hello Airpal 웹 쿼리 인터페이스는 hello 인터넷을 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-154">This ensures that hello Airpal web query interface is available over hello Internet.</span></span>

1. <span data-ttu-id="535ea-155">SSH를 사용 하 여 새 설치 hello HDInsight 클러스터의 헤드 노드에 toohello 연결:</span><span class="sxs-lookup"><span data-stu-id="535ea-155">Using SSH, connect toohello headnode of hello HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="535ea-156">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="535ea-156">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="535ea-157">연결 되 면 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-157">Once you are connected, run hello following command.</span></span>

        sudo slider registry  --name presto1 --getexp presto 
   
    <span data-ttu-id="535ea-158">Hello 다음과 같은 출력을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-158">You should see an output like hello following:</span></span>

        {
            "coordinator_address" : [ {
                "value" : "10.0.0.12:9090",
                "level" : "application",
                "updatedTime" : "Mon Apr 03 20:13:41 UTC 2017"
        } ]

3. <span data-ttu-id="535ea-159">Hello 출력에서 hello에 대 한 hello 값을 확인 **값** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-159">From hello output, note hello value for hello **value** property.</span></span> <span data-ttu-id="535ea-160">Airpal hello 클러스터 edgenode에 설치 하는 동안이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-160">You will need this while installing Airpal on hello cluster edgenode.</span></span> <span data-ttu-id="535ea-161">Hello 출력 해야 하는 hello 값 보다는 **10.0.0.12:9090**합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-161">From hello output above, hello value that you will need is **10.0.0.12:9090**.</span></span>

4. <span data-ttu-id="535ea-162">서식 파일을 사용 hello  **[여기](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)**  toocreate HDInsight 클러스터 edgenode 고 hello 스크린 샷 뒤에 표시 된 대로 hello 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-162">Use hello template **[here](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)** toocreate an HDInsight cluster edgenode and provide hello values as shown in hello following screenshot.</span></span>

    ![HDInsight에서 Presto 클러스터에 Airpal 설치](./media/hdinsight-hadoop-install-presto/hdinsight-install-airpal.png)

5. <span data-ttu-id="535ea-164">**구매**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-164">Click **Purchase**.</span></span>

6. <span data-ttu-id="535ea-165">Hello 변경 내용이 적용 된 toohello 클러스터 구성, 후 단계를 수행 하는 hello를 사용 하 여 hello Airpal 웹 인터페이스를 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-165">Once hello changes are applied toohello cluster configuration, you can access hello Airpal web interface by using hello following steps.</span></span>

    <span data-ttu-id="535ea-166">a.</span><span class="sxs-lookup"><span data-stu-id="535ea-166">a.</span></span> <span data-ttu-id="535ea-167">Hello 클러스터 블레이드에서 클릭 **응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-167">From hello cluster blade, click **Applications**.</span></span>

    ![HDInsight에서 Presto 클러스터에 Airpal 시작](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal.png)

    <span data-ttu-id="535ea-169">b.</span><span class="sxs-lookup"><span data-stu-id="535ea-169">b.</span></span> <span data-ttu-id="535ea-170">Hello에서 **설치 된 앱** 블레이드에서 클릭 **포털** airpal에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-170">From hello **Installed Apps** blade, click **Portal** against airpal.</span></span>

    ![HDInsight에서 Presto 클러스터에 Airpal 시작](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal-1.png)

    <span data-ttu-id="535ea-172">c.</span><span class="sxs-lookup"><span data-stu-id="535ea-172">c.</span></span> <span data-ttu-id="535ea-173">메시지가 표시 되 면 hello HDInsight Hadoop 클러스터를 만드는 동안 지정한 hello 관리자 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-173">When prompted, enter hello admin credentials that you specified while creating hello HDInsight Hadoop cluster.</span></span>

## <a name="customize-a-presto-installation-on-hdinsight-cluster"></a><span data-ttu-id="535ea-174">HDInsight 클러스터에서 Presto 설치 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="535ea-174">Customize a Presto installation on HDInsight cluster</span></span>

<span data-ttu-id="535ea-175">HDInsight Hadoop 클러스터에 기능을 설치한 후 변경 등 커넥터 하, hello 설치 toomake 변경 업데이트 메모리 설정 등을 사용자 지정할 수 있습니다. Hello 단계 toodo 하므로 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-175">After you have installed Presto on an HDInsight Hadoop cluster, you can customize hello installation toomake changes such as update memory settings, change connectors, etc. Perform hello following steps toodo so.</span></span>

1. <span data-ttu-id="535ea-176">SSH를 사용 하 여 새 설치 hello HDInsight 클러스터의 헤드 노드에 toohello 연결:</span><span class="sxs-lookup"><span data-stu-id="535ea-176">Using SSH, connect toohello headnode of hello HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="535ea-177">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="535ea-177">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="535ea-178">Hello 파일에서 구성 변경을 수행 `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-178">Make your configuration changes in hello file `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span></span> <span data-ttu-id="535ea-179">Presto 구성에 대한 자세한 내용은 [YARN 기반 클러스터에 대한 Presto 구성](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="535ea-179">For more information on Presto configuration, see [Presto configuration for YARN-based clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).</span></span>

3. <span data-ttu-id="535ea-180">중지 하 고 hello 기능의 현재 실행 중인 인스턴스를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-180">Stop and kill hello current running instance of Presto.</span></span>

        sudo slider stop presto1 --force
        sudo slider destroy presto1 --force

4. <span data-ttu-id="535ea-181">Hello 사용자 지정과 기능의 새 인스턴스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-181">Start a new instance of Presto with hello customization.</span></span>

       sudo slider create presto1 --template /var/lib/presto/presto-hdinsight-master/appConfig-default.json --resources /var/lib/presto/presto-hdinsight-master/resources-default.json

5. <span data-ttu-id="535ea-182">Hello 새 인스턴스 toobe 준비 기다렸다가 presto 코디네이터 주소를 적어 두세요.</span><span class="sxs-lookup"><span data-stu-id="535ea-182">Wait for hello new instance toobe ready and note presto coordinator address.</span></span>


       sudo slider registry --name presto1 --getexp presto

## <a name="generate-benchmark-data-for-hdinsight-clusters-that-run-presto"></a><span data-ttu-id="535ea-183">Presto를 실행하는 HDInsight 클러스터에 대한 벤치마크 데이터를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-183">Generate benchmark data for HDInsight clusters that run Presto</span></span>

<span data-ttu-id="535ea-184">TPC DS는 hello 업계의 빅 데이터 시스템을 비롯 한 여러 의사 결정 지원 시스템 hello 성능을 측정 하기 위한 표준.</span><span class="sxs-lookup"><span data-stu-id="535ea-184">TPC-DS is hello industry standard for measuring hello performance of many decision support systems, including big data systems.</span></span> <span data-ttu-id="535ea-185">새 HDInsight 클러스터 toogenerate 데이터에 사용할 수 있으며 HDInsight 벤치 마크 데이터와 비교 하는 방법을 평가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-185">You can use Presto on HDInsight clusters toogenerate data and evaluate how it compares with your own HDInsight benchmark data.</span></span> <span data-ttu-id="535ea-186">자세한 내용은 [여기](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="535ea-186">For more information, see [here](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span></span>



## <a name="see-also"></a><span data-ttu-id="535ea-187">참고 항목</span><span class="sxs-lookup"><span data-stu-id="535ea-187">See also</span></span>
* <span data-ttu-id="535ea-188">[HDInsight 클러스터에서 Hue 설치 및 사용](hdinsight-hadoop-hue-linux.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-188">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="535ea-189">색상은 웹 UI를 실행 하는 쉬운 toocreate 있도록 찾아서 지정 Pig 및 Hive 작업을 저장도 마찬가지로 HDInsight 클러스터에 대 한 기본 저장소 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-189">Hue is a web UI that makes it easy toocreate, run and save Pig and Hive jobs, as well as browse hello default storage for your HDInsight cluster.</span></span>

* <span data-ttu-id="535ea-190">[HDInsight 클러스터에 Giraph 설치](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="535ea-190">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="535ea-191">클러스터 사용자 지정 tooinstall Giraph에 HDInsight Hadoop 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-191">Use cluster customization tooinstall Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="535ea-192">Giraph는 tooperform 그래프 Hadoop을 사용 하 여 처리를 허용 하 고 Azure HDInsight 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-192">Giraph allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="535ea-193">[HDInsight 클러스터에 Solr 설치](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="535ea-193">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> <span data-ttu-id="535ea-194">클러스터 사용자 지정 tooinstall Solr에 HDInsight Hadoop 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-194">Use cluster customization tooinstall Solr on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="535ea-195">Solr 저장 된 데이터에 tooperform 강력한 검색 작업을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="535ea-195">Solr allows you tooperform powerful search operations on stored data.</span></span>

[hdinsight-install-r]: hdinsight-hadoop-r-scripts-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
