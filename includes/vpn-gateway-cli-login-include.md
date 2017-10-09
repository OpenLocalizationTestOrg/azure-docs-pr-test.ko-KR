Tooyour hello로 Azure 구독에에서 로그인 [az 로그인](/cli/azure/#login) 명령 열고 지시를 따른 hello 화면에 표시 합니다. 로그인에 대한 자세한 내용은 [Azure CLI 2.0 시작](/cli/azure/get-started-with-azure-cli)을 참조하세요.

```azurecli
az login
```

Azure 구독이 여러 개 있는 경우 hello 계정에 대 한 hello 구독을 나열 합니다.

```azurecli
az account list --all
```

Toouse hello 구독을 지정 합니다.

```azurecli
az account set --subscription <replace_with_your_subscription_id>
```