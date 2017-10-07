---
title: "hello 소스 및 대상에 Azure 사이트 복구와 Hyper-v 복제 tooAzure (System Center VMM 없음)를 aaaSet | Microsoft Docs"
description: "Azure Site Recovery를 사용 하 여 Hyper-v Vm tooAzure 저장소의 복제에 대 한 원본 및 대상 설정을 hello 단계 tooset을 요약 되어 있습니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d2010d85-77fd-4dea-84f3-1c960ed4c63f
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 105b90e6ac053d5b842c54a36c460a26d0f5c2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-replication-tooazure"></a><span data-ttu-id="17e72-103">8 단계: hello 소스 및 대상 Hyper-v 복제 tooAzure에 대 한 설정</span><span class="sxs-lookup"><span data-stu-id="17e72-103">Step 8: Set up hello source and target for Hyper-V replication tooAzure</span></span>

<span data-ttu-id="17e72-104">이 문서에서는 어떻게 tooconfigure 원본 및 대상 설정을 복제할 때 온-프레미스 Hyper-v 가상 컴퓨터 (System Center VMM) 없이 tooAzure hello를 사용 하 여 설명 [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-104">This article describes how tooconfigure source and target settings when replicating on-premises Hyper-V virtual machines (without System Center VMM) tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="17e72-105">Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="17e72-106">Hello 소스 환경 설정</span><span class="sxs-lookup"><span data-stu-id="17e72-106">Set up hello source environment</span></span>

<span data-ttu-id="17e72-107">Hello 하이퍼-V 사이트를 설정 하 고, Hyper-v 호스트에 hello Azure Site Recovery Provider 및 hello Azure 복구 서비스 에이전트를 설치 하 고 및 hello 사이트 hello 자격 증명 모음에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-107">Set up hello Hyper-V site, install hello Azure Site Recovery Provider and hello Azure Recovery Services agent on Hyper-V hosts, and register hello site in hello vault.</span></span>

1. <span data-ttu-id="17e72-108">**인프라 준비**에서 **원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-108">In **Prepare Infrastructure**, click **Source**.</span></span> <span data-ttu-id="17e72-109">새 Hyper-v 사이트에 Hyper-v 호스트 또는 클러스터에 대 한 컨테이너로 tooadd 클릭 **+ Hyper-v 사이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-109">tooadd a new Hyper-V site as a container for your Hyper-V hosts or clusters, click **+Hyper-V Site**.</span></span>

    ![원본 설정](./media/hyper-v-site-walkthrough-source-target/set-source1.png)
2. <span data-ttu-id="17e72-111">**만들 Hyper-v 사이트**, hello 사이트에 대 한 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-111">In **Create Hyper-V site**, specify a name for hello site.</span></span> <span data-ttu-id="17e72-112">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-112">Then click **OK**.</span></span> <span data-ttu-id="17e72-113">이제 작성 하 고 클릭 하 여 hello 사이트를 선택 **+ Hyper-v 서버** tooadd 서버 toohello 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-113">Now, select hello site you created, and click **+Hyper-V Server** tooadd a server toohello site.</span></span>

    ![원본 설정](./media/hyper-v-site-walkthrough-source-target/set-source2.png)

3. <span data-ttu-id="17e72-115">**서버 추가** > **서버 형식**에 **Hyper-V 서버**가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-115">In **Add Server** > **Server type**, check that **Hyper-V server** is displayed.</span></span>

    - <span data-ttu-id="17e72-116">Tooadd hello를 준수 하는 것이 원하는 hello Hyper-v server에 해당 하는지 확인 한 [필수 구성 요소](#on-premises-prerequisites), 및가 수 tooaccess hello 지정 된 Url입니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-116">Make sure that hello Hyper-V server you want tooadd complies with hello [prerequisites](#on-premises-prerequisites), and is able tooaccess hello specified URLs.</span></span>
    - <span data-ttu-id="17e72-117">Hello Azure Site Recovery Provider 설치 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-117">Download hello Azure Site Recovery Provider installation file.</span></span> <span data-ttu-id="17e72-118">이 파일 tooinstall hello 공급자를 실행 하 고 각 Hyper-v 호스트에서 복구 서비스 에이전트 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-118">You run this file tooinstall hello Provider and hello Recovery Services agent on each Hyper-V host.</span></span>

    ![원본 설정](./media/hyper-v-site-walkthrough-source-target/set-source3.png)


## <a name="install-hello-provider-and-agent"></a><span data-ttu-id="17e72-120">Hello 공급자 및 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="17e72-120">Install hello Provider and agent</span></span>

1. <span data-ttu-id="17e72-121">Toohello 하이퍼-V 사이트를 추가 각 호스트에서 hello 공급자 설치 파일을 실행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-121">Run hello Provider setup file on each host you added toohello Hyper-V site.</span></span> <span data-ttu-id="17e72-122">Hyper-V 클러스터에 설치하는 경우 각 클러스터 노드에서 설치 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-122">If you're installing on a Hyper-V cluster, run setup on each cluster node.</span></span> <span data-ttu-id="17e72-123">각 Hyper-V 클러스터 노드를 설치하고 등록하면 노드 간 마이그레이션에서도 VM이 안전하게 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-123">Installing and registering each Hyper-V cluster node ensures that VMs are protected, even if they migrate across nodes.</span></span>
2. <span data-ttu-id="17e72-124">Microsoft Update 정책에 따라 공급자 업데이트가 설치되도록 **Microsoft Update**에서 업데이트를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-124">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="17e72-125">**설치**, 수락 하거나 hello 기본 공급자 설치 위치를 수정 하 고 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-125">In **Installation**, accept or modify hello default Provider installation location and click **Install**.</span></span>
4. <span data-ttu-id="17e72-126">**자격 증명 모음 설정을**, 클릭 **찾아보기** tooselect hello 자격 증명 모음 키 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-126">In **Vault Settings**, click **Browse** tooselect hello vault key file that you downloaded.</span></span> <span data-ttu-id="17e72-127">Hello Azure Site Recovery 구독 hello 자격 증명 모음 이름을 지정 하 고 hello 하이퍼-V 사이트 toowhich hello Hyper-v 서버가 속하는 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-127">Specify hello Azure Site Recovery subscription, hello vault name, and hello Hyper-V site toowhich hello Hyper-V server belongs.</span></span>

    ![서버 등록](./media/hyper-v-site-walkthrough-source-target/provider3.png)

5. <span data-ttu-id="17e72-129">**프록시 설정을**, Hyper-v 호스트에서 실행 중인 공급자를 통해 tooAzure 사이트 복구를 연결 하는 hello 인터넷 hello 하는 방법을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-129">In **Proxy Settings**, specify how hello Provider running on Hyper-V hosts connects tooAzure Site Recovery over hello internet.</span></span>

    * <span data-ttu-id="17e72-130">Hello 공급자 tooconnect 직접 선택 하려면 **tooAzure Site Recovery 프록시 없이 직접 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-130">If you want hello Provider tooconnect directly select **Connect directly tooAzure Site Recovery without a proxy**.</span></span>
    * <span data-ttu-id="17e72-131">기존 프록시 인증 필요 hello 공급자 연결에 대 한 사용자 지정 프록시 toouse를 원하는 경우 선택 **연결에서 프록시 서버를 사용 하 여 사이트 복구 tooAzure**합니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-131">If your existing proxy requires authentication, or you want toouse a custom proxy for hello Provider connection, select **Connect tooAzure Site Recovery using a proxy server**.</span></span>
    * <span data-ttu-id="17e72-132">프록시를 사용하는 경우:</span><span class="sxs-lookup"><span data-stu-id="17e72-132">If you use a proxy:</span></span>
        - <span data-ttu-id="17e72-133">Hello 주소, 포트 및 자격 증명을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-133">Specify hello address, port, and credentials</span></span>
        - <span data-ttu-id="17e72-134">Hello에 설명 된 있는지 hello Url 확인 [필수 구성 요소](#prerequisites) hello 프록시를 통해 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-134">Make sure hello URLs described in hello [prerequisites](#prerequisites) are allowed through hello proxy.</span></span>

    ![인터넷](./media/hyper-v-site-walkthrough-source-target/provider7.png)

6. <span data-ttu-id="17e72-136">설치를 마친 후 클릭 **등록** tooregister hello 서버 hello 자격 증명 모음에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-136">After installation finishes, click **Register** tooregister hello server in hello vault.</span></span>

    ![설치 위치](./media/hyper-v-site-walkthrough-source-target/provider2.png)

7. <span data-ttu-id="17e72-138">등록 완료 되 면 hello Hyper-v 서버에서 메타 데이터를 Azure Site Recovery에서 검색 되 고 hello 서버에 표시 되 **사이트 복구 인프라** > **Hyper-v 호스트**합니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-138">After registration finishes, metadata from hello Hyper-V server is retrieved by Azure Site Recovery, and hello server is displayed in **Site Recovery Infrastructure** > **Hyper-V Hosts**.</span></span>


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="17e72-139">Hello 대상 환경 설정</span><span class="sxs-lookup"><span data-stu-id="17e72-139">Set up hello target environment</span></span>

<span data-ttu-id="17e72-140">복제에 대 한 hello Azure 저장소 계정을 지정 하 고 hello Azure 네트워크 toowhich Azure Vm 장애 조치 후 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-140">Specify hello Azure storage account for replication, and hello Azure network toowhich Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="17e72-141">**인프라 준비** > **대상**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-141">Click **Prepare infrastructure** > **Target**.</span></span>
2. <span data-ttu-id="17e72-142">Hello 구독 및 장애 조치 후 toocreate hello Azure Vm 만들려는 hello 리소스 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-142">Select hello subscription and hello resource group in which you want toocreate hello Azure VMs after failover.</span></span> <span data-ttu-id="17e72-143">Hello 배포 선택 hello Vm에 대 한 Azure (기본 또는 리소스 관리)에서 toouse 되도록 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-143">Choose hello deployment model that you want toouse in Azure (classic or resource management) for hello VMs.</span></span>

3. <span data-ttu-id="17e72-144">Site Recovery가 호환되는 Azure 저장소 계정 및 네트워크가 하나 이상 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-144">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    - <span data-ttu-id="17e72-145">저장소 계정에 없으면 클릭 **+ 저장소** toocreate 리소스 관리자 기반 계정 인라인 합니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-145">If you don't have a storage account, click **+Storage** toocreate a Resource Manager-based account inline.</span></span> 
    - <span data-ttu-id="17e72-146">Azure 네트워크를 설정 하지 않은 경우 클릭 **+ 네트워크** toocreate 리소스 관리자 기반 네트워크 인라인 합니다.</span><span class="sxs-lookup"><span data-stu-id="17e72-146">If you don't have a Azure network, click **+Network** toocreate a Resource Manager-based network inline.</span></span>






## <a name="next-steps"></a><span data-ttu-id="17e72-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="17e72-147">Next steps</span></span>

<span data-ttu-id="17e72-148">너무 이동[9 단계: 복제 정책 설정](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="17e72-148">Go too[Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>
