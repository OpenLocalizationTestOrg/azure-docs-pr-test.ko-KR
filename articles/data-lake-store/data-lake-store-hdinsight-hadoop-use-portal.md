---
title: "데이터 레이크 저장소와 aaaUse hello Azure 포털 toocreate Azure HDInsight 클러스터 | Microsoft Docs"
description: "Azure 포털 toocreate hello를 사용 하 고 HDInsight 클러스터를 사용 하 여 Azure 데이터 레이크 저장소"
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
ms.openlocfilehash: f23113d444a3c5a01894dba29f75f3621b2d16bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-by-using-hello-azure-portal"></a><span data-ttu-id="fda7d-103">데이터 레이크 저장소와 hello Azure 포털을 사용 하 여 HDInsight 클러스터를 만들려면</span><span class="sxs-lookup"><span data-stu-id="fda7d-103">Create HDInsight clusters with Data Lake Store by using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fda7d-104">Hello Azure 포털을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="fda7d-104">Use hello Azure portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="fda7d-105">PowerShell 사용(기본 저장소의 경우)</span><span class="sxs-lookup"><span data-stu-id="fda7d-105">Use PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="fda7d-106">PowerShell 사용(추가 저장소의 경우)</span><span class="sxs-lookup"><span data-stu-id="fda7d-106">Use PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="fda7d-107">Resource Manager 사용</span><span class="sxs-lookup"><span data-stu-id="fda7d-107">Use Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="fda7d-108">어떻게 toouse hello Azure 포털 toocreate Azure 데이터 레이크 저장소 계정 사용 하 여 HDInsight 클러스터로 추가 저장소 또는 hello 기본 저장소에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-108">Learn how toouse hello Azure portal toocreate a HDInsight cluster with an Azure Data Lake Store account as hello default storage or an additional storage.</span></span> <span data-ttu-id="fda7d-109">추가 저장소는 HDInsight 클러스터에 대 한 선택적으로 있지만 toostore hello 추가 저장소 계정에서 비즈니스 데이터를 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-109">Even though additional storage is optional for a HDInsight cluster, it is recommended toostore your business data in hello additional storage accounts.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fda7d-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fda7d-110">Prerequisites</span></span>
<span data-ttu-id="fda7d-111">이 자습서를 시작 하기 전에 hello 요구 사항을 준수를 충족 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-111">Before you begin this tutorial, ensure that you've met hello following requirements:</span></span>

* <span data-ttu-id="fda7d-112">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="fda7d-112">**An Azure subscription**.</span></span> <span data-ttu-id="fda7d-113">너무 이동[가져오기 Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-113">Go too[Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="fda7d-114">**Azure 데이터 레이크 저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="fda7d-114">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="fda7d-115">Hello 지침을 따릅니다 [hello Azure 포털을 사용 하 여 Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-115">Follow hello instructions from [Get started with Azure Data Lake Store by using hello Azure portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="fda7d-116">Hello 계정에도 루트 폴더를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-116">You must also create a root folder on hello account.</span></span>  <span data-ttu-id="fda7d-117">이 자습서에서는 __/clusters__라는 루트 폴더가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-117">In this tutorial, a root folder called __/clusters__ is used.</span></span>
* <span data-ttu-id="fda7d-118">**Azure Active Directory 서비스 주체**</span><span class="sxs-lookup"><span data-stu-id="fda7d-118">**An Azure Active Directory service principal**.</span></span> <span data-ttu-id="fda7d-119">이 자습서는 방법에 대해 설명 toocreate Azure Active Directory (Azure AD)에 서비스 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-119">This tutorial provides instructions on how toocreate a service principal in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="fda7d-120">그러나 toocreate 서비스 사용자 여야 Azure AD 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-120">However, toocreate a service principal, you must be an Azure AD administrator.</span></span> <span data-ttu-id="fda7d-121">관리자 인 경우이 필수 구성이 요소를 건너뛰고 hello 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-121">If you are an administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    >[!NOTE]
    ><span data-ttu-id="fda7d-122">Azure AD 관리자인 경우에만 서비스 주체를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-122">You can create a service principal only if you are an Azure AD administrator.</span></span> <span data-ttu-id="fda7d-123">Azure AD 관리자가 서비스 주체를 만들어야 Data Lake Store와 HDInsight 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-123">Your Azure AD administrator must create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="fda7d-124">또한 hello 서비스 사용자에서 만들어야 합니다는 인증서에 설명 된 대로 [인증서로 서비스 사용자를 만들](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate)합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-124">Also, hello service principal must be created with a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span></span>
    >

## <a name="create-an-hdinsight-cluster"></a><span data-ttu-id="fda7d-125">HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="fda7d-125">Create an HDInsight cluster</span></span>

<span data-ttu-id="fda7d-126">이 섹션에서는 hello 기본 문화권 이나 hello 추가 저장으로 데이터 레이크 저장소 계정에 HDInsight 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-126">In this section, you create a HDInsight cluster with Data Lake Store accounts as hello default or hello additional storage.</span></span> <span data-ttu-id="fda7d-127">이 문서는 데이터 레이크 저장소 계정을 구성 하는 hello 과정만 집중 합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-127">This article only focuses hello part of configuring Data Lake Store accounts.</span></span>  <span data-ttu-id="fda7d-128">Hello 일반 클러스터 생성 정보 및 절차에 대 한 참조 [HDInsight 클러스터를 만드는 Hadoop](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-128">For hello general cluster creation information and procedures, see [Create Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span></span>

### <a name="create-a-cluster-with-data-lake-store-as-default-storage"></a><span data-ttu-id="fda7d-129">Data Lake Store를 기본 저장소로 사용하여 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="fda7d-129">Create a cluster with Data Lake Store as default storage</span></span>

<span data-ttu-id="fda7d-130">**hello 기본 저장소 계정으로 데이터 레이크 저장소와 toocreate는 HDInsight 클러스터**</span><span class="sxs-lookup"><span data-stu-id="fda7d-130">**toocreate a HDInsight cluster with a Data Lake Store as hello default storage account**</span></span>

1. <span data-ttu-id="fda7d-131">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-131">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="fda7d-132">에 따라 [클러스터를 만들어](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters) hello 일반 정보는 HDInsight 클러스터를 만드는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-132">Follow [Create clusters](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters) for hello general information on creating HDInsight clusters.</span></span>
3. <span data-ttu-id="fda7d-133">Hello에 **저장소** 블레이드 아래에서 **기본 저장소 형식**을 선택 **데이터 레이크 저장소**, hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-133">On hello **Storage** blade, under **Primary storage type**, select **Data Lake Store**, and then enter hello following information:</span></span>

    <span data-ttu-id="fda7d-134">![추가 서비스 보안 주체 tooHDInsight 클러스터](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.adls.storage.png "추가 서비스 보안 주체 tooHDInsight 클러스터")</span><span class="sxs-lookup"><span data-stu-id="fda7d-134">![Add service principal tooHDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.adls.storage.png "Add service principal tooHDInsight cluster")</span></span>

    - <span data-ttu-id="fda7d-135">**Data Lake Store 계정 선택**: 기존 Data Lake Store 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-135">**Select Data Lake Store account**: Select an existing Data Lake Store account.</span></span> <span data-ttu-id="fda7d-136">기존 Data Lake Store 계정은 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-136">An existing Data Lake Store account is required.</span></span>  <span data-ttu-id="fda7d-137">[필수 조건](#prereuisites)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fda7d-137">See [Prerequisites](#prereuisites).</span></span>
    - <span data-ttu-id="fda7d-138">**루트 경로**: toobe 저장는 hello 클러스터 전용 파일의 위치 경로 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-138">**Root path**: Enter a path where hello cluster-specific files are toobe stored.</span></span> <span data-ttu-id="fda7d-139">hello 스크린 샷 __클러스터/myhdiadlcluster / /__, 어떤 hello에 __클러스터/__ 폴더 존재 해야 하며 hello 포털에서는 *myhdicluster* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-139">On hello screenshot, it is __/clusters/myhdiadlcluster/__, in which hello __/clusters__ folder must exist, and hello Portal creates *myhdicluster* folder.</span></span>  <span data-ttu-id="fda7d-140">hello *myhdicluster* hello 클러스터 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-140">hello *myhdicluster* is hello cluster name.</span></span>
    - <span data-ttu-id="fda7d-141">**데이터 레이크 저장소 액세스**: hello Data Lake 저장소 계정 및 HDInsight 클러스터 간의 액세스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-141">**Data Lake Store access**: Configure access between hello Data Lake Store account and HDInsight cluster.</span></span> <span data-ttu-id="fda7d-142">지침은 [Data Lake Store 액세스 구성](#configure-data-lake-store-access)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fda7d-142">For instructions, see [Configure Data Lake Store access](#configure-data-lake-store-access).</span></span>
    - <span data-ttu-id="fda7d-143">**추가 저장소 계정을**: hello 클러스터에 대 한 계정 추가 저장소로 Azure 저장소 계정을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-143">**Additional storage accounts**: Add Azure Storage Accounts as additional storage accounts for hello cluster.</span></span> <span data-ttu-id="fda7d-144">데이터 레이크 저장소를 추가 하는 tooadd hello 기본 저장소 형식으로 데이터 레이크 저장소 계정을 구성 하는 동안 더 많은 데이터 레이크 저장소 계정에 데이터에 hello 클러스터 사용 권한을 제공 하 여 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-144">tooadd additional Data Lake Stores is done by giving hello cluster permissions on data in more Data Lake Store accounts while configuring a Data Lake Store account as hello primary storage type.</span></span> <span data-ttu-id="fda7d-145">[Data Lake Store 액세스 구성](#configure-data-lake-store-access)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fda7d-145">See [Configure Data Lake Store access](#configure-data-lake-store-access).</span></span>

4. <span data-ttu-id="fda7d-146">Hello에 **데이터 레이크 저장소 액세스**, 클릭 **선택**, 다음에 설명 된 대로 클러스터 만들기를 계속 [HDInsight 클러스터를 만드는 Hadoop](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-146">On hello **Data Lake Store access**, click **Select**, and then continue with cluster creation as described in [Create Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>


### <a name="create-a-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="fda7d-147">Data Lake Store를 추가 저장소로 사용하여 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="fda7d-147">Create a cluster with Data Lake Store as additional storage</span></span>

<span data-ttu-id="fda7d-148">hello 다음 지침 HDInsight 클러스터 만들기 hello 기본 저장소로 Azure 저장소 계정과 추가 저장소로 데이터 레이크 저장소 계정을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="fda7d-148">hello following instructions create a HDInsight cluster with an Azure Storage account as hello default storage, and a Data Lake Store account as an additional storage.</span></span>
<span data-ttu-id="fda7d-149">**hello 기본 저장소 계정으로 데이터 레이크 저장소와 toocreate는 HDInsight 클러스터**</span><span class="sxs-lookup"><span data-stu-id="fda7d-149">**toocreate a HDInsight cluster with a Data Lake Store as hello default storage account**</span></span>

1. <span data-ttu-id="fda7d-150">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-150">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="fda7d-151">에 따라 [클러스터를 만들어](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters) hello 일반 정보는 HDInsight 클러스터를 만드는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-151">Follow [Create clusters](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters) for hello general information on creating HDInsight clusters.</span></span>
3. <span data-ttu-id="fda7d-152">Hello에 **저장소** 블레이드 아래에서 **기본 저장소 형식**을 선택 **Azure 저장소**, hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-152">On hello **Storage** blade, under **Primary storage type**, select **Azure Storage**, and then enter hello following information:</span></span>

    <span data-ttu-id="fda7d-153">![추가 서비스 보안 주체 tooHDInsight 클러스터](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.png "추가 서비스 보안 주체 tooHDInsight 클러스터")</span><span class="sxs-lookup"><span data-stu-id="fda7d-153">![Add service principal tooHDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.png "Add service principal tooHDInsight cluster")</span></span>

    - <span data-ttu-id="fda7d-154">**선택 방법을**: hello 다음 옵션 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-154">**Selection method**: use one of hello following options:</span></span>

        * <span data-ttu-id="fda7d-155">toospecify Azure 구독에 포함 된 저장소 계정을 선택 **내 구독**를 선택한 다음 hello 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-155">toospecify a storage account that is part of your Azure subscription, select **My subscriptions**, and then select hello storage account.</span></span>
        * <span data-ttu-id="fda7d-156">toospecify Azure 구독 외부에 있는 저장소 계정 **선택 키**, 외부 저장소 계정 hello에 대 한 hello 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-156">toospecify a storage account that is outside your Azure subscription, select **Access key**, and then provide hello information for hello outside storage account.</span></span>

    - <span data-ttu-id="fda7d-157">**기본 컨테이너**: hello 기본값 중 하나를 사용 하거나 고유한 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-157">**Default container**: use either hello default value or specify your own name.</span></span>

    - <span data-ttu-id="fda7d-158">추가 저장소 계정: hello 추가 저장소로 Azure 저장소 계정을 더 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-158">Additional Storage accounts: add more Azure Storage accounts as hello additional storage.</span></span>
    - <span data-ttu-id="fda7d-159">데이터 레이크 저장소 액세스: hello Data Lake 저장소 계정 및 HDInsight 클러스터 간의 액세스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-159">Data Lake Store access: configure access between hello Data Lake Store account and HDInsight cluster.</span></span> <span data-ttu-id="fda7d-160">지침은 [Data Lake Store 액세스 구성](#configure-data-lake-store-access)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fda7d-160">For instructions see [Configure Data Lake Store access](#configure-data-lake-store-access).</span></span>

## <a name="configure-data-lake-store-access"></a><span data-ttu-id="fda7d-161">Data Lake Store 액세스 구성</span><span class="sxs-lookup"><span data-stu-id="fda7d-161">Configure Data Lake Store access</span></span> 

<span data-ttu-id="fda7d-162">이 섹션에서는 Azure Active Directory 서비스 주체를 사용하여 HDInsight 클러스터에서 Data Lake Store 액세스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-162">In this section, you configure Data Lake Store access from HDInsight clusters using an Azure Active Directory service principal.</span></span> 

### <a name="specify-a-service-principal"></a><span data-ttu-id="fda7d-163">서비스 주체 지정</span><span class="sxs-lookup"><span data-stu-id="fda7d-163">Specify a service principal</span></span>

<span data-ttu-id="fda7d-164">Hello Azure 포털에서에서 기존 서비스 보안 주체를 사용 하거나 새로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-164">From hello Azure portal, you can either use an existing service principal or create a new one.</span></span>

<span data-ttu-id="fda7d-165">**toocreate hello Azure 포털에서에서 서비스 사용자**</span><span class="sxs-lookup"><span data-stu-id="fda7d-165">**toocreate a service principal from hello Azure portal**</span></span>

1. <span data-ttu-id="fda7d-166">클릭 **데이터 레이크 저장소 액세스** hello 저장소 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-166">Click **Data Lake Store access** from hello Store blade.</span></span>
2. <span data-ttu-id="fda7d-167">Hello에 **데이터 레이크 저장소 액세스** 블레이드에서 클릭 **새로 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-167">On hello **Data Lake Store access** blade, click **Create new**.</span></span>
3. <span data-ttu-id="fda7d-168">클릭 **서비스 사용자**를 선택한 다음 hello 지침 toocreate 서비스 사용자를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-168">Click **Service Principal**, and then follow hello instructions toocreate a service principal.</span></span>
4. <span data-ttu-id="fda7d-169">Toouse 결정 한 경우 hello 인증서를 다운로드 hello 나중에 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-169">Download hello certificate if you decide toouse it again in hello future.</span></span> <span data-ttu-id="fda7d-170">다운로드 hello 인증서 추가 하는 HDInsight 클러스터를 만들 때 보안 주체를 서비스 동일 toouse hello 하려는 경우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-170">Downloading hello certificate is useful if you want toouse hello same service principal when you create additional HDInsight clusters.</span></span>

    <span data-ttu-id="fda7d-171">![추가 서비스 보안 주체 tooHDInsight 클러스터](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.2.png "추가 서비스 보안 주체 tooHDInsight 클러스터")</span><span class="sxs-lookup"><span data-stu-id="fda7d-171">![Add service principal tooHDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.2.png "Add service principal tooHDInsight cluster")</span></span>

4. <span data-ttu-id="fda7d-172">클릭 **액세스** tooconfigure hello 폴더에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-172">Click **Access** tooconfigure hello folder access.</span></span>  <span data-ttu-id="fda7d-173">[파일 권한 구성](#configure-file-permissions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fda7d-173">See [Configure file permissions](#configure-file-permissions).</span></span>


<span data-ttu-id="fda7d-174">**기존 서비스 hello Azure 포털에서에서 사용자 toouse**</span><span class="sxs-lookup"><span data-stu-id="fda7d-174">**toouse an existing service principal from hello Azure portal**</span></span>

1. <span data-ttu-id="fda7d-175">**Data Lake Store 액세스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-175">Click **Data Lake Store access**.</span></span>
1. <span data-ttu-id="fda7d-176">Hello에 **데이터 레이크 저장소 액세스** 블레이드에서 클릭 **기존 항목 사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-176">On hello **Data Lake Store access** blade, click **Use existing**.</span></span>
2. <span data-ttu-id="fda7d-177">**서비스 주체**를 클릭한 다음 서비스 주체를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-177">Click **Service Principal**, and then select a service principal.</span></span> 
3. <span data-ttu-id="fda7d-178">사용자 선택 된 서비스 사용자와 연결 된 hello 인증서 (.pfx 파일)를 업로드 하 고 hello 인증서 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-178">Upload hello certificate (.pfx file) that's associated with your selected service principal, and then enter hello certificate password.</span></span>

    <span data-ttu-id="fda7d-179">![추가 서비스 보안 주체 tooHDInsight 클러스터](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.5.png "추가 서비스 보안 주체 tooHDInsight 클러스터")</span><span class="sxs-lookup"><span data-stu-id="fda7d-179">![Add service principal tooHDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.5.png "Add service principal tooHDInsight cluster")</span></span>

4. <span data-ttu-id="fda7d-180">클릭 **액세스** tooconfigure hello 폴더에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-180">Click **Access** tooconfigure hello folder access.</span></span>  <span data-ttu-id="fda7d-181">[파일 권한 구성](#configure-file-permissions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fda7d-181">See [Configure file permissions](#configure-file-permissions).</span></span>


### <span data-ttu-id="fda7d-182"><a name="configure-file-permissions"></a>파일 권한 구성</span><span class="sxs-lookup"><span data-stu-id="fda7d-182"><a name="configure-file-permissions"></a>Configure file permissions</span></span>

<span data-ttu-id="fda7d-183">hello 구성 hello 기본 저장소 또는 추가 저장소 계정으로 hello 계정 사용 여부에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-183">hello configures are different depending on whether hello account is used as hello default storage or an additional storage account:</span></span>

- <span data-ttu-id="fda7d-184">기본 저장소로 사용됨</span><span class="sxs-lookup"><span data-stu-id="fda7d-184">Used as default storage</span></span>

    - <span data-ttu-id="fda7d-185">데이터 레이크 저장소 계정 hello의 hello 루트 수준에서 사용 권한</span><span class="sxs-lookup"><span data-stu-id="fda7d-185">permission at hello root level of hello Data Lake Store account</span></span>
    - <span data-ttu-id="fda7d-186">hello HDInsight 클러스터 저장소의 hello 루트 수준에서 권한입니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-186">permission at hello root level of hello HDInsight cluster storage.</span></span> <span data-ttu-id="fda7d-187">예를 들어 hello __클러스터/__ hello 자습서의 앞부분에서 사용 되는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-187">For example, hello __/clusters__ folder used earlier in hello tutorial.</span></span>
- <span data-ttu-id="fda7d-188">추가 저장소로 사용</span><span class="sxs-lookup"><span data-stu-id="fda7d-188">Use as an additional storage</span></span>

    - <span data-ttu-id="fda7d-189">액세스를 제출 해야 하는 hello 폴더에 대 한 권한입니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-189">Permission at hello folders where you need file access.</span></span>

<span data-ttu-id="fda7d-190">**hello Data Lake 저장소 계정 루트 수준에서 tooassign 권한**</span><span class="sxs-lookup"><span data-stu-id="fda7d-190">**tooassign permission at hello Data Lake Store account root level**</span></span>

1. <span data-ttu-id="fda7d-191">Hello에 **데이터 레이크 저장소 액세스** 블레이드에서 클릭 **액세스**합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-191">On hello **Data Lake Store access** blade, click **Access**.</span></span> <span data-ttu-id="fda7d-192">hello **파일 사용 권한을 선택** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-192">hello **Select file permissions** blade is opened.</span></span> <span data-ttu-id="fda7d-193">구독에서 모든 hello 데이터 레이크 저장소 계정을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-193">It lists all hello Data Lake Store accounts in your subscription.</span></span>
2. <span data-ttu-id="fda7d-194">마우스를 가져가고 (클릭 하지 마십시오) hello hello Data Lake 저장소 계정 선택 확인란 hello 다음 toomake hello 표시 확인란의 hello 이름 위로 마우스를 가져갑니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-194">Hover (do not click) hello mouse over hello name of hello Data Lake Store account toomake hello check box visible, then select hello check box.</span></span>

    <span data-ttu-id="fda7d-195">![추가 서비스 보안 주체 tooHDInsight 클러스터](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3.png "추가 서비스 보안 주체 tooHDInsight 클러스터")</span><span class="sxs-lookup"><span data-stu-id="fda7d-195">![Add service principal tooHDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3.png "Add service principal tooHDInsight cluster")</span></span>

  <span data-ttu-id="fda7d-196">기본적으로 __읽기__, __쓰기__ 및 __실행__이 모두 선택되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-196">By default, __READ__, __WRITE__, AND __EXECUTE__ are all selected.</span></span>

3. <span data-ttu-id="fda7d-197">클릭 **선택** hello hello 페이지 아래쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-197">Click **Select** on hello bottom of hello page.</span></span>
4. <span data-ttu-id="fda7d-198">클릭 **실행** tooassign 권한.</span><span class="sxs-lookup"><span data-stu-id="fda7d-198">Click **Run** tooassign permission.</span></span>
5. <span data-ttu-id="fda7d-199">**Done**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-199">Click **Done**.</span></span>

<span data-ttu-id="fda7d-200">**hello HDInsight 클러스터 루트 수준에서 tooassign 권한**</span><span class="sxs-lookup"><span data-stu-id="fda7d-200">**tooassign permission at hello HDInsight cluster root level**</span></span>

1. <span data-ttu-id="fda7d-201">Hello에 **데이터 레이크 저장소 액세스** 블레이드에서 클릭 **액세스**합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-201">On hello **Data Lake Store access** blade, click **Access**.</span></span> <span data-ttu-id="fda7d-202">hello **파일 사용 권한을 선택** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-202">hello **Select file permissions** blade is opened.</span></span> <span data-ttu-id="fda7d-203">구독에서 모든 hello 데이터 레이크 저장소 계정을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-203">It lists all hello Data Lake Store accounts in your subscription.</span></span>
1. <span data-ttu-id="fda7d-204">Hello에서 **파일 사용 권한을 선택** 블레이드에서 hello 데이터 레이크 저장소 이름 tooshow 해당 콘텐츠를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-204">From hello **Select file permissions** blade, click hello Data Lake Store name tooshow its content.</span></span>
2. <span data-ttu-id="fda7d-205">Hello hello 왼쪽 hello 폴더의 확인란을 선택 하 여 hello HDInsight 클러스터 저장소 루트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-205">Select hello HDInsight cluster storage root by selecting hello checkbox on hello left of hello folder.</span></span> <span data-ttu-id="fda7d-206">Hello 클러스터 저장소 루트는 toohello 스크린 샷을 이전 버전에 따라, __클러스터/__ 기본 저장소로 hello 데이터 레이크 저장소를 선택 하는 동안 지정한 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-206">According toohello screenshot earlier, hello cluster storage root is __/clusters__ folder that you specified while selecting hello Data Lake Store as default storage.</span></span>
3. <span data-ttu-id="fda7d-207">Hello 폴더에 hello 사용 권한을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-207">Set hello permissions on hello folder.</span></span>  <span data-ttu-id="fda7d-208">기본적으로 읽기, 쓰기 및 실행이 모두 선택되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-208">By default, read, write, and execute are all selected.</span></span>
4. <span data-ttu-id="fda7d-209">클릭 **선택** hello hello 페이지 아래쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-209">Click **Select** on hello bottom of hello page.</span></span>
5. <span data-ttu-id="fda7d-210">**실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-210">Click **Run**.</span></span>
6. <span data-ttu-id="fda7d-211">**Done**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-211">Click **Done**.</span></span>

<span data-ttu-id="fda7d-212">데이터 레이크 저장소로 추가 저장소를 사용 하는 경우 할당 해야 hello 폴더에 대 한 권한을 hello HDInsight 클러스터에서 tooaccess 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-212">If you are using Data Lake Store as additional storage, you must assign permission only for hello folders that you want tooaccess from hello HDInsight cluster.</span></span> <span data-ttu-id="fda7d-213">예를 들어 아래 hello 스크린샷에서에서 제공한 액세스 너무만**hdiaddonstorage** 데이터 레이크 저장소 계정에는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-213">For example, in hello screenshot below, you provide access only too**hdiaddonstorage** folder in a Data Lake Store account.</span></span>

<span data-ttu-id="fda7d-214">![서비스 보안 주체 권한 toohello HDInsight 클러스터 할당](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3-1.png "할당 서비스 보안 주체 권한 toohello HDInsight 클러스터")</span><span class="sxs-lookup"><span data-stu-id="fda7d-214">![Assign service principal permissions toohello HDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3-1.png "Assign service principal permissions toohello HDInsight cluster")</span></span>


## <a name="verify-cluster-set-up"></a><span data-ttu-id="fda7d-215">클러스터 설정 확인</span><span class="sxs-lookup"><span data-stu-id="fda7d-215">Verify cluster set up</span></span>

<span data-ttu-id="fda7d-216">Hello 클러스터 설치가 완료 되 면 hello 클러스터 블레이드에서 결과 확인 단계를 수행 하는 hello 중 하나 또는 모두를 수행 하 여:</span><span class="sxs-lookup"><span data-stu-id="fda7d-216">After hello cluster setup is complete, on hello cluster blade, verify your results by doing either or both of hello following steps:</span></span>

* <span data-ttu-id="fda7d-217">hello 클러스터는 지정한 hello 데이터 레이크 저장소 계정에 대 한 연결 된 저장소를 hello를 클릭 tooverify **저장소 계정은** hello 왼쪽된 창에서.</span><span class="sxs-lookup"><span data-stu-id="fda7d-217">tooverify that hello associated storage for hello cluster is hello Data Lake Store account that you specified, click **Storage accounts** in hello left pane.</span></span>

    <span data-ttu-id="fda7d-218">![추가 서비스 보안 주체 tooHDInsight 클러스터](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6-1.png "추가 서비스 보안 주체 tooHDInsight 클러스터")</span><span class="sxs-lookup"><span data-stu-id="fda7d-218">![Add service principal tooHDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6-1.png "Add service principal tooHDInsight cluster")</span></span>

* <span data-ttu-id="fda7d-219">서비스 사용자 hello tooverify 올바르게 hello HDInsight 클러스터와 연결 된, 클릭 **데이터 레이크 저장소 액세스** hello 왼쪽된 창에서.</span><span class="sxs-lookup"><span data-stu-id="fda7d-219">tooverify that hello service principal is correctly associated with hello HDInsight cluster, click **Data Lake Store access** in hello left pane.</span></span>

    <span data-ttu-id="fda7d-220">![추가 서비스 보안 주체 tooHDInsight 클러스터](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6.png "추가 서비스 보안 주체 tooHDInsight 클러스터")</span><span class="sxs-lookup"><span data-stu-id="fda7d-220">![Add service principal tooHDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6.png "Add service principal tooHDInsight cluster")</span></span>


## <a name="examples"></a><span data-ttu-id="fda7d-221">예</span><span class="sxs-lookup"><span data-stu-id="fda7d-221">Examples</span></span>

<span data-ttu-id="fda7d-222">데이터 레이크 저장소를 사용 하는 hello 클러스터에서 저장소로 설정한 후에 어떻게 toouse HDInsight 클러스터 데이터 레이크 저장소에 저장 된 tooanalyze hello 데이터의 toothese 예 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="fda7d-222">After you have set up hello cluster with Data Lake Store as your storage, refer toothese examples of how toouse HDInsight cluster tooanalyze hello data that's stored in Data Lake Store.</span></span>

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-primary-storage"></a><span data-ttu-id="fda7d-223">기본 저장소인 Data Lake Store에서 데이터에 대한 Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="fda7d-223">Run a Hive query against data in a Data Lake Store (as primary storage)</span></span>

<span data-ttu-id="fda7d-224">toorun 하이브 쿼리 hello Ambari 포털에서 hello 하이브 뷰 인터페이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-224">toorun a Hive query, use hello Hive views interface in hello Ambari portal.</span></span> <span data-ttu-id="fda7d-225">Ambari 하이브 toouse 보는 방법에 지침은 [사용 하 여 hello HDInsight에서 Hadoop으로 하이브 보기](../hdinsight/hdinsight-hadoop-use-hive-ambari-view.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-225">For instructions on how toouse Ambari Hive views, see [Use hello Hive View with Hadoop in HDInsight](../hdinsight/hdinsight-hadoop-use-hive-ambari-view.md).</span></span>

<span data-ttu-id="fda7d-226">데이터 레이크 저장소의 데이터로 작업할 때 문자열 toochange 몇 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-226">When you work with data in a Data Lake Store, there are a few strings toochange.</span></span>

<span data-ttu-id="fda7d-227">Hello 경로 toohello 데이터를 사용 하는 경우, 예를 들어 주 저장소로 데이터 레이크 저장소를 사용 하 여 만든 hello 클러스터: *adl: / / < data_lake_store_account_name > /azuredatalakestore.net/path/to/file*합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-227">If you use, for example, hello cluster that you created with Data Lake Store as primary storage, hello path toohello data is: *adl://<data_lake_store_account_name>/azuredatalakestore.net/path/to/file*.</span></span> <span data-ttu-id="fda7d-228">하이브 쿼리 toocreate hello Data Lake 저장소 계정에에서 저장 되어 있는 샘플 데이터에서 테이블 문 다음 hello 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-228">A Hive query toocreate a table from sample data that's stored in hello Data Lake Store account looks like hello following statement:</span></span>

    CREATE EXTERNAL TABLE websitelog (str string) LOCATION 'adl://hdiadlsstorage.azuredatalakestore.net/clusters/myhdiadlcluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/'

<span data-ttu-id="fda7d-229">설명:</span><span class="sxs-lookup"><span data-stu-id="fda7d-229">Descriptions:</span></span>
* <span data-ttu-id="fda7d-230">`adl://hdiadlstorage.azuredatalakestore.net/`데이터 레이크 저장소 계정 hello hello 루트가입니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-230">`adl://hdiadlstorage.azuredatalakestore.net/` is hello root of hello Data Lake Store account.</span></span>
* <span data-ttu-id="fda7d-231">`/clusters/myhdiadlcluster`hello 클러스터를 만드는 동안 지정한 hello 클러스터 데이터의 hello 루트가입니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-231">`/clusters/myhdiadlcluster` is hello root of hello cluster data that you specified while creating hello cluster.</span></span>
* <span data-ttu-id="fda7d-232">`/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/`hello hello 쿼리에서 사용 하는 hello 샘플 파일 위치가입니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-232">`/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/` is hello location of hello sample file that you used in hello query.</span></span>

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-additional-storage"></a><span data-ttu-id="fda7d-233">추가 저장소인 Data Lake Store에 저장된 데이터에 대한 Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="fda7d-233">Run a Hive query against data in a Data Lake Store (as additional storage)</span></span>

<span data-ttu-id="fda7d-234">Blob 저장소를 사용 하 여 기본 저장소로 만든 hello 클러스터, 샘플 데이터 hello hello 추가 저장소로 사용 되는 Azure 데이터 레이크 저장소 계정에에서 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-234">If hello cluster that you created uses Blob storage as default storage, hello sample data is not contained in hello Azure Data Lake Store account that's used as additional storage.</span></span> <span data-ttu-id="fda7d-235">이 경우 먼저 Blob 저장소 toohello 데이터 레이크 저장소에서에서 hello 데이터를 전송 하 고 hello 이전 예제와 같이 hello 쿼리를 실행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="fda7d-235">In such a case, first transfer hello data from Blob storage toohello Data Lake Store, and then run hello queries as shown in hello preceding example.</span></span>

<span data-ttu-id="fda7d-236">어떻게 toocopy 데이터 Blob 저장소에서 tooa 데이터 레이크 저장소에 대 한 내용은 다음 문서는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="fda7d-236">For information on how toocopy data from Blob storage tooa Data Lake Store, see hello following articles:</span></span>

* [<span data-ttu-id="fda7d-237">Azure 저장소 blob와 데이터 레이크 저장소 간에 Distcp toocopy 데이터 사용</span><span class="sxs-lookup"><span data-stu-id="fda7d-237">Use Distcp toocopy data between Azure Storage blobs and Data Lake Store</span></span>](data-lake-store-copy-data-wasb-distcp.md)
* [<span data-ttu-id="fda7d-238">Azure 저장소에서 사용 하 여 AdlCopy toocopy 데이터 레이크 저장소 tooData blob</span><span class="sxs-lookup"><span data-stu-id="fda7d-238">Use AdlCopy toocopy data from Azure Storage blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)

### <a name="use-data-lake-store-with-a-spark-cluster"></a><span data-ttu-id="fda7d-239">Spark 클러스터에서 Data Lake Store 사용</span><span class="sxs-lookup"><span data-stu-id="fda7d-239">Use Data Lake Store with a Spark cluster</span></span>
<span data-ttu-id="fda7d-240">데이터 레이크 저장소에 저장 된 데이터에서 Spark 클러스터 toorun Spark 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-240">You can use a Spark cluster toorun Spark jobs on data that is stored in a Data Lake Store.</span></span> <span data-ttu-id="fda7d-241">자세한 내용은 참조 [데이터 레이크 저장소에서 사용 하 여 HDInsight Spark 클러스터 tooanalyze 데이터](../hdinsight/hdinsight-apache-spark-use-with-data-lake-store.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-241">For more information, see [Use HDInsight Spark cluster tooanalyze data in Data Lake Store](../hdinsight/hdinsight-apache-spark-use-with-data-lake-store.md).</span></span>


### <a name="use-data-lake-store-in-a-storm-topology"></a><span data-ttu-id="fda7d-242">Storm 토폴로지에서 Data Lake 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="fda7d-242">Use Data Lake Store in a Storm topology</span></span>
<span data-ttu-id="fda7d-243">Storm 토폴로지에서 hello 데이터 레이크 저장소 toowrite 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-243">You can use hello Data Lake Store toowrite data from a Storm topology.</span></span> <span data-ttu-id="fda7d-244">방법에 대 한 지침은 tooachieve이이 시나리오에서는 참조 [HDInsight와 Apache Storm를 사용 하 여 Azure 데이터 레이크 저장소](../hdinsight/hdinsight-storm-write-data-lake-store.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fda7d-244">For instructions on how tooachieve this scenario, see [Use Azure Data Lake Store with Apache Storm with HDInsight](../hdinsight/hdinsight-storm-write-data-lake-store.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="fda7d-245">참고 항목</span><span class="sxs-lookup"><span data-stu-id="fda7d-245">See also</span></span>
* [<span data-ttu-id="fda7d-246">PowerShell: 만들 HDInsight 클러스터 toouse 데이터 레이크 저장소</span><span class="sxs-lookup"><span data-stu-id="fda7d-246">PowerShell: Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
