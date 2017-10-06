---
title: "HDInsight Linux 기반 클러스터-Azure에서 Hadoop으로 aaaHue | Microsoft Docs"
description: "HDInsight의 색상을 나타내는 tooinstall 클러스터 방법을 알아보고 tooroute hello 요청 tooHue 터널링을 사용 합니다. 색상 toobrowse 저장소를 사용 하 고 하이브 또는 Pig를 실행 합니다."
keywords: hue hadoop
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 9e57fcca-e26c-479d-a745-7b80a9290447
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: f086cbad2a90cc6903fbfccbf4a6be44f8999d07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-hue-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="a9d3d-105">HDInsight Hadoop 클러스터에 Hue 설치 및 사용</span><span class="sxs-lookup"><span data-stu-id="a9d3d-105">Install and use Hue on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="a9d3d-106">HDInsight의 색상을 나타내는 tooinstall 클러스터 방법을 알아보고 tooroute hello 요청 tooHue 터널링을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-106">Learn how tooinstall Hue on HDInsight clusters and use tunneling tooroute hello requests tooHue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a9d3d-107">이 문서의 단계 hello Linux를 사용 하는 HDInsight 클러스터를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-107">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="a9d3d-108">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a9d3d-109">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="what-is-hue"></a><span data-ttu-id="a9d3d-110">Hue 정의</span><span class="sxs-lookup"><span data-stu-id="a9d3d-110">What is Hue?</span></span>
<span data-ttu-id="a9d3d-111">색상은 Hadoop 클러스터 toointeract를 사용 하는 웹 응용 프로그램 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-111">Hue is a set of Web applications used toointeract with a Hadoop cluster.</span></span> <span data-ttu-id="a9d3d-112">Hadoop 클러스터 (HDInsight 클러스터의 hello 대/소문자 WASB)와 연결 된 색상을 나타내는 toobrowse hello 저장소를 사용 하 고, 작업 Hive 및 Pig 스크립트를 실행 하 고, 등 수입니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-112">You can use Hue toobrowse hello storage associated with a Hadoop cluster (WASB, in hello case of HDInsight clusters), run Hive jobs and Pig scripts, and so on.</span></span> <span data-ttu-id="a9d3d-113">hello 다음 구성 요소가 HDInsight Hadoop 클러스터에서 색상 설치와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-113">hello following components are available with Hue installations on an HDInsight Hadoop cluster.</span></span>

* <span data-ttu-id="a9d3d-114">Beeswax Hive 편집기</span><span class="sxs-lookup"><span data-stu-id="a9d3d-114">Beeswax Hive Editor</span></span>
* <span data-ttu-id="a9d3d-115">Pig</span><span class="sxs-lookup"><span data-stu-id="a9d3d-115">Pig</span></span>
* <span data-ttu-id="a9d3d-116">메타스토어 관리자</span><span class="sxs-lookup"><span data-stu-id="a9d3d-116">Metastore manager</span></span>
* <span data-ttu-id="a9d3d-117">Oozie</span><span class="sxs-lookup"><span data-stu-id="a9d3d-117">Oozie</span></span>
* <span data-ttu-id="a9d3d-118">FileBrowser (있음 tooWASB 기본 컨테이너 발언)</span><span class="sxs-lookup"><span data-stu-id="a9d3d-118">FileBrowser (which talks tooWASB default container)</span></span>
* <span data-ttu-id="a9d3d-119">작업 브라우저</span><span class="sxs-lookup"><span data-stu-id="a9d3d-119">Job Browser</span></span>

> [!WARNING]
> <span data-ttu-id="a9d3d-120">Hello HDInsight 클러스터와 함께 제공 되는 구성 요소 완벽 하 게 지원를 Microsoft 지원 tooisolate는 데 도움이 되며 관련된 toothese 구성 요소 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-120">Components provided with hello HDInsight cluster are fully supported and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="a9d3d-121">사용자 지정 구성 요소 상업적으로 적절 한 지원 toohelp 수신 하면 toofurther hello 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-121">Custom components receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="a9d3d-122">이 hello 문제를 해결 하거나 hello에 대 한 사용 가능한 채널 tooengage 열면 해당 기술에 대 한 심층 전문 지식이 있는 소스 기술을 요청 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-122">This might result in resolving hello issue OR asking you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="a9d3d-123">예를 들어 [HDInsight에 대한 MSDN 포럼](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com)과 같은 여러 커뮤니티 사이트를 사용할 수 있습니다. Apache 프로젝트는 [http://apache.org](http://apache.org)에 프로젝트 사이트가 있습니다(예: [Hadoop](http://hadoop.apache.org/)).</span><span class="sxs-lookup"><span data-stu-id="a9d3d-123">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>
>
>

## <a name="install-hue-using-script-actions"></a><span data-ttu-id="a9d3d-124">스크립트 동작을 사용하여 Hue 설치</span><span class="sxs-lookup"><span data-stu-id="a9d3d-124">Install Hue using Script Actions</span></span>

<span data-ttu-id="a9d3d-125">hello 스크립트 tooinstall Linux 기반 HDInsight 클러스터에서 색상은 https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh에서 사용할 수 있습니다. 기본 저장소로 Azure 저장소 Blob (WASB) 또는 Azure 데이터 레이크 저장소 클러스터에서이 스크립트 tooinstall 색상을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-125">hello script tooinstall Hue on a Linux-based HDInsight cluster is available at https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. You can use this script tooinstall Hue on clusters with either Azure Storage Blobs (WASB) or Azure Data Lake Store as default storage.</span></span>

<span data-ttu-id="a9d3d-126">이 섹션에서는 hello Azure 포털을 사용 하 여 hello 클러스터를 프로 비전 할 때 스크립트 toouse hello 하는 방법에 대 한 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-126">This section provides instructions about how toouse hello script when provisioning hello cluster using hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="a9d3d-127">Azure PowerShell, hello Azure CLI, hello HDInsight.NET SDK 또는 Azure 리소스 관리자 템플릿을 사용 하는 tooapply 스크립트 동작 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-127">Azure PowerShell, hello Azure CLI, hello HDInsight .NET SDK, or Azure Resource Manager templates can also be used tooapply script actions.</span></span> <span data-ttu-id="a9d3d-128">클러스터를 실행 하는 스크립트 작업 tooalready를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-128">You can also apply script actions tooalready running clusters.</span></span> <span data-ttu-id="a9d3d-129">자세한 내용은 [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-129">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
>
>

1. <span data-ttu-id="a9d3d-130">hello 단계를 사용 하 여 클러스터를 프로 비전 시작 [Linux 클러스터로 프로 비전 HDInsight](hdinsight-hadoop-provision-linux-clusters.md), 하지만 프로 비전을 완료 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-130">Start provisioning a cluster by using hello steps in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md), but do not complete provisioning.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a9d3d-131">HDInsight의 색상을 나타내는 tooinstall 클러스터, hello 헤드 노드에 권장된 크기는 적어도 A4 (8 코어, 14GB 메모리).</span><span class="sxs-lookup"><span data-stu-id="a9d3d-131">tooinstall Hue on HDInsight clusters, hello recommended headnode size is at least A4 (8 cores, 14 GB memory).</span></span>
   >
   >
2. <span data-ttu-id="a9d3d-132">Hello에 **옵션 구성** 블레이드를 **스크립트 동작**, 아래와 같이 hello 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-132">On hello **Optional Configuration** blade, select **Script Actions**, and provide hello information as shown below:</span></span>

    <span data-ttu-id="a9d3d-133">![색상에 대한 스크립트 작업 매개 변수 제공](./media/hdinsight-hadoop-hue-linux/hue-script-action.png "색상에 대한 스크립트 작업 매개 변수 제공")</span><span class="sxs-lookup"><span data-stu-id="a9d3d-133">![Provide script action parameters for Hue](./media/hdinsight-hadoop-hue-linux/hue-script-action.png "Provide script action parameters for Hue")</span></span>

   * <span data-ttu-id="a9d3d-134">**이름**: hello 스크립트 동작에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-134">**NAME**: Enter a friendly name for hello script action.</span></span>
   * <span data-ttu-id="a9d3d-135">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh</span><span class="sxs-lookup"><span data-stu-id="a9d3d-135">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh</span></span>
   * <span data-ttu-id="a9d3d-136">**HEAD**: 이 옵션 선택</span><span class="sxs-lookup"><span data-stu-id="a9d3d-136">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="a9d3d-137">**작업자**: 이 옵션을 비워둡니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-137">**WORKER**: Leave this blank.</span></span>
   * <span data-ttu-id="a9d3d-138">**ZOOKEEPER**: 이 옵션을 비워둡니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-138">**ZOOKEEPER**: Leave this blank.</span></span>
   * <span data-ttu-id="a9d3d-139">**PARAMETERS**: 이 옵션을 비워둡니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-139">**PARAMETERS**: Leave this blank.</span></span>
3. <span data-ttu-id="a9d3d-140">Hello hello 맨 아래에 **스크립트 동작**, hello를 사용 하 여 **선택** 단추 toosave hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-140">At hello bottom of hello **Script Actions**, use hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="a9d3d-141">마지막으로 hello를 사용 하 여 **선택** hello 아래쪽 hello의 단추 **선택적 구성** 블레이드 toosave hello 선택적 구성 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-141">Finally, use hello **Select** button at hello bottom of hello **Optional Configuration** blade toosave hello optional configuration information.</span></span>
4. <span data-ttu-id="a9d3d-142">에 설명 된 대로 hello 클러스터를 프로 비전 계속 [Linux 클러스터로 프로 비전 HDInsight](hdinsight-hadoop-provision-linux-clusters.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-142">Continue provisioning hello cluster as described in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="use-hue-with-hdinsight-clusters"></a><span data-ttu-id="a9d3d-143">HDInsight 클러스터로 Hue 사용</span><span class="sxs-lookup"><span data-stu-id="a9d3d-143">Use Hue with HDInsight clusters</span></span>

<span data-ttu-id="a9d3d-144">SSH 터널링 실행 되 면 hello 유일한 방법은 tooaccess 색상 hello 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-144">SSH Tunneling is hello only way tooaccess Hue on hello cluster once it is running.</span></span> <span data-ttu-id="a9d3d-145">SSH를 통해 터널링 toohello 헤드 노드에 hello의 색상을 나타내는 실행 중인 클러스터 직접 hello 트래픽 toogo를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-145">Tunneling via SSH allows hello traffic toogo directly toohello headnode of hello cluster where Hue is running.</span></span> <span data-ttu-id="a9d3d-146">Hello 클러스터 프로 비전 완료 되 면 hello 단계 toouse 색상 HDInsight Linux 클러스터에서 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-146">After hello cluster has finished provisioning, use hello following steps toouse Hue on an HDInsight Linux cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="a9d3d-147">아래 Firefox 웹 브라우저 toofollow hello 지침을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-147">We recommend using Firefox web browser toofollow hello instructions below.</span></span>
>
>

1. <span data-ttu-id="a9d3d-148">Hello 정보에 사용 하 여 [사용 하 여 SSH 터널링 tooaccess Ambari 웹 UI, ResourceManager, JobHistory, NameNode, Oozie, 및 기타 웹 UI](hdinsight-linux-ambari-ssh-tunnel.md) toocreate는 SSH 터널링 클라이언트 시스템 toohello HDInsight 클러스터에서 한 다음 구성 사용자 웹 브라우저 toouse hello SSH 터널을 프록시로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-148">Use hello information in [Use SSH Tunneling tooaccess Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UI's](hdinsight-linux-ambari-ssh-tunnel.md) toocreate an SSH tunnel from your client system toohello HDInsight cluster, and then configure your Web browser toouse hello SSH tunnel as a proxy.</span></span>

2. <span data-ttu-id="a9d3d-149">SSH 터널을 생성 하 고이 통해 브라우저 tooproxy 트래픽의 구성 후 hello 호스트 이름의 hello 기본 헤드 노드를 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-149">Once you have created an SSH tunnel and configured your browser tooproxy traffic through it, you must find hello host name of hello primary head node.</span></span> <span data-ttu-id="a9d3d-150">SSH를 사용 하 여 포트 22에서 toohello 클러스터를 연결 하 여이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-150">You can do this by connecting toohello cluster using SSH on port 22.</span></span> <span data-ttu-id="a9d3d-151">예를 들어 `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net` 여기서 **USERNAME** 은 SSH 사용자 이름 및 **CLUSTERNAME** hello 클러스터 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-151">For example, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net` where **USERNAME** is your SSH user name and **CLUSTERNAME** is hello name of your cluster.</span></span>

    <span data-ttu-id="a9d3d-152">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-152">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="a9d3d-153">연결 되 면 hello 기본 헤드 노드에 명령 tooobtain hello 정규화 된 도메인 이름 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-153">Once connected, use hello following command tooobtain hello fully qualified domain name of hello primary headnode:</span></span>

        hostname -f

    <span data-ttu-id="a9d3d-154">이 이름이 비슷한 toohello 다음을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-154">This will return a name similar toohello following:</span></span>

        hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

    <span data-ttu-id="a9d3d-155">Hello 색상 웹 사이트 위치한 hello 기본 헤드 노드에의 hello 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-155">This is hello hostname of hello primary headnode where hello Hue website is located.</span></span>
4. <span data-ttu-id="a9d3d-156">Http://HOSTNAME:8888에 hello 브라우저 tooopen hello 색상 포털을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-156">Use hello browser tooopen hello Hue portal at http://HOSTNAME:8888.</span></span> <span data-ttu-id="a9d3d-157">호스트 이름을 hello 이전 단계에서 얻은 hello 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-157">Replace HOSTNAME with hello name you obtained in hello previous step.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a9d3d-158">에 로그인 할 때 hello에 대 한 처음으로, 입력 정보 요청된 toocreate toohello 색상 포털에는 계정 toolog 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-158">When you log in for hello first time, you will be prompted toocreate an account toolog in toohello Hue portal.</span></span> <span data-ttu-id="a9d3d-159">여기에서 지정 하는 hello 자격 증명을 제한 toohello 포털 되며은 관련된 toohello 관리자 또는 hello 클러스터 프로 비전 하는 동안 지정 된 SSH 사용자 자격 증명.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-159">hello credentials you specify here will be limited toohello portal and are not related toohello admin or SSH user credentials you specified while provision hello cluster.</span></span>
   >
   >

    <span data-ttu-id="a9d3d-160">![로그인 toohello 색상 포털](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-login.png "색상 포털에 대 한 자격 증명 지정")</span><span class="sxs-lookup"><span data-stu-id="a9d3d-160">![Login toohello Hue portal](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-login.png "Specify credentials for Hue portal")</span></span>

### <a name="run-a-hive-query"></a><span data-ttu-id="a9d3d-161">HIVE 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="a9d3d-161">Run a Hive query</span></span>
1. <span data-ttu-id="a9d3d-162">Hello 색상 포털에서 클릭 **쿼리 편집기**, 클릭 하 고 **하이브** tooopen hello 하이브 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-162">From hello Hue portal, click **Query Editors**, and then click **Hive** tooopen hello Hive editor.</span></span>

    <span data-ttu-id="a9d3d-163">![Hive 사용](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-use-hive.png "Hive 사용")</span><span class="sxs-lookup"><span data-stu-id="a9d3d-163">![Use Hive](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-use-hive.png "Use Hive")</span></span>
2. <span data-ttu-id="a9d3d-164">Hello에 **Assist** 탭의 **데이터베이스**, 나타납니다 **hivesampletable**합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-164">On hello **Assist** tab, under **Database**, you should see **hivesampletable**.</span></span> <span data-ttu-id="a9d3d-165">HDInsight에서 모든 Hadoop 클러스터로 제공되는 예제 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-165">This is a sample table that is shipped with all Hadoop clusters on HDInsight.</span></span> <span data-ttu-id="a9d3d-166">Hello 오른쪽 창에서 예제 쿼리를 입력 하 고 hello에 hello 출력을 참조 하십시오. **결과** hello 화면 캡처에 나와 있는 것 처럼, 아래의 hello 창에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-166">Enter a sample query in hello right pane and see hello output on hello **Results** tab in hello pane below, as shown in hello screen capture.</span></span>

    <span data-ttu-id="a9d3d-167">![Hive 쿼리 실행](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-hive-query.png "Hive 쿼리 실행")</span><span class="sxs-lookup"><span data-stu-id="a9d3d-167">![Run Hive query](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-hive-query.png "Run Hive query")</span></span>

    <span data-ttu-id="a9d3d-168">Hello를 사용할 수도 있습니다 **차트** toosee을 시각적으로 hello 결과 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-168">You can also use hello **Chart** tab toosee a visual representation of hello result.</span></span>

### <a name="browse-hello-cluster-storage"></a><span data-ttu-id="a9d3d-169">Hello 클러스터 저장소 찾아보기</span><span class="sxs-lookup"><span data-stu-id="a9d3d-169">Browse hello cluster storage</span></span>
1. <span data-ttu-id="a9d3d-170">Hello 색상 포털에서 클릭 **파일 브라우저** hello 메뉴 표시줄의 hello 오른쪽 위 모서리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-170">From hello Hue portal, click **File Browser** in hello top-right corner of hello menu bar.</span></span>
2. <span data-ttu-id="a9d3d-171">기본적으로 hello에 hello 파일 브라우저가 열립니다 **/사용자/myuser** 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-171">By default hello file browser opens at hello **/user/myuser** directory.</span></span> <span data-ttu-id="a9d3d-172">Hello 클러스터와 연결 된 hello Azure storage 컨테이너의 hello 경로 toogo toohello 루트에서 hello 사용자 디렉터리 직전 hello 앞에 슬래시를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-172">Click hello forward slash right before hello user directory in hello path toogo toohello root of hello Azure storage container associated with hello cluster.</span></span>

    <span data-ttu-id="a9d3d-173">![파일 브라우저 사용](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-file-browser.png "파일 브라우저 사용")</span><span class="sxs-lookup"><span data-stu-id="a9d3d-173">![Use file browser](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-file-browser.png "Use file browser")</span></span>
3. <span data-ttu-id="a9d3d-174">파일 또는 폴더 toosee hello 사용 가능한 작업을 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-174">Right-click on a file or folder toosee hello available operations.</span></span> <span data-ttu-id="a9d3d-175">사용 하 여 hello **업로드** 단추 hello 오른쪽 모서리 tooupload 파일 toohello 현재 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-175">Use hello **Upload** button in hello right corner tooupload files toohello current directory.</span></span> <span data-ttu-id="a9d3d-176">사용 하 여 hello **새로** 단추 toocreate 새 파일 또는 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-176">Use hello **New** button toocreate new files or directories.</span></span>

> [!NOTE]
> <span data-ttu-id="a9d3d-177">hello 색상을 나타내는 파일 브라우저 hello HDInsight 클러스터와 연결 된 hello 기본 컨테이너의 hello 내용을 하나만 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-177">hello Hue file browser can only show hello contents of hello default container associated with hello HDInsight cluster.</span></span> <span data-ttu-id="a9d3d-178">추가 저장소 계정/컨테이너 hello 클러스터와 연결 된 hello 파일 탐색기를 사용 하 여 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-178">Any additional storage accounts/containers that you might have associated with hello cluster will not be accessible using hello file browser.</span></span> <span data-ttu-id="a9d3d-179">그러나 hello 클러스터와 연결 된 hello 추가 컨테이너 항상 hello 하이브 작업에 대 한 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-179">However, hello additional containers associated with hello cluster will always be accessible for hello Hive jobs.</span></span> <span data-ttu-id="a9d3d-180">예를 들어 hello 명령을 입력 하면 `dfs -ls wasb://newcontainer@mystore.blob.core.windows.net` hello 하이브 편집기에서 추가 컨테이너도의 hello 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-180">For example, if you enter hello command `dfs -ls wasb://newcontainer@mystore.blob.core.windows.net` in hello Hive editor, you can see hello contents of additional containers as well.</span></span> <span data-ttu-id="a9d3d-181">이 명령에서 **newcontainer** 클러스터와 연결 된 hello 기본 컨테이너 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-181">In this command, **newcontainer** is not hello default container associated with a cluster.</span></span>
>
>

## <a name="important-considerations"></a><span data-ttu-id="a9d3d-182">중요 고려 사항</span><span class="sxs-lookup"><span data-stu-id="a9d3d-182">Important considerations</span></span>
1. <span data-ttu-id="a9d3d-183">hello 사용 되는 스크립트 tooinstall 색상 hello 클러스터의 기본 헤드 노드에 hello에만 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-183">hello script used tooinstall Hue installs it only on hello primary headnode of hello cluster.</span></span>

2. <span data-ttu-id="a9d3d-184">설치 하는 동안 여러 Hadoop 서비스 (HDFS, YARN, MR2, Oozie) hello 구성을 업데이트 하는 것에 대 한 다시 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-184">During installation, multiple Hadoop services (HDFS, YARN, MR2, Oozie) are restarted for updating hello configuration.</span></span> <span data-ttu-id="a9d3d-185">Hello 스크립트 색상 설치 완료 되 면이 걸릴 수도 있습니다 Hadoop 서비스 toostart 다른 약간의 시간이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-185">After hello script finishes installing Hue, it might take some time for other Hadoop services toostart up.</span></span> <span data-ttu-id="a9d3d-186">처음에 Hue의 성능이 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-186">This might affect Hue's performance initially.</span></span> <span data-ttu-id="a9d3d-187">모든 서비스를 시작하면 Hue는 완벽하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-187">Once all services start up, Hue will be fully functional.</span></span>
3. <span data-ttu-id="a9d3d-188">색상을 인식 하지 못하는 Tez 작업 hello 하이브에 대 한 현재 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-188">Hue does not understand Tez jobs, which is hello current default for Hive.</span></span> <span data-ttu-id="a9d3d-189">Hello 하이브 실행 엔진으로 toouse MapReduce를 원하는 경우 다음 스크립트에 명령을 hello 스크립트 toouse hello를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-189">If you want toouse MapReduce as hello Hive execution engine, update hello script toouse hello following command in your script:</span></span>

        set hive.execution.engine=mr;

4. <span data-ttu-id="a9d3d-190">Linux 클러스터 서비스가 실행 되 고 있는 hello 기본 헤드 노드에에서 리소스 관리자 hello hello 보조에서 실행 될 수 하는 동안 시나리오를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-190">With Linux clusters, you can have a scenario where your services are running on hello primary headnode while hello Resource Manager could be running on hello secondary.</span></span> <span data-ttu-id="a9d3d-191">이러한 시나리오 hello 클러스터에서 실행 중인 작업의 색상을 나타내는 tooview 세부 정보를 사용 하는 경우 (아래 참조) 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-191">Such a scenario might result in errors (shown below) when using Hue tooview details of RUNNING jobs on hello cluster.</span></span> <span data-ttu-id="a9d3d-192">그러나 hello 작업이 완료 되 면 hello 작업 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-192">However, you can view hello job details when hello job has completed.</span></span>

   <span data-ttu-id="a9d3d-193">![Hue 포털 오류](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-error.png "Hue 포털 오류")</span><span class="sxs-lookup"><span data-stu-id="a9d3d-193">![Hue portal error](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-error.png "Hue portal error")</span></span>

   <span data-ttu-id="a9d3d-194">원인인 tooa 알려진 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-194">This is due tooa known issue.</span></span> <span data-ttu-id="a9d3d-195">이 문제를 해결 hello 활성 리소스 관리자도 실행 되도록 기본 헤드 노드에 hello에 Ambari를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-195">As a workaround, modify Ambari so that hello active Resource Manager also runs on hello primary headnode.</span></span>
5. <span data-ttu-id="a9d3d-196">`wasb://`을 사용하여 HDInsight 클러스터가 Azure 저장소를 사용하는 동안 Hue는 WebHDFS를 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-196">Hue understands WebHDFS while HDInsight clusters use Azure Storage using `wasb://`.</span></span> <span data-ttu-id="a9d3d-197">따라서 스크립트 동작에 사용할 사용자 지정 스크립트를 hello tooWASB 통신에 WebHDFS 호환 서비스인 WebWasb를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-197">So, hello custom script used with script action installs WebWasb, which is a WebHDFS-compatible service for talking tooWASB.</span></span> <span data-ttu-id="a9d3d-198">따라서 hello 색상 포털 HDFS 위치에 표시 하는 경우에 (hello 위로 마우스를 이동 하면 같은 **파일 브라우저**), WASB으로 해석 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-198">So, even though hello Hue portal says HDFS in places (like when you move your mouse over hello **File Browser**), it should be interpreted as WASB.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9d3d-199">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a9d3d-199">Next steps</span></span>
* <span data-ttu-id="a9d3d-200">[HDInsight 클러스터에 Giraph 설치](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a9d3d-200">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="a9d3d-201">클러스터 사용자 지정 tooinstall Giraph에 HDInsight Hadoop 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-201">Use cluster customization tooinstall Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="a9d3d-202">Giraph tooperform 그래프 Hadoop를 사용 하 여 처리를 허용 하 고 Azure HDInsight를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-202">Giraph allows you tooperform graph processing using Hadoop, and it can be used with Azure HDInsight.</span></span>
* <span data-ttu-id="a9d3d-203">[HDInsight 클러스터에 Solr 설치](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a9d3d-203">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> <span data-ttu-id="a9d3d-204">클러스터 사용자 지정 tooinstall Solr에 HDInsight Hadoop 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-204">Use cluster customization tooinstall Solr on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="a9d3d-205">Solr 저장 된 데이터에 tooperform 강력한 검색 작업을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-205">Solr allows you tooperform powerful search operations on stored data.</span></span>
* <span data-ttu-id="a9d3d-206">[HDInsight 클러스터에 R 설치](hdinsight-hadoop-r-scripts-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a9d3d-206">[Install R on HDInsight clusters](hdinsight-hadoop-r-scripts-linux.md).</span></span> <span data-ttu-id="a9d3d-207">HDInsight Hadoop 클러스터에서 클러스터 사용자 지정 tooinstall R을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-207">Use cluster customization tooinstall R on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="a9d3d-208">R은 통계 계산을 위한 오픈 소스 언어 및 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-208">R is an open-source language and environment for statistical computing.</span></span> <span data-ttu-id="a9d3d-209">수백 개의 기본 제공 통계 함수와 기능 및 개체 지향 프로그래밍의 측면을 결합하는 고유한 프로그래밍 언어를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-209">It provides hundreds of built-in statistical functions and its own programming language that combines aspects of functional and object-oriented programming.</span></span> <span data-ttu-id="a9d3d-210">또한 광범위한 그래픽 기능도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a9d3d-210">It also provides extensive graphical capabilities.</span></span>

[powershell-install-configure]: install-configure-powershell-linux.md
[hdinsight-provision]: hdinsight-provision-clusters-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
