---
title: "가져오기 작업에 대 한 Azure 가져오기/내보내기 aaaCreate | Microsoft Docs"
description: "자세한 내용은 방법 toocreate hello Microsoft Azure 가져오기/내보내기 서비스에 대 한 가져오기."
author: muralikk
manager: syadav
editor: syadav
services: storage
documentationcenter: 
ms.assetid: 8b886e83-6148-4149-9d0f-5d48ec822475
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: da974c33a3688bb5e2412c8bfcbeca704096c2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-import-job-for-hello-azure-importexport-service"></a>Hello Azure 가져오기/내보내기 서비스에 대 한 가져오기 작업 만들기

Hello REST API를 사용 하 여 hello Microsoft Azure 가져오기/내보내기 서비스에 대 한 가져오기 작업 만들기 단계를 수행 하는 hello 포함 됩니다.

-   Azure 가져오기/내보내기 도구 hello로 드라이브를 준비 합니다.

-   Hello 위치 toowhich tooship hello 드라이브를 가져오세요.

-   Hello 가져오기 작업 만들기

-   지원 되는 운송 업체 서비스를 통해 tooMicrosoft 드라이브 hello를 전달 합니다.

-   세부 정보를 전달 하는 hello로 hello 가져오기 작업을 업데이트 합니다.

 참조 [hello Microsoft Azure 가져오기/내보내기 서비스 tooTransfer 데이터 tooBlob 저장소를 사용 하 여](storage-import-export-service.md) hello 가져오기/내보내기 서비스 및 설명 하는 자습서에 대 한 개요 방법을 toouse hello [Azure 포털](https://portal.azure.com/) toocreate 가져오기 및 내보내기 작업 합니다.

## <a name="preparing-drives-with-hello-azure-importexport-tool"></a>Azure 가져오기/내보내기 도구 hello가 있는 드라이브 준비

가져오기 작업에 대 한 hello 단계 tooprepare 드라이브는 동일한 jobvia hello 포털 hello 또는 hello REST API를 통해 만드는 지 hello 됩니다.

다음은 드라이브 준비에 대한 간단한 설명입니다. Toohello 참조 [Azure 가져오기 ExportTool 참조](storage-import-export-tool-how-to-v1.md) 자세한 지침은 합니다. Hello Azure 가져오기/내보내기 도구를 다운로드할 수 있습니다 [여기](http://go.microsoft.com/fwlink/?LinkID=301900)합니다.

드라이브를 준비하는 과정은 다음과 같습니다.

-   가져온 hello 데이터 toobe를 식별 합니다.

-   Windows Azure 저장소에 hello 대상 blob을 식별 합니다.

-   Azure 가져오기/내보내기 도구 toocopy hello를 사용 하 여 데이터 tooone 또는 더 많은 하드 드라이브입니다.

 준비가 된 것 처럼 각 hello 드라이브 hello Azure 가져오기/내보내기 도구를 사용 하면 매니페스트 파일 또한 생성 합니다. 매니페스트 파일에는 다음이 포함됩니다.

-   모든 hello 파일 업로드 및 이러한 파일 tooblobs hello 매핑을 위한의 열거형입니다.

-   각 파일의 hello 세그먼트의 체크섬입니다.

-   각 blob과 함께 메타 데이터 및 속성 tooassociate hello에 대 한 정보입니다.

-   Hello 컨테이너에 있는 기존 blob 이름을 업로드 될 blob hello에는 목록 hello 동작 tootake 동일 합니다. 가능한 옵션은: a) hello blob 버전으로 덮어쓰기 hello 파일, b) hello 기존 blob 및 hello 파일 업로드 건너뛰기 유지, c) 다른 파일과 충돌 하지 않는 접미사 toohello 이름을 추가 합니다.

## <a name="obtaining-your-shipping-location"></a>배송 위치 가져오기

가져오기 작업을 만들기 전에 tooobtain 배송 위치 이름 및 주소에서 필요한 호출 hello [위치 나열](/rest/api/storageimportexport/listlocations) 작업 합니다. `List Locations`는 위치 목록과 해당 우편 발송 주소 목록을 반환합니다. Hello 반환 된 목록에서에서 위치를 선택 하 고 인 하드 드라이브 toothat 주소 수 있습니다. Hello를 사용할 수도 있습니다 `Get Location` 작업 tooobtain hello 특정 위치에 대 한 주소를 직접 전달 합니다.

 Tooobtain hello 배송 위치 아래에 있는 hello 단계를 수행 합니다.

-   저장소 계정의 hello 위치의 hello 이름을 식별 합니다. Hello이이 값을 확인할 수 있습니다 **위치** 필드 hello 저장소 계정에 **대시보드** hello Azure 포털 또는 hello 서비스 관리 API 작업을 사용 하 여 쿼리할에 [저장소 가져오기 계정 속성](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties)합니다.

-   Hello를 호출 하 여 hello 위치를 사용할 수 있는 tooprocess이 저장소 계정을 검색 `Get Location` 작업 합니다.

-   경우 hello `AlternateLocations` 자체 hello 위치를 포함 하는 hello 위치의 속성을 덮어쓰려면 toouse이이 위치입니다. 그렇지 않으면 hello 호출 `Get Location` hello 대체 위치 중 하나를 사용 하 여 다시 작업 합니다. 유지 관리에 대 한 hello 원래 위치를 일시적으로 닫혔을 수 있습니다.

## <a name="creating-hello-import-job"></a>Hello 가져오기 작업 만들기
toocreate hello 가져오기 작업을 호출 hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) 작업 합니다. 다음 정보는 tooprovide hello이 필요 합니다.

-   Hello 작업에 대 한 이름입니다.

-   hello 저장소 계정 이름입니다.

-   배송 위치 이름, hello 이전 단계에서 가져온 번호입니다.

-   작업 유형(가져오기)입니다.

-   hello 반송 주소는 hello 가져오기 작업이 완료 된 후 hello 드라이브를 전송 해야 합니다.

-   hello hello 작업의 드라이브 목록입니다. 각 드라이브에 대 한 hello 다음 hello 드라이브 준비 단계에서 가져온 정보를 포함 해야 합니다.

    -   hello 드라이브 Id

    -   hello BitLocker 키

    -   hello hello 하드 드라이브에 매니페스트 파일 상대 경로

    -   hello Base16 인코딩된 매니페스트 파일 MD5 해시

## <a name="shipping-your-drives"></a>드라이브 배송
Hello 이전 단계에서 가져온 사용자 드라이브 toohello 주소를 배송 해야 하 고 hello 패키지 수를 추적 하는 hello로 hello 가져오기/내보내기 서비스를 제공 해야 합니다.

> [!NOTE]
>  패키지의 추적 번호를 제공하는 지원 운송업체 서비스를 통해 드라이브를 배송해야 합니다.

## <a name="updating-hello-import-job-with-your-shipping-information"></a>배송 정보 사용 hello 가져오기 작업 업데이트
추적 번호를 사용 하는 다음 호출 hello [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) 작업 tooupdate hello 통신 회사 이름, hello 작업에 대 한 추적 번호 hello 및 반환 전달용 hello 운송 업체 계정 번호를 전달 합니다. 필요에 따라 hello 드라이브 수 및 배송 날짜도 hello를 지정할 수 있습니다.

## <a name="next-steps"></a>다음 단계

* [Hello 가져오기/내보내기 서비스 REST API를 사용 하 여](storage-import-export-using-the-rest-api.md)
