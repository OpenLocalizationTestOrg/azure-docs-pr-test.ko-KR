---
title: "Azure 클라우드 서비스에서 원격 데스크톱 사용 | Microsoft Docs"
description: "원격 데스크톱 연결을 허용하기 위해 Azure 클라우드 서비스 응용 프로그램을 구성하는 방법"
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
ms.openlocfilehash: 413e72e9a39fcde84f56bfc61a6bc72dbadf1c97
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="700ce-103">Azure 클라우드 서비스의 역할에 대해 원격 데스크톱 연결 사용</span><span class="sxs-lookup"><span data-stu-id="700ce-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="700ce-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="700ce-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="700ce-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="700ce-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="700ce-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="700ce-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="700ce-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="700ce-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)

<span data-ttu-id="700ce-108">서비스 정의에 원격 데스크톱 모듈을 포함하여 개발 중에 원격 데스크톱 연결을 사용하도록 설정하거나 원격 데스크톱 확장을 통해 원격 데스크톱을 사용 하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-108">You can enable a Remote Desktop connection in your role during development by including the Remote Desktop modules in your service definition or you can choose to enable Remote Desktop through the Remote Desktop Extension.</span></span> <span data-ttu-id="700ce-109">권장되는 방법은 원격 데스크톱 확장을 사용하는 것입니다. 이 방법을 사용하면 응용 프로그램이 배포된 후에도 응용 프로그램을 다시 배포할 필요 없이 원격 데스크톱을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-109">The preferred approach is to use the Remote Desktop extension as you can enable Remote Desktop even after the application is deployed without having to redeploy your application.</span></span>

## <a name="configure-remote-desktop-from-the-azure-classic-portal"></a><span data-ttu-id="700ce-110">Azure 클래식 포털에서 원격 데스크톱 구성</span><span class="sxs-lookup"><span data-stu-id="700ce-110">Configure Remote Desktop from the Azure classic portal</span></span>
<span data-ttu-id="700ce-111">Azure 클래식 포털에서는 응용 프로그램이 배포된 후에도 원격 데스크톱을 사용 가능하게 설정할 수 있도록 원격 데스크톱 확장 접근 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-111">The Azure classic portal uses the Remote Desktop Extension approach so you can enable Remote Desktop even after the application is deployed.</span></span> <span data-ttu-id="700ce-112">클라우드 서비스의 **구성** 페이지에서 원격 데스크톱을 사용하도록 설정하거나 가상 컴퓨터에 연결하는 데 사용되는 로컬 관리자 계정, 인증에 사용되는 인증서를 변경하고 만료 날짜를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-112">The **Configure** page for your cloud service allows you to enable Remote Desktop, change the local Administrator account used to connect to the virtual machines, the certificate used in authentication and set the expiration date.</span></span>

1. <span data-ttu-id="700ce-113">**클라우드 서비스**, 클라우드 서비스의 이름, **구성**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-113">Click **Cloud Services**, click the name of the cloud service, and then click **Configure**.</span></span>
2. <span data-ttu-id="700ce-114">맨 아래에 있는 **원격** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-114">Click the **Remote** button at the bottom.</span></span>

    ![클라우드 서비스 원격](./media/cloud-services-role-enable-remote-desktop/CloudServices_Remote.png)

   > [!WARNING]
   > <span data-ttu-id="700ce-116">처음으로 원격 데스크톱을 사용하도록 설정한 후 확인(확인 표시)을 클릭하면 모든 역할 인스턴스가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-116">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="700ce-117">다시 부팅되지 않도록 하려면 암호를 암호화하는 데 사용되는 인증서가 역할에 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-117">To prevent a reboot, the certificate used to encrypt the password must be installed on the role.</span></span> <span data-ttu-id="700ce-118">다시 시작되지 않도록 하려면 [클라우드 서비스에 대 한 인증서를 업로드](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) 하고 이 대화 상자로 돌아옵니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-118">To prevent a restart, [upload a certificate for the cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return to this dialog.</span></span>

3. <span data-ttu-id="700ce-119">**역할**에서 업데이트할 역할을 선택하거나 모든 역할을 선택하려면 **모두**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-119">In **Roles**, select the role you want to update or select **All** for all roles.</span></span>
4. <span data-ttu-id="700ce-120">다음 중 하나를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-120">Make any of the following changes:</span></span>

   * <span data-ttu-id="700ce-121">원격 데스크톱을 사용하도록 설정하려면 **Enable Remote Desktop** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-121">To enable Remote Desktop, select the **Enable Remote Desktop** check box.</span></span> <span data-ttu-id="700ce-122">원격 데스크톱을 사용하지 않도록 설정하려면 확인란을 선택 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-122">To disable Remote Desktop, clear the check box.</span></span>
   * <span data-ttu-id="700ce-123">역할 인스턴스에 원격 데스크톱을 연결하는 데 사용할 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-123">Create an account to use in Remote Desktop connections to the role instances.</span></span>
   * <span data-ttu-id="700ce-124">기존 계정의 암호를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-124">Update the password for the existing account.</span></span>
   * <span data-ttu-id="700ce-125">인증에 사용할 업데이트된 인증서를 선택(**인증서** 페이지에서 **업로드**를 사용하여 인증서 업로드)하거나 새 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-125">Select an uploaded certificate to use for authentication (upload the certificate using **Upload** on the **Certificates** page) or create a new certificate.</span></span>
   * <span data-ttu-id="700ce-126">원격 데스크톱 구성의 만료 날짜를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-126">Change the expiration date for the Remote Desktop configuration.</span></span>

5. <span data-ttu-id="700ce-127">구성 업데이트를 마치면 **확인** (확인 표시)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-127">When you finish your configuration updates, click **OK** (checkmark).</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="700ce-128">원격으로 역할 인스턴스 액세스</span><span class="sxs-lookup"><span data-stu-id="700ce-128">Remote into role instances</span></span>
<span data-ttu-id="700ce-129">역할에 대해 원격 데스크톱이 사용되도록 설정되면 다양한 도구를 통해 역할 인스턴스에 원격으로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-129">Once Remote Desktop is enabled on the roles you can remote into a role instance through various tools.</span></span>

<span data-ttu-id="700ce-130">Azure 클래식 포털에서 역할 인스턴스에 연결하려면</span><span class="sxs-lookup"><span data-stu-id="700ce-130">To connect to a role instance from the Azure classic portal:</span></span>

1. <span data-ttu-id="700ce-131">**인스턴스**를 클릭하여 **인스턴스** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-131">Click **Instances** to open the **Instances** page.</span></span>
2. <span data-ttu-id="700ce-132">원격 데스크톱이 구성된 역할 인스턴스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-132">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="700ce-133">**연결**을 클릭하고 지침에 따라 데스크톱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-133">Click **Connect**, and follow the instructions to open the desktop.</span></span>
4. <span data-ttu-id="700ce-134">**열기**를 클릭한 후 **연결**을 클릭하여 원격 데스크톱 연결을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-134">Click **Open** and then **Connect** to start the Remote Desktop connection.</span></span>

### <a name="use-visual-studio-to-remote-into-a-role-instance"></a><span data-ttu-id="700ce-135">Visual Studio를 사용하여 역할 인스턴스에 원격으로 연결</span><span class="sxs-lookup"><span data-stu-id="700ce-135">Use Visual Studio to remote into a role instance</span></span>
<span data-ttu-id="700ce-136">Visual Studio의 서버 탐색기:</span><span class="sxs-lookup"><span data-stu-id="700ce-136">In Visual Studio, Server Explorer:</span></span>

1. <span data-ttu-id="700ce-137">**Azure** > **Cloud Services** > **[클라우드 서비스 이름]** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-137">Expand the **Azure** > **Cloud Services** > **[cloud service name]** node.</span></span>
2. <span data-ttu-id="700ce-138">**스테이징** 또는 **프로덕션**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-138">Expand either **Staging** or **Production**.</span></span>
3. <span data-ttu-id="700ce-139">개별 역할을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-139">Expand the individual role.</span></span>
4. <span data-ttu-id="700ce-140">역할 인스턴스 중 하나를 마우스 오른쪽 단추로 클릭하고 **원격 데스크톱을 사용하여 연결...**을 클릭한 다음 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-140">Right-click one of the role instances, click **Connect using Remote Desktop...**, and then enter the user name and password.</span></span>

![서버 탐색기 원격 데스크톱](./media/cloud-services-role-enable-remote-desktop/ServerExplorer_RemoteDesktop.png)

### <a name="use-powershell-to-get-the-rdp-file"></a><span data-ttu-id="700ce-142">PowerShell을 사용하여 RDP 파일 가져오기</span><span class="sxs-lookup"><span data-stu-id="700ce-142">Use PowerShell to get the RDP file</span></span>
<span data-ttu-id="700ce-143">[Get-azureremotedesktopfile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet을 사용하면 RDP 파일을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-143">You can use the [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet to retrieve the RDP file.</span></span> <span data-ttu-id="700ce-144">그런 다음 원격 데스크톱 연결에서 RDP 파일을 사용하여 클라우드 서비스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-144">You can then use the RDP file with Remote Desktop Connection to access the cloud service.</span></span>

### <a name="programmatically-download-the-rdp-file-through-the-service-management-rest-api"></a><span data-ttu-id="700ce-145">서비스 관리 REST API를 통해 프로그래밍 방식으로 RDP 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="700ce-145">Programmatically download the RDP file through the Service Management REST API</span></span>
<span data-ttu-id="700ce-146">[RDP 파일 다운로드](https://msdn.microsoft.com/library/jj157183.aspx) REST 작업을 사용하면 RDP 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-146">You can use the [Download RDP File](https://msdn.microsoft.com/library/jj157183.aspx) REST operation to download the RDP file.</span></span>

## <a name="to-configure-remote-desktop-in-the-service-definition-file"></a><span data-ttu-id="700ce-147">서비스 정의 파일에서 원격 데스크톱을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="700ce-147">To configure Remote Desktop in the service definition file</span></span>
<span data-ttu-id="700ce-148">이 방법을 사용하면 개발하는 동안 응용 프로그램에 대한 원격 데스크톱을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-148">This method allows you to enable Remote Desktop for the application during development.</span></span> <span data-ttu-id="700ce-149">이 방법을 사용할 경우 암호화된 암호가 서비스 구성 파일에 저장되어야 하며 원격 데스크톱 구성을 업데이트하기 위해서는 응용 프로그램을 재배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-149">This approach requires encrypted passwords be stored in your service configuration file and any updates to the remote desktop configuration would require a redeployment of the application.</span></span> <span data-ttu-id="700ce-150">이러한 단점이 방지하려면 위에서 설명하는 원격 데스크톱 확장 기반 접근 방법을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-150">If you want to avoid these downsides you should use the remote desktop extension based approach described above.</span></span>  

<span data-ttu-id="700ce-151">Visual Studio를 사용하여 서비스 정의 파일 접근 방식을 통해 [원격 데스크톱 연결을 사용하도록 설정](../vs-azure-tools-remote-desktop-roles.md) 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-151">You can use Visual Studio to [enable a remote desktop connection](../vs-azure-tools-remote-desktop-roles.md) using the service definition file approach.</span></span>  
<span data-ttu-id="700ce-152">아래 단계에서는 원격 데스크톱을 사용하도록 설정하기 위해 서비스 모델 파일에 필요한 변경 내용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-152">The steps below describe the changes needed to the service model files to enable remote desktop.</span></span> <span data-ttu-id="700ce-153">게시가 진행되면 Visual Studio에서 이러한 변경을 자동으로 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-153">Visual Studio will automatically makes these changes when publishing.</span></span>

### <a name="set-up-the-connection-in-the-service-model"></a><span data-ttu-id="700ce-154">서비스 모델에서 연결 설정</span><span class="sxs-lookup"><span data-stu-id="700ce-154">Set up the connection in the service model</span></span>
<span data-ttu-id="700ce-155">**Imports** 요소를 사용하여 **RemoteAccess** 모듈 및 **RemoteForwarder** 모듈을 [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) 파일로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-155">Use the **Imports** element to import the **RemoteAccess** module and the **RemoteForwarder** module to the [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) file.</span></span>

<span data-ttu-id="700ce-156">서비스 정의 파일은 `<Imports>` 요소가 추가된 다음 예제와 유사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-156">The service definition file should be similar to the following example with the `<Imports>` element added.</span></span>

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
<span data-ttu-id="700ce-157">[ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) 파일은 `<ConfigurationSettings>` 및 `<Certificates>` 요소가 추가된 다음 예제와 유사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-157">The [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) file should be similar to the following example, note the `<ConfigurationSettings>` and `<Certificates>` elements.</span></span> <span data-ttu-id="700ce-158">지정된 인증서를 [클라우드 서비스에 업로드](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="700ce-158">The Certificate specified must be [uploaded to the cloud service](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).</span></span>

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


## <a name="additional-resources"></a><span data-ttu-id="700ce-159">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="700ce-159">Additional Resources</span></span>
<span data-ttu-id="700ce-160">[Cloud Services를 구성하는 방법](cloud-services-how-to-configure.md)
[Cloud Services FAQ - 원격 데스크톱](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="700ce-160">[How to Configure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
