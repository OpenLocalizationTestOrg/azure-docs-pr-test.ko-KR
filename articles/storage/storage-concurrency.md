---
title: "Microsoft Azure 저장소에 대 한 동시성 aaaManaging"
description: "방법에 대 한 동시성 toomanage hello Blob, 큐, 테이블 및 파일 서비스"
services: storage
documentationcenter: 
author: jasontang501
manager: tadb
editor: tysonn
ms.assetid: cc6429c4-23ee-46e3-b22d-50dd68bd4680
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/11/2017
ms.author: jasontang501
ms.openlocfilehash: 277fbbb880906da6be67b2267ed5c8e457455bd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-concurrency-in-microsoft-azure-storage"></a>Microsoft Azure 저장소에서 동시성 관리
## <a name="overview"></a>개요
최신 인터넷 기반 응용 프로그램에서는 대개 여러 사용자가 데이터를 동시에 보고 업데이트합니다. 이렇게 하려면 예측 가능한 a tooprovide tootheir 최종 사용자가 경험 하는 방법에 대 한 신중 하 게 응용 프로그램 개발자가 toothink 특히 동일한 여러 사용자가 업데이트할 수 있는 시나리오 hello에 대 한 데이터입니다. 개발자가 일반적으로 고려하는 주요 데이터 동시성 전략에는 다음의 세 가지가 있습니다.  

1. 낙관적 동시성 – 데이터를 읽는 마지막 업데이트는 해당 업데이트의 일부로 확인 hello 응용 프로그램 이후 hello 데이터가 변경 되었는지 여부는 응용 프로그램이 수행 합니다. 예를 들어 두 사용자를 한 wiki 페이지 보기 업데이트 toohello 확인 하는 경우 동일한 페이지 hello wiki 플랫폼 해당 hello 두 번째 업데이트 hello 첫 번째 업데이트 –를 덮어쓰지 않습니다을 확인 해야 하 고 두 사용자가 자신의 업데이트가 성공 했는지 여부를 이해 하는 합니다. 이 전략은 웹 응용 프로그램에서 가장 흔히 사용됩니다.
2. 비관적 동시성 – tooperform 업데이트를 확인 하는 응용 프로그램 다른 사용자 hello 잠금이 해제 될 때까지 hello 데이터를 업데이트 하는 것을 방지 하는 개체를 잠금을 수행 합니다. 예를 들어 마스터/슬레이브 데이터 복제 시나리오만 hello 마스터 업데이트를 수행 하는 hello 마스터에서는 일반적으로 보관 한 단독 잠금을 오랜 시간에 없는 다른 사람이 hello 데이터 tooensure 문자열을 업데이트할 수에 대 한 합니다.
3. 마지막 기록자 우선 – hello 응용 프로그램 먼저 hello 데이터를 읽은 후 다른 응용 프로그램 hello 데이터에 업데이트를 확인 하지 않고 모든 업데이트 작업이 tooproceed를 허용 하 합니다. 이 전략 (또는 정식 전략의 부족)은 여러 사용자가 hello를 액세스 가능성이 없는 인지 하는 방식으로 데이터 분할 되는 위치 사용 일반적으로 동일한 데이터입니다. 일시적인 데이터 스트림을 처리하는 경우에도 이 전략이 유용할 수 있습니다.  

이 문서에서는 hello Azure 저장소 플랫폼 이러한 동시성 전략의 세 가지 모두에 대 한 최고 수준의 지원을 제공 하 여 배포를 간소화 하는 방법의 개요를 제공 합니다.  

## <a name="azure-storage--simplifies-cloud-development"></a>Azure 저장소 - 클라우드 개발 간소화
hello Azure 저장소 서비스는 어떠한 강력한 일관성 모델 디자인 된 tooembrace 되었기 때문에 낙관적 및 비관적 동시성에 대 한 기능 tooprovide 완전히 지원에 고유한 기능은 없지만 모든 세 가지 전략을 지 원하는 안녕 저장소 서비스 커밋 데이터 삽입 또는 업데이트 작업 이후의 모든 액세스 toothat 데이터가 최신 업데이트 hello 표시 됩니다. 최고의 일관성 모델이 사용 하는 저장소 플랫폼에 대 한 쓰기 사용자가 수행 될 때 사이는 간격이 존재 하 고 따라서 순서 tooprevent 불일치가 클라이언트 응용 프로그램을 개발 하므로 복잡해 집니다. 다른 사용자가 데이터를 볼 수 hello 업데이트 될 때 최종 사용자가에 영향을 주는 합니다.  

또한 tooselecting 적절 한 동시성 전략 개발자도 알고 있어야 하는 저장소 플랫폼 변경 내용 – 동일한 트랜잭션에 걸쳐 개체 변경 내용 toohello 특히를 격리 하는 방법입니다. hello Azure 저장소 서비스는 단일 파티션 내에서 쓰기 작업이 동시에 작업 toohappen 읽기 스냅숏 격리 tooallow를 사용 합니다. 다른 격리 수준이 달리 스냅숏 격리를 사용 하면 모든 읽기 확인 hello 데이터의 일관 된 스냅숏을 업데이트가 발생 – 기본적으로 처리 되는 업데이트 트랜잭션 동안 hello 마지막으로 커밋된 값을 반환 하 여는 동안에 합니다.  

## <a name="managing-concurrency-in-blob-storage"></a>Blob 저장소에서 동시성 관리
Toouse 낙관적 또는 비관적 동시성 모델 toomanage 액세스 tooblobs 및 컨테이너에서 hello blob 서비스 중 하나를 선택할 수 있습니다. 전략을 명시적으로 지정 하지 않으면 마지막 wins는 hello 기본 기록 합니다.  

### <a name="optimistic-concurrency-for-blobs-and-containers"></a>Blob 및 컨테이너에 대한 낙관적 동시성
저장소 서비스 hello 식별자 tooevery 저장 된 개체를 할당 합니다. 이 식별자는 개체에 대해 업데이트 작업을 수행할 때마다 업데이트되며, HTTP 프로토콜 내에 정의된 ETag(엔터티 태그) 헤더를 사용하여 HTTP GET 응답의 일부분으로 클라이언트에 반환됩니다. hello 식별자 toohello 클라이언트 hello HTTP 프로토콜 내에 정의 된 hello (엔터티 태그) ETag 헤더를 사용 하 여 HTTP GET 응답의 일부로 반환 됩니다. 특정 조건이 충족 hello 조건이 hello 저장소를 필요로 하는 "If-match" 헤더가 예제의 경우 업데이트가 발생 하는 조건부 헤더를 tooensure 함께 원래 ETag hello를 수행 하는 사용자에 이러한 개체에 대 한 업데이트를 보낼 수 있습니다. 서비스 tooensure hello hello 업데이트 요청에 지정 된 ETag는 hello 저장소 서비스에에서 저장 된 것과 동일한 hello hello의 값입니다.  

이 프로세스의 hello 개요는 다음과 같습니다.  

1. Hello 저장소 서비스에서 blob를 검색, hello 응답 hello hello 저장소 서비스에 hello 개체의 현재 버전을 식별 하는 HTTP ETag 헤더 값을 포함 합니다.
2. Hello blob를 업데이트 하는 경우 hello에 1 단계에서 받은 hello ETag 값이 포함 **If-match** toohello 서비스 보낼 hello 요청의 조건부 헤더입니다.
3. hello 서비스 hello 요청의 hello hello blob의 현재 ETag 값을 가진 hello ETag 값을 비교합니다.
4. Hello hello blob의 현재 ETag 값이 서로 다른 버전 hello에 ETag를 hello 보다 **If-match** hello 서비스 hello 요청에 조건부 헤더가 412 오류 toohello 클라이언트를 반환 합니다. 이 toohello 클라이언트 hello 클라이언트 것으로 검색 한 이후 다른 프로세스 hello blob가 업데이트를 나타냅니다.
5. Hello 현재 ETag hello blob의 값이 동일한 버전으로 hello 경우 ETag hello에 hello **If-match** 조건부 헤더를 요청 hello hello 서비스에서에서 수행 hello 작업 및 업데이트 hello hello blob의 현재 ETag 값 요청 새 버전 만들었음을 tooshow 합니다.  

hello 다음 C# 코드 조각 (클라이언트 저장소 라이브러리 4.2.0 hello를 사용 하 여) 예제를 보여 주는 간단한 방법의 tooconstruct는 **If-match AccessCondition** hello 않은 blob의 hello 속성에서 액세스 하는 ETag 값에 따라 이전에 검색 된 또는 삽입 합니다. Hello 사용 하 여 다음 **AccessCondition** 개체 때 hello blob를 업데이트 하기: hello **AccessCondition** hello를 추가 하는 개체 **If-match** toohello 요청 헤더입니다. 다른 프로세스가 hello blob가 업데이트 면 hello blob 서비스는 HTTP 412 (전제 조건 실패) 상태 메시지를 반환 합니다. 전체 샘플 hello 다운로드할 수 있습니다: [Azure 저장소를 사용 하 여 관리 동시성](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114)합니다.  

```csharp
// Retrieve hello ETag from hello newly created blob
// Etag is already populated as UploadText should cause a PUT Blob call
// toostorage blob service which returns hello etag in response.
string orignalETag = blockBlob.Properties.ETag;

// This code simulates an update by a third party.
string helloText = "Blob updated by a third party.";

// No etag, provided so orignal blob is overwritten (thus generating a new etag)
blockBlob.UploadText(helloText);
Console.WriteLine("Blob updated. Updated ETag = {0}",
blockBlob.Properties.ETag);

// Now try tooupdate hello blob using hello orignal ETag provided when hello blob was created
try
{
    Console.WriteLine("Trying tooupdate blob using orignal etag toogenerate if-match access condition");
    blockBlob.UploadText(helloText,accessCondition:
    AccessCondition.GenerateIfMatchCondition(orignalETag));
}
catch (StorageException ex)
{
    if (ex.RequestInformation.HttpStatusCode == (int)HttpStatusCode.PreconditionFailed)
    {
        Console.WriteLine("Precondition failure as expected. Blob's orignal etag no longer matches");
        // TODO: client can decide on how it wants toohandle hello 3rd party updated content.
    }
    else
        throw;
}  
```

저장소 서비스 hello도 포함 되어 추가 조건부 헤더에 대 한 지원 같은 **If-수정-이후**, **If-수정 되지 않은-이후** 및 **없음-If-match** 으로 이들 조합 합니다. 자세한 내용은 MSDN의 [Blob 서비스 작업의 조건부 헤더 지정](http://msdn.microsoft.com/library/azure/dd179371.aspx) 을 참조하세요.  

hello 다음 표에 요약 되어와 같은 조건부 헤더를 허용 하는 hello 컨테이너 작업 **If-match** 에 해당 하며 hello 요청 hello 응답에 ETag 값을 반환 합니다.  

| 작업 | 컨테이너 ETag 값 반환 | 추가 헤더 수락 |
|:--- |:--- |:--- |
| 컨테이너 만들기 |예 |아니요 |
| 컨테이너 속성 가져오기 |예 |아니요 |
| 컨테이너 메타데이터 가져오기 |예 |아니요 |
| 컨테이너 메타데이터 설정 |예 |예 |
| 컨테이너 ACL 가져오기 |예 |아니요 |
| 컨테이너 ACL 설정 |예 |예(*) |
| 컨테이너 삭제 |아니요 |예 |
| 컨테이너 임대 |예 |예 |
| Blob 나열 |아니요 |아니요 |

(*) hello 권한을 SetContainerACL 정의한 캐시 하 고 업데이트 toothese 사용 권한을 toopropagate는 기간 동안 업데이트 되지 않습니다 보장 toobe 일치 하는 30 초를 수행 합니다.  

hello 다음 표에 요약 되어와 같은 조건부 헤더를 허용 하는 hello blob 작업 **If-match** 에 해당 하며 hello 요청 hello 응답에 ETag 값을 반환 합니다.

| 작업 | ETag 값 반환 | 추가 헤더 수락 |
|:--- |:--- |:--- |
| Blob 배치 |예 |예 |
| Blob 가져오기 |예 |예 |
| Blob 속성 가져오기 |예 |예 |
| Blob 속성 설정 |예 |예 |
| Blob 메타데이터 가져오기 |예 |예 |
| Blob 메타데이터 설정 |예 |예 |
| Blob 임대(*) |예 |예 |
| Blob 스냅숏 |예 |예 |
| Blob 복사 |예 |예(원본 및 대상 Blob의 경우) |
| Blob 복사 중단 |아니요 |아니요 |
| Blob 삭제 |아니요 |예 |
| 블록 배치 |아니요 |아니요 |
| 블록 목록 배치 |예 |예 |
| 블록 목록 가져오기 |예 |아니요 |
| 페이지 가져오기 |예 |예 |
| 페이지 범위 가져오기 |예 |예 |

(*) Blob 임대 된 blob에서 ETag hello를 변경 되지 않습니다.  

### <a name="pessimistic-concurrency-for-blobs"></a>Blob에 대한 비관적 동시성
toolock 독점적인 사용을 위해 blob을 얻을 수 있습니다는 [임대](http://msdn.microsoft.com/library/azure/ee691972.aspx) 에 있습니다. 기간에 대 한 임대를 hello 필요한 지정 임대를 획득 하는 경우:이 수에 대 한 15 too60 초 사이 또는 무한 금액 tooan 배타적 잠금. 한 있습니다 함께 했으면 모든 임대를 해제할 수 유한 임대 tooextend를 갱신할 수 있습니다. hello blob 서비스는 자동으로 만료 될 때 유한 임대를 해제 합니다.  

임대 다른 동기화 전략 toobe 지원 단독 쓰기를 포함 하 여 사용 / 읽기, 전용 쓰기 공유 / 단독 읽기 및 쓰기 공유 / 단독 읽기입니다. 하지만 Hello 저장소 서비스에서 배타적 쓰기 (put, 설정 및 삭제 작업) 한 번에 모든 클라이언트 응용 프로그램 사용 임대 ID와 하나의 해당 클라이언트는 hello 개발자 tooensure 필요 읽기 작업에 대 한 단독으로 사용할 보장 강제로 적용 한 임 대권을 존재 하는 경우 유효한 임대 ID를 가집니다. 임대 ID를 포함하지 않는 읽기 작업에서는 공유 읽기가 수행됩니다.  

hello 다음 C# 조각은의 예가 나와 blob에서 30 초 동안 단독 임대를 획득를 hello blob의 hello 콘텐츠를 업데이트 한 다음 hello 임대를 해제 합니다. 이미 있으면 유효한 임대 hello blob에서 새로운 임대 tooacquire 려 할 때, hello blob 서비스는 "HTTP (409) 충돌" 상태 결과 반환 합니다. 사용 하 여 hello 조각은 **AccessCondition** hello 저장소 서비스에 요청 tooupdate hello blob는 시 tooencapsulate hello 임대 정보 개체입니다.  전체 샘플 hello 다운로드할 수 있습니다: [Azure 저장소를 사용 하 여 관리 동시성](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114)합니다.

```csharp
// Acquire lease for 15 seconds
string lease = blockBlob.AcquireLease(TimeSpan.FromSeconds(15), null);
Console.WriteLine("Blob lease acquired. Lease = {0}", lease);

// Update blob using lease. This operation will succeed
const string helloText = "Blob updated";
var accessCondition = AccessCondition.GenerateLeaseCondition(lease);
blockBlob.UploadText(helloText, accessCondition: accessCondition);
Console.WriteLine("Blob updated using an exclusive lease");

//Simulate third party update tooblob without lease
try
{
    // Below operation will fail as no valid lease provided
    Console.WriteLine("Trying tooupdate blob without valid lease");
    blockBlob.UploadText("Update without lease, will fail");
}
catch (StorageException ex)
{
    if (ex.RequestInformation.HttpStatusCode == (int)HttpStatusCode.PreconditionFailed)
        Console.WriteLine("Precondition failure as expected. Blob's lease does not match");
    else
        throw;
}  
```

Hello 임대 ID를 전달 하지 않고 임대 된 blob에 쓰기 작업을 시도 하면 hello 요청이 412 오류와 함께 실패 합니다. 참고 경우 hello 임대가 만료 hello를 호출 하기 전에 되 **UploadText** 메서드 있지만 여전히 hello 임대 ID,와 hello 요청도 실패 한 **412** 오류입니다. 임대 만료 시간 및 표준 임대 id를 관리 하는 방법에 대 한 자세한 내용은 참조 hello [Blob 임대](http://msdn.microsoft.com/library/azure/ee691972.aspx) REST 설명서입니다.  

hello 다음 blob 작업 צ ְ ײ 임대 toomanage 비관적 동시성:  

* Blob 배치
* Blob 가져오기
* Blob 속성 가져오기
* Blob 속성 설정
* Blob 메타데이터 가져오기
* Blob 메타데이터 설정
* Blob 삭제
* 블록 배치
* 블록 목록 배치
* 블록 목록 가져오기
* 페이지 가져오기
* 페이지 범위 가져오기
* 스냅숏 Blob - 임대가 있는 경우 임대 ID는 선택 사항임
* Blob 복사-임대 ID 필요한 hello 대상 blob에 임대가 있는 경우
* Blob 복사 중단-임대 ID hello 대상 blob에 무한 임대 존재 하는 경우 필수
* Blob 임대  

### <a name="pessimistic-concurrency-for-containers"></a>컨테이너에 대한 비관적 동시성
그러나 컨테이너에서 임대 blob에서와 같은 동기화 전략 toobe 지원 hello를 사용 하도록 설정 (단독 쓰기 / 읽기, 전용 쓰기 공유 / 단독 읽기 및 쓰기 공유 단독 읽기 /) 달리 blob 저장소 서비스 hello만 강제 단독으로 사용할 delete 작업입니다. 활성 임대가 있는 컨테이너 toodelete 클라이언트 hello 삭제 요청에 hello 활성 임대 ID가 포함 되어야 합니다. 다른 모든 컨테이너 작업 하지 않아도 임대 된 컨테이너에서 hello 임대 ID를 포함 하 여 작업을 공유 하는 경우. 업데이트(배치 또는 설정) 또는 읽기 작업에서 독점성이 필요한 경우 개발자는 모든 클라이언트가 임대 ID를 사용하고 한 번에 한 클라이언트만 유효한 임대 ID를 사용하도록 해야 합니다.  

hello 다음 컨테이너 작업 צ ְ ײ 임대 toomanage 비관적 동시성:  

* 컨테이너 삭제
* 컨테이너 속성 가져오기
* 컨테이너 메타데이터 가져오기
* 컨테이너 메타데이터 설정
* 컨테이너 ACL 가져오기
* 컨테이너 ACL 설정
* 컨테이너 임대  

자세한 내용은 다음을 참조하세요.  

* [Blob 서비스 작업의 조건부 헤더 지정](http://msdn.microsoft.com/library/azure/dd179371.aspx)
* [컨테이너 임대](http://msdn.microsoft.com/library/azure/jj159103.aspx)
* [Blob 임대 ](http://msdn.microsoft.com/library/azure/ee691972.aspx)

## <a name="managing-concurrency-in-hello-table-service"></a>Hello 테이블 서비스의에서 동시성을 관리합니다.
hello 테이블 서비스에서는 낙관적 동시성 tooperform 낙관적 동시성 검사를 명시적으로 선택 해야 하는 hello blob 서비스와 달리 엔터티를 사용 하 여 작업할 때 hello 기본 동작으로 검사 합니다. hello 다른 차이점 hello 테이블 및 blob 서비스는 hello blob 서비스의 컨테이너와 blob hello 동시성을 관리할 수 있습니다 하지만 엔터티 hello 동시성 동작만 관리할 수 있습니다.  

toouse 낙관적 동시성 및 toocheck hello 테이블 저장소 서비스에서 검색 한 후 다른 프로세스가 엔터티를 수정 하는 경우에 hello 테이블 서비스 엔터티를 반환 하는 경우 수신 hello ETag 값을 사용할 수 있습니다. 이 프로세스의 hello 개요는 다음과 같습니다.  

1. Hello 테이블 저장소 서비스에서 엔터티를 검색, hello 응답 hello 저장소 서비스에 해당 엔터티와 관련 된 hello 현재 식별자를 식별 하는 ETag 값을 포함 합니다.
2. Hello 엔터티를 업데이트할 때 필수 hello에 1 단계에서 받은 hello ETag 값이 포함 **If-match** toohello 서비스 보낼 hello 요청의 헤더입니다.
3. hello 서비스는 hello 요청의 hello hello 엔터티의 현재 ETag 값을 가진 hello ETag 값을 비교합니다.
4. Hello hello 엔터티의 현재 ETag 값과 다른 필수 hello에 ETag hello 경우 **If-match** hello 서비스 hello 요청에서 헤더 412 오류 toohello 클라이언트를 반환 합니다. 이 다른 프로세스가 hello 클라이언트 것으로 검색 한 이후 hello 엔터티를 업데이트 하는 toohello 클라이언트를 나타냅니다.
5. Hello hello 엔터티의 현재 ETag 값이 필수 hello에 ETag를 hello와 동일 hello는 경우 **If-match** 헤더 hello 요청 또는 hello에 **If-match** 헤더 hello 와일드 카드 문자 (*) hello 서비스 포함 수행 작업 및 업데이트에 업데이트 된 hello 엔터티 tooshow의 현재 ETag 값 hello hello 요청 합니다.  

Hello blob 서비스와 달리 hello 테이블 서비스 해야 hello 클라이언트 tooinclude는 **If-match** 업데이트 요청에 헤더입니다. 그러나 가능한 tooforce는 무조건는 (마지막 기록기 wins 전략)를 업데이트 하 고 hello 클라이언트 hello를 설정 하는 경우 동시성 검사를 무시 **If-match** hello 요청에 헤더 toohello 와일드 카드 문자 (*).  

다음 C# 조각은 hello 이전에 만들어졌거나 업데이트 자신의 전자 메일 주소를 검색 하는 customer 엔터티를 보여 줍니다. hello 초기를 삽입 하거나 hello customer 개체의 작업 저장소 hello ETag 값을 검색할 hello hello를 실행 하는 경우 동일한 개체 인스턴스 바꾸기 작업 hello 샘플에서 사용 하기 때문에, hello ETag 값 백 toohello 테이블 서비스를 자동으로 전송 동시성 위반에 대 한 서비스 toocheck hello를 사용 하도록 설정 합니다. 다른 프로세스가 테이블 저장소의 엔터티에 hello 업데이트 hello 서비스가 HTTP 412 (전제 조건 실패) 상태 메시지를 반환 합니다.  전체 샘플 hello 다운로드할 수 있습니다: [Azure 저장소를 사용 하 여 관리 동시성](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114)합니다.

```csharp
try
{
    customer.Email = "updatedEmail@contoso.org";
    TableOperation replaceCustomer = TableOperation.Replace(customer);
    customerTable.Execute(replaceCustomer);
    Console.WriteLine("Replace operation succeeded.");
}
catch (StorageException ex)
{
    if (ex.RequestInformation.HttpStatusCode == 412)
        Console.WriteLine("Optimistic concurrency violation – entity has changed since it was retrieved.");
    else
        throw;
}  
```

tooexplicitly hello 동시성 검사 사용 안 함, hello 설정할지 **ETag** hello 속성 **직원** 너무 개체 "*" hello 바꾸기 작업을 실행 하기 전에.  

```csharp
customer.ETag = "*";  
```

hello 다음 표에 요약 hello 테이블 엔터티 작업 ETag 값을 사용 하는 방법.

| 작업 | ETag 값 반환 | If-Match 요청 헤더 필요 여부 |
|:--- |:--- |:--- |
| 엔터티 쿼리 |예 |아니요 |
| 엔터티 삽입 |예 |아니요 |
| 엔터티 업데이트 |예 |예 |
| 엔터티 병합 |예 |예 |
| 엔터티 삭제 |아니요 |예 |
| 엔터티 삽입 또는 바꾸기 |예 |아니요 |
| 엔터티 삽입 또는 병합 |예 |아니요 |

해당 hello 참고 **삽입 또는 교체 엔터티** 및 **삽입 또는 병합 엔터티** operations *하지* ETag 값 toohello 보내지 동시성 검사를 수행 합니다. 테이블 서비스입니다.  

일반적으로 테이블을 사용하는 개발자는 확장 가능한 응용 프로그램을 개발할 때 낙관적 동시성을 사용해야 합니다. 비관적 잠금 필요한 한 가지 방법은 개발자 tooassign 각 테이블에 대해 지정 된 blob는 테이블에 액세스할 때 수행할 수 고 hello 테이블을 조작 하기 전에 tootake hello blob에서 임대를 시도 합니다. 이 방법에는 필요 hello 응용 프로그램 tooensure 데이터에 대 한 모든 액세스 경로 hello hello 테이블에서 이전 toooperating 임대를 가져옵니다. hello 최소 임대 시간은 15 초 필요한입니다 확장성을 위해 신중 하 게 고려 점에 유의 해야 합니다.  

자세한 내용은 다음을 참조하세요.  

* [엔터티에 대한 작업](http://msdn.microsoft.com/library/azure/dd179375.aspx)  

## <a name="managing-concurrency-in-hello-queue-service"></a>Hello 큐 서비스의에서 동시성을 관리합니다.
동시성 hello 큐 서비스의 우려가 하는 한 시나리오는 여러 클라이언트가 큐에서 메시지를 검색 됩니다. 를 hello 큐에서 메시지를 검색할 때 hello 응답에는 hello 메시지와 필요한 toodelete hello 메시지 popreceipt 값 포함 됩니다. hello 메시지가 hello 큐에서 자동으로 삭제 되지 않으면 검색 한 후 것만 표시 tooother 클라이언트 hello visibilitytimeout 매개 변수로 지정 된 hello 시간 간격에 대 한 합니다. hello 전에 지정 된 시간 hello hello 응답의 계산 된 hello visibilitytimeout hello 값에 따라 TimeNextVisible 요소 및 처리 된 후 hello 클라이언트 hello 메시지를 검색 하는 예상된 toodelete hello 메시지 매개 변수입니다. visibilitytimeout hello 값 toohello 시간은 hello 메시지 TimeNextVisible toodetermine hello 값 검색을 추가 합니다.  

hello 큐 서비스에 낙관적 또는 비관적 동시성에 대 한 지원 없고이 큐에서 검색 된 메시지를 처리 하는 이유 클라이언트 idempotent 방식으로 메시지를 처리 하기 해야 합니다. SetQueueServiceProperties, SetQueueMetaData, SetQueueACL, UpdateMessage 등의 업데이트 작업에는 마지막 작성자의 업데이트 적용 전략이 사용됩니다.  

자세한 내용은 다음을 참조하세요.  

* [큐 서비스 REST API](http://msdn.microsoft.com/library/azure/dd179363.aspx)
* [메시지 가져오기](http://msdn.microsoft.com/library/azure/dd179474.aspx)  

## <a name="managing-concurrency-in-hello-file-service"></a>Hello 파일 서비스의에서 동시성을 관리합니다.
hello 파일 서비스는 두 개의 다른 프로토콜 끝점-SMB 및 REST를 사용 하 여 액세스할 수 있습니다. hello REST 서비스에 낙관적 잠금 또는 비관적 잠금에 대 한 지원 없고 모든 업데이트는 마지막 기록기 wins 전략을 따를 것입니다. 파일 공유를 탑재 된 SMB 클라이언트 파일 시스템 잠금 메커니즘 toomanage tooshared 파일 액세스 – hello 기능 tooperform 비관적 잠금을 포함 하 여 활용할 수 있습니다. Hello 파일 액세스 및 공유를 모두 지정 SMB 클라이언트는 파일을 열면 모드입니다. "None"의 파일 공유 모드와 함께 "쓰기" 또는 "읽기/쓰기"의 파일 액세스 옵션을 설정 hello 파일을 닫을 때까지 SMB 클라이언트에 의해 잠기지 hello 파일에서 발생 합니다. SMB 클라이언트 hello 파일이 잠겨에 있는 파일에 대해 REST 작업을 시도 하는 경우 hello REST 서비스는 오류 코드 sharingviolation이 표시와 함께 상태 코드 409 (충돌)를 반환 합니다.  

SMB 클라이언트에서 삭제를 위해 파일을 열면 해당 파일에 대해 열린 핸들이 닫힐 때 보류 중인 다른 모든 SMB 클라이언트까지 삭제가 때 hello 파일을 표시 합니다. 파일이 삭제 보류 중으로 표시되어 있는 동안 해당 파일에 대해 REST 작업을 수행하면 상태 코드 409(충돌)와 오류 코드 SMBDeletePending이 반환됩니다. 보류 중인 삭제 플래그 이전 tooclosing hello 파일 hello SMB 클라이언트 tooremove hello에 대 한 수 있기 때문에 상태 코드 404 (찾을 수 없음) 반환 되지 않습니다. 즉, 상태 코드 404 (찾을 수 없음)는 hello 파일 제거 된 경우에 필요 합니다. 파일이 smb 삭제 보류 중 상태가 상태 것 포함 되지 않습니다 hello 파일 목록 결과에서 note 합니다. 또한 hello 파일을 삭제 하는 REST 및 디렉터리를 삭제 하는 REST 작업은 원자성으로 되는데도 나타나지 보류 중 상태를 삭제 합니다.  

자세한 내용은 다음을 참조하세요.  

* [파일 잠금 관리](http://msdn.microsoft.com/library/azure/dn194265.aspx)  

## <a name="summary-and-next-steps"></a>요약 및 다음 단계
hello Microsoft Azure 저장소 서비스 했습니다 설계 hello 가장 복잡 한 온라인 응용 프로그램의 toomeet hello 요구 개발자 toocompromise 또는 재고 주요 디자인 가정 동시성 및 데이터 일관성 등 tootake를 발견 했을 시작 하지 않고 당연 합니다.  

Hello에 대 한이 블로그에서 참조 하는 샘플 응용 프로그램을 완료 합니다.  

* [Azure 저장소를 사용하여 동시성 관리 - 샘플 응용 프로그램](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114)  

Azure 저장소에 대한 자세한 내용은 다음을 참조하세요.  

* [Microsoft Azure 저장소 홈페이지](https://azure.microsoft.com/services/storage/)
* [소개 tooAzure 저장소](storage-introduction.md)
* [Blob](storage-dotnet-how-to-use-blobs.md), [테이블](storage-dotnet-how-to-use-tables.md), [큐](storage-dotnet-how-to-use-queues.md) 및 [파일](storage-dotnet-how-to-use-files.md)에 대한 저장소 시작
* 저장소 아키텍처 – [Azure 저장소: 강력한 일관성과 함께 항상 사용 가능한 클라우드 저장소 서비스](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

