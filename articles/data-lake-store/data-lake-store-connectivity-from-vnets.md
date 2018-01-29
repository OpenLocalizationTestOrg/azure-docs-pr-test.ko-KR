---
title: "Vnet에서 Azure Data Lake Store 연결 | Microsoft 문서"
description: "Azure VNET에서 Azure Data Lake Store에 연결합니다."
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
ms.date: 08/28/2017
ms.author: nitinme
ms.openlocfilehash: 029939eabc7283d7591576fa1b14731a9e626a88
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="access-azure-data-lake-store-from-vms-within-an-azure-vnet"></a>Azure VNET 내 VM에서 Azure Data Lake Store 액세스
Azure Data Lake Store는 공용 인터넷 IP 주소에서 실행되는 PaaS 서비스입니다. 공용 인터넷에 연결할 수 있는 서버는 일반적으로 Azure Data Lake Store 끝점에도 연결할 수 있습니다. 기본적으로 Azure VNET에 있는 모든 VM은 인터넷에 액세스할 수 있으므로 Azure Data Lake Store에 액세스할 수 있습니다. 그러나 VNET에서 VM을 인터넷에 액세스하지 못하도록 구성할 수 있습니다. 이러한 VM의 경우 Azure Data Lake Store에 대한 액세스도 제한됩니다. Azure VNET의 VM에 대한 공용 인터넷 액세스를 차단하려면 다음 방법 중 하나를 사용하여 수행할 수 있습니다.

* NSG(네트워크 보안 그룹) 구성
* UDR(사용자 정의 경로) 구성
* BGP(업계 표준 동적 라우팅 프로토콜)를 통해 경로 교환(ExpressRoute를 사용하여 인터넷에 대한 액세스를 차단하는 경우)

이 문서에서는 위에서 나열한 세 가지 방법 중 하나를 사용하여 리소스에 액세스하도록 제한된 Azure VM에서 Azure Data Lake Store에 액세스할 수 있도록 설정하는 방법을 알아봅니다.

## <a name="enabling-connectivity-to-azure-data-lake-store-from-vms-with-restricted-connectivity"></a>연결이 제한된 VM에서 Azure Data Lake Store에 대한 연결 사용 설정
이러한 VM에서 Azure Data Lake Store에 액세스하려면 Azure Data Lake Store 계정을 사용할 수 있는 IP 주소에 액세스하도록 구성해야 합니다. 계정의 DNS 이름(`<account>.azuredatalakestore.net`)을 확인하여 Data Lake Store 계정의 IP 주소를 식별할 수 있습니다. 이를 위해 **nslookup**와 같은 도구를 사용할 수 있습니다. 컴퓨터에서 명령 프롬프트를 열고 다음 명령을 실행합니다.

    nslookup mydatastore.azuredatalakestore.net

출력은 다음과 비슷합니다. **Address** 속성에 대한 값은 Data Lake Store 계정과 연결된 IP 주소입니다.

    Non-authoritative answer:
    Name:    1434ceb1-3a4b-4bc0-9c69-a0823fd69bba-mydatastore.projectcabostore.net
    Address:  104.44.88.112
    Aliases:  mydatastore.azuredatalakestore.net


### <a name="enabling-connectivity-from-vms-restricted-by-using-nsg"></a>NSG를 사용하여 제한된 VM에서 연결을 사용하도록 설정
NSG 규칙을 사용하여 인터넷 액세스를 차단하면 Data Lake Store IP 주소에 액세스할 수 있는 다른 NSG를 만들 수 있습니다. NSG 규칙에 대한 자세한 내용은 [네트워크 보안 그룹이란?](../virtual-network/virtual-networks-nsg.md)을 참조하세요. NSG를 만드는 방법에 대한 지침은 [Azure Portal을 사용하여 NSG를 관리하는 방법](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)을 참조하세요.

### <a name="enabling-connectivity-from-vms-restricted-by-using-udr-or-expressroute"></a>UDR 또는 ExpressRoute를 사용하여 제한된 VM에서 연결을 사용하도록 설정
UDR 또는 BGP 교환 경로 중 하나를 사용하여 인터넷 액세스를 차단하는 경우 해당 서브넷의 VM이 Data Lake Store 끝점에 액세스할 수 있도록 특별한 경로를 구성해야 합니다. 자세한 내용은 [사용자 정의 경로란?](../virtual-network/virtual-networks-udr-overview.md)을 참조하세요. UDR 만들기에 대한 지침은 [Resource Manager에서 UDR 만들기](../virtual-network/virtual-network-create-udr-arm-ps.md)를 참조하세요.

### <a name="enabling-connectivity-from-vms-restricted-by-using-expressroute"></a>ExpressRoute를 사용하여 제한된 VM에서 연결을 사용하도록 설정
ExpressRoute 회로가 구성되면 온-프레미스 서버는 공용 피어링을 통해 Data Lake Store에 액세스할 수 있습니다. 공용 피어링을 위한 ExpressRoute 구성에 대한 자세한 내용은 [ExpressRoute FAQ](../expressroute/expressroute-faqs.md)에서 확인할 수 있습니다.

## <a name="see-also"></a>참고 항목
* [Azure Data Lake Store 개요](data-lake-store-overview.md)
* [Azure Data Lake Store에 저장된 데이터 보호](data-lake-store-security-overview.md)

