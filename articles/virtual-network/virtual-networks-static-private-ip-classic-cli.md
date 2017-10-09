---
title: "Vm (클래식)-Azure CLI 1.0에 대 한 aaaConfigure 개인 IP 주소 | Microsoft Docs"
description: "Tooconfigure 개인 IP 주소를 사용 하 여 가상 컴퓨터 (클래식)에 대 한 Azure CLI (명령줄 인터페이스) 1.0 hello 하는 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17386acf-c708-4103-9b22-ff9bf04b778d
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 417a57181bcf5c2e6101bf3bdf63fc94ebc99df5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-cli-10"></a>Hello Azure CLI 1.0을 사용 하 여 가상 컴퓨터 (클래식)에 대 한 개인 IP 주소를 구성 합니다.

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

이 문서에서는 hello 클래식 배포 모델에 설명 합니다. 수도 있습니다 [hello 리소스 관리자 배포 모델에서 정적 개인 IP 주소 관리](virtual-networks-static-private-ip-arm-cli.md)합니다.

hello 샘플 Azure CLI 명령 아래에 이미 만든 단순한 환경이 필요 합니다. 이 문서에 표시 된 대로 toorun hello 명령을 원하는 경우 먼저 hello 테스트 환경을 구축에 설명 된 [vnet을 만든](virtual-networks-create-vnet-classic-cli.md)합니다.

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a>어떻게 toospecify 정적 개인 IP 주소는 VM을 만들 때
명명 된 새 VM toocreate *DNS01* 라는 새 클라우드 서비스에 *TestService* 위의 hello 시나리오에 따라, 다음이 단계를 수행 합니다.

1. Azure CLI 처음 사용 하는 경우 참조 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md) Azure 계정 및 구독을 선택 하면 toohello 포인트 hello 지침을 따릅니다.
2. Hello 실행 **azure 서비스를 만들** toocreate hello 클라우드 서비스 명령입니다.
   
        azure service create TestService --location uscentral
   
    예상 출력:
   
        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name TestService
        info:    service create command OK
3. Hello 실행 **azure vm 만들기** 명령 toocreate hello VM입니다. 개인 고정 IP 주소에 대 한 hello 값을 확인 합니다. hello 출력 뒤에 표시 된 hello 목록 사용 되는 hello 매개 변수를 설명 합니다.
   
        azure vm create -l centralus -n DNS01 -w TestVNet -S "192.168.1.101" TestService bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 adminuser AdminP@ssw0rd
   
    예상 출력:
   
        info:    Executing command vm create
        warn:    --vm-size has not been specified. Defaulting too"Small".
        info:    Looking up image bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
        info:    Looking up virtual network
        info:    Looking up cloud service
        warn:    --location option will be ignored
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Retrieving storage accounts
        info:    Creating VM
        info:    OK
        info:    vm create command OK
   
   * **-l(또는 --location)**. Azure 지역 hello VM 만들어집니다. 이 시나리오에서는 *centralus*입니다.
   * **-n(또는 --vm-name)**. 만든 hello VM toobe의 이름입니다.
   * **-w(또는 --virtual-network-name)**. Hello hello VM을 만들 위치는 VNet의 이름입니다. 
   * **-S(또는 --static-ip)**. Hello VM에 대 한 정적 개인 IP 주소를 선택 합니다.
   * **TestService**. Hello VM 만들어지는 hello 클라우드 서비스의 이름입니다.
   * **bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**. 이미지는 toocreate hello VM을 사용 합니다.
   * **adminuser**. Windows VM hello에 대 한 로컬 관리자입니다.
   * **AdminP@ssw0rd**. Windows VM hello에 대 한 로컬 관리자 암호입니다.

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>어떻게 tooretrieve 정적 개인 IP 주소는 VM에 대 한 정보
tooview hello 정적 개인 IP 주소 VM hello 다음 Azure CLI 명령을 실행 합니다. 위의 hello 스크립트를 사용 하 여 만든 hello에 대 한 정보 및 hello 값에 대 한 관찰 *네트워크 StaticIP*:

    azure vm static-ip show DNS01

예상 출력:

    info:    Executing command vm static-ip show
    info:    Getting virtual machines
    data:    Network StaticIP "192.168.1.101"
    info:    vm static-ip show command OK

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>어떻게 tooremove 정적 개인 IP는 VM에서을 해결합니다
VM toohello 다음 Azure CLI 명령이 실행된 hello 위의 hello 스크립트에 추가 하는 tooremove hello 정적 개인 IP 주소.

    azure vm static-ip remove DNS01

예상 출력:

    info:    Executing command vm static-ip remove
    info:    Getting virtual machines
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip remove command OK

## <a name="how-tooadd-a-static-private-ip-tooan-existing-vm"></a>어떻게 tooadd 정적 개인 IP tooan 기존 VM
정적 개인 IP 주소 toohello VM 사용 하 여 만든 녀석 위의 hello 스크립트 명령을 다음 tooadd:

    azure vm static-ip set DNS01 192.168.1.101

예상 출력:

    info:    Executing command vm static-ip set
    info:    Getting virtual machines
    info:    Looking up virtual network
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip set command OK

## <a name="next-steps"></a>다음 단계
* [예약된 공용 IP](virtual-networks-reserved-public-ip.md) 주소에 대해 알아봅니다.
* [ILPIP(인스턴스 수준 공용 IP)](virtual-networks-instance-level-public-ip.md) 주소에 대해 알아봅니다.
* Hello 참조 [예약 된 IP REST Api](https://msdn.microsoft.com/library/azure/dn722420.aspx)합니다.

