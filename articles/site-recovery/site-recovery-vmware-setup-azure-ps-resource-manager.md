---
title: " Azure(Resource Manager)에서 실행되는 프로세스 서버 관리 | Microsoft Docs"
description: "이 문서에서는 Azure에서 한 장애 복구를 tooset (리소스 관리자)를 처리 하는 방법을 설명 합니다."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 70426b96095cc42befff6c4114fb56536284a667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-resource-manager"></a><span data-ttu-id="87079-103">Azure에서 실행되는 프로세스 서버 관리(Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="87079-103">Manage a process server running in Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="87079-104">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="87079-104">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)
> * [<span data-ttu-id="87079-105">클래식</span><span class="sxs-lookup"><span data-stu-id="87079-105">Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)

<span data-ttu-id="87079-106">장애 복구 하는 동안 좋습니다 toodeploy 프로세스 서버가 Azure의 hello Azure 가상 네트워크와 온-프레미스 네트워크 간의 대기 시간이 긴 경우.</span><span class="sxs-lookup"><span data-stu-id="87079-106">During failback, it is recommended toodeploy process server in Azure if there is high latency between hello Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="87079-107">이 문서에서는 설정, 구성 하는 방법을 hello 프로세스 서버를 Azure에서 실행 중인 관리를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="87079-107">This article describes how you can set up, configure, and manage hello process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="87079-108">이 문서는 사용 하는 경우 사용 되는 toobe **리소스 관리자** hello 가상 컴퓨터 장애 조치 중에 대 한 hello 배포 모델로 합니다.</span><span class="sxs-lookup"><span data-stu-id="87079-108">This article is toobe used if you used **Resource Manager** as hello deployment model for hello virtual machines during failover.</span></span> <span data-ttu-id="87079-109">사용 하는 경우 **클래식** hello 배포 모델로 hello 단계에 따라 [어떻게 tooset 위로 및 장애 복구 (클래식) 프로세스 서버를 구성 합니다.](./site-recovery-vmware-setup-azure-ps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="87079-109">If you used **Classic** as hello deployment model, follow hello steps in [How tooset up & configure a Failback process server (Classic)](./site-recovery-vmware-setup-azure-ps-classic.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87079-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="87079-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prerequ](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="87079-111">Azure에 프로세스 서버 배포</span><span class="sxs-lookup"><span data-stu-id="87079-111">Deploy a process server on Azure</span></span>
1. <span data-ttu-id="87079-112">Hello 자격 증명 모음에서에서 > **사이트 복구 인프라** (아래 hello "Manage") > **구성 서버** (아래에서 "컴퓨터에 대 한 VMware 및 물리적" 제목) hello 구성 서버를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="87079-112">In hello Vault > **Site Recovery Infrastructure** (under hello "Manage" heading) > **Configuration Servers** (under "For VMware and Physical Machines" heading), select hello configuration server.</span></span>
2. <span data-ttu-id="87079-113">열리는 hello 구성 서버 세부 정보 페이지에서 클릭 "+ 서버 프로세스"</span><span class="sxs-lookup"><span data-stu-id="87079-113">In hello Configuration Server details page that opens click "+ Process server"</span></span>

  ![프로세스 서버 갤러리 추가](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps.png)

3.  <span data-ttu-id="87079-115">Hello에 **추가 프로세스 서버** 페이지에서 다음 값에는 선택 hello</span><span class="sxs-lookup"><span data-stu-id="87079-115">On hello **Add process server** page, select hello following values</span></span>

  ![프로세스 서버 갤러리 항목 추가](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-1.png)
|<span data-ttu-id="87079-117">**필드 이름**</span><span class="sxs-lookup"><span data-stu-id="87079-117">**Field Name**</span></span>|<span data-ttu-id="87079-118">**값**</span><span class="sxs-lookup"><span data-stu-id="87079-118">**Value**</span></span>|
|-|-|
|<span data-ttu-id="87079-119">저장할 toodeploy 프로세스 서버 선택</span><span class="sxs-lookup"><span data-stu-id="87079-119">Choose where you want toodeploy your process server</span></span>|<span data-ttu-id="87079-120">Hello 값 선택 **Azure의 장애 복구 프로세스 서버 배포**</span><span class="sxs-lookup"><span data-stu-id="87079-120">Select hello value **Deploy a failback process server in Azure**</span></span> |
|<span data-ttu-id="87079-121">구독</span><span class="sxs-lookup"><span data-stu-id="87079-121">Subscription</span></span>|<span data-ttu-id="87079-122">Hello 장애 조치 hello 가상 컴퓨터를 Azure 구독 선택</span><span class="sxs-lookup"><span data-stu-id="87079-122">Select hello Azure Subscription where you failed over hello virtual machines</span></span>|
|<span data-ttu-id="87079-123">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="87079-123">Resource Group</span></span>|<span data-ttu-id="87079-124">기존 리소스 그룹에서 toodeploy hello 프로세스 서버를 선택 하거나 리소스 그룹 toodeploy이 프로세스 서버를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87079-124">You can create a Resource Group toodeploy this process server or choose toodeploy hello process server in an existing Resource Group</span></span>|
|<span data-ttu-id="87079-125">위치</span><span class="sxs-lookup"><span data-stu-id="87079-125">Location</span></span>|<span data-ttu-id="87079-126">Hello Azure 데이터 센터는 hello 가상 컴퓨터를 선택으로 장애 조치 하는 경우</span><span class="sxs-lookup"><span data-stu-id="87079-126">Select hello Azure Data Center into which hello virtual machines where failed over into</span></span>|
|<span data-ttu-id="87079-127">Azure 네트워크</span><span class="sxs-lookup"><span data-stu-id="87079-127">Azure Network</span></span>|<span data-ttu-id="87079-128">가상 컴퓨터를 hello Azure 가상 Network(VNet) 선택 hello에 장애 조치를 합니다.</span><span class="sxs-lookup"><span data-stu-id="87079-128">Select hello Azure Virtual Network(VNet) that hello virtual machines where failed over into.</span></span> <span data-ttu-id="87079-129">가상 컴퓨터를 여러 Azure Vnet으로 장애 조치한 경우 VNet마다 배포된 프로세스 서버가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87079-129">If you failed over virtual machines into multiple Azure VNets, then you need a process server deployed per VNet</span></span>|

4. <span data-ttu-id="87079-130">프로세스 서버 hello에 대 한 hello 속성 hello 나머지를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="87079-130">Fill in hello rest of hello properties for hello process server</span></span>

  ![프로세스 서버 요약 추가](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-2.png)
|<span data-ttu-id="87079-132">**필드 이름**</span><span class="sxs-lookup"><span data-stu-id="87079-132">**Field Name**</span></span>|<span data-ttu-id="87079-133">**값**</span><span class="sxs-lookup"><span data-stu-id="87079-133">**Value**</span></span>|
|-|-|
|<span data-ttu-id="87079-134">서버 이름</span><span class="sxs-lookup"><span data-stu-id="87079-134">Server Name</span></span>|<span data-ttu-id="87079-135">프로세스 서버 가상 컴퓨터에 대한 표시 이름/호스트 이름</span><span class="sxs-lookup"><span data-stu-id="87079-135">Display name & Host name for your process server virtual machine</span></span>|
| <span data-ttu-id="87079-136">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="87079-136">User Name</span></span>|<span data-ttu-id="87079-137">해당 가상 컴퓨터에서 관리자가 되는 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="87079-137">A user name that becomes an Administrator on that virtual machine</span></span>|
|<span data-ttu-id="87079-138">저장소 계정</span><span class="sxs-lookup"><span data-stu-id="87079-138">Storage Account</span></span>|<span data-ttu-id="87079-139">hello hello 가상 컴퓨터의 가상 디스크의 위치는 저장소 계정 이름</span><span class="sxs-lookup"><span data-stu-id="87079-139">Name of hello Storage Account where hello virtual machine's virtual disk's are placed</span></span>|
|<span data-ttu-id="87079-140">서브넷</span><span class="sxs-lookup"><span data-stu-id="87079-140">Subnet</span></span>|<span data-ttu-id="87079-141">hello Azure VNet toowhich hello 가상 컴퓨터의 hello 서브넷 연결</span><span class="sxs-lookup"><span data-stu-id="87079-141">hello subnet of hello Azure VNet toowhich hello virtual machine is connected</span></span>|
| <span data-ttu-id="87079-142">IP 주소</span><span class="sxs-lookup"><span data-stu-id="87079-142">IP Address</span></span>|<span data-ttu-id="87079-143">싶다는 의사를 hello 프로세스 서버 tooassume 부팅 되 면 IP 주소</span><span class="sxs-lookup"><span data-stu-id="87079-143">IP Address that you would like hello process server tooassume once it boots up</span></span>|
5. <span data-ttu-id="87079-144">Hello 확인 단추 toostart hello 프로세스 서버 가상 컴퓨터 배포를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="87079-144">Click hello OK button toostart deploying hello process server virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="87079-145">toobe 수 toouse이 프로세스 서버 tooregister 해야 장애 복구를 사용 하 여 hello 온-프레미스 구성 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="87079-145">toobe able toouse this process server for failback, you need tooregister it with hello on-premises configuration server.</span></span>

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a><span data-ttu-id="87079-146">Hello 프로세스 서버 (Azure에서 실행) tooa (온-프레미스로 실행) 구성 서버를 등록 하는 중</span><span class="sxs-lookup"><span data-stu-id="87079-146">Registering hello process server (running in Azure) tooa Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a><span data-ttu-id="87079-147">Hello 프로세스 서버 toolatest 버전을 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="87079-147">Upgrading hello process server toolatest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="87079-148">구성 서버 (온-프레미스로 실행)에서 (Azure에서 실행) 하는 hello 프로세스 서버를 등록 취소</span><span class="sxs-lookup"><span data-stu-id="87079-148">Unregistering hello process server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-unregister-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
