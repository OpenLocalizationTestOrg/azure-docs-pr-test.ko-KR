---
title: "-Microsoft 위협 모델링 도구-aaaAuthentication Azure | Microsoft Docs"
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
ms.openlocfilehash: 06c1b1aebab25e6fb5b666d24ecd9d86085d656c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-authentication--mitigations"></a>보안 프레임: 인증 | 완화 
| 제품/서비스 | 문서 |
| --------------- | ------- |
| **웹 응용 프로그램**    | <ul><li>[표준 인증 메커니즘 tooauthenticate tooWeb 응용 프로그램을 사용 하는 것이 좋습니다.](#standard-authn-web-app)</li><li>[응용 프로그램에서 실패한 인증 시나리오를 안전하게 처리해야 함](#handle-failed-authn)</li><li>[버전 업그레이드 또는 적응 인증을 사용하도록 설정](#step-up-adaptive-authn)</li><li>[관리 인터페이스가 적절하게 잠겨 있는지 확인](#admin-interface-lockdown)</li><li>[암호 찾기 기능을 안전하게 구현](#forgot-pword-fxn)</li><li>[암호 및 계정 정책이 구현되었는지 확인](#pword-account-policy)</li><li>[구현 컨트롤 tooprevent username 열거형](#controls-username-enum)</li></ul> |
| **데이터베이스** | <ul><li>[가능 하면 Windows 인증을 사용 하 여 tooSQL 서버를 연결 하기 위한](#win-authn-sql)</li><li>[가능한 경우 연결 tooSQL 데이터베이스에 대 한 Azure Active Directory 인증 사용](#aad-authn-sql)</li><li>[SQL 인증 모드가 사용되는 경우 계정 및 암호 정책이 SQL Server에 적용되어야 함](#authn-account-pword)</li><li>[포함된 데이터베이스에 SQL 인증을 사용하지 마세요](#autn-contained-db)</li></ul> |
| **Azure 이벤트 허브** | <ul><li>[SaS 토큰을 사용하여 장치당 인증 자격 증명 사용](#authn-sas-tokens)</li></ul> |
| **Azure 신뢰 경계** | <ul><li>[Azure 관리자에 Azure Multi-Factor Authentication을 사용하도록 설정](#multi-factor-azure-admin)</li></ul> |
| **Service Fabric 신뢰 경계** | <ul><li>[익명 액세스 tooService 패브릭 클러스터를 제한 합니다.](#anon-access-cluster)</li><li>[Service Fabric 클라이언트-노드 인증서가 노드-노드 인증서와 다른지 확인](#fabric-cn-nn)</li><li>[AAD tooauthenticate 클라이언트 tooservice 패브릭 클러스터를 사용 하 여](#aad-client-fabric)</li><li>[Service Fabric 인증서가 승인된 인증 기관(CA)에서 가져온 것인지 확인](#fabric-cert-ca)</li></ul> |
| **Identity Server** | <ul><li>[Identity Server에서 지원하는 표준 인증 시나리오 사용](#standard-authn-id)</li><li>[확장 가능한 대체 항목으로 hello 기본 Identityserver 토큰 캐시를 재정의 합니다.](#override-token)</li></ul> |
| **컴퓨터 신뢰 경계** | <ul><li>[배포된 응용 프로그램의 이진 파일이 디지털로 서명되었는지 확인](#binaries-signed)</li></ul> |
| **WCF** | <ul><li>[WCF의 tooMSMQ 큐를 연결할 때 인증을 사용 하도록 설정](#msmq-queues)</li><li>[Do WCF 메시지 clientCredentialType toonone를 설정 하지](#message-none)</li><li>[Do WCF 전송 clientCredentialType toonone를 설정 하지](#transport-none)</li></ul> |
| **앱 API** | <ul><li>[표준 인증 기술을 사용 하는 toosecure 웹 Api 되는지 확인](#authn-secure-api)</li></ul> |
| **Azure AD** | <ul><li>[Azure Active Directory에서 지원하는 표준 인증 시나리오 사용](#authn-aad)</li><li>[Hello 기본 ADAL 토큰 캐시 확장 가능한 대체 항목으로 재정의](#adal-scalable)</li><li>[ADAL 인증 토큰의 hello 재생을 사용 하는 tooprevent TokenReplayCache 인지 확인](#tokenreplaycache-adal)</li><li>[ADAL 라이브러리 toomanage 토큰을 사용 하 여 OAuth2 클라이언트 tooAAD에서 요청 (또는 온-프레미스 AD)](#adal-oauth2)</li></ul> |
| **IoT 필드 게이트웨이** | <ul><li>[Toohello 필드 게이트웨이 연결 하는 장치 인증](#authn-devices-field)</li></ul> |
| **IoT 클라우드 게이트웨이** | <ul><li>[TooCloud 게이트웨이 연결 하는 장치의 인증 확인](#authn-devices-cloud)</li><li>[장치당 인증 자격 증명 사용](#authn-cred)</li></ul> |
| **Azure 저장소** | <ul><li>[해당만 hello 필수 컨테이너 및 blob 라면 익명 읽기 액세스 권한을 확인합니다](#req-containers-anon)</li><li>[SAS 또는 SAP를 사용 하 여 Azure 저장소에 tooobjects 제한 된 액세스를 부여 합니다.](#limited-access-sas)</li></ul> |

## <a id="standard-authn-web-app"></a>표준 인증 메커니즘 tooauthenticate tooWeb 응용 프로그램을 사용 하는 것이 좋습니다.

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| 세부 정보 | <p>인증은 사용자 이름 및 암호 같은 자격 증명을 통해 일반적으로 해당 id를 검증 여기서 hello 프로세스입니다. 제공되는 여러 인증 프로토콜을 고려할 수 있습니다. 그 중 일부는 다음과 같습니다.</p><ul><li>클라이언트 인증서</li><li>Windows 기반</li><li>양식 기반</li><li>페더레이션 - ADFS</li><li>페더레이션 - Azure AD</li><li>Federation - Identity Server</li></ul><p>표준 인증 메커니즘 tooidentify hello 소스 프로세스를 사용 하는 것이 좋습니다.</p>|

## <a id="handle-failed-authn"></a>응용 프로그램에서 실패한 인증 시나리오를 안전하게 처리해야 함

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| 세부 정보 | <p>사용자가 명시적으로 인증 하는 응용 프로그램 securely.hello 인증 메커니즘 해야 하는 실패 한 인증 시나리오를 처리 해야 합니다.</p><ul><li>인증에 실패 하면 tooprivileged 리소스 액세스 거부</li><li>인증 실패 및 액세스 거부가 발생한 후 일반 오류 메시지 표시</li></ul><p>다음을 테스트합니다.</p><ul><li>로그인 실패 후 권한이 있는 리소스 보호</li><li>인증 실패 및 액세스 거부 이벤트 발생 시 일반 오류 메시지가 표시됨</li><li>과도하게 실패한 경우 계정을 사용할 수 없음</li><ul>|

## <a id="step-up-adaptive-authn"></a>버전 업그레이드 또는 적응 인증을 사용하도록 설정

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| 세부 정보 | <p>Hello 응용 프로그램에 추가 권한 부여 (예: 최대 또는 적응 인증을 통해 OTP SMS, 전자 메일 등 또는 재인증에 대 한 메시지를 표시에서 보내는 것과 같은 다단계 인증) 확인 액세스 권한을 부여 하기 전에 hello 사용자는 문제가 있으므로 toosensitive 정보입니다. 이 규칙을 중요 한 변경 사항 tooan 계정 또는 작업을 만드는 것도 적용 됩니다.</p><p>인증의 hello 조정 구현 toobe 있는 의미도 hello 응용 프로그램에서 올바르게 상황에 맞는 권한 부여를 적용 하는 방식으로 toonot으로 될 수 있으므로 무단된 조작 방법으로 예제에서는 매개 변수 변경</p>|

## <a id="admin-interface-lockdown"></a>관리 인터페이스가 적절하게 잠겨 있는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| 세부 정보 | hello 첫 번째 솔루션은 특정 소스 IP 범위 toohello 관리 인터페이스를 통해서만 toogrant 액세스입니다. 해당 솔루션은 항상 보다 변경할 수 없습니다 것이 좋습니다 tooenforce hello 관리 인터페이스에 로그인 하기 위한 버전 업그레이드 또는 적응 인증을 |

## <a id="forgot-pword-fxn"></a>암호 찾기 기능을 안전하게 구현

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| 세부 정보 | <p>hello 암호 및 다른 복구 경로는 시간이 제한 된 활성화 hello 대신 토큰 암호 자체를 포함 하 여에 게 링크 보내기 찾기 tooverify을 것입니다. 추가 인증 소프트 토큰 (예: SMS 토큰, 네이티브 모바일 응용 프로그램, 등)에 따라 필요할 수 있습니다도 hello 링크를 통해 전송 하기 전에. 둘째, 하지 잠가야 hello 사용자 계정을 차단한 hello 새 암호를 가져오는 과정 진행 중인 동안 합니다.</p><p>이 인해 toointentionally 잠금 공격이 자동화 있는 hello 사용자를 결정 하는 경우 공격자가 때마다 tooa 서비스 거부 공격 발생할 수 있습니다. 셋째, 진행 중인 설정 된 hello 새 암호 요청 될 때마다 hello 메시지를 표시 하면 순서 tooprevent 사용자 이름 열거에 일반화 해야 합니다. 넷째, 항상 hello 기존 암호를 사용 하지 못하게 하 고 강력한 암호 정책을 구현 합니다.</p> |

## <a id="pword-account-policy"></a>암호 및 계정 정책이 구현되었는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| 세부 정보 | <p>조직의 정책 및 모범 사례에 따라 암호 및 계정 정책이 구현되어야 합니다.</p><p>무차별 암호 대입 공격과 사전에 대해 toodefend 추측 기반: 강력한 암호 정책이 구현된 tooensure 복잡 한 암호 (예: 12 자 최소 길이, 영숫자와 특수 문자)를 생성할 것 이어야 합니다.</p><p>계정 잠금 정책은 hello 방식으로 다음에서 구현 될 수 있습니다.</p><ul><li>**소프트 잠금:** 무차별 암호 대입 공격에 대해 사용자를 보호하는 데 적합한 옵션일 수 있습니다. 예를 들어 hello 사용자 전환 될 때마다 잘못 된 암호로 세 번 hello 응용 프로그램 hello 계정 아래로 무작위 있어서 덜 수익성 공격자가 tooproceed hello에 대 한 암호의 hello 프로세스를 순서 tooslow에 1 분에 대 한 잠글 수입니다. 이 예제에 얻을 수에 대 한 하드 잠금 대책 tooimplement 있었다면 "dos"에서 계정을 영구적으로 잠그는 합니다. 응용 프로그램 OTP (1 회 암호)를 생성 하 고 대역폭을 벗어난 보내기 또는 (전자 메일을 통해 sms 등) toohello 사용자입니다. 또 다른 방법은 실패 한 시도 횟수는 임계값에 도달 하면 tooimplement CAPTCHA를 수 있습니다.</li><li>**하드 잠금:** 응용 프로그램을 공격 하는 사용자를 찾아 그 때까지 대응 팀 시간 toodo 자신의 법정 계정의 잠금을 영구적으로 잠그는 사용 하 여 카운터 때마다이 유형의 잠금 적용 해야 합니다. 이 프로세스 후 다시 toogive hello 사용자 계정의 잠금을 결정 수도 있고 그에 대 한 추가 법적 작업을 수행할 수 있습니다. 이 유형의 방법 더 이상 응용 프로그램 및 인프라 셸이 통과 hello 공격자를 방지 합니다.</li></ul><p>대 한 공격 으로부터 기본 및 예측 가능한 계정 toodefend 있는지 모든 키와 암호는를 교체할 수 및 생성 되거나 설치 시간 이후 버전에서는 대체를 확인 합니다.</p><p>Hello 응용 프로그램에 tooauto-생성 된 hello 암호 임의 고 높은 엔트로피가, 암호를 생성 합니다.</p>|

## <a id="controls-username-enum"></a>구현 컨트롤 tooprevent username 열거형

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 모든 오류 메시지는 순서 tooprevent 사용자 이름 열거에 일반화 해야 합니다. 또한 등록 페이지처럼 기능에 따라 정보 누출이 불가피한 경우도 있습니다. 여기 CAPTCHA tooprevent 공격자가 자동화 된 공격 등의 속도 제한 방법을 toouse 필요합니다. |

## <a id="win-authn-sql"></a>가능 하면 Windows 인증을 사용 하 여 tooSQL 서버를 연결 하기 위한

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 데이터베이스 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | OnPrem |
| **특성**              | SQL 버전 - 모두 |
| **참조**              | [SQL Server - 인증 모드 선택](https://msdn.microsoft.com/library/ms144284.aspx) |
| **단계** | Windows 인증은 Kerberos 보안 프로토콜을 사용 하 여을 강력한 암호에 대 한 관계 toocomplexity 유효성 검사와 암호 정책 적용, 계정 잠금에 대 한 지원을 제공 하 고 암호 만료를 지원 합니다.|

## <a id="aad-authn-sql"></a>가능한 경우 연결 tooSQL 데이터베이스에 대 한 Azure Active Directory 인증 사용

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 데이터베이스 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | SQL Azure |
| **특성**              | SQL 버전 - V12 |
| **참조**              | [데이터베이스를 사용 하 여 Azure Active Directory 인증 여 tooSQL 연결](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/) |
| **단계** | **최소 버전:** Azure SQL 데이터베이스 V12 tooallow hello Microsoft 디렉터리에 대 한 Azure SQL 데이터베이스 toouse AAD 인증 필요 |

## <a id="authn-account-pword"></a>SQL 인증 모드가 사용되는 경우 계정 및 암호 정책이 SQL Server에 적용되어야 함

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 데이터베이스 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [SQL Server 암호 정책](https://technet.microsoft.com/library/ms161959(v=sql.110).aspx) |
| **단계** | SQL Server 인증을 사용하는 경우 Windows 사용자 계정을 기반으로 하지 않는 로그인이 SQL Server에 만들어집니다. Hello 사용자 이름 및 hello 암호를 모두 SQL Server를 사용 하 여 생성 되며 SQL Server에 저장 됩니다. SQL Server는 Windows 암호 정책 메커니즘을 사용할 수 있습니다. SQL Server 내에서 사용 하는 Windows toopasswords에 동일한 복잡성 및 만료 정책을 사용 하는 hello를 적용할 수 있습니다. |

## <a id="autn-contained-db"></a>포함된 데이터베이스에 SQL 인증을 사용하지 마세요

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 데이터베이스 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | OnPrem, SQL Azure |
| **특성**              | SQL 버전 - MSSQL2012, SQL 버전 - V12 |
| **참조**              | [포함된 데이터베이스의 보안 모범 사례](http://msdn.microsoft.com/library/ff929055.aspx) |
| **단계** | hello 없을 경우 적용된 암호 정책에 포함된 된 데이터베이스에서 설정 되는 취약 한 자격 증명의 hello 가능성을 증가할 수 있습니다. Windows 인증을 활용합니다. |

## <a id="authn-sas-tokens"></a>SaS 토큰을 사용하여 장치당 인증 자격 증명 사용

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure Event Hub | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [Event Hubs 인증 및 보안 모델 개요](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **단계** | <p>hello 이벤트 허브 보안 모델은 공유 액세스 서명 (SAS) 토큰 및 이벤트 게시자의 조합을 기반으로 합니다. hello 게시자 이름은 hello를 hello 토큰을 받는 DeviceID를 나타냅니다. Hello 해당 장치를 사용 하 여 생성 하는 hello 토큰을 연결할 도움이 될 것입니다.</p><p>모든 메시지에는 서비스 쪽 송신자로 태그가 지정되어 페이로드 내 원본 스푸핑 시도를 검색할 수 있습니다. 장치를 인증할 때 생성 한 장치 SaS 토큰 범위 지정 된 tooa 고유 게시자 별.</p>|

## <a id="multi-factor-azure-admin"></a>Azure 관리자에 Azure Multi-Factor Authentication을 사용하도록 설정

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure 신뢰 경계 | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [Azure Multi-Factor Authentication 정의](https://azure.microsoft.com/documentation/articles/multi-factor-authentication/) |
| **단계** | <p>Multi-factor authentication (MFA)은 확인 방법을 두 개 이상 필요 하 고 보안 toouser 로그인 및 트랜잭션에 중요 한 두 번째 계층을 추가 하는 인증 방법입니다. 둘 이상 확인 방법을 따르는 hello 요구 하 여 작동 합니다.</p><ul><li>사용자가 알고 있는 정보(일반적으로 암호)</li><li>사용자가 보유한 장치(예: 휴대폰과 같이 쉽게 복제되지 않는 신뢰할 수 있는 장치)</li><li>사용자의 신원 정보(생체 인식)</li><ul>|

## <a id="anon-access-cluster"></a>익명 액세스 tooService 패브릭 클러스터를 제한 합니다.

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Service Fabric 트러스트 경계 | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 환경 - Azure  |
| **참조**              | [Service Fabric 클러스터 보안 시나리오](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security) |
| **단계** | <p>클러스터에서 실행 되는 프로덕션 작업 되었을 경우, 특히 tooyour 클러스터를 연결 하지 못하도록 보안된 tooprevent 권한이 없는 사용자가 항상 있어야 합니다.</p><p>서비스 패브릭 클러스터를 만드는 동안 hello 보안 모드를 사용 하는 "안전한" 너무 설정 되어 있는지 확인 하 고 필요한 hello X.509 서버 인증서를 구성 합니다. "안전 하지 않은" 클러스터를 만드는 사용 하면 모든 익명 사용자 tooconnect tooit 관리 끝점 toohello를 노출 하는 경우 공용 인터넷 합니다.</p>|

## <a id="fabric-cn-nn"></a>Service Fabric 클라이언트-노드 인증서가 노드-노드 인증서와 다른지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Service Fabric 트러스트 경계 | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 환경 - Azure, 환경 - 독립 실행형 |
| **참조**              | [서비스 패브릭 노드 클라이언트 인증서 보안](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/#_client-to-node-certificate-security), [클라이언트 인증서를 사용 하 여 연결 tooa 보안 클러스터](https://azure.microsoft.com/documentation/articles/service-fabric-connect-to-secure-cluster/) |
| **단계** | <p>보안 노드를 클라이언트 인증서는 관리 클라이언트 인증서 및/또는 사용자 클라이언트 인증서를 지정 하 여 hello Azure 포털을 통해, 리소스 관리자 템플릿 또는 독립 실행형 JSON 템플릿 hello 클러스터를 만드는 동안 구성 됩니다.</p><p>hello 관리 클라이언트와 사용자 클라이언트 인증서 지정 hello 기본 및 보조 인증서 노드를 보안에 대해 지정한 계정과 달라 야 합니다.</p>|

## <a id="aad-client-fabric"></a>AAD tooauthenticate 클라이언트 tooservice 패브릭 클러스터를 사용 하 여

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Service Fabric 트러스트 경계 | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 환경 - Azure |
| **참조**              | [클러스터 보안 시나리오 - 보안 권장 사항](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/#security-recommendations) |
| **단계** | Azure에서 실행 하는 클러스터 액세스 Azure Active Directory (AAD)를 사용 하 여 클라이언트 인증서와는 별도로 toohello 관리 끝점 보안 수도 있습니다. Azure의 클러스터에 대 한 노드를 보안에 대 한 AAD tooauthenticate 클라이언트 보안 및 인증서를 사용 것이 좋습니다.|

## <a id="fabric-cert-ca"></a>Service Fabric 인증서가 승인된 인증 기관(CA)에서 가져온 것인지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Service Fabric 트러스트 경계 | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 환경 - Azure |
| **참조**              | [X.509 인증서 및 Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/#x509-certificates-and-service-fabric) |
| **단계** | <p>Service Fabric은 노드 및 클라이언트를 인증하는 데 X.509 서버 인증서를 사용합니다.</p><p>서비스 패브릭에서 인증서를 사용 하는 동안 몇 가지 중요 한 사항이 tooconsider:</p><ul><li>프로덕션 워크로드를 실행하는 클러스터에 사용되는 인증서는 올바르게 구성된 Windows Server 인증서 서비스를 사용하여 만들어지거나 승인된 CA(인증 기관)에서 획득해야 합니다. hello CA는 승인 된 외부 CA 또는 제대로 관리 되는 내부 공개 키 인프라 (PKI) 수 있습니다.</li><li>프로덕션 환경에서 MakeCert.exe와 같은 도구를 사용하여 만든 임시 또는 테스트 인증서를 사용하지 마세요.</li><li>자체 서명된 인증서를 사용할 수 있지만 프로덕션이 아닌 테스트 클러스터에 대해서만 이러한 인증서를 사용해야 합니다.</li></ul>|

## <a id="standard-authn-id"></a>Identity Server에서 지원하는 표준 인증 시나리오 사용

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | ID 서버 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [IdentityServer3-hello 큰 그림](https://identityserver.github.io/Documentation/docsv2/overview/bigPicture.html) |
| **단계** | <p>다음 hello Id 서버에서 지 원하는 일반적인 상호 작용은.</p><ul><li>브라우저는 웹 응용 프로그램과 통신</li><li>웹 응용 프로그램은 Web API와 통신(때로는 자체적으로, 때로는 사용자 대신)</li><li>브라우저 기반 응용 프로그램은 Web API와 통신</li><li>네이티브 응용 프로그램은 Web API와 통신</li><li>서버 기반 응용 프로그램은 Web API와 통신</li><li>Web API가 Web API와 통신(때로는 자체적으로, 때로는 사용자 대신)</li></ul>|

## <a id="override-token"></a>확장 가능한 대체 항목으로 hello 기본 Identityserver 토큰 캐시를 재정의 합니다.

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | ID 서버 | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [Identity Server 배포 - 캐싱](https://identityserver.github.io/Documentation/docsv2/advanced/deployment.html)(영문) |
| **단계** | <p>IdentityServer는 간단한 기본 메모리 내 캐시를 포함합니다. 소규모 네이티브 응용 프로그램에 대 한 것 이지만, 이유 뒤 hello에 대 한 중간 계층 및 백 엔드 응용 프로그램에 대 한 확장 되지 않습니다.</p><ul><li>이러한 응용 프로그램은 한 번에 많은 사용자가 액세스합니다. 동일한 저장소 격리 문제를 만들고 차원에서 작동할 때 문제가 hello에서 모든 액세스 토큰을 저장 합니다: 많은 사용자가 많은 토큰으로 각각 hello 리소스 hello을 대신해 응용 프로그램 액세스 하는 대로 의미할 수 있습니다 무수 및 부담이 조회 작업</li><li>이러한 응용 프로그램의 여러 노드에 액세스 toohello 있어야 하는 분산 토폴로지에 일반적으로 배포 됩니다 같은 캐시</li><li>캐시된 토큰은 프로세스 재활용 및 비활성화에도 유지되어야 함</li><li>웹 응용 프로그램을 구현 하는 동안의 이유로, 위의 모든 hello에 대 한 것이 좋습니다 Azure Redis 캐시 같은 확장 가능한 대안와 토큰 캐시 toooverride hello 기본 Id 서버</li></ul>|

## <a id="binaries-signed"></a>배포된 응용 프로그램의 이진 파일이 디지털로 서명되었는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 컴퓨터 신뢰 경계 | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | Hello 이진 파일의 hello 무결성을 확인할 수 있도록 배포 된 응용 프로그램의 이진 파일이 디지털 서명 확인|

## <a id="msmq-queues"></a>WCF의 tooMSMQ 큐를 연결할 때 인증을 사용 하도록 설정

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | WCF | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반, .NET Framework 3 |
| **특성**              | 해당 없음 |
| **참조**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx) |
| **단계** | 프로그램 tooMSMQ 큐를 연결할 때 tooenable 인증에 실패, 공격자가 처리를 위해 메시지 toohello 큐를 익명으로 제출할 수 있습니다. 인증 사용된 tooconnect tooan MSMQ 사용 되는 큐 toodeliver 메시지 tooanother 프로그램 없으면 공격자 해로운는 익명 메시지를 전송할 수 없습니다.|

### <a name="example"></a>예제
hello `<netMsmqBinding/>` 요소 아래의 hello WCF 구성 파일의 메시지 배달 위한 tooan MSMQ 큐를 연결할 때 WCF toodisable 인증 하도록 지시 합니다.
```
<bindings>
    <netMsmqBinding>
        <binding>
            <security>
                <transport msmqAuthenticationMode=""None"" />
            </security>
        </binding>
    </netMsmqBinding>
</bindings>
```
항상 모든 들어오거나 보내는 메시지에 대 한 MSMQ toorequire Windows 도메인 또는 인증서 인증을 구성 합니다.

### <a name="example"></a>예제
hello `<netMsmqBinding/>` tooan MSMQ 큐를 연결할 때 WCF tooenable 인증서 인증 아래 hello WCF 구성 파일의 요소에 지시 합니다. hello 클라이언트 X.509 인증서를 사용 하 여 인증 됩니다. hello 클라이언트 인증서는 hello 서버 hello 인증서 저장소에 있어야 합니다.
```
<bindings>
    <netMsmqBinding>
        <binding>
            <security>
                <transport msmqAuthenticationMode=""Certificate"" />
            </security>
        </binding>
    </netMsmqBinding>
</bindings>
```

## <a id="message-none"></a>Do WCF 메시지 clientCredentialType toonone를 설정 하지

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | WCF | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | .NET Framework 3 |
| **특성**              | 클라이언트 자격 증명 유형 - 없음 |
| **참조**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify](https://vulncat.fortify.com/en/vulncat/index.html) |
| **단계** | 인증 hello 없으면 의미 모든 사용자는 수 tooaccess이이 서비스입니다. 여기에 클라이언트를 인증 하지 않는 서비스 tooall 사용자가 액세스할 수 있습니다. 클라이언트 자격 증명에 대 한 응용 프로그램 tooauthenticate hello를 구성 합니다. Hello 메시지 clientCredentialType tooWindows 또는 인증서를 설정 하 여이 작업을 수행할 수 있습니다. |

### <a name="example"></a>예제
```
<message clientCredentialType=""Certificate""/>
```

## <a id="transport-none"></a>Do WCF 전송 clientCredentialType toonone를 설정 하지

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | WCF | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반, .NET Framework 3 |
| **특성**              | 클라이언트 자격 증명 유형 - 없음 |
| **참조**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify](https://vulncat.fortify.com/en/vulncat/index.html) |
| **단계** | 인증 hello 없으면 의미 모든 사용자는 수 tooaccess이이 서비스입니다. 여기에 클라이언트를 인증 하지 않는 서비스는 모든 사용자가 tooaccess 기능을 허용 합니다. 클라이언트 자격 증명에 대 한 응용 프로그램 tooauthenticate hello를 구성 합니다. Hello 전송 clientCredentialType tooWindows 또는 인증서를 설정 하 여이 작업을 수행할 수 있습니다. |

### <a name="example"></a>예제
```
<transport clientCredentialType=""Certificate""/>
```

## <a id="authn-secure-api"></a>표준 인증 기술을 사용 하는 toosecure 웹 Api 되는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Web API | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [ASP.NET Web API의 인증 및 권한 부여](http://www.asp.net/web-api/overview/security/authentication-and-authorization-in-aspnet-web-api)(영문), [ASP.NET Web API의 외부 인증 서비스(C#)](http://www.asp.net/web-api/overview/security/external-authentication-services)(영문) |
| **단계** | <p>인증은 사용자 이름 및 암호 같은 자격 증명을 통해 일반적으로 해당 id를 검증 여기서 hello 프로세스입니다. 제공되는 여러 인증 프로토콜을 고려할 수 있습니다. 그 중 일부는 다음과 같습니다.</p><ul><li>클라이언트 인증서</li><li>Windows 기반</li><li>양식 기반</li><li>페더레이션 - ADFS</li><li>페더레이션 - Azure AD</li><li>Federation - Identity Server</li></ul><p>Hello references 섹션에 링크는 각각 hello 인증 체계의 수 있는 방법에 대 한 하위 수준 내용은 구현 toosecure 웹 API를 제공 합니다.</p>|

## <a id="authn-aad"></a>Azure Active Directory에서 지원하는 표준 인증 시나리오 사용

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure AD | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [Azure AD의 인증 시나리오](https://azure.microsoft.com/documentation/articles/active-directory-authentication-scenarios/), [Azure Active Directory 코드 샘플](https://azure.microsoft.com/documentation/articles/active-directory-code-samples/), [Azure Active Directory 개발자 가이드](https://azure.microsoft.com/documentation/articles/active-directory-developers-guide/) |
| **단계** | <p>Azure AD(Azure Active Directory)는 IDaaS(Identity as a Service)를 제공하며 OAuth 2.0 및 OpenID Connect 등의 업계 표준 프로토콜을 지원하여 개발자의 인증 작업을 간소화합니다. 다음 Azure AD에서 지 원하는 다섯 가지 기본 응용 프로그램 시나리오 hello에은입니다.</p><ul><li>웹 브라우저 tooWeb 응용 프로그램: 사용자는 Azure AD로 보호 되는 tooa 웹 응용 프로그램에서 toosign 있어야 합니다.</li><li>단일 페이지 응용 프로그램 (SPA): 사용자는 Azure AD로 보호 되는 tooa 단일 페이지 응용 프로그램에서 toosign 있어야 합니다.</li><li>네이티브 응용 프로그램 tooWeb API: 네이티브 응용 프로그램에서 실행 되는 휴대폰, 태블릿 또는 PC 요구 tooauthenticate 사용자 tooget 리소스 web API에서에서 Azure AD로 보호 되는</li><li>웹 응용 프로그램 tooWeb API: 웹 응용 프로그램 웹 Azure AD에서 보호 하는 API에서에서 tooget 리소스가 필요</li><li>디먼 또는 서버 응용 프로그램 tooWeb API: 디먼 응용 프로그램 또는 서버 응용 프로그램 웹 사용자 인터페이스 없이 웹 Azure AD에서 보호 하는 API에서에서 tooget 리소스가 필요</li></ul><p>하위 수준 구현 세부 사항에 대 한 hello references 섹션에 toohello 링크를 참조 하십시오</p>|

## <a id="adal-scalable"></a>Hello 기본 ADAL 토큰 캐시 확장 가능한 대체 항목으로 재정의

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure AD | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [웹 응용 프로그램에 대한 Azure Active Directory의 최신 인증](https://blogs.msdn.microsoft.com/microsoft_press/2016/01/04/new-book-modern-authentication-with-azure-active-directory-for-web-applications/)(영문), [ADAL 토큰 캐시로 Redis 사용](https://blogs.msdn.microsoft.com/mrochon/2016/09/19/using-redis-as-adal-token-cache/)(영문)  |
| **단계** | <p>사용 하 여 ADAL (Active Directory 인증 라이브러리)은 사용 가능한 프로세스 범위 정적 저장소를 사용 하는 메모리에 캐시 하는 hello 기본 캐시 합니다. 네이티브 응용 프로그램에 대 한이 작동 하는 동안 다음 이유로 hello에 대 한 중간 계층 및 백 엔드 응용 프로그램에 대 한 확장 되지 않습니다.</p><ul><li>이러한 응용 프로그램은 한 번에 많은 사용자가 액세스합니다. 동일한 저장소 격리 문제를 만들고 차원에서 작동할 때 문제가 hello에서 모든 액세스 토큰을 저장 합니다: 많은 사용자가 많은 토큰으로 각각 hello 리소스 hello을 대신해 응용 프로그램 액세스 하는 대로 의미할 수 있습니다 무수 및 부담이 조회 작업</li><li>이러한 응용 프로그램의 여러 노드에 액세스 toohello 있어야 하는 분산 토폴로지에 일반적으로 배포 됩니다 같은 캐시</li><li>캐시된 토큰은 프로세스 재활용 및 비활성화에도 유지되어야 함</li></ul><p>웹 응용 프로그램을 구현 하는 동안의 이유로, 위의 모든 hello에 대 한 toooverride hello 기본 ADAL 토큰 캐시 Azure Redis 캐시 같은 확장 가능한 대안으로 좋습니다.</p>|

## <a id="tokenreplaycache-adal"></a>ADAL 인증 토큰의 hello 재생을 사용 하는 tooprevent TokenReplayCache 인지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure AD | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [웹 응용 프로그램에 대한 Azure Active Directory의 최신 인증](https://blogs.msdn.microsoft.com/microsoft_press/2016/01/04/new-book-modern-authentication-with-azure-active-directory-for-web-applications/)(영문) |
| **단계** | <p>hello TokenReplayCache 속성을 사용 하면 개발자가 toodefine 토큰 재생 캐시를 확인 하는 hello 용도 대 한 토큰 토큰 없이 저장에 사용할 수 있는 저장소를 두 번 이상 사용할 수 있습니다.</p><p>이 일반적인 공격에 대 한 측정 hello 토큰 재생 공격을 적절 하 게 호출: 로그인 시 전송 된 hello 토큰을 가로채는 공격자가 toosend 하려고 할 수도 있습니다 것 다시 toohello 응용 프로그램 ("재생")는 새 세션을 설정 합니다. 예:에서 OIDC 코드-부여 흐름을 사용자가 인증을 요청 후 너무 "/ signin oidc" hello 신뢰 당사자의 끝점은 "id_token"와 "코드" 및 "상태" 매개 변수 생성 됩니다.</p><p>신뢰 당사자 hello이이 요청의 유효성을 검사 하 고 새 세션을 설정 합니다. 이 요청을 캡처하고를 재생 하는 악의적인 사용자, 경우에 성공적인 세션 및 스 푸 프 hello 사용자를 설정할 수 합리적인. OpenID Connect의 hello nonce의 hello 존재를 제한할 수 있지만는 hello 공격 수 성공적으로 시행할 hello 상황을 완전히 제거 됩니다. tooprotect 개발자가 응용 프로그램 수 ITokenReplayCache의 구현을 제공 하 고 할당 인스턴스 tooTokenReplayCache 합니다.</p>|

### <a name="example"></a>예제
```C#
// ITokenReplayCache defined in ADAL
public interface ITokenReplayCache
{
bool TryAdd(string securityToken, DateTime expiresOn);
bool TryFind(string securityToken);
}
```

### <a name="example"></a>예제
Hello ITokenReplayCache 인터페이스의 예제 구현은 다음과 같습니다. (프로젝트별 캐싱 프레임워크를 사용자 지정 및 구현하세요)
```C#
public class TokenReplayCache : ITokenReplayCache
{
    private readonly ICacheProvider cache; // Your project-specific cache provider
    public TokenReplayCache(ICacheProvider cache)
    {
        this.cache = cache;
    }
    public bool TryAdd(string securityToken, DateTime expiresOn)
    {
        if (this.cache.Get<string>(securityToken) == null)
        {
            this.cache.Set(securityToken, securityToken);
            return true;
        }
        return false;
    }
    public bool TryFind(string securityToken)
    {
        return this.cache.Get<string>(securityToken) != null;
    }
}
```
구현 하는 hello 캐시 toobe hello "TokenValidationParameters" 속성을 통해 OIDC 옵션에서 다음과 같이 참조에 있습니다.
```C#
OpenIdConnectOptions openIdConnectOptions = new OpenIdConnectOptions
{
    AutomaticAuthenticate = true,
    ... // other configuration properties follow..
    TokenValidationParameters = new TokenValidationParameters
    {
        TokenReplayCache = new TokenReplayCache(/*Inject your cache provider*/);
    }
}
```

OIDC 암호로 보호 된 응용 프로그램에 로그인이이 구성의 해당 tootest hello 효율성을 확인 하 고 캡처 hello 요청 너무 하십시오`"/signin-oidc"` fiddler에 대 한 끝점입니다. Hello 보호 위치에 없는 경우이 요청에서 fiddler 재생 합니다. 새 세션 쿠키를 설정 합니다. Hello 요청 hello TokenReplayCache 보호를 추가한 후 재생 될 때 hello 응용 프로그램 다음과 같은 예외가 throw 됩니다.`SecurityTokenReplayDetectedException: IDX10228: hello securityToken has previously been validated, securityToken: 'eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ1......`

## <a id="adal-oauth2"></a>ADAL 라이브러리 toomanage 토큰을 사용 하 여 OAuth2 클라이언트 tooAAD에서 요청 (또는 온-프레미스 AD)

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure AD | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [ADAL](https://azure.microsoft.com/documentation/articles/active-directory-authentication-libraries/) |
| **단계** | <p>hello Azure AD 인증 라이브러리 (ADAL) 사용 하면 클라이언트 응용 프로그램 개발자가 tooeasily 인증 사용자 toocloud 또는 온-프레미스 Active Directory (AD) 하 고 후 보안 API 호출용 액세스 토큰을 가져올.</p><p>ADAL에는 비동기 지원, 액세스 토큰 및 새로고침 토큰을 저장하는 구성 가능한 토큰 캐시, 액세스 토큰이 만료되고 새로고침 토큰을 사용할 수 있을 때 자동 토큰 새로고침 등, 개발자들의 인증을 쉽게 지원하는 많은 기능이 있습니다.</p><p>대부분의 hello 복잡성을 처리 함으로써 ADAL는 개발자가 응용 프로그램의 비즈니스 논리에 초점을 맞춥니다 하 고 보안 전문가가 아니더라도 리소스를 쉽게 보호 수 있습니다. .NET, JavaScript(클라이언트 및 Node.js), iOS, Android 및 Java에 대해 별도의 라이브러리를 사용할 수 있습니다.</p>|

## <a id="authn-devices-field"></a>Toohello 필드 게이트웨이 연결 하는 장치 인증

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | IoT 필드 게이트웨이 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 데이터를 받기 전에 및 클라우드 게이트웨이 hello와의 통신을 업스트림을 촉진 하기 전에 hello 게이트웨이 필드에서 각 장치가 인증 되었는지 확인 합니다. 또한 장치가 장치별 자격 증명에 연결되었는지 확인하여 개별 장치를 고유하게 식별할 수 있도록 합니다.|

## <a id="authn-devices-cloud"></a>TooCloud 게이트웨이 연결 하는 장치의 인증 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | IoT 클라우드 게이트웨이 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반, C#, Node.JS,  |
| **특성**              | 해당 없음, 게이트웨이 선택 - Azure IoT Hub |
| **참조**              | 해당 없음, [Azure IoT Hub 및 .NET](https://azure.microsoft.com/documentation/articles/iot-hub-csharp-csharp-getstarted/), [IoT Hub 및 Node JS 시작](https://azure.microsoft.com/documentation/articles/iot-hub-node-node-getstarted), [SAS 및 인증서로 IoT 보호](https://azure.microsoft.com/documentation/articles/iot-hub-sas-tokens/), [Git 리포지토리](https://github.com/Azure/azure-iot-sdks/tree/master/node) |
| **단계** | <ul><li>**일반:** 보안 TLS (전송 계층) 또는 IPSec을 사용 하 여 Authenticate hello 장치입니다. 전체 비대칭 암호화를 처리할 수 없는 PSK(미리 공유한 키)를 해당 장치에서 사용할 수 있도록 인프라가 지원해야 합니다. Azure AD, Oauth를 활용하세요.</li><li>**C#의 경우:** hello Create 메서드를 기본적으로 DeviceClient 인스턴스를 만들 때 hello AMQP 프로토콜 toocommunicate IoT 허브를 사용 하는 DeviceClient 인스턴스를 만듭니다. HTTPS 프로토콜을 toouse hello toospecify hello 프로토콜 수 있도록 하는 hello Create 메서드의 hello 재정의 사용 합니다. Hello hello HTTPS 프로토콜을 사용 하는 경우도 추가 해야 `Microsoft.AspNet.WebApi.Client` NuGet 패키지 tooyour 프로젝트 tooinclude hello `System.Net.Http.Formatting` 네임 스페이스입니다.</li></ul>|

### <a name="example"></a>예제
```C#
static DeviceClient deviceClient;

static string deviceKey = "{device key}";
static string iotHubUri = "{iot hub hostname}";

var messageString = "{message in string format}";
var message = new Message(Encoding.ASCII.GetBytes(messageString));

deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey("myFirstDevice", deviceKey));

await deviceClient.SendEventAsync(message);
```

### <a name="example"></a>예제
**Node.JS: 인증**
#### <a name="symmetric-key"></a>대칭 키
* azure에서 IoT Hub 만들기
* Hello 장치 id 레지스트리에서 항목을 만듭니다
    ```javascript
    var device = new iothub.Device(null);
    device.deviceId = <DeviceId >
    registry.create(device, function(err, deviceInfo, res) {})
    ```
* 시뮬레이션된 장치 만들기
    ```javascript
    var clientFromConnectionString = require('azure-iot-device-amqp').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    var connectionString = 'HostName=<HostName>DeviceId=<DeviceId>SharedAccessKey=<SharedAccessKey>';
    var client = clientFromConnectionString(connectionString);
    ```
#### <a name="sas-token"></a>SAS 토큰
* 대칭 키를 사용할 때 내부적으로 생성된 것을 가져오지만 명시적으로도 생성 및 사용할 수 있음
* 프로토콜 정의 : `var Http = require('azure-iot-device-http').Http;`
* sas 토큰 만들기:
    ```javascript
    resourceUri = encodeURIComponent(resourceUri.toLowerCase()).toLowerCase();
    var deviceName = "<deviceName >";
    var expires = (Date.now() / 1000) + expiresInMins * 60;
    var toSign = resourceUri + '\n' + expires;
    // using crypto
    var decodedPassword = new Buffer(signingKey, 'base64').toString('binary');
    const hmac = crypto.createHmac('sha256', decodedPassword);
    hmac.update(toSign);
    var base64signature = hmac.digest('base64');
    var base64UriEncoded = encodeURIComponent(base64signature);
    // construct authorization string
    var token = "SharedAccessSignature sr=" + resourceUri + "%2fdevices%2f"+deviceName+"&sig="
    + base64UriEncoded + "&se=" + expires;
    if (policyName) token += "&skn="+policyName;
    return token;
    ```
* sas 토큰을 사용하여 연결: 
    ```javascript
    Client.fromSharedAccessSignature(sas, Http); 
    ```
#### <a name="certificates"></a>인증서
* 생성 된 자체 서명 된 X509 인증서를 사용 하 여 같은 도구를 OpenSSL toogenerate 여.cert 키와.key 파일 toostore hello 인증서와 hello 키를 각각
* 인증서를 사용하여 보안 연결을 허용하는 장치 프로비전
    ```javascript
    var connectionString = '<connectionString>';
    var registry = iothub.Registry.fromConnectionString(connectionString);
    var deviceJSON = {deviceId:"<deviceId>",
    authentication: {
        x509Thumbprint: {
        primaryThumbprint: "<PrimaryThumbprint>",
        secondaryThumbprint: "<SecondaryThumbprint>"
        }
    }}
    var device = deviceJSON;
    registry.create(device, function (err) {});
    ```
* 인증서를 사용하여 장치 연결
    ```javascript
    var Protocol = require('azure-iot-device-http').Http;
    var Client = require('azure-iot-device').Client;
    var connectionString = 'HostName=<HostName>DeviceId=<DeviceId>x509=true';
    var client = Client.fromConnectionString(connectionString, Protocol);
    var options = {
        key: fs.readFileSync('./key.pem', 'utf8'),
        cert: fs.readFileSync('./server.crt', 'utf8')
    }; 
    // Calling setOptions with hello x509 certificate and key (and optionally, passphrase) will configure hello client //transport toouse x509 when connecting tooIoT Hub
    client.setOptions(options);
    //call fn tooexecute after hello connection is set up
    client.open(fn);
    ```

## <a id="authn-cred"></a>장치당 인증 자격 증명 사용

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | IoT 클라우드 게이트웨이  | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 게이트웨이 선택 - Azure IoT Hub |
| **참조**              | [Azure IoT Hub 보안 토큰](https://azure.microsoft.com/documentation/articles/iot-hub-sas-tokens/) |
| **단계** | IoT Hub 수준 공유 액세스 정책 대신, 장치 키 또는 클라이언트 인증서를 기반으로 SaS 토큰을 사용하여 장치당 인증 자격 증명을 사용합니다. 다른 하나의 장치 또는 필드 게이트웨이의 인증 토큰이 hello 다시 사용을 방지이 |

## <a id="req-containers-anon"></a>해당만 hello 필수 컨테이너 및 blob 라면 익명 읽기 액세스 권한을 확인합니다

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure 저장소 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | StorageType - Blob |
| **참조**              | [익명 읽기 권한을 toocontainers 및 blob 관리](https://azure.microsoft.com/documentation/articles/storage-manage-access-to-resources/), [공유 액세스 서명, 1 부: hello SAS 모델 이해](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/) |
| **단계** | <p>기본적으로 컨테이너와 그 안에 모든 blob hello 저장소 계정의 소유자 hello에 의해서만 액세스할 수 있습니다. toogive 익명 사용자에 게 읽기 권한이 있으면 tooa 컨테이너와 그 blob hello 컨테이너 권한을 tooallow 공용 액세스를 설정할 수 하나. 익명 사용자에 게 hello 요청을 인증 하지 않고 공개적으로 액세스할 수 있는 컨테이너 내 blob를 읽을 수 있습니다.</p><p>컨테이너는 hello 다음 컨테이너 액세스를 관리 하기 위한 옵션 제공:</p><ul><li>전체 공개 읽기 액세스: 익명 요청을 통해 컨테이너와 Blob 데이터를 읽을 수 있습니다. 클라이언트가 익명 요청을 통해 hello 컨테이너 내 blob를 열거할 수 있지만 hello 저장소 계정 내 컨테이너는 열거할 수 없습니다.</li><li>Blob에 대해서만 공개 읽기 액세스: 이 컨테이너 내의 Blob 데이터는 익명 요청을 통해 읽을 수 있으나 컨테이너 데이터는 읽을 수 없습니다. 클라이언트가 익명 요청을 통해 hello 컨테이너 내 blob를 열거할 수 없습니다.</li><li>공용 읽기 권한 없음: hello 계정 소유자만 컨테이너 및 blob 데이터를 읽을 수</li></ul><p>익명 액세스는 특정 Blob을 익명 읽기 권한에 사용해야 하는 경우에 가장 적합합니다. 세부적인 제어에 대 한 다른 사용 권한을 사용 하 여 제한 된 toodelegate 액세스할 수 있도록 하는 공유 액세스 서명을 만들 수 하나 지정된 된 시간 간격에 걸쳐 있습니다. 중요한 데이터를 포함할 가능성이 있는 컨테이너 및 Blob를 실수로 익명 액세스하지 않는지 확인합니다.</p>|

## <a id="limited-access-sas"></a>SAS 또는 SAP를 사용 하 여 Azure 저장소에 tooobjects 제한 된 액세스를 부여 합니다.

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure 저장소 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음 |
| **참조**              | [공유 액세스 서명, 1 부: 이해 hello SAS 모델](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/), [공유 액세스 서명, 2 부: 만들기 및 SAS를 사용 하 여 Blob 저장소와](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-2/), [toodelegate tooobjects 사용 하 여 사용자 계정에 액세스 하는 방법 공유 액세스 서명과 저장 된 액세스 정책](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_how-to-delegate-access-to-objects-in-your-account-using-shared-access-signatures-and-stored-access-policies) |
| **단계** | <p>공유 액세스 서명 (SAS)를 사용 하는 강력한 방법을 toogrant 제한 된 액세스 tooobjects tooexpose 계정 액세스 키 필요 없이 저장소 계정 tooother 클라이언트에서입니다. hello SAS는 해당 쿼리 매개 변수를 포함 하는 URI의 모든 인증에 대 한 필요한 hello 정보 tooa 저장소 리소스에 액세스 합니다. tooaccess hello SAS로 저장소 리소스를 hello 클라이언트 hello SAS toohello 적절 한 생성자 또는 메서드에 toopass를 해야합니다.</p><p>저장소 계정 tooa 클라이언트 hello 계정 키를 가진 신뢰할 수 없는 tooprovide 액세스 tooresources 하려는 경우 SAS를 사용할 수 있습니다. 저장소 계정 키를 모두 관리 액세스 tooyour 계정 및 모든 hello 리소스에 부여 되는 기본 및 보조 키를 포함 합니다. 계정 키 중 하나를 노출 악성 또는 부주의로 사용 하 여 사용자 계정 toohello 가능성이 열립니다. 공유 액세스 서명을 toohello 사용 권한을 부여 하지에 따라 저장소 계정에 및 hello 계정 키에 대 한 필요 없이 tooread, 쓰기 및 삭제 데이터 다른 클라이언트를 허용 하는 안전한 좋은 제공 합니다.</p><p>매번 비슷한 매개 변수의 논리적 집합을 사용한다면 저장된 액세스 정책(SAP)을 사용하는 것이 더 좋습니다. 저장 된 액세스 정책에서 파생 된 SAS를 사용 하 여 제공 하기 때문에 SAS를 즉시 인지 hello 권장 모범 사례 tooalways hello 기능 toorevoke 가능 하면 저장 된 액세스 정책을 사용 합니다.</p>|
