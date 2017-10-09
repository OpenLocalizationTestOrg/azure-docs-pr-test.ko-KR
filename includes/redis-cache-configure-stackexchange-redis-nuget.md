<span data-ttu-id="912cd-101">.NET 응용 프로그램에서는 hello **StackExchange.Redis** 캐시 클라이언트에 캐시 클라이언트 응용 프로그램의 hello 구성을 단순화 하는 NuGet 패키지를 사용 하 여 Visual Studio에서 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="912cd-101">.NET applications can use hello **StackExchange.Redis** cache client, which can be configured in Visual Studio using a NuGet package that simplifies hello configuration of cache client applications.</span></span> 

> [!NOTE]
> <span data-ttu-id="912cd-102">자세한 내용은 참조 hello [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github 페이지 및 hello [StackExchange.Redis 캐시 클라이언트 설명서](http://github.com/StackExchange/StackExchange.Redis#documentation)합니다.</span><span class="sxs-lookup"><span data-stu-id="912cd-102">For more information, see hello [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github page and  hello [StackExchange.Redis cache client documentation](http://github.com/StackExchange/StackExchange.Redis#documentation).</span></span>
> 
> 

<span data-ttu-id="912cd-103">tooconfigure hello StackExchange.Redis NuGet 패키지를 사용 하 여 Visual Studio에서 클라이언트 응용 프로그램에서 hello 프로젝트를 마우스 오른쪽 단추로 클릭 **솔루션 탐색기** 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="912cd-103">tooconfigure a client application in Visual Studio using hello StackExchange.Redis NuGet package, right-click hello project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span> 

![NuGet 패키지 관리](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-manage-nuget-menu.png)

<span data-ttu-id="912cd-105">형식 **StackExchange.Redis** 또는 **StackExchange.Redis.StrongName** hello 검색 텍스트 상자에 hello 결과에서 hello 원하는 버전을 선택 하 고 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="912cd-105">Type **StackExchange.Redis** or **StackExchange.Redis.StrongName** into hello search text box, select hello desired version from hello results, and click **Install**.</span></span>

> [!NOTE]
> <span data-ttu-id="912cd-106">강력한 이름의 버전의 hello toouse 것을 선호 하는 경우 **StackExchange.Redis** 클라이언트 라이브러리를 선택 **StackExchange.Redis.StrongName**; 그렇지 않은 경우 선택 **StackExchange.Redis**.</span><span class="sxs-lookup"><span data-stu-id="912cd-106">If you prefer toouse a strong-named version of hello **StackExchange.Redis** client library, choose **StackExchange.Redis.StrongName**; otherwise choose **StackExchange.Redis**.</span></span>
> 
> 

![StackExchange.Redis NuGet 패키지](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-stackexchange-redis.png)

<span data-ttu-id="912cd-108">NuGet 패키지가 다운로드 되 고 추가 하는 hello hello hello StackExchange.Redis 캐시 클라이언트를 사용한 프로그램 클라이언트 응용 프로그램 tooaccess Azure Redis Cache에 대 한 어셈블리 참조가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="912cd-108">hello NuGet package downloads and adds hello required assembly references for your client application tooaccess Azure Redis Cache with hello StackExchange.Redis cache client.</span></span>

> [!NOTE]
> <span data-ttu-id="912cd-109">사용자 프로젝트 toouse StackExchange.Redis 이전에 구성한 경우 hello에서 toohello 패키지 업데이트를 확인할 수 있습니다 **NuGet 패키지 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="912cd-109">If you have previously configured your project toouse StackExchange.Redis, you can check for updates toohello package from hello **NuGet Package Manager**.</span></span> <span data-ttu-id="912cd-110">에 대 한 toocheck hello StackExchange.Redis NuGet 패키지의 업데이트 설치 버전을 클릭 하 여 **업데이트** hello hello에 **NuGet 패키지 관리자** 창.</span><span class="sxs-lookup"><span data-stu-id="912cd-110">toocheck for and install updated versions of hello StackExchange.Redis NuGet package, click **Updates** in hello hello **NuGet Package Manager** window.</span></span> <span data-ttu-id="912cd-111">업데이트 toohello StackExchange.Redis NuGet 패키지를 사용할 수 있는 경우에 프로젝트 toouse hello 업데이트 버전을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="912cd-111">If an update toohello StackExchange.Redis NuGet package is available, you can update your project toouse hello updated version.</span></span>
> 
> 

<span data-ttu-id="912cd-112">클릭 하 여 hello StackExchange.Redis NuGet 패키지를 설치할 수도 있습니다 **NuGet 패키지 관리자**, **패키지 관리자 콘솔** hello에서 **도구** 메뉴 및 실행 중인 hello hello에서 다음 명령을 **패키지 관리자 콘솔** 창.</span><span class="sxs-lookup"><span data-stu-id="912cd-112">You can also install hello StackExchange.Redis NuGet package by clicking **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu, and running hello following command from hello **Package Manager Console** window.</span></span>
    
```
Install-Package StackExchange.Redis
```
