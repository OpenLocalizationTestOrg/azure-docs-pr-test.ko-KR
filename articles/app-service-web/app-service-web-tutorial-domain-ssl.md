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
# <a name="add-custom-domain-and-ssl-tooan-azure-web-app"></a><span data-ttu-id="17ee8-104">사용자 지정 도메인 및 SSL tooan Azure 웹 앱 추가</span><span class="sxs-lookup"><span data-stu-id="17ee8-104">Add custom domain and SSL tooan Azure web app</span></span>

<span data-ttu-id="17ee8-105">이 자습서에는 tooquickly 매핑하는 사용자 지정 도메인 이름을 tooyour Azure 웹 앱 하 고 다음 사용자 지정 SSL 인증서를 사용 하 여 보안 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-105">This tutorial shows you how tooquickly map a custom domain name tooyour Azure web app and then secure it with a custom SSL certificate.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="17ee8-106">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="17ee8-106">Before you begin</span></span>

<span data-ttu-id="17ee8-107">이 샘플을 실행 하기 전에 hello 설치 [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) 로컬로 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-107">Before running this sample, install hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) locally.</span></span>

<span data-ttu-id="17ee8-108">또한 각 도메인 공급자에 대 한 관리 액세스 toohello DNS 구성 페이지가 있어야 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-108">You also need administrative access toohello DNS configuration page for your respective domain provider.</span></span> <span data-ttu-id="17ee8-109">예를 들어 tooadd `www.contoso.com`, toobe 수 tooconfigure DNS 항목에 대 한 필요한 `contoso.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-109">For example, tooadd `www.contoso.com`, you need toobe able tooconfigure DNS entries for `contoso.com`.</span></span>

<span data-ttu-id="17ee8-110">마지막으로, 유효한 필요합니다. PFX 파일 _및_ tooupload 원하는 hello SSL 인증서에 대 한 암호 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-110">Lastly, you need a valid .PFX file _and_ its password for hello SSL certificate you want tooupload and bind.</span></span> <span data-ttu-id="17ee8-111">이 SSL 인증서에는 원하는 구성된 toosecure hello 사용자 지정 도메인 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-111">This SSL certificate should be configured toosecure hello custom domain name you want.</span></span> <span data-ttu-id="17ee8-112">위 예제는 hello에서 SSL 인증서를 보호 해야 `www.contoso.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-112">In hello above example, your SSL certificate should secure `www.contoso.com`.</span></span> 

## <a name="step-1---create-an-azure-web-app"></a><span data-ttu-id="17ee8-113">1단계 - Azure 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="17ee8-113">Step 1 - Create an Azure web app</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="17ee8-114">TooAzure 로그인</span><span class="sxs-lookup"><span data-stu-id="17ee8-114">Log in tooAzure</span></span>

<span data-ttu-id="17ee8-115">진행 중인 toouse hello Azure CLI 2.0 터미널 윈도우 toocreate hello 리소스에서 필요한 toohost Azure에서 Node.js 앱 이제는입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-115">We are now going toouse hello Azure CLI 2.0 in a terminal window toocreate hello resources needed toohost our Node.js app in Azure.</span></span>  <span data-ttu-id="17ee8-116">Tooyour hello로 Azure 구독에에서 로그인 [az 로그인](/cli/azure/#login) 명령 열고 지시를 따른 hello 화면에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-116">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> 

```azurecli 
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="17ee8-117">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="17ee8-117">Create a resource group</span></span>   
<span data-ttu-id="17ee8-118">Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-118">Create a resource group with hello [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="17ee8-119">Azure 리소스 그룹은 웹앱, 데이터베이스, 저장소 계정이 관리되었는지 등 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-119">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span> 

```azurecli
az group create --name myResourceGroup --location westeurope 
```

<span data-ttu-id="17ee8-120">toosee에 사용할 수 있는 가능한 값은 있습니다 `---location`, hello를 사용 하 여 `az appservice list-locations` Azure CLI 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-120">toosee what possible values you can use for `---location`, use hello `az appservice list-locations` Azure CLI command.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="17ee8-121">App Service 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="17ee8-121">Create an App Service plan</span></span>

<span data-ttu-id="17ee8-122">Hello로 앱 서비스 계획 만들기 [az 앱 서비스 계획 만들기](/cli/azure/appservice/plan#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-122">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="17ee8-123">hello 다음 예제에서는 명명 된 앱 서비스 계획 `myAppServicePlan` hello를 사용 하 여 **기본** 가격 책정 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-123">hello following example creates an App Service plan named `myAppServicePlan` using hello **Basic** pricing tier.</span></span>

<span data-ttu-id="17ee8-124">az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1</span><span class="sxs-lookup"><span data-stu-id="17ee8-124">az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1</span></span>

<span data-ttu-id="17ee8-125">Hello 앱 서비스 계획을 만든 hello Azure CLI 정보 비슷한 toohello 다음 예제에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-125">When hello App Service plan has been created, hello Azure CLI shows information similar toohello following example.</span></span> 

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

## <a name="create-a-web-app"></a><span data-ttu-id="17ee8-126">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="17ee8-126">Create a web app</span></span>

<span data-ttu-id="17ee8-127">앱 서비스 계획을 만든 했으므로 hello 내에서 웹 응용 프로그램을 만들 `myAppServicePlan` 앱 서비스 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-127">Now that an App Service plan has been created, create a web app within hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="17ee8-128">호스팅 공간 toodeploy 코드 하는 것은 물론 있습니다 자동으로 제공 하는 URL tooview hello hello 웹 응용 프로그램은 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-128">hello web app gives your a hosting space toodeploy your code as well as provides a URL for you tooview hello deployed application.</span></span> <span data-ttu-id="17ee8-129">사용 하 여 hello [az 앱 서비스 웹 만들](/cli/azure/appservice/web#create) 명령 toocreate hello 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-129">Use hello [az appservice web create](/cli/azure/appservice/web#create) command toocreate hello web app.</span></span> 

<span data-ttu-id="17ee8-130">Hello 명령 아래에 hello 나타나는 자신의 고유한 응용 프로그램 이름으로 대체 하세요 `<app_name>` 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-130">In hello command below, please substitute your own unique app name where you see hello `<app_name>` placeholder.</span></span> <span data-ttu-id="17ee8-131">이 고유 이름이 hello 이름 해야 toobe 고유 Azure에서 모든 앱 간에 hello 웹 앱에 대 한 기본 도메인 이름 hello의 hello 일부로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-131">This unique name will be used as hello part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="17ee8-132">나중에 tooyour 사용자 노출 먼저 모든 사용자 지정 DNS 항목 toohello 웹 앱을 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-132">You can later map any custom DNS entry toohello web app before you expose it tooyour users.</span></span> 

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan 
```

<span data-ttu-id="17ee8-133">Hello 웹 응용 프로그램을 만든 hello Azure CLI 정보 비슷한 toohello 다음 예제에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-133">When hello web app has been created, hello Azure CLI shows information similar toohello following example.</span></span> 

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

<span data-ttu-id="17ee8-134">Hello JSON 출력에서에서 `defaultHostName` 웹 앱의 기본 도메인 이름을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-134">From hello JSON output, `defaultHostName` shows your web app's default domain name.</span></span> <span data-ttu-id="17ee8-135">브라우저에서 toothis 주소를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-135">In your browser, navigate toothis address.</span></span>

```
http://<app_name>.azurewebsites.net 
``` 
 
![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-created.png)  

## <a name="step-2---configure-dns-mapping"></a><span data-ttu-id="17ee8-137">2단계 - DNS 매핑 구성</span><span class="sxs-lookup"><span data-stu-id="17ee8-137">Step 2 - Configure DNS mapping</span></span>

<span data-ttu-id="17ee8-138">이 단계에서는 사용자 지정 도메인 tooyour 웹 앱의 기본 도메인 이름에서 매핑을 추가 `<app_name>.azurewebsites.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-138">In this step, you add a mapping from a custom domain tooyour web app's default domain name, `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="17ee8-139">일반적으로 도메인 공급자의 웹 사이트에서 이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-139">Typically, you perform this step in your domain provider's website.</span></span> <span data-ttu-id="17ee8-140">각 도메인 등록 기관의 웹 사이트는 약간씩 다르므로 공급자의 설명서를 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-140">Every domain registrar's website is slightly different, so you should consult your provider's documentation.</span></span> <span data-ttu-id="17ee8-141">하지만 다음은 몇 가지 일반적인 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-141">However, here are some general guidelines.</span></span> 

### <a name="navigate-tootoodns-management-page"></a><span data-ttu-id="17ee8-142">TootooDNS 관리 페이지로 이동</span><span class="sxs-lookup"><span data-stu-id="17ee8-142">Navigate tootooDNS management page</span></span>

<span data-ttu-id="17ee8-143">첫째, tooyour 도메인 등록 기관의 웹 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-143">First, log in tooyour domain registrar's website.</span></span>  

<span data-ttu-id="17ee8-144">그런 다음 DNS 레코드를 관리 하기 위한 hello 페이지를 찾을 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-144">Then, find hello page for managing DNS records.</span></span> <span data-ttu-id="17ee8-145">링크 또는 레이블이 지정 된 hello 사이트의 영역을 찾고 **도메인 이름**, **DNS**, 또는 **이름 서버 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-145">Look for links or areas of hello site labeled **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="17ee8-146">종종, 계정 정보를 표시 하 고 다음 찾고 링크와 같은 여 hello 링크를 찾을 수 있습니다 **내 도메인**합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-146">Often, you can find hello link by viewing your account information, and then looking for a link such as **My domains**.</span></span>

<span data-ttu-id="17ee8-147">이 페이지를 찾았으면 DNS 레코드를 추가하거나 편집할 수 있는 링크를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-147">Once you find this page, look for a link that lets you add or edit DNS records.</span></span> <span data-ttu-id="17ee8-148">이는 **영역 파일** 또는 **DNS 레코드** 링크이거나 **고급 구성** 링크일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-148">This might be a **Zone file** or **DNS Records** link, or an **Advanced configuration** link.</span></span>

### <a name="create-a-cname-record"></a><span data-ttu-id="17ee8-149">CNAME 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="17ee8-149">Create a CNAME record</span></span>

<span data-ttu-id="17ee8-150">Hello 원하는 하위 도메인 이름 tooyour 웹 응용 프로그램의 기본 도메인 이름을 매핑하는 CNAME 레코드 추가 (`<app_name>.azurewebsites.net`여기서 `<app_name>` 응용 프로그램의 고유 이름입니다).</span><span class="sxs-lookup"><span data-stu-id="17ee8-150">Add a CNAME record that maps hello desired subdomain name tooyour web app's default domain name (`<app_name>.azurewebsites.net`, where `<app_name>` is your app's unique name).</span></span>

<span data-ttu-id="17ee8-151">Hello에 대 한 `www.contoso.com` hello에 매핑하는 CNAME을 만들어야 예제에서는 `www` hostname 너무`<app_name>.azurewebsites.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-151">For hello `www.contoso.com` example, you create a CNAME that maps hello `www` hostname too`<app_name>.azurewebsites.net`.</span></span>

## <a name="step-3---configure-hello-custom-domain-on-your-web-app"></a><span data-ttu-id="17ee8-152">3 단계-웹 응용 프로그램에서 hello 사용자 지정 도메인 구성</span><span class="sxs-lookup"><span data-stu-id="17ee8-152">Step 3 - Configure hello custom domain on your web app</span></span>

<span data-ttu-id="17ee8-153">작업을 마치면 hello 호스트 이름 매핑 도메인 공급자의 웹 사이트에서 구성 하 고 준비 tooconfigure hello에 대 한 사용자 지정 도메인 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-153">When you finish configuring hello hostname mapping in your domain provider's website, you're ready tooconfigure hello custom domain on your web app.</span></span> <span data-ttu-id="17ee8-154">사용 하 여 hello [az 앱 서비스 웹 구성 호스트 이름 추가](/cli/azure/appservice/web/config/hostname#add) tooadd이이 구성을 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-154">Use hello [az appservice web config hostname add](/cli/azure/appservice/web/config/hostname#add) command tooadd this configuration.</span></span> 

<span data-ttu-id="17ee8-155">아래 hello 명령을 대체할 하십시오 `<app_name>` 고유한 응용 프로그램 이름 및 < your_custom_domain > hello 정규화 된 사용자 지정 도메인 이름으로 (예: `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="17ee8-155">In hello command below, please substitute `<app_name>` with your unique app name, and <your_custom_domain> with hello fully qualified custom domain name (e.g. `www.contoso.com`).</span></span> 

```azurecli
az appservice web config hostname add --webapp <app_name> --resource-group myResourceGroup --name <your_custom_domain>
```

<span data-ttu-id="17ee8-156">hello 사용자 지정 도메인에는 이제 완벽 하 게 매핑된 tooyour 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-156">hello custom domain now is fully mapped tooyour web app.</span></span> <span data-ttu-id="17ee8-157">브라우저에서 toohello 사용자 지정 도메인 이름을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-157">In your browser, navigate toohello custom domain name.</span></span> <span data-ttu-id="17ee8-158">예:</span><span class="sxs-lookup"><span data-stu-id="17ee8-158">For example:</span></span>

```
http://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-custom-domain.png)  

## <a name="step-4---bind-a-custom-ssl-certificate-tooyour-web-app"></a><span data-ttu-id="17ee8-160">4 단계-바인딩 사용자 지정 SSL 인증서 tooyour 웹 앱</span><span class="sxs-lookup"><span data-stu-id="17ee8-160">Step 4 - Bind a custom SSL certificate tooyour web app</span></span>

<span data-ttu-id="17ee8-161">Hello 브라우저의 주소 표시줄에 원하는 hello 도메인 이름 사용 하 여 Azure 웹 앱을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-161">You now have an Azure web app, with hello domain name you want in hello browser's address bar.</span></span> <span data-ttu-id="17ee8-162">그러나 toohello 이동 하는 경우 `https://<your_custom_domain>` 이제 인증서 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-162">However, if you navigate toohello `https://<your_custom_domain>` now, you get a certificate error.</span></span> 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-cert-error.png)  

<span data-ttu-id="17ee8-164">이 오류는 웹앱에 사용자 지정 도메인 이름과 일치하는 SSL 인증서 바인딩 아직 없기 때문에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-164">This error occurs because your web app doesn't yet have an SSL certificate binding that matches your custom domain name.</span></span> <span data-ttu-id="17ee8-165">너무 이동 하는 경우 오류가 발생 하지 않는 반면`https://<app_name>.azurewebsites.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-165">However, you don't get an error if you navigate too`https://<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="17ee8-166">응용 프로그램 뿐 아니라 모든 Azure 앱 서비스 앱 hello에 대 한 hello SSL 인증서로 보호 되 때문에 이것이 `*.azurewebsites.net` 기본적으로 와일드 카드 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-166">This is because your app, as well as all Azure App Service apps, is secured with hello SSL certificate for hello `*.azurewebsites.net` wildcard domain by default.</span></span> 

<span data-ttu-id="17ee8-167">tooaccess 웹 앱 사용자 지정 도메인 이름을 주문, 사용자 지정 도메인 toohello 웹 앱에 대 한 toobind hello SSL 인증서를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-167">In order tooaccess your web app by your custom domain name, you need toobind hello SSL certificate for your custom domain toohello web app.</span></span> <span data-ttu-id="17ee8-168">바로 이 단계에서 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-168">You will do it in this step.</span></span> 

### <a name="upload-hello-ssl-certificate"></a><span data-ttu-id="17ee8-169">Hello SSL 인증서를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-169">Upload hello SSL certificate</span></span>

<span data-ttu-id="17ee8-170">Hello를 사용 하 여 사용자 지정 도메인 tooyour 웹 앱에 대 한 hello SSL 인증서를 업로드 [az 앱 서비스 웹 구성 ssl 업로드](/cli/azure/appservice/web/config/ssl#upload) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-170">Upload hello SSL certificate for your custom domain tooyour web app by using hello [az appservice web config ssl upload](/cli/azure/appservice/web/config/ssl#upload) command.</span></span>

<span data-ttu-id="17ee8-171">아래 hello 명령을 대체할 하십시오 `<app_name>` 을 고유한 응용 프로그램 이름으로, `<path_to_ptx_file>` hello 경로 tooyour 사용 합니다. PFX 파일 및 `<password>` 인증서의 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-171">In hello command below, please substitute `<app_name>` with your unique app name, `<path_to_ptx_file>` with hello path tooyour .PFX file, and `<password>` with your certificate's password.</span></span> 

```azurecli
az appservice web config ssl upload --name <app_name> --resource-group myResourceGroup --certificate-file <path_to_pfx_file> --certificate-password <password> 
```

<span data-ttu-id="17ee8-172">Hello 인증서 업로드 되 면 hello Azure CLI 정보 비슷한 toohello를 다음 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-172">When hello certificate is uploaded, hello Azure CLI shows information similar toohello following example:</span></span>

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

<span data-ttu-id="17ee8-173">Hello JSON 출력에서에서 `thumbprint` 업로드 된 인증서의 지문을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-173">From hello JSON output, `thumbprint` shows your uploaded certificate's thumbprint.</span></span> <span data-ttu-id="17ee8-174">Hello 다음 단계에 대 한 해당 값을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-174">Copy its value for hello next step.</span></span>

### <a name="bind-hello-uploaded-ssl-certificate-toohello-web-app"></a><span data-ttu-id="17ee8-175">Toohello 웹 응용 프로그램 업로드 hello SSL 인증서 바인딩</span><span class="sxs-lookup"><span data-stu-id="17ee8-175">Bind hello uploaded SSL certificate toohello web app</span></span>

<span data-ttu-id="17ee8-176">이제 웹 앱 원하는 hello 사용자 지정 도메인 이름을 있으며 해당 사용자 지정 도메인을 보호 하는 한 SSL 인증서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-176">Your web app now has hello custom domain name you want, and it also has a SSL certificate that secures that custom domain.</span></span> <span data-ttu-id="17ee8-177">hello 것만 왼쪽된 toodo toobind hello 인증서를 업로드 toohello 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-177">hello only thing left toodo is toobind hello uploaded certificate toohello web app.</span></span> <span data-ttu-id="17ee8-178">Hello를 사용 하 여이 작업을 수행 [az 앱 서비스 웹 구성 ssl 바인딩을](/cli/azure/appservice/web/config/ssl#bind) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-178">You do this by using hello [az appservice web config ssl bind](/cli/azure/appservice/web/config/ssl#bind) command.</span></span>

<span data-ttu-id="17ee8-179">아래 hello 명령을 대체할 하십시오 `<app_name>` 을 고유한 응용 프로그램 이름 및 `<thumbprint-from-previous-output>` hello 이전 명령에서 얻을 수 있는 hello 인증서 지 문으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-179">In hello command below, please substitute `<app_name>` with your unique app name and `<thumbprint-from-previous-output>` with hello certificate thumbprint that you get from hello previous command.</span></span> 

<span data-ttu-id="17ee8-180">az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI</span><span class="sxs-lookup"><span data-stu-id="17ee8-180">az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI</span></span>

<span data-ttu-id="17ee8-181">Hello 인증서가 바인딩된 tooyour 웹 응용 프로그램, 다음 예제에서는 정보 비슷한 toohello를 hello Azure CLI로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-181">When hello certificate is bound tooyour web app, hello Azure CLI shows information similar toohello following example:</span></span>

<span data-ttu-id="17ee8-182">{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }</span><span class="sxs-lookup"><span data-stu-id="17ee8-182">{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }</span></span>

<span data-ttu-id="17ee8-183">브라우저에서 사용자 지정 도메인 이름의 tooHTTPS 끝점을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="17ee8-183">In your browser, navigate tooHTTPS endpoint of your custom domain name.</span></span> <span data-ttu-id="17ee8-184">예:</span><span class="sxs-lookup"><span data-stu-id="17ee8-184">For example:</span></span>

```
https://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-ssl-success.png)  

## <a name="more-resources"></a><span data-ttu-id="17ee8-186">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="17ee8-186">More resources</span></span>

<span data-ttu-id="17ee8-187">[Azure App Service에서 사용자 지정 도메인 이름 구입 및 구성](custom-dns-web-site-buydomains-web-app.md)
[Azure App Service에 대한 SSL 인증서 구입 및 구성](web-sites-purchase-ssl-web-site.md)</span><span class="sxs-lookup"><span data-stu-id="17ee8-187">[Buy and Configure a custom domain name in Azure App Service](custom-dns-web-site-buydomains-web-app.md)
[Buy and Configure an SSL Certificate for your Azure App Service](web-sites-purchase-ssl-web-site.md)</span></span>
