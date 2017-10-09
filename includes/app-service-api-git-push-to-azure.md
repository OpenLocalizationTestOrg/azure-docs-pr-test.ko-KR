<span data-ttu-id="100ff-101">API 앱에 대 한 hello Azure CLI tooget hello 원격 배포 URL을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="100ff-101">Use hello Azure CLI tooget hello remote deployment URL for your API App.</span></span> <span data-ttu-id="100ff-102">Hello에서 다음 명령을, 대체  *\<app_name >* 웹 앱의 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="100ff-102">In hello following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="100ff-103">사용자 로컬 Git 배포 toobe 수 toopush toohello 원격를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="100ff-103">Configure your local Git deployment toobe able toopush toohello remote.</span></span>

```bash
git remote add azure <URI from previous step>
```

<span data-ttu-id="100ff-104">Azure 원격 toodeploy toohello 응용 프로그램을 푸시하십시오.</span><span class="sxs-lookup"><span data-stu-id="100ff-104">Push toohello Azure remote toodeploy your app.</span></span> <span data-ttu-id="100ff-105">Hello 배포 사용자를 만들 때 앞에서 만든 hello 암호를 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="100ff-105">You are prompted for hello password you created earlier when you created hello deployment user.</span></span> <span data-ttu-id="100ff-106">Hello 퀵 스타트 앞부분에서에서 만든 hello 암호 및 toolog toohello Azure 포털에서에서 사용 하 여 hello 암호가 하지 않은 경우을 입력 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="100ff-106">Make sure that you enter hello password you created in earlier in hello quickstart, and not hello password you use toolog in toohello Azure portal.</span></span>

```bash
git push azure master
```
