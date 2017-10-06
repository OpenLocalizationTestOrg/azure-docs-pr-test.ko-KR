---
title: "hello 소스 및 대상에 Azure 사이트 복구와 Hyper-v 복제 tooa 보조 사이트를 aaaSet | Microsoft Docs"
description: "어떻게 tooset hello 소스 및 대상 때 설명 Azure Site Recovery와 VMM toosecondary 사이트 Hyper-v Vm을 복제 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: fa7809f1-7633-425f-b25d-d10d004e8d0b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 451cb4413ca5c09777a7faf512b1c8ea43e695f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-hello-replication-source-and-target"></a><span data-ttu-id="ce9e2-103">6 단계: hello 복제 원본 및 대상 설정</span><span class="sxs-lookup"><span data-stu-id="ce9e2-103">Step 6: Set up hello replication source and target</span></span>


<span data-ttu-id="ce9e2-104">Hyper-v 복제 tooa 보조 VMM 사이트에 대 한 자격 증명 모음 복구 서비스를 만든 후 [Azure Site Recovery](site-recovery-overview.md),이 문서 tooset hello 소스를 사용 하 고 복제 위치 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-104">After creating a Recovery Services vault for Hyper-V replication tooa secondary VMM site with [Azure Site Recovery](site-recovery-overview.md), use this article tooset up hello source and target replication locations.</span></span> 

<span data-ttu-id="ce9e2-105">이 문서를 읽은 후 게시 설명을 hello 맨 아래에 하거나 hello에 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="set-up-hello-source-environment"></a><span data-ttu-id="ce9e2-106">Hello 소스 환경 설정</span><span class="sxs-lookup"><span data-stu-id="ce9e2-106">Set up hello source environment</span></span>

<span data-ttu-id="ce9e2-107">VMM 서버에 hello Azure Site Recovery Provider를 설치 하 고 검색 및 hello 자격 증명 모음에 서버를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-107">Install hello Azure Site Recovery Provider on VMM servers, and discover and register servers in hello vault.</span></span>

1. <span data-ttu-id="ce9e2-108">**1단계: 인프라 준비** > **원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-108">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span>

    ![원본 설정](./media/vmm-to-vmm-walkthrough-source-target/goals-source.png)
2. <span data-ttu-id="ce9e2-110">**준비 소스**, 클릭 **+ VMM** tooadd VMM 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-110">In **Prepare source**, click **+ VMM** tooadd a VMM server.</span></span>

    ![원본 설정](./media/vmm-to-vmm-walkthrough-source-target/set-source1.png)
3. <span data-ttu-id="ce9e2-112">**서버 추가**, 있는지 여부를 확인 **System Center VMM 서버** 에 표시 **서버 유형** 해당 hello VMM 서버 hello 충족 [필수구성요소](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="ce9e2-112">In **Add Server**, check that **System Center VMM server** appears in **Server type** and that hello VMM server meets hello [prerequisites](#prerequisites).</span></span>
4. <span data-ttu-id="ce9e2-113">Hello Azure Site Recovery Provider 설치 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-113">Download hello Azure Site Recovery Provider installation file.</span></span>
5. <span data-ttu-id="ce9e2-114">Hello 등록 키를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-114">Download hello registration key.</span></span> <span data-ttu-id="ce9e2-115">설정을 실행할 때 이 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-115">You need this when you run setup.</span></span> <span data-ttu-id="ce9e2-116">hello 키가 생성 한 후 5 일 동안 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-116">hello key is valid for five days after you generate it.</span></span>

    ![원본 설정](./media/vmm-to-vmm-walkthrough-source-target/set-source3.png)
6. <span data-ttu-id="ce9e2-118">VMM 서버 hello에 hello Azure Site Recovery Provider를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-118">Install hello Azure Site Recovery Provider on hello VMM server.</span></span> <span data-ttu-id="ce9e2-119">필요 하지 않습니다 tooexplicitly Hyper-v 호스트 서버에 아무 것도 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-119">You don't need tooexplicitly install anything on Hyper-V host servers.</span></span>


## <a name="install-hello-azure-site-recovery-provider"></a><span data-ttu-id="ce9e2-120">Hello Azure Site Recovery Provider 설치</span><span class="sxs-lookup"><span data-stu-id="ce9e2-120">Install hello Azure Site Recovery Provider</span></span>

1. <span data-ttu-id="ce9e2-121">각 VMM 서버에 hello 공급자 설정 파일을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-121">Run hello Provider setup file on each VMM server.</span></span> <span data-ttu-id="ce9e2-122">VMM 클러스터에 배포 된 hello hello 처음 설치할 때 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-122">If VMM is deployed in a cluster, do hello following hello first time you install:</span></span>
    -  <span data-ttu-id="ce9e2-123">액티브 노드에서 hello 공급자를 설치 하 고 hello 자격 증명 모음에 hello 설치 tooregister hello VMM 서버를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-123">Install hello provider on an active node, and finish hello installation tooregister hello VMM server in hello vault.</span></span>
    - <span data-ttu-id="ce9e2-124">그런 다음 설치 hello 공급자 hello에 다른 노드.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-124">Then, install hello Provider on hello other nodes.</span></span> <span data-ttu-id="ce9e2-125">클러스터 노드 hello 실행할지 동일한 버전의 hello 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-125">Cluster nodes should all run hello same version of hello Provider.</span></span>
2. <span data-ttu-id="ce9e2-126">설치 프로그램 몇 가지 필수 구성 요소 검사를 실행 하 고 권한 toostop hello VMM 서비스를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-126">Setup runs a few prerequisite checks, and requests permission toostop hello VMM service.</span></span> <span data-ttu-id="ce9e2-127">자동으로 설치가 완료 되 면 hello VMM 서비스에 다시 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-127">hello VMM service will be restarted automatically when setup finishes.</span></span> <span data-ttu-id="ce9e2-128">VMM 클러스터를 설치 하는 경우 메시지 표시 toostop hello 클러스터 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-128">If you install on a VMM cluster, you're prompted toostop hello Cluster role.</span></span>
3. <span data-ttu-id="ce9e2-129">**Microsoft Update**, 공급자 업데이트가 Microsoft Update 정책에 따라 설치 되어 있는지 toospecify에 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-129">In **Microsoft Update**, you can opt in toospecify that provider updates are installed in accordance with your Microsoft Update policy.</span></span>
4. <span data-ttu-id="ce9e2-130">**설치**, 수락 하거나 hello 기본 설치 위치를 수정 하 고 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-130">In **Installation**, accept or modify hello default installation location, and click **Install**.</span></span>

    ![설치 위치](./media/vmm-to-vmm-walkthrough-source-target/provider-location.png)
5. <span data-ttu-id="ce9e2-132">설치가 완료 되 면 클릭 **등록** tooregister hello 서버 hello 자격 증명 모음에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-132">After installation is complete, click **Register** tooregister hello server in hello vault.</span></span>

    ![설치 위치](./media/vmm-to-vmm-walkthrough-source-target/provider-register.png)
6. <span data-ttu-id="ce9e2-134">**자격 증명 모음 이름**, hello는 hello 서버를 등록할 자격 증명 모음의 hello 이름이 유효한 지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-134">In **Vault name**, verify hello name of hello vault in which hello server will be registered.</span></span> <span data-ttu-id="ce9e2-135">*다음*을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-135">Click *Next*.</span></span>

    ![서버 등록](./media/vmm-to-vmm-walkthrough-source-target/vaultcred.png)
7. <span data-ttu-id="ce9e2-137">**인터넷 연결**, hello VMM 서버에서 실행 되는 hello 공급자 tooAzure를 연결 하는 방법을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-137">In **Internet Connection**, specify how hello provider running on hello VMM server connects tooAzure.</span></span>

    ![인터넷 설정](./media/vmm-to-vmm-walkthrough-source-target/proxydetails.png)

   - <span data-ttu-id="ce9e2-139">해당 hello 공급자 직접 toohello 연결 되도록 지정할 수 있습니다, 인터넷 또는 프록시를 통해.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-139">You can specify that hello provider should connect directly toohello internet, or via a proxy.</span></span>
   - <span data-ttu-id="ce9e2-140">필요한 경우 프록시 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-140">Specify proxy settings if needed.</span></span>
   - <span data-ttu-id="ce9e2-141">VMM RunAs 계정 (DRAProxyAccount) 지정 하는 hello를 사용 하 여 자동으로 만들어집니다 프록시를 사용 하는 경우 프록시 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-141">If you use a proxy, a VMM RunAs account (DRAProxyAccount) is created automatically using hello specified proxy credentials.</span></span> <span data-ttu-id="ce9e2-142">이 계정을 올바르게 인증할 수 있도록 hello 프록시 서버를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-142">Configure hello proxy server so that this account can authenticate successfully.</span></span> <span data-ttu-id="ce9e2-143">hello RunAs 계정 설정은 수정할 수 있는 hello VMM 콘솔에서 > **설정** > **보안** > **실행 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-143">hello RunAs account settings can be modified in hello VMM console > **Settings** > **Security** > **Run As Accounts**.</span></span> <span data-ttu-id="ce9e2-144">VMM 서비스 tooupdate 변경 hello를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-144">Restart hello VMM service tooupdate changes.</span></span>
8. <span data-ttu-id="ce9e2-145">**등록 키**선택, hello 키를 Azure Site Recovery에서 다운로드 한 toohello VMM 서버에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-145">In **Registration Key**, select hello key that you downloaded from Azure Site Recovery and copied toohello VMM server.</span></span>
9. <span data-ttu-id="ce9e2-146">hello 암호화 설정은 VMM 클라우드에 tooAzure의 Hyper-v Vm을 복제 하는 경우에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-146">hello encryption setting is only used when you're replicating Hyper-V VMs in VMM clouds tooAzure.</span></span> <span data-ttu-id="ce9e2-147">Tooa 보조 사이트를 복제 하는 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-147">If you're replicating tooa secondary site it's not used.</span></span>
10. <span data-ttu-id="ce9e2-148">**서버 이름**, hello 자격 증명 모음에 친숙 한 이름 tooidentify hello VMM 서버를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-148">In **Server name**, specify a friendly name tooidentify hello VMM server in hello vault.</span></span> <span data-ttu-id="ce9e2-149">클러스터 구성에서 hello VMM 클러스터 역할 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-149">In a cluster configuration specify hello VMM cluster role name.</span></span>
11. <span data-ttu-id="ce9e2-150">**클라우드 메타 데이터 동기화**hello 자격 증명 모음과 hello VMM 서버의 모든 클라우드에 대 한 toosynchronize 메타 데이터를 사용할지 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-150">In **Synchronize cloud metadata**, select whether you want toosynchronize metadata for all clouds on hello VMM server with hello vault.</span></span> <span data-ttu-id="ce9e2-151">이 작업은 toohappen 각 서버에서 한 번만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-151">This action only needs toohappen once on each server.</span></span> <span data-ttu-id="ce9e2-152">Toosynchronize 모든 클라우드를 않으려는 경우에이 설정을 선택 되지 않은 상태로 두고 수 있으며 hello VMM 콘솔에서 hello 클라우드 속성에서 개별적으로 각 클라우드를 동기화 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-152">If you don't want toosynchronize all clouds, you can leave this setting unchecked, and synchronize each cloud individually in hello cloud properties in hello VMM console.</span></span>
12. <span data-ttu-id="ce9e2-153">클릭 **다음** toocomplete hello 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-153">Click **Next** toocomplete hello process.</span></span> <span data-ttu-id="ce9e2-154">등록 후 hello VMM 서버에서 메타 데이터를 Azure Site Recovery에서 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-154">After registration, metadata from hello VMM server is retrieved by Azure Site Recovery.</span></span> <span data-ttu-id="ce9e2-155">hello 서버 hello에 표시 된 **VMM 서버** hello에 탭 **서버** hello 자격 증명 모음에 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-155">hello server is displayed on hello **VMM Servers** tab on hello **Servers** page in hello vault.</span></span>

    ![서버](./media/vmm-to-vmm-walkthrough-source-target/provider13.png)
13. <span data-ttu-id="ce9e2-157">Hello 서버 hello Site Recovery 콘솔에서 사용할 수 있게 되에서 **소스** > **준비 소스** hello VMM 서버 및 선택 hello 클라우드에 hello Hyper-v 호스트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-157">After hello server is available in hello Site Recovery console, in **Source** > **Prepare source** select hello VMM server, and select hello cloud in which hello Hyper-V host is located.</span></span> <span data-ttu-id="ce9e2-158">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-158">Then click **OK**.</span></span>

<span data-ttu-id="ce9e2-159">Hello 명령줄에서 hello 공급자를 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-159">You can also install hello provider from hello command line:</span></span>

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="ce9e2-160">Hello 대상 환경 설정</span><span class="sxs-lookup"><span data-stu-id="ce9e2-160">Set up hello target environment</span></span>

<span data-ttu-id="ce9e2-161">Hello 대상 VMM 서버와 클라우드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-161">Select hello target VMM server and cloud:</span></span>

1. <span data-ttu-id="ce9e2-162">클릭 **준비 인프라** > **대상**, 선택한 toouse 원하는 선택 hello 대상 VMM 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-162">Click **Prepare infrastructure** > **Target**, and select hello target VMM server you want toouse.</span></span>
2. <span data-ttu-id="ce9e2-163">Site Recovery와 동기화 된 hello 서버에 클라우드가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-163">Clouds on hello server that are synchronized with Site Recovery will be displayed.</span></span> <span data-ttu-id="ce9e2-164">Hello 대상 클라우드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-164">Select hello target cloud.</span></span>

   ![대상](./media/vmm-to-vmm-walkthrough-source-target/target-vmm.png)



## <a name="next-steps"></a><span data-ttu-id="ce9e2-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ce9e2-166">Next steps</span></span>

<span data-ttu-id="ce9e2-167">너무 이동[7 단계: 네트워크 매핑을 구성](vmm-to-vmm-walkthrough-network-mapping.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ce9e2-167">Go too[Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>
