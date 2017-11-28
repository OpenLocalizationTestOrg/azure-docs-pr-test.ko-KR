<span data-ttu-id="6bcf6-101">[az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) 명령을 사용하여 웹앱에 로컬 Git 배포를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6bcf6-101">Configure local Git deployment to the web app with the [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command.</span></span>

<span data-ttu-id="6bcf6-102">App Service는 FTP, 로컬 Git, GitHub, Visual Studio Team Services, Bitbucket 등의 웹앱에 콘텐츠를 배포하는 여러 방법을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6bcf6-102">App Service supports several ways to deploy content to a web app, such as FTP, local Git, GitHub, Visual Studio Team Services, and Bitbucket.</span></span> <span data-ttu-id="6bcf6-103">이 빠른 시작을 위해 로컬 Git을 사용하여 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="6bcf6-103">For this quickstart, you deploy by using local Git.</span></span> <span data-ttu-id="6bcf6-104">즉, 로컬 리포지토리에서 Azure의 리포지토리로 푸시하기 위해 Git 명령을 사용하여 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="6bcf6-104">That means you deploy by using a Git command to push from a local repository to a repository in Azure.</span></span> 

<span data-ttu-id="6bcf6-105">다음 명령에서 *\<app_name>*을 웹앱의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6bcf6-105">In the following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="6bcf6-106">출력 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6bcf6-106">The output has the following format:</span></span>

```bash
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git
```

<span data-ttu-id="6bcf6-107">`<username>`은 이전 단계에서 만든 [배포 사용자](#configure-a-deployment-user)입니다.</span><span class="sxs-lookup"><span data-stu-id="6bcf6-107">The `<username>` is the [deployment user](#configure-a-deployment-user) that you created in a previous step.</span></span>

<span data-ttu-id="6bcf6-108">다음 단계에서 사용하므로 표시된 URI를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6bcf6-108">Copy the URI shown; you'll use it in the next step.</span></span>
