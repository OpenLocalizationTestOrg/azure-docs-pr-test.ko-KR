---
title: "일괄 처리에 대 한 Azure CLI aaaGet 시작 | Microsoft Docs"
description: "간략 한 소개 toohello 일괄 처리의에서 명령을 가져오려면 Azure CLI Azure 배치 서비스 리소스를 관리 하기 위한"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: fcd76587-1827-4bc8-a84d-bba1cd980d85
ms.service: batch
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14f28311ecb16c8097d0d304a4ad89de282a2e9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-azure-cli"></a><span data-ttu-id="c820d-103">Azure CLI를 사용하여 Batch 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="c820d-103">Manage Batch resources with Azure CLI</span></span>

<span data-ttu-id="c820d-104">hello Azure CLI 2.0은 Azure 리소스 관리를 위해 Azure의 새로운 명령줄 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-104">hello Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="c820d-105">macOS, Linux 및 Windows에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-105">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="c820d-106">Azure CLI 2.0 hello 명령줄에서 Azure 리소스를 관리 및 관리 하기 위한 최적화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-106">Azure CLI 2.0 is optimized for managing and administering Azure resources from hello command line.</span></span> <span data-ttu-id="c820d-107">Azure 배치 계정 및 toomanage 리소스 풀, 작업, 작업 등 hello Azure CLI toomanage를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-107">You can use hello Azure CLI toomanage your Azure Batch accounts and toomanage resources such as pools, jobs, and tasks.</span></span> <span data-ttu-id="c820d-108">Azure CLI hello로 다양 한 hello 스크립팅할 수 있습니다 일괄 처리 Api, Azure 포털 및 일괄 처리 PowerShell cmdlet를 실행 하는 동일한 작업 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-108">With hello Azure CLI, you can script many of hello same tasks you carry out with hello Batch APIs, Azure portal, and Batch PowerShell cmdlets.</span></span>

<span data-ttu-id="c820d-109">이 문서에서는 Batch와 함께 [Azure CLI 버전 2.0](https://docs.microsoft.com/cli/azure/overview)을 사용하는 방법에 대해 간략히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-109">This article provides an overview of using [Azure CLI version 2.0](https://docs.microsoft.com/cli/azure/overview) with Batch.</span></span> <span data-ttu-id="c820d-110">참조 [Azure CLI 2.0 시작](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) hello CLI를 사용 하 여 azure에 대 한 개요입니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-110">See [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) for an overview of using hello CLI with Azure.</span></span>

<span data-ttu-id="c820d-111">Hello hello Azure CLI 버전 2.0의 최신 버전을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-111">Microsoft recommends using hello latest version of hello Azure CLI, version 2.0.</span></span> <span data-ttu-id="c820d-112">버전 2.0에 대한 자세한 내용은 [현재 일반적으로 사용할 수 있는 Azure CLI 2.0](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c820d-112">For more information about version 2.0, see [Azure Command Line 2.0 now generally available](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/).</span></span>

## <a name="set-up-hello-azure-cli"></a><span data-ttu-id="c820d-113">Hello Azure CLI 설정</span><span class="sxs-lookup"><span data-stu-id="c820d-113">Set up hello Azure CLI</span></span>

<span data-ttu-id="c820d-114">에 설명 된 hello 단계를 수행 하는 tooinstall hello Azure CLI [설치 hello Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-114">tooinstall hello Azure CLI, follow hello steps outlined in [Install hello Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli.md).</span></span>

> [!TIP]
> <span data-ttu-id="c820d-115">Azure CLI 설치를 업데이트 하는 것이 좋습니다 자주 tootake 활용 해도 서비스 업데이트 및 향상 된 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-115">We recommend that you update your Azure CLI installation frequently tootake advantage of service updates and enhancements.</span></span>
> 
> 

## <a name="command-help"></a><span data-ttu-id="c820d-116">명령 도움말</span><span class="sxs-lookup"><span data-stu-id="c820d-116">Command help</span></span>

<span data-ttu-id="c820d-117">추가 하 여 hello Azure CLI에에서는 모든 명령에 대 한 도움말 텍스트를 표시할 수 있습니다 `-h` toohello 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-117">You can display help text for every command in hello Azure CLI by appending `-h` toohello command.</span></span> <span data-ttu-id="c820d-118">다른 모든 옵션은 생략합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-118">Omit any other options.</span></span> <span data-ttu-id="c820d-119">예:</span><span class="sxs-lookup"><span data-stu-id="c820d-119">For example:</span></span>

* <span data-ttu-id="c820d-120">hello에 대 한 도움말 tooget `az` 명령 입력 합니다.`az -h`</span><span class="sxs-lookup"><span data-stu-id="c820d-120">tooget help for hello `az` command, enter: `az -h`</span></span>
* <span data-ttu-id="c820d-121">tooget CLI hello에서 모든 일괄 처리 명령의 목록을 사용 합니다.`az batch -h`</span><span class="sxs-lookup"><span data-stu-id="c820d-121">tooget a list of all Batch commands in hello CLI, use: `az batch -h`</span></span>
* <span data-ttu-id="c820d-122">일괄 처리 계정을 만드는 방법에 대 한 tooget 도움말을 입력 합니다.`az batch account create -h`</span><span class="sxs-lookup"><span data-stu-id="c820d-122">tooget help on creating a Batch account, enter: `az batch account create -h`</span></span>

<span data-ttu-id="c820d-123">의심에서 hello를 사용 하 여 `-h` 모든 Azure CLI 명령에 대 한 명령줄 옵션 tooget 도움말입니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-123">When in doubt, use hello `-h` command-line option tooget help on any Azure CLI command.</span></span>

> [!NOTE]
> <span data-ttu-id="c820d-124">이전 버전의 hello 사용 되는 Azure CLI `azure` toopreface CLI 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-124">Earlier versions of hello Azure CLI used `azure` toopreface a CLI command.</span></span> <span data-ttu-id="c820d-125">버전 2.0에서는 이제 모든 명령 앞에 `az`를 사용하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-125">In version 2.0, all commands are now prefaced with `az`.</span></span> <span data-ttu-id="c820d-126">있는지 tooupdate 버전 2.0과 스크립트 toouse hello 새 구문을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-126">Be sure tooupdate your scripts toouse hello new syntax with version 2.0.</span></span>
>
>  

<span data-ttu-id="c820d-127">또한에 대 한 자세한 내용은 toohello Azure CLI 참조 설명서를 참조할 [일괄 처리에 대 한 Azure CLI 명령을](https://docs.microsoft.com/cli/azure/batch)합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-127">Additionally, refer toohello Azure CLI reference documentation for details about [Azure CLI commands for Batch](https://docs.microsoft.com/cli/azure/batch).</span></span> 

## <a name="log-in-and-authenticate"></a><span data-ttu-id="c820d-128">로그인 및 인증</span><span class="sxs-lookup"><span data-stu-id="c820d-128">Log in and authenticate</span></span>

<span data-ttu-id="c820d-129">toouse hello Azure CLI, 일괄 처리에서 toolog 필요 하 고이 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-129">toouse hello Azure CLI with Batch, you need toolog in and authenticate.</span></span> <span data-ttu-id="c820d-130">두 가지 간단한 단계만 거치면 toofollow 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-130">There are two simple steps toofollow:</span></span>

1. <span data-ttu-id="c820d-131">**Azure에 로그인합니다.**</span><span class="sxs-lookup"><span data-stu-id="c820d-131">**Log into Azure.**</span></span> <span data-ttu-id="c820d-132">포함 하 여 리소스 관리자 tooAzure 명령을 액세스 제공 Azure에 로그인 할 [일괄 처리 관리 서비스](batch-management-dotnet.md) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-132">Logging into Azure gives you access tooAzure Resource Manager commands, including [Batch Management service](batch-management-dotnet.md) commands.</span></span>  
2. <span data-ttu-id="c820d-133">**배치 계정에 로그인합니다.**</span><span class="sxs-lookup"><span data-stu-id="c820d-133">**Log into your Batch account.**</span></span> <span data-ttu-id="c820d-134">일괄 처리 계정 제공에 로그인 할 tooBatch 서비스 명령 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-134">Logging into your Batch account gives you access tooBatch service commands.</span></span>   

### <a name="log-in-tooazure"></a><span data-ttu-id="c820d-135">TooAzure 로그인</span><span class="sxs-lookup"><span data-stu-id="c820d-135">Log in tooAzure</span></span>

<span data-ttu-id="c820d-136">에 자세하게 설명 Azure에 몇 가지 방법으로 toolog 가지 [Azure CLI 2.0 로그인](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):</span><span class="sxs-lookup"><span data-stu-id="c820d-136">There are a few different ways toolog into Azure, described in detail in [Log in with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):</span></span>

1. <span data-ttu-id="c820d-137">[대화형으로 로그인합니다](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in).</span><span class="sxs-lookup"><span data-stu-id="c820d-137">[Log in interactively](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in).</span></span> <span data-ttu-id="c820d-138">로그인 대화형으로 실행 하는 경우 Azure CLI 명령을 직접 hello 명령줄에서.</span><span class="sxs-lookup"><span data-stu-id="c820d-138">Log in interactively when you are running Azure CLI commands yourself from hello command line.</span></span>
2. <span data-ttu-id="c820d-139">[서비스 주체를 사용하여 로그인합니다](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="c820d-139">[Log in with a service principal](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal).</span></span> <span data-ttu-id="c820d-140">스크립트 또는 응용 프로그램에서 Azure CLI 명령을 실행할 때 서비스 주체를 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-140">Log in with a service principal when you are running Azure CLI commands from a script or an application.</span></span>

<span data-ttu-id="c820d-141">이 문서의 hello 위해 보여줍니다 어떻게 toolog Azure에 대화형으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-141">For hello purposes of this article, we show how toolog into Azure interactively.</span></span> <span data-ttu-id="c820d-142">형식 [az 로그인](https://docs.microsoft.com/cli/azure/#login) hello 명령줄에서:</span><span class="sxs-lookup"><span data-stu-id="c820d-142">Type [az login](https://docs.microsoft.com/cli/azure/#login) on hello command line:</span></span>

```azurecli
# Log in tooAzure and authenticate interactively.
az login
```

<span data-ttu-id="c820d-143">hello `az login` 명령은 다음과 같이 tooauthenticate를 사용할 수 있는 토큰을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-143">hello `az login` command returns a token that you can use tooauthenticate, as shown here.</span></span> <span data-ttu-id="c820d-144">Hello 제공 된 지침 tooopen 웹 페이지를 따르고 hello 토큰 tooAzure 제출:</span><span class="sxs-lookup"><span data-stu-id="c820d-144">Follow hello instructions provided tooopen a web page and submit hello token tooAzure:</span></span>

![TooAzure 로그인](./media/batch-cli-get-started/az-login.png)

<span data-ttu-id="c820d-146">hello에 나열 된 hello 예제 [셸 스크립트 샘플](#sample-shell-scripts) 표시 방법을 섹션도 toostart 대화형으로 Azure에 로그인 하 여 Azure CLI 세션입니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-146">hello examples listed in hello [Sample shell scripts](#sample-shell-scripts) section also show how toostart your Azure CLI session by logging into Azure interactively.</span></span> <span data-ttu-id="c820d-147">로그인 하면 일괄 처리 계정, 키, 응용 프로그램 패키지 및 할당량을 포함 하 여 일괄 처리 관리 리소스와 toowork 명령을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-147">Once you have logged in, you can call commands toowork with Batch Management resources, including Batch accounts, keys, application packages, and quotas.</span></span>  

### <a name="log-in-tooyour-batch-account"></a><span data-ttu-id="c820d-148">일괄 처리 계정 tooyour에 로그인</span><span class="sxs-lookup"><span data-stu-id="c820d-148">Log in tooyour Batch account</span></span>

<span data-ttu-id="c820d-149">toouse hello Azure CLI toomanage 일괄 처리와 같은 리소스 풀, 작업, 작업, 일괄 처리 계정에 toolog 필요 하 고 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-149">toouse hello Azure CLI toomanage Batch resources, such as pools, jobs, and tasks, you need toolog into your Batch account and authenticate.</span></span> <span data-ttu-id="c820d-150">toolog toohello 일괄 처리 서비스에서에서 사용 하 여 hello [az 일괄 처리 계정 로그인](https://docs.microsoft.com/cli/azure/batch/account#login) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-150">toolog in toohello Batch service, use hello [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) command.</span></span> 

<span data-ttu-id="c820d-151">배치 계정에 대한 인증에는 다음 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-151">You have two options for authenticating against your Batch account:</span></span>

- <span data-ttu-id="c820d-152">**Azure AD(Azure Active Directory) 인증 사용**</span><span class="sxs-lookup"><span data-stu-id="c820d-152">**By using Azure Active Directory (Azure AD) authentication.**</span></span> 

    <span data-ttu-id="c820d-153">Azure AD를 사용 하 여 인증 hello 기본 hello Azure CLI를 사용 하 여 일괄 처리를 사용 하는 경우 이며 대부분의 시나리오에 대 한 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-153">Authenticating with Azure AD is hello default when you use hello Azure CLI with Batch, and recommended for most scenarios.</span></span> 
    
    <span data-ttu-id="c820d-154">TooAzure를 대화형으로 hello 이전 섹션에 설명 된 대로 로그인 할 때 하므로 hello Azure CLI tooyour 동일한 자격 증명을 사용 하 여 일괄 처리 계정 로그인 자격 증명 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-154">When you log in tooAzure interactively, as described in hello previous section, your credentials are cached, so hello Azure CLI can log you in tooyour Batch account using those same credentials.</span></span> <span data-ttu-id="c820d-155">서비스 사용자를 사용 하 여 tooAzure 로그인 하면 해당 자격 증명 tooyour 일괄 처리 계정에에서 사용 되는 toolog도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-155">If you log in tooAzure using a service principal, those credentials are also used toolog in tooyour Batch account.</span></span>

    <span data-ttu-id="c820d-156">Azure AD의 이점은 RBAC(역할 기반 액세스 제어)를 제공한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-156">An advantage of Azure AD is that it offers role-based access control (RBAC).</span></span> <span data-ttu-id="c820d-157">RBAC는 사용자의 액세스에 따라 달라 집니다 할당된 된 역할 보다 hello 계정 키 소유 해야 할지 여부는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-157">With RBAC, a user's access depends on their assigned role, rather than whether or not they possess hello account keys.</span></span> <span data-ttu-id="c820d-158">계정 키를 관리하는 대신 RBAC 역할을 관리하고 Azure AD에서 액세스와 인증을 처리하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-158">Instead of managing account keys, you can manage RBAC roles, and let Azure AD handle access and authentication.</span></span>  

    <span data-ttu-id="c820d-159">Azure AD를 사용 하 여 인증 필수가 만든 경우 해당 풀 할당 모드를 사용 하 여 Azure 배치 계정 설정 too'User 구독 '.</span><span class="sxs-lookup"><span data-stu-id="c820d-159">Authenticating with Azure AD is required if you created your Azure Batch account with its pool allocation mode set too'User Subscription'.</span></span> 

    <span data-ttu-id="c820d-160">Azure AD를 사용 하 여 계정, hello 호출이 tooyour 일괄 처리에서에서 toolog [az 일괄 처리 계정 로그인](https://docs.microsoft.com/cli/azure/batch/account#login) 명령:</span><span class="sxs-lookup"><span data-stu-id="c820d-160">toolog in tooyour Batch account using Azure AD, call hello [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) command:</span></span> 

    ```azurecli
    az batch account login -g myresource group -n mybatchaccount
    ```

- <span data-ttu-id="c820d-161">**공유 키 인증 사용**</span><span class="sxs-lookup"><span data-stu-id="c820d-161">**By using Shared Key authentication.**</span></span>

    <span data-ttu-id="c820d-162">[공유 키 인증](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) 계정 액세스 키 hello에 대 한 tooauthenticate Azure CLI 명령을 사용 하 여 서비스를 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-162">[Shared Key authentication](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) uses your account access keys tooauthenticate Azure CLI commands for hello Batch service.</span></span>

    <span data-ttu-id="c820d-163">스크립트를 만드는 Azure CLI tooautomate 호출 일괄 처리 명령, 공유 키 인증 또는 Azure AD 서비스 사용자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-163">If you are creating Azure CLI scripts tooautomate calling Batch commands, you can use either Shared Key authentication, or an Azure AD service principal.</span></span> <span data-ttu-id="c820d-164">일부 시나리오에서는 공유 키 인증을 사용하는 것이 서비스 주체를 만드는 것보다 더 간단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-164">In some scenarios, using Shared Key authentication may be simpler than creating a service principal.</span></span>  

    <span data-ttu-id="c820d-165">공유 키 인증을 사용 하 여 toolog 포함 hello `--shared-key-auth` hello 명령줄 옵션에:</span><span class="sxs-lookup"><span data-stu-id="c820d-165">toolog in using Shared Key authentication, include hello `--shared-key-auth` option on hello command line:</span></span>

    ```azurecli
    az batch account login -g myresourcegroup -n mybatchaccount --shared-key-auth
    ```

<span data-ttu-id="c820d-166">hello에 나열 된 hello 예제 [셸 스크립트 샘플](#sample-shell-scripts) 섹션 toolog 일괄 처리 계정에 모두 사용 하 여 Azure CLI hello 하는 방법을 보여 줍니다. Azure AD와 공유 키입니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-166">hello examples listed in hello [Sample shell scripts](#sample-shell-scripts) section show how toolog into your Batch account with hello Azure CLI using both Azure AD and Shared Key.</span></span>

## <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a><span data-ttu-id="c820d-167">Azure Batch CLI 템플릿 및 파일 전송 사용(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="c820d-167">Use Azure Batch CLI Templates and File Transfer (Preview)</span></span>

<span data-ttu-id="c820d-168">Hello Azure CLI toorun 일괄 처리 작업에 종단 간 코드를 작성 하지 않고도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-168">You can use hello Azure CLI toorun Batch jobs end-to-end without writing code.</span></span> <span data-ttu-id="c820d-169">일괄 처리 템플릿 파일 만드는 풀, 작업, 및 hello Azure CLI를 사용 하 여 작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-169">Batch template files support creating pools, jobs, and tasks with hello Azure CLI.</span></span> <span data-ttu-id="c820d-170">Hello Azure CLI tooupload 작업 입력된 파일을 사용할 수도 있습니다 toohello Azure 저장소 계정을 hello와 연결 된 일괄 처리 계정을, 및에서 작업 출력 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-170">You can also use hello Azure CLI tooupload job input files toohello Azure Storage account associated with hello Batch account, and download job output files from it.</span></span> <span data-ttu-id="c820d-171">자세한 내용은 [Azure Batch CLI 템플릿 및 파일 전송 사용(미리 보기)](batch-cli-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c820d-171">For more information, see [Use Azure Batch CLI Templates and File Transfer (Preview)](batch-cli-templates.md).</span></span>

## <a name="sample-shell-scripts"></a><span data-ttu-id="c820d-172">샘플 셸 스크립트</span><span class="sxs-lookup"><span data-stu-id="c820d-172">Sample shell scripts</span></span>

<span data-ttu-id="c820d-173">hello 일괄 처리 서비스 및 일괄 처리 관리 서비스 tooaccomplish 일반적인 작업으로 toouse Azure CLI 명령을 하는 방법을 hello 테이블 표시 뒤에 나열 된 hello 예제 스크립트.</span><span class="sxs-lookup"><span data-stu-id="c820d-173">hello sample scripts listed in hello following table show how toouse Azure CLI commands with hello Batch service and Batch Management service tooaccomplish common tasks.</span></span> <span data-ttu-id="c820d-174">이 샘플 스크립트 다양 한 일괄 처리에 대 한 Azure CLI hello에서 사용할 수 있는 hello 명령을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-174">These sample scripts cover many of hello commands available in hello Azure CLI for Batch.</span></span> 

| <span data-ttu-id="c820d-175">스크립트</span><span class="sxs-lookup"><span data-stu-id="c820d-175">Script</span></span> | <span data-ttu-id="c820d-176">참고 사항</span><span class="sxs-lookup"><span data-stu-id="c820d-176">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c820d-177">배치 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="c820d-177">Create a Batch account</span></span>](./scripts/batch-cli-sample-create-account.md) | <span data-ttu-id="c820d-178">배치 계정을 만들고 저장소 계정과 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-178">Creates a Batch account and associates it with a storage account.</span></span> |
| [<span data-ttu-id="c820d-179">응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="c820d-179">Add an application</span></span>](./scripts/batch-cli-sample-add-application.md) | <span data-ttu-id="c820d-180">응용 프로그램을 추가하고 패키지된 이진 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-180">Adds an application and uploads packaged binaries.</span></span>|
| [<span data-ttu-id="c820d-181">Batch 풀 관리</span><span class="sxs-lookup"><span data-stu-id="c820d-181">Manage Batch pools</span></span>](./scripts/batch-cli-sample-manage-pool.md) | <span data-ttu-id="c820d-182">풀을 만들고, 크기 조정하며, 관리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-182">Demonstrates creating, resizing, and managing pools.</span></span> |
| [<span data-ttu-id="c820d-183">Batch로 작업 및 태스크 실행</span><span class="sxs-lookup"><span data-stu-id="c820d-183">Run a job and tasks with Batch</span></span>](./scripts/batch-cli-sample-run-job.md) | <span data-ttu-id="c820d-184">작업 실행 및 태스크 추가를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-184">Demonstrates running a job and adding tasks.</span></span> |

## <a name="json-files-for-resource-creation"></a><span data-ttu-id="c820d-185">리소스를 만들기 위한 JSON 파일</span><span class="sxs-lookup"><span data-stu-id="c820d-185">JSON files for resource creation</span></span>

<span data-ttu-id="c820d-186">풀 및 작업 같은 일괄 처리 리소스를 만들 때에 명령줄 옵션으로 해당 매개 변수를 전달 하는 대신 hello 새 리소스의 구성이 포함 된 JSON 파일을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-186">When you create Batch resources like pools and jobs, you can specify a JSON file containing hello new resource's configuration instead of passing its parameters as command-line options.</span></span> <span data-ttu-id="c820d-187">예:</span><span class="sxs-lookup"><span data-stu-id="c820d-187">For example:</span></span>

```azurecli
az batch pool create my_batch_pool.json
```

<span data-ttu-id="c820d-188">명령줄 옵션에만 사용 하 여 대부분의 일괄 처리 리소스를 만들 수 있지만 hello 리소스 세부 정보를 포함 하는 JSON 형식의 파일을 지정 하는 일부 기능이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-188">While you can create most Batch resources using only command-line options, some features require that you specify a JSON-formatted file containing hello resource details.</span></span> <span data-ttu-id="c820d-189">예를 들어 시작 작업에 대 한 리소스 파일 toospecify JSON 파일을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-189">For example, you must use a JSON file if you want toospecify resource files for a start task.</span></span>

<span data-ttu-id="c820d-190">JSON 구문 toosee hello 필수 toocreate 리소스, toohello 참조 [배치 REST API 참조] [ rest_api] 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-190">toosee hello JSON syntax required toocreate a resource, refer toohello [Batch REST API reference][rest_api] documentation.</span></span> <span data-ttu-id="c820d-191">각 "추가 *리소스 종류*" hello REST API 참조의에서 항목을 해당 리소스를 만들기 위한 샘플 JSON 스크립트를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-191">Each "Add *resource type*" topic in hello REST API reference contains sample JSON scripts for creating that resource.</span></span> <span data-ttu-id="c820d-192">JSON 파일 toouse hello Azure CLI로에 대 한 템플릿으로 이러한 샘플 JSON 스크립트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-192">You can use those sample JSON scripts as templates for JSON files toouse with hello Azure CLI.</span></span> <span data-ttu-id="c820d-193">예를 들어 너무 toosee hello 풀 만들기에 대 한 JSON 구문을 참조[풀 tooan 계정 추가][rest_add_pool]합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-193">For example, toosee hello JSON syntax for pool creation, refer too[Add a pool tooan account][rest_add_pool].</span></span>

<span data-ttu-id="c820d-194">JSON 파일을 지정하는 샘플 스크립트는 [Batch로 작업 및 태스크 실행](./scripts/batch-cli-sample-run-job.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c820d-194">For a sample script that specifies a JSON file, see [Run a job and tasks with Batch](./scripts/batch-cli-sample-run-job.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c820d-195">리소스를 만들 때 JSON 파일을 지정 하는 경우 해당 리소스에 대 한 hello 명령줄에서 지정 하는 다른 매개 변수는 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-195">If you specify a JSON file when you create a resource, any other parameters that you specify on hello command line for that resource are ignored.</span></span>
> 
> 

## <a name="efficient-queries-for-batch-resources"></a><span data-ttu-id="c820d-196">Batch 리소스에 대한 효율적 쿼리</span><span class="sxs-lookup"><span data-stu-id="c820d-196">Efficient queries for Batch resources</span></span>

<span data-ttu-id="c820d-197">각 Batch 리소스 유형은 배치 계정을 쿼리하고 해당 형식의 리소스를 나열하는 `list` 명령을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-197">Each Batch resource type supports a `list` command that queries your Batch account and lists resources of that type.</span></span> <span data-ttu-id="c820d-198">예를 들어 hello 풀에서 작업 계정 및 hello 작업에 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-198">For example, you can list hello pools in your account and hello tasks in a job:</span></span>

```azurecli
az batch pool list
az batch task list --job-id job001
```

<span data-ttu-id="c820d-199">Hello 일괄 처리 서비스를 쿼리할 때는 `list` 작업에서 반환 된 데이터는 OData 절 toolimit hello 양을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-199">When you query hello Batch service with a `list` operation, you can specify an OData clause toolimit hello amount of data returned.</span></span> <span data-ttu-id="c820d-200">모든 필터링 서버 쪽 나타나므로 요청 hello 데이터만 hello 와이어를 교차 합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-200">Because all filtering occurs server-side, only hello data you request crosses hello wire.</span></span> <span data-ttu-id="c820d-201">이러한 절 toosave 대역폭을 사용 하 여 (및 따라서 시간) 목록 작업을 수행 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="c820d-201">Use these clauses toosave bandwidth (and therefore time) when you perform list operations.</span></span>

<span data-ttu-id="c820d-202">hello 다음 표에서 설명 hello 일괄 처리 서비스에서 지 원하는 hello OData 절:</span><span class="sxs-lookup"><span data-stu-id="c820d-202">hello following table describes hello OData clauses supported by hello Batch service:</span></span>

| <span data-ttu-id="c820d-203">절</span><span class="sxs-lookup"><span data-stu-id="c820d-203">Clause</span></span> | <span data-ttu-id="c820d-204">설명</span><span class="sxs-lookup"><span data-stu-id="c820d-204">Description</span></span> |
|---|---|
| `--select-clause [select-clause]` | <span data-ttu-id="c820d-205">각 엔터티에 대한 속성의 하위 집합을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-205">Returns a subset of properties for each entity.</span></span> |
| `--filter-clause [filter-clause]` | <span data-ttu-id="c820d-206">Hello와 일치 하는 엔터티만 반환 OData 식 지정.</span><span class="sxs-lookup"><span data-stu-id="c820d-206">Returns only entities that match hello specified OData expression.</span></span> |
| `--expand-clause [expand-clause]` | <span data-ttu-id="c820d-207">단일 기본 REST 호출의 hello 엔터티 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-207">Obtains hello entity information in a single underlying REST call.</span></span> <span data-ttu-id="c820d-208">hello 확장 지원만 hello 현재을 절 `stats` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-208">hello expand clause currently supports only hello `stats` property.</span></span> |

<span data-ttu-id="c820d-209">샘플 toouse OData 절을 참조 하는 방법을 보여 줍니다 해당 스크립트에 대 한 [일괄 처리 작업 및 작업을 실행](./scripts/batch-cli-sample-run-job.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-209">For a sample script that shows how toouse an OData clause, see [Run a job and tasks with Batch](./scripts/batch-cli-sample-run-job.md).</span></span>

<span data-ttu-id="c820d-210">OData 절과 함께 효율적인 목록 쿼리 수행에 대 한 자세한 내용은 참조 하십시오. [hello Azure 배치 서비스를 효율적으로 쿼리](batch-efficient-list-queries.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-210">For more information on performing efficient list queries with OData clauses, see [Query hello Azure Batch service efficiently](batch-efficient-list-queries.md).</span></span>

## <a name="troubleshooting-tips"></a><span data-ttu-id="c820d-211">문제 해결 팁</span><span class="sxs-lookup"><span data-stu-id="c820d-211">Troubleshooting tips</span></span>

<span data-ttu-id="c820d-212">hello 다음 사항을 참고 Azure CLI 문제를 해결 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="c820d-212">hello following tips may help when you are troubleshooting Azure CLI issues:</span></span>

* <span data-ttu-id="c820d-213">사용 하 여 `-h` tooget **도움말 텍스트** 모든 CLI 명령에 대 한</span><span class="sxs-lookup"><span data-stu-id="c820d-213">Use `-h` tooget **help text** for any CLI command</span></span>
* <span data-ttu-id="c820d-214">사용 하 여 `-v` 및 `-vv` toodisplay **verbose** 출력 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-214">Use `-v` and `-vv` toodisplay **verbose** command output.</span></span> <span data-ttu-id="c820d-215">Hello 때 `-vv` 플래그를 포함 hello Azure CLI hello 실제 REST 요청 및 응답이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-215">When hello `-vv` flag is included, hello Azure CLI displays hello actual REST requests and responses.</span></span> <span data-ttu-id="c820d-216">이러한 스위치는 전체 오류 출력을 표시하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-216">These switches are handy for displaying full error output.</span></span>
* <span data-ttu-id="c820d-217">볼 수 있습니다 **JSON으로 출력 명령** hello로 `--json` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-217">You can view **command output as JSON** with hello `--json` option.</span></span> <span data-ttu-id="c820d-218">예를 들어 `az batch pool show pool001 --json` 은 JSON 형식으로 pool001의 속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-218">For example, `az batch pool show pool001 --json` displays pool001's properties in JSON format.</span></span> <span data-ttu-id="c820d-219">그런 다음 복사 하 고 수정할 수에서이 출력 toouse는 `--json-file` (참조 [JSON 파일](#json-files) 이 문서의 앞부분에).</span><span class="sxs-lookup"><span data-stu-id="c820d-219">You can then copy and modify this output toouse in a `--json-file` (see [JSON files](#json-files) earlier in this article).</span></span>
<!---Loc Comment: Please, check link [JSON files] since it's not redirecting tooany location.--->
* <span data-ttu-id="c820d-220">hello [배치 포럼] [ batch_forum] 일괄 처리 팀 구성원이 모니터링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-220">hello [Batch forum][batch_forum] is monitored by Batch team members.</span></span> <span data-ttu-id="c820d-221">문제가 발생하거나 특정 작업에 도움이 필요한 경우 질문을 여기에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-221">You can post your questions there if you run into issues or would like help with a specific operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c820d-222">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c820d-222">Next steps</span></span>

* <span data-ttu-id="c820d-223">Azure CLI hello에 대 한 자세한 내용은 참조 hello [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-223">For more information about hello Azure CLI, see hello [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>
* <span data-ttu-id="c820d-224">Batch 리소스에 대한 자세한 내용은 [개발자를 위한 Azure Batch 개요](batch-api-basics.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c820d-224">For more information about Batch resources, see [Overview of Azure Batch for developers](batch-api-basics.md).</span></span>
* <span data-ttu-id="c820d-225">일괄 처리 템플릿 toocreate 풀, 작업 및 작업을 사용 하 여 코드를 작성 하지 않고도 하는 방법에 대 한 자세한 내용은 참조 [Azure 일괄 처리 CLI 템플릿 및 파일 전송 (미리 보기)](batch-cli-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c820d-225">For more information about using Batch templates toocreate pools, jobs, and tasks without writing code, see [Use Azure Batch CLI Templates and File Transfer (Preview)](batch-cli-templates.md).</span></span>

[batch_forum]: https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch
[github_readme]: https://github.com/Azure/azure-xplat-cli/blob/dev/README.md
[rest_api]: https://msdn.microsoft.com/library/azure/dn820158.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
