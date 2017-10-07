---
title: "hello Azure 포털을 통해 Azure Cosmos DB 계정 aaaManage | Microsoft Docs"
description: "어떻게 toomanage Azure Cosmos DB는 hello Azure 포털을 통해을 계정에 대해 알아봅니다. Azure 포털 tooview hello, 복사, 삭제 및 액세스 계정 사용에 대 한 지침을 찾습니다."
keywords: "Azure 포털, Documentdb, Azure, Microsoft Azure"
services: cosmos-db
documentationcenter: 
author: kirillg
manager: jhubbard
editor: cgronlun
ms.assetid: 00fc172f-f86c-44ca-8336-11998dcab45c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kirillg
ms.openlocfilehash: 77ad953cf558a519674be08ad913a12202f69496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-an-azure-cosmos-db-account"></a>어떻게 toomanage Azure Cosmos DB 계정
자세한 내용은 tooset 전역 일관성을, 키를 사용 하 고 hello Azure 포털에서에서 Azure Cosmos DB 계정을 삭제 하는 방법입니다.

## <a id="consistency"></a>Azure Cosmos DB 일관성 설정 관리
Hello 오른쪽 일관성 수준을 선택 하는 응용 프로그램의 hello 의미 체계에 따라 달라 집니다. 잘 이해 해야 Azure Cosmos DB에 hello 사용할 수 있는 일관성 수준으로 읽어 [toomaximize 가용성 및 Azure Cosmos DB의 성능 수준 일관성을 사용 하 여][consistency]합니다. Azure Cosmos DB는 데이터베이스 계정에서 사용할 수 있는 모든 일관성 수준에서 일관성, 가용성 및 성능을 보증합니다. 강력한 일관성 수준이 데이터베이스 계정을 구성 하려면 데이터를 단일 Azure 지역 예외일된 tooa 및 전체적으로 사용할 수 없습니다. 반면 hello, bounded 부실, 세션 또는 최종 사용 상대적으로 느 일관성 수준-hello 있습니다 tooassociate 개수에 관계 없이 데이터베이스 계정 사용 하 여 Azure 지역입니다. 간단한 단계를 수행 하는 hello tooselect 기본 일관성 수준이 데이터베이스 계정에 대 한 hello 하는 방법을 보여 줍니다. 

### <a name="toospecify-hello-default-consistency-for-an-azure-cosmos-db-account"></a>Cosmos DB Azure 계정에 대 한 toospecify hello 기본 일관성
1. Hello에 [Azure 포털](https://portal.azure.com/), Azure Cosmos DB 계정에 액세스 합니다.
2. Hello 계정 블레이드에서 클릭 **일관성 기본**합니다.
3. Hello에 **기본 일관성** 블레이드, 새 일관성 수준 선택 hello 및 클릭 **저장**합니다.
    ![기본 일관성 세션][5]

## <a id="keys"></a>선택키 보기, 복사 및 다시 생성
Azure Cosmos DB 계정을 만들 때 hello 서비스는 hello Azure Cosmos DB 계정에 액세스할 때 인증에 사용할 수 있는 두 개의 마스터 액세스 키를 생성 합니다. 두 개의 액세스 키를 제공 함으로써 Azure Cosmos DB 하면 없는 중단 tooyour Azure Cosmos DB 계정 사용 하 여 tooregenerate hello 키. 

Hello에 [Azure 포털](https://portal.azure.com/), 액세스 hello **키** hello hello 메뉴 리소스에서에서 블레이드 **Azure Cosmos DB 계정** 블레이드 tooview / 복사 / 재생성 hello 액세스 키를 사용 되는 tooaccess Azure Cosmos DB 계정 됩니다.

![Azure 포털 스크린샷, 키 블레이드](./media/manage-account/keys.png)

> [!NOTE]
> hello **키** 블레이드도 포함 되어 기본 및 hello에서 계정을 사용 하는 tooconnect tooyour 일 수 있는 보조 연결 문자열 [데이터 마이그레이션 도구](import-data.md)합니다.
> 
> 

읽기 전용 키도 이 블레이드에서 사용할 수 있습니다. 읽기 및 쿼리는 읽기 전용 작업이며 만들기, 삭제 및 바꾸기는 읽기 전용 작업이 아닙니다.

### <a name="copy-an-access-key-in-hello-azure-portal"></a>Hello Azure 포털의에서 선택 키 복사
Hello에 **키** 블레이드에서 hello 클릭 **복사** toocopy 원하는 단추 toohello hello 키의 오른쪽입니다.

![표시 및 선택 키 hello 키 블레이드에서 Azure 포털에서 복사](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a>액세스 키 다시 생성
Hello 액세스 키 tooyour Azure Cosmos DB 계정을 변경 해야 주기적으로 toohelp 유지 되며 연결 더 안전 합니다. 두 개의 액세스 키 tooenable 할당 하면 toomaintain 연결 toohello 다시 생성 하는 동안에 한 선택 키를 사용 하 여 Azure Cosmos DB 계정을 hello 다른 선택 키입니다.

> [!WARNING]
> 액세스 키 다시 생성 하는 hello 현재 키에 의존 하는 모든 응용 프로그램을 영향을 줍니다. Hello 액세스 키 tooaccess hello Azure Cosmos DB 계정을 사용 하는 모든 클라이언트에 업데이트 된 toouse hello에 대 한 새 키 여야 합니다.
> 
> 

응용 프로그램 또는 Azure Cosmos DB 계정 hello를 사용 하 여 클라우드 서비스를 설정한 경우 손실 됩니다 hello 연결 키를 다시 생성 하는 경우 키 롤 하지 않는 한 합니다. hello 다음 단계에 간략하게 설명 키 롤링에 관련 된 hello 프로세스입니다.

1. 응용 프로그램 코드 tooreference hello 보조 액세스 키의 hello Azure Cosmos DB 계정에 대 한 hello 액세스 키를 업데이트 합니다.
2. Cosmos DB Azure 계정에 대 한 hello 기본 액세스 키 다시 생성 합니다. Hello에 [Azure 포털](https://portal.azure.com/), Azure Cosmos DB 계정에 액세스 합니다.
3. Hello에 **Azure Cosmos DB 계정** 블레이드에서 클릭 **키**합니다.
4. Hello에 **키** 블레이드에서 hello 다시 생성 단추를 클릭 한 다음 클릭 **확인** tooconfirm 원하는 toogenerate 새 키입니다.
    ![액세스 키 다시 생성](./media/manage-account/regenerate-keys.png)
5. 해당 hello 새 키를 사용 하기 위해 사용할 수를 확인 한 후 (약 5 분 후 다시 생성), 응용 프로그램 코드 tooreference hello 새 기본 액세스 키에 대 한 hello 액세스 키를 업데이트 합니다.
6. Hello 보조 액세스 키 다시 생성 합니다.
   
    ![액세스 키 다시 생성](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> Azure Cosmos DB 계정을 새로 생성 된 키를 사용 하는 tooaccess 수 전에 몇 분 정도 걸릴 수 있습니다.
> 
> 

## <a name="get-hello--connection-string"></a>Hello 구성 된 연결 문자열
tooretrieve 연결 문자열, 다음 hello지 않습니다. 

1. Hello에 [Azure 포털](https://portal.azure.com), Azure Cosmos DB 계정에 액세스 합니다.
2. Hello 리소스 메뉴에서 클릭 **키**합니다.
3. Hello 클릭 **복사** 단추 다음 toohello **기본 연결 문자열** 또는 **보조 연결 문자열** 상자입니다. 

Hello에서 연결 문자열 hello를 사용 하는 경우 [Azure Cosmos DB 데이터베이스 마이그레이션 도구](import-data.md), hello 데이터베이스 이름 toohello hello 연결 문자열의 끝에 추가 합니다. `AccountEndpoint=< >;AccountKey=< >;Database=< >`

## <a id="delete"></a> Azure Cosmos DB 계정 삭제
tooremove Azure Cosmos DB 계정에서 hello Azure 포털 더 이상 사용 하는 hello 계정 이름 마우스 오른쪽 단추로 클릭 하 고 클릭 **계정 삭제**합니다.

![에 Azure Cosmos DB toodelete 계정을 방법 hello Azure 포털](./media/manage-account/deleteaccount.png)

1. Hello에 [Azure 포털](https://portal.azure.com/), toodelete 원하는 hello Azure Cosmos DB 계정에 액세스 합니다.
2. Hello에 **Azure Cosmos DB 계정** 블레이드에서 hello 계정을 마우스 오른쪽 단추로 클릭 하 고 **계정 삭제**합니다. 
3. 결과 확인 블레이드에서 hello hello Azure Cosmos DB 계정 이름 tooconfirm toodelete hello 계정 한다는 것을 입력 합니다.
4. Hello 클릭 **삭제** 단추입니다.

![에 Azure Cosmos DB toodelete 계정을 방법 hello Azure 포털](./media/manage-account/delete-account-confirm.png)

## <a id="next"></a>다음 단계
너무 방법에 대해 알아봅니다[Azure Cosmos DB 계정 시작](http://go.microsoft.com/fwlink/p/?LinkId=402364)합니다.

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
