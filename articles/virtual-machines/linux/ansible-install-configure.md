---
title: "aaaInstall 및 Azure 가상 컴퓨터를 사용 하기 위해 Ansible 구성 | Microsoft Docs"
description: "자세한 내용은 방법 tooinstall Ansible Ubuntu, CentOS 및 SLES에서 Azure 리소스를 관리 하기 위한 구성"
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
ms.openlocfilehash: b33d1893909b6134a5474617c9af2d6e4f627c05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-ansible-toomanage-virtual-machines-in-azure"></a><span data-ttu-id="af39f-103">설치 하 고 Azure에서 Ansible toomanage 가상 컴퓨터 구성</span><span class="sxs-lookup"><span data-stu-id="af39f-103">Install and configure Ansible toomanage virtual machines in Azure</span></span>
<span data-ttu-id="af39f-104">이 문서 tooinstall Ansible와 필수 Azure Python SDK 모듈의 일부에 대 한 가장 일반적인 Linux 배포판 hello 방법을 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-104">This article details how tooinstall Ansible and required Azure Python SDK modules for some of hello most common Linux distros.</span></span> <span data-ttu-id="af39f-105">에 설치할 수 있습니다 Ansible 다른 배포판 hello 설치 패키지 toofit 조정 하 여 특정 플랫폼에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-105">You can install Ansible on other distros by adjusting hello installed packages toofit your particular platform.</span></span> <span data-ttu-id="af39f-106">toocreate Azure 안전한 방식으로 리소스를 배울 있습니다 어떻게 toocreate Ansible toouse에 대 한 자격 증명을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-106">toocreate Azure resources in a secure manner, you also learn how toocreate and define credentials for Ansible toouse.</span></span> 

<span data-ttu-id="af39f-107">자세한 설치 옵션 및 다른 플랫폼에 대 한 단계에 대 한 참조 hello [Ansible 설치 가이드](https://docs.ansible.com/ansible/intro_installation.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-107">For more installation options and steps for additional platforms, see hello [Ansible install guide](https://docs.ansible.com/ansible/intro_installation.html).</span></span>


## <a name="install-ansible"></a><span data-ttu-id="af39f-108">Ansible 설치</span><span class="sxs-lookup"><span data-stu-id="af39f-108">Install Ansible</span></span>
<span data-ttu-id="af39f-109">먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-109">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="af39f-110">hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroupAnsible* hello에 *eastus* 위치:</span><span class="sxs-lookup"><span data-stu-id="af39f-110">hello following example creates a resource group named *myResourceGroupAnsible* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroupAnsible --location eastus
```

<span data-ttu-id="af39f-111">이제 VM을 만들고 Ansible hello 배포판을 다음 중 하나에 대 한 설치:</span><span class="sxs-lookup"><span data-stu-id="af39f-111">Now create a VM and install Ansible for one of hello following distros:</span></span>

- [<span data-ttu-id="af39f-112">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="af39f-112">Ubuntu 16.04 LTS</span></span>](#ubuntu1604-lts)
- [<span data-ttu-id="af39f-113">CentOS 7.3</span><span class="sxs-lookup"><span data-stu-id="af39f-113">CentOS 7.3</span></span>](#centos-73)
- [<span data-ttu-id="af39f-114">SLES 12.2 SP2</span><span class="sxs-lookup"><span data-stu-id="af39f-114">SLES 12.2 SP2</span></span>](#sles-122-sp2)

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="af39f-115">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="af39f-115">Ubuntu 16.04 LTS</span></span>
<span data-ttu-id="af39f-116">[az vm create](/cli/azure/vm#create)로 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-116">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="af39f-117">hello 다음 예제에서는 V *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="af39f-117">hello following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="af39f-118">SSH tooyour VM를 사용 하 여 hello `publicIpAddress` hello에 명시 된 hello VM에서에서 출력 만들기 작업:</span><span class="sxs-lookup"><span data-stu-id="af39f-118">SSH tooyour VM using hello `publicIpAddress` noted in hello output from hello VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="af39f-119">VM에 Azure Python SDK 모듈과 Ansible hello에 대 한 hello 필요한 패키지를 다음과 같이 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-119">On your VM, install hello required packages for hello Azure Python SDK modules and Ansible as follows:</span></span>

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

<span data-ttu-id="af39f-120">이제 너무 이동[만들 Azure 자격 증명](#create-azure-credentials)합니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-120">Now move on too[Create Azure credentials](#create-azure-credentials).</span></span>


### <a name="centos-73"></a><span data-ttu-id="af39f-121">CentOS 7.3</span><span class="sxs-lookup"><span data-stu-id="af39f-121">CentOS 7.3</span></span>
<span data-ttu-id="af39f-122">[az vm create](/cli/azure/vm#create)로 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-122">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="af39f-123">hello 다음 예제에서는 V *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="af39f-123">hello following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="af39f-124">SSH tooyour VM를 사용 하 여 hello `publicIpAddress` hello에 명시 된 hello VM에서에서 출력 만들기 작업:</span><span class="sxs-lookup"><span data-stu-id="af39f-124">SSH tooyour VM using hello `publicIpAddress` noted in hello output from hello VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="af39f-125">VM에 Azure Python SDK 모듈과 Ansible hello에 대 한 hello 필요한 패키지를 다음과 같이 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-125">On your VM, install hello required packages for hello Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo yum check-update; sudo yum install -y gcc libffi-devel python-devel openssl-devel epel-release
sudo yum install -y python-pip python-wheel

## Install Azure SDKs via pip
sudo pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via yum
sudo yum install -y ansible
```

<span data-ttu-id="af39f-126">이제 너무 이동[만들 Azure 자격 증명](#create-azure-credentials)합니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-126">Now move on too[Create Azure credentials](#create-azure-credentials).</span></span>


### <a name="sles-122-sp2"></a><span data-ttu-id="af39f-127">SLES 12.2 SP2</span><span class="sxs-lookup"><span data-stu-id="af39f-127">SLES 12.2 SP2</span></span>
<span data-ttu-id="af39f-128">[az vm create](/cli/azure/vm#create)로 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-128">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="af39f-129">hello 다음 예제에서는 V *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="af39f-129">hello following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image SLES \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="af39f-130">SSH tooyour VM를 사용 하 여 hello `publicIpAddress` hello에 명시 된 hello VM에서에서 출력 만들기 작업:</span><span class="sxs-lookup"><span data-stu-id="af39f-130">SSH tooyour VM using hello `publicIpAddress` noted in hello output from hello VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="af39f-131">VM에 Azure Python SDK 모듈과 Ansible hello에 대 한 hello 필요한 패키지를 다음과 같이 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-131">On your VM, install hello required packages for hello Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo zypper refresh && sudo zypper --non-interactive install gcc libffi-devel-gcc5 python-devel \
    libopenssl-devel python-pip python-setuptools python-azure-sdk

## Install Ansible via zypper
sudo zypper addrepo http://download.opensuse.org/repositories/systemsmanagement/SLE_12_SP2/systemsmanagement.repo
sudo zypper refresh && sudo zypper install ansible
```

<span data-ttu-id="af39f-132">이제 너무 이동[만들 Azure 자격 증명](#create-azure-credentials)합니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-132">Now move on too[Create Azure credentials](#create-azure-credentials).</span></span>


## <a name="create-azure-credentials"></a><span data-ttu-id="af39f-133">Azure 자격 증명 만들기</span><span class="sxs-lookup"><span data-stu-id="af39f-133">Create Azure credentials</span></span>
<span data-ttu-id="af39f-134">Ansible은 사용자 이름 및 암호 또는 서비스 주체를 사용하여 Azure와 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-134">Ansible communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="af39f-135">Azure 서비스 주체는 앱, 서비스 및 Ansible과 같은 자동화 도구를 사용할 수 있는 보안 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Ansible.</span></span> <span data-ttu-id="af39f-136">제어 하 고이 정보를 toowhat 작업 hello 서비스 사용자는 Azure에서 수행할 수 있는 대로 hello 사용 권한을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-136">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span> <span data-ttu-id="af39f-137">제공 하는 것 사용자 이름 및 암호를 통해 tooimprove 보안,이 예제에서는 기본 서비스 보안 주체</span><span class="sxs-lookup"><span data-stu-id="af39f-137">tooimprove security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="af39f-138">서비스와 사용자 만들기 [az ad sp 만들기에 대 한-rbac](/cli/azure/ad/sp#create-for-rbac) Ansible 해야 하는 출력 hello 자격 증명:</span><span class="sxs-lookup"><span data-stu-id="af39f-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output hello credentials that Ansible needs:</span></span>

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

<span data-ttu-id="af39f-139">Hello 명령 앞에서 hello 출력의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-139">An example of hello output from hello preceding commands is as follows:</span></span>

```json
[
  "eec5624a-90f8-4386-8a87-02730b5410d5",
  "531dcffa-3aff-4488-99bb-4816c395ea3f",
  "72f988bf-86f1-41af-91ab-2d7cd011db47"
]
```

<span data-ttu-id="af39f-140">tooauthenticate tooAzure 하면 Azure 구독 ID와 tooobtain [az 계정 표시](/cli/azure/account#show):</span><span class="sxs-lookup"><span data-stu-id="af39f-140">tooauthenticate tooAzure, you also need tooobtain your Azure subscription ID with [az account show](/cli/azure/account#show):</span></span>

```azurecli
az account show --query [id] --output tsv
```

<span data-ttu-id="af39f-141">Hello 다음 단계에서이 두 명령은에서 hello 출력을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-141">You use hello output from these two commands in hello next step.</span></span>


## <a name="create-ansible-credentials-file"></a><span data-ttu-id="af39f-142">Ansible 자격 증명 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="af39f-142">Create Ansible credentials file</span></span>
<span data-ttu-id="af39f-143">tooprovide tooAnsible 자격 증명을 환경 변수를 정의 하거나 로컬 자격 증명 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-143">tooprovide credentials tooAnsible, you define environment variables or create a local credentials file.</span></span> <span data-ttu-id="af39f-144">방법에 대 한 자세한 내용은 toodefine Ansible 자격 증명 참조 [자격 증명을 제공 하 tooAzure 모듈](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules)합니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-144">For more information about how toodefine Ansible credentials, see [Providing Credentials tooAzure Modules](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules).</span></span> 

<span data-ttu-id="af39f-145">개발 환경의 경우 호스트 VM에서 다음과 같이 Ansible에 대한 *자격 증명* 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-145">For a development environment, create a *credentials* file for Ansible on your host VM as follows:</span></span>

```bash
mkdir ~/.azure
vi ~/.azure/credentials
```

<span data-ttu-id="af39f-146">hello *자격 증명* 파일 자체 hello 구독 ID를 결합 하 여 서비스 사용자를 만드는 hello 출력을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-146">hello *credentials* file itself combines hello subscription ID with hello output of creating a service principal.</span></span> <span data-ttu-id="af39f-147">이전 hello에서 출력 [az ad sp 만들기에 대 한-rbac](/cli/azure/ad/sp#create-for-rbac) 동일 hello 명령입니다 필요에 따라 주문 *client_id*, *비밀*, 및 *테 넌 트* .</span><span class="sxs-lookup"><span data-stu-id="af39f-147">Output from hello previous [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) command is hello same order as needed for *client_id*, *secret*, and *tenant*.</span></span> <span data-ttu-id="af39f-148">다음 예에서는 hello *자격 증명* 파일 hello 이전 출력 일치 하는 이러한 값을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-148">hello following example *credentials* file shows these values matching hello previous output.</span></span> <span data-ttu-id="af39f-149">다음과 같이 사용자 고유의 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-149">Enter your own values as follows:</span></span>

```bash
[default]
subscription_id=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
client_id=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
secret=b8326643-f7e9-48fb-b0d5-952b68ab3def
tenant=72f988bf-86f1-41af-91ab-2d7cd011db47
```


## <a name="use-ansible-environment-variables"></a><span data-ttu-id="af39f-150">Ansible 환경 변수 사용</span><span class="sxs-lookup"><span data-stu-id="af39f-150">Use Ansible environment variables</span></span>
<span data-ttu-id="af39f-151">Toouse Ansible 타워 또는 Jenkins 등의 도구를 사용 하도록 하려는 경우 환경 변수를 다음과 같이 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-151">If you are going toouse tools such as Ansible Tower or Jenkins, you can define environment variables as follows.</span></span> <span data-ttu-id="af39f-152">이러한 변수 서비스 보안 주체를 만드는 hello 출력 hello 구독 ID를 결합 합니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-152">These variables combine hello subscription ID with hello output from creating a service principal.</span></span> <span data-ttu-id="af39f-153">이전 hello에서 출력 [az ad sp 만들기에 대 한-rbac](/cli/azure/ad/sp#create-for-rbac) 명령 동일 hello입니다 필요에 따라 주문 *AZURE_CLIENT_ID*, *AZURE_SECRET*, 및 *AZURE_ 테 넌 트*합니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-153">Output from hello previous [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) command is hello same order as needed for *AZURE_CLIENT_ID*, *AZURE_SECRET*, and *AZURE_TENANT*.</span></span> 

```bash
export AZURE_SUBSCRIPTION_ID=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
export AZURE_CLIENT_ID=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
export AZURE_SECRET=8326643-f7e9-48fb-b0d5-952b68ab3def
export AZURE_TENANT=72f988bf-86f1-41af-91ab-2d7cd011db47
```

## <a name="next-steps"></a><span data-ttu-id="af39f-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="af39f-154">Next steps</span></span>
<span data-ttu-id="af39f-155">Ansible 있으며 Azure Python SDK 모듈 설치 및 자격 증명 Ansible toouse에 대해 정의 된 hello 필요한 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-155">You now have Ansible and hello required Azure Python SDK modules installed, and credentials defined for Ansible toouse.</span></span> <span data-ttu-id="af39f-156">너무 방법에 대해 알아봅니다[VM Ansible을 만들어](ansible-create-vm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-156">Learn how too[create a VM with Ansible](ansible-create-vm.md).</span></span> <span data-ttu-id="af39f-157">배울 수 있습니다 어떻게 너무[전체 Azure VM을 만들고 Ansible 사용 하 여 리소스를 지 원하는](ansible-create-complete-vm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="af39f-157">You can also learn how too[create a complete Azure VM and supporting resources with Ansible](ansible-create-complete-vm.md).</span></span>
