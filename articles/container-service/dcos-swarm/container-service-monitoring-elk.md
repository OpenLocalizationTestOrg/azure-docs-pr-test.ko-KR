---
title: "Azure DC/OS 클러스터-ELK 스택 aaaMonitor | Microsoft Docs"
description: "ELK(Elasticsearch, Logstash 및 Kibana)를 사용하여 Azure Container Service 클러스터에서 DC/OS 클러스터를 모니터링합니다."
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "컨테이너, DC/OS, Azure, 모니터링, elk"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 8d81c5342616ec14880d38803cdf95f5845a669b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-elk"></a>ELK를 사용하여 Azure Container Service 클러스터 모니터링
이 문서에서는 Azure 컨테이너 서비스에서 DC/OS 클러스터에 toodeploy hello ELK (Elasticsearch Logstash, Kibana) 스택 하는 방법을 보여 줍니다. 

## <a name="prerequisites"></a>필수 조건
Azure Container Service를 통해 구성된 DC/OS 클러스터를 [배포](container-service-deployment.md) 및 [연결](../container-service-connect.md)합니다. DC/OS 대시보드 hello 및 마라톤 서비스 탐색 [여기](container-service-mesos-marathon-ui.md)합니다. 또한 hello 설치 [부하 분산 장치 풀 마라톤](container-service-load-balancing.md)합니다.


## <a name="elk-elasticsearch-logstash-kibana"></a>ELK(Elasticsearch, Logstash, Kibana)
ELK 스택 Elasticsearch Logstash의 조합을 이며 Kibana 최종 tooend 스택을 제공 하는 사용 되는 toomonitor 수 있으며 클러스터의 로그를 분석 합니다.

## <a name="configure-hello-elk-stack-on-a-dcos-cluster"></a>DC/OS 클러스터에 hello ELK 스택 구성
DC/OS UI를 통해 액세스 [http://localhost:80 /](http://localhost:80/) hello DC/OS UI 너무 탐색에서 한 번**Universe**합니다. 검색 하 고 해당 특정 순서로 및 hello DC/OS Universe에서에서 Elasticsearch, Logstash, 및 Kibana를 설치 합니다. Toohello 전환 되는 경우 구성에 대 한 자세히 알아볼 수 있습니다 **고급 설치** 링크 합니다.

![ELK1](./media/container-service-monitoring-elk/elk1.PNG) ![ELK2](./media/container-service-monitoring-elk/elk2.PNG) ![ELK3](./media/container-service-monitoring-elk/elk3.PNG) 

ELK 컨테이너와 작동 하 고 실행은 한 번 hello tooenable Kibana toobe 마라톤 LB를 통해 액세스를 해야 합니다. 너무 이동 **서비스** > **kibana**를 클릭 하 고 **편집** 다음과 같이 합니다.

![ELK4](./media/container-service-monitoring-elk/elk4.PNG)


너무 설정/해제**JSON 모드** toohello 레이블 섹션 아래로 스크롤합니다.
Tooadd 필요는 `"HAPROXY_GROUP": "external"` 항목이 여기에 표시 된 대로 아래 합니다.
**변경 내용 배포**를 클릭하면 컨테이너가 다시 시작됩니다.

![ELK5](./media/container-service-monitoring-elk/elk5.PNG)


Tooverify 하려는 경우 해당 Kibana hello haproxy와 대시보드는 서비스로 서 등록 haproxy와 9090 포트에서 실행 될 때 tooopen 포트 9090 hello 에이전트 클러스터에서를 해야 합니다.
기본적으로에서는 포트 80, 8080 열고 443에서 DC/OS 에이전트 클러스터 hello 합니다.
지침 tooopen 포트 공용 평가 제공 하 고 제공 [여기](container-service-enable-public-access.md)합니다.

tooaccess hello haproxy와 대시보드를 열고 hello 마라톤 LB 관리 인터페이스에서: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`합니다.
Toohello URL을 탐색 한 후 아래와 같이 hello haproxy와 대시보드를 참조 해야 및 Kibana에 대 한 서비스 항목을 표시 되어야 합니다.

![ELK6](./media/container-service-monitoring-elk/elk6.PNG)


포트 5601에 배포 된 tooaccess hello Kibana 대시보드에 tooopen 포트 5601 해야 합니다. [여기](container-service-enable-public-access.md)에 나와 있는 지침을 따르세요. hello Kibana 대시보드를 엽니다. `http://localhost:5601`합니다.

## <a name="next-steps"></a>다음 단계

* 시스템 및 응용 프로그램 로그 전달 및 설정은 [ELK로 DC/OS에서 로그 관리](https://docs.mesosphere.com/1.8/administration/logging/elk/)를 참조하세요.

* toofilter 로그 참조 [ELK 사용 하 여 로그 필터링](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/)합니다. 

 

