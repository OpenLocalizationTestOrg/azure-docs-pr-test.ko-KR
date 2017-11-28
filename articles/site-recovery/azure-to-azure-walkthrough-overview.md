---
title: "Azure 지역 간에 Azure Vm aaaReplicate | Microsoft Docs"
description: "Hello 단계 필요한 tooreplicate를 Azure Vm hello Azure 포털에서에서 hello Azure Site Recovery 서비스와 Azure 지역 간 요약 되어 있습니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 6dd36239-4363-4538-bf80-a18e71b8ec67
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: f4ac386f040945131f8a10f02143437f4441e298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="d25c8-103">Azure Site Recovery를 사용하여 지역 간 Azure VM 복제</span><span class="sxs-lookup"><span data-stu-id="d25c8-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

><span data-ttu-id="d25c8-104">이 문서에서는 Azure 지역 tooAzure 다른 지역에 Vm에서에서 Azure 가상 컴퓨터 (Vm) hello 단계 필요한 tooreplicate의 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d25c8-104">This article provides an overview of hello steps required tooreplicate Azure virtual machines (VMs) in one Azure region tooAzure VMs in a different region.</span></span> 

>[!NOTE]
>
> <span data-ttu-id="d25c8-105">Azure VM 복제는 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d25c8-105">Azure VM replication is currently in preview.</span></span>

<span data-ttu-id="d25c8-106">Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="d25c8-106">Post comments and questions at hello bottom of this article or on hello [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="step-1-review-architecture"></a><span data-ttu-id="d25c8-107">1단계: 아키텍처 검토</span><span class="sxs-lookup"><span data-stu-id="d25c8-107">Step 1: Review architecture</span></span>

<span data-ttu-id="d25c8-108">배포를 시작 하기 전에 hello 시나리오 아키텍처 및 toodeploy 필요한 hello 구성 요소를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="d25c8-108">Before you start deployment, review hello scenario architecture, and hello components you need toodeploy.</span></span>

<span data-ttu-id="d25c8-109">너무 이동[1 단계: hello 아키텍처 검토](azure-to-azure-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="d25c8-109">Go too[Step 1: Review hello architecture](azure-to-azure-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="d25c8-110">2단계: 필수 구성 요소 검토</span><span class="sxs-lookup"><span data-stu-id="d25c8-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="d25c8-111">구독, 가상 네트워크, 저장소 계정 및 VM 요구 사항을 비롯 한 위치에서 필수 구성 요소를 Azure에 hello가 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d25c8-111">Check that you have hello Azure prerequisites in places, including a subscription, virtual networks, storage accounts, and VM requirements.</span></span>

<span data-ttu-id="d25c8-112">너무 이동[2 단계: 사전 요구 사항 및 제한 사항 확인](azure-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="d25c8-112">Go too[Step 2: Verify prerequisites and limitations](azure-to-azure-walkthrough-prerequisites.md)</span></span>


## <a name="step-3-plan-networking"></a><span data-ttu-id="d25c8-113">3단계: 네트워킹 계획</span><span class="sxs-lookup"><span data-stu-id="d25c8-113">Step 3: Plan networking</span></span>

<span data-ttu-id="d25c8-114">아웃 바운드 연결 tooreplicate, 온-프레미스에서 연결 설정 하 고 원하는 Azure Vm에 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d25c8-114">Check that outbound connectivity is set up on Azure VMs you want tooreplicate, and that connections from on-premises are set up.</span></span>

<span data-ttu-id="d25c8-115">너무 이동[4 단계: 네트워킹 계획](azure-to-azure-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="d25c8-115">Go too[Step 4: Plan networking](azure-to-azure-walkthrough-network.md)</span></span>



## <a name="step-4-create-a-vault"></a><span data-ttu-id="d25c8-116">4단계: 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="d25c8-116">Step 4: Create a vault</span></span> 

<span data-ttu-id="d25c8-117">복제를 관리 하며 hello 소스 지역을 지정 복구 서비스 자격 증명 모음 tooorchestrate tooset 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d25c8-117">You need tooset up a Recovery Services vault tooorchestrate and manage replication, and specify hello source region.</span></span>

<span data-ttu-id="d25c8-118">너무 이동[4 단계: 자격 증명 모음 만들기](azure-to-azure-walkthrough-vault.md)</span><span class="sxs-lookup"><span data-stu-id="d25c8-118">Go too[Step 4: Create a vault](azure-to-azure-walkthrough-vault.md)</span></span>


## <a name="step-5-enable-replication"></a><span data-ttu-id="d25c8-119">5단계: 복제 사용</span><span class="sxs-lookup"><span data-stu-id="d25c8-119">Step 5: Enable replication</span></span>


<span data-ttu-id="d25c8-120">tooenable 복제 대상 위치 설정을 구성 하 고 복제 정책을 설정한 tooreplicate 원하는 hello Azure Vm을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d25c8-120">tooenable replication, you configure target location settings, set up a replication policy, and select hello Azure VMs that you want tooreplicate.</span></span> <span data-ttu-id="d25c8-121">를 사용 하도록 설정한 후 hello VM의 초기 복제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="d25c8-121">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="d25c8-122">너무 이동[5 단계: 복제 사용](azure-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="d25c8-122">Go too[Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>


## <a name="step-6-run-a-test-failover"></a><span data-ttu-id="d25c8-123">6단계: 테스트 장애 조치 실행</span><span class="sxs-lookup"><span data-stu-id="d25c8-123">Step 6: Run a test failover</span></span>

<span data-ttu-id="d25c8-124">초기 복제가 완료 된 후 델타 복제 실행 되 고 정상적으로 작동 하는지 테스트 장애 조치 toomake를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d25c8-124">After initial replication finishes, and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="d25c8-125">너무 이동[6 단계: 테스트 장애 조치 실행](azure-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="d25c8-125">Go too[Step 6: Run a test failover](azure-to-azure-walkthrough-test-failover.md)</span></span>


