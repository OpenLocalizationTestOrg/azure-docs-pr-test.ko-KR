---
title: "aaaInstall 및 Azure에서 Terraform tooprovision Vm 및 기타 인프라 구성 | Microsoft Docs"
description: "자세한 내용은 방법 tooinstall Terraform toocreate Azure 구성 및 리소스"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: echuvyrov
manager: jtalkar
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: echuvyrov
ms.openlocfilehash: b6706f53b21347442def05a592c30a2d22718984
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-terraform-tooprovision-vms-and-other-infrastructure-into-azure"></a><span data-ttu-id="74f03-103">설치 하 고 Azure에 Terraform tooprovision Vm 및 기타 인프라 구성</span><span class="sxs-lookup"><span data-stu-id="74f03-103">Install and configure Terraform tooprovision VMs and other infrastructure into Azure</span></span> 
<span data-ttu-id="74f03-104">이 문서 hello 필요한 단계 tooinstall에 설명 하 고 Azure에 가상 컴퓨터와 같은 Terraform tooprovision 리소스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-104">This article describes hello necessary steps tooinstall and configure Terraform tooprovision resources such as virtual machines into Azure.</span></span> <span data-ttu-id="74f03-105">어떻게 toocreate 및 Azure 사용 하 여 자격 증명 tooenable Terraform tooprovision 클라우드 리소스에 안전 하 게 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-105">You will learn how toocreate and use Azure credentials tooenable Terraform tooprovision cloud resources in a secure manner.</span></span>

<span data-ttu-id="74f03-106">HashiCorp Terraform 쉽게 toodefine 제공 하 고 HashiCorp 구성 언어 (HCL) 이라는 사용자 지정 템플릿 언어를 사용 하 여 클라우드 인프라를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-106">HashiCorp Terraform provides an easy way toodefine and deploy cloud infrastructure by using a custom templating language called HashiCorp configuration language (HCL).</span></span> <span data-ttu-id="74f03-107">이 사용자 지정 언어는 [쉽게 toowrite 및 쉽게 toounderstand](terraform-create-complete-vm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-107">This custom language is [easy toowrite and easy toounderstand](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="74f03-108">또한 hello를 사용 하 여 `terraform plan` 명령, 커밋하기 전에 hello 변경 tooyour 인프라를 시각화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-108">Additionally, by using hello `terraform plan` command, you can visualize hello changes tooyour infrastructure before you commit them.</span></span> <span data-ttu-id="74f03-109">이러한 단계 toostart Terraform Azure와 함께 사용 하 여 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-109">Follow these steps toostart using Terraform with Azure.</span></span>

## <a name="install-terraform"></a><span data-ttu-id="74f03-110">Terraform 설치</span><span class="sxs-lookup"><span data-stu-id="74f03-110">Install Terraform</span></span>
<span data-ttu-id="74f03-111">tooinstall Terraform, [다운로드](https://www.terraform.io/downloads.html) hello 패키지 별도 설치 디렉터리에 운영 체제에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-111">tooinstall Terraform, [download](https://www.terraform.io/downloads.html) hello package appropriate for your operating system into a separate install directory.</span></span> <span data-ttu-id="74f03-112">hello 다운로드 전역 경로 정의 해야 하는 단일 실행 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-112">hello download contains a single executable file, for which you should also define a global path.</span></span> <span data-ttu-id="74f03-113">에 대 한 tooset Linux 및 Mac에서 경로 hello 하는 방법에 대 한 지침 너무[이 웹 페이지](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux)합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-113">For instructions on how tooset hello path on Linux and Mac, go too[this webpage](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span></span> <span data-ttu-id="74f03-114">에 대 한 tooset windows에서 경로 hello 하는 방법에 대 한 지침 너무[이 웹 페이지](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows)합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-114">For instructions on how tooset hello path on Windows, go too[this webpage](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span></span> <span data-ttu-id="74f03-115">tooverify hello를 실행 하 여 설치 `terraform` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-115">tooverify your installation, run hello `terraform` command.</span></span> <span data-ttu-id="74f03-116">출력으로 사용할 수 있는 Terraform 옵션 목록이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-116">You should see a list of available Terraform options as output.</span></span>

<span data-ttu-id="74f03-117">다음으로, tooallow Terraform 액세스 tooyour Azure 구독 tooperform 인프라 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-117">Next, you need tooallow Terraform access tooyour Azure subscription tooperform infrastructure provisioning.</span></span>

## <a name="set-up-terraform-access-tooazure"></a><span data-ttu-id="74f03-118">Terraform 액세스 tooAzure 설정</span><span class="sxs-lookup"><span data-stu-id="74f03-118">Set up Terraform access tooAzure</span></span>
<span data-ttu-id="74f03-119">Azure Active Directory (Azure AD)에 두 개의 엔터티가 toocreate 필요를 Azure로 Terraform tooprovision 리소스 tooenable: Azure AD 응용 프로그램 및 Azure AD 서비스 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-119">tooenable Terraform tooprovision resources into Azure, you need toocreate two entities in Azure Active Directory (Azure AD): an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="74f03-120">그런 다음 Terraform 스크립트에서 이러한 엔터티의 식별자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-120">Then, you use these entities' identifiers in your Terraform scripts.</span></span> <span data-ttu-id="74f03-121">서비스 주체는 글로벌 Azure AD 응용 프로그램의 로컬 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-121">A service principal is a local instance of a global Azure AD application.</span></span> <span data-ttu-id="74f03-122">서비스 사용자는 로컬 세부적인 액세스 제어 tooglobal 리소스 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-122">A service principal allows granular local access control tooglobal resources.</span></span>

<span data-ttu-id="74f03-123">Azure AD 응용 프로그램 및 Azure AD 서비스 사용자는 여러 가지 방법으로 toocreate가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-123">There are several ways toocreate an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="74f03-124">hello 빠르고 쉬운 방식으로 임 toouse Azure CLI 2.0는 [다운로드 하 여 Windows, Linux 또는 Mac에 설치](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-124">hello easiest and fastest way today is toouse Azure CLI 2.0, which [you can download and install on Windows, Linux, or a Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="74f03-125">PowerShell 또는 Azure CLI 1.0 toocreate hello 필요한 보안 인프라를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-125">You also can use PowerShell or Azure CLI 1.0 toocreate hello necessary security infrastructure.</span></span> <span data-ttu-id="74f03-126">표시 하는 hello 나오는 지침에 따라 모든 이러한 접근 방식을 사용 하 여 Azure에 대 한 Terraform tooconfigure 합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-126">hello instructions that follow show you how tooconfigure Terraform for Azure by using all of these approaches.</span></span>

### <a name="use-azure-cli-20-for-windows-linux-or-mac-users"></a><span data-ttu-id="74f03-127">Azure CLI 2.0 사용(Windows, Linux 또는 Mac 사용자의 경우)</span><span class="sxs-lookup"><span data-stu-id="74f03-127">Use Azure CLI 2.0 (for Windows, Linux, or Mac users)</span></span> 
<span data-ttu-id="74f03-128">다운로드 하 고 hello를 설치한 후 [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), hello 다음 명령을 실행 하 여 Azure 구독을 tooadminister에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-128">After you download and install hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), sign in tooadminister your Azure subscription by issuing hello following command:</span></span>

```
az login
```

>[!NOTE]
><span data-ttu-id="74f03-129">Toofirst 필요한 hello 중국, Azure 독일 또는 Azure Government 클라우드를 사용 하는 경우 해당 클라우드를 사용 하 여 hello Azure CLI toowork를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-129">If you use hello China, Azure Germany, or Azure Government clouds, you need toofirst configure hello Azure CLI toowork with that cloud.</span></span> <span data-ttu-id="74f03-130">Hello 다음을 실행 하 여이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-130">You can do this by running hello following:</span></span>

```
az cloud set --name AzureChinaCloud|AzureGermanCloud|AzureUSGovernment
```

<span data-ttu-id="74f03-131">여러 Azure 구독이 있는 경우 해당 세부 정보에 반환한 hello `az login` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-131">If you have multiple Azure subscriptions, their details are returned by hello `az login` command.</span></span> <span data-ttu-id="74f03-132">집합 hello `SUBSCRIPTION_ID` hello의 환경 변수 toohold hello 값이 반환 `id` hello 구독에서 필드 toouse 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-132">Set hello `SUBSCRIPTION_ID` environment variable toohold hello value of hello returned `id` field from hello subscription you want toouse.</span></span> 

<span data-ttu-id="74f03-133">이 세션에 대 한 toouse 되도록 hello 구독을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-133">Set hello subscription that you want toouse for this session.</span></span>

```
az account set --subscription="${SUBSCRIPTION_ID}"
```

<span data-ttu-id="74f03-134">Hello 계정 tooget hello 구독 ID를 쿼리 하 한 ID 값을 테 넌 트 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-134">Query hello account tooget hello subscription ID and tenant ID values.</span></span>

```
az account show --query "{subscriptionId:id, tenantId:tenantId}"
```

<span data-ttu-id="74f03-135">다음으로 Terraform에 대한 별도의 자격 증명을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-135">Next, create separate credentials for Terraform.</span></span>

```
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/${SUBSCRIPTION_ID}"
```

<span data-ttu-id="74f03-136">appId, 암호, sp_name, 및 테넌트가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-136">Your appId, password, sp_name, and tenant are returned.</span></span> <span data-ttu-id="74f03-137">Hello appId 및 암호를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-137">Make a note of hello appId and password.</span></span>

<span data-ttu-id="74f03-138">tooconfirm (서비스 사용자) 자격 증명 새 셸을 열고 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-138">tooconfirm your credentials (service principal), open a new shell and run hello following commands.</span></span> <span data-ttu-id="74f03-139">대체 hello sp_name, 암호 및 테 넌 트에 대 한 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-139">Substitute hello returned values for sp_name, password, and tenant:</span></span>

```
az login --service-principal -u SP_NAME -p PASSWORD --tenant TENANT
az vm list-sizes --location westus
```

### <a name="use-powershell-for-windows-users"></a><span data-ttu-id="74f03-140">PowerShell 사용(Windows 사용자의 경우)</span><span class="sxs-lookup"><span data-stu-id="74f03-140">Use PowerShell (for Windows users)</span></span> 
<span data-ttu-id="74f03-141">toouse Windows toowrite 컴퓨터 및 사용자 Terraform 실행 스크립트 및 구성 작업에 대 한 PowerShell toouse hello 오른쪽 PowerShell 도구와 함께 컴퓨터를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-141">toouse a Windows machine toowrite and execute your Terraform scripts and toouse PowerShell for configuration tasks, configure your machine with hello right PowerShell tools.</span></span> 

1. <span data-ttu-id="74f03-142">hello 단계에 따라 PowerShell 도구 설치 [설치 Azure PowerShell을 구성 하 고](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps)합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-142">Install PowerShell tools by following hello steps in [Install and configure Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> 

2. <span data-ttu-id="74f03-143">다운로드 및 실행 hello [azure setup.ps1 스크립트](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) hello PowerShell 콘솔에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-143">Download and execute hello [azure-setup.ps1 script](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) from hello PowerShell console.</span></span>

3. <span data-ttu-id="74f03-144">toorun hello azure setup.ps1 스크립트를 다운로드 하 여 hello 실행 `./azure-setup.ps1 setup` hello PowerShell 콘솔에서 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-144">toorun hello azure-setup.ps1 script, download it and execute hello `./azure-setup.ps1 setup` command from hello PowerShell console.</span></span> <span data-ttu-id="74f03-145">Tooyour 관리자 권한으로 Azure 구독에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-145">Then sign in tooyour Azure subscription with administrative privileges.</span></span>

4. <span data-ttu-id="74f03-146">메시지가 표시되면 응용 프로그램 이름(임의 문자열, 필수)을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-146">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="74f03-147">필요에 따라 메시지가 표시되면 강력한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-147">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="74f03-148">암호를 입력하지 않으면 .NET 보안 라이브러리를 사용하여 강력한 암호가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-148">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

### <a name="use-azure-cli-10-for-linux-or-mac-users"></a><span data-ttu-id="74f03-149">Azure CLI 1.0 사용(Linux 또는 Mac 사용자의 경우)</span><span class="sxs-lookup"><span data-stu-id="74f03-149">Use Azure CLI 1.0 (for Linux or Mac users)</span></span>
<span data-ttu-id="74f03-150">tooget Terraform 설치 컴퓨터에 적절 한 라이브러리 hello Azure CLI 1.0과 함께 Mac 또는 Linux 컴퓨터에서 시작 하세요.</span><span class="sxs-lookup"><span data-stu-id="74f03-150">tooget started with Terraform on Linux machines or Macs with Azure CLI 1.0, install hello proper libraries on your machine.</span></span>  

1. <span data-ttu-id="74f03-151">hello 단계에 따라 Azure xPlat CLI 도구 설치 [Azure CLI 2.0 설치](https://docs.microsoft.com/cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-151">Install Azure xPlat CLI tools by following hello steps in [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> 

2. <span data-ttu-id="74f03-152">다운로드 하 여 JSON 프로세서 hello 지침에 따라 설치 [jq 다운로드](https://stedolan.github.io/jq/download/)합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-152">Download and install a JSON processor by following hello instructions in [Download jq](https://stedolan.github.io/jq/download/).</span></span>

3. <span data-ttu-id="74f03-153">다운로드 및 실행 hello [azure setup.sh 스크립트](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) hello 콘솔에서 스크립트를 이용한 적입니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-153">Download and execute hello [azure-setup.sh script](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash script from hello console.</span></span>

4. <span data-ttu-id="74f03-154">toorun hello azure setup.sh 스크립트를 다운로드 하 여 hello 실행 `./azure-setup setup` hello 콘솔에서 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-154">toorun hello azure-setup.sh script, download it and execute hello `./azure-setup setup` command from hello console.</span></span> <span data-ttu-id="74f03-155">Tooyour 관리자 권한으로 Azure 구독에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-155">Then sign in tooyour Azure subscription with administrative privileges.</span></span>
 
5. <span data-ttu-id="74f03-156">메시지가 표시되면 응용 프로그램 이름(임의 문자열, 필수)을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-156">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="74f03-157">필요에 따라 메시지가 표시되면 강력한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-157">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="74f03-158">암호를 입력하지 않으면 .NET 보안 라이브러리를 사용하여 강력한 암호가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-158">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

<span data-ttu-id="74f03-159">모든 hello 이전 스크립트는 Azure AD 응용 프로그램 및 서비스를 만들 주입니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-159">All hello previous scripts create an Azure AD application and service principal.</span></span> <span data-ttu-id="74f03-160">hello 서비스 사용자 hello 구독에서 참가자 또는 소유자 수준의 액세스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-160">hello service principal gets a contributor or owner-level access on hello subscription.</span></span> <span data-ttu-id="74f03-161">Hello 높은 수준의 액세스 권한을 부여, 인해 항상 해당 스크립트에 의해 생성 된 hello 보안 정보를 보호 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-161">Because of hello high level of access granted, you should always protect hello security information generated by those scripts.</span></span> <span data-ttu-id="74f03-162">해당 스크립트에서 제공한 다음 4가지 모든 보안 정보(appId, 암호, subscription_id 및 tenant_id)를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-162">Make a note of all four pieces of security information provided by those scripts: appId, password, subscription_id, and tenant_id.</span></span>

## <a name="set-environment-variables"></a><span data-ttu-id="74f03-163">환경 변수 설정</span><span class="sxs-lookup"><span data-stu-id="74f03-163">Set environment variables</span></span>
<span data-ttu-id="74f03-164">Toolet을 만들고 Azure AD 서비스 사용자를 구성한 후 해야 hello 테 넌 트 ID, 구독 ID, 클라이언트 ID 및 클라이언트 비밀 toouse Terraform 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-164">After you create and configure an Azure AD service principal, you need toolet Terraform know hello tenant ID, subscription ID, client ID, and client secret toouse.</span></span> <span data-ttu-id="74f03-165">[Terraform을 사용하여 기본 인프라 만들기](terraform-create-complete-vm.md)에서 설명한 대로 Terraform 스크립트에 해당 값을 포함하면 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-165">You can do it by embedding those values in your Terraform scripts, as described in [Create basic infrastructure by using Terraform](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="74f03-166">또는 다음 환경 변수는 hello (를 실수로 체크 인 또는 사용자의 자격 증명을 공유 되지 않도록):</span><span class="sxs-lookup"><span data-stu-id="74f03-166">Alternately, you can set hello following environment variables (and thus avoid accidentally checking in or sharing your credentials):</span></span>

- <span data-ttu-id="74f03-167">ARM_SUBSCRIPTION_ID</span><span class="sxs-lookup"><span data-stu-id="74f03-167">ARM_SUBSCRIPTION_ID</span></span>
- <span data-ttu-id="74f03-168">ARM_CLIENT_ID</span><span class="sxs-lookup"><span data-stu-id="74f03-168">ARM_CLIENT_ID</span></span>
- <span data-ttu-id="74f03-169">ARM_CLIENT_SECRET</span><span class="sxs-lookup"><span data-stu-id="74f03-169">ARM_CLIENT_SECRET</span></span>
- <span data-ttu-id="74f03-170">ARM_TENANT_ID</span><span class="sxs-lookup"><span data-stu-id="74f03-170">ARM_TENANT_ID</span></span>

<span data-ttu-id="74f03-171">이 샘플 셸 스크립트 tooset 해당 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-171">You can use this sample shell script tooset those variables:</span></span>

```
#!/bin/sh
echo "Setting environment variables for Terraform"
export ARM_SUBSCRIPTION_ID=your_subscription_id
export ARM_CLIENT_ID=your_appId
export ARM_CLIENT_SECRET=your_password
export ARM_TENANT_ID=your_tenant_id
```

<span data-ttu-id="74f03-172">또한 Azure Government 중 또는 중국의 Azure 또는 Azure 독일 Terraform를 사용 하는 경우 필요한 tooset hello 환경 변수가 적절 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-172">Additionally, if you use Terraform with Azure in China or either Azure Government or Azure Germany, you need tooset hello ENVIRONMENT variable appropriately.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74f03-173">다음 단계</span><span class="sxs-lookup"><span data-stu-id="74f03-173">Next steps</span></span>
<span data-ttu-id="74f03-174">이제 Terraform을 설치했고 Azure 자격 증명을 구성했으므로 Azure 구독에 인프라를 배포하기 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-174">You have now installed Terraform and configured Azure credentials so that you can start deploying infrastructure into your Azure subscription.</span></span> <span data-ttu-id="74f03-175">배우는 것이 너무 어떻게[Terraform와 인프라를 만들](terraform-create-complete-vm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="74f03-175">Next, learn how too[create infrastructure with Terraform](terraform-create-complete-vm.md).</span></span>
