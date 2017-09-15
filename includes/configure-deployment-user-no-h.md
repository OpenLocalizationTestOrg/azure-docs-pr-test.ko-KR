<span data-ttu-id="b1fda-101">[az webapp deployment user set](/cli/azure/webapp/deployment/user#set) 명령을 사용하여 배포 자격 증명을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1fda-101">Create deployment credentials with the [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) command.</span></span>

<span data-ttu-id="b1fda-102">배포 사용자는 웹앱에 대한 FTP 및 로컬 Git 배포에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b1fda-102">A deployment user is required for FTP and local Git deployment to a web app.</span></span> <span data-ttu-id="b1fda-103">사용자 이름과 암호는 계정 수준이며,</span><span class="sxs-lookup"><span data-stu-id="b1fda-103">The user name and password are account level.</span></span> <span data-ttu-id="b1fda-104">_Azure 구독 자격 증명과 다릅니다._</span><span class="sxs-lookup"><span data-stu-id="b1fda-104">_They are different from your Azure subscription credentials._</span></span>

<span data-ttu-id="b1fda-105">다음 명령에서 *\<사용자 이름>* 및 *\<암호>*를 새 사용자 이름 및 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b1fda-105">In the following command, replace *\<user-name>* and *\<password>* with a new user name and password.</span></span> <span data-ttu-id="b1fda-106">사용자 이름은 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1fda-106">The user name must be unique.</span></span> <span data-ttu-id="b1fda-107">암호는 글자, 숫자, 기호와 같은 세 가지 요소 중 두 가지를 포함하여 8자 이상이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1fda-107">The password must be at least eight characters long, with two of the following three elements: letters, numbers, symbols.</span></span> 

```azurecli-interactive
az webapp deployment user set --user-name <username> --password <password>
```

<span data-ttu-id="b1fda-108">` 'Conflict'. Details: 409` 오류가 발생하면 사용자 이름을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b1fda-108">If you get a ` 'Conflict'. Details: 409` error, change the username.</span></span> <span data-ttu-id="b1fda-109">` 'Bad Request'. Details: 400` 오류가 발생하면 더 강력한 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b1fda-109">If you get a ` 'Bad Request'. Details: 400` error, use a stronger password.</span></span>

<span data-ttu-id="b1fda-110">이 배포 사용자는 한 번만 만들며, 모든 Azure 배포에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1fda-110">You create this deployment user only once; you can use it for all your Azure deployments.</span></span>

> [!NOTE]
> <span data-ttu-id="b1fda-111">사용자 이름과 암호는 나중에 웹앱을 배포하는 데 필요하므로</span><span class="sxs-lookup"><span data-stu-id="b1fda-111">Record the user name and password.</span></span> <span data-ttu-id="b1fda-112">기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="b1fda-112">You need them to deploy the web app later.</span></span>
>
>