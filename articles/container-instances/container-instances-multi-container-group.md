---
title: "컨테이너 인스턴스-다중 컨테이너 그룹 aaaAzure | Azure 문서"
description: "Azure Container Instances - 다중 컨테이너 그룹"
services: container-instances
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 976f578cd2a9bf7f05ab97f24662139bb72062ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-container-group"></a>컨테이너 그룹 배포

Azure 컨테이너 인스턴스를 사용 하 여를 하나의 호스트에 여러 컨테이너의 hello 배포를 지원 합니다.는 *컨테이너 그룹*합니다. 로깅, 모니터링 또는 서비스에 두 번째 연결된 프로세스가 필요한 기타 구성용으로 응용 프로그램 사이드카를 빌드할 때 이러한 기능을 사용하면 유용합니다. 

이 문서에서는 Azure Resource Manager 템플릿을 사용하여 간단한 다중 컨테이너 사이드카 구성을 실행하는 과정을 안내합니다.

## <a name="configure-hello-template"></a>Hello 템플릿 구성

라는 파일을 만들어 `azuredeploy.json` 고 복사 hello에 json을 따릅니다. 

이 샘플에서는 두 개의 컨테이너와 공용 IP 주소 하나가 포함된 컨테이너 그룹을 정의합니다. 인터넷 연결 응용 프로그램을 실행 하는 hello hello 그룹의 첫 번째 컨테이너입니다. hello 사이드카 hello 두 번째 컨테이너 HTTP 요청 toohello 기본 웹 응용을 프로그램 hello 그룹의 로컬 네트워크를 통해 만듭니다. 

200 이외의 HTTP 응답 코드를 확인 수신한 경우 사이드카 예제 확장된 tootrigger 경고 수 있습니다. 

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
  },
  "variables": {
    "container1name": "aci-tutorial-app",
    "container1image": "microsoft/aci-helloworld:latest",
    "container2name": "aci-tutorial-sidecar",    
    "container2image": "microsoft/aci-tutorial-sidecar"
  },
    "resources": [
      {
        "name": "myContainerGroup",
        "type": "Microsoft.ContainerInstance/containerGroups",
        "apiVersion": "2017-08-01-preview",
        "location": "[resourceGroup().location]",
        "properties": {
          "containers": [
            {
              "name": "[variables('container1name')]",
              "properties": {
                "image": "[variables('container1image')]",
                "resources": {
                  "requests": {
                    "cpu": 1,
                    "memoryInGb": 1.5
                    }
                },
                "ports": [
                  {
                    "port": 80
                  }
                ]
              }
            },
            {
              "name": "[variables('container2name')]",
              "properties": {
                "image": "[variables('container2image')]",
                "resources": {
                  "requests": {
                    "cpu": 1,
                    "memoryInGb": 1.5
                    }
                }
              }
            }
          ],
          "osType": "Linux",
          "ipAddress": {
            "type": "Public",
            "ports": [
              {
                "protocol": "tcp",
                "port": "80"
              }
            ]
          }
        }
      }
    ],
    "outputs": {
      "containerIPv4Address": {
        "type": "string",
        "value": "[reference(resourceId('Microsoft.ContainerInstance/containerGroups/', 'myContainerGroup')).ipAddress.ip]"
      }
    }
  }
```

toouse 개인 컨테이너 이미지 레지스트리를 형식에 따라 hello로 개체 toohello json 문서를 추가 합니다.

```json
"imageRegistryCredentials": [
    {
    "server": "[parameters('imageRegistryLoginServer')]",
    "username": "[parameters('imageRegistryUsername')]",
    "password": "[parameters('imageRegistryPassword')]"
    }
]
```

## <a name="deploy-hello-template"></a>Hello 템플릿을 배포합니다

Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다.

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

Hello로 hello 템플릿을 배포 [az 그룹 배포 만들기](/cli/azure/group/deployment#create) 명령입니다.

```azurecli-interactive
az group deployment create --name myContainerGroup --resource-group myResourceGroup --template-file azuredeploy.json
```

몇 초 정도 지나면 Azure에서 초기 응답이 수신됩니다. 

## <a name="view-deployment-state"></a>배포 상태 확인

tooview hello 배포 상태를 hello 사용 하 여 hello `az container show` 명령입니다. 사용자를 프로 비전 하는 hello 공용 IP 주소는 hello를 통해 응용 프로그램에 액세스할 수 있습니다를 반환 합니다.

```azurecli-interactive
az container show --name myContainerGroup --resource-group myResourceGroup -o table
```

출력:

```azurecli
Name              ResourceGroup    ProvisioningState    Image                                                             IP:ports           CPU/Memory    OsType    Location
----------------  ---------------  -------------------  ----------------------------------------------------------------  -----------------  ------------  --------  ----------
myContainerGroup  myResourceGrou2  Succeeded            microsoft/aci-tutorial-sidecar,microsoft/aci-tutorial-app:v1      40.118.253.154:80  1.0 core/1.5 gb   Linux     westus
```

## <a name="view-logs"></a>로그 보기   

Hello를 사용 하 여 컨테이너의 hello 로그 출력을 볼 `az container logs` 명령입니다. hello `--container-name` 인수 toopull 로그에서 hello 컨테이너를 지정 합니다. 이 예제에서는 hello 첫 번째 컨테이너를 지정 합니다. 

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-app --resource-group myResourceGroup
```

출력:

```bash
istening on port 80
::1 - - [27/Jul/2017:17:35:29 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:32 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:35 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:38 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
```

toosee hello hello 측 자동차 컨테이너에 대 한 로그, 지정 하 여 hello 두 번째 컨테이너 이름 명령 동일 hello를 실행 합니다.

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-sidecar --resource-group myResourceGroup
```

출력:

```bash
Every 3.0s: curl -I http://localhost                                                                                                                       Mon Jul 17 11:27:36 2017

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0  0  1663    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
HTTP/1.1 200 OK
Accept-Ranges: bytes
Content-Length: 1663
Content-Type: text/html; charset=utf-8
Last-Modified: Sun, 16 Jul 2017 02:08:22 GMT
Date: Mon, 17 Jul 2017 18:27:36 GMT
```

볼 수 있듯이 hello 사이드카 주기적으로 HTTP 요청 toohello 기본 웹 응용 프로그램을 만드는 실행 중인 hello 그룹의 로컬 네트워크 tooensure 통해 합니다.

## <a name="next-steps"></a>다음 단계

이 문서는 다중 컨테이너 Azure 컨테이너 인스턴스를 배포 하는 데 필요한 hello 단계를 설명 합니다. Azure 컨테이너 인스턴스 발생 하는 끝 tooend, hello Azure 컨테이너 인스턴스 자습서를 참조 하십시오.

> [!div class="nextstepaction"]
> [Azure Container Instances 자습서]: ./container-instances-tutorial-prepare-app.md
