---
title: "자습서: Entity Framework 및 행 수준 보안을 사용하여 다중 테넌트 데이트베이스를 포함하는 웹 앱"
description: "Toodevelop ASP.NET MVC 5는 다중 테 넌 트와 SQL 데이터베이스 backent, Entity Framework와 행 수준 보안을 사용 하 여 응용 프로그램 웹 하는 방법에 대해 알아봅니다."
metakeywords: azure asp.net mvc entity framework multi tenant row level security rls sql database
services: app-service\web
documentationcenter: .net
manager: jeffreyg
author: tmullaney
ms.assetid: 8fdc47a5-6fc3-4d29-ab6a-33e79f50699f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/25/2016
ms.author: thmullan
ms.openlocfilehash: 1b715e01807032c3f6497c374ce427dd762af141
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a><span data-ttu-id="4f4db-103">자습서: Entity Framework 및 행 수준 보안을 사용하여 다중 테넌트 데이트베이스를 포함하는 웹 앱</span><span class="sxs-lookup"><span data-stu-id="4f4db-103">Tutorial: Web app with a multi-tenant database using Entity Framework and Row-Level Security</span></span>
<span data-ttu-id="4f4db-104">이 자습서에서는 어떻게 toobuild 다중 테 넌 트 웹 응용 프로그램으로는 "[공유 데이터베이스, 공유 스키마](https://msdn.microsoft.com/library/aa479086.aspx)" Entity Framework를 사용 하 여 테 넌 트 모델 및 [행 수준 보안](https://msdn.microsoft.com/library/dn765131.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-104">This tutorial shows how toobuild a multi-tenant web app with a "[shared database, shared schema](https://msdn.microsoft.com/library/aa479086.aspx)" tenancy model, using Entity Framework and [Row-Level Security](https://msdn.microsoft.com/library/dn765131.aspx).</span></span> <span data-ttu-id="4f4db-105">이 모델에서 단일 데이터베이스는 많은 테넌트의 데이터를 포함하고 각 테이블의 각 행은 "Tenant ID"와 연결되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-105">In this model, a single database contains data for many tenants, and each row in each table is associated with a "Tenant ID."</span></span> <span data-ttu-id="4f4db-106">행 수준 보안 (RLS), Azure SQL 데이터베이스에 대 한 새로운 기능에는 다른 사용자의 데이터에 액세스 하지 못하도록 tooprevent 사용 되는 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-106">Row-Level Security (RLS), a new feature for Azure SQL Database, is used tooprevent tenants from accessing each other's data.</span></span> <span data-ttu-id="4f4db-107">여기에 단일, 작은 변경 toohello 응용 프로그램만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-107">This requires just a single, small change toohello application.</span></span> <span data-ttu-id="4f4db-108">중앙 집중화 hello 테 넌 트 액세스 hello 데이터베이스 자체 내의 논리에 의해 RLS hello 응용 프로그램 코드를 간소화 하 고 hello 테 넌 트 간에 데이터를 유출할 위험도 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-108">By centralizing hello tenant access logic within hello database itself, RLS simplifies hello application code and reduces hello risk of accidental data leakage between tenants.</span></span>

<span data-ttu-id="4f4db-109">Hello 간단한에서 않아 응용 프로그램부터 살펴보겠습니다 [인증 및 SQL DB ASP.NET MVP 응용 프로그램을 만들고 tooAzure 앱 서비스 배포](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-109">Let's start with hello simple Contact Manager application from [Create an ASP.NET MVP app with auth and SQL DB and deploy tooAzure App Service](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span> <span data-ttu-id="4f4db-110">권한을 이제 hello 응용 프로그램 사용 하면 모든 사용자 (테 넌 트) toosee 모든 연락처:</span><span class="sxs-lookup"><span data-stu-id="4f4db-110">Right now, hello application allows all users (tenants) toosee all contacts:</span></span>

![RLS를 활성화하기 전의 연락처 관리자 응용 프로그램](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

<span data-ttu-id="4f4db-112">몇 개의 작은 변경과 수 toosee hello 연락처만 toothem 속해 있는 사용자가 없도록 다중 테 넌 트에 대 한 지원을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-112">With just a few small changes, we will add support for multi-tenancy, so that users are able toosee only hello contacts that belong toothem.</span></span>

## <a name="step-1-add-an-interceptor-class-in-hello-application-tooset-hello-sessioncontext"></a><span data-ttu-id="4f4db-113">1 단계: hello 응용 프로그램 tooset hello SESSION_CONTEXT에서에서 인터셉터 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="4f4db-113">Step 1: Add an Interceptor class in hello application tooset hello SESSION_CONTEXT</span></span>
<span data-ttu-id="4f4db-114">하나의 응용 프로그램 변경 toomake 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-114">There is one application change we need toomake.</span></span> <span data-ttu-id="4f4db-115">모든 응용 프로그램 사용자가 연결 때문에 동일한 연결 문자열 (즉, 같은 SQL 로그인) hello toohello 데이터베이스를 사용 하 여, 현재 사용자에 대 한 필터링 해야 하는 RLS 정책 tooknow에 대 한 방법이 있으면 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-115">Because all application users connect toohello database using hello same connection string (i.e. same SQL login), there is currently no way for an RLS policy tooknow which user it should filter for.</span></span> <span data-ttu-id="4f4db-116">이 방법은 효율적인 연결 풀링을 사용 하면 출력 형식 이지만 다른 방식으로 tooidentify hello 현재 응용 프로그램 사용자 hello 데이터베이스 내에서 필요 하기 때문에 웹 응용 프로그램에서 매우 흔히 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-116">This approach is very common in web applications because it enables efficient connection pooling, but it means we need another way tooidentify hello current application user within hello database.</span></span> <span data-ttu-id="4f4db-117">hello 솔루션은 toohave hello 응용 프로그램 집합에 대 한 키-값 쌍 hello의 현재 UserId hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) 한 연결을 연 후 바로 전에 실행 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-117">hello solution is toohave hello application set a key-value pair for hello current UserId in hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) immediately after opening a connection, before it executes any queries.</span></span> <span data-ttu-id="4f4db-118">SESSION_CONTEXT 세션 범위 키-값 저장소 이며 우리의 RLS 정책을 hello에 저장 된 사용자 Id ´ ֲ tooidentify hello에 대 한 현재 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-118">SESSION_CONTEXT is a session-scoped key-value store, and our RLS policy will use hello UserId stored in it tooidentify hello current user.</span></span>

<span data-ttu-id="4f4db-119">추가 [인터셉터](https://msdn.microsoft.com/data/dn469464.aspx) (특히는 [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), 새로운 기능에 Entity Framework (EF) 6, tooautomatically 집합을 실행 하 여 현재 사용자 Id SESSION_CONTEXT hello에 hello는 T-SQL 문 때마다 EF 연결을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-119">We will add an [interceptor](https://msdn.microsoft.com/data/dn469464.aspx) (in particular, a [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), a new feature in Entity Framework (EF) 6, tooautomatically set hello current UserId in hello SESSION_CONTEXT by executing a T-SQL statement whenever EF opens a connection.</span></span>

1. <span data-ttu-id="4f4db-120">Visual Studio에서 hello ContactManager 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-120">Open hello ContactManager project in Visual Studio.</span></span>
2. <span data-ttu-id="4f4db-121">Hello 솔루션 탐색기에서에서 hello 모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 추가 선택 > 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-121">Right-click on hello Models folder in hello Solution Explorer, and choose Add > Class.</span></span>
3. <span data-ttu-id="4f4db-122">"SessionContextInterceptor.cs" hello 새 클래스를 이름을 지정 하 고 추가 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-122">Name hello new class "SessionContextInterceptor.cs" and click Add.</span></span>
4. <span data-ttu-id="4f4db-123">Hello 내용의 SessionContextInterceptor.cs 코드 다음 hello로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-123">Replace hello contents of SessionContextInterceptor.cs with hello following code.</span></span>

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Data.Common;
using System.Data.Entity;
using System.Data.Entity.Infrastructure.Interception;
using Microsoft.AspNet.Identity;

namespace ContactManager.Models
{
    public class SessionContextInterceptor : IDbConnectionInterceptor
    {
        public void Opened(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
            // Set SESSION_CONTEXT toocurrent UserId whenever EF opens a connection
            try
            {
                var userId = System.Web.HttpContext.Current.User.Identity.GetUserId();
                if (userId != null)
                {
                    DbCommand cmd = connection.CreateCommand();
                    cmd.CommandText = "EXEC sp_set_session_context @key=N'UserId', @value=@UserId";
                    DbParameter param = cmd.CreateParameter();
                    param.ParameterName = "@UserId";
                    param.Value = userId;
                    cmd.Parameters.Add(param);
                    cmd.ExecuteNonQuery();
                }
            }
            catch (System.NullReferenceException)
            {
                // If no user is logged in, leave SESSION_CONTEXT null (all rows will be filtered)
            }
        }

        public void Opening(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void BeganTransaction(DbConnection connection, BeginTransactionInterceptionContext interceptionContext)
        {
        }

        public void BeginningTransaction(DbConnection connection, BeginTransactionInterceptionContext interceptionContext)
        {
        }

        public void Closed(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void Closing(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void ConnectionStringGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionStringGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionStringSet(DbConnection connection, DbConnectionPropertyInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionStringSetting(DbConnection connection, DbConnectionPropertyInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionTimeoutGetting(DbConnection connection, DbConnectionInterceptionContext<int> interceptionContext)
        {
        }

        public void ConnectionTimeoutGot(DbConnection connection, DbConnectionInterceptionContext<int> interceptionContext)
        {
        }

        public void DataSourceGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void DataSourceGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void DatabaseGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void DatabaseGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void Disposed(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void Disposing(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void EnlistedTransaction(DbConnection connection, EnlistTransactionInterceptionContext interceptionContext)
        {
        }

        public void EnlistingTransaction(DbConnection connection, EnlistTransactionInterceptionContext interceptionContext)
        {
        }

        public void ServerVersionGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void ServerVersionGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void StateGetting(DbConnection connection, DbConnectionInterceptionContext<System.Data.ConnectionState> interceptionContext)
        {
        }

        public void StateGot(DbConnection connection, DbConnectionInterceptionContext<System.Data.ConnectionState> interceptionContext)
        {
        }
    }

    public class SessionContextConfiguration : DbConfiguration
    {
        public SessionContextConfiguration()
        {
            AddInterceptor(new SessionContextInterceptor());
        }
    }
}
```

<span data-ttu-id="4f4db-124">그건 hello 전용 응용 프로그램 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-124">That's hello only application change required.</span></span> <span data-ttu-id="4f4db-125">계속 하 고 빌드를 hello 응용 프로그램을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-125">Go ahead and build and publish hello application.</span></span>

## <a name="step-2-add-a-userid-column-toohello-database-schema"></a><span data-ttu-id="4f4db-126">2 단계: 사용자 Id 열 toohello 데이터베이스 스키마를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-126">Step 2: Add a UserId column toohello database schema</span></span>
<span data-ttu-id="4f4db-127">다음으로 필요 tooadd UserId 열 toohello 연락처 테이블 tooassociate 각 행에 사용자 (테 넌 트) 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-127">Next, we need tooadd a UserId column toohello Contacts table tooassociate each row with a user (tenant).</span></span> <span data-ttu-id="4f4db-128">Hello 데이터베이스에서 직접 hello 스키마를 변경 했습니다 하 아직 tooinclude이이 필드의 EF 데이터 모델에서 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-128">We will alter hello schema directly in hello database, so that we don't have tooinclude this field in our EF data model.</span></span>

<span data-ttu-id="4f4db-129">Toohello 데이터베이스 SQL Server Management Studio 또는 Visual Studio를 사용 하 여 직접 연결 하 고 hello 다음 T-SQL을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-129">Connect toohello database directly, using either SQL Server Management Studio or Visual Studio, and then execute hello following T-SQL:</span></span>

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

<span data-ttu-id="4f4db-130">이 사용자 Id 열 toohello Contacts 테이블을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-130">This adds a UserId column toohello Contacts table.</span></span> <span data-ttu-id="4f4db-131">Hello nvarchar (128) 데이터 형식 toomatch hello hello AspNetUsers 테이블에 저장 된 사용자 Id를 사용 하 고 새로 삽입된 된 행 toobe hello SESSION_CONTEXT에 현재 저장 된 사용자 Id에 대 한 UserId hello에서 자동으로 설정 하는 기본 제약 조건을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-131">We use hello nvarchar(128) data type toomatch hello UserIds stored in hello AspNetUsers table, and we create a DEFAULT constraint that will automatically set hello UserId for newly inserted rows toobe hello UserId currently stored in SESSION_CONTEXT.</span></span>

<span data-ttu-id="4f4db-132">이제 hello 테이블은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-132">Now hello table looks like this:</span></span>

![SSMS Contacts 테이블](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

<span data-ttu-id="4f4db-134">새 연락처가 만들어지면 이러한 합니다 자동으로 할당 hello 사용자 Id를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-134">When new contacts are created, they'll automatically be assigned hello correct UserId.</span></span> <span data-ttu-id="4f4db-135">하지만 데모 목적에 대 한 사용자를 기존의 이러한 기존 연락처 tooan 중 몇 가지 보겠습니다 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-135">For demo purposes, however, let's assign a few of these existing contacts tooan existing user.</span></span>

<span data-ttu-id="4f4db-136">하는 경우 사용자가 이미 hello 응용 프로그램에서 만든 (예: 로컬을 사용 하 여, Google 또는 Facebook 계정), hello AspNetUsers 표에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-136">If you've created a few users in hello application already (e.g., using local, Google, or Facebook accounts), you'll see them in hello AspNetUsers table.</span></span> <span data-ttu-id="4f4db-137">Hello 아래 스크린샷, 즉 한 명의 사용자만 지금까지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-137">In hello screenshot below, there is only one user so far.</span></span>

![SSMS AspNetUsers 테이블](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

<span data-ttu-id="4f4db-139">복사 hello Id에 대 한 user1@contoso.com, hello T-SQL 문 아래에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-139">Copy hello Id for user1@contoso.com, and paste it into hello T-SQL statement below.</span></span> <span data-ttu-id="4f4db-140">이 사용자 Id 사용 하 여 hello 연락처의이 문을 tooassociate 3을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-140">Execute this statement tooassociate three of hello Contacts with this UserId.</span></span>

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-hello-database"></a><span data-ttu-id="4f4db-141">3 단계: hello 데이터베이스에서 행 수준 보안 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="4f4db-141">Step 3: Create a Row-Level Security policy in hello database</span></span>
<span data-ttu-id="4f4db-142">hello 최종 단계 toocreate SESSION_CONTEXT tooautomatically 필터 hello 결과 쿼리에 의해 반환 된에 UserId hello를 사용 하는 보안 정책을입니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-142">hello final step is toocreate a security policy that uses hello UserId in SESSION_CONTEXT tooautomatically filter hello results returned by queries.</span></span>

<span data-ttu-id="4f4db-143">계속 연결 된 toohello 데이터베이스 동안 hello 다음 T-SQL을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-143">While still connected toohello database, execute hello following T-SQL:</span></span>

```
CREATE SCHEMA Security
go

CREATE FUNCTION Security.userAccessPredicate(@UserId nvarchar(128))
    RETURNS TABLE
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS accessResult
    WHERE @UserId = CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
go

CREATE SECURITY POLICY Security.userSecurityPolicy
    ADD FILTER PREDICATE Security.userAccessPredicate(UserId) ON dbo.Contacts,
    ADD BLOCK PREDICATE Security.userAccessPredicate(UserId) ON dbo.Contacts
go

```

<span data-ttu-id="4f4db-144">이 코드는 세 가지를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-144">This code does three things.</span></span> <span data-ttu-id="4f4db-145">첫째, 중앙 집중화 하 고 toohello RLS 개체 액세스 제한에 대 한 가장 좋은 방법은 새 스키마를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-145">First, it creates a new schema as a best practice for centralizing and limiting access toohello RLS objects.</span></span> <span data-ttu-id="4f4db-146">다음으로 행의 UserId hello hello SESSION_CONTEXT에서 사용자 Id와 일치 하는 경우 '1'을 반환 하는 조건자 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-146">Next, it creates a predicate function that will return '1' when hello UserId of a row matches hello UserId in SESSION_CONTEXT.</span></span> <span data-ttu-id="4f4db-147">마지막으로 hello Contacts 테이블에 필터와 차단 조건자로이 함수를 추가 하는 보안 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-147">Finally, it creates a security policy that adds this function as both a filter and block predicate on hello Contacts table.</span></span> <span data-ttu-id="4f4db-148">hello 필터 조건자 쿼리 tooreturn toohello 현재 사용자에 속하는 행만 시키고 hello 블록 조건자 역할 보호 tooprevent hello 응용 프로그램에서 현재까지 실수로 hello 잘못 된 사용자에 대 한 행을 삽입을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-148">hello filter predicate causes queries tooreturn only rows that belong toohello current user, and hello block predicate acts as a safeguard tooprevent hello application from ever accidentally inserting a row for hello wrong user.</span></span>

<span data-ttu-id="4f4db-149">이제 hello 응용 프로그램을 실행 하 고로 로그인 user1@contoso.com합니다. 이 사용자는 이제 toothis UserId 이전 할당 hello 연락처만에서는 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-149">Now run hello application, and sign in as user1@contoso.com. This user now sees only hello Contacts we assigned toothis UserId earlier:</span></span>

![RLS를 활성화하기 전의 연락처 관리자 응용 프로그램](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

<span data-ttu-id="4f4db-151">toovalidate 새 사용자를 등록 하는 중이 추가 해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="4f4db-151">toovalidate this further, try registering a new user.</span></span> <span data-ttu-id="4f4db-152">없는 연락처 toothem 할당 된 none 때문에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-152">They will see no contacts, because none have been assigned toothem.</span></span> <span data-ttu-id="4f4db-153">새 연락처를 만들 toothem, 할당 됩니다 하 고 수 toosee 수만 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-153">If they create a new contact, it will be assigned toothem, and only they will be able toosee it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f4db-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4f4db-154">Next steps</span></span>
<span data-ttu-id="4f4db-155">이것으로 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-155">That's it!</span></span> <span data-ttu-id="4f4db-156">hello 간단한 연락처 관리자 웹 응용 프로그램은 각 사용자는 자체 대화 상대 목록에 하나 다중 테 넌 트로 변환 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-156">hello simple Contact Manager web app has been converted into a multi-tenant one where each user has its own contact list.</span></span> <span data-ttu-id="4f4db-157">행 수준 보안을 사용 하 여 응용 프로그램 코드에서 테 넌 트 액세스 논리를 적용 하는 hello 복잡성을 피할 수 했습니다 우리 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-157">By using Row-Level Security, we've avoided hello complexity of enforcing tenant access logic in our application code.</span></span> <span data-ttu-id="4f4db-158">이 투명도 hello 응용 프로그램 toofocus hello 실제 비즈니스 문제,에 있으며 실수로 hello 응용 프로그램의 코드 베이스 처럼 데이터 노출이 대수롭지 hello 위험이 감소 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-158">This transparency allows hello application toofocus on hello real business problem at hand, and it also reduces hello risk of accidentally leaking data as hello application's codebase grows.</span></span>

<span data-ttu-id="4f4db-159">이 자습서에는 RLS로 가능한의 긁힌된 hello 화면만 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-159">This tutorial has only scratched hello surface of what's possible with RLS.</span></span> <span data-ttu-id="4f4db-160">예를 들어, 가능한 toohave 보다 정교한 나 hello SESSION_CONTEXT hello에 현재 사용자 Id 보다 더 세부적인 액세스 논리 및 가능한 toostore 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-160">For instance, it's possible toohave more sophisticated or granular access logic, and it's possible toostore more than just hello current UserId in hello SESSION_CONTEXT.</span></span> <span data-ttu-id="4f4db-161">것도 가능 너무[hello 탄력적 데이터베이스 도구 클라이언트 라이브러리와 함께 RLS 통합](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) 확장 데이터 계층의 toosupport 다중 테 넌 트 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-161">It's also possible too[integrate RLS with hello elastic database tools client libraries](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) toosupport multi-tenant shards in a scale-out data tier.</span></span>

<span data-ttu-id="4f4db-162">이러한 가능성 외도 최선을 다하고 toomake RLS 모양을 개선 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-162">Beyond these possibilities, we're also working toomake RLS even better.</span></span> <span data-ttu-id="4f4db-163">질문, 의견, 또는 toosee 원하는 작업 있으면 알려 주시면 hello 설명에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-163">If you have any questions, ideas, or things you'd like toosee, please let us know in hello comments.</span></span> <span data-ttu-id="4f4db-164">여러분의 의견에 감사드립니다.</span><span class="sxs-lookup"><span data-stu-id="4f4db-164">We appreciate your feedback!</span></span>

