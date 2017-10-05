---
title: "서비스 관리 API를 사용하는 방법(Python) - 기능 가이드"
description: "Python에서 프로그래밍 방식으로 일반 서비스 관리 작업을 수행하는 방법에 대해 알아봅니다."
services: cloud-services
documentationcenter: python
author: lmazuel
manager: wpickett
editor: 
ms.assetid: 61538ec0-1536-4a7e-ae89-95967fe35d73
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/30/2017
ms.author: lmazuel
ms.openlocfilehash: 13249ba9a4b317a3154776b411ce0bb1f316b3bb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-service-management-from-python"></a><span data-ttu-id="59b0b-103">Python에서 서비스 관리를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="59b0b-103">How to use Service Management from Python</span></span>
<span data-ttu-id="59b0b-104">이 가이드에서는 Python에서 프로그래밍 방식으로 일반 서비스 관리 작업을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-104">This guide shows you how to programmatically perform common service management tasks from Python.</span></span> <span data-ttu-id="59b0b-105">[Python용 Azure SDK](https://github.com/Azure/azure-sdk-for-python)의 **ServiceManagementService** 클래스는 [Azure 클래식 포털][management-portal]에서 사용할 수 있는 대부분의 서비스 관리 관련 기능에 대해 프로그래밍 방식의 액세스를 지원합니다(예: **클라우드 서비스, 배포, 데이터 관리 서비스, 가상 컴퓨터 만들기, 업데이트 및 삭제**).</span><span class="sxs-lookup"><span data-stu-id="59b0b-105">The **ServiceManagementService** class in the [Azure SDK for Python](https://github.com/Azure/azure-sdk-for-python) supports programmatic access to much of the service management-related functionality that is available in the [Azure classic portal][management-portal] (such as **creating, updating, and deleting cloud services, deployments, data management services, and virtual machines**).</span></span> <span data-ttu-id="59b0b-106">이 기능은 서비스 관리에 프로그래밍 방식으로 액세스해야 하는 응용 프로그램을 빌드하는 데 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-106">This functionality can be useful in building applications that need programmatic access to service management.</span></span>

## <span data-ttu-id="59b0b-107"><a name="WhatIs"> </a>서비스 관리 정의</span><span class="sxs-lookup"><span data-stu-id="59b0b-107"><a name="WhatIs"> </a>What is Service Management</span></span>
<span data-ttu-id="59b0b-108">Service Management API는 [Azure 클래식 포털][management-portal]을 통해 사용할 수 있는 대부분의 서비스 관리 기능에 대해 프로그래밍 방식의 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-108">The Service Management API provides programmatic access to much of the service management functionality available through the [Azure classic portal][management-portal].</span></span> <span data-ttu-id="59b0b-109">Python용 Azure SDK를 사용하여 클라우드 서비스 및 저장소 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-109">The Azure SDK for Python allows you to manage your cloud services and storage accounts.</span></span>

<span data-ttu-id="59b0b-110">서비스 관리 API를 사용하려면 [Azure 계정을 만들어야](https://azure.microsoft.com/pricing/free-trial/)합니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-110">To use the Service Management API, you need to [create an Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <span data-ttu-id="59b0b-111"><a name="Concepts"> </a>개념</span><span class="sxs-lookup"><span data-stu-id="59b0b-111"><a name="Concepts"> </a>Concepts</span></span>
<span data-ttu-id="59b0b-112">Python용 Azure SDK는 REST API인 [Azure Service Management API][svc-mgmt-rest-api]를 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-112">The Azure SDK for Python wraps the [Azure Service Management API][svc-mgmt-rest-api], which is a REST API.</span></span> <span data-ttu-id="59b0b-113">모든 API 작업은 SSL을 통해 수행되고 X.509 v3 인증서를 사용하여 서로 인증됩니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-113">All API operations are performed over SSL and mutually authenticated using X.509 v3 certificates.</span></span> <span data-ttu-id="59b0b-114">관리 서비스는 Azure에서 실행 중인 서비스 내에서 액세스할 수 있거나, HTTPS 요청을 보내고 HTTPS 응답을 받을 수 있는 응용 프로그램에서 인터넷을 통해 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-114">The management service may be accessed from within a service running in Azure, or directly over the Internet from any application that can send an HTTPS request and receive an HTTPS response.</span></span>

## <span data-ttu-id="59b0b-115"><a name="Installation"> </a>설치</span><span class="sxs-lookup"><span data-stu-id="59b0b-115"><a name="Installation"> </a>Installation</span></span>
<span data-ttu-id="59b0b-116">이 문서에서 설명한 모든 기능은 `azure-servicemanagement-legacy` 패키지에서 사용할 수 있으며, 이 패키지는 pip을 사용하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-116">All the features described in this article are available in the `azure-servicemanagement-legacy` package, which you can install using pip.</span></span> <span data-ttu-id="59b0b-117">(예를 들어 Python을 처음 사용한다면) 설치에 관한 자세한 내용은 [Python 설치 및 Azure SDK](../python-how-to-install.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59b0b-117">For more information about installation (for example, if you are new to Python), see this article: [Installing Python and the Azure SDK](../python-how-to-install.md)</span></span>

## <span data-ttu-id="59b0b-118"><a name="Connect"> </a>방법: 서비스 관리에 연결</span><span class="sxs-lookup"><span data-stu-id="59b0b-118"><a name="Connect"> </a>How to: Connect to service management</span></span>
<span data-ttu-id="59b0b-119">서비스 관리 끝점에 연결하려면 Azure 구독 ID 및 유효한 관리 인증서가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-119">To connect to the Service Management endpoint, you need your Azure subscription ID and a valid management certificate.</span></span> <span data-ttu-id="59b0b-120">[Azure 클래식 포털][management-portal]을 통해 구독 ID를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-120">You can obtain your subscription ID through the [Azure classic portal][management-portal].</span></span>

> [!NOTE]
> <span data-ttu-id="59b0b-121">이제 Windows에서 실행할 때 OpenSSL로 만든 인증서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-121">It is now possible to use certificates created with OpenSSL when running on Windows.</span></span>  <span data-ttu-id="59b0b-122">Python 2.7.4 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-122">It requires Python 2.7.4 or later.</span></span> <span data-ttu-id="59b0b-123">.pfx 인증서 지원은 나중에 제거될 가능성이 크기 때문에 사용자는 .pfx 대신 OpenSSL을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-123">We recommend users to use OpenSSL instead of .pfx, since support for .pfx certificates will likely be removed in the future.</span></span>
>
>

### <a name="management-certificates-on-windowsmaclinux-openssl"></a><span data-ttu-id="59b0b-124">Windows/Mac/Linux의 관리 인증서(OpenSSL)</span><span class="sxs-lookup"><span data-stu-id="59b0b-124">Management certificates on Windows/Mac/Linux (OpenSSL)</span></span>
<span data-ttu-id="59b0b-125">[OpenSSL](http://www.openssl.org/) 을 사용하여 관리 인증서를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-125">You can use [OpenSSL](http://www.openssl.org/) to create your management certificate.</span></span>  <span data-ttu-id="59b0b-126">실제로 서버용(`.cer` 파일)과 클라이언트용(`.pem` 파일)으로 두 개의 인증서를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-126">You actually need to create two certificates, one for the server (a `.cer` file) and one for the client (a `.pem` file).</span></span> <span data-ttu-id="59b0b-127">`.pem` 파일을 만들려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-127">To create the `.pem` file, execute:</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="59b0b-128">`.cer` 인증서를 만들려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-128">To create the `.cer` certificate, execute:</span></span>

    openssl x509 -inform pem -in mycert.pem -outform der -out mycert.cer

<span data-ttu-id="59b0b-129">Azure 인증서에 대한 자세한 내용은 [Azure 클라우드 서비스 인증서](cloud-services-certs-create.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59b0b-129">For more information about Azure certificates, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="59b0b-130">OpenSSL 매개 변수에 대한 자세한 설명은 [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html)(영문)의 자료를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59b0b-130">For a complete description of OpenSSL parameters, see the documentation at [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span></span>

<span data-ttu-id="59b0b-131">이러한 파일을 만든 후에는 [Azure 클래식 포털][management-portal]에서 "설정" 탭의 "업로드" 작업을 통해 `.cer` 파일을 Azure에 업로드해야 하고, `.pem` 파일을 저장한 위치를 적어 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-131">After you have created these files, you need to upload the `.cer` file to Azure via the "Upload" action of the "Settings" tab of the [Azure classic portal][management-portal], and you need to make note of where you saved the `.pem` file.</span></span>

<span data-ttu-id="59b0b-132">구독 ID를 얻어 인증서를 만들고 `.cer` 파일을 Azure에 업로드하고 나면 구독 ID 및 `.pem` 파일의 경로를 **ServiceManagementService**에 전달하여 Azure 관리 끝점에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-132">After you have obtained your subscription ID, created a certificate, and uploaded the `.cer` file to Azure, you can connect to the Azure management endpoint by passing the subscription id and the path to the `.pem` file to **ServiceManagementService**:</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = '<path_to_.pem_certificate>'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="59b0b-133">앞의 예제에서 `sms` 은 **ServiceManagementService** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-133">In the preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="59b0b-134">**ServiceManagementService** 클래스는 Azure 서비스를 관리하는 데 사용되는 주 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-134">The **ServiceManagementService** class is the primary class used to manage Azure services.</span></span>

### <a name="management-certificates-on-windows-makecert"></a><span data-ttu-id="59b0b-135">Windows의 관리 인증서(MakeCert)</span><span class="sxs-lookup"><span data-stu-id="59b0b-135">Management certificates on Windows (MakeCert)</span></span>
<span data-ttu-id="59b0b-136">`makecert.exe`를 사용하여 컴퓨터에 자체 서명된 관리 인증서를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-136">You can create a self-signed management certificate on your machine using `makecert.exe`.</span></span>  <span data-ttu-id="59b0b-137">**Visual Studio 명령 프롬프트**를 **관리자**로 열고 *AzureCertificate*를 사용할 인증서 이름으로 바꿔서 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-137">Open a **Visual Studio command prompt** as an **administrator** and use the following command, replacing *AzureCertificate* with the certificate name you would like to use.</span></span>

    makecert -sky exchange -r -n "CN=AzureCertificate" -pe -a sha1 -len 2048 -ss My "AzureCertificate.cer"

<span data-ttu-id="59b0b-138">이 명령은 `.cer` 파일을 만들고 만든 파일을 **개인** 인증서 저장소에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-138">The command creates the `.cer` file, and installs it in the **Personal** certificate store.</span></span> <span data-ttu-id="59b0b-139">자세한 내용은 [Azure Cloud Services 인증서 개요](cloud-services-certs-create.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59b0b-139">For more information, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span>

<span data-ttu-id="59b0b-140">인증서를 만든 후에는 [Azure 클래식 포털][management-portal]에서 "설정" 탭의 "업로드" 작업을 통해 `.cer` 파일을 Azure에 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-140">After you have created the certificate, you need to upload the `.cer` file to Azure via the "Upload" action of the "Settings" tab of the [Azure classic portal][management-portal].</span></span>

<span data-ttu-id="59b0b-141">구독 ID를 얻어 인증서를 만들고 `.cer` 파일을 Azure에 업로드하고 나면 구독 ID 및 **개인** 인증서 저장소에 있는 인증서의 위치를 **ServiceManagementService**에 전달하여(다시 말해, *AzureCertificate*를 인증서 이름으로 바꿈) Azure 관리 끝점에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-141">After you have obtained your subscription ID, created a certificate, and uploaded the `.cer` file to Azure, you can connect to the Azure management endpoint by passing the subscription id and the location of the certificate in your **Personal** certificate store to **ServiceManagementService** (again, replace *AzureCertificate* with the name of your certificate):</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = 'CURRENT_USER\\my\\AzureCertificate'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="59b0b-142">앞의 예제에서 `sms` 은 **ServiceManagementService** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-142">In the preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="59b0b-143">**ServiceManagementService** 클래스는 Azure 서비스를 관리하는 데 사용되는 주 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-143">The **ServiceManagementService** class is the primary class used to manage Azure services.</span></span>

## <span data-ttu-id="59b0b-144"><a name="ListAvailableLocations"> </a>방법: 사용 가능한 위치 나열</span><span class="sxs-lookup"><span data-stu-id="59b0b-144"><a name="ListAvailableLocations"> </a>How to: List available locations</span></span>
<span data-ttu-id="59b0b-145">서비스를 호스트하는 데 사용할 수 있는 위치를 나열하려면 **list\_locations** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-145">To list the locations that are available for hosting services, use the **list\_locations** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_locations()
    for location in result:
        print(location.name)

<span data-ttu-id="59b0b-146">클라우드 서비스 또는 저장소 서비스를 만드는 경우 유효한 위치를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-146">When you create a cloud service or storage service you need to provide a valid location.</span></span> <span data-ttu-id="59b0b-147">**list\_locations** 메서드는 항상 현재 사용 가능한 위치의 최신 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-147">The **list\_locations** method always returns an up-to-date list of the currently available locations.</span></span> <span data-ttu-id="59b0b-148">현재 사용 가능한 위치는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-148">As of this writing, the available locations are:</span></span>

* <span data-ttu-id="59b0b-149">서유럽</span><span class="sxs-lookup"><span data-stu-id="59b0b-149">West Europe</span></span>
* <span data-ttu-id="59b0b-150">북유럽</span><span class="sxs-lookup"><span data-stu-id="59b0b-150">North Europe</span></span>
* <span data-ttu-id="59b0b-151">동남아시아</span><span class="sxs-lookup"><span data-stu-id="59b0b-151">Southeast Asia</span></span>
* <span data-ttu-id="59b0b-152">동아시아</span><span class="sxs-lookup"><span data-stu-id="59b0b-152">East Asia</span></span>
* <span data-ttu-id="59b0b-153">미국 중부</span><span class="sxs-lookup"><span data-stu-id="59b0b-153">Central US</span></span>
* <span data-ttu-id="59b0b-154">미국 중북부</span><span class="sxs-lookup"><span data-stu-id="59b0b-154">North Central US</span></span>
* <span data-ttu-id="59b0b-155">미국 중남부</span><span class="sxs-lookup"><span data-stu-id="59b0b-155">South Central US</span></span>
* <span data-ttu-id="59b0b-156">미국 서부</span><span class="sxs-lookup"><span data-stu-id="59b0b-156">West US</span></span>
* <span data-ttu-id="59b0b-157">미국 동부</span><span class="sxs-lookup"><span data-stu-id="59b0b-157">East US</span></span>
* <span data-ttu-id="59b0b-158">일본 동부</span><span class="sxs-lookup"><span data-stu-id="59b0b-158">Japan East</span></span>
* <span data-ttu-id="59b0b-159">일본 서부</span><span class="sxs-lookup"><span data-stu-id="59b0b-159">Japan West</span></span>
* <span data-ttu-id="59b0b-160">브라질 남부</span><span class="sxs-lookup"><span data-stu-id="59b0b-160">Brazil South</span></span>
* <span data-ttu-id="59b0b-161">오스트레일리아 동부</span><span class="sxs-lookup"><span data-stu-id="59b0b-161">Australia East</span></span>
* <span data-ttu-id="59b0b-162">오스트레일리아 남동부</span><span class="sxs-lookup"><span data-stu-id="59b0b-162">Australia Southeast</span></span>

## <span data-ttu-id="59b0b-163"><a name="CreateCloudService"> </a>방법: 클라우드 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="59b0b-163"><a name="CreateCloudService"> </a>How to: Create a cloud service</span></span>
<span data-ttu-id="59b0b-164">응용 프로그램을 만들어 Azure에서 실행하면 코드와 구성은 모두 Azure [클라우드 서비스][cloud service](이전 Azure 릴리스에서는 *호스티드 서비스*라 함)라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-164">When you create an application and run it in Azure, the code and configuration together are called an Azure [cloud service][cloud service] (known as a *hosted service* in earlier Azure releases).</span></span> <span data-ttu-id="59b0b-165">**create\_hosted\_service** 메서드를 통해 호스팅 서비스 이름(Azure에서 고유해야 함), 레이블(base64로 자동 인코딩됨), 설명 및 위치를 제공하여 새 호스팅 서비스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-165">The **create\_hosted\_service** method allows you to create a new hosted service by providing a hosted service name (which must be unique in Azure), a label (automatically encoded to base64), a description, and a location.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myhostedservice'
    label = 'myhostedservice'
    desc = 'my hosted service'
    location = 'West US'

    sms.create_hosted_service(name, label, desc, location)

<span data-ttu-id="59b0b-166">**list\_hosted\_services** 메서드로 구독의 모든 호스팅 서비스를 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-166">You can list all the hosted services for your subscription with the **list\_hosted\_services** method:</span></span>

    result = sms.list_hosted_services()

    for hosted_service in result:
        print('Service name: ' + hosted_service.service_name)
        print('Management URL: ' + hosted_service.url)
        print('Location: ' + hosted_service.hosted_service_properties.location)
        print('')

<span data-ttu-id="59b0b-167">특정 호스티드 서비스에 대한 정보를 가져오려는 경우 호스티드 서비스 이름을 **get\_hosted\_service\_properties** 메서드에 전달하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-167">If you want to get information about a particular hosted service, you can do so by passing the hosted service name to the **get\_hosted\_service\_properties** method:</span></span>

    hosted_service = sms.get_hosted_service_properties('myhostedservice')

    print('Service name: ' + hosted_service.service_name)
    print('Management URL: ' + hosted_service.url)
    print('Location: ' + hosted_service.hosted_service_properties.location)

<span data-ttu-id="59b0b-168">클라우드 서비스를 만든 후 **create\_deployment** 메서드를 사용하여 코드를 서비스에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-168">After you have created a cloud service, you can deploy your code to the service with the **create\_deployment** method.</span></span>

## <span data-ttu-id="59b0b-169"><a name="DeleteCloudService"> </a>방법: 클라우드 서비스 삭제</span><span class="sxs-lookup"><span data-stu-id="59b0b-169"><a name="DeleteCloudService"> </a>How to: Delete a cloud service</span></span>
<span data-ttu-id="59b0b-170">서비스 이름을 **delete\_hosted\_service** 메서드에 전달하여 클라우드 서비스를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-170">You can delete a cloud service by passing the service name to the **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service('myhostedservice')

<span data-ttu-id="59b0b-171">서비스의 모든 배포를 먼저 삭제해야 서비스를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-171">Before you can delete a service, all deployments for the service must first be deleted.</span></span> <span data-ttu-id="59b0b-172">자세한 내용은 [방법: 배포 삭제](#DeleteDeployment) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59b0b-172">(See [How to: Delete a deployment](#DeleteDeployment) for details.)</span></span>

## <span data-ttu-id="59b0b-173"><a name="DeleteDeployment"> </a>방법: 배포 삭제</span><span class="sxs-lookup"><span data-stu-id="59b0b-173"><a name="DeleteDeployment"> </a>How to: Delete a deployment</span></span>
<span data-ttu-id="59b0b-174">배포를 삭제하려면 **delete\_deployment** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-174">To delete a deployment, use the **delete\_deployment** method.</span></span> <span data-ttu-id="59b0b-175">다음 예제에서는 이름이 `v1`인 배포를 삭제하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-175">The following example shows how to delete a deployment named `v1`.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment('myhostedservice', 'v1')

## <span data-ttu-id="59b0b-176"><a name="CreateStorageService"> </a>방법: 저장소 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="59b0b-176"><a name="CreateStorageService"> </a>How to: Create a storage service</span></span>
<span data-ttu-id="59b0b-177">[저장소 서비스](../storage/common/storage-create-storage-account.md)로 Azure [Blob](../storage/blobs/storage-python-how-to-use-blob-storage.md), [테이블](../cosmos-db/table-storage-how-to-use-python.md), [큐](../storage/queues/storage-python-how-to-use-queue-storage.md)에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-177">A [storage service](../storage/common/storage-create-storage-account.md) gives you access to Azure [Blobs](../storage/blobs/storage-python-how-to-use-blob-storage.md), [Tables](../cosmos-db/table-storage-how-to-use-python.md), and [Queues](../storage/queues/storage-python-how-to-use-queue-storage.md).</span></span> <span data-ttu-id="59b0b-178">저장소 서비스를 만들려면 서비스(3자에서 24자 사이의 소문자로서 Azure 내에서 고유해야 함), 설명, 레이블(base64로 자동 인코딩되며 최대 100자까지 가능) 및 위치에 대해 이름이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-178">To create a storage service, you need a name for the service (between 3 and 24 lowercase characters and unique within Azure), a description, a label (up to 100 characters, automatically encoded to base64), and a location.</span></span> <span data-ttu-id="59b0b-179">다음 예제에서는 위치를 지정하여 저장소 서비스를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-179">The following example shows how to create a storage service by specifying a location.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mystorageaccount'
    label = 'mystorageaccount'
    location = 'West US'
    desc = 'My storage account description.'

    result = sms.create_storage_account(name, desc, label, location=location)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

<span data-ttu-id="59b0b-180">앞의 예제에서 **create\_storage\_account** 작업 상태는 **create\_storage\_account**가 반환한 결과를 **get\_operation\_status** 메서드에 전달하여 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-180">Note in the preceding example that the status of the **create\_storage\_account** operation can be retrieved by passing the result returned by **create\_storage\_account** to the **get\_operation\_status** method.</span></span>  

<span data-ttu-id="59b0b-181">**list\_storage\_accounts** 메서드로 저장소 계정 및 그 속성을 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-181">You can list your storage accounts and their properties with the **list\_storage\_accounts** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_storage_accounts()
    for account in result:
        print('Service name: ' + account.service_name)
        print('Location: ' + account.storage_service_properties.location)
        print('')

## <span data-ttu-id="59b0b-182"><a name="DeleteStorageService"> </a>방법: 저장소 서비스 삭제</span><span class="sxs-lookup"><span data-stu-id="59b0b-182"><a name="DeleteStorageService"> </a>How to: Delete a storage service</span></span>
<span data-ttu-id="59b0b-183">저장소 서비스 이름을 **delete\_storage\_account** 메서드에 전달하여 저장소 서비스를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-183">You can delete a storage service by passing the storage service name to the **delete\_storage\_account** method.</span></span> <span data-ttu-id="59b0b-184">저장소 서비스를 삭제하면 그 서비스에 저장되어 있는 모든 데이터(Blob, 테이블, 큐)가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-184">Deleting a storage service deletes all data stored in the service (blobs, tables, and queues).</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_storage_account('mystorageaccount')

## <span data-ttu-id="59b0b-185"><a name="ListOperatingSystems"> </a>방법: 사용 가능한 운영 체제 나열</span><span class="sxs-lookup"><span data-stu-id="59b0b-185"><a name="ListOperatingSystems"> </a>How to: List available operating systems</span></span>
<span data-ttu-id="59b0b-186">서비스를 호스트하는 데 사용할 수 있는 운영 체제를 나열하려면 **list\_operating\_systems** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-186">To list the operating systems that are available for hosting services, use the **list\_operating\_systems** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_operating_systems()

    for os in result:
        print('OS: ' + os.label)
        print('Family: ' + os.family_label)
        print('Active: ' + str(os.is_active))

<span data-ttu-id="59b0b-187">또는 운영 체제를 제품군별로 그룹화하는 **list\_operating\_system\_families** 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-187">Alternatively, you can use the **list\_operating\_system\_families** method, which groups the operating systems by family:</span></span>

    result = sms.list_operating_system_families()

    for family in result:
        print('Family: ' + family.label)
        for os in family.operating_systems:
            if os.is_active:
                print('OS: ' + os.label)
                print('Version: ' + os.version)
        print('')

## <span data-ttu-id="59b0b-188"><a name="CreateVMImage"> </a>방법: 운영 체제 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="59b0b-188"><a name="CreateVMImage"> </a>How to: Create an operating system image</span></span>
<span data-ttu-id="59b0b-189">운영 체제 이미지를 이미지 리포지토리에 추가하려면 **add\_os\_image** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-189">To add an operating system image to the image repository, use the **add\_os\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mycentos'
    label = 'mycentos'
    os = 'Linux' # Linux or Windows
    media_link = 'url_to_storage_blob_for_source_image_vhd'

    result = sms.add_os_image(label, media_link, name, os)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

<span data-ttu-id="59b0b-190">사용 가능한 운영 체제 이미지를 나열하려면 **list\_os\_images** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-190">To list the operating system images that are available, use the **list\_os\_images** method.</span></span> <span data-ttu-id="59b0b-191">여기에는 모든 플랫폼 이미지 및 사용자 이미지가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-191">It includes all platform images and user images:</span></span>

    result = sms.list_os_images()

    for image in result:
        print('Name: ' + image.name)
        print('Label: ' + image.label)
        print('OS: ' + image.os)
        print('Category: ' + image.category)
        print('Description: ' + image.description)
        print('Location: ' + image.location)
        print('Media link: ' + image.media_link)
        print('')

## <span data-ttu-id="59b0b-192"><a name="DeleteVMImage"> </a>방법: 운영 체제 이미지 삭제</span><span class="sxs-lookup"><span data-stu-id="59b0b-192"><a name="DeleteVMImage"> </a>How to: Delete an operating system image</span></span>
<span data-ttu-id="59b0b-193">사용자 이미지를 삭제하려면 **delete\_os\_image** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-193">To delete a user image, use the **delete\_os\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.delete_os_image('mycentos')

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

## <span data-ttu-id="59b0b-194"><a name="CreateVM"> </a>방법: 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="59b0b-194"><a name="CreateVM"> </a>How to: Create a virtual machine</span></span>
<span data-ttu-id="59b0b-195">가상 컴퓨터를 만들려면 먼저 [클라우드 서비스](#CreateCloudService)를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-195">To create a virtual machine, you first need to create a [cloud service](#CreateCloudService).</span></span>  <span data-ttu-id="59b0b-196">그런 다음 **create\_virtual\_machine\_deployment** 메서드를 사용하여 가상 컴퓨터 배포를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-196">Then create the virtual machine deployment using the **create\_virtual\_machine\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set the location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    # Name of an os image as returned by list_os_images
    image_name = 'OpenLogic__OpenLogic-CentOS-62-20120531-en-us-30GB.vhd'

    # Destination storage account container/blob where the VM disk
    # will be created
    media_link = 'url_to_target_storage_blob_for_vm_hd'

    # Linux VM configuration, you can use WindowsConfigurationSet
    # for a Windows VM instead
    linux_config = LinuxConfigurationSet('myhostname', 'myuser', 'mypassword', True)

    os_hd = OSVirtualHardDisk(image_name, media_link)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=os_hd,
        role_size='Small')

## <span data-ttu-id="59b0b-197"><a name="DeleteVM"> </a>방법: 가상 컴퓨터 삭제</span><span class="sxs-lookup"><span data-stu-id="59b0b-197"><a name="DeleteVM"> </a>How to: Delete a virtual machine</span></span>
<span data-ttu-id="59b0b-198">가상 컴퓨터를 삭제하려면 **delete\_deployment** 메서드를 사용하여 먼저 배포를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-198">To delete a virtual machine, you first delete the deployment using the **delete\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment(service_name='myvm',
        deployment_name='myvm')

<span data-ttu-id="59b0b-199">그런 다음 **delete\_hosted\_service** 메서드를 사용하여 클라우드 서비스를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-199">The cloud service can then be deleted using the **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service(service_name='myvm')

## <a name="how-to-create-a-virtual-machine-from-a-captured-virtual-machine-image"></a><span data-ttu-id="59b0b-200">방법: 캡처된 가상 컴퓨터 이미지에서 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="59b0b-200">How To: Create a Virtual Machine from a Captured Virtual Machine Image</span></span>
<span data-ttu-id="59b0b-201">VM 이미지를 캡처하기 위해 먼저 **capture\_vm\_image** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-201">To capture a VM image, you first call the **capture\_vm\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    # replace the below three parameters with actual values
    hosted_service_name = 'hs1'
    deployment_name = 'dep1'
    vm_name = 'vm1'

    image_name = vm_name + 'image'
    image = CaptureRoleAsVMImage    ('Specialized',
        image_name,
        image_name + 'label',
        image_name + 'description',
        'english',
        'mygroup')

    result = sms.capture_vm_image(
            hosted_service_name,
            deployment_name,
            vm_name,
            image
        )

<span data-ttu-id="59b0b-202">그런 다음 이미지가 캡처되었는지 확인하기 위해 **list\_vm\_images** API를 사용하여 이미지가 결과에 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-202">Next, to make sure that you have successfully captured the image, use the **list\_vm\_images** api, and make sure your image is displayed in the results:</span></span>

    images = sms.list_vm_images()

<span data-ttu-id="59b0b-203">최종적으로 캡처된 이미지를 사용하여 가상 컴퓨터를 만들기 위해 이전처럼 **create\_virtual\_machine\_deployment** 메서드를 사용하지만, 이번에는 대신 vm_image_name을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-203">To finally create the virtual machine using the captured image, use the **create\_virtual\_machine\_deployment** method as before, but this time pass in the vm_image_name instead</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set the location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=None,
        role_size='Small',
        vm_image_name = image_name)

<span data-ttu-id="59b0b-204">Linux 가상 컴퓨터를 캡처하는 방법에 대한 자세한 내용은 [Linux 가상 컴퓨터를 캡처하는 방법](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59b0b-204">To learn more about how to capture a Linux Virtual Machine, see [How to Capture a Linux Virtual Machine.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="59b0b-205">Windows 가상 컴퓨터를 캡처하는 방법에 대한 자세한 내용은 [Windows 가상 컴퓨터를 캡처하는 방법](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59b0b-205">To learn more about how to capture a Windows Virtual Machine, see [How to Capture a Windows Virtual Machine.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="59b0b-206"><a name="What's Next"> </a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="59b0b-206"><a name="What's Next"> </a>Next Steps</span></span>
<span data-ttu-id="59b0b-207">서비스 관리의 기본 사항을 배웠으므로 이제 [Azure Python SDK에 대한 전체 API 참조 설명서](http://azure-sdk-for-python.readthedocs.org/) 에 액세스하고 쉽게 복잡한 작업을 수행하여 Python 응용 프로그램을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59b0b-207">Now that you've learned the basics of service management, you can access the [Complete API reference documentation for the Azure Python SDK](http://azure-sdk-for-python.readthedocs.org/) and perform complex tasks easily to manage your python application.</span></span>

<span data-ttu-id="59b0b-208">자세한 내용은 [Python 개발자 센터](/develop/python/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59b0b-208">For more information, see the [Python Developer Center](/develop/python/).</span></span>

[What is Service Management]: #WhatIs
[Concepts]: #Concepts
[How to: Connect to service management]: #Connect
[How to: List available locations]: #ListAvailableLocations
[How to: Create a cloud service]: #CreateCloudService
[How to: Delete a cloud service]: #DeleteCloudService
[How to: Create a deployment]: #CreateDeployment
[How to: Update a deployment]: #UpdateDeployment
[How to: Move deployments between staging and production]: #MoveDeployments
[How to: Delete a deployment]: #DeleteDeployment
[How to: Create a storage service]: #CreateStorageService
[How to: Delete a storage service]: #DeleteStorageService
[How to: List available operating systems]: #ListOperatingSystems
[How to: Create an operating system image]: #CreateVMImage
[How to: Delete an operating system image]: #DeleteVMImage
[How to: Create a virtual machine]: #CreateVM
[How to: Delete a virtual machine]: #DeleteVM
[Next Steps]: #NextSteps
[management-portal]: https://manage.windowsazure.com/
[svc-mgmt-rest-api]: http://msdn.microsoft.com/library/windowsazure/ee460799.aspx


[cloud service]:/services/cloud-services/
