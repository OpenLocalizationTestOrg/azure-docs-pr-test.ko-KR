---
title: "웹 브라우저-Azure HDInsight를 사용 하 여 aaaCreate Hadoop 클러스터 | Microsoft Docs"
description: "Azure preview 포털 hello와 어떻게 toocreate Hadoop, HBase, 스톰, 또는 Spark 클러스터로 Linux 웹 브라우저를 사용 하 여 HDInsight에 대 한 알아봅니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 697278cf-0032-4f7c-b9b2-a84c4347659e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 63027e35e2d66dd76218aff3e0c085fc811736ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-hello-azure-portal"></a><span data-ttu-id="90470-103">Hello Azure 포털을 사용 하 여 HDInsight의 Linux 기반 클러스터를 만들려면</span><span class="sxs-lookup"><span data-stu-id="90470-103">Create Linux-based clusters in HDInsight using hello Azure portal</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="90470-104">Azure 포털 hello는 서비스 및 hello Microsoft Azure 클라우드에서 호스트 되는 리소스에 대 한 웹 기반 관리 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="90470-104">hello Azure portal is a web-based management tool for services and resources hosted in hello Microsoft Azure cloud.</span></span> <span data-ttu-id="90470-105">이 문서에서 toocreate Linux 기반 HDInsight 클러스터 hello 포털을 사용 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="90470-105">In this article you will learn how toocreate Linux-based HDInsight clusters using hello portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90470-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="90470-106">Prerequisites</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="90470-107">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="90470-107">**An Azure subscription**.</span></span> <span data-ttu-id="90470-108">[Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90470-108">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="90470-109">**최신 웹 브라우저**.</span><span class="sxs-lookup"><span data-stu-id="90470-109">**A modern web browser**.</span></span> <span data-ttu-id="90470-110">Azure 포털 hello HTML5 및 Javascript를 사용 하 여 및 이전 버전의 웹 브라우저에서 제대로 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90470-110">hello Azure  portal uses HTML5 and Javascript, and may not function correctly in older web browsers.</span></span>

## <a name="create-clusters"></a><span data-ttu-id="90470-111">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="90470-111">Create clusters</span></span>
<span data-ttu-id="90470-112">Azure 포털 hello hello 클러스터 속성의 대부분을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-112">hello Azure portal exposes most of hello cluster properties.</span></span> <span data-ttu-id="90470-113">Azure Resource Manager 템플릿을 사용하여 이러한 많은 속성을 숨길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90470-113">Using Azure Resource Manager template, you can hide a lot of details.</span></span> <span data-ttu-id="90470-114">자세한 내용은 [Azure Resource Manager 템플릿을 사용하여 HDInsight의 Linux 기반 Hadoop 클러스터 만들기](hdinsight-hadoop-create-linux-clusters-arm-templates.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90470-114">For more information, see [Create Linux-based Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md).</span></span>

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


1. <span data-ttu-id="90470-115">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-115">Sign in toohello [Azure  portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="90470-116">**+**, **인텔리전스 + 분석** 및 **HDInsight**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-116">Click **+**, click **Intelligence + Analytics**, and then click **HDInsight**.</span></span>
   
    <span data-ttu-id="90470-117">![Hello Azure 포털에서에서 새 클러스터를 만드는](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster.png "hello Azure 포털에서에서 새 클러스터 만들기")</span><span class="sxs-lookup"><span data-stu-id="90470-117">![Creating a new cluster in hello Azure portal](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster.png "Creating a new cluster in hello Azure portal")</span></span>

3. <span data-ttu-id="90470-118">Hello에 **HDInsight** 블레이드에서 클릭 **(크기, 설정, 응용 프로그램) 사용자 지정**, 클릭 **기본 사항**, hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-118">In hello **HDInsight** blade, click **Custom (size, settings, apps)**, click **Basics**, and then enter hello following information.</span></span>

    <span data-ttu-id="90470-119">![Hello Azure 포털에서에서 새 클러스터를 만드는](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-basics.png "hello Azure 포털에서에서 새 클러스터 만들기")</span><span class="sxs-lookup"><span data-stu-id="90470-119">![Creating a new cluster in hello Azure portal](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-basics.png "Creating a new cluster in hello Azure portal")</span></span>

    * <span data-ttu-id="90470-120">**클러스터 이름**입력: 이 이름은 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-120">Enter **Cluster Name**: This name must be globally unique.</span></span>

    * <span data-ttu-id="90470-121">Hello에서 **구독** 드롭다운 목록에서 선택 hello hello 클러스터에 사용할 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="90470-121">From hello **Subscription** drop-down, select hello Azure subscription that will be used for hello cluster.</span></span>

    * <span data-ttu-id="90470-122">**클러스터 유형**을 클릭한 후 다음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-122">Click **Cluster type**, and then select:</span></span>
   
        * <span data-ttu-id="90470-123">**클러스터 유형**: 어떤 toochoose를 모르는 경우 선택 **Hadoop**합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-123">**Cluster Type**: If you don't know what toochoose, select **Hadoop**.</span></span> <span data-ttu-id="90470-124">Hello 가장 인기 있는 클러스터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="90470-124">It is hello most popular cluster type.</span></span>
     
            > [!IMPORTANT]
            > <span data-ttu-id="90470-125">HDInsight 클러스터 hello 기술에 대 한 튜닝 또는 클러스터 toohello 작업 부하를 해당 형식에 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-125">HDInsight clusters come in a variety of types, which correspond toohello workload or technology that hello cluster is tuned for.</span></span> <span data-ttu-id="90470-126">Storm 및 한 개의 클러스터에서 HBase 같은 여러 형식을 결합 하는 클러스터는 지원 되는 방법은 toocreate 없습니다.</span><span class="sxs-lookup"><span data-stu-id="90470-126">There is no supported method toocreate a cluster that combines multiple types, such as Storm and HBase on one cluster.</span></span> 
            > 
            > 
        
        * <span data-ttu-id="90470-127">**운영 체제**: **Linux**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-127">**Operating System**: Select **Linux**.</span></span>
        
        * <span data-ttu-id="90470-128">**버전**: 어떤 toochoose 모르는 경우 hello 기본 버전을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-128">**Version**: Use hello default version if you don't know what toochoose.</span></span> <span data-ttu-id="90470-129">자세한 내용은 [HDInsight 클러스터 버전](hdinsight-component-versioning.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90470-129">For more information, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>
        * <span data-ttu-id="90470-130">**계층 클러스터**: 두 가지 범주의 hello 빅 데이터 클라우드 서비스를 제공 하는 Azure HDInsight: 표준 계층과 고급 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="90470-130">**Cluster Tier**: Azure HDInsight provides hello big data cloud offerings in two categories: Standard tier and Premium tier.</span></span> <span data-ttu-id="90470-131">자세한 내용은 [클러스터 계층](hdinsight-hadoop-provision-linux-clusters.md#cluster-tiers)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90470-131">For more information, see [Cluster tiers](hdinsight-hadoop-provision-linux-clusters.md#cluster-tiers).</span></span>

    * <span data-ttu-id="90470-132">에 대 한 **클러스터 로그인 사용자 이름과** 및 **클러스터 로그인 암호**, hello 사용자 이름 및 hello 관리: 사용자에 대 한 암호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-132">For **Cluster login username** and **Cluster login password**, provide hello username and password for hello admin user.</span></span>

    * <span data-ttu-id="90470-133">입력 한 **SSH 사용자 이름** toohave hello SSH 암호가 이전에 지정한 관리자 암호와 동일 hello를 사용 하도록 하려는 경우 선택 hello **동일한 암호를 사용 하 여 클러스터 로그인으로** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-133">Enter an **SSH Username** and if you want toohave hello SSH password same as hello admin password you specified earlier, select hello **Use same password as cluster login** check box.</span></span> <span data-ttu-id="90470-134">그렇지 않은 경우 제공 중 하나는 **암호** 또는 **공개 키**를 사용 하는 tooauthenticate hello SSH 사용자 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90470-134">If not, provide either a **PASSWORD** or **PUBLIC KEY**, which will be used tooauthenticate hello SSH user.</span></span> <span data-ttu-id="90470-135">공개 키를 사용 하 여 hello 권장 접근법입니다.</span><span class="sxs-lookup"><span data-stu-id="90470-135">Using a public key is hello recommended approach.</span></span> <span data-ttu-id="90470-136">클릭 **선택** hello 아래쪽 toosave hello 자격 증명 구성 시.</span><span class="sxs-lookup"><span data-stu-id="90470-136">Click **Select** at hello bottom toosave hello credentials configuration.</span></span>
   
        <span data-ttu-id="90470-137">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90470-137">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

    * <span data-ttu-id="90470-138">에 대 한 **리소스 그룹**, 여부를 지정할 toocreate 새 리소스 그룹을 원하는 기존 집합을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-138">For **Resource group**, specify whether you want toocreate a new resource group or use an existing one.</span></span>

    * <span data-ttu-id="90470-139">데이터 센터 지정 **위치** hello 클러스터를 만들 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="90470-139">Specify a data center **location** where hello cluster will be created.</span></span>

    * <span data-ttu-id="90470-140">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="90470-140">Click **Next**.</span></span>

4. <span data-ttu-id="90470-141">Hello에 **저장소** 블레이드를 기본 저장소로 Azure 저장소 (WASB) 또는 데이터 레이크 저장소 사용할지를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-141">On hello **Storage** blade, specify whether you want Azure Storage (WASB) or Data Lake Store as your default storage.</span></span> <span data-ttu-id="90470-142">자세한 내용은 아래 hello 표 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-142">Look at hello table below for more information.</span></span>

    <span data-ttu-id="90470-143">![Hello Azure 포털에서에서 새 클러스터를 만드는](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-storage.png "hello Azure 포털에서에서 새 클러스터 만들기")</span><span class="sxs-lookup"><span data-stu-id="90470-143">![Creating a new cluster in hello Azure portal](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-storage.png "Creating a new cluster in hello Azure portal")</span></span>

    | <span data-ttu-id="90470-144">저장소</span><span class="sxs-lookup"><span data-stu-id="90470-144">Storage</span></span>                                      | <span data-ttu-id="90470-145">설명</span><span class="sxs-lookup"><span data-stu-id="90470-145">Description</span></span> |
    |----------------------------------------------|-------------|
    | <span data-ttu-id="90470-146">**기본 저장소인 Azure Storage Blob**</span><span class="sxs-lookup"><span data-stu-id="90470-146">**Azure Storage Blobs as default storage**</span></span>   | <ul><li><span data-ttu-id="90470-147">**기본 저장소 형식**으로 **Azure Storage**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-147">For **Primary Storage type**, select **Azure Storage**.</span></span> <span data-ttu-id="90470-148">그 후에 대 한 **선택 방법을**를 선택할 수 있습니다 **내 구독** Azure 구독에 포함 된 저장소 계정 및 저장소 계정 선택 hello toospecify 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="90470-148">After that, for **Selection method**, you can choose **My subscriptions** if you want toospecify a storage account that is part of your Azure subscription and then select hello storage account.</span></span> <span data-ttu-id="90470-149">그렇지 않으면 클릭 **선택 키** 외부 Azure 구독에서 toochoose 되도록 hello 저장소 계정에 대 한 hello 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-149">Otherwise, click **Access key** and provide hello information for hello storage account that you want toochoose from outside your Azure subscription.</span></span></li><li><span data-ttu-id="90470-150">에 대 한 **기본 컨테이너**를 직접 지정 하거나 toogo hello 포털에 제안 된 hello 기본 컨테이너 이름으로 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90470-150">For **Default container**, you can choose toogo with hello default container name suggested by hello portal or specify your own.</span></span></li><li><span data-ttu-id="90470-151">WASB를 기본 저장소로 사용 하는 경우 클릭할 수 있는 (선택 사항) **추가 저장소 계정을** toospecify 추가 저장소 계정 hello 클러스터와 tooassociate 합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-151">If you are using WASB as default storage, you can (optionally) click **Additional Storage Accounts** toospecify additional storage accounts tooassociate with hello cluster.</span></span> <span data-ttu-id="90470-152">Hello에 **Azure 저장소 키** 블레이드에서 클릭 **저장소 키를 추가**, 다음 제공할 수 있습니다는 저장소 계정을 Azure 구독 또는 다른 구독에서 (함으로써 hello 저장소 계정 선택 키)입니다.</span><span class="sxs-lookup"><span data-stu-id="90470-152">In hello **Azure Storage Keys** blade, click **Add a storage key**, and then you can provide a storage account from your Azure subscriptions or from other subscriptions (by providing hello storage account access key).</span></span></li><li><span data-ttu-id="90470-153">WASB를 기본 저장소로 사용 하는 경우 클릭할 수 있는 (선택 사항) **데이터 레이크 저장소 액세스** toospecify 추가 저장소로 Azure 데이터 레이크 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="90470-153">If you are using WASB as default storage, you can (optionally) click **Data Lake Store access** toospecify Azure Data Lake Store as additional storage.</span></span> <span data-ttu-id="90470-154">자세한 내용은 [Azure Portal을 사용하여 Data Lake Store로 HDInsight 클러스터 만들기](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90470-154">For more information, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span></li></ul> |
    | <span data-ttu-id="90470-155">**기본 저장소로 Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="90470-155">**Azure Data Lake Store as default storage**</span></span> | <span data-ttu-id="90470-156">에 대 한 **기본 저장소 형식**선택, **데이터 레이크 저장소** toohello 문서를 참조 하십시오 [Azure 포털을 사용 하 여 데이터 레이크 저장소는 HDInsight 클러스터 만들기](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md) 에 대 한 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="90470-156">For **Primary storage type**, select **Data Lake Store** and then refer toohello article [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md) for instructions.</span></span> |
    | <span data-ttu-id="90470-157">**외부 Metastore**</span><span class="sxs-lookup"><span data-stu-id="90470-157">**External metastores**</span></span>                      | <span data-ttu-id="90470-158">필요에 따라 SQL 데이터베이스 toosave Hive 및 Oozie 메타 데이터 hello 클러스터와 연결 된 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90470-158">Optionally, you can specify a SQL database toosave Hive and Oozie metadata associated with hello cluster.</span></span> <span data-ttu-id="90470-159">에 대 한 **하이브에 대 한 SQL 데이터베이스를 선택 합니다.** SQL 데이터베이스를 선택 하 고 다음 hello 데이터베이스에 대 한 hello 사용자 이름/암호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-159">For **Select a SQL database for Hive** select a SQL database, and then provide hello username/password for hello database.</span></span> <span data-ttu-id="90470-160">Oozie 메타데이터에 대해 이러한 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-160">Repeat these steps for Oozie metadata.</span></span><br><br><span data-ttu-id="90470-161">metastores에 대한 Azure SQL Database를 사용하는 동안 몇 가지 고려 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="90470-161">Some considerations while using Azure SQL database for metastores.</span></span> <ul><li><span data-ttu-id="90470-162">hello Azure SQL 데이터베이스 metastore hello에 사용 되는 연결 tooother Azure HDInsight를 포함 한 Azure 서비스를 허용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-162">hello Azure SQL database used for hello metastore must allow connectivity tooother Azure services, including Azure HDInsight.</span></span> <span data-ttu-id="90470-163">Hello Azure SQL 데이터베이스 대시보드 hello 오른쪽에에서 hello 서버 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-163">On hello Azure SQL database dashboard, on hello right side, click hello server name.</span></span> <span data-ttu-id="90470-164">어떤 hello SQL 데이터베이스 인스턴스가 실행 중인 hello 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="90470-164">This is hello server on which hello SQL database instance is running.</span></span> <span data-ttu-id="90470-165">Hello 서버 보기에서 후 클릭 **구성**, 고 **Azure 서비스**, 클릭 **예**, 클릭 하 고 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-165">Once you are on hello server view, click **Configure**, and then for **Azure Services**, click **Yes**, and then click **Save**.</span></span></li><li><span data-ttu-id="90470-166">Metastore는를 만들 때는 hello 클러스터 만들기 프로세스 toofail 생길 수 있으므로 대시 또는 하이픈을 포함 하는 데이터베이스 이름을 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="90470-166">When creating a metastore, do not use a database name that contains dashes or hyphens, as this can cause hello cluster creation process toofail.</span></span></li></ul>                                                                                                                                                                       |

    <span data-ttu-id="90470-167">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="90470-167">Click **Next**.</span></span> 

    > [!WARNING]
    > <span data-ttu-id="90470-168">추가 저장소 계정을 사용 하 여 hello HDInsight 클러스터와 다른 위치에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90470-168">Using an additional storage account in a different location than hello HDInsight cluster is not supported.</span></span>

5. <span data-ttu-id="90470-169">필요에 따라 **응용 프로그램** HDInsight 클러스터와 함께 작동 하는 tooinstall 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="90470-169">Optionally, click **Applications** tooinstall applications that work with HDInsight clusters.</span></span> <span data-ttu-id="90470-170">Microsoft, ISV(독립 소프트웨어 공급 업체) 또는 사용자가 직접 이러한 응용 프로그램을 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90470-170">These applications can be developed by Microsoft, independent software vendors (ISV) or by yourself.</span></span> <span data-ttu-id="90470-171">자세한 내용은 [HDInsight 응용 프로그램 설치](hdinsight-apps-install-applications.md#install-applications-during-cluster-creation)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90470-171">For more information, see [Install HDInsight applications](hdinsight-apps-install-applications.md#install-applications-during-cluster-creation).</span></span>


6. <span data-ttu-id="90470-172">클릭 **클러스터 크기** 이 클러스터에 대해 생성 되는 hello 노드에 대 한 toodisplay 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="90470-172">Click **Cluster size** toodisplay information about hello nodes that will be created for this cluster.</span></span> <span data-ttu-id="90470-173">Hello hello 클러스터에 필요한 작업자 노드 수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-173">Set hello number of worker nodes that you need for hello cluster.</span></span> <span data-ttu-id="90470-174">hello 예상 비용 hello 클러스터의 hello 블레이드 내에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90470-174">hello estimated cost of hello cluster will be shown within hello blade.</span></span>
   
    <span data-ttu-id="90470-175">![노드 가격 책정 계층 블레이드](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-nodes.png "클러스터 노드 수 지정")</span><span class="sxs-lookup"><span data-stu-id="90470-175">![Node pricing tiers blade](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-nodes.png "Specify number of cluster nodes")</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="90470-176">32 개 이상의 작업자 노드를 하려는 경우 클러스터를 만들 때 또는 적어도 8 코어, 14GB에 헤드 노드 크기를 선택 해야 합니다를 만든 후 hello 클러스터를 확장 하 여 ram.</span><span class="sxs-lookup"><span data-stu-id="90470-176">If you plan on more than 32 worker nodes, either at cluster creation or by scaling hello cluster after creation, then you must select a head node size with at least 8 cores and 14GB ram.</span></span>
   > 
   > <span data-ttu-id="90470-177">노드 크기 및 관련된 비용에 대한 자세한 내용은 [HDInsight 가격 책정](https://azure.microsoft.com/pricing/details/hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90470-177">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>
   > 
   > 
   
   <span data-ttu-id="90470-178">클릭 **다음** toosave hello 노드 가격 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-178">Click **Next** toosave hello node pricing configuration.</span></span>

7. <span data-ttu-id="90470-179">클릭 **고급 설정** tooconfigure 사용 하는 등 기타 옵션 설정 **스크립트 동작** toocustomize 클러스터 tooinstall 조인 또는 사용자 지정 구성 요소는 **가상네트워크**.</span><span class="sxs-lookup"><span data-stu-id="90470-179">Click **Advanced settings** tooconfigure other optional settings such as using **Script Actions** toocustomize a cluster tooinstall custom components or joining a **Virtual Network**.</span></span> <span data-ttu-id="90470-180">자세한 내용은 아래 hello 표 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-180">Look at hello table below for more information.</span></span>

    <span data-ttu-id="90470-181">![노드 가격 책정 계층 블레이드](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-advanced.png "클러스터 노드 수 지정")</span><span class="sxs-lookup"><span data-stu-id="90470-181">![Node pricing tiers blade](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-advanced.png "Specify number of cluster nodes")</span></span>

    | <span data-ttu-id="90470-182">옵션</span><span class="sxs-lookup"><span data-stu-id="90470-182">Option</span></span> | <span data-ttu-id="90470-183">설명</span><span class="sxs-lookup"><span data-stu-id="90470-183">Description</span></span> |
    |--------|-------------|
    | <span data-ttu-id="90470-184">**스크립트 작업**</span><span class="sxs-lookup"><span data-stu-id="90470-184">**Script Actions**</span></span> | <span data-ttu-id="90470-185">Hello 클러스터를 만드는 중으로 toouse 사용자 지정 스크립트 toocustomize는 클러스터를 원하는 경우이 옵션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-185">Use this option if you want toouse a custom script toocustomize a cluster, as hello cluster is being created.</span></span> <span data-ttu-id="90470-186">스크립트 동작에 대한 자세한 내용은 [스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90470-186">For more information about script actions, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span> |
    | <span data-ttu-id="90470-187">**Virtual Network**</span><span class="sxs-lookup"><span data-stu-id="90470-187">**Virtual Network**</span></span> | <span data-ttu-id="90470-188">Tooplace hello 클러스터 내 가상 네트워크에 Azure 가상 네트워크 및 hello 서브넷을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-188">Select an Azure virtual network and hello subnet if you want tooplace hello cluster into a virtual network.</span></span> <span data-ttu-id="90470-189">HDInsight를 사용 하 여 hello 가상 네트워크에 대 한 특정 구성 요구 사항을 포함 하 여 가상 네트워크에 대 한 내용은 [Azure 가상 네트워크를 사용 하 여 HDInsight 확장 기능](hdinsight-extend-hadoop-virtual-network.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-189">For information on using HDInsight with a Virtual Network, including specific configuration requirements for hello Virtual Network, see [Extend HDInsight capabilities by using an Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span></span> |

    <span data-ttu-id="90470-190">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="90470-190">Click **Next**.</span></span>

8. <span data-ttu-id="90470-191">Hello에 **요약** 블레이드에서 이전에 입력 한 hello 정보를 확인 하 고 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-191">On hello **Summary** blade, verify hello information you entered earlier and then click **Create**.</span></span>

    <span data-ttu-id="90470-192">![노드 가격 책정 계층 블레이드](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-summary.png "클러스터 노드 수 지정")</span><span class="sxs-lookup"><span data-stu-id="90470-192">![Node pricing tiers blade](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-summary.png "Specify number of cluster nodes")</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="90470-193">일반적으로 약 15 분을 만든 hello 클러스터 toobe 약간의 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="90470-193">It will take some time for hello cluster toobe created, usually around 15 minutes.</span></span> <span data-ttu-id="90470-194">Hello 타일 hello 시작 보드를 사용 하거나 hello **알림** hello 페이지 toocheck의 프로 비전 프로세스는 hello에 남아 있는 hello에 대 한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="90470-194">Use hello tile on hello Startboard, or hello **Notifications** entry on hello left of hello page toocheck on hello provisioning process.</span></span>
    > 
    > 
12. <span data-ttu-id="90470-195">Hello 생성 프로세스가 완료 되 면 hello 시작 보드 toolaunch hello 클러스터 블레이드에서 hello 클러스터에 대 한 hello 타일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-195">Once hello creation process completes, click hello tile for hello cluster from hello Startboard toolaunch hello cluster blade.</span></span> <span data-ttu-id="90470-196">hello 클러스터 블레이드 hello 다음 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-196">hello cluster blade provides hello following information.</span></span>
    
    <span data-ttu-id="90470-197">![클러스터 블레이드](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-completed.png "클러스터 속성")</span><span class="sxs-lookup"><span data-stu-id="90470-197">![Cluster blade](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-completed.png "Cluster properties")</span></span>
    
    <span data-ttu-id="90470-198">이 블레이드의 hello 위쪽 toounderstand hello 아이콘 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-198">Use hello following toounderstand hello icons at hello top of this blade.</span></span>
    
    * <span data-ttu-id="90470-199">**개요** 탭 hello 이름, hello hello 위치, hello 운영 체제 hello 클러스터 대시보드 등에 대 한 URL에 포함 된 리소스 그룹이 같은 hello 클러스터에 대 한 모든 hello 필수 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-199">**Overview** tab provides all hello essential information about hello cluster such as hello name, hello resource group it belongs to, hello location, hello operating system, URL for hello cluster dashboard, etc.</span></span>
    * <span data-ttu-id="90470-200">**대시보드** hello 클러스터와 연결 된 toohello Ambari 포털을 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="90470-200">**Dashboard** directs you toohello Ambari portal associated with hello cluster.</span></span>
    * <span data-ttu-id="90470-201">**Secure Shell**: tooaccess hello 클러스터 SSH를 사용 하는 데 필요한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="90470-201">**Secure Shell**: Information needed tooaccess hello cluster using SSH.</span></span>
    * <span data-ttu-id="90470-202">**크기 조정 클러스터** hello hello 클러스터와 연결 된 작업자 노드 수를 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90470-202">**Scale cluster** lets you increase hello number of worker nodes associated with hello cluster.</span></span>
    * <span data-ttu-id="90470-203">**삭제**: hello HDInsight 클러스터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-203">**Delete**: Deletes hello HDInsight cluster.</span></span>
    

## <a name="customize-clusters"></a><span data-ttu-id="90470-204">클러스터 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="90470-204">Customize clusters</span></span>
* <span data-ttu-id="90470-205">[부트스트랩을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-bootstrap.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90470-205">See [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md).</span></span>
* <span data-ttu-id="90470-206">[스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90470-206">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="90470-207">Hello 클러스터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="90470-207">Delete hello cluster</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="90470-208">문제 해결</span><span class="sxs-lookup"><span data-stu-id="90470-208">Troubleshoot</span></span>

<span data-ttu-id="90470-209">HDInsight 클러스터를 만드는 동안 문제가 발생할 경우 [액세스 제어 요구 사항](hdinsight-administer-use-portal-linux.md#create-clusters)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90470-209">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="90470-210">다음 단계</span><span class="sxs-lookup"><span data-stu-id="90470-210">Next steps</span></span>
<span data-ttu-id="90470-211">HDInsight 클러스터를 성공적으로 만든 toolearn 방법을 따르는 hello를 사용 하 여 클러스터와 toowork:</span><span class="sxs-lookup"><span data-stu-id="90470-211">Now that you have successfully created an HDInsight cluster, use hello following toolearn how toowork with your cluster:</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="90470-212">Hadoop 클러스터</span><span class="sxs-lookup"><span data-stu-id="90470-212">Hadoop clusters</span></span>
* [<span data-ttu-id="90470-213">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="90470-213">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="90470-214">HDInsight에서 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="90470-214">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="90470-215">HDInsight와 함께 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="90470-215">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="90470-216">HBase 클러스터</span><span class="sxs-lookup"><span data-stu-id="90470-216">HBase clusters</span></span>
* [<span data-ttu-id="90470-217">HDInsight에서 HBase 시작</span><span class="sxs-lookup"><span data-stu-id="90470-217">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="90470-218">HDInsight에서 HBase용 Java 응용 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="90470-218">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="90470-219">Storm 클러스터</span><span class="sxs-lookup"><span data-stu-id="90470-219">Storm clusters</span></span>
* [<span data-ttu-id="90470-220">HDInsight에서 Storm용 Java 토폴로지 개발</span><span class="sxs-lookup"><span data-stu-id="90470-220">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="90470-221">HDInsight의 Storm에서 Python 구성 요소 사용</span><span class="sxs-lookup"><span data-stu-id="90470-221">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="90470-222">HDInsight에서 Storm을 사용하는 토폴로지 배포 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="90470-222">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a><span data-ttu-id="90470-223">Spark 클러스터</span><span class="sxs-lookup"><span data-stu-id="90470-223">Spark clusters</span></span>
* [<span data-ttu-id="90470-224">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="90470-224">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="90470-225">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="90470-225">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="90470-226">BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행</span><span class="sxs-lookup"><span data-stu-id="90470-226">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="90470-227">Spark와 기계 학습: HDInsight toopredict 음식 검사 결과에 사용 하 여 Spark</span><span class="sxs-lookup"><span data-stu-id="90470-227">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="90470-228">Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="90470-228">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

