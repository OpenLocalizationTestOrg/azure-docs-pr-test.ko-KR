---
title: "Windows 기반 HDInsight에서 aaaMigrate tooLinux 기반 HDInsight-Azure | Microsoft Docs"
description: "Windows 기반 HDInsight에서 toomigrate tooa Linux 기반 HDInsight 클러스터를 클러스터 하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: ff35be59-bae3-42fd-9edc-77f0041bab93
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 7e5e536e8672d7e7c3086c6860cec062d05eda65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-a-windows-based-hdinsight-cluster-tooa-linux-based-cluster"></a><span data-ttu-id="9f737-103">Windows 기반 HDInsight 클러스터 tooa Linux 기반 클러스터에서 마이그레이션하십시오</span><span class="sxs-lookup"><span data-stu-id="9f737-103">Migrate from a Windows-based HDInsight cluster tooa Linux-based cluster</span></span>

<span data-ttu-id="9f737-104">Windows 및 Linux에서 HDInsight와 방법에 대 한 지침 hello 차이점에 자세히 설명 하는이 문서 toomigrate 기존 작업 tooa Linux 기반 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-104">This document provides details on hello differences between HDInsight on Windows and Linux, and guidance on how toomigrate existing workloads tooa Linux-based cluster.</span></span>

<span data-ttu-id="9f737-105">Windows 기반 HDInsight 쉽게 toouse hello 클라우드에서 Hadoop을 제공 하지만 toomigrate tooa Linux 기반 클러스터를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-105">While Windows-based HDInsight provides an easy way toouse Hadoop in hello cloud, you may need toomigrate tooa Linux-based cluster.</span></span> <span data-ttu-id="9f737-106">예를 들어 Linux 기반 도구와 기술 솔루션에 필요한 tootake 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-106">For example, tootake advantage of Linux-based tools and technologies that are required for your solution.</span></span> <span data-ttu-id="9f737-107">Hello Hadoop 에코 시스템의 다양 한 개체는 Linux 기반 시스템에서 개발 하며 Windows 기반 HDInsight 사용할 수 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-107">Many things in hello Hadoop ecosystem are developed on Linux-based systems, and may not be available for use with Windows-based HDInsight.</span></span> <span data-ttu-id="9f737-108">또한 많은 책, 동영상 및 기타 교육 자료에서 Hadoop 작업 시 Linux 시스템을 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-108">Additionally, many books, videos, and other training material assume that you are using a Linux system when working with Hadoop.</span></span>

> [!NOTE]
> <span data-ttu-id="9f737-109">HDInsight 클러스터는 hello 클러스터의 노드 hello에 대 한 hello 운영 체제와 Ubuntu 장기 지원 (LTS)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-109">HDInsight clusters use Ubuntu long-term support (LTS) as hello operating system for hello nodes in hello cluster.</span></span> <span data-ttu-id="9f737-110">다른 구성 요소 버전 관리 정보와 함께, HDInsight와 Ubuntu의 hello 버전에 대 한 정보를 참조 하십시오. [HDInsight 구성 요소 버전](hdinsight-component-versioning.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-110">For information on hello version of Ubuntu available with HDInsight, along with other component versioning information, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span>

## <a name="migration-tasks"></a><span data-ttu-id="9f737-111">마이그레이션 작업</span><span class="sxs-lookup"><span data-stu-id="9f737-111">Migration tasks</span></span>

<span data-ttu-id="9f737-112">hello 일반적인 마이그레이션 워크플로 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-112">hello general workflow for migration is as follows.</span></span>

![마이그레이션 워크플로 다이어그램](./media/hdinsight-migrate-from-windows-to-linux/workflow.png)

1. <span data-ttu-id="9f737-114">기존 워크플로, 작업, 등 tooa Linux 기반 클러스터를 마이그레이션할 때 필요할 수 있는 toounderstand 변경 내용을이 문서의 각 섹션을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-114">Read each section of this document toounderstand changes that may be required when migrating your existing workflow, jobs, etc. tooa Linux-based cluster.</span></span>

2. <span data-ttu-id="9f737-115">테스트/품질 보증 환경으로 Linux 기반 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-115">Create a Linux-based cluster as a test/quality assurance environment.</span></span> <span data-ttu-id="9f737-116">Linux 기반 클러스터를 만드는 방법에 대한 자세한 내용은 [HDInsight에서 Linux 기반 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f737-116">For more information on creating a Linux-based cluster, see [Create Linux-based clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

3. <span data-ttu-id="9f737-117">기존 작업, 데이터 원본 및 싱크 toohello 새 환경 복사본입니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-117">Copy existing jobs, data sources, and sinks toohello new environment.</span></span>

4. <span data-ttu-id="9f737-118">Toomake 작업 hello 새 클러스터에서 예상 대로 작동 하는지 테스트 하는 유효성 검사를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-118">Perform validation testing toomake sure that your jobs work as expected on hello new cluster.</span></span>

<span data-ttu-id="9f737-119">예상 대로 작동 하는 것을 확인 한 후 hello 마이그레이션에 대 한 가동 중지 시간을 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-119">Once you have verified that everything works as expected, schedule downtime for hello migration.</span></span> <span data-ttu-id="9f737-120">이 작동 중단이 시간 동안 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-120">During this downtime, perform hello following actions:</span></span>

1. <span data-ttu-id="9f737-121">Hello 클러스터 노드에서 로컬에 저장 된 임시 데이터를 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-121">Back up any transient data stored locally on hello cluster nodes.</span></span> <span data-ttu-id="9f737-122">예를 들어 헤드 노드에 직접 저장된 데이터가 있는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-122">For example, if you have data stored directly on a head node.</span></span>

2. <span data-ttu-id="9f737-123">Hello Windows 기반 클러스터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-123">Delete hello Windows-based cluster.</span></span>

3. <span data-ttu-id="9f737-124">동일한 기본 데이터 저장소에 사용 되는 Windows 기반 클러스터 hello hello를 사용 하 여 Linux 기반 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-124">Create a Linux-based cluster using hello same default data store that hello Windows-based cluster used.</span></span> <span data-ttu-id="9f737-125">hello Linux 기반 클러스터 기존 프로덕션 데이터에 대해 작업을 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-125">hello Linux-based cluster can continue working against your existing production data.</span></span>

4. <span data-ttu-id="9f737-126">백업한 모든 임시 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-126">Import any transient data you backed up.</span></span>

5. <span data-ttu-id="9f737-127">시작 작업/계속 hello 새 클러스터를 사용 하 여 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-127">Start jobs/continue processing using hello new cluster.</span></span>

### <a name="copy-data-toohello-test-environment"></a><span data-ttu-id="9f737-128">복사본 데이터 toohello 테스트 환경</span><span class="sxs-lookup"><span data-stu-id="9f737-128">Copy data toohello test environment</span></span>

<span data-ttu-id="9f737-129">하지만 많은 방법 toocopy hello 데이터 및 작업, 두 hello이이 섹션에서 설명 hello 가장 간단한 방법 toodirectly 이동 파일 tooa 클러스터 테스트.</span><span class="sxs-lookup"><span data-stu-id="9f737-129">There are many methods toocopy hello data and jobs, however hello two discussed in this section are hello simplest methods toodirectly move files tooa test cluster.</span></span>

#### <a name="hdfs-copy"></a><span data-ttu-id="9f737-130">HDFS 복사</span><span class="sxs-lookup"><span data-stu-id="9f737-130">HDFS copy</span></span>

<span data-ttu-id="9f737-131">Hello 단계 toocopy 데이터 hello 프로덕션 클러스터 toohello 테스트 클러스터에서 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-131">Use hello following steps toocopy data from hello production cluster toohello test cluster.</span></span> <span data-ttu-id="9f737-132">이 단계 사용 hello `hdfs dfs` HDInsight에 포함 된 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-132">These steps use hello `hdfs dfs` utility that is included with HDInsight.</span></span>

1. <span data-ttu-id="9f737-133">기존 클러스터에 대 한 hello 저장소 계정 및 기본 컨테이너 정보를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-133">Find hello storage account and default container information for your existing cluster.</span></span> <span data-ttu-id="9f737-134">다음 예제는 hello PowerShell tooretrieve이이 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-134">hello following example uses PowerShell tooretrieve this information:</span></span>

    ```powershell
    $clusterName="Your existing HDInsight cluster name"
    $clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    write-host "Storage account name: $clusterInfo.DefaultStorageAccount.split('.')[0]"
    write-host "Default container: $clusterInfo.DefaultStorageContainer"
    ```

2. <span data-ttu-id="9f737-135">테스트 환경 toocreate HDInsight 문서에서 만드는 Linux 기반 클러스터 hello hello 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-135">toocreate a test environment, follow hello steps in hello Create Linux-based clusters in HDInsight document.</span></span> <span data-ttu-id="9f737-136">Hello 클러스터를 만들기 전에 중지 하 고 대신 선택 **선택적 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-136">Stop before creating hello cluster, and instead select **Optional Configuration**.</span></span>

3. <span data-ttu-id="9f737-137">Hello 선택적 구성 블레이드에서 선택 **연결 된 저장소 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-137">From hello Optional Configuration blade, select **Linked Storage Accounts**.</span></span>

4. <span data-ttu-id="9f737-138">선택 **저장소 키를 추가**, 메시지가 표시 되 면 hello 1 단계에서 PowerShell 스크립트에서 반환 된 hello 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-138">Select **Add a storage key**, and when prompted, select hello storage account that was returned by hello PowerShell script in step 1.</span></span> <span data-ttu-id="9f737-139">각 블레이드에서 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-139">Click **Select** on each blade.</span></span> <span data-ttu-id="9f737-140">마지막으로 hello 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-140">Finally, create hello cluster.</span></span>

5. <span data-ttu-id="9f737-141">Hello 클러스터를 만든 후 다음을 사용 하 여 tooit 연결 **SSH 합니다.**</span><span class="sxs-lookup"><span data-stu-id="9f737-141">Once hello cluster has been created, connect tooit using **SSH.**</span></span> <span data-ttu-id="9f737-142">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f737-142">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

6. <span data-ttu-id="9f737-143">Hello SSH 세션에서 연결 된 hello 저장소 계정 toohello 새 기본 저장소 계정에서 다음 명령을 toocopy 파일이 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-143">From hello SSH session, use hello following command toocopy files from hello linked storage account toohello new default storage account.</span></span> <span data-ttu-id="9f737-144">컨테이너 PowerShell에서 반환 된 hello 컨테이너 정보로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-144">Replace CONTAINER with hello container information returned by PowerShell.</span></span> <span data-ttu-id="9f737-145">대체 __계정__ hello 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-145">Replace __ACCOUNT__ with hello account name.</span></span> <span data-ttu-id="9f737-146">Hello 경로 toodata를 hello 경로 tooa 데이터 파일로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-146">Replace hello path toodata with hello path tooa data file.</span></span>

    ```bash
    hdfs dfs -cp wasb://CONTAINER@ACCOUNT.blob.core.windows.net/path/to/old/data /path/to/new/location
    ```

    > [!NOTE]
    > <span data-ttu-id="9f737-147">Hello 데이터를 포함 하는 hello 디렉터리 구조 hello 테스트 환경에 없는 경우 다음 명령을 hello를 사용 하 여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-147">If hello directory structure that contains hello data does not exist on hello test environment, you can create it using hello following command:</span></span>

    ```bash
    hdfs dfs -mkdir -p /new/path/to/create
    ```

    <span data-ttu-id="9f737-148">hello `-p` 스위치 hello hello 경로에 모든 디렉터리를 만들 수 있음.</span><span class="sxs-lookup"><span data-stu-id="9f737-148">hello `-p` switch enables hello creation of all directories in  hello path.</span></span>

#### <a name="direct-copy-between-blobs-in-azure-storage"></a><span data-ttu-id="9f737-149">Azure Storage Blob 간 직접 복사</span><span class="sxs-lookup"><span data-stu-id="9f737-149">Direct copy between blobs in Azure Storage</span></span>

<span data-ttu-id="9f737-150">또는 toouse hello 경우가 `Start-AzureStorageBlobCopy` HDInsight 외부 저장소 계정 간에 Azure PowerShell cmdlet toocopy blob입니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-150">Alternatively, you may want toouse hello `Start-AzureStorageBlobCopy` Azure PowerShell cmdlet toocopy blobs between storage accounts outside of HDInsight.</span></span> <span data-ttu-id="9f737-151">자세한 내용은 참조 hello 어떻게 toomanage의 Azure 저장소와 Azure PowerShell을 사용 하 여 Azure Blob 섹션.</span><span class="sxs-lookup"><span data-stu-id="9f737-151">For more information, see hello How toomanage Azure Blobs section of Using Azure PowerShell with Azure Storage.</span></span>

## <a name="client-side-technologies"></a><span data-ttu-id="9f737-152">클라이언트 쪽 기술</span><span class="sxs-lookup"><span data-stu-id="9f737-152">Client-side technologies</span></span>

<span data-ttu-id="9f737-153">와 같은 클라이언트 쪽 기술과 [Azure PowerShell cmdlet](/powershell/azureps-cmdlets-docs), [Azure CLI](../cli-install-nodejs.md), 또는 hello [Hadoop에 대 한.NET SDK](https://hadoopsdk.codeplex.com/) toowork Linux 기반 클러스터를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-153">Client-side technologies such as [Azure PowerShell cmdlets](/powershell/azureps-cmdlets-docs), [Azure CLI](../cli-install-nodejs.md), or hello [.NET SDK for Hadoop](https://hadoopsdk.codeplex.com/) continue toowork Linux-based clusters.</span></span> <span data-ttu-id="9f737-154">이러한 기술을 REST 클러스터 운영 체제 유형에 모두에서 동일 hello는 Api에 의존 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-154">These technologies rely on REST APIs that are hello same across both cluster OS types.</span></span>

## <a name="server-side-technologies"></a><span data-ttu-id="9f737-155">서버 쪽 기술</span><span class="sxs-lookup"><span data-stu-id="9f737-155">Server-side technologies</span></span>

<span data-ttu-id="9f737-156">다음 표에서 hello 마이그레이션 서버 쪽 구성 요소에 Windows 관련 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-156">hello following table provides guidance on migrating server-side components that are Windows-specific.</span></span>

| <span data-ttu-id="9f737-157">사용 기술</span><span class="sxs-lookup"><span data-stu-id="9f737-157">If you are using this technology...</span></span> | <span data-ttu-id="9f737-158">수행 작업</span><span class="sxs-lookup"><span data-stu-id="9f737-158">Take this action...</span></span> |
| --- | --- |
| <span data-ttu-id="9f737-159">**PowerShell** (서버 쪽 스크립트, 클러스터 생성 중 사용한 스크립트 동작 포함)</span><span class="sxs-lookup"><span data-stu-id="9f737-159">**PowerShell** (server-side scripts, including Script Actions used during cluster creation)</span></span> |<span data-ttu-id="9f737-160">Bash 스크립트로 다시 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-160">Rewrite as Bash scripts.</span></span> <span data-ttu-id="9f737-161">스크립트 동작의 경우 [스크립트 동작에서 Linux 기반 HDInsight 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md) 및 [Linux 기반 HDInsight에 대한 스크립트 동작 개발](hdinsight-hadoop-script-actions-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f737-161">For Script Actions, see [Customize Linux-based HDInsight with Script Actions](hdinsight-hadoop-customize-cluster-linux.md) and [Script action development for Linux-based HDInsight](hdinsight-hadoop-script-actions-linux.md).</span></span> |
| <span data-ttu-id="9f737-162">**Azure CLI** (서버 쪽 스크립트)</span><span class="sxs-lookup"><span data-stu-id="9f737-162">**Azure CLI** (server-side scripts)</span></span> |<span data-ttu-id="9f737-163">Hello Azure CLI Linux에서 사용할 수 있는 동안 오지 않는 사전 설치 된 hello HDInsight 클러스터 헤드 노드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-163">While hello Azure CLI is available on Linux, it does not come pre-installed on hello HDInsight cluster head nodes.</span></span> <span data-ttu-id="9f737-164">Hello Azure CLI를 설치 하는 방법에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 2.0 시작](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-164">For more information on installing hello Azure CLI, see [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span> |
| <span data-ttu-id="9f737-165">**.NET 구성 요소**</span><span class="sxs-lookup"><span data-stu-id="9f737-165">**.NET components**</span></span> |<span data-ttu-id="9f737-166">.NET은 Linux 기반 HDInsight 클러스터에서 [Mono](https://mono-project.com)를 통해 완전히 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-166">.NET is supported on Linux-based HDInsight through [Mono](https://mono-project.com).</span></span> <span data-ttu-id="9f737-167">자세한 내용은 참조 [마이그레이션할.NET 솔루션 tooLinux 기반 HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-167">For more information, see [Migrate .NET solutions tooLinux-based HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md).</span></span> |
| <span data-ttu-id="9f737-168">**Win32 구성 요소 또는 기타 Windows 전용 기술**</span><span class="sxs-lookup"><span data-stu-id="9f737-168">**Win32 components or other Windows-only technology**</span></span> |<span data-ttu-id="9f737-169">지침은 hello 구성 요소 또는 기술에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-169">Guidance depends on hello component or technology.</span></span> <span data-ttu-id="9f737-170">수 toofind Linux와 호환 되는 버전 하거나 대체 솔루션 toofind 필요 하거나이 구성 요소를 다시 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-170">You may be able toofind a version that is compatible with Linux, or you may need toofind an alternate solution or rewrite this component.</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="9f737-171">hello HDInsight 관리 SDK 모노와 완벽 하 게 호환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-171">hello HDInsight management SDK is not fully compatible with Mono.</span></span> <span data-ttu-id="9f737-172">솔루션의 일부분 지금은 toohello HDInsight 클러스터를 배포 하지 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-172">It should not be used as part of solutions deployed toohello HDInsight cluster at this time.</span></span>

## <a name="cluster-creation"></a><span data-ttu-id="9f737-173">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="9f737-173">Cluster creation</span></span>

<span data-ttu-id="9f737-174">이 섹션에서는 클러스터 만들기의 차이에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-174">This section provides information on differences in cluster creation.</span></span>

### <a name="ssh-user"></a><span data-ttu-id="9f737-175">SSH 사용자</span><span class="sxs-lookup"><span data-stu-id="9f737-175">SSH User</span></span>

<span data-ttu-id="9f737-176">Linux 기반 HDInsight 클러스터 hello를 사용 하 여 **SSH (보안 셸)** tooprovide 원격 액세스 toohello 클러스터 노드 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-176">Linux-based HDInsight clusters use hello **Secure Shell (SSH)** protocol tooprovide remote access toohello cluster nodes.</span></span> <span data-ttu-id="9f737-177">Window 기반 클러스터용 원격 데스크톱과 달리, 대부분의 SSH 클라이언트는 그래픽 사용자 경험을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-177">Unlike Remote Desktop for Windows-based clusters, most SSH clients do not provide a graphical user experience.</span></span> <span data-ttu-id="9f737-178">대신, SSH 클라이언트 hello 클러스터에서 toorun 명령을 허용 하는 명령줄을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-178">Instead, SSH clients provide a command line that allows you toorun commands on hello cluster.</span></span> <span data-ttu-id="9f737-179">일부 클라이언트 (예: [MobaXterm](http://mobaxterm.mobatek.net/)) 더하기 tooa 원격 명령줄에서 그래픽 파일 시스템 브라우저를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-179">Some clients (such as [MobaXterm](http://mobaxterm.mobatek.net/)) provide a graphical file system browser in addition tooa remote command line.</span></span>

<span data-ttu-id="9f737-180">클러스터를 생성하는 동안 인증을 위해 SSH 사용자와 더불어 **암호** 또는 **공개 키 인증서** 중 하나를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-180">During cluster creation, you must provide an SSH user and either a **password** or **public key certificate** for authentication.</span></span>

<span data-ttu-id="9f737-181">암호보다는 공개 키 인증서가 더 안전하므로 공개 키 인증서를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-181">We recommend using Public key certificate, as it is more secure than using a password.</span></span> <span data-ttu-id="9f737-182">인증서 인증 서명 된 공개/개인 키 쌍을 생성 한 다음 hello 클러스터를 만들 때 hello 공개 키를 제공 하 여 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-182">Certificate authentication works by generating a signed public/private key pair, then providing hello public key when creating hello cluster.</span></span> <span data-ttu-id="9f737-183">SSH를 사용 하 여 toohello 서버에 연결할 때 클라이언트 hello에 개인 키 hello hello 연결에 대 한 인증을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-183">When connecting toohello server using SSH, hello private key on hello client provides authentication for hello connection.</span></span>

<span data-ttu-id="9f737-184">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f737-184">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

### <a name="cluster-customization"></a><span data-ttu-id="9f737-185">클러스터 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="9f737-185">Cluster customization</span></span>

<span data-ttu-id="9f737-186">**스크립트 동작** 은 Bash 스크립트에서 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-186">**Script Actions** used with Linux-based clusters must be written in Bash script.</span></span> <span data-ttu-id="9f737-187">스크립트 동작 실행 되 고 Linux 기반 클러스터를 클러스터 된 후 tooperform 사용 되는 사용자 지정 있을 수도 있습니다에 대 한 클러스터를 만드는 동안 사용할 수 있지만 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-187">While Script Actions can be used during cluster creation, for Linux-based clusters they can also be used tooperform customization after a cluster is up and running.</span></span> <span data-ttu-id="9f737-188">자세한 내용은 [스크립트 동작에서 Linux 기반 HDInsight 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md) 및 [Linux 기반 HDInsight에 대한 스크립트 동작 개발](hdinsight-hadoop-script-actions-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f737-188">For more information, see [Customize Linux-based HDInsight with Script Actions](hdinsight-hadoop-customize-cluster-linux.md) and [Script action development for Linux-based HDInsight](hdinsight-hadoop-script-actions-linux.md).</span></span>

<span data-ttu-id="9f737-189">다른 사용자 지정 기능은 **부트스트랩**입니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-189">Another customization feature is **bootstrap**.</span></span> <span data-ttu-id="9f737-190">Windows 클러스터의 경우이 기능은 하이브와 함께 사용할 추가 라이브러리의 toospecify hello 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-190">For Windows clusters, this feature allows you toospecify hello location of additional libraries for use with Hive.</span></span> <span data-ttu-id="9f737-191">클러스터를 만든 후 이러한 라이브러리는 자동으로 함께 사용할 수 있는 hello 필요 toouse 없이 하이브 쿼리 `ADD JAR`합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-191">After cluster creation, these libraries are automatically available for use with Hive queries without hello need toouse `ADD JAR`.</span></span>

<span data-ttu-id="9f737-192">Linux 기반 클러스터용 hello 부트스트랩 기능과이 기능을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-192">hello Bootstrap feature for Linux-based clusters does not provide this functionality.</span></span> <span data-ttu-id="9f737-193">대신 [클러스터 생성 중 Hive 라이브러리 추가](hdinsight-hadoop-add-hive-libraries.md)에 설명된 스크립트 동작을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-193">Instead, use script action documented in [Add Hive libraries during cluster creation](hdinsight-hadoop-add-hive-libraries.md).</span></span>

### <a name="virtual-networks"></a><span data-ttu-id="9f737-194">가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="9f737-194">Virtual Networks</span></span>

<span data-ttu-id="9f737-195">Windows 기반 HDInsight 클러스터는 클래식 가상 네트워크에서만 작동하는 반면 Linux 기반 HDInsight 클러스터는 리소스 관리자 가상 네트워크가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-195">Windows-based HDInsight clusters only work with Classic Virtual Networks, while Linux-based HDInsight clusters require Resource Manager Virtual Networks.</span></span> <span data-ttu-id="9f737-196">Hello Linux HDInsight 클러스터는 클래식 가상 네트워크에 연결 해야, 참조 리소스가 있는 경우 [클래식 가상 네트워크 tooa 리소스 관리자 가상 네트워크 연결](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-196">If you have resources in a Classic Virtual Network that hello Linux-HDInsight cluster must connect to, see [Connecting a Classic Virtual Network tooa Resource Manager Virtual Network](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span></span>

<span data-ttu-id="9f737-197">HDInsight에서 Azure 가상 네트워크를 사용하기 위한 구성 요구 사항에 대한 자세한 내용은 [가상 네트워크를 사용하여 HDInsight 기능 확장](hdinsight-extend-hadoop-virtual-network.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f737-197">For more information on configuration requirements for using Azure Virtual Networks with HDInsight, see [Extend HDInsight capabilities by using a Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span></span>

## <a name="management-and-monitoring"></a><span data-ttu-id="9f737-198">관리 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="9f737-198">Management and monitoring</span></span>

<span data-ttu-id="9f737-199">Ambari를 통해 사용할 수는 많이 한 hello 웹 Ui 작업 기록 또는 Yarn UI와 같은 Windows 기반 HDInsight에 사용한 경우일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-199">Many of hello web UIs you may have used with Windows-based HDInsight, such as Job History or Yarn UI, are available through Ambari.</span></span> <span data-ttu-id="9f737-200">또한 hello Ambari 하이브 보기 웹 브라우저를 사용 하 여 하이브 쿼리 방법을 toorun를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-200">In addition, hello Ambari Hive View provides a way toorun Hive queries using your web browser.</span></span> <span data-ttu-id="9f737-201">hello Ambari 웹 UI에서 https://CLUSTERNAME.azurehdinsight.net Linux 기반 클러스터에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-201">hello Ambari Web UI is available on Linux-based clusters at https://CLUSTERNAME.azurehdinsight.net.</span></span>

<span data-ttu-id="9f737-202">Ambari 사용한 작업에 대 한 자세한 내용은 다음 문서는 hello를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="9f737-202">For more information on working with Ambari, see hello following documents:</span></span>

* [<span data-ttu-id="9f737-203">Ambari 웹</span><span class="sxs-lookup"><span data-stu-id="9f737-203">Ambari Web</span></span>](hdinsight-hadoop-manage-ambari.md)
* [<span data-ttu-id="9f737-204">Ambari REST API</span><span class="sxs-lookup"><span data-stu-id="9f737-204">Ambari REST API</span></span>](hdinsight-hadoop-manage-ambari-rest-api.md)

### <a name="ambari-alerts"></a><span data-ttu-id="9f737-205">Ambari 경고</span><span class="sxs-lookup"><span data-stu-id="9f737-205">Ambari Alerts</span></span>

<span data-ttu-id="9f737-206">Ambari의 hello 클러스터에 문제가 발생할 가능성을 확인할 수 있는 경고는 시스템을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-206">Ambari has an alert system that can tell you of potential problems with hello cluster.</span></span> <span data-ttu-id="9f737-207">하지만 경고는 hello REST API를 통해 검색할 수 있습니다 hello Ambari 웹 UI에서에서 빨간색 또는 노란색 항목으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-207">Alerts appear as red or yellow entries in hello Ambari Web UI, however you can also retrieve them through hello REST API.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9f737-208">Ambari 경고는 문제가 *있을 수 있다*라는 의미이며, 문제가 *있다*는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-208">Ambari alerts indicate that there *may* be a problem, not that there *is* a problem.</span></span> <span data-ttu-id="9f737-209">예를 들어 평소처럼 액세스할 수 있는데도 HiveServer2에 액세스할 수 없다는 경고가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-209">For example, you may receive an alert that HiveServer2 cannot be accessed, even though you can access it normally.</span></span>
>
> <span data-ttu-id="9f737-210">많은 경고는 서비스에서 간격 기반 쿼리로 구현되므로 특정 시간 프레임 내에서 응답을 기대합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-210">Many alerts are implemented as interval-based queries against a service, and expect a response within a specific time frame.</span></span> <span data-ttu-id="9f737-211">따라서 hello 경고 반드시 의미 hello 서비스가 중지 되었습니다, 그리고 just hello 예상 된 시간 안에 결과 반환 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-211">So hello alert doesn't necessarily mean that hello service is down, just that it didn't return results within hello expected time frame.</span></span>

<span data-ttu-id="9f737-212">사용자는 조치를 취하기 전에 경고가 오랜 시간 동안 발생했는지 또는 이전에 보고되었던 사용자 문제를 반영하는지 여부를 평가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-212">You should evaluate whether an alert has been occurring for an extended period, or mirrors user problems that have been reported before taking action on it.</span></span>

## <a name="file-system-locations"></a><span data-ttu-id="9f737-213">파일 시스템 위치</span><span class="sxs-lookup"><span data-stu-id="9f737-213">File system locations</span></span>

<span data-ttu-id="9f737-214">Linux 클러스터 파일 시스템 hello Windows 기반 HDInsight 클러스터와는 다르게 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-214">hello Linux cluster file system is laid out differently than Windows-based HDInsight clusters.</span></span> <span data-ttu-id="9f737-215">다음 테이블 toofind 일반적으로 사용 되는 파일이 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-215">Use hello following table toofind commonly used files.</span></span>

| <span data-ttu-id="9f737-216">Toofind... 필요</span><span class="sxs-lookup"><span data-stu-id="9f737-216">I need toofind...</span></span> | <span data-ttu-id="9f737-217">위치</span><span class="sxs-lookup"><span data-stu-id="9f737-217">It is located...</span></span> |
| --- | --- |
| <span data-ttu-id="9f737-218">구성</span><span class="sxs-lookup"><span data-stu-id="9f737-218">Configuration</span></span> |<span data-ttu-id="9f737-219">`/etc`.</span><span class="sxs-lookup"><span data-stu-id="9f737-219">`/etc`.</span></span> <span data-ttu-id="9f737-220">예: `/etc/hadoop/conf/core-site.xml`</span><span class="sxs-lookup"><span data-stu-id="9f737-220">For example, `/etc/hadoop/conf/core-site.xml`</span></span> |
| <span data-ttu-id="9f737-221">로그 파일</span><span class="sxs-lookup"><span data-stu-id="9f737-221">Log files</span></span> |`/var/logs` |
| <span data-ttu-id="9f737-222">HDP(Hortonworks Data Platform)</span><span class="sxs-lookup"><span data-stu-id="9f737-222">Hortonworks Data Platform (HDP)</span></span> |<span data-ttu-id="9f737-223">`/usr/hdp`. 두 디렉터리 여기에 있는, 하나는 현재 HDP 버전 hello 및 `current`합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-223">`/usr/hdp`.There are two directories located here, one that is hello current HDP version and `current`.</span></span> <span data-ttu-id="9f737-224">hello `current` 디렉터리 기호화 된 링크 toofiles 및 hello 버전 번호 디렉터리에 디렉터리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-224">hello `current` directory contains symbolic links toofiles and directories located in hello version number directory.</span></span> <span data-ttu-id="9f737-225">hello `current` 디렉터리는 버전은 업데이트 hello 버전 번호 변경 HDP hello 대로 이후 HDP 파일에 액세스 하는 편리한 방법으로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-225">hello `current` directory is provided as a convenient way of accessing HDP files since hello version number changes as hello HDP version is updated.</span></span> |
| <span data-ttu-id="9f737-226">hadoop-streaming.jar</span><span class="sxs-lookup"><span data-stu-id="9f737-226">hadoop-streaming.jar</span></span> |`/usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar` |

<span data-ttu-id="9f737-227">일반적으로 hello 파일의 hello 이름을 알고 있는 경우에 hello SSH 세션 toofind hello 파일 경로에서 다음 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-227">In general, if you know hello name of hello file, you can use hello following command from an SSH session toofind hello file path:</span></span>

    find / -name FILENAME 2>/dev/null

<span data-ttu-id="9f737-228">또한 hello 파일 이름에 와일드 카드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-228">You can also use wildcards with hello file name.</span></span> <span data-ttu-id="9f737-229">예를 들어 `find / -name *streaming*.jar 2>/dev/null` hello 경로 tooany '스트리밍' hello 파일 이름의 일부로 hello 단어를 포함 하는 jar 파일을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-229">For example, `find / -name *streaming*.jar 2>/dev/null` returns hello path tooany jar files that contain hello word 'streaming' as part of hello file name.</span></span>

## <a name="hive-pig-and-mapreduce"></a><span data-ttu-id="9f737-230">Hive, Pig 및 MapReduce</span><span class="sxs-lookup"><span data-stu-id="9f737-230">Hive, Pig, and MapReduce</span></span>

<span data-ttu-id="9f737-231">Pig 및 MapReduce 워크로드는 Linux 기반 클러스터에서 매우 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-231">Pig and MapReduce workloads are similar on Linux-based clusters.</span></span> <span data-ttu-id="9f737-232">하지만 Linux 기반 HDInsight 클러스터는 Hadoop, Hive, Pig의 최신 버전을 사용하여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-232">However, Linux-based HDInsight clusters can be created using newer versions of Hadoop, Hive, and Pig.</span></span> <span data-ttu-id="9f737-233">이러한 버전 차이로 인해 기존 솔루션이 작동하는 방식이 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-233">These version differences may introduce changes in how your existing solutions function.</span></span> <span data-ttu-id="9f737-234">Hello 버전의 HDInsight에 포함 된 구성 요소에 대 한 자세한 내용은 참조 하십시오. [HDInsight 구성 요소 버전 관리](hdinsight-component-versioning.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-234">For more information on hello versions of components included with HDInsight, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="9f737-235">Linux 기반 HDInsight는 원격 데스크톱 기능을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-235">Linux-based HDInsight does not provide remote desktop functionality.</span></span> <span data-ttu-id="9f737-236">대신, SSH를 사용할 수 있습니다 tooremotely toohello 클러스터 헤드 노드를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-236">Instead, you can use SSH tooremotely connect toohello cluster head nodes.</span></span> <span data-ttu-id="9f737-237">자세한 내용은 다음 문서는 hello를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="9f737-237">For more information, see hello following documents:</span></span>

* [<span data-ttu-id="9f737-238">SSH와 함께 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="9f737-238">Use Hive with SSH</span></span>](hdinsight-hadoop-use-hive-ssh.md)
* [<span data-ttu-id="9f737-239">SSH와 함께 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="9f737-239">Use Pig with SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md)
* [<span data-ttu-id="9f737-240">SSH와 함께 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="9f737-240">Use MapReduce with SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md)

### <a name="hive"></a><span data-ttu-id="9f737-241">Hive</span><span class="sxs-lookup"><span data-stu-id="9f737-241">Hive</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9f737-242">외부 하이브 metastore를 사용 하는 경우 Linux 기반 HDInsight와 사용 하기 전에 hello metastore를 백업 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-242">If you use an external Hive metastore, you should back up hello metastore before using it with Linux-based HDInsight.</span></span> <span data-ttu-id="9f737-243">Linux 기반 HDInsight는 최신 버전의 Hive에서 사용할 수 있으며, 이 경우 이전 버전에서 만든 메타스토어와 호환되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-243">Linux-based HDInsight is available with newer versions of Hive, which may have incompatibilities with metastores created by earlier versions.</span></span>

<span data-ttu-id="9f737-244">다음 차트 hello 하이브 작업 마이그레이션하는 방법에 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-244">hello following chart provides guidance on migrating your Hive workloads.</span></span>

| <span data-ttu-id="9f737-245">Windows 기반</span><span class="sxs-lookup"><span data-stu-id="9f737-245">On Windows-based, I use...</span></span> | <span data-ttu-id="9f737-246">Linux 기반에서...</span><span class="sxs-lookup"><span data-stu-id="9f737-246">On Linux-based...</span></span> |
| --- | --- |
| <span data-ttu-id="9f737-247">**Hive 편집기**</span><span class="sxs-lookup"><span data-stu-id="9f737-247">**Hive Editor**</span></span> |[<span data-ttu-id="9f737-248">Ambari에서 Hive 보기</span><span class="sxs-lookup"><span data-stu-id="9f737-248">Hive View in Ambari</span></span>](hdinsight-hadoop-use-hive-ambari-view.md) |
| <span data-ttu-id="9f737-249">`set hive.execution.engine=tez;`tooenable Tez</span><span class="sxs-lookup"><span data-stu-id="9f737-249">`set hive.execution.engine=tez;` tooenable Tez</span></span> |<span data-ttu-id="9f737-250">Tez는 Linux 기반 클러스터용 hello 기본 실행 엔진, hello에 실행할 문을 설정 되므로 더 이상 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-250">Tez is hello default execution engine for Linux-based clusters, so hello set statement is no longer needed.</span></span> |
| <span data-ttu-id="9f737-251">C# 사용자 정의 함수</span><span class="sxs-lookup"><span data-stu-id="9f737-251">C# user-defined functions</span></span> | <span data-ttu-id="9f737-252">Linux 기반 HDInsight와 C# 구성 요소 유효성 검사에 대 한 자세한 내용은 참조 하세요. [마이그레이션할.NET 솔루션 HDInsight tooLinux 기반](hdinsight-hadoop-migrate-dotnet-to-linux.md)</span><span class="sxs-lookup"><span data-stu-id="9f737-252">For information on validating C# components with Linux-based HDInsight, see [Migrate .NET solutions tooLinux-based HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)</span></span> |
| <span data-ttu-id="9f737-253">CMD 파일 서버에서 나 스크립트 hello 하이브 작업의 일부로 실행</span><span class="sxs-lookup"><span data-stu-id="9f737-253">CMD files or scripts on hello server invoked as part of a Hive job</span></span> |<span data-ttu-id="9f737-254">Bash 스크립트 사용</span><span class="sxs-lookup"><span data-stu-id="9f737-254">use Bash scripts</span></span> |
| <span data-ttu-id="9f737-255">`hive` 명령</span><span class="sxs-lookup"><span data-stu-id="9f737-255">`hive` command from remote desktop</span></span> |<span data-ttu-id="9f737-256">[SSH 세션에서 Hive](hdinsight-hadoop-use-hive-ssh.md) 또는 [Beeline](hdinsight-hadoop-use-hive-beeline.md) 사용</span><span class="sxs-lookup"><span data-stu-id="9f737-256">Use [Beeline](hdinsight-hadoop-use-hive-beeline.md) or [Hive from an SSH session](hdinsight-hadoop-use-hive-ssh.md)</span></span> |

### <a name="pig"></a><span data-ttu-id="9f737-257">Pig</span><span class="sxs-lookup"><span data-stu-id="9f737-257">Pig</span></span>

| <span data-ttu-id="9f737-258">Windows 기반</span><span class="sxs-lookup"><span data-stu-id="9f737-258">On Windows-based, I use...</span></span> | <span data-ttu-id="9f737-259">Linux 기반에서...</span><span class="sxs-lookup"><span data-stu-id="9f737-259">On Linux-based...</span></span> |
| --- | --- |
| <span data-ttu-id="9f737-260">C# 사용자 정의 함수</span><span class="sxs-lookup"><span data-stu-id="9f737-260">C# user-defined functions</span></span> | <span data-ttu-id="9f737-261">Linux 기반 HDInsight와 C# 구성 요소 유효성 검사에 대 한 자세한 내용은 참조 하세요. [마이그레이션할.NET 솔루션 HDInsight tooLinux 기반](hdinsight-hadoop-migrate-dotnet-to-linux.md)</span><span class="sxs-lookup"><span data-stu-id="9f737-261">For information on validating C# components with Linux-based HDInsight, see [Migrate .NET solutions tooLinux-based HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)</span></span> |
| <span data-ttu-id="9f737-262">CMD 파일 서버에서 나 스크립트 hello Pig 작업의 일부로 실행</span><span class="sxs-lookup"><span data-stu-id="9f737-262">CMD files or scripts on hello server invoked as part of a Pig job</span></span> |<span data-ttu-id="9f737-263">Bash 스크립트 사용</span><span class="sxs-lookup"><span data-stu-id="9f737-263">use Bash scripts</span></span> |

### <a name="mapreduce"></a><span data-ttu-id="9f737-264">MapReduce</span><span class="sxs-lookup"><span data-stu-id="9f737-264">MapReduce</span></span>

| <span data-ttu-id="9f737-265">Windows 기반</span><span class="sxs-lookup"><span data-stu-id="9f737-265">On Windows-based, I use...</span></span> | <span data-ttu-id="9f737-266">Linux 기반에서...</span><span class="sxs-lookup"><span data-stu-id="9f737-266">On Linux-based...</span></span> |
| --- | --- |
| <span data-ttu-id="9f737-267">C# 매퍼 및 리듀서 구성 요소</span><span class="sxs-lookup"><span data-stu-id="9f737-267">C# mapper and reducer components</span></span> | <span data-ttu-id="9f737-268">Linux 기반 HDInsight와 C# 구성 요소 유효성 검사에 대 한 자세한 내용은 참조 하세요. [마이그레이션할.NET 솔루션 HDInsight tooLinux 기반](hdinsight-hadoop-migrate-dotnet-to-linux.md)</span><span class="sxs-lookup"><span data-stu-id="9f737-268">For information on validating C# components with Linux-based HDInsight, see [Migrate .NET solutions tooLinux-based HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)</span></span> |
| <span data-ttu-id="9f737-269">CMD 파일 서버에서 나 스크립트 hello 하이브 작업의 일부로 실행</span><span class="sxs-lookup"><span data-stu-id="9f737-269">CMD files or scripts on hello server invoked as part of a Hive job</span></span> |<span data-ttu-id="9f737-270">Bash 스크립트 사용</span><span class="sxs-lookup"><span data-stu-id="9f737-270">use Bash scripts</span></span> |

## <a name="oozie"></a><span data-ttu-id="9f737-271">Oozie</span><span class="sxs-lookup"><span data-stu-id="9f737-271">Oozie</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9f737-272">외부 Oozie metastore를 사용 하는 경우 Linux 기반 HDInsight와 사용 하기 전에 hello metastore를 백업 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-272">If you use an external Oozie metastore, you should back up hello metastore before using it with Linux-based HDInsight.</span></span> <span data-ttu-id="9f737-273">Linux 기반 HDInsight는 최신 버전의 Oozie에서 사용할 수 있으며, 이 경우 이전 버전에서 만든 메타스토어와 호환되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-273">Linux-based HDInsight is available with newer versions of Oozie, which may have incompatibilities with metastores created by earlier versions.</span></span>

<span data-ttu-id="9f737-274">Oozie 워크플로에서는 셸 작업이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-274">Oozie workflows allow shell actions.</span></span> <span data-ttu-id="9f737-275">셸 작업 hello 운영 체제 toorun 명령줄 명령에 대 한 hello 기본 셸을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-275">Shell actions use hello default shell for hello operating system toorun command-line commands.</span></span> <span data-ttu-id="9f737-276">Windows 셸 hello를 사용 하는 Oozie 워크플로 설정한 경우 hello 워크플로 toorely hello Linux 셸 환경 (Bash)에 다시 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-276">If you have Oozie workflows that rely on hello Windows shell, you must rewrite hello workflows toorely on hello Linux shell environment (Bash).</span></span> <span data-ttu-id="9f737-277">Oozie와 함께 셸 작업을 사용하는 방법에 대한 자세한 내용은 [Oozie 셸 작업 확장](http://oozie.apache.org/docs/3.3.0/DG_ShellActionExtension.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f737-277">For more information on using shell actions with Oozie, see [Oozie shell action extension](http://oozie.apache.org/docs/3.3.0/DG_ShellActionExtension.html).</span></span>

<span data-ttu-id="9f737-278">셸 작업을 통해 호출된 C# 응용 프로그램에 의존하는 Oozie 워크플로가 있는 경우 Linux 환경에서 이러한 응용 프로그램을 검증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-278">If you have Oozie workflows that rely on C# applications invoked through shell actions, you must validate these applications in a Linux environment.</span></span> <span data-ttu-id="9f737-279">자세한 내용은 참조 [마이그레이션할.NET 솔루션 tooLinux 기반 HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-279">For more information, see [Migrate .NET solutions tooLinux-based HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md).</span></span>

## <a name="storm"></a><span data-ttu-id="9f737-280">Storm</span><span class="sxs-lookup"><span data-stu-id="9f737-280">Storm</span></span>

| <span data-ttu-id="9f737-281">Windows 기반</span><span class="sxs-lookup"><span data-stu-id="9f737-281">On Windows-based, I use...</span></span> | <span data-ttu-id="9f737-282">Linux 기반에서...</span><span class="sxs-lookup"><span data-stu-id="9f737-282">On Linux-based...</span></span> |
| --- | --- |
| <span data-ttu-id="9f737-283">Storm 대시보드</span><span class="sxs-lookup"><span data-stu-id="9f737-283">Storm Dashboard</span></span> |<span data-ttu-id="9f737-284">hello 스톰 대시보드를 사용할 수 없는 경우</span><span class="sxs-lookup"><span data-stu-id="9f737-284">hello Storm Dashboard is not available.</span></span> <span data-ttu-id="9f737-285">참조 [Linux 기반 HDInsight의 배포 및 관리 스톰 토폴로지](hdinsight-storm-deploy-monitor-topology-linux.md) 방법 toosubmit 토폴로지에 대 한</span><span class="sxs-lookup"><span data-stu-id="9f737-285">See [Deploy and Manage Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md) for ways toosubmit topologies</span></span> |
| <span data-ttu-id="9f737-286">Storm UI</span><span class="sxs-lookup"><span data-stu-id="9f737-286">Storm UI</span></span> |<span data-ttu-id="9f737-287">hello 스톰 UI https://CLUSTERNAME.azurehdinsight.net/stormui에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-287">hello Storm UI is available at https://CLUSTERNAME.azurehdinsight.net/stormui</span></span> |
| <span data-ttu-id="9f737-288">Visual Studio toocreate 배포 하 고 C# 또는 하이브리드 토폴로지를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-288">Visual Studio toocreate, deploy, and manage C# or hybrid topologies</span></span> |<span data-ttu-id="9f737-289">Visual Studio 사용한 toocreate 수 하 고 배포 하 고 C# (SCP.NET) 또는 2016 년 10 월 28 일 이후에 작성 하는 HDInsight 클러스터에서 Linux 기반 스톰에 하이브리드 토폴로지를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-289">Visual Studio can be used toocreate, deploy, and manage C# (SCP.NET) or hybrid topologies on Linux-based Storm on HDInsight clusters created after 10/28/2016.</span></span> |

## <a name="hbase"></a><span data-ttu-id="9f737-290">HBase</span><span class="sxs-lookup"><span data-stu-id="9f737-290">HBase</span></span>

<span data-ttu-id="9f737-291">Linux 기반 클러스터에서 HBase에 대 한 hello znode 부모는 `/hbase-unsecure`합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-291">On Linux-based clusters, hello znode parent for HBase is `/hbase-unsecure`.</span></span> <span data-ttu-id="9f737-292">네이티브 HBase Java API를 사용 하는 모든 Java 클라이언트 응용 프로그램에 대 한 hello 구성에서이 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-292">Set this value in hello configuration for any Java client applications that use native HBase Java API.</span></span>

<span data-ttu-id="9f737-293">이 값을 설정하는 예제 클라이언트에 대한 내용은 [Java 기반 HBase 응용 프로그램 빌드](hdinsight-hbase-build-java-maven.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f737-293">See [Build a Java-based HBase application](hdinsight-hbase-build-java-maven.md) for an example client that sets this value.</span></span>

## <a name="spark"></a><span data-ttu-id="9f737-294">Spark</span><span class="sxs-lookup"><span data-stu-id="9f737-294">Spark</span></span>

<span data-ttu-id="9f737-295">Spark 클러스터는 미리 보기 중 Windows 클러스터에서 사용 가능했지만</span><span class="sxs-lookup"><span data-stu-id="9f737-295">Spark clusters were available on Windows-clusters during preview.</span></span> <span data-ttu-id="9f737-296">Spark GA은 Linux 기반 클러스터에서만 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-296">Spark GA is only available with Linux-based clusters.</span></span> <span data-ttu-id="9f737-297">Windows 기반 Spark 클러스터 tooa 미리 보기 릴리스 Linux 기반 Spark 클러스터에서 마이그레이션 경로가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-297">There is no migration path from a Windows-based Spark preview cluster tooa release Linux-based Spark cluster.</span></span>

## <a name="known-issues"></a><span data-ttu-id="9f737-298">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="9f737-298">Known issues</span></span>

### <a name="azure-data-factory-custom-net-activities"></a><span data-ttu-id="9f737-299">Azure Data Factory 사용자 지정 .NET 작업</span><span class="sxs-lookup"><span data-stu-id="9f737-299">Azure Data Factory custom .NET activities</span></span>

<span data-ttu-id="9f737-300">Azure Data Factory 사용자 지정 .NET 작업은 현재 Linux 기반 HDInsight 클러스터에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-300">Azure Data Factory custom .NET activities are not currently supported on Linux-based HDInsight clusters.</span></span> <span data-ttu-id="9f737-301">대신, hello ADF 파이프라인의 일부로 메서드 tooimplement 사용자 지정 활동을 다음 중 하나를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-301">Instead, you should use one of hello following methods tooimplement custom activities as part of your ADF pipeline.</span></span>

* <span data-ttu-id="9f737-302">Azure 배치 풀에서 .NET 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-302">Execute .NET activities on Azure Batch pool.</span></span> <span data-ttu-id="9f737-303">hello 사용 하 여 Azure 배치 연결 된 서비스 섹션을 참조 [Azure 데이터 팩터리 파이프라인에서 사용자 지정 활동 사용](../data-factory/data-factory-use-custom-activities.md)</span><span class="sxs-lookup"><span data-stu-id="9f737-303">See hello Use Azure Batch linked service section of [Use custom activities in an Azure Data Factory pipeline](../data-factory/data-factory-use-custom-activities.md)</span></span>
* <span data-ttu-id="9f737-304">MapReduce 작업으로 hello 활동을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-304">Implement hello activity as a MapReduce activity.</span></span> <span data-ttu-id="9f737-305">자세한 내용은 [데이터 팩터리에서 MapReduce 프로그램 호출](../data-factory/data-factory-map-reduce.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f737-305">For more information, see [Invoke MapReduce Programs from Data Factory](../data-factory/data-factory-map-reduce.md).</span></span>

### <a name="line-endings"></a><span data-ttu-id="9f737-306">줄 끝</span><span class="sxs-lookup"><span data-stu-id="9f737-306">Line endings</span></span>

<span data-ttu-id="9f737-307">일반적으로 Windows 기반 시스템에서는 줄 끝으로 CRLF를 사용하며, Linux 기반 시스템에서는 LF를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-307">In general, line endings on Windows-based systems use CRLF, while Linux-based systems use LF.</span></span> <span data-ttu-id="9f737-308">생성 또는 CRLF 줄 끝을 사용 하 여 데이터에 예상 되는 경우 toomodify hello 생산자 또는 소비자 toowork hello LF 줄 끝으로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-308">If you produce, or expect, data with CRLF line endings, you may need toomodify hello producers or consumers toowork with hello LF line ending.</span></span>

<span data-ttu-id="9f737-309">Windows 기반 클러스터에서 HDInsight CRLF 사용 하 여 데이터를 반환 하는 예를 들어 tooquery Azure PowerShell을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-309">For example, using Azure PowerShell tooquery HDInsight on a Windows-based cluster returns data with CRLF.</span></span> <span data-ttu-id="9f737-310">hello Linux 기반으로 하는 클러스터로 동일한 쿼리에 반환 LF 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-310">hello same query with a Linux-based cluster returns LF.</span></span> <span data-ttu-id="9f737-311">Hello 줄 끝 마이그레이션을 수행 하기 전에 프로그램 solutuion에 문제가 발생 하는 경우에 toosee를 테스트 해야 tooa Linux 기반 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-311">You should test toosee if hello line ending causes a problem with your solutuion before migrating tooa Linux-based cluster.</span></span>

<span data-ttu-id="9f737-312">Hello Linux 클러스터 노드에서 직접 실행 되는 스크립트를 사용 하도록 설정한 경우에 hello 줄 끝으로 항상 LF를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-312">If you have scripts that are executed directly on hello Linux-cluster nodes, you should always use LF as hello line ending.</span></span> <span data-ttu-id="9f737-313">CRLF를 사용 하는 경우 Linux 기반 클러스터에서 hello 스크립트를 실행할 때 오류가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-313">If you use CRLF, you may see errors when running hello scripts on a Linux-based cluster.</span></span>

<span data-ttu-id="9f737-314">Hello 스크립트가 포함 된 CR 문자를 사용 하 여 문자열에 포함 되지 않도록를 알고 있으면 변경 hello 줄 끝 hello 메서드를 다음 중 하나를 사용 하 여 대량 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-314">If you know that hello scripts do not contain strings with embedded CR characters, you can bulk change hello line endings using one of hello following methods:</span></span>

* <span data-ttu-id="9f737-315">**Toohello 클러스터를 업로드 하기 전에**: hello 스크립트 toohello 클러스터를 업로드 하기 전에 PowerShell 문을 toochange hello 줄 끝 CRLF tooLF에서 다음 사용 하 여 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-315">**Before uploading toohello cluster**: Use hello following PowerShell statements toochange hello line endings from CRLF tooLF before uploading hello script toohello cluster.</span></span>

    ```powershell
    $original_file ='c:\path\to\script.py'
    $text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
    [IO.File]::WriteAllText($original_file, $text)
    ```

* <span data-ttu-id="9f737-316">**Toohello 클러스터 업로드 한 후**: SSH 세션 toohello Linux 기반 클러스터 toomodify hello 스크립트에서에서 사용 하 여 hello 다음 명령은 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f737-316">**After uploading toohello cluster**: Use hello following command from an SSH session toohello Linux-based cluster toomodify hello script.</span></span>

    ```bash
    hdfs dfs -get wasb:///path/to/script.py oldscript.py
    tr -d '\r' < oldscript.py > script.py
    hdfs dfs -put -f script.py wasb:///path/to/script.py
    ```

## <a name="next-steps"></a><span data-ttu-id="9f737-317">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9f737-317">Next Steps</span></span>

* [<span data-ttu-id="9f737-318">어떻게 toocreate Linux 기반 HDInsight 클러스터에 대해 알아봅니다</span><span class="sxs-lookup"><span data-stu-id="9f737-318">Learn how toocreate Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="9f737-319">SSH tooconnect tooHDInsight를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="9f737-319">Use SSH tooconnect tooHDInsight</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)
* [<span data-ttu-id="9f737-320">Ambari를 사용하여 Linux 기반 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="9f737-320">Manage a Linux-based cluster using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)
