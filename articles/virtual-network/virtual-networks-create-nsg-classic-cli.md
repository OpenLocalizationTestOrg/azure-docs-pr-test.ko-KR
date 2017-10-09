---
title: "사용 하 여 클래식 모드로 aaaHow toocreate Nsg hello Azure CLI | Microsoft Docs"
description: "자세한 내용은 방법 toocreate hello Azure CLI를 사용 하 여 클래식 모드에서 Nsg를 배포 하 고"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: 17d98950-5fbb-4653-bef6-d822ab37541e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: eb78861e10a0dd950bb2c3783ee957d1cce55016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-nsgs-classic-in-hello-azure-cli"></a>Toocreate Nsg (클래식)를 Azure CLI hello 하는 방법
[!INCLUDE [virtual-networks-create-nsg-selectors-classic-include](../../includes/virtual-networks-create-nsg-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

이 문서에서는 hello 클래식 배포 모델에 설명 합니다. 수도 있습니다 [hello 리소스 관리자 배포 모델에서 Nsg 만들기](virtual-networks-create-nsg-arm-cli.md)합니다.

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

hello 샘플 Azure CLI 명령 아래에 이미 위의 hello 시나리오를 기반으로 만들어진 단순 환경이 필요 합니다. 이 문서에 표시 된 대로 toorun hello 명령을 원하는 경우 먼저 hello 테스트 환경을 구축 하 여 [VNet을 만드는](virtual-networks-create-vnet-classic-cli.md)합니다.

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a>Toocreate NSG hello 프런트 엔드 서브넷에 대 한 hello 하는 방법
명명 된 NSG 라는 toocreate **NSG 프런트 엔드** 아래 hello 단계에 따라 위의 hello 시나리오에 따라, 합니다.

1. Azure CLI 처음 사용 하는 경우 참조 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md) Azure 계정 및 구독을 선택 하면 toohello 포인트 hello 지침을 따릅니다.
2. Hello 실행  **`azure config mode`**  아래와 같이 명령 tooswitch tooclassic 모드입니다.
   
        azure config mode asm
   
    예상 출력:
   
        info:    New mode is asm
3. Hello 실행  **`azure network nsg create`**  명령 toocreate NSG 합니다.
   
        azure network nsg create -l uswest -n NSG-FrontEnd
   
    예상 출력:
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : NSG-FrontEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    매개 변수
   
   * **-l(또는 --location)**. Azure 지역 hello 새 NSG를 만들 위치입니다. 이 시나리오에서는 *westus*입니다.
   * **-n (or --name)**. Hello에 대 한 이름을 새 NSG 합니다. 이 시나리오에서는 *NSG-FrontEnd*입니다.
4. Hello 실행  **`azure network nsg rule create`**  명령 toocreate hello 인터넷에서에서 액세스 tooport 3389 (RDP)를 허용 하는 규칙입니다.
   
        azure network nsg rule create -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    예상 출력:
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : rdp-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 3389
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
   
    매개 변수
   
   * **-a(또는 --nsg-name)**. Hello NSG 규칙 만들 수 있는 hello의 이름입니다. 이 시나리오에서는 *NSG-FrontEnd*입니다.
   * **-n (or --name)**. Hello 새 규칙의 이름입니다. 이 시나리오에서는 *rdp-rule*입니다.
   * **-c(또는 --action)**. Hello 규칙 (Deny 또는 허용)에 대 한 액세스 수준입니다.
   * **-p(또는 --protocol)**. 프로토콜 (Tcp, Udp 또는 *) hello 규칙에 대 한 합니다.
   * **-r(또는 --type)**. 연결 방향(인바운드 또는 아웃바운드)입니다.
   * **-y(또는 --priority)**. Hello 규칙에 대 한 우선 순위입니다.
   * **-f(또는 --source-address-prefix)**. CIDR 또는 기본 태그를 사용하는 원본 주소 접두사입니다.
   * **-o(또는 --source-port-range)**. 원본 포트 또는 포트 범위입니다.
   * **-e(또는 --destination-address-prefix)**. CIDR 또는 기본 태그를 사용하는 대상 주소 접두사입니다.
   * **-u(또는 --destination-port-range)**. 대상 포트 또는 포트 범위입니다.
5. Hello 실행  **`azure network nsg rule create`**  명령 toocreate hello 인터넷에서에서 액세스 tooport 80 (HTTP)를 허용 하는 규칙입니다.
   
        azure network nsg rule create -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    예상 출력:
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 200
        info:    network nsg rule create command OK
6. Hello 실행  **`azure network nsg subnet add`**  명령 toolink hello NSG toohello 프런트 엔드 서브넷입니다.
   
        azure network nsg subnet add -a NSG-FrontEnd --vnet-name TestVNet --subnet-name FrontEnd
   
    예상 출력:
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-FrontEnd"
        info:    network nsg subnet add command OK

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a>Toocreate hello NSG 다시 hello에 대 한 서브넷을 종료 하는 방법
명명 된 NSG 라는 toocreate *NSG 백 엔드* 아래 hello 단계에 따라 위의 hello 시나리오에 따라, 합니다.

1. Hello 실행  **`azure network nsg create`**  명령 toocreate NSG 합니다.
   
        azure network nsg create -l uswest -n NSG-BackEnd
   
    예상 출력:
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : NSG-BackEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    매개 변수
   
   * **-l(또는 --location)**. Azure 지역 hello 새 NSG를 만들 위치입니다. 이 시나리오에서는 *westus*입니다.
   * **-n (or --name)**. Hello에 대 한 이름을 새 NSG 합니다. 이 시나리오에서는 *NSG-FrontEnd*입니다.
2. Hello 실행  **`azure network nsg rule create`**  명령 toocreate hello 프런트 엔드 서브넷의 액세스 tooport 1433 (SQL)를 허용 하는 규칙입니다.
   
        azure network nsg rule create -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    예상 출력:
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : sql-rule
        data:    Source address prefix           : 192.168.1.0/24
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 1433
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
3. Hello 실행  **`azure network nsg rule create`**  명령 toocreate 액세스 toohello 인터넷 거부 하는 규칙입니다.
   
        azure network nsg rule create -a NSG-BackEnd -n web-rule -c Deny -p Tcp -r Outbound -y 200 -f * -o * -e Internet -u 80
   
    예상 출력:
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : *
        data:    Source Port                     : *
        data:    Destination address prefix      : INTERNET
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Outbound
        data:    Action                          : Deny
        data:    Priority                        : 200
        info:    network nsg rule create command OK
4. Hello 실행  **`azure network nsg subnet add`**  명령 toolink hello NSG toohello 다시 서브넷을 종료 합니다.
   
        azure network nsg subnet add -a NSG-BackEnd --vnet-name TestVNet --subnet-name BackEnd
   
    예상 출력:
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-BackEndX"
        info:    Looking up hello subnet "BackEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-BackEndX"
        info:    network nsg subnet add command OK

