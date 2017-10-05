---
title: "Azure 웹앱에 사용자 지정 도메인 및 SSL 추가 | Microsoft Docs"
description: "회사 브랜딩을 추가하여 프로덕션으로 전환하도록 Azure 웹앱을 준비하는 방법에 알아봅니다. 사용자 지정 도메인 이름(베니티 도메인)을 사용자 웹앱에 매핑하고 사용자 지정 SSL 인증서로 안전하게 유지합니다."
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
ms.openlocfilehash: c9d00f678b6257a8aafb35acd2d5a2292703a2dc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="add-custom-domain-and-ssl-to-an-azure-web-app"></a><span data-ttu-id="e94af-104">Azure 웹앱에 사용자 지정 도메인 및 SSL 추가</span><span class="sxs-lookup"><span data-stu-id="e94af-104">Add custom domain and SSL to an Azure web app</span></span>

<span data-ttu-id="e94af-105">이 자습서에서는 신속하게 사용자 지정 도메인 이름을 Azure 웹앱에 매핑한 다음 사용자 지정 SSL 인증서로 보호하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-105">This tutorial shows you how to quickly map a custom domain name to your Azure web app and then secure it with a custom SSL certificate.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="e94af-106">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="e94af-106">Before you begin</span></span>

<span data-ttu-id="e94af-107">이 샘플을 실행하기 전에 [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)을 로컬로 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-107">Before running this sample, install the [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) locally.</span></span>

<span data-ttu-id="e94af-108">또한 각 도메인 공급자에 대한 DNS 구성 페이지의 관리자 액세스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-108">You also need administrative access to the DNS configuration page for your respective domain provider.</span></span> <span data-ttu-id="e94af-109">예를 들어 `www.contoso.com`을 추가하려면 `contoso.com`에 대한 DNS 항목을 구성할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-109">For example, to add `www.contoso.com`, you need to be able to configure DNS entries for `contoso.com`.</span></span>

<span data-ttu-id="e94af-110">마지막으로 업로드하고 바인딩하려는 SSL 인증서에 사용할 .PFX 파일 _및_ 해당 암호가 유효해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-110">Lastly, you need a valid .PFX file _and_ its password for the SSL certificate you want to upload and bind.</span></span> <span data-ttu-id="e94af-111">원하는 사용자 지정 도메인 이름을 보호하도록 이 SSL 인증서를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-111">This SSL certificate should be configured to secure the custom domain name you want.</span></span> <span data-ttu-id="e94af-112">위의 예제에서 SSL 인증서는 `www.contoso.com`을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-112">In the above example, your SSL certificate should secure `www.contoso.com`.</span></span> 

## <a name="step-1---create-an-azure-web-app"></a><span data-ttu-id="e94af-113">1단계 - Azure 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="e94af-113">Step 1 - Create an Azure web app</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="e94af-114">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="e94af-114">Log in to Azure</span></span>

<span data-ttu-id="e94af-115">이제 터미널 창에서 Azure CLI 2.0을 사용하여 Azure에서 Node.js 앱을 호스팅하는 데 필요한 리소스를 만들 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-115">We are now going to use the Azure CLI 2.0 in a terminal window to create the resources needed to host our Node.js app in Azure.</span></span>  <span data-ttu-id="e94af-116">[az login](/cli/azure/#login) 명령으로 Azure 구독에 로그인하고 화면의 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-116">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> 

```azurecli 
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="e94af-117">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="e94af-117">Create a resource group</span></span>   
<span data-ttu-id="e94af-118">[az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-118">Create a resource group with the [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="e94af-119">Azure 리소스 그룹은 웹앱, 데이터베이스, 저장소 계정이 관리되었는지 등 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-119">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span> 

```azurecli
az group create --name myResourceGroup --location westeurope 
```

<span data-ttu-id="e94af-120">`---location`에 사용할 수 있는 가능한 값을 보려면 `az appservice list-locations` Azure CLI 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-120">To see what possible values you can use for `---location`, use the `az appservice list-locations` Azure CLI command.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="e94af-121">App Service 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="e94af-121">Create an App Service plan</span></span>

<span data-ttu-id="e94af-122">[az appservice plan create](/cli/azure/appservice/plan#create) 명령으로 App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-122">Create an App Service plan with the [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="e94af-123">다음 예제에서는 **기본** 가격 책정 계층을 사용하는 `myAppServicePlan`이라는 App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-123">The following example creates an App Service plan named `myAppServicePlan` using the **Basic** pricing tier.</span></span>

<span data-ttu-id="e94af-124">az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1</span><span class="sxs-lookup"><span data-stu-id="e94af-124">az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1</span></span>

<span data-ttu-id="e94af-125">App Service 계획을 만들었으면 Azure CLI는 다음 예제와 비슷한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-125">When the App Service plan has been created, the Azure CLI shows information similar to the following example.</span></span> 

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

## <a name="create-a-web-app"></a><span data-ttu-id="e94af-126">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="e94af-126">Create a web app</span></span>

<span data-ttu-id="e94af-127">이제 App Service 계획을 만들었으므로 `myAppServicePlan` App Service 계획 내에서 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-127">Now that an App Service plan has been created, create a web app within the `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="e94af-128">웹앱은 코드를 배포할 호스팅 공간을 제공할 뿐만 아니라 배포된 응용 프로그램을 확인할 수 있도록 URL도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-128">The web app gives your a hosting space to deploy your code as well as provides a URL for you to view the deployed application.</span></span> <span data-ttu-id="e94af-129">[az appservice web create](/cli/azure/appservice/web#create) 명령을 사용하여 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-129">Use the [az appservice web create](/cli/azure/appservice/web#create) command to create the web app.</span></span> 

<span data-ttu-id="e94af-130">아래 명령에서 `<app_name>` 자리 표시자를 확인한 고유한 앱 이름을 대체하세요.</span><span class="sxs-lookup"><span data-stu-id="e94af-130">In the command below, please substitute your own unique app name where you see the `<app_name>` placeholder.</span></span> <span data-ttu-id="e94af-131">이 고유한 이름은 웹앱에 대한 기본 도메인 이름의 일부로 사용되므로 이름은 Azure에 있는 모든 앱에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-131">This unique name will be used as the part of the default domain name for the web app, so the name needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="e94af-132">나중에 사용자에게 노출하기 전에 웹앱에 사용자 지정 DNS 항목을 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-132">You can later map any custom DNS entry to the web app before you expose it to your users.</span></span> 

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan 
```

<span data-ttu-id="e94af-133">웹앱을 만들었으면 Azure CLI는 다음 예제와 비슷한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-133">When the web app has been created, the Azure CLI shows information similar to the following example.</span></span> 

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

<span data-ttu-id="e94af-134">JSON 출력에서 `defaultHostName`은 웹앱의 기본 도메인 이름을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-134">From the JSON output, `defaultHostName` shows your web app's default domain name.</span></span> <span data-ttu-id="e94af-135">브라우저에서 이 주소로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-135">In your browser, navigate to this address.</span></span>

```
http://<app_name>.azurewebsites.net 
``` 
 
![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-created.png)  

## <a name="step-2---configure-dns-mapping"></a><span data-ttu-id="e94af-137">2단계 - DNS 매핑 구성</span><span class="sxs-lookup"><span data-stu-id="e94af-137">Step 2 - Configure DNS mapping</span></span>

<span data-ttu-id="e94af-138">이 단계에서는 사용자 지정 도메인의 매핑을 사용자 웹앱의 기본 도메인 이름인 `<app_name>.azurewebsites.net`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-138">In this step, you add a mapping from a custom domain to your web app's default domain name, `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="e94af-139">일반적으로 도메인 공급자의 웹 사이트에서 이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-139">Typically, you perform this step in your domain provider's website.</span></span> <span data-ttu-id="e94af-140">각 도메인 등록 기관의 웹 사이트는 약간씩 다르므로 공급자의 설명서를 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-140">Every domain registrar's website is slightly different, so you should consult your provider's documentation.</span></span> <span data-ttu-id="e94af-141">하지만 다음은 몇 가지 일반적인 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-141">However, here are some general guidelines.</span></span> 

### <a name="navigate-to-to-dns-management-page"></a><span data-ttu-id="e94af-142">DNS 관리 페이지로 이동</span><span class="sxs-lookup"><span data-stu-id="e94af-142">Navigate to to DNS management page</span></span>

<span data-ttu-id="e94af-143">먼저 도메인 등록 기관의 웹 사이트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-143">First, log in to your domain registrar's website.</span></span>  

<span data-ttu-id="e94af-144">그런 다음 DNS 레코드를 관리하기 위한 페이지를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-144">Then, find the page for managing DNS records.</span></span> <span data-ttu-id="e94af-145">**도메인 이름**, **DNS** 또는 **이름 서버 관리** 레이블이 지정된 사이트의 링크 또는 영역을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-145">Look for links or areas of the site labeled **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="e94af-146">계정 정보를 확인한 다음 **내 도메인**과 같은 링크를 검색하여 링크를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-146">Often, you can find the link by viewing your account information, and then looking for a link such as **My domains**.</span></span>

<span data-ttu-id="e94af-147">이 페이지를 찾았으면 DNS 레코드를 추가하거나 편집할 수 있는 링크를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-147">Once you find this page, look for a link that lets you add or edit DNS records.</span></span> <span data-ttu-id="e94af-148">이는 **영역 파일** 또는 **DNS 레코드** 링크이거나 **고급 구성** 링크일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-148">This might be a **Zone file** or **DNS Records** link, or an **Advanced configuration** link.</span></span>

### <a name="create-a-cname-record"></a><span data-ttu-id="e94af-149">CNAME 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="e94af-149">Create a CNAME record</span></span>

<span data-ttu-id="e94af-150">원하는 하위 도메인 이름을 웹앱의 기본 도메인 이름(`<app_name>.azurewebsites.net`, 여기서 `<app_name>`은 앱의 고유 이름)에 매핑하는 CNAME 레코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-150">Add a CNAME record that maps the desired subdomain name to your web app's default domain name (`<app_name>.azurewebsites.net`, where `<app_name>` is your app's unique name).</span></span>

<span data-ttu-id="e94af-151">`www.contoso.com` 예제의 경우 `www` 호스트 이름을 `<app_name>.azurewebsites.net`에 매핑하는 CNAME을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-151">For the `www.contoso.com` example, you create a CNAME that maps the `www` hostname to `<app_name>.azurewebsites.net`.</span></span>

## <a name="step-3---configure-the-custom-domain-on-your-web-app"></a><span data-ttu-id="e94af-152">3단계 - 웹앱에서 사용자 지정 도메인 구성</span><span class="sxs-lookup"><span data-stu-id="e94af-152">Step 3 - Configure the custom domain on your web app</span></span>

<span data-ttu-id="e94af-153">도메인 공급자의 웹 사이트에서 호스트 이름 매핑의 구성을 마쳤다면 웹앱에서 사용자 지정 도메인을 구성할 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-153">When you finish configuring the hostname mapping in your domain provider's website, you're ready to configure the custom domain on your web app.</span></span> <span data-ttu-id="e94af-154">[az appservice web config hostname add](/cli/azure/appservice/web/config/hostname#add) 명령을 사용하여 이 구성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-154">Use the [az appservice web config hostname add](/cli/azure/appservice/web/config/hostname#add) command to add this configuration.</span></span> 

<span data-ttu-id="e94af-155">아래 명령에서 `<app_name>`을 고유한 앱 이름으로, <your_custom_domain>을 정규화된 사용자 지정 도메인 이름(예: `www.contoso.com`)으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-155">In the command below, please substitute `<app_name>` with your unique app name, and <your_custom_domain> with the fully qualified custom domain name (e.g. `www.contoso.com`).</span></span> 

```azurecli
az appservice web config hostname add --webapp <app_name> --resource-group myResourceGroup --name <your_custom_domain>
```

<span data-ttu-id="e94af-156">이제 사용자 지정 도메인은 완전하게 사용자 웹앱에 매핑되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-156">The custom domain now is fully mapped to your web app.</span></span> <span data-ttu-id="e94af-157">브라우저에서 사용자 지정 도메인 이름으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-157">In your browser, navigate to the custom domain name.</span></span> <span data-ttu-id="e94af-158">예:</span><span class="sxs-lookup"><span data-stu-id="e94af-158">For example:</span></span>

```
http://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-custom-domain.png)  

## <a name="step-4---bind-a-custom-ssl-certificate-to-your-web-app"></a><span data-ttu-id="e94af-160">4단계 - 웹앱에 사용자 지정 SSL 인증서 바인딩</span><span class="sxs-lookup"><span data-stu-id="e94af-160">Step 4 - Bind a custom SSL certificate to your web app</span></span>

<span data-ttu-id="e94af-161">이제 브라우저의 주소 표시줄에 원하는 도메인 이름을 사용하는 Azure 웹앱이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-161">You now have an Azure web app, with the domain name you want in the browser's address bar.</span></span> <span data-ttu-id="e94af-162">하지만 `https://<your_custom_domain>`으로 이동하는 경우 인증서 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-162">However, if you navigate to the `https://<your_custom_domain>` now, you get a certificate error.</span></span> 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-cert-error.png)  

<span data-ttu-id="e94af-164">이 오류는 웹앱에 사용자 지정 도메인 이름과 일치하는 SSL 인증서 바인딩 아직 없기 때문에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-164">This error occurs because your web app doesn't yet have an SSL certificate binding that matches your custom domain name.</span></span> <span data-ttu-id="e94af-165">하지만 `https://<app_name>.azurewebsites.net`으로 이동하면 오류가 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-165">However, you don't get an error if you navigate to `https://<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="e94af-166">즉, 사용자의 앱 뿐 아니라 모든 Azure App Service 앱은 기본적으로 `*.azurewebsites.net` 와일드카드 도메인에 대한 SSL 인증서로 보호되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-166">This is because your app, as well as all Azure App Service apps, is secured with the SSL certificate for the `*.azurewebsites.net` wildcard domain by default.</span></span> 

<span data-ttu-id="e94af-167">사용자 지정 도메인 이름으로 웹앱에 액세스하려면 웹앱에 사용자 지정 도메인에 대한 SSL 인증서를 바인딩해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-167">In order to access your web app by your custom domain name, you need to bind the SSL certificate for your custom domain to the web app.</span></span> <span data-ttu-id="e94af-168">바로 이 단계에서 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-168">You will do it in this step.</span></span> 

### <a name="upload-the-ssl-certificate"></a><span data-ttu-id="e94af-169">SSL 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="e94af-169">Upload the SSL certificate</span></span>

<span data-ttu-id="e94af-170">[az appservice web config ssl upload](/cli/azure/appservice/web/config/ssl#upload) 명령을 사용하여 사용자 지정 도메인에 대한 SSL 인증서를 웹앱에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-170">Upload the SSL certificate for your custom domain to your web app by using the [az appservice web config ssl upload](/cli/azure/appservice/web/config/ssl#upload) command.</span></span>

<span data-ttu-id="e94af-171">아래 명령에서 `<app_name>`을 고유한 앱 이름으로, `<path_to_ptx_file>`을 .PFX 파일에 대한 경로로, `<password>`를 인증서의 암호로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-171">In the command below, please substitute `<app_name>` with your unique app name, `<path_to_ptx_file>` with the path to your .PFX file, and `<password>` with your certificate's password.</span></span> 

```azurecli
az appservice web config ssl upload --name <app_name> --resource-group myResourceGroup --certificate-file <path_to_pfx_file> --certificate-password <password> 
```

<span data-ttu-id="e94af-172">인증서를 업로드하면 Azure CLI는 다음 예제와 비슷한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-172">When the certificate is uploaded, the Azure CLI shows information similar to the following example:</span></span>

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

<span data-ttu-id="e94af-173">JSON 출력에서 `thumbprint`는 업로드된 인증서의 지문을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-173">From the JSON output, `thumbprint` shows your uploaded certificate's thumbprint.</span></span> <span data-ttu-id="e94af-174">다음 단계를 위해 해당 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-174">Copy its value for the next step.</span></span>

### <a name="bind-the-uploaded-ssl-certificate-to-the-web-app"></a><span data-ttu-id="e94af-175">업로드한 SSL 인증서를 웹앱에 바인딩</span><span class="sxs-lookup"><span data-stu-id="e94af-175">Bind the uploaded SSL certificate to the web app</span></span>

<span data-ttu-id="e94af-176">이제 웹앱에 원하는 사용자 지정 도메인 이름과 해당 사용자 지정 도메인을 보호하는 SSL 인증서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-176">Your web app now has the custom domain name you want, and it also has a SSL certificate that secures that custom domain.</span></span> <span data-ttu-id="e94af-177">이제 남은 것은 업로드된 인증서를 웹앱에 바인딩하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-177">The only thing left to do is to bind the uploaded certificate to the web app.</span></span> <span data-ttu-id="e94af-178">[az appservice web config ssl bind](/cli/azure/appservice/web/config/ssl#bind) 명령을 사용하여 이를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-178">You do this by using the [az appservice web config ssl bind](/cli/azure/appservice/web/config/ssl#bind) command.</span></span>

<span data-ttu-id="e94af-179">아래 명령에서 `<app_name>`을 고유한 앱 이름으로, `<thumbprint-from-previous-output>`을 이전 명령에서 가져온 인증서 지문으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-179">In the command below, please substitute `<app_name>` with your unique app name and `<thumbprint-from-previous-output>` with the certificate thumbprint that you get from the previous command.</span></span> 

<span data-ttu-id="e94af-180">az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI</span><span class="sxs-lookup"><span data-stu-id="e94af-180">az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI</span></span>

<span data-ttu-id="e94af-181">인증서를 웹앱에 바인딩하면 Azure CLI는 다음 예제와 비슷한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-181">When the certificate is bound to your web app, the Azure CLI shows information similar to the following example:</span></span>

<span data-ttu-id="e94af-182">{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }</span><span class="sxs-lookup"><span data-stu-id="e94af-182">{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }</span></span>

<span data-ttu-id="e94af-183">브라우저에서 사용자 지정 도메인 이름의 HTTPS 끝점으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e94af-183">In your browser, navigate to HTTPS endpoint of your custom domain name.</span></span> <span data-ttu-id="e94af-184">예:</span><span class="sxs-lookup"><span data-stu-id="e94af-184">For example:</span></span>

```
https://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-ssl-success.png)  

## <a name="more-resources"></a><span data-ttu-id="e94af-186">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="e94af-186">More resources</span></span>

<span data-ttu-id="e94af-187">[Azure App Service에서 사용자 지정 도메인 이름 구입 및 구성](custom-dns-web-site-buydomains-web-app.md)
[Azure App Service에 대한 SSL 인증서 구입 및 구성](web-sites-purchase-ssl-web-site.md)</span><span class="sxs-lookup"><span data-stu-id="e94af-187">[Buy and Configure a custom domain name in Azure App Service](custom-dns-web-site-buydomains-web-app.md)
[Buy and Configure an SSL Certificate for your Azure App Service](web-sites-purchase-ssl-web-site.md)</span></span>
