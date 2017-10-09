---
title: "Azure 저장소와 Azure CLI 2.0 aaaUsing hello | Microsoft Docs"
description: "Toouse를 Azure CLI (명령줄 인터페이스 Azure) 2.0으로 Azure 저장소 toocreate hello 및 저장소 계정 관리 및 Azure blob와 파일을 작동 방법에 대해 알아봅니다. hello Azure CLI 2.0에는 Python로 작성 된 플랫폼 간 도구입니다."
services: storage
documentationcenter: na
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 06/02/2017
ms.author: marsma
ms.openlocfilehash: 14e6eb0c913676380c90a72563276245e7f08aa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-20-with-azure-storage"></a><span data-ttu-id="d695c-104">Hello Azure CLI 2.0을 사용 하 여 Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="d695c-104">Using hello Azure CLI 2.0 with Azure Storage</span></span>

<span data-ttu-id="d695c-105">hello 오픈 소스 플랫폼 간 Azure CLI 2.0 hello Azure 플랫폼을 사용 하기 위한 명령 집합을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-105">hello open-source, cross-platform Azure CLI 2.0 provides a set of commands for working with hello Azure platform.</span></span> <span data-ttu-id="d695c-106">Hello hello에 있는 동일한 기능을 많이 제공 [Azure 포털](https://portal.azure.com), 다양 한 데이터 액세스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-106">It provides much of hello same functionality found in hello [Azure portal](https://portal.azure.com), including rich data access.</span></span>

<span data-ttu-id="d695c-107">이 가이드에서는 보여줍니다 어떻게 toouse hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform Azure 저장소 계정에 리소스를 사용 하는 몇 가지 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-107">In this guide, we show you how toouse hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform several tasks working with resources in your Azure Storage account.</span></span> <span data-ttu-id="d695c-108">다운로드 및 설치 하거나 업그레이드 toohello 최신 버전의 hello CLI 2.0이이 가이드를 사용 하기 전에 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-108">We recommend that you download and install or upgrade toohello latest version of hello CLI 2.0 before using this guide.</span></span>

<span data-ttu-id="d695c-109">hello 가이드의 hello 예 hello ubuntu, Bash 셸의 hello 사용 가정 하지만 다른 플랫폼과 마찬가지로 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-109">hello examples in hello guide assume hello use of hello Bash shell on Ubuntu, but other platforms should perform similarly.</span></span> 

[!INCLUDE [storage-cli-versions](../../../includes/storage-cli-versions.md)]

## <a name="prerequisites"></a><span data-ttu-id="d695c-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d695c-110">Prerequisites</span></span>
<span data-ttu-id="d695c-111">이 가이드 hello Azure 저장소의 기본 개념을 이해 해야 하는 것으로 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-111">This guide assumes that you understand hello basic concepts of Azure Storage.</span></span> <span data-ttu-id="d695c-112">또한 Azure와 hello 저장소 서비스에 대 한 아래 지정 된 수 toosatisfy hello 계정 만들기 요구 하 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-112">It also assumes that you're able toosatisfy hello account creation requirements that are specified below for Azure and hello Storage service.</span></span>

### <a name="accounts"></a><span data-ttu-id="d695c-113">계정</span><span class="sxs-lookup"><span data-stu-id="d695c-113">Accounts</span></span>
* <span data-ttu-id="d695c-114">**Azure 계정**: Azure 구독이 아직 없는 경우 [무료 Azure 계정을 만듭니다](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="d695c-114">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="d695c-115">**Storage 계정**: [Azure Storage 계정 정보](storage-create-storage-account.md)의 [저장소 계정 만들기](storage-create-storage-account.md#create-a-storage-account) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d695c-115">**Storage account**: See [Create a storage account](storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](storage-create-storage-account.md).</span></span>

### <a name="install-hello-azure-cli-20"></a><span data-ttu-id="d695c-116">Hello Azure CLI 2.0를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-116">Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="d695c-117">에 설명 된 hello 지침에 따라 hello Azure CLI 2.0을 설치 및 다운로드 [Azure CLI 2.0 설치](/cli/azure/install-az-cli2)합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-117">Download and install hello Azure CLI 2.0 by following hello instructions outlined in [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

> [!TIP]
> <span data-ttu-id="d695c-118">Hello 설치에 문제가 있는 경우 체크 아웃 hello [설치 문제 해결](/cli/azure/install-az-cli2#installation-troubleshooting) hello 아티클과 hello 섹션 [설치 문제 해결](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) GitHub에 대 한 가이드입니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-118">If you have trouble with hello installation, check out hello [Installation Troubleshooting](/cli/azure/install-az-cli2#installation-troubleshooting) section of hello article, and hello [Install Troubleshooting](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) guide on GitHub.</span></span>
>

## <a name="working-with-hello-cli"></a><span data-ttu-id="d695c-119">CLI hello 사용</span><span class="sxs-lookup"><span data-stu-id="d695c-119">Working with hello CLI</span></span>

<span data-ttu-id="d695c-120">Hello CLI를 설치 했으므로 사용 하 여 hello `az` 명령줄 인터페이스 (예: Bash, 터미널, 명령 프롬프트) tooaccess hello Azure CLI 명령에서는 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-120">Once you've installed hello CLI, you can use hello `az` command in your command-line interface (Bash, Terminal, Command Prompt) tooaccess hello Azure CLI commands.</span></span> <span data-ttu-id="d695c-121">형식 hello `az` 명령 toosee 전체 hello 기본 명령 (다음 예제 출력 hello 잘립니다) 목록이:</span><span class="sxs-lookup"><span data-stu-id="d695c-121">Type hello `az` command toosee a full list of hello base commands (hello following example output has been truncated):</span></span>

```
     /\
    /  \    _____   _ _ __ ___
   / /\ \  |_  / | | | \'__/ _ \
  / ____ \  / /| |_| | | |  __/
 /_/    \_\/___|\__,_|_|  \___|


Welcome toohello cool new Azure CLI!

Here are hello base commands:

    account          : Manage subscriptions.
    acr              : Manage Azure container registries.
    acs              : Manage Azure Container Services.
    ad               : Synchronize on-premises directories and manage Azure Active Directory
                       resources.
    ...
```

<span data-ttu-id="d695c-122">Hello 명령을 실행 하면 명령줄 인터페이스에서 `az storage --help` toolist hello `storage` 하위 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-122">In your command-line interface, execute hello command `az storage --help` toolist hello `storage` command subgroups.</span></span> <span data-ttu-id="d695c-123">저장소 리소스를 사용 하는 것에 대 한 Azure CLI 제공 hello 기능 hello의 개요를 제공 하는 hello hello 하위 그룹에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-123">hello descriptions of hello subgroups provide an overview of hello functionality hello Azure CLI provides for working with your storage resources.</span></span>

```
Group
    az storage: Durable, highly available, and massively scalable cloud storage.

Subgroups:
    account  : Manage storage accounts.
    blob     : Object storage for unstructured data.
    container: Manage blob storage containers.
    cors     : Manage Storage service Cross-Origin Resource Sharing (CORS).
    directory: Manage file storage directories.
    entity   : Manage table storage entities.
    file     : File shares that use hello standard SMB 3.0 protocol.
    logging  : Manage Storage service logging information.
    message  : Manage queue storage messages.
    metrics  : Manage Storage service metrics.
    queue    : Use queues tooeffectively scale applications according tootraffic.
    share    : Manage file shares.
    table    : NoSQL key-value storage using semi-structured datasets.
```

## <a name="connect-hello-cli-tooyour-azure-subscription"></a><span data-ttu-id="d695c-124">Hello CLI tooyour Azure 구독 연결</span><span class="sxs-lookup"><span data-stu-id="d695c-124">Connect hello CLI tooyour Azure subscription</span></span>

<span data-ttu-id="d695c-125">Azure 구독에 있는 hello 리소스와 toowork, 먼저 로그인 해야 tooyour 된 Azure 계정 `az login`합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-125">toowork with hello resources in your Azure subscription, you must first log in tooyour Azure account with `az login`.</span></span> <span data-ttu-id="d695c-126">로그인할 수 있는 몇 가지 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-126">There are several ways you can log in:</span></span>

* <span data-ttu-id="d695c-127">**대화형 로그인**: `az login`</span><span class="sxs-lookup"><span data-stu-id="d695c-127">**Interactive login**: `az login`</span></span>
* <span data-ttu-id="d695c-128">**사용자 이름 및 암호로 로그인**: `az login -u johndoe@contoso.com -p VerySecret`</span><span class="sxs-lookup"><span data-stu-id="d695c-128">**Log in with user name and password**: `az login -u johndoe@contoso.com -p VerySecret`</span></span>
  * <span data-ttu-id="d695c-129">Microsoft 계정 또는 다단계 인증을 사용하는 계정에서는 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-129">This doesn't work with Microsoft accounts or accounts that use multi-factor authentication.</span></span>
* <span data-ttu-id="d695c-130">**서비스 주체로 로그인**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="d695c-130">**Log in with a service principal**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span></span>

## <a name="azure-cli-20-sample-script"></a><span data-ttu-id="d695c-131">Azure CLI 2.0 샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="d695c-131">Azure CLI 2.0 sample script</span></span>

<span data-ttu-id="d695c-132">다음으로, Azure 저장소 리소스와 몇 가지 기본 Azure CLI 2.0 명령을 toointeract 발급 하는 작은 셸 스크립트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-132">Next, we'll work with a small shell script that issues a few basic Azure CLI 2.0 commands toointeract with Azure Storage resources.</span></span> <span data-ttu-id="d695c-133">hello 스크립트는 먼저 저장소 계정에 새 컨테이너를 만듦 다음 기존 toothat 컨테이너 (blob)으로 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-133">hello script first creates a new container in your storage account, then uploads an existing file (as a blob) toothat container.</span></span> <span data-ttu-id="d695c-134">그런 다음 hello 컨테이너의 모든 blob을 나열 하 고 마지막으로 hello 파일 tooa 대상을 지정 하는 로컬 컴퓨터에 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-134">It then lists all blobs in hello container, and finally, downloads hello file tooa destination on your local computer that you specify.</span></span>

```bash
#!/bin/bash
# A simple Azure Storage example script

export AZURE_STORAGE_ACCOUNT=<storage_account_name>
export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

export container_name=<container_name>
export blob_name=<blob_name>
export file_to_upload=<file_to_upload>
export destination_file=<destination_file>

echo "Creating hello container..."
az storage container create --name $container_name

echo "Uploading hello file..."
az storage blob upload --container-name $container_name --file $file_to_upload --name $blob_name

echo "Listing hello blobs..."
az storage blob list --container-name $container_name --output table

echo "Downloading hello file..."
az storage blob download --container-name $container_name --name $blob_name --file $destination_file --output table

echo "Done"
```

<span data-ttu-id="d695c-135">**구성 하 고 hello 스크립트를 실행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d695c-135">**Configure and run hello script**</span></span>

1. <span data-ttu-id="d695c-136">원하는 텍스트 편집기, 다음 열고 복사 hello 스크립트 앞에 오는 hello 편집기에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-136">Open your favorite text editor, then copy and paste hello preceding script into hello editor.</span></span>

2. <span data-ttu-id="d695c-137">다음으로 hello 스크립트의 변수 tooreflect 구성 설정을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-137">Next, update hello script's variables tooreflect your configuration settings.</span></span> <span data-ttu-id="d695c-138">Hello를 다음 지정 된 대로 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-138">Replace hello following values as specified:</span></span>

   * <span data-ttu-id="d695c-139">**\<storage_account_name\>**  hello 사용자의 저장소 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-139">**\<storage_account_name\>** hello name of your storage account.</span></span>
   * <span data-ttu-id="d695c-140">**\<storage_account_key\>**  저장소 계정에 대 한 hello 기본 또는 보조 액세스 키입니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-140">**\<storage_account_key\>** hello primary or secondary access key for your storage account.</span></span>
   * <span data-ttu-id="d695c-141">**\<container_name\>**  이름을 "azure cli-샘플-컨테이너"와 같은 새 컨테이너 toocreate hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-141">**\<container_name\>** A name hello new container toocreate, such as "azure-cli-sample-container".</span></span>
   * <span data-ttu-id="d695c-142">**\<blob_name\>**  hello 컨테이너에서 hello 대상 blob에 대 한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-142">**\<blob_name\>** A name for hello destination blob in hello container.</span></span>
   * <span data-ttu-id="d695c-143">**\<file_to_upload\>**  로컬 컴퓨터에 toosmall 파일 경로 같은 hello "~ / images/HelloWorld.png"입니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-143">**\<file_to_upload\>** hello path toosmall file on your local computer, such as "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="d695c-144">**\<destination_file\>**  대상 파일 경로 같은 hello "~ / downloadedImage.png"입니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-144">**\<destination_file\>** hello destination file path, such as "~/downloadedImage.png".</span></span>

3. <span data-ttu-id="d695c-145">Hello 필요한 변수를 업데이트 한 후 hello 스크립트를 저장 하 고 편집기를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-145">After you've updated hello necessary variables, save hello script and exit your editor.</span></span> <span data-ttu-id="d695c-146">스크립트 이름을 지정한 다음 단계 hello 가정 **my_storage_sample.sh**합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-146">hello next steps assume you've named your script **my_storage_sample.sh**.</span></span>

4. <span data-ttu-id="d695c-147">필요한 경우 hello 스크립트 실행으로 표시 합니다.`chmod +x my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="d695c-147">Mark hello script as executable, if necessary: `chmod +x my_storage_sample.sh`</span></span>

5. <span data-ttu-id="d695c-148">Hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-148">Execute hello script.</span></span> <span data-ttu-id="d695c-149">예를 들어 Bash에서는 `./my_storage_sample.sh`입니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-149">For example, in Bash: `./my_storage_sample.sh`</span></span>

<span data-ttu-id="d695c-150">출력 유사한 toohello 다음을 참조 하 고 hello 해야  **\<destination_file\>**  hello에 지정 된 스크립트는 로컬 컴퓨터에 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-150">You should see output similar toohello following, and hello **\<destination_file\>** you specified in hello script should appear on your local computer.</span></span>

```
Creating hello container...
{
  "created": true
}
Uploading hello file...
Percent complete: %100.0
Listing hello blobs...
Name       Blob Type      Length  Content Type              Last Modified
---------  -----------  --------  ------------------------  -------------------------
README.md  BlockBlob        6700  application/octet-stream  2017-05-12T20:54:59+00:00
Downloading hello file...
Name
---------
README.md
Done
```

> [!TIP]
> <span data-ttu-id="d695c-151">hello 위의 출력은 **테이블** 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-151">hello preceding output is in **table** format.</span></span> <span data-ttu-id="d695c-152">그러면 형식 toouse hello를 지정 하 여 출력을 지정할 수 있습니다 `--output` 인수 CLI 명령에서는 전역적으로 사용 하 여 설정 하거나 `az configure`합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-152">You can specify which output format toouse by specifying hello `--output` argument in your CLI commands, or set it globally using `az configure`.</span></span>
>

## <a name="manage-storage-accounts"></a><span data-ttu-id="d695c-153">저장소 계정 관리</span><span class="sxs-lookup"><span data-stu-id="d695c-153">Manage storage accounts</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="d695c-154">새 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="d695c-154">Create a new storage account</span></span>
<span data-ttu-id="d695c-155">Azure 저장소 toouse 저장소 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-155">toouse Azure Storage, you need a storage account.</span></span> <span data-ttu-id="d695c-156">컴퓨터를 너무 구성한 후 새 Azure 저장소 계정을 만들 수 있습니다[tooyour 구독 연결](#connect-to-your-azure-subscription)합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-156">You can create a new Azure Storage account after you've configured your computer too[connect tooyour subscription](#connect-to-your-azure-subscription).</span></span>

```azurecli
az storage account create \
    --location <location> \
    --name <account_name> \
    --resource-group <resource_group> \
    --sku <account_sku>
```

* <span data-ttu-id="d695c-157">`--location`[필수]: 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-157">`--location` [Required]: Location.</span></span> <span data-ttu-id="d695c-158">예를 들어 "미국 서부"를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-158">For example, "West US".</span></span>
* <span data-ttu-id="d695c-159">`--name`[필수]: hello 저장소 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-159">`--name` [Required]: hello storage account name.</span></span> <span data-ttu-id="d695c-160">hello 이름은 길이가 3 too24 자가 하 여야 하 고 소문자 영숫자 문자만 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-160">hello name must be 3 too24 characters in length, and use only lowercase alphanumeric characters.</span></span>
* <span data-ttu-id="d695c-161">`--resource-group`[필수]: 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-161">`--resource-group` [Required]: Name of resource group.</span></span>
* <span data-ttu-id="d695c-162">`--sku`[필수]: 저장소 계정 SKU hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-162">`--sku` [Required]: hello storage account SKU.</span></span> <span data-ttu-id="d695c-163">허용되는 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-163">Allowed values:</span></span>
  * `Premium_LRS`
  * `Standard_GRS`
  * `Standard_LRS`
  * `Standard_RAGRS`
  * `Standard_ZRS`

### <a name="set-default-azure-storage-account-environment-variables"></a><span data-ttu-id="d695c-164">기본 Azure Storage 계정 환경 변수 설정</span><span class="sxs-lookup"><span data-stu-id="d695c-164">Set default Azure storage account environment variables</span></span>
<span data-ttu-id="d695c-165">Azure 구독에서 여러 저장소 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-165">You can have multiple storage accounts in your Azure subscription.</span></span> <span data-ttu-id="d695c-166">그 중 하나가 tooselect toouse 모든 후속 저장소에 대 한 명령을 이러한 환경 변수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-166">tooselect one of them toouse for all subsequent storage commands, you can set these environment variables:</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="d695c-167">또 다른 방법은 tooset 기본 저장소 계정 연결 문자열을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-167">Another way tooset a default storage account is by using a connection string.</span></span> <span data-ttu-id="d695c-168">첫째, hello로 hello 연결 문자열을 가져올 `show-connection-string` 명령:</span><span class="sxs-lookup"><span data-stu-id="d695c-168">First, get hello connection string with hello `show-connection-string` command:</span></span>

```azurecli
az storage account show-connection-string \
    --name <account_name> \
    --resource-group <resource_group>
```

<span data-ttu-id="d695c-169">그런 다음 복사본 hello 연결 문자열을 출력 하 고 hello 설정 `AZURE_STORAGE_CONNECTION_STRING` 환경 변수 (따옴표로 tooenclose hello 연결 문자열을 할 수 있음):</span><span class="sxs-lookup"><span data-stu-id="d695c-169">Then copy hello output connection string and set hello `AZURE_STORAGE_CONNECTION_STRING` environment variable (you might need tooenclose hello connection string in quotes):</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING="<connection_string>"
```

> [!NOTE]
> <span data-ttu-id="d695c-170">모든 예제에서는 다음이 문서의 섹션 hello hello를 설정 하는 것으로 가정 `AZURE_STORAGE_ACCOUNT` 및 `AZURE_STORAGE_ACCESS_KEY` 환경 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-170">All examples in hello following sections of this article assume that you've set hello `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY` environment variables.</span></span>
>

## <a name="create-and-manage-blobs"></a><span data-ttu-id="d695c-171">Blob 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="d695c-171">Create and manage blobs</span></span>
<span data-ttu-id="d695c-172">Azure Blob 저장소는 많은 양의 텍스트 또는 이진 데이터를 액세스할 수 있는에서 아무 곳 이나 HTTP 또는 HTTPS를 통해 hello world에 같은 구조화 되지 않은 데이터를 저장 하기 위한 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-172">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="d695c-173">이 섹션에서는 Azure Blob 저장소 개념에 이미 익숙하다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-173">This section assumes that you are already familiar with Azure Blob storage concepts.</span></span> <span data-ttu-id="d695c-174">자세한 내용은 [.NET을 사용하여 Azure Blob Storage 시작](../blobs/storage-dotnet-how-to-use-blobs.md) 및 [Blob Service 개념](/rest/api/storageservices/blob-service-concepts)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d695c-174">For detailed information, see [Get started with Azure Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](/rest/api/storageservices/blob-service-concepts).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="d695c-175">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="d695c-175">Create a container</span></span>
<span data-ttu-id="d695c-176">Azure 저장소의 모든 Blob은 컨테이너에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-176">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="d695c-177">Hello를 사용 하 여 컨테이너를 만들 수 `az storage container create` 명령:</span><span class="sxs-lookup"><span data-stu-id="d695c-177">You can create a container by using hello `az storage container create` command:</span></span>

```azurecli
az storage container create --name <container_name>
```

<span data-ttu-id="d695c-178">설정할 수 있습니다 읽기 액세스의 세 가지 수준 중 하나를 새 컨테이너에 대 한 선택적 hello를 지정 하 여 `--public-access` 인수:</span><span class="sxs-lookup"><span data-stu-id="d695c-178">You can set one of three levels of read access for a new container by specifying hello optional  `--public-access` argument:</span></span>

* <span data-ttu-id="d695c-179">`off`(기본값): 컨테이너 데이터는 개인 toohello 계정 소유자입니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-179">`off` (default): Container data is private toohello account owner.</span></span>
* <span data-ttu-id="d695c-180">`blob`: Blob에 대한 공용 읽기 액세스입니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-180">`blob`: Public read access for blobs.</span></span>
* <span data-ttu-id="d695c-181">`container`: 공용 읽기 및 목록 toohello 전체 컨테이너에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-181">`container`: Public read and list access toohello entire container.</span></span>

<span data-ttu-id="d695c-182">자세한 내용은 참조 [익명 읽기 권한을 toocontainers 및 blob 관리](../blobs/storage-manage-access-to-resources.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-182">For more information, see [Manage anonymous read access toocontainers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>

### <a name="upload-a-blob-tooa-container"></a><span data-ttu-id="d695c-183">Blob tooa 컨테이너를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-183">Upload a blob tooa container</span></span>
<span data-ttu-id="d695c-184">Azure Blob 저장소는 블록 Blob, 추가 Blob 및 페이지 Blob을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-184">Azure Blob storage supports block, append, and page blobs.</span></span> <span data-ttu-id="d695c-185">업로드 hello를 사용 하 여 tooa 컨테이너 blob `blob upload` 명령:</span><span class="sxs-lookup"><span data-stu-id="d695c-185">Upload blobs tooa container by using hello `blob upload` command:</span></span>

```azurecli
az storage blob upload \
    --file <local_file_path> \
    --container-name <container_name> \
    --name <blob_name>
```

 <span data-ttu-id="d695c-186">기본적으로 hello `blob upload` 명령 *.vhd 파일 toopage blob 또는 그렇지 않으면 블록 blob을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-186">By default, hello `blob upload` command uploads *.vhd files toopage blobs, or block blobs otherwise.</span></span> <span data-ttu-id="d695c-187">toospecify 다른 유형에 사용할 blob 업로드, hello를 사용할 수 있습니다 `--type` 인수-허용 되는 값은 `append`, `block`, 및 `page`합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-187">toospecify another type when you upload a blob, you can use hello `--type` argument--allowed values are `append`, `block`, and `page`.</span></span>

 <span data-ttu-id="d695c-188">Hello 다른 blob 형식에 대 한 자세한 내용은 참조 하십시오. [이해 블록 Blob, 추가 Blob 및 페이지 Blob](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs)합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-188">For more information on hello different blob types, see [Understanding Block Blobs, Append Blobs, and Page Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span></span>


### <a name="download-a-blob-from-a-container"></a><span data-ttu-id="d695c-189">컨테이너에서 Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="d695c-189">Download a blob from a container</span></span>
<span data-ttu-id="d695c-190">이 예제에서는 어떻게 toodownload 컨테이너에서 blob:</span><span class="sxs-lookup"><span data-stu-id="d695c-190">This example demonstrates how toodownload a blob from a container:</span></span>

```azurecli
az storage blob download \
    --container-name mycontainer \
    --name myblob.png \
    --file ~/mydownloadedblob.png
```

### <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="d695c-191">컨테이너에서 hello blob 나열</span><span class="sxs-lookup"><span data-stu-id="d695c-191">List hello blobs in a container</span></span>

<span data-ttu-id="d695c-192">Hello 사용 하 여 컨테이너에서 hello blob 나열 [az 저장소 blob 목록](/cli/azure/storage/blob#list) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-192">List hello blobs in a container with hello [az storage blob list](/cli/azure/storage/blob#list) command.</span></span>

```azurecli
az storage blob list \
    --container-name mycontainer \
    --output table
```

### <a name="copy-blobs"></a><span data-ttu-id="d695c-193">Blob 복사</span><span class="sxs-lookup"><span data-stu-id="d695c-193">Copy blobs</span></span>
<span data-ttu-id="d695c-194">저장소 계정 및 지역 내 또는 전체에 걸쳐 비동기적으로 Blob을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-194">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="d695c-195">hello 다음 예제에서는 하나의 저장소에서 blob toocopy tooanother를 고려 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d695c-195">hello following example demonstrates how toocopy blobs from one storage account tooanother.</span></span> <span data-ttu-id="d695c-196">먼저 만듭니다 컨테이너 hello 원본 저장소 계정에 해당 blob에 대 한 공용 읽기 권한을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-196">We first create a container in hello source storage account, specifying public read-access for its blobs.</span></span> <span data-ttu-id="d695c-197">다음으로, 우리 파일 toohello 컨테이너 및 마지막으로, 해당 컨테이너에서 hello blob 복사에 업로드 hello 대상 저장소 계정에서 컨테이너 합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-197">Next, we upload a file toohello container, and finally, copy hello blob from that container into a container in hello destination storage account.</span></span>

```azurecli
# Create container in source account
az storage container create \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --name sourcecontainer \
    --public-access blob

# Upload blob toocontainer in source account
az storage blob upload \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --container-name sourcecontainer \
    --file ~/Pictures/sourcefile.png \
    --name sourcefile.png

# Copy blob from source account toodestination account (destcontainer must exist)
az storage blob copy start \
    --account-name destaccountname \
    --account-key destaccountkey \
    --destination-blob destfile.png \
    --destination-container destcontainer \
    --source-uri https://sourceaccountname.blob.core.windows.net/sourcecontainer/sourcefile.png
```

<span data-ttu-id="d695c-198">위 예제는 hello에서 hello 대상 컨테이너 복사 작업 toosucceed hello에 대 한 hello 대상 저장소 계정에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-198">In hello above example, hello destination container must already exist in hello destination storage account for hello copy operation toosucceed.</span></span> <span data-ttu-id="d695c-199">Hello에 지정 된 hello 원본 blob 또한 `--source-uri` 인수 공유 액세스 서명 (SAS) 토큰을 포함 하거나 다음이 예제와 같이 공개적으로 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-199">Additionally, hello source blob specified in hello `--source-uri` argument must either include a shared access signature (SAS) token, or be publicly accessible, as in this example.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="d695c-200">Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="d695c-200">Delete a blob</span></span>
<span data-ttu-id="d695c-201">toodelete blob를 사용 하 여 hello `blob delete` 명령:</span><span class="sxs-lookup"><span data-stu-id="d695c-201">toodelete a blob, use hello `blob delete` command:</span></span>

```azurecli
az storage blob delete --container-name <container_name> --name <blob_name>
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="d695c-202">파일 공유 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="d695c-202">Create and manage file shares</span></span>
<span data-ttu-id="d695c-203">Azure 파일 저장소 hello 서버 메시지 블록 (SMB) 프로토콜을 사용 하 여 응용 프로그램에 대 한 공유 저장소를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-203">Azure File storage offers shared storage for applications using hello Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="d695c-204">Microsoft Azure 가상 컴퓨터 및 클라우드 서비스 그리고 온-프레미스 응용 프로그램은 탑재된 공유를 통해 파일 데이터를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-204">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="d695c-205">파일 공유 및 파일 데이터 hello Azure CLI를 통해 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-205">You can manage file shares and file data via hello Azure CLI.</span></span> <span data-ttu-id="d695c-206">Azure 파일 저장소에 대 한 자세한 내용은 참조 하십시오. [Windows에서 Azure 파일 저장소 시작](../storage-dotnet-how-to-use-files.md) 또는 [어떻게 toouse Azure 파일 저장소와 Linux](../storage-how-to-use-files-linux.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-206">For more information on Azure File storage, see [Get started with Azure File storage on Windows](../storage-dotnet-how-to-use-files.md) or [How toouse Azure File storage with Linux](../storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="d695c-207">파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="d695c-207">Create a file share</span></span>
<span data-ttu-id="d695c-208">Azure에서 Azure 파일 공유는 SMB 파일 공유입니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-208">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="d695c-209">모든 디렉터리 및 파일을 파일 공유에서 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-209">All directories and files must be created in a file share.</span></span> <span data-ttu-id="d695c-210">계정에 공유를 개수에 제한 없이 포함 될 수 있습니다 및 공유 파일 toohello hello 저장소 계정의 용량 한도를 개수에 제한 없이 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-210">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up toohello capacity limits of hello storage account.</span></span> <span data-ttu-id="d695c-211">hello 다음 예제에서는 라는 파일 공유 **myshare**합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-211">hello following example creates a file share named **myshare**.</span></span>

```azurecli
az storage share create --name myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="d695c-212">디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="d695c-212">Create a directory</span></span>
<span data-ttu-id="d695c-213">디렉터리는 Azure 파일 공유에 대한 계층 구조를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-213">A directory provides a hierarchical structure in an Azure file share.</span></span> <span data-ttu-id="d695c-214">hello 다음 예에서는 라는 디렉터리를 만듭니다 **myDir** hello 파일 공유에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-214">hello following example creates a directory named **myDir** in hello file share.</span></span>

```azurecli
az storage directory create --name myDir --share-name myshare
```

<span data-ttu-id="d695c-215">디렉터리 경로에는 여러 수준이 포함 될 수 있습니다(예:**dir1/dir2**).</span><span class="sxs-lookup"><span data-stu-id="d695c-215">A directory path can include multiple levels, for example **dir1/dir2**.</span></span> <span data-ttu-id="d695c-216">그러나 하위 디렉터리를 만들기 전에 모든 부모 디렉터리가 존재하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-216">However, you must ensure that all parent directories exist before creating a subdirectory.</span></span> <span data-ttu-id="d695c-217">예를 들어, 경로 **dir1/dir2**의 경우, 먼저 **dir1** 디렉터리를 만든 다음, **dir2** 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-217">For example, for path **dir1/dir2**, you must first create directory **dir1**, then create directory **dir2**.</span></span>

### <a name="upload-a-local-file-tooa-share"></a><span data-ttu-id="d695c-218">로컬 파일 tooa 공유 업로드</span><span class="sxs-lookup"><span data-stu-id="d695c-218">Upload a local file tooa share</span></span>
<span data-ttu-id="d695c-219">hello 다음 예제에서는 파일을 업로드에서 **~/temp/samplefile.txt** 의 hello tooroot **myshare** 파일 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-219">hello following example uploads a file from **~/temp/samplefile.txt** tooroot of hello **myshare** file share.</span></span> <span data-ttu-id="d695c-220">hello `--source` hello 기존 로컬 파일 tooupload 인수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-220">hello `--source` argument specifies hello existing local file tooupload.</span></span>

```azurecli
az storage file upload --share-name myshare --source ~/temp/samplefile.txt
```

<span data-ttu-id="d695c-221">디렉터리 만들기와 마찬가지로 hello 공유 tooupload hello 파일 tooan 기존 디렉터리 내 hello 공유 내 디렉터리 경로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-221">As with directory creation, you can specify a directory path within hello share tooupload hello file tooan existing directory within hello share:</span></span>

```azurecli
az storage file upload --share-name myshare/myDir --source ~/temp/samplefile.txt
```

<span data-ttu-id="d695c-222">Hello 공유에 파일 크기가 too1 TB 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-222">A file in hello share can be up too1 TB in size.</span></span>

### <a name="list-hello-files-in-a-share"></a><span data-ttu-id="d695c-223">공유에 hello 파일 나열</span><span class="sxs-lookup"><span data-stu-id="d695c-223">List hello files in a share</span></span>
<span data-ttu-id="d695c-224">Hello를 사용 하 여 공유의 파일 및 디렉터리를 나열할 수 있습니다 `az storage file list` 명령:</span><span class="sxs-lookup"><span data-stu-id="d695c-224">You can list files and directories in a share by using hello `az storage file list` command:</span></span>

```azurecli
# List hello files in hello root of a share
az storage file list --share-name myshare --output table

# List hello files in a directory within a share
az storage file list --share-name myshare/myDir --output table

# List hello files in a path within a share
az storage file list --share-name myshare --path myDir/mySubDir/MySubDir2 --output table
```

### <a name="copy-files"></a><span data-ttu-id="d695c-225">파일 복사</span><span class="sxs-lookup"><span data-stu-id="d695c-225">Copy files</span></span>      
<span data-ttu-id="d695c-226">파일 tooanother 파일, 파일 tooa blob 또는 blob tooa 파일을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-226">You can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="d695c-227">예를 들어 toocopy 다른 공유에 파일 tooa 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="d695c-227">For example, toocopy a file tooa directory in a different share:</span></span>        
        
```azurecli
az storage file copy start \
--source-share share1 --source-path dir1/file.txt \
--destination-share share2 --destination-path dir2/file.txt     
```

## <a name="next-steps"></a><span data-ttu-id="d695c-228">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d695c-228">Next steps</span></span>
<span data-ttu-id="d695c-229">다음은 Azure CLI 2.0 hello를 사용 하는 방법에 대 한 좀 더에 대 한 몇 가지 추가 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="d695c-229">Here are some additional resources for learning more about working with hello Azure CLI 2.0.</span></span>

* [<span data-ttu-id="d695c-230">Azure CLI 2.0 시작</span><span class="sxs-lookup"><span data-stu-id="d695c-230">Get started with Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="d695c-231">Azure CLI 2.0 명령 참조</span><span class="sxs-lookup"><span data-stu-id="d695c-231">Azure CLI 2.0 command reference</span></span>](/cli/azure)
* [<span data-ttu-id="d695c-232">GitHub의 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d695c-232">Azure CLI 2.0 on GitHub</span></span>](https://github.com/Azure/azure-cli)
