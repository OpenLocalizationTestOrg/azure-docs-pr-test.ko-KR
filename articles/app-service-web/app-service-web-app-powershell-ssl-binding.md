---
title: "PowerShell을 사용하여 SSL 인증서 바인딩"
description: "PowerShell을 사용하여 웹앱에 SSL 인증서를 바인딩하는 방법을 알아봅니다."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 8ce32508-e982-48d3-b878-0e526afda537
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: a1fcc618fb0c68778e39cc227368a60b008f9401
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a><span data-ttu-id="77920-103">PowerShell을 사용하여 Azure 앱 서비스 SSL 인증서 바인딩</span><span class="sxs-lookup"><span data-stu-id="77920-103">Azure App Service SSL Certificate Binding using PowerShell</span></span>
<span data-ttu-id="77920-104">새 cmdlet이 추가된 Microsoft Azure PowerShell 버전 1.1.0이 출시되어 사용자는 기존 또는 새 SSL 인증서를 기존 웹앱에 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77920-104">With the release of Microsoft Azure PowerShell version 1.1.0 a new cmdlet has been added that would give the user the ability to bind existing or new SSL certificates to an existing Web App.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="77920-105">Azure Resource Manager 기반 Azure PowerShell cmdlet을 사용하여 [Azure 웹앱용 Azure Resource Manager 기반 PowerShell 명령](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="77920-105">To learn about using Azure Resource Manager based Azure PowerShell cmdlets to manage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="uploading-and-binding-a-new-ssl-certificate"></a><span data-ttu-id="77920-106">새 SSL 인증서 업로드 및 바인딩</span><span class="sxs-lookup"><span data-stu-id="77920-106">Uploading and Binding a new SSL certificate</span></span>
<span data-ttu-id="77920-107">시나리오: 사용자가 SSL 인증서를 웹앱 중 하나에 바인딩하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="77920-107">Scenario: The user would like to bind an SSL certificate to one of his web apps.</span></span>

<span data-ttu-id="77920-108">웹앱, 웹앱 이름, 인증서, 사용자 컴퓨터의 .pfx 파일 경로, 인증서 암호 및 사용자 지정 호스트 이름을 포함한 리소스 그룹 이름을 알고 있으면 다음 PowerShell 명령을 사용하여 해당 SSL 바인딩을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77920-108">Knowing the resource group name that contains the web app, the web app name, the certificate .pfx file path on the user machine, the password for the certificate, and the custom hostname, we can use the following PowerShell command to create that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

<span data-ttu-id="77920-109">SSL 바인딩을 웹앱에 추가하기 전에 이미 구성된 호스트 이름(사용자 지정 도메인)이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77920-109">Note that before adding a SSL binding to a web app, you must have a host name (custom domain) already configured.</span></span> <span data-ttu-id="77920-110">호스트 이름이 구성되지 않은 경우 New-AzureRmWebAppSSLBinding을 실행하는 동안 'hostname'가 존재하지 않는다는 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="77920-110">If the host name is not configured , then you will get an error 'hostname' does not exist while running  New-AzureRmWebAppSSLBinding.</span></span> <span data-ttu-id="77920-111">포털에서 또는 Azure PowerShell을 사용하여 직접 호스트 이름을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77920-111">You can add a hostname directly from the portal or using Azure PowerShell.</span></span> <span data-ttu-id="77920-112">다음 PowerShell 조각은 New-AzureRmWebAppSSLBinding을 실행하기 전에 호스트 이름을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77920-112">The following PowerShell snippet can be to configure the hostname before running New-AzureRmWebAppSSLBinding.</span></span>   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

<span data-ttu-id="77920-113">Set-AzureRmWebApp cmdlet이 웹앱에 대한 호스트 이름을 덮어쓴다는 것을 이해하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="77920-113">It is important to understand that the Set-AzureRmWebApp cmdlet overwrites the hostnames for the web app.</span></span> <span data-ttu-id="77920-114">따라서 위의 PowerShell 조각은 웹앱에 대한 호스트 이름의 기존 목록에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="77920-114">Hence the above PowerShell snippet is appending to the existing list of the host names for the web app.</span></span>  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a><span data-ttu-id="77920-115">기존 SSL 인증서 업로드 및 바인딩</span><span class="sxs-lookup"><span data-stu-id="77920-115">Uploading and Binding an existing SSL certificate</span></span>
<span data-ttu-id="77920-116">시나리오: 사용자가 이전에 업로드한 SSL 인증서를 웹앱 중 하나에 바인딩하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="77920-116">Scenario: The user would like to bind a previously uploaded SSL certificate to one of his web apps.</span></span>

<span data-ttu-id="77920-117">다음 명령을 사용하여 특정 리소스 그룹에 이미 업로드된 인증서 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77920-117">We can get the list of certificates already uploaded to a specific resource group by using the following command</span></span>

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

<span data-ttu-id="77920-118">인증서는 특정 위치 및 리소스 그룹에 로컬이며 구성된 웹앱이 필요한 인증서가 아닌 리소스 그룹 및 다른 위치에 있으면 사용자는 인증서를 다시 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77920-118">Note that the certificates are local to a specific location and resource group, the user need to re-upload the certificate if the configured web app is in a different location and resource group other that that of the needed certificate</span></span> 

<span data-ttu-id="77920-119">웹앱, 웹앱 이름, 인증서 지문 및 사용자 지정 호스트 이름이 포함된 리소스 그룹 이름을 알고 있으면 다음 PowerShell 명령을 사용하여 해당 SSL 바인딩을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77920-119">Knowing the resource group name that contains the web app, the web app name, the certificate thumbprint, and the custom hostname, we can use the following PowerShell command to create that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a><span data-ttu-id="77920-120">기존 SSL 바인딩 삭제</span><span class="sxs-lookup"><span data-stu-id="77920-120">Deleting an existing SSL binding</span></span>
<span data-ttu-id="77920-121">시나리오: 사용자가 기존 SSL 바인딩을 삭제하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="77920-121">Scenario: The user would like to delete an existing SSL binding.</span></span>

<span data-ttu-id="77920-122">웹앱, 웹앱 이름, 사용자 지정 호스트 이름이 포함된 리소스 그룹 이름을 알고 있으면 다음 PowerShell 명령을 사용하여 해당 SSL 바인딩을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77920-122">Knowing the resource group name that contains the web app, the web app name, and the custom hostname, we can use the following PowerShell command to remove that SSL binding:</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

<span data-ttu-id="77920-123">제거한 SSL 바인딩이 해당 위치에서 해당 인증서를 사용한 마지막 바인딩인 경우 기본적으로 인증서는 삭제되고 사용자가 인증서를 유지하려면 DeleteCertificate 옵션을 사용하여 인증서를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77920-123">Note that if the removed SSL binding was the last binding using that certificate in that location, by default the certificate will be deleted, if the user want to keep the certificate he can use the DeleteCertificate option to keep the certificate</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a><span data-ttu-id="77920-124">참조</span><span class="sxs-lookup"><span data-stu-id="77920-124">References</span></span>
* [<span data-ttu-id="77920-125">Azure 웹앱용 Azure Resource Manager 기반 PowerShell 명령</span><span class="sxs-lookup"><span data-stu-id="77920-125">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="77920-126">앱 서비스 환경 소개</span><span class="sxs-lookup"><span data-stu-id="77920-126">Introduction to App Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="77920-127">Azure 리소스 관리자로 Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="77920-127">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

