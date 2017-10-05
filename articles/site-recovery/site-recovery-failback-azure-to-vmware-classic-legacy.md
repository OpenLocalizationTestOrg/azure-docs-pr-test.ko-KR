---
title: "클래식 레거시 포털에서 Azure의 VMware VM 장애 복구 | Microsoft Docs"
description: "이 문서에서는 Azure Site Recovery를 사용하여 Azure에 복제된 VMware 가상 컴퓨터를 장애 복구하는 방법을 설명합니다."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: a63524bf-990c-42ee-8554-e017e6e67e68
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 3053fc622c6343898e2007b8aaafbe1fa8e6934e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-from-azure-to-vmware-with-azure-site-recovery-legacy"></a><span data-ttu-id="db95b-103">Azure Site Recovery를 사용하여 Azure의 VMware 가상 컴퓨터 및 물리적 서버를 VMware로 장애 복구(failback)(레거시)</span><span class="sxs-lookup"><span data-stu-id="db95b-103">Fail back VMware virtual machines and physical servers from Azure to VMware with Azure Site Recovery (legacy)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="db95b-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="db95b-104">Azure Portal</span></span>](site-recovery-failback-azure-to-vmware.md)
> * [<span data-ttu-id="db95b-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="db95b-105">Azure Classic Portal</span></span>](site-recovery-failback-azure-to-vmware-classic.md)
> * [<span data-ttu-id="db95b-106">Azure 클래식 포털(레거시)</span><span class="sxs-lookup"><span data-stu-id="db95b-106">Azure Classic Portal (Legacy)</span></span>](site-recovery-failback-azure-to-vmware-classic-legacy.md)
>
>

<span data-ttu-id="db95b-107">이 문서에서는 [Azure Site Recovery란?](site-recovery-overview.md)을 사용하여 VMware 가상 컴퓨터 및 Windows/Linux 물리적 서버를 온-프레미스 사이트에서 Azure로 복제한 후 Azure에서 온-프레미스 사이트로 장애 복구하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-107">This article describes how to fail back VMware virtual machines and Windows/Linux physical servers from Azure to your on-premises site after you've replicated from your on-premises site to Azure using [Azure Site Recovery?](site-recovery-overview.md).</span></span>

<span data-ttu-id="db95b-108">여기서는 이전 구성을 설명하며 새 자격 증명 모음에 사용하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-108">This article describes an old configuration and shouldn't be used for new vaults.</span></span>

## <a name="architecture"></a><span data-ttu-id="db95b-109">아키텍처</span><span class="sxs-lookup"><span data-stu-id="db95b-109">Architecture</span></span>
<span data-ttu-id="db95b-110">이 다이어그램은 장애 조치 및 장애 복구 시나리오를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-110">This diagram represents the failover and failback scenario.</span></span> <span data-ttu-id="db95b-111">파란색 선은 장애 조치 중에 사용되는 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-111">The blue lines are the connections used during failover.</span></span> <span data-ttu-id="db95b-112">빨간색 선은 장애 조치 중에 사용되는 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-112">The red lines are the connections used during failback.</span></span> <span data-ttu-id="db95b-113">화살표가 있는 선이 인터넷을 통해 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-113">The lines with arrows go over the internet.</span></span>

![](./media/site-recovery-failback-azure-to-vmware/vconports.png)

## <a name="before-you-start"></a><span data-ttu-id="db95b-114">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="db95b-114">Before you start</span></span>
* <span data-ttu-id="db95b-115">VMware VM 또는 물리적 서버를 통해 실패해야 하며 Azure에서 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-115">You should have failed over your VMware VMs or physical servers and they should be running in Azure.</span></span>
* <span data-ttu-id="db95b-116">Azure의 VMware 가상 컴퓨터 및 Windows/Linux 물리적 서버를 온-프레미스 기본 사이트의 VMware 가상 컴퓨터로 장애 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-116">You should note that you can only fail back VMware virtual machines and Windows/Linux physical servers from Azure to VMware virtual machines in the on-premises primary site.</span></span>  <span data-ttu-id="db95b-117">물리적 컴퓨터를 장애 복구하는 경우 Azure로 장애 조치는 이를 Azure VM으로 변환시키고 VMware로 장애 복구는 이를 VMware VM으로 변환시킵니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-117">If you're failing back a physical machine, failover to Azure will convert it to an Azure VM, and failback to VMware will convert it to a VMware VM.</span></span>

<span data-ttu-id="db95b-118">장애 복구를 설정하는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-118">Here's how you set up failback:</span></span>

1. <span data-ttu-id="db95b-119">**장애 복구 구성 요소 설정**: 온-프레미스에 vContinuum 서버를 설정하고 Azure의 구성 서버 VM을 가리키도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-119">**Set up failback components**: You'll need to set up a vContinuum server on-premises, and point it to the configuration server VM in Azure.</span></span> <span data-ttu-id="db95b-120">또한 온-프레미스 마스터 대상 서버에 데이터를 다시 보내려면 프로세스 서버를 Azure VM으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-120">You'll also set up a process server as an Azure VM to send data back to the on-premises master target server.</span></span> <span data-ttu-id="db95b-121">장애 조치를 처리하는 구성 서버와 프로세스 서버를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-121">You register the process server with the configuration server that  handled the failover.</span></span> <span data-ttu-id="db95b-122">온-프레미스 마스터 대상 서버를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-122">You install an on-premises master target server.</span></span> <span data-ttu-id="db95b-123">Windows 마스터 대상 서버가 필요한 경우 vContinuum을 설치하면 자동으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-123">If you need a Windows master target server it's set up automatically when you install vContinuum.</span></span> <span data-ttu-id="db95b-124">Linux가 필요한 경우 별도 서버에서 수동으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-124">If you need Linux you'll need to set it up manually on a separate server.</span></span>
2. <span data-ttu-id="db95b-125">**보호 및 장애 복구 사용**: 구성 요소를 설정한 후 vContinuum에서 Azure VM에 대한 장애 조치를 위해 보호를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-125">**Enable protection and failback**: After you've set up the components, in vContinuum you'll need to enable protection for failed over Azure VMs.</span></span> <span data-ttu-id="db95b-126">VM에 대한 준비 상태 확인을 실행하고 Azure에서 온-프레미스 사이트로 장애 조치를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-126">You'll run a readiness check on the VMs and run a failover from Azure to your on-premises site.</span></span> <span data-ttu-id="db95b-127">장애 복구가 완료된 후 Azure에 복제를 시작하도록 온-프레미스 컴퓨터를 다시 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-127">After failback finishes you reprotect on-premises machines so that they start replicating to Azure.</span></span>

## <a name="step-1-install-vcontinuum-on-premises"></a><span data-ttu-id="db95b-128">1단계: 온-프레미스에 vContinuum 설치</span><span class="sxs-lookup"><span data-stu-id="db95b-128">Step 1: Install vContinuum on-premises</span></span>
<span data-ttu-id="db95b-129">온-프레미스에 vContinuum 서버를 설치하고 구성 서버를 가리키도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-129">You'll need to install a vContinuum server on premises and point it to the configuration server.</span></span>

1. <span data-ttu-id="db95b-130">[VContinuum을 다운로드합니다](http://go.microsoft.com/fwlink/?linkid=526305).</span><span class="sxs-lookup"><span data-stu-id="db95b-130">[Download vContinuum](http://go.microsoft.com/fwlink/?linkid=526305).</span></span>
2. <span data-ttu-id="db95b-131">그런 다음 [vContinuum 업데이트](http://go.microsoft.com/fwlink/?LinkID=533813) 버전을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-131">Then download the [vContinuum update](http://go.microsoft.com/fwlink/?LinkID=533813) version.</span></span>
3. <span data-ttu-id="db95b-132">최신 버전의 vContinuum을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-132">Install the latest version of vContinuum.</span></span> <span data-ttu-id="db95b-133">**Welcome** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-133">On the **Welcome** page click **Next**.</span></span>
    ![](./media/site-recovery-failback-azure-to-vmware/image2.png)
4. <span data-ttu-id="db95b-134">마법사의 첫 번째 페이지에서 CX 서버 IP 주소 및 CX 서버 포트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-134">On the first page of the wizard specify the CX server IP address and the CX server port.</span></span> <span data-ttu-id="db95b-135">**HTTPS 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-135">Select **Use HTTPS**.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image3.png)
5. <span data-ttu-id="db95b-136">Azure에서 구성 서버 VM의 **대시보드** 탭에서 구성 서버 IP 주소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-136">Find the configuration server IP address on the **Dashboard** tab of the configuration server VM in Azure.</span></span>
   ![](./media/site-recovery-failback-azure-to-vmware/image4.png)
6. <span data-ttu-id="db95b-137">Azure에서 구성 서버 VM의 **끝점** 탭에서 구성 서버 HTTPS 공용 포트를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-137">Find the configuration server HTTPS public port on the **Endpoints** tab of the configuration server VM in Azure.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image5.png)
7. <span data-ttu-id="db95b-138">**CS 암호 상세 사항** 페이지에서 구성 서버를 등록할 때 적어둔 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-138">On the **CS Passphrase Details** page specify the passphrase that you noted down when you registered the configuration server.</span></span> <span data-ttu-id="db95b-139">기억하지 못하는 경우 구성 서버 VM의 **C:\\Program Files (x86)\\InMage Systems\\private\\connection.passphrase**에서 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-139">If you don't remember it check it in **C:\\Program Files (x86)\\InMage Systems\\private\\connection.passphrase** on the configuration server VM.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image6.png)
8. <span data-ttu-id="db95b-140">**대상 위치 선택** 페이지에서 vContinuum 서버를 설치하려는 위치를 지정하고 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-140">In the **Select Destination Location** page specify where you want to install the vContinuum server and click **Install**.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image7.png)
9. <span data-ttu-id="db95b-141">설치가 완료되면 vContinuum을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-141">After installation completes, you can launch vContinuum.</span></span>
    ![](./media/site-recovery-failback-azure-to-vmware/image8.png)

## <a name="step-2-install-a-process-server-in-azure"></a><span data-ttu-id="db95b-142">2단계: Azure에 프로세스 서버 설치</span><span class="sxs-lookup"><span data-stu-id="db95b-142">Step 2: Install a process server in Azure</span></span>
<span data-ttu-id="db95b-143">프로세스 서버를 Azure에 설치해야 Azure 내의 VM이 데이터를 온-프레미스 마스터 대상 서버에 다시 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-143">You need to install a process server in Azure so that the VMs in Azure can send the data back to an on-premises master target server.</span></span>

1. <span data-ttu-id="db95b-144">Azure의 **구성 서버** 페이지에서 선택하여 새 프로세스 서버를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-144">On the **Configuration Servers** page in Azure, select to add a new process server.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image9.png)
2. <span data-ttu-id="db95b-145">프로세스 서버 이름, 이름 및 암호를 지정하여 관리자로 가상 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-145">Specify a process server name, and a name and password to connect to the virtual machine as an administrator.</span></span> <span data-ttu-id="db95b-146">프로세스 서버를 등록하려는 구성 서버를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-146">Select the configuration server to which you want to register the process server.</span></span> <span data-ttu-id="db95b-147">이 서버는 가상 컴퓨터를 보호하고 장애 조치(failover)하는 데 사용하는 서버와 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-147">This should be the same server you're using to protect and fail over your virtual machines.</span></span>
3. <span data-ttu-id="db95b-148">프로세스 서버가 배포되어야 하는 Azure 네트워크를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-148">Specify the Azure network in which the process server should be deployed.</span></span> <span data-ttu-id="db95b-149">구성 서버와 동일한 네트워크여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-149">It should be the same network as the configuration server.</span></span> <span data-ttu-id="db95b-150">선택한 서브넷에서 고유한 IP 주소를 지정하고 배포를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-150">Specify a unique IP address selected subnet and begin deployment.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image10.png)
4. <span data-ttu-id="db95b-151">프로세스 서버를 배포하기 위한 작업이 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-151">A job is triggered to deploy the process server.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image11.png)
5. <span data-ttu-id="db95b-152">프로세스 서버가 Azure에 배포되면 지정한 자격 증명을 사용하여 서버에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-152">After the process server is deployed in Azure you can log into the server using the credentials you specified.</span></span> <span data-ttu-id="db95b-153">온-프레미스 프로세스 서버를 등록한 것과 같은 방식으로 프로세스 서버를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-153">Register the process server in the same way you registered the on-premises process server.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image12.png)

> [!NOTE]
> <span data-ttu-id="db95b-154">장애 복구 중에 등록된 서버는 Site Recovery의 VM 속성 아래에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-154">The servers registered during failback won't be visible under VM properties in Site Recovery.</span></span> <span data-ttu-id="db95b-155">등록된 구성 서버의 **서버** 탭 아래에서만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-155">They are only visible under the **Servers** tab of the configuration server to which they're registered.</span></span> <span data-ttu-id="db95b-156">프로세스 서버가 탭에 표시될 때까지 약 10-15분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-156">It can take about 10-15 minutes until they the process server appears on the tab.</span></span>
>
>

## <a name="step-3-install-a-master-target-server-on-premises"></a><span data-ttu-id="db95b-157">3단계: 온-프레미스에 마스터 대상 서버 설치</span><span class="sxs-lookup"><span data-stu-id="db95b-157">Step 3: Install a master target server on-premises</span></span>
<span data-ttu-id="db95b-158">원본 가상 컴퓨터 운영 체제에 따라 Linux 또는 Windows 마스터 대상 서버를 온-프레미스에 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-158">Depending on your source virtual machines operating system, you need to install a Linux or a Windows master target server on-premises.</span></span>

### <a name="deploy-a-windows-master-target-server"></a><span data-ttu-id="db95b-159">Windows 마스터 대상 서버 배포</span><span class="sxs-lookup"><span data-stu-id="db95b-159">Deploy a Windows master target server</span></span>
<span data-ttu-id="db95b-160">Windows 마스터 대상은 이미 vContinuum 설정에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-160">A Windows master target is already bundled with vContinuum setup.</span></span> <span data-ttu-id="db95b-161">vContinuum을 설치하면 마스터 대상이 동일한 컴퓨터에 배포되며 구성 서버에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-161">When you install the vContinuum, a master server is also deployed on the same machine and registered to the configuration server.</span></span>

1. <span data-ttu-id="db95b-162">배포를 시작하려면 Azure에서 VM을 복구하고자 하는 ESX 호스트에 빈 컴퓨터 온-프레미스를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-162">To begin deployment, create an empty machine on-premises on the ESX host onto which you want to recover the VMs from Azure.</span></span>
2. <span data-ttu-id="db95b-163">VM에 최소 2개의 디스크가 연결되어 있는지 확인하십시오. 하나는 운영 체제에, 다른 것은 보존 드라이브에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-163">Ensure that there are at least two disks attached to the VM – one is used for the operating system and the other is used for the retention drive.</span></span>
3. <span data-ttu-id="db95b-164">운영 체제를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-164">Install the operating system.</span></span>
4. <span data-ttu-id="db95b-165">서버에 vContinuum을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-165">Install the vContinuum on the server.</span></span> <span data-ttu-id="db95b-166">이 또한 마스터 대상 서버 설치를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-166">This also completes installation of the master target server.</span></span>

### <a name="deploy-a-linux-master-target-server"></a><span data-ttu-id="db95b-167">Linux 마스터 대상 서버 배포</span><span class="sxs-lookup"><span data-stu-id="db95b-167">Deploy a Linux master target server</span></span>
1. <span data-ttu-id="db95b-168">배포를 시작하려면 Azure에서 VM을 복구하고자 하는 ESX 호스트에 빈 컴퓨터 온-프레미스를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-168">To begin deployment, create an empty machine on-premises on the ESX host onto which you want to recover the VMs from Azure.</span></span>
2. <span data-ttu-id="db95b-169">VM에 최소 2개의 디스크가 연결되어 있는지 확인하십시오. 하나는 운영 체제에, 다른 것은 보존 드라이브에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-169">Ensure that there are at least two disks attached to the VM – one is used for the operating system and the other is used for the retention drive.</span></span>
3. <span data-ttu-id="db95b-170">Linux 운영 체제를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-170">Install the Linux operating system.</span></span> <span data-ttu-id="db95b-171">Linux 마스터 대상 시스템은 루트 또는 보존 저장소 공간에 LVM을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-171">The Linux master target system should not use LVM for root or retention storage spaces.</span></span> <span data-ttu-id="db95b-172">Linux 마스터 대상 서버는 기본적으로 LVM 파티션/디스크 검색을 방지하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-172">A Linux master target server is configured to avoid LVM partitions/disks discovery by default.</span></span>
4. <span data-ttu-id="db95b-173">만들 수 있는 파티션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-173">Partitions that you can create:</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image13.png)
5. <span data-ttu-id="db95b-174">마스터 대상 설치를 시작하기 전에 아래 사후 설치 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-174">Carry out the below post installation steps before beginning the master target installation.</span></span>

#### <a name="post-os-installation-steps"></a><span data-ttu-id="db95b-175">사후 OS 설치 단계</span><span class="sxs-lookup"><span data-stu-id="db95b-175">Post OS Installation Steps</span></span>
<span data-ttu-id="db95b-176">Linux 가상 컴퓨터에서 각 SCSI 하드 디스크에 대해 SCSI ID를 가져오려면 다음과 같이 “disk.EnableUUID = TRUE” 매개 변수를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-176">To get the SCSI ID’s for each of SCSI hard disk in a Linux virtual machine, enable the parameter “disk.EnableUUID = TRUE” as follows:</span></span>

1. <span data-ttu-id="db95b-177">가상 컴퓨터를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-177">Shut down your virtual machine.</span></span>
2. <span data-ttu-id="db95b-178">왼쪽 패널에서 VM 항목을 마우스 오른쪽 단추로 클릭하고 **설정 편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-178">Right-click the VM entry in the left-hand panel > **Edit Settings**.</span></span>
3. <span data-ttu-id="db95b-179">**옵션** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-179">Click the **Options** tab.</span></span> <span data-ttu-id="db95b-180">**고급\>일반 항목** > **구성 매개 변수**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-180">Select **Advanced\>General item** > **Configuration Parameters**.</span></span> <span data-ttu-id="db95b-181">**구성 매개 변수** 옵션은 컴퓨터가 종료될 때만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-181">The **Configuration Parameters** option is only available when the machine is shut down.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image14.png)
4. <span data-ttu-id="db95b-182">**disk.EnableUUID** 가 있는 행이 존재하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-182">Checks whether a row with **disk.EnableUUID** exists.</span></span> <span data-ttu-id="db95b-183">존재하며 **False**로 설정된 경우 **True**로 설정합니다(대/소문자 구분 안 함).</span><span class="sxs-lookup"><span data-stu-id="db95b-183">If it does and is set to **False** then set it to **True** (not case sensitive).</span></span> <span data-ttu-id="db95b-184">존재하며 true로 설정되어 있는 경우 **취소** 를 클릭하고 부팅된 후 게스트 운영 체제 내에서SCSI 명령을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-184">If exists and is set to true, click **Cancel** and test the SCSI command inside the guest operating system after it's booted up.</span></span> <span data-ttu-id="db95b-185">존재하지 않는 경우 **행 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-185">If doesn't exist click **Add Row**.</span></span>
5. <span data-ttu-id="db95b-186">**이름** 열에 disk.EnableUUID를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-186">Add disk.EnableUUID in the **Name** column.</span></span> <span data-ttu-id="db95b-187">해당 값을 TRUE로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-187">Set its value as TRUE.</span></span> <span data-ttu-id="db95b-188">위의 값을 큰따옴표와 함께 추가하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="db95b-188">Don't add the above values along with double-quotes.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image15.png)

#### <a name="download-and-install-the-additional-packages"></a><span data-ttu-id="db95b-189">추가 패키지 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="db95b-189">Download and install the additional packages</span></span>
<span data-ttu-id="db95b-190">참고: 추가 패키지를 다운로드하고 설치하기 전에 시스템이 인터넷에 연결되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-190">NOTE: Make sure the system has internet connectivity before downloading and installing the additional packages.</span></span>

<span data-ttu-id="db95b-191">\# yum install -y xfsprogs perl lsscsi rsync wget kexec-tools</span><span class="sxs-lookup"><span data-stu-id="db95b-191">\# yum install -y xfsprogs perl lsscsi rsync wget kexec-tools</span></span>

<span data-ttu-id="db95b-192">이 명령은 CentOS 6.6 저장소에서 이러한 15개의 패키지를 다운로드 및 설치:</span><span class="sxs-lookup"><span data-stu-id="db95b-192">This command downloads these 15 packages from CentOS 6.6 repository and installs them:</span></span>

<span data-ttu-id="db95b-193">bc-1.06.95-1.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="db95b-193">bc-1.06.95-1.el6.x86\_64.rpm</span></span>

<span data-ttu-id="db95b-194">busybox-1.15.1-20.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="db95b-194">busybox-1.15.1-20.el6.x86\_64.rpm</span></span>

<span data-ttu-id="db95b-195">elfutils-libs-0.158-3.2.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="db95b-195">elfutils-libs-0.158-3.2.el6.x86\_64.rpm</span></span>

<span data-ttu-id="db95b-196">kexec-tools-2.0.0-280.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="db95b-196">kexec-tools-2.0.0-280.el6.x86\_64.rpm</span></span>

<span data-ttu-id="db95b-197">lsscsi-0.23-2.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="db95b-197">lsscsi-0.23-2.el6.x86\_64.rpm</span></span>

<span data-ttu-id="db95b-198">lzo-2.03-3.1.el6\_5.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="db95b-198">lzo-2.03-3.1.el6\_5.1.x86\_64.rpm</span></span>

<span data-ttu-id="db95b-199">perl-5.10.1-136.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="db95b-199">perl-5.10.1-136.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="db95b-200">perl-Module-Pluggable-3.90-136.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="db95b-200">perl-Module-Pluggable-3.90-136.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="db95b-201">perl-Pod-Escapes-1.04-136.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="db95b-201">perl-Pod-Escapes-1.04-136.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="db95b-202">perl-Pod-Simple-3.13-136.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="db95b-202">perl-Pod-Simple-3.13-136.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="db95b-203">perl-libs-5.10.1-136.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="db95b-203">perl-libs-5.10.1-136.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="db95b-204">perl-version-0.77-136.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="db95b-204">perl-version-0.77-136.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="db95b-205">rsync-3.0.6-12.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="db95b-205">rsync-3.0.6-12.el6.x86\_64.rpm</span></span>

<span data-ttu-id="db95b-206">snappy-1.1.0-1.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="db95b-206">snappy-1.1.0-1.el6.x86\_64.rpm</span></span>

<span data-ttu-id="db95b-207">wget-1.12-5.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="db95b-207">wget-1.12-5.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="db95b-208">원본 컴퓨터가 루트 또는 부팅 장치에 Reiser 또는 XFS 파일 시스템을 사용하는 경우 보호하기 전에 다음 패키지를 Linux 마스터 대상에 다운로드하고 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-208">If the source machine uses Reiser or XFS filesystem for the root or boot device, then following packages should be downloaded and installed on Linux master target prior to protection.</span></span>

<span data-ttu-id="db95b-209">\# cd /usr/local</span><span class="sxs-lookup"><span data-stu-id="db95b-209">\# cd /usr/local</span></span>

<span data-ttu-id="db95b-210">\# wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm></span><span class="sxs-lookup"><span data-stu-id="db95b-210">\# wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm></span></span>

<span data-ttu-id="db95b-211">\# wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm></span><span class="sxs-lookup"><span data-stu-id="db95b-211">\# wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm></span></span>

<span data-ttu-id="db95b-212">\# rpm -ivh kmod-reiserfs-0.0-1.el6.elrepo.x86\_64.rpm reiserfs-utils-3.6.21-1.el6.elrepo.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="db95b-212">\# rpm -ivh kmod-reiserfs-0.0-1.el6.elrepo.x86\_64.rpm reiserfs-utils-3.6.21-1.el6.elrepo.x86\_64.rpm</span></span>

<span data-ttu-id="db95b-213">\# wget <http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_64.rpm></span><span class="sxs-lookup"><span data-stu-id="db95b-213">\# wget <http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_64.rpm></span></span>

<span data-ttu-id="db95b-214">\# rpm -ivh xfsprogs-3.1.1-16.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="db95b-214">\# rpm -ivh xfsprogs-3.1.1-16.el6.x86\_64.rpm</span></span>

#### <a name="apply-custom-configuration-changes"></a><span data-ttu-id="db95b-215">사용자 지정 구성 변경 내용 적용</span><span class="sxs-lookup"><span data-stu-id="db95b-215">Apply custom configuration changes</span></span>
<span data-ttu-id="db95b-216">이러한 변경 내용을 적용하기 전에 이전 섹션을 완료했는지 확인한 후 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-216">Before applying these changes make sure you've completed the previous section, then follow these steps:</span></span>

1. <span data-ttu-id="db95b-217">RHEL 6-64 통합 에이전트 바이너리를 새롭게 생성한 OS에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-217">Copy the RHEL 6-64 Unified Agent binary to the newly created OS.</span></span>
2. <span data-ttu-id="db95b-218">**tar -zxvf \<파일 이름\>** 명령을 실행하여 바이너리를 untar합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-218">Run this command to untar the binary: **tar -zxvf \<File name\>**</span></span>
3. <span data-ttu-id="db95b-219">\# **chmod 755 ./ApplyCustomChanges.sh** 명령을 실행하여 사용 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-219">Run this command to give permissions: \# **chmod 755 ./ApplyCustomChanges.sh**</span></span>
4. <span data-ttu-id="db95b-220">**\# ./ApplyCustomChanges.sh** 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-220">Run the script: **\# ./ApplyCustomChanges.sh**.</span></span> <span data-ttu-id="db95b-221">서버에서 스크립트를 한 번만 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-221">Run the script only once on the server.</span></span> <span data-ttu-id="db95b-222">스크립트가 실행된 후 서버를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-222">Restart the server after the script runs.</span></span>

### <a name="install-the-linux-server"></a><span data-ttu-id="db95b-223">Linux 서버 설치</span><span class="sxs-lookup"><span data-stu-id="db95b-223">Install the Linux server</span></span>
1. <span data-ttu-id="db95b-224">[다운로드](http://go.microsoft.com/fwlink/?LinkID=529757) 합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-224">[Download](http://go.microsoft.com/fwlink/?LinkID=529757) the installation file.</span></span>
2. <span data-ttu-id="db95b-225">선택한 sftp 클라이언트 유틸리티를 사용하여 파일을 Linux 마스터 대상 가상 컴퓨터에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-225">Copy the file to the Linux Master Target virtual machine using an sftp client utility of your choice.</span></span> <span data-ttu-id="db95b-226">또는 Linux 마스터 대상 가상 컴퓨터에 로그인 하여 wget을 사용하여 제공된 링크에서 설치 패키지를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-226">Alternately you can log onto the Linux master target virtual machine and use wget to download the installation package from the provided link</span></span>
3. <span data-ttu-id="db95b-227">선택한 ssh 클라이언트를 사용하여 Linux 마스터 대상 서버 가상 컴퓨터에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-227">Log onto the Linux master target server virtual machine using an ssh client of your choice</span></span>
4. <span data-ttu-id="db95b-228">VPN 연결을 통해 Linux 마스터 대상 서버를 배포한 Azure 네트워크에 연결하는 경우 가상 컴퓨터 **대시보드** 탭 및 포트 22에서 찾을 수 있는 서버에 대한 내부 IP 주소를 사용하여 Secure Shell을 통해 Linux 마스터 대상 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-228">If you're connected to the Azure network on which you deployed your Linux master target server through a VPN connection then use the internal IP address for the server that you can find in the virtual machine **Dashboard** tab, and port 22 to connect to the Linux master target Server using Secure Shell.</span></span>
5. <span data-ttu-id="db95b-229">공용 인터넷 연결을 통해 Linux 마스터 대상 서버에 연결하는 경우 Linux 마스터 대상 서버의 공용 가상 IP 주소(가상 컴퓨터 **대시보드** 탭에서) 및 ssh용으로 생성된 공용 끝점을 사용하여 Linux 서버에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-229">If you're connecting to the Linux master target server over a public internet connection use the Linux master target server’s public virtual IP address (from the virtual machines **Dashboard** tab) and the public endpoint created for ssh to login to the Linux servder.</span></span>
6. <span data-ttu-id="db95b-230">설치 관리자 파일을 포함하는 디렉터리에서 *“tar –xvzf Microsoft-ASR\_UA\_8.2.0.0\_RHEL6-64\”*를 실행하여 GZip 압축된 Linux 마스터 대상 서버 설치 프로그램 tar 보관 파일에서 파일을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-230">Extract the files from the gzipped Linux master target Server installer tar archive by running: *“tar –xvzf Microsoft-ASR\_UA\_8.2.0.0\_RHEL6-64\”* from the directory that contains the installer file.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image16.png)
7. <span data-ttu-id="db95b-231">설치 프로그램 파일을 다른 디렉터리로 추출했다면 tar 압축 파일의 내용이 추출된 디렉터리로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-231">If you extracted the installer files to a different directory change to the directory to which the contents of the tar archive were extracted.</span></span> <span data-ttu-id="db95b-232">이 디렉터리 경로에서 “sudo ./install.sh”를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-232">From this directory path run “sudo ./install.sh”.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image17.png)
8. <span data-ttu-id="db95b-233">주 역할을 선택하라는 메시지가 나타나면 **2(마스터 대상)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-233">When prompted to choose a primary role select **2 (Master Target)**.</span></span> <span data-ttu-id="db95b-234">다른 대화형 설치 옵션은 기본값으로 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-234">Leave the other interactive install options at their default values.</span></span>
9. <span data-ttu-id="db95b-235">설치가 계속되고 호스트 구성 인터페이스가 나타날 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-235">Wait for installation to continue and the Host Config Interface to appear.</span></span> <span data-ttu-id="db95b-236">Linux 마스터 대상 서버에 대한 호스트 구성 유틸리티는 명령줄 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-236">The Host Configuration utility for the Linux master sarget Server is a command line utility.</span></span> <span data-ttu-id="db95b-237">ssh 클라이언트 유틸리티 창의 크기를 조정하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="db95b-237">Don’t resize the ssh client utility window.</span></span> <span data-ttu-id="db95b-238">화살표 키를 사용하여 **전역** 옵션을 선택하고 키보드에서 ENTER 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-238">Use the arrow keys to select the **Global** option and press ENTER on your keyboard.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image18.png)

    ![](./media/site-recovery-failback-azure-to-vmware/image19.png)
10. <span data-ttu-id="db95b-239">**IP** 필드에 구성 서버의 내부 IP 주소를 입력한 다음(구성 서버 VM의 **대시보드** 탭에서 찾을 수 있음) ENTER 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-239">In the field **IP** enter the Internal IP address of the configuration server (you can find it in the **Dashboard** tab of the configuration server VM) and press ENTER.</span></span> <span data-ttu-id="db95b-240">**포트**에 **22**를 입력하고 ENTER 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-240">In **Port** enter **22** and press ENTER.</span></span>
11. <span data-ttu-id="db95b-241">**HTTPS 사용**을 **예**로 두고 ENTER 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-241">Leave **Use HTTPS** as **Yes**, and press ENTER.</span></span>
12. <span data-ttu-id="db95b-242">구성 서버에서 생성된 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-242">Enter the Passphrase that was generated on the configuration server.</span></span> <span data-ttu-id="db95b-243">Windows 컴퓨터에서 PUTTY 클라이언트를 사용하여 Linux 가상 컴퓨터에 ssh를 실행하는 경우 Shift + Insert를 사용하여 클립보드의 내용을 붙여넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-243">If you're using a PUTTY client from a Windows machine to ssh to the Linux virtual machine you can use Shift+Insert to paste the contents of the clipboard.</span></span> <span data-ttu-id="db95b-244">Ctrl + C를 사용하여 로컬 클립보드에 암호를 복사하고 Shift + Insert를 사용하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-244">Copy the Passphrase to the local clipboard using Ctrl-C and use Shift+Insert to paste it.</span></span> <span data-ttu-id="db95b-245">ENTER 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-245">Press ENTER.</span></span>
13. <span data-ttu-id="db95b-246">오른쪽 화살표 키를 사용하여 종료를 찾아가서 ENTER 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-246">Use the right arrow key to navigate to quit and press ENTER.</span></span> <span data-ttu-id="db95b-247">설치가 완료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-247">Wait for installation to complete.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image20.png)

<span data-ttu-id="db95b-248">어떠한 이유로 Linux 마스터 대상 서버를 구성 서버에 등록하지 못했다면 /usr/local/ASR/Vx/bin/hostconfigcli로부터 호스트 구성 유틸리티를 실행하여 다시 수행할 수 있습니다(먼저 chmod를 슈퍼 사용자로 실행하여 이 디렉터리에 대한 액세스 권한을 설정해야 함).</span><span class="sxs-lookup"><span data-stu-id="db95b-248">If for some reason you failed to register your Linux master target server to the configuration server you can do so again by running the host configuration utility from /usr/local/ASR/Vx/bin/hostconfigcli (you'll first need to set access permissions to this directory by running chmod as a super user).</span></span>

#### <a name="validate-master-target-registration"></a><span data-ttu-id="db95b-249">마스터 대상 등록의 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="db95b-249">Validate master target registration</span></span>
<span data-ttu-id="db95b-250">Azure Site Recovery 자격 증명 모음 > **구성 서버** > **서버 세부 정보**에서 마스터 대상 서버가 구성 서버로 성공적으로 등록되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-250">You can validate that the master target server was registered successfully to the configuration server in Azure Site Recovery vault > **Configuration Server** > **Server Details**.</span></span>

> [!NOTE]
> <span data-ttu-id="db95b-251">마스터 대상 서버를 등록한 후 Azure에서 가상 컴퓨터가 삭제되었을 수 있거나 끝점이 제대로 구성되지 않았다는 구성 오류가 발생하는 경우 마스터 대상이 Azure에 배포될 때 Azure 끝점에서 마스터 대상 구성이 감지되어도 온-프레미스 마스터 대상 서버 온-프레미스에 대해 true가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-251">After registering the master target server, if you receive configuration errors that the virtual machine might have been deleted from Azure or that endpoints are not properly configured, this is because although the master target configuration is detected by the Azure dndpoints when the master target is deployed in Azure, this isn't true for an on-premises master target server on-premises.</span></span> <span data-ttu-id="db95b-252">장애 복구에 영향을 주지 않으며 이러한 오류는 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-252">This won't affect failback and you can ignore these errors.</span></span>
>
>

## <a name="step-4-protect-the-virtual-machines-to-the-on-premises-site"></a><span data-ttu-id="db95b-253">4단계: 온-프레미스 사이트에 가상 컴퓨터 보호</span><span class="sxs-lookup"><span data-stu-id="db95b-253">Step 4: Protect the virtual machines to the on-premises site</span></span>
<span data-ttu-id="db95b-254">장애 복구 전에 온-프레미스 사이트에 VM을 보호해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-254">You need to protect VMs to the on-premises site before you fail back.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="db95b-255">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="db95b-255">Before you begin</span></span>
<span data-ttu-id="db95b-256">VM이 Azure로 장애 조치되면 페이지 파일에 임시 드라이브가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-256">When a VM is failed over to Azure, it adds an extra temp drive for page file.</span></span> <span data-ttu-id="db95b-257">이것은 이미 페이지 파일 전용 드라이브를 가지고 있을 수도 있으므로 일반적으로 장애 조치된 VM에서 필요로 하지 않는 추가 드라이브입니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-257">This is an extra drive that is typically not required by your failed over VM since it might already have a drive dedicated for the page file.</span></span> <span data-ttu-id="db95b-258">가상 컴퓨터의 역방향 보호를 시작하기 전에 보호되지 않도록 드라이브가 오프라인으로 가져와지도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-258">Before you begin reverse protection of the virtual machines, you need to ensure that this drive is taken offline so that it does not get protected.</span></span> <span data-ttu-id="db95b-259">다음과 같이 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-259">Do this as follows:</span></span>

1. <span data-ttu-id="db95b-260">컴퓨터 관리를 열고 저장소 관리를 선택하여 온라인 디스크와 컴퓨터에 연결된 디스크를 나열시킵니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-260">Open Computer Management and select Storage Management so that it lists the disks online and attached to the machine.</span></span>
2. <span data-ttu-id="db95b-261">컴퓨터에 연결된 임시 디스크를 선택하고 오프라인으로 전환을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-261">Select the temporary disk attached to the machine and choose to bring it offline.</span></span>

### <a name="protect-the-vms"></a><span data-ttu-id="db95b-262">VM 보호</span><span class="sxs-lookup"><span data-stu-id="db95b-262">Protect the VMs</span></span>
1. <span data-ttu-id="db95b-263">Azure 포털에서 가상 컴퓨터의 상태를 확인하여 장애 조치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-263">In the Azure portal, check the states of the virtual machine to ensure that they're failed over.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image21.png)
2. <span data-ttu-id="db95b-264">컴퓨터에 vContinuum을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-264">Launch vContinuum on your machine.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image8.png)
3. <span data-ttu-id="db95b-265">**새 보호** 를 클릭하고 작업 시스템 유형을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-265">Click **New Protection** and select the operation system type, the</span></span>
4. <span data-ttu-id="db95b-266">열리는 새 창에서 장애 복구하려는 VM에 대해 **OS 유형** > **세부 정보**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-266">In the new window that open select the **OS type** > **Get Details** for the VMs you want to fail back.</span></span> <span data-ttu-id="db95b-267">**주 서버 세부 정보**에서 보호하려는 가상 컴퓨터를 식별하고 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-267">In **Primary server details**, identify and select the virtual machines that you want to protect.</span></span> <span data-ttu-id="db95b-268">VM이 장애 조치 전에 있었던 vCenter 호스트 이름 아래에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-268">VMs are listed under the vCenter host name that they were on before failover.</span></span>
5. <span data-ttu-id="db95b-269">가상 컴퓨터를 선택하여 보호하면(이미 Azure에 장애 조치된 경우) 팝업 창이 가상 컴퓨터에 대한 두 가지 항목을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-269">When you select a virtual machine to protect (and it has already failed over to Azure) a pop-up window provides two entries for the virtual machine.</span></span> <span data-ttu-id="db95b-270">이것은 구성 서버가 등록된 가상 컴퓨터의 인스턴스 2개를 발견했기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-270">This is because the configuration server detects two instances of the virtual machines registered to it.</span></span> <span data-ttu-id="db95b-271">올바른 VM을 보호할 수 있도록 온-프레미스 VM에 대한 항목을 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-271">You need to remove the entry for the on-premises VM so that you can protect the correct VM.</span></span> <span data-ttu-id="db95b-272">여기에서 올바른 Azure VM 항목을 식별하려면 Azure VM에 로그인하여 C:\Program Files (x86)\Microsoft Azure Site Recovery\Application Data\etc로 이동합니다. 파일 drscout.conf에서 호스트 ID를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-272">To identify the correct Azure VM entry here, you can log into the Azure VM and go to C:\Program Files (x86)\Microsoft Azure Site Recovery\Application Data\etc. In the file drscout.conf , identify the host ID.</span></span> <span data-ttu-id="db95b-273">vContinuum 대화 상자에서 VM에서 호스트 ID를 발견한 항목을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-273">In the vContinuum dialog, keep the entry for which you found the host ID on  the VM.</span></span> <span data-ttu-id="db95b-274">다른 모든 항목을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-274">Delete all other entries.</span></span> <span data-ttu-id="db95b-275">올바른 VM을 선택하기 위해 해당 IP 주소를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-275">To select the correct VM you can refer to its IP address.</span></span> <span data-ttu-id="db95b-276">IP 주소 범위 온-프레미스는 온-프레미스 VM이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-276">The IP address range on-premises will be the on-premises VM.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image22.png)

   ![](./media/site-recovery-failback-azure-to-vmware/image23.png)
6. <span data-ttu-id="db95b-277">VCenter 서버에서 가상 컴퓨터를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-277">On the vCenter server stop the virtual machine.</span></span> <span data-ttu-id="db95b-278">또한 온-프레미스에서 VM을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-278">You can also delete the VMs on-premises.</span></span>
7. <span data-ttu-id="db95b-279">그런 다음 VM을 보호하고자 하는 온-프레미스 MT 서버를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-279">Then specify the on-premises MT server to which you want to protect the VMs.</span></span> <span data-ttu-id="db95b-280">이를 위해 장애 복구하려는 vCenter 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-280">To do this, connect to the vCenter server to which you want to fail back.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image24.png)
8. <span data-ttu-id="db95b-281">VM을 복구하려는 호스트를 기반으로 마스터 대상 서버를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-281">Select the master target server based on the host to which you want to recover the VM.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image24.png)
9. <span data-ttu-id="db95b-282">각 가상 컴퓨터에 대해 복제 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-282">Provide the replication option for each of the virtual machines.</span></span> <span data-ttu-id="db95b-283">이를 위해 VM이 복구되는 복구 쪽 데이터 저장소를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-283">To do this you need to select the recovery side datastore to which the VMs will be recovered.</span></span> <span data-ttu-id="db95b-284">표에서 각 VM에 대해 제공해야 하는 다양한 옵션을 요약합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-284">The table summarizes the different options you need to provide for each VM.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image25.png)

   | <span data-ttu-id="db95b-285">**옵션**</span><span class="sxs-lookup"><span data-stu-id="db95b-285">**Option**</span></span> | <span data-ttu-id="db95b-286">**옵션이 권장하는 값**</span><span class="sxs-lookup"><span data-stu-id="db95b-286">**Option recommended value**</span></span> |
   | --- | --- |
   |  <span data-ttu-id="db95b-287">프로세스 서버 IP 주소</span><span class="sxs-lookup"><span data-stu-id="db95b-287">Process server IP address</span></span> |<span data-ttu-id="db95b-288">Azure에 배포된 프로세스 서버를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-288">Select the process server deployed in Azure</span></span> |
   |  <span data-ttu-id="db95b-289">보존 크기(MB)</span><span class="sxs-lookup"><span data-stu-id="db95b-289">Retention size in MB</span></span> | |
   |  <span data-ttu-id="db95b-290">보존 값</span><span class="sxs-lookup"><span data-stu-id="db95b-290">Retention value</span></span> |<span data-ttu-id="db95b-291">1</span><span class="sxs-lookup"><span data-stu-id="db95b-291">1</span></span> |
   |  <span data-ttu-id="db95b-292">날짜/시간</span><span class="sxs-lookup"><span data-stu-id="db95b-292">Days/Hours</span></span> |<span data-ttu-id="db95b-293">일</span><span class="sxs-lookup"><span data-stu-id="db95b-293">Days</span></span> |
   |  <span data-ttu-id="db95b-294">일관성 간격</span><span class="sxs-lookup"><span data-stu-id="db95b-294">Consistency interval</span></span> |<span data-ttu-id="db95b-295">1</span><span class="sxs-lookup"><span data-stu-id="db95b-295">1</span></span> |
   |  <span data-ttu-id="db95b-296">대상 데이터 저장소를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-296">Select target datastore</span></span> |<span data-ttu-id="db95b-297">복구 쪽에서 사용할 수 있는 데이터 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-297">The datastore available on the recovery site.</span></span> <span data-ttu-id="db95b-298">이 데이터 저장소는 공간이 충분해야 하며 가상 컴퓨터를 복원하려는 ESX 호스트에서 제공되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-298">The data store should have enough space, and be available to the ESX host on which you want to restore the virtual machine.</span></span> |
10. <span data-ttu-id="db95b-299">온-프레미스 사이트로 장애 조치 후 가상 컴퓨터가 입수하는 속성을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-299">Configure the properties that the virtual machine will acquire after failover to on-premises site.</span></span> <span data-ttu-id="db95b-300">속성은 다음 표에 요약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-300">The properties are summarized in the following table.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image26.png)

    | <span data-ttu-id="db95b-301">**속성**</span><span class="sxs-lookup"><span data-stu-id="db95b-301">**Property**</span></span> | <span data-ttu-id="db95b-302">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="db95b-302">**Details**</span></span> |
    | --- | --- |
    | <span data-ttu-id="db95b-303">네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="db95b-303">Network configuration</span></span> |<span data-ttu-id="db95b-304">검색된 각 네트워크 어댑터에 대해 선택하고 **변경** 을 클릭하여 가상 컴퓨터에 대한 장애 복구 IP 주소를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-304">For each network adapter detected, select it and click **Change** to configure the failback IP address for the virtual machine.</span></span> |
    | <span data-ttu-id="db95b-305">하드웨어 구성</span><span class="sxs-lookup"><span data-stu-id="db95b-305">Hardware Configuration</span></span> |<span data-ttu-id="db95b-306">VM에 대한 CPU 및 메모리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-306">Specify the CPU and the memory for the VM.</span></span> <span data-ttu-id="db95b-307">설정은 보호하고자 하는 모든 VM에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-307">Settings can be applied to all the VMs you are trying to protect.</span></span> <span data-ttu-id="db95b-308">CPU 및 메모리에 대해 올바른 값을 식별하려면 IAAS Vm 역할 크기를 참조하고 할당된 메모리 및 코어 수를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-308">To identify the correct values for the CPU and memory, you can refer to the IAAS VMs role size and see the number of cores and memory assigned.</span></span> |
    | <span data-ttu-id="db95b-309">표시 이름</span><span class="sxs-lookup"><span data-stu-id="db95b-309">Display name</span></span> |<span data-ttu-id="db95b-310">온-프레미스로 장애 복구 후 vCenter 인벤토리에 표시될 가상 컴퓨터의 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-310">After failback to on-premises, you can rename the virtual machines as they'll appear in the vCenter inventory.</span></span> <span data-ttu-id="db95b-311">기본 이름은 가상 컴퓨터 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-311">The default name is the virtual machine computer host name.</span></span> <span data-ttu-id="db95b-312">VM 이름을 식별하려면 보호 그룹 내 VM 목록을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-312">To identify the VM name, you can refer to the VM list in the Protection group.</span></span> |
    | <span data-ttu-id="db95b-313">NAT 구성</span><span class="sxs-lookup"><span data-stu-id="db95b-313">NAT Configuration</span></span> |<span data-ttu-id="db95b-314">아래에 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-314">Discussed in detail below</span></span> |

    ![](./media/site-recovery-failback-azure-to-vmware/image27.png)

#### <a name="configure-nat-settings"></a><span data-ttu-id="db95b-315">NAT 설정 구성</span><span class="sxs-lookup"><span data-stu-id="db95b-315">Configure NAT settings</span></span>
1. <span data-ttu-id="db95b-316">가상 컴퓨터의 보호를 활성화하려면 통신 채널 2개를 구축해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-316">To enable protection of the virtual machines, two communication channels need to be established.</span></span> <span data-ttu-id="db95b-317">첫 번째 채널은 가상 컴퓨터와 프로세스 서버 사이입니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-317">The first channel is between the virtual machine and the process server.</span></span> <span data-ttu-id="db95b-318">이 채널은 VM에서 데이터를 수집하고 마스터 대상 서버에 데이터를 전송하는 프로세스 서버에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-318">This channel collects the data from the VM and sends it to the process server which then sends the data to the master target server.</span></span> <span data-ttu-id="db95b-319">프로세스 서버와 보호할 가상 컴퓨터가 동일한 Azure 가상 네트워크에 있다면 NAT 설정을 사용하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-319">If the process server and the virtual machine to be protected are on the same Azure virtual network then you don't need to use NAT settings.</span></span> <span data-ttu-id="db95b-320">그렇지 않으면 NAT 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-320">Otherwise specify NAT settings.</span></span> <span data-ttu-id="db95b-321">Azure에서 프로세스 서버의 공용 IP 주소를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-321">View the public IP address of the process server in Azure.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image28.png)
2. <span data-ttu-id="db95b-322">두 번째 채널은 프로세스 서버와 마스터 대상 서버 사이입니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-322">The second channel is between the process server and the master target server.</span></span> <span data-ttu-id="db95b-323">NAT을 사용할 것인지 여부는 VPN 기반 연결을 사용하는지 또는 인터넷을 통해 통신하는지 여부에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-323">The option to use NAT or not depends on whether you are using a VPN based connection or communicating over the internet.</span></span> <span data-ttu-id="db95b-324">VPN을 사용하는 경우 NAt를 선택하지 마십시오. 인터넷 연결을 사용하는 경우만 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-324">Don't select NAt if you're using VPN, but only if you're using an internet connection.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image29.png)

    ![](./media/site-recovery-failback-azure-to-vmware/image30.png)
3. <span data-ttu-id="db95b-325">지정한 대로 온-프레미스 가상 컴퓨터를 삭제하지 않았으며 장애 복구를 실행하는 데이터 저장소에 여전히 기존의 VMDK가 포함되어 있다면 장애 복구 VM이 역시 새로운 위치에 생성되도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-325">If you haven't deleted the on-premises virtual machines as specified and if the datastore you are failing back to still contains the old VMDK’s then you will need to ensure that the failback VM gets created in a new place.</span></span> <span data-ttu-id="db95b-326">이를 위해 **고급** 설정을 선택하고 **폴더 이름 설정**에서 복원할 대체 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-326">To do this select the **Advanced** settings and specify an alternate Folder to restore to in **Folder Name Settings**.</span></span> <span data-ttu-id="db95b-327">다른 옵션은 기본 설정을 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-327">Leave the other options with their default settings.</span></span> <span data-ttu-id="db95b-328">모든 서버에 폴더 이름을 설정을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-328">Apply the folder name settings to all the servers.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image31.png)
4. <span data-ttu-id="db95b-329">가상 컴퓨터가 준비 검사를 실행하여 온-프레미스로 다시 보호될 준비가 되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-329">Run a Readiness Check to ensure that the virtual machines are ready to be protected back to on-premises.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image32.png)
5. <span data-ttu-id="db95b-330">완료할 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-330">Wait for it to complete.</span></span> <span data-ttu-id="db95b-331">모든 VM에서 완료되면 보호 계획에 대한 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-331">If it's successfully on all VMs you can specify a name for the protection plan.</span></span> <span data-ttu-id="db95b-332">그런 다음 **보호** 를 클릭하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-332">Then click **Protect** to begin.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image33.png)
6. <span data-ttu-id="db95b-333">vContinuum에서 진행률을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-333">You can monitor progress in vContinuum.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image34.png)
7. <span data-ttu-id="db95b-334">**보호 계획 활성화** 단계가 완료된 후 사이트 복구 포털에서 VM 보호를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-334">After the step **Activating Protection Plan** finishes you can monitor VM protection in the Site Recovery portal.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image35.png)
8. <span data-ttu-id="db95b-335">VM을 클릭하고 진행률을 모니터링하여 정확한 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-335">You can see the exact status clicking on the VM and monitoring its progress.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image36.png)

## <a name="prepare-the-failback-plan"></a><span data-ttu-id="db95b-336">장애 복구 계획 준비</span><span class="sxs-lookup"><span data-stu-id="db95b-336">Prepare the failback plan</span></span>
<span data-ttu-id="db95b-337">응용프로그램이 언제든지 온-프레미스 사이트로 장애 복구될 수 있도록 vContinuum을 사용하여 장애 복구 계획을 준비할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-337">You can prepare a failback plan using vContinuum so that the application can be failed back to the on-premises site at any time.</span></span> <span data-ttu-id="db95b-338">이러한 복구 계획은 사이트 복구의 복구 계획과 매우 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-338">These recovery plans are very similar to the recovery plans in Site Recovery.</span></span>

1. <span data-ttu-id="db95b-339">vContinuum을 시작하고 **계획 관리** > **복구**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-339">Launch vContinuum and select **Manage plans** > **Recover.**</span></span> <span data-ttu-id="db95b-340">장애 조치 VM에 사용된 모든 계획의 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-340">You can see of list of all the plans that have been used to fail over VMs.</span></span> <span data-ttu-id="db95b-341">복구를 위해 동일한 계획을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-341">You can use the same plans to recover.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image37.png)
2. <span data-ttu-id="db95b-342">보호 계획 및 그 안에서 복구하려는 모든 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-342">Select the protection plan and all of the VMs you want to recover in it.</span></span> <span data-ttu-id="db95b-343">각 VM을 선택하면 대상 ESX 서버와 원본 VM 디스크를 포함한 자세한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-343">When you select each VM you can see more details including the target ESX server and the source VM disk.</span></span> <span data-ttu-id="db95b-344">**다음** 을 클릭하여 복구 마법사를 시작하고 복구하려는 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-344">Click **Next** to begin the Recover Wizard and select the VMs you want to recover.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image38.png)
3. <span data-ttu-id="db95b-345">여러 옵션에 따라 복구할 수는 있지만 **최신 태그**를 사용하고 **모든 VM에 적용**을 선택하여 가상 컴퓨터에서 최신 데이터를 사용하는지 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-345">You can recover based on multiple options but we recommend you use **Latest Tag** and select **Apply for All VMs** to ensure that the latest data from the virtual machine will be used.</span></span>
4. <span data-ttu-id="db95b-346">**준비 검사**를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-346">Run the **Readiness Check.**</span></span> <span data-ttu-id="db95b-347">이 올바른 매개 변수가 VM 복구를 활성화하도록 구성되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-347">This will check if the right parameters are configured to enable VM recovery.</span></span> <span data-ttu-id="db95b-348">**다음**을 클릭하여 모든 검사가 성공적으로 수행되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-348">Click **Next** if all the checks are successful.</span></span> <span data-ttu-id="db95b-349">그렇지 않은 경우 로그를 확인하고 오류를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-349">If not check the log and resolve the errors.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image39.png)
5. <span data-ttu-id="db95b-350">**VM 구성** 에서 복구 설정이 올바르게 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-350">In **VM Configuration** ensure that the recovery settings are correctly set.</span></span> <span data-ttu-id="db95b-351">필요한 경우 VM 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-351">You can change the VM settings if you need to.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image40.png)
6. <span data-ttu-id="db95b-352">복구될 가상 컴퓨터의 목록을 검토하고 복구 순서를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-352">Review the list of virtual machines that will be recovered and specify a recovery order.</span></span> <span data-ttu-id="db95b-353">컴퓨터 호스트 이름을 사용하여 VM이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-353">Note that VMs are listed using the computer host name.</span></span> <span data-ttu-id="db95b-354">컴퓨터 호스트 이름을 가상 컴퓨터에 매핑하기 어려울 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-354">It might be difficult to map the computer host name to the virtual machine.</span></span>
   <span data-ttu-id="db95b-355">이름을 매핑하려면 Azure의 가상 컴퓨터 **대시보드** 로 이동하고 VM 호스트 이름을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-355">To map the names, go to the virtual machines **Dashboard** in Azure and check the VM host name.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image41.png)
7. <span data-ttu-id="db95b-356">계획 이름을 지정하고 **나중에 복구**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-356">Specify a plan name and select **Recover later**.</span></span> <span data-ttu-id="db95b-357">초기 보호가 불완전할 수 있으므로 나중에 복구하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-357">We recommend to recover later since the initial protection might not be complete.</span></span>
8. <span data-ttu-id="db95b-358">**복구** 를 클릭하여 계획을 저장하거나 나중이 아닌 지금 복구하도록 선택한 경우 복구를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-358">Click on **Recover** to save the plan or trigger the recovery if you've selected to recover now and not later.</span></span> <span data-ttu-id="db95b-359">계획이 저장되었는지 복구 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-359">You can check the recovery status to see if the plan's been saved.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image42.png)

   ![](./media/site-recovery-failback-azure-to-vmware/image43.png)

## <a name="recover-virtual-machines"></a><span data-ttu-id="db95b-360">가상 컴퓨터 복구</span><span class="sxs-lookup"><span data-stu-id="db95b-360">Recover virtual machines</span></span>
<span data-ttu-id="db95b-361">계획을 만든 후에 가상 컴퓨터를 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-361">After the plan's been created, you can recover the virtual machines.</span></span> <span data-ttu-id="db95b-362">실행하기 전에 가상 컴퓨터가 동기화를 완료했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-362">Before you do check that the virtual machines have completed synchronization.</span></span> <span data-ttu-id="db95b-363">복제 상태에서 OK를 표시하는 경우 보호가 완료되었으며 RPO 임계값을 충족하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-363">If replication status shows OK then the protection is completed and the RPO threshold has been met.</span></span> <span data-ttu-id="db95b-364">VM 속성에서 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-364">You can verify health in the VM properties.</span></span>

![](./media/site-recovery-failback-azure-to-vmware/image44.png)

<span data-ttu-id="db95b-365">복구를 시작하기 전에 Azure 가상 컴퓨터를 끕니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-365">Turn off the Azure virtual machines before you initiate the recovery.</span></span> <span data-ttu-id="db95b-366">이렇게 하면 스플릿 브레인이 없으며 사용자가 응용 프로그램의 사본 하나에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-366">This ensures there's no split brain and that users will only access one copy of the application.</span></span>

1. <span data-ttu-id="db95b-367">저장된 계획을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-367">Start the saved plan.</span></span> <span data-ttu-id="db95b-368">vContinuum에서 계획 **모니터링** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-368">In vContinuum select **Monitor** the plans.</span></span> <span data-ttu-id="db95b-369">실행된 모든 계획을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-369">This lists all the plans that have been run.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image45.png)
2. <span data-ttu-id="db95b-370">**복구**에서 계획을 선택하고 **시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-370">Select the plan in **Recovery** and click **Start**.</span></span> <span data-ttu-id="db95b-371">복구를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-371">You can monitor recovery.</span></span> <span data-ttu-id="db95b-372">VM이 켜진 후 vcenter에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-372">After VMs have been turned on you can connect to them in vCenter.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image46.png)

## <a name="protect-to-azure-again-after-failback"></a><span data-ttu-id="db95b-373">장애 복구 후 Azure로 다시 보호</span><span class="sxs-lookup"><span data-stu-id="db95b-373">Protect to Azure again after failback</span></span>
<span data-ttu-id="db95b-374">장애 복구가 완료된 후 가상 컴퓨터를 다시 보호하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-374">After failback has been completed you'll probably want to protect the virtual machines again.</span></span> <span data-ttu-id="db95b-375">다음과 같이 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-375">Do this as follows:</span></span>

1. <span data-ttu-id="db95b-376">가상 컴퓨터 온-프레미스가 작동되는지, 응용프로그램이 도달할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-376">Check that the virtual machines on-premises are working and that applications are reachable.</span></span>
2. <span data-ttu-id="db95b-377">Azure Site Recovery 포털에서 가상 컴퓨터를 선택하고 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-377">In the Azure Site Recovery portal, select the virtual machines and delete them.</span></span> <span data-ttu-id="db95b-378">가상 컴퓨터의 보호를 사용하지 않도록 설정하려면 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-378">Select to disable the protection of the virtual machines.</span></span> <span data-ttu-id="db95b-379">이렇게 하면 VM이 더 이상 보호되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-379">This ensures that the VMs are no more protected.</span></span>
3. <span data-ttu-id="db95b-380">Azure에서 장애 조치된 Azure 가상 컴퓨터 삭제</span><span class="sxs-lookup"><span data-stu-id="db95b-380">In Azure delete the failed over Azure virtual machines</span></span>
4. <span data-ttu-id="db95b-381">VSpehere에서 오래된 가상 컴퓨터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-381">Delete the old virtual machine on vSpehere.</span></span> <span data-ttu-id="db95b-382">이들은 이전에 Azure로 장애 조치된 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-382">These are the VMs that you previously failed over to Azure.</span></span>
5. <span data-ttu-id="db95b-383">사이트 복구 포털에서 최근에 장애 조치된 VM을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-383">In the Site Recovery portal protect the VMs that recently failed over.</span></span> <span data-ttu-id="db95b-384">보호된 후 복구 계획에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db95b-384">After they're protected  you can add them to a recovery plan.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db95b-385">다음 단계</span><span class="sxs-lookup"><span data-stu-id="db95b-385">Next steps</span></span>
* <span data-ttu-id="db95b-386">[알아봅니다](site-recovery-vmware-to-azure-classic.md) .</span><span class="sxs-lookup"><span data-stu-id="db95b-386">[Read about](site-recovery-vmware-to-azure-classic.md) replicating VMware virtual machines and physical servers to Azure using the enhanced deployment.</span></span>
