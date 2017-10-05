---
title: "Azure의 Linux 가상 컴퓨터에 LAMP 배포 | Microsoft Docs"
description: "Azure의 Linux VM에 LAMP 스택 설치 방법을 알아보기"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jluk
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: ad69876bfbeba5f948a81e5c48c659fdf2265ae2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-lamp-stack-on-azure"></a><span data-ttu-id="34800-103">Azure에서 LAMP 스택 배포</span><span class="sxs-lookup"><span data-stu-id="34800-103">Deploy LAMP stack on Azure</span></span>
<span data-ttu-id="34800-104">이 문서에서는 Azure에서 Apache 웹 서버, MySQL 및 PHP(LAMP 스택)를 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="34800-104">This article walks you through how to deploy an Apache web server, MySQL, and PHP (the LAMP stack) on Azure.</span></span> <span data-ttu-id="34800-105">Azure 계정([무료 평가판 받기](https://azure.microsoft.com/pricing/free-trial/)) 및 [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="34800-105">You need an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and the [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span> <span data-ttu-id="34800-106">[Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 이러한 단계를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34800-106">You can also perform these steps with the [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="34800-107">빠른 명령 요약</span><span class="sxs-lookup"><span data-stu-id="34800-107">Quick command summary</span></span>

1. <span data-ttu-id="34800-108">선호하는 로컬 컴퓨터에 [azuredeploy.parameters.json 파일](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json)을 저장하고 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="34800-108">Save and edit the [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) to your preference on your local machine.</span></span>
2. <span data-ttu-id="34800-109">리소스 그룹을 만들고 템플릿을 배포하려면 두 개의 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="34800-109">Run the following two commands to create a resource group and then deploy your template:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

### <a name="deploy-lamp-on-existing-vm"></a><span data-ttu-id="34800-110">기존 VM에 LAMP 배포</span><span class="sxs-lookup"><span data-stu-id="34800-110">Deploy LAMP on existing VM</span></span>
<span data-ttu-id="34800-111">다음 명령은 패키지를 업데이트한 다음 Apache, MySQL 및 PHP를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="34800-111">The following commands updates packages, then installs Apache, MySQL, and PHP:</span></span>

```bash
sudo apt-get update
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="34800-112">새 VM에 LAMP 배포 연습</span><span class="sxs-lookup"><span data-stu-id="34800-112">Deploy LAMP on new VM walkthrough</span></span>

1. <span data-ttu-id="34800-113">새 VM을 포함하려면 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="34800-113">Create a resource group with [az group create](/cli/azure/group#create) to contain the new VM:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
```
<span data-ttu-id="34800-114">VM 자체를 만들려면 [여기 GitHub에서](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app)찾을 수 있는 이미 작성된 Azure Resource Manager 템플릿을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34800-114">To create the VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

2. <span data-ttu-id="34800-115">로컬 컴퓨터에 [azuredeploy.parameters.json 파일](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json)을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="34800-115">Save the [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) to your local machine.</span></span>
3. <span data-ttu-id="34800-116">기본 설정된 컴퓨터에 대한 **azuredeploy.parameters.json 파일**을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="34800-116">Edit the **azuredeploy.parameters.json** file to your preferred inputs.</span></span>
4. <span data-ttu-id="34800-117">다운로드한 json 파일을 참조하여 [az group deployment create]로 템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="34800-117">Deploy the template with [az group deployment create] referencing the downloaded json file:</span></span>

```azurecli
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

<span data-ttu-id="34800-118">다음 예제와 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="34800-118">The output is similar to the following example:</span></span>

```json
{
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup/providers/Microsoft.Resources/deployments/azuredeploy",
"name": "azuredeploy",
"properties": {
    "correlationId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "debugSetting": null,
}
...
"provisioningState": "Succeeded",
"template": null,
"templateLink": {
    "contentVersion": "1.0.0.0",
    "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json"
    },
    "timestamp": "2017-02-22T00:05:51.860411+00:00"
},
"resourceGroup": "myResourceGroup"
}
```

<span data-ttu-id="34800-119">이미 설치된 LAMP를 사용해 이제 Linux VM을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="34800-119">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="34800-120">원하는 경우 [LAMP가 성공적으로 설치되었는지 확인](#verify-lamp-successfully-installed)으로 이동하여 설치를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34800-120">If you wish, you can verify the install by jumping down to [Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="34800-121">기존 VM에 LAMP 배포 연습</span><span class="sxs-lookup"><span data-stu-id="34800-121">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="34800-122">Linux VM을 만드는 데 도움이 필요한 경우 [Linux VM을 만드는 방법을 알아보려면 여기](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli)로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34800-122">If you need help creating a Linux VM, you can head [here to learn how to create a Linux VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span></span> <span data-ttu-id="34800-123">다음으로, Linux VM에 SSH해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34800-123">Next, you need to SSH into the Linux VM.</span></span> <span data-ttu-id="34800-124">SSH 키를 만드는 데 도움이 필요한 경우 [Linux/Mac에서 SSH 키를 만드는 방법을 알아보려면 여기](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34800-124">If you need help with creating an SSH key, you can head [here to learn how to create an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="34800-125">SSH 키가 있는 경우 계속해서 `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`을 사용하여 Linux VM에 SSH합니다.</span><span class="sxs-lookup"><span data-stu-id="34800-125">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="34800-126">이제 Linux VM 내에서 작업할 수 있으므로 Debian 기반 배포에 LAMP 스택을 설치하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="34800-126">Now that you are working within your Linux VM, we can walk through installing the LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="34800-127">정확한 명령은 다른 Linux 배포판에서 다를 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34800-127">The exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="34800-128">Debian/Ubuntu에 설치</span><span class="sxs-lookup"><span data-stu-id="34800-128">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="34800-129">`apache2`, `mysql-server`, `php5`, `php5-mysql` 패키지를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34800-129">You need the following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="34800-130">이러한 패키지를 직접 가져오거나 Tasksel을 사용하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34800-130">You can install these packages by directly grabbing these packages or using Tasksel.</span></span>
<span data-ttu-id="34800-131">설치하기 전에 패키지 목록을 다운로드하고 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34800-131">Before installing you need to download and update package lists.</span></span>

```bash
sudo apt-get update
```

##### <a name="individual-packages"></a><span data-ttu-id="34800-132">개별 패키지</span><span class="sxs-lookup"><span data-stu-id="34800-132">Individual packages</span></span>
<span data-ttu-id="34800-133">apt-get을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="34800-133">Using apt-get:</span></span>

```bash
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

##### <a name="using-tasksel"></a><span data-ttu-id="34800-134">Tasksel 사용</span><span class="sxs-lookup"><span data-stu-id="34800-134">Using tasksel</span></span>
<span data-ttu-id="34800-135">또는 관련된 여러 패키지를 하나의 조정된 “작업”으로 시스템에 설치하는 Debian/Ubuntu 도구인 Tasksel을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34800-135">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

```bash
sudo apt-get install tasksel
sudo tasksel install lamp-server
```

<span data-ttu-id="34800-136">이전의 옵션 중 하나를 실행하고 나면 이러한 패키지와 다양한 다른 종속성을 설치할지를 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="34800-136">After running either of the previous options, you will be prompted to install these packages and various other dependencies.</span></span> <span data-ttu-id="34800-137">MySQL에 대한 관리 암호를 설정하려면 'y'를 누른 후 'Enter' 키를 누르고 다른 프롬프트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="34800-137">To set an administrative password for MySQL, press 'y' and then 'Enter' to continue, and follow any other prompts.</span></span> <span data-ttu-id="34800-138">이 프로세스에서는 PHP와 MySQL을 함께 사용하는 데 필요한 최소한의 PHP 확장을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="34800-138">This process installs the minimum required PHP extensions needed to use PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="34800-139">다음 명령을 실행하여 패키지로 사용 가능한 다른 PHP 확장을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="34800-139">Run the following command to see other PHP extensions that are available as packages:</span></span>

```bash
apt-cache search php5
```

#### <a name="create-infophp-document"></a><span data-ttu-id="34800-140">Info.php 문서 만들기</span><span class="sxs-lookup"><span data-stu-id="34800-140">Create info.php document</span></span>
<span data-ttu-id="34800-141">이제 명령줄에 `apache2 -v`, `mysql -v`, 또는 `php -v`을 입력하여 Apache, MySQL 및 PHP의 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34800-141">You should now be able to check what version of Apache, MySQL, and PHP you have through the command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="34800-142">테스트를 추가 하려는 경우 브라우저에서 보려면 빠른 PHP 정보 페이지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34800-142">If you would like to test further, you can create a quick PHP info page to view in a browser.</span></span> <span data-ttu-id="34800-143">이 명령을 사용하여 Nano 텍스트 편집기로 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="34800-143">Create a file with Nano text editor with this command:</span></span>

```bash
sudo nano /var/www/html/info.php
```

<span data-ttu-id="34800-144">GNU Nano 텍스트 편집기에서 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="34800-144">Within the GNU Nano text editor, add the following lines:</span></span>

```php
<?php
phpinfo();
?>
```

<span data-ttu-id="34800-145">그런 다음 저장하고 텍스트 편집기를 끝냅니다.</span><span class="sxs-lookup"><span data-stu-id="34800-145">Then save and exit the text editor.</span></span>

<span data-ttu-id="34800-146">모든 새 설치 항목이 적용되도록 이 명령을 사용하여 Apache를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="34800-146">Restart Apache with this command so all new installs take effect.</span></span>

```bash
sudo service apache2 restart
```

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="34800-147">LAMP 설치가 성공적인지 확인</span><span class="sxs-lookup"><span data-stu-id="34800-147">Verify LAMP successfully installed</span></span>
<span data-ttu-id="34800-148">이제 브라우저를 열고 http://youruniqueDNS/info.php로 이동하여 만든 PHP 정보 페이지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34800-148">Now you can check the PHP info page you created by opening a browser and going to http://youruniqueDNS/info.php.</span></span> <span data-ttu-id="34800-149">이 이미지와 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="34800-149">It should look similar to this image.</span></span>

![][2]

<span data-ttu-id="34800-150">http://youruniqueDNS/로 이동하여 Apache2 Ubuntu 기본 페이지 보기로 Apache 설치를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34800-150">You can check your Apache installation by viewing the Apache2 Ubuntu Default Page by going to you http://youruniqueDNS/.</span></span> <span data-ttu-id="34800-151">다음 예제와 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="34800-151">The output is similar to the following example:</span></span>

![][3]

<span data-ttu-id="34800-152">축하합니다. 이제 방금 Azure Vm에 LAMP 스택 설정을 마쳤습니다!</span><span class="sxs-lookup"><span data-stu-id="34800-152">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="34800-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="34800-153">Next steps</span></span>
<span data-ttu-id="34800-154">LAMP 스택에서 Ubuntu 설명서를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="34800-154">Check out the Ubuntu documentation on the LAMP stack:</span></span>

* [<span data-ttu-id="34800-155">https://help.ubuntu.com/community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="34800-155">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png
