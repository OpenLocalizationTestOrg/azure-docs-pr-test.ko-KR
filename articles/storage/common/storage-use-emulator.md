---
title: "개발 및 테스트에 대 한 aaaUse hello Azure 저장소 에뮬레이터 | Microsoft Docs"
description: "hello Azure 저장소 에뮬레이터는 개발 및 Azure 저장소 응용 프로그램을 테스트 하기 위한 가능한 로컬 개발 환경을 제공 합니다. 인증 요청은 어떻게은 자세한 방법을 toouse hello 명령줄 도구 및 응용 프로그램에서 tooconnect toohello 에뮬레이터입니다."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: f480b059-df8a-4a63-b05a-7f2f5d1f5c2a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: marsma
ms.openlocfilehash: 7cbe6ef5f172bb526c9d8a329b2fe9e6c0ec59d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-storage-emulator-for-development-and-testing"></a>Hello Azure 저장소 에뮬레이터를 사용 하 여 개발 및 테스트

Microsoft Azure 저장소 에뮬레이터 hello hello Azure Blob, 큐 및 테이블 서비스를 개발 목적으로 에뮬레이트하는 로컬 환경을 제공 합니다. Hello 저장소 에뮬레이터를 사용 하 여 Azure 구독을 만들거나 모든 비용이 발생 하지 않고 로컬에 hello 저장소 서비스에 대해 응용 프로그램을 테스트할 수 있습니다. Hello 에뮬레이터에서 응용 프로그램이 작동 방식을 만족 스 러 우면 toousing hello 클라우드에서 Azure 저장소 계정을 전환할 수 있습니다.

## <a name="get-hello-storage-emulator"></a>저장소 에뮬레이터 hello 가져오기
hello 저장소 에뮬레이터를 사용할 수 hello의 일부로 [Microsoft Azure SDK](https://azure.microsoft.com/downloads/)합니다. Hello를 사용 하 여 hello 저장소 에뮬레이터를 설치할 수도 있습니다 [독립 실행형 설치 관리자](https://go.microsoft.com/fwlink/?linkid=717179&clcid=0x409) (직접 다운로드). tooinstall hello 저장소 에뮬레이터를 컴퓨터에 관리자 권한이 있어야 합니다.

hello 저장소 에뮬레이터는 현재 Windows에만 실행 됩니다. Linux 용 저장소 에뮬레이터에서 앱을 고려할 것에 대 한 한 가지 옵션은 오픈 소스 저장소 에뮬레이터를 유지 하는 hello 커뮤니티 [Azurite](https://github.com/arafato/azurite)합니다.

> [!NOTE]
> Hello 저장소 에뮬레이터의 특정 버전에서 만든 데이터 보장 되지 않습니다 toobe 액세스할 수 있는 다른 버전을 사용 하는 경우. Hello 장기에 대 한 데이터 toopersist 경우 아니라 hello 저장소 에뮬레이터는 Azure 저장소 계정에 해당 데이터를 저장 하는 것이 좋습니다.
> <p/>
> hello 저장소 에뮬레이터의 hello OData 라이브러리는 특정 버전에 따라 달라 집니다. 다른 버전과 함께 hello 저장소 에뮬레이터 사용 하는 hello OData Dll 지원 되지 않는 바꾸고 예기치 않은 동작이 발생할 수 있습니다. 그러나 hello 저장소 서비스에서 지 원하는 OData의 모든 버전에 사용 되는 toosend 요청 toohello 에뮬레이터 수 있습니다.
>

## <a name="how-hello-storage-emulator-works"></a>Hello 저장소 에뮬레이터의 작동 원리
hello 저장소 에뮬레이터 로컬 Microsoft SQL Server 인스턴스 및 hello 로컬 파일 시스템 tooemulate Azure 저장소 서비스를 사용합니다. 기본적으로 hello 저장소 에뮬레이터는 Microsoft SQL Server 2012 Express LocalDB에서 데이터베이스를 사용합니다. Tooconfigure hello 저장소 에뮬레이터 tooaccess hello LocalDB 인스턴스 대신 SQL Server의 로컬 인스턴스를 선택할 수 있습니다. 자세한 내용은 참조 hello [시작 및 초기화 hello 저장소 에뮬레이터](#start-and-initialize-the-storage-emulator) 이 문서의 뒷부분에 나오는 섹션.

저장소 에뮬레이터 hello tooSQL 서버 또는 Windows 인증을 사용 하 여 LocalDB에 연결 합니다.

몇 가지 기능에서 차이점이 hello 저장소 에뮬레이터와 Azure 저장소 서비스. 이러한 차이점에 대 한 자세한 내용은 참조 hello [hello 저장소 에뮬레이터와 Azure 저장소의 차이점](#differences-between-the-storage-emulator-and-azure-storage) 이 문서의 뒷부분에 나오는 섹션.

## <a name="start-and-initialize-hello-storage-emulator"></a>시작 및 hello 저장소 에뮬레이터를 초기화 합니다.
toostart hello Azure 저장소 에뮬레이터:
1. 선택 hello **시작** 단추를 클릭 하거나 눌러 hello **Windows** 키입니다.
1. `Azure Storage Emulator`를 입력하여 시작합니다.
1. 표시 된 응용 프로그램의 hello 목록에서 hello 에뮬레이터를 선택 합니다.

Hello 저장소 에뮬레이터를 시작 하는 경우에 명령 프롬프트 창이 표시 됩니다. 이 콘솔 창 toostart 및 중지 hello 저장소 에뮬레이터를 사용 하 여 데이터 지우기 및 상태를 가져오기 hello 에뮬레이터를 초기화할 수 있습니다. 자세한 내용은 참조 hello [저장소 에뮬레이터 명령줄 도구 참조](#storage-emulator-command-line-tool-reference) 이 문서의 뒷부분에 나오는 섹션.

Hello 에뮬레이터를 실행 하는 경우에 hello Windows 작업 표시줄 알림 영역에서에서 아이콘을 표시 됩니다.

Hello 저장소 에뮬레이터 명령 프롬프트 창의 닫을 때 hello 저장소 에뮬레이터 toorun을 계속 됩니다. 저장소 에뮬레이터 콘솔 창을 hello toobring 다시 hello hello 저장소 에뮬레이터를 시작 하는 경우 이전 단계를 따릅니다.

hello 처음 hello 저장소 에뮬레이터를 실행 하면 hello 로컬 저장소 환경이 자동으로 초기화 됩니다. hello 초기화 프로세스 LocalDB에서 데이터베이스를 만들고 각 로컬 저장소 서비스에 대 한 HTTP 포트를 예약 합니다.

hello 저장소 에뮬레이터는 기본적으로 설치 너무`C:\Program Files (x86)\Microsoft SDKs\Azure\Storage Emulator`합니다.

> [!TIP]
> Hello를 사용할 수 있습니다 [Microsoft Azure 저장소 탐색기](http://storageexplorer.com) toowork 로컬 저장소 에뮬레이터 리소스입니다. 트리를 확인 "(개발)"에 대 한 "저장소 계정"으로 hello 저장소 탐색기 리소스를 설치 하 고 hello 저장소 에뮬레이터를 시작한 후입니다.
>

### <a name="initialize-hello-storage-emulator-toouse-a-different-sql-database"></a>Hello 저장소 에뮬레이터 toouse 다른 SQL 데이터베이스를 초기화 합니다.
Hello 저장소 에뮬레이터 명령줄 도구 tooinitialize hello 저장소 에뮬레이터 toopoint tooa SQL 데이터베이스 인스턴스 이외의 hello 기본 LocalDB 인스턴스를 사용할 수 있습니다.

1. Hello에 설명 된 대로 저장소 에뮬레이터 콘솔 창 열기 hello [시작 및 초기화 hello 저장소 에뮬레이터](#start-and-initialize-the-storage-emulator) 섹션.
1. Hello 콘솔 창에서 다음 명령을, hello를 입력 합니다. 여기서 `<SQLServerInstance>` hello hello SQL Server 인스턴스의 이름입니다. LocalDB, toouse 지정 `(localdb)\MSSQLLocalDb` hello SQL Server 인스턴스로.

  `AzureStorageEmulator.exe init /server <SQLServerInstance>`

  다음 명령을 hello 에뮬레이터 toouse hello 기본 SQL Server 인스턴스를 전송 하는 hello를 사용할 수 있습니다.

  `AzureStorageEmulator.exe init /server .\\`

  또는 다음 명령을 hello 데이터베이스 toohello 기본 LocalDB 인스턴스를 다시 초기화 하는 hello를 사용할 수 있습니다.

  `AzureStorageEmulator.exe init /forceCreate`

이 명령에 대한 자세한 내용은 [저장소 에뮬레이터 명령줄 도구 참조](#storage-emulator-command-line-tool-reference)를 참조하세요.

> [!TIP]
> Hello를 사용할 수 있습니다 [Microsoft SQL Server Management Studio](/sql/ssms/download-sql-server-management-studio-ssms) hello LocalDB 설치 비롯 하 여 SQL Server 인스턴스 (SSMS) toomanage 합니다. Hello SMSS에서에서 **tooServer 연결** 대화 상자에서 지정 `(localdb)\MSSQLLocalDb` hello에 **서버 이름:** 필드 tooconnect toohello LocalDB 인스턴스.

## <a name="authenticating-requests-against-hello-storage-emulator"></a>Hello 저장소 에뮬레이터에 대 한 요청 인증
설치 하 고 hello 저장소 에뮬레이터를 시작, 되 면에 대해 코드를 테스트할 수 있습니다. Hello 클라우드에서 Azure 저장소의 경우와 마찬가지로 hello 저장소 에뮬레이터에 대 한 모든 요청, 인증을 거쳐야 하지 않은 경우 익명 요청입니다. 공유 액세스 서명 (SAS)으로 또는 공유 키 인증을 사용 하 여 hello 저장소 에뮬레이터에 대 한 요청을 인증할 수 있습니다.

### <a name="authenticate-with-shared-key-credentials"></a>공유 키 자격 증명 인증
[!INCLUDE [storage-emulator-connection-string-include](../../../includes/storage-emulator-connection-string-include.md)]

연결 문자열에 대한 자세한 내용은 [Azure Storage 연결 문자열 구성](../storage-configure-connection-string.md)을 참조하세요.

### <a name="authenticate-with-a-shared-access-signature"></a>공유 액세스 서명 인증
Hello Xamarin 라이브러리와 같은 일부 Azure 저장소 클라이언트 라이브러리는 공유 액세스 서명 (SAS) 토큰으로 인증을 지원합니다. Hello와 같은 도구를 사용 하 여 hello SAS 토큰을 만들 수 있습니다 [저장소 탐색기](http://storageexplorer.com/) 또는 공유 키 인증을 지 원하는 다른 응용 프로그램입니다.

또한 Azure PowerShell을 사용하여 SAS 토큰을 생성할 수 있습니다. hello 다음 예제에서는 발생 하는 모든 권한 tooa blob 컨테이너와 SAS 토큰:

1. 아직 없는 경우 Azure PowerShell을 설치 (hello 최신 버전의 hello Azure PowerShell cmdlet 사용 하 여 권장). 설치 지침은 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/install-azurerm-ps)을 참조하세요.
2. Azure PowerShell을 열고 다음 명령, 대체 hello 실행 `ACCOUNT_NAME` 및 `ACCOUNT_KEY==` 자신의 자격 증명을 사용 하 고 `CONTAINER_NAME` 선택한 이름으로:

```powershell
$context = New-AzureStorageContext -StorageAccountName "ACCOUNT_NAME" -StorageAccountKey "ACCOUNT_KEY=="

New-AzureStorageContainer CONTAINER_NAME -Permission Off -Context $context

$now = Get-Date

New-AzureStorageContainerSASToken -Name CONTAINER_NAME -Permission rwdl -ExpiryTime $now.AddDays(1.0) -Context $context -FullUri
```

hello 결과 공유 액세스 서명 URI hello 새 컨테이너와 유사 해야 합니다.

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2015-07-08T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3Dsss
```

이 예제를 사용 하 여 만든 hello 공유 액세스 서명 1 일 동안 유효 합니다. hello 서명은 hello 컨테이너 내에서 모든 권한 (읽기, 쓰기, 삭제, 나열) tooblobs를 부여합니다.

공유 액세스 서명에 대한 자세한 내용은 [Azure Storage에서 SAS(공유 액세스 서명) 사용](../storage-dotnet-shared-access-signature-part-1.md)을 참조하세요.

## <a name="addressing-resources-in-hello-storage-emulator"></a>Hello 저장소 에뮬레이터에서 리소스 주소 지정
hello 저장소 에뮬레이터에 대 한 hello 서비스 끝점은 Azure 저장소 계정의 속성과 다릅니다. hello 차이가 hello 로컬 컴퓨터가 hello 저장소 에뮬레이터 끝점 toobe 로컬 주소를 요구 되는 도메인 이름 확인을 수행 하지 않기 때문에 있습니다.

Azure 저장소 계정에 리소스를 처리할 때 스키마를 따르는 hello를 사용 합니다. hello 계정 이름은 hello URI 호스트 이름의 일부가 고 요청 되는 hello 리소스는 hello URI 경로의 일부:

`<http|https>://<account-name>.<service-name>.core.windows.net/<resource-path>`

예를 들어 hello 다음 URI는 Azure 저장소 계정의 blob에에서 대 한 올바른 주소:

`https://myaccount.blob.core.windows.net/mycontainer/myblob.txt`

그러나 저장소 에뮬레이터를 hello를 hello 로컬 컴퓨터에서 도메인 이름 확인을 수행 하지 않으므로, hello 계정 이름을 hello 호스트 이름 대신 hello URI 경로의 일부입니다. Hello 저장소 에뮬레이터에서 리소스에 대 한 URI 형식에 따라 hello를 사용 합니다.

`http://<local-machine-address>:<port>/<account-name>/<resource-path>`

예를 들어 hello 다음 주소 사용될지 hello 저장소 에뮬레이터에서 blob에 액세스 하기 위한:

`http://127.0.0.1:10000/myaccount/mycontainer/myblob.txt`

hello 저장소 에뮬레이터에 대 한 hello 서비스 끝점은:

* Blob service: `http://127.0.0.1:10000/<account-name>/<resource-path>`
* 큐 서비스: `http://127.0.0.1:10001/<account-name>/<resource-path>`
* Table service: `http://127.0.0.1:10002/<account-name>/<resource-path>`

### <a name="addressing-hello-account-secondary-with-ra-grs"></a>RA-GRS를 사용 하 여 보조 hello 계정 주소 지정
Hello 저장소 에뮬레이터 버전 3.1 부터는 읽기 액세스 지리적 중복 복제 (RA-GRS)를 지원 합니다. Hello 클라우드와 hello 로컬 에뮬레이터에서 저장소 리소스에 대 한 hello 보조 위치에 액세스할 수 있습니다 보조 toohello 계정 이름을-으로 추가 합니다. 예를 들어 주소 다음 hello hello 저장소 에뮬레이터의 hello 읽기 전용 보조 복제본을 사용 하 여 blob에 액세스 하기 위한 사용 수 있습니다.

`http://127.0.0.1:10000/myaccount-secondary/mycontainer/myblob.txt`

> [!NOTE]
> 프로그래밍 방식 액세스 toohello hello 저장소 에뮬레이터를 사용 하 여 보조, for.NET 버전 3.2 이상을 hello 저장소 클라이언트 라이브러리를 사용 합니다. Hello 참조 [.NET 용 Microsoft Azure 저장소 클라이언트 라이브러리](https://msdn.microsoft.com/library/azure/dn261237.aspx) 대 한 자세한 내용은 합니다.
>
>

## <a name="storage-emulator-command-line-tool-reference"></a>저장소 에뮬레이터 명령줄 도구 참조
버전 3.0부터, 콘솔 창에 hello 저장소 에뮬레이터를 시작할 때 표시 됩니다. 상태에 대 한 쿼리를 비롯 하 여 hello 콘솔 창 toostart 및 중지 hello 에뮬레이터에 hello 명령줄을 사용 하 고 다른 작업을 수행 합니다.

> [!NOTE]
> Microsoft Azure 계산 에뮬레이터를 설치 하는 hello를 사용 하도록 설정한 경우 hello 저장소 에뮬레이터를 시작할 때 시스템 트레이 아이콘이 나타납니다. Hello 아이콘 tooreveal 그래픽 방식으로 toostart 제공 하는 메뉴가 고 hello 저장소 에뮬레이터를 중지 합니다.
>
>

### <a name="command-line-syntax"></a>명령줄 구문
`AzureStorageEmulator.exe [start] [stop] [status] [clear] [init] [help]`

### <a name="options"></a>옵션
옵션을 형식 tooview hello 목록 `/help` hello 명령 프롬프트입니다.

| 옵션 | 설명 | 명령 | 인수 |
| --- | --- | --- | --- |
| **시작** |Hello 저장소 에뮬레이터를 시작 합니다. |`AzureStorageEmulator.exe start [-inprocess]` |*-inprocess*: hello 새 프로세스를 만드는 대신 현재 프로세스의 hello 에뮬레이터를 시작 합니다. |
| **중지** |Hello 저장소 에뮬레이터를 중지 합니다. |`AzureStorageEmulator.exe stop` | |
| **상태** |인쇄 hello hello 저장소 에뮬레이터의 상태입니다. |`AzureStorageEmulator.exe status` | |
| **지우기** |Hello 명령줄에 지정 된 모든 서비스에 대 한 hello 데이터를 지웁니다. |`AzureStorageEmulator.exe clear [blob] [table] [queue] [all]                                                    ` |*blob*: blob 데이터를 지웁니다. <br/>*queue*: 큐 데이터를 지웁니다. <br/>*table*: 테이블 데이터를 지웁니다. <br/>*all*: 모든 서비스의 모든 데이터를 지웁니다. |
| **Init** |한 번만 초기화 tooset hello 에뮬레이터를 수행합니다. |<code>AzureStorageEmulator.exe init [-server serverName] [-sqlinstance instanceName] [-forcecreate&#124;-skipcreate] [-reserveports&#124;-unreserveports] [-inprocess]</code> |*-서버 serverName\instanceName*: hello SQL 인스턴스를 호스트 하는 hello 서버를 지정 합니다. <br/>*-sqlinstance instanceName*: hello 기본 서버 인스턴스에 사용 되는 hello SQL 인스턴스 toobe의 hello 이름을 지정 합니다. <br/>*-forcecreate*: 이미 있는 경우에 hello SQL 데이터베이스 만들기를 강제로 수행 합니다. <br/>*-skipcreate*: hello SQL 데이터베이스 만들기를 건너뜁니다. 이 옵션은 -forcecreate보다 우선합니다.<br/>*-reserveports*: hello 서비스와 관련 된 tooreserve hello HTTP 포트를 시도 합니다.<br/>*-unreserveports*: hello 서비스와 관련 된 hello HTTP 포트에 대 한 tooremove 예약을 시도 합니다. 이 옵션은 -reserveports보다 우선합니다.<br/>*-inprocess*: hello 새 프로세스를 생성 하는 대신 현재 프로세스에서 초기화를 수행 합니다. 현재 프로세스 hello 포트 예약을 변경 하는 경우 승격 된 권한으로 시작 해야 합니다. |

## <a name="differences-between-hello-storage-emulator-and-azure-storage"></a>Hello 저장소 에뮬레이터와 Azure 저장소의 차이점
Hello 저장소 에뮬레이터에서 로컬 SQL 인스턴스를 실행 하는 에뮬레이트된 환경 이기 때문에 hello 클라우드를 hello 에뮬레이터와 Azure 저장소 계정 간 기능 차이 있습니다.

* hello 저장소 에뮬레이터만는 단일 고정 계정과 잘 알려진 인증 키를 지원합니다.
* hello 저장소 에뮬레이터는 확장 가능한 저장소 서비스가 아니며 많은 수의 동시 클라이언트를 지원 하지 않습니다.
* 에 설명 된 대로 [hello 저장소 에뮬레이터에서 리소스 주소 지정](#addressing-resources-in-the-storage-emulator), hello 저장소 에뮬레이터와 Azure 저장소 계정에서에서 리소스는 다르게 주소가 지정 합니다. 이러한 차이가 hello 클라우드 있지만 없습니다 hello 로컬 컴퓨터의 도메인 이름 확인을 사용할 수 있습니다.
* 버전 3.1 부터는 hello 저장소 에뮬레이터 계정 읽기 액세스 지리적 중복 복제 (RA-GRS)를 지원 합니다. Hello 에뮬레이터에서 모든 계정 RA-GRS를 사용할 수 있고 hello 기본 및 보조 복제본 간의 모든 지연 되지 않습니다. hello Blob 서비스 통계 가져오기, 큐 서비스 통계 가져오기 및 테이블 서비스 통계 가져오기 작업은 보조 hello 계정에서 지원 및 항상 hello hello 값을 반환 합니다 `LastSyncTime` 응답 요소 중 현재 시간에 따라 toohello 기본 hello SQL 데이터베이스입니다.
* hello 파일 서비스 및 SMB 프로토콜 서비스 끝점 hello 저장소 에뮬레이터에서 현재 지원 되지 않습니다.
* Hello 에뮬레이터에서 아직 지원 되지 않는 hello 저장소 서비스의 버전을 사용 하는 경우 저장소 에뮬레이터 hello VersionNotSupportedByEmulator 오류 (HTTP 상태 코드 400-잘못 된 요청)을 반환 합니다.

### <a name="differences-for-blob-storage"></a>Blob 저장소의 차이점
다음 차이점 hello tooBlob 저장소 hello 에뮬레이터에 적용 됩니다.

* hello 저장소 에뮬레이터만 too2 GB blob 크기를 지원합니다.
* 증분 복사 hello 서비스에서 오류를 반환 하는 복사 되는 blob 덮어쓴된 toobe 스냅숏 수 있습니다.
* Get Page Ranges Diff는 Incremental Copy Blob을 사용하여 복사한 스냅숏 간에는 작동하지 않습니다.
* Hello 요청에 hello 임대 ID를 지정 하지 않은 경우에 활성 임대가 있는 hello 저장소 에뮬레이터에 존재 하는 blob에 대해 Put Blob 작업이 성공할 수 있습니다.
* Hello 에뮬레이터에서 지원 되지 않는 Blob에 추가 합니다. 추가 Blob에 대한 작업을 시도하면 FeatureNotSupportedByEmulator 오류(HTTP 상태 코드 400 - 잘못된 요청)가 반환됩니다.

### <a name="differences-for-table-storage"></a>테이블 저장소의 차이점
다음 차이점 hello tooTable 저장소 hello 에뮬레이터에 적용 됩니다.

* Hello hello 저장소 에뮬레이터의 테이블 서비스에서에서 날짜 속성 (서로 필요한 toobe 1753 년 1 월 1 일 이후의) SQL Server 2005에서 지 원하는 hello 범위만을 지원 합니다. 1753 년 1 월 1 일 전의 모든 날짜가 변경 toothis 값입니다. hello 날짜 정밀도 SQL Server 2005, 날짜를 정확 하 게 too1 있음을 의미의 제한 된 toohello 정밀도/300 초입니다.
* hello 저장소 에뮬레이터는 512 바이트 미만의 각 파티션 키와 행 키 속성 값을 지원합니다. 또한 hello 총 크기 hello 계정 이름, 테이블 이름 및 키 속성 이름 함께 초과할 수 없습니다 900 바이트입니다.
* hello hello 저장소 에뮬레이터의 테이블에 행의 총 크기는 1MB 보다 제한 된 tooless입니다.
* 데이터의 속성을 입력 hello 저장소 에뮬레이터에서 `Edm.Guid` 또는 `Edm.Binary` 지원만 hello `Equal (eq)` 및 `NotEqual (ne)` 쿼리에서 비교 연산자 필터 문자열입니다.

### <a name="differences-for-queue-storage"></a>큐 저장소의 차이점
Hello 에뮬레이터에는 차이점 특정 tooQueue 저장소가 없습니다.

## <a name="storage-emulator-release-notes"></a>저장소 에뮬레이터 릴리스 정보
### <a name="version-52"></a>버전 5.2
* hello 저장소 에뮬레이터는 이제 Blob, 큐 및 테이블 서비스 끝점에 hello 저장소 서비스의 2017-04-17 버전을 지원합니다.
* 테이블 속성 값이 제대로 인코딩되지 않는 버그를 수정했습니다.

### <a name="version-51"></a>버전 5.1
* 저장소 에뮬레이터 hello hello를 반환 했습니다 버그가 수정 `DataServiceVersion` 일부 hello 서비스 되지 않는다는 응답의 헤더입니다.

### <a name="version-50"></a>버전 5.0
* hello 저장소 에뮬레이터 설치 관리자가 더 이상 기존 MSSQL 확인 하 고.NET Framework 설치 합니다.
* hello 저장소 에뮬레이터 설치 관리자는 더 이상 설치의 일부로 hello 데이터베이스를 만듭니다. 필요한 경우 시작 시 데이터베이스가 만들어집니다.
* 데이터베이스를 만들 때 더 이상 관리자 권한이 필요하지 않습니다.
* 시작 시 더 이상 포트 예약이 필요하지 않습니다.
* 다음 옵션을 너무 hello 추가`init`: `-reserveports` (권한 상승이 필요한) `-unreserveports` (권한 상승이 필요한) `-skipcreate`합니다.
* 저장소 에뮬레이터 UI 옵션 hello 시스템 트레이 아이콘 이제 hello hello 명령줄 인터페이스를 시작합니다. hello 이전 GUI를 사용할 수 없습니다.
* 일부 DLL이 제거되거나 이름이 바뀌었습니다.

### <a name="version-46"></a>버전 4.6
* hello 저장소 에뮬레이터는 이제 Blob, 큐 및 테이블 서비스 끝점에 2016-05-31 hello 저장소 서비스의 버전을 지원합니다.

### <a name="version-45"></a>버전 4.5
* 초기화 및 hello 저장소 에뮬레이터 toofail의 설치 데이터베이스를 백업 하는 hello 이름이 바뀐 경우 발생 하는 버그를 수정 했습니다.

### <a name="version-44"></a>버전 4.4
* hello 저장소 에뮬레이터는 이제 Blob, 큐 및 테이블 서비스 끝점에 hello 저장소 서비스의 2015 년 12 월 11 버전을 지원합니다.
* hello blob 데이터의 저장소 에뮬레이터의 가비지 수집 이제 더 효율적입니다 다 수의 blob으로 처리 하는 경우.
* 컨테이너 ACL XML toobe hello 저장소 서비스 수행 방법에서 약간 다르게 유효성을 검사를 발생 시킨는 버그를 수정 합니다.
* 버그를 발생 시킨 경우에 따라 max 고정 되 고 hello 잘못 된 표준 시간대의 날짜/시간 값 toobe min 보고 합니다.

### <a name="version-43"></a>버전 4.3
* hello 저장소 에뮬레이터는 이제 Blob, 큐 및 테이블 서비스 끝점에 hello 저장소 서비스의 2015-07-08 버전을 지원합니다.

### <a name="version-42"></a>버전 4.2
* hello 저장소 에뮬레이터는 이제 Blob, 큐 및 테이블 서비스 끝점에 hello 저장소 서비스의 2015-04-05 버전을 지원합니다.

### <a name="version-41"></a>버전 4.1
* hello 저장소 에뮬레이터는 이제 hello 새로운 Blob 추가 기능을 제외 하 고 Blob, 큐 및 테이블 서비스 끝점에 hello 저장소 서비스의 버전 2015-02-21을 지원합니다.
* Hello 에뮬레이터에서 아직 지원 되지 않는 hello 저장소 서비스의 버전을 사용 하 여 hello 에뮬레이터 의미 있는 오류 메시지가 반환 됩니다. Hello 에뮬레이터의 hello 최신 버전을 사용 하는 것이 좋습니다. VersionNotSupportedByEmulator 오류 (HTTP 상태 코드 400-잘못 된 요청) 발생 하는 경우 hello 저장소 에뮬레이터의 hello 최신 버전을 다운로드 하십시오.
* 경합 조건이 발생할 테이블 엔터티 데이터 toobe 동시 병합 작업 중 잘못 된 여기서는 버그를 수정 합니다.

### <a name="version-40"></a>버전 4.0
* hello 저장소 에뮬레이터 실행 파일 이름을 바꾼 너무*AzureStorageEmulator.exe*합니다.

### <a name="version-32"></a>버전 3.2
* hello 저장소 에뮬레이터는 이제 Blob, 큐 및 테이블 서비스 끝점에 hello 저장소 서비스의 버전 2014-02-14를 지원합니다. 파일 서비스 끝점 hello 저장소 에뮬레이터에서 현재 지원 되지 않습니다. 참조 [hello Azure 저장소 서비스에 대 한 버전 관리](/rest/api/storageservices/Versioning-for-the-Azure-Storage-Services) 2014-02-14 버전에 대 한 세부 정보에 대 한 합니다.

### <a name="version-31"></a>버전 3.1
* 이제 읽기 액세스 지역 중복 저장소 (RA-GRS) hello 저장소 에뮬레이터에서 지원 됩니다. hello Blob 서비스 통계 가져오기, 큐 서비스 통계 가져오기 및 테이블 서비스 통계 Api 가져오기 hello 계정 보조에 대 한 지원 및 항상 hello LastSyncTime 응답 요소 중 현재 시간에 따라 toohello SQL 기본 hello hello 값을 반환 합니다. 데이터베이스입니다. 프로그래밍 방식 액세스 toohello hello 저장소 에뮬레이터를 사용 하 여 보조, for.NET 버전 3.2 이상을 hello 저장소 클라이언트 라이브러리를 사용 합니다. .NET 참조에 대 한 자세한 내용은 hello Microsoft Azure 저장소 클라이언트 라이브러리를 참조 하십시오.

### <a name="version-30"></a>버전 3.0
* hello Azure 저장소 에뮬레이터는 hello 계산 에뮬레이터와 동일한 패키지 hello 더 이상 제공 됩니다.
* 스크립트 가능한 명령줄 인터페이스 대신 hello 저장소 에뮬레이터 그래픽 사용자 인터페이스를 사용 하는 사용 되지 않습니다. Hello 명령줄 인터페이스에 대 한 자세한 내용은 저장소 에뮬레이터 명령줄 도구 참조를 참조 하십시오. hello 그래픽 인터페이스 toobe 버전 3.0에 계속 하지만 hello 시스템 트레이 아이콘을 마우스 오른쪽 단추로 클릭 하 고 저장소 에뮬레이터 UI 표시를 선택 하 여 hello 계산 에뮬레이터를 설치할 때에 액세스할 수 있습니다.
* 버전 2013-08-15 hello Azure 저장소 서비스는 완벽 하 게 지원 됩니다. (이전에 이 버전은 저장소 에뮬레이터 버전 2.2.1 미리 보기에서만 지원되었습니다.)

## <a name="next-steps"></a>다음 단계

* Hello 오픈 소스 플랫폼 간, 커뮤니티에서 유지 관리 되며 저장소 에뮬레이터를 평가 [Azurite](https://github.com/arafato/azurite)합니다. 
* [.NET을 사용 하 여 azure 저장소 예제](../storage-samples-dotnet.md) 응용 프로그램을 개발할 때 사용할 수 있는 링크 tooseveral 코드 샘플이 포함 되어 있습니다.
* Hello를 사용할 수 있습니다 [Microsoft Azure 저장소 탐색기](http://storageexplorer.com) hello 저장소 에뮬레이터 및 클라우드 저장소 계정에서에서 리소스와 toowork 합니다.
