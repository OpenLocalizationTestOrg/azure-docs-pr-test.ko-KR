---
title: "hello 소스 및 대상에 Azure Site Recovery와 실제 서버 복제 tooAzure aaaSet | Microsoft Docs"
description: "물리적 서버 tooAzure 저장소 hello Azure Site Recovery 서비스와의 복제에 대 한 원본 및 대상 설정을 hello 단계 tooset을 요약 되어 있습니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 2e3d03bc-4e53-4590-8a01-f702d3cc9500
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: e75ef23174d77509bf54380eba8f251a7337a45f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-hello-source-and-target-for-physical-server-replication-tooazure"></a><span data-ttu-id="f960f-103">7 단계: hello 원본 및 복제 tooAzure 물리적 서버에 대 한 대상 설정</span><span class="sxs-lookup"><span data-stu-id="f960f-103">Step 7: Set up hello source and target for physical server replication tooAzure</span></span>

<span data-ttu-id="f960f-104">이 문서에서는 어떻게 tooconfigure 원본 및 대상 설정을 복제할 때 온-프레미스 물리적 서버 tooAzure hello를 사용 하 여 설명 [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="f960f-104">This article describes how tooconfigure source and target settings when replicating on-premises physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="f960f-105">Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="f960f-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="f960f-106">Hello 소스 환경 설정</span><span class="sxs-lookup"><span data-stu-id="f960f-106">Set up hello source environment</span></span>

<span data-ttu-id="f960f-107">Hello 구성 서버를 설정 하 고 hello 자격 증명 모음에 등록 한 다음 컴퓨터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="f960f-107">Set up hello configuration server, register it in hello vault, and discover machines.</span></span>

1. <span data-ttu-id="f960f-108">**Site Recovery** > **1단계: 인프라 준비** > **원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f960f-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="f960f-109">구성 서버가 없는 경우 **+구성 서버**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f960f-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="f960f-110">**서버 추가**에서 **구성 서버**가 **서버 형식**에 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f960f-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="f960f-111">Hello Site Recovery 통합 설치 설치 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="f960f-111">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="f960f-112">Hello 자격 증명 모음 등록 키를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="f960f-112">Download hello vault registration key.</span></span> <span data-ttu-id="f960f-113">통합 설치를 실행할 때 이 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f960f-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="f960f-114">hello 키가 생성 한 후 5 일 동안 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="f960f-114">hello key is valid for five days after you generate it.</span></span>

   ![원본 설정](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a><span data-ttu-id="f960f-116">Hello 구성 서버 hello 자격 증명 모음 등록</span><span class="sxs-lookup"><span data-stu-id="f960f-116">Register hello configuration server in hello vault</span></span>

<span data-ttu-id="f960f-117">수행 하기 전에 hello 다음로 시작 하 고 통합 설치 tooinstall hello 구성 서버, hello 프로세스 서버 및 마스터 대상 서버 hello 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f960f-117">Do hello following before you start, then run Unified Setup tooinstall hello configuration server, hello process server, and hello master target server.</span></span> <span data-ttu-id="f960f-118">비디오 hello 설정을 VMware VM tooAzure 복제에 대 한 hello 구성 요소를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f960f-118">hello video describes setting up hello components for VMware VM tooAzure replication.</span></span> <span data-ttu-id="f960f-119">그러나 hello 동일한 프로세스에 대해 올바른지 물리적 서버 tooAzure 복제.</span><span class="sxs-lookup"><span data-stu-id="f960f-119">However, hello same process is valid for physical server tooAzure replication.</span></span>

- <span data-ttu-id="f960f-120">Hello 구성 서버 VM에서 해당 hello 시스템 시계와 동기화 되었는지 확인 한 [시간 서버](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service)합니다.</span><span class="sxs-lookup"><span data-stu-id="f960f-120">On hello configuration server VM, make sure that hello system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="f960f-121">서로 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f960f-121">It should match.</span></span> <span data-ttu-id="f960f-122">15분 빠르거나 늦은 경우 설치가 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f960f-122">If it's 15 minutes in front or behind, setup might fail.</span></span>
- <span data-ttu-id="f960f-123">Hello 구성 서버 컴퓨터에 로컬 관리자로 설치 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f960f-123">Run setup as a Local Administrator on hello configuration server machine.</span></span>
- <span data-ttu-id="f960f-124">Hello VM에서 TLS 1.0을 사용할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f960f-124">Make sure TLS 1.0 is enabled on hello VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="f960f-125">hello 구성 서버를 설치할 수도 있습니다 [hello 명령줄에서](http://aka.ms/installconfigsrv)합니다.</span><span class="sxs-lookup"><span data-stu-id="f960f-125">hello configuration server can also be installed [from hello command line](http://aka.ms/installconfigsrv).</span></span>




## <a name="set-up-hello-target-environment"></a><span data-ttu-id="f960f-126">Hello 대상 환경 설정</span><span class="sxs-lookup"><span data-stu-id="f960f-126">Set up hello target environment</span></span>

<span data-ttu-id="f960f-127">Hello 대상 환경 설정 하기 전에 Azure 저장소 계정 및 가상 네트워크를 설정 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f960f-127">Before you set up hello target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="f960f-128">클릭 **준비 인프라** > **대상**, 선택 hello toouse를 원하는 Azure 구독 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="f960f-128">Click **Prepare infrastructure** > **Target**, and select hello Azure subscription you want toouse.</span></span>
2. <span data-ttu-id="f960f-129">대상 배포 모델이 리소스 관리자 기반인지, 클래식인지 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f960f-129">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="f960f-130">Site Recovery가 호환되는 Azure 저장소 계정 및 네트워크가 하나 이상 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f960f-130">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![대상](./media/physical-walkthrough-source-target/gs-target.png)

4. <span data-ttu-id="f960f-132">저장소 계정 또는 네트워크를 만들지 않은 경우 클릭 **저장소 계정 추가** 또는 **+ 네트워크**, 리소스 관리자 계정 또는 네트워크 인라인 toocreate 합니다.</span><span class="sxs-lookup"><span data-stu-id="f960f-132">If you haven't created a storage account or network, click **+Storage account** or **+Network**, toocreate a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f960f-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f960f-133">Next steps</span></span>

<span data-ttu-id="f960f-134">너무 이동[8 단계: 복제 정책 설정](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="f960f-134">Go too[Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>
