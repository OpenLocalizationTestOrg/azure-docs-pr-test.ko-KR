---
title: "VMM에서 Hyper-v Vm을 복제 하기 위한 네트워크 매핑 aaaConfigure 클라우드의 Azure Site Recovery와 tooAzure | Microsoft Docs"
description: "Tooconfigure 네트워크 매핑을 VMM에서 Hyper-v Vm을 복제 하는 경우 클라우드를 Azure Site Recovery와 tooAzure 방법을 설명 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 081a9fdb0ffa4114099e9bcb9c1b1e43ad26ecbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-configure-network-mapping-for-hyper-v-replication-with-vmm-tooazure"></a><span data-ttu-id="655df-103">9 단계: Hyper-v (VMM)와 복제 tooAzure에 대 한 네트워크 매핑 구성</span><span class="sxs-lookup"><span data-stu-id="655df-103">Step 9: Configure network mapping for Hyper-V replication (with VMM) tooAzure</span></span>

<span data-ttu-id="655df-104">Hello를 설정한 후 [원본 및 대상 복제 설정을](vmm-to-azure-walkthrough-source-target.md), 온-프레미스 VMM VM 네트워크와 Azure 네트워크 간에이 문서 tooconfigure 네트워크 매핑 toomap를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="655df-104">After you set up hello [source and target replication settings](vmm-to-azure-walkthrough-source-target.md), use this article tooconfigure network mapping toomap between on-premises VMM VM networks, and Azure networks.</span></span>

<span data-ttu-id="655df-105">Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="655df-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="655df-106">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="655df-106">Before you start</span></span>

- <span data-ttu-id="655df-107">[네트워크 매핑](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="655df-107">Learn about [network mapping](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span></span>
- <span data-ttu-id="655df-108">[네트워크 매핑용 VMM을 준비합니다](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping).</span><span class="sxs-lookup"><span data-stu-id="655df-108">[Prepare VMM for network mapping](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping).</span></span> 
- <span data-ttu-id="655df-109">있는지 hello VMM 서버의 가상 컴퓨터에 연결 된 tooa VM 네트워크와 Azure 가상 네트워크를 하나 이상 만든를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="655df-109">Verify that virtual machines on hello VMM server are connected tooa VM network, and that you've created at least one Azure virtual network.</span></span> <span data-ttu-id="655df-110">여러 VM 네트워크에 매핑된 tooa 단일 Azure 네트워크 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="655df-110">Multiple VM networks can be mapped tooa single Azure network.</span></span>

## <a name="configure-mapping"></a><span data-ttu-id="655df-111">매핑 구성</span><span class="sxs-lookup"><span data-stu-id="655df-111">Configure mapping</span></span>

<span data-ttu-id="655df-112">다음과 같이 매핑을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="655df-112">Configure mapping as follows:</span></span>

1. <span data-ttu-id="655df-113">**사이트 복구 인프라** > **네트워크 매핑을** > **네트워크 매핑을**, hello 클릭 **+ 네트워크 매핑**  아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="655df-113">In **Site Recovery Infrastructure** > **Network mappings** > **Network Mapping**, click hello **+Network Mapping** icon.</span></span>

    ![네트워크 매핑](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping1.png)
2. <span data-ttu-id="655df-115">**네트워크 매핑을 추가**선택, hello 원본 VMM 서버 및 **Azure** hello 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="655df-115">In **Add network mapping**, select hello source VMM server, and **Azure** as hello target.</span></span>
3. <span data-ttu-id="655df-116">장애 조치 후 구독 hello 및 hello 배포 모델을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="655df-116">Verify hello subscription and hello deployment model after failover.</span></span>
4. <span data-ttu-id="655df-117">**원본 네트워크**선택, toomap hello VMM 서버와 관련 된 hello 목록에서 원하는 hello 원본 온-프레미스 VM 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="655df-117">In **Source network**, select hello source on-premises VM network you want toomap from hello list associated with hello VMM server.</span></span>
5. <span data-ttu-id="655df-118">**대상 네트워크**, 어떤 복제본에서 Azure Vm 배치 될 만들 때 Azure 네트워크를 hello 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="655df-118">In **Target network**, select hello Azure network in which replica Azure VMs will be located when they're created.</span></span> <span data-ttu-id="655df-119">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="655df-119">Then click **OK**.</span></span>

    ![네트워크 매핑](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping2.png)

<span data-ttu-id="655df-121">네트워크 매핑이 시작되면 다음과 같은 동작이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="655df-121">Here's what happens when network mapping begins:</span></span>

* <span data-ttu-id="655df-122">Hello 원본 VM 네트워크에서 기존 Vm은 연결 된 toohello 대상 네트워크 매핑을 시작 될 때입니다.</span><span class="sxs-lookup"><span data-stu-id="655df-122">Existing VMs on hello source VM network are connected toohello target network when mapping begins.</span></span> <span data-ttu-id="655df-123">새 Vm 연결 된 toohello 원본 VM 네트워크에 연결 되어 복제가 실행 되 면 toohello 매핑된 Azure 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="655df-123">New VMs connected toohello source VM network are connected toohello mapped Azure network when replication occurs.</span></span>
* <span data-ttu-id="655df-124">기존 네트워크 매핑을 수정 하는 경우 복제본 가상 컴퓨터는 hello 새 설정을 사용 하 여 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="655df-124">If you modify an existing network mapping, replica virtual machines connect using hello new settings.</span></span>
* <span data-ttu-id="655df-125">Hello 대상 네트워크에 여러 서브넷이 hello에 이러한 서브넷 중 하나는 hello 원본 가상 컴퓨터는 서브넷 이름이 같은 있는 경우 hello 복제본 가상 컴퓨터가 장애 조치 후 toothat 대상 서브넷 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="655df-125">If hello target network has multiple subnets, and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine connects toothat target subnet after failover.</span></span>
* <span data-ttu-id="655df-126">이름이 일치 하는 대상 서브넷 이면 hello 네트워크의 첫 번째 서브넷 toohello hello 가상 컴퓨터에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="655df-126">If there’s no target subnet with a matching name, hello virtual machine connects toohello first subnet in hello network.</span></span>



## <a name="next-steps"></a><span data-ttu-id="655df-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="655df-127">Next steps</span></span>

<span data-ttu-id="655df-128">너무 이동[10 단계: 복제 정책 만들기](vmm-to-azure-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="655df-128">Go too[Step 10: Create a replication policy](vmm-to-azure-walkthrough-replication.md)</span></span>
