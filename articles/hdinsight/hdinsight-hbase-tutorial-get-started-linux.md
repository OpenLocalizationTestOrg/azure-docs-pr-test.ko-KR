---
title: "HDInsight에서 HBase 예제 시작 - Azure | Microsoft Docs"
description: "이 Apache HBase 예제에 따라 HDInsight에서 hadoop 사용을 시작합니다. HBase 셸에서 테이블을 만들고 Hive를 사용하여 쿼리합니다."
keywords: "hbasecommand, hbase 예제"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 4d6a2658-6b19-4268-95ee-822890f5a33a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: bbd8a838062795ee03ae02dc5e3fd45d841a6e17
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-an-apache-hbase-example-in-hdinsight"></a><span data-ttu-id="b5eec-105">HDInsight에서 Apache HBase 예제 시작</span><span class="sxs-lookup"><span data-stu-id="b5eec-105">Get started with an Apache HBase example in HDInsight</span></span>

<span data-ttu-id="b5eec-106">HDInsight에서 HBase 클러스터를 만들고, HBase 테이블을 만들고 Hive를 사용하여 테이블을 쿼리하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-106">Learn how to create an HBase cluster in HDInsight, create HBase tables, and query tables by using Hive.</span></span> <span data-ttu-id="b5eec-107">일반 HBase 정보는 [HDInsight HBase 개요][hdinsight-hbase-overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b5eec-107">For general HBase information, see [HDInsight HBase overview][hdinsight-hbase-overview].</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a><span data-ttu-id="b5eec-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b5eec-108">Prerequisites</span></span>
<span data-ttu-id="b5eec-109">이 HBase 예제를 시작하기 전에 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-109">Before you begin trying this HBase example, you must have the following items:</span></span>

* <span data-ttu-id="b5eec-110">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="b5eec-110">**An Azure subscription**.</span></span> <span data-ttu-id="b5eec-111">[Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b5eec-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="b5eec-112">[SSH(Secure Shell)](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="b5eec-112">[Secure Shell(SSH)](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> 
* <span data-ttu-id="b5eec-113">[curl](http://curl.haxx.se/download.html).</span><span class="sxs-lookup"><span data-stu-id="b5eec-113">[curl](http://curl.haxx.se/download.html).</span></span>

## <a name="create-hbase-cluster"></a><span data-ttu-id="b5eec-114">HBase 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="b5eec-114">Create HBase cluster</span></span>
<span data-ttu-id="b5eec-115">다음 절차에서는 Azure Resource Manager 템플릿을 사용하여 버전 3.4 HBase Linux 기반 클러스터 및 종속된 기본 Azure Storage 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-115">The following procedure uses an Azure Resource Manager template to create a version 3.4 Linux-based HBase cluster and the dependent default Azure Storage account.</span></span> <span data-ttu-id="b5eec-116">절차에 사용되는 매개 변수와 다른 클러스터 생성 메서드를 이해하려면 [HDInsight에서 Linux 기반 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b5eec-116">To understand the parameters used in the procedure and other cluster creation methods, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="b5eec-117">Azure 포털에서 템플릿을 열려면 다음 이미지를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-117">Click the following image to open the template in the Azure portal.</span></span> <span data-ttu-id="b5eec-118">템플릿은 공용 Blob 컨테이너에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-118">The template is located in a public blob container.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-tutorial-get-started-linux/deploy-to-azure.png" alt="Deploy to Azure"></a>
2. <span data-ttu-id="b5eec-119">**사용자 지정 배포** 블레이드에서 다음 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-119">From the **Custom deployment** blade, enter the following values:</span></span>
   
   * <span data-ttu-id="b5eec-120">**구독**: 클러스터를 만드는 데 사용할 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-120">**Subscription**: Select your Azure subscription that is used to create the cluster.</span></span>
   * <span data-ttu-id="b5eec-121">**리소스 그룹**: Azure 리소스 관리 그룹을 만들거나 기존 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-121">**Resource group**: Create an Azure Resource Management group or use an existing one.</span></span>
   * <span data-ttu-id="b5eec-122">**위치**: 리소스 그룹의 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-122">**Location**: Specify the location of the resource group.</span></span> 
   * <span data-ttu-id="b5eec-123">**클러스터 이름**: HBase 클러스터의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-123">**ClusterName**: Enter a name for the HBase cluster.</span></span>
   * <span data-ttu-id="b5eec-124">**클러스터 로그인 이름 및 암호**: 기본 로그인 이름은 **admin**입니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-124">**Cluster login name and password**: The default login name is **admin**.</span></span>
   * <span data-ttu-id="b5eec-125">**SSH 사용자 이름 및 암호**: 기본 사용자 이름은 **sshuser**입니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-125">**SSH username and password**: The default username is **sshuser**.</span></span>  <span data-ttu-id="b5eec-126">이름은 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-126">You can rename it.</span></span>
     
     <span data-ttu-id="b5eec-127">다른 매개 변수는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-127">Other parameters are optional.</span></span>  
     
     <span data-ttu-id="b5eec-128">각 클러스터에는 Azure Storage 계정 종속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-128">Each cluster has an Azure Storage account dependency.</span></span> <span data-ttu-id="b5eec-129">클러스터를 삭제한 후에는 데이터가 저장소 계정에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-129">After you delete a cluster, the data retains in the storage account.</span></span> <span data-ttu-id="b5eec-130">클러스터 기본 저장소 계정 이름은 "저장소"가 추가된 클러스터 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-130">The cluster default storage account name is the cluster name with "store" appended.</span></span> <span data-ttu-id="b5eec-131">템플릿 변수 섹션에 하드 코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-131">It is hardcoded in the template variables section.</span></span>
3. <span data-ttu-id="b5eec-132">**위에 명시된 사용 약관에 동의함**을 선택한 다음 **구매**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-132">Select **I agree to the terms and conditions stated above**, and then click **Purchase**.</span></span> <span data-ttu-id="b5eec-133">클러스터를 만들려면 20분 정도가 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-133">It takes about 20 minutes to create a cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="b5eec-134">HBase 클러스터를 삭제한 후에는 동일한 기본 Blob 컨테이너를 사용하여 다른 HBase 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-134">After an HBase cluster is deleted, you can create another HBase cluster by using the same default blob container.</span></span> <span data-ttu-id="b5eec-135">새 클러스터에서는 원래 클러스터에서 만든 HBase 테이블을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-135">The new cluster picks up the HBase tables you created in the original cluster.</span></span> <span data-ttu-id="b5eec-136">불일치를 방지하기 위해 클러스터를 삭제하기 전에 HBase 테이블을 사용하지 않도록 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-136">To avoid inconsistencies, we recommend that you disable the HBase tables before you delete the cluster.</span></span>
> 
> 

## <a name="create-tables-and-insert-data"></a><span data-ttu-id="b5eec-137">테이블 만들기 및 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="b5eec-137">Create tables and insert data</span></span>
<span data-ttu-id="b5eec-138">SSH를 사용하여 HBase 클러스터를 연결하고 HBase 셸을 사용하여 HBase 테이블을 만들고 데이터 및 쿼리 데이터를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-138">You can use SSH to connect to HBase clusters and then use HBase Shell to create HBase tables, insert data, and query data.</span></span> <span data-ttu-id="b5eec-139">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b5eec-139">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="b5eec-140">대부분의 사람들의 경우, 데이터는 테이블 형식으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-140">For most people, data appears in the tabular format:</span></span>

![HDInsight HBase 테이블 형식 데이터][img-hbase-sample-data-tabular]

<span data-ttu-id="b5eec-142">BigTable의 구현인 HBase에서 동일한 데이터는 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-142">In HBase (an implementation of BigTable), the same data looks like:</span></span>

![HDInsight HBase BigTable 데이터][img-hbase-sample-data-bigtable]


<span data-ttu-id="b5eec-144">**HBase 셸을 사용하려면**</span><span class="sxs-lookup"><span data-stu-id="b5eec-144">**To use the HBase shell**</span></span>

1. <span data-ttu-id="b5eec-145">SSH에서 다음 HBase 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-145">From SSH, run the following HBase command:</span></span>
   
    ```bash
    hbase shell
    ```

2. <span data-ttu-id="b5eec-146">두 열 패밀리가 있는 HBase를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-146">Create an HBase with two-column families:</span></span>

    ```hbaseshell   
    create 'Contacts', 'Personal', 'Office'
    list
    ```
3. <span data-ttu-id="b5eec-147">일부 데이터 삽입:</span><span class="sxs-lookup"><span data-stu-id="b5eec-147">Insert some data:</span></span>
    
    ```hbaseshell   
    put 'Contacts', '1000', 'Personal:Name', 'John Dole'
    put 'Contacts', '1000', 'Personal:Phone', '1-425-000-0001'
    put 'Contacts', '1000', 'Office:Phone', '1-425-000-0002'
    put 'Contacts', '1000', 'Office:Address', '1111 San Gabriel Dr.'
    scan 'Contacts'
    ```
   
    ![HDInsight Hadoop HBase 셸][img-hbase-shell]
4. <span data-ttu-id="b5eec-149">단일 행 가져오기</span><span class="sxs-lookup"><span data-stu-id="b5eec-149">Get a single row</span></span>
   
    ```hbaseshell
    get 'Contacts', '1000'
    ```
   
    <span data-ttu-id="b5eec-150">행이 하나만 있기 때문에 스캔 명령을 사용하여 동일한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-150">You shall see the same results as using the scan command because there is only one row.</span></span>
   
    <span data-ttu-id="b5eec-151">HBase 테이블 스키마에 대한 자세한 내용은 [HBase 스키마 디자인 소개][hbase-schema]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b5eec-151">For more information about the HBase table schema, see [Introduction to HBase Schema Design][hbase-schema].</span></span> <span data-ttu-id="b5eec-152">HBase 명령에 대한 자세한 내용은 [Apache HBase 참조 가이드][hbase-quick-start]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b5eec-152">For more HBase commands, see [Apache HBase reference guide][hbase-quick-start].</span></span>
5. <span data-ttu-id="b5eec-153">셸 종료</span><span class="sxs-lookup"><span data-stu-id="b5eec-153">Exit the shell</span></span>
   
    ```hbaseshell
    exit
    ```

<span data-ttu-id="b5eec-154">**연락처 HBase 테이블로 대량으로 데이터 로드**</span><span class="sxs-lookup"><span data-stu-id="b5eec-154">**To bulk load data into the contacts HBase table**</span></span>

<span data-ttu-id="b5eec-155">HBase는 테이블로 데이터를 로드하는 여러 방법을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-155">HBase includes several methods of loading data into tables.</span></span>  <span data-ttu-id="b5eec-156">자세한 내용은 [대량 로드](http://hbase.apache.org/book.html#arch.bulk.load)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b5eec-156">For more information, see [Bulk loading](http://hbase.apache.org/book.html#arch.bulk.load).</span></span>

<span data-ttu-id="b5eec-157">샘플 데이터 파일은 공용 Blob 컨테이너인 *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-157">A sample data file can be found in a public blob container, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.</span></span>  <span data-ttu-id="b5eec-158">데이터 파일 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-158">The content of the data file is:</span></span>

    8396    Calvin Raji      230-555-0191    230-555-0191    5415 San Gabriel Dr.
    16600   Karen Wu         646-555-0113    230-555-0192    9265 La Paz
    4324    Karl Xie         508-555-0163    230-555-0193    4912 La Vuelta
    16891   Jonn Jackson     674-555-0110    230-555-0194    40 Ellis St.
    3273    Miguel Miller    397-555-0155    230-555-0195    6696 Anchor Drive
    3588    Osa Agbonile     592-555-0152    230-555-0196    1873 Lion Circle
    10272   Julia Lee        870-555-0110    230-555-0197    3148 Rose Street
    4868    Jose Hayes       599-555-0171    230-555-0198    793 Crawford Street
    4761    Caleb Alexander  670-555-0141    230-555-0199    4775 Kentucky Dr.
    16443   Terry Chander    998-555-0171    230-555-0200    771 Northridge Drive

<span data-ttu-id="b5eec-159">필요에 따라 텍스트 파일을 만들고 고유한 저장소 계정에 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-159">You can optionally create a text file and upload the file to your own storage account.</span></span> <span data-ttu-id="b5eec-160">지침에 대해서는 [HDInsight에서 Hadoop 작업용 데이터 업로드][hdinsight-upload-data]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b5eec-160">For the instructions, see [Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data].</span></span>

> [!NOTE]
> <span data-ttu-id="b5eec-161">이 절차는 마지막 절차에서 만든 연락처 HBase 테이블을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-161">This procedure uses the Contacts HBase table you have created in the last procedure.</span></span>
> 

1. <span data-ttu-id="b5eec-162">SSH에서 다음 명령을 실행하여 데이터 파일을 StoreFiles로 변형하고 Dimporttsv.bulk.output에서 지정한 상대 경로에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-162">From SSH, run the following command to transform the data file to StoreFiles and store at a relative path specified by Dimporttsv.bulk.output.</span></span>  <span data-ttu-id="b5eec-163">HBase 셸인 경우에는 exit 명령을 사용하여 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-163">If you are in HBase Shell, use the exit command to exit.</span></span>

    ```bash   
    hbase org.apache.hadoop.hbase.mapreduce.ImportTsv -Dimporttsv.columns="HBASE_ROW_KEY,Personal:Name,Personal:Phone,Office:Phone,Office:Address" -Dimporttsv.bulk.output="/example/data/storeDataFileOutput" Contacts wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt
    ```

2. <span data-ttu-id="b5eec-164">/Example/data/storeDataFileOutput에서 HBase 테이블로 데이터를 업로드하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-164">Run the following command to upload the data from  /example/data/storeDataFileOutput to the HBase table:</span></span>
   
    ```bash
    hbase org.apache.hadoop.hbase.mapreduce.LoadIncrementalHFiles /example/data/storeDataFileOutput Contacts
    ```

3. <span data-ttu-id="b5eec-165">HBase 셸을 열고 스캔 명령을 사용하여 테이블 내용을 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-165">You can open the HBase shell, and use the scan command to list the table content.</span></span>

## <a name="use-hive-to-query-hbase"></a><span data-ttu-id="b5eec-166">Hive를 사용하여 HBase 쿼리</span><span class="sxs-lookup"><span data-stu-id="b5eec-166">Use Hive to query HBase</span></span>

<span data-ttu-id="b5eec-167">Hive를 사용하여 HBase 테이블의 데이터를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-167">You can query data in HBase tables by using Hive.</span></span> <span data-ttu-id="b5eec-168">이 섹션에서는 HBase 테이블에 매핑되는 Hive 테이블을 만들고 이를 사용하여 HBase 테이블의 데이터를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-168">In this section, you create a Hive table that maps to the HBase table and uses it to query the data in your HBase table.</span></span>

1. <span data-ttu-id="b5eec-169">**PuTTY**를 열고 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-169">Open **PuTTY**, and connect to the cluster.</span></span>  <span data-ttu-id="b5eec-170">이전 절차의 지침을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b5eec-170">See the instructions in the previous procedure.</span></span>
2. <span data-ttu-id="b5eec-171">SSH 세션에서 다음 명령을 사용하여 Beeline을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-171">From the SSH session, use the following command to start Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="b5eec-172">Beeline에 대한 자세한 내용은 [Beeline을 사용하여 HDInsight에서 Hadoop과 Hive 사용](hdinsight-hadoop-use-hive-beeline.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b5eec-172">For more information about Beeline, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
       
3. <span data-ttu-id="b5eec-173">다음 HiveQL 스크립트를 실행하여 HBase 테이블에 매핑되는 Hive 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-173">Run the following HiveQL script  to create a Hive table that maps to the HBase table.</span></span> <span data-ttu-id="b5eec-174">이 문을 실행하기 전에 HBase 셸을 사용하여 이 자습서의 앞에서 참조한 샘플 테이블을 만들었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-174">Make sure that you have created the sample table referenced earlier in this tutorial by using the HBase shell before you run this statement.</span></span>

    ```hiveql   
    CREATE EXTERNAL TABLE hbasecontacts(rowkey STRING, name STRING, homephone STRING, officephone STRING, officeaddress STRING)
    STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
    WITH SERDEPROPERTIES ('hbase.columns.mapping' = ':key,Personal:Name,Personal:Phone,Office:Phone,Office:Address')
    TBLPROPERTIES ('hbase.table.name' = 'Contacts');
    ```

4. <span data-ttu-id="b5eec-175">HBase 테이블에서 데이터를 쿼리하려면 다음 HiveQL 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-175">Run the following HiveQL script to query the data in the HBase table:</span></span>

    ```hiveql   
    SELECT count(rowkey) FROM hbasecontacts;
    ```

## <a name="use-hbase-rest-apis-using-curl"></a><span data-ttu-id="b5eec-176">Curl을 사용하여 HBase REST API 사용</span><span class="sxs-lookup"><span data-stu-id="b5eec-176">Use HBase REST APIs using Curl</span></span>

<span data-ttu-id="b5eec-177">REST API는 [기본 인증](http://en.wikipedia.org/wiki/Basic_access_authentication)을 통해 보안됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-177">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="b5eec-178">자격 증명이 안전하게 서버에 전송되도록 하려면 항상 보안 HTTP(HTTPS)를 사용하여 요청해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-178">You shall always make requests by using Secure HTTP (HTTPS) to help ensure that your credentials are securely sent to the server.</span></span>

2. <span data-ttu-id="b5eec-179">다음 명령을 사용하여 기존의 HBase 테이블을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-179">Use the following command to list the existing HBase tables:</span></span>

    ```bash
    curl -u <UserName>:<Password> \
    -G https://<ClusterName>.azurehdinsight.net/hbaserest/
    ```

3. <span data-ttu-id="b5eec-180">다음 명령을 사용하여 두 열 패밀리가 있는 새 HBase 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-180">Use the following command to create a new HBase table with two-column families:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/schema" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"@name\":\"Contact1\",\"ColumnSchema\":[{\"name\":\"Personal\"},{\"name\":\"Office\"}]}" \
    -v
    ```

    <span data-ttu-id="b5eec-181">스키마는 JSon 형식으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-181">The schema is provided in the JSon format.</span></span>
4. <span data-ttu-id="b5eec-182">다음 명령을 사용하여 데이터 일부를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-182">Use the following command to insert some data:</span></span>

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/false-row-key" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"Row\":[{\"key\":\"MTAwMA==\",\"Cell\": [{\"column\":\"UGVyc29uYWw6TmFtZQ==\", \"$\":\"Sm9obiBEb2xl\"}]}]}" \
    -v
    ```
   
    <span data-ttu-id="b5eec-183">-d 스위치에 지정된 값을 base64로 인코딩해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-183">You must base64 encode the values specified in the -d switch.</span></span> <span data-ttu-id="b5eec-184">예제:</span><span class="sxs-lookup"><span data-stu-id="b5eec-184">In the example:</span></span>
   
   * <span data-ttu-id="b5eec-185">MTAwMA==: 1000</span><span class="sxs-lookup"><span data-stu-id="b5eec-185">MTAwMA==: 1000</span></span>
   * <span data-ttu-id="b5eec-186">UGVyc29uYWw6TmFtZQ==: Personal:Name</span><span class="sxs-lookup"><span data-stu-id="b5eec-186">UGVyc29uYWw6TmFtZQ==: Personal:Name</span></span>
   * <span data-ttu-id="b5eec-187">Sm9obiBEb2xl: John Dole</span><span class="sxs-lookup"><span data-stu-id="b5eec-187">Sm9obiBEb2xl: John Dole</span></span>
     
     <span data-ttu-id="b5eec-188">[false-row-key](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single)를 사용하면 여러 (일괄 처리된) 값을 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-188">[false-row-key](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) allows you to insert multiple (batched) values.</span></span>
5. <span data-ttu-id="b5eec-189">다음 명령을 사용하여 행을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-189">Use the following command to get a row:</span></span>
   
    ```bash 
    curl -u <UserName>:<Password> \
    -X GET "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/1000" \
    -H "Accept: application/json" \
    -v
    ```

<span data-ttu-id="b5eec-190">HBase Rest에 대한 자세한 내용은 [Apache HBase 참조 가이드](https://hbase.apache.org/book.html#_rest)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b5eec-190">For more information about HBase Rest, see [Apache HBase Reference Guide](https://hbase.apache.org/book.html#_rest).</span></span>

> [!NOTE]
> <span data-ttu-id="b5eec-191">Thrift는 HDInsight의 HBase에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-191">Thrift is not supported by HBase in HDInsight.</span></span>
>
> <span data-ttu-id="b5eec-192">WebHCat에서 Curl 또는 다른 모든 REST 통신을 사용하는 경우 HDInsight 클러스터 관리자의 사용자 이름 및 암호를 제공하여 요청을 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-192">When using Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span></span> <span data-ttu-id="b5eec-193">또한 클러스터 이름을 서버로 요청을 보내는 데 사용되는 URI(Uniform Resource Identifier)의 일부로 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-193">You must also use the cluster name as part of the Uniform Resource Identifier (URI) used to send the requests to the server:</span></span>
> 
>   
>        curl -u <UserName>:<Password> \
>        -G https://<ClusterName>.azurehdinsight.net/templeton/v1/status
>   
>    <span data-ttu-id="b5eec-194">그러면 다음과 유사한 응답이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-194">You should receive a response similar to the following response:</span></span>
>   
>        {"status":"ok","version":"v1"}
   


## <a name="check-cluster-status"></a><span data-ttu-id="b5eec-195">클러스터 상태 확인</span><span class="sxs-lookup"><span data-stu-id="b5eec-195">Check cluster status</span></span>
<span data-ttu-id="b5eec-196">HDInsight에서 HBase는 클러스터 모니터링에 대한 웹 UI와 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-196">HBase in HDInsight ships with a Web UI for monitoring clusters.</span></span> <span data-ttu-id="b5eec-197">웹 UI를 사용하여 지역에 대한 정보 또는 통계를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-197">Using the Web UI, you can request statistics or information about regions.</span></span>

<span data-ttu-id="b5eec-198">**HBase Master UI에 액세스하려면**</span><span class="sxs-lookup"><span data-stu-id="b5eec-198">**To access the HBase Master UI**</span></span>

1. <span data-ttu-id="b5eec-199">https://&lt;Clustername>.azurehdinsight.net에서 Ambari 웹 UI에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-199">Sign into the the Ambari Web UI at https://&lt;Clustername>.azurehdinsight.net.</span></span>
2. <span data-ttu-id="b5eec-200">왼쪽 메뉴에서 **HBase**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-200">Click **HBase** from the left menu.</span></span>
3. <span data-ttu-id="b5eec-201">페이지 위쪽에서 **빠른 링크**를 클릭하고 활성 Zookeeper 노드 링크를 가리킨 다음 **HBase Master UI**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-201">Click **Quick links** on the top of the page, point to the active Zookeeper node link, and then click **HBase Master UI**.</span></span>  <span data-ttu-id="b5eec-202">UI는 다른 브라우저 탭에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-202">The UI is opened in another browser tab:</span></span>

  ![HDInsight HBase HMaster UI](./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hmaster-ui.png)

  <span data-ttu-id="b5eec-204">HBase Master UI에는 다음 섹션이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-204">The HBase Master UI contains the following sections:</span></span>

  - <span data-ttu-id="b5eec-205">지역 서버</span><span class="sxs-lookup"><span data-stu-id="b5eec-205">region servers</span></span>
  - <span data-ttu-id="b5eec-206">백업 마스터</span><span class="sxs-lookup"><span data-stu-id="b5eec-206">backup masters</span></span>
  - <span data-ttu-id="b5eec-207">테이블</span><span class="sxs-lookup"><span data-stu-id="b5eec-207">tables</span></span>
  - <span data-ttu-id="b5eec-208">태스크</span><span class="sxs-lookup"><span data-stu-id="b5eec-208">tasks</span></span>
  - <span data-ttu-id="b5eec-209">소프트웨어 특성</span><span class="sxs-lookup"><span data-stu-id="b5eec-209">software attributes</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="b5eec-210">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="b5eec-210">Delete the cluster</span></span>
<span data-ttu-id="b5eec-211">불일치를 방지하기 위해 클러스터를 삭제하기 전에 HBase 테이블을 사용하지 않도록 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-211">To avoid inconsistencies, we recommend that you disable the HBase tables before you delete the cluster.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="b5eec-212">문제 해결</span><span class="sxs-lookup"><span data-stu-id="b5eec-212">Troubleshoot</span></span>

<span data-ttu-id="b5eec-213">HDInsight 클러스터를 만드는 동안 문제가 발생할 경우 [액세스 제어 요구 사항](hdinsight-administer-use-portal-linux.md#create-clusters)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b5eec-213">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5eec-214">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b5eec-214">Next steps</span></span>
<span data-ttu-id="b5eec-215">이 문서에서는 HBase 클러스터를 만드는 방법 및 테이블을 만들고 HBase 셸의 데이터를 이 테이블에서 보는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-215">In this article, you learned how to create an HBase cluster and how to create tables and view the data in those tables from the HBase shell.</span></span> <span data-ttu-id="b5eec-216">또한 HBase 테이블에서 데이터에 대해 Hive 쿼리를 사용하는 방법 및 HBase C# REST API를 사용하여 HBase 테이블을 만들고 이 테이블에서 데이터를 검색하는 방법도 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-216">You also learned how to use a Hive query on data in HBase tables and how to use the HBase C# REST APIs to create an HBase table and retrieve data from the table.</span></span>

<span data-ttu-id="b5eec-217">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b5eec-217">To learn more, see:</span></span>

* <span data-ttu-id="b5eec-218">[HDInsight HBase 개요][hdinsight-hbase-overview]: HBase는 대량의 비구조적/반구조적 데이터에 대해 임의 액세스 및 강력한 일관성을 제공하는 Hadoop 기반의 Apache 오픈 소스 NoSQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="b5eec-218">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>

[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hbase-reference]: http://hbase.apache.org/book.html#importtsv
[hbase-schema]: http://0b4af6cdc2f0c5998459-c0245c5c937c5dedcca3f1764ecc9b2f.r43.cf2.rackcdn.com/9353-login1210_khurana.pdf
[hbase-quick-start]: http://hbase.apache.org/book.html#quickstart





[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-versions]: hdinsight-component-versioning.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-portal]: https://portal.azure.com/
[azure-create-storageaccount]: http://azure.microsoft.com/documentation/articles/storage-create-storage-account/

[img-hdinsight-hbase-cluster-quick-create]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-quick-create.png
[img-hdinsight-hbase-hive-editor]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hive-editor.png
[img-hdinsight-hbase-file-browser]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-file-browser.png
[img-hbase-shell]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-shell.png
[img-hbase-sample-data-tabular]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-tabular.png
[img-hbase-sample-data-bigtable]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-bigtable.png
