---
title: "aaaManage 도메인에 가입 된 HDInsight 클러스터-Azure | Microsoft Docs"
description: "어떻게 toomanage 도메인에 가입 된 HDInsight 클러스터에 대해 알아봅니다"
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
ms.openlocfilehash: 233ddf0953e981f9a24b77d9dde194d590e5e6d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-domain-joined-hdinsight-clusters-preview"></a><span data-ttu-id="a6f0f-103">도메인에 가입된 HDInsight 클러스터 관리(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="a6f0f-103">Manage Domain-joined HDInsight clusters (Preview)</span></span>
<span data-ttu-id="a6f0f-104">Hello 사용자 및 도메인에 가입 된 HDInsight 클러스터와 어떻게 toomanage 도메인에 가입 된 HDInsight 클러스터에 hello 역할에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-104">Learn hello users and hello roles in Domain-joined HDInsight, and how toomanage domain-joined HDInsight clusters.</span></span>

## <a name="users-of-domain-joined-hdinsight-clusters"></a><span data-ttu-id="a6f0f-105">도메인에 가입된 HDInsight 클러스터의 사용자</span><span class="sxs-lookup"><span data-stu-id="a6f0f-105">Users of Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="a6f0f-106">도메인에 가입 되지 않은 하는 HDInsight 클러스터에 hello 클러스터 생성 중에 생성 되는 두 개의 사용자 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-106">An HDInsight cluster that is not domain-joined has two user accounts that are created during hello cluster creation:</span></span>

* <span data-ttu-id="a6f0f-107">**Ambari 관리자**: 이 계정을 *Hadoop 사용자* 또는 *HTTP 사용자*라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-107">**Ambari admin**: This account is also known as *Hadoop user* or *HTTP user*.</span></span> <span data-ttu-id="a6f0f-108">이 계정에서 https:// tooAmbari에 사용 되는 toolog 수&lt;clustername >. azurehdinsight.net 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-108">This account can be used toolog on tooAmbari at https://&lt;clustername>.azurehdinsight.net.</span></span> <span data-ttu-id="a6f0f-109">또한 Ambari 뷰에 대 한 사용된 toorun 쿼리 수, 외부 도구 (즉, PowerShell, Templeton, Visual Studio)를 통해 작업을 실행 및 hello 하이브 ODBC 드라이버 및 (즉, Excel, PowerBI, 또는 Tableau)의 BI 도구를 사용 하 여 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-109">It can also be used toorun queries on Ambari views, execute jobs via external tools (i.e. PowerShell, Templeton, Visual Studio), and authenticate with hello Hive ODBC driver and BI tools (i.e. Excel, PowerBI, or Tableau).</span></span>
* <span data-ttu-id="a6f0f-110">**SSH 사용자**: 이 계정은 SSH와 함께 사용할 수 있으며, sudo 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-110">**SSH user**:  This account can be used with SSH, and execute sudo commands.</span></span> <span data-ttu-id="a6f0f-111">루트 권한이 toohello Linux Vm에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-111">It has root privileges toohello Linux VMs.</span></span>

<span data-ttu-id="a6f0f-112">또한 tooAmbari Admin 및 SSH 사용자 3 개의 새 사용자가 포함 하는 도메인에 가입 된 HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-112">A domain-joined HDInsight cluster has three new users in addition tooAmbari Admin and SSH user.</span></span>

* <span data-ttu-id="a6f0f-113">**레인저 admin**:이 계정은 로컬 hello Apache 레인저 관리자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-113">**Ranger admin**:  This account is hello local Apache Ranger admin account.</span></span> <span data-ttu-id="a6f0f-114">이 계정은 Active Directory 도메인 사용자가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-114">It is not an active directory domain user.</span></span> <span data-ttu-id="a6f0f-115">이 계정을 사용 하는 toosetup 정책을 수 있으며 (해당 사용자가 관리할 수 있도록 정책) 다른 사용자가 관리자 또는 위임 된 관리자를 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-115">This account can be used toosetup policies and make other users admins or delegated admins (so that those users can manage policies).</span></span> <span data-ttu-id="a6f0f-116">기본적으로 hello username는 *관리자* hello 암호 hello Ambari 관리자 암호와 동일 hello는 및입니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-116">By default, hello username is *admin* and hello password is hello same as hello Ambari admin password.</span></span> <span data-ttu-id="a6f0f-117">hello 암호 레인저의 hello 설정 페이지에서 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-117">hello password can be updated from hello Settings page in Ranger.</span></span>
* <span data-ttu-id="a6f0f-118">**클러스터 관리: 도메인 사용자**:이 계정은 Ambari 및 레인저 포함 하 여 Hadoop 클러스터 관리자 hello으로 지정 된 active directory 도메인 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-118">**Cluster admin domain user**: This account is an active directory domain user designated as hello Hadoop cluster admin including Ambari and Ranger.</span></span> <span data-ttu-id="a6f0f-119">클러스터를 만드는 동안 이 사용자의 자격 증명을 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-119">You must provide this user’s credentials during cluster creation.</span></span> <span data-ttu-id="a6f0f-120">이 사용자에 게 다음 권한을 hello:</span><span class="sxs-lookup"><span data-stu-id="a6f0f-120">This user has hello following privileges:</span></span>

  * <span data-ttu-id="a6f0f-121">컴퓨터 toohello 도메인에 가입 하 고 클러스터를 만드는 동안 지정 된 OU hello 내에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-121">Join machines toohello domain and place them within hello OU that you specify during cluster creation.</span></span>
  * <span data-ttu-id="a6f0f-122">Hello 클러스터 생성 중에 지정 된 OU 내에서 서비스 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-122">Create service principals within hello OU that you specify during cluster creation.</span></span>
  * <span data-ttu-id="a6f0f-123">역방향 DNS 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-123">Create reverse DNS entries.</span></span>

    <span data-ttu-id="a6f0f-124">참고 hello 다른 AD 사용자는 또한 이러한 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-124">Note hello other AD users also have these privileges.</span></span>

    <span data-ttu-id="a6f0f-125">일부 끝점 (예를 들어, Templeton) hello 클러스터 내에서 레인저를 통해 관리 되지 않는 이며 안전 하지 않은 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-125">There are some end points within hello cluster (for example, Templeton) which are not managed by Ranger, and hence are not secure.</span></span> <span data-ttu-id="a6f0f-126">이러한 끝점 hello 클러스터 관리: 도메인 사용자를 제외한 모든 사용자에 대해 잠겨 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-126">These end points are locked down for all users except hello cluster admin domain user.</span></span>
* <span data-ttu-id="a6f0f-127">**일반**: 클러스터를 만들 때 여러 Active Directory 그룹을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-127">**Regular**: During cluster creation, you can provide multiple active directory groups.</span></span> <span data-ttu-id="a6f0f-128">이러한 그룹의 hello 사용자 Ambari 동기화 된 tooRanger 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-128">hello users in these groups will be synced tooRanger and Ambari.</span></span> <span data-ttu-id="a6f0f-129">이러한 사용자는 도메인 사용자를 액세스 tooonly 레인저 관리 끝점 (예를 들어 Hiveserver2)을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-129">These users are domain users and will have access tooonly Ranger-managed endpoints (for example, Hiveserver2).</span></span> <span data-ttu-id="a6f0f-130">RBAC 정책을 모든 hello 및 적용 가능한 toothese 사용자 감사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-130">All hello RBAC policies and auditing will be applicable toothese users.</span></span>

## <a name="roles-of-domain-joined-hdinsight-clusters"></a><span data-ttu-id="a6f0f-131">도메인에 가입된 HDInsight 클러스터의 역할</span><span class="sxs-lookup"><span data-stu-id="a6f0f-131">Roles of Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="a6f0f-132">도메인에 가입 된 HDInsight 사용할 역할을 수행 하는 hello 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-132">Domain-joined HDInsight have hello following roles:</span></span>

* <span data-ttu-id="a6f0f-133">클러스터 관리자</span><span class="sxs-lookup"><span data-stu-id="a6f0f-133">Cluster Administrator</span></span>
* <span data-ttu-id="a6f0f-134">클러스터 운영자</span><span class="sxs-lookup"><span data-stu-id="a6f0f-134">Cluster Operator</span></span>
* <span data-ttu-id="a6f0f-135">서비스 관리자</span><span class="sxs-lookup"><span data-stu-id="a6f0f-135">Service Administrator</span></span>
* <span data-ttu-id="a6f0f-136">서비스 운영자</span><span class="sxs-lookup"><span data-stu-id="a6f0f-136">Service Operator</span></span>
* <span data-ttu-id="a6f0f-137">클러스터 사용자</span><span class="sxs-lookup"><span data-stu-id="a6f0f-137">Cluster User</span></span>

<span data-ttu-id="a6f0f-138">**이러한 역할의 toosee hello 사용 권한**</span><span class="sxs-lookup"><span data-stu-id="a6f0f-138">**toosee hello permissions of these roles**</span></span>

1. <span data-ttu-id="a6f0f-139">Hello Ambari 관리 UI를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-139">Open hello Ambari Management UI.</span></span>  <span data-ttu-id="a6f0f-140">참조 [열려 hello Ambari 관리 UI](#open-the-ambari-management-ui)합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-140">See [Open hello Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="a6f0f-141">Hello 왼쪽된 메뉴에서 클릭 **역할**합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-141">From hello left menu, click **Roles**.</span></span>
3. <span data-ttu-id="a6f0f-142">Hello 파란색 물음표 toosee hello 사용 권한을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-142">Click hello blue question mark toosee hello permissions:</span></span>

    ![도메인에 가입된 HDInsight 클러스터의 역할 사용 권한](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-roles-permissions.png)

## <a name="open-hello-ambari-management-ui"></a><span data-ttu-id="a6f0f-144">Hello Ambari 관리 UI를 열으십시오</span><span class="sxs-lookup"><span data-stu-id="a6f0f-144">Open hello Ambari Management UI</span></span>
1. <span data-ttu-id="a6f0f-145">Toohello 로그온 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-145">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a6f0f-146">블레이드에서 HDInsight 클러스터를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-146">Open your HDInsight cluster in a blade.</span></span> <span data-ttu-id="a6f0f-147">[클러스터 나열 및 표시](hdinsight-administer-use-management-portal.md#list-and-show-clusters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-147">See [List and show clusters](hdinsight-administer-use-management-portal.md#list-and-show-clusters).</span></span>
3. <span data-ttu-id="a6f0f-148">클릭 **대시보드** hello 상단 메뉴 tooopen Ambari에서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-148">Click **Dashboard** from hello top menu tooopen Ambari.</span></span>
4. <span data-ttu-id="a6f0f-149">TooAmbari hello 클러스터 관리자가 도메인 사용자 이름 및 암호를 사용 하 여 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-149">Log on tooAmbari using hello cluster administrator domain user name and password.</span></span>
5. <span data-ttu-id="a6f0f-150">Hello 클릭 **Admin** hello 오른쪽 상단에서 드롭다운 메뉴 **관리 Ambari**합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-150">Click hello **Admin** dropdown menu from hello upper right corner, and then click **Manage Ambari**.</span></span>

    ![도메인에 가입된 HDInsight 관리 Ambari](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-manage-ambari.png)

    <span data-ttu-id="a6f0f-152">hello UI는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-152">hello UI looks like:</span></span>

    ![도메인에 가입된 HDInsight Ambari 관리 UI](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui.png)

## <a name="list-hello-domain-users-synchronized-from-your-active-directory"></a><span data-ttu-id="a6f0f-154">Active Directory에서 동기화 hello 도메인 사용자를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-154">List hello domain users synchronized from your Active Directory</span></span>
1. <span data-ttu-id="a6f0f-155">Hello Ambari 관리 UI를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-155">Open hello Ambari Management UI.</span></span>  <span data-ttu-id="a6f0f-156">참조 [열려 hello Ambari 관리 UI](#open-the-ambari-management-ui)합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-156">See [Open hello Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="a6f0f-157">Hello 왼쪽된 메뉴에서 클릭 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-157">From hello left menu, click **Users**.</span></span> <span data-ttu-id="a6f0f-158">Active Directory toohello HDInsight 클러스터에서 동기화 하는 모든 hello 사용자를 확인할 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-158">You shall see all hello users synced from your Active Directory toohello HDInsight cluster.</span></span>

    ![도메인에 가입된 HDInsight Ambari 관리 UI 사용자 나열](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-users.png)

## <a name="list-hello-domain-groups-synchronized-from-your-active-directory"></a><span data-ttu-id="a6f0f-160">Hello 도메인 그룹 목록을 Active Directory에서 동기화</span><span class="sxs-lookup"><span data-stu-id="a6f0f-160">List hello domain groups synchronized from your Active Directory</span></span>
1. <span data-ttu-id="a6f0f-161">Hello Ambari 관리 UI를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-161">Open hello Ambari Management UI.</span></span>  <span data-ttu-id="a6f0f-162">참조 [열려 hello Ambari 관리 UI](#open-the-ambari-management-ui)합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-162">See [Open hello Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="a6f0f-163">Hello 왼쪽된 메뉴에서 클릭 **그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-163">From hello left menu, click **Groups**.</span></span> <span data-ttu-id="a6f0f-164">Active Directory toohello HDInsight 클러스터에서 동기화 하는 모든 hello 그룹을 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-164">You shall see all hello groups synced from your Active Directory toohello HDInsight cluster.</span></span>

    ![도메인에 가입된 HDInsight Ambari 관리 UI 그룹 나열](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-groups.png)

## <a name="configure-hive-views-permissions"></a><span data-ttu-id="a6f0f-166">Hive 뷰 사용 권한 구성</span><span class="sxs-lookup"><span data-stu-id="a6f0f-166">Configure Hive Views permissions</span></span>
1. <span data-ttu-id="a6f0f-167">Hello Ambari 관리 UI를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-167">Open hello Ambari Management UI.</span></span>  <span data-ttu-id="a6f0f-168">참조 [열려 hello Ambari 관리 UI](#open-the-ambari-management-ui)합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-168">See [Open hello Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="a6f0f-169">Hello 왼쪽된 메뉴에서 클릭 **뷰**합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-169">From hello left menu, click **Views**.</span></span>
3. <span data-ttu-id="a6f0f-170">클릭 **하이브** tooshow hello 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-170">Click **HIVE** tooshow hello details.</span></span>

    ![도메인에 가입된 HDInsight Ambari 관리 UI Hive 뷰](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views.png)
4. <span data-ttu-id="a6f0f-172">Hello 클릭 **하이브 보기** tooconfigure 하이브 뷰를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-172">Click hello **Hive View** link tooconfigure Hive Views.</span></span>
5. <span data-ttu-id="a6f0f-173">Toohello 아래로 스크롤하여 **권한을** 섹션.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-173">Scroll down toohello **Permissions** section.</span></span>

    ![도메인에 가입된 HDInsight Ambari 관리 UI Hive 뷰 사용 권한 구성](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views-permissions.png)
6. <span data-ttu-id="a6f0f-175">클릭 **사용자 추가** 또는 **그룹 추가**, 하이브 보기를 사용할 수 있는 hello 사용자 또는 그룹을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-175">Click **Add User** or **Add Group**, and then specify hello users or groups that can use Hive Views.</span></span>

## <a name="configure-users-for-hello-roles"></a><span data-ttu-id="a6f0f-176">Hello 역할에 대 한 사용자 구성</span><span class="sxs-lookup"><span data-stu-id="a6f0f-176">Configure users for hello roles</span></span>
 <span data-ttu-id="a6f0f-177">toosee 역할과 해당 사용 권한을 목록이 참조 [역할의 도메인에 가입 된 HDInsight 클러스터](#roles-of-domain---joined-hdinsight-clusters)합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-177">toosee a list of roles and their permissions, see [Roles of Domain-joined HDInsight clusters](#roles-of-domain---joined-hdinsight-clusters).</span></span>

1. <span data-ttu-id="a6f0f-178">Hello Ambari 관리 UI를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-178">Open hello Ambari Management UI.</span></span>  <span data-ttu-id="a6f0f-179">참조 [열려 hello Ambari 관리 UI](#open-the-ambari-management-ui)합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-179">See [Open hello Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="a6f0f-180">Hello 왼쪽된 메뉴에서 클릭 **역할**합니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-180">From hello left menu, click **Roles**.</span></span>
3. <span data-ttu-id="a6f0f-181">클릭 **사용자 추가** 또는 **그룹 추가** tooassign 사용자 및 그룹 toodifferent 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-181">Click **Add User** or **Add Group** tooassign users and groups toodifferent roles.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6f0f-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a6f0f-182">Next steps</span></span>
* <span data-ttu-id="a6f0f-183">도메인에 가입된 HDInsight 클러스터 구성에 대한 자세한 내용은 [도메인에 가입된 HDInsight 클러스터 구성](hdinsight-domain-joined-configure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-183">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="a6f0f-184">Hive 정책 및 Hive 쿼리 실행에 대한 자세한 내용은 [도메인에 가입된 HDInsight 클러스터에 대한 Hive 정책 구성](hdinsight-domain-joined-run-hive.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-184">For configuring Hive policies and run Hive queries, see [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md).</span></span>
* <span data-ttu-id="a6f0f-185">도메인에 가입된 HDInsight 클러스터에서 SSH를 사용하여 Hive 쿼리를 실행하려면 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6f0f-185">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>
