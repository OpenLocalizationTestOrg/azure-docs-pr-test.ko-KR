---
title: "Azure HDInsight-hello JDBC 드라이버를 통해 Hive aaaQuery | Microsoft Docs"
description: "HDInsight의 Java 응용 프로그램 toosubmit 하이브 쿼리 tooHadoop에서 hello JDBC 드라이버를 사용 합니다. 프로그래밍 방식으로 및 hello 스 쿼 럴 SQL client에서 연결 합니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 928f8d2a-684d-48cb-894c-11c59a5599ae
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 93178da3b8d497faa4c788e91dba89c4e45d3fff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="query-hive-through-hello-jdbc-driver-in-hdinsight"></a><span data-ttu-id="b7a07-104">HDInsight의 hello JDBC 드라이버를 통해 하이브 쿼리</span><span class="sxs-lookup"><span data-stu-id="b7a07-104">Query Hive through hello JDBC driver in HDInsight</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="b7a07-105">Toouse hello JDBC 드라이버는 Java 응용 프로그램 toosubmit 하이브에서에서 Azure HDInsight의 tooHadoop를 쿼리 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-105">Learn how toouse hello JDBC driver from a Java application toosubmit Hive queries tooHadoop in Azure HDInsight.</span></span> <span data-ttu-id="b7a07-106">이 문서에서 hello 정보를 보여 줍니다 방법을 tooconnect 프로그래밍 방식으로 고 hello 스 쿼 럴 SQL 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-106">hello information in this document demonstrates how tooconnect programmatically and from hello SQuirrel SQL client.</span></span>

<span data-ttu-id="b7a07-107">Hello 하이브 JDBC 인터페이스에 대 한 자세한 내용은 참조 하십시오. [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface)합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-107">For more information on hello Hive JDBC Interface, see [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7a07-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b7a07-108">Prerequisites</span></span>

* <span data-ttu-id="b7a07-109">HDInsight 클러스터의 Hadoop.</span><span class="sxs-lookup"><span data-stu-id="b7a07-109">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="b7a07-110">Linux 또는 Windows 기반의 클러스터가 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-110">Either Linux-based or Windows-based clusters work.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="b7a07-111">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b7a07-112">자세한 내용은 [HDInsight 3.3 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b7a07-112">For more information, see [HDInsight 3.3 retirement](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="b7a07-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span><span class="sxs-lookup"><span data-stu-id="b7a07-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span></span> <span data-ttu-id="b7a07-114">SQuirreL은 JDBC 클라이언트 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-114">SQuirreL is a JDBC client application.</span></span>

* <span data-ttu-id="b7a07-115">hello [개발자 키트 JDK (Java) 버전 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) 이상.</span><span class="sxs-lookup"><span data-stu-id="b7a07-115">hello [Java Developer Kit (JDK) version 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span>

* <span data-ttu-id="b7a07-116">[Apache Maven](https://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="b7a07-116">[Apache Maven](https://maven.apache.org).</span></span> <span data-ttu-id="b7a07-117">Maven은 프로젝트 빌드 Java 프로젝트에 대 한이 문서와 연결 된 hello 프로젝트에서 사용 되는 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-117">Maven is a project build system for Java projects that is used by hello project associated with this article.</span></span>

## <a name="jdbc-connection-string"></a><span data-ttu-id="b7a07-118">JDBC 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="b7a07-118">JDBC connection string</span></span>

<span data-ttu-id="b7a07-119">Azure에서 JDBC 연결 tooan HDInsight 클러스터는 넘는 443 이루어지고 hello 트래픽이 SSL을 사용 하 여 보호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-119">JDBC connections tooan HDInsight cluster on Azure are made over 443, and hello traffic is secured using SSL.</span></span> <span data-ttu-id="b7a07-120">hello 클러스터 뒤 sit hello 공용 게이트웨이 hello 트래픽 toohello 포트를 HiveServer2에서 실제로 수신 대기를 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-120">hello public gateway that hello clusters sit behind redirects hello traffic toohello port that HiveServer2 is actually listening on.</span></span> <span data-ttu-id="b7a07-121">hello 다음은 연결 문자열의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-121">hello following is an example connection string:</span></span>

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

<span data-ttu-id="b7a07-122">대체 `CLUSTERNAME` HDInsight 클러스터의 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-122">Replace `CLUSTERNAME` with hello name of your HDInsight cluster.</span></span>

## <a name="authentication"></a><span data-ttu-id="b7a07-123">인증</span><span class="sxs-lookup"><span data-stu-id="b7a07-123">Authentication</span></span>

<span data-ttu-id="b7a07-124">Hello 연결을 설정할 때 hello HDInsight 클러스터 관리자 이름 및 암호 tooauthenticate toohello 클러스터 게이트웨이 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-124">When establishing hello connection, you must use hello HDInsight cluster admin name and password tooauthenticate toohello cluster gateway.</span></span> <span data-ttu-id="b7a07-125">스 쿼 럴 SQL과 같은 JDBC 클라이언트를 연결할 때 클라이언트 설정에서 hello 관리자 이름 및 암호를 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-125">When connecting from JDBC clients such as SQuirreL SQL, you must enter hello admin name and password in client settings.</span></span>

<span data-ttu-id="b7a07-126">Java 응용 프로그램에서 연결을 설정할 때 hello 이름 및 암호 사용 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-126">From a Java application, you must use hello name and password when establishing a connection.</span></span> <span data-ttu-id="b7a07-127">예를 들어 hello 다음 Java 코드 새 연결을 열고 hello 연결 문자열, 관리자 이름 및 암호를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="b7a07-127">For example, hello following Java code opens a new connection using hello connection string, admin name, and password:</span></span>

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a><span data-ttu-id="b7a07-128">SQuirreL SQL 클라이언트를 사용하여 연결</span><span class="sxs-lookup"><span data-stu-id="b7a07-128">Connect with SQuirreL SQL client</span></span>

<span data-ttu-id="b7a07-129">스 쿼 럴 SQL은 HDInsight 클러스터와 하이브 쿼리를 사용 하는 tooremotely 실행 될 수 있는 JDBC 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-129">SQuirreL SQL is a JDBC client that can be used tooremotely run Hive queries with your HDInsight cluster.</span></span> <span data-ttu-id="b7a07-130">hello 다음 단계에서는 가정 스 쿼 럴 SQL을 이미 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-130">hello following steps assume that you have already installed SQuirreL SQL.</span></span>

1. <span data-ttu-id="b7a07-131">HDInsight 클러스터에서 hello 하이브 JDBC 드라이버를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-131">Copy hello Hive JDBC drivers from your HDInsight cluster.</span></span>

    * <span data-ttu-id="b7a07-132">에 대 한 **Linux 기반 HDInsight**를 사용 하 여 hello 다음 단계 toodownload 필요한 hello jar 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-132">For **Linux-based HDInsight**, use hello following steps toodownload hello required jar files.</span></span>

        1. <span data-ttu-id="b7a07-133">Hello 파일이 포함 된 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-133">Create a directory that contains hello files.</span></span> <span data-ttu-id="b7a07-134">예: `mkdir hivedriver`.</span><span class="sxs-lookup"><span data-stu-id="b7a07-134">For example, `mkdir hivedriver`.</span></span>

        2. <span data-ttu-id="b7a07-135">명령줄에서 사용 하 여 hello 다음 hello HDInsight 클러스터에서 toocopy hello 파일 명령:</span><span class="sxs-lookup"><span data-stu-id="b7a07-135">From a command line, use hello following commands toocopy hello files from hello HDInsight cluster:</span></span>

            ```bash
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-jdbc*standalone.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .
            ```

            <span data-ttu-id="b7a07-136">대체 `USERNAME` hello 클러스터에 대 한 hello SSH 사용자 계정 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-136">Replace `USERNAME` with hello SSH user account name for hello cluster.</span></span> <span data-ttu-id="b7a07-137">대체 `CLUSTERNAME` hello HDInsight 클러스터 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-137">Replace `CLUSTERNAME` with hello HDInsight cluster name.</span></span>

    * <span data-ttu-id="b7a07-138">에 대 한 **Windows 기반 HDInsight**를 사용 하 여 hello 다음 단계 toodownload hello jar 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-138">For **Windows-based HDInsight**, use hello following steps toodownload hello jar files.</span></span>

        1. <span data-ttu-id="b7a07-139">Hello Azure 포털에서에서 HDInsight 클러스터를 선택한 다음 선택 hello **원격 데스크톱** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-139">From hello Azure portal, select your HDInsight cluster, and then select hello **Remote Desktop** icon.</span></span>

            ![원격 데스크톱 아이콘](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopicon.png)

        2. <span data-ttu-id="b7a07-141">Hello 원격 데스크톱 블레이드에서 hello를 사용 하 여 **연결** 단추 tooconnect toohello 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-141">On hello Remote Desktop blade, use hello **Connect** button tooconnect toohello cluster.</span></span> <span data-ttu-id="b7a07-142">Hello 원격 데스크톱을 사용 하지 않는 경우 hello 양식 tooprovide 사용자 이름 및 암호를 사용 하 여 다음 선택 **사용** hello 클러스터에 대 한 원격 데스크톱 tooenable 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-142">If hello Remote Desktop is not enabled, use hello form tooprovide a user name and password, then select **Enable** tooenable Remote Desktop for hello cluster.</span></span>

            ![원격 데스크톱 블레이드](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopblade.png)

            <span data-ttu-id="b7a07-144">**연결**을 선택하면 .rdp 파일이 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-144">After selecting **Connect**, a .rdp file is downloaded.</span></span> <span data-ttu-id="b7a07-145">이 파일 toolaunch hello 원격 데스크톱 클라이언트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-145">Use this file toolaunch hello Remote Desktop client.</span></span> <span data-ttu-id="b7a07-146">메시지가 표시 되 면 hello 사용자 이름 및 원격 데스크톱 액세스를 위해 입력 한 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-146">When prompted, use hello user name and password you entered for Remote Desktop access.</span></span>

        3. <span data-ttu-id="b7a07-147">연결 되 면 hello hello 원격 데스크톱 세션 tooyour 로컬 컴퓨터에서 다음 파일이 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-147">Once connected, copy hello following files from hello Remote Desktop session tooyour local machine.</span></span> <span data-ttu-id="b7a07-148">`hivedriver`라는 이름의 로컬 디렉터리에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-148">Put them in a local directory named `hivedriver`.</span></span>

            * <span data-ttu-id="b7a07-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar</span><span class="sxs-lookup"><span data-stu-id="b7a07-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar</span></span>
            * <span data-ttu-id="b7a07-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar</span><span class="sxs-lookup"><span data-stu-id="b7a07-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar</span></span>
            * <span data-ttu-id="b7a07-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span><span class="sxs-lookup"><span data-stu-id="b7a07-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span></span>

            > [!NOTE]
            > <span data-ttu-id="b7a07-152">hello 버전 번호 hello 경로 및 파일 이름에 포함 된 클러스터에 대해 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-152">hello version numbers included in hello paths and file names may be different for your cluster.</span></span>

        4. <span data-ttu-id="b7a07-153">Hello 파일 복사 완료 hello 원격 데스크톱 세션 연결을 끊습니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-153">Disconnect hello Remote Desktop session once you have finished copying hello files.</span></span>

2. <span data-ttu-id="b7a07-154">Hello 스 쿼 럴 SQL 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-154">Start hello SQuirreL SQL application.</span></span> <span data-ttu-id="b7a07-155">Hello 창의 hello 왼쪽에서 선택 **드라이버**합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-155">From hello left of hello window, select **Drivers**.</span></span>

    ![Hello hello 창 왼쪽에 드라이버 탭](./media/hdinsight-connect-hive-jdbc-driver/squirreldrivers.png)

3. <span data-ttu-id="b7a07-157">Hello 위쪽 hello에 hello 아이콘에서 **드라이버** 대화 상자에서 선택 hello  **+**  아이콘 toocreate 드라이버입니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-157">From hello icons at hello top of hello **Drivers** dialog, select hello **+** icon toocreate a driver.</span></span>

    ![드라이버 아이콘](./media/hdinsight-connect-hive-jdbc-driver/driversicons.png)

4. <span data-ttu-id="b7a07-159">Hello 드라이버 추가 대화 상자에서 다음 정보는 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-159">In hello Add Driver dialog, add hello following information:</span></span>

    * <span data-ttu-id="b7a07-160">**이름**: Hive</span><span class="sxs-lookup"><span data-stu-id="b7a07-160">**Name**: Hive</span></span>
    * <span data-ttu-id="b7a07-161">**예제 URL**: `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span><span class="sxs-lookup"><span data-stu-id="b7a07-161">**Example URL**: `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span></span>
    * <span data-ttu-id="b7a07-162">**추가 클래스 경로**: 이전에 다운로드 한 hello 추가 단추 tooadd hello jar 파일 사용</span><span class="sxs-lookup"><span data-stu-id="b7a07-162">**Extra Class Path**: Use hello Add button tooadd hello jar files downloaded earlier</span></span>
    * <span data-ttu-id="b7a07-163">**클래스 이름**: org.apache.hive.jdbc.HiveDriver</span><span class="sxs-lookup"><span data-stu-id="b7a07-163">**Class Name**: org.apache.hive.jdbc.HiveDriver</span></span>

   ![드라이버 추가 대화 상자](./media/hdinsight-connect-hive-jdbc-driver/adddriver.png)

   <span data-ttu-id="b7a07-165">클릭 **확인** toosave 이러한 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-165">Click **OK** toosave these settings.</span></span>

5. <span data-ttu-id="b7a07-166">Hello 스 쿼 럴 SQL 창의 hello 왼쪽에서 선택 **별칭**합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-166">On hello left of hello SQuirreL SQL window, select **Aliases**.</span></span> <span data-ttu-id="b7a07-167">Hello 클릭  **+**  아이콘 toocreate 연결 별칭입니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-167">Then click hello **+** icon toocreate a connection alias.</span></span>

    ![새 별칭 추가](./media/hdinsight-connect-hive-jdbc-driver/aliases.png)

6. <span data-ttu-id="b7a07-169">Hello에 대 한 값을 사용 하 여 hello 다음 **추가 별칭** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="b7a07-169">Use hello following values for hello **Add Alias** dialog.</span></span>

    * <span data-ttu-id="b7a07-170">**이름**: Hive on HDInsight</span><span class="sxs-lookup"><span data-stu-id="b7a07-170">**Name**: Hive on HDInsight</span></span>

    * <span data-ttu-id="b7a07-171">**드라이버**: 사용 하 여 hello 드롭다운 tooselect hello **하이브** 드라이버</span><span class="sxs-lookup"><span data-stu-id="b7a07-171">**Driver**: Use hello dropdown tooselect hello **Hive** driver</span></span>

    * <span data-ttu-id="b7a07-172">**URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span><span class="sxs-lookup"><span data-stu-id="b7a07-172">**URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span></span>

        <span data-ttu-id="b7a07-173">대체 **CLUSTERNAME** HDInsight 클러스터의 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-173">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

    * <span data-ttu-id="b7a07-174">**사용자 이름**: HDInsight 클러스터에 대 한 hello 클러스터 로그인 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-174">**User Name**: hello cluster login account name for your HDInsight cluster.</span></span> <span data-ttu-id="b7a07-175">hello 기본값은 `admin`합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-175">hello default is `admin`.</span></span>

    * <span data-ttu-id="b7a07-176">**암호**: hello 클러스터 로그인 계정에 대 한 hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-176">**Password**: hello password for hello cluster login account.</span></span>

 ![별칭 추가 대화 상자](./media/hdinsight-connect-hive-jdbc-driver/addalias.png)

    <span data-ttu-id="b7a07-178">사용 하 여 hello **테스트** 연결이 작동 hello 단추 tooverify 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-178">Use hello **Test** button tooverify that hello connection works.</span></span> <span data-ttu-id="b7a07-179">때 **연결할: HDInsight의 Hive** 선택 대화 상자가 나타나면 **연결** tooperform hello 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-179">When **Connect to: Hive on HDInsight** dialog appears, select **Connect** tooperform hello test.</span></span> <span data-ttu-id="b7a07-180">표시 hello 테스트에 성공 하면는 **성공적으로 연결** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="b7a07-180">If hello test succeeds, you see a **Connection successful** dialog.</span></span>

    <span data-ttu-id="b7a07-181">별칭을 사용 하 여 hello toosave hello 연결 **확인** hello 아래쪽 hello의 단추 **추가 별칭** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="b7a07-181">toosave hello connection alias, use hello **Ok** button at hello bottom of hello **Add Alias** dialog.</span></span>

7. <span data-ttu-id="b7a07-182">Hello에서 **연결할** 스 쿼 럴 SQL의 hello 위쪽 드롭다운 선택 **HDInsight의 Hive**합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-182">From hello **Connect to** dropdown at hello top of SQuirreL SQL, select **Hive on HDInsight**.</span></span> <span data-ttu-id="b7a07-183">메시지가 표시되면 **연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-183">When prompted, select **Connect**.</span></span>

    ![연결 대화 상자](./media/hdinsight-connect-hive-jdbc-driver/connect.png)

8. <span data-ttu-id="b7a07-185">연결 되 면 다음 hello SQL 쿼리 대화 상자에 쿼리를 클릭 한 hello hello 입력 **실행** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-185">Once connected, enter hello following query into hello SQL query dialog, and then select hello **Run** icon.</span></span> <span data-ttu-id="b7a07-186">hello 결과 영역을 hello hello 쿼리 결과 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-186">hello results area should show hello results of hello query.</span></span>

        select * from hivesampletable limit 10;

    ![결과를 포함한 sql 쿼리 대화 상자](./media/hdinsight-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a><span data-ttu-id="b7a07-188">Java 응용 프로그램 예제에서 연결</span><span class="sxs-lookup"><span data-stu-id="b7a07-188">Connect from an example Java application</span></span>

<span data-ttu-id="b7a07-189">HDInsight의 Java 클라이언트 tooquery 하이브를 사용 하는 예제에서 제공 됩니다. [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc)합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-189">An example of using a Java client tooquery Hive on HDInsight is available at [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span></span> <span data-ttu-id="b7a07-190">Hello 리포지토리 toobuild의 hello 지침에 따르고 hello 샘플을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-190">Follow hello instructions in hello repository toobuild and run hello sample.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b7a07-191">문제 해결</span><span class="sxs-lookup"><span data-stu-id="b7a07-191">Troubleshooting</span></span>

### <a name="unexpected-error-occurred-attempting-tooopen-an-sql-connection"></a><span data-ttu-id="b7a07-192">예기치 않은 오류가 발생 오류가 tooopen SQL 연결</span><span class="sxs-lookup"><span data-stu-id="b7a07-192">Unexpected Error occurred attempting tooopen an SQL connection</span></span>

<span data-ttu-id="b7a07-193">**증상**: 버전 3.3 또는 3.4 tooan HDInsight 클러스터를 연결할 때 예기치 않은 오류가 발생 한 오류에 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-193">**Symptoms**: When connecting tooan HDInsight cluster that is version 3.3 or 3.4, you may receive an error that an unexpected error occurred.</span></span> <span data-ttu-id="b7a07-194">이 오류에 대 한 스택 추적 hello hello 다음 줄으로 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-194">hello stack trace for this error begins with hello following lines:</span></span>

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

<span data-ttu-id="b7a07-195">**원인**:이 오류는 스 쿼 럴 및 hello hello 하이브 JDBC 구성 요소에 필요한 하나에서 사용 하는 hello commons codec.jar 파일의 hello 버전 불일치로 인해 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-195">**Cause**: This error is caused by a mismatch in hello version of hello commons-codec.jar file used by SQuirreL and hello one required by hello Hive JDBC components.</span></span>

<span data-ttu-id="b7a07-196">**해결 방법**: toofix이이 오류를 사용 하 여 hello 다음 단계:</span><span class="sxs-lookup"><span data-stu-id="b7a07-196">**Resolution**: toofix this error, use hello following steps:</span></span>

1. <span data-ttu-id="b7a07-197">HDInsight 클러스터에서 hello commons 코덱 jar 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-197">Download hello commons-codec jar file from your HDInsight cluster.</span></span>

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. <span data-ttu-id="b7a07-198">스 쿼 럴을 종료 하 고 스 쿼 럴 시스템에 설치 되어 있는 되 toohello 디렉터리 이동 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b7a07-198">Exit SQuirreL, and then go toohello directory where SQuirreL is installed on your system.</span></span> <span data-ttu-id="b7a07-199">Hello 아래의 hello 스 쿼 럴 디렉터리에서 `lib` 바꾸기 hello 기존 commons-codec.jar hello HDInsight 클러스터에서 다운로드 한 hello로 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-199">In hello SquirreL directory, under hello `lib` directory, replace hello existing commons-codec.jar with hello one downloaded from hello HDInsight cluster.</span></span>

3. <span data-ttu-id="b7a07-200">SQuirreL을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-200">Restart SQuirreL.</span></span> <span data-ttu-id="b7a07-201">HDInsight의 tooHive 연결할 때 hello 오류가 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-201">hello error should no longer occur when connecting tooHive on HDInsight.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7a07-202">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b7a07-202">Next steps</span></span>

<span data-ttu-id="b7a07-203">이제는 어떻게 하이브를 사용 하 여 hello 뒤와 toouse JDBC toowork 링크 tooexplore Azure HDInsight와 다른 방법으로 toowork 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="b7a07-203">Now that you have learned how toouse JDBC toowork with Hive, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* [<span data-ttu-id="b7a07-204">데이터 tooHDInsight 업로드</span><span class="sxs-lookup"><span data-stu-id="b7a07-204">Upload data tooHDInsight</span></span>](hdinsight-upload-data.md)
* [<span data-ttu-id="b7a07-205">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="b7a07-205">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="b7a07-206">HDInsight에서 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="b7a07-206">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="b7a07-207">HDInsight에서 MapReduce 작업 사용</span><span class="sxs-lookup"><span data-stu-id="b7a07-207">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
