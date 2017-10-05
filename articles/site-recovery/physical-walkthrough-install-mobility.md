---
title: "물리적 서버의 Azure에 복제를 위해 모바일 서비스 설치 | Microsoft Docs"
description: "이 문서에서는 Azure Site Recovery 서비스를 통해 Azure에 복제되는 물리적 서버에 모바일 서비스 에이전트를 설치하는 방법을 설명합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 3189fbcd-6b5b-4ffb-b5a9-e2080c37f9d9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: d73267d7a64221a3138af19e9a2d5dd15809b927
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="step-9-install-the-mobility-service"></a><span data-ttu-id="5b6ef-103">9단계: 모바일 서비스 설치</span><span class="sxs-lookup"><span data-stu-id="5b6ef-103">Step 9: Install the Mobility service</span></span>


<span data-ttu-id="5b6ef-104">이 문서에서는 Azure Portal에서 [Azure Site Recovery](site-recovery-overview.md) 서비스를 사용하여 Azure에 온-프레미스 Windows/Linux 물리적 서버를 복제할 때 모바일 서비스 구성 요소를 설치하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5b6ef-104">This article describes how to install the Mobility service component when replicating on-premises Windows/Linux physical servers to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="5b6ef-105">모바일 서비스는 컴퓨터에 기록된 데이터를 캡처하고 이를 프로세스 서버에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="5b6ef-105">The Mobility service captures data writes on a machine, and forwards them to the process server.</span></span> <span data-ttu-id="5b6ef-106">Azure에 복제하려는 각 서버에 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b6ef-106">It should be installed on each server that you want to replicate to Azure.</span></span>

<span data-ttu-id="5b6ef-107">모바일 서비스는 수동으로, 복제가 설정된 경우 Site Recovery 프로세스 서버에서 푸시 설치를 사용하거나, System Center Configuration Manager와 같은 도구를 사용하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b6ef-107">You can install the Mobility service manually, or using a push installation from the Site Recovery process server when replication is enabled, or using a tool such as System Center Configuration Manager.</span></span> <span data-ttu-id="5b6ef-108">푸시 설치를 사용하는 경우 복제를 설정한 경우 서버에 서비스가 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b6ef-108">If you use push installation, the service is installed on the server when you enable replication.</span></span>

<span data-ttu-id="5b6ef-109">이 문서의 하단 또는 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 의견이나 질문을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="5b6ef-109">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="5b6ef-110">수동 설치</span><span class="sxs-lookup"><span data-stu-id="5b6ef-110">Install manually</span></span>

1. <span data-ttu-id="5b6ef-111">수동 설치를 위한 [필수 조건](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites)을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5b6ef-111">Check the [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="5b6ef-112">포털을 사용하여 수동 설치를 위한 [이러한 지침](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="5b6ef-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using the portal.</span></span>
3. <span data-ttu-id="5b6ef-113">명령줄에서 설치하는 것을 선호하는 경우 [이러한 지침](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="5b6ef-113">If you prefer to install from the command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-the-process-server"></a><span data-ttu-id="5b6ef-114">프로세스 서버에서 설치</span><span class="sxs-lookup"><span data-stu-id="5b6ef-114">Install from the process server</span></span>

<span data-ttu-id="5b6ef-115">컴퓨터에 대해 복제가 설정된 경우 프로세스 서버에서 모바일 서비스 설치를 푸시하려면 프로세스 서버에서 컴퓨터에 액세스하는 데 사용할 수 있는 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5b6ef-115">If you want to push the Mobility service installation from the process server when you enable replication for a machine, you need an account that can be used by the process server to access the machine.</span></span> <span data-ttu-id="5b6ef-116">이 계정은 푸시 설치에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b6ef-116">The account is only used for the push installation.</span></span>

1. <span data-ttu-id="5b6ef-117">계정이 생성되지 않은 경우 다음 지침에 따라 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5b6ef-117">If you haven't created an account, do so using these guidelines:</span></span>

    - <span data-ttu-id="5b6ef-118">도메인 또는 로컬 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b6ef-118">You can use a domain or local account</span></span>
    - <span data-ttu-id="5b6ef-119">Windows에서는 도메인 계정을 사용하지 않는 경우 로컬 컴퓨터에서 원격 사용자 액세스 제어를 사용하지 않도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b6ef-119">For Windows, if you're not using a domain account, you need to disable Remote User Access control on the local machine.</span></span> <span data-ttu-id="5b6ef-120">그러려면 레지스터의 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**에서 값이 1인 **LocalAccountTokenFilterPolicy** DWORD 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5b6ef-120">To do this, in the register under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, add the DWORD entry **LocalAccountTokenFilterPolicy**, with a value of 1.</span></span>
    - <span data-ttu-id="5b6ef-121">CLI에서 Windows의 레지스트리 항목을 추가하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5b6ef-121">If you want to add the registry entry for Windows from a CLI, type:</span></span>

        ```
        REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.
        ```

    - <span data-ttu-id="5b6ef-122">Linux에서 계정은 원본 Linux 서버의 루트여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b6ef-122">For Linux, the account should be root on the source Linux server.</span></span>

2. <span data-ttu-id="5b6ef-123">Windows 또는 Linux를 실행하는 VM에서 모바일 서비스를 푸시하는 경우 [이러한 지침](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="5b6ef-123">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want to push the Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-installation-methods"></a><span data-ttu-id="5b6ef-124">다른 설치 방법</span><span class="sxs-lookup"><span data-stu-id="5b6ef-124">Other installation methods</span></span>

- <span data-ttu-id="5b6ef-125">Configuration Manager를 사용하여 모바일 서비스 설치에 대해 [자세히 알아보기](site-recovery-install-mobility-service-using-sccm.md)</span><span class="sxs-lookup"><span data-stu-id="5b6ef-125">[Learn about](site-recovery-install-mobility-service-using-sccm.md) installing the Mobility service using Configuration Manager</span></span>
- <span data-ttu-id="5b6ef-126">Azure Automation DSC로 설치에 대해 [자세히 알아보기](site-recovery-automate-mobility-service-install.md)</span><span class="sxs-lookup"><span data-stu-id="5b6ef-126">[Learn about](site-recovery-automate-mobility-service-install.md) installing with Azure Automation DSC.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5b6ef-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5b6ef-127">Next steps</span></span>

<span data-ttu-id="5b6ef-128">[10단계: 복제 활성화](physical-walkthrough-enable-replication.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5b6ef-128">Go to [Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>
