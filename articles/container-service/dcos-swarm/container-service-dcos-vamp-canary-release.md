---
title: "Azure DC/OS 클러스터에서 Vamp로 aaaCanary 버전 | Microsoft Docs"
description: "Toouse는 toocanary 릴리스 서비스 Vamp 하 고 스마트 트래픽 Azure 컨테이너 서비스 DC/OS 클러스터에서 필터링을 적용 하는 방법"
services: container-service
author: gggina
manager: rasquill
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/17/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: e7b8658a161a7cddcf718e3e1c12a889a330d3d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="canary-release-microservices-with-vamp-on-an-azure-container-service-dcos-cluster"></a>Azure Container Service DC/OS 클러스터에서 Vamp를 사용하여 마이크로 서비스 카나리아 릴리스

이 연습에서는 DC/OS 클러스터를 사용하여 Azure Container Service에 Vamp를 설정합니다. 카나리아 म hello Vamp 데모 서비스 "sava" 놓은 다음 스마트 트래픽 필터링을 적용 하 여 hello 서비스 Firefox와의 비 호환성을 해결 합니다. 

> [!TIP] 
> 이 연습에서 Vamp DC/OS 클러스터에서 실행 되지만 hello 조정자로 Kubernetes와 Vamp을 사용할 수도 있습니다.
>

## <a name="about-canary-releases-and-vamp"></a>카나리아 릴리스 및 Vamp에 대한 정보


[카나리아 릴리스](https://martinfowler.com/bliki/CanaryRelease.html)란 Netflix, Facebook, Spotify 등의 혁신적인 조직에서 채택한 영리한 배포 전략입니다. 문제를 줄이고, 안전망을 도입하고, 혁신을 가속화하는 합리적인 방법입니다. 그렇다면 왜 모든 회사에서 이 방법을 사용하지 않을까요? CI/CD 파이프라인 tooinclude 카나리아 전략 확장 복잡성을 추가 하 고 광범위 한 devops 지식 및 전문 필요 합니다. 도 시작 가져오기 전에 충분 한 tooblock 작은 회사 및 기업 유사 합니다. 

[Vamp](http://vamp.io/) 카나리아 해제 기능 tooyour 기본 컨테이너 스케줄러 전환한은 설계 된 오픈 소스 시스템 tooease이이 전환 합니다. Vamp의 카나리아 기능은 백분율 기반 롤아웃보다 우수합니다. 트래픽 필터링 하 고 다양 한 조건에서 예를 들어 tootarget 특정 사용자, IP 범위 또는 장치에 따라 분할 합니다. Vamp는 성능 메트릭을 추적 및 분석하여 실제 데이터를 기반으로 자동화가 가능합니다. 오류 발생 시 자동으로 롤백하도록 설정하거나 부하 또는 대기 시간에 따라 개별 서비스 변형의 규모를 조정할 수 있습니다.

## <a name="set-up-azure-container-service-with-dcos"></a>DC/OS를 사용하여 Azure Container Service 설정



1. 마스터 하나와 기본 크기의 에이전트 두 개가 있는 [DC/OS 클러스터를 배포](container-service-deployment.md)합니다. 

2. [SSH 터널을 만들어](../container-service-connect.md) tooconnect toohello DC/OS 클러스터입니다. 이 문서에서는 로컬 포트 80에서 toohello 클러스터 터널을 가정 합니다.


## <a name="set-up-vamp"></a>Vamp 설치

실행 중인 DC/OS 클러스터를가지고 Vamp hello DC/OS UI (http://localhost:80)에서 설치할 수 있습니다. 

![DC/OS UI](./media/container-service-dcos-vamp-canary-release/01_set_up_vamp.png)

설치는 두 단계로 수행됩니다.

1. **Elasticsearch를 배포**합니다.

2. 그런 다음 **Vamp 배포** hello Vamp DC/OS universe 패키지를 설치 하 여 합니다.

### <a name="deploy-elasticsearch"></a>Elasticsearch 배포

Vamp는 메트릭 수집 및 집계에 사용할 Elasticsearch가 필요합니다. Hello를 사용할 수 있습니다 [magneticio Docker images](https://hub.docker.com/r/magneticio/elastic/) toodeploy 호환 Vamp Elasticsearch 스택 합니다.

1. DC/OS UI hello에서 이동 너무**서비스** 클릭 **서비스 배포**합니다.

2. 선택 **JSON 모드** hello에서 **새 서비스 배포** 팝업 합니다.

  ![JSON 모드 선택](./media/container-service-dcos-vamp-canary-release/02_deploy_service_json_mode.png)

3. 다음 JSON hello에 붙여 넣습니다. 이 구성은 1GB의 RAM 및 hello Elasticsearch 포트에는 기본적인 상태 검사를 hello 컨테이너를 실행합니다.
  
  ```JSON
  {
    "id": "elasticsearch",
    "instances": 1,
    "cpus": 0.2,
    "mem": 1024.0,
    "container": {
      "docker": {
        "image": "magneticio/elastic:2.2",
        "network": "HOST",
        "forcePullImage": true
      }
    },
    "healthChecks": [
      {
        "protocol": "TCP",
        "gracePeriodSeconds": 30,
        "intervalSeconds": 10,
        "timeoutSeconds": 5,
        "port": 9200,
        "maxConsecutiveFailures": 0
      }
    ]
  }
  ```
  

3. **배포**를 클릭합니다.

  DC/OS hello Elasticsearch 컨테이너를 배포합니다. Hello에 진행률을 추적할 수 **서비스** 페이지.  

  ![Elasticsearch 배포](./media/container-service-dcos-vamp-canary-release/03_deply_elasticsearch.png)

### <a name="deploy-vamp"></a>Vamp 배포

Elasticsearch로 보고 되 면 **실행**, hello DC/OS Universe Vamp 패키지를 추가할 수 있습니다. 

1. 너무 이동**Universe** 검색 한 **vamp**합니다. 
  ![DC/OS universe의 Vamp](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)

2. 클릭 **설치** 다음 toohello vamp 패키지를 선택 하 고 **고급 설치**합니다.

3. 아래로 스크롤하여 hello elasticsearch url 입력: `http://elasticsearch.marathon.mesos:9200`합니다. 

  ![Elasticsearch URL 입력](./media/container-service-dcos-vamp-canary-release/05_universe_elasticsearch_url.png)

4. 클릭 **검토 하 고 설치**, 클릭 **설치** toostart hello 배포 합니다.  

  DC/OS가 모든 필수 Vamp 구성 요소를 배포합니다. Hello에 진행률을 추적할 수 **서비스** 페이지.
  
  ![universe 패키지로 Vamp 배포](./media/container-service-dcos-vamp-canary-release/06_deploy_vamp.png)
  
5. 배포가 완료 되 면 hello Vamp UI를 액세스할 수 있습니다.

  ![DC/OS의 Vamp 서비스](./media/container-service-dcos-vamp-canary-release/07_deploy_vamp_complete.png)
  
  ![Vamp UI](./media/container-service-dcos-vamp-canary-release/08_vamp_ui.png)


## <a name="deploy-your-first-service"></a>첫 번째 서비스 배포

Vamp가 실행 중이니, 청사진의 서비스를 배포합니다. 

가장 간단한 형태의 [Vamp 청사진](http://vamp.io/documentation/using-vamp/blueprints/) hello 끝점 (게이트웨이), 클러스터 및 toodeploy 서비스에 설명 합니다. 사용 하 여 클러스터 toogroup hello 동일 카나리아 해제, A에 대 한 논리적 그룹으로 서비스의 여러 변형이 vamp / B 테스트 합니다.  

이 시나리오에서는 [**sava**](https://github.com/magneticio/sava)라고 하는 샘플 모놀리식 응용 프로그램을 사용하며 버전은 1.0입니다. hello monolith magneticio/sava:1.0.0 아래 Docker 허브에 있는 Docker 컨테이너에 패키지 됩니다. 포트 8080에서 hello 응용 프로그램을 정상적으로 실행 되지만 있습니다 tooexpose 아래 포트 9050이 경우. 간단한 청사진을 사용 하 여 Vamp 통해 hello 응용 프로그램을 배포 합니다.

1. 너무 이동**배포**합니다.

2. **추가**를 클릭합니다.

3. 붙여넣기를 수행 하는 hello에 YAML 세부 계획 합니다. 이 청사진에는 서비스 변형이 하나뿐인 클러스터가 하나 포함되어 있으며 이후 단계에서 변경할 것입니다.

  ```YAML
  name: sava                        # deployment name
  gateways:
    9050: sava_cluster/webport      # stable endpoint
  clusters:
    sava_cluster:               # cluster toocreate
     services:
        -
          breed:
            name: sava:1.0.0        # service variant name
            deployable: magneticio/sava:1.0.0
            ports:
              webport: 8080/http # cluster endpoint, used for canary releasing
  ```

4. **Save**를 클릭합니다. Vamp은 hello 배포를 시작합니다.

hello 배포 hello에 나열 되어 **배포** 페이지. Hello 배포 toomonitor의 상태를 클릭 합니다.

![Vamp UI - sava 배포](./media/container-service-dcos-vamp-canary-release/09_sava100.png)

![Vamp UI의 sava 서비스](./media/container-service-dcos-vamp-canary-release/09a_sava100.png)

Hello에 나열 되는 두 게이트웨이 생성 됩니다 **게이트웨이** 페이지:

* (포트 9050) 서비스를 실행 하는 안정적인 끝점 tooaccess hello 
* Vamp가 관리하는 내부 게이트웨이(이 게이트웨이는 나중에 자세히 설명). 

![Vamp UI - sava 게이트웨이](./media/container-service-dcos-vamp-canary-release/10_vamp_sava_gateways.png)

hello sava 서비스가 이제 배포 있지만 hello Azure 부하 분산 장치는 아직 tooforward 트래픽 tooit를 인식 하지 때문에 외부에서 액세스할 수 없습니다. tooaccess hello 서비스 업데이트 hello Azure 네트워킹 구성입니다.


## <a name="update-hello-azure-network-configuration"></a>Hello Azure 네트워크 구성을 업데이트합니다

Vamp 배포 된 hello sava 서비스 노드에서 hello DC/OS 에이전트 9050 포트에서 안정적인 끝점을 노출 합니다. 외부 hello DC/OS 클러스터에서 tooaccess hello 서비스 같은 클러스터 배포에서 변경 내용을 toohello Azure 네트워크 구성이 hello를 확인 합니다. 

1. **Hello Azure 부하 분산 장치 구성** hello 에이전트에 대 한 (라는 리소스 hello **에이전트 lb xxxx dcos**) 상태 검색 및 포트 9050 toohello sava 인스턴스에서 규칙 tooforward 트래픽입니다. 

2. **업데이트 hello 네트워크 보안 그룹** hello 공용 에이전트에 대 한 (라는 리소스 hello **XXXX 에이전트-public이-nsg-XXXX**) 포트 9050 tooallow 트래픽을 합니다.

자세한 단계 toocomplete에 대 한 이러한 작업을 사용 하 여 hello Azure 포털에서 참조 [공용 액세스 tooan Azure 컨테이너 서비스 응용 프로그램 활성화](container-service-enable-public-access.md)합니다. 모든 포트 설정에 대해 포트 9050을 지정합니다.


모든 항목을 만든 후 이동 toohello **개요** hello DC/OS 에이전트 부하 분산 장치의 블레이드 (라는 리소스 hello **에이전트 lb xxxx dcos**). Hello **공용 IP 주소**, 9050 포트에서 주소 tooaccess sava hello를 사용 합니다.

![Azure Portal - 공용 IP 주소 가져오기](./media/container-service-dcos-vamp-canary-release/18_public_ip_address.png)

![sava](./media/container-service-dcos-vamp-canary-release/19_sava100.png)


## <a name="run-a-canary-release"></a>카나리아 릴리스 실행

이 응용 프로그램의 새 버전 toocanary 릴리스를 프로덕션 환경 한다고 가정 합니다. Magneticio/sava:1.1.0으로 컨테이너 화 된 것 되 toogo 준비 합니다. Vamp 쉽게 배포를 실행 하는 새 서비스 toohello를 추가할 수 있습니다. 이러한 "병합된" 서비스는 hello hello 클러스터의 기존 서비스와 함께 배포 되 고 0%의 가중치를 할당 합니다. 트래픽이 hello 트래픽 분배로 인해 조정 될 때까지 새로 병합 라우트된 tooa 서비스입니다. hello 가중치 슬라이더 hello Vamp UI에서에서 완전히 제어할 hello 분포를 증분 조정 (카나리아 릴리스) 이나 인스턴트 롤백 범위를 제공 합니다.

### <a name="merge-a-new-service-variant"></a>새로운 서비스 변형 병합

toomerge hello 새 sava 1.1 서비스 배포를 실행 하는 hello로:

1. Hello Vamp UI, 클릭 **청사진**합니다.

2. 클릭 **추가** 및 붙여넣기를 수행 하는 hello에 YAML 세부 계획:이 청사진 hello 기존 클러스터 (sava_cluster) 내에서 새 서비스 (sava: 1.1.0) variant toodeploy에 설명 합니다.

  ```YAML
  name: sava:1.1.0      # blueprint name
  clusters:
    sava_cluster:       # cluster tooupdate
      services:
        -
          breed:
            name: sava:1.1.0    # service variant name
            deployable: magneticio/sava:1.1.0    
            ports:
              webport: 8080/http # cluster endpoint tooupdate
  ```
  
3. **Save**를 클릭합니다. hello 청사진 저장 되 고 hello에 나열 된 **청사진** 페이지.

4. 열기 hello 동작 메뉴를 클릭 한 hello sava: 1.1 청사진 **병합**합니다.

  ![Vamp UI - 청사진](./media/container-service-dcos-vamp-canary-release/20_sava110_mergeto.png)

5. 선택 hello **sava** 배포 및 클릭 **병합**합니다.

  ![UI vamp-청사진 toodeployment 병합](./media/container-service-dcos-vamp-canary-release/21_sava110_merge.png)

Vamp hello 새 sava: 1.1.0 서비스 variant sava: 1.0.0 hello에 함께 hello 청사진에 설명 된 배포 **sava_cluster** 의 hello 배포를 실행 합니다. 

![Vamp UI - 업데이트된 sava 배포](./media/container-service-dcos-vamp-canary-release/22_sava_cluster.png)

hello **sava/sava_cluster/webport** 게이트웨이 (hello 클러스터 끝점)도 업데이트, sava: 1.1.0 배포 경로 toohello 새로 추가 합니다. 이 시점에서 트래픽이 라우팅됩니다 여기 (hello **가중치** too0% 설정).

![Vamp UI - 클러스터 게이트웨이](./media/container-service-dcos-vamp-canary-release/23_sava_cluster_webport.png)

### <a name="canary-release"></a>카나리아 릴리스

두 버전의 sava에에서 배포 된 hello 동일 클러스터 hello를 이동 하 여 서로 트래픽의 hello 배포를 조정 하세요 **가중치** 슬라이더 합니다.

1. 클릭 ![Vamp UI-편집](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) 다음 너무**가중치**합니다.

2. Hello 가중치 배포 too50%/50%를 설정 하 고 클릭 **저장**합니다.

  ![Vamp UI - 게이트웨이 가중치 슬라이더](./media/container-service-dcos-vamp-canary-release/24_sava_cluster_webport_weight.png)

3. Tooyour 브라우저와를 몇 번 더 hello sava 페이지를 새로 고칩니다. hello sava 응용 프로그램을 지금 sava: 1.0 및 1.1 sava: 페이지가 사이 전환 합니다.

  ![sava1.0 및 sava1.1 서비스 교대](./media/container-service-dcos-vamp-canary-release/25_sava_100_101.png)


  > [!NOTE]
  > 이 교체 hello 페이지의 정적 자산 hello 캐싱 때문에 hello "Incognito" 또는 "Anonymous" 모드 브라우저의 가장 잘 작동 합니다.
  >

### <a name="filter-traffic"></a>트래픽 필터링

배포 후 sava:1.1.0에서 Firefox 브라우저 표시 문제를 일으키는 호환성 문제를 발견했다고 가정해 봅시다. Vamp toofilter 들어오는 트래픽을 설정할 수 있으며 모든 Firefox 사용자 다시 안정적인 sava: 1.0.0 알려진 toohello 직접 있습니다. 이 필터도 다른 모든 사용자의 hello tooenjoy hello 이점을 계속 되는 동안 확인 hello Firefox 사용자를 사용 하지 못하게 하는 바로 sava: 1.1.0 향상.

사용 하 여 vamp **조건** toofilter 트래픽 간의 게이트웨이의 경로입니다. 먼저 필터링 된 트래픽과 toohello 조건이 적용 tooeach 경로 따라 이동 합니다. 나머지 모든 트래픽이 toohello 게이트웨이 가중치 설정에 따라 배포 됩니다.

조건 toofilter 모든 Firefox 사용자를 만들 수 있고 이전 sava 1.0.0 toohello 가리킬 됩니다.:

1. Hello sava/sava_cluster/webport에 **게이트웨이** 페이지 ![Vamp UI-편집](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) tooadd는 **조건** toohello 경로 sava/sava_cluster/sava:1.0.0/webport 합니다. 

2. Hello 조건을 입력 **사용자 에이전트 Firefox = =** 클릭 ![Vamp UI-저장](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png)합니다.

  Vamp 0%의 기본 강도 가진 hello 상태를 추가합니다. toostart 필터링 트래픽 tooadjust hello 조건 강도 필요합니다.

3. 클릭 ![Vamp UI-편집](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) toochange hello **강도** toohello 조건을 적용 합니다.
 
4. 집합 hello **강도** too100% 클릭 ![Vamp UI-저장](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) toosave 합니다.

  이제 vamp hello 조건 (모든 Firefox 사용자) toosava:1.0.0 일치 하는 모든 트래픽을 보냅니다.

  ![UI vamp-조건 toogateway 적용](./media/container-service-dcos-vamp-canary-release/26_apply_condition.png)

5. 마지막으로 hello 게이트웨이 가중치 toosend 모든 나머지 트래픽 (모든 Firefox 아닌 사용자) toohello 새 sava: 1.1.0 조정 합니다. 클릭 ![Vamp UI-편집](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) 다음 너무**가중치** 100%는 방향이 지정 된 toohello 경로 sava/sava_cluster/sava:1.1.0/webport hello 가중치 배포를 설정 합니다.

  Hello 조건에 의해 필터링 되지 않으면 모든 트래픽을 지정 된 toohello 새 sava: 1.1.0 되었습니다.

6. toosee hello 필터 작업에서 두 개의 서로 다른 브라우저 (하나 Firefox 및 다른 브라우저)를 열고 둘 다에서 hello sava 서비스에 액세스 합니다. 다른 모든 브라우저는 방향이 지정 된 toosava:1.1.0 Firefox에 대 한 모든 요청에서 toosava:1.0.0, 전송 됩니다.

  ![Vamp UI - 트래픽 필터링](./media/container-service-dcos-vamp-canary-release/27_filter_traffic.png)

## <a name="summing-up"></a>요약

이 문서에서 DC/OS 클러스터에 간략 한 소개 tooVamp. 먼저 Vamp를 까 배포 하 고에서 Azure 컨테이너 서비스 DC/OS를 실행 중인 클러스터 Vamp 청사진을 사용 하 여 서비스 hello 노출 된 끝점 (게이트웨이)에서 액세스 합니다.

또한 Vamp의 강력한 기능 일부 다루었습니다 우리: 병합을 새 서비스 variant toohello 배포를 실행 하 고 증분 소개 다음 트래픽 tooresolve 알려진된 호환성 문제를 필터링 합니다.


## <a name="next-steps"></a>다음 단계

* Hello 통해 Vamp 동작을 관리 하는 방법에 대 한 자세한 내용은 [REST API Vamp](http://vamp.io/documentation/api/api-reference/)합니다.

* Node.js에서 Vamp 자동화 스크립트를 빌드하고 [Vamp 워크플로](http://vamp.io/documentation/tutorials/create-a-workflow/)로 실행합니다.

* 추가 [VAMP 자습서](http://vamp.io/documentation/tutorials/overview/)를 살펴봅니다.

