---
title: "Entity Framework와 함께 aaaUsing 탄력적 데이터베이스 클라이언트 라이브러리 | Microsoft Docs"
description: "데이터베이스 코딩을 위해 탄력적 데이터베이스 클라이언트 라이브러리 및 Entity Framework 사용"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: b9c3065b-cb92-41be-aa7f-deba23e7e159
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: torsteng
ms.openlocfilehash: 917f6d28d9855c0b42afe2c008613a9bbb3ec6b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-client-library-with-entity-framework"></a>엔터티 프레임 작업과 함께 탄력적 데이터베이스 클라이언트 라이브러리
이 문서에서는 필요한 toointegrate hello로는 Entity Framework 응용 프로그램에서 hello 변경을 보여 줍니다. [탄력적 데이터베이스 도구](sql-database-elastic-scale-introduction.md)합니다. 작성에 포커스가 hello [분할 맵 관리](sql-database-elastic-scale-shard-map-management.md) 및 [데이터 종속 라우팅](sql-database-elastic-scale-data-dependent-routing.md) hello Entity Framework로 **Code First** 접근 방식입니다. hello [Code First-새 데이터베이스를](http://msdn.microsoft.com/data/jj193542.aspx) EF에 대 한 자습서는이 문서 전체에서 예제로 사용 합니다. 이 문서와 함께 제공 되는 hello 샘플 코드의 일부인 탄력적 데이터베이스 도구 hello Visual Studio 코드 샘플에 있는 샘플을 설정 합니다.

## <a name="downloading-and-running-hello-sample-code"></a>다운로드 하 고 hello 샘플 코드를 실행 합니다.
이 문서에 대 한 toodownload hello 코드:

* Visual Studio 2012 이상이 필요합니다. 
* Hello 다운로드 [엔터티 프레임 워크 통합 샘플-Azure sql 탄력적 DB 도구](https://code.msdn.microsoft.com/windowsapps/Elastic-Scale-with-Azure-bae904ba) MSDN에서. 선택한 hello 샘플 tooa 위치를 압축을 풉니다.
* Visual Studio를 시작합니다. 
* Visual Studio에서 [파일] -> [프로젝트/솔루션 열기]를 선택합니다. 
* Hello에 **프로젝트 열기** 대화 상자에서 다운로드 한 toohello 샘플을 찾아서 선택 **EntityFrameworkCodeFirst.sln** tooopen hello 예제입니다. 

toorun hello 샘플 toocreate Azure SQL 데이터베이스에 3 개의 빈 데이터베이스가 필요합니다.

* 분할된 데이터베이스 맵 관리자 데이터베이스
* 분할 1 데이터베이스
* 분할 2 데이터베이스

이러한 데이터베이스를 만든 후 hello 자리 표시자를 입력 **Program.cs** 를 Azure SQL DB 서버 이름, hello 데이터베이스 이름 및 자격 증명 tooconnect toohello 데이터베이스. Visual Studio에서 hello 솔루션을 빌드하십시오. Visual Studio에서 hello 탄력적 데이터베이스 클라이언트 라이브러리, Entity Framework 및 일시적인 오류 hello 빌드 프로세스의 일부로 처리에 대 한 hello 필요한 NuGet 패키지를 다운로드 합니다. 사용 중인 솔루션에 대해 NuGet 패키지를 복원할 수 있는지 확인합니다. Hello Visual Studio 솔루션 탐색기에서에서 hello 솔루션 파일을 마우스 오른쪽 단추로 클릭 하 여이 설정을 사용할 수 있습니다. 

## <a name="entity-framework-workflows"></a>Entity Framework 워크플로
Entity Framework 개발자가 hello 네 개의 워크플로 toobuild 응용 프로그램 및 응용 프로그램 개체에 대 한 tooensure 지 속성을 다음 중 하나에 의존 합니다. 

* **Code First (새 데이터베이스)**: hello EF 개발자 hello 모델 hello 응용 프로그램 코드에서 만들고 EF hello 데이터베이스를 생성 합니다. 
* **Code First (기존 데이터베이스)**: hello developer 기존 데이터베이스에서 hello 모델에 대 한 hello 응용 프로그램 코드를 생성 하는 EF를 사용 합니다.
* **첫 번째 모델**: hello 개발자 hello 모델 hello EF 디자이너에서 만들고 다음 EF hello 모델에서 hello 데이터베이스를 만듭니다.
* **첫 번째 데이터베이스**: hello 개발자 EF 기존 데이터베이스에서 tooinfer hello 모델 도구를 사용 합니다. 

이러한 접근 방식은 hello DbContext 클래스 tootransparently에 의존 하는 모든 데이터베이스 연결 및 응용 프로그램에 대 한 데이터베이스 스키마를 관리 합니다. 다음과 같은 작용이 hello 문서의 뒷부분에 보다 자세히 hello DbContext 기본 클래스에 대 한 다른 생성자에 대 한 서로 다른 수준의 연결 생성에 대 한 제어를 허용 하는 대로 데이터베이스 부트스트래핑 및 스키마 작성 합니다. 문제가는 hello 탄력적 데이터베이스 클라이언트 라이브러리에서 EF에서 제공 하는 hello 데이터베이스 연결 관리 hello 데이터 종속 라우팅 제공 하는 인터페이스의 연결 관리 기능을 hello와 교차 하는 hello 사실에서 주로 발생 합니다. 

## <a name="elastic-database-tools-assumptions"></a>탄력적 데이터베이스 도구 가정
용어 정의는 [탄력적 데이터베이스 도구 용어집](sql-database-elastic-scale-glossary.md)을 참조하세요.

탄력적 데이터베이스 클라이언트 라이브러리를 사용하여 shardlet이라고 하는 응용 프로그램 데이터의 파티션을 정의합니다. Shardlet 분할 키로 식별 되며 매핑된 toospecific 데이터베이스. 응용 프로그램 필요에 따라 많은 데이터베이스가 있고 충분 한 용량이 나 현재 비즈니스 요구 사항을 지정 하는 성능 hello shardlet tooprovide를 배포할 수 있습니다. 분할 키 값 toohello 데이터베이스의 hello 매핑 hello 탄력적 데이터베이스 클라이언트 Api에서 제공 되는 분할 맵을로 저장 됩니다. 이 기능을 **분할된 데이터베이스 맵 관리**또는 줄여서 SMM이라고 합니다. 분할 키를 전송 하는 요청에 대 한 데이터베이스 연결의 hello 브로커로 hello 분할 맵은 사용 됩니다. 여기서 스 toothis 기능 **데이터 종속 라우팅**합니다. 

hello shard map manager shardlet 동시 관리 작업 (예: 하나의 분할 tooanother에서 데이터를 재배치) 수행 중인 경우 발생할 수 있는 shardlet 데이터에 일관성이 없는 뷰에서 사용자가 보호 합니다. 따라서 toodo hello 클라이언트 라이브러리 브로커 hello 데이터베이스에 대 한 연결 응용 프로그램에서 관리 하는 분할 영역 맵의 hello 합니다. 따라서 hello 분할 맵 기능 tooautomatically kill 데이터베이스 연결 때 분할 관리 작업에 대해 작성 된 hello 연결 hello shardlet 영향을 줄 수 있습니다. 이 방법은 데이터베이스 존재에 대 한 기존는 하나의 toocheck에서 새 연결을 만드는 등의 EF의 기능 중 일부가 toointegrate가 필요 합니다. 일반적으로 관찰 되었습니다 hello 표준 DbContext 생성자만 작동 하는지 안정적으로 안전 하 게 복제할 수 있는 닫힌된 데이터베이스 연결에 대 한 EF 작업에 대 한 합니다. 탄력적 데이터베이스의 hello 디자인 원칙은 대신 tooonly broker 열린 연결입니다. Toohello EF DbContext를 전달 하기 전에 hello 클라이언트 라이브러리에서 조정 된 연결을 닫는 중이 문제를 해결할 수 있습니다 하 고 생각 합니다. 그러나 하 여 hello 연결을 닫는 EF toore 열 신뢰를 hello 라이브러리 수행 hello 유효성 검사 및 일관성 검사를 foregoes 하나입니다. 그러나 hello 마이그레이션 기능, EF에서 사용 하는 데이터베이스 스키마는 투명 toohello 응용 프로그램 방식으로 이러한 연결 toomanage hello를 사용 합니다. 이상적으로 우리 tooretain 선택한 hello에서 hello 탄력적 데이터베이스 클라이언트 라이브러리와 EF에서 이러한 모든 기능을 결합 같은 응용 프로그램입니다. hello 다음 섹션에서는 이러한 속성 및 요구 사항을 자세히 합니다. 

## <a name="requirements"></a>요구 사항
Hello 탄력적 데이터베이스 클라이언트 라이브러리와 엔터티 프레임 워크 Api를 사용할 때 다음과 같은 속성 tooretain hello를 하겠습니다. 

* **확장**: hello 분할 응용 프로그램의 용량 요구 hello에 대 한 필요에 따라 hello 응용 프로그램의 hello 데이터 계층에서 데이터베이스 tooadd 또는 제거 합니다. 즉, 데이터베이스 및 hello 탄력적 데이터베이스 shard map manager Api toomanage 데이터베이스 및 shardlet의 매핑을 사용 하 여의 hello hello 생성 및 삭제에 대 한 제어 합니다. 
* **일관성**: hello 응용 프로그램에서는 분할을 사용 하 고 사용 하 여 hello hello 클라이언트 라이브러리의 데이터 종속 라우팅 기능입니다. 연결을 통해 조정 된 tooavoid 손상 또는 잘못 된 쿼리 결과 hello shard map manager. 또한 유효성 검사 및 일관성도 유지됩니다.
* **Code First**: EF의 코드에 대 한 첫 번째 패러다임 tooretain hello 편리 합니다. Hello 응용 프로그램의 클래스를 투명 하 게 매핑된에서 Code First toohello 기본 데이터베이스 구조입니다. hello 응용 프로그램 코드를 기본 데이터베이스를 처리 하는 hello에 관련 된 대부분의 측면을 마스킹할 DbSets 상호 작용 합니다.
* **Schema**: Entity Framework는 초기 데이터베이스 스키마 생성과 마이그레이션을 통한 후속 스키마 전개를 처리합니다. 이러한 기능을 유지 하 여 앱을 위해 조정은 hello 데이터 진화 함에 따라 것 만큼 쉽지 합니다. 

hello 다음과 같은 지침 지시 어떻게 toosatisfy 탄력적 데이터베이스 도구를 사용 하 여 코드 첫 번째 응용 프로그램에 대 한 이러한 요구 사항입니다. 

## <a name="data-dependent-routing-using-ef-dbcontext"></a>EF DbContext를 사용하는 데이터 종속 라우팅
Entity Framework를 사용하는 데이터베이스 연결은 대개 **DbContext**의 서브클래스를 통해 관리합니다. 이러한 서브클래스는 **DbContext**에서 파생시키는 방식으로 만듭니다. 이 정의 하는 프로그램 **DbSets** 응용 프로그램에 대 한 CLR 개체의 hello 데이터베이스 기반 컬렉션을 구현 하는 합니다. 데이터 종속 라우팅의 hello 컨텍스트에서 다른 EF 코드 첫 번째 응용 프로그램 시나리오에 포함 되지 않은 몇 가지 유용한 속성을 확인할 수 있습니다. 

* hello 데이터베이스 이미 있으며이 hello 탄력적 데이터베이스 분할 맵을 등록 합니다. 
* hello 응용 프로그램의 hello 스키마 이미 배포 된 toohello 데이터베이스 아래에서 설명 되었습니다. 
* 데이터 종속 라우팅 연결 toohello 데이터베이스 hello 분할 맵을 여 조정 된 합니다. 

toointegrate **DbContexts** 데이터 종속 라우팅 확장에:

1. Hello shard map manager의 hello 탄력적 데이터베이스 클라이언트 인터페이스를 통해 실제 데이터베이스 연결 만들기 
2. Hello 연결 hello로 래핑할 **DbContext** 하위 클래스
3. Hello에 hello 연결 전달 **DbContext** 기본 클래스 tooensure 모든 hello 처리 hello EF 쪽에도 발생 합니다. 

다음 코드 예제는 hello이이 방법을 보여 줍니다. (이 코드는 또한 Visual Studio 프로젝트와 함께 제공 되는 hello)

    public class ElasticScaleContext<T> : DbContext
    {
    public DbSet<Blog> Blogs { get; set; }
    …

        // C'tor for data dependent routing. This call will open a validated connection 
        // routed toohello proper shard by hello shard map manager. 
        // Note that hello base class c'tor call will fail for an open connection
        // if migrations need toobe done and SQL credentials are used. This is hello reason for hello 
        // separation of c'tors into hello data-dependent routing case (this c'tor) and hello internal c'tor for new shards.
        public ElasticScaleContext(ShardMap shardMap, T shardingKey, string connectionStr)
            : base(CreateDDRConnection(shardMap, shardingKey, connectionStr), 
            true /* contextOwnsConnection */)
        {
        }

        // Only static methods are allowed in calls into base class c'tors.
        private static DbConnection CreateDDRConnection(
        ShardMap shardMap, 
        T shardingKey, 
        string connectionStr)
        {
            // No initialization
            Database.SetInitializer<ElasticScaleContext<T>>(null);

            // Ask shard map toobroker a validated connection for hello given key
            SqlConnection conn = shardMap.OpenConnectionForKey<T>
                                (shardingKey, connectionStr, ConnectionOptions.Validate);
            return conn;
        }    

## <a name="main-points"></a>요점
* 새로운 생성자 hello DbContext 하위 클래스에 기본 생성자가 hello를 대체합니다. 
* hello 새로운 생성자는 탄력적 데이터베이스 클라이언트 라이브러리를 통해 데이터 종속 라우팅에 필요한 hello 인수, 즉
  
  * hello shard map tooaccess hello 데이터 종속 라우팅 인터페이스
  * hello 분할 키 tooidentify hello shardlet
  * hello 데이터 종속 라우팅 연결 toohello 분할에 대 한 hello 자격 증명으로 연결 문자열입니다. 
* hello 호출 toohello 기본 클래스 생성자는 우회를 모든 hello 단계를 수행 하는 정적 메서드가 데이터 종속 라우팅에 대 한 필요 합니다. 
  
  * Hello shard map tooestablish 열려 있는 연결에서 hello OpenConnectionForKey 호출 hello 탄력적 데이터베이스 클라이언트 인터페이스를 사용합니다.
  * hello 분할 맵은 분할 키를 제공 하는 hello에 대 한 hello shardlet을 보유 하는 hello 열린 연결 toohello 분할 영역을 만듭니다.
  * 이 열린 연결의이 연결이 새 연결을 자동으로 만들 EF 하도록 하는 대신 EF에서 사용 하는 toobe DbContext tooindicate 백 toohello 기본 클래스 생성자에 전달 됩니다. 이 방식으로 hello 연결 hello 탄력적 데이터베이스 클라이언트 API에서 표시 된 분할 맵 관리 작업에서 일관성을 보장할 수 있도록 합니다.

코드에서 hello 기본 생성자 대신 DbContext 서브 클래스에 대 한 hello 새 생성자를 사용 합니다. 다음은 예제입니다. 

    // Create and save a new blog.

    Console.Write("Enter a name for a new blog: "); 
    var name = Console.ReadLine(); 

    using (var db = new ElasticScaleContext<int>( 
                            sharding.ShardMap,  
                            tenantId1,  
                            connStrBldr.ConnectionString)) 
    { 
        var blog = new Blog { Name = name }; 
        db.Blogs.Add(blog); 
        db.SaveChanges(); 

        // Display all Blogs for tenant 1 
        var query = from b in db.Blogs 
                    orderby b.Name 
                    select b; 
     … 
    }

hello 새로운 생성자의 hello 값으로 식별 된 hello shardlet에 대 한 hello 데이터를 보유 하는 hello 연결 toohello 분할 열립니다 **tenantid1**합니다. hello에 대 한 코드 hello **를 사용 하 여** 블록 유지 변경 되지 않은 tooaccess hello **DbSet** 블로그에 EF를 사용 하 여 hello에 대 한 분할 된 데이터베이스에 대 한 **tenantid1**합니다. 모든 데이터베이스 작업은 이제 되도록 블록을 사용 하 여 hello의 hello 코드 범위 toohello 하나의 분할 영역에 대 한 의미 체계가 변경 여기서 **tenantid1** 유지 됩니다. 예를 들어, LINQ 쿼리를 통해 hello 블로그 **DbSet** hello 현재 분할 영역에 저장 된 블로그 반환 하는 다른 분할 된 데이터베이스에 저장 하는 스토리를 hello 하지 합니다.  

#### <a name="transient-faults-handling"></a>일시적인 오류 처리
hello Microsoft Patterns & Practices 팀 게시 된 hello [hello 일시적인 오류 처리 응용 프로그램 블록](https://msdn.microsoft.com/library/dn440719.aspx)합니다. hello 라이브러리 EF 함께에서 탄력적인 크기 조정 클라이언트 라이브러리와 함께 사용 됩니다. 그러나 모든 일시적인 예외 tooa 위치 하는 새 연결 시도가 조정 우리는 hello 생성자를 사용 하 여 일시적인 오류 이후 hello 새 생성자를 사용 중인 될를 확인할 수 있습니다를 반환 하는지 확인 합니다. 그렇지 않은 경우 올바른 분할 보장 되지 않습니다 되며 보증이 없는 hello 연결 하는 연결 toohello toohello 분할 맵은 발생 하는 변경 내용으로 유지 됩니다. 

hello 다음 코드 예제에서는 SQL 재시도 정책을 사용할 수 있는 방법을 hello 주위 새 **DbContext** 하위 클래스의 생성자: 

    SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
    { 
        using (var db = new ElasticScaleContext<int>( 
                                sharding.ShardMap,  
                                tenantId1,  
                                connStrBldr.ConnectionString)) 
            { 
                    var blog = new Blog { Name = name }; 
                    db.Blogs.Add(blog); 
                    db.SaveChanges(); 
            … 
            } 
        }); 

**SqlDatabaseUtils.SqlRetryPolicy** 로 정의 된 hello 위의 코드는 **SqlDatabaseTransientErrorDetectionStrategy** 10 및 5 초 동안 다시 시도 횟수를 시도 간 대기 시간입니다. 이 방법은 EF 및 사용자가 시작한 트랜잭션을 비슷한 toohello 지침 (참조 [실행을 다시 시도 전략 (EF6부터)의 제한 사항](http://msdn.microsoft.com/data/dn307226)합니다. 두 경우 모두 해당 hello 응용 프로그램 제어 hello 범위 toowhich hello 일시적인 예외가 반환 필요: tooeither hello 트랜잭션을 닫았다가 다시 열거나 (같이) hello hello 탄력적 데이터베이스를 사용 하는 적절 한 생성자에서 hello 컨텍스트를 다시 만듭니다. 클라이언트 라이브러리입니다.

hello 여기서 일시적인 예외 살펴보실 범위에 다시 필요 toocontrol도 불가능 hello를 사용 하 여 hello 기본 제공 **SqlAzureExecutionStrategy** EF와 함께 제공 되 합니다. **SqlAzureExecutionStrategy** 연결을 다시 하지만 사용 하지는 **OpenConnectionForKey** 따라서 hello의 일환으로 수행 된 모든 hello 유효성 검사를 건너뛰는 **OpenConnectionForKey** 호출 합니다. Hello 코드 예제에서는 기본 제공 hello를 사용 하는 대신, **DefaultExecutionStrategy** 도 있는 EF 함께 제공 합니다. 너무 것이 아니라**SqlAzureExecutionStrategy**, hello 재시도 정책을 통해 일시적인 오류 처리와 함께에서 올바르게 작동 합니다. hello에 hello 실행 정책이 설정 되었는지 **ElasticScaleDbConfiguration** 클래스입니다. 참고 하지 toouse 하기로 **DefaultSqlExecutionStrategy** toouse 하도록 제안 하는 이후 **SqlAzureExecutionStrategy** 설명 했 듯이 toowrong 동작 일시적 예외가 발생-될 것입니다. Hello 다시 시도 정책 및 EF에 대 한 자세한 내용은 참조 하십시오. [EF에서 연결 복원](http://msdn.microsoft.com/data/dn456835.aspx)합니다.     

#### <a name="constructor-rewrites"></a>생성자 다시 작성
hello 위의 보여 주는 코드 예제 hello 기본 생성자는 주문 toouse 데이터 종속 라우팅 hello Entity Framework로 응용 프로그램에 필요한 다시 작성 합니다. 다음 표에 hello이 접근 방식을 tooother 생성자를 일반화 합니다. 

| 현재 생성자 | 데이터에 맞게 다시 작성된 생성자 | 기본 생성자 | 참고 |
| --- | --- | --- | --- |
| MyContext() |ElasticScaleContext(ShardMap, TKey) |DbContext(DbConnection, bool) |hello 연결 toobe hello 분할 맵은 hello 데이터 종속 라우팅 키의 기능을 필요합니다. 대신 hello 분할 맵 toobroker hello 연결을 사용 하 여 및 EF 별로 tooby 패스 자동 연결 생성 해야 합니다. |
| MyContext(string) |ElasticScaleContext(ShardMap, TKey) |DbContext(DbConnection, bool) |hello 연결이 함수 hello 분할 맵 및 hello 데이터 종속 라우팅 키입니다. 고정된 데이터베이스 이름 또는 연결 문자열은으로 작동 하지 것입니다 hello 분할 맵 유효성 검사 무시 합니다. |
| MyContext(DbCompiledModel) |ElasticScaleContext(ShardMap, TKey, DbCompiledModel) |DbContext(DbConnection, DbCompiledModel, bool) |hello 연결 분할 맵 및 분할 키를 제공 하는 hello 모델 개념을 제공 하는 hello에 대해 작성 됩니다. hello 컴파일된 모델 toohello 기본 c'tor에 전달 됩니다. |
| MyContext(DbConnection, bool) |ElasticScaleContext(ShardMap, TKey, bool) |DbContext(DbConnection, bool) |hello 연결 hello 분할 맵 및 hello 키에서 유추 toobe가 필요 합니다. 것 (사용 하지 않는 경우 해당 입력 된 이미 hello 분할 맵 및 hello 키)을 입력으로 제공할 수 없습니다. 부울 hello 전달 됩니다. |
| MyContext(string, DbCompiledModel) |ElasticScaleContext(ShardMap, TKey, DbCompiledModel) |DbContext(DbConnection, DbCompiledModel, bool) |hello 연결 hello 분할 맵 및 hello 키에서 유추 toobe가 필요 합니다. 것 (사용 하지 않는 경우 해당 입력 된 hello 분할 맵 및 hello 키)을 입력으로 제공할 수 없습니다. hello 컴파일된 모델 전달 됩니다. |
| MyContext(ObjectContext, bool) |ElasticScaleContext(ShardMap, TKey, ObjectContext, bool) |DbContext(ObjectContext, bool) |새로운 생성자 hello ObjectContext 입력으로 전달 하는 hello에서 모든 연결을 탄력적인 크기 조정에서 관리 하는 다시 경로 tooa 연결 tooensure가 필요 합니다. ObjectContexts에 대 한 자세한 내용은이 문서의 hello 범위를 벗어납니다. |
| MyContext(DbConnection, DbCompiledModel,bool) |ElasticScaleContext(ShardMap, TKey, DbCompiledModel, bool) |DbContext(DbConnection, DbCompiledModel, bool); |hello 연결 hello 분할 맵 및 hello 키에서 유추 toobe가 필요 합니다. hello 연결 (사용 하지 않는 경우 해당 입력 된 이미 hello 분할 맵 및 hello 키)을 입력으로 제공할 수 없습니다. 모델 및 Boolean toohello 기본 클래스 생성자에 전달 됩니다. |

## <a name="shard-schema-deployment-through-ef-migrations"></a>EF 마이그레이션을 통해 분할된 데이터베이스 스키마 배포
자동 스키마 관리는 편의 위해 hello Entity Framework에서 제공 합니다. 탄력적 데이터베이스 도구를 사용 하 여 응용 프로그램의 hello 컨텍스트에서 원하는 tooretain이 기능 tooautomatically 프로 비전 hello 스키마 toonewly 만든 분할 된 데이터베이스는 toohello 분할 응용 프로그램을 추가 하는 경우. hello 기본 사용 사례에는 분할 응용 프로그램의 EF를 사용 하 여 hello 데이터 계층에서 tooincrease 용량입니다. 스키마 관리에 대 한 EF의 기능에 의존 hello 데이터베이스 관리 작업 EF 기반으로 분할 응용 프로그램으로 줄일 수 있습니다. 

EF 마이그레이션을 통한 스키마 배포는 **열려 있지 않은 연결**에서 가장 효율적으로 작동합니다. 반대로 hello 탄력적 데이터베이스 클라이언트 API에서 제공 하는 hello 열린 연결을 사용 하는 데이터 종속 라우팅에 대 한 toohello 시나리오입니다. 또 다른 차이점은 hello 일관성 요구 사항: 동시 분할 맵 조작에 대 한 모든 데이터 종속 라우팅 연결 tooprotect에 바람직한 tooensure 일관성을 하는 동안 아니므로 처음 스키마 배포 tooa 새 데이터베이스는 중요 한 문제 이 있고 hello 분할 맵을에 등록 되어이 아직 할당 toohold shardlet이 아직 있습니다. 따라서 것과 반대로 toodata 종속 라우팅으로이 시나리오에 대 한 일반 데이터베이스 연결에 의존 수 있습니다.  

여기서 EF 마이그레이션을 통해 스키마 배포는 밀접 하 게 hello 등록 hello 새 데이터베이스의 분할 맵 hello 응용 프로그램의에서 한 조각으로 tooan 접근 방식을 안내 합니다. 이 필수 구성 요소를 다음 hello에 의존 합니다. 

* hello 데이터베이스를 이미 생성 되었습니다. 
* hello 데이터베이스가 비어-사용자 스키마와 사용자 데이터를 보유 합니다.
* 아직 hello 데이터베이스 데이터 종속 라우팅에 대 한 hello 탄력적 데이터베이스 클라이언트 Api 통해 액세스할 수 없습니다. 

위치에서 이러한 필수 구성이 요소는 일반을 만들 수 있습니다 되지 않은 열린 **SqlConnection** tookick 스키마 배포에 대 한 EF 마이그레이션 해제 합니다. 아래의 코드 예제는 hello이이 방법을 보여 줍니다. 

        // Enter a new shard - i.e. an empty database - toohello shard map, allocate a first tenant tooit  
        // and kick off EF intialization of hello database toodeploy schema 

        public void RegisterNewShard(string server, string database, string connStr, int key) 
        { 

            Shard shard = this.ShardMap.CreateShard(new ShardLocation(server, database)); 

            SqlConnectionStringBuilder connStrBldr = new SqlConnectionStringBuilder(connStr); 
            connStrBldr.DataSource = server; 
            connStrBldr.InitialCatalog = database; 

            // Go into a DbContext tootrigger migrations and schema deployment for hello new shard. 
            // This requires an un-opened connection. 
            using (var db = new ElasticScaleContext<int>(connStrBldr.ConnectionString)) 
            { 
                // Run a query tooengage EF migrations 
                (from b in db.Blogs 
                    select b).Count(); 
            } 

            // Register hello mapping of hello tenant toohello shard in hello shard map. 
            // After this step, data-dependent routing on hello shard map can be used 

            this.ShardMap.CreatePointMapping(key, shard); 
        } 


이 샘플은 hello 메서드 **RegisterNewShard** EF 마이그레이션을 통해 hello 스키마가 배포 레지스터 hello hello shard map의 분할 된 데이터베이스는 분할 키 toohello 분할의 매핑을 저장 합니다. Hello의 생성자에 의존 **DbContext** 하위 클래스 (**ElasticScaleContext** hello 샘플에) SQL 연결 문자열을 입력으로 사용 합니다. 이 생성자의 hello 코드에는 다음 예제와 hello로 간단한 것입니다. 

        // C'tor toodeploy schema and migrations tooa new shard 
        protected internal ElasticScaleContext(string connectionString) 
            : base(SetInitializerForConnection(connectionString)) 
        { 
        } 

        // Only static methods are allowed in calls into base class c'tors 
        private static string SetInitializerForConnection(string connnectionString) 
        { 
            // We want existence checks so that hello schema can get deployed 
            Database.SetInitializer<ElasticScaleContext<T>>( 
        new CreateDatabaseIfNotExists<ElasticScaleContext<T>>()); 

            return connnectionString; 
        } 

Hello 기본 클래스에서 상속 하는 hello 생성자의 hello 버전을 사용 하나 있습니다. 그러나 EF에 대 한 기본 이니셜라이저 hello hello 코드 요구 tooensure 연결할 때 사용 됩니다. 따라서 hello 연결 문자열과 함께 hello 기본 클래스 생성자를 호출 하기 전에 hello 정적 메서드로 짧은 우회를 hello 합니다. Note hello 등록 분할 된 데이터베이스의 EF에 대 한 hello 이니셜라이저 설정을 충돌 하지 않는 다른 응용 프로그램 도메인 또는 프로세스 tooensure에서 실행 해야 합니다. 

## <a name="limitations"></a>제한 사항
이 문서에 설명 된 hello 접근 방식에 몇 가지 제한 필요 합니다. 

* 사용 하는 EF 응용 프로그램 **LocalDb** 탄력적 데이터베이스 클라이언트 라이브러리를 사용 하기 전에 먼저 toomigrate tooa 일반 SQL Server 데이터베이스를 해야 합니다. **LocalDb**의 경우 탄력적인 확장을 사용하는 분할된 데이터베이스를 통해 응용 프로그램의 규모를 확장할 수 없습니다. 개발에서는 **LocalDb**를 계속 사용할 수 있습니다. 
* 데이터베이스 스키마 변경을 내재 된 모든 변경 내용을 toohello 응용 프로그램을 모든 분할 영역에 EF 마이그레이션을 통해 toogo가 필요 합니다. 이 문서에 대 한 hello 샘플 코드를 보여 주지 않습니다 방법을 toodo이 있습니다. 모든 분할 영역; 통해 ConnectionString 매개 변수 tooiterate 데이터베이스 업데이트 사용 하는 것이 좋습니다. 또는 추출 hello T-SQL 스크립트와 데이터베이스 업데이트를 사용 하 여 마이그레이션 보류 중인 hello에 대 한 hello-위에 스크립트 옵션이 고 hello T-SQL 스크립트 tooyour 분할 영역을 적용 합니다.  
* 요청에 지정 된 경우 해당 데이터베이스 처리의 모든 포함 되도록 단일 분할 영역 내에서 hello 요청에서 제공 하는 hello 분할 키로 식별 한 대로 간주 됩니다. 그러나 이 가정이 항상 참인 것은 아닙니다. 예를 들어 때 가능한 toomake 분할 키를 사용할 수 있습니다. tooaddress이 hello이, 클라이언트 라이브러리는 hello **MultiShardQuery** 여러 분할 된 데이터베이스를 쿼리 하기 위한 연결 추상화를 구현 하는 클래스입니다. Toouse hello 학습 **MultiShardQuery** EF와 함께에서이 문서의 hello 다루지 않습니다.

## <a name="conclusion"></a>결론
이 문서에 설명 된 hello 단계를 통해 EF 응용 프로그램 수 hello 탄력적 데이터베이스 클라이언트 라이브러리의 기능에 사용할 데이터 종속 라우팅 리팩터링 hello의 생성자에서 **DbContext** hello EF에에서 사용 되는 하위 클래스 응용 프로그램입니다. 이 제한을 hello 변경할 필요가 toothose 위치 **DbContext** 클래스가 이미 존재 합니다. 또한 EF 응용 프로그램 hello 필요한 EF hello 등록의 마이그레이션 새 분할 영역 및 hello 분할 맵의 매핑을 호출 하는 hello 단계를 결합 하 여 자동 스키마 배포에서 toobenefit을 계속 수 있습니다. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-use-entity-framework-applications-visual-studio/sample.png
