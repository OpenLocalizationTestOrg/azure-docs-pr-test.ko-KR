---
title: "Azure 클라우드 서비스에 대 한 부하 분산 장치는 인터넷 연결 aaaCreate | Microsoft Docs"
description: "인터넷 연결 toocreate 분산 장치 클라우드 서비스에 대 한 클래식 배포 모델에 로드 하는 방법에 대해 알아봅니다"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 0bb16f96-56a6-429f-88f5-0de2d0136756
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: d93cf76d417cbfc744cf07ba48c43a63cc14df69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-for-cloud-services"></a>클라우드 서비스를 위한 인터넷 연결 부하 분산 장치 만들기 시작

> [!div class="op_single_selector"]
> * [Azure 클래식 포털](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Azure 클라우드 서비스](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Azure 리소스를 사용 하기 전에 Azure에 현재 두 가지 배포 모델에 중요 한 toounderstand: Azure 리소스 관리자 및 기본 합니다. Azure 리소스로 작업하기 전에 [배포 모델 및 도구](../azure-classic-rm.md) 를 이해해야 합니다. 이 문서의 hello 위쪽 hello 탭을 클릭 하 여 다양 한 도구에 대 한 hello 설명서를 볼 수 있습니다. 이 문서에서는 hello 클래식 배포 모델에 설명 합니다. 수도 있습니다 [toocreate 인터넷 연결 로드 분산 장치는 Azure 리소스 관리자를 사용 하는 방법에 대해 알아봅니다](load-balancer-get-started-internet-arm-ps.md)합니다.

클라우드 서비스는 자동으로 부하 분산 장치 구성 및 hello 서비스 모델을 통해 사용자 지정할 수 있습니다.

## <a name="create-a-load-balancer-using-hello-service-definition-file"></a>Hello 서비스 정의 파일을 사용 하 여 부하 분산 장치 만들기

클라우드 서비스에 대 한.NET 2.5 tooupdate hello Azure SDK를 활용할 수 있습니다. 클라우드 서비스에 대 한 끝점 설정 hello 내용이 [서비스 정의](https://msdn.microsoft.com/library/azure/gg557553.aspx) .csdef 파일입니다.

hello 다음 예제는 클라우드 배포에 대 한 servicedefinition.csdef 파일은 구성 하는 방법.

클라우드 배포에서 생성 된 hello.csdef 파일에 대 한 hello 조각 검사 hello 구성 된 외부 끝점이 toouse 포트 HTTP 포트 10000, 10001, 및 10002에서 볼 수 있습니다.

```xml
<ServiceDefinition name=“Tenant“>
    <WorkerRole name=“FERole” vmsize=“Small“>
<Endpoints>
    <InputEndpoint name=“FE_External_Http” protocol=“http” port=“10000“ />
    <InputEndpoint name=“FE_External_Tcp“  protocol=“tcp“  port=“10001“ />
    <InputEndpoint name=“FE_External_Udp“  protocol=“udp“  port=“10002“ />

    <InputEndpointname=“HTTP_Probe” protocol=“http” port=“80” loadBalancerProbe=“MyProbe“ />

    <InstanceInputEndpoint name=“InstanceEP” protocol=“tcp” localPort=“80“>
        <AllocatePublicPortFrom>
            <FixedPortRange min=“10110” max=“10120“  />
        </AllocatePublicPortFrom>
    </InstanceInputEndpoint>
    <InternalEndpoint name=“FE_InternalEP_Tcp” protocol=“tcp“ />
</Endpoints>
    </WorkerRole>
</ServiceDefinition>
```

## <a name="check-load-balancer-health-status-for-cloud-services"></a>클라우드 서비스에 대한 부하 분산 장치 상태 확인

hello 다음은 상태 검색의 예입니다.

```xml
<LoadBalancerProbes>
    <LoadBalancerProbe name=“MyProbe” protocol=“http” path=“Probe.aspx” intervalInSeconds=“5” timeoutInSeconds=“100“ />
</LoadBalancerProbes>
```

hello 부하 분산 장치 결합 하 여 hello 끝점의 hello 정보와 hello 프로브 toocreate의 hello 정보 hello 형식의 URL `http://{DIP of VM}:80/Probe.aspx` hello 서비스의 hello 상태를 사용 하는 tooquery 일 수 있는 합니다.

hello 서비스에서 검색 주기 프로브 hello에서 동일한 IP 주소입니다. Hello 가상 컴퓨터가 실행 되 고 hello 노드의 hello 호스트에서 들어오는 hello 상태 프로브 요청입니다. hello 서비스는 hello 부하 분산 장치 tooassume hello 서비스가 정상 임을 대 한 HTTP 200 상태 코드로 toorespond에 있습니다. 다른 모든 HTTP 상태는 hello 순환 순서에서 가상 컴퓨터는 직접 (예: 503) 코드.

또한 hello 프로브 정의 hello hello 프로브 빈도 제어합니다. 경우에 위의 hello 부하 분산 장치는 hello 끝점 마다 5 초를 검색 합니다. No로 대답 양의 10 초 (두 개의 프로브 간격) 동안 수신 되 면 hello 프로브 다운 가정 하 고 hello 가상 컴퓨터 순환 순서에서 사용 됩니다. 마찬가지로, 회전 hello 서비스는 양의 응답을 받을 경우 hello 서비스 다시 배치는 toorotation 바로 합니다. Hello 서비스는 변동이 간의 정상 및 비정상을 하는 경우 hello 부하 분산 장치 프로브 수에 대 한 정상까지 hello 서비스 백 toorotation toodelay hello 다시 도입을 결정할 수 있습니다.

Hello에 대 한 hello 서비스 정의 스키마를 확인 [상태 프로브](https://msdn.microsoft.com/library/azure/jj151530.aspx) 자세한 정보에 대 한 합니다.

## <a name="next-steps"></a>다음 단계

[내부 부하 분산 장치 구성 시작](load-balancer-get-started-ilb-arm-ps.md)

[부하 분산 장치 배포 모드 구성](load-balancer-distribution-mode.md)

[부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성](load-balancer-tcp-idle-timeout.md)

