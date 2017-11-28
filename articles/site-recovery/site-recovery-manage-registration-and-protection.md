---
title: "aaaRemove 서버 및 보호 사용 안 함 | Microsoft Docs"
description: "이 문서에서는 어떻게 toounregister 서버에서 사이트 복구 자격 증명 모음 및 toodisable 보호 가상 컴퓨터 및 물리적 서버에 대 한 설명입니다."
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
ms.openlocfilehash: 95f20433f782c93685ad4bae93c6bc0e2d2f2356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="remove-servers-and-disable-protection"></a><span data-ttu-id="72c7b-103">서버 제거 및 보호 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="72c7b-103">Remove servers and disable protection</span></span>

<span data-ttu-id="72c7b-104">Azure Site Recovery 서비스 hello tooyour 비즈니스 연속성 및 재해 복구 (BCDR) 전략에 기여합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-104">hello Azure Site Recovery service contributes tooyour business continuity and disaster recovery (BCDR) strategy.</span></span> <span data-ttu-id="72c7b-105">hello 서비스에는 복제, 장애 조치 및 복구 가상 컴퓨터와 물리적 서버와 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-105">hello service orchestrates replication, failover and recovery of virtual machines and physical servers.</span></span> <span data-ttu-id="72c7b-106">복제 된 tooAzure 또는 tooa 보조 온-프레미스 데이터 센터 컴퓨터 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-106">Machines can be replicated tooAzure, or tooa secondary on-premises data center.</span></span> <span data-ttu-id="72c7b-107">빠른 개요를 알아보려면 [Azure Site Recovery란?](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="72c7b-107">For a quick overview read [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>

<span data-ttu-id="72c7b-108">이 문서에서는 복구 서비스에서 toounregister 서버 hello Azure 포털에서에서 자격 증명 모음에 어떻게 및 toodisable 보호 컴퓨터에 대 한 Site Recovery에서 보호 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-108">This article describes how toounregister servers from a Recovery Services vault in hello Azure portal, and how toodisable protection for machines protected by Site Recovery.</span></span>

<span data-ttu-id="72c7b-109">Hello 또는이 문서의 hello 맨 아래에 설명 이나 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-109">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="unregister-a-connected-configuration-server"></a><span data-ttu-id="72c7b-110">연결된 구성 서버 등록 취소</span><span class="sxs-lookup"><span data-stu-id="72c7b-110">Unregister a connected configuration server</span></span>

<span data-ttu-id="72c7b-111">VMware Vm 또는 실제 서버 tooAzure Windows/Linux를 복제 하는 경우 연결 된 구성 서버에서 자격 증명 모음을 다음과 같이 등록 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-111">If you replicate VMware VMs or Windows/Linux physical servers tooAzure, you can unregister a connected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="72c7b-112">컴퓨터 보호 사용 안 함.</span><span class="sxs-lookup"><span data-stu-id="72c7b-112">Disable machine protection.</span></span> <span data-ttu-id="72c7b-113">**보호 된 항목** > **복제 항목**를 마우스 오른쪽 단추로 클릭 hello 컴퓨터 > **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-113">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="72c7b-114">모든 정책 연결 해제.</span><span class="sxs-lookup"><span data-stu-id="72c7b-114">Disassociate any policies.</span></span> <span data-ttu-id="72c7b-115">**사이트 복구 인프라** > **물리적 컴퓨터 및 VMWare에 대 한** > **복제 정책**, hello를 두 번 클릭 연결 된 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-115">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="72c7b-116">Hello 구성 서버를 마우스 오른쪽 단추로 클릭 > **연관 해제**합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-116">Right-click hello configuration server > **Disassociate**.</span></span>
3. <span data-ttu-id="72c7b-117">추가 온-프레미스 프로세스 또는 마스터 대상 서버를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-117">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="72c7b-118">**사이트 복구 인프라** > **물리적 컴퓨터 및 VMWare에 대 한** > **구성 서버**를 마우스 오른쪽 단추로 클릭 hello 서버 > **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-118">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click hello server > **Delete**.</span></span>
4. <span data-ttu-id="72c7b-119">Hello 구성 서버를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-119">Delete hello configuration server.</span></span>
5. <span data-ttu-id="72c7b-120">Hello 마스터 대상 서버에서 실행 되는 hello 모바일 서비스를 수동으로 제거 (이 됩니다는 별도 서버 또는 hello 구성 서버에서 실행).</span><span class="sxs-lookup"><span data-stu-id="72c7b-120">Manually uninstall hello Mobility service running on hello master target server (this will be either a separate server, or running on hello configuration server).</span></span>
6. <span data-ttu-id="72c7b-121">추가 프로세스 서버를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-121">Uninstall any additional process servers.</span></span>
7. <span data-ttu-id="72c7b-122">Hello 구성 서버를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-122">Uninstall hello configuration server.</span></span>
8. <span data-ttu-id="72c7b-123">Hello 구성 서버에서 hello Site Recovery에 의해 설치 된 MySQL 인스턴스를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-123">On hello configuration server, uninstall hello instance of MySQL that was installed by Site Recovery.</span></span>
9. <span data-ttu-id="72c7b-124">Hello 구성 서버 hello 레지스트리에 hello 키 삭제 ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-124">In hello registry of hello configuration server delete hello key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-unconnected-configuration-server"></a><span data-ttu-id="72c7b-125">연결되지 않은 구성 서버 등록 취소</span><span class="sxs-lookup"><span data-stu-id="72c7b-125">Unregister a unconnected configuration server</span></span>

<span data-ttu-id="72c7b-126">VMware Vm 또는 실제 서버 tooAzure Windows/Linux를 복제 하는 경우는 연결 되지 않은 구성 서버에서 자격 증명 모음을 다음과 같이 등록 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-126">If you replicate VMware VMs or Windows/Linux physical servers tooAzure, you can unregister an unconnected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="72c7b-127">컴퓨터 보호 사용 안 함.</span><span class="sxs-lookup"><span data-stu-id="72c7b-127">Disable machine protection.</span></span> <span data-ttu-id="72c7b-128">**보호 된 항목** > **복제 항목**를 마우스 오른쪽 단추로 클릭 hello 컴퓨터 > **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-128">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span> <span data-ttu-id="72c7b-129">선택 **hello 컴퓨터 관리 중지**합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-129">Select **Stop managing hello machine**.</span></span>
2. <span data-ttu-id="72c7b-130">추가 온-프레미스 프로세스 또는 마스터 대상 서버를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-130">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="72c7b-131">**사이트 복구 인프라** > **물리적 컴퓨터 및 VMWare에 대 한** > **구성 서버**를 마우스 오른쪽 단추로 클릭 hello 서버 > **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-131">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click hello server > **Delete**.</span></span>
3. <span data-ttu-id="72c7b-132">Hello 구성 서버를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-132">Delete hello configuration server.</span></span>
4. <span data-ttu-id="72c7b-133">Hello 마스터 대상 서버에서 실행 되는 hello 모바일 서비스를 수동으로 제거 (이 됩니다는 별도 서버 또는 hello 구성 서버에서 실행).</span><span class="sxs-lookup"><span data-stu-id="72c7b-133">Manually uninstall hello Mobility service running on hello master target server (this will be either a separate server, or running on hello configuration server).</span></span>
5. <span data-ttu-id="72c7b-134">추가 프로세스 서버를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-134">Uninstall any additional process servers.</span></span>
6. <span data-ttu-id="72c7b-135">Hello 구성 서버를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-135">Uninstall hello configuration server.</span></span>
7. <span data-ttu-id="72c7b-136">Hello 구성 서버에서 hello Site Recovery에 의해 설치 된 MySQL 인스턴스를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-136">On hello configuration server, uninstall hello instance of MySQL that was installed by Site Recovery.</span></span>
8. <span data-ttu-id="72c7b-137">Hello 구성 서버 hello 레지스트리에 hello 키 삭제 ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-137">In hello registry of hello configuration server delete hello key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-connected-vmm-server"></a><span data-ttu-id="72c7b-138">연결된 VMM 서버 등록 취소</span><span class="sxs-lookup"><span data-stu-id="72c7b-138">Unregister a connected VMM server</span></span>

<span data-ttu-id="72c7b-139">모범 사례로, tooAzure에 연결한 경우 hello VMM 서버를 등록 취소 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-139">As a best practice, we recommend that you unregister hello VMM server when it's connected tooAzure.</span></span> <span data-ttu-id="72c7b-140">이렇게 하면 설정 hello VMM 서버에 (및 클라우드와 쌍을 이루는 다른 VMM 서버에서) 제대로 정리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-140">This ensures that settings on hello VMM servers (and on other VMM servers with paired clouds) are cleaned up properly.</span></span> <span data-ttu-id="72c7b-141">연결에 영구적인 문제가 있는 경우에만 연결되지 않은 서버를 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-141">You should only remove an unconnected server if there's a permanent issue with connectivity.</span></span> <span data-ttu-id="72c7b-142">Hello VMM 서버에 연결 되지 않아 경우 해야 toomanually 설정을 스크립트 tooclean를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-142">If hello VMM server isn’t connected, you will need toomanually run a script tooclean up settings.</span></span>

1. <span data-ttu-id="72c7b-143">Vm 클라우드에 hello tooremove VMM 서버에서 복제를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-143">Stop replicating VMs in clouds on hello VMM server you want tooremove.</span></span>
2. <span data-ttu-id="72c7b-144">Hello toodelete VMM 서버에 클라우드 사용 되는 모든 네트워크 매핑이 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-144">Delete any network mappings used by clouds on hello VMM server you want toodelete.</span></span> <span data-ttu-id="72c7b-145">**사이트 복구 인프라** > **System Center VMM** > **네트워크 매핑을**, hello 네트워크 매핑을 마우스 오른쪽 단추로 클릭 >  **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-145">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click hello network mapping > **Delete**.</span></span>
3. <span data-ttu-id="72c7b-146">Hello tooremove VMM 서버에 클라우드가 복제 정책 연결이 해제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-146">Disassociate replication policies from clouds on hello VMM server you want tooremove.</span></span>  <span data-ttu-id="72c7b-147">**사이트 복구 인프라** > **System Center VMM** >  **복제 정책**, 연결 된 hello 정책을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-147">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="72c7b-148">Hello 클라우드를 마우스 오른쪽 단추로 클릭 > **연관 해제**합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-148">Right-click hello cloud > **Disassociate**.</span></span>
4. <span data-ttu-id="72c7b-149">Hello VMM 서버 또는 현재 VMM 노드를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-149">Delete hello VMM server or active VMM node.</span></span> <span data-ttu-id="72c7b-150">**사이트 복구 인프라** > **System Center VMM** > **VMM 서버**를 마우스 오른쪽 단추로 클릭 hello 서버 >  **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-150">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click hello server > **Delete**.</span></span>
5. <span data-ttu-id="72c7b-151">Hello 공급자 hello VMM 서버에서 수동으로 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-151">Uninstall hello Provider manually on hello VMM server.</span></span> <span data-ttu-id="72c7b-152">클러스터가 있는 경우 모든 노드에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-152">If you have a cluster, remove from all nodes.</span></span>
6. <span data-ttu-id="72c7b-153">TooAzure를 복제 하는 경우 삭제 하는 hello 클라우드에서 Hyper-v 호스트에서 수동으로 hello Microsoft 복구 서비스 에이전트를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-153">If you're replicating tooAzure, manually remove hello Microsoft Recovery Services agent from Hyper-V hosts in hello deleted clouds.</span></span>



### <a name="unregister-an-unconnected-vmm-server"></a><span data-ttu-id="72c7b-154">연결되지 않은 VMM 서버 등록 취소</span><span class="sxs-lookup"><span data-stu-id="72c7b-154">Unregister an unconnected VMM server</span></span>

1. <span data-ttu-id="72c7b-155">Vm 클라우드에 hello tooremove VMM 서버에서 복제를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-155">Stop replicating VMs in clouds on hello VMM server you want tooremove.</span></span>
2. <span data-ttu-id="72c7b-156">원하는 toodelete hello VMM 서버의 클라우드에 사용 되는 모든 네트워크 매핑이 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-156">Delete any network mappings used by clouds on hello VMM server that you want toodelete.</span></span> <span data-ttu-id="72c7b-157">**사이트 복구 인프라** > **System Center VMM** > **네트워크 매핑을**, hello 네트워크 매핑을 마우스 오른쪽 단추로 클릭 >  **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-157">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click hello network mapping > **Delete**.</span></span>
3. <span data-ttu-id="72c7b-158">Note hello ID hello VMM 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-158">Note hello ID of hello VMM server.</span></span>
4. <span data-ttu-id="72c7b-159">Hello tooremove VMM 서버에 클라우드가 복제 정책 연결이 해제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-159">Disassociate replication policies from clouds on hello VMM server you want tooremove.</span></span>  <span data-ttu-id="72c7b-160">**사이트 복구 인프라** > **System Center VMM** >  **복제 정책**, 연결 된 hello 정책을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-160">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="72c7b-161">Hello 클라우드를 마우스 오른쪽 단추로 클릭 > **연관 해제**합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-161">Right-click hello cloud > **Disassociate**.</span></span>
5. <span data-ttu-id="72c7b-162">VMM 서버 hello 또는 액티브 노드를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-162">Delete hello VMM server or active node.</span></span> <span data-ttu-id="72c7b-163">**사이트 복구 인프라** > **System Center VMM** > **VMM 서버**를 마우스 오른쪽 단추로 클릭 hello 서버 >  **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-163">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click hello server > **Delete**.</span></span>
6. <span data-ttu-id="72c7b-164">다운로드 및 실행 hello [정리 스크립트](http://aka.ms/asr-cleanup-script-vmm) hello VMM 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-164">Download and run hello [cleanup script](http://aka.ms/asr-cleanup-script-vmm) on hello VMM server.</span></span> <span data-ttu-id="72c7b-165">Hello로 PowerShell을 열고 **관리자 권한으로 실행** toochange hello 실행 정책을 hello 기본 (LocalMachine) 범위에 대 한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-165">Open PowerShell with hello **Run as Administrator** option, toochange hello execution policy for hello default (LocalMachine) scope.</span></span> <span data-ttu-id="72c7b-166">Hello 스크립트에 hello hello tooremove VMM 서버 ID를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-166">In hello script, specify hello ID of hello VMM server you want tooremove.</span></span> <span data-ttu-id="72c7b-167">hello 스크립트 등록 및 클라우드 페어링 hello 서버에서 정보를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-167">hello script removes registration and cloud pairing information from hello server.</span></span>
5. <span data-ttu-id="72c7b-168">Hello tooremove VMM 서버에 클라우드가 함께 사용 되는 클라우드를 포함 하는 다른 VMM 서버 hello 정리 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-168">Run hello cleanup script on any other VMM servers that contain clouds that are paired with clouds on hello VMM server you want tooremove.</span></span>
6. <span data-ttu-id="72c7b-169">모든 다른 패시브 노드에서 VMM 클러스터 hello 공급자가 설치 되어 있는 hello 정리 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-169">Run hello  cleanup script on any other passive VMM cluster nodes that have hello Provider installed.</span></span>
7. <span data-ttu-id="72c7b-170">Hello 공급자 hello VMM 서버에서 수동으로 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-170">Uninstall hello Provider manually on hello VMM server.</span></span> <span data-ttu-id="72c7b-171">클러스터가 있는 경우 모든 노드에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-171">If you have a cluster, remove from all nodes.</span></span>
8. <span data-ttu-id="72c7b-172">TooAzure 복제 하면을 제거할 수 있으면 hello Microsoft 복구 서비스 에이전트 hello 삭제 클라우드에서 Hyper-v 호스트에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-172">If you replicating tooAzure, you can remove hello Microsoft Recovery Services agent from Hyper-V hosts in hello deleted clouds.</span></span>

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a><span data-ttu-id="72c7b-173">Hyper-V 사이트에서 Hyper-V 호스트 등록 취소</span><span class="sxs-lookup"><span data-stu-id="72c7b-173">Unregister a Hyper-V host in a Hyper-V Site</span></span>

<span data-ttu-id="72c7b-174">VMM에 의해 관리되지 않는 Hyper-V 호스트가 Hyper-V 사이트로 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-174">Hyper-V hosts that aren't managed by VMM are gathered into a Hyper-V site.</span></span> <span data-ttu-id="72c7b-175">다음과 같이 Hyper-V 사이트에서 호스트를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-175">Remove a host in a Hyper-V site as follows:</span></span>

1. <span data-ttu-id="72c7b-176">Hello 호스트에 있는 Hyper-v Vm에 대 한 복제를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-176">Disable replication for Hyper-V VMs located on hello host.</span></span>
2. <span data-ttu-id="72c7b-177">Hello 하이퍼-V 사이트에 대 한 정책 연결이 해제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-177">Disassociate policies for hello Hyper-V site.</span></span> <span data-ttu-id="72c7b-178">**사이트 복구 인프라** > **하이퍼-V 사이트에 대 한** >  **복제 정책**, 연결 된 hello 정책을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-178">In **Site Recovery Infrastructure** > **For Hyper-V Sites** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="72c7b-179">마우스 오른쪽 단추로 클릭 hello 사이트 > **연관 해제**합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-179">Right-click hello site > **Disassociate**.</span></span>
3. <span data-ttu-id="72c7b-180">Hyper-V 호스트를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-180">Delete Hyper-V hosts.</span></span> <span data-ttu-id="72c7b-181">**사이트 복구 인프라** > **System Center VMM** > **Hyper-v 호스트**를 마우스 오른쪽 단추로 클릭 hello 서버 >  **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-181">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Hosts**, right-click hello server > **Delete**.</span></span>
4. <span data-ttu-id="72c7b-182">모든 호스트에서 제거 된 후 hello 하이퍼-V 사이트를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-182">Delete hello Hyper-V site after all hosts have been removed from it.</span></span> <span data-ttu-id="72c7b-183">**사이트 복구 인프라** > **System Center VMM** > **Hyper-v 사이트**를 마우스 오른쪽 단추로 클릭 hello 사이트 >  **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-183">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Sites**, right-click hello site > **Delete**.</span></span>
5. <span data-ttu-id="72c7b-184">제거 된 각 Hyper-v 호스트에서 스크립트를 다음 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-184">Run hello following script on each Hyper-V host that you removed.</span></span> <span data-ttu-id="72c7b-185">hello 스크립트 hello 서버의 설정을 정리 하 고 hello 자격 증명 모음에서 등록을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-185">hello script cleans up settings on hello server, and unregisters it from hello vault.</span></span>


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run hello script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove hello old Azure Site Recovery Provider related properties. Do you want toocontinue (Y/N) ?"
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
                "Stopping hello Azure Site Recovery service..."
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

            # First retrive all hello certificates toobe deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete hello certs
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



## <a name="disable-protection-for-a-vmware-vm-or-physical-server"></a><span data-ttu-id="72c7b-186">VMware VM 또는 물리적 서버에 대한 보호를 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="72c7b-186">Disable protection for a VMware VM or physical server</span></span>

1. <span data-ttu-id="72c7b-187">**보호 된 항목** > **복제 항목**를 마우스 오른쪽 단추로 클릭 hello 컴퓨터 > **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-187">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="72c7b-188">**컴퓨터 제거**에서 다음 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-188">In **Remove Machine**, select one of these options:</span></span>
    - <span data-ttu-id="72c7b-189">**(권장) hello 컴퓨터에 대 한 보호 사용 안 함**합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-189">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="72c7b-190">이 옵션 toostop hello 컴퓨터에 복제를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-190">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="72c7b-191">Site Recovery 설정은 자동으로 정리됩니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-191">Site Recovery settings will be cleaned up automatically.</span></span> <span data-ttu-id="72c7b-192">이 옵션의 경우 다음 hello에만 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-192">You will only see this option in hello following circumstances:</span></span>
        - <span data-ttu-id="72c7b-193">**Hello VM 볼륨 크기를 조정할**-컴퓨터 위험 상태 전환 되는 볼륨 hello 가상 크기를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-193">**You've resized hello VM volume**—When you resize a volume hello virtual machine goes into a critical state.</span></span> <span data-ttu-id="72c7b-194">Azure에서 복구 지점을 유지 하는 동안이 옵션 toodisables 보호를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-194">Select this option toodisables protection while retaining recovery points in Azure.</span></span> <span data-ttu-id="72c7b-195">Hello 컴퓨터에 대 한 보호를 다시 사용 하도록 설정 하면 크기가 조정 hello 볼륨에 대 한 hello 데이터 전송된 tooAzure 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-195">When you enable protection for hello machine again, hello data for hello resized volume will be transferred tooAzure.</span></span>
        - <span data-ttu-id="72c7b-196">**장애 조치를 최근에 실행 한**-장애 조치 tootest 환경을 실행 한 후이 옵션 toostart 온-프레미스 컴퓨터를 다시 보호를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-196">**You've recently run a failover**—After you've run a failover tootest your environment, select this option toostart protecting on-premises machines again.</span></span> <span data-ttu-id="72c7b-197">각 가상 컴퓨터를 비활성화 한 다음 있습니다 tooenable 보호를 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-197">It disables each virtual machine, and then you need tooenable protection for them again.</span></span> <span data-ttu-id="72c7b-198">이 설정을 사용 하지 않도록 설정 hello 컴퓨터 Azure의 hello 복제 가상 컴퓨터에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-198">Disabling hello machine with this setting doesn't affect hello replica virtual machine in Azure.</span></span> <span data-ttu-id="72c7b-199">Hello 컴퓨터에서 hello 모바일 서비스를 제거 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="72c7b-199">Don't uninstall hello Mobility service from hello machine.</span></span>
    - <span data-ttu-id="72c7b-200">**Hello 컴퓨터 관리 중지**합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-200">**Stop managing hello machine**.</span></span> <span data-ttu-id="72c7b-201">이 옵션을 선택 하는 경우 hello 컴퓨터만 hello 자격 증명 모음에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-201">If you select this option, hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="72c7b-202">Hello 컴퓨터에 대 한 온-프레미스 보호 설정의 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-202">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="72c7b-203">hello 컴퓨터와 hello Azure 구독에서에서 tooremove hello 컴퓨터, tooremove 설정이 hello 모바일 서비스를 제거 하 여 tooclean hello 설정이 필요 하면 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-203">tooremove settings on hello machine, and tooremove hello machine from hello Azure subscription, you need tooclean hello settings by uninstalling hello Mobility service.</span></span>

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a><span data-ttu-id="72c7b-204">VMM 클라우드에서 Hyper-V VM에 대한 보호 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="72c7b-204">Disable protection for a Hyper-V VM in a VMM cloud</span></span>

1. <span data-ttu-id="72c7b-205">**보호 된 항목** > **복제 항목**를 마우스 오른쪽 단추로 클릭 hello 컴퓨터 > **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-205">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="72c7b-206">**컴퓨터 제거**에서 다음 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-206">In **Remove Machine**, select one of these options:</span></span>

    - <span data-ttu-id="72c7b-207">**(권장) hello 컴퓨터에 대 한 보호 사용 안 함**합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-207">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="72c7b-208">이 옵션 toostop hello 컴퓨터에 복제를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-208">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="72c7b-209">Site Recovery 설정은 자동으로 정리됩니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-209">Site Recovery settings will be cleaned up automatically.</span></span>
    - <span data-ttu-id="72c7b-210">**Hello 컴퓨터 관리 중지**합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-210">**Stop managing hello machine**.</span></span> <span data-ttu-id="72c7b-211">이 옵션을 선택 하는 경우 hello 컴퓨터만 hello 자격 증명 모음에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-211">If you select this option, hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="72c7b-212">Hello 컴퓨터에 대 한 온-프레미스 보호 설정의 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-212">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="72c7b-213">hello 컴퓨터와 hello Azure 구독에서에서 tooremove hello 컴퓨터, tooremove 설정이 필요한 tooclean hello 설정을 수동으로 아래 hello 지침을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-213">tooremove settings on hello machine, and tooremove hello machine from hello Azure subscription, you need tooclean hello settings up manually, using hello instructions below.</span></span> <span data-ttu-id="72c7b-214">참고 toodelete hello 가상 컴퓨터와 해당 하드 디스크를 선택한 경우 이러한 것에서 꺼내야 합니다 hello 대상 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-214">Note that if you select toodelete hello virtual machine and its hard disks, they'll be removed from hello target location.</span></span>

### <a name="clean-up-protection-settings---replication-tooa-secondary-vmm-site"></a><span data-ttu-id="72c7b-215">복제 tooa 보조 VMM 사이트-보호 설정 정리</span><span class="sxs-lookup"><span data-stu-id="72c7b-215">Clean up protection settings - replication tooa secondary VMM site</span></span>

<span data-ttu-id="72c7b-216">선택한 경우 **hello 컴퓨터 관리 중지** hello 주 가상 컴퓨터에 대 한 hello 설정을 hello 주 서버 tooclean에서이 스크립트 실행 tooa 보조 사이트를 복제 해야 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-216">If you selected **Stop managing hello machine** and you replicating tooa secondary site, run this script on hello primary server tooclean up hello settings for hello primary virtual machine.</span></span> <span data-ttu-id="72c7b-217">Hello VMM 콘솔에서 hello PowerShell 단추 tooopen hello VMM PowerShell 콘솔을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-217">In hello VMM console click hello PowerShell button tooopen hello VMM PowerShell console.</span></span> <span data-ttu-id="72c7b-218">SQLVM1 가상 컴퓨터의 hello 이름으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-218">Replace SQLVM1 with hello name of your virtual machine.</span></span>

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="72c7b-219">Hello 보조 VMM 서버에서이 스크립트 tooclean hello 보조 가상 컴퓨터에 대 한 hello 설정을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-219">On hello secondary VMM server run this script tooclean up hello settings for hello secondary virtual machine:</span></span>

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. <span data-ttu-id="72c7b-220">보조 VMM 서버 hello hello Hyper-v 호스트 서버의 가상 컴퓨터 hello hello 보조 VM 가져옵니다 검색 되도록 다시 hello VMM 콘솔에서 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-220">On hello secondary VMM server, refresh hello virtual machines on hello Hyper-V host server, so that hello secondary VM gets detected again in hello VMM console.</span></span>
4. <span data-ttu-id="72c7b-221">단계는 hello hello 복제 설정을 hello VMM 서버에서 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-221">hello above steps clear up hello replication settings on hello VMM server.</span></span> <span data-ttu-id="72c7b-222">Hello 가상 컴퓨터를 다음 hello 실행에 대 한 toostop 복제 하려는 경우 스크립트 안녕하세요 기본 및 보조 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-222">If you want toostop replication for hello virtual machine, run hello following script oh hello primary and secondary VMs.</span></span> <span data-ttu-id="72c7b-223">SQLVM1 가상 컴퓨터의 hello 이름으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-223">Replace SQLVM1 with hello name of your virtual machine.</span></span>

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-tooazure"></a><span data-ttu-id="72c7b-224">보호 설정-복제 tooAzure 정리</span><span class="sxs-lookup"><span data-stu-id="72c7b-224">Clean up protection settings - replication tooAzure</span></span>

1. <span data-ttu-id="72c7b-225">선택한 경우 **hello 컴퓨터 관리 중지** tooAzure 복제, hello VMM 콘솔에서 PowerShell을 사용 하 여 hello 원본 VMM 서버에서이 스크립트를 실행 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-225">If you selected **Stop managing hello machine** and you replicate tooAzure, run this script on hello source VMM server, using PowerShell from hello VMM console.</span></span>
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="72c7b-226">단계는 hello hello VMM 서버의 복제 설정을 hello 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-226">hello above steps clear hello replication settings on hello VMM server.</span></span> <span data-ttu-id="72c7b-227">이 스크립트를 실행 하는 hello Hyper-v 호스트 서버에서 실행 하는 hello 가상 컴퓨터에 대 한 toostop 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-227">toostop replication for hello virtual machine running on hello Hyper-V host server, run this script.</span></span> <span data-ttu-id="72c7b-228">SQLVM1 hello Hyper-v 호스트 서버 hello 이름 가진 가상 컴퓨터 및 host01.contoso.com hello 이름을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-228">Replace SQLVM1 with hello name of your virtual machine, and host01.contoso.com with hello name of hello Hyper-V host server.</span></span>

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a><span data-ttu-id="72c7b-229">Hyper-V 사이트에서 Hyper-V VM에 대한 보호 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="72c7b-229">Disable protection for a Hyper-V VM in a Hyper-V Site</span></span>

<span data-ttu-id="72c7b-230">VMM 서버 없이 tooAzure Hyper-v Vm을 복제 하는 경우이 절차를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-230">Use this procedure if you're replicating Hyper-V VMs tooAzure without a VMM server.</span></span>

1. <span data-ttu-id="72c7b-231">**보호 된 항목** > **복제 항목**를 마우스 오른쪽 단추로 클릭 hello 컴퓨터 > **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-231">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="72c7b-232">**컴퓨터 제거**, hello 다음 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-232">In **Remove Machine**, you can select hello following options:</span></span>

   - <span data-ttu-id="72c7b-233">**(권장) hello 컴퓨터에 대 한 보호 사용 안 함**합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-233">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="72c7b-234">이 옵션 toostop hello 컴퓨터에 복제를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-234">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="72c7b-235">Site Recovery 설정은 자동으로 정리됩니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-235">Site Recovery settings will be cleaned up automatically.</span></span>
   - <span data-ttu-id="72c7b-236">**Hello 컴퓨터 관리 중지**합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-236">**Stop managing hello machine**.</span></span> <span data-ttu-id="72c7b-237">이 옵션을 선택 하는 경우 hello 컴퓨터만 hello 자격 증명 모음에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-237">If you select this option hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="72c7b-238">Hello 컴퓨터에 대 한 온-프레미스 보호 설정의 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-238">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="72c7b-239">hello 컴퓨터와 hello Azure 구독에서에서 tooremove hello 가상 컴퓨터, tooremove 설정이 필요한 tooclean hello 설정을 수동으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-239">tooremove settings on hello machine, and tooremove hello virtual machine from hello Azure subscription, you need tooclean hello settings up manually.</span></span> <span data-ttu-id="72c7b-240">Toodelete hello 가상 컴퓨터와 해당 하드 디스크를 선택 하는 경우 hello 대상 위치에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-240">If you select toodelete hello virtual machine and its hard disks they will be removed from hello target location.</span></span>
3. <span data-ttu-id="72c7b-241">선택한 경우 **hello 컴퓨터 관리 중지**,이 hello 원본 Hyper-v 호스트 서버에서 스크립트, tooremove hello 가상 컴퓨터 복제를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-241">If you selected **Stop managing hello machine**, run this script on hello source Hyper-V host server, tooremove replication for hello virtual machine.</span></span> <span data-ttu-id="72c7b-242">SQLVM1 가상 컴퓨터의 hello 이름으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="72c7b-242">Replace SQLVM1 with hello name of your virtual machine.</span></span>

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
