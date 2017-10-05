---
title: "Azure 지역 간에 Azure IaaS VM 마이그레이션 | Microsoft Docs"
description: "Azure Site Recovery를 사용하여 Azure 지역 간에 Azure IaaS 가상 컴퓨터를 마이그레이션합니다."
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
ms.openlocfilehash: ef2972c077a2b1dd2b2fd6ce53cc6560520ea870
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-azure-iaas-virtual-machines-between-azure-regions-with-azure-site-recovery"></a><span data-ttu-id="da2cf-103">Azure Site Recovery를 사용하여 Azure 지역 간에 Azure IaaS 가상 컴퓨터 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="da2cf-103">Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery</span></span>
## <a name="overview"></a><span data-ttu-id="da2cf-104">개요</span><span class="sxs-lookup"><span data-stu-id="da2cf-104">Overview</span></span>
<span data-ttu-id="da2cf-105">Azure Site Recovery에 오신 것을 환영합니다!</span><span class="sxs-lookup"><span data-stu-id="da2cf-105">Welcome to Azure Site Recovery!</span></span> <span data-ttu-id="da2cf-106">Azure 지역 간에 Azure VM을 마이그레이션할 경우 이 문서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="da2cf-106">Use this article if you want to migrate Azure VMs between Azure regions.</span></span> <span data-ttu-id="da2cf-107">시작하기 전에 다음 사항에 주의하세요.</span><span class="sxs-lookup"><span data-stu-id="da2cf-107">Before you start, note that:</span></span>

* <span data-ttu-id="da2cf-108">Azure에는 리소스를 만들고 작업하기 위한 두 가지 배포 모델인 Azure Resource Manager 배포 모델과 클래식 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da2cf-108">Azure has two different deployment models for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="da2cf-109">또한 Azure에는 두 가지 포털이 있는데, 하나는 클래식 배포 모델을 지원하는 Azure 클래식 포털이고 다른 하나는 두 가지 배포 모델을 모두 지원하는 Azure 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="da2cf-109">Azure also has two portals – the Azure classic portal that supports the classic deployment model, and the Azure portal with support for both deployment models.</span></span> <span data-ttu-id="da2cf-110">Resource Manager와 클래식 중에서 Site Recovery를 어떤 방식으로 구성하든 마이그레이션의 기본 단계는 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="da2cf-110">The basic steps for migration are the same whether you're configuring Site Recovery in Resource Manager or in classic.</span></span> <span data-ttu-id="da2cf-111">그러나 이 문서의 UI 지침과 스크린샷은 Azure 포털과 관련된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="da2cf-111">However the UI instructions and screenshots in this article are relevant for the Azure portal.</span></span>
* <span data-ttu-id="da2cf-112">**현재 한 지역에서 다른 지역으로만 마이그레이션할 수 있습니다. 한 Azure 지역에서 다른 지역으로 VM을 장애 조치(failover)할 수 있으나 장애 복구(failback)할 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="da2cf-112">**Currently you can only migrate from one region to another. You can fail over VMs from one Azure region to another, but you can't fail them back again.**</span></span>

<span data-ttu-id="da2cf-113">이 문서의 하단 또는 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 의견이나 질문을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="da2cf-113">Post any comments or questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="da2cf-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="da2cf-114">Prerequisites</span></span>
<span data-ttu-id="da2cf-115">이 배포에 대해 필요한 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="da2cf-115">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="da2cf-116">**IaaS 가상 컴퓨터**: 마이그레이션하려는 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="da2cf-116">**IaaS virtual machines**: The VMs you want to migrate.</span></span> <span data-ttu-id="da2cf-117">이러한 VM을 실제 컴퓨터로 간주하여 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="da2cf-117">You migrate these VMs by treating them as physical machines.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="da2cf-118">배포 단계</span><span class="sxs-lookup"><span data-stu-id="da2cf-118">Deployment steps</span></span>
<span data-ttu-id="da2cf-119">이 섹션에서는 새 Azure 포털의 배포 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="da2cf-119">This section describes the deployment steps in the new Azure portal.</span></span>

1. <span data-ttu-id="da2cf-120">[자격 증명 모음을 만듭니다](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="da2cf-120">[Create a vault](site-recovery-vmware-to-azure.md).</span></span>
2. <span data-ttu-id="da2cf-121">[복제를 활성화합니다](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="da2cf-121">[Enable replication](site-recovery-vmware-to-azure.md).</span></span> <span data-ttu-id="da2cf-122">마이그레이션할 VM에 대해 복제를 사용하도록 설정하고 Azure를 원본으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da2cf-122">Enable replication for the VMs you want to migrate, and choose Azure as source.</span></span> 
3. <span data-ttu-id="da2cf-123">[ 계획되지 않은 장애 조치를 실행합니다](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="da2cf-123">[ Run an unplanned failover](site-recovery-failover.md).</span></span> <span data-ttu-id="da2cf-124">초기 복제가 완료된 후에 Azure 지역 간에 계획되지 않은 장애 조치를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da2cf-124">After initial replication is complete, you can run an unplanned failover from one Azure region to another.</span></span> <span data-ttu-id="da2cf-125">선택적으로 복구 계획을 만들고 장애 조치를 실행하여 Azure 지역 간에 여러 가상 컴퓨터를 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da2cf-125">Optionally, you can create a recovery plan and run an unplanned failover, to migrate multiple virtual machines between regions.</span></span> <span data-ttu-id="da2cf-126">[자세히 알아봅니다](site-recovery-create-recovery-plans.md) .</span><span class="sxs-lookup"><span data-stu-id="da2cf-126">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da2cf-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="da2cf-127">Next steps</span></span>
<span data-ttu-id="da2cf-128">[Azure Site Recovery란?](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="da2cf-128">Learn more about other replication scenarios in [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>
