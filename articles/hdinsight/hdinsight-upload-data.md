---
title: "HDInsight에서 Hadoop 작업용 데이터 업로드 | Microsoft Docs"
description: "Azure CLI, Azure 저장소 탐색기, Azure PowerShell, Hadoop 명령줄 또는 Sqoop을 사용하여 HDInsight에서 Hadoop 작업 데이터를 업로드 및 액세스하는 방법에 대해 알아봅니다."
keywords: "etl hadoop, hadoop으로 데이터 가져오기, hadoop 데이터 로드"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 56b913ee-0f9a-4e9f-9eaf-c571f8603dd6
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: jgao
ms.openlocfilehash: 6867f96c8ea0e31ed0e682cef48e7aa5e3f65f86
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-data-for-hadoop-jobs-in-hdinsight"></a><span data-ttu-id="1f3b9-104">HDInsight에서 Hadoop 작업용 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="1f3b9-104">Upload data for Hadoop jobs in HDInsight</span></span>
<span data-ttu-id="1f3b9-105">Azure HDInsight는 Azure Blob 저장소를 통해 모든 기능을 갖춘 HDFS(Hadoop Distributed File System)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-105">Azure HDInsight provides a full-featured Hadoop distributed file system (HDFS) over Azure Blob storage.</span></span> <span data-ttu-id="1f3b9-106">고객에게 원활한 환경을 제공하기 위해 HDFS를 확장하여 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-106">It is designed as an HDFS extension to provide a seamless experience to customers.</span></span> <span data-ttu-id="1f3b9-107">이를 통해 Hadoop 에코 시스템에서 구성 요소의 전체 집합이 관리하는 데이터에서 직접 작동하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-107">It enables the full set of components in the Hadoop ecosystem to operate directly on the data it manages.</span></span> <span data-ttu-id="1f3b9-108">Azure Blob 저장소와 HDFS는 데이터의 저장소 및 해당 데이터의 계산을 최적화하는 별개의 파일 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-108">Azure Blob storage and HDFS are distinct file systems that are optimized for storage of data and computations on that data.</span></span> <span data-ttu-id="1f3b9-109">Azure Blob Storage를 사용하는 이점에 대한 자세한 내용은 [HDInsight에서 Azure Blob Storage 사용][hdinsight-storage]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-109">For information about the benefits of using Azure Blob storage, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="1f3b9-110">**필수 구성 요소**</span><span class="sxs-lookup"><span data-stu-id="1f3b9-110">**Prerequisites**</span></span>

<span data-ttu-id="1f3b9-111">시작하기 전에 다음 요구 사항을 확인하세요:</span><span class="sxs-lookup"><span data-stu-id="1f3b9-111">Note the following requirement before you begin:</span></span>

* <span data-ttu-id="1f3b9-112">Azure HDInsight 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-112">An Azure HDInsight cluster.</span></span> <span data-ttu-id="1f3b9-113">자세한 내용은 [Azure HDInsight 시작][hdinsight-get-started] 또는 [HDInsight 클러스터 프로비전][hdinsight-provision]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-113">For instructions, see [Get started with Azure HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span>

## <a name="why-blob-storage"></a><span data-ttu-id="1f3b9-114">Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="1f3b9-114">Why blob storage?</span></span>
<span data-ttu-id="1f3b9-115">Azure HDInsight 클러스터는 일반적으로 MapReduce 작업 실행을 위해 배포되며 이러한 작업이 완료되면 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-115">Azure HDInsight clusters are typically deployed to run MapReduce jobs, and the clusters are dropped after these jobs complete.</span></span> <span data-ttu-id="1f3b9-116">계산이 완료된 후 HDFS 클러스터에 데이터를 유지하면 데이터 저장에 비용이 많이 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-116">Keeping the data in the HDFS clusters after computations are complete would be an expensive way to store this data.</span></span> <span data-ttu-id="1f3b9-117">Azure Blob 저장소는 HDInsight를 사용하여 처리할 데이터를 위한 옵션으로서 확장성, 가용성, 용량이 뛰어나고 경제적이며 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-117">Azure Blob storage is a highly available, highly scalable, high capacity, low cost, and shareable storage option for data that is to be processed using HDInsight.</span></span> <span data-ttu-id="1f3b9-118">Blob에 데이터를 저장하면 계산에 사용할 HDInsight 클러스터를 데이터 손실 없이 안전하게 릴리스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-118">Storing data in a blob enables the HDInsight clusters that are used for computation to be safely released without losing data.</span></span>

### <a name="directories"></a><span data-ttu-id="1f3b9-119">디렉터리</span><span class="sxs-lookup"><span data-stu-id="1f3b9-119">Directories</span></span>
<span data-ttu-id="1f3b9-120">Azure Blob 저장소 컨테이너는 키/값 쌍으로 데이터를 저장하며, 디렉터리 계층 구조는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-120">Azure Blob storage containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="1f3b9-121">그러나 파일이 디렉터리 구조 내에 저장된 것처럼 보이도록 키 이름에 "/" 문자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-121">However the "/" character can be used within the key name to make it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="1f3b9-122">HDInsight는 실제 디렉토리처럼 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-122">HDInsight sees these as if they are actual directories.</span></span>

<span data-ttu-id="1f3b9-123">예를 들어 Blob의 키 이름을 *input/log1.txt*로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-123">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="1f3b9-124">실제로 "input" 디렉터리는 없지만 키 이름에 "/" 문자가 있으므로 파일 경로처럼 보입니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-124">No actual "input" directory exists, but due to the presence of the "/" character in the key name, it has the appearance of a file path.</span></span>

<span data-ttu-id="1f3b9-125">이 때문에, Azure 탐색기 도구를 사용하면 몇몇 0바이트 파일을 발견할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-125">Because of this, if you use Azure Explorer tools you may notice some 0 byte files.</span></span> <span data-ttu-id="1f3b9-126">이러한 파일의 목적은 두 가지입니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-126">These files serve two purposes:</span></span>

* <span data-ttu-id="1f3b9-127">빈 폴더가 있으면 폴더의 존재를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-127">If there are empty folders, they mark of the existence of the folder.</span></span> <span data-ttu-id="1f3b9-128">Azure Blob 저장소는 지능적이어서 foo/bar라는 Blob이 있으면 **foo**라는 폴더도 있다는 사실을 압니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-128">Azure Blob storage is clever enough to know that if a blob called foo/bar exists, there is a folder called **foo**.</span></span> <span data-ttu-id="1f3b9-129">그러나 **foo** 라는 빈 폴더를 보여주려는 경우 유일한 방법은 이 특별한 0바이트 파일을 만들어 두는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-129">But the only way to signify an empty folder called **foo** is by having this special 0 byte file in place.</span></span>
* <span data-ttu-id="1f3b9-130">Hadoop 파일 시스템에 필요한 몇몇 특수 메타데이터, 특히 폴더에 대한 사용 권한 및 소유자를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-130">They hold special metadata that is needed by the Hadoop file system, notably the permissions and owners for the folders.</span></span>

## <a name="command-line-utilities"></a><span data-ttu-id="1f3b9-131">명령줄 유틸리티</span><span class="sxs-lookup"><span data-stu-id="1f3b9-131">Command-line utilities</span></span>
<span data-ttu-id="1f3b9-132">Microsoft는 Azure Blob 저장소에서 작업할 다음 유틸리티를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-132">Microsoft provides the following utilities to work with Azure Blob storage:</span></span>

| <span data-ttu-id="1f3b9-133">도구</span><span class="sxs-lookup"><span data-stu-id="1f3b9-133">Tool</span></span> | <span data-ttu-id="1f3b9-134">Linux</span><span class="sxs-lookup"><span data-stu-id="1f3b9-134">Linux</span></span> | <span data-ttu-id="1f3b9-135">OS X</span><span class="sxs-lookup"><span data-stu-id="1f3b9-135">OS X</span></span> | <span data-ttu-id="1f3b9-136">Windows</span><span class="sxs-lookup"><span data-stu-id="1f3b9-136">Windows</span></span> |
| --- |:---:|:---:|:---:|
| <span data-ttu-id="1f3b9-137">[Azure 명령줄 인터페이스][azurecli]</span><span class="sxs-lookup"><span data-stu-id="1f3b9-137">[Azure Command-Line Interface][azurecli]</span></span> |<span data-ttu-id="1f3b9-138">✔</span><span class="sxs-lookup"><span data-stu-id="1f3b9-138">✔</span></span> |<span data-ttu-id="1f3b9-139">✔</span><span class="sxs-lookup"><span data-stu-id="1f3b9-139">✔</span></span> |<span data-ttu-id="1f3b9-140">✔</span><span class="sxs-lookup"><span data-stu-id="1f3b9-140">✔</span></span> |
| <span data-ttu-id="1f3b9-141">[Azure PowerShell][azure-powershell]</span><span class="sxs-lookup"><span data-stu-id="1f3b9-141">[Azure PowerShell][azure-powershell]</span></span> | | |<span data-ttu-id="1f3b9-142">✔</span><span class="sxs-lookup"><span data-stu-id="1f3b9-142">✔</span></span> |
| <span data-ttu-id="1f3b9-143">[AzCopy][azure-azcopy]</span><span class="sxs-lookup"><span data-stu-id="1f3b9-143">[AzCopy][azure-azcopy]</span></span> | | |<span data-ttu-id="1f3b9-144">✔</span><span class="sxs-lookup"><span data-stu-id="1f3b9-144">✔</span></span> |
| [<span data-ttu-id="1f3b9-145">Hadoop 명령</span><span class="sxs-lookup"><span data-stu-id="1f3b9-145">Hadoop command</span></span>](#commandline) |<span data-ttu-id="1f3b9-146">✔</span><span class="sxs-lookup"><span data-stu-id="1f3b9-146">✔</span></span> |<span data-ttu-id="1f3b9-147">✔</span><span class="sxs-lookup"><span data-stu-id="1f3b9-147">✔</span></span> |<span data-ttu-id="1f3b9-148">✔</span><span class="sxs-lookup"><span data-stu-id="1f3b9-148">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="1f3b9-149">모든 Azure CLI, Azure PowerShell 및 AzCopy는 외부 Azure에서 사용될 수 있지만, Hadoop 명령만 HDInsight 클러스터에서 사용할 수 있으며 데이터를 로컬 파일 시스템에서 Azure Blob 저장소로 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-149">While the Azure CLI, Azure PowerShell, and AzCopy can all be used from outside Azure, the Hadoop command is only available on the HDInsight cluster and only allows loading data from the local file system into Azure Blob storage.</span></span>
>
>

### <span data-ttu-id="1f3b9-150"><a id="xplatcli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1f3b9-150"><a id="xplatcli"></a>Azure CLI</span></span>
<span data-ttu-id="1f3b9-151">Azure CLI는 Azure 서비스를 관리할 수 있도록 하는 크로스 플랫폼 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-151">The Azure CLI is a cross-platform tool that allows you to manage Azure services.</span></span> <span data-ttu-id="1f3b9-152">Azure Blob 저장소에 데이터를 업로드하려면 다음 단계를 사용합니다:</span><span class="sxs-lookup"><span data-stu-id="1f3b9-152">Use the following steps to upload data to Azure Blob storage:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="1f3b9-153">[Mac, Linux 및 Windows용 Azure CLI의 설치 및 구성](../cli-install-nodejs.md)</span><span class="sxs-lookup"><span data-stu-id="1f3b9-153">[Install and configure the Azure CLI for Mac, Linux and Windows](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="1f3b9-154">명령 프롬프트, bash 또는 다른 셸을 열고 다음을 사용하여 Azure 구독을 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-154">Open a command prompt, bash, or other shell, and use the following to authenticate to your Azure subscription.</span></span>

        azure login

    <span data-ttu-id="1f3b9-155">메시지가 표시되면 구독하려는 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-155">When prompted, enter the user name and password for your subscription.</span></span>
3. <span data-ttu-id="1f3b9-156">다음 명령을 사용하여 구독하려는 저장소 계정을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-156">Enter the following command to list the storage accounts for your subscription:</span></span>

        azure storage account list
4. <span data-ttu-id="1f3b9-157">작업하려는 blob이 포함된 저장소 계정을 선택한 후에 다음 명령을 사용하여 이 계정에 대한 키를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-157">Select the storage account that contains the blob you want to work with, then use the following command to retrieve the key for this account:</span></span>

        azure storage account keys list <storage-account-name>

    <span data-ttu-id="1f3b9-158">**기본** 및 **보조** 키가 반환되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-158">This should return **Primary** and **Secondary** keys.</span></span> <span data-ttu-id="1f3b9-159">다음 단계에서 사용되므로 **기본** 키 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-159">Copy the **Primary** key value because it will be used in the next steps.</span></span>
5. <span data-ttu-id="1f3b9-160">저장소 계정 내에서 blob 컨테이너의 목록을 검색하려면 다음 명령을 사용합니다:</span><span class="sxs-lookup"><span data-stu-id="1f3b9-160">Use the following command to retrieve a list of blob containers within the storage account:</span></span>

        azure storage container list -a <storage-account-name> -k <primary-key>
6. <span data-ttu-id="1f3b9-161">파일을 blob에 업로드 및 다운로드하려면 다음 명령을 사용합니다:</span><span class="sxs-lookup"><span data-stu-id="1f3b9-161">Use the following commands to upload and download files to the blob:</span></span>

   * <span data-ttu-id="1f3b9-162">파일을 업로드하려면:</span><span class="sxs-lookup"><span data-stu-id="1f3b9-162">To upload a file:</span></span>

           azure storage blob upload -a <storage-account-name> -k <primary-key> <source-file> <container-name> <blob-name>
   * <span data-ttu-id="1f3b9-163">파일을 다운로드하려면:</span><span class="sxs-lookup"><span data-stu-id="1f3b9-163">To download a file:</span></span>

           azure storage blob download -a <storage-account-name> -k <primary-key> <container-name> <blob-name> <destination-file>

> [!NOTE]
> <span data-ttu-id="1f3b9-164">항상 동일한 저장소 계정으로 작업하는 경우 모든 명령에 대한 키를 지정하는 대신 다음의 환경 변수를 설정할 수 있습니다:</span><span class="sxs-lookup"><span data-stu-id="1f3b9-164">If you will always be working with the same storage account, you can set the following environment variables instead of specifying the account and key for every command:</span></span>
>
> * <span data-ttu-id="1f3b9-165">**AZURE\_STORAGE\_ACCOUNT**: 저장소 계정 이름</span><span class="sxs-lookup"><span data-stu-id="1f3b9-165">**AZURE\_STORAGE\_ACCOUNT**: The storage account name</span></span>
> * <span data-ttu-id="1f3b9-166">**AZURE\_STORAGE\_ACCESS\_KEY**: 저장소 계정 키</span><span class="sxs-lookup"><span data-stu-id="1f3b9-166">**AZURE\_STORAGE\_ACCESS\_KEY**: The storage account key</span></span>
>
>

### <span data-ttu-id="1f3b9-167"><a id="powershell"></a>Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f3b9-167"><a id="powershell"></a>Azure PowerShell</span></span>
<span data-ttu-id="1f3b9-168">Azure PowerShell은 Azure에서 작업의 배포와 관리를 제어 및 자동화하기 위해 사용할 수 있는 스크립팅 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-168">Azure PowerShell is a scripting environment that you can use to control and automate the deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="1f3b9-169">Azure PowerShell을 실행하기 위해 워크스테이션을 구성하는 방법에 대한 자세한 내용은 [Azure PowerShell 설치 및 구성](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-169">For information about configuring your workstation to run Azure PowerShell, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="1f3b9-170">**Azure Blob 저장소에 로컬 파일을 업로드하려면**</span><span class="sxs-lookup"><span data-stu-id="1f3b9-170">**To upload a local file to Azure Blob storage**</span></span>

1. <span data-ttu-id="1f3b9-171">[Azure PowerShell 설치 및 구성](/powershell/azure/overview)의 지침에 따라 Azure PowerShell 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-171">Open the Azure PowerShell console as instructed in [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="1f3b9-172">다음 스크립트에서 처음 5개의 변수 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-172">Set the values of the first five variables in the following script:</span></span>

        $resourceGroupName = "<AzureResourceGroupName>"
        $storageAccountName = "<StorageAccountName>"
        $containerName = "<ContainerName>"

        $fileName ="<LocalFileName>"
        $blobName = "<BlobName>"

        # Get the storage account key
        $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
        # Create the storage context object
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

        # Copy the file from local workstation to the Blob container
        Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob $blobName -context $destContext
3. <span data-ttu-id="1f3b9-173">Azure PowerShell 콘솔에 스크립트를 붙여넣고 실행하여 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-173">Paste the script into the Azure PowerShell console to run it to copy the file.</span></span>

<span data-ttu-id="1f3b9-174">예를 들어, HDInsight와 함께 작동하도록 만들진 PowerShell 스크립트는 [HDInsight 도구](https://github.com/blackmist/hdinsight-tools)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-174">For example PowerShell scripts created to work with HDInsight, see [HDInsight tools](https://github.com/blackmist/hdinsight-tools).</span></span>

### <span data-ttu-id="1f3b9-175"><a id="azcopy"></a>AzCopy</span><span class="sxs-lookup"><span data-stu-id="1f3b9-175"><a id="azcopy"></a>AzCopy</span></span>
<span data-ttu-id="1f3b9-176">AzCopy는 데이터를 Azure 저장소 계정으로 보내고 받는 작업을 간소화하도록 설계된 명령줄 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-176">AzCopy is a command-line tool that is designed to simplify the task of transferring data into and out of an Azure Storage account.</span></span> <span data-ttu-id="1f3b9-177">이 유틸리티는 독립 실행형 도구로 사용할 수도 있고 기존 응용 프로그램에 통합할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-177">You can use it as a standalone tool or incorporate this tool in an existing application.</span></span> <span data-ttu-id="1f3b9-178">[AzCopy를 다운로드][azure-azcopy-download]하세요.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-178">[Download AzCopy][azure-azcopy-download].</span></span>

<span data-ttu-id="1f3b9-179">AzCopy 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-179">The AzCopy syntax is:</span></span>

    AzCopy <Source> <Destination> [filePattern [filePattern...]] [Options]

<span data-ttu-id="1f3b9-180">자세한 내용은 [AzCopy - Azure Blob용 파일 업로드/다운로드][azure-azcopy]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-180">For more information, see [AzCopy - Uploading/Downloading files for Azure Blobs][azure-azcopy].</span></span>

### <span data-ttu-id="1f3b9-181"><a id="commandline"></a>Hadoop 명령줄</span><span class="sxs-lookup"><span data-stu-id="1f3b9-181"><a id="commandline"></a>Hadoop command line</span></span>
<span data-ttu-id="1f3b9-182">데이터가 클러스터 헤드 노드에 존재하는 경우 Hadoop 명령줄은 blob 저장소에 데이터를 저장하는데만 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-182">The Hadoop command line is only useful for storing data into blob storage when the data is already present on the cluster head node.</span></span>

<span data-ttu-id="1f3b9-183">Hadoop 명령을 사용하려면 먼저 다음 방법 중 하나를 사용하여 헤드 노드에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-183">In order to use the Hadoop command, you must first connect to the headnode using one of the following methods:</span></span>

* <span data-ttu-id="1f3b9-184">**Windows 기반 HDInsight**: [원격 데스크톱을 사용하여 연결](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="1f3b9-184">**Windows-based HDInsight**: [Connect using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>
* <span data-ttu-id="1f3b9-185">**Linux 기반 HDInsight**: SSH를 사용하여 연결([SSH 명령](hdinsight-hadoop-linux-use-ssh-unix.md) 또는 [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span><span class="sxs-lookup"><span data-stu-id="1f3b9-185">**Linux-based HDInsight**: Connect using SSH ([the SSH command](hdinsight-hadoop-linux-use-ssh-unix.md) or [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span></span>

<span data-ttu-id="1f3b9-186">연결된 후에 저장소에 파일을 업로드하려면 다음 구문을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-186">Once connected, you can use the following syntax to upload a file to storage.</span></span>

    hadoop -copyFromLocal <localFilePath> <storageFilePath>

<span data-ttu-id="1f3b9-187">위치(예: `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span><span class="sxs-lookup"><span data-stu-id="1f3b9-187">For example, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span></span>

<span data-ttu-id="1f3b9-188">HDInsight의 기본 파일 시스템은 Azure Blob 저장소에 있으므로 /example/datadavinci.txt는 실제로 Azure Blob 저장소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-188">Because the default file system for HDInsight is in Azure Blob storage, /example/data.txt is actually in Azure Blob storage.</span></span> <span data-ttu-id="1f3b9-189">파일이 다음과 같을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-189">You can also refer to the file as:</span></span>

    wasb:///example/data/data.txt

<span data-ttu-id="1f3b9-190">또는</span><span class="sxs-lookup"><span data-stu-id="1f3b9-190">or</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/example/data/davinci.txt

<span data-ttu-id="1f3b9-191">파일과 함께 작동하는 다른 Hadoop 명령의 목록은 [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span><span class="sxs-lookup"><span data-stu-id="1f3b9-191">For a list of other Hadoop commands that work with files, see [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span></span>

> [!WARNING]
> <span data-ttu-id="1f3b9-192">HBase 클러스터에서 데이터 쓰기 시 사용되는 기본 블록 크기는 256KB입니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-192">On HBase clusters, the default block size used when writing data is 256KB.</span></span> <span data-ttu-id="1f3b9-193">HBase API 또는 REST API를 사용할 때는 잘 작동하는 반면 `hadoop` 또는 `hdfs dfs` 명령을 사용하여 12GB를 초과하는 데이터를 기록하면 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-193">While this works fine when using HBase APIs or REST APIs, using the `hadoop` or `hdfs dfs` commands to write data larger than ~12GB results in an error.</span></span> <span data-ttu-id="1f3b9-194">자세한 내용은 아래 [Blob에서 쓰기를 위한 저장소 예외](#storageexception) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-194">See the [storage exception for write on blob](#storageexception) section below for more information.</span></span>
>
>

## <a name="graphical-clients"></a><span data-ttu-id="1f3b9-195">그래픽 클라이언트</span><span class="sxs-lookup"><span data-stu-id="1f3b9-195">Graphical clients</span></span>
<span data-ttu-id="1f3b9-196">Azure 저장소를 사용하기 위한 그래픽 인터페이스를 제공하는 몇몇 응용 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-196">There are also several applications that provide a graphical interface for working with Azure Storage.</span></span> <span data-ttu-id="1f3b9-197">다음은 이러한 응용 프로그램 중 일부의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-197">The following is a list of a few of these applications:</span></span>

| <span data-ttu-id="1f3b9-198">클라이언트</span><span class="sxs-lookup"><span data-stu-id="1f3b9-198">Client</span></span> | <span data-ttu-id="1f3b9-199">Linux</span><span class="sxs-lookup"><span data-stu-id="1f3b9-199">Linux</span></span> | <span data-ttu-id="1f3b9-200">OS X</span><span class="sxs-lookup"><span data-stu-id="1f3b9-200">OS X</span></span> | <span data-ttu-id="1f3b9-201">Windows</span><span class="sxs-lookup"><span data-stu-id="1f3b9-201">Windows</span></span> |
| --- |:---:|:---:|:---:|
| [<span data-ttu-id="1f3b9-202">HDInsight 용 Microsoft Visual Studio Tools</span><span class="sxs-lookup"><span data-stu-id="1f3b9-202">Microsoft Visual Studio Tools for HDInsight</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources) |<span data-ttu-id="1f3b9-203">✔</span><span class="sxs-lookup"><span data-stu-id="1f3b9-203">✔</span></span> |<span data-ttu-id="1f3b9-204">✔</span><span class="sxs-lookup"><span data-stu-id="1f3b9-204">✔</span></span> |<span data-ttu-id="1f3b9-205">✔</span><span class="sxs-lookup"><span data-stu-id="1f3b9-205">✔</span></span> |
| [<span data-ttu-id="1f3b9-206">Azure 저장소 탐색기</span><span class="sxs-lookup"><span data-stu-id="1f3b9-206">Azure Storage Explorer</span></span>](http://storageexplorer.com/) |<span data-ttu-id="1f3b9-207">✔</span><span class="sxs-lookup"><span data-stu-id="1f3b9-207">✔</span></span> |<span data-ttu-id="1f3b9-208">✔</span><span class="sxs-lookup"><span data-stu-id="1f3b9-208">✔</span></span> |<span data-ttu-id="1f3b9-209">✔</span><span class="sxs-lookup"><span data-stu-id="1f3b9-209">✔</span></span> |
| [<span data-ttu-id="1f3b9-210">클라우드 저장소 스튜디오 2</span><span class="sxs-lookup"><span data-stu-id="1f3b9-210">Cloud Storage Studio 2</span></span>](http://www.cerebrata.com/Products/CloudStorageStudio/) | | |<span data-ttu-id="1f3b9-211">✔</span><span class="sxs-lookup"><span data-stu-id="1f3b9-211">✔</span></span> |
| [<span data-ttu-id="1f3b9-212">CloudXplorer</span><span class="sxs-lookup"><span data-stu-id="1f3b9-212">CloudXplorer</span></span>](http://clumsyleaf.com/products/cloudxplorer) | | |<span data-ttu-id="1f3b9-213">✔</span><span class="sxs-lookup"><span data-stu-id="1f3b9-213">✔</span></span> |
| [<span data-ttu-id="1f3b9-214">Azure 탐색기</span><span class="sxs-lookup"><span data-stu-id="1f3b9-214">Azure Explorer</span></span>](http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx) | | |<span data-ttu-id="1f3b9-215">✔</span><span class="sxs-lookup"><span data-stu-id="1f3b9-215">✔</span></span> |
| [<span data-ttu-id="1f3b9-216">Cyberduck</span><span class="sxs-lookup"><span data-stu-id="1f3b9-216">Cyberduck</span></span>](https://cyberduck.io/) | |<span data-ttu-id="1f3b9-217">✔</span><span class="sxs-lookup"><span data-stu-id="1f3b9-217">✔</span></span> |<span data-ttu-id="1f3b9-218">✔</span><span class="sxs-lookup"><span data-stu-id="1f3b9-218">✔</span></span> |

### <a name="visual-studio-tools-for-hdinsight"></a><span data-ttu-id="1f3b9-219">HDInsight 용 Visual Studio Tools</span><span class="sxs-lookup"><span data-stu-id="1f3b9-219">Visual Studio Tools for HDInsight</span></span>
<span data-ttu-id="1f3b9-220">자세한 내용은 [연결된 리소스 탐색](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-220">For more information, see [Navigate the linked resources](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span></span>

### <span data-ttu-id="1f3b9-221"><a id="storageexplorer"></a>Azure 저장소 탐색기</span><span class="sxs-lookup"><span data-stu-id="1f3b9-221"><a id="storageexplorer"></a>Azure Storage Explorer</span></span>
<span data-ttu-id="1f3b9-222">*Azure 저장소 탐색기* 는 Blob의 데이터를 검사하고 변경하는 데 유용한 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-222">*Azure Storage Explorer* is a useful tool for inspecting and altering the data in blobs.</span></span> <span data-ttu-id="1f3b9-223">[http://storageexplorer.com/](http://storageexplorer.com/)에서 다운로드할 수 있는 무료 오픈 소스 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-223">It is a free, open source tool that can be downloaded from [http://storageexplorer.com/](http://storageexplorer.com/).</span></span> <span data-ttu-id="1f3b9-224">소스 코드도 이 링크에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-224">The source code is available from this link as well.</span></span>

<span data-ttu-id="1f3b9-225">이 도구를 사용하기 전에 Azure 저장소 계정 이름과 계정 키를 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-225">Before using the tool, you must know your Azure storage account name and account key.</span></span> <span data-ttu-id="1f3b9-226">더 자세한 정보를 얻을 지침을 보려면 [저장소 계정 생성, 관리 또는 삭제][azure-create-storage-account]에서 "방법: 저장소 액세스 키 보기, 복사 및 다시 생성" 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-226">For instructions about getting this information, see the "How to: View, copy and regenerate storage access keys" section of [Create, manage, or delete a storage account][azure-create-storage-account].</span></span>

1. <span data-ttu-id="1f3b9-227">Azure 저장소 탐색기를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-227">Run Azure Storage Explorer.</span></span> <span data-ttu-id="1f3b9-228">저장소 탐색기를 처음 실행하는 경우 **저장소 계정 이름** 및 **저장소 계정 키**를 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-228">If this is the first time you have run the Storage Explorer, you will be prompted for the **_Storage account name** and **Storage account key**.</span></span> <span data-ttu-id="1f3b9-229">이전에 실행한 적이 있는 경우 **추가** 단추를 사용하여 새 저장소 계정 이름과 키를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-229">If you have run it before, use the **Add** button to add a new storage account name and key.</span></span>

    <span data-ttu-id="1f3b9-230">HDInsight 클러스터에서 사용하는 저장소 계정에 대한 이름과 키를 입력한 다음 **저장 및 열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-230">Enter the name and key for the storage account used by your HDInsight cluster and then select **SAVE & OPEN**.</span></span>

    ![HDI.AzureStorageExplorer][image-azure-storage-explorer]
2. <span data-ttu-id="1f3b9-232">인터페이스 왼쪽의 컨테이너 목록에서 HDInsight 클러스터와 연결된 컨테이너의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-232">In the list of containers to the left of the interface, click the name of the container that is associated with your HDInsight cluster.</span></span> <span data-ttu-id="1f3b9-233">기본적으로 HDInsight 클러스터의 이름이지만 클러스터를 만들 때 특정 이름을 입력한 경우에는 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-233">By default, this is the name of the HDInsight cluster, but may be different if you entered a specific name when creating the cluster.</span></span>
3. <span data-ttu-id="1f3b9-234">도구 모음에서 업로드 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-234">From the tool bar, select the upload icon.</span></span>

    ![업로드 아이콘이 강조 표시된 도구 모음](./media/hdinsight-upload-data/toolbar.png)
4. <span data-ttu-id="1f3b9-236">업로드할 파일을 지정한 다음 **열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-236">Specify a file to upload, and then click **Open**.</span></span> <span data-ttu-id="1f3b9-237">메시지가 표시되면 **업로드** 를 선택하여 저장소 컨테이너의 루트에 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-237">When prompted, select **Upload** to upload the file to the root of the storage container.</span></span> <span data-ttu-id="1f3b9-238">특정 경로에 파일을 업로드하려는 경우 **대상** 필드에서 경로를 입력하고 **업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-238">If you want to upload the file to a specific path, enter the path in the **Destination** field and then select **Upload**.</span></span>

    ![파일 업로드 대화 상자](./media/hdinsight-upload-data/fileupload.png)

    <span data-ttu-id="1f3b9-240">파일 업로드가 완료되면 HDInsight 클러스터의 작업에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-240">Once the file has finished uploading, you can use it from jobs on the HDInsight cluster.</span></span>

## <a name="mount-azure-blob-storage-as-local-drive"></a><span data-ttu-id="1f3b9-241">Azure Blob 저장소를 로컬 드라이브로 탑재</span><span class="sxs-lookup"><span data-stu-id="1f3b9-241">Mount Azure Blob Storage as Local Drive</span></span>
<span data-ttu-id="1f3b9-242">[Azure Blob 저장소를 로컬 드라이브로 탑재](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-242">See [Mount Azure Blob Storage as Local Drive](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span></span>

## <a name="services"></a><span data-ttu-id="1f3b9-243">서비스</span><span class="sxs-lookup"><span data-stu-id="1f3b9-243">Services</span></span>
### <a name="azure-data-factory"></a><span data-ttu-id="1f3b9-244">Azure 데이터 팩터리</span><span class="sxs-lookup"><span data-stu-id="1f3b9-244">Azure Data Factory</span></span>
<span data-ttu-id="1f3b9-245">Azure 데이터 팩터리 서비스는 데이터 저장소, 처리 및 이동 서비스를 효율적이고 확장 가능하며 안정적인 데이터 프로덕션 파이프라인으로 구성하기 위한 완전히 관리되는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-245">The Azure Data Factory service is a fully managed service for composing data storage, data processing, and data movement services into streamlined, scalable, and reliable data production pipelines.</span></span>

<span data-ttu-id="1f3b9-246">Azure 데이터 팩터리를 사용하여 Azure Blob 저장소로 데이터를 이동하거나 Hive 및 Pig와 같은 HDInsight 기능을 직접 사용하는 데이터 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-246">Azure Data Factory can be used to move data into Azure Blob storage, or to create data pipelines that directly use HDInsight features such as Hive and Pig.</span></span>

<span data-ttu-id="1f3b9-247">자세한 내용은 [Azure 데이터 팩터리 설명서](https://azure.microsoft.com/documentation/services/data-factory/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-247">For more information, see the [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/).</span></span>

### <span data-ttu-id="1f3b9-248"><a id="sqoop"></a>Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="1f3b9-248"><a id="sqoop"></a>Apache Sqoop</span></span>
<span data-ttu-id="1f3b9-249">Sqoop은 Hadoop과 관계형 데이터베이스 간 데이터 전송을 위해 설계된 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-249">Sqoop is a tool designed to transfer data between Hadoop and relational databases.</span></span> <span data-ttu-id="1f3b9-250">이 도구를 사용하면 SQL Server, MySQL, Oracle 등의 관계형 데이터베이스 관리 시스템(RDBMS)에서 Hadoop 분산형 파일 시스템(HDFS)으로 데이터를 가져오고, MapReduce 또는 Hive로 Hadoop의 데이터를 변환한 후 데이터를 RDBMS로 다시 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-250">You can use it to import data from a relational database management system (RDBMS), such as SQL Server, MySQL, or Oracle into the Hadoop distributed file system (HDFS), transform the data in Hadoop with MapReduce or Hive, and then export the data back into an RDBMS.</span></span>

<span data-ttu-id="1f3b9-251">자세한 내용은 [HDInsight에서 Sqoop 사용][hdinsight-use-sqoop]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-251">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

## <a name="development-sdks"></a><span data-ttu-id="1f3b9-252">개발 SDK</span><span class="sxs-lookup"><span data-stu-id="1f3b9-252">Development SDKs</span></span>
<span data-ttu-id="1f3b9-253">Azure Blob 저장소는 다음 프로그래밍 언어에서 Azure SDK를 사용하여 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-253">Azure Blob storage can also be accessed using an Azure SDK from the following programming languages:</span></span>

* <span data-ttu-id="1f3b9-254">.NET</span><span class="sxs-lookup"><span data-stu-id="1f3b9-254">.NET</span></span>
* <span data-ttu-id="1f3b9-255">Java</span><span class="sxs-lookup"><span data-stu-id="1f3b9-255">Java</span></span>
* <span data-ttu-id="1f3b9-256">Node.js</span><span class="sxs-lookup"><span data-stu-id="1f3b9-256">Node.js</span></span>
* <span data-ttu-id="1f3b9-257">PHP</span><span class="sxs-lookup"><span data-stu-id="1f3b9-257">PHP</span></span>
* <span data-ttu-id="1f3b9-258">Python</span><span class="sxs-lookup"><span data-stu-id="1f3b9-258">Python</span></span>
* <span data-ttu-id="1f3b9-259">Ruby</span><span class="sxs-lookup"><span data-stu-id="1f3b9-259">Ruby</span></span>

<span data-ttu-id="1f3b9-260">Azure SDK 설치에 대한 자세한 내용은 [Azure 다운로드](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="1f3b9-260">For more information on installing the Azure SDKs, see [Azure downloads](https://azure.microsoft.com/downloads/)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="1f3b9-261">문제 해결</span><span class="sxs-lookup"><span data-stu-id="1f3b9-261">Troubleshooting</span></span>
### <span data-ttu-id="1f3b9-262"><a id="storageexception"></a>Blob에서 쓰기를 위한 저장소 예외</span><span class="sxs-lookup"><span data-stu-id="1f3b9-262"><a id="storageexception"></a>Storage exception for write on blob</span></span>
<span data-ttu-id="1f3b9-263">**증상**: `hadoop` 또는 `hdfs dfs` 명령을 사용하여 HBase 클러스터에12GB를 초과하는 데이터를 기록하면 다음 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-263">**Symptoms**: When using the `hadoop` or `hdfs dfs` commands to write files that are ~12GB or larger on an HBase cluster, you may encounter the following error:</span></span>

    ERROR azure.NativeAzureFileSystem: Encountered Storage Exception for write on Blob : example/test_large_file.bin._COPYING_ Exception details: null Error Code : RequestBodyTooLarge
    copyFromLocal: java.io.IOException
            at com.microsoft.azure.storage.core.Utility.initIOException(Utility.java:661)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:366)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:350)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:471)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
            at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
            at java.lang.Thread.run(Thread.java:745)
    Caused by: com.microsoft.azure.storage.StorageException: The request body is too large and exceeds the maximum permissible limit.
            at com.microsoft.azure.storage.StorageException.translateException(StorageException.java:89)
            at com.microsoft.azure.storage.core.StorageRequest.materializeException(StorageRequest.java:307)
            at com.microsoft.azure.storage.core.ExecutionEngine.executeWithRetry(ExecutionEngine.java:182)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlockInternal(CloudBlockBlob.java:816)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlock(CloudBlockBlob.java:788)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:354)
            ... 7 more

<span data-ttu-id="1f3b9-264">**원인**: HDInsight의 HBase는 Azure 저장소에 쓸 때 기본 블록 크기가 256KB입니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-264">**Cause**: HBase on HDInsight clusters default to a block size of 256KB when writing to Azure storage.</span></span> <span data-ttu-id="1f3b9-265">HBase API 또는 REST API를 사용할 때는 잘 작동하는 반면 `hadoop` 또는 `hdfs dfs` 명령줄 유틸리티를 사용할 때 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-265">While this works for HBase APIs or REST APIs, it will result in an error when using the `hadoop` or `hdfs dfs` command-line utilities.</span></span>

<span data-ttu-id="1f3b9-266">**해결 방법**: `fs.azure.write.request.size`를 사용하여 블록 크기를 더 크기 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-266">**Resolution**: Use `fs.azure.write.request.size` to specify a larger block size.</span></span> <span data-ttu-id="1f3b9-267">`-D` 매개 변수를 사용하여 사용량에 따라 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-267">You can do this on a per-use basis by using the `-D` parameter.</span></span> <span data-ttu-id="1f3b9-268">`hadoop` 명령에서 이 매개 변수를 사용하는 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-268">The following is an example using this parameter with the `hadoop` command:</span></span>

    hadoop -fs -D fs.azure.write.request.size=4194304 -copyFromLocal test_large_file.bin /example/data

<span data-ttu-id="1f3b9-269">Ambari를 사용하여 `fs.azure.write.request.size` 값을 전역적으로 늘릴 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-269">You can also increase the value of `fs.azure.write.request.size` globally by using Ambari.</span></span> <span data-ttu-id="1f3b9-270">다음 단계에 따라 Ambari 웹 UI 값을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-270">The following steps can be used to change the value in the Ambari Web UI:</span></span>

1. <span data-ttu-id="1f3b9-271">브라우저에서 클러스터에 대한 Ambari 웹 UI로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-271">In your browser, go to the Ambari Web UI for your cluster.</span></span> <span data-ttu-id="1f3b9-272">https://CLUSTERNAME.azurehdinsight.net이며, **CLUSTERNAME**은 클러스터 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-272">This is https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your cluster.</span></span>

    <span data-ttu-id="1f3b9-273">메시지가 표시되면 클러스터의 관리자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-273">When prompted, enter the admin name and password for the cluster.</span></span>
2. <span data-ttu-id="1f3b9-274">화면 왼쪽에서 **HDFS**를 선택한 다음 **구성** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-274">From the left side of the screen, select **HDFS**, and then select the **Configs** tab.</span></span>
3. <span data-ttu-id="1f3b9-275">**필터...** 필드에 `fs.azure.write.request.size`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-275">In the **Filter...** field, enter `fs.azure.write.request.size`.</span></span> <span data-ttu-id="1f3b9-276">그러면 페이지 가운데에 필드 및 현재 값이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-276">This will display the field and current value in the middle of the page.</span></span>
4. <span data-ttu-id="1f3b9-277">값을 262144(256KB)에서 새 값으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-277">Change the value from 262144 (256KB) to the new value.</span></span> <span data-ttu-id="1f3b9-278">예를 들면, 4194304(4MB)입니다.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-278">For example, 4194304 (4MB).</span></span>

![Ambari 웹 UI를 통해 값을 변경하는 이미지](./media/hdinsight-upload-data/hbase-change-block-write-size.png)

<span data-ttu-id="1f3b9-280">Ambari 사용에 대한 자세한 내용은 [Ambari 웹 UI를 사용하여 HDInsight 클러스터 관리](hdinsight-hadoop-manage-ambari.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f3b9-280">For more information on using Ambari, see [Manage HDInsight clusters using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f3b9-281">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1f3b9-281">Next steps</span></span>
<span data-ttu-id="1f3b9-282">이제 HDInsight로 데이터를 가져오는 방법을 익혔으니 다음 문서를 읽고 분석을 수행하는 방법을 알아보세요:</span><span class="sxs-lookup"><span data-stu-id="1f3b9-282">Now that you understand how to get data into HDInsight, read the following articles to learn how to perform analysis:</span></span>

* <span data-ttu-id="1f3b9-283">[Azure HDInsight 시작][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="1f3b9-283">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="1f3b9-284">[프로그래밍 방식으로 Hadoop 작업 제출][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="1f3b9-284">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="1f3b9-285">[HDInsight에서 Hive 사용][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="1f3b9-285">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="1f3b9-286">[HDInsight에서 Pig 사용][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="1f3b9-286">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>

[azure-management-portal]: https://porta.azure.com
[azure-powershell]: http://msdn.microsoft.com/library/windowsazure/jj152841.aspx

[azure-storage-client-library]: /develop/net/how-to-guides/blob-storage/
[azure-create-storage-account]:../storage/common/storage-create-storage-account.md
[azure-azcopy-download]:../storage/common/storage-use-azcopy.md
[azure-azcopy]:../storage/common/storage-use-azcopy.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md

[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md

[sqldatabase-create-configure]: ../sql-database-create-configure.md

[apache-sqoop-guide]: http://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[azurecli]: ../cli-install-nodejs.md


[image-azure-storage-explorer]: ./media/hdinsight-upload-data/HDI.AzureStorageExplorer.png
[image-ase-addaccount]: ./media/hdinsight-upload-data/HDI.ASEAddAccount.png
[image-ase-blob]: ./media/hdinsight-upload-data/HDI.ASEBlob.png
