<span data-ttu-id="2f3f5-101">[az webapp create](/cli/azure/webapp#create) 명령을 사용하여 `myAppServicePlan` App Service 계획에 [웹앱](../articles/app-service-web/app-service-web-overview.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2f3f5-101">Create a [web app](../articles/app-service-web/app-service-web-overview.md) in the `myAppServicePlan` App Service plan with the [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="2f3f5-102">웹앱은 코드에 대한 호스팅 공간을 제공하고, 배포된 앱을 확인하도록 URL을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2f3f5-102">The web app provides a hosting space for your code and provides a URL to view the deployed app.</span></span>

<span data-ttu-id="2f3f5-103">다음 명령에서 *\<app_name>*을 고유한 이름으로 바꿉니다(유효한 문자는 `a-z`, `0-9` 및 `-`).</span><span class="sxs-lookup"><span data-stu-id="2f3f5-103">In the following command, replace *\<app_name>* with a unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="2f3f5-104">`<app_name>`이 고유하지 않으면 "지정된 이름이 <app_name>인 웹 사이트가 이미 있습니다."라는 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f3f5-104">If `<app_name>` is not unique, you get the error message "Website with given name <app_name> already exists."</span></span> <span data-ttu-id="2f3f5-105">웹앱의 기본 URL은 `https://<app_name>.azurewebsites.net`입니다.</span><span class="sxs-lookup"><span data-stu-id="2f3f5-105">The default URL of the web app is `https://<app_name>.azurewebsites.net`.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="2f3f5-106">웹앱을 만들었으면 Azure CLI는 다음 예와 비슷한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2f3f5-106">When the web app has been created, the Azure CLI shows information similar to the following example:</span></span>

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

<span data-ttu-id="2f3f5-107">사이트로 이동하여 새로 만든 웹앱을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="2f3f5-107">Browse to the site to see your newly created web app.</span></span>

```bash
http://<app_name>.azurewebsites.net
```
