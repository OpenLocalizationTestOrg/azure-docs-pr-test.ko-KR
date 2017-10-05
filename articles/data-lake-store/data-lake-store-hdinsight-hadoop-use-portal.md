---
title: "Azure Portal을 사용하여 Data Lake Store로 Azure HDInsight 클러스터 만들기 | Microsoft Docs"
description: "Azure Portal을 사용하여 Azure Data Lake Store로 HDInsight Hadoop 클러스터 만들기 및 사용"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: a8c45a83-a8e3-4227-8b02-1bc1e1de6767
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: nitinme
ms.openlocfilehash: 9dd56efb89e07ea61ae431d1ea2accd721cd6502
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-by-using-the-azure-portal"></a><span data-ttu-id="af69d-103">Azure Portal을 사용하여 Data Lake Store로 HDInsight 클러스터 만들기 | Azure</span><span class="sxs-lookup"><span data-stu-id="af69d-103">Create HDInsight clusters with Data Lake Store by using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="af69d-104">Azure Portal 사용</span><span class="sxs-lookup"><span data-stu-id="af69d-104">Use the Azure portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="af69d-105">PowerShell 사용(기본 저장소의 경우)</span><span class="sxs-lookup"><span data-stu-id="af69d-105">Use PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="af69d-106">PowerShell 사용(추가 저장소의 경우)</span><span class="sxs-lookup"><span data-stu-id="af69d-106">Use PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="af69d-107">Resource Manager 사용</span><span class="sxs-lookup"><span data-stu-id="af69d-107">Use Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="af69d-108">Azure Portal을 사용하여 기본 저장소 또는 추가 저장소로 Azure Data Lake Store 계정을 사용하여 HDInsight 클러스터를 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-108">Learn how to use the Azure portal to create a HDInsight cluster with an Azure Data Lake Store account as the default storage or an additional storage.</span></span> <span data-ttu-id="af69d-109">추가 저장소는 HDInsight 클러스터에 대해 선택적 사항이지만 추가 저장소 계정에 비즈니스 데이터를 저장하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-109">Even though additional storage is optional for a HDInsight cluster, it is recommended to store your business data in the additional storage accounts.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af69d-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="af69d-110">Prerequisites</span></span>
<span data-ttu-id="af69d-111">이 자습서를 시작하기 전에 다음 요구 사항을 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-111">Before you begin this tutorial, ensure that you've met the following requirements:</span></span>

* <span data-ttu-id="af69d-112">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="af69d-112">**An Azure subscription**.</span></span> <span data-ttu-id="af69d-113">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-113">Go to [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="af69d-114">**Azure 데이터 레이크 저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="af69d-114">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="af69d-115">[Azure Portal을 사용하여 Azure Data Lake Store 시작](data-lake-store-get-started-portal.md)의 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-115">Follow the instructions from [Get started with Azure Data Lake Store by using the Azure portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="af69d-116">또한 계정에서 루트 폴더를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-116">You must also create a root folder on the account.</span></span>  <span data-ttu-id="af69d-117">이 자습서에서는 __/clusters__라는 루트 폴더가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-117">In this tutorial, a root folder called __/clusters__ is used.</span></span>
* <span data-ttu-id="af69d-118">**Azure Active Directory 서비스 주체**</span><span class="sxs-lookup"><span data-stu-id="af69d-118">**An Azure Active Directory service principal**.</span></span> <span data-ttu-id="af69d-119">이 자습서에서는 Azure AD(Azure Active Directory)에서 서비스 주체를 만드는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-119">This tutorial provides instructions on how to create a service principal in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="af69d-120">그러나 서비스 주체를 만들려면 Azure AD 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-120">However, to create a service principal, you must be an Azure AD administrator.</span></span> <span data-ttu-id="af69d-121">관리자인 경우 이 필수 요소를 건너뛰고 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-121">If you are an administrator, you can skip this prerequisite and proceed with the tutorial.</span></span>

    >[!NOTE]
    ><span data-ttu-id="af69d-122">Azure AD 관리자인 경우에만 서비스 주체를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-122">You can create a service principal only if you are an Azure AD administrator.</span></span> <span data-ttu-id="af69d-123">Azure AD 관리자가 서비스 주체를 만들어야 Data Lake Store와 HDInsight 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-123">Your Azure AD administrator must create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="af69d-124">또한 [인증서를 사용하여 서비스 주체 만들기](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate)에 설명된 대로 인증서를 사용하여 서비스 주체를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-124">Also, the service principal must be created with a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span></span>
    >

## <a name="create-an-hdinsight-cluster"></a><span data-ttu-id="af69d-125">HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="af69d-125">Create an HDInsight cluster</span></span>

<span data-ttu-id="af69d-126">이 섹션에서는 기본 또는 추가 저장소로 Data Lake Store 계정을 사용하여 HDInsight 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-126">In this section, you create a HDInsight cluster with Data Lake Store accounts as the default or the additional storage.</span></span> <span data-ttu-id="af69d-127">이 문서는 Data Lake Store 계정을 구성하는 과정만 주로 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-127">This article only focuses the part of configuring Data Lake Store accounts.</span></span>  <span data-ttu-id="af69d-128">클러스터 만들기에 대한 일반적인 정보 및 절차는 [HDInsight에서 Hadoop 클러스터 만들기](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af69d-128">For the general cluster creation information and procedures, see [Create Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span></span>

### <a name="create-a-cluster-with-data-lake-store-as-default-storage"></a><span data-ttu-id="af69d-129">Data Lake Store를 기본 저장소로 사용하여 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="af69d-129">Create a cluster with Data Lake Store as default storage</span></span>

<span data-ttu-id="af69d-130">**Data Lake Store를 기본 저장소 계정으로 사용하여 HDInsight 클러스터를 만들려면**</span><span class="sxs-lookup"><span data-stu-id="af69d-130">**To create a HDInsight cluster with a Data Lake Store as the default storage account**</span></span>

1. <span data-ttu-id="af69d-131">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-131">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="af69d-132">HDInsight 클러스터를 만드는 방법에 대한 일반 정보는 [클러스터 만들기](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters)를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-132">Follow [Create clusters](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters) for the general information on creating HDInsight clusters.</span></span>
3. <span data-ttu-id="af69d-133">**저장소** 블레이드의 **기본 저장소 형식** 아래에서 **Data Lake Store**를 선택한 후 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-133">On the **Storage** blade, under **Primary storage type**, select **Data Lake Store**, and then enter the following information:</span></span>

    <span data-ttu-id="af69d-134">![HDInsight 클러스터에 서비스 주체 추가](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.adls.storage.png "HDInsight 클러스터에 서비스 주체 추가")</span><span class="sxs-lookup"><span data-stu-id="af69d-134">![Add service principal to HDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.adls.storage.png "Add service principal to HDInsight cluster")</span></span>

    - <span data-ttu-id="af69d-135">**Data Lake Store 계정 선택**: 기존 Data Lake Store 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-135">**Select Data Lake Store account**: Select an existing Data Lake Store account.</span></span> <span data-ttu-id="af69d-136">기존 Data Lake Store 계정은 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-136">An existing Data Lake Store account is required.</span></span>  <span data-ttu-id="af69d-137">[필수 조건](#prereuisites)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af69d-137">See [Prerequisites](#prereuisites).</span></span>
    - <span data-ttu-id="af69d-138">**루트 경로**: 클러스터 관련 파일이 저장되는 경로를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-138">**Root path**: Enter a path where the cluster-specific files are to be stored.</span></span> <span data-ttu-id="af69d-139">스크린샷에서 __/clusters__ 폴더가 존재해야 하는 __/clusters/myhdiadlcluster/__이며 포털은 *myhdicluster* 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-139">On the screenshot, it is __/clusters/myhdiadlcluster/__, in which the __/clusters__ folder must exist, and the Portal creates *myhdicluster* folder.</span></span>  <span data-ttu-id="af69d-140">*myhdicluster*는 클러스터 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-140">The *myhdicluster* is the cluster name.</span></span>
    - <span data-ttu-id="af69d-141">**Data Lake Store 액세스**: Data Lake Store 계정과 HDInsight 클러스터 간의 액세스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-141">**Data Lake Store access**: Configure access between the Data Lake Store account and HDInsight cluster.</span></span> <span data-ttu-id="af69d-142">지침은 [Data Lake Store 액세스 구성](#configure-data-lake-store-access)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af69d-142">For instructions, see [Configure Data Lake Store access](#configure-data-lake-store-access).</span></span>
    - <span data-ttu-id="af69d-143">**추가 저장소 계정**: 클러스터에 대한 추가 저장소 계정으로 Azure Storage 계정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-143">**Additional storage accounts**: Add Azure Storage Accounts as additional storage accounts for the cluster.</span></span> <span data-ttu-id="af69d-144">추가 Data Lake Store 추가는 Data Lake Store 계정을 기본 저장소 형식으로 구성하는 동안 Data Lake Store 계정에 더 많은 데이터의 클러스터 권한을 제공하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-144">To add additional Data Lake Stores is done by giving the cluster permissions on data in more Data Lake Store accounts while configuring a Data Lake Store account as the primary storage type.</span></span> <span data-ttu-id="af69d-145">[Data Lake Store 액세스 구성](#configure-data-lake-store-access)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af69d-145">See [Configure Data Lake Store access](#configure-data-lake-store-access).</span></span>

4. <span data-ttu-id="af69d-146">**Data Lake Store 액세스**에서 **선택**을 클릭한 다음 [HDInsight에서 Hadoop 클러스터 만들기](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md)에서 설명한 대로 클러스터 만들기를 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-146">On the **Data Lake Store access**, click **Select**, and then continue with cluster creation as described in [Create Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>


### <a name="create-a-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="af69d-147">Data Lake Store를 추가 저장소로 사용하여 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="af69d-147">Create a cluster with Data Lake Store as additional storage</span></span>

<span data-ttu-id="af69d-148">다음 지침은 기본 저장소로 Azure Storage 계정을 사용하고 추가 저장소로 Data Lake Store 계정을 사용하여 HDInsight 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-148">The following instructions create a HDInsight cluster with an Azure Storage account as the default storage, and a Data Lake Store account as an additional storage.</span></span>
<span data-ttu-id="af69d-149">**Data Lake Store를 기본 저장소 계정으로 사용하여 HDInsight 클러스터를 만들려면**</span><span class="sxs-lookup"><span data-stu-id="af69d-149">**To create a HDInsight cluster with a Data Lake Store as the default storage account**</span></span>

1. <span data-ttu-id="af69d-150">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-150">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="af69d-151">HDInsight 클러스터를 만드는 방법에 대한 일반 정보는 [클러스터 만들기](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters)를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-151">Follow [Create clusters](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters) for the general information on creating HDInsight clusters.</span></span>
3. <span data-ttu-id="af69d-152">**저장소** 블레이드의 **기본 저장소 형식** 아래에서 **Azure Storage**를 선택한 후 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-152">On the **Storage** blade, under **Primary storage type**, select **Azure Storage**, and then enter the following information:</span></span>

    <span data-ttu-id="af69d-153">![HDInsight 클러스터에 서비스 주체 추가](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.png "HDInsight 클러스터에 서비스 주체 추가")</span><span class="sxs-lookup"><span data-stu-id="af69d-153">![Add service principal to HDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.png "Add service principal to HDInsight cluster")</span></span>

    - <span data-ttu-id="af69d-154">**선택 메서드**: 다음 옵션 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-154">**Selection method**: use one of the following options:</span></span>

        * <span data-ttu-id="af69d-155">Azure 구독의 일부인 저장소 계정을 지정하려면 **내 구독**을 선택한 다음 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-155">To specify a storage account that is part of your Azure subscription, select **My subscriptions**, and then select the storage account.</span></span>
        * <span data-ttu-id="af69d-156">Azure 구독 외부에 있는 저장소 계정을 지정하려면 **선택키**를 선택한 다음 외부 저장소 계정에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-156">To specify a storage account that is outside your Azure subscription, select **Access key**, and then provide the information for the outside storage account.</span></span>

    - <span data-ttu-id="af69d-157">**기본 컨테이너**: 기본값을 사용하거나 고유한 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-157">**Default container**: use either the default value or specify your own name.</span></span>

    - <span data-ttu-id="af69d-158">추가 저장소 계정: 추가 저장소로 Azure Storage 계정을 더 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-158">Additional Storage accounts: add more Azure Storage accounts as the additional storage.</span></span>
    - <span data-ttu-id="af69d-159">Data Lake Store 액세스: Data Lake Store 계정과 HDInsight 클러스터 간의 액세스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-159">Data Lake Store access: configure access between the Data Lake Store account and HDInsight cluster.</span></span> <span data-ttu-id="af69d-160">지침은 [Data Lake Store 액세스 구성](#configure-data-lake-store-access)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af69d-160">For instructions see [Configure Data Lake Store access](#configure-data-lake-store-access).</span></span>

## <a name="configure-data-lake-store-access"></a><span data-ttu-id="af69d-161">Data Lake Store 액세스 구성</span><span class="sxs-lookup"><span data-stu-id="af69d-161">Configure Data Lake Store access</span></span> 

<span data-ttu-id="af69d-162">이 섹션에서는 Azure Active Directory 서비스 주체를 사용하여 HDInsight 클러스터에서 Data Lake Store 액세스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-162">In this section, you configure Data Lake Store access from HDInsight clusters using an Azure Active Directory service principal.</span></span> 

### <a name="specify-a-service-principal"></a><span data-ttu-id="af69d-163">서비스 주체 지정</span><span class="sxs-lookup"><span data-stu-id="af69d-163">Specify a service principal</span></span>

<span data-ttu-id="af69d-164">Azure Portal에서 기존 서비스 주체를 사용하거나 새로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-164">From the Azure portal, you can either use an existing service principal or create a new one.</span></span>

<span data-ttu-id="af69d-165">**Azure Portal에서 서비스 주체를 만들려면**</span><span class="sxs-lookup"><span data-stu-id="af69d-165">**To create a service principal from the Azure portal**</span></span>

1. <span data-ttu-id="af69d-166">저장소 블레이드에서 **Data Lake Store 액세스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-166">Click **Data Lake Store access** from the Store blade.</span></span>
2. <span data-ttu-id="af69d-167">**Data Lake Store 액세스** 블레이드에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-167">On the **Data Lake Store access** blade, click **Create new**.</span></span>
3. <span data-ttu-id="af69d-168">**서비스 주체**를 클릭한 다음 지침을 따라 서비스 주체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-168">Click **Service Principal**, and then follow the instructions to create a service principal.</span></span>
4. <span data-ttu-id="af69d-169">나중에 다시 사용하려는 경우 인증서를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-169">Download the certificate if you decide to use it again in the future.</span></span> <span data-ttu-id="af69d-170">추가 HDInsight 클러스터를 만들 때 동일한 서비스 주체를 사용하려면 인증서를 다운로드하는 것이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-170">Downloading the certificate is useful if you want to use the same service principal when you create additional HDInsight clusters.</span></span>

    <span data-ttu-id="af69d-171">![HDInsight 클러스터에 서비스 주체 추가](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.2.png "HDInsight 클러스터에 서비스 주체 추가")</span><span class="sxs-lookup"><span data-stu-id="af69d-171">![Add service principal to HDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.2.png "Add service principal to HDInsight cluster")</span></span>

4. <span data-ttu-id="af69d-172">**액세스**를 클릭하여 폴더 액세스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-172">Click **Access** to configure the folder access.</span></span>  <span data-ttu-id="af69d-173">[파일 권한 구성](#configure-file-permissions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af69d-173">See [Configure file permissions](#configure-file-permissions).</span></span>


<span data-ttu-id="af69d-174">**Azure Portal에서 기존 서비스 주체를 사용하려면**</span><span class="sxs-lookup"><span data-stu-id="af69d-174">**To use an existing service principal from the Azure portal**</span></span>

1. <span data-ttu-id="af69d-175">**Data Lake Store 액세스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-175">Click **Data Lake Store access**.</span></span>
1. <span data-ttu-id="af69d-176">**Data Lake Store 액세스** 블레이드에서 **기존 항목 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-176">On the **Data Lake Store access** blade, click **Use existing**.</span></span>
2. <span data-ttu-id="af69d-177">**서비스 주체**를 클릭한 다음 서비스 주체를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-177">Click **Service Principal**, and then select a service principal.</span></span> 
3. <span data-ttu-id="af69d-178">선택한 서비스 주체와 연결된 인증서(.pfx 파일)를 업로드한 다음 인증서 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-178">Upload the certificate (.pfx file) that's associated with your selected service principal, and then enter the certificate password.</span></span>

    <span data-ttu-id="af69d-179">![HDInsight 클러스터에 서비스 주체 추가](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.5.png "HDInsight 클러스터에 서비스 주체 추가")</span><span class="sxs-lookup"><span data-stu-id="af69d-179">![Add service principal to HDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.5.png "Add service principal to HDInsight cluster")</span></span>

4. <span data-ttu-id="af69d-180">**액세스**를 클릭하여 폴더 액세스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-180">Click **Access** to configure the folder access.</span></span>  <span data-ttu-id="af69d-181">[파일 권한 구성](#configure-file-permissions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af69d-181">See [Configure file permissions](#configure-file-permissions).</span></span>


### <span data-ttu-id="af69d-182"><a name="configure-file-permissions"></a>파일 권한 구성</span><span class="sxs-lookup"><span data-stu-id="af69d-182"><a name="configure-file-permissions"></a>Configure file permissions</span></span>

<span data-ttu-id="af69d-183">구성은 계정이 기본 저장소 또는 추가 저장소 계정으로 사용되는지 여부에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-183">The configures are different depending on whether the account is used as the default storage or an additional storage account:</span></span>

- <span data-ttu-id="af69d-184">기본 저장소로 사용됨</span><span class="sxs-lookup"><span data-stu-id="af69d-184">Used as default storage</span></span>

    - <span data-ttu-id="af69d-185">Data Lake Store 계정의 루트 수준에서 권한</span><span class="sxs-lookup"><span data-stu-id="af69d-185">permission at the root level of the Data Lake Store account</span></span>
    - <span data-ttu-id="af69d-186">HDInsight 클러스터 저장소의 루트 수준에서 권한</span><span class="sxs-lookup"><span data-stu-id="af69d-186">permission at the root level of the HDInsight cluster storage.</span></span> <span data-ttu-id="af69d-187">예를 들어 자습서의 앞부분에서 사용된 __/clusters__ 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-187">For example, the __/clusters__ folder used earlier in the tutorial.</span></span>
- <span data-ttu-id="af69d-188">추가 저장소로 사용</span><span class="sxs-lookup"><span data-stu-id="af69d-188">Use as an additional storage</span></span>

    - <span data-ttu-id="af69d-189">파일 액세스가 필요한 폴더에서 권한</span><span class="sxs-lookup"><span data-stu-id="af69d-189">Permission at the folders where you need file access.</span></span>

<span data-ttu-id="af69d-190">**Data Lake Store 계정 루트 수준에서 권한을 할당하려면**</span><span class="sxs-lookup"><span data-stu-id="af69d-190">**To assign permission at the Data Lake Store account root level**</span></span>

1. <span data-ttu-id="af69d-191">**Data Lake Store 액세스** 블레이드에서 **액세스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-191">On the **Data Lake Store access** blade, click **Access**.</span></span> <span data-ttu-id="af69d-192">**파일 권한 선택** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-192">The **Select file permissions** blade is opened.</span></span> <span data-ttu-id="af69d-193">구독에서 모든 Data Lake Store 계정을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-193">It lists all the Data Lake Store accounts in your subscription.</span></span>
2. <span data-ttu-id="af69d-194">확인란이 표시되도록 Data Lake Store 계정의 이름 위로 마우스를 가리킨 다음(클릭하지 마십시오) 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-194">Hover (do not click) the mouse over the name of the Data Lake Store account to make the check box visible, then select the check box.</span></span>

    <span data-ttu-id="af69d-195">![HDInsight 클러스터에 서비스 주체 추가](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3.png "HDInsight 클러스터에 서비스 주체 추가")</span><span class="sxs-lookup"><span data-stu-id="af69d-195">![Add service principal to HDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3.png "Add service principal to HDInsight cluster")</span></span>

  <span data-ttu-id="af69d-196">기본적으로 __읽기__, __쓰기__ 및 __실행__이 모두 선택되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-196">By default, __READ__, __WRITE__, AND __EXECUTE__ are all selected.</span></span>

3. <span data-ttu-id="af69d-197">페이지 아래쪽에서 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-197">Click **Select** on the bottom of the page.</span></span>
4. <span data-ttu-id="af69d-198">**실행**을 클릭하여 권한을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-198">Click **Run** to assign permission.</span></span>
5. <span data-ttu-id="af69d-199">**Done**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-199">Click **Done**.</span></span>

<span data-ttu-id="af69d-200">**HDInsight 클러스터 루트 수준에서 권한을 할당하려면**</span><span class="sxs-lookup"><span data-stu-id="af69d-200">**To assign permission at the HDInsight cluster root level**</span></span>

1. <span data-ttu-id="af69d-201">**Data Lake Store 액세스** 블레이드에서 **액세스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-201">On the **Data Lake Store access** blade, click **Access**.</span></span> <span data-ttu-id="af69d-202">**파일 권한 선택** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-202">The **Select file permissions** blade is opened.</span></span> <span data-ttu-id="af69d-203">구독에서 모든 Data Lake Store 계정을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-203">It lists all the Data Lake Store accounts in your subscription.</span></span>
1. <span data-ttu-id="af69d-204">**파일 권한 선택** 블레이드에서 해당 콘텐츠를 표시할 Data Lake Store 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-204">From the **Select file permissions** blade, click the Data Lake Store name to show its content.</span></span>
2. <span data-ttu-id="af69d-205">폴더 왼쪽의 확인란을 선택하여 HDInsight 클러스터 저장소 루트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-205">Select the HDInsight cluster storage root by selecting the checkbox on the left of the folder.</span></span> <span data-ttu-id="af69d-206">앞쪽의 스크린샷에 따르면 클러스터 저장소 루트는 Data Lake Store를 기본 저장소로 선택하는 동안 지정한 __/clusters__ 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-206">According to the screenshot earlier, the cluster storage root is __/clusters__ folder that you specified while selecting the Data Lake Store as default storage.</span></span>
3. <span data-ttu-id="af69d-207">폴더에 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-207">Set the permissions on the folder.</span></span>  <span data-ttu-id="af69d-208">기본적으로 읽기, 쓰기 및 실행이 모두 선택되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-208">By default, read, write, and execute are all selected.</span></span>
4. <span data-ttu-id="af69d-209">페이지 아래쪽에서 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-209">Click **Select** on the bottom of the page.</span></span>
5. <span data-ttu-id="af69d-210">**실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-210">Click **Run**.</span></span>
6. <span data-ttu-id="af69d-211">**Done**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-211">Click **Done**.</span></span>

<span data-ttu-id="af69d-212">Data Lake Store를 추가 저장소로 사용하는 경우 HDInsight 클러스터에서 액세스하려는 폴더에만 권한을 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-212">If you are using Data Lake Store as additional storage, you must assign permission only for the folders that you want to access from the HDInsight cluster.</span></span> <span data-ttu-id="af69d-213">예를 들어 아래 스크린샷에서 Data Lake Store 계정의 **hdiaddonstorage** 폴더에만 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-213">For example, in the screenshot below, you provide access only to **hdiaddonstorage** folder in a Data Lake Store account.</span></span>

<span data-ttu-id="af69d-214">![HDInsight 클러스터에 서비스 주체 사용 권한 할당](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3-1.png "HDInsight 클러스터에 서비스 주체 사용 권한 할당")</span><span class="sxs-lookup"><span data-stu-id="af69d-214">![Assign service principal permissions to the HDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3-1.png "Assign service principal permissions to the HDInsight cluster")</span></span>


## <a name="verify-cluster-set-up"></a><span data-ttu-id="af69d-215">클러스터 설정 확인</span><span class="sxs-lookup"><span data-stu-id="af69d-215">Verify cluster set up</span></span>

<span data-ttu-id="af69d-216">클러스터 설정을 완료한 후에 클러스터 블레이드에서 다음 단계 중 하나 또는 모두를 수행하여 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-216">After the cluster setup is complete, on the cluster blade, verify your results by doing either or both of the following steps:</span></span>

* <span data-ttu-id="af69d-217">클러스터에 대한 연결된 저장소가 지정한 Data Lake Store 계정인지 확인하려면 왼쪽 창에서 **저장소 계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-217">To verify that the associated storage for the cluster is the Data Lake Store account that you specified, click **Storage accounts** in the left pane.</span></span>

    <span data-ttu-id="af69d-218">![HDInsight 클러스터에 서비스 주체 추가](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6-1.png "HDInsight 클러스터에 서비스 주체 추가")</span><span class="sxs-lookup"><span data-stu-id="af69d-218">![Add service principal to HDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6-1.png "Add service principal to HDInsight cluster")</span></span>

* <span data-ttu-id="af69d-219">서비스 주체가 HDInsight 클러스터와 올바르게 연결되었는지 확인하려면 왼쪽 창에서 **Data Lake Store 액세스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-219">To verify that the service principal is correctly associated with the HDInsight cluster, click **Data Lake Store access** in the left pane.</span></span>

    <span data-ttu-id="af69d-220">![HDInsight 클러스터에 서비스 주체 추가](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6.png "HDInsight 클러스터에 서비스 주체 추가")</span><span class="sxs-lookup"><span data-stu-id="af69d-220">![Add service principal to HDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6.png "Add service principal to HDInsight cluster")</span></span>


## <a name="examples"></a><span data-ttu-id="af69d-221">예</span><span class="sxs-lookup"><span data-stu-id="af69d-221">Examples</span></span>

<span data-ttu-id="af69d-222">Data Lake Store를 저장소로 사용하여 클러스터를 설정한 후에 HDInsight 클러스터를 사용하여 Data Lake Store에 저장된 데이터를 분석하는 방법에 대한 다음과 같은 예제를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-222">After you have set up the cluster with Data Lake Store as your storage, refer to these examples of how to use HDInsight cluster to analyze the data that's stored in Data Lake Store.</span></span>

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-primary-storage"></a><span data-ttu-id="af69d-223">기본 저장소인 Data Lake Store에서 데이터에 대한 Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="af69d-223">Run a Hive query against data in a Data Lake Store (as primary storage)</span></span>

<span data-ttu-id="af69d-224">Hive 쿼리를 실행하려면 Ambari 포털에서 [Hive 보기] 인터페이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-224">To run a Hive query, use the Hive views interface in the Ambari portal.</span></span> <span data-ttu-id="af69d-225">[Ambari Hive 보기]를 사용하는 방법에 대한 지침은 [ HDInsight에서 Hadoop을 사용하여 Hive 보기 사용](../hdinsight/hdinsight-hadoop-use-hive-ambari-view.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af69d-225">For instructions on how to use Ambari Hive views, see [Use the Hive View with Hadoop in HDInsight](../hdinsight/hdinsight-hadoop-use-hive-ambari-view.md).</span></span>

<span data-ttu-id="af69d-226">Data Lake Store에서 데이터를 사용하는 경우 다음과 같은 몇 가지 문자열을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-226">When you work with data in a Data Lake Store, there are a few strings to change.</span></span>

<span data-ttu-id="af69d-227">예를 들어, Data Lake Store를 주 저장소로 사용하여 만든 클러스터를 사용하는 경우 데이터의 경로는 *adl://<data_lake_store_account_name>/azuredatalakestore.net/path/to/file*입니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-227">If you use, for example, the cluster that you created with Data Lake Store as primary storage, the path to the data is: *adl://<data_lake_store_account_name>/azuredatalakestore.net/path/to/file*.</span></span> <span data-ttu-id="af69d-228">Data Lake Store 계정에 저장된 샘플 데이터에서 테이블을 만드는 Hive 쿼리는 다음 문과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-228">A Hive query to create a table from sample data that's stored in the Data Lake Store account looks like the following statement:</span></span>

    CREATE EXTERNAL TABLE websitelog (str string) LOCATION 'adl://hdiadlsstorage.azuredatalakestore.net/clusters/myhdiadlcluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/'

<span data-ttu-id="af69d-229">설명:</span><span class="sxs-lookup"><span data-stu-id="af69d-229">Descriptions:</span></span>
* <span data-ttu-id="af69d-230">`adl://hdiadlstorage.azuredatalakestore.net/`은 Data Lake Store 계정의 루트입니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-230">`adl://hdiadlstorage.azuredatalakestore.net/` is the root of the Data Lake Store account.</span></span>
* <span data-ttu-id="af69d-231">`/clusters/myhdiadlcluster`는 클러스터를 만드는 동안에 지정한 클러스터 데이터의 루트입니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-231">`/clusters/myhdiadlcluster` is the root of the cluster data that you specified while creating the cluster.</span></span>
* <span data-ttu-id="af69d-232">`/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/`는 쿼리에서 사용하는 샘플 파일의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-232">`/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/` is the location of the sample file that you used in the query.</span></span>

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-additional-storage"></a><span data-ttu-id="af69d-233">추가 저장소인 Data Lake Store에 저장된 데이터에 대한 Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="af69d-233">Run a Hive query against data in a Data Lake Store (as additional storage)</span></span>

<span data-ttu-id="af69d-234">사용자가 만든 클러스터에서 Blob Storage를 기본 저장소로 사용하는 경우 샘플 데이터는 추가 저장소로 사용된 Azure Data Lake Store 계정에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-234">If the cluster that you created uses Blob storage as default storage, the sample data is not contained in the Azure Data Lake Store account that's used as additional storage.</span></span> <span data-ttu-id="af69d-235">이와 같은 경우에는 먼저 Blob Storage에서 Data Lake Store로 데이터를 전송하고 앞의 예제와 같이 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-235">In such a case, first transfer the data from Blob storage to the Data Lake Store, and then run the queries as shown in the preceding example.</span></span>

<span data-ttu-id="af69d-236">Blob Storage에서 Azure Data Lake Store로 데이터를 복사하는 방법에 대한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af69d-236">For information on how to copy data from Blob storage to a Data Lake Store, see the following articles:</span></span>

* [<span data-ttu-id="af69d-237">Distcp를 사용하여 Azure Storage Blob과 Data Lake Store 간에 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="af69d-237">Use Distcp to copy data between Azure Storage blobs and Data Lake Store</span></span>](data-lake-store-copy-data-wasb-distcp.md)
* [<span data-ttu-id="af69d-238">AdlCopy를 사용하여 Azure Storage Blob에서 Data Lake Store로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="af69d-238">Use AdlCopy to copy data from Azure Storage blobs to Data Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)

### <a name="use-data-lake-store-with-a-spark-cluster"></a><span data-ttu-id="af69d-239">Spark 클러스터에서 Data Lake Store 사용</span><span class="sxs-lookup"><span data-stu-id="af69d-239">Use Data Lake Store with a Spark cluster</span></span>
<span data-ttu-id="af69d-240">Spark 클러스터를 사용하여 Data Lake Store에 저장된 데이터에서 Spark 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-240">You can use a Spark cluster to run Spark jobs on data that is stored in a Data Lake Store.</span></span> <span data-ttu-id="af69d-241">자세한 내용은 [HDInsight Spark 클러스터를 사용하여 Data Lake Store의 데이터 분석](../hdinsight/hdinsight-apache-spark-use-with-data-lake-store.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af69d-241">For more information, see [Use HDInsight Spark cluster to analyze data in Data Lake Store](../hdinsight/hdinsight-apache-spark-use-with-data-lake-store.md).</span></span>


### <a name="use-data-lake-store-in-a-storm-topology"></a><span data-ttu-id="af69d-242">Storm 토폴로지에서 Data Lake 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="af69d-242">Use Data Lake Store in a Storm topology</span></span>
<span data-ttu-id="af69d-243">데이터 레이크 저장소를 사용하여 Storm 토폴로지에서 데이터를 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af69d-243">You can use the Data Lake Store to write data from a Storm topology.</span></span> <span data-ttu-id="af69d-244">이 시나리오를 수행하는 방법에 대한 자세한 내용은 [HDInsight에서 Apache Storm에 Azure Data Lake Store 사용](../hdinsight/hdinsight-storm-write-data-lake-store.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af69d-244">For instructions on how to achieve this scenario, see [Use Azure Data Lake Store with Apache Storm with HDInsight](../hdinsight/hdinsight-storm-write-data-lake-store.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="af69d-245">참고 항목</span><span class="sxs-lookup"><span data-stu-id="af69d-245">See also</span></span>
* [<span data-ttu-id="af69d-246">PowerShell: HDInsight 클러스터를 만들어 데이터 레이크 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="af69d-246">PowerShell: Create an HDInsight cluster to use Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
