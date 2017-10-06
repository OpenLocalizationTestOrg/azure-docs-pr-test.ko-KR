---
title: "aaaPowerShell 커넥터 | Microsoft Docs"
description: "이 문서에서는 설명 방법을 tooconfigure Microsoft의 Windows PowerShell 커넥터입니다."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6dba8e34-a874-4ff0-90bc-bd2b0a4199b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 44ff6b1f53283000b72e15f861e0f86c21afe12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-powershell-connector-technical-reference"></a>WIndows PowerShell 커넥터 기술 참조
이 문서에서는 Windows PowerShell 커넥터 hello를 설명 합니다. hello 문서 toohello 제품 다음이 적용 됩니다.

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * 핫픽스 4.1.3671.0 이상 [KB3092178](https://support.microsoft.com/kb/3092178)을 사용해야 합니다.

Hello 커넥터 MIM2016 및 FIM2010R2 hello에서 다운로드할 수는 [Microsoft 다운로드 센터](http://go.microsoft.com/fwlink/?LinkId=717495)합니다.

## <a name="overview-of-hello-powershell-connector"></a>Hello PowerShell 커넥터 개요
hello PowerShell 커넥터는 Windows PowerShell 기반 Api를 제공 하는 외부 시스템과 toointegrate hello 동기화 서비스를 수 있습니다. hello 커넥터 2 (ECMA2) 프레임 워크와 Windows PowerShell hello 확장 가능한 연결 호출 기반 관리 에이전트의 hello 기능 사이의 다리를 제공 합니다. Hello ECMA 프레임 워크에 대 한 자세한 내용은 참조 hello [확장 가능한 연결 2.2 관리 에이전트 참조](https://msdn.microsoft.com/library/windows/desktop/hh859557.aspx)합니다.

### <a name="prerequisites"></a>필수 조건
Hello 커넥터를 사용 하기 전에 hello 동기화 서버에 hello 다음 있는지 확인 합니다.

* Microsoft.NET 4.5.2 Framework 이상
* Windows PowerShell 2.0, 3.0 또는 4.0

hello 실행 정책을 hello 동기화 서비스 서버에서 구성 된 tooallow hello 커넥터 toorun Windows PowerShell 스크립트 여야 합니다. 디지털 서명 된 hello 스크립트 hello 커넥터가 실행 된 경우가 아니면이 명령을 실행 하 여 hello 실행 정책을 구성 합니다.  
`Set-ExecutionPolicy -ExecutionPolicy RemoteSigned`

## <a name="create-a-new-connector"></a>새 커넥터 만들기
hello 동기화 서비스에서 Windows PowerShell 커넥터 toocreate 일련의 hello 단계 hello 동기화 서비스에서 요청을 실행 하는 Windows PowerShell 스크립트를 제공 해야 합니다. Hello 데이터 원본 필요한 tooand hello 기능을 연결에 따라 구현 해야 하는 hello 스크립트 달라 집니다. 이 섹션에서는 구현할 수 있으며 필요한 hello 스크립트에 설명 합니다.

hello 커넥터는 Windows PowerShell 디자인 각 toostore hello 동기화 서비스 데이터베이스 내부의 hello 스크립트. 가능한 toorun 스크립트 hello 파일 시스템에 저장 된 상태인 동안에 각 스크립트 toohello 커넥터 구성에서 직접 쉽게 tooinsert hello 본문입니다.

tooCreate PowerShell 커넥터의 **동기화 서비스** 선택 **관리 에이전트** 및 **만들기**합니다. 선택 hello **PowerShell (Microsoft)** 커넥터입니다.

![커넥터 만들기](./media/active-directory-aadconnectsync-connector-powershell/createconnector.png)

### <a name="connectivity"></a>연결
Tooa 원격 시스템에 연결 하기 위한 구성 매개 변수를 제공 합니다. 이러한 값은 안전 하 게 hello 동기화 서비스에 의해 저장 있으며 hello 커넥터를 실행할 때 사용할 수 있는 tooyour Windows PowerShell 스크립트를 수행 합니다.

![연결](./media/active-directory-aadconnectsync-connector-powershell/connectivity.png)

연결 매개 변수 뒤 hello를 구성할 수 있습니다.

**연결**

| 매개 변수 | 기본값 | 목적 |
| --- | --- | --- |
| 서버 |<Blank> |커넥터 hello 서버 이름에 연결 해야 합니다. |
| 도메인 |<Blank> |Hello 커넥터를 실행할 때 사용 하기 위해 자격 증명 toostore hello의 도메인입니다. |
| 사용자 |<Blank> |Hello 커넥터를 실행할 때 사용 하기 위해 자격 증명 toostore hello의 사용자 이름입니다. |
| 암호 |<Blank> |Hello 커넥터를 실행할 때 사용 하기 위해 자격 증명 toostore hello의 암호입니다. |
| 커넥터 계정 가장 |False |True 인 경우 hello 동기화 서비스는 제공 된 hello 자격 증명의 hello 컨텍스트에서 hello Windows PowerShell 스크립트를 실행 합니다. 가능 하면 해당 hello 좋습니다 **$Credentials** 매개 변수가 전달 tooeach 가장 대신 스크립트를 사용 합니다. 추가 사용 권한에 대 한 자세한 내용은 필수 toouse이이 옵션을 참조 [가장에 대 한 추가 구성](#additional-configuration-for-impersonation)합니다. |
| 가장 시 사용자 프로필 로드 |False |가장 하는 동안 Windows hello 커넥터의 자격 증명의 tooload hello 사용자 프로필을 지시합니다. Hello 가장 된 사용자가 로밍 프로필 hello 커넥터 hello 로밍 프로필을 로드 하지 않습니다. 추가 사용 권한에 대 한 자세한 내용은 필수 toouse이 매개이 변수를 참조 [가장에 대 한 추가 구성](#additional-configuration-for-impersonation)합니다. |
| 가장 시 로그온 형식 |없음 |가장하는 동안 로그온 형식입니다. 자세한 내용은 참조 hello [dwLogonType] [ dw] 설명서입니다. |
| 서명된 스크립트만 해당 |False |True 이면 hello Windows PowerShell 커넥터 각 스크립트에는 유효한 디지털 서명이 있는지 확인 합니다. False 인 경우 hello 동기화 서비스 서버의 Windows PowerShell 실행 정책을 RemoteSigned 또는 제한 없음 인지 확인 합니다. |

**일반 모듈**  
hello 커넥터 hello 구성에 공유 Windows PowerShell 모듈 toostore를 허용합니다. 스크립트를 실행 하는 hello 커넥터, hello Windows PowerShell 모듈은 추출 toohello 파일 시스템 각 스크립트에서 가져올 수 있도록 합니다.

가져오기, 내보내기 및 암호 동기화 스크립트에 대 한 일반적인 모듈 hello는 추출 된 toohello 커넥터의 MAData 폴더입니다. 스키마, 유효성 검사, 계층 및 파티션 검색 스크립트에 대 한 hello 일반적인 모듈이 경우 압축 푼된 toohello % TEMP % 폴더 두 경우 모두 hello toohello 일반 모듈 스크립트 이름 설정에 따라 스크립트 라는 공용 모듈을 추출 합니다.

tooload 모듈 hello MAData 폴더에서 FIMPowerShellConnectorModule.psm1 호출 문 다음 hello를 사용 합니다.`Import-Module (Join-Path -Path [Microsoft.MetadirectoryServices.MAUtils]::MAFolder -ChildPath "FIMPowerShellConnectorModule.psm1")`

모듈 tooload hello % TEMP % 폴더에서 FIMPowerShellConnectorModule.psm1 호출 문 다음 hello를 사용 합니다.`Import-Module (Join-Path -Path $env:TEMP -ChildPath "FIMPowerShellConnectorModule.psm1")`

**매개 변수 유효성 검사**  
hello 유효성 검사 스크립트에서 관리자에 게 제공 하는 커넥터 구성 매개 변수가 유효한 지 사용 되는 tooensure 일 수 있는 선택적 Windows PowerShell 스크립트입니다. 유효성 검사 서버, 연결 자격 증명 및 연결 매개 변수는 hello 유효성 검사 스크립트의 일반적인 사용 합니다. hello 유효성 검사 스크립트 라고 hello 다음과 같은 탭과 대화 상자는 수정 후:

* 연결
* 글로벌 매개 변수
* 파티션 구성

hello 유효성 검사 스크립트 hello hello 커넥터에서 매개 변수를 다음을 수신 합니다.

| 이름 | 데이터 형식 | 설명 |
| --- | --- | --- |
| ConfigParameterPage |[ConfigParameterPage][cpp] |hello 구성 탭 이나 hello 유효성 검사 요청을 트리거한 대화 상자. |
| ConfigParameters |[KeyedCollection][keyk] [string, [ConfigParameter][cp]] |테이블 hello 커넥터에 대 한 구성 매개 변수입니다. |
| 자격 증명 |[PSCredential][pscred] |Hello 연결 탭에서 관리자에 게가 입력 한 자격 증명을 포함 합니다. |

hello 유효성 검사 스크립트는 단일 ParameterValidationResult 개체 toohello 파이프라인을 반환 해야 합니다.

**스키마 검색**  
hello 스키마 검색 스크립트는 필수입니다. 이 스크립트는 hello 특성 흐름 규칙을 구성할 때 동기화 서비스에 사용 하 여 hello 개체 유형, 특성 및 특성 제약 조건을 반환 합니다. 스키마 검색 스크립트 hello 커넥터를 만드는 동안 실행 하 여 hello 커넥터의 스키마를 채웁니다. 또한 hello hello 동기화 서비스 관리자에서에서 스키마 새로 고침 작업 에서도 사용 합니다.

hello 스키마 검색 스크립트 hello hello 커넥터에서 매개 변수를 다음을 수신 합니다.

| 이름 | 데이터 형식 | 설명 |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk] [string, [ConfigParameter][cp]] |테이블 hello 커넥터에 대 한 구성 매개 변수입니다. |
| 자격 증명 |[PSCredential][pscred] |Hello 연결 탭에서 관리자에 게가 입력 한 자격 증명을 포함 합니다. |

hello 스크립트는 단일 반환 해야 [스키마] [ schema] 개체 toohello 파이프라인. hello 스키마 개체는 구성 되어 [SchemaType] [ schemaT] 개체 형식을 나타내는 개체 (예: 사용자 및 그룹). hello SchemaType 개체의 컬렉션을 보유 [SchemaAttribute] [ schemaA] hello 특성을 나타내는 개체 (예: 지정 된 이름, 성 및 우편 주소) hello 유형입니다.

**추가 매개 변수**  
또한 toohello 표준 구성 설정은 hello 커넥터의 특정 toohello 인스턴스 추가 사용자 지정 구성 설정을 정의할 수 있습니다. Hello 커넥터, 파티션에서 이러한 매개 변수를 지정할 수 있습니다 또는 실행된 단계의 수준 및 hello 관련 Windows PowerShell 스크립트에서 액세스 합니다. 사용자 지정 구성 설정을 일반 텍스트 형식의 hello 동기화 서비스 데이터베이스에 저장 하거나 암호화할 수 있습니다. hello 동기화 서비스는 자동으로 암호화 하 고 필요한 경우 보안 구성 설정을 해독 합니다.

각 매개 변수는 쉼표 (,)로 별도 hello 이름 toospecify 사용자 지정 구성 설정입니다.

스크립트에서 사용자 지정 구성 설정을 tooaccess hello 이름에 밑줄 접미사 해야 합니다 ( \_ ) 및 hello 범위 (Global, 파티션 또는 RunStep) hello 매개 변수입니다. 예를 들어 tooaccess hello 글로벌 파일 이름 매개 변수,이 코드 조각을 사용:`$ConfigurationParameters["FileName_Global"].Value`

### <a name="capabilities"></a>기능
관리 에이전트 디자이너 hello hello 기능 탭 hello 커넥터의 hello 동작 및 기능을 정의합니다. hello 커넥터를 만들 때이 탭에서 변경한 hello 선택 항목을 수정할 수 없습니다. 이 표에서 hello 기능 설정을 보여 줍니다.

![기능](./media/active-directory-aadconnectsync-connector-powershell/capabilities.png)

| 기능 | 설명 |
| --- | --- |
| [고유 이름 스타일][dnstyle] |Hello 커넥터 고유 이름을 지원 하 고, 어떤 스타일 경우를 나타냅니다. |
| [내보내기 형식][exportT] |Toohello 내보내기 스크립트에 표시 되는 개체의 hello 유형을 결정 합니다. <li>AttributeReplace – hello 특성 변경 될 때 hello 전체 다중 값된 특성에 대 한 값 집합을 포함 합니다.</li><li>AttributeUpdate – hello 특성 변경 될 때만 hello 델타 tooa 다중 값된 특성을 포함 합니다.</li><li>MultivaluedReferenceAttributeUpdate - 비참조 다중값 특성에 대한 값의 전체 집합과 다중값 참조 특성에 대한 델타만 포함합니다.</li><li>ObjectReplace – 특성을 변경하는 경우 개체에 대한 모든 특성을 포함합니다.</li> |
| [데이터 정규화][DataNorm] |Tooscripts 제공 되는 전에 hello 동기화 서비스 toonormalize 앵커 특성을 지시 합니다. |
| [개체 확인][oconf] |Hello 동기화 서비스에서에서 가져오기 동작 보류 중인 hello를 구성합니다. <li>보통-가져오기를 통해 확인 되는 모든 내보낸된 변경 toobe를 필요로 하는 기본 동작</li><li>NoDeleteConfirmation – 개체를 삭제하면 생성 보류 중인 가져오기 작업이 없습니다.</li><li>NoAddAndDeleteConfirmation – 개체를 생성하거나 삭제하면 생성 보류 중인 가져오기 작업이 없습니다.</li> |
| 앵커로 DN 사용 |Hello 고유 이름 스타일 tooLDAP을 설정 하는 경우 hello 커넥터 공간에 대 한 hello 앵커 특성 hello 고유 이름 이기도 합니다. |
| 여러 커넥터의 동시 작업 |옵션을 선택하면 여러 Windows PowerShell 커넥터는 동시에 실행할 수 있습니다. |
| 파티션 |옵션을 선택 하면 hello 커넥터 여러 파티션 및 파티션 검색을 지원 합니다. |
| 계층 구조 |옵션을 선택 하면 hello 커넥터 LDAP 스타일 계층 구조를 지원 합니다. |
| 가져오기 사용 |옵션을 선택 하면 hello 커넥터 가져오기 스크립트를 통해 데이터를 가져옵니다. |
| 델타 가져오기 사용 |옵션을 선택 하면 델타 hello에서 스크립트를 가져오는 hello 커넥터 요청할 수 있습니다. |
| 내보내기 사용 |이 옵션을 선택 하는 경우 hello 커넥터 내보내기 스크립트를 통해 데이터를 내보냅니다. |
| 전체 내보내기 사용 |옵션을 선택 하면 hello hello 전체 커넥터 공간 내보내기 스크립트 지원을 내보냅니다. toouse 내보내기 사용 하도록 설정 하는이 옵션을 선택 해야 합니다. |
| 첫 번째 내보내기 단계에서 참조 값 없음 |옵션을 선택하면 두 번째 내보내기 과정에서 참조 특성을 내보냅니다. |
| 개체 이름 바꾸기 사용 |옵션을 선택하면 고유 이름을 수정할 수 있습니다. |
| 바꾸기로 삭제-추가 |옵션을 선택하면 삭제-추가 작업이 단일 교체로 내보내집니다. |
| 암호 작업 사용 |옵션을 선택하면 암호 동기화 스크립트가 지원됩니다. |
| 첫 번째 패스에서 암호 내보내기 사용 |옵션을 선택 하면 프로 비전 하는 동안 설정 된 암호는 hello 개체를 만들 때 내보내집니다. |

### <a name="global-parameters"></a>글로벌 매개 변수
hello 관리 에이전트 디자이너의에서 hello 글로벌 매개 변수 탭을 사용 하면 hello 커넥터에서 실행 되는 tooconfigure hello Windows PowerShell 스크립트 있습니다. 또한 hello 연결 탭에 정의 된 사용자 지정 구성 설정에 대 한 전역 값을 구성할 수 있습니다.

**파티션 검색**  
파티션은 하나의 공유 스키마 내에서 별도의 네임스페이스입니다. 예를 들어 Active Directory에서 모든 도메인은 한 포리스트 내의 파티션입니다. 되는 가져오기에 대 한 논리적 그룹화 hello 및 내보내기 작업 합니다. 가져오기 및 내보내기에는 파티션이 컨텍스트로 존재하고 모든 작업은 이 컨텍스트에서 발생합니다. 파티션을은 LDAP에 toorepresent 계층 예정입니다. 파티션의 고유 이름 hello 파티션의 hello 범위 내에서 개체는 모두 반환 하는 가져오기 tooverify에 사용 됩니다. hello 파티션의 고유 이름 구축 파티션에서 hello 메타 버스 toohello 커넥터 공간 toodetermine hello 내보내는 동안 개체와 연결 해야 하는 동안도 사용 됩니다.

hello 파티션 검색 스크립트 hello hello 커넥터에서 매개 변수를 다음을 수신 합니다.

| 이름 | 데이터 형식 | 설명 |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |테이블 hello 커넥터에 대 한 구성 매개 변수입니다. |
| 자격 증명 |[PSCredential][pscred] |Hello 연결 탭에서 관리자에 게가 입력 한 자격 증명을 포함 합니다. |

hello 스크립트 반환 해야는 단일 [파티션] [ part] 개체 또는 파티션 개체 toohello 파이프라인의 목록을 [T].

**계층 구조 검색**  
hello 계층 구조 검색 스크립트는 LDAP 고유 이름 스타일 기능 hello 하는 경우에 사용 됩니다. hello 스크립트에 사용 되는 tooallow toobrowse 하 고 선택 또는 범위에 속하지 하다 고 판단 되는 컨테이너 집합 가져오기 및 내보내기 작업입니다. hello 스크립트 hello 루트 노드 제공 toohello 스크립트의 직접 자식 노드의 목록을 제공 해야 합니다.

hello 계층 구조 검색 스크립트 hello hello 커넥터에서 매개 변수를 다음을 수신 합니다.

| 이름 | 데이터 형식 | 설명 |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |테이블 hello 커넥터에 대 한 구성 매개 변수입니다. |
| 자격 증명 |[PSCredential][pscred] |Hello 연결 탭에서 관리자에 게가 입력 한 자격 증명을 포함 합니다. |
| ParentNode |[HierarchyNode][hn] |hello는 hello 아래 스크립트 직계 자식만 반환 해야 하는 hello 계층의 루트 노드. |

hello 스크립트는 단일 자식 HierarchyNode 개체 또는 자식 HierarchyNode 개체 toohello 파이프라인의 목록을 [T] 중 하나를 반환 해야 합니다.

#### <a name="import"></a>가져오기
가져오기 작업을 지원하는 커넥터는 세 가지 스크립트를 구현해야 합니다.

**가져오기 시작**  
hello 가져오기를 시작 스크립트를 실행 하는 가져오기 단계 hello 맨 앞에서 실행 됩니다. 이 단계에서는 연결 toohello 원본 시스템을 설정할 수 있으며 시스템 연결 hello에서 데이터를 가져오기 전에 준비 단계를 수행 수 있습니다.

hello 가져오기를 시작 스크립트 hello 커넥터에서 매개 변수 뒤 hello를 받습니다.

| 이름 | 데이터 형식 | 설명 |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |테이블 hello 커넥터에 대 한 구성 매개 변수입니다. |
| 자격 증명 |[PSCredential][pscred] |Hello 연결 탭에서 관리자에 게가 입력 한 자격 증명을 포함 합니다. |
| OpenImportConnectionRunStep |[OpenImportConnectionRunStep][oicrs] |Hello 유형 가져오기 실행 (델타 또는 전체), 파티션, 계층, 워터 마크 및 예상된 페이지 크기에 대 한 hello 스크립트를 알립니다. |
| 형식 |[Schema][schema] |가져온 hello 커넥터 공간에 대 한 스키마입니다. |

hello 스크립트는 단일 반환 해야 [OpenImportConnectionResults] [ oicres] toohello 파이프라인을 예를 들어 개체:`Write-Output (New-Object Microsoft.MetadirectoryServices.OpenImportConnectionResults)`

**데이터 가져오기**  
hello 스크립트 없습니다 자세한 데이터 tooimport 임을 나타냅니다 될 때까지 데이터 스크립트를 가져오기 하는 hello hello 커넥터에서 호출 됩니다. Windows PowerShell 커넥터 hello 9, 999 개체의 페이지 크기를 있습니다. 스크립트가 가져오기에 9,999개 이상의 개체를 반환하면 페이징을 지원해야 합니다. hello 커넥터 각 시간 hello 데이터 스크립트를 가져올 수 있도록 tooa 저장소 워터 마크를 사용할 수 있는 사용자 지정 데이터 속성을 노출 스크립트 중단 된 개체를 가져오고 다시 시작 합니다.

hello 데이터 스크립트 가져오기 hello hello 커넥터에서 매개 변수를 다음을 수신 합니다.

| 이름 | 데이터 형식 | 설명 |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |테이블 hello 커넥터에 대 한 구성 매개 변수입니다. |
| 자격 증명 |[PSCredential][pscred] |Hello 연결 탭에서 관리자에 게가 입력 한 자격 증명을 포함 합니다. |
| GetImportEntriesRunStep |[ImportRunStep][irs] |델타 가져오기 및 보류 hello 워터 마크 (CustomData) 페이징된 가져오기 중에 사용할 수 있는 합니다. |
| OpenImportConnectionRunStep |[OpenImportConnectionRunStep][oicrs] |Hello 유형 가져오기 실행 (델타 또는 전체), 파티션, 계층, 워터 마크 및 예상된 페이지 크기에 대 한 hello 스크립트를 알립니다. |
| 형식 |[Schema][schema] |가져온 hello 커넥터 공간에 대 한 스키마입니다. |

hello 가져오기 데이터 스크립트를 작성 해야 목록 [[CSEntryChange][csec]] 개체 toohello 파이프라인. 이 컬렉션은 가져오는 각 개체를 나타내는 CSEntryChange 특성으로 구성됩니다. 전체 가져오기를 실행하는 동안 이 컬렉션에는 모든 개체에 대한 속성을 모두 가진 CSEntryChange 개체의 전체 집합이 있어야 합니다. 델타 가져오기 작업 중 hello CSEntryChange 개체 하거나 각 개체 tooimport 또는 (대체 모드) 변경 된 hello 개체의 전체 표시에 대 한 hello 특성 수준 델타를 포함 해야 합니다.

**최종 가져오기**  
실행 하는 hello 가져오기의 hello 결론 시 hello 스크립트 끝 가져오기 실행 됩니다. 이 스크립트는 모든 정리 필요한 작업 (예: 연결 닫기 toosystems 및 응답 toofailures)를 수행 해야 합니다.

hello 끝 가져오기 스크립트 hello hello 커넥터에서 매개 변수를 다음을 수신 합니다.

| 이름 | 데이터 형식 | 설명 |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |테이블 hello 커넥터에 대 한 구성 매개 변수입니다. |
| 자격 증명 |[PSCredential][pscred] |Hello 연결 탭에서 관리자에 게가 입력 한 자격 증명을 포함 합니다. |
| OpenImportConnectionRunStep |[OpenImportConnectionRunStep][oicrs] |Hello 유형 가져오기 실행 (델타 또는 전체), 파티션, 계층, 워터 마크 및 예상된 페이지 크기에 대 한 hello 스크립트를 알립니다. |
| CloseImportConnectionRunStep |[CloseImportConnectionRunStep][cecrs] |Hello 가져오기 종료 된 hello 원인에 대 한 hello 스크립트를 알립니다. |

hello 스크립트는 단일 반환 해야 [CloseImportConnectionResults] [ cicres] toohello 파이프라인을 예를 들어 개체:`Write-Output (New-Object Microsoft.MetadirectoryServices.CloseImportConnectionResults)`

#### <a name="export"></a>내보내기
Hello 커넥터의 동일한 toohello 가져오기 아키텍처, 내보내기를 지원 커넥터 세 가지 스크립트를 구현 해야 합니다.

**내보내기 시작**  
hello 내보내기를 시작 스크립트 내보내기 실행 단계의 hello 시작 부분에서 실행 됩니다. 이 단계에서는 연결 toohello 원본 시스템을 설정할 수 있으며 시스템 연결 데이터 toohello 내보내기 전에 모든 준비 단계를 수행할 수 있습니다.

hello 내보내기를 시작 스크립트 hello 커넥터에서 매개 변수 뒤 hello를 받습니다.

| 이름 | 데이터 형식 | 설명 |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |테이블 hello 커넥터에 대 한 구성 매개 변수입니다. |
| 자격 증명 |[PSCredential][pscred] |Hello 연결 탭에서 관리자에 게가 입력 한 자격 증명을 포함 합니다. |
| OpenExportConnectionRunStep |[OpenExportConnectionRunStep][oecrs] |Hello 유형의 내보내기 실행 (델타 또는 전체), 파티션, 계층 및 예상된 페이지 크기에 대 한 hello 스크립트를 알립니다. |
| 형식 |[Schema][schema] |내보내는 hello 커넥터 공간에 대 한 스키마입니다. |

hello 스크립트 출력 toohello 파이프라인을 반환 해야 합니다.

**데이터 내보내기**  
hello 동기화 서비스는 필요한 tooprocess 모든 보류 중인 내보내기 횟수 만큼 hello 데이터 내보내기 스크립트를 호출 합니다. Hello 커넥터 공간 hello 커넥터의 페이지 크기 보다 더 많은 보류 중인 내보내기 있으면 hello 내보내기 데이터 스크립트에 여러 번 호출할 수 있습니다 및에 대 한 가능한 여러 번 hello 동일한 개체입니다.

hello 내보내기 데이터 스크립트 hello hello 커넥터에서 매개 변수를 다음을 수신 합니다.

| 이름 | 데이터 형식 | 설명 |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |테이블 hello 커넥터에 대 한 구성 매개 변수입니다. |
| 자격 증명 |[PSCredential][pscred] |Hello 연결 탭에서 관리자에 게가 입력 한 자격 증명을 포함 합니다. |
| CSEntries |IList[CSEntryChange][csec] |모든 hello 커넥터 공간 개체를이 단계 중 처리 된 내보내기 toobe 보류 중인의 목록입니다. |
| OpenExportConnectionRunStep |[OpenExportConnectionRunStep][oecrs] |Hello 유형의 내보내기 실행 (델타 또는 전체), 파티션, 계층 및 예상된 페이지 크기에 대 한 hello 스크립트를 알립니다. |
| 형식 |[Schema][schema] |내보내는 hello 커넥터 공간에 대 한 스키마입니다. |

hello 내보내기 데이터 스크립트 반환 해야 합니다는 [PutExportEntriesResults] [ peeres] 개체 toohello 파이프라인. 이 개체는 오류 또는 toohello 앵커 특성을 변경 하는 발생 하지 않는 한 tooinclude 결과 정보 내보낸된 각 커넥터에 대 한 필요 하지 않습니다. 예를 들어 tooreturn PutExportEntriesResults 개체 toohello 파이프라인:`Write-Output (New-Object Microsoft.MetadirectoryServices.PutExportEntriesResults)`

**최종 내보내기**  
Hello 결론 hello 내보내기의 실행을 hello 스크립트 toorun 끝 내보내기. 이 스크립트는 모든 정리 필요한 작업 (예: 연결 닫기 toosystems 및 응답 toofailures)를 수행 해야 합니다.

hello 끝 내보내기 스크립트 hello hello 커넥터에서 매개 변수를 다음을 수신 합니다.

| 이름 | 데이터 형식 | 설명 |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |테이블 hello 커넥터에 대 한 구성 매개 변수입니다. |
| 자격 증명 |[PSCredential][pscred] |Hello 연결 탭에서 관리자에 게가 입력 한 자격 증명을 포함 합니다. |
| OpenExportConnectionRunStep |[OpenExportConnectionRunStep][oecrs] |Hello 유형의 내보내기 실행 (델타 또는 전체), 파티션, 계층 및 예상된 페이지 크기에 대 한 hello 스크립트를 알립니다. |
| CloseExportConnectionRunStep |[CloseExportConnectionRunStep][cecrs] |Hello 내보내기가 종료 된 hello 원인에 대 한 hello 스크립트를 알립니다. |

hello 스크립트 출력 toohello 파이프라인을 반환 해야 합니다.

#### <a name="password-synchronization"></a>암호 동기화
Windows PowerShell 커넥터는 암호 변경/재설정에 대한 대상으로 사용될 수 있습니다.

hello 암호 스크립트 hello hello 커넥터에서 매개 변수를 다음을 수신 합니다.

| 이름 | 데이터 형식 | 설명 |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |테이블 hello 커넥터에 대 한 구성 매개 변수입니다. |
| 자격 증명 |[PSCredential][pscred] |Hello 연결 탭에서 관리자에 게가 입력 한 자격 증명을 포함 합니다. |
| 파티션 |[파티션][part] |CSEntry hello 디렉터리 파티션에입니다. |
| CSEntry |[CSEntry][cse] |커넥터 공간 항목은 hello 개체에 대 한 암호 변경 또는 다시 설정 받았습니다. |
| OperationType |문자열 |Hello 작업은 기본 설정 인지 여부를 나타냅니다 (**SetPassword**) 또는 변경 (**ChangePassword**). |
| PasswordOptions |[PasswordOptions][pwdopt] |Hello를 지정 하는 플래그는 암호 재설정 동작 것입니다. 이 매개 변수는 OperationType이 **SetPassword**인 경우에만 사용할 수 있습니다. |
| OldPassword |문자열 |암호 변경에 대 한 hello 개체의 현재 암호도 채워집니다. 이 매개 변수는 OperationType이 **ChangePassword**인 경우에만 사용할 수 있습니다. |
| NewPassword |문자열 |Hello 스크립트 설정 해야 하는 hello 개체의 새 암호도 채워집니다. |

hello 암호 스크립트는 예상된 되지 tooreturn 결과 toohello Windows PowerShell 파이프라인. Hello 암호 스크립트에서 오류가 발생 하는 경우 hello 스크립트 hello hello 문제에 대 한 예외 tooinform hello 동기화 서비스를 다음 중 하나를 throw 해야 합니다.

* [PasswordPolicyViolationException] [ pwdex1] – hello 암호 hello 연결 된 시스템의 hello 암호 정책을 충족 하지 않는 경우 Throw 됩니다.
* [PasswordIllFormedException] [ pwdex2] – hello 암호 hello 연결 된 시스템에 대 한 허용 되지 않는 경우 Throw 됩니다.
* [PasswordExtension] [ pwdex3] – hello 암호 스크립트의 다른 모든 오류에 대해 발생 합니다.

## <a name="sample-connectors"></a>샘플 커넥터
Hello 사용할 수 있는 샘플 커넥터의 전체 목록은 참조 하십시오. [Windows PowerShell 커넥터 샘플 커넥터 컬렉션][samp]합니다.

## <a name="other-notes"></a>기타 참고 사항
### <a name="additional-configuration-for-impersonation"></a>가장에 대한 추가 구성
Hello 사용자의 구성이 personated hello hello 동기화 서비스 서버에 대 한 다음 권한을 부여 합니다.

읽기 액세스 toohello 다음 레지스트리 키:

* HKEY_USERS\\[SynchronizationServiceServiceAccountSID]\Software\Microsoft\PowerShell
* HKEY_USERS\\[SynchronizationServiceServiceAccountSID]\Environment

toodetermine hello SID (보안 식별자) hello 동기화 서비스 서비스 계정, hello 다음 PowerShell 명령을 실행 합니다.

```
$account = New-Object System.Security.Principal.NTAccount "<domain>\<username>"
$account.Translate([System.Security.Principal.SecurityIdentifier]).Value
```

읽기 액세스 toohello 다음 파일 시스템 폴더:

* %ProgramFiles%\Microsoft Forefront Identity Manager\2010\Synchronization Service\Extensions
* %ProgramFiles%\Microsoft Forefront Identity Manager\2010\Synchronization Service\ExtensionsCache
* %ProgramFiles%\Microsoft Forefront Identity Manager\2010\Synchronization Service\MaData\\{ConnectorName}

Hello {connectorname은 (는) 자리 표시자에 대 한 hello 이름을 hello Windows PowerShell 커넥터를 대체 합니다.

## <a name="troubleshooting"></a>문제 해결
* 참조 hello tooenable 로깅 tootroubleshoot 커넥터 hello 하는 방법에 대 한 내용은 [어떻게 커넥터에 대 한 ETW 추적 tooEnable](http://go.microsoft.com/fwlink/?LinkId=335731)합니다.

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[cpp]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.configparameterpage.aspx
[keyk]: https://msdn.microsoft.com/library/ms132438.aspx
[cp]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.configparameter.aspx
[pscred]: https://msdn.microsoft.com/library/system.management.automation.pscredential.aspx
[schema]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.schema.aspx
[schemaT]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.schematype.aspx
[schemaA]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.schemaattribute.aspx
[dnstyle]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.madistinguishednamestyle.aspx
[exportT]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.maexporttype.aspx
[DataNorm]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.manormalizations.aspx
[oconf]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.maobjectconfirmation.aspx
[dw]: https://msdn.microsoft.com/library/windows/desktop/aa378184.aspx
[part]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.partition.aspx
[hn]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.hierarchynode.aspx
[oicrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.openimportconnectionrunstep.aspx
[cecrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.closeexportconnectionrunstep.aspx
[oicres]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.openimportconnectionresults.aspx
[cecrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.closeexportconnectionrunstep.aspx
[cicres]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.closeimportconnectionresults.aspx
[oecrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.openexportconnectionrunstep.aspx
[irs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.importrunstep.aspx
[cse]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.csentry.aspx
[csec]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.csentrychange.aspx
[peeres]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.putexportentriesresults.aspx
[pwdopt]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordoptions.aspx
[pwdex1]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordpolicyviolationexception.aspx
[pwdex2]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordillformedexception.aspx
[pwdex3]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordextensionexception.aspx
[samp]: http://go.microsoft.com/fwlink/?LinkId=394291
