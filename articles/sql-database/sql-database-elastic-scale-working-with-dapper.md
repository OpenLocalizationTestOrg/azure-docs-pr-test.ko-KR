---
title: "Dapper와 aaaUsing 탄력적 데이터베이스 클라이언트 라이브러리 | Microsoft Docs"
description: "Dapper과 함께 탄력적 데이터베이스 클라이언트 라이브러리 사용"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 463d2676-3b19-47c2-83df-f8c50492c9d2
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: c22ece2a977265e93850f0ad3f3ca48f0a8733ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-elastic-database-client-library-with-dapper"></a>Dapper과 함께 탄력적 데이터베이스 클라이언트 라이브러리 사용
이 문서는 Dapper toobuild 응용 프로그램에 의존 하지만 tooembrace을 할 수도 있는 개발자를 위한 [탄력적 데이터베이스 도구](sql-database-elastic-scale-introduction.md) 데이터 계층 분할 tooscale 아웃을 구현 하는 toocreate 응용 프로그램입니다.  이 문서는 탄력적 데이터베이스 도구와 함께 필요한 toointegrate Dapper 기반 응용 프로그램의 hello 변경 내용을 보여 줍니다. Hello 탄력적 데이터베이스 분할 관리 및 데이터에 종속 된 구성에 집중은 Dapper와 라우팅입니다. 

**샘플 코드**: [Azure SQL 데이터베이스-Dapper 통합에 대한 탄력적 데이터베이스 도구](https://code.msdn.microsoft.com/Elastic-Scale-with-Azure-e19fc77f).

통합 **Dapper** 및 **DapperExtensions** hello로 Azure SQL 데이터베이스 탄력적 데이터베이스 클라이언트 라이브러리 쉽습니다. 응용 프로그램 데이터 종속 라우팅 hello 만들기를 변경 하 고 새로운를 열 여 צ ְ ײ [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) 개체 toouse hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) hello에서 호출 [클라이언트 라이브러리](http://msdn.microsoft.com/library/azure/dn765902.aspx)합니다. 새 연결이 만들어지고 열려 있는 프로그램 응용 프로그램 tooonly의 변경 내용을 제한 합니다. 

## <a name="dapper-overview"></a>Dapper 개요
**Dapper** 는 개체 관계형 매퍼입니다. .NET 개체 응용 프로그램 tooa 관계형 데이터베이스에서 (또는 그 반대로) 매핑됩니다. hello 예제 코드의 첫 번째 부분 hello Dapper 기반 응용 프로그램과 함께 hello 탄력적 데이터베이스 클라이언트 라이브러리를 통합 하는 방법을 보여 줍니다. hello hello 예제 코드의 두 번째 부분에서는 어떻게 toointegrate Dapper와 DapperExtensions 둘 다 사용 하는 경우.  

Dapper hello 매퍼 기능은 제출 하는 중 T-SQL 문을 실행 하거나 hello 데이터베이스 쿼리를 단순화 하는 데이터베이스 연결에 확장 메서드를 제공 합니다. 예를 들어, Dapper를 사용 하면.NET 개체 및에 대 한 SQL 문의 hello 매개 변수 간의 쉽게 toomap **Execute** 호출 또는 SQL 쿼리를 사용 하 여.NET 개체로 tooconsume hello 결과 **쿼리**Dapper에서 호출 합니다. 

DapperExtensions을 사용할 경우 tooprovide hello SQL 문을 더 이상 필요 합니다. 와 같은 확장 메서드 **GetList** 또는 **삽입** hello 데이터베이스 연결을 통해 hello SQL 문을 만드는 hello 내부적입니다.

Dapper와 DapperExtensions 또 다른 이점은 응용 프로그램 컨트롤의 hello hello hello 데이터베이스 연결 만들기는 것입니다. 이렇게 하면 브로커 데이터베이스 shardlet toodatabases의 hello 매핑을 기반으로 연결 하는 hello 탄력적 데이터베이스 클라이언트 라이브러리와 상호 작용할 수 있습니다.

tooget hello Dapper 어셈블리 참조 [net Dapper 점](http://www.nuget.org/packages/Dapper/)합니다. Hello Dapper 확장에 대 한 참조 [DapperExtensions](http://www.nuget.org/packages/DapperExtensions)합니다.

## <a name="a-quick-look-at-hello-elastic-database-client-library"></a>Hello 탄력적 데이터베이스 클라이언트 라이브러리 개요
Hello 탄력적 데이터베이스 클라이언트 라이브러리를 사용 하면 호출 응용 프로그램 데이터의 파티션을 정의할 *shardlet* 매핑하십시오 toodatabases, 및 식별 하 여 *분할 키*합니다. 데이터베이스는 필요한 수만큼 포함할 수 있으며 이러한 데이터베이스에 대해 shardlet을 배포할 수 있습니다. 분할 키 값 toohello 데이터베이스의 hello 매핑 hello 라이브러리의 Api에서 제공 하는 분할 맵을로 저장 됩니다. 이 기능을 **분할된 데이터베이스 맵 관리**라고 합니다. 분할 키를 전송 하는 요청에 대 한 데이터베이스 연결의 hello 브로커로 hello 분할 맵은 사용 됩니다. 이 기능은 참조 tooas **데이터 종속 라우팅**합니다.

![분할된 데이터베이스 맵과 데이터 종속 라우팅][1]

hello shard map manager hello 데이터베이스에서 shardlet 동시 관리 작업 중인 경우 발생할 수 있는 shardlet 데이터에 일관성이 없는 뷰에서 사용자가 보호 합니다. 따라서 toodo hello 라이브러리를 사용 하 여 빌드한 응용 프로그램에 대 한 분할 맵을 브로커 hello 데이터베이스 연결을 hello 합니다. 분할 관리 작업 hello shardlet에 영향을 줄 수, 하는 경우 이렇게 하면 hello 분할 맵 기능 tooautomatically kill 데이터베이스 연결 합니다. 

Toouse hello Dapper에 대 한 hello 전통적인 방법 toocreate 연결을 사용 하는 대신 필요 [OpenConnectionForKey 메서드](http://msdn.microsoft.com/library/azure/dn824099.aspx)합니다. 이렇게 하면 모든 hello 유효성 검사를 수행 하 고 분할 된 데이터베이스 간에 데이터를 이동할 때 연결을 올바르게 관리 합니다.

### <a name="requirements-for-dapper-integration"></a>Dapper 통합을 위한 요구 사항
Hello 탄력적 데이터베이스 클라이언트 라이브러리와 hello Dapper Api를 사용할 때는 다음과 같은 속성 tooretain hello 원하는:

* **확장**: tooadd 또는 hello 분할 응용 프로그램의 용량 요구 hello에 대 한 필요에 따라 hello 응용 프로그램의 hello 데이터 계층에서 데이터베이스를 제거 했습니다. 
* **일관성**: 응용 프로그램은 분할을 사용 하 여 확장할 이후 tooperform 데이터 종속 라우팅 필요 합니다. 따라서 toouse hello 데이터 종속 라우팅 기능을 hello 라이브러리 toodo 하려고합니다. 특히, 원하는 tooretain hello 유효성 검사 하 고 일관성 순서 tooavoid 손상이 나 잘못 된 쿼리 결과의 hello shard map 관리자를 통해 조정 된 연결에서 제공 되도록 합니다. 이렇게 하면 해당 연결 tooa shardlet을 지정 된 거부 또는 (예를 들어) hello shardlet은 분할/병합 Api를 사용 하 여 현재 이동된 tooa 다른 분할 하는 경우 중지 됩니다.
* **개체의 매핑**: Dapper tootranslate hello 응용 프로그램의 클래스 및 기본 데이터베이스 구조 hello 사이 제공 하는 hello 매핑의 tooretain hello 편의 주시기 바랍니다. 

hello 다음 섹션에서는 이러한 요구 사항 기반으로 하는 응용 프로그램에 대 한 지침 **Dapper** 및 **DapperExtensions**합니다.

## <a name="technical-guidance"></a>기술 지침
### <a name="data-dependent-routing-with-dapper"></a>Dapper를 사용한 데이터 종속 라우팅
Dapper와 hello 응용 프로그램은 일반적으로 만들고 hello 연결 toohello 기본 데이터베이스 열에 대 한 책임 지. T 형식이 hello 응용 프로그램에 제공한, Dapper 쿼리 결과 반환 화 Dapper 유형의.NET 컬렉션에서 화 유형의 hello T-SQL 결과 행 toohello 개체 hello 매핑을 수행 마찬가지로, Dapper SQL 값 또는 데이터 조작 언어 (DML) 문에 대 한 매개 변수를.NET 개체를 매핑합니다. 일반 hello에 대 한 확장 메서드를 통해이 기능을 제공 하는 Dapper [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) hello ADO.NET SQL 클라이언트 라이브러리에서 개체입니다. 탄력적인 확장 Api hello DDR이 반환한 SQL 연결 hello 일반도 있습니다. [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) 개체입니다. 이 통해 toodirectly 사용 Dapper 확장 hello 클라이언트 라이브러리의 DDR API에서 반환 하는 hello 형식에 대해 간단한 SQL 클라이언트 연결은도 있습니다.

이러한 결과이 따르면 Dapper에 대 한 hello 탄력적 데이터베이스 클라이언트 라이브러리에서 조정 된 간단한 toouse 연결을 만듭니다.

이 코드 예제 (샘플 약관과 hello)에 hello 응용 프로그램 toohello 라이브러리 toobroker hello 연결 toohello 오른쪽 분할 hello 분할 키가 제공한 hello 방법을 보여 줍니다.   

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                     key: tenantId1, 
                     connectionString: connStrBldr.ConnectionString, 
                     options: ConnectionOptions.Validate))
    {
        var blog = new Blog { Name = name };
        sqlconn.Execute(@"
                      INSERT INTO
                            Blog (Name)
                            VALUES (@name)", new { name = blog.Name }
                        );
    }

hello 호출 toohello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) API hello 기본 만들기 및 SQL 클라이언트 연결 열기를 대체 합니다. hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) 호출 데이터 종속 라우팅에 필요한 hello 인수를 사용 합니다. 

* hello shard map tooaccess hello 데이터 종속 라우팅 인터페이스
* hello 분할 키 tooidentify hello shardlet
* hello 자격 증명 (사용자 이름 및 암호) tooconnect toohello 분할

hello shard map 개체 분할 키를 제공 하는 hello에 대 한 hello shardlet을 보유 하는 연결 toohello 분할 영역을 만듭니다. hello 탄력적 데이터베이스 클라이언트 Api에는 또한 일관성을 보장 하는 hello 연결 tooimplement을 태그입니다. Hello 이후 호출을 통해서도[OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) 일반 SQL 클라이언트 연결 개체를 후속 호출 toohello hello 반환 **Execute** Dapper 다음과에서 확장 메서드는 표준 Dapper hello 연습 합니다.

쿼리 작업 거의 동일한 hello 방법-처음 열면 사용 하 여 hello 연결 [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) hello 클라이언트 API에서에서 합니다. 다음 SQL 쿼리 hello 정규 Dapper 확장 메서드 toomap hello 결과 사용 하 여.NET 개체로:

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId1, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate ))
    {    
           // Display all Blogs for tenant 1
           IEnumerable<Blog> result = sqlconn.Query<Blog>(@"
                                SELECT * 
                                FROM Blog
                                ORDER BY Name");

           Console.WriteLine("All blogs for tenant id {0}:", tenantId1);
           foreach (var item in result)
           {
                Console.WriteLine(item.Name);
            }
    }

해당 hello 참고 **를 사용 하 여** hello DDR 연결 범위가 hello 블록 toohello 하나의 분할 tenantId1 보관할 내의 모든 데이터베이스 작업을 차단 합니다. hello 쿼리는 hello 현재 분할 하지만 다른 분할 영역에 저장 된 hello 하지에 저장 된 블로그만 반환 합니다. 

## <a name="data-dependent-routing-with-dapper-and-dapperextensions"></a>Dapper 및 DapperExtensions를 사용한 데이터 종속 라우팅
Dapper는 데이터베이스 응용 프로그램을 개발 하는 경우 추가 편 및 hello 데이터베이스에서 추상화를 제공할 수 있는 추가 확장 프로그램 에코 시스템 함께 제공 됩니다. 이러한 기능의 한 가지 예가 DapperExtensions입니다. 

응용 프로그램에서 DapperExtensions를 사용하더라도 데이터베이스 연결 작성 및 관리 방식은 변경되지 않습니다. Hello 응용 프로그램의 책임 tooopen 연결에는 여전히와 일반 SQL 클라이언트 연결 개체는 hello 확장명 메서드에 의해 합니다. Hello에 의존 수 [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) 위에서 설명한 대로 합니다. 다음 코드 예제 표시, hello로는 더 이상 것 toowrite hello T-SQL 문을으로 hello 변경 됩니다.

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId2, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate))
    {
           var blog = new Blog { Name = name2 };
           sqlconn.Insert(blog);
    }

및 다음은 hello 쿼리에 대 한 hello 코드 샘플: 

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId2, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate))
    {
           // Display all Blogs for tenant 2
           IEnumerable<Blog> result = sqlconn.GetList<Blog>();
           Console.WriteLine("All blogs for tenant id {0}:", tenantId2);
           foreach (var item in result)
           {
               Console.WriteLine(item.Name);
           }
    }

### <a name="handling-transient-faults"></a>일시적인 오류 처리
hello Microsoft Patterns & Practices 팀 게시 된 hello [일시적인 오류 처리 응용 프로그램 블록](http://msdn.microsoft.com/library/hh680934.aspx) toohelp 응용 프로그램 개발자가 hello 클라우드에서 실행 하는 경우에 발생 한 일반적인 일시적인 오류 상황을 완화 합니다. 자세한 내용은 참조 [해냈다, 암호의 모든의 전리품이 야: hello 일시적인 오류 처리 응용 프로그램 블록을 사용 하 여](http://msdn.microsoft.com/library/dn440719.aspx)합니다.

hello 코드 예제는 hello 일시적인 오류 라이브러리 tooprotect 일시적 오류에 대해 사용합니다. 

    SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() =>
    {
       using (SqlConnection sqlconn = 
          shardingLayer.ShardMap.OpenConnectionForKey(tenantId2, connStrBldr.ConnectionString, ConnectionOptions.Validate))
          {
              var blog = new Blog { Name = name2 };
              sqlconn.Insert(blog);
          }
    });

**SqlDatabaseUtils.SqlRetryPolicy** 로 정의 된 hello 위의 코드는 **SqlDatabaseTransientErrorDetectionStrategy** 10 및 5 초 동안 다시 시도 횟수를 시도 간 대기 시간입니다. 트랜잭션을 사용 하는 경우 다시 시도 범위 toohello 돌아갑니다 있는지 확인의 일시적인 오류의 경우 hello hello 트랜잭션을 시작 합니다.

## <a name="limitations"></a>제한 사항
이 문서에 설명 된 hello 접근 방식에 몇 가지 제한 필요 합니다.

* 이 문서에 대 한 hello 샘플 코드를 보여 주지 않습니다 방법을 분할 영역 간에 toomanage 스키마입니다.
* 요청 제공을 hello 요청에서 제공 하는 hello 분할 키로 식별 되는 모든 데이터베이스 처리 단일 분할 영역에 포함 된 가정 합니다. 그러나이 가정을 유지 하지 않으면 항상, 예를 들어 가능한 toomake 분할 키를 사용할 수 없는 경우. tooaddress이,이 hello 탄력적 데이터베이스 클라이언트 라이브러리 포함 hello [MultiShardQuery 클래스](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardexception.aspx)합니다. hello 클래스에는 여러 분할 된 데이터베이스를 쿼리 하기 위한 연결 추상화를 구현 합니다. MultiShardQuery Dapper와 함께에서 사용 하 여이 설명서의 hello 다루지 않습니다.

## <a name="conclusion"></a>결론
Dapper 및 DapperExtensions를 사용하는 응용 프로그램에서는 Azure SQL 데이터베이스의 탄력적 데이터베이스 도구를 쉽게 활용할 수 있습니다. 이 문서에 설명 된 hello 단계를 통해 해당 응용 프로그램에 사용할 수 hello 도구 기능 변경 hello 작성 및 열기를 새로운 라우팅을 종속 데이터 [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) 개체 toouse hello [ OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) hello 탄력적 데이터베이스 클라이언트 라이브러리를 호출 합니다. 새 연결이 만들어지고 열려 있는 hello 응용 프로그램 변경 내용이 필요한 toothose 위치를 제한 합니다. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-working-with-dapper/dapperimage1.png
