---
title: "Ambari 웹 UI를 사용하여 Azure HDInsight 모니터링 및 관리 | Microsoft Docs"
description: "Ambari를 사용하여 Linux 기반 HDInsight 클러스터를 모니터링하고 관리하는 방법에 대해 알아봅니다. 이 문서에서는 HDInsight 클러스터에 포함된 Ambari 웹 UI를 사용하는 방법을 배웁니다."
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
ms.openlocfilehash: dc0f9ff030f70985dad0f3b74ba0ee3dda1d9f4b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-hdinsight-clusters-by-using-the-ambari-web-ui"></a><span data-ttu-id="b7c4e-104">Ambari 웹 UI를 사용하여 HDInsight 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="b7c4e-104">Manage HDInsight clusters by using the Ambari Web UI</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="b7c4e-105">Apache Ambari는 손쉬운 웹 UI 및 REST API 사용을 제공하여 Hadoop 클러스터의 관리 및 모니터링을 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-105">Apache Ambari simplifies the management and monitoring of a Hadoop cluster by providing an easy to use web UI and REST API.</span></span> <span data-ttu-id="b7c4e-106">Ambari는 Linux 기반 HDInsight 클러스터에 포함되어 있으며 클러스터를 모니터링하고 구성을 변경하는데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-106">Ambari is included on Linux-based HDInsight clusters, and is used to monitor the cluster and make configuration changes.</span></span>

<span data-ttu-id="b7c4e-107">이 문서에서는 HDInsight 클러스터와 Ambari 웹 UI를 사용하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-107">In this document, you learn how to use the Ambari Web UI with an HDInsight cluster.</span></span>

## <span data-ttu-id="b7c4e-108"><a id="whatis"></a>Ambari 정의</span><span class="sxs-lookup"><span data-stu-id="b7c4e-108"><a id="whatis"></a>What is Ambari?</span></span>

<span data-ttu-id="b7c4e-109">[Apache Ambari](http://ambari.apache.org)는 사용하기 쉬운 웹 UI를 제공하여 Hadoop 관리를 단순화합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-109">[Apache Ambari](http://ambari.apache.org) simplifies Hadoop management by providing an easy-to-use web UI.</span></span> <span data-ttu-id="b7c4e-110">Ambari를 사용하여 Hadoop 클러스터를 생성, 관리 및 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-110">You can use Ambari create, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="b7c4e-111">개발자는 [Ambari REST API](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)를 사용하여 자신의 응용 프로그램에 이러한 기능을 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-111">Developers can integrate these capabilities into their applications by using the [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="b7c4e-112">Ambari 웹 UI는 기본적으로 Linux 운영 체제를 사용하는 HDInsight 클러스터와 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-112">The Ambari Web UI is provided by default with HDInsight clusters that use the Linux operating system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b7c4e-113">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-113">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b7c4e-114">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-114">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 

## <a name="connectivity"></a><span data-ttu-id="b7c4e-115">연결</span><span class="sxs-lookup"><span data-stu-id="b7c4e-115">Connectivity</span></span>

<span data-ttu-id="b7c4e-116">Ambari 웹 UI는 HTTPS://CLUSTERNAME.azurehdidnsnsight.net의 HDInsight 클러스터에서 사용할 수 있습니다. 여기서 **CLUSTERNAME**은 클러스터 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-116">The Ambari Web UI is available on your HDInsight cluster at HTTPS://CLUSTERNAME.azurehdidnsight.net, where **CLUSTERNAME** is the name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b7c4e-117">HTTPS를 요구하는 HDInsight에서 Ambari로 연결</span><span class="sxs-lookup"><span data-stu-id="b7c4e-117">Connecting to Ambari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="b7c4e-118">인증에 대한 대화 상자가 나타나면 클러스터를 만들 때 제공한 관리자 계정 이름 및 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-118">When prompted for authentication, use the admin account name and password you provided when the cluster was created.</span></span>

## <a name="ssh-tunnel-proxy"></a><span data-ttu-id="b7c4e-119">SSH 터널(프록시)</span><span class="sxs-lookup"><span data-stu-id="b7c4e-119">SSH tunnel (proxy)</span></span>

<span data-ttu-id="b7c4e-120">클러스터의 Ambari는 인터넷을 통해 직접 액세스할 수 있지만 Ambari 웹 UI의 일부 링크(예: JobTracker)는 인터넷에 노출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-120">While Ambari for your cluster is accessible directly over the Internet, some links from the Ambari Web UI (such as to the JobTracker) are not exposed on the internet.</span></span> <span data-ttu-id="b7c4e-121">이러한 서비스에 액세스하려면 SSH 터널을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-121">To access these services, you must create an SSH tunnel.</span></span> <span data-ttu-id="b7c4e-122">자세한 내용은 [HDInsight와 SSH 터널링 사용](hdinsight-linux-ambari-ssh-tunnel.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-122">For more information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

## <a name="ambari-web-ui"></a><span data-ttu-id="b7c4e-123">Ambari 웹 UI</span><span class="sxs-lookup"><span data-stu-id="b7c4e-123">Ambari Web UI</span></span>

<span data-ttu-id="b7c4e-124">Ambari 웹 UI를 연결할 때 페이지에 인증하라는 메시지가 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-124">When connecting to the Ambari Web UI, you are prompted to authenticate to the page.</span></span> <span data-ttu-id="b7c4e-125">클러스터를 만들 때 사용했던 클러스터 관리자 사용자(기본값 관리자)와 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-125">Use the cluster admin user (default Admin) and password you used during cluster creation.</span></span>

<span data-ttu-id="b7c4e-126">페이지가 열리면 위쪽의 표시줄을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-126">When the page opens, note the bar at the top.</span></span> <span data-ttu-id="b7c4e-127">이 표시줄에는 다음 정보 및 컨트롤이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-127">This bar contains the following information and controls:</span></span>

![ambari-nav](./media/hdinsight-hadoop-manage-ambari/ambari-nav.png)

* <span data-ttu-id="b7c4e-129">**Ambari 로고** - 클러스터를 모니터링하는 데 사용할 수 있는 대시보드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-129">**Ambari logo** - Opens the dashboard, which can be used to monitor the cluster.</span></span>

* <span data-ttu-id="b7c4e-130">**클러스터 이름 # ops** - 진행 중인 Ambari 작업 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-130">**Cluster name # ops** - Displays the number of ongoing Ambari operations.</span></span> <span data-ttu-id="b7c4e-131">클러스터 이름 또는 **# ops**를 선택하면 백그라운드 작업 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-131">Selecting the cluster name or **# ops** displays a list of background operations.</span></span>

* <span data-ttu-id="b7c4e-132">**# alerts** - 클러스터에 대한 경고 또는 중요한 알림(있을 경우)을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-132">**# alerts** - Displays warnings or critical alerts, if any, for the cluster.</span></span>

* <span data-ttu-id="b7c4e-133">**Dashboard** - 대시보드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-133">**Dashboard** - Displays the dashboard.</span></span>

* <span data-ttu-id="b7c4e-134">**Services** - 클러스터의 서비스에 대한 정보 및 구성 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-134">**Services** - Information and configuration settings for the services in the cluster.</span></span>

* <span data-ttu-id="b7c4e-135">**Hosts** - 클러스터의 노드에 대한 정보 및 구성 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-135">**Hosts** - Information and configuration settings for the nodes in the cluster.</span></span>

* <span data-ttu-id="b7c4e-136">**Alerts** - 정보, 경고 및 중요한 알림에 대한 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-136">**Alerts** - A log of information, warnings, and critical alerts.</span></span>

* <span data-ttu-id="b7c4e-137">**Admin** - 클러스터에 설치된 소프트웨어 스택/서비스, 서비스 계정 정보 및 Kerberos 보안입니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-137">**Admin** - Software stack/services that are installed on the cluster, service account information, and Kerberos security.</span></span>

* <span data-ttu-id="b7c4e-138">**Admin 단추** - Ambari 관리, 사용자 설정 및 로그 아웃입니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-138">**Admin button** - Ambari management, user settings, and logout.</span></span>

## <a name="monitoring"></a><span data-ttu-id="b7c4e-139">모니터링</span><span class="sxs-lookup"><span data-stu-id="b7c4e-139">Monitoring</span></span>

### <a name="alerts"></a><span data-ttu-id="b7c4e-140">경고</span><span class="sxs-lookup"><span data-stu-id="b7c4e-140">Alerts</span></span>

<span data-ttu-id="b7c4e-141">다음 목록은 Ambari에서 사용하는 일반적인 경고 상태를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-141">The following list contains the common alert statuses used by Ambari:</span></span>

* <span data-ttu-id="b7c4e-142">**OK**</span><span class="sxs-lookup"><span data-stu-id="b7c4e-142">**OK**</span></span>
* <span data-ttu-id="b7c4e-143">**Warning**</span><span class="sxs-lookup"><span data-stu-id="b7c4e-143">**Warning**</span></span>
* <span data-ttu-id="b7c4e-144">**CRITICAL**</span><span class="sxs-lookup"><span data-stu-id="b7c4e-144">**CRITICAL**</span></span>
* <span data-ttu-id="b7c4e-145">**UNKNOWN**</span><span class="sxs-lookup"><span data-stu-id="b7c4e-145">**UNKNOWN**</span></span>

<span data-ttu-id="b7c4e-146">**확인**이 아닌 다른 경고는 페이지 위쪽의 **# alerts** 항목에 경고 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-146">Alerts other than **OK** cause the **# alerts** entry at the top of the page to display the number of alerts.</span></span> <span data-ttu-id="b7c4e-147">이 항목을 선택하면 경고 및 해당 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-147">Selecting this entry displays the alerts and their status.</span></span>

<span data-ttu-id="b7c4e-148">경고는 여러 가지 기본 그룹으로 구성되며 **Alerts** 페이지에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-148">Alerts are organized into several default groups, which can be viewed from the **Alerts** page.</span></span>

![경고 페이지](./media/hdinsight-hadoop-manage-ambari/alerts.png)

<span data-ttu-id="b7c4e-150">**작업** 메뉴를 사용하고 **경고 그룹 관리**를 선택하여 그룹을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-150">You can manage the groups by using the **Actions** menu and selecting **Manage Alert Groups**.</span></span>

![경고 그룹 관리 대화 상자](./media/hdinsight-hadoop-manage-ambari/manage-alerts.png)

<span data-ttu-id="b7c4e-152">또한 __경고 알림 관리__를 선택하여 **작업** 메뉴에서 경고 방법을 관리하고 경고 알림을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-152">You can also manage alerting methods, and create alert notifications from the **Actions** menu by selecting __Manage Alert Notifications__.</span></span> <span data-ttu-id="b7c4e-153">모든 현재 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-153">Any current notifications are displayed.</span></span> <span data-ttu-id="b7c4e-154">여기에서 알림을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-154">You can also create notifications from here.</span></span> <span data-ttu-id="b7c4e-155">특정 경고/심각도 조합이 발생하면 **전자 메일** 또는 **SNMP**를 통해 알림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-155">Notifications can be sent via **EMAIL** or **SNMP** when specific alert/severity combinations occur.</span></span> <span data-ttu-id="b7c4e-156">예를 들어 **YARN Default** 그룹에 **위험**으로 설정된 경고가 있으면 전자 메일 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-156">For example, you can send an email message when any of the alerts in the **YARN Default** group is set to **Critical**.</span></span>

![경고 만들기 대화 상자](./media/hdinsight-hadoop-manage-ambari/create-alert-notification.png)

<span data-ttu-id="b7c4e-158">마지막으로, __작업__ 메뉴에서 __경고 설정 관리__를 선택하면 알림을 보내기 전에 경고가 발생해야 하는 횟수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-158">Finally, selecting __Manage Alert Settings__ from the __Actions__ menu allows you to set the number of times an alert must occur before a notification is sent.</span></span> <span data-ttu-id="b7c4e-159">일시적인 오류에 대한 알림을 방지하는 데 이 설정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-159">This setting can be used to prevent notifications for transient errors.</span></span>

### <a name="cluster"></a><span data-ttu-id="b7c4e-160">프로비전</span><span class="sxs-lookup"><span data-stu-id="b7c4e-160">Cluster</span></span>

<span data-ttu-id="b7c4e-161">대시보드의 **Metrics** 탭은 클러스터의 상태를 한 눈에 쉽게 모니터할 수 있는 일련의 위젯을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-161">The **Metrics** tab of the dashboard contains a series of widgets that make it easy to monitor the status of your cluster at a glance.</span></span> <span data-ttu-id="b7c4e-162">**CPU Usage**와 같은 여러 위젯은 클릭하면 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-162">Several widgets, such as **CPU Usage**, provide additional information when clicked.</span></span>

![메트릭이 표시된 대시보드](./media/hdinsight-hadoop-manage-ambari/metrics.png)

<span data-ttu-id="b7c4e-164">**Heatmaps** 탭은 녹색에서 빨간색으로 변하는 히트맵처럼 메트릭을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-164">The **Heatmaps** tab displays metrics as colored heatmaps, going from green to red.</span></span>

![히트맵이 표시된 대시보드](./media/hdinsight-hadoop-manage-ambari/heatmap.png)

<span data-ttu-id="b7c4e-166">클러스터 내의 노드에 대한 자세한 내용은 **호스트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-166">For more information on the nodes within the cluster, select **Hosts**.</span></span> <span data-ttu-id="b7c4e-167">그런 다음 관심 있는 특정 노드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-167">Then select the specific node you are interested in.</span></span>

![호스트 세부 정보](./media/hdinsight-hadoop-manage-ambari/host-details.png)

### <a name="services"></a><span data-ttu-id="b7c4e-169">Services</span><span class="sxs-lookup"><span data-stu-id="b7c4e-169">Services</span></span>

<span data-ttu-id="b7c4e-170">대시보드의 **Services** 세로 막대는 클러스터에서 실행되는 서비스 상태에 대한 빠른 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-170">The **Services** sidebar on the dashboard provides quick insight into the status of the services running on the cluster.</span></span> <span data-ttu-id="b7c4e-171">다양한 아이콘은 수행해야 하는 상태 또는 작업을 나타내는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-171">Various icons are used to indicate status or actions that should be taken.</span></span> <span data-ttu-id="b7c4e-172">예를 들어 서비스가 재활용되어야 하는 경우 노란색 재활용 기호가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-172">For example, a yellow recycle symbol is displayed if a service needs to be recycled.</span></span>

![서비스 세로 막대](./media/hdinsight-hadoop-manage-ambari/service-bar.png)

> [!NOTE]
> <span data-ttu-id="b7c4e-174">표시된 서비스는 HDInsight 클러스터 유형과 버전 간에 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-174">The services displayed differ between HDInsight cluster types and versions.</span></span> <span data-ttu-id="b7c4e-175">여기에 표시된 서비스는 클러스터에 대해 표시된 서비스와 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-175">The services displayed here may be different than the services displayed for your cluster.</span></span>

<span data-ttu-id="b7c4e-176">서비스를 선택하면 해당 서비스에 대한 자세한 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-176">Selecting a service displays more detailed information on the service.</span></span>

![서비스 요약 정보](./media/hdinsight-hadoop-manage-ambari/service-details.png)

#### <a name="quick-links"></a><span data-ttu-id="b7c4e-178">빠른 링크</span><span class="sxs-lookup"><span data-stu-id="b7c4e-178">Quick links</span></span>

<span data-ttu-id="b7c4e-179">일부 서비스는 페이지의 위쪽에 **Quick Links** 링크를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-179">Some services display a **Quick Links** link at the top of the page.</span></span> <span data-ttu-id="b7c4e-180">이를 사용하여 서비스 관련 웹 UI에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-180">This can be used to access service-specific web UIs, such as:</span></span>

* <span data-ttu-id="b7c4e-181">**Job History** - MapReduce 작업 기록</span><span class="sxs-lookup"><span data-stu-id="b7c4e-181">**Job History** - MapReduce job history.</span></span>
* <span data-ttu-id="b7c4e-182">**Resource Manager** - YARN ResourceManager UI</span><span class="sxs-lookup"><span data-stu-id="b7c4e-182">**Resource Manager** - YARN ResourceManager UI.</span></span>
* <span data-ttu-id="b7c4e-183">**NameNode** - HDFS(Hadoop Distributed File System) NameNode UI</span><span class="sxs-lookup"><span data-stu-id="b7c4e-183">**NameNode** - Hadoop Distributed File System (HDFS) NameNode UI.</span></span>
* <span data-ttu-id="b7c4e-184">**Oozie Web UI** - Oozie UI</span><span class="sxs-lookup"><span data-stu-id="b7c4e-184">**Oozie Web UI** - Oozie UI.</span></span>

<span data-ttu-id="b7c4e-185">이러한 링크 중 하나를 선택하면 브라우저에서 선택한 페이지를 표시하는 새 탭이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-185">Selecting any of these links opens a new tab in your browser, which displays the selected page.</span></span>

> [!NOTE]
> <span data-ttu-id="b7c4e-186">서비스에 대해 **빠른 링크** 항목을 선택하면 "서버를 찾을 수 없음" 오류를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-186">Selecting the **Quick Links** entry for a service may return a "server not found" error.</span></span> <span data-ttu-id="b7c4e-187">이 오류가 발생하는 경우 이 서비스에 대해 **빠른 링크** 항목을 사용할 때 SSH 터널을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-187">If you encounter this error, you must use an SSH tunnel when using the **Quick Links** entry for this service.</span></span> <span data-ttu-id="b7c4e-188">자세한 내용은 [HDInsight와 SSH 터널링 사용](hdinsight-linux-ambari-ssh-tunnel.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-188">For information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)</span></span>

## <a name="management"></a><span data-ttu-id="b7c4e-189">관리</span><span class="sxs-lookup"><span data-stu-id="b7c4e-189">Management</span></span>

### <a name="ambari-users-groups-and-permissions"></a><span data-ttu-id="b7c4e-190">Ambari 사용자, 그룹 및 사용 권한</span><span class="sxs-lookup"><span data-stu-id="b7c4e-190">Ambari users, groups, and permissions</span></span>

<span data-ttu-id="b7c4e-191">[도메인 가입](hdinsight-domain-joined-introduction.md) HDInsight 클러스터를 사용할 때 사용자, 그룹 및 권한을 사용하는 작업이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-191">Working with users, groups, and permissions are supported when using a [domain joined](hdinsight-domain-joined-introduction.md) HDInsight cluster.</span></span> <span data-ttu-id="b7c4e-192">도메인 가입 클러스터에서 Ambari 관리 UI를 사용하는 방법에 대한 자세한 내용은 [도메인 가입 HDInsight 클러스터 관리](hdinsight-domain-joined-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-192">For information on using the Ambari Management UI on a domain-joined cluster, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-introduction.md).</span></span>

> [!WARNING]
> <span data-ttu-id="b7c4e-193">Linux 기반 HDInsight 클러스터에서 Ambari watchdog(hdinsightwatchdog)의 암호는 변경하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-193">Do not change the password of the Ambari watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="b7c4e-194">암호를 변경하면 스크립트 동작을 사용하거나 클러스터에서 크기 조정 작업을 수행하는 기능이 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-194">Changing the password breaks the ability to use script actions or perform scaling operations with your cluster.</span></span>

### <a name="hosts"></a><span data-ttu-id="b7c4e-195">호스트</span><span class="sxs-lookup"><span data-stu-id="b7c4e-195">Hosts</span></span>

<span data-ttu-id="b7c4e-196">**Hosts** 페이지는 클러스터의 모든 호스트를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-196">The **Hosts** page lists all hosts in the cluster.</span></span> <span data-ttu-id="b7c4e-197">호스트를 관리하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-197">To manage hosts, follow these steps.</span></span>

![호스트 페이지](./media/hdinsight-hadoop-manage-ambari/hosts.png)

> [!NOTE]
> <span data-ttu-id="b7c4e-199">호스트 추가, 서비스 해제 및 서비스 등록은 HDInsight 클러스터에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-199">Adding, decommissioning, and recommissioning a host should not be used with HDInsight clusters.</span></span>

1. <span data-ttu-id="b7c4e-200">관리하려는 호스트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-200">Select the host that you wish to manage.</span></span>

2. <span data-ttu-id="b7c4e-201">**Actions** 메뉴를 사용하여 수행할 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-201">Use the **Actions** menu to select the action that you wish to perform:</span></span>

   * <span data-ttu-id="b7c4e-202">**Start all components** - 호스트에서 모든 구성 요소를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-202">**Start all components** - Start all components on the host.</span></span>

   * <span data-ttu-id="b7c4e-203">**Stop all components** - 호스트에서 모든 구성 요소를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-203">**Stop all components** - Stop all components on the host.</span></span>

   * <span data-ttu-id="b7c4e-204">**Restart all components** - 호스트에서 모든 구성 요소를 중지하고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-204">**Restart all components** - Stop and start all components on the host.</span></span>

   * <span data-ttu-id="b7c4e-205">**Turn on maintenance mode** - 호스트에 대한 경고를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-205">**Turn on maintenance mode** - Suppresses alerts for the host.</span></span> <span data-ttu-id="b7c4e-206">경고를 생성하는 작업을 수행하는 경우 이 모드를 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-206">This mode should be enabled if you are performing actions that generate alerts.</span></span> <span data-ttu-id="b7c4e-207">예를 들어 서비스를 중지하고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-207">For example, stopping and starting a service.</span></span>

   * <span data-ttu-id="b7c4e-208">**Turn off maintenance mode** - 호스트를 정상 경고 상태로 되돌립니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-208">**Turn off maintenance mode** - Returns the host to normal alerting.</span></span>

   * <span data-ttu-id="b7c4e-209">**Stop** - 호스트에서 DataNode 또는 NodeManagers를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-209">**Stop** - Stops DataNode or NodeManagers on the host.</span></span>

   * <span data-ttu-id="b7c4e-210">**Start** - 호스트에서 DataNode 또는 NodeManagers를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-210">**Start** - Starts DataNode or NodeManagers on the host.</span></span>

   * <span data-ttu-id="b7c4e-211">**Restart** - 호스트에서 DataNode 또는 NodeManagers를 중지하고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-211">**Restart** - Stops and starts DataNode or NodeManagers on the host.</span></span>

   * <span data-ttu-id="b7c4e-212">**Decommission** - 호스트를 클러스터에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-212">**Decommission** - Removes a host from the cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="b7c4e-213">HDInsight 클러스터에서는 이 작업을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-213">Do not use this action on HDInsight clusters.</span></span>

   * <span data-ttu-id="b7c4e-214">**Recommission** - 이전에 서비스를 해지한 호스트를 클러스터에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-214">**Recommission** - Adds a previously decommissioned host to the cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="b7c4e-215">HDInsight 클러스터에서는 이 작업을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-215">Do not use this action on HDInsight clusters.</span></span>

### <span data-ttu-id="b7c4e-216"><a id="service"></a>Services</span><span class="sxs-lookup"><span data-stu-id="b7c4e-216"><a id="service"></a>Services</span></span>

<span data-ttu-id="b7c4e-217">**대시보드** 또는 **서비스** 페이지에서 서비스 목록 아래쪽의 **작업** 단추를 사용하여 모든 서비스를 중지하고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-217">From the **Dashboard** or **Services** page, use the **Actions** button at the bottom of the list of services to stop and start all services.</span></span>

![Service Actions](./media/hdinsight-hadoop-manage-ambari/service-actions.png)

> [!WARNING]
> <span data-ttu-id="b7c4e-219">이 메뉴에 나열되어 있는 **서비스 추가**는 HDInsight 클러스터에 서비스를 추가하는 데 사용하면 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-219">While **Add Service** is listed in this menu, it should not be used to add services to the HDInsight cluster.</span></span> <span data-ttu-id="b7c4e-220">클러스터를 프로비전하는 동안 스크립트 작업을 사용하여 새 서비스를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-220">New services should be added using a Script Action during cluster provisioning.</span></span> <span data-ttu-id="b7c4e-221">스크립트 작업에 대한 자세한 내용은 [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-221">For more information on using Script Actions, see [Customize HDInsight clusters using Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="b7c4e-222">**Actions** 단추는 모든 서비스를 다시 시작할 수 있는 반면, 특정 서비스를 시작하거나 중지, 다시 시작하려는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-222">While the **Actions** button can restart all services, often you want to start, stop, or restart a specific service.</span></span> <span data-ttu-id="b7c4e-223">다음 단계를 사용하여 개별 서비스에서 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-223">Use the following steps to perform actions on an individual service:</span></span>

1. <span data-ttu-id="b7c4e-224">**대시보드** 또는 **서비스** 페이지에서 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-224">From the **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="b7c4e-225">**요약** 탭 위쪽에서 **서비스 작업** 단추를 사용하여 수행할 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-225">From the top of the **Summary** tab, use the **Service Actions** button and select the action to take.</span></span> <span data-ttu-id="b7c4e-226">모든 노드의 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-226">This restarts the service on all nodes.</span></span>

    ![서비스 작업](./media/hdinsight-hadoop-manage-ambari/individual-service-actions.png)

   > [!NOTE]
   > <span data-ttu-id="b7c4e-228">클러스터가 실행되는 동안 일부 서비스를 다시 시작하면 경고가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-228">Restarting some services while the cluster is running may generate alerts.</span></span> <span data-ttu-id="b7c4e-229">경고를 방지하려면 **서비스 작업** 단추를 사용하여 다시 시작하기 전에 서비스에 대한 **유지 관리 모드**를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-229">To avoid alerts, you can use the **Service Actions** button to enable **Maintenance mode** for the service before performing the restart.</span></span>

3. <span data-ttu-id="b7c4e-230">동작이 선택되어 있고, 백그라운드 작업이 발생하면 페이지 위쪽에 있는 **# op** 항목의 숫자가 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-230">Once an action has been selected, the **# op** entry at the top of the page increments to show that a background operation is occurring.</span></span> <span data-ttu-id="b7c4e-231">백그라운드 작업 목록을 표시하도록 구성한 경우 백그라운드 작업 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-231">If configured to display, the list of background operations is displayed.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b7c4e-232">서비스에 대한 **유지 관리 모드**를 사용하도록 설정하여 작업이 완료된 후에는 **서비스 작업** 단추를 사용하여 이 모드를 해제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-232">If you enabled **Maintenance mode** for the service, remember to disable it by using the **Service Actions** button once the operation has finished.</span></span>

<span data-ttu-id="b7c4e-233">서비스를 구성하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-233">To configure a service, use the following steps:</span></span>

1. <span data-ttu-id="b7c4e-234">**대시보드** 또는 **서비스** 페이지에서 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-234">From the **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="b7c4e-235">**Configs** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-235">Select the **Configs** tab.</span></span> <span data-ttu-id="b7c4e-236">현재 구성이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-236">The current configuration is displayed.</span></span> <span data-ttu-id="b7c4e-237">이전 구성의 목록도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-237">A list of previous configurations is also displayed.</span></span>

    ![구성](./media/hdinsight-hadoop-manage-ambari/service-configs.png)

3. <span data-ttu-id="b7c4e-239">구성을 수정하려면 표시된 목록을 클릭하고 **Save**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-239">Use the fields displayed to modify the configuration, and then select **Save**.</span></span> <span data-ttu-id="b7c4e-240">또는 이전 구성을 선택한 다음 **Make current** 를 선택하여 이전 설정으로 롤백할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-240">Or select a previous configuration and then select **Make current** to roll back to the previous settings.</span></span>

## <a name="ambari-views"></a><span data-ttu-id="b7c4e-241">Ambari 뷰</span><span class="sxs-lookup"><span data-stu-id="b7c4e-241">Ambari views</span></span>

<span data-ttu-id="b7c4e-242">Ambari 뷰를 사용하면 개발자가 [Ambari 보기 프레임워크](https://cwiki.apache.org/confluence/display/AMBARI/Views)를 사용하여 Ambari 웹 UI에 UI 요소를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-242">Ambari Views allow developers to plug UI elements into the Ambari Web UI using the [Ambari Views Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span></span> <span data-ttu-id="b7c4e-243">HDInsight은 Hadoop 클러스터 종류를 사용하여 다음 뷰를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-243">HDInsight provides the following views with Hadoop cluster types:</span></span>

* <span data-ttu-id="b7c4e-244">Yarn 큐 관리자: 큐 관리자는 YARN 큐를 보고 수정하기 위한 간단한 UI를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-244">Yarn Queue Manager: The queue manager provides a simple UI for viewing and modifying YARN queues.</span></span>

* <span data-ttu-id="b7c4e-245">Hive 뷰: Hive 뷰를 사용하면 웹 브라우저에서 직접 Hive 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-245">Hive View: The Hive View allows you to run Hive queries directly from your web browser.</span></span> <span data-ttu-id="b7c4e-246">쿼리를 저장하고 결과 확인하며 클러스터 저장소에 결과를 저장하거나 로컬 시스템에 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-246">You can save queries, view results, save results to the cluster storage, or download results to your local system.</span></span> <span data-ttu-id="b7c4e-247">Hive 뷰 사용에 대한 자세한 내용은 [HDInsight와 함께 Hive 뷰 사용](hdinsight-hadoop-use-hive-ambari-view.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-247">For more information on using Hive Views, see [Use Hive Views with HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>

* <span data-ttu-id="b7c4e-248">Tez 보기: Tez 뷰를 사용하면 작업을 더 잘 이해하고 최적화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-248">Tez View: The Tez View allows you to better understand and optimize jobs.</span></span> <span data-ttu-id="b7c4e-249">Tez 작업 실행 방법 및 사용되는 리소스에 대한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c4e-249">You can view information on how Tez jobs are executed and what resources are used.</span></span>
