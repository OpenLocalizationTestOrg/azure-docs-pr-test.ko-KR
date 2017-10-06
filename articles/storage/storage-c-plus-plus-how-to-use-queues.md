---
title: "aaaHow toouse 큐 저장소 (c + +) | Microsoft Docs"
description: "어떻게 toouse hello azure에서 큐 저장소 서비스에 알아봅니다. 샘플은 C++로 작성되었습니다."
services: storage
documentationcenter: .net
author: cbrooksmsft
manager: jahogg
editor: tysonn
ms.assetid: c8a36365-29f6-404d-8fd1-858a7f33b50a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 05/11/2017
ms.author: cbrooksmsft
ms.openlocfilehash: 755380824890ad83774e14d258975915e10cfede
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-c"></a>어떻게 toouse c + +에서 큐 저장소
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>개요
이 가이드 어떻게 tooperform 일반적인 시나리오를 사용 하 여 hello Azure 큐 저장소 서비스에 표시 됩니다. hello 예제 c + +에서 작성 되 고 hello를 사용 하 여 [c + +에 대 한 Azure 저장소 클라이언트 라이브러리](http://github.com/Azure/azure-storage-cpp/blob/master/README.md)합니다. hello 가이드에서 다루는 시나리오 포함 **삽입**, **관찰**, **가져오는**, 및 **삭제** 메시지를 큐와  **만들기 및 큐 삭제**합니다.

> [!NOTE]
> 이 가이드의 대상으로 c + + 버전 1.0.0 이상용 Azure 저장소 클라이언트 라이브러리를 hello 합니다. hello 권장 버전을 통해 사용할 수 있는 저장소 클라이언트 라이브러리, 2.2.0 [NuGet](http://www.nuget.org/packages/wastorage) 또는 [GitHub](http://github.com/Azure/azure-storage-cpp/)합니다.
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>C++ 응용 프로그램 만들기
이 가이드에서는 C++ 응용 프로그램 내에서 실행할 수 있는 저장소 기능을 사용합니다.

toodo tooinstall, 나오는 c + +에 대 한 Azure 저장소 클라이언트 라이브러리를 hello 및 Azure 구독에 Azure 저장소 계정을 만듭니다.

Azure 저장소 클라이언트 라이브러리 tooinstall hello c + +에 대 한 hello 다음 메서드를 사용할 수 있습니다.

* **Linux:** hello에 제공 된 hello 지침에 따라 [c + + 추가 정보에 대 한 Azure 저장소 클라이언트 라이브러리](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) 페이지.
* **Windows:** Visual Studio에서 **도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔**을 클릭합니다. Hello에 형식 hello 다음 명령은 [NuGet 패키지 관리자 콘솔](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) 누릅니다 **ENTER**합니다.

```  
Install-Package wastorage
```

## <a name="configure-your-application-tooaccess-queue-storage"></a>사용자 응용 프로그램 tooaccess 큐 저장소를 구성 합니다.
Hello 다음 포함 toouse hello Azure 저장소 Api tooaccess 큐 저장할 hello c + + 파일의 문 toohello 맨 위에 추가 합니다.  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>Azure 저장소 연결 문자열 설정
Azure 저장소 클라이언트는 저장소 연결 문자열 toostore 끝점을 사용 하 여 및 데이터 관리 서비스에 액세스 하기 위한 자격 증명입니다. 형식에 따라, hello에 나열 된 hello 저장소 계정에 대 한 저장소 계정 및 hello 저장소 액세스 키의 hello 이름을 사용 하 여 hello hello 저장소 연결 문자열을 제공 해야, 클라이언트 응용 프로그램에서 실행할 때는 [Azure 포털](https://portal.azure.com)hello에 대 한 *AccountName* 및 *AccountKey* 값입니다. 저장소 계정 및 액세스 키에 대한 자세한 내용은 [Azure 저장소 계정 정보](storage-create-storage-account.md)를 참조하세요. 이 예에서는 정적 필드 toohold hello 연결 문자열을 선언할 수는 방법을 보여 줍니다.  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest 응용 프로그램 사용자의 로컬 Windows 컴퓨터에서 Microsoft Azure hello를 사용할 수 있습니다 [저장소 에뮬레이터](storage-use-emulator.md) hello로 설치 된 [Azure SDK](https://azure.microsoft.com/downloads/)합니다. hello 저장소 에뮬레이터는 로컬 개발 컴퓨터에 Azure에서 제공 하는 hello Blob, 큐 및 테이블 서비스를 시뮬레이션 하는 유틸리티입니다. hello 다음 예제는 어떻게는 정적 필드 toohold hello 연결 문자열 tooyour 로컬 저장소 에뮬레이터를 선언할 수 있습니다.  

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

toostart hello Azure 저장소 에뮬레이터를 선택 하는 hello **시작** 단추를 클릭 하거나 눌러 hello **Windows** 키입니다. 입력을 시작 **Azure 저장소 에뮬레이터**를 선택 하 고 **Microsoft Azure 저장소 에뮬레이터** hello 응용 프로그램 목록에서 합니다.

hello 다음과 같은 샘플 가정 이러한 두 가지 방법 tooget hello 저장소 연결 문자열 중 하나 사용 하 합니다.

## <a name="retrieve-your-connection-string"></a>연결 문자열 검색
Hello를 사용할 수 있습니다 **cloud_storage_account** 클래스 toorepresent 저장소 계정 정보. tooretrieve 저장소 계정 hello 저장소 연결 문자열 정보, hello를 사용할 수 있습니다 **구문 분석** 메서드.

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a>방법: 큐 만들기
**cloud_queue_client** 개체를 통해 큐에 대한 참조 개체를 가져올 수 있습니다. hello 다음 코드에서는 **cloud_queue_client** 개체입니다.

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

사용 하 여 hello **cloud_queue_client** tooget toouse 원하는 참조 toohello 큐 개체입니다. 존재 하지 않는 경우 hello 큐를 만들 수 있습니다.

```cpp
// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a>방법: 큐에 메시지 삽입
tooinsert를 기존 큐에 메시지를 먼저 새로 만들려면 **cloud_queue_message**합니다. 그런 다음 호출 하는 hello **add_message** 메서드. **cloud_queue_message**는 문자열 또는 **바이트** 배열에서 만들 수 있습니다. 코드 (존재 하지 않는) 하는 경우 큐를 만듦 및 삽입 hello 메시지 'Hello World' 다음과 같습니다.

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
queue.create_if_not_exists();

// Create a message and add it toohello queue.
azure::storage::cloud_queue_message message1(U("Hello, World"));
queue.add_message(message1);  
```

## <a name="how-to-peek-at-hello-next-message"></a>방법: hello 다음 메시지 피킹
Hello를 호출 하 여 hello 큐에서 제거 하지 않고 큐의 hello 앞에 hello 메시지를 피킹할 수 있습니다 **peek_message** 메서드.

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Peek at hello next message.
azure::storage::cloud_queue_message peeked_message = queue.peek_message();

// Output hello message content.
std::wcout << U("Peeked message content: ") << peeked_message.content_as_string() << std::endl;
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>방법: 대기 중인된 메시지의 hello 내용을 변경
메시지 전체 hello 큐에서의 hello 내용을 변경할 수 있습니다. Hello 메시지 작업 작업을 나타내는 경우에이 기능 tooupdate hello hello 작업 작업의 상태를 사용할 수 있습니다. 코드 다음 hello hello 큐 메시지를 새 내용으로 업데이트 하 고 집합 hello 가시성 제한 시간 tooextend 다른 60 초입니다. 이 hello 메시지와 관련 된 작업의 hello 상태를 저장 하 고 hello 클라이언트 hello 메시지에서 작업 하는 다른 분 toocontinue를 제공 합니다. 부터 hello toohardware 또는 소프트웨어 오류로 인해 실패 하면 처리 단계를 통해 toostart 필요 없이 큐의 메시지에이 기술을 tootrack multi-step 워크플로 사용할 수 있습니다. 일반적으로는 다시 시도 횟수를 보관할 때 고 hello 메시지를 여러 개 n 번 다시 시도 하는 경우 파일을 삭제 합니다. 이 기능은 처리될 때마다 응용 프로그램 오류를 트리거하는 메시지를 차단하여 보호해 줍니다.

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_conection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get hello message from hello queue and update hello message contents.
// hello visibility timeout "0" means make it visible immediately.
// hello visibility timeout "60" means hello client can get another minute toocontinue
// working on hello message.
azure::storage::cloud_queue_message changed_message = queue.get_message();

changed_message.set_content(U("Changed message"));
queue.update_message(changed_message, std::chrono::seconds(60), true);

// Output hello message content.
std::wcout << U("Changed message content: ") << changed_message.content_as_string() << std::endl;  
```

## <a name="how-to-de-queue-hello-next-message"></a>방법: hello 다음 메시지 큐에서 제거
다음 코드는 2단계를 거쳐 큐에서 메시지를 제거합니다. 호출 하는 경우 **get_message**, 큐에 있는 hello 다음 메시지를 가져옵니다. 반환 된 메시지 **get_message** 보이지 않는 tooany이이 큐에서 메시지를 읽을 다른 코드 됩니다. toofinish 제거 hello 큐에서에서 메시지를 hello 호출 해야 **delete_message**합니다. 이 2 단계 프로세스의 메시지를 제거 하는 코드 tooprocess toohardware 또는 소프트웨어 오류가, 코드의 다른 인스턴스는 메시지를 가져올 수 없으면 동일한 메시지 hello 고 다시 시도 하십시오 보장 합니다. 코드 호출 **delete_message** 직후 hello 메시지를 처리 합니다.

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get hello next message.
azure::storage::cloud_queue_message dequeued_message = queue.get_message();
std::wcout << U("Dequeued message: ") << dequeued_message.content_as_string() << std::endl;

// Delete hello message.
queue.delete_message(dequeued_message);
```

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a>방법: 큐에서 메시지를 제거하는 추가 옵션 활용
큐에서 메시지 검색을 사용자 지정할 수 있는 방법으로는 두 가지가 있습니다. 첫째, 일괄 처리 메시지 (위쪽 too32)을 얻을 수 있습니다. 둘째, 하면 프로그램 코드를 더 길거나 더 짧은 표시 안 함 시간 제한이 설정할 수 있습니다 또는 적은 시간 toofully 각 메시지를 처리 합니다. hello 다음 코드 예제에서는 hello **get_messages** 메서드 tooget 20 메시지 한 번 호출에서 합니다. 그런 다음 **for** 루프를 사용하여 각 메시지를 처리합니다. 또한 각 메시지에 대 한 hello 표시 안 함 시간 초과 toofive 분을 설정합니다. 5 분 해당 hello 참고 hello에서 모든 메시지에 대 한 시작 시간이, 하므로 5 분 이후 경과한 hello 호출 너무 나면**get_messages**, 모든 메시지는 삭제 되지 않았으므로 다시 표시 됩니다.

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Dequeue some queue messages (maximum 32 at a time) and set their visibility timeout to
// 5 minutes (300 seconds).
azure::storage::queue_request_options options;
azure::storage::operation_context context;

// Retrieve 20 messages from hello queue with a visibility timeout of 300 seconds.
std::vector<azure::storage::cloud_queue_message> messages = queue.get_messages(20, std::chrono::seconds(300), options, context);

for (auto it = messages.cbegin(); it != messages.cend(); ++it)
{
    // Display hello contents of hello message.
    std::wcout << U("Get: ") << it->content_as_string() << std::endl;
}
```

## <a name="how-to-get-hello-queue-length"></a>방법: hello 큐 길이 가져오기
큐에 있는 hello 메시지 수의 예측을 얻을 수 있습니다. hello **download_attributes** 메서드 hello 큐 서비스 tooretrieve hello 메시지 수를 포함 된 hello 큐 특성을 요청 합니다. hello **approximate_message_count** 메서드 hello 큐에 있는 hello 대략적인 메시지 수를 가져옵니다.

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Fetch hello queue attributes.
queue.download_attributes();

// Retrieve hello cached approximate message count.
int cachedMessageCount = queue.approximate_message_count();

// Display number of messages.
std::wcout << U("Number of messages in queue: ") << cachedMessageCount << std::endl;  
```

## <a name="how-to-delete-a-queue"></a>방법: 큐 삭제
큐와 모든 hello 메시지에 포함 된, 호출 hello toodelete **delete_queue_if_exists** hello 큐 개체에서 메서드.

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// If hello queue exists and delete it.
queue.delete_queue_if_exists();  
```

## <a name="next-steps"></a>다음 단계
큐 저장소의 hello 기본 사항 학습 한, 했으므로 이러한 링크 toolearn Azure 저장소에 대 한 자세한를 수행 합니다.

* [어떻게 toouse c + +에서 Blob 저장소](storage-c-plus-plus-how-to-use-blobs.md)
* [어떻게 toouse c + +에서 테이블 저장소](storage-c-plus-plus-how-to-use-tables.md)
* [C++에서 Azure 저장소 리소스 나열](storage-c-plus-plus-enumeration.md)
* [C++용 Storage Client Library 참조(영문)](http://azure.github.io/azure-storage-cpp)
* [Azure 저장소 설명서](https://azure.microsoft.com/documentation/services/storage/)