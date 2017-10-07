---
title: "데이터 레이크 저장소 Vnet에서 aaaConnect tooAzure | Microsoft Docs"
description: "Azure Vnet에서 tooAzure 데이터 레이크 저장소 연결"
services: data-lake-store,data-catalog
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 683fcfdc-cf93-46c3-b2d2-5cb79f5e9ea5
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: c695dcf49fe4e1a87a90729cf085a938f3b51fe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="access-azure-data-lake-store-from-vms-within-an-azure-vnet"></a>Azure VNET 내 VM에서 Azure Data Lake Store 액세스
Azure Data Lake Store는 공용 인터넷 IP 주소에서 실행되는 PaaS 서비스입니다. 일반적으로 toohello 공용 인터넷 수를 연결할 수 있는 모든 서버 tooAzure 데이터 레이크 저장소 끝점으로 연결 합니다. 기본적으로 Azure Vnet에 있는 모든 Vm hello 인터넷에 액세스할 수 있습니다 및 따라서 Azure 데이터 레이크 저장소에 액세스할 수 있습니다. 그러나 VNET toonot의 가능한 tooconfigure Vm은 인터넷 액세스 toohello 있어야 합니다. 이러한 Vm에 대 한 액세스 tooAzure 데이터 레이크 저장소 제한도 됩니다. Azure Vnet의 Vm에 대 한 공용 인터넷 액세스가 차단 수행할 수 있습니다 hello 방법 중 하나를 사용 하 여 합니다.

* NSG(네트워크 보안 그룹) 구성
* UDR(사용자 정의 경로) 구성
* BGP (업계 표준 동적 라우팅 프로토콜)를 통해 경로 교환 하 여 ExpressRoute 사용 되는 경우 해당 블록 toohello 인터넷 액세스

이 문서에서는 tooenable 제한 tooaccess hello 세 가지 방법 중 하나를 사용 하 여 리소스 위에 나열 된는 Azure Vm에서 toohello Azure Data Lake 저장소에 액세스 하는 방법을 배웁니다.

## <a name="enabling-connectivity-tooazure-data-lake-store-from-vms-with-restricted-connectivity"></a>제한 된 연결에 사용할 수 있도록 연결 tooAzure Vm에서 데이터 레이크 저장소
이러한 Vm에서 tooaccess Azure 데이터 레이크 저장소, Azure 데이터 레이크 저장소 계정 hello를 사용할 수 있는 tooaccess hello IP 주소 구성 해야 합니다. 계정을 hello DNS 이름을 확인 하 여 데이터 레이크 저장소 계정에 대 한 hello IP 주소를 확인할 수 있습니다 (`<account>.azuredatalakestore.net`). 이를 위해 **nslookup**와 같은 도구를 사용할 수 있습니다. 컴퓨터에서 명령 프롬프트를 열고 hello 다음 명령을 실행 합니다.

    nslookup mydatastore.azuredatalakestore.net

hello 출력 hello 다음과 유사 합니다. 에 대 한 가치 hello **주소** 속성은 데이터 레이크 저장소 계정에 연결 된 hello IP 주소입니다.

    Non-authoritative answer:
    Name:    1434ceb1-3a4b-4bc0-9c69-a0823fd69bba-mydatastore.projectcabostore.net
    Address:  104.44.88.112
    Aliases:  mydatastore.azuredatalakestore.net


### <a name="enabling-connectivity-from-vms-restricted-by-using-nsg"></a>NSG를 사용하여 제한된 VM에서 연결을 사용하도록 설정
그러면 액세스 toohello 데이터 레이크 저장소 IP 주소를 허용 하는 다른 NSG를 만들 수 있습니다 NSG 규칙은 사용 tooblock toohello 인터넷에 액세스 합니다. NSG 규칙에 대한 자세한 내용은 [네트워크 보안 그룹이란?](../virtual-network/virtual-networks-nsg.md)을 참조하세요. Toocreate Nsg 확인 하는 방법에 대 한 지침은 [어떻게 toomanage Nsg를 사용 하 여 Azure 포털을 hello](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)합니다.

### <a name="enabling-connectivity-from-vms-restricted-by-using-udr-or-expressroute"></a>UDR 또는 ExpressRoute를 사용하여 제한된 VM에서 연결을 사용하도록 설정
경로, UDRs 하거나 BGP 교환 경로 사용 되는 tooblock 액세스 toohello 인터넷을 특수 경로 toobe Vm 이러한 서브넷에 있는 데이터 레이크 저장소 끝점에 액세스할 수 있도록 구성 해야 합니다. 자세한 내용은 [사용자 정의 경로란?](../virtual-network/virtual-networks-udr-overview.md)을 참조하세요. UDR 만들기에 대한 지침은 [Resource Manager에서 UDR 만들기](../virtual-network/virtual-network-create-udr-arm-ps.md)를 참조하세요.

### <a name="enabling-connectivity-from-vms-restricted-by-using-expressroute"></a>ExpressRoute를 사용하여 제한된 VM에서 연결을 사용하도록 설정
ExpressRoute 회로 구성 된 온-프레미스 서버 hello 데이터 레이크 저장소 공용 피어 링을 통해 액세스할 수 있습니다. 공용 피어링을 위한 ExpressRoute 구성에 대한 자세한 내용은 [ExpressRoute FAQ](../expressroute/expressroute-faqs.md)에서 확인할 수 있습니다.

## <a name="see-also"></a>참고 항목
* [Azure Data Lake Store 개요](data-lake-store-overview.md)
* [Azure Data Lake Store에 저장된 데이터 보호](data-lake-store-security-overview.md)

