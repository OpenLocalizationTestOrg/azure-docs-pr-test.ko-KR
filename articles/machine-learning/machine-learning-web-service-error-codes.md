---
title: "aaaAzure 컴퓨터 학습 REST API 오류 코드 | Microsoft Docs"
description: "이러한 오류 코드는 Azure Machine Learning 웹 서비스의 작업에서 반환될 수 있습니다."
keywords: 
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 0923074b-3728-439d-a1b8-8a7245e39be4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: reference
ms.date: 11/16/2016
ms.author: garye
ms.openlocfilehash: 9495c8ef16e684d3c8978bcd11747cf95227b091
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-rest-api-error-codes"></a>Machine Learning REST API 오류 코드
 
hello 다음과 같은 오류 코드가 반환 될 수는 Azure 기계 학습 웹 서비스에 대 한 작업으로 합니다.
 
## <a name="badargument-http-status-code-400"></a>BadArgument(HTTP 상태 코드 400)
 
잘못된 인수가 제공되었습니다.
 
이 오류 클래스는 어딘가에 제공된 인수가 잘못되었다는 의미입니다. Azure 저장소 toosomething 전달 toohello 웹 서비스의 위치 또는 자격 증명 수 있습니다. Hello 오류 "코드" 필드 hello "details 라는" 섹션 toodiagnose 된 특정 인수에 올바르지 않은를 참조 하십시오.
 
| 오류 코드 | 사용자 메시지 |
| ---------- |--------------|
| BadParameterValue | hello 매개 변수 값이 제공 hello 매개 변수에서 hello 매개 변수 규칙을 만족 하지 않습니다. |
| BadSubscriptionId | hello 구독 Id를 사용 하는 tooscore hello 리소스에 있는 하나 hello 않습니다. |
| BadVersionCall | Hello API 호출 하는 동안 잘못 된 버전 매개 변수가 전달 되었습니다: {0}. Hello API 도움말 페이지 hello 올바른 버전을 전달 하 고 다시 시도 확인 합니다. |
| BatchJobInputsNotSpecified | 필수 입력은 다음 hello hello 요청과 함께 지정 하지 않았습니다: {0}. 입력 데이터를 모두 지정하고 다시 시도하세요. |
| BatchJobInputsTooManySpecified | hello 요청 hello 서비스에서 정의 된 것 보다 많은 입력을 지정 합니다. 허용된 입력 목록: {0}. 입력 데이터를 모두 올바르게 지정하고 다시 시도하세요. |
| BlobNameTooLong | 진단 출력을 위해 제공된 Azure Blob Storage 경로가 너무 깁니다. {0}. Hello 경로 줄이고 다시 시도 하십시오. |
| BlobNotFound | 없습니다 tooaccess hello 제공 Azure blob-{0}.  Azure 오류 메시지: {1}. |
| ContainerIsEmpty | Azure Storage 컨테이너 이름이 제공되지 않았습니다. 유효한 컨테이너 이름을 제공하고 다시 시도하세요. |
| ContainerSegmentInvalid | 컨테이너 이름이 잘못되었습니다. 유효한 컨테이너 이름을 제공하고 다시 시도하세요. |
| ContainerValidationFailed | Blob 컨테이너 유효성 검사가 {0} 오류로 인해 실패했습니다. |
| DataTypeNotSupported | 지원되지 않는 데이터 형식이 제공되었습니다. 유효한 데이터 형식을 제공하고 다시 시도하세요. |
| DuplicateInputInBatchCall | hello 일괄 처리 요청이 잘못 되었습니다. 단일 및 다중 입력 hello에 동일한 지정할 수 없습니다 시간입니다. Hello 요청에서 이러한 항목 중 하나를 제거 하 고 다시 시도 하십시오. |
| ExpiryTimeInThePast | Hello 과거에 제공 된 만료 시간: {0}. 미래의 만료 시간을 UTC로 제공하고 다시 시도하세요. toonever 만료, 만료 시간 tooNULL를 설정 합니다. |
| IncompleteSettings | 진단 설정이 완전하지 않습니다. |
| InputBlobRelativeLocationInvalid | Azure Storage Blob 이름이 제공되지 않았습니다. 유효한 Blob 이름을 제공하고 다시 시도하세요. |
| InvalidBlob | Blob {0}에 대한 Blob 사양이 잘못되었습니다. 연결 문자열/상대 경로 또는 SAS 토큰 사양이 올바른지 확인하고 다시 시도하세요. |
| InvalidBlobConnectionString | 잘못 된에서 hello 입/출력 blob 중 하나에 대해 지정 된 연결 문자열 hello: {0}. 잘못된 내용을 수정하고 다시 시도하세요. |
| InvalidBlobExtension | blob 참조 hello: {0}에 잘못 되었거나 누락 된 파일 확장명입니다. 이 출력 형식에 지원되는 파일 확장명은 "{1}"입니다. |
| InvalidInputNames | 잘못 된 서비스는 hello 요청에 지정 된 이름 입력: {0}. 매핑할 hello 입력된 데이터 toohello 올바른 서비스 입력 하 고 다시 시도 하십시오. |
| InvalidOutputOverrideName | 잘못된 출력 재정의 이름: {0}. hello 서비스에는이 이름 가진 출력 노드로 없습니다. 올바른 출력 노드 이름 toooverride을 전달 하세요 (대/소문자 구분 적용 됨). |
| InvalidQueryParameter | 잘못된 쿼리 매개 변수 '{0}'. {1} |
| MissingInputBlobInformation | Azure Storage Blob 정보가 누락되었습니다. 유효한 연결 문자열 및 상대 경로 또는 URI를 제공하고 다시 시도하세요. |
| MissingJobId | 작업 ID가 제공되지 않았습니다. 작업 Id는 작업이 처음으로 hello에 대 한 전송 될 때 반환 됩니다. Hello 작업 Id가 올바른지 및 다시 시도 확인 합니다. |
| MissingKeys | 키가 제공되지 않았거나 기본 또는 보조 키 중 하나가 제공되지 않았습니다. |
| MissingModelPackage | 모델 패키지 ID 또는 모델 패키지가 제공되지 않았습니다. 유효한 모델 패키지 ID 또는 모델 패키지를 제공하고 다시 시도하세요. |
| MissingOutputOverrideSpecification | hello 요청 출력 재정의 {0}에 대 한 hello blob 사양이 없습니다. Hello 요청과 함께 유효한 blob 위치를 지정 하거나 위치가 재정의 되지 원하면 hello 출력 사양이 제거 하십시오. |
| MissingRequestInput | hello 웹 서비스는 입력에 필요 하지만 없는 입력이 제공 되었습니다. 게시 된 hello를 기준으로 유효한 입력 제공 확인할 hello 모델에서 포트를 입력 하 고 다시 시도 하십시오. |
| MissingRequiredGlobalParameters | 필수 웹 서비스 매개 변수 중 일부가 제공되지 않았습니다. Hello 매개 변수에 대 한 모듈 올바른지, 그리고 다시 시도 하는 hello에 대 한 예상 확인 합니다. |
| MissingRequiredOutputOverrides | 필수 toopass는 암호화 된 서비스 끝점을 호출 하는 경우 모든 hello 서비스의 출력에 대 한 출력을 재정의 합니다. 이러한 출력에 대해 현재 누락된 재정의: {0} |
| MissingWebServiceGroupId | 웹 서비스 그룹 ID가 제공되지 않았습니다. 유효한 웹 서비스 그룹 ID를 제공하고 다시 시도하세요. |
| MissingWebServiceId | 웹 서비스 ID가 제공되지 않았습니다. 유효한 웹 서비스 ID를 제공하고 다시 시도하세요. |
| MissingWebServicePackage | 웹 서비스 패키지가 제공되지 않았습니다. 유효한 웹 서비스 패키지를 제공하고 다시 시도하세요. |
| MissingWorkspaceId | 작업 영역 ID가 제공되지 않았습니다. 유효한 작업 영역 ID를 제공하고 다시 시도하세요. |
| ModelConfigurationInvalid | Hello 모델 패키지에 잘못 된 모델 구성입니다. 출력 끝점 정의 표준 오류 끝점을 포함 하는 hello 모델 구성 및 std 끝점을 종료 하 고 다시 시도 확인 합니다. |
| ModelPackageIdInvalid | 모델 패키지 ID가 잘못되었습니다. 해당 hello 모델 패키지 Id가 올바른지 확인 하 고 다시 시도 하십시오. |
| RequestBodyInvalid | 제공 하는 요청 본문 또는 hello 요청 본문을 역직렬화 하는 동안 오류가 발생 했습니다. 없습니다. |
| RequestIsEmpty | 요청이 제공되지 않았습니다. 유효한 요청을 제공하고 다시 시도하세요. |
| UnexpectedParameter | 예기치 않은 매개 변수가 제공되었습니다. 모든 매개 변수 이름의 철자가 올바른지, 예상된 매개 변수가 전달되는지 확인하고 다시 시도하세요. |
| UnknownError | 알 수 없는 오류입니다. |
| UserParameterInvalid | {0} |
| WebServiceConcurrentRequestRequirementInvalid | {0} 웹 서비스에 대한 동시 요청 요구 사항을 변경할 수 없습니다. |
| WebServiceIdInvalid | 잘못된 웹 서비스 ID가 제공되었습니다. 웹 서비스 ID는 유효한 GUID여야 합니다. |
| WebServiceTooManyConcurrentRequestRequirement | {0} 보다 요구 사항이 toomore 동시 요청을 설정할 수 없습니다. |
| WebServiceTypeInvalid | 잘못된 웹 서비스 유형이 제공되었습니다. Hello 올바른 웹 서비스 형식이 올바른지 확인 하 고 다시 시도 하십시오. 유효한 웹 서비스 유형: {0}. |
 
## <a name="baduserargument-http-status-code-400"></a>BadUserArgument(HTTP 상태 코드 400)
 
잘못된 사용자 인수가 제공되었습니다.
 
| 오류 코드 | 사용자 메시지 |
| ---------- |--------------|
| InputMismatchError | 입력 데이터가 입력 포트 스키마와 일치하지 않습니다. |
| InputParseError | 입력 벡터의 구문 분석에 실패했습니다.  Hello 입력된 벡터에 hello 올바른 개수의 열과 데이터 형식을 확인 합니다.  추가 정보: {0}. |
| MissingRequiredGlobalParameters | Hello 웹 서비스에 필요한 매개 변수가 누락 되어 있습니다. Hello 웹 서비스에서 모든 필요한 hello 매개 변수가 올바른지 확인 하 고 다시 시도 하십시오. |
| UnexpectedParameter | Hello만 필수 hello 웹 서비스에 필요한 매개 변수 전달 되는지 확인 하 고 다시 시도 하십시오. |
| UserParameterInvalid | {0} |
 
## <a name="invalidoperation-http-status-code-400"></a>InvalidOperation(HTTP 상태 코드 400)
 
hello 요청 hello 현재 컨텍스트에서 올바르지 않습니다.
 
| 오류 코드 | 사용자 메시지 |
| ---------- |--------------|
| CannotStartJob | {0} 상태 이므로 hello 작업을 시작할 수 없습니다. |
| IncompatibleModel | hello 모델 hello 요청 버전과 호환 되지 않습니다. hello 요청 버전 단일 datatable 출력 모델을 지원합니다. |
| MultipleInputsNotAllowed | hello 모델에서 여러 입력을 허용 하지 않습니다. |
 
## <a name="libraryexecutionerror-http-status-code-400"></a>LibraryExecutionError(HTTP 상태 코드 400)
 
모듈 실행에 내부 라이브러리 오류가 발생했습니다.
 
 
## <a name="moduleexecutionerror-http-status-code-400"></a>ModuleExecutionError(HTTP 상태 코드 400)
 
모듈 실행에 오류가 발생했습니다.
 
 
## <a name="webservicepackageerror-http-status-code-400"></a>WebServicePackageError(HTTP 상태 코드 400)
 
웹 서비스 패키지가 잘못되었습니다. 제공 하는 hello 웹 서비스 패키지 올바른지 확인 하 고 다시 시도 하십시오.
 
| 오류 코드 | 사용자 메시지 |
| ---------- |--------------|
| FormatError | hello 웹 서비스 패키지 형식이 잘못 되었습니다. 세부 정보: {0} |
| RuntimesError | hello 웹 서비스 패키지 그래프 올바르지 않습니다. 세부 정보: {0} |
| ValidationError | hello 웹 서비스 패키지 그래프 올바르지 않습니다. 세부 정보: {0} |
 
## <a name="unauthorized-http-status-code-401"></a>Unauthorized(HTTP 상태 코드 401)
 
요청은 인증 되지 않은 tooaccess 리소스입니다.
 
| 오류 코드 | 사용자 메시지 |
| ---------- |--------------|
| AdminRequestUnauthorized | 권한 없음 |
| ManagementRequestUnauthorized | 권한 없음 |
| ScoreRequestUnauthorized | 잘못된 자격 증명이 제공되었습니다. |
 
## <a name="notfound-http-status-code-404"></a>NotFound (HTTP 상태 코드 404)
 
리소스를 찾을 수 없습니다.
 
| 오류 코드 | 사용자 메시지 |
| ---------- |--------------|
| ModelPackageNotFound | 모델 패키지를 찾을 수 없습니다. Hello 모델 패키지 Id가 올바른지와 다시 시도 확인 합니다. |
| WebServiceIdNotFoundInWorkspace | 이 작업 영역에서 웹 서비스를 찾을 수 없습니다. Hello webServiceId 및 hello workspaceId 사이 불일치가 있습니다. 제공 하는 hello 웹 서비스는 hello 작업 영역에 포함을 확인 하 고 다시 시도 하십시오. |
| WebServiceNotFound | 웹 서비스를 찾을 수 없습니다. Hello 웹 서비스 Id가 올바른지와 다시 시도 확인 합니다. |
| WorkspaceNotFound | 작업 영역을 찾을 수 없습니다. Hello 작업 영역 Id가 올바른지와 다시 시도 확인 합니다. |
 
## <a name="requesttimeout-http-status-code-408"></a>RequestTimeout(HTTP 상태 코드 408)
 
시간을 허용 하는 hello 내 hello 작업을 완료할 수 없습니다.
 
| 오류 코드 | 사용자 메시지 |
| ---------- |--------------|
| RequestCanceled | 클라이언트 hello에서 요청이 취소 되었습니다. |
| ScoreRequestTimeout | 실행 요청 시간이 초과되었습니다. |
 
## <a name="conflict-http-status-code-409"></a>Conflict(HTTP 상태 코드 409)
 
리소스가 이미 있습니다.
 
| 오류 코드 | 사용자 메시지 |
| ---------- |--------------|
| ModelOutputMetadataMismatch | 출력 매개 변수 이름이 잘못되었습니다. Hello 메타 데이터 편집기 모듈 toorename 열을 사용 하 고 다시 시도 하십시오. |
 
## <a name="memoryquotaviolation-http-status-code-413"></a>MemoryQuotaViolation(HTTP 상태 코드 413)
 
hello 모델 tooit 할당 hello 메모리 할당량을 초과 했습니다.
 
| 오류 코드 | 사용자 메시지 |
| ---------- |--------------|
| OutOfMemoryLimit | hello 모델에 대 한 appropriated가 보다 더 많은 메모리를 사용 합니다. Hello 모델에 대 한 최대 허용된 메모리는 {0} MB입니다. 모델에서 문제를 확인하세요. |
 
## <a name="internalerror-http-status-code-500"></a>InternalError(HTTP 상태 코드 500)
 
실행에 내부 오류가 발생했습니다.
 
| 오류 코드 | 사용자 메시지 |
| ---------- |--------------|
| AdminAuthenticationFailed |  |
| BackendArgumentError |  |
| BackendBadRequest |  |
| ClusterConfigBlobMisconfigured |  |
| ContainerProcessTerminatedWithSystemError | 시스템 오류 hello 컨테이너 프로세스가 손상 |
| ContainerProcessTerminatedWithUnknownError | 알 수 없는 오류 hello 컨테이너 프로세스가 손상 |
| ContainerValidationFailed | Blob 컨테이너 유효성 검사가 {0} 오류로 인해 실패했습니다. |
| DeleteWebServiceResourceFailed |  |
| ExceptionDeserializationError |  |
| FailedGettingApiDocument |  |
| FailedStoringWebService |  |
| InvalidMemoryConfiguration | InvalidMemoryConfiguration, ConfigValue: {0} |
| InvalidResourceCacheConfiguration |  |
| InvalidResourceDownloadConfiguration |  |
| InvalidWebServiceResources |  |
| MissingTaskInstance | 인수가 제공되지 않았습니다. 유효한 인수가 전달되는지 확인하고 다시 시도하세요. |
| ModelPackageInvalid |  |
| ModuleExecutionFailed |  |
| ModuleLoadFailed |  |
| ModuleObjectCloneFailed |  |
| OutputConversionFailed |  |
| PortDataTypeNotSupported | Port id={0}에 지원되지 않는 데이터 형식 {1}이(가) 있습니다. |
| ResourceDownload |  |
| ResourceLoadFailed |  |
| ServiceUrisNotFound |  |
| SwaggerGeneration | Swagger를 생성하지 못했습니다. 세부 정보: {0} |
| UnexpectedScoreStatus |  |
| UnknownBackendErrorResponse |  |
| UnknownError |  |
| UnknownJobStatusCode | 알 수 없는 작업 상태 코드 {0}. |
| UnknownModuleError |  |
| UpdateWebServiceResourceFailed |  |
| WebServiceGroupNotFound |  |
| WebServicePackageInvalid | InvalidWebServicePackage, 세부 정보: {0} |
| WorkerAuthorizationFailed |  |
| WorkerUnreachable |  |
 
## <a name="internalerrorsystemlowonmemory-http-status-code-500"></a>InternalErrorSystemLowOnMemory(HTTP 상태 코드 500)
 
실행에 내부 오류가 발생했습니다. 시스템 메모리가 부족합니다. 나중에 다시 시도하세요.
 
 
## <a name="modelpackageformaterror-http-status-code-500"></a>ModelPackageFormatError(HTTP 상태 코드 500)
 
모델 패키지가 잘못되었습니다. 제공 된 hello 모델 패키지 올바른지 확인 하 고 다시 시도 하십시오.
 
 
## <a name="webservicepackageinternalerror-http-status-code-500"></a>WebServicePackageInternalError(HTTP 상태 코드 500)
 
웹 서비스 패키지가 잘못되었습니다. 제공 된 hello 웹 패키지 올바른지 확인 하 고 다시 시도 하십시오.
 
| 오류 코드 | 사용자 메시지 |
| ---------- |--------------|
| ModuleError | hello 웹 서비스 패키지 그래프 올바르지 않습니다. 세부 정보: {0} |
 
## <a name="initializingcontainers-http-status-code-503"></a>InitializingContainers(HTTP 상태 코드 503)
 
hello 요청 컨테이너를 초기화 하는 hello로 실행할 수 없습니다.
 
 
## <a name="serviceunavailable-http-status-code-503"></a>ServiceUnavailable(HTTP 상태 코드 503)
 
서비스를 일시적으로 사용할 수 없습니다.
 
| 오류 코드 | 사용자 메시지 |
| ---------- |--------------|
| NoMoreResources | 요청에 사용할 수 있는 리소스가 없습니다. |
| RequestThrottled | 요청이 {0} 끝점에 대해 제한되었습니다. hello 끝점에 대 한 최대 동시성 hello {1 \}입니다. |
| TooManyConcurrentRequests | 동시 요청을 너무 많이 보냈습니다. |
| TooManyHostsBeingInitialized | 너무 많은 호스트에서 초기화 되 고 동일한 hello 시간입니다. 제한/다시 시도하는 것이 좋습니다. |
| TooManyHostsBeingInitializedPerModel | 너무 많은 호스트에서 초기화 되 고 동일한 hello 시간입니다. 제한/다시 시도하는 것이 좋습니다. |
 
## <a name="gatewaytimeout-http-status-code-504"></a>GatewayTimeout(HTTP 상태 코드 504)
 
시간을 허용 하는 hello 내 hello 작업을 완료할 수 없습니다.
 
| 오류 코드 | 사용자 메시지 |
| ---------- |--------------|
| BackendInitializationTimeout | 시간을 허용 하는 hello 내 hello 웹 서비스 초기화를 완료할 수 없습니다. |
| BackendScoreTimeout | 시간을 허용 하는 hello 내 hello 웹 서비스 요청 실행을 완료할 수 없습니다. |
 
