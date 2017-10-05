---
title: "서버 제거 및 보호 사용 안 함 | Microsoft Docs"
description: "이 문서에서는 사이트 복구 자격 증명 모음에서 서버 등록을 취소하고 가상 컴퓨터 및 물리적 서버의 보호를 사용하지 않도록 설정하는 방법을 설명합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: ef1f31d5-285b-4a0f-89b5-0123cd422d80
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: raynew
ms.openlocfilehash: 43f92a35dc9b04584badd1c9f1152470246b5012
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="remove-servers-and-disable-protection"></a><span data-ttu-id="ce80f-103">서버 제거 및 보호 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="ce80f-103">Remove servers and disable protection</span></span>

<span data-ttu-id="ce80f-104">Azure Site Recovery 서비스는 BCDR(비즈니스 연속성 및 재해 복구 개선) 전략에 기여하는 서비스로</span><span class="sxs-lookup"><span data-stu-id="ce80f-104">The Azure Site Recovery service contributes to your business continuity and disaster recovery (BCDR) strategy.</span></span> <span data-ttu-id="ce80f-105">가상 컴퓨터 및 물리적 서버의 복제, 장애 조치(failover) 및 복구(failback)를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-105">The service orchestrates replication, failover and recovery of virtual machines and physical servers.</span></span> <span data-ttu-id="ce80f-106">컴퓨터는 Azure 또는 보조 온-프레미스 데이터 센터로 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-106">Machines can be replicated to Azure, or to a secondary on-premises data center.</span></span> <span data-ttu-id="ce80f-107">빠른 개요를 알아보려면 [Azure Site Recovery란?](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="ce80f-107">For a quick overview read [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>

<span data-ttu-id="ce80f-108">이 문서에는 Azure Portal의 Recovery Services 자격 증명 모음에서 서버의 등록을 취소하는 방법 및 Site Recovery를 통해 보호되는 컴퓨터에 대한 보호를 사용하지 않도록 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-108">This article describes how to unregister servers from a Recovery Services vault in the Azure portal, and how to disable protection for machines protected by Site Recovery.</span></span>

<span data-ttu-id="ce80f-109">이 문서의 하단 또는 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 의견이나 질문을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-109">Post any comments or questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="unregister-a-connected-configuration-server"></a><span data-ttu-id="ce80f-110">연결된 구성 서버 등록 취소</span><span class="sxs-lookup"><span data-stu-id="ce80f-110">Unregister a connected configuration server</span></span>

<span data-ttu-id="ce80f-111">VMware VM 또는 Windows/Linux 물리적 서버를 Azure에 복제하는 경우 다음과 같이 자격 증명 모음에서 연결된 구성 서버를 등록 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-111">If you replicate VMware VMs or Windows/Linux physical servers to Azure, you can unregister a connected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="ce80f-112">컴퓨터 보호 사용 안 함.</span><span class="sxs-lookup"><span data-stu-id="ce80f-112">Disable machine protection.</span></span> <span data-ttu-id="ce80f-113">**보호된 항목** > **복제된 항목**을 클릭하고 컴퓨터를 마우스 오른쪽 단추로 클릭한 후 > **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-113">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span>
2. <span data-ttu-id="ce80f-114">모든 정책 연결 해제.</span><span class="sxs-lookup"><span data-stu-id="ce80f-114">Disassociate any policies.</span></span> <span data-ttu-id="ce80f-115">**사이트 복구 인프라** > **VMWare 및 물리적 컴퓨터** > **복제 정책**에서 연결된 정책을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-115">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Replication Policies**, double-click the associated policy.</span></span> <span data-ttu-id="ce80f-116">구성 서버를 마우스 오른쪽 단추로 클릭하고 > **연결 해제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-116">Right-click the configuration server > **Disassociate**.</span></span>
3. <span data-ttu-id="ce80f-117">추가 온-프레미스 프로세스 또는 마스터 대상 서버를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-117">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="ce80f-118">**사이트 복구 인프라** > **VMWare 및 물리적 컴퓨터** > **구성 서버**에서 서버를 마우스 오른쪽 단추로 클릭하고 > **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-118">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click the server > **Delete**.</span></span>
4. <span data-ttu-id="ce80f-119">구성 서버를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-119">Delete the configuration server.</span></span>
5. <span data-ttu-id="ce80f-120">마스터 대상 서버에서 실행되는 이동성 서비스를 수동으로 제거합니다(별도의 서버이거나 구성 서버에서 실행 중).</span><span class="sxs-lookup"><span data-stu-id="ce80f-120">Manually uninstall the Mobility service running on the master target server (this will be either a separate server, or running on the configuration server).</span></span>
6. <span data-ttu-id="ce80f-121">추가 프로세스 서버를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-121">Uninstall any additional process servers.</span></span>
7. <span data-ttu-id="ce80f-122">구성 서버를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-122">Uninstall the configuration server.</span></span>
8. <span data-ttu-id="ce80f-123">구성 서버에서 Site Recovery에 의해 설치된 MySQL 인스턴스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-123">On the configuration server, uninstall the instance of MySQL that was installed by Site Recovery.</span></span>
9. <span data-ttu-id="ce80f-124">구성 서버의 레지스트리에서 ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery`` 키를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-124">In the registry of the configuration server delete the key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-unconnected-configuration-server"></a><span data-ttu-id="ce80f-125">연결되지 않은 구성 서버 등록 취소</span><span class="sxs-lookup"><span data-stu-id="ce80f-125">Unregister a unconnected configuration server</span></span>

<span data-ttu-id="ce80f-126">VMware VM 또는 Windows/Linux 물리적 서버를 Azure에 복제하는 경우 다음과 같이 자격 증명 모음에서 연결되지 않은 구성 서버를 등록 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-126">If you replicate VMware VMs or Windows/Linux physical servers to Azure, you can unregister an unconnected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="ce80f-127">컴퓨터 보호 사용 안 함.</span><span class="sxs-lookup"><span data-stu-id="ce80f-127">Disable machine protection.</span></span> <span data-ttu-id="ce80f-128">**보호된 항목** > **복제된 항목**을 클릭하고 컴퓨터를 마우스 오른쪽 단추로 클릭한 후 > **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-128">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span> <span data-ttu-id="ce80f-129">**컴퓨터 관리 중지**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-129">Select **Stop managing the machine**.</span></span>
2. <span data-ttu-id="ce80f-130">추가 온-프레미스 프로세스 또는 마스터 대상 서버를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-130">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="ce80f-131">**사이트 복구 인프라** > **VMWare 및 물리적 컴퓨터** > **구성 서버**에서 서버를 마우스 오른쪽 단추로 클릭하고 > **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-131">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click the server > **Delete**.</span></span>
3. <span data-ttu-id="ce80f-132">구성 서버를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-132">Delete the configuration server.</span></span>
4. <span data-ttu-id="ce80f-133">마스터 대상 서버에서 실행되는 이동성 서비스를 수동으로 제거합니다(별도의 서버이거나 구성 서버에서 실행 중).</span><span class="sxs-lookup"><span data-stu-id="ce80f-133">Manually uninstall the Mobility service running on the master target server (this will be either a separate server, or running on the configuration server).</span></span>
5. <span data-ttu-id="ce80f-134">추가 프로세스 서버를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-134">Uninstall any additional process servers.</span></span>
6. <span data-ttu-id="ce80f-135">구성 서버를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-135">Uninstall the configuration server.</span></span>
7. <span data-ttu-id="ce80f-136">구성 서버에서 Site Recovery에 의해 설치된 MySQL 인스턴스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-136">On the configuration server, uninstall the instance of MySQL that was installed by Site Recovery.</span></span>
8. <span data-ttu-id="ce80f-137">구성 서버의 레지스트리에서 ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery`` 키를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-137">In the registry of the configuration server delete the key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-connected-vmm-server"></a><span data-ttu-id="ce80f-138">연결된 VMM 서버 등록 취소</span><span class="sxs-lookup"><span data-stu-id="ce80f-138">Unregister a connected VMM server</span></span>

<span data-ttu-id="ce80f-139">Azure에 연결된 경우 VMM 서버의 등록을 취소하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-139">As a best practice, we recommend that you unregister the VMM server when it's connected to Azure.</span></span> <span data-ttu-id="ce80f-140">이렇게 하면 VMM 서버(및 페어링된 클라우드가 있는 다른 VMM 서버)의 설정이 알맞게 정리됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-140">This ensures that settings on the VMM servers (and on other VMM servers with paired clouds) are cleaned up properly.</span></span> <span data-ttu-id="ce80f-141">연결에 영구적인 문제가 있는 경우에만 연결되지 않은 서버를 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-141">You should only remove an unconnected server if there's a permanent issue with connectivity.</span></span> <span data-ttu-id="ce80f-142">VMM 서버가 연결되지 않은 경우 스크립트를 직접 실행하여 설정을 정리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-142">If the VMM server isn’t connected, you will need to manually run a script to clean up settings.</span></span>

1. <span data-ttu-id="ce80f-143">제거할 VMM에서 클라우드에 VM 복제를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-143">Stop replicating VMs in clouds on the VMM server you want to remove.</span></span>
2. <span data-ttu-id="ce80f-144">삭제할 VMM 서버에서 클라우드에 사용된 모든 네트워크 매핑을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-144">Delete any network mappings used by clouds on the VMM server you want to delete.</span></span> <span data-ttu-id="ce80f-145">**사이트 복구 인프라** > **System Center VMM** > **네트워크 매핑**에서 네트워크 매핑을 마우스 오른쪽 단추로 클릭하고 > **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-145">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click the network mapping > **Delete**.</span></span>
3. <span data-ttu-id="ce80f-146">제거할 VMM 서버의 클라우드에서 복제 정책을 연결 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-146">Disassociate replication policies from clouds on the VMM server you want to remove.</span></span>  <span data-ttu-id="ce80f-147">**사이트 복구 인프라** > **System Center VMM** >  **복제 정책**에서 연결된 정책을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-147">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click the associated policy.</span></span> <span data-ttu-id="ce80f-148">클라우드를 마우스 오른쪽 단추로 클릭하고 > **연결 해제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-148">Right-click the cloud > **Disassociate**.</span></span>
4. <span data-ttu-id="ce80f-149">VMM 서버 또는 활성 VMM 노드를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-149">Delete the VMM server or active VMM node.</span></span> <span data-ttu-id="ce80f-150">**사이트 복구 인프라** > **System Center VMM** > **VMM 서버**에서 서버를 마우스 오른쪽 단추로 클릭하고 > **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-150">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click the server > **Delete**.</span></span>
5. <span data-ttu-id="ce80f-151">VMM 서버에서 공급자를 수동으로 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-151">Uninstall the Provider manually on the VMM server.</span></span> <span data-ttu-id="ce80f-152">클러스터가 있는 경우 모든 노드에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-152">If you have a cluster, remove from all nodes.</span></span>
6. <span data-ttu-id="ce80f-153">Azure에 복제하는 경우 삭제된 클라우드의 Hyper-V 호스트에서 Microsoft Recovery Services 에이전트를 수동으로 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-153">If you're replicating to Azure, manually remove the Microsoft Recovery Services agent from Hyper-V hosts in the deleted clouds.</span></span>



### <a name="unregister-an-unconnected-vmm-server"></a><span data-ttu-id="ce80f-154">연결되지 않은 VMM 서버 등록 취소</span><span class="sxs-lookup"><span data-stu-id="ce80f-154">Unregister an unconnected VMM server</span></span>

1. <span data-ttu-id="ce80f-155">제거할 VMM에서 클라우드에 VM 복제를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-155">Stop replicating VMs in clouds on the VMM server you want to remove.</span></span>
2. <span data-ttu-id="ce80f-156">삭제할 VMM 서버에서 클라우드에 사용된 모든 네트워크 매핑을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-156">Delete any network mappings used by clouds on the VMM server that you want to delete.</span></span> <span data-ttu-id="ce80f-157">**사이트 복구 인프라** > **System Center VMM** > **네트워크 매핑**에서 네트워크 매핑을 마우스 오른쪽 단추로 클릭하고 > **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-157">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click the network mapping > **Delete**.</span></span>
3. <span data-ttu-id="ce80f-158">VMM 서버의 ID를 메모해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-158">Note the ID of the VMM server.</span></span>
4. <span data-ttu-id="ce80f-159">제거할 VMM 서버의 클라우드에서 복제 정책을 연결 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-159">Disassociate replication policies from clouds on the VMM server you want to remove.</span></span>  <span data-ttu-id="ce80f-160">**사이트 복구 인프라** > **System Center VMM** >  **복제 정책**에서 연결된 정책을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-160">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click the associated policy.</span></span> <span data-ttu-id="ce80f-161">클라우드를 마우스 오른쪽 단추로 클릭하고 > **연결 해제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-161">Right-click the cloud > **Disassociate**.</span></span>
5. <span data-ttu-id="ce80f-162">VMM 서버 또는 활성 노드를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-162">Delete the VMM server or active node.</span></span> <span data-ttu-id="ce80f-163">**사이트 복구 인프라** > **System Center VMM** > **VMM 서버**에서 서버를 마우스 오른쪽 단추로 클릭하고 > **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-163">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click the server > **Delete**.</span></span>
6. <span data-ttu-id="ce80f-164">VMM 서버에서 [정리 스크립트](http://aka.ms/asr-cleanup-script-vmm)를 다운로드하여 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-164">Download and run the [cleanup script](http://aka.ms/asr-cleanup-script-vmm) on the VMM server.</span></span> <span data-ttu-id="ce80f-165">기본(LocalMachine) 범위에 대한 실행 정책을 변경하려면 **관리자 권한으로 실행** 옵션으로 PowerShell을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-165">Open PowerShell with the **Run as Administrator** option, to change the execution policy for the default (LocalMachine) scope.</span></span> <span data-ttu-id="ce80f-166">스크립트에서 제거할 VMM 서버의 ID를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-166">In the script, specify the ID of the VMM server you want to remove.</span></span> <span data-ttu-id="ce80f-167">이 스크립트는 서버에서 등록 및 클라우드 페어링을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-167">The script removes registration and cloud pairing information from the server.</span></span>
5. <span data-ttu-id="ce80f-168">제거할 VMM 서버에서 클라우드와 페어링되는 클라우드가 포함된 다른 모든 VMM 서버에서 정리 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-168">Run the cleanup script on any other VMM servers that contain clouds that are paired with clouds on the VMM server you want to remove.</span></span>
6. <span data-ttu-id="ce80f-169">공급자가 설치된 다른 모든 수동 VMM 클러스터 노드에서 정리 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-169">Run the  cleanup script on any other passive VMM cluster nodes that have the Provider installed.</span></span>
7. <span data-ttu-id="ce80f-170">VMM 서버에서 공급자를 수동으로 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-170">Uninstall the Provider manually on the VMM server.</span></span> <span data-ttu-id="ce80f-171">클러스터가 있는 경우 모든 노드에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-171">If you have a cluster, remove from all nodes.</span></span>
8. <span data-ttu-id="ce80f-172">Azure에 복제하는 경우 삭제된 클라우드의 Hyper-V 호스트에서 Microsoft Recovery Services 에이전트를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-172">If you replicating to Azure, you can remove the Microsoft Recovery Services agent from Hyper-V hosts in the deleted clouds.</span></span>

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a><span data-ttu-id="ce80f-173">Hyper-V 사이트에서 Hyper-V 호스트 등록 취소</span><span class="sxs-lookup"><span data-stu-id="ce80f-173">Unregister a Hyper-V host in a Hyper-V Site</span></span>

<span data-ttu-id="ce80f-174">VMM에 의해 관리되지 않는 Hyper-V 호스트가 Hyper-V 사이트로 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-174">Hyper-V hosts that aren't managed by VMM are gathered into a Hyper-V site.</span></span> <span data-ttu-id="ce80f-175">다음과 같이 Hyper-V 사이트에서 호스트를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-175">Remove a host in a Hyper-V site as follows:</span></span>

1. <span data-ttu-id="ce80f-176">호스트에 있는 Hyper-V VM에 대한 복제를 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-176">Disable replication for Hyper-V VMs located on the host.</span></span>
2. <span data-ttu-id="ce80f-177">Hyper-V 사이트에 대한 정책을 연결 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-177">Disassociate policies for the Hyper-V site.</span></span> <span data-ttu-id="ce80f-178">**사이트 복구 인프라** > **Hyper-V 사이트** >  **복제 정책**에서 연결된 정책을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-178">In **Site Recovery Infrastructure** > **For Hyper-V Sites** >  **Replication Policies**, double-click the associated policy.</span></span> <span data-ttu-id="ce80f-179">사이트를 마우스 오른쪽 단추로 클릭하고 > **연결 해제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-179">Right-click the site > **Disassociate**.</span></span>
3. <span data-ttu-id="ce80f-180">Hyper-V 호스트를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-180">Delete Hyper-V hosts.</span></span> <span data-ttu-id="ce80f-181">**사이트 복구 인프라** > **System Center VMM** > **Hyper-V 호스트**에서 서버를 마우스 오른쪽 단추로 클릭하고 > **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-181">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Hosts**, right-click the server > **Delete**.</span></span>
4. <span data-ttu-id="ce80f-182">모든 호스트가 제거되었으면 Hyper-V 사이트를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-182">Delete the Hyper-V site after all hosts have been removed from it.</span></span> <span data-ttu-id="ce80f-183">**사이트 복구 인프라** > **System Center VMM** > **Hyper-V 사이트**에서 사이트를 마우스 오른쪽 단추로 클릭하고 > **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-183">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Sites**, right-click the site > **Delete**.</span></span>
5. <span data-ttu-id="ce80f-184">제거한 각 Hyper-V 호스트에서 다음 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-184">Run the following script on each Hyper-V host that you removed.</span></span> <span data-ttu-id="ce80f-185">스크립트는 서버에서 설정을 정리하고 자격 증명 모음에서 설정을 등록 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-185">The script cleans up settings on the server, and unregisters it from the vault.</span></span>


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run the script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove the old Azure Site Recovery Provider related properties. Do you want to continue (Y/N) ?"
            $choice =  Read-Host

            if (!($choice -eq 'Y' -or $choice -eq 'y'))
            {
            "Stopping cleanup."
            return;
            }

            $serviceName = "dra"
            $service = Get-Service -Name $serviceName
            if ($service.Status -eq "Running")
            {
                "Stopping the Azure Site Recovery service..."
                net stop $serviceName
            }

            $asrHivePath = "HKLM:\SOFTWARE\Microsoft\Azure Site Recovery"
            $registrationPath = $asrHivePath + '\Registration'
            $proxySettingsPath = $asrHivePath + '\ProxySettings'
            $draIdvalue = 'DraID'

            if (Test-Path $asrHivePath)
            {
                if (Test-Path $registrationPath)
                {
                    "Removing registration related registry keys."    
                    Remove-Item -Recurse -Path $registrationPath
                }

                if (Test-Path $proxySettingsPath)
            {
                    "Removing proxy settings"
                    Remove-Item -Recurse -Path $proxySettingsPath
                }

                $regNode = Get-ItemProperty -Path $asrHivePath
                if($regNode.DraID -ne $null)
                {            
                    "Removing DraId"
                    Remove-ItemProperty -Path $asrHivePath -Name $draIdValue
                }
                "Registry keys removed."
            }

            # First retrive all the certificates to be deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete the certs
            "Removing all related certificates"
            foreach ($cert in $ASRcerts)
            {
                $store.Remove($cert)
            }
        }catch
        {    
            [system.exception]
            Write-Host "Error occured" -ForegroundColor "Red"
            $error[0]
            Write-Host "FAILED" -ForegroundColor "Red"
        }
        popd``



## <a name="disable-protection-for-a-vmware-vm-or-physical-server"></a><span data-ttu-id="ce80f-186">VMware VM 또는 물리적 서버에 대한 보호를 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="ce80f-186">Disable protection for a VMware VM or physical server</span></span>

1. <span data-ttu-id="ce80f-187">**보호된 항목** > **복제된 항목**을 클릭하고 컴퓨터를 마우스 오른쪽 단추로 클릭한 후 > **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-187">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span>
2. <span data-ttu-id="ce80f-188">**컴퓨터 제거**에서 다음 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-188">In **Remove Machine**, select one of these options:</span></span>
    - <span data-ttu-id="ce80f-189">**컴퓨터에 대한 보호 사용 안 함(권장)**.</span><span class="sxs-lookup"><span data-stu-id="ce80f-189">**Disable protection for the machine (recommended)**.</span></span> <span data-ttu-id="ce80f-190">컴퓨터 복제를 중지하려면 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-190">Use this option to stop replicating the machine.</span></span> <span data-ttu-id="ce80f-191">Site Recovery 설정은 자동으로 정리됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-191">Site Recovery settings will be cleaned up automatically.</span></span> <span data-ttu-id="ce80f-192">다음 상황에서만 이 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-192">You will only see this option in the following circumstances:</span></span>
        - <span data-ttu-id="ce80f-193">**VM 볼륨을 크기 조정했음** - 볼륨 크기를 조정하면 가상 컴퓨터 상태가 심각해집니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-193">**You've resized the VM volume**—When you resize a volume the virtual machine goes into a critical state.</span></span> <span data-ttu-id="ce80f-194">이 옵션을 선택하면 Azure의 복구 지점을 유지하는 동시에 보호가 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-194">Select this option to disables protection while retaining recovery points in Azure.</span></span> <span data-ttu-id="ce80f-195">컴퓨터에 보호를 사용하도록 다시 설정할 경우 크기 조정된 볼륨의 데이터가 Azure로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-195">When you enable protection for the machine again, the data for the resized volume will be transferred to Azure.</span></span>
        - <span data-ttu-id="ce80f-196">**최근에 장애 조치를 실행했음** - 장애 조치를 실행하여 환경을 테스트한 후 이 옵션을 선택하여 온-프레미스 컴퓨터에서 보호를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-196">**You've recently run a failover**—After you've run a failover to test your environment, select this option to start protecting on-premises machines again.</span></span> <span data-ttu-id="ce80f-197">그러면 각각의 가상 컴퓨터가 비활성화되며, 다시 보호를 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-197">It disables each virtual machine, and then you need to enable protection for them again.</span></span> <span data-ttu-id="ce80f-198">이 설정으로 컴퓨터를 비활성화할 경우 Azure의 복제 가상 컴퓨터에 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-198">Disabling the machine with this setting doesn't affect the replica virtual machine in Azure.</span></span> <span data-ttu-id="ce80f-199">컴퓨터에서 모바일 서비스를 제거하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="ce80f-199">Don't uninstall the Mobility service from the machine.</span></span>
    - <span data-ttu-id="ce80f-200">**컴퓨터 관리 중지**.</span><span class="sxs-lookup"><span data-stu-id="ce80f-200">**Stop managing the machine**.</span></span> <span data-ttu-id="ce80f-201">이 옵션을 선택하면 컴퓨터가 자격 증명 모음에서만 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-201">If you select this option, the machine will only be removed from the vault.</span></span> <span data-ttu-id="ce80f-202">컴퓨터에 대한 온-프레미스 보호 설정은 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-202">On-premises protection settings for the machine won’t be affected.</span></span> <span data-ttu-id="ce80f-203">컴퓨터의 설정을 제거하고 Azure 구독에서 컴퓨터를 제거하려면 이동성 서비스를 제거하여 설정을 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-203">To remove settings on the machine, and to remove the machine from the Azure subscription, you need to clean the settings by uninstalling the Mobility service.</span></span>

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a><span data-ttu-id="ce80f-204">VMM 클라우드에서 Hyper-V VM에 대한 보호 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="ce80f-204">Disable protection for a Hyper-V VM in a VMM cloud</span></span>

1. <span data-ttu-id="ce80f-205">**보호된 항목** > **복제된 항목**을 클릭하고 컴퓨터를 마우스 오른쪽 단추로 클릭한 후 > **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-205">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span>
2. <span data-ttu-id="ce80f-206">**컴퓨터 제거**에서 다음 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-206">In **Remove Machine**, select one of these options:</span></span>

    - <span data-ttu-id="ce80f-207">**컴퓨터에 대한 보호 사용 안 함(권장)**.</span><span class="sxs-lookup"><span data-stu-id="ce80f-207">**Disable protection for the machine (recommended)**.</span></span> <span data-ttu-id="ce80f-208">컴퓨터 복제를 중지하려면 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-208">Use this option to stop replicating the machine.</span></span> <span data-ttu-id="ce80f-209">Site Recovery 설정은 자동으로 정리됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-209">Site Recovery settings will be cleaned up automatically.</span></span>
    - <span data-ttu-id="ce80f-210">**컴퓨터 관리 중지**.</span><span class="sxs-lookup"><span data-stu-id="ce80f-210">**Stop managing the machine**.</span></span> <span data-ttu-id="ce80f-211">이 옵션을 선택하면 컴퓨터가 자격 증명 모음에서만 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-211">If you select this option, the machine will only be removed from the vault.</span></span> <span data-ttu-id="ce80f-212">컴퓨터에 대한 온-프레미스 보호 설정은 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-212">On-premises protection settings for the machine won’t be affected.</span></span> <span data-ttu-id="ce80f-213">컴퓨터의 설정을 제거하고 Azure 구독에서 컴퓨터를 제거하려면 아래 명령을 사용하여 설정을 수동으로 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-213">To remove settings on the machine, and to remove the machine from the Azure subscription, you need to clean the settings up manually, using the instructions below.</span></span> <span data-ttu-id="ce80f-214">가상 컴퓨터와 해당 하드 디스크를 삭제하도록 선택하면 대상 위치에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-214">Note that if you select to delete the virtual machine and its hard disks, they'll be removed from the target location.</span></span>

### <a name="clean-up-protection-settings---replication-to-a-secondary-vmm-site"></a><span data-ttu-id="ce80f-215">보호 설정 정리 - 보조 VMM 사이트로 복제</span><span class="sxs-lookup"><span data-stu-id="ce80f-215">Clean up protection settings - replication to a secondary VMM site</span></span>

<span data-ttu-id="ce80f-216">**컴퓨터 관리 중지**를 선택했고 보조 사이트로 복제하는 경우 주 서버에서 이 스크립트를 실행하여 주 가상 컴퓨터에 대한 설정을 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-216">If you selected **Stop managing the machine** and you replicating to a secondary site, run this script on the primary server to clean up the settings for the primary virtual machine.</span></span> <span data-ttu-id="ce80f-217">VMM 콘솔에서 VMM PowerShell 콘솔을 열려면 PowerShell 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-217">In the VMM console click the PowerShell button to open the VMM PowerShell console.</span></span> <span data-ttu-id="ce80f-218">SQLVM1을 가상 컴퓨터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-218">Replace SQLVM1 with the name of your virtual machine.</span></span>

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="ce80f-219">보조 VMM 서버에서 이 스크립트를 실행하여 보조 가상 컴퓨터의 설정을 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-219">On the secondary VMM server run this script to clean up the settings for the secondary virtual machine:</span></span>

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. <span data-ttu-id="ce80f-220">두 번째 VMM 서버에서 Hyper-V 호스트 서버에서 가상 컴퓨터를 새로 고쳐 보조 VM이 VMM 콘솔에서 다시 감지되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-220">On the secondary VMM server, refresh the virtual machines on the Hyper-V host server, so that the secondary VM gets detected again in the VMM console.</span></span>
4. <span data-ttu-id="ce80f-221">위의 단계는 VMM 서버에서 복제 설정을 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-221">The above steps clear up the replication settings on the VMM server.</span></span> <span data-ttu-id="ce80f-222">가상 컴퓨터에 대한 복제를 중지하려면 주 및 보조 VM에서 다음 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-222">If you want to stop replication for the virtual machine, run the following script oh the primary and secondary VMs.</span></span> <span data-ttu-id="ce80f-223">SQLVM1을 가상 컴퓨터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-223">Replace SQLVM1 with the name of your virtual machine.</span></span>

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-to-azure"></a><span data-ttu-id="ce80f-224">보호 설정 정리 - Azure로 복제</span><span class="sxs-lookup"><span data-stu-id="ce80f-224">Clean up protection settings - replication to Azure</span></span>

1. <span data-ttu-id="ce80f-225">**컴퓨터 관리 중지**를 선택했고 Azure로 복제하는 경우 VMM 콘솔에서 PowerShell을 사용하여 원본 VMM 서버에서 이 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-225">If you selected **Stop managing the machine** and you replicate to Azure, run this script on the source VMM server, using PowerShell from the VMM console.</span></span>
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="ce80f-226">위의 단계는 VMM 서버에서 복제 설정을 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-226">The above steps clear the replication settings on the VMM server.</span></span> <span data-ttu-id="ce80f-227">Hyper-V 호스트 서버에서 실행하는 가상 컴퓨터의 복제를 중지하려면 이 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-227">To stop replication for the virtual machine running on the Hyper-V host server, run this script.</span></span> <span data-ttu-id="ce80f-228">SQLVM1을 가상 컴퓨터의 이름으로 바꾸고 host01.contoso.com을 Hyper-V 호스트 서버의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-228">Replace SQLVM1 with the name of your virtual machine, and host01.contoso.com with the name of the Hyper-V host server.</span></span>

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a><span data-ttu-id="ce80f-229">Hyper-V 사이트에서 Hyper-V VM에 대한 보호 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="ce80f-229">Disable protection for a Hyper-V VM in a Hyper-V Site</span></span>

<span data-ttu-id="ce80f-230">VMM 서버 없이 Hyper-V VM을 Azure에 복제하는 경우 이 절차를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-230">Use this procedure if you're replicating Hyper-V VMs to Azure without a VMM server.</span></span>

1. <span data-ttu-id="ce80f-231">**보호된 항목** > **복제된 항목**을 클릭하고 컴퓨터를 마우스 오른쪽 단추로 클릭한 후 > **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-231">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span>
2. <span data-ttu-id="ce80f-232">**컴퓨터 제거**에서 다음 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-232">In **Remove Machine**, you can select the following options:</span></span>

   - <span data-ttu-id="ce80f-233">**컴퓨터에 대한 보호 사용 안 함(권장)**.</span><span class="sxs-lookup"><span data-stu-id="ce80f-233">**Disable protection for the machine (recommended)**.</span></span> <span data-ttu-id="ce80f-234">컴퓨터 복제를 중지하려면 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-234">Use this option to stop replicating the machine.</span></span> <span data-ttu-id="ce80f-235">Site Recovery 설정은 자동으로 정리됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-235">Site Recovery settings will be cleaned up automatically.</span></span>
   - <span data-ttu-id="ce80f-236">**컴퓨터 관리 중지**.</span><span class="sxs-lookup"><span data-stu-id="ce80f-236">**Stop managing the machine**.</span></span> <span data-ttu-id="ce80f-237">이 옵션을 선택하면 컴퓨터가 자격 증명 모음에서만 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-237">If you select this option the machine will only be removed from the vault.</span></span> <span data-ttu-id="ce80f-238">컴퓨터에 대한 온-프레미스 보호 설정은 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-238">On-premises protection settings for the machine won’t be affected.</span></span> <span data-ttu-id="ce80f-239">컴퓨터의 설정을 제거하고 Azure 구독에서 가상 컴퓨터를 제거하려면 설정을 수동으로 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-239">To remove settings on the machine, and to remove the virtual machine from the Azure subscription, you need to clean the settings up manually.</span></span> <span data-ttu-id="ce80f-240">가상 컴퓨터와 해당 하드 디스크를 삭제하도록 선택하면 대상 위치에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-240">If you select to delete the virtual machine and its hard disks they will be removed from the target location.</span></span>
3. <span data-ttu-id="ce80f-241">**컴퓨터 관리 중지**를 선택한 경우, 원본 Hyper-V 호스트 서버에서 이 스크립트를 실행하여 가상 컴퓨터에 대한 복제를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-241">If you selected **Stop managing the machine**, run this script on the source Hyper-V host server, to remove replication for the virtual machine.</span></span> <span data-ttu-id="ce80f-242">SQLVM1을 가상 컴퓨터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ce80f-242">Replace SQLVM1 with the name of your virtual machine.</span></span>

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
