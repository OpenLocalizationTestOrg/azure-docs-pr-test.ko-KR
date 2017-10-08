---
title: "Azure 클라우드 서비스에 대 한 내부 부하 분산 장치는 aaaCreate | Microsoft Docs"
description: "내부 프로그램 toocreate hello 클래식 배포 모델에서 PowerShell을 사용 하 여 분산 장치를 로드 하는 방법에 대해 알아봅니다"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 57966056-0f46-4f95-a295-483ca1ad135d
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: fe7975bca7bec3248626b0ad0fad6823e278ade2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-for-cloud-services"></a>클라우드 서비스를 위한 내부 부하 분산 장치(클래식) 만들기 시작

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [Cloud services](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

> [!IMPORTANT]
> Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.  이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다. 너무 방법에 대해 알아봅니다[hello 리소스 관리자 모델을 사용 하 여 이러한 단계를 수행](load-balancer-get-started-ilb-arm-ps.md)합니다.

## <a name="configure-internal-load-balancer-for-cloud-services"></a>클라우드 서비스에 대한 내부 부하 분산 장치 구성하기

내부 부하 분산 장치는 가상 컴퓨터 및 클라우드 서비스를 모두 지원합니다. 지역 가상 네트워크 외부에 있는 클라우드 서비스에서 만든 내부 부하 분산 장치 끝점 hello 클라우드 서비스 내 에서만 액세스할 수 있습니다.

내부 부하 분산 장치 구성에 hello toobe hello 샘플 아래와 같이 hello hello hello 클라우드 서비스에 대 한 첫 번째 배포를 만드는 동안 설정에 있습니다.

> [!IMPORTANT]
> 다음 필수 구성 요소 toorun hello 단계 toohave hello 클라우드 배포를 위해 이미 만든 가상 네트워크입니다. 가상 네트워크 이름 및 서브넷 이름 toocreate hello 내부 부하 분산 hello 필요 합니다.

### <a name="step-1"></a>1단계

Visual Studio에서 클라우드 배포에 대 한 hello 서비스 구성 파일 (.cscfg)을 열고 마지막 섹션 toocreate hello 내부 부하 분산 hello 아래에서 다음 hello 추가 "`</Role>`" hello 네트워크 구성에 대 한 항목입니다.

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="name of hello load balancer">
        <FrontendIPConfiguration type="private" subnet="subnet-name" staticVirtualNetworkIPAddress="static-IP-address"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

Hello 네트워크 구성 파일 tooshow 모양을 대 한 hello 값을 추가 해 보겠습니다. Hello 예제에서는 "test_vnet" test_subnet 및 고정 IP 10.0.0.4 라는 서브넷 10.0.0.0/24를 사용 하 여 호출 VNet을 만든 가정 합니다. testLB hello 부하 분산 장치에 이름이 지정 됩니다.

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="testLB">
        <FrontendIPConfiguration type="private" subnet="test_subnet" staticVirtualNetworkIPAddress="10.0.0.4"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

Hello 부하 분산 장치 스키마에 대 한 자세한 내용은 참조 [부하 분산 장치 추가](https://msdn.microsoft.com/library/azure/dn722411.aspx)합니다.

### <a name="step-2"></a>2단계

Hello 서비스 정의 (.csdef) 파일 tooadd 끝점 toohello 내부 부하 분산을 변경 합니다. hello 순간 역할 인스턴스가 만들어지고, hello 서비스 정의 파일 내부 부하 분산 hello 역할 인스턴스 toohello를 추가 합니다.

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancer="load-balancer-name" />
    </Endpoints>
</WorkerRole>
```

위의 hello 예제에서 값 hello, 다음 hello 값 toohello 서비스 정의 파일을 추가 해 보겠습니다.

```xml
<WorkerRole name="WorkerRole1" vmsize="A7" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="endpoint1" protocol="http" localPort="80" port="80" loadBalancer="testLB" />
    </Endpoints>
</WorkerRole>
```

hello 네트워크 트래픽 부하 균형 hello testLB 부하 분산 장치 포트 80을 사용 하 여 들어오는 요청을 보내는 tooworker 역할 인스턴스에 또한 포트 80에 대 한 사용 됩니다.

## <a name="next-steps"></a>다음 단계

[원본 IP 선호도를 사용하여 부하 분산 장치 배포 모드 구성](load-balancer-distribution-mode.md)

[부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성](load-balancer-tcp-idle-timeout.md)

