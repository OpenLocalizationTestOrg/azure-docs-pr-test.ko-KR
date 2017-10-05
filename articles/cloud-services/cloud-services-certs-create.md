---
title: "클라우드 서비스 및 관리 인증서 | Microsoft Docs"
description: "Microsoft Azure에서 인증서를 만들고 사용하는 방법 알아보기"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: fc70d00d-899b-4771-855f-44574dc4bfc6
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: f760bfd93b19c43d12889b5dd38015c5eba0a8ac
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="certificates-overview-for-azure-cloud-services"></a><span data-ttu-id="dfcfc-103">Azure 클라우드 서비스 인증서 개요</span><span class="sxs-lookup"><span data-stu-id="dfcfc-103">Certificates overview for Azure Cloud Services</span></span>
<span data-ttu-id="dfcfc-104">Azure에서는 인증서가 Cloud Services([서비스 인증서](#what-are-service-certificates)) 및 관리 API를 사용한 인증(비 클래식 Azure Portal이 아닌 Azure 클래식 포털을 사용하는 경우 [관리 인증서](#what-are-management-certificates))에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-104">Certificates are used in Azure for cloud services ([service certificates](#what-are-service-certificates)) and for authenticating with the management API ([management certificates](#what-are-management-certificates) when using the Azure classic portal and not the non-classic Azure portal).</span></span> <span data-ttu-id="dfcfc-105">이 항목에서는 두 가지 인증서 형식에 대한 일반적인 개요와 인증서를 [만들고](#create) Azure에 [배포하는](#deploy) 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-105">This topic gives a general overview of both certificate types, how to [create](#create) and [deploy](#deploy) them to Azure.</span></span>

<span data-ttu-id="dfcfc-106">Azure에서 사용되는 인증서는 x.509 v3 인증서이며 다른 신뢰할 수 있는 인증서에 의해 서명되거나 자체 서명될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-106">Certificates used in Azure are x.509 v3 certificates and can be signed by another trusted certificate or they can be self-signed.</span></span> <span data-ttu-id="dfcfc-107">자체 서명된 인증서는 해당 작성자에 의해 서명되므로 기본적으로 신뢰할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-107">A self-signed certificate is signed by its own creator, therefore it is not trusted by default.</span></span> <span data-ttu-id="dfcfc-108">대부분의 브라우저는 이러한 문제를 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-108">Most browsers can ignore this problem.</span></span> <span data-ttu-id="dfcfc-109">Cloud Services를 개발하고 테스트하는 경우에만 자체 서명된 인증서를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-109">You should only use self-signed certificates when developing and testing your cloud services.</span></span> 

<span data-ttu-id="dfcfc-110">Azure에서 사용하는 인증서에는 개인 또는 공개 키가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-110">Certificates used by Azure can contain a private or a public key.</span></span> <span data-ttu-id="dfcfc-111">인증서에는 지문이 포함되어 있어 모호하지 않은 방식의 식별 수단을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-111">Certificates have a thumbprint that provides a means to identify them in an unambiguous way.</span></span> <span data-ttu-id="dfcfc-112">이 지문은 Azure [구성 파일](cloud-services-configure-ssl-certificate.md) 에서 클라우드 서비스가 사용할 인증서를 식별하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-112">This thumbprint is used in the Azure [configuration file](cloud-services-configure-ssl-certificate.md) to identify which certificate a cloud service should use.</span></span> 

## <a name="what-are-service-certificates"></a><span data-ttu-id="dfcfc-113">서비스 인증서란 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="dfcfc-113">What are service certificates?</span></span>
<span data-ttu-id="dfcfc-114">서비스 인증서는 클라우드 서비스에 첨부되며 서비스와 보안 통신을 사용할 수 있도록 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-114">Service certificates are attached to cloud services and enable secure communication to and from the service.</span></span> <span data-ttu-id="dfcfc-115">예를 들어 웹 역할을 배포한 경우 노출된 HTTPS 끝점을 인증할 수 있는 인증서를 제공하려고 할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-115">For example, if you deployed a web role, you would want to supply a certificate that can authenticate an exposed HTTPS endpoint.</span></span> <span data-ttu-id="dfcfc-116">서비스 정의에 있는 서비스 인증서는 자동으로 해당 역할 인스턴스를 실행하는 가상 컴퓨터에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-116">Service certificates, defined in your service definition, are automatically deployed to the virtual machine that is running an instance of your role.</span></span> 

<span data-ttu-id="dfcfc-117">Azure 클래식 포털을 사용하거나 클래식 배포 모델을 사용하여 서비스 인증서를 Azure 클래식 포털에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-117">You can upload service certificates to Azure classic portal either using the Azure classic portal or by using the classic deployment model.</span></span> <span data-ttu-id="dfcfc-118">서비스 인증서는 특정 클라우드 서비스와 연관됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-118">Service certificates are associated with a specific cloud service.</span></span> <span data-ttu-id="dfcfc-119">서비스 정의 파일에서 배포에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-119">They are assigned to a deployment in the service definition file.</span></span>

<span data-ttu-id="dfcfc-120">서비스 인증서는 서비스와 별도로 관리할 수 있으며 다른 개인이 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-120">Service certificates can be managed separately from your services, and may be managed by different individuals.</span></span> <span data-ttu-id="dfcfc-121">예를 들어 개발자는 IT 관리자가 이전에 Azure로 업로드한 인증서를 참조하는 서비스 패키지를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-121">For example, a developer may upload a service package that refers to a certificate that an IT manager has previously uploaded to Azure.</span></span> <span data-ttu-id="dfcfc-122">IT 관리자는 새 서비스 패키지를 업로드할 필요 없이 서비스 구성을 변경하는 해당 인증서를 관리하고 갱신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-122">An IT manager can manage and renew that certificate (changing the configuration of the service) without needing to upload a new service package.</span></span> <span data-ttu-id="dfcfc-123">새 서비스 패키지 없이 업데이트가 가능한 이유는 인증서의 논리적 이름과 저장소 이름 및 위치는 서비스 정의 파일에 있고 인증서 지문은 서비스 구성 파일에 지정되어 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-123">Updating without a new service package is possible because the logical name, store name, and location of the certificate is in the service definition file and while the certificate thumbprint is specified in the service configuration file.</span></span> <span data-ttu-id="dfcfc-124">인증서를 업데이트하려면 새 인증서를 업로드하고 서비스 구성 파일의 지문 값을 변경하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-124">To update the certificate, it's only necessary to upload a new certificate and change the thumbprint value in the service configuration file.</span></span>

>[!Note]
><span data-ttu-id="dfcfc-125">[Cloud Services FAQ](cloud-services-faq.md) 문서에는 인증서에 대한 몇 가지 유용한 정보가 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-125">The [Cloud Services FAQ](cloud-services-faq.md) article has some helpful information about certificates.</span></span>

## <a name="what-are-management-certificates"></a><span data-ttu-id="dfcfc-126">관리 인증서란 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="dfcfc-126">What are management certificates?</span></span>
<span data-ttu-id="dfcfc-127">관리 인증서를 사용하면 클래식 배포 모델로 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-127">Management certificates allow you to authenticate with the classic deployment model.</span></span> <span data-ttu-id="dfcfc-128">Visual Studio 또는 Azure SDK와 같은 많은 프로그램 및 도구에서 이러한 인증서를 사용하여 다양한 Azure 서비스의 구성 및 배포를 자동화합니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-128">Many programs and tools (such as Visual Studio or the Azure SDK) use these certificates to automate configuration and deployment of various Azure services.</span></span> <span data-ttu-id="dfcfc-129">클라우드 서비스와는 실제로 관련이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-129">These are not really related to cloud services.</span></span> 

> [!WARNING]
> <span data-ttu-id="dfcfc-130">주의가 필요합니다!</span><span class="sxs-lookup"><span data-stu-id="dfcfc-130">Be careful!</span></span> <span data-ttu-id="dfcfc-131">이러한 형식의 인증서를 사용하면 해당 인증서로 인증된 사람은 누구나 연결된 구독을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-131">These types of certificates allow anyone who authenticates with them to manage the subscription they are associated with.</span></span> 
> 
> 

### <a name="limitations"></a><span data-ttu-id="dfcfc-132">제한 사항</span><span class="sxs-lookup"><span data-stu-id="dfcfc-132">Limitations</span></span>
<span data-ttu-id="dfcfc-133">관리 인증서는 구독당 100개로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-133">There is a limit of 100 management certificates per subscription.</span></span> <span data-ttu-id="dfcfc-134">특정 서비스 관리자의 사용자 ID에서 모든 구독에 대한 관리 인증서가 100개로 제한되기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-134">There is also a limit of 100 management certificates for all subscriptions under a specific service administrator’s user ID.</span></span> <span data-ttu-id="dfcfc-135">계정 관리자의 사용자 ID가 이미 관리 인증서 100개를 추가하는 데 사용되었으나 인증서가 더 필요한 경우 공동 관리자를 추가하여 인증서를 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-135">If the user ID for the account administrator has already been used to add 100 management certificates and there is a need for more certificates, you can add a co-administrator to add the additional certificates.</span></span> 

<span data-ttu-id="dfcfc-136">100개가 넘는 인증서를 추가하기 전에 기존 인증서를 다시 사용할 수 있는지 확인해보세요.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-136">Before adding more than 100 certificates, see if you can reuse an existing certificate.</span></span> <span data-ttu-id="dfcfc-137">공동 관리자를 사용하면 인증서 관리 프로세스에 불필요한 복잡성이 가중될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-137">Using co-administrators adds potentially unneeded complexity to your certificate management process.</span></span>

<a name="create"></a>
## <a name="create-a-new-self-signed-certificate"></a><span data-ttu-id="dfcfc-138">자체 서명된 새로운 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="dfcfc-138">Create a new self-signed certificate</span></span>
<span data-ttu-id="dfcfc-139">어떠한 도구든 다음 설정을 준수하는 경우 자체 서명된 인증서를 만드는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-139">You can use any tool available to create a self-signed certificate as long as they adhere to these settings:</span></span>

* <span data-ttu-id="dfcfc-140">X.509 인증서여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-140">An X.509 certificate.</span></span>
* <span data-ttu-id="dfcfc-141">개인 키가 포함되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-141">Contains a private key.</span></span>
* <span data-ttu-id="dfcfc-142">키 교환용으로 만들어졌어야 합니다(.pfx 파일).</span><span class="sxs-lookup"><span data-stu-id="dfcfc-142">Created for key exchange (.pfx file).</span></span>
* <span data-ttu-id="dfcfc-143">주체 이름은 클라우드 서비스 액세스에 사용되는 도메인과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-143">Subject name must match the domain used to access the cloud service.</span></span>

    > <span data-ttu-id="dfcfc-144">cloudapp.net(또는 Azure 관련) 도메인용 SSL 인증서를 얻을 수 없으므로, 인증서의 주체 이름은 사용 중인 응용 프로그램 액세스에 사용되는 사용자 지정 도메인 이름과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-144">You cannot acquire an SSL certificate for the cloudapp.net (or for any Azure-related) domain; the certificate's subject name must match the custom domain name used to access your application.</span></span> <span data-ttu-id="dfcfc-145">예를 들어, **contoso.cloudapp.net**이 아니라**contoso.net**입니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-145">For example, **contoso.net**, not **contoso.cloudapp.net**.</span></span>

* <span data-ttu-id="dfcfc-146">최소한 2048비트 암호화를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-146">Minimum of 2048-bit encryption.</span></span>
* <span data-ttu-id="dfcfc-147">**서비스 인증서에만 해당**: 클라이언트 쪽 인증서는 *개인* 인증서 저장소에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-147">**Service Certificate Only**: Client-side certificate must reside in the *Personal* certificate store.</span></span>

<span data-ttu-id="dfcfc-148">Windows에서는 두 가지 방법, `makecert.exe` 유틸리티 또는 IIS를 사용하여 쉽게 인증서를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-148">There are two easy ways to create a certificate on Windows, with the `makecert.exe` utility, or IIS.</span></span>

### <a name="makecertexe"></a><span data-ttu-id="dfcfc-149">Makecert.exe</span><span class="sxs-lookup"><span data-stu-id="dfcfc-149">Makecert.exe</span></span>
<span data-ttu-id="dfcfc-150">이 유틸리티는 사용되지 않으므로 여기에 더 이상 설명되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-150">This utility has been deprecated and is no longer documented here.</span></span> <span data-ttu-id="dfcfc-151">자세한 내용은 [이 MSDN 문서](https://msdn.microsoft.com/library/windows/desktop/aa386968)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-151">For more information, see [this MSDN article](https://msdn.microsoft.com/library/windows/desktop/aa386968).</span></span>

### <a name="powershell"></a><span data-ttu-id="dfcfc-152">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dfcfc-152">PowerShell</span></span>
```powershell
$cert = New-SelfSignedCertificate -DnsName yourdomain.cloudapp.net -CertStoreLocation "cert:\LocalMachine\My"
$password = ConvertTo-SecureString -String "your-password" -Force -AsPlainText
Export-PfxCertificate -Cert $cert -FilePath ".\my-cert-file.pfx" -Password $password
```

> [!NOTE]
> <span data-ttu-id="dfcfc-153">도메인 대신에 IP 주소가 들어 있는 인증서를 사용하려는 경우 -DnsName 매개 변수에서 IP 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-153">If you want to use the certificate with an IP address instead of a domain, use the IP address in the -DnsName parameter.</span></span>


<span data-ttu-id="dfcfc-154">[관리 포털에서 인증서](../azure-api-management-certs.md)를 사용하려는 경우 **.cer** 파일로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-154">If you want to use this [certificate with the management portal](../azure-api-management-certs.md), export it to a **.cer** file:</span></span>

```powershell
Export-Certificate -Type CERT -Cert $cert -FilePath .\my-cert-file.cer
```

### <a name="internet-information-services-iis"></a><span data-ttu-id="dfcfc-155">IIS(인터넷 정보 서비스)</span><span class="sxs-lookup"><span data-stu-id="dfcfc-155">Internet Information Services (IIS)</span></span>
<span data-ttu-id="dfcfc-156">인터넷에는 IIS를 사용하여 이 작업을 수행하는 방법을 다룬 내용이 많이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-156">There are many pages on the internet that cover how to do this with IIS.</span></span> <span data-ttu-id="dfcfc-157">[여기](https://www.sslshopper.com/article-how-to-create-a-self-signed-certificate-in-iis-7.html) 에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-157">[Here](https://www.sslshopper.com/article-how-to-create-a-self-signed-certificate-in-iis-7.html) is a great one I found that I think explains it well.</span></span> 

### <a name="java"></a><span data-ttu-id="dfcfc-158">Java</span><span class="sxs-lookup"><span data-stu-id="dfcfc-158">Java</span></span>
<span data-ttu-id="dfcfc-159">Java를 사용하여 [인증서를 만들](../app-service-web/java-create-azure-website-using-java-sdk.md#create-a-certificate)수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-159">You can use Java to [create a certificate](../app-service-web/java-create-azure-website-using-java-sdk.md#create-a-certificate).</span></span>

### <a name="linux"></a><span data-ttu-id="dfcfc-160">Linux</span><span class="sxs-lookup"><span data-stu-id="dfcfc-160">Linux</span></span>
<span data-ttu-id="dfcfc-161">[이](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 문서에서는 SSH로 인증서를 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-161">[This](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) article describes how to create certificates with SSH.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dfcfc-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dfcfc-162">Next steps</span></span>
<span data-ttu-id="dfcfc-163">[서비스 인증서를 Azure 클래식 포털](cloud-services-configure-ssl-certificate.md)(또는 [Azure Portal](cloud-services-configure-ssl-certificate-portal.md))에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-163">[Upload your service certificate to the Azure classic portal](cloud-services-configure-ssl-certificate.md) (or the [Azure portal](cloud-services-configure-ssl-certificate-portal.md)).</span></span>

<span data-ttu-id="dfcfc-164">[관리 API 인증서](../azure-api-management-certs.md) 를 Azure 클래식 포털에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-164">Upload a [management API certificate](../azure-api-management-certs.md) to the Azure classic portal.</span></span> <span data-ttu-id="dfcfc-165">Azure Portal에서는 인증을 위해 관리 인증서를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dfcfc-165">The Azure portal does not use management certificates for authentication.</span></span>

