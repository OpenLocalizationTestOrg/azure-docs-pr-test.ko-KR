---
title: "Azure Storage에서 Azure CLI 1.0 사용 | Microsoft Docs"
description: "Azure Storage에서 Azure 명령줄 인터페이스(Azure CLI) 1.0을 사용하여 저장소 계정을 만들어 관리하고 Azure blob과 파일 작업을 수행하는 방법에 대해 알아봅니다. Azure CLI는 플랫폼 간 도구입니다."
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: b502232a-e8f6-4d6c-befd-3476592e0e35
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: seguler
ms.openlocfilehash: b246d8813a41d353a9c0fa31fe838e025fc93046
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-cli-10-with-azure-storage"></a><span data-ttu-id="41722-104">Azure Storage에서 Azure CLI 1.0 사용</span><span class="sxs-lookup"><span data-stu-id="41722-104">Using the Azure CLI 1.0 with Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="41722-105">개요</span><span class="sxs-lookup"><span data-stu-id="41722-105">Overview</span></span>

<span data-ttu-id="41722-106">Azure CLI는 Azure 플랫폼 작업을 위한 플랫폼 간 오픈 소스 명령 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-106">The Azure CLI provides a set of open source, cross-platform commands for working with the Azure Platform.</span></span> <span data-ttu-id="41722-107">다양한 데이터 액세스 기능뿐만 아니라 [Azure 포털](https://portal.azure.com) 에 있는 동일한 기능을 대부분 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-107">It provides much of the same functionality found in the [Azure portal](https://portal.azure.com) as well as rich data access functionality.</span></span>

<span data-ttu-id="41722-108">이 가이드에서는 Azure Storage에서 [Azure CLI(명령줄 인터페이스 Azure)](../cli-install-nodejs.md)를 사용하여 다양한 개발 및 관리 작업을 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-108">In this guide, we'll explore how to use [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md) to perform a variety of development and administration tasks with Azure Storage.</span></span> <span data-ttu-id="41722-109">이 가이드를 사용하기 전에 최신 Azure CLI를 다운로드 및 설치하거나, 최신 버전으로 업그레이드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="41722-109">We recommend that you download and install or upgrade to the latest Azure CLI before using this guide.</span></span>

<span data-ttu-id="41722-110">이 가이드에서는 Azure 저장소의 기본 개념을 이해하고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-110">This guide assumes that you understand the basic concepts of Azure Storage.</span></span> <span data-ttu-id="41722-111">이 가이드는 Azure 저장소에서 Azure CLI를 사용하는 방법을 보여주는 몇 가지 스크립트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-111">The guide provides a number of scripts to demonstrate the usage of the Azure CLI with Azure Storage.</span></span> <span data-ttu-id="41722-112">각 스크립트를 실행하기 전에 구성에 따라 스크립트 변수를 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-112">Be sure to update the script variables based on your configuration before running each script.</span></span>

> [!NOTE]
> <span data-ttu-id="41722-113">이 가이드에서는 클래식 저장소 계정에 대한 Azure CLI 명령 및 스크립트 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-113">The guide provides the Azure CLI command and script examples for classic storage accounts.</span></span> <span data-ttu-id="41722-114">Resource Manager 저장소 계정에 대한 Azure CLI 명령은 [Azure 리소스 관리에서 Mac, Linux 및 Windows용 Azure CLI 사용](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41722-114">See [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) for Azure CLI commands for Resource Manager storage accounts.</span></span>
>
>

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="get-started-with-azure-storage-and-the-azure-cli-in-5-minutes"></a><span data-ttu-id="41722-115">5분 안에 Azure 저장소 및 Azure CLI 시작하기</span><span class="sxs-lookup"><span data-stu-id="41722-115">Get started with Azure Storage and the Azure CLI in 5 minutes</span></span>
<span data-ttu-id="41722-116">이 가이드에서는 예제를 보려면 Ubuntu를 사용하며 다른 OS 플랫폼에서도 유사하게 수행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-116">This guide uses Ubuntu for examples, but other OS platforms should perform similarly.</span></span>

<span data-ttu-id="41722-117">**Azure에 새로 만들기:** Microsoft Azure 구독 및 해당 구독과 연결된 Microsoft 계정을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="41722-117">**New to Azure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="41722-118">Azure 구입 옵션에 대한 자세한 내용은 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/), [구입 옵션](https://azure.microsoft.com/pricing/purchase-options/) 및 [회원 제안](https://azure.microsoft.com/pricing/member-offers/)(MSDN, Microsoft 파트너 네트워크, BizSpark 및 기타 Microsoft 프로그램의 회원인 경우)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41722-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="41722-119">Azure 구독에 대한 자세한 내용은 [Azure AD(Azure Active Directory)에서 관리자 역할 할당](https://msdn.microsoft.com/library/azure/hh531793.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41722-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="41722-120">**Microsoft Azure 구독 및 계정을 만든 후:**</span><span class="sxs-lookup"><span data-stu-id="41722-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="41722-121">[Azure CLI 설치](../cli-install-nodejs.md)에 설명된 지침에 따라 Azure CLI를 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-121">Download and install the Azure CLI following the instructions outlined in [Install the Azure CLI](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="41722-122">Azure CLI가 설치되었으면 명령줄 인터페이스(Bash, 터미널, 명령 프롬프트)에서 azure 명령을 사용하여 Azure CLI 명령에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41722-122">Once the Azure CLI has been installed, you will be able to use the azure command from your command-line interface (Bash, Terminal, Command prompt) to access the Azure CLI commands.</span></span> <span data-ttu-id="41722-123">_azure_ 명령을 입력하면 다음 출력이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-123">Type the _azure_ command and you should see the following output.</span></span>

    ![Azure 명령 출력][Image1]
3. <span data-ttu-id="41722-125">명령줄 인터페이스에 `azure storage`를 입력하여 모든 azure storage 명령을 나열하고 Azure CLI가 제공하는 기능의 첫 인상을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41722-125">In the command-line interface, type `azure storage` to list out all the azure storage commands and get a first impression of the functionalities the Azure CLI provides.</span></span> <span data-ttu-id="41722-126">명령 이름에 **-h** 매개 변수를 입력하여(예: `azure storage share create -h`) 명령 구문에 대한 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41722-126">You can type command name with **-h** parameter (for example, `azure storage share create -h`) to see details of command syntax.</span></span>
4. <span data-ttu-id="41722-127">이제 Azure Storage에 액세스할 수 있는 기본 Azure CLI 명령을 보여주는 간단한 스크립트를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="41722-127">Now, we'll give you a simple script that shows basic Azure CLI commands to access Azure Storage.</span></span> <span data-ttu-id="41722-128">먼저 스크립트가 저장소 계정 및 키에 대한 두 변수를 설정할 것인지 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="41722-128">The script will first ask you to set two variables for your storage account and key.</span></span> <span data-ttu-id="41722-129">그런 다음 이 스크립트는 새 저장소 계정에 새 컨테이너를 만들고 해당 컨테이너에 기존 이미지 파일(Blob)을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-129">Then, the script will create a new container in this new storage account and upload an existing image file (blob) to that container.</span></span> <span data-ttu-id="41722-130">스크립트가 해당 컨테이너의 모든 Blob을 나열한 후 로컬 컴퓨터에 있는 대상 디렉터리에 이미지 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-130">After the script lists all blobs in that container, it will download the image file to the destination directory which exists on the local computer.</span></span>

    ```azurecli
    #!/bin/bash
    # A simple Azure storage example

    export AZURE_STORAGE_ACCOUNT=<storage_account_name>
    export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

    export container_name=<container_name>
    export blob_name=<blob_name>
    export image_to_upload=<image_to_upload>
    export destination_folder=<destination_folder>

    echo "Creating the container..."
    azure storage container create $container_name

    echo "Uploading the image..."
    azure storage blob upload $image_to_upload $container_name $blob_name

    echo "Listing the blobs..."
    azure storage blob list $container_name

    echo "Downloading the image..."
    azure storage blob download $container_name $blob_name $destination_folder

    echo "Done"
    ```

5. <span data-ttu-id="41722-131">로컬 컴퓨터에서 원하는 텍스트 편집기(예: vim)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="41722-131">In your local computer, open your preferred text editor (vim for example).</span></span> <span data-ttu-id="41722-132">텍스트 편집기에 위의 스크립트를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-132">Type the above script into your text editor.</span></span>
6. <span data-ttu-id="41722-133">이제, 구성 설정에 따라 스크립트 변수를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-133">Now, you need to update the script variables based on your configuration settings.</span></span>

   * <span data-ttu-id="41722-134">**<storage_account_name>** 스크립트에 지정된 이름을 사용하거나 사용자 저장소 계정에 대한 새 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-134">**<storage_account_name>** Use the given name in the script or enter a new name for your storage account.</span></span> <span data-ttu-id="41722-135">**중요:** 저장소 계정 이름은 Azure에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-135">**Important:** The name of the storage account must be unique in Azure.</span></span> <span data-ttu-id="41722-136">소문자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-136">It must be lowercase, too!</span></span>
   * <span data-ttu-id="41722-137">**<storage_account_key>** 저장소 계정의 액세스 키</span><span class="sxs-lookup"><span data-stu-id="41722-137">**<storage_account_key>** The access key of your storage account.</span></span>
   * <span data-ttu-id="41722-138">**<container_name>** 스크립트에 지정된 이름을 사용하거나 사용자 컨테이너에 대한 새 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-138">**<container_name>** Use the given name in the script or enter a new name for your container.</span></span>
   * <span data-ttu-id="41722-139">**<image_to_upload>** 로컬 컴퓨터의 그림 경로(예: "~/images/HelloWorld.png")를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-139">**<image_to_upload>** Enter a path to a picture on your local computer, such as: "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="41722-140">**<destination_folder>** Azure Storage에서 다운로드한 파일을 보관할 로컬 디렉터리의 경로(예: "~/downloadImages")를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-140">**<destination_folder>** Enter a path to a local directory to store files downloaded from Azure Storage, such as: "~/downloadImages".</span></span>
7. <span data-ttu-id="41722-141">vim에서 필요한 변수를 업데이트 한 후 키 조합 `ESC`, `:`, `wq!`를 눌러 스크립트를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-141">After you've updated the necessary variables in vim, press key combinations `ESC`, `:`, `wq!` to save the script.</span></span>
8. <span data-ttu-id="41722-142">이 스크립트를 실행하려면 bash 콘솔에서 스크립트 파일 이름만 입력하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41722-142">To run this script, simply type the script file name in the bash console.</span></span> <span data-ttu-id="41722-143">스크립트가 실행된 후 다운로드한 이미지 파일을 포함하는 로컬 대상 폴더가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-143">After this script runs, you should have a local destination folder that includes the downloaded image file.</span></span> <span data-ttu-id="41722-144">다음 스크린샷은 예제 출력을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="41722-144">The following screenshot shows an example output:</span></span>

<span data-ttu-id="41722-145">스크립트가 실행된 후 다운로드한 이미지 파일을 포함하는 로컬 대상 폴더가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-145">After the script runs, you should have a local destination folder that includes the downloaded image file.</span></span>

## <a name="manage-storage-accounts-with-the-azure-cli"></a><span data-ttu-id="41722-146">Azure CLI를 사용하여 저장소 계정 관리</span><span class="sxs-lookup"><span data-stu-id="41722-146">Manage storage accounts with the Azure CLI</span></span>
### <a name="connect-to-your-azure-subscription"></a><span data-ttu-id="41722-147">Azure 구독에 연결</span><span class="sxs-lookup"><span data-stu-id="41722-147">Connect to your Azure subscription</span></span>
<span data-ttu-id="41722-148">대부분의 저장소 명령이 Azure 구독 없이 작동하지만 Azure CLI에서 구독에 연결하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="41722-148">While most of the storage commands will work without an Azure subscription, we recommend you to connect to your subscription from the Azure CLI.</span></span> <span data-ttu-id="41722-149">구독과 함께 작동하도록 Azure CLI를 구성하려면 [Azure CLI에서 Azure 구독에 연결](../xplat-cli-connect.md)의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="41722-149">To configure the Azure CLI to work with your subscription, follow the steps in [Connect to an Azure subscription from the Azure CLI](../xplat-cli-connect.md).</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="41722-150">새 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="41722-150">Create a new storage account</span></span>
<span data-ttu-id="41722-151">Azure 저장소를 사용하려면 저장소 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-151">To use Azure storage, you will need a storage account.</span></span> <span data-ttu-id="41722-152">구독에 연결하도록 컴퓨터를 구성한 후 새 Azure 저장소 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41722-152">You can create a new Azure storage account after you have configured your computer to connect to your subscription.</span></span>

```azurecli
azure storage account create <account_name>
```

<span data-ttu-id="41722-153">사용자의 저장소 계정 이름은 3자에서 24자 사이여야 하고 숫자 및 소문자만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-153">The name of your storage account must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

### <a name="set-a-default-azure-storage-account-in-environment-variables"></a><span data-ttu-id="41722-154">환경 변수에서 기본 Azure 저장소 계정 설정</span><span class="sxs-lookup"><span data-stu-id="41722-154">Set a default Azure storage account in environment variables</span></span>
<span data-ttu-id="41722-155">구독에서 여러 저장소 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41722-155">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="41722-156">그중 하나를 선택하여 동일한 세션의 모든 저장소 명령에 대한 환경 변수에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41722-156">You can choose one of them and set it in the environment variables for all the storage commands in the same session.</span></span> <span data-ttu-id="41722-157">이렇게 하면 저장소 계정 및 키를 명시적으로 지정하지 않고 Azure CLI 저장소 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41722-157">This enables you to run the Azure CLI storage commands without specifying the storage account and key explicitly.</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="41722-158">기본 저장소 계정을 설정하는 다른 방법은 연결 문자열을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="41722-158">Another way to set a default storage account is using connection string.</span></span> <span data-ttu-id="41722-159">첫째, 명령으로 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="41722-159">Firstly get the connection string by command:</span></span>

```azurecli
azure storage account connectionstring show <account_name>
```

<span data-ttu-id="41722-160">그런 다음 출력 연결 문자열을 복사 하여 환경 변수로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-160">Then copy the output connection string and set it to environment variable:</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=<connection_string>
```

## <a name="create-and-manage-blobs"></a><span data-ttu-id="41722-161">Blob 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="41722-161">Create and manage blobs</span></span>
<span data-ttu-id="41722-162">Azure Blob 저장소는 HTTP 또는 HTTPS를 통해 전 세계 어디에서든 액세스할 수 있는 다량의 구조화되지 않은 데이터(예: 텍스트 또는 이진 데이터)를 저장할 수 있는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="41722-162">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="41722-163">이 섹션에서는 Azure Blob 저장소 개념에 이미 익숙하다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-163">This section assumes that you are already familiar with the Azure Blob storage concepts.</span></span> <span data-ttu-id="41722-164">자세한 내용은 [.NET을 사용하여 Azure Blob Storage 시작](storage-dotnet-how-to-use-blobs.md) 및 [Blob Service 개념](http://msdn.microsoft.com/library/azure/dd179376.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41722-164">For detailed information, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="41722-165">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="41722-165">Create a container</span></span>
<span data-ttu-id="41722-166">Azure 저장소의 모든 Blob은 컨테이너에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-166">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="41722-167">`azure storage container create` 명령을 사용하여 개인 컨테이너를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41722-167">You can create a private container using the `azure storage container create` command:</span></span>

```azurecli
azure storage container create mycontainer
```

> [!NOTE]
> <span data-ttu-id="41722-168">익명 읽기 액세스의 세가지 수준은 **해제**, **Blob** 및 **컨테이너**입니다.</span><span class="sxs-lookup"><span data-stu-id="41722-168">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="41722-169">Blob에 대한 익명 액세스를 방지하려면 권한 매개 변수를 **해제**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-169">To prevent anonymous access to blobs, set the Permission parameter to **Off**.</span></span> <span data-ttu-id="41722-170">기본적으로 새 컨테이너는 전용이며 계정 소유자만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41722-170">By default, the new container is private and can be accessed only by the account owner.</span></span> <span data-ttu-id="41722-171">익명 공용 읽기 권한을 Blob 리소스에 대해 허용하지만 컨테이너 메타데이터나 컨테이너의 Blob 목록에 대해서는 허용하지 않으려면, 사용 권한 매개 변수를 **Blob**으로 설정하세요.</span><span class="sxs-lookup"><span data-stu-id="41722-171">To allow anonymous public read access to blob resources, but not to container metadata or to the list of blobs in the container, set the Permission parameter to **Blob**.</span></span> <span data-ttu-id="41722-172">Blob 리소스, 컨테이너 메타데이터 및 컨테이너의 Blob 목록에 대한 전체 공용 읽기 권한을 허용하려면, 권한 매개 변수를 **컨테이너**로 설정하세요.</span><span class="sxs-lookup"><span data-stu-id="41722-172">To allow full public read access to blob resources, container metadata, and the list of blobs in the container, set the Permission parameter to **Container**.</span></span> <span data-ttu-id="41722-173">자세한 내용은 [컨테이너 및 Blob에 대한 익명 읽기 권한 관리](storage-manage-access-to-resources.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41722-173">For more information, see [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span></span>
>
>

### <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="41722-174">컨테이너에 Blob 업로드</span><span class="sxs-lookup"><span data-stu-id="41722-174">Upload a blob into a container</span></span>
<span data-ttu-id="41722-175">Azure Blob 저장소는 블록 Blob 및 페이지 Blob을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-175">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="41722-176">자세한 내용은 [블록 Blob, 추가 Blob 및 페이지 Blob 이해](http://msdn.microsoft.com/library/azure/ee691964.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41722-176">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="41722-177">컨테이너의 blob를 업로드하도록 `azure storage blob upload`을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41722-177">To upload blobs in to a container, you can use the `azure storage blob upload`.</span></span> <span data-ttu-id="41722-178">기본적으로 이 명령은 로컬 파일을 블록 Blob에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-178">By default, this command uploads the local files to a block blob.</span></span> <span data-ttu-id="41722-179">Blob의 종류를 지정하기 위해 `--blobtype` 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41722-179">To specify the type for the blob, you can use the `--blobtype` parameter.</span></span>

```azurecli
azure storage blob upload '~/images/HelloWorld.png' mycontainer myBlockBlob
```

### <a name="download-blobs-from-a-container"></a><span data-ttu-id="41722-180">컨테이너에서 Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="41722-180">Download blobs from a container</span></span>
<span data-ttu-id="41722-181">다음 예제에서는 컨테이너에서 Blob을 다운로드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="41722-181">The following example demonstrates how to download blobs from a container.</span></span>

```azurecli
azure storage blob download mycontainer myBlockBlob '~/downloadImages/downloaded.png'
```

### <a name="copy-blobs"></a><span data-ttu-id="41722-182">Blob 복사</span><span class="sxs-lookup"><span data-stu-id="41722-182">Copy blobs</span></span>
<span data-ttu-id="41722-183">저장소 계정 및 지역 내 또는 전체에 걸쳐 비동기적으로 Blob을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41722-183">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="41722-184">다음 예제에서는 한 저장소 계정에서 다른 계정으로 Blob을 복사하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="41722-184">The following example demonstrates how to copy blobs from one storage account to another.</span></span> <span data-ttu-id="41722-185">이 샘플에서는 blob을 공개적으로 하는 컨테이너 만들어 익명으로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41722-185">In this sample we create a container where blobs are publicly, anonymously accessible.</span></span>

```azurecli
azure storage container create mycontainer2 -a <accountName2> -k <accountKey2> -p Blob

azure storage blob upload '~/Images/HelloWorld.png' mycontainer2 myBlockBlob2 -a <accountName2> -k <accountKey2>

azure storage blob copy start 'https://<accountname2>.blob.core.windows.net/mycontainer2/myBlockBlob2' mycontainer
```

<span data-ttu-id="41722-186">이 예제에서는 비동기 복사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-186">This sample performs an asynchronous copy.</span></span> <span data-ttu-id="41722-187">`azure storage blob copy show` 작업을 실행하여 각 복사 작업의 상태를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41722-187">You can monitor the status of each copy operation by running the `azure storage blob copy show` operation.</span></span>

<span data-ttu-id="41722-188">복사 작업을 위해 제공되는 원본 URL에 공개적으로 액세스할 수 있도록 하거나 SAS(공유 액세스 서명) 토큰을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-188">Note that the source URL provided for the copy operation must either be publicly accessible, or include a SAS (shared access signature) token.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="41722-189">Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="41722-189">Delete a blob</span></span>
<span data-ttu-id="41722-190">Blob을 삭제하려면 아래 명령을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="41722-190">To delete a blob, use the below command:</span></span>

```azurecli
azure storage blob delete mycontainer myBlockBlob2
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="41722-191">파일 공유 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="41722-191">Create and manage file shares</span></span>
<span data-ttu-id="41722-192">Azure 파일 저장소는 표준 SMB 프로토콜을 사용하여 응용 프로그램을 위한 공유 저장소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-192">Azure File storage offers shared storage for applications using the standard SMB protocol.</span></span> <span data-ttu-id="41722-193">Microsoft Azure 가상 컴퓨터 및 클라우드 서비스 그리고 온-프레미스 응용 프로그램은 탑재된 공유를 통해 파일 데이터를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41722-193">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="41722-194">Azure CLI를 통해 파일 공유 및 파일 데이터를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41722-194">You can manage file shares and file data via the Azure CLI.</span></span> <span data-ttu-id="41722-195">Azure File Storage에 대한 자세한 내용은 [Windows에서 Azure File Storage 시작](storage-dotnet-how-to-use-files.md) 또는 [Linux에서 Azure File Storage 사용 방법](storage-how-to-use-files-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41722-195">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) or [How to use Azure File storage with Linux](storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="41722-196">파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="41722-196">Create a file share</span></span>
<span data-ttu-id="41722-197">Azure에서 Azure 파일 공유는 SMB 파일 공유입니다.</span><span class="sxs-lookup"><span data-stu-id="41722-197">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="41722-198">모든 디렉터리 및 파일을 파일 공유에서 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-198">All directories and files must be created in a file share.</span></span> <span data-ttu-id="41722-199">계정에 포함할 수 있는 공유 수에는 제한이 없으며, 공유에 저장할 수 있는 파일 수에는 저장소 계정의 최대 용량 한도까지 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="41722-199">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up to the capacity limits of the storage account.</span></span> <span data-ttu-id="41722-200">다음 예제에서는 **myshare**라는 파일 공유를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41722-200">The following example creates a file share named **myshare**.</span></span>

```azurecli
azure storage share create myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="41722-201">디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="41722-201">Create a directory</span></span>
<span data-ttu-id="41722-202">디렉터리는 Azure 파일 공유에 대한 선택적 계층적 구조를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-202">A directory provides an optional hierarchical structure for an Azure file share.</span></span> <span data-ttu-id="41722-203">다음 예에서는 파일 공유에 **myDir** 이라는 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41722-203">The following example creates a directory named **myDir** in the file share.</span></span>

```azurecli
azure storage directory create myshare myDir
```

<span data-ttu-id="41722-204">해당 디렉터리 경로에 여러 수준이 포함 될 수 있습니다( *예:***a/b**).</span><span class="sxs-lookup"><span data-stu-id="41722-204">Note that directory path can include multiple levels, *e.g.*, **a/b**.</span></span> <span data-ttu-id="41722-205">그러나 모든 부모 디렉터리가 존재하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-205">However, you must ensure that all parent directories exist.</span></span> <span data-ttu-id="41722-206">예를 들어, 경로 **a/b**의 경우, 먼저 디렉터리 **a**를 만든 다음, **b** 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41722-206">For example, for path **a/b**, you must create directory **a** first, then create directory **b**.</span></span>

### <a name="upload-a-local-file-to-directory"></a><span data-ttu-id="41722-207">디렉터리에 로컬 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="41722-207">Upload a local file to directory</span></span>
<span data-ttu-id="41722-208">다음 예제에서는 **~/temp/samplefile.txt**에서 **myDir** 디렉터리로 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-208">The following example uploads a file from **~/temp/samplefile.txt** to the **myDir** directory.</span></span> <span data-ttu-id="41722-209">로컬 컴퓨터의 유효한 파일을 가리키도록 파일 경로를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-209">Edit the file path so that it points to a valid file on your local machine:</span></span>

```azurecli
azure storage file upload '~/temp/samplefile.txt' myshare myDir
```

<span data-ttu-id="41722-210">공유 중인 파일 하나는 최대 1TB일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41722-210">Note that a file in the share can be up to 1 TB in size.</span></span>

### <a name="list-the-files-in-the-share-root-or-directory"></a><span data-ttu-id="41722-211">공유 루트 또는 디렉터리의 파일 목록</span><span class="sxs-lookup"><span data-stu-id="41722-211">List the files in the share root or directory</span></span>
<span data-ttu-id="41722-212">다음 명령을 사용하여 공유 루트 또는 디렉터리에 있는 파일 및 하위 디렉터리를 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41722-212">You can list the files and subdirectories in a share root or a directory using the following command:</span></span>

```azurecli
azure storage file list myshare myDir
```

<span data-ttu-id="41722-213">나열 작업에 대해 디렉터리 이름은 선택적입니다.</span><span class="sxs-lookup"><span data-stu-id="41722-213">Note that the directory name is optional for the listing operation.</span></span> <span data-ttu-id="41722-214">생략하면 명령이 공유의 루트 디렉터리의 내용을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-214">If omitted, the command lists the contents of the root directory of the share.</span></span>

### <a name="copy-files"></a><span data-ttu-id="41722-215">파일 복사</span><span class="sxs-lookup"><span data-stu-id="41722-215">Copy files</span></span>
<span data-ttu-id="41722-216">Azure CLI 버전 0.9.8부터 파일을 다른 파일로, 파일을 Blob으로 또는 Blob을 파일로 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41722-216">Beginning with version 0.9.8 of Azure CLI, you can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="41722-217">아래에는 CLI 명령을 사용하여 이러한 복사 작업을 수행하는 방법이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41722-217">Below we demonstrate how to perform these copy operations using CLI commands.</span></span> <span data-ttu-id="41722-218">새 디렉터리에 파일을 복사하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-218">To copy a file to the new directory:</span></span>

```azurecli
azure storage file copy start --source-share srcshare --source-path srcdir/hello.txt --dest-share destshare
    --dest-path destdir/hellocopy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

<span data-ttu-id="41722-219">파일 디렉터리에 Blob을 복사하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="41722-219">To copy a blob to a file directory:</span></span>

```azurecli
azure storage file copy start --source-container srcctn --source-blob hello2.txt --dest-share hello
    --dest-path hellodir/hello2copy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

## <a name="next-steps"></a><span data-ttu-id="41722-220">다음 단계</span><span class="sxs-lookup"><span data-stu-id="41722-220">Next Steps</span></span>

<span data-ttu-id="41722-221">여기 있는 저장소 리소스와 함께 사용할 수 있는 Azure CLI 1.0 명령 참조를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41722-221">You can find Azure CLI 1.0 command reference for working with Storage resources here:</span></span>

* [<span data-ttu-id="41722-222">Resource Manager 모드에서 Azure CLI 명령</span><span class="sxs-lookup"><span data-stu-id="41722-222">Azure CLI commands in Resource Manager mode</span></span>](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)
* [<span data-ttu-id="41722-223">Azure 서비스 관리 모드의 Azure CLI 명령</span><span class="sxs-lookup"><span data-stu-id="41722-223">Azure CLI commands in Azure Service Management mode</span></span>](../cli-install-nodejs.md)

<span data-ttu-id="41722-224">Resource Manager 배포 모델과 함께 사용할 수 있도록 Python으로 작성된 차세대 CLI인 [Azure CLI 2.0](storage-azure-cli.md)도 사용해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41722-224">You may also like to try the [Azure CLI 2.0](storage-azure-cli.md), our next-generation CLI written in Python, for use with the Resource Manager deployment model.</span></span>

[Image1]: ./media/storage-azure-cli/azure_command.png
