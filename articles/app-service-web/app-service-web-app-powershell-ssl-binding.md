---
title: "PowerShell을 사용 하 여 바인딩 aaaSSL 인증서"
description: "어떻게 toobind SSL 인증서 PowerShell을 사용 하 여 tooyour 웹 앱에 알아봅니다."
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
ms.openlocfilehash: 82f0e7c796da99ab50f69f3638ef64d55a94fc8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a><span data-ttu-id="38b9c-103">PowerShell을 사용하여 Azure 앱 서비스 SSL 인증서 바인딩</span><span class="sxs-lookup"><span data-stu-id="38b9c-103">Azure App Service SSL Certificate Binding using PowerShell</span></span>
<span data-ttu-id="38b9c-104">Hello 릴리스의 Microsoft Azure PowerShell 버전 1.1.0 새 cmdlet이 추가 되었습니다 hello 사용자 hello 기능 toobind 기존 또는 새 SSL 인증서 tooan 기존 웹 앱을 가지게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="38b9c-104">With hello release of Microsoft Azure PowerShell version 1.1.0 a new cmdlet has been added that would give hello user hello ability toobind existing or new SSL certificates tooan existing Web App.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="38b9c-105">Azure 리소스 관리자를 사용 하는 방법에 대 한 toolearn 기반 Azure PowerShell cmdlet toomanage 웹 응용 프로그램 확인 [Azure 리소스 관리자 기반 Azure 웹 앱에 대 한 PowerShell 명령](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="38b9c-105">toolearn about using Azure Resource Manager based Azure PowerShell cmdlets toomanage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="uploading-and-binding-a-new-ssl-certificate"></a><span data-ttu-id="38b9c-106">새 SSL 인증서 업로드 및 바인딩</span><span class="sxs-lookup"><span data-stu-id="38b9c-106">Uploading and Binding a new SSL certificate</span></span>
<span data-ttu-id="38b9c-107">시나리오: hello 사용자가 웹 응용 프로그램의는 SSL 인증서 tooone toobind를 것인지 합니다.</span><span class="sxs-lookup"><span data-stu-id="38b9c-107">Scenario: hello user would like toobind an SSL certificate tooone of his web apps.</span></span>

<span data-ttu-id="38b9c-108">Hello hello 인증서에 대 한 암호 및 사용자 지정 호스트 이름을 hello hello 웹 응용 프로그램, hello 웹 응용 프로그램 이름, hello 사용자 컴퓨터에 hello 인증서.pfx 파일 경로 포함 하는 hello 리소스 그룹 이름을 알고 있으면, 다음 PowerShell 명령을 toocreate hello 사용할 수 있는 SSL 바인딩:</span><span class="sxs-lookup"><span data-stu-id="38b9c-108">Knowing hello resource group name that contains hello web app, hello web app name, hello certificate .pfx file path on hello user machine, hello password for hello certificate, and hello custom hostname, we can use hello following PowerShell command toocreate that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

<span data-ttu-id="38b9c-109">Note SSL 바인딩 tooa 웹 응용 프로그램을 추가 하기 전에 호스트 이름 (사용자 지정 도메인) 이미 구성 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="38b9c-109">Note that before adding a SSL binding tooa web app, you must have a host name (custom domain) already configured.</span></span> <span data-ttu-id="38b9c-110">Hello 호스트 이름이 구성 되지 않은 경우 오류가 발생 합니다 AzureRmWebAppSSLBinding 새로 만들기를 실행 하는 동안 'hostname'가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="38b9c-110">If hello host name is not configured , then you will get an error 'hostname' does not exist while running  New-AzureRmWebAppSSLBinding.</span></span> <span data-ttu-id="38b9c-111">Hello 포털 또는 Azure PowerShell을 사용 하 여에서 직접 호스트 이름을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38b9c-111">You can add a hostname directly from hello portal or using Azure PowerShell.</span></span> <span data-ttu-id="38b9c-112">hello 다음 PowerShell 코드 조각을 수 tooconfigure hello hostname AzureRmWebAppSSLBinding 새로 만들기를 실행 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="38b9c-112">hello following PowerShell snippet can be tooconfigure hello hostname before running New-AzureRmWebAppSSLBinding.</span></span>   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

<span data-ttu-id="38b9c-113">집합 AzureRmWebApp cmdlet hello toounderstand 덮어씁니다 hello 웹 앱에 대 한 호스트 이름을 hello 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="38b9c-113">It is important toounderstand that hello Set-AzureRmWebApp cmdlet overwrites hello hostnames for hello web app.</span></span> <span data-ttu-id="38b9c-114">따라서 PowerShell 코드 조각 위에 hello hello 웹 앱에 대 한 hello 호스트 이름의 toohello 기존 목록을 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="38b9c-114">Hence hello above PowerShell snippet is appending toohello existing list of hello host names for hello web app.</span></span>  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a><span data-ttu-id="38b9c-115">기존 SSL 인증서 업로드 및 바인딩</span><span class="sxs-lookup"><span data-stu-id="38b9c-115">Uploading and Binding an existing SSL certificate</span></span>
<span data-ttu-id="38b9c-116">시나리오: hello 사용자가 웹 응용 프로그램의 이전에 업로드 된 SSL 인증서 tooone toobind를 것인지 합니다.</span><span class="sxs-lookup"><span data-stu-id="38b9c-116">Scenario: hello user would like toobind a previously uploaded SSL certificate tooone of his web apps.</span></span>

<span data-ttu-id="38b9c-117">가져올 수 있습니다 hello 인증서 목록에 이미 업로드 된 tooa 특정 리소스 그룹 hello 다음 명령을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="38b9c-117">We can get hello list of certificates already uploaded tooa specific resource group by using hello following command</span></span>

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

<span data-ttu-id="38b9c-118">Note hello 인증서는 로컬 tooa 특정 위치 및 리소스 그룹, hello 사용자 toore 업로드 hello 인증서 필요 hello 구성 된 웹 앱이 다른 위치에 리소스 그룹 다른 hello의 인증서를 필요한 경우</span><span class="sxs-lookup"><span data-stu-id="38b9c-118">Note that hello certificates are local tooa specific location and resource group, hello user need toore-upload hello certificate if hello configured web app is in a different location and resource group other that that of hello needed certificate</span></span> 

<span data-ttu-id="38b9c-119">Hello 웹 응용 프로그램 이름, 인증서 지문을 hello 및 사용자 지정 호스트 이름을 hello hello 웹 앱을 포함 하는 hello 리소스 그룹 이름을 알고 있으면, 다음 PowerShell 명령을 toocreate hello에 해당 SSL 바인딩을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38b9c-119">Knowing hello resource group name that contains hello web app, hello web app name, hello certificate thumbprint, and hello custom hostname, we can use hello following PowerShell command toocreate that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a><span data-ttu-id="38b9c-120">기존 SSL 바인딩 삭제</span><span class="sxs-lookup"><span data-stu-id="38b9c-120">Deleting an existing SSL binding</span></span>
<span data-ttu-id="38b9c-121">시나리오: hello 사용자는 기존 SSL 바인딩을 toodelete를 것인지 합니다.</span><span class="sxs-lookup"><span data-stu-id="38b9c-121">Scenario: hello user would like toodelete an existing SSL binding.</span></span>

<span data-ttu-id="38b9c-122">웹 응용 프로그램 이름, hello 및 사용자 지정 호스트 이름을 hello hello 웹 앱을 포함 하는 hello 리소스 그룹 이름을 알고 있으면, 다음 PowerShell 명령을 tooremove hello에 해당 SSL 바인딩을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38b9c-122">Knowing hello resource group name that contains hello web app, hello web app name, and hello custom hostname, we can use hello following PowerShell command tooremove that SSL binding:</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

<span data-ttu-id="38b9c-123">Hello SSL 바인딩을 제거 된 hello 마지막는 해당 인증서를 사용 하 여 해당 위치에 바인딩 기본 hello 인증서에 의해 삭제 됩니다, 그리고 hello DeleteCertificate 옵션 tookeep hello 인증서 사용 하기 위해 hello 사용자 tookeep hello 인증서 선택</span><span class="sxs-lookup"><span data-stu-id="38b9c-123">Note that if hello removed SSL binding was hello last binding using that certificate in that location, by default hello certificate will be deleted, if hello user want tookeep hello certificate he can use hello DeleteCertificate option tookeep hello certificate</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a><span data-ttu-id="38b9c-124">참조</span><span class="sxs-lookup"><span data-stu-id="38b9c-124">References</span></span>
* [<span data-ttu-id="38b9c-125">Azure 웹앱용 Azure Resource Manager 기반 PowerShell 명령</span><span class="sxs-lookup"><span data-stu-id="38b9c-125">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="38b9c-126">소개 tooApp 서비스 환경</span><span class="sxs-lookup"><span data-stu-id="38b9c-126">Introduction tooApp Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="38b9c-127">Azure 리소스 관리자로 Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="38b9c-127">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

