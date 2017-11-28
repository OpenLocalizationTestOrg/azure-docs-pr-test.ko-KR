---
title: "HDInsight를 사용 하 여의 aaaManage Windows 기반 Hadoop 클러스터 hello Azure 포털 | Microsoft Docs"
description: "자세한 내용은 방법 tooadminister HDInsight 서비스입니다. HDInsight 클러스터, 대화형 JavaScript 콘솔 열기 hello 및 열기 hello Hadoop 명령 콘솔을 만듭니다."
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
ms.openlocfilehash: a237726b0e37a08005ce22e96581739e93edb050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-windows-based-hadoop-clusters-in-hdinsight-by-using-hello-azure-portal"></a><span data-ttu-id="67f41-104">Hello Azure 포털을 사용 하 여 HDInsight의 Hadoop Windows 기반 클러스터를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-104">Manage Windows-based Hadoop clusters in HDInsight by using hello Azure portal</span></span>

<span data-ttu-id="67f41-105">Hello를 사용 하 여 [Azure 포털][azure-portal]프로토콜 RDP (원격 데스크톱)를 사용 하도록 설정에 액세스할 수 있도록 hello Hadoop 및 Azure HDInsight의 Hadoop Windows 기반 클러스터를 만들, Hadoop 사용자 암호를 변경할 수 있습니다, hello 클러스터에서 명령 콘솔입니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-105">Using hello [Azure portal][azure-portal], you can create Windows-based Hadoop clusters in Azure HDInsight, change Hadoop user password, and enable Remote Desktop Protocol (RDP) so you can access hello Hadoop command console on hello cluster.</span></span>

<span data-ttu-id="67f41-106">이 문서의 정보 hello에 tooWindow 기반 HDInsight 클러스터에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-106">hello information in this article only applies tooWindow-based HDInsight clusters.</span></span> <span data-ttu-id="67f41-107">Linux 기반 클러스터 관리에 대 한 자세한 내용은 참조 하십시오. [를 사용 하 여 HDInsight의 Hadoop 관리 클러스터에 Azure 포털 hello](hdinsight-administer-use-portal-linux.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-107">For information on managing Linux-based clusters, see [Manage Hadoop clusters in HDInsight by using hello Azure portal](hdinsight-administer-use-portal-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="67f41-108">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="67f41-109">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67f41-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="67f41-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="67f41-110">Prerequisites</span></span>

<span data-ttu-id="67f41-111">이 문서를 시작 하기 전에 hello 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-111">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="67f41-112">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="67f41-112">**An Azure subscription**.</span></span> <span data-ttu-id="67f41-113">[Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67f41-113">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="67f41-114">**Azure 저장소 계정** -는 HDInsight 클러스터 hello 기본 파일 시스템으로 Azure Blob 저장소 컨테이너를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-114">**Azure Storage account** - An HDInsight cluster uses an Azure Blob storage container as hello default file system.</span></span> <span data-ttu-id="67f41-115">Azure Blob 저장소가 HDInsight 클러스터에서 매끄럽게 작동하는 방식에 대한 자세한 내용은 [HDInsight에서 Azure Blob 저장소 사용](hdinsight-hadoop-use-blob-storage.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67f41-115">For more information about how Azure Blob storage provides a seamless experience with HDInsight clusters, see [Use Azure Blob Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="67f41-116">Azure 저장소 계정을 만드는 방법에 대 한 세부 정보를 참조 하십시오. [어떻게 tooCreate 저장소 계정](../storage/common/storage-create-storage-account.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-116">For details on creating an Azure Storage account, see [How tooCreate a Storage Account](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="open-hello-portal"></a><span data-ttu-id="67f41-117">Hello 포털 열기</span><span class="sxs-lookup"><span data-stu-id="67f41-117">Open hello Portal</span></span>
1. <span data-ttu-id="67f41-118">역시 로그인[https://portal.azure.com](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-118">Sign in too[https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="67f41-119">Hello 포털을 연 후 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-119">After you open hello portal, you can:</span></span>

   * <span data-ttu-id="67f41-120">클릭 **새로** hello 왼쪽된 메뉴 toocreate 새 클러스터에서에서:</span><span class="sxs-lookup"><span data-stu-id="67f41-120">Click **New** from hello left menu toocreate a new cluster:</span></span>

       ![새 HDInsight 클러스터 단추](./media/hdinsight-administer-use-management-portal/azure-portal-new-button.png)
   * <span data-ttu-id="67f41-122">클릭 **HDInsight 클러스터** hello 왼쪽된 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-122">Click **HDInsight Clusters** from hello left menu.</span></span>

       ![Azure 포털 HDInsight 클러스터 단추](./media/hdinsight-administer-use-management-portal/azure-portal-hdinsight-button.png)

     <span data-ttu-id="67f41-124">경우 **HDInsight** hello 왼쪽된 메뉴에 표시를 클릭 하지 **찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-124">If **HDInsight** doesn't appear in hello left menu, click **Browse**.</span></span>

     ![Azure Portal 찾아보기 클러스터 단추](./media/hdinsight-administer-use-management-portal/azure-portal-browse-button.png)

## <a name="create-clusters"></a><span data-ttu-id="67f41-126">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="67f41-126">Create clusters</span></span>
<span data-ttu-id="67f41-127">Hello 만들기 hello 포털을 사용 하 여 지침은 [만들 HDInsight 클러스터](hdinsight-hadoop-provision-linux-clusters.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-127">For hello creation instructions using hello Portal, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="67f41-128">HDInsight는 다양한 Hadoop 구성 요소에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-128">HDInsight works with a wide range of Hadoop components.</span></span> <span data-ttu-id="67f41-129">Hello 구성 요소 확인 및 지원 된 hello 목록에 대 한 참조 [Azure HDInsight의 Hadoop의 어떤 버전은](hdinsight-component-versioning.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-129">For hello list of hello components that have been verified and supported, see [What version of Hadoop is in Azure HDInsight](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="67f41-130">Hello 다음 옵션 중 하나를 사용 하 여 HDInsight를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-130">You can customize HDInsight by using one of hello following options:</span></span>

* <span data-ttu-id="67f41-131">사용 하 여 작업 스크립팅 toorun 사용자 지정 스크립트 클러스터 tooeither를 사용자 지정할 수 있는 클러스터 구성을 변경 하거나 Giraph 또는 Solr 같은 사용자 지정 구성 요소를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-131">Use Script Action toorun custom scripts that can customize a cluster tooeither change cluster configuration or install custom components such as Giraph or Solr.</span></span> <span data-ttu-id="67f41-132">자세한 내용은 [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster.md)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67f41-132">For more information, see [Customize HDInsight cluster using Script Action](hdinsight-hadoop-customize-cluster.md).</span></span>
* <span data-ttu-id="67f41-133">클러스터를 만드는 동안 hello HDInsight.NET SDK 또는 Azure PowerShell에서 hello 클러스터 사용자 지정 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-133">Use hello cluster customization parameters in hello HDInsight .NET SDK or Azure PowerShell during cluster creation.</span></span> <span data-ttu-id="67f41-134">이러한 구성 변경 내용을 다음 hello 클러스터의 hello 수명을 통해 보존 됩니다 및 유지 관리를 위해 Azure 플랫폼 주기적으로 수행 하는 클러스터 노드 reimages 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-134">These configuration changes are then preserved through hello lifetime of hello cluster and are not affected by cluster node reimages that Azure platform periodically performs for maintenance.</span></span> <span data-ttu-id="67f41-135">Hello 클러스터에 대 한 사용자 지정 매개 변수를 사용 하 여에 대 한 자세한 내용은 참조 하십시오. [만들 HDInsight 클러스터](hdinsight-hadoop-provision-linux-clusters.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-135">For more information on using hello cluster customization parameters, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="67f41-136">Mahout 및 Cascading와 같은 일부 네이티브 Java 구성 요소가 JAR 파일로 hello 클러스터에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-136">Some native Java components, like Mahout and Cascading, can be run on hello cluster as JAR files.</span></span> <span data-ttu-id="67f41-137">이러한 JAR 파일 분산된 tooAzure Blob 저장소 일 수 있습니다 및 tooHDInsight 클러스터 Hadoop 작업 전송 메커니즘을 통해 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-137">These JAR files can be distributed tooAzure Blob storage, and submitted tooHDInsight clusters through Hadoop job submission mechanisms.</span></span> <span data-ttu-id="67f41-138">자세한 내용은 [프로그래밍 방식으로 Hadoop 작업 제출](hdinsight-submit-hadoop-jobs-programmatically.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67f41-138">For more information, see [Submit Hadoop jobs programmatically](hdinsight-submit-hadoop-jobs-programmatically.md).</span></span>

  > [!NOTE]
  > <span data-ttu-id="67f41-139">JAR 파일 tooHDInsight 클러스터 배포 문제 또는 문의 HDInsight 클러스터에서 JAR 파일을 호출할 경우 [Microsoft 지원](https://azure.microsoft.com/support/options/)합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-139">If you have issues deploying JAR files tooHDInsight clusters or calling JAR files on HDInsight clusters, contact [Microsoft Support](https://azure.microsoft.com/support/options/).</span></span>
  >
  > <span data-ttu-id="67f41-140">Cascading은 HDInsight에서 지원되지 않으며 Microsoft 지원 대상이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-140">Cascading is not supported by HDInsight, and is not eligible for Microsoft Support.</span></span> <span data-ttu-id="67f41-141">지원 되는 구성의 목록에 대 한 참조 [HDInsight에서 제공 하는 hello 클러스터 버전의 새로운 기능](hdinsight-component-versioning.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-141">For lists of supported components, see [What's new in hello cluster versions provided by HDInsight](hdinsight-component-versioning.md).</span></span>
  >
  >

<span data-ttu-id="67f41-142">원격 데스크톱 연결을 사용 하 여 hello 클러스터에 있는 사용자 지정 소프트웨어 설치는 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-142">Installation of custom software on hello cluster by using Remote Desktop Connection is not supported.</span></span> <span data-ttu-id="67f41-143">Toore 해야 할 경우 삭제 될 것으로 hello 헤드 노드의 hello 드라이브에 모든 파일을 저장 하지 않아야-hello 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-143">You should avoid storing any files on hello drives of hello head node, as they will be lost if you need toore-create hello clusters.</span></span> <span data-ttu-id="67f41-144">Azure Blob 저장소에 파일을 저장하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-144">We recommend storing files on Azure Blob storage.</span></span> <span data-ttu-id="67f41-145">Blob 저장소는 영구적입니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-145">Blob storage is persistent.</span></span>

## <a name="list-and-show-clusters"></a><span data-ttu-id="67f41-146">클러스터 나열 및 표시</span><span class="sxs-lookup"><span data-stu-id="67f41-146">List and show clusters</span></span>
1. <span data-ttu-id="67f41-147">역시 로그인[https://portal.azure.com](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-147">Sign in too[https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="67f41-148">클릭 **HDInsight 클러스터** hello 왼쪽된 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-148">Click **HDInsight Clusters** from hello left menu.</span></span>
3. <span data-ttu-id="67f41-149">Hello 클러스터 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-149">Click hello cluster name.</span></span> <span data-ttu-id="67f41-150">Hello 클러스터 목록이 긴 경우에 hello hello 페이지 위쪽에 필터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-150">If hello cluster list is long, you can use filter on hello top of hello page.</span></span>
4. <span data-ttu-id="67f41-151">Hello 목록 tooshow hello 세부 정보에서 클러스터를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-151">Double-click a cluster from hello list tooshow hello details.</span></span>

    <span data-ttu-id="67f41-152">**메뉴 및 요점**:</span><span class="sxs-lookup"><span data-stu-id="67f41-152">**Menu and essentials**:</span></span>

    ![Azure Portal HDInsight 클러스터 요점](./media/hdinsight-administer-use-management-portal/hdinsight-essentials.png)

   * <span data-ttu-id="67f41-154">toocustomize hello 메뉴 hello 메뉴에서 아무 곳 이나 마우스 오른쪽 단추로 클릭 한 다음 클릭 **사용자 지정**합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-154">toocustomize hello menu, right-click anywhere on hello menu, and then click **Customize**.</span></span>
   * <span data-ttu-id="67f41-155">**설정** 및 **모든 설정을**: 표시 hello **설정을** 블레이드 tooaccess 수 있는 hello 클러스터에 대 한 자세한 hello 클러스터에 대 한 구성 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-155">**Settings** and **All Settings**: Displays hello **Settings** blade for hello cluster, which allows you tooaccess detailed configuration information for hello cluster.</span></span>
   * <span data-ttu-id="67f41-156">**대시보드**, **클러스터 대시보드** 및 **URL: 모든 방법으로 tooaccess hello 클러스터 대시보드 Linux 기반 클러스터용 Ambari Web 즉 이들은 합니다. -**보안 셸 * *: hello 지침 tooconnect toohello 클러스터를 SSH (보안 셸) 연결을 사용 하 여 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-156">**Dashboard**, **Cluster Dashboard** and **URL: These are all ways tooaccess hello cluster dashboard, which is Ambari Web for Linux-based clusters. -**Secure Shell**: Shows hello instructions tooconnect toohello cluster using Secure Shell (SSH) connection.</span></span>
   * <span data-ttu-id="67f41-157">**클러스터의 크기를 조정**:이 클러스터에 대 한 toochange hello 작업자 노드 수를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-157">**Scale Cluster**: Allows you toochange hello number of worker nodes for this cluster.</span></span>
   * <span data-ttu-id="67f41-158">**삭제**: hello 클러스터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-158">**Delete**: Deletes hello cluster.</span></span>
   * <span data-ttu-id="67f41-159">**빠른 시작**: HDInsight를 사용하여 시작하는 데 도움이 되는 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-159">**Quickstart**: Displays information that will help you get started using HDInsight.</span></span>
   * <span data-ttu-id="67f41-160">* * 사용자: 있습니다에 대 한 권한을 tooset *포털 관리* Azure 구독에서 다른 사용자에 대 한이 클러스터의 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-160">**Users: Allows you tooset permissions for *portal management* of this cluster for other users on your Azure subscription.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="67f41-161">이 *만* hello Azure 포털에에서 대 한 액세스 권한과 toothis 클러스터 미치며 tooor 전송 작업 toohello HDInsight 클러스터를 연결할 수 있는 사용자에 아무 효과가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-161">This *only* affects access and permissions toothis cluster in hello Azure portal, and has no effect on who can connect tooor submit jobs toohello HDInsight cluster.</span></span>
     >
     >
   * <span data-ttu-id="67f41-162">**태그**: 태그 있습니다 tooset 키/값 쌍 toodefine 클라우드 서비스의 사용자 정의 분류를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-162">**Tags**: Tags allow you tooset key/value pairs toodefine a custom taxonomy of your cloud services.</span></span> <span data-ttu-id="67f41-163">예를 들어 **project**라는 키를 만든 다음 특정 프로젝트와 연결된 모든 서비스에 공통 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-163">For example, you may create a key named **project**, and then use a common value for all services associated with a specific project.</span></span>
   * <span data-ttu-id="67f41-164">**Ambari 뷰**: tooAmbari 웹 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-164">**Ambari Views**: Links tooAmbari Web.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="67f41-165">HDInsight 클러스터 hello에서 toomanage hello 서비스 제공, Ambari Web을 사용 하거나 REST API Ambari hello 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-165">toomanage hello services provided by hello HDInsight cluster, you must use Ambari Web or hello Ambari REST API.</span></span> <span data-ttu-id="67f41-166">Ambari 사용에 대한 자세한 내용은 [Ambari를 사용하여 HDInsight 클러스터 관리](hdinsight-hadoop-manage-ambari.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67f41-166">For more information on using Ambari, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
     >
     >

     <span data-ttu-id="67f41-167">**사용 현황**</span><span class="sxs-lookup"><span data-stu-id="67f41-167">**Usage**:</span></span>

     ![Azure Portal HDInsight 클러스터 사용 현황](./media/hdinsight-administer-use-management-portal/hdinsight-portal-cluster-usage.png)
5. <span data-ttu-id="67f41-169">**설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-169">Click **Settings**.</span></span>

    ![Azure Portal HDInsight 클러스터 사용 현황](./media/hdinsight-administer-use-management-portal/hdinsight.portal.cluster.settings.png)

   * <span data-ttu-id="67f41-171">**속성**: hello 클러스터 속성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-171">**Properties**: View hello cluster properties.</span></span>
   * <span data-ttu-id="67f41-172">**클러스터 AAD ID**:</span><span class="sxs-lookup"><span data-stu-id="67f41-172">**Cluster AAD Identity**:</span></span>
   * <span data-ttu-id="67f41-173">**Azure 저장소 키**: hello 기본 저장소 계정 및 키를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-173">**Azure Storage Keys**: View hello default storage account and its key.</span></span> <span data-ttu-id="67f41-174">hello 저장소 계정은 hello 클러스터를 만드는 프로세스 동안 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-174">hello storage account is configuration during hello cluster creation process.</span></span>
   * <span data-ttu-id="67f41-175">**로그인 클러스터**: hello 클러스터 HTTP 사용자 이름 및 암호를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-175">**Cluster Login**: Change hello cluster HTTP user name and password.</span></span>
   * <span data-ttu-id="67f41-176">**외부 Metastore**: hello Hive 및 Oozie metastore를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-176">**External Metastores**: View hello Hive and Oozie metastores.</span></span> <span data-ttu-id="67f41-177">hello metastore hello 클러스터를 만드는 프로세스 동안만 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-177">hello metastores can only be configured during hello cluster creation process.</span></span>
   * <span data-ttu-id="67f41-178">**클러스터의 크기를 조정**: 증가 및 감소 hello 클러스터 작업자 노드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-178">**Scale Cluster**: Increase and decrease hello number of cluster worker nodes.</span></span>
   * <span data-ttu-id="67f41-179">**원격 데스크톱**: 설정 및 원격 데스크톱 (RDP) 액세스를 사용 하지 않도록 설정 및 hello RDP 사용자 이름을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-179">**Remote Desktop**: Enable and disable remote desktop (RDP) access, and configure hello RDP username.</span></span>  <span data-ttu-id="67f41-180">hello RDP 사용자 이름은 hello HTTP 사용자 이름은 달라 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-180">hello RDP user name must be different from hello HTTP user name.</span></span>
   * <span data-ttu-id="67f41-181">**공식 파트너**:</span><span class="sxs-lookup"><span data-stu-id="67f41-181">**Partner of Record**:</span></span>

     > [!NOTE]
     > <span data-ttu-id="67f41-182">이것은 사용 가능한 설정의 일반적인 목록이며 여기의 모든 설정이 모든 클러스터 유형에 제공되는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-182">This is a generic list of available settings; not all of them will be present for all cluster types.</span></span>
     >
     >
6. <span data-ttu-id="67f41-183">**속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-183">Click **Properties**:</span></span>

    <span data-ttu-id="67f41-184">hello 속성 섹션 hello 다음을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-184">hello properties section lists hello following:</span></span>

   * <span data-ttu-id="67f41-185">**호스트 이름**: 클러스터 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-185">**Hostname**: Cluster name.</span></span>
   * <span data-ttu-id="67f41-186">**클러스터 URL**.</span><span class="sxs-lookup"><span data-stu-id="67f41-186">**Cluster URL**.</span></span>
   * <span data-ttu-id="67f41-187">**상태**: 중단됨, 수락됨, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, 운영, 실행 중, 오류, 삭제 중, 삭제됨, 시간 초과됨, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-187">**Status**: Include Aborted, Accepted, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, Operational, Running, Error, Deleting, Deleted, Timedout, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization</span></span>
   * <span data-ttu-id="67f41-188">**지역**: Azure 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-188">**Region**: Azure location.</span></span> <span data-ttu-id="67f41-189">목록이 지원 되는 Azure 위치에 대 한 참조 hello **지역** 드롭다운 목록 상자 [HDInsight 가격](https://azure.microsoft.com/pricing/details/hdinsight/)합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-189">For a list of supported Azure locations, see hello **Region** dropdown list box on [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>
   * <span data-ttu-id="67f41-190">**생성된 데이터**.</span><span class="sxs-lookup"><span data-stu-id="67f41-190">**Data created**.</span></span>
   * <span data-ttu-id="67f41-191">**운영 체제**: **Windows** 또는 **Linux**입니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-191">**Operating system**: Either **Windows** or **Linux**.</span></span>
   * <span data-ttu-id="67f41-192">**형식**: Hadoop, HBase, Storm, Spark.</span><span class="sxs-lookup"><span data-stu-id="67f41-192">**Type**: Hadoop, HBase, Storm, Spark.</span></span>
   * <span data-ttu-id="67f41-193">**버전**.</span><span class="sxs-lookup"><span data-stu-id="67f41-193">**Version**.</span></span> <span data-ttu-id="67f41-194">[HDInsight 버전](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="67f41-194">See [HDInsight versions](hdinsight-component-versioning.md)</span></span>
   * <span data-ttu-id="67f41-195">**구독**: 구독 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-195">**Subscription**: Subscription name.</span></span>
   * <span data-ttu-id="67f41-196">**구독 ID**.</span><span class="sxs-lookup"><span data-stu-id="67f41-196">**Subscription ID**.</span></span>
   * <span data-ttu-id="67f41-197">**주 데이터 원본**.</span><span class="sxs-lookup"><span data-stu-id="67f41-197">**Primary data source**.</span></span> <span data-ttu-id="67f41-198">Azure Blob 저장소 계정 hello Hadoop 파일 시스템 hello 기본값으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-198">hello Azure Blob storage account used as hello default Hadoop file system.</span></span>
   * <span data-ttu-id="67f41-199">**작업자 노드 가격 책정 계층**.</span><span class="sxs-lookup"><span data-stu-id="67f41-199">**Worker nodes pricing tier**.</span></span>
   * <span data-ttu-id="67f41-200">**헤드 노드 가격 책정 계층**.</span><span class="sxs-lookup"><span data-stu-id="67f41-200">**Head node pricing tier**.</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="67f41-201">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="67f41-201">Delete clusters</span></span>
<span data-ttu-id="67f41-202">Hello 기본 저장소 계정 또는 연결 된 저장소 계정을 삭제 하는 클러스터 삭제 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-202">Delete a cluster will not delete hello default storage account or any linked storage accounts.</span></span> <span data-ttu-id="67f41-203">사용 하 여 hello 클러스터를 다시 만들 수 있습니다 hello 동일한 저장소 계정 및 동일한 metastore hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-203">You can re-create hello cluster by using hello same storage accounts and hello same metastores.</span></span>

1. <span data-ttu-id="67f41-204">Toohello 로그인 [포털][azure-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-204">Sign in toohello [Portal][azure-portal].</span></span>
2. <span data-ttu-id="67f41-205">클릭 **모두 찾아보기** hello 왼쪽된 메뉴에서 클릭 **HDInsight 클러스터**, 클러스터 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-205">Click **Browse All** from hello left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="67f41-206">클릭 **삭제** hello 위쪽 메뉴에서 다음 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-206">Click **Delete** from hello top menu, and then follow hello instructions.</span></span>

<span data-ttu-id="67f41-207">참고 항목: [클러스터 일시 중지/종료](#pauseshut-down-clusters)</span><span class="sxs-lookup"><span data-stu-id="67f41-207">See also [Pause/shut down clusters](#pauseshut-down-clusters).</span></span>

## <a name="scale-clusters"></a><span data-ttu-id="67f41-208">클러스터 크기 조정</span><span class="sxs-lookup"><span data-stu-id="67f41-208">Scale clusters</span></span>
<span data-ttu-id="67f41-209">hello 클러스터 기능을 확장 하면 toochange hello toore 필요 없이 Azure HDInsight에서 실행 되는 클러스터에서 사용 하는 작업자 노드 수-hello 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-209">hello cluster scaling feature allows you toochange hello number of worker nodes used by a cluster that is running in Azure HDInsight without having toore-create hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="67f41-210">HDInsight 버전 3.1.3 이상을 사용하는 클러스터만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-210">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="67f41-211">클러스터의 hello 버전을 잘 모를 경우 hello 속성 페이지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-211">If you are unsure of hello version of your cluster, you can check hello Properties page.</span></span>  <span data-ttu-id="67f41-212">[클러스터 나열 및 표시](#list-and-show-clusters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67f41-212">See [List and show clusters](#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="67f41-213">hello HDInsight에서 지원 되는 클러스터의 각 형식에 대 한 데이터 노드 수를 변경 하는 hello 미치는 영향:</span><span class="sxs-lookup"><span data-stu-id="67f41-213">hello impact of changing hello number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="67f41-214">Hadoop은</span><span class="sxs-lookup"><span data-stu-id="67f41-214">Hadoop</span></span>

    <span data-ttu-id="67f41-215">원활 하 게 hello 보류 중 또는 실행 중인 작업이 모두 영향을 주지 않고 실행 되는 Hadoop 클러스터의 작업자 노드 수를 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-215">You can seamlessly increase hello number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="67f41-216">Hello 작업이 진행 중인 동안에 새 작업을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-216">New jobs can also be submitted while hello operation is in progress.</span></span> <span data-ttu-id="67f41-217">크기 조정 작업의 오류는 hello 클러스터는 항상를 작동 상태로 남아 있도록 정상적으로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-217">Failures in a scaling operation are gracefully handled so that hello cluster is always left in a functional state.</span></span>

    <span data-ttu-id="67f41-218">Hadoop 클러스터는 hello 데이터 노드 수를 줄여 규모 축소, hello 클러스터의 hello 서비스 중 일부를 다시 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-218">When a Hadoop cluster is scaled down by reducing hello number of data nodes, some of hello services in hello cluster are restarted.</span></span> <span data-ttu-id="67f41-219">이렇게 하면 실행 중인 모든와 hello hello 크기 조정 작업이 완료 될 때 작업 toofail 보류 중.</span><span class="sxs-lookup"><span data-stu-id="67f41-219">This causes all running and pending jobs toofail at hello completion of hello scaling operation.</span></span> <span data-ttu-id="67f41-220">그러나 hello 작업이 완료 되 면 hello 작업을 다시 전송할을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-220">You can, however, resubmit hello jobs once hello operation is complete.</span></span>
* <span data-ttu-id="67f41-221">HBase</span><span class="sxs-lookup"><span data-stu-id="67f41-221">HBase</span></span>

    <span data-ttu-id="67f41-222">원활 하 게 추가 하거나 실행 하는 동안 노드 tooyour HBase 클러스터를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-222">You can seamlessly add or remove nodes tooyour HBase cluster while it is running.</span></span> <span data-ttu-id="67f41-223">지역 서버는 hello 크기 조정 작업을 완료 하는 몇 분 안에 자동으로 균형이 조정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-223">Regional Servers are automatically balanced within a few minutes of completing hello scaling operation.</span></span> <span data-ttu-id="67f41-224">그러나 명령을 명령 프롬프트 창에서 다음 실행 중인 hello와 클러스터의 헤드 노드에 hello에 로그인 하 여 hello 지역 서버를 수동으로 분산 시킬 수 있습니다 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-224">However, you can also manually balance hello regional servers by logging into hello headnode of cluster and running hello following commands from a command prompt window:</span></span>

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer

    <span data-ttu-id="67f41-225">Hello HBase 셸을 사용 하 여에 대 한 자세한 내용은 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="67f41-225">For more information on using hello HBase shell, see []</span></span>
* <span data-ttu-id="67f41-226">Storm</span><span class="sxs-lookup"><span data-stu-id="67f41-226">Storm</span></span>

    <span data-ttu-id="67f41-227">원활 하 게 추가 하거나 실행 하는 동안 데이터 노드 tooyour Storm 클러스터를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-227">You can seamlessly add or remove data nodes tooyour Storm cluster while it is running.</span></span> <span data-ttu-id="67f41-228">하지만 hello 크기 조정 작업을 성공적으로 완료 한 후 toorebalance hello 토폴로지를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-228">But after a successful completion of hello scaling operation, you will need toorebalance hello topology.</span></span>

    <span data-ttu-id="67f41-229">다음 두 가지 방법으로 사용하여 균형을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-229">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="67f41-230">Storm 웹 UI</span><span class="sxs-lookup"><span data-stu-id="67f41-230">Storm web UI</span></span>
  * <span data-ttu-id="67f41-231">명령줄 인터페이스(CLI) 도구</span><span class="sxs-lookup"><span data-stu-id="67f41-231">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="67f41-232">Toohello를 참조 하십시오 [Apache Storm 설명서](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) 자세한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-232">Please refer toohello [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="67f41-233">hello 스톰 웹 UI hello HDInsight 클러스터에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-233">hello Storm web UI is available on hello HDInsight cluster:</span></span>

    ![HDInsight Storm 규모 균형 재조정](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)

    <span data-ttu-id="67f41-235">다음은 예제 어떻게 toouse hello CLI 명령을 toorebalance hello 스톰 토폴로지:</span><span class="sxs-lookup"><span data-stu-id="67f41-235">Here is an example how toouse hello CLI command toorebalance hello Storm topology:</span></span>

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="67f41-236">**tooscale 클러스터**</span><span class="sxs-lookup"><span data-stu-id="67f41-236">**tooscale clusters**</span></span>

1. <span data-ttu-id="67f41-237">Toohello 로그인 [포털][azure-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-237">Sign in toohello [Portal][azure-portal].</span></span>
2. <span data-ttu-id="67f41-238">클릭 **모두 찾아보기** hello 왼쪽된 메뉴에서 클릭 **HDInsight 클러스터**, 클러스터 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-238">Click **Browse All** from hello left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="67f41-239">클릭 **설정** hello 상단 메뉴에서 **배율 클러스터**합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-239">Click **Settings** from hello top menu, and then click **Scale Cluster**.</span></span>
4. <span data-ttu-id="67f41-240">**작업자 노드 수**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-240">Enter **Number of Worker nodes**.</span></span> <span data-ttu-id="67f41-241">클러스터 노드의 hello 수 제한을 15 hello Azure 구독 마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-241">hello limit on hello number of cluster node varies among Azure subscriptions.</span></span> <span data-ttu-id="67f41-242">청구 지원 tooincrease hello 제한을 문의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-242">You can contact billing support tooincrease hello limit.</span></span>  <span data-ttu-id="67f41-243">hello 비용 정보 hello 변경 사항을 toohello 노드 수를 반영 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-243">hello cost information will reflect hello changes you have made toohello number of nodes.</span></span>

    ![HDinsight Hadoop Hbase Storm Spark 크기 조정](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

## <a name="pauseshut-down-clusters"></a><span data-ttu-id="67f41-245">클러스터 일시 중지/종료</span><span class="sxs-lookup"><span data-stu-id="67f41-245">Pause/shut down clusters</span></span>
<span data-ttu-id="67f41-246">대부분의 Hadoop 작업은 이따금 실행되는 일괄 처리 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-246">Most of Hadoop jobs are batch jobs that are only ran occasionally.</span></span> <span data-ttu-id="67f41-247">대부분의 Hadoop 클러스터에 대 한는 오랜 시간 해당 hello 클러스터 사용 하지 않는 처리를 위해 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-247">For most Hadoop clusters, there are large periods of time that hello cluster is not being used for processing.</span></span> <span data-ttu-id="67f41-248">HDInsight를 사용하면 데이터가 Azure 저장소에 저장되기 때문에 클러스터를 사용하지 않을 때 안전하게 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-248">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span>
<span data-ttu-id="67f41-249">HDInsight 클러스터를 사용하지 않는 기간에도 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-249">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="67f41-250">Hello 클러스터에 대 한 hello 요금이 저장소에 대 한 hello 요금 보다 많은 배 더 많은 경우 이렇게 하면 경제 toodelete 클러스터 사용에서 되지 않은 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-250">Since hello charges for hello cluster are many times more than hello charges for storage, it makes economic sense toodelete clusters when they are not in use.</span></span>

<span data-ttu-id="67f41-251">여러 가지 방법으로 hello 프로세스를 프로그래밍할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-251">There are many ways you can program hello process:</span></span>

* <span data-ttu-id="67f41-252">사용자 Azure 데이터 팩터리.</span><span class="sxs-lookup"><span data-stu-id="67f41-252">User Azure Data Factory.</span></span> <span data-ttu-id="67f41-253">주문형 및 자체 정의 HDInsight 연결된 서비스는 [Azure HDInsight 연결된 서비스](../data-factory/data-factory-compute-linked-services.md) 및 [Azure 데이터 팩터리를 사용한 분석 및 변환](../data-factory/data-factory-data-transformation-activities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67f41-253">See [Azure HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md) and [Transform and analyze using Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md) for on-demand and self-defined HDInsight linked services.</span></span>
* <span data-ttu-id="67f41-254">Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="67f41-254">Use Azure PowerShell.</span></span>  <span data-ttu-id="67f41-255">[비행 지연 데이터 분석](hdinsight-analyze-flight-delay-data.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67f41-255">See [Analyze flight delay data](hdinsight-analyze-flight-delay-data.md).</span></span>
* <span data-ttu-id="67f41-256">Azure CLI 사용</span><span class="sxs-lookup"><span data-stu-id="67f41-256">Use Azure CLI.</span></span> <span data-ttu-id="67f41-257">[Azure CLI를 사용하여 HDInsight 클러스터 관리](hdinsight-administer-use-command-line.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67f41-257">See [Manage HDInsight clusters using Azure CLI](hdinsight-administer-use-command-line.md).</span></span>
* <span data-ttu-id="67f41-258">HDInsight .NET SDK 사용</span><span class="sxs-lookup"><span data-stu-id="67f41-258">Use HDInsight .NET SDK.</span></span> <span data-ttu-id="67f41-259">[Hadoop 작업 제출](hdinsight-submit-hadoop-jobs-programmatically.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67f41-259">See [Submit Hadoop jobs](hdinsight-submit-hadoop-jobs-programmatically.md).</span></span>

<span data-ttu-id="67f41-260">가격 책정 정보는 hello에 대 한 참조 [HDInsight 가격](https://azure.microsoft.com/pricing/details/hdinsight/)합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-260">For hello pricing information, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span> <span data-ttu-id="67f41-261">hello 포털에서에서 클러스터 toodelete 참조 [클러스터를 삭제 합니다.](#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="67f41-261">toodelete a cluster from hello Portal, see [Delete clusters](#delete-clusters)</span></span>

## <a name="change-cluster-username"></a><span data-ttu-id="67f41-262">클러스터 사용자 이름 변경</span><span class="sxs-lookup"><span data-stu-id="67f41-262">Change cluster username</span></span>
<span data-ttu-id="67f41-263">HDInsight 클러스터마다 두 개의 사용자 계정이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-263">An HDInsight cluster can have two user accounts.</span></span> <span data-ttu-id="67f41-264">HDInsight 클러스터 사용자 계정 hello hello 만들기 프로세스 중 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-264">hello HDInsight cluster user account is created during hello creation process.</span></span> <span data-ttu-id="67f41-265">또한 RDP 통해 hello 클러스터에 액세스 하기 위한 RDP 사용자 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-265">You can also create an RDP user account for accessing hello cluster via RDP.</span></span> <span data-ttu-id="67f41-266">[원격 데스크톱 사용](#connect-to-hdinsight-clusters-by-using-rdp)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67f41-266">See [Enable remote desktop](#connect-to-hdinsight-clusters-by-using-rdp).</span></span>

<span data-ttu-id="67f41-267">**toochange hello HDInsight 클러스터 사용자 이름 및 암호**</span><span class="sxs-lookup"><span data-stu-id="67f41-267">**toochange hello HDInsight cluster user name and password**</span></span>

1. <span data-ttu-id="67f41-268">Toohello 로그인 [포털][azure-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-268">Sign in toohello [Portal][azure-portal].</span></span>
2. <span data-ttu-id="67f41-269">클릭 **모두 찾아보기** hello 왼쪽된 메뉴에서 클릭 **HDInsight 클러스터**, 클러스터 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-269">Click **Browse All** from hello left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="67f41-270">클릭 **설정** hello 상단 메뉴에서 **클러스터 로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-270">Click **Settings** from hello top menu, and then click **Cluster Login**.</span></span>
4. <span data-ttu-id="67f41-271">경우 **클러스터 로그인** 되었습니다 클릭 해야 사용 하도록 설정 **사용 하지 않도록 설정**, 클릭 하 고 **사용** hello 사용자 이름 및 암호를 변경할 수 있습니다...</span><span class="sxs-lookup"><span data-stu-id="67f41-271">If **Cluster login** has been enabled, you must click **Disable**, and then click **Enable** before you can change hello username and password..</span></span>
5. <span data-ttu-id="67f41-272">변경 hello **클러스터 로그인 이름** hello 및/또는 **클러스터 로그인 암호**, 클릭 하 고 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-272">Change hello **Cluster Login Name** and/or hello **Cluster Login Password**, and then click **Save**.</span></span>

    ![HDinsight 변경 클러스터 사용자 사용자 이름 암호 http 사용자](./media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="grantrevoke-access"></a><span data-ttu-id="67f41-274">액세스 권한 부여/해지</span><span class="sxs-lookup"><span data-stu-id="67f41-274">Grant/revoke access</span></span>
<span data-ttu-id="67f41-275">HDInsight 클러스터에는 HTTP 웹 서비스 (모든 이러한 서비스는 RESTful 끝점)를 수행 하는 hello:</span><span class="sxs-lookup"><span data-stu-id="67f41-275">HDInsight clusters have hello following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="67f41-276">ODBC</span><span class="sxs-lookup"><span data-stu-id="67f41-276">ODBC</span></span>
* <span data-ttu-id="67f41-277">JDBC</span><span class="sxs-lookup"><span data-stu-id="67f41-277">JDBC</span></span>
* <span data-ttu-id="67f41-278">Ambari</span><span class="sxs-lookup"><span data-stu-id="67f41-278">Ambari</span></span>
* <span data-ttu-id="67f41-279">Oozie</span><span class="sxs-lookup"><span data-stu-id="67f41-279">Oozie</span></span>
* <span data-ttu-id="67f41-280">Templeton</span><span class="sxs-lookup"><span data-stu-id="67f41-280">Templeton</span></span>

<span data-ttu-id="67f41-281">이러한 서비스에는 기본적으로 액세스 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-281">By default, these services are granted for access.</span></span> <span data-ttu-id="67f41-282">있습니다 수 revoke/부여 hello 액세스 hello Azure 포털에서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-282">You can revoke/grant hello access from hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="67f41-283">Hello 액세스 권한을 부여/취소를 하 여 hello 클러스터 사용자 이름 및 암호를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-283">By granting/revoking hello access, you will reset hello cluster user name and password.</span></span>
>
>

<span data-ttu-id="67f41-284">**HTTP toogrant/revoke 웹 서비스 액세스**</span><span class="sxs-lookup"><span data-stu-id="67f41-284">**toogrant/revoke HTTP web services access**</span></span>

1. <span data-ttu-id="67f41-285">Toohello 로그인 [포털][azure-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-285">Sign in toohello [Portal][azure-portal].</span></span>
2. <span data-ttu-id="67f41-286">클릭 **모두 찾아보기** hello 왼쪽된 메뉴에서 클릭 **HDInsight 클러스터**, 클러스터 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-286">Click **Browse All** from hello left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="67f41-287">클릭 **설정** hello 상단 메뉴에서 **클러스터 로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-287">Click **Settings** from hello top menu, and then click **Cluster Login**.</span></span>
4. <span data-ttu-id="67f41-288">경우 **클러스터 로그인** 되었습니다 클릭 해야 사용 하도록 설정 **사용 하지 않도록 설정**, 클릭 하 고 **사용** hello 사용자 이름 및 암호를 변경할 수 있습니다...</span><span class="sxs-lookup"><span data-stu-id="67f41-288">If **Cluster login** has been enabled, you must click **Disable**, and then click **Enable** before you can change hello username and password..</span></span>
5. <span data-ttu-id="67f41-289">에 대 한 **클러스터 로그인 사용자 이름과** 및 **클러스터 로그인 암호**, hello 클러스터에 대 한 hello 새 사용자 이름 및 암호를 각각 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-289">For **Cluster Login Username** and **Cluster Login Password**, enter hello new user name and password (respectively) for hello cluster.</span></span>
6. <span data-ttu-id="67f41-290">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-290">Click **SAVE**.</span></span>

    ![HDinsight 총합계 제거 http 웹 서비스 액세스](./media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="find-hello-default-storage-account"></a><span data-ttu-id="67f41-292">Hello 기본 저장소 계정 찾기</span><span class="sxs-lookup"><span data-stu-id="67f41-292">Find hello default storage account</span></span>
<span data-ttu-id="67f41-293">각 HDInsight 클러스터에는 기본 저장소 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-293">Each HDInsight cluster has a default storage account.</span></span> <span data-ttu-id="67f41-294">아래에 표시 하는 클러스터에 대 한 기본 저장소 계정 및 해당 키를 hello **설정**/**속성**/**Azure 저장소 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-294">hello default storage account and its keys for a cluster appears under **Settings**/**Properties**/**Azure Storage Keys**.</span></span> <span data-ttu-id="67f41-295">[클러스터 나열 및 표시](#list-and-show-clusters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67f41-295">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="find-hello-resource-group"></a><span data-ttu-id="67f41-296">Hello 리소스 그룹 찾기</span><span class="sxs-lookup"><span data-stu-id="67f41-296">Find hello resource group</span></span>
<span data-ttu-id="67f41-297">Hello Azure 리소스 관리자 모드에서 각 HDInsight 클러스터는 Azure 리소스 그룹으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-297">In hello Azure Resource Manager mode, each HDInsight cluster is created with an Azure resource group.</span></span> <span data-ttu-id="67f41-298">클러스터에 tooappears 속하는 hello Azure 리소스 그룹:</span><span class="sxs-lookup"><span data-stu-id="67f41-298">hello Azure resource group that a cluster belongs tooappears in:</span></span>

* <span data-ttu-id="67f41-299">hello 클러스터 목록에는 **리소스 그룹** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-299">hello cluster list has a **Resource Group** column.</span></span>
* <span data-ttu-id="67f41-300">클러스터 **Essential** 타일.</span><span class="sxs-lookup"><span data-stu-id="67f41-300">Cluster **Essential** tile.</span></span>  

<span data-ttu-id="67f41-301">[클러스터 나열 및 표시](#list-and-show-clusters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67f41-301">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="open-hdinsight-query-console"></a><span data-ttu-id="67f41-302">HDInsight 쿼리 콘솔 열기</span><span class="sxs-lookup"><span data-stu-id="67f41-302">Open HDInsight Query console</span></span>
<span data-ttu-id="67f41-303">hello HDInsight 쿼리 콘솔 hello 같은 기능에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-303">hello HDInsight Query console includes hello following features:</span></span>

* <span data-ttu-id="67f41-304">**Hive 편집기**: Hive 작업 제출을 위한 GUI 웹 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-304">**Hive Editor**: A GUI web interface for submitting Hive jobs.</span></span>  <span data-ttu-id="67f41-305">참조 [실행 하이브 쿼리를 사용 하 여 hello 쿼리 콘솔](hdinsight-hadoop-use-hive-query-console.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-305">See [Run Hive queries using hello Query Console](hdinsight-hadoop-use-hive-query-console.md).</span></span>

    ![HDInsight 포털 Hive 편집기](./media/hdinsight-administer-use-management-portal/hdinsight-hive-editor.png)
* <span data-ttu-id="67f41-307">**작업 내역**: Hadoop 작업을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-307">**Job history**: Monitor Hadoop jobs.</span></span>  

    ![HDInsight 포털 작업 내역](./media/hdinsight-administer-use-management-portal/hdinsight-job-history.png)

    <span data-ttu-id="67f41-309">클릭 **쿼리 이름** tooshow hello 작업 속성을 비롯 한 세부 정보 **작업 쿼리**, 및 * * 작업 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-309">Click **Query Name** tooshow hello details including Job properties, **Job Query**, and **Job Output.</span></span> <span data-ttu-id="67f41-310">Hello 쿼리와 hello 출력 tooyour 워크스테이션 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-310">You can also download both hello query and hello output tooyour workstation.</span></span>
* <span data-ttu-id="67f41-311">**브라우저 파일**: hello 기본 저장소 계정 찾아보기 및 연결 된 저장소 계정을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-311">**File Browser**: Browse hello default storage account and hello linked storage accounts.</span></span>

    ![HDInsight 포털 파일 브라우저 찾아보기](./media/hdinsight-administer-use-management-portal/hdinsight-file-browser.png)

    <span data-ttu-id="67f41-313">Hello 스크린 샷에 hello  **<Account>**  형식은 hello 항목은 Azure 저장소 계정을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-313">On hello screenshot, hello **<Account>** type indicates hello item is an Azure storage account.</span></span>  <span data-ttu-id="67f41-314">Hello 계정 이름 toobrowse hello 파일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-314">Click hello account name toobrowse hello files.</span></span>
* <span data-ttu-id="67f41-315">**Hadoop UI**.</span><span class="sxs-lookup"><span data-stu-id="67f41-315">**Hadoop UI**.</span></span>

    ![HDInsight 포털 Hadoop UI](./media/hdinsight-administer-use-management-portal/hdinsight-hadoop-ui.png)

    <span data-ttu-id="67f41-317">**Hadoop UI*에서 파일을 찾아보고 로그를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-317">From **Hadoop UI*, you can browse files, and check logs.</span></span>
* <span data-ttu-id="67f41-318">**Yarn UI**.</span><span class="sxs-lookup"><span data-stu-id="67f41-318">**Yarn UI**.</span></span>

    ![HDInsight 포털 YARN UI](./media/hdinsight-administer-use-management-portal/hdinsight-yarn-ui.png)

## <a name="run-hive-queries"></a><span data-ttu-id="67f41-320">Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="67f41-320">Run Hive queries</span></span>
<span data-ttu-id="67f41-321">tooran 하이브 작업은 hello 포털에서에서 클릭 **하이브 편집기** hello HDInsight 쿼리 콘솔.</span><span class="sxs-lookup"><span data-stu-id="67f41-321">tooran Hive jobs from hello Portal, click **Hive Editor** in hello HDInsight Query console.</span></span> <span data-ttu-id="67f41-322">[HDInsight 쿼리 콘솔 열기](#open-hdinsight-query-console)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67f41-322">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

## <a name="monitor-jobs"></a><span data-ttu-id="67f41-323">작업 모니터링</span><span class="sxs-lookup"><span data-stu-id="67f41-323">Monitor jobs</span></span>
<span data-ttu-id="67f41-324">toomonitor 작업은 hello 포털에서에서 클릭 **작업 기록** hello HDInsight 쿼리 콘솔.</span><span class="sxs-lookup"><span data-stu-id="67f41-324">toomonitor jobs from hello Portal, click **Job History** in hello HDInsight Query console.</span></span> <span data-ttu-id="67f41-325">[HDInsight 쿼리 콘솔 열기](#open-hdinsight-query-console)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67f41-325">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

## <a name="browse-files"></a><span data-ttu-id="67f41-326">파일 찾아보기</span><span class="sxs-lookup"><span data-stu-id="67f41-326">Browse files</span></span>
<span data-ttu-id="67f41-327">toobrowse 파일 hello 기본 저장소 계정에 저장 하 고 연결 된 저장소 계정을 hello, 클릭 **파일 브라우저** hello HDInsight 쿼리 콘솔.</span><span class="sxs-lookup"><span data-stu-id="67f41-327">toobrowse files stored in hello default storage account and hello linked storage accounts, click **File Browser** in hello HDInsight Query console.</span></span> <span data-ttu-id="67f41-328">[HDInsight 쿼리 콘솔 열기](#open-hdinsight-query-console)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67f41-328">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

<span data-ttu-id="67f41-329">Hello를 사용할 수도 있습니다 **hello 파일 시스템 검색** hello에서 유틸리티 **Hadoop UI** hello HDInsight 콘솔에서.</span><span class="sxs-lookup"><span data-stu-id="67f41-329">You can also use hello **Browse hello file system** utility from hello **Hadoop UI** in hello HDInsight console.</span></span>  <span data-ttu-id="67f41-330">[HDInsight 쿼리 콘솔 열기](#open-hdinsight-query-console)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67f41-330">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

## <a name="monitor-cluster-usage"></a><span data-ttu-id="67f41-331">클러스터 사용 현황 모니터링</span><span class="sxs-lookup"><span data-stu-id="67f41-331">Monitor cluster usage</span></span>
<span data-ttu-id="67f41-332">hello **사용** hello HDInsight 클러스터 블레이드의 섹션에는 hello HDInsight 함께 사용할 사용 가능한 tooyour 구독 코어 수가 hello toothis 클러스터 하 게 하는 방법을 할당 하는 코어 수에 대 한 정보가 표시 됩니다. 이 클러스터 내에서 hello 노드에 대 한 할당.</span><span class="sxs-lookup"><span data-stu-id="67f41-332">hello **Usage** section of hello HDInsight cluster blade displays information about hello number of cores available tooyour subscription for use with HDInsight, as well as hello number of cores allocated toothis cluster and how they are allocated for hello nodes within this cluster.</span></span> <span data-ttu-id="67f41-333">[클러스터 나열 및 표시](#list-and-show-clusters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67f41-333">See [List and show clusters](#list-and-show-clusters).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="67f41-334">HDInsight 클러스터 hello에서 toomonitor hello 서비스 제공, Ambari Web을 사용 하거나 REST API Ambari hello 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-334">toomonitor hello services provided by hello HDInsight cluster, you must use Ambari Web or hello Ambari REST API.</span></span> <span data-ttu-id="67f41-335">Ambari 사용에 대한 자세한 내용은 [Ambari를 사용하여 HDInsight 클러스터 관리](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="67f41-335">For more information on using Ambari, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>
>
>

## <a name="open-hadoop-ui"></a><span data-ttu-id="67f41-336">Hadoop UI 열기</span><span class="sxs-lookup"><span data-stu-id="67f41-336">Open Hadoop UI</span></span>
<span data-ttu-id="67f41-337">toomonitor hello 클러스터, 찾아보기 hello 파일 시스템 및 로그를 확인 하 고, 클릭 **Hadoop UI** hello HDInsight 쿼리 콘솔.</span><span class="sxs-lookup"><span data-stu-id="67f41-337">toomonitor hello cluster, browse hello file system, and check logs, click **Hadoop UI** in hello HDInsight Query console.</span></span> <span data-ttu-id="67f41-338">[HDInsight 쿼리 콘솔 열기](#open-hdinsight-query-console)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67f41-338">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

## <a name="open-yarn-ui"></a><span data-ttu-id="67f41-339">Yarn UI 열기</span><span class="sxs-lookup"><span data-stu-id="67f41-339">Open Yarn UI</span></span>
<span data-ttu-id="67f41-340">toouse Yarn 사용자 인터페이스를 클릭 하 여 **Yarn UI** hello HDInsight 쿼리 콘솔.</span><span class="sxs-lookup"><span data-stu-id="67f41-340">toouse Yarn user interface, click **Yarn UI** in hello HDInsight Query console.</span></span> <span data-ttu-id="67f41-341">[HDInsight 쿼리 콘솔 열기](#open-hdinsight-query-console)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67f41-341">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

## <a name="connect-tooclusters-using-rdp"></a><span data-ttu-id="67f41-342">Tooclusters RDP를 사용 하 여 연결</span><span class="sxs-lookup"><span data-stu-id="67f41-342">Connect tooclusters using RDP</span></span>
<span data-ttu-id="67f41-343">생성 시 사용자가 제공한 hello 클러스터에 대 한 자격 증명 hello hello 클러스터 있지만 하지 toohello 클러스터 자체 원격 데스크톱을 통해 toohello 서비스 액세스를 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-343">hello credentials for hello cluster that you provided at its creation give access toohello services on hello cluster, but not toohello cluster itself through Remote Desktop.</span></span> <span data-ttu-id="67f41-344">클러스터를 프로비전할 때 또는 클러스터가 프로비전된 후 원격 데스크톱 액세스를 켤 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-344">You can turn on Remote Desktop access when you provision a cluster or after a cluster is provisioned.</span></span> <span data-ttu-id="67f41-345">Hello 생성 시 원격 데스크톱을 사용 하는 방법에 대 한 지침은 [만들 HDInsight 클러스터](hdinsight-hadoop-provision-linux-clusters.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-345">For hello instructions about enabling Remote Desktop at creation, see [Create HDInsight cluster](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="67f41-346">**원격 데스크톱 tooenable**</span><span class="sxs-lookup"><span data-stu-id="67f41-346">**tooenable Remote Desktop**</span></span>

1. <span data-ttu-id="67f41-347">Toohello 로그인 [포털][azure-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-347">Sign in toohello [Portal][azure-portal].</span></span>
2. <span data-ttu-id="67f41-348">클릭 **모두 찾아보기** hello 왼쪽된 메뉴에서 클릭 **HDInsight 클러스터**, 클러스터 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-348">Click **Browse All** from hello left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="67f41-349">클릭 **설정** hello 상단 메뉴에서 **원격 데스크톱**합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-349">Click **Settings** from hello top menu, and then click **Remote Desktop**.</span></span>
4. <span data-ttu-id="67f41-350">**만료 날짜**, **원격 데스크톱 사용자 이름** 및 **원격 데스크톱 암호**를 입력한 다음 **사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-350">Enter **Expires On**, **Remote Desktop Username** and **Remote Desktop Password**, and then click **Enable**.</span></span>

    ![HDInsight에서 원격 데스크톱 비활성화 구성 해제](./media/hdinsight-administer-use-management-portal/hdinsight.portal.remote.desktop.png)

    <span data-ttu-id="67f41-352">만료에 대 한 hello 기본값은 1 주일입니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-352">hello default values for Expires On is a week.</span></span>

   > [!NOTE]
   > <span data-ttu-id="67f41-353">클러스터에 hello HDInsight.NET SDK tooenable 원격 데스크톱을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-353">You can also use hello HDInsight .NET SDK tooenable Remote Desktop on a cluster.</span></span> <span data-ttu-id="67f41-354">사용 하 여 hello **EnableRdp** hello 방식으로 다음에 hello HDInsight 클라이언트 개체에서 메서드: **클라이언트입니다. EnableRdp (clustername, 위치, "rdpuser", "rdppassword", DateTime.Now.AddDays(6))**합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-354">Use hello **EnableRdp** method on hello HDInsight client object in hello following manner: **client.EnableRdp(clustername, location, "rdpuser", "rdppassword", DateTime.Now.AddDays(6))**.</span></span> <span data-ttu-id="67f41-355">마찬가지로, hello 클러스터에 원격 데스크톱을 toodisable를 사용할 수 있습니다 **클라이언트입니다. (Clustername, 위치) DisableRdp**합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-355">Similarly, toodisable Remote Desktop on hello cluster, you can use **client.DisableRdp(clustername, location)**.</span></span> <span data-ttu-id="67f41-356">이러한 메서드에 대한 자세한 내용은 [HDInsight .NET SDK 참조](http://go.microsoft.com/fwlink/?LinkId=529017)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67f41-356">For more information on these methods, see [HDInsight .NET SDK Reference](http://go.microsoft.com/fwlink/?LinkId=529017).</span></span> <span data-ttu-id="67f41-357">Windows에서 실행되는 HDInsight 클러스터에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-357">This is applicable only for HDInsight clusters running on Windows.</span></span>
   >
   >

<span data-ttu-id="67f41-358">**RDP를 사용 하 여 tooconnect tooa 클러스터**</span><span class="sxs-lookup"><span data-stu-id="67f41-358">**tooconnect tooa cluster by using RDP**</span></span>

1. <span data-ttu-id="67f41-359">Toohello 로그인 [포털][azure-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-359">Sign in toohello [Portal][azure-portal].</span></span>
2. <span data-ttu-id="67f41-360">클릭 **모두 찾아보기** hello 왼쪽된 메뉴에서 클릭 **HDInsight 클러스터**, 클러스터 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-360">Click **Browse All** from hello left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="67f41-361">클릭 **설정** hello 상단 메뉴에서 **원격 데스크톱**합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-361">Click **Settings** from hello top menu, and then click **Remote Desktop**.</span></span>
4. <span data-ttu-id="67f41-362">클릭 **연결** hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-362">Click **Connect** and follow hello instructions.</span></span> <span data-ttu-id="67f41-363">연결이 사용 안함인 경우 먼저 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-363">If Connect is disable, you must enable it first.</span></span> <span data-ttu-id="67f41-364">Hello 원격 데스크톱 사용자 이름과 암호를 사용 하 여 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-364">Make sure using hello Remote Desktop user username and password.</span></span>  <span data-ttu-id="67f41-365">Hello 클러스터 사용자 자격 증명을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-365">You can't use hello Cluster user credentials.</span></span>

## <a name="open-hadoop-command-line"></a><span data-ttu-id="67f41-366">Hadoop 명령줄 열기</span><span class="sxs-lookup"><span data-stu-id="67f41-366">Open Hadoop command line</span></span>
<span data-ttu-id="67f41-367">원격 데스크톱을 사용 하 여 hello Hadoop 명령줄을 사용 하 여 tooconnect toohello 클러스터를 먼저 설정 해야 원격 데스크톱 액세스 toohello 클러스터 hello 이전 섹션에 설명 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-367">tooconnect toohello cluster by using Remote Desktop and use hello Hadoop command line, you must first have enabled Remote Desktop access toohello cluster as described in hello previous section.</span></span>

<span data-ttu-id="67f41-368">**tooopen Hadoop 명령줄**</span><span class="sxs-lookup"><span data-stu-id="67f41-368">**tooopen a Hadoop command line**</span></span>

1. <span data-ttu-id="67f41-369">원격 데스크톱을 사용 하 여 toohello 클러스터에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-369">Connect toohello cluster using Remote Desktop.</span></span>
2. <span data-ttu-id="67f41-370">Hello 바탕 화면에서 두 번 클릭 **Hadoop 명령줄**합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-370">From hello desktop, double-click **Hadoop Command Line**.</span></span>

    <span data-ttu-id="67f41-371">![HDI.HadoopCommandLine][image-hadoopcommandline]</span><span class="sxs-lookup"><span data-stu-id="67f41-371">![HDI.HadoopCommandLine][image-hadoopcommandline]</span></span>

    <span data-ttu-id="67f41-372">Hadoop 명령에 대한 자세한 내용은 [Hadoop 명령 참조](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/CommandsManual.html)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67f41-372">For more information on Hadoop commands, see [Hadoop commands reference](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/CommandsManual.html).</span></span>

<span data-ttu-id="67f41-373">Hello 이전 스크린 샷 hello 폴더 이름에는 내장 된 hello Hadoop 버전 번호를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-373">In hello previous screenshot, hello folder name has hello Hadoop version number embedded.</span></span> <span data-ttu-id="67f41-374">hello 버전 번호 수에 따라 hello 변경 된 버전의 hello Hadoop 구성 요소가 hello 클러스터에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-374">hello version number can changed based on hello version of hello Hadoop components installed on hello cluster.</span></span> <span data-ttu-id="67f41-375">Hadoop 환경 변수 toorefer toothose 폴더를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-375">You can use Hadoop environment variables toorefer toothose folders.</span></span> <span data-ttu-id="67f41-376">예:</span><span class="sxs-lookup"><span data-stu-id="67f41-376">For example:</span></span>

    cd %hadoop_home%
    cd %hive_home%
    cd %hbase_home%
    cd %pig_home%
    cd %sqoop_home%
    cd %hcatalog_home%

## <a name="next-steps"></a><span data-ttu-id="67f41-377">다음 단계</span><span class="sxs-lookup"><span data-stu-id="67f41-377">Next steps</span></span>
<span data-ttu-id="67f41-378">이 문서에서는 방법을 사용 하 여 HDInsight 클러스터 toocreate hello 포털 및 tooopen Hadoop 명령줄 도구를 hello 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="67f41-378">In this article, you have learned how toocreate an HDInsight cluster by using hello Portal, and how tooopen hello Hadoop command-line tool.</span></span> <span data-ttu-id="67f41-379">더 toolearn hello 다음 문서를 참조:</span><span class="sxs-lookup"><span data-stu-id="67f41-379">toolearn more, see hello following articles:</span></span>

* [<span data-ttu-id="67f41-380">Azure PowerShell을 사용하여 HDInsight 관리</span><span class="sxs-lookup"><span data-stu-id="67f41-380">Administer HDInsight Using Azure PowerShell</span></span>](hdinsight-administer-use-powershell.md)
* [<span data-ttu-id="67f41-381">Azure CLI를 사용하여 HDInsight 관리</span><span class="sxs-lookup"><span data-stu-id="67f41-381">Administer HDInsight Using Azure CLI</span></span>](hdinsight-administer-use-command-line.md)
* [<span data-ttu-id="67f41-382">HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="67f41-382">Create HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="67f41-383">프로그래밍 방식으로 Hadoop 작업 제출</span><span class="sxs-lookup"><span data-stu-id="67f41-383">Submit Hadoop jobs programmatically</span></span>](hdinsight-submit-hadoop-jobs-programmatically.md)
* [<span data-ttu-id="67f41-384">Azure HDInsight 시작</span><span class="sxs-lookup"><span data-stu-id="67f41-384">Get Started with Azure HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="67f41-385">Azure HDInsight에 포함된 Hadoop 버전</span><span class="sxs-lookup"><span data-stu-id="67f41-385">What version of Hadoop is in Azure HDInsight?</span></span>](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-management-portal/hdinsight-hadoop-command-line.png "Hadoop 명령줄"
