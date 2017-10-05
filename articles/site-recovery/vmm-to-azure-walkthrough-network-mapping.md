---
title: "Azure Site Recovery를 사용하여 VMM 클라우드의 Hyper-V VM을 Azure로 복제하기 위한 네트워크 매핑 구성"
description: "이 문서에서는 Azure Site Recovery를 사용하여 VMM 클라우드의 Hyper-V VM을 Azure로 복제할 때 네트워크 매핑을 구성하는 방법을 설명합니다."
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
ms.openlocfilehash: ed6f73d8baea5af0d2aa5f0ae885f305911ccc82
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="step-9-configure-network-mapping-for-hyper-v-replication-with-vmm-to-azure"></a><span data-ttu-id="45d01-103">9단계: Azure로의 Hyper-V 복제(VMM 포함)를 위한 네트워크 매핑 구성</span><span class="sxs-lookup"><span data-stu-id="45d01-103">Step 9: Configure network mapping for Hyper-V replication (with VMM) to Azure</span></span>

<span data-ttu-id="45d01-104">[소스 및 대상 복제 설정](vmm-to-azure-walkthrough-source-target.md)을 지정한 후 이 문서의 내용을 참조하여 온-프레미스 VMM VM 네트워크와 Azure 네트워크 간을 매핑하는 네트워크 매핑을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d01-104">After you set up the [source and target replication settings](vmm-to-azure-walkthrough-source-target.md), use this article to configure network mapping to map between on-premises VMM VM networks, and Azure networks.</span></span>

<span data-ttu-id="45d01-105">이 문서의 하단 또는 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 의견이나 질문을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="45d01-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="45d01-106">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="45d01-106">Before you start</span></span>

- <span data-ttu-id="45d01-107">[네트워크 매핑](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="45d01-107">Learn about [network mapping](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span></span>
- <span data-ttu-id="45d01-108">[네트워크 매핑용 VMM을 준비합니다](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping).</span><span class="sxs-lookup"><span data-stu-id="45d01-108">[Prepare VMM for network mapping](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping).</span></span> 
- <span data-ttu-id="45d01-109">VMM 서버의 가상 컴퓨터가 VM 네트워크에 연결되었으며 Azure 가상 네트워크를 하나 이상 만들었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="45d01-109">Verify that virtual machines on the VMM server are connected to a VM network, and that you've created at least one Azure virtual network.</span></span> <span data-ttu-id="45d01-110">단일 Azure 네트워크에 여러 개의 VM 네트워크를 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45d01-110">Multiple VM networks can be mapped to a single Azure network.</span></span>

## <a name="configure-mapping"></a><span data-ttu-id="45d01-111">매핑 구성</span><span class="sxs-lookup"><span data-stu-id="45d01-111">Configure mapping</span></span>

<span data-ttu-id="45d01-112">다음과 같이 매핑을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="45d01-112">Configure mapping as follows:</span></span>

1. <span data-ttu-id="45d01-113">**Site Recovery 인프라** > **네트워크 매핑** > **네트워크 매핑**에서 **+네트워크 매핑** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="45d01-113">In **Site Recovery Infrastructure** > **Network mappings** > **Network Mapping**, click the **+Network Mapping** icon.</span></span>

    ![네트워크 매핑](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping1.png)
2. <span data-ttu-id="45d01-115">**네트워크 매핑 추가**에서 원본 VMM 서버를 선택하고, 대상으로 **Azure**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="45d01-115">In **Add network mapping**, select the source VMM server, and **Azure** as the target.</span></span>
3. <span data-ttu-id="45d01-116">장애 조치(failover) 후 구독과 배포 모델을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="45d01-116">Verify the subscription and the deployment model after failover.</span></span>
4. <span data-ttu-id="45d01-117">**원본 네트워크**에서 VMM 서버에 연결된 목록에서 매핑하려는 원본 온-프레미스 VM 네트워크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="45d01-117">In **Source network**, select the source on-premises VM network you want to map from the list associated with the VMM server.</span></span>
5. <span data-ttu-id="45d01-118">**대상 네트워크**에서 Azure 네트워크를 만들 때 배치될 Azure VM 복제본을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="45d01-118">In **Target network**, select the Azure network in which replica Azure VMs will be located when they're created.</span></span> <span data-ttu-id="45d01-119">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="45d01-119">Then click **OK**.</span></span>

    ![네트워크 매핑](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping2.png)

<span data-ttu-id="45d01-121">네트워크 매핑이 시작되면 다음과 같은 동작이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="45d01-121">Here's what happens when network mapping begins:</span></span>

* <span data-ttu-id="45d01-122">원본 VM 네트워크에 있는 기존 VM은 매핑이 시작될 때 대상 네트워크에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d01-122">Existing VMs on the source VM network are connected to the target network when mapping begins.</span></span> <span data-ttu-id="45d01-123">원본 VM 네트워크에 연결된 새 VM은 복제된 후에 매핑된 Azure 네트워크에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d01-123">New VMs connected to the source VM network are connected to the mapped Azure network when replication occurs.</span></span>
* <span data-ttu-id="45d01-124">기존 네트워크 매핑을 수정하면 복제본 가상 컴퓨터가 새 설정을 사용하여 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d01-124">If you modify an existing network mapping, replica virtual machines connect using the new settings.</span></span>
* <span data-ttu-id="45d01-125">대상 네트워크에 여러 서브넷이 있고 이 서브넷 중 하나의 이름이 원본 가상 컴퓨터가 있는 서브넷과 같으면 복제 가상 컴퓨터가 장애 조치(failover) 후에 대상 서브넷에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d01-125">If the target network has multiple subnets, and one of those subnets has the same name as subnet on which the source virtual machine is located, then the replica virtual machine connects to that target subnet after failover.</span></span>
* <span data-ttu-id="45d01-126">일치하는 이름을 가진 대상 서브넷이 없으면 가상 컴퓨터가 네트워크의 첫 번째 서브넷에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="45d01-126">If there’s no target subnet with a matching name, the virtual machine connects to the first subnet in the network.</span></span>



## <a name="next-steps"></a><span data-ttu-id="45d01-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="45d01-127">Next steps</span></span>

<span data-ttu-id="45d01-128">[10단계: 복제 정책 만들기](vmm-to-azure-walkthrough-replication.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="45d01-128">Go to [Step 10: Create a replication policy](vmm-to-azure-walkthrough-replication.md)</span></span>
