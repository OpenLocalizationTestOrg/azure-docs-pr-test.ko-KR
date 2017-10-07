---
title: "aaaAzure 컨테이너 인스턴스 컨테이너 그룹"
description: "컨테이너 그룹이 Azure Container Instances에서 작동하는 방법 이해"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2b0e784609979045c8f77d7b6d0987ec3fee714c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="container-groups-in-azure-container-instances"></a>Azure Container Instances의 컨테이너 그룹

컨테이너 인스턴스를 Azure의 hello 최상위 리소스는 컨테이너 그룹. 이 문서에서는 컨테이너 그룹의 정의와 이들이 지원하는 시나리오 유형에 대해 설명합니다.

## <a name="how-a-container-group-works"></a>컨테이너 그룹 작동 방식

컨테이너 그룹은 컬렉션 hello에 예약 하는 컨테이너의 동일 컴퓨터를 호스트 하 고 전체 수명 주기, 로컬 네트워크 및 저장소 볼륨을 공유 합니다. 유사한 toohello 개념는 *pod* 에 [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) 및 [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/)합니다.

hello 다음 다이어그램의 예가 나와 여러 컨테이너를 포함 하는 컨테이너 그룹입니다.

![컨테이너 그룹 예][container-groups-example]

다음 사항에 유의하세요.

- hello 그룹은 단일 호스트 컴퓨터에서 예약 됩니다.
- hello 그룹에는 단일 공용 IP 주소를 하나의 노출 된 포트와 노출합니다.
- 두 컨테이너의 hello 그룹으로 이루어집니다. 하나의 컨테이너 hello 다른 5000 포트에서 수신 하는 동안 포트 80에서 수신 합니다.
- 각 컨테이너 로컬로 hello 공유 중 하나를 탑재 및 hello 그룹 볼륨 마운트도 두 개의 Azure 파일 공유를 포함 합니다.

### <a name="networking"></a>네트워킹

컨테이너 그룹은 IP 주소와 해당 IP 주소에서 포트 네임스페이스를 공유합니다. tooenable 외부 클라이언트 tooreach hello 그룹 내에서 컨테이너를 hello IP 주소에 대 한 hello 컨테이너에서 hello 포트를 노출 해야 합니다. Hello 그룹 내의 컨테이너 포트 네임 스페이스를 공유 하므로 포트 매핑은 지원 되지 않습니다. 그룹 내의 컨테이너 도달할 수 서로 hello에 localhost를 통해를 노출 하는 포트 hello 그룹의 IP 주소에 해당 포트를 외부적으로 노출 되지 않는 경우에 합니다.

### <a name="storage"></a>저장소

컨테이너 그룹 내에서 외부 볼륨 toomount를 지정할 수 있습니다. 해당 볼륨 그룹의 hello 개별 컨테이너 내에서 특정 경로에 매핑할 수 있습니다.

## <a name="common-scenarios"></a>일반적인 시나리오

다중 컨테이너 그룹은 적은 수의 다른 팀에서 제공 되며,와 별도 리소스 요구 사항이 있는 컨테이너 이미지에는 단일 기능 작업을 toodivide을 원하는 경우에 유용 합니다. 사용 예는 다음과 같습니다.

- 응용 프로그램 컨테이너 및 로깅 컨테이너. hello 로깅 컨테이너는 hello 주 응용 프로그램에 의해 hello 로그 및 메트릭 출력을 수집 하 고 toolong 장기적 저장을 기록 합니다.
- 응용 프로그램 및 모니터링 컨테이너. 컨테이너를 주기적으로 모니터링 하는 hello 실행 중 이며 올바르게 응답 하지 않으면 경고를 발생 하는 요청 toohello 응용 프로그램 tooensure를 만듭니다.
- 웹 응용 프로그램을 처리 하는 컨테이너 및 소스 제어에서 최신 콘텐츠 hello 당겨 컨테이너.

## <a name="next-steps"></a>다음 단계

너무 방법에 대해 알아봅니다[다중 컨테이너 그룹 배포](container-instances-multi-container-group.md) Azure 리소스 관리자 템플릿을 사용 하 여 합니다.

<!-- IMAGES -->

[container-groups-example]: ./media/container-instances-container-groups/container-groups-example.png