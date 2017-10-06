---
title: "컨테이너 레지스트리 webhook aaaAzure | Microsoft Docs"
description: "Azure Container Registry 웹후크"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acr, azure-container-registry
keywords: "Docker, 컨테이너, ACR"
ms.assetid: 
ms.service: container-registry
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/06/2017
ms.author: nepeters
ms.openlocfilehash: adc2afec486007e2d54cd689e6f7ef8b1098db06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-container-registry-webhooks---azure-portal"></a>Azure Container Registry 웹후크 사용 - Azure Portal

Azure 컨테이너 레지스트리에 저장 및 전용 Docker 컨테이너 이미지를 Docker 허브 공용 Docker 이미지를 저장 하는 비슷한 toohello 방식으로 관리 합니다. 레지스트리 리포지토리 중 하나에서 특정 작업이 수행 될 때 webhook tootrigger 이벤트를 사용 합니다. 또한 Webhook tooevents hello 레지스트리 수준에서 응답할 수 또는 tooa 특정 저장소 태그 아래로 범위 지정할 수 있습니다. 

자세한 배경 및 개념에 대 한 참조 hello [개요](./container-registry-intro.md)합니다.

## <a name="prerequisites"></a>필수 조건 

- Azure 컨테이너 관리 레지스트리 - Azure 구독에서 관리되는 컨테이너 레지스트리를 만듭니다. 예를 들어 hello Azure 포털을 사용 하 여 또는 Azure CLI 2.0을 환영 합니다. 
- Docker CLI-tooset는 Docker 호스트 및 액세스 hello Docker CLI 명령으로 로컬 컴퓨터를 Docker 엔진을 설치 합니다. 

## <a name="create-webhook-azure-portal"></a>웹후크 Azure Portal 만들기

1. Azure 포털 toohello을 고 toocreate webhook 원하는 toohello 레지스트리를 탐색 합니다. 

2. Hello 컨테이너 블레이드 hello "Webhook" 탭을 선택 합니다. 

3. Hello webhook 블레이드 도구 모음에서 "추가"를 선택 합니다. 

4. 전체 hello *Webhook 만들기* 양식에 다음 정보는 hello로:

| 값 | 설명 |
|---|---|
| 이름 | hello 이름 toogive toohello webhook입니다. 소문자와 숫자만 사용할 수 있으며 5-50자 사이입니다. |
| 서비스 URI | hello hello webhook POST 알림을 보내야 위치 URI입니다. |
| 사용자 지정 헤더 | Hello POST 요청과 함께 toopass 원하는 헤더입니다. "키: 값" 형식이어야 합니다. |
| 트리거 동작 | Hello webhook을 트리거하는 동작입니다. 현재 webhook 푸시에 의해 트리거될 수 및/또는 동작 tooan 이미지를 삭제 합니다. |
| 가동 상태 | hello webhook 만든 후에 대 한 hello 상태입니다. 기본적으로 사용하도록 설정되어 있습니다. |
| 범위 | hello 범위는 hello webhook 작동 합니다. 기본 hello 레지스트리의 모든 이벤트에 대 한 hello 범위가입니다. Hello 형식을 사용 하 여 저장소 또는 태그를 지정할 수 있습니다 "저장소: 태그"입니다. |

웹후크 양식 예제:

![DCOS UI](./media/container-registry-webhook/webhook.png)

## <a name="create-webhook-azure-cli"></a>웹후크 Azure CLI 만들기

사용 하 여 webhook toocreate hello Azure CLI를 사용 하 여 hello [az acr webhook 만들기](/cli/azure/acr/webhook#create) 명령입니다.

```azurecli-interactive
az acr webhook create --registry mycontainerregistry --name myacrwebhook01 --actions delete --uri http://webhookuri.com
```

## <a name="test-webhook"></a>웹후크 테스트

### <a name="azure-portal"></a>Azure portal

Hello를 사용 하 여 테스트할 수 있습니다, 컨테이너에 이전 toousing hello webhook 밀어넣기 이미지 및 삭제 작업 **Ping** 단추입니다. 을 사용 하는 제네릭 post 요청 toohello 지정한 끝점 및 로그 hello 응답 Ping hello가 보냅니다. 이 기능은 유용 webhook hello tooverify가 올바르게 설정 되어 있습니다.

1. 원하는 tootest hello webhook을 선택 합니다. 
2. Hello 맨 위의 도구 모음에서 hello "Ping" 작업을 선택 합니다. 
3. Hello 요청 및 응답을 확인 합니다.

### <a name="azure-cli"></a>Azure CLI

tootest hello Azure CLI로 ACR webhook hello를 사용 하 여 [az acr webhook ping](/cli/azure/acr/webhook#ping) 명령입니다.

```azurecli-interactive
az acr webhook ping --registry mycontainerregistry --name myacrwebhook01
```

toosee hello 결과 사용 하 여 hello [az acr webhook 목록 이벤트](/cli/azure/acr/webhook#list-events) 명령입니다. 

```azurecli-interactive
az acr webhook list-events --registry mycontainerregistry08 --name myacrwebhook01
```

## <a name="delete-webhook"></a>웹후크 삭제

### <a name="azure-portal"></a>Azure portal

Hello webhook 및 hello Azure 포털에서 hello 삭제 단추를 선택 하 여 각 webhook은 삭제할 수 있습니다.

### <a name="azure-cli"></a>Azure CLI

```azurecli-interactive
az acr webhook delete --registry mycontainerregistry --name myacrwebhook01
```