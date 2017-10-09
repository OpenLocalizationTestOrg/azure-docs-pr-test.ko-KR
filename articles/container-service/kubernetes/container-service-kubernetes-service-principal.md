---
title: "Azure Kubernetes 클러스터에 대 한 보안 주체 aaaService | Microsoft Docs"
description: "Azure Container Service에서 Kubernetes 클러스터에 대한 Azure Active Directory 서비스 주체를 만들고 관리합니다."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/08/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 7a01624c5ac3fa717dbcbd570e05ceb4d917c53a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-ad-service-principal-for-a-kubernetes-cluster-in-container-service"></a>Container Service에서 Kubernetes 클러스터에 대한 Azure AD 서비스 주체 설정


Azure 컨테이너 서비스의 Kubernetes 클러스터 필요는 [Azure Active Directory 서비스 사용자](../../active-directory/develop/active-directory-application-objects.md) toointeract Azure는 api입니다. hello 서비스 사용자는 필요 toodynamically와 같은 리소스를 관리할 [사용자 정의 경로](../../virtual-network/virtual-networks-udr-overview.md) 및 hello [계층 4 Azure 부하 분산 장치](../../load-balancer/load-balancer-overview.md)합니다. 


이 문서에서는 서비스를 다양 한 옵션 tooset을 Kubernetes 클러스터에 대 한 주 보여 줍니다. 예를 들어, 설치 하 고 hello를 설정 하는 경우 [Azure CLI 2.0](/cli/azure/install-az-cli2), hello를 실행할 수 있습니다 [ `az acs create` ](/cli/azure/acs#create) 명령 toocreate hello Kubernetes 클러스터와 hello 서비스 hello에서 사용자 같은 시간입니다.


## <a name="requirements-for-hello-service-principal"></a>Hello 서비스 사용자에 대 한 요구 사항

기존 Azure AD 서비스 보안 주체 충족 hello 요구 사항을 준수, 또는 새로 만들를 사용할 수 있습니다.

* **범위**: hello 구독 toodeploy hello 클러스터를 사용 하는 (덜 제한적으로) 또는 hello 구독에서 리소스 그룹 hello toodeploy hello Kubernetes 클러스터를 사용 합니다.

* **역할**: **참여자**

* **클라이언트 암호**: 암호여야 합니다. 현재 인증서 인증을 위해 설정된 서비스 주체는 사용할 수 없습니다.

> [!IMPORTANT] 
> toocreate 서비스 사용자 있어야 권한을 tooregister, Azure AD 테 넌 트 및 tooassign hello 응용 프로그램 tooa 역할 응용 프로그램을 구독에 있습니다. hello 필요한 권한이 있는 경우 toosee [hello 포털 체크인](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions)합니다. 
>

## <a name="option-1-create-a-service-principal-in-azure-ad"></a>옵션 1: Azure AD에서 서비스 주체 만들기

Kubernetes 클러스터를 배포 하기 전에 toocreate Azure AD 서비스 사용자를 원하는 경우 Azure는 여러 가지 방법을 제공 합니다. 

표시 하는 다음 예제 명령은 hello toodo hello로이 [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)합니다. 보안 주체 사용 하는 서비스 또는 만들 수 있습니다 [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), hello [포털](../../azure-resource-manager/resource-group-create-service-principal-portal.md), 또는 기타 방법.

```azurecli
az login

az account set --subscription "mySubscriptionID"

az group create -n "myResourceGroupName" -l "westus"

az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/mySubscriptionID/resourceGroups/myResourceGroupName"
```

출력은 유사한 toohello 다음 (교정 여기 표시).

![서비스 주체 만들기](./media/container-service-kubernetes-service-principal/service-principal-creds.png)

강조 표시 되어 있습니다 hello **클라이언트 ID** (`appId`) 및 hello **클라이언트 암호** (`password`) 클러스터 배포에 대 한 서비스 주체 매개 변수로 사용 하는 합니다.


### <a name="specify-service-principal-when-creating-hello-kubernetes-cluster"></a>Hello Kubernetes 클러스터를 만들 때 서비스 사용자를 지정 합니다.

Hello 제공 **클라이언트 ID** (라고도 함 hello `appId`, 응용 프로그램 ID에 대 한) 및 **클라이언트 암호** (`password`) 기존 서비스 hello를 만들 때 매개 변수로 사용자의 Kubernetes 클러스터입니다. Hello 서비스 사용자 hello 시작 하 고이 문서에서 hello 요구 사항을 충족 하는지 확인 합니다.

Hello를 사용 하 여 hello Kubernetes 클러스터를 배포할 때 이러한 매개 변수를 지정할 수 있습니다 [Azure 명령줄 인터페이스 (CLI) 2.0](container-service-kubernetes-walkthrough.md), [Azure 포털](../dcos-swarm/container-service-deployment.md), 또는 기타 방법.

>[!TIP] 
>Hello를 지정 하는 경우 **클라이언트 ID**, 있는지 toouse hello 수 `appId`, 하지 hello `ObjectId`, hello 서비스 사용자의 합니다.
>

hello 다음 예제에서는 한 가지 방법은 toopass Azure CLI 2.0 hello로 hello 매개 변수 이 예에서는 hello [Kubernetes 퀵 스타트 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)합니다.

1. [다운로드](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) hello 템플릿 매개 변수 파일 `azuredeploy.parameters.json` GitHub에서 합니다.

2. 값을 입력 하는 toospecify hello 서비스 사용자, `servicePrincipalClientId` 및 `servicePrincipalClientSecret` hello 파일에 있습니다. (또한 해야 tooprovide에 대 한 값으로 바꾸어야 `dnsNamePrefix` 및 `sshRSAPublicKey`합니다. hello 후자는 hello SSH 공개 키 tooaccess hello 클러스터입니다.) Hello 파일을 저장 합니다.

    ![서비스 주체 매개 변수 전달](./media/container-service-kubernetes-service-principal/service-principal-params.png)

3. 다음 명령을 사용 하 여, 실행된 hello `--parameters` tooset hello toohello azuredeploy.parameters.json 파일 경로입니다. 이 명령은 배포 호출 만들면 리소스 그룹의 클러스터 hello `myResourceGroup` hello 미국 서 부 지역에 있습니다.

    ```azurecli
    az login

    az account set --subscription "mySubscriptionID"

    az group create --name "myResourceGroup" --location "westus" 
    
    az group deployment create -g "myResourceGroup" --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.json" --parameters @azuredeploy.parameters.json
    ```


## <a name="option-2-generate-a-service-principal-when-creating-hello-cluster-with-az-acs-create"></a>옵션 2: hello를 사용 하는 클러스터를 만들 때 서비스 사용자를 생성`az acs create`

Hello를 실행 하는 경우 [ `az acs create` ](/cli/azure/acs#create) 명령 toocreate Kubernetes 클러스터 hello, 있는 hello 옵션 toogenerate 서비스 사용자는 자동으로 합니다.

다른 Kubernetes 클러스터 만들기 옵션과 마찬가지로 `az acs create`를 실행할 때 기존 서비스 주체에 대한 매개 변수를 지정할 수 있습니다. 그러나 이러한 매개 변수를 생략 하면 hello Azure CLI 다른 하나는 자동으로 컨테이너 서비스로 만듭니다. 이것은 투명 하 게 중에 발생 hello 배포 합니다. 

hello 다음 명령을 Kubernetes 클러스터를 만들고 SSH 키와 서비스 사용자 자격 증명을 모두 생성 합니다.

```console
az acs create -n myClusterName -d myDNSPrefix -g myResourceGroup --generate-ssh-keys --orchestrator-type kubernetes
```

> [!IMPORTANT]
> Hello 명령은 유사한 오류가 너무 생성 계정이 없으면 hello Azure AD 및 구독 사용 권한 toocreate 서비스 사용자`Insufficient privileges toocomplete hello operation.`
> 

## <a name="additional-considerations"></a>추가 고려 사항

* 가 없는 사용 권한을 toocreate 서비스 사용자 구독에 tooask 할 수 있습니다 Azure AD 또는 구독 관리자 tooassign 필요한 권한을 hello 또는 Azure 컨테이너 서비스와 서비스 보안 주체 toouse를 제공 하도록 요청 합니다. 

* Kubernetes에 대 한 주 hello 서비스는 hello 클러스터 구성의 일부입니다. 그러나 hello identity toodeploy hello 클러스터를 사용 하지 마십시오.

* 모든 서비스 주체는 Azure AD 응용 프로그램과 연결됩니다. hello Kubernetes 클러스터에 대 한 서비스 사용자와 연결할 수 있는 유효한 Azure AD 응용 프로그램 이름 (예: `https://www.contoso.org/example`). hello 응용 프로그램에 대 한 hello URL toobe 실제 끝점이 되어 있지 않습니다.

* Hello 서비스 사용자를 지정 하는 경우 **클라이언트 ID**의 hello hello 값을 사용할 수 `appId` (이 문서에 나와 있는 것) 처럼 hello 해당 서비스 사용자 또는 `name` (예를 들어`https://www.contoso.org/example`).

* Hello 마스터와 hello Kubernetes 클러스터에서 Vm 에이전트에 hello 서비스 사용자 자격 증명 hello 파일 /etc/kubernetes/azure.json에 저장 됩니다.

* Hello를 사용 하는 경우 `az acs create` toogenerate hello 서비스 사용자를 자동으로 명령을, hello 서비스 사용자 자격 증명 toorun hello 명령을 사용 하는 hello 머신에서 toohello 파일 ~/.azure/acsServicePrincipal.json 기록 됩니다. 

* Hello를 사용 하는 경우 `az acs create` toogenerate hello 서비스 사용자를 자동으로 명령을, hello 서비스 사용자로도 인증할 수는 [Azure 컨테이너 레지스트리](../../container-registry/container-registry-intro.md) 동일 hello에서 만든 구독입니다.




## <a name="next-steps"></a>다음 단계

* 컨테이너 서비스 클러스터에서 [Kubernetes를 시작합니다](container-service-kubernetes-walkthrough.md).

* tootroubleshoot hello 서비스를 사용자 Kubernetes에 대 한 참조 hello [ACS 엔진 설명서](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting)합니다.


