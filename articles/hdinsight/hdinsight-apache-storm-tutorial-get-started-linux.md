---
title: "Azure HDInsight의 Apache Storm aaaStorm 스타터 보여 주는 예 | Microsoft Docs"
description: "자세한 방법을 toodo 빅 데이터 분석 및 프로세스 데이터를 실시간으로 Apache Storm를 사용 하 여 하 고 hello HDInsight의 storm 스타터 예제입니다."
keywords: "storm-starter, apache storm 예제"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: d710dcac-35d1-4c27-a8d6-acaf8146b485
ms.service: hdinsight
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: bb6d6549e67ca5b557f0692f98c89692a87267b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
#<a name="get-started-with-apache-storm-on-hdinsight-using-hello-storm-starter-examples"></a><span data-ttu-id="cdeff-104">Hello 스톰 시작 예제를 사용 하 여 HDInsight의 Apache Storm 시작</span><span class="sxs-lookup"><span data-stu-id="cdeff-104">Get started with Apache Storm on HDInsight using hello storm-starter examples</span></span>

<span data-ttu-id="cdeff-105">방법을 사용 하 여 HDInsight의 Apache Storm toouse hello 스톰 스타터 예제에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-105">Learn how toouse Apache Storm in HDInsight using hello storm-starter examples.</span></span>

<span data-ttu-id="cdeff-106">Apache Storm은 데이터 스트림 처리용 확장 가능한 분산형 실시간 계산 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-106">Apache Storm is a scalable, fault-tolerant, distributed, real-time computation system for processing streams of data.</span></span> <span data-ttu-id="cdeff-107">Azure HDInsight의 Storm을 사용하여 실시간 데이터 분석을 수행하는 클라우드 기반 Storm 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-107">With Storm on Azure HDInsight, you can create a cloud-based Storm cluster that performs big data analytics in real time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cdeff-108">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="cdeff-109">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cdeff-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cdeff-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="cdeff-110">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="cdeff-111">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="cdeff-111">**An Azure subscription**.</span></span> <span data-ttu-id="cdeff-112">[Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cdeff-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="cdeff-113">**SSH 및 SCP 사용 경험**.</span><span class="sxs-lookup"><span data-stu-id="cdeff-113">**Familiarity with SSH and SCP**.</span></span> <span data-ttu-id="cdeff-114">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cdeff-114">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-a-storm-cluster"></a><span data-ttu-id="cdeff-115">Storm 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="cdeff-115">Create a Storm cluster</span></span>

<span data-ttu-id="cdeff-116">Hello 단계 toocreate 스톰은 HDInsight 클러스터에서 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-116">Use hello following steps toocreate a Storm on HDInsight cluster:</span></span>

1. <span data-ttu-id="cdeff-117">Hello에서 [Azure 포털](https://portal.azure.com)선택, **+ 새로 만들기**, **인텔리전스 + 분석**를 선택한 후 **HDInsight**합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-117">From hello [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>

    ![HDInsight 클러스터 만들기](./media/hdinsight-apache-storm-tutorial-get-started-linux/create-hdinsight.png)

2. <span data-ttu-id="cdeff-119">Hello에서 **기본 사항** 블레이드에서 hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-119">From hello **Basics** blade, enter hello following information:</span></span>

    * <span data-ttu-id="cdeff-120">**클러스터 이름**: hello HDInsight 클러스터의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-120">**Cluster Name**: hello name of hello HDInsight cluster.</span></span>
    * <span data-ttu-id="cdeff-121">**구독**: hello 구독 toouse를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-121">**Subscription**: Select hello subscription toouse.</span></span>
    * <span data-ttu-id="cdeff-122">**클러스터 로그인 사용자 이름과** 및 **클러스터 로그인 암호**: HTTPS를 통해 hello 클러스터에 액세스할 때 hello 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-122">**Cluster login username** and **Cluster login password**: hello login when accessing hello cluster over HTTPS.</span></span> <span data-ttu-id="cdeff-123">Hello Ambari 웹 UI 또는 REST API와 같은 이러한 자격 증명 tooaccess 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-123">You use these credentials tooaccess services such as hello Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="cdeff-124">**SSH 사용자 이름 보안**: SSH를 통해 hello 클러스터에 액세스할 때 사용 하는 hello 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-124">**Secure Shell (SSH) username**: hello login used when accessing hello cluster over SSH.</span></span> <span data-ttu-id="cdeff-125">기본적으로 hello 암호 hello 클러스터 로그인 암호와 같은 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-125">By default hello password is hello same as hello cluster login password.</span></span>
    * <span data-ttu-id="cdeff-126">**리소스 그룹**: hello 리소스 그룹 toocreate hello 클러스터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-126">**Resource Group**: hello resource group toocreate hello cluster in.</span></span>
    * <span data-ttu-id="cdeff-127">**위치**: hello Azure 지역 toocreate hello 클러스터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-127">**Location**: hello Azure region toocreate hello cluster in.</span></span>

    ![구독 선택](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-basic-configuration.png)

3. <span data-ttu-id="cdeff-129">선택 **형식 클러스터**, 집합 hello hello에 값에 따라 다음 **클러스터 구성** 블레이드:</span><span class="sxs-lookup"><span data-stu-id="cdeff-129">Select **Cluster type**, and then set hello following values on hello **Cluster configuration** blade:</span></span>

    * <span data-ttu-id="cdeff-130">**클러스터 유형**: Storm</span><span class="sxs-lookup"><span data-stu-id="cdeff-130">**Cluster Type**: Storm</span></span>

    * <span data-ttu-id="cdeff-131">**운영 체제**: Linux</span><span class="sxs-lookup"><span data-stu-id="cdeff-131">**Operating system**: Linux</span></span>

    * <span data-ttu-id="cdeff-132">**버전**: Storm 1.1.0(HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="cdeff-132">**Version**: Storm 1.1.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="cdeff-133">**클러스터 계층**: 표준</span><span class="sxs-lookup"><span data-stu-id="cdeff-133">**Cluster Tier**: Standard</span></span>

    <span data-ttu-id="cdeff-134">마지막으로 hello를 사용 하 여 **선택** toosave 설정 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-134">Finally, use hello **Select** button toosave settings.</span></span>

    ![클러스터 유형 선택](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="cdeff-136">Hello 클러스터 종류를 선택한 후 hello를 사용 하 여 __선택__ tooset hello 클러스터 유형 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-136">After selecting hello cluster type, use hello __Select__ button tooset hello cluster type.</span></span> <span data-ttu-id="cdeff-137">를 사용 하 여 hello __다음__ 단추 toofinish 기본 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-137">Next, use hello __Next__ button toofinish basic configuration.</span></span>

5. <span data-ttu-id="cdeff-138">Hello에서 **저장소** 블레이드를 선택 하거나 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-138">From hello **Storage** blade, select or create a Storage account.</span></span> <span data-ttu-id="cdeff-139">이 문서의 단계 hello에 대 한 hello 나머지 필드는 둡니다 hello 기본 값이 블레이드를 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-139">For hello steps in this document, leave hello other fields on this blade at hello default values.</span></span> <span data-ttu-id="cdeff-140">사용 하 여 hello __다음__ 단추 toosave 저장소 구성.</span><span class="sxs-lookup"><span data-stu-id="cdeff-140">Use hello __Next__ button toosave storage configuration.</span></span>

    ![HDInsight에 대 한 저장소 계정 설정을 hello 설정](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-storage-account.png)

6. <span data-ttu-id="cdeff-142">Hello에서 **요약** 블레이드에서 hello 클러스터에 대 한 hello 구성 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-142">From hello **Summary** blade, review hello configuration for hello cluster.</span></span> <span data-ttu-id="cdeff-143">사용 하 여 hello __편집__ toochange 올바르지 않은 설정을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-143">Use hello __Edit__ links toochange any settings that are incorrect.</span></span> <span data-ttu-id="cdeff-144">마지막으로, the__Create__ 단추 toocreate hello 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-144">Finally, use the__Create__ button toocreate hello cluster.</span></span>

    ![클러스터 구성 요약](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-configuration-summary.png)

    > [!NOTE]
    > <span data-ttu-id="cdeff-146">Too20 분 toocreate hello 클러스터를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-146">It can take up too20 minutes toocreate hello cluster.</span></span>

## <a name="run-a-storm-starter-sample-on-hdinsight"></a><span data-ttu-id="cdeff-147">HDInsight에서 storm-starter 샘플 실행</span><span class="sxs-lookup"><span data-stu-id="cdeff-147">Run a storm-starter sample on HDInsight</span></span>

1. <span data-ttu-id="cdeff-148">SSH를 사용 하 여 toohello HDInsight 클러스터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-148">Connect toohello HDInsight cluster using SSH:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="cdeff-149">입력 정보 요청된 tooenter 모르는 암호 toosecure을 SSH 사용자 계정을 사용 하는 경우 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-149">If you used a password toosecure your SSH user account, you are prompted tooenter it.</span></span> <span data-ttu-id="cdeff-150">공개 키를 사용 하는 경우 필요한 활용해 hello `-i` 매개 변수 toospecify hello 일치 하는 개인 키입니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-150">If you used a public key, you may need use hello `-i` parameter toospecify hello matching private key.</span></span> <span data-ttu-id="cdeff-151">예: `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="cdeff-151">For example, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

    <span data-ttu-id="cdeff-152">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cdeff-152">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="cdeff-153">다음 명령 예제에서는 토폴로지 toostart hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-153">Use hello following command toostart an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology wordcount

    > [!NOTE]
    > <span data-ttu-id="cdeff-154">HDInsight의 이전 버전의 hello 토폴로지의 hello 클래스 이름으로 `storm.starter.WordCountTopology` 대신 `org.apache.storm.starter.WordCountTopology`합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-154">On previous versions of HDInsight, hello class name of hello topology is `storm.starter.WordCountTopology` instead of `org.apache.storm.starter.WordCountTopology`.</span></span>

    <span data-ttu-id="cdeff-155">이 명령은 '단어 수'의 이름으로 hello 클러스터에서 hello WordCount 토폴로지 예제를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-155">This command starts hello example WordCount topology on hello cluster, with a friendly name of 'wordcount'.</span></span> <span data-ttu-id="cdeff-156">임의로 hello 문장에서 각 단어의 hello 발생 횟수 및 문장 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-156">It randomly generates sentences and count hello occurrence of each word in hello sentences.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cdeff-157">Hello를 사용 하기 전에 hello 클러스터를 포함 하는 hello jar 파일을 먼저 복사 해야 토폴로지 toohello 클러스터를 전송할 때 `storm` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-157">When submitting your own topologies toohello cluster, you must first copy hello jar file containing hello cluster before using hello `storm` command.</span></span> <span data-ttu-id="cdeff-158">사용 하 여 hello `scp` 명령 toocopy hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-158">Use hello `scp` command toocopy hello file.</span></span> <span data-ttu-id="cdeff-159">예를 들어 `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="cdeff-159">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
    >
    > <span data-ttu-id="cdeff-160">hello WordCount 예제 및 기타 스톰 시작 예제에서 클러스터에 이미 포함 되어 `/usr/hdp/current/storm-client/contrib/storm-starter/`합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-160">hello WordCount example, and other storm-starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

<span data-ttu-id="cdeff-161">hello 코드를 찾을 수 인 경우 hello 소스 hello 스톰 시작 예제를 보려면 [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter)합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-161">If you are interested in viewing hello source for hello storm-starter examples, you can find hello code at [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span></span> <span data-ttu-id="cdeff-162">이 링크는 Storm 1.1.x에 해당하며 HDInsight 3.6과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-162">This link is for Storm 1.1.x, which is provided with HDInsight 3.6.</span></span> <span data-ttu-id="cdeff-163">다른 버전 Storm의 hello를 사용 하 여 __분기__ 다른 스톰 버전 hello 페이지 tooselect hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-163">For other versions of Storm, use hello __Branch__ button at hello top of hello page tooselect a different Storm version.</span></span>

## <a name="monitor-hello-topology"></a><span data-ttu-id="cdeff-164">모니터 hello 토폴로지</span><span class="sxs-lookup"><span data-stu-id="cdeff-164">Monitor hello topology</span></span>

<span data-ttu-id="cdeff-165">hello 스톰 UI 작업 토폴로지, 실행을 위한 웹 인터페이스를 제공 하 고 HDInsight 클러스터에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-165">hello Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span>

<span data-ttu-id="cdeff-166">Hello 단계 toomonitor hello 토폴로지 hello 스톰 UI를 사용 하 여 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-166">Use hello following steps toomonitor hello topology using hello Storm UI:</span></span>

1. <span data-ttu-id="cdeff-167">toodisplay hello 스톰 UI, 웹 브라우저 toohttps://CLUSTERNAME.azurehdinsight.net/stormui를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-167">toodisplay hello Storm UI, open a web browser toohttps://CLUSTERNAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="cdeff-168">대체 **CLUSTERNAME** 클러스터의 hello 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-168">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cdeff-169">사용자 이름 및 암호 tooprovide 요청 되 면 hello 클러스터 관리자 (관리자) 및 때 사용한 암호를 입력 hello 클러스터를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-169">If asked tooprovide a user name and password, enter hello cluster administrator (admin) and password that you used when creating hello cluster.</span></span>

2. <span data-ttu-id="cdeff-170">아래 **토폴로지 요약**선택, hello **wordcount** hello에 항목 **이름** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-170">Under **Topology summary**, select hello **wordcount** entry in hello **Name** column.</span></span> <span data-ttu-id="cdeff-171">Hello 토폴로지에 대 한 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-171">Information about hello topology is displayed.</span></span>

    ![storm-starter WordCount 토폴로지 정보가 있는 Storm 대시보드.](./media/hdinsight-apache-storm-tutorial-get-started-linux/topology-summary.png)

    <span data-ttu-id="cdeff-173">이 페이지에서는 hello를 다음 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-173">This page provides hello following information:</span></span>

    * <span data-ttu-id="cdeff-174">**토폴로지 통계** -hello 토폴로지 성능에 대 한 기본 정보가 시간 창으로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-174">**Topology stats** - Basic information on hello topology performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="cdeff-175">Hello 페이지의 다른 섹션에 표시 되는 정보에 대 한 특정 시간 창 변경 내용이 hello 시간 창을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-175">Selecting a specific time window changes hello time window for information displayed in other sections of hello page.</span></span>

    * <span data-ttu-id="cdeff-176">**Spouts** -각 배출구에서 반환 된 hello 마지막 오류를 포함 하 여 spouts에 대 한 기본 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-176">**Spouts** - Basic information about spouts, including hello last error returned by each spout.</span></span>

    * <span data-ttu-id="cdeff-177">**Bolt** - Bolt에 대한 기본 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-177">**Bolts** - Basic information about bolts.</span></span>

    * <span data-ttu-id="cdeff-178">**토폴로지 구성** -hello 토폴로지 구성에 대 한 정보를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-178">**Topology configuration** - Detailed information about hello topology configuration.</span></span>

    <span data-ttu-id="cdeff-179">이 페이지에는 hello 토폴로지에 수행 될 작업을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-179">This page also provides actions that can be taken on hello topology:</span></span>

    * <span data-ttu-id="cdeff-180">**활성화** - 비활성화된 토폴로지 처리를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-180">**Activate** - Resumes processing of a deactivated topology.</span></span>

    * <span data-ttu-id="cdeff-181">**비활성화** - 실행 중인 토폴로지를 일시 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-181">**Deactivate** - Pauses a running topology.</span></span>

    * <span data-ttu-id="cdeff-182">**균형을 다시 조정할** -hello 토폴로지의 hello 병렬 처리를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-182">**Rebalance** - Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="cdeff-183">하면 해야 균형을 다시 조정 실행 중인 토폴로지 hello hello 클러스터의 노드 수를 변경한 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-183">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="cdeff-184">Hello hello 클러스터의 노드 수 증가/감소에 대 한 병렬 처리 수준 toocompensate를 조정 리 밸런스 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-184">Rebalancing adjusts parallelism toocompensate for hello increased/decreased number of nodes in hello cluster.</span></span> <span data-ttu-id="cdeff-185">자세한 내용은 참조 [스톰 토폴로지의 hello parallelism 이해](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-185">For more information, see [Understanding hello parallelism of a Storm topology](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

    * <span data-ttu-id="cdeff-186">**Kill** -hello 제한 시간을 지정한 후 스톰 토폴로지를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-186">**Kill** - Terminates a Storm topology after hello specified timeout.</span></span>

3. <span data-ttu-id="cdeff-187">이 페이지에서 hello에서 항목을 선택 **Spouts** 또는 **쐐기** 섹션.</span><span class="sxs-lookup"><span data-stu-id="cdeff-187">From this page, select an entry from hello **Spouts** or **Bolts** section.</span></span> <span data-ttu-id="cdeff-188">Hello 선택한 구성 요소에 대 한 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-188">Information about hello selected component is displayed.</span></span>

    ![선택한 구성 요소에 대한 정보가 있는 스톰 대시보드.](./media/hdinsight-apache-storm-tutorial-get-started-linux/component-summary.png)

    <span data-ttu-id="cdeff-190">이 페이지는 hello 다음 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-190">This page displays hello following information:</span></span>

    * <span data-ttu-id="cdeff-191">**Stats 배출구/볼트** -hello 구성 요소 성능에 대 한 기본 정보가 시간 창으로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-191">**Spout/Bolt stats** - Basic information on hello component performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="cdeff-192">Hello 페이지의 다른 섹션에 표시 되는 정보에 대 한 특정 시간 창 변경 내용이 hello 시간 창을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-192">Selecting a specific time window changes hello time window for information displayed in other sections of hello page.</span></span>

    * <span data-ttu-id="cdeff-193">**Stats 입력** (볼트만)-hello 볼트에서 사용 하는 데이터를 생성 하는 구성 요소에 대 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-193">**Input stats** (bolt only) - Information on components that produce data consumed by hello bolt.</span></span>

    * <span data-ttu-id="cdeff-194">**출력 통계** - 이 Bolt에서 내보낸 데이터에 대한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-194">**Output stats** - Information on data emitted by this bolt.</span></span>

    * <span data-ttu-id="cdeff-195">**실행자** - 이 구성 요소의 인스턴스에 대한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-195">**Executors** - Information on instances of this component.</span></span>

    * <span data-ttu-id="cdeff-196">**오류** - 이 구성 요소에 의해 생성된 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-196">**Errors** - Errors produced by this component.</span></span>

4. <span data-ttu-id="cdeff-197">배출구 또는 번개 hello 세부 정보를 볼 때 hello에서 항목을 선택 **포트** 열 hello에 **Executor** hello 구성의 특정 인스턴스에 대 한 tooview 세부 정보 섹션.</span><span class="sxs-lookup"><span data-stu-id="cdeff-197">When viewing hello details of a spout or bolt, select an entry from hello **Port** column in hello **Executors** section tooview details for a specific instance of hello component.</span></span>

        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

    <span data-ttu-id="cdeff-198">이 예제에서는 word hello **7** 1493957 번 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-198">In this example, hello word **seven** has occurred 1493957 times.</span></span> <span data-ttu-id="cdeff-199">이 개수는 몇 번이이 토폴로지 시작 된 이후 hello word가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-199">This count is how many times hello word has been encountered since this topology was started.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="cdeff-200">Hello 토폴로지를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-200">Stop hello topology</span></span>

<span data-ttu-id="cdeff-201">Toohello 반환 **토폴로지 요약** hello 단어 개수 토폴로지에 대 한 페이지 선택한 후 hello **Kill** hello에서 단추 **토폴로지 작업** 섹션.</span><span class="sxs-lookup"><span data-stu-id="cdeff-201">Return toohello **Topology summary** page for hello word-count topology, and then select hello **Kill** button from hello **Topology actions** section.</span></span> <span data-ttu-id="cdeff-202">메시지가 표시 되 면 hello 토폴로지를 중지 하기 전에 10 초 toowait hello에 대 한 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-202">When prompted, enter 10 for hello seconds toowait before stopping hello topology.</span></span> <span data-ttu-id="cdeff-203">Hello 제한 시간 이후 hello 토폴로지 더 이상 나타나지 않습니다 hello를 방문 하면 **스톰 UI** hello 대시보드의 섹션.</span><span class="sxs-lookup"><span data-stu-id="cdeff-203">After hello timeout period, hello topology no longer appears when you visit hello **Storm UI** section of hello dashboard.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="cdeff-204">Hello 클러스터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-204">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="cdeff-205">HDInsight 클러스터를 만드는 동안 문제가 발생할 경우 [액세스 제어 요구 사항](hdinsight-administer-use-portal-linux.md#create-clusters)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cdeff-205">If you run into an issue with creating HDInsight cluster, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <span data-ttu-id="cdeff-206"><a id="next"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="cdeff-206"><a id="next"></a>Next steps</span></span>

<span data-ttu-id="cdeff-207">Apache Storm이 자습서에서는 hello의 기본적인 사용 HDInsight의 Storm 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-207">In this Apache Storm tutorial, you learned hello basics of working with Storm on HDInsight.</span></span> <span data-ttu-id="cdeff-208">배우는 것이 너무 어떻게[Maven를 사용 하 여 개발 하는 Java 기반 토폴로지](hdinsight-storm-develop-java-topology.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-208">Next, learn how too[Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="cdeff-209">이미 익숙한 Java 기반 토폴로지를 개발 하 고는 기존 토폴로지에 tooHDInsight toodeploy 원하는 참조 [배포 HDInsight의 Apache Storm 토폴로지를 관리할 및](hdinsight-storm-deploy-monitor-topology-linux.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-209">If you're already familiar with developing Java-based topologies and want toodeploy an existing topology tooHDInsight, see [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).</span></span>

<span data-ttu-id="cdeff-210">.NET 개발자인 경우 Visual Studio를 사용하여 C# 또는 하이브리드 C#/Java 토폴로지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdeff-210">If you are a .NET developer, you can create C# or hybrid C#/Java topologies using Visual Studio.</span></span> <span data-ttu-id="cdeff-211">자세한 내용은 [Visual Studio용 Hadoop 도구를 사용하여 HDInsight에서 Apache Storm에 대한 C# 토폴로지 개발](hdinsight-storm-develop-csharp-visual-studio-topology.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cdeff-211">For more information, see [Develop C# topologies for Apache Storm on HDInsight using Hadoop tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="cdeff-212">HDInsight의 Storm 함께 사용할 수 있는 예제 토폴로지 예제 따르는 hello를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="cdeff-212">For example topologies that can be used with Storm on HDInsight, see hello following examples:</span></span>

* [<span data-ttu-id="cdeff-213">HDInsight의 Storm에 대한 예제 토폴로지</span><span class="sxs-lookup"><span data-stu-id="cdeff-213">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[preview-portal]: https://portal.azure.com/
