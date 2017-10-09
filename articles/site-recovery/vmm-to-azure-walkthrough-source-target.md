---
title: "hello 소스 및 대상 Hyper-v 복제 tooAzure (System Center VMM)을 사용한 Azure Site recovery에 대 한를 aaaSet | Microsoft Docs"
description: "Azure Site Recovery를 사용 하 여 VMM 클라우드에 tooAzure 저장소에서 Hyper-v Vm의 복제에 대 한 원본 및 대상 설정을 hello 단계 tooset을 요약 되어 있습니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5edb6d87-25a5-40fe-b6f1-ddf7b55a6b31
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/25/2017
ms.author: raynew
ms.openlocfilehash: 3f8c5386cb64527c775aef636980bac098ee9905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-with-vmm-replication-tooazure"></a><span data-ttu-id="e1345-103">8 단계: hello 소스 및 대상 (VMM)와 Hyper-v 복제 tooAzure에 대 한 설정</span><span class="sxs-lookup"><span data-stu-id="e1345-103">Step 8: Set up hello source and target for Hyper-V (with VMM) replication tooAzure</span></span>

<span data-ttu-id="e1345-104">후 [자격 증명 모음 만들기](vmm-to-azure-walkthrough-create-vault.md) 지정 하는 tooreplicate,이 문서 tooconfigure 원본을 사용 하 고 System Center Virtual Machine Manager (VMM)의 온-프레미스 Hyper-v 가상 컴퓨터를 복제할 때 대상으로 설정 하 고 hello를 사용 하 여 클라우드 tooAzure, [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-104">After [creating a vault](vmm-to-azure-walkthrough-create-vault.md) and specifying what you want tooreplicate, use this article tooconfigure source and target settings when replicating on-premises Hyper-V virtual machines in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="e1345-105">Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="e1345-106">Hello 소스 환경 설정</span><span class="sxs-lookup"><span data-stu-id="e1345-106">Set up hello source environment</span></span>

<span data-ttu-id="e1345-107">S1.</span><span class="sxs-lookup"><span data-stu-id="e1345-107">S1.</span></span> <span data-ttu-id="e1345-108">**인프라 준비** > **원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-108">Click **Prepare Infrastructure** > **Source**.</span></span>

    ![Set up source](./media/vmm-to-azure-walkthrough-source-target/set-source1.png)

2. <span data-ttu-id="e1345-109">**준비 소스**, 클릭 **+ VMM** tooadd VMM 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-109">In **Prepare source**, click **+ VMM** tooadd a VMM server.</span></span>

    ![원본 설정](./media/vmm-to-azure-walkthrough-source-target/set-source2.png)

3. <span data-ttu-id="e1345-111">**서버 추가**, 있는지 여부를 확인 **System Center VMM 서버** 에 표시 **서버 유형** 해당 hello VMM 서버 hello 충족 [필수 구성 요소 및 URL 요구 사항](#prerequisites)합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-111">In **Add Server**, check that **System Center VMM server** appears in **Server type** and that hello VMM server meets hello [prerequisites and URL requirements](#prerequisites).</span></span>
4. <span data-ttu-id="e1345-112">Hello Azure Site Recovery Provider 설치 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-112">Download hello Azure Site Recovery Provider installation file.</span></span>
5. <span data-ttu-id="e1345-113">Hello 등록 키를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-113">Download hello registration key.</span></span> <span data-ttu-id="e1345-114">설정을 실행할 때 이 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-114">You need this when you run setup.</span></span> <span data-ttu-id="e1345-115">hello 키가 생성 한 후 5 일 동안 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-115">hello key is valid for five days after you generate it.</span></span>

    ![원본 설정](./media/vmm-to-azure-walkthrough-source-target/set-source3.png)

## <a name="install-hello-provider-on-hello-vmm-server"></a><span data-ttu-id="e1345-117">Hello VMM 서버에 hello 공급자를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-117">Install hello Provider on hello VMM server</span></span>

1. <span data-ttu-id="e1345-118">VMM 서버 hello에 hello 공급자 설정 파일을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-118">Run hello Provider setup file on hello VMM server.</span></span>
2. <span data-ttu-id="e1345-119">Microsoft Update 정책에 따라 공급자 업데이트가 설치되도록 **Microsoft Update**에서 업데이트를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-119">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="e1345-120">**설치**, 수락 하거나 hello 기본 공급자 설치 위치를 수정 하 고 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-120">In **Installation**, accept or modify hello default Provider installation location and click **Install**.</span></span>

    ![설치 위치](./media/vmm-to-azure-walkthrough-source-target/provider2.png)
4. <span data-ttu-id="e1345-122">설치가 완료 되 면 클릭 **등록** hello 자격 증명 모음에 tooregister hello VMM 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-122">When installation finishes, click **Register** tooregister hello VMM server in hello vault.</span></span>
5. <span data-ttu-id="e1345-123">Hello에 **자격 증명 모음 설정을** 페이지 **찾아보기** tooselect hello 자격 증명 모음 키 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-123">In hello **Vault Settings** page, click **Browse** tooselect hello vault key file.</span></span> <span data-ttu-id="e1345-124">Hello Azure Site Recovery 구독 및 hello 자격 증명 모음 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-124">Specify hello Azure Site Recovery subscription and hello vault name.</span></span>

    ![서버 등록](./media/vmm-to-azure-walkthrough-source-target/provider10.png)
6. <span data-ttu-id="e1345-126">**인터넷 연결**, hello VMM 서버에서 실행 중인 공급자는 tooSite 복구를 통해 연결 하는 hello 인터넷 hello 하는 방법을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-126">In **Internet Connection**, specify how hello Provider running on hello VMM server will connect tooSite Recovery over hello internet.</span></span>

   * <span data-ttu-id="e1345-127">Hello 공급자 tooconnect을 직접 하려는 경우 선택 **tooAzure Site Recovery 프록시 없이 직접 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-127">If you want hello Provider tooconnect directly, select **Connect directly tooAzure Site Recovery without a proxy**.</span></span>
   * <span data-ttu-id="e1345-128">기존 프록시 인증 필요 또는 사용자 지정 프록시 toouse 하려는 경우 선택 **연결에서 프록시 서버를 사용 하 여 사이트 복구 tooAzure**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-128">If your existing proxy requires authentication, or you want toouse a custom proxy, select **Connect tooAzure Site Recovery using a proxy server**.</span></span>
   * <span data-ttu-id="e1345-129">사용자 지정 프록시를 사용 하는 경우 hello 주소, 포트 및 자격 증명을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-129">If you use a custom proxy, specify hello address, port, and credentials.</span></span>
   * <span data-ttu-id="e1345-130">프록시를 사용 하는 경우 해야 이미 허용한에 설명 된 hello Url [필수 구성 요소](#on-premises-prerequisites)합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-130">If you're using a proxy, you should have already allowed hello URLs described in [prerequisites](#on-premises-prerequisites).</span></span>
   * <span data-ttu-id="e1345-131">자동으로 지정 하는 hello를 사용 하 여 VMM RunAs 계정 (DRAProxyAccount) 만들어집니다는 사용자 지정 프록시를 사용 하는 경우 프록시 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-131">If you use a custom proxy, a VMM RunAs account (DRAProxyAccount) will be created automatically using hello specified proxy credentials.</span></span> <span data-ttu-id="e1345-132">이 계정을 올바르게 인증할 수 있도록 hello 프록시 서버를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-132">Configure hello proxy server so that this account can authenticate successfully.</span></span> <span data-ttu-id="e1345-133">VMM RunAs 계정 설정은 hello hello VMM 콘솔에서 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-133">hello VMM RunAs account settings can be modified in hello VMM console.</span></span> <span data-ttu-id="e1345-134">**설정**를 확장 하 고 **보안** > **실행 계정**, 한 다음 DRAProxyAccount에 대 한 hello 암호를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-134">In **Settings**, expand **Security** > **Run As Accounts**, and then modify hello password for DRAProxyAccount.</span></span> <span data-ttu-id="e1345-135">이 설정은 적용 됩니다에 toorestart hello VMM 서비스를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-135">You’ll need toorestart hello VMM service so that this setting takes effect.</span></span>

     ![인터넷](./media/vmm-to-azure-walkthrough-source-target/provider13.png)
7. <span data-ttu-id="e1345-137">적용 하거나 데이터 암호화에 자동으로 생성 된 SSL 인증서의 hello 위치를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-137">Accept or modify hello location of an SSL certificate that’s automatically generated for data encryption.</span></span> <span data-ttu-id="e1345-138">이 인증서는 hello Azure Site Recovery 포털에서 Azure에 의해 보호 되는 클라우드에 대 한 데이터 암호화를 사용 하는 경우에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-138">This certificate is used if you enable data encryption for a cloud protected by Azure in hello Azure Site Recovery portal.</span></span> <span data-ttu-id="e1345-139">안전하게 보관해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-139">Keep this certificate safe.</span></span> <span data-ttu-id="e1345-140">장애 조치 tooAzure를 실행 하는 경우 해야 toodecrypt, 데이터 암호화를 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="e1345-140">When you run a failover tooAzure you’ll need it toodecrypt, if data encryption is enabled.</span></span>
8. <span data-ttu-id="e1345-141">**서버 이름**, hello 자격 증명 모음에 친숙 한 이름 tooidentify hello VMM 서버를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-141">In **Server name**, specify a friendly name tooidentify hello VMM server in hello vault.</span></span> <span data-ttu-id="e1345-142">클러스터 구성에서 hello VMM 클러스터 역할 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-142">In a cluster configuration, specify hello VMM cluster role name.</span></span>
9. <span data-ttu-id="e1345-143">사용 하도록 설정 **클라우드 메타 데이터 동기화**hello 자격 증명 모음과 hello VMM 서버의 모든 클라우드에 대 한 toosynchronize 메타 데이터를 사용 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="e1345-143">Enable **Sync cloud metadata**, if you want toosynchronize metadata for all clouds on hello VMM server with hello vault.</span></span> <span data-ttu-id="e1345-144">이 작업은 toohappen 각 서버에서 한 번만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-144">This action only needs toohappen once on each server.</span></span> <span data-ttu-id="e1345-145">Toosynchronize 모든 클라우드를 않으려는 경우에이 설정을 선택 되지 않은 상태로 두고 수 있으며 hello VMM 콘솔에서 hello 클라우드 속성에서 개별적으로 각 클라우드를 동기화 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-145">If you don't want toosynchronize all clouds, you can leave this setting unchecked and synchronize each cloud individually in hello cloud properties in hello VMM console.</span></span> <span data-ttu-id="e1345-146">클릭 **등록** toocomplete hello 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-146">Click **Register** toocomplete hello process.</span></span>

    ![서버 등록](./media/vmm-to-azure-walkthrough-source-target/provider16.png)
10. <span data-ttu-id="e1345-148">등록이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-148">Registration starts.</span></span> <span data-ttu-id="e1345-149">등록 완료 되 면 hello 서버에 표시 됩니다 **사이트 복구 인프라** > **VMM 서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-149">After registration finishes, hello server is displayed in **Site Recovery Infrastructure** > **VMM Servers**.</span></span>


## <a name="install-hello-azure-recovery-services-agent-on-hyper-v-hosts"></a><span data-ttu-id="e1345-150">Hyper-v 호스트에 hello Azure 복구 서비스 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-150">Install hello Azure Recovery Services agent on Hyper-V hosts</span></span>

1. <span data-ttu-id="e1345-151">Hello 공급자를 설정한 후 hello Azure 복구 서비스 에이전트에 대 한 toodownload hello 설치 파일이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-151">After you've set up hello Provider, you need toodownload hello installation file for hello Azure Recovery Services agent.</span></span> <span data-ttu-id="e1345-152">Hello VMM 클라우드의 각 Hyper-v 서버에서 설치 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-152">Run setup on each Hyper-V server in hello VMM cloud.</span></span>

    ![Hyper-V 사이트](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent1.png)
2. <span data-ttu-id="e1345-154">**필수 구성 요소 확인**에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-154">In **Prerequisites Check**, click **Next**.</span></span> <span data-ttu-id="e1345-155">누락된 필수 구성 요소는 자동으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-155">Any missing prerequisites will be automatically installed.</span></span>

    ![필수 구성 요소 복구 서비스 에이전트](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent2.png)
3. <span data-ttu-id="e1345-157">**설치 설정**그대로 사용 하거나 hello 설치 위치 및 hello 캐시 위치를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-157">In **Installation Settings**, accept or modify hello installation location, and hello cache location.</span></span> <span data-ttu-id="e1345-158">5GB 이상의 사용 가능한 저장소에 있는 드라이브에 hello 캐시를 구성할 수 있지만 600 g B 이상의 여유 공간이 있는 드라이브에 캐시 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-158">You can configure hello cache on a drive that has at least 5 GB of storage available but we recommend a cache drive with 600 GB or more of free space.</span></span> <span data-ttu-id="e1345-159">**설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-159">Then click **Install**.</span></span>
4. <span data-ttu-id="e1345-160">설치가 완료 되 면 클릭 **닫기** toofinish 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-160">After installation is complete, click **Close** toofinish.</span></span>

    ![MARS 에이전트 등록](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent3.png)

### <a name="command-line-installation"></a><span data-ttu-id="e1345-162">명령줄 설치</span><span class="sxs-lookup"><span data-stu-id="e1345-162">Command line installation</span></span>
<span data-ttu-id="e1345-163">다음 명령을 hello를 사용 하 여 명령줄에서 hello Microsoft Azure 복구 서비스 에이전트를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-163">You can install hello Microsoft Azure Recovery Services Agent from command line using hello following command:</span></span>

     marsagentinstaller.exe /q /nu

### <a name="set-up-internet-proxy-access-toosite-recovery-from-hyper-v-hosts"></a><span data-ttu-id="e1345-164">인터넷 프록시 액세스 tooSite Hyper-v 호스트에서 복구를 설정</span><span class="sxs-lookup"><span data-stu-id="e1345-164">Set up internet proxy access tooSite Recovery from Hyper-V hosts</span></span>

<span data-ttu-id="e1345-165">hello 복구 서비스 에이전트가 Hyper-v 호스트에서 실행 되는 VM 복제에 대 한 인터넷 액세스 tooAzure 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-165">hello Recovery Services agent running on Hyper-V hosts needs internet access tooAzure for VM replication.</span></span> <span data-ttu-id="e1345-166">에 액세스할 때는 hello 인터넷 프록시를 통해이 다음과 같이 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-166">If you're accessing hello internet through a proxy, set it up as follows:</span></span>

1. <span data-ttu-id="e1345-167">Hello Microsoft Azure 백업 MMC 스냅인에 hello Hyper-v 호스트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-167">Open hello Microsoft Azure Backup MMC snap-in on hello Hyper-V host.</span></span> <span data-ttu-id="e1345-168">기본적으로 Microsoft Azure 백업에 대 한 바로 가기는 C:\Program Files\Microsoft Azure 복구 서비스 Agent\bin\wabadmin 또는 hello 바탕 화면에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-168">By default, a shortcut for Microsoft Azure Backup is available on hello desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="e1345-169">Hello 스냅인에서 클릭 **속성 변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-169">In hello snap-in, click **Change Properties**.</span></span>
3. <span data-ttu-id="e1345-170">Hello에 **프록시 구성을** 탭에서 프록시 서버 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-170">On hello **Proxy Configuration** tab, specify proxy server information.</span></span>

    ![MARS 에이전트 등록](./media/vmm-to-azure-walkthrough-source-target/mars-proxy.png)
4. <span data-ttu-id="e1345-172">해당 hello 에이전트 hello에 설명 된 hello Url에 도달할 수 확인 [필수 구성 요소](#on-premises-prerequisites)합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-172">Check that hello agent can reach hello URLs described in hello [prerequisites](#on-premises-prerequisites).</span></span>

## <a name="set-up-hello-target-environment"></a><span data-ttu-id="e1345-173">Hello 대상 환경 설정</span><span class="sxs-lookup"><span data-stu-id="e1345-173">Set up hello target environment</span></span>
<span data-ttu-id="e1345-174">복제에 사용 되는 hello Azure 저장소 계정 toobe를 지정 하 고 hello Azure 네트워크 toowhich Azure Vm 장애 조치 후 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-174">Specify hello Azure storage account toobe used for replication, and hello Azure network toowhich Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="e1345-175">클릭 **준비 인프라** > **대상**hello toocreate hello 장애 조치 가상 컴퓨터를 원하는 리소스 그룹을 hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-175">Click **Prepare infrastructure** > **Target**, select hello subscription and hello resource group where you want toocreate hello failed over virtual machines.</span></span> <span data-ttu-id="e1345-176">Toouse (기본 또는 리소스 관리) Azure에서 가상 컴퓨터를 조치할 hello에 대 한 원하는 hello 배포 모델을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-176">Choose hello deployment model that you want toouse in Azure (classic or resource management) for hello failed over virtual machines.</span></span>

    ![저장소](./media/vmm-to-azure-walkthrough-source-target/enablerep3.png)

2. <span data-ttu-id="e1345-178">Site Recovery가 호환되는 Azure 저장소 계정 및 네트워크가 하나 이상 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-178">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    ![저장소](./media/vmm-to-azure-walkthrough-source-target/compatible-storage.png)

3. <span data-ttu-id="e1345-180">저장소 계정을 만들지 않은 toocreate 하나 하려는 경우 리소스 관리자를 사용 하 여 클릭 **저장소 계정 추가** toodo 인라인 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-180">If you haven't created a storage account, and you want toocreate one using Resource Manager, click **+Storage account** toodo that inline.</span></span>  <span data-ttu-id="e1345-181">Hello에 **저장소 계정 만들기** 블레이드 계정 이름, 유형, 구독 및 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-181">On hello **Create storage account** blade specify an account name, type, subscription, and location.</span></span> <span data-ttu-id="e1345-182">hello 계정 hello에 있어야 합니다. hello와 동일한 위치 복구 서비스 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-182">hello account should be in hello same location as hello Recovery Services vault.</span></span>

   ![저장소](./media/vmm-to-azure-walkthrough-source-target/gs-createstorage.png)


   * <span data-ttu-id="e1345-184">Hello 일반 모델을 사용 하 여 저장소 계정을 toocreate을 원하는 경우 hello Azure 포털에서에서 수행할.</span><span class="sxs-lookup"><span data-stu-id="e1345-184">If you want toocreate a storage account using hello classic model, do that in hello Azure portal.</span></span> [<span data-ttu-id="e1345-185">자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="e1345-185">Learn more</span></span>](../storage/common/storage-create-storage-account.md)
   * <span data-ttu-id="e1345-186">프리미엄 저장소 계정 복제 된 데이터를 사용 하는 경우 추가 표준 저장소 계정을 설정, toostore 복제 로그를 가져갈 변화 들이 tooon 온-프레미스 데이터를 캡처하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-186">If you’re using a premium storage account for replicated data, set up an additional standard storage account, toostore replication logs that capture ongoing changes tooon-premises data.</span></span>
5. <span data-ttu-id="e1345-187">Azure 네트워크를 만들지 않은 toocreate 하나 하려는 경우 리소스 관리자를 사용 하 여 클릭 **+ 네트워크** toodo 인라인 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-187">If you haven't created an Azure network, and you want toocreate one using Resource Manager, click **+Network** toodo that inline.</span></span> <span data-ttu-id="e1345-188">Hello에 **가상 네트워크 만들기** 블레이드 네트워크 이름, 주소 범위, 서브넷 정보, 구독 및 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-188">On hello **Create virtual network** blade specify a network name, address range, subnet details, subscription, and location.</span></span> <span data-ttu-id="e1345-189">hello 네트워크 hello에 있어야 hello와 동일한 위치 복구 서비스 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="e1345-189">hello network should be in hello same location as hello Recovery Services vault.</span></span>

   ![네트워크](./media/vmm-to-azure-walkthrough-source-target/gs-createnetwork.png)

   <span data-ttu-id="e1345-191">Hello 일반 모델을 사용 하는 네트워크 toocreate을 원하는 경우 hello Azure 포털에서에서 수행할.</span><span class="sxs-lookup"><span data-stu-id="e1345-191">If you want toocreate a network using hello classic model, do that in hello Azure portal.</span></span> <span data-ttu-id="e1345-192">[자세히 알아봅니다](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="e1345-192">[Learn more](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span></span>





## <a name="next-steps"></a><span data-ttu-id="e1345-193">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e1345-193">Next steps</span></span>

<span data-ttu-id="e1345-194">너무 이동[9 단계: 네트워크 매핑 구성](vmm-to-azure-walkthrough-network-mapping.md)</span><span class="sxs-lookup"><span data-stu-id="e1345-194">Go too[Step 9: Configure network mapping](vmm-to-azure-walkthrough-network-mapping.md)</span></span>
