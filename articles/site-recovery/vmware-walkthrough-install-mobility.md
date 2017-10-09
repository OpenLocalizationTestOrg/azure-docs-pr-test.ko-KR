---
title: "aaaInstall hello VMware tooAzure 복제에 대 한 모바일 서비스 | Microsoft Docs"
description: "이 문서에서는 tooinstall hello Azure Site Recovery 서비스와 VMware tooAzure 복제에 대 한 모바일 서비스 에이전트가 hello 하는 방법을 설명 합니다."
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
ms.openlocfilehash: d3b7bc9c4d84d13317e0b0b47adcf38e8c41d0bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-install-hello-mobility-service"></a><span data-ttu-id="1f401-103">10 단계: hello 모바일 서비스를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f401-103">Step 10: Install hello Mobility service</span></span>


<span data-ttu-id="1f401-104">이 문서에서는 어떻게 tooconfigure 원본 및 대상 설정을 복제할 때 온-프레미스 VMware 가상 컴퓨터 tooAzure hello를 사용 하 여 설명 [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="1f401-104">This article describes how tooconfigure source and target settings when replicating on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="1f401-105">hello 모바일 서비스는 컴퓨터에 데이터 쓰기를 캡처하고 toohello 프로세스 서버에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f401-105">hello Mobility service captures data writes on a machine, and forwards them toohello process server.</span></span> <span data-ttu-id="1f401-106">Tooreplicate tooAzure 하려는 각 컴퓨터에 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f401-106">It should be installed on each machine that you want tooreplicate tooAzure.</span></span>

<span data-ttu-id="1f401-107">복제를 사용 하는 경우 hello 사이트 복구 프로세스 서버에서 강제 설치를 사용 하 여 hello 모바일 서비스 설명서를 설치 하거나 System Center Configuration Manager 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f401-107">You can install hello Mobility service manual, using a push installation from hello Site Recovery process server when replication is enabled, or use a tool System Center Configuration Manager.</span></span> <span data-ttu-id="1f401-108">강제 설치를 사용 하는 경우 복제를 사용할 때 hello 서비스는 hello VM에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f401-108">If you use push installation, hello service is installed on hello VM when replication is enabled.</span></span>

<span data-ttu-id="1f401-109">Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f401-109">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="1f401-110">수동 설치</span><span class="sxs-lookup"><span data-stu-id="1f401-110">Install manually</span></span>

1. <span data-ttu-id="1f401-111">Hello 확인 [필수 구성 요소](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) 수동 설치를 위한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f401-111">Check hello [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="1f401-112">에 따라 [이러한 지침](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) hello 포털을 사용 하 여 수동 설치에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f401-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using hello portal.</span></span>
3. <span data-ttu-id="1f401-113">Hello 명령줄에서 tooinstall를 선호 하는 경우에 따라 [이러한 지침](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f401-113">If you prefer tooinstall from hello command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-hello-process-server"></a><span data-ttu-id="1f401-114">Hello 프로세스 서버에서 설치</span><span class="sxs-lookup"><span data-stu-id="1f401-114">Install from hello process server</span></span>

<span data-ttu-id="1f401-115">VM에 대 한 복제를 사용 하도록 설정 하면 hello 프로세스 서버에서 toopush hello 모바일 서비스 설치를 수행 하는 경우에 hello 프로세스 서버 tooaccess hello VM에서 사용할 수 있는 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f401-115">If you want toopush hello Mobility service installation from hello process server when you enable replication for a VM, you need an account that can be used by hello process server tooaccess hello VM.</span></span> <span data-ttu-id="1f401-116">hello 계정 hello 강제 설치에만 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f401-116">hello account is only used for hello push installation.</span></span>

1. <span data-ttu-id="1f401-117">푸시 설치에 사용할 수 있는 [계정을 만들](vmware-walkthrough-prepare-vmware.md)어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f401-117">You should have [created an account](vmware-walkthrough-prepare-vmware.md) that can be used for push installation.</span></span> <span data-ttu-id="1f401-118">그런 다음 사이트 복구 배포 하는 동안 원본 설정을 구성할 때 원하는 toouse hello 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f401-118">You then specify hello account you want toouse when you configure source settings during Site Recovery deployment.</span></span>
2. <span data-ttu-id="1f401-119">다음에 따라 [이러한 지침](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) toopush Windows 또는 Linux를 실행 하는 Vm에서 모바일 서비스를 hello 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="1f401-119">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want toopush hello Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-methods"></a><span data-ttu-id="1f401-120">다른 방법</span><span class="sxs-lookup"><span data-stu-id="1f401-120">Other methods</span></span>

<span data-ttu-id="1f401-121">에 대 한 자세한 내용은 [Configuration Manager를 사용 하 여 hello 모바일 서비스를 설치](site-recovery-install-mobility-service-using-sccm.md)를 사용 하 여 또는 [Azure 자동화 DSC](site-recovery-automate-mobility-service-install.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f401-121">Learn more about [installing hello Mobility service using Configuration Manager](site-recovery-install-mobility-service-using-sccm.md), or using [Azure Automation DSC](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f401-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1f401-122">Next steps</span></span>

<span data-ttu-id="1f401-123">너무 이동[11 단계: 복제 사용](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="1f401-123">Go too[Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>
