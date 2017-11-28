---
title: "aaaUpgrade HDInsight 클러스터 tooa 최신 버전이-Azure | Microsoft Docs"
description: "어떻게 tooUpgrade HDInsight 클러스터 tooa 최신 버전에 알아봅니다."
services: hdinsight
documentationcenter: 
author: bhanupr
manager: asadk
editor: bhanupr
ms.assetid: 60eb573c-e639-4815-9fc6-ea8b106d8dbc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/04/2017
ms.author: bhanupr
ms.openlocfilehash: 5fff3c9bc88dfbcbc1ccb0188accdfbbec3a62f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-hdinsight-cluster-tooa-newer-version"></a><span data-ttu-id="4b952-103">HDInsight 클러스터 tooa 새 버전 업그레이드</span><span class="sxs-lookup"><span data-stu-id="4b952-103">Upgrade HDInsight cluster tooa newer version</span></span>
<span data-ttu-id="4b952-104">tootake 활용 hello 최신 HDInsight 기능, HDInsight 클러스터 업그레이드 toolatest 버전 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4b952-104">tootake advantage of hello latest HDInsight features, we recommend that HDInsight clusters be upgraded toolatest version.</span></span> <span data-ttu-id="4b952-105">HDInsight 클러스터 버전이 아래 지침 tooupgrade hello를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="4b952-105">Follow hello below guidelines tooupgrade your HDInsight cluster versions.</span></span>

> [!NOTE]
> <span data-ttu-id="4b952-106">HDInsight 클러스터 버전 3.2 및 3.3은 곧 사용이 중단될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="4b952-106">HDInsight clusters version 3.2 and 3.3 are nearing retirement date.</span></span> <span data-ttu-id="4b952-107">지원되는 HDInsight 버전에 대한 자세한 내용은 [HDInsight 구성 요소 버전](hdinsight-component-versioning.md#supported-hdinsight-versions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4b952-107">For information on supported version of HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>
>
>

## <a name="upgrade-tasks"></a><span data-ttu-id="4b952-108">업그레이드 작업</span><span class="sxs-lookup"><span data-stu-id="4b952-108">Upgrade tasks</span></span>
<span data-ttu-id="4b952-109">hello 워크플로 tooupgrade HDInsight 클러스터는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4b952-109">hello workflow tooupgrade HDInsight Cluster is as follows.</span></span>

![업그레이드 워크플로 다이어그램](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. <span data-ttu-id="4b952-111">HDInsight 클러스터를 업그레이드 하는 경우 필요할 수 있는 toounderstand 변경 내용을이 문서의 각 섹션을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="4b952-111">Read each section of this document toounderstand changes that may be required when upgrading your HDInsight cluster.</span></span>
2. <span data-ttu-id="4b952-112">클러스터를 테스트/품질 보증 환경으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b952-112">Create a cluster as a test/quality assurance environment.</span></span> <span data-ttu-id="4b952-113">클러스터를 만드는 방법에 대 한 자세한 내용은 참조 하세요. [어떻게 toocreate Linux 기반 HDInsight 클러스터에 대해 알아봅니다](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="4b952-113">For more information on creating a cluster, see [Learn how toocreate Linux-based HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
3. <span data-ttu-id="4b952-114">기존 작업, 데이터 원본 및 싱크 toohello 새 환경 복사본입니다.</span><span class="sxs-lookup"><span data-stu-id="4b952-114">Copy existing jobs, data sources, and sinks toohello new environment.</span></span> <span data-ttu-id="4b952-115">참조 [데이터 복사 tooTest 환경](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b952-115">See [Copy Data tooTest Environment](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) for more details.</span></span>
4. <span data-ttu-id="4b952-116">Toomake 작업 hello 새 클러스터에서 예상 대로 작동 하는지 테스트 하는 유효성 검사를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b952-116">Perform validation testing toomake sure that your jobs work as expected on hello new cluster.</span></span>


<span data-ttu-id="4b952-117">예상 대로 작동 하는 것을 확인 한 후 hello 마이그레이션에 대 한 가동 중지 시간을 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b952-117">Once you have verified that everything works as expected, schedule downtime for hello migration.</span></span> <span data-ttu-id="4b952-118">이 작동 중단이 시간 동안 다음 작업 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4b952-118">During this downtime, do hello following actions:</span></span>

1.  <span data-ttu-id="4b952-119">Hello 클러스터 노드에서 로컬에 저장 된 임시 데이터를 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b952-119">Back up any transient data stored locally on hello cluster nodes.</span></span> <span data-ttu-id="4b952-120">예를 들어 헤드 노드에 직접 저장된 데이터가 있는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="4b952-120">For example, if you have data stored directly on a head node.</span></span>
2.  <span data-ttu-id="4b952-121">Hello 기존 클러스터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b952-121">Delete hello existing cluster.</span></span>
3.  <span data-ttu-id="4b952-122">클러스터 만들기 hello에 동일한 기본 데이터 저장소에 사용 되는 이전 클러스터 hello hello VNET 최신 (또는 지원 되는) 서브넷 HDI 버전 사용 하 여 동일한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b952-122">Create a cluster in hello same VNET subnet with latest (or supported) HDI version using hello same default data store that hello previous cluster used.</span></span> <span data-ttu-id="4b952-123">이렇게 하면 hello 새 클러스터 toocontinue 기존 프로덕션 데이터에 대해 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b952-123">This allows hello new cluster toocontinue working against your existing production data.</span></span>
4.  <span data-ttu-id="4b952-124">백업한 모든 임시 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4b952-124">Import any transient data you backed up.</span></span>
5.  <span data-ttu-id="4b952-125">시작 작업/계속 hello 새 클러스터를 사용 하 여 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b952-125">Start jobs/continue processing using hello new cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b952-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4b952-126">Next Steps</span></span>
* [<span data-ttu-id="4b952-127">어떻게 toocreate Linux 기반 HDInsight 클러스터에 대해 알아봅니다</span><span class="sxs-lookup"><span data-stu-id="4b952-127">Learn how toocreate Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="4b952-128">TooHDInsight SSH를 사용 하 여 연결</span><span class="sxs-lookup"><span data-stu-id="4b952-128">Connect tooHDInsight using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)
* [<span data-ttu-id="4b952-129">Ambari를 사용하여 Linux 기반 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="4b952-129">Manage a Linux-based cluster using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

