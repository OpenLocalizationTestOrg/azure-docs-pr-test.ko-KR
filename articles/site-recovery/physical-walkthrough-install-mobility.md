---
title: "aaaInstall hello 물리적 서버 tooAzure 복제에 대 한 모바일 서비스 | Microsoft Docs"
description: "이 문서에서는 tooinstall hello Azure Site Recovery 서비스와 tooAzure를 복제 하는 물리적 서버에서 모바일 서비스 에이전트가 hello 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 48fd2c0ffe67875ed446c8167c2ae7f90d3f537c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-install-hello-mobility-service"></a><span data-ttu-id="50524-103">9 단계: hello 모바일 서비스를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="50524-103">Step 9: Install hello Mobility service</span></span>


<span data-ttu-id="50524-104">이 문서에서는 어떻게 tooinstall hello 모바일 서비스 구성 요소를 복제할 때 온-프레미스 Windows/Linux 물리적 서버의 tooAzure, hello를 사용 하 여 설명 [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="50524-104">This article describes how tooinstall hello Mobility service component when replicating on-premises Windows/Linux physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="50524-105">hello 모바일 서비스는 컴퓨터에 데이터 쓰기를 캡처하고 toohello 프로세스 서버에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="50524-105">hello Mobility service captures data writes on a machine, and forwards them toohello process server.</span></span> <span data-ttu-id="50524-106">Tooreplicate tooAzure 하려는 각 서버에 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="50524-106">It should be installed on each server that you want tooreplicate tooAzure.</span></span>

<span data-ttu-id="50524-107">Hello 모바일 서비스를 수동으로 설치할 수 있습니다 또는 복제를 사용 하는 경우 서버 또는 System Center Configuration Manager와 같은 도구를 사용 하 여 사이트 복구 처리 hello에서 강제 설치를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="50524-107">You can install hello Mobility service manually, or using a push installation from hello Site Recovery process server when replication is enabled, or using a tool such as System Center Configuration Manager.</span></span> <span data-ttu-id="50524-108">강제 설치를 사용 하는 경우 복제를 사용 하도록 설정 하면 hello 서비스는 hello 서버에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50524-108">If you use push installation, hello service is installed on hello server when you enable replication.</span></span>

<span data-ttu-id="50524-109">Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="50524-109">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="50524-110">수동 설치</span><span class="sxs-lookup"><span data-stu-id="50524-110">Install manually</span></span>

1. <span data-ttu-id="50524-111">Hello 확인 [필수 구성 요소](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) 수동 설치를 위한 합니다.</span><span class="sxs-lookup"><span data-stu-id="50524-111">Check hello [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="50524-112">에 따라 [이러한 지침](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) hello 포털을 사용 하 여 수동 설치에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="50524-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using hello portal.</span></span>
3. <span data-ttu-id="50524-113">Hello 명령줄에서 tooinstall를 선호 하는 경우에 따라 [이러한 지침](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)합니다.</span><span class="sxs-lookup"><span data-stu-id="50524-113">If you prefer tooinstall from hello command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-hello-process-server"></a><span data-ttu-id="50524-114">Hello 프로세스 서버에서 설치</span><span class="sxs-lookup"><span data-stu-id="50524-114">Install from hello process server</span></span>

<span data-ttu-id="50524-115">컴퓨터에서 복제를 사용 하도록 설정 하면 toopush hello hello 프로세스 서버에서 모바일 서비스를 설치 하려는 경우 hello 프로세스 서버 tooaccess hello 컴퓨터에서 사용할 수 있는 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="50524-115">If you want toopush hello Mobility service installation from hello process server when you enable replication for a machine, you need an account that can be used by hello process server tooaccess hello machine.</span></span> <span data-ttu-id="50524-116">hello 계정 hello 강제 설치에만 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50524-116">hello account is only used for hello push installation.</span></span>

1. <span data-ttu-id="50524-117">계정이 생성되지 않은 경우 다음 지침에 따라 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="50524-117">If you haven't created an account, do so using these guidelines:</span></span>

    - <span data-ttu-id="50524-118">도메인 또는 로컬 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50524-118">You can use a domain or local account</span></span>
    - <span data-ttu-id="50524-119">Windows 도메인 계정을 사용 하지 않는 경우 필요 toodisable hello 로컬 컴퓨터에 원격 사용자 액세스 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="50524-119">For Windows, if you're not using a domain account, you need toodisable Remote User Access control on hello local machine.</span></span> <span data-ttu-id="50524-120">이 hello에 등록할 toodo **찾아**, hello DWORD 항목을 추가 **LocalAccountTokenFilterPolicy**, 값이 1 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="50524-120">toodo this, in hello register under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, add hello DWORD entry **LocalAccountTokenFilterPolicy**, with a value of 1.</span></span>
    - <span data-ttu-id="50524-121">Windows에서 CLI tooadd hello 레지스트리 항목을 하려는 경우 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="50524-121">If you want tooadd hello registry entry for Windows from a CLI, type:</span></span>

        ```
        REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.
        ```

    - <span data-ttu-id="50524-122">Linux 용 hello 계정은 hello 원본 Linux 서버에 루트 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="50524-122">For Linux, hello account should be root on hello source Linux server.</span></span>

2. <span data-ttu-id="50524-123">다음에 따라 [이러한 지침](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) toopush Windows 또는 Linux를 실행 하는 Vm에서 모바일 서비스를 hello 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="50524-123">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want toopush hello Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-installation-methods"></a><span data-ttu-id="50524-124">다른 설치 방법</span><span class="sxs-lookup"><span data-stu-id="50524-124">Other installation methods</span></span>

- <span data-ttu-id="50524-125">[에 대 한 자세한 내용은](site-recovery-install-mobility-service-using-sccm.md) Configuration Manager를 사용 하 여 hello 이동성 서비스를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="50524-125">[Learn about](site-recovery-install-mobility-service-using-sccm.md) installing hello Mobility service using Configuration Manager</span></span>
- <span data-ttu-id="50524-126">Azure Automation DSC로 설치에 대해 [자세히 알아보기](site-recovery-automate-mobility-service-install.md)</span><span class="sxs-lookup"><span data-stu-id="50524-126">[Learn about](site-recovery-automate-mobility-service-install.md) installing with Azure Automation DSC.</span></span>


## <a name="next-steps"></a><span data-ttu-id="50524-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="50524-127">Next steps</span></span>

<span data-ttu-id="50524-128">너무 이동[10 단계: 복제 사용](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="50524-128">Go too[Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>
