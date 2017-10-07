---
title: "-Microsoft 위협 모델링 도구-aaaCryptography Azure | Microsoft Docs"
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
ms.openlocfilehash: cab981bf116a0e76bbf44fe0f0a1a3650e4ab0f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-cryptography--mitigations"></a>보안 프레임: 암호화 | 완화 
| 제품/서비스 | 문서 |
| --------------- | ------- |
| **웹 응용 프로그램** | <ul><li>[승인된 대칭 블록 암호화 및 키 길이만 사용](#cipher-length)</li><li>[대칭 암호화에 승인된 블록 암호화 모드 및 초기화 벡터 사용](#vector-ciphers)</li><li>[승인된 비대칭 알고리즘, 키 길이 및 패딩 사용](#padding)</li><li>[승인된 난수 생성기 사용](#numgen)</li><li>[대칭 스트림 암호화 사용 금지](#stream-ciphers)</li><li>[승인된 MAC/HMAC/키 해시 알고리즘 사용](#mac-hash)</li><li>[승인된 암호화 해시 함수만 사용](#hash-functions)</li></ul> |
| **데이터베이스** | <ul><li>[Hello 데이터베이스의 강력한 암호화 알고리즘 tooencrypt 데이터를 사용 합니다.](#strong-db)</li><li>[암호화되고 디지털 서명되어야 하는 SSIS 패키지](#ssis-signed)</li><li>[디지털 서명 toocritical 데이터베이스 보안 개체를 추가 합니다.](#securables-db)</li><li>[SQL server EKM tooprotect 암호화 키를 사용 하 여](#ekm-keys)</li><li>[암호화 키에는 표시 되 tooDatabase 엔진을 사용 해야 합니다. AlwaysEncrypted 기능을 사용 하 여](#keys-engine)</li></ul> |
| **IoT 장치** | <ul><li>[IoT 장치에 안전하게 암호화 키 저장](#keys-iot)</li></ul> | 
| **IoT 클라우드 게이트웨이** | <ul><li>[충분 한 길이의 인증 tooIoT 허브에 대 한 임의의 대칭 키를 생성 합니다.](#random-hub)</li></ul> | 
| **Dynamics CRM 모바일 클라이언트** | <ul><li>[PIN 사용이 필요하고 원격 지우기를 허용하는 장치 관리 정책이 있는지 확인](#pin-remote)</li></ul> | 
| **Dynamics CRM Outlook 클라이언트** | <ul><li>[PIN/암호/자동 잠금이 필요하고 모든 데이터를 암호화(예: Bitlocker)하는 장치 관리 정책이 있는지 확인](#bitlocker)</li></ul> | 
| **Identity Server** | <ul><li>[Identity Server를 사용할 때 서명 키가 롤오버되는지 확인](#rolled-server)</li><li>[Identity Server에서 암호화된 강력한 클라이언트 ID와 클라이언트 비밀이 사용되는지 확인](#client-server)</li></ul> | 

## <a id="cipher-length"></a>승인된 대칭 블록 암호화 및 키 길이만 사용

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | <p>제품 대칭 블록 암호화 및 조직의 hello Crypto 관리자가 명시적으로 승인한는 관련 된 키 길이만 사용 해야 합니다. Microsoft에서 승인 된 대칭 알고리즘 포함 하는 블록 암호화를 수행 하는 hello:</p><ul><li>새로운 코드의 경우 AES-128, AES-192, AES-256이 허용됩니다.</li><li>기존 코드를 사용하는 이전 버전과의 호환성을 위해 3개 키를 사용하는 3DES가 허용됩니다.</li><li>대칭 블록 암호화를 사용하는 제품의 경우:<ul><li>새로운 코드에는 AES(Advanced Encryption Standard)가 필요합니다.</li><li>이전 버전과의 호환성을 위해 기존 코드에 3DES(3키 3중 Data Encryption Standard)가 허용됩니다.</li><li>RC2, DES, 2키 3DES, DESX 및 Skipjack을 포함한 다른 모든 블록 암호화는 이전 데이터를 해독하는 데만 사용할 수 있으며, 암호화에 사용되는 경우 교체해야 합니다.</li></ul></li><li>대칭 블록 암호화 알고리즘의 경우 최소 키 길이는 128비트입니다. 새 코드에 대 한 권장 하는 블록 암호화 알고리즘은 AES hello (AES 128, AES 192 및 AES 256를 모두 사용할 수)</li><li>3 키 3DES; 기존 코드의 경우 이미 사용 중인 현재 허용 되는 전환 tooAES 것이 좋습니다. DES, DESX, RC2 및 Skipjack은 더 이상 안전한 것으로 간주되지 않습니다. 이러한 알고리즘 hello 찾았의 이전 버전과 호환성에 대 한 기존 데이터를 암호 해독에 사용할 수 있습니다 및 데이터를 다시 암호화 권장된 블록 암호화를 사용 하 여</li></ul><p>모든 대칭 블록 암호화는 적절한 IV(초기화 벡터)를 사용해야 하는 승인된 암호화 모드와 함께 사용해야 합니다. 적절한 IV는 일반적으로 난수이며, 절대로 상수 값이 아닙니다.</p><p>조직의 Crypto 보드 검토 (것과 반대로 toowriting 새 데이터)으로 기존 데이터를 읽기 위한 명시적이 든 레거시 승인 되지 않은 암호화 알고리즘 및 키 길이 보다 작은 hello 사용을 허용할 수도 있습니다. 그러나 이 요구 사항에 대한 예외를 제출해야 합니다. 또한 엔터프라이즈 배포에서 제품 때 고려해 야 경고 관리자가 약한 암호화에 사용 되는 tooread 데이터입니다. 이러한 경고는 설명적이고 실행 가능해야 합니다. 일부 경우에는 것이 적절 한 toohave 약한 암호화의 그룹 정책 제어 hello 사용</p><p>관리되는 암호화 민첩성을 위해 허용되는 .NET 알고리즘(기본 설정 순서대로)</p><ul><li>AesCng(FIPS 규격)</li><li>AuthenticatedAesCng(FIPS 규격)</li><li>AESCryptoServiceProvider(FIPS 규격)</li><li>AESManaged(비 FIPS 규격)</li></ul><p>이러한 알고리즘 중 지정할 수 있음을 hello를 통해 점에 유의 하십시오 `SymmetricAlgorithm.Create` 또는 `CryptoConfig.CreateFromName` 변경 toohello machine.config 파일을 만들지 않고 메서드. 또한 AES 버전의.NET 이전 too.NET 3.5 라는 확인 `RijndaelManaged`, 및 `AesCng` 및 `AuthenticatedAesCng` 는 > CodePlex를 통해 사용할 수 있는 OS 기본 hello CNG를 필요로 하 고</p>

## <a id="vector-ciphers"></a>대칭 암호화에 승인된 블록 암호화 모드 및 초기화 벡터 사용

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 모든 대칭 블록 암호화는 승인된 대칭 암호화 모드와 함께 사용해야 합니다. 승인 된 hello 모드는 CBC 및 CTS 합니다. 특히, 연산의 hello 전자 코드 책 (ECB) 모드 피해 야 합니다. ECB 사용 하면 조직의 Crypto 보드 검토를 해야합니다. OFB, CFB, CTR, CCM 및 GCM 또는 다른 암호화 모드의 모든 사용은 조직의 Crypto Board에서 검토해야 합니다. 동일한 hello 재사용 초기화 벡터 (IV)에서 "스트리밍 암호 모드" CTR, 같은 블록 암호는 암호화 된 데이터 toobe 공개 발생할 수 있습니다. 또한 모든 대칭 블록 암호화도 적절한 IV와 함께 사용해야 합니다. 적절한 IV는 암호화된 강력한 난수이며, 절대로 상수 값이 아닙니다. |

## <a id="padding"></a>승인된 비대칭 알고리즘, 키 길이 및 패딩 사용

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | <p>hello 사용 금지 된 암호화 알고리즘의는 상당한 위험 tooproduct 보안을 소개 하 고 방지 해야 합니다. 제품에서는 조직의 Crypto Board에서 명시적으로 승인한 암호화 알고리즘, 관련 키 길이 및 패딩만 사용해야 합니다.</p><ul><li>**RSA -** 암호화, 키 교환 및 서명에 사용할 수 있습니다. RSA 암호화만 hello OAEP 또는 RSA KEM 패딩 모드를 사용 해야 합니다. 기존 코드는 호환성을 위해서만 PKCS #1 v1.5 패딩 모드를 사용할 수 있습니다. 널 패딩 사용은 명시적으로 금지됩니다. 새 코드에는 2,048비트 이상의 키가 필요합니다. 기존 코드는 조직의 Crypto Board에서 검토한 후 이전 버전과의 호환성을 위해서만 2,048비트 미만의 키를 지원할 수 있습니다. 1,024비트 미만의 키는 이전 데이터의 암호 해독/확인에만 사용할 수 있으며, 암호화 또는 서명 작업에 사용되는 경우 교체해야 합니다.</li><li>**ECDSA -** 서명에만 사용할 수 있습니다. 새 코드에는 256비트 이상의 키가 있는 ECDSA가 필요합니다. ECDSA 기반 서명이 hello 3 승인 NIST 곡선 중 하나를 사용 해야 합니다 (P-256, P-384 또는 P521). 철저히 분석된 곡선은 조직의 Crypto Board에서 검토한 후에만 사용할 수 있습니다.</li><li>**ECDH -** 키 교환에만 사용할 수 있습니다. 새 코드에는 256비트 이상의 키가 있는 ECDH가 필요합니다. 키 교환 ECDH 기반 hello 3 승인 NIST 곡선 중 하나를 사용 해야 합니다 (P-256, P-384 또는 P521). 철저히 분석된 곡선은 조직의 Crypto Board에서 검토한 후에만 사용할 수 있습니다.</li><li>**DSA -** 조직의 Crypto Board에서 검토하고 승인한 후에 허용될 수 있습니다. 조직의 Crypto 보드 검토를 보안 관리자 tooschedule에 게 문의 하십시오. DSA 사용 승인 되 면가 필요 합니다 tooprohibit 사용 키 길이가 2048 비트 미만의 note 합니다. CNG는 Windows 8부터 2,048비트 이상의 키 길이를 지원합니다.</li><li>**Diffie-Hellman -** 세션 키 관리에만 사용할 수 있습니다. 새 코드에는 2,048비트 이상의 키가 필요합니다. 기존 코드는 조직의 Crypto Board에서 검토한 후 이전 버전과의 호환성을 위해서만 2,048비트 미만의 키를 지원할 수 있습니다. 1,024비트 미만의 키는 사용할 수 없습니다.</li><ul>

## <a id="numgen"></a>승인된 난수 생성기 사용

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | <p>제품에서는 승인된 난수 발생기를 사용해야 합니다. Hello C 런타임 함수 rand, hello.NET Framework 클래스 System.Random, GetTickCount와 같은 시스템 함수 등 의사 난수 기능, 따라서 사용할 수 없습니다 이러한 코드입니다. Hello 이중 타원 곡선 난수 생성기 (DUAL_EC_DRBG) 알고리즘의 사용은 금지 되어 있습니다.</p><ul><li>**CNG-** BCryptGenRandom (hello 호출자 [PASSIVE_LEVEL] 0 보다 큰 모든 IRQL에서 실행 될 수 있습니다 않는 것이 좋습니다 hello BCRYPT_USE_SYSTEM_PREFERRED_RNG 플래그 사용)</li><li>**CAPI -** cryptGenRandom</li><li>**Win32/64 -** RtlGenRandom(새 구현에서는 BCryptGenRandom 또는 CryptGenRandom을 사용해야 함) * rand_s * SystemPrng(커널 모드의 경우)</li><li>**.NET -** RNGCryptoServiceProvider 또는 RNGCng</li><li>**Windows 스토어 앱-** Windows.Security.Cryptography.CryptographicBuffer.GenerateRandom 또는 .GenerateRandomNumber</li><li>**Apple OS X (10.7+)/iOS(2.0+)-** int SecRandomCopyBytes (SecRandomRef 임의 size_t 수, uint8_t *바이트)</li><li>**Apple OS X (< 10.7)-** 사용 / 개발/임의 tooretrieve 난수</li><li>**Java(Google Android Java 코드 포함) -** java.security.SecureRandom 클래스입니다. 에 불과하며 Android 4.3 (젤리 Bean)에 대 한 개발자 해야 hello Android 권장 해결 방법에 따라 해당 응용 프로그램 tooexplicitly 업데이트 /dev/urandom 또는 /dev/random 엔트로피와 PRNG hello를 초기화 합니다.</li></ul>|

## <a id="stream-ciphers"></a>대칭 스트림 암호화 사용 금지

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 대칭 스트림 암호화(예: RC4)는 사용하지 않아야 합니다. 대칭 스트림 암호화 대신 제품에서 키 길이가 128비트 이상인 AES와 같은 블록 암호화를 사용해야 합니다. |

## <a id="mac-hash"></a>승인된 MAC/HMAC/키 해시 알고리즘 사용

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | <p>제품에서는 승인된 MAC(메시지 인증 코드) 또는 HMAC(해시 기반 메시지 인증 코드) 알고리즘만 사용해야 합니다.</p><p>메시지 인증 코드 (MAC)은 모두 hello hello 발신자의의 신뢰성과 hello 무결성 비밀 키를 사용 하 여 hello 메시지의 받는 사람 tooverify 수 있는 정보 tooa 연결 된 메시지입니다. 어느 해시를 기반으로 MAC 사용 하 여 hello ([HMAC](http://csrc.nist.gov/publications/nistpubs/800-107-rev1/sp800-107-rev1.pdf)) 또는 [블록 암호 기반 MAC](http://csrc.nist.gov/publications/nistpubs/800-38B/SP_800-38B.pdf) 허용 되는 것은 모두 기본 해시 또는 대칭 암호화 알고리즘은도 사용할 수 있도록 승인;이 현재 에 포함 됩니다 (HMAC SHA256, SHA384 HMAC 및 hmac-sha512) HMAC SHA2 함수 hello 및 CMAC/OMAC1 hello 및 OMAC2 (이러한 템플릿은 기반 AES) 암호 기반 Mac을 차단 합니다.</p><p>HMAC SHA1 사용 플랫폼 호환성에 대 한 허용 될 수 있습니다 하지만 있습니다 필요한 toofile 예외 toothis 프로시저 되며 조직의 암호화 검토를 거쳐야 합니다. 128 비트 보다 Hmac tooless의 잘림을 허용 되지 않습니다. 고객 메서드 toohash 키와 데이터를 사용 하 여 승인 되지 않은 및 조직의 Crypto 보드 이전 toouse 검토를 거쳐야 합니다.</p>|

## <a id="hash-functions"></a>승인된 암호화 해시 함수만 사용

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | <p>제품은 hello sha-2 해시 알고리즘 패밀리입니다 (SHA256, SHA384 및 SHA512)를 사용 해야 합니다. 순서 toofit hello 짧은 MD5 해시를 염두에서에 두고 설계 하는 데이터 구조에에서 128 비트 출력 길이 같은 짧은 해시, 필요한 경우 제품 팀 hello SHA2 해시 (일반적으로 SHA256) 중 하나를 잘라낼 수 있습니다. SHA384는 SHA512의 잘린 버전입니다. 보안 목적으로 tooless 128 비트 보다에 대 한 암호화 해시의 잘림을 허용 되지 않습니다. 새 코드는 hello MD2, MD4, MD5, SHA 0, s h A-1 또는 RIPEMD 해시 알고리즘을 사용 하지 마십시오. 해시 충돌은 이러한 알고리즘에 대해 컴퓨터를 통해 실행 가능하며 효과적으로 해독할 수 있습니다.</p><p>관리되는 암호화 민첩성을 위해 허용되는 .NET 해시 알고리즘(기본 설정 순서대로)</p><ul><li>SHA512Cng(FIPS 규격)</li><li>SHA384Cng(FIPS 규격)</li><li>SHA256Cng(FIPS 규격)</li><li>SHA512Managed (FIPS 규격이 아닌) () 사용 하 여 SHA512 호출 tooHashAlgorithm.Create 또는 CryptoConfig.CreateFromName 알고리즘 이름으로</li><li>SHA384Managed (FIPS 규격이 아닌) () 사용 하 여 SHA384 호출 tooHashAlgorithm.Create 또는 CryptoConfig.CreateFromName 알고리즘 이름으로</li><li>SHA256Managed (FIPS 규격이 아닌) () 사용 하 여 s h a 256 호출 tooHashAlgorithm.Create 또는 CryptoConfig.CreateFromName 알고리즘 이름으로</li><li>SHA512CryptoServiceProvider(FIPS 규격)</li><li>SHA256CryptoServiceProvider(FIPS 규격)</li><li>SHA384CryptoServiceProvider(FIPS 규격)</li></ul>| 

## <a id="strong-db"></a>Hello 데이터베이스의 강력한 암호화 알고리즘 tooencrypt 데이터를 사용 합니다.

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 데이터베이스 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [암호화 알고리즘 선택](https://technet.microsoft.com/library/ms345262(v=sql.130).aspx) |
| **단계** | 암호화 알고리즘은 권한이 없는 사용자가 쉽게 바꿀 수 없는 데이터 변환을 정의합니다. SQL Server에서는 DES, Triple DES, TRIPLE_DES_3KEY, RC2, RC4, 128 비트 RC4, DESX, 128 비트 AES, 192 비트 AES 및 256 비트 AES를 비롯 한 여러 알고리즘 중에서 관리자와 개발자가 toochoose |

## <a id="ssis-signed"></a>암호화되고 디지털 서명되어야 하는 SSIS 패키지

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 데이터베이스 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [Hello 디지털 서명으로 패키지의 원본을 식별](https://msdn.microsoft.com/library/ms141174.aspx), [위협 요소 및 취약성 완화 (Integration Services)](https://msdn.microsoft.com/library/bb522559.aspx) |
| **단계** | hello 패키지의 원본이 개별 hello 또는 hello 패키지를 만든 조직입니다. 알 수 없거나 신뢰할 수 없는 원본에서 패키지를 실행하는 것은 위험할 수 있습니다. SSIS 패키지, 변조 tooprevent 무단 디지털 서명을 사용 해야 합니다. 또한 저장소/전송 중 hello 패키지 tooensure hello 기밀성, SSIS 패키지 두 개 toobe 암호화 |

## <a id="securables-db"></a>디지털 서명 toocritical 데이터베이스 보안 개체를 추가 합니다.

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 데이터베이스 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [ADD SIGNATURE(TRANSACT-SQL)](https://msdn.microsoft.com/library/ms181700) |
| **단계** | 중요 한 데이터베이스 보안 개체의 hello 무결성 확인 toobe에 있는 경우에 디지털 서명은 사용 해야 합니다. 저장 프로시저, 함수, 어셈블리 또는 트리거와 같은 데이터베이스 보안 개체는 디지털로 서명할 수 있습니다. 다음은 예의 경우이 유용할 수 있습니다: ISV (Independent Software Vendor)는 해당 고객의 지원 tooa 배달 소프트웨어 tooone 제공를 가정해 보겠습니다. 지원을 제공 하기 전에 hello ISV가 실수로 또는 악의적 시도 하는 데이터베이스 보안 개체에 hello 소프트웨어 손상 되지 않았음을 tooensure를 할 수 있습니다. Hello 보안 디지털 서명 되어 hello ISV 수 디지털 서명을 확인 하 고 무결성의 유효성을 검사 합니다.| 

## <a id="ekm-keys"></a>SQL server EKM tooprotect 암호화 키를 사용 하 여

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 데이터베이스 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [SQL Server EKM(확장 가능 키 관리)](https://msdn.microsoft.com/library/bb895340), [Azure Key Vault(SQL Server)를 사용한 확장 가능 키 관리](https://msdn.microsoft.com/library/dn198405) |
| **단계** | SQL Server 확장 가능 키 관리를 사용 하면 스마트 카드, USB 장치 또는 EKM/HSM 모듈과 같은 외부 장치에 저장 된 hello 데이터베이스 파일 toobe를 보호 하는 hello 암호화 키입니다. 그러면 상태도 (hello sysadmin 그룹의 구성원)을 제외한 데이터베이스 관리자 로부터 데이터 보호. 암호화 키만 hello 데이터베이스 사용자는 액세스 tooon hello 외부 EKM/HSM 모듈을 사용 하 여 데이터를 암호화할 수 있습니다. |

## <a id="keys-engine"></a>암호화 키에는 표시 되 tooDatabase 엔진을 사용 해야 합니다. AlwaysEncrypted 기능을 사용 하 여

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 데이터베이스 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | SQL Azure, 온-프레미스 |
| **특성**              | SQL 버전 - V12, MsSQL2016 |
| **참조**              | [상시 암호화(데이터베이스 엔진)](https://msdn.microsoft.com/library/mt163865) |
| **단계** | 상시 암호화는를 위해 설계 된 기능 tooprotect 중요 한 데이터를 신용 카드 번호나 주민 등록 번호 (예: 미국 사회 보장 번호), Azure SQL 데이터베이스 또는 SQL Server 데이터베이스에 저장 합니다. 항상 암호화 된 클라이언트 tooencrypt 중요 한 클라이언트 응용 프로그램 데이터를 허용 하 고 hello 암호화 키 toohello 데이터베이스 엔진 (SQL 데이터베이스 또는 SQL Server)를 표시 하지 않을 합니다. 결과적으로, 사용자에 게 소유 하는 hello 데이터 (및 대시보드를 볼 수)을 분리 상시 암호화는 고객과 구매할 hello 데이터 관리 (하지만 액세스 권한이 없어야) |

## <a id="keys-iot"></a>IoT 장치에 안전하게 암호화 키 저장

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | IoT 장치 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 장치 OS - Windows IoT Core, 장치 연결 - Azure IoT 장치 SDK |
| **참조**              | [Windows IoT Core의 TPM](https://developer.microsoft.com/windows/iot/docs/tpm)(영문), [Windows IoT Core에서 TPM 설정](https://developer.microsoft.com/windows/iot/win10/setuptpm)(영문), [Azure IoT 장치 SDK TPM](https://github.com/Azure/azure-iot-hub-vs-cs/wiki/Device-Provisioning-with-TPM)(영문) |
| **단계** | 대칭 또는 인증서 개인 키는 TPM 또는 스마트 카드 칩과 같은 하드웨어로 보호된 저장소에 안전하게 보관됩니다. Windows 10 IoT Core tpm hello 사용자 지원 되며 사용할 수 있는 몇 가지 호환 가능한 Tpm: https://developer.microsoft.com/windows/iot/win10/tpm 합니다. 펌웨어 또는 불연속 TPM toouse 것이 좋습니다. 소프트웨어 TPM은 개발 및 테스트 용도로만 사용해야 합니다. Tpm이 설치를 사용할 수 있고 그 안에 hello 키 프로 비전 되 면 hello 토큰을 생성 하는 hello 코드의 중요 정보를 하드 코드 하지 않고 작성 되어야 합니다. | 

### <a name="example"></a>예제
```
TpmDevice myDevice = new TpmDevice(0);
// Use logical device 0 on hello TPM 
string hubUri = myDevice.GetHostName(); 
string deviceId = myDevice.GetDeviceId(); 
string sasToken = myDevice.GetSASToken(); 

var deviceClient = DeviceClient.Create( hubUri, AuthenticationMethodFactory. CreateAuthenticationWithToken(deviceId, sasToken), TransportType.Amqp); 
```
볼 수 있듯이 hello 장치에 대 한 기본 키 hello 코드에 나타나지 않습니다. Hello 슬롯 0에서 TPM에에서 저장 됩니다. TPM 장치에서는 오류가 발생 하는 수명이 짧은 SAS 토큰을 다음 tooconnect toohello IoT 허브를 사용 합니다. 

## <a id="random-hub"></a>충분 한 길이의 인증 tooIoT 허브에 대 한 임의의 대칭 키를 생성 합니다.

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | IoT 클라우드 게이트웨이 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 게이트웨이 선택 - Azure IoT Hub |
| **참조**              | 해당 없음  |
| **단계** | IoT Hub는 장치 ID 레지스트리를 포함하고, 장치를 프로비전하는 동안 임의 대칭 키를 자동으로 생성합니다. Toouse hello Azure IoT 허브 Id 레지스트리에 toogenerate hello 키의이 기능은 인증에 사용 되는 것이 좋습니다. IoT Hub 사용 hello 장치를 만드는 동안 지정 된 키 toobe 수도 있습니다. IoT Hub 외부 장치 프로 비전 하는 동안 한 키를 생성 하는 경우 임의의 대칭 키 또는 256 비트 이상 toocreate 것이 좋습니다. |

## <a id="pin-remote"></a>PIN 사용이 필요하고 원격 지우기를 허용하는 장치 관리 정책이 있는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Dynamics CRM 모바일 클라이언트 | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | PIN 사용이 필요하고 원격 지우기를 허용하는 장치 관리 정책이 있는지 확인합니다. |

## <a id="bitlocker"></a>PIN/암호/자동 잠금이 필요하고 모든 데이터를 암호화(예: Bitlocker)하는 장치 관리 정책이 있는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Dynamics CRM Outlook 클라이언트 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | PIN/암호/자동 잠금이 필요하고 모든 데이터를 암호화(예: Bitlocker)하는 장치 관리 정책이 있는지 확인합니다. |

## <a id="rolled-server"></a>Identity Server를 사용할 때 서명 키가 롤오버되는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | ID 서버 | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [Identity Server - 키, 서명 및 암호화](https://identityserver.github.io/Documentation/docsv2/configuration/crypto.html)(영문) |
| **단계** | Identity Server를 사용할 때 서명 키가 롤오버되는지 확인합니다. hello references 섹션에 hello 링크 Id 서버에 의존 하는 작동 중단 tooapplications 발생 하지 않고이 해야 계획 하는 방법을 설명 합니다. |

## <a id="client-server"></a>Identity Server에서 암호화된 강력한 클라이언트 ID와 클라이언트 비밀이 사용되는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | ID 서버 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | <p>Identity Server에서 암호화된 강력한 클라이언트 ID와 클라이언트 비밀이 사용되는지 확인합니다. 지침에 따라 hello 클라이언트 ID와 암호를 생성 하는 동안 사용 되어야 합니다.</p><ul><li>Hello 클라이언트 ID로 임의 GUID를 생성 합니다.</li><li>Hello 암호로 암호화 된 난수 256 비트 키를 생성 합니다.</li></ul>|
