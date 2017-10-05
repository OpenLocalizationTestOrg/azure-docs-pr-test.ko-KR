---
title: "JDBC 드라이버를 통해 Hive 쿼리 - Azure HDInsight | Microsoft Docs"
description: "Java 응용 프로그램에서 JDBC 드라이버를 사용하여 HDInsight의 Hadoop에 Hive 쿼리를 제출합니다. 프로그래밍 방식으로 SQuirrel SQL 클라이언트에서 연결합니다."
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
ms.openlocfilehash: f2de58c2763b2ddd0926336164738929c477c4ae
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="query-hive-through-the-jdbc-driver-in-hdinsight"></a><span data-ttu-id="28d02-104">HDInsight에서 JDBC 드라이버를 통해 Hive 쿼리</span><span class="sxs-lookup"><span data-stu-id="28d02-104">Query Hive through the JDBC driver in HDInsight</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="28d02-105">Java 응용 프로그램에서 JDBC 드라이버를 사용하여 Azure HDInsight의 Hadoop에 Hive 쿼리를 제출하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-105">Learn how to use the JDBC driver from a Java application to submit Hive queries to Hadoop in Azure HDInsight.</span></span> <span data-ttu-id="28d02-106">이 문서의 정보는 프로그래밍 방식으로 SQuirrel SQL 클라이언트에서 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-106">The information in this document demonstrates how to connect programmatically and from the SQuirrel SQL client.</span></span>

<span data-ttu-id="28d02-107">Hive JDBC 인터페이스에 대한 자세한 내용은 [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="28d02-107">For more information on the Hive JDBC Interface, see [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="28d02-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="28d02-108">Prerequisites</span></span>

* <span data-ttu-id="28d02-109">HDInsight 클러스터의 Hadoop.</span><span class="sxs-lookup"><span data-stu-id="28d02-109">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="28d02-110">Linux 또는 Windows 기반의 클러스터가 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-110">Either Linux-based or Windows-based clusters work.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="28d02-111">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="28d02-112">자세한 내용은 [HDInsight 3.3 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="28d02-112">For more information, see [HDInsight 3.3 retirement](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="28d02-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span><span class="sxs-lookup"><span data-stu-id="28d02-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span></span> <span data-ttu-id="28d02-114">SQuirreL은 JDBC 클라이언트 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-114">SQuirreL is a JDBC client application.</span></span>

* <span data-ttu-id="28d02-115">[JDK(Java Developer Kit) 버전 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) 이상</span><span class="sxs-lookup"><span data-stu-id="28d02-115">The [Java Developer Kit (JDK) version 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span>

* <span data-ttu-id="28d02-116">[Apache Maven](https://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="28d02-116">[Apache Maven](https://maven.apache.org).</span></span> <span data-ttu-id="28d02-117">Maven은 이 문서와 관련된 프로젝트에서 사용되는 Java 프로젝트에 대한 프로젝트 빌드 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-117">Maven is a project build system for Java projects that is used by the project associated with this article.</span></span>

## <a name="jdbc-connection-string"></a><span data-ttu-id="28d02-118">JDBC 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="28d02-118">JDBC connection string</span></span>

<span data-ttu-id="28d02-119">Azure에서 HDInsight 클러스터에 대한 JDBC가 443을 통해 연결되어 트래픽이 SSL을 사용하여 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-119">JDBC connections to an HDInsight cluster on Azure are made over 443, and the traffic is secured using SSL.</span></span> <span data-ttu-id="28d02-120">클러스터가 뒤에 있는 공용 게이트웨이는 HiveServer2에서 실제로 수신하는 포트로 트래픽을 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-120">The public gateway that the clusters sit behind redirects the traffic to the port that HiveServer2 is actually listening on.</span></span> <span data-ttu-id="28d02-121">다음은 예제 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-121">The following is an example connection string:</span></span>

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

<span data-ttu-id="28d02-122">`CLUSTERNAME` 을 HDInsight 클러스터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-122">Replace `CLUSTERNAME` with the name of your HDInsight cluster.</span></span>

## <a name="authentication"></a><span data-ttu-id="28d02-123">인증</span><span class="sxs-lookup"><span data-stu-id="28d02-123">Authentication</span></span>

<span data-ttu-id="28d02-124">연결을 설정할 때 HDInsight 클러스터 관리자 이름 및 암호를 사용하여 클러스터 게이트웨이에 대해 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-124">When establishing the connection, you must use the HDInsight cluster admin name and password to authenticate to the cluster gateway.</span></span> <span data-ttu-id="28d02-125">SQuirreL SQL 등의 JDBC 클라이언트에서 연결할 때 클라이언트 설정에 관리자 이름 및 암호를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-125">When connecting from JDBC clients such as SQuirreL SQL, you must enter the admin name and password in client settings.</span></span>

<span data-ttu-id="28d02-126">Java 응용 프로그램에서 연결을 설정할 때 이름 및 암호를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-126">From a Java application, you must use the name and password when establishing a connection.</span></span> <span data-ttu-id="28d02-127">예를 들어 다음 Java 코드는 연결 문자열, 관리자 이름 및 암호를 사용하여 새 연결을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-127">For example, the following Java code opens a new connection using the connection string, admin name, and password:</span></span>

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a><span data-ttu-id="28d02-128">SQuirreL SQL 클라이언트를 사용하여 연결</span><span class="sxs-lookup"><span data-stu-id="28d02-128">Connect with SQuirreL SQL client</span></span>

<span data-ttu-id="28d02-129">SQuirreL SQL은 HDInsight 클러스터와 함께 Hive 쿼리를 원격으로 실행하는 데 사용할 수 있는 JDBC 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-129">SQuirreL SQL is a JDBC client that can be used to remotely run Hive queries with your HDInsight cluster.</span></span> <span data-ttu-id="28d02-130">다음 단계에서는 SQuirreL SQL을 이미 설치했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-130">The following steps assume that you have already installed SQuirreL SQL.</span></span>

1. <span data-ttu-id="28d02-131">HDInsight 클러스터에서 Hive JDBC 드라이버를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-131">Copy the Hive JDBC drivers from your HDInsight cluster.</span></span>

    * <span data-ttu-id="28d02-132">**Linux 기반 HDInsight**의 경우 다음 단계에 따라 필요한 jar 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-132">For **Linux-based HDInsight**, use the following steps to download the required jar files.</span></span>

        1. <span data-ttu-id="28d02-133">파일을 포함하는 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-133">Create a directory that contains the files.</span></span> <span data-ttu-id="28d02-134">예: `mkdir hivedriver`.</span><span class="sxs-lookup"><span data-stu-id="28d02-134">For example, `mkdir hivedriver`.</span></span>

        2. <span data-ttu-id="28d02-135">명령줄에서 다음 명령을 사용하여 HDInsight 클러스터에서 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-135">From a command line, use the following commands to copy the files from the HDInsight cluster:</span></span>

            ```bash
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-jdbc*standalone.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .
            ```

            <span data-ttu-id="28d02-136">`USERNAME`은 클러스터의 SSH 사용자 계정 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-136">Replace `USERNAME` with the SSH user account name for the cluster.</span></span> <span data-ttu-id="28d02-137">`CLUSTERNAME`은 HDInsight 클러스터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-137">Replace `CLUSTERNAME` with the HDInsight cluster name.</span></span>

    * <span data-ttu-id="28d02-138">**Windows 기반 HDInsight**의 경우 다음 단계에 따라 jar 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-138">For **Windows-based HDInsight**, use the following steps to download the jar files.</span></span>

        1. <span data-ttu-id="28d02-139">Azure Portal에서 HDInsight 클러스터를 선택한 다음 **원격 데스크톱** 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-139">From the Azure portal, select your HDInsight cluster, and then select the **Remote Desktop** icon.</span></span>

            ![원격 데스크톱 아이콘](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopicon.png)

        2. <span data-ttu-id="28d02-141">[원격 데스크톱] 블레이드에서 **연결** 단추를 사용하여 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-141">On the Remote Desktop blade, use the **Connect** button to connect to the cluster.</span></span> <span data-ttu-id="28d02-142">원격 데스크톱을 사용하지 않는 경우 사용자 이름 및 암호를 입력하는 양식을 사용한 다음 **사용**을 선택하여 클러스터에서 원격 데스크톱을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-142">If the Remote Desktop is not enabled, use the form to provide a user name and password, then select **Enable** to enable Remote Desktop for the cluster.</span></span>

            ![원격 데스크톱 블레이드](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopblade.png)

            <span data-ttu-id="28d02-144">**연결**을 선택하면 .rdp 파일이 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-144">After selecting **Connect**, a .rdp file is downloaded.</span></span> <span data-ttu-id="28d02-145">이 파일을 사용하여 원격 데스크톱 클라이언트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-145">Use this file to launch the Remote Desktop client.</span></span> <span data-ttu-id="28d02-146">메시지가 표시되면 원격 데스크톱 액세스에 입력한 사용자 이름 및 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-146">When prompted, use the user name and password you entered for Remote Desktop access.</span></span>

        3. <span data-ttu-id="28d02-147">연결되면 원격 데스크톱 세션에서 다음 파일을 로컬 컴퓨터에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-147">Once connected, copy the following files from the Remote Desktop session to your local machine.</span></span> <span data-ttu-id="28d02-148">`hivedriver`라는 이름의 로컬 디렉터리에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-148">Put them in a local directory named `hivedriver`.</span></span>

            * <span data-ttu-id="28d02-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar</span><span class="sxs-lookup"><span data-stu-id="28d02-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar</span></span>
            * <span data-ttu-id="28d02-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar</span><span class="sxs-lookup"><span data-stu-id="28d02-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar</span></span>
            * <span data-ttu-id="28d02-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span><span class="sxs-lookup"><span data-stu-id="28d02-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span></span>

            > [!NOTE]
            > <span data-ttu-id="28d02-152">경로 및 파일 이름에 포함된 버전 번호는 클러스터마다 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-152">The version numbers included in the paths and file names may be different for your cluster.</span></span>

        4. <span data-ttu-id="28d02-153">파일을 복사한 후 원격 데스크톱 세션의 연결을 끊습니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-153">Disconnect the Remote Desktop session once you have finished copying the files.</span></span>

2. <span data-ttu-id="28d02-154">SQuirreL SQL 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-154">Start the SQuirreL SQL application.</span></span> <span data-ttu-id="28d02-155">왼쪽 창에서 **드라이버**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-155">From the left of the window, select **Drivers**.</span></span>

    ![창 왼쪽의 드라이버 탭](./media/hdinsight-connect-hive-jdbc-driver/squirreldrivers.png)

3. <span data-ttu-id="28d02-157">**드라이버** 대화 상자 위쪽의 아이콘에서 **+** 아이콘을 선택하여 드라이버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-157">From the icons at the top of the **Drivers** dialog, select the **+** icon to create a driver.</span></span>

    ![드라이버 아이콘](./media/hdinsight-connect-hive-jdbc-driver/driversicons.png)

4. <span data-ttu-id="28d02-159">드라이버 추가 대화 상자에 다음 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-159">In the Add Driver dialog, add the following information:</span></span>

    * <span data-ttu-id="28d02-160">**이름**: Hive</span><span class="sxs-lookup"><span data-stu-id="28d02-160">**Name**: Hive</span></span>
    * <span data-ttu-id="28d02-161">**예제 URL**: `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span><span class="sxs-lookup"><span data-stu-id="28d02-161">**Example URL**: `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span></span>
    * <span data-ttu-id="28d02-162">**추가 클래스 경로**: [추가] 단추를 사용하여 이전에 다운로드한 jar 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-162">**Extra Class Path**: Use the Add button to add the jar files downloaded earlier</span></span>
    * <span data-ttu-id="28d02-163">**클래스 이름**: org.apache.hive.jdbc.HiveDriver</span><span class="sxs-lookup"><span data-stu-id="28d02-163">**Class Name**: org.apache.hive.jdbc.HiveDriver</span></span>

   ![드라이버 추가 대화 상자](./media/hdinsight-connect-hive-jdbc-driver/adddriver.png)

   <span data-ttu-id="28d02-165">**확인**을 클릭하여 이러한 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-165">Click **OK** to save these settings.</span></span>

5. <span data-ttu-id="28d02-166">SQuirreL SQL 창의 왼쪽에서 **별칭**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-166">On the left of the SQuirreL SQL window, select **Aliases**.</span></span> <span data-ttu-id="28d02-167">그런 다음 **+** 아이콘을 클릭하여 연결 별칭을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-167">Then click the **+** icon to create a connection alias.</span></span>

    ![새 별칭 추가](./media/hdinsight-connect-hive-jdbc-driver/aliases.png)

6. <span data-ttu-id="28d02-169">**별칭 추가** 대화 상자에서 다음 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-169">Use the following values for the **Add Alias** dialog.</span></span>

    * <span data-ttu-id="28d02-170">**이름**: Hive on HDInsight</span><span class="sxs-lookup"><span data-stu-id="28d02-170">**Name**: Hive on HDInsight</span></span>

    * <span data-ttu-id="28d02-171">**드라이버**: 드롭다운에서 **Hive** 드라이버를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-171">**Driver**: Use the dropdown to select the **Hive** driver</span></span>

    * <span data-ttu-id="28d02-172">**URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span><span class="sxs-lookup"><span data-stu-id="28d02-172">**URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span></span>

        <span data-ttu-id="28d02-173">**CLUSTERNAME** 을 HDInsight 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-173">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>

    * <span data-ttu-id="28d02-174">**사용자 이름**: HDInsight 클러스터의 클러스터 로그인 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-174">**User Name**: The cluster login account name for your HDInsight cluster.</span></span> <span data-ttu-id="28d02-175">기본값은 `admin`입니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-175">The default is `admin`.</span></span>

    * <span data-ttu-id="28d02-176">**암호**: 클러스터 로그인 계정의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-176">**Password**: The password for the cluster login account.</span></span>

 ![별칭 추가 대화 상자](./media/hdinsight-connect-hive-jdbc-driver/addalias.png)

    <span data-ttu-id="28d02-178">**테스트** 단추를 사용하여 연결이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-178">Use the **Test** button to verify that the connection works.</span></span> <span data-ttu-id="28d02-179">**연결 대상: Hive on HDInsight** 대화 상자가 나타나면 **연결**을 선택하여 테스트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-179">When **Connect to: Hive on HDInsight** dialog appears, select **Connect** to perform the test.</span></span> <span data-ttu-id="28d02-180">테스트가 성공하면 **연결 성공** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-180">If the test succeeds, you see a **Connection successful** dialog.</span></span>

    <span data-ttu-id="28d02-181">연결 별칭을 저장하려면 **별칭 추가** 대화 상자의 아래쪽에 있는 **확인** 단추를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-181">To save the connection alias, use the **Ok** button at the bottom of the **Add Alias** dialog.</span></span>

7. <span data-ttu-id="28d02-182">SQuirreL SQL 위쪽의 **연결 대상** 드롭다운에서 **Hive on HDInsight**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-182">From the **Connect to** dropdown at the top of SQuirreL SQL, select **Hive on HDInsight**.</span></span> <span data-ttu-id="28d02-183">메시지가 표시되면 **연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-183">When prompted, select **Connect**.</span></span>

    ![연결 대화 상자](./media/hdinsight-connect-hive-jdbc-driver/connect.png)

8. <span data-ttu-id="28d02-185">연결되면 SQL 쿼리 대화 상자에 다음 쿼리를 입력한 다음 **실행** 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-185">Once connected, enter the following query into the SQL query dialog, and then select the **Run** icon.</span></span> <span data-ttu-id="28d02-186">결과 영역에 쿼리 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-186">The results area should show the results of the query.</span></span>

        select * from hivesampletable limit 10;

    ![결과를 포함한 sql 쿼리 대화 상자](./media/hdinsight-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a><span data-ttu-id="28d02-188">Java 응용 프로그램 예제에서 연결</span><span class="sxs-lookup"><span data-stu-id="28d02-188">Connect from an example Java application</span></span>

<span data-ttu-id="28d02-189">HDInsight에서 Hive를 쿼리하는 데 Java 클라이언트를 사용하는 예제를 [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-189">An example of using a Java client to query Hive on HDInsight is available at [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span></span> <span data-ttu-id="28d02-190">리포지토리의 지침에 따라 샘플을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-190">Follow the instructions in the repository to build and run the sample.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="28d02-191">문제 해결</span><span class="sxs-lookup"><span data-stu-id="28d02-191">Troubleshooting</span></span>

### <a name="unexpected-error-occurred-attempting-to-open-an-sql-connection"></a><span data-ttu-id="28d02-192">SQL 연결을 열 때 예기치 않은 오류가 발생했습니다</span><span class="sxs-lookup"><span data-stu-id="28d02-192">Unexpected Error occurred attempting to open an SQL connection</span></span>

<span data-ttu-id="28d02-193">**증상**: 버전 3.3 또는 3.4인 HDInsight 클러스터에 연결할 때 예기치 않은 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-193">**Symptoms**: When connecting to an HDInsight cluster that is version 3.3 or 3.4, you may receive an error that an unexpected error occurred.</span></span> <span data-ttu-id="28d02-194">이 오류에 대한 스택 추적은 다음 줄로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-194">The stack trace for this error begins with the following lines:</span></span>

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

<span data-ttu-id="28d02-195">**원인**: 이 오류는 SQuirreL에서 사용하는 common-codec.jar 파일 버전과 Hive JDBC 구성 요소에 필요한 파일의 버전과 일치하지 않아 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-195">**Cause**: This error is caused by a mismatch in the version of the commons-codec.jar file used by SQuirreL and the one required by the Hive JDBC components.</span></span>

<span data-ttu-id="28d02-196">**해결**: 이 오류를 해결하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-196">**Resolution**: To fix this error, use the following steps:</span></span>

1. <span data-ttu-id="28d02-197">HDInsight 클러스터에서 common-codec jar 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-197">Download the commons-codec jar file from your HDInsight cluster.</span></span>

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. <span data-ttu-id="28d02-198">SQuirreL을 종료한 다음 시스템에서 SQuirreL이 설치된 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-198">Exit SQuirreL, and then go to the directory where SQuirreL is installed on your system.</span></span> <span data-ttu-id="28d02-199">SquirreL 디렉터리의 `lib` 디렉터리에서 기존 common-codec.jar 파일을 HDInsight 클러스터에서 다운로드한 파일로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-199">In the SquirreL directory, under the `lib` directory, replace the existing commons-codec.jar with the one downloaded from the HDInsight cluster.</span></span>

3. <span data-ttu-id="28d02-200">SQuirreL을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-200">Restart SQuirreL.</span></span> <span data-ttu-id="28d02-201">HDInsight에서 Hive에 연결할 때 오류가 더 이상 발생하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-201">The error should no longer occur when connecting to Hive on HDInsight.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28d02-202">다음 단계</span><span class="sxs-lookup"><span data-stu-id="28d02-202">Next steps</span></span>

<span data-ttu-id="28d02-203">JDBC를 사용하여 Hive와 함께 작업하는 방법을 살펴보았으므로 이제 다음 링크를 사용하여 Azure HDInsight로 작업하는 다른 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="28d02-203">Now that you have learned how to use JDBC to work with Hive, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* [<span data-ttu-id="28d02-204">HDInsight에 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="28d02-204">Upload data to HDInsight</span></span>](hdinsight-upload-data.md)
* [<span data-ttu-id="28d02-205">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="28d02-205">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="28d02-206">HDInsight에서 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="28d02-206">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="28d02-207">HDInsight에서 MapReduce 작업 사용</span><span class="sxs-lookup"><span data-stu-id="28d02-207">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
