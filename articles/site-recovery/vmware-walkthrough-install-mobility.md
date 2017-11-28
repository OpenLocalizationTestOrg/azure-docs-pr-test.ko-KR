---
title: "Azure 복제를 위해 VMware에 모바일 서비스 설치 | Microsoft Docs"
description: "이 문서에서는 Azure Site Recovery 서비스를 통해 Azure 복제를 위해 VMware에 모바일 서비스 에이전트를 설치하는 방법을 설명합니다."
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
ms.openlocfilehash: bc520bd2ea54208889861a7a3b275e3008a05d53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="step-10-install-the-mobility-service"></a><span data-ttu-id="4c16d-103">10단계: 모바일 서비스 설치</span><span class="sxs-lookup"><span data-stu-id="4c16d-103">Step 10: Install the Mobility service</span></span>


<span data-ttu-id="4c16d-104">이 문서에서는 Azure Portal에서 [Azure Site Recovery](site-recovery-overview.md) 서비스를 사용하여 Azure에 온-프레미스 VMware 가상 컴퓨터를 복제할 때 소스 및 대상 설정을 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4c16d-104">This article describes how to configure source and target settings when replicating on-premises VMware virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="4c16d-105">모바일 서비스는 컴퓨터에 기록된 데이터를 캡처하고 이를 프로세스 서버에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="4c16d-105">The Mobility service captures data writes on a machine, and forwards them to the process server.</span></span> <span data-ttu-id="4c16d-106">Azure에 복제하려는 각 컴퓨터에 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c16d-106">It should be installed on each machine that you want to replicate to Azure.</span></span>

<span data-ttu-id="4c16d-107">모바일 서비스는 복제가 설정된 경우 Site Recovery 프로세스 서버에서 푸시 설치를 사용하여 수동으로 설치하거나 System Center Configuration Manager 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c16d-107">You can install the Mobility service manual, using a push installation from the Site Recovery process server when replication is enabled, or use a tool System Center Configuration Manager.</span></span> <span data-ttu-id="4c16d-108">푸시 설치를 사용하는 경우 복제를 활성화할 때 VM에 서비스를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4c16d-108">If you use push installation, the service is installed on the VM when replication is enabled.</span></span>

<span data-ttu-id="4c16d-109">이 문서의 하단 또는 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 의견이나 질문을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="4c16d-109">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="4c16d-110">수동 설치</span><span class="sxs-lookup"><span data-stu-id="4c16d-110">Install manually</span></span>

1. <span data-ttu-id="4c16d-111">수동 설치를 위한 [필수 조건](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites)을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4c16d-111">Check the [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="4c16d-112">포털을 사용하여 수동 설치를 위한 [이러한 지침](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="4c16d-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using the portal.</span></span>
3. <span data-ttu-id="4c16d-113">명령줄에서 설치하는 것을 선호하는 경우 [이러한 지침](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="4c16d-113">If you prefer to install from the command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-the-process-server"></a><span data-ttu-id="4c16d-114">프로세스 서버에서 설치</span><span class="sxs-lookup"><span data-stu-id="4c16d-114">Install from the process server</span></span>

<span data-ttu-id="4c16d-115">VM에 대해 복제가 설정된 경우 프로세스 서버에서 모바일 서비스 설치를 푸시하려면 프로세스 서버에서 VM에 액세스하는 데 사용할 수 있는 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4c16d-115">If you want to push the Mobility service installation from the process server when you enable replication for a VM, you need an account that can be used by the process server to access the VM.</span></span> <span data-ttu-id="4c16d-116">이 계정은 푸시 설치에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c16d-116">The account is only used for the push installation.</span></span>

1. <span data-ttu-id="4c16d-117">푸시 설치에 사용할 수 있는 [계정을 만들](vmware-walkthrough-prepare-vmware.md)어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c16d-117">You should have [created an account](vmware-walkthrough-prepare-vmware.md) that can be used for push installation.</span></span> <span data-ttu-id="4c16d-118">그런 다음 Site Recovery 배포 중에 소스 설정을 구성할 때 사용할 계정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4c16d-118">You then specify the account you want to use when you configure source settings during Site Recovery deployment.</span></span>
2. <span data-ttu-id="4c16d-119">Windows 또는 Linux를 실행하는 VM에서 모바일 서비스를 푸시하는 경우 [이러한 지침](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="4c16d-119">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want to push the Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-methods"></a><span data-ttu-id="4c16d-120">다른 방법</span><span class="sxs-lookup"><span data-stu-id="4c16d-120">Other methods</span></span>

<span data-ttu-id="4c16d-121">[Configuration Manager 또는](site-recovery-install-mobility-service-using-sccm.md) [Azure Automation DSC](site-recovery-automate-mobility-service-install.md)를 사용하여 모바일 서비스를 설치하는 방법에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4c16d-121">Learn more about [installing the Mobility service using Configuration Manager](site-recovery-install-mobility-service-using-sccm.md), or using [Azure Automation DSC](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c16d-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4c16d-122">Next steps</span></span>

<span data-ttu-id="4c16d-123">[11단계: 복제 활성화](vmware-walkthrough-enable-replication.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4c16d-123">Go to [Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>
