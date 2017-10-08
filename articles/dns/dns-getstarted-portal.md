---
title: "hello Azure 포털을 사용 하 여 Azure DNS aaaGet 시작 | Microsoft Docs"
description: "자세한 내용은 방법 toocreate DNS 영역 및 Azure DNS에 레코드입니다. 단계별 가이드 toocreate 이며 첫 번째 DNS 영역 및 hello Azure 포털을 사용 하 여 레코드를 관리 합니다."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 5cea01d840d794001cccac64defed8b329d948db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-hello-azure-portal"></a>Azure DNS hello Azure 포털을 사용 하 여 시작

> [!div class="op_single_selector"]
> * [Azure 포털](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [Azure CLI 1.0](dns-getstarted-cli-nodejs.md)
> * [Azure CLI 2.0](dns-getstarted-cli.md)

이 문서 안내 hello 단계 toocreate 첫 번째 DNS 영역과 hello Azure 포털을 사용 하 여 레코드. Azure PowerShell을 사용 하 여 이러한 단계를 수행 하거나 플랫폼 간 Azure CLI hello 수도 있습니다.

DNS 영역에는 특정 도메인에 대 한 사용 되는 toohost hello DNS 레코드입니다. Azure DNS에서 도메인 호스팅 toostart toocreate DNS 영역 해당 도메인 이름을 사용 해야 합니다. 그러면 이 DNS 영역 안에 도메인의 각 DNS 레코드가 생성됩니다. 마지막으로, toopublish DNS 영역 toohello 인터넷 tooconfigure hello 이름 서버 hello 도메인에 대 한 필요 합니다. 이러한 각 단계는 단계를 수행 하는 hello에 설명 되어 있습니다.

## <a name="create-a-dns-zone"></a>DNS 영역 만들기

1. Azure 포털 toohello에 로그인
2. Hello 허브 메뉴에서를 클릭 하 고 클릭 **새로 만들기 > 네트워킹 >** 클릭 하 고 **DNS 영역** tooopen hello 만들 DNS 영역 블레이드입니다.

    ![DNS 영역](./media/dns-getstarted-portal/openzone650.png)

4. Hello에 **만들 DNS 영역** 블레이드 hello 다음 값을 입력 한 다음 클릭 **만들기**:


   | **설정** | **값** | **세부 정보** |
   |---|---|---|
   |**Name**|contoso.com|hello hello DNS 영역 이름|
   |**구독**|[구독 이름]|구독 toocreate hello DNS 영역을 선택 합니다.|
   |**리소스 그룹**|**새로 만들기:** contosoDNSRG|리소스 그룹을 만듭니다. hello 리소스 그룹 이름은 선택한 hello 구독 내에서 고유 해야 합니다. 리소스 그룹을 읽기 hello에 대 한 자세한 toolearn [리소스 관리자](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) 개요 문서.|
   |**위치**:|미국 서부||

> [!NOTE]
> hello 리소스 그룹 hello 리소스 그룹의 toohello 위치 참조 되었으며 hello DNS 영역에 영향을 주지 않습니다. hello DNS 영역의 위치는 항상 "전역" 하 고 표시 되지 않습니다.

## <a name="create-a-dns-record"></a>DNS 레코드 만들기

hello 다음 예에서는 과정을 보여 줍니다 hello 새 'A' 레코드를 만드는 중입니다. 다른 레코드 종류 및 toomodify 기존 레코드에 대 한 참조 [관리 DNS 레코드 및 레코드 집합 사용 하 여 Azure 포털 hello](dns-operations-recordsets-portal.md)합니다. 

1. Hello로 DNS 영역에서에서 만든 hello Azure 포털 **즐겨찾기** 창에서 클릭 **모든 리소스**합니다. Hello 클릭 **contoso.com** 모든 리소스 블레이드 hello에 DNS 영역입니다. 이미 선택한 hello 구독에 여러 자원이 인 경우 입력 하면 **contoso.com** hello에 **이름별으로 필터링...** 상자 tooeasily hello DNS 영역에 액세스 합니다.

1. Hello의 hello 위쪽 **DNS 영역** 블레이드를 **집합을 기록해 +** tooopen hello **레코드 집합을 추가** 블레이드입니다.

1. Hello에 **레코드 집합을 추가** 블레이드에서 hello 다음 값을 입력 하 고 클릭 **확인**합니다. 이 예에서는 A 레코드를 만들 것입니다.

   |**설정** | **값** | **세부 정보** |
   |---|---|---|
   |**Name**|www|Hello 레코드의 이름|
   |**형식**|A| 유형 DNS 레코드 toocreate의 허용 되는 값은 A, AAAA, CNAME, MX, NS, SRV, TXT, 및 PTR입니다.  레코드 유형에 대한 자세한 내용은 [DNS 영역 및 레코드 개요](dns-zones-records.md)를 참조하세요.|
   |**TTL**|1|-Time-to-live hello DNS 요청 합니다.|
   |**TTL 단위**|시간|TTL 값에 대한 시간 측정입니다.|
   |**IP 주소**|ipAddressValue| 이 값은 hello DNS 레코드를 해결 하는 hello IP 주소.|

## <a name="view-records"></a>레코드 보기

Hello hello DNS 영역 블레이드의 아래 부분을 hello DNS 영역에 대 한 hello 레코드를 볼 수 있습니다. Hello 기본 DNS 및 SOA 레코드를 모든 영역에 만들어지는 플러스 만든 새 레코드를 볼 수 있습니다.

![영역](./media/dns-getstarted-portal/viewzone500.png)


## <a name="update-name-servers"></a>이름 서버 업데이트

일단 시작 되 면 DNS 영역과 레코드는 올바르게 설정 되었는지, tooconfigure 필요한 충족 도메인 이름 toouse hello Azure DNS 이름 서버입니다. 이렇게 하면 다른 사용자 hello 인터넷 toofind에 DNS 레코드입니다.

영역에 대 한 이름 서버 hello hello Azure 포털에서에서 제공 됩니다.

![영역](./media/dns-getstarted-portal/viewzonens500.png)

이러한 이름 서버 hello 도메인 이름 등록 기관 (여기서 구입한 hello 도메인 이름)으로 구성 해야 합니다. 등록 자가 hello 옵션 tooset hello 도메인에 대 한 hello 이름 서버를 제공합니다. 자세한 내용은 참조 [사용자 도메인 tooAzure DNS 위임](dns-domain-delegation.md)합니다.

## <a name="delete-all-resources"></a>모든 리소스 삭제

이 문서에서는 다음 단계 완료 hello에서에서 만든 모든 리소스를 toodelete:

1. Hello Azure 포털에서에서 **즐겨찾기** 창에서 클릭 **모든 리소스**합니다. Hello 클릭 **MyResourceGroup** 리소스 그룹 hello에서 모든 리소스 블레이드입니다. 이미 선택한 hello 구독에 여러 자원이 인 경우 입력 하면 **MyResourceGroup** hello에 **이름별으로 필터링...** 상자 tooeasily 액세스 hello 리소스 그룹입니다.
1. Hello에 **MyResourceGroup** 블레이드에서 hello 클릭 **삭제** 단추입니다.
1. hello 포털 해야 tootype hello 이름의 hello 리소스 그룹 tooconfirm toodelete 원하는 것입니다. 클릭 **삭제**, 형식 *MyResourceGroup* hello 리소스 그룹 이름에 대 한 클릭 **삭제**합니다. 리소스 그룹을 삭제 hello 리소스 그룹 내에서 모든 리소스에 있으므로 항상 있는지 tooconfirm 리소스 그룹의 hello 내용을 삭제 하기 전에 합니다. hello 포털 hello 리소스 그룹 내에 포함 된 모든 리소스를 삭제 한 다음 자체 hello 리소스 그룹을 삭제 합니다. 이 프로세스는 몇 분 정도 걸립니다.


## <a name="next-steps"></a>다음 단계

Azure DNS에 대해 자세히 toolearn 참조 [Azure DNS 개요](dns-overview.md)합니다.

Azure DNS에 DNS 레코드를 관리에 대해 자세히 toolearn 참조 [관리 DNS 레코드 및 레코드 집합 사용 하 여 Azure 포털 hello](dns-operations-recordsets-portal.md)합니다.

