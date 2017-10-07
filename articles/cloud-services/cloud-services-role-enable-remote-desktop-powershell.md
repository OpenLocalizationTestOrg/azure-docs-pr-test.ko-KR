---
title: "aaaEnable PowerShell을 사용 하 여 Azure 클라우드 서비스에서 역할에 대 한 원격 데스크톱 연결"
description: "어떻게 tooconfigure azure 클라우드 PowerShell tooallow 원격 데스크톱 연결을 사용 하 여 서비스 응용 프로그램"
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
ms.openlocfilehash: 3f46b014f29f1c0be0e1b485d2f0152424162bb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="aa8a5-103">PowerShell을 사용하여 Azure 클라우드 서비스의 역할에 대해 원격 데스크톱 연결 사용</span><span class="sxs-lookup"><span data-stu-id="aa8a5-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="aa8a5-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="aa8a5-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="aa8a5-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="aa8a5-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="aa8a5-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa8a5-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="aa8a5-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="aa8a5-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="aa8a5-108">원격 데스크톱 사용 하면 Azure에서 실행 중인 역할의 tooaccess hello 데스크톱 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-108">Remote Desktop enables you tooaccess hello desktop of a role running in Azure.</span></span> <span data-ttu-id="aa8a5-109">원격 데스크톱 연결 tootroubleshoot를 사용할 수 있으며 실행 되는 동안 응용 프로그램 문제를 진단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-109">You can use a Remote Desktop connection tootroubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="aa8a5-110">이 문서에서는 설명 방법을 PowerShell을 사용 하 여 클라우드 서비스 역할에 원격 데스크톱 tooenable 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-110">This article describes how tooenable remote desktop on your Cloud Service Roles using PowerShell.</span></span> <span data-ttu-id="aa8a5-111">참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) hello이이 문서에 필요한 필수 구성 요소에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-111">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello prerequisites needed for this article.</span></span> <span data-ttu-id="aa8a5-112">Hello 응용 프로그램 배포 된 후 원격 데스크톱을 사용할 수 있도록 PowerShell에서 원격 데스크톱 확장 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-112">PowerShell utilizes hello Remote Desktop Extension so you can enable Remote Desktop after hello application is deployed.</span></span>

## <a name="configure-remote-desktop-from-powershell"></a><span data-ttu-id="aa8a5-113">PowerShell에서 원격 데스크톱 구성</span><span class="sxs-lookup"><span data-stu-id="aa8a5-113">Configure Remote Desktop from PowerShell</span></span>
<span data-ttu-id="aa8a5-114">hello [집합 AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet는 지정 된 역할 또는 클라우드 서비스 배포의 모든 역할에 원격 데스크톱 tooenable 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-114">hello [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet allows you tooenable Remote Desktop on specified roles or all roles of your cloud service deployment.</span></span> <span data-ttu-id="aa8a5-115">hello cmdlet을 사용 하면 hello hello 통해 원격 데스크톱 사용자에 대 한 hello 사용자 이름 및 암호를 지정 하면 *자격 증명* PSCredential 개체를 받는 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-115">hello cmdlet lets you specify hello Username and Password for hello remote desktop user through hello *Credential* parameter that accepts a PSCredential object.</span></span>

<span data-ttu-id="aa8a5-116">Hello를 호출 하 여 hello PSCredential 개체를 쉽게 설정할 수 PowerShell 대화형으로 사용 하는 경우 [자격 증명 가져오기](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-116">If you are using PowerShell interactively, you can easily set hello PSCredential object by calling hello [Get-Credentials](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

```
$remoteusercredentials = Get-Credential
```

<span data-ttu-id="aa8a5-117">이 명령은 tooenter hello 사용자 이름과 암호 hello 원격 사용자를 안전 하 게에서 허용 대화 상자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-117">This command displays a dialog box allowing you tooenter hello username and password for hello remote user in a secure manner.</span></span>

<span data-ttu-id="aa8a5-118">Hello를 설정할 수 있으므로 PowerShell 자동화 시나리오에 유용 합니다 **PSCredential** 사용자 상호 작용이 필요 하지 않은 방식으로 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-118">Since PowerShell helps in automation scenarios, you can also set up hello **PSCredential** object in a way that doesn't require user interaction.</span></span> <span data-ttu-id="aa8a5-119">첫째, tooset 보안 암호 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-119">First, you need tooset up a secure password.</span></span> <span data-ttu-id="aa8a5-120">Tooa 보안 문자열로 변환할 일반 텍스트 암호를 지정 하 여 시작 하기를 사용 하 여 [Convertto-securestring](https://technet.microsoft.com/library/hh849818.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-120">You begin with specifying a plain text password convert it tooa secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span> <span data-ttu-id="aa8a5-121">다음 해야 tooconvert이 보안 문자열 사용 하 여 암호화 된 표준 문자열 [Convertfrom-securestring](https://technet.microsoft.com/library/hh849814.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-121">Next you need tooconvert this secure string into an encrypted standard string using [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span></span> <span data-ttu-id="aa8a5-122">이 암호화 된 표준 문자열 tooa 사용 하 여 파일을 저장할 수 이제 [Set-content](https://technet.microsoft.com/library/ee176959.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-122">Now you can save this encrypted standard string tooa file using [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span></span>

<span data-ttu-id="aa8a5-123">또한 tootype에에서 없는 hello 암호 될 때마다 있도록 보안 암호 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-123">You can also create a secure password file so that you don't have tootype in hello password every time.</span></span> <span data-ttu-id="aa8a5-124">보안 암호 파일은 일반 텍스트 파일보다 더 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-124">Also, a secure password file is better than a plain text file.</span></span> <span data-ttu-id="aa8a5-125">다음 PowerShell toocreate 보안 암호 파일 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-125">Use hello following PowerShell toocreate a secure password file:</span></span>

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> <span data-ttu-id="aa8a5-126">Hello 암호를 설정할 때는 hello를 충족 하는지 확인 [복잡성 요구 사항을](https://technet.microsoft.com/library/cc786468.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-126">When setting hello password, make sure that you meet hello [complexity requirements](https://technet.microsoft.com/library/cc786468.aspx).</span></span>
>
>

<span data-ttu-id="aa8a5-127">hello 보안 암호 파일에서 toocreate hello 자격 증명 개체를 hello 파일 내용을 읽고 해야 변환할 백 tooa 사용 하 여 문자열을 보안 [Convertto-securestring](https://technet.microsoft.com/library/hh849818.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-127">toocreate hello credential object from hello secure password file, you must read hello file contents and convert them back tooa secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span>

<span data-ttu-id="aa8a5-128">hello [집합 AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet도 허용는 *만료* 매개 변수를 지정 하는 한 **DateTime** hello 사용자 계정이 만료 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-128">hello [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet also accepts an *Expiration* parameter, which specifies a **DateTime** at which hello user account expires.</span></span> <span data-ttu-id="aa8a5-129">예를 들어 설정할 수 있습니다 hello 계정 tooexpire 몇 일 동안 hello 현재 날짜와 시간에서.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-129">For example, you could set hello account tooexpire a few days from hello current date and time.</span></span>

<span data-ttu-id="aa8a5-130">PowerShell 예제 tooset 클라우드 서비스에 원격 데스크톱 확장을 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-130">This PowerShell example shows you how tooset hello Remote Desktop Extension on a cloud service:</span></span>

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
<span data-ttu-id="aa8a5-131">또한 필요에 따라 hello 배포 슬롯 및 tooenable 원격 데스크톱에서 원하는 역할을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-131">You can also optionally specify hello deployment slot and roles that you want tooenable remote desktop on.</span></span> <span data-ttu-id="aa8a5-132">Hello cmdlet hello에서 모든 역할에 원격 데스크톱을 사용 하면 이러한 매개 변수를 지정 하지 않은 경우 **프로덕션** 배포 슬롯입니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-132">If these parameters are not specified, hello cmdlet enables remote desktop on all roles in hello **Production** deployment slot.</span></span>

<span data-ttu-id="aa8a5-133">원격 데스크톱 확장 hello 배포와 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-133">hello Remote Desktop extension is associated with a deployment.</span></span> <span data-ttu-id="aa8a5-134">Hello 서비스에 대 한 새 배포를 만드는 경우 해당 배포에 tooenable 원격 데스크톱을가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-134">If you create a new deployment for hello service, you have tooenable remote desktop on that deployment.</span></span> <span data-ttu-id="aa8a5-135">항상 toohave 원격 데스크톱 사용 하도록 설정 하려면, hello PowerShell 스크립트를 배포 워크플로에 통합 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-135">If you always want toohave remote desktop enabled, then you should consider integrating hello PowerShell scripts into your deployment workflow.</span></span>

## <a name="remote-desktop-into-a-role-instance"></a><span data-ttu-id="aa8a5-136">원격 데스크톱을 역할 인스턴스로 가져오기</span><span class="sxs-lookup"><span data-stu-id="aa8a5-136">Remote Desktop into a role instance</span></span>
<span data-ttu-id="aa8a5-137">hello [Get-azureremotedesktopfile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet은 사용 되는 tooremote 데스크톱을 사용 하 여 클라우드 서비스의 특정 역할 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-137">hello [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet is used tooremote desktop into a specific role instance of your cloud service.</span></span> <span data-ttu-id="aa8a5-138">Hello를 사용할 수 있습니다 *LocalPath* 매개 변수 toodownload hello RDP 파일을 로컬입니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-138">You can use hello *LocalPath* parameter toodownload hello RDP file locally.</span></span> <span data-ttu-id="aa8a5-139">Hello를 사용할 수 있습니다 또는 *시작* 매개 변수 toodirectly 시작 hello 원격 데스크톱 연결 대화 tooaccess hello 클라우드 서비스 역할 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-139">Or you can use hello *Launch* parameter toodirectly launch hello Remote Desktop Connection dialog tooaccess hello cloud service role instance.</span></span>

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a><span data-ttu-id="aa8a5-140">서비스에서 원격 데스크톱 확장을 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-140">Check if Remote Desktop extension is enabled on a service</span></span>
<span data-ttu-id="aa8a5-141">hello [Get AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet을 표시 하는 원격 데스크톱 설정 또는 서비스 배포에서 수행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-141">hello [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet displays that remote desktop is enabled or disabled on a service deployment.</span></span> <span data-ttu-id="aa8a5-142">hello cmdlet에는 원격 데스크톱 사용자 hello 및 원격 데스크톱 확장 hello를 사용 하는 hello 역할에 대 한 hello 사용자 이름을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-142">hello cmdlet returns hello username for hello remote desktop user and hello roles that hello remote desktop extension is enabled for.</span></span> <span data-ttu-id="aa8a5-143">기본적으로이 hello 배포 슬롯에서 발생 하 고 대신 슬롯 준비 toouse hello를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-143">By default, this happens on hello deployment slot and you can choose toouse hello staging slot instead.</span></span>

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a><span data-ttu-id="aa8a5-144">서비스에서 원격 데스크톱 확장 제거</span><span class="sxs-lookup"><span data-stu-id="aa8a5-144">Remove Remote Desktop extension from a service</span></span>
<span data-ttu-id="aa8a5-145">이미 활성화 된 배포에서 원격 데스크톱 확장 hello tooupdate hello 필요한 원격 데스크톱 설정 하는 경우 먼저 hello 확장을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-145">If you have already enabled hello remote desktop extension on a deployment, and need tooupdate hello remote desktop settings, first remove hello extension.</span></span> <span data-ttu-id="aa8a5-146">고 hello 새 설정으로 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-146">And enable it again with hello new settings.</span></span> <span data-ttu-id="aa8a5-147">예를 들어 tooset 하려는 경우 hello 원격 사용자 계정 또는 hello 계정에 대 한 새 암호를 만료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-147">For example, if you want tooset a new password for hello remote user account, or hello account expired.</span></span> <span data-ttu-id="aa8a5-148">이 작업을 수행 hello 원격 데스크톱 확장을 사용 하는 기존 배포에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-148">Doing this is required on existing deployments that have hello remote desktop extension enabled.</span></span> <span data-ttu-id="aa8a5-149">새 배포를 위해 적용할 수 있습니다 단순히 hello 확장 직접.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-149">For new deployments, you can simply apply hello extension directly.</span></span>

<span data-ttu-id="aa8a5-150">tooremove hello 원격 데스크톱 확장 hello 배포에서 hello를 사용할 수 있습니다 [제거 AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-150">tooremove hello remote desktop extension from hello deployment, you can use hello [Remove-AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="aa8a5-151">또한 필요에 따라 hello 배포 슬롯 및 tooremove hello 원격 데스크톱 확장 하려는 역할을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-151">You can also optionally specify hello deployment slot and role from which you want tooremove hello remote desktop extension.</span></span>

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> <span data-ttu-id="aa8a5-152">호출 해야 hello toocompletely 제거 hello 확장 구성 *제거* hello 사용 하 여 cmdlet **UninstallConfiguration** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-152">toocompletely remove hello extension configuration, you should call hello *remove* cmdlet with hello **UninstallConfiguration** parameter.</span></span>
>
> <span data-ttu-id="aa8a5-153">hello **UninstallConfiguration** 모든 확장 구성을 제거 하는 매개 변수 즉 toohello 적용 된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-153">hello **UninstallConfiguration** parameter uninstalls any extension configuration that is applied toohello service.</span></span> <span data-ttu-id="aa8a5-154">모든 확장 구성 hello 서비스 구성에 연관 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-154">Every extension configuration is associated with hello service configuration.</span></span> <span data-ttu-id="aa8a5-155">호출 hello *제거* 없이 cmdlet **UninstallConfiguration** hello 연결을 끊습니다 <mark>배포</mark> hello 확장 구성에서 효과적으로 제거 hello 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-155">Calling hello *remove* cmdlet without **UninstallConfiguration** disassociates hello <mark>deployment</mark> from hello extension configuration, thus effectively removing hello extension.</span></span> <span data-ttu-id="aa8a5-156">그러나 hello 확장 구성을 유지 hello 서비스와 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa8a5-156">However, hello extension configuration remains associated with hello service.</span></span>
>
>

## <a name="additional-resources"></a><span data-ttu-id="aa8a5-157">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="aa8a5-157">Additional resources</span></span>

<span data-ttu-id="aa8a5-158">[어떻게 tooConfigure 클라우드 서비스](cloud-services-how-to-configure.md)
[클라우드 서비스 FAQ-원격 데스크톱](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="aa8a5-158">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
