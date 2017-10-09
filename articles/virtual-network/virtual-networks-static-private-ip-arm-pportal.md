---
title: "Vm-Azure 포털에 대 한 aaaConfigure 개인 IP 주소 | Microsoft Docs"
description: "Tooconfigure 개인 IP 주소를 사용 하 여 가상 컴퓨터에 대 한 Azure 포털을 hello 하는 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 11245645-357d-4358-9a14-dd78e367b494
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 474161303cdf8cb98e16ffd7cef6b74debdbc49a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 가상 컴퓨터에 대 한 개인 IP 주소를 구성 합니다.

> [!div class="op_single_selector"]
> * [Azure 포털](virtual-networks-static-private-ip-arm-pportal.md)
> * [PowerShell](virtual-networks-static-private-ip-arm-ps.md)
> * [Azure CLI](virtual-networks-static-private-ip-arm-cli.md)
> * [Azure Portal(클래식)](virtual-networks-static-private-ip-classic-pportal.md)
> * [PowerShell(클래식)](virtual-networks-static-private-ip-classic-ps.md)
> * [Azure CLI(클래식)](virtual-networks-static-private-ip-classic-cli.md)


[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

이 문서에서는 hello 리소스 관리자 배포 모델에 설명 합니다. 수도 있습니다 [hello 클래식 배포 모델에 개인 고정 IP 주소 관리](virtual-networks-static-private-ip-classic-pportal.md)합니다.

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

다음 hello 샘플 단계를 이미 만든 단순한 환경을 기대 합니다. 이 문서에 표시 된 대로 toorun hello 단계를 원하는 경우 먼저 hello 테스트 환경을 구축에 설명 된 [vnet을 만든](virtual-networks-create-vnet-arm-pportal.md)합니다.

## <a name="how-toocreate-a-vm-for-testing-static-private-ip-addresses"></a>개인 고정 IP를 테스트 하기 위한 VM toocreate 해결 하는 방법을
Hello Azure 포털을 사용 하 여 hello hello 리소스 관리자 배포 모드에서 vm을 만드는 동안 정적 개인 IP 주소를 설정할 수 없습니다. 다음 설정의 개인 IP toobe을 정적, VM hello를 먼저 만들어야 합니다.

toocreate 라는 VM *DNS01* hello에 *프런트 엔드* 라는 VNet의 서브넷 *TestVNet*, 아래의 hello 단계를 수행 합니다.

1. 브라우저에서 toohttp://portal.azure.com를 탐색 하 고, 필요한 경우 Azure 계정을 사용해 합니다.
2. 클릭 **새로** > **계산** > **Windows Server 2012 R2 Datacenter**, 해당 hello 확인 **배포모델선택** 목록 표시 이미 **리소스 관리자**, 클릭 하 고 **만들기**그림과 같이 hello 아래, 합니다.
   
    ![Azure 포털에서 VM 만들기](./media/virtual-networks-static-ip-arm-pportal/figure01.png)
3. Hello에 **기본 사항** 블레이드를 생성 하는 hello VM toobe의 hello 이름을 입력 (*DNS01* 시나리오에서), 로컬 관리자 계정 및 암호를 아래 hello 그림 에서처럼 hello 합니다.
   
    ![기본 사항 블레이드](./media/virtual-networks-static-ip-arm-pportal/figure02.png)
4. Hello 있는지 확인 **위치** 선택한 *중앙 미국*, 클릭 **기존 선택** 아래 **리소스 그룹**, 클릭**리소스 그룹** 클릭 한 다음 다시 *TestRG*, 클릭 하 고 **확인**합니다.
   
    ![기본 사항 블레이드](./media/virtual-networks-static-ip-arm-pportal/figure03.png)
5. Hello에 **크기 선택** 블레이드를 **표준 A1**, 클릭 하 고 **선택**합니다.
   
    ![크기 선택 블레이드](./media/virtual-networks-static-ip-arm-pportal/figure04.png)    
6. 에 **설정** 블레이드에서 확인 되었는지 hello 다음 속성이 설정 된 아래의 hello 값으로 설정 되 고 클릭 **확인**합니다.
   
    -**저장소 계정**: *vnetstorage*
   
   * **네트워크**: *TestVNet*
   * **서브넷**: *FrontEnd*
     
     ![크기 선택 블레이드](./media/virtual-networks-static-ip-arm-pportal/figure05.png)     
7. Hello에 **요약** 블레이드에서 클릭 **확인**합니다. 공지 hello 타일 아래에 대시보드를 표시 합니다.
   
    ![Azure 포털에서 VM 만들기](./media/virtual-networks-static-ip-arm-pportal/figure06.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>어떻게 tooretrieve 정적 개인 IP 주소는 VM에 대 한 정보
tooview hello 정적 개인 IP 주소 정보 hello에 대 한 위의 hello 단계를 사용 하 여 만든 VM 아래 hello 단계를 실행 합니다.

1. Hello Azure Azure 포털에서 클릭 **모두 찾아보기** > **가상 컴퓨터** > **DNS01** > **모든 설정** > **네트워크 인터페이스** 나열 된 hello 유일한 네트워크 인터페이스에서 다음을 클릭 합니다.
   
    ![VM 타일 배포](./media/virtual-networks-static-ip-arm-pportal/figure07.png)
2. Hello에 **네트워크 인터페이스** 블레이드에서 클릭 **모든 설정을** > **IP 주소** 및 통지 hello **할당** 및 **IP 주소** 값입니다.
   
    ![VM 타일 배포](./media/virtual-networks-static-ip-arm-pportal/figure08.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a>정적 개인 IP tooadd tooan 기존 VM을 처리 하는 방법
아래의 hello 단계를 수행 하는 tooadd는 정적 개인 IP 주소 toohello 위의 hello 단계를 사용 하 여 만든 VM:

1. Hello에서 **IP 주소** 위에 표시 된 블레이드 클릭 **정적** 아래 **할당**합니다.
2. **IP 주소**에 *192.168.1.101*을 입력하고 **저장**을 클릭합니다.
   
    ![Azure 포털에서 VM 만들기](./media/virtual-networks-static-ip-arm-pportal/figure09.png)

> [!NOTE]
> 클릭 한 후 if **저장** hello 할당 너무 설정 않음을 알게**동적**, 입력 한 hello IP 주소를 이미 사용 중임을 의미 합니다. 다른 IP 주소로 시도하세요.
> 
> 

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>어떻게 tooremove 정적 개인 IP는 VM에서을 해결합니다
tooremove hello 정적 개인 IP 주소, 위에서 만든 VM hello에서 단계 다음에 나오는 hello를 완료 합니다.

Hello에서 **IP 주소** 위에 표시 된 블레이드 클릭 **동적** 아래 **할당**, 클릭 하 고 **저장**합니다.

## <a name="next-steps"></a>다음 단계
* [예약된 공용 IP](virtual-networks-reserved-public-ip.md) 주소에 대해 알아봅니다.
* [ILPIP(인스턴스 수준 공용 IP)](virtual-networks-instance-level-public-ip.md) 주소에 대해 알아봅니다.
* Hello 참조 [예약 된 IP REST Api](https://msdn.microsoft.com/library/azure/dn722420.aspx)합니다.

