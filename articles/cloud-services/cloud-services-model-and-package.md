---
title: "클라우드 서비스 모델 및 패키지 정의 | Microsoft Docs"
description: "Azure의 클라우드 서비스 모델(.csdef,.cscfg) 및 패키지(.cspkg)에 대해 설명합니다."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 4ce2feb5-0437-496c-98da-1fb6dcb7f59e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 21fbdbc4c24440c6fbbd7487cfbb2e0a3140aa96
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="what-is-the-cloud-service-model-and-how-do-i-package-it"></a><span data-ttu-id="36f64-103">클라우드 서비스 모델 정의 및 패키지 방법</span><span class="sxs-lookup"><span data-stu-id="36f64-103">What is the Cloud Service model and how do I package it?</span></span>
<span data-ttu-id="36f64-104">클라우드 서비스는 서비스 정의*(.csdef)*, 서비스 구성*(.cscfg)*, 서비스 패키지*(.cspkg)*의 세 구성 요소에서 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-104">A cloud service is created from three components, the service definition *(.csdef)*, the service config *(.cscfg)*, and a service package *(.cspkg)*.</span></span> <span data-ttu-id="36f64-105">**ServiceDefinition.csdef** 및 **ServiceConfig.cscfg** 파일은 둘 다 XML 기반으로, 클라우드 서비스의 구조 및 구성 방법(합쳐서 모델이라고 함)을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-105">Both the **ServiceDefinition.csdef** and **ServiceConfig.cscfg** files are XML-based and describe the structure of the cloud service and how it's configured; collectively called the model.</span></span> <span data-ttu-id="36f64-106">**ServicePackage.cspkg**는 **ServiceDefinition.csdef** 및 다른 구성 요소에서 생성되는 zip 파일로, 필수 이진 기반 종속성을 모두 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-106">The **ServicePackage.cspkg** is a zip file that is generated from the **ServiceDefinition.csdef** and among other things, contains all the required binary-based dependencies.</span></span> <span data-ttu-id="36f64-107">Azure는 **ServicePackage.cspkg**와 **ServiceConfig.cscfg**에서 모두 클라우드 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-107">Azure creates a cloud service from both the **ServicePackage.cspkg** and the **ServiceConfig.cscfg**.</span></span>

<span data-ttu-id="36f64-108">Azure에서 클라우드 서비스가 실행 중이면 **ServiceConfig.cscfg** 파일을 통해 다시 구성할 수 있지만 정의는 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-108">Once the cloud service is running in Azure, you can reconfigure it through the **ServiceConfig.cscfg** file, but you cannot alter the definition.</span></span>

## <a name="what-would-you-like-to-know-more-about"></a><span data-ttu-id="36f64-109">자세하게 알고 싶은 내용이 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="36f64-109">What would you like to know more about?</span></span>
* <span data-ttu-id="36f64-110">[ServiceDefinition.csdef](#csdef) 및 [ServiceConfig.cscfg](#cscfg) 파일에 대해 자세하게 알고 싶습니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-110">I want to know more about the [ServiceDefinition.csdef](#csdef) and [ServiceConfig.cscfg](#cscfg) files.</span></span>
* <span data-ttu-id="36f64-111">이미 내용을 알고 있으므로 무엇을 구성할 수 있는지에 대한 [몇 가지 예](#next-steps) 를 보여 주세요.</span><span class="sxs-lookup"><span data-stu-id="36f64-111">I already know about that, give me [some examples](#next-steps) on what I can configure.</span></span>
* <span data-ttu-id="36f64-112">[ServicePackage.cspkg](#cspkg)를 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-112">I want to create the [ServicePackage.cspkg](#cspkg).</span></span>
* <span data-ttu-id="36f64-113">Visual Studio를 사용하여 다음 작업을 수행하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-113">I am using Visual Studio and I want to...</span></span>
  * <span data-ttu-id="36f64-114">[클라우드 서비스 만들기][vs_create]</span><span class="sxs-lookup"><span data-stu-id="36f64-114">[Create a cloud service][vs_create]</span></span>
  * <span data-ttu-id="36f64-115">[기존 클라우드 서비스 재구성][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="36f64-115">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
  * <span data-ttu-id="36f64-116">[클라우드 서비스 프로젝트 배포][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="36f64-116">[Deploy a Cloud Service project][vs_deploy]</span></span>
  * <span data-ttu-id="36f64-117">[원격 데스크톱에서 클라우드 서비스 인스턴스에 연결][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="36f64-117">[Remote desktop into a cloud service instance][remotedesktop]</span></span>

<a name="csdef"></a>

## <a name="servicedefinitioncsdef"></a><span data-ttu-id="36f64-118">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="36f64-118">ServiceDefinition.csdef</span></span>
<span data-ttu-id="36f64-119">**ServiceDefinition.csdef** 파일은 클라우드 서비스를 구성하기 위해 Azure에서 사용되는 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-119">The **ServiceDefinition.csdef** file specifies the settings that are used by Azure to configure a cloud service.</span></span> <span data-ttu-id="36f64-120">[Azure 서비스 정의 스키마(.csdef 파일)](https://msdn.microsoft.com/library/azure/ee758711.aspx) 는 서비스 정의 파일에 허용되는 형식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-120">The [Azure Service Definition Schema (.csdef File)](https://msdn.microsoft.com/library/azure/ee758711.aspx) provides the allowable format for a service definition file.</span></span> <span data-ttu-id="36f64-121">다음 예제에서는 웹 및 작업자 역할에 정의할 수 있는 설정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-121">The following example shows the settings that can be defined for the Web and Worker roles:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WebRole name="WebRole1" vmsize="Medium">
    <Sites>
      <Site name="Web">
        <Bindings>
          <Binding name="HttpIn" endpointName="HttpIn" />
        </Bindings>
      </Site>
    </Sites>
    <Endpoints>
      <InputEndpoint name="HttpIn" protocol="http" port="80" />
      <InternalEndpoint name="InternalHttpIn" protocol="http" />
    </Endpoints>
    <Certificates>
      <Certificate name="Certificate1" storeLocation="LocalMachine" storeName="My" />
    </Certificates>
    <Imports>
      <Import moduleName="Connect" />
      <Import moduleName="Diagnostics" />
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <LocalResources>
      <LocalStorage name="localStoreOne" sizeInMB="10" />
      <LocalStorage name="localStoreTwo" sizeInMB="10" cleanOnRoleRecycle="false" />
    </LocalResources>
    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" />
    </Startup>
  </WebRole>

  <WorkerRole name="WorkerRole1">
    <ConfigurationSettings>
      <Setting name="DiagnosticsConnectionString" />
    </ConfigurationSettings>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <Endpoints>
      <InputEndpoint name="Endpoint1" protocol="tcp" port="10000" />
      <InternalEndpoint name="Endpoint2" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="36f64-122">여기에 사용되는 XML 스키마를 더 잘 이해하려면 [서비스 정의 스키마](https://msdn.microsoft.com/library/azure/ee758711.aspx)를 참조하면 됩니다. 그러나 여기서 간략하게 몇 가지 요소를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-122">You can refer to the [Service Definition Schema](https://msdn.microsoft.com/library/azure/ee758711.aspx) for a better understanding of the XML schema used here, however, here is a quick explanation of some of the elements:</span></span>

<span data-ttu-id="36f64-123">**Sites**</span><span class="sxs-lookup"><span data-stu-id="36f64-123">**Sites**</span></span>  
<span data-ttu-id="36f64-124">IIS7에서 호스트되는 웹 사이트 또는 웹 응용 프로그램에 대한 정의를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-124">Contains the definitions for websites or web applications that are hosted in IIS7.</span></span>

<span data-ttu-id="36f64-125">**InputEndpoints**</span><span class="sxs-lookup"><span data-stu-id="36f64-125">**InputEndpoints**</span></span>  
<span data-ttu-id="36f64-126">클라우드 서비스에 연결하는 데 사용되는 끝점에 대한 정의를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-126">Contains the definitions for endpoints that are used to contact the cloud service.</span></span>

<span data-ttu-id="36f64-127">**InternalEndpoints**</span><span class="sxs-lookup"><span data-stu-id="36f64-127">**InternalEndpoints**</span></span>  
<span data-ttu-id="36f64-128">서로 통신하기 위해 역할 인스턴스에서 사용되는 끝점에 대한 정의를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-128">Contains the definitions for endpoints that are used by role instances to communicate with each other.</span></span>

<span data-ttu-id="36f64-129">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="36f64-129">**ConfigurationSettings**</span></span>  
<span data-ttu-id="36f64-130">특정 역할의 기능에 대한 설정 정의를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-130">Contains the setting definitions for features of a specific role.</span></span>

<span data-ttu-id="36f64-131">**Certificates**</span><span class="sxs-lookup"><span data-stu-id="36f64-131">**Certificates**</span></span>  
<span data-ttu-id="36f64-132">역할에 필요한 인증서에 대한 정의를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-132">Contains the definitions for certificates that are needed for a role.</span></span> <span data-ttu-id="36f64-133">앞의 코드 예제에서는 Azure Connect 구성에 사용되는 인증서를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-133">The previous code example shows a certificate that is used for the configuration of Azure Connect.</span></span>

<span data-ttu-id="36f64-134">**LocalResources**</span><span class="sxs-lookup"><span data-stu-id="36f64-134">**LocalResources**</span></span>  
<span data-ttu-id="36f64-135">로컬 저장소 리소스에 대한 정의를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-135">Contains the definitions for local storage resources.</span></span> <span data-ttu-id="36f64-136">로컬 저장소 리소스는 역할의 인스턴스가 실행 중인 가상 컴퓨터의 파일 시스템에 예약된 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-136">A local storage resource is a reserved directory on the file system of the virtual machine in which an instance of a role is running.</span></span>

<span data-ttu-id="36f64-137">**Imports**</span><span class="sxs-lookup"><span data-stu-id="36f64-137">**Imports**</span></span>  
<span data-ttu-id="36f64-138">가져온 모듈에 대한 정의를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-138">Contains the definitions for imported modules.</span></span> <span data-ttu-id="36f64-139">앞의 코드 예제에서는 원격 데스크톱 연결 및 Azure Connect에 대한 모듈을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-139">The previous code example shows the modules for Remote Desktop Connection and Azure Connect.</span></span>

<span data-ttu-id="36f64-140">**Startup**</span><span class="sxs-lookup"><span data-stu-id="36f64-140">**Startup**</span></span>  
<span data-ttu-id="36f64-141">역할이 시작될 때 실행되는 작업을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-141">Contains tasks that are run when the role starts.</span></span> <span data-ttu-id="36f64-142">작업은 .cmd 또는 실행 파일에 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-142">The tasks are defined in a .cmd or executable file.</span></span>

<a name="cscfg"></a>

## <a name="serviceconfigurationcscfg"></a><span data-ttu-id="36f64-143">ServiceConfiguration.cscfg</span><span class="sxs-lookup"><span data-stu-id="36f64-143">ServiceConfiguration.cscfg</span></span>
<span data-ttu-id="36f64-144">클라우드 서비스에 대한 설정 구성은 **ServiceConfiguration.cscfg** 파일의 값에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-144">The configuration of the settings for your cloud service is determined by the values in the **ServiceConfiguration.cscfg** file.</span></span> <span data-ttu-id="36f64-145">이 파일의 각 역할에 배포하려는 인스턴스 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-145">You specify the number of instances that you want to deploy for each role in this file.</span></span> <span data-ttu-id="36f64-146">서비스 정의 파일에서 정의한 구성 설정에 대한 값이 서비스 구성 파일에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-146">The values for the configuration settings that you defined in the service definition file are added to the service configuration file.</span></span> <span data-ttu-id="36f64-147">클라우드 서비스와 연결된 모든 관리 인증서의 지문도 파일에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-147">The thumbprints for any management certificates that are associated with the cloud service are also added to the file.</span></span> <span data-ttu-id="36f64-148">[Azure 서비스 구성 스키마(.cscfg 파일)](https://msdn.microsoft.com/library/azure/ee758710.aspx) 에서 서비스 구성 파일에 허용되는 형식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-148">The [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx) provides the allowable format for a service configuration file.</span></span>

<span data-ttu-id="36f64-149">서비스 구성 파일은 응용 프로그램과 함께 패키지되지 않지만 별도 파일로 Azure에 업로드되어 클라우드 서비스를 구성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-149">The service configuration file is not packaged with the application, but is uploaded to Azure as a separate file and is used to configure the cloud service.</span></span> <span data-ttu-id="36f64-150">클라우드 서비스를 다시 배포하지 않고 새 서비스 구성 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-150">You can upload a new service configuration file without redeploying your cloud service.</span></span> <span data-ttu-id="36f64-151">클라우드 서비스가 실행되는 동안 클라우드 서비스에 대한 구성 값을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-151">The configuration values for the cloud service can be changed while the cloud service is running.</span></span> <span data-ttu-id="36f64-152">다음 예제에서는 웹 및 작업자 역할에 정의할 수 있는 구성 설정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-152">The following example shows the configuration settings that can be defined for the Web and Worker roles:</span></span>

```xml
<?xml version="1.0"?>
<ServiceConfiguration serviceName="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration">
  <Role name="WebRole1">
    <Instances count="2" />
    <ConfigurationSettings>
      <Setting name="SettingName" value="SettingValue" />
    </ConfigurationSettings>

    <Certificates>
      <Certificate name="CertificateName" thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
      <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption"
         thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
    </Certificates>
  </Role>
</ServiceConfiguration>
```

<span data-ttu-id="36f64-153">여기에 사용되는 XML 스키마를 더 잘 이해하려면 [서비스 구성 스키마](https://msdn.microsoft.com/library/azure/ee758710.aspx)를 참조하면 됩니다. 그러나 여기서 간략하게 요소를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-153">You can refer to the [Service Configuration Schema](https://msdn.microsoft.com/library/azure/ee758710.aspx) for better understanding the XML schema used here, however, here is a quick explanation of the elements:</span></span>

<span data-ttu-id="36f64-154">**인스턴스**</span><span class="sxs-lookup"><span data-stu-id="36f64-154">**Instances**</span></span>  
<span data-ttu-id="36f64-155">역할에 대해 실행 중인 인스턴스 수를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-155">Configures the number of running instances for the role.</span></span> <span data-ttu-id="36f64-156">업그레이드하는 동안 잠재적으로 클라우드 서비스를 사용할 수 없게 되는 것을 방지하려면 웹과 관련된 역할의 인스턴스를 두 개 이상 배포하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-156">To prevent your cloud service from potentially becoming unavailable during upgrades, it is recommended that you deploy more than one instance of your web-facing roles.</span></span> <span data-ttu-id="36f64-157">둘 이상의 인스턴스를 배포하면 [Azure 계산 SLA(서비스 수준 계약)](http://azure.microsoft.com/support/legal/sla/)의 지침을 준수하게 되므로 서비스를 위해 둘 이상의 역할 인스턴스가 배포될 때 인터넷 연결 역할에 대한 99.95%의 외부 연결을 보증합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-157">By deploying more than one instance, you are adhering to the guidelines in the [Azure Compute Service Level Agreement (SLA)](http://azure.microsoft.com/support/legal/sla/), which guarantees 99.95% external connectivity for Internet-facing roles when two or more role instances are deployed for a service.</span></span>

<span data-ttu-id="36f64-158">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="36f64-158">**ConfigurationSettings**</span></span>  
<span data-ttu-id="36f64-159">역할에 대해 실행 중인 인스턴스의 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-159">Configures the settings for the running instances for a role.</span></span> <span data-ttu-id="36f64-160">`<Setting>` 요소의 이름은 서비스 정의 파일에 있는 설정 정의와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-160">The name of the `<Setting>` elements must match the setting definitions in the service definition file.</span></span>

<span data-ttu-id="36f64-161">**Certificates**</span><span class="sxs-lookup"><span data-stu-id="36f64-161">**Certificates**</span></span>  
<span data-ttu-id="36f64-162">서비스에서 사용되는 인증서를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-162">Configures the certificates that are used by the service.</span></span> <span data-ttu-id="36f64-163">앞의 코드 예제에서는 RemoteAccess 모듈의 인증서를 정의하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-163">The previous code example shows how to define the certificate for the RemoteAccess module.</span></span> <span data-ttu-id="36f64-164">*thumbprint* 특성 값은 사용할 인증서의 지문으로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-164">The value of the *thumbprint* attribute must be set to the thumbprint of the certificate to use.</span></span>

<p/>

> [!NOTE]
> <span data-ttu-id="36f64-165">인증서의 지문은 텍스트 편집기를 사용하여 구성 파일에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-165">The thumbprint for the certificate can be added to the configuration file by using a text editor.</span></span> <span data-ttu-id="36f64-166">또는 Visual Studio에서 역할 **속성** 페이지의 **인증서** 탭에서 값을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-166">Or, the value can be added on the **Certificates** tab of the **Properties** page of the role in Visual Studio.</span></span>
> 
> 

## <a name="defining-ports-for-role-instances"></a><span data-ttu-id="36f64-167">역할 인스턴스에 대한 포트 정의</span><span class="sxs-lookup"><span data-stu-id="36f64-167">Defining ports for role instances</span></span>
<span data-ttu-id="36f64-168">Azure는 웹 역할에 하나의 진입점만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-168">Azure allows only one entry point to a web role.</span></span> <span data-ttu-id="36f64-169">하나의 IP 주소를 통해 모든 트래픽이 발생한다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-169">Meaning that all traffic occurs through one IP address.</span></span> <span data-ttu-id="36f64-170">올바른 위치로 요청을 전송하도록 호스트 헤더를 구성하여 포트를 공유하도록 웹 사이트를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-170">You can configure your websites to share a port by configuring the host header to direct the request to the correct location.</span></span> <span data-ttu-id="36f64-171">IP 주소에서 잘 알려진 포트를 수신 대기하도록 응용 프로그램을 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-171">You can also configure your applications to listen to well-known ports on the IP address.</span></span>

<span data-ttu-id="36f64-172">다음 샘플은 웹 사이트 및 웹 응용 프로그램에서 웹 역할 구성 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-172">The following sample shows the configuration for a web role with a website and web application.</span></span> <span data-ttu-id="36f64-173">웹 사이트는 포트 80에서 기본 입력 위치로 구성되어 있고 웹 응용 프로그램은 “mail.mysite.cloudapp.net”이라는 대체 호스트 헤더에서 요청을 수신하도록 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-173">The website is configured as the default entry location on port 80, and the web applications are configured to receive requests from an alternate host header that is called “mail.mysite.cloudapp.net”.</span></span>

```xml
<WebRole>
  <ConfigurationSettings>
    <Setting name="DiagnosticsConnectionString" />
  </ConfigurationSettings>
  <Endpoints>
    <InputEndpoint name="HttpIn" protocol="http" port="80" />
    <InputEndpoint name="Https" protocol="https" port="443" certificate="SSL"/>
    <InputEndpoint name="NetTcp" protocol="tcp" port="808" certificate="SSL"/>
  </Endpoints>
  <LocalResources>
    <LocalStorage name="Sites" cleanOnRoleRecycle="true" sizeInMB="100" />
  </LocalResources>
  <Site name="Mysite" packageDir="Sites\Mysite">
    <Bindings>
      <Binding name="http" endpointName="HttpIn" />
      <Binding name="https" endpointName="Https" />
      <Binding name="tcp" endpointName="NetTcp" />
    </Bindings>
  </Site>
  <Site name="MailSite" packageDir="MailSite">
    <Bindings>
      <Binding name="mail" endpointName="HttpIn" hostheader="mail.mysite.cloudapp.net" />
    </Bindings>
    <VirtualDirectory name="artifacts" />
    <VirtualApplication name="storageproxy">
      <VirtualDirectory name="packages" packageDir="Sites\storageProxy\packages"/>
    </VirtualApplication>
  </Site>
</WebRole>
```


## <a name="changing-the-configuration-of-a-role"></a><span data-ttu-id="36f64-174">역할의 구성 변경</span><span class="sxs-lookup"><span data-stu-id="36f64-174">Changing the configuration of a role</span></span>
<span data-ttu-id="36f64-175">클라우드 서비스가 Azure에서 실행 중인 상태에서 서비스를 오프라인으로 전환하지 않고 클라우드 서비스의 구성을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-175">You can update the configuration of your cloud service while it is running in Azure, without taking the service offline.</span></span> <span data-ttu-id="36f64-176">구성 정보를 변경하려면 새 구성 파일을 업로드하거나 가동 중인 구성 파일을 편집하고 실행 중인 서비스에 적용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-176">To change configuration information, you can either upload a new configuration file, or edit the configuration file in place and apply it to your running service.</span></span> <span data-ttu-id="36f64-177">서비스 구성에서 변경할 수 있는 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-177">The following changes can be made to the configuration of a service:</span></span>

* <span data-ttu-id="36f64-178">**구성 설정 값 변경**</span><span class="sxs-lookup"><span data-stu-id="36f64-178">**Changing the values of configuration settings**</span></span>  
  <span data-ttu-id="36f64-179">구성 설정 변경 시 인스턴스가 온라인인 상태에서 역할 인스턴스가 변경 사항을 적용하도록 선택하거나, 인스턴스가 오프라인인 상태에서 인스턴스를 정상적으로 재활용하여 변경 사항을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-179">When a configuration setting changes, a role instance can choose to apply the change while the instance is online, or to recycle the instance gracefully and apply the change while the instance is offline.</span></span>
* <span data-ttu-id="36f64-180">**역할 인스턴스의 서비스 토폴로지 변경**</span><span class="sxs-lookup"><span data-stu-id="36f64-180">**Changing the service topology of role instances**</span></span>  
  <span data-ttu-id="36f64-181">인스턴스가 제거되는 경우를 제외하고 토폴로지 변경은 실행 중인 인스턴스에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-181">Topology changes do not affect running instances, except where an instance is being removed.</span></span> <span data-ttu-id="36f64-182">일반적으로 나머지 모든 인스턴스는 재활용하지 않아도 됩니다. 하지만 토폴로지 변경에 대한 응답으로 역할 인스턴스를 재활용하도록 선택할 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-182">All remaining instances generally do not need to be recycled; however, you can choose to recycle role instances in response to a topology change.</span></span>
* <span data-ttu-id="36f64-183">**인증서 지문 변경**</span><span class="sxs-lookup"><span data-stu-id="36f64-183">**Changing the certificate thumbprint**</span></span>  
  <span data-ttu-id="36f64-184">역할 인스턴스가 오프라인인 상태에서는 인증서만 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-184">You can only update a certificate when a role instance is offline.</span></span> <span data-ttu-id="36f64-185">역할 인스턴스가 온라인인 상태에서 인증서를 추가, 삭제 또는 변경하면 Azure가 정상적으로 인스턴스를 오프라인 상태로 전환하여 인증서를 업데이트하고 변경이 완료되면 온라인 상태로 다시 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-185">If a certificate is added, deleted, or changed while a role instance is online, Azure gracefully takes the instance offline to update the certificate and bring it back online after the change is complete.</span></span>

### <a name="handling-configuration-changes-with-service-runtime-events"></a><span data-ttu-id="36f64-186">서비스 런타임 이벤트를 사용하여 구성 변경 사항 처리</span><span class="sxs-lookup"><span data-stu-id="36f64-186">Handling configuration changes with Service Runtime Events</span></span>
<span data-ttu-id="36f64-187">[Azure 런타임 라이브러리](https://msdn.microsoft.com/library/azure/mt419365.aspx)는 [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) 네임스페이스를 포함하여 역할에서 Azure 환경과 상호 작용하기 위한 클래스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-187">The [Azure Runtime Library](https://msdn.microsoft.com/library/azure/mt419365.aspx) includes the [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) namespace, which provides classes for interacting with the Azure environment from a role.</span></span> <span data-ttu-id="36f64-188">[RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) 클래스는 구성 변경 전후 발생하는 다음 이벤트를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-188">The [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) class defines the following events that are raised before and after a configuration change:</span></span>

* <span data-ttu-id="36f64-189">**[Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) 이벤트**</span><span class="sxs-lookup"><span data-stu-id="36f64-189">**[Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) event**</span></span>  
  <span data-ttu-id="36f64-190">필요한 경우 구성 변경이 지정된 역할 인스턴스에 적용되어 역할 인스턴스가 작동 중지하는 기회가 생기기 전에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-190">This occurs before the configuration change is applied to a specified instance of a role giving you a chance to take down the role instances if necessary.</span></span>
* <span data-ttu-id="36f64-191">**[Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) 이벤트**</span><span class="sxs-lookup"><span data-stu-id="36f64-191">**[Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) event**</span></span>  
  <span data-ttu-id="36f64-192">지정된 역할 인스턴스에 구성 변경이 적용된 후 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-192">Occurs after the configuration change is applied to a specified instance of a role.</span></span>

> [!NOTE]
> <span data-ttu-id="36f64-193">인증서 변경 사항이 있으면 항상 역할 인스턴스가 오프라인으로 전환되기 때문에 RoleEnvironment.Changing 또는 RoleEnvironment.Changed 이벤트가 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-193">Because certificate changes always take the instances of a role offline, they do not raise the RoleEnvironment.Changing or RoleEnvironment.Changed events.</span></span>
> 
> 

<a name="cspkg"></a>

## <a name="servicepackagecspkg"></a><span data-ttu-id="36f64-194">ServicePackage.cspkg</span><span class="sxs-lookup"><span data-stu-id="36f64-194">ServicePackage.cspkg</span></span>
<span data-ttu-id="36f64-195">응용 프로그램을 Azure에서 클라우드 서비스로 배포하려면 먼저 적절한 형식으로 응용 프로그램을 패키지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-195">To deploy an application as a cloud service in Azure, you must first package the application in the appropriate format.</span></span> <span data-ttu-id="36f64-196">**CSPack** 명령줄 도구( [Azure SDK](https://azure.microsoft.com/downloads/)와 함께 설치됨)를 사용하여 Visual Studio 대신 패키지 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-196">You can use the **CSPack** command-line tool (installed with the [Azure SDK](https://azure.microsoft.com/downloads/)) to create the package file as an alternative to Visual Studio.</span></span>

<span data-ttu-id="36f64-197">**CSPack** 은 서비스 정의 파일 및 서비스 구성 파일의 콘텐츠를 사용하여 패키지의 콘텐츠를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-197">**CSPack** uses the contents of the service definition file and service configuration file to define the contents of the package.</span></span> <span data-ttu-id="36f64-198">**CSPack** 은 [Azure 포털](cloud-services-how-to-create-deploy-portal.md#create-and-deploy)을 사용하여 Azure에 업로드할 수 있는 응용 프로그램 패키지 파일(.cspkg)을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-198">**CSPack** generates an application package file (.cspkg) that you can upload to Azure by using the [Azure portal](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span></span> <span data-ttu-id="36f64-199">기본적으로 패키지의 이름은 `[ServiceDefinitionFileName].cspkg`이지만 **CSPack**의 `/out` 옵션을 사용하여 다른 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-199">By default, the package is named `[ServiceDefinitionFileName].cspkg`, but you can specify a different name by using the `/out` option of **CSPack**.</span></span>

<span data-ttu-id="36f64-200">**CSPack**은 다음 위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-200">**CSPack** is located at</span></span>  
`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\[sdk-version]\bin\`

> [!NOTE]
> <span data-ttu-id="36f64-201">CSPack.exe(Windows)는 SDK로 설치되는 **Microsoft Azure 명령 프롬프트** 바로 가기를 실행하여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-201">CSPack.exe (on windows) is available by running the **Microsoft Azure Command Prompt** shortcut that is installed with the SDK.</span></span>  
> 
> <span data-ttu-id="36f64-202">가능한 모든 스위치 및 명령에 대한 설명서를 보려면 자체적으로 CSPack.exe 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-202">Run the CSPack.exe program by itself to see documentation about all the possible switches and commands.</span></span>
> 
> 

<p />

> [!TIP]
> <span data-ttu-id="36f64-203">**Microsoft Azure 계산 에뮬레이터**에서 로컬로 클라우드 서비스를 실행하고 **/copyonly** 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-203">Run your cloud service locally in the **Microsoft Azure Compute Emulator**, use the **/copyonly** option.</span></span> <span data-ttu-id="36f64-204">이 옵션을 사용하면 계산 에뮬레이터에서 실행할 수 있는 디렉터리 레이아웃에 응용 프로그램의 이진 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-204">This option copies the binary files for the application to a directory layout from which they can be run in the compute emulator.</span></span>
> 
> 

### <a name="example-command-to-package-a-cloud-service"></a><span data-ttu-id="36f64-205">클라우드 서비스를 패키지하는 예제 명령</span><span class="sxs-lookup"><span data-stu-id="36f64-205">Example command to package a cloud service</span></span>
<span data-ttu-id="36f64-206">다음 예제에서는 웹 역할에 대한 정보를 포함하는 응용 프로그램 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-206">The following example creates an application package that contains the information for a web role.</span></span> <span data-ttu-id="36f64-207">명령으로 사용할 서비스 정의 파일, 이진 파일을 찾을 수 있는 디렉터리 및 패키지 파일의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-207">The command specifies the service definition file to use, the directory where binary files can be found, and the name of the package file.</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /out:[OutputFileName]
```

<span data-ttu-id="36f64-208">응용 프로그램에 웹 역할 및 작업자 역할이 포함된 경우 다음 명령이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-208">If the application contains both a web role and a worker role, the following command is used:</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /out:[OutputFileName]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /role:[RoleName];[RoleBinariesDirectory];[RoleAssemblyName]
```

<span data-ttu-id="36f64-209">여기서는 변수가 다음과 같이 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-209">Where the variables are defined as follows:</span></span>

| <span data-ttu-id="36f64-210">변수</span><span class="sxs-lookup"><span data-stu-id="36f64-210">Variable</span></span> | <span data-ttu-id="36f64-211">값</span><span class="sxs-lookup"><span data-stu-id="36f64-211">Value</span></span> |
| --- | --- |
| <span data-ttu-id="36f64-212">\[DirectoryName\]</span><span class="sxs-lookup"><span data-stu-id="36f64-212">\[DirectoryName\]</span></span> |<span data-ttu-id="36f64-213">Azure 프로젝트의 .csdef 파일을 포함하는 루트 프로젝트 디렉터리의 하위 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-213">The subdirectory under the root project directory that contains the .csdef file of the Azure project.</span></span> |
| <span data-ttu-id="36f64-214">\[ServiceDefinition\]</span><span class="sxs-lookup"><span data-stu-id="36f64-214">\[ServiceDefinition\]</span></span> |<span data-ttu-id="36f64-215">서비스 정의 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-215">The name of the service definition file.</span></span> <span data-ttu-id="36f64-216">기본적으로 이 파일의 이름은 ServiceDefinition.csdef입니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-216">By default, this file is named ServiceDefinition.csdef.</span></span> |
| <span data-ttu-id="36f64-217">\[OutputFileName\]</span><span class="sxs-lookup"><span data-stu-id="36f64-217">\[OutputFileName\]</span></span> |<span data-ttu-id="36f64-218">생성된 패키지 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-218">The name for the generated package file.</span></span> <span data-ttu-id="36f64-219">일반적으로 응용 프로그램의 이름으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-219">Typically, this is set to the name of the application.</span></span> <span data-ttu-id="36f64-220">파일 이름이 지정되지 않은 경우 응용 프로그램 패키지는 \[ApplicationName\].cspkg로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-220">If no file name is specified, the application package is created as \[ApplicationName\].cspkg.</span></span> |
| <span data-ttu-id="36f64-221">\[RoleName\]</span><span class="sxs-lookup"><span data-stu-id="36f64-221">\[RoleName\]</span></span> |<span data-ttu-id="36f64-222">서비스 정의 파일에서 정의된 역할 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-222">The name of the role as defined in the service definition file.</span></span> |
| <span data-ttu-id="36f64-223">\[RoleBinariesDirectory]</span><span class="sxs-lookup"><span data-stu-id="36f64-223">\[RoleBinariesDirectory]</span></span> |<span data-ttu-id="36f64-224">역할에 대한 이진 파일의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-224">The location of the binary files for the role.</span></span> |
| <span data-ttu-id="36f64-225">\[VirtualPath\]</span><span class="sxs-lookup"><span data-stu-id="36f64-225">\[VirtualPath\]</span></span> |<span data-ttu-id="36f64-226">서비스 정의의 Sites 섹션에서 정의된 각 가상 경로에 대한 실제 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-226">The physical directories for each virtual path defined in the Sites section of the service definition.</span></span> |
| <span data-ttu-id="36f64-227">\[PhysicalPath\]</span><span class="sxs-lookup"><span data-stu-id="36f64-227">\[PhysicalPath\]</span></span> |<span data-ttu-id="36f64-228">서비스 정의의 사이트 노드에서 정의된 각 가상 경로에 대한 콘텐츠의 실제 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-228">The physical directories of the contents for each virtual path defined in the site node of the service definition.</span></span> |
| <span data-ttu-id="36f64-229">\[RoleAssemblyName\]</span><span class="sxs-lookup"><span data-stu-id="36f64-229">\[RoleAssemblyName\]</span></span> |<span data-ttu-id="36f64-230">역할에 대한 이진 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-230">The name of the binary file for the role.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="36f64-231">다음 단계</span><span class="sxs-lookup"><span data-stu-id="36f64-231">Next steps</span></span>
<span data-ttu-id="36f64-232">클라우드 서비스 패키지를 만들고 있으며 다음 작업을 수행하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-232">I'm creating a cloud service package and I want to...</span></span>

* <span data-ttu-id="36f64-233">[클라우드 서비스 인스턴스에 대해 원격 데스크톱 설정][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="36f64-233">[Setup remote desktop for a cloud service instance][remotedesktop]</span></span>
* <span data-ttu-id="36f64-234">[클라우드 서비스 프로젝트 배포][deploy]</span><span class="sxs-lookup"><span data-stu-id="36f64-234">[Deploy a Cloud Service project][deploy]</span></span>

<span data-ttu-id="36f64-235">Visual Studio를 사용하여 다음 작업을 수행하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="36f64-235">I am using Visual Studio and I want to...</span></span>

* <span data-ttu-id="36f64-236">[새 클라우드 서비스 만들기][vs_create]</span><span class="sxs-lookup"><span data-stu-id="36f64-236">[Create a new cloud service][vs_create]</span></span>
* <span data-ttu-id="36f64-237">[기존 클라우드 서비스 재구성][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="36f64-237">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
* <span data-ttu-id="36f64-238">[클라우드 서비스 프로젝트 배포][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="36f64-238">[Deploy a Cloud Service project][vs_deploy]</span></span>
* <span data-ttu-id="36f64-239">[클라우드 서비스 인스턴스에 대해 원격 데스크톱 설정][vs_remote]</span><span class="sxs-lookup"><span data-stu-id="36f64-239">[Setup remote desktop for a cloud service instance][vs_remote]</span></span>

[deploy]: cloud-services-how-to-create-deploy-portal.md
[remotedesktop]: cloud-services-role-enable-remote-desktop.md
[vs_remote]: ../vs-azure-tools-remote-desktop-roles.md
[vs_deploy]: ../vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md
[vs_reconfigure]: ../vs-azure-tools-configure-roles-for-cloud-service.md
[vs_create]: ../vs-azure-tools-azure-project-create.md
