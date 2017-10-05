---
title: "HDInsight에 추가 Azure 저장소 계정 추가 | Microsoft 문서"
description: "기존 HDInsight 클러스터에 추가 Azure 저장소 계정을 추가하는 방법에 대해 알아봅니다."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/04/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 0853e8605e07c28867676e9c13b89263ade67c88
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="add-additional-storage-accounts-to-hdinsight"></a><span data-ttu-id="ccf35-103">HDInsight에 추가 저장소 계정 추가</span><span class="sxs-lookup"><span data-stu-id="ccf35-103">Add additional storage accounts to HDInsight</span></span>

<span data-ttu-id="ccf35-104">스크립트 동작을 사용하여 추가 Azure 저장소 계정을 HDInsight에 추가하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-104">Learn how to use script actions to add additional Azure storage accounts to HDInsight.</span></span> <span data-ttu-id="ccf35-105">이 문서의 단계는 기존 Linux 기반 HDInsight 클러스터에 저장소 계정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-105">The steps in this document add a storage account to an existing Linux-based HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ccf35-106">이 문서의 내용은 클러스터를 만든 후 클러스터에 추가 저장소를 추가하는 방법에 대한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-106">The information in this document is about adding additional storage to a cluster after it has been created.</span></span> <span data-ttu-id="ccf35-107">클러스터를 만드는 동안 저장소 계정을 추가하는 방법에 대한 자세한 내용은 [Hadoop, Spark, Kafka 등으로 HDInsight에서 클러스터를 설정](hdinsight-hadoop-provision-linux-clusters.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ccf35-107">For information on adding storage accounts during cluster creation, see [Set up clusters in HDInsight with Hadoop, Spark, Kafka, and more](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="how-it-works"></a><span data-ttu-id="ccf35-108">작동 방법</span><span class="sxs-lookup"><span data-stu-id="ccf35-108">How it works</span></span>

<span data-ttu-id="ccf35-109">이 스크립트는 다음 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-109">This script takes the following parameters:</span></span>

* <span data-ttu-id="ccf35-110">__Azure 저장소 계정 이름__: HDInsight 클러스터에 추가할 저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-110">__Azure storage account name__: The name of the storage account to add to the HDInsight cluster.</span></span> <span data-ttu-id="ccf35-111">스크립트를 실행한 후 HDInsight에서 이 저장소 계정에 저장된 데이터를 읽고 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-111">After running the script, HDInsight can read and write data stored in this storage account.</span></span>

* <span data-ttu-id="ccf35-112">__Azure 저장소 계정 키__: 저장소 계정에 대한 액세스 권한을 부여하는 키입니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-112">__Azure storage account key__: A key that grants access to the storage account.</span></span>

* <span data-ttu-id="ccf35-113">__-p__(선택 사항): 지정되는 경우 키가 암호화되지 않고 core-site.xml 파일에 일반 텍스트로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-113">__-p__ (optional): If specified, the key is not encrypted and is stored in the core-site.xml file as plain text.</span></span>

<span data-ttu-id="ccf35-114">처리 중에 스크립트는 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-114">During processing, the script performs the following actions:</span></span>

* <span data-ttu-id="ccf35-115">클러스터의 core-site.xml 구성에 저장소 계정이 이미 있는 경우 스크립트가 종료되고 더 이상의 추가 동작이 수행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-115">If the storage account already exists in the core-site.xml configuration for the cluster, the script exits and no further actions are performed.</span></span>

* <span data-ttu-id="ccf35-116">저장소 계정이 있고 키를 사용하여 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-116">Verifies that the storage account exists and can be accessed using the key.</span></span>

* <span data-ttu-id="ccf35-117">클러스터 자격 증명을 사용하여 키를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-117">Encrypts the key using the cluster credential.</span></span>

* <span data-ttu-id="ccf35-118">core-site.xml 파일에 저장소 계정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-118">Adds the storage account to the core-site.xml file.</span></span>

* <span data-ttu-id="ccf35-119">Oozie, YARN, MapReduce2 및 HDFS 서비스를 중지하고 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-119">Stops and restarts the Oozie, YARN, MapReduce2, and HDFS services.</span></span> <span data-ttu-id="ccf35-120">이러한 서비스를 중지하고 시작하면 서비스에서 새 저장소 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-120">Stopping and starting these services allows them to use the new storage account.</span></span>

> [!WARNING]
> <span data-ttu-id="ccf35-121">HDInsight 클러스터와 다른 위치에서는 저장소 계정을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-121">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span>

## <a name="the-script"></a><span data-ttu-id="ccf35-122">스크립트</span><span class="sxs-lookup"><span data-stu-id="ccf35-122">The script</span></span>

<span data-ttu-id="ccf35-123">__스크립트 위치__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="ccf35-123">__Script location__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span></span>

<span data-ttu-id="ccf35-124">__요구 사항__:</span><span class="sxs-lookup"><span data-stu-id="ccf35-124">__Requirements__:</span></span>

* <span data-ttu-id="ccf35-125">스크립트는 __헤드 노드__에 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-125">The script must be applied on the __Head nodes__.</span></span>

## <a name="to-use-the-script"></a><span data-ttu-id="ccf35-126">스크립트 사용</span><span class="sxs-lookup"><span data-stu-id="ccf35-126">To use the script</span></span>

<span data-ttu-id="ccf35-127">Azure Portal, Azure PowerShell 또는 Azure CLI 1.0에서 이 스크립트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-127">This script can be used from the Azure portal, Azure PowerShell, or the Azure CLI 1.0.</span></span> <span data-ttu-id="ccf35-128">자세한 내용은 [스크립트 작업을 사용하여 Linux 기반 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ccf35-128">For more information, see the [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ccf35-129">사용자 지정 문서에 제공된 단계를 사용할 때는 다음 정보를 사용하여 이 스크립트를 적용하세요.</span><span class="sxs-lookup"><span data-stu-id="ccf35-129">When using the steps provided in the customization document, use the following information to apply this script:</span></span>
>
> * <span data-ttu-id="ccf35-130">예제 스크립트 동작 URI를 이 스크립트의 URI(https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-130">Replace any example script action URI with the URI for this script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span></span>
> * <span data-ttu-id="ccf35-131">모든 예제 매개 변수를 Azure 저장소 계정 이름과 클러스터에 추가할 저장소 계정의 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-131">Replace any example parameters with the Azure storage account name and key of the storage account to be added to the cluster.</span></span> <span data-ttu-id="ccf35-132">Azure Portal을 사용하는 경우 이러한 매개 변수는 공백으로 구분되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-132">If using the Azure portal, these parameters must be separated by a space.</span></span>
> * <span data-ttu-id="ccf35-133">클러스터의 Ambari 구성을 직접 업데이트하므로 이 스크립트를 __지속형__으로 표시할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-133">You do not need to mark this script as __Persisted__, as it directly updates the Ambari configuration for the cluster.</span></span>

## <a name="known-issues"></a><span data-ttu-id="ccf35-134">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="ccf35-134">Known issues</span></span>

### <a name="storage-accounts-not-displayed-in-azure-portal-or-tools"></a><span data-ttu-id="ccf35-135">Azure Portal 또는 도구에 저장소 계정이 표시되지 않음</span><span class="sxs-lookup"><span data-stu-id="ccf35-135">Storage accounts not displayed in Azure portal or tools</span></span>

<span data-ttu-id="ccf35-136">Azure Portal에서 HDInsight 클러스터를 볼 때 __속성__에서 __저장소 계정__ 항목을 선택하면 이 스크립트 동작을 통해 추가된 저장소 계정이 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-136">When viewing the HDInsight cluster in the Azure portal, selecting the __Storage Accounts__ entry under __Properties__ does not display storage accounts added through this script action.</span></span> <span data-ttu-id="ccf35-137">Azure PowerShell 및 Azure CLI도 추가 저장소 계정을 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-137">Azure PowerShell and Azure CLI do not display the additional storage account either.</span></span>

<span data-ttu-id="ccf35-138">이 저장소 정보는 스크립트에서 클러스터의 core-site.xml 구성만 수정하기 때문에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-138">The storage information isn't displayed because the script only modifies the core-site.xml configuration for the cluster.</span></span> <span data-ttu-id="ccf35-139">이 정보는 Azure 관리 API를 사용하여 클러스터 정보를 검색할 때 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-139">This information is not used when retrieving the cluster information using Azure management APIs.</span></span>

<span data-ttu-id="ccf35-140">이 스크립트를 사용하여 클러스터에 추가된 저장소 계정 정보를 보려면 Ambari REST API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-140">To view storage account information added to the cluster using this script, use the Ambari REST API.</span></span> <span data-ttu-id="ccf35-141">다음 명령을 사용하여 클러스터에 대한 이 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-141">Use the following commands to retrieve this information for your cluster:</span></span>

```PowerShell
$creds = Get-Credential -UserName "admin" -Message "Enter the cluster login credentials"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties."fs.azure.account.key.$storageAccountName.blob.core.windows.net"
```

> [!NOTE]
> <span data-ttu-id="ccf35-142">`$clusterName`을 HDInsight 클러스터의 이름으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-142">Set `$clusterName` to the name of the HDInsight cluster.</span></span> <span data-ttu-id="ccf35-143">`$storageAccountName`을 저장소 계정의 이름으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-143">Set `$storageAccountName` to the name of the storage account.</span></span> <span data-ttu-id="ccf35-144">메시지가 표시되면 클러스터 로그인(관리자) 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-144">When prompted, enter the cluster login (admin) and password.</span></span>

```Bash
curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.azure.account.key.$STORAGEACCOUNTNAME.blob.core.windows.net"] | select(. != null)'
```

> [!NOTE]
> <span data-ttu-id="ccf35-145">`$PASSWORD`를 클러스터 로그인(관리자) 계정 암호로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-145">Set `$PASSWORD` to the cluster login (admin) account password.</span></span> <span data-ttu-id="ccf35-146">`$CLUSTERNAME`을 HDInsight 클러스터의 이름으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-146">Set `$CLUSTERNAME` to the name of the HDInsight cluster.</span></span> <span data-ttu-id="ccf35-147">`$STORAGEACCOUNTNAME`을 저장소 계정의 이름으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-147">Set `$STORAGEACCOUNTNAME` to the name of the storage account.</span></span>
>
> <span data-ttu-id="ccf35-148">이 예제는 [curl(http://curl.haxx.se/)](http://curl.haxx.se/) 및 [jq(https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/)를 사용하여 JSON 데이터를 검색하고 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-148">This example uses [curl (http://curl.haxx.se/)](http://curl.haxx.se/) and [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) to retrieve and parse JSON data.</span></span>

<span data-ttu-id="ccf35-149">이 명령을 사용할 때는 __CLUSTERNAME__을 HDInsight 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-149">When using this command, replace __CLUSTERNAME__ with the name of the HDInsight cluster.</span></span> <span data-ttu-id="ccf35-150">__PASSWORD__는 클러스터의 HTTP 로그인 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-150">Replace __PASSWORD__ with the HTTP login password for the cluster.</span></span> <span data-ttu-id="ccf35-151">__STORAGEACCOUNT__는 스크립트 동작을 사용하여 추가한 저장소 계정의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-151">Replace __STORAGEACCOUNT__ with the name of the storage account added using script action.</span></span> <span data-ttu-id="ccf35-152">이 명령에서 반환되는 정보는 다음 텍스트와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-152">Information returned from this command appears similar to the following text:</span></span>

    "MIIB+gYJKoZIhvcNAQcDoIIB6zCCAecCAQAxggFaMIIBVgIBADA+MCoxKDAmBgNVBAMTH2RiZW5jcnlwdGlvbi5henVyZWhkaW5zaWdodC5uZXQCEA6GDZMW1oiESKFHFOOEgjcwDQYJKoZIhvcNAQEBBQAEggEATIuO8MJ45KEQAYBQld7WaRkJOWqaCLwFub9zNpscrquA2f3o0emy9Vr6vu5cD3GTt7PmaAF0pvssbKVMf/Z8yRpHmeezSco2y7e9Qd7xJKRLYtRHm80fsjiBHSW9CYkQwxHaOqdR7DBhZyhnj+DHhODsIO2FGM8MxWk4fgBRVO6CZ5eTmZ6KVR8wYbFLi8YZXb7GkUEeSn2PsjrKGiQjtpXw1RAyanCagr5vlg8CicZg1HuhCHWf/RYFWM3EBbVz+uFZPR3BqTgbvBhWYXRJaISwssvxotppe0ikevnEgaBYrflB2P+PVrwPTZ7f36HQcn4ifY1WRJQ4qRaUxdYEfzCBgwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAhRdscgRV3wmYBg3j/T1aEnO3wLWCRpgZa16MWqmfQPuansKHjLwbZjTpeirqUAQpZVyXdK/w4gKlK+t1heNsNo1Wwqu+Y47bSAX1k9Ud7+Ed2oETDI7724IJ213YeGxvu4Ngcf2eHW+FRK"

<span data-ttu-id="ccf35-153">이 텍스트는 저장소 계정에 액세스하는 데 사용되는 암호화된 키의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-153">This text is an example of an encrypted key, which is used to access the storage account.</span></span>

### <a name="unable-to-access-storage-after-changing-key"></a><span data-ttu-id="ccf35-154">키를 변경한 후 저장소에 액세스할 수 없음</span><span class="sxs-lookup"><span data-stu-id="ccf35-154">Unable to access storage after changing key</span></span>

<span data-ttu-id="ccf35-155">저장소 계정의 키를 변경하면 HDInsight에서 더 이상 저장소 계정에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-155">If you change the key for a storage account, HDInsight can no longer access the storage account.</span></span> <span data-ttu-id="ccf35-156">HDInsight에서는 클러스터에 대한 core-site.xml에서 키의 캐시된 복사본을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-156">HDInsight uses a cached copy of key in the core-site.xml for the cluster.</span></span> <span data-ttu-id="ccf35-157">이 캐시된 복사본은 새 키와 일치하도록 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-157">This cached copy must be updated to match the new key.</span></span>

<span data-ttu-id="ccf35-158">스크립트 동작을 다시 실행하면 스크립트에서 저장소 계정에 대한 항목이 이미 있는지 확인하기 때문에 키를 업데이트하지 __않습니다__.</span><span class="sxs-lookup"><span data-stu-id="ccf35-158">Running the script action again does __not__ update the key, as the script checks to see if an entry for the storage account already exists.</span></span> <span data-ttu-id="ccf35-159">항목이 존재하는 경우 변경하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-159">If an entry already exists, it does not make any changes.</span></span>

<span data-ttu-id="ccf35-160">이 문제를 해결하려면 저장소 계정에 대한 기존 항목을 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-160">To work around this problem, you must remove the existing entry for the storage account.</span></span> <span data-ttu-id="ccf35-161">기존 항목을 제거하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-161">Use the following steps to remove the existing entry:</span></span>

1. <span data-ttu-id="ccf35-162">웹 브라우저에서 HDInsight 클러스터에 대한 Ambari 웹 UI를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-162">In a web browser, open the Ambari Web UI for your HDInsight cluster.</span></span> <span data-ttu-id="ccf35-163">URI는 https://CLUSTERNAME.azurehdinsight.net입니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-163">The URI is https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="ccf35-164">__CLUSTERNAME__ 을 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-164">Replace __CLUSTERNAME__ with the name of your cluster.</span></span>

    <span data-ttu-id="ccf35-165">메시지가 표시되면 클러스터에 대한 HTTP 로그인 사용자 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-165">When prompted, enter the HTTP login user and password for your cluster.</span></span>

2. <span data-ttu-id="ccf35-166">페이지 왼쪽의 서비스 목록에서 __HDFS__를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-166">From the list of services on the left of the page, select __HDFS__.</span></span> <span data-ttu-id="ccf35-167">그런 다음 페이지 중앙의 __구성__ 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-167">Then select the __Configs__ tab in the center of the page.</span></span>

3. <span data-ttu-id="ccf35-168">__필터 ...__ 필드에서 __fs.azure.account__의 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-168">In the __Filter...__ field, enter a value of __fs.azure.account__.</span></span> <span data-ttu-id="ccf35-169">이렇게 하면 클러스터에 추가된 추가 저장소 계정에 대한 항목이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-169">This returns entries for any additional storage accounts that have been added to the cluster.</span></span> <span data-ttu-id="ccf35-170">항목에는 두 가지 유형, __keyprovider__와 __key__가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-170">There are two types of entries; __keyprovider__ and __key__.</span></span> <span data-ttu-id="ccf35-171">둘 다 키 이름의 일부로 저장소 계정의 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-171">Both contain the name of the storage account as part of the key name.</span></span>

    <span data-ttu-id="ccf35-172">다음은 __mystorage__라는 저장소 계정의 예제 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-172">The following are example entries for a storage account named __mystorage__:</span></span>

        fs.azure.account.keyprovider.mystorage.blob.core.windows.net
        fs.azure.account.key.mystorage.blob.core.windows.net

4. <span data-ttu-id="ccf35-173">제거해야 하는 저장소 계정의 키를 확인한 후 항목 오른쪽에 있는 '-'(대시) 빨강 아이콘을 사용하여 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-173">After you have identified the keys for the storage account you need to remove, use the red '-' icon to the right of the entry to delete it.</span></span> <span data-ttu-id="ccf35-174">그런 다음 __저장__ 단추를 사용하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-174">Then use the __Save__ button to save your changes.</span></span>

5. <span data-ttu-id="ccf35-175">변경 사항을 저장한 후 스크립트 동작을 사용하여 저장소 계정과 새 키 값을 클러스터에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-175">After changes have been saved, use the script action to add the storage account and new key value to the cluster.</span></span>

### <a name="poor-performance"></a><span data-ttu-id="ccf35-176">성능 저하</span><span class="sxs-lookup"><span data-stu-id="ccf35-176">Poor performance</span></span>

<span data-ttu-id="ccf35-177">저장소 계정이 HDInsight 클러스터와 다른 하위 지역에 있는 경우 성능이 저하될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-177">If the storage account is in a different region than the HDInsight cluster, you may experience poor performance.</span></span> <span data-ttu-id="ccf35-178">다른 하위 지역의 데이터에 액세스하면 하위 지역 Azure 데이터 센터 외부와 공용 인터넷을 통해 네트워크 트래픽이 전송되어 대기 시간이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-178">Accessing data in a different region sends network traffic outside the regional Azure data center and across the public internet, which can introduce latency.</span></span>

> [!WARNING]
> <span data-ttu-id="ccf35-179">HDInsight 클러스터와 다른 지역에서는 저장소 계정을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-179">Using a storage account in a different region than the HDInsight cluster is not supported.</span></span>

### <a name="additional-charges"></a><span data-ttu-id="ccf35-180">추가 요금</span><span class="sxs-lookup"><span data-stu-id="ccf35-180">Additional charges</span></span>

<span data-ttu-id="ccf35-181">저장소 계정이 HDInsight 클러스터와 다른 하위 지역에 있는 경우 Azure 청구에서 추가 송신 요금이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-181">If the storage account is in a different region than the HDInsight cluster, you may notice additional egress charges on your Azure billing.</span></span> <span data-ttu-id="ccf35-182">데이터가 지역 데이터 센터를 떠날 때 송신 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-182">An egress charge is applied when data leaves a regional data center.</span></span> <span data-ttu-id="ccf35-183">트래픽이 다른 하위 지역의 또 다른 Azure 데이터 센터로 전송되는 경우에도 이 요금이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-183">This charge is applied even if the traffic is destined for another Azure data center in a different region.</span></span>

> [!WARNING]
> <span data-ttu-id="ccf35-184">HDInsight 클러스터와 다른 지역에서는 저장소 계정을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-184">Using a storage account in a different region than the HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ccf35-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ccf35-185">Next steps</span></span>

<span data-ttu-id="ccf35-186">기존 HDInsight 클러스터에 추가 저장소 계정을 추가하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="ccf35-186">You have learned how to add additional storage accounts to an existing HDInsight cluster.</span></span> <span data-ttu-id="ccf35-187">스크립트 동작에 대한 자세한 내용은 [스크립트 동작을 사용하여 Linux 기반 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ccf35-187">For more information on script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
