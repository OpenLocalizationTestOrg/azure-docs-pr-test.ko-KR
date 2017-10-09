.NET 응용 프로그램에서는 hello **StackExchange.Redis** 캐시 클라이언트에 캐시 클라이언트 응용 프로그램의 hello 구성을 단순화 하는 NuGet 패키지를 사용 하 여 Visual Studio에서 구성할 수 있습니다. 

> [!NOTE]
> 자세한 내용은 참조 hello [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github 페이지 및 hello [StackExchange.Redis 캐시 클라이언트 설명서](http://github.com/StackExchange/StackExchange.Redis#documentation)합니다.
> 
> 

tooconfigure hello StackExchange.Redis NuGet 패키지를 사용 하 여 Visual Studio에서 클라이언트 응용 프로그램에서 hello 프로젝트를 마우스 오른쪽 단추로 클릭 **솔루션 탐색기** 선택 **NuGet 패키지 관리**합니다. 

![NuGet 패키지 관리](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-manage-nuget-menu.png)

형식 **StackExchange.Redis** 또는 **StackExchange.Redis.StrongName** hello 검색 텍스트 상자에 hello 결과에서 hello 원하는 버전을 선택 하 고 클릭 **설치**합니다.

> [!NOTE]
> 강력한 이름의 버전의 hello toouse 것을 선호 하는 경우 **StackExchange.Redis** 클라이언트 라이브러리를 선택 **StackExchange.Redis.StrongName**; 그렇지 않은 경우 선택 **StackExchange.Redis**.
> 
> 

![StackExchange.Redis NuGet 패키지](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-stackexchange-redis.png)

NuGet 패키지가 다운로드 되 고 추가 하는 hello hello hello StackExchange.Redis 캐시 클라이언트를 사용한 프로그램 클라이언트 응용 프로그램 tooaccess Azure Redis Cache에 대 한 어셈블리 참조가 필요 합니다.

> [!NOTE]
> 사용자 프로젝트 toouse StackExchange.Redis 이전에 구성한 경우 hello에서 toohello 패키지 업데이트를 확인할 수 있습니다 **NuGet 패키지 관리자**합니다. 에 대 한 toocheck hello StackExchange.Redis NuGet 패키지의 업데이트 설치 버전을 클릭 하 여 **업데이트** hello hello에 **NuGet 패키지 관리자** 창. 업데이트 toohello StackExchange.Redis NuGet 패키지를 사용할 수 있는 경우에 프로젝트 toouse hello 업데이트 버전을 업데이트할 수 있습니다.
> 
> 

클릭 하 여 hello StackExchange.Redis NuGet 패키지를 설치할 수도 있습니다 **NuGet 패키지 관리자**, **패키지 관리자 콘솔** hello에서 **도구** 메뉴 및 실행 중인 hello hello에서 다음 명령을 **패키지 관리자 콘솔** 창.
    
```
Install-Package StackExchange.Redis
```
