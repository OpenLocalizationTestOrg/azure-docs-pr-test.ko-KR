---
title: "aaaHow toouse hello 서비스 관리 API (Python)-기능 가이드"
description: "Tooprogrammatically Python에서 일반적인 서비스 관리 작업을 수행 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: b59622203470e1586484cec4033515edb39ca4d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-management-from-python"></a><span data-ttu-id="5ce0f-103">어떻게 toouse Python에서 서비스 관리</span><span class="sxs-lookup"><span data-stu-id="5ce0f-103">How toouse Service Management from Python</span></span>
<span data-ttu-id="5ce0f-104">이 가이드에서는 tooprogrammatically Python에서 서비스 관리 작업을 수행 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-104">This guide shows you how tooprogrammatically perform common service management tasks from Python.</span></span> <span data-ttu-id="5ce0f-105">hello **ServiceManagementService** hello 클래스 [Python 용 Azure SDK](https://github.com/Azure/azure-sdk-for-python) hello 서비스 관리 관련 기능 hello 에서에서사용할수있는프로그래밍방식액세스toomuch지원[Azure 클래식 포털] [ management-portal] (예: **만들기, 업데이트 및 클라우드 서비스, 배포, 데이터 관리 서비스 및 가상 컴퓨터 삭제**).</span><span class="sxs-lookup"><span data-stu-id="5ce0f-105">hello **ServiceManagementService** class in hello [Azure SDK for Python](https://github.com/Azure/azure-sdk-for-python) supports programmatic access toomuch of hello service management-related functionality that is available in hello [Azure classic portal][management-portal] (such as **creating, updating, and deleting cloud services, deployments, data management services, and virtual machines**).</span></span> <span data-ttu-id="5ce0f-106">이 기능에 프로그래밍 방식 액세스 tooservice 관리 해야 하는 응용 프로그램을 구축 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-106">This functionality can be useful in building applications that need programmatic access tooservice management.</span></span>

## <span data-ttu-id="5ce0f-107"><a name="WhatIs"> </a>서비스 관리 정의</span><span class="sxs-lookup"><span data-stu-id="5ce0f-107"><a name="WhatIs"> </a>What is Service Management</span></span>
<span data-ttu-id="5ce0f-108">프로그래밍 방식 액세스 toomuch hello를 통해 사용할 수 있는 hello 서비스 관리 기능을 제공 하는 hello 서비스 관리 API [Azure 클래식 포털][management-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-108">hello Service Management API provides programmatic access toomuch of hello service management functionality available through hello [Azure classic portal][management-portal].</span></span> <span data-ttu-id="5ce0f-109">Python 용 Azure SDK hello toomanage을 사용 하면 클라우드 서비스 및 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-109">hello Azure SDK for Python allows you toomanage your cloud services and storage accounts.</span></span>

<span data-ttu-id="5ce0f-110">toouse hello 서비스 관리 API를 필요한 너무[Azure 계정을 만들려면](https://azure.microsoft.com/pricing/free-trial/)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-110">toouse hello Service Management API, you need too[create an Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <span data-ttu-id="5ce0f-111"><a name="Concepts"> </a>개념</span><span class="sxs-lookup"><span data-stu-id="5ce0f-111"><a name="Concepts"> </a>Concepts</span></span>
<span data-ttu-id="5ce0f-112">Python 용 Azure SDK hello 래핑합니다 hello [Azure 서비스 관리 API][svc-mgmt-rest-api], 하는 REST API입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-112">hello Azure SDK for Python wraps hello [Azure Service Management API][svc-mgmt-rest-api], which is a REST API.</span></span> <span data-ttu-id="5ce0f-113">모든 API 작업은 SSL을 통해 수행되고 X.509 v3 인증서를 사용하여 서로 인증됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-113">All API operations are performed over SSL and mutually authenticated using X.509 v3 certificates.</span></span> <span data-ttu-id="5ce0f-114">hello 관리 서비스는 Azure에서 또는 hello 인터넷을 통해 직접 HTTPS 요청을 보내고 HTTPS 응답을 받을 수 있는 모든 응용 프로그램에서 실행 되는 서비스 내에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-114">hello management service may be accessed from within a service running in Azure, or directly over hello Internet from any application that can send an HTTPS request and receive an HTTPS response.</span></span>

## <span data-ttu-id="5ce0f-115"><a name="Installation"> </a>설치</span><span class="sxs-lookup"><span data-stu-id="5ce0f-115"><a name="Installation"> </a>Installation</span></span>
<span data-ttu-id="5ce0f-116">Hello에 사용할 수 있는이 문서에서 설명 하는 모든 hello 기능 `azure-servicemanagement-legacy` 패키지는 pip를 사용 하 여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-116">All hello features described in this article are available in hello `azure-servicemanagement-legacy` package, which you can install using pip.</span></span> <span data-ttu-id="5ce0f-117">설치 (예: 새 tooPython 하려는 경우)에 대 한 자세한 내용은이 문서를 참조 하십시오.: [Python 설치 및 hello Azure SDK](../python-how-to-install.md)</span><span class="sxs-lookup"><span data-stu-id="5ce0f-117">For more information about installation (for example, if you are new tooPython), see this article: [Installing Python and hello Azure SDK](../python-how-to-install.md)</span></span>

## <span data-ttu-id="5ce0f-118"><a name="Connect"></a>하는 방법: tooservice management 연결</span><span class="sxs-lookup"><span data-stu-id="5ce0f-118"><a name="Connect"> </a>How to: Connect tooservice management</span></span>
<span data-ttu-id="5ce0f-119">Azure 구독 ID와 유효한 관리 인증서 tooconnect toohello 서비스 관리 끝점 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-119">tooconnect toohello Service Management endpoint, you need your Azure subscription ID and a valid management certificate.</span></span> <span data-ttu-id="5ce0f-120">Hello 통해 구독 ID를 가져올 수 있습니다 [Azure 클래식 포털][management-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-120">You can obtain your subscription ID through hello [Azure classic portal][management-portal].</span></span>

> [!NOTE]
> <span data-ttu-id="5ce0f-121">이제 Windows에서 실행 되는 경우에 OpenSSL을 사용 하 여 만든 가능한 toouse 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-121">It is now possible toouse certificates created with OpenSSL when running on Windows.</span></span>  <span data-ttu-id="5ce0f-122">Python 2.7.4 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-122">It requires Python 2.7.4 or later.</span></span> <span data-ttu-id="5ce0f-123">.Pfx 인증서 hello 미래에서는 제거 될 가능성이 대 한 지원을 이후.pfx, 대신 사용자가 toouse OpenSSL을 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-123">We recommend users toouse OpenSSL instead of .pfx, since support for .pfx certificates will likely be removed in hello future.</span></span>
>
>

### <a name="management-certificates-on-windowsmaclinux-openssl"></a><span data-ttu-id="5ce0f-124">Windows/Mac/Linux의 관리 인증서(OpenSSL)</span><span class="sxs-lookup"><span data-stu-id="5ce0f-124">Management certificates on Windows/Mac/Linux (OpenSSL)</span></span>
<span data-ttu-id="5ce0f-125">사용할 수 있습니다 [OpenSSL](http://www.openssl.org/) toocreate 관리 인증서.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-125">You can use [OpenSSL](http://www.openssl.org/) toocreate your management certificate.</span></span>  <span data-ttu-id="5ce0f-126">실제로 hello 서버에 대 한 toocreate 두 개의 인증서가 필요 (한 `.cer` 파일) hello 클라이언트에 대 한 하나 (한 `.pem` 파일).</span><span class="sxs-lookup"><span data-stu-id="5ce0f-126">You actually need toocreate two certificates, one for hello server (a `.cer` file) and one for hello client (a `.pem` file).</span></span> <span data-ttu-id="5ce0f-127">toocreate hello `.pem` 파일을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-127">toocreate hello `.pem` file, execute:</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="5ce0f-128">toocreate hello `.cer` 인증서, 실행:</span><span class="sxs-lookup"><span data-stu-id="5ce0f-128">toocreate hello `.cer` certificate, execute:</span></span>

    openssl x509 -inform pem -in mycert.pem -outform der -out mycert.cer

<span data-ttu-id="5ce0f-129">Azure 인증서에 대한 자세한 내용은 [Azure 클라우드 서비스 인증서](cloud-services-certs-create.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-129">For more information about Azure certificates, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="5ce0f-130">OpenSSL 매개 변수 설명과 hello 설명서를 참조 [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-130">For a complete description of OpenSSL parameters, see hello documentation at [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span></span>

<span data-ttu-id="5ce0f-131">Tooupload hello 이러한 파일을 만든 후 해야 `.cer` tooAzure hello의 hello "설정" 탭의 hello "업로드 하세요." 동작을 통해 파일 [Azure 클래식 포털][management-portal], toomake 기록 필요 hello 저장 `.pem` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-131">After you have created these files, you need tooupload hello `.cer` file tooAzure via hello "Upload" action of hello "Settings" tab of hello [Azure classic portal][management-portal], and you need toomake note of where you saved hello `.pem` file.</span></span>

<span data-ttu-id="5ce0f-132">구독 ID를 가져온 후 인증서를 만들고 업로드 hello `.cer` 파일 tooAzure toohello Azure 관리 끝점 hello 구독 id로, hello 경로 toohello 전달 하 여 연결할 수 있습니다 `.pem` 파일 너무**ServiceManagementService**:</span><span class="sxs-lookup"><span data-stu-id="5ce0f-132">After you have obtained your subscription ID, created a certificate, and uploaded hello `.cer` file tooAzure, you can connect toohello Azure management endpoint by passing hello subscription id and hello path toohello `.pem` file too**ServiceManagementService**:</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = '<path_to_.pem_certificate>'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="5ce0f-133">Hello 예제에서는 앞에서 `sms` 는 **ServiceManagementService** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-133">In hello preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="5ce0f-134">hello **ServiceManagementService** 클래스 hello 사용 되는 기본 클래스 toomanage Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-134">hello **ServiceManagementService** class is hello primary class used toomanage Azure services.</span></span>

### <a name="management-certificates-on-windows-makecert"></a><span data-ttu-id="5ce0f-135">Windows의 관리 인증서(MakeCert)</span><span class="sxs-lookup"><span data-stu-id="5ce0f-135">Management certificates on Windows (MakeCert)</span></span>
<span data-ttu-id="5ce0f-136">`makecert.exe`를 사용하여 컴퓨터에 자체 서명된 관리 인증서를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-136">You can create a self-signed management certificate on your machine using `makecert.exe`.</span></span>  <span data-ttu-id="5ce0f-137">열기는 **Visual Studio 명령 프롬프트** 로 **관리자** 다음 명령을, 대체 hello를 사용 하 여 *AzureCertificate* 원하는 hello 인증서 이름으로 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-137">Open a **Visual Studio command prompt** as an **administrator** and use hello following command, replacing *AzureCertificate* with hello certificate name you would like toouse.</span></span>

    makecert -sky exchange -r -n "CN=AzureCertificate" -pe -a sha1 -len 2048 -ss My "AzureCertificate.cer"

<span data-ttu-id="5ce0f-138">hello 명령은 hello `.cer` 파일과 hello에 설치 **개인** 인증서 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-138">hello command creates hello `.cer` file, and installs it in hello **Personal** certificate store.</span></span> <span data-ttu-id="5ce0f-139">자세한 내용은 [Azure Cloud Services 인증서 개요](cloud-services-certs-create.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-139">For more information, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span>

<span data-ttu-id="5ce0f-140">Tooupload hello hello 인증서를 만든 후 해야 `.cer` tooAzure hello의 hello "설정" 탭의 hello "업로드 하세요." 동작을 통해 파일 [Azure 클래식 포털][management-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-140">After you have created hello certificate, you need tooupload hello `.cer` file tooAzure via hello "Upload" action of hello "Settings" tab of hello [Azure classic portal][management-portal].</span></span>

<span data-ttu-id="5ce0f-141">구독 ID를 가져온 후 인증서를 만들고 업로드 hello `.cer` 파일 tooAzure toohello Azure 관리 끝점에 프로그램 hello구독id로,hello인증서의hello위치를전달하여연결할수있습니다**개인** 인증서 저장소에 너무**ServiceManagementService** (다시 대체 *AzureCertificate* 인증서의 hello 이름의):</span><span class="sxs-lookup"><span data-stu-id="5ce0f-141">After you have obtained your subscription ID, created a certificate, and uploaded hello `.cer` file tooAzure, you can connect toohello Azure management endpoint by passing hello subscription id and hello location of hello certificate in your **Personal** certificate store too**ServiceManagementService** (again, replace *AzureCertificate* with hello name of your certificate):</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = 'CURRENT_USER\\my\\AzureCertificate'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="5ce0f-142">Hello 예제에서는 앞에서 `sms` 는 **ServiceManagementService** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-142">In hello preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="5ce0f-143">hello **ServiceManagementService** 클래스 hello 사용 되는 기본 클래스 toomanage Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-143">hello **ServiceManagementService** class is hello primary class used toomanage Azure services.</span></span>

## <span data-ttu-id="5ce0f-144"><a name="ListAvailableLocations"> </a>방법: 사용 가능한 위치 나열</span><span class="sxs-lookup"><span data-stu-id="5ce0f-144"><a name="ListAvailableLocations"> </a>How to: List available locations</span></span>
<span data-ttu-id="5ce0f-145">서비스를 호스트 하는 데 사용할 수 있는 toolist hello 위치가 사용 하는 hello **목록\_위치** 메서드:</span><span class="sxs-lookup"><span data-stu-id="5ce0f-145">toolist hello locations that are available for hosting services, use hello **list\_locations** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_locations()
    for location in result:
        print(location.name)

<span data-ttu-id="5ce0f-146">클라우드 서비스 또는 저장소 서비스를 만들 때 tooprovide 유효한 위치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-146">When you create a cloud service or storage service you need tooprovide a valid location.</span></span> <span data-ttu-id="5ce0f-147">hello **목록\_위치** 메서드는 항상 최신 hello 현재 사용할 수 있는 위치의 목록을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-147">hello **list\_locations** method always returns an up-to-date list of hello currently available locations.</span></span> <span data-ttu-id="5ce0f-148">이 문서의 작성일 hello 사용 가능한 위치는:</span><span class="sxs-lookup"><span data-stu-id="5ce0f-148">As of this writing, hello available locations are:</span></span>

* <span data-ttu-id="5ce0f-149">서유럽</span><span class="sxs-lookup"><span data-stu-id="5ce0f-149">West Europe</span></span>
* <span data-ttu-id="5ce0f-150">북유럽</span><span class="sxs-lookup"><span data-stu-id="5ce0f-150">North Europe</span></span>
* <span data-ttu-id="5ce0f-151">동남아시아</span><span class="sxs-lookup"><span data-stu-id="5ce0f-151">Southeast Asia</span></span>
* <span data-ttu-id="5ce0f-152">동아시아</span><span class="sxs-lookup"><span data-stu-id="5ce0f-152">East Asia</span></span>
* <span data-ttu-id="5ce0f-153">미국 중부</span><span class="sxs-lookup"><span data-stu-id="5ce0f-153">Central US</span></span>
* <span data-ttu-id="5ce0f-154">미국 중북부</span><span class="sxs-lookup"><span data-stu-id="5ce0f-154">North Central US</span></span>
* <span data-ttu-id="5ce0f-155">미국 중남부</span><span class="sxs-lookup"><span data-stu-id="5ce0f-155">South Central US</span></span>
* <span data-ttu-id="5ce0f-156">미국 서부</span><span class="sxs-lookup"><span data-stu-id="5ce0f-156">West US</span></span>
* <span data-ttu-id="5ce0f-157">미국 동부</span><span class="sxs-lookup"><span data-stu-id="5ce0f-157">East US</span></span>
* <span data-ttu-id="5ce0f-158">일본 동부</span><span class="sxs-lookup"><span data-stu-id="5ce0f-158">Japan East</span></span>
* <span data-ttu-id="5ce0f-159">일본 서부</span><span class="sxs-lookup"><span data-stu-id="5ce0f-159">Japan West</span></span>
* <span data-ttu-id="5ce0f-160">브라질 남부</span><span class="sxs-lookup"><span data-stu-id="5ce0f-160">Brazil South</span></span>
* <span data-ttu-id="5ce0f-161">오스트레일리아 동부</span><span class="sxs-lookup"><span data-stu-id="5ce0f-161">Australia East</span></span>
* <span data-ttu-id="5ce0f-162">오스트레일리아 남동부</span><span class="sxs-lookup"><span data-stu-id="5ce0f-162">Australia Southeast</span></span>

## <span data-ttu-id="5ce0f-163"><a name="CreateCloudService"> </a>방법: 클라우드 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="5ce0f-163"><a name="CreateCloudService"> </a>How to: Create a cloud service</span></span>
<span data-ttu-id="5ce0f-164">응용 프로그램을 만들 Azure에서 실행 hello 코드와 구성이 함께 라고 Azure 시점과 [클라우드 서비스] [ cloud service] (라고는 *호스 티 드 서비스* 에 이전 버전 Azure 릴리스).</span><span class="sxs-lookup"><span data-stu-id="5ce0f-164">When you create an application and run it in Azure, hello code and configuration together are called an Azure [cloud service][cloud service] (known as a *hosted service* in earlier Azure releases).</span></span> <span data-ttu-id="5ce0f-165">hello **만들\_호스팅된\_서비스** 방법을 사용 하면 toocreate 새 호스팅된 서비스는 호스팅된 서비스 이름 (Azure에서 고유 해야 함)를 제공 하 여 레이블 (자동으로 인코딩된 toobase64)는 설명 및 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-165">hello **create\_hosted\_service** method allows you toocreate a new hosted service by providing a hosted service name (which must be unique in Azure), a label (automatically encoded toobase64), a description, and a location.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myhostedservice'
    label = 'myhostedservice'
    desc = 'my hosted service'
    location = 'West US'

    sms.create_hosted_service(name, label, desc, location)

<span data-ttu-id="5ce0f-166">Hello로 구독에 대 한 모든 hello 호스팅된 서비스를 나열할 수 있습니다 **목록\_호스팅된\_서비스** 메서드:</span><span class="sxs-lookup"><span data-stu-id="5ce0f-166">You can list all hello hosted services for your subscription with hello **list\_hosted\_services** method:</span></span>

    result = sms.list_hosted_services()

    for hosted_service in result:
        print('Service name: ' + hosted_service.service_name)
        print('Management URL: ' + hosted_service.url)
        print('Location: ' + hosted_service.hosted_service_properties.location)
        print('')

<span data-ttu-id="5ce0f-167">특정 호스팅된 서비스에 대 한 tooget 정보를 원할 경우 후 그렇게 hello 호스팅 서비스 이름 toohello 전달 하 여 **가져오기\_호스팅된\_서비스\_속성** 메서드:</span><span class="sxs-lookup"><span data-stu-id="5ce0f-167">If you want tooget information about a particular hosted service, you can do so by passing hello hosted service name toohello **get\_hosted\_service\_properties** method:</span></span>

    hosted_service = sms.get_hosted_service_properties('myhostedservice')

    print('Service name: ' + hosted_service.service_name)
    print('Management URL: ' + hosted_service.url)
    print('Location: ' + hosted_service.hosted_service_properties.location)

<span data-ttu-id="5ce0f-168">클라우드 서비스를 만든 후 hello 사용 하 여 코드 toohello 서비스를 배포할 수 있습니다 **만들\_배포** 메서드.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-168">After you have created a cloud service, you can deploy your code toohello service with hello **create\_deployment** method.</span></span>

## <span data-ttu-id="5ce0f-169"><a name="DeleteCloudService"> </a>방법: 클라우드 서비스 삭제</span><span class="sxs-lookup"><span data-stu-id="5ce0f-169"><a name="DeleteCloudService"> </a>How to: Delete a cloud service</span></span>
<span data-ttu-id="5ce0f-170">서비스 이름 toohello hello를 전달 하 여 클라우드 서비스를 삭제 하려면 **삭제\_호스팅된\_서비스** 메서드:</span><span class="sxs-lookup"><span data-stu-id="5ce0f-170">You can delete a cloud service by passing hello service name toohello **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service('myhostedservice')

<span data-ttu-id="5ce0f-171">서비스를 삭제 하기 전에 hello 서비스에 대 한 모든 배포 먼저 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-171">Before you can delete a service, all deployments for hello service must first be deleted.</span></span> <span data-ttu-id="5ce0f-172">자세한 내용은 [방법: 배포 삭제](#DeleteDeployment) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-172">(See [How to: Delete a deployment](#DeleteDeployment) for details.)</span></span>

## <span data-ttu-id="5ce0f-173"><a name="DeleteDeployment"> </a>방법: 배포 삭제</span><span class="sxs-lookup"><span data-stu-id="5ce0f-173"><a name="DeleteDeployment"> </a>How to: Delete a deployment</span></span>
<span data-ttu-id="5ce0f-174">toodelete 해당 배포를 사용 하 여 hello **삭제\_배포** 메서드.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-174">toodelete a deployment, use hello **delete\_deployment** method.</span></span> <span data-ttu-id="5ce0f-175">hello 다음 예제에서는 어떻게 toodelete 배포 라는 `v1`합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-175">hello following example shows how toodelete a deployment named `v1`.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment('myhostedservice', 'v1')

## <span data-ttu-id="5ce0f-176"><a name="CreateStorageService"> </a>방법: 저장소 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="5ce0f-176"><a name="CreateStorageService"> </a>How to: Create a storage service</span></span>
<span data-ttu-id="5ce0f-177">A [저장소 서비스](../storage/common/storage-create-storage-account.md) 액세스할 수 있도록 tooAzure [Blob](../storage/blobs/storage-python-how-to-use-blob-storage.md), [테이블](../cosmos-db/table-storage-how-to-use-python.md), 및 [큐](../storage/queues/storage-python-how-to-use-queue-storage.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-177">A [storage service](../storage/common/storage-create-storage-account.md) gives you access tooAzure [Blobs](../storage/blobs/storage-python-how-to-use-blob-storage.md), [Tables](../cosmos-db/table-storage-how-to-use-python.md), and [Queues](../storage/queues/storage-python-how-to-use-queue-storage.md).</span></span> <span data-ttu-id="5ce0f-178">저장소 서비스 toocreate hello 서비스 (소문자 3 ~ 24 자 사이 및 Azure 내에서 고유)에 대 한 이름, 설명, too100 문자인 자동으로 인코딩된 toobase64), (위쪽 레이블 및 위치 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-178">toocreate a storage service, you need a name for hello service (between 3 and 24 lowercase characters and unique within Azure), a description, a label (up too100 characters, automatically encoded toobase64), and a location.</span></span> <span data-ttu-id="5ce0f-179">다음 예제는 hello toocreate 저장소 위치를 지정 하 여 처리할 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-179">hello following example shows how toocreate a storage service by specifying a location.</span></span>

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

<span data-ttu-id="5ce0f-180">해당 hello 상태의 hello 앞 예제는 hello에 언급 **만들\_저장소\_계정** 작업에서 반환 되는 hello 결과 전달 하 여 검색할 수 **만들\_저장소 \_계정** toohello **가져오기\_작업\_상태** 메서드.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-180">Note in hello preceding example that hello status of hello **create\_storage\_account** operation can be retrieved by passing hello result returned by **create\_storage\_account** toohello **get\_operation\_status** method.</span></span>  

<span data-ttu-id="5ce0f-181">저장소 계정 및 hello 사용 하 여 해당 속성을 나열할 수 **목록\_저장소\_계정** 메서드:</span><span class="sxs-lookup"><span data-stu-id="5ce0f-181">You can list your storage accounts and their properties with hello **list\_storage\_accounts** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_storage_accounts()
    for account in result:
        print('Service name: ' + account.service_name)
        print('Location: ' + account.storage_service_properties.location)
        print('')

## <span data-ttu-id="5ce0f-182"><a name="DeleteStorageService"> </a>방법: 저장소 서비스 삭제</span><span class="sxs-lookup"><span data-stu-id="5ce0f-182"><a name="DeleteStorageService"> </a>How to: Delete a storage service</span></span>
<span data-ttu-id="5ce0f-183">저장소 서비스 이름 toohello hello를 전달 하 여 저장소 서비스를 삭제 하려면 **삭제\_저장소\_계정** 메서드.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-183">You can delete a storage service by passing hello storage service name toohello **delete\_storage\_account** method.</span></span> <span data-ttu-id="5ce0f-184">저장소 서비스를 삭제 hello 서비스 (blob, 테이블 및 큐)에 저장 된 모든 데이터가 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-184">Deleting a storage service deletes all data stored in hello service (blobs, tables, and queues).</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_storage_account('mystorageaccount')

## <span data-ttu-id="5ce0f-185"><a name="ListOperatingSystems"> </a>방법: 사용 가능한 운영 체제 나열</span><span class="sxs-lookup"><span data-stu-id="5ce0f-185"><a name="ListOperatingSystems"> </a>How to: List available operating systems</span></span>
<span data-ttu-id="5ce0f-186">hello를 사용 하 여 서비스를 호스트 하는 데 사용할 수 있는 toolist hello 운영 체제 **목록\_운영\_시스템** 메서드:</span><span class="sxs-lookup"><span data-stu-id="5ce0f-186">toolist hello operating systems that are available for hosting services, use hello **list\_operating\_systems** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_operating_systems()

    for os in result:
        print('OS: ' + os.label)
        print('Family: ' + os.family_label)
        print('Active: ' + str(os.is_active))

<span data-ttu-id="5ce0f-187">Hello 또는 사용할 수 있습니다 **목록\_운영\_시스템\_제품군** hello 운영 체제 제품군 별로 그룹화 하는 메서드:</span><span class="sxs-lookup"><span data-stu-id="5ce0f-187">Alternatively, you can use hello **list\_operating\_system\_families** method, which groups hello operating systems by family:</span></span>

    result = sms.list_operating_system_families()

    for family in result:
        print('Family: ' + family.label)
        for os in family.operating_systems:
            if os.is_active:
                print('OS: ' + os.label)
                print('Version: ' + os.version)
        print('')

## <span data-ttu-id="5ce0f-188"><a name="CreateVMImage"> </a>방법: 운영 체제 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="5ce0f-188"><a name="CreateVMImage"> </a>How to: Create an operating system image</span></span>
<span data-ttu-id="5ce0f-189">운영 체제 이미지 toohello 이미지 리포지토리에 tooadd hello를 사용 하 여 **추가\_os\_이미지** 메서드:</span><span class="sxs-lookup"><span data-stu-id="5ce0f-189">tooadd an operating system image toohello image repository, use hello **add\_os\_image** method:</span></span>

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

<span data-ttu-id="5ce0f-190">toolist hello 운영 체제 이미지를 사용할 수 있는 hello를 사용 하 여 **목록\_os\_이미지** 메서드.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-190">toolist hello operating system images that are available, use hello **list\_os\_images** method.</span></span> <span data-ttu-id="5ce0f-191">여기에는 모든 플랫폼 이미지 및 사용자 이미지가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-191">It includes all platform images and user images:</span></span>

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

## <span data-ttu-id="5ce0f-192"><a name="DeleteVMImage"> </a>방법: 운영 체제 이미지 삭제</span><span class="sxs-lookup"><span data-stu-id="5ce0f-192"><a name="DeleteVMImage"> </a>How to: Delete an operating system image</span></span>
<span data-ttu-id="5ce0f-193">toodelete 사용자 이미지를 사용 하 여 hello **삭제\_os\_이미지** 메서드:</span><span class="sxs-lookup"><span data-stu-id="5ce0f-193">toodelete a user image, use hello **delete\_os\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.delete_os_image('mycentos')

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

## <span data-ttu-id="5ce0f-194"><a name="CreateVM"> </a>방법: 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="5ce0f-194"><a name="CreateVM"> </a>How to: Create a virtual machine</span></span>
<span data-ttu-id="5ce0f-195">가상 컴퓨터 toocreate 먼저 toocreate는 [클라우드 서비스](#CreateCloudService)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-195">toocreate a virtual machine, you first need toocreate a [cloud service](#CreateCloudService).</span></span>  <span data-ttu-id="5ce0f-196">그런 다음 hello를 사용 하 여 hello 가상 컴퓨터 배포를 만들 **만들\_가상\_컴퓨터\_배포** 메서드:</span><span class="sxs-lookup"><span data-stu-id="5ce0f-196">Then create hello virtual machine deployment using hello **create\_virtual\_machine\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set hello location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    # Name of an os image as returned by list_os_images
    image_name = 'OpenLogic__OpenLogic-CentOS-62-20120531-en-us-30GB.vhd'

    # Destination storage account container/blob where hello VM disk
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

## <span data-ttu-id="5ce0f-197"><a name="DeleteVM"> </a>방법: 가상 컴퓨터 삭제</span><span class="sxs-lookup"><span data-stu-id="5ce0f-197"><a name="DeleteVM"> </a>How to: Delete a virtual machine</span></span>
<span data-ttu-id="5ce0f-198">toodelete 가상 컴퓨터를 먼저 삭제 하면 hello를 사용 하 여 hello 배포 **삭제\_배포** 메서드:</span><span class="sxs-lookup"><span data-stu-id="5ce0f-198">toodelete a virtual machine, you first delete hello deployment using hello **delete\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment(service_name='myvm',
        deployment_name='myvm')

<span data-ttu-id="5ce0f-199">hello를 사용 하 여 hello 클라우드 서비스가 삭제 한 다음 수 **삭제\_호스팅된\_서비스** 메서드:</span><span class="sxs-lookup"><span data-stu-id="5ce0f-199">hello cloud service can then be deleted using hello **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service(service_name='myvm')

## <a name="how-to-create-a-virtual-machine-from-a-captured-virtual-machine-image"></a><span data-ttu-id="5ce0f-200">방법: 캡처된 가상 컴퓨터 이미지에서 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="5ce0f-200">How To: Create a Virtual Machine from a Captured Virtual Machine Image</span></span>
<span data-ttu-id="5ce0f-201">VM 이미지 toocapture 처음 호출 하면 hello **캡처\_vm\_이미지** 메서드:</span><span class="sxs-lookup"><span data-stu-id="5ce0f-201">toocapture a VM image, you first call hello **capture\_vm\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    # replace hello below three parameters with actual values
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

<span data-ttu-id="5ce0f-202">그런 다음, toomake 성공적으로 hello 이미지를 캡처한, hello를 사용 하 여 않았는지 **목록\_vm\_이미지** api를 이미지 hello 결과에 표시 되 고 있는지 확인:</span><span class="sxs-lookup"><span data-stu-id="5ce0f-202">Next, toomake sure that you have successfully captured hello image, use hello **list\_vm\_images** api, and make sure your image is displayed in hello results:</span></span>

    images = sms.list_vm_images()

<span data-ttu-id="5ce0f-203">toofinally hello 캡처된 이미지를 사용 하 여 hello 가상 컴퓨터를 만들고, hello를 사용 하 여 **만들\_가상\_컴퓨터\_배포** 앞, 하지만이 이번 전달 hello vm_image_name에 대신 메서드</span><span class="sxs-lookup"><span data-stu-id="5ce0f-203">toofinally create hello virtual machine using hello captured image, use hello **create\_virtual\_machine\_deployment** method as before, but this time pass in hello vm_image_name instead</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set hello location
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

<span data-ttu-id="5ce0f-204">toocapture Linux 가상 컴퓨터를 확인 하는 방법에 대해 더 알아봅니다을 toolearn [어떻게 tooCapture Linux 가상 컴퓨터.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="5ce0f-204">toolearn more about how toocapture a Linux Virtual Machine, see [How tooCapture a Linux Virtual Machine.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="5ce0f-205">toocapture Windows 가상 컴퓨터를 확인 하는 방법에 대해 더 알아봅니다을 toolearn [어떻게 tooCapture Windows 가상 컴퓨터.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="5ce0f-205">toolearn more about how toocapture a Windows Virtual Machine, see [How tooCapture a Windows Virtual Machine.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="5ce0f-206"><a name="What's Next"> </a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="5ce0f-206"><a name="What's Next"> </a>Next Steps</span></span>
<span data-ttu-id="5ce0f-207">서비스 관리 기본 사항 hello 배운, 했으므로 hello에 액세스할 수 있습니다 [hello Azure Python SDK에 대 한 전체 API 참조 설명서](http://azure-sdk-for-python.readthedocs.org/) 수행 하 고 복잡 한 작업을 쉽게 toomanage python 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-207">Now that you've learned hello basics of service management, you can access hello [Complete API reference documentation for hello Azure Python SDK](http://azure-sdk-for-python.readthedocs.org/) and perform complex tasks easily toomanage your python application.</span></span>

<span data-ttu-id="5ce0f-208">자세한 내용은 참조 hello [Python 개발자 센터](/develop/python/)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce0f-208">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

[What is Service Management]: #WhatIs
[Concepts]: #Concepts
[How to: Connect tooservice management]: #Connect
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
