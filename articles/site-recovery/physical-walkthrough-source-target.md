---
title: "Azure Site Recovery를 사용하여 Azure에 물리적 서버 복제를 위한 원본 및 대상 설정 | Microsoft Docs"
description: "Azure Site Recovery 서비스를 사용하여 Azure Storage에 물리적 서버의 복제를 위한 원본 및 대상 설정을 수행하는 단계를 요약합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 2e3d03bc-4e53-4590-8a01-f702d3cc9500
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: e89bbf5a2c1d71852e49da43d3106a05ebfc28a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="step-7-set-up-the-source-and-target-for-physical-server-replication-to-azure"></a><span data-ttu-id="a3be6-103">7단계: Azure에 물리적 서버 복제를 위한 원본 및 대상 설정</span><span class="sxs-lookup"><span data-stu-id="a3be6-103">Step 7: Set up the source and target for physical server replication to Azure</span></span>

<span data-ttu-id="a3be6-104">이 문서에서는 Azure Portal에서 [Azure Site Recovery](site-recovery-overview.md) 서비스를 사용하여 Azure에 온-프레미스 물리적 서버를 복제할 때 원본 및 대상 설정을 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a3be6-104">This article describes how to configure source and target settings when replicating on-premises physical servers to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="a3be6-105">이 문서의 하단 또는 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 의견이나 질문을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="a3be6-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-the-source-environment"></a><span data-ttu-id="a3be6-106">원본 환경 설정</span><span class="sxs-lookup"><span data-stu-id="a3be6-106">Set up the source environment</span></span>

<span data-ttu-id="a3be6-107">구성 서버를 설정하고 자격 증명 모음에 등록한 후 컴퓨터를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a3be6-107">Set up the configuration server, register it in the vault, and discover machines.</span></span>

1. <span data-ttu-id="a3be6-108">**Site Recovery** > **1단계: 인프라 준비** > **원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3be6-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="a3be6-109">구성 서버가 없는 경우 **+구성 서버**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3be6-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="a3be6-110">**서버 추가**에서 **구성 서버**가 **서버 형식**에 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a3be6-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="a3be6-111">Site Recovery 통합 설치 프로그램 설치 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a3be6-111">Download the Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="a3be6-112">자격 증명 모음 등록 키를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a3be6-112">Download the vault registration key.</span></span> <span data-ttu-id="a3be6-113">통합 설치를 실행할 때 이 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a3be6-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="a3be6-114">이 키는 생성된 날로부터 5일간 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="a3be6-114">The key is valid for five days after you generate it.</span></span>

   ![원본 설정](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-the-configuration-server-in-the-vault"></a><span data-ttu-id="a3be6-116">자격 증명 모음에 구성 서버 등록</span><span class="sxs-lookup"><span data-stu-id="a3be6-116">Register the configuration server in the vault</span></span>

<span data-ttu-id="a3be6-117">다음을 수행하여 시작하기 전에 통합 설치 프로그램을 실행하여 구성 서버, 프로세스 서버 및 마스터 대상 서버를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a3be6-117">Do the following before you start, then run Unified Setup to install the configuration server, the process server, and the master target server.</span></span> <span data-ttu-id="a3be6-118">이 비디오에서는 VMware VM을 Azure로 복제하기 위한 구성 요소를 설정하는 과정을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a3be6-118">The video describes setting up the components for VMware VM to Azure replication.</span></span> <span data-ttu-id="a3be6-119">그러나 물리적 서버를 Azure로 복제하는 과정에도 동일한 프로세스가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3be6-119">However, the same process is valid for physical server to Azure replication.</span></span>

- <span data-ttu-id="a3be6-120">구성 서버 VM에서 시스템 시계가 [시간 서버](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service)와 동기화되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a3be6-120">On the configuration server VM, make sure that the system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="a3be6-121">서로 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3be6-121">It should match.</span></span> <span data-ttu-id="a3be6-122">15분 빠르거나 늦은 경우 설치가 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3be6-122">If it's 15 minutes in front or behind, setup might fail.</span></span>
- <span data-ttu-id="a3be6-123">구성 서버 컴퓨터에서 로컬 관리자로 설치 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a3be6-123">Run setup as a Local Administrator on the configuration server machine.</span></span>
- <span data-ttu-id="a3be6-124">TLS 1.0이 VM에서 활성화되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a3be6-124">Make sure TLS 1.0 is enabled on the VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="a3be6-125">[명령줄](http://aka.ms/installconfigsrv)을 통해 구성 서버를 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3be6-125">The configuration server can also be installed [from the command line](http://aka.ms/installconfigsrv).</span></span>




## <a name="set-up-the-target-environment"></a><span data-ttu-id="a3be6-126">대상 환경 설정</span><span class="sxs-lookup"><span data-stu-id="a3be6-126">Set up the target environment</span></span>

<span data-ttu-id="a3be6-127">대상 환경을 설정하기 전에 Azure Storage 계정 및 가상 네트워크가 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a3be6-127">Before you set up the target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="a3be6-128">**인프라 준비** > **대상**을 클릭하고 사용하려는 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a3be6-128">Click **Prepare infrastructure** > **Target**, and select the Azure subscription you want to use.</span></span>
2. <span data-ttu-id="a3be6-129">대상 배포 모델이 리소스 관리자 기반인지, 클래식인지 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a3be6-129">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="a3be6-130">Site Recovery가 호환되는 Azure 저장소 계정 및 네트워크가 하나 이상 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a3be6-130">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![대상](./media/physical-walkthrough-source-target/gs-target.png)

4. <span data-ttu-id="a3be6-132">저장소 계정 또는 네트워크를 만들지 않았으면 **+저장소 계정** 또는 **+네트워크**를 클릭하여 리소스 관리자 계정이나 인라인 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a3be6-132">If you haven't created a storage account or network, click **+Storage account** or **+Network**, to create a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3be6-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a3be6-133">Next steps</span></span>

<span data-ttu-id="a3be6-134">[8단계: 복제 정책 설정](physical-walkthrough-replication.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a3be6-134">Go to [Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>
