---
title: "Apache 피닉스 aaaUse 및 Windows 기반 Azure HDInsight와 스 쿼 럴 | Microsoft Docs"
description: "자세한 방법을 toouse, HDInsight의 Apache 피닉스 방법과 tooinstall 스 쿼 럴 HDInsight에서 워크스테이션 tooconnect tooan HBase 클러스터에 구성 합니다."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1a756e98-75c1-44cd-a178-c5119683b7b7
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 147ac35fa882fd1bedbc5361ac804c36a4d56de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-and-squirrel-with-windows-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="d9708-103">HDInsight에서 Windows 기반 HBase 클러스터와 함께 Apache Phoenix 및 SQuirreL 사용</span><span class="sxs-lookup"><span data-stu-id="d9708-103">Use Apache Phoenix and SQuirreL with Windows-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="d9708-104">자세한 방법을 toouse [Apache 피닉스](http://phoenix.apache.org/) , HDInsight의 방법과 tooinstall 스 쿼 럴 HDInsight에서 워크스테이션 tooconnect tooan HBase 클러스터에 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-104">Learn how toouse [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how tooinstall and configure SQuirreL on your workstation tooconnect tooan HBase cluster in HDInsight.</span></span> <span data-ttu-id="d9708-105">Phoenix에 대한 자세한 내용은 [15분 이내의 Phoenix](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9708-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="d9708-106">Hello 피닉스 문법에 대 한 참조 [피닉스 문법](http://phoenix.apache.org/language/index.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-106">For hello Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="d9708-107">HDInsight의 버전 정보 피닉스 hello에 대 한 참조 [HDInsight에서 제공 하는 hello Hadoop 클러스터 버전의 새로운 기능?](hdinsight-component-versioning.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-107">For hello Phoenix version information in HDInsight, see [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>

> [!IMPORTANT]
> <span data-ttu-id="d9708-108">hello 단계에서 Windows 기반 HDInsight 클러스터에 대 한이 문서 에서만 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-108">hello steps in this document only work for Windows-based HDInsight clusters.</span></span> <span data-ttu-id="d9708-109">HDInsight는 HDInsight 3.4 이하 버전의 경우 Windows에서만 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-109">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="d9708-110">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d9708-111">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9708-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="d9708-112">Linux 기반 HDInsight에서 Phoenix 사용 방법에 대한 자세한 내용은 [HDInsight의 Linux 기반 HBase 클러스터와 함께 Apache Phoenix 사용](hdinsight-hbase-phoenix-squirrel-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9708-112">For information on using Phoenix on Linux-based HDInsight, see [Use Apache Phoenix with Linux-based HBase clusters in HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).</span></span>
>



## <a name="use-sqlline"></a><span data-ttu-id="d9708-113">SQLLine 사용</span><span class="sxs-lookup"><span data-stu-id="d9708-113">Use SQLLine</span></span>
<span data-ttu-id="d9708-114">[SQLLine](http://sqlline.sourceforge.net/) 명령줄 유틸리티 tooexecute SQL 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-114">[SQLLine](http://sqlline.sourceforge.net/) is a command line utility tooexecute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="d9708-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d9708-115">Prerequisites</span></span>
<span data-ttu-id="d9708-116">SQLLine를 사용 하려면 먼저 hello 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-116">Before you can use SQLLine, you must have hello following:</span></span>

* <span data-ttu-id="d9708-117">**HDInsight의 HBase 클러스터**.</span><span class="sxs-lookup"><span data-stu-id="d9708-117">**A HBase cluster in HDInsight**.</span></span> <span data-ttu-id="d9708-118">HBase 클러스터 프로비전에 대한 자세한 내용은 [HDInsight에서 Apache HBase 시작][hdinsight-hbase-get-started]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9708-118">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="d9708-119">**Hello 원격 데스크톱 프로토콜을 통해 toohello HBase 클러스터를 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-119">**Connect toohello HBase cluster via hello remote desktop protocol**.</span></span> <span data-ttu-id="d9708-120">자세한 내용은 [hello Azure 클래식 포털을 사용 하 여 HDInsight의 Hadoop 관리 클러스터][hdinsight-manage-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-120">For instructions, see [Manage Hadoop clusters in HDInsight by using hello Azure Classic Portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="d9708-121">**toofind hello 호스트 이름**</span><span class="sxs-lookup"><span data-stu-id="d9708-121">**toofind out hello host name**</span></span>

1. <span data-ttu-id="d9708-122">열기 **Hadoop 명령줄** hello 바탕 화면에서.</span><span class="sxs-lookup"><span data-stu-id="d9708-122">Open **Hadoop Command Line** from hello desktop.</span></span>
2. <span data-ttu-id="d9708-123">Hello 명령 tooget hello DNS 접미사를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-123">Run hello following command tooget hello DNS suffix:</span></span>

        ipconfig

    <span data-ttu-id="d9708-124">**연결별 DNS 접미사**를 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-124">Write down **Connection-specific DNS Suffix**.</span></span> <span data-ttu-id="d9708-125">예를 들면 *myhbasecluster.f5.internal.cloudapp.net*과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-125">For example, *myhbasecluster.f5.internal.cloudapp.net*.</span></span> <span data-ttu-id="d9708-126">Tooan HBase 클러스터를 연결 하면의 FQDN을 사용 하 여 hello 사육 tooconnect tooone가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-126">When you connect tooan HBase cluster, you will need tooconnect tooone of hello Zookeepers using FQDN.</span></span> <span data-ttu-id="d9708-127">각 HDInsight 클러스터에는 3개의 Zookeeper,</span><span class="sxs-lookup"><span data-stu-id="d9708-127">Each HDInsight cluster has 3 Zookeepers.</span></span> <span data-ttu-id="d9708-128">*zookeeper0*, *zookeeper1* 및 *zookeeper2*가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-128">They are *zookeeper0*, *zookeeper1*, and *zookeeper2*.</span></span> <span data-ttu-id="d9708-129">hello FQDN 됩니다 다음과 같이 *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-129">hello FQDN will be something like *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span></span>

<span data-ttu-id="d9708-130">**toouse SQLLine**</span><span class="sxs-lookup"><span data-stu-id="d9708-130">**toouse SQLLine**</span></span>

1. <span data-ttu-id="d9708-131">열기 **Hadoop 명령줄** hello 바탕 화면에서.</span><span class="sxs-lookup"><span data-stu-id="d9708-131">Open **Hadoop Command Line** from hello desktop.</span></span>
2. <span data-ttu-id="d9708-132">다음 명령을 tooopen SQLLine hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-132">Run hello following commands tooopen SQLLine:</span></span>

        cd %phoenix_home%\bin
        sqlline.py [hello FQDN of one of hello Zookeepers]

    ![HDInsight hbase phoenix sqlline][hdinsight-hbase-phoenix-sqlline]

    <span data-ttu-id="d9708-134">hello 샘플에 사용 된 hello 명령:</span><span class="sxs-lookup"><span data-stu-id="d9708-134">hello commands used in hello sample:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

<span data-ttu-id="d9708-135">자세한 내용은 [SQLLine 설명서](http://sqlline.sourceforge.net/#manual) 및 [Phoenix 문법](http://phoenix.apache.org/language/index.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9708-135">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="use-squirrel"></a><span data-ttu-id="d9708-136">SQuirrel 사용</span><span class="sxs-lookup"><span data-stu-id="d9708-136">Use SQuirreL</span></span>
<span data-ttu-id="d9708-137">[SQL 클라이언트 스 쿼 럴](http://squirrel-sql.sourceforge.net/) 됩니다 tooview hello 구조의 JDBC 규격 데이터베이스를 사용 하면 hello 테이블의에서 데이터를 찾아보고 등 SQL 명령을 실행 하는 그래픽 Java 프로그램입니다. 사용 되는 tooconnect tooApache HDInsight의 피닉스 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-137">[SQuirreL SQL Client](http://squirrel-sql.sourceforge.net/) is a graphical Java program that will allow you tooview hello structure of a JDBC compliant database, browse hello data in tables, issue SQL commands etc. It can be used tooconnect tooApache Phoenix on HDInsight.</span></span>

<span data-ttu-id="d9708-138">이 섹션에서는 tooinstall 스 쿼 럴 VPN 통해 HDInsight에서 워크스테이션 tooconnect tooan HBase 클러스터에 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-138">This section shows you how tooinstall and configure SQuirreL on your workstation tooconnect tooan HBase cluster in HDInsight via VPN.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="d9708-139">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d9708-139">Prerequisites</span></span>
<span data-ttu-id="d9708-140">Hello 절차를 수행 하기 전에 hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-140">Before following hello procedures, you must have hello following:</span></span>

* <span data-ttu-id="d9708-141">HBase 클러스터 tooan Azure 가상 네트워크 DNS 가상 컴퓨터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-141">An HBase cluster deployed tooan Azure virtual network with a DNS virtual machine.</span></span>  <span data-ttu-id="d9708-142">자세한 내용은 [Azure Virtual Network에 HBase 클러스터 만들기][hdinsight-hbase-provision-vnet]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9708-142">For instructions, see [Create HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet].</span></span>

* <span data-ttu-id="d9708-143">Hello HBase 클러스터 클러스터 연결별 DNS 접미사를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-143">Get hello HBase cluster cluster Connection-specific DNS suffix.</span></span> <span data-ttu-id="d9708-144">tooget 것 hello 클러스터에 RDP 다음 IPConfig를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-144">tooget it, RDP into hello cluster, and then run IPConfig.</span></span>  <span data-ttu-id="d9708-145">hello DNS 접미사는 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-145">hello DNS suffix is similar to:</span></span>

        myhbase.b7.internal.cloudapp.net
* <span data-ttu-id="d9708-146">워크스테이션에서 [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx)을 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-146">Download and install [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) on your workstation.</span></span> <span data-ttu-id="d9708-147">Makecert hello 패키지 toocreate에서 인증서가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-147">You will need makecert from hello package toocreate your certificate.</span></span>  
* <span data-ttu-id="d9708-148">워크스테이션에서 [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) 을 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-148">Download and install [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) on your workstation.</span></span>  <span data-ttu-id="d9708-149">SQuirreL SQL Client 버전 3.0 이상에는 JRE 버전 1.6 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-149">SQuirreL SQL client version 3.0 and higher requires JRE version 1.6 or higher.</span></span>  

### <a name="configure-a-point-to-site-vpn-connection-toohello-azure-virtual-network"></a><span data-ttu-id="d9708-150">지점-사이트 VPN 연결 toohello Azure 가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="d9708-150">Configure a Point-to-Site VPN connection toohello Azure virtual network</span></span>
<span data-ttu-id="d9708-151">지점 및 사이트 간 VPN 연결을 구성하는 단계는 3단계로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-151">There are 3 steps involved configuring a point-to-site VPN connection:</span></span>

1. [<span data-ttu-id="d9708-152">가상 네트워크 및 동적 라우팅 게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="d9708-152">Configure a virtual network and a dynamic routing gateway</span></span>](#Configure-a-virtual-network-and-a-dynamic-routing-gateway)
2. [<span data-ttu-id="d9708-153">인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="d9708-153">Create your certificates</span></span>](#Create-your-certificates)
3. [<span data-ttu-id="d9708-154">VPN 클라이언트 구성</span><span class="sxs-lookup"><span data-stu-id="d9708-154">Configure your VPN client</span></span>](#Configure-your-VPN-client)

<span data-ttu-id="d9708-155">참조 [지점-사이트 VPN 연결 tooan Azure 가상 네트워크 구성](../vpn-gateway/vpn-gateway-point-to-site-create.md) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-155">See [Configure a Point-to-Site VPN connection tooan Azure Virtual Network](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>

#### <a name="configure-a-virtual-network-and-a-dynamic-routing-gateway"></a><span data-ttu-id="d9708-156">가상 네트워크 및 동적 라우팅 게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="d9708-156">Configure a virtual network and a dynamic routing gateway</span></span>
<span data-ttu-id="d9708-157">Azure 가상 네트워크에서 HBase 클러스터를 프로 비전을 위해 (이 섹션에 대 한 hello 필수 구성 요소 참조).</span><span class="sxs-lookup"><span data-stu-id="d9708-157">Assure you have provisioned an HBase cluster in an Azure virtual network (see hello prerequisites for this section).</span></span> <span data-ttu-id="d9708-158">hello 다음 단계는 tooconfigure 지점 및 사이트 간 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-158">hello next step is tooconfigure a point-to-site connection.</span></span>

<span data-ttu-id="d9708-159">**tooconfigure hello 지점 및 사이트 연결**</span><span class="sxs-lookup"><span data-stu-id="d9708-159">**tooconfigure hello point-to-site connectivity**</span></span>

1. <span data-ttu-id="d9708-160">Toohello 로그인 [Azure 클래식 포털][azure-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-160">Sign in toohello [Azure Classic Portal][azure-portal].</span></span>
2. <span data-ttu-id="d9708-161">Hello 왼쪽에서 클릭 **네트워크**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-161">On hello left, click **NETWORKS**.</span></span>
3. <span data-ttu-id="d9708-162">만든 hello 가상 네트워크를 클릭 합니다. (참조 [Azure 가상 네트워크에서 프로 비전 HBase 클러스터][hdinsight-hbase-provision-vnet]).</span><span class="sxs-lookup"><span data-stu-id="d9708-162">Click hello virtual network you have created (see [Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]).</span></span>
4. <span data-ttu-id="d9708-163">클릭 **구성** hello 위에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-163">Click **CONFIGURE** from hello top.</span></span>
5. <span data-ttu-id="d9708-164">Hello에 **지점 및 사이트 연결** 섹션에서 **지점 및 사이트 연결을 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-164">In hello **point-to-site connectivity** section, select **Configure point-to-site connectivity**.</span></span>
6. <span data-ttu-id="d9708-165">구성 **시작 IP** 및 **CIDR** toospecify hello IP 주소 범위를 VPN 클라이언트가 수신할 IP 주소 연결 된 경우.</span><span class="sxs-lookup"><span data-stu-id="d9708-165">Configure **STARTING IP** and **CIDR** toospecify hello IP address range from which your VPN clients will receive an IP address when connected.</span></span> <span data-ttu-id="d9708-166">온-프레미스에 있는 범위 네트워크 및 Azure 가상 네트워크에 연결 hello hello를 사용 하 여 hello 범위 겹칠 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-166">hello range cannot overlap with any of hello ranges located on your on-premises network and hello Azure virtual network you will be connecting to.</span></span> <span data-ttu-id="d9708-167">예를 들어 모바일 서비스는 스크립트 실행 간에 상태를 유지하지 않으므로 스크립트 실행 간에 지속되어야 하는 모든 데이터를 테이블에 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-167">For example.</span></span> <span data-ttu-id="d9708-168">10.0.0.0/20 hello 가상 네트워크를 선택한 경우에 hello 클라이언트 주소 공간에 대 한 10.1.0.0/24를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-168">if you selected 10.0.0.0/20 for hello virtual network, you can select 10.1.0.0/24 for hello client address space.</span></span> <span data-ttu-id="d9708-169">Hello 참조 [지점 및 사이트 연결] [ vnet-point-to-site-connectivity] 자세한 내용을 보려면 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-169">See hello [Point-To-Site Connectivity][vnet-point-to-site-connectivity] page for more information.</span></span>
7. <span data-ttu-id="d9708-170">Hello 가상 네트워크 주소 공간 섹션에서 클릭 **게이트웨이 서브넷 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-170">In hello virtual network address spaces section, click **add gateway subnet**.</span></span>
8. <span data-ttu-id="d9708-171">클릭 **저장** hello hello 페이지 아래쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-171">Click **SAVE** on hello bottom of hello page.</span></span>
9. <span data-ttu-id="d9708-172">클릭 **예** tooconfirm hello 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-172">Click **YES** tooconfirm hello change.</span></span> <span data-ttu-id="d9708-173">Hello 시스템에서 변경할 toohello 다음 절차를 계속 하기 전에 hello 만들기를 완료할 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-173">Wait until hello system has finished making hello change before you proceed toohello next procedure.</span></span>

<span data-ttu-id="d9708-174">**동적 라우팅 게이트웨이 toocreate**</span><span class="sxs-lookup"><span data-stu-id="d9708-174">**toocreate a dynamic routing gateway**</span></span>

1. <span data-ttu-id="d9708-175">Hello Azure 클래식 포털에서에서 클릭 **대시보드** hello hello 페이지 위쪽에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-175">From hello Azure Classic Portal, click **DASHBOARD** from hello top of hello page.</span></span>
2. <span data-ttu-id="d9708-176">클릭 **게이트웨이 만들기** hello hello 페이지 아래에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-176">Click **CREATE GATEWAY** from hello bottom of hello page.</span></span>
3. <span data-ttu-id="d9708-177">클릭 **예** tooconfirm 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-177">Click **YES** tooconfirm.</span></span> <span data-ttu-id="d9708-178">Hello 게이트웨이 만들어질 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-178">Wait until hello gateway is created.</span></span>
4. <span data-ttu-id="d9708-179">클릭 **대시보드** hello 위에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-179">Click **DASHBOARD** from hello top.</span></span>  <span data-ttu-id="d9708-180">Hello 가상 네트워크의 시각적 다이어그램을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-180">You will see a visual diagram of hello virtual network:</span></span>

    ![Azure 가상 네트워크 지점 및 사이트 간 가상 다이어그램][img-vnet-diagram]

    <span data-ttu-id="d9708-182">hello 다이어그램 0 클라이언트 연결을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-182">hello diagram shows 0 client connections.</span></span> <span data-ttu-id="d9708-183">연결 toohello 가상 네트워크를 변경한 후 hello 번호가 업데이트 된 tooone 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-183">After you make a connection toohello virtual network, hello number will be updated tooone.</span></span>

#### <a name="create-your-certificates"></a><span data-ttu-id="d9708-184">인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="d9708-184">Create your certificates</span></span>
<span data-ttu-id="d9708-185">사용 하 여 X.509 인증서는 한 가지 방법은 toocreate hello 인증서 작성 도구 (makecert.exe)와 함께 제공 되 [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-185">One way toocreate an X.509 certificate is by using hello Certificate Creation Tool (makecert.exe) that comes with [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span></span>

<span data-ttu-id="d9708-186">**toocreate 자체 서명 된 루트 인증서**</span><span class="sxs-lookup"><span data-stu-id="d9708-186">**toocreate a self-signed root certificate**</span></span>

1. <span data-ttu-id="d9708-187">워크스테이션에서 명령 프롬프트 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-187">From your workstation, open a command prompt window.</span></span>
2. <span data-ttu-id="d9708-188">Toohello Visual Studio tools 폴더로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-188">Navigate toohello Visual Studio tools folder.</span></span>
3. <span data-ttu-id="d9708-189">다음 명령을 아래의 hello 예에서 hello 및 워크스테이션에서 hello 개인 인증서 저장소에 루트 인증서를 설치 만들고 toohello Azure 클래식 포털을 나중에 업로드 합니다 해당.cer 파일을 만들 수도 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-189">hello following command in hello example below will create and install a root certificate in hello Personal certificate store on your workstation and also create a corresponding .cer file that you’ll later upload toohello Azure Classic Portal.</span></span>

        makecert -sky exchange -r -n "CN=HBaseVnetVPNRootCertificate" -pe -a sha1 -len 2048 -ss My "C:\Users\JohnDole\Desktop\HBaseVNetVPNRootCertificate.cer"

    <span data-ttu-id="d9708-190">.Cer 파일 toobe 여기서 HBaseVnetVPNRootCertificate은 hello 인증서에 대 한 toouse 되도록 hello 이름에 있는 hello 원하는 toohello 디렉터리를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-190">Change toohello directory that you want hello .cer file toobe located in, where HBaseVnetVPNRootCertificate is hello name that you want toouse for hello certificate.</span></span>

    <span data-ttu-id="d9708-191">Hello 명령 프롬프트를 닫지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="d9708-191">Don't close hello command prompt.</span></span>  <span data-ttu-id="d9708-192">Hello 다음 절차에서 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-192">You will need it in hello next procedure.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d9708-193">클라이언트 인증서가 만들어집니다 루트 인증서를 만들었으므로 tooexport이이 인증서의 개인 키와 함께 사용할 하 고 tooa 안전한 위치에 복구 될 수 있습니다 저장 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-193">Because you have created a root certificate from which client certificates will be generated, you may want tooexport this certificate along with its private key and save it tooa safe location where it may be recovered.</span></span>
   >
   >

<span data-ttu-id="d9708-194">**toocreate 클라이언트 인증서**</span><span class="sxs-lookup"><span data-stu-id="d9708-194">**toocreate a client certificate**</span></span>

* <span data-ttu-id="d9708-195">동일한 명령 프롬프트에서 hello (toobe hello에 hello 루트 인증서를 만든 동일한 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="d9708-195">From hello same command prompt (It has toobe on hello same computer where you created hello root certificate.</span></span> <span data-ttu-id="d9708-196">hello 클라이언트 인증서를 생성 해야 hello 루트 인증서에서)를 실행 hello 다음 명령을:</span><span class="sxs-lookup"><span data-stu-id="d9708-196">hello client certificate must be generated from hello root certificate), run hello following command:</span></span>

          makecert.exe -n "CN=HBaseVnetVPNClientCertificate" -pe -sky exchange -m 96 -ss My -in "HBaseVnetVPNRootCertificate" -is my -a sha1

    <span data-ttu-id="d9708-197">HBaseVnetVPNRootCertificate은 hello 루트 인증서 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-197">HBaseVnetVPNRootCertificate is hello root certificate name.</span></span>  <span data-ttu-id="d9708-198">과 toomatch hello 루트 인증서 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-198">It has toomatch hello root certificate name.</span></span>  

    <span data-ttu-id="d9708-199">Hello 루트 인증서와 hello 클라이언트 인증서는 컴퓨터에 개인 인증서 저장소에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-199">Both hello root certificate and hello client certificate are stored in your Personal certificate store on your computer.</span></span> <span data-ttu-id="d9708-200">Certmgr.msc tooverify를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-200">Use certmgr.msc tooverify.</span></span>

    ![Azure Virtual Network 지점 및 사이트 간 VPN 인증서][img-certificate]

    <span data-ttu-id="d9708-202">클라이언트 인증서 tooconnect toohello 가상 네트워크를 지정 하는 각 컴퓨터에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-202">A client certificate must be installed on each computer that you want tooconnect toohello virtual network.</span></span> <span data-ttu-id="d9708-203">인증서를 만드는 고유한 클라이언트는 각 컴퓨터에 대 한 tooconnect toohello 가상 네트워크를 지정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-203">We recommend that you create unique client certificates for each computer that you want tooconnect toohello virtual network.</span></span> <span data-ttu-id="d9708-204">tooexport hello 클라이언트 인증서 certmgr.msc를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-204">tooexport hello client certificates, use certmgr.msc.</span></span>

<span data-ttu-id="d9708-205">**tooupload hello 루트 인증서 toohello Azure 클래식 포털**</span><span class="sxs-lookup"><span data-stu-id="d9708-205">**tooupload hello root certificate toohello Azure Classic Portal**</span></span>

1. <span data-ttu-id="d9708-206">Hello Azure 클래식 포털에서에서 클릭 **네트워크** hello 왼쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-206">From hello Azure Classic Portal, click **NETWORK** on hello left.</span></span>
2. <span data-ttu-id="d9708-207">이때 HBase 클러스터에 배포 하는 hello 가상 네트워크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-207">Click hello virtual network where your HBase cluster is deployed to.</span></span>
3. <span data-ttu-id="d9708-208">클릭 **인증서** hello 위에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-208">Click **CERTIFICATES** from hello top.</span></span>
4. <span data-ttu-id="d9708-209">클릭 **업로드** hello에서 아래쪽 및 마지막 하기 전에 hello 절차에서 만든 hello 루트 인증서 파일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-209">Click **UPLOAD** from hello bottom, and specify hello root certificate file you have created in hello procedure before last.</span></span> <span data-ttu-id="d9708-210">가져온 hello 인증서를 가져올 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-210">Wait until hello certificate got imported.</span></span>
5. <span data-ttu-id="d9708-211">클릭 **대시보드** hello 위에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-211">Click **DASHBOARD** on hello top.</span></span>  <span data-ttu-id="d9708-212">hello 가상 다이어그램 hello 상태가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-212">hello virtual diagram shows hello status.</span></span>

#### <a name="configure-your-vpn-client"></a><span data-ttu-id="d9708-213">VPN 클라이언트 구성</span><span class="sxs-lookup"><span data-stu-id="d9708-213">Configure your VPN client</span></span>
<span data-ttu-id="d9708-214">**hello 클라이언트 VPN 패키지 toodownload 및 설치**</span><span class="sxs-lookup"><span data-stu-id="d9708-214">**toodownload and install hello client VPN package**</span></span>

1. <span data-ttu-id="d9708-215">Hello 빠른 보기 섹션의 hello 가상 네트워크의 hello 대시보드 페이지에서 하나를 클릭 **다운로드 hello 64 비트 클라이언트 VPN 패키지** 또는 **다운로드 hello 32 비트 클라이언트 VPN 패키지** 기반 사용자 워크스테이션 운영 체제 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-215">From hello DASHBOARD page of hello virtual network, in hello quick glance section, click either **Download hello 64-bit Client VPN Package** or **Download hello 32-bit Client VPN Package** based on your workstation OS version.</span></span>
2. <span data-ttu-id="d9708-216">클릭 **실행** tooinstall hello 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-216">Click **Run** tooinstall hello package.</span></span>
3. <span data-ttu-id="d9708-217">Hello 보안 프롬프트 클릭 **자세한 정보**, 클릭 하 고 **그래도 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-217">At hello security prompt, click **More info**, and then click **Run anyway**.</span></span>
4. <span data-ttu-id="d9708-218">**예** 를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-218">Click **Yes** twice.</span></span>

<span data-ttu-id="d9708-219">**tooconnect tooVPN**</span><span class="sxs-lookup"><span data-stu-id="d9708-219">**tooconnect tooVPN**</span></span>

1. <span data-ttu-id="d9708-220">워크스테이션의 hello 바탕 화면에서 hello 작업 표시줄에서 hello 네트워크 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-220">On hello desktop of your workstation, click hello Networks icon on hello Task bar.</span></span> <span data-ttu-id="d9708-221">가상 네트워크 이름과 함께 VPN 연결이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-221">You shall see a VPN connection with your virtual network name.</span></span>
2. <span data-ttu-id="d9708-222">Hello VPN 연결 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-222">Click hello VPN connection name.</span></span>
3. <span data-ttu-id="d9708-223">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-223">Click **Connect**.</span></span>

<span data-ttu-id="d9708-224">**tootest hello VPN 연결 및 도메인 이름 확인**</span><span class="sxs-lookup"><span data-stu-id="d9708-224">**tootest hello VPN connection and domain name resolution**</span></span>

* <span data-ttu-id="d9708-225">Hello 워크스테이션에서 명령 프롬프트를 열고 이며 hello hello HBase 클러스터의 DNS 접미사를 지정 하는 이름 다음의 하나를 ping myhbase.b7.internal.cloudapp.net:</span><span class="sxs-lookup"><span data-stu-id="d9708-225">From hello workstation, open a command prompt and ping one of hello following names given hello HBase cluster's DNS suffix is myhbase.b7.internal.cloudapp.net:</span></span>

        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        headnode0.myhbase.b7.internal.cloudapp.net
        headnode1.myhbase.b7.internal.cloudapp.net
        workernode0.myhbase.b7.internal.cloudapp.net

### <a name="install-and-configure-squirrel-on-your-workstation"></a><span data-ttu-id="d9708-226">워크스테이션에서 SQuirreL 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="d9708-226">Install and configure SQuirreL on your workstation</span></span>
<span data-ttu-id="d9708-227">**스 쿼 럴 tooinstall**</span><span class="sxs-lookup"><span data-stu-id="d9708-227">**tooinstall SQuirreL**</span></span>

1. <span data-ttu-id="d9708-228">Hello 스 쿼 럴 SQL 클라이언트 jar 파일을 다운로드 [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-228">Download hello SQuirreL SQL client jar file from [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span></span>
2. <span data-ttu-id="d9708-229">열기/실행 hello jar 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-229">Open/run hello jar file.</span></span> <span data-ttu-id="d9708-230">Hello 필요 [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-230">It requires hello [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span></span>
3. <span data-ttu-id="d9708-231">**다음** 를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-231">Click **Next** twice.</span></span>
4. <span data-ttu-id="d9708-232">Hello 쓰기 권한, 클릭 하 고 있는 경우 경로 지정 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-232">Specify a path where you have hello write permission, and then click **Next**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="d9708-233">hello 기본 설치 폴더는 hello C:\Program Files\squirrel sql 3.6 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-233">hello default installation folder is in hello C:\Program Files\squirrel-sql-3.6 folder.</span></span>  <span data-ttu-id="d9708-234">순서 toowrite toothis 경로에 hello installer hello 관리자 권한이 부여 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-234">In order toowrite toothis path, hello installer must be granted hello administrator privilege.</span></span> <span data-ttu-id="d9708-235">관리자 권한으로 명령 프롬프트를 열고 지정, tooJava의 bin 폴더 탐색을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-235">You can open a command prompt as administrator, navigate tooJava's bin folder, and then run:</span></span>
  >
  >     <span data-ttu-id="d9708-236">java.exe-jar [hello hello 스 쿼 럴 jar 파일의 경로]</span><span class="sxs-lookup"><span data-stu-id="d9708-236">java.exe -jar [hello path of hello SQuirreL jar file]</span></span>
5. <span data-ttu-id="d9708-237">클릭 **확인** tooconfirm hello 대상 디렉터리를 만드는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-237">Click **OK** tooconfirm creating hello target directory.</span></span>
6. <span data-ttu-id="d9708-238">hello 기본 설정은 tooinstall hello 기본 및 표준 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-238">hello default setting is tooinstall hello Base and Standard packages.</span></span>  <span data-ttu-id="d9708-239">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-239">Click **Next**.</span></span>
7. <span data-ttu-id="d9708-240">**다음**을 두 번 클릭한 후 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-240">Click **Next** twice, and then click **Done**.</span></span>

<span data-ttu-id="d9708-241">**tooinstall hello 피닉스 드라이버**</span><span class="sxs-lookup"><span data-stu-id="d9708-241">**tooinstall hello Phoenix driver**</span></span>

<span data-ttu-id="d9708-242">hello 피닉스 드라이버 jar 파일은 hello HBase 클러스터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-242">hello phoenix driver jar file is located on hello HBase cluster.</span></span> <span data-ttu-id="d9708-243">hello 경로 hello 버전에 따라 유사한 toohello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-243">hello path is similar toohello following based on hello versions:</span></span>

    C:\apps\dist\phoenix-4.0.0.2.1.11.0-2316\phoenix-4.0.0.2.1.11.0-2316-client.jar
<span data-ttu-id="d9708-244">Toocopy 필요한 것 hello [스 쿼 럴 설치 폴더] 아래에서 tooyour 워크스테이션 /lib 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-244">You need toocopy it tooyour workstation under hello [SQuirreL installation folder]/lib path.</span></span>  <span data-ttu-id="d9708-245">hello 가장 쉬운 방법은 hello 클러스터 변환한 다음 사용 하 여 파일 복사/붙여넣기 (CTRL + C 및 CTRL + V) toocopy tooRDP 것 tooyour 워크스테이션.</span><span class="sxs-lookup"><span data-stu-id="d9708-245">hello easiest way is tooRDP into hello cluster, and then use file copy/paste (CTRL+C and CTRL+V) toocopy it tooyour workstation.</span></span>

<span data-ttu-id="d9708-246">**tooadd 피닉스 드라이버 tooSQuirreL**</span><span class="sxs-lookup"><span data-stu-id="d9708-246">**tooadd a Phoenix driver tooSQuirreL**</span></span>

1. <span data-ttu-id="d9708-247">워크스테이션에서 SQuirreL SQL Client를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-247">Open SQuirreL SQL Client from your workstation.</span></span>
2. <span data-ttu-id="d9708-248">Hello 클릭 **드라이버** hello 왼쪽에 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-248">Click hello **Driver** tab on hello left.</span></span>
3. <span data-ttu-id="d9708-249">Hello에서 **드라이버** 메뉴를 클릭 하 여 **새 드라이버**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-249">From hello **Drivers** menu, click **New Driver**.</span></span>
4. <span data-ttu-id="d9708-250">Hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-250">Enter hello following information:</span></span>

   * <span data-ttu-id="d9708-251">**이름**: Phoenix</span><span class="sxs-lookup"><span data-stu-id="d9708-251">**Name**: Phoenix</span></span>
   * <span data-ttu-id="d9708-252">**예제 URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="d9708-252">**Example URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span></span>
   * <span data-ttu-id="d9708-253">**클래스 이름**: org.apache.phoenix.jdbc.PhoenixDriver</span><span class="sxs-lookup"><span data-stu-id="d9708-253">**Class Name**: org.apache.phoenix.jdbc.PhoenixDriver</span></span>

     > [!WARNING]
     > <span data-ttu-id="d9708-254">사용자 hello 예를 들어 URL에에서 모든 소문자로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-254">User all lower case in hello Example URL.</span></span> <span data-ttu-id="d9708-255">그 중 하나가 다운된 경우 전체 zookeeper 쿼럼을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-255">You can use they full zookeeper quorum in case one of them is down.</span></span>  <span data-ttu-id="d9708-256">hello hostnames은 zookeeper0, zookeeper1, 및 zookeeper2입니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-256">hello hostnames are zookeeper0, zookeeper1, and zookeeper2.</span></span>
     >
     >

     ![HDInsight HBase Phoenix SQuirreL 드라이버][img-squirrel-driver]
5. <span data-ttu-id="d9708-258">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-258">Click **OK**.</span></span>

<span data-ttu-id="d9708-259">**toocreate 별칭 toohello HBase 클러스터**</span><span class="sxs-lookup"><span data-stu-id="d9708-259">**toocreate an alias toohello HBase cluster**</span></span>

1. <span data-ttu-id="d9708-260">스 쿼 럴, 클릭 hello **별칭** hello 왼쪽에 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-260">From SQuirreL, Click hello **Aliases** tab on hello left.</span></span>
2. <span data-ttu-id="d9708-261">Hello에서 **별칭** 메뉴를 클릭 하 여 **새 별칭**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-261">From hello **Aliases** menu, click **New Alias**.</span></span>
3. <span data-ttu-id="d9708-262">Hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-262">Enter hello following information:</span></span>

   * <span data-ttu-id="d9708-263">**이름**: hello 이름 hello HBase 클러스터 또는 원하는 모든 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-263">**Name**: hello name of hello HBase cluster or any name you prefer.</span></span>
   * <span data-ttu-id="d9708-264">**드라이버**: Phoenix.</span><span class="sxs-lookup"><span data-stu-id="d9708-264">**Driver**: Phoenix.</span></span>  <span data-ttu-id="d9708-265">이 hello 마지막 절차에서 만든 hello 드라이버 이름은 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-265">This must match hello driver name you created in hello last procedure.</span></span>
   * <span data-ttu-id="d9708-266">**URL**: hello URL 드라이버 구성에서 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-266">**URL**: hello URL is copied from your driver configuration.</span></span> <span data-ttu-id="d9708-267">모든 소문자 toouser 있는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-267">Make sure toouser all lower case.</span></span>
   * <span data-ttu-id="d9708-268">**사용자 이름**: 모든 텍스트일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-268">**User name**: It can be any text.</span></span>  <span data-ttu-id="d9708-269">여기서 VPN 연결을 사용 하므로 hello 사용자 이름이 전혀 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-269">Because you use VPN connectivity here, hello user name is not used at all.</span></span>
   * <span data-ttu-id="d9708-270">**암호**: 모든 텍스트일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-270">**Password**: It can be any text.</span></span>

     ![HDInsight HBase Phoenix SQuirreL 드라이버][img-squirrel-alias]
4. <span data-ttu-id="d9708-272">**테스트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-272">Click **Test**.</span></span>
5. <span data-ttu-id="d9708-273">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-273">Click **Connect**.</span></span> <span data-ttu-id="d9708-274">Hello 연결 하면 스 쿼 럴이 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-274">When it makes hello connection, SQuirreL looks like:</span></span>

    ![HBase Phoenix SQuirreL][img-squirrel]

<span data-ttu-id="d9708-276">**toorun 테스트**</span><span class="sxs-lookup"><span data-stu-id="d9708-276">**toorun a test**</span></span>

1. <span data-ttu-id="d9708-277">Hello 클릭 **SQL** 바로 다음 toohello 탭 **개체** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-277">Click hello **SQL** tab right next toohello **Objects** tab.</span></span>
2. <span data-ttu-id="d9708-278">복사한 코드 다음 hello를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-278">Copy and paste hello following code:</span></span>

        CREATE TABLE IF NOT EXISTS us_population (state CHAR(2) NOT NULL, city VARCHAR NOT NULL, population BIGINT  CONSTRAINT my_pk PRIMARY KEY (state, city))
3. <span data-ttu-id="d9708-279">Hello 실행된 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-279">Click hello run button.</span></span>

    ![HBase Phoenix SQuirreL][img-squirrel-sql]
4. <span data-ttu-id="d9708-281">뒤로 toohello 전환 **개체** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-281">Switch back toohello **Objects** tab.</span></span>
5. <span data-ttu-id="d9708-282">Hello 별칭 이름을 확장 한 다음 확장 **테이블**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-282">Expand hello alias name, and then expand **TABLE**.</span></span>  <span data-ttu-id="d9708-283">Hello 새 테이블 아래에 나열 참조 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-283">You shall see hello new table listed under.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9708-284">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d9708-284">Next steps</span></span>
<span data-ttu-id="d9708-285">이 문서에서는 배웠습니다 어떻게 toouse HDInsight의 Apache 피닉스 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-285">In this article, you have learned how toouse Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="d9708-286">toolearn을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-286">toolearn more, see</span></span>

* <span data-ttu-id="d9708-287">[HDInsight HBase 개요][hdinsight-hbase-overview]: HBase는 대량의 비구조적/반구조적 데이터에 대해 임의 액세스 및 강력한 일관성을 제공하는 Hadoop 기반의 Apache 오픈 소스 NoSQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-287">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="d9708-288">[Azure 가상 네트워크에서 HBase 클러스터를 프로 비전][hdinsight-hbase-provision-vnet]: 가상 네트워크 통합 HBase 클러스터 동일한 가상 네트워크로 응용 프로그램 이므로 배포 된 toohello 수 있는 응용 프로그램이 통신할 수 HBase에 직접 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-288">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="d9708-289">[HDInsight에서 HBase 복제 구성](hdinsight-hbase-replication.md): 자세한 방법 두 Azure 데이터 센터에서 tooconfigure HBase 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-289">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how tooconfigure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="d9708-290">[HDInsight에서 HBase와 Twitter 감성 분석][hbase-twitter-sentiment]: 자세한 방법을 toodo 실시간 [감성 분석](http://en.wikipedia.org/wiki/Sentiment_analysis) HDInsight의 Hadoop 클러스터의 HBase를 사용 하 여 빅 데이터의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9708-290">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how toodo real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
