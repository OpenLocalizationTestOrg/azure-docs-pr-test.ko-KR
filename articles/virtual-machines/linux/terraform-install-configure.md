---
title: "Azure에서 VM 및 기타 인프라를 프로비전하기 위해 Terraform 설치 및 구성 | Microsoft Docs"
description: "Terraform을 설치하고 구성하여 Azure 리소스를 만드는 방법을 알아봅니다."
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
ms.openlocfilehash: da567097be38ac649c6bf1de1508de24d21cb877
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="install-and-configure-terraform-to-provision-vms-and-other-infrastructure-into-azure"></a><span data-ttu-id="ddf0a-103">Azure에 VM 및 기타 인프라를 프로비전하기 위해 Terraform 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="ddf0a-103">Install and configure Terraform to provision VMs and other infrastructure into Azure</span></span> 
<span data-ttu-id="ddf0a-104">이 문서에서는 가상 컴퓨터와 같은 리소스를 Azure에 프로비전하기 위해 Terraform를 설치 및 구성하는 필수 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-104">This article describes the necessary steps to install and configure Terraform to provision resources such as virtual machines into Azure.</span></span> <span data-ttu-id="ddf0a-105">Azure 자격 증명을 만들고 사용하여 Terraform에서 클라우드 리소스를 안전하게 프로비전하도록 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-105">You will learn how to create and use Azure credentials to enable Terraform to provision cloud resources in a secure manner.</span></span>

<span data-ttu-id="ddf0a-106">HashiCorp Terraform은 HCL(HashiCorp configuration language)이라는 사용자 지정 템플릿 언어를 사용하여 클라우드 인프라를 정의 및 배포하는 쉬운 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-106">HashiCorp Terraform provides an easy way to define and deploy cloud infrastructure by using a custom templating language called HashiCorp configuration language (HCL).</span></span> <span data-ttu-id="ddf0a-107">이 사용자 지정 언어는 [작성하고 이해하기 쉽습니다](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="ddf0a-107">This custom language is [easy to write and easy to understand](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="ddf0a-108">또한 `terraform plan` 명령을 사용하여 커밋하기 전에 인프라에 대한 변경 내용을 시각화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-108">Additionally, by using the `terraform plan` command, you can visualize the changes to your infrastructure before you commit them.</span></span> <span data-ttu-id="ddf0a-109">다음 단계를 수행하여 Azure에서 Terraform을 사용하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-109">Follow these steps to start using Terraform with Azure.</span></span>

## <a name="install-terraform"></a><span data-ttu-id="ddf0a-110">Terraform 설치</span><span class="sxs-lookup"><span data-stu-id="ddf0a-110">Install Terraform</span></span>
<span data-ttu-id="ddf0a-111">Terraform를 설치하려면 운영 체제에 적합한 패키지를 별도의 설치 디렉터리에 [다운로드](https://www.terraform.io/downloads.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-111">To install Terraform, [download](https://www.terraform.io/downloads.html) the package appropriate for your operating system into a separate install directory.</span></span> <span data-ttu-id="ddf0a-112">다운로드에는 전역 경로를 정의해야 하는 단일 실행 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-112">The download contains a single executable file, for which you should also define a global path.</span></span> <span data-ttu-id="ddf0a-113">Linux 및 Mac에서 경로를 설정하는 방법에 대한 지침은 [이 웹 페이지](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-113">For instructions on how to set the path on Linux and Mac, go to [this webpage](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span></span> <span data-ttu-id="ddf0a-114">Windows에서 경로를 설정하는 방법에 대한 지침은 [이 웹 페이지](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-114">For instructions on how to set the path on Windows, go to [this webpage](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span></span> <span data-ttu-id="ddf0a-115">설치를 확인하려면 `terraform` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-115">To verify your installation, run the `terraform` command.</span></span> <span data-ttu-id="ddf0a-116">출력으로 사용할 수 있는 Terraform 옵션 목록이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-116">You should see a list of available Terraform options as output.</span></span>

<span data-ttu-id="ddf0a-117">다음으로, 인프라 프로비전을 수행하기 위해 Azure 구독에 대한 Terraform 액세스를 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-117">Next, you need to allow Terraform access to your Azure subscription to perform infrastructure provisioning.</span></span>

## <a name="set-up-terraform-access-to-azure"></a><span data-ttu-id="ddf0a-118">Azure에 대한 Terraform 액세스 설정</span><span class="sxs-lookup"><span data-stu-id="ddf0a-118">Set up Terraform access to Azure</span></span>
<span data-ttu-id="ddf0a-119">Terraform에서 Azure에 리소스를 프로비전하도록 하려면 Azure AD(Azure Active Directory)에서 Azure AD 응용 프로그램 및 Azure AD 서비스 주체라는 두 개의 엔터티를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-119">To enable Terraform to provision resources into Azure, you need to create two entities in Azure Active Directory (Azure AD): an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="ddf0a-120">그런 다음 Terraform 스크립트에서 이러한 엔터티의 식별자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-120">Then, you use these entities' identifiers in your Terraform scripts.</span></span> <span data-ttu-id="ddf0a-121">서비스 주체는 글로벌 Azure AD 응용 프로그램의 로컬 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-121">A service principal is a local instance of a global Azure AD application.</span></span> <span data-ttu-id="ddf0a-122">서비스 주체를 사용하면 전역 리소스에 대한 세분화된 로컬 액세스 제어가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-122">A service principal allows granular local access control to global resources.</span></span>

<span data-ttu-id="ddf0a-123">여러 가지 방법으로 Azure AD 응용 프로그램 및 Azure AD 서비스 주체를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-123">There are several ways to create an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="ddf0a-124">현재 가장 쉽고 빠른 방법은 Azure CLI 2.0을 사용하는 것이며 [Windows, Linux 또는 Mac에 다운로드하여 설치](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-124">The easiest and fastest way today is to use Azure CLI 2.0, which [you can download and install on Windows, Linux, or a Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="ddf0a-125">또한 PowerShell 또는 Azure CLI 1.0을 사용하여 필요한 보안 인프라를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-125">You also can use PowerShell or Azure CLI 1.0 to create the necessary security infrastructure.</span></span> <span data-ttu-id="ddf0a-126">아래 지침은 해당하는 모든 방법을 사용하여 Azure에 대해 Terraform을 구성하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-126">The instructions that follow show you how to configure Terraform for Azure by using all of these approaches.</span></span>

### <a name="use-azure-cli-20-for-windows-linux-or-mac-users"></a><span data-ttu-id="ddf0a-127">Azure CLI 2.0 사용(Windows, Linux 또는 Mac 사용자의 경우)</span><span class="sxs-lookup"><span data-stu-id="ddf0a-127">Use Azure CLI 2.0 (for Windows, Linux, or Mac users)</span></span> 
<span data-ttu-id="ddf0a-128">[Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)을 다운로드 및 설치한 후에 다음 명령을 실행하여 Azure 구독을 관리하기 위해 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-128">After you download and install the [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), sign in to administer your Azure subscription by issuing the following command:</span></span>

```
az login
```

>[!NOTE]
><span data-ttu-id="ddf0a-129">중국, Azure 독일 또는 Azure Government Clouds를 사용하는 경우 해당 클라우드에서 작동하도록 먼저 Azure CLI를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-129">If you use the China, Azure Germany, or Azure Government clouds, you need to first configure the Azure CLI to work with that cloud.</span></span> <span data-ttu-id="ddf0a-130">다음을 실행하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-130">You can do this by running the following:</span></span>

```
az cloud set --name AzureChinaCloud|AzureGermanCloud|AzureUSGovernment
```

<span data-ttu-id="ddf0a-131">여러 Azure 구독이 있는 경우 `az login` 명령을 사용하면 세부 정보가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-131">If you have multiple Azure subscriptions, their details are returned by the `az login` command.</span></span> <span data-ttu-id="ddf0a-132">사용하려는 구독에서 반환된 `id` 필드 값을 보유하도록 `SUBSCRIPTION_ID` 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-132">Set the `SUBSCRIPTION_ID` environment variable to hold the value of the returned `id` field from the subscription you want to use.</span></span> 

<span data-ttu-id="ddf0a-133">이 세션에 사용할 구독을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-133">Set the subscription that you want to use for this session.</span></span>

```
az account set --subscription="${SUBSCRIPTION_ID}"
```

<span data-ttu-id="ddf0a-134">계정을 쿼리하여 구독 ID 및 테넌트 ID 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-134">Query the account to get the subscription ID and tenant ID values.</span></span>

```
az account show --query "{subscriptionId:id, tenantId:tenantId}"
```

<span data-ttu-id="ddf0a-135">다음으로 Terraform에 대한 별도의 자격 증명을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-135">Next, create separate credentials for Terraform.</span></span>

```
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/${SUBSCRIPTION_ID}"
```

<span data-ttu-id="ddf0a-136">appId, 암호, sp_name, 및 테넌트가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-136">Your appId, password, sp_name, and tenant are returned.</span></span> <span data-ttu-id="ddf0a-137">appId 및 암호를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-137">Make a note of the appId and password.</span></span>

<span data-ttu-id="ddf0a-138">자격 증명(서비스 주체)을 확인하려면 새 셸을 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-138">To confirm your credentials (service principal), open a new shell and run the following commands.</span></span> <span data-ttu-id="ddf0a-139">sp_name, 암호 및 테넌트에 반환된 값으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-139">Substitute the returned values for sp_name, password, and tenant:</span></span>

```
az login --service-principal -u SP_NAME -p PASSWORD --tenant TENANT
az vm list-sizes --location westus
```

### <a name="use-powershell-for-windows-users"></a><span data-ttu-id="ddf0a-140">PowerShell 사용(Windows 사용자의 경우)</span><span class="sxs-lookup"><span data-stu-id="ddf0a-140">Use PowerShell (for Windows users)</span></span> 
<span data-ttu-id="ddf0a-141">Windows 컴퓨터를 사용하여 Terraform 스크립트를 작성 및 실행하고 구성 작업에 PowerShell을 사용하려면 적절한 PowerShell 도구로 컴퓨터를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-141">To use a Windows machine to write and execute your Terraform scripts and to use PowerShell for configuration tasks, configure your machine with the right PowerShell tools.</span></span> 

1. <span data-ttu-id="ddf0a-142">[Azure PowerShell 설치 및 구성](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps)의 단계에 따라 PowerShell 도구를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-142">Install PowerShell tools by following the steps in [Install and configure Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> 

2. <span data-ttu-id="ddf0a-143">PowerShell 콘솔에서 [azure-setup.ps1 스크립트](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1)를 다운로드하여 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-143">Download and execute the [azure-setup.ps1 script](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) from the PowerShell console.</span></span>

3. <span data-ttu-id="ddf0a-144">azure-setup.ps1 스크립트를 실행하려면 다운로드하여 PowerShell 콘솔에서 `./azure-setup.ps1 setup` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-144">To run the azure-setup.ps1 script, download it and execute the `./azure-setup.ps1 setup` command from the PowerShell console.</span></span> <span data-ttu-id="ddf0a-145">관리자 권한으로 Azure 구독에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-145">Then sign in to your Azure subscription with administrative privileges.</span></span>

4. <span data-ttu-id="ddf0a-146">메시지가 표시되면 응용 프로그램 이름(임의 문자열, 필수)을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-146">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="ddf0a-147">필요에 따라 메시지가 표시되면 강력한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-147">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="ddf0a-148">암호를 입력하지 않으면 .NET 보안 라이브러리를 사용하여 강력한 암호가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-148">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

### <a name="use-azure-cli-10-for-linux-or-mac-users"></a><span data-ttu-id="ddf0a-149">Azure CLI 1.0 사용(Linux 또는 Mac 사용자의 경우)</span><span class="sxs-lookup"><span data-stu-id="ddf0a-149">Use Azure CLI 1.0 (for Linux or Mac users)</span></span>
<span data-ttu-id="ddf0a-150">Azure CLI 1.0이 설치된 Linux 컴퓨터 또는 Mac에서 Terraform을 시작하려면 컴퓨터에 적절한 라이브러리를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-150">To get started with Terraform on Linux machines or Macs with Azure CLI 1.0, install the proper libraries on your machine.</span></span>  

1. <span data-ttu-id="ddf0a-151">[Azure CLI 2.0 설치](https://docs.microsoft.com/cli/azure/install-azure-cli)의 단계에 따라 Azure xPlat CLI 도구를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-151">Install Azure xPlat CLI tools by following the steps in [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> 

2. <span data-ttu-id="ddf0a-152">[jq 다운로드](https://stedolan.github.io/jq/download/)의 지침에 따라 JSON 프로세서를 다운로드하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-152">Download and install a JSON processor by following the instructions in [Download jq](https://stedolan.github.io/jq/download/).</span></span>

3. <span data-ttu-id="ddf0a-153">콘솔에서 [azure-setup.sh 스크립트](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) 일괄 처리를 다운로드하여 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-153">Download and execute the [azure-setup.sh script](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash script from the console.</span></span>

4. <span data-ttu-id="ddf0a-154">azure-setup.sh 스크립트를 실행하려면 다운로드하여 콘솔에서 `./azure-setup setup` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-154">To run the azure-setup.sh script, download it and execute the `./azure-setup setup` command from the console.</span></span> <span data-ttu-id="ddf0a-155">관리자 권한으로 Azure 구독에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-155">Then sign in to your Azure subscription with administrative privileges.</span></span>
 
5. <span data-ttu-id="ddf0a-156">메시지가 표시되면 응용 프로그램 이름(임의 문자열, 필수)을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-156">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="ddf0a-157">필요에 따라 메시지가 표시되면 강력한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-157">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="ddf0a-158">암호를 입력하지 않으면 .NET 보안 라이브러리를 사용하여 강력한 암호가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-158">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

<span data-ttu-id="ddf0a-159">모든 이전 스크립트는 Azure AD 응용 프로그램 및 서비스 주체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-159">All the previous scripts create an Azure AD application and service principal.</span></span> <span data-ttu-id="ddf0a-160">서비스 주체는 구독에서 참가자 또는 소유자 수준의 액세스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-160">The service principal gets a contributor or owner-level access on the subscription.</span></span> <span data-ttu-id="ddf0a-161">높은 수준의 액세스 권한이 부여되므로 해당 스크립트에서 생성한 보안 정보를 항상 보호해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-161">Because of the high level of access granted, you should always protect the security information generated by those scripts.</span></span> <span data-ttu-id="ddf0a-162">해당 스크립트에서 제공한 다음 4가지 모든 보안 정보(appId, 암호, subscription_id 및 tenant_id)를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-162">Make a note of all four pieces of security information provided by those scripts: appId, password, subscription_id, and tenant_id.</span></span>

## <a name="set-environment-variables"></a><span data-ttu-id="ddf0a-163">환경 변수 설정</span><span class="sxs-lookup"><span data-stu-id="ddf0a-163">Set environment variables</span></span>
<span data-ttu-id="ddf0a-164">Azure AD 서비스 주체를 만들고 구성한 후에 Terraform이 사용할 테넌트 ID, 구독 ID, 클라이언트 ID 및 클라이언트 암호를 알 수 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-164">After you create and configure an Azure AD service principal, you need to let Terraform know the tenant ID, subscription ID, client ID, and client secret to use.</span></span> <span data-ttu-id="ddf0a-165">[Terraform을 사용하여 기본 인프라 만들기](terraform-create-complete-vm.md)에서 설명한 대로 Terraform 스크립트에 해당 값을 포함하면 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-165">You can do it by embedding those values in your Terraform scripts, as described in [Create basic infrastructure by using Terraform](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="ddf0a-166">또는 다음 환경 변수를 설정할 수 있습니다(따라서 실수로 체크 인하거나 자격 증명을 공유하지 않도록 방지할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="ddf0a-166">Alternately, you can set the following environment variables (and thus avoid accidentally checking in or sharing your credentials):</span></span>

- <span data-ttu-id="ddf0a-167">ARM_SUBSCRIPTION_ID</span><span class="sxs-lookup"><span data-stu-id="ddf0a-167">ARM_SUBSCRIPTION_ID</span></span>
- <span data-ttu-id="ddf0a-168">ARM_CLIENT_ID</span><span class="sxs-lookup"><span data-stu-id="ddf0a-168">ARM_CLIENT_ID</span></span>
- <span data-ttu-id="ddf0a-169">ARM_CLIENT_SECRET</span><span class="sxs-lookup"><span data-stu-id="ddf0a-169">ARM_CLIENT_SECRET</span></span>
- <span data-ttu-id="ddf0a-170">ARM_TENANT_ID</span><span class="sxs-lookup"><span data-stu-id="ddf0a-170">ARM_TENANT_ID</span></span>

<span data-ttu-id="ddf0a-171">이 샘플 셸 스크립트를 사용하여 해당 변수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-171">You can use this sample shell script to set those variables:</span></span>

```
#!/bin/sh
echo "Setting environment variables for Terraform"
export ARM_SUBSCRIPTION_ID=your_subscription_id
export ARM_CLIENT_ID=your_appId
export ARM_CLIENT_SECRET=your_password
export ARM_TENANT_ID=your_tenant_id
```

<span data-ttu-id="ddf0a-172">또한 중국, Azure Government 또는 Azure Germany에서 Azure로 Terraform을 사용하는 경우 ENVIRONMENT 변수를 적절하게 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-172">Additionally, if you use Terraform with Azure in China or either Azure Government or Azure Germany, you need to set the ENVIRONMENT variable appropriately.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ddf0a-173">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ddf0a-173">Next steps</span></span>
<span data-ttu-id="ddf0a-174">이제 Terraform을 설치했고 Azure 자격 증명을 구성했으므로 Azure 구독에 인프라를 배포하기 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-174">You have now installed Terraform and configured Azure credentials so that you can start deploying infrastructure into your Azure subscription.</span></span> <span data-ttu-id="ddf0a-175">다음으로 [Terraform으로 인프라를 만드는 방법](terraform-create-complete-vm.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ddf0a-175">Next, learn how to [create infrastructure with Terraform](terraform-create-complete-vm.md).</span></span>
