---
title: "웹 브라우저를 사용하여 Hadoop 클러스터 만들기 - Azure HDInsight | Microsoft Docs"
description: "웹 브라우저와 Azure Preview 포털을 사용하여 Linux 기반 HDInsight에서 Hadoop, HBase, Storm 또는 Spark 클러스터를 만드는 방법을 알아봅니다."
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
ms.openlocfilehash: d002e362cda2f0ca991b2a13d41c01c13929cdba
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-the-azure-portal"></a><span data-ttu-id="a333b-103">Azure 포털을 사용하여 HDInsight에서 Linux 기반 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="a333b-103">Create Linux-based clusters in HDInsight using the Azure portal</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="a333b-104">Azure 포털은 Microsoft Azure 클라우드에 호스트된 서비스와 리소스에 대한 웹 기반 관리 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-104">The Azure portal is a web-based management tool for services and resources hosted in the Microsoft Azure cloud.</span></span> <span data-ttu-id="a333b-105">이 문서에서는 포털을 사용하여 Linux 기반 HDInsight 클러스터를 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-105">In this article you will learn how to create Linux-based HDInsight clusters using the portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a333b-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a333b-106">Prerequisites</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="a333b-107">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="a333b-107">**An Azure subscription**.</span></span> <span data-ttu-id="a333b-108">[Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a333b-108">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="a333b-109">**최신 웹 브라우저**.</span><span class="sxs-lookup"><span data-stu-id="a333b-109">**A modern web browser**.</span></span> <span data-ttu-id="a333b-110">Azure 포털은 HTML5 및 Javascript를 사용하며 이전 웹 브라우저에서 제대로 작동하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-110">The Azure  portal uses HTML5 and Javascript, and may not function correctly in older web browsers.</span></span>

## <a name="create-clusters"></a><span data-ttu-id="a333b-111">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="a333b-111">Create clusters</span></span>
<span data-ttu-id="a333b-112">Azure 포털은 대부분의 클러스터 속성을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-112">The Azure portal exposes most of the cluster properties.</span></span> <span data-ttu-id="a333b-113">Azure Resource Manager 템플릿을 사용하여 이러한 많은 속성을 숨길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-113">Using Azure Resource Manager template, you can hide a lot of details.</span></span> <span data-ttu-id="a333b-114">자세한 내용은 [Azure Resource Manager 템플릿을 사용하여 HDInsight의 Linux 기반 Hadoop 클러스터 만들기](hdinsight-hadoop-create-linux-clusters-arm-templates.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a333b-114">For more information, see [Create Linux-based Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md).</span></span>

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


1. <span data-ttu-id="a333b-115">[Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-115">Sign in to the [Azure  portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a333b-116">**+**, **인텔리전스 + 분석** 및 **HDInsight**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-116">Click **+**, click **Intelligence + Analytics**, and then click **HDInsight**.</span></span>
   
    <span data-ttu-id="a333b-117">![Azure Portal에서 새 클러스터 만들기](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster.png "Azure Portal에서 새 클러스터 만들기")</span><span class="sxs-lookup"><span data-stu-id="a333b-117">![Creating a new cluster in the Azure portal](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster.png "Creating a new cluster in the Azure portal")</span></span>

3. <span data-ttu-id="a333b-118">**HDInsight** 블레이드에서 **(크기, 설정, 응용 프로그램) 사용자 지정**을 클릭한 다음 **기본 사항**을 클릭하고 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-118">In the **HDInsight** blade, click **Custom (size, settings, apps)**, click **Basics**, and then enter the following information.</span></span>

    <span data-ttu-id="a333b-119">![Azure Portal에서 새 클러스터 만들기](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-basics.png "Azure Portal에서 새 클러스터 만들기")</span><span class="sxs-lookup"><span data-stu-id="a333b-119">![Creating a new cluster in the Azure portal](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-basics.png "Creating a new cluster in the Azure portal")</span></span>

    * <span data-ttu-id="a333b-120">**클러스터 이름**입력: 이 이름은 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-120">Enter **Cluster Name**: This name must be globally unique.</span></span>

    * <span data-ttu-id="a333b-121">**구독** 드롭다운에서 클러스터에 사용할 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-121">From the **Subscription** drop-down, select the Azure subscription that will be used for the cluster.</span></span>

    * <span data-ttu-id="a333b-122">**클러스터 유형**을 클릭한 후 다음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-122">Click **Cluster type**, and then select:</span></span>
   
        * <span data-ttu-id="a333b-123">**클러스터 유형**: 어떤 유형을 선택할지 잘 모르는 경우 **Hadoop**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-123">**Cluster Type**: If you don't know what to choose, select **Hadoop**.</span></span> <span data-ttu-id="a333b-124">가장 인기 있는 클러스터 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-124">It is the most popular cluster type.</span></span>
     
            > [!IMPORTANT]
            > <span data-ttu-id="a333b-125">HDInsight 클러스터는 작업 부하 또는 클러스터에 대한 튜닝 기술에 해당하는 다양한 형식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-125">HDInsight clusters come in a variety of types, which correspond to the workload or technology that the cluster is tuned for.</span></span> <span data-ttu-id="a333b-126">하나의 클러스터에서 Storm 및 HBase 등의 여러 유형을 결합하는 클러스터를 만들기 위해 지원되는 메서드가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-126">There is no supported method to create a cluster that combines multiple types, such as Storm and HBase on one cluster.</span></span> 
            > 
            > 
        
        * <span data-ttu-id="a333b-127">**운영 체제**: **Linux**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-127">**Operating System**: Select **Linux**.</span></span>
        
        * <span data-ttu-id="a333b-128">**버전**: 어떤 버전을 선택할지 잘 모르는 경우 기본 버전을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-128">**Version**: Use the default version if you don't know what to choose.</span></span> <span data-ttu-id="a333b-129">자세한 내용은 [HDInsight 클러스터 버전](hdinsight-component-versioning.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a333b-129">For more information, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>
        * <span data-ttu-id="a333b-130">**클러스터 계층**: Azure HDInsight는 빅 데이터 클라우드 제품을 표준 계층 및 프리미엄 계층의 두 범주로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-130">**Cluster Tier**: Azure HDInsight provides the big data cloud offerings in two categories: Standard tier and Premium tier.</span></span> <span data-ttu-id="a333b-131">자세한 내용은 [클러스터 계층](hdinsight-hadoop-provision-linux-clusters.md#cluster-tiers)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a333b-131">For more information, see [Cluster tiers](hdinsight-hadoop-provision-linux-clusters.md#cluster-tiers).</span></span>

    * <span data-ttu-id="a333b-132">**클러스터 로그인 사용자 이름** 및 **클러스터 로그인 암호**에 관리 사용자의 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-132">For **Cluster login username** and **Cluster login password**, provide the username and password for the admin user.</span></span>

    * <span data-ttu-id="a333b-133">**SSH 사용자 이름**을 입력하고 SSH 암호를 이전에 지정한 관리자 암호와 동일하게 하려면 **클러스터 로그인과 동일한 암호 사용** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-133">Enter an **SSH Username** and if you want to have the SSH password same as the admin password you specified earlier, select the **Use same password as cluster login** check box.</span></span> <span data-ttu-id="a333b-134">그렇지 않으면 **암호** 또는 **공개 키**를 제공합니다. 이 항목은 SSH 사용자를 인증하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-134">If not, provide either a **PASSWORD** or **PUBLIC KEY**, which will be used to authenticate the SSH user.</span></span> <span data-ttu-id="a333b-135">공개 키를 사용하는 것이 권장 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-135">Using a public key is the recommended approach.</span></span> <span data-ttu-id="a333b-136">아래쪽의 **선택** 을 클릭하여 자격 증명 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-136">Click **Select** at the bottom to save the credentials configuration.</span></span>
   
        <span data-ttu-id="a333b-137">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a333b-137">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

    * <span data-ttu-id="a333b-138">**리소스 그룹**에서 새 리소스 그룹을 만들지 아니면 기존 집합을 사용할지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-138">For **Resource group**, specify whether you want to create a new resource group or use an existing one.</span></span>

    * <span data-ttu-id="a333b-139">클러스터를 만들 데이터 센터 **위치**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-139">Specify a data center **location** where the cluster will be created.</span></span>

    * <span data-ttu-id="a333b-140">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-140">Click **Next**.</span></span>

4. <span data-ttu-id="a333b-141">**저장소** 블레이드에서 Azure Storage(WASB) 또는 Data Lake Store를 기본 저장소로 사용할지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-141">On the **Storage** blade, specify whether you want Azure Storage (WASB) or Data Lake Store as your default storage.</span></span> <span data-ttu-id="a333b-142">자세한 내용은 아래 테이블을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="a333b-142">Look at the table below for more information.</span></span>

    <span data-ttu-id="a333b-143">![Azure Portal에서 새 클러스터 만들기](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-storage.png "Azure Portal에서 새 클러스터 만들기")</span><span class="sxs-lookup"><span data-stu-id="a333b-143">![Creating a new cluster in the Azure portal](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-storage.png "Creating a new cluster in the Azure portal")</span></span>

    | <span data-ttu-id="a333b-144">저장소</span><span class="sxs-lookup"><span data-stu-id="a333b-144">Storage</span></span>                                      | <span data-ttu-id="a333b-145">설명</span><span class="sxs-lookup"><span data-stu-id="a333b-145">Description</span></span> |
    |----------------------------------------------|-------------|
    | <span data-ttu-id="a333b-146">**기본 저장소인 Azure Storage Blob**</span><span class="sxs-lookup"><span data-stu-id="a333b-146">**Azure Storage Blobs as default storage**</span></span>   | <ul><li><span data-ttu-id="a333b-147">**기본 저장소 형식**으로 **Azure Storage**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-147">For **Primary Storage type**, select **Azure Storage**.</span></span> <span data-ttu-id="a333b-148">그런 다음 Azure 구독의 일부인 저장소 계정을 지정하고 저장소 계정을 선택하려는 경우 **선택 방법**에서 **내 구독**을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-148">After that, for **Selection method**, you can choose **My subscriptions** if you want to specify a storage account that is part of your Azure subscription and then select the storage account.</span></span> <span data-ttu-id="a333b-149">그렇지 않으면 **선택키**를 클릭하고 Azure 구독 외부에서 선택하려는 저장소 계정에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-149">Otherwise, click **Access key** and provide the information for the storage account that you want to choose from outside your Azure subscription.</span></span></li><li><span data-ttu-id="a333b-150">**기본 컨테이너**의 경우 포털에서 제안한 기본 컨테이너 이름을 사용하거나 고유한 이름을 지정하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-150">For **Default container**, you can choose to go with the default container name suggested by the portal or specify your own.</span></span></li><li><span data-ttu-id="a333b-151">WASB를 기본 저장소를 사용하는 경우 선택적으로 **추가 저장소 계정**을 클릭하여 클러스터와 연결할 추가 저장소 계정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-151">If you are using WASB as default storage, you can (optionally) click **Additional Storage Accounts** to specify additional storage accounts to associate with the cluster.</span></span> <span data-ttu-id="a333b-152">**Azure Storage 키** 블레이드에서 **저장소 키 추가**를 클릭한 다음 Azure 구독 또는 다른 구독에서 저장소 계정 선택키를 제공하여 저장소 계정을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-152">In the **Azure Storage Keys** blade, click **Add a storage key**, and then you can provide a storage account from your Azure subscriptions or from other subscriptions (by providing the storage account access key).</span></span></li><li><span data-ttu-id="a333b-153">WASB를 기본 저장소로 사용하는 경우 선택적으로 **Data Lake Store 액세스**를 클릭하여 Azure Data Lake Store를 추가 저장소로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-153">If you are using WASB as default storage, you can (optionally) click **Data Lake Store access** to specify Azure Data Lake Store as additional storage.</span></span> <span data-ttu-id="a333b-154">자세한 내용은 [Azure Portal을 사용하여 Data Lake Store로 HDInsight 클러스터 만들기](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a333b-154">For more information, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span></li></ul> |
    | <span data-ttu-id="a333b-155">**기본 저장소로 Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="a333b-155">**Azure Data Lake Store as default storage**</span></span> | <span data-ttu-id="a333b-156">**기본 저장소 유형**에서 **데이터 레이크 저장소**를 선택하고 지침은 [Azure Portal을 사용하여 Data Lake Store로 HDInsight 클러스터 만들기](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md) 문서를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-156">For **Primary storage type**, select **Data Lake Store** and then refer to the article [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md) for instructions.</span></span> |
    | <span data-ttu-id="a333b-157">**외부 Metastore**</span><span class="sxs-lookup"><span data-stu-id="a333b-157">**External metastores**</span></span>                      | <span data-ttu-id="a333b-158">필요에 따라 SQL Database를 지정하여 클러스터와 연결된 Hive 및 Oozie 메타데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-158">Optionally, you can specify a SQL database to save Hive and Oozie metadata associated with the cluster.</span></span> <span data-ttu-id="a333b-159">**Hive용 SQL Database 사용**에 대해 SQL Database를 클릭하고 데이터베이스의 사용자 이름/암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-159">For **Select a SQL database for Hive** select a SQL database, and then provide the username/password for the database.</span></span> <span data-ttu-id="a333b-160">Oozie 메타데이터에 대해 이러한 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-160">Repeat these steps for Oozie metadata.</span></span><br><br><span data-ttu-id="a333b-161">metastores에 대한 Azure SQL Database를 사용하는 동안 몇 가지 고려 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-161">Some considerations while using Azure SQL database for metastores.</span></span> <ul><li><span data-ttu-id="a333b-162">메타스토어에 사용되는 Azure SQL 데이터베이스는 Azure HDInsight를 비롯한 다른 Azure 서비스로의 연결을 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-162">The Azure SQL database used for the metastore must allow connectivity to other Azure services, including Azure HDInsight.</span></span> <span data-ttu-id="a333b-163">Azure SQL 데이터베이스 대시보드의 오른쪽에서 서버 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-163">On the Azure SQL database dashboard, on the right side, click the server name.</span></span> <span data-ttu-id="a333b-164">이 서버는 SQL 데이터베이스 인스턴스가 실행되는 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-164">This is the server on which the SQL database instance is running.</span></span> <span data-ttu-id="a333b-165">서버 보기에서 **구성**을 클릭하고 **Azure 서비스**에 대해 **예**를 클릭한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-165">Once you are on the server view, click **Configure**, and then for **Azure Services**, click **Yes**, and then click **Save**.</span></span></li><li><span data-ttu-id="a333b-166">Metastore를 만들 때 클러스터를 만드는 프로세스가 실패할 수 있으므로 대시 또는 하이픈을 포함하는 데이터베이스 이름을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-166">When creating a metastore, do not use a database name that contains dashes or hyphens, as this can cause the cluster creation process to fail.</span></span></li></ul>                                                                                                                                                                       |

    <span data-ttu-id="a333b-167">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-167">Click **Next**.</span></span> 

    > [!WARNING]
    > <span data-ttu-id="a333b-168">HDInsight 클러스터와 다른 위치에서는 추가 저장소 계정을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-168">Using an additional storage account in a different location than the HDInsight cluster is not supported.</span></span>

5. <span data-ttu-id="a333b-169">필요에 따라 **응용 프로그램**을 클릭하여 HDInsight 클러스터에 작동하는 응용 프로그램을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-169">Optionally, click **Applications** to install applications that work with HDInsight clusters.</span></span> <span data-ttu-id="a333b-170">Microsoft, ISV(독립 소프트웨어 공급 업체) 또는 사용자가 직접 이러한 응용 프로그램을 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-170">These applications can be developed by Microsoft, independent software vendors (ISV) or by yourself.</span></span> <span data-ttu-id="a333b-171">자세한 내용은 [HDInsight 응용 프로그램 설치](hdinsight-apps-install-applications.md#install-applications-during-cluster-creation)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a333b-171">For more information, see [Install HDInsight applications](hdinsight-apps-install-applications.md#install-applications-during-cluster-creation).</span></span>


6. <span data-ttu-id="a333b-172">**클러스터 크기**를 클릭하여 이 클러스터에 대해 만들어질 노드에 대한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-172">Click **Cluster size** to display information about the nodes that will be created for this cluster.</span></span> <span data-ttu-id="a333b-173">클러스터에 필요한 작업자 노드 수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-173">Set the number of worker nodes that you need for the cluster.</span></span> <span data-ttu-id="a333b-174">클러스터의 예상 비용이 블레이드 내에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-174">The estimated cost of the cluster will be shown within the blade.</span></span>
   
    <span data-ttu-id="a333b-175">![노드 가격 책정 계층 블레이드](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-nodes.png "클러스터 노드 수 지정")</span><span class="sxs-lookup"><span data-stu-id="a333b-175">![Node pricing tiers blade](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-nodes.png "Specify number of cluster nodes")</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="a333b-176">클러스터 만들기에서 또는 클러스터를 만든 후 확장하여 32개 이상의 작업자 노드를 계획하는 경우 최소한 코어 8개와 14GB RAM을 가진 헤드 노드 크기를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-176">If you plan on more than 32 worker nodes, either at cluster creation or by scaling the cluster after creation, then you must select a head node size with at least 8 cores and 14GB ram.</span></span>
   > 
   > <span data-ttu-id="a333b-177">노드 크기 및 관련된 비용에 대한 자세한 내용은 [HDInsight 가격 책정](https://azure.microsoft.com/pricing/details/hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a333b-177">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>
   > 
   > 
   
   <span data-ttu-id="a333b-178">**다음**을 클릭하여 노드 가격 책정 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-178">Click **Next** to save the node pricing configuration.</span></span>

7. <span data-ttu-id="a333b-179">**고급 설정**을 클릭하여 **스크립트 작업**을 사용하는 등 다른 선택적 설정을 구성하고 **가상 네트워크**에 조인하여 사용자 지정 구성 요소를 설치하도록 클러스터를 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-179">Click **Advanced settings** to configure other optional settings such as using **Script Actions** to customize a cluster to install custom components or joining a **Virtual Network**.</span></span> <span data-ttu-id="a333b-180">자세한 내용은 아래 테이블을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="a333b-180">Look at the table below for more information.</span></span>

    <span data-ttu-id="a333b-181">![노드 가격 책정 계층 블레이드](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-advanced.png "클러스터 노드 수 지정")</span><span class="sxs-lookup"><span data-stu-id="a333b-181">![Node pricing tiers blade](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-advanced.png "Specify number of cluster nodes")</span></span>

    | <span data-ttu-id="a333b-182">옵션</span><span class="sxs-lookup"><span data-stu-id="a333b-182">Option</span></span> | <span data-ttu-id="a333b-183">설명</span><span class="sxs-lookup"><span data-stu-id="a333b-183">Description</span></span> |
    |--------|-------------|
    | <span data-ttu-id="a333b-184">**스크립트 작업**</span><span class="sxs-lookup"><span data-stu-id="a333b-184">**Script Actions**</span></span> | <span data-ttu-id="a333b-185">클러스터를 만들 때 사용자 지정 스크립트를 사용하여 클러스터를 사용자 지정하려는 경우에 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-185">Use this option if you want to use a custom script to customize a cluster, as the cluster is being created.</span></span> <span data-ttu-id="a333b-186">스크립트 동작에 대한 자세한 내용은 [스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a333b-186">For more information about script actions, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span> |
    | <span data-ttu-id="a333b-187">**Virtual Network**</span><span class="sxs-lookup"><span data-stu-id="a333b-187">**Virtual Network**</span></span> | <span data-ttu-id="a333b-188">클러스터를 가상 네트워크에 배치하려는 경우 Azure Virtual Network 및 서브넷을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-188">Select an Azure virtual network and the subnet if you want to place the cluster into a virtual network.</span></span> <span data-ttu-id="a333b-189">가상 네트워크에 대한 특정 구성 요구 사항을 포함하여 가상 네트워크로 HDInsight를 사용하는 방법에 대한 자세한 내용은 [Azure 가상 네트워크를 사용하여 HDInsight 기능 확장](hdinsight-extend-hadoop-virtual-network.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a333b-189">For information on using HDInsight with a Virtual Network, including specific configuration requirements for the Virtual Network, see [Extend HDInsight capabilities by using an Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span></span> |

    <span data-ttu-id="a333b-190">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-190">Click **Next**.</span></span>

8. <span data-ttu-id="a333b-191">**요약** 블레이드에서 이전에 입력한 정보를 확인한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-191">On the **Summary** blade, verify the information you entered earlier and then click **Create**.</span></span>

    <span data-ttu-id="a333b-192">![노드 가격 책정 계층 블레이드](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-summary.png "클러스터 노드 수 지정")</span><span class="sxs-lookup"><span data-stu-id="a333b-192">![Node pricing tiers blade](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-summary.png "Specify number of cluster nodes")</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="a333b-193">클러스터를 만드는데 약간의 시간이 걸리며, 일반적으로 약 15분이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-193">It will take some time for the cluster to be created, usually around 15 minutes.</span></span> <span data-ttu-id="a333b-194">시작 보드에 있는 타일 또는 페이지 왼쪽에 있는 **알림** 항목을 사용하여 프로비전 프로세스를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="a333b-194">Use the tile on the Startboard, or the **Notifications** entry on the left of the page to check on the provisioning process.</span></span>
    > 
    > 
12. <span data-ttu-id="a333b-195">생성 프로세스가 완료되면 시작 보드에서 클러스터 타일을 클릭하여 클러스터 블레이드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-195">Once the creation process completes, click the tile for the cluster from the Startboard to launch the cluster blade.</span></span> <span data-ttu-id="a333b-196">클러스터 블레이드에서는 다음 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-196">The cluster blade provides the following information.</span></span>
    
    <span data-ttu-id="a333b-197">![클러스터 블레이드](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-completed.png "클러스터 속성")</span><span class="sxs-lookup"><span data-stu-id="a333b-197">![Cluster blade](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-completed.png "Cluster properties")</span></span>
    
    <span data-ttu-id="a333b-198">다음을 사용하여 이 블레이드의 위쪽에 있는 아이콘을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-198">Use the following to understand the icons at the top of this blade.</span></span>
    
    * <span data-ttu-id="a333b-199">**개요** 탭은 이름, 속한 리소스 그룹, 위치, 운영 체제, 클러스터 대시보드의 URL 등 클러스터에 대한 모든 필수 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-199">**Overview** tab provides all the essential information about the cluster such as the name, the resource group it belongs to, the location, the operating system, URL for the cluster dashboard, etc.</span></span>
    * <span data-ttu-id="a333b-200">**대시보드**는 사용자를 클러스터와 연결된 Ambari 포털로 다이렉트합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-200">**Dashboard** directs you to the Ambari portal associated with the cluster.</span></span>
    * <span data-ttu-id="a333b-201">**보안 셸**: SSH를 사용하여 클러스터에 액세스하는 데 필요한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-201">**Secure Shell**: Information needed to access the cluster using SSH.</span></span>
    * <span data-ttu-id="a333b-202">**클러스터 크기 조정**을 통해 클러스터와 연결된 작업자 노드 수를 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-202">**Scale cluster** lets you increase the number of worker nodes associated with the cluster.</span></span>
    * <span data-ttu-id="a333b-203">**삭제**: HDInsight 클러스터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-203">**Delete**: Deletes the HDInsight cluster.</span></span>
    

## <a name="customize-clusters"></a><span data-ttu-id="a333b-204">클러스터 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="a333b-204">Customize clusters</span></span>
* <span data-ttu-id="a333b-205">[부트스트랩을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-bootstrap.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a333b-205">See [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md).</span></span>
* <span data-ttu-id="a333b-206">[스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a333b-206">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="a333b-207">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="a333b-207">Delete the cluster</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="a333b-208">문제 해결</span><span class="sxs-lookup"><span data-stu-id="a333b-208">Troubleshoot</span></span>

<span data-ttu-id="a333b-209">HDInsight 클러스터를 만드는 동안 문제가 발생할 경우 [액세스 제어 요구 사항](hdinsight-administer-use-portal-linux.md#create-clusters)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a333b-209">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a333b-210">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a333b-210">Next steps</span></span>
<span data-ttu-id="a333b-211">HDInsight 클러스터를 성공적으로 만들었으므로 다음을 사용하여 클러스터 작업을 수행하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a333b-211">Now that you have successfully created an HDInsight cluster, use the following to learn how to work with your cluster:</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="a333b-212">Hadoop 클러스터</span><span class="sxs-lookup"><span data-stu-id="a333b-212">Hadoop clusters</span></span>
* [<span data-ttu-id="a333b-213">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="a333b-213">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="a333b-214">HDInsight에서 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="a333b-214">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="a333b-215">HDInsight와 함께 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="a333b-215">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="a333b-216">HBase 클러스터</span><span class="sxs-lookup"><span data-stu-id="a333b-216">HBase clusters</span></span>
* [<span data-ttu-id="a333b-217">HDInsight에서 HBase 시작</span><span class="sxs-lookup"><span data-stu-id="a333b-217">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="a333b-218">HDInsight에서 HBase용 Java 응용 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="a333b-218">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="a333b-219">Storm 클러스터</span><span class="sxs-lookup"><span data-stu-id="a333b-219">Storm clusters</span></span>
* [<span data-ttu-id="a333b-220">HDInsight에서 Storm용 Java 토폴로지 개발</span><span class="sxs-lookup"><span data-stu-id="a333b-220">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="a333b-221">HDInsight의 Storm에서 Python 구성 요소 사용</span><span class="sxs-lookup"><span data-stu-id="a333b-221">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="a333b-222">HDInsight에서 Storm을 사용하는 토폴로지 배포 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="a333b-222">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a><span data-ttu-id="a333b-223">Spark 클러스터</span><span class="sxs-lookup"><span data-stu-id="a333b-223">Spark clusters</span></span>
* [<span data-ttu-id="a333b-224">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="a333b-224">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="a333b-225">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="a333b-225">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="a333b-226">BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행</span><span class="sxs-lookup"><span data-stu-id="a333b-226">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="a333b-227">기계 학습과 Spark: 음식 검사 결과를 예측하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="a333b-227">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="a333b-228">Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="a333b-228">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

