---
title: "hello 소스 및 대상에 Azure Site Recovery와 VMware 복제 tooAzure aaaSet | Microsoft Docs"
description: "Azure Site Recovery를 사용 하 여 VMware Vm tooAzure 저장소의 복제에 대 한 원본 및 대상 설정을 hello 단계 tooset을 요약 되어 있습니다."
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
ms.openlocfilehash: ef33a44bc5da17afb0442be63f576925f5b9a8b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-vmware-replication-tooazure"></a><span data-ttu-id="74a02-103">8 단계: hello 원본 및 복제 tooAzure VMware에 대 한 대상 설정</span><span class="sxs-lookup"><span data-stu-id="74a02-103">Step 8: Set up hello source and target for VMware replication tooAzure</span></span>

<span data-ttu-id="74a02-104">이 문서에서는 어떻게 tooconfigure 원본 및 대상 설정을 복제할 때 온-프레미스 VMware 가상 컴퓨터 tooAzure hello를 사용 하 여 설명 [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-104">This article describes how tooconfigure source and target settings when replicating on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="74a02-105">Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="74a02-106">Hello 소스 환경 설정</span><span class="sxs-lookup"><span data-stu-id="74a02-106">Set up hello source environment</span></span>

<span data-ttu-id="74a02-107">Hello 구성 서버를 설정 하 고 hello 자격 증명 모음에 등록 한 다음 Vm을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-107">Set up hello configuration server, register it in hello vault, and discover VMs.</span></span>

1. <span data-ttu-id="74a02-108">**Site Recovery** > **1단계: 인프라 준비** > **원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="74a02-109">구성 서버가 없는 경우 **+구성 서버**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="74a02-110">**서버 추가**에서 **구성 서버**가 **서버 형식**에 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="74a02-111">Hello Site Recovery 통합 설치 설치 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-111">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="74a02-112">Hello 자격 증명 모음 등록 키를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-112">Download hello vault registration key.</span></span> <span data-ttu-id="74a02-113">통합 설치를 실행할 때 이 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="74a02-114">hello 키가 생성 한 후 5 일 동안 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-114">hello key is valid for five days after you generate it.</span></span>

   ![원본 설정](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a><span data-ttu-id="74a02-116">Hello 구성 서버 hello 자격 증명 모음 등록</span><span class="sxs-lookup"><span data-stu-id="74a02-116">Register hello configuration server in hello vault</span></span>

<span data-ttu-id="74a02-117">수행 하기 전에 hello 다음로 시작 하 고 통합 설치 tooinstall hello 구성 서버, hello 프로세스 서버 및 마스터 대상 서버 hello 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-117">Do hello following before you start, then run Unified Setup tooinstall hello configuration server, hello process server, and hello master target server.</span></span>
    - <span data-ttu-id="74a02-118">간단한 동영상 개요 보기</span><span class="sxs-lookup"><span data-stu-id="74a02-118">Get a quick video overview</span></span>

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - <span data-ttu-id="74a02-119">Hello 구성 서버 VM에서 해당 hello 시스템 시계와 동기화 되었는지 확인 한 [시간 서버](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service)합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-119">On hello configuration server VM, make sure that hello system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="74a02-120">서로 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-120">It should match.</span></span> <span data-ttu-id="74a02-121">15분 빠르거나 늦은 경우 설치가 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-121">If it's 15 minutes in front or behind, setup might fail.</span></span>
    - <span data-ttu-id="74a02-122">Hello 구성 서버 VM에서 로컬 관리자로 설치 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-122">Run setup as a Local Administrator on hello configuration server VM.</span></span>
    - <span data-ttu-id="74a02-123">Hello VM에서 TLS 1.0을 사용할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-123">Make sure TLS 1.0 is enabled on hello VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="74a02-124">hello 구성 서버를 설치할 수도 있습니다 [hello 명령줄에서](http://aka.ms/installconfigsrv)합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-124">hello configuration server can also be installed [from hello command line](http://aka.ms/installconfigsrv).</span></span>



## <a name="connect-toovmware-servers"></a><span data-ttu-id="74a02-125">TooVMware 서버 연결</span><span class="sxs-lookup"><span data-stu-id="74a02-125">Connect tooVMware servers</span></span>

<span data-ttu-id="74a02-126">tooallow Azure Site Recovery toodiscover 가상 컴퓨터 사용자의 온-프레미스 환경에서 실행 해야 tooconnect VMware vCenter Server 또는 사이트 복구와 vSphere ESXi 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-126">tooallow Azure Site Recovery toodiscover virtual machines running in your on-premises environment, you need tooconnect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span> <span data-ttu-id="74a02-127">시작 하기 전에 hello 다음 note:</span><span class="sxs-lookup"><span data-stu-id="74a02-127">Note hello following before you start:</span></span>

- <span data-ttu-id="74a02-128">Hello 서버에서 관리자 권한이 없는 계정으로 vSphere 호스트 tooSite 복구 또는 hello vCenter 서버를 추가 하는 경우 hello 계정이 이러한 권한을 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-128">If you add hello vCenter server or vSphere hosts tooSite Recovery with an account without administrator privileges on hello server, hello account needs these privileges enabled:</span></span>
    - <span data-ttu-id="74a02-129">데이터 센터, 데이터 저장소, 폴더, 호스트, 네트워크, 리소스, 가상 컴퓨터, vSphere 분산 스위치 등의 권한을 사용할 수 있도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-129">Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, vSphere Distributed Switch.</span></span>
    - <span data-ttu-id="74a02-130">hello vCenter 서버에 저장소 보기 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-130">hello vCenter server needs Storage views permissions.</span></span>
- <span data-ttu-id="74a02-131">VMware 서버 tooSite 복구를 추가 하면 15 분이 걸릴 수 정도을 tooappear hello 포털에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-131">When you add VMware servers tooSite Recovery, it can take 15 minutes or longer for them tooappear in hello portal.</span></span>

### <a name="add-hello-account-for-automatic-discovery"></a><span data-ttu-id="74a02-132">자동 검색에 대 한 hello 계정 추가</span><span class="sxs-lookup"><span data-stu-id="74a02-132">Add hello account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="set-up-a-connection"></a><span data-ttu-id="74a02-133">연결 설정</span><span class="sxs-lookup"><span data-stu-id="74a02-133">Set up a connection</span></span>

<span data-ttu-id="74a02-134">다음과 같이 tooservers 연결:</span><span class="sxs-lookup"><span data-stu-id="74a02-134">Connect tooservers as follows:</span></span>

1. <span data-ttu-id="74a02-135">선택 **+ vCenter** toostart VMware vCenter server 또는 VMware vSphere ESXi 호스트를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-135">Select **+vCenter** toostart connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>
2. <span data-ttu-id="74a02-136">**vCenter 추가**hello vSphere 호스트 또는 vCenter 서버에 대 한 알기 쉬운 이름을 지정 하 고 다음 hello IP 주소 또는 hello 서버의 FQDN을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-136">In **Add vCenter**, specify a friendly name for hello vSphere host or vCenter server, and then specify hello IP address or FQDN of hello server.</span></span>
3. <span data-ttu-id="74a02-137">다른 포트에서 요청에 대해 구성 된 toolisten VMware 서버 도달 하지 못할 경우 hello 포트를 443으로 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-137">Leave hello port as 443 unless your VMware servers are configured toolisten for requests on a different port.</span></span> <span data-ttu-id="74a02-138">tooconnect toohello VMware vCenter 또는 vSphere ESXi 서버 hello 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-138">Select hello account that is tooconnect toohello VMware vCenter or vSphere ESXi server.</span></span> <span data-ttu-id="74a02-139">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-139">Click **OK**.</span></span>
4. <span data-ttu-id="74a02-140">TooVMware 서버를 연결 하는 사이트 복구 hello를 사용 하 여 설정을 지정 하 고 Vm을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-140">Site Recovery connects tooVMware servers using hello specified settings, and discovers VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="74a02-141">서버 또는 hello vCenter 또는 호스트 서버에 대 한 관리자 권한이 없는 계정으로는 호스트를 추가 하는 경우 hello 계정에 이러한 권한을 사용할 수 있는지 확인 하십시오: 데이터 센터, 데이터 저장소, 폴더, 호스트, 네트워크, 리소스, 가상 컴퓨터 및 vSphere 분산 스위치입니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-141">If you're adding a server or host with an account that doesn't have administrator privileges on hello vCenter or host server, make sure that hello account has these privileges enabled: Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, and vSphere Distributed Switch.</span></span> <span data-ttu-id="74a02-142">또한 hello VMware vCenter server는 권한 사용 하도록 설정 하는 hello 저장소 뷰가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-142">In addition, hello VMware vCenter server needs hello Storage Views privilege enabled.</span></span>


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="74a02-143">Hello 대상 환경 설정</span><span class="sxs-lookup"><span data-stu-id="74a02-143">Set up hello target environment</span></span>

<span data-ttu-id="74a02-144">Hello 대상 환경 설정 하기 전에 Azure 저장소 계정 및 가상 네트워크를 설정 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-144">Before you set up hello target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="74a02-145">클릭 **준비 인프라** > **대상**, 선택 hello toouse를 원하는 Azure 구독 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-145">Click **Prepare infrastructure** > **Target**, and select hello Azure subscription you want toouse.</span></span>
2. <span data-ttu-id="74a02-146">대상 배포 모델이 리소스 관리자 기반인지, 클래식인지 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-146">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="74a02-147">Site Recovery가 호환되는 Azure 저장소 계정 및 네트워크가 하나 이상 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-147">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![대상](./media/vmware-walkthrough-source-target/gs-target.png)
4. <span data-ttu-id="74a02-149">저장소 계정 또는 네트워크를 만들지 않은 경우 클릭 **저장소 계정 추가** 또는 **+ 네트워크**, 리소스 관리자 계정 또는 네트워크 인라인 toocreate 합니다.</span><span class="sxs-lookup"><span data-stu-id="74a02-149">If you haven't created a storage account or network, click **+Storage account** or **+Network**, toocreate a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74a02-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="74a02-150">Next steps</span></span>

<span data-ttu-id="74a02-151">너무 이동[9 단계: 복제 정책 설정](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="74a02-151">Go too[Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>
