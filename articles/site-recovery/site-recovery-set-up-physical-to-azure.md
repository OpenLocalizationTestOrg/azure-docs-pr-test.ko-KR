---
title: "원본 환경 설정(Azure에 대한 물리적 서버) | Microsoft Docs"
description: "이 문서에서는 온-프레미스 환경을 설정하여 Windows 또는 Linux를 실행 중인 물리적 서버를 Azure에 복제하기 시작하는 방법을 설명합니다."
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
ms.openlocfilehash: 49b9d2e21dbcb612828a25f21ed4382327d6f64c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-the-source-environment-physical-server-to-azure"></a><span data-ttu-id="19f2b-103">원본 환경 설정(Azure에 대한 물리적 서버)</span><span class="sxs-lookup"><span data-stu-id="19f2b-103">Set up the source environment (physical server to Azure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="19f2b-104">VMware에서 Azure로</span><span class="sxs-lookup"><span data-stu-id="19f2b-104">VMware to Azure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="19f2b-105">물리적 서버에서 Azure로</span><span class="sxs-lookup"><span data-stu-id="19f2b-105">Physical to Azure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="19f2b-106">이 문서에서는 온-프레미스 환경을 설정하여 Windows 또는 Linux를 실행 중인 물리적 서버를 Azure에 복제하기 시작하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="19f2b-106">This article describes how to set up your on-premises environment to start replicating physical servers running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19f2b-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="19f2b-107">Prerequisites</span></span>

<span data-ttu-id="19f2b-108">이 문서에서는 사용자가 다음 항목을 이미 가지고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="19f2b-108">The article assumes that you already have:</span></span>
1. <span data-ttu-id="19f2b-109">[Azure Portal](http://portal.azure.com "Azure Portal")의 Recovery Services 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="19f2b-109">A Recovery Services vault in the [Azure portal](http://portal.azure.com "Azure portal").</span></span>
3. <span data-ttu-id="19f2b-110">구성 서버를 설치할 물리적 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="19f2b-110">A physical computer on which to install the configuration server.</span></span>

### <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="19f2b-111">구성 서버 최소 요구 사항</span><span class="sxs-lookup"><span data-stu-id="19f2b-111">Configuration server minimum requirements</span></span>
<span data-ttu-id="19f2b-112">다음 테이블에는 구성 서버에 대한 최소 하드웨어, 소프트웨어 및 네트워크 요구 사항이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19f2b-112">The following table lists the minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="19f2b-113">HTTPS 기반 프록시 서버는 구성 서버에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19f2b-113">HTTPS-based proxy servers are not supported by the configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="19f2b-114">보호 목표 선택</span><span class="sxs-lookup"><span data-stu-id="19f2b-114">Choose your protection goals</span></span>

1. <span data-ttu-id="19f2b-115">Azure Portal에서 **Recovery Services** 자격 증명 모음 블레이드로 이동한 후 사용자 자격 증명 모음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="19f2b-115">In the Azure portal, go to the **Recovery Services** vaults blade and select your vault.</span></span>
2. <span data-ttu-id="19f2b-116">자격 증명 모음의 **리소스** 메뉴에서 **시작** > **Site Recovery** > **1단계: 인프라 준비** > **보호 목표**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19f2b-116">In the **Resource** menu of the vault, click **Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![목표 선택](./media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. <span data-ttu-id="19f2b-118">**보호 목표**에서 **Azure에**를 선택하고 **가상화되지 않음/기타**를 선택한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19f2b-118">In **Protection goal**, select **To Azure** and **Not virtualized/Other**, and then click **OK**.</span></span>

    ![목표 선택](./media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-the-source-environment"></a><span data-ttu-id="19f2b-120">원본 환경 설정</span><span class="sxs-lookup"><span data-stu-id="19f2b-120">Set up the source environment</span></span>

1. <span data-ttu-id="19f2b-121">**원본 준비**에서 구성 서버가 없는 경우 **+구성 서버**를 클릭하여 하나를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="19f2b-121">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** to add one.</span></span>

  ![원본 설정](./media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. <span data-ttu-id="19f2b-123">**서버 추가** 블레이드에서 **구성 서버**가 **서버 형식**에 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="19f2b-123">In the **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="19f2b-124">Site Recovery 통합 설치 프로그램 설치 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="19f2b-124">Download the Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="19f2b-125">자격 증명 모음 등록 키를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="19f2b-125">Download the vault registration key.</span></span> <span data-ttu-id="19f2b-126">통합 설치 프로그램을 실행하는 경우 등록 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="19f2b-126">You need the registration key when you run Unified Setup.</span></span> <span data-ttu-id="19f2b-127">이 키는 생성된 날로부터 5일간 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="19f2b-127">The key is valid for five days after you generate it.</span></span>

    ![원본 설정](./media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. <span data-ttu-id="19f2b-129">구성 서버로 사용 중인 컴퓨터에서 **Azure Site Recovery 통합 설치 프로그램**을 실행하여 구성 서버, 프로세스 서버 및 마스터 대상 서버를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="19f2b-129">On the machine you’re using as the configuration server, run **Azure Site Recovery Unified Setup** to install the configuration server, the process server, and the master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="19f2b-130">Azure Site Recovery 통합 설치 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="19f2b-130">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="19f2b-131">사용자 컴퓨터의 시스템 클록에서 시간이 현지 시간보다 5분 이상 차이가 날 경우 구성 서버 등록에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="19f2b-131">Configuration server registration fails if the time on your computer's system clock is more than five minutes off of local time.</span></span> <span data-ttu-id="19f2b-132">설치를 시작하기 전에 시스템 클록을 [시간 서버](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service)와 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="19f2b-132">Synchronize your system clock with a [time server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting the installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="19f2b-133">명령줄을 통해 구성 서버를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19f2b-133">The configuration server can be installed via a command line.</span></span> <span data-ttu-id="19f2b-134">자세한 내용은 [명령줄 도구를 사용하여 구성 서버 설치](http://aka.ms/installconfigsrv)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19f2b-134">For more information, see [Installing configuration server using command-line tools](http://aka.ms/installconfigsrv).</span></span>


## <a name="common-issues"></a><span data-ttu-id="19f2b-135">일반적인 문제</span><span class="sxs-lookup"><span data-stu-id="19f2b-135">Common issues</span></span>

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="19f2b-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="19f2b-136">Next steps</span></span>

<span data-ttu-id="19f2b-137">다음 단계는 Azure에서 [대상 환경 설정](./site-recovery-prepare-target-physical-to-azure.md)을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="19f2b-137">Next step involves [setting up your target environment](./site-recovery-prepare-target-physical-to-azure.md) in Azure.</span></span>
