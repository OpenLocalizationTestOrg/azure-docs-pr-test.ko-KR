---
title: "Azure Portal을 사용하여 Windows 기반 HDInsight의 Hadoop 클러스터 관리 | Microsoft Docs"
description: "HDInsight 서비스를 관리하는 방법에 대해 알아봅니다. HDInsight 클러스터를 만들고 대화형 JavaScript 콘솔을 열고 Hadoop 명령 콘솔을 여는 방법에 대해 설명합니다."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 9295a988-bd88-453a-8c8b-55fa103bf39c
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: f69fa4f838b22ccbb25186c08cac9744bb31c6d1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-windows-based-hadoop-clusters-in-hdinsight-by-using-the-azure-portal"></a><span data-ttu-id="b6f2d-104">Azure Portal을 사용하여 HDInsight의 Windows 기반 Hadoop 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="b6f2d-104">Manage Windows-based Hadoop clusters in HDInsight by using the Azure portal</span></span>

<span data-ttu-id="b6f2d-105">[Azure Portal][azure-portal]에서 Azure HDInsight의 Windows 기반 Hadoop 클러스터를 만들고, Hadoop 사용자의 암호를 변경하고, RDP (원격 데스크톱 프로토콜)를 사용하도록 설정하여 클러스터의 Hadoop 명령 콘솔에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-105">Using the [Azure portal][azure-portal], you can create Windows-based Hadoop clusters in Azure HDInsight, change Hadoop user password, and enable Remote Desktop Protocol (RDP) so you can access the Hadoop command console on the cluster.</span></span>

<span data-ttu-id="b6f2d-106">이 문서의 정보는 Windows 기반 HDInsight 클러스터에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-106">The information in this article only applies to Window-based HDInsight clusters.</span></span> <span data-ttu-id="b6f2d-107">Linux 기반 클러스터 관리에 대한 자세한 내용은 [Azure Portal을 사용하여 HDInsight의 Hadoop 클러스터 관리](hdinsight-administer-use-portal-linux.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-107">For information on managing Linux-based clusters, see [Manage Hadoop clusters in HDInsight by using the Azure portal](hdinsight-administer-use-portal-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b6f2d-108">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b6f2d-109">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="b6f2d-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b6f2d-110">Prerequisites</span></span>

<span data-ttu-id="b6f2d-111">이 문서를 시작하기 전에 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-111">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="b6f2d-112">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-112">**An Azure subscription**.</span></span> <span data-ttu-id="b6f2d-113">[Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-113">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="b6f2d-114">**Azure 저장소 계정** - HDInsight 클러스터는 Azure Blob 저장소 컨테이너를 기본 파일 시스템으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-114">**Azure Storage account** - An HDInsight cluster uses an Azure Blob storage container as the default file system.</span></span> <span data-ttu-id="b6f2d-115">Azure Blob 저장소가 HDInsight 클러스터에서 매끄럽게 작동하는 방식에 대한 자세한 내용은 [HDInsight에서 Azure Blob 저장소 사용](hdinsight-hadoop-use-blob-storage.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-115">For more information about how Azure Blob storage provides a seamless experience with HDInsight clusters, see [Use Azure Blob Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="b6f2d-116">Azure 저장소 계정 만들기에 대한 자세한 내용은 [저장소 계정을 만드는 방법](../storage/common/storage-create-storage-account.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-116">For details on creating an Azure Storage account, see [How to Create a Storage Account](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="open-the-portal"></a><span data-ttu-id="b6f2d-117">포털 열기</span><span class="sxs-lookup"><span data-stu-id="b6f2d-117">Open the Portal</span></span>
1. <span data-ttu-id="b6f2d-118">[https://portal.azure.com](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-118">Sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b6f2d-119">포털을 연 후 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-119">After you open the portal, you can:</span></span>

   * <span data-ttu-id="b6f2d-120">왼쪽 메뉴에서 **새로 만들기** 를 클릭하여 새 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-120">Click **New** from the left menu to create a new cluster:</span></span>

       ![새 HDInsight 클러스터 단추](./media/hdinsight-administer-use-management-portal/azure-portal-new-button.png)
   * <span data-ttu-id="b6f2d-122">왼쪽 메뉴에서 **HDInsight 클러스터** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-122">Click **HDInsight Clusters** from the left menu.</span></span>

       ![Azure 포털 HDInsight 클러스터 단추](./media/hdinsight-administer-use-management-portal/azure-portal-hdinsight-button.png)

     <span data-ttu-id="b6f2d-124">왼쪽 메뉴에 **HDInsight**가 표시되지 않으면 **찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-124">If **HDInsight** doesn't appear in the left menu, click **Browse**.</span></span>

     ![Azure Portal 찾아보기 클러스터 단추](./media/hdinsight-administer-use-management-portal/azure-portal-browse-button.png)

## <a name="create-clusters"></a><span data-ttu-id="b6f2d-126">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="b6f2d-126">Create clusters</span></span>
<span data-ttu-id="b6f2d-127">포털을 사용하여 만드는 지침은 [HDInsight 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-127">For the creation instructions using the Portal, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="b6f2d-128">HDInsight는 다양한 Hadoop 구성 요소에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-128">HDInsight works with a wide range of Hadoop components.</span></span> <span data-ttu-id="b6f2d-129">검증되어 지원되는 구성 요소 목록은 [Azure HDInsight에 포함된 Hadoop 버전](hdinsight-component-versioning.md)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-129">For the list of the components that have been verified and supported, see [What version of Hadoop is in Azure HDInsight](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="b6f2d-130">다음 옵션 중 하나를 사용하여 HDInsight를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-130">You can customize HDInsight by using one of the following options:</span></span>

* <span data-ttu-id="b6f2d-131">스크립트 작업을 사용하여 클러스터 구성을 변경하거나 Giraph 또는 Solr과 같은 사용자 지정 구성 요소를 설치하도록 클러스터를 사용자 지정할 수 있는 사용자 지정 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-131">Use Script Action to run custom scripts that can customize a cluster to either change cluster configuration or install custom components such as Giraph or Solr.</span></span> <span data-ttu-id="b6f2d-132">자세한 내용은 [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster.md)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-132">For more information, see [Customize HDInsight cluster using Script Action](hdinsight-hadoop-customize-cluster.md).</span></span>
* <span data-ttu-id="b6f2d-133">클러스터를 만드는 동안 HDInsight .NET SDK 또는 Azure PowerShell의 클러스터 사용자 지정 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-133">Use the cluster customization parameters in the HDInsight .NET SDK or Azure PowerShell during cluster creation.</span></span> <span data-ttu-id="b6f2d-134">그러면 이러한 구성 변경 내용이 클러스터 수명 동안 유지되며 Azure 플랫폼이 유지 관리를 위해 정기적으로 수행하는 클러스터 노드 이미지로 다시 설치의 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-134">These configuration changes are then preserved through the lifetime of the cluster and are not affected by cluster node reimages that Azure platform periodically performs for maintenance.</span></span> <span data-ttu-id="b6f2d-135">클러스터 사용자 지정 매개 변수 사용에 대한 자세한 내용은 [HDInsight 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-135">For more information on using the cluster customization parameters, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="b6f2d-136">Mahout, Cascading 등의 일부 네이티브 Java 구성 요소는 클러스터에서 JAR 파일로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-136">Some native Java components, like Mahout and Cascading, can be run on the cluster as JAR files.</span></span> <span data-ttu-id="b6f2d-137">이러한 JAR 파일은 Azure Blob 저장소에 배포되고 Hadoop 작업 제출 메커니즘을 통해 HDInsight 클러스터에 제출될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-137">These JAR files can be distributed to Azure Blob storage, and submitted to HDInsight clusters through Hadoop job submission mechanisms.</span></span> <span data-ttu-id="b6f2d-138">자세한 내용은 [프로그래밍 방식으로 Hadoop 작업 제출](hdinsight-submit-hadoop-jobs-programmatically.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-138">For more information, see [Submit Hadoop jobs programmatically](hdinsight-submit-hadoop-jobs-programmatically.md).</span></span>

  > [!NOTE]
  > <span data-ttu-id="b6f2d-139">HDInsight 클러스터에 Jar 파일을 배포하거나 HDInsight 클러스터에서 Jar 파일을 호출하는 데 문제가 있는 경우 [Microsoft 지원 센터](https://azure.microsoft.com/support/options/)로 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-139">If you have issues deploying JAR files to HDInsight clusters or calling JAR files on HDInsight clusters, contact [Microsoft Support](https://azure.microsoft.com/support/options/).</span></span>
  >
  > <span data-ttu-id="b6f2d-140">Cascading은 HDInsight에서 지원되지 않으며 Microsoft 지원 대상이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-140">Cascading is not supported by HDInsight, and is not eligible for Microsoft Support.</span></span> <span data-ttu-id="b6f2d-141">지원되는 구성 요소 목록은 [HDInsight에서 제공하는 클러스터 버전의 새로운 기능](hdinsight-component-versioning.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-141">For lists of supported components, see [What's new in the cluster versions provided by HDInsight](hdinsight-component-versioning.md).</span></span>
  >
  >

<span data-ttu-id="b6f2d-142">원격 데스크톱 연결을 사용하여 클러스터에 사용자 지정 소프트웨어를 설치하는 기능은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-142">Installation of custom software on the cluster by using Remote Desktop Connection is not supported.</span></span> <span data-ttu-id="b6f2d-143">헤드 노드의 드라이브에는 파일을 저장하면 안 됩니다. 클러스터를 다시 만들어야 하는 경우 파일이 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-143">You should avoid storing any files on the drives of the head node, as they will be lost if you need to re-create the clusters.</span></span> <span data-ttu-id="b6f2d-144">Azure Blob 저장소에 파일을 저장하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-144">We recommend storing files on Azure Blob storage.</span></span> <span data-ttu-id="b6f2d-145">Blob 저장소는 영구적입니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-145">Blob storage is persistent.</span></span>

## <a name="list-and-show-clusters"></a><span data-ttu-id="b6f2d-146">클러스터 나열 및 표시</span><span class="sxs-lookup"><span data-stu-id="b6f2d-146">List and show clusters</span></span>
1. <span data-ttu-id="b6f2d-147">[https://portal.azure.com](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-147">Sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b6f2d-148">왼쪽 메뉴에서 **HDInsight 클러스터** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-148">Click **HDInsight Clusters** from the left menu.</span></span>
3. <span data-ttu-id="b6f2d-149">클러스터 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-149">Click the cluster name.</span></span> <span data-ttu-id="b6f2d-150">클러스터 목록이 긴 경우 페이지 상단의 필터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-150">If the cluster list is long, you can use filter on the top of the page.</span></span>
4. <span data-ttu-id="b6f2d-151">목록에서 클러스터를 두 번 클릭하여 세부 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-151">Double-click a cluster from the list to show the details.</span></span>

    <span data-ttu-id="b6f2d-152">**메뉴 및 요점**:</span><span class="sxs-lookup"><span data-stu-id="b6f2d-152">**Menu and essentials**:</span></span>

    ![Azure Portal HDInsight 클러스터 요점](./media/hdinsight-administer-use-management-portal/hdinsight-essentials.png)

   * <span data-ttu-id="b6f2d-154">메뉴를 사용자 지정하려면 메뉴의 아무 곳이나 마우스 오른쪽 단추로 클릭한 후 **사용자 지정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-154">To customize the menu, right-click anywhere on the menu, and then click **Customize**.</span></span>
   * <span data-ttu-id="b6f2d-155">**설정** 및 **모든 설정**: 클러스터의 **설정** 블레이드를 표시하여 자세한 구성 정보에 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-155">**Settings** and **All Settings**: Displays the **Settings** blade for the cluster, which allows you to access detailed configuration information for the cluster.</span></span>
   * <span data-ttu-id="b6f2d-156">**대시보드**, **클러스터 대시보드** 및 **URL: 이러한 항목을 통해 Linux 기반 클러스터용 Ambari 웹인 클러스터 대시보드에 액세스할 수 있습니다. -**보안 셸**: SSH(보안 셸) 연결을 사용하여 클러스터에 연결하는 지침을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-156">**Dashboard**, **Cluster Dashboard** and **URL: These are all ways to access the cluster dashboard, which is Ambari Web for Linux-based clusters. -**Secure Shell**: Shows the instructions to connect to the cluster using Secure Shell (SSH) connection.</span></span>
   * <span data-ttu-id="b6f2d-157">**클러스터 크기 조정**: 이 클러스터의 작업자 노드 수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-157">**Scale Cluster**: Allows you to change the number of worker nodes for this cluster.</span></span>
   * <span data-ttu-id="b6f2d-158">**삭제**: 클러스터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-158">**Delete**: Deletes the cluster.</span></span>
   * <span data-ttu-id="b6f2d-159">**빠른 시작**: HDInsight를 사용하여 시작하는 데 도움이 되는 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-159">**Quickstart**: Displays information that will help you get started using HDInsight.</span></span>
   * <span data-ttu-id="b6f2d-160">**사용자: Azure 구독의 다른 사용자를 위해 이 클러스터의 *포털 관리* 권한을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-160">**Users: Allows you to set permissions for *portal management* of this cluster for other users on your Azure subscription.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="b6f2d-161">이는 *오직* Azure 포털에서 이 클러스터에 대한 액세스 및 권한에만 영향을 미치며, HDInsight 클러스터에 연결하거나 작업을 제출할 수 있는 사용자에게는 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-161">This *only* affects access and permissions to this cluster in the Azure portal, and has no effect on who can connect to or submit jobs to the HDInsight cluster.</span></span>
     >
     >
   * <span data-ttu-id="b6f2d-162">**태그**: 태그를 사용하면 클라우드 서비스의 사용자 지정 분류를 정의하기 위한 키/값 쌍을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-162">**Tags**: Tags allow you to set key/value pairs to define a custom taxonomy of your cloud services.</span></span> <span data-ttu-id="b6f2d-163">예를 들어 **project**라는 키를 만든 다음 특정 프로젝트와 연결된 모든 서비스에 공통 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-163">For example, you may create a key named **project**, and then use a common value for all services associated with a specific project.</span></span>
   * <span data-ttu-id="b6f2d-164">**Ambari 보기**: Ambari 웹에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-164">**Ambari Views**: Links to Ambari Web.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="b6f2d-165">HDInsight 클러스터에 의해 제공되는 서비스를 관리하려면 Ambari 웹 또는 Ambari REST API를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-165">To manage the services provided by the HDInsight cluster, you must use Ambari Web or the Ambari REST API.</span></span> <span data-ttu-id="b6f2d-166">Ambari 사용에 대한 자세한 내용은 [Ambari를 사용하여 HDInsight 클러스터 관리](hdinsight-hadoop-manage-ambari.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-166">For more information on using Ambari, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
     >
     >

     <span data-ttu-id="b6f2d-167">**사용 현황**</span><span class="sxs-lookup"><span data-stu-id="b6f2d-167">**Usage**:</span></span>

     ![Azure Portal HDInsight 클러스터 사용 현황](./media/hdinsight-administer-use-management-portal/hdinsight-portal-cluster-usage.png)
5. <span data-ttu-id="b6f2d-169">**설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-169">Click **Settings**.</span></span>

    ![Azure Portal HDInsight 클러스터 사용 현황](./media/hdinsight-administer-use-management-portal/hdinsight.portal.cluster.settings.png)

   * <span data-ttu-id="b6f2d-171">**속성**: 클러스터 속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-171">**Properties**: View the cluster properties.</span></span>
   * <span data-ttu-id="b6f2d-172">**클러스터 AAD ID**:</span><span class="sxs-lookup"><span data-stu-id="b6f2d-172">**Cluster AAD Identity**:</span></span>
   * <span data-ttu-id="b6f2d-173">**Azure 저장소 키**: 기본 저장소 계정 및 키를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-173">**Azure Storage Keys**: View the default storage account and its key.</span></span> <span data-ttu-id="b6f2d-174">저장소 계정은 클러스터를 만드는 과정에서 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-174">The storage account is configuration during the cluster creation process.</span></span>
   * <span data-ttu-id="b6f2d-175">**클러스터 로그인**: 클러스터 HTTP 사용자 이름 및 암호를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-175">**Cluster Login**: Change the cluster HTTP user name and password.</span></span>
   * <span data-ttu-id="b6f2d-176">**외부 Metastore**: Hive 및 Oozie Metastore를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-176">**External Metastores**: View the Hive and Oozie metastores.</span></span> <span data-ttu-id="b6f2d-177">Metastore는 클러스터 생성 과정 중에만 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-177">The metastores can only be configured during the cluster creation process.</span></span>
   * <span data-ttu-id="b6f2d-178">**클러스터 크기 조정**: 클러스터 작업자 노드의 수를 늘리거나 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-178">**Scale Cluster**: Increase and decrease the number of cluster worker nodes.</span></span>
   * <span data-ttu-id="b6f2d-179">**원격 데스크톱**: 원격 데스크톱(RDP) 액세스를 활성화하거나 비활성화하고 RDP 사용자 이름을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-179">**Remote Desktop**: Enable and disable remote desktop (RDP) access, and configure the RDP username.</span></span>  <span data-ttu-id="b6f2d-180">RDP 사용자 이름은 HTTP 사용자 이름과 반드시 달라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-180">The RDP user name must be different from the HTTP user name.</span></span>
   * <span data-ttu-id="b6f2d-181">**공식 파트너**:</span><span class="sxs-lookup"><span data-stu-id="b6f2d-181">**Partner of Record**:</span></span>

     > [!NOTE]
     > <span data-ttu-id="b6f2d-182">이것은 사용 가능한 설정의 일반적인 목록이며 여기의 모든 설정이 모든 클러스터 유형에 제공되는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-182">This is a generic list of available settings; not all of them will be present for all cluster types.</span></span>
     >
     >
6. <span data-ttu-id="b6f2d-183">**속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-183">Click **Properties**:</span></span>

    <span data-ttu-id="b6f2d-184">속성 섹션에는 다음 내용이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-184">The properties section lists the following:</span></span>

   * <span data-ttu-id="b6f2d-185">**호스트 이름**: 클러스터 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-185">**Hostname**: Cluster name.</span></span>
   * <span data-ttu-id="b6f2d-186">**클러스터 URL**.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-186">**Cluster URL**.</span></span>
   * <span data-ttu-id="b6f2d-187">**상태**: 중단됨, 수락됨, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, 운영, 실행 중, 오류, 삭제 중, 삭제됨, 시간 초과됨, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-187">**Status**: Include Aborted, Accepted, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, Operational, Running, Error, Deleting, Deleted, Timedout, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization</span></span>
   * <span data-ttu-id="b6f2d-188">**지역**: Azure 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-188">**Region**: Azure location.</span></span> <span data-ttu-id="b6f2d-189">지원되는 Azure 위치를 보려면, **HDInsight 가격** 의 [지역](https://azure.microsoft.com/pricing/details/hdinsight/)드롭다운 목록 상자를 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-189">For a list of supported Azure locations, see the **Region** dropdown list box on [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>
   * <span data-ttu-id="b6f2d-190">**생성된 데이터**.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-190">**Data created**.</span></span>
   * <span data-ttu-id="b6f2d-191">**운영 체제**: **Windows** 또는 **Linux**입니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-191">**Operating system**: Either **Windows** or **Linux**.</span></span>
   * <span data-ttu-id="b6f2d-192">**형식**: Hadoop, HBase, Storm, Spark.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-192">**Type**: Hadoop, HBase, Storm, Spark.</span></span>
   * <span data-ttu-id="b6f2d-193">**버전**.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-193">**Version**.</span></span> <span data-ttu-id="b6f2d-194">[HDInsight 버전](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="b6f2d-194">See [HDInsight versions](hdinsight-component-versioning.md)</span></span>
   * <span data-ttu-id="b6f2d-195">**구독**: 구독 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-195">**Subscription**: Subscription name.</span></span>
   * <span data-ttu-id="b6f2d-196">**구독 ID**.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-196">**Subscription ID**.</span></span>
   * <span data-ttu-id="b6f2d-197">**주 데이터 원본**.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-197">**Primary data source**.</span></span> <span data-ttu-id="b6f2d-198">Azure Blob 저장소 계정이 기본 Hadoop 파일 시스템으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-198">The Azure Blob storage account used as the default Hadoop file system.</span></span>
   * <span data-ttu-id="b6f2d-199">**작업자 노드 가격 책정 계층**.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-199">**Worker nodes pricing tier**.</span></span>
   * <span data-ttu-id="b6f2d-200">**헤드 노드 가격 책정 계층**.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-200">**Head node pricing tier**.</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="b6f2d-201">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="b6f2d-201">Delete clusters</span></span>
<span data-ttu-id="b6f2d-202">클러스터 삭제는 기본 저장소 계정이나 연결된 저장소 계정을 삭제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-202">Delete a cluster will not delete the default storage account or any linked storage accounts.</span></span> <span data-ttu-id="b6f2d-203">동일한 저장소 계정과 동일한 Metastore를 사용하여 클러스터를 다시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-203">You can re-create the cluster by using the same storage accounts and the same metastores.</span></span>

1. <span data-ttu-id="b6f2d-204">[포털][azure-portal]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-204">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="b6f2d-205">왼쪽 메뉴에서 **모두 찾아보기**, **HDInsight 클러스터**, 클러스터 이름을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-205">Click **Browse All** from the left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="b6f2d-206">상단 메뉴에서 **삭제** 를 클릭하고 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-206">Click **Delete** from the top menu, and then follow the instructions.</span></span>

<span data-ttu-id="b6f2d-207">참고 항목: [클러스터 일시 중지/종료](#pauseshut-down-clusters)</span><span class="sxs-lookup"><span data-stu-id="b6f2d-207">See also [Pause/shut down clusters](#pauseshut-down-clusters).</span></span>

## <a name="scale-clusters"></a><span data-ttu-id="b6f2d-208">클러스터 크기 조정</span><span class="sxs-lookup"><span data-stu-id="b6f2d-208">Scale clusters</span></span>
<span data-ttu-id="b6f2d-209">클러스터 크기 조정 기능을 사용하여 클러스터를 다시 생성하지 않고 Azure HDInsight에서 실행되는 클러스터에서 사용되는 작업자 노드 수를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-209">The cluster scaling feature allows you to change the number of worker nodes used by a cluster that is running in Azure HDInsight without having to re-create the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="b6f2d-210">HDInsight 버전 3.1.3 이상을 사용하는 클러스터만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-210">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="b6f2d-211">클러스터 버전을 알 수 없는 경우 속성 페이지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-211">If you are unsure of the version of your cluster, you can check the Properties page.</span></span>  <span data-ttu-id="b6f2d-212">[클러스터 나열 및 표시](#list-and-show-clusters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-212">See [List and show clusters](#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="b6f2d-213">HDInsight에서 지원되는 클러스터의 각 형식에 대한 데이터 노드 수를 변경하는 영향은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-213">The impact of changing the number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="b6f2d-214">Hadoop은</span><span class="sxs-lookup"><span data-stu-id="b6f2d-214">Hadoop</span></span>

    <span data-ttu-id="b6f2d-215">모든 보류 중인 또는 실행 중인 작업에 영향을 주지 않고 실행되는 Hadoop 클러스터의 작업자 노드 수를 원활하게 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-215">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="b6f2d-216">작업이 진행 중인 동안에 새 작업을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-216">New jobs can also be submitted while the operation is in progress.</span></span> <span data-ttu-id="b6f2d-217">크기 조정 작업의 오류는 정상적으로 처리되므로 클러스터는 항상 기능 상태로 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-217">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span></span>

    <span data-ttu-id="b6f2d-218">데이터 노드 수를 줄여 Hadoop 클러스터를 축소하면 클러스터의 서비스 중 일부가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-218">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span></span> <span data-ttu-id="b6f2d-219">그러면 실행 중인 작업과 보류 중인 작업이 크기 조정 작업을 완료하지 못하고 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-219">This causes all running and pending jobs to fail at the completion of the scaling operation.</span></span> <span data-ttu-id="b6f2d-220">그러나 작업이 완료되면 작업을 다시 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-220">You can, however, resubmit the jobs once the operation is complete.</span></span>
* <span data-ttu-id="b6f2d-221">HBase</span><span class="sxs-lookup"><span data-stu-id="b6f2d-221">HBase</span></span>

    <span data-ttu-id="b6f2d-222">HBase 클러스터가 실행 중인 동안 데이터 노드를 원활하게 추가하거나 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-222">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span></span> <span data-ttu-id="b6f2d-223">지역 서버는 크기 조정 작업을 완료하는 몇 분 안에 자동으로 균형을 맞춥니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-223">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span></span> <span data-ttu-id="b6f2d-224">그러나 클러스터의 헤드 노드에 로그인한 다음 명령 프롬프트 창에서 다음 명령을 실행하여 자동으로 지역 서버의 균형을 맞출 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-224">However, you can also manually balance the regional servers by logging into the headnode of cluster and running the following commands from a command prompt window:</span></span>

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer

    <span data-ttu-id="b6f2d-225">HBase 셸 사용에 대한 자세한 내용은 []을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-225">For more information on using the HBase shell, see []</span></span>
* <span data-ttu-id="b6f2d-226">Storm</span><span class="sxs-lookup"><span data-stu-id="b6f2d-226">Storm</span></span>

    <span data-ttu-id="b6f2d-227">실행 중인 동안 Storm 클러스터에 데이터 노드를 원활하게 추가하거나 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-227">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span></span> <span data-ttu-id="b6f2d-228">하지만 크기 조정 작업이 성공적으로 완료되면 다시 토폴로지 균형을 조정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-228">But after a successful completion of the scaling operation, you will need to rebalance the topology.</span></span>

    <span data-ttu-id="b6f2d-229">다음 두 가지 방법으로 사용하여 균형을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-229">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="b6f2d-230">Storm 웹 UI</span><span class="sxs-lookup"><span data-stu-id="b6f2d-230">Storm web UI</span></span>
  * <span data-ttu-id="b6f2d-231">명령줄 인터페이스(CLI) 도구</span><span class="sxs-lookup"><span data-stu-id="b6f2d-231">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="b6f2d-232">자세한 내용은 [Apache Storm 설명서](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) (영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-232">Please refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="b6f2d-233">Storm 웹 UI는 HDInsight 클러스터에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-233">The Storm web UI is available on the HDInsight cluster:</span></span>

    ![HDInsight Storm 규모 균형 재조정](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)

    <span data-ttu-id="b6f2d-235">다음은 CLI 명령을 사용하여 Storm 토폴로지 균형을 다시 조정하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-235">Here is an example how to use the CLI command to rebalance the Storm topology:</span></span>

        ## Reconfigure the topology "mytopology" to use 5 worker processes,
        ## the spout "blue-spout" to use 3 executors, and
        ## the bolt "yellow-bolt" to use 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="b6f2d-236">**클러스터 크기를 조정하려면**</span><span class="sxs-lookup"><span data-stu-id="b6f2d-236">**To scale clusters**</span></span>

1. <span data-ttu-id="b6f2d-237">[포털][azure-portal]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-237">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="b6f2d-238">왼쪽 메뉴에서 **모두 찾아보기**, **HDInsight 클러스터**, 클러스터 이름을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-238">Click **Browse All** from the left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="b6f2d-239">위쪽 메뉴에서 **설정**을 클릭한 다음 **클러스터 크기 조정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-239">Click **Settings** from the top menu, and then click **Scale Cluster**.</span></span>
4. <span data-ttu-id="b6f2d-240">**작업자 노드 수**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-240">Enter **Number of Worker nodes**.</span></span> <span data-ttu-id="b6f2d-241">클러스터 노드 수에 대한 제한은 Azure 구독에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-241">The limit on the number of cluster node varies among Azure subscriptions.</span></span> <span data-ttu-id="b6f2d-242">제한을 늘리려면 청구 지원 팀에 문의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-242">You can contact billing support to increase the limit.</span></span>  <span data-ttu-id="b6f2d-243">비용 정보는 노드 수에 대한 변경 내용을 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-243">The cost information will reflect the changes you have made to the number of nodes.</span></span>

    ![HDinsight Hadoop Hbase Storm Spark 크기 조정](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

## <a name="pauseshut-down-clusters"></a><span data-ttu-id="b6f2d-245">클러스터 일시 중지/종료</span><span class="sxs-lookup"><span data-stu-id="b6f2d-245">Pause/shut down clusters</span></span>
<span data-ttu-id="b6f2d-246">대부분의 Hadoop 작업은 이따금 실행되는 일괄 처리 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-246">Most of Hadoop jobs are batch jobs that are only ran occasionally.</span></span> <span data-ttu-id="b6f2d-247">대부분의 Hadoop 클러스터는 프로세스에 사용되지 않는 기간이 깁니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-247">For most Hadoop clusters, there are large periods of time that the cluster is not being used for processing.</span></span> <span data-ttu-id="b6f2d-248">HDInsight를 사용하면 데이터가 Azure 저장소에 저장되기 때문에 클러스터를 사용하지 않을 때 안전하게 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-248">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span>
<span data-ttu-id="b6f2d-249">HDInsight 클러스터를 사용하지 않는 기간에도 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-249">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="b6f2d-250">클러스터에 대한 요금이 저장소에 대한 요금보다 몇 배 더 많기 때문에, 클러스터를 사용하지 않을 때는 삭제하는 것이 경제적인 면에서 더 합리적입니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-250">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span></span>

<span data-ttu-id="b6f2d-251">프로세스를 프로그래밍할 수 있는 방법은 다양합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-251">There are many ways you can program the process:</span></span>

* <span data-ttu-id="b6f2d-252">사용자 Azure 데이터 팩터리.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-252">User Azure Data Factory.</span></span> <span data-ttu-id="b6f2d-253">주문형 및 자체 정의 HDInsight 연결된 서비스는 [Azure HDInsight 연결된 서비스](../data-factory/data-factory-compute-linked-services.md) 및 [Azure 데이터 팩터리를 사용한 분석 및 변환](../data-factory/data-factory-data-transformation-activities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-253">See [Azure HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md) and [Transform and analyze using Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md) for on-demand and self-defined HDInsight linked services.</span></span>
* <span data-ttu-id="b6f2d-254">Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="b6f2d-254">Use Azure PowerShell.</span></span>  <span data-ttu-id="b6f2d-255">[비행 지연 데이터 분석](hdinsight-analyze-flight-delay-data.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-255">See [Analyze flight delay data](hdinsight-analyze-flight-delay-data.md).</span></span>
* <span data-ttu-id="b6f2d-256">Azure CLI 사용</span><span class="sxs-lookup"><span data-stu-id="b6f2d-256">Use Azure CLI.</span></span> <span data-ttu-id="b6f2d-257">[Azure CLI를 사용하여 HDInsight 클러스터 관리](hdinsight-administer-use-command-line.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-257">See [Manage HDInsight clusters using Azure CLI](hdinsight-administer-use-command-line.md).</span></span>
* <span data-ttu-id="b6f2d-258">HDInsight .NET SDK 사용</span><span class="sxs-lookup"><span data-stu-id="b6f2d-258">Use HDInsight .NET SDK.</span></span> <span data-ttu-id="b6f2d-259">[Hadoop 작업 제출](hdinsight-submit-hadoop-jobs-programmatically.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-259">See [Submit Hadoop jobs](hdinsight-submit-hadoop-jobs-programmatically.md).</span></span>

<span data-ttu-id="b6f2d-260">가격 정보는 [HDInsight 가격](https://azure.microsoft.com/pricing/details/hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-260">For the pricing information, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span> <span data-ttu-id="b6f2d-261">포털에서 클러스터를 삭제하려면 [클러스터 삭제](#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="b6f2d-261">To delete a cluster from the Portal, see [Delete clusters](#delete-clusters)</span></span>

## <a name="change-cluster-username"></a><span data-ttu-id="b6f2d-262">클러스터 사용자 이름 변경</span><span class="sxs-lookup"><span data-stu-id="b6f2d-262">Change cluster username</span></span>
<span data-ttu-id="b6f2d-263">HDInsight 클러스터마다 두 개의 사용자 계정이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-263">An HDInsight cluster can have two user accounts.</span></span> <span data-ttu-id="b6f2d-264">HDInsight 클러스터 사용자 계정은 만드는 과정 중에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-264">The HDInsight cluster user account is created during the creation process.</span></span> <span data-ttu-id="b6f2d-265">RDP를 통해 클러스터에 액세스하기 위해 RDP 사용자 계정을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-265">You can also create an RDP user account for accessing the cluster via RDP.</span></span> <span data-ttu-id="b6f2d-266">[원격 데스크톱 사용](#connect-to-hdinsight-clusters-by-using-rdp)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-266">See [Enable remote desktop](#connect-to-hdinsight-clusters-by-using-rdp).</span></span>

<span data-ttu-id="b6f2d-267">**HDInsight 클러스터 사용자 이름 및 암호 변경**</span><span class="sxs-lookup"><span data-stu-id="b6f2d-267">**To change the HDInsight cluster user name and password**</span></span>

1. <span data-ttu-id="b6f2d-268">[포털][azure-portal]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-268">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="b6f2d-269">왼쪽 메뉴에서 **모두 찾아보기**, **HDInsight 클러스터**, 클러스터 이름을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-269">Click **Browse All** from the left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="b6f2d-270">상단 메뉴에서 **설정**을 클릭한 다음 **클러스터 로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-270">Click **Settings** from the top menu, and then click **Cluster Login**.</span></span>
4. <span data-ttu-id="b6f2d-271">**클러스터 로그인**이 활성화되어 있으면 **사용 안함**을 클릭한 후 **사용**을 클릭해야 사용자 이름과 암호를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-271">If **Cluster login** has been enabled, you must click **Disable**, and then click **Enable** before you can change the username and password..</span></span>
5. <span data-ttu-id="b6f2d-272">**클러스터 로그인 이름** 및/또는 **클러스터 로그인 암호**를 변경한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-272">Change the **Cluster Login Name** and/or the **Cluster Login Password**, and then click **Save**.</span></span>

    ![HDinsight 변경 클러스터 사용자 사용자 이름 암호 http 사용자](./media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="grantrevoke-access"></a><span data-ttu-id="b6f2d-274">액세스 권한 부여/해지</span><span class="sxs-lookup"><span data-stu-id="b6f2d-274">Grant/revoke access</span></span>
<span data-ttu-id="b6f2d-275">HDInsight 클러스터에는 다음과 같은 HTTP 웹 서비스가 있습니다(이러한 모든 서비스에 RESTful 끝점이 있음).</span><span class="sxs-lookup"><span data-stu-id="b6f2d-275">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="b6f2d-276">ODBC</span><span class="sxs-lookup"><span data-stu-id="b6f2d-276">ODBC</span></span>
* <span data-ttu-id="b6f2d-277">JDBC</span><span class="sxs-lookup"><span data-stu-id="b6f2d-277">JDBC</span></span>
* <span data-ttu-id="b6f2d-278">Ambari</span><span class="sxs-lookup"><span data-stu-id="b6f2d-278">Ambari</span></span>
* <span data-ttu-id="b6f2d-279">Oozie</span><span class="sxs-lookup"><span data-stu-id="b6f2d-279">Oozie</span></span>
* <span data-ttu-id="b6f2d-280">Templeton</span><span class="sxs-lookup"><span data-stu-id="b6f2d-280">Templeton</span></span>

<span data-ttu-id="b6f2d-281">이러한 서비스에는 기본적으로 액세스 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-281">By default, these services are granted for access.</span></span> <span data-ttu-id="b6f2d-282">Azure 포털에서 액세스 권한을 해지/부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-282">You can revoke/grant the access from the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="b6f2d-283">액세스 권한을 부여/해지하여 클러스터 사용자 이름 및 암호를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-283">By granting/revoking the access, you will reset the cluster user name and password.</span></span>
>
>

<span data-ttu-id="b6f2d-284">**HTTP 웹 서비스 액세스 권한을 부여/해지하려면**</span><span class="sxs-lookup"><span data-stu-id="b6f2d-284">**To grant/revoke HTTP web services access**</span></span>

1. <span data-ttu-id="b6f2d-285">[포털][azure-portal]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-285">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="b6f2d-286">왼쪽 메뉴에서 **모두 찾아보기**, **HDInsight 클러스터**, 클러스터 이름을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-286">Click **Browse All** from the left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="b6f2d-287">상단 메뉴에서 **설정**을 클릭한 다음 **클러스터 로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-287">Click **Settings** from the top menu, and then click **Cluster Login**.</span></span>
4. <span data-ttu-id="b6f2d-288">**클러스터 로그인**이 활성화되어 있으면 **사용 안함**을 클릭한 후 **사용**을 클릭해야 사용자 이름과 암호를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-288">If **Cluster login** has been enabled, you must click **Disable**, and then click **Enable** before you can change the username and password..</span></span>
5. <span data-ttu-id="b6f2d-289">**클러스터 로그인 사용자 이름** 및 **클러스터 로그인 암호**에 클러스터의 새 사용자 이름 및 암호를 각각 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-289">For **Cluster Login Username** and **Cluster Login Password**, enter the new user name and password (respectively) for the cluster.</span></span>
6. <span data-ttu-id="b6f2d-290">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-290">Click **SAVE**.</span></span>

    ![HDinsight 총합계 제거 http 웹 서비스 액세스](./media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="find-the-default-storage-account"></a><span data-ttu-id="b6f2d-292">기본 저장소 계정 찾기</span><span class="sxs-lookup"><span data-stu-id="b6f2d-292">Find the default storage account</span></span>
<span data-ttu-id="b6f2d-293">각 HDInsight 클러스터에는 기본 저장소 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-293">Each HDInsight cluster has a default storage account.</span></span> <span data-ttu-id="b6f2d-294">클러스터의 기본 저장소 계정 및 키는 **설정**/**속성**/**Azure 저장소 키**.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-294">The default storage account and its keys for a cluster appears under **Settings**/**Properties**/**Azure Storage Keys**.</span></span> <span data-ttu-id="b6f2d-295">[클러스터 나열 및 표시](#list-and-show-clusters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-295">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="find-the-resource-group"></a><span data-ttu-id="b6f2d-296">리소스 그룹 찾기</span><span class="sxs-lookup"><span data-stu-id="b6f2d-296">Find the resource group</span></span>
<span data-ttu-id="b6f2d-297">Azure Resource Manager 모드에서는 각각의 HDInsight 클러스터가 Azure 리소스 그룹과 함께 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-297">In the Azure Resource Manager mode, each HDInsight cluster is created with an Azure resource group.</span></span> <span data-ttu-id="b6f2d-298">클러스터가 속하는 Azure 리소스 그룹이 아래 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-298">The Azure resource group that a cluster belongs to appears in:</span></span>

* <span data-ttu-id="b6f2d-299">클러스터 목록에 **리소스 그룹** 열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-299">The cluster list has a **Resource Group** column.</span></span>
* <span data-ttu-id="b6f2d-300">클러스터 **Essential** 타일.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-300">Cluster **Essential** tile.</span></span>  

<span data-ttu-id="b6f2d-301">[클러스터 나열 및 표시](#list-and-show-clusters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-301">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="open-hdinsight-query-console"></a><span data-ttu-id="b6f2d-302">HDInsight 쿼리 콘솔 열기</span><span class="sxs-lookup"><span data-stu-id="b6f2d-302">Open HDInsight Query console</span></span>
<span data-ttu-id="b6f2d-303">HDInsight 쿼리 콘솔에는 다음 기능이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-303">The HDInsight Query console includes the following features:</span></span>

* <span data-ttu-id="b6f2d-304">**Hive 편집기**: Hive 작업 제출을 위한 GUI 웹 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-304">**Hive Editor**: A GUI web interface for submitting Hive jobs.</span></span>  <span data-ttu-id="b6f2d-305">[쿼리 콘솔을 사용하여 Hive 쿼리 실행](hdinsight-hadoop-use-hive-query-console.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-305">See [Run Hive queries using the Query Console](hdinsight-hadoop-use-hive-query-console.md).</span></span>

    ![HDInsight 포털 Hive 편집기](./media/hdinsight-administer-use-management-portal/hdinsight-hive-editor.png)
* <span data-ttu-id="b6f2d-307">**작업 내역**: Hadoop 작업을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-307">**Job history**: Monitor Hadoop jobs.</span></span>  

    ![HDInsight 포털 작업 내역](./media/hdinsight-administer-use-management-portal/hdinsight-job-history.png)

    <span data-ttu-id="b6f2d-309">작업 속성, **작업 쿼리**, **작업 출력을 비롯한 세부 정보를 표시하려면 **쿼리 이름**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-309">Click **Query Name** to show the details including Job properties, **Job Query**, and **Job Output.</span></span> <span data-ttu-id="b6f2d-310">사용자의 워크스테이션에 쿼리와 출력을 모두 다운로드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-310">You can also download both the query and the output to your workstation.</span></span>
* <span data-ttu-id="b6f2d-311">**파일 브라우저**: 기본 저장소 계정 및 연결된 저장소 계정을 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-311">**File Browser**: Browse the default storage account and the linked storage accounts.</span></span>

    ![HDInsight 포털 파일 브라우저 찾아보기](./media/hdinsight-administer-use-management-portal/hdinsight-file-browser.png)

    <span data-ttu-id="b6f2d-313">스크린샷에서 **<Account>** 형식은 해당 항목이 Azure 저장소 계정이라는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-313">On the screenshot, the **<Account>** type indicates the item is an Azure storage account.</span></span>  <span data-ttu-id="b6f2d-314">계정 이름을 클릭하여 파일을 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-314">Click the account name to browse the files.</span></span>
* <span data-ttu-id="b6f2d-315">**Hadoop UI**.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-315">**Hadoop UI**.</span></span>

    ![HDInsight 포털 Hadoop UI](./media/hdinsight-administer-use-management-portal/hdinsight-hadoop-ui.png)

    <span data-ttu-id="b6f2d-317">**Hadoop UI*에서 파일을 찾아보고 로그를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-317">From **Hadoop UI*, you can browse files, and check logs.</span></span>
* <span data-ttu-id="b6f2d-318">**Yarn UI**.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-318">**Yarn UI**.</span></span>

    ![HDInsight 포털 YARN UI](./media/hdinsight-administer-use-management-portal/hdinsight-yarn-ui.png)

## <a name="run-hive-queries"></a><span data-ttu-id="b6f2d-320">Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="b6f2d-320">Run Hive queries</span></span>
<span data-ttu-id="b6f2d-321">포털에서 Hive 작업을 실행하려면 HDInsight 쿼리 콘솔에서 **Hive 편집기** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-321">To ran Hive jobs from the Portal, click **Hive Editor** in the HDInsight Query console.</span></span> <span data-ttu-id="b6f2d-322">[HDInsight 쿼리 콘솔 열기](#open-hdinsight-query-console)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-322">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

## <a name="monitor-jobs"></a><span data-ttu-id="b6f2d-323">작업 모니터링</span><span class="sxs-lookup"><span data-stu-id="b6f2d-323">Monitor jobs</span></span>
<span data-ttu-id="b6f2d-324">포털에서 작업을 모니터링하려면 HDInsight 쿼리 콘솔에서 **작업 내역** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-324">To monitor jobs from the Portal, click **Job History** in the HDInsight Query console.</span></span> <span data-ttu-id="b6f2d-325">[HDInsight 쿼리 콘솔 열기](#open-hdinsight-query-console)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-325">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

## <a name="browse-files"></a><span data-ttu-id="b6f2d-326">파일 찾아보기</span><span class="sxs-lookup"><span data-stu-id="b6f2d-326">Browse files</span></span>
<span data-ttu-id="b6f2d-327">기본 저장소 계정 및 연결된 저장소 계정에 저장된 파일을 찾아보려면 HDInsight 쿼리 콘솔에서 **파일 브라우저** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-327">To browse files stored in the default storage account and the linked storage accounts, click **File Browser** in the HDInsight Query console.</span></span> <span data-ttu-id="b6f2d-328">[HDInsight 쿼리 콘솔 열기](#open-hdinsight-query-console)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-328">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

<span data-ttu-id="b6f2d-329">HDInsight 콘솔의 **Hadoop UI**에서 **파일 시스템 찾아보기** 유틸리티를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-329">You can also use the **Browse the file system** utility from the **Hadoop UI** in the HDInsight console.</span></span>  <span data-ttu-id="b6f2d-330">[HDInsight 쿼리 콘솔 열기](#open-hdinsight-query-console)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-330">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

## <a name="monitor-cluster-usage"></a><span data-ttu-id="b6f2d-331">클러스터 사용 현황 모니터링</span><span class="sxs-lookup"><span data-stu-id="b6f2d-331">Monitor cluster usage</span></span>
<span data-ttu-id="b6f2d-332">HDInsight 클러스터 블레이드의 **사용량** 섹션에는 HDInsight에서 사용하기 위해 구독에서 사용할 수 있는 코어 수뿐만 아니라 이 클러스터에 할당된 코어 수 및 이 클러스터 내에서 노드에 할당된 방법에 대한 정보도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-332">The **Usage** section of the HDInsight cluster blade displays information about the number of cores available to your subscription for use with HDInsight, as well as the number of cores allocated to this cluster and how they are allocated for the nodes within this cluster.</span></span> <span data-ttu-id="b6f2d-333">[클러스터 나열 및 표시](#list-and-show-clusters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-333">See [List and show clusters](#list-and-show-clusters).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b6f2d-334">HDInsight 클러스터에 의해 제공되는 서비스를 모니터링하려면 Ambari 웹 또는 Ambari REST API를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-334">To monitor the services provided by the HDInsight cluster, you must use Ambari Web or the Ambari REST API.</span></span> <span data-ttu-id="b6f2d-335">Ambari 사용에 대한 자세한 내용은 [Ambari를 사용하여 HDInsight 클러스터 관리](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="b6f2d-335">For more information on using Ambari, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>
>
>

## <a name="open-hadoop-ui"></a><span data-ttu-id="b6f2d-336">Hadoop UI 열기</span><span class="sxs-lookup"><span data-stu-id="b6f2d-336">Open Hadoop UI</span></span>
<span data-ttu-id="b6f2d-337">클러스터를 모니터링하고, 파일 시스템을 찾아보고, 로그를 확인하려면 HDInsight 쿼리 콘솔에서 **Hadoop UI** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-337">To monitor the cluster, browse the file system, and check logs, click **Hadoop UI** in the HDInsight Query console.</span></span> <span data-ttu-id="b6f2d-338">[HDInsight 쿼리 콘솔 열기](#open-hdinsight-query-console)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-338">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

## <a name="open-yarn-ui"></a><span data-ttu-id="b6f2d-339">Yarn UI 열기</span><span class="sxs-lookup"><span data-stu-id="b6f2d-339">Open Yarn UI</span></span>
<span data-ttu-id="b6f2d-340">Yarn 사용자 인터페이스를 사용하려면 HDInsight 쿼리 콘솔에서 **Yarn UI** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-340">To use Yarn user interface, click **Yarn UI** in the HDInsight Query console.</span></span> <span data-ttu-id="b6f2d-341">[HDInsight 쿼리 콘솔 열기](#open-hdinsight-query-console)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-341">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

## <a name="connect-to-clusters-using-rdp"></a><span data-ttu-id="b6f2d-342">RDP를 사용하여 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="b6f2d-342">Connect to clusters using RDP</span></span>
<span data-ttu-id="b6f2d-343">생성 시 제공한 클러스터의 자격 증명은 원격 데스크톱을 통해 클러스터 자체가 아니라 클러스터의 서비스에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-343">The credentials for the cluster that you provided at its creation give access to the services on the cluster, but not to the cluster itself through Remote Desktop.</span></span> <span data-ttu-id="b6f2d-344">클러스터를 프로비전할 때 또는 클러스터가 프로비전된 후 원격 데스크톱 액세스를 켤 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-344">You can turn on Remote Desktop access when you provision a cluster or after a cluster is provisioned.</span></span> <span data-ttu-id="b6f2d-345">생성 시 원격 데스크톱을 사용하도록 설정하는 방법에 대한 지침은 [HDInsight 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-345">For the instructions about enabling Remote Desktop at creation, see [Create HDInsight cluster](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="b6f2d-346">**원격 데스크톱을 사용하도록 설정하려면**</span><span class="sxs-lookup"><span data-stu-id="b6f2d-346">**To enable Remote Desktop**</span></span>

1. <span data-ttu-id="b6f2d-347">[포털][azure-portal]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-347">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="b6f2d-348">왼쪽 메뉴에서 **모두 찾아보기**, **HDInsight 클러스터**, 클러스터 이름을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-348">Click **Browse All** from the left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="b6f2d-349">상단 메뉴에서 **설정**을 클릭한 다음 **원격 데스크톱**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-349">Click **Settings** from the top menu, and then click **Remote Desktop**.</span></span>
4. <span data-ttu-id="b6f2d-350">**만료 날짜**, **원격 데스크톱 사용자 이름** 및 **원격 데스크톱 암호**를 입력한 다음 **사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-350">Enter **Expires On**, **Remote Desktop Username** and **Remote Desktop Password**, and then click **Enable**.</span></span>

    ![HDInsight에서 원격 데스크톱 비활성화 구성 해제](./media/hdinsight-administer-use-management-portal/hdinsight.portal.remote.desktop.png)

    <span data-ttu-id="b6f2d-352">만료 날짜에 대한 기본 값은 1주일입니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-352">The default values for Expires On is a week.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b6f2d-353">HDInsight .NET SDK를 통해 클러스터에서 원격 데스크톱을 사용하도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-353">You can also use the HDInsight .NET SDK to enable Remote Desktop on a cluster.</span></span> <span data-ttu-id="b6f2d-354">다음과 같은 방식으로 HDInsight 클라이언트 개체에서 **EnableRdp** 메서드를 사용합니다 **client.EnableRdp(clustername, location, "rdpuser", "rdppassword", DateTime.Now.AddDays(6))**.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-354">Use the **EnableRdp** method on the HDInsight client object in the following manner: **client.EnableRdp(clustername, location, "rdpuser", "rdppassword", DateTime.Now.AddDays(6))**.</span></span> <span data-ttu-id="b6f2d-355">마찬가지로, 클러스터에서 원격 데스크톱을 사용하지 않도록 설정하려면 **client.DisableRdp(clustername, location)**을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-355">Similarly, to disable Remote Desktop on the cluster, you can use **client.DisableRdp(clustername, location)**.</span></span> <span data-ttu-id="b6f2d-356">이러한 메서드에 대한 자세한 내용은 [HDInsight .NET SDK 참조](http://go.microsoft.com/fwlink/?LinkId=529017)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-356">For more information on these methods, see [HDInsight .NET SDK Reference](http://go.microsoft.com/fwlink/?LinkId=529017).</span></span> <span data-ttu-id="b6f2d-357">Windows에서 실행되는 HDInsight 클러스터에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-357">This is applicable only for HDInsight clusters running on Windows.</span></span>
   >
   >

<span data-ttu-id="b6f2d-358">**RDP를 사용하여 클러스터에 연결하려면**</span><span class="sxs-lookup"><span data-stu-id="b6f2d-358">**To connect to a cluster by using RDP**</span></span>

1. <span data-ttu-id="b6f2d-359">[포털][azure-portal]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-359">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="b6f2d-360">왼쪽 메뉴에서 **모두 찾아보기**, **HDInsight 클러스터**, 클러스터 이름을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-360">Click **Browse All** from the left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="b6f2d-361">상단 메뉴에서 **설정**을 클릭한 다음 **원격 데스크톱**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-361">Click **Settings** from the top menu, and then click **Remote Desktop**.</span></span>
4. <span data-ttu-id="b6f2d-362">**연결** 을 클릭하고 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-362">Click **Connect** and follow the instructions.</span></span> <span data-ttu-id="b6f2d-363">연결이 사용 안함인 경우 먼저 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-363">If Connect is disable, you must enable it first.</span></span> <span data-ttu-id="b6f2d-364">원격 데스크톱 사용자 이름 및 암호를 사용하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-364">Make sure using the Remote Desktop user username and password.</span></span>  <span data-ttu-id="b6f2d-365">클러스터 사용자 자격 증명을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-365">You can't use the Cluster user credentials.</span></span>

## <a name="open-hadoop-command-line"></a><span data-ttu-id="b6f2d-366">Hadoop 명령줄 열기</span><span class="sxs-lookup"><span data-stu-id="b6f2d-366">Open Hadoop command line</span></span>
<span data-ttu-id="b6f2d-367">원격 데스크톱을 통해 클러스터에 연결하고 Hadoop 명령줄을 사용하려면 이전 섹션에 설명된 대로 먼저 클러스터에 대한 원격 데스크톱 액세스를 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-367">To connect to the cluster by using Remote Desktop and use the Hadoop command line, you must first have enabled Remote Desktop access to the cluster as described in the previous section.</span></span>

<span data-ttu-id="b6f2d-368">**Hadoop 명령줄을 열려면**</span><span class="sxs-lookup"><span data-stu-id="b6f2d-368">**To open a Hadoop command line**</span></span>

1. <span data-ttu-id="b6f2d-369">원격 데스크톱을 사용하여 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-369">Connect to the cluster using Remote Desktop.</span></span>
2. <span data-ttu-id="b6f2d-370">데스크톱에서 **Hadoop 명령줄**을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-370">From the desktop, double-click **Hadoop Command Line**.</span></span>

    <span data-ttu-id="b6f2d-371">![HDI.HadoopCommandLine][image-hadoopcommandline]</span><span class="sxs-lookup"><span data-stu-id="b6f2d-371">![HDI.HadoopCommandLine][image-hadoopcommandline]</span></span>

    <span data-ttu-id="b6f2d-372">Hadoop 명령에 대한 자세한 내용은 [Hadoop 명령 참조](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/CommandsManual.html)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-372">For more information on Hadoop commands, see [Hadoop commands reference](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/CommandsManual.html).</span></span>

<span data-ttu-id="b6f2d-373">이전 스크린샷의 폴더 이름에는 Hadoop 버전 번호가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-373">In the previous screenshot, the folder name has the Hadoop version number embedded.</span></span> <span data-ttu-id="b6f2d-374">버전 번호는 클러스터에 설치된 Hadoop 구성 요소의 버전에 따라 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-374">The version number can changed based on the version of the Hadoop components installed on the cluster.</span></span> <span data-ttu-id="b6f2d-375">Hadoop 환경 변수를 사용하여 해당 폴더를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-375">You can use Hadoop environment variables to refer to those folders.</span></span> <span data-ttu-id="b6f2d-376">예:</span><span class="sxs-lookup"><span data-stu-id="b6f2d-376">For example:</span></span>

    cd %hadoop_home%
    cd %hive_home%
    cd %hbase_home%
    cd %pig_home%
    cd %sqoop_home%
    cd %hcatalog_home%

## <a name="next-steps"></a><span data-ttu-id="b6f2d-377">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b6f2d-377">Next steps</span></span>
<span data-ttu-id="b6f2d-378">이 문서에서는 포털을 사용하여 HDInsight 클러스터를 만드는 방법과 Hadoop 명령줄 도구를 여는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-378">In this article, you have learned how to create an HDInsight cluster by using the Portal, and how to open the Hadoop command-line tool.</span></span> <span data-ttu-id="b6f2d-379">자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6f2d-379">To learn more, see the following articles:</span></span>

* [<span data-ttu-id="b6f2d-380">Azure PowerShell을 사용하여 HDInsight 관리</span><span class="sxs-lookup"><span data-stu-id="b6f2d-380">Administer HDInsight Using Azure PowerShell</span></span>](hdinsight-administer-use-powershell.md)
* [<span data-ttu-id="b6f2d-381">Azure CLI를 사용하여 HDInsight 관리</span><span class="sxs-lookup"><span data-stu-id="b6f2d-381">Administer HDInsight Using Azure CLI</span></span>](hdinsight-administer-use-command-line.md)
* [<span data-ttu-id="b6f2d-382">HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="b6f2d-382">Create HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="b6f2d-383">프로그래밍 방식으로 Hadoop 작업 제출</span><span class="sxs-lookup"><span data-stu-id="b6f2d-383">Submit Hadoop jobs programmatically</span></span>](hdinsight-submit-hadoop-jobs-programmatically.md)
* [<span data-ttu-id="b6f2d-384">Azure HDInsight 시작</span><span class="sxs-lookup"><span data-stu-id="b6f2d-384">Get Started with Azure HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="b6f2d-385">Azure HDInsight에 포함된 Hadoop 버전</span><span class="sxs-lookup"><span data-stu-id="b6f2d-385">What version of Hadoop is in Azure HDInsight?</span></span>](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-management-portal/hdinsight-hadoop-command-line.png "Hadoop 명령줄"
