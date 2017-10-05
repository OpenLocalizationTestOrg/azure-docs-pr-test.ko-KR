---
title: "Azure Portal을 사용하여 HDInsight의 Hadoop 클러스터 관리 | Microsoft Docs"
description: "Azure Portal을 사용하여 HDInsight 클러스터를 만들고 관리하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5a76f897-02e8-4437-8f2b-4fb12225854a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: c9cb631aef71f72457c3517d02566a56919f82bc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-the-azure-portal"></a><span data-ttu-id="ebffa-103">Azure 포털을 사용하여 HDInsight의 Hadoop 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="ebffa-103">Manage Hadoop clusters in HDInsight by using the Azure portal</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="ebffa-104">[Azure Portal][azure-portal]을 사용하여 Azure HDInsight에서 Hadoop 클러스터를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-104">Using the [Azure portal][azure-portal], you can manage Hadoop clusters in Azure HDInsight.</span></span> <span data-ttu-id="ebffa-105">다른 도구를 사용하여 HDInsight에서 Hadoop 클러스터를 관리하는 정보를 보려면 탭 선택기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-105">Use the tab selector for information on managing Hadoop clusters in HDInsight using other tools.</span></span>

<span data-ttu-id="ebffa-106">**필수 구성 요소**</span><span class="sxs-lookup"><span data-stu-id="ebffa-106">**Prerequisites**</span></span>

<span data-ttu-id="ebffa-107">이 문서를 시작하기 전에 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-107">Before you begin this article, you must have the following items:</span></span>

* <span data-ttu-id="ebffa-108">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="ebffa-108">**An Azure subscription**.</span></span> <span data-ttu-id="ebffa-109">[Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebffa-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="open-the-portal"></a><span data-ttu-id="ebffa-110">포털 열기</span><span class="sxs-lookup"><span data-stu-id="ebffa-110">Open the portal</span></span>
1. <span data-ttu-id="ebffa-111">[https://portal.azure.com](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-111">Sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ebffa-112">포털을 연 후 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-112">After you open the portal, you can:</span></span>

   * <span data-ttu-id="ebffa-113">왼쪽 메뉴에서 **새로 만들기** 를 클릭하여 새 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-113">Click **New** from the left menu to create a new cluster:</span></span>

       ![새 HDInsight 클러스터 단추](./media/hdinsight-administer-use-portal-linux/azure-portal-new-button.png)
   * <span data-ttu-id="ebffa-115">왼쪽 메뉴에서 **HDInsight 클러스터** 를 클릭하여 기존 클러스터를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-115">Click **HDInsight Clusters** from the left menu to list the existing clusters</span></span>

       ![Azure 포털 HDInsight 클러스터 단추](./media/hdinsight-administer-use-portal-linux/azure-portal-hdinsight-button.png)

       <span data-ttu-id="ebffa-117">HDInsight 클러스터가 표시되지 않으면 목록 아래쪽에서 **더 많은 서비스**를 클릭한 다음 **인텔리전스 + 분석** 섹션에서 **HDInsight 클러스터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-117">If you don't see HDInsight cluster, click **More services** on the bottom of the list, and then click **HDInsight clusters** under the **Intelligence + Analytics** section.</span></span>


## <a name="create-clusters"></a><span data-ttu-id="ebffa-118">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="ebffa-118">Create clusters</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="ebffa-119">HDInsight는 다양한 Hadoop 구성 요소에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-119">HDInsight works with a wide range of Hadoop components.</span></span> <span data-ttu-id="ebffa-120">검증되어 지원되는 구성 요소 목록은 [Azure HDInsight에 포함된 Hadoop 버전](hdinsight-component-versioning.md)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebffa-120">For the list of the components that have been verified and supported, see [What version of Hadoop is in Azure HDInsight](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="ebffa-121">클러스터 만들기에 대한 일반적인 정보는 [HDInsight에서 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebffa-121">For the general cluster creation information, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

### <a name="access-control-requirements"></a><span data-ttu-id="ebffa-122">액세스 제어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="ebffa-122">Access control requirements</span></span>

<span data-ttu-id="ebffa-123">HDInsight 클러스터를 만들 때 Azure 구독을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-123">You must specify an Azure subscription when you create an HDInsight cluster.</span></span> <span data-ttu-id="ebffa-124">새 Azure 리소스 그룹 또는 기존 리소스 그룹에서 이 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-124">This cluster can be created in either a new Azure Resource group or an existing Resource group.</span></span> <span data-ttu-id="ebffa-125">다음 단계를 사용하여 HDInsight 클러스터를 만들기 위한 권한을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-125">You can use the following steps to verify your permissions for creating HDInsight clusters:</span></span>

- <span data-ttu-id="ebffa-126">기존 리소스 그룹을 사용하려면</span><span class="sxs-lookup"><span data-stu-id="ebffa-126">To use an existing resource group.</span></span>

    1. <span data-ttu-id="ebffa-127">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-127">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
    2. <span data-ttu-id="ebffa-128">왼쪽 메뉴에서 **리소스 그룹**을 클릭하여 리소스 그룹을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-128">Click **Resource groups** from the left menu to list the resource groups.</span></span>
    3. <span data-ttu-id="ebffa-129">HDInsight 클러스터를 만드는 데 사용할 리소스 그룹을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-129">Click the resource group you want to use for creating your HDInsight cluster.</span></span>
    4. <span data-ttu-id="ebffa-130">**액세스 제어(IAM)**를 클릭하고 사용자(또는 사용자가 속하는 그룹)에 리소스 그룹에 대한 참여자 액세스 권한 이상이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-130">Click **Access control (IAM)**, and verify that you (or a group that you belong to) have at least the Contributor access to the resource group.</span></span>

- <span data-ttu-id="ebffa-131">새 리소스 그룹을 만들려면</span><span class="sxs-lookup"><span data-stu-id="ebffa-131">To create a new resource group</span></span>

    1. <span data-ttu-id="ebffa-132">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-132">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
    2. <span data-ttu-id="ebffa-133">왼쪽 메뉴에서 **구독**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-133">Click **Subscription** from the left menu.</span></span> <span data-ttu-id="ebffa-134">노란색 키 아이콘이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-134">It has a yellow key icon.</span></span> <span data-ttu-id="ebffa-135">구독의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-135">You shall see a list of subscriptions.</span></span>
    3. <span data-ttu-id="ebffa-136">클러스터를 만드는 데 사용할 구독을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-136">Click the subscription that you use to create clusters.</span></span> 
    4. <span data-ttu-id="ebffa-137">**내 사용 권한**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-137">Click **My permissions**.</span></span>  <span data-ttu-id="ebffa-138">구독에 [역할](../active-directory/role-based-access-control-what-is.md#built-in-roles)이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-138">It shows your [role](../active-directory/role-based-access-control-what-is.md#built-in-roles) on the subscription.</span></span> <span data-ttu-id="ebffa-139">HDInsight 클러스터를 만들기 위해서는 참여자 액세스 권한 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-139">You need at least Contributor access to create HDInsight cluster.</span></span>

<span data-ttu-id="ebffa-140">NoRegisteredProviderFound 오류 또는 MissingSubscriptionRegistration 오류가 발생하면 [Azure 리소스 관리자를 사용한 일반적인 Azure 배포 오류 해결](../azure-resource-manager/resource-manager-common-deployment-errors.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebffa-140">If you receive the NoRegisteredProviderFound error or the MissingSubscriptionRegistration error, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](../azure-resource-manager/resource-manager-common-deployment-errors.md).</span></span>

## <a name="list-and-show-clusters"></a><span data-ttu-id="ebffa-141">클러스터 나열 및 표시</span><span class="sxs-lookup"><span data-stu-id="ebffa-141">List and show clusters</span></span>
1. <span data-ttu-id="ebffa-142">[https://portal.azure.com](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-142">Sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ebffa-143">왼쪽 메뉴에서 **HDInsight 클러스터** 를 클릭하여 기존 클러스터를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-143">Click **HDInsight Clusters** from the left menu to list the existing clusters.</span></span>
3. <span data-ttu-id="ebffa-144">클러스터 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-144">Click the cluster name.</span></span> <span data-ttu-id="ebffa-145">클러스터 목록이 긴 경우 페이지 상단의 필터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-145">If the cluster list is long, you can use filter on the top of the page.</span></span>
4. <span data-ttu-id="ebffa-146">개요 페이지를 보려면 목록에서 클러스터를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-146">Click a cluster from the list to see the overview page:</span></span>

    ![Azure Portal HDInsight 클러스터 요점](./media/hdinsight-administer-use-portal-linux/hdinsight-essentials.png)

    * <span data-ttu-id="ebffa-148">**대시보드**: Linux 기반 클러스터용 Ambari Web인 클러스터 대시보드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-148">**Dashboard**: Opens the cluster dashboard, which is Ambari Web for Linux-based clusters.</span></span>
    * <span data-ttu-id="ebffa-149">**보안 셸**: SSH(보안 셸) 연결을 사용하여 클러스터에 연결하는 지침을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-149">**Secure Shell**: Shows the instructions to connect to the cluster using Secure Shell (SSH) connection.</span></span>
    * <span data-ttu-id="ebffa-150">**클러스터 크기 조정**: 이 클러스터의 작업자 노드 수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-150">**Scale Cluster**: Allows you to change the number of worker nodes for this cluster.</span></span>
    * <span data-ttu-id="ebffa-151">**삭제**: 클러스터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-151">**Delete**: Deletes the cluster.</span></span>
    * <span data-ttu-id="ebffa-152">**활동 로그**: 활동 로그를 표시하고 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-152">**Activity logs**: Show and query activity logs.</span></span>
    * <span data-ttu-id="ebffa-153">**Access Control(IAM)**: 역할 할당을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-153">**Access control (IAM)**: Use role assignments.</span></span>  <span data-ttu-id="ebffa-154">[역할 할당을 사용하여 Azure 구독 리소스에 대한 액세스 관리](../active-directory/role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebffa-154">See [Use role assignments to manage access to your Azure subscription resources](../active-directory/role-based-access-control-configure.md).</span></span>
    * <span data-ttu-id="ebffa-155">**태그**: 태그를 사용하면 Cloud Services의 사용자 지정 분류를 정의하기 위한 키/값 쌍을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-155">**Tags**: Allows you to set key/value pairs to define a custom taxonomy of your cloud services.</span></span> <span data-ttu-id="ebffa-156">예를 들어 **project**라는 키를 만든 다음 특정 프로젝트와 연결된 모든 서비스에 공통 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-156">For example, you may create a key named **project**, and then use a common value for all services associated with a specific project.</span></span>
    * <span data-ttu-id="ebffa-157">**문제 진단 및 해결**: 문제 해결 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-157">**Diagnose and solve problems**: Display troubleshooting information.</span></span>
    * <span data-ttu-id="ebffa-158">**잠금**: 클러스터가 수정되거나 삭제되지 않도록 잠금을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-158">**Locks**: Add lock to prevent the cluster being modified or deleted.</span></span>
    * <span data-ttu-id="ebffa-159">**자동화 스크립트**: 클러스터에 대한 Azure Resource Manager 템플릿을 표시하고 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-159">**Automation script**: Display and export the Azure Resource Manager template for the cluster.</span></span> <span data-ttu-id="ebffa-160">현재는 Azure Storage 계정만 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-160">Currently, you can only export the dependent Azure storage account.</span></span> <span data-ttu-id="ebffa-161">[Azure Resource Manager 템플릿을 사용하여 HDInsight의 Linux 기반 Hadoop 클러스터 만들기](hdinsight-hadoop-create-linux-clusters-arm-templates.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebffa-161">See [Create Linux-based Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md).</span></span>
    * <span data-ttu-id="ebffa-162">**빠른 시작**: HDInsight를 사용하여 시작하는 데 도움이 되는 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-162">**Quick Start**:  Displays information that helps you get started using HDInsight.</span></span>
    * <span data-ttu-id="ebffa-163">**HDInsight용 도구**: HDInsight 관련 도구에 대한 도움말 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-163">**Tools for HDInsight**: Help information for HDInsight related tools.</span></span>
    * <span data-ttu-id="ebffa-164">**클러스터 로그인**: 클러스터 로그인 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-164">**Cluster Login**: Display the cluster login information.</span></span>
    * <span data-ttu-id="ebffa-165">**구독 코어 사용량**: 구독에 사용된 코어 및 사용 가능한 코어를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-165">**Subscription Core Usage**: Display the used and available cores for your subscription.</span></span>
    * <span data-ttu-id="ebffa-166">**클러스터 크기 조정**: 클러스터 작업자 노드의 수를 늘리거나 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-166">**Scale Cluster**: Increase and decrease the number of cluster worker nodes.</span></span> <span data-ttu-id="ebffa-167">[클러스터 크기 조정](hdinsight-administer-use-management-portal.md#scale-clusters)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebffa-167">See[Scale clusters](hdinsight-administer-use-management-portal.md#scale-clusters).</span></span>
    * <span data-ttu-id="ebffa-168">**보안 셸**: SSH(보안 셸) 연결을 사용하여 클러스터에 연결하는 지침을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-168">**Secure Shell**: Shows the instructions to connect to the cluster using Secure Shell (SSH) connection.</span></span> <span data-ttu-id="ebffa-169">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebffa-169">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
    * <span data-ttu-id="ebffa-170">**HDInsight 파트너**: 현재 HDInsight 파트너를 추가/제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-170">**HDInsight Partner**: Add/remove the current HDInsight Partner.</span></span>
    * <span data-ttu-id="ebffa-171">**외부 Metastore**: Hive 및 Oozie Metastore를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-171">**External Metastores**: View the Hive and Oozie metastores.</span></span> <span data-ttu-id="ebffa-172">Metastore는 클러스터 생성 과정 중에만 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-172">The metastores can only be configured during the cluster creation process.</span></span> <span data-ttu-id="ebffa-173">[Hive/Oozie metastore 사용](hdinsight-hadoop-provision-linux-clusters.md#use-hiveoozie-metastore)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebffa-173">See [use Hive/Oozie metastore](hdinsight-hadoop-provision-linux-clusters.md#use-hiveoozie-metastore).</span></span>
    * <span data-ttu-id="ebffa-174">**스크립트 작업**: 클러스터에서 Bash 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-174">**Script Actions**: Run Bash scripts on the cluster.</span></span> <span data-ttu-id="ebffa-175">[스크립트 작업을 사용하여 Linux 기반 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebffa-175">See [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
    * <span data-ttu-id="ebffa-176">**응용 프로그램**: HDInsight 응용 프로그램을 추가/제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-176">**Applications**: Add/remove HDInsight applications.</span></span>  <span data-ttu-id="ebffa-177">[사용자 지정 HDInsight 응용 프로그램 설치](hdinsight-apps-install-custom-applications.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebffa-177">See [Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md).</span></span>
    * <span data-ttu-id="ebffa-178">**속성**: 클러스터 속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-178">**Properties**: View the cluster properties.</span></span>
    * <span data-ttu-id="ebffa-179">**저장소 계정**: 저장소 계정 및 키를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-179">**Storage accounts**: View the storage accounts and the keys.</span></span> <span data-ttu-id="ebffa-180">저장소 계정은 클러스터를 만드는 과정에서 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-180">The storage accounts are configured during the cluster creation process.</span></span>
    * <span data-ttu-id="ebffa-181">**클러스터 AAD ID**:</span><span class="sxs-lookup"><span data-stu-id="ebffa-181">**Cluster AAD Identity**:</span></span>
    * <span data-ttu-id="ebffa-182">**새 지원 요청**: Microsoft 지원에 지원 티켓을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-182">**New support request**: Allows you to create a support ticket with Microsoft support.</span></span>
    
6. <span data-ttu-id="ebffa-183">**속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-183">Click **Properties**:</span></span>

    <span data-ttu-id="ebffa-184">속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-184">The properties are:</span></span>

   * <span data-ttu-id="ebffa-185">**호스트 이름**: 클러스터 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-185">**Hostname**: Cluster name.</span></span>
   * <span data-ttu-id="ebffa-186">**클러스터 URL**.</span><span class="sxs-lookup"><span data-stu-id="ebffa-186">**Cluster URL**.</span></span> <span data-ttu-id="ebffa-187">Ambari 웹 인터페이스에 대한 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-187">The URL for the Ambari web interface.</span></span>
   * <span data-ttu-id="ebffa-188">**상태**: 중단됨, 수락됨, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, 운영, 실행 중, 오류, 삭제 중, 삭제됨, 시간 초과됨, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-188">**Status**: Include Aborted, Accepted, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, Operational, Running, Error, Deleting, Deleted, Timedout, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization</span></span>
   * <span data-ttu-id="ebffa-189">**지역**: Azure 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-189">**Region**: Azure location.</span></span> <span data-ttu-id="ebffa-190">지원되는 Azure 위치를 보려면, **HDInsight 가격** 의 [지역](https://azure.microsoft.com/pricing/details/hdinsight/)드롭다운 목록 상자를 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="ebffa-190">For a list of supported Azure locations, see the **Region** dropdown list box on [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>
   * <span data-ttu-id="ebffa-191">**만든 날짜**</span><span class="sxs-lookup"><span data-stu-id="ebffa-191">**Date created**.</span></span>
   * <span data-ttu-id="ebffa-192">**운영 체제**: **Windows** 또는 **Linux**입니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-192">**Operating system**: Either **Windows** or **Linux**.</span></span>
   * <span data-ttu-id="ebffa-193">**형식**: Hadoop, HBase, Storm, Spark.</span><span class="sxs-lookup"><span data-stu-id="ebffa-193">**Type**: Hadoop, HBase, Storm, Spark.</span></span>
   * <span data-ttu-id="ebffa-194">**버전**.</span><span class="sxs-lookup"><span data-stu-id="ebffa-194">**Version**.</span></span> <span data-ttu-id="ebffa-195">[HDInsight 버전](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="ebffa-195">See [HDInsight versions](hdinsight-component-versioning.md)</span></span>
   * <span data-ttu-id="ebffa-196">**구독**: 구독 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-196">**Subscription**: Subscription name.</span></span>
   * <span data-ttu-id="ebffa-197">**기본 데이터 원본**: 기본 클러스터 파일 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-197">**Default data source**: The default cluster file system.</span></span>
   * <span data-ttu-id="ebffa-198">**작업자 노드 크기**</span><span class="sxs-lookup"><span data-stu-id="ebffa-198">**Worker nodes size**.</span></span>
   * <span data-ttu-id="ebffa-199">**헤드 노드 크기**</span><span class="sxs-lookup"><span data-stu-id="ebffa-199">**Head node size**.</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="ebffa-200">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="ebffa-200">Delete clusters</span></span>
<span data-ttu-id="ebffa-201">클러스터 삭제는 기본 저장소 계정이나 연결된 저장소 계정을 삭제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-201">Deleting a cluster does not delete the default storage account or any linked storage accounts.</span></span> <span data-ttu-id="ebffa-202">동일한 저장소 계정과 동일한 Metastore를 사용하여 클러스터를 다시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-202">You can re-create the cluster by using the same storage accounts and the same metastores.</span></span> <span data-ttu-id="ebffa-203">클러스터를 다시 만들 때 새 기본 Blob 컨테이너를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-203">It is recommended to use a new default Blob container when you re-create the cluster.</span></span>

1. <span data-ttu-id="ebffa-204">[포털][azure-portal]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-204">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="ebffa-205">왼쪽 메뉴에서 **HDInsight 클러스터** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-205">Click **HDInsight Clusters** from the left menu.</span></span> <span data-ttu-id="ebffa-206">**HDInsight 클러스터**가 표시되지 않으면 먼저 **추가 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-206">If you don't see **HDInsight Clusters**, click **More services** first.</span></span>
3. <span data-ttu-id="ebffa-207">삭제할 클러스터를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-207">Click the cluster that you want to delete.</span></span>
4. <span data-ttu-id="ebffa-208">상단 메뉴에서 **삭제** 를 클릭하고 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-208">Click **Delete** from the top menu, and then follow the instructions.</span></span>

<span data-ttu-id="ebffa-209">참고 항목: [클러스터 일시 중지/종료](#pauseshut-down-clusters)</span><span class="sxs-lookup"><span data-stu-id="ebffa-209">See also [Pause/shut down clusters](#pauseshut-down-clusters).</span></span>

## <a name="add-additional-storage-accounts"></a><span data-ttu-id="ebffa-210">추가 저장소 계정 추가</span><span class="sxs-lookup"><span data-stu-id="ebffa-210">Add additional storage accounts</span></span>

<span data-ttu-id="ebffa-211">클러스터를 만든 후 Azure Storage 계정 및 Azure Data Lake Store 계정을 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-211">You can add additional Azure Storage accounts and Azure Data Lake Store accounts after a cluster is created.</span></span> <span data-ttu-id="ebffa-212">자세한 내용은 [HDInsight에 추가 저장소 계정 추가](./hdinsight-hadoop-add-storage.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebffa-212">For more information, see [Add additional storage accounts to HDInsight](./hdinsight-hadoop-add-storage.md).</span></span>

## <a name="scale-clusters"></a><span data-ttu-id="ebffa-213">클러스터 크기 조정</span><span class="sxs-lookup"><span data-stu-id="ebffa-213">Scale clusters</span></span>
<span data-ttu-id="ebffa-214">클러스터 크기 조정 기능을 사용하여 클러스터를 다시 생성하지 않고 Azure HDInsight에서 실행되는 클러스터에서 사용되는 작업자 노드 수를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-214">The cluster scaling feature allows you to change the number of worker nodes used by a cluster that is running in Azure HDInsight without having to re-create the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="ebffa-215">HDInsight 버전 3.1.3 이상을 사용하는 클러스터만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-215">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="ebffa-216">클러스터 버전을 알 수 없는 경우 속성 페이지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-216">If you are unsure of the version of your cluster, you can check the Properties page.</span></span>  <span data-ttu-id="ebffa-217">[클러스터 나열 및 표시](#list-and-show-clusters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebffa-217">See [List and show clusters](#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="ebffa-218">HDInsight에서 지원되는 클러스터의 각 형식에 대한 데이터 노드 수를 변경하는 영향은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-218">The impact of changing the number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="ebffa-219">Hadoop은</span><span class="sxs-lookup"><span data-stu-id="ebffa-219">Hadoop</span></span>

    <span data-ttu-id="ebffa-220">모든 보류 중인 또는 실행 중인 작업에 영향을 주지 않고 실행되는 Hadoop 클러스터의 작업자 노드 수를 원활하게 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-220">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="ebffa-221">작업이 진행 중인 동안에 새 작업을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-221">New jobs can also be submitted while the operation is in progress.</span></span> <span data-ttu-id="ebffa-222">크기 조정 작업의 오류는 정상적으로 처리되므로 클러스터는 항상 기능 상태로 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-222">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span></span>

    <span data-ttu-id="ebffa-223">데이터 노드 수를 줄여 Hadoop 클러스터를 축소하면 클러스터의 서비스 중 일부가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-223">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span></span> <span data-ttu-id="ebffa-224">그러면 실행 중인 작업과 보류 중인 작업이 크기 조정 작업을 완료하지 못하고 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-224">This behavior causes all running and pending jobs to fail at the completion of the scaling operation.</span></span> <span data-ttu-id="ebffa-225">그러나 작업이 완료되면 작업을 다시 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-225">You can, however, resubmit the jobs once the operation is complete.</span></span>
* <span data-ttu-id="ebffa-226">HBase</span><span class="sxs-lookup"><span data-stu-id="ebffa-226">HBase</span></span>

    <span data-ttu-id="ebffa-227">HBase 클러스터가 실행 중인 동안 데이터 노드를 원활하게 추가하거나 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-227">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span></span> <span data-ttu-id="ebffa-228">지역 서버는 크기 조정 작업을 완료하는 몇 분 안에 자동으로 균형을 맞춥니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-228">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span></span> <span data-ttu-id="ebffa-229">그러나 클러스터의 헤드 노드에 로그인한 다음 명령 프롬프트 창에서 다음 명령을 실행하여 자동으로 지역 서버의 균형을 맞출 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-229">However, you can also manually balance the regional servers by logging in to the headnode of cluster and running the following commands from a command prompt window:</span></span>

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer

    <span data-ttu-id="ebffa-230">HBase 셸 사용에 대한 자세한 내용은 []을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebffa-230">For more information on using the HBase shell, see []</span></span>
* <span data-ttu-id="ebffa-231">Storm</span><span class="sxs-lookup"><span data-stu-id="ebffa-231">Storm</span></span>

    <span data-ttu-id="ebffa-232">실행 중인 동안 Storm 클러스터에 데이터 노드를 원활하게 추가하거나 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-232">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span></span> <span data-ttu-id="ebffa-233">하지만 크기 조정 작업이 성공적으로 완료되면 다시 토폴로지 균형을 조정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-233">But after a successful completion of the scaling operation, you will need to rebalance the topology.</span></span>

    <span data-ttu-id="ebffa-234">다음 두 가지 방법으로 사용하여 균형을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-234">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="ebffa-235">Storm 웹 UI</span><span class="sxs-lookup"><span data-stu-id="ebffa-235">Storm web UI</span></span>
  * <span data-ttu-id="ebffa-236">명령줄 인터페이스(CLI) 도구</span><span class="sxs-lookup"><span data-stu-id="ebffa-236">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="ebffa-237">자세한 내용은 [Apache Storm 설명서](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebffa-237">Refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="ebffa-238">Storm 웹 UI는 HDInsight 클러스터에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-238">The Storm web UI is available on the HDInsight cluster:</span></span>

    ![HDInsight Storm 규모 균형 재조정](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster-storm-rebalance.png)

    <span data-ttu-id="ebffa-240">다음은 CLI 명령을 사용하여 Storm 토폴로지 균형을 다시 조정하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-240">Here is an example how to use the CLI command to rebalance the Storm topology:</span></span>

        ## Reconfigure the topology "mytopology" to use 5 worker processes,
        ## the spout "blue-spout" to use 3 executors, and
        ## the bolt "yellow-bolt" to use 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="ebffa-241">**클러스터 크기를 조정하려면**</span><span class="sxs-lookup"><span data-stu-id="ebffa-241">**To scale clusters**</span></span>

1. <span data-ttu-id="ebffa-242">[포털][azure-portal]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-242">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="ebffa-243">왼쪽 메뉴에서 **HDInsight 클러스터** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-243">Click **HDInsight Clusters** from the left menu.</span></span>
3. <span data-ttu-id="ebffa-244">크기 조정하려는 클러스터를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-244">Click the cluster you want to scale.</span></span>
3. <span data-ttu-id="ebffa-245">**클러스터 크기 조정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-245">Click **Scale Cluster**.</span></span>
4. <span data-ttu-id="ebffa-246">**작업자 노드 수**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-246">Enter **Number of Worker nodes**.</span></span> <span data-ttu-id="ebffa-247">클러스터 노드 수에 대한 제한은 Azure 구독에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-247">The limit on the number of cluster nodes varies among Azure subscriptions.</span></span> <span data-ttu-id="ebffa-248">제한을 늘리려면 청구 지원 팀에 문의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-248">You can contact billing support to increase the limit.</span></span>  <span data-ttu-id="ebffa-249">비용 정보는 노드 수에 대한 변경 내용을 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-249">The cost information reflects the changes you have made to the number of nodes.</span></span>

    ![HDinsight Hadoop Hbase Storm Spark 크기 조정](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster.png)

## <a name="pauseshut-down-clusters"></a><span data-ttu-id="ebffa-251">클러스터 일시 중지/종료</span><span class="sxs-lookup"><span data-stu-id="ebffa-251">Pause/shut down clusters</span></span>

<span data-ttu-id="ebffa-252">대부분의 Hadoop 작업은 이따금 실행되는 일괄 처리 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-252">Most of Hadoop jobs are batch jobs that are only run occasionally.</span></span> <span data-ttu-id="ebffa-253">대부분의 Hadoop 클러스터는 프로세스에 사용되지 않는 기간이 깁니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-253">For most Hadoop clusters, there are large periods of time that the cluster is not being used for processing.</span></span> <span data-ttu-id="ebffa-254">HDInsight를 사용하면 데이터가 Azure 저장소에 저장되기 때문에 클러스터를 사용하지 않을 때 안전하게 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-254">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span>
<span data-ttu-id="ebffa-255">HDInsight 클러스터를 사용하지 않는 기간에도 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-255">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="ebffa-256">클러스터에 대한 요금이 저장소에 대한 요금보다 몇 배 더 많기 때문에, 클러스터를 사용하지 않을 때는 삭제하는 것이 경제적인 면에서 더 합리적입니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-256">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span></span>

<span data-ttu-id="ebffa-257">프로세스를 프로그래밍할 수 있는 방법은 다양합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-257">There are many ways you can program the process:</span></span>

* <span data-ttu-id="ebffa-258">사용자 Azure 데이터 팩터리.</span><span class="sxs-lookup"><span data-stu-id="ebffa-258">User Azure Data Factory.</span></span> <span data-ttu-id="ebffa-259">주문형 HDInsight 연결된 서비스 만들기는 [Azure Data Factory를 사용하여 HDInsight에서 주문형 Linux 기반 Hadoop 클러스터 만들기](hdinsight-hadoop-create-linux-clusters-adf.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebffa-259">See [Create on-demand Linux-based Hadoop clusters in HDInsight using Azure Data Factory](hdinsight-hadoop-create-linux-clusters-adf.md) for creating on-demand HDInsight linked services.</span></span>
* <span data-ttu-id="ebffa-260">Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="ebffa-260">Use Azure PowerShell.</span></span>  <span data-ttu-id="ebffa-261">[비행 지연 데이터 분석](hdinsight-analyze-flight-delay-data.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebffa-261">See [Analyze flight delay data](hdinsight-analyze-flight-delay-data.md).</span></span>
* <span data-ttu-id="ebffa-262">Azure CLI 사용</span><span class="sxs-lookup"><span data-stu-id="ebffa-262">Use Azure CLI.</span></span> <span data-ttu-id="ebffa-263">[Azure CLI를 사용하여 HDInsight 클러스터 관리](hdinsight-administer-use-command-line.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebffa-263">See [Manage HDInsight clusters using Azure CLI](hdinsight-administer-use-command-line.md).</span></span>
* <span data-ttu-id="ebffa-264">HDInsight .NET SDK 사용</span><span class="sxs-lookup"><span data-stu-id="ebffa-264">Use HDInsight .NET SDK.</span></span> <span data-ttu-id="ebffa-265">[Hadoop 작업 제출](hdinsight-submit-hadoop-jobs-programmatically.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebffa-265">See [Submit Hadoop jobs](hdinsight-submit-hadoop-jobs-programmatically.md).</span></span>

<span data-ttu-id="ebffa-266">가격 정보는 [HDInsight 가격](https://azure.microsoft.com/pricing/details/hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebffa-266">For the pricing information, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span> <span data-ttu-id="ebffa-267">포털에서 클러스터를 삭제하려면 [클러스터 삭제](#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="ebffa-267">To delete a cluster from the Portal, see [Delete clusters](#delete-clusters)</span></span>


## <a name="upgrade-clusters"></a><span data-ttu-id="ebffa-268">클러스터 업그레이드</span><span class="sxs-lookup"><span data-stu-id="ebffa-268">Upgrade clusters</span></span>

<span data-ttu-id="ebffa-269">[HDInsight 클러스터를 최신 버전으로 업그레이드](./hdinsight-upgrade-cluster.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebffa-269">See [Upgrade HDInsight cluster to a newer version](./hdinsight-upgrade-cluster.md).</span></span>

## <a name="change-passwords"></a><span data-ttu-id="ebffa-270">암호 변경</span><span class="sxs-lookup"><span data-stu-id="ebffa-270">Change passwords</span></span>
<span data-ttu-id="ebffa-271">HDInsight 클러스터마다 두 개의 사용자 계정이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-271">An HDInsight cluster can have two user accounts.</span></span> <span data-ttu-id="ebffa-272">HDInsight 클러스터 사용자 이름(HTTP</span><span class="sxs-lookup"><span data-stu-id="ebffa-272">The HDInsight cluster user account (A.K.A.</span></span> <span data-ttu-id="ebffa-273">사용자 계정이라고도 함) 및 SSH 사용자 계정은 만들기 프로세스 중에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-273">HTTP user account) and the SSH user account are created during the creation process.</span></span> <span data-ttu-id="ebffa-274">Ambari 웹 UI를 사용하여 클러스터 사용자 계정의 사용자 이름 및 암호를 변경할 수 있으며 스크립트 작업을 사용하여 SSH 사용자 계정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-274">You can use the Ambari web UI to change the cluster user account username and password, and script actions to change the SSH user account</span></span>

### <a name="change-the-cluster-user-password"></a><span data-ttu-id="ebffa-275">클러스터 사용자 암호 변경</span><span class="sxs-lookup"><span data-stu-id="ebffa-275">Change the cluster user password</span></span>
<span data-ttu-id="ebffa-276">Ambari 웹 UI를 사용하여 클러스터 사용자 암호를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-276">You can use the Ambari Web UI to change the Cluster user password.</span></span> <span data-ttu-id="ebffa-277">Ambari에 로그인하려면 기존 클러스터 사용자 이름 및 암호를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-277">To log in to Ambari, you must use the existing cluster username and password.</span></span>

> [!NOTE]
> <span data-ttu-id="ebffa-278">클러스터 사용자(관리자) 암호를 변경하면 이 클러스터를 실행하는 스크립트 작업에 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-278">Changing the cluster user (admin) password may cause script actions ran against this cluster to fail.</span></span> <span data-ttu-id="ebffa-279">작업자 노드를 대상으로 하는 지속적인 스크립트 작업이 있는 경우 이러한 스크립트는 작업의 크기 조정을 통해 클러스터에 노드를 추가할 때 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-279">If you have any persisted script actions that target worker nodes, these scripts may fail when you add nodes to the cluster through resize operations.</span></span> <span data-ttu-id="ebffa-280">스크립트 작업에 대한 자세한 내용은 [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebffa-280">For more information on script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
>
>

1. <span data-ttu-id="ebffa-281">HDInsight 클러스터 사용자 자격 증명을 사용하여 Ambari 웹 UI에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-281">Sign in to the Ambari Web UI using the HDInsight cluster user credentials.</span></span> <span data-ttu-id="ebffa-282">기본 사용자 이름은 **admin**입니다. URL은 **https://&lt;HDInsight Cluster Name>azurehdinsight.net**입니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-282">The default username is **admin**. The URL is **https://&lt;HDInsight Cluster Name>azurehdinsight.net**.</span></span>
2. <span data-ttu-id="ebffa-283">위쪽 메뉴에서 **관리자** 를 클릭한 다음 "Ambari 관리"를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-283">Click **Admin** from the top menu, and then click "Manage Ambari".</span></span>
3. <span data-ttu-id="ebffa-284">왼쪽 메뉴에서 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-284">From the left menu, click **Users**.</span></span>
4. <span data-ttu-id="ebffa-285">**Admin**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-285">Click **Admin**.</span></span>
5. <span data-ttu-id="ebffa-286">**암호 변경**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-286">Click **Change Password**.</span></span>

<span data-ttu-id="ebffa-287">Ambari는 클러스터의 모든 노드에 대해 암호를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-287">Ambari then changes the password on all nodes in the cluster.</span></span>

### <a name="change-the-ssh-user-password"></a><span data-ttu-id="ebffa-288">SSH 사용자 암호 변경</span><span class="sxs-lookup"><span data-stu-id="ebffa-288">Change the SSH user password</span></span>
1. <span data-ttu-id="ebffa-289">텍스트 편집기를 사용하여 다음 텍스트를 **changepassword.sh**라는 파일로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-289">Using a text editor, save the following text as a file named **changepassword.sh**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="ebffa-290">줄 끝으로 LF를 사용하는 편집기를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-290">You must use an editor that uses LF as the line ending.</span></span> <span data-ttu-id="ebffa-291">편집기에서 CRLF를 사용하는 경우 스크립트가 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-291">If the editor uses CRLF, then the script does not work.</span></span>
   >
   >

        #! /bin/bash
        USER=$1
        PASS=$2

        usermod --password $(echo $PASS | openssl passwd -1 -stdin) $USER
2. <span data-ttu-id="ebffa-292">HTTP 또는 HTTPS 주소를 사용하여 HDInsight에서 액세스할 수 있는 저장소 위치에 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-292">Upload the file to a storage location that can be accessed from HDInsight using an HTTP or HTTPS address.</span></span> <span data-ttu-id="ebffa-293">예를 들어 OneDrive 또는 Azure Blob 저장소와 같은 공용 파일 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-293">For example, a public file store such as OneDrive or Azure Blob storage.</span></span> <span data-ttu-id="ebffa-294">다음 단계에서 이 URI가 필요하므로 URI(HTTP 또는 HTTPS 주소)를 파일에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-294">Save the URI (HTTP or HTTPS address) to the file, as this URI is needed in the next step.</span></span>
3. <span data-ttu-id="ebffa-295">Azure Portal에서 **HDInsight 클러스터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-295">From the Azure portal, click **HDInsight Clusters**.</span></span>
4. <span data-ttu-id="ebffa-296">HDInsight 클러스터를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-296">Click your HDInsight cluster.</span></span>
4. <span data-ttu-id="ebffa-297">**스크립트 작업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-297">Click **Script Actions**.</span></span>
4. <span data-ttu-id="ebffa-298">**스크립트 동작** 블레이드에서 **새로운 항목 제출**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-298">From the **Script Actions** blade, select **Submit New**.</span></span> <span data-ttu-id="ebffa-299">**스크립트 동작 제출** 블레이드가 나타나면 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-299">When the **Submit script action** blade appears, enter the following information:</span></span>

   | <span data-ttu-id="ebffa-300">필드</span><span class="sxs-lookup"><span data-stu-id="ebffa-300">Field</span></span> | <span data-ttu-id="ebffa-301">값</span><span class="sxs-lookup"><span data-stu-id="ebffa-301">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="ebffa-302">Name</span><span class="sxs-lookup"><span data-stu-id="ebffa-302">Name</span></span> |<span data-ttu-id="ebffa-303">SSH 암호 변경</span><span class="sxs-lookup"><span data-stu-id="ebffa-303">Change ssh password</span></span> |
   | <span data-ttu-id="ebffa-304">Bash 스크립트 URI</span><span class="sxs-lookup"><span data-stu-id="ebffa-304">Bash script URI</span></span> |<span data-ttu-id="ebffa-305">Changepassword.sh 파일에 대한 URI</span><span class="sxs-lookup"><span data-stu-id="ebffa-305">The URI to the changepassword.sh file</span></span> |
   | <span data-ttu-id="ebffa-306">노드(헤드, 작업자, Nimbus, 감독자, Zookeeper 등)</span><span class="sxs-lookup"><span data-stu-id="ebffa-306">Nodes (Head, Worker, Nimbus, Supervisor, Zookeeper, etc.)</span></span> |<span data-ttu-id="ebffa-307">나열된 모든 노드 형식에 대한 ✓</span><span class="sxs-lookup"><span data-stu-id="ebffa-307">✓ for all node types listed</span></span> |
   | <span data-ttu-id="ebffa-308">매개 변수</span><span class="sxs-lookup"><span data-stu-id="ebffa-308">Parameters</span></span> |<span data-ttu-id="ebffa-309">SSH 사용자 이름 및 새 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-309">Enter the SSH user name and then the new password.</span></span> <span data-ttu-id="ebffa-310">사용자 이름과 암호 사이에 공백이 하나 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-310">There should be one space between the user name and the password.</span></span> |
   | <span data-ttu-id="ebffa-311">이 스크립트 작업을 유지...</span><span class="sxs-lookup"><span data-stu-id="ebffa-311">Persist this script action ...</span></span> |<span data-ttu-id="ebffa-312">이 필드는 선택 취소로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-312">Leave this field unchecked.</span></span> |
5. <span data-ttu-id="ebffa-313">**만들기**를 선택하여 스크립트를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-313">Select **Create** to apply the script.</span></span> <span data-ttu-id="ebffa-314">스크립트가 완료되면 새 암호와 함께 SSH를 사용하여 클러스터에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-314">Once the script finishes, you are able to connect to the cluster using SSH with the new password.</span></span>

## <a name="grantrevoke-access"></a><span data-ttu-id="ebffa-315">액세스 권한 부여/해지</span><span class="sxs-lookup"><span data-stu-id="ebffa-315">Grant/revoke access</span></span>
<span data-ttu-id="ebffa-316">HDInsight 클러스터에는 다음과 같은 HTTP 웹 서비스가 있습니다(이러한 모든 서비스에 RESTful 끝점이 있음).</span><span class="sxs-lookup"><span data-stu-id="ebffa-316">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="ebffa-317">ODBC</span><span class="sxs-lookup"><span data-stu-id="ebffa-317">ODBC</span></span>
* <span data-ttu-id="ebffa-318">JDBC</span><span class="sxs-lookup"><span data-stu-id="ebffa-318">JDBC</span></span>
* <span data-ttu-id="ebffa-319">Ambari</span><span class="sxs-lookup"><span data-stu-id="ebffa-319">Ambari</span></span>
* <span data-ttu-id="ebffa-320">Oozie</span><span class="sxs-lookup"><span data-stu-id="ebffa-320">Oozie</span></span>
* <span data-ttu-id="ebffa-321">Templeton</span><span class="sxs-lookup"><span data-stu-id="ebffa-321">Templeton</span></span>

<span data-ttu-id="ebffa-322">이러한 서비스에는 기본적으로 액세스 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-322">By default, these services are granted for access.</span></span> <span data-ttu-id="ebffa-323">[Azure CLI](hdinsight-administer-use-command-line.md#enabledisable-http-access-for-a-cluster) 및 [Azure PowerShell](hdinsight-administer-use-powershell.md#grantrevoke-access)을 사용하여 액세스 권한을 해지/부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-323">You can revoke/grant the access using [Azure CLI](hdinsight-administer-use-command-line.md#enabledisable-http-access-for-a-cluster) and [Azure PowerShell](hdinsight-administer-use-powershell.md#grantrevoke-access).</span></span>

## <a name="find-the-subscription-id"></a><span data-ttu-id="ebffa-324">구독 ID 찾기</span><span class="sxs-lookup"><span data-stu-id="ebffa-324">Find the subscription ID</span></span>

<span data-ttu-id="ebffa-325">**Azure 구독 ID를 찾으려면**</span><span class="sxs-lookup"><span data-stu-id="ebffa-325">**To find your Azure subscription IDs**</span></span>

1. <span data-ttu-id="ebffa-326">[포털][azure-portal]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-326">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="ebffa-327">**구독**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-327">Click **Subscriptions**.</span></span> <span data-ttu-id="ebffa-328">각 구독에는 이름 및 ID가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-328">Each subscription has a name and an ID.</span></span>

<span data-ttu-id="ebffa-329">각 클러스터가 Azure 구독에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-329">Each cluster is tied to an Azure subscription.</span></span> <span data-ttu-id="ebffa-330">ID 구독은 클러스터 **필수** 타일에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-330">The subscription ID is shown on the cluster **Essential** tile.</span></span> <span data-ttu-id="ebffa-331">[클러스터 나열 및 표시](#list-and-show-clusters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebffa-331">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="find-the-resource-group"></a><span data-ttu-id="ebffa-332">리소스 그룹 찾기</span><span class="sxs-lookup"><span data-stu-id="ebffa-332">Find the resource group</span></span>
<span data-ttu-id="ebffa-333">Azure Resource Manager 모드에서는 각각의 HDInsight 클러스터가 Azure Resource Manager 그룹과 함께 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-333">In the Azure Resource Manager mode, each HDInsight cluster is created with an Azure Resource Manager group.</span></span> <span data-ttu-id="ebffa-334">클러스터가 속하는 Resource Manager 그룹이 아래 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-334">The Resource Manager group that a cluster belongs to appears in:</span></span>

* <span data-ttu-id="ebffa-335">클러스터 목록에 **리소스 그룹** 열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-335">The cluster list has a **Resource Group** column.</span></span>
* <span data-ttu-id="ebffa-336">클러스터 **Essential** 타일.</span><span class="sxs-lookup"><span data-stu-id="ebffa-336">Cluster **Essential** tile.</span></span>  

<span data-ttu-id="ebffa-337">[클러스터 나열 및 표시](#list-and-show-clusters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebffa-337">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="find-the-default-storage-account"></a><span data-ttu-id="ebffa-338">기본 저장소 계정 찾기</span><span class="sxs-lookup"><span data-stu-id="ebffa-338">Find the default storage account</span></span>
<span data-ttu-id="ebffa-339">각 HDInsight 클러스터에는 기본 저장소 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-339">Each HDInsight cluster has a default storage account.</span></span> <span data-ttu-id="ebffa-340">클러스터의 기본 저장소 계정 및 키는 **저장소 계정**에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-340">The default storage account and its keys for a cluster appears under **Storage Accounts**.</span></span> <span data-ttu-id="ebffa-341">[클러스터 나열 및 표시](#list-and-show-clusters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebffa-341">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="run-hive-queries"></a><span data-ttu-id="ebffa-342">Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="ebffa-342">Run Hive queries</span></span>
<span data-ttu-id="ebffa-343">Azure 포털에서 직접 Hive 작업을 실행할 수는 없지만 Ambari 웹 UI에서 Hive View를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-343">You cannot run Hive job directly from the Azure portal, but you can use the Hive View on Ambari Web UI.</span></span>

<span data-ttu-id="ebffa-344">**Ambari Hive View를 사용하여 Hive 쿼리를 실행하려면**</span><span class="sxs-lookup"><span data-stu-id="ebffa-344">**To run Hive queries using Ambari Hive View**</span></span>

1. <span data-ttu-id="ebffa-345">HDInsight 클러스터 사용자 자격 증명을 사용하여 Ambari 웹 UI에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-345">Sign in to the Ambari Web UI using the HDInsight cluster user credentials.</span></span> <span data-ttu-id="ebffa-346">기본 사용자 이름은 **admin**입니다. URL은 **https://&lt;HDInsight Cluster Name>azurehdinsight.net**입니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-346">The default username is **admin**. The URL is **https://&lt;HDInsight Cluster Name>azurehdinsight.net**.</span></span>
2. <span data-ttu-id="ebffa-347">다음 스크린샷에 표시된 것처럼 Hive View를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-347">Open Hive View as shown in the following screenshot:</span></span>  

    ![HDInsight Hive 보기](./media/hdinsight-administer-use-portal-linux/hdinsight-hive-view.png)
3. <span data-ttu-id="ebffa-349">위쪽 메뉴에서 **쿼리** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-349">Click **Query** from the top menu.</span></span>
4. <span data-ttu-id="ebffa-350">**쿼리 편집기**에서 Hive 쿼리를 입력한 다음 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-350">Enter a Hive query in **Query Editor**, and then click **Execute**.</span></span>

## <a name="monitor-jobs"></a><span data-ttu-id="ebffa-351">작업 모니터링</span><span class="sxs-lookup"><span data-stu-id="ebffa-351">Monitor jobs</span></span>
<span data-ttu-id="ebffa-352">[Ambari 웹 UI를 사용하여 HDInsight 클러스터 관리](hdinsight-hadoop-manage-ambari.md#monitoring)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebffa-352">See [Manage HDInsight clusters by using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md#monitoring).</span></span>

## <a name="browse-files"></a><span data-ttu-id="ebffa-353">파일 찾아보기</span><span class="sxs-lookup"><span data-stu-id="ebffa-353">Browse files</span></span>
<span data-ttu-id="ebffa-354">Azure 포털을 사용하여 기본 컨테이너의 콘텐츠를 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-354">Using the Azure portal, you can browse the content of the default container.</span></span>

1. <span data-ttu-id="ebffa-355">[https://portal.azure.com](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-355">Sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ebffa-356">왼쪽 메뉴에서 **HDInsight 클러스터** 를 클릭하여 기존 클러스터를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-356">Click **HDInsight Clusters** from the left menu to list the existing clusters.</span></span>
3. <span data-ttu-id="ebffa-357">클러스터 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-357">Click the cluster name.</span></span> <span data-ttu-id="ebffa-358">클러스터 목록이 긴 경우 페이지 상단의 필터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-358">If the cluster list is long, you can use filter on the top of the page.</span></span>
4. <span data-ttu-id="ebffa-359">클러스터 왼쪽 메뉴에서 **저장소 계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-359">Click **Storage Accounts** from the cluster left menu.</span></span>
5. <span data-ttu-id="ebffa-360">Storage 계정을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-360">Click a Storage account.</span></span>
7. <span data-ttu-id="ebffa-361">**Blob** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-361">Click the **Blobs** tile.</span></span>
8. <span data-ttu-id="ebffa-362">기본 컨테이너 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-362">Click the default container name.</span></span>

## <a name="monitor-cluster-usage"></a><span data-ttu-id="ebffa-363">클러스터 사용 현황 모니터링</span><span class="sxs-lookup"><span data-stu-id="ebffa-363">Monitor cluster usage</span></span>
<span data-ttu-id="ebffa-364">HDInsight 클러스터 블레이드의 **사용량** 섹션에는 HDInsight에서 사용하기 위해 구독에서 사용할 수 있는 코어 수뿐만 아니라 이 클러스터에 할당된 코어 수 및 이 클러스터 내에서 노드에 할당된 방법에 대한 정보도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-364">The **Usage** section of the HDInsight cluster blade displays information about the number of cores available to your subscription for use with HDInsight, as well as the number of cores allocated to this cluster and how they are allocated for the nodes within this cluster.</span></span> <span data-ttu-id="ebffa-365">[클러스터 나열 및 표시](#list-and-show-clusters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebffa-365">See [List and show clusters](#list-and-show-clusters).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ebffa-366">HDInsight 클러스터에 의해 제공되는 서비스를 모니터링하려면 Ambari 웹 또는 Ambari REST API를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-366">To monitor the services provided by the HDInsight cluster, you must use Ambari Web or the Ambari REST API.</span></span> <span data-ttu-id="ebffa-367">Ambari 사용에 대한 자세한 내용은 [Ambari를 사용하여 HDInsight 클러스터 관리](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="ebffa-367">For more information on using Ambari, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>
>
>

## <a name="connect-to-a-cluster"></a><span data-ttu-id="ebffa-368">클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="ebffa-368">Connect to a cluster</span></span>

* [<span data-ttu-id="ebffa-369">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="ebffa-369">Use Hive with HDInsight</span></span>](hdinsight-hadoop-use-hive-ambari-view.md)
* [<span data-ttu-id="ebffa-370">HDInsight와 함께 SSH 사용</span><span class="sxs-lookup"><span data-stu-id="ebffa-370">Use SSH with HDInsight</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)

## <a name="next-steps"></a><span data-ttu-id="ebffa-371">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ebffa-371">Next steps</span></span>
<span data-ttu-id="ebffa-372">이 문서에서는 몇 가지 기본 관리 함수에 대해 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="ebffa-372">In this article, you have learned some basic administative functions.</span></span> <span data-ttu-id="ebffa-373">자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebffa-373">To learn more, see the following articles:</span></span>

* [<span data-ttu-id="ebffa-374">Azure PowerShell을 사용하여 HDInsight 관리</span><span class="sxs-lookup"><span data-stu-id="ebffa-374">Administer HDInsight Using Azure PowerShell</span></span>](hdinsight-administer-use-powershell.md)
* [<span data-ttu-id="ebffa-375">Azure CLI를 사용하여 HDInsight 관리</span><span class="sxs-lookup"><span data-stu-id="ebffa-375">Administer HDInsight Using Azure CLI</span></span>](hdinsight-administer-use-command-line.md)
* [<span data-ttu-id="ebffa-376">HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="ebffa-376">Create HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="ebffa-377">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="ebffa-377">Use Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="ebffa-378">HDInsight에서 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="ebffa-378">Use Pig in HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="ebffa-379">HDInsight에서 Sqoop 사용</span><span class="sxs-lookup"><span data-stu-id="ebffa-379">Use Sqoop in HDInsight</span></span>](hdinsight-use-sqoop.md)
* [<span data-ttu-id="ebffa-380">Azure HDInsight 시작</span><span class="sxs-lookup"><span data-stu-id="ebffa-380">Get Started with Azure HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="ebffa-381">Azure HDInsight에 포함된 Hadoop 버전</span><span class="sxs-lookup"><span data-stu-id="ebffa-381">What version of Hadoop is in Azure HDInsight?</span></span>](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-portal-linux/hdinsight-hadoop-command-line.png "Hadoop 명령줄"
