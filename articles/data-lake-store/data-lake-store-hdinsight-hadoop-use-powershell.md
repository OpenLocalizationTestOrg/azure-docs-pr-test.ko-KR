---
title: "PowerShell: Data Lake Store를 추가 기능 저장소로 사용하는 Azure HDInsight 클러스터 | Microsoft Docs"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 164ada5a-222e-4be2-bd32-e51dbe993bc0
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/08/2017
ms.author: nitinme
ms.openlocfilehash: 7a7069adab5742a9dae2833c13a1db57337a41a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-powershell-to-create-an-hdinsight-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="b5eaf-102">Azure PowerShell을 사용하여 Data Lake Store를 (추가 저장소로) 사용하여 HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="b5eaf-102">Use Azure PowerShell to create an HDInsight cluster with Data Lake Store (as additional storage)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b5eaf-103">포털 사용</span><span class="sxs-lookup"><span data-stu-id="b5eaf-103">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="b5eaf-104">PowerShell 사용(기본 저장소의 경우)</span><span class="sxs-lookup"><span data-stu-id="b5eaf-104">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="b5eaf-105">PowerShell 사용(추가 저장소의 경우)</span><span class="sxs-lookup"><span data-stu-id="b5eaf-105">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="b5eaf-106">Resource Manager 사용</span><span class="sxs-lookup"><span data-stu-id="b5eaf-106">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="b5eaf-107">Azure PowerShell을 사용하여 Azure Data Lake Store에서 HDInsight 클러스터를 **추가 저장소로** 구성하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-107">Learn how to use Azure PowerShell to configure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span> <span data-ttu-id="b5eaf-108">기본 저장소로 Azure Data Lake Store를 사용하여 HDInsight 클러스터를 만드는 방법에 대한 지침은 [Data Lake Store를 기본 저장소로 사용하여 HDInsight 클러스터 만들기](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-108">For instructions on how to create an HDInsight cluster with Azure Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store as default storage](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b5eaf-109">Azure Data Lake Store를 HDInsight 클러스터의 추가 저장소로 사용하려는 경우 이 문서에서 설명한 대로 클러스터를 만드는 동안 이 작업을 수행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-109">If you are going to use Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create the cluster as described in this article.</span></span> <span data-ttu-id="b5eaf-110">기존의 HDInsight 클러스터에 Azure Data Lake Store를 추가 저장소로 추가하는 것은 복잡한 프로세스이며 오류가 발생하기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-110">Adding Azure Data Lake Store as additional storage to an existing HDInsight cluster is a complicated process and prone to errors.</span></span>
>

<span data-ttu-id="b5eaf-111">지원되는 클러스터 유형의 경우 Data Lake Store는 기본 저장소 또는 추가 저장소 계정으로 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-111">For supported cluster types, Data Lake Store can be used as a default storage or additional storage account.</span></span> <span data-ttu-id="b5eaf-112">Data Lake Store를 추가 저장소로 사용하는 경우 클러스터의 기본 저장소 계정은 여전히 Azure Storage Blob(WASB)이고 클러스터 관련 파일(예: 로그 등)은 여전히 기본 저장소에 기록되지만 처리하려는 데이터는 Data Lake Store 계정에 저장될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-112">When Data Lake Store is used as additional storage, the default storage account for the clusters will still be Azure Storage Blobs (WASB) and the cluster-related files (such as logs, etc.) are still written to the default storage, while the data that you want to process can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="b5eaf-113">Data Lake 저장소를 추가 저장소 계정으로 사용하면 클러스터에서 저장소로 읽고 쓰는 성능 또는 기능에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-113">Using Data Lake Store as an additional storage account does not impact performance or the ability to read/write to the storage from the cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="b5eaf-114">HDInsight 클러스터 저장소에서 Data Lake Store 사용</span><span class="sxs-lookup"><span data-stu-id="b5eaf-114">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="b5eaf-115">Data Lake Store에서 HDInsight를 사용하는 몇 가지 중요한 고려 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-115">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="b5eaf-116">추가 저장소로 Data Lake Store에 액세스할 수 있는 HDInsight 클러스터를 만드는 옵션은 HDInsight 버전 3.2, 3.4, 3.5 및 3.6에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-116">Option to create HDInsight clusters with access to Data Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="b5eaf-117">PowerShell을 사용하여 데이터 레이크 저장소와 함께 작동하도록 HDInsight를 구성하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-117">Configuring HDInsight to work with Data Lake Store using PowerShell involves the following steps:</span></span>

* <span data-ttu-id="b5eaf-118">Azure 데이터 레이크 저장소 만들기</span><span class="sxs-lookup"><span data-stu-id="b5eaf-118">Create an Azure Data Lake Store</span></span>
* <span data-ttu-id="b5eaf-119">데이터 레이크 저장소에 대한 역할 기반 액세스를 위한 인증 설정</span><span class="sxs-lookup"><span data-stu-id="b5eaf-119">Set up authentication for role-based access to Data Lake Store</span></span>
* <span data-ttu-id="b5eaf-120">데이터 레이크 저장소에 대한 인증을 사용하여 HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="b5eaf-120">Create HDInsight cluster with authentication to Data Lake Store</span></span>
* <span data-ttu-id="b5eaf-121">클러스터에서 테스트 작업 실행</span><span class="sxs-lookup"><span data-stu-id="b5eaf-121">Run a test job on the cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5eaf-122">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b5eaf-122">Prerequisites</span></span>
<span data-ttu-id="b5eaf-123">이 자습서를 시작하기 전에 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-123">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="b5eaf-124">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-124">**An Azure subscription**.</span></span> <span data-ttu-id="b5eaf-125">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-125">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b5eaf-126">**Azure PowerShell 1.0 이상**.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-126">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="b5eaf-127">[Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-127">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="b5eaf-128">**Windows SDK**.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-128">**Windows SDK**.</span></span> <span data-ttu-id="b5eaf-129">[여기](https://dev.windows.com/en-us/downloads)에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-129">You can install it from [here](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="b5eaf-130">이를 사용하여 보안 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-130">You use this to create a security certificate.</span></span>
* <span data-ttu-id="b5eaf-131">**Azure Active Directory 서비스 사용자**.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-131">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="b5eaf-132">이 자습서의 단계에서는 Azure AD에서 서비스 사용자를 만드는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-132">Steps in this tutorial provide instructions on how to create a service principal in Azure AD.</span></span> <span data-ttu-id="b5eaf-133">그러나 서비스 사용자를 만들려면 Azure AD 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-133">However, you must be an Azure AD administrator to be able to create a service principal.</span></span> <span data-ttu-id="b5eaf-134">Azure AD 관리자인 경우 이 필수 조건을 건너뛰고 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-134">If you are an Azure AD administrator, you can skip this prerequisite and proceed with the tutorial.</span></span>

    <span data-ttu-id="b5eaf-135">**Azure AD 관리자가 아닌 경우** 서비스 사용자를 만드는 데 필요한 단계를 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-135">**If you are not an Azure AD administrator**, you will not be able to perform the steps required to create a service principal.</span></span> <span data-ttu-id="b5eaf-136">이 경우 먼저 Azure AD 관리자가 서비스 사용자를 만들어야 Data Lake Store와 HDInsight 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-136">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="b5eaf-137">또한 [인증서를 사용하여 서비스 사용자 만들기](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority)에 설명된 대로 인증서를 사용하여 서비스 사용자를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-137">Also, the service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="b5eaf-138">Azure 데이터 레이크 저장소 만들기</span><span class="sxs-lookup"><span data-stu-id="b5eaf-138">Create an Azure Data Lake Store</span></span>
<span data-ttu-id="b5eaf-139">다음 단계에 따라 데이터 레이크 저장소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-139">Follow these steps to create a Data Lake Store.</span></span>

1. <span data-ttu-id="b5eaf-140">바탕 화면에서 새 Azure PowerShell 창을 열고 다음 코드 조각을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-140">From your desktop, open a new Azure PowerShell window, and enter the following snippet.</span></span> <span data-ttu-id="b5eaf-141">로그인하라는 메시지가 표시되면 구독 관리자/소유자 중 하나로 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-141">When prompted to log in, make sure you log in as one of the subscription administrator/owner:</span></span>

        # Log in to your Azure account
        Login-AzureRmAccount

        # List all the subscriptions associated to your account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

   > [!NOTE]
   > <span data-ttu-id="b5eaf-142">Data Lake Store 리소스 공급자를 등록할 때 `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid`와 유사한 오류가 나타나는 경우 구독이 Azure Data Lake Store에 대한 허용 목록에 추가되지 않았을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-142">If you receive an error similar to `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid` when registering the Data Lake Store resource provider, it is possible that your subscription is not whitelisted for Azure Data Lake Store.</span></span> <span data-ttu-id="b5eaf-143">이 [지침](data-lake-store-get-started-portal.md)에 따라 Data Lake 저장소 공개 미리 보기에 대한 Azure 구독을 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-143">Make sure you enable your Azure subscription for Data Lake Store public preview by following these [instructions](data-lake-store-get-started-portal.md).</span></span>
   >
   >
2. <span data-ttu-id="b5eaf-144">Azure 데이터 레이크 저장소 계정은 Azure 리소스 그룹과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-144">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="b5eaf-145">Azure 리소스 그룹을 만드는 작업부터 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-145">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="b5eaf-146">다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-146">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="b5eaf-147">Azure 데이터 레이크 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-147">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="b5eaf-148">지정하는 계정 이름은 소문자와 숫자만 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-148">The account name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="b5eaf-149">다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-149">You should see an output like the following:</span></span>

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

5. <span data-ttu-id="b5eaf-150">일부 샘플 데이터를 Azure 데이터 레이크에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-150">Upload some sample data to Azure Data Lake.</span></span> <span data-ttu-id="b5eaf-151">나중에 이 문서에서 사용하여 HDInsight 클러스터에서 데이터에 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-151">We'll use this later in this article to verify that the data is accessible from an HDInsight cluster.</span></span> <span data-ttu-id="b5eaf-152">업로드할 일부 샘플 데이터를 찾는 경우 **Azure 데이터 레이크 Git 리포지토리** 의 [Ambulance Data](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData)폴더에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-152">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

        $myrootdir = "/"
        Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\<path to data>\vehicle1_09142014.csv" -Destination $myrootdir\vehicle1_09142014.csv


## <a name="set-up-authentication-for-role-based-access-to-data-lake-store"></a><span data-ttu-id="b5eaf-153">데이터 레이크 저장소에 대한 역할 기반 액세스를 위한 인증 설정</span><span class="sxs-lookup"><span data-stu-id="b5eaf-153">Set up authentication for role-based access to Data Lake Store</span></span>
<span data-ttu-id="b5eaf-154">모든 Azure 구독은 Azure Active Directory와 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-154">Every Azure subscription is associated with an Azure Active Directory.</span></span> <span data-ttu-id="b5eaf-155">Azure 클래식 포털 또는 Azure 리소스 관리자 API를 사용하여 구독 리소스에 액세스하는 사용자와 서비스는 먼저 해당 Azure Active Directory에 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-155">Users and services that access resources of the subscription using the Azure Classic Portal or Azure Resource Manager API must first authenticate with that Azure Active Directory.</span></span> <span data-ttu-id="b5eaf-156">Azure 리소스에 대한 적절한 역할을 할당하여 Azure 구독과 서비스에 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-156">Access is granted to Azure subscriptions and services by assigning them the appropriate role on an Azure resource.</span></span>  <span data-ttu-id="b5eaf-157">서비스의 경우 서비스 주체는 Azure Active Directory(AAD)의 서비스를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-157">For services, a service principal identifies the service in the Azure Active Directory (AAD).</span></span> <span data-ttu-id="b5eaf-158">이 섹션에서는 서비스 주체를 만들고 Azure PowerShell을 통해 역할을 할당하여 HDInsight, Azure 리소스(이전에 만든 Azure 데이터 레이크 저장소 계정)에 대한 액세스와 같은 응용 프로그램 서비스를 부여하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-158">This section illustrates how to grant an application service, like HDInsight, access to an Azure resource (the Azure Data Lake Store account you created earlier) by creating a service principal for the application and assigning roles to that via Azure PowerShell.</span></span>

<span data-ttu-id="b5eaf-159">Azure 데이터 레이크에 대한 Active Directory 인증을 설정하려면 다음 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-159">To set up Active Directory authentication for Azure Data Lake, you must perform the following tasks.</span></span>

* <span data-ttu-id="b5eaf-160">자체 서명된 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="b5eaf-160">Create a self-signed certificate</span></span>
* <span data-ttu-id="b5eaf-161">Azure Active Directory 및 서비스 주체의 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="b5eaf-161">Create an application in Azure Active Directory and a Service Principal</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="b5eaf-162">자체 서명된 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="b5eaf-162">Create a self-signed certificate</span></span>
<span data-ttu-id="b5eaf-163">이 섹션의 단계를 진행하기 전에 [Windows SDK](https://dev.windows.com/en-us/downloads) 가 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-163">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with the steps in this section.</span></span> <span data-ttu-id="b5eaf-164">또한 인증서가 만들어지는 **C:\mycertdir**과 같은 디렉터리가 만들어져 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-164">You must have also created a directory, such as **C:\mycertdir**, where the certificate will be created.</span></span>

1. <span data-ttu-id="b5eaf-165">PowerShell 창에서 Windows SDK를 설치한 위치로 이동(일반적으로 `C:\Program Files (x86)\Windows Kits\10\bin\x86`)하고 [MakeCert][makecert] 유틸리티를 사용하여 자체 서명된 인증서와 개인 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-165">From the PowerShell window, navigate to the location where you installed Windows SDK (typically, `C:\Program Files (x86)\Windows Kits\10\bin\x86` and use the [MakeCert][makecert] utility to create a self-signed certificate and a private key.</span></span> <span data-ttu-id="b5eaf-166">다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-166">Use the following commands.</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="b5eaf-167">개인 키 암호를 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-167">You will be prompted to enter the private key password.</span></span> <span data-ttu-id="b5eaf-168">명령을 성공적으로 실행한 후 지정한 인증서 디렉터리에서 **CertFile.cer** 및 **mykey.pvk**를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-168">After the command successfully executes, you should see a **CertFile.cer** and **mykey.pvk** in the certificate directory you specified.</span></span>
2. <span data-ttu-id="b5eaf-169">[Pvk2Pfx][pvk2pfx] 유틸리티를 사용하여 MakeCert가 생성한 .pvk 및 .cer 파일을 .pfx 파일로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-169">Use the [Pvk2Pfx][pvk2pfx] utility to convert the .pvk and .cer files that MakeCert created to a .pfx file.</span></span> <span data-ttu-id="b5eaf-170">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-170">Run the following command.</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="b5eaf-171">메시지가 표시되면 이전에 지정한 개인 키 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-171">When prompted enter the private key password you specified earlier.</span></span> <span data-ttu-id="b5eaf-172">**-po** 매개 변수에 대해 지정한 값은 .pfx 파일에 연관된 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-172">The value you specify for the **-po** parameter is the password that is associated with the .pfx file.</span></span> <span data-ttu-id="b5eaf-173">명령을 성공적으로 완료한 후 지정한 인증서 디렉터리에서 CertFile.pfx도 또한 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-173">After the command successfully completes, you should also see a CertFile.pfx in the certificate directory you specified.</span></span>

### <a name="create-an-azure-active-directory-and-a-service-principal"></a><span data-ttu-id="b5eaf-174">Azure Active Directory 및 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="b5eaf-174">Create an Azure Active Directory and a service principal</span></span>
<span data-ttu-id="b5eaf-175">이 섹션에서는 Azure Active Directory 응용 프로그램용 서비스 주체를 만들고, 서비스 주체에 역할을 할당하고, 인증서를 제공하여 서비스 주체로 인증하는 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-175">In this section, you perform the steps to create a service principal for an Azure Active Directory application, assign a role to the service principal, and authenticate as the service principal by providing a certificate.</span></span> <span data-ttu-id="b5eaf-176">다음 명령을 실행하여 Azure Active Directory에서 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-176">Run the following commands to create an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="b5eaf-177">PowerShell 콘솔 창에 다음 cmdlet을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-177">Paste the following cmdlets in the PowerShell console window.</span></span> <span data-ttu-id="b5eaf-178">**-DisplayName** 속성에 대해 지정한 값이 고유한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-178">Make sure the value you specify for the **-DisplayName** property is unique.</span></span> <span data-ttu-id="b5eaf-179">또한 **-HomePage** 및 **-IdentiferUris**에 대한 값은 자리 표시자이며 확인되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-179">Also, the values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter the password" # This is the password you specified for the .pfx file

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
2. <span data-ttu-id="b5eaf-180">응용 프로그램 ID를 사용하여 서비스 주체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-180">Create a service principal using the application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="b5eaf-181">서비스 주체에게 HDInsight 클러스터에서 액세스할 Data Lake Store 폴더 및 파일에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-181">Grant the service principal access to the Data Lake Store folder and the file that you will access from the HDInsight cluster.</span></span> <span data-ttu-id="b5eaf-182">아래 코드 조각은 Data Lake Store 계정의 루트(샘플 데이터 파일을 복사한 위치)와 파일 자체에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-182">The snippet below provides access to the root of the Data Lake Store account (where you copied the sample data file), and the file itself.</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /vehicle1_09142014.csv -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="b5eaf-183">Data Lake Store를 추가 저장소로 사용하여 HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="b5eaf-183">Create an HDInsight Linux cluster with Data Lake Store as additional storage</span></span>

<span data-ttu-id="b5eaf-184">이 섹션에서는 Data Lake Store를 추가 저장소로 사용하여 HDInsight 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-184">In this section, we create an HDInsight Hadoop Linux cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="b5eaf-185">이 릴리스의 경우 HDInsight 클러스터와 Data Lake Store는 동일한 위치에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-185">For this release, the HDInsight cluster and the Data Lake Store must be in the same location.</span></span>

1. <span data-ttu-id="b5eaf-186">구독 테넌트 ID 검색을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-186">Start with retrieving the subscription tenant ID.</span></span> <span data-ttu-id="b5eaf-187">나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-187">You will need that later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId
2. <span data-ttu-id="b5eaf-188">이 릴리스에서 Hadoop 클러스터의 경우 데이터 레이크 저장소는 클러스터에 대해 추가 저장소로만 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-188">For this release, for a Hadoop cluster, Data Lake Store can only be used as an additional storage for the cluster.</span></span> <span data-ttu-id="b5eaf-189">기본 저장소는 여전히 Azure 저장소 Blob(WASB)이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-189">The default storage will still be the Azure storage blobs (WASB).</span></span> <span data-ttu-id="b5eaf-190">따라서 먼저 클러스터에 필요한 저장소 계정 및 저장소 컨테이너를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-190">So, we'll first create the storage account and storage containers required for the cluster.</span></span>

        # Create an Azure storage account
        $location = "East US 2"
        $storageAccountName = "<StorageAcccountName>"   # Provide a Storage account name

        New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $storageAccountName -Location $location -Type Standard_GRS

        # Create an Azure Blob Storage container
        $containerName = "<ContainerName>"              # Provide a container name
        $storageAccountKey = (Get-AzureRmStorageAccountKey -Name $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        New-AzureStorageContainer -Name $containerName -Context $destContext
3. <span data-ttu-id="b5eaf-191">HDInsight 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-191">Create the HDInsight cluster.</span></span> <span data-ttu-id="b5eaf-192">다음 cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-192">Use the following cmdlets.</span></span>

        # Set these variables
        $clusterName = $containerName                   # As a best practice, have the same name for the cluster and container
        $clusterNodes = <ClusterSizeInNodes>            # The number of nodes in the HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster -ClusterName $clusterName -ResourceGroupName $resourceGroupName -HttpCredential $httpCredentials -Location $location -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" -DefaultStorageAccountKey $storageAccountKey -DefaultStorageContainer $containerName  -ClusterSizeInNodes $clusterNodes -ClusterType Hadoop -Version "3.4" -OSType Linux -SshCredential $sshCredentials -ObjectID $objectId -AadTenantId $tenantID -CertificateFilePath $certificateFilePath -CertificatePassword $password

    <span data-ttu-id="b5eaf-193">cmdlet이 성공적으로 완료된 후 클러스터 세부 정보가 나열되는 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-193">After the cmdlet successfully completes, you should see an output listing the cluster details.</span></span>


## <a name="run-test-jobs-on-the-hdinsight-cluster-to-use-the-data-lake-store"></a><span data-ttu-id="b5eaf-194">HDInsight 클러스터에서 테스트 작업을 실행하여 데이터 레이크 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="b5eaf-194">Run test jobs on the HDInsight cluster to use the Data Lake Store</span></span>
<span data-ttu-id="b5eaf-195">HDInsight 클러스터를 구성한 후에 클러스터에서 테스트 작업을 실행하여 HDInsight 클러스터가 데이터 레이크 저장소에 액세스할 수 있는지 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-195">After you have configured an HDInsight cluster, you can run test jobs on the cluster to test that the HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="b5eaf-196">이렇게 하려면 데이터 레이크 저장소에 이전에 업로드한 샘플 데이터를 사용하여 테이블을 만드는 샘플 Hive 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-196">To do so, we will run a sample Hive job that creates a table using the sample data that you uploaded earlier to your Data Lake Store.</span></span>

<span data-ttu-id="b5eaf-197">이 섹션에서는 사용자가 만든 HDInsight Linux 클러스터로 SSH하고 샘플 Hive 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-197">In this section you will SSH into the HDInsight Linux cluster you created and run the a sample Hive query.</span></span>

* <span data-ttu-id="b5eaf-198">Windows 클라이언트를 사용하여 클러스터로 SSH하는 경우 [Windows에서 HDInsight의 Linux 기반 Hadoop과 SSH 사용](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-198">If you are using a Windows client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="b5eaf-199">Linux 클라이언트를 사용하여 클러스터로 SSH하는 경우 [Linux에서 HDInsight의 Linux 기반 Hadoop과 SSH 사용](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-199">If you are using a Linux client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

1. <span data-ttu-id="b5eaf-200">연결되면 다음 명령을 사용하여 Hive CLI를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-200">Once connected, start the Hive CLI by using the following command:</span></span>

        hive
2. <span data-ttu-id="b5eaf-201">CLI를 사용하여 다음 문을 입력하여 Data Lake 저장소에서 샘플 데이터를 사용한 **vehicles**라는 새 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-201">Using the CLI, enter the following statements to create a new table named **vehicles** by using the sample data in the Data Lake Store:</span></span>

        DROP TABLE vehicles;
        CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
        SELECT * FROM vehicles LIMIT 10;

    <span data-ttu-id="b5eaf-202">다음과 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-202">You should see an output similar to the following:</span></span>

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

## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="b5eaf-203">HDFS 명령을 사용한 액세스 데이터 레이크 저장소</span><span class="sxs-lookup"><span data-stu-id="b5eaf-203">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="b5eaf-204">데이터 레이크 저장소를 사용하도록 HDInsight 클러스터를 구성한 후 HDFS 셸 명령을 사용하여 저장소에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-204">Once you have configured the HDInsight cluster to use Data Lake Store, you can use the HDFS shell commands to access the store.</span></span>

<span data-ttu-id="b5eaf-205">이 섹션에서는 사용자가 만든 HDInsight Linux 클러스터로 SSH하고 HDFS 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-205">In this section you will SSH into the HDInsight Linux cluster you created and run the HDFS commands.</span></span>

* <span data-ttu-id="b5eaf-206">Windows 클라이언트를 사용하여 클러스터로 SSH하는 경우 [Windows에서 HDInsight의 Linux 기반 Hadoop과 SSH 사용](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-206">If you are using a Windows client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="b5eaf-207">Linux 클라이언트를 사용하여 클러스터로 SSH하는 경우 [Linux에서 HDInsight의 Linux 기반 Hadoop과 SSH 사용](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-207">If you are using a Linux client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

<span data-ttu-id="b5eaf-208">연결되면 다음 HDFS 파일 시스템 명령을 사용하여 데이터 레이크 저장소에 파일을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-208">Once connected, use the following HDFS filesystem command to list the files in the Data Lake Store.</span></span>

    hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/

<span data-ttu-id="b5eaf-209">데이터 레이크 저장소에 이전에 업로드한 파일이 나열되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-209">This should list the file that you uploaded earlier to the Data Lake Store.</span></span>

    15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
    Found 1 items
    -rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder

<span data-ttu-id="b5eaf-210">`hdfs dfs -put` 명령을 사용하여 일부 파일을 데이터 레이크 저장소에 업로드한 다음 `hdfs dfs -ls`을(를) 사용하여 파일이 성공적으로 업로드되었는지 여부를 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5eaf-210">You can also use the `hdfs dfs -put` command to upload some files to the Data Lake Store, and then use `hdfs dfs -ls` to verify whether the files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="b5eaf-211">참고 항목</span><span class="sxs-lookup"><span data-stu-id="b5eaf-211">See Also</span></span>
* [<span data-ttu-id="b5eaf-212">포털: HDInsight 클러스터를 만들어 데이터 레이크 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="b5eaf-212">Portal: Create an HDInsight cluster to use Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
