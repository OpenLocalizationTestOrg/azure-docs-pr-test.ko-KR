---
title: "hello Azure Cosmos DB 에뮬레이터를 사용 하 여 로컬로 aaaDevelop | Microsoft Docs"
description: "Hello Azure Cosmos DB 에뮬레이터를 사용 하 여 개발 하 고 Azure 구독을 만들지 않고 비어 있거나 응용 프로그램을 로컬로 테스트할 수 있습니다."
services: cosmos-db
documentationcenter: 
keywords: "Azure Cosmos DB 에뮬레이터"
author: arramac
manager: jhubbard
editor: 
ms.assetid: 90b379a6-426b-4915-9635-822f1a138656
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: arramac
ms.openlocfilehash: fb5449489e5f71664e72d8e11e583315be371bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cosmos-db-emulator-for-local-development-and-testing"></a>Hello Azure Cosmos DB 에뮬레이터를 사용 하 여 로컬 개발 및 테스트

<table>
<tr>
  <td><strong>이진 파일</strong></td>
  <td>[MSI 다운로드](https://aka.ms/cosmosdb-emulator)</td>
</tr>
<tr>
  <td><strong>Docker</strong></td>
  <td>[Docker 허브](https://hub.docker.com/r/microsoft/azure-documentdb-emulator/)</td>
</tr>
<tr>
  <td><strong>Docker 원본</strong></td>
  <td>[Github](https://github.com/azure/azure-documentdb-emulator-docker)</td>
</tr>
</table>
  
hello Azure Cosmos DB 에뮬레이터 hello Azure Cosmos DB 서비스를 개발 목적으로 에뮬레이트하는 로컬 환경을 제공 합니다. Hello Azure Cosmos DB 에뮬레이터를 사용 하 여 개발 하 고 Azure 구독을 만들거나 모든 비용이 발생 하지 않고 응용 프로그램을 로컬로 테스트할 수 있습니다. Hello Azure Cosmos DB 에뮬레이터에서에서 응용 프로그램 작동 방식을 만족 스 러 우면 toousing hello 클라우드에서 Azure Cosmos DB 계정을 전환할 수 있습니다.

이 문서에서는 다음 작업 hello를 다룹니다. 

> [!div class="checklist"]
> * Hello 에뮬레이터를 설치합니다.
> * Windows 용 Docker에 hello 에뮬레이터 실행
> * 요청 인증
> * Hello 에뮬레이터의에서 hello 데이터 탐색기를 사용 하 여
> * SSL 인증서 내보내기
> * 에뮬레이터의 hello hello 명령줄에서 호출
> * 추적 파일 수집

다음 비디오에서는 Kirill Gavrylyuk tooget Azure Cosmos DB 에뮬레이터 hello로 시작 하는 방법을 보여 줍니다 hello를 시청 하 여 시작 하는 것이 좋습니다. Hello 비디오를 눌러 이후 Azure Cosmos DB 에뮬레이터 hello 하는 hello 비디오에서는 DocumentDB 에뮬레이터 hello 라고 toohello 에뮬레이터 되지만 hello 도구 자체 이름이 변경 되었습니다. 비디오 hello에서 모든 정보는 hello Azure Cosmos DB 에뮬레이터에 대 한 정확 해야 합니다. 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-hello-emulator-works"></a>Hello 에뮬레이터의 작동 원리
hello Azure Cosmos DB 에뮬레이터의 hello Azure Cosmos DB 서비스의 충실도 높은 재현 에뮬레이션을 제공합니다. JSON 문서 만들기 및 쿼리, 컬렉션 프로비전 및 확장, 저장 프로시저 및 트리거 실행을 비롯하여 Azure Cosmos DB으로 동일한 기능을 지원합니다. 개발 및 hello Azure Cosmos DB 에뮬레이터를 사용 하 여 응용 프로그램을 테스트 하 고 방금 단일 구성을 Azure Cosmos DB에 대 한 toohello 연결 끝점을 변경 하 여 세계적인 규모에 tooAzure 배포 수입니다.

Hello 실제 Azure Cosmos DB 서비스의 충실도 높은 재현 로컬 에뮬레이션 만들었습니다 동안 hello Azure Cosmos DB 에뮬레이터의 hello 구현 hello 서비스의 차이가 있습니다. 예를 들어 hello Azure Cosmos DB 에뮬레이터는 지 속성 및 연결에 대 한 HTTPS 프로토콜 스택에 hello 로컬 파일 시스템 등 표준 OS 구성 요소를 사용합니다. 즉, 글로벌 복제, 읽기/쓰기 및 튜닝할 수 있는 일관성 수준에 대 한 대기 시간이 단일 자리 숫자 밀리초를 hello Azure Cosmos DB 에뮬레이터를 통해 사용할 수 없는 경우와 같은 Azure 인프라를 사용 하는 몇 가지 기능이 있습니다.

> [!NOTE]
> Hello에이 시간 hello 데이터 탐색기에서 에뮬레이터는 DocumentDB API 컬렉션과 MongoDB 컬렉션 hello 만들기만 지원합니다. hello 에뮬레이터의 hello 데이터 탐색기 현재 테이블 및 그래프의 hello 생성을 지원 하지 않습니다. 

## <a name="system-requirements"></a>시스템 요구 사항
hello Azure Cosmos DB 에뮬레이터의 hello 하드웨어 및 소프트웨어 요구 사항:

* 소프트웨어 요구 사항
  * Windows Server 2012 R2, Windows Server 2016 또는 Windows 10
*   최소 하드웨어 요구 사항
  * 2GB RAM
  * 10GB의 하드 디스크 여유 공간

## <a name="installation"></a>설치
다운로드 하 여 hello에서 hello Azure Cosmos DB 에뮬레이터 설치 [Microsoft 다운로드 센터](https://aka.ms/cosmosdb-emulator)합니다. 

> [!NOTE]
> tooinstall를 구성 하 고 hello Azure Cosmos DB 에뮬레이터를 실행, hello 컴퓨터에서 관리자 권한이 있어야 합니다.

## <a name="running-on-docker-for-windows"></a>Windows용 Docker에서 실행

Windows 용 Docker에 hello Azure Cosmos DB 에뮬레이터를 실행할 수 있습니다. Oracle Linux에 대 한 hello 에뮬레이터 Docker에서 작동 하지 않습니다.

설정한 후 [Windows 용 Docker](https://www.docker.com/docker-windows) 설치 되어 끌어올 수 있습니다 hello 에뮬레이터 이미지 Docker 허브에서 hello 즐겨 찾는 셸에서 다음 명령을 실행 하 여 (cmd.exe, PowerShell 등.).

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
toostart hello 이미지를 hello 다음 명령을 실행 합니다.

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

hello 응답 비슷한 toohello 다음과 같습니다.

```
Starting Emulator
Emulator Endpoint: https://172.20.229.193:8081/
Master Key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==
Exporting SSL Certificate
You can import hello SSL certificate from an administrator command prompt on hello host by running:
cd /d %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
--------------------------------------------------------------------------------------------------
Starting interactive shell
``` 

에뮬레이터를 시작 하는 hello 종료 hello 에뮬레이터의 컨테이너는 면 대화형 셸 hello를 종료 했습니다.

클라이언트에서 hello 끝점과 hello 응답에서의 마스터 키를 사용 하 하며 호스트로 hello SSL 인증서를 가져옵니다. tooimport hello SSL 인증서를 관리자 명령 프롬프트에서 다음 hello지 않습니다.

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-hello-emulator"></a>Hello 에뮬레이터를 시작 합니다.

toostart hello Azure Cosmos DB 에뮬레이터 hello 시작 단추를 선택 하거나 hello Windows 키를 누릅니다. 입력을 시작 **Azure Cosmos DB 에뮬레이터**, 및 응용 프로그램의 hello 목록에서 선택 hello 에뮬레이터입니다. 

![Hello 시작 단추를 클릭 하거나 눌러 hello Windows 키를 선택, 입력을 시작 * * Azure Cosmos DB 에뮬레이터 * *, 및 응용 프로그램의 hello 목록에서 선택 hello 에뮬레이터](./media/local-emulator/database-local-emulator-start.png)

Hello 에뮬레이터를 실행 하는 경우에 hello Windows 작업 표시줄 알림 영역에서에서 아이콘을 표시 됩니다. ![Azure Cosmos DB 로컬 에뮬레이터 작업 표시줄 알림](./media/local-emulator/database-local-emulator-taskbar.png)

기본적으로 Azure Cosmos DB 에뮬레이터 hello 포트 8081에서 수신 대기 로컬 hello 컴퓨터 ("localhost")에서 실행 됩니다.

hello Azure Cosmos DB 에뮬레이터가 설치 되어 기본 toohello로 `C:\Program Files\Azure Cosmos DB Emulator` 디렉터리입니다. 또한 시작 하 고 hello 명령줄에서 hello 에뮬레이터를 중지할 수 있습니다. 자세한 내용은 [명령줄 도구 참조](#command-line)를 참조하세요.

## <a name="start-data-explorer"></a>데이터 탐색기 시작

Hello Azure Cosmos DB 에뮬레이터를 시작할 때 자동으로 열립니다 hello Azure Cosmos DB 데이터 탐색기 브라우저에서 합니다. hello 주소도 나타납니다. [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html)합니다. 닫기 탐색기 hello을 하면 toore 열기 원하는 것 이상 hello URL을 브라우저에서 열 하거나 아래와 같이 hello Windows 트레이 아이콘에에서 hello Azure Cosmos DB 에뮬레이터에서에서 실행 합니다.

![Azure Cosmos DB의 로컬 에뮬레이터 데이터 탐색기 시작 관리자](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a>업데이트 확인
데이터 탐색기에 다운로드할 수 있는 새 업데이트가 있는지 표시됩니다. 

> [!NOTE]
> 한 버전의 hello Azure Cosmos DB 에뮬레이터에서 만든 데이터 보장 되지 않습니다 toobe 액세스할 수 있는 다른 버전을 사용 하는 경우. Hello 장기에 대 한 데이터 toopersist 경우 아닌 hello Azure Cosmos DB 에뮬레이터는 Azure Cosmos DB 계정에 해당 데이터를 저장 하는 것이 좋습니다. 

## <a name="authenticating-requests"></a>요청 인증
마찬가지로 hello 클라우드에서 Azure Cosmos DB와 함께 hello Azure Cosmos DB 에뮬레이터에 대해 구성 하는 모든 요청 인증 되어야 합니다. hello Azure Cosmos DB 에뮬레이터 마스터 키 인증을 위해 단일 고정 계정과 잘 알려진 인증 키를 지원 합니다. 이 계정과 키는 hello Azure Cosmos DB 에뮬레이터로 사용 하기 위해 허용 hello 유일한 자격 증명. 아래에 이 계정과 키의 예제가 나와 있습니다.

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> hello Azure Cosmos DB 에뮬레이터에서 지 원하는 hello 마스터 키 hello 에뮬레이터에만 사용이 됩니다. Azure Cosmos DB 에뮬레이터 hello로 프로덕션 Azure Cosmos DB 계정 및 키를 사용할 수 없습니다. 

> [!NOTE] 
> /Key 옵션 hello로 hello 에뮬레이터를 시작한 경우 그런 다음 대신 hello 생성 된 키 사용 "C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw = ="

또한와 마찬가지로 Azure Cosmos DB 서비스를 Azure Cosmos DB 에뮬레이터 hello hello SSL 통해 안전한 통신만을 지원 합니다.

## <a name="running-hello-emulator-on-a-local-network"></a>로컬 네트워크 hello 에뮬레이터를 실행합니다.

로컬 네트워크 hello 에뮬레이터를 실행할 수 있습니다. tooenable 네트워크 액세스, hello에 hello /AllowNetworkAccess 옵션을 지정할 [명령줄](#command-line-syntax), /Key를 지정 하는 또한 합니다 key_string 또는 /KeyFile = file_name = 합니다. /GenKeyFile를 사용할 수 있습니다 = file_name toogenerate 파일 현상을 임의 키 사용 합니다.  해당 너무/키 파일을 전달할 수 = file_name 또는 /Key = contents_of_file 합니다.

hello 신규 hello 사용자에 대 한 네트워크 액세스 tooenable hello 에뮬레이터를 종료 해야 하 고 hello 에뮬레이터의 데이터 디렉터리 (C:\Users\user_name\AppData\Local\CosmosDBEmulator)를 삭제 합니다.

## <a name="developing-with-hello-emulator"></a>Hello 에뮬레이터를 사용 하 여 개발
데스크톱에서 실행 되는 Azure DB Cosmos 에뮬레이터 hello 있는, 지원 되는 사용할 수 있습니다 [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) 또는 hello [Azure Cosmos DB REST API](/rest/api/documentdb/) toointeract 에뮬레이터 hello로 합니다. hello Azure Cosmos DB 에뮬레이터에는 모든 코드를 작성 하지 않고도 문서를 편집 하 고 hello DocumentDB MongoDB Api 및 보기에 대 한 컬렉션을 만들 수 있는 기본 제공 데이터 탐색기 포함 되어 있습니다.   

    // Connect toohello Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

사용 중인 경우 [MongoDB에 대 한 Azure Cosmos DB 프로토콜 지원](mongodb-introduction.md), 다음 연결 문자열 hello를 사용 하십시오.

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

와 같은 기존 도구를 사용할 수 있습니다 [Azure DocumentDB 스튜디오](https://github.com/mingaliu/DocumentDBStudio) tooconnect toohello Azure Cosmos DB 에뮬레이터입니다. Hello Azure Cosmos DB 에뮬레이터와 hello를 사용 하 여 hello Azure Cosmos DB 서비스 간에 데이터를 마이그레이션할 수도 있습니다 [Azure Cosmos DB 데이터 마이그레이션 도구](https://github.com/azure/azure-documentdb-datamigrationtool)합니다.

> [!NOTE] 
> /Key 옵션 hello로 hello 에뮬레이터를 시작한 경우 그런 다음 대신 hello 생성 된 키 사용 "C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw = ="

Hello Azure Cosmos DB 에뮬레이터를 사용 하 여 기본적으로, too25 단일 파티션 컬렉션 또는 1 분할 된 컬렉션을 만들 수 있습니다. 이 값을 변경 하는 방법에 대 한 자세한 내용은 참조 [hello PartitionCount 값 설정](#set-partitioncount)합니다.

## <a name="export-hello-ssl-certificate"></a>Hello SSL 인증서 내보내기

.NET 언어 및 런타임 사용 하 여 hello Windows 인증서 저장소 toosecurely toohello Azure Cosmos DB 로컬 에뮬레이터를 연결합니다. 다른 언어의 경우 해당 언어만의 인증서 관리 및 사용 방법이 있습니다. Java는 자체의 고유 [인증서 저장소](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html)를 사용하고 Python은 [소켓 래퍼](https://docs.python.org/2/library/ssl.html)를 사용합니다.

순서 tooobtain에서 언어 및 통합 되지 않습니다 hello Windows 인증서 저장소로 있습니다 있는 런타임과 상호 인증서 toouse 할 tooexport 인증서 관리자 Windows hello를 사용 하 여 수 있습니다. Certlm.msc를 실행 하 여 시작 하거나 hello 단계별 지침에 따라 수 [hello Azure Cosmos DB 에뮬레이터 인증서 내보내기](./local-emulator-export-ssl-certificates.md)합니다. Hello 인증서 관리자를 실행 하 고, 내보내기 및 열기 hello 개인 인증서 아래와 같이 hello hello 친숙 한 이름이 "DocumentDBEmulatorCertificate" 인증서 대로 E-64로 인코딩된 X.509 (.cer) 파일입니다.

![Azure Cosmos DB 로컬 에뮬레이터 SSL 인증서](./media/local-emulator/database-local-emulator-ssl_certificate.png)

hello 지침에 따라 hello Java 인증서 저장소로 hello X.509 인증서를 가져올 수 [Java CA 인증서를 저장 하는 인증서 toohello 추가](https://docs.microsoft.com/azure/java-add-certificate-ca-store)합니다. 가져온 hello 인증서는 hello 인증서 저장소로 MongoDB 및 Java 응용 프로그램 수 tooconnect toohello Azure Cosmos DB 에뮬레이터 됩니다.

Python 및 Node.js Sdk에서 toohello 에뮬레이터에 연결할 때 SSL 유효성 검사 불가능 합니다.

## <a id="command-line"></a>명령줄 도구 참조
Hello 설치 위치에서 있습니다 수 명령줄 toostart hello를 사용 하 여 중지 hello 에뮬레이터, 옵션을 구성 하 고 다른 작업을 수행 합니다.

### <a name="command-line-syntax"></a>명령줄 구문

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

옵션을 형식 tooview hello 목록 `CosmosDB.Emulator.exe /?` hello 명령 프롬프트입니다.

<table>
<tr>
  <td><strong>옵션</strong></td>
  <td><strong>설명</strong></td>
  <td><strong>명령</strong></td>
  <td><strong>인수</strong></td>
</tr>
<tr>
  <td>[인수 없음]</td>
  <td>기본 설정으로 hello Azure Cosmos DB 에뮬레이터를 시작합니다.</td>
  <td>CosmosDB.Emulator.exe</td>
  <td></td>
</tr>
<tr>
  <td>[도움말]</td>
  <td>Hello 목록을 표시 합니다. 명령줄 인수를 지원 합니다.</td>
  <td>CosmosDB.Emulator.exe /?</td>
  <td></td>
</tr>
<tr>
  <td>Shutdown</td>
  <td>Hello Azure Cosmos DB 에뮬레이터를 종료합니다.</td>
  <td>CosmosDB.Emulator.exe /Shutdown</td>
  <td></td>
</tr>
<tr>
  <td>DataPath</td>
  <td>어떤 toostore 데이터 파일에 hello 경로 지정합니다. 기본값은 %LocalAppdata%\CosmosDBEmulator입니다.</td>
  <td>CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</td>
  <td>&lt;datapath&gt;: 액세스 가능한 경로</td>
</tr>
<tr>
  <td>포트</td>
  <td>Hello 에뮬레이터에 대 한 포트 번호 toouse hello를 지정합니다.  기본값은 8081입니다.</td>
  <td>CosmosDB.Emulator.exe /Port=&lt;port&gt;</td>
  <td>&lt;port&gt;: 단일 포트 번호</td>
</tr>
<tr>
  <td>MongoPort</td>
  <td>MongoDB 호환성 API에 대 한 포트 번호 toouse hello를 지정합니다. 기본값은 10255입니다.</td>
  <td>CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</td>
  <td>&lt;mongoport&gt;: 단일 포트 번호</td>
</tr>
<tr>
  <td>DirectPorts</td>
  <td>직접 연결에 대 한 포트 toouse hello를 지정합니다. 기본값은 10251,10252,10253,10254입니다.</td>
  <td>CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</td>
  <td>&lt;directports&gt;: 쉼표로 구분된 4개의 포트 목록</td>
</tr>
<tr>
  <td>키</td>
  <td>Hello 에뮬레이터에 대 한 권한 부여 키입니다. 키는 64 바이트 벡터의 hello base 64 인코딩 이어야 합니다.</td>
  <td>CosmosDB.Emulator.exe /Key:&lt;key&gt;</td>
  <td>&lt;키&gt;: 키 64 바이트 벡터의 hello base 64 인코딩 이어야 합니다</td>
</tr>
<tr>
  <td>EnableRateLimiting</td>
  <td>요청 속도 제한 동작을 사용하도록 지정합니다.</td>
  <td>CosmosDB.Emulator.exe /EnableRateLimiting</td>
  <td></td>
</tr>
<tr>
  <td>DisableRateLimiting</td>
  <td>요청 속도 제한 동작을 사용하지 않도록 지정합니다.</td>
  <td>CosmosDB.Emulator.exe /DisableRateLimiting</td>
  <td></td>
</tr>
<tr>
  <td>NoUI</td>
  <td>Hello 에뮬레이터 사용자 인터페이스를 표시 하지 않습니다.</td>
  <td>CosmosDB.Emulator.exe /NoUI</td>
  <td></td>
</tr>
<tr>
  <td>NoExplorer</td>
  <td>시작 시 문서 탐색기를 표시하지 않습니다.</td>
  <td>CosmosDB.Emulator.exe /NoExplorer</td>
  <td></td>
</tr>
<tr>
  <td>PartitionCount</td>
  <td>Hello 분할 된 컬렉션의 최대 수를 지정합니다. 참조 [hello 컬렉션 수를 변경](#set-partitioncount) 자세한 정보에 대 한 합니다.</td>
  <td>CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</td>
  <td>&lt;partitioncount&gt;: 허용되는 단일 파티션 컬렉션의 최대 수입니다. 기본값은 25입니다. 허용되는 최대값은 250입니다.</td>
</tr>
<tr>
  <td>DefaultPartitionCount</td>
  <td>Hello 기본 분할 된 컬렉션에 대 한 파티션 수를 지정합니다.</td>
  <td>CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</td>
  <td>&lt;defaultpartitioncount&gt; 기본값은 25입니다.</td>
</tr>
<tr>
  <td>AllowNetworkAccess</td>
  <td>Toohello 에뮬레이터는 네트워크를 통해 액세스 하는 사용 하도록 설정 합니다. /Key 전달 해야 =&lt;key_string&gt; 또는 /KeyFile =&lt;file_name&gt; tooenable 네트워크 액세스.</td>
  <td>CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;<br><br>또는<br><br>CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</td>
  <td></td>
</tr>
<tr>
  <td>NoFirewall</td>
  <td>/AllowNetworkAccess가 사용되는 경우 방화벽 규칙을 조정하지 마십시오.</td>
  <td>CosmosDB.Emulator.exe /NoFirewall</td>
  <td></td>
</tr>
<tr>
  <td>GenKeyFile</td>
  <td>새 인증 키를 생성 하 고 toohello 지정된 파일을 저장 합니다. /Key hello 또는 /KeyFile 옵션 hello 생성 키를 사용할 수 있습니다.</td>
  <td>CosmosDB.Emulator.exe /GenKeyFile =&lt;tookey 파일 경로&gt;</td>
  <td></td>
</tr>
<tr>
  <td>일관성</td>
  <td>Hello 계정에 대 한 hello 기본 일관성 수준을 설정 합니다.</td>
  <td>CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</td>
  <td>&lt;일관성&gt;: 값 hello 다음 중 하나 여야 합니다 [일관성 수준](consistency-levels.md): 세션, 강력한, 차례로 Eventual, 또는 BoundedStaleness 합니다.  hello 기본값은 세션입니다.</td>
</tr>
<tr>
  <td>?</td>
  <td>Hello 도움말 메시지를 표시 합니다.</td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-hello-azure-cosmos-db-emulator-and-azure-cosmos-db"></a>Hello Azure Cosmos DB 에뮬레이터와 Azure Cosmos DB의 차이점 
Hello Azure Cosmos DB 에뮬레이터 로컬 개발자 워크스테이션에서 실행 되는 에뮬레이트된 환경을 제공 하기 때문에 일부 간 기능 차이 hello 에뮬레이터와 Azure Cosmos DB 계정을 hello 클라우드에서 있습니다.

* hello Azure Cosmos DB 에뮬레이터만는 단일 고정 계정과 잘 알려진 마스터 키를 지원합니다.  키 다시 생성 hello Azure Cosmos DB 에뮬레이터의에서 수는 없습니다.
* hello Azure Cosmos DB 에뮬레이터는 확장 가능한 서비스 아니며 많은 수의 컬렉션을 지원 하지 않습니다.
* hello Azure Cosmos DB 에뮬레이터 시뮬레이션 하지 않습니다 다른 [Azure Cosmos DB 일관성 수준](consistency-levels.md)합니다.
* hello Azure Cosmos DB 에뮬레이터 시뮬레이션 하지 않습니다 [다중 지역 복제](distribute-data-globally.md)합니다.
* hello Azure Cosmos DB 에뮬레이터 hello Azure Cosmos DB 서비스 (예: 문서 크기 제한, 향상 된 분할 된 컬렉션 저장소)에서 사용할 수 있는 hello 서비스 할당량 재정의 지원 하지 않습니다.
* Hello Azure Cosmos DB 에뮬레이터의 사본을 수 toodate hello Azure Cosmos DB 서비스와 hello 가장 최근 변경 내용으로 구성 되지 않아, 하세요 [Azure Cosmos DB 용량 플래너](https://www.documentdb.com/capacityplanner) tooaccurately 예상 프로덕션 처리량 (RUs) 응용 프로그램의 필요 합니다.

## <a id="set-partitioncount"></a>컬렉션의 hello 수 변경

기본적으로 too25 단일 파티션 컬렉션 또는 hello Azure Cosmos DB 에뮬레이터를 사용 하 여 1 분할 된 컬렉션을 만들 수 있습니다. Hello를 수정 하 여 **PartitionCount** 어떠한 조합의 hello 250 단일을 초과 하지 않는 두 개의 파티션 (위치 1 분할 또는 값을 too250 단일 파티션 컬렉션 또는 10 분할 된 컬렉션을 만들 수 있습니다 컬렉션 = 25 단일 파티션 컬렉션).

Hello 현재 파티션 수를 초과한 후 toocreate 컬렉션을 시도 하면 hello 에뮬레이터 hello 메시지의 뒤에 있는 ServiceUnavailable 예외를 throw 합니다.

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    toobring more and more capacity online, and encourage you tootry again. 
    Please do not hesitate tooemail docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

컬렉션 사용 가능한 toohello Azure Cosmos DB 에뮬레이터의 hello 수 toochange 다음 hello지 않습니다.

1. Hello를 마우스 오른쪽 단추로 클릭 하 여 모든 로컬 Azure Cosmos DB 에뮬레이터 데이터를 삭제 **Azure Cosmos DB 에뮬레이터** hello 시스템 트레이 클릭 한 다음에 아이콘 **데이터를 다시 설정...** .
2. C:\Users\user_name\AppData\Local\CosmosDBEmulator 폴더에 있는 모든 에뮬레이터 데이터를 삭제합니다.
3. Hello를 마우스 오른쪽 단추로 클릭 하 여 열려 있는 모든 인스턴스를 종료 **Azure Cosmos DB 에뮬레이터** hello 시스템 트레이 클릭 한 다음에 아이콘 **종료**합니다. 모든 인스턴스 tooexit 1 분을 걸릴 수 있습니다.
4. 최신 버전의 hello hello 설치 [Azure Cosmos DB 에뮬레이터](https://aka.ms/cosmosdb-emulator)합니다.
5. 값을 설정 하 여 hello PartitionCount 플래그로 hello 에뮬레이터를 시작 합니다. < = 250 합니다. 예: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`

## <a name="troubleshooting"></a>문제 해결

다음 팁 toohelp hello Azure Cosmos DB 에뮬레이터와 함께 발생할 문제를 해결 하는 hello를 사용 합니다.

- 새 버전의 hello 에뮬레이터를 설치 하 여 오류를 발생 하는 경우 데이터를 다시 설정 확인 합니다. Hello 시스템 트레이에서 hello Azure Cosmos DB 에뮬레이터 아이콘을 마우스 오른쪽 단추로 클릭 한 다음 데이터를 다시 설정 클릭 하 여 데이터를 다시 설정할 수 있습니다... Hello 오류를 해결 하지 않으면 제거 하 고 hello 앱을 다시 설치 수 있습니다. 참조 [hello 로컬 에뮬레이터를 제거할](#uninstall) 지침에 대 한 합니다.

- Hello Azure Cosmos DB 에뮬레이터가 충돌 하면 c:\Users\user_name\AppData\Local\CrashDumps 폴더에서 덤프 파일을 수집, 압축 및 첨부할 tooan 전자 메일 너무[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com)합니다.

- 충돌 발생 하는 경우, CosmosDB.StartupEntryPoint.exe hello 관리자 명령 프롬프트에서 다음 명령을 실행 합니다.`lodctr /R` 

- 연결에 문제가 발생 하는 경우 [추적 파일을 수집](#trace-files), 압축 및 첨부할 tooan 전자 메일 너무[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com)합니다.

- 표시 되 면 한 **서비스를 사용할 수 없는** hello 에뮬레이터에서 실패할 수 tooinitialize hello 네트워크 스택, 메시지입니다. 검사 toosee hello 펄스 있는 경우 보안 클라이언트 또는 Juniper 네트워크 클라이언트를 설치 하 고, 해당 네트워크 필터 드라이버는 hello 문제가 발생할 수 있습니다. Hello 문제를 해결 일반적으로 타사 네트워크 필터 드라이버를 제거 합니다.

### <a id="trace-files"></a>추적 파일 수집

toocollect hello 명령 관리 명령 프롬프트에서 다음을 실행 하는 추적을 디버깅 합니다.

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. `CosmosDB.Emulator.exe /shutdown` 조사식 hello 시스템 트레이 toomake 있는지 hello 프로그램이 종료 된, 1 분이 걸릴 수 있습니다. 클릭 해도 **종료** hello Azure Cosmos DB 에뮬레이터 사용자 인터페이스에 있습니다.
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. Hello 문제를 재현 합니다. 데이터 탐색기 작동 하지 않는 경우만 toowait은 몇 초 toocatch hello 오류에 대 한 브라우저 tooopen hello에 대 한 필요 합니다.
5. `CosmosDB.Emulator.exe /stoptraces`
6. 너무 이동`%ProgramFiles%\Azure Cosmos DB Emulator` hello docdbemulator_000001.etl 파일을 찾습니다.
7. 재현 단계와 함께 hello.etl 파일을 너무 보내기[ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com) 디버깅 합니다.

### <a id="uninstall"></a>제거의 로컬 에뮬레이터 hello

1. Hello의 열려 있는 모든 인스턴스를 종료 hello 시스템 트레이에서 hello Azure Cosmos DB 에뮬레이터 아이콘을 마우스 오른쪽 단추로 클릭 한 다음 종료를 클릭 하 여 로컬 에뮬레이터입니다. 모든 인스턴스 tooexit 1 분을 걸릴 수 있습니다.
2. Hello Windows 검색 상자에 입력 **응용 프로그램 및 기능** hello에서을 클릭 하 고 **응용 프로그램 및 기능 (시스템 설정)** 결과입니다.
3. Hello 앱 목록에서 스크롤합니다 너무**Azure Cosmos DB 에뮬레이터**, 선택, 클릭 **제거**후 확인 하 고 클릭 **제거** 다시 합니다.
4. Hello 앱을 제거할 때 이동 tooC:\Users\<사용자 > \AppData\Local\CosmosDBEmulator 및 delete hello 폴더입니다. 

## <a name="next-steps"></a>다음 단계

이 자습서에서는 hello 다음 작업을 수행 하면:

> [!div class="checklist"]
> * 설치의 로컬 에뮬레이터 hello
> * Rand hello Windows 용 Docker에는 에뮬레이터
> * 요청 인증
> * Hello 에뮬레이터의에서 hello 데이터 탐색기를 사용합니다.
> * SSL 인증서 내보내기
> * 에뮬레이터의 hello hello 명령줄에서 호출
> * 추적 파일 수집

이 자습서에서는 toouse 무료 로컬 개발을 위한 로컬 에뮬레이터 hello 하는 방법을 배웠습니다. 이제 toohello 다음 자습서를 진행 하 고 알아볼 수 있습니다 어떻게 tooexport 에뮬레이터 SSL 인증서입니다. 

> [!div class="nextstepaction"]
> [Hello Azure Cosmos DB 에뮬레이터 인증서 내보내기](local-emulator-export-ssl-certificates.md)
