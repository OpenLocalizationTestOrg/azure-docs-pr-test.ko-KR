---
title: "aaaAdd 사용자 지정 도메인 및 SSL tooan Azure 웹 앱 | Microsoft Docs"
description: "어떻게 tooprepare Azure 웹 앱 toogo 프로덕션 내용을 회사 브랜딩 추가 하 여에 대해 알아봅니다. Hello 사용자 지정 도메인 이름 (베 니 티 도메인) tooyour 웹 앱을 매핑한 사용자 지정 SSL 인증서를 사용 하 여 보안 합니다."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 03/29/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2679ed8b2dbbeba0b128c1a3ec01148f97c35342
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-domain-and-ssl-tooan-azure-web-app"></a>사용자 지정 도메인 및 SSL tooan Azure 웹 앱 추가

이 자습서에는 tooquickly 매핑하는 사용자 지정 도메인 이름을 tooyour Azure 웹 앱 하 고 다음 사용자 지정 SSL 인증서를 사용 하 여 보안 하는 방법을 보여줍니다. 

## <a name="before-you-begin"></a>시작하기 전에

이 샘플을 실행 하기 전에 hello 설치 [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) 로컬로 합니다.

또한 각 도메인 공급자에 대 한 관리 액세스 toohello DNS 구성 페이지가 있어야 되었습니다. 예를 들어 tooadd `www.contoso.com`, toobe 수 tooconfigure DNS 항목에 대 한 필요한 `contoso.com`합니다.

마지막으로, 유효한 필요합니다. PFX 파일 _및_ tooupload 원하는 hello SSL 인증서에 대 한 암호 바인딩합니다. 이 SSL 인증서에는 원하는 구성된 toosecure hello 사용자 지정 도메인 이름 이어야 합니다. 위 예제는 hello에서 SSL 인증서를 보호 해야 `www.contoso.com`합니다. 

## <a name="step-1---create-an-azure-web-app"></a>1단계 - Azure 웹앱 만들기

### <a name="log-in-tooazure"></a>TooAzure 로그인

진행 중인 toouse hello Azure CLI 2.0 터미널 윈도우 toocreate hello 리소스에서 필요한 toohost Azure에서 Node.js 앱 이제는입니다.  Tooyour hello로 Azure 구독에에서 로그인 [az 로그인](/cli/azure/#login) 명령 열고 지시를 따른 hello 화면에 표시 합니다. 

```azurecli 
az login 
``` 
   
### <a name="create-a-resource-group"></a>리소스 그룹 만들기   
Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create)합니다. Azure 리소스 그룹은 웹앱, 데이터베이스, 저장소 계정이 관리되었는지 등 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다. 

```azurecli
az group create --name myResourceGroup --location westeurope 
```

toosee에 사용할 수 있는 가능한 값은 있습니다 `---location`, hello를 사용 하 여 `az appservice list-locations` Azure CLI 명령입니다.

## <a name="create-an-app-service-plan"></a>App Service 계획 만들기

Hello로 앱 서비스 계획 만들기 [az 앱 서비스 계획 만들기](/cli/azure/appservice/plan#create) 명령입니다. 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

hello 다음 예제에서는 명명 된 앱 서비스 계획 `myAppServicePlan` hello를 사용 하 여 **기본** 가격 책정 계층입니다.

az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1

Hello 앱 서비스 계획을 만든 hello Azure CLI 정보 비슷한 toohello 다음 예제에 표시 됩니다. 

```json 
{ 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "kind": "app", 
    "location": "West Europe", 
    "sku": { 
    "capacity": 1, 
    "family": "B", 
    "name": "B1", 
    "tier": "Basic" 
    }, 
    "status": "Ready", 
    "type": "Microsoft.Web/serverfarms" 
} 
``` 

## <a name="create-a-web-app"></a>웹앱 만들기

앱 서비스 계획을 만든 했으므로 hello 내에서 웹 응용 프로그램을 만들 `myAppServicePlan` 앱 서비스 계획 합니다. 호스팅 공간 toodeploy 코드 하는 것은 물론 있습니다 자동으로 제공 하는 URL tooview hello hello 웹 응용 프로그램은 응용 프로그램을 배포 합니다. 사용 하 여 hello [az 앱 서비스 웹 만들](/cli/azure/appservice/web#create) 명령 toocreate hello 웹 앱입니다. 

Hello 명령 아래에 hello 나타나는 자신의 고유한 응용 프로그램 이름으로 대체 하세요 `<app_name>` 자리 표시자입니다. 이 고유 이름이 hello 이름 해야 toobe 고유 Azure에서 모든 앱 간에 hello 웹 앱에 대 한 기본 도메인 이름 hello의 hello 일부로 사용 됩니다. 나중에 tooyour 사용자 노출 먼저 모든 사용자 지정 DNS 항목 toohello 웹 앱을 매핑할 수 있습니다. 

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan 
```

Hello 웹 응용 프로그램을 만든 hello Azure CLI 정보 비슷한 toohello 다음 예제에 표시 됩니다. 

```json 
{ 
    "clientAffinityEnabled": true, 
    "defaultHostName": "<app_name>.azurewebsites.net", 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/sites/<app_name>", 
    "isDefaultContainer": null, 
    "kind": "app", 
    "location": "West Europe", 
    "name": "<app_name>", 
    "repositorySiteName": "<app_name>", 
    "reserved": true, 
    "resourceGroup": "myResourceGroup", 
    "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "state": "Running", 
    "type": "Microsoft.Web/sites", 
} 
```

Hello JSON 출력에서에서 `defaultHostName` 웹 앱의 기본 도메인 이름을 표시 합니다. 브라우저에서 toothis 주소를 이동 합니다.

```
http://<app_name>.azurewebsites.net 
``` 
 
![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-created.png)  

## <a name="step-2---configure-dns-mapping"></a>2단계 - DNS 매핑 구성

이 단계에서는 사용자 지정 도메인 tooyour 웹 앱의 기본 도메인 이름에서 매핑을 추가 `<app_name>.azurewebsites.net`합니다. 일반적으로 도메인 공급자의 웹 사이트에서 이 단계를 수행 합니다. 각 도메인 등록 기관의 웹 사이트는 약간씩 다르므로 공급자의 설명서를 참조해야 합니다. 하지만 다음은 몇 가지 일반적인 지침입니다. 

### <a name="navigate-tootoodns-management-page"></a>TootooDNS 관리 페이지로 이동

첫째, tooyour 도메인 등록 기관의 웹 사이트에 로그인 합니다.  

그런 다음 DNS 레코드를 관리 하기 위한 hello 페이지를 찾을 합니다. 링크 또는 레이블이 지정 된 hello 사이트의 영역을 찾고 **도메인 이름**, **DNS**, 또는 **이름 서버 관리**합니다. 종종, 계정 정보를 표시 하 고 다음 찾고 링크와 같은 여 hello 링크를 찾을 수 있습니다 **내 도메인**합니다.

이 페이지를 찾았으면 DNS 레코드를 추가하거나 편집할 수 있는 링크를 찾습니다. 이는 **영역 파일** 또는 **DNS 레코드** 링크이거나 **고급 구성** 링크일 수 있습니다.

### <a name="create-a-cname-record"></a>CNAME 레코드 만들기

Hello 원하는 하위 도메인 이름 tooyour 웹 응용 프로그램의 기본 도메인 이름을 매핑하는 CNAME 레코드 추가 (`<app_name>.azurewebsites.net`여기서 `<app_name>` 응용 프로그램의 고유 이름입니다).

Hello에 대 한 `www.contoso.com` hello에 매핑하는 CNAME을 만들어야 예제에서는 `www` hostname 너무`<app_name>.azurewebsites.net`합니다.

## <a name="step-3---configure-hello-custom-domain-on-your-web-app"></a>3 단계-웹 응용 프로그램에서 hello 사용자 지정 도메인 구성

작업을 마치면 hello 호스트 이름 매핑 도메인 공급자의 웹 사이트에서 구성 하 고 준비 tooconfigure hello에 대 한 사용자 지정 도메인 웹 앱입니다. 사용 하 여 hello [az 앱 서비스 웹 구성 호스트 이름 추가](/cli/azure/appservice/web/config/hostname#add) tooadd이이 구성을 명령입니다. 

아래 hello 명령을 대체할 하십시오 `<app_name>` 고유한 응용 프로그램 이름 및 < your_custom_domain > hello 정규화 된 사용자 지정 도메인 이름으로 (예: `www.contoso.com`). 

```azurecli
az appservice web config hostname add --webapp <app_name> --resource-group myResourceGroup --name <your_custom_domain>
```

hello 사용자 지정 도메인에는 이제 완벽 하 게 매핑된 tooyour 웹 앱입니다. 브라우저에서 toohello 사용자 지정 도메인 이름을 이동 합니다. 예:

```
http://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-custom-domain.png)  

## <a name="step-4---bind-a-custom-ssl-certificate-tooyour-web-app"></a>4 단계-바인딩 사용자 지정 SSL 인증서 tooyour 웹 앱

Hello 브라우저의 주소 표시줄에 원하는 hello 도메인 이름 사용 하 여 Azure 웹 앱을 만들었습니다. 그러나 toohello 이동 하는 경우 `https://<your_custom_domain>` 이제 인증서 오류가 발생 합니다. 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-cert-error.png)  

이 오류는 웹앱에 사용자 지정 도메인 이름과 일치하는 SSL 인증서 바인딩 아직 없기 때문에 발생합니다. 너무 이동 하는 경우 오류가 발생 하지 않는 반면`https://<app_name>.azurewebsites.net`합니다. 응용 프로그램 뿐 아니라 모든 Azure 앱 서비스 앱 hello에 대 한 hello SSL 인증서로 보호 되 때문에 이것이 `*.azurewebsites.net` 기본적으로 와일드 카드 도메인입니다. 

tooaccess 웹 앱 사용자 지정 도메인 이름을 주문, 사용자 지정 도메인 toohello 웹 앱에 대 한 toobind hello SSL 인증서를 필요 합니다. 바로 이 단계에서 수행합니다. 

### <a name="upload-hello-ssl-certificate"></a>Hello SSL 인증서를 업로드 합니다.

Hello를 사용 하 여 사용자 지정 도메인 tooyour 웹 앱에 대 한 hello SSL 인증서를 업로드 [az 앱 서비스 웹 구성 ssl 업로드](/cli/azure/appservice/web/config/ssl#upload) 명령입니다.

아래 hello 명령을 대체할 하십시오 `<app_name>` 을 고유한 응용 프로그램 이름으로, `<path_to_ptx_file>` hello 경로 tooyour 사용 합니다. PFX 파일 및 `<password>` 인증서의 암호를 사용 합니다. 

```azurecli
az appservice web config ssl upload --name <app_name> --resource-group myResourceGroup --certificate-file <path_to_pfx_file> --certificate-password <password> 
```

Hello 인증서 업로드 되 면 hello Azure CLI 정보 비슷한 toohello를 다음 예제를 보여 줍니다.

```json
{
  "cerBlob": null,
  "expirationDate": "2018-03-29T14:12:57+00:00",
  "friendlyName": "",
  "hostNames": [
    "www.contoso.com"
  ],
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/cert
ificates/9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "issueDate": "2017-03-29T14:12:57+00:00",
  "issuer": "www.contoso.com",
  "keyVaultId": null,
  "keyVaultSecretName": null,
  "keyVaultSecretStatus": "Initialized",
  "kind": null,
  "location": "West Europe",
  "name": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "password": null,
 "pfxBlob": null,
  "publicKeyHash": null,
  "resourceGroup": "myResourceGroup",
  "selfLink": null,
  "serverFarmId": null,
  "siteName": null,
  "subjectName": "www.contoso.com",
  "tags": null,
  "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00",
  "type": "Microsoft.Web/certificates",
  "valid": null
}
```

Hello JSON 출력에서에서 `thumbprint` 업로드 된 인증서의 지문을 표시 합니다. Hello 다음 단계에 대 한 해당 값을 복사 합니다.

### <a name="bind-hello-uploaded-ssl-certificate-toohello-web-app"></a>Toohello 웹 응용 프로그램 업로드 hello SSL 인증서 바인딩

이제 웹 앱 원하는 hello 사용자 지정 도메인 이름을 있으며 해당 사용자 지정 도메인을 보호 하는 한 SSL 인증서가 있습니다. hello 것만 왼쪽된 toodo toobind hello 인증서를 업로드 toohello 웹 앱입니다. Hello를 사용 하 여이 작업을 수행 [az 앱 서비스 웹 구성 ssl 바인딩을](/cli/azure/appservice/web/config/ssl#bind) 명령입니다.

아래 hello 명령을 대체할 하십시오 `<app_name>` 을 고유한 응용 프로그램 이름 및 `<thumbprint-from-previous-output>` hello 이전 명령에서 얻을 수 있는 hello 인증서 지 문으로 합니다. 

az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI

Hello 인증서가 바인딩된 tooyour 웹 응용 프로그램, 다음 예제에서는 정보 비슷한 toohello를 hello Azure CLI로 표시 됩니다.

{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }

브라우저에서 사용자 지정 도메인 이름의 tooHTTPS 끝점을 이동 합니다. 예:

```
https://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-ssl-success.png)  

## <a name="more-resources"></a>추가 리소스

[Azure App Service에서 사용자 지정 도메인 이름 구입 및 구성](custom-dns-web-site-buydomains-web-app.md)
[Azure App Service에 대한 SSL 인증서 구입 및 구성](web-sites-purchase-ssl-web-site.md)
