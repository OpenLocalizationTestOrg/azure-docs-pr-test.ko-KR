---
title: "aaaAzure 컨테이너 서비스 자습서-모니터 Kubernetes | Microsoft Docs"
description: "Azure Container Service 자습서 - Microsoft OMS(Operations Management Suite)를 사용하여 Kubernetes 모니터링"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로 서비스, Kubernetes, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 54fa789453768529deaf25d7575e5b21d0e41882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-kubernetes-cluster-with-operations-management-suite"></a>Operations Management Suite를 사용하여 Kubernetes 클러스터 모니터링

Kubernetes 클러스터 및 컨테이너를 모니터링하는 것은 중요하며, 특히 여러 앱을 사용하여 대규모의 프로덕션 클러스터를 관리하는 경우 그렇습니다. 

Microsoft 또는 다른 공급자가 제공하는 여러 Kubernetes 모니터링 솔루션을 활용할 수 있습니다. 이 자습서에서 hello 컨테이너 솔루션을 사용 하 여 Kubernetes 클러스터 모니터링 [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), Microsoft의 클라우드 기반 IT 관리 솔루션입니다. (hello 컨테이너 OMS 솔루션은 미리 보기.)

이 자습서의 7, 7 일부 작업을 수행 하는 hello를 다룹니다.

> [!div class="checklist"]
> * OMS 작업 영역 설정 가져오기
> * Hello Kubernetes 노드에서 OMS 에이전트를 설정
> * Hello OMS 포털 또는 Azure 포털에서 모니터링 정보에 액세스

## <a name="before-you-begin"></a>시작하기 전에

이전 자습서에서 컨테이너 이미지에 패키지 된 응용 프로그램, 컨테이너 레지스트리 tooAzure 및 만들어진 Kubernetes 클러스터 이러한 이미지 업로드 합니다. 다음이 단계를 수행 하지 않은 toofollow을 따라 하려는 경우 너무 반환[자습서 1-컨테이너 이미지 만들기](./container-service-tutorial-kubernetes-prepare-app.md)합니다. 

최소한 이 자습서에는 Linux 에이전트 노드가 있는 Kubernetes 클러스터 및 OMS(Operations Management Suite) 계정이 필요합니다. 필요한 경우 [OMS 평가판](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial)에 등록합니다.

## <a name="get-workspace-settings"></a>작업 영역 설정 가져오기

Hello에 액세스할 수 있습니다 때 [OMS 포털](https://mms.microsoft.com), 너무 이동**설정** > **연결 된 원본** > **Linux 서버**. Hello를 찾을 수 있습니다, *작업 영역 ID* primary 또는 secondary 상태 및 *작업 영역 키*합니다. 필요한 이러한 값을 기록해 tooset hello 클러스터에 OMS 에이전트를 합니다.

## <a name="set-up-oms-agents"></a>OMS 에이전트 설정

Hello Linux 클러스터 노드에서 OMS 에이전트를 YAML 파일 tooset 다음과 같습니다. 이 파일은 Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)를 만들며, 이는 각 클러스터 노드에서 하나의 같은 Pod를 실행합니다. hello DaemonSet 리소스는 모니터링 에이전트를 배포 하는 데 이상적입니다. 

Hello 다음 라는 텍스트 tooa 파일 저장 `oms-daemonset.yaml`, 및에 대 한 hello 자리 표시자 값 바꾸기 *myWorkspaceID* 및 *myWorkspaceKey* OMS 작업 영역 ID와 키를 사용 합니다. (프로덕션에서 이러한 값을 비밀로 인코딩할 수 있습니다.)

```YAML
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
 name: omsagent
spec:
 template:
  metadata:
   labels:
    app: omsagent
    agentVersion: v1.3.4-127
    dockerProviderVersion: 10.0.0-25
  spec:
   containers:
     - name: omsagent 
       image: "microsoft/oms"
       imagePullPolicy: Always
       env:
       - name: WSID
         value: myWorkspaceID
       - name: KEY 
         value: myWorkspaceKey
       - name: DOMAIN
         value: opinsights.azure.com
       securityContext:
         privileged: true
       ports:
       - containerPort: 25225
         protocol: TCP 
       - containerPort: 25224
         protocol: UDP
       volumeMounts:
        - mountPath: /var/run/docker.sock
          name: docker-sock
        - mountPath: /var/log 
          name: host-log
       livenessProbe:
        exec:
         command:
         - /bin/bash
         - -c
         - ps -ef | grep omsagent | grep -v "grep"
        initialDelaySeconds: 60
        periodSeconds: 60
   volumes:
    - name: docker-sock 
      hostPath:
       path: /var/run/docker.sock
    - name: host-log
      hostPath:
       path: /var/log
```

다음 명령을 hello로 DaemonSet hello를 만듭니다.

```azurecli-interactive
kubectl create -f oms-daemonset.yaml
```

toosee DaemonSet 만들어지면 해당 hello를 실행 합니다.

```azurecli-interactive
kubectl get daemonset
```

출력은 toohello 다음과 유사 합니다.

```azurecli-interactive
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE-SELECTOR   AGE
omsagent   3         3         3         0            3           <none>          5m
```

일치 하지 않음 hello 에이전트를 실행 한 후에 OMS tooingest 및 프로세스 hello 데이터에 대 일 분 정도 걸립니다.

## <a name="access-monitoring-data"></a>모니터링 데이터 액세스

보기 및 분석 hello 사용 하 여 데이터를 모니터링 하는 hello OMS 컨테이너 [컨테이너 솔루션](../../log-analytics/log-analytics-containers.md) hello OMS 포털 또는 Azure 포털 hello에 있습니다. 

hello를 사용 하 여 tooinstall hello 컨테이너 솔루션 [OMS 포털](https://mms.microsoft.com), 너무 이동**솔루션 갤러리**합니다. 그런 다음 **컨테이너 솔루션**을 추가합니다. 또는 hello에서 hello 컨테이너 솔루션에 추가할 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview)합니다.

Hello OMS 포털에서 찾아봅니다는 **컨테이너** hello OMS 대시보드의 타일 요약 합니다. 포함 한 자세한 내용은 hello 타일을 클릭 합니다: 컨테이너 이벤트, 오류, 상태, 이미지 인벤토리 및 CPU 및 메모리 사용량입니다. 더 세부적인 정보를 보려면 아무 타일에서 행을 클릭하거나 [로그 검색](../../log-analytics/log-analytics-log-searches.md)을 수행합니다.

![OMS 포털의 컨테이너 대시보드](./media/container-service-tutorial-kubernetes-monitor/oms-containers-dashboard.png)

마찬가지로, Azure 포털 hello 이동 너무**로그 분석** 작업 영역 이름을 선택 합니다. toosee hello **컨테이너** 요약 타일을 클릭 하 여 **솔루션** > **컨테이너**합니다. toosee 세부 정보는 hello 타일을 클릭 합니다.

Hello 참조 [Azure 로그 분석 설명서](../../log-analytics/index.md) 에 대 한 자세한 지침은 쿼리 및 모니터링 데이터를 분석 합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 OMS를 사용하여 Kubernetes 클러스터를 모니터링했습니다. 설명한 작업은 다음과 같습니다.

> [!div class="checklist"]
> * OMS 작업 영역 설정 가져오기
> * Hello Kubernetes 노드에서 OMS 에이전트를 설정
> * Hello OMS 포털 또는 Azure 포털에서 모니터링 정보에 액세스


컨테이너 서비스에 대 한 스크립트 샘플을 미리 만들어진이 링크 toosee를 따릅니다.

> [!div class="nextstepaction"]
> [Azure Container Service 스크립트 샘플](cli-samples.md)
