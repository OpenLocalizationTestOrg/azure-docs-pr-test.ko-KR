---
title: "원본 환경 설정(Azure-VMware) | Microsoft Docs"
description: "이 문서에서는 온-프레미스 환경을 설정하여 VMware 가상 컴퓨터를 Azure에 복제하기 시작하는 방법을 설명합니다."
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
ms.openlocfilehash: a2fabc56463c8cbf0b8a76b7a84369ed8e535486
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="set-up-the-source-environment-vmware-to-azure"></a><span data-ttu-id="cfaf2-103">원본 환경 설정(Azure-VMware)</span><span class="sxs-lookup"><span data-stu-id="cfaf2-103">Set up the source environment (VMware to Azure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cfaf2-104">VMware에서 Azure로</span><span class="sxs-lookup"><span data-stu-id="cfaf2-104">VMware to Azure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="cfaf2-105">물리적 서버에서 Azure로</span><span class="sxs-lookup"><span data-stu-id="cfaf2-105">Physical to Azure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="cfaf2-106">이 문서에서는 온-프레미스 환경을 설정하여 VMware에서 실행 중인 가상 컴퓨터를 Azure에 복제하기 시작하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cfaf2-106">This article describes how to set up your on-premises environment to start replicating virtual machines running on VMware to Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cfaf2-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="cfaf2-107">Prerequisites</span></span>

<span data-ttu-id="cfaf2-108">이 문서에서는 사용자가 다음 항목을 이미 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="cfaf2-108">The article assumes that you have already created:</span></span>
- <span data-ttu-id="cfaf2-109">[Azure Portal](http://portal.azure.com "Azure Portal")의 Recovery Services 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="cfaf2-109">A Recovery Services Vault in the [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="cfaf2-110">[자동 검색](./site-recovery-vmware-to-azure.md)에 사용할 수 있는 VMware vCenter의 전용 계정</span><span class="sxs-lookup"><span data-stu-id="cfaf2-110">A dedicated account in your VMware vCenter that can be used for [automatic discovery](./site-recovery-vmware-to-azure.md).</span></span>
- <span data-ttu-id="cfaf2-111">구성 서버를 설치할 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="cfaf2-111">A virtual machine on which to install the configuration server.</span></span>

## <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="cfaf2-112">구성 서버 최소 요구 사항</span><span class="sxs-lookup"><span data-stu-id="cfaf2-112">Configuration server minimum requirements</span></span>
<span data-ttu-id="cfaf2-113">항상 사용 가능한 VMware 가상 컴퓨터에 구성 서버 소프트웨어를 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfaf2-113">The configuration server software should be deployed on a highly available VMware virtual machine.</span></span> <span data-ttu-id="cfaf2-114">다음 표에는 구성 서버에 대한 최소 하드웨어, 소프트웨어 및 네트워크 요구 사항이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfaf2-114">The following table lists the minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="cfaf2-115">HTTPS 기반 프록시 서버는 구성 서버에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cfaf2-115">HTTPS-based proxy servers are not supported by the configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="cfaf2-116">보호 목표 선택</span><span class="sxs-lookup"><span data-stu-id="cfaf2-116">Choose your protection goals</span></span>

1. <span data-ttu-id="cfaf2-117">Azure Portal에서 **Recovery Services** 자격 증명 모음 블레이드로 이동한 후 사용자 자격 증명 모음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cfaf2-117">In the Azure portal, go to the **Recovery Services** vault blade and select your vault.</span></span>
2. <span data-ttu-id="cfaf2-118">자격 증명 모음의 리소스 메뉴에서 **시작** > **Site Recovery** > **1단계: 인프라 준비** > **보호 목표**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="cfaf2-118">On the resource menu of the vault, go to **Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![목표 선택](./media/site-recovery-set-up-vmware-to-azure/choose-goals.png)
3. <span data-ttu-id="cfaf2-120">**보호 목표**에서 **Azure에**를 선택하고 **예, VMware vSphere 하이퍼바이저 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cfaf2-120">In **Protection goal**, select **To Azure**, and choose **Yes, with VMware vSphere Hypervisor**.</span></span> <span data-ttu-id="cfaf2-121">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cfaf2-121">Then click **OK**.</span></span>

    ![목표 선택](./media/site-recovery-set-up-vmware-to-azure/choose-goals2.png)

## <a name="set-up-the-source-environment"></a><span data-ttu-id="cfaf2-123">원본 환경 설정</span><span class="sxs-lookup"><span data-stu-id="cfaf2-123">Set up the source environment</span></span>
<span data-ttu-id="cfaf2-124">두 가지 주요 작업을 포함한 원본 환경 설정</span><span class="sxs-lookup"><span data-stu-id="cfaf2-124">Setting up the source environment involves two main activities:</span></span>

- <span data-ttu-id="cfaf2-125">Site Recovery를 사용하여 구성 서버를 설치 및 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="cfaf2-125">Install and register a configuration server with Site Recovery.</span></span>
- <span data-ttu-id="cfaf2-126">Site Recovery를 온-프레미스 VMware vCenter 또는 vSphere EXSi 호스트에 연결하여 온-프레미스 가상 컴퓨터를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="cfaf2-126">Discover your on-premises virtual machines by connecting Site Recovery to your on-premises VMware vCenter or vSphere EXSi hosts.</span></span>

### <a name="step-1-install-and-register-a-configuration-server"></a><span data-ttu-id="cfaf2-127">1단계: 구성 서버 설치 및 등록</span><span class="sxs-lookup"><span data-stu-id="cfaf2-127">Step 1: Install and register a configuration server</span></span>

1. <span data-ttu-id="cfaf2-128">**1단계: 인프라 준비** > **원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cfaf2-128">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span> <span data-ttu-id="cfaf2-129">**원본 준비**에서 구성 서버가 없는 경우 **+구성 서버**를 클릭하여 하나를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cfaf2-129">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** to add one.</span></span>

    ![원본 설정](./media/site-recovery-set-up-vmware-to-azure/set-source1.png)
2. <span data-ttu-id="cfaf2-131">**서버 추가** 블레이드에서 **구성 서버**가 **서버 형식**에 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cfaf2-131">On the **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="cfaf2-132">Site Recovery 통합 설치 프로그램 설치 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="cfaf2-132">Download the Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="cfaf2-133">자격 증명 모음 등록 키를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="cfaf2-133">Download the vault registration key.</span></span> <span data-ttu-id="cfaf2-134">통합 설치 프로그램을 실행하는 경우 등록 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cfaf2-134">You need the registration key when you run Unified Setup.</span></span> <span data-ttu-id="cfaf2-135">이 키는 생성된 날로부터 5일간 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="cfaf2-135">The key is valid for five days after you generate it.</span></span>

    ![원본 설정](./media/site-recovery-set-up-vmware-to-azure/set-source2.png)
6. <span data-ttu-id="cfaf2-137">구성 서버로 사용 중인 컴퓨터에서 **Azure Site Recovery 통합 설치 프로그램**을 실행하여 구성 서버, 프로세스 서버 및 마스터 대상 서버를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cfaf2-137">On the machine you’re using as the configuration server, run **Azure Site Recovery Unified Setup** to install the configuration server, the process server, and the master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="cfaf2-138">Azure Site Recovery 통합 설치 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="cfaf2-138">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="cfaf2-139">사용자 컴퓨터 시스템 클록의 시간이 현지 시간보다 5분 이상 차이가 날 경우 구성 서버 등록에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="cfaf2-139">Configuration server registration fails if the time on your computer's system clock differs from local time by more than five minutes.</span></span> <span data-ttu-id="cfaf2-140">설치를 시작하기 전에 시스템 클록을 [시간 서버](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service)와 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="cfaf2-140">Synchronize your system clock with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting the installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="cfaf2-141">명령줄을 통해 구성 서버를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfaf2-141">The configuration server can be installed via command line.</span></span> <span data-ttu-id="cfaf2-142">자세한 내용은 [명령줄 도구를 사용하여 구성 서버 설치](http://aka.ms/installconfigsrv)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cfaf2-142">For more information, see [Installing the configuration server using Command-line tools](http://aka.ms/installconfigsrv).</span></span>

#### <a name="add-the-vmware-account-for-automatic-discovery"></a><span data-ttu-id="cfaf2-143">자동 검색에 VMware 계정 추가</span><span class="sxs-lookup"><span data-stu-id="cfaf2-143">Add the VMware account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="step-2-add-a-vcenter"></a><span data-ttu-id="cfaf2-144">2단계: vCenter 추가</span><span class="sxs-lookup"><span data-stu-id="cfaf2-144">Step 2: Add a vCenter</span></span>
<span data-ttu-id="cfaf2-145">Azure Site Recovery가 온-프레미스 환경에서 실행 중인 가상 컴퓨터를 검색할 수 있게 하려면 Site Recovery와 VMware vCenter 서버 또는 vSphere ESXi 호스트를 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfaf2-145">To allow Azure Site Recovery to discover virtual machines running in your on-premises environment, you need to connect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span>

<span data-ttu-id="cfaf2-146">**+vCenter**를 선택하여 VMware vCenter 서버 또는 VMware vSphere ESXi 호스트를 연결하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cfaf2-146">Select **+vCenter** to start connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]


## <a name="common-issues"></a><span data-ttu-id="cfaf2-147">일반적인 문제</span><span class="sxs-lookup"><span data-stu-id="cfaf2-147">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="cfaf2-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cfaf2-148">Next steps</span></span>
<span data-ttu-id="cfaf2-149">Azure에서 [대상 환경 설정](./site-recovery-prepare-target-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="cfaf2-149">[Set up your target environment](./site-recovery-prepare-target-vmware-to-azure.md) in Azure.</span></span>
