---
title: "Microsoft Azure 저장소에 대 한.net aaaClient 쪽 암호화 | Microsoft Docs"
description: ".NET 용 Azure 저장소 클라이언트 라이브러리 hello Azure 저장소 응용 프로그램에 대 한 보안을 최대화 하기 위해 클라이언트 쪽 암호화 및 Azure 키 자격 증명 모음 통합을 지원합니다."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: becfccca-510a-479e-a798-2044becd9a64
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: e99551925069d5e05bc283039b252cffe8df5383
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="client-side-encryption-and-azure-key-vault-for-microsoft-azure-storage"></a>Microsoft Azure 저장소용 클라이언트 쪽 암호화 및 Azure 키 자격 증명 모음
[!INCLUDE [storage-selector-client-side-encryption-include](../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a>개요
hello [.NET Nuget 패키지용 Azure 저장소 클라이언트 라이브러리](https://www.nuget.org/packages/WindowsAzure.Storage) tooAzure 저장소에 업로드 하 고 toohello 클라이언트를 다운로드 하는 동안 데이터를 해독 하기 전에 클라이언트 응용 프로그램 내에서 데이터를 암호화를 지원 합니다. hello 라이브러리와의 통합에서는 [Azure 키 자격 증명 모음](https://azure.microsoft.com/services/key-vault/) 저장소 계정 키 관리에 대 한 합니다.

클라이언트 쪽 암호화 및 Azure 키 자격 증명 모음을 사용 하 여 blob 암호화 hello 과정을 안내 하는 단계별 자습서를 참조 하십시오. [Azure 키 자격 증명 모음을 사용 하 여 Microsoft Azure 저장소에서 암호화 및 암호 해독 blob](storage-encrypt-decrypt-blobs-key-vault.md)합니다.

Java를 사용하는 클라이언트 쪽 암호화는 [Microsoft Azure 저장소용 Java를 사용하는 클라이언트 쪽 암호화](storage-client-side-encryption-java.md)를 참조하세요.

## <a name="encryption-and-decryption-via-hello-envelope-technique"></a>암호화 및 암호 해독 hello 봉투 (envelope) 기술을 통해
암호화 및 암호 해독의 hello 프로세스 hello 봉투 (envelope) 기법을 따릅니다.

### <a name="encryption-via-hello-envelope-technique"></a>Hello 봉투 (envelope) 기술을 통해 암호화
Hello 봉투 (envelope) 기술을 통해 암호화 hello 방식으로 다음에서 작동 합니다.

1. hello Azure 저장소 클라이언트 라이브러리는 콘텐츠 암호화 키 (CEK)는 한 번 사용 대칭 키를 생성 합니다.
2. 사용자 데이터는 이 CEK를 사용하여 암호화됩니다.
3. hello CEK 다음 래핑된 hello 키 암호화 키 KEK ()를 사용 하 여 (암호화) 합니다. hello KEK 키 식별자로 식별 되 및 수 비대칭 키 쌍 또는 대칭 키 및 수 수 로컬로 관리 하거나 Azure 키 자격 증명 모음에 저장 합니다.
   
    자체 hello 저장소 클라이언트 라이브러리에 대 한 액세스 tooKEK에 없습니다. hello 라이브러리 주요 자격 증명 모음에서 제공 하는 hello 키 래핑 알고리즘을 호출 합니다. 사용자에 대 한 키 래핑/원하는 경우 사용자 지정 공급자 toouse를 선택할 수 있습니다.

4. hello 암호화 된 데이터는 다음 toohello Azure 저장소 서비스에 업로드 합니다. 몇 가지 추가 암호화 메타 데이터와 함께 hello 래핑된 키 (blob)에 메타 데이터로 저장 또는 보간 hello 암호화 된 데이터 (메시지 큐 및 테이블 엔터티)를 사용 합니다.

### <a name="decryption-via-hello-envelope-technique"></a>Hello 봉투 (envelope) 기술을 통해 암호 해독
Hello 봉투 (envelope) 기술을 통해 암호 해독 hello 방식으로 다음에서 작동 합니다.

1. hello 클라이언트 라이브러리는 hello 사용자 관리 하는 hello 키 암호화 키 (KEK) 로컬로 또는 Azure 키 자격 증명 모음에 있다고 가정 합니다. hello 사용자 암호화에 사용 된 tooknow hello 특정 키가 필요 하지 않습니다. 대신, 서로 다른 키 식별자 tookeys 확인 되는 키 확인자 수를 설정 하 고 사용 합니다.
2. hello 클라이언트 라이브러리는 hello 서비스에 저장 된 모든 암호화 자료 함께 hello 암호화 된 데이터를 다운로드 합니다.
3. 키 암호화 키 (KEK) hello 래핑되지 않은 (암호 해독 된)를 사용 하 여 hello 래핑된 콘텐츠 암호화 키 (CEK)가 있습니다. 여기서 다시 hello 클라이언트 라이브러리 않아도 액세스 tooKEK 됩니다. 사용자 지정 hello 또는 키 자격 증명 모음 공급자의 래핑 해제 알고리즘을 호출 하기만 합니다.
4. hello 암호화 키 (CEK)는 다음 콘텐츠 toodecrypt hello 암호화 된 사용자 데이터를 사용 합니다.

## <a name="encryption-mechanism"></a>암호화 메커니즘
hello 저장소 클라이언트 라이브러리를 사용 하 여 [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) 주문 tooencrypt 사용자 데이터에서입니다. 특히, AES를 이용한 [CBC(암호화 블록 체인)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) 모드입니다. 각 서비스는 하는 일이 각각 다르므로 여기서 이것들을 살펴볼 것입니다.

### <a name="blobs"></a>Blob
hello 클라이언트 라이브러리는 현재 전체 blob만 암호화를 지원합니다. 사용자가 hello를 사용할 때 암호화가 지원 특히 **UploadFrom*** 메서드나 hello **OpenWrite** 메서드. 다운로드는 전체 및 범위 다운로드가 모두 지원됩니다.

암호화 하는 동안 hello 클라이언트 라이브러리는 임의의 IV (Initialization Vector) 32 바이트는 임의의 콘텐츠 암호화 키 (CEK)와 함께 16 바이트의 생성 되며이 정보를 사용 하 여 hello blob 데이터의 봉투 (envelope) 암호화를 수행 합니다. hello CEK 되 고 몇 가지 추가 암호화 메타 데이터 함께 hello hello 서비스에 암호화 된 blob 메타 데이터를 blob으로 저장 됩니다.

> [!WARNING]
> 편집 하거나 hello blob에 대 한 사용자 고유의 메타 데이터를 업로드 하는 경우 tooensure이 메타이 데이터는 유지 해야 합니다. 이 메타 데이터 없이 새 메타 데이터를 업로드 하는 경우 hello 래핑된 CEK, IV 및 기타 메타 데이터 손실 되 고 hello blob 콘텐츠를 절대로 다시 검색할 수 없는 합니다.
> 
> 

Hello를 사용 하 여 hello 전체 blob의 hello 콘텐츠를 검색에서는 암호화 된 blob 다운로드 **DownloadTo***/**BlobReadStream** 편의 메서드를 합니다. 래핑된 CEK 래핑이 해제 하 고 hello IV와 함께 사용 하는 hello (으로 저장 blob 메타 데이터가 예제의) tooreturn hello 암호 해독 데이터 toohello 사용자.

임의의 범위를 다운로드 (**DownloadRange*** 메서드) hello에서 암호화 된 blob의 순서 tooget 사용자가 적은 양의 toosuccessfully 사용된 될 수 있는 추가 데이터의 암호를 해독 hello 제공 hello 범위를 조정 하려면 요청 된 범위입니다.

이 스키마를 사용하여 모든 blob 유형(블록 blob, 페이지 blob 및 추가 blob)을 암호화/암호 해독할 수 있습니다.

### <a name="queues"></a>큐
큐 메시지의 모든 형식이 될 수, 있으므로 hello 클라이언트 라이브러리 hello 메시지 텍스트에 IV (Initialization Vector) hello 및 hello 암호화 된 콘텐츠 암호화 키 (CEK) 포함 된 사용자 지정 형식을 정의 합니다.

암호화 하는 동안 hello 클라이언트 라이브러리는 32 바이트의 임의 CEK 함께 16 바이트의 임의 IV를 생성 하 고이 정보를 사용 하 여 hello 큐 메시지 텍스트의 봉투 (envelope) 암호화를 수행 합니다. hello CEK 되 고 몇 가지 추가 암호화 메타 데이터 toohello 암호화 된 큐 메시지 추가 됩니다. (아래 참조)이 수정 된 메시지는 hello 서비스에 저장 됩니다.

    <MessageText>{"EncryptedMessageContents":"6kOu8Rq1C3+M1QO4alKLmWthWXSmHV3mEfxBAgP9QGTU++MKn2uPq3t2UjF1DO6w","EncryptionData":{…}}</MessageText>

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
3. hello CEK 되 고 그런 다음 몇 가지 추가 암호화 메타 데이터는 두 개의 추가 예약 된 속성으로 저장 합니다. hello 첫 번째 예약 된 속성 (_ClientEncryptionMetadata1)은 4, 버전 및 래핑된 키에 대 한 hello 정보를 포함 하는 문자열 속성입니다. hello 두 번째 예약 된 속성 (_ClientEncryptionMetadata2)은 암호화 된 hello 속성에 대 한 hello 정보를 보유 하는 이진 속성. 이 두 번째 속성 (_ClientEncryptionMetadata2)의 hello 정보 암호화 됩니다.
4. Toothese 추가 예약 된 속성 암호화에 필요, 인해 이제가 있습니다 252 대신 사용자 지정 속성을 250만. hello hello 엔터티의 전체 크기는 1MB 미만 이어야 합니다.

문자열 속성만 암호화 할 수 있다는 것을 참고하세요. 다른 유형의 속성 암호화 toobe 인 경우 변환 된 toostrings 되어야 합니다. 이진 속성으로 암호화 하는 hello 문자열 hello 서비스에 저장 됩니다 및 암호 해독 한 후 뒤로 toostrings 변환 됩니다.

테이블의 경우 또한 toohello 암호화 정책 사용자 지정 해야 hello 속성 toobe 암호화 합니다. 이것은 특성(TableEntity에서 파생 되는 POCO 엔터티)을 지정[EncryptProperty]하거나 암호화 해결 프로그램 요청 옵션에서 수행할 수 있습니다.  암호화 해결 프로그램은 파티션 키, 행 키, 그리고 속성 이름 및 암호화 여부 속성을 나타내는  Bool방식을 반환하는 대표자입니다. 암호화 하는 동안 toohello 통신에 쓰는 동안 속성을 암호화 해야 하는지 여부를 hello 클라이언트 라이브러리 정보 toodecide이를 사용 합니다. 또한 hello 대리자 hello 가능성은 속성이 암호화 주위 논리를 제공 합니다. (예를 들어 X의 경우, A 속성을 암호화하고 그렇지 않은 경우 A와 B 속성을 암호화) 한다는 확인은 필요 하지 않은 tooprovide 읽기 또는 엔터티를 쿼리 하는 동안이 정보입니다.

### <a name="batch-operations"></a>배치 작업
일괄 처리 작업에서 hello 동일한 KEK 여러 사용 될 해당 일괄 처리 작업의 모든 hello 행 hello 클라이언트 라이브러리는 하나의 옵션 개체 (및 따라서 하나의 정책/KEK)에 허용 하기 때문에 일괄 처리 작업 단위입니다. 그러나 hello 클라이언트 라이브러리는 hello 일괄 처리에서 새로운 임의 IV 및 행당 임의 CEK를 생성 내부적으로 합니다. 사용자가 선택할 수도 tooencrypt 모든 작업에 대해 서로 다른 속성 hello 일괄 처리의 hello 암호화 해결 프로그램에서이 동작을 정의 하 여 합니다.

### <a name="queries"></a>쿼리
tooperform 쿼리 작업 수 tooresolve 있는 키 해결 프로그램을 지정 해야 모든 hello hello 결과 집합의 키입니다. Hello 쿼리 결과에 포함 된 엔터티 해결된 tooa 공급자 일 수 없습니다, hello 클라이언트 라이브러리는 오류를 throw 합니다. 서버 쪽 프로젝션을 수행 하는 모든 쿼리에 대 한 hello 클라이언트 라이브러리는 기본 선택 toohello 열으로 hello 특수 한 암호화 메타 데이터 속성 (_ClientEncryptionMetadata1 및 _ClientEncryptionMetadata2)을 추가 합니다.

## <a name="azure-key-vault"></a>Azure 키 자격 증명 모음
Azure 키 자격 증명 모음은 클라우드 응용 프로그램 및 서비스에서 사용되는 암호화 키 및 비밀을 보호하는데 도움이 됩니다. Azure 키 자격 증명 모음을 사용하여, 사용자는 키와 비밀(예: 인증 키, 저장소 계정 키, 데이터 암호화 키, PFX 파일 및 암호)을 암호화하여 하드웨어 보안 모듈(HSM)로 보호된 키를 사용합니다. 자세한 내용은 [Azure 주요 자격 증명 모음이란?](../key-vault/key-vault-whatis.md)을 참조하세요.

hello 저장소 클라이언트 라이브러리는 키를 관리 하기 위한 Azure 전체에서 순서 tooprovide 공통 프레임 워크에에서 hello 주요 자격 증명 모음 핵심 라이브러리를 사용 합니다. 사용자가 가져올 hello 주요 자격 증명 모음 확장 라이브러리를 사용 하 여 hello 장점이 있습니다. hello 확장 프로그램 라이브러리 캐싱 및 집계와 뿐만 아니라 간단 하 고 원활한 대칭/RSA 로컬 및 클라우드 키 공급자의 유용한 기능을 제공합니다.

### <a name="interface-and-dependencies"></a>인터페이스 및 종속성
세 가지 키 자격증명 모음 패키지가 있습니다.

* Microsoft.Azure.KeyVault.Core는 IKey hello 및 IKeyResolver 포함 되어 있습니다. 어떤 부속품도 없는 작은 패키지입니다. .NET 용 저장소 클라이언트 라이브러리 hello 종속성으로 정의 합니다.
* Microsoft.Azure.KeyVault은 hello 키 자격 증명 모음 REST 클라이언트를 포함합니다.
* Microsoft.Azure.KeyVault.Extensions 은 암호화 알고리즘 및 RSAKey와  SymmetricKey의 구현이 포함 된 확장 프로그램 코드를 포함합니다. Hello 코어 및 KeyVault 네임 스페이스에 따라 달라 집니다 하 고 집계 해결 프로그램 (사용자가 여러 키 공급자 toouse를 원하는) 하는 경우 및 캐싱 키 확인자 toodefine 기능을 제공 합니다. Hello 저장소 클라이언트 라이브러리에 종속 되지 않지만 직접이 패키지에 사용자가 원하는 toouse Azure 키 자격 증명 모음 toostore가 키 또는 toouse hello 주요 자격 증명 모음 확장 tooconsume hello 로컬 및 클라우드 암호화 공급자 경우,이 패키지를 해야 합니다.

키 자격증명모음은 고급 가치 마스터키로 고안되었으며 키 자격증명 모음당 스로틀 한계는 이것을 염두에 두고 만들어졌습니다. 주요 자격 증명 모음을 사용 하 여 클라이언트 쪽 암호화를 수행할 때는 hello 기본 모델 toouse 대칭 마스터 키는 암호로 키 자격 증명 모음에 저장 하 고 로컬로 캐시은입니다. 사용자가 수행 해야 hello 다음:

1. 암호를 오프 라인으로 만들고 tooKey 자격 증명 모음을 업로드 합니다.
2. Hello 암호의 기본 식별자를 사용 하 여 매개 변수 tooresolve hello 현재 버전의 hello 암호를 암호화 하 고이 정보를 로컬로 캐시 합니다. CachingKeyResolver; 캐싱에 사용 사용자는 예상된 되지 tooimplement 자체 캐싱 논리입니다.
3. 입력으로 hello 암호화 정책을 만드는 동안 hello 캐싱 확인자를 사용 합니다.

주요 자격 증명 모음 사용과 관련 된 자세한 내용은 hello에 있습니다 [암호화 코드 샘플](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples)합니다.

## <a name="best-practices"></a>모범 사례
.NET 용 저장소 클라이언트 라이브러리 hello에만 암호화 지원이 제공 됩니다. Windows Phone 및 Windows 런타임은 현재 암호화를 지원하지 않습니다.

> [!IMPORTANT]
> 클라이언트 쪽 암호화를 사용할 때는 이러한 중요점을 유의하세요.
> 
> * 읽기 또는 쓰기 tooan 암호화 경우 blob, 전체 blob 업로드 명령을 사용 하 여 및 범위/전체 blob 다운로드 명령입니다. 블록 배치, 블록 목록 배치, 페이지 쓰기, 일반 페이지 또는 블록 추가; 등의 프로토콜 작업을 사용 하 여 tooan 암호화 된 blob에 쓰기 방지 그렇지 않으면 hello 암호화 blob를 손상 하 고 읽을 수 없도록 수 있습니다.
> * 테이블의 경우에는 유사한 제약 조건이 있습니다. Hello 암호화 메타 데이터를 업데이트 하지 않고 toonot 신중 하 게 암호화 하는 업데이트 속성 이어야 합니다.
> * Hello 암호화 된 blob에서 메타 데이터를 설정 하는 경우 hello 암호화 관련에 필요한 메타 데이터 암호 해독, 가산적가 메타 데이터를 덮어쓸 수 있습니다. 이것은 스냅숏에 대해서 마찬가지입니다. 암호화된 blob의 스냅숏을 생성하는 동안 메타데이터를 지정하지 않도록 하세요. 메타 데이터와 설정 해야 하는 경우 수 있는지 toocall hello **FetchAttributes** 메서드 첫 번째 tooget hello 현재 암호화 메타 데이터 및 메타 데이터 설정 되어 있는 동안 동시 쓰기를 방지 합니다.
> * Hello를 사용 하도록 설정 **RequireEncryption** hello 기본 요청 옵션에만 작동 해야 하는 사용자가을 속성 데이터를 암호화 합니다. 자세한 내용은 다음을 참조하세요.
> 
> 

## <a name="client-api--interface"></a>클라이언트 API / 인터페이스
EncryptionPolicy 개체를 만드는 동안 사용자만 키를 공급 (IKey 구현), 확인자만 키를 공급 (IKeyResolver 구현) 또는 둘 모두 키를 공급. IKey 형식이 hello 기본 키에 대 한 래핑/hello 논리를 제공 하 고 키 식별자를 사용 하 여 식별 되는. IKeyResolver는 hello 암호 해독 프로세스 동안 사용 되는 tooresolve 키입니다. 키 식별자가 제공하는 IKey를 반환하는 ResolveKey 메서드를 정의 합니다. 여러 위치에서 관리 되는 여러 키 간의 사용자 hello 기능 toochoose를 제공 합니다.

* 암호화, hello 키가 항상 사용 하 고 키 hello 없을 경우 오류가 발생 합니다.
* 암호를 해독하려면
  * hello 키 확인자 tooget hello 키를 지정 하는 경우 호출 됩니다. 가 지정 hello 확인자 hello 키 식별자에 대 한 매핑이 없는 경우 오류가 throw 됩니다.
  * 해결 프로그램 지정 하지 않으면 표시 되지만 키가 지정 하는 경우 해당 식별자에는 필요한 hello 키 식별자와 일치 하는 경우 hello 키는 사용 됩니다. Hello 식별자와 일치 하지 않는 경우 오류가 throw 됩니다.

hello [암호화 샘플](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples) 주요 자격 증명 모음 통합 blob, 큐 및 테이블에 대 한 보다 자세한 종단 간 시나리오를 함께 보여 줍니다.

### <a name="requireencryption-mode"></a>RequireEncryption 모드
사용자는 모든 업로드 및 다운로드를 암호화해야 할 경우 작업 모드를 선택적으로 사용하도록 설정할 수 있습니다. 이 모드에서는 hello 서비스에서 암호화 되지 않은 한 암호화 정책 또는 다운로드 데이터 없이 시도 tooupload 데이터는 클라이언트 hello에 실패 합니다. hello **RequireEncryption** hello 요청 옵션 개체의 속성을이 동작을 제어 합니다. 응용 프로그램은 Azure 저장소에 저장 된 모든 개체를 암호화 하는 경우 hello를 설정할 수 있습니다 **RequireEncryption** hello 서비스 클라이언트 개체에 대 한 hello 기본 요청 옵션에는 속성입니다. 예를 들어 설정 **CloudBlobClient.DefaultRequestOptions.RequireEncryption** 너무**true** toorequire 암호화 모든 blob 작업에 대해 해당 클라이언트 개체를 통해 수행 합니다.

### <a name="blob-service-encryption"></a>Blob 서비스 암호화
만들기는 **BlobEncryptionPolicy** hello 요청 옵션에 설정 및 개체 (또는 API를 사용 하 여 클라이언트 수준에서 **DefaultRequestOptions**). 다른 모든 항목에서 처리 되는 클라이언트 라이브러리 hello 내부적으로 합니다.

```csharp
// Create hello IKey used for encryption.
 RsaKey key = new RsaKey("private:key1" /* key identifier */);

 // Create hello encryption policy toobe used for upload and download.
 BlobEncryptionPolicy policy = new BlobEncryptionPolicy(key, null);

 // Set hello encryption policy on hello request options.
 BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

 // Upload hello encrypted contents toohello blob.
 blob.UploadFromStream(stream, size, null, options, null);

 // Download and decrypt hello encrypted contents from hello blob.
 MemoryStream outputStream = new MemoryStream();
 blob.DownloadToStream(outputStream, null, options, null);
```

### <a name="queue-service-encryption"></a>큐 서비스 암호화
만들기는 **QueueEncryptionPolicy** hello 요청 옵션에 설정 및 개체 (또는 API를 사용 하 여 클라이언트 수준에서 **DefaultRequestOptions**). 다른 모든 항목에서 처리 되는 클라이언트 라이브러리 hello 내부적으로 합니다.

```csharp
// Create hello IKey used for encryption.
 RsaKey key = new RsaKey("private:key1" /* key identifier */);

 // Create hello encryption policy toobe used for upload and download.
 QueueEncryptionPolicy policy = new QueueEncryptionPolicy(key, null);

 // Add message
 QueueRequestOptions options = new QueueRequestOptions() { EncryptionPolicy = policy };
 queue.AddMessage(message, null, null, options, null);

 // Retrieve message
 CloudQueueMessage retrMessage = queue.GetMessage(null, options, null);
```

### <a name="table-service-encryption"></a>테이블 서비스 암호화
또한 암호화 정책 toocreating 및 요청 옵션에 설정 지정는 **EncryptionResolver** 에 **TableRequestOptions**, 또는에 hello [EncryptProperty] 특성 집합 hello 엔터티입니다.

#### <a name="using-hello-resolver"></a>Hello 확인자를 사용 하 여

```csharp
// Create hello IKey used for encryption.
 RsaKey key = new RsaKey("private:key1" /* key identifier */);

 // Create hello encryption policy toobe used for upload and download.
 TableEncryptionPolicy policy = new TableEncryptionPolicy(key, null);

 TableRequestOptions options = new TableRequestOptions()
 {
    EncryptionResolver = (pk, rk, propName) =>
     {
        if (propName == "foo")
         {
            return true;
         }
         return false;
     },
     EncryptionPolicy = policy
 };

 // Insert Entity
 currentTable.Execute(TableOperation.Insert(ent), options, null);

 // Retrieve Entity
 // No need toospecify an encryption resolver for retrieve
 TableRequestOptions retrieveOptions = new TableRequestOptions()
 {
    EncryptionPolicy = policy
 };

 TableOperation operation = TableOperation.Retrieve(ent.PartitionKey, ent.RowKey);
 TableResult result = currentTable.Execute(operation, retrieveOptions, null);
```

#### <a name="using-attributes"></a>특성을 사용하여
Hello 엔터티 TableEntity 구현 하는 경우, 위에서 설명한 대로 다음 hello 속성 수 특성으로 데코레이팅 할 hello [EncryptProperty] hello를 지정 하는 대신 **EncryptionResolver**합니다.

```csharp
[EncryptProperty]
 public string EncryptedProperty1 { get; set; }
```

## <a name="encryption-and-performance"></a>암호화 및 성능
저장소 데이터를 암호화하면 추가 성능 오버헤드가 발생합니다. hello 콘텐츠 키와 IV를 생성 해야, hello 콘텐츠 자체 암호화, 및 추가 메타 데이터를 포맷 하 고 업로드 해야 합니다. 이 오버 헤드는 암호화 되는 데이터의 hello 양에 따라 달라 집니다. 고객은 항상 개발 중에 응용 프로그램 성능을 테스트하는 것이 좋습니다.

## <a name="next-steps"></a>다음 단계
* [자습서: Microsoft Azure 저장소에서 Azure 키 자격 증명 모음을 사용하여 Blob 암호화 및 해독](storage-encrypt-decrypt-blobs-key-vault.md)
* Hello 다운로드 [.NET NuGet 패키지용 Azure 저장소 클라이언트 라이브러리](https://www.nuget.org/packages/WindowsAzure.Storage)
* Azure 키 자격 증명 모음 NuGet hello 다운로드 [코어](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Core/), [클라이언트](http://www.nuget.org/packages/Microsoft.Azure.KeyVault/), 및 [확장](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Extensions/) 패키지  
* Hello 방문 [Azure 키 자격 증명 모음 설명서](../key-vault/key-vault-whatis.md)
