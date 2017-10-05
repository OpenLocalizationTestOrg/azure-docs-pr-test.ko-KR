---
title: " Azure(Resource Manager)에서 실행되는 프로세스 서버 관리 | Microsoft Docs"
description: "이 문서에서는 Azure에서 장애 복구 프로세스 서버(Resource Manager)를 설정하는 방법을 설명합니다."
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
ms.openlocfilehash: 2b9b31abd5d11d02935a74e47d26be9803cdc920
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-process-server-running-in-azure-resource-manager"></a><span data-ttu-id="aa26f-103">Azure에서 실행되는 프로세스 서버 관리(Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="aa26f-103">Manage a process server running in Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="aa26f-104">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="aa26f-104">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)
> * [<span data-ttu-id="aa26f-105">클래식</span><span class="sxs-lookup"><span data-stu-id="aa26f-105">Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)

<span data-ttu-id="aa26f-106">장애 복구 동안 Azure Virtual Network와 온-프레미스 네트워크 간에 대기 시간이 긴 경우 Azure에서 프로세스 서버를 배포하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="aa26f-106">During failback, it is recommended to deploy process server in Azure if there is high latency between the Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="aa26f-107">이 문서에서는 Azure에서 실행 중인 프로세스 서버를 설정, 구성 및 관리하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="aa26f-107">This article describes how you can set up, configure, and manage the process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="aa26f-108">이 문서는 장애 조치 중에 가상 컴퓨터에 대한 배포 모델로 **Resource Manager**를 사용한 경우에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa26f-108">This article is to be used if you used **Resource Manager** as the deployment model for the virtual machines during failover.</span></span> <span data-ttu-id="aa26f-109">배포 모델로 **클래식**을 사용한 경우 [장애 복구 프로세스 서버를 설정 및 구성하는 방법(클래식)](./site-recovery-vmware-setup-azure-ps-classic.md)의 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="aa26f-109">If you used **Classic** as the deployment model, follow the steps in [How to set up & configure a Failback process server (Classic)](./site-recovery-vmware-setup-azure-ps-classic.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa26f-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="aa26f-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prerequ](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="aa26f-111">Azure에 프로세스 서버 배포</span><span class="sxs-lookup"><span data-stu-id="aa26f-111">Deploy a process server on Azure</span></span>
1. <span data-ttu-id="aa26f-112">자격 증명 모음 > **Site Recovery 인프라**("관리" 헤드에 있음) > **구성 서버**("VMware 및 실제 컴퓨터" 헤드에 있음)에서 구성 서버를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aa26f-112">In the Vault > **Site Recovery Infrastructure** (under the "Manage" heading) > **Configuration Servers** (under "For VMware and Physical Machines" heading), select the configuration server.</span></span>
2. <span data-ttu-id="aa26f-113">열리는 구성 서버 세부 정보 페이지에서 "+프로세스 서버" 클릭</span><span class="sxs-lookup"><span data-stu-id="aa26f-113">In the Configuration Server details page that opens click "+ Process server"</span></span>

  ![프로세스 서버 갤러리 추가](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps.png)

3.  <span data-ttu-id="aa26f-115">**프로세스 서버 추가** 페이지에서 다음 값 선택</span><span class="sxs-lookup"><span data-stu-id="aa26f-115">On the **Add process server** page, select the following values</span></span>

  ![프로세스 서버 갤러리 항목 추가](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-1.png)
|<span data-ttu-id="aa26f-117">**필드 이름**</span><span class="sxs-lookup"><span data-stu-id="aa26f-117">**Field Name**</span></span>|<span data-ttu-id="aa26f-118">**값**</span><span class="sxs-lookup"><span data-stu-id="aa26f-118">**Value**</span></span>|
|-|-|
|<span data-ttu-id="aa26f-119">프로세스 서버를 배포할 위치 선택</span><span class="sxs-lookup"><span data-stu-id="aa26f-119">Choose where you want to deploy your process server</span></span>|<span data-ttu-id="aa26f-120">**Azure에 장애 복구 프로세스 서버 배포** 값 선택</span><span class="sxs-lookup"><span data-stu-id="aa26f-120">Select the value **Deploy a failback process server in Azure**</span></span> |
|<span data-ttu-id="aa26f-121">구독</span><span class="sxs-lookup"><span data-stu-id="aa26f-121">Subscription</span></span>|<span data-ttu-id="aa26f-122">가상 컴퓨터를 장애 조치한 Azure 구독 선택</span><span class="sxs-lookup"><span data-stu-id="aa26f-122">Select the Azure Subscription where you failed over the virtual machines</span></span>|
|<span data-ttu-id="aa26f-123">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="aa26f-123">Resource Group</span></span>|<span data-ttu-id="aa26f-124">리소스 그룹을 만들어 이 프로세스 서버를 배포하거나 기존 리소스 그룹에 프로세스 서버를 배포하도록 선택</span><span class="sxs-lookup"><span data-stu-id="aa26f-124">You can create a Resource Group to deploy this process server or choose to deploy the process server in an existing Resource Group</span></span>|
|<span data-ttu-id="aa26f-125">위치</span><span class="sxs-lookup"><span data-stu-id="aa26f-125">Location</span></span>|<span data-ttu-id="aa26f-126">가상 컴퓨터가 장애 조치된 Azure 데이터 센터 선택</span><span class="sxs-lookup"><span data-stu-id="aa26f-126">Select the Azure Data Center into which the virtual machines where failed over into</span></span>|
|<span data-ttu-id="aa26f-127">Azure 네트워크</span><span class="sxs-lookup"><span data-stu-id="aa26f-127">Azure Network</span></span>|<span data-ttu-id="aa26f-128">가상 컴퓨터가 장애 조치된 Azure VNet(Virtual Network) 선택.</span><span class="sxs-lookup"><span data-stu-id="aa26f-128">Select the Azure Virtual Network(VNet) that the virtual machines where failed over into.</span></span> <span data-ttu-id="aa26f-129">가상 컴퓨터를 여러 Azure Vnet으로 장애 조치한 경우 VNet마다 배포된 프로세스 서버가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa26f-129">If you failed over virtual machines into multiple Azure VNets, then you need a process server deployed per VNet</span></span>|

4. <span data-ttu-id="aa26f-130">프로세스 서버에 대한 나머지 속성 채우기</span><span class="sxs-lookup"><span data-stu-id="aa26f-130">Fill in the rest of the properties for the process server</span></span>

  ![프로세스 서버 요약 추가](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-2.png)
|<span data-ttu-id="aa26f-132">**필드 이름**</span><span class="sxs-lookup"><span data-stu-id="aa26f-132">**Field Name**</span></span>|<span data-ttu-id="aa26f-133">**값**</span><span class="sxs-lookup"><span data-stu-id="aa26f-133">**Value**</span></span>|
|-|-|
|<span data-ttu-id="aa26f-134">서버 이름</span><span class="sxs-lookup"><span data-stu-id="aa26f-134">Server Name</span></span>|<span data-ttu-id="aa26f-135">프로세스 서버 가상 컴퓨터에 대한 표시 이름/호스트 이름</span><span class="sxs-lookup"><span data-stu-id="aa26f-135">Display name & Host name for your process server virtual machine</span></span>|
| <span data-ttu-id="aa26f-136">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="aa26f-136">User Name</span></span>|<span data-ttu-id="aa26f-137">해당 가상 컴퓨터에서 관리자가 되는 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="aa26f-137">A user name that becomes an Administrator on that virtual machine</span></span>|
|<span data-ttu-id="aa26f-138">저장소 계정</span><span class="sxs-lookup"><span data-stu-id="aa26f-138">Storage Account</span></span>|<span data-ttu-id="aa26f-139">가상 컴퓨터의 가상 디스크가 배치되는 저장소 계정의 이름</span><span class="sxs-lookup"><span data-stu-id="aa26f-139">Name of the Storage Account where the virtual machine's virtual disk's are placed</span></span>|
|<span data-ttu-id="aa26f-140">서브넷</span><span class="sxs-lookup"><span data-stu-id="aa26f-140">Subnet</span></span>|<span data-ttu-id="aa26f-141">가상 컴퓨터가 연결되는 Azure VNet의 서브넷</span><span class="sxs-lookup"><span data-stu-id="aa26f-141">The subnet of the Azure VNet to which the virtual machine is connected</span></span>|
| <span data-ttu-id="aa26f-142">IP 주소</span><span class="sxs-lookup"><span data-stu-id="aa26f-142">IP Address</span></span>|<span data-ttu-id="aa26f-143">프로세스 서버가 부팅될 경우 간주되는 IP 주소</span><span class="sxs-lookup"><span data-stu-id="aa26f-143">IP Address that you would like the process server to assume once it boots up</span></span>|
5. <span data-ttu-id="aa26f-144">확인 단추를 클릭하여 프로세스 서버 가상 컴퓨터 배포를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="aa26f-144">Click the OK button to start deploying the process server virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="aa26f-145">장애 복구를 위해 이 프로세스 서버를 사용하려면 온-프레미스 구성 서버에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa26f-145">To be able to use this process server for failback, you need to register it with the on-premises configuration server.</span></span>

## <a name="registering-the-process-server-running-in-azure-to-a-configuration-server-running-on-premises"></a><span data-ttu-id="aa26f-146">프로세스 서버(Azure에서 실행)를 구성 서버(온-프레미스에서 실행)에 등록</span><span class="sxs-lookup"><span data-stu-id="aa26f-146">Registering the process server (running in Azure) to a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-the-process-server-to-latest-version"></a><span data-ttu-id="aa26f-147">프로세스 서버를 최신 버전으로 업그레이드</span><span class="sxs-lookup"><span data-stu-id="aa26f-147">Upgrading the process server to latest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-the-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="aa26f-148">프로세스 서버(Azure에서 실행)를 구성 서버(온-프레미스에서 실행)에 등록 취소</span><span class="sxs-lookup"><span data-stu-id="aa26f-148">Unregistering the process server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-unregister-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
