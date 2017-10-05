---
title: "Azure Site Recovery를 사용하여 Azure로 Hyper-V(System Center VMM 없음) 복제를 위한 원본 및 대상 설정 | Microsoft Docs"
description: "Azure Site Recovery를 사용하여 Azure Storage에 Hyper-V VM의 복제를 위한 원본 및 대상 설정을 설정하는 단계를 요약"
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
ms.openlocfilehash: b38eb3a011d46f2239891ea1d1bcac2a4059a866
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="step-8-set-up-the-source-and-target-for-hyper-v-replication-to-azure"></a><span data-ttu-id="33afd-103">8단계: Azure에 Hyper-V 복제를 위한 원본 및 대상</span><span class="sxs-lookup"><span data-stu-id="33afd-103">Step 8: Set up the source and target for Hyper-V replication to Azure</span></span>

<span data-ttu-id="33afd-104">이 문서에서는 Azure Portal에서 [Azure Site Recovery](site-recovery-overview.md) 서비스를 사용하여 Azure에 온-프레미스 Hyper-V 가상 컴퓨터(System Center VMM 없음)를 복제할 때 원본 및 대상 설정을 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-104">This article describes how to configure source and target settings when replicating on-premises Hyper-V virtual machines (without System Center VMM) to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="33afd-105">이 문서의 하단 또는 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 의견이나 질문을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-the-source-environment"></a><span data-ttu-id="33afd-106">원본 환경 설정</span><span class="sxs-lookup"><span data-stu-id="33afd-106">Set up the source environment</span></span>

<span data-ttu-id="33afd-107">Hyper-V 사이트를 설정하고, Hyper-V 호스트에 Azure Site Recovery 공급자와 Azure Recovery Services 에이전트를 설치하고, 자격 증명 모음에 사이트를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-107">Set up the Hyper-V site, install the Azure Site Recovery Provider and the Azure Recovery Services agent on Hyper-V hosts, and register the site in the vault.</span></span>

1. <span data-ttu-id="33afd-108">**인프라 준비**에서 **원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-108">In **Prepare Infrastructure**, click **Source**.</span></span> <span data-ttu-id="33afd-109">Hyper-V 호스트 또는 클러스터의 컨테이너로 새 Hyper-V 사이트를 추가하려면 **+Hyper-V 사이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-109">To add a new Hyper-V site as a container for your Hyper-V hosts or clusters, click **+Hyper-V Site**.</span></span>

    ![원본 설정](./media/hyper-v-site-walkthrough-source-target/set-source1.png)
2. <span data-ttu-id="33afd-111">**Hyper-V 사이트 만들기**에서 사이트의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-111">In **Create Hyper-V site**, specify a name for the site.</span></span> <span data-ttu-id="33afd-112">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-112">Then click **OK**.</span></span> <span data-ttu-id="33afd-113">앞에서 만든 사이트를 선택하고 **+Hyper-V 서버**를 클릭하여 사이트에 서버를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-113">Now, select the site you created, and click **+Hyper-V Server** to add a server to the site.</span></span>

    ![원본 설정](./media/hyper-v-site-walkthrough-source-target/set-source2.png)

3. <span data-ttu-id="33afd-115">**서버 추가** > **서버 형식**에 **Hyper-V 서버**가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-115">In **Add Server** > **Server type**, check that **Hyper-V server** is displayed.</span></span>

    - <span data-ttu-id="33afd-116">추가하려는 Hyper-V 서버가 [필수 구성 요소](#on-premises-prerequisites)를 충족하며 지정된 URL에 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-116">Make sure that the Hyper-V server you want to add complies with the [prerequisites](#on-premises-prerequisites), and is able to access the specified URLs.</span></span>
    - <span data-ttu-id="33afd-117">Azure Site Recovery 공급자 설치 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-117">Download the Azure Site Recovery Provider installation file.</span></span> <span data-ttu-id="33afd-118">이 파일을 실행하여 공급자와 Recovery Services 에이전트를 각 Hyper-V 호스트에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-118">You run this file to install the Provider and the Recovery Services agent on each Hyper-V host.</span></span>

    ![원본 설정](./media/hyper-v-site-walkthrough-source-target/set-source3.png)


## <a name="install-the-provider-and-agent"></a><span data-ttu-id="33afd-120">공급자 및 에이전트를 설치</span><span class="sxs-lookup"><span data-stu-id="33afd-120">Install the Provider and agent</span></span>

1. <span data-ttu-id="33afd-121">Hyper-V 사이트를 추가할 각 호스트에서 공급자 설치 파일을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-121">Run the Provider setup file on each host you added to the Hyper-V site.</span></span> <span data-ttu-id="33afd-122">Hyper-V 클러스터에 설치하는 경우 각 클러스터 노드에서 설치 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-122">If you're installing on a Hyper-V cluster, run setup on each cluster node.</span></span> <span data-ttu-id="33afd-123">각 Hyper-V 클러스터 노드를 설치하고 등록하면 노드 간 마이그레이션에서도 VM이 안전하게 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-123">Installing and registering each Hyper-V cluster node ensures that VMs are protected, even if they migrate across nodes.</span></span>
2. <span data-ttu-id="33afd-124">Microsoft Update 정책에 따라 공급자 업데이트가 설치되도록 **Microsoft Update**에서 업데이트를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-124">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="33afd-125">**설치**에서 기본 공급자 설치 위치를 수락하거나 수정하고 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-125">In **Installation**, accept or modify the default Provider installation location and click **Install**.</span></span>
4. <span data-ttu-id="33afd-126">**자격 증명 모음 설정**에서 **찾아보기**를 클릭하고 다운로드한 자격 증명 모음 키 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-126">In **Vault Settings**, click **Browse** to select the vault key file that you downloaded.</span></span> <span data-ttu-id="33afd-127">Azure Site Recovery 구독, 자격 증명 모음 이름 및 Hyper-V 서버가 속한 Hyper-V 사이트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-127">Specify the Azure Site Recovery subscription, the vault name, and the Hyper-V site to which the Hyper-V server belongs.</span></span>

    ![서버 등록](./media/hyper-v-site-walkthrough-source-target/provider3.png)

5. <span data-ttu-id="33afd-129">**프록시 설정**에서, Hyper-V 호스트에서 실행 중인 공급자가 인터넷을 통해 Azure Site Recovery에 연결하는 방법을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-129">In **Proxy Settings**, specify how the Provider running on Hyper-V hosts connects to Azure Site Recovery over the internet.</span></span>

    * <span data-ttu-id="33afd-130">공급자를 직접 연결하려면 **프록시 없이 Azure Site Recovery에 직접 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-130">If you want the Provider to connect directly select **Connect directly to Azure Site Recovery without a proxy**.</span></span>
    * <span data-ttu-id="33afd-131">기존 프록시에 인증이 필요하거나 공급자 연결에 사용자 지정 프록시를 사용하려면 **프록시 서버를 사용하여 Azure Site Recovery에 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-131">If your existing proxy requires authentication, or you want to use a custom proxy for the Provider connection, select **Connect to Azure Site Recovery using a proxy server**.</span></span>
    * <span data-ttu-id="33afd-132">프록시를 사용하는 경우:</span><span class="sxs-lookup"><span data-stu-id="33afd-132">If you use a proxy:</span></span>
        - <span data-ttu-id="33afd-133">주소, 포트 및 자격 증명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-133">Specify the address, port, and credentials</span></span>
        - <span data-ttu-id="33afd-134">[필수 구성 요소](#prerequisites)에 설명된 URL이 프록시를 통과할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-134">Make sure the URLs described in the [prerequisites](#prerequisites) are allowed through the proxy.</span></span>

    ![인터넷](./media/hyper-v-site-walkthrough-source-target/provider7.png)

6. <span data-ttu-id="33afd-136">설치가 완료되면 **등록**을 클릭하여 자격 증명 모음에 서버를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-136">After installation finishes, click **Register** to register the server in the vault.</span></span>

    ![설치 위치](./media/hyper-v-site-walkthrough-source-target/provider2.png)

7. <span data-ttu-id="33afd-138">등록이 완료되면 Azure Site Recovery에서 Hyper-V 서버의 메타데이터가 검색되며 서버가 **Site Recovery 인프라** > **Hyper-V 호스트**에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-138">After registration finishes, metadata from the Hyper-V server is retrieved by Azure Site Recovery, and the server is displayed in **Site Recovery Infrastructure** > **Hyper-V Hosts**.</span></span>


## <a name="set-up-the-target-environment"></a><span data-ttu-id="33afd-139">대상 환경 설정</span><span class="sxs-lookup"><span data-stu-id="33afd-139">Set up the target environment</span></span>

<span data-ttu-id="33afd-140">복제에 사용할 Azure 저장소 계정과 장애 조치(failover) 후 Azure VM이 연결될 Azure 네트워크를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-140">Specify the Azure storage account for replication, and the Azure network to which Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="33afd-141">**인프라 준비** > **대상**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-141">Click **Prepare infrastructure** > **Target**.</span></span>
2. <span data-ttu-id="33afd-142">장애 조치(failover) 후 Azure VM을 만들 구독 및 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-142">Select the subscription and the resource group in which you want to create the Azure VMs after failover.</span></span> <span data-ttu-id="33afd-143">Azure(클래식 또는 리소스 관리)에서 VM에 사용할 배포 모델을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-143">Choose the deployment model that you want to use in Azure (classic or resource management) for the VMs.</span></span>

3. <span data-ttu-id="33afd-144">Site Recovery가 호환되는 Azure 저장소 계정 및 네트워크가 하나 이상 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-144">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    - <span data-ttu-id="33afd-145">저장소 계정이 없으면 **+저장소**를 클릭하여 Resource Manager 기반 계정 인라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-145">If you don't have a storage account, click **+Storage** to create a Resource Manager-based account inline.</span></span> 
    - <span data-ttu-id="33afd-146">Azure 네트워크가 없으면 **+네트워크**를 클릭하여 Resource Manager 기반 네트워크 인라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-146">If you don't have a Azure network, click **+Network** to create a Resource Manager-based network inline.</span></span>






## <a name="next-steps"></a><span data-ttu-id="33afd-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="33afd-147">Next steps</span></span>

<span data-ttu-id="33afd-148">[9단계: 복제 정책 설정](hyper-v-site-walkthrough-replication.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="33afd-148">Go to [Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>
