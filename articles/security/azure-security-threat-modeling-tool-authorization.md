---
title: "-Microsoft 위협 모델링 도구-aaaAuthorization Azure | Microsoft Docs"
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
ms.openlocfilehash: 3ea7ae2b46baa8578e574e6006b98dfe172829e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-authorization--mitigations"></a>보안 프레임: 권한 부여 | 완화 
| 제품/서비스 | 문서 |
| --------------- | ------- |
| **컴퓨터 신뢰 경계** | <ul><li>[적절 한 Acl hello 장치에 구성 된 toorestrict 무단 액세스 toodata 되는지 확인](#acl-restricted-access)</li><li>[사용자 고유의 중요한 응용 프로그램 콘텐츠가 사용자 프로필 디렉터리에 저장되는지 확인](#sensitive-directory)</li><li>[배포 된 hello 응용 프로그램이 최소 권한으로 실행 확인](#deployed-privileges)</li></ul> |
| **웹 응용 프로그램** | <ul><li>[비즈니스 논리 흐름을 처리할 때 순차적 단계 순서 적용](#sequential-logic)</li><li>[속도 제한 메커니즘 tooprevent 열거형을 구현 합니다.](#rate-enumeration)</li><li>[적절한 권한이 부여되고 최소 권한의 원칙이 준수되는지 확인](#principle-least-privilege)</li><li>[들어오는 요청 매개 변수를 기반으로 하지 않는 비즈니스 논리 및 리소스 액세스 권한 부여 결정](#logic-request-parameters)</li><li>[강제 검색을 통해 콘텐츠와 리소스를 열거하거나 액세스할 수 없는지 확인](#enumerable-browsing)</li></ul> |
| **데이터베이스** | <ul><li>[최소 권한의 계정을 사용 하는 tooconnect tooDatabase 서버 인지 확인](#privileged-server)</li><li>[다른 사용자의 데이터에 액세스 하지 못하도록 RLS 행 수준 보안 tooprevent 테 넌 트를 구현 합니다.](#rls-tenants)</li><li>[유효한 필수 사용자에게만 부여되는 sysadmin 역할](#sysadmin-users)</li></ul> |
| **IoT 클라우드 게이트웨이** | <ul><li>[TooCloud 게이트웨이 연결 최소 권한 토큰을 사용 하 여](#cloud-least-privileged)</li></ul> |
| **Azure 이벤트 허브** | <ul><li>[송신 전용 권한 SAS 키를 사용하여 장치 토큰 생성](#sendonly-sas)</li><li>[직접 액세스 toohello 이벤트 허브를 제공 하는 액세스 토큰을 사용 하지 마십시오](#access-tokens-hub)</li><li>[연결 하는 hello 필요한 최소 사용 권한 SAS를 사용 하 여 허브 키 tooEvent](#sas-minimum-permissions)</li></ul> |
| **Azure Document DB** | <ul><li>[리소스 토큰 tooconnect tooDocumentDB 가능 하면 항상 사용 합니다.](#resource-docdb)</li></ul> |
| **Azure 신뢰 경계** | <ul><li>[세분화 된 액세스 관리 tooAzure 구독을 사용 하도록 설정 RBAC를 사용 하 여](#grained-rbac)</li></ul> |
| **Service Fabric 신뢰 경계** | <ul><li>[RBAC를 사용 하 여 클라이언트의 액세스 toocluster 작업 제한](#cluster-rbac)</li></ul> |
| **Dynamics CRM** | <ul><li>[보안 모델링 수행 및 필요한 경우 필드 수준 보안 사용](#modeling-field)</li></ul> |
| **Dynamics CRM 포털** | <ul><li>[염두에서에 두고 해당 hello 보안 모델 CRM hello 나머지에서와 다른 hello 포털에 대 한 포털 계정의 보안 모델링을 수행 합니다.](#portal-security)</li></ul> |
| **Azure 저장소** | <ul><li>[Azure Table Storage의 엔터티 범위에 대해 세분화된 권한 부여](#permission-entities)</li><li>[Azure 리소스 관리자를 사용 하 여 역할 기반 액세스 제어 (RBAC) tooAzure 저장소 계정을 사용 하도록 설정](#rbac-azure-manager)</li></ul> |
| **모바일 클라이언트** | <ul><li>[암시적 무단 해제 또는 루팅 검색 구현](#rooting-detection)</li></ul> |
| **WCF** | <ul><li>[WCF - 약한 클래스 참조](#weak-class-wcf)</li><li>[WCF - 권한 부여 제어 구현](#wcf-authz)</li></ul> |
| **앱 API** | <ul><li>[ASP.NET Web API에서 적절한 권한 부여 메커니즘 구현](#authz-aspnet)</li></ul> |
| **IoT 장치** | <ul><li>[여러 권한 수준이 필요로 하는 다양 한 작업을 지 원하는 경우 hello 장치에서 인증 검사를 수행](#device-permission)</li></ul> |
| **IoT 필드 게이트웨이** | <ul><li>[필드 게이트웨이 hello에 다른 사용 권한 수준이 필요로 하는 다양 한 작업을 지 원하는 경우 인증 검사를 수행](#field-permission)</li></ul> |

## <a id="acl-restricted-access"></a>적절 한 Acl hello 장치에 구성 된 toorestrict 무단 액세스 toodata 되는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 컴퓨터 신뢰 경계 | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 적절 한 Acl hello 장치에 구성 된 toorestrict 무단 액세스 toodata 되는지 확인|

## <a id="sensitive-directory"></a>사용자 고유의 중요한 응용 프로그램 콘텐츠가 사용자 프로필 디렉터리에 저장되는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 컴퓨터 신뢰 경계 | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 사용자 고유의 중요한 응용 프로그램 콘텐츠가 사용자 프로필 디렉터리에 저장되는지 확인합니다. 이 hello의 여러 사용자가 다른 사용자의 데이터에 액세스 하지 못하도록 컴퓨터 tooprevent입니다.|

## <a id="deployed-privileges"></a>배포 된 hello 응용 프로그램이 최소 권한으로 실행 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 컴퓨터 신뢰 경계 | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 배포 된 hello 응용 프로그램이 최소 권한으로 실행 될 것을 확인 합니다. |

## <a id="sequential-logic"></a>비즈니스 논리 흐름을 처리할 때 순차적 단계 순서 적용

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | Tooverify tooenforce hello 응용 프로그램 tooonly 프로세스 비즈니스 논리 흐름 순차 단계 순서로 현실적인 휴먼 시간 내에 처리 중인 모든 단계를 통해을 순서 대로 처리할 정품 사용자가이 단계를 통해 실행 된 순서 대로 생략 단계 처리 단계를 다른 사용자 로부터 또는 너무 빨리 트랜잭션을 제출 합니다.|

## <a id="rate-enumeration"></a>속도 제한 메커니즘 tooprevent 열거형을 구현 합니다.

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 중요한 식별자가 임의적인 식별자인지 확인합니다. 익명 페이지에 대해 CAPTCHA 제어를 구현합니다. 오류 및 예외로 인해 특정 데이터가 표시되지 않아야 합니다.|

## <a id="principle-least-privilege"></a>적절한 권한이 부여되고 최소 권한의 원칙이 준수되는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | <p>hello 원칙 사용자 계정 필수 toothat 사용자 작업에는 권한 부여를 의미 합니다. 예를 들어 backup 사용자 tooinstall 소프트웨어가 필요 하지 않습니다: 따라서 hello 백업 사용자에 게 권한을 toorun 백업 및 백업 관련 응용 프로그램입니다. 새 소프트웨어 설치와 같은 다른 모든 권한은 차단됩니다. hello 원칙이 적용 됩니다도 tooa 개인용 컴퓨터 사용자에 게 일반적으로 일반 사용자 계정에서 작동 하 고, 권한 있는 암호로 보호 된 계정 (즉, superuser) 열립니다만 경우 hello 반드시 필요한 상황 것입니다. </p><p>이 원칙 적용된 tooyour 웹 응용 프로그램 일 수도 있습니다. 대신 세션을 사용 하 여 역할 기반 인증 방법에 따라 전적으로 대신 원하는 tooassign 데이터베이스 기반 인증 시스템을 통해 toousers 권한입니다. 여전히 hello 사용자가 로그인 올바르게 이제만 hello 시스템에 권한 있는 tooperform 할당 그 권한 tooverify와 그는 작업 특정 역할과 해당 사용자를 할당 하는 대신 순서 tooidentify에서 세션에 사용 합니다. 또한 사용자에 게 toobe hello 할당 hello 세션 있는 먼저 tooexpire에 종속 되지 않는 변경 내용을 hello 신속 하 게 적용 됩니다 권한이 할당 될 때마다이 메서드의 큰 pro가 됩니다.</p>|

## <a id="logic-request-parameters"></a>들어오는 요청 매개 변수를 기반으로 하지 않는 비즈니스 논리 및 리소스 액세스 권한 부여 결정

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 사용자가 제한 된 tooreview 있는지 여부를 확인 될 때마다 특정 데이터를 제한 해야 하는 hello 액세스 서버 쪽 처리. hello userID 로그인에 대 한 세션 변수 안에 저장 해야 하 고 hello 데이터베이스에서 사용자 데이터를 사용 하는 tooretrieve 여야 합니다. |

### <a name="example"></a>예제
```SQL
SELECT data 
FROM personaldata 
WHERE userID=:id < - session var 
```
이제 가능한 공격자 하지 조작 하 고 변경할 수 hello 응용 프로그램 작업을 hello 식별자 hello 데이터를 검색 하기 위한 처리 서버 쪽입니다.

## <a id="enumerable-browsing"></a>강제 검색을 통해 콘텐츠와 리소스를 열거하거나 액세스할 수 없는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | <p>Hello 웹 루트에 중요 한 정적 및 구성 파일을 유지 되어야 합니다. 콘텐츠 필요 없음 toobe 공용에 대 한 제어를 적용 해야 하는 적절 한 액세스 또는 hello 제거 콘텐츠 자체입니다.</p><p>또한 강제 검색은 일반적으로 정보와 함께 취합 무작위 기술을 toogather tooaccess 시도 하 여 가능한 tooenumerate 디렉터리, 파일 서버의 Url. 공격자는 일반적으로 존재하는 파일의 모든 변형을 검사할 수 있습니다. 예를 들어 암호 파일 검색에는 passwd.txt, password.htm, password.dat 및 다른 변형 파일 등이 포함됩니다.</p><p>시도 toomitigate이 무작위를 감지 하기 위한 기능을 포함 해야 합니다.</p>|

## <a id="privileged-server"></a>최소 권한의 계정을 사용 하는 tooconnect tooDatabase 서버 인지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 데이터베이스 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [SQL Database 권한 계층](https://msdn.microsoft.com/library/ms191465), [SQL 데이터베이스 보안 개체](https://msdn.microsoft.com/library/ms190401) |
| **단계** | 최소 권한의 계정을 사용 하는 tooconnect toohello 데이터베이스 이어야 합니다. 응용 프로그램 로그인 hello 데이터베이스의 제한 해야 하며 선택한 저장된 프로시저에만 실행 해야 합니다. 응용 프로그램응용 프로그램의 로그인에는 직접적인 테이블 액세스가 없어야 합니다. |

## <a id="rls-tenants"></a>다른 사용자의 데이터에 액세스 하지 못하도록 RLS 행 수준 보안 tooprevent 테 넌 트를 구현 합니다.

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 데이터베이스 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | SQL Azure, 온-프레미스 |
| **특성**              | SQL 버전 - V12, SQL 버전 - MsSQL2016 |
| **참조**              | [SQL Server RLS(행 수준 보안)](https://msdn.microsoft.com/library/azure/dn765131.aspx) |
| **단계** | <p>행 수준 보안 (예:: 그룹 멤버십 또는 실행 컨텍스트) 쿼리를 실행 하는 hello 사용자의 hello 특성에 따라 데이터베이스 테이블에서 고객 toocontrol 액세스 toorows를 수 있습니다.</p><p>행 수준 보안 (RLS) hello 설계 및 응용 프로그램의 보안 코딩을 간소화 합니다. RLS 사용 하면 데이터 행 액세스에 tooimplement 제한 사항이 있습니다. 예를 들어 작업 자가 관련 tootheir 부서는 데이터 행만 액세스할 수 있는지를 확인 하거나 고객의 데이터 액세스 tooonly hello 데이터 관련 tootheir 회사를 제한 합니다.</p><p>hello 액세스 제한 논리는 hello 데이터베이스 계층에서 다소 떨어진 위치에서 다른 응용 프로그램 계층의 hello 데이터는 합니다. hello 데이터베이스 시스템은 모든 계층에서 데이터 액세스를 시도할 때마다 hello 액세스를 제한 합니다. 그러면 hello 보안 시스템이 더 안정적이 고 강력한 hello hello 보안 시스템의 노출 영역 줄이기 합니다.</p><p>|

참고 적용 가능한 유일한 tooSQL 2016을 시작 하는 서버 및 Azure SQL 데이터베이스의 기본 데이터베이스 기능으로 해당 RLS는 합니다. Hello 기본적으로 RLS 기능이 구현 되지 않은 경우 그 해야 보장할 수 데이터를 제한 된 사용 하 여 뷰 및 프로시저

## <a id="sysadmin-users"></a>유효한 필수 사용자에게만 부여되는 sysadmin 역할

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 데이터베이스 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [SQL Database 권한 계층](https://msdn.microsoft.com/library/ms191465), [SQL 데이터베이스 보안 개체](https://msdn.microsoft.com/library/ms190401) |
| **단계** | Hello SysAdmin 고정 서버 역할의 멤버는 매우 제한 되어야 하 고 응용 프로그램에서 사용 되는 계정을 포함 해야 합니다.  Hello hello 역할의 사용자 목록을 검토 하 고 불필요 한 계정을 제거 하십시오|

## <a id="cloud-least-privileged"></a>TooCloud 게이트웨이 연결 최소 권한 토큰을 사용 하 여

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | IoT 클라우드 게이트웨이 | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 게이트웨이 선택 - Azure IoT Hub |
| **참조**              | [Iot Hub 액세스 제어](https://azure.microsoft.com/documentation/articles/iot-hub-devguide/#Security) |
| **단계** | 최소 권한 tooCloud (IoT 허브) 게이트웨이 연결 하는 권한을 toovarious 구성 요소를 제공 합니다. 일반적인 예로 장치 관리/프로비전 구성 요소는 레지스트리 읽기/쓰기를 사용하고, 이벤트 프로세서(ASA)는 서비스 연결을 사용합니다. 개별 장치는 장치 자격 증명을 사용하여 연결합니다.|

## <a id="sendonly-sas"></a>송신 전용 권한 SAS 키를 사용하여 장치 토큰 생성

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure Event Hub | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [Event Hubs 인증 및 보안 모델 개요](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **단계** | SAS 키는 toogenerate 사용 되는 개별 장치 토큰입니다. 지정된 된 게시자에 대 한 hello 장치 토큰을 생성 하는 동안 보내기 전용 권한을 SAS 키를 사용 하 여|

## <a id="access-tokens-hub"></a>직접 액세스 toohello 이벤트 허브를 제공 하는 액세스 토큰을 사용 하지 마십시오

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure Event Hub | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [Event Hubs 인증 및 보안 모델 개요](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **단계** | Toohello 이벤트 허브에 직접 액세스를 부여 하는 토큰 toohello 장치를 부여 하지 않아야 합니다. 유일한 tooa 게시자 식별 하 고 블랙 리스트에 추가 하는 경우 도움이 될 액세스를 제공 하는 hello 장치에 대 한 최소 권한이 지정 된 토큰을 사용 하는 rogue toobe를 찾을 수 또는 장치를 손상 합니다.|

## <a id="sas-minimum-permissions"></a>연결 하는 hello 필요한 최소 사용 권한 SAS를 사용 하 여 허브 키 tooEvent

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure Event Hub | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [Event Hubs 인증 및 보안 모델 개요](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **단계** | 최소 권한 toohello 이벤트 허브를 연결 하는 권한을 toovarious 백 엔드 응용 프로그램을 제공 합니다. 각 백 엔드 응용 프로그램에 대 한 별도 SAS 키를 생성 하 고 hello 필요한 사용 권한-송신, 수신 또는 관리 toothem 제공 합니다.|

## <a id="resource-docdb"></a>리소스 토큰 tooconnect tooCosmos 가능 DB를 사용 하 여

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure Document DB | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 리소스 토큰은 DocumentDB 사용 권한 리소스에 연결 하 고 캡처 hello 간의 관계는 특정 DocumentDB 응용 프로그램 리소스 (예: 컬렉션, 문서)에 대 한 해당 사용자에 게 데이터베이스 및 hello 권한의 hello 사용자입니다. 클라이언트 hello 모바일 또는 데스크톱 클라이언트와 같은 최종 사용자 응용 프로그램 같은 마스터 또는 읽기 전용 키-처리와 신뢰할 수 없는 경우 리소스 토큰 tooaccess hello DocumentDB를 항상 사용 합니다. 마스터 키 또는 이러한 키를 안전 하 게 저장할 수 있는 백 엔드 응용 프로그램에서 읽기 전용 키를 사용 합니다.|

## <a id="grained-rbac"></a>세분화 된 액세스 관리 tooAzure 구독을 사용 하도록 설정 RBAC를 사용 하 여

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure 신뢰 경계 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [역할 할당 toomanage tooyour Azure 구독의 리소스에 액세스를 사용 하 여](https://azure.microsoft.com/documentation/articles/role-based-access-control-configure/)  |
| **단계** | Azure RBAC(역할 기반 액세스 제어)를 통해 Azure에 대한 세밀한 액세스 관리가 가능합니다. RBAC를 사용 하 여 권한을 부여할 수 있습니다만 hello 제한 된 액세스 사용자를에 tooperform 업무를 필요 합니다.|

## <a id="cluster-rbac"></a>RBAC를 사용 하 여 클라이언트의 액세스 toocluster 작업 제한

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Service Fabric 트러스트 경계 | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 환경 - Azure |
| **참조**              | [Service Fabric 클라이언트용 역할 기반 액세스 제어](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security-roles/) |
| **단계** | <p>Azure 서비스 패브릭 연결된 tooa 서비스 패브릭 클러스터에 있는 클라이언트에 대 한 두 개의 서로 다른 액세스 제어 유형을 지원: 관리자와 사용자입니다. 액세스 제어 작업을 허용 hello 클러스터 관리자 toolimit 액세스 toocertain 클러스터 hello 클러스터를 보안 하는 사용자의 다른 그룹에 대 한 합니다.</p><p>관리자에 대 한 모든 권한을 toomanagement 기능 (읽기/쓰기 기능만 포함)가 있습니다. 사용자가 기본적으로 읽기 액세스 toomanagement 기능 (예: 쿼리 기능) 및 hello 기능 tooresolve 응용 프로그램 및 서비스입니다.</p><p>각각에 대해 별도 인증서를 제공 하 여 클러스터 생성 hello 시 hello 두 클라이언트 역할 (관리자 및 클라이언트)을 지정 합니다.</p>|

## <a id="modeling-field"></a>보안 모델링 수행 및 필요한 경우 필드 수준 보안 사용

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Dynamics CRM | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 보안 모델링을 수행하고 필요한 경우 필드 수준 보안을 사용합니다.|

## <a id="portal-security"></a>염두에서에 두고 해당 hello 보안 모델 CRM hello 나머지에서와 다른 hello 포털에 대 한 포털 계정의 보안 모델링을 수행 합니다.

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Dynamics CRM 포털 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 염두에서에 두고 해당 hello 보안 모델 CRM hello 나머지에서와 다른 hello 포털에 대 한 포털 계정의 보안 모델링을 수행 합니다.|

## <a id="permission-entities"></a>Azure Table Storage의 엔터티 범위에 대해 세분화된 권한 부여

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure 저장소 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | StorageType - 테이블 |
| **참조**              | [Toodelegate tooobjects SAS를 사용 하 여 Azure 저장소 계정에 액세스 하는 방법](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_data-plane-security) |
| **단계** | 특정 비즈니스 시나리오에서 Azure 테이블 저장소는 toodifferent 당사자는 필요한 toostore 중요 한 데이터를 수 있습니다. 예를 들어, 중요 한 관련 된 데이터 toodifferent 국가입니다. 이러한 경우 사용자가 데이터 특정 tooa 특정 국가 액세스할 수 있도록 SAS 서명을 hello 파티션 및 행 키 범위를 지정 하 여 생성할 수 있습니다.| 

## <a id="rbac-azure-manager"></a>Azure 리소스 관리자를 사용 하 여 역할 기반 액세스 제어 (RBAC) tooAzure 저장소 계정을 사용 하도록 설정

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure 저장소 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [어떻게 toosecure 저장소 계정을 역할 기반 액세스 제어 (RBAC)](https://azure.microsoft.com/documentation/articles/storage-security-guide/#management-plane-security) |
| **단계** | <p>새 저장소 계정을 만들 때 클래식 배포 모델 또는 Azure Resource Manager 배포 모델 중에서 선택합니다. Azure의 리소스를 만드는 hello 클래식 모델 전부 아니면 전무 액세스 toohello 구독을 허용 및 저장소 계정을 차례로 hello 합니다.</p><p>Hello Azure 리소스 관리자, 모델로 hello 저장소 계정 리소스 그룹 및 컨트롤 액세스 toohello 관리 평면에서 Azure Active Directory를 사용 하 여 해당 특정 저장소 계정의 넣을 있습니다. 예를 들어 사용자 제공할 수 있습니다 특정 hello 기능 tooaccess hello 저장소 계정 키를 다른 사용자가 hello 저장소 계정에 대 한 정보를 볼 수 있지만 hello 저장소 계정 키에 액세스할 수 없습니다.</p>|

## <a id="rooting-detection"></a>암시적 무단 해제 또는 루팅 검색 구현

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 모바일 클라이언트 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | <p>휴대폰이 루팅되거나 무단 해제되는 경우 응용 프로그램에서 자체 구성 및 사용자 데이터를 보호해야 합니다. 루팅/무단 해제는 일반 사용자가 자신의 휴대폰에서 수행하지 않는 무단 액세스를 의미합니다. 따라서 응용 프로그램 응용 프로그램 시작 시 hello 전화 루 팅 되었는지 경우 toodetect 암시적 검색 논리가 있어야 합니다.</p><p>hello 검색 논리 예를 들어 일반적으로 유일한 루트 사용자는 액세스할 수 있습니다. 파일 단순히 액세스 될 수 있습니다.:</p><ul><li>/system/app/Superuser.apk</li><li>/sbin/su</li><li>/system/bin/su</li><li>/system/xbin/su</li><li>/data/local/xbin/su</li><li>/data/local/bin/su</li><li>/system/sd/xbin/su</li><li>/system/bin/failsafe/su</li><li>/data/local/su</li></ul><p>Hello 응용 프로그램 수 이러한 파일에 액세스할 경우 hello 응용 프로그램 루트 사용자로 실행 되 고 있는지를 나타냅니다.</p>|

## <a id="weak-class-wcf"></a>WCF - 약한 클래스 참조

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | WCF | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반, .NET Framework 3 |
| **특성**              | 해당 없음  |
| **참조**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify, 영국](https://vulncat.fortify.com/en/vulncat/index.html) |
| **단계** | <p>hello 시스템 침입자 무단 tooexecute 코드 하는 약한 클래스 참조를 사용 합니다. hello 프로그램 고유 하 게 확인 되지 않은 사용자 정의 클래스를 참조 합니다. .NET이 약하게 식별 된 클래스 hello CLR 형식 로더 hello 클래스 다음 hello에 위치 하는 hello에 대 한 로드 될 때 순서를 지정 합니다.</p><ol><li>Hello 로더 검색 구성 파일의 리디렉션 위치, GAC, hello 현재 어셈블리 구성 정보를 사용 하 여 hello 및 응용 프로그램 기본 디렉터리 hello hello 형식의 hello 어셈블리를 알 경우</li><li>현재 어셈블리, mscorlib 및 hello TypeResolve 이벤트 처리기가 반환 하는 hello 위치 hello 로더 검색 hello hello 어셈블리를 알 수 없는 경우</li><li>형식 전달 메커니즘 hello 같은 후크로 hello AppDomain.TypeResolve 이벤트와 CLR 검색 순서를 수정할 수 있습니다.</li></ol><p>만들어 hello CLR 검색 순서를 이용 하는 경우 동일한 이름 및 해당 hello CLR가 먼저 로드 대체 위치에 배치 된 대체 클래스 hello, CLR hello hello 공격자가 제공한 코드를 실행할 의도 하지 않게 됩니다.</p>|

### <a name="example"></a>예제
hello `<behaviorExtensions/>` 아래의 hello WCF 구성 파일의 요소에는 WCF tooadd 사용자 지정 동작 클래스 tooa 특정 WCF 확장 하도록 지시 합니다.
```
<system.serviceModel>
    <extensions>
        <behaviorExtensions>
            <add name=""myBehavior"" type=""MyBehavior"" />
        </behaviorExtensions>
    </extensions>
</system.serviceModel>
```
정규화된(강력한) 이름을 사용하면 형식을 고유하게 식별하고 시스템 보안을 더욱 강화할 수 있습니다. Hello machine.config와 app.config 파일에서 형식을 등록할 때는 정규화 된 어셈블리 이름을 사용 합니다.

### <a name="example"></a>예제
hello `<behaviorExtensions/>` 아래의 hello WCF 구성 파일의 요소에는 WCF tooadd 강력 하 게 참조 된 사용자 지정 동작 클래스 tooa 특정 WCF 확장 하도록 지시 합니다.
```
<system.serviceModel>
    <extensions>
        <behaviorExtensions>
            <add name=""myBehavior"" type=""Microsoft.ServiceModel.Samples.MyBehaviorSection, MyBehavior,
            Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"" />
        </behaviorExtensions>
    </extensions>
</system.serviceModel>
```

## <a id="wcf-authz"></a>WCF - 권한 부여 제어 구현

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | WCF | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반, .NET Framework 3 |
| **특성**              | 해당 없음  |
| **참조**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify, 영국](https://vulncat.fortify.com/en/vulncat/index.html) |
| **단계** | <p>이 서비스는 권한 부여 제어를 사용하지 않습니다. 클라이언트가 특정 WCF 서비스를 호출 하면 WCF hello 호출자에 게 hello 서버에 권한 tooexecute hello 서비스 메서드를 확인 하는 다양 한 권한 부여 체계를 제공 합니다. WCF 서비스에 대해 권한 부여 제어를 사용할 수 없으면 인증된 사용자가 권한 에스컬레이션을 수행할 수 있습니다.</p>|

### <a name="example"></a>예제
hello 같은 구성이 hello 서비스를 실행할 때 hello 클라이언트의 WCF toonot 검사 hello 인증 수준을 지시 합니다.
```
<behaviors>
    <serviceBehaviors>
        <behavior>
            ...
            <serviceAuthorization principalPermissionMode=""None"" />
        </behavior>
    </serviceBehaviors>
</behaviors>
```
권한 있는 toodo를 따라서 hello hello 서비스 메서드의 호출자에 게 서비스 권한 부여 체계 tooverify 사용 됩니다. WCF는 두 가지 모드를 제공 하 고 사용자 지정 권한 부여 체계의 hello 정의 허용 합니다. hello UseWindowsGroups 모드에서는 Windows 역할 및 사용자가 사용 하 고 hello UseAspNetRoles 모드 등 SQL Server, tooauthenticate는 ASP.NET 역할 공급자를 사용 합니다.

### <a name="example"></a>예제
hello 다음 구성 지시 WCF toomake 인지 hello 클라이언트 hello 관리자 그룹의 일부 hello 추가 서비스를 실행 하기 전에:
```
<behaviors>
    <serviceBehaviors>
        <behavior>
            ...
            <serviceAuthorization principalPermissionMode=""UseWindowsGroups"" />
        </behavior>
    </serviceBehaviors>
</behaviors>
```
다음 hello 서비스는 hello 다음과 같이 선언 됩니다.
```
[PrincipalPermission(SecurityAction.Demand,
Role = ""Builtin\\Administrators"")]
public double Add(double n1, double n2)
{
double result = n1 + n2;
return result;
}
```

## <a id="authz-aspnet"></a>ASP.NET Web API에서 적절한 권한 부여 메커니즘 구현

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Web API | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반, MVC5 |
| **특성**              | 해당 없음, ID 공급자 - ADFS, ID 공급자 - Azure AD |
| **참조**              | [ASP.NET Web API의 인증 및 권한 부여](http://www.asp.net/web-api/overview/security/authentication-and-authorization-in-aspnet-web-api)(영문) |
| **단계** | <p>Hello 응용 프로그램 사용자에 대 한 역할 정보를 Azure AD에서 파생 될 수 있습니다 또는 ADFS 클레임 hello 응용 프로그램을 Id 공급자로 사용 하거나 자체 hello 응용 프로그램 수 하는 경우 제공 합니다. 이러한 경우에 사용자 지정 권한 부여 구현 hello hello 사용자 역할 정보를 확인 해야 합니다.</p><p>Hello 응용 프로그램 사용자에 대 한 역할 정보를 Azure AD에서 파생 될 수 있습니다 또는 ADFS 클레임 hello 응용 프로그램을 Id 공급자로 사용 하거나 자체 hello 응용 프로그램 수 하는 경우 제공 합니다. 이러한 경우에 사용자 지정 권한 부여 구현 hello hello 사용자 역할 정보를 확인 해야 합니다.</p>

### <a name="example"></a>예제
```C#
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
public class ApiAuthorizeAttribute : System.Web.Http.AuthorizeAttribute
{
        public async override Task OnAuthorizationAsync(HttpActionContext actionContext, CancellationToken cancellationToken)
        {
            if (actionContext == null)
            {
                throw new Exception();
            }

            if (!string.IsNullOrEmpty(base.Roles))
            {
                bool isAuthorized = ValidateRoles(actionContext);
                if (!isAuthorized)
                {
                    HandleUnauthorizedRequest(actionContext);
                }
            }

            base.OnAuthorization(actionContext);
        }

public bool ValidateRoles(actionContext)
{
   //Authorization logic here; returns true or false
}

}
```
모든 컨트롤러를 hello 및 tooprotected는 작업 메서드 위에 특성으로 데코레이팅 될 해야 합니다.
```C#
[ApiAuthorize]
public class CustomController : ApiController
{
     //Application code goes here
}
```

## <a id="device-permission"></a>여러 권한 수준이 필요로 하는 다양 한 작업을 지 원하는 경우 hello 장치에서 인증 검사를 수행

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | IoT 장치 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | <p>hello 호출자에 게 요청 하는 데 필요한 hello 권한 tooperform hello 동작 하는 경우 hello 호출자 toocheck hello 장치에 권한을 부여 해야 합니다. 사용 예: 예: hello 장치는 hello 클라우드에서 모니터링할 수 있는 스마트 도어 잠금 및 원격으로 hello 도어를 잠금와 같은 기능을 제공 합니다.</p><p>hello 스마트 도어 잠금 누군가가 실제로 제공 hello 도어 근처 카드를 포함 하는 경우에 잠금 해제 기능을 제공 합니다. 이 경우 hello hello 원격 명령 및 컨트롤의 구현 수행 해야 방식 hello 클라우드 게이트웨이 권한 있는 toosend 명령 toounlock hello 문을 지 않으므로 모든 기능 toounlock hello 도어 제공 하지 않습니다.</p>|

## <a id="field-permission"></a>필드 게이트웨이 hello에 다른 사용 권한 수준이 필요로 하는 다양 한 작업을 지 원하는 경우 인증 검사를 수행

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | IoT 필드 게이트웨이 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 필드 게이트웨이 hello hello 호출자에 게 요청 하는 데 필요한 hello 권한 tooperform hello 동작 하는 경우 hello 호출자 toocheck이 권한을 부여 해야 합니다. Admin 사용자에 대 한 다른 사용 권한이 있어야 예: API 인터페이스/tooit를 연결 하는 필드 게이트웨이 v/s 장치 tooconfigure 사용 합니다.|
