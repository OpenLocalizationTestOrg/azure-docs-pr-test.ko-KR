<span data-ttu-id="f8cb8-101">[az login](/cli/azure/#login) 명령으로 Azure 구독에 로그인하고 화면의 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-101">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> <span data-ttu-id="f8cb8-102">로그인에 대한 자세한 내용은 [Azure CLI 2.0 시작](/cli/azure/get-started-with-azure-cli)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-102">For more information about logging in, see [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

```azurecli
az login
```

<span data-ttu-id="f8cb8-103">Azure 구독이 두 개 이상인 경우 계정의 구독을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-103">If you have more than one Azure subscription, list the subscriptions for the account.</span></span>

```azurecli
az account list --all
```

<span data-ttu-id="f8cb8-104">사용할 구독을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-104">Specify the subscription that you want to use.</span></span>

```azurecli
az account set --subscription <replace_with_your_subscription_id>
```