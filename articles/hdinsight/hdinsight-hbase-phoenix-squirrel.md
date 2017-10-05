---
title: "Windows 기반 Azure HDinsight에서 Apache Phoenix 및 SQuirreL 사용 | Microsoft Docs"
description: "HDInsight에서 Apache Phoenix를 사용하는 방법 및 워크스테이션에서 SQuirreL을 설치 및 구성하여 HDInsight에서 HBase 클러스터에 연결하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 024b70df99fdefa1598225ebb1fbfee85ea375d0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-apache-phoenix-and-squirrel-with-windows-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="1238c-103">HDInsight에서 Windows 기반 HBase 클러스터와 함께 Apache Phoenix 및 SQuirreL 사용</span><span class="sxs-lookup"><span data-stu-id="1238c-103">Use Apache Phoenix and SQuirreL with Windows-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="1238c-104">HDInsight에서 [Apache Phoenix](http://phoenix.apache.org/) 를 사용하는 방법 및 워크스테이션에서 SQuirrel을 설치 및 구성하여 HDInsight에서 HBase 클러스터에 연결하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-104">Learn how to use [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how to install and configure SQuirreL on your workstation to connect to an HBase cluster in HDInsight.</span></span> <span data-ttu-id="1238c-105">Phoenix에 대한 자세한 내용은 [15분 이내의 Phoenix](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1238c-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="1238c-106">Phoenix 문법은 [피닉스 문법](http://phoenix.apache.org/language/index.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1238c-106">For the Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="1238c-107">HDInsight의 Phoenix 버전 정보는 [HDInsight에서 제공하는 Hadoop 클러스터 버전의 새로운 기능](hdinsight-component-versioning.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1238c-107">For the Phoenix version information in HDInsight, see [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>

> [!IMPORTANT]
> <span data-ttu-id="1238c-108">이 문서의 단계는 Windows 기반 HDInsight 클러스터에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-108">The steps in this document only work for Windows-based HDInsight clusters.</span></span> <span data-ttu-id="1238c-109">HDInsight는 HDInsight 3.4 이하 버전의 경우 Windows에서만 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-109">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="1238c-110">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1238c-111">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1238c-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="1238c-112">Linux 기반 HDInsight에서 Phoenix 사용 방법에 대한 자세한 내용은 [HDInsight의 Linux 기반 HBase 클러스터와 함께 Apache Phoenix 사용](hdinsight-hbase-phoenix-squirrel-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1238c-112">For information on using Phoenix on Linux-based HDInsight, see [Use Apache Phoenix with Linux-based HBase clusters in HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).</span></span>
>



## <a name="use-sqlline"></a><span data-ttu-id="1238c-113">SQLLine 사용</span><span class="sxs-lookup"><span data-stu-id="1238c-113">Use SQLLine</span></span>
<span data-ttu-id="1238c-114">[SQLLine](http://sqlline.sourceforge.net/) 은 SQL을 실행하는 명령줄 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-114">[SQLLine](http://sqlline.sourceforge.net/) is a command line utility to execute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="1238c-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1238c-115">Prerequisites</span></span>
<span data-ttu-id="1238c-116">SQLLine을 시작하려면 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-116">Before you can use SQLLine, you must have the following:</span></span>

* <span data-ttu-id="1238c-117">**HDInsight의 HBase 클러스터**.</span><span class="sxs-lookup"><span data-stu-id="1238c-117">**A HBase cluster in HDInsight**.</span></span> <span data-ttu-id="1238c-118">HBase 클러스터 프로비전에 대한 자세한 내용은 [HDInsight에서 Apache HBase 시작][hdinsight-hbase-get-started]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1238c-118">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="1238c-119">**원격 데스크톱 프로토콜을 통해 HBase 클러스터에 연결**.</span><span class="sxs-lookup"><span data-stu-id="1238c-119">**Connect to the HBase cluster via the remote desktop protocol**.</span></span> <span data-ttu-id="1238c-120">자세한 내용은 [Azure 클래식 포털을 사용하여 HDInsight의 Hadoop 클러스터 관리][hdinsight-manage-portal]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1238c-120">For instructions, see [Manage Hadoop clusters in HDInsight by using the Azure Classic Portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="1238c-121">**호스트 이름을 확인하려면**</span><span class="sxs-lookup"><span data-stu-id="1238c-121">**To find out the host name**</span></span>

1. <span data-ttu-id="1238c-122">데스크톱에서 **Hadoop 명령줄** 을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-122">Open **Hadoop Command Line** from the desktop.</span></span>
2. <span data-ttu-id="1238c-123">다음 명령을 실행하여 DNS 접미사를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-123">Run the following command to get the DNS suffix:</span></span>

        ipconfig

    <span data-ttu-id="1238c-124">**연결별 DNS 접미사**를 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-124">Write down **Connection-specific DNS Suffix**.</span></span> <span data-ttu-id="1238c-125">예를 들면 *myhbasecluster.f5.internal.cloudapp.net*과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-125">For example, *myhbasecluster.f5.internal.cloudapp.net*.</span></span> <span data-ttu-id="1238c-126">HBase 클러스터에 연결할 때 FQDN을 사용하여 Zookeeper 중 하나에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-126">When you connect to an HBase cluster, you will need to connect to one of the Zookeepers using FQDN.</span></span> <span data-ttu-id="1238c-127">각 HDInsight 클러스터에는 3개의 Zookeeper,</span><span class="sxs-lookup"><span data-stu-id="1238c-127">Each HDInsight cluster has 3 Zookeepers.</span></span> <span data-ttu-id="1238c-128">*zookeeper0*, *zookeeper1* 및 *zookeeper2*가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-128">They are *zookeeper0*, *zookeeper1*, and *zookeeper2*.</span></span> <span data-ttu-id="1238c-129">FQDN은 *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-129">The FQDN will be something like *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span></span>

<span data-ttu-id="1238c-130">**SQLLine을 사용하려면**</span><span class="sxs-lookup"><span data-stu-id="1238c-130">**To use SQLLine**</span></span>

1. <span data-ttu-id="1238c-131">데스크톱에서 **Hadoop 명령줄** 을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-131">Open **Hadoop Command Line** from the desktop.</span></span>
2. <span data-ttu-id="1238c-132">다음 명령을 실행하여 SQLLine을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-132">Run the following commands to open SQLLine:</span></span>

        cd %phoenix_home%\bin
        sqlline.py [The FQDN of one of the Zookeepers]

    ![HDInsight hbase phoenix sqlline][hdinsight-hbase-phoenix-sqlline]

    <span data-ttu-id="1238c-134">이 샘플에 사용되는 명령:</span><span class="sxs-lookup"><span data-stu-id="1238c-134">The commands used in the sample:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

<span data-ttu-id="1238c-135">자세한 내용은 [SQLLine 설명서](http://sqlline.sourceforge.net/#manual) 및 [Phoenix 문법](http://phoenix.apache.org/language/index.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1238c-135">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="use-squirrel"></a><span data-ttu-id="1238c-136">SQuirrel 사용</span><span class="sxs-lookup"><span data-stu-id="1238c-136">Use SQuirreL</span></span>
<span data-ttu-id="1238c-137">[SQuirreL SQL Client](http://squirrel-sql.sourceforge.net/)는 JDBC 호환 데이터베이스를 보고, 테이블에서 데이터를 찾고, SQL 명령을 실행할 수 있는 그래픽 Java 프로그램입니다. HDInsight에서 Apache 피닉스에 연결하는데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-137">[SQuirreL SQL Client](http://squirrel-sql.sourceforge.net/) is a graphical Java program that will allow you to view the structure of a JDBC compliant database, browse the data in tables, issue SQL commands etc. It can be used to connect to Apache Phoenix on HDInsight.</span></span>

<span data-ttu-id="1238c-138">이 섹션에서는 워크스테이션에서 SQuirreL을 설치 및 구성하여 HDInsight에서 VPN을 통해 HBase 클러스터에 연결하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-138">This section shows you how to install and configure SQuirreL on your workstation to connect to an HBase cluster in HDInsight via VPN.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="1238c-139">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1238c-139">Prerequisites</span></span>
<span data-ttu-id="1238c-140">다음 절차를 수행하기 전에 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-140">Before following the procedures, you must have the following:</span></span>

* <span data-ttu-id="1238c-141">DNS 가상 컴퓨터를 사용하여 Azure 가상 네트워크에 배포한 HBase 클러스터.</span><span class="sxs-lookup"><span data-stu-id="1238c-141">An HBase cluster deployed to an Azure virtual network with a DNS virtual machine.</span></span>  <span data-ttu-id="1238c-142">자세한 내용은 [Azure Virtual Network에 HBase 클러스터 만들기][hdinsight-hbase-provision-vnet]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1238c-142">For instructions, see [Create HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet].</span></span>

* <span data-ttu-id="1238c-143">HBase 클러스터 연결별 DNS 접미사를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-143">Get the HBase cluster cluster Connection-specific DNS suffix.</span></span> <span data-ttu-id="1238c-144">이렇게 하려면 클러스터에 RDP를 연결하고 IPConfig를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-144">To get it, RDP into the cluster, and then run IPConfig.</span></span>  <span data-ttu-id="1238c-145">DNS 접미사는 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-145">The DNS suffix is similar to:</span></span>

        myhbase.b7.internal.cloudapp.net
* <span data-ttu-id="1238c-146">워크스테이션에서 [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx)을 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-146">Download and install [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) on your workstation.</span></span> <span data-ttu-id="1238c-147">인증서를 만들려면 패키지의 makecert가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-147">You will need makecert from the package to create your certificate.</span></span>  
* <span data-ttu-id="1238c-148">워크스테이션에서 [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) 을 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-148">Download and install [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) on your workstation.</span></span>  <span data-ttu-id="1238c-149">SQuirreL SQL Client 버전 3.0 이상에는 JRE 버전 1.6 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-149">SQuirreL SQL client version 3.0 and higher requires JRE version 1.6 or higher.</span></span>  

### <a name="configure-a-point-to-site-vpn-connection-to-the-azure-virtual-network"></a><span data-ttu-id="1238c-150">Azure 가상 네트워크에 대한 지점 및 사이트 간 VPN 연결 구성</span><span class="sxs-lookup"><span data-stu-id="1238c-150">Configure a Point-to-Site VPN connection to the Azure virtual network</span></span>
<span data-ttu-id="1238c-151">지점 및 사이트 간 VPN 연결을 구성하는 단계는 3단계로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-151">There are 3 steps involved configuring a point-to-site VPN connection:</span></span>

1. [<span data-ttu-id="1238c-152">가상 네트워크 및 동적 라우팅 게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="1238c-152">Configure a virtual network and a dynamic routing gateway</span></span>](#Configure-a-virtual-network-and-a-dynamic-routing-gateway)
2. [<span data-ttu-id="1238c-153">인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="1238c-153">Create your certificates</span></span>](#Create-your-certificates)
3. [<span data-ttu-id="1238c-154">VPN 클라이언트 구성</span><span class="sxs-lookup"><span data-stu-id="1238c-154">Configure your VPN client</span></span>](#Configure-your-VPN-client)

<span data-ttu-id="1238c-155">자세한 내용은 [Azure 가상 네트워크에 대한 지점 및 사이트 간 VPN 연결 구성](../vpn-gateway/vpn-gateway-point-to-site-create.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1238c-155">See [Configure a Point-to-Site VPN connection to an Azure Virtual Network](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>

#### <a name="configure-a-virtual-network-and-a-dynamic-routing-gateway"></a><span data-ttu-id="1238c-156">가상 네트워크 및 동적 라우팅 게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="1238c-156">Configure a virtual network and a dynamic routing gateway</span></span>
<span data-ttu-id="1238c-157">Azure 가상 네트워크에서 HBase 클러스터를 프로비전했는지 확인합니다(이 섹션의 필수 조건 참조).</span><span class="sxs-lookup"><span data-stu-id="1238c-157">Assure you have provisioned an HBase cluster in an Azure virtual network (see the prerequisites for this section).</span></span> <span data-ttu-id="1238c-158">다음 단계에서는 지점 및 사이트 간 연결을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-158">The next step is to configure a point-to-site connection.</span></span>

<span data-ttu-id="1238c-159">**지점 및 사이트 간 연결을 구성하려면**</span><span class="sxs-lookup"><span data-stu-id="1238c-159">**To configure the point-to-site connectivity**</span></span>

1. <span data-ttu-id="1238c-160">[Azure 클래식 포털][azure-portal]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-160">Sign in to the [Azure Classic Portal][azure-portal].</span></span>
2. <span data-ttu-id="1238c-161">왼쪽에서 **네트워크**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-161">On the left, click **NETWORKS**.</span></span>
3. <span data-ttu-id="1238c-162">만든 Virtual Network를 클릭합니다([Azure Virtual Network에 HBase 클러스터 프로비전][hdinsight-hbase-provision-vnet] 참조).</span><span class="sxs-lookup"><span data-stu-id="1238c-162">Click the virtual network you have created (see [Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]).</span></span>
4. <span data-ttu-id="1238c-163">위쪽에서 **구성** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-163">Click **CONFIGURE** from the top.</span></span>
5. <span data-ttu-id="1238c-164">**지점 및 사이트 간 연결** 섹션에서 **지점 및 사이트 간 연결 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-164">In the **point-to-site connectivity** section, select **Configure point-to-site connectivity**.</span></span>
6. <span data-ttu-id="1238c-165">**시작 IP** 및 **CIDR**을 구성하여 연결된 경우 VPN 클라이언트에서 IP 주소를 받을 IP 주소 범위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-165">Configure **STARTING IP** and **CIDR** to specify the IP address range from which your VPN clients will receive an IP address when connected.</span></span> <span data-ttu-id="1238c-166">범위는 온-프레미스 네트워크 및 연결할 Azure 가상 네트워크에 있는 범위와 겹칠 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-166">The range cannot overlap with any of the ranges located on your on-premises network and the Azure virtual network you will be connecting to.</span></span> <span data-ttu-id="1238c-167">예를 들어 모바일 서비스는 스크립트 실행 간에 상태를 유지하지 않으므로 스크립트 실행 간에 지속되어야 하는 모든 데이터를 테이블에 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-167">For example.</span></span> <span data-ttu-id="1238c-168">가상 네트워크에 대해 10.0.0.0/20을 선택한 경우 클라이언트 주소 공간은 10.1.0.0/24를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-168">if you selected 10.0.0.0/20 for the virtual network, you can select 10.1.0.0/24 for the client address space.</span></span> <span data-ttu-id="1238c-169">자세한 내용은 [지점 및 사이트 간 연결][vnet-point-to-site-connectivity] 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1238c-169">See the [Point-To-Site Connectivity][vnet-point-to-site-connectivity] page for more information.</span></span>
7. <span data-ttu-id="1238c-170">가상 네트워크 주소 공간 섹션에서 **게이트웨이 서브넷 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-170">In the virtual network address spaces section, click **add gateway subnet**.</span></span>
8. <span data-ttu-id="1238c-171">페이지 아래쪽에서 **저장** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-171">Click **SAVE** on the bottom of the page.</span></span>
9. <span data-ttu-id="1238c-172">**예** 를 클릭하여 변경 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-172">Click **YES** to confirm the change.</span></span> <span data-ttu-id="1238c-173">시스템에서 변경을 완료할 때까지 기다린 후 다음 절차를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-173">Wait until the system has finished making the change before you proceed to the next procedure.</span></span>

<span data-ttu-id="1238c-174">**동적 라우팅 게이트웨이를 만들려면**</span><span class="sxs-lookup"><span data-stu-id="1238c-174">**To create a dynamic routing gateway**</span></span>

1. <span data-ttu-id="1238c-175">Azure 클래식 포털의 페이지 위쪽에서 **대시보드** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-175">From the Azure Classic Portal, click **DASHBOARD** from the top of the page.</span></span>
2. <span data-ttu-id="1238c-176">페이지 아래쪽에서 **게이트웨이 만들기** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-176">Click **CREATE GATEWAY** from the bottom of the page.</span></span>
3. <span data-ttu-id="1238c-177">**예** 를 클릭하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-177">Click **YES** to confirm.</span></span> <span data-ttu-id="1238c-178">게이트웨이가 만들어질 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-178">Wait until the gateway is created.</span></span>
4. <span data-ttu-id="1238c-179">위쪽에서 **대시보드** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-179">Click **DASHBOARD** from the top.</span></span>  <span data-ttu-id="1238c-180">가상 네트워크에 대한 시각적 다이어그램이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-180">You will see a visual diagram of the virtual network:</span></span>

    ![Azure 가상 네트워크 지점 및 사이트 간 가상 다이어그램][img-vnet-diagram]

    <span data-ttu-id="1238c-182">다이어그램에 클라이언트 연결이 0개인 것으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-182">The diagram shows 0 client connections.</span></span> <span data-ttu-id="1238c-183">가상 네트워크에 연결하면 이 숫자가 1로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-183">After you make a connection to the virtual network, the number will be updated to one.</span></span>

#### <a name="create-your-certificates"></a><span data-ttu-id="1238c-184">인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="1238c-184">Create your certificates</span></span>
<span data-ttu-id="1238c-185">X.509 인증서를 만드는 한 가지 방법은 [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx)과 함께 제공되는 인증서 만들기 도구(makecert.exe)를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-185">One way to create an X.509 certificate is by using the Certificate Creation Tool (makecert.exe) that comes with [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span></span>

<span data-ttu-id="1238c-186">**자체 서명된 루트 인증서를 만들려면**</span><span class="sxs-lookup"><span data-stu-id="1238c-186">**To create a self-signed root certificate**</span></span>

1. <span data-ttu-id="1238c-187">워크스테이션에서 명령 프롬프트 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-187">From your workstation, open a command prompt window.</span></span>
2. <span data-ttu-id="1238c-188">Visual Studio Tools 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-188">Navigate to the Visual Studio tools folder.</span></span>
3. <span data-ttu-id="1238c-189">아래 예제의 다음 명령은 워크스테이션의 개인 인증서 저장소에 루트 인증서를 만들고 설치하며, 나중에 Azure 클래식 포털에 업로드할 해당.cer 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-189">The following command in the example below will create and install a root certificate in the Personal certificate store on your workstation and also create a corresponding .cer file that you’ll later upload to the Azure Classic Portal.</span></span>

        makecert -sky exchange -r -n "CN=HBaseVnetVPNRootCertificate" -pe -a sha1 -len 2048 -ss My "C:\Users\JohnDole\Desktop\HBaseVNetVPNRootCertificate.cer"

    <span data-ttu-id="1238c-190">.cer 파일을 저장할 디렉터리로 변경합니다. 여기서 HBaseVnetVPNRootCertificate는 인증서에 사용할 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-190">Change to the directory that you want the .cer file to be located in, where HBaseVnetVPNRootCertificate is the name that you want to use for the certificate.</span></span>

    <span data-ttu-id="1238c-191">명령 프롬프트를 닫지 마세요.</span><span class="sxs-lookup"><span data-stu-id="1238c-191">Don't close the command prompt.</span></span>  <span data-ttu-id="1238c-192">다음 절차에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-192">You will need it in the next procedure.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1238c-193">클라이언트 인증서를 생성할 루트 인증서를 만들었기 때문에 이 인증서를 해당 개인 키와 함께 내보내고 복구 가능한 안전한 위치에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-193">Because you have created a root certificate from which client certificates will be generated, you may want to export this certificate along with its private key and save it to a safe location where it may be recovered.</span></span>
   >
   >

<span data-ttu-id="1238c-194">**클라이언트 인증서를 만들려면**</span><span class="sxs-lookup"><span data-stu-id="1238c-194">**To create a client certificate**</span></span>

* <span data-ttu-id="1238c-195">동일한 명령 프롬프트(루트 인증서를 만든 것과 동일한 컴퓨터에 있어야 하며,</span><span class="sxs-lookup"><span data-stu-id="1238c-195">From the same command prompt (It has to be on the same computer where you created the root certificate.</span></span> <span data-ttu-id="1238c-196">루트 인증서에서 클라이언트 인증서를 생성해야 함)에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-196">The client certificate must be generated from the root certificate), run the following command:</span></span>

          makecert.exe -n "CN=HBaseVnetVPNClientCertificate" -pe -sky exchange -m 96 -ss My -in "HBaseVnetVPNRootCertificate" -is my -a sha1

    <span data-ttu-id="1238c-197">HBaseVnetVPNRootCertificate는 루트 인증서 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-197">HBaseVnetVPNRootCertificate is the root certificate name.</span></span>  <span data-ttu-id="1238c-198">루트 인증서 이름과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-198">It has to match the root certificate name.</span></span>  

    <span data-ttu-id="1238c-199">루트 인증서 및 클라이언트 인증서는 컴퓨터의 개인 인증서 저장소에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-199">Both the root certificate and the client certificate are stored in your Personal certificate store on your computer.</span></span> <span data-ttu-id="1238c-200">Certmgr.msc를 사용하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-200">Use certmgr.msc to verify.</span></span>

    ![Azure Virtual Network 지점 및 사이트 간 VPN 인증서][img-certificate]

    <span data-ttu-id="1238c-202">클라이언트 인증서는 가상 네트워크에 연결하려는 각 컴퓨터에 설치되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-202">A client certificate must be installed on each computer that you want to connect to the virtual network.</span></span> <span data-ttu-id="1238c-203">가상 네트워크에 연결 하려는 각 컴퓨터에 대해 고유한 클라이언트 인증서를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-203">We recommend that you create unique client certificates for each computer that you want to connect to the virtual network.</span></span> <span data-ttu-id="1238c-204">클라이언트 인증서를 내보내려면 certmgr.msc를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-204">To export the client certificates, use certmgr.msc.</span></span>

<span data-ttu-id="1238c-205">**Azure 클래식 포털에 루트 인증서를 업로드하려면**</span><span class="sxs-lookup"><span data-stu-id="1238c-205">**To upload the root certificate to the Azure Classic Portal**</span></span>

1. <span data-ttu-id="1238c-206">Azure 클래식 포털의 왼쪽에서 **네트워크** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-206">From the Azure Classic Portal, click **NETWORK** on the left.</span></span>
2. <span data-ttu-id="1238c-207">HBase 클러스터가 배포된 가상 네트워크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-207">Click the virtual network where your HBase cluster is deployed to.</span></span>
3. <span data-ttu-id="1238c-208">위쪽에서 **인증서** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-208">Click **CERTIFICATES** from the top.</span></span>
4. <span data-ttu-id="1238c-209">아래쪽에서 **업로드** 를 클릭하고 마지막 이전 절차에서 만든 루트 인증서 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-209">Click **UPLOAD** from the bottom, and specify the root certificate file you have created in the procedure before last.</span></span> <span data-ttu-id="1238c-210">인증서를 가져올 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-210">Wait until the certificate got imported.</span></span>
5. <span data-ttu-id="1238c-211">위쪽에서 **대시보드** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-211">Click **DASHBOARD** on the top.</span></span>  <span data-ttu-id="1238c-212">가상 다이어그램에 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-212">The virtual diagram shows the status.</span></span>

#### <a name="configure-your-vpn-client"></a><span data-ttu-id="1238c-213">VPN 클라이언트 구성</span><span class="sxs-lookup"><span data-stu-id="1238c-213">Configure your VPN client</span></span>
<span data-ttu-id="1238c-214">**클라이언트 VPN 패키지를 다운로드하여 설치하려면**</span><span class="sxs-lookup"><span data-stu-id="1238c-214">**To download and install the client VPN package**</span></span>

1. <span data-ttu-id="1238c-215">가상 네트워크의 대시보드 페이지에 있는 간략 상태 섹션에서 워크스테이션 OS 버전에 따라 **64비트 클라이언트 VPN 패키지 다운로드** 또는 **32비트 클라이언트 VPN 패키지 다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-215">From the DASHBOARD page of the virtual network, in the quick glance section, click either **Download the 64-bit Client VPN Package** or **Download the 32-bit Client VPN Package** based on your workstation OS version.</span></span>
2. <span data-ttu-id="1238c-216">**실행** 을 클릭하여 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-216">Click **Run** to install the package.</span></span>
3. <span data-ttu-id="1238c-217">보안 프롬프트에서 **추가 정보**를 클릭한 다음 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-217">At the security prompt, click **More info**, and then click **Run anyway**.</span></span>
4. <span data-ttu-id="1238c-218">**예** 를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-218">Click **Yes** twice.</span></span>

<span data-ttu-id="1238c-219">**VPN에 연결**</span><span class="sxs-lookup"><span data-stu-id="1238c-219">**To connect to VPN**</span></span>

1. <span data-ttu-id="1238c-220">워크스테이션의 바탕 화면에서 작업 표시줄에 있는 네트워크 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-220">On the desktop of your workstation, click the Networks icon on the Task bar.</span></span> <span data-ttu-id="1238c-221">가상 네트워크 이름과 함께 VPN 연결이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-221">You shall see a VPN connection with your virtual network name.</span></span>
2. <span data-ttu-id="1238c-222">VPN 연결 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-222">Click the VPN connection name.</span></span>
3. <span data-ttu-id="1238c-223">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-223">Click **Connect**.</span></span>

<span data-ttu-id="1238c-224">**VPN 연결 및 도메인 이름 확인을 테스트하려면**</span><span class="sxs-lookup"><span data-stu-id="1238c-224">**To test the VPN connection and domain name resolution**</span></span>

* <span data-ttu-id="1238c-225">워크스테이션에서 명령 프롬프트를 열고 다음 이름 중 하나를 ping합니다(HBase 클러스터의 DNS 접미사는 myhbase.b7.internal.cloudapp.net).</span><span class="sxs-lookup"><span data-stu-id="1238c-225">From the workstation, open a command prompt and ping one of the following names given the HBase cluster's DNS suffix is myhbase.b7.internal.cloudapp.net:</span></span>

        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        headnode0.myhbase.b7.internal.cloudapp.net
        headnode1.myhbase.b7.internal.cloudapp.net
        workernode0.myhbase.b7.internal.cloudapp.net

### <a name="install-and-configure-squirrel-on-your-workstation"></a><span data-ttu-id="1238c-226">워크스테이션에서 SQuirreL 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="1238c-226">Install and configure SQuirreL on your workstation</span></span>
<span data-ttu-id="1238c-227">**SQuirreL을 설치하려면**</span><span class="sxs-lookup"><span data-stu-id="1238c-227">**To install SQuirreL**</span></span>

1. <span data-ttu-id="1238c-228">[http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation)에서 SQuirreL SQL Client jar 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-228">Download the SQuirreL SQL client jar file from [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span></span>
2. <span data-ttu-id="1238c-229">jar 파일을 엽니다/실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-229">Open/run the jar file.</span></span> <span data-ttu-id="1238c-230">[Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html)가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-230">It requires the [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span></span>
3. <span data-ttu-id="1238c-231">**다음** 를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-231">Click **Next** twice.</span></span>
4. <span data-ttu-id="1238c-232">쓰기 권한이 있는 경로를 지정하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-232">Specify a path where you have the write permission, and then click **Next**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="1238c-233">기본 설치 폴더는 C:\Program Files\squirrel-sql-3.6 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-233">The default installation folder is in the C:\Program Files\squirrel-sql-3.6 folder.</span></span>  <span data-ttu-id="1238c-234">이 경로에 쓰려면 설치 관리자에 관리자 권한이 부여되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-234">In order to write to this path, the installer must be granted the administrator privilege.</span></span> <span data-ttu-id="1238c-235">관리자 권한으로 명령 프롬프트를 열고 Java의 bin 폴더로 이동한 후 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-235">You can open a command prompt as administrator, navigate to Java's bin folder, and then run:</span></span>
  >
  >     <span data-ttu-id="1238c-236">java.exe -jar[SQuirreL jar 파일 경로]</span><span class="sxs-lookup"><span data-stu-id="1238c-236">java.exe -jar [the path of the SQuirreL jar file]</span></span>
5. <span data-ttu-id="1238c-237">**확인** 을 클릭하여 대상 디렉터리 만들기를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-237">Click **OK** to confirm creating the target directory.</span></span>
6. <span data-ttu-id="1238c-238">기본 설정은 기본 및 표준 패키지를 설치하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-238">The default setting is to install the Base and Standard packages.</span></span>  <span data-ttu-id="1238c-239">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-239">Click **Next**.</span></span>
7. <span data-ttu-id="1238c-240">**다음**을 두 번 클릭한 후 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-240">Click **Next** twice, and then click **Done**.</span></span>

<span data-ttu-id="1238c-241">**Phoenix 드라이버를 설치하려면**</span><span class="sxs-lookup"><span data-stu-id="1238c-241">**To install the Phoenix driver**</span></span>

<span data-ttu-id="1238c-242">Phoenix 드라이버 jar 파일은 HBase 클러스터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-242">The phoenix driver jar file is located on the HBase cluster.</span></span> <span data-ttu-id="1238c-243">경로는 버전에 따라 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-243">The path is similar to the following based on the versions:</span></span>

    C:\apps\dist\phoenix-4.0.0.2.1.11.0-2316\phoenix-4.0.0.2.1.11.0-2316-client.jar
<span data-ttu-id="1238c-244">워크스테이션의 [SQuirrel 설치 폴더]/lib 경로 아래에 복사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-244">You need to copy it to your workstation under the [SQuirreL installation folder]/lib path.</span></span>  <span data-ttu-id="1238c-245">가장 쉬운 방법은 RDP를 통해 클러스터에 연결한 후 파일 복사/붙여넣기(Ctrl+C 및 Ctrl+V)를 사용하여 워크스테이션에 복사하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-245">The easiest way is to RDP into the cluster, and then use file copy/paste (CTRL+C and CTRL+V) to copy it to your workstation.</span></span>

<span data-ttu-id="1238c-246">**SQuirreL에 Phoenix 드라이버를 추가하려면**</span><span class="sxs-lookup"><span data-stu-id="1238c-246">**To add a Phoenix driver to SQuirreL**</span></span>

1. <span data-ttu-id="1238c-247">워크스테이션에서 SQuirreL SQL Client를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-247">Open SQuirreL SQL Client from your workstation.</span></span>
2. <span data-ttu-id="1238c-248">왼쪽에서 **드라이버** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-248">Click the **Driver** tab on the left.</span></span>
3. <span data-ttu-id="1238c-249">**드라이버** 메뉴에서 **새 드라이버**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-249">From the **Drivers** menu, click **New Driver**.</span></span>
4. <span data-ttu-id="1238c-250">다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-250">Enter the following information:</span></span>

   * <span data-ttu-id="1238c-251">**이름**: Phoenix</span><span class="sxs-lookup"><span data-stu-id="1238c-251">**Name**: Phoenix</span></span>
   * <span data-ttu-id="1238c-252">**예제 URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="1238c-252">**Example URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span></span>
   * <span data-ttu-id="1238c-253">**클래스 이름**: org.apache.phoenix.jdbc.PhoenixDriver</span><span class="sxs-lookup"><span data-stu-id="1238c-253">**Class Name**: org.apache.phoenix.jdbc.PhoenixDriver</span></span>

     > [!WARNING]
     > <span data-ttu-id="1238c-254">예제 URL에는 모두 소문자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-254">User all lower case in the Example URL.</span></span> <span data-ttu-id="1238c-255">그 중 하나가 다운된 경우 전체 zookeeper 쿼럼을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-255">You can use they full zookeeper quorum in case one of them is down.</span></span>  <span data-ttu-id="1238c-256">호스트 이름은 zookeeper0, zookeeper1 및 zookeeper2입니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-256">The hostnames are zookeeper0, zookeeper1, and zookeeper2.</span></span>
     >
     >

     ![HDInsight HBase Phoenix SQuirreL 드라이버][img-squirrel-driver]
5. <span data-ttu-id="1238c-258">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-258">Click **OK**.</span></span>

<span data-ttu-id="1238c-259">**HBase 클러스터에 대한 별칭을 만들려면**</span><span class="sxs-lookup"><span data-stu-id="1238c-259">**To create an alias to the HBase cluster**</span></span>

1. <span data-ttu-id="1238c-260">SQuirreL에서 왼쪽의 **별칭** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-260">From SQuirreL, Click the **Aliases** tab on the left.</span></span>
2. <span data-ttu-id="1238c-261">**별칭** 메뉴에서 **새 별칭**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-261">From the **Aliases** menu, click **New Alias**.</span></span>
3. <span data-ttu-id="1238c-262">다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-262">Enter the following information:</span></span>

   * <span data-ttu-id="1238c-263">**이름**: HBase 클러스터의 이름 또는 사용자가 원하는 이름</span><span class="sxs-lookup"><span data-stu-id="1238c-263">**Name**: The name of the HBase cluster or any name you prefer.</span></span>
   * <span data-ttu-id="1238c-264">**드라이버**: Phoenix.</span><span class="sxs-lookup"><span data-stu-id="1238c-264">**Driver**: Phoenix.</span></span>  <span data-ttu-id="1238c-265">마지막 절차에서 만든 드라이버 이름과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-265">This must match the driver name you created in the last procedure.</span></span>
   * <span data-ttu-id="1238c-266">**URL**: 드라이버 구성에서 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-266">**URL**: The URL is copied from your driver configuration.</span></span> <span data-ttu-id="1238c-267">모두 소문자를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-267">Make sure to user all lower case.</span></span>
   * <span data-ttu-id="1238c-268">**사용자 이름**: 모든 텍스트일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-268">**User name**: It can be any text.</span></span>  <span data-ttu-id="1238c-269">여기 VPN 연결을 사용하기 때문에 사용자 이름은 전혀 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-269">Because you use VPN connectivity here, the user name is not used at all.</span></span>
   * <span data-ttu-id="1238c-270">**암호**: 모든 텍스트일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-270">**Password**: It can be any text.</span></span>

     ![HDInsight HBase Phoenix SQuirreL 드라이버][img-squirrel-alias]
4. <span data-ttu-id="1238c-272">**테스트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-272">Click **Test**.</span></span>
5. <span data-ttu-id="1238c-273">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-273">Click **Connect**.</span></span> <span data-ttu-id="1238c-274">연결된 경우 SQuirreL은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-274">When it makes the connection, SQuirreL looks like:</span></span>

    ![HBase Phoenix SQuirreL][img-squirrel]

<span data-ttu-id="1238c-276">**테스트를 실행하려면**</span><span class="sxs-lookup"><span data-stu-id="1238c-276">**To run a test**</span></span>

1. <span data-ttu-id="1238c-277">**개체** 탭 오른쪽에 있는 **SQL** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-277">Click the **SQL** tab right next to the **Objects** tab.</span></span>
2. <span data-ttu-id="1238c-278">다음 코드를 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-278">Copy and paste the following code:</span></span>

        CREATE TABLE IF NOT EXISTS us_population (state CHAR(2) NOT NULL, city VARCHAR NOT NULL, population BIGINT  CONSTRAINT my_pk PRIMARY KEY (state, city))
3. <span data-ttu-id="1238c-279">실행 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-279">Click the run button.</span></span>

    ![HBase Phoenix SQuirreL][img-squirrel-sql]
4. <span data-ttu-id="1238c-281">**개체** 탭으로 다시 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-281">Switch back to the **Objects** tab.</span></span>
5. <span data-ttu-id="1238c-282">별칭 이름을 확장한 다음 **테이블**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-282">Expand the alias name, and then expand **TABLE**.</span></span>  <span data-ttu-id="1238c-283">새 테이블이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-283">You shall see the new table listed under.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1238c-284">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1238c-284">Next steps</span></span>
<span data-ttu-id="1238c-285">이 문서에서는 HDInsight에서 Apache Phoenix를 사용하는 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-285">In this article, you have learned how to use Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="1238c-286">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1238c-286">To learn more, see</span></span>

* <span data-ttu-id="1238c-287">[HDInsight HBase 개요][hdinsight-hbase-overview]: HBase는 대량의 비구조적/반구조적 데이터에 대해 임의 액세스 및 강력한 일관성을 제공하는 Hadoop 기반의 Apache 오픈 소스 NoSQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-287">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="1238c-288">[Azure Virtual Network에서 HBase 클러스터 프로비전][hdinsight-hbase-provision-vnet]: Virtual Network 통합을 사용하면 응용 프로그램이 HBase와 직접 통신할 수 있도록 응용 프로그램과 동일한 Virtual Network에 HBase 클러스터를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-288">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="1238c-289">[HDInsight에서 HBase 복제 구성](hdinsight-hbase-replication.md): 두 Azure 데이터 센터에서 HBase 복제를 구성하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-289">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how to configure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="1238c-290">[HDInsight에서 HBase를 사용하여 Twitter 감정][hbase-twitter-sentiment]: HDInsight의 Hadoop 클러스터에서 HBase를 사용하여 빅 데이터에 대한 실시간 [감정 분석](http://en.wikipedia.org/wiki/Sentiment_analysis)을 수행하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1238c-290">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how to do real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

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
