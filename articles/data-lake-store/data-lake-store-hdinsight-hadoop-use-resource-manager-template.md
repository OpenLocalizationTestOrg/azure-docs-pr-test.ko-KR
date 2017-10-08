---
title: "Azure 템플릿 toocreate aaaUse HDInsight 및 데이터 레이크 저장소 | Microsoft Docs"
description: "Azure 리소스 관리자 템플릿 toocreate를 사용 하 고 HDInsight 클러스터를 사용 하 여 Azure 데이터 레이크 저장소"
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
ms.openlocfilehash: eb88a626f2837dcc29295f3f73a91757059c3bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-hdinsight-cluster-with-data-lake-store-using-azure-resource-manager-template"></a><span data-ttu-id="e0ef9-103">Azure Resource Manager 템플릿을 사용하여 Data Lake Store로 HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="e0ef9-103">Create an HDInsight cluster with Data Lake Store using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e0ef9-104">포털 사용</span><span class="sxs-lookup"><span data-stu-id="e0ef9-104">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="e0ef9-105">PowerShell 사용(기본 저장소의 경우)</span><span class="sxs-lookup"><span data-stu-id="e0ef9-105">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="e0ef9-106">PowerShell 사용(추가 저장소의 경우)</span><span class="sxs-lookup"><span data-stu-id="e0ef9-106">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="e0ef9-107">Resource Manager 사용</span><span class="sxs-lookup"><span data-stu-id="e0ef9-107">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="e0ef9-108">Azure 데이터 레이크 저장소와 toouse Azure PowerShell tooconfigure HDInsight 클러스터 되는 방법에 대해 알아봅니다 **추가 저장소로**합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-108">Learn how toouse Azure PowerShell tooconfigure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span>

<span data-ttu-id="e0ef9-109">지원되는 클러스터 유형의 경우 Data Lake Store는 기본 저장소 또는 추가 저장소 계정으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-109">For supported cluster types, Data Lake Store be used as an default storage or additional storage account.</span></span> <span data-ttu-id="e0ef9-110">데이터 레이크 저장소는 추가 저장소로 사용 되는, hello 클러스터에 대 한 기본 저장소 계정 hello 계속 Azure 저장소 Blob (WASB) 이며 hello 클러스터 관련 파일 (예: 로그 등) 동안 hello 데이터 toohello 기본 저장소 계속 기록 했는지 원하는 tooprocess 데이터 레이크 저장소 계정에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-110">When Data Lake Store is used as additional storage, hello default storage account for hello clusters will still be Azure Storage Blobs (WASB) and hello cluster-related files (such as logs, etc.) are still written toohello default storage, while hello data that you want tooprocess can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="e0ef9-111">데이터 레이크 저장소를 사용 하 여 추가 저장소 계정으로 영향을 주지 않습니다 성능이 나 hello 기능 tooread/쓰기 toohello hello 클러스터에서 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-111">Using Data Lake Store as an additional storage account does not impact performance or hello ability tooread/write toohello storage from hello cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="e0ef9-112">HDInsight 클러스터 저장소에서 Data Lake Store 사용</span><span class="sxs-lookup"><span data-stu-id="e0ef9-112">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="e0ef9-113">Data Lake Store에서 HDInsight를 사용하는 몇 가지 중요한 고려 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-113">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="e0ef9-114">옵션 toocreate HDInsight 클러스터에 액세스할 수 있는 기본 저장소로 tooData Lake 저장소는 HDInsight 버전 3.5 및 3.6 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-114">Option toocreate HDInsight clusters with access tooData Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="e0ef9-115">옵션 toocreate HDInsight 클러스터에 액세스할 수 있는 추가 저장소로 tooData Lake 저장소는 HDInsight 버전 3.2, 3.4, 3.5, 및 3.6 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-115">Option toocreate HDInsight clusters with access tooData Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="e0ef9-116">이 문서에서 데이터 레이크 저장소를 추가 저장소로 사용하여 Hadoop 클러스터를 프로비저닝합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-116">In this article, we provision a Hadoop cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="e0ef9-117">기본 저장소로 데이터 레이크 저장소와 toocreate Hadoop 클러스터 되는 방법에 지침은 [Azure 포털을 사용 하 여 데이터 레이크 저장소는 HDInsight 클러스터 만들기](data-lake-store-hdinsight-hadoop-use-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-117">For instructions on how toocreate a Hadoop cluster with Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0ef9-118">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e0ef9-118">Prerequisites</span></span>
<span data-ttu-id="e0ef9-119">이 자습서를 시작 하기 전에 hello 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-119">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="e0ef9-120">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-120">**An Azure subscription**.</span></span> <span data-ttu-id="e0ef9-121">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-121">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="e0ef9-122">**Azure PowerShell 1.0 이상**.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-122">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="e0ef9-123">참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-123">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="e0ef9-124">**Azure Active Directory 서비스 사용자**.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-124">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="e0ef9-125">이 자습서의 단계는 방법에 지침을 제공 toocreate Azure AD에서 서비스 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-125">Steps in this tutorial provide instructions on how toocreate a service principal in Azure AD.</span></span> <span data-ttu-id="e0ef9-126">그러나는 Azure AD 관리자 toobe 수 toocreate 서비스 사용자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-126">However, you must be an Azure AD administrator toobe able toocreate a service principal.</span></span> <span data-ttu-id="e0ef9-127">Azure AD 관리자 인 경우이 필수 구성이 요소를 건너뛰고 hello 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-127">If you are an Azure AD administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    <span data-ttu-id="e0ef9-128">**Azure AD 관리자가 아닌 경우**, 수 tooperform hello 단계 필요한 toocreate 서비스 사용자 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-128">**If you are not an Azure AD administrator**, you will not be able tooperform hello steps required toocreate a service principal.</span></span> <span data-ttu-id="e0ef9-129">이 경우 먼저 Azure AD 관리자가 서비스 사용자를 만들어야 Data Lake Store와 HDInsight 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-129">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="e0ef9-130">또한 hello 서비스 사용자 사용 하 여 만들어야는 인증서에 설명 된 대로 [인증서로 서비스 사용자를 만들](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-130">Also, hello service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-hdinsight-cluster-with-azure-data-lake-store"></a><span data-ttu-id="e0ef9-131">Azure Data Lake Store로 HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="e0ef9-131">Create an HDInsight cluster with Azure Data Lake Store</span></span>
<span data-ttu-id="e0ef9-132">hello 리소스 관리자 템플릿 및 hello hello 템플릿을 사용 하 여 필수 구성 요소에는 GitHub에서 사용할 수 있는 [새 데이터 레이크 저장소를 사용 하 여 HDInsight Linux 클러스터 배포](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-132">hello Resource Manager template, and hello prerequisites for using hello template, are available on GitHub at [Deploy a HDInsight Linux cluster with new Data Lake Store](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage).</span></span> <span data-ttu-id="e0ef9-133">에 제공 된 링크 toocreate이 HDInsight 클러스터와 Azure 데이터 레이크 저장소로 저장소를 추가 하는 hello hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-133">Follow hello instructions provided at this link toocreate an HDInsight cluster with Azure Data Lake Store as hello additional storage.</span></span>

<span data-ttu-id="e0ef9-134">위에서 언급 한 hello 링크에서 지침 hello PowerShell이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-134">hello instructions at hello link mentioned above require PowerShell.</span></span> <span data-ttu-id="e0ef9-135">이러한 지침을 시작 하기 전에 tooyour Azure 계정에에서 로그인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-135">Before you start with those instructions, make sure you log in tooyour Azure account.</span></span> <span data-ttu-id="e0ef9-136">바탕 화면에서 새 Azure PowerShell 창을 열고 hello 조각 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-136">From your desktop, open a new Azure PowerShell window, and enter hello following snippets.</span></span> <span data-ttu-id="e0ef9-137">, 입력 정보 요청된 toolog 있는지 확인 하는 경우 로그인 할 hello 구독 admininistrators/소유자 중 하나로:</span><span class="sxs-lookup"><span data-stu-id="e0ef9-137">When prompted toolog in, make sure you log in as one of hello subscription admininistrators/owner:</span></span>

```
# Log in tooyour Azure account
Login-AzureRmAccount

# List all hello subscriptions associated tooyour account
Get-AzureRmSubscription

# Select a subscription
Set-AzureRmContext -SubscriptionId <subscription ID>
```

## <a name="upload-sample-data-toohello-azure-data-lake-store"></a><span data-ttu-id="e0ef9-138">샘플 데이터 toohello Azure Data Lake 저장소에 업로드</span><span class="sxs-lookup"><span data-stu-id="e0ef9-138">Upload sample data toohello Azure Data Lake Store</span></span>
<span data-ttu-id="e0ef9-139">hello 리소스 관리자 템플릿을 새 데이터 레이크 저장소 계정을 만들고 hello HDInsight 클러스터에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-139">hello Resource Manager template creates a new Data Lake Store account and associates it with hello HDInsight cluster.</span></span> <span data-ttu-id="e0ef9-140">지금 일부 샘플 데이터 toohello Data Lake 저장소를 업로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-140">You must now upload some sample data toohello Data Lake Store.</span></span> <span data-ttu-id="e0ef9-141">Hello 데이터 레이크 저장소의에서 데이터를 액세스 하는 HDInsight 클러스터에서 hello 자습서 toorun 작업에서 나중에이 데이터를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-141">You'll need this data later in hello tutorial toorun jobs from an HDInsight cluster that access data in hello Data Lake Store.</span></span> <span data-ttu-id="e0ef9-142">방법에 대 한 지침은 tooupload 데이터 참조 [파일 tooyour 데이터 레이크 저장소 업로드](data-lake-store-get-started-portal.md#uploaddata)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-142">For instructions on how tooupload data, see [Upload a file tooyour Data Lake Store](data-lake-store-get-started-portal.md#uploaddata).</span></span> <span data-ttu-id="e0ef9-143">몇 가지 샘플 데이터 tooupload를 찾고 hello를 얻을 수 있습니다 **Ambulance 데이터** hello 폴더 [Azure 데이터 레이크 Git 리포지토리](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-143">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

## <a name="set-relevant-acls-on-hello-sample-data"></a><span data-ttu-id="e0ef9-144">Hello 예제 데이터에서 관련 Acl 설정</span><span class="sxs-lookup"><span data-stu-id="e0ef9-144">Set relevant ACLs on hello sample data</span></span>
<span data-ttu-id="e0ef9-145">toomake hello 샘플 데이터 업로드 hello HDInsight 클러스터에서 액세스할 수 있는지를 확인 해야 hello HDInsight 클러스터와 데이터 레이크 저장소 간에 사용 되는 tooestablish id가 있는 hello Azure AD 응용 프로그램에는 액세스 toohello 파일/폴더는 tooaccess를 하려고합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-145">toomake sure hello sample data you upload is accessible from hello HDInsight cluster, you must ensure that hello Azure AD application that is used tooestablish identity between hello HDInsight cluster and Data Lake Store has access toohello file/folder you are trying tooaccess.</span></span> <span data-ttu-id="e0ef9-146">toodo이 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-146">toodo this, perform hello following steps.</span></span>

1. <span data-ttu-id="e0ef9-147">Hello HDInsight 클러스터와 연결 된 Azure AD 응용 프로그램 및 hello 데이터 레이크 저장소의 hello 이름을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-147">Find hello name of hello Azure AD application that is associated with HDInsight cluster and hello Data Lake Store.</span></span> <span data-ttu-id="e0ef9-148">Hello 이름에 대 한 한 가지 방법은 toolook tooopen hello HDInsight 클러스터 블레이드 hello 리소스 관리자 템플릿을 사용 하 여 만든 이면 hello 클릭 **클러스터 AAD Id** 탭을 hello 값 찾기 위해 **서비스 사용자 표시 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-148">One way toolook for hello name is tooopen hello HDInsight cluster blade that you created using hello Resource Manager template, click hello **Cluster AAD Identity** tab, and look for hello value of **Service Principal Display Name**.</span></span>
2. <span data-ttu-id="e0ef9-149">이제 hello 파일/폴더 tooaccess hello HDInsight 클러스터에서 원하는 액세스 toothis Azure AD 응용 프로그램을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-149">Now, provide access toothis Azure AD application on hello file/folder that you want tooaccess from hello HDInsight cluster.</span></span> <span data-ttu-id="e0ef9-150">데이터 레이크 저장소의 파일/폴더 hello tooset hello 오른쪽 Acl 참조 [데이터 레이크 저장소의 데이터를 보호 하려면](data-lake-store-secure-data.md#filepermissions)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-150">tooset hello right ACLs on hello file/folder in Data Lake Store, see [Securing data in Data Lake Store](data-lake-store-secure-data.md#filepermissions).</span></span>

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a><span data-ttu-id="e0ef9-151">Hello HDInsight 클러스터 toouse hello 데이터 레이크 저장소에서 테스트 작업 실행</span><span class="sxs-lookup"><span data-stu-id="e0ef9-151">Run test jobs on hello HDInsight cluster toouse hello Data Lake Store</span></span>
<span data-ttu-id="e0ef9-152">HDInsight 클러스터를 구성 하 고 나면에서 실행할 수 있습니다 테스트 작업이 hello 클러스터 tootest 해당 hello HDInsight 클러스터 Data Lake 저장소에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-152">After you have configured an HDInsight cluster, you can run test jobs on hello cluster tootest that hello HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="e0ef9-153">toodo, 이전 tooyour 데이터 레이크 저장소를 업로드 하는 hello 샘플 데이터를 사용 하 여 테이블을 만드는 예제 Hive 작업을 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-153">toodo so, we will run a sample Hive job that creates a table using hello sample data that you uploaded earlier tooyour Data Lake Store.</span></span>

<span data-ttu-id="e0ef9-154">이 섹션에서는 SSH HDInsight Linux 클러스터와 실행된 hello에 샘플 Hive 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-154">In this section you will SSH into an HDInsight Linux cluster and run hello a sample Hive query.</span></span> <span data-ttu-id="e0ef9-155">Windows 클라이언트를 사용 중인 경우 **PuTTY**를 사용하는 것이 좋습니다([http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)에서 다운로드할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="e0ef9-155">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="e0ef9-156">PuTTY 사용에 대한 자세한 내용은 [Windows에서 HDInsight의 Linux 기반 Hadoop과 SSH 사용 ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-156">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

1. <span data-ttu-id="e0ef9-157">연결 되 면 다음 명령을 hello를 사용 하 여 hello 하이브 CLI를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-157">Once connected, start hello Hive CLI by using hello following command:</span></span>

   ```
   hive
   ```
2. <span data-ttu-id="e0ef9-158">Hello CLI를 사용 하 여 hello 문을 toocreate 라는 새 테이블을 다음 입력 **차량** hello 데이터 레이크 저장소의에서 hello 예제 데이터를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="e0ef9-158">Using hello CLI, enter hello following statements toocreate a new table named **vehicles** by using hello sample data in hello Data Lake Store:</span></span>

   ```
   DROP TABLE vehicles;
   CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
   SELECT * FROM vehicles LIMIT 10;
   ```

   <span data-ttu-id="e0ef9-159">출력 유사한 toohello 다음을 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-159">You should see an output similar toohello following:</span></span>

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


## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="e0ef9-160">HDFS 명령을 사용한 액세스 데이터 레이크 저장소</span><span class="sxs-lookup"><span data-stu-id="e0ef9-160">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="e0ef9-161">Hello HDInsight 클러스터 toouse Data Lake 저장소를 구성한 후에 hello HDFS 셸 명령을 tooaccess hello 저장소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-161">Once you have configured hello HDInsight cluster toouse Data Lake Store, you can use hello HDFS shell commands tooaccess hello store.</span></span>

<span data-ttu-id="e0ef9-162">이 섹션에서는 SSH HDInsight Linux 클러스터 및 실행된 hello HDFS 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-162">In this section you will SSH into an HDInsight Linux cluster and run hello HDFS commands.</span></span> <span data-ttu-id="e0ef9-163">Windows 클라이언트를 사용 중인 경우 **PuTTY**를 사용하는 것이 좋습니다([http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)에서 다운로드할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="e0ef9-163">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="e0ef9-164">PuTTY 사용에 대한 자세한 내용은 [Windows에서 HDInsight의 Linux 기반 Hadoop과 SSH 사용 ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-164">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

<span data-ttu-id="e0ef9-165">연결 되 면 hello Data Lake 저장소에 있는 HDFS 파일 시스템 명령 toolist hello 파일을 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-165">Once connected, use hello following HDFS filesystem command toolist hello files in hello Data Lake Store.</span></span>

```
hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/
```

<span data-ttu-id="e0ef9-166">이전 toohello 데이터 레이크 저장소를 업로드 하는 hello 파일을 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-166">This should list hello file that you uploaded earlier toohello Data Lake Store.</span></span>

```
15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
Found 1 items
-rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder
```

<span data-ttu-id="e0ef9-167">Hello를 사용할 수도 있습니다 `hdfs dfs -put` 일부 파일 toohello 데이터 레이크 저장소 tooupload 명령을 클릭 한 다음 사용 하 여 `hdfs dfs -ls` tooverify hello 파일이 성공적으로 업로드 된 여부.</span><span class="sxs-lookup"><span data-stu-id="e0ef9-167">You can also use hello `hdfs dfs -put` command tooupload some files toohello Data Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e0ef9-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e0ef9-168">Next steps</span></span>
* [<span data-ttu-id="e0ef9-169">Azure 저장소 Blob tooData Lake 저장소에서 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="e0ef9-169">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-wasb-distcp.md)
