---
title: "aaaMonitor Azure Kubernetes 클러스터 운영 관리 | Microsoft Docs"
description: "Microsoft Operations Management Suite를 사용하여 Azure Container Service에서 Kubernetes 클러스터 모니터링"
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
ms.openlocfilehash: 7474ee1571134ffe43ff8e4041cf5a64f5635bb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-microsoft-operations-management-suite-oms"></a>Microsoft OMS(Operations Management Suite)를 사용하여 Azure Container Service 클러스터 모니터링

## <a name="prerequisites"></a>필수 조건
이 연습에서는 [Azure Container Service를 사용하여 Kubernetes 클러스터를 만들었다고](container-service-kubernetes-walkthrough.md) 가정합니다.

또한 hello 있다고 가정 `az` Azure cli 및 `kubectl` 도구가 설치 되어 있습니다.

Hello 있는 경우 테스트할 수 `az` 도구를 실행 하 여 설치 합니다.

```console
$ az --version
```

Hello 없는 경우 `az` 도구를 설치 하는 명령 [여기](https://github.com/azure/azure-cli#installation)합니다.  
사용할 수 있습니다 [Azure 클라우드 셸](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), hello가 `az` Azure cli 및 `kubectl` 도구가 이미 설치 되어 있습니다.  

Hello 있는 경우 테스트할 수 `kubectl` 도구를 실행 하 여 설치 합니다.

```console
$ kubectl version
```

`kubectl`이 설치되어 있지 않으면 다음을 실행할 수 있습니다.
```console
$ az acs kubernetes install-cli
```

tootest kubernetes 키 kubectl 도구에 설치 되어 있는 경우 실행할 수 있습니다.
```console
$ kubectl get nodes
```

경우 hello 아웃 명령 오류, 위에 kubectl 도구 tooinstall kubernetes 클러스터 키 필요 합니다. 다음 명령을 hello로 수행할 수 있습니다.
```console
RESOURCE_GROUP=my-resource-group
CLUSTER_NAME=my-acs-name
az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME
```

## <a name="monitoring-containers-with-operations-management-suite-oms"></a>OMS(Operations Management Suite)를 사용하여 컨테이너 모니터링

OMS(Microsoft Operations Management)는 온-프레미스 및 클라우드 인프라를 관리 및 보호하는 데 유용한 Microsoft의 클라우드 기반 IT 관리 솔루션입니다. 컨테이너에서 hello 컨테이너 인벤토리 보기, 성능 및 단일 위치에 있는 로그를 사용 하면 OMS 로그 분석 솔루션을 합니다. 감사, 중앙된 위치에 hello 로그를 확인 하 여 컨테이너 문제 해결 및 사용 과다 컨테이너 호스트에 잡음이 있는 확인할 수 있습니다.

![](media/container-service-monitoring-oms/image1.png)

컨테이너 솔루션에 대 한 자세한 내용은 읽어보십시오 toothe [컨테이너, 로그 분석 솔루션](../../log-analytics/log-analytics-containers.md)합니다.

## <a name="installing-oms-on-kubernetes"></a>Kubernetes에 OMS 설치

### <a name="obtain-your-workspace-id-and-key"></a>작업 영역 ID 및 키 가져오기
OMS 에이전트 tootalk toohello 서비스 hello에 대 한 toobe 작업 영역 id와 작업 영역 키를 사용 하 여 구성 해야 합니다. 계정 tooget hello 작업 영역 id 및 toocreate는 OMS에 필요한 키 <https://mms.microsoft.com>합니다. Hello 단계 toocreate 계정을 수행 하십시오. Hello 계정 만들기를 완료 해야 tooobtain id 및 키를 클릭 하 여 **설정**, 다음 **연결 된 원본**, 차례로 **Linux 서버**다음과 같이 합니다.

 ![](media/container-service-monitoring-oms/image5.png)

### <a name="install-hello-oms-agent-using-a-daemonset"></a>DaemonSet를 사용 하 여 hello OMS 에이전트를 설치 합니다.
Kubernetes toorun에서 DaemonSets 사용 hello 클러스터의 각 호스트에서 컨테이너의 단일 인스턴스.
모니터링 에이전트를 실행하는 데 완벽합니다.

여기에 hello [DaemonSet YAML 파일](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)합니다. Tooa 파일의 이름이 저장 `oms-daemonset.yaml` 및 바꾸기에 대 한 자리 표시자 값 hello `WSID` 및 `KEY` 작업 영역 id와 hello 파일의 키입니다.

작업 영역 ID 및 키 toohello DaemonSet 구성을 추가한 후 hello 사용 하 여 클러스터에 hello OMS 에이전트를 설치할 수 있습니다 `kubectl` 명령줄 도구:

```console
$ kubectl create -f oms-daemonset.yaml
```

### <a name="installing-hello-oms-agent-using-a-kubernetes-secret"></a>Kubernetes 암호를 사용 하 여 hello OMS 에이전트를 설치 합니다.
tooprotect OMS 작업 영역 ID 및 키 Kubernetes 비밀 DaemonSet YAML 파일의 일부로 사용할 수 있습니다.

 - Hello 스크립트, 비밀 템플릿 파일 및 hello DaemonSet YAML 파일 복사 (에서 [리포지토리](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) hello에 있는지 확인 하 고 동일한 디렉터리입니다. 
      - 비밀 생성 스크립트 - secret-gen.sh
      - 비밀 템플릿 - secret-template.yaml
   - DaemonSet YAML 파일 - omsagent-ds-secrets.yaml
 - Hello 스크립트를 실행 합니다. OMS 작업 영역 ID와 기본 키 hello 스크립트 hello에 대 한 요청 합니다. 넣은 hello 스크립트에서 실행할 수 있도록 비밀 yaml 파일을 만듭니다.   
   ```
   #> sudo bash ./secret-gen.sh 
   ```

   - Hello 비밀 pod를 hello 다음을 실행 하 여 만듭니다.``` kubectl create -f omsagentsecret.yaml ```
 
   - toocheck hello 다음 실행: 

   ``` 
   root@ubuntu16-13db:~# kubectl get secrets
   NAME                  TYPE                                  DATA      AGE
   default-token-gvl91   kubernetes.io/service-account-token   3         50d
   omsagent-secret       Opaque                                2         1d
   root@ubuntu16-13db:~# kubectl describe secrets omsagent-secret
   Name:           omsagent-secret
   Namespace:      default
   Labels:         <none>
   Annotations:    <none>

   Type:   Opaque

   Data
   ====
   WSID:   36 bytes
   KEY:    88 bytes 
   ```
 
  - ``` kubectl create -f omsagent-ds-secrets.yaml ```을 실행하여 omsagent daemon-set 만들기

### <a name="conclusion"></a>결론
이것으로 끝입니다. 몇 분 후 수 toosee 데이터 tooyour OMS 대시보드에 흐름 있어야 합니다.
