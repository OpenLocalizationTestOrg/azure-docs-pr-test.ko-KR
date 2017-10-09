
만들기는 [API 앱](../articles/app-service-api/app-service-api-apps-why-best-platform.md) hello에 `myAppServicePlan` hello로 앱 서비스 계획 [az webapp 만들](/cli/azure/appservice/web#create) 명령입니다. 

hello 웹 응용 프로그램 API에 대 한 호스팅 공간을 제공 하 고 URL tooview hello 배포 응용 프로그램을 제공 합니다.

Hello에서 다음 명령을, 대체  *\<app_name >* 고유한 이름을 사용 합니다. 경우 `<app_name>` 가 고유 하지 않은 오류 메시지가 표시 hello "< app_name > 지정 된 이름의 웹 사이트 이미 있습니다." hello 웹 앱의 URL은 기본 hello `https://<app_name>.azurewebsites.net`합니다. 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

Hello 웹 응용 프로그램을 만들면 Azure CLI hello 정보 비슷한 toohello를 다음 예제를 보여 줍니다.

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