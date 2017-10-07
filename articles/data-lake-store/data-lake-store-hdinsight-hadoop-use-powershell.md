---
<span data-ttu-id="a598d-101">제목: aaa "PowerShell: 추가 기능 저장소로 데이터 레이크 저장소와 Azure HDInsight 클러스터 | Microsoft Docs "서비스: 데이터 레이크-저장소, hdinsight documentationcenter: ' 작성자: nitinme 관리자: jhubbard 편집기: cgronlun</span><span class="sxs-lookup"><span data-stu-id="a598d-101">title: aaa"PowerShell: Azure HDInsight cluster with Data Lake Store as add-on storage | Microsoft Docs" services: data-lake-store,hdinsight documentationcenter: '' author: nitinme manager: jhubbard editor: cgronlun</span></span>

<span data-ttu-id="a598d-102">ms.assetid: 164ada5a-222e-4be2-bd32-e51dbe993bc0 ms.service: 데이터 레이크 저장소 ms.devlang: na ms.topic: article ms.tgt_pltfrm: na ms.workload: 빅 데이터 ms.date: 06/08/2017 ms.author: nitinme</span><span class="sxs-lookup"><span data-stu-id="a598d-102">ms.assetid: 164ada5a-222e-4be2-bd32-e51dbe993bc0 ms.service: data-lake-store ms.devlang: na ms.topic: article ms.tgt_pltfrm: na ms.workload: big-data ms.date: 06/08/2017 ms.author: nitinme</span></span>

---
# <a name="use-azure-powershell-toocreate-an-hdinsight-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="a598d-103">데이터 레이크 저장소와 Azure PowerShell toocreate HDInsight 클러스터를 사용 하 여 (으로 추가 저장소)</span><span class="sxs-lookup"><span data-stu-id="a598d-103">Use Azure PowerShell toocreate an HDInsight cluster with Data Lake Store (as additional storage)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a598d-104">포털 사용</span><span class="sxs-lookup"><span data-stu-id="a598d-104">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="a598d-105">PowerShell 사용(기본 저장소의 경우)</span><span class="sxs-lookup"><span data-stu-id="a598d-105">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="a598d-106">PowerShell 사용(추가 저장소의 경우)</span><span class="sxs-lookup"><span data-stu-id="a598d-106">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="a598d-107">Resource Manager 사용</span><span class="sxs-lookup"><span data-stu-id="a598d-107">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="a598d-108">Azure 데이터 레이크 저장소와 toouse Azure PowerShell tooconfigure HDInsight 클러스터 되는 방법에 대해 알아봅니다 **추가 저장소로**합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-108">Learn how toouse Azure PowerShell tooconfigure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span> <span data-ttu-id="a598d-109">기본 저장소로 Azure 데이터 레이크 저장소와 toocreate HDInsight 클러스터 되는 방법에 지침은 [기본 저장소로 데이터 레이크 저장소와 HDInsight 클러스터를 만드는](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-109">For instructions on how toocreate an HDInsight cluster with Azure Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store as default storage](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a598d-110">HDInsight 클러스터에 대 한 추가 저장소로 toouse Azure 데이터 레이크 저장소 하려는 경우 이렇게 하는 동안이 문서에 설명 된 대로 hello 클러스터를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-110">If you are going toouse Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create hello cluster as described in this article.</span></span> <span data-ttu-id="a598d-111">추가 저장소 tooan로 Azure 데이터 레이크 저장소 추가 기존 HDInsight 클러스터는 복잡 한 프로세스 및 tooerrors 발생 하기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-111">Adding Azure Data Lake Store as additional storage tooan existing HDInsight cluster is a complicated process and prone tooerrors.</span></span>
>

<span data-ttu-id="a598d-112">지원되는 클러스터 유형의 경우 Data Lake Store는 기본 저장소 또는 추가 저장소 계정으로 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-112">For supported cluster types, Data Lake Store can be used as a default storage or additional storage account.</span></span> <span data-ttu-id="a598d-113">데이터 레이크 저장소는 추가 저장소로 사용 되는, hello 클러스터에 대 한 기본 저장소 계정 hello 계속 Azure 저장소 Blob (WASB) 이며 hello 클러스터 관련 파일 (예: 로그 등) 동안 hello 데이터 toohello 기본 저장소 계속 기록 했는지 원하는 tooprocess 데이터 레이크 저장소 계정에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-113">When Data Lake Store is used as additional storage, hello default storage account for hello clusters will still be Azure Storage Blobs (WASB) and hello cluster-related files (such as logs, etc.) are still written toohello default storage, while hello data that you want tooprocess can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="a598d-114">데이터 레이크 저장소를 사용 하 여 추가 저장소 계정으로 영향을 주지 않습니다 성능이 나 hello 기능 tooread/쓰기 toohello hello 클러스터에서 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-114">Using Data Lake Store as an additional storage account does not impact performance or hello ability tooread/write toohello storage from hello cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="a598d-115">HDInsight 클러스터 저장소에서 Data Lake Store 사용</span><span class="sxs-lookup"><span data-stu-id="a598d-115">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="a598d-116">Data Lake Store에서 HDInsight를 사용하는 몇 가지 중요한 고려 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-116">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="a598d-117">옵션 toocreate HDInsight 클러스터에 액세스할 수 있는 추가 저장소로 tooData Lake 저장소는 HDInsight 버전 3.2, 3.4, 3.5, 및 3.6 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-117">Option toocreate HDInsight clusters with access tooData Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="a598d-118">PowerShell을 사용 하 여 데이터 레이크 저장소와 toowork HDInsight를 구성할 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-118">Configuring HDInsight toowork with Data Lake Store using PowerShell involves hello following steps:</span></span>

* <span data-ttu-id="a598d-119">Azure 데이터 레이크 저장소 만들기</span><span class="sxs-lookup"><span data-stu-id="a598d-119">Create an Azure Data Lake Store</span></span>
* <span data-ttu-id="a598d-120">역할 기반 인증에 대 한 설정 tooData 레이크 스토어에 액세스</span><span class="sxs-lookup"><span data-stu-id="a598d-120">Set up authentication for role-based access tooData Lake Store</span></span>
* <span data-ttu-id="a598d-121">인증 tooData Lake 저장소에 HDInsight 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-121">Create HDInsight cluster with authentication tooData Lake Store</span></span>
* <span data-ttu-id="a598d-122">Hello 클러스터에서 테스트 작업 실행</span><span class="sxs-lookup"><span data-stu-id="a598d-122">Run a test job on hello cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a598d-123">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a598d-123">Prerequisites</span></span>
<span data-ttu-id="a598d-124">이 자습서를 시작 하기 전에 hello 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-124">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="a598d-125">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="a598d-125">**An Azure subscription**.</span></span> <span data-ttu-id="a598d-126">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a598d-126">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a598d-127">**Azure PowerShell 1.0 이상**.</span><span class="sxs-lookup"><span data-stu-id="a598d-127">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="a598d-128">참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-128">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="a598d-129">**Windows SDK**.</span><span class="sxs-lookup"><span data-stu-id="a598d-129">**Windows SDK**.</span></span> <span data-ttu-id="a598d-130">[여기](https://dev.windows.com/en-us/downloads)에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-130">You can install it from [here](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="a598d-131">이 toocreate 보안 인증서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-131">You use this toocreate a security certificate.</span></span>
* <span data-ttu-id="a598d-132">**Azure Active Directory 서비스 사용자**.</span><span class="sxs-lookup"><span data-stu-id="a598d-132">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="a598d-133">이 자습서의 단계는 방법에 지침을 제공 toocreate Azure AD에서 서비스 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-133">Steps in this tutorial provide instructions on how toocreate a service principal in Azure AD.</span></span> <span data-ttu-id="a598d-134">그러나는 Azure AD 관리자 toobe 수 toocreate 서비스 사용자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-134">However, you must be an Azure AD administrator toobe able toocreate a service principal.</span></span> <span data-ttu-id="a598d-135">Azure AD 관리자 인 경우이 필수 구성이 요소를 건너뛰고 hello 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-135">If you are an Azure AD administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    <span data-ttu-id="a598d-136">**Azure AD 관리자가 아닌 경우**, 수 tooperform hello 단계 필요한 toocreate 서비스 사용자 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-136">**If you are not an Azure AD administrator**, you will not be able tooperform hello steps required toocreate a service principal.</span></span> <span data-ttu-id="a598d-137">이 경우 먼저 Azure AD 관리자가 서비스 사용자를 만들어야 Data Lake Store와 HDInsight 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-137">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="a598d-138">또한 hello 서비스 사용자 사용 하 여 만들어야는 인증서에 설명 된 대로 [인증서로 서비스 사용자를 만들](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority)합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-138">Also, hello service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="a598d-139">Azure 데이터 레이크 저장소 만들기</span><span class="sxs-lookup"><span data-stu-id="a598d-139">Create an Azure Data Lake Store</span></span>
<span data-ttu-id="a598d-140">이러한 단계 toocreate 데이터 레이크 저장소를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-140">Follow these steps toocreate a Data Lake Store.</span></span>

1. <span data-ttu-id="a598d-141">바탕 화면에서 새 Azure PowerShell 창을 열고 다음 코드 조각 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-141">From your desktop, open a new Azure PowerShell window, and enter hello following snippet.</span></span> <span data-ttu-id="a598d-142">, 입력 정보 요청된 toolog 있는지 확인 하는 경우 로그인 할 hello 구독 관리자/소유자 중 하나로:</span><span class="sxs-lookup"><span data-stu-id="a598d-142">When prompted toolog in, make sure you log in as one of hello subscription administrator/owner:</span></span>

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

   > [!NOTE]
   > <span data-ttu-id="a598d-143">너무 유사한 오류가 나타나면`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid` 구독이 허용 목록 Azure 데이터 레이크 저장소에 있지 않기 수 있기 hello 데이터 레이크 저장소 리소스 공급자를 등록할 때.</span><span class="sxs-lookup"><span data-stu-id="a598d-143">If you receive an error similar too`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid` when registering hello Data Lake Store resource provider, it is possible that your subscription is not whitelisted for Azure Data Lake Store.</span></span> <span data-ttu-id="a598d-144">이 [지침](data-lake-store-get-started-portal.md)에 따라 Data Lake 저장소 공개 미리 보기에 대한 Azure 구독을 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-144">Make sure you enable your Azure subscription for Data Lake Store public preview by following these [instructions](data-lake-store-get-started-portal.md).</span></span>
   >
   >
2. <span data-ttu-id="a598d-145">Azure 데이터 레이크 저장소 계정은 Azure 리소스 그룹과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-145">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="a598d-146">Azure 리소스 그룹을 만드는 작업부터 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-146">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="a598d-147">다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-147">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="a598d-148">Azure 데이터 레이크 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-148">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="a598d-149">지정한 이름은 소문자와 숫자만 포함 해야 하는 hello 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-149">hello account name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="a598d-150">Hello 다음과 같은 출력을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-150">You should see an output like hello following:</span></span>

        ...
        ProvisioningState           : Succeeded
        State                       : Active
        CreationTime                : 5/5/2017 10:53:56 PM
        EncryptionState             : Enabled
        ...
        LastModifiedTime            : 5/5/2017 10:53:56 PM
        Endpoint                    : hdiadlstore.azuredatalakestore.net
        DefaultGroup                :
        Id                          : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp/providers/Microsoft.DataLakeStore/accounts/hdiadlstore
        Name                        : hdiadlstore
        Type                        : Microsoft.DataLakeStore/accounts
        Location                    : East US 2
        Tags                        : {}

5. <span data-ttu-id="a598d-151">데이터 레이크 몇 가지 샘플 데이터 tooAzure 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-151">Upload some sample data tooAzure Data Lake.</span></span> <span data-ttu-id="a598d-152">이 문서 tooverify hello 데이터는 HDInsight 클러스터에서 액세스할 수 있는 뒷부분에 나오는이 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-152">We'll use this later in this article tooverify that hello data is accessible from an HDInsight cluster.</span></span> <span data-ttu-id="a598d-153">몇 가지 샘플 데이터 tooupload를 찾고 hello를 얻을 수 있습니다 **Ambulance 데이터** hello 폴더 [Azure 데이터 레이크 Git 리포지토리](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData)합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-153">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

        $myrootdir = "/"
        Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\<path toodata>\vehicle1_09142014.csv" -Destination $myrootdir\vehicle1_09142014.csv


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a><span data-ttu-id="a598d-154">역할 기반 인증에 대 한 설정 tooData 레이크 스토어에 액세스</span><span class="sxs-lookup"><span data-stu-id="a598d-154">Set up authentication for role-based access tooData Lake Store</span></span>
<span data-ttu-id="a598d-155">모든 Azure 구독은 Azure Active Directory와 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-155">Every Azure subscription is associated with an Azure Active Directory.</span></span> <span data-ttu-id="a598d-156">사용자 및 서비스의 hello Azure 클래식 포털 또는 Azure 리소스 관리자 API를 사용 하 여 hello 구독 리소스에 액세스 하는 먼저 해당 Azure Active Directory에 인증 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-156">Users and services that access resources of hello subscription using hello Azure Classic Portal or Azure Resource Manager API must first authenticate with that Azure Active Directory.</span></span> <span data-ttu-id="a598d-157">액세스가는 hello Azure 리소스에 적절 한 역할을 지정 하 여 tooAzure 구독 및 서비스 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-157">Access is granted tooAzure subscriptions and services by assigning them hello appropriate role on an Azure resource.</span></span>  <span data-ttu-id="a598d-158">서비스에 대 한 서비스 사용자는 Azure Active Directory (AAD) hello에 hello 서비스를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-158">For services, a service principal identifies hello service in hello Azure Active Directory (AAD).</span></span> <span data-ttu-id="a598d-159">이 섹션에서는 HDInsight에 대 한 액세스 tooan Azure 리소스 (hello 이전에 만든 Azure 데이터 레이크 저장소 계정)와 같은 응용 프로그램 toogrant 서비스 어떻게 hello 응용 프로그램에 대 한 서비스 사용자를 만들고 Azure 통해 역할 toothat 할당 하 여 PowerShell입니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-159">This section illustrates how toogrant an application service, like HDInsight, access tooan Azure resource (hello Azure Data Lake Store account you created earlier) by creating a service principal for hello application and assigning roles toothat via Azure PowerShell.</span></span>

<span data-ttu-id="a598d-160">Azure 데이터 레이크에 대 한 Active Directory 인증을 tooset, hello 다음 작업을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-160">tooset up Active Directory authentication for Azure Data Lake, you must perform hello following tasks.</span></span>

* <span data-ttu-id="a598d-161">자체 서명된 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="a598d-161">Create a self-signed certificate</span></span>
* <span data-ttu-id="a598d-162">Azure Active Directory 및 서비스 주체의 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="a598d-162">Create an application in Azure Active Directory and a Service Principal</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="a598d-163">자체 서명된 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="a598d-163">Create a self-signed certificate</span></span>
<span data-ttu-id="a598d-164">있는지 [Windows SDK](https://dev.windows.com/en-us/downloads) 이 섹션의 단계를 hello 계속 하기 전에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-164">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with hello steps in this section.</span></span> <span data-ttu-id="a598d-165">또한 만들었어야 디렉터리와 같은 **C:\mycertdir**, hello 인증서를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-165">You must have also created a directory, such as **C:\mycertdir**, where hello certificate will be created.</span></span>

1. <span data-ttu-id="a598d-166">Hello PowerShell 창에서 Windows SDK를 설치한 toohello 위치로 이동 합니다 (일반적으로 `C:\Program Files (x86)\Windows Kits\10\bin\x86` hello를 사용 하 여 [MakeCert] [ makecert] 유틸리티 toocreate 자체 서명 된 인증서와 개인 키입니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-166">From hello PowerShell window, navigate toohello location where you installed Windows SDK (typically, `C:\Program Files (x86)\Windows Kits\10\bin\x86` and use hello [MakeCert][makecert] utility toocreate a self-signed certificate and a private key.</span></span> <span data-ttu-id="a598d-167">다음 명령을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-167">Use hello following commands.</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="a598d-168">입력 정보 요청된 tooenter hello 개인 키 암호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-168">You will be prompted tooenter hello private key password.</span></span> <span data-ttu-id="a598d-169">실행 된 후 hello 명령을 성공적으로 표시 됩니다는 **CertFile.cer** 및 **mykey.pvk** 지정한 hello 인증서 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-169">After hello command successfully executes, you should see a **CertFile.cer** and **mykey.pvk** in hello certificate directory you specified.</span></span>
2. <span data-ttu-id="a598d-170">사용 하 여 hello [Pvk2Pfx] [ pvk2pfx] 유틸리티 tooconvert hello.pvk와.cer 파일 MakeCert 만든된 tooa.pfx 파일에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-170">Use hello [Pvk2Pfx][pvk2pfx] utility tooconvert hello .pvk and .cer files that MakeCert created tooa .pfx file.</span></span> <span data-ttu-id="a598d-171">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-171">Run hello following command.</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="a598d-172">메시지가 표시 되 면 이전에 지정한 hello 개인 키 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-172">When prompted enter hello private key password you specified earlier.</span></span> <span data-ttu-id="a598d-173">hello에 대 한 사용자가 지정한 값 hello **po** 매개 변수는 hello 암호 hello.pfx 파일과 연결 된입니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-173">hello value you specify for hello **-po** parameter is hello password that is associated with hello .pfx file.</span></span> <span data-ttu-id="a598d-174">Hello 명령이 성공적으로 완료 된 후 지정한 hello 인증서 디렉터리에서 CertFile.pfx 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-174">After hello command successfully completes, you should also see a CertFile.pfx in hello certificate directory you specified.</span></span>

### <a name="create-an-azure-active-directory-and-a-service-principal"></a><span data-ttu-id="a598d-175">Azure Active Directory 및 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="a598d-175">Create an Azure Active Directory and a service principal</span></span>
<span data-ttu-id="a598d-176">Azure Active Directory 응용 프로그램에 대 한 hello 단계 toocreate 서비스 사용자를 수행이 섹션에서는 역할 toohello 서비스 사용자를 할당 한 인증서를 제공 하 여 hello 서비스 사용자로 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-176">In this section, you perform hello steps toocreate a service principal for an Azure Active Directory application, assign a role toohello service principal, and authenticate as hello service principal by providing a certificate.</span></span> <span data-ttu-id="a598d-177">Azure Active Directory에서 다음 명령을 toocreate hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-177">Run hello following commands toocreate an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="a598d-178">Hello를 hello PowerShell 콘솔 창에서 cmdlet 뒤에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-178">Paste hello following cmdlets in hello PowerShell console window.</span></span> <span data-ttu-id="a598d-179">Hello에 대 한 지정 hello 값이 있는지 확인 **-DisplayName** 속성은 고유 합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-179">Make sure hello value you specify for hello **-DisplayName** property is unique.</span></span> <span data-ttu-id="a598d-180">또한에 대 한 값을 hello **-홈 페이지** 및 **-IdentiferUris** 자리 표시자 값 이며 확인 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-180">Also, hello values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter hello password" # This is hello password you specified for hello .pfx file

        $certificatePFX = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($certificateFilePath, $password)

        $rawCertificateData = $certificatePFX.GetRawCertData()

        $credential = [System.Convert]::ToBase64String($rawCertificateData)

        $application = New-AzureRmADApplication `
            -DisplayName "HDIADL" `
            -HomePage "https://contoso.com" `
            -IdentifierUris "https://mycontoso.com" `
            -CertValue $credential  `
            -StartDate $certificatePFX.NotBefore  `
            -EndDate $certificatePFX.NotAfter

        $applicationId = $application.ApplicationId
2. <span data-ttu-id="a598d-181">Hello 응용 프로그램 ID를 사용 하 여 서비스 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a598d-181">Create a service principal using hello application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="a598d-182">Hello 서비스 보안 주체 액세스 toohello Data Lake 저장소 폴더와 hello 파일 hello HDInsight 클러스터에서 액세스할 수 있는 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-182">Grant hello service principal access toohello Data Lake Store folder and hello file that you will access from hello HDInsight cluster.</span></span> <span data-ttu-id="a598d-183">아래 hello 조각 hello 데이터 레이크 저장소 (복사한 hello 예제 데이터 파일), 계정 및 hello 파일 자체의 toohello 루트 액세스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-183">hello snippet below provides access toohello root of hello Data Lake Store account (where you copied hello sample data file), and hello file itself.</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /vehicle1_09142014.csv -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="a598d-184">Data Lake Store를 추가 저장소로 사용하여 HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="a598d-184">Create an HDInsight Linux cluster with Data Lake Store as additional storage</span></span>

<span data-ttu-id="a598d-185">이 섹션에서는 Data Lake Store를 추가 저장소로 사용하여 HDInsight 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-185">In this section, we create an HDInsight Hadoop Linux cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="a598d-186">이 릴리스에 대 한 hello HDInsight 클러스터와 hello Data Lake 저장소에에서 있어야 hello 동일한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-186">For this release, hello HDInsight cluster and hello Data Lake Store must be in hello same location.</span></span>

1. <span data-ttu-id="a598d-187">Hello 구독 테 넌 트 id입니다. 검색 시작</span><span class="sxs-lookup"><span data-stu-id="a598d-187">Start with retrieving hello subscription tenant ID.</span></span> <span data-ttu-id="a598d-188">나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-188">You will need that later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId
2. <span data-ttu-id="a598d-189">이 릴리스의 Hadoop 클러스터에 대 한 데이터 레이크 저장소만 사용할 수 추가 저장소로 hello 클러스터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-189">For this release, for a Hadoop cluster, Data Lake Store can only be used as an additional storage for hello cluster.</span></span> <span data-ttu-id="a598d-190">hello 기본 저장소 (WASB) hello Azure 저장소 blob을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-190">hello default storage will still be hello Azure storage blobs (WASB).</span></span> <span data-ttu-id="a598d-191">따라서 먼저 만들겠습니다 hello hello 클러스터에 필요한 저장소 계정 및 저장소 컨테이너.</span><span class="sxs-lookup"><span data-stu-id="a598d-191">So, we'll first create hello storage account and storage containers required for hello cluster.</span></span>

        # Create an Azure storage account
        $location = "East US 2"
        $storageAccountName = "<StorageAcccountName>"   # Provide a Storage account name

        New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $storageAccountName -Location $location -Type Standard_GRS

        # Create an Azure Blob Storage container
        $containerName = "<ContainerName>"              # Provide a container name
        $storageAccountKey = (Get-AzureRmStorageAccountKey -Name $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        New-AzureStorageContainer -Name $containerName -Context $destContext
3. <span data-ttu-id="a598d-192">Hello HDInsight 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-192">Create hello HDInsight cluster.</span></span> <span data-ttu-id="a598d-193">Hello 다음 cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-193">Use hello following cmdlets.</span></span>

        # Set these variables
        $clusterName = $containerName                   # As a best practice, have hello same name for hello cluster and container
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster -ClusterName $clusterName -ResourceGroupName $resourceGroupName -HttpCredential $httpCredentials -Location $location -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" -DefaultStorageAccountKey $storageAccountKey -DefaultStorageContainer $containerName  -ClusterSizeInNodes $clusterNodes -ClusterType Hadoop -Version "3.4" -OSType Linux -SshCredential $sshCredentials -ObjectID $objectId -AadTenantId $tenantID -CertificateFilePath $certificateFilePath -CertificatePassword $password

    <span data-ttu-id="a598d-194">Hello cmdlet이 성공적으로 완료 된 후 hello 클러스터 세부 정보를 나열 하는 출력을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-194">After hello cmdlet successfully completes, you should see an output listing hello cluster details.</span></span>


## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a><span data-ttu-id="a598d-195">Hello HDInsight 클러스터 toouse hello 데이터 레이크 저장소에서 테스트 작업 실행</span><span class="sxs-lookup"><span data-stu-id="a598d-195">Run test jobs on hello HDInsight cluster toouse hello Data Lake Store</span></span>
<span data-ttu-id="a598d-196">HDInsight 클러스터를 구성 하 고 나면에서 실행할 수 있습니다 테스트 작업이 hello 클러스터 tootest 해당 hello HDInsight 클러스터 Data Lake 저장소에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-196">After you have configured an HDInsight cluster, you can run test jobs on hello cluster tootest that hello HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="a598d-197">toodo, 이전 tooyour 데이터 레이크 저장소를 업로드 하는 hello 샘플 데이터를 사용 하 여 테이블을 만드는 예제 Hive 작업을 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-197">toodo so, we will run a sample Hive job that creates a table using hello sample data that you uploaded earlier tooyour Data Lake Store.</span></span>

<span data-ttu-id="a598d-198">이 섹션에서 HDInsight Linux 클러스터 만들고 hello 샘플 Hive 쿼리를 실행 하는 hello에 SSH 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-198">In this section you will SSH into hello HDInsight Linux cluster you created and run hello a sample Hive query.</span></span>

* <span data-ttu-id="a598d-199">Windows 클라이언트 tooSSH hello 클러스터를 사용 하는 경우 참조 [SSH를 Windows에서 HDInsight의 Linux 기반 Hadoop 사용](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-199">If you are using a Windows client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="a598d-200">Linux 클라이언트 tooSSH hello 클러스터를 사용 하는 경우 참조 [SSH Linux에서 HDInsight의 Hadoop Linux 기반를 사용](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="a598d-200">If you are using a Linux client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

1. <span data-ttu-id="a598d-201">연결 되 면 다음 명령을 hello를 사용 하 여 hello 하이브 CLI를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-201">Once connected, start hello Hive CLI by using hello following command:</span></span>

        hive
2. <span data-ttu-id="a598d-202">Hello CLI를 사용 하 여 hello 문을 toocreate 라는 새 테이블을 다음 입력 **차량** hello 데이터 레이크 저장소의에서 hello 예제 데이터를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="a598d-202">Using hello CLI, enter hello following statements toocreate a new table named **vehicles** by using hello sample data in hello Data Lake Store:</span></span>

        DROP TABLE vehicles;
        CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
        SELECT * FROM vehicles LIMIT 10;

    <span data-ttu-id="a598d-203">출력 유사한 toohello 다음을 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-203">You should see an output similar toohello following:</span></span>

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

## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="a598d-204">HDFS 명령을 사용한 액세스 데이터 레이크 저장소</span><span class="sxs-lookup"><span data-stu-id="a598d-204">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="a598d-205">Hello HDInsight 클러스터 toouse Data Lake 저장소를 구성한 후에 hello HDFS 셸 명령을 tooaccess hello 저장소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-205">Once you have configured hello HDInsight cluster toouse Data Lake Store, you can use hello HDFS shell commands tooaccess hello store.</span></span>

<span data-ttu-id="a598d-206">이 섹션에서 HDInsight Linux 클러스터 만들고 hello HDFS 명령을 실행 하는 hello에 SSH 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-206">In this section you will SSH into hello HDInsight Linux cluster you created and run hello HDFS commands.</span></span>

* <span data-ttu-id="a598d-207">Windows 클라이언트 tooSSH hello 클러스터를 사용 하는 경우 참조 [SSH를 Windows에서 HDInsight의 Linux 기반 Hadoop 사용](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-207">If you are using a Windows client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="a598d-208">Linux 클라이언트 tooSSH hello 클러스터를 사용 하는 경우 참조 [SSH Linux에서 HDInsight의 Hadoop Linux 기반를 사용](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="a598d-208">If you are using a Linux client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

<span data-ttu-id="a598d-209">연결 되 면 hello Data Lake 저장소에 있는 HDFS 파일 시스템 명령 toolist hello 파일을 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-209">Once connected, use hello following HDFS filesystem command toolist hello files in hello Data Lake Store.</span></span>

    hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/

<span data-ttu-id="a598d-210">이전 toohello 데이터 레이크 저장소를 업로드 하는 hello 파일을 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a598d-210">This should list hello file that you uploaded earlier toohello Data Lake Store.</span></span>

    15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
    Found 1 items
    -rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder

<span data-ttu-id="a598d-211">Hello를 사용할 수도 있습니다 `hdfs dfs -put` 일부 파일 toohello 데이터 레이크 저장소 tooupload 명령을 클릭 한 다음 사용 하 여 `hdfs dfs -ls` tooverify hello 파일이 성공적으로 업로드 된 여부.</span><span class="sxs-lookup"><span data-stu-id="a598d-211">You can also use hello `hdfs dfs -put` command tooupload some files toohello Data Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="a598d-212">참고 항목</span><span class="sxs-lookup"><span data-stu-id="a598d-212">See Also</span></span>
* [<span data-ttu-id="a598d-213">HDInsight 클러스터 toouse Data Lake 저장소를 만듭니다 포털:</span><span class="sxs-lookup"><span data-stu-id="a598d-213">Portal: Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
