tooconnect tooan Azure Redis Cache 인스턴스 캐시 클라이언트 hello 호스트 이름, 포트와 hello 캐시의 키가 필요 합니다. 일부 클라이언트는 약간 다른 이름으로 toothese 항목을 참조할 수 있습니다. Hello Azure 포털 또는 Azure CLI 같은 명령줄 도구를 사용 하 여이 정보를 검색할 수 있습니다.

### <a name="retrieve-host-name-ports-and-access-keys-using-hello-azure-portal"></a>호스트 이름, 포트 및 hello Azure 포털을 사용 하 여 액세스 키를 검색 합니다.
tooretrieve 호스트 이름, 포트 및 액세스 키 hello Azure 포털을 사용 하 여 [찾아보기](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) tooyour 캐시 hello에 [Azure 포털](https://portal.azure.com) 클릭 **선택키가** 및  **속성** hello에 **리소스 메뉴**합니다. 

![Redis Cache 설정](media/redis-cache-access-keys/redis-cache-hostname-ports-keys.png)

### <a name="retrieve-host-name-ports-and-access-keys-using-azure-cli"></a>Azure CLI를 사용하여 호스트 이름, 포트 및 액세스 키를 검색합니다.
tooretrieve hello 호스트 이름 및 Azure CLI 2.0을 사용 하 여 포트를 호출할 수 있습니다 [az redis 표시](https://docs.microsoft.com/cli/azure/redis#show), 및를 호출할 수 있습니다 tooretrieve hello 키 [az redis 키 나열](https://docs.microsoft.com/cli/azure/redis#list-keys)합니다. hello 다음 스크립트를 호출 하이 두 명령은 echos hello 호스트 이름, 포트 및 키 toohello 콘솔.

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

이 스크립트에 대 한 자세한 내용은 참조 [Azure Redis Cache에 대 한 hello 호스트 이름, 포트 및 키 가져오기](../articles/redis-cache/scripts/cache-keys-ports.md)합니다. Azure CLI 2.0에 대한 자세한 내용은 [Azure CLI 2.0 설치](https://docs.microsoft.com/cli/azure/install-azure-cli) 및 [Azure CLI 2.0 시작](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)을 참조하세요.
