---
title: "Azure Site Recovery와 aaaEnable Hyper-v 복제 tooa 보조 사이트 | Microsoft Docs"
description: "어떻게 tooa 복제 Hyper-v Vm에 대 한 복제 tooenable 보조 System Center VMM 인 사이트를 Azure Site Recovery에 설명 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d8782d14-9fef-4396-8912-ff945efc851b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: b4484e0118cb23f343187fe867d9795d30926baf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-enable-replication-tooa-secondary-site-for-hyper-v-vms"></a><span data-ttu-id="9727e-103">9 단계: Hyper-v Vm에 대 한 복제 tooa 보조 사이트를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="9727e-103">Step 9: Enable replication tooa secondary site for Hyper-V VMs</span></span>


<span data-ttu-id="9727e-104">복제 정책을 설정한 후이 사이트를 사용할 문서 tooenable 복제 tooa 보조 System Center Virtual Machine Manager (VMM) 온-프레미스 Hyper-v 가상 컴퓨터 (VM)를 사용 하 여 [Azure Site Recovery](site-recovery-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9727e-104">After setting up a replication policy, use this article tooenable replication tooa secondary System Center Virtual Machine Manager (VMM) site for on-premises Hyper-V virtual machines (VM), using [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="9727e-105">이 문서를 읽은 후 게시 설명을 hello 맨 아래에 하거나 hello에 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="9727e-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="select-vms-tooreplicate"></a><span data-ttu-id="9727e-106">Vm tooreplicate 선택</span><span class="sxs-lookup"><span data-stu-id="9727e-106">Select VMs tooreplicate</span></span>

1. <span data-ttu-id="9727e-107">**2단계: 응용 프로그램 복제** > **원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9727e-107">Click **Step 2: Replicate application** > **Source**.</span></span> 

    ![복제 활성화](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication1.png)

2. <span data-ttu-id="9727e-109">**소스**hello VMM 서버를 선택 하 고 hello 클라우드는 hello tooreplicate 추가할 Hyper-v 호스트 위치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9727e-109">In **Source**, select hello VMM server, and hello cloud in which hello Hyper-V hosts you want tooreplicate are located.</span></span> <span data-ttu-id="9727e-110">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9727e-110">Then click **OK**.</span></span>

    ![복제 활성화](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication2.png)
3. <span data-ttu-id="9727e-112">**대상**, hello 보조 VMM 서버와 클라우드를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9727e-112">In **Target**, verify hello secondary VMM server and cloud.</span></span>
4. <span data-ttu-id="9727e-113">**가상 컴퓨터**, tooprotect hello 목록에서 원하는 hello Vm을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9727e-113">In **Virtual machines**, select hello VMs you want tooprotect from hello list.</span></span>

    ![가상 컴퓨터 보호 사용](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication5.png)

<span data-ttu-id="9727e-115">Hello의 진행률을 추적할 수 있습니다 **보호 사용** 동작에서 **작업** > **사이트 복구 작업이**합니다.</span><span class="sxs-lookup"><span data-stu-id="9727e-115">You can track progress of hello **Enable Protection** action in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="9727e-116">Hello 후 **보호 완료** 작업을 완료 하 고 hello 초기 복제가 완료 되 면 hello 가상 컴퓨터가 장애 조치에 대해 준비 되었는지 합니다.</span><span class="sxs-lookup"><span data-stu-id="9727e-116">After hello **Finalize Protection** job completes, hello initial replication is complete, and hello virtual machine is ready for failover.</span></span>

<span data-ttu-id="9727e-117">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="9727e-117">Note that:</span></span>

- <span data-ttu-id="9727e-118">Hello VMM 콘솔에서 가상 컴퓨터에 대 한 보호를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9727e-118">You can also enable protection for virtual machines in hello VMM console.</span></span> <span data-ttu-id="9727e-119">클릭 **보호 사용** hello 가상 컴퓨터 속성에서 hello 도구 모음 > **Azure Site Recovery** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9727e-119">Click **Enable Protection** on hello toolbar in hello virtual machine properties > **Azure Site Recovery** tab.</span></span>
- <span data-ttu-id="9727e-120">복제를 사용 하도록 설정한 후에 VM hello에 대 한 속성을 볼 수 있습니다에 **복제 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="9727e-120">After you've enabled replication, you can view properties for hello VM in **Replicated Items**.</span></span> <span data-ttu-id="9727e-121">Hello에 **Essentials** 대시보드를 hello VM 및 서버 인스턴스의 상태에 대 한 hello 복제 정책에 대 한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9727e-121">On hello **Essentials** dashboard, you can see information about hello replication policy for hello VM and its status.</span></span> <span data-ttu-id="9727e-122">자세한 내용을 보려면 **속성** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9727e-122">Click **Properties** for more details.</span></span>

## <a name="onboard-existing-vms"></a><span data-ttu-id="9727e-123">기존 VM 온보딩</span><span class="sxs-lookup"><span data-stu-id="9727e-123">Onboard existing VMs</span></span>

<span data-ttu-id="9727e-124">Hyper-V 복제본을 사용하여 복제 중인 기존 가상 컴퓨터가 VMM에 있는 경우 Azure Site Recovery 복제를 위해 다음과 같이 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9727e-124">If you have existing virtual machines in VMM that are replicating with Hyper-V Replica, you can onboard them for Azure Site Recovery replication as follows:</span></span>

1. <span data-ttu-id="9727e-125">Hello 기존 VM을 호스트 하는 hello Hyper-v 서버 hello 기본 클라우드에 위치한 hello 복제본 가상 컴퓨터를 호스팅하는 hello Hyper-v 서버 hello 보조 클라우드에 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="9727e-125">Ensure that hello Hyper-V server hosting hello existing VM is located in hello primary cloud, and that hello Hyper-V server hosting hello replica virtual machine is located in hello secondary cloud.</span></span>
2. <span data-ttu-id="9727e-126">기본 VMM 클라우드 hello에 대 한 복제 정책이 구성 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9727e-126">Make sure a replication policy is configured for hello primary VMM cloud.</span></span>
3. <span data-ttu-id="9727e-127">Hello 주 가상 컴퓨터에 대 한 복제를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9727e-127">Enable replication for hello primary virtual machine.</span></span> <span data-ttu-id="9727e-128">Azure 사이트 복구 및 VMM hello 동일한 복제본 호스트 및 가상 컴퓨터가 감지 되는지, 및 Azure 사이트 복구를 다시 사용 hello를 사용 하 여 다시 시작 복제 설정을 지정을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9727e-128">Azure Site Recovery and VMM ensure that hello same replica host and virtual machine is detected, and Azure Site Recovery will reuse and reestablish replication using hello specified settings.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9727e-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9727e-129">Next steps</span></span>

<span data-ttu-id="9727e-130">너무 이동[10 단계: 테스트 장애 조치 실행](vmm-to-vmm-walkthrough-test-failover.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9727e-130">Go too[Step 10: Run a test failover](vmm-to-vmm-walkthrough-test-failover.md).</span></span>
