---
title: "aaaHow tooinstall Azure tooon 온-프레미스에서 장애 조치에 대 한 Linux 마스터 대상 서버 | Microsoft Docs"
description: "Linux 가상 컴퓨터를 다시 보호하려면 Linux 마스터 대상 서버가 필요합니다. 자세한 내용은 방법 tooinstall 하나입니다."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: d7c55d115712b9862414979f89efb1f177c5f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-linux-master-target-server"></a><span data-ttu-id="5cd6a-104">Linux 마스터 대상 서버 설치</span><span class="sxs-lookup"><span data-stu-id="5cd6a-104">Install a Linux master target server</span></span>
<span data-ttu-id="5cd6a-105">가상 컴퓨터를 통해 실패 한 후 뒤로 hello 가상 컴퓨터 toohello 온-프레미스 사이트를 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-105">After you fail over your virtual machines, you can fail back hello virtual machines toohello on-premises site.</span></span> <span data-ttu-id="5cd6a-106">toofail 다시 Azure toohello 온-프레미스 사이트에서 tooreprotect hello 가상 컴퓨터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-106">toofail back, you need tooreprotect hello virtual machine from Azure toohello on-premises site.</span></span> <span data-ttu-id="5cd6a-107">이 프로세스는 온-프레미스 마스터 대상 서버 tooreceive hello 트래픽을 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-107">For this process, you need an on-premises master target server tooreceive hello traffic.</span></span> 

<span data-ttu-id="5cd6a-108">보호된 가상 컴퓨터가 Windows 가상 컴퓨터인 경우 Windows 마스터 대상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-108">If your protected virtual machine is a Windows virtual machine, then you need a Windows master target.</span></span> <span data-ttu-id="5cd6a-109">Linux 가상 컴퓨터인 경우 Linux 마스터 대상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-109">For a Linux virtual machine, you need a Linux master target.</span></span> <span data-ttu-id="5cd6a-110">읽기 hello 다음 단계 toolearn toocreate 및 설치 된 Linux 마스터 대상에 어떻게 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-110">Read hello following steps toolearn how toocreate and install a Linux master target.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5cd6a-111">릴리스부터 hello 9.10.0 마스터 대상 서버를 마스터 대상 서버를 최신 hello 설치할 수 있습니다만 16.04 Ubuntu 서버에.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-111">Starting with release of hello 9.10.0 master target server, hello latest master target server can be only installed on an Ubuntu 16.04 server.</span></span> <span data-ttu-id="5cd6a-112">새로운 설치는 CentOS6.6 서버에서 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-112">New installations aren't allowed on  CentOS6.6 servers.</span></span> <span data-ttu-id="5cd6a-113">그러나 계속할 수 있습니다 tooupgrade 이전 마스터 대상 서버 hello 9.10.0 버전을 사용 하 여.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-113">However, you can continue tooupgrade your old master target servers by using hello 9.10.0 version.</span></span>

## <a name="overview"></a><span data-ttu-id="5cd6a-114">개요</span><span class="sxs-lookup"><span data-stu-id="5cd6a-114">Overview</span></span>
<span data-ttu-id="5cd6a-115">이 문서에서는 어떻게 tooinstall Linux 마스터 대상에 대 한 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-115">This article provides instructions for how tooinstall a Linux master target.</span></span>

<span data-ttu-id="5cd6a-116">Hello 또는이 문서의 hello 끝에 메모 또는 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-116">Post comments or questions at hello end of this article or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5cd6a-117">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5cd6a-117">Prerequisites</span></span>

* <span data-ttu-id="5cd6a-118">어떤 toodeploy hello 마스터 대상에서 toochoose hello 호스트 hello 장애 복구 toobe tooan 기존 온-프레미스 가상 컴퓨터 또는 가상 컴퓨터를 새 tooa 진행 되는 경우를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-118">toochoose hello host on which toodeploy hello master target, determine if hello failback is going toobe tooan existing on-premises virtual machine or tooa new virtual machine.</span></span> 
    * <span data-ttu-id="5cd6a-119">기존 가상 컴퓨터에 대 한 hello 마스터 대상의 hello 호스트 hello 가상 컴퓨터의 액세스 toohello 데이터 저장소가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-119">For an existing virtual machine, hello host of hello master target should have access toohello data stores of hello virtual machine.</span></span>
    * <span data-ttu-id="5cd6a-120">Hello 온-프레미스 가상 컴퓨터가 없는 경우 동일한 호스트 hello 마스터 대상으로 하는 hello에 hello 장애 복구 가상 컴퓨터가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-120">If hello on-premises virtual machine does not exist, hello failback virtual machine is created on hello same host as hello master target.</span></span> <span data-ttu-id="5cd6a-121">Tooinstall hello 마스터 대상 모든 ESXi 호스트를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-121">You can choose any ESXi host tooinstall hello master target.</span></span>
* <span data-ttu-id="5cd6a-122">마스터 대상 hello hello 프로세스 서버와 hello 구성 서버와 통신할 수 있는 네트워크에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-122">hello master target should be on a network that can communicate with hello process server and hello configuration server.</span></span>
* <span data-ttu-id="5cd6a-123">hello 마스터 대상의 hello 버전 같으면 tooor를 hello 버전의 프로세스 서버 hello 및 hello 구성 서버 보다 이전 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-123">hello version of hello master target must be equal tooor earlier than hello versions of hello process server and hello configuration server.</span></span> <span data-ttu-id="5cd6a-124">예를 들어 9.4 hello hello 구성 서버 버전을 사용 하는 경우 9.4 또는 9.3 있지만 하지 9.5 hello 버전 hello 마스터 대상의 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-124">For example, if hello version of hello configuration server is 9.4, hello version of hello master target can be 9.4 or 9.3 but not 9.5.</span></span>
* <span data-ttu-id="5cd6a-125">않을 hello 마스터 대상을 VMware 가상 컴퓨터와 물리적 서버 하지 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-125">hello master target can only be a VMware virtual machine and not a physical server.</span></span>

## <a name="create-hello-master-target-according-toohello-sizing-guidelines"></a><span data-ttu-id="5cd6a-126">Toohello 크기 조정 지침에 따라 hello 마스터 대상 만들기</span><span class="sxs-lookup"><span data-stu-id="5cd6a-126">Create hello master target according toohello sizing guidelines</span></span>

<span data-ttu-id="5cd6a-127">Hello hello 크기 조정 지침에 따라 마스터 대상 만들기:</span><span class="sxs-lookup"><span data-stu-id="5cd6a-127">Create hello master target in accordance with hello following sizing guidelines:</span></span>
- <span data-ttu-id="5cd6a-128">**RAM**: 6GB 이상</span><span class="sxs-lookup"><span data-stu-id="5cd6a-128">**RAM**: 6 GB or more</span></span>
- <span data-ttu-id="5cd6a-129">**OS 디스크 크기**: 100GB 또는 자세한 (tooinstall CentOS6.6)</span><span class="sxs-lookup"><span data-stu-id="5cd6a-129">**OS disk size**: 100 GB or more (tooinstall CentOS6.6)</span></span>
- <span data-ttu-id="5cd6a-130">**보존 드라이브에 대한 추가 디스크 크기**: 1TB</span><span class="sxs-lookup"><span data-stu-id="5cd6a-130">**Additional disk size for retention drive**: 1 TB</span></span>
- <span data-ttu-id="5cd6a-131">**CPU 코어**: 코어 4개 이상</span><span class="sxs-lookup"><span data-stu-id="5cd6a-131">**CPU cores**: 4 cores or more</span></span>

<span data-ttu-id="5cd6a-132">hello 다음 지원 Ubuntu 커널 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-132">hello following supported Ubuntu kernels are supported.</span></span>


|<span data-ttu-id="5cd6a-133">커널 시리즈</span><span class="sxs-lookup"><span data-stu-id="5cd6a-133">Kernel Series</span></span>  |<span data-ttu-id="5cd6a-134">너무 지원</span><span class="sxs-lookup"><span data-stu-id="5cd6a-134">Support up too</span></span> |
|---------|---------|
|<span data-ttu-id="5cd6a-135">4.4.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-135">4.4</span></span>      |<span data-ttu-id="5cd6a-136">4.4.0-81-제네릭</span><span class="sxs-lookup"><span data-stu-id="5cd6a-136">4.4.0-81-generic</span></span>         |
|<span data-ttu-id="5cd6a-137">4.8</span><span class="sxs-lookup"><span data-stu-id="5cd6a-137">4.8</span></span>      |<span data-ttu-id="5cd6a-138">4.8.0-56-제네릭</span><span class="sxs-lookup"><span data-stu-id="5cd6a-138">4.8.0-56-generic</span></span>         |
|<span data-ttu-id="5cd6a-139">4.10</span><span class="sxs-lookup"><span data-stu-id="5cd6a-139">4.10</span></span>     |<span data-ttu-id="5cd6a-140">4.10.0-24-제네릭</span><span class="sxs-lookup"><span data-stu-id="5cd6a-140">4.10.0-24-generic</span></span>        |


## <a name="deploy-hello-master-target-server"></a><span data-ttu-id="5cd6a-141">Hello 마스터 대상 서버를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-141">Deploy hello master target server</span></span>

### <a name="install-ubuntu-16042-minimal"></a><span data-ttu-id="5cd6a-142">Ubuntu 16.04.2 최소 설치</span><span class="sxs-lookup"><span data-stu-id="5cd6a-142">Install Ubuntu 16.04.2 Minimal</span></span>

<span data-ttu-id="5cd6a-143">Hello hello 단계 tooinstall hello Ubuntu 16.04.2 64 비트 운영 체제에 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-143">Take hello following hello steps tooinstall hello Ubuntu 16.04.2 64-bit operating system.</span></span>

<span data-ttu-id="5cd6a-144">**1 단계:** toohello 이동 [다운로드 링크](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) hello 가장 가까운 미러를 선택 하 고에서 Ubuntu 16.04.2 최소 64 비트 ISO를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-144">**Step 1:** Go toohello [download link](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) and choose hello closest mirror from which download an Ubuntu 16.04.2 minimal 64-bit ISO.</span></span>

<span data-ttu-id="5cd6a-145">Ubuntu 16.04.2 최소 64 비트 ISO hello DVD 드라이브에 유지 하 고 hello 시스템을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-145">Keep an Ubuntu 16.04.2 minimal 64-bit ISO in hello DVD drive and start hello system.</span></span>

<span data-ttu-id="5cd6a-146">**2단계:** 원하는 언어로 **영어**를 선택하고 **Enter** 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-146">**Step 2:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![언어 선택](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image1.png)

<span data-ttu-id="5cd6a-148">**3단계:** **Ubuntu 서버 설치**를 선택하고 **Enter** 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-148">**Step 3:** Select **Install Ubuntu Server**, and then select **Enter**.</span></span>

![Ubuntu Server 설치 선택](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image2.png)

<span data-ttu-id="5cd6a-150">**4단계:** 원하는 언어로 **영어**를 선택하고 **Enter** 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-150">**Step 4:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![원하는 언어로 영어 선택](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image3.png)

<span data-ttu-id="5cd6a-152">**5 단계:** 선택 hello hello에서 적절 한 옵션 **시간대** 옵션 목록에서 선택한 후 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-152">**Step 5:** Select hello appropriate option from hello **Time Zone** options list, and then select **Enter**.</span></span>

![Hello 올바른 표준 시간대를 선택 합니다.](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image4.png)

<span data-ttu-id="5cd6a-154">**6 단계:** 선택 **아니요** (기본 옵션 hello)를 선택한 후 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-154">**Step 6:** Select **No** (hello default option), and then select **Enter**.</span></span>


![Hello 키보드 구성](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image5.png)

<span data-ttu-id="5cd6a-156">**7 단계:** 선택 **영어 (미국)** hello 키보드에 대 한 원본 국가 및 선택 hello로 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-156">**Step 7:** Select **English (US)** as hello country of origin for hello keyboard, and then select **Enter**.</span></span>

![미국 원본 hello 국가 선택](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image6.png)

<span data-ttu-id="5cd6a-158">**8 단계:** 선택 **영어 (미국)** hello 자판 배열, 한 다음 선택으로 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-158">**Step 8:** Select **English (US)** as hello keyboard layout, and then select **Enter**.</span></span>

![영어 (미국) hello 키보드 레이아웃으로 선택](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image7.png)

<span data-ttu-id="5cd6a-160">**9 단계:** 서버 hello에 대 한 hello 호스트 이름을 입력 하십시오 **Hostname** 상자를 선택한 후 **계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-160">**Step 9:** Enter hello hostname for your server in hello **Hostname** box, and then select **Continue**.</span></span>

![서버에 대 한 hello 호스트 이름 입력](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image8.png)

<span data-ttu-id="5cd6a-162">**10 단계:** toocreate 사용자 계정 hello 사용자 이름을 입력 한 다음 선택 **계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-162">**Step 10:** toocreate a user account, enter hello user name, and then select **Continue**.</span></span>

![사용자 계정 만들기](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image9.png)

<span data-ttu-id="5cd6a-164">**11 단계:** hello 새 사용자 계정에 대 한 hello 암호를 입력 한 다음 선택 **계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-164">**Step 11:** Enter hello password for hello new user account, and then select **Continue**.</span></span>

![Hello 암호를 입력 합니다.](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image10.png)

<span data-ttu-id="5cd6a-166">**12 단계:** hello 암호 hello 새 사용자를 확인 한 다음 선택 **계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-166">**Step 12:** Confirm hello password for hello new user, and then select **Continue**.</span></span>

![Hello 암호 확인](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image11.png)

<span data-ttu-id="5cd6a-168">**13 단계:** 선택 **아니요** (기본 옵션 hello)를 선택한 후 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-168">**Step 13:** Select **No** (hello default option), and then select **Enter**.</span></span>

![사용자 및 암호 설정](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image12.png)

<span data-ttu-id="5cd6a-170">**14 단계:** hello 표준 시간대 표시 되는 정확한 경우 선택 **예** (기본 옵션 hello)를 선택한 후 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-170">**Step 14:** If hello time zone that's displayed is correct, select **Yes** (hello default option), and then select **Enter**.</span></span>

<span data-ttu-id="5cd6a-171">tooreconfigure 시간대를 선택 **아니요**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-171">tooreconfigure your time zone, select **No**.</span></span>

![Hello 클록 구성](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image13.png)

<span data-ttu-id="5cd6a-173">**15 단계:** hello 분할 방법 옵션을 선택 **전체 디스크를 사용 하 여 문제 해결-**를 선택한 후 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-173">**Step 15:** From hello partitioning method options, select **Guided - use entire disk**, and then select **Enter**.</span></span>

![Hello 분할 방법 옵션을 선택 합니다.](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image14.png)

<span data-ttu-id="5cd6a-175">**16 단계:** 선택 hello hello에서 적절 한 디스크 **디스크 toopartition 선택** 옵션을 선택한 후 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-175">**Step 16:** Select hello appropriate disk from hello **Select disk toopartition** options, and then select **Enter**.</span></span>


![Hello 디스크 선택](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image15.png)

<span data-ttu-id="5cd6a-177">**17 단계:** 선택 **예** toowrite 변경 toodisk hello 선택한 후 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-177">**Step 17:** Select **Yes** toowrite hello changes toodisk, and then select **Enter**.</span></span>

![Hello 변경 toodisk 작성](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image16.png)

<span data-ttu-id="5cd6a-179">**18 단계:** hello 기본 옵션을 선택 **계속**를 선택한 후 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-179">**Step 18:** Select hello default option, select **Continue**, and then select **Enter**.</span></span>

![Hello 기본 옵션을 선택 합니다.](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image17.png)

<span data-ttu-id="5cd6a-181">**단계 19:** hello 시스템에서 업그레이드를 관리 하기 위한 적절 한 옵션을 선택한 다음 선택 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-181">**Step 19:** Select hello appropriate option for managing upgrades on your system, and then select **Enter**.</span></span>

![Toomanage 업그레이드 방법 선택](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image18.png)

> [!WARNING]
> <span data-ttu-id="5cd6a-183">Hello Azure Site Recovery 마스터 대상 서버에서 특정 버전의 hello Ubuntu 필요로 하므로 해야 tooensure 업그레이드를 사용할 수 없습니다. 해당 hello 커널 hello 가상 컴퓨터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-183">Because hello Azure Site Recovery master target server requires a very specific version of hello Ubuntu, you need tooensure that hello kernel upgrades are disabled for hello virtual machine.</span></span> <span data-ttu-id="5cd6a-184">사용 되는 경우 일반 업그레이드 hello 마스터 대상 서버 toomalfunction을 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-184">If they are enabled, then any regular upgrades cause hello master target server toomalfunction.</span></span> <span data-ttu-id="5cd6a-185">Hello를 선택 했는지 확인 **자동 업데이트가** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-185">Make sure you select hello **No automatic updates** option.</span></span>


<span data-ttu-id="5cd6a-186">**20단계:** 기본 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-186">**Step 20:** Select default options.</span></span> <span data-ttu-id="5cd6a-187">SSH 연결을 위해 openSSH를 하려는 경우 선택 hello **OpenSSH 서버** 옵션을 선택한 다음 선택 **계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-187">If you want openSSH for SSH connect, select hello **OpenSSH server** option, and then select **Continue**.</span></span>

![소프트웨어 선택](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image19.png)

<span data-ttu-id="5cd6a-189">**21단계:** **예**를 선택한 후 **Enter** 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-189">**Step 21:** Select **Yes**, and then select **Enter**.</span></span>

![Hello GRUB 부팅 로더가 설치](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image20.png)

<span data-ttu-id="5cd6a-191">**22 단계:** 선택 hello hello 부팅 로더가 설치에 대 한 적절 한 장치 (가급적 **/개발/sda**)를 선택한 후 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-191">**Step 22:** Select hello appropriate device for hello boot loader installation (preferably **/dev/sda**), and then select **Enter**.</span></span>

![부팅 로더 설치를 위한 장치 선택](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image21.png)

<span data-ttu-id="5cd6a-193">**23 단계:** 선택 **계속**를 선택한 후 **Enter** toofinish hello 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-193">**Step 23:** Select **Continue**, and then select **Enter** toofinish hello installation.</span></span>

![Hello 설치 완료](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image22.png)

<span data-ttu-id="5cd6a-195">Hello 설치가 완료 되 면 VM toohello hello 새 사용자 자격 증명으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-195">After hello installation has finished, sign in toohello VM with hello new user credentials.</span></span> <span data-ttu-id="5cd6a-196">(너무 참조**10 단계** 자세한 정보에 대 한 합니다.)</span><span class="sxs-lookup"><span data-stu-id="5cd6a-196">(Refer too**Step 10** for more information.)</span></span>

<span data-ttu-id="5cd6a-197">사용자 암호 hello 스크린 샷 tooset hello 루트 다음에 설명 된 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-197">Take hello steps that are described in hello following screenshot tooset hello ROOT user password.</span></span> <span data-ttu-id="5cd6a-198">그런 다음 루트 사용자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-198">Then sign in as ROOT user.</span></span>

![Hello 루트 사용자 암호 설정](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image23.png)


### <a name="prepare-hello-machine-for-configuration-as-a-master-target-server"></a><span data-ttu-id="5cd6a-200">마스터 대상 서버와 구성에 대 한 hello 컴퓨터를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-200">Prepare hello machine for configuration as a master target server</span></span>
<span data-ttu-id="5cd6a-201">다음으로 마스터 대상 서버와 구성에 대 한 hello 컴퓨터를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-201">Next, prepare hello machine for configuration as a master target server.</span></span>

<span data-ttu-id="5cd6a-202">Linux 가상 컴퓨터에서 각 SCSI 하드 디스크에 대 한 tooget hello ID 사용 hello **디스크. EnableUUID = TRUE** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-202">tooget hello ID for each SCSI hard disk in a Linux virtual machine, enable hello **disk.EnableUUID = TRUE** parameter.</span></span>

<span data-ttu-id="5cd6a-203">이 매개 변수를 다음 take hello 단계 tooenable:</span><span class="sxs-lookup"><span data-stu-id="5cd6a-203">tooenable this parameter, take hello following steps:</span></span>

1. <span data-ttu-id="5cd6a-204">가상 컴퓨터를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-204">Shut down your virtual machine.</span></span>

2. <span data-ttu-id="5cd6a-205">Hello 왼쪽된 창에서 가상 컴퓨터 hello에 대 한 hello 항목을 마우스 오른쪽 단추로 클릭 한 다음 선택 **설정 편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-205">Right-click hello entry for hello virtual machine in hello left pane, and then select **Edit Settings**.</span></span>

3. <span data-ttu-id="5cd6a-206">선택 hello **옵션** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-206">Select hello **Options** tab.</span></span>

4. <span data-ttu-id="5cd6a-207">Hello 왼쪽된 창에서 선택 **고급** > **일반**를 선택한 후 hello **구성 매개 변수** hello hello 화면 오른쪽 아래 부분에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-207">In hello left pane, select **Advanced** > **General**, and then select hello **Configuration Parameters** button on hello lower-right part of hello screen.</span></span>

    ![옵션 탭](./media/site-recovery-how-to-install-linux-master-target/media/image20.png)

    <span data-ttu-id="5cd6a-209">hello **구성 매개 변수** hello 컴퓨터가 실행 중인 경우이 옵션을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-209">hello **Configuration Parameters** option is not available when hello machine is running.</span></span> <span data-ttu-id="5cd6a-210">toomake이이 탭이 활성화를 hello 가상 컴퓨터를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-210">toomake this tab active, shut down hello virtual machine.</span></span>

5. <span data-ttu-id="5cd6a-211">**disk.EnableUUID**가 있는 행이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-211">See whether a row with **disk.EnableUUID** already exists.</span></span>

    - <span data-ttu-id="5cd6a-212">Hello 값이 있고 너무 설정 된 경우**False**, hello 값도 변경**True**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-212">If hello value exists and is set too**False**, change hello value too**True**.</span></span> <span data-ttu-id="5cd6a-213">(hello 값은 대/소문자 구분.)</span><span class="sxs-lookup"><span data-stu-id="5cd6a-213">(hello values are not case-sensitive.)</span></span>

    - <span data-ttu-id="5cd6a-214">Hello 값이 있고 너무 설정 된 경우**True**선택, **취소**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-214">If hello value exists and is set too**True**, select **Cancel**.</span></span>

    - <span data-ttu-id="5cd6a-215">Hello 값이 존재 하지 않는 경우 선택 **행 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-215">If hello value does not exist, select **Add Row**.</span></span>

    - <span data-ttu-id="5cd6a-216">Hello 이름 열에서 추가 **디스크. EnableUUID**를 설정한 다음 hello 값을 너무**TRUE**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-216">In hello name column, add **disk.EnableUUID**, and then set hello value too**TRUE**.</span></span>

    ![disk.EnableUUID가 있는지 확인](./media/site-recovery-how-to-install-linux-master-target/media/image21.png)

#### <a name="disable-kernel-upgrades"></a><span data-ttu-id="5cd6a-218">커널 업그레이드 비활성화</span><span class="sxs-lookup"><span data-stu-id="5cd6a-218">Disable kernel upgrades</span></span>

<span data-ttu-id="5cd6a-219">Azure Site Recovery 마스터 대상 서버 hello Ubuntu의 매우 구체적인 버전이 필요, hello 커널 업그레이드 hello 가상 컴퓨터에 대 한 해제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-219">Azure Site Recovery master target server requires a very specific version of hello Ubuntu, ensure that hello kernel upgrades are disabled for hello virtual machine.</span></span>

<span data-ttu-id="5cd6a-220">커널 업그레이드 사용 되는 경우 일반 업그레이드 hello 마스터 대상 서버 toomalfunction을 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-220">If kernel upgrades are enabled, then any regular upgrades cause hello master target server toomalfunction.</span></span>

#### <a name="download-and-install-additional-packages"></a><span data-ttu-id="5cd6a-221">추가 패키지를 다운로드하여 설치</span><span class="sxs-lookup"><span data-stu-id="5cd6a-221">Download and install additional packages</span></span>

> [!NOTE]
> <span data-ttu-id="5cd6a-222">인터넷 연결 toodownload 있고 추가 패키지를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-222">Make sure that you have Internet connectivity toodownload and install additional packages.</span></span> <span data-ttu-id="5cd6a-223">Toomanually 인터넷 연결을 설정 하지 않은 경우 해야 이러한 RPM 패키지를 찾아 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-223">If you don't have Internet connectivity, you need toomanually find these RPM packages and install them.</span></span>

```
apt-get install -y multipath-tools lsscsi python-pyasn1 lvm2 kpartx
```

### <a name="get-hello-installer-for-setup"></a><span data-ttu-id="5cd6a-224">설치 프로그램에 대 한 hello 설치 관리자 가져오기</span><span class="sxs-lookup"><span data-stu-id="5cd6a-224">Get hello installer for setup</span></span>

<span data-ttu-id="5cd6a-225">마스터 대상에 인터넷 연결이 있는 경우 다음 단계 toodownload hello installer hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-225">If your master target has Internet connectivity, you can use hello following steps toodownload hello installer.</span></span> <span data-ttu-id="5cd6a-226">그렇지 않으면 hello installer hello 프로세스 서버에서 복사한 다음 설치 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-226">Otherwise, you can copy hello installer from hello process server and then install it.</span></span>

#### <a name="download-hello-master-target-installation-packages"></a><span data-ttu-id="5cd6a-227">Hello 마스터 대상 설치 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-227">Download hello master target installation packages</span></span>

<span data-ttu-id="5cd6a-228">[Hello 최신 Linux 마스터 대상 설치 파일 다운로드](https://aka.ms/latestlinuxmobsvc)합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-228">[Download hello latest Linux master target installation bits](https://aka.ms/latestlinuxmobsvc).</span></span>

<span data-ttu-id="5cd6a-229">toodownload Linux 형식을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="5cd6a-229">toodownload it by using Linux, type:</span></span>

```
wget https://aka.ms/latestlinuxmobsvc -O latestlinuxmobsvc.tar.gz
```

<span data-ttu-id="5cd6a-230">다운로드 하 고 홈 디렉터리의 hello 설치 관리자의 압축을 푸는 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-230">Make sure that you download and unzip hello installer in your home directory.</span></span> <span data-ttu-id="5cd6a-231">너무 압축을 푸는**/usr/Local**, hello 설치에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-231">If you unzip too**/usr/Local**, then hello installation  fails.</span></span>


#### <a name="access-hello-installer-from-hello-process-server"></a><span data-ttu-id="5cd6a-232">Hello 프로세스 서버에서 액세스 hello 설치 관리자</span><span class="sxs-lookup"><span data-stu-id="5cd6a-232">Access hello installer from hello process server</span></span>

1. <span data-ttu-id="5cd6a-233">Hello 프로세스 서버에서 이동 너무**C:\Program Files (x86) \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-233">On hello process server, go too**C:\Program Files (x86)\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.</span></span>

2. <span data-ttu-id="5cd6a-234">Hello 프로세스 서버에서 hello 필요한 설치 관리자 파일을 복사 하 고로 저장 **latestlinuxmobsvc.tar.gz** 홈 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-234">Copy hello required installer file from hello process server, and save it as **latestlinuxmobsvc.tar.gz** in your home directory.</span></span>


### <a name="apply-custom-configuration-changes"></a><span data-ttu-id="5cd6a-235">사용자 지정 구성 변경 내용 적용</span><span class="sxs-lookup"><span data-stu-id="5cd6a-235">Apply custom configuration changes</span></span>

<span data-ttu-id="5cd6a-236">tooapply 사용자 지정 구성 변경 단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-236">tooapply custom configuration changes, use hello following steps:</span></span>


1. <span data-ttu-id="5cd6a-237">다음 명령 toountar hello 이진 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-237">Run hello following command toountar hello binary.</span></span>
    ```
    tar -zxvf latestlinuxmobsvc.tar.gz
    ```
    ![Hello 명령 toorun의 스크린샷](./media/site-recovery-how-to-install-linux-master-target/image16.png)

2. <span data-ttu-id="5cd6a-239">다음 명령 toogive 권한 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-239">Run hello following command toogive permission.</span></span>
    ```
    chmod 755 ./ApplyCustomChanges.sh
    ```

3. <span data-ttu-id="5cd6a-240">Hello 다음 명령 toorun hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-240">Run hello following command toorun hello script.</span></span>
    ```
    ./ApplyCustomChanges.sh
    ```
> [!NOTE]
> <span data-ttu-id="5cd6a-241">Hello 서버의 hello 스크립트를 한 번만 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-241">Run hello script only once on hello server.</span></span> <span data-ttu-id="5cd6a-242">Hello 서버를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-242">Shut down hello server.</span></span> <span data-ttu-id="5cd6a-243">Hello 서버를 다시 디스크를 추가한 후 hello 다음 섹션에 설명 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-243">Then restart hello server after you add a disk, as described in hello next section.</span></span>

### <a name="add-a-retention-disk-toohello-linux-master-target-virtual-machine"></a><span data-ttu-id="5cd6a-244">보존 디스크 toohello Linux 마스터 대상 가상 컴퓨터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-244">Add a retention disk toohello Linux master target virtual machine</span></span>

<span data-ttu-id="5cd6a-245">다음 단계 toocreate 보존 디스크 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-245">Use hello following steps toocreate a retention disk:</span></span>

1. <span data-ttu-id="5cd6a-246">새 1TB 디스크 toohello Linux 마스터 대상 가상 컴퓨터를 연결 하 고 hello 컴퓨터를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-246">Attach a new 1-TB disk toohello Linux master target virtual machine, and then start hello machine.</span></span>

2. <span data-ttu-id="5cd6a-247">사용 하 여 hello **다중 경로 ll** 명령 hello 보존 디스크의 toolearn hello 다중 경로 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-247">Use hello **multipath -ll** command toolearn hello multipath ID of hello retention disk.</span></span>

    ```
    multipath -ll
    ```
    ![hello 보존 디스크의 hello 다중 경로 ID](./media/site-recovery-how-to-install-linux-master-target/media/image22.png)

3. <span data-ttu-id="5cd6a-249">Hello 드라이브를 포맷 하 고 hello 새 드라이브에서 파일 시스템을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-249">Format hello drive, and then create a file system on hello new drive.</span></span>

    ```
    mkfs.ext4 /dev/mapper/<Retention disk's multipath id>
    ```
    ![Hello 드라이브에 파일 시스템 만들기](./media/site-recovery-how-to-install-linux-master-target/media/image23.png)

4. <span data-ttu-id="5cd6a-251">Hello 파일 시스템을 만든 후에 hello 보존 디스크를 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-251">After you create hello file system, mount hello retention disk.</span></span>
    ```
    mkdir /mnt/retention
    mount /dev/mapper/<Retention disk's multipath id> /mnt/retention
    ```
    ![탑재 hello 보존 디스크](./media/site-recovery-how-to-install-linux-master-target/media/image24.png)

5. <span data-ttu-id="5cd6a-253">Hello 만들기 **fstab** hello 시스템 시작 될 때마다 항목 toomount hello 보존 드라이브입니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-253">Create hello **fstab** entry toomount hello retention drive every time hello system starts.</span></span>
    ```
    vi /etc/fstab
    ```
    <span data-ttu-id="5cd6a-254">선택 **삽입** toobegin hello 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-254">Select **Insert** toobegin editing hello file.</span></span> <span data-ttu-id="5cd6a-255">새 줄을 만들고 텍스트 다음 hello를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-255">Create a new line, and then insert hello following text.</span></span> <span data-ttu-id="5cd6a-256">강조 표시 하는 hello hello 이전 명령에서 다중 경로 ID에 따라 hello 디스크 다중 경로 ID를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-256">Edit hello disk multipath ID based on hello highlighted multipath ID from hello previous command.</span></span>

    <span data-ttu-id="5cd6a-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span><span class="sxs-lookup"><span data-stu-id="5cd6a-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span></span>

    <span data-ttu-id="5cd6a-258">선택 **Esc**, 한 다음 입력 **: wq** (쓰기 및 종료) tooclose hello 편집기 창입니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-258">Select **Esc**, and then type **:wq** (write and quit) tooclose hello editor window.</span></span>

### <a name="install-hello-master-target"></a><span data-ttu-id="5cd6a-259">Hello 마스터 대상 설치</span><span class="sxs-lookup"><span data-stu-id="5cd6a-259">Install hello master target</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5cd6a-260">hello 버전의 hello 마스터 대상 서버는 같은 tooor hello 버전의 프로세스 서버 hello 및 hello 구성 서버 보다 이전 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-260">hello version of hello master target server must be equal tooor earlier than hello versions of hello process server and hello configuration server.</span></span> <span data-ttu-id="5cd6a-261">이 조건이 충족되지 않으면 다시 보호에 성공하지만 복제는 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-261">If this condition is not met, reprotect succeeds, but replication fails.</span></span>


> [!NOTE]
> <span data-ttu-id="5cd6a-262">Hello 마스터 대상 서버를 설치 하기 전에 확인 해당 hello **/등/호스트** hello 가상 컴퓨터 파일에 모든 네트워크 어댑터와 관련 된 hello 로컬 호스트 이름 toohello IP 주소를 매핑하는 항목이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-262">Before you install hello master target server, check that hello **/etc/hosts** file on hello virtual machine contains entries that map hello local hostname toohello IP addresses that are associated with all network adapters.</span></span>

1. <span data-ttu-id="5cd6a-263">Hello 전달 구가 복사 **C:\ProgramData\Microsoft Azure 사이트 Recovery\private\connection.passphrase** hello 구성 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-263">Copy hello passphrase from **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase** on hello configuration server.</span></span> <span data-ttu-id="5cd6a-264">다음으로 저장 **passphrase.txt** hello에 같은 로컬 디렉터리를 실행 하 여 다음 명령을 hello:</span><span class="sxs-lookup"><span data-stu-id="5cd6a-264">Then save it as **passphrase.txt** in hello same local directory by running hello following command:</span></span>

    ```
    echo <passphrase> >passphrase.txt
    ```
    <span data-ttu-id="5cd6a-265">예제:</span><span class="sxs-lookup"><span data-stu-id="5cd6a-265">Example:</span></span> 
    
    ```
    echo itUx70I47uxDuUVY >passphrase.txt
    ```

2. <span data-ttu-id="5cd6a-266">Note hello 구성 서버 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-266">Note hello configuration server's IP address.</span></span> <span data-ttu-id="5cd6a-267">Hello 다음 단계에 있어야합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-267">You need it in hello next step.</span></span>

3. <span data-ttu-id="5cd6a-268">다음 명령은 tooinstall hello 마스터 대상 서버 hello를 실행 하 고 hello 서버 hello 구성 서버를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-268">Run hello following command tooinstall hello master target server and register hello server with hello configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```

    <span data-ttu-id="5cd6a-269">예제:</span><span class="sxs-lookup"><span data-stu-id="5cd6a-269">Example:</span></span> 
    
    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

    <span data-ttu-id="5cd6a-270">Hello 스크립트에 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-270">Wait until hello script finishes.</span></span> <span data-ttu-id="5cd6a-271">마스터 대상 hello hello에 나열 되어 hello 마스터 대상에 성공적으로 등록 하면 **사이트 복구 인프라** hello 포털의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-271">If hello master target registers sucessfully, hello master target is listed on hello **Site Recovery Infrastructure** page of hello portal.</span></span>


#### <a name="install-hello-master-target-by-using-interactive-installation"></a><span data-ttu-id="5cd6a-272">대화형 설치를 사용 하 여 hello 마스터 대상 설치</span><span class="sxs-lookup"><span data-stu-id="5cd6a-272">Install hello master target by using interactive installation</span></span>

1. <span data-ttu-id="5cd6a-273">다음 명령 tooinstall hello에 대 한 마스터 대상을 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-273">Run hello following command tooinstall hello master target.</span></span> <span data-ttu-id="5cd6a-274">Hello 에이전트 역할에 대 한 선택 **마스터 대상**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-274">For hello agent role, choose **Master Target**.</span></span>

    ```
    ./install
    ```

2. <span data-ttu-id="5cd6a-275">설치를 위한 hello 기본 위치를 선택한 다음 선택 **Enter** toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-275">Choose hello default location for installation, and then select **Enter** toocontinue.</span></span>

    ![마스터 대상의 기본 설치 위치 선택](./media/site-recovery-how-to-install-linux-master-target/image17.png)

<span data-ttu-id="5cd6a-277">Hello 설치가 완료 되 면 hello 명령줄을 사용 하 여 hello 구성 서버를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-277">After hello installation has finished, register hello configuration server by using hello command line.</span></span>

1. <span data-ttu-id="5cd6a-278">Hello 구성 서버 IP 주소 hello note 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-278">Note hello IP address of hello configuration server.</span></span> <span data-ttu-id="5cd6a-279">Hello 다음 단계에 있어야합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-279">You need it in hello next step.</span></span>

2. <span data-ttu-id="5cd6a-280">다음 명령은 tooinstall hello 마스터 대상 서버 hello를 실행 하 고 hello 서버 hello 구성 서버를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-280">Run hello following command tooinstall hello master target server and register hello server with hello configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```
    <span data-ttu-id="5cd6a-281">예제:</span><span class="sxs-lookup"><span data-stu-id="5cd6a-281">Example:</span></span> 

    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

   <span data-ttu-id="5cd6a-282">Hello 스크립트에 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-282">Wait until hello script finishes.</span></span> <span data-ttu-id="5cd6a-283">마스터 대상 hello hello에 나열 되어 hello 마스터 대상에 성공적으로 등록 된 경우 **사이트 복구 인프라** hello 포털의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-283">If hello master target is registered succesfully, hello master target is listed on hello **Site Recovery Infrastructure** page of hello portal.</span></span>


### <a name="upgrade-hello-master-target"></a><span data-ttu-id="5cd6a-284">마스터 대상 hello 업그레이드</span><span class="sxs-lookup"><span data-stu-id="5cd6a-284">Upgrade hello master target</span></span>

<span data-ttu-id="5cd6a-285">Hello 설치 관리자를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-285">Run hello installer.</span></span> <span data-ttu-id="5cd6a-286">Hello 마스터 대상에 해당 hello 에이전트가 설치 되어 자동으로 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-286">It automatically detects that hello agent is installed on hello master target.</span></span> <span data-ttu-id="5cd6a-287">tooupgrade, **Y**합니다.  Hello 설치가 완료 된 후 다음 명령을 hello를 사용 하 여 설치 하는 hello 마스터 대상의 hello 버전을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-287">tooupgrade, select **Y**.  After hello setup has been completed, check hello version of hello master target installed by using hello following command.</span></span>

    ```
    cat /usr/local/.vx_version
    ```

<span data-ttu-id="5cd6a-288">해당 hello 나타나면 **버전** 필드 hello 마스터 대상의 hello 버전 번호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-288">You can see that hello **Version** field gives hello version number of hello master target.</span></span>

### <a name="install-vmware-tools-on-hello-master-target-server"></a><span data-ttu-id="5cd6a-289">Hello 마스터 대상 서버에서 VMware 도구를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-289">Install VMware tools on hello master target server</span></span>

<span data-ttu-id="5cd6a-290">Hello 데이터 저장소를 검색할 수 있도록 hello 마스터 대상에서 tooinstall VMware 도구가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-290">You need tooinstall VMware tools on hello master target so that it can discover hello data stores.</span></span> <span data-ttu-id="5cd6a-291">Hello 도구가 설치 되지 않은 경우 hello 다시 보호 화면 hello 데이터 저장소에 나열 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-291">If hello tools are not installed, hello reprotect screen isn't listed in hello data stores.</span></span> <span data-ttu-id="5cd6a-292">Hello VMware 도구를 설치 후 toorestart를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-292">After installation of hello VMware tools, you need toorestart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5cd6a-293">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5cd6a-293">Next steps</span></span>
<span data-ttu-id="5cd6a-294">Hello 설치 및 등록 hello 마스터 대상에 finsihed를 만든 후 hello 마스터 대상에 hello 표시를 볼 수 있습니다 **마스터 대상** 섹션 **사이트 복구 인프라**, hello에서 구성 서버 개요</span><span class="sxs-lookup"><span data-stu-id="5cd6a-294">After hello installation and registration of hello master target has finsihed, you can see hello master target appear on hello **Master Target** section in **Site Recovery Infrastructure**, under hello configuration server overview.</span></span>

<span data-ttu-id="5cd6a-295">이제 [다시 보호](site-recovery-how-to-reprotect.md)와 장애 복구를 계속 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-295">You can now proceed with [reprotection](site-recovery-how-to-reprotect.md), followed by failback.</span></span>

## <a name="common-issues"></a><span data-ttu-id="5cd6a-296">일반적인 문제</span><span class="sxs-lookup"><span data-stu-id="5cd6a-296">Common issues</span></span>

* <span data-ttu-id="5cd6a-297">마스터 대상 같은 관리 구성 요소에서 Storage vMotion을 설정하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-297">Make sure you do not turn on Storage vMotion on any management components such as a master target.</span></span> <span data-ttu-id="5cd6a-298">성공적으로 다시 보호 한 후 이동 하는 hello 마스터 대상 가상 컴퓨터 디스크 hello (Vmdk)을 분리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-298">If hello master target moves after a successful reprotect, hello virtual machine disks (VMDKs) cannot be detached.</span></span> <span data-ttu-id="5cd6a-299">이 경우, 장애 복구에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-299">In this case, failback fails.</span></span>

* <span data-ttu-id="5cd6a-300">hello 가상 컴퓨터에서 마스터 대상 hello 스냅숏이 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-300">hello master target should not have any snapshots on hello virtual machine.</span></span> <span data-ttu-id="5cd6a-301">스냅숏이 있으면 장애 복구에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-301">If there are snapshots, failback fails.</span></span>

* <span data-ttu-id="5cd6a-302">Toosome 사용자 지정 NIC 구성은 일부 고객, 기한 hello 네트워크 인터페이스는 시작 하는 동안 사용 하지 않도록 설정 하 고 hello 마스터 대상 에이전트를 초기화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-302">Due toosome custom NIC configurations at some customers, hello network interface is disabled during startup, and hello master target agent cannot initialize.</span></span> <span data-ttu-id="5cd6a-303">다음 속성이 해당 hello 올바르게 설정 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-303">Make sure that hello following properties are correctly set.</span></span> <span data-ttu-id="5cd6a-304">Hello 이더넷에서에서 이러한 속성에는 파일의 /etc/sysconfig/network-scripts/ifcfg 카드 확인-eth * 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cd6a-304">Check these properties in hello Ethernet card file's /etc/sysconfig/network-scripts/ifcfg-eth*.</span></span>
    * <span data-ttu-id="5cd6a-305">BOOTPROTO=dhcp</span><span class="sxs-lookup"><span data-stu-id="5cd6a-305">BOOTPROTO=dhcp</span></span>
    * <span data-ttu-id="5cd6a-306">ONBOOT=yes</span><span class="sxs-lookup"><span data-stu-id="5cd6a-306">ONBOOT=yes</span></span>
