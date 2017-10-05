---
title: "Azure Site Recovery를 사용하여 Azure로 Hyper-V VM(System Center VMM 없음) 복제하기 위한 Azure 리소스 준비 | Microsoft Docs"
description: "Azure Site Recovery를 사용하여 Hyper-V VM(VMM 없음)을 Azure에 복제하기 전에 Azure에서 준비해야 하는 항목을 설명합니다."
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
ms.openlocfilehash: 1a30cadaab7e053184f0be133f1da5bfddc1fd91
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-to-azure"></a><span data-ttu-id="11872-103">5단계: Azure에 Hyper-V 복제를 위한 Azure 리소스 준비</span><span class="sxs-lookup"><span data-stu-id="11872-103">Step 5: Prepare Azure resources for Hyper-V replication to Azure</span></span>

<span data-ttu-id="11872-104">Azure 리소스를 준비하는 이 문서의 지침을 사용하여 [Azure Site Recovery](site-recovery-overview.md) 서비스를 사용하여 온-프레미스 Hyper-V VM(System Center VMM 없음)을 Azure에 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11872-104">Use the instructions in this article to prepare Azure resources so that you can replicate on-premises Hyper-V VMs (without System Center VMM) to Azure using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="11872-105">이 문서를 읽은 후에는 하단에서 의견을 게시하거나 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 기술적인 질문을 합니다.</span><span class="sxs-lookup"><span data-stu-id="11872-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="11872-106">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="11872-106">Before you start</span></span>

<span data-ttu-id="11872-107">[필수 조건](hyper-v-site-walkthrough-prerequisites.md)을 읽었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="11872-107">Make sure you've read the [prerequisites](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="11872-108">Azure 계정 설정</span><span class="sxs-lookup"><span data-stu-id="11872-108">Set up an Azure account</span></span>

- <span data-ttu-id="11872-109">[Microsoft Azure 계정](http://azure.microsoft.com/)을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="11872-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="11872-110">[평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11872-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="11872-111">[Azure Site Recovery 가격 책정 세부 정보](https://azure.microsoft.com/pricing/details/site-recovery/)의 지역 가용성에서 Site Recovery에 지원되는 지역을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="11872-111">Check the supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="11872-112">[Site Recovery 가격 책정](site-recovery-faq.md#pricing)에 대해 알아보고 [가격 책정 세부 정보](https://azure.microsoft.com/pricing/details/site-recovery/)를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="11872-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get the [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>


## <a name="set-up-an-azure-network"></a><span data-ttu-id="11872-113">Azure 네트워크를 설정합니다</span><span class="sxs-lookup"><span data-stu-id="11872-113">Set up an Azure network</span></span>

- <span data-ttu-id="11872-114">Azure 네트워크 설정</span><span class="sxs-lookup"><span data-stu-id="11872-114">Set up an Azure network.</span></span> <span data-ttu-id="11872-115">Azure VM은 장애 조치 후 처음 만들 때 이 네트워크에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="11872-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="11872-116">네트워크가 Recovery Services 자격 증명 모음과 같은 지역에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11872-116">The network should be in the same region as the Recovery Services vault</span></span>
- <span data-ttu-id="11872-117">Azure Portal의 Site Recovery에서는 [리소스 관리자](../resource-manager-deployment-model.md) 또는 클래식 모드에서 설정된 네트워크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11872-117">Site Recovery in the Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="11872-118">시작하기 전에 네트워크를 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="11872-118">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="11872-119">그렇지 않으면 Site Recovery를 배포하는 동안 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11872-119">If you don't, you need to do it during Site Recovery deployment.</span></span>
- <span data-ttu-id="11872-120">[가상 네트워크 가격 책정](https://azure.microsoft.com/pricing/details/virtual-network/)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="11872-120">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="11872-121">Azure 저장소 계정을 설정</span><span class="sxs-lookup"><span data-stu-id="11872-121">Set up an Azure storage account</span></span>

- <span data-ttu-id="11872-122">Site Recovery는 온-프레미스 컴퓨터를 Azure Storage에 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="11872-122">Site Recovery replicates on-premises machines to Azure storage.</span></span> <span data-ttu-id="11872-123">장애 조치(failover)가 발생한 후에 저장소에서 Azure VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="11872-123">Azure VMs are created from the storage after failover occurs.</span></span>
- <span data-ttu-id="11872-124">표준/프리미엄 [Azure Storage 계정](../storage/common/storage-create-storage-account.md#create-a-storage-account)을 설정하여 Azure로 복제된 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="11872-124">Set up a standard/premium [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) to hold data replicated to Azure.</span></span>
- <span data-ttu-id="11872-125">[Premium Storage](../storage/common/storage-premium-storage.md)는 IO를 많이 사용하는 워크로드를 호스트하기 위해 일관된 IO 고성능과 짧은 대기 시간이 요구되는 가상 컴퓨터에 일반적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="11872-125">[Premium storage](../storage/common/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency to host IO intensive workloads.</span></span>
- <span data-ttu-id="11872-126">프리미엄 계정을 사용하여 복제된 데이터를 저장하려는 경우 온-프레미스 데이터에 대한 지속적인 변화를 캡처하는 복제 로그를 저장하는 표준 저장소 계정이 필요할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11872-126">If you want to use a premium account to store replicated data, you also need a standard storage account to store replication logs that capture ongoing changes to on-premises data.</span></span>
- <span data-ttu-id="11872-127">장애 조치(failover)된 Azure VM에 사용하려는 리소스 모델에 따라 [Resource Manager 모드](../storage/common/storage-create-storage-account.md) 또는 [클래식 모드](../storage/common/storage-create-storage-account.md)에서 계정을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="11872-127">Depending on the resource model you want to use for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/common/storage-create-storage-account.md), or [classic mode](../storage/common/storage-create-storage-account.md).</span></span>
- <span data-ttu-id="11872-128">시작하기 전에 저장소 계정을 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="11872-128">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="11872-129">그렇지 않으면 Site Recovery를 배포하는 동안 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11872-129">If you don't you need to do it during Site Recovery deployment.</span></span> <span data-ttu-id="11872-130">계정은 Recovery Services 자격 증명 모음과 동일한 지역에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11872-130">The accounts must be in the same region as the Recovery Services vault.</span></span>
- <span data-ttu-id="11872-131">Site Recovery에 사용되는 저장소 계정은 동일한 구독 내의 리소스 그룹 간이나 서로 다른 구독 간에 이동할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="11872-131">You can't move storage accounts used by Site Recovery across resource groups within the same subscription, or across different subscriptions.</span></span>


## <a name="next-steps"></a><span data-ttu-id="11872-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="11872-132">Next steps</span></span>

<span data-ttu-id="11872-133">[6단계: Hyper-V 리소스 준비](hyper-v-site-walkthrough-prepare-hyper-v.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="11872-133">Go to [Step 6: Prepare Hyper-V resources](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>
