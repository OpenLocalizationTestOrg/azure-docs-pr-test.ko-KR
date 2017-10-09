tooadd 태그 tooa 리소스 그룹을 사용 하 여 **으로 azure 그룹 집합**합니다. Hello 리소스 그룹에는 기존 태그 hello 태그에 전달 됩니다.

```azurecli
azure group set -n tag-demo-group -t Dept=Finance
```

태그는 전체적으로 업데이트됩니다. Tooadd 기존 태그 된 태그 tooa 리소스 그룹을 사용 하도록 하려는 경우 모든 hello 태그를 전달 합니다. 

```azurecli
azure group set -n tag-demo-group -t Dept=Finance;Environment=Production;Project=Upgrade
```

태그는 리소스 그룹에 있는 리소스에 의해 상속되지 않습니다. tooadd 태그 tooa 리소스를 사용 하 여 **azure 리소스 집합**합니다. Hello hello 태그를 추가 하는 hello 리소스 유형에 대 한 API 버전 번호를 전달 합니다. Tooretrieve hello API 버전을 해야 하는 경우 다음 설정 하는 hello 형식에 대 한 hello 리소스 공급자와 명령을 hello를 사용 합니다.

```azurecli
azure provider show -n Microsoft.Storage --json
```

Hello 결과에서 원하는 hello 리소스 종류를 찾습니다.

```azurecli
"resourceTypes": [
{
  "resourceType": "storageAccounts",
  ...
  "apiVersions": [
    "2016-01-01",
    "2015-06-15",
    "2015-05-01-preview"
  ]
}
...
```

이제 API 버전, 리소스 그룹 이름, 리소스 이름, 리소스 유형 및 태그 값을 매개 변수로 제공합니다.

```azurecli
azure resource set -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -t Dept=Finance -o 2016-01-01
```

태그는 리소스 및 리소스 그룹에 직접 존재합니다. 리소스 그룹을 사용 하 여 해당 리소스 toosee hello 기존 태그 가져오기 **으로 azure 그룹 표시**합니다.

```azurecli
azure group show -n tag-demo-group --json
```

모든 태그가 적용 tooit 포함 hello 리소스 그룹에 대 한 메타 데이터를 반환 합니다.

```azurecli
{
  "id": "/subscriptions/4705409c-9372-42f0-914c-64a504530837/resourceGroups/tag-demo-group",
  "name": "tag-demo-group",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "location": "southcentralus",
  "tags": {
    "Dept": "Finance",
    "Environment": "Production",
    "Project": "Upgrade"
  },
  ...
}
```

사용 하 여 특정 리소스에 대 한 hello 태그를 보면 **azure 리소스 표시**합니다.

```azurecli
azure resource show -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -o 2016-01-01 --json
```

tooretrieve 모든 hello 리소스 태그 값으로 사용 합니다.

```azurecli
azure resource list -t Dept=Finance --json
```

tooretrieve 태그 값을 가진 모든 hello 리소스 그룹을 사용 합니다.

```azurecli
azure group list -t Dept=Finance
```

다음 명령을 hello로 구독에 기존 태그 hello를 볼 수 있습니다.

```azurecli
azure tag list
```
