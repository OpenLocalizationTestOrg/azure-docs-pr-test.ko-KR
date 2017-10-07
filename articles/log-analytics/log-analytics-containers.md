---
title: "Azure 로그 분석에서 모니터링 솔루션 aaaContainer | Microsoft Docs"
description: "로그 분석에서 솔루션 컨테이너 모니터링 hello를 사용 하면 Docker 및 Windows 보기 및 관리를 단일 위치에서 컨테이너 호스트입니다."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e1e4b52b-92d5-4bfa-8a09-ff8c6b5a9f78
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte;banders
ms.openlocfilehash: 2eed1dd81c22faef78a375fca3ebece9e5300c09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="container-monitoring-solution-in-log-analytics"></a>Log Analytics의 컨테이너 모니터링 솔루션

![컨테이너 기호](./media/log-analytics-containers/containers-symbol.png)

이 문서에서 설명 하는 방법을 tooset를 사용 하 여 hello Docker 및 Windows 보기 및 관리 하는 데 도움이 되는 로그 분석에서 컨테이너 모니터링 솔루션을 한 위치에 컨테이너 호스트입니다. 소프트웨어 배포 tootheir IT 자동화 하는 toocreate 컨테이너를 사용 하는 소프트웨어 가상화 시스템으로 한 docker는 인프라입니다.

솔루션에서는 컨테이너는 실행 되는 어떤 컨테이너 이미지를 실행 중인 hello 및 컨테이너를 실행 하는 합니다. 컨테이너에 사용하는 명령을 표시하는 상세한 감사 정보를 확인할 수 있습니다. 및 보기 tooremotely 보기 Docker 또는 Windows 호스트 필요 없이 중앙 집중화 된 로그를 검색 하 여 컨테이너의 문제를 해결할 수 있습니다. 호스트에서 성가시고 과도한 리소스를 소모하는 컨테이너를 찾을 수 있습니다. 또한 컨테이너에 대해 중앙화된 CPU 메모리, 저장소, 네트워크 사용 및 성능 정보를 확인할 수 있습니다. Windows를 실행하는 컴퓨터에서 Windows Server, Hyper-V, Docker 컨테이너에서 로그를 중앙 집중화 및 비교할 수 있습니다. hello 솔루션 컨테이너 orchestrators 다음 hello를 지원 합니다.

- Docker Swarm
- DC/OS
- kubernetes
- 서비스 패브릭
- Red Hat OpenShift


hello 다음 다이어그램 관계를 보여 hello 다양 한 컨테이너 호스트와 에이전트가 OMS와 함께 합니다.

![컨테이너 다이어그램](./media/log-analytics-containers/containers-diagram.png)

## <a name="system-requirements"></a>시스템 요구 사항

을 시작 하기 전에 다음 세부 정보 tooverify hello 필수 조건을 충족 하는 hello를 검토 합니다.

### <a name="container-monitoring-solution-support-for-docker-orchestrator-and-os-platform"></a>Docker Orchestrator 및 OS 플랫폼에 대한 컨테이너 모니터링 솔루션 지원
hello 다음 표에 정리 되어 hello Docker 오케스트레이션 및 운영 체제 지원 컨테이너 인벤토리, 성능 및 로그 분석을 사용 하 여 로그를 모니터링 합니다.   

| | ACS | Linux | Windows | 컨테이너<br>인벤토리 | 이미지<br>인벤토리 | 노드<br>인벤토리 | 컨테이너<br>성능 | 컨테이너<br>이벤트 | 이벤트<br>로그 | 컨테이너<br>로그 |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| kubernetes | &#8226; | &#8226; | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; |
| Mesosphere<br>DC/OS | &#8226; | &#8226; | | &#8226; | &#8226; | &#8226; | &#8226;| &#8226; | &#8226; | &#8226; |
| Docker<br>Swarm | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | | &#8226; |
| 부여<br>Fabric | | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; |
| Red Hat Open<br>Shift | | &#8226; | | &#8226; | &#8226;| &#8226; | &#8226; | &#8226; | | &#8226; |
| Windows Server<br>(독립 실행형) | | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | | &#8226; |
| Linux 서버<br>(독립 실행형) | | &#8226; | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | | &#8226; |


### <a name="docker-versions-supported-on-linux"></a>Linux에서 지원되는 Docker 버전

- Docker 1.11 too1.13
- Docker CE 및 EE v17.06

### <a name="x64-linux-distributions-supported-as-container-hosts"></a>컨테이너 호스트로 지원되는 x64 Linux 배포

- Ubuntu 14.04 LTS 및 16.04 LTS
- CoreOS(stable)
- Amazon Linux 2016.09.0
- openSUSE 13.2
- openSUSE LEAP 42.2
- CentOS 7.2 및 7.3
- SLES 12
- RHEL 7.2 및 7.3
- Red Hat OCP(OpenShift Container Platform) 3.4 및 3.5
- ACS Mesosphere DC/OS 1.7.3 too1.8.8
- ACS Kubernetes 1.4.5 too1.6
- ACS Docker Swarm

### <a name="supported-windows-operating-system"></a>지원되는 Windows 운영 체제

- Windows Server 2016
- Windows 10 1주년 버전(Professional 또는 Enterprise)

### <a name="docker-versions-supported-on-windows"></a>Windows에서 지원되는 Docker 버전

- Docker 1.12 - 1.13
- Docker 17.03.0 이상

## <a name="installing-and-configuring-hello-solution"></a>설치 하 고 hello 솔루션 구성
다음 정보 tooinstall hello를 사용 하 고 hello 솔루션을 구성 합니다.

1. Hello 컨테이너 모니터링 솔루션 tooyour OMS 작업 영역에서 추가 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) 또는에 설명 된 hello 프로세스를 사용 하 여 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.

2. OMS 에이전트를 사용하여 Docker를 설치 및 사용합니다.  운영 체제에 따라 hello 메서드를 다음에서 선택할 수 있습니다.

  * 지원 되는 Linux 운영 체제에 설치 및 Docker를 실행 하 고 하 고 다음을 설치 하 고 hello 구성 [Linux 용 OMS 에이전트](log-analytics-agent-linux.md)합니다.  
  * CoreOS에 Linux 용 OMS 에이전트 hello를 실행할 수 없습니다. 대신, Linux에 대 한 컨테이너 화 된 버전의 hello OMS 에이전트를 실행 합니다. Azure Government 클라우드에서 컨테이너를 사용하는 경우 [CoreOS를 포함한 Linux 컨테이너 호스트](#for-all-linux-container-hosts-including-coreos) 또는 [CoreOS을 포함한 Azure Government Linux 컨테이너 호스트](#for-all-azure-government-linux-container-hosts-including-coreos)를 검토하세요.
  * Windows Server 2016 및 Windows 10에서 hello Docker 엔진 및 클라이언트를 설치 후 에이전트 toogather 정보를 연결 하 고 tooLog 분석을 보냅니다.  

### <a name="container-services"></a>Container Service

- Red Hat OpenShift 환경인 경우 [Red Hat OpenShift용 OMS 에이전트 구성](#configure-an-oms-agent-for-red-hat-openshift)을 검토하세요.
- Hello Azure 컨테이너 서비스를 사용 하는 Kubernetes 클러스터를 설정한 경우 검토 [Azure 컨테이너 서비스 클러스터 Microsoft 작업 관리 도구 모음 (OMS)으로 모니터링](../container-service/kubernetes/container-service-kubernetes-oms.md)합니다.
- Azure Container Service DC/OS 클러스터가 있는 경우 [Operations Management Suite를 사용하여 Azure Container Service DC/OS 클러스터 모니터링](../container-service/dcos-swarm/container-service-monitoring-oms.md)에서 자세한 내용을 참조하세요.
- Docker Swarm 모드 환경에 있는 경우 [Docker Swarm용 OMS 에이전트 구성](#configure-an-oms-agent-for-docker-swarm)에서 자세히 알아보세요.
- Service Fabric과 함께 컨테이너를 사용하는 경우 [Azure Service Fabric의 개요](../service-fabric/service-fabric-overview.md)에서 자세히 알아보세요.
- 검토 hello [Windows에서 Docker 엔진](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) 방법에 대 한 자세한 내용은 문서 tooinstall 하 고 Windows를 실행 하는 컴퓨터에 Docker 엔진을 구성 합니다.

> [!IMPORTANT]
> Docker 실행 중 이어야 합니다 **전에** hello 설치 [Linux 용 OMS 에이전트](log-analytics-agent-linux.md) 컨테이너 호스트에 있습니다. Docker를 설치 하기 전에 hello 에이전트를 이미 설치한 경우 Linux 용 OMS 에이전트 tooreinstall hello가 필요 합니다. Docker에 대 한 자세한 내용은 참조 hello [Docker 웹 사이트](https://www.docker.com)합니다.


## <a name="linux-container-hosts"></a>Linux 컨테이너 호스트

Docker를 설치 하 고 나면 다음 Docker와 함께 사용할 컨테이너 호스트 tooconfigure hello 에이전트에 대 한 설정을 hello를 사용 합니다. 먼저 OMS 작업 영역 ID 및 키 hello Azure 포털에서에서 찾을 수 있습니다. 작업 영역에서 클릭 **빠른 시작** > **컴퓨터** tooview 프로그램 **작업 영역 ID** 및 **기본 키**합니다.  두 항목을 복사하여 선호하는 편집기에 붙여넣습니다.

### <a name="for-all-linux-container-hosts-except-coreos"></a>CoreOS를 제외한 모든 Linux 컨테이너 호스트의 경우

- 자세한 내용 및 단계 tooinstall Linux 용 OMS 에이전트를 hello 하는 방법에 대 한 참조 [프로그램 Linux 컴퓨터 tooOperations Management Suite (OMS) 연결](log-analytics-agent-linux.md)합니다.

### <a name="for-all-linux-container-hosts-including-coreos"></a>CoreOS를 포함한 모든 Linux 컨테이너 호스트의 경우

원하는 toomonitor hello OMS 컨테이너를 시작 합니다. 수정 하 고 다음 예제는 hello를 사용 하 여:

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -e WSID="your workspace id" -e KEY="your key" -h=`hostname` -p 127.0.0.1:25225:25225 --name="omsagent" --restart=always microsoft/oms
```

### <a name="for-all-azure-government-linux-container-hosts-including-coreos"></a>CoreOS를 포함한 모든 Azure Government Linux 컨테이너 호스트의 경우

원하는 toomonitor hello OMS 컨테이너를 시작 합니다. 수정 하 고 다음 예제는 hello를 사용 하 여:

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/log:/var/log -e WSID="your workspace id" -e KEY="your key" -e DOMAIN="opinsights.azure.us" -p 127.0.0.1:25225:25225 -p 127.0.0.1:25224:25224/udp --name="omsagent" -h=`hostname` --restart=always microsoft/oms
```

### <a name="switching-from-using-an-installed-linux-agent-tooone-in-a-container"></a>컨테이너에는 설치 된 Linux 에이전트 tooone를 사용 하 여에서 전환
이전에 에이전트를 직접 설치 하는 hello를 사용 하 고 원하는 경우 tooinstead 컨테이너에서 실행 중인 에이전트를 먼저 사용 하 여 Linux 용 OMS 에이전트 hello를 제거 합니다. 참조 [Linux 용 OMS 에이전트 제거 시 hello](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) toosuccessfully 제거 하는 방법을 toounderstand hello 에이전트입니다.  

### <a name="configure-an-oms-agent-for-docker-swarm"></a>Docker Swarm용 OMS 에이전트 구성

Docker는 Docker Swarm에서 글로벌 서비스 hello OMS 에이전트를 실행할 수 있습니다. 다음 정보 toocreate OMS 에이전트 서비스는 hello를 사용 합니다. OMS 작업 영역 ID와 기본 키 tooinsert 해야합니다.

- Hello 다음 hello 마스터 노드에서 실행 됩니다.

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock  -e WSID="<WORKSPACE ID>" -e KEY="<PRIMARY KEY>" -p 25225:25225 -p 25224:25224/udp  --restart-condition=on-failure microsoft/oms
    ```

### <a name="configure-an-oms-agent-for-red-hat-openshift"></a>Red Hat OpenShift용 OMS 에이전트 구성
세 가지 방법으로 tooadd hello OMS 에이전트 tooRed Hat OpenShift toostart 컨테이너 모니터링 데이터를 수집할 가지가 있습니다.

* [Linux 용 OMS 에이전트 hello 설치](log-analytics-agent-linux.md) 각 OpenShift 노드에서 직접  
* Azure에 있는 각 OpenShift 노드에서 [Log Analytics VM 확장을 사용하도록 설정](log-analytics-azure-vm-extension.md)  
* OpenShift 데몬 집합으로 hello OMS 에이전트를 설치 합니다.  

이 섹션에서는 OpenShift 데몬 집합으로 hello 단계 필요한 tooinstall hello OMS 에이전트를 다룹니다.  

1. Toohello OpenShift 마스터 노드 및 복사 hello yaml 파일 로그온 [ocp omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) GitHub에서 tooyour 노드를 마스터 및 hello 값 OMS 작업 영역 ID와 기본 키를 수정 합니다.
2. OMS에 대 한 hello 명령을 toocreate 다음 프로젝트를 실행 하 고 hello 사용자 계정을 설정 합니다.

    ```
    oadm new-project omslogging --node-selector='zone=default'
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. toodeploy hello 데몬 집합 hello 다음을 실행 합니다.

    `oc create -f ocp-omsagent.yaml`

5. tooverify 구성 되어 있으며 제대로 작동 hello 다음을 입력 합니다.

    `oc describe daemonset omsagent`  

    및 hello 출력와 유사 합니다.

    ```
    [ocpadmin@khm-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

원할 경우 toouse 비밀 toosecure OMS 작업 영역 ID와 기본 키 hello OMS 에이전트 데몬 집합 yaml 파일을 사용 하는 경우 hello 다음 단계를 수행 합니다.

1. Toohello OpenShift 마스터 노드 및 복사 hello yaml 파일 로그온 [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) 및 스크립트를 생성 하는 암호 [ocp secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) GitHub에서 합니다.  이 스크립트는 hello 비밀 yaml 파일 toosecure OMS 작업 영역 ID와 기본 키를 생성 하는 사용자 정보를 분입니다.  
2. OMS에 대 한 hello 명령을 toocreate 다음 프로젝트를 실행 하 고 hello 사용자 계정을 설정 합니다. OMS 작업 영역 ID에 대 한 스크립트를 생성 하는 hello 비밀 요청 <WSID> 와 기본 키 <KEY> 완료 되 면 hello ocp secret.yaml 파일을 만듭니다.  

    ```
    oadm new-project omslogging --node-selector='zone=default'  
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. Hello 다음을 실행 하 여 hello 보안 파일을 배포 합니다.

    `oc create -f ocp-secret.yaml`

5. Hello 다음을 실행 하 여 배포를 확인 합니다.

    `oc describe secret omsagent-secret`  

    및 hello 출력와 유사 합니다.  

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

6. Hello 다음을 실행 하 여 hello OMS 에이전트 데몬 집합 yaml 파일을 배포 합니다.

    `oc create -f ocp-ds-omsagent.yaml`  

7. Hello 다음을 실행 하 여 배포를 확인 합니다.

    `oc describe ds oms`

    및 hello 출력와 유사 합니다.

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe secret omsagent-secret  
    Name:           omsagent-secret  
    Namespace:      omslogging  
    Labels:         <none>  
    Annotations:    <none>  

    Type:   Opaque  

     Data  
     ====  
     KEY:    89 bytes  
     WSID:   37 bytes  
    ```

### <a name="secure-your-secret-information-for-docker-swarm-and-kubernetes"></a>Docker Swarm 및 Kubernetes에 대한 비밀 정보를 보호합니다.

Docker Swarm 및 Kubernetes 컨테이너 서비스에 대한 비밀 OMS 작업 영역 ID 및 기본 키를 보호할 수 있습니다.

#### <a name="secure-secrets-for-docker-swarm"></a>Docker Swarm에 대한 비밀 보호

Docker는 Docker Swarm 작업 영역 ID와 기본 키에 대 한 hello 암호를 만든 후 실행 하면 hello OMSagent 용 hello Docker 서비스를 만듭니다. 다음 정보 toocreate hello 비밀 정보를 사용 합니다.

1. Hello 다음 hello 마스터 노드에서 실행 됩니다.

    ```
    echo "WSID" | docker secret create WSID -
    echo "KEY" | docker secret create KEY -
    ```

2. 비밀이 제대로 생성되었는지 확인합니다.

    ```
    keiko@swarmm-master-13957614-0:/run# sudo docker secret ls
    ```

    ```
    ID                          NAME                CREATED             UPDATED
    j2fj153zxy91j8zbcitnjxjiv   WSID                43 minutes ago      43 minutes ago
    l9rh3n987g9c45zffuxdxetd9   KEY                 38 minutes ago      38 minutes ago
    ```

3. 다음 명령은 toomount hello 비밀 toohello 실행된 hello OMS 에이전트 컨테이너 화 된 합니다.

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock --secret source=WSID,target=WSID --secret source=KEY,target=KEY  -p 25225:25225 -p 25224:25224/udp --restart-condition=on-failure microsoft/oms
    ```

#### <a name="secure-secrets-for-kubernetes-with-yaml-files"></a>yaml 파일로 Kubernetes에 대한 비밀 보호

Kubernetes, 작업 영역 ID와 기본 키에 대 한 스크립트 toogenerate hello 비밀 yaml 파일을 사용 합니다. Hello에 [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) 페이지에 상관 없이 사용자의 비밀 정보를 사용할 수 있는 파일이 있습니다.

- 기본 OMS 에이전트 DaemonSet hello 비밀 정보 (omsagent.yaml)가 없습니다.
- hello OMS 에이전트 DaemonSet yaml 파일 비밀 생성 스크립트 toogenerate hello 비밀 yaml (omsagentsecret.yaml) 파일이 있는 비밀 정보 (omsagent ds secrets.yaml)를 사용합니다.

Toocreate omsagent DaemonSets 상관 없이 암호를 선택할 수 있습니다.

##### <a name="default-omsagent-daemonset-yaml-file-without-secrets"></a>비밀이 없는 기본 OMSagent DaemonSet yaml 파일

- Hello 기본 OMS 에이전트 DaemonSet yaml 파일에 대 한 대체 hello `<WSID>` 및 `<KEY>` tooyour WSID 및 키입니다. Hello 파일 tooyour 마스터 노드 및 실행된 hello 다음 복사 합니다.

    ```
    sudo kubectl create -f omsagent.yaml
    ```

##### <a name="default-omsagent-daemonset-yaml-file-with-secrets"></a>비밀이 있는 기본 OMSagent DaemonSet yaml 파일

1. toouse 비밀 정보를 사용 하 여 OMS 에이전트 DaemonSet hello 비밀을 먼저 만듭니다.
    1. Hello 스크립트 및 비밀 템플릿 파일을 복사 하 고 hello에 있는지 확인 동일한 디렉터리입니다.
        - 비밀 생성 스크립트 - secret-gen.sh
        - 비밀 템플릿 - secret-template.yaml
    2. 다음 예제는 hello 같은 hello 스크립트를 실행 합니다. OMS 작업 영역 ID와 기본 키 hello 스크립트 hello에 대 한 요청에 입력 한 후 hello 스크립트 파일을 만듭니다 비밀 yaml 실행할 수 있도록 합니다.   

        ```
        #> sudo bash ./secret-gen.sh
        ```

    3. Hello 비밀 pod를 hello 다음을 실행 하 여 만듭니다.
        ```
        sudo kubectl create -f omsagentsecret.yaml
        ```

    4. tooverify hello 다음 실행:

        ```
        keiko@ubuntu16-13db:~# sudo kubectl get secrets
        ```

        출력은 다음과 유사합니다.

        ```
        NAME                  TYPE                                  DATA      AGE
        default-token-gvl91   kubernetes.io/service-account-token   3         50d
        omsagent-secret       Opaque                                2         1d
        ```

        ```
        keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
        ```

        출력은 다음과 유사합니다.

        ```
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

    5. ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```을 실행하여 omsagent daemon-set 만들기

2. 해당 hello OMS 에이전트 DaemonSet 실행 중인 비슷한 toohello 다음을 확인 합니다.

    ```
    keiko@ubuntu16-13db:~# sudo kubectl get ds omsagent
    ```

    ```
    NAME       DESIRED   CURRENT   NODE-SELECTOR   AGE
    omsagent   3         3         <none>          1h
    ```


Kubernetes에 대 한 작업 영역 ID와 기본 키에 대 한 스크립트 toogenerate hello 비밀 yaml 파일을 사용 합니다. 다음 예에서는 정보 hello로 사용 하 여 hello [omsagent yaml 파일](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) toosecure 비밀 정보입니다.

```
keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
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

## <a name="windows-container-hosts"></a>Windows 컨테이너 호스트

### <a name="preparation-before-installing-windows-agents"></a>Windows 에이전트 설치 전 준비

Windows를 실행 하는 컴퓨터에 에이전트를 설치 하기 전에 tooconfigure hello Docker 서비스가 필요 합니다. hello 구성은 모니터링에 대 한 hello Windows 에이전트 또는 hello 로그 분석 가상 컴퓨터 확장 toouse hello hello 에이전트 hello Docker 디먼에 원격으로 액세스할 수 있도록 Docker TCP 소켓 및 toocapture 데이터를 허용 합니다.

#### <a name="toostart-docker-and-verify-its-configuration"></a>Docker toostart 하 고 해당 구성을 확인

Windows Server에 대 한 명명 된 파이프 TCP 필요한 단계 tooset 가지가 있습니다.

1. Windows PowerShell에서 TCP 파이프 및 명명된 파이프를 사용하도록 설정합니다.

    ```
    Stop-Service docker
    dockerd --unregister-service
    dockerd --register-service -H npipe:// -H 0.0.0.0:2375  
    Start-Service docker
    ```

2. 명명 된 파이프 및 TCP 파이프에 대 한 hello 구성 파일을 사용 하 여 Docker를 구성 합니다. hello 구성 파일은 C:\ProgramData\docker\config\daemon.json에 있습니다.

    Hello daemon.json 파일에 hello 다음이 필요 합니다.

    ```
    {
    "hosts": ["tcp://0.0.0.0:2375", "npipe://"]
    }
    ```

Windows 컨테이너와 함께 사용 하는 hello Docker 디먼 구성에 대 한 자세한 내용은 참조 [Windows에서 Docker 엔진](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon)합니다.


### <a name="install-windows-agents"></a>Windows 에이전트 설치

Windows tooenable 및 모니터링, Hyper-v 컨테이너는 컨테이너 호스트 하는 Windows 컴퓨터에서 Microsoft Monitoring Agent (MMA) hello를 설치 합니다. 온-프레미스 환경에서 Windows를 실행 하는 컴퓨터에 대 한 참조 [연결 Windows 컴퓨터 tooLog 분석](log-analytics-windows-agents.md)합니다. 가상 컴퓨터에 대 한 Azure에서 실행에 연결 분석 tooLog hello를 사용 하 여 [가상 컴퓨터 확장](log-analytics-azure-vm-extension.md)합니다.

Service Fabric에서 실행 중인 Windows 컨테이너를 모니터링할 수 있습니다. 그러나 [Azure에서 실행 중인 가상 컴퓨터](log-analytics-azure-vm-extension.md) 및 [온-프레미스 환경에서 Windows를 실행하는 컴퓨터](log-analytics-windows-agents.md)만 현재 Service Fabric에 대해 지원됩니다.

Windows에 대 한 해당 hello 솔루션 컨테이너 모니터링이 올바르게 설정 되어 확인할 수 있습니다. 에 대 한 확인 여부에 관계 없이 hello 관리 팩 다운로드 제대로 toocheck *ContainerManagement.xxx*합니다. hello 파일 hello C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs 폴더에 있어야 합니다.


## <a name="solution-components"></a>솔루션 구성 요소

Windows 에이전트를 사용 하는 경우 다음 hello 다음 관리 팩은 각 컴퓨터에 설치 에이전트가이 솔루션을 추가 합니다. 구성 또는 유지 관리 없습니다 hello 관리 팩에 대 한 필수입니다.

- C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs에 설치된 *ContainerManagement.xxx*

## <a name="container-data-collection-details"></a>컨테이너 데이터 컬렉션 세부 정보
컨테이너 모니터링 솔루션 hello 컨테이너 호스트 및 사용 하도록 설정 하면 에이전트를 사용 하 여 컨테이너에서 다양 한 성능 메트릭 및 로그 데이터를 수집 합니다.

데이터 수집 3 분 마다 에이전트 유형만 hello 합니다.

- [OMS Agent for Linux](log-analytics-linux-agents.md)
- [Windows 에이전트](log-analytics-windows-agents.md)
- [Log Analytics VM 확장](log-analytics-azure-vm-extension.md)


### <a name="container-records"></a>컨테이너 레코드

hello 다음 표에서 hello 컨테이너 모니터링 솔루션 및 로그 검색 결과에 표시 되는 hello 데이터 형식에 의해 수집 된 레코드입니다.

| 데이터 형식 | 로그 검색의 데이터 유형 | 필드 |
| --- | --- | --- |
| 호스트 및 컨테이너에 대한 성능 | `Type=Perf` | 컴퓨터, ObjectName, CounterName &#40;%프로세서 시간, 디스크 읽기 MB, 디스크 쓰기 MB, 메모리 사용 MB, 네트워크 수신 바이트, 네트워크 송신 바이트, 프로세서 사용 초, 네트워크&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem |
| 컨테이너 인벤토리 | `Type=ContainerInventory` | TimeGenerated, 컴퓨터, 컨테이너 이름, ContainerHostname, 이미지, ImageTag, ContainerState, ExitCode, EnvironmentVar, 명령, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID |
| 컨테이너 이미지 인벤토리 | `Type=ContainerImageInventory` | TimeGenerated, 컴퓨터, 이미지, ImageTag, ImageSize, VirtualSize, 실행 중, 일시 중지됨, 중지됨, 실패, SourceSystem, ImageID, TotalContainer |
| 컨테이너 로그 | `Type=ContainerLog` | TimeGenerated, 컴퓨터, 이미지 ID, 컨테이너 이름, LogEntrySource, LogEntry, SourceSystem, ContainerID |
| 컨테이너 서비스 로그 | `Type=ContainerServiceLog`  | TimeGenerated, 컴퓨터, TimeOfCommand, 이미지, 명령, SourceSystem, ContainerID |
| 컨테이너 노드 인벤토리 | `Type=ContainerNodeInventory_CL`| TimeGenerated, 컴퓨터, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem|
| Kubernetes 인벤토리 | `Type=KubePodInventory_CL` | TimeGenerated, 컴퓨터, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem |
| 컨테이너 프로세스 | `Type=ContainerProcess_CL` | TimeGenerated, 컴퓨터, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem |
| kubernetes 이벤트 | `Type=KubeEvents_CL` | TimeGenerated, 컴퓨터, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, 메시지 |

레이블 추가 너무*PodLabel* 데이터 유형은 사용자 지정 레이블을 합니다. hello hello 테이블에 표시 되는 추가 된 PodLabel 레이블을 예입니다. 따라서 `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s`는 사용자 환경의 데이터 집합에 따라 달라지며 일반적으로 `PodLabel_yourlabel_s`와 비슷합니다.


## <a name="monitor-containers"></a>모니터 컨테이너
Hello OMS 포털에서 사용 하도록 설정 하는 hello 솔루션을 사용 하는 다음 hello **컨테이너** 타일 컨테이너 호스트와 호스트에서 실행 되는 hello 컨테이너에 대 한 요약 정보가 표시 됩니다.

![컨테이너 타일](./media/log-analytics-containers/containers-title.png)

hello 타일 실행 중 또는 중지 된 hello 환경 및 실패 하는 여부에 있는 개수 컨테이너의 개요를 보여 줍니다.

### <a name="using-hello-containers-dashboard"></a>Hello 컨테이너 대시보드를 사용 하 여
Hello 클릭 **컨테이너** 바둑판식으로 배열입니다. 여기에서는 다음에 따라 구성된 보기를 확인할 수 있습니다.

- **컨테이너 이벤트** - 컨테이너 상태 및 실패한 컨테이너가 있는 컴퓨터를 보여 줍니다.
- **컨테이너 로그** -로그 파일의 가장 높은 수 hello 사용 하 여 시간에 따른 컴퓨터의 목록을 생성 하는 컨테이너 로그 파일의 차트를 보여 줍니다.
- **Kubernetes 이벤트** -시간 hello 원인은 포드 hello 이벤트를 생성 하는 원인에 따라 생성 된 Kubernetes 이벤트의 차트를 보여 줍니다. *이 데이터 집합은 Linux 환경에만 사용됩니다.*
- **Kubernetes Namespace 인벤토리** -네임 스페이스 및 포드 hello 수를 표시 하 고 해당 계층을 보여 줍니다. *이 데이터 집합은 Linux 환경에만 사용됩니다.*
- **컨테이너 노드 인벤토리** -컨테이너 노드/호스트에서 사용 되는 오케스트레이션 형식의 hello 수를 보여 줍니다. 컨테이너의 hello 번호로 hello 컴퓨터 노드/호스트도 나열 됩니다. *이 데이터 집합은 Linux 환경에만 사용됩니다.*
- **컨테이너 이미지 인벤토리** -hello 사용 되는 컨테이너 이미지의 총 수와 이미지 형식의 수를 표시 합니다. 이미지의 hello 수 hello 이미지 태그로 나열 됩니다.
- **컨테이너 상태** -노드/호스트 컴퓨터를 실행 중인 컨테이너 hello 컨테이너의 총 수를 보여 줍니다. 호스트를 실행 중인 hello 번호로 컴퓨터도 나열 됩니다.
- **컨테이너 프로세스** - 시간에 따른 실행 중인 컨테이너 프로세스의 꺾은선형 차트를 보여 줍니다. 컨테이너는 컨테이너 내 실행 중인 명령/프로세스를 기준으로 나열됩니다. *이 데이터 집합은 Linux 환경에만 사용됩니다.*
- **컨테이너 CPU 성능** -hello 컴퓨터 노드/호스트에 대 한 시간에 따라 평균 CPU 사용률의 꺾은선형 차트를 보여 줍니다. 또한 목록 hello 컴퓨터 노드/호스트 기반 평균 CPU 사용률입니다.
- **컨테이너 메모리 성능** - 시간에 따른 메모리 사용량의 꺾은선형 차트를 보여 줍니다. 또한 인스턴스 이름을 기준으로 컴퓨터 메모리 사용률을 나열합니다.
- **컴퓨터 성능** -시간대 시간에 따른 CPU 성능의 hello % 꺾은선형 차트의 여유 디스크 공간이 메가바이트 고 시간에 따라 메모리 사용 백분율을 표시 합니다. 자세한 내용을 보려면 차트 tooview에서 해당 줄 위로 가져가면 수 있습니다.


Hello 대시보드의 각 영역에 수집 된 데이터에서 실행 되는 검색의 시각적 표현입니다.

![컨테이너 대시보드 ](./media/log-analytics-containers/containers-dash01.png)

![컨테이너 대시보드 ](./media/log-analytics-containers/containers-dash02.png)

Hello에 **컨테이너 상태** 영역에서 아래와 같이 hello 위쪽 영역을 클릭 합니다.

![컨테이너 상태](./media/log-analytics-containers/containers-status.png)

사용자 컨테이너의 hello 상태에 관한 정보 표시 로그 검색이 열립니다.

![컨테이너에 대한 로그 검색](./media/log-analytics-containers/containers-log-search.png)

여기에서는 hello 검색 쿼리 toomodify를 편집할 수 있습니다이 toofind hello 특정 정보에 관심이 있습니다. 로그 검색에 대한 자세한 내용은 [Log Analytics의 로그 검색](log-analytics-log-searches.md)을 참조하세요.

## <a name="troubleshoot-by-finding-a-failed-container"></a>실패한 컨테이너를 검색하여 문제 해결

0이 아닌 종료 코드로 종료된 경우 Log Analytics는 이 컨테이너를 **Failed**로 표시합니다. Hello 오류 및 실패 hello에 hello 환경에 대 한 개요를 확인할 수 있습니다 **실패 컨테이너** 영역입니다.

### <a name="toofind-failed-containers"></a>toofind 컨테이너를 실패 했습니다.
1. Hello 클릭 **컨테이너 상태** 영역입니다.  
   ![컨테이너 상태](./media/log-analytics-containers/containers-status.png)
2. 로그 검색 열리고 다음 유사한 toohello 컨테이너의 hello 상태가 표시 됩니다.  
   ![컨테이너 상태](./media/log-analytics-containers/containers-log-search.png)
3. 다음으로 실패 한 컨테이너 tooview 추가 정보의 hello 집계 값을 클릭 합니다. 확장 **자세히 표시** tooview hello 이미지 id입니다.  
   ![실패한 컨테이너](./media/log-analytics-containers/containers-state-failed.png)  
4. 그런 다음 hello 검색 쿼리에서 hello 다음을 입력 합니다. `Type=ContainerInventory <ImageID>`중지 되 고 실패 한 이미지의 이미지 크기와 수 같은 hello 이미지에 대 한 세부 정보를 toosee 합니다.  
   ![실패한 컨테이너](./media/log-analytics-containers/containers-failed04.png)

## <a name="search-logs-for-container-data"></a>컨테이너 데이터에 대한 로그 검색
특정 오류 문제를 해결 하는 경우 사용자 환경에서 발생 하는 toosee를 유용 합니다. 로그 유형만 hello는 원하는 tooreturn hello 정보 쿼리를 작성 하는 데 도움이 됩니다.


- **ContainerImageInventory** – 이미지 Id 또는 크기와 같은 이미지와 tooview 이미지 정보로 구성 된 toofind 정보를 시도 하는 경우이 유형을 사용 합니다.
- **ContainerInventory** – 컨테이너 위치, 해당 컨테이너 이름, 실행 중인 이미지에 대한 정보가 필요할 때 이 유형을 사용합니다.
- **ContainerLog** – toofind 특정 오류 로그 정보 및 항목을 원하는 경우이 유형을 사용 합니다.
- **ContainerNodeInventory_CL** 이 유형을 사용 호스트/노드에 대 한 hello 정보를 원하는 컨테이너 있는 됩니다. Docker 버전, 오케스트레이션 형식, 저장소 및 네트워크 정보를 제공합니다.
- **ContainerProcess_CL** 사용 하 여가 형식 tooquickly hello 컨테이너 내에서 실행 하는 hello 프로세스를 참조 하십시오.
- **ContainerServiceLog** – hello Docker 디먼을 시작, 예: 중지, 삭제 또는 끌어오기 명령에 대 한 toofind 감사 추적 정보를 시도 하는 경우이 유형을 사용 합니다.
- **KubeEvents_CL** 이 형식의 toosee hello Kubernetes 이벤트를 사용 합니다.
- **KubePodInventory_CL** toounderstand hello 클러스터 계층 구조 정보를 원하는 경우이 유형을 사용 합니다.


### <a name="toosearch-logs-for-container-data"></a>컨테이너 데이터에 대 한 toosearch 로그
* 사용자가 알고 있는 이미지 최근에 실패 했습니다 및 hello 오류 로그에 대 한 찾기 선택 합니다. **ContainerInventory** 검색을 통해 해당 이미지를 실행 중인 컨테이너 이름부터 찾습니다. 예를 들어, `Type=ContainerInventory ubuntu Failed`를 검색합니다.  
    ![Ubuntu 컨테이너에 대한 검색](./media/log-analytics-containers/search-ubuntu.png)

  hello 컨테이너의 이름 옆 너무 hello**이름**, 이러한 로그를 검색 합니다. 이 예제에서는 `Type=ContainerLog cranky_stonebreaker`입니다.

**성능 정보 보기**

Tooconstruct 쿼리를 시작 하는 경우 손쉽게 toosee 먼저 가능한 것입니다. 예를 들어 toosee 모든 성능 데이터, 시도 광범위 한 쿼리를 입력 하 여 hello 다음 검색 쿼리.

```
Type=Perf
```

![컨테이너 성능](./media/log-analytics-containers/containers-perf01.png)

표시 되는 tooa 특정 컨테이너의 hello 이름을 입력 하 여 쿼리의 오른쪽 toohello hello 성능 데이터 범위를 지정할 수 있습니다.

```
Type=Perf <containerName>
```

개별 컨테이너에 대해 수집 되는 성능 메트릭에 hello 목록을 표시를 합니다.

![컨테이너 성능](./media/log-analytics-containers/containers-perf03.png)

## <a name="example-log-search-queries"></a>로그 검색 쿼리 예제
종종 유용한 toobuild 사용자 환경 또는 예 2부터 다음 toofit 수정 쿼리 합니다. 시작 지점으로 hello로 실험 **샘플 쿼리** 영역 toohelp 보다 고급 수준의 쿼리를 작성 합니다.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![컨테이너 쿼리](./media/log-analytics-containers/containers-queries.png)


## <a name="saving-log-search-queries"></a>로그 검색 쿼리 저장
쿼리 저장은 Log Analytics의 표준 기능입니다. 이를 저장해 두면 향후 유용하게 사용할 수 있습니다.

유용한 쿼리를 만든 후 클릭 하 여 저장 **즐겨찾기** hello hello 로그 검색 페이지 위쪽에 있습니다. 쉽게 액세스할 수 나중 hello에서 다음 **내 대시보드** 페이지.

## <a name="next-steps"></a>다음 단계
* [로그 검색](log-analytics-log-searches.md) tooview 컨테이너 데이터 레코드를 자세히 설명 합니다.
