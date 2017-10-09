---
title: "가상 네트워크 구성 파일에서 DNS 설정을 aaaSpecifying | Microsoft Docs"
description: "가상 네트워크 구성을 사용 하 여 가상 네트워크의 DNS 서버 설정을 toochange hello 클래식 배포 모델에서 파일을 어떻게"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a8905927-92ac-42b5-8c33-8e42c000692c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.openlocfilehash: d53a658773e1c930b5a28a701db0be9edd26565e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-dns-settings-in-a-virtual-network-configuration-file"></a>가상 네트워크 구성 파일에서 DNS 설정 지정
네트워크 구성 파일을 두 개의 요소가 toospecify 도메인 이름 (DNS System) 설정을 사용할 수 있는: **DnsServers** 및 **DnsServerRef**합니다. IP 주소를 지정 하 여 DNS 서버 목록을 추가할 수 있으며 이름 toohello 참조 **DnsServers** 요소입니다. 그런 다음 사용할 수는 **DnsServerRef** 요소 toospecify hello DnsServers 요소에서 DNS 서버 항목은 가상 네트워크 내의 다른 네트워크 사이트에 사용 됩니다.

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

이 문서에서는 hello 클래식 배포 모델에 설명 합니다.

hello 네트워크 구성 파일 요소 다음 hello를 포함할 수 있습니다. hello 각 요소의 제목은 값 설정 hello 요소에 대 한 추가 정보를 제공 하는 연결 된 tooa 페이지입니다.

> [!IMPORTANT]
> 어떻게 tooconfigure hello 네트워크 구성 파일에 대 한 정보를 참조 하십시오. [네트워크 구성 파일을 사용 하 여 가상 네트워크 구성](virtual-networks-using-network-configuration-file.md)합니다. Hello 네트워크 구성 파일에 포함 된 각 요소에 대 한 정보를 참조 하십시오. [Azure 가상 네트워크 구성 스키마](https://msdn.microsoft.com/library/azure/jj157100.aspx)합니다.
> 
> 

[Dns 요소](http://go.microsoft.com/fwlink/?LinkId=248093)

    <Dns>
      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>
    </Dns>

> [!WARNING]
> hello **이름** hello에 대 한 특성 **DnsServer** 요소 hello에 대 한 참조로만 사용 됩니다 **DnsServerRef** 요소입니다. DNS 서버 hello에 대 한 호스트 이름을 hello를 표시 하지 않습니다. 각 **DnsServer** 특성 값 hello 전체 Microsoft Azure 구독에서 고유 해야
> 
> 

[가상 네트워크 사이트 요소](http://go.microsoft.com/fwlink/?LinkId=248093)

    <DnsServersRef>
      <DnsServerRef name="ID1" />
      <DnsServerRef name="ID2" />
      <DnsServerRef name="ID3" />
    </DnsServersRef>

> [!NOTE]
> 주문 toospecify hello 가상 네트워크 사이트 요소에 대 한이 설정은, 이전에 hello DNS 요소에 정의 되어야 합니다. hello DnsServerRef *이름* hello 가상 네트워크 사이트 요소 dns 서버에 대 한 hello DNS 요소에 지정 된 tooa 이름 값을 참조 해야 *이름*합니다.
> 
> 

## <a name="next-steps"></a>다음 단계
* Hello 이해 [Azure 가상 네트워크 구성 스키마](http://go.microsoft.com/fwlink/?LinkId=248093)합니다.
* Hello 이해 [Azure 서비스 구성 스키마](https://msdn.microsoft.com/library/windowsazure/ee758710)합니다.
* [네트워크 구성 파일을 사용하여 가상 네트워크 구성](virtual-networks-using-network-configuration-file.md)

