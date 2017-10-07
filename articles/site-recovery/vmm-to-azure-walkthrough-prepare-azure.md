---
title: "Azure Site Recovery를 사용 하 여 aaaPrepare Azure 리소스 tooreplicate (System Center VMM)을 통해 Hyper-v Vm tooAzure | Microsoft Docs"
description: "필요한 Azure에서 시작 하기 전에 복제 (VMM)과 Hyper-v Vm tooAzure Azure Site Recovery를 사용 하 여 설명 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1568bdc3-e767-477b-b040-f13699ab5644
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 86bfbab7722fe5bd5b93b92e398d1d441505d3b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-with-vmm-tooazure"></a><span data-ttu-id="ded55-103">5 단계: Hyper-v (VMM)와 복제 tooAzure Azure 리소스 준비</span><span class="sxs-lookup"><span data-stu-id="ded55-103">Step 5: Prepare Azure resources for Hyper-V replication (with VMM) tooAzure</span></span>

<span data-ttu-id="ded55-104">확인 한 후 [네트워크 요구 사항](vmm-to-azure-walkthrough-network.md),이 문서 tooprepare Azure의에서 hello 지침을 사용 하 여 리소스 사용 하 여 클라우드 tooAzure System Center Virtual Machine Manager (VMM)의 온-프레미스 Hyper-v Vm, 복제할 수 있도록 hello [Azure Site Recovery](site-recovery-overview.md) 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="ded55-104">After verifying [network requirements](vmm-to-azure-walkthrough-network.md), use hello instructions in this article tooprepare Azure resources so that you can replicate on-premises Hyper-V VMs in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="ded55-105">이 문서를 읽은 후 hello 맨 아래에 모든 메모를 게시 하거나 hello에 대 한 기술적 질문 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="ded55-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-an-azure-account"></a><span data-ttu-id="ded55-106">Azure 계정 설정</span><span class="sxs-lookup"><span data-stu-id="ded55-106">Set up an Azure account</span></span>

- <span data-ttu-id="ded55-107">[Microsoft Azure 계정](http://azure.microsoft.com/)을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ded55-107">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="ded55-108">[평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ded55-108">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="ded55-109">사이트 복구를 아래에서 지역 가용성을 위한 지원 hello 영역 확인 [Azure 사이트 복구 가격 정보](https://azure.microsoft.com/pricing/details/site-recovery/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ded55-109">Check hello supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="ded55-110">에 대 한 자세한 내용은 [사이트 복구 가격](site-recovery-faq.md#pricing), 가져오고, hello [가격 정보](https://azure.microsoft.com/pricing/details/site-recovery/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ded55-110">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get hello [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="ded55-111">Azure 계정에 올바른 hello 확인 [권한을](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)toocreate Azure Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="ded55-111">Make sure your Azure account has hello correct [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)toocreate Azure VMs.</span></span> <span data-ttu-id="ded55-112">Azure 역할 기반 액세스 제어에 대해 자세히 알아보려면 [여기](../active-directory/role-based-access-built-in-roles.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ded55-112">[Learn more](../active-directory/role-based-access-built-in-roles.md) about Azure role-based access control.</span></span>


## <a name="set-up-an-azure-network"></a><span data-ttu-id="ded55-113">Azure 네트워크를 설정</span><span class="sxs-lookup"><span data-stu-id="ded55-113">Set up an Azure network</span></span>

- <span data-ttu-id="ded55-114">[Azure 네트워크](../virtual-network/virtual-network-get-started-vnet-subnet.md)를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ded55-114">Set up an [Azure network](../virtual-network/virtual-network-get-started-vnet-subnet.md).</span></span> <span data-ttu-id="ded55-115">Azure VM은 장애 조치 후 처음 만들 때 이 네트워크에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="ded55-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="ded55-116">hello 네트워크 hello에 있어야 hello와 동일한 지역 복구 서비스 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="ded55-116">hello network should be in hello same region as hello Recovery Services vault</span></span>
- <span data-ttu-id="ded55-117">Hello Azure 포털에서에서 사이트 복구에서를 설정 하는 네트워크를 사용할 수 있습니다 [리소스 관리자](../resource-manager-deployment-model.md), 또는 클래식 모드에서.</span><span class="sxs-lookup"><span data-stu-id="ded55-117">Site Recovery in hello Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="ded55-118">시작하기 전에 네트워크를 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ded55-118">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="ded55-119">Toodo 필요 하지 않으면 사이트 복구 배포 시이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ded55-119">If you don't, you need toodo it during Site Recovery deployment.</span></span>
- <span data-ttu-id="ded55-120">[가상 네트워크 가격 책정](https://azure.microsoft.com/pricing/details/virtual-network/)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ded55-120">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="ded55-121">Azure 저장소 계정을 설정</span><span class="sxs-lookup"><span data-stu-id="ded55-121">Set up an Azure storage account</span></span>

- <span data-ttu-id="ded55-122">Site Recovery 온-프레미스 컴퓨터 tooAzure 저장소를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="ded55-122">Site Recovery replicates on-premises machines tooAzure storage.</span></span> <span data-ttu-id="ded55-123">Azure Vm 장애 조치 발생 후 hello 저장소에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ded55-123">Azure VMs are created from hello storage after failover occurs.</span></span>
- <span data-ttu-id="ded55-124">표준/프리미엄 설정 [Azure 저장소 계정](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold 데이터 tooAzure 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="ded55-124">Set up a standard/premium [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold data replicated tooAzure.</span></span>
- <span data-ttu-id="ded55-125">[프리미엄 저장소](../storage/common/storage-premium-storage.md) 계속 높게 IO 성능과 짧은 대기 시간 toohost IO가 많은 작업을 필요로 하는 가상 컴퓨터에 대해 일반적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ded55-125">[Premium storage](../storage/common/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency toohost IO intensive workloads.</span></span>
- <span data-ttu-id="ded55-126">Toouse 프리미엄 계정 toostore 복제 된 데이터를 캡처 지속적인 tooon 온-프레미스 데이터를 변경 표준 저장소 계정을 toostore 복제 로그를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ded55-126">If you want toouse a premium account toostore replicated data, you also need a standard storage account toostore replication logs that capture ongoing changes tooon-premises data.</span></span>
- <span data-ttu-id="ded55-127">Hello 리소스 모델에 따라 원하는 toouse 장애 조치 Azure Vm에 대 한에서 계정을 설정한 [Resource Manager 모드](../storage/common/storage-create-storage-account.md), 또는 [클래식 모드](../storage/common/storage-create-storage-account.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ded55-127">Depending on hello resource model you want toouse for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/common/storage-create-storage-account.md), or [classic mode](../storage/common/storage-create-storage-account.md).</span></span>
- <span data-ttu-id="ded55-128">시작하기 전에 저장소 계정을 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ded55-128">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="ded55-129">그렇지 않으면 toodo 해야 사이트 복구 배포 시이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ded55-129">If you don't you need toodo it during Site Recovery deployment.</span></span> <span data-ttu-id="ded55-130">hello 계정은 hello에 있어야 hello와 동일한 지역 복구 서비스 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="ded55-130">hello accounts must be in hello same region as hello Recovery Services vault.</span></span>
- <span data-ttu-id="ded55-131">저장소 계정에서 사용 되는 사이트 복구 hello 내의 리소스 그룹 동일 이동할 수 없습니다, 구독 또는 다른 구독에서.</span><span class="sxs-lookup"><span data-stu-id="ded55-131">You can't move storage accounts used by Site Recovery across resource groups within hello same subscription, or across different subscriptions.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ded55-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ded55-132">Next steps</span></span>

<span data-ttu-id="ded55-133">너무 이동[6 단계: 준비 VMM](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="ded55-133">Go too[Step 6: Prepare VMM](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span></span>
