---
title: "aaaCreate는 내부 부하 분산 장치-Azure 포털 | Microsoft Docs"
description: "어떻게 toocreate는 내부 부하 분산 장치 hello Azure 포털을 사용 하 여 리소스 관리자에 알아봅니다."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ac14fb9-8d14-4892-bfe6-8bc74c48ae2c
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 80124217a84857b542eb41cb814ec97234176dd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-in-hello-azure-portal"></a>Hello Azure 포털에에서는 내부 부하 분산 장치 만들기

> [!div class="op_single_selector"]
> * [Azure 포털](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [템플릿](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.  사용 하 여이 문서에서는 Microsoft hello 대신 대부분의 새 배포에 권장 하는 hello 리소스 관리자 배포 모델 [클래식 배포 모델](load-balancer-get-started-ilb-classic-ps.md)합니다.

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="get-started-creating-an-internal-load-balancer-using-azure-portal"></a>Azure 포털을 사용하여 내부 부하 분산 장치 만들기 시작

Hello 단계 toocreate 내부 부하 분산 장치는 hello Azure 포털에서에서 다음을 사용 합니다.

1. 브라우저를 열고 탐색 toohello [Azure 포털](http://portal.azure.com), Azure 계정으로 로그인 합니다.
2. Hello hello 화면의 왼쪽 위 측면, 클릭 **새로** > **네트워킹** > **부하 분산 장치**합니다.
3. Hello에 **부하 분산 장치 만들기** 블레이드를 입력 한 **이름** 부하 분산 장치에 대 한 합니다.
4. **구성표**에서 **내부**를 클릭합니다.
5. 클릭 **가상 네트워크**을 다음 선택 hello toocreate hello에 대 한 부하 분산 장치를 원하는 가상 네트워크 및 합니다.

   > [!NOTE]
   > Hello 가상 네트워크 toouse를 원하는 경우 확인 hello **위치** hello 부하 분산을 사용 하 고 적절 하 게 변경 합니다.

6. 클릭 **서브넷**, 한 다음 toocreate hello에 대 한 부하 분산 장치를 원하는 hello 서브넷을 선택 합니다.
7. 아래 **IP 주소 할당**, 클릭 **동적** 또는 **정적**여부 hello IP 주소에 대해 원하는 hello 부하 분산 장치 toobe 고정 (정적) 여부에 따라 합니다.

   > [!NOTE]
   > Toouse 고정 IP 주소를 선택 해야 합니다 tooprovide hello 부하 분산 장치에 대 한 주소입니다.

8. 아래 **리소스 그룹** hello 부하 분산 장치에 대 한 새 리소스 그룹의 hello 이름을 지정 하거나 클릭 **기존 선택** 기존 리소스 그룹을 선택 합니다.
9. **만들기**를 클릭합니다.

## <a name="configure-load-balancing-rules"></a>부하 분산 규칙 구성

Hello 후 부하 분산 장치 만들기, 이동 toohello 부하 분산 장치 리소스 tooconfigure 것입니다.
Tooconfigure 먼저 백 엔드 주소 풀 및 필요에 검색 부하 분산 규칙을 구성 하기 전에.

### <a name="step-1-configure-a-back-end-pool"></a>1단계: 백 엔드 풀 구성

1. Hello Azure 포털에서에서 클릭 **찾아보기** > **부하 분산 장치**, 다음 위에서 만든 hello 부하 분산 장치를 클릭 합니다.
2. Hello에 **설정** 블레이드에서 클릭 **백 엔드 풀**합니다.
3. Hello에 **백 엔드 주소 풀** 블레이드에서 클릭 **추가**합니다.
4. Hello에 **백 엔드 풀 추가** 블레이드를 입력 한 **이름** hello 백 엔드 풀 및 클릭 한 다음에 대 한 **확인**합니다.

### <a name="step-2-configure-a-probe"></a>2단계: 프로브 구성

1. Hello Azure 포털에서에서 클릭 **찾아보기** > **부하 분산 장치**, 다음 위에서 만든 hello 부하 분산 장치를 클릭 합니다.
2. Hello에 **설정** 블레이드에서 클릭 **프로브**합니다.
3. Hello에 **프로브** 블레이드에서 클릭 **추가**합니다.
4. Hello에 **추가 프로브** 블레이드를 입력 한 **이름** hello 검색 합니다.
5. **프로토콜**에서 **HTTP**(웹 사이트용) 또는 **TCP**(기타 TCP 기반 응용 프로그램용)를 선택합니다.
6. 아래 **포트**, hello 프로브에 액세스할 때 hello 포트 toouse를 지정 합니다.
7. 아래 **경로** (프로브에 대해 HTTP만), hello 경로 toouse에 검색으로 지정 합니다.
8. 아래 **간격** 얼마나 자주 tooprobe hello 응용 프로그램을 지정 합니다.
9. 아래 **비정상 임계값**, hello 백 엔드 가상 컴퓨터를 비정상으로 표시 되기 전에 개수 시도가 실패 하는지 지정 합니다.
10. 클릭 **확인** toocreate 프로브 합니다.

### <a name="step-3-configure-load-balancing-rules"></a>3단계: 부하 분산 규칙 구성

1. Hello Azure 포털에서에서 클릭 **찾아보기** > **부하 분산 장치**, 다음 위에서 만든 hello 부하 분산 장치를 클릭 합니다.
2. Hello에 **설정** 블레이드에서 클릭 **부하 분산 규칙**합니다.
3. Hello에 **부하 분산 규칙** 블레이드에서 클릭 **추가**합니다.
4. Hello에 **추가 부하 분산 규칙** 블레이드를 입력 한 **이름** hello 규칙에 대 한 합니다.
5. **프로토콜**에서 **HTTP**(웹 사이트용) 또는 **TCP**(기타 TCP 기반 응용 프로그램용)를 선택합니다.
6. 아래 **포트**, hello 포트 클라이언트가 tooin hello에 대 한 부하 분산 장치 연결을 지정 합니다.
7. 아래 **백 엔드 포트가**, hello 백 엔드 풀에서 사용 하는 hello 포트 toobe 지정 (일반적으로 hello 부하 분산 장치 포트와 백 엔드 포트가 hello는 hello 동일).
8. 아래 **백 엔드 풀**선택, 위에서 만든 hello 백 엔드 풀입니다.
9. 아래 **세션 지 속성**세션 toopersist 원하는 방식을 선택 합니다.
10. 아래 **유휴 시간 제한 (분)**, hello 유휴 시간 제한을 지정 합니다.
11. **부동 IP(Direct Server Return(DSR))**에서 **사용 안 함** 또는 **사용**을 클릭합니다.
12. **확인**을 클릭합니다.

## <a name="next-steps"></a>다음 단계

[부하 분산 장치 배포 모드 구성](load-balancer-distribution-mode.md)

[부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성](load-balancer-tcp-idle-timeout.md)

