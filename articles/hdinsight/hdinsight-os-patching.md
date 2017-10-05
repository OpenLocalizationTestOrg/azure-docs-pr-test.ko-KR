---
title: "Linux 기반 HDInsight 클러스터의 OS 패치 일정 구성 - Azure | Microsoft Docs"
description: "Linux 기반 HDInsight 클러스터의 OS 패치 일정을 구성하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: bprakash
manager: asadk
editor: bprakash
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: bhanupr
ms.openlocfilehash: af3c5a19ae8e2e606e4b0506f9f6dddb41192e40
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="os-patching-for-hdinsight"></a><span data-ttu-id="41ee3-103">HDInsight의 OS 패치</span><span class="sxs-lookup"><span data-stu-id="41ee3-103">OS patching for HDInsight</span></span> 
<span data-ttu-id="41ee3-104">관리되는 Hadoop 서비스인 HDInsight는 HDInsight 클러스터에서 사용하는 기본 VM의 OS를 패치하는 작업을 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="41ee3-104">As a managed Hadoop service, HDInsight takes care of patching the OS of the underlying VMs used by HDInsight clusters.</span></span> <span data-ttu-id="41ee3-105">2016년 8월 1일을 기준으로 Linux 기반 HDInsight 클러스터에 대한 게스트 OS 패치 정책을 변경했습니다(버전 3.4 이상).</span><span class="sxs-lookup"><span data-stu-id="41ee3-105">As of August 1, 2016, we have changed the guest OS patching policy for Linux-based HDInsight clusters (version 3.4 or greater).</span></span> <span data-ttu-id="41ee3-106">새 정책의 목표는 패치로 인해 부팅 횟수를 크게 줄이는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="41ee3-106">The goal of the new policy is to significantly reduce the number of reboots due to patching.</span></span> <span data-ttu-id="41ee3-107">새 정책은 월요일 또는 목요일 오전 12시(UTC)마다 시차를 두고 모든 지정된 클러스터의 노드에 있는 Linux 클러스터에서 계속 VM(가상 컴퓨터)을 패치합니다.</span><span class="sxs-lookup"><span data-stu-id="41ee3-107">The new policy will continue to patch virtual machines (VMs) on Linux clusters every Monday or Thursday starting at 12AM UTC in a staggered fashion across nodes in any given cluster.</span></span> <span data-ttu-id="41ee3-108">그러나 지정된 VM은 게스트 OS 패치로 인해 최대 30일마다 다시 부팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="41ee3-108">However, any given VM will only reboot at most once every 30 days due to guest OS patching.</span></span> <span data-ttu-id="41ee3-109">또한 새로 만든 클러스터는 생성된 날짜로부터 30일보다 이전에 첫 번째로 다시 부팅되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41ee3-109">In addition, the first reboot for a newly created cluster will not happen sooner than 30 days from the cluster creation date.</span></span> <span data-ttu-id="41ee3-110">VM이 다시 부팅되면 패치가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="41ee3-110">Patches will be effective once the VMs are rebooted.</span></span>

## <a name="how-to-configure-the-os-patching-schedule-for-linux-based-hdinsight-clusters"></a><span data-ttu-id="41ee3-111">Linux 기반 HDInsight 클러스터의 OS 패치 일정을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="41ee3-111">How to configure the OS patching schedule for Linux-based HDInsight clusters</span></span>
<span data-ttu-id="41ee3-112">중요한 보안 패치를 설치할 수 있도록 간혹 HDInsight 클러스터에서 가상 컴퓨터를 다시 부팅해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41ee3-112">The virtual machines in an HDInsight cluster need to be rebooted occasionally so that important security patches can be installed.</span></span> <span data-ttu-id="41ee3-113">새 Linux 기반 HDInsight 클러스터(버전 3.4 이상)는 2016년 8월 1일을 기준으로 다음 일정을 사용하여 다시 부팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="41ee3-113">As of August 1, 2016, new Linux-based HDInsight clusters (version 3.4 or greater,) are rebooted using the following schedule:</span></span>

1. <span data-ttu-id="41ee3-114">패치를 위해 30일 기간 내에서 최대 한 번 클러스터에 있는 가상 컴퓨터를 다시 부팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41ee3-114">A virtual machine in the cluster can only reboot for patches at most, once within a 30-day period.</span></span>
2. <span data-ttu-id="41ee3-115">다시 부팅은 오전 12시(UTC)에 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="41ee3-115">The reboot occurs starting at 12AM UTC.</span></span>
3. <span data-ttu-id="41ee3-116">다시 부팅 프로세스 중 클러스터를 계속 사용할 수 있도록 다시 부팅 프로세스는 가상 컴퓨터 클러스터에 걸쳐 지연됩니다.</span><span class="sxs-lookup"><span data-stu-id="41ee3-116">The reboot process is staggered across virtual machines in the cluster, so the cluster is still available during the reboot process.</span></span>
4. <span data-ttu-id="41ee3-117">새로 만든 클러스터의 첫 번째 다시 부팅은 클러스터 생성 날짜 이후 30일이 지나기 전에 일어나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41ee3-117">The first reboot for a newly created cluster will not happen sooner than 30 days after the cluster creation date.</span></span>

<span data-ttu-id="41ee3-118">이 문서에서 설명한 스크립트 작업을 사용하여 다음과 같이 OS 패치 일정을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41ee3-118">Using the script action described in this article, you can modify the OS patching schedule as follows:</span></span>
1. <span data-ttu-id="41ee3-119">자동 다시 부팅 사용 또는 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="41ee3-119">Enable or disable automatic reboots</span></span>
2. <span data-ttu-id="41ee3-120">다시 부팅 빈도 설정(다시 부팅 간의 날짜)</span><span class="sxs-lookup"><span data-stu-id="41ee3-120">Set the frequency of reboots (days between reboots)</span></span>
3. <span data-ttu-id="41ee3-121">다시 부팅을 수행할 요일 설정</span><span class="sxs-lookup"><span data-stu-id="41ee3-121">Set the day of the week when a reboot occurs</span></span>

> [!NOTE]
> <span data-ttu-id="41ee3-122">2016년 8월 1일 이후에 만들어진 Linux 기반 HDInsight 클러스터에서만 이 스크립트 작업이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="41ee3-122">This script action will only work with Linux-based HDInsight clusters created after August 1st, 2016.</span></span> <span data-ttu-id="41ee3-123">VM이 다시 부팅되는 경우에만 패치가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="41ee3-123">Patches will be effective only when VMs are rebooted.</span></span> 
>

## <a name="how-to-use-the-script"></a><span data-ttu-id="41ee3-124">스크립트를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="41ee3-124">How to use the script</span></span> 

<span data-ttu-id="41ee3-125">이 스크립트를 사용하는 경우 다음 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="41ee3-125">When using this script requires the following information:</span></span>
1. <span data-ttu-id="41ee3-126">스크립트 위치: https://hdiconfigactions.blob.core.windows.net/linuxospatchingrebootconfigv01/os-patching-reboot-config.sh</span><span class="sxs-lookup"><span data-stu-id="41ee3-126">The script location: https://hdiconfigactions.blob.core.windows.net/linuxospatchingrebootconfigv01/os-patching-reboot-config.sh.</span></span>
    <span data-ttu-id="41ee3-127">HDInsight는 이 URI를 사용하여 클러스터의 모든 가상 컴퓨터에서 스크립트를 찾아 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="41ee3-127">HDInsight uses this URI to find and run the script on all the virtual machines in the cluster.</span></span>
  
2. <span data-ttu-id="41ee3-128">스크립트를 적용하는 클러스터 노드 유형: 헤드 노드, workernode, zookeeper</span><span class="sxs-lookup"><span data-stu-id="41ee3-128">The cluster node types that the script is applied to: headnode, workernode, zookeeper.</span></span> <span data-ttu-id="41ee3-129">이 스크립트는 클러스터의 모든 노드 유형에 적용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41ee3-129">This script must be applied to all node types in the cluster.</span></span> <span data-ttu-id="41ee3-130">노드 유형에 적용되지 않으면 해당 노드 유형인 가상 컴퓨터는 계속 이전 패치 일정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41ee3-130">If it is not applied to a node type, then the virtual machines for that node type will continue to use the previous patching schedule.</span></span>


3.  <span data-ttu-id="41ee3-131">매개 변수: 이 스크립트는 세 가지 숫자 매개 변수를 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="41ee3-131">Parameter: This script accepts three numeric parameters:</span></span>

    | <span data-ttu-id="41ee3-132">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41ee3-132">Parameter</span></span> | <span data-ttu-id="41ee3-133">정의</span><span class="sxs-lookup"><span data-stu-id="41ee3-133">Definition</span></span> |
    | --- | --- |
    | <span data-ttu-id="41ee3-134">자동 다시 부팅 사용/사용 안 함</span><span class="sxs-lookup"><span data-stu-id="41ee3-134">Enable/disable automatic reboots</span></span> |<span data-ttu-id="41ee3-135">0 또는 1입니다.</span><span class="sxs-lookup"><span data-stu-id="41ee3-135">0 or 1.</span></span> <span data-ttu-id="41ee3-136">0 값은 자동 다시 부팅을 사용하지 않는 반면 1은 자동 다시 부팅을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="41ee3-136">A value of 0 disables automatic reboots while 1 enables automatic reboots.</span></span> |
    | <span data-ttu-id="41ee3-137">Frequency(빈도)</span><span class="sxs-lookup"><span data-stu-id="41ee3-137">Frequency</span></span> |<span data-ttu-id="41ee3-138">7~90입니다(포괄).</span><span class="sxs-lookup"><span data-stu-id="41ee3-138">7 to 90 (inclusive).</span></span> <span data-ttu-id="41ee3-139">다시 부팅해야 하는 패치를 위해 가상 컴퓨터를 다시 부팅하기 전에 대기한 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="41ee3-139">The number of days to wait before rebooting the virtual machines for patches that require a reboot.</span></span> |
    | <span data-ttu-id="41ee3-140">요일</span><span class="sxs-lookup"><span data-stu-id="41ee3-140">Day of week</span></span> |<span data-ttu-id="41ee3-141">1~7입니다(포괄).</span><span class="sxs-lookup"><span data-stu-id="41ee3-141">1 to 7 (inclusive).</span></span> <span data-ttu-id="41ee3-142">1 값은 월요일에 재부팅해야 함을 나타내고 7은 일요일을 나타냅니다. 예를 들어 매개 변수 1 60 2를 사용하면 최대 60일마다 화요일에 자동 다시 부팅이 발생하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41ee3-142">A value of 1 indicates the reboot should occur on a Monday, and 7 indicates a Sunday.For example, using parameters of 1 60 2 results in automatic reboots every 60 days (at most) on Tuesday.</span></span> |
    | <span data-ttu-id="41ee3-143">지속성</span><span class="sxs-lookup"><span data-stu-id="41ee3-143">Persistence</span></span> |<span data-ttu-id="41ee3-144">기존 클러스터에 스크립트 작업을 적용할 경우 스크립트를 지속형으로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41ee3-144">When applying a script action to an existing cluster, you can mark the script as persisted.</span></span> <span data-ttu-id="41ee3-145">지속형 스크립트는 크기 조정 작업을 통해 클러스터에 새 작업자 노드를 추가할 경우에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="41ee3-145">Persisted scripts are applied when new workernodes are added to the cluster through scaling operations.</span></span> |

> [!NOTE]
> <span data-ttu-id="41ee3-146">기존 클러스터에 적용하는 경우 이 스크립트를 지속형으로 표시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41ee3-146">You must mark this script as persisted when applying to an existing cluster.</span></span> <span data-ttu-id="41ee3-147">그렇지 않은 경우 크기 조정 작업을 통해 만들어진 모든 새 노드는 기본 패치 일정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41ee3-147">Otherwise, any new nodes created through scaling      operations will use the default patching schedule.</span></span>
<span data-ttu-id="41ee3-148">클러스터를 만드는 프로세스의 일부로 스크립트를 적용하는 경우 자동으로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="41ee3-148">If you apply the script as part of the cluster creation process, it is persisted automatically.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="41ee3-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="41ee3-149">Next steps</span></span>

<span data-ttu-id="41ee3-150">스크립트 작업을 사용하는 방법에 대한 특정 단계는 [스크립트 작업을 사용하여 Linux 기반 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)에서 다음 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41ee3-150">For specific steps on using the script action, see the following sections in the [Customize Linuz-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md):</span></span>

* [<span data-ttu-id="41ee3-151">클러스터를 만드는 동안 스크립트 작업 사용</span><span class="sxs-lookup"><span data-stu-id="41ee3-151">Use a script action during cluster creation</span></span>](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation)
* [<span data-ttu-id="41ee3-152">실행 중인 클러스터에 스크립트 작업 적용</span><span class="sxs-lookup"><span data-stu-id="41ee3-152">Apply a script action to a running cluster</span></span>](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster)
