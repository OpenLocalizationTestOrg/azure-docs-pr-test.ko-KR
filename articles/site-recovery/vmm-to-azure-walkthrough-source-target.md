---
title: "Azure Site Recovery를 사용하여 Azure로의 Hyper-V(System Center VMM 포함) 복제를 위한 원본 및 대상 설정 | Microsoft 문서"
description: "Azure Site Recovery를 사용하여 VMM 클라우드의 Hyper-V VM을 Azure Storage로 복제하기 위한 원본 및 대상 설정을 지정하는 단계를 요약하여 설명합니다."
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
ms.openlocfilehash: c72f839d0a1288dccb7deb3e44fc2b20d64818f0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="step-8-set-up-the-source-and-target-for-hyper-v-with-vmm-replication-to-azure"></a><span data-ttu-id="189eb-103">8단계: Azure로의 Hyper-V(VMM 포함) 복제를 위한 원본 및 대상 설정</span><span class="sxs-lookup"><span data-stu-id="189eb-103">Step 8: Set up the source and target for Hyper-V (with VMM) replication to Azure</span></span>

<span data-ttu-id="189eb-104">[자격 증명 모음 만들기](vmm-to-azure-walkthrough-create-vault.md)와 복제할 항목 지정을 수행한 후 이 문서의 내용을 참조하여 Azure Portal에서 [Azure Site Recovery](site-recovery-overview.md) 서비스를 사용해 System Center Virtual Machine Manager(VMM) 클라우드의 온-프레미스 Hyper-V 가상 컴퓨터를 Azure로 복제할 때 사용할 원본 및 대상 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-104">After [creating a vault](vmm-to-azure-walkthrough-create-vault.md) and specifying what you want to replicate, use this article to configure source and target settings when replicating on-premises Hyper-V virtual machines in System Center Virtual Machine Manager (VMM) clouds to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="189eb-105">이 문서의 하단 또는 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 의견이나 질문을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-the-source-environment"></a><span data-ttu-id="189eb-106">원본 환경 설정</span><span class="sxs-lookup"><span data-stu-id="189eb-106">Set up the source environment</span></span>

<span data-ttu-id="189eb-107">S1.</span><span class="sxs-lookup"><span data-stu-id="189eb-107">S1.</span></span> <span data-ttu-id="189eb-108">**인프라 준비** > **원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-108">Click **Prepare Infrastructure** > **Source**.</span></span>

    ![Set up source](./media/vmm-to-azure-walkthrough-source-target/set-source1.png)

2. <span data-ttu-id="189eb-109">**소스 준비**에서 **+VMM**을 클릭하여 VMM 서버를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-109">In **Prepare source**, click **+ VMM** to add a VMM server.</span></span>

    ![원본 설정](./media/vmm-to-azure-walkthrough-source-target/set-source2.png)

3. <span data-ttu-id="189eb-111">**서버 추가**에서 **System Center VMM 서버**가 **서버 형식**에 표시되고 해당 VMM 서버가 [필수 조건 및 URL 요구 사항](#prerequisites)을 만족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-111">In **Add Server**, check that **System Center VMM server** appears in **Server type** and that the VMM server meets the [prerequisites and URL requirements](#prerequisites).</span></span>
4. <span data-ttu-id="189eb-112">Azure Site Recovery 공급자 설치 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-112">Download the Azure Site Recovery Provider installation file.</span></span>
5. <span data-ttu-id="189eb-113">등록 키를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-113">Download the registration key.</span></span> <span data-ttu-id="189eb-114">설정을 실행할 때 이 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-114">You need this when you run setup.</span></span> <span data-ttu-id="189eb-115">이 키는 생성된 날로부터 5일간 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-115">The key is valid for five days after you generate it.</span></span>

    ![원본 설정](./media/vmm-to-azure-walkthrough-source-target/set-source3.png)

## <a name="install-the-provider-on-the-vmm-server"></a><span data-ttu-id="189eb-117">VMM 서버에 공급자 설치</span><span class="sxs-lookup"><span data-stu-id="189eb-117">Install the Provider on the VMM server</span></span>

1. <span data-ttu-id="189eb-118">VMM 서버에서 공급자 설치 파일을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-118">Run the Provider setup file on the VMM server.</span></span>
2. <span data-ttu-id="189eb-119">Microsoft Update 정책에 따라 공급자 업데이트가 설치되도록 **Microsoft Update**에서 업데이트를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-119">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="189eb-120">**설치**에서 기본 공급자 설치 위치를 수락하거나 수정하고 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-120">In **Installation**, accept or modify the default Provider installation location and click **Install**.</span></span>

    ![설치 위치](./media/vmm-to-azure-walkthrough-source-target/provider2.png)
4. <span data-ttu-id="189eb-122">설치가 완료되면 **등록**을 클릭하여 자격 증명 모음에 VMM 서버를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-122">When installation finishes, click **Register** to register the VMM server in the vault.</span></span>
5. <span data-ttu-id="189eb-123">**자격 증명 모음 설정** 페이지에서 **찾아보기**를 클릭하고 자격 증명 모음 키 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-123">In the **Vault Settings** page, click **Browse** to select the vault key file.</span></span> <span data-ttu-id="189eb-124">Azure Site Recovery 구독 및 자격 증명 모음 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-124">Specify the Azure Site Recovery subscription and the vault name.</span></span>

    ![서버 등록](./media/vmm-to-azure-walkthrough-source-target/provider10.png)
6. <span data-ttu-id="189eb-126">VMM 서버에서 실행 중인 공급자가 인터넷을 통해 Site Recovery에 연결하는 방법을 **인터넷 연결**에서 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-126">In **Internet Connection**, specify how the Provider running on the VMM server will connect to Site Recovery over the internet.</span></span>

   * <span data-ttu-id="189eb-127">공급자를 직접 연결하려면 **프록시 없이 Azure Site Recovery에 직접 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-127">If you want the Provider to connect directly, select **Connect directly to Azure Site Recovery without a proxy**.</span></span>
   * <span data-ttu-id="189eb-128">기존 프록시에 인증이 필요하거나 사용자 지정 프록시를 사용하려면 **프록시 서버를 사용하여 Azure Site Recovery에 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-128">If your existing proxy requires authentication, or you want to use a custom proxy, select **Connect to Azure Site Recovery using a proxy server**.</span></span>
   * <span data-ttu-id="189eb-129">사용자 지정 프록시를 사용하는 경우 주소, 포트 및 자격 증명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-129">If you use a custom proxy, specify the address, port, and credentials.</span></span>
   * <span data-ttu-id="189eb-130">프록시를 사용하는 경우 [필수 조건](#on-premises-prerequisites)에 설명된 URL을 이미 허용했어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-130">If you're using a proxy, you should have already allowed the URLs described in [prerequisites](#on-premises-prerequisites).</span></span>
   * <span data-ttu-id="189eb-131">사용자 지정 프록시를 사용하는 경우 지정된 프록시 자격 증명을 사용하여 VMM 실행 계정(DRAProxyAccount)이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-131">If you use a custom proxy, a VMM RunAs account (DRAProxyAccount) will be created automatically using the specified proxy credentials.</span></span> <span data-ttu-id="189eb-132">이 계정이 성공적으로 인증될 수 있도록 프록시 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-132">Configure the proxy server so that this account can authenticate successfully.</span></span> <span data-ttu-id="189eb-133">VMM 콘솔에서 VMM 실행 계정 설정을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-133">The VMM RunAs account settings can be modified in the VMM console.</span></span> <span data-ttu-id="189eb-134">**설정**에서 **보안** > **실행 계정**을 차례로 확장한 다음 DRAProxyAccount의 암호를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-134">In **Settings**, expand **Security** > **Run As Accounts**, and then modify the password for DRAProxyAccount.</span></span> <span data-ttu-id="189eb-135">이 설정이 적용되도록 VMM 서비스를 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-135">You’ll need to restart the VMM service so that this setting takes effect.</span></span>

     ![인터넷](./media/vmm-to-azure-walkthrough-source-target/provider13.png)
7. <span data-ttu-id="189eb-137">데이터 암호화를 위해 자동으로 생성되는 SSL 인증서를 저장할 위치를 수락하거나 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-137">Accept or modify the location of an SSL certificate that’s automatically generated for data encryption.</span></span> <span data-ttu-id="189eb-138">이 인증서는 Azure Site Recovery 포털에서 Azure가 보호하는 클라우드에 대해 데이터 암호화를 사용하도록 설정하는 경우 사용되므로</span><span class="sxs-lookup"><span data-stu-id="189eb-138">This certificate is used if you enable data encryption for a cloud protected by Azure in the Azure Site Recovery portal.</span></span> <span data-ttu-id="189eb-139">안전하게 보관해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-139">Keep this certificate safe.</span></span> <span data-ttu-id="189eb-140">데이터 암호화가 활성화된 경우 Azure에 장애 조치(failover)를 실행할 때 암호 해독에 이 인증서가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-140">When you run a failover to Azure you’ll need it to decrypt, if data encryption is enabled.</span></span>
8. <span data-ttu-id="189eb-141">자격 증명 모음에서 VMM 서버를 식별하기 위한 이름을 **서버 이름**에서 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-141">In **Server name**, specify a friendly name to identify the VMM server in the vault.</span></span> <span data-ttu-id="189eb-142">클러스터 구성에서 VMM 클러스터 역할 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-142">In a cluster configuration, specify the VMM cluster role name.</span></span>
9. <span data-ttu-id="189eb-143">VMM 서버에 있는 모든 클라우드의 메타데이터를 자격 증명 모음과 동기화하려면 **클라우드 메타데이터 동기화**를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-143">Enable **Sync cloud metadata**, if you want to synchronize metadata for all clouds on the VMM server with the vault.</span></span> <span data-ttu-id="189eb-144">이 작업은 각 서버에서 한 번만 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-144">This action only needs to happen once on each server.</span></span> <span data-ttu-id="189eb-145">모든 클라우드를 동기화하지 않는 경우 이 설정을 선택 취소된 상태로 두고 VMM 콘솔의 클라우드 속성에서 각 클라우드를 개별적으로 동기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-145">If you don't want to synchronize all clouds, you can leave this setting unchecked and synchronize each cloud individually in the cloud properties in the VMM console.</span></span> <span data-ttu-id="189eb-146">**등록**을 클릭하여 프로세스를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-146">Click **Register** to complete the process.</span></span>

    ![서버 등록](./media/vmm-to-azure-walkthrough-source-target/provider16.png)
10. <span data-ttu-id="189eb-148">등록이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-148">Registration starts.</span></span> <span data-ttu-id="189eb-149">등록이 완료되면 **Site Recovery 인프라** > **VMM 서버**에 해당 서버가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-149">After registration finishes, the server is displayed in **Site Recovery Infrastructure** > **VMM Servers**.</span></span>


## <a name="install-the-azure-recovery-services-agent-on-hyper-v-hosts"></a><span data-ttu-id="189eb-150">Hyper-V 호스트에 Azure 복구 서비스 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="189eb-150">Install the Azure Recovery Services agent on Hyper-V hosts</span></span>

1. <span data-ttu-id="189eb-151">공급자를 설치한 후에는 Azure 복구 서비스 에이전트 설치 파일을 다운로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-151">After you've set up the Provider, you need to download the installation file for the Azure Recovery Services agent.</span></span> <span data-ttu-id="189eb-152">VMM 클라우드의 각 Hyper-V 서버에서 설치 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-152">Run setup on each Hyper-V server in the VMM cloud.</span></span>

    ![Hyper-V 사이트](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent1.png)
2. <span data-ttu-id="189eb-154">**필수 구성 요소 확인**에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-154">In **Prerequisites Check**, click **Next**.</span></span> <span data-ttu-id="189eb-155">누락된 필수 구성 요소는 자동으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-155">Any missing prerequisites will be automatically installed.</span></span>

    ![필수 구성 요소 복구 서비스 에이전트](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent2.png)
3. <span data-ttu-id="189eb-157">**설치 설정**에서 설치 위치 및 캐시 위치를 수락하거나 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-157">In **Installation Settings**, accept or modify the installation location, and the cache location.</span></span> <span data-ttu-id="189eb-158">최소 5GB의 저장 공간이 있는 드라이브에 캐시를 구성할 수 있지만 600GB 이상의 여유 공간이 있는 캐시 드라이브에 구성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-158">You can configure the cache on a drive that has at least 5 GB of storage available but we recommend a cache drive with 600 GB or more of free space.</span></span> <span data-ttu-id="189eb-159">**설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-159">Then click **Install**.</span></span>
4. <span data-ttu-id="189eb-160">설치가 완료되면 **닫기** 를 클릭하여 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-160">After installation is complete, click **Close** to finish.</span></span>

    ![MARS 에이전트 등록](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent3.png)

### <a name="command-line-installation"></a><span data-ttu-id="189eb-162">명령줄 설치</span><span class="sxs-lookup"><span data-stu-id="189eb-162">Command line installation</span></span>
<span data-ttu-id="189eb-163">다음 명령을 사용하여 명령줄에서 Microsoft Azure 복구 서비스 에이전트를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-163">You can install the Microsoft Azure Recovery Services Agent from command line using the following command:</span></span>

     marsagentinstaller.exe /q /nu

### <a name="set-up-internet-proxy-access-to-site-recovery-from-hyper-v-hosts"></a><span data-ttu-id="189eb-164">Hyper-V 호스트에서 Site Recovery에 대한 인터넷 프록시 액세스를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-164">Set up internet proxy access to Site Recovery from Hyper-V hosts</span></span>

<span data-ttu-id="189eb-165">VM을 복제하려면 Hyper-V 호스트에서 실행되는 복구 서비스 에이전트가 인터넷을 통해 Azure에 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-165">The Recovery Services agent running on Hyper-V hosts needs internet access to Azure for VM replication.</span></span> <span data-ttu-id="189eb-166">프록시를 통해 인터넷에 액세스하는 경우 다음과 같이 프록시를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-166">If you're accessing the internet through a proxy, set it up as follows:</span></span>

1. <span data-ttu-id="189eb-167">Hyper-V 호스트에서 Microsoft Azure 백업 MMC 스냅인을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-167">Open the Microsoft Azure Backup MMC snap-in on the Hyper-V host.</span></span> <span data-ttu-id="189eb-168">기본적으로 Microsoft Azure Backup에 대한 바로 가기가 바탕 화면 또는 C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-168">By default, a shortcut for Microsoft Azure Backup is available on the desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="189eb-169">스냅인에서 **속성 변경**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-169">In the snap-in, click **Change Properties**.</span></span>
3. <span data-ttu-id="189eb-170">**프록시 구성** 탭에서 프록시 서버 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-170">On the **Proxy Configuration** tab, specify proxy server information.</span></span>

    ![MARS 에이전트 등록](./media/vmm-to-azure-walkthrough-source-target/mars-proxy.png)
4. <span data-ttu-id="189eb-172">에이전트가 [필수 조건](#on-premises-prerequisites)에 설명된 URL에 연결할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-172">Check that the agent can reach the URLs described in the [prerequisites](#on-premises-prerequisites).</span></span>

## <a name="set-up-the-target-environment"></a><span data-ttu-id="189eb-173">대상 환경 설정</span><span class="sxs-lookup"><span data-stu-id="189eb-173">Set up the target environment</span></span>
<span data-ttu-id="189eb-174">복제에 사용될 Azure 저장소 계정과 장애 조치(failover) 후 Azure VM이 연결될 Azure 네트워크를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-174">Specify the Azure storage account to be used for replication, and the Azure network to which Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="189eb-175">**인프라 준비** > **대상**을 클릭하고 장애 조치 가상 컴퓨터를 만들려는 구독 및 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-175">Click **Prepare infrastructure** > **Target**, select the subscription and the resource group where you want to create the failed over virtual machines.</span></span> <span data-ttu-id="189eb-176">장애 조치 가상 컴퓨터에 대해 Azure(클래식 또는 리소스 관리)에서 사용하려는 배포 모델을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-176">Choose the deployment model that you want to use in Azure (classic or resource management) for the failed over virtual machines.</span></span>

    ![창고](./media/vmm-to-azure-walkthrough-source-target/enablerep3.png)

2. <span data-ttu-id="189eb-178">Site Recovery가 호환되는 Azure 저장소 계정 및 네트워크가 하나 이상 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-178">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    ![저장소](./media/vmm-to-azure-walkthrough-source-target/compatible-storage.png)

3. <span data-ttu-id="189eb-180">아직 저장소 계정을 만들지 않았으며 Resource Manager를 사용하여 계정을 만들려면 **+저장소 계정**을 클릭하여 인라인에서 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-180">If you haven't created a storage account, and you want to create one using Resource Manager, click **+Storage account** to do that inline.</span></span>  <span data-ttu-id="189eb-181">**저장소 계정 만들기** 블레이드에서 계정 이름, 형식, 구독 및 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-181">On the **Create storage account** blade specify an account name, type, subscription, and location.</span></span> <span data-ttu-id="189eb-182">계정이 복구 서비스 자격 증명 모음과 같은 위치에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-182">The account should be in the same location as the Recovery Services vault.</span></span>

   ![저장소](./media/vmm-to-azure-walkthrough-source-target/gs-createstorage.png)


   * <span data-ttu-id="189eb-184">클래식 모델을 사용하여 저장소 계정을 만들려면 Azure 포털에서 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-184">If you want to create a storage account using the classic model, do that in the Azure portal.</span></span> [<span data-ttu-id="189eb-185">자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="189eb-185">Learn more</span></span>](../storage/common/storage-create-storage-account.md)
   * <span data-ttu-id="189eb-186">복제된 데이터에 프리미엄 저장소 계정을 사용하는 경우 온-프레미스 데이터에 지속적인 변화를 캡처하는 복제 로그를 저장하는 추가 표준 저장소 계정을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-186">If you’re using a premium storage account for replicated data, set up an additional standard storage account, to store replication logs that capture ongoing changes to on-premises data.</span></span>
5. <span data-ttu-id="189eb-187">아직 Azure 네트워크를 만들지 않았으며 Resource Manager를 사용하여 네트워크를 만들려면 **+네트워크**를 클릭하여 인라인에서 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-187">If you haven't created an Azure network, and you want to create one using Resource Manager, click **+Network** to do that inline.</span></span> <span data-ttu-id="189eb-188">**가상 네트워크 만들기** 블레이드에서 네트워크 이름, 주소 범위, 서브넷 세부 정보, 구독 및 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-188">On the **Create virtual network** blade specify a network name, address range, subnet details, subscription, and location.</span></span> <span data-ttu-id="189eb-189">네트워크가 복구 서비스 자격 증명 모음과 같은 위치에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-189">The network should be in the same location as the Recovery Services vault.</span></span>

   ![네트워크](./media/vmm-to-azure-walkthrough-source-target/gs-createnetwork.png)

   <span data-ttu-id="189eb-191">클래식 모델을 사용하여 네트워크를 만들려면 Azure 포털에서 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-191">If you want to create a network using the classic model, do that in the Azure portal.</span></span> <span data-ttu-id="189eb-192">[자세히 알아보기](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="189eb-192">[Learn more](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span></span>





## <a name="next-steps"></a><span data-ttu-id="189eb-193">다음 단계</span><span class="sxs-lookup"><span data-stu-id="189eb-193">Next steps</span></span>

<span data-ttu-id="189eb-194">[9단계: 네트워크 매핑 구성](vmm-to-azure-walkthrough-network-mapping.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="189eb-194">Go to [Step 9: Configure network mapping](vmm-to-azure-walkthrough-network-mapping.md)</span></span>
