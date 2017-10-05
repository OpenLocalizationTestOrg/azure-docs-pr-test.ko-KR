---
title: "Azure Storage에서 Azure CLI 2.0 사용 | Microsoft Docs"
description: "Azure Storage에서 Azure 명령줄 인터페이스(Azure CLI) 2.0을 사용하여 저장소 계정을 만들어 관리하고 Azure blob과 파일 작업을 수행하는 방법에 대해 알아봅니다. Azure CLI 2.0은 Python으로 작성된 플랫폼 간 도구입니다."
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
ms.openlocfilehash: 6098216f7dd901ea48fb3ab969c7934cc288b247
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-cli-20-with-azure-storage"></a><span data-ttu-id="f52ec-104">Azure Storage에서 Azure CLI 2.0 사용</span><span class="sxs-lookup"><span data-stu-id="f52ec-104">Using the Azure CLI 2.0 with Azure Storage</span></span>

<span data-ttu-id="f52ec-105">플랫폼 간 오픈 소스 Azure CLI 2.0은 Azure 플랫폼을 사용하기 위한 명령 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-105">The open-source, cross-platform Azure CLI 2.0 provides a set of commands for working with the Azure platform.</span></span> <span data-ttu-id="f52ec-106">풍부한 데이터 액세스를 포함하여 [Azure Portal](https://portal.azure.com)과 동일한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-106">It provides much of the same functionality found in the [Azure portal](https://portal.azure.com), including rich data access.</span></span>

<span data-ttu-id="f52ec-107">이 가이드에서는 [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)을 통해 Azure Storage 계정의 리소스를 사용하는 몇 가지 작업을 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-107">In this guide, we show you how to use the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) to perform several tasks working with resources in your Azure Storage account.</span></span> <span data-ttu-id="f52ec-108">이 가이드를 사용하기 전에 최신 버전의 CLI 2.0을 다운로드하여 설치하거나 업그레이드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-108">We recommend that you download and install or upgrade to the latest version of the CLI 2.0 before using this guide.</span></span>

<span data-ttu-id="f52ec-109">이 가이드의 예제에서는 Ubuntu에서 Bash 셸을 사용한다고 가정하지만 다른 플랫폼에서도 비슷하게 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-109">The examples in the guide assume the use of the Bash shell on Ubuntu, but other platforms should perform similarly.</span></span> 

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="prerequisites"></a><span data-ttu-id="f52ec-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f52ec-110">Prerequisites</span></span>
<span data-ttu-id="f52ec-111">이 가이드에서는 Azure 저장소의 기본 개념을 이해하고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-111">This guide assumes that you understand the basic concepts of Azure Storage.</span></span> <span data-ttu-id="f52ec-112">또한 Azure와 저장소 서비스에 대해 아래에 지정된 계정 만들기 요구 사항을 충족할 수 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-112">It also assumes that you're able to satisfy the account creation requirements that are specified below for Azure and the Storage service.</span></span>

### <a name="accounts"></a><span data-ttu-id="f52ec-113">계정</span><span class="sxs-lookup"><span data-stu-id="f52ec-113">Accounts</span></span>
* <span data-ttu-id="f52ec-114">**Azure 계정**: Azure 구독이 아직 없는 경우 [무료 Azure 계정을 만듭니다](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="f52ec-114">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="f52ec-115">**저장소 계정**: [Azure 저장소 계정 정보](../storage/storage-create-storage-account.md)의 [저장소 계정 만들기](../storage/storage-create-storage-account.md#create-a-storage-account) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f52ec-115">**Storage account**: See [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/storage-create-storage-account.md).</span></span>

### <a name="install-the-azure-cli-20"></a><span data-ttu-id="f52ec-116">Azure CLI 2.0 설치</span><span class="sxs-lookup"><span data-stu-id="f52ec-116">Install the Azure CLI 2.0</span></span>

<span data-ttu-id="f52ec-117">[Azure CLI 2.0 설치](/cli/azure/install-az-cli2)에 설명된 지침에 따라 Azure CLI 2.0을 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-117">Download and install the Azure CLI 2.0 by following the instructions outlined in [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

> [!TIP]
> <span data-ttu-id="f52ec-118">설치하는 데 문제가 있으면 관련 문서의 [설치 문제 해결](/cli/azure/install-az-cli2#installation-troubleshooting) 섹션 및 GitHub의 [설치 문제 해결](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) 가이드를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f52ec-118">If you have trouble with the installation, check out the [Installation Troubleshooting](/cli/azure/install-az-cli2#installation-troubleshooting) section of the article, and the [Install Troubleshooting](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) guide on GitHub.</span></span>
>

## <a name="working-with-the-cli"></a><span data-ttu-id="f52ec-119">CLI 사용</span><span class="sxs-lookup"><span data-stu-id="f52ec-119">Working with the CLI</span></span>

<span data-ttu-id="f52ec-120">CLI를 설치했으면 명령줄 인터페이스(Bash, 터미널, 명령 프롬프트)에서 `az` 명령을 사용하여 Azure CLI 명령에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-120">Once you've installed the CLI, you can use the `az` command in your command-line interface (Bash, Terminal, Command Prompt) to access the Azure CLI commands.</span></span> <span data-ttu-id="f52ec-121">`az` 명령을 입력하여 기본 명령의 전체 목록을 확인합니다(다음 예제 출력이 잘림).</span><span class="sxs-lookup"><span data-stu-id="f52ec-121">Type the `az` command to see a full list of the base commands (the following example output has been truncated):</span></span>

```
     /\
    /  \    _____   _ _ __ ___
   / /\ \  |_  / | | | \'__/ _ \
  / ____ \  / /| |_| | | |  __/
 /_/    \_\/___|\__,_|_|  \___|


Welcome to the cool new Azure CLI!

Here are the base commands:

    account          : Manage subscriptions.
    acr              : Manage Azure container registries.
    acs              : Manage Azure Container Services.
    ad               : Synchronize on-premises directories and manage Azure Active Directory
                       resources.
    ...
```

<span data-ttu-id="f52ec-122">명령줄 인터페이스에서 `az storage --help` 명령을 실행하여 `storage` 명령 하위 그룹을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-122">In your command-line interface, execute the command `az storage --help` to list the `storage` command subgroups.</span></span> <span data-ttu-id="f52ec-123">하위 그룹에 대한 설명은 Azure CLI에서 저장소 리소스 작업을 위해 제공하는 기능에 대한 개요입니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-123">The descriptions of the subgroups provide an overview of the functionality the Azure CLI provides for working with your storage resources.</span></span>

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
    file     : File shares that use the standard SMB 3.0 protocol.
    logging  : Manage Storage service logging information.
    message  : Manage queue storage messages.
    metrics  : Manage Storage service metrics.
    queue    : Use queues to effectively scale applications according to traffic.
    share    : Manage file shares.
    table    : NoSQL key-value storage using semi-structured datasets.
```

## <a name="connect-the-cli-to-your-azure-subscription"></a><span data-ttu-id="f52ec-124">Azure 구독에 CLI 연결</span><span class="sxs-lookup"><span data-stu-id="f52ec-124">Connect the CLI to your Azure subscription</span></span>

<span data-ttu-id="f52ec-125">Azure 구독에 있는 리소스를 사용하려면 먼저 `az login`으로 Azure 계정에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-125">To work with the resources in your Azure subscription, you must first log in to your Azure account with `az login`.</span></span> <span data-ttu-id="f52ec-126">로그인할 수 있는 몇 가지 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-126">There are several ways you can log in:</span></span>

* <span data-ttu-id="f52ec-127">**대화형 로그인**: `az login`</span><span class="sxs-lookup"><span data-stu-id="f52ec-127">**Interactive login**: `az login`</span></span>
* <span data-ttu-id="f52ec-128">**사용자 이름 및 암호로 로그인**: `az login -u johndoe@contoso.com -p VerySecret`</span><span class="sxs-lookup"><span data-stu-id="f52ec-128">**Log in with user name and password**: `az login -u johndoe@contoso.com -p VerySecret`</span></span>
  * <span data-ttu-id="f52ec-129">Microsoft 계정 또는 다단계 인증을 사용하는 계정에서는 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-129">This doesn't work with Microsoft accounts or accounts that use multi-factor authentication.</span></span>
* <span data-ttu-id="f52ec-130">**서비스 주체로 로그인**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="f52ec-130">**Log in with a service principal**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span></span>

## <a name="azure-cli-20-sample-script"></a><span data-ttu-id="f52ec-131">Azure CLI 2.0 샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="f52ec-131">Azure CLI 2.0 sample script</span></span>

<span data-ttu-id="f52ec-132">다음으로 Azure Storage 리소스와 상호 작용하는 몇 가지 기본 Azure CLI 2.0 명령을 발급하는 작은 셸 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-132">Next, we'll work with a small shell script that issues a few basic Azure CLI 2.0 commands to interact with Azure Storage resources.</span></span> <span data-ttu-id="f52ec-133">이 스크립트는 먼저 저장소 계정에 새 컨테이너를 만든 다음 해당 컨테이너에 기존 파일(Blob)을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-133">The script first creates a new container in your storage account, then uploads an existing file (as a blob) to that container.</span></span> <span data-ttu-id="f52ec-134">그런 다음 컨테이너에 있는 모든 Blob을 나열하고, 마지막으로 사용자가 지정한 로컬 컴퓨터의 대상에 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-134">It then lists all blobs in the container, and finally, downloads the file to a destination on your local computer that you specify.</span></span>

```bash
#!/bin/bash
# A simple Azure Storage example script

export AZURE_STORAGE_ACCOUNT=<storage_account_name>
export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

export container_name=<container_name>
export blob_name=<blob_name>
export file_to_upload=<file_to_upload>
export destination_file=<destination_file>

echo "Creating the container..."
az storage container create --name $container_name

echo "Uploading the file..."
az storage blob upload --container-name $container_name --file $file_to_upload --name $blob_name

echo "Listing the blobs..."
az storage blob list --container-name $container_name --output table

echo "Downloading the file..."
az storage blob download --container-name $container_name --name $blob_name --file $destination_file --output table

echo "Done"
```

<span data-ttu-id="f52ec-135">**스크립트 구성 및 실행**</span><span class="sxs-lookup"><span data-stu-id="f52ec-135">**Configure and run the script**</span></span>

1. <span data-ttu-id="f52ec-136">원하는 텍스트 편집기를 연 다음 앞서의 스크립트를 복사하여 편집기에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-136">Open your favorite text editor, then copy and paste the preceding script into the editor.</span></span>

2. <span data-ttu-id="f52ec-137">다음으로 구성 설정을 반영하도록 스크립트의 변수를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-137">Next, update the script's variables to reflect your configuration settings.</span></span> <span data-ttu-id="f52ec-138">다음 값을 지정한 대로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-138">Replace the following values as specified:</span></span>

   * <span data-ttu-id="f52ec-139">**\<storage_account_name\>** 저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-139">**\<storage_account_name\>** The name of your storage account.</span></span>
   * <span data-ttu-id="f52ec-140">**\<storage_account_key\>** 저장소 계정의 기본 또는 보조 액세스 키입니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-140">**\<storage_account_key\>** The primary or secondary access key for your storage account.</span></span>
   * <span data-ttu-id="f52ec-141">**\<container_name\>** 새로 만들 컨테이너의 이름입니다(예: "azure-cli-sample-container").</span><span class="sxs-lookup"><span data-stu-id="f52ec-141">**\<container_name\>** A name the new container to create, such as "azure-cli-sample-container".</span></span>
   * <span data-ttu-id="f52ec-142">**\<Blob_name\>** 컨테이너에 있는 대상 Blob의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-142">**\<blob_name\>** A name for the destination blob in the container.</span></span>
   * <span data-ttu-id="f52ec-143">**\<file_to_upload\>** 로컬 컴퓨터의 작은 파일 경로입니다(예: "~/images/HelloWorld.png").</span><span class="sxs-lookup"><span data-stu-id="f52ec-143">**\<file_to_upload\>** The path to small file on your local computer, such as "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="f52ec-144">**\<destination_file\>** 대상 파일 경로입니다(예: "~/downloadedImage.png").</span><span class="sxs-lookup"><span data-stu-id="f52ec-144">**\<destination_file\>** The destination file path, such as "~/downloadedImage.png".</span></span>

3. <span data-ttu-id="f52ec-145">필요한 변수를 업데이트한 후 해당 스크립트를 저장하고 편집기를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-145">After you've updated the necessary variables, save the script and exit your editor.</span></span> <span data-ttu-id="f52ec-146">다음 단계에서는 스크립트 이름으로 **my_storage_sample.sh**를 지정했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-146">The next steps assume you've named your script **my_storage_sample.sh**.</span></span>

4. <span data-ttu-id="f52ec-147">필요한 경우 다음과 같이 스크립트를 실행 가능으로 표시합니다. `chmod +x my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="f52ec-147">Mark the script as executable, if necessary: `chmod +x my_storage_sample.sh`</span></span>

5. <span data-ttu-id="f52ec-148">스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-148">Execute the script.</span></span> <span data-ttu-id="f52ec-149">예를 들어 Bash에서는 `./my_storage_sample.sh`입니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-149">For example, in Bash: `./my_storage_sample.sh`</span></span>

<span data-ttu-id="f52ec-150">다음과 비슷한 출력이 표시되며, 스크립트에 지정한 **\<destination_file\>**이 로컬 컴퓨터에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-150">You should see output similar to the following, and the **\<destination_file\>** you specified in the script should appear on your local computer.</span></span>

```
Creating the container...
{
  "created": true
}
Uploading the file...
Percent complete: %100.0
Listing the blobs...
Name       Blob Type      Length  Content Type              Last Modified
---------  -----------  --------  ------------------------  -------------------------
README.md  BlockBlob        6700  application/octet-stream  2017-05-12T20:54:59+00:00
Downloading the file...
Name
---------
README.md
Done
```

> [!TIP]
> <span data-ttu-id="f52ec-151">앞서의 출력은 **테이블** 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-151">The preceding output is in **table** format.</span></span> <span data-ttu-id="f52ec-152">CLI 명령에서 `--output` 인수를 지정하여 사용할 출력 형식을 지정하거나 `az configure`를 사용하여 전역으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-152">You can specify which output format to use by specifying the `--output` argument in your CLI commands, or set it globally using `az configure`.</span></span>
>

## <a name="manage-storage-accounts"></a><span data-ttu-id="f52ec-153">저장소 계정 관리</span><span class="sxs-lookup"><span data-stu-id="f52ec-153">Manage storage accounts</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="f52ec-154">새 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="f52ec-154">Create a new storage account</span></span>
<span data-ttu-id="f52ec-155">Azure Storage를 사용하려면 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-155">To use Azure Storage, you need a storage account.</span></span> <span data-ttu-id="f52ec-156">[구독에 연결](#connect-to-your-azure-subscription)하도록 컴퓨터를 구성한 후 새 Azure Storage 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-156">You can create a new Azure Storage account after you've configured your computer to [connect to your subscription](#connect-to-your-azure-subscription).</span></span>

```azurecli
az storage account create \
    --location <location> \
    --name <account_name> \
    --resource-group <resource_group> \
    --sku <account_sku>
```

* <span data-ttu-id="f52ec-157">`--location`[필수]: 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-157">`--location` [Required]: Location.</span></span> <span data-ttu-id="f52ec-158">예를 들어 "미국 서부"를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-158">For example, "West US".</span></span>
* <span data-ttu-id="f52ec-159">`--name`[필수]: 저장소 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-159">`--name` [Required]: The storage account name.</span></span> <span data-ttu-id="f52ec-160">이름의 길이는 3-24자여야 하며, 소문자 영숫자만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-160">The name must be 3 to 24 characters in length, and use only lowercase alphanumeric characters.</span></span>
* <span data-ttu-id="f52ec-161">`--resource-group`[필수]: 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-161">`--resource-group` [Required]: Name of resource group.</span></span>
* <span data-ttu-id="f52ec-162">`--sku`[필수]: 저장소 계정 SKU입니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-162">`--sku` [Required]: The storage account SKU.</span></span> <span data-ttu-id="f52ec-163">허용되는 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-163">Allowed values:</span></span>
  * `Premium_LRS`
  * `Standard_GRS`
  * `Standard_LRS`
  * `Standard_RAGRS`
  * `Standard_ZRS`

### <a name="set-default-azure-storage-account-environment-variables"></a><span data-ttu-id="f52ec-164">기본 Azure Storage 계정 환경 변수 설정</span><span class="sxs-lookup"><span data-stu-id="f52ec-164">Set default Azure storage account environment variables</span></span>
<span data-ttu-id="f52ec-165">Azure 구독에서 여러 저장소 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-165">You can have multiple storage accounts in your Azure subscription.</span></span> <span data-ttu-id="f52ec-166">모든 후속 저장소 명령에 사용하기 위해 이러한 계정 중 하나를 선택하려면 환경 변수를 다음과 같이 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-166">To select one of them to use for all subsequent storage commands, you can set these environment variables:</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="f52ec-167">기본 저장소 계정을 설정하는 또 다른 방법은 연결 문자열을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-167">Another way to set a default storage account is by using a connection string.</span></span> <span data-ttu-id="f52ec-168">먼저 `show-connection-string` 명령으로 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-168">First, get the connection string with the `show-connection-string` command:</span></span>

```azurecli
az storage account show-connection-string \
    --name <account_name> \
    --resource-group <resource_group>
```

<span data-ttu-id="f52ec-169">그런 다음 출력 연결 문자열을 복사하고 `AZURE_STORAGE_CONNECTION_STRING` 환경 변수를 설정합니다(연결 문자열을 따옴표로 묶어야 할 수도 있음).</span><span class="sxs-lookup"><span data-stu-id="f52ec-169">Then copy the output connection string and set the `AZURE_STORAGE_CONNECTION_STRING` environment variable (you might need to enclose the connection string in quotes):</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING="<connection_string>"
```

> [!NOTE]
> <span data-ttu-id="f52ec-170">이 문서의 다음 섹션에 나오는 모든 예제에서는 `AZURE_STORAGE_ACCOUNT` 및 `AZURE_STORAGE_ACCESS_KEY` 환경 변수를 설정했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-170">All examples in the following sections of this article assume that you've set the `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY` environment variables.</span></span>
>

## <a name="create-and-manage-blobs"></a><span data-ttu-id="f52ec-171">Blob 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="f52ec-171">Create and manage blobs</span></span>
<span data-ttu-id="f52ec-172">Azure Blob 저장소는 HTTP 또는 HTTPS를 통해 전 세계 어디에서든 액세스할 수 있는 다량의 구조화되지 않은 데이터(예: 텍스트 또는 이진 데이터)를 저장할 수 있는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-172">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="f52ec-173">이 섹션에서는 Azure Blob 저장소 개념에 이미 익숙하다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-173">This section assumes that you are already familiar with Azure Blob storage concepts.</span></span> <span data-ttu-id="f52ec-174">자세한 내용은 [.NET을 사용하여 Azure Blob Storage 시작](storage-dotnet-how-to-use-blobs.md) 및 [Blob Service 개념](/rest/api/storageservices/blob-service-concepts)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f52ec-174">For detailed information, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](/rest/api/storageservices/blob-service-concepts).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="f52ec-175">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="f52ec-175">Create a container</span></span>
<span data-ttu-id="f52ec-176">Azure 저장소의 모든 Blob은 컨테이너에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-176">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="f52ec-177">`az storage container create` 명령을 사용하면 컨테이너를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-177">You can create a container by using the `az storage container create` command:</span></span>

```azurecli
az storage container create --name <container_name>
```

<span data-ttu-id="f52ec-178">선택적인 `--public-access` 인수를 지정하면 새 컨테이너에 대한 읽기 액세스의 다음 세 가지 수준 중 하나를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-178">You can set one of three levels of read access for a new container by specifying the optional  `--public-access` argument:</span></span>

* <span data-ttu-id="f52ec-179">`off`(기본값): 컨테이너 데이터가 계정 소유자 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-179">`off` (default): Container data is private to the account owner.</span></span>
* <span data-ttu-id="f52ec-180">`blob`: Blob에 대한 공용 읽기 액세스입니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-180">`blob`: Public read access for blobs.</span></span>
* <span data-ttu-id="f52ec-181">`container`: 전체 컨테이너에 대한 공용 읽기 및 목록 액세스입니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-181">`container`: Public read and list access to the entire container.</span></span>

<span data-ttu-id="f52ec-182">자세한 내용은 [컨테이너 및 Blob에 대한 익명 읽기 권한 관리](storage-manage-access-to-resources.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f52ec-182">For more information, see [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span></span>

### <a name="upload-a-blob-to-a-container"></a><span data-ttu-id="f52ec-183">컨테이너에 Blob 업로드</span><span class="sxs-lookup"><span data-stu-id="f52ec-183">Upload a blob to a container</span></span>
<span data-ttu-id="f52ec-184">Azure Blob 저장소는 블록 Blob, 추가 Blob 및 페이지 Blob을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-184">Azure Blob storage supports block, append, and page blobs.</span></span> <span data-ttu-id="f52ec-185">`blob upload` 명령을 사용하여 컨테이너에 Blob을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-185">Upload blobs to a container by using the `blob upload` command:</span></span>

```azurecli
az storage blob upload \
    --file <local_file_path> \
    --container-name <container_name> \
    --name <blob_name>
```

 <span data-ttu-id="f52ec-186">기본적으로 `blob upload` 명령은 페이지 Blob에 *.vhd 파일을 업로드하며, 그렇지 않으면 블록 Blob에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-186">By default, the `blob upload` command uploads *.vhd files to page blobs, or block blobs otherwise.</span></span> <span data-ttu-id="f52ec-187">Blob을 업로드할 때 다른 유형을 지정하려면 `--type` 인수를 사용할 수 있으며, 허용되는 값은 `append`, `block` 및 `page`입니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-187">To specify another type when you upload a blob, you can use the `--type` argument--allowed values are `append`, `block`, and `page`.</span></span>

 <span data-ttu-id="f52ec-188">Blob에 대한 자세한 내용은 [블록 Blob, 추가 Blob 및 페이지 Blob 이해](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f52ec-188">For more information on the different blob types, see [Understanding Block Blobs, Append Blobs, and Page Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span></span>


### <a name="download-a-blob-from-a-container"></a><span data-ttu-id="f52ec-189">컨테이너에서 Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="f52ec-189">Download a blob from a container</span></span>
<span data-ttu-id="f52ec-190">다음 예제에서는 컨테이너에서 Blob을 다운로드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-190">This example demonstrates how to download a blob from a container:</span></span>

```azurecli
az storage blob download \
    --container-name mycontainer \
    --name myblob.png \
    --file ~/mydownloadedblob.png
```

### <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="f52ec-191">컨테이너의 Blob 나열</span><span class="sxs-lookup"><span data-stu-id="f52ec-191">List the blobs in a container</span></span>

<span data-ttu-id="f52ec-192">[az storage blob list](/cli/azure/storage/blob#list) 명령으로 컨테이너에 있는 Blob을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-192">List the blobs in a container with the [az storage blob list](/cli/azure/storage/blob#list) command.</span></span>

```azurecli
az storage blob list \
    --container-name mycontainer \
    --output table
```

### <a name="copy-blobs"></a><span data-ttu-id="f52ec-193">Blob 복사</span><span class="sxs-lookup"><span data-stu-id="f52ec-193">Copy blobs</span></span>
<span data-ttu-id="f52ec-194">저장소 계정 및 지역 내 또는 전체에 걸쳐 비동기적으로 Blob을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-194">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="f52ec-195">다음 예제에서는 한 저장소 계정에서 다른 계정으로 Blob을 복사하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-195">The following example demonstrates how to copy blobs from one storage account to another.</span></span> <span data-ttu-id="f52ec-196">먼저 해당 Blob에 대해 공용 읽기 액세스를 지정하여 원본 저장소 계정에 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-196">We first create a container in the source storage account, specifying public read-access for its blobs.</span></span> <span data-ttu-id="f52ec-197">그런 다음 컨테이너에 파일을 업로드하고, 마지막으로 해당 컨테이너의 Blob을 대상 저장소 계정의 컨테이너에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-197">Next, we upload a file to the container, and finally, copy the blob from that container into a container in the destination storage account.</span></span>

```azurecli
# Create container in source account
az storage container create \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --name sourcecontainer \
    --public-access blob

# Upload blob to container in source account
az storage blob upload \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --container-name sourcecontainer \
    --file ~/Pictures/sourcefile.png \
    --name sourcefile.png

# Copy blob from source account to destination account (destcontainer must exist)
az storage blob copy start \
    --account-name destaccountname \
    --account-key destaccountkey \
    --destination-blob destfile.png \
    --destination-container destcontainer \
    --source-uri https://sourceaccountname.blob.core.windows.net/sourcecontainer/sourcefile.png
```

<span data-ttu-id="f52ec-198">위의 예제에서는 복사 작업이 성공하기 위해 대상 컨테이너가 대상 저장소 계정에 이미 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-198">In the above example, the destination container must already exist in the destination storage account for the copy operation to succeed.</span></span> <span data-ttu-id="f52ec-199">또한 `--source-uri` 인수에 지정된 원본 Blob는 SAS(공유 액세스 서명) 토큰을 포함하거나 이 예제에서처럼 공개적으로 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-199">Additionally, the source blob specified in the `--source-uri` argument must either include a shared access signature (SAS) token, or be publicly accessible, as in this example.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="f52ec-200">Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="f52ec-200">Delete a blob</span></span>
<span data-ttu-id="f52ec-201">Blob을 삭제하려면 `blob delete` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-201">To delete a blob, use the `blob delete` command:</span></span>

```azurecli
az storage blob delete --container-name <container_name> --name <blob_name>
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="f52ec-202">파일 공유 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="f52ec-202">Create and manage file shares</span></span>
<span data-ttu-id="f52ec-203">Azure File Storage는 SMB(서버 메시지 블록) 프로토콜을 사용하는 응용 프로그램을 위한 공유 저장소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-203">Azure File storage offers shared storage for applications using the Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="f52ec-204">Microsoft Azure 가상 컴퓨터 및 클라우드 서비스 그리고 온-프레미스 응용 프로그램은 탑재된 공유를 통해 파일 데이터를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-204">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="f52ec-205">Azure CLI를 통해 파일 공유 및 파일 데이터를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-205">You can manage file shares and file data via the Azure CLI.</span></span> <span data-ttu-id="f52ec-206">Azure File Storage에 대한 자세한 내용은 [Windows에서 Azure File Storage 시작](storage-dotnet-how-to-use-files.md) 또는 [Linux에서 Azure File Storage 사용 방법](storage-how-to-use-files-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f52ec-206">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) or [How to use Azure File storage with Linux](storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="f52ec-207">파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="f52ec-207">Create a file share</span></span>
<span data-ttu-id="f52ec-208">Azure에서 Azure 파일 공유는 SMB 파일 공유입니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-208">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="f52ec-209">모든 디렉터리 및 파일을 파일 공유에서 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-209">All directories and files must be created in a file share.</span></span> <span data-ttu-id="f52ec-210">계정에 포함할 수 있는 공유 수에는 제한이 없으며, 공유에 저장할 수 있는 파일 수에는 저장소 계정의 최대 용량 한도까지 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-210">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up to the capacity limits of the storage account.</span></span> <span data-ttu-id="f52ec-211">다음 예제에서는 **myshare**라는 파일 공유를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-211">The following example creates a file share named **myshare**.</span></span>

```azurecli
az storage share create --name myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="f52ec-212">디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="f52ec-212">Create a directory</span></span>
<span data-ttu-id="f52ec-213">디렉터리는 Azure 파일 공유에 대한 계층 구조를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-213">A directory provides a hierarchical structure in an Azure file share.</span></span> <span data-ttu-id="f52ec-214">다음 예에서는 파일 공유에 **myDir** 이라는 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-214">The following example creates a directory named **myDir** in the file share.</span></span>

```azurecli
az storage directory create --name myDir --share-name myshare
```

<span data-ttu-id="f52ec-215">디렉터리 경로에는 여러 수준이 포함 될 수 있습니다(예:**dir1/dir2**).</span><span class="sxs-lookup"><span data-stu-id="f52ec-215">A directory path can include multiple levels, for example **dir1/dir2**.</span></span> <span data-ttu-id="f52ec-216">그러나 하위 디렉터리를 만들기 전에 모든 부모 디렉터리가 존재하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-216">However, you must ensure that all parent directories exist before creating a subdirectory.</span></span> <span data-ttu-id="f52ec-217">예를 들어, 경로 **dir1/dir2**의 경우, 먼저 **dir1** 디렉터리를 만든 다음, **dir2** 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-217">For example, for path **dir1/dir2**, you must first create directory **dir1**, then create directory **dir2**.</span></span>

### <a name="upload-a-local-file-to-a-share"></a><span data-ttu-id="f52ec-218">공유에 로컬 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="f52ec-218">Upload a local file to a share</span></span>
<span data-ttu-id="f52ec-219">다음 예제에서는 **~/temp/samplefile.txt**에서 **myshare** 파일 공유의 루트로 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-219">The following example uploads a file from **~/temp/samplefile.txt** to root of the **myshare** file share.</span></span> <span data-ttu-id="f52ec-220">`--source` 인수는 업로드할 기존 로컬 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-220">The `--source` argument specifies the existing local file to upload.</span></span>

```azurecli
az storage file upload --share-name myshare --source ~/temp/samplefile.txt
```

<span data-ttu-id="f52ec-221">디렉터리를 만드는 것과 마찬가지로 다음과 같이 공유 내의 디렉터리 경로를 지정하여 공유 내의 기존 디렉터리에 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-221">As with directory creation, you can specify a directory path within the share to upload the file to an existing directory within the share:</span></span>

```azurecli
az storage file upload --share-name myshare/myDir --source ~/temp/samplefile.txt
```

<span data-ttu-id="f52ec-222">공유에 있는 파일의 크기는 각각 최대 1TB일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-222">A file in the share can be up to 1 TB in size.</span></span>

### <a name="list-the-files-in-a-share"></a><span data-ttu-id="f52ec-223">공유에 있는 파일 나열</span><span class="sxs-lookup"><span data-stu-id="f52ec-223">List the files in a share</span></span>
<span data-ttu-id="f52ec-224">`az storage file list` 명령을 사용하여 공유에 있는 파일과 디렉터리를 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-224">You can list files and directories in a share by using the `az storage file list` command:</span></span>

```azurecli
# List the files in the root of a share
az storage file list --share-name myshare --output table

# List the files in a directory within a share
az storage file list --share-name myshare/myDir --output table

# List the files in a path within a share
az storage file list --share-name myshare --path myDir/mySubDir/MySubDir2 --output table
```

### <a name="copy-files"></a><span data-ttu-id="f52ec-225">파일 복사</span><span class="sxs-lookup"><span data-stu-id="f52ec-225">Copy files</span></span>      
<span data-ttu-id="f52ec-226">파일을 다른 파일로, 파일을 Blob으로 또는 Blob을 파일로 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-226">You can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="f52ec-227">예를 들어 파일을 다른 공유의 디렉터리에 복사하려면 다음과 같이 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-227">For example, to copy a file to a directory in a different share:</span></span>        
        
```azurecli
az storage file copy start \
--source-share share1 --source-path dir1/file.txt \
--destination-share share2 --destination-path dir2/file.txt     
```

## <a name="next-steps"></a><span data-ttu-id="f52ec-228">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f52ec-228">Next steps</span></span>
<span data-ttu-id="f52ec-229">Azure CLI 2.0을 사용하는 방법에 대해 자세히 알아볼 수 있는 몇 가지 추가 리소스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f52ec-229">Here are some additional resources for learning more about working with the Azure CLI 2.0.</span></span>

* [<span data-ttu-id="f52ec-230">Azure CLI 2.0 시작</span><span class="sxs-lookup"><span data-stu-id="f52ec-230">Get started with Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="f52ec-231">Azure CLI 2.0 명령 참조</span><span class="sxs-lookup"><span data-stu-id="f52ec-231">Azure CLI 2.0 command reference</span></span>](/cli/azure)
* [<span data-ttu-id="f52ec-232">GitHub의 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f52ec-232">Azure CLI 2.0 on GitHub</span></span>](https://github.com/Azure/azure-cli)
