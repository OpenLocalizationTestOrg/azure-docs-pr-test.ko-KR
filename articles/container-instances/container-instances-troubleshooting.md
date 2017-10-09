---
title: "Azure 컨테이너 인스턴스 aaaTroubleshooting"
description: "Azure 컨테이너 인스턴스와 tootroubleshoot 발급 하는 방법에 대해 알아봅니다"
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
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/03/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: dfec636a0a174c74a6f2e9d9c4da6e871f8d2fda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-azure-container-instances"></a>Azure Container Instances로의 배포 문제 해결

이 문서에서는 컨테이너 tooAzure 컨테이너 인스턴스를 배포할 때 tootroubleshoot 발급 하는 방법을 보여 줍니다. 또한 hello 발생할 수 있습니다는 일반적인 문제 중 일부를 설명 합니다.

## <a name="getting-diagnostic-events"></a>진단 이벤트 가져오기

컨테이너 내에서 응용 프로그램 코드에서 tooview 로그, hello를 사용할 수 있습니다 [az 컨테이너 로그](/cli/azure/container#logs) 명령입니다. 하지만 컨테이너 성공적으로 배포 하지 않는 경우 tooreview hello 진단 정보 hello Azure 컨테이너 인스턴스 리소스 공급자가 제공 합니다. hello 다음 명령을 실행 하 여 컨테이너에 대 한 tooview hello 이벤트:

```azurecli-interactive
az container show -n mycontainername -g myresourcegroup
```

hello 출력 배포 이벤트와 함께 컨테이너의 hello 핵심 속성에 포함 됩니다.

```bash
{
  "containers": [
    {
      "command": null,
      "environmentVariables": [],
      "image": "microsoft/aci-helloworld",
      ...

      "events": [
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:52+00:00",
        "lastTimestamp": "2017-08-03T22:12:52+00:00",
        "message": "Pulling: pulling image \"microsoft/aci-helloworld\"",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Pulled: Successfully pulled image \"microsoft/aci-helloworld\"",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Created: Created container with id 61602059d6c31529c27609ef4ec0c858b0a96150177fa045cf944d7cf8fbab69",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Started: Started container with id 61602059d6c31529c27609ef4ec0c858b0a96150177fa045cf944d7cf8fbab69",
        "type": "Normal"
      }
    ],
    "name": "helloworld",
      "ports": [
        {
          "port": 80
        }
      ],
    ...
  ]
}
```

## <a name="common-deployment-issues"></a>일반 배포 문제

배포에서 대부분 오류를 차지하는 몇 가지 일반적인 문제가 있습니다.

### <a name="unable-toopull-image"></a>없습니다 toopull 이미지

Azure 컨테이너 인스턴스 수 없습니다 toopull 경우 이미지에 처음에 다시 시도 결국 실패 하기 전에 특정 기간에 대 한 합니다. Hello 이미지를 끌어올 수 없는 경우 hello 다음과 같은 이벤트가 표시 됩니다.

```bash
"events": [
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:31+00:00",
    "lastTimestamp": "2017-08-03T22:19:31+00:00",
    "message": "Pulling: pulling image \"microsoft/aci-hellowrld\"",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:32+00:00",
    "lastTimestamp": "2017-08-03T22:19:32+00:00",
    "message": "Failed: Failed toopull image \"microsoft/aci-hellowrld\": rpc error: code 2 desc Error: image microsoft/aci-hellowrld:latest not found",
    "type": "Warning"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:33+00:00",
    "lastTimestamp": "2017-08-03T22:19:33+00:00",
    "message": "BackOff: Back-off pulling image \"microsoft/aci-hellowrld\"",
    "type": "Normal"
  }
]
```

tooresolve, hello 컨테이너를 삭제 하 고 유료 면밀 hello 이미지 이름을 올바르게 입력 했는지, 배포를 다시 시도 하십시오.

### <a name="container-continually-exits-and-restarts"></a>컨테이너가 지속적으로 종료 후 다시 시작함

현재 Azure Container Instances는 장기 실행 서비스만 지원합니다. 컨테이너 toocompletion 및 종료를 실행 하는 경우 자동으로 다시 시작 하 고 다시 실행 합니다. 이 경우 다음과 같은 이벤트가 표시됩니다. Note 해당 hello 컨테이너 성공적으로 시작 하 여 다음 신속 하 게 다시 시작 합니다. hello 컨테이너 인스턴스 API에는 `retryCount` 특정 컨테이너 횟수를 보여 주는 속성을 다시 시작 했습니다.

```bash
"events": [
  {
    "count": 5,
    "firstTimestamp": "2017-08-03T22:21:55+00:00",
    "lastTimestamp": "2017-08-03T22:23:22+00:00",
    "message": "Pulling: pulling image \"alpine\"",
    "type": "Normal"
  },
  {
    "count": 5,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:23:23+00:00",
    "message": "Pulled: Successfully pulled image \"alpine\"",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:21:57+00:00",
    "message": "Created: Created container with id ad2bf9bc51761c5f935260b4bab53b164d52d9cbc045b16afcb26fb4d14d0a70",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:21:57+00:00",
    "message": "Started: Started container with id ad2bf9bc51761c5f935260b4bab53b164d52d9cbc045b16afcb26fb4d14d0a70",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:58+00:00",
    "lastTimestamp": "2017-08-03T22:21:58+00:00",
    "message": "Created: Created container with id 7687b9bd15dc01731fa66fc45f6f0241495600602dd03841e559453245e7f70b",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:58+00:00",
    "lastTimestamp": "2017-08-03T22:21:58+00:00",
    "message": "Started: Started container with id 7687b9bd15dc01731fa66fc45f6f0241495600602dd03841e559453245e7f70b",
    "type": "Normal"
  },
  {
    "count": 13,
    "firstTimestamp": "2017-08-03T22:21:59+00:00",
    "lastTimestamp": "2017-08-03T22:24:36+00:00",
    "message": "BackOff: Back-off restarting failed container",
    "type": "Warning"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:22:13+00:00",
    "lastTimestamp": "2017-08-03T22:22:13+00:00",
    "message": "Created: Created container with id 72e347e891290e238135e4a6b3078748ca25a1275dbbff30d8d214f026d89220",
    "type": "Normal"
  },
  ...
```

> [!NOTE]
> 예: bash, 셸을 hello 기본 명령으로 설정 하는 Linux 배포판에 대 한 대부분의 컨테이너 이미지 합니다. 자체 셸은 장기 실행 서비스이므로, 이러한 컨테이너는 즉시 종료된 후 다시 시작 루프를 시작합니다.

### <a name="container-takes-a-long-time-toostart"></a>컨테이너는 오랜 시간이 toostart

컨테이너는 오랜 시간이 toostart 걸리지만 최종적으로 성공, 경우에 컨테이너 이미지의 hello 크기를 확인 하 여 시작 합니다. Azure 컨테이너 인스턴스 필요에 따라 컨테이너 이미지를 가져오고, hello 시작 시간이 발생 되므로 직접 관련된 tooits 크기입니다.

Hello Docker CLI를 사용 하 여 컨테이너 이미지의 hello 크기를 볼 수 있습니다.

```bash
docker images
```

출력:

```bash
REPOSITORY                             TAG                 IMAGE ID            CREATED             SIZE
microsoft/aci-helloworld               latest              7f78509b568e        13 days ago         68.1MB
```

최종 이미지에 포함 되지 않도록 런타임에 필요 하지 않은 모든 항목 작은 hello 키 tookeeping 이미지 크기는 그대로 됩니다. 사용 하는 한 가지 방법은 toodo [여러 단계로 이루어진 빌드](https://docs.docker.com/engine/userguide/eng-image/multistage-build/)합니다. 여러 단계로 이루어진 빌드 쉽게 tooensure 게 빌드 시 응용 프로그램에 필요한 유일한 hello 아티팩트를 포함 하는 hello 최종 이미지 및는 콘텐츠의 hello 추가 필요 했습니다.

hello hello 이미지 끌어오기 컨테이너의 시작 시간에 다른 방식으로 tooreduce hello 영향은 toohost hello 컨테이너 이미지 hello에 hello Azure 컨테이너 레지스트리를 사용 하 여 동일한 지역 toouse Azure 컨테이너 인스턴스 이점을 얻을 수 있습니다. 이 hello 다운로드 시간이 크게 단축 컨테이너 이미지 요구 tootravel hello hello 네트워크 경로 단축 합니다.
