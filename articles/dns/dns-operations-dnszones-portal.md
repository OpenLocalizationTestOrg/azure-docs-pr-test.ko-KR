---
title: "Azure DNS-Azure 포털에서에서 aaaManage DNS 영역 | Microsoft Docs"
description: "Hello Azure 포털을 사용 하 여 DNS 영역을 관리할 수 있습니다. 이 문서에서는 tooupdate, 삭제 하 고 dns를 Azure DNS 영역을 만드는 방법을 설명합니다"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/18/2017
ms.author: gwallace
ms.openlocfilehash: 0d8ce302bb7126dfe8077a6f3e33418e16fcea64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-hello-azure-portal"></a>Toomanage DNS 영역에 Azure 포털을 hello 하는 방법

> [!div class="op_single_selector"]
> * [포털](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-dnszones-cli.md)

이 문서에서는 어떻게 toomanage DNS 영역을 hello Azure 포털을 사용 하 여 보여 줍니다. 플랫폼 간 hello를 사용 하 여 DNS 영역을 관리할 수 있습니다 [Azure CLI](dns-operations-dnszones-cli.md) Azure hello 또는 [PowerShell](dns-operations-dnszones.md)합니다.

## <a name="create-a-dns-zone"></a>DNS 영역 만들기

1. Azure 포털 toohello에 로그인
2. Hello 허브 메뉴에서를 클릭 하 고 클릭 **새로 만들기 > 네트워킹 >** 클릭 하 고 **DNS 영역** tooopen hello 만들 DNS 영역 블레이드입니다.

    ![DNS 영역](./media/dns-operations-dnszones-portal/openzone650.png)

4. Hello에 **만들 DNS 영역** 블레이드 hello 다음 값을 입력 한 다음 클릭 **만들기**:


   | **설정** | **값** | **세부 정보** |
   |---|---|---|
   |**Name**|contoso.com|hello hello DNS 영역 이름|
   |**구독**|[구독 이름]|구독 toocreate hello DNS 영역을 선택 합니다.|
   |**리소스 그룹**|**새로 만들기:** contosoDNSRG|리소스 그룹을 만듭니다. hello 리소스 그룹 이름은 선택한 hello 구독 내에서 고유 해야 합니다. 리소스 그룹을 읽기 hello에 대 한 자세한 toolearn [리소스 관리자](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) 개요 문서.|
   |**위치**:|미국 서부||

> [!NOTE]
> hello 리소스 그룹 hello 리소스 그룹의 toohello 위치 참조 되었으며 hello DNS 영역에 영향을 주지 않습니다. hello DNS 영역의 위치는 항상 "전역" 하 고 표시 되지 않습니다.

## <a name="list-dns-zones"></a>DNS 영역 나열

Hello Azure 포털에서 탐색 너무**더 많은 서비스** > **네트워킹** > **DNS 영역**합니다. 각 DNS 영역은 자체 리소스이며, 레코드 집합의 수 및 이름 서버와 같은 정보를 이 보기에서 볼 수 있습니다. hello 열 **이름 서버** tooadd hello 기본 뷰에서 해당 클릭 되지 않습니다 **열**선택, **이름 서버** 클릭 **수행**합니다.

![DNS 영역 나열](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a>DNS 영역 삭제

Hello 포털에서 tooa DNS 영역을 이동 합니다. Hello에 **DNS 영역** 블레이드에서 클릭 **영역 삭제**합니다. 입력 정보 요청된 tooconfirm toodelete hello DNS 영역 부호 됩니다. DNS 영역을 삭제 하면 hello 영역에 포함 된 모든 hello 레코드 삭제 합니다.

## <a name="next-steps"></a>다음 단계

자세한 방법을 프로그램 DNS 영역 및 레코드를 방문 하 여 toowork [hello Azure 포털을 사용 하 여 Azure DNS 시작](dns-getstarted-portal.md)합니다.
