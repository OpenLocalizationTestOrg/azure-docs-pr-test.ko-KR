---
title: "PowerShell을 사용하여 Azure 클라우드 서비스의 역할에 대해 원격 데스크톱 연결 사용"
description: "원격 데스크톱 연결을 허용하기 위해 PowerShell을 사용하여 Azure 클라우드 서비스 응용 프로그램을 구성하는 방법"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: bf2f70a4-20dc-4302-a91a-38cd7a2baa62
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 171f27c92ee9de14301ebb664e9ba3bcd98c394d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="da173-103">PowerShell을 사용하여 Azure 클라우드 서비스의 역할에 대해 원격 데스크톱 연결 사용</span><span class="sxs-lookup"><span data-stu-id="da173-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="da173-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="da173-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="da173-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="da173-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="da173-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="da173-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="da173-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="da173-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="da173-108">원격 데스크톱을 사용하면 Azure에서 실행 중인 역할의 데스크톱에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da173-108">Remote Desktop enables you to access the desktop of a role running in Azure.</span></span> <span data-ttu-id="da173-109">원격 데스크톱 연결을 사용하여 응용 프로그램 실행 중에 응용 프로그램 문제를 진단하고 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da173-109">You can use a Remote Desktop connection to troubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="da173-110">이 문서에서는 PowerShell을 사용하여 클라우드 서비스 역할에 대해 원격 데스크톱을 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="da173-110">This article describes how to enable remote desktop on your Cloud Service Roles using PowerShell.</span></span> <span data-ttu-id="da173-111">이 문서에 필요한 필수 조건은 [Azure PowerShell 설치 및 구성하는 방법](/powershell/azure/overview) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da173-111">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the prerequisites needed for this article.</span></span> <span data-ttu-id="da173-112">PowerShell에서는 응용 프로그램이 배포된 후 원격 데스크톱을 사용 가능하게 설정할 수 있도록 원격 데스크톱 확장을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="da173-112">PowerShell utilizes the Remote Desktop Extension so you can enable Remote Desktop after the application is deployed.</span></span>

## <a name="configure-remote-desktop-from-powershell"></a><span data-ttu-id="da173-113">PowerShell에서 원격 데스크톱 구성</span><span class="sxs-lookup"><span data-stu-id="da173-113">Configure Remote Desktop from PowerShell</span></span>
<span data-ttu-id="da173-114">[Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet을 사용하면 지정된 역할 또는 클라우드 서비스 배포의 모든 역할에 대해 원격 데스크톱을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da173-114">The [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet allows you to enable Remote Desktop on specified roles or all roles of your cloud service deployment.</span></span> <span data-ttu-id="da173-115">cmdlet을 사용하면 PSCredential 개체를 수용하는 *Credential* 매개 변수를 통해 원격 데스크톱 사용자의 사용자 이름 및 암호를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da173-115">The cmdlet lets you specify the Username and Password for the remote desktop user through the *Credential* parameter that accepts a PSCredential object.</span></span>

<span data-ttu-id="da173-116">대화형으로 PowerShell을 사용하는 경우, [Get-Credentials](https://technet.microsoft.com/library/hh849815.aspx) cmdlet을 호출하여 PSCredential 개체를 쉽게 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da173-116">If you are using PowerShell interactively, you can easily set the PSCredential object by calling the [Get-Credentials](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

```
$remoteusercredentials = Get-Credential
```

<span data-ttu-id="da173-117">이 명령은 안전하게 원격 사용자의 사용자 이름과 암호를 입력할 수 있는 대화 상자를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="da173-117">This command displays a dialog box allowing you to enter the username and password for the remote user in a secure manner.</span></span>

<span data-ttu-id="da173-118">PowerShell은 자동화 시나리오에 유용하므로 사용자 조작이 필요하지 않은 방식으로 **PSCredential** 개체를 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da173-118">Since PowerShell helps in automation scenarios, you can also set up the **PSCredential** object in a way that doesn't require user interaction.</span></span> <span data-ttu-id="da173-119">먼저 보안 암호를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da173-119">First, you need to set up a secure password.</span></span> <span data-ttu-id="da173-120">일반 텍스트 암호를 지정하는 것으로 시작하고 [Convertto-securestring](https://technet.microsoft.com/library/hh849818.aspx)을 사용하여 보안 문자열로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="da173-120">You begin with specifying a plain text password convert it to a secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span> <span data-ttu-id="da173-121">그런 다음 이 보안 문자열을 [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx)을 사용하여 암호화된 표준 문자열로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da173-121">Next you need to convert this secure string into an encrypted standard string using [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span></span> <span data-ttu-id="da173-122">이제 이 암호화된 표준 문자열을 [Set-Content](https://technet.microsoft.com/library/ee176959.aspx)를 사용하여 파일로 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da173-122">Now you can save this encrypted standard string to a file using [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span></span>

<span data-ttu-id="da173-123">또한 매번 암호를 입력하지 않아도 되도록 보안 암호 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da173-123">You can also create a secure password file so that you don't have to type in the password every time.</span></span> <span data-ttu-id="da173-124">보안 암호 파일은 일반 텍스트 파일보다 더 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="da173-124">Also, a secure password file is better than a plain text file.</span></span> <span data-ttu-id="da173-125">다음과 같은 PowerShell을 사용하여 보안 암호 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="da173-125">Use the following PowerShell to create a secure password file:</span></span>

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> <span data-ttu-id="da173-126">암호를 설정할 때 [복잡성 요구 사항](https://technet.microsoft.com/library/cc786468.aspx)을 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="da173-126">When setting the password, make sure that you meet the [complexity requirements](https://technet.microsoft.com/library/cc786468.aspx).</span></span>
>
>

<span data-ttu-id="da173-127">보안 암호 파일에서 자격 증명 개체를 만들려면 파일 내용을 읽고 [Convertto-securestring](https://technet.microsoft.com/library/hh849818.aspx)을 사용하여 이를 다시 보안 문자열로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da173-127">To create the credential object from the secure password file, you must read the file contents and convert them back to a secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span>

<span data-ttu-id="da173-128">[Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet은 사용자 계정이 만료되는 *DateTime* 을 지정하는 **Expiration** 매개 변수를 수락하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="da173-128">The [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet also accepts an *Expiration* parameter, which specifies a **DateTime** at which the user account expires.</span></span> <span data-ttu-id="da173-129">예를 들어 현재 날짜 및 시간부터 며칠 후에 만료되도록 계정을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da173-129">For example, you could set the account to expire a few days from the current date and time.</span></span>

<span data-ttu-id="da173-130">이 PowerShell 예는 클라우드 서비스에서 원격 데스크톱 확장을 설정하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="da173-130">This PowerShell example shows you how to set the Remote Desktop Extension on a cloud service:</span></span>

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
<span data-ttu-id="da173-131">또한 원격 데스크톱을 사용하려는 배포 슬롯와 역할을 선택적으로 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da173-131">You can also optionally specify the deployment slot and roles that you want to enable remote desktop on.</span></span> <span data-ttu-id="da173-132">이러한 매개 변수가 지정되지 않은 경우 cmdlet은 **프로덕션** 배포 슬롯의 모든 역할에 대해 원격 데스크톱을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="da173-132">If these parameters are not specified, the cmdlet enables remote desktop on all roles in the **Production** deployment slot.</span></span>

<span data-ttu-id="da173-133">원격 데스크톱 확장은 배포와 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="da173-133">The Remote Desktop extension is associated with a deployment.</span></span> <span data-ttu-id="da173-134">서비스에 대한 새 배포를 만드는 경우 해당 배포에 대해 원격 데스크톱을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da173-134">If you create a new deployment for the service, you have to enable remote desktop on that deployment.</span></span> <span data-ttu-id="da173-135">원격 데스크톱을 항상 사용하려는 경우 PowerShell 스크립트를 배포 워크플로에 통합하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="da173-135">If you always want to have remote desktop enabled, then you should consider integrating the PowerShell scripts into your deployment workflow.</span></span>

## <a name="remote-desktop-into-a-role-instance"></a><span data-ttu-id="da173-136">원격 데스크톱을 역할 인스턴스로 가져오기</span><span class="sxs-lookup"><span data-stu-id="da173-136">Remote Desktop into a role instance</span></span>
<span data-ttu-id="da173-137">[Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet은 원격 데스크톱을 클라우드 서비스의 특정 역할 인스턴스에 가져오는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="da173-137">The [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet is used to remote desktop into a specific role instance of your cloud service.</span></span> <span data-ttu-id="da173-138">*LocalPath* 매개 변수를 사용하여 RDP 파일을 로컬로 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da173-138">You can use the *LocalPath* parameter to download the RDP file locally.</span></span> <span data-ttu-id="da173-139">또는 *Launch* 매개 변수를 사용하여 클라우드 서비스 역할 인스턴스에 액세스하기 위해 원격 데스크톱 연결 대화 상자를 바로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da173-139">Or you can use the *Launch* parameter to directly launch the Remote Desktop Connection dialog to access the cloud service role instance.</span></span>

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a><span data-ttu-id="da173-140">서비스에서 원격 데스크톱 확장을 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="da173-140">Check if Remote Desktop extension is enabled on a service</span></span>
<span data-ttu-id="da173-141">[Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet은 원격 데스크톱이 서비스 배포에 사용되는지 여부를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="da173-141">The [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet displays that remote desktop is enabled or disabled on a service deployment.</span></span> <span data-ttu-id="da173-142">이 cmdlet은 원격 데스크톱 확장을 사용할 수 있는 원격 데스크톱 사용자 및 역할에 대한 사용자 이름을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="da173-142">The cmdlet returns the username for the remote desktop user and the roles that the remote desktop extension is enabled for.</span></span> <span data-ttu-id="da173-143">기본적으로 이는 배포 슬롯에서 발생하며, 대신 스테이징 슬롯을 사용하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da173-143">By default, this happens on the deployment slot and you can choose to use the staging slot instead.</span></span>

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a><span data-ttu-id="da173-144">서비스에서 원격 데스크톱 확장 제거</span><span class="sxs-lookup"><span data-stu-id="da173-144">Remove Remote Desktop extension from a service</span></span>
<span data-ttu-id="da173-145">배포에 대해 원격 데스크톱 확장을 이미 확장하고 원격 데스크톱 설정을 업데이트해야 하는 경우, 먼저 확장을 제거한 다음</span><span class="sxs-lookup"><span data-stu-id="da173-145">If you have already enabled the remote desktop extension on a deployment, and need to update the remote desktop settings, first remove the extension.</span></span> <span data-ttu-id="da173-146">새 설정으로 다시 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da173-146">And enable it again with the new settings.</span></span> <span data-ttu-id="da173-147">예를 들어 원격 사용자 계정에 대한 새 암호를 설정하려는 경우 또는 계정이 만료된 경우가 여기에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="da173-147">For example, if you want to set a new password for the remote user account, or the account expired.</span></span> <span data-ttu-id="da173-148">이는 원격 데스크톱 확장을 사용하도록 설정된 기존 배포에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="da173-148">Doing this is required on existing deployments that have the remote desktop extension enabled.</span></span> <span data-ttu-id="da173-149">새 배포의 경우 확장을 바로 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da173-149">For new deployments, you can simply apply the extension directly.</span></span>

<span data-ttu-id="da173-150">배포에서 원격 데스크톱 확장을 제거하려면 [Remove-AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da173-150">To remove the remote desktop extension from the deployment, you can use the [Remove-AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="da173-151">또한 원격 데스크톱을 제거하려는  배포 슬롯와 역할을 선택적으로 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da173-151">You can also optionally specify the deployment slot and role from which you want to remove the remote desktop extension.</span></span>

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> <span data-ttu-id="da173-152">확장 구성을 완전히 제거하려면 *UninstallConfiguration* 매개 변수와 **remove** cmdlet을 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da173-152">To completely remove the extension configuration, you should call the *remove* cmdlet with the **UninstallConfiguration** parameter.</span></span>
>
> <span data-ttu-id="da173-153">**UninstallConfiguration** 매개 변수는 서비스에 적용된 모든 확장 구성을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="da173-153">The **UninstallConfiguration** parameter uninstalls any extension configuration that is applied to the service.</span></span> <span data-ttu-id="da173-154">모든 확장 구성은 서비스 구성과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="da173-154">Every extension configuration is associated with the service configuration.</span></span> <span data-ttu-id="da173-155">**UninstallConfiguration** 없이 *remove* cmdlet을 호출하면 확장 구성에서 <mark>배포</mark>가 분리되어 확장이 효과적으로 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="da173-155">Calling the *remove* cmdlet without **UninstallConfiguration** disassociates the <mark>deployment</mark> from the extension configuration, thus effectively removing the extension.</span></span> <span data-ttu-id="da173-156">그러나 확장 구성은 서비스와 연결된 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="da173-156">However, the extension configuration remains associated with the service.</span></span>
>
>

## <a name="additional-resources"></a><span data-ttu-id="da173-157">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="da173-157">Additional resources</span></span>

<span data-ttu-id="da173-158">[Cloud Services를 구성하는 방법](cloud-services-how-to-configure.md)
[Cloud Services FAQ - 원격 데스크톱](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="da173-158">[How to Configure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
