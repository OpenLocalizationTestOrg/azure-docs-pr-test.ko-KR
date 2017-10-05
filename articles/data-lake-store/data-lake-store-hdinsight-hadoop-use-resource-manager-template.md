---
title: "Azure 템플릿을 사용하여 Azure HDInsight 및 Data Lake Store 만들기 | Microsoft Docs"
description: "Azure Resource Manager 템플릿을 사용하여 Azure Data Lake Store로 HDInsight Hadoop 클러스터 만들기 및 사용"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8ef8152f-2121-461e-956c-51c55144919d
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: nitinme
ms.openlocfilehash: 6f43423096f0e74f41afea275e4ec9801dc2cea5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-hdinsight-cluster-with-data-lake-store-using-azure-resource-manager-template"></a><span data-ttu-id="ccb87-103">Azure Resource Manager 템플릿을 사용하여 Data Lake Store로 HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="ccb87-103">Create an HDInsight cluster with Data Lake Store using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ccb87-104">포털 사용</span><span class="sxs-lookup"><span data-stu-id="ccb87-104">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="ccb87-105">PowerShell 사용(기본 저장소의 경우)</span><span class="sxs-lookup"><span data-stu-id="ccb87-105">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="ccb87-106">PowerShell 사용(추가 저장소의 경우)</span><span class="sxs-lookup"><span data-stu-id="ccb87-106">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="ccb87-107">Resource Manager 사용</span><span class="sxs-lookup"><span data-stu-id="ccb87-107">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="ccb87-108">Azure PowerShell을 사용하여 Azure Data Lake Store에서 HDInsight 클러스터를 **추가 저장소로** 구성하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-108">Learn how to use Azure PowerShell to configure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span>

<span data-ttu-id="ccb87-109">지원되는 클러스터 유형의 경우 Data Lake Store는 기본 저장소 또는 추가 저장소 계정으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-109">For supported cluster types, Data Lake Store be used as an default storage or additional storage account.</span></span> <span data-ttu-id="ccb87-110">Data Lake Store를 추가 저장소로 사용하는 경우 클러스터의 기본 저장소 계정은 여전히 Azure Storage Blob(WASB)이고 클러스터 관련 파일(예: 로그 등)은 여전히 기본 저장소에 기록되지만 처리하려는 데이터는 Data Lake Store 계정에 저장될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-110">When Data Lake Store is used as additional storage, the default storage account for the clusters will still be Azure Storage Blobs (WASB) and the cluster-related files (such as logs, etc.) are still written to the default storage, while the data that you want to process can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="ccb87-111">Data Lake 저장소를 추가 저장소 계정으로 사용하면 클러스터에서 저장소로 읽고 쓰는 성능 또는 기능에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-111">Using Data Lake Store as an additional storage account does not impact performance or the ability to read/write to the storage from the cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="ccb87-112">HDInsight 클러스터 저장소에서 Data Lake Store 사용</span><span class="sxs-lookup"><span data-stu-id="ccb87-112">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="ccb87-113">Data Lake Store에서 HDInsight를 사용하는 몇 가지 중요한 고려 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-113">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="ccb87-114">기본 저장소로 Data Lake Store에 액세스할 수 있는 HDInsight 클러스터를 만드는 옵션은 HDInsight 버전 3.5 및 3.6에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-114">Option to create HDInsight clusters with access to Data Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="ccb87-115">추가 저장소로 Data Lake Store에 액세스할 수 있는 HDInsight 클러스터를 만드는 옵션은 HDInsight 버전 3.2, 3.4, 3.5 및 3.6에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-115">Option to create HDInsight clusters with access to Data Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="ccb87-116">이 문서에서 데이터 레이크 저장소를 추가 저장소로 사용하여 Hadoop 클러스터를 프로비저닝합니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-116">In this article, we provision a Hadoop cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="ccb87-117">기본 저장소로 Data Lake Store를 사용하여 Hadoop 클러스터를 만드는 방법에 대한 지침은 [Azure Portal을 사용하여 Data Lake 저장소를 포함한 HDInsight 클러스터 만들기](data-lake-store-hdinsight-hadoop-use-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ccb87-117">For instructions on how to create a Hadoop cluster with Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ccb87-118">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ccb87-118">Prerequisites</span></span>
<span data-ttu-id="ccb87-119">이 자습서를 시작하기 전에 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-119">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="ccb87-120">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="ccb87-120">**An Azure subscription**.</span></span> <span data-ttu-id="ccb87-121">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ccb87-121">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ccb87-122">**Azure PowerShell 1.0 이상**.</span><span class="sxs-lookup"><span data-stu-id="ccb87-122">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="ccb87-123">[Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ccb87-123">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="ccb87-124">**Azure Active Directory 서비스 사용자**.</span><span class="sxs-lookup"><span data-stu-id="ccb87-124">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="ccb87-125">이 자습서의 단계에서는 Azure AD에서 서비스 사용자를 만드는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-125">Steps in this tutorial provide instructions on how to create a service principal in Azure AD.</span></span> <span data-ttu-id="ccb87-126">그러나 서비스 사용자를 만들려면 Azure AD 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-126">However, you must be an Azure AD administrator to be able to create a service principal.</span></span> <span data-ttu-id="ccb87-127">Azure AD 관리자인 경우 이 필수 조건을 건너뛰고 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-127">If you are an Azure AD administrator, you can skip this prerequisite and proceed with the tutorial.</span></span>

    <span data-ttu-id="ccb87-128">**Azure AD 관리자가 아닌 경우** 서비스 사용자를 만드는 데 필요한 단계를 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-128">**If you are not an Azure AD administrator**, you will not be able to perform the steps required to create a service principal.</span></span> <span data-ttu-id="ccb87-129">이 경우 먼저 Azure AD 관리자가 서비스 사용자를 만들어야 Data Lake Store와 HDInsight 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-129">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="ccb87-130">또한 [인증서를 사용하여 서비스 사용자 만들기](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority)에 설명된 대로 인증서를 사용하여 서비스 사용자를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-130">Also, the service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-hdinsight-cluster-with-azure-data-lake-store"></a><span data-ttu-id="ccb87-131">Azure Data Lake Store로 HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="ccb87-131">Create an HDInsight cluster with Azure Data Lake Store</span></span>
<span data-ttu-id="ccb87-132">Resource Manager 템플릿 및 템플릿 사용을 위한 필수 조건은 GitHub의 [새 Data Lake Store로 HDInsight Linux 클러스터 배포](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-132">The Resource Manager template, and the prerequisites for using the template, are available on GitHub at [Deploy a HDInsight Linux cluster with new Data Lake Store](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage).</span></span> <span data-ttu-id="ccb87-133">이 링크에 제공된 지침에 따라 Azure Data Lake Store를 추가 저장소로 사용하는 HDInsight 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-133">Follow the instructions provided at this link to create an HDInsight cluster with Azure Data Lake Store as the additional storage.</span></span>

<span data-ttu-id="ccb87-134">위에 언급된 링크의 지침에는 PowerShell이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-134">The instructions at the link mentioned above require PowerShell.</span></span> <span data-ttu-id="ccb87-135">이러한 지침을 시작하기 전에 Azure 계정에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-135">Before you start with those instructions, make sure you log in to your Azure account.</span></span> <span data-ttu-id="ccb87-136">바탕 화면에서 새 Azure PowerShell 창을 열고 다음 코드 조각을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-136">From your desktop, open a new Azure PowerShell window, and enter the following snippets.</span></span> <span data-ttu-id="ccb87-137">로그인하라는 메시지가 표시되면 구독 관리자/소유자 중 하나로 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-137">When prompted to log in, make sure you log in as one of the subscription admininistrators/owner:</span></span>

```
# Log in to your Azure account
Login-AzureRmAccount

# List all the subscriptions associated to your account
Get-AzureRmSubscription

# Select a subscription
Set-AzureRmContext -SubscriptionId <subscription ID>
```

## <a name="upload-sample-data-to-the-azure-data-lake-store"></a><span data-ttu-id="ccb87-138">Azure Data Lake Store에 샘플 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="ccb87-138">Upload sample data to the Azure Data Lake Store</span></span>
<span data-ttu-id="ccb87-139">Resource Manager 템플릿은 새 Data Lake Store 계정을 만들어 HDInsight 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-139">The Resource Manager template creates a new Data Lake Store account and associates it with the HDInsight cluster.</span></span> <span data-ttu-id="ccb87-140">이제 일부 샘플 데이터를 Data Lake Store에 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-140">You must now upload some sample data to the Data Lake Store.</span></span> <span data-ttu-id="ccb87-141">데이터 레이크 저장소의 데이터에 액세스하는 HDInsight 클러스터에서 작업을 실행하려면 자습서의 뒷부분에서 이 데이터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-141">You'll need this data later in the tutorial to run jobs from an HDInsight cluster that access data in the Data Lake Store.</span></span> <span data-ttu-id="ccb87-142">데이터를 업로드하는 방법은 [Data Lake Store에 파일 업로드](data-lake-store-get-started-portal.md#uploaddata)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ccb87-142">For instructions on how to upload data, see [Upload a file to your Data Lake Store](data-lake-store-get-started-portal.md#uploaddata).</span></span> <span data-ttu-id="ccb87-143">업로드할 일부 샘플 데이터를 찾는 경우 **Azure 데이터 레이크 Git 리포지토리** 의 [Ambulance Data](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData)폴더에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-143">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

## <a name="set-relevant-acls-on-the-sample-data"></a><span data-ttu-id="ccb87-144">샘플 데이터에서 관련 ACL 설정</span><span class="sxs-lookup"><span data-stu-id="ccb87-144">Set relevant ACLs on the sample data</span></span>
<span data-ttu-id="ccb87-145">HDInsight 클러스터에서 업로드한 샘플 데이터에 액세스할 수 있는지 확인하려면 HDInsight 클러스터와 Data Lake Store 간의 ID를 설정하는 데 사용되는 Azure AD 응용 프로그램에서 액세스하려는 파일/폴더에 액세스할 수 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-145">To make sure the sample data you upload is accessible from the HDInsight cluster, you must ensure that the Azure AD application that is used to establish identity between the HDInsight cluster and Data Lake Store has access to the file/folder you are trying to access.</span></span> <span data-ttu-id="ccb87-146">이렇게 하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-146">To do this, perform the following steps.</span></span>

1. <span data-ttu-id="ccb87-147">HDInsight 클러스터 및 Data Lake Store와 연결된 Azure AD 응용 프로그램의 이름을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-147">Find the name of the Azure AD application that is associated with HDInsight cluster and the Data Lake Store.</span></span> <span data-ttu-id="ccb87-148">이름을 찾는 한 가지 방법은 Resource Manager 템플릿을 사용하여 만든 HDInsight 클러스터 블레이드를 열고 **클러스터 AAD ID** 탭을 클릭한 다음 **서비스 사용자 표시 이름** 값을 확인하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-148">One way to look for the name is to open the HDInsight cluster blade that you created using the Resource Manager template, click the **Cluster AAD Identity** tab, and look for the value of **Service Principal Display Name**.</span></span>
2. <span data-ttu-id="ccb87-149">이제 HDInsight 클러스터에서 액세스하려는 파일/폴더에서 Azure AD 응용 프로그램에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-149">Now, provide access to this Azure AD application on the file/folder that you want to access from the HDInsight cluster.</span></span> <span data-ttu-id="ccb87-150">Data Lake Store의 파일/폴더에 대한 올바른 ACL을 설정하려면 [Data Lake Store의 데이터 보안](data-lake-store-secure-data.md#filepermissions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ccb87-150">To set the right ACLs on the file/folder in Data Lake Store, see [Securing data in Data Lake Store](data-lake-store-secure-data.md#filepermissions).</span></span>

## <a name="run-test-jobs-on-the-hdinsight-cluster-to-use-the-data-lake-store"></a><span data-ttu-id="ccb87-151">HDInsight 클러스터에서 테스트 작업을 실행하여 데이터 레이크 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="ccb87-151">Run test jobs on the HDInsight cluster to use the Data Lake Store</span></span>
<span data-ttu-id="ccb87-152">HDInsight 클러스터를 구성한 후에 클러스터에서 테스트 작업을 실행하여 HDInsight 클러스터가 데이터 레이크 저장소에 액세스할 수 있는지 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-152">After you have configured an HDInsight cluster, you can run test jobs on the cluster to test that the HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="ccb87-153">이렇게 하려면 데이터 레이크 저장소에 이전에 업로드한 샘플 데이터를 사용하여 테이블을 만드는 샘플 Hive 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-153">To do so, we will run a sample Hive job that creates a table using the sample data that you uploaded earlier to your Data Lake Store.</span></span>

<span data-ttu-id="ccb87-154">이 섹션에서는 HDInsight Linux 클러스터로 SSH하고 샘플 Hive 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-154">In this section you will SSH into an HDInsight Linux cluster and run the a sample Hive query.</span></span> <span data-ttu-id="ccb87-155">Windows 클라이언트를 사용 중인 경우 **PuTTY**를 사용하는 것이 좋습니다([http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)에서 다운로드할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="ccb87-155">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="ccb87-156">PuTTY 사용에 대한 자세한 내용은 [Windows에서 HDInsight의 Linux 기반 Hadoop과 SSH 사용 ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ccb87-156">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

1. <span data-ttu-id="ccb87-157">연결되면 다음 명령을 사용하여 Hive CLI를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-157">Once connected, start the Hive CLI by using the following command:</span></span>

   ```
   hive
   ```
2. <span data-ttu-id="ccb87-158">CLI를 사용하여 다음 문을 입력하여 Data Lake 저장소에서 샘플 데이터를 사용한 **vehicles**라는 새 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-158">Using the CLI, enter the following statements to create a new table named **vehicles** by using the sample data in the Data Lake Store:</span></span>

   ```
   DROP TABLE vehicles;
   CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
   SELECT * FROM vehicles LIMIT 10;
   ```

   <span data-ttu-id="ccb87-159">다음과 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-159">You should see an output similar to the following:</span></span>

   ```
   1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
   1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
   1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
   1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
   1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
   1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
   1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
   1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
   1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
   1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1
   ```


## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="ccb87-160">HDFS 명령을 사용한 액세스 데이터 레이크 저장소</span><span class="sxs-lookup"><span data-stu-id="ccb87-160">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="ccb87-161">데이터 레이크 저장소를 사용하도록 HDInsight 클러스터를 구성한 후 HDFS 셸 명령을 사용하여 저장소에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-161">Once you have configured the HDInsight cluster to use Data Lake Store, you can use the HDFS shell commands to access the store.</span></span>

<span data-ttu-id="ccb87-162">이 섹션에서는 HDInsight Linux 클러스터로 SSH하고 HDFS 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-162">In this section you will SSH into an HDInsight Linux cluster and run the HDFS commands.</span></span> <span data-ttu-id="ccb87-163">Windows 클라이언트를 사용 중인 경우 **PuTTY**를 사용하는 것이 좋습니다([http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)에서 다운로드할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="ccb87-163">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="ccb87-164">PuTTY 사용에 대한 자세한 내용은 [Windows에서 HDInsight의 Linux 기반 Hadoop과 SSH 사용 ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ccb87-164">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

<span data-ttu-id="ccb87-165">연결되면 다음 HDFS 파일 시스템 명령을 사용하여 데이터 레이크 저장소에 파일을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-165">Once connected, use the following HDFS filesystem command to list the files in the Data Lake Store.</span></span>

```
hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/
```

<span data-ttu-id="ccb87-166">데이터 레이크 저장소에 이전에 업로드한 파일이 나열되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-166">This should list the file that you uploaded earlier to the Data Lake Store.</span></span>

```
15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
Found 1 items
-rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder
```

<span data-ttu-id="ccb87-167">`hdfs dfs -put` 명령을 사용하여 일부 파일을 데이터 레이크 저장소에 업로드한 다음 `hdfs dfs -ls`을(를) 사용하여 파일이 성공적으로 업로드되었는지 여부를 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccb87-167">You can also use the `hdfs dfs -put` command to upload some files to the Data Lake Store, and then use `hdfs dfs -ls` to verify whether the files were successfully uploaded.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ccb87-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ccb87-168">Next steps</span></span>
* [<span data-ttu-id="ccb87-169">Azure Storage Blob에서 Data Lake Store로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="ccb87-169">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-wasb-distcp.md)
