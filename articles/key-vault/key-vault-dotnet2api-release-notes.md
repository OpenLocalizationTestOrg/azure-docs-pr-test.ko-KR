---
title: "aaaKey 자격 증명 모음.NET 2.x API 릴리스 정보 | Microsoft Docs"
description: ".NET 개발자가이 API toocode을 사용 하 여 Azure 키 자격 증명 모음에 대 한"
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
editor: bruceper
ms.assetid: 1cccf21b-5be9-4a49-8145-483b695124ba
ms.service: key-vault
ms.devlang: CSharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/02/2017
ms.author: bruceper
ms.openlocfilehash: d95b84cf73c155f117f37e93893f27b02a75855c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-net-20---release-notes-and-migration-guide"></a>Azure Key Vault .NET 2.0 - 릴리스 정보 및 마이그레이션 가이드
hello 다음 참고 사항과 지침은 Azure 키 자격 증명 모음.NET을 사용 하는 개발자를 위한 / C# 라이브러리입니다. Hello 전환을 hello 1.0 버전 toohello 2.0 버전에서 업데이트 수가 지정 되었습니다 toobenefit hello 기능 향상에서을 위해에서 코드에서 마이그레이션 작업이 필요한 지와 같은 추가 기능 및은 **키 자격 증명 모음 인증서** 지원 합니다.

## <a name="key-vault-certificates"></a>Key Vault 인증서

주요 자격 증명 모음 인증서 지원을 통해 프로그램 x509의 관리에 대 한 인증서와 동작을 수행 하는 hello:  

* 인증서 소유자 toocreate hello 가져오기 기존 인증서 또는 키 자격 증명 모음 만들기 프로세스를 통해 인증서를 허용합니다. 여기에는 자체 서명된 인증서 및 인증 기관 생성 인증서가 모두 포함됩니다.
* Tooimplement 안전한 저장 및 관리 X509의 주요 자격 증명 모음 인증서 소유자 수 인증서 개인 키 자료와 상호 작용 없이 합니다.  
* 인증서 소유자 toocreate 키 자격 증명 모음 toomanage hello의 수명 주기는 인증서에 지시 하는 정책을 수 있습니다.  
* 인증서 소유자 tooprovide 연락처 정보 알림에 대 한 수명 주기 이벤트에 대 한 만료 및 갱신을 인증서의 수입니다.  
* 선택한 발급자 - Key Vault 파트너 X509 인증서 공급자/인증서 기관을 통한 자동 갱신을 지원합니다.
  
  * NOTE-비 맺은 공급자/기관도 사용할 수 있지만, hello 자동 갱신 기능을 지원 하지 것입니다.

## <a name="net-support"></a>.NET 지원

* **.NET 4.0** hello 2.0 버전의 hello Azure 키 자격 증명 모음.NET에서 지원 되지 않습니다 / C# 라이브러리
* **.NET core** hello 2.0 버전의 hello Azure 키 자격 증명 모음.NET에서 사용할 수 / C# 라이브러리

## <a name="namespaces"></a>네임스페이스

* 네임 스페이스에 대 한 hello **모델** 에서 변경 **Microsoft.Azure.KeyVault** 너무**Microsoft.Azure.KeyVault.Models**합니다.
* hello **Microsoft.Azure.KeyVault.Internal** 네임 스페이스 삭제 됩니다.
* hello Azure SDK 종속성 네임 스페이스에서 변경 된 **Hyak.Common** 및 **Hyak.Common.Internals** 너무**Microsoft.Rest** 및  **Microsoft.Rest.Serialization**

## <a name="type-changes"></a>유형 변경

* *비밀* 너무 변경*SecretBundle*
* *사전* 너무 변경*IDictionary*
* *목록<T>, string* 너무 변경*IList<T>*
* *NextList* 너무 변경 *NextPageLink*

## <a name="return-types"></a>반환 유형

* **KeyList** 및 **SecretList**는 *ListKeysResponseMessage* 대신 *IPage<T>*를 반환합니다.
* 생성 된 hello **BackupKeyAsync** 돌아갑니다 *BackupKeyResult* 포함 된 *값* (백업 blob). 메서드는 hello 전에 래핑된 및 재 가입 hello 값만 했습니다.

## <a name="exceptions"></a>예외

* *KeyVaultClientException* 너무 변경*KeyVaultErrorException*
* hello 서비스 오류 상태에서 변경 될 *예외입니다. 오류* 너무*예외입니다. Body.Error.Message*합니다.
* 추가 정보에 대 한 hello 오류 메시지에서 제거 **[JsonExtensionData]**합니다.

## <a name="constructors"></a>생성자

* 적용 하는 대신는 *HttpClient* 생성자 인수로 hello 생성자만 허용 *HttpClientHandler* 또는 *DelegatingHandler*합니다.

## <a name="downloaded-packages"></a>다운로드한 패키지

주요 자격 증명 모음 hello 다음 다운로드 한 클라이언트에서 종속성을 처리 중인 경우

### <a name="previous-package-list"></a>이전 패키지 목록

* package id="Hyak.Common" version="1.0.2" targetFramework="net45"
* package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"
* package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"
* package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"
* package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"
* package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"
* package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"
* package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"

### <a name="current-package-list"></a>현재 패키지 목록

* package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"
* package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"
* package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"

## <a name="class-changes"></a>클래스 변경

* **UnixEpoch** 클래스가 제거되었습니다.
* **Base64UrlConverter** 클래스 이름이 너무**Base64UrlJsonConverter**

## <a name="other-changes"></a>기타 변경 내용

* Toothis 버전의 hello API의 일시적 오류 KV 작업을 다시 시도 정책은 hello 구성에 대 한 지원이 추가 되었습니다.

## <a name="microsoftazuremanagementkeyvault-nuget"></a>Microsoft.Azure.Management.KeyVault NuGet

* 반환 하는 hello 작업에는 *자격 증명 모음*, hello 반환 형식이 된 자격 증명 모음의 속성을 포함 하는 클래스입니다. hello 반환 형식이 이제 *자격 증명 모음*합니다.
* *PermissionsToKeys* 및 *PermissionsToSecrets*는 이제 *Permissions.Keys* 및 *Permissions.Secrets*입니다.
* 형식 변경 내용은 적용 toohello 제어 평면도 hello 중 일부를 반환 합니다.

## <a name="microsoftazurekeyvaultextensions-nuget"></a>Microsoft.Azure.KeyVault.Extensions NuGet

* hello 패키지 너무 분해할**Microsoft.Azure.KeyVault.Extensions** 및 **Microsoft.Azure.KeyVault.Cryptography** hello 암호화 작업에 대 한 합니다.

