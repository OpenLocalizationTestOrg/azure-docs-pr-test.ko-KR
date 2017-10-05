---
title: "Windows 기반 HDInsight에서 Linux 기반 HDInsight로 마이그레이션 - Azure | Microsoft Docs"
description: "Windows 기반 HDInsight 클러스터에서 Linux 기반 HDInsight 클러스터로 마이그레이션하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 35e80efe27081cd43243f488fa60447b76a20c32
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-from-a-windows-based-hdinsight-cluster-to-a-linux-based-cluster"></a><span data-ttu-id="c4ce6-103">Windows 기반 HDInsight 클러스터에서 Linux 기반 클러스터로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="c4ce6-103">Migrate from a Windows-based HDInsight cluster to a Linux-based cluster</span></span>

<span data-ttu-id="c4ce6-104">이 문서는 Windows와 Linux에서의 HDInsight 차이점과 기존 작업에서 Linux 기반 클러스터로 마이그레이션하는 방법에 대한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-104">This document provides details on the differences between HDInsight on Windows and Linux, and guidance on how to migrate existing workloads to a Linux-based cluster.</span></span>

<span data-ttu-id="c4ce6-105">Windows 기반 HDInsight가 클라우드에서 Hadoop을 사용하는 쉬운 방법을 제공하지만 Linux 기반 클러스터로 마이그레이션해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-105">While Windows-based HDInsight provides an easy way to use Hadoop in the cloud, you may need to migrate to a Linux-based cluster.</span></span> <span data-ttu-id="c4ce6-106">예를 들어, 솔루션에 필요한 Linux 기반 도구 및 기술을 활요하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-106">For example, to take advantage of Linux-based tools and technologies that are required for your solution.</span></span> <span data-ttu-id="c4ce6-107">Hadoop 에코시스템 내의 많은 개체가 Linux 기반 시스템에서 개발되며 Windows 기반 HDInsight에서 사용하지 못할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-107">Many things in the Hadoop ecosystem are developed on Linux-based systems, and may not be available for use with Windows-based HDInsight.</span></span> <span data-ttu-id="c4ce6-108">또한 많은 책, 동영상 및 기타 교육 자료에서 Hadoop 작업 시 Linux 시스템을 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-108">Additionally, many books, videos, and other training material assume that you are using a Linux system when working with Hadoop.</span></span>

> [!NOTE]
> <span data-ttu-id="c4ce6-109">HDInsight 클러스터는 클러스터의 노드에 대한 운영 체제로 Ubuntu LTS(장기 지원)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-109">HDInsight clusters use Ubuntu long-term support (LTS) as the operating system for the nodes in the cluster.</span></span> <span data-ttu-id="c4ce6-110">HDInsight와 함께 사용할 수 있는 Ubuntu의 버전 및 기타 구성 요소 버전 정보는 [HDInsight 구성 요소 버전](hdinsight-component-versioning.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-110">For information on the version of Ubuntu available with HDInsight, along with other component versioning information, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span>

## <a name="migration-tasks"></a><span data-ttu-id="c4ce6-111">마이그레이션 작업</span><span class="sxs-lookup"><span data-stu-id="c4ce6-111">Migration tasks</span></span>

<span data-ttu-id="c4ce6-112">마이그레이션에 대한 일반적인 워크플로는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-112">The general workflow for migration is as follows.</span></span>

![마이그레이션 워크플로 다이어그램](./media/hdinsight-migrate-from-windows-to-linux/workflow.png)

1. <span data-ttu-id="c4ce6-114">기존의 워크플로, 작업 등을 Linux 기반 클러스터로 마이그레이션할 때 필요한 변경 사항을 파악하려면 이 문서의 각 섹션을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-114">Read each section of this document to understand changes that may be required when migrating your existing workflow, jobs, etc. to a Linux-based cluster.</span></span>

2. <span data-ttu-id="c4ce6-115">테스트/품질 보증 환경으로 Linux 기반 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-115">Create a Linux-based cluster as a test/quality assurance environment.</span></span> <span data-ttu-id="c4ce6-116">Linux 기반 클러스터를 만드는 방법에 대한 자세한 내용은 [HDInsight에서 Linux 기반 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-116">For more information on creating a Linux-based cluster, see [Create Linux-based clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

3. <span data-ttu-id="c4ce6-117">기존 작업, 데이터 원본 및 싱크를 새 환경으로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-117">Copy existing jobs, data sources, and sinks to the new environment.</span></span>

4. <span data-ttu-id="c4ce6-118">작업이 새 클러스터에서 예상대로 작동하는지 확인하려면 유효성 검사 테스트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-118">Perform validation testing to make sure that your jobs work as expected on the new cluster.</span></span>

<span data-ttu-id="c4ce6-119">예상대로 작동하는 것이 확인되면 마이그레이션을 위해 가동 중지 시간을 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-119">Once you have verified that everything works as expected, schedule downtime for the migration.</span></span> <span data-ttu-id="c4ce6-120">가동 중지 시간 중 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-120">During this downtime, perform the following actions:</span></span>

1. <span data-ttu-id="c4ce6-121">클러스터 노드에 로컬로 저장된 모든 임시 데이터를 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-121">Back up any transient data stored locally on the cluster nodes.</span></span> <span data-ttu-id="c4ce6-122">예를 들어 헤드 노드에 직접 저장된 데이터가 있는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-122">For example, if you have data stored directly on a head node.</span></span>

2. <span data-ttu-id="c4ce6-123">Windows 기반 클러스터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-123">Delete the Windows-based cluster.</span></span>

3. <span data-ttu-id="c4ce6-124">Windows 기반 클러스터가 사용한 기본 데이터 저장소를 동일하게 사용하여 Linux 기반 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-124">Create a Linux-based cluster using the same default data store that the Windows-based cluster used.</span></span> <span data-ttu-id="c4ce6-125">Linux 기반 클러스터는 기존 프로덕션 데이터에 대한 작업을 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-125">The Linux-based cluster can continue working against your existing production data.</span></span>

4. <span data-ttu-id="c4ce6-126">백업한 모든 임시 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-126">Import any transient data you backed up.</span></span>

5. <span data-ttu-id="c4ce6-127">새 클러스터를 사용하여 작업을 시작하거나 계속 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-127">Start jobs/continue processing using the new cluster.</span></span>

### <a name="copy-data-to-the-test-environment"></a><span data-ttu-id="c4ce6-128">테스트 환경으로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="c4ce6-128">Copy data to the test environment</span></span>

<span data-ttu-id="c4ce6-129">데이터 및 작업을 복사하는 방법은 여러 가지가 있지만, 이 섹션에서 설명하는 두 가지 방법이 파일을 테스트 클러스터로 직접 이동시키는 가장 간단한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-129">There are many methods to copy the data and jobs, however the two discussed in this section are the simplest methods to directly move files to a test cluster.</span></span>

#### <a name="hdfs-copy"></a><span data-ttu-id="c4ce6-130">HDFS 복사</span><span class="sxs-lookup"><span data-stu-id="c4ce6-130">HDFS copy</span></span>

<span data-ttu-id="c4ce6-131">다음 단계를 사용하여 프로덕션 클러스터에서 테스트 클러스터로 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-131">Use the following steps to copy data from the production cluster to the test cluster.</span></span> <span data-ttu-id="c4ce6-132">이 단계에서는 HDInsight에 포함된 `hdfs dfs` 유틸리티를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-132">These steps use the `hdfs dfs` utility that is included with HDInsight.</span></span>

1. <span data-ttu-id="c4ce6-133">기존 클러스터에 대한 저장소 계정 및 기본 컨테이너 정보를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-133">Find the storage account and default container information for your existing cluster.</span></span> <span data-ttu-id="c4ce6-134">다음 예제에서는 PowerShell을 사용하여 이 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-134">The following example uses PowerShell to retrieve this information:</span></span>

    ```powershell
    $clusterName="Your existing HDInsight cluster name"
    $clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    write-host "Storage account name: $clusterInfo.DefaultStorageAccount.split('.')[0]"
    write-host "Default container: $clusterInfo.DefaultStorageContainer"
    ```

2. <span data-ttu-id="c4ce6-135">새 테스트 환경을 만들려면 HDInsight에서 Linux 기반 클러스터 만들기 문서에 나와 있는 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-135">To create a test environment, follow the steps in the Create Linux-based clusters in HDInsight document.</span></span> <span data-ttu-id="c4ce6-136">클러스터를 만들기 전에 **옵션 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-136">Stop before creating the cluster, and instead select **Optional Configuration**.</span></span>

3. <span data-ttu-id="c4ce6-137">옵션 구성 블레이드에서 **연결된 저장소 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-137">From the Optional Configuration blade, select **Linked Storage Accounts**.</span></span>

4. <span data-ttu-id="c4ce6-138">**저장소 키 추가**를 선택하고 메시지가 표시되면, 1단계의 PowerShell 스크립트에서 반환된 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-138">Select **Add a storage key**, and when prompted, select the storage account that was returned by the PowerShell script in step 1.</span></span> <span data-ttu-id="c4ce6-139">각 블레이드에서 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-139">Click **Select** on each blade.</span></span> <span data-ttu-id="c4ce6-140">마지막으로 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-140">Finally, create the cluster.</span></span>

5. <span data-ttu-id="c4ce6-141">클러스터가 만들어지면 **SSH**를 사용하여 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-141">Once the cluster has been created, connect to it using **SSH.**</span></span> <span data-ttu-id="c4ce6-142">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-142">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

6. <span data-ttu-id="c4ce6-143">SSH 세션에서 다음 명령을 사용하여 연결된 저장소 계정에서 새 기본 저장소 계정으로 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-143">From the SSH session, use the following command to copy files from the linked storage account to the new default storage account.</span></span> <span data-ttu-id="c4ce6-144">CONTAINER를 PowerShell에서 반환하는 컨테이너 정보로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-144">Replace CONTAINER with the container information returned by PowerShell.</span></span> <span data-ttu-id="c4ce6-145">__ACCOUNT__를 계정 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-145">Replace __ACCOUNT__ with the account name.</span></span> <span data-ttu-id="c4ce6-146">데이터 경로를 데이터 파일 경로로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-146">Replace the path to data with the path to a data file.</span></span>

    ```bash
    hdfs dfs -cp wasb://CONTAINER@ACCOUNT.blob.core.windows.net/path/to/old/data /path/to/new/location
    ```

    > [!NOTE]
    > <span data-ttu-id="c4ce6-147">데이터를 포함하는 디렉터리 구조가 테스트 환경에 없는 경우 다음 명령을 사용하면 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-147">If the directory structure that contains the data does not exist on the test environment, you can create it using the following command:</span></span>

    ```bash
    hdfs dfs -mkdir -p /new/path/to/create
    ```

    <span data-ttu-id="c4ce6-148">`-p` 스위치를 사용하면 경로의 모든 디렉터리를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-148">The `-p` switch enables the creation of all directories in  the path.</span></span>

#### <a name="direct-copy-between-blobs-in-azure-storage"></a><span data-ttu-id="c4ce6-149">Azure Storage Blob 간 직접 복사</span><span class="sxs-lookup"><span data-stu-id="c4ce6-149">Direct copy between blobs in Azure Storage</span></span>

<span data-ttu-id="c4ce6-150">또는 `Start-AzureStorageBlobCopy` Azure PowerShell cmdlet을 사용하여 HDInsight 외부의 저장소 계정 간에 Blob을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-150">Alternatively, you may want to use the `Start-AzureStorageBlobCopy` Azure PowerShell cmdlet to copy blobs between storage accounts outside of HDInsight.</span></span> <span data-ttu-id="c4ce6-151">자세한 내용은 Azure 저장소에서 Azure PowerShell 사용에 대한 Azure Blob 섹션 관리 방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-151">For more information, see the How to manage Azure Blobs section of Using Azure PowerShell with Azure Storage.</span></span>

## <a name="client-side-technologies"></a><span data-ttu-id="c4ce6-152">클라이언트 쪽 기술</span><span class="sxs-lookup"><span data-stu-id="c4ce6-152">Client-side technologies</span></span>

<span data-ttu-id="c4ce6-153">[Azure PowerShell cmdlets](/powershell/azureps-cmdlets-docs), [Azure CLI](../cli-install-nodejs.md), [.NET SDK for Hadoop](https://hadoopsdk.codeplex.com/) 등의 클라이언트 쪽 기술은 계속해서 Linux 기반 클러스터에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-153">Client-side technologies such as [Azure PowerShell cmdlets](/powershell/azureps-cmdlets-docs), [Azure CLI](../cli-install-nodejs.md), or the [.NET SDK for Hadoop](https://hadoopsdk.codeplex.com/) continue to work Linux-based clusters.</span></span> <span data-ttu-id="c4ce6-154">이러한 기술은 두 클러스터 OS 유형에서 동일한 REST API에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-154">These technologies rely on REST APIs that are the same across both cluster OS types.</span></span>

## <a name="server-side-technologies"></a><span data-ttu-id="c4ce6-155">서버 쪽 기술</span><span class="sxs-lookup"><span data-stu-id="c4ce6-155">Server-side technologies</span></span>

<span data-ttu-id="c4ce6-156">다음 표는 Windows와 관련된 서버 쪽 구성 요소 마이그레이션에 대한 참고 자료를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-156">The following table provides guidance on migrating server-side components that are Windows-specific.</span></span>

| <span data-ttu-id="c4ce6-157">사용 기술</span><span class="sxs-lookup"><span data-stu-id="c4ce6-157">If you are using this technology...</span></span> | <span data-ttu-id="c4ce6-158">수행 작업</span><span class="sxs-lookup"><span data-stu-id="c4ce6-158">Take this action...</span></span> |
| --- | --- |
| <span data-ttu-id="c4ce6-159">**PowerShell** (서버 쪽 스크립트, 클러스터 생성 중 사용한 스크립트 동작 포함)</span><span class="sxs-lookup"><span data-stu-id="c4ce6-159">**PowerShell** (server-side scripts, including Script Actions used during cluster creation)</span></span> |<span data-ttu-id="c4ce6-160">Bash 스크립트로 다시 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-160">Rewrite as Bash scripts.</span></span> <span data-ttu-id="c4ce6-161">스크립트 동작의 경우 [스크립트 동작에서 Linux 기반 HDInsight 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md) 및 [Linux 기반 HDInsight에 대한 스크립트 동작 개발](hdinsight-hadoop-script-actions-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-161">For Script Actions, see [Customize Linux-based HDInsight with Script Actions](hdinsight-hadoop-customize-cluster-linux.md) and [Script action development for Linux-based HDInsight](hdinsight-hadoop-script-actions-linux.md).</span></span> |
| <span data-ttu-id="c4ce6-162">**Azure CLI** (서버 쪽 스크립트)</span><span class="sxs-lookup"><span data-stu-id="c4ce6-162">**Azure CLI** (server-side scripts)</span></span> |<span data-ttu-id="c4ce6-163">Linux에서 Azure CLI를 사용할 수 있지만, HDInsight 클러스터 헤드 노드에 사전에 설치되어 있지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-163">While the Azure CLI is available on Linux, it does not come pre-installed on the HDInsight cluster head nodes.</span></span> <span data-ttu-id="c4ce6-164">Azure CLI 설치에 대한 자세한 내용은 [Azure CLI 2.0 시작](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-164">For more information on installing the Azure CLI, see [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span> |
| <span data-ttu-id="c4ce6-165">**.NET 구성 요소**</span><span class="sxs-lookup"><span data-stu-id="c4ce6-165">**.NET components**</span></span> |<span data-ttu-id="c4ce6-166">.NET은 Linux 기반 HDInsight 클러스터에서 [Mono](https://mono-project.com)를 통해 완전히 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-166">.NET is supported on Linux-based HDInsight through [Mono](https://mono-project.com).</span></span> <span data-ttu-id="c4ce6-167">자세한 내용은 [.NET 솔루션을 Linux 기반 HDInsight로 마이그레이션](hdinsight-hadoop-migrate-dotnet-to-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-167">For more information, see [Migrate .NET solutions to Linux-based HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md).</span></span> |
| <span data-ttu-id="c4ce6-168">**Win32 구성 요소 또는 기타 Windows 전용 기술**</span><span class="sxs-lookup"><span data-stu-id="c4ce6-168">**Win32 components or other Windows-only technology**</span></span> |<span data-ttu-id="c4ce6-169">참고 자료는 구성 요소 또는 기술에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-169">Guidance depends on the component or technology.</span></span> <span data-ttu-id="c4ce6-170">Linux와 호환되는 버전을 찾을 수도 있고 대체 솔루션을 찾거나 이 구성 요소를 다시 작성해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-170">You may be able to find a version that is compatible with Linux, or you may need to find an alternate solution or rewrite this component.</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="c4ce6-171">HDInsight 관리 SDK는 Mono와 완전히 호환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-171">The HDInsight management SDK is not fully compatible with Mono.</span></span> <span data-ttu-id="c4ce6-172">이때에는 HDInsight 클러스터에 배포된 솔루션의 일부로 사용하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-172">It should not be used as part of solutions deployed to the HDInsight cluster at this time.</span></span>

## <a name="cluster-creation"></a><span data-ttu-id="c4ce6-173">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="c4ce6-173">Cluster creation</span></span>

<span data-ttu-id="c4ce6-174">이 섹션에서는 클러스터 만들기의 차이에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-174">This section provides information on differences in cluster creation.</span></span>

### <a name="ssh-user"></a><span data-ttu-id="c4ce6-175">SSH 사용자</span><span class="sxs-lookup"><span data-stu-id="c4ce6-175">SSH User</span></span>

<span data-ttu-id="c4ce6-176">Linux 기반 HDInsight 클러스터는 클러스터 노드에 원격 액세스를 제공하기 위해 **SSH(Secure Shell)** 프로토콜을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-176">Linux-based HDInsight clusters use the **Secure Shell (SSH)** protocol to provide remote access to the cluster nodes.</span></span> <span data-ttu-id="c4ce6-177">Window 기반 클러스터용 원격 데스크톱과 달리, 대부분의 SSH 클라이언트는 그래픽 사용자 경험을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-177">Unlike Remote Desktop for Windows-based clusters, most SSH clients do not provide a graphical user experience.</span></span> <span data-ttu-id="c4ce6-178">대신, SSH 클라이언트가 클러스터에서 명령을 실행할 수 있는 명령줄을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-178">Instead, SSH clients provide a command line that allows you to run commands on the cluster.</span></span> <span data-ttu-id="c4ce6-179">일부 클라이언트(예: [MobaXterm](http://mobaxterm.mobatek.net/))는 원격 명령줄 외에 그래픽 파일 시스템 브라우저를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-179">Some clients (such as [MobaXterm](http://mobaxterm.mobatek.net/)) provide a graphical file system browser in addition to a remote command line.</span></span>

<span data-ttu-id="c4ce6-180">클러스터를 생성하는 동안 인증을 위해 SSH 사용자와 더불어 **암호** 또는 **공개 키 인증서** 중 하나를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-180">During cluster creation, you must provide an SSH user and either a **password** or **public key certificate** for authentication.</span></span>

<span data-ttu-id="c4ce6-181">암호보다는 공개 키 인증서가 더 안전하므로 공개 키 인증서를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-181">We recommend using Public key certificate, as it is more secure than using a password.</span></span> <span data-ttu-id="c4ce6-182">서명된 공개/개인 키 쌍을 생성한 후 클러스터를 생성할 때 공개 키를 제공하면 인증서 인증이 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-182">Certificate authentication works by generating a signed public/private key pair, then providing the public key when creating the cluster.</span></span> <span data-ttu-id="c4ce6-183">SSH를 사용하여 서버에 연결할 때 클라이언트의 개인 키는 연결을 위한 인증을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-183">When connecting to the server using SSH, the private key on the client provides authentication for the connection.</span></span>

<span data-ttu-id="c4ce6-184">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-184">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

### <a name="cluster-customization"></a><span data-ttu-id="c4ce6-185">클러스터 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="c4ce6-185">Cluster customization</span></span>

<span data-ttu-id="c4ce6-186">**스크립트 동작** 은 Bash 스크립트에서 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-186">**Script Actions** used with Linux-based clusters must be written in Bash script.</span></span> <span data-ttu-id="c4ce6-187">스크립트 동작은 클러스터 생성 중 사용할 수 있지만 Linux 기반 클러스터의 경우 클러스터가 작업을 실행한 후 사용자 지정을 수행할 때에도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-187">While Script Actions can be used during cluster creation, for Linux-based clusters they can also be used to perform customization after a cluster is up and running.</span></span> <span data-ttu-id="c4ce6-188">자세한 내용은 [스크립트 동작에서 Linux 기반 HDInsight 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md) 및 [Linux 기반 HDInsight에 대한 스크립트 동작 개발](hdinsight-hadoop-script-actions-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-188">For more information, see [Customize Linux-based HDInsight with Script Actions](hdinsight-hadoop-customize-cluster-linux.md) and [Script action development for Linux-based HDInsight](hdinsight-hadoop-script-actions-linux.md).</span></span>

<span data-ttu-id="c4ce6-189">다른 사용자 지정 기능은 **부트스트랩**입니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-189">Another customization feature is **bootstrap**.</span></span> <span data-ttu-id="c4ce6-190">Windows 클러스터의 경우 이 기능을 사용하면 Hive와 함께 사용하기 위한 추가 라이브러리 위치를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-190">For Windows clusters, this feature allows you to specify the location of additional libraries for use with Hive.</span></span> <span data-ttu-id="c4ce6-191">클러스터를 생성한 다음 이러한 라이브러리는 `ADD JAR`를 사용할 필요 없이 자동으로 Hive 쿼리와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-191">After cluster creation, these libraries are automatically available for use with Hive queries without the need to use `ADD JAR`.</span></span>

<span data-ttu-id="c4ce6-192">Linux 기반 클러스터용 부트스트랩은 이 기능을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-192">The Bootstrap feature for Linux-based clusters does not provide this functionality.</span></span> <span data-ttu-id="c4ce6-193">대신 [클러스터 생성 중 Hive 라이브러리 추가](hdinsight-hadoop-add-hive-libraries.md)에 설명된 스크립트 동작을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-193">Instead, use script action documented in [Add Hive libraries during cluster creation](hdinsight-hadoop-add-hive-libraries.md).</span></span>

### <a name="virtual-networks"></a><span data-ttu-id="c4ce6-194">가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="c4ce6-194">Virtual Networks</span></span>

<span data-ttu-id="c4ce6-195">Windows 기반 HDInsight 클러스터는 클래식 가상 네트워크에서만 작동하는 반면 Linux 기반 HDInsight 클러스터는 리소스 관리자 가상 네트워크가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-195">Windows-based HDInsight clusters only work with Classic Virtual Networks, while Linux-based HDInsight clusters require Resource Manager Virtual Networks.</span></span> <span data-ttu-id="c4ce6-196">Linux-HDInsight 클러스터에서 연결해야 하는 Classic Virtual Network에 리소스가 있는 경우 [Resource Manager Virtual Network에 Classic Virtual Network 연결](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-196">If you have resources in a Classic Virtual Network that the Linux-HDInsight cluster must connect to, see [Connecting a Classic Virtual Network to a Resource Manager Virtual Network](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span></span>

<span data-ttu-id="c4ce6-197">HDInsight에서 Azure 가상 네트워크를 사용하기 위한 구성 요구 사항에 대한 자세한 내용은 [가상 네트워크를 사용하여 HDInsight 기능 확장](hdinsight-extend-hadoop-virtual-network.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-197">For more information on configuration requirements for using Azure Virtual Networks with HDInsight, see [Extend HDInsight capabilities by using a Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span></span>

## <a name="management-and-monitoring"></a><span data-ttu-id="c4ce6-198">관리 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="c4ce6-198">Management and monitoring</span></span>

<span data-ttu-id="c4ce6-199">작업 기록 또는 Yarn UI와 같이 Windows 기반 HDInsight와 함께 사용했을 수도 있는 여러 웹 UI는 Ambari를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-199">Many of the web UIs you may have used with Windows-based HDInsight, such as Job History or Yarn UI, are available through Ambari.</span></span> <span data-ttu-id="c4ce6-200">또한 Ambari Hive 보기는 사용자의 웹 브라우저를 사용하여 Hive 쿼리를 실행하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-200">In addition, the Ambari Hive View provides a way to run Hive queries using your web browser.</span></span> <span data-ttu-id="c4ce6-201">Ambari 웹 UI는 https://CLUSTERNAME.azurehdinsight.net의 Linux 기반 클러스터에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-201">The Ambari Web UI is available on Linux-based clusters at https://CLUSTERNAME.azurehdinsight.net.</span></span>

<span data-ttu-id="c4ce6-202">Ambari 작업에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-202">For more information on working with Ambari, see the following documents:</span></span>

* [<span data-ttu-id="c4ce6-203">Ambari 웹</span><span class="sxs-lookup"><span data-stu-id="c4ce6-203">Ambari Web</span></span>](hdinsight-hadoop-manage-ambari.md)
* [<span data-ttu-id="c4ce6-204">Ambari REST API</span><span class="sxs-lookup"><span data-stu-id="c4ce6-204">Ambari REST API</span></span>](hdinsight-hadoop-manage-ambari-rest-api.md)

### <a name="ambari-alerts"></a><span data-ttu-id="c4ce6-205">Ambari 경고</span><span class="sxs-lookup"><span data-stu-id="c4ce6-205">Ambari Alerts</span></span>

<span data-ttu-id="c4ce6-206">Ambari에는 클러스터의 잠재적인 문제를 알려주는 경고 시스템이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-206">Ambari has an alert system that can tell you of potential problems with the cluster.</span></span> <span data-ttu-id="c4ce6-207">경고는 Ambari 웹 UI에 빨간색 또는 노란색 항목으로 나타나며 REST API를 통해서도 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-207">Alerts appear as red or yellow entries in the Ambari Web UI, however you can also retrieve them through the REST API.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c4ce6-208">Ambari 경고는 문제가 *있을 수 있다*라는 의미이며, 문제가 *있다*는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-208">Ambari alerts indicate that there *may* be a problem, not that there *is* a problem.</span></span> <span data-ttu-id="c4ce6-209">예를 들어 평소처럼 액세스할 수 있는데도 HiveServer2에 액세스할 수 없다는 경고가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-209">For example, you may receive an alert that HiveServer2 cannot be accessed, even though you can access it normally.</span></span>
>
> <span data-ttu-id="c4ce6-210">많은 경고는 서비스에서 간격 기반 쿼리로 구현되므로 특정 시간 프레임 내에서 응답을 기대합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-210">Many alerts are implemented as interval-based queries against a service, and expect a response within a specific time frame.</span></span> <span data-ttu-id="c4ce6-211">그러므로 경고가 발생했다고 해서 반드시 해당 서비스가 다운되었다는 것이 아니라 예상된 시간 프레임 내에 결과를 반환하지 않았다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-211">So the alert doesn't necessarily mean that the service is down, just that it didn't return results within the expected time frame.</span></span>

<span data-ttu-id="c4ce6-212">사용자는 조치를 취하기 전에 경고가 오랜 시간 동안 발생했는지 또는 이전에 보고되었던 사용자 문제를 반영하는지 여부를 평가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-212">You should evaluate whether an alert has been occurring for an extended period, or mirrors user problems that have been reported before taking action on it.</span></span>

## <a name="file-system-locations"></a><span data-ttu-id="c4ce6-213">파일 시스템 위치</span><span class="sxs-lookup"><span data-stu-id="c4ce6-213">File system locations</span></span>

<span data-ttu-id="c4ce6-214">Linux 클러스터 파일 시스템은 Windows 기반 HDInsight 클러스터와는 다르게 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-214">The Linux cluster file system is laid out differently than Windows-based HDInsight clusters.</span></span> <span data-ttu-id="c4ce6-215">다음 표를 사용하여 일반적으로 사용되는 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-215">Use the following table to find commonly used files.</span></span>

| <span data-ttu-id="c4ce6-216">찾는 대상</span><span class="sxs-lookup"><span data-stu-id="c4ce6-216">I need to find...</span></span> | <span data-ttu-id="c4ce6-217">위치</span><span class="sxs-lookup"><span data-stu-id="c4ce6-217">It is located...</span></span> |
| --- | --- |
| <span data-ttu-id="c4ce6-218">구성</span><span class="sxs-lookup"><span data-stu-id="c4ce6-218">Configuration</span></span> |<span data-ttu-id="c4ce6-219">`/etc`.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-219">`/etc`.</span></span> <span data-ttu-id="c4ce6-220">예: `/etc/hadoop/conf/core-site.xml`</span><span class="sxs-lookup"><span data-stu-id="c4ce6-220">For example, `/etc/hadoop/conf/core-site.xml`</span></span> |
| <span data-ttu-id="c4ce6-221">로그 파일</span><span class="sxs-lookup"><span data-stu-id="c4ce6-221">Log files</span></span> |`/var/logs` |
| <span data-ttu-id="c4ce6-222">HDP(Hortonworks Data Platform)</span><span class="sxs-lookup"><span data-stu-id="c4ce6-222">Hortonworks Data Platform (HDP)</span></span> |<span data-ttu-id="c4ce6-223">`/usr/hdp`.두 개의 디렉터리가 여기에 있으며 현재 HDP 버전 및 `current`입니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-223">`/usr/hdp`.There are two directories located here, one that is the current HDP version and `current`.</span></span> <span data-ttu-id="c4ce6-224">`current` 디렉터리에는 버전 번호 디렉터리에 있는 파일 및 디렉터리에 대한 바로 가기 링크가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-224">The `current` directory contains symbolic links to files and directories located in the version number directory.</span></span> <span data-ttu-id="c4ce6-225">`current` 디렉터리는 HDP 버전의 업데이트에 따라 버전 번호가 변경되므로 HDP 파일에 액세스하는 편리한 방법으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-225">The `current` directory is provided as a convenient way of accessing HDP files since the version number changes as the HDP version is updated.</span></span> |
| <span data-ttu-id="c4ce6-226">hadoop-streaming.jar</span><span class="sxs-lookup"><span data-stu-id="c4ce6-226">hadoop-streaming.jar</span></span> |`/usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar` |

<span data-ttu-id="c4ce6-227">일반적으로 파일 이름을 알면 파일 경로를 찾을 때 SSH 세션에서 다음 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-227">In general, if you know the name of the file, you can use the following command from an SSH session to find the file path:</span></span>

    find / -name FILENAME 2>/dev/null

<span data-ttu-id="c4ce6-228">파일 이름과 함께 와일드카드를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-228">You can also use wildcards with the file name.</span></span> <span data-ttu-id="c4ce6-229">예를 들어 `find / -name *streaming*.jar 2>/dev/null`는 파일 이름 중 'streaming'이라는 단어를 포함하는 모든 jar 파일의 경로를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-229">For example, `find / -name *streaming*.jar 2>/dev/null` returns the path to any jar files that contain the word 'streaming' as part of the file name.</span></span>

## <a name="hive-pig-and-mapreduce"></a><span data-ttu-id="c4ce6-230">Hive, Pig 및 MapReduce</span><span class="sxs-lookup"><span data-stu-id="c4ce6-230">Hive, Pig, and MapReduce</span></span>

<span data-ttu-id="c4ce6-231">Pig 및 MapReduce 워크로드는 Linux 기반 클러스터에서 매우 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-231">Pig and MapReduce workloads are similar on Linux-based clusters.</span></span> <span data-ttu-id="c4ce6-232">하지만 Linux 기반 HDInsight 클러스터는 Hadoop, Hive, Pig의 최신 버전을 사용하여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-232">However, Linux-based HDInsight clusters can be created using newer versions of Hadoop, Hive, and Pig.</span></span> <span data-ttu-id="c4ce6-233">이러한 버전 차이로 인해 기존 솔루션이 작동하는 방식이 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-233">These version differences may introduce changes in how your existing solutions function.</span></span> <span data-ttu-id="c4ce6-234">HDInsight와 함께 제공되는 구성 요소 버전에 대한 자세한 내용은 [HDInsight 구성 요소 버전 관리](hdinsight-component-versioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-234">For more information on the versions of components included with HDInsight, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="c4ce6-235">Linux 기반 HDInsight는 원격 데스크톱 기능을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-235">Linux-based HDInsight does not provide remote desktop functionality.</span></span> <span data-ttu-id="c4ce6-236">대신, SSH를 사용하여 클러스터 헤드 노드로 원격으로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-236">Instead, you can use SSH to remotely connect to the cluster head nodes.</span></span> <span data-ttu-id="c4ce6-237">자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-237">For more information, see the following documents:</span></span>

* [<span data-ttu-id="c4ce6-238">SSH와 함께 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="c4ce6-238">Use Hive with SSH</span></span>](hdinsight-hadoop-use-hive-ssh.md)
* [<span data-ttu-id="c4ce6-239">SSH와 함께 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="c4ce6-239">Use Pig with SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md)
* [<span data-ttu-id="c4ce6-240">SSH와 함께 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="c4ce6-240">Use MapReduce with SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md)

### <a name="hive"></a><span data-ttu-id="c4ce6-241">Hive</span><span class="sxs-lookup"><span data-stu-id="c4ce6-241">Hive</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c4ce6-242">외부 Hive 메타스토어를 사용하는 경우 Linux 기반 HDInsight와 함께 사용하기 전에 메타스토어를 백업해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-242">If you use an external Hive metastore, you should back up the metastore before using it with Linux-based HDInsight.</span></span> <span data-ttu-id="c4ce6-243">Linux 기반 HDInsight는 최신 버전의 Hive에서 사용할 수 있으며, 이 경우 이전 버전에서 만든 메타스토어와 호환되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-243">Linux-based HDInsight is available with newer versions of Hive, which may have incompatibilities with metastores created by earlier versions.</span></span>

<span data-ttu-id="c4ce6-244">다음 차트는 Hive 작업 마이그레이션에 대한 참고 자료를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-244">The following chart provides guidance on migrating your Hive workloads.</span></span>

| <span data-ttu-id="c4ce6-245">Windows 기반</span><span class="sxs-lookup"><span data-stu-id="c4ce6-245">On Windows-based, I use...</span></span> | <span data-ttu-id="c4ce6-246">Linux 기반에서...</span><span class="sxs-lookup"><span data-stu-id="c4ce6-246">On Linux-based...</span></span> |
| --- | --- |
| <span data-ttu-id="c4ce6-247">**Hive 편집기**</span><span class="sxs-lookup"><span data-stu-id="c4ce6-247">**Hive Editor**</span></span> |[<span data-ttu-id="c4ce6-248">Ambari에서 Hive 보기</span><span class="sxs-lookup"><span data-stu-id="c4ce6-248">Hive View in Ambari</span></span>](hdinsight-hadoop-use-hive-ambari-view.md) |
| <span data-ttu-id="c4ce6-249">`set hive.execution.engine=tez;` - Tez 사용 설정</span><span class="sxs-lookup"><span data-stu-id="c4ce6-249">`set hive.execution.engine=tez;` to enable Tez</span></span> |<span data-ttu-id="c4ce6-250">Tez는 Linux 기반 클러스터에 대한 기본 실행 엔진이므로 SET 문이 더 이상 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-250">Tez is the default execution engine for Linux-based clusters, so the set statement is no longer needed.</span></span> |
| <span data-ttu-id="c4ce6-251">C# 사용자 정의 함수</span><span class="sxs-lookup"><span data-stu-id="c4ce6-251">C# user-defined functions</span></span> | <span data-ttu-id="c4ce6-252">Linux 기반 HDInsight로 C# 구성 요소를 검증하는 방법에 대한 자세한 내용은 [.NET 솔루션을 Linux 기반 HDInsight로 마이그레이션](hdinsight-hadoop-migrate-dotnet-to-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-252">For information on validating C# components with Linux-based HDInsight, see [Migrate .NET solutions to Linux-based HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)</span></span> |
| <span data-ttu-id="c4ce6-253">Hive 작업의 일부로 호출된 서버의 CMD 파일 또는 스크립트</span><span class="sxs-lookup"><span data-stu-id="c4ce6-253">CMD files or scripts on the server invoked as part of a Hive job</span></span> |<span data-ttu-id="c4ce6-254">Bash 스크립트 사용</span><span class="sxs-lookup"><span data-stu-id="c4ce6-254">use Bash scripts</span></span> |
| <span data-ttu-id="c4ce6-255">`hive` 명령</span><span class="sxs-lookup"><span data-stu-id="c4ce6-255">`hive` command from remote desktop</span></span> |<span data-ttu-id="c4ce6-256">[SSH 세션에서 Hive](hdinsight-hadoop-use-hive-ssh.md) 또는 [Beeline](hdinsight-hadoop-use-hive-beeline.md) 사용</span><span class="sxs-lookup"><span data-stu-id="c4ce6-256">Use [Beeline](hdinsight-hadoop-use-hive-beeline.md) or [Hive from an SSH session](hdinsight-hadoop-use-hive-ssh.md)</span></span> |

### <a name="pig"></a><span data-ttu-id="c4ce6-257">Pig</span><span class="sxs-lookup"><span data-stu-id="c4ce6-257">Pig</span></span>

| <span data-ttu-id="c4ce6-258">Windows 기반</span><span class="sxs-lookup"><span data-stu-id="c4ce6-258">On Windows-based, I use...</span></span> | <span data-ttu-id="c4ce6-259">Linux 기반에서...</span><span class="sxs-lookup"><span data-stu-id="c4ce6-259">On Linux-based...</span></span> |
| --- | --- |
| <span data-ttu-id="c4ce6-260">C# 사용자 정의 함수</span><span class="sxs-lookup"><span data-stu-id="c4ce6-260">C# user-defined functions</span></span> | <span data-ttu-id="c4ce6-261">Linux 기반 HDInsight로 C# 구성 요소를 검증하는 방법에 대한 자세한 내용은 [.NET 솔루션을 Linux 기반 HDInsight로 마이그레이션](hdinsight-hadoop-migrate-dotnet-to-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-261">For information on validating C# components with Linux-based HDInsight, see [Migrate .NET solutions to Linux-based HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)</span></span> |
| <span data-ttu-id="c4ce6-262">서버에서 Pig 작업의 일부로 호출된 CMD 파일 또는 스크립트</span><span class="sxs-lookup"><span data-stu-id="c4ce6-262">CMD files or scripts on the server invoked as part of a Pig job</span></span> |<span data-ttu-id="c4ce6-263">Bash 스크립트 사용</span><span class="sxs-lookup"><span data-stu-id="c4ce6-263">use Bash scripts</span></span> |

### <a name="mapreduce"></a><span data-ttu-id="c4ce6-264">MapReduce</span><span class="sxs-lookup"><span data-stu-id="c4ce6-264">MapReduce</span></span>

| <span data-ttu-id="c4ce6-265">Windows 기반</span><span class="sxs-lookup"><span data-stu-id="c4ce6-265">On Windows-based, I use...</span></span> | <span data-ttu-id="c4ce6-266">Linux 기반에서...</span><span class="sxs-lookup"><span data-stu-id="c4ce6-266">On Linux-based...</span></span> |
| --- | --- |
| <span data-ttu-id="c4ce6-267">C# 매퍼 및 리듀서 구성 요소</span><span class="sxs-lookup"><span data-stu-id="c4ce6-267">C# mapper and reducer components</span></span> | <span data-ttu-id="c4ce6-268">Linux 기반 HDInsight로 C# 구성 요소를 검증하는 방법에 대한 자세한 내용은 [.NET 솔루션을 Linux 기반 HDInsight로 마이그레이션](hdinsight-hadoop-migrate-dotnet-to-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-268">For information on validating C# components with Linux-based HDInsight, see [Migrate .NET solutions to Linux-based HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)</span></span> |
| <span data-ttu-id="c4ce6-269">Hive 작업의 일부로 호출된 서버의 CMD 파일 또는 스크립트</span><span class="sxs-lookup"><span data-stu-id="c4ce6-269">CMD files or scripts on the server invoked as part of a Hive job</span></span> |<span data-ttu-id="c4ce6-270">Bash 스크립트 사용</span><span class="sxs-lookup"><span data-stu-id="c4ce6-270">use Bash scripts</span></span> |

## <a name="oozie"></a><span data-ttu-id="c4ce6-271">Oozie</span><span class="sxs-lookup"><span data-stu-id="c4ce6-271">Oozie</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c4ce6-272">외부 Oozie 메타스토어를 사용하는 경우 Linux 기반 HDInsight와 함께 사용하기 전에 메타스토어를 백업해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-272">If you use an external Oozie metastore, you should back up the metastore before using it with Linux-based HDInsight.</span></span> <span data-ttu-id="c4ce6-273">Linux 기반 HDInsight는 최신 버전의 Oozie에서 사용할 수 있으며, 이 경우 이전 버전에서 만든 메타스토어와 호환되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-273">Linux-based HDInsight is available with newer versions of Oozie, which may have incompatibilities with metastores created by earlier versions.</span></span>

<span data-ttu-id="c4ce6-274">Oozie 워크플로에서는 셸 작업이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-274">Oozie workflows allow shell actions.</span></span> <span data-ttu-id="c4ce6-275">셸 작업은 운영 체제의 기본 셸을 사용하여 명령줄 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-275">Shell actions use the default shell for the operating system to run command-line commands.</span></span> <span data-ttu-id="c4ce6-276">Windows 셸에 의존하는 Oozie 워크플로가 있는 경우 Linux 셸 환경(Bash)에 의존하도록 워크플로를 다시 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-276">If you have Oozie workflows that rely on the Windows shell, you must rewrite the workflows to rely on the Linux shell environment (Bash).</span></span> <span data-ttu-id="c4ce6-277">Oozie와 함께 셸 작업을 사용하는 방법에 대한 자세한 내용은 [Oozie 셸 작업 확장](http://oozie.apache.org/docs/3.3.0/DG_ShellActionExtension.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-277">For more information on using shell actions with Oozie, see [Oozie shell action extension](http://oozie.apache.org/docs/3.3.0/DG_ShellActionExtension.html).</span></span>

<span data-ttu-id="c4ce6-278">셸 작업을 통해 호출된 C# 응용 프로그램에 의존하는 Oozie 워크플로가 있는 경우 Linux 환경에서 이러한 응용 프로그램을 검증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-278">If you have Oozie workflows that rely on C# applications invoked through shell actions, you must validate these applications in a Linux environment.</span></span> <span data-ttu-id="c4ce6-279">자세한 내용은 [.NET 솔루션을 Linux 기반 HDInsight로 마이그레이션](hdinsight-hadoop-migrate-dotnet-to-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-279">For more information, see [Migrate .NET solutions to Linux-based HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md).</span></span>

## <a name="storm"></a><span data-ttu-id="c4ce6-280">Storm</span><span class="sxs-lookup"><span data-stu-id="c4ce6-280">Storm</span></span>

| <span data-ttu-id="c4ce6-281">Windows 기반</span><span class="sxs-lookup"><span data-stu-id="c4ce6-281">On Windows-based, I use...</span></span> | <span data-ttu-id="c4ce6-282">Linux 기반에서...</span><span class="sxs-lookup"><span data-stu-id="c4ce6-282">On Linux-based...</span></span> |
| --- | --- |
| <span data-ttu-id="c4ce6-283">Storm 대시보드</span><span class="sxs-lookup"><span data-stu-id="c4ce6-283">Storm Dashboard</span></span> |<span data-ttu-id="c4ce6-284">Storm 대시보드를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-284">The Storm Dashboard is not available.</span></span> <span data-ttu-id="c4ce6-285">토폴로지를 제출하는 방법은 [Linux 기반 HDInsight에서 Storm 토폴로지 배포 및 관리](hdinsight-storm-deploy-monitor-topology-linux.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-285">See [Deploy and Manage Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md) for ways to submit topologies</span></span> |
| <span data-ttu-id="c4ce6-286">Storm UI</span><span class="sxs-lookup"><span data-stu-id="c4ce6-286">Storm UI</span></span> |<span data-ttu-id="c4ce6-287">Storm UI는 https://CLUSTERNAME.azurehdinsight.net/stormui에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-287">The Storm UI is available at https://CLUSTERNAME.azurehdinsight.net/stormui</span></span> |
| <span data-ttu-id="c4ce6-288">C# 또는 하이브리드 토폴로지를 생성, 배포 및 관리하기 위한 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c4ce6-288">Visual Studio to create, deploy, and manage C# or hybrid topologies</span></span> |<span data-ttu-id="c4ce6-289">Visual Studio를 사용하여 2016년 10월 28일 이후 생성된 HDInsight 클러스터의 Linux 기반 Storm에서 C#(SCP.NET) 또는 하이브리드 토폴로지를 생성, 배포 및 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-289">Visual Studio can be used to create, deploy, and manage C# (SCP.NET) or hybrid topologies on Linux-based Storm on HDInsight clusters created after 10/28/2016.</span></span> |

## <a name="hbase"></a><span data-ttu-id="c4ce6-290">HBase</span><span class="sxs-lookup"><span data-stu-id="c4ce6-290">HBase</span></span>

<span data-ttu-id="c4ce6-291">Linux 기반 클러스터에서 HBase에 대한 znode 상위는 `/hbase-unsecure`입니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-291">On Linux-based clusters, the znode parent for HBase is `/hbase-unsecure`.</span></span> <span data-ttu-id="c4ce6-292">기본 HBase Java API를 사용하는 모든 Java 클라이언트 응용 프로그램 구성에서 이 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-292">Set this value in the configuration for any Java client applications that use native HBase Java API.</span></span>

<span data-ttu-id="c4ce6-293">이 값을 설정하는 예제 클라이언트에 대한 내용은 [Java 기반 HBase 응용 프로그램 빌드](hdinsight-hbase-build-java-maven.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-293">See [Build a Java-based HBase application](hdinsight-hbase-build-java-maven.md) for an example client that sets this value.</span></span>

## <a name="spark"></a><span data-ttu-id="c4ce6-294">Spark</span><span class="sxs-lookup"><span data-stu-id="c4ce6-294">Spark</span></span>

<span data-ttu-id="c4ce6-295">Spark 클러스터는 미리 보기 중 Windows 클러스터에서 사용 가능했지만</span><span class="sxs-lookup"><span data-stu-id="c4ce6-295">Spark clusters were available on Windows-clusters during preview.</span></span> <span data-ttu-id="c4ce6-296">Spark GA은 Linux 기반 클러스터에서만 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-296">Spark GA is only available with Linux-based clusters.</span></span> <span data-ttu-id="c4ce6-297">Windows 기반 Spark 미리 보기 클러스터에서 릴리스 Linux 기반 Spark 클러스터까지의 마이그레이션 경로는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-297">There is no migration path from a Windows-based Spark preview cluster to a release Linux-based Spark cluster.</span></span>

## <a name="known-issues"></a><span data-ttu-id="c4ce6-298">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="c4ce6-298">Known issues</span></span>

### <a name="azure-data-factory-custom-net-activities"></a><span data-ttu-id="c4ce6-299">Azure Data Factory 사용자 지정 .NET 작업</span><span class="sxs-lookup"><span data-stu-id="c4ce6-299">Azure Data Factory custom .NET activities</span></span>

<span data-ttu-id="c4ce6-300">Azure Data Factory 사용자 지정 .NET 작업은 현재 Linux 기반 HDInsight 클러스터에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-300">Azure Data Factory custom .NET activities are not currently supported on Linux-based HDInsight clusters.</span></span> <span data-ttu-id="c4ce6-301">대신 ADF 파이프라인의 일부로 사용자 지정 작업을 구현하기 위해서는 다음 방법 중 하나를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-301">Instead, you should use one of the following methods to implement custom activities as part of your ADF pipeline.</span></span>

* <span data-ttu-id="c4ce6-302">Azure 배치 풀에서 .NET 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-302">Execute .NET activities on Azure Batch pool.</span></span> <span data-ttu-id="c4ce6-303">[Azure Data Factory 파이프라인에서 사용자 지정 작업 사용](../data-factory/data-factory-use-custom-activities.md)</span><span class="sxs-lookup"><span data-stu-id="c4ce6-303">See the Use Azure Batch linked service section of [Use custom activities in an Azure Data Factory pipeline](../data-factory/data-factory-use-custom-activities.md)</span></span>
* <span data-ttu-id="c4ce6-304">MapReduce 작업으로 작업을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-304">Implement the activity as a MapReduce activity.</span></span> <span data-ttu-id="c4ce6-305">자세한 내용은 [데이터 팩터리에서 MapReduce 프로그램 호출](../data-factory/data-factory-map-reduce.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-305">For more information, see [Invoke MapReduce Programs from Data Factory](../data-factory/data-factory-map-reduce.md).</span></span>

### <a name="line-endings"></a><span data-ttu-id="c4ce6-306">줄 끝</span><span class="sxs-lookup"><span data-stu-id="c4ce6-306">Line endings</span></span>

<span data-ttu-id="c4ce6-307">일반적으로 Windows 기반 시스템에서는 줄 끝으로 CRLF를 사용하며, Linux 기반 시스템에서는 LF를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-307">In general, line endings on Windows-based systems use CRLF, while Linux-based systems use LF.</span></span> <span data-ttu-id="c4ce6-308">CRLF 줄 끝을 사용하여 데이터를 생성 또는 예상하는 경우, LF 줄 끝을 사용하여 작업하려면 공급자 또는 소비자를 수정해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-308">If you produce, or expect, data with CRLF line endings, you may need to modify the producers or consumers to work with the LF line ending.</span></span>

<span data-ttu-id="c4ce6-309">예를 들어 Windows 기반 클러스터에서 Azure PowerShell을 사용하여 HDInsight를 쿼리하면 CRLF를 사용하여 데이터를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-309">For example, using Azure PowerShell to query HDInsight on a Windows-based cluster returns data with CRLF.</span></span> <span data-ttu-id="c4ce6-310">Linux 기반 클러스터의 동일한 쿼리는 LF를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-310">The same query with a Linux-based cluster returns LF.</span></span> <span data-ttu-id="c4ce6-311">Linux 기반 클러스터로 마이그레이션하기 전에 줄 끝이 솔루션에 문제를 일으키는지 테스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-311">You should test to see if the line ending causes a problem with your solutuion before migrating to a Linux-based cluster.</span></span>

<span data-ttu-id="c4ce6-312">Linux 클러스터 노드에서 직접 실행되는 스크립트가 있는 경우에는 항상 LF를 줄 끝으로 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-312">If you have scripts that are executed directly on the Linux-cluster nodes, you should always use LF as the line ending.</span></span> <span data-ttu-id="c4ce6-313">CRLF를 사용하는 경우 Linux 기반 클러스터에서 스크립트를 실행할 때 오류가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-313">If you use CRLF, you may see errors when running the scripts on a Linux-based cluster.</span></span>

<span data-ttu-id="c4ce6-314">포함된 CR 문자가 있는 문자열이 스크립트에 없는 경우 다음 방법 중 하나를 사용하여 줄 끝을 대량 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-314">If you know that the scripts do not contain strings with embedded CR characters, you can bulk change the line endings using one of the following methods:</span></span>

* <span data-ttu-id="c4ce6-315">**스크립트를 클러스터에 업로드하기 전**: 스크립트를 클러스터에 업로드하기 전 다음 PowerShell 문을 사용하여 줄 끝을 CRLF에서 LF로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-315">**Before uploading to the cluster**: Use the following PowerShell statements to change the line endings from CRLF to LF before uploading the script to the cluster.</span></span>

    ```powershell
    $original_file ='c:\path\to\script.py'
    $text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
    [IO.File]::WriteAllText($original_file, $text)
    ```

* <span data-ttu-id="c4ce6-316">**클러스터에 업로드한 후:** Linux 기반 클러스터에 대한 SSH 세션에서 다음 명령을 사용하여 스크립트를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="c4ce6-316">**After uploading to the cluster**: Use the following command from an SSH session to the Linux-based cluster to modify the script.</span></span>

    ```bash
    hdfs dfs -get wasb:///path/to/script.py oldscript.py
    tr -d '\r' < oldscript.py > script.py
    hdfs dfs -put -f script.py wasb:///path/to/script.py
    ```

## <a name="next-steps"></a><span data-ttu-id="c4ce6-317">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c4ce6-317">Next Steps</span></span>

* [<span data-ttu-id="c4ce6-318">Linux 기반 HDInsight 클러스터를 만드는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="c4ce6-318">Learn how to create Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="c4ce6-319">SSH를 사용하여 HDInsight에 연결</span><span class="sxs-lookup"><span data-stu-id="c4ce6-319">Use SSH to connect to HDInsight</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)
* [<span data-ttu-id="c4ce6-320">Ambari를 사용하여 Linux 기반 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="c4ce6-320">Manage a Linux-based cluster using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)
