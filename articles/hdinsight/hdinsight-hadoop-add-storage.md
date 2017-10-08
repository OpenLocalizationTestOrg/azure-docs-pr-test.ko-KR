---
title: "aaaAdd 추가 Azure 저장소 계정 tooHDInsight | Microsoft Docs"
description: "어떻게 tooadd 추가 Azure 저장소 계정 tooan 기존 HDInsight 클러스터에 알아봅니다."
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
ms.openlocfilehash: ce5acfa4b61bf7e83b1fb374d64a1eaa3182fbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-additional-storage-accounts-toohdinsight"></a><span data-ttu-id="6ac4a-103">추가 저장소 계정을 tooHDInsight 추가</span><span class="sxs-lookup"><span data-stu-id="6ac4a-103">Add additional storage accounts tooHDInsight</span></span>

<span data-ttu-id="6ac4a-104">Toouse 스크립트 작업 tooadd 추가 Azure 저장소 tooHDInsight를 계정 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-104">Learn how toouse script actions tooadd additional Azure storage accounts tooHDInsight.</span></span> <span data-ttu-id="6ac4a-105">hello이 문서의 단계는 저장소 계정 tooan 기존 Linux 기반 HDInsight 클러스터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-105">hello steps in this document add a storage account tooan existing Linux-based HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6ac4a-106">만든 후에 추가 저장소 tooa 클러스터를 추가 하는 방법에 대 한이 문서의 hello 정보가입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-106">hello information in this document is about adding additional storage tooa cluster after it has been created.</span></span> <span data-ttu-id="6ac4a-107">클러스터를 만드는 동안 저장소 계정을 추가하는 방법에 대한 자세한 내용은 [Hadoop, Spark, Kafka 등으로 HDInsight에서 클러스터를 설정](hdinsight-hadoop-provision-linux-clusters.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-107">For information on adding storage accounts during cluster creation, see [Set up clusters in HDInsight with Hadoop, Spark, Kafka, and more](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="how-it-works"></a><span data-ttu-id="6ac4a-108">작동 방법</span><span class="sxs-lookup"><span data-stu-id="6ac4a-108">How it works</span></span>

<span data-ttu-id="6ac4a-109">이 스크립트는 hello 매개 변수 뒤에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-109">This script takes hello following parameters:</span></span>

* <span data-ttu-id="6ac4a-110">__Azure 저장소 계정 이름__: hello 저장소 계정 tooadd toohello HDInsight 클러스터의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-110">__Azure storage account name__: hello name of hello storage account tooadd toohello HDInsight cluster.</span></span> <span data-ttu-id="6ac4a-111">Hello 스크립트를 실행 한 후 HDInsight 읽고이 저장소 계정에 저장 된 데이터를 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-111">After running hello script, HDInsight can read and write data stored in this storage account.</span></span>

* <span data-ttu-id="6ac4a-112">__Azure 저장소 계정 키__: toohello 저장소 계정 액세스를 부여 하는 키입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-112">__Azure storage account key__: A key that grants access toohello storage account.</span></span>

* <span data-ttu-id="6ac4a-113">__-p__ (선택 사항): 지정을 hello 키 암호화 되지 않은 하 고 일반 텍스트로 hello 코어 site.xml 파일에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-113">__-p__ (optional): If specified, hello key is not encrypted and is stored in hello core-site.xml file as plain text.</span></span>

<span data-ttu-id="6ac4a-114">처리 하는 동안 hello 스크립트 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-114">During processing, hello script performs hello following actions:</span></span>

* <span data-ttu-id="6ac4a-115">Hello 저장소 계정에 이미 있으면 hello 클러스터에 대 한 hello 코어 site.xml 구성 hello 스크립트가 종료 하 고 더 이상 매크로 수행 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-115">If hello storage account already exists in hello core-site.xml configuration for hello cluster, hello script exits and no further actions are performed.</span></span>

* <span data-ttu-id="6ac4a-116">Hello 저장소 계정이 있고 hello 키를 사용 하 여 액세스할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-116">Verifies that hello storage account exists and can be accessed using hello key.</span></span>

* <span data-ttu-id="6ac4a-117">Hello 클러스터 자격 증명을 사용 하 여 hello 키를 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-117">Encrypts hello key using hello cluster credential.</span></span>

* <span data-ttu-id="6ac4a-118">Hello 저장소 계정 toohello site.xml 코어 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-118">Adds hello storage account toohello core-site.xml file.</span></span>

* <span data-ttu-id="6ac4a-119">중지 하 고 hello Oozie, YARN, MapReduce2, 및 HDFS 서비스를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-119">Stops and restarts hello Oozie, YARN, MapReduce2, and HDFS services.</span></span> <span data-ttu-id="6ac4a-120">이러한 서비스를 시작 및 중지 toouse hello 새로운 저장소 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-120">Stopping and starting these services allows them toouse hello new storage account.</span></span>

> [!WARNING]
> <span data-ttu-id="6ac4a-121">저장소 계정을 사용 하 여 hello HDInsight 클러스터와 다른 위치에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-121">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span>

## <a name="hello-script"></a><span data-ttu-id="6ac4a-122">hello 스크립트</span><span class="sxs-lookup"><span data-stu-id="6ac4a-122">hello script</span></span>

<span data-ttu-id="6ac4a-123">__스크립트 위치__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="6ac4a-123">__Script location__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span></span>

<span data-ttu-id="6ac4a-124">__요구 사항__:</span><span class="sxs-lookup"><span data-stu-id="6ac4a-124">__Requirements__:</span></span>

* <span data-ttu-id="6ac4a-125">hello에 hello 스크립트를 적용 해야 __헤드 노드__합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-125">hello script must be applied on hello __Head nodes__.</span></span>

## <a name="toouse-hello-script"></a><span data-ttu-id="6ac4a-126">toouse hello 스크립트</span><span class="sxs-lookup"><span data-stu-id="6ac4a-126">toouse hello script</span></span>

<span data-ttu-id="6ac4a-127">이 스크립트는 Azure PowerShell hello Azure 포털에서에서 사용할 수 있습니다 또는 Azure CLI 1.0 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-127">This script can be used from hello Azure portal, Azure PowerShell, or hello Azure CLI 1.0.</span></span> <span data-ttu-id="6ac4a-128">자세한 내용은 참조 hello [스크립트 동작을 사용 하 여 사용자 지정 하는 Linux 기반 HDInsight 클러스터](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) 문서.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-128">For more information, see hello [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6ac4a-129">Hello 사용자 지정 문서에서 제공 하는 hello 단계를 사용할 때 정보 tooapply 다음 hello이이 스크립트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-129">When using hello steps provided in hello customization document, use hello following information tooapply this script:</span></span>
>
> * <span data-ttu-id="6ac4a-130">이 스크립트 (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)에 대 한 hello URI가 있는 예제 스크립트 동작 URI를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-130">Replace any example script action URI with hello URI for this script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span></span>
> * <span data-ttu-id="6ac4a-131">Hello Azure 저장소 계정 이름과 키 hello 저장소 계정 toobe toohello 추가 된 클러스터의 모든 예에서는 매개 변수 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-131">Replace any example parameters with hello Azure storage account name and key of hello storage account toobe added toohello cluster.</span></span> <span data-ttu-id="6ac4a-132">Azure 포털을 hello를 사용 하 여, 경우 이러한 매개 변수를 공백으로 구분 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-132">If using hello Azure portal, these parameters must be separated by a space.</span></span>
> * <span data-ttu-id="6ac4a-133">이 스크립트도 toomark를 불필요 __Persisted__hello 클러스터에 대 한 hello Ambari 구성을 직접 업데이트 될 때, 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-133">You do not need toomark this script as __Persisted__, as it directly updates hello Ambari configuration for hello cluster.</span></span>

## <a name="known-issues"></a><span data-ttu-id="6ac4a-134">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="6ac4a-134">Known issues</span></span>

### <a name="storage-accounts-not-displayed-in-azure-portal-or-tools"></a><span data-ttu-id="6ac4a-135">Azure Portal 또는 도구에 저장소 계정이 표시되지 않음</span><span class="sxs-lookup"><span data-stu-id="6ac4a-135">Storage accounts not displayed in Azure portal or tools</span></span>

<span data-ttu-id="6ac4a-136">Hello Azure 포털에서에서 보기 hello HDInsight 클러스터를 선택을 선택 하면 hello __저장소 계정은__ 항목 __속성__ 이 스크립트 동작을 통해 추가 된 저장소 계정에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-136">When viewing hello HDInsight cluster in hello Azure portal, selecting hello __Storage Accounts__ entry under __Properties__ does not display storage accounts added through this script action.</span></span> <span data-ttu-id="6ac4a-137">Azure PowerShell 및 Azure CLI 표시 되지 않습니다 hello 추가 저장소 계정 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-137">Azure PowerShell and Azure CLI do not display hello additional storage account either.</span></span>

<span data-ttu-id="6ac4a-138">hello 저장소 정보 hello 스크립트 hello 클러스터에 대 한 hello 코어 site.xml 구성을 수정 하기 때문에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-138">hello storage information isn't displayed because hello script only modifies hello core-site.xml configuration for hello cluster.</span></span> <span data-ttu-id="6ac4a-139">이 정보는 Azure 관리 Api를 사용 하 여 hello 클러스터 정보를 검색할 때 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-139">This information is not used when retrieving hello cluster information using Azure management APIs.</span></span>

<span data-ttu-id="6ac4a-140">tooview 저장소 계정 정보는이 스크립트를 사용 하 여 hello Ambari REST API를 사용 하 여 toohello 클러스터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-140">tooview storage account information added toohello cluster using this script, use hello Ambari REST API.</span></span> <span data-ttu-id="6ac4a-141">클러스터에 대 한 hello 명령을 tooretrieve 다음이 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-141">Use hello following commands tooretrieve this information for your cluster:</span></span>

```PowerShell
$creds = Get-Credential -UserName "admin" -Message "Enter hello cluster login credentials"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties."fs.azure.account.key.$storageAccountName.blob.core.windows.net"
```

> [!NOTE]
> <span data-ttu-id="6ac4a-142">설정 `$clusterName` hello HDInsight 클러스터의 toohello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-142">Set `$clusterName` toohello name of hello HDInsight cluster.</span></span> <span data-ttu-id="6ac4a-143">설정 `$storageAccountName` toohello hello 저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-143">Set `$storageAccountName` toohello name of hello storage account.</span></span> <span data-ttu-id="6ac4a-144">메시지가 표시 되 면 hello 클러스터 로그인 (관리자)과 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-144">When prompted, enter hello cluster login (admin) and password.</span></span>

```Bash
curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.azure.account.key.$STORAGEACCOUNTNAME.blob.core.windows.net"] | select(. != null)'
```

> [!NOTE]
> <span data-ttu-id="6ac4a-145">설정 `$PASSWORD` toohello 클러스터 로그인 (관리자) 계정 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-145">Set `$PASSWORD` toohello cluster login (admin) account password.</span></span> <span data-ttu-id="6ac4a-146">설정 `$CLUSTERNAME` hello HDInsight 클러스터의 toohello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-146">Set `$CLUSTERNAME` toohello name of hello HDInsight cluster.</span></span> <span data-ttu-id="6ac4a-147">설정 `$STORAGEACCOUNTNAME` toohello hello 저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-147">Set `$STORAGEACCOUNTNAME` toohello name of hello storage account.</span></span>
>
> <span data-ttu-id="6ac4a-148">이 예에서는 [curl (http://curl.haxx.se/)](http://curl.haxx.se/) 및 [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) JSON 데이터 tooretrieve 및 구문 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-148">This example uses [curl (http://curl.haxx.se/)](http://curl.haxx.se/) and [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) tooretrieve and parse JSON data.</span></span>

<span data-ttu-id="6ac4a-149">이 명령을 사용 하는 경우 대체 __CLUSTERNAME__ hello HDInsight 클러스터의 hello 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-149">When using this command, replace __CLUSTERNAME__ with hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="6ac4a-150">대체 __암호__ hello 클러스터에 대 한 HTTP hello 로그인 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-150">Replace __PASSWORD__ with hello HTTP login password for hello cluster.</span></span> <span data-ttu-id="6ac4a-151">대체 __STORAGEACCOUNT__ 와 hello hello 저장소 계정의 이름으로 스크립트 동작을 사용 하 여 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-151">Replace __STORAGEACCOUNT__ with hello name of hello storage account added using script action.</span></span> <span data-ttu-id="6ac4a-152">이 명령에서 반환 된 정보는 텍스트 다음 유사한 toohello 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-152">Information returned from this command appears similar toohello following text:</span></span>

    "MIIB+gYJKoZIhvcNAQcDoIIB6zCCAecCAQAxggFaMIIBVgIBADA+MCoxKDAmBgNVBAMTH2RiZW5jcnlwdGlvbi5henVyZWhkaW5zaWdodC5uZXQCEA6GDZMW1oiESKFHFOOEgjcwDQYJKoZIhvcNAQEBBQAEggEATIuO8MJ45KEQAYBQld7WaRkJOWqaCLwFub9zNpscrquA2f3o0emy9Vr6vu5cD3GTt7PmaAF0pvssbKVMf/Z8yRpHmeezSco2y7e9Qd7xJKRLYtRHm80fsjiBHSW9CYkQwxHaOqdR7DBhZyhnj+DHhODsIO2FGM8MxWk4fgBRVO6CZ5eTmZ6KVR8wYbFLi8YZXb7GkUEeSn2PsjrKGiQjtpXw1RAyanCagr5vlg8CicZg1HuhCHWf/RYFWM3EBbVz+uFZPR3BqTgbvBhWYXRJaISwssvxotppe0ikevnEgaBYrflB2P+PVrwPTZ7f36HQcn4ifY1WRJQ4qRaUxdYEfzCBgwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAhRdscgRV3wmYBg3j/T1aEnO3wLWCRpgZa16MWqmfQPuansKHjLwbZjTpeirqUAQpZVyXdK/w4gKlK+t1heNsNo1Wwqu+Y47bSAX1k9Ud7+Ed2oETDI7724IJ213YeGxvu4Ngcf2eHW+FRK"

<span data-ttu-id="6ac4a-153">이 텍스트에 사용 되는 암호화 된 키의 예는 tooaccess hello 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-153">This text is an example of an encrypted key, which is used tooaccess hello storage account.</span></span>

### <a name="unable-tooaccess-storage-after-changing-key"></a><span data-ttu-id="6ac4a-154">없습니다 tooaccess 저장소 키를 변경한 후</span><span class="sxs-lookup"><span data-stu-id="6ac4a-154">Unable tooaccess storage after changing key</span></span>

<span data-ttu-id="6ac4a-155">저장소 계정에 대 한 hello 키를 변경 하면 HDInsight hello 저장소 계정을 더 이상 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-155">If you change hello key for a storage account, HDInsight can no longer access hello storage account.</span></span> <span data-ttu-id="6ac4a-156">HDInsight은 hello 클러스터에 대 한 hello 코어 site.xml에서 키의 캐시 된 복사본을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-156">HDInsight uses a cached copy of key in hello core-site.xml for hello cluster.</span></span> <span data-ttu-id="6ac4a-157">이 캐시 된 복사본에 업데이트 된 toomatch hello에 대 한 새 키 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-157">This cached copy must be updated toomatch hello new key.</span></span>

<span data-ttu-id="6ac4a-158">hello 스크립트 작업을 다시 실행 __하지__ hello 스크립트 hello 저장소 계정에 대 한 항목이 이미 있으면 toosee를 확인 하는 대로 hello 키를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-158">Running hello script action again does __not__ update hello key, as hello script checks toosee if an entry for hello storage account already exists.</span></span> <span data-ttu-id="6ac4a-159">항목이 존재하는 경우 변경하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-159">If an entry already exists, it does not make any changes.</span></span>

<span data-ttu-id="6ac4a-160">이 문제를 해결 toowork, hello 저장소 계정에 대 한 hello 기존 항목을 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-160">toowork around this problem, you must remove hello existing entry for hello storage account.</span></span> <span data-ttu-id="6ac4a-161">다음 단계 tooremove hello 기존 항목 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-161">Use hello following steps tooremove hello existing entry:</span></span>

1. <span data-ttu-id="6ac4a-162">웹 브라우저에서 HDInsight 클러스터에 대 한 hello Ambari 웹 UI를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-162">In a web browser, open hello Ambari Web UI for your HDInsight cluster.</span></span> <span data-ttu-id="6ac4a-163">hello URI https://CLUSTERNAME.azurehdinsight.net입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-163">hello URI is https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="6ac4a-164">대체 __CLUSTERNAME__ 클러스터의 hello 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-164">Replace __CLUSTERNAME__ with hello name of your cluster.</span></span>

    <span data-ttu-id="6ac4a-165">메시지가 표시 되 면 클러스터에 대 한 hello HTTP 로그인 사용자 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-165">When prompted, enter hello HTTP login user and password for your cluster.</span></span>

2. <span data-ttu-id="6ac4a-166">Hello hello hello 페이지 왼쪽에 있는 서비스 목록에서 선택 __HDFS__합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-166">From hello list of services on hello left of hello page, select __HDFS__.</span></span> <span data-ttu-id="6ac4a-167">다음 hello 선택 __Configs__ hello 센터 hello 페이지의 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-167">Then select hello __Configs__ tab in hello center of hello page.</span></span>

3. <span data-ttu-id="6ac4a-168">Hello에 __필터...__  필드의 값을 입력 합니다. __fs.azure.account__합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-168">In hello __Filter...__ field, enter a value of __fs.azure.account__.</span></span> <span data-ttu-id="6ac4a-169">Toohello 클러스터에 추가 된 모든 추가 저장소 계정에 대 한 항목을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-169">This returns entries for any additional storage accounts that have been added toohello cluster.</span></span> <span data-ttu-id="6ac4a-170">항목에는 두 가지 유형, __keyprovider__와 __key__가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-170">There are two types of entries; __keyprovider__ and __key__.</span></span> <span data-ttu-id="6ac4a-171">둘 다 hello 키 이름의 일부로 hello 저장소 계정의 hello 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-171">Both contain hello name of hello storage account as part of hello key name.</span></span>

    <span data-ttu-id="6ac4a-172">hello 다음은 라는 저장소 계정에 대 한 예제 항목 __mystorage__:</span><span class="sxs-lookup"><span data-stu-id="6ac4a-172">hello following are example entries for a storage account named __mystorage__:</span></span>

        fs.azure.account.keyprovider.mystorage.blob.core.windows.net
        fs.azure.account.key.mystorage.blob.core.windows.net

4. <span data-ttu-id="6ac4a-173">Tooremove 필요한 hello 저장소 계정에 대 한 hello 키를 식별 한 후 사용 하 여 hello 빨간색 '-' hello 항목 toodelete의 오른쪽 아이콘 toohello 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-173">After you have identified hello keys for hello storage account you need tooremove, use hello red '-' icon toohello right of hello entry toodelete it.</span></span> <span data-ttu-id="6ac4a-174">다음 hello를 사용 하 여 __저장__ toosave 변경 내용을 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-174">Then use hello __Save__ button toosave your changes.</span></span>

5. <span data-ttu-id="6ac4a-175">변경 내용을 저장 한 후 hello 스크립트 작업 tooadd hello 저장소 계정 및 새 키 값 toohello 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-175">After changes have been saved, use hello script action tooadd hello storage account and new key value toohello cluster.</span></span>

### <a name="poor-performance"></a><span data-ttu-id="6ac4a-176">성능 저하</span><span class="sxs-lookup"><span data-stu-id="6ac4a-176">Poor performance</span></span>

<span data-ttu-id="6ac4a-177">저장소 계정 hello hello HDInsight 클러스터와 다른 지역에 있으면 성능이 저하를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-177">If hello storage account is in a different region than hello HDInsight cluster, you may experience poor performance.</span></span> <span data-ttu-id="6ac4a-178">다른 지역 보냅니다 네트워크 트래픽이 hello 지역의 Azure 데이터 센터 외부와 across 데이터 액세스 hello 공용 인터넷을 지연이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-178">Accessing data in a different region sends network traffic outside hello regional Azure data center and across hello public internet, which can introduce latency.</span></span>

> [!WARNING]
> <span data-ttu-id="6ac4a-179">Hello HDInsight 클러스터와 다른 지역에서 저장소 계정을 사용 하는 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-179">Using a storage account in a different region than hello HDInsight cluster is not supported.</span></span>

### <a name="additional-charges"></a><span data-ttu-id="6ac4a-180">추가 요금</span><span class="sxs-lookup"><span data-stu-id="6ac4a-180">Additional charges</span></span>

<span data-ttu-id="6ac4a-181">이면 hello 저장소 계정이 다른 지역에 HDInsight 클러스터를 hello 보다 사용자 Azure 청구에 추가 전송 요금을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-181">If hello storage account is in a different region than hello HDInsight cluster, you may notice additional egress charges on your Azure billing.</span></span> <span data-ttu-id="6ac4a-182">데이터가 지역 데이터 센터를 떠날 때 송신 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-182">An egress charge is applied when data leaves a regional data center.</span></span> <span data-ttu-id="6ac4a-183">대금이 청구는 다른 지역에 있는 다른 Azure 데이터 센터에 대 한 hello 트래픽을 전송 하는 경우에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-183">This charge is applied even if hello traffic is destined for another Azure data center in a different region.</span></span>

> [!WARNING]
> <span data-ttu-id="6ac4a-184">Hello HDInsight 클러스터와 다른 지역에서 저장소 계정을 사용 하는 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-184">Using a storage account in a different region than hello HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ac4a-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6ac4a-185">Next steps</span></span>

<span data-ttu-id="6ac4a-186">추가 저장소 tooadd tooan 기존 HDInsight 클러스터를 계정 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-186">You have learned how tooadd additional storage accounts tooan existing HDInsight cluster.</span></span> <span data-ttu-id="6ac4a-187">스크립트 동작에 대한 자세한 내용은 [스크립트 동작을 사용하여 Linux 기반 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6ac4a-187">For more information on script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
