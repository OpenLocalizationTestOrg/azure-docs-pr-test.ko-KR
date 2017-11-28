---
title: "Azure Site Recovery를 사용하여 Azure에 VMware 복제를 위한 소스 및 대상 설정 | Microsoft Docs"
description: "Azure Site Recovery를 사용하여 Azure Storage에 VMware VM의 복제를 위한 원본 및 대상 설정을 설정하는 단계를 요약"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99e422e-daf7-4fa8-af3c-af2340340136
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 94b629a62c3a54eee69ee397b2f27e3f20b753d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="step-8-set-up-the-source-and-target-for-vmware-replication-to-azure"></a><span data-ttu-id="9e1c5-103">8단계: Azure에 VMware 복제를 위한 원본 및 대상</span><span class="sxs-lookup"><span data-stu-id="9e1c5-103">Step 8: Set up the source and target for VMware replication to Azure</span></span>

<span data-ttu-id="9e1c5-104">이 문서에서는 Azure Portal에서 [Azure Site Recovery](site-recovery-overview.md) 서비스를 사용하여 Azure에 온-프레미스 VMware 가상 컴퓨터를 복제할 때 소스 및 대상 설정을 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-104">This article describes how to configure source and target settings when replicating on-premises VMware virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="9e1c5-105">이 문서의 하단 또는 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 의견이나 질문을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-the-source-environment"></a><span data-ttu-id="9e1c5-106">원본 환경 설정</span><span class="sxs-lookup"><span data-stu-id="9e1c5-106">Set up the source environment</span></span>

<span data-ttu-id="9e1c5-107">구성 서버를 설정하고 자격 증명 모음에 등록한 후 VM을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-107">Set up the configuration server, register it in the vault, and discover VMs.</span></span>

1. <span data-ttu-id="9e1c5-108">**Site Recovery** > **1단계: 인프라 준비** > **원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="9e1c5-109">구성 서버가 없는 경우 **+구성 서버**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="9e1c5-110">**서버 추가**에서 **구성 서버**가 **서버 형식**에 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="9e1c5-111">Site Recovery 통합 설치 프로그램 설치 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-111">Download the Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="9e1c5-112">자격 증명 모음 등록 키를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-112">Download the vault registration key.</span></span> <span data-ttu-id="9e1c5-113">통합 설치를 실행할 때 이 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="9e1c5-114">이 키는 생성된 날로부터 5일간 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-114">The key is valid for five days after you generate it.</span></span>

   ![원본 설정](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-the-configuration-server-in-the-vault"></a><span data-ttu-id="9e1c5-116">자격 증명 모음에 구성 서버 등록</span><span class="sxs-lookup"><span data-stu-id="9e1c5-116">Register the configuration server in the vault</span></span>

<span data-ttu-id="9e1c5-117">다음을 수행하여 시작하기 전에 통합 설치 프로그램을 실행하여 구성 서버, 프로세스 서버 및 마스터 대상 서버를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-117">Do the following before you start, then run Unified Setup to install the configuration server, the process server, and the master target server.</span></span>
    - <span data-ttu-id="9e1c5-118">간단한 동영상 개요 보기</span><span class="sxs-lookup"><span data-stu-id="9e1c5-118">Get a quick video overview</span></span>

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - <span data-ttu-id="9e1c5-119">구성 서버 VM에서 시스템 시계가 [시간 서버](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service)와 동기화되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-119">On the configuration server VM, make sure that the system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="9e1c5-120">서로 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-120">It should match.</span></span> <span data-ttu-id="9e1c5-121">15분 빠르거나 늦은 경우 설치가 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-121">If it's 15 minutes in front or behind, setup might fail.</span></span>
    - <span data-ttu-id="9e1c5-122">구성 서버 VM에서 로컬 관리자로 설치 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-122">Run setup as a Local Administrator on the configuration server VM.</span></span>
    - <span data-ttu-id="9e1c5-123">TLS 1.0이 VM에서 활성화되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-123">Make sure TLS 1.0 is enabled on the VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="9e1c5-124">[명령줄](http://aka.ms/installconfigsrv)을 통해 구성 서버를 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-124">The configuration server can also be installed [from the command line](http://aka.ms/installconfigsrv).</span></span>



## <a name="connect-to-vmware-servers"></a><span data-ttu-id="9e1c5-125">VMware 서버에 연결</span><span class="sxs-lookup"><span data-stu-id="9e1c5-125">Connect to VMware servers</span></span>

<span data-ttu-id="9e1c5-126">Azure Site Recovery가 온-프레미스 환경에서 실행 중인 가상 컴퓨터를 검색할 수 있게 하려면 Site Recovery와 VMware vCenter 서버 또는 vSphere ESXi 호스트를 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-126">To allow Azure Site Recovery to discover virtual machines running in your on-premises environment, you need to connect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span> <span data-ttu-id="9e1c5-127">시작하기 전에 다음을 기억하세요.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-127">Note the following before you start:</span></span>

- <span data-ttu-id="9e1c5-128">서버에 관리자 권한이 없는 계정으로 Site Recovery에 vCenter 서버 또는 vSphere 호스트를 추가하는 경우 계정에서</span><span class="sxs-lookup"><span data-stu-id="9e1c5-128">If you add the vCenter server or vSphere hosts to Site Recovery with an account without administrator privileges on the server, the account needs these privileges enabled:</span></span>
    - <span data-ttu-id="9e1c5-129">데이터 센터, 데이터 저장소, 폴더, 호스트, 네트워크, 리소스, 가상 컴퓨터, vSphere 분산 스위치 등의 권한을 사용할 수 있도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-129">Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, vSphere Distributed Switch.</span></span>
    - <span data-ttu-id="9e1c5-130">vCenter 서버에는 Storage 보기 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-130">The vCenter server needs Storage views permissions.</span></span>
- <span data-ttu-id="9e1c5-131">Site Recovery에 VMware 서버를 추가하는 경우 포털에 나타나려면 15분 이상 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-131">When you add VMware servers to Site Recovery, it can take 15 minutes or longer for them to appear in the portal.</span></span>

### <a name="add-the-account-for-automatic-discovery"></a><span data-ttu-id="9e1c5-132">자동 검색에 사용할 계정 추가</span><span class="sxs-lookup"><span data-stu-id="9e1c5-132">Add the account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="set-up-a-connection"></a><span data-ttu-id="9e1c5-133">연결 설정</span><span class="sxs-lookup"><span data-stu-id="9e1c5-133">Set up a connection</span></span>

<span data-ttu-id="9e1c5-134">다음과 같이 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-134">Connect to servers as follows:</span></span>

1. <span data-ttu-id="9e1c5-135">**+vCenter**를 선택하여 VMware vCenter 서버 또는 VMware vSphere ESXi 호스트를 연결하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-135">Select **+vCenter** to start connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>
2. <span data-ttu-id="9e1c5-136">**vCenter 추가**에서 vSphere 호스트 또는 vCenter Server에 대한 식별 이름을 지정하고 서버의 IP 주소 또는 FQDN을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-136">In **Add vCenter**, specify a friendly name for the vSphere host or vCenter server, and then specify the IP address or FQDN of the server.</span></span>
3. <span data-ttu-id="9e1c5-137">VMware 서버가 다른 포트에서 요청을 수신하도록 구성되지 않은 경우 포트를 443으로 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-137">Leave the port as 443 unless your VMware servers are configured to listen for requests on a different port.</span></span> <span data-ttu-id="9e1c5-138">VMware vCenter 또는 vSphere ESXi 서버에 연결할 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-138">Select the account that is to connect to the VMware vCenter or vSphere ESXi server.</span></span> <span data-ttu-id="9e1c5-139">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-139">Click **OK**.</span></span>
4. <span data-ttu-id="9e1c5-140">Site Recovery는 지정한 설정을 사용하여 VMware 서버에 연결하고 VM을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-140">Site Recovery connects to VMware servers using the specified settings, and discovers VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="9e1c5-141">vCenter 또는 호스트 서버에 대해 관리자 권한이 없는 계정으로 서버 또는 호스트를 추가하는 경우 계정에 데이터 센터, 데이터 저장소, 폴더, 호스트, 네트워크, 리소스, 가상 컴퓨터 및 vSphere 분산 스위치에 대한 권한이 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-141">If you're adding a server or host with an account that doesn't have administrator privileges on the vCenter or host server, make sure that the account has these privileges enabled: Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, and vSphere Distributed Switch.</span></span> <span data-ttu-id="9e1c5-142">또한 VMware vCenter 서버에 저장소 보기 권한을 사용하도록 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-142">In addition, the VMware vCenter server needs the Storage Views privilege enabled.</span></span>


## <a name="set-up-the-target-environment"></a><span data-ttu-id="9e1c5-143">대상 환경 설정</span><span class="sxs-lookup"><span data-stu-id="9e1c5-143">Set up the target environment</span></span>

<span data-ttu-id="9e1c5-144">대상 환경을 설정하기 전에 Azure Storage 계정 및 가상 네트워크가 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-144">Before you set up the target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="9e1c5-145">**인프라 준비** > **대상**을 클릭하고 사용하려는 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-145">Click **Prepare infrastructure** > **Target**, and select the Azure subscription you want to use.</span></span>
2. <span data-ttu-id="9e1c5-146">대상 배포 모델이 리소스 관리자 기반인지, 클래식인지 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-146">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="9e1c5-147">Site Recovery가 호환되는 Azure 저장소 계정 및 네트워크가 하나 이상 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-147">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![대상](./media/vmware-walkthrough-source-target/gs-target.png)
4. <span data-ttu-id="9e1c5-149">저장소 계정 또는 네트워크를 만들지 않았으면 **+저장소 계정** 또는 **+네트워크**를 클릭하여 리소스 관리자 계정이나 인라인 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-149">If you haven't created a storage account or network, click **+Storage account** or **+Network**, to create a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e1c5-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9e1c5-150">Next steps</span></span>

<span data-ttu-id="9e1c5-151">[9단계: 복제 정책 설정](vmware-walkthrough-replication.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1c5-151">Go to [Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>
