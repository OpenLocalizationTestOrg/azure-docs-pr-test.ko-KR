---
title: "Azure Site Recovery와 tooAzure를 복제 하는 물리적 서버에 대 한 복제 aaaEnable | Microsoft Docs"
description: "Tooenable 복제 tooAzure에 필요한 실제 서버 hello Azure Site Recovery 서비스를 사용 하 여 hello 단계가 요약 되어 있습니다."
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 519c5559-7032-4954-b8b5-f24f5242a954
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: dde4b1463023d2ccefa498f72bb51e57d60ac0d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-enable-replication-for-physical-servers-tooazure"></a><span data-ttu-id="07748-103">10 단계: 실제 서버 tooAzure에 대 한 복제를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="07748-103">Step 10: Enable replication for physical servers tooAzure</span></span>


<span data-ttu-id="07748-104">이 문서에서는 방법에 대 한 복제 tooenable 온-프레미스 Windows/Linux를 설명 hello를 사용 하 여, 물리적 서버 tooAzure [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털에서에서 서비스 합니다.</span><span class="sxs-lookup"><span data-stu-id="07748-104">This article describes how tooenable replication for on-premises Windows/Linux physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="07748-105">Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="07748-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="07748-106">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="07748-106">Before you start</span></span>

- <span data-ttu-id="07748-107">서버 hello 있어야 [모바일 서비스 구성 요소가 설치](physical-walkthrough-install-mobility.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="07748-107">Servers must have hello [Mobility service component installed](physical-walkthrough-install-mobility.md).</span></span>
- <span data-ttu-id="07748-108">강제 설치에 대 한 VM 준비 된 경우 복제를 사용 하도록 설정 하면 프로세스 서버 hello가 자동으로 hello 모바일 서비스를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="07748-108">If a VM is prepared for push installation, hello process server automatically installs hello Mobility service when you enable replication.</span></span>
- <span data-ttu-id="07748-109">Azure 사용자 계정에 필요한 특정 복제에 대 한 컴퓨터를 사용 하도록 설정 하면 [권한을](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooensure 수 toouse Azure 저장소와는 Azure Vm을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07748-109">When you enable a machine for replication, your Azure user account needs specific [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooensure you're able toouse Azure storage, and create Azure VMs.</span></span>
- <span data-ttu-id="07748-110">를 추가 하거나 서버에 대 한 IP 주소를 수정할 때이 지나야 too15 분 또는 더 이상 하 고 변경 tootake 효과 대 한 hello 포털에서 tooappear 합니다.</span><span class="sxs-lookup"><span data-stu-id="07748-110">When you add or modify IP addresses for servers, it can take up too15 minutes or longer for changes tootake effect, and for them tooappear in hello portal.</span></span>


## <a name="exclude-disks-from-replication"></a><span data-ttu-id="07748-111">복제에서 디스크 제외</span><span class="sxs-lookup"><span data-stu-id="07748-111">Exclude disks from replication</span></span>

<span data-ttu-id="07748-112">기본적으로 컴퓨터의 모든 디스크가 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="07748-112">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="07748-113">디스크를 복제에서 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07748-113">You can exclude disks from replication.</span></span> <span data-ttu-id="07748-114">예를 들어 임시 데이터, 또는 새로 고쳐지는 데이터 때마다 컴퓨터 tooreplicate 디스크 원하지 않을 수 있습니다 또는 응용 프로그램 (예: pagefile.sys 또는 SQL Server tempdb)를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="07748-114">For example you might not want tooreplicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span> [<span data-ttu-id="07748-115">자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="07748-115">Learn more</span></span>](site-recovery-exclude-disk.md)

## <a name="replicate-servers"></a><span data-ttu-id="07748-116">서버 복제</span><span class="sxs-lookup"><span data-stu-id="07748-116">Replicate servers</span></span>

1. <span data-ttu-id="07748-117">**2단계: 응용 프로그램 복제** > **원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07748-117">Click **Step 2: Replicate application** > **Source**.</span></span>
2. <span data-ttu-id="07748-118">**소스**선택, hello 구성 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="07748-118">In **Source**, select hello configuration server.</span></span>
3. <span data-ttu-id="07748-119">**컴퓨터 형식**에서 **물리적 컴퓨터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07748-119">In **Machine type**, select **Physical Machines**.</span></span>
4. <span data-ttu-id="07748-120">Hello 프로세스 서버를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="07748-120">Select hello process server.</span></span> <span data-ttu-id="07748-121">모든 추가 프로세스 서버를 만들지 않은 경우 구성 서버 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07748-121">If you haven't created any additional process servers this will be hello configuration server.</span></span> <span data-ttu-id="07748-122">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07748-122">Then click **OK**.</span></span>
5. <span data-ttu-id="07748-123">**대상**리소스 그룹을 장애 조치 Vm toocreate hello 원하는 hello을 hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="07748-123">In **Target**, select hello subscription and hello resource group in which you want toocreate hello failed over VMs.</span></span> <span data-ttu-id="07748-124">장애 조치 Vm hello에 대 한 (기본 또는 리소스 관리), Azure에서 toouse 원하는 hello 배포 모델을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="07748-124">Choose hello deployment model that you want toouse in Azure (classic or resource management), for hello failed over VMs.</span></span>
6. <span data-ttu-id="07748-125">데이터 복제를 위한 toouse 원하는 hello Azure 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="07748-125">Select hello Azure storage account you want toouse for replicating data.</span></span> <span data-ttu-id="07748-126">Toouse를 이미 설정한 계정을 사용 하지 않으려는 경우 새를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07748-126">If you don't want toouse an account you've already set up, you can create a new one.</span></span>
7. <span data-ttu-id="07748-127">선택 hello **Azure 네트워크** 및 **서브넷** 장애 조치 후 toowhich Azure Vm에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="07748-127">Select hello **Azure network** and **Subnet** toowhich Azure VMs connect after failover.</span></span> <span data-ttu-id="07748-128">선택 **선택한 컴퓨터에 지금 구성** tooapply hello 네트워크 설정 tooall 선택한 컴퓨터에 대 한 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="07748-128">Select **Configure now for selected machines** tooapply hello network setting tooall machines you select for protection.</span></span> <span data-ttu-id="07748-129">선택 **나중에 구성** tooselect hello 컴퓨터당 Azure 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="07748-129">Select **Configure later** tooselect hello Azure network per machine.</span></span> <span data-ttu-id="07748-130">Toouse 기존 네트워크를 사용 하지 않으려는 경우 하나를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07748-130">If you don't want toouse an existing network, you can create one.</span></span>

    ![복제 활성화](./media/physical-walkthrough-enable-replication/targetsettings.png)

8. <span data-ttu-id="07748-132">**물리적 컴퓨터**, 클릭 **+ 물리적 컴퓨터** hello 입력 **이름** 및 **IP 주소**합니다.</span><span class="sxs-lookup"><span data-stu-id="07748-132">In **Physical machines**, click **+Physical machine** and enter hello **Name** and **IP address**.</span></span> <span data-ttu-id="07748-133">Hello 운영 체제를 선택 하려는 tooreplicate hello 컴퓨터의 합니다.</span><span class="sxs-lookup"><span data-stu-id="07748-133">Choose hello operating system of hello machine you want tooreplicate.</span></span> <span data-ttu-id="07748-134">컴퓨터 검색 되 고 hello 목록에 표시 될 때까지 몇 분 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="07748-134">It takes a few minutes until machines are discovered and shown in hello list.</span></span>
9. <span data-ttu-id="07748-135">**속성** > **속성 구성**을 선택 하는 hello 프로세스 서버 tooautomatically 사용한 hello 계정 hello 머신에서 hello 모바일 서비스를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="07748-135">In **Properties** > **Configure properties**, select hello account that will be used by hello process server tooautomatically install hello Mobility service on hello machine.</span></span>
10. <span data-ttu-id="07748-136">기본적으로 모든 디스크가 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="07748-136">By default all disks are replicated.</span></span> <span data-ttu-id="07748-137">클릭 **모든 디스크** tooreplicate 원하는 디스크의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="07748-137">Click **All Disks** and clear any disks you don't want tooreplicate.</span></span> <span data-ttu-id="07748-138">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07748-138">Then click **OK**.</span></span> <span data-ttu-id="07748-139">나중에 추가 VM 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07748-139">You can set additional VM properties later.</span></span>

    ![복제 활성화](./media/physical-walkthrough-enable-replication/enable-replication6.png)
11. <span data-ttu-id="07748-141">**복제 설정을** > **복제 설정을 구성**, 복제 정책을 선택 되어 올바른 해당 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="07748-141">In **Replication settings** > **Configure replication settings**, verify that hello correct replication policy is selected.</span></span> <span data-ttu-id="07748-142">정책을 수정 하면 변경 사항이 적용 된 tooreplicating 시스템과 toonew 컴퓨터 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07748-142">If you modify a policy, changes will be applied tooreplicating machine, and toonew machines.</span></span>
12. <span data-ttu-id="07748-143">사용 하도록 설정 **다중 VM 일관성** toogather 컴퓨터를 복제 그룹으로 사용할 hello 그룹의 이름을 지정 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="07748-143">Enable **Multi-VM consistency** if you want toogather machines into a replication group, and specify a name for hello group.</span></span> <span data-ttu-id="07748-144">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07748-144">Then click **OK**.</span></span> <span data-ttu-id="07748-145">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="07748-145">Note that:</span></span>

    * <span data-ttu-id="07748-146">복제 그룹의 컴퓨터는 함께 복제되고 장애 조치(failover) 시 공유 크래시 일관성 및 앱 일치 복구 지점을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="07748-146">Machines in replication groups replicate together, and have shared crash-consistent and app-consistent recovery points when they fail over.</span></span>
    * <span data-ttu-id="07748-147">워크로드를 미러링하도록 물리적 서버를 함께 수집하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="07748-147">We recommend that you gather physical servers together so that they mirror your workloads.</span></span> <span data-ttu-id="07748-148">작업 성능에 영향을 줄 수 다중 VM 일관성이 사용 하도록 설정 하 고 컴퓨터가 hello를 실행 하는 경우에 사용 해야 동일한 작업 및 일관성에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="07748-148">Enabling multi-VM consistency can impact workload performance, and should only be used if machines are running hello same workload and you need consistency.</span></span>

13. <span data-ttu-id="07748-149">**복제 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07748-149">Click **Enable Replication**.</span></span> <span data-ttu-id="07748-150">Hello의 진행률을 추적할 수 있습니다 **보호 사용** 작업 **설정** > **작업** > **사이트 복구 작업이**.</span><span class="sxs-lookup"><span data-stu-id="07748-150">You can track progress of hello **Enable Protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span> <span data-ttu-id="07748-151">Hello 후 **보호 완료** 실행 작업 hello 컴퓨터는 장애 조치에 대해 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="07748-151">After hello **Finalize Protection** job runs hello machine is ready for failover.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07748-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="07748-152">Next steps</span></span>

<span data-ttu-id="07748-153">너무 이동[11 단계: 테스트 장애 조치 실행](physical-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="07748-153">Go too[Step 11: Run a test failover](physical-walkthrough-test-failover.md)</span></span>
