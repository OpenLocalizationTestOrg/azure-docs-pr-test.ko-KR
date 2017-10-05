---
title: "HDInsight의 R Server에 대한 Azure Storage 옵션 - Azure | Microsoft Docs"
description: "HDInsight의 R Server에서 사용할 수 있는 다양한 저장소 옵션에 대해 알아봅니다."
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
ms.openlocfilehash: aef9c15636ccaecce07d4fa218a40ed26ebad9df
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a><span data-ttu-id="9bbcf-103">HDInsight의 R Server에 대한 Azure Storage 솔루션</span><span class="sxs-lookup"><span data-stu-id="9bbcf-103">Azure Storage solutions for R Server on HDInsight</span></span>

<span data-ttu-id="9bbcf-104">HDInsight의 Microsoft R Server에는 데이터, 코드, 또는 분석 결과가 포함된 개체를 유지할 수 있는 다양한 저장 솔루션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-104">Microsoft R Server on HDInsight has a variety of storage solutions to persist data, code, or objects that contain results from analysis.</span></span> <span data-ttu-id="9bbcf-105">여기에는 다음 옵션이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-105">These include the following options:</span></span>

- [<span data-ttu-id="9bbcf-106">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="9bbcf-106">Azure Blob</span></span>](https://azure.microsoft.com/services/storage/blobs/)
- [<span data-ttu-id="9bbcf-107">Azure 데이터 레이크 저장소</span><span class="sxs-lookup"><span data-stu-id="9bbcf-107">Azure Data Lake Storage</span></span>](https://azure.microsoft.com/services/data-lake-store/)
- [<span data-ttu-id="9bbcf-108">Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="9bbcf-108">Azure File storage</span></span>](https://azure.microsoft.com/services/storage/files/)

<span data-ttu-id="9bbcf-109">필요한 경우 HDI 클러스터가 있는 여러 Azure Storage 계정 또는 컨테이너에 액세스할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-109">You also have the option of accessing multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="9bbcf-110">Azure File Storage는 Azure Storage 파일 공유를 Linux 파일 시스템 등에 마운팅할 수 있도록 에지 노드에서 사용할 수 있는 편리한 데이터 저장 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-110">Azure File storage is a convenient data storage option for use on the edge node that enables you to mount an Azure Storage file share to, for example, the Linux file system.</span></span> <span data-ttu-id="9bbcf-111">하지만, Azure File 공유는 마운팅이 가능하고 Windows 또는 Linux 등 지원되는 OS가 있는 모든 시스템에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-111">But Azure File shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> 

<span data-ttu-id="9bbcf-112">HDInsight에서 Hadoop 클러스터를 만들 때 **Azure Storage** 계정 또는 **Data Lake Store**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-112">When you create an Hadoop cluster in HDInsight, you specify either an **Azure storage** account or a **Data Lake store**.</span></span> <span data-ttu-id="9bbcf-113">해당 계정의 특정 저장소 컨테이너에는 사용자가 만든 클러스터의 파일 시스템(예: Hadoop 분산 파일 시스템)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-113">A specific storage container from that account holds the file system for the cluster that you create (for example, the Hadoop Distributed File System).</span></span> <span data-ttu-id="9bbcf-114">자세한 내용 및 지침은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-114">For more information and guidance, see:</span></span>

- [<span data-ttu-id="9bbcf-115">HDInsight에서 Azure Storage 사용</span><span class="sxs-lookup"><span data-stu-id="9bbcf-115">Use Azure storage with HDInsight</span></span>](hdinsight-hadoop-use-blob-storage.md)
- <span data-ttu-id="9bbcf-116">[Azure HDInsight 클러스터에 Data Lake Store 사용](hdinsight-hadoop-use-data-lake-store.md)</span><span class="sxs-lookup"><span data-stu-id="9bbcf-116">[Use Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> 

<span data-ttu-id="9bbcf-117">Azure Storage 솔루션에 대한 자세한 내용은 [Microsoft Azure Storage 소개](../storage/common/storage-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-117">For more information on the Azure storage solutions, see [Introduction to Microsoft Azure Storage](../storage/common/storage-introduction.md).</span></span> 

<span data-ttu-id="9bbcf-118">시나리오에 사용할 가장 적합한 저장소 옵션을 선택하는 방법에 대한 지침은 [Azure Blob, Azure File 또는 Azure Data Disk 사용 시기 결정](../storage/common/storage-decide-blobs-files-disks.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-118">For guidance on selecting the most appropriate storage option to use for your scenario, see [Deciding when to use Azure Blobs, Azure Files, or Azure Data Disks](../storage/common/storage-decide-blobs-files-disks.md)</span></span> 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a><span data-ttu-id="9bbcf-119">R Server에 Azure Blob Storage 계정 사용</span><span class="sxs-lookup"><span data-stu-id="9bbcf-119">Use Azure Blob storage accounts with R Server</span></span>

<span data-ttu-id="9bbcf-120">필요한 경우 HDI 클러스터가 있는 여러 Azure 저장소 계정 또는 컨테이너에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-120">If necessary, you can access multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="9bbcf-121">이렇게 하려면 클러스터를 만들 때 UI에서 추가 저장소 계정을 지정하고 다음 단계에 따라 R Server에서 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-121">To do so, you need to specify the additional storage accounts in the UI when you create the cluster, and then follow these steps to use them with R Server.</span></span>

> [!WARNING]
> <span data-ttu-id="9bbcf-122">성능을 위해 HDInsight 클러스터는 사용자가 지정한 기본 저장소 계정과 동일한 데이터 센터에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-122">For performance purposes, the HDInsight cluster is created in the same data center as the primary storage account that you specify.</span></span> <span data-ttu-id="9bbcf-123">HDInsight 클러스터와 다른 위치에서는 저장소 계정을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-123">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span>

1. <span data-ttu-id="9bbcf-124">저장소 계정 이름이 **storage1**이고 기본 컨테이너가 **container1**인 HDInsight 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-124">Create an HDInsight cluster with a storage account name of **storage1** and a default container called **container1**.</span></span>
2. <span data-ttu-id="9bbcf-125">**storage2**라는 추가 저장소 계정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-125">Specify an additional storage account called **storage2**.</span></span>  
3. <span data-ttu-id="9bbcf-126">/share 디렉터리로 mycsv.csv 파일을 복사하고 해당 파일에 대한 분석을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-126">Copy the mycsv.csv file to the /share directory, and perform analysis on that file.</span></span>  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. <span data-ttu-id="9bbcf-127">R 코드에서 이름 노드를 **default** 로 설정하고 처리할 디렉터리 및 파일을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-127">In R code, set the name node to **default,** and set your directory and file to process.</span></span>  

        myNameNode <- "default"
        myPort <- 0

        #Location of the data:  
        bigDataDirRoot <- "/share"  

        #Define Spark compute context:
        mySparkCluster <- RxSpark(consoleOutput=TRUE)

        #Set compute context:
        rxSetComputeContext(mySparkCluster)

        #Define the Hadoop Distributed File System (HDFS) file system:
        hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

        #Specify the input file to analyze in HDFS:
        inputFile <-file.path(bigDataDirRoot,"mycsv.csv")

<span data-ttu-id="9bbcf-128">모든 디렉터리와 파일 참조는 저장소 계정 wasb://container1@storage1.blob.core.windows.net을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-128">All the directory and file references point to the storage account wasb://container1@storage1.blob.core.windows.net.</span></span> <span data-ttu-id="9bbcf-129">이는 HDInsight 클러스터와 연결된 **기본 저장소 계정**입니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-129">This is the **default storage account** that's associated with the HDInsight cluster.</span></span>

<span data-ttu-id="9bbcf-130">**storage2**에 있는 **container2**의 /private 디렉터리에 있는 mySpecial.csv 파일을 처리한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-130">Now, suppose you want to process a file called mySpecial.csv that's located in the  /private directory of **container2** in **storage2**.</span></span>

<span data-ttu-id="9bbcf-131">R 코드에서 이름 노드 참조를 **storage2** 저장소 계정으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-131">In your R code, point the name node reference to the **storage2** storage account.</span></span>


    myNameNode <- "wasb://container2@storage2.blob.core.windows.net"
    myPort <- 0

    #Location of the data:
    bigDataDirRoot <- "/private"

    #Define Spark compute context:
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    #Set compute context:
    rxSetComputeContext(mySparkCluster)

    #Define HDFS file system:
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    #Specify the input file to analyze in HDFS:
    inputFile <-file.path(bigDataDirRoot,"mySpecial.csv")

<span data-ttu-id="9bbcf-132">모든 디렉터리와 파일 참조는 이제 저장소 계정 wasb://container2@storage2.blob.core.windows.net을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-132">All of the directory and file references now point to the storage account wasb://container2@storage2.blob.core.windows.net.</span></span> <span data-ttu-id="9bbcf-133">지정한 **이름 노드**입니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-133">This is the **Name Node** that you’ve specified.</span></span>

<span data-ttu-id="9bbcf-134">다음과 같이 **storage2**에서 /user/RevoShare/<SSH username> 디렉터리를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-134">You have to configure the /user/RevoShare/<SSH username> directory on **storage2** as follows:</span></span>


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a><span data-ttu-id="9bbcf-135">R Server에서 Azure Data Lake Store 사용</span><span class="sxs-lookup"><span data-stu-id="9bbcf-135">Use an Azure Data Lake store with R Server</span></span>

<span data-ttu-id="9bbcf-136">HDInsight 계정과 함께 Data Lake 저장소를 사용하려면 사용하려는 Azure Data Lake 저장소 각각에 클러스터 액세스 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-136">To use Data Lake stores with your HDInsight account, you need to give your cluster access to each Azure Data Lake store that you want to use.</span></span> <span data-ttu-id="9bbcf-137">Azure Portal에서 기본 저장소 또는 추가 저장소로 Azure Data Lake Store 계정을 사용하여 HDInsight 클러스터를 만드는 방법에 대한 지침은 [Azure Portal을 사용하여 Data Lake Store를 포함한 HDInsight 클러스터 만들기](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-137">For instructions on how to use the Azure portal to create a HDInsight cluster with an Azure Data Lake Store account as the default storage or as an additional store, see [Create an HDInsight cluster with Data Lake Store using Azure portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

<span data-ttu-id="9bbcf-138">그런 다음, 보조 Azure Storage 계정을 사용하는 것처럼 R 스크립트에서 저장소를 사용합니다(이전 절차에서 설명한 대로).</span><span class="sxs-lookup"><span data-stu-id="9bbcf-138">You then use the store in your R script much like you did a secondary Azure storage account as described in the previous procedure.</span></span>

### <a name="add-cluster-access-to-your-azure-data-lake-stores"></a><span data-ttu-id="9bbcf-139">Azure Data Lake 저장소에 클러스터 액세스 추가</span><span class="sxs-lookup"><span data-stu-id="9bbcf-139">Add cluster access to your Azure Data Lake stores</span></span>
<span data-ttu-id="9bbcf-140">HDInsight 클러스터와 연결된 Azure AD(Azure Active Directory) 서비스 주체를 사용하여 Azure Data Lake 저장소에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-140">You access a Data Lake store by using an Azure Active Directory (Azure AD) Service Principal that's associated with your HDInsight cluster.</span></span>

<span data-ttu-id="9bbcf-141">Azure AD 서비스 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="9bbcf-141">To add an Azure AD Service Principal:</span></span>

1. <span data-ttu-id="9bbcf-142">HDInsight 클러스터를 만들 때 **데이터 원본** 탭에서 **클러스터 AAD ID**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-142">When you create your HDInsight cluster, select **Cluster AAD Identity** from the **Data Source** tab.</span></span>

2. <span data-ttu-id="9bbcf-143">**클러스터 AAD ID** 대화 상자의**AD 서비스 주체 선택**에서 **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-143">In the **Cluster AAD Identity** dialog box, under **Select AD Service Principal**, select **Create new**.</span></span>

<span data-ttu-id="9bbcf-144">서비스 사용자에 이름을 지정하고 암호를 만든 후에 **ADLS 액세스 관리**를 클릭하여 Data Lake Store와 서비스 사용자를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-144">After you give the Service Principal a name and create a password for it, click **Manage ADLS Access** to associate the Service Principal with your Data Lake stores.</span></span>

<span data-ttu-id="9bbcf-145">클러스터를 만든 후 하나 이상의 Data Lake Store에 클러스터 액세스를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-145">It’s also possible to add cluster access to one or more Data Lake stores following cluster creation.</span></span> <span data-ttu-id="9bbcf-146">Data Lake Store에 대한 Azure Portal 항목을 열고 **데이터 탐색기 > 액세스 > 추가**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-146">Open the Azure portal entry for a Data Lake store and go to **Data Explorer > Access > Add**.</span></span> 

### <a name="how-to-access-the-data-lake-store-from-r-server"></a><span data-ttu-id="9bbcf-147">R Server에서 Data Lake Store에 액세스하는 방법</span><span class="sxs-lookup"><span data-stu-id="9bbcf-147">How to access the Data Lake store from R Server</span></span>

<span data-ttu-id="9bbcf-148">Data Lake 저장소에 액세스 권한을 부여하면 보조 Azure 저장소 계정과 동일한 방식으로 HDInsight의 R 서버에서 저장소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-148">Once you’ve given access to a Data Lake store, you can use the store in R Server on HDInsight the way you would a secondary Azure storage account.</span></span> <span data-ttu-id="9bbcf-149">유일한 차이점은 다음과 같이 **wasb://** 접두사가 **adl://**로 변경된다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-149">The only difference is that the prefix **wasb://** changes to **adl://** as follows:</span></span>


    # Point to the ADL store (e.g. ADLtest)
    myNameNode <- "adl://rkadl1.azuredatalakestore.net"
    myPort <- 0

    # Location of the data (assumes a /share directory on the ADL account)
    bigDataDirRoot <- "/share"  

    # Define Spark compute context
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    # Set compute context
    rxSetComputeContext(mySparkCluster)

    # Define HDFS file system
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    # Specify the input file in HDFS to analyze
    inputFile <-file.path(bigDataDirRoot,"AirlineDemoSmall.csv")

    # Create factors for days of the week
    colInfo <- list(DayOfWeek = list(type = "factor",
               levels = c("Monday", "Tuesday", "Wednesday", "Thursday",
                          "Friday", "Saturday", "Sunday")))

    # Define the data source
    airDS <- RxTextData(file = inputFile, missingValueString = "M",
                    colInfo  = colInfo, fileSystem = hdfsFS)

    # Run a linear regression
    model <- rxLinMod(ArrDelay~CRSDepTime+DayOfWeek, data = airDS)


<span data-ttu-id="9bbcf-150">다음 명령은 RevoShare 디렉터리로 Data Lake Store 계정을 구성하고 이전 예제의 샘플 .csv 파일을 추가하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-150">The following commands are used to configure the Data Lake storage account with the RevoShare directory and add the sample .csv file from the previous example:</span></span>


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a><span data-ttu-id="9bbcf-151">R Server에서 Azure File Storage 사용</span><span class="sxs-lookup"><span data-stu-id="9bbcf-151">Use Azure File storage with R Server</span></span>

<span data-ttu-id="9bbcf-152">에지 노드에 사용할 수 있는 [Azure 파일]이라고 하는 편리한 데이터 저장소 옵션도 있습니다(https://azure.microsoft.com/services/storage/files/).</span><span class="sxs-lookup"><span data-stu-id="9bbcf-152">There is also a convenient data storage option for use on the edge node called [Azure Files]((https://azure.microsoft.com/services/storage/files/).</span></span> <span data-ttu-id="9bbcf-153">Azure 파일을 사용하면 Linux 파일 시스템에서 Azure 저장소 파일 공유를 탑재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-153">It enables you to mount an Azure Storage file share to the Linux file system.</span></span> <span data-ttu-id="9bbcf-154">이 옵션은 특히 나중에 HDFS 대신 에지 노드의 원시 파일 시스템을 사용하는 것이 유용할 때 필요할 수 있는 데이터 파일, R 스크립트 및 결과 개체를 저장하는 데 편리합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-154">This option can be handy for storing data files, R scripts, and result objects that might be needed later, especially when it makes sense to use the native file system on the edge node rather than HDFS.</span></span> 

<span data-ttu-id="9bbcf-155">Azure 파일의 장점은 파일 공유가 탑재되고 Windows 또는 Linux 등 지원되는 OS가 있는 모든 시스템에서 사용할 수 있다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-155">A major benefit of Azure Files is that the file shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> <span data-ttu-id="9bbcf-156">예를 들어, 사용자 또는 팀의 다른 사용자가 보유한 HDInsight 클러스터, Azure VM 또는 온-프레미스 시스템에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-156">For example, it can be used by another HDInsight cluster that you or someone on your team has, by an Azure VM, or even by an on-premises system.</span></span> <span data-ttu-id="9bbcf-157">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-157">For more information, see:</span></span>

- [<span data-ttu-id="9bbcf-158">Linux에서 Azure File Storage 사용 방법</span><span class="sxs-lookup"><span data-stu-id="9bbcf-158">How to use Azure File storage with Linux</span></span>](../storage/files/storage-how-to-use-files-linux.md)
- [<span data-ttu-id="9bbcf-159">Windows에서 Azure File Storage 사용 방법</span><span class="sxs-lookup"><span data-stu-id="9bbcf-159">How to use Azure File storage on Windows</span></span>](../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a><span data-ttu-id="9bbcf-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9bbcf-160">Next steps</span></span>

<span data-ttu-id="9bbcf-161">Azure Storage 옵션을 이해했으므로, 이제 다음 링크를 사용하여 HDInsight의 R Server로 데이터 과학 작업을 수행하는 방법을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="9bbcf-161">Now that you understand the Azure storage options, use the following links to discover ways of getting data science tasks done with R Server on HDInsight.</span></span>

* [<span data-ttu-id="9bbcf-162">HDInsight의 R 서버 개요</span><span class="sxs-lookup"><span data-stu-id="9bbcf-162">Overview of R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-overview.md)
* [<span data-ttu-id="9bbcf-163">Hadoop에서 R 서버 시작</span><span class="sxs-lookup"><span data-stu-id="9bbcf-163">Get started with R server on Hadoop</span></span>](hdinsight-hadoop-r-server-get-started.md)
* [<span data-ttu-id="9bbcf-164">HDInsight에 RStudio Server 추가(클러스터를 만드는 중에 추가되지 않은 경우)</span><span class="sxs-lookup"><span data-stu-id="9bbcf-164">Add RStudio Server to HDInsight (if not added during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="9bbcf-165">HDInsight의 R 서버에 대한 계산 컨텍스트 옵션</span><span class="sxs-lookup"><span data-stu-id="9bbcf-165">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)

