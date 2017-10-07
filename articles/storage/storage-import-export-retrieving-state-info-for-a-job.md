---
title: "Azure 가져오기/내보내기 작업에 대 한 상태 정보 aaaRetrieving | Microsoft Docs"
description: "Tooobtain Microsoft Azure 가져오기/내보내기 서비스 작업에 대 한 정보를 명시 하는 방법에 대해 알아봅니다."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 22d7e5f0-94da-49b4-a1ac-dd4c14a423c2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: muralikk
ms.openlocfilehash: cbc35660519573d92f641924ac0025c9e577d69b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="retrieving-state-information-for-an-importexport-job"></a>Import/Export 작업에 대한 상태 정보 검색
Hello를 호출할 수 있습니다 [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) 작업 tooretrieve 정보 둘 다에 대 한 가져오기 및 내보내기 작업 합니다. 반환 된 hello 정보에는 다음이 포함 됩니다.

-   hello hello 작업의 현재 상태입니다.

-   각 작업이 완료 된 hello 대략적인 백분율.

-   hello 각 드라이브의 현재 상태입니다.

-   오류 로그 및 자세한 로깅 정보를 포함한 Blob에 대한 URI(사용 가능한 경우)

hello 다음 섹션에 설명 hello에서 반환 하는 hello 정보 `Get Job` 작업 합니다.

## <a name="job-states"></a>작업 상태
hello 테이블과 hello 상태 다이어그램 아래 수명 주기 작업을 전환 하는 hello 상태를 설명 합니다. 호출 hello 여 hello hello 작업의 현재 상태를 확인할 수 있습니다 `Get Job` 작업 합니다.

![작업 상태](./media/storage-import-export-retrieving-state-info-for-a-job/JobStates.png "작업 상태")

hello 다음 표에서 작업이 통과할 수 있는 각 상태.

|작업 상태|설명|
|---------------|-----------------|
|`Creating`|Hello Put Job 작업을 호출 하 고 ְ  해당 상태는 너무 설정 후`Creating`합니다. Hello 작업 hello 중인 동안 `Creating` 상태 이면 hello 가져오기/내보내기 서비스 hello 드라이브 배송된 toohello 데이터 센터 적용 되지 않은 것으로 가정 합니다. 한 작업 hello에 남아 있을 수 `Creating` tootwo 주, 지나면 hello 서비스에 의해 삭제 자동으로 구성에 대 한 상태입니다.<br /><br /> Hello 작업 hello 중인 동안 hello Update Job Properties 작업을 호출 하는 경우 `Creating` 상태 이면 hello 유지 hello `Creating` 상태 및 hello 제한 시간 간격은 재설정 tootwo 주입니다.|
|`Shipping`|Hello 작업의 hello 작업 속성을 업데이트 작업 업데이트 hello 상태 너무 호출 해야 패키지를 배송 한 후`Shipping`합니다. 경우에 hello hello 배송 상태를 설정할 수 있습니다 `DeliveryPackage` (배송 업체 및 추적 번호) 및 hello `ReturnAddress` hello 작업에 대 한 속성이 설정 되어 있는지 합니다.<br /><br /> hello 작업 tootwo 주를 hello 배송 상태에 대 한 유지 됩니다. 2 주 경과한 hello 드라이브를 받지 못한 경우 가져오기/내보내기 서비스 운영자 hello 알림을 받게 됩니다.|
|`Received`|모든 드라이브 hello 데이터 센터에서 받은, hello 작업 상태 toohello Received 상태가 설정 됩니다.|
|`Transferring`|Hello 드라이브 hello 데이터 센터에서 받은 후 하나 이상의 드라이브가 처리를 시작 하는 hello 작업 상태를 설정할 toohello `Transferring` 상태입니다. Hello 참조 `Drive States` 아래의 세부 정보에 대 한 섹션.|
|`Packaging`|모든 드라이브 처리를 완료 한 후 hello 작업에에서 표시 됩니다 hello `Packaging` hello 드라이브는 배송된 백 toohello 고객 될 때까지 상태입니다.|
|`Completed`|모든 드라이브 배송된 백 toohello 고객 된 hello 작업이 오류 없이 완료 된 경우, 다음 hello 작업 설정 됩니다 toohello `Completed` 상태입니다. hello 작업을 자동으로 삭제 hello에서 90 일이 지나면 `Completed` 상태입니다.|
|`Closed`|모든 드라이브 배송된 백 toohello 고객 된 내용이 있는 경우 모든 오류 hello 작업의 hello 처리 하는 동안, 후 다음 hello 작업을 설정할 toohello `Closed` 상태입니다. hello 작업을 자동으로 삭제 hello에서 90 일이 지나면 `Closed` 상태입니다.|

작업은 특정 상태에서만 취소할 수 있습니다. 취소 된 작업 hello 데이터 복사 단계를 건너뛰고 하지만 그렇지 않으면 취소 되지 않은 작업으로 동일한 상태 전환 hello을 따릅니다.

hello 다음 설명 오류가 있을 때 hello 작업에는 hello 영향 뿐만 아니라 각 작업 상태에 대 한 발생할 수 있는 오류입니다.

|작업 상태|이벤트|해결 방법/다음 단계|
|---------------|-----------|------------------------------|
|`Creating or Undefined`|작업에 대 한 하나 이상의 드라이브가 도착 했지만 hello 작업 hello에 없는 `Shipping` 상태 또는 hello 서비스에서 hello 작업의 기록이 없습니다.|hello 가져오기/내보내기 서비스 운영 팀 toocontact hello 고객 toocreate 또는 hello 작업 작업과 필요한 정보 toomove hello 앞으로 업데이트 됩니다.<br /><br /> Hello 운영 팀 후 2 주 안에 없습니다 toocontact hello 고객 이면 hello 운영 팀 tooreturn hello 드라이브를 시도 합니다.<br /><br /> Hello 드라이브를 반환할 수 없습니다 및 hello 고객에 연결할 수 없습니다는 hello 이벤트에서 90 일 안에 hello 드라이브는 안전 하 게 제거 됩니다.<br /><br /> 상태로 너무 업데이트 될 때까지 작업을 처리할 수에 유의`Shipping`합니다.|
|`Shipping`|hello 직업 패키지가 2 주 이상 동안 도착 하지 않았습니다.|hello 운영 팀은 hello 누락 된 패키지의 hello 고객을 게 알립니다. Hello 고객의 응답에 따라 hello 운영 팀은 확장 hello 패키지 tooarrive에 대 한 hello 간격 toowait 하거나 hello 작업을 취소 하십시오.<br /><br /> Hello 이벤트에 해당 hello 고객에 연결할 수 없는 되었거나 hello 운영 팀 hello에서 동작 toomove hello 작업 시작 30 일 이내 응답 하지 않으면 `Shipping` 상태 직접 toohello `Closed` 상태입니다.|
|`Completed/Closed`|hello 되지 hello 반송 주소에 도달 드라이버나 배송 (내보내기 작업의 유일한 tooan 적용 됨) 중에 손상 되었습니다.|Hello 드라이브 hello 반송 주소에 도달 하지 않으므로 hello 고객은 첫 번째 호출 hello Get Job 작업이 또는에서 hello 작업 상태를 확인 hello 포털 tooensure 드라이브가 배송 되었음을 해당 hello 합니다. Hello 드라이브 배송 된 후 hello 고객 hello 배송 공급자 tootry에 게 문의 하 고 hello 드라이브를 찾을 해야 합니다.<br /><br /> Hello 드라이브 배송 하는 동안 손상 된 경우 hello 고객 다른 내보내기 작업 또는 다운로드 hello 누락 된 blob toorequest 좋습니다.|
|`Transferring/Packaging`|작업의 반송 주소가 잘못되었거나 누락되었습니다.|hello 운영 팀 toohello 책임자 hello 작업 tooobtain hello 올바른 주소에 연락 합니다.<br /><br /> Hello 이벤트에 해당 hello 고객 연락할 수 없는 경우 hello 90 일 이내에 드라이브를 안전 하 게 폐기 합니다.|
|`Creating / Shipping/ Transferring`|가져올 드라이브 toobe hello 목록에 나타나지 않는 드라이브 hello 배송 패키지에에서 포함 됩니다.|hello 추가 드라이브 처리 되지 않습니다 및 hello 작업이 완료 될 때 toohello 고객이 반환 됩니다.|

## <a name="drive-states"></a>드라이브 상태
hello 테이블과 아래 hello 다이어그램으로 가져오기 또는 내보내기 작업 전환 될 때 개별 드라이브의 수명 주기 hello에 설명 합니다. 호출 hello 여 hello 현재 드라이브 상태를 검색할 수 있습니다 `Get Job` 작업 및 검사 hello `State` hello 요소의 `DriveList` 속성입니다.

![드라이브 상태](./media/storage-import-export-retrieving-state-info-for-a-job/DriveStates.png "드라이브 상태")

hello 다음 표에서 드라이브가 통과할 수 있는 각 상태.

|드라이브 상태|설명|
|-----------------|-----------------|
|`Specified`|가져오기 작업에 대 한 hello 작업이 Put Job 작업 hello로 만들어질 때 드라이브에 대 한 hello 초기 상태는 hello `Specified` 상태입니다. 내보내기 작업에 대 한 hello 작업이 만들어질 때 드라이브를 지정 하므로 hello 초기 드라이브 상태는 hello `Received` 상태입니다.|
|`Received`|hello toohello 전환 `Received` 가져오기/내보내기 서비스 운영자가 가져오기 작업에 대 한 회사를 전달 하는 hello 로부터 받은 hello 드라이브를 처리 하는 경우 hello 상태입니다. 내보내기 작업에 대 한 hello 초기 드라이브 상태는 hello `Received` 상태입니다.|
|`NeverReceived`|hello 드라이브 toohello 들어왔다 `NeverReceived` 직업 패키지가 도착 했지만 hello 패키지 hello 드라이브를 포함 하지 않는 경우 hello 상태입니다. Hello 서비스 hello 배송 정보를 받았지만 hello 패키지 hello 데이터 센터에 아직 도착 하지 않은 후 2 주 후 경과 된 경우에이 상태로 드라이브를 이동할 수도 있습니다.|
|`Transferring`|Toohello 이동 됩니다 `Transferring` 상태 때 hello tootransfer 데이터로 hello 드라이브 tooWindows Azure 저장소 서비스를 시작 합니다.|
|`Completed`|Toohello 이동 됩니다 `Completed` hello 서비스 모든 hello 데이터를 오류 없이 성공적으로 전송 때 상태입니다.|
|`CompletedMoreInfo`|Toohello 이동 됩니다 `CompletedMoreInfo` 때 hello 서비스에서 문제가 발생 했습니다 일부 데이터를 복사 하는 동안에서 또는 toohello 드라이브 상태입니다. hello 정보는 오류, 경고 또는 blob 덮어쓰기에 대 한 정보 메시지에 포함할 수 있습니다.|
|`ShippedBack`|hello 드라이브 toohello 들어왔다 `ShippedBack` hello 데이터 센터 백 toohello 반송 주소에서 배송 되는 경우 상태입니다.|

hello 다음 표에 hello 드라이브 오류 상태와 각 상태에 대해 수행 하는 hello 작업이 있습니다.

|드라이브 상태|이벤트|해결 방법/다음 단계|
|-----------------|-----------|-----------------------------|
|`NeverReceived`|로 표시 된 드라이브 `NeverReceived` (hello 작업 배송의 일부로 수신 되지 않았으므로) 이므로 다른 배송으로 도착 합니다.|hello 운영 팀에 들어왔다 hello 드라이브 toohello `Received` 상태입니다.|
|`N/A`|작업의 일부가 아닌 드라이브는 다른 작업의 일부로 hello 데이터 센터에 도착 합니다.|hello 드라이브는 추가 드라이브로 표시 하 고 hello 원래 패키지와 관련 된 hello 작업이 완료 될 때 toohello 고객 반환 됩니다.|

## <a name="faulted-states"></a>오류(Faulted) 상태
Hello 작업 또는 드라이브 오류가 발생 하면 일반적으로 예상된 수명 주기를 통한 tooprogress 작업 또는 드라이브로 이동 될 예정는 `Faulted` 상태입니다. 해당 시점에 hello 운영 팀에 전자 메일 이나 전화를 통해 hello 고객을 연락 합니다. Hello 문제가 해결 되 면 hello faulted 작업 또는 드라이브 hello 부족 수행 될 `Faulted` 적절 한 상태를 상태 그리고 hello로 이동 합니다.

## <a name="next-steps"></a>다음 단계

* [Hello 가져오기/내보내기 서비스 REST API를 사용 하 여](storage-import-export-using-the-rest-api.md)
