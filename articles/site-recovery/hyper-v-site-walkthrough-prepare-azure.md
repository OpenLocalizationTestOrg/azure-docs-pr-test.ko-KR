---
title: "Azure Site Recovery를 사용 하 여 aaaPrepare Azure 리소스 tooreplicate (System Center VMM) 없이 Hyper-v Vm tooAzure | Microsoft Docs"
description: "필요한 Azure에서 위치에 Azure Site Recovery를 사용 하 여 Hyper-v Vm (없이 VMM) tooAzure 복제를 시작 하기 전에 설명"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 28fa722c-675e-4637-98eb-7ccbf3806d69
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: f659e300c39253b0eaf7218bee9d39b11682edb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-tooazure"></a><span data-ttu-id="a56e9-103">5 단계: Hyper-v 복제 tooAzure Azure 리소스 준비</span><span class="sxs-lookup"><span data-stu-id="a56e9-103">Step 5: Prepare Azure resources for Hyper-V replication tooAzure</span></span>

<span data-ttu-id="a56e9-104">Hello 지침을 사용 하 여이 문서 tooprepare Azure의에서 리소스 복제할 수 있도록 온-프레미스 Hyper-v Vm (System Center VMM) 없이 hello를 사용 하 여 tooAzure [Azure Site Recovery](site-recovery-overview.md) 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="a56e9-104">Use hello instructions in this article tooprepare Azure resources so that you can replicate on-premises Hyper-V VMs (without System Center VMM) tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="a56e9-105">이 문서를 읽은 후 hello 맨 아래에 모든 메모를 게시 하거나 hello에 대 한 기술적 질문 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="a56e9-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="a56e9-106">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="a56e9-106">Before you start</span></span>

<span data-ttu-id="a56e9-107">Hello 참고 있는지 확인 하십시오 [필수 구성 요소](hyper-v-site-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="a56e9-107">Make sure you've read hello [prerequisites](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="a56e9-108">Azure 계정 설정</span><span class="sxs-lookup"><span data-stu-id="a56e9-108">Set up an Azure account</span></span>

- <span data-ttu-id="a56e9-109">[Microsoft Azure 계정](http://azure.microsoft.com/)을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a56e9-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="a56e9-110">[평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a56e9-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="a56e9-111">사이트 복구를 아래에서 지역 가용성을 위한 지원 hello 영역 확인 [Azure 사이트 복구 가격 정보](https://azure.microsoft.com/pricing/details/site-recovery/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a56e9-111">Check hello supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="a56e9-112">에 대 한 자세한 내용은 [사이트 복구 가격](site-recovery-faq.md#pricing), 가져오고, hello [가격 정보](https://azure.microsoft.com/pricing/details/site-recovery/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a56e9-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get hello [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>


## <a name="set-up-an-azure-network"></a><span data-ttu-id="a56e9-113">Azure 네트워크를 설정</span><span class="sxs-lookup"><span data-stu-id="a56e9-113">Set up an Azure network</span></span>

- <span data-ttu-id="a56e9-114">Azure 네트워크 설정</span><span class="sxs-lookup"><span data-stu-id="a56e9-114">Set up an Azure network.</span></span> <span data-ttu-id="a56e9-115">Azure VM은 장애 조치 후 처음 만들 때 이 네트워크에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="a56e9-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="a56e9-116">hello 네트워크 hello에 있어야 hello와 동일한 지역 복구 서비스 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="a56e9-116">hello network should be in hello same region as hello Recovery Services vault</span></span>
- <span data-ttu-id="a56e9-117">Hello Azure 포털에서에서 사이트 복구에서를 설정 하는 네트워크를 사용할 수 있습니다 [리소스 관리자](../resource-manager-deployment-model.md), 또는 클래식 모드에서.</span><span class="sxs-lookup"><span data-stu-id="a56e9-117">Site Recovery in hello Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="a56e9-118">시작하기 전에 네트워크를 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a56e9-118">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="a56e9-119">Toodo 필요 하지 않으면 사이트 복구 배포 시이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a56e9-119">If you don't, you need toodo it during Site Recovery deployment.</span></span>
- <span data-ttu-id="a56e9-120">[가상 네트워크 가격 책정](https://azure.microsoft.com/pricing/details/virtual-network/)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a56e9-120">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="a56e9-121">Azure 저장소 계정을 설정</span><span class="sxs-lookup"><span data-stu-id="a56e9-121">Set up an Azure storage account</span></span>

- <span data-ttu-id="a56e9-122">Site Recovery 온-프레미스 컴퓨터 tooAzure 저장소를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="a56e9-122">Site Recovery replicates on-premises machines tooAzure storage.</span></span> <span data-ttu-id="a56e9-123">Azure Vm 장애 조치 발생 후 hello 저장소에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a56e9-123">Azure VMs are created from hello storage after failover occurs.</span></span>
- <span data-ttu-id="a56e9-124">표준/프리미엄 설정 [Azure 저장소 계정](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold 데이터 tooAzure 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="a56e9-124">Set up a standard/premium [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold data replicated tooAzure.</span></span>
- <span data-ttu-id="a56e9-125">[프리미엄 저장소](../storage/common/storage-premium-storage.md) 계속 높게 IO 성능과 짧은 대기 시간 toohost IO가 많은 작업을 필요로 하는 가상 컴퓨터에 대해 일반적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a56e9-125">[Premium storage](../storage/common/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency toohost IO intensive workloads.</span></span>
- <span data-ttu-id="a56e9-126">Toouse 프리미엄 계정 toostore 복제 된 데이터를 캡처 지속적인 tooon 온-프레미스 데이터를 변경 표준 저장소 계정을 toostore 복제 로그를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a56e9-126">If you want toouse a premium account toostore replicated data, you also need a standard storage account toostore replication logs that capture ongoing changes tooon-premises data.</span></span>
- <span data-ttu-id="a56e9-127">Hello 리소스 모델에 따라 원하는 toouse 장애 조치 Azure Vm에 대 한에서 계정을 설정한 [Resource Manager 모드](../storage/common/storage-create-storage-account.md), 또는 [클래식 모드](../storage/common/storage-create-storage-account.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a56e9-127">Depending on hello resource model you want toouse for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/common/storage-create-storage-account.md), or [classic mode](../storage/common/storage-create-storage-account.md).</span></span>
- <span data-ttu-id="a56e9-128">시작하기 전에 저장소 계정을 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a56e9-128">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="a56e9-129">그렇지 않으면 toodo 해야 사이트 복구 배포 시이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a56e9-129">If you don't you need toodo it during Site Recovery deployment.</span></span> <span data-ttu-id="a56e9-130">hello 계정은 hello에 있어야 hello와 동일한 지역 복구 서비스 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="a56e9-130">hello accounts must be in hello same region as hello Recovery Services vault.</span></span>
- <span data-ttu-id="a56e9-131">저장소 계정에서 사용 되는 사이트 복구 hello 내의 리소스 그룹 동일 이동할 수 없습니다, 구독 또는 다른 구독에서.</span><span class="sxs-lookup"><span data-stu-id="a56e9-131">You can't move storage accounts used by Site Recovery across resource groups within hello same subscription, or across different subscriptions.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a56e9-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a56e9-132">Next steps</span></span>

<span data-ttu-id="a56e9-133">너무 이동[6 단계: 준비 Hyper-v 리소스](hyper-v-site-walkthrough-prepare-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="a56e9-133">Go too[Step 6: Prepare Hyper-V resources](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>
