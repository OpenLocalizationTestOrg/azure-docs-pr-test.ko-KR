---
title: " Azure에서 실행되는 프로세스 서버 관리(클래식) | Microsoft Docs"
description: "이 문서에서는 설명 어떻게 tooset 장애 프로세스 Server(Classic)에서 Azure를 구성 합니다."
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
ms.openlocfilehash: eadcc0236c77c9ebbbc885c4a7ee81098f1f4e72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-classic"></a><span data-ttu-id="9f1e4-103">Azure에서 실행되는 프로세스 서버 관리(클래식)</span><span class="sxs-lookup"><span data-stu-id="9f1e4-103">Manage a Process Server running in Azure (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9f1e4-104">Azure 클래식</span><span class="sxs-lookup"><span data-stu-id="9f1e4-104">Azure Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)
> * [<span data-ttu-id="9f1e4-105">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="9f1e4-105">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

<span data-ttu-id="9f1e4-106">장애 복구 하는 동안 좋습니다 toodeploy 프로세스 서버가 Azure의 hello Azure 가상 네트워크와 온-프레미스 네트워크 간의 대기 시간이 긴 경우.</span><span class="sxs-lookup"><span data-stu-id="9f1e4-106">During failback, it is recommended toodeploy Process Server in Azure if there is high latency between hello Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="9f1e4-107">이 문서에서는 설정, 구성 하는 방법을 hello 프로세스 서버를 Azure에서 실행 중인 관리를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f1e4-107">This article describes how you can set up, configure, and manage hello process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="9f1e4-108">이 문서는 toobe로 사용한 경우 클래식 배포 모델 hello hello 가상 컴퓨터에 대 한 장애 조치 중에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f1e4-108">This article is toobe used if you used Classic as hello deployment model for hello virtual machines during failover.</span></span> <span data-ttu-id="9f1e4-109">Hello 배포 모델에 따라 hello 단계에 따라 리소스 관리자를 사용 하는 경우 [어떻게 tooset 위로 및 장애 복구 프로세스 서버 (리소스 관리자) 구성](./site-recovery-vmware-setup-azure-ps-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="9f1e4-109">If you used Resource Manager as hello deployment model follow hello steps in [How tooset up & configure a Failback Process Server (Resource Manager)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f1e4-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9f1e4-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prereq](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="9f1e4-111">Azure에 프로세스 서버 배포</span><span class="sxs-lookup"><span data-stu-id="9f1e4-111">Deploy a Process Server on Azure</span></span>

1. <span data-ttu-id="9f1e4-112">Azure 마켓플레이스에서 hello를 사용 하 여 가상 컴퓨터를 만들 **Microsoft Azure 사이트 복구 프로세스 서버 V2**</span><span class="sxs-lookup"><span data-stu-id="9f1e4-112">In Azure Marketplace, create a virtual machine using hello **Microsoft Azure Site Recovery Process Server V2**</span></span> </br>
    <span data-ttu-id="9f1e4-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span><span class="sxs-lookup"><span data-stu-id="9f1e4-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span></span>
2. <span data-ttu-id="9f1e4-114">Hello 배포 모델을 선택 해야 **클래식**</span><span class="sxs-lookup"><span data-stu-id="9f1e4-114">Ensure that you select hello deployment model as **Classic**</span></span> </br><span data-ttu-id="9f1e4-115">
  ![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span><span class="sxs-lookup"><span data-stu-id="9f1e4-115">
![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span></span>
3. <span data-ttu-id="9f1e4-116">Hello 만들기 가상 컴퓨터 마법사에서 > 기본 설정 확인 hello 구독 및 위치 toowhere 장애 조치 hello 가상 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f1e4-116">In hello Create virtual machine wizard > Basic Settings, ensure you select hello Subscription and Location toowhere you failed over hello virtual machines.</span></span></br><span data-ttu-id="9f1e4-117">
  ![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span><span class="sxs-lookup"><span data-stu-id="9f1e4-117">
![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span></span>
4. <span data-ttu-id="9f1e4-118">Hello 가상 컴퓨터에 연결 되어 있는지 확인 toohello Azure 가상 네트워크 toowhich hello 장애 조치 가상 컴퓨터에 연결 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f1e4-118">Ensure that hello virtual machine is connected toohello Azure Virtual Network toowhich hello failed over virtual machine is connected.</span></span></br><span data-ttu-id="9f1e4-119">
  ![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span><span class="sxs-lookup"><span data-stu-id="9f1e4-119">
![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span></span>
5. <span data-ttu-id="9f1e4-120">Hello 프로세스 서버 가상 컴퓨터를 프로 비전 되 면 toolog에 필요 하 고 구성 서버 hello로 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f1e4-120">Once hello Process Server virtual machine is provisioned, you need toolog in and register it with hello Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="9f1e4-121">toobe 수 toouse이 프로세스 서버 tooregister 해야 장애 복구를 사용 하 여 hello 온-프레미스 구성 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="9f1e4-121">toobe able toouse this Process Server for failback, you need tooregister it with hello on-premises configuration server.</span></span>

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a><span data-ttu-id="9f1e4-122">Hello (Azure에서 실행) 프로세스 서버 tooa (온-프레미스로 실행) 구성 서버를 등록 하는 중</span><span class="sxs-lookup"><span data-stu-id="9f1e4-122">Registering hello Process Server (running in Azure) tooa Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a><span data-ttu-id="9f1e4-123">Hello 프로세스 서버 toolatest 버전을 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f1e4-123">Upgrading hello Process Server toolatest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="9f1e4-124">등록을 취소 hello (온-프레미스로 실행) 하 여 구성 서버에서 프로세스 서버 (Azure에서 실행)</span><span class="sxs-lookup"><span data-stu-id="9f1e4-124">Unregistering hello Process Server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
