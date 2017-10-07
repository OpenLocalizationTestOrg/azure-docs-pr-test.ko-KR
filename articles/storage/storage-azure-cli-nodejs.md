---
title: "Azure 저장소와 Azure CLI 1.0 aaaUsing hello | Microsoft Docs"
description: "Toouse를 Azure CLI (명령줄 인터페이스 Azure) 1.0와 Azure 저장소 toocreate hello 및 저장소 계정 관리 및 Azure blob와 파일을 작동 방법에 대해 알아봅니다. hello Azure CLI는 플랫폼 간 도구"
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
ms.openlocfilehash: 786f2be64875f5094f09fd6e4a47532889c3a82f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-10-with-azure-storage"></a><span data-ttu-id="9b86d-104">Hello Azure CLI 1.0을 사용 하 여 Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="9b86d-104">Using hello Azure CLI 1.0 with Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="9b86d-105">개요</span><span class="sxs-lookup"><span data-stu-id="9b86d-105">Overview</span></span>

<span data-ttu-id="9b86d-106">hello Azure CLI hello Azure 플랫폼을 다루기 위한 크로스 플랫폼 명령 집합이 한 오픈 소스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-106">hello Azure CLI provides a set of open source, cross-platform commands for working with hello Azure Platform.</span></span> <span data-ttu-id="9b86d-107">Hello hello에 있는 동일한 기능을 많이 제공 [Azure 포털](https://portal.azure.com) 도 같이 다양 한 데이터 기능에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-107">It provides much of hello same functionality found in hello [Azure portal](https://portal.azure.com) as well as rich data access functionality.</span></span>

<span data-ttu-id="9b86d-108">이 가이드에서는 살펴볼 것 어떻게 toouse [Azure CLI (명령줄 인터페이스 Azure)](../cli-install-nodejs.md) tooperform 다양 한 Azure 저장소와 개발 및 관리 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-108">In this guide, we'll explore how toouse [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md) tooperform a variety of development and administration tasks with Azure Storage.</span></span> <span data-ttu-id="9b86d-109">다운로드 및 설치 하거나 업그레이드 toohello 권장이 가이드를 사용 하기 전에 최신 Azure CLI 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-109">We recommend that you download and install or upgrade toohello latest Azure CLI before using this guide.</span></span>

<span data-ttu-id="9b86d-110">이 가이드 hello Azure 저장소의 기본 개념을 이해 해야 하는 것으로 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-110">This guide assumes that you understand hello basic concepts of Azure Storage.</span></span> <span data-ttu-id="9b86d-111">hello 가이드의 hello Azure 저장소와 Azure CLI toodemonstrate hello 사용 스크립트의 수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-111">hello guide provides a number of scripts toodemonstrate hello usage of hello Azure CLI with Azure Storage.</span></span> <span data-ttu-id="9b86d-112">있는지 tooupdate 각 스크립트를 실행 하기 전에 구성에 따라 hello 스크립트 변수 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-112">Be sure tooupdate hello script variables based on your configuration before running each script.</span></span>

> [!NOTE]
> <span data-ttu-id="9b86d-113">hello 가이드 클래식 저장소 계정에 대 한 hello Azure CLI 명령 및 스크립트 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-113">hello guide provides hello Azure CLI command and script examples for classic storage accounts.</span></span> <span data-ttu-id="9b86d-114">참조 [Mac, Linux 및 Windows Azure 리소스 관리에 대 한 Azure CLI를 사용 하 여 hello](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) 리소스 관리자 저장소 계정에 대 한 Azure CLI 명령에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-114">See [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) for Azure CLI commands for Resource Manager storage accounts.</span></span>
>
>

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="get-started-with-azure-storage-and-hello-azure-cli-in-5-minutes"></a><span data-ttu-id="9b86d-115">5 분 이내에 Azure 저장소 및 Azure CLI hello 시작</span><span class="sxs-lookup"><span data-stu-id="9b86d-115">Get started with Azure Storage and hello Azure CLI in 5 minutes</span></span>
<span data-ttu-id="9b86d-116">이 가이드에서는 예제를 보려면 Ubuntu를 사용하며 다른 OS 플랫폼에서도 유사하게 수행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-116">This guide uses Ubuntu for examples, but other OS platforms should perform similarly.</span></span>

<span data-ttu-id="9b86d-117">**새 tooAzure:** Microsoft Azure 구독 및 해당 구독과 연결 된 Microsoft 계정을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-117">**New tooAzure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="9b86d-118">Azure 구입 옵션에 대한 자세한 내용은 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/), [구입 옵션](https://azure.microsoft.com/pricing/purchase-options/) 및 [회원 제안](https://azure.microsoft.com/pricing/member-offers/)(MSDN, Microsoft 파트너 네트워크, BizSpark 및 기타 Microsoft 프로그램의 회원인 경우)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9b86d-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="9b86d-119">Azure 구독에 대한 자세한 내용은 [Azure AD(Azure Active Directory)에서 관리자 역할 할당](https://msdn.microsoft.com/library/azure/hh531793.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9b86d-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="9b86d-120">**Microsoft Azure 구독 및 계정을 만든 후:**</span><span class="sxs-lookup"><span data-stu-id="9b86d-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="9b86d-121">다운로드 및 설치에 설명 된 지침을 진행 hello Azure CLI hello [설치 hello Azure CLI](../cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-121">Download and install hello Azure CLI following hello instructions outlined in [Install hello Azure CLI](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="9b86d-122">Hello Azure CLI 설치가 완료 된 후 수 toouse 수 hello azure 명령줄 인터페이스 (Bash, 터미널, 명령 프롬프트) tooaccess hello Azure CLI 명령 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-122">Once hello Azure CLI has been installed, you will be able toouse hello azure command from your command-line interface (Bash, Terminal, Command prompt) tooaccess hello Azure CLI commands.</span></span> <span data-ttu-id="9b86d-123">형식 hello _azure_ 명령을 hello 출력 뒤에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-123">Type hello _azure_ command and you should see hello following output.</span></span>

    ![Azure 명령 출력][Image1]
3. <span data-ttu-id="9b86d-125">Hello 명령줄 인터페이스에서 입력 `azure storage` toolist 모든 azure 저장소 명령을 hello 및 Azure CLI 제공 hello 기능 hello의 첫 번째 인상을 가져오기.</span><span class="sxs-lookup"><span data-stu-id="9b86d-125">In hello command-line interface, type `azure storage` toolist out all hello azure storage commands and get a first impression of hello functionalities hello Azure CLI provides.</span></span> <span data-ttu-id="9b86d-126">으로 명령 이름을 입력할 수 **-h** 매개 변수 (예를 들어 `azure storage share create -h`) 명령 구문의 toosee 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-126">You can type command name with **-h** parameter (for example, `azure storage share create -h`) toosee details of command syntax.</span></span>
4. <span data-ttu-id="9b86d-127">이제 기본 Azure CLI 명령을 tooaccess Azure 저장소를 보여 주는 간단한 스크립트를 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-127">Now, we'll give you a simple script that shows basic Azure CLI commands tooaccess Azure Storage.</span></span> <span data-ttu-id="9b86d-128">hello 스크립트 먼저 묻습니다 tooset 두 변수 저장소 계정 및 키에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-128">hello script will first ask you tooset two variables for your storage account and key.</span></span> <span data-ttu-id="9b86d-129">그런 다음 hello 스크립트는 새 컨테이너를이 새 저장소 계정에서 만들고 기존 이미지 파일 (blob) toothat 컨테이너를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-129">Then, hello script will create a new container in this new storage account and upload an existing image file (blob) toothat container.</span></span> <span data-ttu-id="9b86d-130">해당 컨테이너의 모든 blob를 나열 하는 hello 스크립트, 후 hello 이미지 파일 toohello 대상 디렉터리 hello 로컬 컴퓨터에 있는 다운로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-130">After hello script lists all blobs in that container, it will download hello image file toohello destination directory which exists on hello local computer.</span></span>

    ```azurecli
    #!/bin/bash
    # A simple Azure storage example

    export AZURE_STORAGE_ACCOUNT=<storage_account_name>
    export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

    export container_name=<container_name>
    export blob_name=<blob_name>
    export image_to_upload=<image_to_upload>
    export destination_folder=<destination_folder>

    echo "Creating hello container..."
    azure storage container create $container_name

    echo "Uploading hello image..."
    azure storage blob upload $image_to_upload $container_name $blob_name

    echo "Listing hello blobs..."
    azure storage blob list $container_name

    echo "Downloading hello image..."
    azure storage blob download $container_name $blob_name $destination_folder

    echo "Done"
    ```

5. <span data-ttu-id="9b86d-131">로컬 컴퓨터에서 원하는 텍스트 편집기(예: vim)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-131">In your local computer, open your preferred text editor (vim for example).</span></span> <span data-ttu-id="9b86d-132">위의 스크립트는 hello 텍스트 편집기에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-132">Type hello above script into your text editor.</span></span>
6. <span data-ttu-id="9b86d-133">이제, 구성 설정에 기반 하 여 tooupdate hello 스크립트 변수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-133">Now, you need tooupdate hello script variables based on your configuration settings.</span></span>

   * <span data-ttu-id="9b86d-134">**< Storage_account_name >** hello 스크립트에 이름이 지정 된 hello를 사용 하거나 저장소 계정에 대 한 새 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-134">**<storage_account_name>** Use hello given name in hello script or enter a new name for your storage account.</span></span> <span data-ttu-id="9b86d-135">**중요:** hello hello 저장소 계정의 이름으로 Azure에서 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-135">**Important:** hello name of hello storage account must be unique in Azure.</span></span> <span data-ttu-id="9b86d-136">소문자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-136">It must be lowercase, too!</span></span>
   * <span data-ttu-id="9b86d-137">**< storage_account_key >** hello 선택 키의 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-137">**<storage_account_key>** hello access key of your storage account.</span></span>
   * <span data-ttu-id="9b86d-138">**< Container_name >** hello 스크립트에 이름이 지정 된 hello를 사용 하거나 컨테이너에 대해 새 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-138">**<container_name>** Use hello given name in hello script or enter a new name for your container.</span></span>
   * <span data-ttu-id="9b86d-139">**< Image_to_upload >** 로컬 컴퓨터에 같은 경로 tooa 그림을 입력: "~ / images/HelloWorld.png"입니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-139">**<image_to_upload>** Enter a path tooa picture on your local computer, such as: "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="9b86d-140">**< Destination_folder >** Enter와 같은 Azure 저장소에서 다운로드 경로 tooa 로컬 디렉터리 toostore 파일: "~/downloadImages"입니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-140">**<destination_folder>** Enter a path tooa local directory toostore files downloaded from Azure Storage, such as: "~/downloadImages".</span></span>
7. <span data-ttu-id="9b86d-141">Hello vim에서 필요한 변수를 업데이트 한 후 키 조합을 눌러 `ESC`, `:`, `wq!` toosave hello 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-141">After you've updated hello necessary variables in vim, press key combinations `ESC`, `:`, `wq!` toosave hello script.</span></span>
8. <span data-ttu-id="9b86d-142">toorun이이 스크립트를 단순히 hello 스크립트 파일의에서 형식 이름은 hello bash 콘솔.</span><span class="sxs-lookup"><span data-stu-id="9b86d-142">toorun this script, simply type hello script file name in hello bash console.</span></span> <span data-ttu-id="9b86d-143">이 스크립트를 실행 한 후 다운로드 한 hello 이미지 파일을 포함 하는 로컬 대상 폴더가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-143">After this script runs, you should have a local destination folder that includes hello downloaded image file.</span></span> <span data-ttu-id="9b86d-144">다음 스크린 샷 hello 출력을 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-144">hello following screenshot shows an example output:</span></span>

<span data-ttu-id="9b86d-145">Hello 스크립트를 실행 한 후 다운로드 한 hello 이미지 파일을 포함 하는 로컬 대상 폴더가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-145">After hello script runs, you should have a local destination folder that includes hello downloaded image file.</span></span>

## <a name="manage-storage-accounts-with-hello-azure-cli"></a><span data-ttu-id="9b86d-146">Hello Azure CLI가 있는 저장소 계정 관리</span><span class="sxs-lookup"><span data-stu-id="9b86d-146">Manage storage accounts with hello Azure CLI</span></span>
### <a name="connect-tooyour-azure-subscription"></a><span data-ttu-id="9b86d-147">Tooyour Azure 구독 연결</span><span class="sxs-lookup"><span data-stu-id="9b86d-147">Connect tooyour Azure subscription</span></span>
<span data-ttu-id="9b86d-148">대부분의 hello 저장소 명령은, Azure 구독 없이 작동 하는 동안 Azure CLI hello에서 tooconnect tooyour 구독을 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-148">While most of hello storage commands will work without an Azure subscription, we recommend you tooconnect tooyour subscription from hello Azure CLI.</span></span> <span data-ttu-id="9b86d-149">구독에 tooconfigure hello Azure CLI toowork hello 단계에 따라 [hello Azure CLI에서에서 tooan Azure 구독 연결](../xplat-cli-connect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-149">tooconfigure hello Azure CLI toowork with your subscription, follow hello steps in [Connect tooan Azure subscription from hello Azure CLI](../xplat-cli-connect.md).</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="9b86d-150">새 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="9b86d-150">Create a new storage account</span></span>
<span data-ttu-id="9b86d-151">Azure 저장소 toouse 저장소 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-151">toouse Azure storage, you will need a storage account.</span></span> <span data-ttu-id="9b86d-152">컴퓨터 tooconnect tooyour 구독을 구성한 후 새 Azure 저장소 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-152">You can create a new Azure storage account after you have configured your computer tooconnect tooyour subscription.</span></span>

```azurecli
azure storage account create <account_name>
```

<span data-ttu-id="9b86d-153">저장소 계정의 hello 이름 길이가 3 ~ 24 자 사이 여야 하 고 숫자 및 소문자만 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-153">hello name of your storage account must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

### <a name="set-a-default-azure-storage-account-in-environment-variables"></a><span data-ttu-id="9b86d-154">환경 변수에서 기본 Azure 저장소 계정 설정</span><span class="sxs-lookup"><span data-stu-id="9b86d-154">Set a default Azure storage account in environment variables</span></span>
<span data-ttu-id="9b86d-155">구독에서 여러 저장소 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-155">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="9b86d-156">그 중 하나를 선택할 수 있으며에 설정 hello 환경 변수 동일 hello에서 모든 hello 저장소 명령에 대 한 세션입니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-156">You can choose one of them and set it in hello environment variables for all hello storage commands in hello same session.</span></span> <span data-ttu-id="9b86d-157">이렇게 하면 toorun hello Azure CLI 저장소 hello 저장소를 지정 하지 않고 명령 계정 및 키를 명시적으로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-157">This enables you toorun hello Azure CLI storage commands without specifying hello storage account and key explicitly.</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="9b86d-158">또 다른 방법은 tooset 기본 저장소 계정 연결 문자열을 사용 중입니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-158">Another way tooset a default storage account is using connection string.</span></span> <span data-ttu-id="9b86d-159">먼저 명령 여 hello 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-159">Firstly get hello connection string by command:</span></span>

```azurecli
azure storage account connectionstring show <account_name>
```

<span data-ttu-id="9b86d-160">다음 hello 출력 연결 문자열을 복사 하 고 tooenvironment 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-160">Then copy hello output connection string and set it tooenvironment variable:</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=<connection_string>
```

## <a name="create-and-manage-blobs"></a><span data-ttu-id="9b86d-161">Blob 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="9b86d-161">Create and manage blobs</span></span>
<span data-ttu-id="9b86d-162">Azure Blob 저장소는 많은 양의 텍스트 또는 이진 데이터를 액세스할 수 있는에서 아무 곳 이나 HTTP 또는 HTTPS를 통해 hello world에 같은 구조화 되지 않은 데이터를 저장 하기 위한 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-162">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="9b86d-163">이 섹션에서는 hello Azure Blob 저장소 개념에 익숙하다고 이미 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-163">This section assumes that you are already familiar with hello Azure Blob storage concepts.</span></span> <span data-ttu-id="9b86d-164">자세한 내용은 [.NET을 사용하여 Azure Blob Storage 시작](storage-dotnet-how-to-use-blobs.md) 및 [Blob Service 개념](http://msdn.microsoft.com/library/azure/dd179376.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9b86d-164">For detailed information, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="9b86d-165">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="9b86d-165">Create a container</span></span>
<span data-ttu-id="9b86d-166">Azure 저장소의 모든 Blob은 컨테이너에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-166">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="9b86d-167">Hello를 사용 하 여 개인 컨테이너를 만들 수 있습니다 `azure storage container create` 명령:</span><span class="sxs-lookup"><span data-stu-id="9b86d-167">You can create a private container using hello `azure storage container create` command:</span></span>

```azurecli
azure storage container create mycontainer
```

> [!NOTE]
> <span data-ttu-id="9b86d-168">익명 읽기 액세스의 세가지 수준은 **해제**, **Blob** 및 **컨테이너**입니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-168">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="9b86d-169">익명 tooprevent tooblobs, 집합 hello 권한 매개 변수를 너무 액세스**오프**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-169">tooprevent anonymous access tooblobs, set hello Permission parameter too**Off**.</span></span> <span data-ttu-id="9b86d-170">기본적으로 hello 새 컨테이너는 전용 포트 이며 hello 계정 소유자만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-170">By default, hello new container is private and can be accessed only by hello account owner.</span></span> <span data-ttu-id="9b86d-171">tooallow 익명 공용 읽기 tooblob 리소스에 액세스 하지만 toocontainer 메타 데이터 또는 toohello 목록이 아니라 hello 컨테이너의 blob, hello 권한 매개 변수를 너무 설정**Blob**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-171">tooallow anonymous public read access tooblob resources, but not toocontainer metadata or toohello list of blobs in hello container, set hello Permission parameter too**Blob**.</span></span> <span data-ttu-id="9b86d-172">tooallow 전체 공용 읽기 액세스 tooblob 리소스, 컨테이너 메타 데이터 및 hello hello 컨테이너의 blob 목록, hello 권한 매개 변수를 너무 설정**컨테이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-172">tooallow full public read access tooblob resources, container metadata, and hello list of blobs in hello container, set hello Permission parameter too**Container**.</span></span> <span data-ttu-id="9b86d-173">자세한 내용은 참조 [익명 읽기 권한을 toocontainers 및 blob 관리](storage-manage-access-to-resources.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-173">For more information, see [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md).</span></span>
>
>

### <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="9b86d-174">컨테이너에 Blob 업로드</span><span class="sxs-lookup"><span data-stu-id="9b86d-174">Upload a blob into a container</span></span>
<span data-ttu-id="9b86d-175">Azure Blob 저장소는 블록 Blob 및 페이지 Blob을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-175">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="9b86d-176">자세한 내용은 [블록 Blob, 추가 Blob 및 페이지 Blob 이해](http://msdn.microsoft.com/library/azure/ee691964.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9b86d-176">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="9b86d-177">tooupload blob tooa 컨테이너에서 hello를 사용할 수 있습니다 `azure storage blob upload`합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-177">tooupload blobs in tooa container, you can use hello `azure storage blob upload`.</span></span> <span data-ttu-id="9b86d-178">기본적으로이 명령은 hello 로컬 파일 tooa 블록 blob을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-178">By default, this command uploads hello local files tooa block blob.</span></span> <span data-ttu-id="9b86d-179">toospecify hello 유형 hello blob hello를 사용할 수 있습니다 `--blobtype` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-179">toospecify hello type for hello blob, you can use hello `--blobtype` parameter.</span></span>

```azurecli
azure storage blob upload '~/images/HelloWorld.png' mycontainer myBlockBlob
```

### <a name="download-blobs-from-a-container"></a><span data-ttu-id="9b86d-180">컨테이너에서 Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="9b86d-180">Download blobs from a container</span></span>
<span data-ttu-id="9b86d-181">다음 예제는 hello toodownload 컨테이너에서 blob 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-181">hello following example demonstrates how toodownload blobs from a container.</span></span>

```azurecli
azure storage blob download mycontainer myBlockBlob '~/downloadImages/downloaded.png'
```

### <a name="copy-blobs"></a><span data-ttu-id="9b86d-182">Blob 복사</span><span class="sxs-lookup"><span data-stu-id="9b86d-182">Copy blobs</span></span>
<span data-ttu-id="9b86d-183">저장소 계정 및 지역 내 또는 전체에 걸쳐 비동기적으로 Blob을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-183">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="9b86d-184">hello 다음 예제에서는 하나의 저장소에서 blob toocopy tooanother를 고려 하는 방법</span><span class="sxs-lookup"><span data-stu-id="9b86d-184">hello following example demonstrates how toocopy blobs from one storage account tooanother.</span></span> <span data-ttu-id="9b86d-185">이 샘플에서는 blob을 공개적으로 하는 컨테이너 만들어 익명으로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-185">In this sample we create a container where blobs are publicly, anonymously accessible.</span></span>

```azurecli
azure storage container create mycontainer2 -a <accountName2> -k <accountKey2> -p Blob

azure storage blob upload '~/Images/HelloWorld.png' mycontainer2 myBlockBlob2 -a <accountName2> -k <accountKey2>

azure storage blob copy start 'https://<accountname2>.blob.core.windows.net/mycontainer2/myBlockBlob2' mycontainer
```

<span data-ttu-id="9b86d-186">이 예제에서는 비동기 복사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-186">This sample performs an asynchronous copy.</span></span> <span data-ttu-id="9b86d-187">Hello를 실행 하 여 각 복사 작업의 hello 상태를 모니터링할 수 있습니다 `azure storage blob copy show` 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-187">You can monitor hello status of each copy operation by running hello `azure storage blob copy show` operation.</span></span>

<span data-ttu-id="9b86d-188">Note hello 복사 작업에 제공 된 hello 소스 URL 해야 공개적으로 액세스할 수 없거나 SAS (공유 액세스 서명) 토큰을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-188">Note that hello source URL provided for hello copy operation must either be publicly accessible, or include a SAS (shared access signature) token.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="9b86d-189">Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="9b86d-189">Delete a blob</span></span>
<span data-ttu-id="9b86d-190">blob toodelete 명령 아래의 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-190">toodelete a blob, use hello below command:</span></span>

```azurecli
azure storage blob delete mycontainer myBlockBlob2
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="9b86d-191">파일 공유 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="9b86d-191">Create and manage file shares</span></span>
<span data-ttu-id="9b86d-192">Azure 파일 저장소 hello 표준 SMB 프로토콜을 사용 하 여 응용 프로그램에 대 한 공유 저장소를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-192">Azure File storage offers shared storage for applications using hello standard SMB protocol.</span></span> <span data-ttu-id="9b86d-193">Microsoft Azure 가상 컴퓨터 및 클라우드 서비스 그리고 온-프레미스 응용 프로그램은 탑재된 공유를 통해 파일 데이터를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-193">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="9b86d-194">파일 공유 및 파일 데이터 hello Azure CLI를 통해 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-194">You can manage file shares and file data via hello Azure CLI.</span></span> <span data-ttu-id="9b86d-195">Azure 파일 저장소에 대 한 자세한 내용은 참조 하십시오. [Windows에서 Azure 파일 저장소 시작](storage-dotnet-how-to-use-files.md) 또는 [어떻게 toouse Azure 파일 저장소와 Linux](storage-how-to-use-files-linux.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-195">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) or [How toouse Azure File storage with Linux](storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="9b86d-196">파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="9b86d-196">Create a file share</span></span>
<span data-ttu-id="9b86d-197">Azure에서 Azure 파일 공유는 SMB 파일 공유입니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-197">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="9b86d-198">모든 디렉터리 및 파일을 파일 공유에서 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-198">All directories and files must be created in a file share.</span></span> <span data-ttu-id="9b86d-199">계정에 공유를 개수에 제한 없이 포함 될 수 있습니다 및 공유 파일 toohello hello 저장소 계정의 용량 한도를 개수에 제한 없이 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-199">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up toohello capacity limits of hello storage account.</span></span> <span data-ttu-id="9b86d-200">hello 다음 예제에서는 라는 파일 공유 **myshare**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-200">hello following example creates a file share named **myshare**.</span></span>

```azurecli
azure storage share create myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="9b86d-201">디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="9b86d-201">Create a directory</span></span>
<span data-ttu-id="9b86d-202">디렉터리는 Azure 파일 공유에 대한 선택적 계층적 구조를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-202">A directory provides an optional hierarchical structure for an Azure file share.</span></span> <span data-ttu-id="9b86d-203">hello 다음 예에서는 라는 디렉터리를 만듭니다 **myDir** hello 파일 공유에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-203">hello following example creates a directory named **myDir** in hello file share.</span></span>

```azurecli
azure storage directory create myshare myDir
```

<span data-ttu-id="9b86d-204">해당 디렉터리 경로에 여러 수준이 포함 될 수 있습니다( *예:***a/b**).</span><span class="sxs-lookup"><span data-stu-id="9b86d-204">Note that directory path can include multiple levels, *e.g.*, **a/b**.</span></span> <span data-ttu-id="9b86d-205">그러나 모든 부모 디렉터리가 존재하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-205">However, you must ensure that all parent directories exist.</span></span> <span data-ttu-id="9b86d-206">예를 들어, 경로 **a/b**의 경우, 먼저 디렉터리 **a**를 만든 다음, **b** 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-206">For example, for path **a/b**, you must create directory **a** first, then create directory **b**.</span></span>

### <a name="upload-a-local-file-toodirectory"></a><span data-ttu-id="9b86d-207">로컬 파일 toodirectory 업로드</span><span class="sxs-lookup"><span data-stu-id="9b86d-207">Upload a local file toodirectory</span></span>
<span data-ttu-id="9b86d-208">hello 다음 예제에서는 파일을 업로드에서 **~/temp/samplefile.txt** toohello **myDir** 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-208">hello following example uploads a file from **~/temp/samplefile.txt** toohello **myDir** directory.</span></span> <span data-ttu-id="9b86d-209">로컬 컴퓨터에 유효한 파일이 tooa 가리키도록 hello 파일 경로 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-209">Edit hello file path so that it points tooa valid file on your local machine:</span></span>

```azurecli
azure storage file upload '~/temp/samplefile.txt' myshare myDir
```

<span data-ttu-id="9b86d-210">크기가 too1 TB를 hello 공유에 있는 파일 수 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-210">Note that a file in hello share can be up too1 TB in size.</span></span>

### <a name="list-hello-files-in-hello-share-root-or-directory"></a><span data-ttu-id="9b86d-211">Hello 공유 루트 디렉터리 또는 hello 파일 나열</span><span class="sxs-lookup"><span data-stu-id="9b86d-211">List hello files in hello share root or directory</span></span>
<span data-ttu-id="9b86d-212">Hello 파일 및 공유 루트 또는 hello 다음 명령을 사용 하 여 디렉터리에 하위 디렉터리를 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-212">You can list hello files and subdirectories in a share root or a directory using hello following command:</span></span>

```azurecli
azure storage file list myshare myDir
```

<span data-ttu-id="9b86d-213">Note hello 디렉터리 이름은 해당 hello 나열 작업에 대 한 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-213">Note that hello directory name is optional for hello listing operation.</span></span> <span data-ttu-id="9b86d-214">생략 하면 hello 명령은 hello 공유의 hello 루트 디렉터리의 hello 내용을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-214">If omitted, hello command lists hello contents of hello root directory of hello share.</span></span>

### <a name="copy-files"></a><span data-ttu-id="9b86d-215">파일 복사</span><span class="sxs-lookup"><span data-stu-id="9b86d-215">Copy files</span></span>
<span data-ttu-id="9b86d-216">버전 0.9.8 Azure cli 부터는 파일 tooanother 파일, 파일 tooa blob 또는 blob tooa 파일을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-216">Beginning with version 0.9.8 of Azure CLI, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="9b86d-217">아래에 대해서도 설명 tooperform 이러한 복사 방법 CLI 명령을 사용 하 여 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-217">Below we demonstrate how tooperform these copy operations using CLI commands.</span></span> <span data-ttu-id="9b86d-218">toocopy toohello 있는 새 파일 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="9b86d-218">toocopy a file toohello new directory:</span></span>

```azurecli
azure storage file copy start --source-share srcshare --source-path srcdir/hello.txt --dest-share destshare
    --dest-path destdir/hellocopy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

<span data-ttu-id="9b86d-219">toocopy blob tooa 파일 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="9b86d-219">toocopy a blob tooa file directory:</span></span>

```azurecli
azure storage file copy start --source-container srcctn --source-blob hello2.txt --dest-share hello
    --dest-path hellodir/hello2copy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

## <a name="next-steps"></a><span data-ttu-id="9b86d-220">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9b86d-220">Next Steps</span></span>

<span data-ttu-id="9b86d-221">여기 있는 저장소 리소스와 함께 사용할 수 있는 Azure CLI 1.0 명령 참조를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-221">You can find Azure CLI 1.0 command reference for working with Storage resources here:</span></span>

* [<span data-ttu-id="9b86d-222">Resource Manager 모드에서 Azure CLI 명령</span><span class="sxs-lookup"><span data-stu-id="9b86d-222">Azure CLI commands in Resource Manager mode</span></span>](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)
* [<span data-ttu-id="9b86d-223">Azure 서비스 관리 모드의 Azure CLI 명령</span><span class="sxs-lookup"><span data-stu-id="9b86d-223">Azure CLI commands in Azure Service Management mode</span></span>](../cli-install-nodejs.md)

<span data-ttu-id="9b86d-224">Tootry hello 또한 수 원하는 [Azure CLI 2.0](storage-azure-cli.md), Python, hello 리소스 관리자 배포 모델에 사용 하기 위해 작성 된 차세대 CLI 취급 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b86d-224">You may also like tootry hello [Azure CLI 2.0](storage-azure-cli.md), our next-generation CLI written in Python, for use with hello Resource Manager deployment model.</span></span>

[Image1]: ./media/storage-azure-cli/azure_command.png
