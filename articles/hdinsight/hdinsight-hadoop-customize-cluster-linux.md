---
title: "스크립트 동작-Azure를 사용 하 여 aaaCustomize HDInsight 클러스터 | Microsoft Docs"
description: "사용자 지정 구성 요소 스크립트 동작을 사용 하 여 tooLinux 기반 HDInsight 클러스터를 추가 합니다. 스크립트 작업을 사용 하는 toocustomize hello 클러스터 구성 하거나 추가 서비스 및 색상, Solr, 또는 지역와 같은 유틸리티를 추가할 수 있는 Bash 스크립트"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48e85f53-87c1-474f-b767-ca772238cc13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: ff22680a8a50b21985f6941f1edaf1dcf863d13f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="86dca-104">스크립트 작업을 사용하여 Linux 기반 HDInsight 클러스터 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="86dca-104">Customize Linux-based HDInsight clusters using Script Action</span></span>

<span data-ttu-id="86dca-105">호출 하는 구성 옵션을 제공 하는 HDInsight **스크립트 동작** hello 클러스터를 사용자 지정 하는 사용자 지정 스크립트를 호출 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-105">HDInsight provides a configuration option called **Script Action** that invokes custom scripts that customize hello cluster.</span></span> <span data-ttu-id="86dca-106">이러한 스크립트는 사용 되는 tooinstall 추가 구성 요소 및 구성 설정을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-106">These scripts are used tooinstall additional components and change configuration settings.</span></span> <span data-ttu-id="86dca-107">스크립트 작업은 클러스터를 만드는 중이거나 만든 후에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-107">Script actions can be used during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="86dca-108">이미 실행 중인 클러스터에 hello 기능 toouse 스크립트 작업은 Linux 기반 HDInsight 클러스터에 사용할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-108">hello ability toouse script actions on an already running cluster is only available for Linux-based HDInsight clusters.</span></span>
>
> <span data-ttu-id="86dca-109">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="86dca-110">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86dca-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="86dca-111">스크립트 동작 HDInsight 응용 프로그램으로 게시 된 toohello Azure 마켓플레이스를 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-111">Script actions can also be published toohello Azure Marketplace as an HDInsight application.</span></span> <span data-ttu-id="86dca-112">이 문서에 hello 예 중 일부는 HDInsight 응용 프로그램에서 PowerShell 및.NET SDK hello 액션 명령 스크립트를 사용 하 여 설치 하는 방법을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-112">Some of hello examples in this document show how you can install an HDInsight application using script action commands from PowerShell and hello .NET SDK.</span></span> <span data-ttu-id="86dca-113">HDInsight 응용 프로그램에 대 한 자세한 내용은 참조 하십시오. [HDInsight 게시 응용 프로그램을 Azure Marketplace hello로](hdinsight-apps-publish-applications.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-113">For more information on HDInsight applications, see [Publish HDInsight applications into hello Azure Marketplace](hdinsight-apps-publish-applications.md).</span></span>

## <a name="permissions"></a><span data-ttu-id="86dca-114">권한</span><span class="sxs-lookup"><span data-stu-id="86dca-114">Permissions</span></span>

<span data-ttu-id="86dca-115">도메인에 가입 된 HDInsight 클러스터를 사용 하는 경우 두 Ambari는 권한은 hello 클러스터와 스크립트 동작을 사용 하는 경우 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-115">If you are using a domain-joined HDInsight cluster, there are two Ambari permissions that are required when using script actions with hello cluster:</span></span>

* <span data-ttu-id="86dca-116">**AMBARI 합니다. 실행\_사용자 지정\_명령**: hello Ambari 관리자 역할에는 기본적으로이 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-116">**AMBARI.RUN\_CUSTOM\_COMMAND**: hello Ambari Administrator role has this permission by default.</span></span>
* <span data-ttu-id="86dca-117">**클러스터입니다. 실행\_사용자 지정\_명령**: HDInsight 클러스터 관리자 모두 hello 및 Ambari 관리자는 기본적으로이 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-117">**CLUSTER.RUN\_CUSTOM\_COMMAND**: Both hello HDInsight Cluster Administrator and Ambari Administrator have this permission by default.</span></span>

<span data-ttu-id="86dca-118">도메인 가입 HDInsight에서 권한으로 작업하는 방법에 대한 자세한 내용은 [도메인 가입 HDInsight 클러스터 관리](hdinsight-domain-joined-manage.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86dca-118">For more information on working with permissions with domain-joined HDInsight, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>

## <a name="access-control"></a><span data-ttu-id="86dca-119">Access Control</span><span class="sxs-lookup"><span data-stu-id="86dca-119">Access control</span></span>

<span data-ttu-id="86dca-120">계정 적어도 있어야 Azure 구독의 관리자/소유자 hello 아니라면 **참가자** hello HDInsight 클러스터를 포함 하는 액세스 toohello 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-120">If you are not hello administrator/owner of your Azure subscription, your account must have at least **Contributor** access toohello resource group that contains hello HDInsight cluster.</span></span>

<span data-ttu-id="86dca-121">또한 이상 있는 사용자는 HDInsight 클러스터를 만드는 경우 **참가자** 액세스 toohello Azure 구독 이전에 등록 해야 HDInsight에 대 한 hello 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-121">Additionally, if you are creating an HDInsight cluster, someone with at least **Contributor** access toohello Azure subscription must have previously registered hello provider for HDInsight.</span></span> <span data-ttu-id="86dca-122">공급자 등록 사용자 만들면 참가자 액세스 toohello 구독과 hello에 대 한 리소스 처음으로 hello 구독에 대해 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-122">Provider registration happens when a user with Contributor access toohello subscription creates a resource for hello first time on hello subscription.</span></span> <span data-ttu-id="86dca-123">[REST를 사용하여 공급자를 등록](https://msdn.microsoft.com/library/azure/dn790548.aspx)하면 리소스를 만들지 않고도 수행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-123">It can also be accomplished without creating a resource by [registering a provider using REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span></span>

<span data-ttu-id="86dca-124">작업 액세스 관리에 대 한 자세한 내용은 다음 문서는 hello를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="86dca-124">For more information on working with access management, see hello following documents:</span></span>

* [<span data-ttu-id="86dca-125">Hello Azure 포털에에서 대 한 액세스 관리 시작</span><span class="sxs-lookup"><span data-stu-id="86dca-125">Get started with access management in hello Azure portal</span></span>](../active-directory/role-based-access-control-what-is.md)
* [<span data-ttu-id="86dca-126">역할 할당 toomanage tooyour Azure 구독의 리소스에 액세스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="86dca-126">Use role assignments toomanage access tooyour Azure subscription resources</span></span>](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a><span data-ttu-id="86dca-127">스크립트 작업 이해</span><span class="sxs-lookup"><span data-stu-id="86dca-127">Understanding Script Actions</span></span>

<span data-ttu-id="86dca-128">스크립트 동작은 단순히 URI 및 해당 매개 변수를 제공하는 Bash 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-128">A Script Action is simply a Bash script that you provide a URI to, and parameters for.</span></span> <span data-ttu-id="86dca-129">hello 스크립트 hello HDInsight 클러스터의 노드에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-129">hello script runs on nodes in hello HDInsight cluster.</span></span> <span data-ttu-id="86dca-130">hello 다음은 특성 및 스크립트 동작의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-130">hello following are characteristics and features of script actions.</span></span>

* <span data-ttu-id="86dca-131">Hello HDInsight 클러스터에서 액세스할 수 있는 URI에 저장 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-131">Must be stored on a URI that is accessible from hello HDInsight cluster.</span></span> <span data-ttu-id="86dca-132">hello 다음 저장소 위치 같습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-132">hello following are possible storage locations:</span></span>

    * <span data-ttu-id="86dca-133">**Azure 데이터 레이크 저장소** hello HDInsight 클러스터에서 액세스할 수 있는 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-133">An **Azure Data Lake Store** account that is accessible by hello HDInsight cluster.</span></span> <span data-ttu-id="86dca-134">HDInsight에서 Azure Data Lake Store를 사용하는 방법에 대한 자세한 내용은 [Azure Data Lake Store에서 HDInsight 클러스터 만들기](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86dca-134">For information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

        <span data-ttu-id="86dca-135">데이터 레이크 저장소에 저장 하는 스크립트를 사용할 경우 hello URI 형식은 `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-135">When using a script stored in Data Lake Store, hello URI format is `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span></span>

        > [!NOTE]
        > <span data-ttu-id="86dca-136">hello 서비스 보안 주체 HDInsight 사용 하 여 tooaccess Data Lake 저장소에 대 한 읽기 액세스 toohello 스크립트가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-136">hello service principal HDInsight uses tooaccess Data Lake Store must have read access toohello script.</span></span>

    * <span data-ttu-id="86dca-137">Blob에는 **Azure 저장소 계정** hello HDInsight 클러스터에 대 한 hello 기본 또는 추가 저장소 계정 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-137">A blob in an **Azure Storage account** that is either hello primary or additional storage account for hello HDInsight cluster.</span></span> <span data-ttu-id="86dca-138">HDInsight은 클러스터를 만드는 동안 저장소 계정에 이러한 유형의 tooboth 액세스 권한이 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-138">HDInsight is granted access tooboth of these types of storage accounts during cluster creation.</span></span>

    * <span data-ttu-id="86dca-139">Azure Blob, GitHub, OneDrive, Dropbox 등과 같은 공용 파일 공유 서비스</span><span class="sxs-lookup"><span data-stu-id="86dca-139">A public file sharing service such as Azure Blob, GitHub, OneDrive, Dropbox, etc.</span></span>

        <span data-ttu-id="86dca-140">예를 들어 Uri 참조 hello [예제 스크립트 작업 스크립트](#example-script-action-scripts) 섹션.</span><span class="sxs-lookup"><span data-stu-id="86dca-140">For example URIs, see hello [Example script action scripts](#example-script-action-scripts) section.</span></span>

        > [!WARNING]
        > <span data-ttu-id="86dca-141">HDInsight는 __범용__ Azure Storage 계정만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-141">HDInsight only supports __General-purpose__ Azure Storage accounts.</span></span> <span data-ttu-id="86dca-142">Hello 현재 지원 하지 않는 __Blob 저장소__ 계정 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-142">It does not currently support hello __Blob storage__ account type.</span></span>

* <span data-ttu-id="86dca-143">너무 제한 될 수 있습니다**특정 노드 유형에 대해**, 예에서는 헤드 노드 또는 작업자 노드에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-143">Can be restricted too**run on only certain node types**, for example head nodes or worker nodes.</span></span>

  > [!NOTE]
  > <span data-ttu-id="86dca-144">프리미엄 HDInsight를 사용할 때는 hello 가장자리 노드에서 hello 스크립트를 사용 해야 함을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-144">When used with HDInsight Premium, you can specify that hello script should be used on hello edge node.</span></span>

* <span data-ttu-id="86dca-145">**지속형** 또는 **임시** 스크립트일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-145">Can be **persisted** or **ad hoc**.</span></span>

    <span data-ttu-id="86dca-146">**지속** hello 스크립트를 실행 한 후 스크립트는 적용 된 tooworker 노드 추가 toohello 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-146">**Persisted** scripts are applied tooworker nodes added toohello cluster after hello script runs.</span></span> <span data-ttu-id="86dca-147">예를 들어 hello 클러스터를 확장 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="86dca-147">For example, when scaling up hello cluster.</span></span>

    <span data-ttu-id="86dca-148">지속형된 스크립트 변경 내용을 tooanother와 같은 노드 유형이 헤드 노드도 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-148">A persisted script might also apply changes tooanother node type, such as a head node.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="86dca-149">지속형 스크립트 작업은 고유한 이름이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-149">Persisted script actions must have a unique name.</span></span>

    <span data-ttu-id="86dca-150">**임시** 스크립트는 지속되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-150">**Ad hoc** scripts are not persisted.</span></span> <span data-ttu-id="86dca-151">가 hello 스크립트를 실행 한 후 노드 추가 toohello 클러스터 tooworker 적용된 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-151">They are not applied tooworker nodes added toohello cluster after hello script has ran.</span></span> <span data-ttu-id="86dca-152">승격할 수 있고 이후에 임시 스크립트 tooa 스크립트를 지 속하거나 지속형된 스크립트 tooan 임시 스크립트 수준을 내립니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-152">You can subsequently promote an ad hoc script tooa persisted script, or demote a persisted script tooan ad hoc script.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="86dca-153">클러스터를 만들 때 사용되는 스크립트 작업은 자동으로 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-153">Script actions used during cluster creation are automatically persisted.</span></span>
  >
  > <span data-ttu-id="86dca-154">사용자가 지속형 스크립트로 지정하더라도 실패하는 스크립트는 보존되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-154">Scripts that fail are not persisted, even if you specifically indicate that they should be.</span></span>

* <span data-ttu-id="86dca-155">수락할 수 있는 **매개 변수** 에서 사용 하는 hello 스크립트 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-155">Can accept **parameters** that are used by hello script during execution.</span></span>
* <span data-ttu-id="86dca-156">사용 하 여 실행 **루트 수준 권한을** hello 클러스터 노드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-156">Run with **root level privileges** on hello cluster nodes.</span></span>
* <span data-ttu-id="86dca-157">Hello를 통해 사용할 수 있습니다 **Azure 포털**, **Azure PowerShell**, **Azure CLI**, 또는 **HDInsight.NET SDK**</span><span class="sxs-lookup"><span data-stu-id="86dca-157">Can be used through hello **Azure portal**, **Azure PowerShell**, **Azure CLI**, or **HDInsight .NET SDK**</span></span>

<span data-ttu-id="86dca-158">hello 클러스터는 실행 된 모든 스크립트의 기록을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-158">hello cluster keeps a history of all scripts that have been ran.</span></span> <span data-ttu-id="86dca-159">hello 기록 올리기 또는 수준 내리기 작업에 대 한 스크립트의 toofind hello ID가 필요 하면 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-159">hello history is useful when you need toofind hello ID of a script for promotion or demotion operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="86dca-160">자동으로 방법 tooundo 없습니다는 hello 스크립트 작업으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-160">There is no automatic way tooundo hello changes made by a script action.</span></span> <span data-ttu-id="86dca-161">Hello 변경 내용이 되돌리는 것 수동으로 하거나 되돌린 해당 하는 스크립트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-161">Either manually reverse hello changes or provide a script that reverses them.</span></span>


### <a name="script-action-in-hello-cluster-creation-process"></a><span data-ttu-id="86dca-162">Hello 클러스터 만들기 프로세스에 스크립트 동작</span><span class="sxs-lookup"><span data-stu-id="86dca-162">Script Action in hello cluster creation process</span></span>

<span data-ttu-id="86dca-163">클러스터를 만들 때 사용되는 스크립트 작업은 기존 클러스터에서 실행되는 스크립트 작업과 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-163">Script Actions used during cluster creation are slightly different from script actions ran on an existing cluster:</span></span>

* <span data-ttu-id="86dca-164">hello 스크립트는 **자동으로 지속형**합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-164">hello script is **automatically persisted**.</span></span>
* <span data-ttu-id="86dca-165">A **오류** hello 스크립트에 hello 클러스터 만들기 프로세스 toofail 인해 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-165">A **failure** in hello script can cause hello cluster creation process toofail.</span></span>

<span data-ttu-id="86dca-166">hello 다음 다이어그램에서는 hello 만드는 프로세스 동안 스크립트 작업을 실행할 때 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-166">hello following diagram illustrates when Script Action is executed during hello creation process:</span></span>

<span data-ttu-id="86dca-167">![HDInsight 클러스터 사용자 지정 및 클러스터 만드는 동안의 단계][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="86dca-167">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="86dca-168">hello 스크립트 HDInsight를 구성 하는 동안 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-168">hello script runs while HDInsight is being configured.</span></span> <span data-ttu-id="86dca-169">이 단계에서 모두에서 동시에 hello 스크립트가 실행 hello 클러스터 hello 노드에서 루트 권한으로 실행 하 고 지정 된 노드에 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-169">At this stage, hello script runs in parallel on all hello specified nodes in hello cluster, and runs with root privileges on hello nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="86dca-170">Hello 스크립트 hello 클러스터 노드에서 루트 수준 권한으로 실행, 되므로 Hadoop 관련 서비스를 포함 한 서비스를 시작 및 중지와 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-170">Because hello script runs with root level privilege on hello cluster nodes, you can perform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="86dca-171">서비스를 중지 하면 hello Ambari 서비스 및 기타 Hadoop 관련 서비스 되는지 실행 되 고 hello 스크립트 실행이 완료 되기 전에 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-171">If you stop services, you must ensure that hello Ambari service and other Hadoop-related services are up and running before hello script finishes running.</span></span> <span data-ttu-id="86dca-172">이러한 서비스는 필요한 생성 되는 동안 toosuccessfully hello 상태 및 hello 클러스터의 상태 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-172">These services are required toosuccessfully determine hello health and state of hello cluster while it is being created.</span></span>


<span data-ttu-id="86dca-173">클러스터를 만드는 동안 한 번에 여러 스크립트 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-173">During cluster creation, you can use multiple script actions at once.</span></span> <span data-ttu-id="86dca-174">이러한 스크립트는 지정 된 hello 순서로 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-174">These scripts are invoked in hello order in which they were specified.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="86dca-175">스크립트 작업은 60분 이내에 완료하지 않으면 시간이 초과됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-175">Script actions must complete within 60 minutes, or timeout.</span></span> <span data-ttu-id="86dca-176">클러스터 프로 비전 하는 동안 hello 스크립트는 다른 설치 및 구성 프로세스와 동시에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-176">During cluster provisioning, hello script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="86dca-177">CPU 시간 또는 네트워크 대역폭 등의 리소스에 대 한 경합은 hello 스크립트 tootake 긴 toofinish 개발 환경에서 사용 하지 않고 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-177">Competition for resources such as CPU time or network bandwidth may cause hello script tootake longer toofinish than it does in your development environment.</span></span>
>
> <span data-ttu-id="86dca-178">toominimize hello 하나 toorun hello 스크립트 시간, 다운로드 및 소스에서 응용 프로그램을 컴파일 등의 작업을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-178">toominimize hello time it takes toorun hello script, avoid tasks such as downloading and compiling applications from source.</span></span> <span data-ttu-id="86dca-179">응용 프로그램을 미리 컴파일 하 고 Azure 저장소의 hello 이진 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-179">Pre-compile applications and store hello binary in Azure Storage.</span></span>


### <a name="script-action-on-a-running-cluster"></a><span data-ttu-id="86dca-180">실행 중인 클러스터의 스크립트 작업</span><span class="sxs-lookup"><span data-stu-id="86dca-180">Script action on a running cluster</span></span>

<span data-ttu-id="86dca-181">이미 실행 중인 클러스터에서 클러스터를 만드는 스크립트에 실패 하는 동안 사용 되는 작업을 실행 하는 스크립트와는 달리 hello 클러스터 toochange tooa 실패 상태가 자동으로 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-181">Unlike script actions used during cluster creation, a failure in a script ran on an already running cluster does not automatically cause hello cluster toochange tooa failed state.</span></span> <span data-ttu-id="86dca-182">스크립트가 완료 되 면 hello 클러스터 tooa "실행 중" 상태를 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-182">Once a script completes, hello cluster should return tooa "running" state.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="86dca-183">Hello 클러스터 상태가 '실행 중', 경우에 hello 실패 한 스크립트 수을 위반한 것 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-183">Even if hello cluster has a 'running' state, hello failed script may have broken things.</span></span> <span data-ttu-id="86dca-184">예를 들어 스크립트는 hello 클러스터에 필요한 파일을 삭제 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-184">For example, a script could delete files needed by hello cluster.</span></span>
>
> <span data-ttu-id="86dca-185">스크립트 동작 tooyour 클러스터를 적용 하기 전에 스크립트를 수행 하는 작업을 이해 해야 확인 해야 하므로 루트 권한으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-185">Scripts actions run with root privileges, so you should make sure that you understand what a script does before applying it tooyour cluster.</span></span>

<span data-ttu-id="86dca-186">Hello 클러스터 상태가 toofrom 변경 스크립트 tooa 클러스터를 적용할 때 **실행** 너무**"승인 됨"**, 다음 **HDInsight 구성**, 한 마지막 너무 다시**실행** 성공적인 스크립트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-186">When applying a script tooa cluster, hello cluster state changes toofrom **Running** too**Accepted**, then **HDInsight configuration**, and finally back too**Running** for successful scripts.</span></span> <span data-ttu-id="86dca-187">hello 스크립트 상태 hello 스크립트 동작 기록을 로그인 하 고 hello 스크립트의 성공 또는 실패 여부 정보 toodetermine이를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-187">hello script status is logged in hello script action history, and you can use this information toodetermine whether hello script succeeded or failed.</span></span> <span data-ttu-id="86dca-188">예를 들어 hello `Get-AzureRmHDInsightScriptActionHistory` PowerShell cmdlet에 사용 되는 tooview hello 상태의 스크립트 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-188">For example, hello `Get-AzureRmHDInsightScriptActionHistory` PowerShell cmdlet can be used tooview hello status of a script.</span></span> <span data-ttu-id="86dca-189">정보 비슷한 toohello를 다음 텍스트를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-189">It returns information similar toohello following text:</span></span>

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> <span data-ttu-id="86dca-190">Hello 클러스터를 만든 후 hello 클러스터 사용자 (관리자) 암호 변경 하면,이 클러스터에 대 한 작업을 실행 하는 스크립트 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-190">If you have changed hello cluster user (admin) password after hello cluster was created, script actions ran against this cluster may fail.</span></span> <span data-ttu-id="86dca-191">모든 지속형된 스크립트 동작을 해당 대상 작업자 노드가 있는 경우 이러한 스크립트는 hello 클러스터 크기를 조정할 때 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-191">If you have any persisted script actions that target worker nodes, these scripts may fail when you scale hello cluster.</span></span>

## <a name="example-script-action-scripts"></a><span data-ttu-id="86dca-192">예제 스크립트 작업 스크립트</span><span class="sxs-lookup"><span data-stu-id="86dca-192">Example Script Action scripts</span></span>

<span data-ttu-id="86dca-193">스크립트 작업 스크립트는 hello 다음 유틸리티를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-193">Script Action scripts can be used through hello following utilities:</span></span>

* <span data-ttu-id="86dca-194">Azure portal</span><span class="sxs-lookup"><span data-stu-id="86dca-194">Azure portal</span></span>
* <span data-ttu-id="86dca-195">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="86dca-195">Azure PowerShell</span></span>
* <span data-ttu-id="86dca-196">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="86dca-196">Azure CLI</span></span>
* <span data-ttu-id="86dca-197">HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="86dca-197">HDInsight .NET SDK</span></span>

<span data-ttu-id="86dca-198">HDInsight는 HDInsight 클러스터에서 다음과 같은 구성 요소가 스크립트 tooinstall hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-198">HDInsight provides scripts tooinstall hello following components on HDInsight clusters:</span></span>

| <span data-ttu-id="86dca-199">이름</span><span class="sxs-lookup"><span data-stu-id="86dca-199">Name</span></span> | <span data-ttu-id="86dca-200">스크립트</span><span class="sxs-lookup"><span data-stu-id="86dca-200">Script</span></span> |
| --- | --- |
| <span data-ttu-id="86dca-201">**Azure Storage 계정 추가**</span><span class="sxs-lookup"><span data-stu-id="86dca-201">**Add an Azure Storage account**</span></span> |<span data-ttu-id="86dca-202">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. 참조 [추가 저장소 추가 tooan HDInsight 클러스터](hdinsight-hadoop-add-storage.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-202">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. See [Add additional storage tooan HDInsight cluster](hdinsight-hadoop-add-storage.md).</span></span> |
| <span data-ttu-id="86dca-203">**Hue 설치**</span><span class="sxs-lookup"><span data-stu-id="86dca-203">**Install Hue**</span></span> |<span data-ttu-id="86dca-204">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. [HDInsight 클러스터에서 Hue 설치 및 사용](hdinsight-hadoop-hue-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86dca-204">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. See [Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> |
| <span data-ttu-id="86dca-205">**Presto 설치**</span><span class="sxs-lookup"><span data-stu-id="86dca-205">**Install Presto**</span></span> |<span data-ttu-id="86dca-206">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. [HDInsight 클러스터에 Presto 설치 및 사용](hdinsight-hadoop-install-presto.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86dca-206">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. See [Install and use Presto on HDInsight clusters](hdinsight-hadoop-install-presto.md).</span></span> |
| <span data-ttu-id="86dca-207">**Solr 설치**</span><span class="sxs-lookup"><span data-stu-id="86dca-207">**Install Solr**</span></span> |<span data-ttu-id="86dca-208">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. [HDInsight 클러스터에서 Solr 설치 및 사용](hdinsight-hadoop-solr-install-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86dca-208">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> |
| <span data-ttu-id="86dca-209">**Giraph 설치**</span><span class="sxs-lookup"><span data-stu-id="86dca-209">**Install Giraph**</span></span> |<span data-ttu-id="86dca-210">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. [HDInsight 클러스터에서 Giraph 설치 및 사용](hdinsight-hadoop-giraph-install-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86dca-210">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> |
| <span data-ttu-id="86dca-211">**Hive 라이브러리 사전 로드**</span><span class="sxs-lookup"><span data-stu-id="86dca-211">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="86dca-212">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. [HDInsight 클러스터에서 Hive 라이브러리 추가](hdinsight-hadoop-add-hive-libraries.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86dca-212">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md).</span></span> |
| <span data-ttu-id="86dca-213">**Mono 설치 또는 업데이트**</span><span class="sxs-lookup"><span data-stu-id="86dca-213">**Install or update Mono**</span></span> | <span data-ttu-id="86dca-214">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash.</span><span class="sxs-lookup"><span data-stu-id="86dca-214">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash.</span></span> <span data-ttu-id="86dca-215">[HDInsight에서 Mono 설치 또는 업데이트](hdinsight-hadoop-install-mono.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86dca-215">See [Install or update Mono on HDInsight](hdinsight-hadoop-install-mono.md).</span></span> |

## <a name="use-a-script-action-during-cluster-creation"></a><span data-ttu-id="86dca-216">클러스터를 만드는 동안 스크립트 작업 사용</span><span class="sxs-lookup"><span data-stu-id="86dca-216">Use a Script Action during cluster creation</span></span>

<span data-ttu-id="86dca-217">이 섹션에는 HDInsight 클러스터를 만들 때 작업 스크립트를 사용 하 여 hello 다른 방법을 예제를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-217">This section provides examples on hello different ways you can use script actions when creating an HDInsight cluster.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-hello-azure-portal"></a><span data-ttu-id="86dca-218">스크립트 작업을 사용 하 여 hello Azure 포털에서에서 클러스터를 만드는 동안</span><span class="sxs-lookup"><span data-stu-id="86dca-218">Use a Script Action during cluster creation from hello Azure portal</span></span>

1. <span data-ttu-id="86dca-219">[HDInsight에서 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)에서 설명한 대로 클러스터를 만들기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-219">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="86dca-220">Hello에 도달 하면 중지 __클러스터 요약__ 섹션.</span><span class="sxs-lookup"><span data-stu-id="86dca-220">Stop when you reach hello __Cluster summary__ section.</span></span>

2. <span data-ttu-id="86dca-221">Hello에서 __클러스터 요약__ 섹션을 선택 하는 hello __편집__ 에 대 한 링크 __고급 설정__합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-221">From hello __Cluster summary__ section, select hello __edit__ link for __Advanced settings__.</span></span>

    ![고급 설정 링크](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. <span data-ttu-id="86dca-223">Hello에서 __고급 설정__ 섹션에서 __스크립트 작업을__합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-223">From hello __Advanced settings__ section, select __Script actions__.</span></span> <span data-ttu-id="86dca-224">Hello에서 __스크립트 작업을__ 섹션에서 __+ new 전송__</span><span class="sxs-lookup"><span data-stu-id="86dca-224">From hello __Script actions__ section, select __+ Submit new__</span></span>

    ![새 스크립트 작업 제출](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. <span data-ttu-id="86dca-226">사용 하 여 hello __스크립트를 선택__ 항목 tooselect 미리 만들어 놓은 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-226">Use hello __Select a script__ entry tooselect a pre-made script.</span></span> <span data-ttu-id="86dca-227">toouse 사용자 지정 스크립트를 선택 __사용자 지정__ hello 다음 설명과 __이름__ 및 __URI 스크립트를 이용한 적__ 스크립트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-227">toouse a custom script, select __Custom__ and then provide hello __Name__ and __Bash script URI__ for your script.</span></span>

    ![Hello 선택 스크립트 형식으로 스크립트 추가](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="86dca-229">다음 표에서 hello hello 양식에 hello 요소에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-229">hello following table describes hello elements on hello form:</span></span>

    | <span data-ttu-id="86dca-230">속성</span><span class="sxs-lookup"><span data-stu-id="86dca-230">Property</span></span> | <span data-ttu-id="86dca-231">값</span><span class="sxs-lookup"><span data-stu-id="86dca-231">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="86dca-232">스크립트 선택</span><span class="sxs-lookup"><span data-stu-id="86dca-232">Select a script</span></span> | <span data-ttu-id="86dca-233">toouse 선택 사용자 지정 스크립트 __사용자 지정__합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-233">toouse your own script, select __Custom__.</span></span> <span data-ttu-id="86dca-234">그렇지 않은 경우 제공 된 hello 스크립트 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-234">Otherwise, select one of hello provided scripts.</span></span> |
    | <span data-ttu-id="86dca-235">이름</span><span class="sxs-lookup"><span data-stu-id="86dca-235">Name</span></span> |<span data-ttu-id="86dca-236">Hello 스크립트 동작에 대 한 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-236">Specify a name for hello script action.</span></span> |
    | <span data-ttu-id="86dca-237">Bash 스크립트 URI</span><span class="sxs-lookup"><span data-stu-id="86dca-237">Bash script URI</span></span> |<span data-ttu-id="86dca-238">가 호출 된 toocustomize hello 클러스터 hello URI toohello 스크립트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-238">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> |
    | <span data-ttu-id="86dca-239">Head/Worker/Zookeeper</span><span class="sxs-lookup"><span data-stu-id="86dca-239">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="86dca-240">Hello 노드를 지정 (**h e a d**, **작업자**, 또는 **사육**) hello 사용자 정의 스크립트 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-240">Specify hello nodes (**Head**, **Worker**, or **ZooKeeper**) on which hello customization script is run.</span></span> |
    | <span data-ttu-id="86dca-241">매개 변수</span><span class="sxs-lookup"><span data-stu-id="86dca-241">Parameters</span></span> |<span data-ttu-id="86dca-242">Hello 스크립트에 필요한 경우 hello 매개 변수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-242">Specify hello parameters, if required by hello script.</span></span> |

    <span data-ttu-id="86dca-243">사용 하 여 hello __이 스크립트 동작이 계속__ 스크립트 hello 항목 tooensure 작업 크기 조정 하는 동안 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-243">Use hello __Persist this script action__ entry tooensure that hello script is applied during scaling operations.</span></span>

5. <span data-ttu-id="86dca-244">선택 __만들기__ toosave hello 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-244">Select __Create__ toosave hello script.</span></span> <span data-ttu-id="86dca-245">사용할 수 있습니다 __+ 새 전송__ tooadd 또 다른 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-245">You can then use __+ Submit new__ tooadd another script.</span></span>

    ![여러 스크립트 작업](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    <span data-ttu-id="86dca-247">Hello를 사용 하 여 스크립트를 추가 마쳤으면 __선택__ 단추를 클릭 한 다음 hello __다음__ 단추 tooreturn toohello __클러스터 요약__ 섹션.</span><span class="sxs-lookup"><span data-stu-id="86dca-247">When you are done adding scripts, use hello __Select__ button, and then hello __Next__ button tooreturn toohello __Cluster summary__ section.</span></span>

3. <span data-ttu-id="86dca-248">선택 toocreate hello 클러스터 __만들기__ hello에서 __클러스터 요약__ 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-248">toocreate hello cluster, select __Create__ from hello __Cluster summary__ selection.</span></span>

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a><span data-ttu-id="86dca-249">Azure 리소스 관리자 템플릿에서 스크립트 작업 사용</span><span class="sxs-lookup"><span data-stu-id="86dca-249">Use a Script Action from Azure Resource Manager templates</span></span>

<span data-ttu-id="86dca-250">이 섹션의 예제 hello toouse Azure 리소스 관리자 템플릿 사용 하 여 작업을 스크립팅 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-250">hello examples in this section demonstrate how toouse script actions with Azure Resource Manager templates.</span></span>

#### <a name="before-you-begin"></a><span data-ttu-id="86dca-251">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="86dca-251">Before you begin</span></span>

* <span data-ttu-id="86dca-252">워크스테이션 toorun HDInsight Powershell cmdlet을 구성 하는 방법에 대 한 정보를 참조 하십시오. [설치 Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-252">For information about configuring a workstation toorun HDInsight Powershell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="86dca-253">방법에 대 한 지침은 toocreate 템플릿 참조 [제작 Azure 리소스 관리자 템플릿을](../azure-resource-manager/resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-253">For instructions on how toocreate templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="86dca-254">이전에 리소스 관리자에서 Azure PowerShell을 사용하지 않은 경우 [Azure 리소스 관리자와 함께 Azure PowerShell 사용](../azure-resource-manager/powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86dca-254">If you have not previously used Azure PowerShell with Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

#### <a name="create-clusters-using-script-action"></a><span data-ttu-id="86dca-255">스크립트 작업을 사용하여 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="86dca-255">Create clusters using Script Action</span></span>

1. <span data-ttu-id="86dca-256">컴퓨터에서 수정할 수 있는 템플릿 tooa 위치 hello를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-256">Copy hello following template tooa location on your computer.</span></span> <span data-ttu-id="86dca-257">이 서식 파일 hello headnodes 및 작업자 클러스터의 노드에서 hello Giraph를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-257">This template installs Giraph on hello headnodes and worker nodes in hello cluster.</span></span> <span data-ttu-id="86dca-258">Hello JSON 템플릿을 유효한 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-258">You can also verify if hello JSON template is valid.</span></span> <span data-ttu-id="86dca-259">템플릿 콘텐츠를 [JSONLint](http://jsonlint.com/), 즉, 온라인 JSON 유효성 검사기 도구에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-259">Paste your template content into [JSONLint](http://jsonlint.com/), an online JSON validation tool.</span></span>

            {
            "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
            "contentVersion": "1.0.0.0",
            "parameters": {
                "clusterLocation": {
                    "type": "string",
                    "defaultValue": "West US",
                    "allowedValues": [ "West US" ]
                },
                "clusterName": {
                    "type": "string"
                },
                "clusterUserName": {
                    "type": "string",
                    "defaultValue": "admin"
                },
                "clusterUserPassword": {
                    "type": "securestring"
                },
                "sshUserName": {
                    "type": "string",
                    "defaultValue": "username"
                },
                "sshPassword": {
                    "type": "securestring"
                },
                "clusterStorageAccountName": {
                    "type": "string"
                },
                "clusterStorageAccountResourceGroup": {
                    "type": "string"
                },
                "clusterStorageType": {
                    "type": "string",
                    "defaultValue": "Standard_LRS",
                    "allowedValues": [
                        "Standard_LRS",
                        "Standard_GRS",
                        "Standard_ZRS"
                    ]
                },
                "clusterStorageAccountContainer": {
                    "type": "string"
                },
                "clusterHeadNodeCount": {
                    "type": "int",
                    "defaultValue": 1
                },
                "clusterWorkerNodeCount": {
                    "type": "int",
                    "defaultValue": 2
                }
            },
            "variables": {
            },
            "resources": [
                {
                    "name": "[parameters('clusterStorageAccountName')]",
                    "type": "Microsoft.Storage/storageAccounts",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-05-01-preview",
                    "dependsOn": [ ],
                    "tags": { },
                    "properties": {
                        "accountType": "[parameters('clusterStorageType')]"
                    }
                },
                {
                    "name": "[parameters('clusterName')]",
                    "type": "Microsoft.HDInsight/clusters",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-03-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Storage/storageAccounts/', parameters('clusterStorageAccountName'))]"
                    ],
                    "tags": { },
                    "properties": {
                        "clusterVersion": "3.2",
                        "osType": "Linux",
                        "clusterDefinition": {
                            "kind": "hadoop",
                            "configurations": {
                                "gateway": {
                                    "restAuthCredential.isEnabled": true,
                                    "restAuthCredential.username": "[parameters('clusterUserName')]",
                                    "restAuthCredential.password": "[parameters('clusterUserPassword')]"
                                }
                            }
                        },
                        "storageProfile": {
                            "storageaccounts": [
                                {
                                    "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                                    "isDefault": true,
                                    "container": "[parameters('clusterStorageAccountContainer')]",
                                    "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), '2015-05-01-preview').key1]"
                                }
                            ]
                        },
                        "computeProfile": {
                            "roles": [
                                {
                                    "name": "headnode",
                                    "targetInstanceCount": "[parameters('clusterHeadNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installGiraph",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                },
                                {
                                    "name": "workernode",
                                    "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installR",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                }
            ],
            "outputs": {
                "cluster":{
                    "type" : "object",
                    "value" : "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                }
            }
        }
2. <span data-ttu-id="86dca-260">Azure PowerShell을 시작 하 고 Azure 계정을 tooyour 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-260">Start Azure PowerShell and Log in tooyour Azure account.</span></span> <span data-ttu-id="86dca-261">Hello 명령은 자격 증명을 입력 한 후 계정에 대 한 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-261">After providing your credentials, hello command returns information about your account.</span></span>

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. <span data-ttu-id="86dca-262">Hello 구독 ID를 제공 하는 여러 구독이 있는 경우 배포에 대 한 toouse를 백업본 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-262">If you have multiple subscriptions, provide hello subscription ID you wish toouse for deployment.</span></span>

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > <span data-ttu-id="86dca-263">사용할 수 있습니다 `Get-AzureRmSubscription` tooget 각각에 대 한 hello 구독 ID를 포함 하는 사용자 계정과 연결 된 모든 구독의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-263">You can use `Get-AzureRmSubscription` tooget a list of all subscriptions associated with your account, which includes hello subscription ID for each one.</span></span>

4. <span data-ttu-id="86dca-264">기본 리소스 그룹이 없는 경우 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-264">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="86dca-265">Hello 이름 hello 리소스 그룹 및 솔루션에 필요한 위치를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-265">Provide hello name of hello resource group and location that you need for your solution.</span></span> <span data-ttu-id="86dca-266">Hello 새 리소스 그룹의 요약이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-266">A summary of hello new resource group is returned.</span></span>

        New-AzureRmResourceGroup -Name myresourcegroup -Location "West US"

        ResourceGroupName : myresourcegroup
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/######/resourceGroups/ExampleResourceGroup

5. <span data-ttu-id="86dca-267">toocreate hello를 실행 하 여 리소스 그룹에 대 한 배포 **새로 AzureRmResourceGroupDeployment** 명령 및 hello 필요한 매개 변수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-267">toocreate a deployment for your resource group, run hello **New-AzureRmResourceGroupDeployment** command and provide hello necessary parameters.</span></span> <span data-ttu-id="86dca-268">hello 매개 변수는 같은 데이터가 hello를 같습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-268">hello parameters include hello following data:</span></span>

    * <span data-ttu-id="86dca-269">배포에 사용할 이름</span><span class="sxs-lookup"><span data-stu-id="86dca-269">A name for your deployment</span></span>
    * <span data-ttu-id="86dca-270">리소스 그룹의 hello 이름</span><span class="sxs-lookup"><span data-stu-id="86dca-270">hello name of your resource group</span></span>
    * <span data-ttu-id="86dca-271">hello 경로 또는 URL toohello 만든 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-271">hello path or URL toohello template you created.</span></span>

  <span data-ttu-id="86dca-272">템플릿에 매개 변수가 필요한 경우 해당 매개 변수를 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-272">If your template requires any parameters, you must pass those parameters as well.</span></span> <span data-ttu-id="86dca-273">이 경우 hello 클러스터에서 hello 스크립트 동작 tooinstall R 매개 변수가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-273">In this case, hello script action tooinstall R on hello cluster does not require any parameters.</span></span>

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    <span data-ttu-id="86dca-274">사용자는 hello 서식 파일에 정의 된 hello 매개 변수에 대 한 증명된 tooprovide 값입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-274">You are prompted tooprovide values for hello parameters defined in hello template.</span></span>

1. <span data-ttu-id="86dca-275">Hello 리소스 그룹 배포 된 hello 배포의 요약이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-275">When hello resource group has been deployed, a summary of hello deployment is displayed.</span></span>

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/14/2017 7:00:27 PM
          Mode              : Incremental
          ...

2. <span data-ttu-id="86dca-276">배포에 실패할 경우에 다음 cmdlet tooget 정보 hello 실패에 대 한 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-276">If your deployment fails, you can use hello following cmdlets tooget information about hello failures.</span></span>

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a><span data-ttu-id="86dca-277">클러스터를 만드는 동안 Azure PowerShell에서 스크립트 작업 사용</span><span class="sxs-lookup"><span data-stu-id="86dca-277">Use a Script Action during cluster creation from Azure PowerShell</span></span>

<span data-ttu-id="86dca-278">이 섹션을 사용 하 여 hello [추가 AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) 스크립트 동작 toocustomize 클러스터를 사용 하 여 cmdlet tooinvoke 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-278">In this section, we use hello [Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet tooinvoke scripts by using Script Action toocustomize a cluster.</span></span> <span data-ttu-id="86dca-279">계속하기 전에 Azure PowerShell을 설치 및 구성했는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="86dca-279">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="86dca-280">워크스테이션 toorun HDInsight PowerShell cmdlet을 구성 하는 방법에 대 한 정보를 참조 하십시오. [설치 Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-280">For information about configuring a workstation toorun HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="86dca-281">hello 다음 스크립트에서는 방법을 tooapply PowerShell을 사용 하는 클러스터를 만들 때 스크립트 동작:</span><span class="sxs-lookup"><span data-stu-id="86dca-281">hello following script demonstrates how tooapply a script action when creating a cluster using PowerShell:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]

<span data-ttu-id="86dca-282">Hello 클러스터를 만들기 전에 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-282">It can take several minutes before hello cluster is created.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-hello-hdinsight-net-sdk"></a><span data-ttu-id="86dca-283">스크립트 작업을 사용 하 여 hello HDInsight.NET SDK에서에서 클러스터를 만드는 동안</span><span class="sxs-lookup"><span data-stu-id="86dca-283">Use a Script Action during cluster creation from hello HDInsight .NET SDK</span></span>

<span data-ttu-id="86dca-284">HDInsight.NET SDK hello HDInsight와 보다 쉽게 toowork.NET 응용 프로그램에서 사용 하면 클라이언트 라이브러리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-284">hello HDInsight .NET SDK provides client libraries that makes it easier toowork with HDInsight from a .NET application.</span></span> <span data-ttu-id="86dca-285">코드 샘플을 보려면 [사용 하 여 HDInsight 클러스터 만들기 Linux 기반 hello.NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-285">For a code sample, see [Create Linux-based clusters in HDInsight using hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span></span>

## <a name="apply-a-script-action-tooa-running-cluster"></a><span data-ttu-id="86dca-286">클러스터 실행 스크립트 동작 tooa 적용</span><span class="sxs-lookup"><span data-stu-id="86dca-286">Apply a Script Action tooa running cluster</span></span>

<span data-ttu-id="86dca-287">이 섹션에서는 tooapply 클러스터를 실행 하는 작업 tooa를 스크립팅 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-287">In this section, learn how tooapply script actions tooa running cluster.</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-portal"></a><span data-ttu-id="86dca-288">Hello Azure 포털에서에서 클러스터를 실행 하는 스크립트 작업 tooa 적용</span><span class="sxs-lookup"><span data-stu-id="86dca-288">Apply a Script Action tooa running cluster from hello Azure portal</span></span>

1. <span data-ttu-id="86dca-289">Hello에서 [Azure 포털](https://portal.azure.com)를 HDInsight 클러스터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-289">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="86dca-290">Hello HDInsight 클러스터 개요에서 선택 hello **스크립트 동작** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-290">From hello HDInsight cluster overview, select hello **Script Actions** tile.</span></span>

    ![스크립트 작업 타일](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="86dca-292">선택할 수도 있습니다 **모든 설정을** 선택한 후 **스크립트 동작** hello 설정 섹션에서에서.</span><span class="sxs-lookup"><span data-stu-id="86dca-292">You can also select **All settings** and then select **Script Actions** from hello Settings section.</span></span>

3. <span data-ttu-id="86dca-293">스크립트 동작 섹션 hello의 hello 위에서 선택 **새 전송**합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-293">From hello top of hello Script Actions section, select **Submit new**.</span></span>

    ![클러스터를 실행 하는 스크립트 tooa 추가](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. <span data-ttu-id="86dca-295">사용 하 여 hello __스크립트를 선택__ 항목 tooselect 미리 만들어 놓은 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-295">Use hello __Select a script__ entry tooselect a pre-made script.</span></span> <span data-ttu-id="86dca-296">toouse 사용자 지정 스크립트를 선택 __사용자 지정__ hello 다음 설명과 __이름__ 및 __URI 스크립트를 이용한 적__ 스크립트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-296">toouse a custom script, select __Custom__ and then provide hello __Name__ and __Bash script URI__ for your script.</span></span>

    ![Hello 선택 스크립트 형식으로 스크립트 추가](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="86dca-298">다음 표에서 hello hello 양식에 hello 요소에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-298">hello following table describes hello elements on hello form:</span></span>

    | <span data-ttu-id="86dca-299">속성</span><span class="sxs-lookup"><span data-stu-id="86dca-299">Property</span></span> | <span data-ttu-id="86dca-300">값</span><span class="sxs-lookup"><span data-stu-id="86dca-300">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="86dca-301">스크립트 선택</span><span class="sxs-lookup"><span data-stu-id="86dca-301">Select a script</span></span> | <span data-ttu-id="86dca-302">toouse 선택 사용자 지정 스크립트 __사용자 지정__합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-302">toouse your own script, select __custom__.</span></span> <span data-ttu-id="86dca-303">그렇지 않은 경우 제공된 스크립트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-303">Otherwise, select a provided script.</span></span> |
    | <span data-ttu-id="86dca-304">이름</span><span class="sxs-lookup"><span data-stu-id="86dca-304">Name</span></span> |<span data-ttu-id="86dca-305">Hello 스크립트 동작에 대 한 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-305">Specify a name for hello script action.</span></span> |
    | <span data-ttu-id="86dca-306">Bash 스크립트 URI</span><span class="sxs-lookup"><span data-stu-id="86dca-306">Bash script URI</span></span> |<span data-ttu-id="86dca-307">가 호출 된 toocustomize hello 클러스터 hello URI toohello 스크립트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-307">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> |
    | <span data-ttu-id="86dca-308">Head/Worker/Zookeeper</span><span class="sxs-lookup"><span data-stu-id="86dca-308">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="86dca-309">Hello 노드를 지정 (**h e a d**, **작업자**, 또는 **사육**) hello 사용자 정의 스크립트 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-309">Specify hello nodes (**Head**, **Worker**, or **ZooKeeper**) on which hello customization script is run.</span></span> |
    | <span data-ttu-id="86dca-310">매개 변수</span><span class="sxs-lookup"><span data-stu-id="86dca-310">Parameters</span></span> |<span data-ttu-id="86dca-311">Hello 스크립트에 필요한 경우 hello 매개 변수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-311">Specify hello parameters, if required by hello script.</span></span> |

    <span data-ttu-id="86dca-312">사용 하 여 hello __이 스크립트 동작이 계속__ 항목 toomake 있는지 hello 스크립트 작업을 확장 하는 동안 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-312">Use hello __Persist this script action__ entry toomake sure hello script is applied during scaling operations.</span></span>

5. <span data-ttu-id="86dca-313">마지막으로 hello를 사용 하 여 **만들기** 단추 tooapply hello 스크립트 toohello 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-313">Finally, use hello **Create** button tooapply hello script toohello cluster.</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-azure-powershell"></a><span data-ttu-id="86dca-314">Azure PowerShell에서 클러스터를 실행 하는 스크립트 작업 tooa 적용</span><span class="sxs-lookup"><span data-stu-id="86dca-314">Apply a Script Action tooa running cluster from Azure PowerShell</span></span>

<span data-ttu-id="86dca-315">계속하기 전에 Azure PowerShell을 설치 및 구성했는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="86dca-315">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="86dca-316">워크스테이션 toorun HDInsight PowerShell cmdlet을 구성 하는 방법에 대 한 정보를 참조 하십시오. [설치 Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-316">For information about configuring a workstation toorun HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="86dca-317">hello 다음 예제에서는 어떻게 tooapply 스크립트 동작 tooa 실행 중인 클러스터:</span><span class="sxs-lookup"><span data-stu-id="86dca-317">hello following example demonstrates how tooapply a script action tooa running cluster:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]

<span data-ttu-id="86dca-318">Hello 작업이 완료 되 면 정보 비슷한 toohello를 텍스트 다음 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-318">Once hello operation completes, you receive information similar toohello following text:</span></span>

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-cli"></a><span data-ttu-id="86dca-319">Hello Azure CLI에서에서 클러스터를 실행 하는 스크립트 작업 tooa 적용</span><span class="sxs-lookup"><span data-stu-id="86dca-319">Apply a Script Action tooa running cluster from hello Azure CLI</span></span>

<span data-ttu-id="86dca-320">계속 하기 전에 설치 하 고 hello Azure CLI를 구성 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-320">Before proceeding, make sure you have installed and configured hello Azure CLI.</span></span> <span data-ttu-id="86dca-321">자세한 내용은 참조 [설치 hello Azure CLI](../cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-321">For more information, see [Install hello Azure CLI](../cli-install-nodejs.md).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="86dca-322">tooswitch tooAzure Resource Manager 모드로, 다음 hello 명령줄에서 명령을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="86dca-322">tooswitch tooAzure Resource Manager mode, use hello following command at hello command line:</span></span>

        azure config mode arm

2. <span data-ttu-id="86dca-323">Hello 다음 tooauthenticate tooyour Azure 구독을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-323">Use hello following tooauthenticate tooyour Azure subscription.</span></span>

        azure login

3. <span data-ttu-id="86dca-324">다음 명령은 tooapply 클러스터를 실행 하는 스크립트 작업 tooa hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="86dca-324">Use hello following command tooapply a script action tooa running cluster</span></span>

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    <span data-ttu-id="86dca-325">이 명령에 대한 매개 변수를 생략한 경우 해당 매개 변수를 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-325">If you omit parameters for this command, you are prompted for them.</span></span> <span data-ttu-id="86dca-326">하는 경우 스크립트를 사용 하 여 지정한 hello `-u` 에서는 매개 변수를 지정할 수 있습니다 hello를 통해 `-p` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-326">If hello script you specify with `-u` accepts parameters, you can specify them using hello `-p` parameter.</span></span>

    <span data-ttu-id="86dca-327">유효한 노드 형식은 `headnode`, `workernode` 및 `zookeeper`입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-327">Valid node types are `headnode`, `workernode`, and `zookeeper`.</span></span> <span data-ttu-id="86dca-328">Hello 스크립트는 노드 유형에 적용된 toomultiple 이어야 하 고, 경우에 hello 형식을 구분 하 여 지정 된 ';'.</span><span class="sxs-lookup"><span data-stu-id="86dca-328">If hello script should be applied toomultiple node types, specify hello types separated by a ';'.</span></span> <span data-ttu-id="86dca-329">예: `-n headnode;workernode`.</span><span class="sxs-lookup"><span data-stu-id="86dca-329">For example, `-n headnode;workernode`.</span></span>

    <span data-ttu-id="86dca-330">toopersist hello 스크립트, 추가 hello `--persistOnSuccess`합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-330">toopersist hello script, add hello `--persistOnSuccess`.</span></span> <span data-ttu-id="86dca-331">사용 하 여 hello 스크립트를 나중에 유지할 수도 있습니다 `azure hdinsight script-action persisted set`합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-331">You can also persist hello script later by using `azure hdinsight script-action persisted set`.</span></span>

    <span data-ttu-id="86dca-332">Hello 작업이 완료 되 면 출력 유사한 toohello를 텍스트 다음 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-332">Once hello job completes, you receive output similar toohello following text:</span></span>

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-tooa-running-cluster-using-rest-api"></a><span data-ttu-id="86dca-333">REST API를 사용 하 여 클러스터를 실행 하는 스크립트 작업 tooa 적용</span><span class="sxs-lookup"><span data-stu-id="86dca-333">Apply a Script Action tooa running cluster using REST API</span></span>

<span data-ttu-id="86dca-334">[실행 중인 클러스터의 스크립트 작업](https://msdn.microsoft.com/library/azure/mt668441.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86dca-334">See [Run Script Actions on a running cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-hdinsight-net-sdk"></a><span data-ttu-id="86dca-335">Hello HDInsight.NET SDK에서에서 클러스터를 실행 하는 스크립트 작업 tooa 적용</span><span class="sxs-lookup"><span data-stu-id="86dca-335">Apply a Script Action tooa running cluster from hello HDInsight .NET SDK</span></span>

<span data-ttu-id="86dca-336">Hello.NET SDK tooapply 스크립트 tooa 클러스터를 사용 하 여 예제를 보려면 [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action)합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-336">For an example of using hello .NET SDK tooapply scripts tooa cluster, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

## <a name="view-history-promote-and-demote-script-actions"></a><span data-ttu-id="86dca-337">기록 보기, 스크립트 작업 승격 및 강등</span><span class="sxs-lookup"><span data-stu-id="86dca-337">View history, promote, and demote Script Actions</span></span>

### <a name="using-hello-azure-portal"></a><span data-ttu-id="86dca-338">Hello Azure 포털을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="86dca-338">Using hello Azure portal</span></span>

1. <span data-ttu-id="86dca-339">Hello에서 [Azure 포털](https://portal.azure.com)를 HDInsight 클러스터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-339">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="86dca-340">Hello HDInsight 클러스터 개요에서 선택 hello **스크립트 동작** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-340">From hello HDInsight cluster overview, select hello **Script Actions** tile.</span></span>

    ![스크립트 작업 타일](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="86dca-342">선택할 수도 있습니다 **모든 설정을** 선택한 후 **스크립트 동작** hello 설정 섹션에서에서.</span><span class="sxs-lookup"><span data-stu-id="86dca-342">You can also select **All settings** and then select **Script Actions** from hello Settings section.</span></span>

4. <span data-ttu-id="86dca-343">이 클러스터에 대 한 스크립트의 기록은 hello 스크립트 동작 섹션에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-343">A history of scripts for this cluster is displayed on hello Script Actions section.</span></span> <span data-ttu-id="86dca-344">이 정보에는 지속된 스크립트 목록이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-344">This information includes a list of persisted scripts.</span></span> <span data-ttu-id="86dca-345">아래 hello 스크린샷에서 Solr 스크립트 되었습니다.이 클러스터에서 실행 하는 hello를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-345">In hello screenshot below, you can see that hello Solr script has been ran on this cluster.</span></span> <span data-ttu-id="86dca-346">hello 스크린 샷 지속형된 스크립트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-346">hello screenshot does not show any persisted scripts.</span></span>

    ![스크립트 작업 섹션](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. <span data-ttu-id="86dca-348">Hello 기록에서 스크립트를 선택 하면이 스크립트에 대 한 hello 속성 섹션을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-348">Selecting a script from hello history displays hello Properties section for this script.</span></span> <span data-ttu-id="86dca-349">Hello 화면 hello 위에서 hello 스크립트를 다시 실행할 수도 있고 수준을 올릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-349">From hello top of hello screen, you can rerun hello script or promote it.</span></span>

    ![스크립트 작업 속성](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. <span data-ttu-id="86dca-351">Hello를 사용할 수도 있습니다 **...**  toohello hello 스크립트 동작 섹션 tooperform 동작에 대 한 항목의 오른쪽입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-351">You can also use hello **...** toohello right of entries on hello Script Actions section tooperform actions.</span></span>

    ![스크립트 작업 ... 사용량](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a><span data-ttu-id="86dca-353">Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="86dca-353">Using Azure PowerShell</span></span>

| <span data-ttu-id="86dca-354">Hello 다음을 사용 하는 중...</span><span class="sxs-lookup"><span data-stu-id="86dca-354">Use hello following...</span></span> | <span data-ttu-id="86dca-355">너무...</span><span class="sxs-lookup"><span data-stu-id="86dca-355">too...</span></span> |
| --- | --- |
| <span data-ttu-id="86dca-356">Get-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="86dca-356">Get-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="86dca-357">지속형 스크립트 작업에 대한 정보 검색</span><span class="sxs-lookup"><span data-stu-id="86dca-357">Retrieve information on persisted script actions</span></span> |
| <span data-ttu-id="86dca-358">Get-AzureRmHDInsightScriptActionHistory</span><span class="sxs-lookup"><span data-stu-id="86dca-358">Get-AzureRmHDInsightScriptActionHistory</span></span> |<span data-ttu-id="86dca-359">기록을 스크립트 적용 되는 동작 toohello 클러스터 또는 특정 스크립트에 대 한 세부 정보를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-359">Retrieve a history of script actions applied toohello cluster, or details for a specific script</span></span> |
| <span data-ttu-id="86dca-360">Set-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="86dca-360">Set-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="86dca-361">임시 승격 스크립트 동작 tooa 지속형 스크립트 동작</span><span class="sxs-lookup"><span data-stu-id="86dca-361">Promotes an ad hoc script action tooa persisted script action</span></span> |
| <span data-ttu-id="86dca-362">Remove-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="86dca-362">Remove-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="86dca-363">지속형된 스크립트 동작 tooan 임시 작업을 강등합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-363">Demotes a persisted script action tooan ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="86dca-364">사용 하 여 `Remove-AzureRmHDInsightPersistedScriptAction` 스크립트에서 수행 하는 hello 동작 실행 취소 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-364">Using `Remove-AzureRmHDInsightPersistedScriptAction` does not undo hello actions performed by a script.</span></span> <span data-ttu-id="86dca-365">이 cmdlet만 hello 지속형된 플래그를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-365">This cmdlet only removes hello persisted flag.</span></span>

<span data-ttu-id="86dca-366">다음 예제 스크립트는 hello hello cmdlet toopromote를 사용 하 여 다음 스크립트의 수준을 내리려면 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-366">hello following example script demonstrates using hello cmdlets toopromote, then demote a script.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]

### <a name="using-hello-azure-cli"></a><span data-ttu-id="86dca-367">Hello Azure CLI를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="86dca-367">Using hello Azure CLI</span></span>

| <span data-ttu-id="86dca-368">Hello 다음을 사용 하는 중...</span><span class="sxs-lookup"><span data-stu-id="86dca-368">Use hello following...</span></span> | <span data-ttu-id="86dca-369">너무...</span><span class="sxs-lookup"><span data-stu-id="86dca-369">too...</span></span> |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |<span data-ttu-id="86dca-370">지속형 스크립트 작업의 목록을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-370">Retrieve a list of persisted script actions</span></span> |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |<span data-ttu-id="86dca-371">특정 지속형 스크립트 작업에 대한 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-371">Retrieve information on a specific persisted script action</span></span> |
| `azure hdinsight script-action history list <clustername>` |<span data-ttu-id="86dca-372">스크립트 적용 되는 동작 toohello 클러스터의 기록을 검색합니다</span><span class="sxs-lookup"><span data-stu-id="86dca-372">Retrieve a history of script actions applied toohello cluster</span></span> |
| `azure hdinsight script-action history show <clustername> <scriptname>` |<span data-ttu-id="86dca-373">특정 스크립트 작업에 대한 정보 검색</span><span class="sxs-lookup"><span data-stu-id="86dca-373">Retrieve information on a specific script action</span></span> |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |<span data-ttu-id="86dca-374">임시 승격 스크립트 동작 tooa 지속형 스크립트 동작</span><span class="sxs-lookup"><span data-stu-id="86dca-374">Promotes an ad hoc script action tooa persisted script action</span></span> |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |<span data-ttu-id="86dca-375">지속형된 스크립트 동작 tooan 임시 작업을 강등합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-375">Demotes a persisted script action tooan ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="86dca-376">사용 하 여 `azure hdinsight script-action persisted delete` 스크립트에서 수행 하는 hello 동작 실행 취소 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-376">Using `azure hdinsight script-action persisted delete` does not undo hello actions performed by a script.</span></span> <span data-ttu-id="86dca-377">이 cmdlet만 hello 지속형된 플래그를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-377">This cmdlet only removes hello persisted flag.</span></span>

### <a name="using-hello-hdinsight-net-sdk"></a><span data-ttu-id="86dca-378">Hello HDInsight.NET SDK를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="86dca-378">Using hello HDInsight .NET SDK</span></span>

<span data-ttu-id="86dca-379">Hello.NET SDK tooretrieve 스크립트 기록 하는 클러스터에서 사용 하는 예로, 승격 또는 스크립트의 수준을 내리려면, 참조 [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action)합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-379">For an example of using hello .NET SDK tooretrieve script history from a cluster, promote or demote scripts, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

> [!NOTE]
> <span data-ttu-id="86dca-380">이 예제에서는 또한 tooinstall HDInsight를 통해 응용 프로그램에서.NET SDK를 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-380">This example also demonstrates how tooinstall an HDInsight application using hello .NET SDK.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="86dca-381">HDInsight 클러스터에서 사용하는 오픈 소스 소프트웨어 지원</span><span class="sxs-lookup"><span data-stu-id="86dca-381">Support for open-source software used on HDInsight clusters</span></span>

<span data-ttu-id="86dca-382">Microsoft Azure HDInsight 서비스 hello Hadoop 주위 형성 하는 오픈 소스 기술 프로그램 에코 시스템을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-382">hello Microsoft Azure HDInsight service uses an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="86dca-383">Microsoft Azure는 오픈 소스 기술에 대한 일반 수준의 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-383">Microsoft Azure provides a general level of support for open-source technologies.</span></span> <span data-ttu-id="86dca-384">자세한 내용은 참조 hello **지원 범위** hello 섹션 [Azure 지원 FAQ 웹 사이트](https://azure.microsoft.com/support/faq/)합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-384">For more information, see hello **Support Scope** section of hello [Azure Support FAQ website](https://azure.microsoft.com/support/faq/).</span></span> <span data-ttu-id="86dca-385">기본 제공 구성 요소에 대 한 지원의 수준을 추가로 제공 하는 hello HDInsight 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-385">hello HDInsight service provides an additional level of support for built-in components.</span></span>

<span data-ttu-id="86dca-386">Hello HDInsight 서비스에서에서 사용할 수 있는 오픈 소스 구성 요소는 다음과 같은 두 종류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-386">There are two types of open-source components that are available in hello HDInsight service:</span></span>

* <span data-ttu-id="86dca-387">**기본 제공 구성 요소** -이 구성 요소는 HDInsight 클러스터에 미리 설치 되어 하며 hello 클러스터의 핵심 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-387">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of hello cluster.</span></span> <span data-ttu-id="86dca-388">예를 들어 YARN ResourceManager, hello 하이브 쿼리 언어 (HiveQL) 및 hello Mahout 라이브러리 toothis 범주에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-388">For example, YARN ResourceManager, hello Hive query language (HiveQL), and hello Mahout library belong toothis category.</span></span> <span data-ttu-id="86dca-389">클러스터 구성 요소 전체 목록은 영어로 [HDInsight에서 제공 하는 hello Hadoop 클러스터 버전의 새로운 기능](hdinsight-component-versioning.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-389">A full list of cluster components is available in [What's new in hello Hadoop cluster versions provided by HDInsight](hdinsight-component-versioning.md).</span></span>
* <span data-ttu-id="86dca-390">**사용자 지정 구성 요소** -, hello 클러스터의 사용자로 설치 또는 hello 커뮤니티에서 사용할 수 있거나 사용자가 만든 모든 구성 요소를 작업에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-390">**Custom components** - You, as a user of hello cluster, can install or use in your workload any component available in hello community or created by you.</span></span>

> [!WARNING]
> <span data-ttu-id="86dca-391">Hello HDInsight 클러스터와 함께 제공 되는 구성 요소를 완전히 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-391">Components provided with hello HDInsight cluster are fully supported.</span></span> <span data-ttu-id="86dca-392">Microsoft 지원 tooisolate 주며 toothese 관련된 구성 요소 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-392">Microsoft Support helps tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="86dca-393">사용자 지정 구성 요소 상업적으로 적절 한 지원 toohelp 수신 하면 toofurther hello 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-393">Custom components receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="86dca-394">Microsoft 지원 수 tooresolve hello 문제 이거나 해당 기술에 대 한 심층 전문 지식이 있는 hello 오픈 소스 기술에 대 한 사용 가능한 채널 tooengage 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-394">Microsoft support may be able tooresolve hello issue OR they may ask you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="86dca-395">예를 들어 [HDInsight에 대한 MSDN 포럼](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com)과 같은 여러 커뮤니티 사이트를 사용할 수 있습니다. Apache 프로젝트는 [http://apache.org](http://apache.org)에 프로젝트 사이트가 있습니다(예: [Hadoop](http://hadoop.apache.org/)).</span><span class="sxs-lookup"><span data-stu-id="86dca-395">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

<span data-ttu-id="86dca-396">HDInsight 서비스 hello toouse 사용자 지정 구성 요소를 여러 가지 방법으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-396">hello HDInsight service provides several ways toouse custom components.</span></span> <span data-ttu-id="86dca-397">hello 구성 요소는 사용 되거나 hello 클러스터에 설치 하는 것에 관계 없이 동일한 지원 수준으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-397">hello same level of support applies, regardless of how a component is used or installed on hello cluster.</span></span> <span data-ttu-id="86dca-398">hello 다음 목록에서는 설명 hello 가장 일반적인 방법은 사용자 지정 구성 요소를 사용할 수 있도록 하는 HDInsight 클러스터에서:</span><span class="sxs-lookup"><span data-stu-id="86dca-398">hello following list describes hello most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="86dca-399">작업 제출-Hadoop 또는 기타 유형의 작업을 실행 하거나 사용자 지정 구성 요소를 사용 하 여 제출 된 toohello 클러스터가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-399">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted toohello cluster.</span></span>

2. <span data-ttu-id="86dca-400">클러스터를 만드는 동안 클러스터 사용자 지정-추가 설정과 hello 클러스터 노드에 설치 된 사용자 지정 구성 요소를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-400">Cluster customization - During cluster creation, you can specify additional settings and custom components that are installed on hello cluster nodes.</span></span>

3. <span data-ttu-id="86dca-401">샘플-인기 있는 사용자 지정 구성 요소, Microsoft 등에 대 한 예제는 hello HDInsight 클러스터에서 이러한 구성 요소를 사용할 수 있는 방법을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-401">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on hello HDInsight clusters.</span></span> <span data-ttu-id="86dca-402">이러한 샘플은 지원 없이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-402">These samples are provided without support.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="86dca-403">문제 해결</span><span class="sxs-lookup"><span data-stu-id="86dca-403">Troubleshooting</span></span>

<span data-ttu-id="86dca-404">스크립트 동작에 의해 기록 된 Ambari 웹 UI tooview 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-404">You can use Ambari web UI tooview information logged by script actions.</span></span> <span data-ttu-id="86dca-405">클러스터를 만드는 동안 실패 하면 hello 스크립트 hello 로그 hello 클러스터와 연결 된 hello 기본 저장소 계정에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-405">If hello script fails during cluster creation, hello logs are also available in hello default storage account associated with hello cluster.</span></span> <span data-ttu-id="86dca-406">이 섹션에서는 이러한 두 옵션을 사용 하 여 tooretrieve hello을 기록 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-406">This section provides information on how tooretrieve hello logs using both these options.</span></span>

### <a name="using-hello-ambari-web-ui"></a><span data-ttu-id="86dca-407">Hello Ambari 웹 UI를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="86dca-407">Using hello Ambari Web UI</span></span>

1. <span data-ttu-id="86dca-408">브라우저에서 toohttps://CLUSTERNAME.azurehdinsight.net 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-408">In your browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="86dca-409">CLUSTERNAME를 HDInsight 클러스터의 hello 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-409">Replace CLUSTERNAME with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="86dca-410">메시지가 표시 되 면 hello 클러스터에 대 한 hello 관리자 계정 이름 (admin) 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-410">When prompted, enter hello admin account name (admin) and password for hello cluster.</span></span> <span data-ttu-id="86dca-411">Web form의 tooreenter hello에 대 한 관리자 자격 증명을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-411">You may have tooreenter hello admin credentials in a web form.</span></span>

2. <span data-ttu-id="86dca-412">Hello hello 페이지 위쪽에 hello 모음에서 선택 hello **ops** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-412">From hello bar at hello top of hello page, select hello **ops** entry.</span></span> <span data-ttu-id="86dca-413">Ambari 통해 hello 클러스터에 대해 현재 및 이전 작업의 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-413">A list of current and previous operations performed on hello cluster through Ambari is displayed.</span></span>

    ![선택한 작업으로 Ambari 웹 UI 모음](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. <span data-ttu-id="86dca-415">포함 된 찾기 hello 항목 **실행\_customscriptaction** hello에 **작업** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-415">Find hello entries that have **run\_customscriptaction** in hello **Operations** column.</span></span> <span data-ttu-id="86dca-416">이러한 항목은 hello 스크립트 동작 실행 될 때 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-416">These entries are created when hello Script Actions run.</span></span>

    ![작업의 스크린샷](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    <span data-ttu-id="86dca-418">tooview hello STDOUT 및 STDERR 출력 hello run\customscriptaction 항목을 선택 하 고 hello 링크를 통해 드릴 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-418">tooview hello STDOUT and STDERR output, select hello run\customscriptaction entry and drill down through hello links.</span></span> <span data-ttu-id="86dca-419">Hello 스크립트를 실행 하는 경우이 출력이 생성 되 고 유용한 정보를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-419">This output is generated when hello script runs, and may contain useful information.</span></span>

### <a name="access-logs-from-hello-default-storage-account"></a><span data-ttu-id="86dca-420">Hello 기본 저장소 계정에서 액세스 로그</span><span class="sxs-lookup"><span data-stu-id="86dca-420">Access logs from hello default storage account</span></span>

<span data-ttu-id="86dca-421">Hello 클러스터 만들기 tooa 스크립트 작업 오류 때문에 실패 하면 hello 로그 hello 클러스터 저장소 계정에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-421">If hello cluster creation fails due tooa script action error, hello logs can be accessed from hello cluster storage account.</span></span>

* <span data-ttu-id="86dca-422">hello 저장소 로그에서 제공 됩니다 `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-422">hello storage logs are available at `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span></span>

    ![작업의 스크린샷](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    <span data-ttu-id="86dca-424">이 디렉터리 아래의 hello 로그 헤드 노드에, workernode, 및 사육 노드를 개별적으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-424">Under this directory, hello logs are organized separately for headnode, workernode, and zookeeper nodes.</span></span> <span data-ttu-id="86dca-425">일부 사례:</span><span class="sxs-lookup"><span data-stu-id="86dca-425">Some examples are:</span></span>

    * <span data-ttu-id="86dca-426">**헤드 노드** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="86dca-426">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="86dca-427">**작업자 노드** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="86dca-427">**Worker node** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="86dca-428">**Zookeeper 노드** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="86dca-428">**Zookeeper node** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span></span>

* <span data-ttu-id="86dca-429">모든 stdout 및 stderr hello 해당 호스트의 toohello 저장소 계정에 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-429">All stdout and stderr of hello corresponding host is uploaded toohello storage account.</span></span> <span data-ttu-id="86dca-430">각 스크립트 동작마다 하나의 **output-\*.txt** 및 **errors-\*.txt**가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-430">There is one **output-\*.txt** and **errors-\*.txt** for each script action.</span></span> <span data-ttu-id="86dca-431">hello 출력 *.txt 파일 내용이 hello 호스트에서 실행 하는 hello 스크립트의 hello URI에 대 한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-431">hello output-*.txt file contains information about hello URI of hello script that got run on hello host.</span></span> <span data-ttu-id="86dca-432">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-432">For example</span></span>

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* <span data-ttu-id="86dca-433">Hello로 스크립트 작업 클러스터를 만드는 반복 해 서 수 같은 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-433">It's possible that you repeatedly create a script action cluster with hello same name.</span></span> <span data-ttu-id="86dca-434">이러한 경우 hello 날짜 폴더 이름에 따라 hello 관련 로그를 구별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-434">In such case, you can distinguish hello relevant logs based on hello DATE folder name.</span></span> <span data-ttu-id="86dca-435">예를 들어 서로 다른 날짜에 만든 클러스터 (mycluster)에 대 한 폴더 구조 hello 로그 항목을 다음 유사한 toohello 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-435">For example, hello folder structure for a cluster (mycluster) created on different dates appears similar toohello following log entries:</span></span>

    <span data-ttu-id="86dca-436">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span><span class="sxs-lookup"><span data-stu-id="86dca-436">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span></span>

* <span data-ttu-id="86dca-437">Hello로 스크립트 작업 클러스터를 만드는 경우 이름과 같은 이름을 hello에 동일 날짜, hello 고유한 접두사 tooidentify hello 관련 로그 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-437">If you create a script action cluster with hello same name on hello same day, you can use hello unique prefix tooidentify hello relevant log files.</span></span>

* <span data-ttu-id="86dca-438">클러스터 근처 오전 12시 (자정)를 만들 경우 2 일 걸쳐 hello 로그 파일 수입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-438">If you create a cluster near 12:00AM (midnight), it's possible that hello log files span across two days.</span></span> <span data-ttu-id="86dca-439">이러한 경우에 hello에 대 한 두 개의 서로 다른 날짜 폴더 표시 동일한 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-439">In such cases, you see two different date folders for hello same cluster.</span></span>

* <span data-ttu-id="86dca-440">업로드 로그 파일 toohello 기본 컨테이너 큰 클러스터를 위해 특별히 too5 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-440">Uploading log files toohello default container can take up too5 mins, especially for large clusters.</span></span> <span data-ttu-id="86dca-441">따라서 tooaccess hello 로그 하려면 삭제 하면 안 즉시 hello 클러스터 경우 스크립트 작업이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-441">So, if you want tooaccess hello logs, you should not immediately delete hello cluster if a script action fails.</span></span>

### <a name="ambari-watchdog"></a><span data-ttu-id="86dca-442">Ambari 감시</span><span class="sxs-lookup"><span data-stu-id="86dca-442">Ambari watchdog</span></span>

> [!WARNING]
> <span data-ttu-id="86dca-443">Linux 기반 HDInsight 클러스터에 Ambari 감시 (hdinsightwatchdog) hello에 대 한 hello 암호를 변경 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="86dca-443">Do not change hello password for hello Ambari Watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="86dca-444">이 계정에 대 한 hello 암호를 변경할 hello HDInsight 클러스터에서 hello 기능 toorun 새 스크립트 동작을 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-444">Changing hello password for this account breaks hello ability toorun new script actions on hello HDInsight cluster.</span></span>

### <a name="cant-import-name-blobservice"></a><span data-ttu-id="86dca-445">이름 BlobService를 가져올 수 없음</span><span class="sxs-lookup"><span data-stu-id="86dca-445">Can't import name BlobService</span></span>

<span data-ttu-id="86dca-446">__증상__: hello 스크립트 동작이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-446">__Symptoms__: hello script action fails.</span></span> <span data-ttu-id="86dca-447">Ambari에서 hello 작업을 볼 때 텍스트 비슷한 toohello 다음 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-447">Text similar toohello following error is displayed when you view hello operation in Ambari:</span></span>

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

<span data-ttu-id="86dca-448">__원인__: hello HDInsight 클러스터에 포함 되어 있는 hello Python Azure 저장소 클라이언트를 업그레이드 하는 경우이 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-448">__Cause__: This error occurs if you upgrade hello Python Azure Storage client that is included with hello HDInsight cluster.</span></span> <span data-ttu-id="86dca-449">HDInsight는 Azure Storage 클라이언트 0.20.0을 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-449">HDInsight expects Azure Storage client 0.20.0.</span></span>

<span data-ttu-id="86dca-450">__해상도__: tooresolve이이 오류를 수동으로 사용 하 여 tooeach 클러스터 노드를 연결 `ssh` 명령 tooreinstall hello 올바른 저장소 클라이언트 버전에 따라 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="86dca-450">__Resolution__: tooresolve this error, manually connect tooeach cluster node using `ssh` and use hello following command tooreinstall hello correct storage client version:</span></span>

```
sudo pip install azure-storage==0.20.0
```

<span data-ttu-id="86dca-451">SSH 사용 하는 연결 toohello 클러스터에 대 한 자세한 내용은 참조 [SSH HDInsight를 사용](hdinsight-hadoop-linux-use-ssh-unix.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-451">For information on connecting toohello cluster with SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a><span data-ttu-id="86dca-452">클러스터를 만드는 동안 기록에 스크립트가 표시되지 않음</span><span class="sxs-lookup"><span data-stu-id="86dca-452">History doesn't show scripts used during cluster creation</span></span>

<span data-ttu-id="86dca-453">2016년 3월 15일 전에 클러스터를 만든 경우에는 스크립트 작업 기록에 항목이 나타나지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-453">If your cluster was created before March 15, 2016, you may not see an entry in Script Action history.</span></span> <span data-ttu-id="86dca-454">2016 년 3 월 15 일 후 hello 클러스터 크기를 조정 하면 클러스터를 만드는 동안 사용 하 여 hello 스크립트 기록에 표시 적용 되는 크기 조정 작업 hello의 일환으로 hello 클러스터의 toonew 노드.</span><span class="sxs-lookup"><span data-stu-id="86dca-454">If you resize hello cluster after March 15, 2016, hello scripts using during cluster creation appear in history as they are applied toonew nodes in hello cluster as part of hello resize operation.</span></span>

<span data-ttu-id="86dca-455">두 가지 예외 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-455">There are two exceptions:</span></span>

* <span data-ttu-id="86dca-456">클러스터가 2015년 9월 1일 전에 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-456">If your cluster was created before September 1, 2015.</span></span> <span data-ttu-id="86dca-457">스크립트 작업이 이 날에 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-457">This date is when Script Actions were introduced.</span></span> <span data-ttu-id="86dca-458">따라서 이 날짜 이전에 생성된 클러스터는 클러스터 생성에 스크립트 작업이 사용되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-458">Any cluster created before this date could not have used Script Actions for cluster creation.</span></span>

* <span data-ttu-id="86dca-459">클러스터를 만드는 동안 여러 스크립트 작업을 사용 하 고 동일한 여러 스크립트에 대 한 이름을 지정 하거나 hello hello를 사용 하는 경우 동일한 이름, 여러 스크립트에 대 한 서로 다른 매개 변수 이지만 동일한 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-459">If you used multiple Script Actions during cluster creation, and used hello same name for multiple scripts, or hello same name, same URI, but different parameters for multiple scripts.</span></span> <span data-ttu-id="86dca-460">이러한 경우 hello 다음 오류가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-460">In these cases, you receive hello following error:</span></span>

    <span data-ttu-id="86dca-461">기존 스크립트의 스크립트 이름 tooconflicting 인해이 클러스터에서 동작은 수 없는 새 스크립트를 실행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-461">No new script actions can be ran on this cluster due tooconflicting script names in existing scripts.</span></span> <span data-ttu-id="86dca-462">클러스터 만들기에 제공되는 스크립트 이름이 모두 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-462">Script names provided at cluster create must be all unique.</span></span> <span data-ttu-id="86dca-463">크기 조정에 기존 스크립트가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-463">Existing scripts are ran on resize.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86dca-464">다음 단계</span><span class="sxs-lookup"><span data-stu-id="86dca-464">Next steps</span></span>

* [<span data-ttu-id="86dca-465">HDInsight용 스크립트 작업 스크립트 개발</span><span class="sxs-lookup"><span data-stu-id="86dca-465">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions-linux.md)
* [<span data-ttu-id="86dca-466">HDInsight 클러스터에 Solr 설치 및 사용</span><span class="sxs-lookup"><span data-stu-id="86dca-466">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="86dca-467">HDInsight 클러스터에 Giraph 설치 및 사용</span><span class="sxs-lookup"><span data-stu-id="86dca-467">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="86dca-468">추가 저장소 tooan HDInsight 클러스터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="86dca-468">Add additional storage tooan HDInsight cluster</span></span>](hdinsight-hadoop-add-storage.md)

[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "클러스터를 만드는 동안의 단계"
