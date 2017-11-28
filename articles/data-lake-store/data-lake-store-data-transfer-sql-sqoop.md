---
title: "데이터 레이크 저장소와 Sqoop를 사용 하 여 Azure SQL 데이터베이스 간에 데이터 aaaCopy | Microsoft Docs"
description: "Azure SQL 데이터베이스와 데이터 레이크 저장소 Sqoop toocopy 데이터를 사용 하 여"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 3f914b2a-83cc-4950-b3f7-69c921851683
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: f58483455f0ebe9544673a1d5c5884f2721c800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-between-data-lake-store-and-azure-sql-database-using-sqoop"></a><span data-ttu-id="1448b-103">Sqoop를 사용하여 Data Lake 저장소와 Azure SQL 데이터베이스 간에 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="1448b-103">Copy data between Data Lake Store and Azure SQL database using Sqoop</span></span>
<span data-ttu-id="1448b-104">자세한 내용은 방법 간에 Azure SQL 데이터베이스 및 데이터 레이크 저장소 toouse Apache Sqoop tooimport 및 내보내기 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-104">Learn how toouse Apache Sqoop tooimport and export data between Azure SQL Database and Data Lake Store.</span></span>

## <a name="what-is-sqoop"></a><span data-ttu-id="1448b-105">Sqoop 정의</span><span class="sxs-lookup"><span data-stu-id="1448b-105">What is Sqoop?</span></span>
<span data-ttu-id="1448b-106">빅 데이터 응용 프로그램은 로그 및 파일과 같은 비구조적 및 반구조적 데이터를 처리하기 위한 자연스러운 선택입니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-106">Big data applications are a natural choice for processing unstructured and semi-structured data, such as logs and files.</span></span> <span data-ttu-id="1448b-107">그러나 수도 있습니다 관계형 데이터베이스에 저장 된 필요 tooprocess 구조화 된 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-107">However, there may also be a need tooprocess structured data that is stored in relational databases.</span></span>

<span data-ttu-id="1448b-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) 은 설계 된 도구 tootransfer 관계형 데이터베이스와 같은 데이터 레이크 저장소는 빅 데이터 저장소 간에 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) is a tool designed tootransfer data between  relational databases and a big data repository, such as Data Lake Store.</span></span> <span data-ttu-id="1448b-109">데이터 레이크 저장소로 tooimport 데이터 Azure SQL 데이터베이스 같은 관계형 데이터베이스 관리 시스템 RDBMS ()를에서 것 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-109">You can use it tooimport data from a relational database management system (RDBMS) such as Azure SQL Database into Data Lake Store.</span></span> <span data-ttu-id="1448b-110">다음이 변환 하 고 및 빅 데이터 워크 로드를 사용 하 여 hello 데이터를 분석 하 고, 다음 RDBMS에 다시 hello 데이터를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-110">You can then transform and analyze hello data using big data workloads and then export hello data back into an RDBMS.</span></span> <span data-ttu-id="1448b-111">이 자습서에서 관계형 데이터베이스 tooimport/내보내기를으로 Azure SQL 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-111">In this tutorial, you use an Azure SQL Database as your relational database tooimport/export from.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1448b-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1448b-112">Prerequisites</span></span>
<span data-ttu-id="1448b-113">이 문서를 시작 하기 전에 hello 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-113">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="1448b-114">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="1448b-114">**An Azure subscription**.</span></span> <span data-ttu-id="1448b-115">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1448b-115">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="1448b-116">**Azure 데이터 레이크 저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="1448b-116">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="1448b-117">방법에 대 한 지침은 toocreate 하나, 참조 [Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="1448b-117">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="1448b-118">**Azure HDInsight 클러스터** 액세스 tooa 데이터 레이크 저장소 계정 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-118">**Azure HDInsight cluster** with access tooa Data Lake Store account.</span></span> <span data-ttu-id="1448b-119">[Data Lake Store가 있는 HDInsight 클러스터 만들기](data-lake-store-hdinsight-hadoop-use-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1448b-119">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="1448b-120">이 문서에서는 Data Lake 저장소가 있는 HDInsight Linux 클러스터 액세스 권한이 있는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-120">This article assumes you have an HDInsight Linux cluster with Data Lake Store access.</span></span>
* <span data-ttu-id="1448b-121">**Azure SQL 데이터베이스**.</span><span class="sxs-lookup"><span data-stu-id="1448b-121">**Azure SQL Database**.</span></span> <span data-ttu-id="1448b-122">방법에 대 한 지침은 toocreate 하나, 참조 [Azure SQL 데이터베이스 만들기](../sql-database/sql-database-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="1448b-122">For instructions on how toocreate one, see [Create an Azure SQL database](../sql-database/sql-database-get-started.md)</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="1448b-123">비디오로 빠르게 배우시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="1448b-123">Do you learn fast with videos?</span></span>
<span data-ttu-id="1448b-124">[이 비디오를 시청](https://mix.office.com/watch/1butcdjxmu114) 방법에 Azure 저장소 Blob와 DistCp를 사용 하 여 데이터 레이크 저장소 간에 toocopy 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-124">[Watch this video](https://mix.office.com/watch/1butcdjxmu114) on how toocopy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="create-sample-tables-in-hello-azure-sql-database"></a><span data-ttu-id="1448b-125">Hello Azure SQL 데이터베이스에서에서 예제 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="1448b-125">Create sample tables in hello Azure SQL Database</span></span>
1. <span data-ttu-id="1448b-126">toostart는 hello Azure SQL 데이터베이스에에서 두 개의 샘플 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-126">toostart with, create two sample tables in hello Azure SQL Database.</span></span> <span data-ttu-id="1448b-127">사용 하 여 [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) 또는 Visual Studio tooconnect toohello Azure SQL 데이터베이스 실행된 hello 쿼리를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="1448b-127">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio tooconnect toohello Azure SQL Database and then run hello following queries.</span></span>

    <span data-ttu-id="1448b-128">**Table1 만들기**</span><span class="sxs-lookup"><span data-stu-id="1448b-128">**Create Table1**</span></span>

        CREATE TABLE [dbo].[Table1](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO

    <span data-ttu-id="1448b-129">**Table2 만들기**</span><span class="sxs-lookup"><span data-stu-id="1448b-129">**Create Table2**</span></span>

        CREATE TABLE [dbo].[Table2](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO
2. <span data-ttu-id="1448b-130">**Table1**에서 몇 가지 샘플 데이터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-130">In **Table1**, add some sample data.</span></span> <span data-ttu-id="1448b-131">**Table2** 를 빈 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-131">Leave **Table2** empty.</span></span> <span data-ttu-id="1448b-132">**Table1** 에서 Data Lake 저장소로 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-132">We will import data from **Table1** into Data Lake Store.</span></span> <span data-ttu-id="1448b-133">그런 다음 Data Lake 저장소에서 **Table2**로 데이터를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-133">Then, we will export data from Data Lake Store into **Table2**.</span></span> <span data-ttu-id="1448b-134">다음 코드 조각 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-134">Run hello following snippet.</span></span>

        INSERT INTO [dbo].[Table1] VALUES (1,'Neal','Kell'), (2,'Lila','Fulton'), (3, 'Erna','Myers'), (4,'Annette','Simpson');


## <a name="use-sqoop-from-an-hdinsight-cluster-with-access-toodata-lake-store"></a><span data-ttu-id="1448b-135">사용 하는 HDInsight 클러스터에서 사용 하 여 Sqoop tooData 레이크 스토어에 액세스</span><span class="sxs-lookup"><span data-stu-id="1448b-135">Use Sqoop from an HDInsight cluster with access tooData Lake Store</span></span>
<span data-ttu-id="1448b-136">HDInsight 클러스터에 사용할 수 있는 hello Sqoop 패키지에 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-136">An HDInsight cluster already has hello Sqoop packages available.</span></span> <span data-ttu-id="1448b-137">추가 저장소로 hello HDInsight 클러스터 toouse Data Lake 저장소를 구성한 경우 (이 예에서는 Azure SQL 데이터베이스)의 관계형 데이터베이스 간의 구성 변경) (없이 Sqoop tooimport/내보내기 데이터를 사용할 수 있습니다 및 데이터 레이크 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-137">If you have configured hello HDInsight cluster toouse Data Lake Store as an additional storage, you can use Sqoop (without any configuration changes) tooimport/export data between a relational database (in this example, Azure SQL Database) and a Data Lake Store account.</span></span>

1. <span data-ttu-id="1448b-138">이 자습서에서는 SSH tooconnect toohello 클러스터를 사용 해야 하는 Linux 클러스터 만들어지므로 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-138">For this tutorial, we assume you created a Linux cluster so you should use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="1448b-139">참조 [연결 tooa Linux 기반 HDInsight 클러스터](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-139">See [Connect tooa Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
2. <span data-ttu-id="1448b-140">데이터 레이크 저장소 계정 hello hello 클러스터에서 액세스할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-140">Verify whether you can access hello Data Lake Store account from hello cluster.</span></span> <span data-ttu-id="1448b-141">Hello hello SSH 프롬프트에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-141">Run hello following command from hello SSH prompt:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net/

    <span data-ttu-id="1448b-142">이 hello Data Lake 저장소 계정에서에서 파일/폴더의 목록을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-142">This should provide a list of files/folders in hello Data Lake Store account.</span></span>

### <a name="import-data-from-azure-sql-database-into-data-lake-store"></a><span data-ttu-id="1448b-143">Azure SQL 데이터베이스에서 Data Lake 저장소로 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="1448b-143">Import data from Azure SQL Database into Data Lake Store</span></span>
1. <span data-ttu-id="1448b-144">Sqoop 패키지를 사용할 수 있는 toohello 디렉터리를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-144">Navigate toohello directory where Sqoop packages are available.</span></span> <span data-ttu-id="1448b-145">일반적으로 `/usr/hdp/<version>/sqoop/bin`에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-145">Typically, this will be at `/usr/hdp/<version>/sqoop/bin`.</span></span>
2. <span data-ttu-id="1448b-146">Hello 데이터를 가져올 **Table1** hello Data Lake 저장소 계정에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-146">Import hello data from **Table1** into hello Data Lake Store account.</span></span> <span data-ttu-id="1448b-147">구문 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-147">Use hello following syntax:</span></span>

        sqoop-import --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table1 --target-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1

    <span data-ttu-id="1448b-148">**데이터베이스 서버 이름 sql** 자리 표시자 hello Azure SQL 데이터베이스 실행 되 고 있는 hello 서버 hello 이름을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-148">Note that **sql-database-server-name** placeholder represents hello name of hello server where hello Azure SQL database is running.</span></span> <span data-ttu-id="1448b-149">**sql 데이터베이스 이름** 자리 표시자 hello 실제 데이터베이스 이름을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-149">**sql-database-name** placeholder represents hello actual database name.</span></span>

    <span data-ttu-id="1448b-150">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-150">For example,</span></span>


        sqoop-import --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table1 --target-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1

1. <span data-ttu-id="1448b-151">된 데이터는 해당 hello 전송 toohello 데이터 레이크 저장소 계정을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-151">Verify that hello data has been transferred toohello Data Lake Store account.</span></span> <span data-ttu-id="1448b-152">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-152">Run hello following command:</span></span>

        hdfs dfs -ls adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/

    <span data-ttu-id="1448b-153">다음 출력 hello를 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-153">You should see hello following output.</span></span>


        -rwxrwxrwx   0 sshuser hdfs          0 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/_SUCCESS
        -rwxrwxrwx   0 sshuser hdfs         12 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00000
        -rwxrwxrwx   0 sshuser hdfs         14 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00001
        -rwxrwxrwx   0 sshuser hdfs         13 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00002
        -rwxrwxrwx   0 sshuser hdfs         18 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00003

    <span data-ttu-id="1448b-154">각 **파트-m-*** 파일 hello 원본 테이블의 tooa 행은 해당 **Table1**합니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-154">Each **part-m-*** file corresponds tooa row in hello source table, **Table1**.</span></span> <span data-ttu-id="1448b-155">-M-hello 부분의 hello 내용을 볼 수 * tooverify 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-155">You can view hello contents of hello part-m-* files tooverify.</span></span>


### <a name="export-data-from-data-lake-store-into-azure-sql-database"></a><span data-ttu-id="1448b-156">Data Lake 저장소에서 Azure SQL 데이터베이스로 데이터 내보내기</span><span class="sxs-lookup"><span data-stu-id="1448b-156">Export data from Data Lake Store into Azure SQL Database</span></span>
1. <span data-ttu-id="1448b-157">데이터 레이크 저장소 계정 toohello 빈 테이블을에서 hello 데이터 내보내기 **Table2**, hello Azure SQL 데이터베이스에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-157">Export hello data from Data Lake Store account toohello empty table, **Table2**, in hello Azure SQL Database.</span></span> <span data-ttu-id="1448b-158">구문 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-158">Use hello following syntax.</span></span>

        sqoop-export --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table2 --export-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

    <span data-ttu-id="1448b-159">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-159">For example,</span></span>


        sqoop-export --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table2 --export-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

1. <span data-ttu-id="1448b-160">데이터를 해당 hello 업로드 toohello SQL 데이터베이스 테이블을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-160">Verify that hello data was uploaded toohello SQL Database table.</span></span> <span data-ttu-id="1448b-161">사용 하 여 [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) 또는 Visual Studio tooconnect toohello Azure SQL 데이터베이스 누른 실행된 hello 다음 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-161">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio tooconnect toohello Azure SQL Database and then run hello following query.</span></span>

        SELECT * FROM TABLE2

    <span data-ttu-id="1448b-162">이 출력을 따라 hello가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-162">This should have hello following output.</span></span>

         ID  FName   LName
        ------------------
        1    Neal    Kell
        2    Lila    Fulton
        3    Erna    Myers
        4    Annette    Simpson

## <a name="performance-considerations-while-using-sqoop"></a><span data-ttu-id="1448b-163">Sqoop 사용에 대한 성능 고려 사항</span><span class="sxs-lookup"><span data-stu-id="1448b-163">Performance considerations while using Sqoop</span></span>

<span data-ttu-id="1448b-164">성능 튜닝에 Sqoop 작업 toocopy 데이터 tooData 레이크 저장소, 참조 [Sqoop 성능 문서](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/)합니다.</span><span class="sxs-lookup"><span data-stu-id="1448b-164">For performance tuning your Sqoop job toocopy data tooData Lake Store, see [Sqoop performance document](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span></span>

## <a name="see-also"></a><span data-ttu-id="1448b-165">참고 항목</span><span class="sxs-lookup"><span data-stu-id="1448b-165">See also</span></span>
* [<span data-ttu-id="1448b-166">Azure 저장소 Blob tooData Lake 저장소에서 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="1448b-166">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="1448b-167">데이터 레이크 저장소의 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="1448b-167">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="1448b-168">Azure 데이터 레이크 분석에 데이터 레이크 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="1448b-168">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="1448b-169">Azure HDInsight에 데이터 레이크 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="1448b-169">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
