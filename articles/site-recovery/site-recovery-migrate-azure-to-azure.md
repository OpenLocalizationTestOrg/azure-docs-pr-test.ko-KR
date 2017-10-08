---
title: "Azure 지역 간의 Azure IaaS Vm aaaMigrate | Microsoft Docs"
description: "하나의 Azure 지역 tooanother에서 Azure Site Recovery toomigrate Azure IaaS 가상 컴퓨터를 사용 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8a29e0d9-0010-4739-972f-02b8bdf360f6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: c84dc77716b8d19969eab60707ed1332ca39b893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-iaas-virtual-machines-between-azure-regions-with-azure-site-recovery"></a><span data-ttu-id="3fb7d-103">Azure Site Recovery를 사용하여 Azure 지역 간에 Azure IaaS 가상 컴퓨터 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="3fb7d-103">Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery</span></span>
## <a name="overview"></a><span data-ttu-id="3fb7d-104">개요</span><span class="sxs-lookup"><span data-stu-id="3fb7d-104">Overview</span></span>
<span data-ttu-id="3fb7d-105">TooAzure 사이트 복구를 시작!</span><span class="sxs-lookup"><span data-stu-id="3fb7d-105">Welcome tooAzure Site Recovery!</span></span> <span data-ttu-id="3fb7d-106">이 문서를 사용 하 여 Azure 지역 간 toomigrate Azure Vm에 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fb7d-106">Use this article if you want toomigrate Azure VMs between Azure regions.</span></span> <span data-ttu-id="3fb7d-107">시작하기 전에 다음 사항에 주의하세요.</span><span class="sxs-lookup"><span data-stu-id="3fb7d-107">Before you start, note that:</span></span>

* <span data-ttu-id="3fb7d-108">Azure에는 리소스를 만들고 작업하기 위한 두 가지 배포 모델인 Azure Resource Manager 배포 모델과 클래식 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fb7d-108">Azure has two different deployment models for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="3fb7d-109">Azure는 두 개의 포털 – hello 클래식 배포 모델을 지 원하는 Azure 클래식 포털 hello 및 두 가지 경우 모두 지원 하 여 Azure 포털 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fb7d-109">Azure also has two portals – hello Azure classic portal that supports hello classic deployment model, and hello Azure portal with support for both deployment models.</span></span> <span data-ttu-id="3fb7d-110">hello 기본 단계 마이그레이션에 대 한 hello 같은 리소스 관리자에서 또는 기본에서 사이트 복구를 구성 하는 여부.</span><span class="sxs-lookup"><span data-stu-id="3fb7d-110">hello basic steps for migration are hello same whether you're configuring Site Recovery in Resource Manager or in classic.</span></span> <span data-ttu-id="3fb7d-111">그러나 UI 지침 hello 이므로이 문서에서 스크린 샷 hello Azure 포털에 대 한 관련 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fb7d-111">However hello UI instructions and screenshots in this article are relevant for hello Azure portal.</span></span>
* <span data-ttu-id="3fb7d-112">**현재 하나의 영역 tooanother에서만 마이그레이션할 수 있습니다. 한 Azure 지역 tooanother에서 Vm 장애 조치할 수 있습니다 하지만 있습니다 수 없는 다시 장애 복구에 다시.**</span><span class="sxs-lookup"><span data-stu-id="3fb7d-112">**Currently you can only migrate from one region tooanother. You can fail over VMs from one Azure region tooanother, but you can't fail them back again.**</span></span>

<span data-ttu-id="3fb7d-113">Hello 또는이 문서의 hello 맨 아래에 설명 이나 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="3fb7d-113">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3fb7d-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3fb7d-114">Prerequisites</span></span>
<span data-ttu-id="3fb7d-115">이 배포에 대해 필요한 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3fb7d-115">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="3fb7d-116">**IaaS 가상 컴퓨터**: hello toomigrate 원하는 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="3fb7d-116">**IaaS virtual machines**: hello VMs you want toomigrate.</span></span> <span data-ttu-id="3fb7d-117">이러한 VM을 실제 컴퓨터로 간주하여 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="3fb7d-117">You migrate these VMs by treating them as physical machines.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="3fb7d-118">배포 단계</span><span class="sxs-lookup"><span data-stu-id="3fb7d-118">Deployment steps</span></span>
<span data-ttu-id="3fb7d-119">이 섹션에서는 hello 새 Azure 포털의 hello 배포 단계를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fb7d-119">This section describes hello deployment steps in hello new Azure portal.</span></span>

1. <span data-ttu-id="3fb7d-120">[자격 증명 모음을 만듭니다](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="3fb7d-120">[Create a vault](site-recovery-vmware-to-azure.md).</span></span>
2. <span data-ttu-id="3fb7d-121">[복제를 활성화합니다](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="3fb7d-121">[Enable replication](site-recovery-vmware-to-azure.md).</span></span> <span data-ttu-id="3fb7d-122">Hello, toomigrate을 원본으로 Azure를 선택 하는 Vm에 대 한 복제를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fb7d-122">Enable replication for hello VMs you want toomigrate, and choose Azure as source.</span></span> 
3. <span data-ttu-id="3fb7d-123">[ 계획되지 않은 장애 조치를 실행합니다](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="3fb7d-123">[ Run an unplanned failover](site-recovery-failover.md).</span></span> <span data-ttu-id="3fb7d-124">초기 복제가 완료 된 후에 하나의 Azure 지역 tooanother에서 예기치 않은 장애 조치가 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fb7d-124">After initial replication is complete, you can run an unplanned failover from one Azure region tooanother.</span></span> <span data-ttu-id="3fb7d-125">필요에 따라 복구 계획을 만들어야 하 고 지역 간 예기치 않은 장애 조치가, toomigrate 여러 가상 컴퓨터를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fb7d-125">Optionally, you can create a recovery plan and run an unplanned failover, toomigrate multiple virtual machines between regions.</span></span> <span data-ttu-id="3fb7d-126">[자세히 알아봅니다](site-recovery-create-recovery-plans.md) .</span><span class="sxs-lookup"><span data-stu-id="3fb7d-126">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3fb7d-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3fb7d-127">Next steps</span></span>
<span data-ttu-id="3fb7d-128">[Azure Site Recovery란?](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="3fb7d-128">Learn more about other replication scenarios in [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>
