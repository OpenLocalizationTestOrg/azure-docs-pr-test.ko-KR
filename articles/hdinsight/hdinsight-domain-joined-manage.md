---
title: "도메인 가입 HDInsight 클러스터 관리 - Azure | Microsoft Docs"
description: "도메인에 가입된 HDInsight 클러스터를 관리하는 방법을 알아봅니다."
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 6ebc4d2f-2f6a-4e1e-ab6d-af4db6b4c87c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 9b56ce6cc5bdd3b8d48d047751e978cad08598e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-domain-joined-hdinsight-clusters-preview"></a><span data-ttu-id="56bf6-103">도메인에 가입된 HDInsight 클러스터 관리(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="56bf6-103">Manage Domain-joined HDInsight clusters (Preview)</span></span>
<span data-ttu-id="56bf6-104">도메인에 가입된 HDInsight의 사용자 및 역할에 대해 알아보고 도메인에 가입된 HDInsight 클러스터를 관리하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-104">Learn the users and the roles in Domain-joined HDInsight, and how to manage domain-joined HDInsight clusters.</span></span>

## <a name="users-of-domain-joined-hdinsight-clusters"></a><span data-ttu-id="56bf6-105">도메인에 가입된 HDInsight 클러스터의 사용자</span><span class="sxs-lookup"><span data-stu-id="56bf6-105">Users of Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="56bf6-106">도메인 가입되어 있지 않은 HDInsight 클러스터에는 클러스터를 만드는 중에 생성되는 두 개의 사용자 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-106">An HDInsight cluster that is not domain-joined has two user accounts that are created during the cluster creation:</span></span>

* <span data-ttu-id="56bf6-107">**Ambari 관리자**: 이 계정을 *Hadoop 사용자* 또는 *HTTP 사용자*라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-107">**Ambari admin**: This account is also known as *Hadoop user* or *HTTP user*.</span></span> <span data-ttu-id="56bf6-108">이 계정은 https://&lt;clustername>.azurehdinsight.net에서 Ambari에 로그온할 때 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-108">This account can be used to log on to Ambari at https://&lt;clustername>.azurehdinsight.net.</span></span> <span data-ttu-id="56bf6-109">또한 Ambari 뷰에서 쿼리를 실행하고, 외부 도구(즉, PowerShell, Templeton, Visual Studio)를 통해 작업을 실행하고, Hive ODBC 드라이버와 BI 도구(즉, Excel, PowerBI 또는 Tableau)를 인증할 때에도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-109">It can also be used to run queries on Ambari views, execute jobs via external tools (i.e. PowerShell, Templeton, Visual Studio), and authenticate with the Hive ODBC driver and BI tools (i.e. Excel, PowerBI, or Tableau).</span></span>
* <span data-ttu-id="56bf6-110">**SSH 사용자**: 이 계정은 SSH와 함께 사용할 수 있으며, sudo 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-110">**SSH user**:  This account can be used with SSH, and execute sudo commands.</span></span> <span data-ttu-id="56bf6-111">그리고 Linux VM에 대한 루트 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-111">It has root privileges to the Linux VMs.</span></span>

<span data-ttu-id="56bf6-112">도메인에 가입된 HDInsight 클러스터에는 Ambari 관리자와 SSH 사용자 외에도 3개의 새로운 사용자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-112">A domain-joined HDInsight cluster has three new users in addition to Ambari Admin and SSH user.</span></span>

* <span data-ttu-id="56bf6-113">**Ranger 관리자**: 이 계정은 로컬 Apache Ranger 관리자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-113">**Ranger admin**:  This account is the local Apache Ranger admin account.</span></span> <span data-ttu-id="56bf6-114">이 계정은 Active Directory 도메인 사용자가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-114">It is not an active directory domain user.</span></span> <span data-ttu-id="56bf6-115">이 계정은 정책을 설정하고 다른 사용자를 관리자 또는 위임된 관리자로 만드는 데(해당 사용자가 정책을 관리할 수 있도록) 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-115">This account can be used to setup policies and make other users admins or delegated admins (so that those users can manage policies).</span></span> <span data-ttu-id="56bf6-116">기본적으로 사용자 이름은 *admin*이고 암호는 Ambari 관리자 암호와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-116">By default, the username is *admin* and the password is the same as the Ambari admin password.</span></span> <span data-ttu-id="56bf6-117">암호는 Ranger의 설정 페이지에서 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-117">The password can be updated from the Settings page in Ranger.</span></span>
* <span data-ttu-id="56bf6-118">**클러스터 관리 도메인 사용자**: 이 계정은 Ambari 및 Ranger를 포함하여 Hadoop 클러스터 관리자로 지정된 Active Directory 도메인 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-118">**Cluster admin domain user**: This account is an active directory domain user designated as the Hadoop cluster admin including Ambari and Ranger.</span></span> <span data-ttu-id="56bf6-119">클러스터를 만드는 동안 이 사용자의 자격 증명을 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-119">You must provide this user’s credentials during cluster creation.</span></span> <span data-ttu-id="56bf6-120">이 사용자는 다음과 같은 권한을 갖고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-120">This user has the following privileges:</span></span>

  * <span data-ttu-id="56bf6-121">컴퓨터를 도메인에 가입하고 클러스터를 만드는 동안 지정하는 OU 내에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-121">Join machines to the domain and place them within the OU that you specify during cluster creation.</span></span>
  * <span data-ttu-id="56bf6-122">클러스터를 만드는 동안 지정하는 OU 내에 서비스 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-122">Create service principals within the OU that you specify during cluster creation.</span></span>
  * <span data-ttu-id="56bf6-123">역방향 DNS 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-123">Create reverse DNS entries.</span></span>

    <span data-ttu-id="56bf6-124">다른 AD 사용자도 이러한 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-124">Note the other AD users also have these privileges.</span></span>

    <span data-ttu-id="56bf6-125">클러스터 내에는 Ranger를 통해 관리되지 않는 끝점(예: Templeton)이 있으며, 따라서 이러한 끝점은 안전하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-125">There are some end points within the cluster (for example, Templeton) which are not managed by Ranger, and hence are not secure.</span></span> <span data-ttu-id="56bf6-126">이러한 끝점은 클러스터 관리 도메인 사용자를 제외한 모든 사용자에게 잠겨 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-126">These end points are locked down for all users except the cluster admin domain user.</span></span>
* <span data-ttu-id="56bf6-127">**일반**: 클러스터를 만들 때 여러 Active Directory 그룹을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-127">**Regular**: During cluster creation, you can provide multiple active directory groups.</span></span> <span data-ttu-id="56bf6-128">이러한 그룹의 사용자는 Ranger 및 Ambari와 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-128">The users in these groups will be synced to Ranger and Ambari.</span></span> <span data-ttu-id="56bf6-129">이러한 사용자는 도메인 사용자이며 Ranger를 통해 관리되는 끝점(예: Hiveserver2)에만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-129">These users are domain users and will have access to only Ranger-managed endpoints (for example, Hiveserver2).</span></span> <span data-ttu-id="56bf6-130">이러한 사용자에게는 모든 RBAC 정책 및 감사가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-130">All the RBAC policies and auditing will be applicable to these users.</span></span>

## <a name="roles-of-domain-joined-hdinsight-clusters"></a><span data-ttu-id="56bf6-131">도메인에 가입된 HDInsight 클러스터의 역할</span><span class="sxs-lookup"><span data-stu-id="56bf6-131">Roles of Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="56bf6-132">도메인에 가입된 HDInsight에는 다음과 같은 역할이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-132">Domain-joined HDInsight have the following roles:</span></span>

* <span data-ttu-id="56bf6-133">클러스터 관리자</span><span class="sxs-lookup"><span data-stu-id="56bf6-133">Cluster Administrator</span></span>
* <span data-ttu-id="56bf6-134">클러스터 운영자</span><span class="sxs-lookup"><span data-stu-id="56bf6-134">Cluster Operator</span></span>
* <span data-ttu-id="56bf6-135">서비스 관리자</span><span class="sxs-lookup"><span data-stu-id="56bf6-135">Service Administrator</span></span>
* <span data-ttu-id="56bf6-136">서비스 운영자</span><span class="sxs-lookup"><span data-stu-id="56bf6-136">Service Operator</span></span>
* <span data-ttu-id="56bf6-137">클러스터 사용자</span><span class="sxs-lookup"><span data-stu-id="56bf6-137">Cluster User</span></span>

<span data-ttu-id="56bf6-138">**이러한 역할의 사용 권한을 보려면**</span><span class="sxs-lookup"><span data-stu-id="56bf6-138">**To see the permissions of these roles**</span></span>

1. <span data-ttu-id="56bf6-139">Ambari 관리 UI를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-139">Open the Ambari Management UI.</span></span>  <span data-ttu-id="56bf6-140">[Ambari 관리 UI 열기](#open-the-ambari-management-ui)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56bf6-140">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="56bf6-141">왼쪽 메뉴에서 **역할**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-141">From the left menu, click **Roles**.</span></span>
3. <span data-ttu-id="56bf6-142">파란색 물음표를 클릭하여 사용 권한을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-142">Click the blue question mark to see the permissions:</span></span>

    ![도메인에 가입된 HDInsight 클러스터의 역할 사용 권한](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-roles-permissions.png)

## <a name="open-the-ambari-management-ui"></a><span data-ttu-id="56bf6-144">Ambari 관리 UI 열기</span><span class="sxs-lookup"><span data-stu-id="56bf6-144">Open the Ambari Management UI</span></span>
1. <span data-ttu-id="56bf6-145">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-145">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="56bf6-146">블레이드에서 HDInsight 클러스터를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-146">Open your HDInsight cluster in a blade.</span></span> <span data-ttu-id="56bf6-147">[클러스터 나열 및 표시](hdinsight-administer-use-management-portal.md#list-and-show-clusters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56bf6-147">See [List and show clusters](hdinsight-administer-use-management-portal.md#list-and-show-clusters).</span></span>
3. <span data-ttu-id="56bf6-148">위쪽 메뉴에서 **대시보드** 를 클릭하여 Ambari를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-148">Click **Dashboard** from the top menu to open Ambari.</span></span>
4. <span data-ttu-id="56bf6-149">클러스터 관리자 도메인 사용자 이름 및 암호를 사용하여 Ambari에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-149">Log on to Ambari using the cluster administrator domain user name and password.</span></span>
5. <span data-ttu-id="56bf6-150">오른쪽 상단 모서리에서 **관리자** 드롭다운 메뉴를 클릭한 다음 **Ambari 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-150">Click the **Admin** dropdown menu from the upper right corner, and then click **Manage Ambari**.</span></span>

    ![도메인에 가입된 HDInsight 관리 Ambari](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-manage-ambari.png)

    <span data-ttu-id="56bf6-152">UI는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-152">The UI looks like:</span></span>

    ![도메인에 가입된 HDInsight Ambari 관리 UI](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui.png)

## <a name="list-the-domain-users-synchronized-from-your-active-directory"></a><span data-ttu-id="56bf6-154">Active Directory에서 동기화된 도메인 사용자 나열</span><span class="sxs-lookup"><span data-stu-id="56bf6-154">List the domain users synchronized from your Active Directory</span></span>
1. <span data-ttu-id="56bf6-155">Ambari 관리 UI를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-155">Open the Ambari Management UI.</span></span>  <span data-ttu-id="56bf6-156">[Ambari 관리 UI 열기](#open-the-ambari-management-ui)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56bf6-156">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="56bf6-157">왼쪽 메뉴에서 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-157">From the left menu, click **Users**.</span></span> <span data-ttu-id="56bf6-158">Active Directory에서 HDInsight 클러스터로 동기화된 모든 사용자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-158">You shall see all the users synced from your Active Directory to the HDInsight cluster.</span></span>

    ![도메인에 가입된 HDInsight Ambari 관리 UI 사용자 나열](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-users.png)

## <a name="list-the-domain-groups-synchronized-from-your-active-directory"></a><span data-ttu-id="56bf6-160">Active Directory에서 동기화된 도메인 그룹 나열</span><span class="sxs-lookup"><span data-stu-id="56bf6-160">List the domain groups synchronized from your Active Directory</span></span>
1. <span data-ttu-id="56bf6-161">Ambari 관리 UI를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-161">Open the Ambari Management UI.</span></span>  <span data-ttu-id="56bf6-162">[Ambari 관리 UI 열기](#open-the-ambari-management-ui)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56bf6-162">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="56bf6-163">왼쪽 메뉴에서 **그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-163">From the left menu, click **Groups**.</span></span> <span data-ttu-id="56bf6-164">Active Directory에서 HDInsight 클러스터로 동기화된 모든 그룹이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-164">You shall see all the groups synced from your Active Directory to the HDInsight cluster.</span></span>

    ![도메인에 가입된 HDInsight Ambari 관리 UI 그룹 나열](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-groups.png)

## <a name="configure-hive-views-permissions"></a><span data-ttu-id="56bf6-166">Hive 뷰 사용 권한 구성</span><span class="sxs-lookup"><span data-stu-id="56bf6-166">Configure Hive Views permissions</span></span>
1. <span data-ttu-id="56bf6-167">Ambari 관리 UI를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-167">Open the Ambari Management UI.</span></span>  <span data-ttu-id="56bf6-168">[Ambari 관리 UI 열기](#open-the-ambari-management-ui)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56bf6-168">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="56bf6-169">왼쪽 메뉴에서 **뷰**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-169">From the left menu, click **Views**.</span></span>
3. <span data-ttu-id="56bf6-170">**HIVE**를 클릭하여 세부 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-170">Click **HIVE** to show the details.</span></span>

    ![도메인에 가입된 HDInsight Ambari 관리 UI Hive 뷰](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views.png)
4. <span data-ttu-id="56bf6-172">**Hive 뷰**를 클릭하여 Hive 뷰를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-172">Click the **Hive View** link to configure Hive Views.</span></span>
5. <span data-ttu-id="56bf6-173">아래에 있는 **사용 권한** 섹션으로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-173">Scroll down to the **Permissions** section.</span></span>

    ![도메인에 가입된 HDInsight Ambari 관리 UI Hive 뷰 사용 권한 구성](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views-permissions.png)
6. <span data-ttu-id="56bf6-175">**사용자 추가** 또는 **그룹 추가**를 클릭한 다음 Hive 뷰를 사용할 수 있는 사용자 또는 그룹을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-175">Click **Add User** or **Add Group**, and then specify the users or groups that can use Hive Views.</span></span>

## <a name="configure-users-for-the-roles"></a><span data-ttu-id="56bf6-176">역할에 대해 사용자 구성</span><span class="sxs-lookup"><span data-stu-id="56bf6-176">Configure users for the roles</span></span>
 <span data-ttu-id="56bf6-177">역할 및 각 역할의 사용 권한을 보려면 [도메인에 가입된 HDInsight 클러스터의 역할](#roles-of-domain---joined-hdinsight-clusters)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56bf6-177">To see a list of roles and their permissions, see [Roles of Domain-joined HDInsight clusters](#roles-of-domain---joined-hdinsight-clusters).</span></span>

1. <span data-ttu-id="56bf6-178">Ambari 관리 UI를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-178">Open the Ambari Management UI.</span></span>  <span data-ttu-id="56bf6-179">[Ambari 관리 UI 열기](#open-the-ambari-management-ui)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56bf6-179">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="56bf6-180">왼쪽 메뉴에서 **역할**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-180">From the left menu, click **Roles**.</span></span>
3. <span data-ttu-id="56bf6-181">**사용자 추가** 또는 **그룹 추가**를 클릭하여 여러 역할에 사용자 및 그룹을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="56bf6-181">Click **Add User** or **Add Group** to assign users and groups to different roles.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56bf6-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="56bf6-182">Next steps</span></span>
* <span data-ttu-id="56bf6-183">도메인에 가입된 HDInsight 클러스터 구성에 대한 자세한 내용은 [도메인에 가입된 HDInsight 클러스터 구성](hdinsight-domain-joined-configure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56bf6-183">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="56bf6-184">Hive 정책 및 Hive 쿼리 실행에 대한 자세한 내용은 [도메인에 가입된 HDInsight 클러스터에 대한 Hive 정책 구성](hdinsight-domain-joined-run-hive.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56bf6-184">For configuring Hive policies and run Hive queries, see [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md).</span></span>
* <span data-ttu-id="56bf6-185">도메인에 가입된 HDInsight 클러스터에서 SSH를 사용하여 Hive 쿼리를 실행하려면 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56bf6-185">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>
