---
title: "분할 / 병합 서비스 aaaDeploy | Microsoft Docs"
description: "탄력적 데이터베이스 도구를 사용하는 분할 및 병합"
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 9a993c0f-7052-46cd-aa59-073bea8d535a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 6fef641cbc1e73ce34a851c53298a072dade8f9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-split-merge-service"></a>분할/병합 서비스 배포
hello 분할 / 병합 도구를 사용 하면 분할 된 데이터베이스 간에 데이터를 이동할 수 있습니다. [확장된 클라우드 데이터베이스 간 데이터 이동](sql-database-elastic-scale-overview-split-and-merge.md)

## <a name="download-hello-split-merge-packages"></a>Hello 분할 / 병합 패키지 다운로드
1. Hello 최신 NuGet 버전에서 다운로드 [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget)합니다.
2. 명령 프롬프트를 열고 nuget.exe 다운로드 toohello 디렉터리를 이동 합니다. hello 다운로드 PowerShell commmands 포함 되어 있습니다.
3. 아래의 명령 hello로 hello 현재 디렉터리로 hello 최신 분할 / 병합 패키지를 다운로드 합니다.
   ```
   nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge
   ```  

hello 파일이 디렉터리에 배치 됩니다 **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** 여기서 *x.x.xxx.x* hello 버전 번호를 반영 합니다. Hello hello 분할 / 병합 서비스 파일을 찾으려면 **content\splitmerge\service** 하위 디렉터리 및 hello 분할 / 병합 PowerShell 스크립트 (및 필요한 클라이언트.dll) hello **content\splitmerge\powershell** 하위 디렉터리입니다.

## <a name="prerequisites"></a>필수 조건
1. Hello 분할 / 병합 상태를 데이터베이스로 사용 될 Azure SQL DB 데이터베이스를 만듭니다. Toohello 이동 [Azure 포털](https://portal.azure.com)합니다. 새 **SQL 데이터베이스**를 만듭니다. Hello 데이터베이스 이름을 지정 하 고 새 관리자 및 암호를 만듭니다. 있는지 toorecord hello 이름 및 암호를 나중에 사용할 수 있습니다.
2. Azure SQL DB 서버에 Azure 서비스 tooconnect tooit을 허용 하는지 확인 합니다. Hello 포털 hello에 **방화벽 설정**, 해당 hello 확인 **tooAzure 서비스 액세스를 허용** 너무 설정은**에**합니다. Hello "저장" 아이콘을 클릭 합니다.
   
   ![허용된 서비스][1]
3. 진단 출력에 사용할 Azure 저장소 계정을 만듭니다. Azure 포털 toohello를 이동 합니다. Hello 왼쪽된 모음에서 **새로**, 클릭 **데이터 + 저장소**, 다음 **저장소**합니다.
4. 분할/병합 서비스를 포함할 Azure 클라우드 서비스를 만듭니다.  Azure 포털 toohello를 이동 합니다. Hello 왼쪽된 모음에서 **새로**, 다음 **계산**, **클라우드 서비스**, 및 **만들기**합니다. 

## <a name="configure-your-split-merge-service"></a>분할/병합 서비스 구성
### <a name="split-merge-service-configuration"></a>분할/병합 서비스 구성
1. 분할 / 병합 hello 어셈블리 다운로드 hello 폴더에서 hello의 복사본을 만듭니다 **ServiceConfiguration.Template.cscfg** 와 함께 제공 된 파일 **SplitMergeService.cspkg** 하 고 이름을 **ServiceConfiguration.cscfg**합니다.
2. 열기 **ServiceConfiguration.cscfg** 인증서 지문 안녕하세요 형식 등의 입력의 유효성을 검사 하는 Visual Studio와 같은 텍스트 편집기에서.
3. 새 데이터베이스 만들기 또는 분할 / 병합 작업에 대 한 hello 상태 데이터베이스 이름으로 기존 데이터베이스 tooserve을 선택 하 고 해당 데이터베이스의 연결 문자열 hello를 검색 합니다. 
   
   > [!IMPORTANT]
   > 이때 hello 상태 데이터베이스 hello 라틴어 데이터 정렬을 사용 해야 합니다 (SQL\_Latin1\_일반\_CP1\_CI\_AS)입니다. 자세한 내용은 [Windows 데이터 정렬 이름(TRANSACT-SQL)](https://msdn.microsoft.com/library/ms188046.aspx)을 참조하세요.
   >

   Azure SQL DB, 연결 문자열 hello hello 폼의 일반적으로 됩니다.
      ```
      Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
      ```

4. 두 hello에 hello cscfg 파일에이 연결 문자열을 입력 **SplitMergeWeb** 및 **SplitMergeWorker** hello ElasticScaleMetadata 설정의 역할 섹션.
5. Hello에 대 한 **SplitMergeWorker** 역할 hello에 대 한 올바른 연결 문자열 tooAzure 저장소 입력 **WorkerRoleSynchronizationStorageAccountConnectionString** 설정 합니다.

### <a name="configure-security"></a>보안 구성
자세한 지침은 tooconfigure hello hello 서비스의 보안을 위해 toohello 참조 [분할 / 병합 보안 구성](sql-database-elastic-scale-split-merge-security-configuration.md)합니다.

Hello이이 자습서에 대 한 간단한 테스트 배포를 위해 최소한의 구성 단계 tooget hello 서비스 시작 및 실행을 수행 합니다. 다음이 단계 계정을 사용 하도록 설정만 hello 하나의 컴퓨터/toocommunicate hello 서비스를 실행 합니다.

### <a name="create-a-self-signed-certificate"></a>자체 서명된 인증서 만들기
새 디렉터리에서 다음 명령을 사용 하 여이 디렉터리 execute hello는 [Visual Studio 용 개발자 명령 프롬프트](http://msdn.microsoft.com/library/ms229859.aspx) 창:

   ```
    makecert ^
    -n "CN=*.cloudapp.net" ^
    -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2" ^
    -a sha1 -len 2048 ^
    -sr currentuser -ss root ^
    -sv MyCert.pvk MyCert.cer
   ```

암호 tooprotect hello 개인 키에 대 한 묻는 메시지가 표시 됩니다. 강력한 암호를 입력하고 이를 확인합니다. 그러면 hello 암호 toobe 그 후 한 번 더 사용에 대 한 메시지가 표시 됩니다. 클릭 **예** hello 끝 tooimport에서 것 toohello 신뢰할 수 있는 인증 기관, 루트 저장소입니다.

### <a name="create-a-pfx-file"></a>PFX 파일 만들기
Hello hello에서 다음 명령을 실행 makecert; 실행 위치 같은 창 사용 하 여 동일한 암호를 사용한 toocreate hello 인증서를 hello:

    pvk2pfx -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx -pi <password>

### <a name="import-hello-client-certificate-into-hello-personal-store"></a>Hello hello 개인 저장소로 클라이언트 인증서 가져오기
1. Windows 탐색기에서 **MyCert.pfx**를 두 번 클릭합니다.
2. Hello에 **인증서 가져오기 마법사** 선택 **현재 사용자** 클릭 **다음**합니다.
3. Hello 파일 경로 확인 하 고 클릭 **다음**합니다.
4. Leave hello 암호 입력 **모든 확장된 속성을 포함** 채로 클릭 **다음**합니다.
5. 둡니다 **자동으로 선택 hello 인증서 저장소 [...]**  채로 클릭 **다음**합니다.
6. **마침**, **확인**을 차례로 클릭합니다.

### <a name="upload-hello-pfx-file-toohello-cloud-service"></a>업로드 hello PFX 파일 toohello 클라우드 서비스
1. Toohello 이동 [Azure 포털](https://portal.azure.com)합니다.
2. **클라우드 서비스**를 선택합니다.
3. Hello 분할/병합 서비스에 대 한 위에서 만든 hello 클라우드 서비스를 선택 합니다.
4. 클릭 **인증서** hello 최상위 메뉴에 있습니다.
5. 클릭 **업로드** hello 아래쪽 표시줄에 있습니다.
6. Hello PFX 파일을 선택 하 고 hello 입력 위와 동일한 암호입니다.
7. 완료 되 면 hello hello 목록에 새 항목에서 hello 인증서 지문을 복사 합니다.

### <a name="update-hello-service-configuration-file"></a>Hello 서비스 구성 파일 업데이트
이러한 설정의 hello 지문/value 특성에 위의 복사 hello 인증서 지문을 붙여 넣습니다.
Hello 작업자 역할:
   ```
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

Hello 웹 역할:

   ```
    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />
    <Setting name="AllowedClientCertificateThumbprints" value="" />
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

암호화, CA, hello에 대 한 별도 인증서를 사용 해야 하는 프로덕션 배포에 대 한 hello 서버 인증서 및 클라이언트 인증서를 하십시오. 이와 관련된 자세한 지침은 [보안 구성](sql-database-elastic-scale-split-merge-security-configuration.md)을 참조하세요.

## <a name="deploy-your-service"></a>서비스 배포
1. Toohello 이동 [Azure 포털](https://manage.windowsazure.com)합니다.
2. Hello 클릭 **클라우드 서비스** hello 왼쪽에 탭을 앞에서 만든 hello 클라우드 서비스를 선택 합니다.
3. **Dashboard**를 클릭합니다.
4. 환경 준비 hello를 선택한 다음 클릭 **새 스테이징 배포를 업로드**합니다.
   
   ![스테이징][3]
5. Hello 대화 상자에서 배포 레이블을 입력 합니다. '패키지'와 '구성' 모두에 대 한 '에서 로컬 '를 클릭 하 고 hello 선택 **SplitMergeService.cspkg** 파일 및 이전에 구성 된.cscfg 파일.
6. 해당 hello 확인란 확인 **하나 이상의 역할 단일 인스턴스가 포함 된 경우에 배포** 을 선택 합니다.
7. Hello 맨 아래 오른쪽 toobegin hello 배포에서 hello 눈금 단추를 누릅니다. Tootake 예상 몇 분 toocomplete 합니다.

   ![업로드][4]

## <a name="troubleshoot-hello-deployment"></a>Hello 배포 문제 해결
웹 역할에 실패 하면 toocome 온라인가 hello 보안 구성에 문제가 있습니다. 위에 설명 된 대로 SSL이 구성 되어 해당 hello를 확인 합니다.

작업자 역할 toocome 온라인으로 실패 하는 경우 웹 역할에 성공 하면 것은 앞에서 만든 toohello 상태 데이터베이스 연결 문제가 있는 대부분입니다.

* 프로그램.cscfg의 hello 연결 문자열이 정확한 지 확인 합니다.
* Hello 서버와 데이터베이스 존재 하는지, 그리고 hello 사용자 id와 암호가 올바른지 확인 합니다.
* Azure SQL DB에 대 한 연결 문자열 hello hello 형식 이어야 합니다.

   ```  
   Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
   ```

* 해당 hello 서버 이름의로 시작 하지 않으면 확인 **https://**합니다.
* Azure SQL DB 서버에 Azure 서비스 tooconnect tooit을 허용 하는지 확인 합니다. toodo이를 열고 https://manage.windowsazure.com 왼쪽 hello에서 "SQL 데이터베이스"를 클릭, 클릭 "서버" hello 위쪽에, 한 서버를 선택 합니다. 클릭 **구성** hello에 가장 많이 사용 하 고 해당 hello 확인 **Azure 서비스** 설정 되어 너무 "Yes"입니다. (Hello 필수 구성 요소를 참조 하십시오.이 문서의 hello 위쪽 섹션).

## <a name="test-hello-service-deployment"></a>Hello 서비스 배포를 테스트 합니다.
### <a name="connect-with-a-web-browser"></a>웹 브라우저와 연결
분할 / 병합 서비스의 hello 웹 끝점을 결정 합니다. Toohello 이동 하 여 hello Azure 클래식 포털에서에서이 찾을 수 있습니다 **대시보드** 클라우드 서비스 및 아래 **사이트 URL** hello 오른쪽에 있습니다. 대체 **http://** 와 **https://** 이후 hello 기본 보안 설정을 hello HTTP 끝점을 사용 하지 않도록 설정 합니다. 이 URL에 대 한 hello 페이지를 브라우저에 로드 합니다.

### <a name="test-with-powershell-scripts"></a>PowerShell 스크립트로 테스트
hello 배포 및 사용자 환경을 포함 하는 hello 샘플 PowerShell 스크립트를 실행 하 여 테스트할 수 있습니다.

hello 스크립트 파일이 포함 됩니다.

1. **SetupSampleSplitMergeEnvironment.ps1** - 분할/병합에 대한 테스트 데이터 계층을 설정합니다. 자세한 설명은 아래 테이블을 참조하세요.
2. **ExecuteSampleSplitMerge.ps1** -hello 테스트에서 테스트 작업을 실행 합니다 (자세한 설명은 아래 표 참조)는 데이터 계층
3. **GetMappings.ps1** 최상위-샘플 hello hello 분할 매핑의 현재 상태를 출력 하는 스크립트입니다.
4. **ShardManagement.psm1** -도우미 스크립트 래핑하는 hello ShardManagement API
5. **SqlDatabaseHelpers.psm1** – SQL Database 생성 및 관리를 위한 도우미 스크립트입니다.
   
   <table style="width:100%">
     <tr>
       <th>PowerShell 파일</th>
       <th>단계</th>
     </tr>
     <tr>
       <th rowspan="5">SetupSampleSplitMergeEnvironment.ps1</th>
       <td>1.    분할된 데이터베이스 맵 관리자 데이터베이스를 만듭니다.</td>
     </tr>
     <tr>
       <td>2.    분할된 데이터베이스를 2개 만듭니다.
     </tr>
     <tr>
       <td>3.    해당 데이터베이스에 대한 분할된 데이터베이스 맵을 만듭니다. 이때 해당 데이터베이스의 기존 분할된 데이터베이스 맵은 삭제됩니다. </td>
     </tr>
     <tr>
       <td>4.    두 hello 분할 영역에는 작은 예제 테이블을 만들고 hello 분할 된 데이터베이스 중 하나에 hello 테이블을 채웁니다.</td>
     </tr>
     <tr>
       <td>5.    Hello 분할 된 테이블에 대 한 hello SchemaInfo를 선언합니다.</td>
     </tr>
   </table>
   <table style="width:100%">
     <tr>
       <th>PowerShell 파일</th>
       <th>단계</th>
     </tr>
   <tr>
       <th rowspan="4">ExecuteSampleSplitMerge.ps1 </th>
       <td>1.    분할 요청 toohello 분할 / 병합 서비스 웹 프런트 엔드를, hello 첫 번째 분할 toohello 두 번째 분할의 절반 hello 데이터를 분할 하 보냅니다.</td>
     </tr>
     <tr>
       <td>2.    설문 hello hello 요청 완료 될 때까지 요청 상태 및 대기를 분할 하는 hello에 대 한 웹 프런트 엔드 합니다.</td>
     </tr>
     <tr>
       <td>3.    병합 요청 toohello 분할 / 병합 서비스 웹 프런트 엔드를, hello 두 번째 분할 백 toohello 첫 번째 분할에서 hello 데이터를 이동 하 보냅니다.</td>
     </tr>
     <tr>
       <td>4.    폴링 hello 웹 프런트 엔드 hello 병합 요청 상태와 hello 요청 완료 될 때까지 대기 합니다.</td>
     </tr>
   </table>
   
## <a name="use-powershell-tooverify-your-deployment"></a>PowerShell tooverify 배포 사용
1. 새 PowerShell 창을 열고 고 hello 분할 / 병합 패키지를 다운로드 한 toohello 디렉터리 이동한 hello "powershell" 디렉터리로 이동 합니다.
2. Azure SQL 데이터베이스 서버 만들기 (또는 기존 서버 선택) 분할 하 고 hello shard map manager 만들 수 있습니다.
   
   > [!NOTE]
   > hello SetupSampleSplitMergeEnvironment.ps1 스크립트 hello에 이러한 모든 데이터베이스를 만듭니다 기본 tookeep hello 스크립트 단순 하 여 동일한 서버입니다. 이 한 제한은 아닙니다 hello 분할 / 병합 서비스의 자체입니다.
   >
   
   SQL 인증 로그인 읽기/쓰기 액세스 toohello Db hello 분할 / 병합 서비스 toomove 데이터 및 업데이트 hello 분할 맵을 충족 합니다. Hello 클라우드에서 hello 분할 / 병합 서비스를 실행 하므로 지원 하지 않습니다 현재 통합 인증.
   
   Hello Azure SQL server 구성 되어 있는지 확인 이러한 스크립트를 실행 하는 hello 컴퓨터의 IP 주소 hello에서에서 tooallow 액세스 합니다. 이 설정은 hello Azure SQL server에서 찾을 수 / 구성 / IP 주소를 사용할 수 있습니다.
3. Hello SetupSampleSplitMergeEnvironment.ps1 스크립트 toocreate hello 예제 환경을 실행 합니다.
   
   이 스크립트를 실행 구조 hello shard map manager 데이터베이스 및 hello 분할 된 데이터베이스에 모든 기존 분할 맵 관리 데이터 초기화 됩니다. 초기화를 toore hello 분할 맵은 또는 분할 하려는 경우 유용한 toorerun hello 스크립트 수도 있습니다.
   
   샘플 명령줄:

   ```   
     .\SetupSampleSplitMergeEnvironment.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'
   ```      
4. Hello Getmappings.ps1 스크립트 tooview hello 매핑이 현재 존재 하는 hello 샘플 환경에서 실행 됩니다.
   
   ```
     .\GetMappings.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'

   ```         
5. (데이터를 이동 절반 hello hello 첫 번째 분할 toohello 두 번째 분할) 분할 작업 한 다음 병합 작업 (hello 데이터를 다시 hello 첫 번째 분할 영역으로 이동) hello ExecuteSampleSplitMerge.ps1 스크립트 tooexecute를 실행 합니다. SSL 및 사용 하지 않도록 설정 하는 왼쪽된 hello http 끝점을 구성한 경우 hello https:// 끝점을 대신 사용 하는 확인 합니다.
   
   샘플 명령줄:

   ```   
     .\ExecuteSampleSplitMerge.ps1
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net' 
         -SplitMergeServiceEndpoint 'https://mysplitmergeservice.cloudapp.net' 
         -CertificateThumbprint '0123456789abcdef0123456789abcdef01234567'
   ```      
   
   Hello 아래의 오류를 받을 경우 대부분 웹 끝점의 인증서에 문제가입니다. 즐겨 찾는 웹 브라우저를 사용 하 여 toohello 웹 끝점 연결을 시도 하 고 인증서 오류가 있는지 확인 합니다.
   
     ```
     Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLSsecure channel.
     ```
   
   성공 하는 경우 아래 hello 같이 hello 출력 표시 됩니다.
   
   ```
   > .\ExecuteSampleSplitMerge.ps1 -UserName 'mysqluser' -Password 'MySqlPassw0rd' -ShardMapManagerServerName 'abcdefghij.database.windows.net' -SplitMergeServiceEndpoint 'http://mysplitmergeservice.cloudapp.net' -CertificateThumbprint 0123456789abcdef0123456789abcdef01234567
   > Sending split request
   > Began split operation with id dc68dfa0-e22b-4823-886a-9bdc903c80f3
   > Polling split-merge request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Waiting for reference tables copy     completion.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > Sending merge request
   > Began merge operation with id 6ffc308f-d006-466b-b24e-857242ec5f66
   > Polling request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > 
   ```
6. 다른 데이터 형식으로도 연결해 봅니다. 이러한 스크립트를 모두 수행 toospecify hello 키 유형 수 있는 선택적-ShardKeyType 매개 변수입니다. hello 기본값은 Int32, 하지만 Int64, Guid 또는 이진 파일을 지정할 수도 있습니다.

## <a name="create-requests"></a>요청 만들기
hello 웹 UI를 사용 하 여 또는 가져오기 및 hello 웹 역할을 통해 사용자 요청을 제출 하는 hello SplitMerge.psm1 PowerShell 모듈을 사용 하 여 hello 서비스를 사용할 수 있습니다.

hello 서비스에 분할 된 테이블과 참조 테이블에서 데이터를 이동할 수 있습니다. 분할된 테이블에는 분할 키 열과 각 분할 키에 대한 여러 행의 데이터가 있습니다. 참조 테이블이 분할 되지 않는 모든 분할 영역에 데이터를 행 동일 하므로 hello를 포함 합니다. 참조 테이블은 데이터가 자주 변경 되지 않는 사용 하는 tooJOIN 된 쿼리에서 분할 된 테이블을 더 유용 합니다.

순서 tooperform 분할 / 병합 작업 hello 분할 된 테이블 및 참조 테이블을 이동 toohave를 선언 해야 합니다. Hello로 이렇게 **SchemaInfo** API입니다. 이 API는 hello에 **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** 네임 스페이스입니다.

1. 각 분할 된 테이블에 대해 만듭니다는 **ShardedTableInfo** hello 테이블의 부모 스키마 이름을 설명 하는 개체 (선택 사항 너무 기본값 "dbo"), 테이블 이름으로 hello 및 hello hello 분할 키가 포함 된 해당 테이블의 열 이름입니다.
2. 각 참조 테이블에 대해 만듭니다는 **ReferenceTableInfo** hello 테이블의 부모 스키마 이름을 설명 하는 개체 (선택 사항 너무 기본값 "dbo")와 hello 테이블 이름입니다.
3. 새 TableInfo 개체 tooa 위에 hello 추가 **SchemaInfo** 개체입니다.
4. 참조 tooa 가져오기 **ShardMapManager** 개체 및 호출 **GetSchemaInfoCollection**합니다.
5. Hello 추가 **SchemaInfo** toohello **SchemaInfoCollection**, hello shard map 이름을 제공 합니다.

이러한 예는 hello SetupSampleSplitMergeEnvironment.ps1 스크립트에서에서 볼 수 있습니다.

분할 / 병합 서비스 hello 만들지 않습니다 hello 대상 데이터베이스 (또는 hello 데이터베이스의 모든 테이블에 대 한 스키마)에 있습니다. 미리 생성 toohello 서비스 요청을 보내기 전에 되어야 합니다.

## <a name="troubleshooting"></a>문제 해결
Hello 샘플 powershell 스크립트를 실행할 때는 hello 아래 메시지가 나타날 수 있습니다.

   ```
   Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLS secure channel.
   ```

이 오류는 SSL 인증서가 제대로 구성되지 않은 것을 의미합니다. '웹 브라우저와 연결' 섹션의 지침에 hello 키를 따르십시오.

요청을 제출할 수 없는 경우에 다음이 나타날 수 있습니다.

```
[Exception] System.Data.SqlClient.SqlException (0x80131904): Could not find stored procedure 'dbo.InsertRequest'. 
```

이 경우에 대해 특정 hello 설정에 구성 파일을 확인 **WorkerRoleSynchronizationStorageAccountConnectionString**합니다. 이 오류는 일반적으로 해당 hello 작업자 역할 처음 사용 시 hello 메타 데이터 데이터베이스를 성공적으로 초기화할 수 없음을 나타냅니다. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/allowed-services.png
[2]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/manage.png
[3]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/staging.png
[4]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/upload.png
[5]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/storage.png

