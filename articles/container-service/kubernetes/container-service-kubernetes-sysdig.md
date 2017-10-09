---
title: "aaaMonitor Azure Kubernetes 클러스터 Sysdig | Microsoft Docs"
description: "Sysdig을 사용하여 Azure Container Service에서 Kubernetes 클러스터 모니터링"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: a27813d01ee4624b9e993f6185169ad73aeec3a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-using-sysdig"></a>Sysdig을 사용하여 Azure Container Service Kubernetes 클러스터 모니터링

## <a name="prerequisites"></a>필수 조건
이 연습에서는 [Azure Container Service를 사용하여 Kubernetes 클러스터를 만들었다고](container-service-kubernetes-walkthrough.md) 가정합니다.

또한 hello azure cli 및 kubectl 도구가 설치 되어 있다고 가정 합니다.

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

## <a name="sysdig"></a>Sysdig
Sysdig은 Azure에서 실행 중인 Kubernetes 클러스터에 대한 컨테이너를 모니터링할 수 있는 외부 모니터링 서비스 회사입니다. Sysdig을 사용하려면 활성 Sysdig 계정이 필요합니다.
[사이트](https://app.sysdigcloud.com)에서 계정에 등록할 수 있습니다.

Toohello Sysdig 클라우드 웹 사이트를 로그인 후 사용자 이름을 클릭 하 고 "액세스 키입니다." hello 페이지에 표시 됩니다. 

![Sysdig API 키](./media/container-service-kubernetes-sysdig/sysdig2.png)

## <a name="installing-hello-sysdig-agents-tookubernetes"></a>Hello Sysdig 에이전트 tooKubernetes 설치
컨테이너, 각 프로세스가 Sysdig 실행 컴퓨터는 Kubernetes를 사용 하 여 toomonitor `DaemonSet`합니다.
DaemonSets은 컴퓨터당 컨테이너의 단일 인스턴스를 실행하는 Kubernetes API 개체입니다.
Hello Sysdig의 모니터링 에이전트와 같은 도구를 설치 하기 위한 완벽 한 일입니다.

tooinstall hello Sysdig daemonset 먼저 다운로드 해야 [hello 템플릿](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) sysdig에서 합니다. 해당 파일을 `sysdig-daemonset.yaml`로 저장합니다.

Linux 및 OS X에서 다음을 실행할 수 있습니다.

```console
$ curl -O https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml
```

PowerShell에서:

```console
$ Invoke-WebRequest -Uri https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml | Select-Object -ExpandProperty Content > sysdig-daemonset.yaml
```

그런 다음 해당 파일 tooinsert Sysdig 계정에서 얻은 하 여 액세스 키를 편집 합니다.

마지막으로, DaemonSet hello를 만듭니다.

```console
$ kubectl create -f sysdig-daemonset.yaml
```

## <a name="view-your-monitoring"></a>모니터링 보기
설치 하 고 실행 되 면 hello 에이전트 백 tooSysdig 데이터를 펌프 해야 합니다.  Toothe 돌아가서 [sysdig 대시보드](https://app.sysdigcloud.com) 사용자 컨테이너에 대 한 정보를 표시 됩니다.

[새 대시보드 마법사](https://app.sysdigcloud.com/#/dashboards/new)를 통해 Kubernetes 특정 대시보드를 설치할 수도 있습니다.
