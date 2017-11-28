---
title: "Azure 포털을 사용 하 여 HDInsight 클러스터를 aaaManage Hadoop | Microsoft Docs"
description: "자세한 내용은 방법 toocreate hello Azure 포털을 사용 하 여 HDInsight 클러스터를 관리 하 고 있습니다."
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
ms.openlocfilehash: c242d43d4ccea7cf1e7be19c3f3d7ed3c4f50918
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-hello-azure-portal"></a><span data-ttu-id="4d05e-103">Hello Azure 포털을 사용 하 여 HDInsight의 Hadoop 클러스터를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-103">Manage Hadoop clusters in HDInsight by using hello Azure portal</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="4d05e-104">Hello를 사용 하 여 [Azure 포털][azure-portal], Azure HDInsight의 Hadoop 클러스터를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-104">Using hello [Azure portal][azure-portal], you can manage Hadoop clusters in Azure HDInsight.</span></span> <span data-ttu-id="4d05e-105">다른 도구를 사용 하 여 HDInsight의 Hadoop 클러스터 관리에 대 한 내용은 hello 탭 선택기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-105">Use hello tab selector for information on managing Hadoop clusters in HDInsight using other tools.</span></span>

<span data-ttu-id="4d05e-106">**필수 구성 요소**</span><span class="sxs-lookup"><span data-stu-id="4d05e-106">**Prerequisites**</span></span>

<span data-ttu-id="4d05e-107">이 문서를 시작 하기 전에 다음 항목 hello가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-107">Before you begin this article, you must have hello following items:</span></span>

* <span data-ttu-id="4d05e-108">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="4d05e-108">**An Azure subscription**.</span></span> <span data-ttu-id="4d05e-109">[Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d05e-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="open-hello-portal"></a><span data-ttu-id="4d05e-110">열기 hello 포털</span><span class="sxs-lookup"><span data-stu-id="4d05e-110">Open hello portal</span></span>
1. <span data-ttu-id="4d05e-111">역시 로그인[https://portal.azure.com](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-111">Sign in too[https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4d05e-112">Hello 포털을 연 후 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-112">After you open hello portal, you can:</span></span>

   * <span data-ttu-id="4d05e-113">클릭 **새로** hello 왼쪽된 메뉴 toocreate 새 클러스터에서에서:</span><span class="sxs-lookup"><span data-stu-id="4d05e-113">Click **New** from hello left menu toocreate a new cluster:</span></span>

       ![새 HDInsight 클러스터 단추](./media/hdinsight-administer-use-portal-linux/azure-portal-new-button.png)
   * <span data-ttu-id="4d05e-115">클릭 **HDInsight 클러스터** hello에서 왼쪽된 메뉴 toolist hello 기존 클러스터</span><span class="sxs-lookup"><span data-stu-id="4d05e-115">Click **HDInsight Clusters** from hello left menu toolist hello existing clusters</span></span>

       ![Azure 포털 HDInsight 클러스터 단추](./media/hdinsight-administer-use-portal-linux/azure-portal-hdinsight-button.png)

       <span data-ttu-id="4d05e-117">HDInsight 클러스터를 클릭 하 여 표시 되지 않으면 **더 많은 서비스** hello 목록의 아래쪽 hello 되 고 클릭 **HDInsight 클러스터** hello에서 **인텔리전스 + 분석** 단원을 참조 하십시오입니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-117">If you don't see HDInsight cluster, click **More services** on hello bottom of hello list, and then click **HDInsight clusters** under hello **Intelligence + Analytics** section.</span></span>


## <a name="create-clusters"></a><span data-ttu-id="4d05e-118">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="4d05e-118">Create clusters</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="4d05e-119">HDInsight는 다양한 Hadoop 구성 요소에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-119">HDInsight works with a wide range of Hadoop components.</span></span> <span data-ttu-id="4d05e-120">Hello 구성 요소 확인 및 지원 된 hello 목록에 대 한 참조 [Azure HDInsight의 Hadoop의 어떤 버전은](hdinsight-component-versioning.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-120">For hello list of hello components that have been verified and supported, see [What version of Hadoop is in Azure HDInsight](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="4d05e-121">Hello 일반 클러스터 만든 정보를 참조 하십시오. [HDInsight 클러스터를 만드는 Hadoop](hdinsight-hadoop-provision-linux-clusters.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-121">For hello general cluster creation information, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

### <a name="access-control-requirements"></a><span data-ttu-id="4d05e-122">액세스 제어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="4d05e-122">Access control requirements</span></span>

<span data-ttu-id="4d05e-123">HDInsight 클러스터를 만들 때 Azure 구독을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-123">You must specify an Azure subscription when you create an HDInsight cluster.</span></span> <span data-ttu-id="4d05e-124">새 Azure 리소스 그룹 또는 기존 리소스 그룹에서 이 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-124">This cluster can be created in either a new Azure Resource group or an existing Resource group.</span></span> <span data-ttu-id="4d05e-125">HDInsight 클러스터를 만들기 위한 다음 단계 tooverify hello 사용 권한을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-125">You can use hello following steps tooverify your permissions for creating HDInsight clusters:</span></span>

- <span data-ttu-id="4d05e-126">toouse 기존 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-126">toouse an existing resource group.</span></span>

    1. <span data-ttu-id="4d05e-127">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-127">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
    2. <span data-ttu-id="4d05e-128">클릭 **리소스 그룹** hello 왼쪽된 메뉴 toolist hello 리소스 그룹에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-128">Click **Resource groups** from hello left menu toolist hello resource groups.</span></span>
    3. <span data-ttu-id="4d05e-129">HDInsight 클러스터를 만들기 위한 toouse 원하는 hello 리소스 그룹을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-129">Click hello resource group you want toouse for creating your HDInsight cluster.</span></span>
    4. <span data-ttu-id="4d05e-130">클릭 **액세스 제어 (IAM)**, 되어 있는지 확인 하 고 사용자 (또는 사용자가 속한 그룹)가 적어도 참가자 액세스 toohello 리소스 그룹을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-130">Click **Access control (IAM)**, and verify that you (or a group that you belong to) have at least hello Contributor access toohello resource group.</span></span>

- <span data-ttu-id="4d05e-131">toocreate 새 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="4d05e-131">toocreate a new resource group</span></span>

    1. <span data-ttu-id="4d05e-132">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-132">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
    2. <span data-ttu-id="4d05e-133">클릭 **구독** hello 왼쪽된 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-133">Click **Subscription** from hello left menu.</span></span> <span data-ttu-id="4d05e-134">노란색 키 아이콘이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-134">It has a yellow key icon.</span></span> <span data-ttu-id="4d05e-135">구독의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-135">You shall see a list of subscriptions.</span></span>
    3. <span data-ttu-id="4d05e-136">Toocreate 클러스터를 사용 하는 hello 구독을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-136">Click hello subscription that you use toocreate clusters.</span></span> 
    4. <span data-ttu-id="4d05e-137">**내 사용 권한**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-137">Click **My permissions**.</span></span>  <span data-ttu-id="4d05e-138">표시 프로그램 [역할](../active-directory/role-based-access-control-what-is.md#built-in-roles) hello 가입 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-138">It shows your [role](../active-directory/role-based-access-control-what-is.md#built-in-roles) on hello subscription.</span></span> <span data-ttu-id="4d05e-139">최소한 필요한 참가자 액세스 toocreate HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-139">You need at least Contributor access toocreate HDInsight cluster.</span></span>

<span data-ttu-id="4d05e-140">Hello NoRegisteredProviderFound 오류 또는 hello MissingSubscriptionRegistration 오류를 표시 되 면 [Azure 리소스 관리자와 일반적인 Azure 배포 오류 문제 해결](../azure-resource-manager/resource-manager-common-deployment-errors.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-140">If you receive hello NoRegisteredProviderFound error or hello MissingSubscriptionRegistration error, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](../azure-resource-manager/resource-manager-common-deployment-errors.md).</span></span>

## <a name="list-and-show-clusters"></a><span data-ttu-id="4d05e-141">클러스터 나열 및 표시</span><span class="sxs-lookup"><span data-stu-id="4d05e-141">List and show clusters</span></span>
1. <span data-ttu-id="4d05e-142">역시 로그인[https://portal.azure.com](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-142">Sign in too[https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4d05e-143">클릭 **HDInsight 클러스터** hello에서 왼쪽된 메뉴 toolist hello 기존 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-143">Click **HDInsight Clusters** from hello left menu toolist hello existing clusters.</span></span>
3. <span data-ttu-id="4d05e-144">Hello 클러스터 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-144">Click hello cluster name.</span></span> <span data-ttu-id="4d05e-145">Hello 클러스터 목록이 긴 경우에 hello hello 페이지 위쪽에 필터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-145">If hello cluster list is long, you can use filter on hello top of hello page.</span></span>
4. <span data-ttu-id="4d05e-146">Hello 목록 toosee hello 개요 페이지에서 클러스터를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-146">Click a cluster from hello list toosee hello overview page:</span></span>

    ![Azure Portal HDInsight 클러스터 요점](./media/hdinsight-administer-use-portal-linux/hdinsight-essentials.png)

    * <span data-ttu-id="4d05e-148">**대시보드**: Linux 기반 클러스터용 Ambari Web 즉 열립니다 hello 클러스터 대시보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-148">**Dashboard**: Opens hello cluster dashboard, which is Ambari Web for Linux-based clusters.</span></span>
    * <span data-ttu-id="4d05e-149">**Secure Shell**: SSH (보안 셸) 연결을 사용 하 여 표시 hello 지침 tooconnect toohello 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-149">**Secure Shell**: Shows hello instructions tooconnect toohello cluster using Secure Shell (SSH) connection.</span></span>
    * <span data-ttu-id="4d05e-150">**클러스터의 크기를 조정**:이 클러스터에 대 한 toochange hello 작업자 노드 수를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-150">**Scale Cluster**: Allows you toochange hello number of worker nodes for this cluster.</span></span>
    * <span data-ttu-id="4d05e-151">**삭제**: hello 클러스터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-151">**Delete**: Deletes hello cluster.</span></span>
    * <span data-ttu-id="4d05e-152">**활동 로그**: 활동 로그를 표시하고 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-152">**Activity logs**: Show and query activity logs.</span></span>
    * <span data-ttu-id="4d05e-153">**Access Control(IAM)**: 역할 할당을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-153">**Access control (IAM)**: Use role assignments.</span></span>  <span data-ttu-id="4d05e-154">참조 [역할 할당 toomanage tooyour Azure 구독의 리소스에 액세스를 사용 하 여](../active-directory/role-based-access-control-configure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-154">See [Use role assignments toomanage access tooyour Azure subscription resources](../active-directory/role-based-access-control-configure.md).</span></span>
    * <span data-ttu-id="4d05e-155">**태그**: 있습니다 tooset 키/값 쌍 toodefine 클라우드 서비스의 사용자 정의 분류를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-155">**Tags**: Allows you tooset key/value pairs toodefine a custom taxonomy of your cloud services.</span></span> <span data-ttu-id="4d05e-156">예를 들어 **project**라는 키를 만든 다음 특정 프로젝트와 연결된 모든 서비스에 공통 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-156">For example, you may create a key named **project**, and then use a common value for all services associated with a specific project.</span></span>
    * <span data-ttu-id="4d05e-157">**문제 진단 및 해결**: 문제 해결 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-157">**Diagnose and solve problems**: Display troubleshooting information.</span></span>
    * <span data-ttu-id="4d05e-158">**Locks**: 수정 되거나 삭제 잠금 tooprevent hello 클러스터 되 고 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-158">**Locks**: Add lock tooprevent hello cluster being modified or deleted.</span></span>
    * <span data-ttu-id="4d05e-159">**자동화 스크립트**: hello 클러스터에 대 한 hello Azure 리소스 관리자 템플릿을 표시 및 내보내기.</span><span class="sxs-lookup"><span data-stu-id="4d05e-159">**Automation script**: Display and export hello Azure Resource Manager template for hello cluster.</span></span> <span data-ttu-id="4d05e-160">현재 hello 종속 Azure 저장소 계정만 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-160">Currently, you can only export hello dependent Azure storage account.</span></span> <span data-ttu-id="4d05e-161">[Azure Resource Manager 템플릿을 사용하여 HDInsight의 Linux 기반 Hadoop 클러스터 만들기](hdinsight-hadoop-create-linux-clusters-arm-templates.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d05e-161">See [Create Linux-based Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md).</span></span>
    * <span data-ttu-id="4d05e-162">**빠른 시작**: HDInsight를 사용하여 시작하는 데 도움이 되는 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-162">**Quick Start**:  Displays information that helps you get started using HDInsight.</span></span>
    * <span data-ttu-id="4d05e-163">**HDInsight용 도구**: HDInsight 관련 도구에 대한 도움말 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-163">**Tools for HDInsight**: Help information for HDInsight related tools.</span></span>
    * <span data-ttu-id="4d05e-164">**로그인 클러스터**: hello 클러스터 로그인 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-164">**Cluster Login**: Display hello cluster login information.</span></span>
    * <span data-ttu-id="4d05e-165">**구독 코어 사용량**: 디스플레이 hello 구독에 대 한 사용 되지 않으며 사용 가능한 코어입니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-165">**Subscription Core Usage**: Display hello used and available cores for your subscription.</span></span>
    * <span data-ttu-id="4d05e-166">**클러스터의 크기를 조정**: 증가 및 감소 hello 클러스터 작업자 노드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-166">**Scale Cluster**: Increase and decrease hello number of cluster worker nodes.</span></span> <span data-ttu-id="4d05e-167">[클러스터 크기 조정](hdinsight-administer-use-management-portal.md#scale-clusters)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d05e-167">See[Scale clusters](hdinsight-administer-use-management-portal.md#scale-clusters).</span></span>
    * <span data-ttu-id="4d05e-168">**Secure Shell**: SSH (보안 셸) 연결을 사용 하 여 표시 hello 지침 tooconnect toohello 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-168">**Secure Shell**: Shows hello instructions tooconnect toohello cluster using Secure Shell (SSH) connection.</span></span> <span data-ttu-id="4d05e-169">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d05e-169">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
    * <span data-ttu-id="4d05e-170">**HDInsight 파트너**: 현재 HDInsight 파트너를 hello 추가/제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-170">**HDInsight Partner**: Add/remove hello current HDInsight Partner.</span></span>
    * <span data-ttu-id="4d05e-171">**외부 Metastore**: hello Hive 및 Oozie metastore를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-171">**External Metastores**: View hello Hive and Oozie metastores.</span></span> <span data-ttu-id="4d05e-172">hello metastore hello 클러스터를 만드는 프로세스 동안만 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-172">hello metastores can only be configured during hello cluster creation process.</span></span> <span data-ttu-id="4d05e-173">[Hive/Oozie metastore 사용](hdinsight-hadoop-provision-linux-clusters.md#use-hiveoozie-metastore)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d05e-173">See [use Hive/Oozie metastore](hdinsight-hadoop-provision-linux-clusters.md#use-hiveoozie-metastore).</span></span>
    * <span data-ttu-id="4d05e-174">**스크립트 작업을**: hello 클러스터에서 스크립트를 이용한 적 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-174">**Script Actions**: Run Bash scripts on hello cluster.</span></span> <span data-ttu-id="4d05e-175">[스크립트 작업을 사용하여 Linux 기반 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d05e-175">See [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
    * <span data-ttu-id="4d05e-176">**응용 프로그램**: HDInsight 응용 프로그램을 추가/제거합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-176">**Applications**: Add/remove HDInsight applications.</span></span>  <span data-ttu-id="4d05e-177">[사용자 지정 HDInsight 응용 프로그램 설치](hdinsight-apps-install-custom-applications.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d05e-177">See [Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md).</span></span>
    * <span data-ttu-id="4d05e-178">**속성**: hello 클러스터 속성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-178">**Properties**: View hello cluster properties.</span></span>
    * <span data-ttu-id="4d05e-179">**저장소 계정**: hello 저장소 계정 및 hello 키를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-179">**Storage accounts**: View hello storage accounts and hello keys.</span></span> <span data-ttu-id="4d05e-180">hello 저장소 계정은 hello 클러스터를 만드는 프로세스 동안 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-180">hello storage accounts are configured during hello cluster creation process.</span></span>
    * <span data-ttu-id="4d05e-181">**클러스터 AAD ID**:</span><span class="sxs-lookup"><span data-stu-id="4d05e-181">**Cluster AAD Identity**:</span></span>
    * <span data-ttu-id="4d05e-182">**새로운 지원 요청**: toocreate Microsoft 지원에 지원 티켓을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-182">**New support request**: Allows you toocreate a support ticket with Microsoft support.</span></span>
    
6. <span data-ttu-id="4d05e-183">**속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-183">Click **Properties**:</span></span>

    <span data-ttu-id="4d05e-184">hello 속성은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-184">hello properties are:</span></span>

   * <span data-ttu-id="4d05e-185">**호스트 이름**: 클러스터 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-185">**Hostname**: Cluster name.</span></span>
   * <span data-ttu-id="4d05e-186">**클러스터 URL**.</span><span class="sxs-lookup"><span data-stu-id="4d05e-186">**Cluster URL**.</span></span> <span data-ttu-id="4d05e-187">hello Ambari 웹 인터페이스에 대 한 hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-187">hello URL for hello Ambari web interface.</span></span>
   * <span data-ttu-id="4d05e-188">**상태**: 중단됨, 수락됨, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, 운영, 실행 중, 오류, 삭제 중, 삭제됨, 시간 초과됨, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-188">**Status**: Include Aborted, Accepted, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, Operational, Running, Error, Deleting, Deleted, Timedout, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization</span></span>
   * <span data-ttu-id="4d05e-189">**지역**: Azure 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-189">**Region**: Azure location.</span></span> <span data-ttu-id="4d05e-190">목록이 지원 되는 Azure 위치에 대 한 참조 hello **지역** 드롭다운 목록 상자 [HDInsight 가격](https://azure.microsoft.com/pricing/details/hdinsight/)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-190">For a list of supported Azure locations, see hello **Region** dropdown list box on [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>
   * <span data-ttu-id="4d05e-191">**만든 날짜**</span><span class="sxs-lookup"><span data-stu-id="4d05e-191">**Date created**.</span></span>
   * <span data-ttu-id="4d05e-192">**운영 체제**: **Windows** 또는 **Linux**입니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-192">**Operating system**: Either **Windows** or **Linux**.</span></span>
   * <span data-ttu-id="4d05e-193">**형식**: Hadoop, HBase, Storm, Spark.</span><span class="sxs-lookup"><span data-stu-id="4d05e-193">**Type**: Hadoop, HBase, Storm, Spark.</span></span>
   * <span data-ttu-id="4d05e-194">**버전**.</span><span class="sxs-lookup"><span data-stu-id="4d05e-194">**Version**.</span></span> <span data-ttu-id="4d05e-195">[HDInsight 버전](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="4d05e-195">See [HDInsight versions](hdinsight-component-versioning.md)</span></span>
   * <span data-ttu-id="4d05e-196">**구독**: 구독 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-196">**Subscription**: Subscription name.</span></span>
   * <span data-ttu-id="4d05e-197">**기본 데이터 원본을**: hello 기본 클러스터 파일 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-197">**Default data source**: hello default cluster file system.</span></span>
   * <span data-ttu-id="4d05e-198">**작업자 노드 크기**</span><span class="sxs-lookup"><span data-stu-id="4d05e-198">**Worker nodes size**.</span></span>
   * <span data-ttu-id="4d05e-199">**헤드 노드 크기**</span><span class="sxs-lookup"><span data-stu-id="4d05e-199">**Head node size**.</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="4d05e-200">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="4d05e-200">Delete clusters</span></span>
<span data-ttu-id="4d05e-201">클러스터를 삭제 해도 hello 기본 저장소 계정 또는 연결 된 저장소 계정을 사용 하는 삭제 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-201">Deleting a cluster does not delete hello default storage account or any linked storage accounts.</span></span> <span data-ttu-id="4d05e-202">사용 하 여 hello 클러스터를 다시 만들 수 있습니다 hello 동일한 저장소 계정 및 동일한 metastore hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-202">You can re-create hello cluster by using hello same storage accounts and hello same metastores.</span></span> <span data-ttu-id="4d05e-203">hello 클러스터를 다시 만들 때 toouse 새 기본 Blob 컨테이너를 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-203">It is recommended toouse a new default Blob container when you re-create hello cluster.</span></span>

1. <span data-ttu-id="4d05e-204">Toohello 로그인 [포털][azure-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-204">Sign in toohello [Portal][azure-portal].</span></span>
2. <span data-ttu-id="4d05e-205">클릭 **HDInsight 클러스터** hello 왼쪽된 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-205">Click **HDInsight Clusters** from hello left menu.</span></span> <span data-ttu-id="4d05e-206">**HDInsight 클러스터**가 표시되지 않으면 먼저 **추가 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-206">If you don't see **HDInsight Clusters**, click **More services** first.</span></span>
3. <span data-ttu-id="4d05e-207">Toodelete hello 클러스터를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-207">Click hello cluster that you want toodelete.</span></span>
4. <span data-ttu-id="4d05e-208">클릭 **삭제** hello 위쪽 메뉴에서 다음 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-208">Click **Delete** from hello top menu, and then follow hello instructions.</span></span>

<span data-ttu-id="4d05e-209">참고 항목: [클러스터 일시 중지/종료](#pauseshut-down-clusters)</span><span class="sxs-lookup"><span data-stu-id="4d05e-209">See also [Pause/shut down clusters](#pauseshut-down-clusters).</span></span>

## <a name="add-additional-storage-accounts"></a><span data-ttu-id="4d05e-210">추가 저장소 계정 추가</span><span class="sxs-lookup"><span data-stu-id="4d05e-210">Add additional storage accounts</span></span>

<span data-ttu-id="4d05e-211">클러스터를 만든 후 Azure Storage 계정 및 Azure Data Lake Store 계정을 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-211">You can add additional Azure Storage accounts and Azure Data Lake Store accounts after a cluster is created.</span></span> <span data-ttu-id="4d05e-212">자세한 내용은 참조 [추가 저장소 계정을 tooHDInsight 추가](./hdinsight-hadoop-add-storage.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-212">For more information, see [Add additional storage accounts tooHDInsight](./hdinsight-hadoop-add-storage.md).</span></span>

## <a name="scale-clusters"></a><span data-ttu-id="4d05e-213">클러스터 크기 조정</span><span class="sxs-lookup"><span data-stu-id="4d05e-213">Scale clusters</span></span>
<span data-ttu-id="4d05e-214">hello 클러스터 기능을 확장 하면 toochange hello toore 필요 없이 Azure HDInsight에서 실행 되는 클러스터에서 사용 하는 작업자 노드 수-hello 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-214">hello cluster scaling feature allows you toochange hello number of worker nodes used by a cluster that is running in Azure HDInsight without having toore-create hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="4d05e-215">HDInsight 버전 3.1.3 이상을 사용하는 클러스터만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-215">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="4d05e-216">클러스터의 hello 버전을 잘 모를 경우 hello 속성 페이지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-216">If you are unsure of hello version of your cluster, you can check hello Properties page.</span></span>  <span data-ttu-id="4d05e-217">[클러스터 나열 및 표시](#list-and-show-clusters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d05e-217">See [List and show clusters](#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="4d05e-218">hello HDInsight에서 지원 되는 클러스터의 각 형식에 대 한 데이터 노드 수를 변경 하는 hello 미치는 영향:</span><span class="sxs-lookup"><span data-stu-id="4d05e-218">hello impact of changing hello number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="4d05e-219">Hadoop은</span><span class="sxs-lookup"><span data-stu-id="4d05e-219">Hadoop</span></span>

    <span data-ttu-id="4d05e-220">원활 하 게 hello 보류 중 또는 실행 중인 작업이 모두 영향을 주지 않고 실행 되는 Hadoop 클러스터의 작업자 노드 수를 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-220">You can seamlessly increase hello number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="4d05e-221">Hello 작업이 진행 중인 동안에 새 작업을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-221">New jobs can also be submitted while hello operation is in progress.</span></span> <span data-ttu-id="4d05e-222">크기 조정 작업의 오류는 hello 클러스터는 항상를 작동 상태로 남아 있도록 정상적으로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-222">Failures in a scaling operation are gracefully handled so that hello cluster is always left in a functional state.</span></span>

    <span data-ttu-id="4d05e-223">Hadoop 클러스터는 hello 데이터 노드 수를 줄여 규모 축소, hello 클러스터의 hello 서비스 중 일부를 다시 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-223">When a Hadoop cluster is scaled down by reducing hello number of data nodes, some of hello services in hello cluster are restarted.</span></span> <span data-ttu-id="4d05e-224">이 동작은 실행 중인 모든 및 hello hello 크기 조정 작업이 완료 될 때 작업 toofail 보류 중.</span><span class="sxs-lookup"><span data-stu-id="4d05e-224">This behavior causes all running and pending jobs toofail at hello completion of hello scaling operation.</span></span> <span data-ttu-id="4d05e-225">그러나 hello 작업이 완료 되 면 hello 작업을 다시 전송할을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-225">You can, however, resubmit hello jobs once hello operation is complete.</span></span>
* <span data-ttu-id="4d05e-226">HBase</span><span class="sxs-lookup"><span data-stu-id="4d05e-226">HBase</span></span>

    <span data-ttu-id="4d05e-227">원활 하 게 추가 하거나 실행 하는 동안 노드 tooyour HBase 클러스터를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-227">You can seamlessly add or remove nodes tooyour HBase cluster while it is running.</span></span> <span data-ttu-id="4d05e-228">지역 서버는 hello 크기 조정 작업을 완료 하는 몇 분 안에 자동으로 균형이 조정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-228">Regional Servers are automatically balanced within a few minutes of completing hello scaling operation.</span></span> <span data-ttu-id="4d05e-229">그러나 명령을 명령 프롬프트 창에서 다음 실행 중인 hello와 클러스터의 헤드 노드에 toohello에 로그인 하 여 hello 지역 서버를 수동으로 분산 시킬 수 있습니다 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-229">However, you can also manually balance hello regional servers by logging in toohello headnode of cluster and running hello following commands from a command prompt window:</span></span>

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer

    <span data-ttu-id="4d05e-230">Hello HBase 셸을 사용 하 여에 대 한 자세한 내용은 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4d05e-230">For more information on using hello HBase shell, see []</span></span>
* <span data-ttu-id="4d05e-231">Storm</span><span class="sxs-lookup"><span data-stu-id="4d05e-231">Storm</span></span>

    <span data-ttu-id="4d05e-232">원활 하 게 추가 하거나 실행 하는 동안 데이터 노드 tooyour Storm 클러스터를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-232">You can seamlessly add or remove data nodes tooyour Storm cluster while it is running.</span></span> <span data-ttu-id="4d05e-233">하지만 hello 크기 조정 작업을 성공적으로 완료 한 후 toorebalance hello 토폴로지를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-233">But after a successful completion of hello scaling operation, you will need toorebalance hello topology.</span></span>

    <span data-ttu-id="4d05e-234">다음 두 가지 방법으로 사용하여 균형을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-234">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="4d05e-235">Storm 웹 UI</span><span class="sxs-lookup"><span data-stu-id="4d05e-235">Storm web UI</span></span>
  * <span data-ttu-id="4d05e-236">명령줄 인터페이스(CLI) 도구</span><span class="sxs-lookup"><span data-stu-id="4d05e-236">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="4d05e-237">Toohello 참조 [Apache Storm 설명서](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-237">Refer toohello [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="4d05e-238">hello 스톰 웹 UI hello HDInsight 클러스터에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-238">hello Storm web UI is available on hello HDInsight cluster:</span></span>

    ![HDInsight Storm 규모 균형 재조정](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster-storm-rebalance.png)

    <span data-ttu-id="4d05e-240">다음은 예제 어떻게 toouse hello CLI 명령을 toorebalance hello 스톰 토폴로지:</span><span class="sxs-lookup"><span data-stu-id="4d05e-240">Here is an example how toouse hello CLI command toorebalance hello Storm topology:</span></span>

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="4d05e-241">**tooscale 클러스터**</span><span class="sxs-lookup"><span data-stu-id="4d05e-241">**tooscale clusters**</span></span>

1. <span data-ttu-id="4d05e-242">Toohello 로그인 [포털][azure-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-242">Sign in toohello [Portal][azure-portal].</span></span>
2. <span data-ttu-id="4d05e-243">클릭 **HDInsight 클러스터** hello 왼쪽된 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-243">Click **HDInsight Clusters** from hello left menu.</span></span>
3. <span data-ttu-id="4d05e-244">Tooscale hello 클러스터를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-244">Click hello cluster you want tooscale.</span></span>
3. <span data-ttu-id="4d05e-245">**클러스터 크기 조정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-245">Click **Scale Cluster**.</span></span>
4. <span data-ttu-id="4d05e-246">**작업자 노드 수**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-246">Enter **Number of Worker nodes**.</span></span> <span data-ttu-id="4d05e-247">클러스터 노드의 hello 수 제한을 15 hello Azure 구독 마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-247">hello limit on hello number of cluster nodes varies among Azure subscriptions.</span></span> <span data-ttu-id="4d05e-248">청구 지원 tooincrease hello 제한을 문의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-248">You can contact billing support tooincrease hello limit.</span></span>  <span data-ttu-id="4d05e-249">hello 비용 정보 hello 변경 사항을 toohello 노드 수를 반영 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-249">hello cost information reflects hello changes you have made toohello number of nodes.</span></span>

    ![HDinsight Hadoop Hbase Storm Spark 크기 조정](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster.png)

## <a name="pauseshut-down-clusters"></a><span data-ttu-id="4d05e-251">클러스터 일시 중지/종료</span><span class="sxs-lookup"><span data-stu-id="4d05e-251">Pause/shut down clusters</span></span>

<span data-ttu-id="4d05e-252">대부분의 Hadoop 작업은 이따금 실행되는 일괄 처리 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-252">Most of Hadoop jobs are batch jobs that are only run occasionally.</span></span> <span data-ttu-id="4d05e-253">대부분의 Hadoop 클러스터에 대 한는 오랜 시간 해당 hello 클러스터 사용 하지 않는 처리를 위해 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-253">For most Hadoop clusters, there are large periods of time that hello cluster is not being used for processing.</span></span> <span data-ttu-id="4d05e-254">HDInsight를 사용하면 데이터가 Azure 저장소에 저장되기 때문에 클러스터를 사용하지 않을 때 안전하게 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-254">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span>
<span data-ttu-id="4d05e-255">HDInsight 클러스터를 사용하지 않는 기간에도 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-255">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="4d05e-256">Hello 클러스터에 대 한 hello 요금이 저장소에 대 한 hello 요금 보다 많은 배 더 많은 경우 이렇게 하면 경제 toodelete 클러스터 사용에서 되지 않은 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-256">Since hello charges for hello cluster are many times more than hello charges for storage, it makes economic sense toodelete clusters when they are not in use.</span></span>

<span data-ttu-id="4d05e-257">여러 가지 방법으로 hello 프로세스를 프로그래밍할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-257">There are many ways you can program hello process:</span></span>

* <span data-ttu-id="4d05e-258">사용자 Azure 데이터 팩터리.</span><span class="sxs-lookup"><span data-stu-id="4d05e-258">User Azure Data Factory.</span></span> <span data-ttu-id="4d05e-259">주문형 HDInsight 연결된 서비스 만들기는 [Azure Data Factory를 사용하여 HDInsight에서 주문형 Linux 기반 Hadoop 클러스터 만들기](hdinsight-hadoop-create-linux-clusters-adf.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d05e-259">See [Create on-demand Linux-based Hadoop clusters in HDInsight using Azure Data Factory](hdinsight-hadoop-create-linux-clusters-adf.md) for creating on-demand HDInsight linked services.</span></span>
* <span data-ttu-id="4d05e-260">Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="4d05e-260">Use Azure PowerShell.</span></span>  <span data-ttu-id="4d05e-261">[비행 지연 데이터 분석](hdinsight-analyze-flight-delay-data.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d05e-261">See [Analyze flight delay data](hdinsight-analyze-flight-delay-data.md).</span></span>
* <span data-ttu-id="4d05e-262">Azure CLI 사용</span><span class="sxs-lookup"><span data-stu-id="4d05e-262">Use Azure CLI.</span></span> <span data-ttu-id="4d05e-263">[Azure CLI를 사용하여 HDInsight 클러스터 관리](hdinsight-administer-use-command-line.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d05e-263">See [Manage HDInsight clusters using Azure CLI](hdinsight-administer-use-command-line.md).</span></span>
* <span data-ttu-id="4d05e-264">HDInsight .NET SDK 사용</span><span class="sxs-lookup"><span data-stu-id="4d05e-264">Use HDInsight .NET SDK.</span></span> <span data-ttu-id="4d05e-265">[Hadoop 작업 제출](hdinsight-submit-hadoop-jobs-programmatically.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d05e-265">See [Submit Hadoop jobs](hdinsight-submit-hadoop-jobs-programmatically.md).</span></span>

<span data-ttu-id="4d05e-266">가격 책정 정보는 hello에 대 한 참조 [HDInsight 가격](https://azure.microsoft.com/pricing/details/hdinsight/)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-266">For hello pricing information, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span> <span data-ttu-id="4d05e-267">hello 포털에서에서 클러스터 toodelete 참조 [클러스터를 삭제 합니다.](#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="4d05e-267">toodelete a cluster from hello Portal, see [Delete clusters](#delete-clusters)</span></span>


## <a name="upgrade-clusters"></a><span data-ttu-id="4d05e-268">클러스터 업그레이드</span><span class="sxs-lookup"><span data-stu-id="4d05e-268">Upgrade clusters</span></span>

<span data-ttu-id="4d05e-269">참조 [업그레이드 HDInsight 클러스터 tooa 최신 버전이](./hdinsight-upgrade-cluster.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-269">See [Upgrade HDInsight cluster tooa newer version](./hdinsight-upgrade-cluster.md).</span></span>

## <a name="change-passwords"></a><span data-ttu-id="4d05e-270">암호 변경</span><span class="sxs-lookup"><span data-stu-id="4d05e-270">Change passwords</span></span>
<span data-ttu-id="4d05e-271">HDInsight 클러스터마다 두 개의 사용자 계정이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-271">An HDInsight cluster can have two user accounts.</span></span> <span data-ttu-id="4d05e-272">HDInsight 클러스터 사용자 계정 (규칙 하위 hello</span><span class="sxs-lookup"><span data-stu-id="4d05e-272">hello HDInsight cluster user account (A.K.A.</span></span> <span data-ttu-id="4d05e-273">HTTP 사용자 계정) 하 고 hello 만드는 프로세스 동안 hello SSH 사용자 계정이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-273">HTTP user account) and hello SSH user account are created during hello creation process.</span></span> <span data-ttu-id="4d05e-274">Hello Ambari 웹 UI toochange hello 클러스터 사용자 계정 사용자 이름 및 암호와 스크립트 동작 toochange hello SSH 사용자 계정 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-274">You can use hello Ambari web UI toochange hello cluster user account username and password, and script actions toochange hello SSH user account</span></span>

### <a name="change-hello-cluster-user-password"></a><span data-ttu-id="4d05e-275">Hello 클러스터 사용자 암호 변경</span><span class="sxs-lookup"><span data-stu-id="4d05e-275">Change hello cluster user password</span></span>
<span data-ttu-id="4d05e-276">Hello Ambari 웹 UI toochange hello 클러스터 사용자 암호를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-276">You can use hello Ambari Web UI toochange hello Cluster user password.</span></span> <span data-ttu-id="4d05e-277">tooAmbari에 toolog, hello 기존 클러스터 사용자 이름 및 암호 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-277">toolog in tooAmbari, you must use hello existing cluster username and password.</span></span>

> [!NOTE]
> <span data-ttu-id="4d05e-278">Hello 클러스터 사용자 (관리자) 암호를 변경할이 클러스터 toofail에 대 한 작업을 실행 하는 스크립트를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-278">Changing hello cluster user (admin) password may cause script actions ran against this cluster toofail.</span></span> <span data-ttu-id="4d05e-279">작업자 노드를 대상으로 하는 지속형된 스크립트 동작을 설정한 경우 이러한 스크립트는 크기 조정 작업을 통해 toohello 클러스터 노드를 추가 하면 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-279">If you have any persisted script actions that target worker nodes, these scripts may fail when you add nodes toohello cluster through resize operations.</span></span> <span data-ttu-id="4d05e-280">스크립트 작업에 대한 자세한 내용은 [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d05e-280">For more information on script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
>
>

1. <span data-ttu-id="4d05e-281">Toohello Ambari 웹 UI를 사용 하 여 로그인 hello HDInsight 클러스터에 대 한 사용자 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-281">Sign in toohello Ambari Web UI using hello HDInsight cluster user credentials.</span></span> <span data-ttu-id="4d05e-282">hello 기본 사용자 이름은 **admin**. URL은 hello **https://&lt;HDInsight 클러스터 이름 > azurehdinsight.net**합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-282">hello default username is **admin**. hello URL is **https://&lt;HDInsight Cluster Name>azurehdinsight.net**.</span></span>
2. <span data-ttu-id="4d05e-283">클릭 **Admin** hello 상단 메뉴에서 다음 "관리 Ambari"를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-283">Click **Admin** from hello top menu, and then click "Manage Ambari".</span></span>
3. <span data-ttu-id="4d05e-284">Hello 왼쪽된 메뉴에서 클릭 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-284">From hello left menu, click **Users**.</span></span>
4. <span data-ttu-id="4d05e-285">**Admin**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-285">Click **Admin**.</span></span>
5. <span data-ttu-id="4d05e-286">**암호 변경**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-286">Click **Change Password**.</span></span>

<span data-ttu-id="4d05e-287">Ambari는 hello 클러스터의 모든 노드에서 hello 암호를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-287">Ambari then changes hello password on all nodes in hello cluster.</span></span>

### <a name="change-hello-ssh-user-password"></a><span data-ttu-id="4d05e-288">Hello SSH 사용자 암호 변경</span><span class="sxs-lookup"><span data-stu-id="4d05e-288">Change hello SSH user password</span></span>
1. <span data-ttu-id="4d05e-289">Hello 이라는 파일로 텍스트를 다음 텍스트 편집기를 사용 하 여 저장할 **changepassword.sh**합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-289">Using a text editor, save hello following text as a file named **changepassword.sh**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="4d05e-290">Hello 줄 끝으로 LF를 사용 하는 편집기를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-290">You must use an editor that uses LF as hello line ending.</span></span> <span data-ttu-id="4d05e-291">Hello 편집기에서는 CRLF hello 스크립트 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-291">If hello editor uses CRLF, then hello script does not work.</span></span>
   >
   >

        #! /bin/bash
        USER=$1
        PASS=$2

        usermod --password $(echo $PASS | openssl passwd -1 -stdin) $USER
2. <span data-ttu-id="4d05e-292">HTTP 또는 HTTPS 주소를 사용 하 여 HDInsight에서 액세스할 수 있는 hello 파일 tooa 저장 위치를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-292">Upload hello file tooa storage location that can be accessed from HDInsight using an HTTP or HTTPS address.</span></span> <span data-ttu-id="4d05e-293">예를 들어 OneDrive 또는 Azure Blob 저장소와 같은 공용 파일 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-293">For example, a public file store such as OneDrive or Azure Blob storage.</span></span> <span data-ttu-id="4d05e-294">이 URI는 hello 다음 단계에서 필요에 따라 hello URI (HTTP 또는 HTTPS 주소) toohello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-294">Save hello URI (HTTP or HTTPS address) toohello file, as this URI is needed in hello next step.</span></span>
3. <span data-ttu-id="4d05e-295">Hello Azure 포털에서에서 클릭 **HDInsight 클러스터**합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-295">From hello Azure portal, click **HDInsight Clusters**.</span></span>
4. <span data-ttu-id="4d05e-296">HDInsight 클러스터를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-296">Click your HDInsight cluster.</span></span>
4. <span data-ttu-id="4d05e-297">**스크립트 작업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-297">Click **Script Actions**.</span></span>
4. <span data-ttu-id="4d05e-298">Hello에서 **스크립트 동작** 블레이드를 **새 제출**합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-298">From hello **Script Actions** blade, select **Submit New**.</span></span> <span data-ttu-id="4d05e-299">Hello 때 **스크립트 동작을 제출** 블레이드 나타나면 hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-299">When hello **Submit script action** blade appears, enter hello following information:</span></span>

   | <span data-ttu-id="4d05e-300">필드</span><span class="sxs-lookup"><span data-stu-id="4d05e-300">Field</span></span> | <span data-ttu-id="4d05e-301">값</span><span class="sxs-lookup"><span data-stu-id="4d05e-301">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="4d05e-302">Name</span><span class="sxs-lookup"><span data-stu-id="4d05e-302">Name</span></span> |<span data-ttu-id="4d05e-303">SSH 암호 변경</span><span class="sxs-lookup"><span data-stu-id="4d05e-303">Change ssh password</span></span> |
   | <span data-ttu-id="4d05e-304">Bash 스크립트 URI</span><span class="sxs-lookup"><span data-stu-id="4d05e-304">Bash script URI</span></span> |<span data-ttu-id="4d05e-305">hello URI toohello changepassword.sh 파일</span><span class="sxs-lookup"><span data-stu-id="4d05e-305">hello URI toohello changepassword.sh file</span></span> |
   | <span data-ttu-id="4d05e-306">노드(헤드, 작업자, Nimbus, 감독자, Zookeeper 등)</span><span class="sxs-lookup"><span data-stu-id="4d05e-306">Nodes (Head, Worker, Nimbus, Supervisor, Zookeeper, etc.)</span></span> |<span data-ttu-id="4d05e-307">나열된 모든 노드 형식에 대한 ✓</span><span class="sxs-lookup"><span data-stu-id="4d05e-307">✓ for all node types listed</span></span> |
   | <span data-ttu-id="4d05e-308">매개 변수</span><span class="sxs-lookup"><span data-stu-id="4d05e-308">Parameters</span></span> |<span data-ttu-id="4d05e-309">Hello SSH 사용자 이름이 고 hello 새 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-309">Enter hello SSH user name and then hello new password.</span></span> <span data-ttu-id="4d05e-310">Hello 사용자 이름 및 암호 hello 사이 공백을 하나 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-310">There should be one space between hello user name and hello password.</span></span> |
   | <span data-ttu-id="4d05e-311">이 스크립트 작업을 유지...</span><span class="sxs-lookup"><span data-stu-id="4d05e-311">Persist this script action ...</span></span> |<span data-ttu-id="4d05e-312">이 필드는 선택 취소로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-312">Leave this field unchecked.</span></span> |
5. <span data-ttu-id="4d05e-313">선택 **만들기** tooapply hello 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-313">Select **Create** tooapply hello script.</span></span> <span data-ttu-id="4d05e-314">Hello 스크립트 완료 SSH를 사용 하 여 hello 새 암호로 수 tooconnect toohello 클러스터 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-314">Once hello script finishes, you are able tooconnect toohello cluster using SSH with hello new password.</span></span>

## <a name="grantrevoke-access"></a><span data-ttu-id="4d05e-315">액세스 권한 부여/해지</span><span class="sxs-lookup"><span data-stu-id="4d05e-315">Grant/revoke access</span></span>
<span data-ttu-id="4d05e-316">HDInsight 클러스터에는 HTTP 웹 서비스 (모든 이러한 서비스는 RESTful 끝점)를 수행 하는 hello:</span><span class="sxs-lookup"><span data-stu-id="4d05e-316">HDInsight clusters have hello following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="4d05e-317">ODBC</span><span class="sxs-lookup"><span data-stu-id="4d05e-317">ODBC</span></span>
* <span data-ttu-id="4d05e-318">JDBC</span><span class="sxs-lookup"><span data-stu-id="4d05e-318">JDBC</span></span>
* <span data-ttu-id="4d05e-319">Ambari</span><span class="sxs-lookup"><span data-stu-id="4d05e-319">Ambari</span></span>
* <span data-ttu-id="4d05e-320">Oozie</span><span class="sxs-lookup"><span data-stu-id="4d05e-320">Oozie</span></span>
* <span data-ttu-id="4d05e-321">Templeton</span><span class="sxs-lookup"><span data-stu-id="4d05e-321">Templeton</span></span>

<span data-ttu-id="4d05e-322">이러한 서비스에는 기본적으로 액세스 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-322">By default, these services are granted for access.</span></span> <span data-ttu-id="4d05e-323">있습니다 수 revoke/부여 사용 하 여 hello 액세스 [Azure CLI](hdinsight-administer-use-command-line.md#enabledisable-http-access-for-a-cluster) 및 [Azure PowerShell](hdinsight-administer-use-powershell.md#grantrevoke-access)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-323">You can revoke/grant hello access using [Azure CLI](hdinsight-administer-use-command-line.md#enabledisable-http-access-for-a-cluster) and [Azure PowerShell](hdinsight-administer-use-powershell.md#grantrevoke-access).</span></span>

## <a name="find-hello-subscription-id"></a><span data-ttu-id="4d05e-324">Hello 구독 ID 찾기</span><span class="sxs-lookup"><span data-stu-id="4d05e-324">Find hello subscription ID</span></span>

<span data-ttu-id="4d05e-325">**toofind Azure 구독 Id**</span><span class="sxs-lookup"><span data-stu-id="4d05e-325">**toofind your Azure subscription IDs**</span></span>

1. <span data-ttu-id="4d05e-326">Toohello 로그인 [포털][azure-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-326">Sign in toohello [Portal][azure-portal].</span></span>
2. <span data-ttu-id="4d05e-327">**구독**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-327">Click **Subscriptions**.</span></span> <span data-ttu-id="4d05e-328">각 구독에는 이름 및 ID가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-328">Each subscription has a name and an ID.</span></span>

<span data-ttu-id="4d05e-329">각 클러스터는 동 점된 tooan Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="4d05e-329">Each cluster is tied tooan Azure subscription.</span></span> <span data-ttu-id="4d05e-330">hello 클러스터에 ID를 표시 하는 구독 hello **필수** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-330">hello subscription ID is shown on hello cluster **Essential** tile.</span></span> <span data-ttu-id="4d05e-331">[클러스터 나열 및 표시](#list-and-show-clusters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d05e-331">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="find-hello-resource-group"></a><span data-ttu-id="4d05e-332">Hello 리소스 그룹 찾기</span><span class="sxs-lookup"><span data-stu-id="4d05e-332">Find hello resource group</span></span>
<span data-ttu-id="4d05e-333">Hello Azure 리소스 관리자 모드에서 각 HDInsight 클러스터는 Azure 리소스 관리자 그룹이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-333">In hello Azure Resource Manager mode, each HDInsight cluster is created with an Azure Resource Manager group.</span></span> <span data-ttu-id="4d05e-334">클러스터에 tooappears 속해 있는 hello 리소스 관리자 그룹:</span><span class="sxs-lookup"><span data-stu-id="4d05e-334">hello Resource Manager group that a cluster belongs tooappears in:</span></span>

* <span data-ttu-id="4d05e-335">hello 클러스터 목록에는 **리소스 그룹** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-335">hello cluster list has a **Resource Group** column.</span></span>
* <span data-ttu-id="4d05e-336">클러스터 **Essential** 타일.</span><span class="sxs-lookup"><span data-stu-id="4d05e-336">Cluster **Essential** tile.</span></span>  

<span data-ttu-id="4d05e-337">[클러스터 나열 및 표시](#list-and-show-clusters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d05e-337">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="find-hello-default-storage-account"></a><span data-ttu-id="4d05e-338">Hello 기본 저장소 계정 찾기</span><span class="sxs-lookup"><span data-stu-id="4d05e-338">Find hello default storage account</span></span>
<span data-ttu-id="4d05e-339">각 HDInsight 클러스터에는 기본 저장소 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-339">Each HDInsight cluster has a default storage account.</span></span> <span data-ttu-id="4d05e-340">아래에 표시 하는 클러스터에 대 한 기본 저장소 계정 및 해당 키를 hello **저장소 계정은**합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-340">hello default storage account and its keys for a cluster appears under **Storage Accounts**.</span></span> <span data-ttu-id="4d05e-341">[클러스터 나열 및 표시](#list-and-show-clusters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d05e-341">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="run-hive-queries"></a><span data-ttu-id="4d05e-342">Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="4d05e-342">Run Hive queries</span></span>
<span data-ttu-id="4d05e-343">Hello Azure 포털에서 직접 하이브 작업을 실행할 수 없습니다 되지만 hello Ambari 웹 UI에서 하이브 보기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-343">You cannot run Hive job directly from hello Azure portal, but you can use hello Hive View on Ambari Web UI.</span></span>

<span data-ttu-id="4d05e-344">**Ambari 하이브 보기를 사용 하 여 toorun 하이브 쿼리**</span><span class="sxs-lookup"><span data-stu-id="4d05e-344">**toorun Hive queries using Ambari Hive View**</span></span>

1. <span data-ttu-id="4d05e-345">Toohello Ambari 웹 UI를 사용 하 여 로그인 hello HDInsight 클러스터에 대 한 사용자 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-345">Sign in toohello Ambari Web UI using hello HDInsight cluster user credentials.</span></span> <span data-ttu-id="4d05e-346">hello 기본 사용자 이름은 **admin**. URL은 hello **https://&lt;HDInsight 클러스터 이름 > azurehdinsight.net**합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-346">hello default username is **admin**. hello URL is **https://&lt;HDInsight Cluster Name>azurehdinsight.net**.</span></span>
2. <span data-ttu-id="4d05e-347">Hello 스크린 샷 뒤에 표시 된 대로 하이브 보기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-347">Open Hive View as shown in hello following screenshot:</span></span>  

    ![HDInsight Hive 보기](./media/hdinsight-administer-use-portal-linux/hdinsight-hive-view.png)
3. <span data-ttu-id="4d05e-349">클릭 **쿼리** hello 상단 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-349">Click **Query** from hello top menu.</span></span>
4. <span data-ttu-id="4d05e-350">**쿼리 편집기**에서 Hive 쿼리를 입력한 다음 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-350">Enter a Hive query in **Query Editor**, and then click **Execute**.</span></span>

## <a name="monitor-jobs"></a><span data-ttu-id="4d05e-351">작업 모니터링</span><span class="sxs-lookup"><span data-stu-id="4d05e-351">Monitor jobs</span></span>
<span data-ttu-id="4d05e-352">참조 [hello Ambari 웹 UI를 사용 하 여 관리 하는 HDInsight 클러스터](hdinsight-hadoop-manage-ambari.md#monitoring)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-352">See [Manage HDInsight clusters by using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md#monitoring).</span></span>

## <a name="browse-files"></a><span data-ttu-id="4d05e-353">파일 찾아보기</span><span class="sxs-lookup"><span data-stu-id="4d05e-353">Browse files</span></span>
<span data-ttu-id="4d05e-354">Hello Azure 포털을 사용 하 여 hello 기본 컨테이너의 hello 내용을 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-354">Using hello Azure portal, you can browse hello content of hello default container.</span></span>

1. <span data-ttu-id="4d05e-355">역시 로그인[https://portal.azure.com](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-355">Sign in too[https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4d05e-356">클릭 **HDInsight 클러스터** hello에서 왼쪽된 메뉴 toolist hello 기존 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-356">Click **HDInsight Clusters** from hello left menu toolist hello existing clusters.</span></span>
3. <span data-ttu-id="4d05e-357">Hello 클러스터 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-357">Click hello cluster name.</span></span> <span data-ttu-id="4d05e-358">Hello 클러스터 목록이 긴 경우에 hello hello 페이지 위쪽에 필터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-358">If hello cluster list is long, you can use filter on hello top of hello page.</span></span>
4. <span data-ttu-id="4d05e-359">클릭 **저장소 계정은** hello 클러스터 왼쪽된 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-359">Click **Storage Accounts** from hello cluster left menu.</span></span>
5. <span data-ttu-id="4d05e-360">Storage 계정을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-360">Click a Storage account.</span></span>
7. <span data-ttu-id="4d05e-361">Hello 클릭 **Blob** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-361">Click hello **Blobs** tile.</span></span>
8. <span data-ttu-id="4d05e-362">Hello 기본 컨테이너 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-362">Click hello default container name.</span></span>

## <a name="monitor-cluster-usage"></a><span data-ttu-id="4d05e-363">클러스터 사용 현황 모니터링</span><span class="sxs-lookup"><span data-stu-id="4d05e-363">Monitor cluster usage</span></span>
<span data-ttu-id="4d05e-364">hello **사용** hello HDInsight 클러스터 블레이드의 섹션에는 hello HDInsight 함께 사용할 사용 가능한 tooyour 구독 코어 수가 hello toothis 클러스터 하 게 하는 방법을 할당 하는 코어 수에 대 한 정보가 표시 됩니다. 이 클러스터 내에서 hello 노드에 대 한 할당.</span><span class="sxs-lookup"><span data-stu-id="4d05e-364">hello **Usage** section of hello HDInsight cluster blade displays information about hello number of cores available tooyour subscription for use with HDInsight, as well as hello number of cores allocated toothis cluster and how they are allocated for hello nodes within this cluster.</span></span> <span data-ttu-id="4d05e-365">[클러스터 나열 및 표시](#list-and-show-clusters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d05e-365">See [List and show clusters](#list-and-show-clusters).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d05e-366">HDInsight 클러스터 hello에서 toomonitor hello 서비스 제공, Ambari Web을 사용 하거나 REST API Ambari hello 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-366">toomonitor hello services provided by hello HDInsight cluster, you must use Ambari Web or hello Ambari REST API.</span></span> <span data-ttu-id="4d05e-367">Ambari 사용에 대한 자세한 내용은 [Ambari를 사용하여 HDInsight 클러스터 관리](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="4d05e-367">For more information on using Ambari, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>
>
>

## <a name="connect-tooa-cluster"></a><span data-ttu-id="4d05e-368">Tooa 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="4d05e-368">Connect tooa cluster</span></span>

* [<span data-ttu-id="4d05e-369">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="4d05e-369">Use Hive with HDInsight</span></span>](hdinsight-hadoop-use-hive-ambari-view.md)
* [<span data-ttu-id="4d05e-370">HDInsight와 함께 SSH 사용</span><span class="sxs-lookup"><span data-stu-id="4d05e-370">Use SSH with HDInsight</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)

## <a name="next-steps"></a><span data-ttu-id="4d05e-371">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4d05e-371">Next steps</span></span>
<span data-ttu-id="4d05e-372">이 문서에서는 몇 가지 기본 관리 함수에 대해 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="4d05e-372">In this article, you have learned some basic administative functions.</span></span> <span data-ttu-id="4d05e-373">더 toolearn hello 다음 문서를 참조:</span><span class="sxs-lookup"><span data-stu-id="4d05e-373">toolearn more, see hello following articles:</span></span>

* [<span data-ttu-id="4d05e-374">Azure PowerShell을 사용하여 HDInsight 관리</span><span class="sxs-lookup"><span data-stu-id="4d05e-374">Administer HDInsight Using Azure PowerShell</span></span>](hdinsight-administer-use-powershell.md)
* [<span data-ttu-id="4d05e-375">Azure CLI를 사용하여 HDInsight 관리</span><span class="sxs-lookup"><span data-stu-id="4d05e-375">Administer HDInsight Using Azure CLI</span></span>](hdinsight-administer-use-command-line.md)
* [<span data-ttu-id="4d05e-376">HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="4d05e-376">Create HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="4d05e-377">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="4d05e-377">Use Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="4d05e-378">HDInsight에서 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="4d05e-378">Use Pig in HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="4d05e-379">HDInsight에서 Sqoop 사용</span><span class="sxs-lookup"><span data-stu-id="4d05e-379">Use Sqoop in HDInsight</span></span>](hdinsight-use-sqoop.md)
* [<span data-ttu-id="4d05e-380">Azure HDInsight 시작</span><span class="sxs-lookup"><span data-stu-id="4d05e-380">Get Started with Azure HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="4d05e-381">Azure HDInsight에 포함된 Hadoop 버전</span><span class="sxs-lookup"><span data-stu-id="4d05e-381">What version of Hadoop is in Azure HDInsight?</span></span>](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-portal-linux/hdinsight-hadoop-command-line.png "Hadoop 명령줄"
