---
title: "사용 하 여 Azure Data Lake 분석 aaaManage hello Azure 포털 | Microsoft Docs"
description: "자세한 내용은 toomanage Data Lake 분석 계정, 데이터 원본, 사용자와 작업 하는 방법입니다."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: a0e045f1-73d6-427f-868d-7b55c10f811b
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: f63ccdfae79772c92e92462194e8cdc636a73dc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-by-using-hello-azure-portal"></a><span data-ttu-id="d8b45-103">Azure 포털 hello를 사용 하 여 Azure 데이터 레이크 분석 관리</span><span class="sxs-lookup"><span data-stu-id="d8b45-103">Manage Azure Data Lake Analytics by using hello Azure portal</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="d8b45-104">어떻게 toomanage Azure Data Lake 분석 계정, 데이터 소스 계정, 사용자 및 사용 하 여 작업 hello Azure 포털에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-104">Learn how toomanage Azure Data Lake Analytics accounts, account data sources, users, and jobs by using hello Azure portal.</span></span> <span data-ttu-id="d8b45-105">다른 도구를 사용 하는 방법에 대 한 관리 항목 toosee hello hello 페이지 위쪽에 있는 탭을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-105">toosee management topics about using other tools, click a tab at hello top of hello page.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-lake-analytics-accounts"></a><span data-ttu-id="d8b45-106">Data Lake Analytics 계정 관리</span><span class="sxs-lookup"><span data-stu-id="d8b45-106">Manage Data Lake Analytics accounts</span></span>

### <a name="create-an-account"></a><span data-ttu-id="d8b45-107">계정 만들기</span><span class="sxs-lookup"><span data-stu-id="d8b45-107">Create an account</span></span>

1. <span data-ttu-id="d8b45-108">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-108">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d8b45-109">**새로 만들기** > **인텔리전스 + 분석** > **Data Lake Analytics**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-109">Click **New** > **Intelligence + analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="d8b45-110">다음 항목 hello에 대 한 값을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-110">Select values for hello following items:</span></span> 
   1. <span data-ttu-id="d8b45-111">**이름**: hello 이름 hello Data Lake 분석 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-111">**Name**: hello name of hello Data Lake Analytics account.</span></span>
   2. <span data-ttu-id="d8b45-112">**구독**: hello hello 계정에 사용 되는 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="d8b45-112">**Subscription**: hello Azure subscription used for hello account.</span></span>
   3. <span data-ttu-id="d8b45-113">**리소스 그룹**: toocreate hello 계정에 hello Azure 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-113">**Resource Group**: hello Azure resource group in which toocreate hello account.</span></span> 
   4. <span data-ttu-id="d8b45-114">**위치**: hello hello Data Lake 분석 계정에 대 한 Azure 데이터 센터입니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-114">**Location**: hello Azure datacenter for hello Data Lake Analytics account.</span></span> 
   5. <span data-ttu-id="d8b45-115">**데이터 레이크 저장소**: hello Data Lake 분석 계정에 사용 되는 기본 저장소 toobe hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-115">**Data Lake Store**: hello default store toobe used for hello Data Lake Analytics account.</span></span> <span data-ttu-id="d8b45-116">hello Azure 데이터 레이크 저장소 계정 및 hello Data Lake 분석 계정에 있어야 합니다. 동일한 위치를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-116">hello Azure Data Lake Store account and hello Data Lake Analytics account must be in hello same location.</span></span>
4. <span data-ttu-id="d8b45-117">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-117">Click **Create**.</span></span> 

### <a name="delete-a-data-lake-analytics-account"></a><span data-ttu-id="d8b45-118">Data Lake Analytics 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="d8b45-118">Delete a Data Lake Analytics account</span></span>

<span data-ttu-id="d8b45-119">Data Lake Analytics 계정을 삭제하기 전에 먼저 해당 기본 Data Lake Store 계정을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-119">Before you delete a Data Lake Analytics account, delete its default Data Lake Store account.</span></span>

1. <span data-ttu-id="d8b45-120">Azure 포털 hello tooyour Data Lake 분석 계정을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-120">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="d8b45-121">**삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-121">Click **Delete**.</span></span>
3. <span data-ttu-id="d8b45-122">형식 hello 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-122">Type hello account name.</span></span>
4. <span data-ttu-id="d8b45-123">**삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-123">Click **Delete**.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-sources"></a><span data-ttu-id="d8b45-124">데이터 원본 관리</span><span class="sxs-lookup"><span data-stu-id="d8b45-124">Manage data sources</span></span>

<span data-ttu-id="d8b45-125">Data Lake 분석 데이터 원본 hello를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-125">Data Lake Analytics supports hello following data sources:</span></span>

* <span data-ttu-id="d8b45-126">데이터 레이크 저장소</span><span class="sxs-lookup"><span data-stu-id="d8b45-126">Data Lake Store</span></span>
* <span data-ttu-id="d8b45-127">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="d8b45-127">Azure Storage</span></span>

<span data-ttu-id="d8b45-128">데이터 탐색기 toobrowse 데이터 원본을 사용 하 고 기본 파일 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-128">You can use Data Explorer toobrowse data sources and perform basic file management operations.</span></span> 

### <a name="add-a-data-source"></a><span data-ttu-id="d8b45-129">데이터 원본 추가</span><span class="sxs-lookup"><span data-stu-id="d8b45-129">Add a data source</span></span>

1. <span data-ttu-id="d8b45-130">Azure 포털 hello tooyour Data Lake 분석 계정을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-130">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="d8b45-131">**데이터 원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-131">Click **Data Sources**.</span></span>
3. <span data-ttu-id="d8b45-132">**데이터 원본 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-132">Click **Add Data Source**.</span></span>
    
   * <span data-ttu-id="d8b45-133">데이터 레이크 저장소 계정 tooadd 해야 hello 계정 이름과 액세스 toohello toobe 수 tooquery 계정 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-133">tooadd a Data Lake Store account, you need hello account name and access toohello account toobe able tooquery it.</span></span>
   * <span data-ttu-id="d8b45-134">Azure Blob 저장소 tooadd hello 저장소 계정 및 계정 키 hello 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-134">tooadd Azure Blob storage, you need hello storage account and hello account key.</span></span> <span data-ttu-id="d8b45-135">toofind hello 포털에서 저장소 계정의 toohello 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-135">toofind them, go toohello storage account in hello portal.</span></span>

## <a name="set-up-firewall-rules"></a><span data-ttu-id="d8b45-136">방화벽 규칙 설정</span><span class="sxs-lookup"><span data-stu-id="d8b45-136">Set up firewall rules</span></span>

<span data-ttu-id="d8b45-137">데이터 레이크 분석 toofurther 잠금 액세스 tooyour Data Lake 분석 계정 hello 네트워크 수준에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-137">You can use Data Lake Analytics toofurther lock down access tooyour Data Lake Analytics account at hello network level.</span></span> <span data-ttu-id="d8b45-138">방화벽을 사용하도록 설정하고 IP 주소를 지정하거나 신뢰할 수 있는 클라이언트에 대한 IP 주소 범위를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-138">You can enable a firewall, specify an IP address, or define an IP address range for your trusted clients.</span></span> <span data-ttu-id="d8b45-139">이러한 측정값을 사용 하도록 설정 하면 범위에 정의 된 hello hello IP 주소를가지고 있는 클라이언트만 toohello 저장소를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-139">After you enable these measures, only clients that have hello IP addresses within hello defined range can connect toohello store.</span></span>

<span data-ttu-id="d8b45-140">다른 Azure 서비스에서 Azure 데이터 팩터리 또는 Vm을 toohello Data Lake 분석 계정에 연결 되어 있는지 확인 **Azure 서비스 허용** 꺼져 **에**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-140">If other Azure services, like Azure Data Factory or VMs, connect toohello Data Lake Analytics account, make sure that **Allow Azure Services** is turned **On**.</span></span> 

### <a name="set-up-a-firewall-rule"></a><span data-ttu-id="d8b45-141">방화벽 규칙 설정</span><span class="sxs-lookup"><span data-stu-id="d8b45-141">Set up a firewall rule</span></span>

1. <span data-ttu-id="d8b45-142">Azure 포털 hello tooyour Data Lake 분석 계정을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-142">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="d8b45-143">Hello hello 왼쪽 메뉴에서 클릭 **방화벽**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-143">On hello menu on hello left, click **Firewall**.</span></span>

## <a name="add-a-new-user"></a><span data-ttu-id="d8b45-144">새 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="d8b45-144">Add a new user</span></span>

<span data-ttu-id="d8b45-145">Hello를 사용할 수 있습니다 **사용자 추가 마법사** tooeasily 새 데이터 레이크 사용자를 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-145">You can use hello **Add User Wizard** tooeasily provision new Data Lake users.</span></span>

1. <span data-ttu-id="d8b45-146">Azure 포털 hello tooyour Data Lake 분석 계정을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-146">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="d8b45-147">왼쪽 아래에서 hello에 **시작**, 클릭 **사용자 추가 마법사**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-147">On hello left, under **Getting Started**, click **Add User Wizard**.</span></span>
3. <span data-ttu-id="d8b45-148">사용자를 선택한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-148">Select a user, and then click **Select**.</span></span>
4. <span data-ttu-id="d8b45-149">역할을 선택한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-149">Select a role, and then click **Select**.</span></span> <span data-ttu-id="d8b45-150">새 개발자 toouse 선택 hello Azure 데이터 레이크를 tooset **데이터 레이크 분석 개발자** 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-150">tooset up a new developer toouse Azure Data Lake, select hello **Data Lake Analytics Developer** role.</span></span>
5. <span data-ttu-id="d8b45-151">Hello U SQL 데이터베이스에 대 한 hello 액세스 제어 목록 (Acl)을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-151">Select hello access control lists (ACLs) for hello U-SQL databases.</span></span> <span data-ttu-id="d8b45-152">선택 사항에 만족하면 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-152">When you're satisfied with your choices, click **Select**.</span></span>
6. <span data-ttu-id="d8b45-153">파일에 대 한 hello Acl을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-153">Select hello ACLs for files.</span></span> <span data-ttu-id="d8b45-154">Hello 기본 저장소에 대 한 hello 루트 폴더에 대 한 hello Acl를 변경 하지 않는 "/" 및 hello/시스템 폴더에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-154">For hello default store, don't change hello ACLs for hello root folder "/" and for hello /system folder.</span></span> <span data-ttu-id="d8b45-155">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-155">Click **Select**.</span></span>
7. <span data-ttu-id="d8b45-156">선택한 변경 내용을 모두 검토한 다음 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-156">Review all your selected changes, and then click **Run**.</span></span>
8. <span data-ttu-id="d8b45-157">Hello 마법사가 완료 되 면 클릭 **수행**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-157">When hello wizard is finished, click **Done**.</span></span>

## <a name="manage-role-based-access-control"></a><span data-ttu-id="d8b45-158">역할 기반 액세스 제어 관리</span><span class="sxs-lookup"><span data-stu-id="d8b45-158">Manage Role-Based Access Control</span></span>

<span data-ttu-id="d8b45-159">다른 Azure 서비스와 마찬가지로 사용자가 어떻게 상호 작용 하는 역할 기반 액세스 제어 (RBAC) toocontrol hello 서비스와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-159">Like other Azure services, you can use Role-Based Access Control (RBAC) toocontrol how users interact with hello service.</span></span>

<span data-ttu-id="d8b45-160">hello 표준 RBAC 역할 기능을 수행 하는 hello를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-160">hello standard RBAC roles have hello following capabilities:</span></span>
* <span data-ttu-id="d8b45-161">**소유자**: 수 작업 제출, 작업을 모니터링, 모든 사용자의 작업을 취소 하 고 hello 계정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-161">**Owner**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure hello account.</span></span>
* <span data-ttu-id="d8b45-162">**참가자**: 수 작업 제출, 작업을 모니터링, 모든 사용자의 작업을 취소 하 고 hello 계정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-162">**Contributor**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure hello account.</span></span>
* <span data-ttu-id="d8b45-163">**독자**: 작업을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-163">**Reader**: Can monitor jobs.</span></span>

<span data-ttu-id="d8b45-164">Hello 데이터 레이크 분석 개발자 역할 tooenable U-SQL 개발자 toouse hello Data Lake 분석 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-164">Use hello Data Lake Analytics Developer role tooenable U-SQL developers toouse hello Data Lake Analytics service.</span></span> <span data-ttu-id="d8b45-165">Hello 데이터 레이크 분석 개발자 역할을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-165">You can use hello Data Lake Analytics Developer role to:</span></span>
* <span data-ttu-id="d8b45-166">작업을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-166">Submit jobs.</span></span>
* <span data-ttu-id="d8b45-167">모든 사용자가 제출한 작업의 작업 상태 및 hello 진행률을 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-167">Monitor job status and hello progress of jobs submitted by any user.</span></span>
* <span data-ttu-id="d8b45-168">모든 사용자가 제출 하는 작업에서 hello U-SQL 스크립트를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d8b45-168">See hello U-SQL scripts from jobs submitted by any user.</span></span>
* <span data-ttu-id="d8b45-169">자신의 작업만을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-169">Cancel only your own jobs.</span></span>

### <a name="add-users-or-security-groups-tooa-data-lake-analytics-account"></a><span data-ttu-id="d8b45-170">사용자 또는 보안 그룹 tooa Data Lake 분석 계정 추가</span><span class="sxs-lookup"><span data-stu-id="d8b45-170">Add users or security groups tooa Data Lake Analytics account</span></span>

1. <span data-ttu-id="d8b45-171">Azure 포털 hello tooyour Data Lake 분석 계정을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-171">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="d8b45-172">**액세스 제어(IAM)** > **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-172">Click **Access control (IAM)** > **Add**.</span></span>
3. <span data-ttu-id="d8b45-173">원하는 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-173">Select a role.</span></span>
4. <span data-ttu-id="d8b45-174">사용자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-174">Add a user.</span></span>
5. <span data-ttu-id="d8b45-175">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-175">Click **OK**.</span></span>

>[!NOTE]
><span data-ttu-id="d8b45-176">사용자 또는 보안 그룹 toosubmit 작업을 필요한 경우 hello 저장소 계정에 대 한 권한이 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-176">If a user or a security group needs toosubmit jobs, they also need permission on hello store account.</span></span> <span data-ttu-id="d8b45-177">자세한 내용은 [Data Lake Store에 저장된 데이터 보호](../data-lake-store/data-lake-store-secure-data.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d8b45-177">For more information, see [Secure data stored in Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).</span></span>
>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-jobs"></a><span data-ttu-id="d8b45-178">작업 관리</span><span class="sxs-lookup"><span data-stu-id="d8b45-178">Manage jobs</span></span>

### <a name="submit-a-job"></a><span data-ttu-id="d8b45-179">작업 제출</span><span class="sxs-lookup"><span data-stu-id="d8b45-179">Submit a job</span></span>

1. <span data-ttu-id="d8b45-180">Azure 포털 hello tooyour Data Lake 분석 계정을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-180">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>

2. <span data-ttu-id="d8b45-181">**새 작업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-181">Click **New Job**.</span></span> <span data-ttu-id="d8b45-182">각 작업에 대해 다음을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-182">For each job,  configure:</span></span>

    1. <span data-ttu-id="d8b45-183">**작업 이름**: hello 작업의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-183">**Job Name**: hello name of hello job.</span></span>
    2. <span data-ttu-id="d8b45-184">**우선 순위**: 숫자가 낮을수록 우선 순위가 높습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-184">**Priority**: Lower numbers have higher priority.</span></span> <span data-ttu-id="d8b45-185">두 개의 작업이 대기 중인 경우 hello 하나 더 낮은 우선 순위 값을 먼저 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-185">If two jobs are queued, hello one with lower priority value runs first.</span></span>
    3. <span data-ttu-id="d8b45-186">**병렬 처리 수준**:이 작업에 대 한 tooreserve를 처리 하는 hello 최대 수를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-186">**Parallelism**: hello maximum number of compute processes tooreserve for this job.</span></span>

3. <span data-ttu-id="d8b45-187">**작업 제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-187">Click **Submit Job**.</span></span>

### <a name="monitor-jobs"></a><span data-ttu-id="d8b45-188">작업 모니터링</span><span class="sxs-lookup"><span data-stu-id="d8b45-188">Monitor jobs</span></span>

1. <span data-ttu-id="d8b45-189">Azure 포털 hello tooyour Data Lake 분석 계정을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-189">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="d8b45-190">**모든 작업 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-190">Click **View All Jobs**.</span></span> <span data-ttu-id="d8b45-191">Hello 계정에서 모든 hello 활성 상태이 고 최근에 완료 된 작업의 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-191">A list of all hello active and recently finished jobs in hello account is shown.</span></span>
3. <span data-ttu-id="d8b45-192">필요에 따라 **필터** 하 여 hello 작업을 찾을 toohelp **시간 범위**, **작업 이름**, 및 **작성자** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-192">Optionally, click **Filter** toohelp you find hello jobs by **Time Range**, **Job Name**, and **Author** values.</span></span> 

### <a name="monitoring-pipeline-jobs"></a><span data-ttu-id="d8b45-193">파이프라인 작업 모니터링</span><span class="sxs-lookup"><span data-stu-id="d8b45-193">Monitoring pipeline jobs</span></span>
<span data-ttu-id="d8b45-194">파이프라인의 일부인 작업도 tooaccomplish 특정 시나리오 함께, 일반적으로 순차적으로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-194">Jobs that are part of a pipeline work together, usually sequentially, tooaccomplish a specific scenario.</span></span> <span data-ttu-id="d8b45-195">예를 들어, 고객 정보의 사용을 정리, 추출, 변환, 집계하는 파이프라인을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-195">For example, you can have a pipeline that cleans, extracts, transforms, aggregates usage for customer insights.</span></span> <span data-ttu-id="d8b45-196">파이프라인 작업이 hello 작업이 제출 된 경우 hello "파이프라인" 속성을 사용 하 여 식별 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-196">Pipeline jobs are identified using hello "Pipeline" property when hello job was submitted.</span></span> <span data-ttu-id="d8b45-197">ADF V2를 사용하여 예약된 작업에는 이 속성이 자동으로 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-197">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span> 

<span data-ttu-id="d8b45-198">파이프라인의 일부인 U-SQL 작업 목록이 tooview:</span><span class="sxs-lookup"><span data-stu-id="d8b45-198">tooview a list of U-SQL jobs that are part of pipelines:</span></span> 

1. <span data-ttu-id="d8b45-199">Azure 포털 hello tooyour Data Lake 분석 계정 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-199">In hello Azure portal, go tooyour Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="d8b45-200">**작업 정보**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-200">Click **Job Insights**.</span></span> <span data-ttu-id="d8b45-201">"모든 작업이" 탭 기본값은 실행 중, 목록을 보여 주는 hello 큐에 대기 하 고 작업을 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-201">hello "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="d8b45-202">Hello 클릭 **파이프라인 작업** 탭 합니다. 파이프라인 작업 목록에 각 파이프라인에 대해 집계된 통계가 함께 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-202">Click hello **Pipeline Jobs** tab. A list of pipeline jobs will be shown along with aggregated statistics for each pipeline.</span></span>

### <a name="monitoring-recurring-jobs"></a><span data-ttu-id="d8b45-203">되풀이 작업 모니터링</span><span class="sxs-lookup"><span data-stu-id="d8b45-203">Monitoring recurring jobs</span></span>
<span data-ttu-id="d8b45-204">Hello 된 되풀이 작업은 동일한 비즈니스 논리는 하지만 서로 다른 입력된 데이터를 사용 될 때마다 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-204">A recurring job is one that has hello same business logic but uses different input data every time it runs.</span></span> <span data-ttu-id="d8b45-205">이상적으로 되풀이 작업 항상 성공 하 고 실행 시간이 상대적으로 안정적인; 이러한 동작은 모니터링 hello 작업은 정상 상태를 확인 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-205">Ideally, recurring jobs should always succeed, and have relatively stable execution time; monitoring these behaviors will help ensure hello job is healthy.</span></span> <span data-ttu-id="d8b45-206">되풀이 작업 hello "Recurrence" 속성을 사용 하 여 식별 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-206">Recurring jobs are identified using hello "Recurrence" property.</span></span> <span data-ttu-id="d8b45-207">ADF V2를 사용하여 예약된 작업에는 이 속성이 자동으로 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-207">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span>

<span data-ttu-id="d8b45-208">tooview U-SQL 작업 되풀이 되는 목록:</span><span class="sxs-lookup"><span data-stu-id="d8b45-208">tooview a list of U-SQL jobs that are recurring:</span></span> 

1. <span data-ttu-id="d8b45-209">Azure 포털 hello tooyour Data Lake 분석 계정 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-209">In hello Azure portal, go tooyour Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="d8b45-210">**작업 정보**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-210">Click **Job Insights**.</span></span> <span data-ttu-id="d8b45-211">"모든 작업이" 탭 기본값은 실행 중, 목록을 보여 주는 hello 큐에 대기 하 고 작업을 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-211">hello "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="d8b45-212">Hello 클릭 **되풀이 작업** 탭 합니다. 되풀이 작업 목록에 각 되풀이 작업에 대해 집계된 통계가 함께 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-212">Click hello **Recurring Jobs** tab. A list of recurring jobs will be shown along with aggregated statistics for each recurring job.</span></span>

## <a name="manage-policies"></a><span data-ttu-id="d8b45-213">정책 관리</span><span class="sxs-lookup"><span data-stu-id="d8b45-213">Manage policies</span></span>

### <a name="account-level-policies"></a><span data-ttu-id="d8b45-214">계정 수준 정책</span><span class="sxs-lookup"><span data-stu-id="d8b45-214">Account-level policies</span></span>

<span data-ttu-id="d8b45-215">이러한 정책은 tooall 작업 Data Lake 분석 계정에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-215">These policies apply tooall jobs in a Data Lake Analytics account.</span></span>

#### <a name="maximum-number-of-aus-in-a-data-lake-analytics-account"></a><span data-ttu-id="d8b45-216">Data Lake Analytics 계정의 최대 AU 수</span><span class="sxs-lookup"><span data-stu-id="d8b45-216">Maximum number of AUs in a Data Lake Analytics account</span></span>
<span data-ttu-id="d8b45-217">정책은 hello Data Lake 분석 계정 צ ְ ײ 분석 단위 (AUs)의 총 수를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-217">A policy controls hello total number of Analytics Units (AUs) your Data Lake Analytics account can use.</span></span> <span data-ttu-id="d8b45-218">기본적으로 hello 값 too250을 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-218">By default, hello value is set too250.</span></span> <span data-ttu-id="d8b45-219">예를 들어이 값은 too250 AUs 설정, 있습니다 있으면 250 할당 AUs tooit를 실행 하는 하나의 작업 또는 25와 실행 중인 10 작업 AUs 각 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-219">For example, if this value is set too250 AUs, you can have one job running with 250 AUs assigned tooit, or 10 jobs running with 25 AUs each.</span></span> <span data-ttu-id="d8b45-220">전송 된 작업을 추가로 hello 실행 중인 작업이 완료 될 때까지 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-220">Additional jobs that are submitted are queued until hello running jobs are finished.</span></span> <span data-ttu-id="d8b45-221">Hello 높아질 AUs 실행 중인 작업이 완료 되 면 작업 toorun 큐에 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-221">When running jobs are finished, AUs are freed up for hello queued jobs toorun.</span></span>

<span data-ttu-id="d8b45-222">toochange hello 수 AUs Data Lake 분석 계정에 대 한:</span><span class="sxs-lookup"><span data-stu-id="d8b45-222">toochange hello number of AUs for your Data Lake Analytics account:</span></span>

1. <span data-ttu-id="d8b45-223">Azure 포털 hello tooyour Data Lake 분석 계정을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-223">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="d8b45-224">**속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-224">Click **Properties**.</span></span>
3. <span data-ttu-id="d8b45-225">아래 **최대 AUs**hello 슬라이더 tooselect 값을 옮기거나 hello 값 hello 텍스트 상자에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-225">Under **Maximum AUs**, move hello slider tooselect a value, or enter hello value in hello text box.</span></span> 
4. <span data-ttu-id="d8b45-226">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-226">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="d8b45-227">기본 (250) hello 하지 더 필요한 경우 AUs, hello 포털에서을 클릭 **도움말 + 지원** toosubmit 지원 요청.</span><span class="sxs-lookup"><span data-stu-id="d8b45-227">If you need more than hello default (250) AUs, in hello portal, click **Help+Support** toosubmit a support request.</span></span> <span data-ttu-id="d8b45-228">Data Lake 분석 계정에 사용할 수 있는 AUs hello 수를 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-228">hello number of AUs available in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="maximum-number-of-jobs-that-can-run-simultaneously"></a><span data-ttu-id="d8b45-229">동시에 실행될 수 있는 최대 작업 수</span><span class="sxs-lookup"><span data-stu-id="d8b45-229">Maximum number of jobs that can run simultaneously</span></span>
<span data-ttu-id="d8b45-230">정책에서 제어 하는 작업 수 hello에 실행할 수 있습니다 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-230">A policy controls how many jobs can run at hello same time.</span></span> <span data-ttu-id="d8b45-231">기본적으로이 값 too20을 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-231">By default, this value is set too20.</span></span> <span data-ttu-id="d8b45-232">데이터 레이크 분석 AUs 사용할 수 있으면 hello 실행 중인 작업의 총 수에는이 정책의 hello 값에 도달할 때까지 즉시 새 작업에 예약 된 toorun은입니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-232">If your Data Lake Analytics has AUs available, new jobs are scheduled toorun immediately until hello total number of running jobs reaches hello value of this policy.</span></span> <span data-ttu-id="d8b45-233">Hello 동시에 실행할 수 있는 작업의 최대 수에 도달 하면 후속 작업 (AU 가용성)에 따라 하나 이상의 실행 중인 작업이 완료 될 때까지 우선 순위에 따라 대기 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-233">When you reach hello maximum number of jobs that can run simultaneously, subsequent jobs are queued in priority order until one or more running jobs complete (depending on AU availability).</span></span>

<span data-ttu-id="d8b45-234">동시에 실행할 수 있습니다. 있는 작업 toochange hello 수:</span><span class="sxs-lookup"><span data-stu-id="d8b45-234">toochange hello number of jobs that can run simultaneously:</span></span>

1. <span data-ttu-id="d8b45-235">Azure 포털 hello tooyour Data Lake 분석 계정을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-235">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="d8b45-236">**속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-236">Click **Properties**.</span></span>
3. <span data-ttu-id="d8b45-237">아래 **실행 작업의 최대 수**hello 슬라이더 tooselect 값을 옮기거나 hello 값 hello 텍스트 상자에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-237">Under **Maximum Number of Running Jobs**, move hello slider tooselect a value, or enter hello value in hello text box.</span></span> 
4. <span data-ttu-id="d8b45-238">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-238">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="d8b45-239">Toorun hello hello 포털에서 작업의 기본 (20) 번호 보다 클릭 더 필요한 경우 **도움말 + 지원** toosubmit 지원 요청.</span><span class="sxs-lookup"><span data-stu-id="d8b45-239">If you need toorun more than hello default (20) number of jobs, in hello portal, click **Help+Support** toosubmit a support request.</span></span> <span data-ttu-id="d8b45-240">hello Data Lake 분석 계정에 동시에 실행할 수 있는 작업 수를 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-240">hello number of jobs that can run simultaneously in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="how-long-tookeep-job-metadata-and-resources"></a><span data-ttu-id="d8b45-241">시간 tookeep 작업 메타 데이터 및 리소스</span><span class="sxs-lookup"><span data-stu-id="d8b45-241">How long tookeep job metadata and resources</span></span> 
<span data-ttu-id="d8b45-242">U-SQL 작업을 실행 하는 사용자가 hello Data Lake 분석 서비스에 관련 된 모든 파일은 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-242">When your users run U-SQL jobs, hello Data Lake Analytics service retains all related files.</span></span> <span data-ttu-id="d8b45-243">관련된 파일 hello U-SQL 스크립트를 hello U-SQL 스크립트, 컴파일된 리소스 및 통계에서 참조 하는 hello DLL 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-243">Related files include hello U-SQL script, hello DLL files referenced in hello U-SQL script, compiled resources, and statistics.</span></span> <span data-ttu-id="d8b45-244">hello 파일이 hello 기본 Azure 데이터 레이크 저장소 계정의 hello /system/ 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-244">hello files are in hello /system/ folder of hello default Azure Data Lake Storage account.</span></span> <span data-ttu-id="d8b45-245">이 정책은 이러한 리소스를 자동으로 삭제 되기 전에 저장 되는 기간을 제어 (hello 기본값은 30 일)입니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-245">This policy controls how long these resources are stored before they are automatically deleted (hello default is 30 days).</span></span> <span data-ttu-id="d8b45-246">디버깅을 위해 및 hello 향후에 다시 실행할 수 있는 작업의 성능 튜닝에 이러한 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-246">You can use these files for debugging, and for performance-tuning of jobs that you'll rerun in hello future.</span></span>

<span data-ttu-id="d8b45-247">toochange 시간 tookeep 작업 메타 데이터 및 리소스:</span><span class="sxs-lookup"><span data-stu-id="d8b45-247">toochange how long tookeep job metadata and resources:</span></span>

1. <span data-ttu-id="d8b45-248">Azure 포털 hello tooyour Data Lake 분석 계정을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-248">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="d8b45-249">**속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-249">Click **Properties**.</span></span>
3. <span data-ttu-id="d8b45-250">아래 **일 tooRetain 작업 쿼리**hello 슬라이더 tooselect 값을 옮기거나 hello 값 hello 텍스트 상자에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-250">Under **Days tooRetain Job Queries**, move hello slider tooselect a value, or enter hello value in hello text box.</span></span>  
4. <span data-ttu-id="d8b45-251">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-251">Click **Save**.</span></span>

### <a name="job-level-policies"></a><span data-ttu-id="d8b45-252">작업 수준 정책</span><span class="sxs-lookup"><span data-stu-id="d8b45-252">Job-level policies</span></span>
<span data-ttu-id="d8b45-253">작업 수준 정책을 사용 하 여 제어할 수 있습니다 최대 AUs hello 및 hello 개별 사용자 (또는 특정 보안 그룹의 구성원) 전송 하는 작업에 설정할 수 있는 최대 우선 순위입니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-253">With job-level policies, you can control hello maximum AUs and hello maximum priority that individual users (or members of specific security groups) can set on jobs that they submit.</span></span> <span data-ttu-id="d8b45-254">사용자가 발생 하는 hello 비용을 제어할 수이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-254">This lets you control hello costs incurred by users.</span></span> <span data-ttu-id="d8b45-255">수도 있습니다 우선 순위가 높은 예약 된 작업을 제어 hello 효과 미칠 수에서 실행 되는 프로덕션 작업 hello 동일한 Data Lake 분석 계정.</span><span class="sxs-lookup"><span data-stu-id="d8b45-255">It also lets you control hello effect that scheduled jobs might have on high-priority production jobs that are running in hello same Data Lake Analytics account.</span></span>

<span data-ttu-id="d8b45-256">Data Lake 분석 hello 작업 수준에서 설정할 수 있는 두 가지 정책에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-256">Data Lake Analytics has two policies that you can set at hello job level:</span></span>

* <span data-ttu-id="d8b45-257">**작업당 AU 제한**: 사용자가 AUs toothis 수를 가진 작업을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-257">**AU limit per job**: Users can only submit jobs that have up toothis number of AUs.</span></span> <span data-ttu-id="d8b45-258">기본적으로이 한도 hello AU 상한 hello 계정에 대 한 동일한 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-258">By default, this limit is hello same as hello maximum AU limit for hello account.</span></span>
* <span data-ttu-id="d8b45-259">**우선 순위**: 사용자가 우선 순위 보다 낮거나 toothis 값을 가진 작업을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-259">**Priority**: Users can only submit jobs that have a priority lower than or equal toothis value.</span></span> <span data-ttu-id="d8b45-260">숫자가 높을수록 우선 순위가 낮습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-260">Note that a higher number means a lower priority.</span></span> <span data-ttu-id="d8b45-261">기본적으로이 설정은 too1, hello 가능한 우선 순위가 가장 높은 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-261">By default, this is set too1, which is hello highest possible priority.</span></span>

<span data-ttu-id="d8b45-262">모든 계정에는 설정된 기본 정책이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-262">There is a default policy set on every account.</span></span> <span data-ttu-id="d8b45-263">hello 기본 정책은 hello 계정의 tooall 사용자가 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-263">hello default policy applies tooall users of hello account.</span></span> <span data-ttu-id="d8b45-264">특정 사용자 및 그룹에 대한 추가 정책을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-264">You can set additional policies for specific users and groups.</span></span> 

> [!NOTE]
> <span data-ttu-id="d8b45-265">계정 수준 정책 및 작업 수준 정책은 동시에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-265">Account-level policies and job-level policies apply simultaneously.</span></span>
>

#### <a name="add-a-policy-for-a-specific-user-or-group"></a><span data-ttu-id="d8b45-266">특정 사용자 또는 그룹에 대한 정책 추가</span><span class="sxs-lookup"><span data-stu-id="d8b45-266">Add a policy for a specific user or group</span></span>

1. <span data-ttu-id="d8b45-267">Azure 포털 hello tooyour Data Lake 분석 계정을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-267">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="d8b45-268">**속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-268">Click **Properties**.</span></span>
3. <span data-ttu-id="d8b45-269">아래 **작업 제출 제한**, hello 클릭 **정책 추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-269">Under **Job Submission Limits**, click hello **Add Policy** button.</span></span> <span data-ttu-id="d8b45-270">그런 다음 선택 하거나 hello 설정을 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-270">Then, select or enter hello following settings:</span></span>
    1. <span data-ttu-id="d8b45-271">**정책 이름 계산**: tooremind 정책 이름을 입력 하면 hello 정책의 hello 목적입니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-271">**Compute Policy Name**: Enter a policy name, tooremind you of hello purpose of hello policy.</span></span>
    2. <span data-ttu-id="d8b45-272">**사용자 또는 그룹 선택**: hello 사용자 또는이 정책이 적용 되는 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-272">**Select User or Group**: Select hello user or group this policy applies to.</span></span>
    3. <span data-ttu-id="d8b45-273">**Hello 작업 AU 제한 설정**: toohello 적용 되는 hello AU 제한 설정 사용자 또는 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-273">**Set hello Job AU Limit**: Set hello AU limit that applies toohello selected user or group.</span></span>
    4. <span data-ttu-id="d8b45-274">**우선 순위 제한 hello 설정**: hello 우선 순위 제한 설정 toohello 적용 되는 사용자 또는 그룹 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-274">**Set hello Priority Limit**: Set hello priority limit that applies toohello selected user or group.</span></span>

4. <span data-ttu-id="d8b45-275">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-275">Click **Ok**.</span></span>

5. <span data-ttu-id="d8b45-276">새 정책 hello hello에 나열 된 **기본** 정책 테이블 **작업 제출 제한**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-276">hello new policy is listed in hello **Default** policy table, under **Job Submission Limits**.</span></span> 

#### <a name="delete-or-edit-an-existing-policy"></a><span data-ttu-id="d8b45-277">기존 정책 삭제 또는 편집</span><span class="sxs-lookup"><span data-stu-id="d8b45-277">Delete or edit an existing policy</span></span>

1. <span data-ttu-id="d8b45-278">Azure 포털 hello tooyour Data Lake 분석 계정을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-278">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="d8b45-279">**속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-279">Click **Properties**.</span></span>
3. <span data-ttu-id="d8b45-280">아래 **작업 제출 제한**, tooedit 원하는 찾기 hello 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="d8b45-280">Under **Job Submission Limits**, find hello policy you want tooedit.</span></span>
4.  <span data-ttu-id="d8b45-281">toosee hello **삭제** 및 **편집** hello hello 테이블의 맨 오른쪽 열에 해당 하는 옵션을 클릭 **중...** .</span><span class="sxs-lookup"><span data-stu-id="d8b45-281">toosee hello **Delete** and **Edit** options, in hello rightmost column of hello table, click **...**.</span></span>

### <a name="additional-resources-for-job-policies"></a><span data-ttu-id="d8b45-282">정책 작업에 대한 추가 리소스</span><span class="sxs-lookup"><span data-stu-id="d8b45-282">Additional resources for job policies</span></span>
* <span data-ttu-id="d8b45-283">[Policy overview blog post](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-overview/)(정책 개요 블로그 게시물)</span><span class="sxs-lookup"><span data-stu-id="d8b45-283">[Policy overview blog post](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-overview/)</span></span>
* <span data-ttu-id="d8b45-284">[Account-level policies blog post](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-account-level-policy/)(계정 수준 정책 블로그 게시물)</span><span class="sxs-lookup"><span data-stu-id="d8b45-284">[Account-level policies blog post](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-account-level-policy/)</span></span>
* <span data-ttu-id="d8b45-285">[Job-level policies blog post](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-job-level-policy/)(작업 수준 정책 블로그 게시물)</span><span class="sxs-lookup"><span data-stu-id="d8b45-285">[Job-level policies blog post](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-job-level-policy/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8b45-286">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d8b45-286">Next steps</span></span>

* [<span data-ttu-id="d8b45-287">Azure Data Lake Analytics 개요</span><span class="sxs-lookup"><span data-stu-id="d8b45-287">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="d8b45-288">데이터 레이크 분석 hello Azure 포털을 사용 하 여 시작</span><span class="sxs-lookup"><span data-stu-id="d8b45-288">Get started with Data Lake Analytics by using hello Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="d8b45-289">Azure PowerShell을 사용하여 Azure Data Lake Analytics 관리</span><span class="sxs-lookup"><span data-stu-id="d8b45-289">Manage Azure Data Lake Analytics by using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)

