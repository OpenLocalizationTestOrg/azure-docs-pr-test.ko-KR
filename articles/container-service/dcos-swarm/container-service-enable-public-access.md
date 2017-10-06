---
title: "DC/OS 컨테이너 응용 프로그램 aaaEnable 액세스 tooAzure | Microsoft Docs"
description: "Tooenable 공용 tooDC/OS 컨테이너 Azure 컨테이너 서비스에 액세스 하는 방법입니다."
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로 서비스, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 1ba251ba5a176a6a5e1c7831655164e380a62b27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-public-access-tooan-azure-container-service-application"></a>공용 액세스 tooan Azure 컨테이너 서비스 응용 프로그램을 사용 하도록 설정
Hello ACS의에서 모든 DC/OS 컨테이너 [공용 에이전트 풀](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) 은 자동으로 노출 된 toohello 인터넷 합니다. 기본적으로 포트 **80**, **443**, **8080**이 열리며 이러한 포트에서 수신 대기하는 모든 (공용) 컨테이너에 액세스할 수 있습니다. 이 문서에서는 tooopen Azure 컨테이너 서비스에서 응용 프로그램에 더 포트 방법을 설명 합니다.

## <a name="open-a-port-portal"></a>포트 열기(포털)
먼저 tooopen hello 포트 주시기 바랍니다.

1. Toohello 포털에 로그인 합니다.
2. 찾기 hello 리소스 그룹 배포 된 hello Azure 컨테이너 서비스를 합니다.
3. Hello 에이전트에 대 한 부하 분산 장치를 선택 (라는 비슷한 너무**XXXX 에이전트-lb XXXX**).
   
    ![Azure Container Service 부하 분산 장치](./media/container-service-enable-public-access/agent-load-balancer.png)
4. **프로브**를 클릭한 후 **추가**를 클릭합니다.
   
    ![Azure Container Service 부하 분산 장치 프로브](./media/container-service-enable-public-access/add-probe.png)
5. Hello 프로브 양식을 작성 하 고 클릭 **확인**합니다.
   
   | 필드 | 설명 |
   | --- | --- |
   | 이름 |Hello 프로브의 설명이 포함 된 이름입니다. |
   | 포트 |hello 컨테이너 tootest의 hello 포트입니다. |
   | Path |(HTTP 모드의 경우) 상대 웹 사이트 경로 tooprobe hello 합니다. HTTPS는 지원되지 않습니다. |
   | 간격 |hello 프로브 시간 간격 (초)에서 시도합니다. |
   | 비정상 임계값 |Hello 컨테이너를 비정상으로 간주 되기 전에 시도 하는 연속 프로브 횟수입니다. |
6. Hello 속성 hello 에이전트에 대 한 부하 분산 장치에서 다시 **부하 분산 규칙** 차례로 **추가**합니다.
   
    ![Azure Container Service 부하 분산 장치 규칙](./media/container-service-enable-public-access/add-balancer-rule.png)
7. Hello 부하 분산 장치 양식을 작성 하 고 클릭 **확인**합니다.
   
   | 필드 | 설명 |
   | --- | --- |
   | 이름 |부하 분산 장치 hello의 설명이 포함 된 이름입니다. |
   | 포트 |hello 공용 수신 포트입니다. |
   | 백 엔드 포트 |hello 컨테이너 tooroute 트래픽을 hello public이 내부 포트입니다. |
   | 백 엔드 풀 |이 풀에 있는 hello 컨테이너에는이 부하 분산 장치에 대 한 hello 대상이 됩니다. |
   | 프로브 |경우 hello에 대상을 사용 하는 프로브 toodetermine hello **백 엔드 풀** 정상입니다. |
   | 세션 지속성 |Hello hello 세션 기간에 대 한 클라이언트의 트래픽을 처리 되는 방법을 결정 합니다.<br><br>**None**: 연속 요청만 hello 동일한 클라이언트 모든 컨테이너에 의해 처리 될 수 있습니다.<br>**클라이언트 IP**: 동일한 컨테이너를 hello 연속 요청만 hello 동일한 클라이언트 IP에 의해 처리 됩니다.<br>**클라이언트 IP 및 프로토콜**: 동일한 컨테이너를 hello 연속 요청만 hello 동일한 클라이언트 IP 및 프로토콜 조합에 의해 처리 됩니다. |
   | 유휴 상태 시간 제한 |TCP (만) 분에서 시간 tookeep TCP/HTTP 클라이언트에 의존 하지 않고 열 hello *유지* 메시지입니다. |

## <a name="add-a-security-rule-portal"></a>보안 규칙 추가(포털)
다음으로, tooadd hello 방화벽을 통해이 열린된 포트에서 트래픽을 라우팅하는 보안 규칙 필요 합니다.

1. Toohello 포털에 로그인 합니다.
2. 찾기 hello 리소스 그룹 배포 된 hello Azure 컨테이너 서비스를 합니다.
3. 선택 hello **공용** 에이전트 네트워크 보안 그룹 (라는 비슷한 너무**XXXX 에이전트-public이-nsg-XXXX**).
   
    ![Azure Container Service 네트워크 보안 그룹](./media/container-service-enable-public-access/agent-nsg.png)
4. **인바운드 보안 규칙**을 선택한 후 **추가**를 선택합니다.
   
    ![Azure Container Service 네트워크 보안 그룹 규칙](./media/container-service-enable-public-access/add-firewall-rule.png)
5. 공용 포트 hello 방화벽 규칙 tooallow 작성 하 고 클릭 **확인**합니다.
   
   | 필드 | 설명 |
   | --- | --- |
   | 이름 |Hello 방화벽 규칙의 설명이 포함 된 이름입니다. |
   | 우선 순위 |Hello 규칙에 대 한 우선 순위입니다. hello 낮은 hello 숫자 hello 더 높은 hello 우선 순위입니다. |
   | 원본 |Hello 들어오는 IP 주소 범위 toobe이이 규칙에 따라 허용 되거나 거부를 제한 합니다. 사용 하 여 **모든** toonot 제한을 지정 합니다. |
   | 부여 |이 보안 규칙을 위한 미리 정의된 서비스 집합을 선택합니다. 그렇지 않으면 사용 **사용자 지정** toocreate 직접 합니다. |
   | 프로토콜 |**TCP** 또는 **UDP**에 따라 트래픽을 제한합니다. 사용 하 여 **모든** toonot 제한을 지정 합니다. |
   | 포트 범위 |때 **서비스** 은 **사용자 지정**,이 규칙에 영향을 주는 포트의 hello 범위를 지정 합니다. **80**과 같은 단일 포트 또는 **1024-1500**과 같은 범위를 사용할 수 있습니다. |
   | 동작 |트래픽을 허용 하거나 거부 hello 조건을 만족 하 합니다. |

## <a name="next-steps"></a>다음 단계
Hello 차이점에 대 한 자세한 내용은 [공용 및 개인 DC/OS 에이전트](container-service-dcos-agents.md)합니다.

[DC/OS 컨테이너 관리](container-service-mesos-marathon-ui.md)에 대해 자세히 알아보세요.

