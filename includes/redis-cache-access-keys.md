<span data-ttu-id="88adb-101">tooconnect tooan Azure Redis Cache 인스턴스 캐시 클라이언트 hello 호스트 이름, 포트와 hello 캐시의 키가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="88adb-101">tooconnect tooan Azure Redis Cache instance, cache clients need hello host name, ports, and keys of hello cache.</span></span> <span data-ttu-id="88adb-102">일부 클라이언트는 약간 다른 이름으로 toothese 항목을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88adb-102">Some clients may refer toothese items by slightly different names.</span></span> <span data-ttu-id="88adb-103">Hello Azure 포털 또는 Azure CLI 같은 명령줄 도구를 사용 하 여이 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88adb-103">You can retrieve this information in hello Azure portal or by using command-line tools such as Azure CLI.</span></span>

### <a name="retrieve-host-name-ports-and-access-keys-using-hello-azure-portal"></a><span data-ttu-id="88adb-104">호스트 이름, 포트 및 hello Azure 포털을 사용 하 여 액세스 키를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="88adb-104">Retrieve host name, ports, and access keys using hello Azure Portal</span></span>
<span data-ttu-id="88adb-105">tooretrieve 호스트 이름, 포트 및 액세스 키 hello Azure 포털을 사용 하 여 [찾아보기](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) tooyour 캐시 hello에 [Azure 포털](https://portal.azure.com) 클릭 **선택키가** 및  **속성** hello에 **리소스 메뉴**합니다.</span><span class="sxs-lookup"><span data-stu-id="88adb-105">tooretrieve host name, ports, and access keys using hello Azure Portal, [browse](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) tooyour cache in hello [Azure portal](https://portal.azure.com) and click **Access keys** and **Properties** in hello **Resource menu**.</span></span> 

![Redis Cache 설정](media/redis-cache-access-keys/redis-cache-hostname-ports-keys.png)

### <a name="retrieve-host-name-ports-and-access-keys-using-azure-cli"></a><span data-ttu-id="88adb-107">Azure CLI를 사용하여 호스트 이름, 포트 및 액세스 키를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="88adb-107">Retrieve host name, ports, and access keys using Azure CLI</span></span>
<span data-ttu-id="88adb-108">tooretrieve hello 호스트 이름 및 Azure CLI 2.0을 사용 하 여 포트를 호출할 수 있습니다 [az redis 표시](https://docs.microsoft.com/cli/azure/redis#show), 및를 호출할 수 있습니다 tooretrieve hello 키 [az redis 키 나열](https://docs.microsoft.com/cli/azure/redis#list-keys)합니다.</span><span class="sxs-lookup"><span data-stu-id="88adb-108">tooretrieve hello host name and ports using Azure CLI 2.0 you can call [az redis show](https://docs.microsoft.com/cli/azure/redis#show), and tooretrieve hello keys you can call [az redis list-keys](https://docs.microsoft.com/cli/azure/redis#list-keys).</span></span> <span data-ttu-id="88adb-109">hello 다음 스크립트를 호출 하이 두 명령은 echos hello 호스트 이름, 포트 및 키 toohello 콘솔.</span><span class="sxs-lookup"><span data-stu-id="88adb-109">hello following script calls these two commands and echos hello hostname, ports, and keys toohello console.</span></span>

```azurecli
#/bin/bash

# Retrieve hello hostname, ports, and keys for contosoCache located in contosoGroup

# Retrieve hello hostname and ports for an Azure Redis Cache instance
redis=($(az redis show --name contosoCache --resource-group contosoGroup --query [hostName,enableNonSslPort,port,sslPort] --output tsv))

# Retrieve hello keys for an Azure Redis Cache instance
keys=($(az redis list-keys --name contosoCache --resource-group contosoGroup --query [primaryKey,secondaryKey] --output tsv))

# Display hello retrieved hostname, keys, and ports
echo "Hostname:" ${redis[0]}
echo "Non SSL Port:" ${redis[2]}
echo "Non SSL Port Enabled:" ${redis[1]}
echo "SSL Port:" ${redis[3]}
echo "Primary Key:" ${keys[0]}
echo "Secondary Key:" ${keys[1]}
```

<span data-ttu-id="88adb-110">이 스크립트에 대 한 자세한 내용은 참조 [Azure Redis Cache에 대 한 hello 호스트 이름, 포트 및 키 가져오기](../articles/redis-cache/scripts/cache-keys-ports.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="88adb-110">For more information about this script, see [Get hello hostname, ports, and keys for Azure Redis Cache](../articles/redis-cache/scripts/cache-keys-ports.md).</span></span> <span data-ttu-id="88adb-111">Azure CLI 2.0에 대한 자세한 내용은 [Azure CLI 2.0 설치](https://docs.microsoft.com/cli/azure/install-azure-cli) 및 [Azure CLI 2.0 시작](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="88adb-111">For more information on Azure CLI 2.0, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) and [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>
