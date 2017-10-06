---
title: "내보내기 작업에 대 한 Azure 가져오기/내보내기 aaaCreate | Microsoft Docs"
description: "내보내기 toocreate hello Microsoft Azure 가져오기/내보내기 서비스에 대 한 작업 하는 방법에 대해 알아봅니다."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 613d480b-a8ef-4b28-8f54-54174d59b3f4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 4a10b42cc86dbf3bcea3a515bc065e2259228ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-export-job-for-hello-azure-importexport-service"></a>Hello Azure 가져오기/내보내기 서비스에 대 한 내보내기 작업 만들기
Hello REST API를 사용 하 여 hello Microsoft Azure 가져오기/내보내기 서비스에 대 한 내보내기 작업 만들기 단계를 수행 하는 hello 포함 됩니다.

-   Tooexport를 blob hello를 선택 합니다.

-   배송 위치 가져오기

-   Hello 내보내기 작업 만들기

-   지원 되는 운송 업체 서비스를 통해에 빈 드라이브 tooMicrosoft으로 배송 됩니다.

-   Hello 패키지 정보로 hello 내보내기 작업을 업데이트합니다.

-   Microsoft에서 다시 수신 hello 드라이브입니다.

 참조 [hello Windows Azure 가져오기/내보내기 서비스 tooTransfer 데이터 tooBlob 저장소를 사용 하 여](storage-import-export-service.md) hello 가져오기/내보내기 서비스 및 설명 하는 자습서에 대 한 개요 방법을 toouse hello [Azure 포털](https://portal.azure.com/) toocreate 가져오기 및 내보내기 작업 합니다.

## <a name="selecting-blobs-tooexport"></a>Blob tooexport 선택
 내보내기 작업 toocreate tooprovide blob 저장소 계정에서 tooexport 되도록 목록이 필요 합니다. 몇 가지 tooselect toobe 내보낼 blob:

-   상대 blob 경로 tooselect 단일 blob 및 해당 스냅숏을 모두 사용할 수 있습니다.

-   상대 blob 경로 tooselect 해당 스냅숏을 제외한 단일 blob를 사용할 수 있습니다.

-   상대 blob 경로 스냅숏 시간 tooselect 단일 스냅숏 사용할 수 있습니다.

-   접두사를 지정 하는 hello로 blob 접두사 tooselect 모든 blob 및 스냅숏을 사용할 수 있습니다.

-   모든 blob 및 스냅숏을 hello 저장소 계정에서 내보낼 수 있습니다.

 지정 하는 방법에 대 한 자세한 내용은 tooexport blob에 대 한 참조 hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) 작업 합니다.

## <a name="obtaining-your-shipping-location"></a>배송 위치 가져오기
내보내기 작업을 만들기 전에 tooobtain 배송 위치 이름 및 주소에서 필요한 호출 hello [가져오기 위치](https://portal.azure.com) 또는 [위치 나열](/rest/api/storageimportexport/listlocations) 작업 합니다. `List Locations`는 위치 목록과 해당 우편 발송 주소 목록을 반환합니다. Hello 반환 된 목록에서에서 위치를 선택 하 고 인 하드 드라이브 toothat 주소 수 있습니다. Hello를 사용할 수도 있습니다 `Get Location` 작업 tooobtain hello 특정 위치에 대 한 주소를 직접 전달 합니다.

Tooobtain hello 배송 위치 아래에 있는 hello 단계를 수행 합니다.

-   저장소 계정의 hello 위치의 hello 이름을 식별 합니다. Hello이이 값을 확인할 수 있습니다 **위치** 필드 hello 저장소 계정에 **대시보드** hello 기본 포털 이나 hello 서비스 관리 API 작업을 사용 하 여에 대 한 쿼리 [가져오기 저장소 계정 속성](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties)합니다.

-   Hello를 호출 하 여이 저장소 계정을 사용할 수 있는 tooprocess 있는 hello 위치를 검색할 `Get Location` 작업 합니다.

-   경우 hello `AlternateLocations` 자체 hello 위치를 포함 하는 hello 위치의 속성을 덮어쓰려면 toouse이이 위치입니다. 그렇지 않으면 hello 호출 `Get Location` hello 대체 위치 중 하나를 사용 하 여 다시 작업 합니다. 유지 관리에 대 한 hello 원래 위치를 일시적으로 닫혔을 수 있습니다.

## <a name="creating-hello-export-job"></a>Hello 내보내기 작업 만들기
 toocreate hello 내보내기 작업을 호출 hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) 작업 합니다. 다음 정보는 tooprovide hello이 필요 합니다.

-   Hello 작업에 대 한 이름입니다.

-   hello 저장소 계정 이름입니다.

-   hello hello 이전 단계에서 얻은 위치 이름을 전달 합니다.

-   작업 유형(내보내기)입니다.

-   hello 반송 주소는 hello 내보내기 작업이 완료 된 후 hello 드라이브를 전송 해야 합니다.

-   hello는 blob (또는 blob 접두사) 목록을 toobe가 내보냅니다.

## <a name="shipping-your-drives"></a>드라이브 배송
 다음으로, 내보낸 toobe 선택한 hello blob 기반 toosend 필요한 드라이브 hello Azure 가져오기/내보내기 도구 toodetermine hello 번호를 사용 하 고 hello 드라이브 크기입니다. Hello 참조 [Azure 가져오기/내보내기 도구 참조](storage-import-export-tool-how-to-v1.md) 대 한 자세한 내용은 합니다.

 단일에서 패키지 hello 드라이브 패키지 및 toohello 보내줄 hello에서 가져온 주소로 앞 단계입니다. Note hello hello 다음 단계에 대 한 패키지 수를 추적 합니다.

> [!NOTE]
>  패키지의 추적 번호를 제공하는 지원 운송업체 서비스를 통해 드라이브를 배송해야 합니다.

## <a name="updating-hello-export-job-with-your-package-information"></a>패키지 정보를 사용 hello 내보내기 작업 업데이트
 추적 번호를 사용 하는 다음 호출 hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) 작업 tooupdated hello 배송 업체 이름과 추적 번호 hello 작업입니다. Hello 드라이브 수, hello 반환 주소 및 hello 배송 날짜도 선택적으로 지정할 수 있습니다.

## <a name="receiving-hello-package"></a>Hello 패키지 받기
 내보내기 작업을 처리 한 후 암호화 된 데이터와 함께 tooyou 드라이브가 반환 됩니다. 각 호출 hello로 hello 드라이브에 대 한 hello BitLocker 키를 검색할 수 있습니다 [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) 작업 합니다. Hello 키를 사용 하 여 hello 드라이브 잠금을 해제할 수 있습니다. 각 드라이브에 hello 드라이브 매니페스트 파일에는 각 파일에 대 한 원래 blob 주소도 hello: hello 드라이브에 파일의 hello 목록을 포함합니다.

## <a name="next-steps"></a>다음 단계

* [Hello 가져오기/내보내기 서비스 REST API를 사용 하 여](storage-import-export-using-the-rest-api.md)
