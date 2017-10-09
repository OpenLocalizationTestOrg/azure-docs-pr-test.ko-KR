---
title: "aaaDeploy OpenShift 원점 tooAzure | Microsoft Docs"
description: "Toodeploy OpenShift 원점 tooAzure 가상 컴퓨터에 알아봅니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jbinder
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 
ms.author: jbinder
ms.openlocfilehash: a67450c46da41134a5f6c669a9e54e14773ac5b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-openshift-origin-tooazure-virtual-machines"></a>OpenShift 원점 tooAzure 가상 컴퓨터 배포 

[OpenShift Origin](https://www.openshift.org/)은 [Kubernetes](https://kubernetes.io/)를 기반으로 하는 오픈 소스 컨테이너 플랫폼입니다. Hello 프로세스 배포를 확장 하 고 다중 테 넌 트 응용 프로그램을 운영을 간소화 합니다. 

이 가이드에서는 Azure CLI 및 Azure 리소스 관리자 템플릿을 사용 하 여 Azure 가상 컴퓨터에서 OpenShift 원점 toodeploy hello 하는 방법을 설명 합니다. 이 자습서에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * KeyVault toomanage hello OpenShift 클러스터에 대 한 SSH 키를 만듭니다.
> * Azure VM에 OpenShift 클러스터를 배포합니다. 
> * 설치 및 구성 hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello 클러스터입니다.
> * Hello OpenShift 배포를 사용자 지정 합니다.

Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.

이 빠른 시작 hello Azure CLI 버전 2.0.8 필요 이상. toofind hello 버전을 실행 `az --version`합니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="log-in-tooazure"></a>TooAzure 로그인 
Tooyour hello로 Azure 구독에에서 로그인 [az 로그인](/cli/azure/#login) 명령 및 지시를 따른 hello 화면에 표시 하거나 클릭 **실습** toouse 클라우드 셸 합니다.

```azurecli 
az login
```
## <a name="create-a-resource-group"></a>리소스 그룹 만들기

Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다. Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다. 

hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *eastus* 위치 합니다.

```azurecli 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-key-vault"></a>주요 자격 증명 모음 만들기
Hello로 KeyVault toostore hello hello 클러스터에 대 한 SSH 키를 만들기 [az keyvault 만들](/cli/azure/keyvault#create) 명령입니다.  

```azurecli 
az keyvault create --resource-group myResourceGroup --name myKeyVault \
       --enabled-for-template-deployment true \
       --location eastus
```

## <a name="create-an-ssh-key"></a>SSH 키 만들기 
SSH 키에는 필요한 toosecure 액세스 toohello OpenShift 원본 클러스터입니다. SSH 키 쌍 만들기 hello를 사용 하 여 `ssh-keygen` 명령입니다. 
 
 ```bash
ssh-keygen -f ~/.ssh/openshift_rsa -t rsa -N ''
```

> [!NOTE]
> SSH 키 쌍 만들면 hello에 암호를 사용할 수 없습니다.

Windows에서는 SSH 키에 대 한 자세한 내용은 [Windows에서 toocreate SSH 키는 어떻게](/azure/virtual-machines/linux/ssh-from-windows)합니다.

## <a name="store-ssh-private-key-in-key-vault"></a>Key Vault에 SSH 개인 키 저장
hello OpenShift 배포 toosecure 액세스 toohello OpenShift 마스터 만든 hello SSH 키를 사용 합니다. tooenable hello 배포 toosecurely hello SSH 키를 검색, 키 자격 증명 모음의 hello 다음 명령을 사용 하 여 hello 키를 저장 합니다.

# <a name="enabled-for-template-deployment"></a>템플릿 배포를 위한 사용
```azurecli
az keyvault secret set --vault-name KeyVaultName --name OpenShiftKey --file ~/.ssh/openshift.rsa
```

## <a name="create-a-service-principal"></a>서비스 주체 만들기 
OpenShift는 사용자 이름 및 암호 또는 서비스 주체를 사용하여 Azure와 통신합니다. Azure 서비스 주체는 앱, 서비스 및 OpenShift와 같은 자동화 도구를 사용할 수 있는 보안 ID입니다. 제어 하 고이 정보를 toowhat 작업 hello 서비스 사용자는 Azure에서 수행할 수 있는 대로 hello 사용 권한을 정의 합니다. 제공 하는 것 사용자 이름 및 암호를 통해 tooimprove 보안,이 예제에서는 기본 서비스 보안 주체

서비스와 사용자 만들기 [az ad sp 만들기에 대 한-rbac](/cli/azure/ad/sp#create-for-rbac) OpenShift 해야 하는 출력 hello 자격 증명:

```azurecli
az ad sp create-for-rbac --name openshiftsp \
          --role Contributor --password {strong password} \
          --scopes $(az group show --name myResourceGroup --query id)
```
Hello 명령에서 반환 된 hello appId 속성을 기록해 둡니다.
```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "openshiftsp",
  "name": "http://openshiftsp",
  "password": {strong password},
  "tenant": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
}
```
 > [!WARNING] 
 > 안전하지 않은 암호를 만들지 마세요.  [Azure AD 암호 규칙 및 제한 사항](/azure/active-directory/active-directory-passwords-policy) 지침을 따르세요.

서비스 주체에 대한 자세한 내용은 [Azure CLI 2.0을 사용하여 Azure 서비스 주체 만들기](/cli/azure/create-an-azure-service-principal-azure-cli)를 참조하세요.

## <a name="deploy-hello-openshift-origin-template"></a>Hello OpenShift 원본 템플릿 배포
다음으로 Azure Resource Manager 템플릿을 사용하여 OpenShift Origin을 배포합니다. 

> [!NOTE] 
> hello 다음 명령을 사용 하려면 CLI 2.0.8 az 이상. 확인할 수 있습니다 az CLI hello hello로 버전 `az --version` 명령입니다. tooupdate hello CLI 버전 참조 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.

사용 하 여 hello `appId` hello에 대 한 이전에 만든 hello 서비스 보안 주체에서 값 `aadClientId` 매개 변수입니다.

```azurecli 
az group deployment create --name myOpenShiftCluster \
      --template-uri https://raw.githubusercontent.com/Microsoft/openshift-origin/master/azuredeploy.json \
      --params \ 
        openshiftMasterPublicIpDnsLabel=myopenshiftmaster \
        infraLbPublicIpDnsLabel=myopenshiftlb \
        openshiftPassword=Pass@word!
        sshPublicKey=~/.ssh/openshift_rsa.pub \
        keyVaultResourceGroup=myResourceGroup \
        keyVaultName=myKeyVault \
        keyVaultSecret=OpenShiftKey \
        aadClientId={appId} \
        aadClientSecret={strong password} 
```
hello 배포 too20 분 toocomplete를 차지할 수 있습니다. hello hello OpenShift 콘솔의 URL 및 hello의 DNS 이름을 OpenShift 마스터는 인쇄 toohello 터미널 hello 배포가 완료 되는 경우.

```json
{
  "OpenShift Console Uri": "http://openshiftlb.cloudapp.azure.com:8443/console",
  "OpenShift Master SSH": "ocpadmin@myopenshiftmaster.cloudapp.azure.com"
}
```
## <a name="connect-toohello-openshift-cluster"></a>Toohello OpenShift 클러스터에 연결
Hello 배포가 완료 되 면 hello를 사용 하 여 hello 브라우저를 사용 하 여 toohello OpenShift 콘솔 연결 `OpenShift Console Uri`합니다. 또는 다음 명령을 hello를 사용 하 여 toohello OpenShift 마스터를 연결할 수 있습니다.

```bash
$ ssh ocpadmin@myopenshiftmaster.cloudapp.azure.com
```

## <a name="clean-up-resources"></a>리소스 정리
더 이상 필요 hello를 사용할 수 없습니다 [az 그룹 삭제](/cli/azure/group#delete) tooremove hello 리소스 그룹, OpenShift 클러스터 및 관련 된 모든 리소스를 명령입니다.

```azurecli 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>다음 단계

이 자습서에서 학습한 방법은 다음과 같습니다.
> [!div class="checklist"]
> * KeyVault toomanage hello OpenShift 클러스터에 대 한 SSH 키를 만듭니다.
> * Azure VM에 OpenShift 클러스터를 배포합니다. 
> * 설치 및 구성 hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello 클러스터입니다.

이제 해당 OpenShift Origin 클러스터가 배포되었습니다. OpenShift 자습서 toolearn 방법을 따를 수 있습니다 toodeploy 첫 번째 응용 프로그램 및 사용 하 여 hello OpenShift 도구입니다. 참조 [OpenShift Origin 시작](https://docs.openshift.org/latest/getting_started/index.html) tooget 시작 합니다. 
