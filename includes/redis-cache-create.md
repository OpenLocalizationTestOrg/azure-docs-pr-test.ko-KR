캐시 toocreate toohello에 처음 로그인 [Azure 포털](https://portal.azure.com), 클릭 하 고 **새로** > **데이터베이스** > **Redis Cache**.

> [!NOTE]
> Azure 계정이 없는 경우 몇 분 만에 [Azure 무료 계정을 열 수 있습니다](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) .
> 
> 

![새 캐시](media/redis-cache-create/redis-cache-new-cache-menu.png)

> [!NOTE]
> 또한 toocreating hello Azure 포털의에서 캐시, 리소스 관리자를 사용 하 여 만들 수도 있습니다 템플릿, PowerShell 또는 Azure CLI 합니다.
> 
> * 리소스 관리자 템플릿을 사용 하 여 캐시 a toocreate 참조 [서식 파일을 사용 하 여 Redis 캐시를 만들](../articles/redis-cache/cache-redis-cache-arm-provision.md)합니다.
> * Azure PowerShell을 사용 하 여 캐시 toocreate 참조 [Azure PowerShell을 사용한 Azure Redis Cache 관리](../articles/redis-cache/cache-howto-manage-redis-cache-powershell.md)합니다.
> * Azure CLI를 사용 하 여 캐시 toocreate 참조 [어떻게 toocreate hello Azure 명령줄 인터페이스 (Azure CLI)를 사용 하 여 Azure Redis 캐시를 관리 하 고](../articles/redis-cache/cache-manage-cli.md)합니다.
> 
> 

Hello에 **새 Redis 캐시** 블레이드에서 hello hello 캐시에 원하는 구성을 지정 합니다.

![캐시 만들기](media/redis-cache-create/redis-cache-cache-create.png) 

* **Dns 이름**, 고유한 캐시 이름 toouse hello 캐시 끝점에 대 한 입력 합니다. hello 캐시 이름은 1 자에서 63 자 사이의 문자열 이어야 하 고 숫자, 문자 및 hello 포함 `-` 문자입니다. hello 캐시 이름은 시작 하거나 끝날 수 없으며 hello로 `-` 문자와 연속 `-` 문자는 유효 하지 않습니다.
* 에 대 한 **구독**, 선택 hello hello 캐시에 대 한 toouse 되도록 Azure 구독. 계정에 구독 하나만, 있으면 자동으로 선택 및 hello **구독** 드롭다운 목록에 표시 되지 것입니다.
* **리소스 그룹**에서 캐시에 대한 리소스 그룹을 선택하거나 만듭니다. 자세한 내용은 참조 [를 사용 하 여 리소스 그룹의 Azure 리소스 toomanage](../articles/azure-resource-manager/resource-group-overview.md)합니다. 
* 사용 하 여 **위치** toospecify hello 여 캐시가 호스트 되는 지리적 위치입니다. Hello 최상의 성능을 위해 가장 좋습니다 hello에 hello 캐시 만들어야 hello 캐시 클라이언트 응용 프로그램과 같은 지역입니다.
* 사용 하 여 **가격 책정 계층** tooselect hello 원하는 캐시 크기 및 기능입니다.
* **Redis 클러스터** 있습니다 toocreate 캐시 53GB 및 tooshard 데이터 보다 큰 여러 Redis 노드에 있습니다. 자세한 내용은 참조 [어떻게 Premium Azure Redis Cache에 대 한 클러스터링 tooconfigure](../articles/redis-cache/cache-how-to-premium-clustering.md)합니다.
* **지 속성 redis** hello 기능 toopersist 프로그램 캐시 tooan Azure 저장소 계정을 제공 합니다. 에 대 한 지침은 지 속성을 구성을 참조 하세요. [어떻게 Premium Azure Redis Cache에 대 한 지 속성 tooconfigure](../articles/redis-cache/cache-how-to-premium-persistence.md)합니다.
* **가상 네트워크** 강화 된 보안 및 격리를 제공 tooyour 캐시 tooonly 액세스를 제한 하 여 해당 클라이언트를 지정 하는 hello 내에서 Azure 가상 네트워크입니다. 서브넷, 액세스 제어 정책 및 기타 기능 toofurther 제한 액세스 tooRedis 같은 VNet의 모든 hello 기능을 사용할 수 있습니다. 자세한 내용은 참조 [Premium Azure Redis Cache에 대 한 tooconfigure 가상 네트워크를 지 원하는 방법](../articles/redis-cache/cache-how-to-premium-vnet.md)합니다.
* 비 SSL 액세스는 기본적으로 새 캐시에 대해 사용하지 않도록 설정됩니다. tooenable hello 비 SSL 포트 검사 **6379 (암호화 된 SSL가 아닌) 포트의 차단을 해제**합니다.

새 캐시 옵션 hello 구성 되 면 클릭 **만들기**합니다. 만든 hello 캐시 toobe 몇 분 정도 걸릴 수 있습니다. toocheck hello 상태 hello 시작 보드 hello 진행 상태를 모니터링할 수 있습니다. Hello 캐시를 만든 후 새 캐시는는 **실행** 상태 이며 사용 하도록 준비 [기본 설정](../articles/redis-cache/cache-configure.md#default-redis-server-configuration)합니다.

![캐시 만듬](media/redis-cache-create/redis-cache-cache-created.png)

