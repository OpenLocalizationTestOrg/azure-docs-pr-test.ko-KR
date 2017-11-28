---
title: "Azure에서 온-프레미스로 장애 조치하기 위해 Linux 마스터 대상 서버를 설치하는 방법 | Microsoft Docs"
description: "Linux 가상 컴퓨터를 다시 보호하려면 Linux 마스터 대상 서버가 필요합니다. 설치 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 5341e3e56e0c366079958dd9a885f6ee3e8436cb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="install-a-linux-master-target-server"></a><span data-ttu-id="65c11-104">Linux 마스터 대상 서버 설치</span><span class="sxs-lookup"><span data-stu-id="65c11-104">Install a Linux master target server</span></span>
<span data-ttu-id="65c11-105">가상 컴퓨터를 장애 조치(failover)한 후 가상 컴퓨터를 다시 온-프레미스 사이트에 장애 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-105">After you fail over your virtual machines, you can fail back the virtual machines to the on-premises site.</span></span> <span data-ttu-id="65c11-106">장애 복구하려면 가상 컴퓨터를 Azure에서 온-프레미스 사이트로 다시 보호해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-106">To fail back, you need to reprotect the virtual machine from Azure to the on-premises site.</span></span> <span data-ttu-id="65c11-107">이 프로세스를 수행하려면 트래픽을 수신할 온-프레미스 마스터 대상 서버가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-107">For this process, you need an on-premises master target server to receive the traffic.</span></span> 

<span data-ttu-id="65c11-108">보호된 가상 컴퓨터가 Windows 가상 컴퓨터인 경우 Windows 마스터 대상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-108">If your protected virtual machine is a Windows virtual machine, then you need a Windows master target.</span></span> <span data-ttu-id="65c11-109">Linux 가상 컴퓨터인 경우 Linux 마스터 대상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-109">For a Linux virtual machine, you need a Linux master target.</span></span> <span data-ttu-id="65c11-110">다음 단계를 읽고 Linux 마스터 대상을 만들고 설치하는 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="65c11-110">Read the following steps to learn how to create and install a Linux master target.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="65c11-111">9.10.0 마스터 대상 서버 릴리스부터 최신 마스터 대상 서버는 Ubuntu 16.04 서버에만 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-111">Starting with release of the 9.10.0 master target server, the latest master target server can be only installed on an Ubuntu 16.04 server.</span></span> <span data-ttu-id="65c11-112">새로운 설치는 CentOS6.6 서버에서 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-112">New installations aren't allowed on  CentOS6.6 servers.</span></span> <span data-ttu-id="65c11-113">그러나 9.10.0 버전을 사용하여 이전 마스터 대상 서버를 계속 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-113">However, you can continue to upgrade your old master target servers by using the 9.10.0 version.</span></span>

## <a name="overview"></a><span data-ttu-id="65c11-114">개요</span><span class="sxs-lookup"><span data-stu-id="65c11-114">Overview</span></span>
<span data-ttu-id="65c11-115">이 문서에서는 Linux 마스터 대상을 설치하는 방법의 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-115">This article provides instructions for how to install a Linux master target.</span></span>

<span data-ttu-id="65c11-116">이 문서의 마지막 부분 또는 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에 의견이나 질문을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-116">Post comments or questions at the end of this article or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65c11-117">필수 조건</span><span class="sxs-lookup"><span data-stu-id="65c11-117">Prerequisites</span></span>

* <span data-ttu-id="65c11-118">마스터 대상을 배포해야 하는 호스트를 선택하려면 기존 온-프레미스 가상 컴퓨터에 장애 복구를 수행할 것인지 아니면 새 가상 컴퓨터에 장애 복구를 수행할 것인지 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-118">To choose the host on which to deploy the master target, determine if the failback is going to be to an existing on-premises virtual machine or to a new virtual machine.</span></span> 
    * <span data-ttu-id="65c11-119">기존 가상 컴퓨터에서 수행하는 경우 마스터 대상의 호스트가 가상 컴퓨터의 데이터 저장소에 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-119">For an existing virtual machine, the host of the master target should have access to the data stores of the virtual machine.</span></span>
    * <span data-ttu-id="65c11-120">온-프레미스 가상 컴퓨터가 없는 경우 마스터 대상과 동일한 호스트에 장애 복구 가상 컴퓨터가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-120">If the on-premises virtual machine does not exist, the failback virtual machine is created on the same host as the master target.</span></span> <span data-ttu-id="65c11-121">아무 ESXi 호스트를 선택하여 마스터 대상을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-121">You can choose any ESXi host to install the master target.</span></span>
* <span data-ttu-id="65c11-122">마스터 대상은 프로세스 서버 및 구성 서버와 통신할 수 있는 네트워크에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-122">The master target should be on a network that can communicate with the process server and the configuration server.</span></span>
* <span data-ttu-id="65c11-123">마스터 대상의 버전이 프로세스 서버 및 구성 서버의 버전과 같거나 그보다 이전 버전이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-123">The version of the master target must be equal to or earlier than the versions of the process server and the configuration server.</span></span> <span data-ttu-id="65c11-124">예를 들어 구성 서버의 버전이 9.4인 경우 마스터 대상의 버전이 9.4 또는 9.3인 것은 괜찮지만 9.5는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-124">For example, if the version of the configuration server is 9.4, the version of the master target can be 9.4 or 9.3 but not 9.5.</span></span>
* <span data-ttu-id="65c11-125">마스터 대상은 VMware 가상 컴퓨터만 될 수 있고 물리적 서버는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-125">The master target can only be a VMware virtual machine and not a physical server.</span></span>

## <a name="create-the-master-target-according-to-the-sizing-guidelines"></a><span data-ttu-id="65c11-126">크기 조정 지침에 따라 마스터 대상 만들기</span><span class="sxs-lookup"><span data-stu-id="65c11-126">Create the master target according to the sizing guidelines</span></span>

<span data-ttu-id="65c11-127">다음 크기 조정 지침에 따라 마스터 대상을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-127">Create the master target in accordance with the following sizing guidelines:</span></span>
- <span data-ttu-id="65c11-128">**RAM**: 6GB 이상</span><span class="sxs-lookup"><span data-stu-id="65c11-128">**RAM**: 6 GB or more</span></span>
- <span data-ttu-id="65c11-129">**OS 디스크 크기**: 100GB 이상(CentOS6.6 설치에 필요)</span><span class="sxs-lookup"><span data-stu-id="65c11-129">**OS disk size**: 100 GB or more (to install CentOS6.6)</span></span>
- <span data-ttu-id="65c11-130">**보존 드라이브에 대한 추가 디스크 크기**: 1TB</span><span class="sxs-lookup"><span data-stu-id="65c11-130">**Additional disk size for retention drive**: 1 TB</span></span>
- <span data-ttu-id="65c11-131">**CPU 코어**: 코어 4개 이상</span><span class="sxs-lookup"><span data-stu-id="65c11-131">**CPU cores**: 4 cores or more</span></span>

<span data-ttu-id="65c11-132">다음 지원되는 Ubuntu 커널을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-132">The following supported Ubuntu kernels are supported.</span></span>


|<span data-ttu-id="65c11-133">커널 시리즈</span><span class="sxs-lookup"><span data-stu-id="65c11-133">Kernel Series</span></span>  |<span data-ttu-id="65c11-134">최대 지원</span><span class="sxs-lookup"><span data-stu-id="65c11-134">Support up to</span></span>  |
|---------|---------|
|<span data-ttu-id="65c11-135">4.4.</span><span class="sxs-lookup"><span data-stu-id="65c11-135">4.4</span></span>      |<span data-ttu-id="65c11-136">4.4.0-81-제네릭</span><span class="sxs-lookup"><span data-stu-id="65c11-136">4.4.0-81-generic</span></span>         |
|<span data-ttu-id="65c11-137">4.8</span><span class="sxs-lookup"><span data-stu-id="65c11-137">4.8</span></span>      |<span data-ttu-id="65c11-138">4.8.0-56-제네릭</span><span class="sxs-lookup"><span data-stu-id="65c11-138">4.8.0-56-generic</span></span>         |
|<span data-ttu-id="65c11-139">4.10</span><span class="sxs-lookup"><span data-stu-id="65c11-139">4.10</span></span>     |<span data-ttu-id="65c11-140">4.10.0-24-제네릭</span><span class="sxs-lookup"><span data-stu-id="65c11-140">4.10.0-24-generic</span></span>        |


## <a name="deploy-the-master-target-server"></a><span data-ttu-id="65c11-141">마스터 대상 서버 배포</span><span class="sxs-lookup"><span data-stu-id="65c11-141">Deploy the master target server</span></span>

### <a name="install-ubuntu-16042-minimal"></a><span data-ttu-id="65c11-142">Ubuntu 16.04.2 최소 설치</span><span class="sxs-lookup"><span data-stu-id="65c11-142">Install Ubuntu 16.04.2 Minimal</span></span>

<span data-ttu-id="65c11-143">다음 단계를 통해 Ubuntu 16.04.2 64비트 운영 체제를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-143">Take the following the steps to install the Ubuntu 16.04.2 64-bit operating system.</span></span>

<span data-ttu-id="65c11-144">**1단계:** [다운로드 링크](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64)로 이동하고 Ubuntu 16.04.2 최소 64비트 ISO를 다운로드할 가장 가까운 미러를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-144">**Step 1:** Go to the [download link](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) and choose the closest mirror from which download an Ubuntu 16.04.2 minimal 64-bit ISO.</span></span>

<span data-ttu-id="65c11-145">DVD 드라이브에서 Ubuntu 16.04.2 최소 64비트 ISO를 유지하고 시스템을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-145">Keep an Ubuntu 16.04.2 minimal 64-bit ISO in the DVD drive and start the system.</span></span>

<span data-ttu-id="65c11-146">**2단계:** 원하는 언어로 **영어**를 선택하고 **Enter** 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-146">**Step 2:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![언어 선택](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image1.png)

<span data-ttu-id="65c11-148">**3단계:** **Ubuntu 서버 설치**를 선택하고 **Enter** 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-148">**Step 3:** Select **Install Ubuntu Server**, and then select **Enter**.</span></span>

![Ubuntu Server 설치 선택](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image2.png)

<span data-ttu-id="65c11-150">**4단계:** 원하는 언어로 **영어**를 선택하고 **Enter** 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-150">**Step 4:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![원하는 언어로 영어 선택](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image3.png)

<span data-ttu-id="65c11-152">**5단계:** **표준 시간대** 옵션 목록에서 적절한 옵션을 선택하고 **Enter** 키를 선택합니다</span><span class="sxs-lookup"><span data-stu-id="65c11-152">**Step 5:** Select the appropriate option from the **Time Zone** options list, and then select **Enter**.</span></span>

![올바른 표준 시간대 선택](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image4.png)

<span data-ttu-id="65c11-154">**6단계:** **아니요**(기본 옵션)를 선택하고 **Enter** 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-154">**Step 6:** Select **No** (the default option), and then select **Enter**.</span></span>


![키보드 구성](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image5.png)

<span data-ttu-id="65c11-156">**7단계:** 키보드에서 국적으로 **영어(미국)**을 선택하고 **Enter** 키를 선택합니다</span><span class="sxs-lookup"><span data-stu-id="65c11-156">**Step 7:** Select **English (US)** as the country of origin for the keyboard, and then select **Enter**.</span></span>

![국적으로 미국 선택](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image6.png)

<span data-ttu-id="65c11-158">**8단계:** 키보드 레이아웃으로 **영어(미국)**을 선택하고 **Enter** 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-158">**Step 8:** Select **English (US)** as the keyboard layout, and then select **Enter**.</span></span>

![키보드 레이아웃으로 영어(미국) 선택](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image7.png)

<span data-ttu-id="65c11-160">**9단계:** **호스트 이름** 상자에 서버의 호스트 이름을 입력하고 **계속**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-160">**Step 9:** Enter the hostname for your server in the **Hostname** box, and then select **Continue**.</span></span>

![서버의 호스트 이름 입력](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image8.png)

<span data-ttu-id="65c11-162">**10단계:** 사용자 계정을 만들려면 사용자 이름을 입력한 다음 **계속**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-162">**Step 10:** To create a user account, enter the user name, and then select **Continue**.</span></span>

![사용자 계정 만들기](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image9.png)

<span data-ttu-id="65c11-164">**11단계:** 새 사용자 계정의 암호를 입력한 다음 **계속**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-164">**Step 11:** Enter the password for the new user account, and then select **Continue**.</span></span>

![암호 입력](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image10.png)

<span data-ttu-id="65c11-166">**12단계:** 새 사용자의 암호를 확인한 다음 **계속**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-166">**Step 12:** Confirm the password for the new user, and then select **Continue**.</span></span>

![암호 확인](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image11.png)

<span data-ttu-id="65c11-168">**13단계:** **아니요**(기본 옵션)를 선택하고 **Enter** 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-168">**Step 13:** Select **No** (the default option), and then select **Enter**.</span></span>

![사용자 및 암호 설정](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image12.png)

<span data-ttu-id="65c11-170">**14단계:** 표시되는 표준 시간대가 올바르면 **예**(기본 옵션)를 선택한 후 **Enter** 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-170">**Step 14:** If the time zone that's displayed is correct, select **Yes** (the default option), and then select **Enter**.</span></span>

<span data-ttu-id="65c11-171">표준 시간대를 다시 구성하려면 **아니요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-171">To reconfigure your time zone, select **No**.</span></span>

![시계 구성](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image13.png)

<span data-ttu-id="65c11-173">**15단계:** 분할 방법 옵션에서 **단계별 - 전체 디스크 사용** 옵션을 선택하고 **Enter** 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-173">**Step 15:** From the partitioning method options, select **Guided - use entire disk**, and then select **Enter**.</span></span>

![분할 방법 옵션 선택](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image14.png)

<span data-ttu-id="65c11-175">**16단계:** **분할할 디스크 선택** 옵션에서 적절한 디스크를 선택하고 **Enter** 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-175">**Step 16:** Select the appropriate disk from the **Select disk to partition** options, and then select **Enter**.</span></span>


![디스크 선택](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image15.png)

<span data-ttu-id="65c11-177">**17단계:** **예**를 선택하여 디스크에 변경 내용을 작성하고 **Enter** 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-177">**Step 17:** Select **Yes** to write the changes to disk, and then select **Enter**.</span></span>

![디스크에 변경 내용 쓰기](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image16.png)

<span data-ttu-id="65c11-179">**18단계:** 기본 옵션을 선택하고 **계속**을 선택한 다음 **Enter** 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-179">**Step 18:** Select the default option, select **Continue**, and then select **Enter**.</span></span>

![기본 옵션 선택](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image17.png)

<span data-ttu-id="65c11-181">**19단계:** 시스템에서 업그레이드를 관리하기 위한 적절한 옵션을 선택한 다음 **Enter** 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-181">**Step 19:** Select the appropriate option for managing upgrades on your system, and then select **Enter**.</span></span>

![업그레이드를 관리하는 방법 선택](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image18.png)

> [!WARNING]
> <span data-ttu-id="65c11-183">Azure Site Recovery 마스터 대상 서버에 Ubuntu의 매우 구체적인 버전이 필요하기 때문에 가상 컴퓨터에서 커널 업그레이드를 비활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-183">Because the Azure Site Recovery master target server requires a very specific version of the Ubuntu, you need to ensure that the kernel upgrades are disabled for the virtual machine.</span></span> <span data-ttu-id="65c11-184">활성화한 경우 일반 업그레이드로 인해 마스터 대상 서버에 오작동이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-184">If they are enabled, then any regular upgrades cause the master target server to malfunction.</span></span> <span data-ttu-id="65c11-185">**자동 업데이트 없음** 옵션을 선택했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-185">Make sure you select the **No automatic updates** option.</span></span>


<span data-ttu-id="65c11-186">**20단계:** 기본 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-186">**Step 20:** Select default options.</span></span> <span data-ttu-id="65c11-187">SSH 연결에 openSSH를 설정하려는 경우 **OpenSSH 서버** 옵션을 선택한 다음 **계속**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-187">If you want openSSH for SSH connect, select the **OpenSSH server** option, and then select **Continue**.</span></span>

![소프트웨어 선택](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image19.png)

<span data-ttu-id="65c11-189">**21단계:** **예**를 선택한 후 **Enter** 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-189">**Step 21:** Select **Yes**, and then select **Enter**.</span></span>

![GRUB 부팅 로더 설치](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image20.png)

<span data-ttu-id="65c11-191">**22단계:** 부팅 로더를 설치하기 위해 적절한 장치를 선택한 다음(가급적 **/dev/sda**) **Enter** 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-191">**Step 22:** Select the appropriate device for the boot loader installation (preferably **/dev/sda**), and then select **Enter**.</span></span>

![부팅 로더 설치를 위한 장치 선택](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image21.png)

<span data-ttu-id="65c11-193">**23단계:** **계속**을 선택한 다음 **Enter** 키를 선택하여 설치를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-193">**Step 23:** Select **Continue**, and then select **Enter** to finish the installation.</span></span>

![설치 완료](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image22.png)

<span data-ttu-id="65c11-195">설치가 완료된 후에 새 사용자 자격 증명을 사용하여 VM에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-195">After the installation has finished, sign in to the VM with the new user credentials.</span></span> <span data-ttu-id="65c11-196">(자세한 정보는 **10단계**를 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="65c11-196">(Refer to **Step 10** for more information.)</span></span>

<span data-ttu-id="65c11-197">루트 사용자 암호를 설정하려면 다음 스크린샷에서 설명하는 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-197">Take the steps that are described in the following screenshot to set the ROOT user password.</span></span> <span data-ttu-id="65c11-198">그런 다음 루트 사용자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-198">Then sign in as ROOT user.</span></span>

![루트 사용자 암호 설정](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image23.png)


### <a name="prepare-the-machine-for-configuration-as-a-master-target-server"></a><span data-ttu-id="65c11-200">마스터 대상 서버로 구성할 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="65c11-200">Prepare the machine for configuration as a master target server</span></span>
<span data-ttu-id="65c11-201">다음으로 마스터 대상 서버로 구성할 컴퓨터를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-201">Next, prepare the machine for configuration as a master target server.</span></span>

<span data-ttu-id="65c11-202">Linux 가상 컴퓨터에 있는 각 SCSI 하드 디스크의 SCSI ID를 가져오려면 **disk.EnableUUID = TRUE** 매개 변수를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-202">To get the ID for each SCSI hard disk in a Linux virtual machine, enable the **disk.EnableUUID = TRUE** parameter.</span></span>

<span data-ttu-id="65c11-203">이 매개 변수를 사용하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="65c11-203">To enable this parameter, take the following steps:</span></span>

1. <span data-ttu-id="65c11-204">가상 컴퓨터를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-204">Shut down your virtual machine.</span></span>

2. <span data-ttu-id="65c11-205">왼쪽 창에서 가상 컴퓨터의 항목을 마우스 오른쪽 단추로 클릭한 다음 **편집 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-205">Right-click the entry for the virtual machine in the left pane, and then select **Edit Settings**.</span></span>

3. <span data-ttu-id="65c11-206">**옵션** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-206">Select the **Options** tab.</span></span>

4. <span data-ttu-id="65c11-207">왼쪽 창에서 **고급** > **일반**을 선택한 다음 화면의 오른쪽 아래에서 **구성 매개 변수** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-207">In the left pane, select **Advanced** > **General**, and then select the **Configuration Parameters** button on the lower-right part of the screen.</span></span>

    ![옵션 탭](./media/site-recovery-how-to-install-linux-master-target/media/image20.png)

    <span data-ttu-id="65c11-209">**구성 매개 변수** 옵션은 컴퓨터가 실행 중인 동안에는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-209">The **Configuration Parameters** option is not available when the machine is running.</span></span> <span data-ttu-id="65c11-210">이 탭을 활성화하려면 가상 컴퓨터를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-210">To make this tab active, shut down the virtual machine.</span></span>

5. <span data-ttu-id="65c11-211">**disk.EnableUUID**가 있는 행이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-211">See whether a row with **disk.EnableUUID** already exists.</span></span>

    - <span data-ttu-id="65c11-212">값이 있고 **False**로 설정되어 있으면 **True**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-212">If the value exists and is set to **False**, change the value to **True**.</span></span> <span data-ttu-id="65c11-213">(이 값은 대/소문자를 구분하지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="65c11-213">(The values are not case-sensitive.)</span></span>

    - <span data-ttu-id="65c11-214">값이 있고 **True**로 설정되어 있으면 **취소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-214">If the value exists and is set to **True**, select **Cancel**.</span></span>

    - <span data-ttu-id="65c11-215">값이 없으면 **행 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-215">If the value does not exist, select **Add Row**.</span></span>

    - <span data-ttu-id="65c11-216">이름 열에서 **disk.EnableUUID**를 추가하고 값을 **TRUE**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-216">In the name column, add **disk.EnableUUID**, and then set the value to **TRUE**.</span></span>

    ![disk.EnableUUID가 있는지 확인](./media/site-recovery-how-to-install-linux-master-target/media/image21.png)

#### <a name="disable-kernel-upgrades"></a><span data-ttu-id="65c11-218">커널 업그레이드 비활성화</span><span class="sxs-lookup"><span data-stu-id="65c11-218">Disable kernel upgrades</span></span>

<span data-ttu-id="65c11-219">Azure Site Recovery 마스터 대상 서버에 Ubuntu의 매우 구체적인 버전이 필요합니다. 가상 컴퓨터에 커널 업그레이드를 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-219">Azure Site Recovery master target server requires a very specific version of the Ubuntu, ensure that the kernel upgrades are disabled for the virtual machine.</span></span>

<span data-ttu-id="65c11-220">커널 업그레이드를 활성화한 경우 일반 업그레이드로 인해 마스터 대상 서버에 오작동이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-220">If kernel upgrades are enabled, then any regular upgrades cause the master target server to malfunction.</span></span>

#### <a name="download-and-install-additional-packages"></a><span data-ttu-id="65c11-221">추가 패키지를 다운로드하여 설치</span><span class="sxs-lookup"><span data-stu-id="65c11-221">Download and install additional packages</span></span>

> [!NOTE]
> <span data-ttu-id="65c11-222">추가 패키지를 다운로드하여 설치할 수 있도록 인터넷에 연결되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-222">Make sure that you have Internet connectivity to download and install additional packages.</span></span> <span data-ttu-id="65c11-223">인터넷에 연결되지 않으면 이러한 RPM 패키지를 수동으로 찾아서 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-223">If you don't have Internet connectivity, you need to manually find these RPM packages and install them.</span></span>

```
apt-get install -y multipath-tools lsscsi python-pyasn1 lvm2 kpartx
```

### <a name="get-the-installer-for-setup"></a><span data-ttu-id="65c11-224">설치를 위한 설치 프로그램 가져오기</span><span class="sxs-lookup"><span data-stu-id="65c11-224">Get the installer for setup</span></span>

<span data-ttu-id="65c11-225">마스터 대상이 인터넷에 연결된 경우 다음 단계에 따라 설치 프로그램을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-225">If your master target has Internet connectivity, you can use the following steps to download the installer.</span></span> <span data-ttu-id="65c11-226">인터넷에 연결되지 않은 경우 프로세스 서버에서 설치 프로그램을 복사하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-226">Otherwise, you can copy the installer from the process server and then install it.</span></span>

#### <a name="download-the-master-target-installation-packages"></a><span data-ttu-id="65c11-227">마스터 대상 설치 패키지 다운로드</span><span class="sxs-lookup"><span data-stu-id="65c11-227">Download the master target installation packages</span></span>

<span data-ttu-id="65c11-228">[최신 Linux 마스터 대상 설치 비트를 다운로드합니다](https://aka.ms/latestlinuxmobsvc).</span><span class="sxs-lookup"><span data-stu-id="65c11-228">[Download the latest Linux master target installation bits](https://aka.ms/latestlinuxmobsvc).</span></span>

<span data-ttu-id="65c11-229">Linux를 사용하여 다운로드하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-229">To download it by using Linux, type:</span></span>

```
wget https://aka.ms/latestlinuxmobsvc -O latestlinuxmobsvc.tar.gz
```

<span data-ttu-id="65c11-230">설치 관리자를 다운로드하고 홈 디렉터리에 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-230">Make sure that you download and unzip the installer in your home directory.</span></span> <span data-ttu-id="65c11-231">**/usr/Local**에 압축을 풀면 설치가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-231">If you unzip to **/usr/Local**, then the installation  fails.</span></span>


#### <a name="access-the-installer-from-the-process-server"></a><span data-ttu-id="65c11-232">프로세스 서버에서 설치 프로그램 액세스</span><span class="sxs-lookup"><span data-stu-id="65c11-232">Access the installer from the process server</span></span>

1. <span data-ttu-id="65c11-233">프로세스 서버에서 **C:\Program Files (x86)\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-233">On the process server, go to **C:\Program Files (x86)\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.</span></span>

2. <span data-ttu-id="65c11-234">프로세스 서버에서 필요한 설치 프로그램 파일을 복사하고 홈 디렉터리에 **latestlinuxmobsvc.tar.gz**로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-234">Copy the required installer file from the process server, and save it as **latestlinuxmobsvc.tar.gz** in your home directory.</span></span>


### <a name="apply-custom-configuration-changes"></a><span data-ttu-id="65c11-235">사용자 지정 구성 변경 내용 적용</span><span class="sxs-lookup"><span data-stu-id="65c11-235">Apply custom configuration changes</span></span>

<span data-ttu-id="65c11-236">사용자 지정 구성 변경 내용을 적용하려면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-236">To apply custom configuration changes, use the following steps:</span></span>


1. <span data-ttu-id="65c11-237">다음 명령을 실행하여 바이너리를 untar합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-237">Run the following command to untar the binary.</span></span>
    ```
    tar -zxvf latestlinuxmobsvc.tar.gz
    ```
    ![실행할 명령 스크린샷](./media/site-recovery-how-to-install-linux-master-target/image16.png)

2. <span data-ttu-id="65c11-239">다음 명령을 실행하여 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-239">Run the following command to give permission.</span></span>
    ```
    chmod 755 ./ApplyCustomChanges.sh
    ```

3. <span data-ttu-id="65c11-240">다음 명령을 사용하여 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-240">Run the following command to run the script.</span></span>
    ```
    ./ApplyCustomChanges.sh
    ```
> [!NOTE]
> <span data-ttu-id="65c11-241">서버에서 스크립트를 한 번만 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-241">Run the script only once on the server.</span></span> <span data-ttu-id="65c11-242">서버를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-242">Shut down the server.</span></span> <span data-ttu-id="65c11-243">다음 섹션에 설명된 대로 디스크를 추가한 후에 서버를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-243">Then restart the server after you add a disk, as described in the next section.</span></span>

### <a name="add-a-retention-disk-to-the-linux-master-target-virtual-machine"></a><span data-ttu-id="65c11-244">보존 디스크를 Linux 마스터 대상 가상 컴퓨터에 추가</span><span class="sxs-lookup"><span data-stu-id="65c11-244">Add a retention disk to the Linux master target virtual machine</span></span>

<span data-ttu-id="65c11-245">다음 단계에 따라 보존 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-245">Use the following steps to create a retention disk:</span></span>

1. <span data-ttu-id="65c11-246">Linux 마스터 대상 가상 컴퓨터에 새로운 1TB 디스크를 연결하고 컴퓨터를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-246">Attach a new 1-TB disk to the Linux master target virtual machine, and then start the machine.</span></span>

2. <span data-ttu-id="65c11-247">**multipath -ll** 명령을 사용하여 보존 디스크의 다중 경로 ID를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-247">Use the **multipath -ll** command to learn the multipath ID of the retention disk.</span></span>

    ```
    multipath -ll
    ```
    ![보존 디스크의 다중 경로 ID](./media/site-recovery-how-to-install-linux-master-target/media/image22.png)

3. <span data-ttu-id="65c11-249">드라이브를 포맷하고 새 드라이브에 파일 시스템을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-249">Format the drive, and then create a file system on the new drive.</span></span>

    ```
    mkfs.ext4 /dev/mapper/<Retention disk's multipath id>
    ```
    ![드라이브에 파일 시스템 만들기](./media/site-recovery-how-to-install-linux-master-target/media/image23.png)

4. <span data-ttu-id="65c11-251">파일 시스템을 만든 후 보존 디스크를 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-251">After you create the file system, mount the retention disk.</span></span>
    ```
    mkdir /mnt/retention
    mount /dev/mapper/<Retention disk's multipath id> /mnt/retention
    ```
    ![보존 디스크 탑재](./media/site-recovery-how-to-install-linux-master-target/media/image24.png)

5. <span data-ttu-id="65c11-253">시스템을 시작할 때마다 보존 드라이브를 탑재하도록 **fstab** 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-253">Create the **fstab** entry to mount the retention drive every time the system starts.</span></span>
    ```
    vi /etc/fstab
    ```
    <span data-ttu-id="65c11-254">**Insert** 키를 눌러 파일을 편집하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-254">Select **Insert** to begin editing the file.</span></span> <span data-ttu-id="65c11-255">새 줄을 만들고 다음 텍스트를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-255">Create a new line, and then insert the following text.</span></span> <span data-ttu-id="65c11-256">이전 명령에서 강조 표시된 다중 경로 ID에 따라 디스크 다중 경로 ID를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-256">Edit the disk multipath ID based on the highlighted multipath ID from the previous command.</span></span>

    <span data-ttu-id="65c11-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span><span class="sxs-lookup"><span data-stu-id="65c11-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span></span>

    <span data-ttu-id="65c11-258">**Esc** 키를 선택하고 **:wq**(쓰기 및 종료)를 입력하여 편집기 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-258">Select **Esc**, and then type **:wq** (write and quit) to close the editor window.</span></span>

### <a name="install-the-master-target"></a><span data-ttu-id="65c11-259">마스터 대상 설치</span><span class="sxs-lookup"><span data-stu-id="65c11-259">Install the master target</span></span>

> [!IMPORTANT]
> <span data-ttu-id="65c11-260">마스터 대상 서버의 버전이 프로세스 서버 및 구성 서버의 버전과 같거나 그보다 이전 버전이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-260">The version of the master target server must be equal to or earlier than the versions of the process server and the configuration server.</span></span> <span data-ttu-id="65c11-261">이 조건이 충족되지 않으면 다시 보호에 성공하지만 복제는 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-261">If this condition is not met, reprotect succeeds, but replication fails.</span></span>


> [!NOTE]
> <span data-ttu-id="65c11-262">마스터 대상 서버를 설치하기 전에 로컬 호스트 이름을 모든 네트워크 어댑터와 연결된 IP 주소에 매핑하는 항목이 가상 컴퓨터의**/etc/hosts** 파일에 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-262">Before you install the master target server, check that the **/etc/hosts** file on the virtual machine contains entries that map the local hostname to the IP addresses that are associated with all network adapters.</span></span>

1. <span data-ttu-id="65c11-263">구성 서버의 **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase**에서 암호를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-263">Copy the passphrase from **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase** on the configuration server.</span></span> <span data-ttu-id="65c11-264">그리고 다음 명령을 실행하여 같은 로컬 디렉터리에서 **passphrase.txt**로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-264">Then save it as **passphrase.txt** in the same local directory by running the following command:</span></span>

    ```
    echo <passphrase> >passphrase.txt
    ```
    <span data-ttu-id="65c11-265">예제:</span><span class="sxs-lookup"><span data-stu-id="65c11-265">Example:</span></span> 
    
    ```
    echo itUx70I47uxDuUVY >passphrase.txt
    ```

2. <span data-ttu-id="65c11-266">구성 서버의 IP 주소를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-266">Note the configuration server's IP address.</span></span> <span data-ttu-id="65c11-267">다음 단계에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-267">You need it in the next step.</span></span>

3. <span data-ttu-id="65c11-268">다음 명령을 실행하여 마스터 대상 서버를 설치하고 이 서버를 구성 서버에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-268">Run the following command to install the master target server and register the server with the configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```

    <span data-ttu-id="65c11-269">예제:</span><span class="sxs-lookup"><span data-stu-id="65c11-269">Example:</span></span> 
    
    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

    <span data-ttu-id="65c11-270">스크립트가 완료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-270">Wait until the script finishes.</span></span> <span data-ttu-id="65c11-271">마스터 대상이 성공적으로 등록되면 해당 마스터 대상이 포털의 **Site Recovery 인프라** 페이지에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-271">If the master target registers sucessfully, the master target is listed on the **Site Recovery Infrastructure** page of the portal.</span></span>


#### <a name="install-the-master-target-by-using-interactive-installation"></a><span data-ttu-id="65c11-272">대화식 설치를 사용하여 마스터 대상 설치</span><span class="sxs-lookup"><span data-stu-id="65c11-272">Install the master target by using interactive installation</span></span>

1. <span data-ttu-id="65c11-273">다음 명령을 실행하여 마스터 대상을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-273">Run the following command to install the master target.</span></span> <span data-ttu-id="65c11-274">에이전트 역할을 **마스터 대상**으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-274">For the agent role, choose **Master Target**.</span></span>

    ```
    ./install
    ```

2. <span data-ttu-id="65c11-275">설치할 기본 위치를 선택하고 **Enter** 키를 선택하여 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-275">Choose the default location for installation, and then select **Enter** to continue.</span></span>

    ![마스터 대상의 기본 설치 위치 선택](./media/site-recovery-how-to-install-linux-master-target/image17.png)

<span data-ttu-id="65c11-277">설치가 완료된 후에 명령줄을 사용하여 구성 서버를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-277">After the installation has finished, register the configuration server by using the command line.</span></span>

1. <span data-ttu-id="65c11-278">구성 서버의 IP 주소를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-278">Note the IP address of the configuration server.</span></span> <span data-ttu-id="65c11-279">다음 단계에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-279">You need it in the next step.</span></span>

2. <span data-ttu-id="65c11-280">다음 명령을 실행하여 마스터 대상 서버를 설치하고 이 서버를 구성 서버에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-280">Run the following command to install the master target server and register the server with the configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```
    <span data-ttu-id="65c11-281">예제:</span><span class="sxs-lookup"><span data-stu-id="65c11-281">Example:</span></span> 

    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

   <span data-ttu-id="65c11-282">스크립트가 완료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-282">Wait until the script finishes.</span></span> <span data-ttu-id="65c11-283">마스터 대상이 성공적으로 등록되면 해당 마스터 대상이 포털의 **Site Recovery 인프라** 페이지에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-283">If the master target is registered succesfully, the master target is listed on the **Site Recovery Infrastructure** page of the portal.</span></span>


### <a name="upgrade-the-master-target"></a><span data-ttu-id="65c11-284">마스터 대상 업그레이드</span><span class="sxs-lookup"><span data-stu-id="65c11-284">Upgrade the master target</span></span>

<span data-ttu-id="65c11-285">설치 관리자를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-285">Run the installer.</span></span> <span data-ttu-id="65c11-286">마스터 대상에 에이전트가 설치되어 있는지를 자동으로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-286">It automatically detects that the agent is installed on the master target.</span></span> <span data-ttu-id="65c11-287">업그레이드하려면 **Y**를 선택합니다.  설치가 완료된 후에 다음 명령을 사용하여 설치된 마스터 대상의 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-287">To upgrade, select **Y**.  After the setup has been completed, check the version of the master target installed by using the following command.</span></span>

    ```
    cat /usr/local/.vx_version
    ```

<span data-ttu-id="65c11-288">**버전** 필드에서 제공된 마스터 대상의 버전 번호를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-288">You can see that the **Version** field gives the version number of the master target.</span></span>

### <a name="install-vmware-tools-on-the-master-target-server"></a><span data-ttu-id="65c11-289">마스터 대상 서버에 VMware 도구 설치</span><span class="sxs-lookup"><span data-stu-id="65c11-289">Install VMware tools on the master target server</span></span>

<span data-ttu-id="65c11-290">VMware 도구가 데이터 저장소를 찾을 수 있도록 마스터 대상에 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-290">You need to install VMware tools on the master target so that it can discover the data stores.</span></span> <span data-ttu-id="65c11-291">도구가 설치되지 않으면 다시 보호 화면이 데이터 저장소에서 나열되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-291">If the tools are not installed, the reprotect screen isn't listed in the data stores.</span></span> <span data-ttu-id="65c11-292">VMware 도구를 설치한 후에 다시 부팅해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-292">After installation of the VMware tools, you need to restart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65c11-293">다음 단계</span><span class="sxs-lookup"><span data-stu-id="65c11-293">Next steps</span></span>
<span data-ttu-id="65c11-294">마스터 대상의 설치 및 등록이 완료되면 구성 서버 개요 아래에 있는 **Site Recovery 인프라**의 **마스터 대상** 섹션에 마스터 대상이 표시된 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-294">After the installation and registration of the master target has finsihed, you can see the master target appear on the **Master Target** section in **Site Recovery Infrastructure**, under the configuration server overview.</span></span>

<span data-ttu-id="65c11-295">이제 [다시 보호](site-recovery-how-to-reprotect.md)와 장애 복구를 계속 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-295">You can now proceed with [reprotection](site-recovery-how-to-reprotect.md), followed by failback.</span></span>

## <a name="common-issues"></a><span data-ttu-id="65c11-296">일반적인 문제</span><span class="sxs-lookup"><span data-stu-id="65c11-296">Common issues</span></span>

* <span data-ttu-id="65c11-297">마스터 대상 같은 관리 구성 요소에서 Storage vMotion을 설정하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-297">Make sure you do not turn on Storage vMotion on any management components such as a master target.</span></span> <span data-ttu-id="65c11-298">마스터 대상이 다시 보호 후에 이동되면 VMDK(가상 컴퓨터 디스크)를 분리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-298">If the master target moves after a successful reprotect, the virtual machine disks (VMDKs) cannot be detached.</span></span> <span data-ttu-id="65c11-299">이 경우, 장애 복구에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-299">In this case, failback fails.</span></span>

* <span data-ttu-id="65c11-300">마스터 대상에는 가상 컴퓨터에 대한 스냅숏이 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-300">The master target should not have any snapshots on the virtual machine.</span></span> <span data-ttu-id="65c11-301">스냅숏이 있으면 장애 복구에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-301">If there are snapshots, failback fails.</span></span>

* <span data-ttu-id="65c11-302">일부 고객의 일부 사용자 지정 NIC 구성 때문에 부팅 시에 네트워크 인터페이스가 비활성화되고 마스터 대상 에이전트를 초기화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-302">Due to some custom NIC configurations at some customers, the network interface is disabled during startup, and the master target agent cannot initialize.</span></span> <span data-ttu-id="65c11-303">다음 속성이 올바르게 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-303">Make sure that the following properties are correctly set.</span></span> <span data-ttu-id="65c11-304">이더넷 카드 파일의 /etc/sysconfig/network-scripts/ifcfg-eth*에서 다음 속성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="65c11-304">Check these properties in the Ethernet card file's /etc/sysconfig/network-scripts/ifcfg-eth*.</span></span>
    * <span data-ttu-id="65c11-305">BOOTPROTO=dhcp</span><span class="sxs-lookup"><span data-stu-id="65c11-305">BOOTPROTO=dhcp</span></span>
    * <span data-ttu-id="65c11-306">ONBOOT=yes</span><span class="sxs-lookup"><span data-stu-id="65c11-306">ONBOOT=yes</span></span>
