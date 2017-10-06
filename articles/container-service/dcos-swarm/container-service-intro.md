---
title: "Azure 클라우드에서 aaaDocker 컨테이너 호스팅 | Microsoft Docs"
description: "Azure 컨테이너 서비스 방식으로 toosimplify hello 만들기, 구성 및 관리는 미리 구성 된 toorun 컨테이너 화 가능한 응용 프로그램이 있는 가상 컴퓨터의 클러스터를 제공 합니다."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로 서비스, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: rogardle
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 46a0071a7497a3ff44d75413b49f1d06f844c446
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toodocker-container-hosting-solutions-with-azure-container-service"></a>Azure 컨테이너 서비스를 사용 하 여 솔루션을 호스팅 소개 tooDocker 컨테이너 
Azure 컨테이너 서비스 간단 하 게 드립니다 toocreate 구성 하 고 미리 구성 된 toorun 컨테이너 화 가능한 응용 프로그램이 있는 가상 컴퓨터의 클러스터를 관리 합니다. Azure 컨테이너 서비스는 일반적인 오픈 소스 예약 및 오케스트레이션 도구의 최적화된 구성을 사용합니다. Toouse 있습니다를 통해 기존 기술을 사용 하면이 커뮤니티 전문, toodeploy 크기가 크고 점점 본문에 대해 하 고 Microsoft Azure에서 컨테이너 기반 응용 프로그램을 관리 합니다.

![Azure 컨테이너 서비스를 통해 toomanage 컨테이너 화 가능한 응용 프로그램 Azure에서 여러 호스트에 있습니다.](./media/acs-intro/acs-cluster-new.png)

Azure 컨테이너 서비스는 hello Docker 컨테이너 형식 tooensure 응용 프로그램 컨테이너가 완전히 이식 가능를 활용 합니다. 또한 컨테이너의 이러한 응용 프로그램 toothousands 또는 짝수 수만 확장할 수 있도록 선택 하는 풀 마라톤 및 DC/OS, docker는 Docker Swarm 또는 Kubernetes 지원 합니다.

Azure 컨테이너 서비스를 사용 하면 응용 프로그램 이식성-hello 오케스트레이션 계층에서 이식성을 포함 하 여 그대로 유지 하면서 Azure의 엔터프라이즈급 기능을 걸릴 수 있습니다.

## <a name="using-azure-container-service"></a>Azure 컨테이너 서비스 사용
Azure 컨테이너 서비스와 이러한 목표는 오픈 소스 도구와 기술을 담아 고객 사이에서 인기 오늘을 통해 tooprovide 컨테이너 호스팅 환경입니다. toothis 끝 (DC/OS, docker는 Docker Swarm 또는 Kubernetes) 하 여 선택한 orchestrator에 대 한 hello 표준 API 끝점 공개 했습니다. 이러한 끝점을 사용 하 여 toothose 끝점 통신의 대상이 될 수 있는 모든 소프트웨어를 활용할 수 있습니다. 예를 들어 hello docker는 Docker Swarm 끝점의 경우 hello toouse hello Docker CLI (명령줄 인터페이스)를 선택할 수 있습니다. DC/OS 용 hello DCOS CLI를 선택할 수 있습니다. Kubernetes의 경우 `kubectl`을 선택할 수 있습니다.

## <a name="creating-a-docker-cluster-by-using-azure-container-service"></a>Azure 컨테이너 서비스를 사용하여 Docker 클러스터 만들기
Azure 컨테이너 서비스를 사용 하 여 toobegin hello 포털을 통해 Azure 컨테이너 서비스 클러스터를 배포할 (마켓플레이스 검색 hello에 대 한 **Azure 컨테이너 서비스**), Azure 리소스 관리자 템플릿을 사용 하 여 ([Docker Swarm](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm), [DC/OS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), 또는 [Kubernetes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)), 또는 hello로 [Azure CLI 2.0](container-service-create-acs-cluster-cli.md)합니다. hello 제공 퀵 스타트 서식 파일 수정된 tooinclude 추가 또는 고급 Azure 구성 될 수 있습니다. 자세한 내용은 [Azure Container Service 클러스터 배포](container-service-deployment.md)를 참조하세요.

## <a name="deploying-an-application"></a>응용 프로그램 배포
Azure Container Service는 오케스트레이션을 위해 Docker Swarm, DC/OS 또는 Kubernetes 옵션을 제공합니다. 응용 프로그램을 배포하는 방법은 선택한 Orchestrator에 따라 달라집니다.

### <a name="using-dcos"></a>DC/OS 사용
DC/OS는 hello Apache Mesos 분산된 시스템 커널 기반 운영 체제를 배포 합니다. Apache Mesos hello Apache 소프트웨어 Foundation에 있는 컴퓨터의 목록과 hello 중 일부 [에서 가장 큰 이름을 IT](http://mesos.apache.org/documentation/latest/powered-by-mesos/) 사용자 및 참가자입니다.

![에이전트 및 마스터가 표시된 DC/OS에 대해 구성된 Azure Container Service.](media/acs-intro/dcos.png)

DC/OS 및 Apache Mesos는 다음과 같은 인상적인 기능 집합을 포함합니다.

* 입증된 확장성
* Apache ZooKeeper를 사용하는 내결함성 있는 복제된 마스터 및 슬레이브
* Docker 형식의 컨테이너에 대한 지원
* Linux 컨테이너를 사용하여 작업 간에 네이티브 격리
* 다중 리소스 예약(메모리, CPU, 디스크 및 포트)
* 새로운 병렬 응용 프로그램을 개발하기 위한 Java, Python 및 C++ API
* 클러스터 상태를 볼 수 있는 웹 UI

Azure 컨테이너 서비스에서 실행 중인 DC/OS는 기본적으로 작업을 예약 하기 위한 hello 마라톤 오케스트레이션 플랫폼을 포함 됩니다. 그러나 hello ACS의 DC/OS 배포에 포함 된 hello Mesosphere Universe tooyour 서비스를 추가할 수 있는 서비스입니다. Hello Universe에서에서 서비스에는 Spark, Hadoop, Cassandra, 및 등 포함 됩니다.

![Azure 컨테이너 서비스의 DC/OS Universe](media/dcos/universe.png)

#### <a name="using-marathon"></a>Marathon 사용
풀 마라톤은 클러스터 전체 init 및 cgroups-또는 hello 경우 Docker로 포맷 된 컨테이너 Azure 컨테이너 서비스의 서비스 제어 시스템입니다. Marathon은 응용 프로그램을 배포할 수 있는 웹 UI를 제공합니다. 사용자는 배포 시 DNS\_PREFIX 및 REGION이 모두 정의된 `http://DNS_PREFIX.REGION.cloudapp.azure.com`과 유사한 URL에서 웹 UI에 액세스할 수 있습니다. 물론, 사용자는 자체 DNS 이름을 제공할 수도 있습니다. Hello 마라톤 웹 UI를 사용 하 여 컨테이너의 실행에 대 한 자세한 내용은 참조 하십시오. [hello 마라톤 웹 UI 통해 DC/OS 컨테이너 관리](container-service-mesos-marathon-ui.md)합니다.

![Marathon 응용 프로그램 목록](media/dcos/marathon-applications-list.png)

또한 풀 마라톤와 통신 하기 위한 hello REST Api를 사용할 수 있습니다. 각 도구에 사용할 수 있는 여러 클라이언트 라이브러리가 있습니다. 다양 한 언어-를 포함 하 고 물론, 모든 언어에서 hello HTTP 프로토콜을 사용할 수 있습니다. 또한 인기 있는 다양한 DevOps 도구는 Marathon에 대한 지원을 제공합니다. Azure 컨테이너 서비스 클러스터를 사용하여 작업하는 경우 운영 팀에 최대의 유연성을 제공합니다. Hello 마라톤 REST API를 사용 하 여 컨테이너의 실행에 대 한 자세한 내용은 참조 하십시오. [hello 마라톤 REST API를 통해 DC/OS 컨테이너 관리](container-service-mesos-marathon-rest.md)합니다.

### <a name="using-docker-swarm"></a>Docker Swarm 사용
Docker Swarm은 Docker에 대한 네이티브 클러스터링을 제공합니다. Docker는 Docker Swarm 사용 되므로 표준 Docker API hello, 이미 Docker 디먼을와 통신 하는 모든 도구 Azure 컨테이너 서비스에서 웜 tootransparently 눈금 toomultiple 호스트를 사용할 수 있습니다.

![Azure 컨테이너 서비스 toouse 웜을 구성합니다.](media/acs-intro/acs-swarm2.png)

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

웜 클러스터에서 컨테이너 관리를 위한 지원 되는 도구를 포함 하지만 hello 다음으로 제한 되지 않습니다.

* Dokku
* Docker CLI 및 Docker Compose
* Krane
* Jenkins

### <a name="using-kubernetes"></a>Kubernetes 사용
Kubernetes는 인기 있는 프로덕션급 오픈 소스 컨테이너 오케스트레이터 도구입니다. Kubernetes는 컨테이너화된 응용 프로그램의 배포, 크기 조정 및 관리를 자동화합니다. 있기 때문에 오픈 소스 솔루션 hello 오픈 소스 커뮤니티를 통해 생성, Azure 컨테이너 서비스에 원활 하 게 실행 되며 Azure 컨테이너 서비스에서 크기 조정에 사용 되는 toodeploy 컨테이너 될 수 있습니다.

![Azure 컨테이너 서비스 toouse Kubernetes를 구성합니다.](media/acs-intro/kubernetes.png)

여기에는 다음과 같이 풍부한 기능들이 포함되어 있습니다.
* 수평적 크기 조정
* 서비스 검색 및 부하 분산
* 비밀 및 구성 관리
* API 기반 자동화된 롤아웃 및 롤백
* 자동 복구

## <a name="videos"></a>비디오
Azure Container Service 시작(101):  

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Container-Service-101/player]
>
>

구성 응용 프로그램에서 사용 하 여 hello Azure 컨테이너 서비스 (빌드 2016)

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/B822/player]
>
>

## <a name="next-steps"></a>다음 단계

Hello를 사용 하 여 컨테이너 서비스 클러스터 배포 [포털](container-service-deployment.md) 또는 [Azure CLI 2.0](container-service-create-acs-cluster-cli.md)합니다.
