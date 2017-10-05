---
title: " Azure에서 실행되는 프로세스 서버 관리(클래식) | Microsoft Docs"
description: "이 문서에서는 Azure에서 장애 복구 프로세스 서버(클래식)를 설정하는 방법을 설명합니다."
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
ms.openlocfilehash: 479bbd207bcf715138c340f9e4d2634120bab85c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-process-server-running-in-azure-classic"></a><span data-ttu-id="d513a-103">Azure에서 실행되는 프로세스 서버 관리(클래식)</span><span class="sxs-lookup"><span data-stu-id="d513a-103">Manage a Process Server running in Azure (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d513a-104">Azure 클래식</span><span class="sxs-lookup"><span data-stu-id="d513a-104">Azure Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)
> * [<span data-ttu-id="d513a-105">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="d513a-105">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

<span data-ttu-id="d513a-106">장애 복구 동안 Azure Virtual Network와 온-프레미스 네트워크 간에 대기 시간이 긴 경우 Azure에서 프로세스 서버를 배포하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d513a-106">During failback, it is recommended to deploy Process Server in Azure if there is high latency between the Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="d513a-107">이 문서에서는 Azure에서 실행 중인 프로세스 서버를 설정, 구성 및 관리하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d513a-107">This article describes how you can set up, configure, and manage the process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="d513a-108">이 문서는 장애 조치 중에 가상 컴퓨터에 대한 배포 모델로 클래식을 사용한 경우에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d513a-108">This article is to be used if you used Classic as the deployment model for the virtual machines during failover.</span></span> <span data-ttu-id="d513a-109">배포 모델로 Resource Manager를 사용한 경우 [장애 복구 프로세스 서버를 설정 및 구성하는 방법(Resource Manager)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)의 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="d513a-109">If you used Resource Manager as the deployment model follow the steps in [How to set up & configure a Failback Process Server (Resource Manager)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d513a-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d513a-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prereq](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="d513a-111">Azure에 프로세스 서버 배포</span><span class="sxs-lookup"><span data-stu-id="d513a-111">Deploy a Process Server on Azure</span></span>

1. <span data-ttu-id="d513a-112">Azure Marketplace에서 **Microsoft Azure Site Recovery 프로세스 서버 V2**를 사용하여 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d513a-112">In Azure Marketplace, create a virtual machine using the **Microsoft Azure Site Recovery Process Server V2**</span></span> </br>
    <span data-ttu-id="d513a-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span><span class="sxs-lookup"><span data-stu-id="d513a-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span></span>
2. <span data-ttu-id="d513a-114">배포 모델로 **클래식**을 선택 했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d513a-114">Ensure that you select the deployment model as **Classic**</span></span> </br><span data-ttu-id="d513a-115">
  ![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span><span class="sxs-lookup"><span data-stu-id="d513a-115">
![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span></span>
3. <span data-ttu-id="d513a-116">가상 컴퓨터 만들기 마법사 > 기본 설정에서 가상 컴퓨터를 장애 조치한 구독 및 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d513a-116">In the Create virtual machine wizard > Basic Settings, ensure you select the Subscription and Location to where you failed over the virtual machines.</span></span></br><span data-ttu-id="d513a-117">
  ![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span><span class="sxs-lookup"><span data-stu-id="d513a-117">
![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span></span>
4. <span data-ttu-id="d513a-118">가상 컴퓨터가 장애 조치된 가상 컴퓨터가 연결된 Azure Virtual Network에 연결되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d513a-118">Ensure that the virtual machine is connected to the Azure Virtual Network to which the failed over virtual machine is connected.</span></span></br><span data-ttu-id="d513a-119">
  ![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span><span class="sxs-lookup"><span data-stu-id="d513a-119">
![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span></span>
5. <span data-ttu-id="d513a-120">프로세스 서버 가상 컴퓨터가 프로비전되면 로그인한 후 구성 서버에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d513a-120">Once the Process Server virtual machine is provisioned, you need to log in and register it with the Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="d513a-121">장애 복구를 위해 이 프로세스 서버를 사용하려면 온-프레미스 구성 서버에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d513a-121">To be able to use this Process Server for failback, you need to register it with the on-premises configuration server.</span></span>

## <a name="registering-the-process-server-running-in-azure-to-a-configuration-server-running-on-premises"></a><span data-ttu-id="d513a-122">프로세스 서버(Azure에서 실행)를 구성 서버(온-프레미스에서 실행)에 등록</span><span class="sxs-lookup"><span data-stu-id="d513a-122">Registering the Process Server (running in Azure) to a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-the-process-server-to-latest-version"></a><span data-ttu-id="d513a-123">프로세스 서버를 최신 버전으로 업그레이드</span><span class="sxs-lookup"><span data-stu-id="d513a-123">Upgrading the Process Server to latest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-the-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="d513a-124">프로세스 서버(Azure에서 실행)를 구성 서버(온-프레미스에서 실행)에 등록 취소</span><span class="sxs-lookup"><span data-stu-id="d513a-124">Unregistering the Process Server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
