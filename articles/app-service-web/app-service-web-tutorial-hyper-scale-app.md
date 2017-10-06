---
title: "Azure에서 대규모 앱 aaaBuild | Microsoft Docs"
description: "Toouse 서로 다른 Azure 서비스 toomaximize Azure에서 ASP.NET 응용 프로그램의 성능을 hello 하는 방법에 대해 알아봅니다."
services: app-service\web
documentationcenter: dotnet
author: cephalin
manager: erikre
editor: 
ms.assetid: a4d49ac7-0f97-4997-84c5-cdb9c4465757
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 03/23/2017
ms.author: cephalin
ms.openlocfilehash: 7952647b49a82c286c6a737eb41a7f23a13fd75e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-hyper-scale-web-app-in-azure"></a>Azure에서 초대형 웹앱 빌드

이 자습서는 ASP.NET 웹 앱에 Azure toomaximize 사용자 아웃 tooscale 요청 하는 방법을 보여 줍니다.

이 자습서를 시작 하기 전에 확인 하는 [hello Azure CLI가 설치 되어](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) 컴퓨터에 있습니다. 또한 필요 [Visual Studio](https://www.visualstudio.com/vs/) 로컬 컴퓨터 toorun hello 예제 응용 프로그램에 있습니다.

## <a name="step-1---get-sample-application"></a>1단계 - 샘플 응용 프로그램 가져오기
이 단계에서는 hello 로컬 ASP.NET 프로젝트를 설정 합니다.

### <a name="clone-hello-application-repository"></a>복제 hello 응용 프로그램 저장소

사용자가 선택한 열려 hello 명령줄 터미널 및 `CD` tooa 작업 디렉터리입니다. 그런 다음 실행된 hello 다음 tooclone hello 샘플 응용 프로그램을 명령입니다. 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-hello-sample-application-in-visual-studio"></a>Visual Studio에서 hello 샘플 응용 프로그램을 실행 합니다.

Visual Studio에서 hello 솔루션을 엽니다.

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

형식 `F5` toorun hello 응용 프로그램입니다.

이 샘플 ASP.NET 웹 응용 프로그램이 hello 기본 서식 파일에서 제공 하 고 사용자 세션 및 사용 하 여 hello 출력 캐시를 유지 합니다. `HighScaleApp\Controllers\HomeController.cs`에 대해 살펴보겠습니다. hello `Index()` 데이터 toohello 세션의 일부 메서드를 추가 합니다.

```csharp
Session.Add("visited", "true"); 
```

Hello 및 `About()` 및 `Contact()` 메서드 출력을 캐시 합니다.

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-tooazure"></a>2 단계-tooAzure 배포
이 단계에서는 Azure 웹 앱 만들고 샘플 ASP.NET 응용 프로그램 tooit 프로그램을 배포 합니다.

### <a name="create-a-resource-group"></a>리소스 그룹 만들기   
사용 하 여 [az 그룹 만들기](https://docs.microsoft.com/cli/azure/group#create) toocreate는 [리소스 그룹](../azure-resource-manager/resource-group-overview.md) hello 서 부 유럽 지역에 있습니다. 리소스 그룹은 모든 정상 상태로 있는 백 엔드 hello 웹 앱 및 모든 SQL 데이터베이스와 같은 Azure 리소스 toomanage 함께 되도록 hello 합니다.

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

toosee에 사용할 수 있는 가능한 값은 있습니다 `---location`, hello를 사용 하 여 [위치 나열 az appservice](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) 명령입니다.

### <a name="create-an-app-service-plan"></a>App Service 계획 만들기
사용 하 여 [az 앱 서비스 계획 만들기](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) toocreate "B1" [앱 서비스 계획](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)합니다. 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

앱 서비스 계획은 배율 단위를 tooscale 원하는 또는 함께 over 아웃 동일를 환영 하는 앱을 개수에 관계 없이 포함할 수 있는 응용 프로그램 서비스 인프라입니다. 또한 각 계획은 [가격 책정 계층](https://azure.microsoft.com/en-us/pricing/details/app-service/)에 할당되어 있습니다. 더 높은 계층은 더 많은 규모 확장 인스턴스와 같이 더 향상된 하드웨어와 더 많은 기능을 포함합니다.

이 자습서에 대 한 b 1은 toothree 인스턴스 확장을 사용 하도록 설정 하는 hello 최소 계층입니다. 위로 또는 아래로 hello 가격대 나중에 실행 하 여 항상 응용 프로그램을 이동할 수 있습니다 [az 앱 서비스 계획 업데이트](https://docs.microsoft.com/cli/azure/appservice/plan#update)합니다. 

### <a name="create-a-web-app"></a>웹앱 만들기
사용 하 여 [az 앱 서비스 웹 만들](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate 고유한 이름의 웹 응용 프로그램에서 `$appName`합니다.

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a>배포 자격 증명 설정
사용 하 여 [az 앱 서비스 웹 설정 된 배포 사용자](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) tooset 응용 프로그램 서비스에 대 한 자격 증명을 계정 수준 배포입니다.

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a>Git 배포 구성
사용 하 여 [az 앱 서비스 웹 소스 제어-config-로컬-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure 로컬 Git 배포 합니다.

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

이 명령은 hello 다음과 같은 출력을 제공 합니다.

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

사용 하 여 hello 반환 URL tooconfigure 프로그램 Git 원격. hello 다음 명령을 사용 하 여 hello 앞에 출력 예입니다.

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-hello-sample-application"></a>Hello 샘플 응용 프로그램 배포
사용자는 이제 준비 toodeploy 샘플 응용 프로그램입니다. `git push`을 실행합니다.

```powershell
git push azure master
```

암호에 대 한 메시지가 표시 되 면 hello 지정한 암호를 실행할 때 사용 하 여 `az appservice web deployment user set`합니다.

### <a name="browse-tooazure-web-app"></a>TooAzure 웹 응용 프로그램 찾아보기
사용 하 여 [az 앱 서비스 웹 찾아보기](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee Azure에서 동시에 실행 되는 앱이이 명령을 실행 합니다.

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-tooredis"></a>3 단계-tooRedis 연결
이 단계에서는 외부 공동 배치 된 캐시 tooyour Azure 웹 앱으로 Azure Redis Cache를 설정할 수 있습니다. 신속 하 게 페이지 출력 Redis toocache를 사용할 수 있습니다. 또한 나중에 웹앱의 규모를 확장할 때 Redis를 사용하면 사용자 세션을 여러 인스턴스에 걸쳐 안정적으로 유지할 수 있습니다.

### <a name="create-an-azure-redis-cache"></a>Azure Redis Cache 만들기
사용 하 여 [az redis 만들](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate Azure Redis 캐시 하 고 JSON 출력 hello 저장 합니다. `$cacheName`에 고유한 이름을 사용합니다.

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-hello-application-toouse-redis"></a>Hello 응용 프로그램 toouse Redis 구성
캐시에 대 한 hello 연결 문자열의 서식을 지정 합니다.

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

다음과 같은 출력 hello 두 번째 줄을 제공 해야 합니다.

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

Visual Studio에서 라는 프로젝트 루트에 웹 구성 파일을 만드는 `redis.config` 붙여넣기 hello에 코드를 다음 및 합니다. `value`, hello PowerShell 출력에서에서 hello 연결 문자열을 사용 합니다.

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

Hello 보면 `.gitignore` 파일에서 Git 리포지토리를 배웁니다이 파일이 소스 제어에서 제외 됩니다. 이런 방식으로 중요한 정보가 안전하게 유지됩니다. 

`Web.config`을(를) 엽니다. 공지 hello `<appSettings file="redis.config">` 요소에서 만든 hello 설정을 가져오는 `redis.config`합니다. 

Hello 주석 찾기 포함 된 섹션 `<sessionState>` 및 `<caching>`합니다. 이 섹션의 주석 처리를 제거합니다.

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

이 코드에서 찾는 hello Redis 연결 문자열에 정의한 `RedisConnection`합니다. 

이제 응용 프로그램에 Redis toomanage 세션 및 캐싱을 사용합니다. 형식 `F5` toorun hello 응용 프로그램입니다. 원하는 경우는 Redis 관리 클라이언트 toovisualize hello 저장 된 데이터는 이제 toohello 캐시를 다운로드할 수 있습니다.

### <a name="configure-hello-connection-string-in-azure"></a>Azure의 hello 연결 문자열을 구성 합니다.

Azure에서 응용 프로그램 toowork 프로그램, tooconfigure 필요 hello Azure 웹 앱에서 동일한 Redis 연결 문자열입니다. 이후 `redis.config` Git 배포를 실행 하는 경우 배포 된 tooAzure은 소스 제어에서 유지 되지 않습니다.

사용 하 여 [az 앱 서비스 웹 구성 appsettings 업데이트](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) hello로 tooadd hello 연결 문자열이 동일한 이름 (`RedisConnection`).

az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup

에 유의 해야 `$connstring` hello 서식이 지정 된 연결 문자열을 포함 합니다.

### <a name="redeploy-hello-application-tooazure"></a>응용 프로그램 tooAzure hello를 다시 배포
Git 명령 toopush 변경 tooAzure 사용

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

암호에 대 한 메시지가 표시 되 면 hello 지정한 암호를 실행할 때 사용 하 여 `az appservice web deployment user set`합니다.

### <a name="browse-toohello-azure-web-app"></a>Toohello Azure 웹 앱을 찾아보기
사용 하 여 [az 앱 서비스 웹 찾아보기](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee hello 변경 내용을 Azure에 거주 합니다.

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-toomultiple-instances"></a>4 단계-눈금 toomultiple 인스턴스
앱 서비스 계획 hello Azure 웹 앱에 대 한 hello 배율 단위입니다. 앱 서비스 계획 hello를 확장할 tooscale 웹 앱, 있습니다.

사용 하 여 [az 앱 서비스 계획 업데이트](https://docs.microsoft.com/cli/azure/appservice/plan#update) 는 hello 앱 서비스 계획 toothree 인스턴스 tooscale hello hello B1 가격 책정 계층에서 허용 되는 최대 수입니다. B1 가격 책정 계층 hello 이전 앱 서비스 계획을 만들 때 선택한 hello 임을 기억 합니다. 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a>5단계 - 지리적으로 크기 조정
지리적으로 크기 조정 하는 경우의 Azure 클라우드 hello 여러 지역에서 앱을 실행 합니다. 이 설치 프로그램 고 부하를 분산 추가로 지리를 기반으로 하는 응용 프로그램 응용 프로그램 자세히 tooclient 브라우저를 배치 하 여 hello 응답 시간을 낮춥니다.

이 단계에서는 해당 ASP.NET 웹 응용 프로그램 tooa 두 번째 지역으로 확장할 있습니다 [Azure 트래픽 관리자](https://docs.microsoft.com/en-us/azure/traffic-manager/)합니다. Hello 단계의 hello 끝 동남 아시아 (아직 만들어지지 않음)에서 실행 되는 웹 응용 프로그램와 웹 앱 (이미 만든)는 서 부 유럽에서 실행 해야 합니다. 두 앱 모두에서 제공 hello 트래픽 관리자 URL 동일 합니다.

### <a name="scale-up-hello-europe-app-toostandard-tier"></a>Hello 유럽 앱 tooStandard 계층 확장
앱 서비스에서 Azure 트래픽 관리자와의 통합 hello 표준 가격 책정 계층이 필요합니다. 사용 하 여 [az 앱 서비스 계획 업데이트](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale 앱 서비스 계획 tooS1 합니다. 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a>Traffic Manager 프로필 만들기 
사용 하 여 [az 네트워크 트래픽 관리자 프로필 만들기](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) toocreate 트래픽 관리자 프로필 및 tooyour 리소스 그룹을 추가 합니다. $dnsName에 고유한 DNS 이름을 사용합니다.

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> `--routing-method Performance`지정 하는이 프로필 [사용자 트래픽을 가장 가까운 끝점 toohello 라우팅합니다](../traffic-manager/traffic-manager-routing-methods.md)합니다.

### <a name="get-hello-resource-id-of-hello-europe-app"></a>Hello 유럽 응용 프로그램의 hello 리소스 ID 가져오기
사용 하 여 [az 앱 서비스 웹 쇼](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) 웹 앱의 tooget hello 리소스 ID입니다.

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-europe-app"></a>Hello 유럽 응용 프로그램에 대 한 트래픽 관리자 끝점 추가
사용 하 여 [az 네트워크 트래픽 관리자 끝점 만들기](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd 끝점 tooyour 트래픽 관리자 프로필 및 웹 응용 프로그램을 사용 하 여 hello 리소스 ID hello 대상입니다.

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-hello-traffic-manager-endpoint-url"></a>Hello 트래픽 관리자 끝점 URL 가져오기
트래픽 관리자 프로필에 끝점이 해당 지점 tooyour 기존 웹 앱 있습니다. 사용 하 여 [az 네트워크 트래픽 관리자 프로필 표시](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) tooget 해당 URL입니다. 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

Hello 출력 브라우저에 복사 합니다. 웹앱을 다시 확인해야 합니다.

### <a name="create-an-azure-redis-cache-in-asia"></a>아시아에 Azure Redis Cache 만들기
이제 Azure 웹 앱 toohello 동남 아시아 지역을 복제할 수 있습니다. toostart를 사용 하 여 [az redis 만들](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate 동남 아시아에 두 번째 Azure Redis 캐시 합니다. 이 캐시 toobe 아시아의 응용 프로그램과 함께 배치 해야 합니다.

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

`--name $cacheName-asia`제공 hello hello로 hello 서 부 유럽 캐시의 캐시 hello 이름을 `-asia` 접미사입니다.

### <a name="create-an-app-service-plan-in-asia"></a>아시아에 App Service 계획 만들기
사용 하 여 [az 앱 서비스 계획 만들기](https://docs.microsoft.com/cli/azure/appservice/plan#create) hello를 사용 하 여 hello 서 부 유럽 계획으로 계층 동일한 S1, 동남 아시아 지역의 hello toocreate 두 번째 응용 프로그램 서비스 계획 합니다.

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a>아시아에 웹앱 만들기
사용 하 여 [az 앱 서비스 웹 만들](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate 두 번째 웹 응용 프로그램입니다.

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

`--name $appName-asia`제공 hello로 hello 서 부 유럽 응용 프로그램의 응용 프로그램 hello 이름 hello `-asia` 접미사입니다.

### <a name="configure-hello-connection-string-for-redis"></a>Redis 용 hello 연결 문자열을 구성 합니다.
사용 하 여 [az 앱 서비스 웹 구성 appsettings 업데이트](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd toohello 웹 응용 프로그램 hello 연결에 대 한 문자열 hello 동남 아시아 캐시 합니다.

az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup

### <a name="configure-git-deployment-for-hello-asia-app"></a>Hello 아시아 앱에 대 한 Git 배포를 구성 합니다.
사용 하 여 [az 앱 서비스 웹 소스 제어-config-로컬-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure hello 두 번째 웹 응용 프로그램에 대 한 로컬 Git 배포 합니다.

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

이 명령은 hello 다음과 같은 출력을 제공 합니다.

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

사용 하 여 hello 반환 URL tooconfigure 두 번째 Git 로컬 저장소에 대 한 원격. hello 다음 명령을 사용 하 여 hello 앞에 출력 예입니다.

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a>샘플 응용 프로그램 배포
실행 `git push` toodeploy 샘플 응용 프로그램 toohello 두 번째 Git 원격입니다. 

```bash
git push azure-asia master
```

암호에 대 한 메시지가 표시 되 면 hello 지정한 암호를 실행할 때 사용 하 여 `az appservice web deployment user set`합니다.

### <a name="browse-toohello-asia-app"></a>Toohello 아시아 응용 프로그램 찾아보기
사용 하 여 [az 앱 서비스 웹 찾아보기](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) tooverify 응용 프로그램은 Azure에서 실시간 실행 합니다.

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-hello-resource-id-of-hello-asia-app"></a>Hello 아시아 응용 프로그램의 hello 리소스 ID 가져오기
사용 하 여 [az 앱 서비스 웹 쇼](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) 동남 아시아에서 웹 응용 프로그램의 tooget hello 리소스 ID입니다.

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-asia-app"></a>Hello 아시아 응용 프로그램에 대 한 트래픽 관리자 끝점 추가
사용 하 여 [az 네트워크 트래픽 관리자 끝점 만들기](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd 두 번째 끝점 toohello 트래픽 관리자 프로필.

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-tooweb-apps"></a>지역 식별자 tooweb 앱 추가
사용 하 여 [az 앱 서비스 웹 구성 appsettings 업데이트](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd 지역별 환경 변수입니다.

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

응용 프로그램 코드는 이미 이 응용 프로그램 설정을 사용합니다. `HighScaleApp\Views\Home\Index.cshtml`에 대해 살펴보겠습니다.

### <a name="complete"></a>완료!

이제 서로 다른 지리적 지역에 대 한 브라우저에서 트래픽 관리자 프로필의 tooaccess hello URL을 시도 하십시오. 유럽의 클라이언트 브라우저는 “ASP.NET West Europe”, 아시아의 클라이언트 브라우저는 “ASP.NET Southeast Asia”가 표시되어야 합니다.

## <a name="more-resources"></a>추가 리소스
