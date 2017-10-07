---
title: "사용 하 여 Linux VM의 MongoDB aaaInstall hello Azure CLI 1.0 | Microsoft Docs"
description: "자세한 방법을 tooinstall 및 MongoDB hello 리소스 관리자 배포 모델을 사용 하 여 Azure에서 Linux 가상 컴퓨터에서 구성 합니다."
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
ms.openlocfilehash: 4ce21a2c63da7d00a4422e0a6766e2103e7f12d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm-using-hello-azure-cli-10"></a><span data-ttu-id="673bd-103">어떻게 tooinstall hello Azure CLI 1.0을 사용 하 여 Linux VM의 MongoDB 구성</span><span class="sxs-lookup"><span data-stu-id="673bd-103">How tooinstall and configure MongoDB on a Linux VM using hello Azure CLI 1.0</span></span>
<span data-ttu-id="673bd-104">[MongoDB](http://www.mongodb.org)는 인기 있는 오픈 소스 고성능 NoSQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="673bd-105">이 문서에서는 어떻게 tooinstall hello 리소스 관리자 배포 모델을 사용 하 여 Azure에서 Linux VM의 MongoDB를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-105">This article shows you how tooinstall and configure MongoDB on a Linux VM in Azure using hello Resource Manager deployment model.</span></span> <span data-ttu-id="673bd-106">표시된 예제는 다음과 같은 방법을 자세히 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-106">Examples are shown that detail how to:</span></span>

* [<span data-ttu-id="673bd-107">기본 MongoDB 인스턴스를 수동으로 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="673bd-107">Manually install and configure a basic MongoDB instance</span></span>](#manually-install-and-configure-mongodb-on-a-vm)
* [<span data-ttu-id="673bd-108">Resource Manager 템플릿을 사용하여 기본 MongoDB 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="673bd-108">Create a basic MongoDB instance using a Resource Manager template</span></span>](#create-basic-mongodb-instance-on-centos-using-a-template)
* [<span data-ttu-id="673bd-109">Resource Manager 템플릿을 사용하여 복제본 세트로 복합적인 MongoDB 분할된 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="673bd-109">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span></span>](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="673bd-110">CLI 버전 toocomplete hello 작업</span><span class="sxs-lookup"><span data-stu-id="673bd-110">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="673bd-111">Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-111">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="673bd-112">Azure CLI 1.0 – 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)</span><span class="sxs-lookup"><span data-stu-id="673bd-112">Azure CLI 1.0 – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="673bd-113">[Azure CLI 2.0](create-cli-complete-nodejs.md) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한</span><span class="sxs-lookup"><span data-stu-id="673bd-113">[Azure CLI 2.0](create-cli-complete-nodejs.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="673bd-114">VM에서 MongoDB 수동 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="673bd-114">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="673bd-115">MongoDB는 Red Hat/CentOS, SUSE, Ubuntu 및 Debian을 포함하는 Linux 배포판에 대한 [설치 지침을 제공](https://docs.mongodb.com/manual/administration/install-on-linux/)합니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-115">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="673bd-116">hello 다음 예제에서는 한 *CentOS* 에 저장 된 SSH 키를 사용 하 여 VM *~/.ssh/id_rsa.pub*합니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-116">hello following example creates a *CentOS* VM using an SSH key stored at *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="673bd-117">저장소 계정 이름, DNS 이름 및 관리자 자격 증명에 대 한 응답 hello 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-117">Answer hello prompts for storage account name, DNS name, and admin credentials:</span></span>

```azurecli
azure vm quick-create \
    --image-urn CentOS \
    --ssh-publickey-file ~/.ssh/id_rsa.pub 
```

<span data-ttu-id="673bd-118">VM toohello 로그온 hello hello VM 생성 단계 앞의 hello 끝에 표시 되는 공용 IP 주소를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="673bd-118">Log on toohello VM using hello public IP address displayed at hello end of hello preceding VM creation step:</span></span>

```bash
ssh azureuser@40.78.23.145
```

<span data-ttu-id="673bd-119">tooadd hello 설치 원본, MongoDB에 대 한 만들기는 **yum** 다음과 같이 저장소 파일:</span><span class="sxs-lookup"><span data-stu-id="673bd-119">tooadd hello installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="673bd-120">편집을 위해 hello MongoDB 리포지토리 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-120">Open hello MongoDB repo file for editing.</span></span> <span data-ttu-id="673bd-121">Hello 다음 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-121">Add hello following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="673bd-122">다음과 같이 **yum**을 사용하여 MongoDB를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-122">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="673bd-123">기본적으로 MongoDB 액세스를 막는 CentOS 이미지에 SELinux가 강제 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-123">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="673bd-124">정책 관리 도구에서 설치 및 구성 SELinux tooallow MongoDB toooperate 기본 TCP 포트 27017 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-124">Install policy management tools and configure SELinux tooallow MongoDB toooperate on its default TCP port 27017 as follows.</span></span> 

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="673bd-125">다음과 같이 hello MongoDB 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-125">Start hello MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="673bd-126">로컬 hello를 사용 하 여 연결 하 여 hello MongoDB 설치 확인 `mongo` 클라이언트:</span><span class="sxs-lookup"><span data-stu-id="673bd-126">Verify hello MongoDB installation by connecting using hello local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="673bd-127">이제 일부 데이터를 추가 하 고 다음 검색 하 여 hello MongoDB 인스턴스를 테스트할:</span><span class="sxs-lookup"><span data-stu-id="673bd-127">Now test hello MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="673bd-128">원하는 경우 MongoDB toostart 자동으로 구성 하는 동안 시스템 다시 부팅:</span><span class="sxs-lookup"><span data-stu-id="673bd-128">If desired, configure MongoDB toostart automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="673bd-129">템플릿을 사용하여 CentOS에서 기본 MongoDB 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="673bd-129">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="673bd-130">Azure 빠른 시작 템플릿 GitHub에서 다음 hello를 사용 하 여 단일 CentOS VM의 기본 MongoDB 인스턴스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-130">You can create a basic MongoDB instance on a single CentOS VM using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="673bd-131">이 템플릿은 hello 사용자 지정 스크립트 확장을 사용 하 여 Linux tooadd에 대 한는 `yum` 리포지토리 tooyour CentOS VM을 새로 작성 한 다음 MongoDB를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-131">This template uses hello Custom Script extension for Linux tooadd a `yum` repository tooyour newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="673bd-132">[CentOS의 기본 MongoDB 인스턴스](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="673bd-132">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="673bd-133">hello 다음 예제에서는 리소스 그룹 이름을 가진 만듭니다 hello `myResourceGroup` hello에 `eastus` 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-133">hello following example creates a resource group with hello name `myResourceGroup` in hello `eastus` region.</span></span> <span data-ttu-id="673bd-134">다음과 같이 사용자 고유의 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-134">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="673bd-135">hello Azure CLI를 반환 하면 tooa 프롬프트 hello 배포 되었지만 hello 설치를 만드는 몇 초 안에 하며 구성 몇 분 toocomplete 합니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-135">hello Azure CLI returns you tooa prompt within a few seconds of creating hello deployment, but hello installation and configuration takes a few minutes toocomplete.</span></span> <span data-ttu-id="673bd-136">Hello 배포 상태를 확인할 hello와 `azure group deployment show myResourceGroup`, 그에 따라 리소스 그룹의 hello 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-136">Check hello status of hello deployment with `azure group deployment show myResourceGroup`, entering hello name of your resource group accordingly.</span></span> <span data-ttu-id="673bd-137">Hello 될 때까지 기다렸다가 **ProvisioningState** 표시 *Succeeded* 동안 tooSSH toohello VM 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="673bd-137">Wait until hello **ProvisioningState** shows *Succeeded* before trying tooSSH toohello VM.</span></span>

<span data-ttu-id="673bd-138">Hello 배포 되 면 완료, SSH toohello VM입니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-138">Once hello deployment is complete, SSH toohello VM.</span></span> <span data-ttu-id="673bd-139">Hello를 사용 하 여 VM의 IP 주소 hello `azure vm show` hello 다음 예제와 같이 명령:</span><span class="sxs-lookup"><span data-stu-id="673bd-139">Obtain hello IP address of your VM using hello `azure vm show` command as in hello following example:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myLinuxVM
```

<span data-ttu-id="673bd-140">Hello 출력의 hello 끝 hello 공용 IP 주소가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-140">Near hello end of hello output, hello public IP address is displayed.</span></span> <span data-ttu-id="673bd-141">VM의 IP 주소 hello와 SSH tooyour VM:</span><span class="sxs-lookup"><span data-stu-id="673bd-141">SSH tooyour VM with hello IP address of your VM:</span></span>

```bash
ssh azureuser@138.91.149.74
```

<span data-ttu-id="673bd-142">로컬 hello를 사용 하 여 연결 하 여 hello MongoDB 설치 확인 `mongo` 다음과 같이 클라이언트:</span><span class="sxs-lookup"><span data-stu-id="673bd-142">Verify hello MongoDB installation by connecting using hello local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="673bd-143">이제 일부 데이터를 추가 하 고 다음과 같이 검색 하 여 hello 인스턴스를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-143">Now test hello instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="673bd-144">템플릿을 사용하여 CentOS에서 복합적인 MongoDB 분할된 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="673bd-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="673bd-145">Azure 빠른 시작 템플릿 GitHub에서 다음 hello를 사용 하 여 복잡 한 MongoDB 분할 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-145">You can create a complex MongoDB sharded cluster using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="673bd-146">이 템플릿은 다음과 hello [MongoDB 분할 클러스터에 대 한 유용한 정보](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide 중복성 및 고가용성 합니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-146">This template follows hello [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redundancy and high availability.</span></span> <span data-ttu-id="673bd-147">hello 템플릿은 각 복제 세트의 3 개의 노드와 두 개의 분할 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-147">hello template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="673bd-148">세 개의 노드를 사용 하 여 설정 하는 하나의 구성 서버 복제본도 만들어지면 2를 더한 **mongos** 라우터 서버 tooprovide 일관성 tooapplications에서 hello 분할 영역에 걸쳐 있습니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-148">One config server replica set with three nodes is also created, plus two **mongos** router servers tooprovide consistency tooapplications from across hello shards.</span></span>

* <span data-ttu-id="673bd-149">[CentOS의 MongoDB 분할 클러스터](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="673bd-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="673bd-150">이 복잡 한 MongoDB 분할 클러스터 배포에 일반적으로 hello 기본 코어 수 구독에 대 한 지역 마다 이것이 20 개 이상의 코어가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically hello default core count per region for a subscription.</span></span> <span data-ttu-id="673bd-151">Azure 지원 요청 tooincrease 코어 수를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-151">Open an Azure support request tooincrease your core count.</span></span>

<span data-ttu-id="673bd-152">hello 다음 예제에서는 리소스 그룹 이름을 가진 만듭니다 hello *myResourceGroup* hello에 *eastus* 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-152">hello following example creates a resource group with hello name *myResourceGroup* in hello *eastus* region.</span></span> <span data-ttu-id="673bd-153">다음과 같이 사용자 고유의 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-153">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="673bd-154">hello Azure CLI 반환 하면 tooa 프롬프트 hello 배포를 만드는 몇 초 안에 하지만 hello 설치 및 구성을 계속 유지할 수 시간 toocomplete 합니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-154">hello Azure CLI returns you tooa prompt within a few seconds of creating hello deployment, but hello installation and configuration can take over an hour toocomplete.</span></span> <span data-ttu-id="673bd-155">Hello 배포 상태를 확인할 hello와 `azure group deployment show myResourceGroup`, 리소스 그룹의 hello 이름을 적절 하 게 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-155">Check hello status of hello deployment with `azure group deployment show myResourceGroup`, adjusting hello name of your resource group accordingly.</span></span> <span data-ttu-id="673bd-156">Hello 될 때까지 기다렸다가 **ProvisioningState** 표시 *Succeeded* toohello Vm에 연결 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="673bd-156">Wait until hello **ProvisioningState** shows *Succeeded* before connecting toohello VMs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="673bd-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="673bd-157">Next steps</span></span>
<span data-ttu-id="673bd-158">이 예제에서는 연결 toohello MongoDB 인스턴스에 로컬로 hello VM에서.</span><span class="sxs-lookup"><span data-stu-id="673bd-158">In these examples, you connect toohello MongoDB instance locally from hello VM.</span></span> <span data-ttu-id="673bd-159">다른 VM 네트워크에서 tooconnect toohello MongoDB 인스턴스를 원하는 경우 적절 한 hello 확인 [네트워크 보안 그룹 규칙을 만드는](nsg-quickstart.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-159">If you want tooconnect toohello MongoDB instance from another VM or network, ensure hello appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="673bd-160">템플릿을 사용 하 여 만들기에 대 한 자세한 내용은 참조 hello [Azure 리소스 관리자 개요](../../azure-resource-manager/resource-group-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-160">For more information about creating using templates, see hello [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="673bd-161">hello Azure 리소스 관리자 템플릿을 사용자 지정 스크립트 확장 toodownload hello를 사용 하 고 Vm에서 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-161">hello Azure Resource Manager templates use hello Custom Script Extension toodownload and execute scripts on your VMs.</span></span> <span data-ttu-id="673bd-162">자세한 내용은 참조 [Azure 사용자 지정 스크립트 확장 Linux 가상 컴퓨터와 함께 사용 하 여 hello](extensions-customscript.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="673bd-162">For more information, see [Using hello Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

