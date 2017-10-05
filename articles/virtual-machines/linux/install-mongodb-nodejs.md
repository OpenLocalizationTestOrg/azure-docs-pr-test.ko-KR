---
title: "Azure CLI 1.0을 사용하여 Linux VM에 MongoDB 설치 | Microsoft Docs"
description: "리소스 관리자 배포 모델을 사용하여 Azure에서 Linux 가상 컴퓨터에 MongoDB를 설치하고 구성하는 방법을 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 3f55b546-86df-4442-9ef4-8a25fae7b96e
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: c97ade0a3d95824f723aad55776de861fe49441f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-install-and-configure-mongodb-on-a-linux-vm-using-the-azure-cli-10"></a><span data-ttu-id="b1482-103">Azure CLI 1.0을 사용하여 Linux VM에 MongoDB를 설치하고 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="b1482-103">How to install and configure MongoDB on a Linux VM using the Azure CLI 1.0</span></span>
<span data-ttu-id="b1482-104">[MongoDB](http://www.mongodb.org)는 인기 있는 고성능 오픈 소스 NoSQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="b1482-105">이 문서는 리소스 관리자 배포 모델을 사용하여 Azure에서 Linux VM에 MongoDB를 설치하고 구성하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-105">This article shows you how to install and configure MongoDB on a Linux VM in Azure using the Resource Manager deployment model.</span></span> <span data-ttu-id="b1482-106">표시된 예제는 다음과 같은 방법을 자세히 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-106">Examples are shown that detail how to:</span></span>

* [<span data-ttu-id="b1482-107">기본 MongoDB 인스턴스를 수동으로 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="b1482-107">Manually install and configure a basic MongoDB instance</span></span>](#manually-install-and-configure-mongodb-on-a-vm)
* [<span data-ttu-id="b1482-108">Resource Manager 템플릿을 사용하여 기본 MongoDB 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="b1482-108">Create a basic MongoDB instance using a Resource Manager template</span></span>](#create-basic-mongodb-instance-on-centos-using-a-template)
* [<span data-ttu-id="b1482-109">Resource Manager 템플릿을 사용하여 복제본 세트로 복합적인 MongoDB 분할된 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="b1482-109">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span></span>](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="b1482-110">태스크를 완료하기 위한 CLI 버전</span><span class="sxs-lookup"><span data-stu-id="b1482-110">CLI versions to complete the task</span></span>
<span data-ttu-id="b1482-111">다음 CLI 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-111">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="b1482-112">Azure CLI 1.0 - 클래식 및 리소스 관리 배포 모델용 CLI(이 문서)</span><span class="sxs-lookup"><span data-stu-id="b1482-112">Azure CLI 1.0 – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="b1482-113">[Azure CLI 2.0](create-cli-complete-nodejs.md) - 리소스 관리 배포 모델용 차세대 CLI</span><span class="sxs-lookup"><span data-stu-id="b1482-113">[Azure CLI 2.0](create-cli-complete-nodejs.md) - our next generation CLI for the resource management deployment model</span></span>


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="b1482-114">VM에서 MongoDB 수동 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="b1482-114">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="b1482-115">MongoDB는 Red Hat/CentOS, SUSE, Ubuntu 및 Debian을 포함하는 Linux 배포판에 대한 [설치 지침을 제공](https://docs.mongodb.com/manual/administration/install-on-linux/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-115">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="b1482-116">다음 예제는 *~/.ssh/id_rsa.pub*에 저장된 SSH 키를 사용하여 *CentOS* VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-116">The following example creates a *CentOS* VM using an SSH key stored at *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="b1482-117">저장소 계정 이름, DNS 이름, 관리자 자격 증명을 묻는 프롬프트에 답변합니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-117">Answer the prompts for storage account name, DNS name, and admin credentials:</span></span>

```azurecli
azure vm quick-create \
    --image-urn CentOS \
    --ssh-publickey-file ~/.ssh/id_rsa.pub 
```

<span data-ttu-id="b1482-118">앞의 VM 생성 단계 끝에 표시된 공용 IP 주소를 사용하여 VM에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-118">Log on to the VM using the public IP address displayed at the end of the preceding VM creation step:</span></span>

```bash
ssh azureuser@40.78.23.145
```

<span data-ttu-id="b1482-119">MongoDB에 대한 설치 원본을 추가하려면 다음과 같이 **yum** 리포지토리 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-119">To add the installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="b1482-120">편집을 위해 MongoDB 리포지토리 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-120">Open the MongoDB repo file for editing.</span></span> <span data-ttu-id="b1482-121">다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-121">Add the following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="b1482-122">다음과 같이 **yum**을 사용하여 MongoDB를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-122">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="b1482-123">기본적으로 MongoDB 액세스를 막는 CentOS 이미지에 SELinux가 강제 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-123">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="b1482-124">다음과 같이 정책 관리 도구를 설치하고 MongoDB가 자체적인 기본 TCP 포트 27017에서 작업을 허용하도록 SELinux를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-124">Install policy management tools and configure SELinux to allow MongoDB to operate on its default TCP port 27017 as follows.</span></span> 

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="b1482-125">다음과 같이 MongoDB 서비스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-125">Start the MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="b1482-126">로컬 `mongo` 클라이언트를 사용하여 연결하여 MongoDB 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-126">Verify the MongoDB installation by connecting using the local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="b1482-127">이제 데이터를 추가한 후 검색하여 MongoDB 인스턴스를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-127">Now test the MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="b1482-128">필요하면 시스템을 다시 부팅하는 동안 MongoDB를 자동으로 시작하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-128">If desired, configure MongoDB to start automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="b1482-129">템플릿을 사용하여 CentOS에서 기본 MongoDB 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="b1482-129">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="b1482-130">GitHub의 다음과 같은 Azure 빠른 시작 템플릿을 사용하여 단일 CentOS VM에 기본 MongoDB 인스턴스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-130">You can create a basic MongoDB instance on a single CentOS VM using the following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="b1482-131">이 템플릿은 Linux용 사용자 지정 스크립트 확장을 사용하여 새로 만든 CentOS VM에 `yum` 리포지토리를 추가한 후 MongoDB를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-131">This template uses the Custom Script extension for Linux to add a `yum` repository to your newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="b1482-132">[CentOS의 기본 MongoDB 인스턴스](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="b1482-132">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="b1482-133">다음 예제는 `eastus` 지역에 `myResourceGroup`이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-133">The following example creates a resource group with the name `myResourceGroup` in the `eastus` region.</span></span> <span data-ttu-id="b1482-134">다음과 같이 사용자 고유의 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-134">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="b1482-135">Azure CLI는 배포 생성 몇 초 내에 프롬프트를 반환하지만 설치 및 구성 작업이 완료되려면 몇 분 정도 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-135">The Azure CLI returns you to a prompt within a few seconds of creating the deployment, but the installation and configuration takes a few minutes to complete.</span></span> <span data-ttu-id="b1482-136">`azure group deployment show myResourceGroup`을 사용하고 해당 리소스 그룹의 이름을 입력하여 배포 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-136">Check the status of the deployment with `azure group deployment show myResourceGroup`, entering the name of your resource group accordingly.</span></span> <span data-ttu-id="b1482-137">VM에 SSH를 시도하기 전에 **ProvisioningState**에 *Succeeded*가 표시될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-137">Wait until the **ProvisioningState** shows *Succeeded* before trying to SSH to the VM.</span></span>

<span data-ttu-id="b1482-138">배포가 완료되면 VM에 SSH를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-138">Once the deployment is complete, SSH to the VM.</span></span> <span data-ttu-id="b1482-139">다음 예제와 같이 `azure vm show` 명령을 사용하여 VM의 IP 주소를 불러옵니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-139">Obtain the IP address of your VM using the `azure vm show` command as in the following example:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myLinuxVM
```

<span data-ttu-id="b1482-140">출력의 끝 쪽에 공용 IP 주소가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-140">Near the end of the output, the public IP address is displayed.</span></span> <span data-ttu-id="b1482-141">VM의 IP 주소를 사용하여 VM에 SSH를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-141">SSH to your VM with the IP address of your VM:</span></span>

```bash
ssh azureuser@138.91.149.74
```

<span data-ttu-id="b1482-142">다음과 같이 로컬 `mongo` 클라이언트를 사용하여 연결하여 MongoDB 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-142">Verify the MongoDB installation by connecting using the local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="b1482-143">이제 다음과 같이 데이터를 추가한 후 검색하여 인스턴스를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-143">Now test the instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="b1482-144">템플릿을 사용하여 CentOS에서 복합적인 MongoDB 분할된 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="b1482-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="b1482-145">GitHub의 다음과 같은 Azure 빠른 시작 템플릿을 사용하여 복합적인 MongoDB 분할된 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-145">You can create a complex MongoDB sharded cluster using the following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="b1482-146">이 템플릿은 [MongoDB 분할된 클러스터 모범 사례](https://docs.mongodb.com/manual/core/sharded-cluster-components/)에 따라 중복성 및 고가용성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-146">This template follows the [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) to provide redundancy and high availability.</span></span> <span data-ttu-id="b1482-147">템플릿은 각 복제본 세트에 3개의 노드가 있는 2개의 분할 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-147">The template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="b1482-148">노드가 3개 있는 구성 서버 복제본 세트 하나와 **mongos** 라우터 서버 2개가 만들어져서 분할 전반의 응용 프로그램에 대한 일관성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-148">One config server replica set with three nodes is also created, plus two **mongos** router servers to provide consistency to applications from across the shards.</span></span>

* <span data-ttu-id="b1482-149">[CentOS의 MongoDB 분할 클러스터](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="b1482-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="b1482-150">이러한 복합적인 MongoDB 분할된 클러스터를 배포하려면 20개가 넘는 코어가 필요하며, 일반적으로 이 수치는 구독에 대한 지역당 기본 코어 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically the default core count per region for a subscription.</span></span> <span data-ttu-id="b1482-151">코어 수를 늘리려면 Azure 지원 요청을 생성하십시오.</span><span class="sxs-lookup"><span data-stu-id="b1482-151">Open an Azure support request to increase your core count.</span></span>

<span data-ttu-id="b1482-152">다음 예제에서는 *eastus* 지역에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-152">The following example creates a resource group with the name *myResourceGroup* in the *eastus* region.</span></span> <span data-ttu-id="b1482-153">다음과 같이 사용자 고유의 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-153">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="b1482-154">Azure CLI는 배포 생성 몇 초 내에 프롬프트를 반환하지만 설치 및 구성 작업이 완료되려면 한 시간이 넘게 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-154">The Azure CLI returns you to a prompt within a few seconds of creating the deployment, but the installation and configuration can take over an hour to complete.</span></span> <span data-ttu-id="b1482-155">`azure group deployment show myResourceGroup`을 사용하고 리소스 그룹의 이름을 맞게 조정하여 배포 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-155">Check the status of the deployment with `azure group deployment show myResourceGroup`, adjusting the name of your resource group accordingly.</span></span> <span data-ttu-id="b1482-156">VM에 연결하기 전에 **ProvisioningState**에 *Succeeded*가 표시될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-156">Wait until the **ProvisioningState** shows *Succeeded* before connecting to the VMs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b1482-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b1482-157">Next steps</span></span>
<span data-ttu-id="b1482-158">이 예는 VM을 통해 로컬에서 MongoDB 인스턴스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-158">In these examples, you connect to the MongoDB instance locally from the VM.</span></span> <span data-ttu-id="b1482-159">다른 VM 또는 네트워크에서 MongoDB 인스턴스에 연결하려면 적절한 [네트워크 보안 그룹 규칙이 생성되어있어야](nsg-quickstart.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-159">If you want to connect to the MongoDB instance from another VM or network, ensure the appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="b1482-160">템플릿을 사용하여 만드는 방법에 대한 자세한 내용은 [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b1482-160">For more information about creating using templates, see the [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="b1482-161">Azure Resource Manager 템플릿은 사용자 지정 스크립트 확장을 사용하여 VM에 스크립트를 다운로드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b1482-161">The Azure Resource Manager templates use the Custom Script Extension to download and execute scripts on your VMs.</span></span> <span data-ttu-id="b1482-162">자세한 내용은 [Linux 가상 컴퓨터에서 Azure 사용자 지정 스크립트 확장 사용](extensions-customscript.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b1482-162">For more information, see [Using the Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

