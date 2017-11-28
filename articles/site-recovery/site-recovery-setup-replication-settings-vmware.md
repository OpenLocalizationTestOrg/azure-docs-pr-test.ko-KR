---
title: "Azure Site Recovery에 대 한 복제 설정을 aaaSet | Microsoft Docs"
description: "Toodeploy 사이트 복구 tooorchestrate 복제, 장애 조치 및 복구 VMM에서 Hyper-v Vm의 클라우드 tooAzure 방법을 설명 합니다."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: rayne-wiselman
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: 618e92e42411732a2a1bb75c5e5ea8a433cd7d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-replication-policy-for-vmware-tooazure"></a><span data-ttu-id="c4ea2-103">VMware tooAzure에 대 한 복제 정책 관리</span><span class="sxs-lookup"><span data-stu-id="c4ea2-103">Manage replication policy for VMware tooAzure</span></span>


## <a name="create-a-replication-policy"></a><span data-ttu-id="c4ea2-104">복제 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="c4ea2-104">Create a replication policy</span></span>

1. <span data-ttu-id="c4ea2-105">**관리** > **Site Recovery 인프라**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-105">Select **Manage** > **Site Recovery Infrastructure**.</span></span>
2. <span data-ttu-id="c4ea2-106">**VMware 및 실제 컴퓨터의 경우** 아래에서 **복제 정책**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-106">Select **Replication policies** under **For VMware and Physical machines**.</span></span>
3. <span data-ttu-id="c4ea2-107">**+ 복제 정책**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-107">Select **+Replication policy**.</span></span>

    ![복제 정책 만들기](./media/site-recovery-setup-replication-settings-vmware/createpolicy.png)

4. <span data-ttu-id="c4ea2-109">Hello 정책 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-109">Enter hello policy name.</span></span>

5. <span data-ttu-id="c4ea2-110">**RPO 임계값**, hello RPO 제한을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-110">In **RPO threshold**, specify hello RPO limit.</span></span> <span data-ttu-id="c4ea2-111">연속 복제가 이 제한을 초과하면 경고가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-111">Alerts will be generated when continuous replication exceeds this limit.</span></span>
6. <span data-ttu-id="c4ea2-112">**복구 지점 보존**, (시간) 지정 hello 각 복구 지점에 대 한 hello 보존 윈도의 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-112">In **Recovery point retention**, specify (in hours) hello duration of hello retention window for each recovery point.</span></span> <span data-ttu-id="c4ea2-113">보호 된 컴퓨터 수 있는 보존 기간 내 tooany 데이터 요소를 복구 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-113">Protected machines can be recovered tooany point within a retention window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c4ea2-114">컴퓨터가 복제 된 toopremium 저장소에 대 한 too24 시간 보존을 모두 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-114">Up too24 hours of retention is supported for machines replicated toopremium storage.</span></span> <span data-ttu-id="c4ea2-115">컴퓨터가 복제 된 toostandard 저장소에 대 한 too72 시간 보존을 모두 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-115">Up too72 hours of retention is supported for machines replicated toostandard storage.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c4ea2-116">장애 복구에 대한 복제 정책은 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-116">A replication policy for failback is automatically created.</span></span>

7. <span data-ttu-id="c4ea2-117">**앱 일치 스냅숏 빈도**에서 응용 프로그램 일치 스냅숏이 포함된 복구 지점을 만드는 빈도(분)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-117">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points that contain application-consistent snapshots will be created.</span></span>

8. <span data-ttu-id="c4ea2-118">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-118">Click **OK**.</span></span> <span data-ttu-id="c4ea2-119">hello 정책 30 too60 초 내에 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-119">hello policy should be created in 30 too60 seconds.</span></span>

![복제 정책 생성](./media/site-recovery-setup-replication-settings-vmware/Creating-Policy.png)

## <a name="associate-a-configuration-server-with-a-replication-policy"></a><span data-ttu-id="c4ea2-121">복제 정책과 구성 서버 연결</span><span class="sxs-lookup"><span data-stu-id="c4ea2-121">Associate a configuration server with a replication policy</span></span>
1. <span data-ttu-id="c4ea2-122">Hello 복제 정책 toowhich 선택 tooassociate hello 구성 서버를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-122">Choose hello replication policy toowhich you want tooassociate hello configuration server.</span></span>
2. <span data-ttu-id="c4ea2-123">**연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-123">Click **Associate**.</span></span>
<span data-ttu-id="c4ea2-124">![구성 서버 연결](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span><span class="sxs-lookup"><span data-stu-id="c4ea2-124">![Associate configuration server](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span></span>

3. <span data-ttu-id="c4ea2-125">서버 hello 목록에서 hello 구성 서버를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-125">Select hello configuration server from hello list of servers.</span></span>
4. <span data-ttu-id="c4ea2-126">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-126">Click **OK**.</span></span> <span data-ttu-id="c4ea2-127">하나의 tootwo 분에서 hello 구성 서버를 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-127">hello configuration server should be associated in one tootwo minutes.</span></span>

![구성 서버 연결](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-2.png)

## <a name="edit-a-replication-policy"></a><span data-ttu-id="c4ea2-129">복제 정책 편집</span><span class="sxs-lookup"><span data-stu-id="c4ea2-129">Edit a replication policy</span></span>
1. <span data-ttu-id="c4ea2-130">Tooedit 복제 설정을 검색할 hello 복제 정책을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-130">Choose hello replication policy for which you want tooedit replication settings.</span></span>
<span data-ttu-id="c4ea2-131">![복제 정책 편집](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="c4ea2-131">![Edit replication policy](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span></span>

2. <span data-ttu-id="c4ea2-132">**설정 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-132">Click **Edit Settings**.</span></span>
<span data-ttu-id="c4ea2-133">![복제 정책 설정 편집](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="c4ea2-133">![Edit replication policy settings](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span></span>

3. <span data-ttu-id="c4ea2-134">필요에 따라 hello 설정을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-134">Change hello settings based on your need.</span></span>
4. <span data-ttu-id="c4ea2-135">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-135">Click **Save**.</span></span> <span data-ttu-id="c4ea2-136">hello 정책 2 toofive 분 저장 하도록, Vm 수에 따라는 해당 복제 정책을 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-136">hello policy should be saved in two toofive minutes, depending on how many VMs are using that replication policy.</span></span>

![복제 정책 저장](./media/site-recovery-setup-replication-settings-vmware/Save-Policy.png)

## <a name="dissociate-a-configuration-server-from-a-replication-policy"></a><span data-ttu-id="c4ea2-138">복제 정책에서 구성 서버 분리</span><span class="sxs-lookup"><span data-stu-id="c4ea2-138">Dissociate a configuration server from a replication policy</span></span>
1. <span data-ttu-id="c4ea2-139">Hello 복제 정책 toowhich 선택 tooassociate hello 구성 서버를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-139">Choose hello replication policy toowhich you want tooassociate hello configuration server.</span></span>
2. <span data-ttu-id="c4ea2-140">**분리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-140">Click **Dissociate**.</span></span>
3. <span data-ttu-id="c4ea2-141">서버 hello 목록에서 hello 구성 서버를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-141">Select hello configuration server from hello list of servers.</span></span>
4. <span data-ttu-id="c4ea2-142">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-142">Click **OK**.</span></span> <span data-ttu-id="c4ea2-143">하나의 tootwo 분에서 hello 구성 서버를 분리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-143">hello configuration server should be dissociated in one tootwo minutes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c4ea2-144">Hello 정책을 사용 하 여 하나 이상의 복제 된 항목이 없는 경우 구성 서버를 분리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-144">You cannot dissociate a configuration server if there is at least one replicated item using hello policy.</span></span> <span data-ttu-id="c4ea2-145">Hello 구성 서버를 분리 하기 전에 hello 정책을 사용 하 여 복제 된 항목이 없는 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-145">Make sure there are no replicated items using hello policy before you dissociate hello configuration server.</span></span>

## <a name="delete-a-replication-policy"></a><span data-ttu-id="c4ea2-146">복제 정책 삭제</span><span class="sxs-lookup"><span data-stu-id="c4ea2-146">Delete a replication policy</span></span>

1. <span data-ttu-id="c4ea2-147">Hello 복제 정책을 선택 toodelete 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-147">Choose hello replication policy that you want toodelete.</span></span>
2. <span data-ttu-id="c4ea2-148">**삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-148">Click **Delete**.</span></span> <span data-ttu-id="c4ea2-149">hello 정책 30 too60 초 내에 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-149">hello policy should be deleted in 30 too60 seconds.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c4ea2-150">구성 서버가 연결 tooit 하나 이상 있는 경우에 복제 정책을 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-150">You cannot delete a replication policy if it has at least one configuration server associated tooit.</span></span> <span data-ttu-id="c4ea2-151">Hello 정책을 사용 하 여 복제 된 항목이 없습니다 및 hello 정책 삭제 하기 전에 구성 서버를 연결 된 모든 hello 삭제 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ea2-151">Make sure there are no replicated items using hello policy and delete all hello associated configuration servers before you delete hello policy.</span></span>
