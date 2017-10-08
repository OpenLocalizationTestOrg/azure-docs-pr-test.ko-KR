---
title: "aaaAzure DNS 위임 개요 | Microsoft Docs"
description: "이름을 어떻게 지정 toochange 도메인 위임 및 Azure DNS를 사용 하 여 서버 tooprovide 도메인 호스팅 이해 합니다."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 257da6ec-d6e2-4b6f-ad76-ee2dde4efbcc
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: gwallace
ms.openlocfilehash: eaf2d2e345004b4d631e8d81d548b8ca23277d05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="delegation-of-dns-zones-with-azure-dns"></a>Azure DNS를 사용하여 DNS 영역 위임

Azure DNS toohost DNS 영역을 허용 하 고 Azure에서 도메인에 대 한 hello DNS 레코드를 관리 합니다. 도메인 tooreach Azure DNS에 대 한 DNS 쿼리에 대 한 순서로 hello 도메인에 toobe tooAzure DNS hello 부모 도메인에서 위임 합니다. Azure DNS에 유의 hello 도메인 등록 기관 않습니다. 이 문서에 설명 하 고 도메인 위임 작동 방법 toodelegate 도메인 tooAzure DNS 합니다.

## <a name="how-dns-delegation-works"></a>DNS 위임의 작동 방식

### <a name="domains-and-zones"></a>도메인 및 영역

Domain Name System hello 도메인의 계층입니다. hello 계층 구조 이름이 단순히 hello '루트' 도메인에서 시작 '**.**'.  그 아래에 'com', 'net', 'org', 'uk' 또는 'jp'와 같은 최상위 도메인이 있습니다.  이러한 최상위 수준 도메인 아래는 'org.uk' 또는 'co.jp'와 같은 두 번째 수준의 도메인입니다.  방식으로 계속됩니다. hello 도메인 hello DNS 계층 구조에에서 별도 DNS 영역을 사용 하 여 호스팅됩니다. 이러한 영역 전체적으로 배포 됩니다 hello 전 세계 DNS 이름 서버에서 호스트.

**DNS 영역** -도메인 Domain Name System, 예를 들어 만든 'contoso.com' hello에는 고유 이름입니다. DNS 영역에는 특정 도메인에 대 한 사용 되는 toohost hello DNS 레코드입니다. 예를 들어 '만든 contoso.com' hello 도메인 (메일 서버)에 대 한 ' mail.contoso.com' 및 'www.contoso.com' (웹 사이트)에 대 한 같은 여러 DNS 레코드를 포함할 수 있습니다.

**도메인 등록 기관** - 도메인 등록 기관은 인터넷 도메인 이름을 제공할 수 있는 회사입니다. 원하는 hello 인터넷 도메인 toouse 사용할 수 있으며 toopurchase 수 있도록 확인 것입니다. Hello 도메인 이름 등록 되 면 hello 도메인 이름에 대 한 hello 법적 소유자가 됩니다. 인터넷 도메인을 이미 보유 하는 경우에 hello 현재 도메인 등록 기관 toodelegate tooAzure DNS를 사용 합니다.

지정 된 도메인 이름, 소유자 또는 방법에 대 한 자세한 내용을 toofind toobuy 도메인에 참조 [Azure AD의 인터넷 도메인 관리](https://msdn.microsoft.com/library/azure/hh969248.aspx)합니다.

### <a name="resolution-and-delegation"></a>확인 및 위임

DNS 서버에는 다음 두 가지 유형이 있습니다.

* *권한이 있는* DNS 서버는 DNS 영역을 호스트합니다. 해당 영역의 레코드에 대한 DNS 쿼리에만 대답합니다.
* *재귀적* DNS 서버는 DNS 영역을 호스트하지 않습니다. 필요한 권한 있는 DNS 서버 toogather hello 데이터를 호출 하 여 모든 DNS 쿼리를 응답 합니다.

Azure DNS는 권한이 있는 DNS 서비스를 제공합니다.  재귀 DNS 서비스를 제공하지 않습니다. 클라우드 서비스 및 Azure에서 Vm에 자동으로 구성 된 toouse Azure의 인프라의 일부로 별도로 제공 되는 재귀 DNS 서비스는입니다. 이러한 DNS 설정을 확인 하는 toochange 방법에 대 한 내용은 [Azure에서 이름 확인](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)합니다.

Pc 또는 모바일 장치에서 DNS 클라이언트는 일반적으로 재귀 DNS 서버 tooperform hello 클라이언트 응용 프로그램에 필요한 모든 DNS 쿼리 호출 합니다.

예: 'www.contoso.com' DNS 레코드에 대 한 쿼리를 수신 하는 재귀 DNS 서버, hello '만든 contoso.com' 도메인에 대 한 먼저 toofind hello 이름 서버 호스팅 hello 영역이 필요 합니다. toofind hello 이름 서버 것 hello 루트 이름 서버에서 시작 찾은 여기에서 hello 'com' 영역을 호스팅하는 hello 이름 서버입니다. 그런 다음 hello 'com' 이름 서버 toofind hello 이름, 서버 hello '만든 contoso.com' 영역을 호스팅하는 쿼리 합니다.  마지막으로, 되었기 수 tooquery 이러한 이름 서버에 대 한 'www.contoso.com'.

이 절차는 hello DNS 이름 확인 이라고 합니다. 엄밀히 말해 다음 CNAMEs 등의 추가 단계를 포함 하는 DNS 확인 수 있지만 중요 한 toounderstanding DNS 위임 작동 방식입니다.

부모 영역 ' 지점을 방법 ' 자식 영역에 대 한 이름 서버 toohello? 이 작업을 위해 NS 레코드(NS는 '이름 서버'의 약자)라는 특수 형식의 DNS 레코드를 사용합니다. 예를 들어 hello 루트 영역 'com'에 대 한 NS 레코드를 포함 하 고 hello 'com' 영역에 대 한 이름 서버 hello를 보여 줍니다. 차례로 hello 'com' 영역 'contoso.com' hello 'contoso.com' 영역에 대 한 이름 서버 hello 표시에 대 한 NS 레코드를 포함 합니다. 부모 영역에는 자식 영역에 대 한 NS 레코드 hello 설정 위임 hello 도메인을 이라고 합니다.

다음 이미지는 hello 예제 DNS 쿼리를 보여 줍니다. hello contoso.net 및 partners.contoso.net Azure DNS 영역은입니다.

![Dns-nameserver](./media/dns-domain-delegation/image1.png)

1. 클라이언트 요청 hello `www.partners.contoso.net` 자신의 로컬 DNS 서버입니다.
1. hello 로컬 DNS 서버는 없으므로 hello 레코드 요청 tootheir 루트 이름 서버를 만듭니다.
1. hello 루트 이름 서버 hello 레코드는 없지만 hello의 hello 주소를 알고 `.net` toohello DNS 서버 주소 제공 이름 서버
1. hello DNS 보냅니다 hello 요청 toohello `.net` 이름 서버 없는 hello contoso.net 이름 서버 hello 주소 않도록 지정 되었으나 hello 레코드입니다. 이 예에서는 Azure DNS에 호스팅되는 DNS 영역입니다.
1. hello 영역 `contoso.net` hello 레코드는 없지만 hello 이름 서버에 대해 알고 `partners.contoso.net` 및 해당 이벤트에 응답 합니다. 이 예에서는 Azure DNS에 호스팅되는 DNS 영역입니다.
1. hello IP 주소를 요청 하는 DNS 서버 hello `partners.contoso.net` hello에서 `partners.contoso.net` 영역입니다. Hello A 레코드를 포함 하 고 hello IP 주소를 사용 하 여 응답 합니다.
1. hello DNS 서버 IP 주소 toohello 클라이언트 hello를 제공합니다.
1. toohello 웹 사이트를 연결 하는 클라이언트 hello `www.partners.contoso.net`합니다.

두 개 hello NS 레코드; 각 위임 toohello 자식 및 자체 hello 자식 영역에서 다른 가리키는 hello 부모 영역에 하나입니다. hello 'contoso.net' 영역 (더하기 toohello NS 레코드는 'net')에 'contoso.net'에 대 한 hello NS 레코드를 포함합니다. 이러한 레코드는 권한 있는 NS 레코드 라고 하 고 hello hello 자식 영역 루트에 도착 합니다.

## <a name="next-steps"></a>다음 단계

너무 방법에 대해 알아봅니다[사용자 도메인 tooAzure DNS 위임](dns-delegate-domain-azure-dns.md)

