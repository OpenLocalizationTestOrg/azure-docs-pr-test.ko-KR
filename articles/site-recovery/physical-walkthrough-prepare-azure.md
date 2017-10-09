---
title: "Azure 리소스 tooreplicate aaaPrepare 온-프레미스 Azure Site Recovery를 사용 하 여 실제 서버 tooAzure | Microsoft Docs"
description: "필요한 Azure에서 시작 하기 전에 온-프레미스 서버 tooAzure 복제 hello Azure Site Recovery 서비스를 사용 하 여 설명 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 4e320d9b-8bb8-46bb-ba21-77c5d16748ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: raynew
ms.openlocfilehash: b1d008dac278bc7797188a3c9c15f2a3b5fe12d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-physical-server-replication-tooazure"></a><span data-ttu-id="8e7ea-103">5 단계: 복제 tooAzure 물리적 서버에 대 한 Azure 리소스 준비</span><span class="sxs-lookup"><span data-stu-id="8e7ea-103">Step 5: Prepare Azure resources for physical server replication tooAzure</span></span>


<span data-ttu-id="8e7ea-104">이 문서 tooprepare Azure의에서 hello 지침을 사용 하 여 리소스 hello를 사용 하 여 온-프레미스 서버 tooAzure 복제할 수 있도록 [Azure Site Recovery](site-recovery-overview.md) 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="8e7ea-104">Use hello instructions in this article tooprepare Azure resources so that you can replicate on-premises servers tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="8e7ea-105">Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e7ea-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="8e7ea-106">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="8e7ea-106">Before you start</span></span>

<span data-ttu-id="8e7ea-107">Hello 참고 있는지 확인 하십시오 [필수 구성 요소](physical-walkthrough-prerequisites.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e7ea-107">Make sure you've read hello [prerequisites](physical-walkthrough-prerequisites.md).</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="8e7ea-108">Azure 계정 설정</span><span class="sxs-lookup"><span data-stu-id="8e7ea-108">Set up an Azure account</span></span>

- <span data-ttu-id="8e7ea-109">[Microsoft Azure 계정](http://azure.microsoft.com/)을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8e7ea-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="8e7ea-110">[평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e7ea-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="8e7ea-111">아래에서 사이트 복구에 대 한 지원 hello 영역 확인 **지리적 가용성** 에 [Azure 사이트 복구 가격 정보](https://azure.microsoft.com/pricing/details/site-recovery/)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e7ea-111">Check hello supported regions for Site Recovery, under **Geographic Availability** in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="8e7ea-112">에 대 한 자세한 내용은 [사이트 복구 가격](site-recovery-faq.md#pricing), 가져오고, hello [가격 정보](https://azure.microsoft.com/pricing/details/site-recovery/)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e7ea-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get hello [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>



## <a name="set-up-an-azure-network"></a><span data-ttu-id="8e7ea-113">Azure 네트워크를 설정</span><span class="sxs-lookup"><span data-stu-id="8e7ea-113">Set up an Azure network</span></span>

- <span data-ttu-id="8e7ea-114">Azure 네트워크 설정</span><span class="sxs-lookup"><span data-stu-id="8e7ea-114">Set up an Azure network.</span></span> <span data-ttu-id="8e7ea-115">Azure VM은 장애 조치 후 처음 만들 때 이 네트워크에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e7ea-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="8e7ea-116">Hello Azure 포털에서에서 사이트 복구에서를 설정 하는 네트워크를 사용할 수 있습니다 [리소스 관리자](../resource-manager-deployment-model.md), 또는 클래식 모드에서.</span><span class="sxs-lookup"><span data-stu-id="8e7ea-116">Site Recovery in hello Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="8e7ea-117">hello 네트워크 hello에 있어야 hello와 동일한 지역 복구 서비스 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="8e7ea-117">hello network should be in hello same region as hello Recovery Services vault.</span></span>
- <span data-ttu-id="8e7ea-118">[가상 네트워크 가격 책정](https://azure.microsoft.com/pricing/details/virtual-network/)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8e7ea-118">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>
- <span data-ttu-id="8e7ea-119">장애 조치 후에 [Azure VM 연결](physical-walkthrough-network.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8e7ea-119">Learn more about [Azure VM connectivity](physical-walkthrough-network.md) after failover.</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="8e7ea-120">Azure 저장소 계정을 설정</span><span class="sxs-lookup"><span data-stu-id="8e7ea-120">Set up an Azure storage account</span></span>

- <span data-ttu-id="8e7ea-121">Site Recovery 온-프레미스 서버 tooAzure 저장소를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="8e7ea-121">Site Recovery replicates on-premises servers tooAzure storage.</span></span> <span data-ttu-id="8e7ea-122">Azure Vm 장애 조치 발생 후 hello 저장소에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e7ea-122">Azure VMs are created from hello storage after failover occurs.</span></span>
- <span data-ttu-id="8e7ea-123">복제 데이터를 저장할 [Azure Storage 계정](../storage/common/storage-create-storage-account.md#create-a-storage-account)을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8e7ea-123">Set up an [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) for replicated data.</span></span>
- <span data-ttu-id="8e7ea-124">Hello Azure 포털에서에서 사이트 복구가 צ ְ ײ 저장소 계정 리소스 관리자, 또는 클래식 모드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e7ea-124">Site Recovery in hello Azure portal can use storage accounts set up in Resource Manager, or in classic mode.</span></span>
- <span data-ttu-id="8e7ea-125">저장소 계정 hello 표준 수 또는 [프리미엄](../storage/common/storage-premium-storage.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e7ea-125">hello storage account can be standard or [premium](../storage/common/storage-premium-storage.md).</span></span>
- <span data-ttu-id="8e7ea-126">프리미엄 계정을 설정하는 경우 로그 데이터에 추가 표준 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8e7ea-126">If you set up a premium account, you will also need an additional standard account for log data.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8e7ea-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8e7ea-127">Next steps</span></span>

<span data-ttu-id="8e7ea-128">너무 이동[6 단계: 자격 증명 모음 설정](physical-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="8e7ea-128">Go too[Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>
