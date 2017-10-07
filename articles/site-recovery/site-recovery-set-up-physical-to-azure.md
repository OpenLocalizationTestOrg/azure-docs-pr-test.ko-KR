---
title: "(실제 서버 tooAzure) hello 소스 환경 설정 | Microsoft Docs"
description: "이 문서에서는 설명 어떻게를 Azure에 Windows 또는 Linux를 실행 하는 물리적 서버를 복제 하 여 온-프레미스 환경 toostart tooset 합니다."
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
ms.openlocfilehash: d4702265bf36910015685d2bba99d6e577531bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-physical-server-tooazure"></a><span data-ttu-id="074fb-103">Hello 소스 환경 (실제 서버 tooAzure) 설정</span><span class="sxs-lookup"><span data-stu-id="074fb-103">Set up hello source environment (physical server tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="074fb-104">VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="074fb-104">VMware tooAzure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="074fb-105">물리적 tooAzure</span><span class="sxs-lookup"><span data-stu-id="074fb-105">Physical tooAzure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="074fb-106">이 문서에서는 설명 어떻게를 Azure에 Windows 또는 Linux를 실행 하는 물리적 서버를 복제 하 여 온-프레미스 환경 toostart tooset 합니다.</span><span class="sxs-lookup"><span data-stu-id="074fb-106">This article describes how tooset up your on-premises environment toostart replicating physical servers running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="074fb-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="074fb-107">Prerequisites</span></span>

<span data-ttu-id="074fb-108">hello 문서에서는 이미 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="074fb-108">hello article assumes that you already have:</span></span>
1. <span data-ttu-id="074fb-109">Hello에 복구 서비스 자격 증명 모음 [Azure 포털](http://portal.azure.com "Azure 포털")합니다.</span><span class="sxs-lookup"><span data-stu-id="074fb-109">A Recovery Services vault in hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
3. <span data-ttu-id="074fb-110">Tooinstall hello 구성 서버에서 물리적 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="074fb-110">A physical computer on which tooinstall hello configuration server.</span></span>

### <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="074fb-111">구성 서버 최소 요구 사항</span><span class="sxs-lookup"><span data-stu-id="074fb-111">Configuration server minimum requirements</span></span>
<span data-ttu-id="074fb-112">다음 표에서 hello hello 최소 하드웨어, 소프트웨어 및 구성 서버에 대 한 네트워크 요구 사항을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="074fb-112">hello following table lists hello minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="074fb-113">HTTPS 기반 프록시 서버 hello 구성 서버에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="074fb-113">HTTPS-based proxy servers are not supported by hello configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="074fb-114">보호 목표 선택</span><span class="sxs-lookup"><span data-stu-id="074fb-114">Choose your protection goals</span></span>

1. <span data-ttu-id="074fb-115">Hello Azure 포털에서에서 toohello 이동 **복구 서비스** 블레이드를 자격 증명 모음 및 자격 증명 모음을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="074fb-115">In hello Azure portal, go toohello **Recovery Services** vaults blade and select your vault.</span></span>
2. <span data-ttu-id="074fb-116">Hello에 **리소스** hello 자격 증명 모음의 메뉴 클릭 **시작** > **사이트 복구** > **1 단계: 준비 인프라** > **보호 목표**합니다.</span><span class="sxs-lookup"><span data-stu-id="074fb-116">In hello **Resource** menu of hello vault, click **Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![목표 선택](./media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. <span data-ttu-id="074fb-118">**보호 목표**선택, **tooAzure** 및 **하지 가상화 된/기타**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="074fb-118">In **Protection goal**, select **tooAzure** and **Not virtualized/Other**, and then click **OK**.</span></span>

    ![목표 선택](./media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-hello-source-environment"></a><span data-ttu-id="074fb-120">Hello 소스 환경 설정</span><span class="sxs-lookup"><span data-stu-id="074fb-120">Set up hello source environment</span></span>

1. <span data-ttu-id="074fb-121">**준비 소스**클릭 하 여 구성 서버, 없는 경우, **구성 서버 +** tooadd 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="074fb-121">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** tooadd one.</span></span>

  ![원본 설정](./media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. <span data-ttu-id="074fb-123">Hello에 **서버 추가** 블레이드에서 있는지 여부를 확인 **구성 서버** 에 표시 **서버 유형**합니다.</span><span class="sxs-lookup"><span data-stu-id="074fb-123">In hello **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="074fb-124">Hello Site Recovery 통합 설치 설치 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="074fb-124">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="074fb-125">Hello 자격 증명 모음 등록 키를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="074fb-125">Download hello vault registration key.</span></span> <span data-ttu-id="074fb-126">통합 설치를 실행할 때 hello 등록 키가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="074fb-126">You need hello registration key when you run Unified Setup.</span></span> <span data-ttu-id="074fb-127">hello 키가 생성 한 후 5 일 동안 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="074fb-127">hello key is valid for five days after you generate it.</span></span>

    ![원본 설정](./media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. <span data-ttu-id="074fb-129">Hello 구성 서버를 사용 하는 hello 컴퓨터에서 실행 **Azure Site Recovery 통합 설치** tooinstall hello 구성 서버, 프로세스 서버 hello 및 hello 마스터 대상 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="074fb-129">On hello machine you’re using as hello configuration server, run **Azure Site Recovery Unified Setup** tooinstall hello configuration server, hello process server, and hello master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="074fb-130">Azure Site Recovery 통합 설치 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="074fb-130">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="074fb-131">컴퓨터의 시스템 시계에 hello 시간은 현지 시간에서 5 분 넘게 구성 서버 등록 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="074fb-131">Configuration server registration fails if hello time on your computer's system clock is more than five minutes off of local time.</span></span> <span data-ttu-id="074fb-132">시스템 시계와 동기화 한 [시간 서버](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) hello 설치를 시작 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="074fb-132">Synchronize your system clock with a [time server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting hello installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="074fb-133">명령줄을 통해 hello 구성 서버를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="074fb-133">hello configuration server can be installed via a command line.</span></span> <span data-ttu-id="074fb-134">자세한 내용은 [명령줄 도구를 사용하여 구성 서버 설치](http://aka.ms/installconfigsrv)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="074fb-134">For more information, see [Installing configuration server using command-line tools](http://aka.ms/installconfigsrv).</span></span>


## <a name="common-issues"></a><span data-ttu-id="074fb-135">일반적인 문제</span><span class="sxs-lookup"><span data-stu-id="074fb-135">Common issues</span></span>

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="074fb-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="074fb-136">Next steps</span></span>

<span data-ttu-id="074fb-137">다음 단계는 Azure에서 [대상 환경 설정](./site-recovery-prepare-target-physical-to-azure.md)을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="074fb-137">Next step involves [setting up your target environment](./site-recovery-prepare-target-physical-to-azure.md) in Azure.</span></span>
