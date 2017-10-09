---
title: "aaaAuditing 및 로깅-Microsoft 위협 모델링 도구-Azure | Microsoft Docs"
description: "hello 위협 모델링 도구에에서 노출 위협에 대 한 완화"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: f28988833eba251b6ceb8bbd47cde37e871af609
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-auditing-and-logging--mitigations"></a>보안 프레임: 감사 및 로깅 | 완화 
| 제품/서비스 | 문서 |
| --------------- | ------- |
| **Dynamics CRM**    | <ul><li>[솔루션의 민감한 엔터티를 식별하고 변경 감사 구현](#sensitive-entities)</li></ul> |
| **웹 응용 프로그램** | <ul><li>[감사 및 로깅 hello 응용 프로그램에 적용 되도록](#auditing)</li><li>[로그 회전 및 분리가 작동하는지 확인](#log-rotation)</li><li>[Hello 응용 프로그램 중요 한 사용자 데이터를 기록 하지 않습니다 확인](#log-sensitive-data)</li><li>[감사 및 로그 파일의 액세스 제한](#log-restricted-access)</li><li>[사용자 관리 이벤트 기록](#user-management)</li><li>[Hello 시스템에 있는지 확인 하십시오. 잘못 된 사용에 대 한 기본 제공 된 방어](#inbuilt-defenses)</li><li>[Azure App Service에서 웹앱에 대한 진단 로깅 설정](#diagnostics-logging)</li></ul> |
| **데이터베이스** | <ul><li>[SQL Server에서 로그인 감사를 사용하도록 설정](#identify-sensitive-entities)</li><li>[Azure SQL에서 위협 감지 사용](#threat-detection)</li></ul> |
| **Azure 저장소** | <ul><li>[Azure 저장소의 Azure 저장소 분석 tooaudit 액세스 사용](#analytics)</li></ul> |
| **WCF** | <ul><li>[충분한 로깅 구현](#sufficient-logging)</li><li>[충분한 감사 실패 처리 구현](#audit-failure-handling)</li></ul> |
| **앱 API** | <ul><li>[웹 API에 감사 및 로깅 적용](#logging-web-api)</li></ul> |
| **IoT 필드 게이트웨이** | <ul><li>[필드 게이트웨이에 적절한 감사 및 로깅 적용](#logging-field-gateway)</li></ul> |
| **IoT 클라우드 게이트웨이** | <ul><li>[클라우드 게이트웨이에 적절한 감사 및 로깅 적용](#logging-cloud-gateway)</li></ul> |

## <a id="sensitive-entities"></a>솔루션의 민감한 엔터티를 식별하고 변경 감사 구현

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Dynamics CRM | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계**                   | 솔루션에서 중요한 데이터가 포함된 엔터티를 식별하고 이러한 엔터티 및 필드에 대한 변경 감사 구현 |

## <a id="auditing"></a>감사 및 로깅 hello 응용 프로그램에 적용 되도록

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계**                   | 모든 구성 요소에 감사 및 로깅을 사용하도록 설정합니다. 감사 로그는 사용자 컨텍스트를 캡처해야 합니다. 모든 중요한 이벤트를 식별하고 해당 이벤트를 기록합니다. 중앙 집중식 로깅 구현 |

## <a id="log-rotation"></a>로그 회전 및 분리가 작동하는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계**                   | <p>로그 회전은 날짜가 지정된 로그 파일이 보관되는 시스템 관리에 사용되는 자동화 프로세스입니다. 종종 대규모 응용 프로그램을 실행 하는 서버는 모든 요청을 기록할: 부피가 로그의 hello 과제를 로그 회전은 방식으로 toolimit hello 최근 이벤트 분석 허용 하면서 전체 hello 로그의 크기입니다. </p><p>분리 로그에 서로 다른 파티션 S/응용 프로그램 실행 되 고 있는 순서 tooavert에서 서비스 거부로 로그 파일 공격 또는 응용 프로그램의 성능을 다운 그레이드 환영 toostore 있다고 것을 의미합니다</p>|

## <a id="log-sensitive-data"></a>Hello 응용 프로그램 중요 한 사용자 데이터를 기록 하지 않습니다 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계**                   | <p>사용자가 tooyour 사이트를 제출 한다고 중요 한 데이터를 기록 하지 않습니다 확인 합니다. 의도적 로깅과 설계 문제로 인한 부작용을 확인합니다. 다음은 민감한 데이터의 예입니다.</p><ul><li>사용자 자격 증명</li><li>사회 보장 번호 또는 기타 식별 정보</li><li>신용 카드 번호 또는 기타 금융 정보</li><li>의료 정보</li><li>개인 키 또는 toodecrypt 사용된 될 수 있는 데이터를 다른 암호화 된 정보</li><li>사용할 수 있는 시스템 또는 응용 프로그램 정보 toomore hello 응용 프로그램을 효과적으로 공격</li></ul>|

## <a id="log-restricted-access"></a>감사 및 로그 파일의 액세스 제한

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계**                   | <p>Tooensure 액세스 권한 toolog 파일은 적절 하 게 설정 확인 합니다. 응용 프로그램 계정은 쓰기 전용 액세스만 가능해야 하고 운영자 및 고객 지원 담당자는 필요에 따라 읽기 전용 액세스만 가능해야 합니다.</p><p>관리자 계정은 되 대 한 모든 권한을 포함 해야 하는 hello 유일한 계정입니다. 로그에 Windows ACL 파일 tooensure 제대로 제한 되는지 확인 합니다.</p><ul><li>응용 프로그램 계정은 쓰기 전용 액세스만 가능해야 함</li><li>운영자 및 고객 지원 담당자는 필요에 따라 읽기 전용 액세스만 가능해야 함</li><li>관리자는 전체 액세스 권한이 있는 계정만 hello</li></ul>|

## <a id="user-management"></a>사용자 관리 이벤트 기록

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계**                   | <p>예: 성공 및 실패 한 사용자 로그인 사용자 관리 이벤트를 모니터링 하는 hello 응용 프로그램, 암호 재설정, 암호 변경, 계정 잠금, 사용자 등록을 확인 합니다. 이 작업을 수행 toodetect 주며 toopotentially 의심 스러운 동작을 대응 합니다. 해줍니다 toogather 작업 데이터를입니다. 예를 들어, tootrack hello 응용 프로그램에 액세스 하는</p>|

## <a id="inbuilt-defenses"></a>Hello 시스템에 있는지 확인 하십시오. 잘못 된 사용에 대 한 기본 제공 된 방어

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계**                   | <p>응용 프로그램이 잘못 사용될 경우 보안 예외를 throw하는 컨트롤이 작동해야 합니다. 예를 들어, 입력된 유효성 검사에에서는 공격자가 악성 코드가 hello 정규식과 일치 하지 않는 tooinject 시도 하는 경우 보안 예외가 throw 될 수는 시스템 오용을 알려 줍니다 될 수 있습니다.</p><p>예를 들어 toohave 보안 예외를 기록 및 될 hello에 대 한 조치 좋습니다.</p><ul><li>입력 유효성 검사</li><li>CSRF 위반</li><li>무차별 암호 대입(리소스당 사용자별 요청 수에 대한 상한)</li><li>파일 업로드 위반</li><ul>|

## <a id="diagnostics-logging"></a>Azure App Service에서 웹앱에 대한 진단 로깅 설정

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | EnvironmentType - Azure |
| **참조**              | 해당 없음  |
| **단계** | <p>Azure 응용 프로그램 서비스를 디버깅 합니다. 기본 제공 진단 tooassist 웹 응용 프로그램을 제공 합니다. TooAPI 앱 및 모바일 앱에도 적용 됩니다. 앱 서비스 웹 앱 hello 웹 서버와 hello 웹 응용 프로그램에서 로깅 정보에 대 한 진단 기능을 제공 합니다.</p><p>이는 논리적으로 웹 서버 진단 및 응용 프로그램 진단으로 구분됩니다.</p>|

## <a id="identify-sensitive-entities"></a>SQL Server에서 로그인 감사를 사용하도록 설정

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 데이터베이스 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [로그인 감사 구성](https://msdn.microsoft.com/library/ms175850.aspx) |
| **단계** | <p>데이터베이스 서버 로그인 감사 암호 추측 공격 활성화 toodetect/확인 해야 합니다. Toocapture 실패 한 로그인 시도 유용 합니다. 성공한 로그인 시도와 실패한 로그인 시도를 모두 캡처하면 법정 조사 시 추가적인 이점이 있습니다.</p>|

## <a id="threat-detection"></a>Azure SQL에서 위협 감지 사용

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 데이터베이스 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | SQL Azure |
| **특성**              | SQL 버전 - V12 |
| **참조**              | [SQL Database 위협 감지 시작](https://azure.microsoft.com/documentation/articles/sql-database-threat-detection-get-started/)|
| **단계** |<p>위협 검색 잠재적 보안 위협을 toohello 데이터베이스 비정상 데이터베이스 작업을 검색 합니다. 새 고객 toodetect 있고 비정상적인 활동에서 보안 경고를 제공 하 여 발생 하는 대로 toopotential 위협 응답을 보안 계층을 제공 합니다.</p><p>사용자가 Azure SQL 데이터베이스 감사 toodetermine는 시도 tooaccess에서 발생 한 경우 위반을 사용 하 여 hello 의심 스러운 이벤트를 탐색 하거나 hello 데이터베이스의에서 데이터를 이용할 수 있습니다.</p><p>위협 요소 탐지 하면 간단한 tooaddress 잠재적인 위협 toohello 데이터베이스 없이 hello 필요 toobe 보안 전문가 또는 시스템 모니터링 하는 고급 보안 관리</p>|

## <a id="analytics"></a>Azure 저장소의 Azure 저장소 분석 tooaudit 액세스 사용

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure 저장소 | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음 |
| **참조**              | [Storage Analytics toomonitor 권한 부여 유형을 사용 하 여](https://azure.microsoft.com/documentation/articles/storage-security-guide/#storage-analytics) |
| **단계** | <p>각 저장소 계정에 대 한 Azure 저장소 분석 tooperform 로깅을 사용 하도록 설정 및 메트릭 데이터를 저장할 수 있습니다 하나입니다. hello 저장소 분석 로그 저장소에 액세스할 때 사용자가 사용 된 인증 방법 같은 중요 한 정보를 제공 합니다.</p><p>이 액세스 toostorage 호위 밀접 하 게 하는 경우에 매우 유용할 수 있습니다. 예를 들어 Blob 저장소에 모든 hello 컨테이너 tooprivate를 hello를 사용 하 여 SAS 서비스의 응용 프로그램 전체 구현 합니다. 다음 보안 위반을 나타낼 수 있습니다, hello 저장소 계정 키를 사용 하 여 blob 액세스 되는 경우 또는 hello blob는 공용 이지만 되지 않아야 하는 경우 hello 기록 toosee 정기적으로 검사할 수 있습니다.</p>|

## <a id="sufficient-logging"></a>충분한 로깅 구현

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | WCF | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | .NET Framework |
| **특성**              | 해당 없음  |
| **참조**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify, 영국](https://vulncat.fortify.com/en/vulncat/index.html) |
| **단계** | <p>보안 문제가 발생 한 후 적절 한 감사 내역의 hello 부족 법정 노력에 방해가 될 수 있습니다. Windows Communication Foundation (WCF) hello 기능 toolog 성공 또는 실패 한 인증 시도 제공합니다.</p><p>실패한 인증 시도를 기록하면 관리자에게 무차별 암호 대입 공격 가능성을 경고할 수 있습니다. 마찬가지로, 성공한 인증 이벤트를 기록하면 합법적 계정이 손상될 때 유용한 감사 추적을 제공할 수 있습니다. WCF의 서비스 보안 감사 기능을 사용하도록 설정 |

### <a name="example"></a>예제
hello 다음은 사용 하도록 설정 하는 포함 하는 예제 구성
```
<system.serviceModel>
    <behaviors>
        <serviceBehaviors>
            <behavior name=""NewBehavior"">
                <serviceSecurityAudit auditLogLocation=""Default""
                suppressAuditFailure=""false"" 
                serviceAuthorizationAuditLevel=""SuccessAndFailure""
                messageAuthenticationAuditLevel=""SuccessAndFailure"" />
                ...
            </behavior>
        </servicebehaviors>
    </behaviors>
</system.serviceModel>
```

## <a id="audit-failure-handling"></a>충분한 감사 실패 처리 구현

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | WCF | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | .NET Framework |
| **특성**              | 해당 없음  |
| **참조**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify, 영국](https://vulncat.fortify.com/en/vulncat/index.html) |
| **단계** | <p>초기에 개발 된 솔루션은 구성 toogenerate toowrite tooan 감사 로그 실패 시 예외를 발생 하지 않습니다. WCF 구성 된 경우 toothrow 예외가 없습니다 toowrite tooan 감사 로그는 hello 프로그램 hello 오류의 알리지 것입니다 하 고 중요 한 보안 이벤트 감사는 발생 하지 않을 수 없습니다.</p>|

### <a name="example"></a>예제
hello `<behavior/>` 아래 hello WCF 구성 파일의 요소에 WCF 지시 toonot WCF toowrite tooan 감사 로그 실패 시 hello 응용 프로그램을 알립니다.
````
<behaviors>
    <serviceBehaviors>
        <behavior name="NewBehavior">
            <serviceSecurityAudit auditLogLocation="Application"
            suppressAuditFailure="true"
            serviceAuthorizationAuditLevel="Success"
            messageAuthenticationAuditLevel="Success" />
        </behavior>
    </serviceBehaviors>
</behaviors>
````
없습니다 toowrite tooan 감사 로그는 WCF toonotify hello 프로그램을 구성 합니다. hello 프로그램 감사 내역은 유지 되는 위치 tooalert hello 조직에서 대체 알림 구성표인이 있어야 합니다. 

## <a id="logging-web-api"></a>웹 API에 감사 및 로깅 적용

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Web API | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 웹 API에서 감사 및 로깅을 사용하도록 설정합니다. 감사 로그는 사용자 컨텍스트를 캡처해야 합니다. 모든 중요한 이벤트를 식별하고 해당 이벤트를 기록합니다. 중앙 집중식 로깅 구현 |

## <a id="logging-field-gateway"></a>필드 게이트웨이에 적절한 감사 및 로깅 적용

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | IoT 필드 게이트웨이 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | <p>여러 장치 tooa 필드 게이트웨이 연결 하는 경우 연결 시도 및 개별 장치에 대 한 인증 상태 (성공 또는 실패)이 기록 되 고 필드 게이트웨이 hello에 유지 관리를 확인 합니다.</p><p>또한 필드 게이트웨이 hello 유지 하는 경우에 IoT Hub 자격 증명을 개별 장치에 대 한, 이러한 자격 증명을 검색 하는 경우 감사 수행 있는지 확인 합니다. 프로세스 tooperiodically 업로드 hello 로그 tooAzure IoT Hub/저장소 장기 보존에 대 한 개발 합니다.</p> |

## <a id="logging-cloud-gateway"></a>클라우드 게이트웨이에 적절한 감사 및 로깅 적용

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | IoT 클라우드 게이트웨이 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [소개 tooIoT 허브 작업 모니터링](https://azure.microsoft.com/documentation/articles/iot-hub-operations-monitoring/) |
| **단계** | <p>IoT Hub 작업 모니터링을 통해 모은 감사 데이터를 수집하고 저장하도록 설계합니다. 다음 모니터링 범주 hello 사용:</p><ul><li>장치 ID 작업</li><li>장치-클라우드 통신</li><li>클라우드-장치 통신</li><li>연결</li><li>파일 업로드</li></ul>|
