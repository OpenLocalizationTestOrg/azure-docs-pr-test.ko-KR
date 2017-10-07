---
title: "aaaHow toouse Ruby에서 큐 저장소 | Microsoft Docs"
description: "방법 toouse hello Azure 큐 서비스 toocreate 및 큐 삭제 및 삽입, 및 메시지 삭제에 대해 알아봅니다. 샘플은 Ruby로 작성되었습니다."
services: storage
documentationcenter: ruby
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 59c2d81b-db9c-46ee-ade2-2f0caae6b1e6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 726c7d2f08b2d5938ee5f9dcdc2735e447388856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-ruby"></a>어떻게 toouse Ruby에서 큐 저장소
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>개요
이 가이드에서는 tooperform 일반적인 시나리오를 사용 하 여 Microsoft Azure 큐 저장소 서비스를 hello 하는 방법을 보여 줍니다. hello 샘플 hello Ruby Azure API를 사용 하 여 기록 됩니다.
hello 가이드에서 다루는 시나리오 포함 **삽입**, **관찰**, **가져오는**, 및 **삭제** 메시지를 큐와  **만들기 및 큐 삭제**합니다.

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Ruby 응용 프로그램 만들기
Ruby 응용 프로그램을 만듭니다. 지침은 [Azure VM의 Ruby on Rails 웹 응용 프로그램](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)을 참조하세요.

## <a name="configure-your-application-tooaccess-storage"></a>응용 프로그램 tooAccess 저장소 구성
Azure 저장소 toouse toodownload 및 사용 하 여 hello hello 저장소 REST 서비스와 통신 하는 편리한 라이브러리의 집합을 포함 하는 Ruby azure 패키지 해야 합니다.

### <a name="use-rubygems-tooobtain-hello-package"></a>RubyGems tooobtain hello 패키지 사용
1. **PowerShell**(Windows), **Terminal**(Mac) 또는 **Bash**(Unix)와 같은 명령줄 인터페이스를 사용합니다.
2. "보석" 설치 azure의 hello 명령 창 tooinstall hello 보석 및 종속성을 입력 합니다.

### <a name="import-hello-package"></a>Hello 패키지 가져오기
원하는 텍스트 편집기를 사용 하 여 hello toohello hello toouse 저장소 이점을 얻을 수 Ruby 파일 맨 뒤를 추가 합니다.

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a>Azure 저장소 연결 설정
hello azure 모듈 hello 환경 변수는 읽기 **AZURE\_저장소\_계정** 및 **AZURE\_저장소\_ACCESS_KEY** 에 대 한 정보는 tooconnect tooyour Azure 저장소 계정이 필요합니다. 사용 하기 전에 hello 계정 정보를 지정 해야 이러한 환경 변수가 설정 되지 않은 경우 **Azure::QueueService** 코드 다음 hello로:

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
```

tooobtain hello Azure 포털에서에서 기존 또는 리소스 관리자 저장소에서 이러한 값 계정:

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Toouse 사용할 toohello 저장소 계정을 이동 합니다.
3. Hello 오른쪽에 hello 설정 블레이드에서 클릭 **선택 키**합니다.
4. 나타나는 hello 액세스 키 블레이드에서 hello 선택 키 1 및 2 선택 키 표시 됩니다. 이 둘 중 하나를 사용할 수 있습니다. 
5. Hello 아이콘 toocopy hello 키 toohello 클립보드로 복사를 클릭 합니다. 

tooobtain 클래식 저장소에서 이러한 값 hello 클래식 Azure 포털의 계정:

1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. Toouse 사용할 toohello 저장소 계정을 이동 합니다.
3. 클릭 **액세스 키 관리** hello hello 탐색 창 맨 아래에 있습니다.
4. 팝업 대화 상자 창이 hello, hello 저장소 계정 이름, 기본 액세스 키 및 보조 액세스 키를 표시 됩니다. 선택 키에 대 한 hello 기본 또는 보조 로케이터로 hello 중 하나를 사용할 수 있습니다. 
5. Hello 아이콘 toocopy hello 키 toohello 클립보드로 복사를 클릭 합니다.

## <a name="how-to-create-a-queue"></a>큐를 만드는 방법
hello 다음 코드에서는 **Azure::QueueService** toowork 큐로 사용할 수 있는 개체입니다.

```ruby
azure_queue_service = Azure::QueueService.new
```

사용 하 여 hello **create_queue()** 메서드 toocreate hello로 큐 이름을 지정 합니다.

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a>큐에 메시지를 삽입하는 방법
메시지 큐를 사용 하 여 hello에 tooinsert **create_message()** 메서드 toocreate 새 메시지 toohello 큐에 추가 합니다.

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-hello-next-message"></a>방법: hello 다음 메시지 피킹
Hello를 호출 하 여 hello 큐에서 제거 하지 않고 큐의 hello 앞에 hello 메시지를 피킹할 수 있습니다 **peek\_messages()** 메서드. 기본적으로 **peek\_messages()**는 단일 메시지를 읽습니다. 메시지 수를 지정할 수도 있습니다 toopeek 원하는 합니다.

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-hello-next-message"></a>방법: hello 다음 메시지 큐에서 제거
2단계를 거쳐 큐에서 메시지를 제거할 수 있습니다.

1. 호출 하는 경우 **목록\_messages()**, 기본적으로 큐에 있는 다음 메시지로 hello를 얻을 수 있습니다. 메시지 수를 지정할 수도 있습니다 tooget 원하는 합니다. 반환 된 메시지 hello **목록\_messages()** 보이지 않는 tooany이이 큐에서 메시지를 읽을 다른 코드 됩니다. 매개 변수로 초 hello 표시 제한 시간에 전달 합니다.
2. toofinish 제거 hello 큐에서에서 메시지를 hello 호출 해야 **delete_message()**합니다.

이러한 2 단계 프로세스의 메시지를 제거 되었는지를 확인 다시 toohardware 또는 소프트웨어 오류가, 코드의 다른 인스턴스는 메시지를 가져올 수 하 여 코드 실패 tooprocess hello 같은 메시지와 시도 하는 경우. 코드 호출 **삭제\_message()** 직후 hello 메시지를 처리 합니다.

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>방법: 대기 중인 메시지의 내용을 hello 변경
메시지 전체 hello 큐에서의 hello 내용을 변경할 수 있습니다. 아래 hello 코드 hello를 사용 하 여 **update_message()** 메서드 tooupdate 메시지입니다. hello 메서드 hello 큐 메시지의 popreceipt hello 포함 된 튜플 및 hello 메시지가 hello 큐에 표시 될 때를 나타내는 UTC 날짜 시간 값을 반환 합니다.

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a>dequeuing 메시지의 추가옵션을 설정하는 방법
큐에서 메시지 검색을 사용자 지정할 수 있는 방법으로는 두 가지가 있습니다.

1. 메시지의 배치를 가져올 수 있습니다.
2. 각 메시지를 처리 하는 작은 시간 toofully 또는 코드를 자세히 허용 더 길거나 더 짧은 표시 안 함 시간 제한이 설정할 수 있습니다.

hello 다음 코드 예제에서는 hello **목록\_messages()** 메서드 tooget 15 메시지 한 번 호출에서 합니다. 그런 다음 각 메시지를 인쇄하고 삭제합니다. 또한 각 메시지에 대 한 hello 표시 안 함 시간 초과 toofive 분을 설정합니다.

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-hello-queue-length"></a>방법: hello 큐 길이 가져오기
Hello 큐에 메시지 hello 수의 예측을 얻을 수 있습니다. hello **가져오기\_큐\_metadata()** 메서드 hello 큐에 대 한 hello 큐 서비스 tooreturn hello 대략적인 메시지 수 및 메타 데이터를 요청 합니다.

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a>방법: 큐 삭제
toodelete는 큐와 모든 hello 메시지에 포함 된, 호출 hello **삭제\_queue ()** hello 큐 개체에서 메서드.

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a>다음 단계
큐 저장소의 hello 기본 사항 학습 한, 했으므로 더 복잡 한 저장소 작업에 대 한 이러한 링크 toolearn을 따릅니다.

* Hello 방문 [Azure 저장소 팀 블로그](http://blogs.msdn.com/b/windowsazurestorage/)
* Hello 방문 [Ruby 용 Azure SDK](https://github.com/WindowsAzure/azure-sdk-for-ruby) GitHub의 리포지토리

간의 비교에 대 한 Azure 큐 서비스 및이 아티클과 hello에서 설명 하는 Azure 서비스 버스 큐에 설명 된 hello [어떻게 toouse 서비스 버스 큐](/develop/ruby/how-to-guides/service-bus-queues/) 문서를 참조 하십시오. [Azure 큐 및 서비스 버스 큐-비교 및 대조](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)
