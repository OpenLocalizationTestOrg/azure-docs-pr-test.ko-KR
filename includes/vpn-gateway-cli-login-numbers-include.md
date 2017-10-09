1. <span data-ttu-id="9b157-101">Tooyour hello로 Azure 구독에에서 로그인 [az 로그인](/cli/azure/#login) 명령 열고 지시를 따른 hello 화면에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b157-101">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> <span data-ttu-id="9b157-102">로그인에 대한 자세한 내용은 [Azure CLI 2.0 시작](/cli/azure/get-started-with-azure-cli)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9b157-102">For more information about logging in, see [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

  ```azurecli
  az login
  ```
2. <span data-ttu-id="9b157-103">Azure 구독이 여러 개 있는 경우 hello 계정에 대 한 hello 구독을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b157-103">If you have more than one Azure subscription, list hello subscriptions for hello account.</span></span>

  ```azurecli
  az account list --all
  ```
3. <span data-ttu-id="9b157-104">Toouse hello 구독을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b157-104">Specify hello subscription that you want toouse.</span></span>

  ```azurecli
  az account set --subscription <replace_with_your_subscription_id>
  ```