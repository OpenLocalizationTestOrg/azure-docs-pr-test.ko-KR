---
title: "클래식 Azure CLI aaaCreate 인터넷 연결 부하 분산 장치-| Microsoft Docs"
description: "인터넷 연결 부하 분산 장치에 사용 하 여 클래식 배포 모델 toocreate Azure CLI hello 하는 방법에 대해 알아봅니다"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: e433a824-4a8a-44d2-8765-a74f52d4e584
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: e6070cbc574f74bca0cccb960ff192847d6511bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-cli"></a>경우에 인터넷 연결 hello Azure CLI에에서 부하 분산 장치 (클래식)를 만들기 시작

> [!div class="op_single_selector"]
> * [Azure 클래식 포털](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Azure 클라우드 서비스](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Azure 리소스를 사용 하기 전에 Azure에 현재 두 가지 배포 모델에 중요 한 toounderstand: Azure 리소스 관리자 및 기본 합니다. Azure 리소스로 작업하기 전에 [배포 모델 및 도구](../azure-classic-rm.md) 를 이해해야 합니다. 이 문서의 hello 위쪽 hello 탭을 클릭 하 여 다양 한 도구에 대 한 hello 설명서를 볼 수 있습니다. 이 문서에서는 hello 클래식 배포 모델에 설명 합니다. 수도 있습니다 [toocreate 인터넷 연결 로드 분산 장치는 Azure 리소스 관리자를 사용 하는 방법에 대해 알아봅니다](load-balancer-get-started-internet-arm-ps.md)합니다.

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="step-by-step-creating-an-internet-facing-load-balancer-using-cli"></a>CLI를 사용하여 인터넷 연결 부하 분산 장치 만들기 단계별 지침

이 가이드에서는 toocreate는 인터넷 부하 분산 장치에 따라 방법 위의 hello 시나리오를 보여 줍니다.

1. Azure CLI 처음 사용 하는 경우 참조 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md) Azure 계정 및 구독을 선택 하면 toohello 포인트 hello 지침을 따릅니다.
2. Hello 실행 **azure 구성 모드** 아래와 같이 명령 tooswitch tooclassic 모드입니다.

    ```azurecli
    azure config mode asm
    ```

    예상 출력:

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a>끝점과 부하 분산 장치 집합 만들기

"web2" 만들어진와 hello 시나리오에서는 가상 컴퓨터 "web1" hello를 가정 합니다.
이 가이드를 통해 공용 포트로 포트 80과 로컬 포트로 포트 80을 사용하여 부하 분산 장치 집합을 만듭니다. 프로브 포트는 포트 80에 구성도 하 고 명명 된 hello 부하 분산 장치 "lbset"를 설정 합니다.

### <a name="step-1"></a>1단계

Hello 첫 번째 끝점을 만들고 부하 분산 장치를 사용 하 여 설정 `azure network vm endpoint create` "web1" 가상 컴퓨터에 대 한 합니다.

```azurecli
azure vm endpoint create web1 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-2"></a>2단계

두 번째 가상 컴퓨터 "web2" toohello 부하 분산 장치 집합을 추가 합니다.

```azurecli
azure vm endpoint create web2 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-3"></a>3단계

Hello 부하 분산 장치 사용 하 여 구성 확인 `azure vm show` 합니다.

```azurecli
azure vm show web1
```

hello 출력이 됩니다.

    data:    DNSName "contoso.cloudapp.net"
    data:    Location "East US"
    data:    VMName "web1"
    data:    IPAddress "10.0.0.5"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-2015
    6-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "joaoma-1-web1-0-201509251804250879"
    data:    OSDisk mediaLink "https://XXXXXXXXXXXXXXX.blob.core.windows.
    /vhds/joaomatest-web1-2015-09-25.vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Se
    r-2012-R2-20150916-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "XXXXXXXXXXXXXXXX"
    data:    VirtualIPAddresses 0 name "XXXXXXXXXXXXXXXXXXXX"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    Network Endpoints 0 loadBalancedEndpointSetName "lbset"
    data:    Network Endpoints 0 localPort 80
    data:    Network Endpoints 0 name "tcp-80-80"
    data:    Network Endpoints 0 port 80
    data:    Network Endpoints 0 loadBalancerProbe port 80
    data:    Network Endpoints 0 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 0 loadBalancerProbe intervalInSeconds 15
    data:    Network Endpoints 0 loadBalancerProbe timeoutInSeconds 31
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "XXXXXXXXXXXX"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 5986
    data:    Network Endpoints 1 name "PowerShell"
    data:    Network Endpoints 1 port 5986
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "XXXXXXXXXXXX"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 3389
    data:    Network Endpoints 2 name "Remote Desktop"
    data:    Network Endpoints 2 port 58081
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a>가상 컴퓨터를 위한 원격 데스크톱 끝점 만들기

원격 데스크톱 끝점 tooforward 네트워크 트래픽을 사용 하 여 특정 가상 컴퓨터에 대 한 공용 포트 tooa 로컬 포트를 만들 수 있습니다 `azure vm endpoint create`합니다.

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a>부하 분산 장치에서 가상 컴퓨터 제거

Toodelete hello 연결 된 끝점 toohello hello 가상 컴퓨터에서 부하 분산 장치 집합을 만들어야 합니다. Hello 끝점 기능이 제거 되 면 hello 가상 컴퓨터 부하 분산 집합을 더 이상을 toohello 속하지 않습니다.

위의 hello 예제를 사용 하 여 제거할 수 있습니다 "web1" 가상 컴퓨터에 대해 만든 hello 끝점 "lbset" hello 명령을 사용 하 여 부하 분산 장치에서 `azure vm endpoint delete`합니다.

```azurecli
azure vm endpoint delete web1 tcp-80-80
```

> [!NOTE]
> Hello 명령을 사용 하 여 더 많은 옵션 toomanage 끝점을 탐색할 수 있습니다.`azure vm endpoint --help`

## <a name="next-steps"></a>다음 단계

[내부 부하 분산 장치 구성 시작](load-balancer-get-started-ilb-arm-ps.md)

[부하 분산 장치 배포 모드 구성](load-balancer-distribution-mode.md)

[부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성](load-balancer-tcp-idle-timeout.md)
