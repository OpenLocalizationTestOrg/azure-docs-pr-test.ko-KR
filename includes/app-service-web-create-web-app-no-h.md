<span data-ttu-id="08589-101">만들기는 [웹 앱](../articles/app-service-web/app-service-web-overview.md) hello에 `myAppServicePlan` hello로 앱 서비스 계획 [az webapp 만들](/cli/azure/webapp#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="08589-101">Create a [web app](../articles/app-service-web/app-service-web-overview.md) in hello `myAppServicePlan` App Service plan with hello [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="08589-102">hello 웹 응용 프로그램 코드에 대 한 호스팅 공간을 제공 하 고 URL tooview hello 배포 응용 프로그램을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="08589-102">hello web app provides a hosting space for your code and provides a URL tooview hello deployed app.</span></span>

<span data-ttu-id="08589-103">Hello에서 다음 명령을, 대체  *\<app_name >* 고유 이름으로 (유효한 문자는 `a-z`, `0-9`, 및 `-`).</span><span class="sxs-lookup"><span data-stu-id="08589-103">In hello following command, replace *\<app_name>* with a unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="08589-104">경우 `<app_name>` 가 고유 하지 않은 오류 메시지가 표시 hello "< app_name > 지정 된 이름의 웹 사이트 이미 있습니다."</span><span class="sxs-lookup"><span data-stu-id="08589-104">If `<app_name>` is not unique, you get hello error message "Website with given name <app_name> already exists."</span></span> <span data-ttu-id="08589-105">hello 웹 앱의 URL은 기본 hello `https://<app_name>.azurewebsites.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="08589-105">hello default URL of hello web app is `https://<app_name>.azurewebsites.net`.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="08589-106">Hello 웹 응용 프로그램을 만들면 Azure CLI hello 정보 비슷한 toohello를 다음 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="08589-106">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "<app_name>.azurewebsites.net",
    "<app_name>.scm.azurewebsites.net"
  ],
  "gatewaySiteName": null,
  "hostNameSslStates": [
    {
      "hostType": "Standard",
      "name": "<app_name>.azurewebsites.net",
      "sslState": "Disabled",
      "thumbprint": null,
      "toUpdate": null,
      "virtualIp": null
    }
    < JSON data removed for brevity. >
}
```

<span data-ttu-id="08589-107">Toohello 사이트 toosee 새로 만든된 웹 응용 프로그램을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="08589-107">Browse toohello site toosee your newly created web app.</span></span>

```bash
http://<app_name>.azurewebsites.net
```
