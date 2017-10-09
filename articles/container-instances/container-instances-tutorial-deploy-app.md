---
title: "aaaAzure 컨테이너 인스턴스 자습서-앱 배포 | Microsoft Docs"
description: "Azure Container Instances 자습서 - 앱 배포"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b9fb098d9491e1073f0be4b14a0b9b1a18f16095
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-container-tooazure-container-instances"></a>컨테이너 tooAzure 컨테이너 인스턴스를 배포 합니다.

이 hello 세 부분으로 이루어진 자습서의 마지막 합니다. 이전 섹션에서 [컨테이너 이미지를 만든](container-instances-tutorial-prepare-app.md) 및 [tooan Azure 컨테이너 레지스트리 푸시](container-instances-tutorial-prepare-acr.md)합니다. 이 섹션 hello 컨테이너 tooAzure 컨테이너 인스턴스를 배포 하 여 hello 자습서를 완료 합니다. 완료되는 단계는 다음과 같습니다.

> [!div class="checklist"]
> * Azure Resource Manager 템플릿을 사용하여 컨테이너 그룹 정의
> * Hello Azure CLI를 사용 하 여 hello 컨테이너 그룹 배포
> * 컨테이너 로그 보기

## <a name="deploy-hello-container-using-hello-azure-cli"></a>Hello Azure CLI를 사용 하 여 hello 컨테이너 배포

hello Azure CLI에는 단일 명령으로 컨테이너 tooAzure 컨테이너 인스턴스를 배포할 수 있습니다. Hello 컨테이너 이미지는 호스트에서 개인 Azure 컨테이너 레지스트리 hello, hello 자격 증명 필요 tooaccess 포함 해야 것입니다. 필요한 경우 아래와 같이 쿼리할 수 있습니다.

컨테이너 레지스트리 로그인 서버(레지스트리 이름을 업데이트):

```azurecli-interactive
az acr show --name <acrName> --query loginServer
```

컨테이너 레지스트리 암호:

```azurecli-interactive
az acr credential show --name <acrName> --query "passwords[0].value"
```

1 CPU 코어 및 hello 다음 명령을 실행 하는 메모리를 1GB toodeploy hello 컨테이너 레지스트리 리소스와에서 컨테이너 이미지 요청입니다.

```azurecli-interactive
az container create --name aci-tutorial-app --image <acrLoginServer>/aci-tutorial-app:v1 --cpu 1 --memory 1 --registry-password <acrPassword> --ip-address public -g myResourceGroup
```

몇 초 정도 지나면 Azure Resource Manager에서 초기 응답이 수신됩니다. hello 배포 사용의 tooview hello 상태:

```azurecli-interactive
az container show --name aci-tutorial-app --resource-group myResourceGroup --query state
```

hello 상태가 변경 될 때까지이 명령을 실행 도움이 될 *보류 중인* 너무*실행*합니다. 그런 다음, 진행할 수 있습니다.

## <a name="view-hello-application-and-container-logs"></a>Hello 응용 프로그램 및 컨테이너 로그 보기

Hello 배포에 성공 하면 다음 명령을 hello의 hello 출력에 표시 된 브라우저 toohello IP 주소를 엽니다.

```bash
az container show --name aci-tutorial-app --resource-group myResourceGroup --query ipAddress.ip
```

```json
"13.88.176.27"
```

![Hello 브라우저에서 hello world 응용 프로그램][aci-app-browser]

또한 hello 컨테이너의 hello 로그 출력을 볼 수 있습니다.

```azurecli-interactive
az container logs --name aci-tutorial-app -g myResourceGroup
```

출력:

```bash
listening on port 80
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://13.88.176.27/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="next-steps"></a>다음 단계

이 자습서에서는 hello 배포 프로세스를 사용자 컨테이너 tooAzure 컨테이너 인스턴스를 완료 합니다. 단계를 수행 하는 hello 완료 되었습니다.

> [!div class="checklist"]
> * Azure CLI hello hello 컨테이너에서 hello Azure 컨테이너 레지스트리를 사용 하 여 배포
> * Hello 브라우저에서 보기 hello 응용 프로그램
> * Hello 컨테이너 로그 보기

<!-- LINKS -->
[prepare-app]: ./container-instances-tutorial-prepare-app.md

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png
