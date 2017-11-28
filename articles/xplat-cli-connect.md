---
title: "CLI에서 Azure에 로그인 | Microsoft Docs"
description: "Mac, Linux 및 Windows용 Azure 명령줄 인터페이스(Azure CLI)에서 Azure 구독에 연결"
editor: tysonn
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: ed856527-d75e-4e16-93fb-253dafad209d
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: rasquill
"\"/": 
ms.openlocfilehash: 31efab60690b54faf7992251fcd01e307c4464f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="log-in-to-azure-from-the-azure-cli"></a><span data-ttu-id="c127c-103">Azure CLI에서 Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="c127c-103">Log in to Azure from the Azure CLI</span></span>
<span data-ttu-id="c127c-104">Azure CLI는 Azure 리소스 작업을 위한 플랫폼 간 공개 소스 명령 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-104">The Azure CLI is a set of open-source, cross-platform commands for working with Azure resources.</span></span> <span data-ttu-id="c127c-105">이 문서에서는 Azure 계정 자격 증명을 제공하여 Azure CLI를 Azure 구독에 연결하는 다양한 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-105">This article describes the different ways to provide your Azure account credentials to connect the Azure CLI to your Azure subscription:</span></span>

* <span data-ttu-id="c127c-106">`azure login` CLI 명령을 실행하여 Azure Active Directory를 통해 인증을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-106">Run the `azure login` CLI command to authenticate through Azure Active Directory.</span></span> <span data-ttu-id="c127c-107">이 방법을 사용하면 두 [명령 모드](#cli-command-modes)에서 CLI 명령에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-107">This method gives you access to CLI commands in both [command modes](#cli-command-modes).</span></span> <span data-ttu-id="c127c-108">추가 옵션 없이 명령을 실행하면 `azure login`에서 웹 포털을 통해 대화형으로 계속 로그인할지 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-108">When you run the command without additional options, `azure login` prompts you to continue logging in interactively through a web portal.</span></span> <span data-ttu-id="c127c-109">추가 `azure login` 명령 옵션에 대해서는 이 문서의 시나리오를 참조하거나 `azure login --help`를 입력하세요.</span><span class="sxs-lookup"><span data-stu-id="c127c-109">For additional `azure login` command options, see the scenarios in this article, or type `azure login --help`.</span></span>
* <span data-ttu-id="c127c-110">Azure 서비스 관리 모드 CLI 명령만 사용해야 하는 경우(대부분의 새로운 배포에서는 권장되지 않음) 컴퓨터에 게시 설정 파일을 다운로드하고 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-110">If you only need to use Azure Service Management mode CLI commands (not recommended for most new deployments), you can download and install a publish settings file on your computer.</span></span>

<span data-ttu-id="c127c-111">이미 CLI를 설치하지 않은 경우 [Azure CLI 설치](cli-install-nodejs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c127c-111">If you haven't already installed the CLI, see [Install the Azure CLI](cli-install-nodejs.md).</span></span> <span data-ttu-id="c127c-112">Azure 구독이 없는 경우 몇 분 만에 [무료 계정](http://azure.microsoft.com/free/) 을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-112">If you don't have an Azure subscription, you can create a [free account](http://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="c127c-113">다른 계정 ID 및 Azure 구독에 대한 배경 정보는 [Azure 구독과 Azure Active Directory의 연관 관계](active-directory/active-directory-how-subscriptions-associated-directory.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c127c-113">For background about different account identities and Azure subscriptions, see [How Azure subscriptions are associated with Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md).</span></span>

## <a name="scenario-1-azure-login-with-interactive-login"></a><span data-ttu-id="c127c-114">시나리오 1: 대화형 로그인을 사용한 Azure 로그인</span><span class="sxs-lookup"><span data-stu-id="c127c-114">Scenario 1: azure login with interactive login</span></span>
<span data-ttu-id="c127c-115">특정 계정에서 CLI는 `azure login`을 실행한 후 웹 포털을 통해 웹 브라우저를 사용해서 로그인 프로세스를 계속 진행하도록 요구합니다. 이 프로세스를 *대화형 로그인*이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-115">With certain accounts, the CLI requires you to run `azure login` and then continue the login process with a web browser through a web portal, a process called *interactive login*.</span></span> <span data-ttu-id="c127c-116">일반적인 이유는 다단계 인증을 요구하도록 설정된 회사 또는 학교 계정(*조직 계정*이라고도 함)이 있는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-116">A common reason is when you have a work or school account (also called an *organizational account*) that is set up to require multifactor authentication.</span></span> <span data-ttu-id="c127c-117">또한 Resource Manager 모드 명령을 사용할 경우 Microsoft 계정으로 대화형 로그인을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-117">Also use interactive login with your Microsoft account, when you want to use Resource Manager mode commands.</span></span>

<span data-ttu-id="c127c-118">대화형 로그인은 쉽습니다. 다음 예제와 같이 아무 옵션도 없이 `azure login`을 입력하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-118">Interactive login is easy: type `azure login` -- without any options -- as shown in the following example:</span></span>

```
azure login
```                                                                                             

<span data-ttu-id="c127c-119">출력은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-119">The output appears something like the following:</span></span>

```         
info:    Executing command login
info:    To sign in, use a web browser to open the page http://aka.ms/devicelogin. Enter the code XXXXXXXXX to authenticate.
```
<span data-ttu-id="c127c-120">제공된 코드를 명령 출력에 복사하고 브라우저에서 http://aka.ms/devicelogin 또는 지정된 다른 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-120">Copy the code offered to you in the command output, and open a browser to http://aka.ms/devicelogin, or other page if specified.</span></span> <span data-ttu-id="c127c-121">(동일한 컴퓨터 또는 다른 컴퓨터나 장치에서 브라우저를 열 수 있습니다.) 코드를 입력하면 사용하려는 ID의 사용자 이름 및 암호를 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-121">(You can open a browser on the same computer, or on a different computer or device.) Enter the code, and then you are prompted to enter the username and password for the identity you want to use.</span></span> <span data-ttu-id="c127c-122">해당 프로세스가 완료되면 명령 셸이 로그인을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-122">When that process completes, the command shell completes the login.</span></span> <span data-ttu-id="c127c-123">다음과 같이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-123">It might look something like:</span></span>

    info:    Added subscription Visual Studio Ultimate with MSDN
    info:    Added subscription Azure Free Trial
    info:    Setting subscription "Visual Studio Ultimate with MSDN" as default
    +
    info:    login command OK

> [!NOTE]
> <span data-ttu-id="c127c-124">대화형 로그인을 사용할 경우 인증 및 권한 부여는 Azure Active Directory를 사용하여 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-124">With interactive login, authentication and authorization are performed using Azure Active Directory.</span></span> <span data-ttu-id="c127c-125">Microsoft 계정 ID를 사용하는 경우 로그인 프로세스에서 Azure Active Directory 기본 도메인에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-125">If you use a Microsoft account identity, the login process accesses your Azure Active Directory default domain.</span></span> <span data-ttu-id="c127c-126">무료 Azure 계정에 등록한 경우 Azure Active Directory에서 계정에 대한 기본 도메인이 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-126">(If you signed up for a free Azure account, Azure Active Directory automatically created a default domain for your account.)</span></span>
>
>

## <a name="scenario-2-azure-login-with-a-username-and-password"></a><span data-ttu-id="c127c-127">시나리오 2: 사용자 이름 및 암호를 사용한 Azure 로그인</span><span class="sxs-lookup"><span data-stu-id="c127c-127">Scenario 2: azure login with a username and password</span></span>
<span data-ttu-id="c127c-128">다단계 인증이 필요 없는 회사 또는 학교 계정을 사용하여 인증하려면 사용자 이름(`-u`) 매개 변수와 함께 `azure login` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-128">Use the `azure login` command with the username (`-u`) parameter to authenticate when you want to use a work or school account that doesn't require multifactor authentication.</span></span> <span data-ttu-id="c127c-129">명령줄에서 암호가 요구되거나 경우에 따라 `azure login` 명령의 추가 매개 변수로 암호를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-129">You are prompted at the command line for the password (or you can optionally pass the password as an additional parameter of the `azure login` command).</span></span> <span data-ttu-id="c127c-130">다음 예제에서는 조직 계정의 사용자 이름을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-130">The following example passes the username of an organizational account:</span></span>

    azure login -u myUserName@contoso.onmicrosoft.com

<span data-ttu-id="c127c-131">그런 다음 암호를 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-131">You are then prompted to enter your password:</span></span>

    info:    Executing command login
    Password: *********

<span data-ttu-id="c127c-132">그런 후에 로그인 프로세스가 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-132">The login process then completes.</span></span>

    info:    Added subscription Visual Studio Ultimate with MSDN
    +
    info:    login command OK

<span data-ttu-id="c127c-133">이러한 자격 증명으로 처음 로그인하는 경우 인증 토큰을 캐시할지 확인하는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-133">If this is your first time logging in with these credentials, you are asked to verify that you wish to cache an authentication token.</span></span> <span data-ttu-id="c127c-134">이 메시지는 `azure logout` 명령(이 문서의 뒷부분에 설명)을 이전에 사용한 경우에도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-134">This prompt also occurs if you previously used the `azure logout` command (described later in the article).</span></span> <span data-ttu-id="c127c-135">자동화 시나리오에서 이 메시지를 표시하지 않으려면 `-q` 매개 변수로 `azure login`을(를) 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-135">To bypass this prompt for automation scenarios, run `azure login` with the `-q` parameter.</span></span>

## <a name="scenario-3-azure-login-with-a-service-principal"></a><span data-ttu-id="c127c-136">시나리오 3: 서비스 사용자와 함께 Azure 로그인 사용</span><span class="sxs-lookup"><span data-stu-id="c127c-136">Scenario 3: azure login with a service principal</span></span>
<span data-ttu-id="c127c-137">Active Directory 응용 프로그램에 대한 서비스 사용자를 만들고 해당 서비스 사용자에게 구독에 대한 권한이 있는 경우 `azure login` 명령을 사용하여 서비스 사용자를 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-137">If you create a service principal for an Active Directory application, and the service principal has permissions on your subscription, you can use the `azure login` command to authenticate the service principal.</span></span> <span data-ttu-id="c127c-138">시나리오에 따라 서비스 사용자의 자격 증명을 `azure login` 명령의 명시적 매개 변수로 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-138">Depending on your scenario, you could provide the credentials of the service principal as explicit parameters of the `azure login` command.</span></span> <span data-ttu-id="c127c-139">예를 들어 다음 명령은 서비스 사용자 이름 및 Active Directory 테넌트 ID를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-139">For example, the following command passes the service principal name and Active Directory tenant ID:</span></span>

    azure login -u https://www.contoso.org/example --service-principal --tenant myTenantID

<span data-ttu-id="c127c-140">그런 다음 암호를 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-140">You are then prompted to provide the password.</span></span> <span data-ttu-id="c127c-141">CLI 스크립트 또는 응용 프로그램 코드를 통해 자격 증명을 제공하거나 인증서를 사용하여 자동화 시나리오에 맞게 비대화식으로 서비스 사용자를 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-141">You can also provide the credentials through a CLI script or application code, or use a certificate to authenticate the service principal non-interactively for automation scenarios.</span></span> <span data-ttu-id="c127c-142">자세한 내용 및 예제는 [Azure Resource Manager를 사용하여 서비스 사용자 인증](resource-group-authenticate-service-principal-cli.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c127c-142">For details and examples, see [Authenticating a service principal with Azure Resource Manager](resource-group-authenticate-service-principal-cli.md).</span></span>

## <a name="scenario-4-use-a-publish-settings-file"></a><span data-ttu-id="c127c-143">시나리오 4: 게시 설정 파일 사용</span><span class="sxs-lookup"><span data-stu-id="c127c-143">Scenario 4: Use a publish settings file</span></span>
<span data-ttu-id="c127c-144">Azure 서비스 관리 모드 CLI 명령만 사용해야 하는 경우(예를 들어 클래식 배포 모델에서 Azure VM을 배포하려는 경우) 게시 설정 파일을 사용하여 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-144">If you only need to use the Azure Service Management mode CLI commands (for example, to deploy Azure VMs in the classic deployment model), you can connect using a publish settings file.</span></span> <span data-ttu-id="c127c-145">이 방법은 구독 및 인증서가 유효한 경우 관리 작업을 수행할 수 있도록 로컬 컴퓨터에 인증서를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-145">This method installs a certificate on your local computer that allows you to perform management tasks for as long as the subscription and the certificate are valid.</span></span>

* <span data-ttu-id="c127c-146">계정에 대한 **게시 설정 파일을 다운로드하려면** `azure config mode asm`CLI가 서비스 관리 모드인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-146">**To download the publish settings file** for your account, ensure that the CLI is in Service Management mode by typing `azure config mode asm`.</span></span> <span data-ttu-id="c127c-147">그런 후 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-147">Then run the following command:</span></span>

        azure account download

<span data-ttu-id="c127c-148">기본 브라우저가 열리고 [Azure 클래식 포털](https://manage.windowsazure.com)에 로그인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-148">This opens your default browser and prompts you to sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="c127c-149">로그인하면 `.publishsettings` 파일이 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-149">After you sign in, a `.publishsettings` file downloads.</span></span> <span data-ttu-id="c127c-150">이 파일이 저장된 위치를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-150">Make note of where this file is saved.</span></span>

> [!NOTE]
> <span data-ttu-id="c127c-151">계정이 여러 개의 Azure Active Directory 테넌트와 연결된 경우 게시 설정 파일을 다운로드하려는 Active Directory를 선택하라는 메시지가 표시될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-151">If your account is associated with multiple Azure Active Directory tenants, you may be prompted to select which Active Directory you wish to download a publish settings file for.</span></span>
>
>

<span data-ttu-id="c127c-152">Azure 클래식 포털을 방문하여 다운로드 페이지를 사용하도록 선택한 후에는 선택한 Active Directory가 클래식 포털 및 다운로드 페이지에서 기본값으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-152">Once selected using the download page, or by visiting the Azure classic portal, the selected Active Directory becomes the default used by the classic portal and download page.</span></span> <span data-ttu-id="c127c-153">기본값이 설정되고 나면 다운로드 페이지의 맨 위에 '**선택 페이지로 돌아가려면 여기를 클릭하십시오.**' 텍스트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-153">Once a default has been established, you see the text '**click here to return to the selection page**' at the top of the download page.</span></span> <span data-ttu-id="c127c-154">제공된 링크를 사용하여 선택 페이지로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-154">Use the provided link to return to the selection page.</span></span>

* <span data-ttu-id="c127c-155">**게시 설정 파일을 가져오려면**다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-155">**To import the publish settings file**, run the following command:</span></span>

        azure account import <path to your .publishsettings file>

> [!IMPORTANT]
> <span data-ttu-id="c127c-156">게시 설정을 가져온 후에는 `.publishsettings` 파일을 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-156">After importing your publish settings, you should delete the `.publishsettings` file.</span></span> <span data-ttu-id="c127c-157">더 이상 Azure CLI에 필요하지 않으며 구독에 액세스하는 데 사용될 수 있으므로 보안상 위험하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-157">It is no longer required by the Azure CLI and presents a security risk as it could be used to gain access to your subscription.</span></span>
>
>

## <a name="cli-command-modes"></a><span data-ttu-id="c127c-158">CLI 명령 모드</span><span class="sxs-lookup"><span data-stu-id="c127c-158">CLI command modes</span></span>
<span data-ttu-id="c127c-159">Azure CLI는 Azure 리소스로 작업하는 두 가지 명령 모드(명령 집합이 서로 다름)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-159">The Azure CLI provides two command modes for working with Azure resources, with different command sets:</span></span>

* <span data-ttu-id="c127c-160">**Resource Manager 모드** - Resource Manager 배포 모델에서 Azure 리소스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-160">**Resource Manager mode** - for working with Azure resources in the Resource Manager deployment model.</span></span> <span data-ttu-id="c127c-161">이 모드를 설정하려면 `azure config mode arm`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-161">To set this mode, run `azure config mode arm`.</span></span>
* <span data-ttu-id="c127c-162">**서비스 관리 모드** - 클래식 배포 모델에서 Azure 리소스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-162">**Service Management mode** - for working with Azure resources in the classic deployment model.</span></span> <span data-ttu-id="c127c-163">이 모드를 설정하려면 `azure config mode asm`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-163">To set this mode, run `azure config mode asm`.</span></span>

<span data-ttu-id="c127c-164">처음 설치 시 CLI의 현재 릴리스는 Resource Manager 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-164">When first installed, the current release of the CLI is in Resource Manager mode.</span></span>

> [!NOTE]
> <span data-ttu-id="c127c-165">리소스 관리자 모드와 서비스 관리 모드는 함께 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-165">The Resource Manager mode and Service Management mode are mutually exclusive.</span></span> <span data-ttu-id="c127c-166">즉, 한 모드에서 만든 리소스는 다른 모드에서 관리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-166">That is, resources created in one mode cannot be managed from the other mode.</span></span>
>
>

## <a name="multiple-subscriptions"></a><span data-ttu-id="c127c-167">여러 구독</span><span class="sxs-lookup"><span data-stu-id="c127c-167">Multiple subscriptions</span></span>
<span data-ttu-id="c127c-168">Azure 구독이 여러 개 있는 경우 Azure에 연결하면 자격 증명과 연결된 모든 구독에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-168">If you have multiple Azure subscriptions, connecting to Azure grants access to all subscriptions associated with your credentials.</span></span> <span data-ttu-id="c127c-169">기본 구독으로 한 가지 구독이 선택되며, 작업을 수행할 때 Azure CLI에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-169">One subscription is selected as the default, and used by the Azure CLI when performing operations.</span></span> <span data-ttu-id="c127c-170">`azure account list` 명령을 사용하여 현재 기본 구독을 포함하는 구독을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-170">You can view the subscriptions, including the current default subscription, using the `azure account list` command.</span></span> <span data-ttu-id="c127c-171">이 명령은 다음과 유사한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-171">This command returns information similar to the following:</span></span>

    info:    Executing command account list
    data:    Name              Id                                    Current
    data:    ----------------  ------------------------------------  -------
    data:    Azure-sub-1       ####################################  true
    data:    Azure-sub-2       ####################################  false

<span data-ttu-id="c127c-172">위의 목록에서 **Current** 열은 현재 기본 구독으로 Azure-sub-1을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-172">In the preceding list, the **Current** column indicates the current default subscription as Azure-sub-1.</span></span> <span data-ttu-id="c127c-173">기본 구독을 변경하려면 `azure account set` 명령을 사용하고, 기본으로 사용할 구독을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-173">To change the default subscription, use the `azure account set` command, and specify the subscription that you wish to be the default.</span></span> <span data-ttu-id="c127c-174">예:</span><span class="sxs-lookup"><span data-stu-id="c127c-174">For example:</span></span>

    azure account set Azure-sub-2

<span data-ttu-id="c127c-175">이 경우 기본 구독이 Azure-sub-2로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-175">This changes the default subscription to Azure-sub-2.</span></span>

> [!NOTE]
> <span data-ttu-id="c127c-176">기본 구독을 변경하면 즉시 적용되며 전역적으로 변경됩니다. 동일한 명령줄 인스턴스에서 실행되거나 다른 인스턴스를 실행되는 새 Azure CLI 명령은 새 기본 구독을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-176">Changing the default subscription takes effect immediately, and is a global change; new Azure CLI commands, whether you run them from the same command-line instance or a different instance, use the new default subscription.</span></span>
>
>

<span data-ttu-id="c127c-177">Azure CLI와 함께 기본값이 아닌 구독을 사용하지만 현재 기본값을 변경하지 않으려는 경우 해당 명령에 대해 `--subscription` 옵션을 사용하고 작업에 사용할 구독의 이름을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-177">If you wish to use a non-default subscription with the Azure CLI, but don't want to change the current default, you can use the `--subscription` option for the command and provide the name of the subscription you wish to use for the operation.</span></span>

<span data-ttu-id="c127c-178">Azure 구독에 연결하게 되면 Azure CLI 명령을 사용하여 Azure 리소스 작업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-178">Once you are connected to your Azure subscription, you can start using the Azure CLI commands to work with Azure resources.</span></span>

## <a name="storage-of-cli-settings"></a><span data-ttu-id="c127c-179">CLI 설정 저장소</span><span class="sxs-lookup"><span data-stu-id="c127c-179">Storage of CLI settings</span></span>
<span data-ttu-id="c127c-180">`azure login` 명령을 사용하여 로그인하거나 게시 설정을 가져올 때 CLI 프로필과 로그가 `user` 디렉터리에 있는 `.azure` 디렉터리에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-180">Whether you log in with the `azure login` command or import publish settings, your CLI profile and logs are stored in a `.azure` directory located in your `user` directory.</span></span> <span data-ttu-id="c127c-181">`user` 디렉터리는 운영 체제에 의해 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-181">Your `user` directory is protected by your operating system.</span></span> <span data-ttu-id="c127c-182">그러나 추가 단계를 수행하여 `user` 디렉터리를 암호화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-182">However, we recommend that you take additional steps to encrypt your `user` directory.</span></span> <span data-ttu-id="c127c-183">다음과 같은 방법으로 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-183">You can do so in the following ways:</span></span>

* <span data-ttu-id="c127c-184">Windows에서는 디렉터리 속성을 수정하거나 BitLocker를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-184">On Windows, modify the directory properties or use BitLocker.</span></span>
* <span data-ttu-id="c127c-185">Mac에서는 디렉터리에 대해 FileVault를 켭니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-185">On Mac, turn on FileVault for the directory.</span></span>
* <span data-ttu-id="c127c-186">Ubuntu에서는 암호화된 홈 디렉터리 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-186">On Ubuntu, use the Encrypted Home directory feature.</span></span> <span data-ttu-id="c127c-187">기타 Linux 배포에서도 유사한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-187">Other Linux distributions offer similar features.</span></span>

## <a name="logging-out"></a><span data-ttu-id="c127c-188">로그아웃</span><span class="sxs-lookup"><span data-stu-id="c127c-188">Logging out</span></span>
<span data-ttu-id="c127c-189">로그아웃하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-189">To log out, use the following command:</span></span>

    azure logout -u <username>

<span data-ttu-id="c127c-190">계정과 연결된 구독이 Active Directory에서만 인증된 경우 로그아웃하면 구독 정보가 로컬 프로필에서 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-190">If the subscriptions associated with the account are only authenticated with Active Directory, logging out deletes the subscription information from the local profile.</span></span> <span data-ttu-id="c127c-191">그러나 구독에 대해 게시 설정 파일도 가져온 경우에는 로그아웃해도 Active Directory 관련 정보만 로컬 프로필에서 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="c127c-191">However, if a publish settings file was also imported for the subscriptions, logging out only deletes Active Directory related information from the local profile.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c127c-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c127c-192">Next steps</span></span>
* <span data-ttu-id="c127c-193">CLI 명령을 사용하려면 [Resource Manager 모드의 Azure CLI 명령](virtual-machines/azure-cli-arm-commands.md) 및 [서비스 관리 모드의 Azure CLI 명령](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c127c-193">To use Azure CLI commands, see [Azure CLI commands in Resource Manager mode](virtual-machines/azure-cli-arm-commands.md) and [Azure CLI commands in Service Management mode](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>
* <span data-ttu-id="c127c-194">Azure CLI에 대한 자세한 내용을 보거나, 소스 코드를 다운로드하거나, 문제를 보고하거나, 프로젝트에 기여하려면 [Azure CLI에 대한 GitHub 리포지토리](https://github.com/azure/azure-xplat-cli)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="c127c-194">To learn more about the Azure CLI, download source code, report problems, or contribute to the project, visit the [GitHub repository for the Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="c127c-195">Azure CLI 또는 Azure를 사용하는 데 문제가 있는 경우 [Azure 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="c127c-195">If you encounter problems using the Azure CLI, or Azure, visit the [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>
