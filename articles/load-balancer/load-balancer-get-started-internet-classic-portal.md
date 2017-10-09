---
title: "aaaCreate 인터넷 연결 부하 분산 장치-클래식 Azure 포털 | Microsoft Docs"
description: "인터넷 연결 부하 분산 장치에 사용 하 여 클래식 배포 모델 toocreate Azure 클래식 포털 hello 하는 방법에 대해 알아봅니다"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fa3e93c0-968a-472d-a17c-65665c050db2
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 27b0d5af6e7b493fa94a9dfbfa260483ae95a2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-classic-portal"></a>경우에 인터넷 연결 hello Azure 클래식 포털에서에서 부하 분산 장치 (클래식)를 만들기 시작

> [!div class="op_single_selector"]
> * [Azure 클래식 포털](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Azure 클라우드 서비스](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Azure 리소스를 사용 하기 전에 Azure에 현재 두 가지 배포 모델에 중요 한 toounderstand: Azure 리소스 관리자 및 기본 합니다. Azure 리소스로 작업하기 전에 [배포 모델 및 도구](../azure-classic-rm.md) 를 이해해야 합니다. 이 문서의 hello 위쪽 hello 탭을 클릭 하 여 다양 한 도구에 대 한 hello 설명서를 볼 수 있습니다. 이 문서에서는 hello 클래식 배포 모델에 설명 합니다. 수도 있습니다 [toocreate 인터넷 연결 로드 분산 장치는 Azure 리소스 관리자를 사용 하는 방법에 대해 알아봅니다](load-balancer-get-started-internet-arm-ps.md)합니다.

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-an-internet-facing-load-balancer-for-virtual-machines"></a>가상 컴퓨터에 대한 인터넷 연결 부하 분산 장치 설정

순서 tooload 분산할 네트워크 트래픽 hello 인터넷 hello 가상 컴퓨터 클라우드 서비스의 사이에서 부하 분산 된 집합을 만들어야 합니다. 이 절차에서는 hello 가상 컴퓨터를 이미 만들었다고 있고 이들이 모두 hello 내에서 동일한 클라우드 서비스입니다.

**가상 컴퓨터에 대 한 부하 분산 집합 tooconfigure**

1. Hello Azure 클래식 포털에서에서 클릭 **가상 컴퓨터**, hello 부하 분산 집합에 가상 컴퓨터의 hello 이름을 클릭 하 고 있습니다.
2. **끝점**을 클릭한 후 **추가**를 클릭합니다.
3. Hello에 **끝점 tooa 가상 컴퓨터 추가** 페이지 hello 오른쪽 화살표를 클릭 합니다.
4. Hello에 **hello 끝점의 hello 세부 정보 지정** 페이지:

   * **이름**, hello 끝점에 대 한 이름을 입력 하거나 일반 프로토콜에 대해 미리 정의 된 끝점의 hello 목록에서 hello 이름을 선택 합니다.
   * **프로토콜**, 필요에 따라 TCP 또는 UDP 끝점의 hello 유형에 필요한 hello 프로토콜을 선택 합니다.
   * **공용 포트 및 개인 포트**, 원하는 가상 컴퓨터 toouse hello 필요에 따라 hello 포트 번호를 입력 합니다. 응용 프로그램에 대 한 적절 한 방식으로 가상 컴퓨터 tooredirect 트래픽을 hello hello 개인 포트 및 방화벽 규칙을 사용할 수 있습니다. hello 개인 포트는 hello 공용 포트와 동일한 hello 수 있습니다. 예를 들어 웹 (HTTP) 트래픽에 대 한 끝점에 대 한 포트 80 tooboth hello 공용 및 개인 포트를 할당할 수 있습니다.

5. 선택 **부하 분산 된 집합을 만들**, 다음 hello 오른쪽 화살표를 클릭 합니다.
6. Hello에 **hello 부하 분산 된 집합 구성** 페이지 hello 부하 분산 집합에 대 한 이름을 입력 한 다음 hello의 hello Azure 부하 분산 장치 프로브 동작 값을 할당 합니다. hello 부하 분산 집합의 hello 가상 컴퓨터는 사용할 수 있는 tooreceive 들어오는 트래픽을 hello 부하 분산 장치 프로브 toodetermine를 사용 합니다.
7. Hello 확인 표시가 toocreate hello 부하 분산 끝점을 클릭 합니다. 나타납니다 **예** hello에 **부하 분산 집합 이름이** hello 열 **끝점** hello 가상 컴퓨터에 대 한 페이지입니다.
8. Hello 포털에서 클릭 **가상 컴퓨터**hello 부하 분산 된 집합에 추가 가상 컴퓨터의 hello 이름을 클릭 하 고 **끝점**, 클릭 하 고 **추가**합니다.
9. Hello에 **끝점 tooa 가상 컴퓨터 추가** 페이지 **끝점 tooan 기존 부하 분산 집합을 추가**hello 부하 분산 된 집합의 hello 이름을 선택한 다음 hello 오른쪽 화살표를 클릭 합니다.
10. Hello에 **hello 끝점의 hello 세부 정보 지정** 페이지 hello 끝점에 대 한 이름을 입력 한 다음 hello 확인 표시를 클릭 합니다.

Hello 추가 가상 컴퓨터의 hello 부하 분산 된 집합의 경우 8 ~ 10 단계를 반복 합니다.

## <a name="next-steps"></a>다음 단계

[내부 부하 분산 장치 구성 시작](load-balancer-get-started-ilb-arm-ps.md)

[부하 분산 장치 배포 모드 구성](load-balancer-distribution-mode.md)

[부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성](load-balancer-tcp-idle-timeout.md)
