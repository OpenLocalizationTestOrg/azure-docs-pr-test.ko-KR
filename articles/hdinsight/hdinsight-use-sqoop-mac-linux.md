---
title: "Azure HDInsight에서 Hadoop으로 Sqoop aaaApache | Microsoft Docs"
description: "자세한 내용은 방법 toouse Apache Sqoop tooimport 및 HDInsight의 Hadoop 및 Azure SQL 데이터베이스 간의 내보내기."
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
ms.openlocfilehash: b256285659bbcf18ff05e220ccdf51c21eb8fbf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-sqoop-tooimport-and-export-data-between-hadoop-on-hdinsight-and-sql-database"></a><span data-ttu-id="59625-104">HDInsight에서 Hadoop 및 SQL 데이터베이스 간에 데이터를 내보내고 Apache Sqoop tooimport를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="59625-104">Use Apache Sqoop tooimport and export data between Hadoop on HDInsight and SQL Database</span></span>

[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="59625-105">Azure HDInsight 및 Azure SQL 데이터베이스 또는 Microsoft SQL Server 데이터베이스에 있는 클러스터 toouse Apache Sqoop tooimport 및 Hadoop 간에 내보내기에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="59625-105">Learn how toouse Apache Sqoop tooimport and export between a Hadoop cluster in Azure HDInsight and Azure SQL Database or Microsoft SQL Server database.</span></span> <span data-ttu-id="59625-106">이 문서 사용 하 여 hello에서 단계를 hello `sqoop` hello Hadoop 클러스터의 헤드 노드에 hello에서 직접 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="59625-106">hello steps in this document use hello `sqoop` command directly from hello headnode of hello Hadoop cluster.</span></span> <span data-ttu-id="59625-107">SSH tooconnect toohello 헤드 노드를 사용 하 고이 문서에서 hello 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="59625-107">You use SSH tooconnect toohello head node and run hello commands in this document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="59625-108">hello이 문서의 단계 에서만 사용 가능 Linux를 사용 하는 HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="59625-108">hello steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="59625-109">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="59625-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="59625-110">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59625-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="install-freetds"></a><span data-ttu-id="59625-111">FreeTDS 설치</span><span class="sxs-lookup"><span data-stu-id="59625-111">Install FreeTDS</span></span>

1. <span data-ttu-id="59625-112">SSH tooconnect toohello HDInsight 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="59625-112">Use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="59625-113">다음 명령을 hello 라는 클러스터의 toohello 기본 헤드 노드에 연결 하는 예를 들어 `mycluster`:</span><span class="sxs-lookup"><span data-stu-id="59625-113">For example, hello following command connects toohello primary headnode of a cluster named `mycluster`:</span></span>

    ```bash
    ssh CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="59625-114">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59625-114">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="59625-115">다음 명령은 tooinstall FreeTDS hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="59625-115">Use hello following command tooinstall FreeTDS:</span></span>

    ```bash
    sudo apt --assume-yes install freetds-dev freetds-bin
    ```

    <span data-ttu-id="59625-116">FreeTDS 몇 가지 단계 tooconnect tooSQL 데이터베이스에에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59625-116">FreeTDS is used in several steps tooconnect tooSQL Database.</span></span>

## <a name="create-hello-table-in-sql-database"></a><span data-ttu-id="59625-117">SQL 데이터베이스에 hello 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="59625-117">Create hello table in SQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="59625-118">SQL 데이터베이스에서 만든 및 hello HDInsight 클러스터를 사용 하는 경우 [클러스터 및 SQL 데이터베이스 만들기](hdinsight-use-sqoop.md), hello이이 섹션의에서 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="59625-118">If you are using hello HDInsight cluster and SQL Database created in [Create cluster and SQL database](hdinsight-use-sqoop.md), skip hello steps in this section.</span></span> <span data-ttu-id="59625-119">hello 데이터베이스 및 테이블 생성 된 hello에 hello의 일부 단계 [클러스터 및 SQL 데이터베이스 만들기](hdinsight-use-sqoop.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="59625-119">hello database and table were created as part of hello steps in hello [Create cluster and SQL database](hdinsight-use-sqoop.md) document.</span></span>

1. <span data-ttu-id="59625-120">Hello SSH 세션에서 다음 명령을 tooconnect toohello SQL 데이터베이스 서버 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="59625-120">From hello SSH session, use hello following command tooconnect toohello SQL Database server.</span></span>

        TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D sqooptest

    <span data-ttu-id="59625-121">텍스트 다음 출력 유사한 toohello를 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="59625-121">You receive output similar toohello following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toosqooptest
        1>

2. <span data-ttu-id="59625-122">Hello에 `1>` hello 다음 쿼리를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="59625-122">At hello `1>` prompt, enter hello following query:</span></span>

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

    <span data-ttu-id="59625-123">Hello 때 `GO` hello 이전 문이 계산을 문을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="59625-123">When hello `GO` statement is entered, hello previous statements are evaluated.</span></span> <span data-ttu-id="59625-124">첫째, hello **mobiledata** 테이블을 만든 다음 클러스터형된 인덱스 (SQL 데이터베이스에 필요). tooit 추가</span><span class="sxs-lookup"><span data-stu-id="59625-124">First, hello **mobiledata** table is created, then a clustered index is added tooit (required by SQL Database.)</span></span>

    <span data-ttu-id="59625-125">다음 테이블 hello 쿼리 tooverify 사용 하 여 hello가 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="59625-125">Use hello following query tooverify that hello table has been created:</span></span>

    ```sql
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="59625-126">텍스트 다음 출력 유사한 toohello를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59625-126">You see output similar toohello following text:</span></span>

        TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
        sqooptest       dbo     mobiledata      BASE TABLE

3. <span data-ttu-id="59625-127">입력 `exit` hello에 `1>` tooexit hello tsql 유틸리티 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="59625-127">Enter `exit` at hello `1>` prompt tooexit hello tsql utility.</span></span>

## <a name="sqoop-export"></a><span data-ttu-id="59625-128">Sqoop 내보내기</span><span class="sxs-lookup"><span data-stu-id="59625-128">Sqoop export</span></span>

1. <span data-ttu-id="59625-129">Hello SSH 연결 toohello 클러스터에서 사용 하 여 hello 다음 명령 수 tooverify Sqoop SQL 데이터베이스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59625-129">From hello SSH connection toohello cluster, use hello following command tooverify that Sqoop can see your SQL Database:</span></span>

    ```bash
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> -P
    ```
    <span data-ttu-id="59625-130">메시지가 표시 되 면 hello SQL 데이터베이스 로그인에 대 한 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="59625-130">When prompted, enter hello password for hello SQL Database login.</span></span>

    <span data-ttu-id="59625-131">이 명령은 hello 등 데이터베이스의 목록을 반환 **sqooptest** 앞에서 만든 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="59625-131">This command returns a list of databases, including hello **sqooptest** database that you created earlier.</span></span>

2. <span data-ttu-id="59625-132">tooexport 데이터로 **hivesampletable** toohello **mobiledata** 테이블에서 다음 명령을 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="59625-132">tooexport data from **hivesampletable** toohello **mobiledata** table, use hello following command:</span></span>

    ```bash
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> -P --table 'mobiledata' --export-dir 'wasb:///hive/warehouse/hivesampletable' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="59625-133">이 명령은 지시 Sqoop tooconnect toohello **sqooptest** 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="59625-133">This command instructs Sqoop tooconnect toohello **sqooptest** database.</span></span> <span data-ttu-id="59625-134">데이터를 내보내므로 Sqoop **wasb: / / / hive/웨어하우스/hivesampletable** toohello **mobiledata** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="59625-134">Sqoop then exports data from **wasb:///hive/warehouse/hivesampletable** toohello **mobiledata** table.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="59625-135">사용 하 여 `wasb:///` hello 기본 저장소 클러스터에 Azure 저장소 계정이 면 합니다.</span><span class="sxs-lookup"><span data-stu-id="59625-135">Use `wasb:///` if hello default storage for your cluster is an Azure Storage account.</span></span> <span data-ttu-id="59625-136">Azure Data Lake Store이면 `adl:///`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59625-136">Use `adl:///` if it is an Azure Data Lake Store.</span></span>

3. <span data-ttu-id="59625-137">Hello 명령이 완료 된 후 다음 TSQL를 사용 하 여 명령 tooconnect toohello 데이터베이스 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="59625-137">After hello command completes, use hello following command tooconnect toohello database using TSQL:</span></span>

    ```bash
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P -p 1433 -D sqooptest
    ```

    <span data-ttu-id="59625-138">다음 데이터 hello 문을 tooverify 사용 하 여 hello 내보낸된 toohello가 연결 되 면 **mobiledata** 테이블:</span><span class="sxs-lookup"><span data-stu-id="59625-138">Once connected, use hello following statements tooverify that hello data was exported toohello **mobiledata** table:</span></span>

    ```sql
    SET ROWCOUNT 50;
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="59625-139">Hello 테이블의에서 데이터를 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59625-139">You should see a listing of data in hello table.</span></span> <span data-ttu-id="59625-140">형식 `exit` tooexit hello tsql 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="59625-140">Type `exit` tooexit hello tsql utility.</span></span>

## <a name="sqoop-import"></a><span data-ttu-id="59625-141">Sqoop 가져오기</span><span class="sxs-lookup"><span data-stu-id="59625-141">Sqoop import</span></span>

1. <span data-ttu-id="59625-142">사용 하 여 hello 다음 명령은 tooimport 데이터로 hello **mobiledata** toohello SQL 데이터베이스의 테이블 **wasb: / / / 자습서/usesqoop/importeddata** 디렉터리 HDInsight에:</span><span class="sxs-lookup"><span data-stu-id="59625-142">Use hello following command tooimport data from hello **mobiledata** table in SQL Database, toohello **wasb:///tutorials/usesqoop/importeddata** directory on HDInsight:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

    <span data-ttu-id="59625-143">hello 데이터의 hello 필드는 탭 문자로 구분 하 고 hello 줄 새 줄 문자로 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59625-143">hello fields in hello data are separated by a tab character, and hello lines are terminated by a new-line character.</span></span>

2. <span data-ttu-id="59625-144">Hello 가져오기 완료 되 면 다음 명령 toolist hello 데이터 hello 새 디렉터리를으로 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="59625-144">Once hello import has completed, use hello following command toolist out hello data in hello new directory:</span></span>

    ```bash
    hdfs dfs -text /tutorials/usesqoop/importeddata/part-m-00000
    ```

## <a name="using-sql-server"></a><span data-ttu-id="59625-145">SQL Server 사용하기</span><span class="sxs-lookup"><span data-stu-id="59625-145">Using SQL Server</span></span>

<span data-ttu-id="59625-146">Sqoop tooimport를 사용 하 고 데이터 센터 또는 Azure에서 호스팅되는 가상 컴퓨터에서 SQL Server에서 데이터를 내보낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59625-146">You can also use Sqoop tooimport and export data from SQL Server, either in your data center or on a Virtual Machine hosted in Azure.</span></span> <span data-ttu-id="59625-147">SQL 데이터베이스 및 SQL Server를 사용 하 여 hello 차이점은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="59625-147">hello differences between using SQL Database and SQL Server are:</span></span>

* <span data-ttu-id="59625-148">HDInsight와 SQL Server 해야 수에 hello 동일한 Azure 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="59625-148">Both HDInsight and SQL Server must be on hello same Azure Virtual Network.</span></span>

    <span data-ttu-id="59625-149">예를 들어 참조 hello [HDInsight 연결 tooyour 온-프레미스 네트워크](./connect-on-premises-network.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="59625-149">For an example, see hello [Connect HDInsight tooyour on-premises network](./connect-on-premises-network.md) document.</span></span>

    <span data-ttu-id="59625-150">HDInsight를 사용 하 여 Azure 가상 네트워크와에 자세한 내용은 참조 hello [Azure 가상 네트워크와 확장 HDInsight](hdinsight-extend-hadoop-virtual-network.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="59625-150">For more information on using HDInsight with an Azure Virtual Network, see hello [Extend HDInsight with Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span> <span data-ttu-id="59625-151">Azure 가상 네트워크에 대 한 자세한 내용은 참조 hello [가상 네트워크 개요](../virtual-network/virtual-networks-overview.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="59625-151">For more information on Azure Virtual Network, see hello [Virtual Network Overview](../virtual-network/virtual-networks-overview.md) document.</span></span>

* <span data-ttu-id="59625-152">SQL Server 구성된 tooallow SQL 인증 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59625-152">SQL Server must be configured tooallow SQL authentication.</span></span> <span data-ttu-id="59625-153">자세한 내용은 참조 hello [인증 모드 선택](https://msdn.microsoft.com/ms144284.aspx) 문서.</span><span class="sxs-lookup"><span data-stu-id="59625-153">For more information, see hello [Choose an Authentication Mode](https://msdn.microsoft.com/ms144284.aspx) document.</span></span>

* <span data-ttu-id="59625-154">Tooconfigure SQL Server tooaccept 원격 연결을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59625-154">You may have tooconfigure SQL Server tooaccept remote connections.</span></span> <span data-ttu-id="59625-155">자세한 내용은 참조 hello [어떻게 tootroubleshoot 연결 toohello SQL Server 데이터베이스 엔진](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) 문서.</span><span class="sxs-lookup"><span data-stu-id="59625-155">For more information, see hello [How tootroubleshoot connecting toohello SQL Server database engine](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) document.</span></span>

* <span data-ttu-id="59625-156">Hello 만들기 **sqooptest** 와 같은 유틸리티를 사용 하 여 SQL Server의 데이터베이스 **SQL Server Management Studio** 또는 **tsql**합니다.</span><span class="sxs-lookup"><span data-stu-id="59625-156">Create hello **sqooptest** database in SQL Server using a utility such as **SQL Server Management Studio** or **tsql**.</span></span> <span data-ttu-id="59625-157">Azure SQL 데이터베이스에 대 한 hello Azure CLI를 사용 하 여 hello 단계 에서만 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="59625-157">hello steps for using hello Azure CLI only work for Azure SQL Database.</span></span>

    <span data-ttu-id="59625-158">다음 TRANSACT-SQL 문을 toocreate hello 사용 하 여 hello **mobiledata** 테이블:</span><span class="sxs-lookup"><span data-stu-id="59625-158">Use hello following Transact-SQL statements toocreate hello **mobiledata** table:</span></span>

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

* <span data-ttu-id="59625-159">SQL Server toohello을 HDInsight에서 연결할 때에 hello SQL Server의 toouse hello IP 주소를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59625-159">When connecting toohello SQL Server from HDInsight, you may have toouse hello IP address of hello SQL Server.</span></span> <span data-ttu-id="59625-160">예:</span><span class="sxs-lookup"><span data-stu-id="59625-160">For example:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://10.0.1.1:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

## <a name="limitations"></a><span data-ttu-id="59625-161">제한 사항</span><span class="sxs-lookup"><span data-stu-id="59625-161">Limitations</span></span>

* <span data-ttu-id="59625-162">대량 내보내기-와 Linux 기반 HDInsight, hello Sqoop 사용 커넥터 tooexport 데이터 tooMicrosoft SQL Server 또는 Azure SQL 데이터베이스 현재 대량 삽입을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="59625-162">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>

* <span data-ttu-id="59625-163">일괄 처리-Linux 기반 HDInsight와 hello를 사용 하는 경우 `-batch` 삽입 수행 시 전환, Sqoop hello 삽입 작업을 일괄 처리 하는 대신 여러 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="59625-163">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop makes multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59625-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="59625-164">Next steps</span></span>

<span data-ttu-id="59625-165">파악 했으므로 이제 어떻게 toouse Sqoop 합니다.</span><span class="sxs-lookup"><span data-stu-id="59625-165">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="59625-166">toolearn 더 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="59625-166">toolearn more, see:</span></span>

* <span data-ttu-id="59625-167">[HDInsight와 함께 Oozie 사용][hdinsight-use-oozie]: Oozie 워크플로에서 Sqoop 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59625-167">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="59625-168">[HDInsight를 사용 하 여 비행 연착 데이터를 분석][hdinsight-analyze-flight-data]: tooanalyze 비행 하이브 사용 하 여 데이터를 지연 하 고 다음 Sqoop tooexport 데이터 tooan Azure SQL 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="59625-168">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="59625-169">[데이터 tooHDInsight 업로드][hdinsight-upload-data]: 데이터 tooHDInsight/Azure Blob 저장소에 업로드 하기 위한 다른 방법을 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59625-169">[Upload data tooHDInsight][hdinsight-upload-data]: Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

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
