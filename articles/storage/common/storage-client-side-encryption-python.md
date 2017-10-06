---
title: "Microsoft Azure 저장소에 대 한 python aaaClient 쪽 암호화 | Microsoft Docs"
description: "hello Python 용 Azure 저장소 클라이언트 라이브러리는 Azure 저장소 응용 프로그램에 대 한 보안을 최대화 하기 위해 클라이언트 쪽 암호화를 지원합니다."
services: storage
documentationcenter: python
author: lakasa
manager: jahogg
editor: tysonn
ms.assetid: f9bf7981-9948-4f83-8931-b15679a09b8a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/11/2017
ms.author: lakasa
ms.openlocfilehash: 3a52b64f93daf85a55308f8a4bee9c98b2315d4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="client-side-encryption-with-python-for-microsoft-azure-storage"></a>Microsoft Azure Storage용 Python을 이용한 클라이언트쪽 암호화
[!INCLUDE [storage-selector-client-side-encryption-include](../../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a>개요
hello [Python 용 Azure 저장소 클라이언트 라이브러리](https://pypi.python.org/pypi/azure-storage) tooAzure 저장소에 업로드 하 고 toohello 클라이언트를 다운로드 하는 동안 데이터를 해독 하기 전에 클라이언트 응용 프로그램 내에서 데이터를 암호화를 지원 합니다.

> [!NOTE]
> hello Azure 저장소 Python 라이브러리는 미리 보기 상태에서입니다.
> 
> 

## <a name="encryption-and-decryption-via-hello-envelope-technique"></a>암호화 및 암호 해독 hello 봉투 (envelope) 기술을 통해
암호화 및 암호 해독의 hello 프로세스 hello 봉투 (envelope) 기법을 따릅니다.

### <a name="encryption-via-hello-envelope-technique"></a>Hello 봉투 (envelope) 기술을 통해 암호화
Hello 봉투 (envelope) 기술을 통해 암호화 hello 방식으로 다음에서 작동 합니다.

1. hello Azure 저장소 클라이언트 라이브러리는 콘텐츠 암호화 키 (CEK)는 한 번 사용 대칭 키를 생성 합니다.
2. 사용자 데이터는 이 CEK를 사용하여 암호화됩니다.
3. hello CEK 다음 래핑된 hello 키 암호화 키 KEK ()를 사용 하 여 (암호화) 합니다. hello KEK 키 식별자로 식별 되 고 비대칭 키 쌍 또는 대칭 키를 로컬로 관리 되는 일 수 있습니다.
   자체 hello 저장소 클라이언트 라이브러리에 대 한 액세스 tooKEK에 없습니다. hello 라이브러리 hello 키 래핑 KEK hello에서 제공 되는 알고리즘을 호출 합니다. 사용자에 대 한 키 래핑/원하는 경우 사용자 지정 공급자 toouse를 선택할 수 있습니다.
4. hello 암호화 된 데이터는 다음 toohello Azure 저장소 서비스에 업로드 합니다. 몇 가지 추가 암호화 메타 데이터와 함께 hello 래핑된 키 (blob)에 메타 데이터로 저장 또는 보간 hello 암호화 된 데이터 (메시지 큐 및 테이블 엔터티)를 사용 합니다.

### <a name="decryption-via-hello-envelope-technique"></a>Hello 봉투 (envelope) 기술을 통해 암호 해독
Hello 봉투 (envelope) 기술을 통해 암호 해독 hello 방식으로 다음에서 작동 합니다.

1. hello 클라이언트 라이브러리 해당 hello 사용자가 (KEK) hello 키 암호화 키를 로컬로 관리 하는 것으로 가정 합니다. hello 사용자 암호화에 사용 된 tooknow hello 특정 키가 필요 하지 않습니다. 대신, 서로 다른 키 식별자 tookeys 확인 되 면 키 해결 프로그램 수를 설정 하 고 사용 합니다.
2. hello 클라이언트 라이브러리는 hello 서비스에 저장 된 모든 암호화 자료 함께 hello 암호화 된 데이터를 다운로드 합니다.
3. 키 암호화 키 (KEK) hello 래핑되지 않은 (암호 해독 된)를 사용 하 여 hello 래핑된 콘텐츠 암호화 키 (CEK)가 있습니다. 여기서 다시 hello 클라이언트 라이브러리 않아도 액세스 tooKEK 됩니다. 래핑 해제 알고리즘 hello 사용자 지정 공급자를 호출 하기만 합니다.
4. hello 암호화 키 (CEK)는 다음 콘텐츠 toodecrypt hello 암호화 된 사용자 데이터를 사용 합니다.

## <a name="encryption-mechanism"></a>암호화 메커니즘
hello 저장소 클라이언트 라이브러리를 사용 하 여 [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) 주문 tooencrypt 사용자 데이터에서입니다. 특히, AES를 이용한 [CBC(암호화 블록 체인)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) 모드입니다. 각 서비스는 하는 일이 각각 다르므로 여기서 이것들을 살펴볼 것입니다.

### <a name="blobs"></a>Blob
hello 클라이언트 라이브러리는 현재 전체 blob만 암호화를 지원합니다. 사용자가 hello를 사용할 때 암호화가 지원 특히 **만들*** 메서드. 다운로드로는 전체 및 범위 다운로드가 지원되며, 업로드 및 다운로드의 병렬화를 사용할 수 있습니다.

암호화 하는 동안 hello 클라이언트 라이브러리는 임의의 IV (Initialization Vector) 32 바이트는 임의의 콘텐츠 암호화 키 (CEK)와 함께 16 바이트의 생성 되며이 정보를 사용 하 여 hello blob 데이터의 봉투 (envelope) 암호화를 수행 합니다. hello CEK 되 고 몇 가지 추가 암호화 메타 데이터 함께 hello hello 서비스에 암호화 된 blob 메타 데이터를 blob으로 저장 됩니다.

> [!WARNING]
> 편집 하거나 hello blob에 대 한 사용자 고유의 메타 데이터를 업로드 하는 경우 tooensure이 메타이 데이터는 유지 해야 합니다. 이 메타 데이터 없이 새 메타 데이터를 업로드 하는 경우 래핑된 CEK hello, IV 및 기타 메타 데이터는 손실 됩니다 및 hello blob 콘텐츠를 절대로 다시 검색할 수 없는 합니다.
> 
> 

Hello를 사용 하 여 hello 전체 blob의 hello 콘텐츠를 검색에서는 암호화 된 blob 다운로드 **가져오기*** 편의 메서드. 래핑된 CEK 래핑이 해제 하 고 hello IV와 함께 사용 하는 hello (으로 저장 blob 메타 데이터가 예제의) tooreturn hello 암호 해독 데이터 toohello 사용자.

임의의 범위를 다운로드 (**가져오기*** 범위 매개 변수가 있는 메서드에 전달 된) hello에서 암호화 된 blob의 순서 tooget 약간의 추가 데이터는 사용할 수 있는 사용자가 제공 된 hello 범위를 조정 하려면 toosuccessfully decrypt hello 범위를 요청 했습니다.

이 스키마를 사용하여 블록 Blob 및 페이지 Blob만 암호화/암호 해독할 수 있습니다. 추가 Blob에 대한 암호화 지원은 현재 없습니다.

### <a name="queues"></a>큐
큐 메시지의 모든 형식이 될 수, 있으므로 hello 클라이언트 라이브러리 hello 메시지 텍스트에 IV (Initialization Vector) hello 및 hello 암호화 된 콘텐츠 암호화 키 (CEK) 포함 된 사용자 지정 형식을 정의 합니다.

암호화 하는 동안 hello 클라이언트 라이브러리는 32 바이트의 임의 CEK 함께 16 바이트의 임의 IV를 생성 하 고이 정보를 사용 하 여 hello 큐 메시지 텍스트의 봉투 (envelope) 암호화를 수행 합니다. hello CEK 되 고 몇 가지 추가 암호화 메타 데이터 toohello 암호화 된 큐 메시지 추가 됩니다. (아래 참조)이 수정 된 메시지는 hello 서비스에 저장 됩니다.

```
<MessageText>{"EncryptedMessageContents":"6kOu8Rq1C3+M1QO4alKLmWthWXSmHV3mEfxBAgP9QGTU++MKn2uPq3t2UjF1DO6w","EncryptionData":{…}}</MessageText>
```

암호 해독 하는 동안 hello 래핑된 키 hello 큐 메시지에서 추출 되며 래핑이 해제 합니다. 또한 hello IV hello 큐 메시지에서 추출 된 이며 래핑이 해제 hello 키 toodecrypt hello 큐 메시지 데이터와 함께 사용 합니다. Hello 암호화 메타 데이터를 작으면 (500 바이트의 경우) 아래 큐 메시지에 대 한 hello 64KB 제한에 대해 계산지 않습니다 것, hello 영향을 관리할 수 있어야 하므로 note 합니다.

### <a name="tables"></a>테이블
삽입을 위한 엔터티 속성의 클라이언트 라이브러리 지원 암호화 hello 및 교체 작업 합니다.

> [!NOTE]
> 병합은 현재 지원 되지 않습니다. 속성 하위 집합 암호화 된 다른 키를 사용 하 여 이전에, 이후 hello 새 속성을 병합 하 고 hello 메타 데이터를 업데이트 하기만 하면 데이터가 손실 됩니다. Hello 서비스에서 tooread hello 기존 엔터티를 호출 추가 서비스를 만드는 또는 속성 당 새 키를 사용 하는 적합 하지 않은 성능상의 이유로 필요 하거나 병합 합니다.
> 
> 

테이블 데이터 암호화는 다음과 같이 작동합니다.

1. 사용자가 hello 속성 toobe 암호화를 지정 합니다.
2. hello 클라이언트 라이브러리는 임의의 IV (Initialization Vector)의 모든 엔터티에 대 한 32 바이트 (CEK) 임의의 콘텐츠 암호화 키와 함께 16 바이트를 생성 하 고 hello 개별 속성 toobe 당 새 IV를 파생 하 여 암호화에서 봉투 (envelope) 암호화를 수행 합니다. 속성입니다. 암호화 된 hello 속성 이진 데이터로 저장 됩니다.
3. hello CEK 되 고 그런 다음 몇 가지 추가 암호화 메타 데이터는 두 개의 추가 예약 된 속성으로 저장 합니다. 먼저 예약 된 hello 속성 (\_ClientEncryptionMetadata1)은 4, 버전 및 래핑된 키에 대 한 hello 정보를 보유 하는 문자열 속성입니다. 두 번째 예약된 속성 hello (\_ClientEncryptionMetadata2) 암호화 된 hello 속성에 대 한 hello 정보를 보유 하는 이진 속성입니다. 이 두 번째 속성에 대 한 정보를 hello (\_ClientEncryptionMetadata2) 암호화 됩니다.
4. Toothese 추가 예약 된 속성 암호화에 필요, 인해 이제가 있습니다 252 대신 사용자 지정 속성을 250만. hello hello 엔터티의 전체 크기는 1MB 미만 이어야 합니다.
   
   문자열 속성만 암호화 할 수 있다는 것을 참고하세요. 다른 유형의 속성 암호화 toobe 인 경우 변환 된 toostrings 되어야 합니다. 이진 속성으로 암호화 하는 hello 문자열 hello 서비스에 저장 됩니다 및 암호 해독 한 후 뒤로 toostrings (EdmType.STRING 형식과 EntityProperties 하지 원시 문자열) 변환 됩니다.
   
   테이블의 경우 또한 toohello 암호화 정책 사용자 지정 해야 hello 속성 toobe 암호화 합니다. 이 중 하나를 저장 하 여 이러한 속성 유형 집합 tooEdmType.STRING hello 사용 하 여 TableEntity 개체에서 수행할 수 있습니다 및 집합 tootrue 또는 설정 hello encryption_resolver_function hello tableservice 개체에 암호화 합니다. 암호화 해결 프로그램은 파티션 키, 행 키, 그리고 속성 이름 및 암호화 여부 속성을 나타내는 부울을 반환하는 함수입니다. 암호화 하는 동안 toohello 통신에 쓰는 동안 속성을 암호화 해야 하는지 여부를 hello 클라이언트 라이브러리 정보 toodecide이를 사용 합니다. 또한 hello 대리자 hello 가능성은 속성이 암호화 주위 논리를 제공 합니다. (예를 들어 X의 경우, A 속성을 암호화하고 그렇지 않은 경우 A와 B 속성을 암호화) 한다는 확인은 필요 하지 않은 tooprovide 읽기 또는 엔터티를 쿼리 하는 동안이 정보입니다.

### <a name="batch-operations"></a>배치 작업
하나의 암호화 정책이 hello 일괄 처리의 tooall 행을 적용합니다. hello 클라이언트 라이브러리 새 임의 IV와 행당 임의 CEK hello 일괄 처리에서 내부적으로 생성 됩니다. 사용자가 선택할 수도 tooencrypt 모든 작업에 대해 서로 다른 속성 hello 일괄 처리의 hello 암호화 해결 프로그램에서이 동작을 정의 하 여 합니다.
컨텍스트 관리자는 hello tableservice batch() 메서드를 통해 일괄 처리를 만든 경우 hello tableservice 암호화 정책에 자동으로 적용 된 toohello 일괄 처리 됩니다. 일괄 처리를를 만드는 경우 명시적으로 hello 생성자를 호출 하 여 hello 암호화 정책 hello 일괄 처리의 hello 수명에 대 한 수정 되지 않은 왼쪽 매개 변수로 전달 되어야 합니다.
Note hello 일괄 처리의 암호화 정책 (엔터티는 hello tableservice 암호화 정책을 사용 하 여 hello 일괄 처리를 커밋할 hello 시 암호화 되지 않습니다)를 사용 하 여 hello 일괄 처리에 삽입 될 때 엔터티 암호화 됩니다.

### <a name="queries"></a>쿼리
tooperform 쿼리 작업 수 tooresolve 있는 키 해결 프로그램을 지정 해야 모든 hello hello 결과 집합의 키입니다. Hello 쿼리 결과에 포함 된 엔터티 해결된 tooa 공급자 일 수 없습니다, hello 클라이언트 라이브러리는 오류를 throw 합니다. 서버 쪽 프로젝션을 수행 하는 모든 쿼리에 대 한 hello 클라이언트 라이브러리 hello 특수 한 암호화 메타 데이터 속성을 추가 합니다 (\_ClientEncryptionMetadata1 및 \_ClientEncryptionMetadata2) toohello 기본적으로 열을 선택 .

> [!IMPORTANT]
> 클라이언트 쪽 암호화를 사용할 때는 이러한 중요점을 유의하세요.
> 
> * 읽기 또는 쓰기 tooan 암호화 경우 blob, 전체 blob 업로드 명령을 사용 하 여 및 범위/전체 blob 다운로드 명령입니다. 블록 배치, 블록 목록 배치, 페이지 쓰기 또는 지우기 페이지; 등의 프로토콜 작업을 사용 하 여 tooan 암호화 된 blob에 쓰기 방지 그렇지 않으면 hello 암호화 blob를 손상 하 고 읽을 수 없도록 수 있습니다.
> * 테이블의 경우에는 유사한 제약 조건이 있습니다. Hello 암호화 메타 데이터를 업데이트 하지 않고 toonot 신중 하 게 암호화 하는 업데이트 속성 이어야 합니다.
> * Hello 암호화 된 blob에서 메타 데이터를 설정 하는 경우 hello 암호화 관련에 필요한 메타 데이터 암호 해독, 가산적가 메타 데이터를 덮어쓸 수 있습니다. 이것은 스냅숏에 대해서 마찬가지입니다. 암호화된 blob의 스냅숏을 생성하는 동안 메타데이터를 지정하지 않도록 하세요. 메타 데이터와 설정 해야 하는 경우 수 있는지 toocall hello **get_blob_metadata** 메서드 첫 번째 tooget hello 현재 암호화 메타 데이터 및 메타 데이터 설정 되어 있는 동안 동시 쓰기를 방지 합니다.
> * Hello를 사용 하도록 설정 **require_encryption** 암호화 된 데이터에만 작동 해야 하는 사용자에 대 한 hello 서비스 개체에 대 한 플래그입니다. 자세한 내용은 다음을 참조하세요.
> 
> 

hello 저장소 클라이언트 라이브러리는 hello 제공 하 고 KEK 키 확인자 인터페이스 뒤 tooimplement hello 필요 합니다. [Azure 주요 자격 증명 모음](https://azure.microsoft.com/services/key-vault/) 지원이 보류 중이며, 완료 시 이 라이브러리에 통합될 예정입니다.

## <a name="client-api--interface"></a>클라이언트 API / 인터페이스
저장소 서비스 개체 (예: blockblobservice)를 만든 후 hello 사용자 수 값을 할당할 암호화 정책을 구성 하는 toohello 필드: key_encryption_key, key_resolver_function, 및 require_encryption 합니다. 사용자는 KEK만, 확인자만 또는 둘 다를 제공할 수 있습니다. key_encryption_key 형식이 hello 기본 키에 대 한 래핑/hello 논리를 제공 하 고 키 식별자를 사용 하 여 식별 되는. key_resolver_function은 hello 암호 해독 프로세스 동안 사용 되는 tooresolve 키입니다. 지정된 키 식별자에 대해 유효한 KEK를 반환합니다. 여러 위치에서 관리 되는 여러 키 간의 사용자 hello 기능 toochoose를 제공 합니다.

hello KEK hello 다음을 구현 해야 메서드 toosuccessfully 데이터를 암호화 합니다.

* wrap_key(cek): 래핑하고 hello hello 사용자가 선택한 알고리즘을 사용 하 여 CEK (바이트)를 지정 합니다. 반환 hello 래핑된 키입니다.
* get_key_wrap_algorithm(): 반환 hello 알고리즘 toowrap 키를 사용 합니다.
* get_kid(): hello 문자열 키 id를 반환이이 KEK에 대 한 합니다.
  hello KEK hello 같은 toosuccessfully decrypt 데이터가 메서드를 구현 해야 합니다.
* (cek, 알고리즘) unwrap_key: 반환 래핑이 해제 hello 형태의 hello hello 문자열이 지정 알고리즘을 사용 하 여 CEK를 지정 합니다.
* get_kid(): 이 KEK에 대한 문자열 키 ID를 반환합니다.

hello 키 해결 프로그램에 반환 하는 메서드, 키 id를 지정 된 hello 해당 KEK 구현 hello 인터페이스 위의 구현 이상 해야 합니다. 만이 방법은 toobe toohello key_resolver_function 속성이 hello 서비스 개체에 할당 합니다.

* 암호화, hello 키가 항상 사용 하 고 키 hello 없을 경우 오류가 발생 합니다.
* 암호를 해독하려면
  
  * hello 키 확인자 tooget hello 키를 지정 하는 경우 호출 됩니다. 가 지정 hello 확인자 hello 키 식별자에 대 한 매핑이 없는 경우 오류가 throw 됩니다.
  * 해결 프로그램 지정 하지 않으면 표시 되지만 키가 지정 하는 경우 해당 식별자에는 필요한 hello 키 식별자와 일치 하는 경우 hello 키는 사용 됩니다. Hello 식별자와 일치 하지 않는 경우 오류가 throw 됩니다.
    
    azure.storage.samples의 암호화 샘플 hello <fix URL>blob, 큐 및 테이블에 대 한 보다 자세한 종단 간 시나리오를 보여 줍니다.
      KEK hello 및 키 해결 프로그램의 예제 구현은 각각 KeyWrapper 및 KeyResolver hello 샘플 파일에서 제공 됩니다.

### <a name="requireencryption-mode"></a>RequireEncryption 모드
사용자는 모든 업로드 및 다운로드를 암호화해야 할 경우 작업 모드를 선택적으로 사용하도록 설정할 수 있습니다. 이 모드에서는 hello 서비스에서 암호화 되지 않은 한 암호화 정책 또는 다운로드 데이터 없이 시도 tooupload 데이터는 클라이언트 hello에 실패 합니다. hello **require_encryption** hello 서비스 개체를 컨트롤에이 동작을 플래그 합니다.

### <a name="blob-service-encryption"></a>Blob 서비스 암호화
Hello blockblobservice 개체에 hello 암호화 정책 필드를 설정 합니다. 다른 모든 항목에서 처리 되는 클라이언트 라이브러리 hello 내부적으로 합니다.

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Set hello KEK and key resolver on hello service object.
my_block_blob_service.key_encryption_key = kek
my_block_blob_service.key_resolver_funcion = key_resolver.resolve_key

# Upload hello encrypted contents toohello blob.
my_block_blob_service.create_blob_from_stream(container_name, blob_name, stream)

# Download and decrypt hello encrypted contents from hello blob.
blob = my_block_blob_service.get_blob_to_bytes(container_name, blob_name)
```

### <a name="queue-service-encryption"></a>큐 서비스 암호화
Hello queueservice 개체에 hello 암호화 정책 필드를 설정 합니다. 다른 모든 항목에서 처리 되는 클라이언트 라이브러리 hello 내부적으로 합니다.

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Set hello KEK and key resolver on hello service object.
my_queue_service.key_encryption_key = kek
my_queue_service.key_resolver_funcion = key_resolver.resolve_key

# Add message
my_queue_service.put_message(queue_name, content)

# Retrieve message
retrieved_message_list = my_queue_service.get_messages(queue_name)
```

### <a name="table-service-encryption"></a>테이블 서비스 암호화
또한 암호화 정책 toocreating 및 요청 옵션에 설정 지정는 **encryption_resolver_function** hello에 **tableservice**, 또는에서 특성을 암호화 하는 집합 hello hello EntityProperty 합니다.

### <a name="using-hello-resolver"></a>Hello 확인자를 사용 하 여

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Define hello encryption resolver_function.
def my_encryption_resolver(pk, rk, property_name):
        if property_name == 'foo':
                return True
        return False

# Set hello KEK and key resolver on hello service object.
my_table_service.key_encryption_key = kek
my_table_service.key_resolver_funcion = key_resolver.resolve_key
my_table_service.encryption_resolver_function = my_encryption_resolver

# Insert Entity
my_table_service.insert_entity(table_name, entity)

# Retrieve Entity
# Note: No need toospecify an encryption resolver for retrieve, but it is harmless tooleave hello property set.
my_table_service.get_entity(table_name, entity['PartitionKey'], entity['RowKey'])
```

### <a name="using-attributes"></a>특성을 사용하여
EntityProperty 개체에 저장 하 여 암호화에 대 한 속성이 표시 될 위에서 설명 했 듯이 하 고 필드 암호화 hello 설정.

```python
encrypted_property_1 = EntityProperty(EdmType.STRING, value, encrypt=True)
```

## <a name="encryption-and-performance"></a>암호화 및 성능
저장소 데이터를 암호화하면 추가 성능 오버헤드가 발생합니다. hello 콘텐츠 키와 IV를 생성 해야, hello 콘텐츠 자체 암호화, 및 추가 메타 데이터를 포맷 하 고 업로드 해야 합니다. 이 오버 헤드는 암호화 되는 데이터의 hello 양에 따라 달라 집니다. 고객은 항상 개발 중에 응용 프로그램 성능을 테스트하는 것이 좋습니다.

## <a name="next-steps"></a>다음 단계
* Hello 다운로드 [Java PyPi 패키지에 대 한 Azure 저장소 클라이언트 라이브러리](https://pypi.python.org/pypi/azure-storage)
* Hello 다운로드 [GitHub에서 Python 소스 코드에 대 한 Azure 저장소 클라이언트 라이브러리](https://github.com/Azure/azure-storage-python)
