---
title: "서비스 구성 파일에서 DNS 설정을 aaaSpecifying | Microsoft Docs"
description: "가상 네트워크에 대한 서비스 구성 파일을 사용하여 사용자 지정 DNS 설정 지정"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 467a4b99-8691-40b3-b640-e25e49675c71
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/24/2016
ms.author: jdial
ms.openlocfilehash: f192e33566dd8e669da04e6378a0c8e4b0b35ecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-dns-settings-in-a-service-configuration-file"></a>서비스 구성 파일에서 DNS 설정 지정
## <a name="dns-elements"></a>DNS 요소
서비스 구성 파일에는 hello 서비스가 사용 하는 hello 도메인 이름 (DNS System) 서버에 대 한 IPv4 주소 목록이 들어 있는 DnsServers 요소가 포함 될 수 있습니다. Hello 서비스 구성 파일의 설정은 hello 네트워크 구성 파일의 설정 보다 우선합니다. 자세한 내용은 [Azure 서비스 구성 스키마(.cscfg 파일)](https://msdn.microsoft.com/library/azure/ee758710.aspx)를 참조하세요.

**네트워크 구성 요소**

      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>

> [!WARNING]
> hello **이름** hello에 대 한 특성 **DnsServer** 요소 참조 이름 으로만 사용 됩니다. DNS 서버 hello에 대 한 호스트 이름을 hello를 표시 하지 않습니다. 각 **DnsServer** 특성 값 hello 전체 Microsoft Azure 구독에서 고유 해야 합니다.
> 
> 

## <a name="see-also"></a>참고 항목
[Azure 서비스 구성 스키마(.cscfg)](https://msdn.microsoft.com/library/windowsazure/ee758710)

[Azure 가상 네트워크 구성 스키마](http://go.microsoft.com/fwlink/?LinkId=248093)

[네트워크 구성 파일을 사용하여 가상 네트워크 구성](http://go.microsoft.com/fwlink/?LinkId=248094)

[Hello 관리 포털의에서 가상 네트워크 설정에 대 한](http://go.microsoft.com/fwlink/?LinkId=248092)

