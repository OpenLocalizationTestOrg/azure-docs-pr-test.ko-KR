---
title: "Azure에서 클러스터를 Docker 컨테이너 aaaDeploy | Microsoft Docs"
description: "Hello Azure 포털 또는 리소스 관리자 템플릿을 사용 하 여 Azure 컨테이너 서비스의 Kubernetes, DC/OS 또는 docker는 Docker Swarm 솔루션을 배포 합니다."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로 서비스, Mesos, Azure, DCOS, Swarm, Kubernetes, Azure Container Service, ACS"
ms.service: container-service
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: rogardle
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 26e3a7d0af9d71acd8b5c85fd667fcf7d84cef66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-hello-azure-portal"></a>호스팅 솔루션 hello Azure 포털을 사용 하 여 Docker 컨테이너 배포



Azure 컨테이너 서비스는 인기 있는 오픈 소스 컨테이너 클러스터링 및 오케스트레이션 솔루션의 신속한 배포를 제공합니다. 이 문서에서는 Azure 리소스 관리자 퀵 스타트 템플릿이나 hello Azure 포털을 사용 하 여 Azure 컨테이너 서비스 클러스터를 배포 하는 과정을 안내 합니다. 

Hello를 사용 하 여 Azure 컨테이너 서비스 클러스터를 배포할 수도 [Azure CLI 2.0](container-service-create-acs-cluster-cli.md) 또는 Azure 컨테이너 서비스 Api를 환영 합니다.

배경 지식은 [Azure Container Service 소개](../container-service-intro.md)를 참조하세요.


## <a name="prerequisites"></a>필수 조건

* **Azure 구독**: 없는 경우 지금 [무료 평가판](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935)에 등록하세요. 대규모 클러스터의 경우, 종량제 구독이나 다른 구매 옵션을 고려하세요.

    > [!NOTE]
    > Azure 구독 사용 현황 및 [리소스 할당량](../../azure-subscription-service-limits.md), 코어 할당량과 같은 hello 클러스터 배포의 hello 크기를 제한할 수 있습니다. 할당량 증가 열기 toorequest는 [온라인 고객 지원 요청](../../azure-supportability/how-to-create-azure-support-request.md) 비용 없이 합니다.
    >

* **SSH RSA 공개 키**: hello 포털 또는 hello Azure 빠른 시작 템플릿 중 하나를 통해 배포, 있습니다 tooprovide hello 공개 키에 대 한 필요 컨테이너 서비스를 Azure 가상 컴퓨터에 대 한 인증 합니다. toocreate SSH (보안 셸) RSA 키 참조 hello [Osx 및 Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) 또는 [Windows](../../virtual-machines/linux/ssh-from-windows.md) 지침. 

* **주 클라이언트 ID와 암호를 서비스** (Kubernetes만): 자세한 정보와 지침 toocreate Azure Active Directory 서비스 사용자를 참조 하십시오. [Kubernetes 클러스터에 대 한 hello 서비스 사용자에 대 한](../kubernetes/container-service-kubernetes-service-principal.md)합니다.



## <a name="create-a-cluster-by-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 클러스터 만들기
1. Toohello Azure 포털에에서 로그인 선택 **새로**, 검색에 대 한 Azure 마켓플레이스 hello **Azure 컨테이너 서비스**합니다.

    ![Marketplace의 Azure Container Service](./media/container-service-deployment/acs-portal1.png)  <br />

2. **Azure Container Service**를 클릭하고 **만들기**를 클릭합니다.

3. Hello에 **기본 사항** 블레이드에서 hello 다음 정보를 입력 합니다.

    * **Orchestrator**: hello 컨테이너 orchestrators toodeploy hello 클러스터 중 하나를 선택 합니다.
        * **DC/OS**: DC/OS 클러스터를 배포합니다.
        * **Swarm**: Docker Swarm 클러스터를 배포합니다.
        * **Kubernetes**: Kubernetes 클러스터를 배포합니다.
    * **구독**: Azure 구독을 선택합니다.
    * **리소스 그룹**: hello 배포에 대 한 새 리소스 그룹의 hello 이름을 입력 합니다.
    * **위치**: hello Azure 컨테이너 서비스 배포에 대 한 Azure 지역을 선택 합니다. 가용성은 [지역별 사용 가능한 제품](https://azure.microsoft.com/regions/services/)을 참조하세요.
    
    ![기본 설정](./media/container-service-deployment/acs-portal3.png)  <br />
    
    클릭 **확인** 준비 tooproceed 라인인 경우입니다.

4. Hello에 **구성 마스터** 블레이드에서 hello hello Linux 마스터 노드 또는 (일부 설정은 특정 tooeach orchestrator 검색) hello 클러스터의 노드에 대 한 설정을 다음 입력:

    * **마스터 DNS 이름**: hello master에 대 한 정규화 된 도메인 이름 (FQDN) hello 사용 되는 접두사 toocreate는 고유 합니다. hello 폼의 마스터 FQDN은 hello *접두사*관리*위치*. cloudapp.azure.com 합니다.
    * **사용자 이름**: hello 클러스터의 hello Linux 가상 컴퓨터의 각 계정에 대 한 hello 사용자 이름입니다.
    * **SSH RSA 공개 키**: hello 공개 키 toobe hello Linux 가상 컴퓨터에 대 한 인증에 사용 되는 추가 합니다. 이 키에 줄 바꿈이 없어야 하 고 hello 포함 것이 중요 `ssh-rsa` 접두사입니다. hello `username@domain` 접미사는 선택 사항입니다. hello 키 해야 hello 다음과 유사할: **ssh rsa AAAAB3Nz... <>...... UcyupgH azureuser@linuxvm** 합니다. 
    * **서비스 사용자**: hello Kubernetes orchestrator를 선택한 경우 입력 Azure Active Directory **주 클라이언트 ID를 서비스** (hello appId 라고도 함) 및 **서비스보안주체클라이언트암호** (암호)입니다. 자세한 내용은 참조 [Kubernetes 클러스터에 대 한 hello 서비스 사용자에 대 한](../kubernetes/container-service-kubernetes-service-principal.md)합니다.
    * **Count 마스터**: hello hello 클러스터에서 마스터의 수입니다.
    * **VM 진단**: 일부 orchestrators VM 진단 hello 마스터에 사용할 수 있습니다.

    ![마스터 구성](./media/container-service-deployment/acs-portal4.png)  <br />

    클릭 **확인** 준비 tooproceed 라인인 경우입니다.

5. Hello에 **에이전트 구성** 블레이드에서 hello 다음 정보를 입력 합니다.

    * **에이전트 개수의**: Docker 웜 및 Kubernetes이이 값은 hello hello 에이전트 크기 집합에 에이전트의 초기 수 있습니다. DC/OS hello 개인 크기 집합에 에이전트의 초기 수는. 또한, 사전에 지정된 수의 에이전트를 포함하는 DC/OS에 대한 공개 규모 집합이 생성됩니다. hello 수가이 공용 크기 집합의 에이전트 결정 hello 클러스터에서 마스터의 hello 번호로: 하나의 마스터에 대해 하나의 공용 에이전트가 및 세 가지 또는 5 개인 마스터에 대 한 두 명의 공용 에이전트입니다.
    * **에이전트가 가상 컴퓨터 크기**: hello hello 에이전트가 가상 컴퓨터의 크기입니다.
    * **운영 체제**:이 설정은 현재 hello Kubernetes orchestrator를 선택한 경우에 사용할 수입니다. Linux 배포 또는 hello 에이전트에서 Windows Server 운영 체제 toorun 중 하나를 선택 합니다. 이 설정은 클러스터가 Linux 또는 Windows 컨테이너 앱을 실행할 수 있을지 여부를 결정합니다. 

        > [!NOTE]
        > Windows 컨테이너 지원은 Kubernetes 클러스터에 대해 미리 보기 상태입니다. DC/OS 및 Swarm 클러스터의 경우 현재 Linux 에이전트만 Azure Container Service에서 지원됩니다.

    * **에이전트 자격 증명**: hello Windows 운영 체제를 선택한 경우 입력 관리자 **사용자 이름** 및 **암호** hello 에이전트 Vm에 대 한 합니다. 

    ![에이전트 구성](./media/container-service-deployment/acs-portal5.png)  <br />

    클릭 **확인** 준비 tooproceed 라인인 경우입니다.

6. 서비스 유효성 검사가 완료되면 **확인**을 클릭합니다.

    ![유효성 검사](./media/container-service-deployment/acs-portal6.png)  <br />

7. Hello 용어를 검토 합니다. toostart hello 배포 프로세스를 클릭 하 여 **만들기**합니다.

    Toopin hello 배포 toohello Azure 포털을 설정 했으면, hello 배포 상태를 볼 수 있습니다.

    ![배포 상태](./media/container-service-deployment/acs-portal8.png)  <br />

hello 배포는 몇 분 toocomplete 합니다. 그런 다음 hello Azure 컨테이너 서비스 클러스터 사용할 준비가 됩니다.


## <a name="create-a-cluster-by-using-a-quickstart-template"></a>빠른 시작 템플릿을 사용하여 클러스터 만들기
Azure 빠른 시작 템플릿은 Azure 컨테이너 서비스의 클러스터 toodeploy를 사용할 수 있습니다. hello 제공 퀵 스타트 서식 파일 수정된 tooinclude 추가 또는 고급 Azure 구성 될 수 있습니다. Azure 빠른 시작 템플릿을 사용 하 여 Azure 컨테이너 서비스 클러스터는 toocreate Azure 구독이 필요 합니다. 없는 경우 [무료 평가판](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935)에 등록하세요. 

이러한 단계 toodeploy 템플릿을 사용 하는 클러스터를 따르고 hello Azure CLI 2.0 (참조 [설치 및 설치 지침](/cli/azure/install-az-cli2)).

> [!NOTE] 
> Windows 시스템을 사용 하는 경우 비슷한 단계 toodeploy을 Azure PowerShell을 사용 하 여 템플릿을 사용할 수 있습니다. 이 섹션의 뒷부분에 나오는 단계를 참조하세요. Hello 통해 서식 파일을 배포할 수도 있습니다 [포털](../../azure-resource-manager/resource-group-template-deploy-portal.md) 또는 다른 방법입니다.

1. DC/OS, docker는 Docker Swarm 또는 Kubernetes 클러스터 toodeploy GitHub에서 hello 빠른 시작 사용 가능한 템플릿 중 하나를 선택 합니다. 다음은 일부 목록입니다. hello DC/OS 및 웜 템플릿 hello 기본 orchestrator 선택 제외 하 고 동일한 hello 됩니다.

    * [DC/OS 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [Swarm 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [Kubernetes 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. Tooyour Azure 계정에에서 로그인 (`az login`), 해당 hello Azure CLI 연결된 tooyour Azure 구독 인지 확인 합니다. 다음 명령을 hello를 사용 하 여 hello 기본 구독을 확인할 수 있습니다.

    ```azurecli
    az account show
    ```
    
    둘 이상의 구독과 필요 tooset 다른 기본 구독을 보유 하는 경우 실행 `az account set --subscription` hello 구독 ID 또는 이름을 지정 합니다.

3. 모범 사례로, hello 배포에 대 한 새 리소스 그룹을 사용 합니다. 리소스 그룹 toocreate hello를 사용 하 여 `az group create` 명령은 리소스 그룹 이름 및 위치 지정: 

    ```azurecli
    az group create --name "RESOURCE_GROUP" --location "LOCATION"
    ```

4. JSON 파일 포함 hello 필요한 템플릿 매개 변수를 만듭니다. 명명 된 다운로드 hello 매개 변수 파일 `azuredeploy.parameters.json` hello Azure 컨테이너 서비스 템플릿을 함께 제공 되는 `azuredeploy.json` GitHub에서 합니다. 클러스터에 대한 필수 매개 변수 값을 입력합니다. 

    예를 들어 toouse hello [DC/OS 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), 매개 변수 값을 제공할 `dnsNamePrefix` 및 `sshRSAPublicKey`합니다. 참조의 hello 설명 `azuredeploy.json` 및 다른 매개 변수에 대 한 옵션입니다.  
 

5. 다음 명령을, hello로 hello 배포 매개 변수 파일을 전달 하 여 컨테이너 서비스 클러스터를 만들 위치:

    * **RESOURCE_GROUP** hello hello 이전 단계에서 만든 hello 리소스 그룹 이름입니다.
    * **DEPLOYMENT_NAME** (선택 사항) 이름인 toohello 배포를 제공 합니다.
    * **TEMPLATE_URI** 는 hello 배포 파일의 위치 hello `azuredeploy.json`합니다. 이 URI는 포인터 toohello GitHub UI hello 원시 파일 이어야 합니다. toofind 선택 hello이이 URI `azuredeploy.json` GitHub에서 파일을 hello 클릭 **Raw** 단추입니다.  

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters @azuredeploy.parameters.json
    ```

    또한 hello 명령줄에서 JSON 형식 문자열 매개 변수를 제공할 수 있습니다. 명령 비슷한 toohello 다음을 사용 합니다.

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters "{ \"param1\": {\"value1\"} … }"
    ```

    > [!NOTE]
    > hello 배포는 몇 분 toocomplete 합니다.
    > 

### <a name="equivalent-powershell-commands"></a>동일한 PowerShell 명령
PowerShell 사용하여 Azure Container Service 클러스터 템플릿을 배포할 수도 있습니다. 이 문서는 hello 버전 1.0 기반 [Azure PowerShell 모듈](https://azure.microsoft.com/blog/azps-1-0/)합니다.

1. DC/OS, docker는 Docker Swarm 또는 Kubernetes 클러스터 toodeploy GitHub에서 hello 빠른 시작 사용 가능한 템플릿 중 하나를 선택 합니다. 다음은 일부 목록입니다. 참고는 hello DC/OS 및 웜 서식 파일은 hello 동일 hello 예외 hello 기본 orchestrator 선택입니다.

    * [DC/OS 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [Swarm 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [Kubernetes 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. Azure 구독에서 클러스터를 만들기 전에 tooAzure에서 PowerShell 세션에 서명이 있는지 확인 합니다. Hello로 이렇게 하려면 `Get-AzureRMSubscription` 명령:

    ```powershell
    Get-AzureRmSubscription
    ```

3. Hello를 사용 하 여 toosign tooAzure에서 해야 할 경우 `Login-AzureRMAccount` 명령:

    ```powershell
    Login-AzureRmAccount
    ```

4. 모범 사례로, hello 배포에 대 한 새 리소스 그룹을 사용 합니다. 리소스 그룹 toocreate hello를 사용 하 여 `New-AzureRmResourceGroup` 명령을 실행 하 고 리소스 그룹 이름 및 대상 지역을 지정 합니다.

    ```powershell
    New-AzureRmResourceGroup -Name GROUP_NAME -Location REGION
    ```

5. 리소스 그룹을 만든 후 다음 명령을 hello로 클러스터를 만들 수 있습니다. hello hello의 URI 템플릿이 hello로 지정 되어 필요한 `-TemplateUri` 매개 변수입니다. 이 명령을 실행하면 PowerShell에서 배포 매개 변수 값을 묻는 메시지가 표시됩니다.

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DEPLOYMENT_NAME -ResourceGroupName RESOURCE_GROUP_NAME -TemplateUri TEMPLATE_URI
    ```

#### <a name="provide-template-parameters"></a>템플릿 매개 변수 제공
PowerShell에 익숙하다면 빼기 기호 (-)를 입력 하 고 다음 hello TAB 키를 눌러 cmdlet에 대 한 사용 가능한 매개 변수 hello 순환 하는 것입니다. 이 기능은 템플릿에 정의하는 매개 변수에 대해서도 작동합니다. Hello 템플릿 이름을 입력 하는 즉시 hello cmdlet는 hello 서식 파일을 인출 하 hello 매개 변수를 구문 분석 하 고 hello 템플릿 매개 변수 toohello 명령을 동적으로 추가 합니다. 이 통해 쉽게 toospecify hello 템플릿 매개 변수 값. 하며, 필요한 매개 변수 값을 잊은 경우 PowerShell 묻는 hello 값에 대 한 합니다.

다음은 매개 변수가 포함 되어 있는 hello 전체 명령이입니다. Hello 리소스의 hello 이름에 대 한 사용자 지정 값을 제공 합니다.

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName RESOURCE_GROUP_NAME-TemplateURI TEMPLATE_URI -adminuser value1 -adminpassword value2 ....
```

## <a name="next-steps"></a>다음 단계
이제 클러스터가 작동하기 시작했으니 연결 및 관리 정보는 다음 문서를 참조하세요.

* [Tooan Azure 컨테이너 서비스 클러스터에 연결](../container-service-connect.md)
* [Azure 컨테이너 서비스 및 DC/OS로 작업](container-service-mesos-marathon-rest.md)
* [Azure 컨테이너 서비스 및 Docker Swarm으로 작업](container-service-docker-swarm.md)
* [Azure Container Service 및 Kubernetes로 작업](../kubernetes/container-service-kubernetes-walkthrough.md)
