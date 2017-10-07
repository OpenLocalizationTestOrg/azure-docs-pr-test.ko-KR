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
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm-using-hello-azure-cli-10"></a>어떻게 tooinstall hello Azure CLI 1.0을 사용 하 여 Linux VM의 MongoDB 구성
[MongoDB](http://www.mongodb.org)는 인기 있는 오픈 소스 고성능 NoSQL 데이터베이스입니다. 이 문서에서는 어떻게 tooinstall hello 리소스 관리자 배포 모델을 사용 하 여 Azure에서 Linux VM의 MongoDB를 구성 합니다. 표시된 예제는 다음과 같은 방법을 자세히 보여줍니다.

* [기본 MongoDB 인스턴스를 수동으로 설치 및 구성](#manually-install-and-configure-mongodb-on-a-vm)
* [Resource Manager 템플릿을 사용하여 기본 MongoDB 클러스터 만들기](#create-basic-mongodb-instance-on-centos-using-a-template)
* [Resource Manager 템플릿을 사용하여 복제본 세트로 복합적인 MongoDB 분할된 클러스터 만들기](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="cli-versions-toocomplete-hello-task"></a>CLI 버전 toocomplete hello 작업
Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.

- Azure CLI 1.0 – 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)
- [Azure CLI 2.0](create-cli-complete-nodejs.md) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a>VM에서 MongoDB 수동 설치 및 구성
MongoDB는 Red Hat/CentOS, SUSE, Ubuntu 및 Debian을 포함하는 Linux 배포판에 대한 [설치 지침을 제공](https://docs.mongodb.com/manual/administration/install-on-linux/)합니다. hello 다음 예제에서는 한 *CentOS* 에 저장 된 SSH 키를 사용 하 여 VM *~/.ssh/id_rsa.pub*합니다. 저장소 계정 이름, DNS 이름 및 관리자 자격 증명에 대 한 응답 hello 메시지가 나타납니다.

```azurecli
azure vm quick-create \
    --image-urn CentOS \
    --ssh-publickey-file ~/.ssh/id_rsa.pub 
```

VM toohello 로그온 hello hello VM 생성 단계 앞의 hello 끝에 표시 되는 공용 IP 주소를 사용 하 여:

```bash
ssh azureuser@40.78.23.145
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
Azure 빠른 시작 템플릿 GitHub에서 다음 hello를 사용 하 여 단일 CentOS VM의 기본 MongoDB 인스턴스를 만들 수 있습니다. 이 템플릿은 hello 사용자 지정 스크립트 확장을 사용 하 여 Linux tooadd에 대 한는 `yum` 리포지토리 tooyour CentOS VM을 새로 작성 한 다음 MongoDB를 설치 합니다.

* [CentOS의 기본 MongoDB 인스턴스](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json

hello 다음 예제에서는 리소스 그룹 이름을 가진 만듭니다 hello `myResourceGroup` hello에 `eastus` 영역입니다. 다음과 같이 사용자 고유의 값을 입력합니다.

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

> [!NOTE]
> hello Azure CLI를 반환 하면 tooa 프롬프트 hello 배포 되었지만 hello 설치를 만드는 몇 초 안에 하며 구성 몇 분 toocomplete 합니다. Hello 배포 상태를 확인할 hello와 `azure group deployment show myResourceGroup`, 그에 따라 리소스 그룹의 hello 이름을 입력 합니다. Hello 될 때까지 기다렸다가 **ProvisioningState** 표시 *Succeeded* 동안 tooSSH toohello VM 하기 전에.

Hello 배포 되 면 완료, SSH toohello VM입니다. Hello를 사용 하 여 VM의 IP 주소 hello `azure vm show` hello 다음 예제와 같이 명령:

```azurecli
azure vm show --resource-group myResourceGroup --name myLinuxVM
```

Hello 출력의 hello 끝 hello 공용 IP 주소가 표시 됩니다. VM의 IP 주소 hello와 SSH tooyour VM:

```bash
ssh azureuser@138.91.149.74
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

hello 다음 예제에서는 리소스 그룹 이름을 가진 만듭니다 hello *myResourceGroup* hello에 *eastus* 영역입니다. 다음과 같이 사용자 고유의 값을 입력합니다.

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json
```

> [!NOTE]
> hello Azure CLI 반환 하면 tooa 프롬프트 hello 배포를 만드는 몇 초 안에 하지만 hello 설치 및 구성을 계속 유지할 수 시간 toocomplete 합니다. Hello 배포 상태를 확인할 hello와 `azure group deployment show myResourceGroup`, 리소스 그룹의 hello 이름을 적절 하 게 조정 합니다. Hello 될 때까지 기다렸다가 **ProvisioningState** 표시 *Succeeded* toohello Vm에 연결 하기 전에.


## <a name="next-steps"></a>다음 단계
이 예제에서는 연결 toohello MongoDB 인스턴스에 로컬로 hello VM에서. 다른 VM 네트워크에서 tooconnect toohello MongoDB 인스턴스를 원하는 경우 적절 한 hello 확인 [네트워크 보안 그룹 규칙을 만드는](nsg-quickstart.md)합니다.

템플릿을 사용 하 여 만들기에 대 한 자세한 내용은 참조 hello [Azure 리소스 관리자 개요](../../azure-resource-manager/resource-group-overview.md)합니다.

hello Azure 리소스 관리자 템플릿을 사용자 지정 스크립트 확장 toodownload hello를 사용 하 고 Vm에서 스크립트를 실행 합니다. 자세한 내용은 참조 [Azure 사용자 지정 스크립트 확장 Linux 가상 컴퓨터와 함께 사용 하 여 hello](extensions-customscript.md)합니다.

