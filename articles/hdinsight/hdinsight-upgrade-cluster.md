---
title: "HDInsight 클러스터를 최신 버전으로 업그레이드 -Azure | Microsoft Docs"
description: "HDInsight 클러스터를 최신 버전으로 업그레이드하는 방법을 알아봅니다."
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
ms.openlocfilehash: fa2e37bd922690322ccc3d8f68128180d013b701
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-hdinsight-cluster-to-a-newer-version"></a><span data-ttu-id="9f0dc-103">HDInsight 클러스터를 최신 버전으로 업그레이드</span><span class="sxs-lookup"><span data-stu-id="9f0dc-103">Upgrade HDInsight cluster to a newer version</span></span>
<span data-ttu-id="9f0dc-104">최신 HDInsight 기능을 활용하려면 HDInsight 클러스터를 최신 버전으로 업그레이드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9f0dc-104">To take advantage of the latest HDInsight features, we recommend that HDInsight clusters be upgraded to latest version.</span></span> <span data-ttu-id="9f0dc-105">아래 지침에 따라 HDInsight 클러스터 버전을 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="9f0dc-105">Follow the below guidelines to upgrade your HDInsight cluster versions.</span></span>

> [!NOTE]
> <span data-ttu-id="9f0dc-106">HDInsight 클러스터 버전 3.2 및 3.3은 곧 사용이 중단될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="9f0dc-106">HDInsight clusters version 3.2 and 3.3 are nearing retirement date.</span></span> <span data-ttu-id="9f0dc-107">지원되는 HDInsight 버전에 대한 자세한 내용은 [HDInsight 구성 요소 버전](hdinsight-component-versioning.md#supported-hdinsight-versions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f0dc-107">For information on supported version of HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>
>
>

## <a name="upgrade-tasks"></a><span data-ttu-id="9f0dc-108">업그레이드 작업</span><span class="sxs-lookup"><span data-stu-id="9f0dc-108">Upgrade tasks</span></span>
<span data-ttu-id="9f0dc-109">HDInsight 클러스터를 업그레이드하는 워크플로는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9f0dc-109">The workflow to upgrade HDInsight Cluster is as follows.</span></span>

![업그레이드 워크플로 다이어그램](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. <span data-ttu-id="9f0dc-111">HDInsight 클러스터를 업그레이드할 때 필요할 수 있는 변경 내용을 이해하려면 이 문서의 각 섹션을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="9f0dc-111">Read each section of this document to understand changes that may be required when upgrading your HDInsight cluster.</span></span>
2. <span data-ttu-id="9f0dc-112">클러스터를 테스트/품질 보증 환경으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f0dc-112">Create a cluster as a test/quality assurance environment.</span></span> <span data-ttu-id="9f0dc-113">클러스터를 만드는 방법에 대한 자세한 내용은 [Linux 기반 HDInsight 클러스터를 만드는 방법 알아보기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f0dc-113">For more information on creating a cluster, see [Learn how to create Linux-based HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
3. <span data-ttu-id="9f0dc-114">기존 작업, 데이터 원본 및 싱크를 새 환경으로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9f0dc-114">Copy existing jobs, data sources, and sinks to the new environment.</span></span> <span data-ttu-id="9f0dc-115">자세한 내용은 [테스트 환경에 데이터 복사](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f0dc-115">See [Copy Data To Test Environment](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) for more details.</span></span>
4. <span data-ttu-id="9f0dc-116">작업이 새 클러스터에서 예상대로 작동하는지 확인하려면 유효성 검사 테스트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9f0dc-116">Perform validation testing to make sure that your jobs work as expected on the new cluster.</span></span>


<span data-ttu-id="9f0dc-117">예상대로 작동하는 것이 확인되면 마이그레이션을 위해 가동 중지 시간을 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="9f0dc-117">Once you have verified that everything works as expected, schedule downtime for the migration.</span></span> <span data-ttu-id="9f0dc-118">이 가동 중지 시간 동안 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9f0dc-118">During this downtime, do the following actions:</span></span>

1.  <span data-ttu-id="9f0dc-119">클러스터 노드에 로컬로 저장된 모든 임시 데이터를 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="9f0dc-119">Back up any transient data stored locally on the cluster nodes.</span></span> <span data-ttu-id="9f0dc-120">예를 들어 헤드 노드에 직접 저장된 데이터가 있는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="9f0dc-120">For example, if you have data stored directly on a head node.</span></span>
2.  <span data-ttu-id="9f0dc-121">기존 클러스터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="9f0dc-121">Delete the existing cluster.</span></span>
3.  <span data-ttu-id="9f0dc-122">이전 클러스터에서 사용된 것과 동일한 기본 데이터 저장소를 사용하여 최신(또는 지원되는) HDI 버전과 동일한 VNET 서브넷에서 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f0dc-122">Create a cluster in the same VNET subnet with latest (or supported) HDI version using the same default data store that the previous cluster used.</span></span> <span data-ttu-id="9f0dc-123">이렇게 하면 새 클러스터에서 기존의 프로덕션 데이터에 대해 작업을 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f0dc-123">This allows the new cluster to continue working against your existing production data.</span></span>
4.  <span data-ttu-id="9f0dc-124">백업한 모든 임시 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9f0dc-124">Import any transient data you backed up.</span></span>
5.  <span data-ttu-id="9f0dc-125">새 클러스터를 사용하여 작업을 시작하거나 계속 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="9f0dc-125">Start jobs/continue processing using the new cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f0dc-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9f0dc-126">Next Steps</span></span>
* [<span data-ttu-id="9f0dc-127">Linux 기반 HDInsight 클러스터를 만드는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="9f0dc-127">Learn how to create Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="9f0dc-128">SSH를 사용하여 HDInsight에 연결</span><span class="sxs-lookup"><span data-stu-id="9f0dc-128">Connect to HDInsight using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)
* [<span data-ttu-id="9f0dc-129">Ambari를 사용하여 Linux 기반 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="9f0dc-129">Manage a Linux-based cluster using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

