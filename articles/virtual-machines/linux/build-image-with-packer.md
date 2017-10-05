---
title: "Packer를 사용하여 Linux Azure VM 이미지를 만드는 방법 | Microsoft Docs"
description: "Azure에서 Packer를 사용하여 Linux 가상 컴퓨터의 이미지를 만드는 방법에 대해 알아보기"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/18/2017
ms.author: iainfou
ms.openlocfilehash: 49a74648bd3953647d581c4e7c548985c5000f17
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-packer-to-create-linux-virtual-machine-images-in-azure"></a><span data-ttu-id="ac2a6-103">Azure에서 Packer를 사용하여 Linux 가상 컴퓨터 이미지를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="ac2a6-103">How to use Packer to create Linux virtual machine images in Azure</span></span>
<span data-ttu-id="ac2a6-104">Azure의 각 VM(가상 컴퓨터)은 Linux 배포판 및 OS 버전을 정의하는 이미지에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-104">Each virtual machine (VM) in Azure is created from an image that defines the Linux distribution and OS version.</span></span> <span data-ttu-id="ac2a6-105">이미지는 사전 설치된 응용 프로그램 및 구성을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-105">Images can include pre-installed applications and configurations.</span></span> <span data-ttu-id="ac2a6-106">Azure Marketplace는 가장 일반적인 배포 및 응용 프로그램 환경에 대한 다양한 자사 및 타사 이미지를 제공하거나 사용자 요구에 맞게 사용자 지정 이미지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-106">The Azure Marketplace provides many first and third-party images for most common distributions and application environments, or you can create your own custom images tailored to your needs.</span></span> <span data-ttu-id="ac2a6-107">이 문서에는 오픈 소스 도구 [Packer](https://www.packer.io/)를 사용하여 Azure에서 사용자 지정 이미지를 정의하고 작성하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-107">This article details how to use the open source tool [Packer](https://www.packer.io/) to define and build custom images in Azure.</span></span>


## <a name="create-azure-resource-group"></a><span data-ttu-id="ac2a6-108">Azure 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="ac2a6-108">Create Azure resource group</span></span>
<span data-ttu-id="ac2a6-109">빌드 프로세스 동안 Packer는 원본 VM을 빌드하므로 임시 Azure 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-109">During the build process, Packer creates temporary Azure resources as it builds the source VM.</span></span> <span data-ttu-id="ac2a6-110">이미지로 사용하기 위해 해당 원본 VM을 캡처하려면 리소스 그룹을 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-110">To capture that source VM for use as an image, you must define a resource group.</span></span> <span data-ttu-id="ac2a6-111">Packer 빌드 프로세스의 출력은 이 리소스 그룹에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-111">The output from the Packer build process is stored in this resource group.</span></span>

<span data-ttu-id="ac2a6-112">[az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-112">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="ac2a6-113">다음 예제에서는 *eastus* 위치에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-113">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create -n myResourceGroup -l eastus
```


## <a name="create-azure-credentials"></a><span data-ttu-id="ac2a6-114">Azure 자격 증명 만들기</span><span class="sxs-lookup"><span data-stu-id="ac2a6-114">Create Azure credentials</span></span>
<span data-ttu-id="ac2a6-115">Packer는 서비스 사용자를 사용하여 Azure를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-115">Packer authenticates with Azure using a service principal.</span></span> <span data-ttu-id="ac2a6-116">Azure 서비스 사용자는 앱, 서비스 및 Packer와 같은 자동화 도구를 사용할 수 있는 보안 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-116">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Packer.</span></span> <span data-ttu-id="ac2a6-117">서비스 사용자가 Azure에서 수행할 수 있는 작업에 대한 사용 권한은 사용자가 제어하고 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-117">You control and define the permissions as to what operations the service principal can perform in Azure.</span></span>

<span data-ttu-id="ac2a6-118">[az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac)를 사용하여 서비스 사용자를 만들고 Packer가 필요로 하는 자격 증명을 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-118">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output the credentials that Packer needs:</span></span>

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

<span data-ttu-id="ac2a6-119">이전 명령에서 출력의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-119">An example of the output from the preceding commands is as follows:</span></span>

```azurecli
"f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
"0e760437-bf34-4aad-9f8d-870be799c55d",
"72f988bf-86f1-41af-91ab-2d7cd011db47"
```

<span data-ttu-id="ac2a6-120">Azure를 인증하기 위해 [az account show](/cli/azure/account#show)를 사용하여 Azure 구독 ID를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-120">To authenticate to Azure, you also need to obtain your Azure subscription ID with [az account show](/cli/azure/account#show):</span></span>

```azurecli
az account show --query [id] --output tsv
```

<span data-ttu-id="ac2a6-121">다음 단계에서 이러한 두 명령의 출력을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-121">You use the output from these two commands in the next step.</span></span>


## <a name="define-packer-template"></a><span data-ttu-id="ac2a6-122">Packer 템플릿 정의</span><span class="sxs-lookup"><span data-stu-id="ac2a6-122">Define Packer template</span></span>
<span data-ttu-id="ac2a6-123">이미지를 작성하려면 JSON 파일로 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-123">To build images, you create a template as a JSON file.</span></span> <span data-ttu-id="ac2a6-124">템플릿에서 실제 빌드 프로세스를 통해 수행하는 작성기와 프로비저너를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-124">In the template, you define builders and provisioners that carry out the actual build process.</span></span> <span data-ttu-id="ac2a6-125">Packer에는 이전 단계에서 만든 서비스 사용자 자격 증명과 같은 Azure 리소스를 정의하도록 허용하는 [Azure용 프로비저너](https://www.packer.io/docs/builders/azure.html)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-125">Packer has a [provisioner for Azure](https://www.packer.io/docs/builders/azure.html) that allows you to define Azure resources, such as the service principal credentials created in the preceding step.</span></span>

<span data-ttu-id="ac2a6-126">*ubuntu.json*이라는 파일을 만들고 다음 콘텐츠를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-126">Create a file named *ubuntu.json* and paste the following content.</span></span> <span data-ttu-id="ac2a6-127">다음에 대해 사용자 고유의 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-127">Enter your own values for the following:</span></span>

| <span data-ttu-id="ac2a6-128">매개 변수</span><span class="sxs-lookup"><span data-stu-id="ac2a6-128">Parameter</span></span>                           | <span data-ttu-id="ac2a6-129">얻을 수 있는 위치</span><span class="sxs-lookup"><span data-stu-id="ac2a6-129">Where to obtain</span></span> |
|-------------------------------------|----------------------------------------------------|
| <span data-ttu-id="ac2a6-130">*client_id*</span><span class="sxs-lookup"><span data-stu-id="ac2a6-130">*client_id*</span></span>                         | <span data-ttu-id="ac2a6-131">`az ad sp` create 명령의 첫 번째 출력 줄 - *appId*</span><span class="sxs-lookup"><span data-stu-id="ac2a6-131">First line of output from `az ad sp` create command - *appId*</span></span> |
| <span data-ttu-id="ac2a6-132">*client_secret*</span><span class="sxs-lookup"><span data-stu-id="ac2a6-132">*client_secret*</span></span>                     | <span data-ttu-id="ac2a6-133">`az ad sp` create 명령의 두 번째 출력 줄 - *password*</span><span class="sxs-lookup"><span data-stu-id="ac2a6-133">Second line of output from `az ad sp` create command - *password*</span></span> |
| <span data-ttu-id="ac2a6-134">*tenant_id*</span><span class="sxs-lookup"><span data-stu-id="ac2a6-134">*tenant_id*</span></span>                         | <span data-ttu-id="ac2a6-135">`az ad sp` create 명령의 세 번째 출력 줄 - *tenant*</span><span class="sxs-lookup"><span data-stu-id="ac2a6-135">Third line of output from `az ad sp` create command - *tenant*</span></span> |
| <span data-ttu-id="ac2a6-136">*subscription_id*</span><span class="sxs-lookup"><span data-stu-id="ac2a6-136">*subscription_id*</span></span>                   | <span data-ttu-id="ac2a6-137">`az account show` 명령의 출력</span><span class="sxs-lookup"><span data-stu-id="ac2a6-137">Output from `az account show` command</span></span> |
| <span data-ttu-id="ac2a6-138">*managed_image_resource_group_name*</span><span class="sxs-lookup"><span data-stu-id="ac2a6-138">*managed_image_resource_group_name*</span></span> | <span data-ttu-id="ac2a6-139">첫 번째 단계에서 만든 리소스 그룹의 이름</span><span class="sxs-lookup"><span data-stu-id="ac2a6-139">Name of resource group you created in the first step</span></span> |
| <span data-ttu-id="ac2a6-140">*managed_image_name*</span><span class="sxs-lookup"><span data-stu-id="ac2a6-140">*managed_image_name*</span></span>                | <span data-ttu-id="ac2a6-141">만들어진 관리되는 디스크 이미지의 이름</span><span class="sxs-lookup"><span data-stu-id="ac2a6-141">Name for the managed disk image that is created</span></span> |


```json
{
  "builders": [{
    "type": "azure-arm",

    "client_id": "f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
    "client_secret": "0e760437-bf34-4aad-9f8d-870be799c55d",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "subscription_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",

    "managed_image_resource_group_name": "myResourceGroup",
    "managed_image_name": "myPackerImage",

    "os_type": "Linux",
    "image_publisher": "Canonical",
    "image_offer": "UbuntuServer",
    "image_sku": "16.04-LTS",

    "azure_tags": {
        "dept": "Engineering",
        "task": "Image deployment"
    },

    "location": "East US",
    "vm_size": "Standard_DS2_v2"
  }],
  "provisioners": [{
    "execute_command": "chmod +x {{ .Path }}; {{ .Vars }} sudo -E sh '{{ .Path }}'",
    "inline": [
      "apt-get update",
      "apt-get upgrade -y",
      "apt-get -y install nginx",

      "/usr/sbin/waagent -force -deprovision+user && export HISTSIZE=0 && sync"
    ],
    "inline_shebang": "/bin/sh -x",
    "type": "shell"
  }]
}
```

<span data-ttu-id="ac2a6-142">이 템플릿은 Ubuntu 16.04 LTS 이미지를 빌드하고 NGINX를 설치한 다음 VM의 프로비전을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-142">This template builds an Ubuntu 16.04 LTS image, installs NGINX, then deprovisions the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="ac2a6-143">이 템플릿을 확장하여 사용자 자격 증명을 프로비전하는 경우 Azure 에이전트의 프로비전을 해제하여 `deprovision+user` 대신 `-deprovision`을 읽는 프로비저너 명령을 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-143">If you expand on this template to provision user credentials, adjust the provisioner command that deprovisions the Azure agent to read `-deprovision` rather than `deprovision+user`.</span></span>
> <span data-ttu-id="ac2a6-144">`+user` 플래그는 원본 VM에서 모든 사용자 계정을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-144">The `+user` flag removes all user accounts from the source VM.</span></span>


## <a name="build-packer-image"></a><span data-ttu-id="ac2a6-145">Packer 이미지 작성</span><span class="sxs-lookup"><span data-stu-id="ac2a6-145">Build Packer image</span></span>
<span data-ttu-id="ac2a6-146">로컬 컴퓨터에 Packer를 아직 설치하지 않은 경우 [Packer 설치 지침을 따릅니다](https://www.packer.io/docs/install/index.html).</span><span class="sxs-lookup"><span data-stu-id="ac2a6-146">If you don't already have Packer installed on your local machine, [follow the Packer installation instructions](https://www.packer.io/docs/install/index.html).</span></span>

<span data-ttu-id="ac2a6-147">다음과 같이 Packer 템플릿 파일을 지정하여 이미지를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-147">Build the image by specifying your Packer template file as follows:</span></span>

```bash
./packer build ubuntu.json
```

<span data-ttu-id="ac2a6-148">이전 명령에서 출력의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-148">An example of the output from the preceding commands is as follows:</span></span>

```bash
azure-arm output will be in this color.

==> azure-arm: Running builder ...
    azure-arm: Creating Azure Resource Manager (ARM) client ...
==> azure-arm: Creating resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Location          : ‘East US’
==> azure-arm:  -> Tags              :
==> azure-arm:  ->> dept : Engineering
==> azure-arm:  ->> task : Image deployment
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Getting the VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.218.147’
==> azure-arm: Waiting for SSH to become available...
==> azure-arm: Connected to SSH!
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-shell868574263
    azure-arm: WARNING! The waagent service will be stopped.
    azure-arm: WARNING! Cached DHCP leases will be deleted.
    azure-arm: WARNING! root password will be disabled. You will not be able to login as root.
    azure-arm: WARNING! /etc/resolvconf/resolv.conf.d/tail and /etc/resolvconf/resolv.conf.d/original will be deleted.
    azure-arm: WARNING! packer account and entire home directory will be deleted.
==> azure-arm: Querying the machine’s properties ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Managed OS Disk   : ‘/subscriptions/guid/resourceGroups/packer-Resource-Group-swtxmqm7ly/providers/Microsoft.Compute/disks/osdisk’
==> azure-arm: Powering off machine ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm: Capturing image ...
==> azure-arm:  -> Compute ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Compute Name              : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Compute Location          : ‘East US’
==> azure-arm:  -> Image ResourceGroupName   : ‘myResourceGroup’
==> azure-arm:  -> Image Name                : ‘myPackerImage’
==> azure-arm:  -> Image Location            : ‘eastus’
==> azure-arm: Deleting resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm: Deleting the temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. The artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```


## <a name="create-vm-from-azure-image"></a><span data-ttu-id="ac2a6-149">Azure 이미지에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="ac2a6-149">Create VM from Azure Image</span></span>
<span data-ttu-id="ac2a6-150">이제 [az vm create](/cli/azure/vm#create)를 사용하여 이미지에서 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-150">You can now create a VM from your Image with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="ac2a6-151">`--image` 매개 변수를 사용하여 만든 이미지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-151">Specify the Image you created with the `--image` parameter.</span></span> <span data-ttu-id="ac2a6-152">다음 예제에서는 *myPackerImage*에서 *myVM*이라는 VM을 만들고 SSH 키가 아직 없으면 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-152">The following example creates a VM named *myVM* from *myPackerImage* and generates SSH keys if they do not already exist:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image myPackerImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="ac2a6-153">VM을 만드는 데 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-153">It takes a few minutes to create the VM.</span></span> <span data-ttu-id="ac2a6-154">VM이 만들어지면 Azure CLI에 표시된 `publicIpAddress`를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-154">Once the VM has been created, take note of the `publicIpAddress` displayed by the Azure CLI.</span></span> <span data-ttu-id="ac2a6-155">이 주소는 웹 브라우저를 통해 NGINX 사이트에 액세스할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-155">This address is used to access the NGINX site via a web browser.</span></span>

<span data-ttu-id="ac2a6-156">웹 트래픽이 VM에 도달하도록 허용하려면 [az vm open-port](/cli/azure/vm#open-port)를 사용하여 인터넷에서 포트 80을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-156">To allow web traffic to reach your VM, open port 80 from the Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli
az vm open-port \
    --resource-group myResourceGroup \
    --name myVM \
    --port 80
```

## <a name="test-vm-and-nginx"></a><span data-ttu-id="ac2a6-157">VM 및 NGINX 테스트</span><span class="sxs-lookup"><span data-stu-id="ac2a6-157">Test VM and NGINX</span></span>
<span data-ttu-id="ac2a6-158">이제 웹 브라우저를 열고 주소 표시줄에 `http://publicIpAddress`를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-158">Now you can open a web browser and enter `http://publicIpAddress` in the address bar.</span></span> <span data-ttu-id="ac2a6-159">VM 만들기 프로세스에서 사용자 고유의 공용 IP 주소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-159">Provide your own public IP address from the VM create process.</span></span> <span data-ttu-id="ac2a6-160">기본 NGINX 페이지는 다음 예제와 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-160">The default NGINX page is displayed as in the following example:</span></span>

![NGINX 기본 사이트](./media/build-image-with-packer/nginx.png) 


## <a name="next-steps"></a><span data-ttu-id="ac2a6-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ac2a6-162">Next steps</span></span>
<span data-ttu-id="ac2a6-163">이 예제에서는 이미 설치된 NGINX를 사용하여 VM 이미지를 만드는 데 Packer를 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-163">In this example, you used Packer to create a VM image with NGINX already installed.</span></span> <span data-ttu-id="ac2a6-164">Ansible, Chef 또는 Puppet를 사용하여 이미지에서 만든 VM에 앱을 배포하는 것과 같은 기존 배포 워크플로와 함께 이 VM 이미지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-164">You can use this VM image alongside existing deployment workflows, such as to deploy your app to VMs created from the Image with Ansible, Chef, or Puppet.</span></span>

<span data-ttu-id="ac2a6-165">다른 Linux 배포판에 대한 추가 예제 Packer 템플릿은 [이 GitHub 리포지토리](https://github.com/hashicorp/packer/tree/master/examples/azure)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac2a6-165">For additional example Packer templates for other Linux distros, see [this GitHub repo](https://github.com/hashicorp/packer/tree/master/examples/azure).</span></span>