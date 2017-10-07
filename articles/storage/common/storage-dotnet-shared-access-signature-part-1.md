---
title: "aaaUsing 공유 액세스 서명 (SAS) Azure 저장소에 | Microsoft Docs"
description: "Toouse 공유 액세스 서명 (SAS) toodelegate tooAzure 저장소 리소스에 액세스, blob, 큐, 테이블, 파일 등을 알아봅니다."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 46fd99d7-36b3-4283-81e3-f214b29f1152
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/18/2017
ms.author: marsma
ms.openlocfilehash: 5b75a3c25bcfb9f1ceb81f31dc2d42376bd105cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-shared-access-signatures-sas"></a>SAS(공유 액세스 서명) 사용

공유 액세스 서명 (SAS) 사용 하면 저장소 계정의 방법 toogrant 제한 된 액세스 tooobjects tooother 클라이언트 계정 키를 노출 하지 않고 있습니다. 이 문서에서는 hello SAS 모델의 개요를 제공, SAS 모범 사례를 검토 하 고 몇 가지 예를 살펴봅니다.

SAS를 사용 하 여 여기에 제시 된 것 이상의 추가 코드 예제를 보려면 [.NET에서 Azure Blob 저장소 시작](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/) 및 hello에서 사용할 수 있는 다른 샘플 [Azure 코드 예제](https://azure.microsoft.com/documentation/samples/?service=storage) 라이브러리입니다. Hello 예제 응용 프로그램을 다운로드 하 고 실행 하거나 GitHub에서 hello 코드를 찾아보려면 수 있습니다.

## <a name="what-is-a-shared-access-signature"></a>공유 액세스 서명이란?
공유 액세스 서명은 저장소 계정에 위임 된 액세스 tooresources를 제공합니다. SAS를 클라이언트에 계정 키를 공유 하지 않고 저장소 계정의 tooresources 액세스할을 부여할 수 있습니다. 이 hello 중요 한 점은 응용 프로그램-SAS에서에서 공유 액세스 서명을 사용 하 여 안전 하 게 tooshare 계정 키를 손상 시 키 지 않고 저장소 리소스는 합니다.

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

SAS를 세밀 하 게 hello 유형의 tooclients SAS를 포함 하 여 hello 있는 권한을 부여 하는 액세스 제어를 제공 합니다.

* SAS는 hello를 통해 유효한 hello 시작 시간 및 hello 만료 시간을 포함 하는 hello 간격입니다.
* hello hello SAS 부여 된 사용 권한입니다. 예를 들어 blob에 대 한 SAS 수 읽기 권한을 부여 및 권한 toothat blob 쓰지만 삭제 권한은 부여 하지 합니다.
* 선택적 IP 주소 또는 IP 주소 범위에서 Azure 저장소를 수락할 SAS hello 합니다. 예를 들어 tooyour 조직에 속한 IP 주소를 지정할 수 있습니다.
* Azure 저장소는 hello SAS을 수락 하는 데는 hello 프로토콜입니다. HTTPS를 사용 하 여이 선택적 매개 변수 toorestrict 액세스 tooclients를 사용할 수 있습니다.

## <a name="when-should-you-use-a-shared-access-signature"></a>공유 액세스 서명은 언제 사용하나요?
저장소 계정의 액세스 키를 소유 하지 저장소 계정 tooany 클라이언트에서 tooprovide 액세스 tooresources 하려는 경우 SAS를 사용할 수 있습니다. 저장소 계정에는 tooyour 계정 관리 액세스를 부여 하는 기본 및 보조 액세스 키와 그 안에 있는 모든 리소스를 모두 포함 되어 있습니다. 이러한 키를 노출 악성 또는 부주의로 사용 하 여 사용자 계정 toohello 가능성이 열립니다. 공유 액세스 서명을 toohello 권한을 명시적으로 부여 하지에 따라 저장소 계정에 및 계정 키에 대 한 필요 없이 tooread, 쓰기 및 삭제 데이터 클라이언트를 허용 하는 안전한 좋은 제공 합니다.

SAS를 유용 하는 일반적인 시나리오는 서비스 사용자가 읽고 쓰는 자신의 데이터 tooyour 저장소 계정입니다. 저장소 계정에 사용자 데이터를 저장하는 시나리오에는 다음과 같은 두 가지 일반적인 디자인 패턴이 있습니다.

1. 클라이언트는 인증을 수행하는 프런트 엔드 프록시 서비스를 통해 데이터를 업로드하고 다운로드합니다. 이 프런트 엔드 프록시 서비스에 비즈니스 규칙 유효성 검사 수 hello 이점이 있지만 데이터 또는 대규모 트랜잭션을, 많은 양의 대 한 toomatch 수요를 확장할 수 있는 서비스를 만드는 수도 비용이 많이 드는 하거나 어려운 합니다.

  ![시나리오 다이어그램: 프런트 엔드 프록시 서비스](./media/storage-dotnet-shared-access-signature-part-1/sas-storage-fe-proxy-service.png)   

1. 필요에 따라 hello 클라이언트를 인증 하 고 SAS를 생성 하는 간단한 서비스입니다. Hello 클라이언트 hello SAS를 받을 저장소 계정 리소스에 의해 정의 hello SAS hello SAS에서 허용 하는 hello 간격에 대 한 hello 권한으로 직접 액세스할 수 있습니다. hello SAS 완화 hello 프런트 엔드 모드 해제 프록시 서비스를 통해 모든 데이터를 라우팅에 대 한 hello 필요 합니다.

  ![시나리오 다이어그램: SAS 공급자 서비스](./media/storage-dotnet-shared-access-signature-part-1/sas-storage-provider-service.png)   

대부분의 실제 서비스에서는 이러한 두 가지 방법을 혼합하여 사용할 수 있습니다. 예를 들어 일부 데이터 처리 및 hello 프런트 엔드 프록시를 통해 다른 데이터 저장 하거나 SAS를 사용 하 여 직접 읽는 동안 유효성을 검사할 수 있습니다.

또한 toouse SAS tooauthenticate hello 원본 개체를 특정 시나리오에서 복사 작업에 필요 합니다.

* 다른 저장소 계정에 있는 blob tooanother blob을 복사할 때 SAS tooauthenticate hello 원본 blob를 사용 해야 합니다. 필요에 따라 SAS tooauthenticate hello 대상 blob도 사용할 수 있습니다.
* 다른 저장소 계정에 있는 파일 tooanother 파일을 복사할 때 SAS tooauthenticate hello 소스 파일을 사용 해야 합니다. 필요에 따라 SAS tooauthenticate hello 대상 파일 에서도 사용할 수 있습니다.
* Hello 원본 및 대상 개체 내에 있는 hello 동일한 경우에 SAS tooauthenticate hello 원본 개체를 사용 해야 blob tooa 파일 또는 파일 tooa blob을 복사할 때 저장소 계정입니다.

## <a name="types-of-shared-access-signatures"></a>공유 액세스 서명의 유형
두 가지 유형의 공유 액세스 서명을 만들 수 있습니다.

* **서비스 SAS** hello 서비스 SAS 대리자 tooa 리소스 hello 저장소 서비스 중 하나에 액세스: Blob, 큐, 테이블 또는 파일 서비스 hello 합니다. 참조 [서비스 SAS를 생성할](https://msdn.microsoft.com/library/dn140255.aspx) 및 [서비스의 SAS 예](https://msdn.microsoft.com/library/dn140256.aspx) hello 서비스 SAS 토큰을 생성 하는 방법에 대 한 자세한 정보에 대 한 합니다.
* **계정 SAS** hello 계정 SAS 대리인 tooresources 하나 이상의 hello 저장소 서비스에 액세스합니다. 모든 서비스 SAS 통해 사용할 수 있는 hello 작업 계정 SAS 통해 사용할 수 있습니다. 또한 hello 계정 SAS에 위임할 수 있습니다 tooa와 같은 특정 서비스, 적용 되는 액세스 toooperations **Get/Set 서비스 속성** 및 **서비스 통계 가져오기**합니다. 또한 액세스 tooread, 쓰기 및 삭제 작업을 blob 컨테이너, 테이블, 큐 및 서비스 SAS와 함께 사용할 수 없는 파일 공유를 위임할 수 있습니다. 참조 [계정 SAS를 생성할](https://msdn.microsoft.com/library/mt584140.aspx) hello 계정 SAS 토큰을 생성 하는 방법에 대 한 자세한 정보에 대 한 합니다.

## <a name="how-a-shared-access-signature-works"></a>공유 액세스 서명 사용 방법
공유 액세스 서명을 tooone 또는 더 많은 저장소 리소스를 가리키는 쿼리 매개 변수는 특별 한 집합을 포함 하는 토큰을 포함 하는 부호 있는 URI입니다. hello 토큰 hello 리소스 hello 클라이언트에서 액세스할 수 있습니다 어떻게 나타냅니다. Hello 쿼리 매개 변수 중 하나 서명 hello hello SAS 매개 변수에서 생성 되며 hello 계정 키로 서명 합니다. Azure 저장소 tooauthenticate hello SAS이이 서명을 사용 됩니다.

SAS URI, 표시 된 hello 리소스 URI 및 hello SAS 토큰의 예는 다음과 같습니다.

![SAS URI의 구성 요소](./media/storage-dotnet-shared-access-signature-part-1/sas-storage-uri.png)   

hello SAS 토큰은 hello를 생성 하는 문자열 *클라이언트* 측면 (hello 참조 [SAS 예제](#sas-examples) 코드 예제에 대 한 섹션). Hello 저장소 클라이언트 라이브러리를 생성 하는 SAS 토큰 예를 들어에서 추적 되지 않은 Azure 저장소에서 어떤 방식으로 합니다. SAS 토큰 개수에 제한 없이 hello 클라이언트 쪽에서 만들 수 있습니다.

요청의 일부로 SAS URI tooAzure 저장소를 제공 하는 클라이언트 hello 서비스가 hello SAS 매개 변수 및 서명 tooverify hello 요청 인증에 대 한 유효한 지 확인 합니다. Hello 서비스는 hello 서명이 유효한 확인, hello 요청이 인증 됩니다. 그렇지 않은 경우 오류 코드 403 (금지 됨)와 함께 hello 요청이 거부 됩니다.

## <a name="shared-access-signature-parameters"></a>공유 액세스 서명 매개 변수
hello 계정 SAS 및 서비스 SAS 토큰 일부 공통 매개 변수를 포함 하 고 있는 다른 몇 가지 매개 변수를 사용할 수도 합니다.

### <a name="parameters-common-tooaccount-sas-and-service-sas-tokens"></a>매개 변수 일반적인 tooaccount SAS 및 서비스 SAS 토큰
* **Api 버전** hello 저장소 서비스 버전 toouse tooexecute hello 요청을 지정 하는 선택적 매개 변수입니다.
* **서비스 버전** hello 저장소 서비스 버전 toouse tooauthenticate hello 요청을 지정 하는 필수 매개 변수입니다.
* **시작 시간.** hello SAS 유효 해지는 hello 시간입니다. 공유 액세스 서명에 대 한 hello 시작 시간 선택 사항입니다. 시작 시간을 생략 하면 hello SAS 즉시 적용 됩니다. hello 시작 시간 단위는 UTC (협정 세계시)를 특수 UTC 지정자 ("Z")와 함께 예를 들어 `1994-11-05T13:15:30Z`합니다.
* **만료 시간.** 이후에 hello SAS가 더 이상 유효 hello 시간입니다. 모범 사례에 따라 SAS의 만료 시간을 지정하거나 만료 시간을 저장된 액세스 정책과 연결하는 것이 좋습니다. hello 만료 시간 단위는 UTC (협정 세계시)를 특수 UTC 지정자 ("Z")와 함께 예를 들어 `1994-11-05T13:15:30Z` (아래 참조).
* **사용 권한** hello SAS에 지정 된 hello 권한을 hello 클라이언트 hello SAS를 사용 하 여 hello 저장소 리소스에 대해 수행할 수 있는 작업을 나타냅니다. 사용 가능한 권한은 계정 SAS와 서비스 SAS가 다릅니다.
* **IP** IP 주소 또는 Azure 외부 범위의 IP 주소를 지정 하는 선택적 매개 변수 (hello 섹션을 참조 [라우팅 세션 구성 상태](../../expressroute/expressroute-workflows.md#routing-session-configuration-state) Express 경로 대 한) tooaccept 요청에서.
* **프로토콜** Hello 프로토콜을 지정 하는 선택적 매개 변수는 요청에 대해 허용 합니다. 가능한 값은 HTTPS와 HTTP (`https,http`)을 하는 경우 hello 기본값 또는 HTTPS만 (`https`). HTTP만은 허용되는 값이 아닙니다.
* **서명** hello 서명을 hello에서 구성 된 다른 매개 변수 부분 토큰으로 지정 하 고 다음 암호화 합니다. Tooauthenticate hello SAS를 사용 하는 합니다.

### <a name="parameters-for-a-service-sas-token"></a>서비스 SAS 토큰의 매개 변수
* **저장소 리소스** 서비스 SAS를 사용하여 액세스 권한을 위임할 수 있는 저장소 리소스는 다음과 같습니다.
  * 컨테이너 및 Blob
  * 파일 공유 및 파일
  * 큐
  * 테이블 및 테이블 엔터티 범위

### <a name="parameters-for-an-account-sas-token"></a>계정 SAS 토큰의 매개 변수
* **서비스** SA 계정 액세스 tooone 또는 그 이상의 hello 저장소 서비스에 위임할 수 있습니다. 예를 들어 대리자 toohello Blob 및 파일 서비스에 액세스 하는 계정을 SAS를 만들 수 있습니다. 또는 대리자 tooall 4 개의 서비스 (Blob, 큐, 테이블 및 파일)에 액세스 하는 SAS를 만들 수 있습니다.
* **저장소 리소스 유형** 계정 SAS tooone 또는 특정 리소스 대신 저장소 리소스의 더 많은 클래스를 적용합니다. 에 대 한 계정 SAS toodelegate 액세스를 만들 수 있습니다.
  * 서비스 수준 Api를 hello 저장소 계정 리소스에 대해 호출 됩니다. 예를 들면 **서비스 속성 가져오기/설정**, **서비스 통계 가져오기**, **컨테이너/큐/테이블/공유 나열**이 포함됩니다.
  * 각 서비스에 대 한 hello 컨테이너 개체에 대해 호출 되는 컨테이너 수준 Api: 컨테이너, 큐, 테이블, blob 및 파일 공유 합니다. 예를 들어 **컨테이너 만들기/삭제**, **큐 만들기/삭제**, **테이블 만들기/삭제**, **공유 만들기/삭제**, **Blob/파일 및 디렉터리 나열**이 있습니다.
  * Blob, 큐 메시지, 테이블 엔터티, 파일에 대해 호출되는 개체 수준 API. 예를 들어 **Blob 배치**, **쿼리 엔터티**, **메시지 가져오기**, **파일 만들기**가 있습니다.

## <a name="examples-of-sas-uris"></a>SAS URI의 예

### <a name="service-sas-uri-example"></a>서비스 SAS URI 예

SAS URI를 제공 하는 한 읽기 및 쓰기 권한을 tooa blob 서비스의 예를 들면 다음과 같습니다. hello 테이블 toohello SAS를 기여 어떻게 hello URI toounderstand의 각 부분 다운이 중단 됩니다.

```
https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2015-04-05&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D
```

| 이름 | SAS 부분 | 설명 |
| --- | --- | --- |
| Blob URI |`https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt` |hello blob의 hello 주소입니다. HTTPS를 사용하는 것이 좋습니다. |
| 저장소 서비스 버전 |`sv=2015-04-05` |저장소 서비스 버전 2012-02-12 및 이상 버전에서는이 매개 변수 hello 버전 toouse를 나타냅니다. |
| 시작 시간 |`st=2015-04-29T22%3A18%3A26Z` |UTC 시간으로 지정됩니다. 원할 경우 hello SAS toobe 유효한 즉시 hello 시작 시간을 생략 합니다. |
| 만료 시간 |`se=2015-04-30T02%3A23%3A26Z` |UTC 시간으로 지정됩니다. |
| 리소스 |`sr=b` |hello 리소스는 blob입니다. |
| 권한 |`sp=rw` |hello SAS가 부여 하는 hello 권한 Read (r) 포함 및 쓰기 (w). |
| IP 범위 |`sip=168.1.5.60-168.1.5.70` |hello IP 주소 범위를 요청을 수락 합니다. |
| 프로토콜 |`spr=https` |HTTPS를 사용하는 요청만 허용됩니다. |
| 서명 |`sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D` |Tooauthenticate 액세스 toohello blob을 사용합니다. hello 서명 문자열 대 기호 및 hello SHA256 알고리즘을 사용 하 여 키를 통해 계산 하 고 다음 Base64 인코딩을 사용 하 여 인코딩된 HMAC입니다. |

### <a name="account-sas-uri-example"></a>계정 SAS URI 예

Hello hello 토큰에 동일한 일반 매개 변수를 사용 하는 계정의 SAS 예를 들면 다음과 같습니다. 이러한 매개 변수는 위에서 설명했으므로 여기에서는 설명을 생략합니다. Hello 매개 변수만 되 특정 tooaccount SAS hello 테이블 아래에 설명 되어 있습니다.

```
https://myaccount.blob.core.windows.net/?restype=service&comp=properties&sv=2015-04-05&ss=bf&srt=s&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=F%6GRVAZ5Cdj2Pw4tgU7IlSTkWgn7bUkkAg8P6HESXwmf%4B
```

| 이름 | SAS 부분 | 설명 |
| --- | --- | --- |
| 리소스 URI |`https://myaccount.blob.core.windows.net/?restype=service&comp=properties` |hello Blob 서비스 끝점 (GET를 사용 하 여 호출) 하는 경우 서비스 속성을 가져오거나 (사용 하 여 호출) 하는 경우 서비스 속성 설정에 대 한 매개 변수를 사용 합니다. |
| Services |`ss=bf` |hello SAS 적용 toohello Blob 및 파일 서비스 |
| 리소스 유형 |`srt=s` |hello SAS tooservice 수준 작업을 적용합니다. |
| 권한 |`sp=rw` |hello 권한을 tooread 액세스를 부여 하 고 쓰기 작업 합니다. |

이 SAS로 액세스할 수 있는 작업, toohello 서비스 수준에는 권한이 제한 된 있다고 가정 **Blob 서비스 속성 가져오기** (읽기) 및 **Blob 서비스 속성 설정** (쓰기). 그러나 다른 리소스 URI와 hello 같은 SAS 토큰 수 toodelegate 액세스도 사용할**Blob 서비스 통계 가져오기** (읽기)입니다.

## <a name="controlling-a-sas-with-a-stored-access-policy"></a>저장된 액세스 정책을 사용하여 SAS 관리
공유 액세스 서명은 다음 두 가지 형식 중 하나를 사용할 수 있습니다.

* **임시 SAS:** 는 임시 SAS, hello 시작 시간, 만료 시간을 만들고 SAS hello에 대 한 권한을 모두에 지정 된 SAS URI hello (명시적 이나 묵시적 시작 시간을 생략 하면 hello 경우에서). 이 SAS 유형은 계정 SAS 또는 서비스 SAS로 만들 수 있습니다.
* **저장 된 액세스 정책 사용 하 여 SAS:** 저장 된 액세스 정책은 리소스 컨테이너-blob 컨테이너에 정의 되어, 테이블, 큐 또는 파일 공유-및 하나 이상의 공유 액세스 서명에 대 한 제약 조건을 사용 하는 toomanage 될 수 있습니다. 저장 된 액세스 정책을 사용 하 여 SAS를 연결 하면 hello SAS hello 시작 시간, 만료 시간 및 권한을-hello 저장 된 액세스 정책에 대해 정의 된 hello 제약을 상속 합니다.

> [!NOTE]
> 현재, 계정 SAS는 애드혹 SAS여야 합니다. 저장된 액세스 정책은 아직 계정 SAS에 지원되지 않습니다.

hello hello 두 형식의 차이 한 가지 주요 시나리오에 대 한 중요: 해지 합니다. SAS URI URL 이기 때문에 hello가 가져오는 모든 사용자에 게 SAS을 사용 하려면 원래 만든 사람에 관계 없이 합니다. SAS를 공개적으로 게시 하는 경우에 hello world의 다른 사용자가 사용할 수 있습니다. SAS 권한 부여 액세스 tooresources tooanyone 4 가지 중 하나가 발생 될 때까지 소유:

1. SAS에 도달 하는 hello에 지정 된 만료 시간을 hello입니다.
2. SAS (저장된 된 액세스 정책을 참조 하는 경우 및 만료 시간을 지정 하는 경우)에 도달 하는 hello에서 참조 하는 hello 저장 된 액세스 정책에 지정 된 만료 시간을 hello입니다. 이 hello 간격이 경과 하거나 한 가지 방법은 toorevoke hello SAS 않는 전의 hello에 만료 시간이 hello 저장 된 액세스 정책을 수정한 발생할 수 있습니다.
3. hello 저장 하는 또 다른 방법은 toorevoke hello SAS SAS 삭제 되 면 hello에서 참조 하는 액세스 정책. 가 토큰을 정확히 hello 저장 된 액세스 정책을 다시 만드는 경우 hello 이름이 같은 모든 기존 SAS는 다시 수에 따라 유효한 toohello 권한 해당 저장 된 액세스 정책과 연관 (SAS을 지나치지 않은 hello에 해당 hello 만료 시간을 가정). Toorevoke hello SAS를 하려는 경우 수 있는지 toouse 다른 이름을 hello 액세스 정책 만료 시간이 hello 나중에 다시 만드는 경우.
4. 사용 하는 toocreate hello SAS hello 계정 키 다시 생성 됩니다. 계정 키를 다시 생성 하면 해당 키 toofail tooauthenticate를 사용 하 여 모든 응용 프로그램 구성 요소 업데이트 될 때까지 toouse 다른 유효한 계정 키 또는 hello 새로 다시 생성된 된 계정 키를 하거나 hello 합니다.

> [!IMPORTANT]
> 공유 액세스 서명 URI hello 계정 키 사용 되는 toocreate hello 서명과 사용 하 여 연결 되며 hello (있는 경우) 저장 된 액세스 정책에 연결 합니다. 저장 된 액세스 정책이 없는 지정, hello만 방법은 toorevoke 공유 액세스 서명을 toochange hello 계정 키입니다.

## <a name="authenticating-from-a-client-application-with-a-sas"></a>SAS를 사용하여 클라이언트 응용 프로그램 인증
클라이언트는 SAS 소유 하는 hello SAS tooauthenticate을가지고 있지 않기 hello 계정 키 저장소 계정에 대 한 요청을 사용할 수 있습니다. SAS 연결 문자열에 포함 또는 hello 적절 한 생성자 또는 메서드에에서 직접 사용할 수 있습니다.

### <a name="using-a-sas-in-a-connection-string"></a>연결 문자열에서 SAS 사용
[!INCLUDE [storage-use-sas-in-connection-string-include](../../../includes/storage-use-sas-in-connection-string-include.md)]

### <a name="using-a-sas-in-a-constructor-or-method"></a>생성자 또는 메서드에서 SAS 사용
여러 Azure 저장소 클라이언트 라이브러리 생성자 및 메서드 오버 로드 된 한 SAS 요청 toohello 서비스를 인증할 수 있도록 SAS 매개 변수를 제공 합니다.

예를 들어 다음 SAS URI은 사용 되는 toocreate 참조 tooa 블록 blob입니다. hello SAS hello 요청에 대 한 필요한 hello 유일한 자격 증명을 제공 합니다. hello 블록 blob 참조 쓰기 작업에 사용 됩니다.

```csharp
string sasUri = "https://storagesample.blob.core.windows.net/sample-container/" +
    "sampleBlob.txt?sv=2015-07-08&sr=b&sig=39Up9JzHkxhUIhFEjEH9594DJxe7w6cIRCg0V6lCGSo%3D" +
    "&se=2016-10-18T21%3A51%3A37Z&sp=rcw";

CloudBlockBlob blob = new CloudBlockBlob(new Uri(sasUri));

// Create operation: Upload a blob with hello specified name toohello container.
// If hello blob does not exist, it will be created. If it does exist, it will be overwritten.
try
{
    MemoryStream msWrite = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    msWrite.Position = 0;
    using (msWrite)
    {
        await blob.UploadFromStreamAsync(msWrite);
    }

    Console.WriteLine("Create operation succeeded for SAS {0}", sasUri);
    Console.WriteLine();
}
catch (StorageException e)
{
    if (e.RequestInformation.HttpStatusCode == 403)
    {
        Console.WriteLine("Create operation failed for SAS {0}", sasUri);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
    else
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}

```

## <a name="best-practices-when-using-sas"></a>SAS를 사용하는 경우 모범 사례
응용 프로그램에서 공유 액세스 서명을 사용 하는 경우 필요 toobe 두 가지 잠재적인 위험을 인식 합니다.

* SAS가 누설될 경우 SAS를 획득한 모든 사용자가 SAS를 사용하여 저장소 계정을 손상시킬 수 있습니다.
* SAS tooa 클라이언트 응용 프로그램이 만료 되 고 hello 응용 프로그램은 없습니다 tooretrieve 서비스에서 새 SAS를 제공 하면 hello 응용 프로그램의 기능 방해 될 수 있습니다.

hello에 대 한 공유 액세스 서명을 사용 하 여 다음 권장 사항을 완화 시킬 수 있습니다 이러한 위험 합니다.

1. **항상 HTTPS를 사용 하 여** toocreate 하거나 SAS를 배포 합니다. SAS를 HTTP를 통해 전달 되며 가로챌, 공격자가 중간자 개입 공격을 수행 수 tooread hello SAS 되며 다음 hello 잠재적으로 중요 한 데이터를 손상 또는 hello 하 여 데이터 손상 수 있도록 사용자가 수 고를 의도 한 것 처럼 사용 악의적인 사용자입니다.
2. **저장된 액세스 정책을 최대한 참조합니다.** Tooregenerate hello 저장소 계정 키 필요 없이 옵션 toorevoke 권한을 hello 액세스 정책을 제공을 저장 합니다. 이후 (또는 무한) hello에 매우 많이 이러한 이벤트에 대해 hello 만료를 설정 하 고 있는지 확인 toomove 정기적으로 업데이트는 hello 향후에 더 멀리 합니다.
3. **임시 SAS의 경우 짧은 만료 시간을 사용합니다.** 그러면 SAS가 손상되더라도 단기적으로만 유효합니다. 이 방법은 저장된 액세스 정책을 참조할 수 없는 경우에 특히 중요합니다. 단기적 만료 시간에는 또한 hello hello 시간 사용 가능한 tooupload tooit 제한 하 여 tooa blob을 쓸 수 있는 데이터 양을 제한 합니다.
4. **에 클라이언트 hello SAS 필요한 경우 자동으로 갱신 합니다.** 클라이언트는 hello SAS를 제공 하는 hello 서비스를 사용할 수 없는 경우 재시도 대 한 순서 tooallow 시간 hello 만료 전에 hello SAS를 갱신 해야 합니다. 프로그램 SAS toobe 적은 수의 직접 실행에 사용 되는 것입니다를 수명이 짧은 작업을 예상 toobe hello 만료 시간 내에 완료할 경우 hello SAS가 갱신 toobe 예상 대로 불필요 할 수 있습니다이 합니다. 그러나 정기적으로 SAS 통해 요청을 수행 하는 클라이언트를 설정한 경우 다음의 만료 hello 가능성 고려해 야 합니다. hello 주요 고려 사항인 toobalance hello 필요는 hello SAS toobe 수명이 짧은 (이전에 명시 된) 클라이언트 hello hello 필요 tooensure와 초기 갱신을 요청에 대 한 충분 한 (tooavoid 중단 toohello SAS 만료 이전 toosuccessful 갱신 인해).
5. **SAS 시작 시간에 유의하세요.** 경우 hello 시작 시간에 대해 설정한 SAS 너무**이제**, tooclock 기울이기 (현재 시간 toodifferent 컴퓨터에 따라 차이점) 기한 오류 관찰 될 수 있습니다 간헐적으로 hello에 대 한 처음 몇 분 후입니다. 일반적으로 설정 hello 시작 시간 toobe 최소 15 분 이상 지난 hello에 있습니다. 설정하지 않습니다. 그러면 시작 시간이 즉시 유효해집니다. 해질 수 있습니다 too15 분의 클럭을 모든 요청에서 어느 방향으로든에서 시간차 기억 하는 hello tooexpiry 시간 역시-일반적으로 적용 됩니다. 클라이언트는 REST 버전 이전 too2012-02-12를 사용 하 여 hello 최대 저장된 된 액세스 정책을 참조 하지 않는 SAS에 대 한 기간은 1 시간 및 정책을 지정 장기적인 보다는 실패 합니다.
6. **구체적으로 액세스 하는 hello 리소스 toobe 해야 합니다.** 보안 모범 사례는 tooprovide hello 필요한 최소한의 권한 있는 사용자입니다. 사용자만 읽기 권한을 tooa 단일 엔터티를 필요로 한다면 하지: 읽기/쓰기/삭제 액세스 tooall 엔터티와 toothat 단일 엔터티 읽기 액세스를 부여 합니다. 또한 SAS hello SAS는 공격자의 hello 손에 전력에 있기 때문에 손상 된 경우 hello 손상 취약성을 줄일 수 있습니다.
7. **SAS 사용 작업을 포함한 모든 사용량에 대한 요금이 계정에 청구됩니다.** 쓰기 액세스 tooa blob를 제공 하면 200GB blob 사용자 tooupload 선택할 수 있습니다. 에 읽기 액세스 권한도 부여 하였습니다, toodownload를 선택할 수 있습니다 10 회 발생 시 키 지 2TB 송신 비용이 있습니다. 제한 된 사용 권한 다시 제공 toohelp hello 잠재적인 작업 악의적인 사용자가 완화 합니다. 이 위협을 수명이 짧은 SAS tooreduce를 사용 합니다 (그러나 클럭 오차가 hello 종료 시간에 주의 기울여야).
8. **SAS를 사용하여 작성된 데이터의 유효성을 검사하세요.** 클라이언트 응용 프로그램 데이터 tooyour 저장소 계정에 쓰기 때 염두에 해당 데이터에 문제가 있을 수 있습니다. 응용 프로그램에 필요한 데이터 유효성을 검사 하거나 준비 toouse 되기 전에 인증 수, 하는 경우에 hello 데이터가 기록 되 고 응용 프로그램에서 사용 하기 전에이 유효성 검사를 수행 해야 합니다. 또한이 연습 유출 된 SAS 악용 사용자 또는 사용자가 제대로 hello SAS를 획득 하거나 tooyour 계정 쓰여지는 손상 되거나 악의적인 데이터에 대 한 보호 합니다.
9. <seg>
  **경우에 따라 SAS를 사용하지 마세요..**</seg> 경우에 따라 저장소 계정에 대해 특정 작업과 관련 된 hello 위험 sa hello 이점을 보다 더 큽니다. 이러한 작업에 대 한 비즈니스를 수행한 후 tooyour 저장소 계정에 기록 하는 중간 계층 서비스를 만드는 규칙 유효성 검사, 인증 및 감사 합니다. 또한, 경우에 다른 방법으로 toomanage 액세스를 더 간단 합니다. 예를 들어 원하는 toomake 컨테이너의 모든 blob 공개적으로 읽을 수 만들면 컨테이너 공용, hello SAS tooevery 클라이언트 액세스를 위해 제공 하는 대신 합니다.
10. **Storage Analytics toomonitor 응용 프로그램을 사용 합니다.** 로깅 및 메트릭 tooobserve tooan 정전 프로그램 SAS 공급자 서비스 또는 toohello 실수로 제거 저장 된 액세스 정책으로 인해 인증 오류가으로 가끔 치솟는 하나를 사용할 수 있습니다. Hello 참조 [Azure 저장소 팀 블로그](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx) 추가 정보에 대 한 합니다.

## <a name="sas-examples"></a>SAS 예제
다음은 공유 액세스 서명의 두 유형(계정 SAS, 서비스 SAS)에 대한 몇 가지 예입니다.

toorun이 C# 예제에서는 프로젝트에서 NuGet 패키지를 다음 tooreference hello 필요:

* [.NET 용 azure 저장소 클라이언트 라이브러리](http://www.nuget.org/packages/WindowsAzure.Storage)을 버전 6.x 또는 이후 (toouse 계정 SAS).
* [Azure 구성 관리자](http://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager)

Toocreate 및 테스트 SAS 참조 하는 방법을 보여 주는 추가 예에 대 한 [저장소에 대 한 Azure 코드 예제](https://azure.microsoft.com/documentation/samples/?service=storage)합니다.

### <a name="example-create-and-use-an-account-sas"></a>예제: SAS 계정 만들기 및 사용
hello 다음 코드 예제에서는 Blob hello 및 파일 서비스를 사용할 수 있는 SA 계정을 만들고 클라이언트 권한 읽기, 쓰기 및 목록 사용 권한 부여 hello tooaccess 서비스 수준 Api입니다. hello 계정 SAS hello 요청 해야 HTTPS를 사용 하므로 hello 프로토콜 tooHTTPS를 제한 합니다.

```csharp
static string GetAccountSASToken()
{
    // toocreate hello account SAS, you need toouse your shared key credentials. Modify for your account.
    const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

    // Create a new access policy for hello account.
    SharedAccessAccountPolicy policy = new SharedAccessAccountPolicy()
        {
            Permissions = SharedAccessAccountPermissions.Read | SharedAccessAccountPermissions.Write | SharedAccessAccountPermissions.List,
            Services = SharedAccessAccountServices.Blob | SharedAccessAccountServices.File,
            ResourceTypes = SharedAccessAccountResourceTypes.Service,
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Protocols = SharedAccessProtocol.HttpsOnly
        };

    // Return hello SAS token.
    return storageAccount.GetSharedAccessSignature(policy);
}
```

toouse hello 계정 SAS tooaccess 서비스 수준 Api hello Blob 서비스에 대해, hello SAS를 사용 하 여 Blob 클라이언트 개체를 생성 및 저장소 계정에 대 한 Blob 저장소 끝점 hello 합니다.

```csharp
static void UseAccountSAS(string sasToken)
{
    // Create new storage credentials using hello SAS token.
    StorageCredentials accountSAS = new StorageCredentials(sasToken);
    // Use these credentials and hello account name toocreate a Blob service client.
    CloudStorageAccount accountWithSAS = new CloudStorageAccount(accountSAS, "account-name", endpointSuffix: null, useHttps: true);
    CloudBlobClient blobClientWithSAS = accountWithSAS.CreateCloudBlobClient();

    // Now set hello service properties for hello Blob client created with hello SAS.
    blobClientWithSAS.SetServiceProperties(new ServiceProperties()
    {
        HourMetrics = new MetricsProperties()
        {
            MetricsLevel = MetricsLevel.ServiceAndApi,
            RetentionDays = 7,
            Version = "1.0"
        },
        MinuteMetrics = new MetricsProperties()
        {
            MetricsLevel = MetricsLevel.ServiceAndApi,
            RetentionDays = 7,
            Version = "1.0"
        },
        Logging = new LoggingProperties()
        {
            LoggingOperations = LoggingOperations.All,
            RetentionDays = 14,
            Version = "1.0"
        }
    });

    // hello permissions granted by hello account SAS also permit you tooretrieve service properties.
    ServiceProperties serviceProperties = blobClientWithSAS.GetServiceProperties();
    Console.WriteLine(serviceProperties.HourMetrics.MetricsLevel);
    Console.WriteLine(serviceProperties.HourMetrics.RetentionDays);
    Console.WriteLine(serviceProperties.HourMetrics.Version);
}
```

### <a name="example-create-a-stored-access-policy"></a>예제: 저장된 액세스 정책 만들기
hello 다음 코드는 저장 된 액세스 정책을 만듭니다 컨테이너. 서비스 hello 컨테이너에 대 한 SAS 또는 해당 blob에 대 한 hello 액세스 정책 toospecify 제약 조건을 사용할 수 있습니다.

```csharp
private static async Task CreateSharedAccessPolicyAsync(CloudBlobContainer container, string policyName)
{
    // Create a new shared access policy and define its constraints.
    // hello access policy provides create, write, read, list, and delete permissions.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
        // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
        SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.List |
            SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create | SharedAccessBlobPermissions.Delete
    };

    // Get hello container's existing permissions.
    BlobContainerPermissions permissions = await container.GetPermissionsAsync();

    // Add hello new policy toohello container's permissions, and set hello container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    await container.SetPermissionsAsync(permissions);
}
```

### <a name="example-create-a-service-sas-on-a-container"></a>예제: 컨테이너에 서비스 SAS 만들기
hello 코드 다음 컨테이너에 대 한 SAS를 만듭니다. 기존 저장 된 액세스 정책의 hello 이름이 제공 된 경우 해당 정책 SAS hello와 관련이 있습니다. 저장 된 액세스 정책이 없는 제공 hello 코드 hello 컨테이너에서 임시 SAS을 만듭니다.

```csharp
private static string GetContainerSasUri(CloudBlobContainer container, string storedPolicyName = null)
{
    string sasContainerToken;

    // If no stored policy is specified, create a new access policy and define its constraints.
    if (storedPolicyName == null)
    {
        // Note that hello SharedAccessBlobPolicy class is used both toodefine hello parameters of an ad-hoc SAS, and
        // tooconstruct a shared access policy that is saved toohello container's shared access policies.
        SharedAccessBlobPolicy adHocPolicy = new SharedAccessBlobPolicy()
        {
            // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
            // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List
        };

        // Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
        sasContainerToken = container.GetSharedAccessSignature(adHocPolicy, null);

        Console.WriteLine("SAS for blob container (ad hoc): {0}", sasContainerToken);
        Console.WriteLine();
    }
    else
    {
        // Generate hello shared access signature on hello container. In this case, all of hello constraints for the
        // shared access signature are specified on hello stored access policy, which is provided by name.
        // It is also possible toospecify some constraints on an ad-hoc SAS and others on hello stored access policy.
        sasContainerToken = container.GetSharedAccessSignature(null, storedPolicyName);

        Console.WriteLine("SAS for blob container (stored access policy): {0}", sasContainerToken);
        Console.WriteLine();
    }

    // Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

### <a name="example-create-a-service-sas-on-a-blob"></a>예제: Blob에 서비스 SAS 만들기
hello 코드 다음 blob에는 SAS를 만듭니다. 기존 저장 된 액세스 정책의 hello 이름이 제공 된 경우 해당 정책 SAS hello와 관련이 있습니다. 저장 된 액세스 정책이 없는 제공 hello 코드 hello blob에서 임시 SAS을 만듭니다.

```csharp
private static string GetBlobSasUri(CloudBlobContainer container, string blobName, string policyName = null)
{
    string sasBlobToken;

    // Get a reference tooa blob within hello container.
    // Note that hello blob may not exist yet, but a SAS can still be created for it.
    CloudBlockBlob blob = container.GetBlockBlobReference(blobName);

    if (policyName == null)
    {
        // Create a new access policy and define its constraints.
        // Note that hello SharedAccessBlobPolicy class is used both toodefine hello parameters of an ad-hoc SAS, and
        // tooconstruct a shared access policy that is saved toohello container's shared access policies.
        SharedAccessBlobPolicy adHocSAS = new SharedAccessBlobPolicy()
        {
            // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
            // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create
        };

        // Generate hello shared access signature on hello blob, setting hello constraints directly on hello signature.
        sasBlobToken = blob.GetSharedAccessSignature(adHocSAS);

        Console.WriteLine("SAS for blob (ad hoc): {0}", sasBlobToken);
        Console.WriteLine();
    }
    else
    {
        // Generate hello shared access signature on hello blob. In this case, all of hello constraints for the
        // shared access signature are specified on hello container's stored access policy.
        sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

        Console.WriteLine("SAS for blob (stored access policy): {0}", sasBlobToken);
        Console.WriteLine();
    }

    // Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

## <a name="conclusion"></a>결론
공유 액세스 서명에 제한 된 권한 hello 계정 키 없어야 tooyour 저장소 계정 tooclients 제공 하는 데 유용 합니다. 따라서 서로 Azure 저장소를 사용 하 여 모든 응용 프로그램에 대 한 hello 보안 모델의 필수 요소입니다. 여기에 나열 된 hello 모범 사례를 따르는 경우에 hello 응용 프로그램의 보안을 손상 시 키 지 않고 저장소 계정의 SAS tooprovide 보다 유연 하 게 액세스 tooresources 사용할 수 있습니다.

## <a name="next-steps"></a>다음 단계
* [익명 읽기 권한을 toocontainers 및 blob 관리](../blobs/storage-manage-access-to-resources.md)
* [공유 액세스 서명을 사용하여 액세스 위임](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [테이블 및 큐 SAS 소개](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
