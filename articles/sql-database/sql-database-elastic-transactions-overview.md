---
title: "클라우드 데이터베이스에 걸쳐 aaaDistributed 트랜잭션"
description: "Azure SQL 데이터베이스와 탄력적 데이터베이스 트랜잭션 개요"
services: sql-database
documentationcenter: 
author: torsteng
manager: jhubbard
editor: torsteng
ms.assetid: e14df7a3-7788-4cfb-bcd1-7ad6433ef1f9
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: sql-database
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 9a18f2749108d337bf115b3dc21dd0c7828dd9c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="distributed-transactions-across-cloud-databases"></a>클라우드 데이터베이스의 분산 트랜잭션
Azure SQL 데이터베이스 (SQL 데이터베이스)에 대 한 탄력적 데이터베이스 트랜잭션은 SQL DB에 여러 데이터베이스에 걸쳐 있는 toorun 트랜잭션을 허용 합니다. SQL DB에 대 한 탄력적 데이터베이스 트랜잭션 ADO.NET을 사용 하 여.NET 응용 프로그램에 사용할 수 있으며 hello를 사용 하 여 hello 친숙 한 프로그래밍 환경에 통합 [리스트](https://msdn.microsoft.com/library/system.transactions.aspx) 클래스입니다. tooget hello 라이브러리 참조 [.NET Framework 4.6.1 (웹 설치 관리자)](https://www.microsoft.com/download/details.aspx?id=49981)합니다.

온-프레미스에서 이러한 시나리오는 Microsoft Distributed Transaction Coordinator(MSDTC) 실행을 필요로 합니다. MSDTC를 azure에서 플랫폼-as a Service 응용 프로그램에 대해 사용할 수 없는 이후 hello 기능 toocoordinate 분산 트랜잭션은 이제 직접에 통합 되었으며 SQL DB 합니다. 응용 프로그램은 tooany SQL 데이터베이스 toolaunch 분산 트랜잭션 연결 하 고 hello 다음 그림에에서 나와 있는 것 처럼에 hello distributed transaction를 투명 하 게 조정 해야 합니다 hello 데이터베이스 중 하나입니다. 

  ![탄력적 데이터베이스 트랜잭션을 사용한 Azure SQL 데이터베이스와 분산 트랜잭션 ][1]

## <a name="common-scenarios"></a>일반적인 시나리오
SQL DB에 대 한 탄력적 데이터베이스 트랜잭션 응용 프로그램 toomake 변경을 toodata 여러 SQL 데이터베이스에 저장을 사용 하도록 설정 합니다. hello 미리 보기는 C# 및.NET에서 클라이언트 쪽 개발 환경을에 중점을 둡니다. T-SQL을 사용한 서버 쪽 환경은 차후에 계획되어 있습니다.  
탄력적 데이터베이스 트랜잭션 대상 hello 다음 시나리오:

* Azure의 다중 데이터베이스 응용 프로그램: 이 시나리오의 경우 데이터가 SQL DB의 여러 데이터베이스에 걸쳐 수직으로 분할되어 있고 다른 종류의 데이터가 다른 데이터베이스에 상주합니다. 일부 작업에 둘 이상의 데이터베이스에서 유지 되는 변경 내용을 toodata가 필요 합니다. hello 응용 프로그램 데이터베이스에 걸쳐 탄력적 데이터베이스 트랜잭션 toocoordinate hello 변경 내용을 사용 하 여 및 원자성을 보장 하기.
* Azure에서 분할 된 데이터베이스 응용 프로그램:이 시나리오에서는 hello 데이터 계층에서 사용 하 여 hello [탄력적 데이터베이스 클라이언트 라이브러리](sql-database-elastic-database-client-library.md) 또는 자체 분할 toohorizontally SQL DB에 여러 데이터베이스에 걸쳐 hello 데이터를 분할 합니다. 한 주요 사용 사례가 hello 필요 tooperform 분할 된 다중 테 넌 트 응용 프로그램에 대 한 원자성 변경 때 테 넌 트에 걸쳐 변경 합니다. 예를 들어 서로 다른 데이터베이스에 상주 하는 한 테 넌 트 tooanother에서 집합으로 전송 생각 하면 됩니다. 두 번째 경우에 일반적으로 hello에 사용 되는 여러 데이터베이스에 걸쳐 원자성 작업 요구 toostretch 일부 동일한 테 넌 트를 의미 함 큰 테 넌 트에 대 한 세분화 된 분할 tooaccommodate 용량 요구 사항입니다. 세 번째 경우는 복제 되는 데이터베이스에 걸쳐 원자성 업데이트 tooreference 데이터입니다. 이러한 맥락 원자성 트랜잭션된 작업 hello 미리 보기를 사용 하 여 여러 데이터베이스 간에 조정 이제 수 있습니다.
  탄력적 데이터베이스 트랜잭션 데이터베이스에서 2 단계 커밋 tooensure 트랜잭션 원자성을 사용합니다. 이것은 단일 트랜잭션 내에 한 번에 100개 미만의 데이터베이스가 관여되는 트랜잭션에 적합합니다. 이러한 한도가 적용 되지 않습니다 되지만 이러한 한도 초과할 때 성능 및 탄력적 데이터베이스 트랜잭션 toosuffer에 대 한 성공률 예상 해야 하나 있습니다.

## <a name="installation-and-migration"></a>설치 및 마이그레이션
SQL DB에서 트랜잭션 탄력적 데이터베이스에 대 한 hello 기능 System.Data.dll 및 System.Transactions.dll 업데이트 toohello.NET 라이브러리를 통해 제공 됩니다. hello Dll 해당 시 점으로부터 2 단계 커밋 사용 되도록 필요한 경우 tooensure 원자성입니다. 탄력적 데이터베이스 트랜잭션을 사용 하 여 toostart 개발할 때는 응용 프로그램 설치 [.NET Framework 4.6.1](https://www.microsoft.com/download/details.aspx?id=49981) 또는 이후 버전입니다. 와 이전 버전의 hello.NET framework에서 실행 되는 경우 트랜잭션을 toopromote tooa distributed transaction 못하며 예외가 발생 합니다.

설치 후 연결 tooSQL DB System.Transactions hello distributed transaction Api를 사용할 수 있습니다. 4.6.1 hello를 설치한 후.NET 4.6에 대 한 기존 응용 프로그램 재작성 이러한 Api를 사용 하는 기존 MSDTC 응용 프로그램의 경우 프레임 워크입니다. 프로젝트는.NET 4.6을 대상으로 하는 경우 연결 tooSQL DB 이제 성공할 함께에서 hello 새 프레임 워크 버전 및 분산된 트랜잭션 API 호출에서 업데이트 하는 hello Dll을 자동으로 사용 됩니다.

탄력적 데이터베이스 트랜잭션은 MSDTC를 설치할 필요가 없습니다. 대신 탄력적 데이터베이스 트랜잭션은 SQL DB 내에서 SQL DB에 의해 직접적으로 관리됩니다. 이 크게 MSDTC의 배포는 SQL DB를 사용 하 여 필요한 toouse 분산 트랜잭션을 아니므로 클라우드 시나리오를 단순화 합니다. 섹션 4 toodeploy 탄력적 데이터베이스 트랜잭션 및 hello 필요한 클라우드 응용 프로그램 tooAzure 함께.NET framework 방법을 자세히 설명 합니다.

## <a name="development-experience"></a>개발 환경
### <a name="multi-database-applications"></a>다중 데이터베이스 응용 프로그램
hello 다음 샘플 코드에서는 hello 익숙한 프로그래밍 경험.NET System.Transactions 사용 TransactionScope 클래스 hello.net에서 앰비언트 트랜잭션을 설정합니다. ("앰비언트 트랜잭션이"는 하나에 있는 현재 스레드의 hello.) Hello TransactionScope 내에서 열린 모든 연결 hello 트랜잭션에 참여 합니다. 서로 다른 데이터베이스 참여 하는 경우 hello 트랜잭션이 자동으로 상승 된 tooa distributed transaction이입니다. hello 트랜잭션의 hello 결과 커밋 hello 범위 toocomplete tooindicate를 설정 하 여 제어 됩니다.

    using (var scope = new TransactionScope())
    {
        using (var conn1 = new SqlConnection(connStrDb1))
        {
            conn1.Open();
            SqlCommand cmd1 = conn1.CreateCommand();
            cmd1.CommandText = string.Format("insert into T1 values(1)");
            cmd1.ExecuteNonQuery();
        }

        using (var conn2 = new SqlConnection(connStrDb2))
        {
            conn2.Open();
            var cmd2 = conn2.CreateCommand();
            cmd2.CommandText = string.Format("insert into T2 values(2)");
            cmd2.ExecuteNonQuery();
        }

        scope.Complete();
    }

### <a name="sharded-database-applications"></a>분할된 데이터베이스 응용 프로그램
SQL DB에 대 한 탄력적 데이터베이스 트랜잭션 위치 방법을 사용 하 여 hello OpenConnectionForKey hello 탄력적 데이터베이스 클라이언트 라이브러리 tooopen 연결의 경우 수평 확장 된 데이터에 대 한 분산된 트랜잭션을 조정도 지원 계층입니다. 여러 다른 분할 키 값에서 변경 내용에 대 한 tooguarantee 트랜잭션 일관성을 해야 하는 경우를 고려 합니다. Hello 다른 분할 키 값을 호스팅 toohello 분할 영역 연결 OpenConnectionForKey를 사용 하 여 조정 된 합니다. Hello 일반적인 경우는 분산된 트랜잭션이 필요 트랜잭션 보장 보장 되도록 hello 연결 toodifferent 분할 될 수 있습니다. 아래의 코드 예제는 hello이이 방법을 보여 줍니다. 있다고 가정 shardmap 라는 변수는 분할 맵 hello 탄력적 데이터베이스 클라이언트 라이브러리에서 사용 되는 toorepresent:

    using (var scope = new TransactionScope())
    {
        using (var conn1 = shardmap.OpenConnectionForKey(tenantId1, credentialsStr))
        {
            conn1.Open();
            SqlCommand cmd1 = conn1.CreateCommand();
            cmd1.CommandText = string.Format("insert into T1 values(1)");
            cmd1.ExecuteNonQuery();
        }

        using (var conn2 = shardmap.OpenConnectionForKey(tenantId2, credentialsStr))
        {
            conn2.Open();
            var cmd2 = conn2.CreateCommand();
            cmd2.CommandText = string.Format("insert into T1 values(2)");
            cmd2.ExecuteNonQuery();
        }

        scope.Complete();
    }


## <a name="net-installation-for-azure-cloud-services"></a>Azure 클라우드 서비스용 .NET 설치
Azure는 여러 제품 toohost.NET 응용 프로그램을 제공합니다. Hello는 다양 한 제품의 비교는에서 사용할 수 있는 [Azure 앱 서비스, 클라우드 서비스 및 가상 컴퓨터 비교](../app-service-web/choose-web-site-cloud-service-vm.md)합니다. Hello hello 제공의 게스트 OS 보다 작은 경우.NET 4.6.1 탄력적 트랜잭션에 필요한, tooupgrade hello 게스트 OS too4.6.1을 해야 합니다. 

Azure 앱 서비스에 대 한 업그레이드 toohello 게스트 OS는 현재 지원 되지 않습니다. Azure 가상 컴퓨터에 대 한 hello VM에 로그인 하기만 하면 및 hello hello 최신.NET framework 설치 관리자를 실행 합니다. Azure 클라우드 서비스에 대 한 배포의 hello 시작 작업에 최신.NET 버전의 tooinclude hello 설치를 해야합니다. hello 개념 및 단계에 설명 되어 [클라우드 서비스 역할에.NET 설치](../cloud-services/cloud-services-dotnet-install-dotnet.md)합니다.  

.NET 4.6.1 hello hello.NET 4.6 설치 관리자 보다 Azure 클라우드 서비스에서 프로세스를 부트스트래핑 하는 동안 임시 저장소를 더 필요할 수 있습니다에 대 한 설치 관리자를 hello 유의 합니다. 설치를 성공적으로 tooensure tooincrease 임시 저장소가 필요한 Azure 클라우드 서비스에 대 한 hello LocalResources 섹션 및 시작 작업의 hello 환경 설정의 ServiceDefinition.csdef 파일에서 hello 다음과 같이 샘플:

    <LocalResources>
    ...
        <LocalStorage name="TEMP" sizeInMB="5000" cleanOnRoleRecycle="false" />
        <LocalStorage name="TMP" sizeInMB="5000" cleanOnRoleRecycle="false" />
    </LocalResources>
    <Startup>
        <Task commandLine="install.cmd" executionContext="elevated" taskType="simple">
            <Environment>
        ...
                <Variable name="TEMP">
                    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='TEMP']/@path" />
                </Variable>
                <Variable name="TMP">
                    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='TMP']/@path" />
                </Variable>
            </Environment>
        </Task>
    </Startup>

## <a name="transactions-across-multiple-servers"></a>여러 서버 간의 트랜잭션
탄력적 데이터베이스 트랜잭션은 Azure SQL 데이터베이스의 여러 논리 서버에 걸쳐 지원됩니다. 트랜잭션을 논리 서버 경계를 넘어서면 hello 참여 하는 서버는 먼저 toobe 상호 통신 관계에 입력 해야 합니다. Hello 통신 관계, 설정 되 면 모든 데이터베이스에 두 명의 서버 데이터베이스를 탄력적인 트랜잭션에 참가할 수 hello의 다른 서버를 hello 합니다. 트랜잭션과 두 개 이상의 논리 서버에 걸쳐 통신 관계 논리 서버의 쌍으로 된 위치에 toobe가 필요 합니다.

탄력적 데이터베이스 트랜잭션에 대 한 PowerShell cmdlet toomanage 통신 서버 간 관계를 따라 hello를 사용 합니다.

* **새 AzureRmSqlServerCommunicationLink**:이 cmdlet toocreate Azure SQL DB에는 두 논리 서버 간에 새 통신 관계를 사용 합니다. hello 관계는 대칭. 즉, 두 서버 hello 사용 하 여 트랜잭션을 다른 서버를 시작할 수 있습니다.
* **Get AzureRmSqlServerCommunicationLink**:이 cmdlet tooretrieve 기존 통신을 사용 하 여 관계 및 해당 속성입니다.
* **제거 AzureRmSqlServerCommunicationLink**:이 cmdlet tooremove 통신 하는 기존 관계를 사용 합니다. 

## <a name="monitoring-transaction-status"></a>트랜잭션 상태 모니터링
SQL DB toomonitor 상태 및 진행 중인 탄력적 데이터베이스 트랜잭션 진행 상황에서 동적 관리 뷰 (Dmv)를 사용 합니다. SQL DB에서 분산된 트랜잭션에 모든 Dmv 관련된 tootransactions 관련이 있습니다. Hello 해당 하는 목록 Dmv의 여기를 찾을 수 있습니다: [트랜잭션 관련 동적 관리 뷰 및 함수 (TRANSACT-SQL)](https://msdn.microsoft.com/library/ms178621.aspx)합니다.

다음 DMV는 특히 유용합니다.

* **sys.dm\_tran\_active\_transactions**: 현재 활성 트랜잭션과 그 상태를 나열합니다. hello UOW (작업 단위) 열 수 hello 다른 자식 트랜잭션을 식별 toohello 속해 있는 분산 트랜잭션을 동일 합니다. 같은 분산된 트랜잭션을 수행 하는 hello 내에서 모든 트랜잭션을 hello 같은 UOW 값입니다. Hello 참조 [DMV 설명서](https://msdn.microsoft.com/library/ms174302.aspx) 자세한 세부 정보에 대 한 합니다.
* **sys.dm\_tran\_데이터베이스\_트랜잭션을**: hello 로그의 hello 트랜잭션의 배치와 같은 트랜잭션에 대 한 추가 정보를 제공 합니다. Hello 참조 [DMV 설명서](https://msdn.microsoft.com/library/ms186957.aspx) 자세한 세부 정보에 대 한 합니다.
* **sys.dm\_tran\_잠금**: 진행 중인 트랜잭션이 현재 보유 하 고 있는 hello 잠금에 대 한 정보를 제공 합니다. Hello 참조 [DMV 설명서](https://msdn.microsoft.com/library/ms190345.aspx) 자세한 세부 정보에 대 한 합니다.

## <a name="limitations"></a>제한 사항
다음 제한 사항이 현재 hello tooelastic 데이터베이스 트랜잭션 SQL DB에 적용 됩니다.

* SQL DB의 데이터베이스 간 트랜잭션만 지원됩니다. 다른 [X/Open XA](https://en.wikipedia.org/wiki/X/Open_XA) 리소스 공급자 및 SQL DB 이외의 데이터베이스는 탄력적 데이터베이스 트랜잭션에 참여할 수 없습니다. 탄력적 데이터베이스 트랜잭션은 온-프레미스 SQL Server와 Azure SQL 데이터베이스 사이에서 확장될 수 없습니다. 온-프레미스 분산 트랜잭션의 경우 toouse MSDTC를 계속 합니다. 
* .NET 응용 프로그램의 클라이언트 조정 트랜잭션만 지원됩니다. BEGIN DISTRIBUTED TRANSACTION 같은 T-SQL에 대한 서버 쪽 지원이 계획되어 있지만 아직 제공되지 않습니다. 
* WCF 서비스에서 트랜잭션은 지원되지 않습니다. 예를 들어 트랜잭션을 실행하는 WCF 서비스 메서드가 있습니다. 트랜잭션 범위 내에서 hello 호출로 실패 합니다는 [System.ServiceModel.ProtocolException](https://msdn.microsoft.com/library/system.servicemodel.protocolexception)합니다.

## <a name="next-steps"></a>다음 단계
질문에 게 연락 하세요 hello에 toous [SQL 데이터베이스 포럼](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) 기능 요청에 대 한 하십시오 추가할 toohello [SQL 데이터베이스 피드백 포럼](https://feedback.azure.com/forums/217321-sql-database/)합니다.

<!--Image references-->
[1]: ./media/sql-database-elastic-transactions-overview/distributed-transactions.png



