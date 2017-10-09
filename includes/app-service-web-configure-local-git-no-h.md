<span data-ttu-id="9c3bf-101">로컬 Git 배포 toohello 웹 응용 프로그램 구성 hello로 [az webapp 배포 소스-config-로컬-git](/cli/azure/webapp/deployment/source#config-local-git) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="9c3bf-101">Configure local Git deployment toohello web app with hello [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command.</span></span>

<span data-ttu-id="9c3bf-102">응용 프로그램 서비스는 여러 가지 방법으로 toodeploy 콘텐츠 tooa 웹 앱, FTP, 로컬 Git, GitHub, Visual Studio Team Services 및 Bitbucket 등을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9c3bf-102">App Service supports several ways toodeploy content tooa web app, such as FTP, local Git, GitHub, Visual Studio Team Services, and Bitbucket.</span></span> <span data-ttu-id="9c3bf-103">이 빠른 시작을 위해 로컬 Git을 사용하여 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="9c3bf-103">For this quickstart, you deploy by using local Git.</span></span> <span data-ttu-id="9c3bf-104">즉, Azure에서 로컬 리포지토리 tooa 저장소에서 Git 명령을 toopush를 사용 하 여 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c3bf-104">That means you deploy by using a Git command toopush from a local repository tooa repository in Azure.</span></span> 

<span data-ttu-id="9c3bf-105">Hello에서 다음 명령을, 대체  *\<app_name >* 웹 앱의 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c3bf-105">In hello following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="9c3bf-106">hello 출력 형식에 따라 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c3bf-106">hello output has hello following format:</span></span>

```bash
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git
```

<span data-ttu-id="9c3bf-107">hello `<username>` 는 hello [배포 사용자](#configure-a-deployment-user) 이전 단계에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c3bf-107">hello `<username>` is hello [deployment user](#configure-a-deployment-user) that you created in a previous step.</span></span>

<span data-ttu-id="9c3bf-108">Hello 표시; URI 복사 hello 다음 단계에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c3bf-108">Copy hello URI shown; you'll use it in hello next step.</span></span>
