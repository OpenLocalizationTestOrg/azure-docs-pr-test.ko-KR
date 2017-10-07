---
title: "DNS aaaManage 집합 및 Azure dns 레코드를 기록 합니다. | Microsoft Docs"
description: "Azure DNS 설정 하 고 도메인을 호스팅할 때 기록 하는 hello 기능 toomanage DNS 레코드를 제공 합니다."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ed44a1-7bfe-454f-964e-922ad978264a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 2e62d017341589eaf8d1f8df2fe5db4b973381d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-record-sets-by-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 DNS 레코드 및 레코드 집합 관리

> [!div class="op_single_selector"]
> * [Azure 포털](dns-operations-recordsets-portal.md)
> * [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

이 문서 toomanage 레코드 집합 및 레코드를 사용 하 여 DNS 영역이 hello Azure 포털에 방법을 보여 줍니다.

DNS 레코드 집합 및 개별 DNS 레코드 간의 중요 한 toounderstand hello 차이 레코드 집합은 hello 동일한 이름을 지정 하 고 동일한 hello는 입력이 있는 영역에 있는 레코드의 컬렉션입니다. 자세한 내용은 참조 [만드는 DNS 레코드 집합 및 레코드를 사용 하 여 Azure 포털 hello](dns-getstarted-create-recordset-portal.md)합니다.

## <a name="create-a-new-record-set-and-record"></a>새 레코드 집합 및 레코드 만들기

toocreate hello Azure 포털에서에서 설정 하는 레코드 참조 [만드는 DNS 레코드를 사용 하 여 Azure 포털 hello](dns-getstarted-create-recordset-portal.md)합니다.

## <a name="view-a-record-set"></a>레코드 집합 보기

1. Hello Azure 포털에서에서 toohello 이동 **DNS 영역** 블레이드입니다.
2. 레코드 집합 hello 찾아 선택 합니다. 이 hello 레코드 집합 속성을 엽니다.

    ![레코드 집합 검색](./media/dns-operations-recordsets-portal/searchset500.png)

## <a name="add-a-new-record-tooa-record-set"></a>새 레코드 tooa 레코드 집합 추가

Too20 레코드 tooany 레코드 집합을 추가할 수 있습니다. 레코드 집합에는 두 개의 동일한 레코드가 포함될 수 없습니다. (0 개 레코드)와 빈 레코드 집합을 만들 수 있지만 hello Azure DNS 이름 서버에 표시 되지 않습니다. CNAME 형식의 레코드 집합은 최대 하나의 레코드를 포함할 수 있습니다.

1. Hello에 **속성을 설정 하는 레코드** hello 레코드를 클릭 하는 DNS 영역이 블레이드 되도록 tooadd 레코드를 설정 합니다.

    ![레코드 집합 선택](./media/dns-operations-recordsets-portal/selectset500.png)

2. Hello 필드에 입력 하 여 속성을 설정 하는 hello 레코드를 지정 합니다.

    ![레코드 추가](./media/dns-operations-recordsets-portal/addrecord500.png)

3. 클릭 **저장** 에 hello hello 블레이드 toosave 맨 설정 합니다. 그런 다음 hello 블레이드를 닫습니다.
4. Hello 구석에 hello 레코드가 저장 하는지 표시 됩니다.

    ![레코드 집합 저장](./media/dns-operations-recordsets-portal/saving150.png)

Hello 레코드를 저장 한 후 hello hello에 대 한 값 **DNS 영역** 블레이드 hello 새 레코드에 반영 됩니다.

## <a name="update-a-record"></a>레코드 업데이트

기존 레코드 집합의 레코드를 업데이트할 때 hello 필드를 업데이트할 수 있습니다 작업 하는 레코드의 hello 형식에 따라 달라 집니다.

1. Hello에 **속성을 설정 하는 레코드** 블레이드 레코드 세트 hello 레코드에 대 한 검색 합니다.
2. Hello 레코드를 수정 합니다. 레코드를 수정 하는 경우 hello hello 레코드에 대 한 사용 가능한 설정을 변경할 수 있습니다. 다음 예제는 hello에서 hello **IP 주소** 필드를 선택 하 고 수정 하 고 hello 프로세스의 hello IP 주소는 합니다.

    ![레코드 수정](./media/dns-operations-recordsets-portal/modifyrecord500.png)

3. 클릭 **저장** 에 hello hello 블레이드 toosave 맨 설정 합니다. Hello 오른쪽 상단에 저장 된 hello 레코드 hello 알림이 표시 됩니다.

    ![저장된 레코드 집합](./media/dns-operations-recordsets-portal/saved150.png)

Hello 레코드에 대 한 hello 값 hello에 설정 hello 레코드를 저장 한 후 **DNS 영역** 블레이드 업데이트 hello 레코드에 반영 됩니다.

## <a name="remove-a-record-from-a-record-set"></a>레코드 집합에서 레코드 제거

레코드 집합에서 hello Azure 포털 tooremove 레코드를 사용할 수 있습니다. Note hello 마지막 레코드를 레코드 집합에서 제거 hello 레코드 집합을 삭제 되지 않습니다.

1. Hello에 **속성을 설정 하는 레코드** 블레이드 레코드 세트 hello 레코드에 대 한 검색 합니다.
2. Tooremove hello 레코드를 클릭 합니다. 그런 후 **제거**를 선택합니다.

    ![레코드 제거](./media/dns-operations-recordsets-portal/removerecord500.png)

3. 클릭 **저장** 에 hello hello 블레이드 toosave 맨 설정 합니다.
4. Hello 레코드를 제거한 후 hello hello 레코드 hello에 대 한 값 **DNS 영역** 블레이드 hello 제거 반영 됩니다.

## <a name="delete"></a>레코드 집합 삭제

1. Hello에 **속성을 설정 하는 레코드** 클릭 하 여 레코드 집합에 대 한 블레이드 **삭제**합니다.

    ![레코드 집합 삭제](./media/dns-operations-recordsets-portal/deleterecordset500.png)

2. Toodelete hello 레코드 집합을 원하는 묻는 메시지가 나타납니다.
3. 설정 되어 있는지 확인 hello 이름 일치 hello 레코드 toodelete를 원하고 클릭 **예**합니다.
4. Hello에 **DNS 영역** 블레이드에서 hello 레코드 집합은 더 이상 볼 수 있는지 확인 합니다.

## <a name="work-with-ns-and-soa-records"></a>NS 및 SOA 레코드 작업

자동으로 생성되는 NS 및 SOA 레코드는 다른 레코드 유형과 다르게 관리됩니다.

### <a name="modify-soa-records"></a>SOA 레코드 수정

추가 하거나 자동으로 설정 hello 영역 루트에 SOA 레코드를 생성 하는 hello에서 레코드를 제거할 수 없습니다 (이름 = "@"). 그러나 hello "호스트") (제외 SOA 레코드 내에 hello 매개 변수 중 하나를 수정 하 고 TTL을 설정 하는 hello 레코드.

### <a name="modify-ns-records-at-hello-zone-apex"></a>Hello 영역 루트에 있는 NS 레코드를 수정 합니다.

hello 영역 루트에서 설정 하는 hello NS 레코드는 각 DNS 영역과 자동으로 만들어집니다. Hello Azure DNS 이름 서버 할당된 toohello 영역의 hello 이름이 포함 되어 있습니다.

추가 이름 서버 toothis NS 레코드 집합을 공동 도메인 DNS 공급자를 둘 이상의 호스팅 toosupport를 추가할 수 있습니다. 또한 TTL hello 및이 레코드 집합에 대 한 메타 데이터를 수정할 수 있습니다. 그러나 제거 하거나 hello 미리 채워진된 Azure DNS 이름 서버를 수정할 수 없습니다.

Note이 적용 hello 영역 루트에서 레코드 집합 toohello NS만 됩니다. 제약 조건 없이 (사용 되는 toodelegate 하위 영역)으로 시간대에서 다른 NS 레코드 집합을 수정할 수 있습니다.

### <a name="delete-soa-or-ns-record-sets"></a>SOA 또는 NS 레코드 집합 삭제

Hello NS 및 SOA 레코드 집합 hello 영역 루트에서 삭제할 수 없습니다 (이름 = "@") hello 영역을 만들 때 자동으로 생성 됩니다입니다. Hello 영역을 삭제 하면 자동으로 삭제 됩니다.

## <a name="next-steps"></a>다음 단계

* Azure DNS에 대 한 자세한 내용은 참조 hello [Azure DNS 개요](dns-overview.md)합니다.
* DNS를 자동화 하는 방법에 대 한 자세한 내용은 참조 [만들 DNS 영역 및 레코드 집합을 사용 하 여 hello.NET SDK](dns-sdk.md)합니다.
* 역방향 DNS 레코드에 대한 자세한 내용은 [Azure의 역방향 DNS 및 지원 개요](dns-reverse-dns-overview.md)를 참조하세요.
