---
title: "hello c + + 용 저장소 클라이언트 라이브러리를 사용 하 여 Azure 저장소 리소스 aaaList | Microsoft Docs"
description: "C + + tooenumerate 컨테이너, blob에 대 한 Microsoft Azure 저장소 클라이언트 라이브러리의 Api 목록 toouse hello 대기 하는 방법에 대해 알아봅니다 테이블 및 엔터티."
documentationcenter: .net
services: storage
author: dineshmurthy
manager: jahogg
editor: tysonn
ms.assetid: 33563639-2945-4567-9254-bc4a7e80698f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: dineshm
ms.openlocfilehash: d20a86688938704c24339aa9a1145786783fea5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="list-azure-storage-resources-in-c"></a>C++에서 Azure 저장소 리소스 나열
목록 작업은 Azure 저장소와 키 toomany 개발 시나리오입니다. 이 문서에서는 toomost이 hello 나열 하는 c + + 용 Microsoft Azure 저장소 클라이언트 라이브러리 hello에 제공 된 Api를 사용 하 여 Azure 저장소의 개체가 효율적으로 열거 하는 방법을 설명 합니다.

> [!NOTE]
> C + + 버전에 대 한 hello Azure 저장소 클라이언트 라이브러리를 대상으로이 가이드를 통해 사용할 수 있는 2.x [NuGet](http://www.nuget.org/packages/wastorage) 또는 [GitHub](https://github.com/Azure/azure-storage-cpp)합니다.
> 
> 

hello 저장소 클라이언트 라이브러리는 다양 한 메서드 toolist 또는 Azure 저장소의 쿼리 개체를 제공합니다. 이 문서에서는 다음 시나리오는 hello:

* 계정에서 컨테이너 나열
* 컨테이너 또는 가상 Blob 디렉터리에서 Blob 나열
* 계정에서 큐 나열
* 계정에서 테이블 나열
* 테이블에 엔터티 쿼리

이러한 각 메서드는 다른 시나리오에 대해 다른 오버로드를 사용하여 표시됩니다.

## <a name="asynchronous-versus-synchronous"></a>비동기 및 동기
C + + 용 저장소 클라이언트 라이브러리 hello hello를 기반으로 빌드되므로 [c + + REST 라이브러리](https://github.com/Microsoft/cpprestsdk), 기본적으로 사용 하 여 비동기 작업 지원 [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html)합니다. 예:

```cpp
pplx::task<list_blob_item_segment> list_blobs_segmented_async(continuation_token& token) const;
```

동기 작업 hello 해당 비동기 작업을 래핑합니다.

```cpp
list_blob_item_segment list_blobs_segmented(const continuation_token& token) const
{
    return list_blobs_segmented_async(token).get();
}
```

다중 스레딩 응용 프로그램 또는 서비스와 함께 작업 하는 경우에 스레드 toocall hello 동기화 크게 성능에 영향을 주는 Api를 만드는 대신 직접 hello 비동기 Api를 사용 하는 것이 좋습니다.

## <a name="segmented-listing"></a>분할된 목록
클라우드 저장소의 hello 배율 세그먼트 목록이 필요합니다. 예를 들어, Azure Blob 컨테이너에 수백만 이상의 Blob이 있거나 Azure 테이블에 수십억 이상의 엔터티가 있을 수 있습니다. 이는 이론적인 수치가 아니라 실제 고객 사용 사례입니다.

따라서 단일 응답에 있는 모든 개체는 비현실적 toolist 버전이 있습니다. 대신 페이징을 사용하여 개체를 나열할 수 있습니다. 각 Api를 나열 하는 hello에는 *분할* 오버 로드 합니다.

세그먼트 나열 작업에 대 한 hello 응답에는 다음이 포함 됩니다.

* <i>_segment</i>, hello API를 나열 하는 단일 호출 toohello에 반환 된 결과 집합이 들어 있는입니다.
* *continuation_token*, toohello 다음 호출 순서 tooget hello 결과의 다음 페이지에 전달 되 합니다. 자세한 결과 tooreturn 없는 경우 hello 연속 토큰은 null입니다.

예를 들어 호출 일반적인 toolist 컨테이너의 모든 blob 처럼 보일 수 hello 다음 코드 조각. hello 코드에서 사용할 수는 우리의 [샘플](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):

```cpp
// List blobs in hello blob container
azure::storage::continuation_token token;
do
{
    azure::storage::list_blob_item_segment segment = container.list_blobs_segmented(token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_diretory(it->as_directory());
    }
}

    token = segment.continuation_token();
}
while (!token.empty());
```

Hello 매개 변수에 의해 hello 페이지에 반환 된 결과 수를 제어할 수 있는 참고 *max_results* 예를 들어 각 API의 hello 오버 로드에서:

```cpp
list_blob_item_segment list_blobs_segmented(const utility::string_t& prefix, bool use_flat_blob_listing,
    blob_listing_details::values includes, int max_results, const continuation_token& token,
    const blob_request_options& options, operation_context context)
```

Hello를 지정 하지 않으면 *max_results* 매개 변수, hello 기본 too5000 결과를 최대 값의 단일 페이지에 반환 됩니다.

또한 레코드가 없는 또는 hello의 hello 값 보다 더 적은 레코드 Azure 테이블 저장소에 대 한 쿼리를 반환할 수 있습니다에 유의 *max_results* hello 연속 토큰이 비어 있지 않은 경우에 지정한 매개 변수입니다. 한 가지 이유는 5 초에 해당 hello 쿼리를 완료할 수 없습니다 수 있습니다. Hello 연속 토큰이 비어 있지 않으면으로 hello 쿼리를 계속 진행 하 고 코드 세그먼트 결과의 hello 크기를 가정 하지 않아야 합니다.

hello 대부분의 시나리오에 대 한 패턴을 코딩 조각화 됩니다 나열 하 고, 명시적 진행률을 나열 하거나, 쿼리를 제공 하는 hello 서비스 tooeach 요청 응답 하는 방법을 것이 좋습니다. C + + 응용 프로그램 또는 서비스에 대해 특히 하위 컨트롤의 진행률을 나열 하는 hello 제어 메모리 및 성능 도움이 될 수 있습니다.

## <a name="greedy-listing"></a>Greedy 목록
이전 버전의 hello c + + 용 저장소 클라이언트 라이브러리 (버전 0.5.0 미리 보기 및 이전 버전)에 대해 테이블 및 hello 다음 예제와 같이 큐에서 분할 되지 않은 목록 Api 포함:

```cpp
std::vector<cloud_table> list_tables(const utility::string_t& prefix) const;
std::vector<table_entity> execute_query(const table_query& query) const;
std::vector<cloud_queue> list_queues() const;
```

이러한 메서드는 분할된 API의 래퍼로 구현되었습니다. 분할 된 목록의 각 응답에 대 한 hello 코드 hello 결과 tooa 벡터를 추가 하 고 hello 전체 컨테이너 검사 된 후에 모든 결과 반환 했습니다.

이 방법은 hello 저장소 계정 또는 테이블에는 적은 수의 개체 포함 된 경우에 도움이 될 수 있습니다. 그러나 hello 개체 수 증가 따라, 필요한 hello 메모리 증가할 수를 제한 없이 모든 결과 메모리에 유지 하기 때문에 있습니다. 하나의 나열 작업 호출자 던 진행 상태에 대 한 정보가 있는 hello 하는 동안 시간이 매우 오래 걸릴 수 있습니다.

Greedy 이러한 hello SDK의에서 Api를 나열 또는 하지 않는 C#, Java, JavaScript Node.js 환경 hello 합니다. greedy 이러한 Api를 사용 하 여 tooavoid hello의 잠재적인 문제를 제거 하 0.6.0 버전에서 미리 보기.

사용자의 코드가 이러한 greedy API를 호출하는 경우:

```cpp
std::vector<azure::storage::table_entity> entities = table.execute_query(query);
for (auto it = entities.cbegin(); it != entities.cend(); ++it)
{
    process_entity(*it);
}
```

다음 코드를 수정 해야 toouse hello 분할 Api를 나열 합니다.

```cpp
azure::storage::continuation_token token;
do
{
    azure::storage::table_query_segment segment = table.execute_query_segmented(query, token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
    {
        process_entity(*it);
    }

    token = segment.continuation_token();
} while (!token.empty());
```

Hello를 지정 하 여 *max_results* hello 세그먼트의 매개 변수를 hello 수의 요청 및 메모리 사용량 toomeet 성능 고려 사항에 대 한 응용 프로그램 간에 분산 시킬 수 있습니다.

또한 세그먼트 목록을 Api를 사용 하 여 하지만 "greedy" 스타일의 로컬 컬렉션에 hello 데이터를 저장 하는으로이 신중 하 게 대규모로 로컬 컬렉션에 데이터를 저장 하 여 코드 toohandle 리팩터링.

## <a name="lazy-listing"></a>Lazy 목록
Greedy 목록 잠재적인 문제를 발생 하 고 있지만 hello 컨테이너에 너무 많은 개체가 없는 경우 편리 하 게 됩니다.

또한 C# 또는 Oracle Java Sdk 사용 중인, 경우에 hello 열거 가능한 프로그래밍 모델에서는 지연 스타일 나열, 여기서 hello 데이터가 특정 오프셋에서만 인출 되 필요한 경우 제공 하는 잘 알고 있어야 합니다. C + +, hello 반복기 기반 템플릿을 유사한 방법을 제공합니다.

예를 들어, **list_blobs**를 사용하는 일반적인 lazy 목록 API는 다음과 같습니다.

```cpp
list_blob_item_iterator list_blobs() const;
```

Hello 지연 목록 패턴을 사용 하는 일반적인 코드 조각을 다음과 같이 표시 될 수 있습니다.

```cpp
// List blobs in hello blob container
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_directory(it->as_directory());
    }
}
```

lazy 목록은 동기화 모드에서만 사용할 수 있습니다.

greedy 목록에 비해 lazy 목록은 필요한 경우에만 데이터를 가져옵니다. Hello 내부적 hello 다음 반복기 다음 세그먼트로 이동 하는 경우에 Azure 저장소에서 데이터 인출 합니다. 따라서 메모리 사용량 한계 크기와 제어 하며 hello 작업은 속도가 빠릅니다.

지연 목록 Api는 2.2.0 버전에서 c + +에 대 한 hello 저장소 클라이언트 라이브러리에에서 포함 됩니다.

## <a name="conclusion"></a>결론
이 문서에서는 c + +에 대 한 다양 한 개체 hello 저장소 클라이언트 라이브러리에에서 대 한 Api를 나열 하기 위한 다양 한 오버 로드에 설명 했습니다. toosummarize:

* 여러 스레드 시나리오에서 비동기 API를 사용하는 것이 좋습니다.
* 분할된 목록은 대부분의 시나리오에서 권장됩니다.
* 지연 목록은 동기 시나리오에서 편리 하 게 래퍼로 hello 라이브러리에서 제공 됩니다.
* Greedy 목록에는 권장 되지 않으며 hello 라이브러리에서 제거 되었습니다.

## <a name="next-steps"></a>다음 단계
C + +에 대 한 Azure 저장소 및 클라이언트 라이브러리에 대 한 자세한 내용은 다음 리소스는 hello를 참조 하세요.

* [어떻게 toouse c + +에서 Blob 저장소](storage-c-plus-plus-how-to-use-blobs.md)
* [어떻게 toouse c + +에서 테이블 저장소](storage-c-plus-plus-how-to-use-tables.md)
* [어떻게 toouse c + +에서 큐 저장소](storage-c-plus-plus-how-to-use-queues.md)
* [Azure Storage Client Library for C++ API 설명서](http://azure.github.io/azure-storage-cpp/)
* [Azure 저장소 팀 블로그](http://blogs.msdn.com/b/windowsazurestorage/)
* [Azure 저장소 설명서](https://azure.microsoft.com/documentation/services/storage/)

