---
title: "이벤트 허브 캡처 aaaAzure 포털을 통해 사용 하도록 설정 | Microsoft Docs"
description: "Hello Azure 포털을 사용 하 여 hello 이벤트 허브 캡처 기능을 사용 하도록 설정 합니다."
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: 27c7528552c497a4d98873a22bd56a991c66247c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-event-hubs-capture-using-hello-azure-portal"></a>이벤트 허브 hello Azure 포털을 사용 하 여 캡처를 사용 하도록 설정

Hello 이벤트 허브를 만들 때 hello를 사용 하 여 캡처를 구성할 수 있습니다 [Azure 포털](https://portal.azure.com)합니다. 두 캡처 hello 데이터 tooan Azure 수 [Blob 저장소](https://azure.microsoft.com/services/storage/blobs/) 컨테이너 또는 tooan [Azure 데이터 레이크 저장소](https://azure.microsoft.com/services/data-lake-store/) 계정.

## <a name="capture-data-tooan-azure-storage-account"></a>캡처 데이터 tooan Azure 저장소 계정  

이벤트 허브를 만들 때 hello를 클릭 하 여 캡처를 설정할 수 있습니다 **에** hello 단추 **이벤트 허브 만들기** 포털 블레이드입니다. 그런 다음를 클릭 하 여 저장소 계정 및 컨테이너를 지정 **Azure 저장소** hello에 **캡처 공급자** 상자입니다. 이벤트 허브 캡처를 사용 하므로 서비스 간 인증 된 저장소에는 저장소 연결 문자열을 toospecify를 설치할 필요가 없습니다. hello 리소스 선택기 저장소 계정에 대 한 hello 리소스 URI를 자동으로 선택 합니다. Azure Resource Manager를 사용하는 경우 이 URI를 문자열로 명백히 제공해야 합니다.

hello 기본 시간 창은 5 분입니다. hello 최소값은 1, hello 최대 15입니다. hello **크기** 창에는 10-500 m B의 범위입니다.

![][1]

## <a name="capture-data-tooan-azure-data-lake-store-account"></a>캡처 데이터 tooan Azure 데이터 레이크 저장소 계정

데이터 레이크 저장소 계정당 하나만 그리고 이벤트 허브 toocapture 데이터 tooAzure Data Lake 저장소를 만듭니다.

### <a name="create-an-azure-data-lake-store-account-and-folders"></a>Azure Data Lake Store 계정 및 폴더 만들기

1. Hello 지침에 데이터 레이크 저장소 계정을 만들 [hello Azure 포털을 사용 하 여 Azure 데이터 레이크 저장소 시작](../data-lake-store/data-lake-store-get-started-portal.md)합니다. 
2. Hello에 hello 지침에 따라이 계정에서 폴더를 만들고 [Azure 데이터 레이크 저장소 계정에 폴더를 만들고](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) 섹션.
3. 데이터 레이크 저장소 계정 블레이드에서 hello 클릭 **데이터 탐색기**합니다.
4. **액세스**를 클릭합니다.
5. **추가**를 클릭합니다.
6. Hello에 **이름이 나 전자 메일 검색** 상자에 입력 **Microsoft.EventHubs** 한 다음이 옵션을 선택 합니다. 
7. hello **권한을** 탭이 나타납니다. Hello 다음 그림에에서 표시 된 대로 hello 권한을 설정 합니다.

    ![][6]

8. **확인**을 클릭합니다.
9. 이제 toohello 대상 폴더를 찾아보고 hello 폴더 이름을 클릭 하 여 hello 루트 폴더에 폴더를 만듭니다.
10. **액세스**를 클릭합니다.
11. **추가**를 클릭합니다.
12. Hello에 **이름이 나 전자 메일 검색** 상자에 입력 **Microsoft.EventHubs** 한 다음이 옵션을 선택 합니다.
13. hello **권한을** 탭이 다시 나타납니다. Hello 다음 그림에에서 표시 된 대로 hello 권한을 설정 합니다.

    ![][5]

### <a name="create-an-event-hub"></a>이벤트 허브 만들기

1. 해당 hello 이벤트 허브 hello에 있어야 합니다. Azure Data Lake 저장소 방금 만든 hello와 동일한 Azure 구독. Hello를 클릭 하면 만들기 hello 이벤트 허브 **에** 단추 **캡처** hello에 **이벤트 허브 만들기** 포털 블레이드입니다. 
2. Hello에 **이벤트 허브 만들기** 포털 블레이드 **Azure 데이터 레이크 저장소** hello에서 **캡처 공급자** 상자입니다.
3. **데이터 레이크 저장소 선택**, hello hello 및 이전에 만든 데이터 레이크 저장소 계정을 지정 **데이터 레이크 경로** 필드에, 사용자가 만든 hello 경로 toohello 데이터 폴더를 입력 합니다.

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a>기존 이벤트 허브에서 캡처 추가 및 구성

Event Hubs 네임스페이스에 있는 기존 이벤트 허브에 캡처를 구성할 수 있습니다. tooenable 기존 이벤트 허브 또는 toochange 캡처 설정을 캡처합니다, hello 네임 스페이스 tooload hello 클릭 **Essentials** 블레이드에서 tooenable 원하는 하거나 hello 캡처 설정을 변경 하는 hello 이벤트 허브를 클릭 합니다. 마지막 hello를 클릭 하 여 **속성** hello 섹션 블레이드를 열고 hello 다음 그림에에서 나와 있는 것 처럼 hello 캡처 설정을 편집 합니다.

### <a name="azure-blob-storage"></a>데이터 이동

![][2]

### <a name="azure-data-lake-store"></a>Azure Data Lake Store

![][4]

[1]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture1.png
[2]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture2.png
[3]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture3.png
[4]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture4.png
[5]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture5.png
[6]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture6.png

## <a name="next-steps"></a>다음 단계

Azure Resource Manager 템플릿을 사용하여 Event Hubs 캡처를 구성할 수도 있습니다. 자세한 내용은 [Azure Resource Manager 템플릿을 사용하여 캡처를 사용하도록 설정](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)을 참조하세요.
