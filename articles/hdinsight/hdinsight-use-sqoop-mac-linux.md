---
title: "Hadoop과 Apache Sqoop - Azure HDInsight | Microsoft Docs"
description: "Apache Sqoop을 사용하여 HDInsight의 Hadoop과 Azure SQL Database 간에 가져오기 및 내보내기를 수행하는 방법을 알아봅니다."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
author: Blackmist
tags: azure-portal
keywords: hadoop sqoop,sqoop
ms.assetid: 303649a5-4be5-4933-bf1d-4b232083c354
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: 35dcbb91e6af1480685c9fd5b829c54277c1c605
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-apache-sqoop-to-import-and-export-data-between-hadoop-on-hdinsight-and-sql-database"></a><span data-ttu-id="d88a6-104">Apache Sqoop을 사용하여 HDInsight의 Hadoop과 SQL Database 간에 데이터 가져오기 및 내보내기</span><span class="sxs-lookup"><span data-stu-id="d88a6-104">Use Apache Sqoop to import and export data between Hadoop on HDInsight and SQL Database</span></span>

[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="d88a6-105">Apache Sqoop을 사용하여 Azure HDInsight의 Hadoop 클러스터와 Azure SQL Database 또는 Microsoft SQL Server Database 사이에서 가져오기 및 내보내기를 수행하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-105">Learn how to use Apache Sqoop to import and export between a Hadoop cluster in Azure HDInsight and Azure SQL Database or Microsoft SQL Server database.</span></span> <span data-ttu-id="d88a6-106">이 문서의 단계에서는 Hadoop 클러스터의 헤드에서 직접 `sqoop` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-106">The steps in this document use the `sqoop` command directly from the headnode of the Hadoop cluster.</span></span> <span data-ttu-id="d88a6-107">SSH를 사용하여 헤드 노드에 연결하고 이 문서의 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-107">You use SSH to connect to the head node and run the commands in this document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d88a6-108">이 문서의 단계는 Linux를 사용하는 HDInsight 클러스터에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-108">The steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="d88a6-109">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d88a6-110">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d88a6-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="install-freetds"></a><span data-ttu-id="d88a6-111">FreeTDS 설치</span><span class="sxs-lookup"><span data-stu-id="d88a6-111">Install FreeTDS</span></span>

1. <span data-ttu-id="d88a6-112">SSH를 사용하여 HDInsight 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-112">Use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="d88a6-113">예를 들어 다음 명령은 `mycluster`라는 클러스터의 기본 헤드 노드에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-113">For example, the following command connects to the primary headnode of a cluster named `mycluster`:</span></span>

    ```bash
    ssh CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="d88a6-114">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d88a6-114">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="d88a6-115">다음 명령을 사용하여 FreeTDS:를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-115">Use the following command to install FreeTDS:</span></span>

    ```bash
    sudo apt --assume-yes install freetds-dev freetds-bin
    ```

    <span data-ttu-id="d88a6-116">FreeTDS는 SQL Database에 연결하기 위해 여러 단계에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-116">FreeTDS is used in several steps to connect to SQL Database.</span></span>

## <a name="create-the-table-in-sql-database"></a><span data-ttu-id="d88a6-117">SQL 데이터베이스에 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="d88a6-117">Create the table in SQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d88a6-118">[클러스터 및 SQL Database 만들기](hdinsight-use-sqoop.md)에서 만든 HDInsight 클러스터 및 SQL Database를 사용하고 있는 경우 이 섹션의 단계를 무시하십시오.</span><span class="sxs-lookup"><span data-stu-id="d88a6-118">If you are using the HDInsight cluster and SQL Database created in [Create cluster and SQL database](hdinsight-use-sqoop.md), skip the steps in this section.</span></span> <span data-ttu-id="d88a6-119">데이터베이스 테이블은 [클러스터 및 SQL Database 만들기](hdinsight-use-sqoop.md)의 단계 중에 생성된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-119">The database and table were created as part of the steps in the [Create cluster and SQL database](hdinsight-use-sqoop.md) document.</span></span>

1. <span data-ttu-id="d88a6-120">SSH 세션에서 다음 명령을 사용하여 SQL Database 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-120">From the SSH session, use the following command to connect to the SQL Database server.</span></span>

        TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D sqooptest

    <span data-ttu-id="d88a6-121">다음 텍스트와 비슷한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-121">You receive output similar to the following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set to sqooptest
        1>

2. <span data-ttu-id="d88a6-122">`1>` 프롬프트에 다음 쿼리를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-122">At the `1>` prompt, enter the following query:</span></span>

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)
    GO
    ```

    <span data-ttu-id="d88a6-123">`GO` 문을 입력하면 이전 문이 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-123">When the `GO` statement is entered, the previous statements are evaluated.</span></span> <span data-ttu-id="d88a6-124">먼저 **mobiledata** 테이블이 생성된 다음 클러스터형 인덱스가 추가됩니다(SQL 데이터베이스에 필수).</span><span class="sxs-lookup"><span data-stu-id="d88a6-124">First, the **mobiledata** table is created, then a clustered index is added to it (required by SQL Database.)</span></span>

    <span data-ttu-id="d88a6-125">다음 쿼리를 사용하여 테이블이 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-125">Use the following query to verify that the table has been created:</span></span>

    ```sql
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="d88a6-126">그러면 다음 텍스트와 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-126">You see output similar to the following text:</span></span>

        TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
        sqooptest       dbo     mobiledata      BASE TABLE

3. <span data-ttu-id="d88a6-127">`exit` at the `1>` 를 입력하여 tsql 유틸리티를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-127">Enter `exit` at the `1>` prompt to exit the tsql utility.</span></span>

## <a name="sqoop-export"></a><span data-ttu-id="d88a6-128">Sqoop 내보내기</span><span class="sxs-lookup"><span data-stu-id="d88a6-128">Sqoop export</span></span>

1. <span data-ttu-id="d88a6-129">SSH와 클러스터 간 연결에서 다음 명령을 사용하여 Sqoop이 SQL Database를 볼 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-129">From the SSH connection to the cluster, use the following command to verify that Sqoop can see your SQL Database:</span></span>

    ```bash
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> -P
    ```
    <span data-ttu-id="d88a6-130">확인 메시지가 표시되면 SQL Database 로그인의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-130">When prompted, enter the password for the SQL Database login.</span></span>

    <span data-ttu-id="d88a6-131">이 명령은 앞에서 만든 **sqooptest** 데이터베이스를 포함한 데이터베이스 목록이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-131">This command returns a list of databases, including the **sqooptest** database that you created earlier.</span></span>

2. <span data-ttu-id="d88a6-132">**hivesampletable**에서 **mobiledata** 테이블로 데이터를 내보내려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-132">To export data from **hivesampletable** to the **mobiledata** table, use the following command:</span></span>

    ```bash
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> -P --table 'mobiledata' --export-dir 'wasb:///hive/warehouse/hivesampletable' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="d88a6-133">이 명령은 Sqoop에 **sqooptest** 데이터베이스에 연결하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-133">This command instructs Sqoop to connect to the **sqooptest** database.</span></span> <span data-ttu-id="d88a6-134">그러면 Sqoop은 **wasb:///hive/warehouse/hivesampletable**에서 **mobiledata** 테이블로 데이터를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-134">Sqoop then exports data from **wasb:///hive/warehouse/hivesampletable** to the **mobiledata** table.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d88a6-135">클러스터의 기본 저장소가 Azure Storage 계정이면 `wasb:///`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-135">Use `wasb:///` if the default storage for your cluster is an Azure Storage account.</span></span> <span data-ttu-id="d88a6-136">Azure Data Lake Store이면 `adl:///`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-136">Use `adl:///` if it is an Azure Data Lake Store.</span></span>

3. <span data-ttu-id="d88a6-137">명령이 완료되면 다음 명령과 TSQL을 사용하여 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-137">After the command completes, use the following command to connect to the database using TSQL:</span></span>

    ```bash
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P -p 1433 -D sqooptest
    ```

    <span data-ttu-id="d88a6-138">연결되면 다음 명령문을 사용하여 데이터가 **mobiledata** 테이블로 내보내기되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-138">Once connected, use the following statements to verify that the data was exported to the **mobiledata** table:</span></span>

    ```sql
    SET ROWCOUNT 50;
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="d88a6-139">테이블에 데이터 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-139">You should see a listing of data in the table.</span></span> <span data-ttu-id="d88a6-140">`exit` 를 입력하여 tsql 유틸리티를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-140">Type `exit` to exit the tsql utility.</span></span>

## <a name="sqoop-import"></a><span data-ttu-id="d88a6-141">Sqoop 가져오기</span><span class="sxs-lookup"><span data-stu-id="d88a6-141">Sqoop import</span></span>

1. <span data-ttu-id="d88a6-142">다음 명령을 사용하여 SQL Database의 **mobiledata** 테이블에서 HDInsight의 **wasb:///tutorials/usesqoop/importeddata** 디렉터리로 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-142">Use the following command to import data from the **mobiledata** table in SQL Database, to the **wasb:///tutorials/usesqoop/importeddata** directory on HDInsight:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

    <span data-ttu-id="d88a6-143">데이터의 필드는 탭 문자로 구분되어 있으며 줄은 줄 바꿈 문자로 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-143">The fields in the data are separated by a tab character, and the lines are terminated by a new-line character.</span></span>

2. <span data-ttu-id="d88a6-144">가져오기가 완료되면 다음 명령을 사용하여 새로운 디렉터리에 데이터를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-144">Once the import has completed, use the following command to list out the data in the new directory:</span></span>

    ```bash
    hdfs dfs -text /tutorials/usesqoop/importeddata/part-m-00000
    ```

## <a name="using-sql-server"></a><span data-ttu-id="d88a6-145">SQL Server 사용하기</span><span class="sxs-lookup"><span data-stu-id="d88a6-145">Using SQL Server</span></span>

<span data-ttu-id="d88a6-146">또한 Sqoop을 사용하여 데이터 센터 내 또는 Azure에 호스팅된 가상 컴퓨터에서 SQL Server로부터 데이터를 가져오기/내보내기할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-146">You can also use Sqoop to import and export data from SQL Server, either in your data center or on a Virtual Machine hosted in Azure.</span></span> <span data-ttu-id="d88a6-147">SQL 데이터베이스와 SQL Server의 차이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-147">The differences between using SQL Database and SQL Server are:</span></span>

* <span data-ttu-id="d88a6-148">HDInsight와 SQL Server가 모두 동일한 Azure Virtual Network에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-148">Both HDInsight and SQL Server must be on the same Azure Virtual Network.</span></span>

    <span data-ttu-id="d88a6-149">예제를 보려면 [온-프레미스 네트워크에 HDInsight 연결](./connect-on-premises-network.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d88a6-149">For an example, see the [Connect HDInsight to your on-premises network](./connect-on-premises-network.md) document.</span></span>

    <span data-ttu-id="d88a6-150">HDInsight와 함께 Azure Virtual Network를 사용하는 방법에 대한 자세한 내용은 [Azure Virtual Network를 사용하여 HDInsight 확장](hdinsight-extend-hadoop-virtual-network.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d88a6-150">For more information on using HDInsight with an Azure Virtual Network, see the [Extend HDInsight with Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span> <span data-ttu-id="d88a6-151">Azure Virtual Network에 대한 자세한 내용은 [가상 네트워크 개요](../virtual-network/virtual-networks-overview.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d88a6-151">For more information on Azure Virtual Network, see the [Virtual Network Overview](../virtual-network/virtual-networks-overview.md) document.</span></span>

* <span data-ttu-id="d88a6-152">SQL Server는 SQL 인증을 허용하도록 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-152">SQL Server must be configured to allow SQL authentication.</span></span> <span data-ttu-id="d88a6-153">자세한 내용은 [인증 모드 선택](https://msdn.microsoft.com/ms144284.aspx) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d88a6-153">For more information, see the [Choose an Authentication Mode](https://msdn.microsoft.com/ms144284.aspx) document.</span></span>

* <span data-ttu-id="d88a6-154">SQL Server를 원격 연결을 허용하도록 구성해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-154">You may have to configure SQL Server to accept remote connections.</span></span> <span data-ttu-id="d88a6-155">자세한 내용은 [SQL Server 데이터베이스 엔진에 연결하는 문제를 해결하는 방법](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx)(영문)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d88a6-155">For more information, see the [How to troubleshoot connecting to the SQL Server database engine](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) document.</span></span>

* <span data-ttu-id="d88a6-156">**SQL Server Management Studio**, **tsql** 등의 유틸리티를 사용하여 SQL Server에 **sqooptest** 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-156">Create the **sqooptest** database in SQL Server using a utility such as **SQL Server Management Studio** or **tsql**.</span></span> <span data-ttu-id="d88a6-157">Azure CLI를 사용하는 단계는 Azure SQL Database에만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-157">The steps for using the Azure CLI only work for Azure SQL Database.</span></span>

    <span data-ttu-id="d88a6-158">다음 Transact-SQL 문을 사용하여 **mobiledata** 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-158">Use the following Transact-SQL statements to create the **mobiledata** table:</span></span>

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    ```

* <span data-ttu-id="d88a6-159">HDInsight에서 SQL Server에 연결하는 경우 SQL Server의 IP 주소를 사용해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-159">When connecting to the SQL Server from HDInsight, you may have to use the IP address of the SQL Server.</span></span> <span data-ttu-id="d88a6-160">예:</span><span class="sxs-lookup"><span data-stu-id="d88a6-160">For example:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://10.0.1.1:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

## <a name="limitations"></a><span data-ttu-id="d88a6-161">제한 사항</span><span class="sxs-lookup"><span data-stu-id="d88a6-161">Limitations</span></span>

* <span data-ttu-id="d88a6-162">대량 내보내기 - Linux 기반 HDInsight와 함께 Microsoft SQL Server 또는 Azure SQL 데이터베이스에 데이터를 내보내는 데 사용된 Sqoop 커넥터도 현재 대량 삽입을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-162">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>

* <span data-ttu-id="d88a6-163">배치 - Linux 기반 HDInsight에서 삽입을 수행할 때 `-batch` 스위치를 사용하는 경우 Sqoop은 삽입 작업을 일괄 처리하는 대신 여러 번의 삽입 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-163">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop makes multiple inserts instead of batching the insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d88a6-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d88a6-164">Next steps</span></span>

<span data-ttu-id="d88a6-165">이제 Sqoop을 사용하는 방법에 대해 알아봤습니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-165">Now you have learned how to use Sqoop.</span></span> <span data-ttu-id="d88a6-166">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d88a6-166">To learn more, see:</span></span>

* <span data-ttu-id="d88a6-167">[HDInsight와 함께 Oozie 사용][hdinsight-use-oozie]: Oozie 워크플로에서 Sqoop 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-167">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="d88a6-168">[HDInsight를 사용하여 비행 지연 데이터 분석][hdinsight-analyze-flight-data]: Hive를 사용하여 비행 지연 데이터를 분석한 후 Sqoop을 사용하여 데이터를 Azure SQL Database로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-168">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span></span>
* <span data-ttu-id="d88a6-169">[HDInsight에 데이터 업로드][hdinsight-upload-data]: HDInsight/Azure Blob Storage에 데이터를 업로드하는 다른 방법을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d88a6-169">[Upload data to HDInsight][hdinsight-upload-data]: Find other methods for uploading data to HDInsight/Azure Blob storage.</span></span>

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database-create-configure.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
