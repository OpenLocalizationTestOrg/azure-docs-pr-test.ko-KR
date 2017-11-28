---
title: "Azure HDInsight에 R Server에 대 한 저장소 솔루션 aaaAzure | Microsoft Docs"
description: "Hello 다른 저장소 옵션 HDInsight에 R server 사용 가능한 toousers에 알아보기"
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 1cf30096-d3ca-45ea-b526-aa3954402f66
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: ff5e80fee14d5e74cbc22e873e6bc1439a3b6037
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a><span data-ttu-id="12d89-103">HDInsight의 R Server에 대한 Azure Storage 솔루션</span><span class="sxs-lookup"><span data-stu-id="12d89-103">Azure Storage solutions for R Server on HDInsight</span></span>

<span data-ttu-id="12d89-104">HDInsight의 Microsoft R Server는 다양 한 저장소 솔루션 toopersist 데이터, 코드 또는 분석의 결과 포함 하는 개체에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-104">Microsoft R Server on HDInsight has a variety of storage solutions toopersist data, code, or objects that contain results from analysis.</span></span> <span data-ttu-id="12d89-105">다음 옵션 hello를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-105">These include hello following options:</span></span>

- [<span data-ttu-id="12d89-106">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="12d89-106">Azure Blob</span></span>](https://azure.microsoft.com/services/storage/blobs/)
- [<span data-ttu-id="12d89-107">Azure 데이터 레이크 저장소</span><span class="sxs-lookup"><span data-stu-id="12d89-107">Azure Data Lake Storage</span></span>](https://azure.microsoft.com/services/data-lake-store/)
- [<span data-ttu-id="12d89-108">Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="12d89-108">Azure File storage</span></span>](https://azure.microsoft.com/services/storage/files/)

<span data-ttu-id="12d89-109">여러 Azure 저장소 계정 또는 HDI 클러스터를 사용 하 여 컨테이너에 액세스 하는 hello 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-109">You also have hello option of accessing multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="12d89-110">Azure 파일 저장소에 toomount 예를 들어 hello Linux 파일 시스템에는 Azure 저장소 파일 공유를 사용 하면 hello 가장자리 노드에서 용도로 편리 하 게 데이터 저장소 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-110">Azure File storage is a convenient data storage option for use on hello edge node that enables you toomount an Azure Storage file share to, for example, hello Linux file system.</span></span> <span data-ttu-id="12d89-111">하지만, Azure File 공유는 마운팅이 가능하고 Windows 또는 Linux 등 지원되는 OS가 있는 모든 시스템에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-111">But Azure File shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> 

<span data-ttu-id="12d89-112">HDInsight에서 Hadoop 클러스터를 만들 때 **Azure Storage** 계정 또는 **Data Lake Store**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-112">When you create an Hadoop cluster in HDInsight, you specify either an **Azure storage** account or a **Data Lake store**.</span></span> <span data-ttu-id="12d89-113">해당 계정에서 특정 저장소 컨테이너 (예: hello Hadoop 분산 파일 시스템)를 만들면 hello 클러스터에 대 한 hello 파일 시스템을 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-113">A specific storage container from that account holds hello file system for hello cluster that you create (for example, hello Hadoop Distributed File System).</span></span> <span data-ttu-id="12d89-114">자세한 내용 및 지침은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12d89-114">For more information and guidance, see:</span></span>

- [<span data-ttu-id="12d89-115">HDInsight에서 Azure Storage 사용</span><span class="sxs-lookup"><span data-stu-id="12d89-115">Use Azure storage with HDInsight</span></span>](hdinsight-hadoop-use-blob-storage.md)
- <span data-ttu-id="12d89-116">[Azure HDInsight 클러스터에 Data Lake Store 사용](hdinsight-hadoop-use-data-lake-store.md)</span><span class="sxs-lookup"><span data-stu-id="12d89-116">[Use Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> 

<span data-ttu-id="12d89-117">Hello Azure 저장소 솔루션에 대 한 자세한 내용은 참조 하십시오. [Azure 저장소 소개 tooMicrosoft](../storage/common/storage-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-117">For more information on hello Azure storage solutions, see [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md).</span></span> 

<span data-ttu-id="12d89-118">Hello 가장 적합 한 저장소 옵션 toouse 시나리오에 대 한 선택에 대 한 지침을 참조 하십시오. [결정 때 toouse Azure Blob, Azure 파일 또는 Azure 데이터 디스크](../storage/common/storage-decide-blobs-files-disks.md)</span><span class="sxs-lookup"><span data-stu-id="12d89-118">For guidance on selecting hello most appropriate storage option toouse for your scenario, see [Deciding when toouse Azure Blobs, Azure Files, or Azure Data Disks](../storage/common/storage-decide-blobs-files-disks.md)</span></span> 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a><span data-ttu-id="12d89-119">R Server에 Azure Blob Storage 계정 사용</span><span class="sxs-lookup"><span data-stu-id="12d89-119">Use Azure Blob storage accounts with R Server</span></span>

<span data-ttu-id="12d89-120">필요한 경우 HDI 클러스터가 있는 여러 Azure 저장소 계정 또는 컨테이너에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-120">If necessary, you can access multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="12d89-121">toodo hello 클러스터를 만들고 다음 이러한 단계 toouse를 따라 hello UI에서에서 toospecify hello 추가 저장소 계정이 필요, R Server를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-121">toodo so, you need toospecify hello additional storage accounts in hello UI when you create hello cluster, and then follow these steps toouse them with R Server.</span></span>

> [!WARNING]
> <span data-ttu-id="12d89-122">성능 향상을 위해 hello HDInsight 클러스터를 만드는 hello에 동일한 사용자가 지정한 hello 기본 저장소 계정으로 데이터 센터입니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-122">For performance purposes, hello HDInsight cluster is created in hello same data center as hello primary storage account that you specify.</span></span> <span data-ttu-id="12d89-123">저장소 계정을 사용 하 여 hello HDInsight 클러스터와 다른 위치에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-123">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span>

1. <span data-ttu-id="12d89-124">저장소 계정 이름이 **storage1**이고 기본 컨테이너가 **container1**인 HDInsight 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-124">Create an HDInsight cluster with a storage account name of **storage1** and a default container called **container1**.</span></span>
2. <span data-ttu-id="12d89-125">**storage2**라는 추가 저장소 계정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-125">Specify an additional storage account called **storage2**.</span></span>  
3. <span data-ttu-id="12d89-126">Hello mycsv.csv 파일 toohello /share 디렉터리를 복사 하 고 해당 파일에 대해 분석을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-126">Copy hello mycsv.csv file toohello /share directory, and perform analysis on that file.</span></span>  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. <span data-ttu-id="12d89-127">R 코드를 설정 hello 이름 노드 너무**기본적** 디렉터리 및 파일 tooprocess를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-127">In R code, set hello name node too**default,** and set your directory and file tooprocess.</span></span>  

        myNameNode <- "default"
        myPort <- 0

        #Location of hello data:  
        bigDataDirRoot <- "/share"  

        #Define Spark compute context:
        mySparkCluster <- RxSpark(consoleOutput=TRUE)

        #Set compute context:
        rxSetComputeContext(mySparkCluster)

        #Define hello Hadoop Distributed File System (HDFS) file system:
        hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

        #Specify hello input file tooanalyze in HDFS:
        inputFile <-file.path(bigDataDirRoot,"mycsv.csv")

<span data-ttu-id="12d89-128">디렉터리 및 파일 참조 지점 toohello 저장소 계정 hello 모든 wasb://container1@storage1.blob.core.windows.net합니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-128">All hello directory and file references point toohello storage account wasb://container1@storage1.blob.core.windows.net.</span></span> <span data-ttu-id="12d89-129">이 hello **기본 저장소 계정** hello HDInsight 클러스터와 연결 된입니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-129">This is hello **default storage account** that's associated with hello HDInsight cluster.</span></span>

<span data-ttu-id="12d89-130">이제 tooprocess 한다고 가정 이라는 파일 mySpecial.csv hello /private에 있는 디렉터리의 **실행 하면 container2** 에 **storage2**합니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-130">Now, suppose you want tooprocess a file called mySpecial.csv that's located in hello  /private directory of **container2** in **storage2**.</span></span>

<span data-ttu-id="12d89-131">R 코드에서 가리키고 hello 이름 노드 참조 toohello **storage2** 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-131">In your R code, point hello name node reference toohello **storage2** storage account.</span></span>


    myNameNode <- "wasb://container2@storage2.blob.core.windows.net"
    myPort <- 0

    #Location of hello data:
    bigDataDirRoot <- "/private"

    #Define Spark compute context:
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    #Set compute context:
    rxSetComputeContext(mySparkCluster)

    #Define HDFS file system:
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    #Specify hello input file tooanalyze in HDFS:
    inputFile <-file.path(bigDataDirRoot,"mySpecial.csv")

<span data-ttu-id="12d89-132">Hello 디렉터리 및 파일 참조 지금 지점 toohello 저장소 계정의 모든 wasb://container2@storage2.blob.core.windows.net합니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-132">All of hello directory and file references now point toohello storage account wasb://container2@storage2.blob.core.windows.net.</span></span> <span data-ttu-id="12d89-133">이 hello **이름 노드** 지정한입니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-133">This is hello **Name Node** that you’ve specified.</span></span>

<span data-ttu-id="12d89-134">Tooconfigure hello /user/RevoShare/있는<SSH username> 디렉터리에 **storage2** 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-134">You have tooconfigure hello /user/RevoShare/<SSH username> directory on **storage2** as follows:</span></span>


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a><span data-ttu-id="12d89-135">R Server에서 Azure Data Lake Store 사용</span><span class="sxs-lookup"><span data-stu-id="12d89-135">Use an Azure Data Lake store with R Server</span></span>

<span data-ttu-id="12d89-136">데이터 레이크 toouse HDInsight 계정을 사용 하 여 저장 toogive toouse 지정 하 여 클러스터 액세스 tooeach Azure 데이터 레이크 저장소를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-136">toouse Data Lake stores with your HDInsight account, you need toogive your cluster access tooeach Azure Data Lake store that you want toouse.</span></span> <span data-ttu-id="12d89-137">Toouse Azure 포털 toocreate는 HDInsight hello 하는 방법에 대 한 지침 Azure 데이터 레이크 저장소 계정 추가 저장소 또는 hello 기본 저장소를 클러스터에 대 한 참조 [Azure포털을사용하여데이터레이크저장소는HDInsight클러스터만들기](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="12d89-137">For instructions on how toouse hello Azure portal toocreate a HDInsight cluster with an Azure Data Lake Store account as hello default storage or as an additional store, see [Create an HDInsight cluster with Data Lake Store using Azure portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

<span data-ttu-id="12d89-138">그런 다음 저장소를 사용 하 hello R 스크립트에서 훨씬 hello 이전 절차에 설명 된 대로 보조 Azure 저장소 계정 했던 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-138">You then use hello store in your R script much like you did a secondary Azure storage account as described in hello previous procedure.</span></span>

### <a name="add-cluster-access-tooyour-azure-data-lake-stores"></a><span data-ttu-id="12d89-139">Azure 데이터 레이크를 저장 하는 클러스터 액세스 tooyour 추가</span><span class="sxs-lookup"><span data-stu-id="12d89-139">Add cluster access tooyour Azure Data Lake stores</span></span>
<span data-ttu-id="12d89-140">HDInsight 클러스터와 연결된 Azure AD(Azure Active Directory) 서비스 주체를 사용하여 Azure Data Lake 저장소에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-140">You access a Data Lake store by using an Azure Active Directory (Azure AD) Service Principal that's associated with your HDInsight cluster.</span></span>

<span data-ttu-id="12d89-141">Azure AD 서비스 주체 tooadd:</span><span class="sxs-lookup"><span data-stu-id="12d89-141">tooadd an Azure AD Service Principal:</span></span>

1. <span data-ttu-id="12d89-142">HDInsight 클러스터를 만들 때 선택 **클러스터 AAD Id** hello에서 **데이터 원본** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-142">When you create your HDInsight cluster, select **Cluster AAD Identity** from hello **Data Source** tab.</span></span>

2. <span data-ttu-id="12d89-143">Hello에 **클러스터 AAD Id** 대화 상자의 **AD 서비스 보안 주체 선택**선택, **새로 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-143">In hello **Cluster AAD Identity** dialog box, under **Select AD Service Principal**, select **Create new**.</span></span>

<span data-ttu-id="12d89-144">Hello 서비스 사용자 이름을 지정 하 고 암호를 만들 후 클릭 **ADLS 액세스 관리** tooassociate hello 데이터 레이크 인 서비스 사용자를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-144">After you give hello Service Principal a name and create a password for it, click **Manage ADLS Access** tooassociate hello Service Principal with your Data Lake stores.</span></span>

<span data-ttu-id="12d89-145">가능한 tooadd 클러스터 액세스 tooone 이기도 하거나 더 많은 데이터 레이크 클러스터를 만든 다음 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-145">It’s also possible tooadd cluster access tooone or more Data Lake stores following cluster creation.</span></span> <span data-ttu-id="12d89-146">데이터 레이크 저장소에 대 한 Azure 포털 항목 hello를 열고 너무 이동**데이터 탐색기 > 액세스 > 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-146">Open hello Azure portal entry for a Data Lake store and go too**Data Explorer > Access > Add**.</span></span> 

### <a name="how-tooaccess-hello-data-lake-store-from-r-server"></a><span data-ttu-id="12d89-147">어떻게 tooaccess hello R 서버에서 데이터 레이크 저장소</span><span class="sxs-lookup"><span data-stu-id="12d89-147">How tooaccess hello Data Lake store from R Server</span></span>

<span data-ttu-id="12d89-148">액세스 tooa 데이터 레이크 저장소를 제공한 후 HDInsight hello 하듯이 보조 Azure 저장소 계정에서 R 서버에서 hello 저장소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-148">Once you’ve given access tooa Data Lake store, you can use hello store in R Server on HDInsight hello way you would a secondary Azure storage account.</span></span> <span data-ttu-id="12d89-149">차이점은 해당 hello 접두사만 hello **wasb: / /** 쪽 변경**adl: / /** 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-149">hello only difference is that hello prefix **wasb://** changes too**adl://** as follows:</span></span>


    # Point toohello ADL store (e.g. ADLtest)
    myNameNode <- "adl://rkadl1.azuredatalakestore.net"
    myPort <- 0

    # Location of hello data (assumes a /share directory on hello ADL account)
    bigDataDirRoot <- "/share"  

    # Define Spark compute context
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    # Set compute context
    rxSetComputeContext(mySparkCluster)

    # Define HDFS file system
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    # Specify hello input file in HDFS tooanalyze
    inputFile <-file.path(bigDataDirRoot,"AirlineDemoSmall.csv")

    # Create factors for days of hello week
    colInfo <- list(DayOfWeek = list(type = "factor",
               levels = c("Monday", "Tuesday", "Wednesday", "Thursday",
                          "Friday", "Saturday", "Sunday")))

    # Define hello data source
    airDS <- RxTextData(file = inputFile, missingValueString = "M",
                    colInfo  = colInfo, fileSystem = hdfsFS)

    # Run a linear regression
    model <- rxLinMod(ArrDelay~CRSDepTime+DayOfWeek, data = airDS)


<span data-ttu-id="12d89-150">hello 다음 명령을 hello RevoShare 디렉터리에 있는 데이터 레이크 저장소 계정이 사용 되는 tooconfigure hello 되며 hello 이전 예제의 hello 샘플.csv 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-150">hello following commands are used tooconfigure hello Data Lake storage account with hello RevoShare directory and add hello sample .csv file from hello previous example:</span></span>


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a><span data-ttu-id="12d89-151">R Server에서 Azure File Storage 사용</span><span class="sxs-lookup"><span data-stu-id="12d89-151">Use Azure File storage with R Server</span></span>

<span data-ttu-id="12d89-152">Hello 가장자리 노드 [Azure Files] ((https://azure.microsoft.com/services/storage/files/) 호출에 사용 하기 위해 편리 하 게 데이터 저장소 옵션은 또한.</span><span class="sxs-lookup"><span data-stu-id="12d89-152">There is also a convenient data storage option for use on hello edge node called [Azure Files]((https://azure.microsoft.com/services/storage/files/).</span></span> <span data-ttu-id="12d89-153">Azure 저장소 파일 공유 toohello Linux 파일 시스템 toomount이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-153">It enables you toomount an Azure Storage file share toohello Linux file system.</span></span> <span data-ttu-id="12d89-154">이 옵션은 데이터 파일, R 스크립트 및 HDFS 보다는 hello 가장자리 노드에 toouse hello 기본 파일 시스템 의미는 시에 특히, 나중에 필요할 수 있는 결과 개체를 저장 하는 데 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-154">This option can be handy for storing data files, R scripts, and result objects that might be needed later, especially when it makes sense toouse hello native file system on hello edge node rather than HDFS.</span></span> 

<span data-ttu-id="12d89-155">Azure 파일의 주요 혜택은 해당 hello 파일 공유를 탑재 하 고 Windows 또는 Linux와 같은 지원 되는 OS 시스템에서 사용 하는 수입니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-155">A major benefit of Azure Files is that hello file shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> <span data-ttu-id="12d89-156">예를 들어, 사용자 또는 팀의 다른 사용자가 보유한 HDInsight 클러스터, Azure VM 또는 온-프레미스 시스템에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-156">For example, it can be used by another HDInsight cluster that you or someone on your team has, by an Azure VM, or even by an on-premises system.</span></span> <span data-ttu-id="12d89-157">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12d89-157">For more information, see:</span></span>

- [<span data-ttu-id="12d89-158">어떻게 toouse Linux로 Azure 파일 저장소</span><span class="sxs-lookup"><span data-stu-id="12d89-158">How toouse Azure File storage with Linux</span></span>](../storage/files/storage-how-to-use-files-linux.md)
- [<span data-ttu-id="12d89-159">어떻게 toouse Windows에서 Azure 파일 저장소</span><span class="sxs-lookup"><span data-stu-id="12d89-159">How toouse Azure File storage on Windows</span></span>](../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a><span data-ttu-id="12d89-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="12d89-160">Next steps</span></span>

<span data-ttu-id="12d89-161">배웠으므로 이제 hello Azure 저장소 옵션을 사용 하 여 hello 다음 toodiscover R Server HDInsight의 완료 한 후에 데이터 과학 작업을 가져오는 방법이 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12d89-161">Now that you understand hello Azure storage options, use hello following links toodiscover ways of getting data science tasks done with R Server on HDInsight.</span></span>

* [<span data-ttu-id="12d89-162">HDInsight의 R 서버 개요</span><span class="sxs-lookup"><span data-stu-id="12d89-162">Overview of R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-overview.md)
* [<span data-ttu-id="12d89-163">Hadoop에서 R 서버 시작</span><span class="sxs-lookup"><span data-stu-id="12d89-163">Get started with R server on Hadoop</span></span>](hdinsight-hadoop-r-server-get-started.md)
* [<span data-ttu-id="12d89-164">RStudio 서버 tooHDInsight 추가 (클러스터 생성 중에 추가 되지) 하는 경우</span><span class="sxs-lookup"><span data-stu-id="12d89-164">Add RStudio Server tooHDInsight (if not added during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="12d89-165">HDInsight의 R 서버에 대한 Compute 컨텍스트 옵션</span><span class="sxs-lookup"><span data-stu-id="12d89-165">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)

