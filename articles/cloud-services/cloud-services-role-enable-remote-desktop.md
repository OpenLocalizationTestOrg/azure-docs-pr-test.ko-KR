---
title: "Azure 클라우드 서비스에 원격 데스크톱 aaaEnable | Microsoft Docs"
description: "어떻게 tooconfigure azure 클라우드 서비스 응용 프로그램 tooallow 원격 데스크톱 연결"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: d3110ee8-6526-4585-aba5-d0bc9a713e9b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: b3c0180bf5ad29cb77e5303ccbd6f9ccc44b7b0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="c81c1-103">Azure 클라우드 서비스의 역할에 대해 원격 데스크톱 연결 사용</span><span class="sxs-lookup"><span data-stu-id="c81c1-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c81c1-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="c81c1-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="c81c1-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="c81c1-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="c81c1-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c81c1-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="c81c1-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c81c1-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)

<span data-ttu-id="c81c1-108">서비스 정의에 hello 원격 데스크톱 모듈을 포함 하 여 개발 하는 동안 원격 데스크톱 연결 사용자 역할에 사용할 수 또는 원격 데스크톱 확장 hello 통해 원격 데스크톱 tooenable를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-108">You can enable a Remote Desktop connection in your role during development by including hello Remote Desktop modules in your service definition or you can choose tooenable Remote Desktop through hello Remote Desktop Extension.</span></span> <span data-ttu-id="c81c1-109">hello 선호 되는 방법은 toouse hello 원격 데스크톱 확장 hello tooredeploy 응용 프로그램 필요 없이 배포 된 후에 원격 데스크톱을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-109">hello preferred approach is toouse hello Remote Desktop extension as you can enable Remote Desktop even after hello application is deployed without having tooredeploy your application.</span></span>

## <a name="configure-remote-desktop-from-hello-azure-classic-portal"></a><span data-ttu-id="c81c1-110">Hello Azure 클래식 포털에서에서 원격 데스크톱을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-110">Configure Remote Desktop from hello Azure classic portal</span></span>
<span data-ttu-id="c81c1-111">Azure 클래식 포털 hello hello 원격 데스크톱 확장 방법을 사용 하 여 hello 응용 프로그램을 배포 후에 원격 데스크톱을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-111">hello Azure classic portal uses hello Remote Desktop Extension approach so you can enable Remote Desktop even after hello application is deployed.</span></span> <span data-ttu-id="c81c1-112">hello **구성** 클라우드 서비스에 대 한 페이지 tooenable 원격 데스크톱을 사용 하면, tooconnect toohello 가상 컴퓨터를 사용 하는 변경 hello 로컬 관리자 계정, hello 인증서 인증에 사용 하 고 hello 설정 만료 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-112">hello **Configure** page for your cloud service allows you tooenable Remote Desktop, change hello local Administrator account used tooconnect toohello virtual machines, hello certificate used in authentication and set hello expiration date.</span></span>

1. <span data-ttu-id="c81c1-113">클릭 **클라우드 서비스**hello 클라우드 서비스의 hello 이름을 클릭 하 고 클릭 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-113">Click **Cloud Services**, click hello name of hello cloud service, and then click **Configure**.</span></span>
2. <span data-ttu-id="c81c1-114">Hello 클릭 **원격** hello 아래쪽 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-114">Click hello **Remote** button at hello bottom.</span></span>

    ![클라우드 서비스 원격](./media/cloud-services-role-enable-remote-desktop/CloudServices_Remote.png)

   > [!WARNING]
   > <span data-ttu-id="c81c1-116">처음으로 원격 데스크톱을 사용하도록 설정한 후 확인(확인 표시)을 클릭하면 모든 역할 인스턴스가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-116">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="c81c1-117">다시 부팅 hello 인증서 사용 되는 tooencrypt hello 암호 tooprevent hello 역할에 설치 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-117">tooprevent a reboot, hello certificate used tooencrypt hello password must be installed on hello role.</span></span> <span data-ttu-id="c81c1-118">tooprevent 다시 시작을 [hello 클라우드 서비스에 대 한 인증서 업로드](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) 다음 toothis 대화를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-118">tooprevent a restart, [upload a certificate for hello cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return toothis dialog.</span></span>

3. <span data-ttu-id="c81c1-119">**역할**선택, 선택 하거나 tooupdate hello 역할 **모든** 모든 역할에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-119">In **Roles**, select hello role you want tooupdate or select **All** for all roles.</span></span>
4. <span data-ttu-id="c81c1-120">Hello 변경 내용이 다음 중 하나를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-120">Make any of hello following changes:</span></span>

   * <span data-ttu-id="c81c1-121">원격 데스크톱을 선택 하는 hello tooenable **원격 데스크톱 사용** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-121">tooenable Remote Desktop, select hello **Enable Remote Desktop** check box.</span></span> <span data-ttu-id="c81c1-122">원격 데스크톱 확인란 선택을 취소 hello toodisable 합니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-122">toodisable Remote Desktop, clear hello check box.</span></span>
   * <span data-ttu-id="c81c1-123">Toohello 역할 인스턴스에 원격 데스크톱 연결에서 계정 toouse을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-123">Create an account toouse in Remote Desktop connections toohello role instances.</span></span>
   * <span data-ttu-id="c81c1-124">Hello 기존 계정에 대 한 hello 암호를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-124">Update hello password for hello existing account.</span></span>
   * <span data-ttu-id="c81c1-125">인증에는 인증서를 업로드 toouse 선택 (사용 하 여 업로드 hello 인증서 **업로드** hello에 **인증서** 페이지) 하거나 새 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-125">Select an uploaded certificate toouse for authentication (upload hello certificate using **Upload** on hello **Certificates** page) or create a new certificate.</span></span>
   * <span data-ttu-id="c81c1-126">원격 데스크톱 구성을 hello hello 만료 날짜를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-126">Change hello expiration date for hello Remote Desktop configuration.</span></span>

5. <span data-ttu-id="c81c1-127">구성 업데이트를 마치면 **확인** (확인 표시)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-127">When you finish your configuration updates, click **OK** (checkmark).</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="c81c1-128">원격으로 역할 인스턴스 액세스</span><span class="sxs-lookup"><span data-stu-id="c81c1-128">Remote into role instances</span></span>
<span data-ttu-id="c81c1-129">Hello 역할에 원격 데스크톱을 사용 하도록 설정 하면 원격 다양 한 도구를 통해 역할 인스턴스로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-129">Once Remote Desktop is enabled on hello roles you can remote into a role instance through various tools.</span></span>

<span data-ttu-id="c81c1-130">hello Azure 클래식 포털에서에서 tooconnect tooa 역할 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="c81c1-130">tooconnect tooa role instance from hello Azure classic portal:</span></span>

1. <span data-ttu-id="c81c1-131">클릭 **인스턴스** tooopen hello **인스턴스** 페이지.</span><span class="sxs-lookup"><span data-stu-id="c81c1-131">Click **Instances** tooopen hello **Instances** page.</span></span>
2. <span data-ttu-id="c81c1-132">원격 데스크톱이 구성된 역할 인스턴스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-132">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="c81c1-133">클릭 **연결**, hello 지침 tooopen hello 바탕 화면을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-133">Click **Connect**, and follow hello instructions tooopen hello desktop.</span></span>
4. <span data-ttu-id="c81c1-134">클릭 **열려** 차례로 **연결** toostart hello 원격 데스크톱 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-134">Click **Open** and then **Connect** toostart hello Remote Desktop connection.</span></span>

### <a name="use-visual-studio-tooremote-into-a-role-instance"></a><span data-ttu-id="c81c1-135">Visual Studio tooremote 역할 인스턴스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="c81c1-135">Use Visual Studio tooremote into a role instance</span></span>
<span data-ttu-id="c81c1-136">Visual Studio의 서버 탐색기:</span><span class="sxs-lookup"><span data-stu-id="c81c1-136">In Visual Studio, Server Explorer:</span></span>

1. <span data-ttu-id="c81c1-137">Hello 확장 **Azure** > **클라우드 서비스** > **[클라우드 서비스 이름]** 노드.</span><span class="sxs-lookup"><span data-stu-id="c81c1-137">Expand hello **Azure** > **Cloud Services** > **[cloud service name]** node.</span></span>
2. <span data-ttu-id="c81c1-138">**스테이징** 또는 **프로덕션**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-138">Expand either **Staging** or **Production**.</span></span>
3. <span data-ttu-id="c81c1-139">Hello 개별 역할을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-139">Expand hello individual role.</span></span>
4. <span data-ttu-id="c81c1-140">Hello 역할 인스턴스 중 하나를 마우스 오른쪽 단추로 클릭 하 여, **원격 데스크톱을 사용 하 여 연결...** , hello 사용자 이름 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-140">Right-click one of hello role instances, click **Connect using Remote Desktop...**, and then enter hello user name and password.</span></span>

![서버 탐색기 원격 데스크톱](./media/cloud-services-role-enable-remote-desktop/ServerExplorer_RemoteDesktop.png)

### <a name="use-powershell-tooget-hello-rdp-file"></a><span data-ttu-id="c81c1-142">PowerShell tooget hello RDP 파일을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="c81c1-142">Use PowerShell tooget hello RDP file</span></span>
<span data-ttu-id="c81c1-143">Hello를 사용할 수 있습니다 [Get-azureremotedesktopfile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet tooretrieve hello RDP 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-143">You can use hello [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet tooretrieve hello RDP file.</span></span> <span data-ttu-id="c81c1-144">그런 다음 원격 데스크톱 연결 tooaccess hello 클라우드 서비스와 hello RDP 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-144">You can then use hello RDP file with Remote Desktop Connection tooaccess hello cloud service.</span></span>

### <a name="programmatically-download-hello-rdp-file-through-hello-service-management-rest-api"></a><span data-ttu-id="c81c1-145">프로그래밍 방식으로 hello 서비스 관리 REST API를 통해 hello RDP 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="c81c1-145">Programmatically download hello RDP file through hello Service Management REST API</span></span>
<span data-ttu-id="c81c1-146">Hello를 사용할 수 있습니다 [RDP 파일 다운로드](https://msdn.microsoft.com/library/jj157183.aspx) REST 작업 toodownload hello RDP 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-146">You can use hello [Download RDP File](https://msdn.microsoft.com/library/jj157183.aspx) REST operation toodownload hello RDP file.</span></span>

## <a name="tooconfigure-remote-desktop-in-hello-service-definition-file"></a><span data-ttu-id="c81c1-147">tooconfigure hello 서비스 정의 파일에 원격 데스크톱</span><span class="sxs-lookup"><span data-stu-id="c81c1-147">tooconfigure Remote Desktop in hello service definition file</span></span>
<span data-ttu-id="c81c1-148">이 방법을 사용 하면 개발 하는 동안 hello 응용 프로그램에 대 한 원격 데스크톱 tooenable 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-148">This method allows you tooenable Remote Desktop for hello application during development.</span></span> <span data-ttu-id="c81c1-149">이 접근 방식에서는 암호화 된 암호 저장에서 서비스 구성 파일 및 모든 업데이트 toohello 원격 데스크톱 구성 해야 합니다 hello 응용 프로그램의 프로젝트를 재배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-149">This approach requires encrypted passwords be stored in your service configuration file and any updates toohello remote desktop configuration would require a redeployment of hello application.</span></span> <span data-ttu-id="c81c1-150">Tooavoid 하려는 경우 원격 데스크톱 확장 hello를 사용 해야 이러한 단점이 기반 위에서 설명한 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="c81c1-150">If you want tooavoid these downsides you should use hello remote desktop extension based approach described above.</span></span>  

<span data-ttu-id="c81c1-151">Visual Studio도 사용할 수 있습니다[원격 데스크톱 연결 설정](../vs-azure-tools-remote-desktop-roles.md) hello 서비스 정의 파일 접근 방식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-151">You can use Visual Studio too[enable a remote desktop connection](../vs-azure-tools-remote-desktop-roles.md) using hello service definition file approach.</span></span>  
<span data-ttu-id="c81c1-152">다음 hello 단계 hello 변경 내용이 필요한 toohello 서비스 모델 파일 tooenable 원격 데스크톱에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-152">hello steps below describe hello changes needed toohello service model files tooenable remote desktop.</span></span> <span data-ttu-id="c81c1-153">게시가 진행되면 Visual Studio에서 이러한 변경을 자동으로 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-153">Visual Studio will automatically makes these changes when publishing.</span></span>

### <a name="set-up-hello-connection-in-hello-service-model"></a><span data-ttu-id="c81c1-154">Hello 서비스 모델에서 hello 연결 설정</span><span class="sxs-lookup"><span data-stu-id="c81c1-154">Set up hello connection in hello service model</span></span>
<span data-ttu-id="c81c1-155">사용 하 여 hello **Imports** 요소 tooimport hello **RemoteAccess** 모듈과 hello **RemoteForwarder** 모듈 toohello [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-155">Use hello **Imports** element tooimport hello **RemoteAccess** module and hello **RemoteForwarder** module toohello [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) file.</span></span>

<span data-ttu-id="c81c1-156">hello 서비스 정의 파일 있어야 다음 hello로 예제와 비슷한 toohello `<Imports>` 요소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-156">hello service definition file should be similar toohello following example with hello `<Imports>` element added.</span></span>

```xml
<ServiceDefinition name="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2013-03.2.0">
    <WebRole name="WebRole1" vmsize="Small">
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="Endpoint1" endpointName="Endpoint1" />
                </Bindings>
            </Site>
        </Sites>
        <Endpoints>
            <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
            <Import moduleName="Diagnostics" />
            <Import moduleName="RemoteAccess" />
            <Import moduleName="RemoteForwarder" />
        </Imports>
    </WebRole>
</ServiceDefinition>
```
<span data-ttu-id="c81c1-157">hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) 파일은 다음 예제와 비슷한 toohello 수, hello 참고 `<ConfigurationSettings>` 및 `<Certificates>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-157">hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) file should be similar toohello following example, note hello `<ConfigurationSettings>` and `<Certificates>` elements.</span></span> <span data-ttu-id="c81c1-158">지정 된 인증서 hello 해야 [toohello 클라우드 서비스 업로드](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service)합니다.</span><span class="sxs-lookup"><span data-stu-id="c81c1-158">hello Certificate specified must be [uploaded toohello cloud service](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2013-03.2.0">
    <Role name="WebRole1">
        <Instances count="2" />
        <ConfigurationSettings>
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.Enabled" value="true" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountUsername" value="[name-of-user-account]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountEncryptedPassword" value="[base-64-encrypted-user-password]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountExpiration" value="[certificate-expiration]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteForwarder.Enabled" value="true" />
        </ConfigurationSettings>
        <Certificates>
            <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="[certificate-thumbprint]" thumbprintAlgorithm="sha1" />
        </Certificates>
    </Role>
</ServiceConfiguration>
```


## <a name="additional-resources"></a><span data-ttu-id="c81c1-159">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="c81c1-159">Additional Resources</span></span>
<span data-ttu-id="c81c1-160">[어떻게 tooConfigure 클라우드 서비스](cloud-services-how-to-configure.md)
[클라우드 서비스 FAQ-원격 데스크톱](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="c81c1-160">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
