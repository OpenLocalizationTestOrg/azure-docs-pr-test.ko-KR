---
title: "Sqoop를 사용하여 Data Lake Store와 Azure SQL 데이터베이스 간에 데이터 복사 | Microsoft 문서"
description: "Sqoop를 사용하여 Azure SQL 데이터베이스와 Data Lake 저장소 간에 데이터 복사"
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
ms.openlocfilehash: 53bf33f6027f1f365bd92251490d5c851fb83f8b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="copy-data-between-data-lake-store-and-azure-sql-database-using-sqoop"></a><span data-ttu-id="c9272-103">Sqoop를 사용하여 Data Lake 저장소와 Azure SQL 데이터베이스 간에 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="c9272-103">Copy data between Data Lake Store and Azure SQL database using Sqoop</span></span>
<span data-ttu-id="c9272-104">Apache Sqoop를 사용하여 Azure SQL 데이터베이스와 Data Lake 저장소 간에 데이터를 가져오고 내보내는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-104">Learn how to use Apache Sqoop to import and export data between Azure SQL Database and Data Lake Store.</span></span>

## <a name="what-is-sqoop"></a><span data-ttu-id="c9272-105">Sqoop 정의</span><span class="sxs-lookup"><span data-stu-id="c9272-105">What is Sqoop?</span></span>
<span data-ttu-id="c9272-106">빅 데이터 응용 프로그램은 로그 및 파일과 같은 비구조적 및 반구조적 데이터를 처리하기 위한 자연스러운 선택입니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-106">Big data applications are a natural choice for processing unstructured and semi-structured data, such as logs and files.</span></span> <span data-ttu-id="c9272-107">그러나 관계형 데이터베이스에 저장된 구조적 데이터를 처리해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-107">However, there may also be a need to process structured data that is stored in relational databases.</span></span>

<span data-ttu-id="c9272-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html)는 Data Lake Store와 같은 빅 데이터 리포지토리와 관계형 데이터베이스 간에 데이터를 전송하도록 설계된 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) is a tool designed to transfer data between  relational databases and a big data repository, such as Data Lake Store.</span></span> <span data-ttu-id="c9272-109">이 도구를 사용하여 Azure SQL 데이터베이스와 같은 RDBMS(관계형 데이터베이스 관리 시스템)에서 Data Lake 저장소로 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-109">You can use it to import data from a relational database management system (RDBMS) such as Azure SQL Database into Data Lake Store.</span></span> <span data-ttu-id="c9272-110">그런 다음 빅 데이터 워크로드를 사용하여 데이터를 변환 및 분석한 후 RDBMS로 다시 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-110">You can then transform and analyze the data using big data workloads and then export the data back into an RDBMS.</span></span> <span data-ttu-id="c9272-111">이 자습서에서는 Azure SQL 데이터베이스를 관계형 데이터베이스로 사용하여 데이터를 가져오고 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-111">In this tutorial, you use an Azure SQL Database as your relational database to import/export from.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9272-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c9272-112">Prerequisites</span></span>
<span data-ttu-id="c9272-113">이 문서를 시작하기 전에 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-113">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="c9272-114">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="c9272-114">**An Azure subscription**.</span></span> <span data-ttu-id="c9272-115">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9272-115">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="c9272-116">**Azure 데이터 레이크 저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="c9272-116">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="c9272-117">만드는 방법에 대한 지침은 [Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="c9272-117">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="c9272-118">**Azure HDInsight 클러스터** 입니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-118">**Azure HDInsight cluster** with access to a Data Lake Store account.</span></span> <span data-ttu-id="c9272-119">[Data Lake 저장소가 있는 HDInsight 클러스터 만들기](data-lake-store-hdinsight-hadoop-use-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9272-119">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="c9272-120">이 문서에서는 Data Lake 저장소가 있는 HDInsight Linux 클러스터 액세스 권한이 있는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-120">This article assumes you have an HDInsight Linux cluster with Data Lake Store access.</span></span>
* <span data-ttu-id="c9272-121">**Azure SQL 데이터베이스**.</span><span class="sxs-lookup"><span data-stu-id="c9272-121">**Azure SQL Database**.</span></span> <span data-ttu-id="c9272-122">데이터베이스를 만드는 방법에 대한 지침은 [Azure SQL 데이터베이스 만들기](../sql-database/sql-database-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="c9272-122">For instructions on how to create one, see [Create an Azure SQL database](../sql-database/sql-database-get-started.md)</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="c9272-123">비디오로 빠르게 배우시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="c9272-123">Do you learn fast with videos?</span></span>
<span data-ttu-id="c9272-124">[비디오를 보세요](https://mix.office.com/watch/1butcdjxmu114) .</span><span class="sxs-lookup"><span data-stu-id="c9272-124">[Watch this video](https://mix.office.com/watch/1butcdjxmu114) on how to copy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="create-sample-tables-in-the-azure-sql-database"></a><span data-ttu-id="c9272-125">Azure SQL 데이터베이스에서 샘플 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="c9272-125">Create sample tables in the Azure SQL Database</span></span>
1. <span data-ttu-id="c9272-126">시작하려면 Azure SQL 데이터베이스에서 두 개의 샘플 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-126">To start with, create two sample tables in the Azure SQL Database.</span></span> <span data-ttu-id="c9272-127">[SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) 또는 Visual Studio를 사용하여 Azure SQL 데이터베이스에 연결한 후 다음 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-127">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio to connect to the Azure SQL Database and then run the following queries.</span></span>

    <span data-ttu-id="c9272-128">**Table1 만들기**</span><span class="sxs-lookup"><span data-stu-id="c9272-128">**Create Table1**</span></span>

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

    <span data-ttu-id="c9272-129">**Table2 만들기**</span><span class="sxs-lookup"><span data-stu-id="c9272-129">**Create Table2**</span></span>

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
2. <span data-ttu-id="c9272-130">**Table1**에서 몇 가지 샘플 데이터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-130">In **Table1**, add some sample data.</span></span> <span data-ttu-id="c9272-131">**Table2** 를 빈 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-131">Leave **Table2** empty.</span></span> <span data-ttu-id="c9272-132">**Table1** 에서 Data Lake 저장소로 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-132">We will import data from **Table1** into Data Lake Store.</span></span> <span data-ttu-id="c9272-133">그런 다음 Data Lake 저장소에서 **Table2**로 데이터를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-133">Then, we will export data from Data Lake Store into **Table2**.</span></span> <span data-ttu-id="c9272-134">다음 조각을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-134">Run the following snippet.</span></span>

        INSERT INTO [dbo].[Table1] VALUES (1,'Neal','Kell'), (2,'Lila','Fulton'), (3, 'Erna','Myers'), (4,'Annette','Simpson');


## <a name="use-sqoop-from-an-hdinsight-cluster-with-access-to-data-lake-store"></a><span data-ttu-id="c9272-135">Data Lake 저장소 계정에 액세스할 수 있는 HDInsight 클러스터에서 Sqoop를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-135">Use Sqoop from an HDInsight cluster with access to Data Lake Store</span></span>
<span data-ttu-id="c9272-136">HDInsight 클러스터에는 사용 가능한 Sqoop 패키지가 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-136">An HDInsight cluster already has the Sqoop packages available.</span></span> <span data-ttu-id="c9272-137">Data Lake 저장소를 추가 저장소로 사용하도록 HDInsight 클러스터를 구성한 경우 Sqoop(구성 변경 없이)를 사용하여 관계형 데이터베이스(이 예제의 경우 Azure SQL 데이터베이스)와 Data Lake 저장소 계정 간에 데이터를 가져오고 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-137">If you have configured the HDInsight cluster to use Data Lake Store as an additional storage, you can use Sqoop (without any configuration changes) to import/export data between a relational database (in this example, Azure SQL Database) and a Data Lake Store account.</span></span>

1. <span data-ttu-id="c9272-138">이 자습서에서는 Linux 클러스터를 만든 것으로 가정하므로 SSH를 사용하여 클러스터에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-138">For this tutorial, we assume you created a Linux cluster so you should use SSH to connect to the cluster.</span></span> <span data-ttu-id="c9272-139">[Linux 기반 HDInsight 클러스터에 연결](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9272-139">See [Connect to a Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
2. <span data-ttu-id="c9272-140">클러스터에서 Data Lake 저장소 계정에 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-140">Verify whether you can access the Data Lake Store account from the cluster.</span></span> <span data-ttu-id="c9272-141">SSH 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-141">Run the following command from the SSH prompt:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net/

    <span data-ttu-id="c9272-142">데이터 레이크 저장소 계정의 파일/폴더 목록이 제공되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-142">This should provide a list of files/folders in the Data Lake Store account.</span></span>

### <a name="import-data-from-azure-sql-database-into-data-lake-store"></a><span data-ttu-id="c9272-143">Azure SQL 데이터베이스에서 Data Lake 저장소로 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="c9272-143">Import data from Azure SQL Database into Data Lake Store</span></span>
1. <span data-ttu-id="c9272-144">Sqoop 패키지를 사용할 수 있는 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-144">Navigate to the directory where Sqoop packages are available.</span></span> <span data-ttu-id="c9272-145">일반적으로 `/usr/hdp/<version>/sqoop/bin`에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-145">Typically, this will be at `/usr/hdp/<version>/sqoop/bin`.</span></span>
2. <span data-ttu-id="c9272-146">**Table1** 에서 Data Lake 저장소 계정으로 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-146">Import the data from **Table1** into the Data Lake Store account.</span></span> <span data-ttu-id="c9272-147">다음 구문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-147">Use the following syntax:</span></span>

        sqoop-import --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table1 --target-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1

    <span data-ttu-id="c9272-148">**sql-database-server-name** 자리 표시자는 Azure SQL 데이터베이스가 실행 중인 서버의 이름을 나타내고,</span><span class="sxs-lookup"><span data-stu-id="c9272-148">Note that **sql-database-server-name** placeholder represents the name of the server where the Azure SQL database is running.</span></span> <span data-ttu-id="c9272-149">**sql-database-name** 자리 표시자는 실제 데이터베이스 이름을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-149">**sql-database-name** placeholder represents the actual database name.</span></span>

    <span data-ttu-id="c9272-150">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-150">For example,</span></span>


        sqoop-import --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table1 --target-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1

1. <span data-ttu-id="c9272-151">데이터가 Data Lake 저장소 계정으로 전송되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-151">Verify that the data has been transferred to the Data Lake Store account.</span></span> <span data-ttu-id="c9272-152">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-152">Run the following command:</span></span>

        hdfs dfs -ls adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/

    <span data-ttu-id="c9272-153">다음 출력이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-153">You should see the following output.</span></span>


        -rwxrwxrwx   0 sshuser hdfs          0 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/_SUCCESS
        -rwxrwxrwx   0 sshuser hdfs         12 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00000
        -rwxrwxrwx   0 sshuser hdfs         14 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00001
        -rwxrwxrwx   0 sshuser hdfs         13 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00002
        -rwxrwxrwx   0 sshuser hdfs         18 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00003

    <span data-ttu-id="c9272-154">각 **part-m-*** 파일은 **Table1** 원본 테이블의 행에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-154">Each **part-m-*** file corresponds to a row in the source table, **Table1**.</span></span> <span data-ttu-id="c9272-155">확인할 part-m-* 파일의 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-155">You can view the contents of the part-m-* files to verify.</span></span>


### <a name="export-data-from-data-lake-store-into-azure-sql-database"></a><span data-ttu-id="c9272-156">Data Lake 저장소에서 Azure SQL 데이터베이스로 데이터 내보내기</span><span class="sxs-lookup"><span data-stu-id="c9272-156">Export data from Data Lake Store into Azure SQL Database</span></span>
1. <span data-ttu-id="c9272-157">Data Lake Store 계정에서 Azure SQL 데이터베이스의 빈 테이블 **Table2**로 데이터를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-157">Export the data from Data Lake Store account to the empty table, **Table2**, in the Azure SQL Database.</span></span> <span data-ttu-id="c9272-158">다음 구문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-158">Use the following syntax.</span></span>

        sqoop-export --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table2 --export-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

    <span data-ttu-id="c9272-159">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-159">For example,</span></span>


        sqoop-export --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table2 --export-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

1. <span data-ttu-id="c9272-160">데이터가 SQL 데이터베이스 테이블에 업로드되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-160">Verify that the data was uploaded to the SQL Database table.</span></span> <span data-ttu-id="c9272-161">[SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) 또는 Visual Studio를 사용하여 Azure SQL 데이터베이스에 연결한 후 다음 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-161">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio to connect to the Azure SQL Database and then run the following query.</span></span>

        SELECT * FROM TABLE2

    <span data-ttu-id="c9272-162">다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9272-162">This should have the following output.</span></span>

         ID  FName   LName
        ------------------
        1    Neal    Kell
        2    Lila    Fulton
        3    Erna    Myers
        4    Annette    Simpson

## <a name="performance-considerations-while-using-sqoop"></a><span data-ttu-id="c9272-163">Sqoop 사용에 대한 성능 고려 사항</span><span class="sxs-lookup"><span data-stu-id="c9272-163">Performance considerations while using Sqoop</span></span>

<span data-ttu-id="c9272-164">Data Lake 저장소에 데이터를 복사하기 위한 Sqoop 작업을 조정하는 성능은 [Sqoop 성능 문서](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9272-164">For performance tuning your Sqoop job to copy data to Data Lake Store, see [Sqoop performance document](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span></span>

## <a name="see-also"></a><span data-ttu-id="c9272-165">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c9272-165">See also</span></span>
* [<span data-ttu-id="c9272-166">Azure 저장소 Blob에서 데이터 레이크 저장소로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="c9272-166">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="c9272-167">데이터 레이크 저장소의 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="c9272-167">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="c9272-168">Azure 데이터 레이크 분석에 데이터 레이크 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="c9272-168">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="c9272-169">Azure HDInsight에 데이터 레이크 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="c9272-169">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
