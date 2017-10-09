---
title: "Azure 데이터 레이크 저장소에 이벤트 허브에서 aaaCapture 데이터 | Microsoft Docs"
description: "이벤트 허브에서 사용 하 여 Azure 데이터 레이크 저장소 toocapture 데이터"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/28/2017
ms.author: nitinme
ms.openlocfilehash: 09b17bd0b47043bd2c83dba72c01a8064f206a0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-store-toocapture-data-from-event-hubs"></a>이벤트 허브에서 사용 하 여 Azure 데이터 레이크 저장소 toocapture 데이터

Azure 데이터 레이크 저장소 toocapture 데이터 toouse Azure 이벤트 허브에서 수신 하는 방법에 대해 알아봅니다.

## <a name="prerequisites"></a>필수 조건

* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.

* **Azure 데이터 레이크 저장소 계정**. 방법에 대 한 지침은 toocreate 하나, 참조 [Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)합니다.

*  **Event Hubs 네임스페이스**. 자세한 내용은 [Event Hubs 네임스페이스 만들기](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace)를 참조하세요. Hello 데이터 레이크 저장소 계정 및 hello 이벤트 허브 네임 스페이스에에서 있어야 hello 동일한 Azure 구독.


## <a name="assign-permissions-tooevent-hubs"></a>TooEvent 허브 사용 권한 할당

이 섹션에서는 이벤트 허브에서 toocapture hello 데이터 hello 계정 내에서 폴더를 만듭니다. 또한 권한을 할당할 있습니다 tooEvent 허브 데이터 레이크 저장소 계정으로 데이터를 쓸 수 있도록 합니다. 

1. 이벤트 허브에서 toocapture 데이터 및 클릭 hello 데이터 레이크 저장소 계정 열기 **데이터 탐색기**합니다.

    ![Data Lake Store 데이터 탐색기](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data Lake Store 데이터 탐색기")

2.  클릭 **새 폴더** toocapture hello 데이터를 원하는 폴더에 대 한 이름을 입력 합니다.

    ![Data Lake Store에 새 폴더 만들기](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Data Lake Store에 새 폴더 만들기")

3. Hello 데이터 레이크 저장소의 hello 루트에서 사용 권한을 할당 합니다. 

    a. 클릭 **데이터 탐색기**hello 루트 hello Data Lake 저장소 계정에 선택한 다음 클릭 **액세스**합니다.

    ![Data Lake Store 루트에 대한 권한 할당](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Data Lake Store 루트에 대한 권한 할당")

    b. **액세스** 아래에서 **추가**를 클릭하고 **사용자 또는 그룹 선택**을 클릭한 후 `Microsoft.EventHubs`를 검색합니다. 

    ![Data Lake Store 루트에 대한 권한 할당](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Data Lake Store 루트에 대한 권한 할당")
    
    **선택**을 클릭합니다.

    c. **권한 할당**에서 **권한 선택**을 클릭합니다. 설정 **권한을** 너무**Execute**합니다. 설정 **추가할** 너무**이 폴더와 모든 자식**합니다. 설정 **로 추가** 너무**액세스 권한 항목 및 기본 권한 항목**합니다.

    ![Data Lake Store 루트에 대한 권한 할당](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Data Lake Store 루트에 대한 권한 할당")

    **확인**을 클릭합니다.

4. Toocapture 데이터 Data Lake 저장소 계정에서 hello 폴더에 대 한 권한을 할당 합니다.

    a. 클릭 **데이터 탐색기**hello Data Lake 저장소 계정에서에서 hello 폴더를 선택 하 고 클릭 한 다음, **액세스**합니다.

    ![Data Lake Store 폴더에 대한 권한 할당](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Data Lake Store 폴더에 대한 권한 할당")

    b. **액세스** 아래에서 **추가**를 클릭하고 **사용자 또는 그룹 선택**을 클릭한 후 `Microsoft.EventHubs`를 검색합니다. 

    ![Data Lake Store 폴더에 대한 권한 할당](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Data Lake Store 폴더에 대한 권한 할당")
    
    **선택**을 클릭합니다.

    c. **권한 할당**에서 **권한 선택**을 클릭합니다. 설정 **권한을** 너무**읽기, 쓰기,** 및 **Execute**합니다. 설정 **추가할** 너무**이 폴더와 모든 자식**합니다. 마지막으로, 설정 **로 추가** 너무**액세스 권한 항목 및 기본 권한 항목**합니다.

    ![Data Lake Store 폴더에 대한 권한 할당](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Data Lake Store 폴더에 대한 권한 할당")
    
    **확인**을 클릭합니다. 

## <a name="configure-event-hubs-toocapture-data-toodata-lake-store"></a>이벤트 허브 toocapture 데이터 tooData 레이크 저장소 구성

이 섹션에서는 Event Hubs 네임스페이스 내에 Event Hubs를 만듭니다. Hello 이벤트 허브 toocapture 데이터 tooan Azure 데이터 레이크 저장소 계정을 구성할 수도 있습니다. 이 섹션에서는 Event Hubs 네임스페이스를 이미 만들었다고 가정합니다.

2. Hello에서 **개요** 창의 hello 이벤트 허브 네임 스페이스의 클릭 **+ 이벤트 허브**합니다.

    ![이벤트 허브 만들기](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "이벤트 허브 만들기")

3. Hello 다음 tooconfigure 이벤트 허브 toocapture 데이터 tooData 레이크 저장소 값을 제공 합니다.

    ![이벤트 허브 만들기](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "이벤트 허브 만들기")

    a. 이벤트 허브 hello에 대 한 이름을 제공 합니다.
    
    b. 이 자습서에 대 한 설정 **파티션 수** 및 **메시지 보존** toohello 기본값입니다.
    
    c. 설정 **캡처** 너무**에**합니다. 집합 hello **시간 창** (얼마나 자주 toocapture) 및 **크기 창** (데이터 크기 toocapture). 
    
    d. 에 대 한 **캡처 공급자**선택, **Azure 데이터 레이크 저장소** hello 선택 hello 앞에서 만든 데이터 레이크 저장소 및 합니다. 에 대 한 **데이터 레이크 경로**, hello Data Lake 저장소 계정에서에서 만든 hello 폴더의 hello 이름을 입력 합니다. Tooprovide hello 상대 경로 toohello 폴더를 하기만 하면 됩니다.

    e. Hello 둡니다 **샘플 캡처 파일 이름 형식을** toohello 기본값입니다. 이 옵션은 hello 캡처 폴더 아래에 생성 된 hello 폴더 구조를 제어 합니다.

    f. **만들기**를 클릭합니다.

## <a name="test-hello-setup"></a>테스트 hello 설정

이제 데이터 toohello Azure 이벤트 허브를 전송 하 여 hello 솔루션을 테스트할 수 있습니다. Hello 지침에 따라 [tooAzure 이벤트 허브 이벤트를 보내는](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md)합니다. Hello 데이터를 보내기 시작 되 면 hello 데이터가 표시 Data Lake 저장소에 반영 지정한 hello 폴더 구조를 사용 하 여 합니다. 예를 들어 hello 스크린 샷 데이터 레이크 저장소의 뒤에 표시 된 대로 폴더 구조를 표시 합니다.

![Data Lake Store의 샘플 EventHub 데이터](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Data Lake Store의 샘플 EventHub 데이터")

> [!NOTE]
> 이벤트 허브로 들어오는 메시지가 없는 경우에 이벤트 허브 hello Data Lake 저장소 계정에만 hello 헤더를 사용 하 여 빈 파일을 씁니다. hello이 파일은 hello에 동일한 사용자가 제공한 hello 이벤트 허브를 만드는 동안 시간 간격입니다.
> 
>

## <a name="analyze-data-in-data-lake-store"></a>Data Lake 저장소의 데이터 분석

데이터 레이크 저장소의 hello 데이터를 tooprocess 및 수치 연산 hello 데이터 분석 작업을 실행할 수 있습니다. 참조 [USQL Avro 예제](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) 방법은 toodo이 Azure 데이터 레이크 분석을 사용 하 여 합니다.
  

## <a name="see-also"></a>참고 항목
* [데이터 레이크 저장소의 데이터 보호](data-lake-store-secure-data.md)
* [Azure 저장소 Blob tooData Lake 저장소에서 데이터 복사](data-lake-store-copy-data-azure-storage-blob.md)
