---
title: "Azure Virtual Machines에서 사용할 Ansible 설치 및 구성 | Microsoft Docs"
description: "Ubuntu, CentOS 및 SLES에서 Azure 리소스를 관리하기 위해 Ansible을 설치 및 구성하는 방법을 알아봅니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/25/2017
ms.author: iainfou
ms.openlocfilehash: 52b763274437961dccfc862c8a45fbd57ea9fc4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-configure-ansible-to-manage-virtual-machines-in-azure"></a><span data-ttu-id="ec001-103">Azure에서 가상 컴퓨터를 관리하기 위한 Ansible 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="ec001-103">Install and configure Ansible to manage virtual machines in Azure</span></span>
<span data-ttu-id="ec001-104">이 문서에는 가장 일반적인 Linux 배포판 중 일부에 대해 Ansible 및 필요한 Azure Python SDK 모듈을 설치하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-104">This article details how to install Ansible and required Azure Python SDK modules for some of the most common Linux distros.</span></span> <span data-ttu-id="ec001-105">설치된 패키지를 특정 플랫폼에 맞게 조정하여 다른 배포판에 Ansible을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-105">You can install Ansible on other distros by adjusting the installed packages to fit your particular platform.</span></span> <span data-ttu-id="ec001-106">Azure 리소스를 안전하게 만들기 위해 Ansible에 대한 자격 증명을 만들고 정의하는 방법도 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-106">To create Azure resources in a secure manner, you also learn how to create and define credentials for Ansible to use.</span></span> 

<span data-ttu-id="ec001-107">추가 플랫폼에 대한 설치 옵션 및 단계는 [Ansible 설치 가이드](https://docs.ansible.com/ansible/intro_installation.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec001-107">For more installation options and steps for additional platforms, see the [Ansible install guide](https://docs.ansible.com/ansible/intro_installation.html).</span></span>


## <a name="install-ansible"></a><span data-ttu-id="ec001-108">Ansible 설치</span><span class="sxs-lookup"><span data-stu-id="ec001-108">Install Ansible</span></span>
<span data-ttu-id="ec001-109">먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-109">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="ec001-110">다음 예제에서는 *eastus* 위치에 *myResourceGroupAnsible*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-110">The following example creates a resource group named *myResourceGroupAnsible* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroupAnsible --location eastus
```

<span data-ttu-id="ec001-111">이제 VM을 만들고 다음 배포판 중 하나에 대해 Ansible을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-111">Now create a VM and install Ansible for one of the following distros:</span></span>

- [<span data-ttu-id="ec001-112">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="ec001-112">Ubuntu 16.04 LTS</span></span>](#ubuntu1604-lts)
- [<span data-ttu-id="ec001-113">CentOS 7.3</span><span class="sxs-lookup"><span data-stu-id="ec001-113">CentOS 7.3</span></span>](#centos-73)
- [<span data-ttu-id="ec001-114">SLES 12.2 SP2</span><span class="sxs-lookup"><span data-stu-id="ec001-114">SLES 12.2 SP2</span></span>](#sles-122-sp2)

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="ec001-115">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="ec001-115">Ubuntu 16.04 LTS</span></span>
<span data-ttu-id="ec001-116">[az vm create](/cli/azure/vm#create)로 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-116">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="ec001-117">다음 예제에서는 *myVMAnsible*이라는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-117">The following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="ec001-118">VM 만들기 작업의 출력에 기록된 `publicIpAddress`를 사용하여 VM에 SSH 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-118">SSH to your VM using the `publicIpAddress` noted in the output from the VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="ec001-119">VM에서 Azure Python SDK 모듈 및 Ansible에 대한 필수 패키지를 다음과 같이 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-119">On your VM, install the required packages for the Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo apt-get update && sudo apt-get install -y libssl-dev libffi-dev python-dev python-pip

## Install Azure SDKs via pip
pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via apt
sudo apt-get install -y software-properties-common
sudo apt-add-repository -y ppa:ansible/ansible
sudo apt-get update && sudo apt-get install -y ansible
```

<span data-ttu-id="ec001-120">이제 계속해서 [Azure 자격 증명 만들기](#create-azure-credentials) 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-120">Now move on to [Create Azure credentials](#create-azure-credentials).</span></span>


### <a name="centos-73"></a><span data-ttu-id="ec001-121">CentOS 7.3</span><span class="sxs-lookup"><span data-stu-id="ec001-121">CentOS 7.3</span></span>
<span data-ttu-id="ec001-122">[az vm create](/cli/azure/vm#create)로 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-122">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="ec001-123">다음 예제에서는 *myVMAnsible*이라는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-123">The following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="ec001-124">VM 만들기 작업의 출력에 기록된 `publicIpAddress`를 사용하여 VM에 SSH 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-124">SSH to your VM using the `publicIpAddress` noted in the output from the VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="ec001-125">VM에서 Azure Python SDK 모듈 및 Ansible에 대한 필수 패키지를 다음과 같이 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-125">On your VM, install the required packages for the Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo yum check-update; sudo yum install -y gcc libffi-devel python-devel openssl-devel epel-release
sudo yum install -y python-pip python-wheel

## Install Azure SDKs via pip
sudo pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via yum
sudo yum install -y ansible
```

<span data-ttu-id="ec001-126">이제 계속해서 [Azure 자격 증명 만들기](#create-azure-credentials) 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-126">Now move on to [Create Azure credentials](#create-azure-credentials).</span></span>


### <a name="sles-122-sp2"></a><span data-ttu-id="ec001-127">SLES 12.2 SP2</span><span class="sxs-lookup"><span data-stu-id="ec001-127">SLES 12.2 SP2</span></span>
<span data-ttu-id="ec001-128">[az vm create](/cli/azure/vm#create)로 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-128">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="ec001-129">다음 예제에서는 *myVMAnsible*이라는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-129">The following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image SLES \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="ec001-130">VM 만들기 작업의 출력에 기록된 `publicIpAddress`를 사용하여 VM에 SSH 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-130">SSH to your VM using the `publicIpAddress` noted in the output from the VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="ec001-131">VM에서 Azure Python SDK 모듈 및 Ansible에 대한 필수 패키지를 다음과 같이 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-131">On your VM, install the required packages for the Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo zypper refresh && sudo zypper --non-interactive install gcc libffi-devel-gcc5 python-devel \
    libopenssl-devel python-pip python-setuptools python-azure-sdk

## Install Ansible via zypper
sudo zypper addrepo http://download.opensuse.org/repositories/systemsmanagement/SLE_12_SP2/systemsmanagement.repo
sudo zypper refresh && sudo zypper install ansible
```

<span data-ttu-id="ec001-132">이제 계속해서 [Azure 자격 증명 만들기](#create-azure-credentials) 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-132">Now move on to [Create Azure credentials](#create-azure-credentials).</span></span>


## <a name="create-azure-credentials"></a><span data-ttu-id="ec001-133">Azure 자격 증명 만들기</span><span class="sxs-lookup"><span data-stu-id="ec001-133">Create Azure credentials</span></span>
<span data-ttu-id="ec001-134">Ansible은 사용자 이름 및 암호 또는 서비스 주체를 사용하여 Azure와 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-134">Ansible communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="ec001-135">Azure 서비스 주체는 앱, 서비스 및 Ansible과 같은 자동화 도구를 사용할 수 있는 보안 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Ansible.</span></span> <span data-ttu-id="ec001-136">서비스 주체가 Azure에서 수행할 수 있는 작업에 대한 사용 권한은 사용자가 제어하고 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-136">You control and define the permissions as to what operations the service principal can perform in Azure.</span></span> <span data-ttu-id="ec001-137">사용자 이름 및 암호를 입력하는 것 이상으로 보안을 강화하기 위해 이 예제에서는 기본 서비스 주체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-137">To improve security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="ec001-138">[az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac)를 사용하여 서비스 주체를 만들고 Ansible에서 요구하는 자격 증명을 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output the credentials that Ansible needs:</span></span>

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

<span data-ttu-id="ec001-139">이전 명령에서 출력의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-139">An example of the output from the preceding commands is as follows:</span></span>

```json
[
  "eec5624a-90f8-4386-8a87-02730b5410d5",
  "531dcffa-3aff-4488-99bb-4816c395ea3f",
  "72f988bf-86f1-41af-91ab-2d7cd011db47"
]
```

<span data-ttu-id="ec001-140">Azure를 인증하기 위해 [az account show](/cli/azure/account#show)를 사용하여 Azure 구독 ID를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-140">To authenticate to Azure, you also need to obtain your Azure subscription ID with [az account show](/cli/azure/account#show):</span></span>

```azurecli
az account show --query [id] --output tsv
```

<span data-ttu-id="ec001-141">다음 단계에서 이러한 두 명령의 출력을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-141">You use the output from these two commands in the next step.</span></span>


## <a name="create-ansible-credentials-file"></a><span data-ttu-id="ec001-142">Ansible 자격 증명 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="ec001-142">Create Ansible credentials file</span></span>
<span data-ttu-id="ec001-143">Ansible에 자격 증명을 제공하려면 환경 변수를 정의하거나 로컬 자격 증명 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-143">To provide credentials to Ansible, you define environment variables or create a local credentials file.</span></span> <span data-ttu-id="ec001-144">Ansible 자격 증명을 정의하는 방법에 대한 자세한 내용은 [Azure 모듈에 자격 증명 제공](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec001-144">For more information about how to define Ansible credentials, see [Providing Credentials to Azure Modules](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules).</span></span> 

<span data-ttu-id="ec001-145">개발 환경의 경우 호스트 VM에서 다음과 같이 Ansible에 대한 *자격 증명* 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-145">For a development environment, create a *credentials* file for Ansible on your host VM as follows:</span></span>

```bash
mkdir ~/.azure
vi ~/.azure/credentials
```

<span data-ttu-id="ec001-146">*자격 증명* 파일 자체는 구독 ID와 서비스 주체 만들기의 출력을 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-146">The *credentials* file itself combines the subscription ID with the output of creating a service principal.</span></span> <span data-ttu-id="ec001-147">이전 [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) 명령의 출력은 *client_id*, *secret* 및 *tenant*에 필요한 대로 동일한 순서입니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-147">Output from the previous [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) command is the same order as needed for *client_id*, *secret*, and *tenant*.</span></span> <span data-ttu-id="ec001-148">다음 예제 *자격 증명* 파일은 이전 출력과 일치하는 이러한 값을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-148">The following example *credentials* file shows these values matching the previous output.</span></span> <span data-ttu-id="ec001-149">다음과 같이 사용자 고유의 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-149">Enter your own values as follows:</span></span>

```bash
[default]
subscription_id=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
client_id=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
secret=b8326643-f7e9-48fb-b0d5-952b68ab3def
tenant=72f988bf-86f1-41af-91ab-2d7cd011db47
```


## <a name="use-ansible-environment-variables"></a><span data-ttu-id="ec001-150">Ansible 환경 변수 사용</span><span class="sxs-lookup"><span data-stu-id="ec001-150">Use Ansible environment variables</span></span>
<span data-ttu-id="ec001-151">Ansible Tower 또는 Jenkins와 같은 도구를 사용하려는 경우 다음과 같이 환경 변수를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-151">If you are going to use tools such as Ansible Tower or Jenkins, you can define environment variables as follows.</span></span> <span data-ttu-id="ec001-152">이러한 변수는 구독 ID와 서비스 주체 만들기의 출력을 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-152">These variables combine the subscription ID with the output from creating a service principal.</span></span> <span data-ttu-id="ec001-153">이전 [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) 명령의 출력은 *AZURE_CLIENT_ID*, *AZURE_SECRET* 및 *AZURE_TENANT*에 필요한 대로 동일한 순서입니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-153">Output from the previous [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) command is the same order as needed for *AZURE_CLIENT_ID*, *AZURE_SECRET*, and *AZURE_TENANT*.</span></span> 

```bash
export AZURE_SUBSCRIPTION_ID=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
export AZURE_CLIENT_ID=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
export AZURE_SECRET=8326643-f7e9-48fb-b0d5-952b68ab3def
export AZURE_TENANT=72f988bf-86f1-41af-91ab-2d7cd011db47
```

## <a name="next-steps"></a><span data-ttu-id="ec001-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ec001-154">Next steps</span></span>
<span data-ttu-id="ec001-155">이제 Ansible 및 필요한 Azure Python SDK 모듈을 설치하고 사용할 Ansible 자격 증명을 정의했습니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-155">You now have Ansible and the required Azure Python SDK modules installed, and credentials defined for Ansible to use.</span></span> <span data-ttu-id="ec001-156">[Ansible을 사용하여 VM을 만드는](ansible-create-vm.md) 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-156">Learn how to [create a VM with Ansible](ansible-create-vm.md).</span></span> <span data-ttu-id="ec001-157">[Ansible을 사용하여 전체 Azure VM 및 지원 리소스를 만드는](ansible-create-complete-vm.md) 방법도 배울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec001-157">You can also learn how to [create a complete Azure VM and supporting resources with Ansible](ansible-create-complete-vm.md).</span></span>