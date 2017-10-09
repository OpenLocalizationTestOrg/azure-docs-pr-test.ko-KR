---
title: "hello Azure CLI를 사용 하 여 Linux VM에 MongoDB aaaInstall | Microsoft Docs"
description: "자세한 내용은 방법 tooinstall MongoDB Linux 가상 컴퓨터 iusing hello Azure CLI 2.0에서 구성 하 고"
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
ms.openlocfilehash: 97a4d9913f0eeaf7b8bf15d7fc81befe538cdc8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm"></a>어떻게 tooinstall 고 Linux VM의 MongoDB 구성
[MongoDB](http://www.mongodb.org)는 인기 있는 오픈 소스 고성능 NoSQL 데이터베이스입니다. 이 문서에서는 어떻게 tooinstall 및 MongoDB hello Azure CLI 2.0을 사용 하 여 Linux VM에서 구성 합니다. Hello로 다음이 단계를 수행할 수도 있습니다 [Azure CLI 1.0](install-mongodb-nodejs.md)합니다. 표시된 예제는 다음과 같은 방법을 자세히 보여줍니다.

* [기본 MongoDB 인스턴스를 수동으로 설치 및 구성](#manually-install-and-configure-mongodb-on-a-vm)
* [Resource Manager 템플릿을 사용하여 기본 MongoDB 클러스터 만들기](#create-basic-mongodb-instance-on-centos-using-a-template)
* [Resource Manager 템플릿을 사용하여 복제본 세트로 복합적인 MongoDB 분할된 클러스터 만들기](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a>VM에서 MongoDB 수동 설치 및 구성
MongoDB는 Red Hat/CentOS, SUSE, Ubuntu 및 Debian을 포함하는 Linux 배포판에 대한 [설치 지침을 제공](https://docs.mongodb.com/manual/administration/install-on-linux/)합니다. hello 다음 예제에서는 한 *CentOS* VM입니다. toocreate이이 환경에서는 최신 hello 필요한 [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치 하 고 tooan Azure 계정을 사용 하 여 로그인 [az 로그인](/cli/azure/#login)합니다.

[az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다. hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *eastus* 위치:

```azurecli
az group create --name myResourceGroup --location eastus
```

[az vm create](/cli/azure/vm#create)로 VM을 만듭니다. hello 다음 예제에서는 V *myVM* 명명 된 사용자와 *azureuser* SSH 공개 키 인증을 사용 하 여

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH toohello 자신의 사용자 이름 및 hello를 사용 하 여 VM `publicIpAddress` hello 이전 단계의 출력 hello에에서 나열 된:

```bash
ssh azureuser@<publicIpAddress>
```

tooadd hello 설치 원본, MongoDB에 대 한 만들기는 **yum** 다음과 같이 저장소 파일:

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

편집을 위해 hello MongoDB 리포지토리 파일을 엽니다. Hello 다음 줄을 추가 합니다.

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

다음과 같이 **yum**을 사용하여 MongoDB를 설치합니다.

```bash
sudo yum install -y mongodb-org
```

기본적으로 MongoDB 액세스를 막는 CentOS 이미지에 SELinux가 강제 적용됩니다. 정책 관리 도구에서 설치 및 구성 SELinux tooallow MongoDB toooperate 기본 TCP 포트 27017 다음과 같습니다.

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

다음과 같이 hello MongoDB 서비스를 시작 합니다.

```bash
sudo service mongod start
```

로컬 hello를 사용 하 여 연결 하 여 hello MongoDB 설치 확인 `mongo` 클라이언트:

```bash
mongo
```

이제 일부 데이터를 추가 하 고 다음 검색 하 여 hello MongoDB 인스턴스를 테스트할:

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

원하는 경우 MongoDB toostart 자동으로 구성 하는 동안 시스템 다시 부팅:

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a>템플릿을 사용하여 CentOS에서 기본 MongoDB 인스턴스 만들기
Azure 빠른 시작 템플릿 GitHub에서 다음 hello를 사용 하 여 단일 CentOS VM의 기본 MongoDB 인스턴스를 만들 수 있습니다. 이 템플릿은 hello 사용자 지정 스크립트 확장을 사용 하 여 Linux tooadd에 대 한 한 **yum** 리포지토리 tooyour CentOS VM을 새로 작성 한 다음 MongoDB를 설치 합니다.

* [CentOS의 기본 MongoDB 인스턴스](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json

toocreate이이 환경에서는 최신 hello 필요한 [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치 하 고 tooan Azure 계정을 사용 하 여 로그인 [az 로그인](/cli/azure/#login)합니다. 먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다. hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *eastus* 위치:

```azurecli
az group create --name myResourceGroup --location eastus
```

다음에 배포 된 hello MongoDB 템플릿을 [az 그룹 배포 만들기](/cli/azure/group/deployment#create)합니다. *newStorageAccountName*, *virtualNetworkName* 및 *vmSize* 등에 필요한 대로, 고유한 리소스 이름 및 크기를 정의합니다.

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

Toohello VM에 로그온 하면 VM의 공용 DNS 주소 hello를 사용 하 여 합니다. 사용 하는 공용 DNS 주소 hello를 볼 수 있습니다 [az vm 표시](/cli/azure/vm#show):

```azurecli
az vm show -g myResourceGroup -n myVM -d --query [fqdns] -o tsv
```

SSH tooyour 자신의 사용자 이름 및 공용 DNS 주소를 사용 하 여 VM:

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

로컬 hello를 사용 하 여 연결 하 여 hello MongoDB 설치 확인 `mongo` 다음과 같이 클라이언트:

```bash
mongo
```

이제 일부 데이터를 추가 하 고 다음과 같이 검색 하 여 hello 인스턴스를 테스트 합니다.

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a>템플릿을 사용하여 CentOS에서 복합적인 MongoDB 분할된 클러스터 만들기
Azure 빠른 시작 템플릿 GitHub에서 다음 hello를 사용 하 여 복잡 한 MongoDB 분할 클러스터를 만들 수 있습니다. 이 템플릿은 다음과 hello [MongoDB 분할 클러스터에 대 한 유용한 정보](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide 중복성 및 고가용성 합니다. hello 템플릿은 각 복제 세트의 3 개의 노드와 두 개의 분할 영역을 만듭니다. 세 개의 노드를 사용 하 여 설정 하는 하나의 구성 서버 복제본도 만들어지면 2를 더한 **mongos** 라우터 서버 tooprovide 일관성 tooapplications에서 hello 분할 영역에 걸쳐 있습니다.

* [CentOS의 MongoDB 분할 클러스터](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json

> [!WARNING]
> 이 복잡 한 MongoDB 분할 클러스터 배포에 일반적으로 hello 기본 코어 수 구독에 대 한 지역 마다 이것이 20 개 이상의 코어가 필요 합니다. Azure 지원 요청 tooincrease 코어 수를 엽니다.

toocreate이이 환경에서는 최신 hello 필요한 [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치 하 고 tooan Azure 계정을 사용 하 여 로그인 [az 로그인](/cli/azure/#login)합니다. 먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다. hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *eastus* 위치:

```azurecli
az group create --name myResourceGroup --location eastus
```

다음에 배포 된 hello MongoDB 템플릿을 [az 그룹 배포 만들기](/cli/azure/group/deployment#create)합니다. *mongoAdminUsername*, *sizeOfDataDiskInGB* 및 *configNodeVmSize* 등에 필요한 대로, 고유한 리소스 이름 및 크기를 정의합니다.

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

이 배포 시간 toodeploy을 모든 hello VM 인스턴스를 구성 합니다. hello `--no-wait` hello 끝 hello hello 템플릿 배포 hello Azure 플랫폼에서 수락 되 면 명령 tooreturn 제어 toohello 명령 프롬프트를 앞에 플래그를 사용 합니다. Hello 배포 상태를 볼 수 있습니다 [az 그룹 배포 쇼](/cli/azure/group/deployment#show)합니다. hello 다음 예에서는 뷰 hello hello에 대 한 상태 *myMongoDBCluster* hello에 대 한 배포 *myResourceGroup* 리소스 그룹:

```azurecli
az group deployment show \
    --resource-group myResourceGroup \
    --name myMongoDBCluster \
    --query [properties.provisioningState] \
    --output tsv
```

## <a name="next-steps"></a>다음 단계
이 예제에서는 연결 toohello MongoDB 인스턴스에 로컬로 hello VM에서. 다른 VM 네트워크에서 tooconnect toohello MongoDB 인스턴스를 원하는 경우 적절 한 hello 확인 [네트워크 보안 그룹 규칙을 만드는](nsg-quickstart.md)합니다.

개발을 위해 hello 코어 MongoDB 환경을 배포 하는 이러한 예제. 사용자 환경에 필요한 hello 보안 구성 옵션을 적용 합니다. 자세한 내용은 참조 hello [MongoDB 보안 docs](https://docs.mongodb.com/manual/security/)합니다.

템플릿을 사용 하 여 만들기에 대 한 자세한 내용은 참조 hello [Azure 리소스 관리자 개요](../../azure-resource-manager/resource-group-overview.md)합니다.

hello Azure 리소스 관리자 템플릿을 사용자 지정 스크립트 확장 toodownload hello를 사용 하 고 Vm에서 스크립트를 실행 합니다. 자세한 내용은 참조 [Azure 사용자 지정 스크립트 확장 Linux 가상 컴퓨터와 함께 사용 하 여 hello](extensions-customscript.md)합니다.

