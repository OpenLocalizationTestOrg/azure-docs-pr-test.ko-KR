---
title: "(VMware tooAzure) hello 소스 환경 설정 | Microsoft Docs"
description: "이 문서에서는 VMware 가상 복제 하 여 온-프레미스 환경 toostart tooset tooAzure 컴퓨터 하는 방법을 설명 합니다."
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
ms.openlocfilehash: cbeeffc1061b11223e12ff3e237fa7e55b999aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-vmware-tooazure"></a><span data-ttu-id="2cbdf-103">Hello 소스 환경 (VMware tooAzure) 설정</span><span class="sxs-lookup"><span data-stu-id="2cbdf-103">Set up hello source environment (VMware tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2cbdf-104">VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="2cbdf-104">VMware tooAzure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="2cbdf-105">물리적 tooAzure</span><span class="sxs-lookup"><span data-stu-id="2cbdf-105">Physical tooAzure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="2cbdf-106">이 문서에서는 tooset 가상 복제 하 여 온-프레미스 환경 toostart 컴퓨터의 실행 방법을 설명 VMware tooAzure에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cbdf-106">This article describes how tooset up your on-premises environment toostart replicating virtual machines running on VMware tooAzure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2cbdf-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2cbdf-107">Prerequisites</span></span>

<span data-ttu-id="2cbdf-108">hello 문서에서는 이미 만들었다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cbdf-108">hello article assumes that you have already created:</span></span>
- <span data-ttu-id="2cbdf-109">Hello에 복구 서비스 자격 증명 모음 [Azure 포털](http://portal.azure.com "Azure 포털")합니다.</span><span class="sxs-lookup"><span data-stu-id="2cbdf-109">A Recovery Services Vault in hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="2cbdf-110">[자동 검색](./site-recovery-vmware-to-azure.md)에 사용할 수 있는 VMware vCenter의 전용 계정</span><span class="sxs-lookup"><span data-stu-id="2cbdf-110">A dedicated account in your VMware vCenter that can be used for [automatic discovery](./site-recovery-vmware-to-azure.md).</span></span>
- <span data-ttu-id="2cbdf-111">Tooinstall hello 구성 서버에서 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="2cbdf-111">A virtual machine on which tooinstall hello configuration server.</span></span>

## <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="2cbdf-112">구성 서버 최소 요구 사항</span><span class="sxs-lookup"><span data-stu-id="2cbdf-112">Configuration server minimum requirements</span></span>
<span data-ttu-id="2cbdf-113">hello 구성 서버 소프트웨어는 항상 사용 가능한 VMware 가상 컴퓨터에 배포 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cbdf-113">hello configuration server software should be deployed on a highly available VMware virtual machine.</span></span> <span data-ttu-id="2cbdf-114">다음 표에서 hello hello 최소 하드웨어, 소프트웨어 및 구성 서버에 대 한 네트워크 요구 사항을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cbdf-114">hello following table lists hello minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="2cbdf-115">HTTPS 기반 프록시 서버 hello 구성 서버에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2cbdf-115">HTTPS-based proxy servers are not supported by hello configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="2cbdf-116">보호 목표 선택</span><span class="sxs-lookup"><span data-stu-id="2cbdf-116">Choose your protection goals</span></span>

1. <span data-ttu-id="2cbdf-117">Hello Azure 포털에서에서 toohello 이동 **복구 서비스** 블레이드를 자격 증명 모음 및 자격 증명 모음을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cbdf-117">In hello Azure portal, go toohello **Recovery Services** vault blade and select your vault.</span></span>
2. <span data-ttu-id="2cbdf-118">Hello 자격 증명 모음의 hello 리소스 메뉴에서 이동 너무**시작** > **사이트 복구** > **1 단계: 인프라 준비**  >  **보호 목표**합니다.</span><span class="sxs-lookup"><span data-stu-id="2cbdf-118">On hello resource menu of hello vault, go too**Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![목표 선택](./media/site-recovery-set-up-vmware-to-azure/choose-goals.png)
3. <span data-ttu-id="2cbdf-120">**보호 목표**선택, **tooAzure**, 선택 **VMware vSphere 하이퍼바이저와 예,**합니다.</span><span class="sxs-lookup"><span data-stu-id="2cbdf-120">In **Protection goal**, select **tooAzure**, and choose **Yes, with VMware vSphere Hypervisor**.</span></span> <span data-ttu-id="2cbdf-121">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2cbdf-121">Then click **OK**.</span></span>

    ![목표 선택](./media/site-recovery-set-up-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a><span data-ttu-id="2cbdf-123">Hello 소스 환경 설정</span><span class="sxs-lookup"><span data-stu-id="2cbdf-123">Set up hello source environment</span></span>
<span data-ttu-id="2cbdf-124">Hello 소스 환경 설정 두 가지 주요 작업이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2cbdf-124">Setting up hello source environment involves two main activities:</span></span>

- <span data-ttu-id="2cbdf-125">Site Recovery를 사용하여 구성 서버를 설치 및 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="2cbdf-125">Install and register a configuration server with Site Recovery.</span></span>
- <span data-ttu-id="2cbdf-126">사이트 복구 tooyour 온-프레미스 VMware vCenter 또는 vSphere EXSi 호스트를 연결 하 여 온-프레미스 가상 컴퓨터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cbdf-126">Discover your on-premises virtual machines by connecting Site Recovery tooyour on-premises VMware vCenter or vSphere EXSi hosts.</span></span>

### <a name="step-1-install-and-register-a-configuration-server"></a><span data-ttu-id="2cbdf-127">1단계: 구성 서버 설치 및 등록</span><span class="sxs-lookup"><span data-stu-id="2cbdf-127">Step 1: Install and register a configuration server</span></span>

1. <span data-ttu-id="2cbdf-128">**1단계: 인프라 준비** > **원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2cbdf-128">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span> <span data-ttu-id="2cbdf-129">**준비 소스**클릭 하 여 구성 서버, 없는 경우, **구성 서버 +** tooadd 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="2cbdf-129">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** tooadd one.</span></span>

    ![원본 설정](./media/site-recovery-set-up-vmware-to-azure/set-source1.png)
2. <span data-ttu-id="2cbdf-131">Hello에 **서버 추가** 블레이드를 확인 하는 **구성 서버** 에 표시 **서버 유형**합니다.</span><span class="sxs-lookup"><span data-stu-id="2cbdf-131">On hello **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="2cbdf-132">Hello Site Recovery 통합 설치 설치 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cbdf-132">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="2cbdf-133">Hello 자격 증명 모음 등록 키를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cbdf-133">Download hello vault registration key.</span></span> <span data-ttu-id="2cbdf-134">통합 설치를 실행할 때 hello 등록 키가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cbdf-134">You need hello registration key when you run Unified Setup.</span></span> <span data-ttu-id="2cbdf-135">hello 키가 생성 한 후 5 일 동안 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cbdf-135">hello key is valid for five days after you generate it.</span></span>

    ![원본 설정](./media/site-recovery-set-up-vmware-to-azure/set-source2.png)
6. <span data-ttu-id="2cbdf-137">Hello 구성 서버를 사용 하는 hello 컴퓨터에서 실행 **Azure Site Recovery 통합 설치** tooinstall hello 구성 서버, 프로세스 서버 hello 및 hello 마스터 대상 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="2cbdf-137">On hello machine you’re using as hello configuration server, run **Azure Site Recovery Unified Setup** tooinstall hello configuration server, hello process server, and hello master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="2cbdf-138">Azure Site Recovery 통합 설치 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="2cbdf-138">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="2cbdf-139">컴퓨터의 시스템 시계에 hello 시간이 현지 시간에서 5 분 이상 차이가 날 구성 서버 등록에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cbdf-139">Configuration server registration fails if hello time on your computer's system clock differs from local time by more than five minutes.</span></span> <span data-ttu-id="2cbdf-140">시스템 시계와 동기화 한 [시간 서버](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) hello 설치를 시작 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="2cbdf-140">Synchronize your system clock with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting hello installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="2cbdf-141">명령줄을 통해 hello 구성 서버를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cbdf-141">hello configuration server can be installed via command line.</span></span> <span data-ttu-id="2cbdf-142">자세한 내용은 참조 [명령줄 도구를 사용 하 여 설치 hello 구성 서버](http://aka.ms/installconfigsrv)합니다.</span><span class="sxs-lookup"><span data-stu-id="2cbdf-142">For more information, see [Installing hello configuration server using Command-line tools](http://aka.ms/installconfigsrv).</span></span>

#### <a name="add-hello-vmware-account-for-automatic-discovery"></a><span data-ttu-id="2cbdf-143">자동 검색에 대 한 hello VMware 계정 추가</span><span class="sxs-lookup"><span data-stu-id="2cbdf-143">Add hello VMware account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="step-2-add-a-vcenter"></a><span data-ttu-id="2cbdf-144">2단계: vCenter 추가</span><span class="sxs-lookup"><span data-stu-id="2cbdf-144">Step 2: Add a vCenter</span></span>
<span data-ttu-id="2cbdf-145">tooallow Azure Site Recovery toodiscover 가상 컴퓨터 사용자의 온-프레미스 환경에서 실행 해야 tooconnect VMware vCenter Server 또는 사이트 복구와 vSphere ESXi 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cbdf-145">tooallow Azure Site Recovery toodiscover virtual machines running in your on-premises environment, you need tooconnect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span>

<span data-ttu-id="2cbdf-146">선택 **+ vCenter** toostart VMware vCenter server 또는 VMware vSphere ESXi 호스트를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cbdf-146">Select **+vCenter** toostart connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]


## <a name="common-issues"></a><span data-ttu-id="2cbdf-147">일반적인 문제</span><span class="sxs-lookup"><span data-stu-id="2cbdf-147">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="2cbdf-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2cbdf-148">Next steps</span></span>
<span data-ttu-id="2cbdf-149">Azure에서 [대상 환경 설정](./site-recovery-prepare-target-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="2cbdf-149">[Set up your target environment](./site-recovery-prepare-target-vmware-to-azure.md) in Azure.</span></span>
