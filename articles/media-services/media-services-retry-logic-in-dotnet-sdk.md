---
title: "hello Media Services SDK for.NET에서에서 aaaRetry 논리 | Microsoft Docs"
description: "hello 항목 for.net hello Media Services SDK에서에서 재시도 논리에 대 한 개요를 제공합니다."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 527b61a6-c862-4bd8-bcbc-b9aea1ffdee3
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: juliako
ms.openlocfilehash: 18d0a9d68e55a48bc769fb6ae5711ddba78ed8e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="retry-logic-in-hello-media-services-sdk-for-net"></a>.NET 용 hello Media Services SDK에서에서 논리를 다시 시도
Microsoft Azure 서비스에서 작업할 때 일시적 오류가 발생할 수 있습니다. 대부분의 경우에서 일시적인 오류를 발생 하는 경우 몇 가지 다시 시도한 후 hello 작업이 성공 합니다. Media Services SDK for.NET hello hello 재시도 논리 toohandle 일시적인 오류 예외 및 웹 요청, 쿼리, 저장 변경 사항 및 저장소 작업을 실행 하 여 발생 하는 오류와 관련 된 구현 합니다.  기본적으로 hello Media Services SDK for.NET hello 예외 tooyour 응용 프로그램을 다시 throw 되기 전에 4 개의 재시도 실행 합니다. 그런 다음 응용 프로그램의 hello 코드가이 예외를 제대로 처리 해야 합니다.  

 hello 다음은 웹 요청, 저장소, 쿼리 및 SaveChanges 정책에 대 한 간략 한 지침입니다.  

* hello 저장소 정책 (업로드 또는 자산 파일의 다운로드) blob 저장소 작업에 사용 됩니다.  
* hello 웹 요청 정책 (예: 인증 토큰 가져오기 및 hello 사용자가 클러스터 끝점을 해결 하는) 제네릭 웹 요청에 사용 됩니다.  
* hello 쿼리 정책 (예를 들어 mediaContext.Assets.Where(...)) 나머지에서 엔터티를 쿼리 하기 위해 사용 됩니다.  
* hello SaveChanges 정책 (예: 함수를 호출 하면 서비스 작업에 대 한 엔터티를 업데이트 하는 엔터티를 만드는) hello 서비스 내에서 데이터를 변경 하는 아무 것도 수행 하는 데 사용 됩니다.  
  
  다시 시도 논리에서 처리 하는 hello Media Services SDK for.NET 오류 코드 및이 항목에 예외 형식을 보여 줍니다.  

## <a name="exception-types"></a>예외 유형
hello 다음 표에서 해당 hello Media Services SDK.NET 핸들에 대 한 예외를 설명 하거나 일시적인 오류를 일으킬 수 있는 일부 작업을 처리 하지 않습니다.  

| 예외 | 웹 요청 | 저장소 | 쿼리 | SaveChanges |
| --- | --- | --- | --- | --- |
| WebException<br/>자세한 내용은 참조 hello [WebException 상태 코드](media-services-retry-logic-in-dotnet-sdk.md#WebExceptionStatus) 섹션. |예 |예 |예 |예 |
| DataServiceClientException<br/> 자세한 내용은 [HTTP 오류 상태 코드](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode)를 참조하세요. |아니요 |예 |예 |예 |
| DataServiceQueryException<br/> 자세한 내용은 [HTTP 오류 상태 코드](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode)를 참조하세요. |아니요 |예 |예 |예 |
| DataServiceRequestException<br/> 자세한 내용은 [HTTP 오류 상태 코드](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode)를 참조하세요. |아니요 |예 |예 |예 |
| DataServiceTransportException |아니요 |아니요 |예 |예 |
| TimeoutException |예 |예 |예 |아니요 |
| SocketException |예 |예 |예 |예 |
| StorageException |아니요 |예 |아니요 |아니요 |
| IOException |아니요 |예 |아니요 |아니요 |

### <a name="WebExceptionStatus"></a> WebException 상태 코드
hello 다음 표에서 WebException 오류 코드 hello 재시도 논리 구현 됩니다. hello [수행 하지](http://msdn.microsoft.com/library/system.net.webexceptionstatus.aspx) 열거형 hello 상태 코드를 정의 합니다.  

| 가동 상태 | 웹 요청 | 저장소 | 쿼리 | SaveChanges |
| --- | --- | --- | --- | --- |
| ConnectFailure |예 |예 |예 |예 |
| NameResolutionFailure |예 |예 |예 |예 |
| ProxyNameResolutionFailure |예 |예 |예 |예 |
| SendFailure |예 |예 |예 |예 |
| PipelineFailure |예 |예 |예 |아니요 |
| ConnectionClosed |예 |예 |예 |아니요 |
| KeepAliveFailure |예 |예 |예 |아니요 |
| UnknownError |예 |예 |예 |아니요 |
| ReceiveFailure |예 |예 |예 |아니요 |
| RequestCanceled |예 |예 |예 |아니요 |
| 시간 제한 |예 |예 |예 |아니요 |
| ProtocolError <br/>hello 다시 시도 횟수를 ProtocolError hello HTTP 상태 코드 처리 하 여 제어 됩니다. 자세한 내용은 [HTTP 오류 상태 코드](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode)를 참조하세요. |예 |예 |예 |예 |

### <a name="HTTPStatusCode"></a> HTTP 오류 상태 코드
쿼리 및 SaveChanges 작업 DataServiceClientException, DataServiceQueryException, 또는 DataServiceQueryException를 throw 하는 경우 HTTP 오류 상태 코드 hello hello StatusCode 속성에에서 반환 됩니다.  hello 다음 표에서 오류 코드에 대 한 hello 재시도 논리 구현 됩니다.  

| 가동 상태 | 웹 요청 | 저장소 | 쿼리 | SaveChanges |
| --- | --- | --- | --- | --- |
| 401 |아니요 |예 |아니요 |아니요 |
| 403 |아니요 |예<br/>더 긴 대기 시간으로 재시도를 처리함. |아니요 |아니요 |
| 408 |예 |예 |예 |예 |
| 429 |예 |예 |예 |예 |
| 500 |예 |예 |예 |아니요 |
| 502 |예 |예 |예 |아니요 |
| 503 |예 |예 |예 |예 |
| 504 |예 |예 |예 |아니요 |

.NET 재시도 논리에 대 한 tootake hello Media Services SDK의 실제 구현과 hello 확인 하려는 경우 참조 [미디어 서비스에 대 한 azure sdk](https://github.com/Azure/azure-sdk-for-media-services/tree/dev/src/net/Client/TransientFaultHandling)합니다.

## <a name="next-steps"></a>다음 단계
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

