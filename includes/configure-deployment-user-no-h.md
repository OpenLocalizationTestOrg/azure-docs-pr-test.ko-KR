<span data-ttu-id="5046c-101">Hello로 배포 자격 증명을 만들어 [az webapp 배포 사용자 집합](/cli/azure/webapp/deployment/user#set) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="5046c-101">Create deployment credentials with hello [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) command.</span></span>

<span data-ttu-id="5046c-102">배포 사용자가 FTP 및 로컬 Git 배포 tooa 웹 앱 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5046c-102">A deployment user is required for FTP and local Git deployment tooa web app.</span></span> <span data-ttu-id="5046c-103">hello 사용자 이름 및 암호는 계정 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="5046c-103">hello user name and password are account level.</span></span> <span data-ttu-id="5046c-104">_Azure 구독 자격 증명과 다릅니다._</span><span class="sxs-lookup"><span data-stu-id="5046c-104">_They are different from your Azure subscription credentials._</span></span>

<span data-ttu-id="5046c-105">Hello에서 다음 명령을, 대체  *\<사용자 이름 >* 및  *\<암호 >* 새 사용자 이름 및 암호.</span><span class="sxs-lookup"><span data-stu-id="5046c-105">In hello following command, replace *\<user-name>* and *\<password>* with a new user name and password.</span></span> <span data-ttu-id="5046c-106">hello 사용자 이름은 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5046c-106">hello user name must be unique.</span></span> <span data-ttu-id="5046c-107">hello 암호 최소 8 자 이어야, hello 세 요소 다음의 두 개의: 문자, 숫자, 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="5046c-107">hello password must be at least eight characters long, with two of hello following three elements: letters, numbers, symbols.</span></span> 

```azurecli-interactive
az webapp deployment user set --user-name <username> --password <password>
```

<span data-ttu-id="5046c-108">발생 하는 경우는 ` 'Conflict'. Details: 409` 오류, hello 사용자 이름을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="5046c-108">If you get a ` 'Conflict'. Details: 409` error, change hello username.</span></span> <span data-ttu-id="5046c-109">` 'Bad Request'. Details: 400` 오류가 발생하면 더 강력한 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5046c-109">If you get a ` 'Bad Request'. Details: 400` error, use a stronger password.</span></span>

<span data-ttu-id="5046c-110">이 배포 사용자는 한 번만 만들며, 모든 Azure 배포에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5046c-110">You create this deployment user only once; you can use it for all your Azure deployments.</span></span>

> [!NOTE]
> <span data-ttu-id="5046c-111">레코드 hello 사용자 이름 및 암호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5046c-111">Record hello user name and password.</span></span> <span data-ttu-id="5046c-112">원하는 toodeploy hello 웹 앱 나중입니다.</span><span class="sxs-lookup"><span data-stu-id="5046c-112">You need them toodeploy hello web app later.</span></span>
>
>