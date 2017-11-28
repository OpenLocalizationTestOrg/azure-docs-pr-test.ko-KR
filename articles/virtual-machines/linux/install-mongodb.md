---
title: "Azure CLI를 사용하여 Linux VM에 MongoDB 설치 | Microsoft Docs"
description: "Azure CLI 2.0을 사용하여 Linux 가상 컴퓨터에 MongoDB를 설치하고 구성하는 방법 알아보기"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 3f55b546-86df-4442-9ef4-8a25fae7b96e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: e19c09558285497f29eb78b4f4ae5b15d7f1a191
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-install-and-configure-mongodb-on-a-linux-vm"></a><span data-ttu-id="b4660-103">Linux VM에 MongoDB를 설치하고 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="b4660-103">How to install and configure MongoDB on a Linux VM</span></span>
<span data-ttu-id="b4660-104">[MongoDB](http://www.mongodb.org)는 인기 있는 고성능 오픈 소스 NoSQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="b4660-105">이 문서에서는 Azure CLI 2.0을 사용하여 Linux VM에 MongoDB를 설치하고 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-105">This article shows you how to install and configure MongoDB on a Linux VM with the Azure CLI 2.0.</span></span> <span data-ttu-id="b4660-106">[Azure CLI 1.0](install-mongodb-nodejs.md)에서 이러한 단계를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-106">You can also perform these steps with the [Azure CLI 1.0](install-mongodb-nodejs.md).</span></span> <span data-ttu-id="b4660-107">표시된 예제는 다음과 같은 방법을 자세히 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-107">Examples are shown that detail how to:</span></span>

* [<span data-ttu-id="b4660-108">기본 MongoDB 인스턴스를 수동으로 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="b4660-108">Manually install and configure a basic MongoDB instance</span></span>](#manually-install-and-configure-mongodb-on-a-vm)
* [<span data-ttu-id="b4660-109">Resource Manager 템플릿을 사용하여 기본 MongoDB 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="b4660-109">Create a basic MongoDB instance using a Resource Manager template</span></span>](#create-basic-mongodb-instance-on-centos-using-a-template)
* [<span data-ttu-id="b4660-110">Resource Manager 템플릿을 사용하여 복제본 세트로 복합적인 MongoDB 분할된 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="b4660-110">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span></span>](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="b4660-111">VM에서 MongoDB 수동 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="b4660-111">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="b4660-112">MongoDB는 Red Hat/CentOS, SUSE, Ubuntu 및 Debian을 포함하는 Linux 배포판에 대한 [설치 지침을 제공](https://docs.mongodb.com/manual/administration/install-on-linux/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-112">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="b4660-113">다음 예제는 *CentOS* VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-113">The following example creates a *CentOS* VM.</span></span> <span data-ttu-id="b4660-114">이 환경을 만들려면 최신 [Azure CLI 2.0](/cli/azure/install-az-cli2)을 설치하고 [az login](/cli/azure/#login)을 사용하여 Azure 계정에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-114">To create this environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="b4660-115">[az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-115">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="b4660-116">다음 예제에서는 *eastus* 위치에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-116">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="b4660-117">[az vm create](/cli/azure/vm#create)로 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-117">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="b4660-118">다음 예제에서는 SSH 공개 키 인증을 사용하여 *azureuser*라는 사용자로 *myVM*이라는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-118">The following example creates a VM named *myVM* with a user named *azureuser* using SSH public key authentication</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="b4660-119">고유한 사용자 이름을 사용하는 VM에 대한 SSH 및 이전 단계의 출력에 나열된 `publicIpAddress`는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-119">SSH to the VM using your own username and the `publicIpAddress` listed in the output from the previous step:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="b4660-120">MongoDB에 대한 설치 원본을 추가하려면 다음과 같이 **yum** 리포지토리 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-120">To add the installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="b4660-121">편집을 위해 MongoDB 리포지토리 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-121">Open the MongoDB repo file for editing.</span></span> <span data-ttu-id="b4660-122">다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-122">Add the following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="b4660-123">다음과 같이 **yum**을 사용하여 MongoDB를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-123">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="b4660-124">기본적으로 MongoDB 액세스를 막는 CentOS 이미지에 SELinux가 강제 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-124">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="b4660-125">다음과 같이 정책 관리 도구를 설치하고 MongoDB가 자체적인 기본 TCP 포트 27017에서 작업을 허용하도록 SELinux를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-125">Install policy management tools and configure SELinux to allow MongoDB to operate on its default TCP port 27017 as follows:</span></span>

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="b4660-126">다음과 같이 MongoDB 서비스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-126">Start the MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="b4660-127">로컬 `mongo` 클라이언트를 사용하여 연결하여 MongoDB 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-127">Verify the MongoDB installation by connecting using the local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="b4660-128">이제 데이터를 추가한 후 검색하여 MongoDB 인스턴스를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-128">Now test the MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="b4660-129">필요하면 시스템을 다시 부팅하는 동안 MongoDB를 자동으로 시작하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-129">If desired, configure MongoDB to start automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="b4660-130">템플릿을 사용하여 CentOS에서 기본 MongoDB 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="b4660-130">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="b4660-131">GitHub의 다음과 같은 Azure 빠른 시작 템플릿을 사용하여 단일 CentOS VM에 기본 MongoDB 인스턴스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-131">You can create a basic MongoDB instance on a single CentOS VM using the following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="b4660-132">이 템플릿은 Linux용 사용자 지정 스크립트 확장을 사용하여 새로 만든 CentOS VM에 **yum** 리포지토리를 추가한 후 MongoDB를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-132">This template uses the Custom Script extension for Linux to add a **yum** repository to your newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="b4660-133">[CentOS의 기본 MongoDB 인스턴스](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="b4660-133">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="b4660-134">이 환경을 만들려면 최신 [Azure CLI 2.0](/cli/azure/install-az-cli2)을 설치하고 [az login](/cli/azure/#login)을 사용하여 Azure 계정에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-134">To create this environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="b4660-135">먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-135">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="b4660-136">다음 예제에서는 *eastus* 위치에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-136">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="b4660-137">다음으로 [az group deployment create](/cli/azure/group/deployment#create)를 사용하여 MongoDB 템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-137">Next, deploy the MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="b4660-138">*newStorageAccountName*, *virtualNetworkName* 및 *vmSize* 등에 필요한 대로, 고유한 리소스 이름 및 크기를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-138">Define your own resource names and sizes where needed such as for *newStorageAccountName*, *virtualNetworkName*, and *vmSize*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"},
    "virtualNetworkName": {"value": "myVnet"},
    "vmSize": {"value": "Standard_DS2_v2"},
    "vmName": {"value": "myVM"},
    "publicIPAddressName": {"value": "myPublicIP"},
    "nicName": {"value": "myNic"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

<span data-ttu-id="b4660-139">VM의 공용 DNS 주소를 사용하여 VM에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-139">Log on to the VM using the public DNS address of your VM.</span></span> <span data-ttu-id="b4660-140">[az vm show](/cli/azure/vm#show)를 사용하여 공용 DNS 주소를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-140">You can view the public DNS address with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show -g myResourceGroup -n myVM -d --query [fqdns] -o tsv
```

<span data-ttu-id="b4660-141">고유한 사용자 이름 및 공용 DNS 주소를 사용하여 VM에 SSH합니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-141">SSH to your VM using your own username and public DNS address:</span></span>

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

<span data-ttu-id="b4660-142">다음과 같이 로컬 `mongo` 클라이언트를 사용하여 연결하여 MongoDB 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-142">Verify the MongoDB installation by connecting using the local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="b4660-143">이제 다음과 같이 데이터를 추가한 후 검색하여 인스턴스를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-143">Now test the instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="b4660-144">템플릿을 사용하여 CentOS에서 복합적인 MongoDB 분할된 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="b4660-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="b4660-145">GitHub의 다음과 같은 Azure 빠른 시작 템플릿을 사용하여 복합적인 MongoDB 분할된 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-145">You can create a complex MongoDB sharded cluster using the following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="b4660-146">이 템플릿은 [MongoDB 분할된 클러스터 모범 사례](https://docs.mongodb.com/manual/core/sharded-cluster-components/)에 따라 중복성 및 고가용성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-146">This template follows the [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) to provide redundancy and high availability.</span></span> <span data-ttu-id="b4660-147">템플릿은 각 복제본 세트에 3개의 노드가 있는 2개의 분할 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-147">The template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="b4660-148">노드가 3개 있는 구성 서버 복제본 세트 하나와 **mongos** 라우터 서버 2개가 만들어져서 분할 전반의 응용 프로그램에 대한 일관성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-148">One config server replica set with three nodes is also created, plus two **mongos** router servers to provide consistency to applications from across the shards.</span></span>

* <span data-ttu-id="b4660-149">[CentOS의 MongoDB 분할 클러스터](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="b4660-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="b4660-150">이러한 복합적인 MongoDB 분할된 클러스터를 배포하려면 20개가 넘는 코어가 필요하며, 일반적으로 이 수치는 구독에 대한 지역당 기본 코어 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically the default core count per region for a subscription.</span></span> <span data-ttu-id="b4660-151">코어 수를 늘리려면 Azure 지원 요청을 생성하십시오.</span><span class="sxs-lookup"><span data-stu-id="b4660-151">Open an Azure support request to increase your core count.</span></span>

<span data-ttu-id="b4660-152">이 환경을 만들려면 최신 [Azure CLI 2.0](/cli/azure/install-az-cli2)을 설치하고 [az login](/cli/azure/#login)을 사용하여 Azure 계정에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-152">To create this environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="b4660-153">먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-153">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="b4660-154">다음 예제에서는 *eastus* 위치에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-154">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="b4660-155">다음으로 [az group deployment create](/cli/azure/group/deployment#create)를 사용하여 MongoDB 템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-155">Next, deploy the MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="b4660-156">*mongoAdminUsername*, *sizeOfDataDiskInGB* 및 *configNodeVmSize* 등에 필요한 대로, 고유한 리소스 이름 및 크기를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-156">Define your own resource names and sizes where needed such as for *mongoAdminUsername*, *sizeOfDataDiskInGB*, and *configNodeVmSize*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "mongoAdminUsername": {"value": "mongoadmin"},
    "mongoAdminPassword": {"value": "P@ssw0rd!"},
    "dnsNamePrefix": {"value": "mypublicdns"},
    "environment": {"value": "AzureCloud"},
    "numDataDisks": {"value": "4"},
    "sizeOfDataDiskInGB": {"value": 20},
    "centOsVersion": {"value": "7.0"},
    "routerNodeVmSize": {"value": "Standard_DS3_v2"},
    "configNodeVmSize": {"value": "Standard_DS3_v2"},
    "replicaNodeVmSize": {"value": "Standard_DS3_v2"},
    "zabbixServerIPAddress": {"value": "Null"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json \
  --name myMongoDBCluster \
  --no-wait
```

<span data-ttu-id="b4660-157">이 배포는 모든 VM 인스턴스를 배포하고 구성하는 데 1시간 이상이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-157">This deployment can take over an hour to deploy and configure all the VM instances.</span></span> <span data-ttu-id="b4660-158">템플릿 배포가 Azure 플랫폼에서 수락되면 명령 프롬프트로 제어를 반환하는 이전 명령의 끝에 `--no-wait` 플래그가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-158">The `--no-wait` flag is used at the end of the preceding command to return control to the command prompt once the template deployment has been accepted by the Azure platform.</span></span> <span data-ttu-id="b4660-159">그런 다음 [az group deployment show](/cli/azure/group/deployment#show)를 사용하여 배포 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-159">You can then view the deployment status with [az group deployment show](/cli/azure/group/deployment#show).</span></span> <span data-ttu-id="b4660-160">다음 예제에서는 *myResourceGroup* 리소스 그룹에서 *myMongoDBCluster* 배포에 대한 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-160">The following example views the status for the *myMongoDBCluster* deployment in the *myResourceGroup* resource group:</span></span>

```azurecli
az group deployment show \
    --resource-group myResourceGroup \
    --name myMongoDBCluster \
    --query [properties.provisioningState] \
    --output tsv
```

## <a name="next-steps"></a><span data-ttu-id="b4660-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b4660-161">Next steps</span></span>
<span data-ttu-id="b4660-162">이 예는 VM을 통해 로컬에서 MongoDB 인스턴스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-162">In these examples, you connect to the MongoDB instance locally from the VM.</span></span> <span data-ttu-id="b4660-163">다른 VM 또는 네트워크에서 MongoDB 인스턴스에 연결하려면 적절한 [네트워크 보안 그룹 규칙이 생성되어있어야](nsg-quickstart.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-163">If you want to connect to the MongoDB instance from another VM or network, ensure the appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="b4660-164">이러한 예제는 개발용으로 코어 MongoDB 환경을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-164">These examples deploy the core MongoDB environment for development purposes.</span></span> <span data-ttu-id="b4660-165">사용자 환경에 필요한 보안 구성 옵션을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-165">Apply the required security configuration options for your environment.</span></span> <span data-ttu-id="b4660-166">자세한 내용은 [MongoDB 보안 문서](https://docs.mongodb.com/manual/security/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4660-166">For more information, see the [MongoDB security docs](https://docs.mongodb.com/manual/security/).</span></span>

<span data-ttu-id="b4660-167">템플릿을 사용하여 만드는 방법에 대한 자세한 내용은 [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4660-167">For more information about creating using templates, see the [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="b4660-168">Azure Resource Manager 템플릿은 사용자 지정 스크립트 확장을 사용하여 VM에 스크립트를 다운로드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b4660-168">The Azure Resource Manager templates use the Custom Script Extension to download and execute scripts on your VMs.</span></span> <span data-ttu-id="b4660-169">자세한 내용은 [Linux 가상 컴퓨터에서 Azure 사용자 지정 스크립트 확장 사용](extensions-customscript.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4660-169">For more information, see [Using the Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

