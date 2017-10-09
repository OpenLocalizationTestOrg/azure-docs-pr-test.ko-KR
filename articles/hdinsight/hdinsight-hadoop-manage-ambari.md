---
title: "aaaMonitor Ambari 웹 UI를 사용 하 여 Azure HDInsight 관리 및 | Microsoft Docs"
description: "자세한 내용은 방법 toouse Ambari toomonitor Linux 기반 HDInsight 클러스터를 관리 하 고 있습니다. 이 문서에서는 toouse hello Ambari 웹 UI에 포함 된 HDInsight 클러스터 방법을 배웁니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4787f3cc-a650-4dc3-9d96-a19a67aad046
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: d422c40e63345d7054839a625e115c50dad040f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-web-ui"></a><span data-ttu-id="c9b5f-104">Hello Ambari 웹 UI를 사용 하 여 HDInsight 클러스터를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-104">Manage HDInsight clusters by using hello Ambari Web UI</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="c9b5f-105">Apache Ambari hello 관리 및 쉽게 toouse 웹 UI 및 REST API를 제공 하 여 Hadoop 클러스터의 모니터링을 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-105">Apache Ambari simplifies hello management and monitoring of a Hadoop cluster by providing an easy toouse web UI and REST API.</span></span> <span data-ttu-id="c9b5f-106">Ambari는 Linux 기반 HDInsight 클러스터에 포함 되 고 사용 되는 toomonitor hello 클러스터 구성 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-106">Ambari is included on Linux-based HDInsight clusters, and is used toomonitor hello cluster and make configuration changes.</span></span>

<span data-ttu-id="c9b5f-107">이 문서에서는 HDInsight 클러스터와 toouse Ambari 웹 UI hello 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-107">In this document, you learn how toouse hello Ambari Web UI with an HDInsight cluster.</span></span>

## <span data-ttu-id="c9b5f-108"><a id="whatis"></a>Ambari 정의</span><span class="sxs-lookup"><span data-stu-id="c9b5f-108"><a id="whatis"></a>What is Ambari?</span></span>

<span data-ttu-id="c9b5f-109">[Apache Ambari](http://ambari.apache.org)는 사용하기 쉬운 웹 UI를 제공하여 Hadoop 관리를 단순화합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-109">[Apache Ambari](http://ambari.apache.org) simplifies Hadoop management by providing an easy-to-use web UI.</span></span> <span data-ttu-id="c9b5f-110">Ambari를 사용하여 Hadoop 클러스터를 생성, 관리 및 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-110">You can use Ambari create, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="c9b5f-111">개발자 hello를 사용 하 여 응용 프로그램에 이러한 기능을 통합할 수 [Ambari REST Api](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-111">Developers can integrate these capabilities into their applications by using hello [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="c9b5f-112">Ambari 웹 UI hello hello Linux 운영 체제를 사용 하는 HDInsight 클러스터를 사용 하 여 기본적으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-112">hello Ambari Web UI is provided by default with HDInsight clusters that use hello Linux operating system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c9b5f-113">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-113">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c9b5f-114">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-114">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 

## <a name="connectivity"></a><span data-ttu-id="c9b5f-115">연결</span><span class="sxs-lookup"><span data-stu-id="c9b5f-115">Connectivity</span></span>

<span data-ttu-id="c9b5f-116">hello Ambari 웹 UI를 HTTPS://CLUSTERNAME.azurehdidnsight.net에서 HDInsight 클러스터에 사용할 수 있는 **CLUSTERNAME** hello 클러스터 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-116">hello Ambari Web UI is available on your HDInsight cluster at HTTPS://CLUSTERNAME.azurehdidnsight.net, where **CLUSTERNAME** is hello name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c9b5f-117">HTTPS 필요 tooAmbari HDInsight에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-117">Connecting tooAmbari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="c9b5f-118">인증에 대 한 메시지가 표시 되 면 hello 관리자 계정 이름 및 hello 클러스터를 만들 때 지정한 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-118">When prompted for authentication, use hello admin account name and password you provided when hello cluster was created.</span></span>

## <a name="ssh-tunnel-proxy"></a><span data-ttu-id="c9b5f-119">SSH 터널(프록시)</span><span class="sxs-lookup"><span data-stu-id="c9b5f-119">SSH tunnel (proxy)</span></span>

<span data-ttu-id="c9b5f-120">Hello 인터넷을 통해 직접 액세스할 수 있는 클러스터에 대해 Ambari 동안 (예: toohello JobTracker) Ambari 웹 UI에 노출 되지 않으므로 hello에서 일부 링크는 인터넷 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-120">While Ambari for your cluster is accessible directly over hello Internet, some links from hello Ambari Web UI (such as toohello JobTracker) are not exposed on hello internet.</span></span> <span data-ttu-id="c9b5f-121">이러한 서비스 tooaccess, SSH 터널을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-121">tooaccess these services, you must create an SSH tunnel.</span></span> <span data-ttu-id="c9b5f-122">자세한 내용은 [HDInsight와 SSH 터널링 사용](hdinsight-linux-ambari-ssh-tunnel.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-122">For more information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

## <a name="ambari-web-ui"></a><span data-ttu-id="c9b5f-123">Ambari 웹 UI</span><span class="sxs-lookup"><span data-stu-id="c9b5f-123">Ambari Web UI</span></span>

<span data-ttu-id="c9b5f-124">Toohello Ambari 웹 UI에 연결할 때 메시지 표시 tooauthenticate toohello 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-124">When connecting toohello Ambari Web UI, you are prompted tooauthenticate toohello page.</span></span> <span data-ttu-id="c9b5f-125">Hello 클러스터 admin 사용자 (Admin 기본값) 및 클러스터를 만드는 동안 사용 되는 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-125">Use hello cluster admin user (default Admin) and password you used during cluster creation.</span></span>

<span data-ttu-id="c9b5f-126">Hello 페이지가 열립니다 때 hello 위쪽에 참고 hello 모음.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-126">When hello page opens, note hello bar at hello top.</span></span> <span data-ttu-id="c9b5f-127">이 모음 포함 hello 다음 정보와 컨트롤:</span><span class="sxs-lookup"><span data-stu-id="c9b5f-127">This bar contains hello following information and controls:</span></span>

![ambari-nav](./media/hdinsight-hadoop-manage-ambari/ambari-nav.png)

* <span data-ttu-id="c9b5f-129">**Ambari 로고** -열립니다 hello 대시보드를 사용 하는 toomonitor hello 클러스터가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-129">**Ambari logo** - Opens hello dashboard, which can be used toomonitor hello cluster.</span></span>

* <span data-ttu-id="c9b5f-130">**클러스터 이름 # ops** -hello 지속적인 Ambari 작업 수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-130">**Cluster name # ops** - Displays hello number of ongoing Ambari operations.</span></span> <span data-ttu-id="c9b5f-131">선택 hello 클러스터 이름 또는 **# ops** 백그라운드 작업의 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-131">Selecting hello cluster name or **# ops** displays a list of background operations.</span></span>

* <span data-ttu-id="c9b5f-132">**# 경고** -hello 클러스터에 대 한 경고 또는 위험 경고를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-132">**# alerts** - Displays warnings or critical alerts, if any, for hello cluster.</span></span>

* <span data-ttu-id="c9b5f-133">**대시보드** -hello 대시보드에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-133">**Dashboard** - Displays hello dashboard.</span></span>

* <span data-ttu-id="c9b5f-134">**서비스** -hello 클러스터에서 hello 서비스에 대 한 정보 및 구성 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-134">**Services** - Information and configuration settings for hello services in hello cluster.</span></span>

* <span data-ttu-id="c9b5f-135">**호스트** -hello 클러스터의 노드 hello에 대 한 정보 및 구성 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-135">**Hosts** - Information and configuration settings for hello nodes in hello cluster.</span></span>

* <span data-ttu-id="c9b5f-136">**Alerts** - 정보, 경고 및 중요한 알림에 대한 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-136">**Alerts** - A log of information, warnings, and critical alerts.</span></span>

* <span data-ttu-id="c9b5f-137">**관리자** -소프트웨어 스택/서비스 hello 클러스터, 서비스 계정 정보 및 Kerberos 보안에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-137">**Admin** - Software stack/services that are installed on hello cluster, service account information, and Kerberos security.</span></span>

* <span data-ttu-id="c9b5f-138">**Admin 단추** - Ambari 관리, 사용자 설정 및 로그 아웃입니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-138">**Admin button** - Ambari management, user settings, and logout.</span></span>

## <a name="monitoring"></a><span data-ttu-id="c9b5f-139">모니터링</span><span class="sxs-lookup"><span data-stu-id="c9b5f-139">Monitoring</span></span>

### <a name="alerts"></a><span data-ttu-id="c9b5f-140">경고</span><span class="sxs-lookup"><span data-stu-id="c9b5f-140">Alerts</span></span>

<span data-ttu-id="c9b5f-141">hello 다음 목록에 포함 되어 Ambari에서 사용 하는 hello 일반적인 경고 상태:</span><span class="sxs-lookup"><span data-stu-id="c9b5f-141">hello following list contains hello common alert statuses used by Ambari:</span></span>

* <span data-ttu-id="c9b5f-142">**OK**</span><span class="sxs-lookup"><span data-stu-id="c9b5f-142">**OK**</span></span>
* <span data-ttu-id="c9b5f-143">**Warning**</span><span class="sxs-lookup"><span data-stu-id="c9b5f-143">**Warning**</span></span>
* <span data-ttu-id="c9b5f-144">**CRITICAL**</span><span class="sxs-lookup"><span data-stu-id="c9b5f-144">**CRITICAL**</span></span>
* <span data-ttu-id="c9b5f-145">**UNKNOWN**</span><span class="sxs-lookup"><span data-stu-id="c9b5f-145">**UNKNOWN**</span></span>

<span data-ttu-id="c9b5f-146">경고 이외의 **확인** hello 인해 **# 경고** hello 위쪽 경고 hello 페이지 toodisplay hello 수의 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-146">Alerts other than **OK** cause hello **# alerts** entry at hello top of hello page toodisplay hello number of alerts.</span></span> <span data-ttu-id="c9b5f-147">이 항목을 선택 하면 hello 경고 및 상태를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-147">Selecting this entry displays hello alerts and their status.</span></span>

<span data-ttu-id="c9b5f-148">경고 hello에서 볼 수 있는 여러 기본 그룹으로 구성 됩니다 **경고** 페이지.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-148">Alerts are organized into several default groups, which can be viewed from hello **Alerts** page.</span></span>

![경고 페이지](./media/hdinsight-hadoop-manage-ambari/alerts.png)

<span data-ttu-id="c9b5f-150">Hello를 사용 하 여 hello 그룹을 관리할 수 **동작** 메뉴에서 **경고 그룹 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-150">You can manage hello groups by using hello **Actions** menu and selecting **Manage Alert Groups**.</span></span>

![경고 그룹 관리 대화 상자](./media/hdinsight-hadoop-manage-ambari/manage-alerts.png)

<span data-ttu-id="c9b5f-152">또한 경고 방법을 직접 관리 하 고 hello에서 경고 알림을 만들 수 있습니다 **동작** 메뉴를 선택 하 여 __경고 알림을 관리__합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-152">You can also manage alerting methods, and create alert notifications from hello **Actions** menu by selecting __Manage Alert Notifications__.</span></span> <span data-ttu-id="c9b5f-153">모든 현재 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-153">Any current notifications are displayed.</span></span> <span data-ttu-id="c9b5f-154">여기에서 알림을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-154">You can also create notifications from here.</span></span> <span data-ttu-id="c9b5f-155">특정 경고/심각도 조합이 발생하면 **전자 메일** 또는 **SNMP**를 통해 알림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-155">Notifications can be sent via **EMAIL** or **SNMP** when specific alert/severity combinations occur.</span></span> <span data-ttu-id="c9b5f-156">예를 들어 hello에 때 hello 경고 전자 메일 메시지를 보낼 수 있습니다 **YARN 기본** 그룹을 너무 설정**위험**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-156">For example, you can send an email message when any of hello alerts in hello **YARN Default** group is set too**Critical**.</span></span>

![경고 만들기 대화 상자](./media/hdinsight-hadoop-manage-ambari/create-alert-notification.png)

<span data-ttu-id="c9b5f-158">마지막으로,을 선택 하면 __경고 설정 관리__ hello에서 __동작__ 메뉴 있습니다 tooset hello 횟수 경고 알림을 전송 되기 전에 발생 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-158">Finally, selecting __Manage Alert Settings__ from hello __Actions__ menu allows you tooset hello number of times an alert must occur before a notification is sent.</span></span> <span data-ttu-id="c9b5f-159">일시적인 오류에 대 한 사용된 tooprevent 알림을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-159">This setting can be used tooprevent notifications for transient errors.</span></span>

### <a name="cluster"></a><span data-ttu-id="c9b5f-160">프로비전</span><span class="sxs-lookup"><span data-stu-id="c9b5f-160">Cluster</span></span>

<span data-ttu-id="c9b5f-161">hello **메트릭** hello 대시보드 탭 일련의 클러스터의 쉽게 toomonitor hello 상태를 한 눈에 확인 하는 위젯 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-161">hello **Metrics** tab of hello dashboard contains a series of widgets that make it easy toomonitor hello status of your cluster at a glance.</span></span> <span data-ttu-id="c9b5f-162">**CPU Usage**와 같은 여러 위젯은 클릭하면 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-162">Several widgets, such as **CPU Usage**, provide additional information when clicked.</span></span>

![메트릭이 표시된 대시보드](./media/hdinsight-hadoop-manage-ambari/metrics.png)

<span data-ttu-id="c9b5f-164">hello **Heatmaps** 탭 하 여 메트릭을 녹색 toored에서 이동 하는 색이 지정 된 heatmaps로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-164">hello **Heatmaps** tab displays metrics as colored heatmaps, going from green toored.</span></span>

![히트맵이 표시된 대시보드](./media/hdinsight-hadoop-manage-ambari/heatmap.png)

<span data-ttu-id="c9b5f-166">Hello 클러스터 내의 hello 노드에 대 한 자세한 내용은 선택 **호스트**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-166">For more information on hello nodes within hello cluster, select **Hosts**.</span></span> <span data-ttu-id="c9b5f-167">다음에 관심이 있는 hello 특정 노드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-167">Then select hello specific node you are interested in.</span></span>

![호스트 세부 정보](./media/hdinsight-hadoop-manage-ambari/host-details.png)

### <a name="services"></a><span data-ttu-id="c9b5f-169">Services</span><span class="sxs-lookup"><span data-stu-id="c9b5f-169">Services</span></span>

<span data-ttu-id="c9b5f-170">hello **서비스** hello 대시보드에서 사이드바 hello 클러스터에서 실행 되는 hello 서비스의 hello 상태에 대 한 빠른 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-170">hello **Services** sidebar on hello dashboard provides quick insight into hello status of hello services running on hello cluster.</span></span> <span data-ttu-id="c9b5f-171">다양 한 아이콘은 사용 되는 tooindicate 상태 또는 수행 해야 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-171">Various icons are used tooindicate status or actions that should be taken.</span></span> <span data-ttu-id="c9b5f-172">예를 들어, 서비스가 필요한 toobe 재활용 하는 경우 노란색 재활용 기호가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-172">For example, a yellow recycle symbol is displayed if a service needs toobe recycled.</span></span>

![서비스 세로 막대](./media/hdinsight-hadoop-manage-ambari/service-bar.png)

> [!NOTE]
> <span data-ttu-id="c9b5f-174">표시 된 hello 서비스 HDInsight 클러스터 유형 및 버전 간에 서로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-174">hello services displayed differ between HDInsight cluster types and versions.</span></span> <span data-ttu-id="c9b5f-175">여기에 표시 된 hello 서비스는 클러스터에 대해 표시 된 hello 서비스 보다 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-175">hello services displayed here may be different than hello services displayed for your cluster.</span></span>

<span data-ttu-id="c9b5f-176">서비스를 선택 하면 hello 서비스에 보다 자세한 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-176">Selecting a service displays more detailed information on hello service.</span></span>

![서비스 요약 정보](./media/hdinsight-hadoop-manage-ambari/service-details.png)

#### <a name="quick-links"></a><span data-ttu-id="c9b5f-178">빠른 링크</span><span class="sxs-lookup"><span data-stu-id="c9b5f-178">Quick links</span></span>

<span data-ttu-id="c9b5f-179">일부 서비스 표시는 **빠른 링크** hello hello 페이지 맨 아래에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-179">Some services display a **Quick Links** link at hello top of hello page.</span></span> <span data-ttu-id="c9b5f-180">이 사용 되는 tooaccess 서비스 관련 웹 ui를 사용 해도 같은 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-180">This can be used tooaccess service-specific web UIs, such as:</span></span>

* <span data-ttu-id="c9b5f-181">**Job History** - MapReduce 작업 기록</span><span class="sxs-lookup"><span data-stu-id="c9b5f-181">**Job History** - MapReduce job history.</span></span>
* <span data-ttu-id="c9b5f-182">**Resource Manager** - YARN ResourceManager UI</span><span class="sxs-lookup"><span data-stu-id="c9b5f-182">**Resource Manager** - YARN ResourceManager UI.</span></span>
* <span data-ttu-id="c9b5f-183">**NameNode** - HDFS(Hadoop Distributed File System) NameNode UI</span><span class="sxs-lookup"><span data-stu-id="c9b5f-183">**NameNode** - Hadoop Distributed File System (HDFS) NameNode UI.</span></span>
* <span data-ttu-id="c9b5f-184">**Oozie Web UI** - Oozie UI</span><span class="sxs-lookup"><span data-stu-id="c9b5f-184">**Oozie Web UI** - Oozie UI.</span></span>

<span data-ttu-id="c9b5f-185">이 링크를 선택 하면 hello 선택한 페이지를 표시 하는 브라우저에서 새 탭이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-185">Selecting any of these links opens a new tab in your browser, which displays hello selected page.</span></span>

> [!NOTE]
> <span data-ttu-id="c9b5f-186">선택 hello **빠른 링크** 서비스에 대 한 항목 "서버를 찾을 수 없습니다." 오류를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-186">Selecting hello **Quick Links** entry for a service may return a "server not found" error.</span></span> <span data-ttu-id="c9b5f-187">Hello를 사용 하는 경우 SSH 터널을 사용 해야이 오류가 발생 하면 **빠른 링크** 이 서비스에 대 한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-187">If you encounter this error, you must use an SSH tunnel when using hello **Quick Links** entry for this service.</span></span> <span data-ttu-id="c9b5f-188">자세한 내용은 [HDInsight와 SSH 터널링 사용](hdinsight-linux-ambari-ssh-tunnel.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-188">For information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)</span></span>

## <a name="management"></a><span data-ttu-id="c9b5f-189">관리</span><span class="sxs-lookup"><span data-stu-id="c9b5f-189">Management</span></span>

### <a name="ambari-users-groups-and-permissions"></a><span data-ttu-id="c9b5f-190">Ambari 사용자, 그룹 및 사용 권한</span><span class="sxs-lookup"><span data-stu-id="c9b5f-190">Ambari users, groups, and permissions</span></span>

<span data-ttu-id="c9b5f-191">[도메인 가입](hdinsight-domain-joined-introduction.md) HDInsight 클러스터를 사용할 때 사용자, 그룹 및 권한을 사용하는 작업이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-191">Working with users, groups, and permissions are supported when using a [domain joined](hdinsight-domain-joined-introduction.md) HDInsight cluster.</span></span> <span data-ttu-id="c9b5f-192">참조에 hello Ambari 관리 UI를 사용 하 여 도메인에 가입 된 클러스터에 대 한 내용은 [도메인에 가입 된 HDInsight 클러스터를 관리](hdinsight-domain-joined-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-192">For information on using hello Ambari Management UI on a domain-joined cluster, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-introduction.md).</span></span>

> [!WARNING]
> <span data-ttu-id="c9b5f-193">Linux 기반 HDInsight 클러스터에 hello Ambari 감시 (hdinsightwatchdog)의 hello 암호를 변경 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-193">Do not change hello password of hello Ambari watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="c9b5f-194">Hello 암호 구분선 변경 기능 toouse 스크립트 동작 hello 또는 클러스터를 사용 하 여 크기 조정 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-194">Changing hello password breaks hello ability toouse script actions or perform scaling operations with your cluster.</span></span>

### <a name="hosts"></a><span data-ttu-id="c9b5f-195">호스트</span><span class="sxs-lookup"><span data-stu-id="c9b5f-195">Hosts</span></span>

<span data-ttu-id="c9b5f-196">hello **호스트** 페이지 hello 클러스터의 모든 호스트를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-196">hello **Hosts** page lists all hosts in hello cluster.</span></span> <span data-ttu-id="c9b5f-197">toomanage 호스트는 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-197">toomanage hosts, follow these steps.</span></span>

![호스트 페이지](./media/hdinsight-hadoop-manage-ambari/hosts.png)

> [!NOTE]
> <span data-ttu-id="c9b5f-199">호스트 추가, 서비스 해제 및 서비스 등록은 HDInsight 클러스터에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-199">Adding, decommissioning, and recommissioning a host should not be used with HDInsight clusters.</span></span>

1. <span data-ttu-id="c9b5f-200">원하는 toomanage hello 호스트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-200">Select hello host that you wish toomanage.</span></span>

2. <span data-ttu-id="c9b5f-201">사용 하 여 hello **동작** tooperform 원하는 메뉴 tooselect hello 작업:</span><span class="sxs-lookup"><span data-stu-id="c9b5f-201">Use hello **Actions** menu tooselect hello action that you wish tooperform:</span></span>

   * <span data-ttu-id="c9b5f-202">**모든 구성 요소 시작** -hello 호스트에서 모든 구성 요소를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-202">**Start all components** - Start all components on hello host.</span></span>

   * <span data-ttu-id="c9b5f-203">**모든 구성 요소도 중지** -hello 호스트에서 모든 구성 요소를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-203">**Stop all components** - Stop all components on hello host.</span></span>

   * <span data-ttu-id="c9b5f-204">**모든 구성 요소를 다시 시작** 중지-hello 호스트에서 모든 구성 요소를 시작 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-204">**Restart all components** - Stop and start all components on hello host.</span></span>

   * <span data-ttu-id="c9b5f-205">**유지 관리 모드를 켜고** -hello 호스트에 대 한 경고를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-205">**Turn on maintenance mode** - Suppresses alerts for hello host.</span></span> <span data-ttu-id="c9b5f-206">경고를 생성하는 작업을 수행하는 경우 이 모드를 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-206">This mode should be enabled if you are performing actions that generate alerts.</span></span> <span data-ttu-id="c9b5f-207">예를 들어 서비스를 중지하고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-207">For example, stopping and starting a service.</span></span>

   * <span data-ttu-id="c9b5f-208">**유지 관리 모드를 해제** -반환 hello 호스트 toonormal 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-208">**Turn off maintenance mode** - Returns hello host toonormal alerting.</span></span>

   * <span data-ttu-id="c9b5f-209">**중지** -중지 DataNode 또는 NodeManagers hello 호스트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-209">**Stop** - Stops DataNode or NodeManagers on hello host.</span></span>

   * <span data-ttu-id="c9b5f-210">**시작** -시작 DataNode 또는 NodeManagers hello 호스트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-210">**Start** - Starts DataNode or NodeManagers on hello host.</span></span>

   * <span data-ttu-id="c9b5f-211">**다시 시작** -중지 및 시작 DataNode 또는 NodeManagers hello 호스트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-211">**Restart** - Stops and starts DataNode or NodeManagers on hello host.</span></span>

   * <span data-ttu-id="c9b5f-212">**서비스 해제** -hello 클러스터에서 호스트를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-212">**Decommission** - Removes a host from hello cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="c9b5f-213">HDInsight 클러스터에서는 이 작업을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-213">Do not use this action on HDInsight clusters.</span></span>

   * <span data-ttu-id="c9b5f-214">**Recommission** -이전에 서비스 해제 된 호스트 toohello 클러스터에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-214">**Recommission** - Adds a previously decommissioned host toohello cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="c9b5f-215">HDInsight 클러스터에서는 이 작업을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-215">Do not use this action on HDInsight clusters.</span></span>

### <span data-ttu-id="c9b5f-216"><a id="service"></a>Services</span><span class="sxs-lookup"><span data-stu-id="c9b5f-216"><a id="service"></a>Services</span></span>

<span data-ttu-id="c9b5f-217">Hello에서 **대시보드** 또는 **서비스** 페이지에서 hello를 사용 하 여 **동작** hello 서비스 toostop hello 목록 맨 아래에 단추 및 모든 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-217">From hello **Dashboard** or **Services** page, use hello **Actions** button at hello bottom of hello list of services toostop and start all services.</span></span>

![Service Actions](./media/hdinsight-hadoop-manage-ambari/service-actions.png)

> [!WARNING]
> <span data-ttu-id="c9b5f-219">동안 **서비스 추가** 나열 되어 사용 되는 tooadd 서비스 toohello HDInsight 클러스터 수 없도록이 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-219">While **Add Service** is listed in this menu, it should not be used tooadd services toohello HDInsight cluster.</span></span> <span data-ttu-id="c9b5f-220">클러스터를 프로비전하는 동안 스크립트 작업을 사용하여 새 서비스를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-220">New services should be added using a Script Action during cluster provisioning.</span></span> <span data-ttu-id="c9b5f-221">스크립트 작업에 대한 자세한 내용은 [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-221">For more information on using Script Actions, see [Customize HDInsight clusters using Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="c9b5f-222">Hello 동안 **동작** 단추 모든 서비스를 다시 시작할 수, 종종 원하는 toostart, 중지 또는 특정 서비스를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-222">While hello **Actions** button can restart all services, often you want toostart, stop, or restart a specific service.</span></span> <span data-ttu-id="c9b5f-223">Hello tooperform 작업 단계에 나오는 개별 서비스에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-223">Use hello following steps tooperform actions on an individual service:</span></span>

1. <span data-ttu-id="c9b5f-224">Hello에서 **대시보드** 또는 **서비스** 페이지에서 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-224">From hello **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="c9b5f-225">Hello의 hello 위에서 **요약** 탭에서 hello를 사용 하 여 **서비스 작업** 단추와 선택 hello 동작 tootake 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-225">From hello top of hello **Summary** tab, use hello **Service Actions** button and select hello action tootake.</span></span> <span data-ttu-id="c9b5f-226">모든 노드에서 hello 서비스를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-226">This restarts hello service on all nodes.</span></span>

    ![서비스 작업](./media/hdinsight-hadoop-manage-ambari/individual-service-actions.png)

   > [!NOTE]
   > <span data-ttu-id="c9b5f-228">Hello 클러스터에서 실행 되는 동안 일부 서비스를 다시 시작 경고를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-228">Restarting some services while hello cluster is running may generate alerts.</span></span> <span data-ttu-id="c9b5f-229">tooavoid 경고 hello를 사용할 수 있습니다 **서비스 작업** 단추 tooenable **유지 관리 모드** hello를 다시 시작을 수행 하기 전에 hello 서비스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-229">tooavoid alerts, you can use hello **Service Actions** button tooenable **Maintenance mode** for hello service before performing hello restart.</span></span>

3. <span data-ttu-id="c9b5f-230">작업을 선택 하 고 나면 hello **# op** 백그라운드 작업이 발생 하는 hello 페이지 단위로 tooshow hello 위쪽에 있는 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-230">Once an action has been selected, hello **# op** entry at hello top of hello page increments tooshow that a background operation is occurring.</span></span> <span data-ttu-id="c9b5f-231">Toodisplay 구성 된 경우 백그라운드 작업의 hello 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-231">If configured toodisplay, hello list of background operations is displayed.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c9b5f-232">사용 하도록 설정한 경우 **유지 관리 모드** 기억 toodisable hello 서비스에 대 한 hello를 사용 하 여 **서비스 작업** hello 작업이 완료 되 면 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-232">If you enabled **Maintenance mode** for hello service, remember toodisable it by using hello **Service Actions** button once hello operation has finished.</span></span>

<span data-ttu-id="c9b5f-233">서비스를 tooconfigure 단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-233">tooconfigure a service, use hello following steps:</span></span>

1. <span data-ttu-id="c9b5f-234">Hello에서 **대시보드** 또는 **서비스** 페이지에서 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-234">From hello **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="c9b5f-235">선택 hello **Configs** 탭 hello 현재 구성이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-235">Select hello **Configs** tab. hello current configuration is displayed.</span></span> <span data-ttu-id="c9b5f-236">이전 구성의 목록도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-236">A list of previous configurations is also displayed.</span></span>

    ![구성](./media/hdinsight-hadoop-manage-ambari/service-configs.png)

3. <span data-ttu-id="c9b5f-238">Hello 표시 되는 필드 toomodify hello 구성을 사용 하 여 선택한 후 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-238">Use hello fields displayed toomodify hello configuration, and then select **Save**.</span></span> <span data-ttu-id="c9b5f-239">또는 이전 구성을 선택한 다음 선택 **현재** tooroll toohello 이전 설정으로 리셋합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-239">Or select a previous configuration and then select **Make current** tooroll back toohello previous settings.</span></span>

## <a name="ambari-views"></a><span data-ttu-id="c9b5f-240">Ambari 뷰</span><span class="sxs-lookup"><span data-stu-id="c9b5f-240">Ambari views</span></span>

<span data-ttu-id="c9b5f-241">Ambari 뷰를 사용 하면 개발자가 tooplug UI 요소 hello Ambari 웹 UI에 hello를 사용 하 여 [Ambari 보기 프레임 워크](https://cwiki.apache.org/confluence/display/AMBARI/Views)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-241">Ambari Views allow developers tooplug UI elements into hello Ambari Web UI using hello [Ambari Views Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span></span> <span data-ttu-id="c9b5f-242">HDInsight은 Hadoop 클러스터 종류를 사용 하 여 뷰를 수행 하는 hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-242">HDInsight provides hello following views with Hadoop cluster types:</span></span>

* <span data-ttu-id="c9b5f-243">큐 관리자 yarn: hello 큐 관리자 보기 및 수정 YARN 큐에 대 한 간단한 UI를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-243">Yarn Queue Manager: hello queue manager provides a simple UI for viewing and modifying YARN queues.</span></span>

* <span data-ttu-id="c9b5f-244">하이브 보기: 보기 하이브 hello가 있습니다 웹 브라우저에서 직접 toorun 하이브 쿼리를.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-244">Hive View: hello Hive View allows you toorun Hive queries directly from your web browser.</span></span> <span data-ttu-id="c9b5f-245">쿼리 저장 결과 확인 또는 결과 toohello 클러스터 저장소에 저장 결과 tooyour 로컬 시스템을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-245">You can save queries, view results, save results toohello cluster storage, or download results tooyour local system.</span></span> <span data-ttu-id="c9b5f-246">Hive 뷰 사용에 대한 자세한 내용은 [HDInsight와 함께 Hive 뷰 사용](hdinsight-hadoop-use-hive-ambari-view.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-246">For more information on using Hive Views, see [Use Hive Views with HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>

* <span data-ttu-id="c9b5f-247">Tez 보기: hello Tez 보기 있습니다 toobetter 이해 하 고 작업을 최적화 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-247">Tez View: hello Tez View allows you toobetter understand and optimize jobs.</span></span> <span data-ttu-id="c9b5f-248">Tez 작업 실행 방법 및 사용되는 리소스에 대한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9b5f-248">You can view information on how Tez jobs are executed and what resources are used.</span></span>
