---
title: "aaaMonitor Azure Kubernetes 클러스터 Datadog으로 | Microsoft Docs"
description: "Datadog을 사용하여 Azure Container Service에서 Kubernetes 클러스터 모니터링"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: bccd8b59a048e0f791172fcfc4eeba6370dafcc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-datadog"></a>Datadog을 사용하여 Azure Container Service 클러스터 모니터링

## <a name="prerequisites"></a>필수 조건
이 연습에서는 [Azure Container Service를 사용하여 Kubernetes 클러스터를 만들었다고](container-service-kubernetes-walkthrough.md) 가정합니다.

또한 hello 있다고 가정 `az` Azure cli 및 `kubectl` 도구가 설치 되어 있습니다.

Hello 있는 경우 테스트할 수 `az` 도구를 실행 하 여 설치 합니다.

```console
$ az --version
```

Hello 없는 경우 `az` 도구를 설치 하는 명령 [여기](https://github.com/azure/azure-cli#installation)합니다.

Hello 있는 경우 테스트할 수 `kubectl` 도구를 실행 하 여 설치 합니다.

```console
$ kubectl version
```

`kubectl`이 설치되어 있지 않으면 다음을 실행할 수 있습니다.

```console
$ az acs kubernetes install-cli
```

## <a name="datadog"></a>DataDog
Datadog은 Azure 컨테이너 서비스 클러스터 내의 컨테이너에서 모니터링 데이터를 수집하는 모니터링 서비스입니다. Datadog에는 컨테이너 내에서 특정 메트릭을 볼 수 있는 Docker 통합 대시보드가 있습니다. 컨테이너에서 수집된 메트릭은 CPU, 메모리, 네트워크 및 I/O로 구성됩니다. Datadog은 메트릭을 컨테이너와 이미지로 분할합니다.

먼저 너무[계정 만들기](https://www.datadoghq.com/lpg/)

## <a name="installing-hello-datadog-agent-with-a-daemonset"></a>DaemonSet를 사용 하 여 hello Datadog 에이전트 설치
Kubernetes toorun에서 DaemonSets 사용 hello 클러스터의 각 호스트에서 컨테이너의 단일 인스턴스.
모니터링 에이전트를 실행하는 데 완벽합니다.

Hello를 따를 수를 Datadog에 로그인 한 후 [Datadog 지침](https://app.datadoghq.com/account/settings#agent/kubernetes) tooinstall Datadog 에이전트는 DaemonSet를 사용 하 여 클러스터에 있습니다.

## <a name="conclusion"></a>결론
이것으로 끝입니다. Hello 에이전트 가동 되 고 실행 하면 몇 분 안에 hello 콘솔의에서 데이터를 표시 됩니다. 통합 hello를 방문할 수 있는 [kubernetes 대시보드](https://app.datadoghq.com/screen/integration/kubernetes) toosee 클러스터에 대 한 요약입니다.
