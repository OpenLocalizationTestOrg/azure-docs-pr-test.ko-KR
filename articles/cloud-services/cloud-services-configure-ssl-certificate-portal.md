---
title: "클라우드 서비스에 대해 SSL 구성 | Microsoft Docs"
description: "웹 역할에 대해 HTTPS 끝점을 지정하는 방법 및 응용 프로그램 보안을 위해 SSL 인증서를 업로드하는 방법에 대해 알아봅니다. 이 예제는 Azure 포털을 사용합니다."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 371ba204-48b6-41af-ab9f-ed1d64efe704
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: e5c8c3b098772c0586712305a577b24a6f0d924c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="89d8e-104">Azure에서 응용 프로그램에 대한 SSL 구성</span><span class="sxs-lookup"><span data-stu-id="89d8e-104">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="89d8e-105">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="89d8e-105">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="89d8e-106">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="89d8e-106">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
>

<span data-ttu-id="89d8e-107">SSL(Secure Socket Layer) 암호화는 인터넷을 통해 전송되는 데이터 보호에 가장 일반적으로 사용되는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-107">Secure Socket Layer (SSL) encryption is the most commonly used method of securing data sent across the internet.</span></span> <span data-ttu-id="89d8e-108">이 일반 작업에서는 웹 역할에 대해 HTTPS 끝점을 지정하는 방법 및 응용 프로그램 보안을 위해 SSL 인증서를 업로드하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-108">This common task discusses how to specify an HTTPS endpoint for a web role and how to upload an SSL certificate to secure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="89d8e-109">이 작업의 절차는 Azure 클라우드 서비스에 적용됩니다. 앱 서비스에 대해서는 [이 항목](../app-service-web/web-sites-configure-ssl-certificate.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89d8e-109">The procedures in this task apply to Azure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md).</span></span>
>

<span data-ttu-id="89d8e-110">이 작업에서는 프로덕션 배포를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-110">This task uses a production deployment.</span></span> <span data-ttu-id="89d8e-111">스테이징 배포에 대한 정보는 이 항목의 끝에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-111">Information on using a staging deployment is provided at the end of this topic.</span></span>

<span data-ttu-id="89d8e-112">클라우드 서비스를 아직 만들지 않은 경우 먼저 [이 문서를](cloud-services-how-to-create-deploy-portal.md) 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="89d8e-112">Read [this](cloud-services-how-to-create-deploy-portal.md) first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="89d8e-113">1단계: SSL 인증서 다운로드</span><span class="sxs-lookup"><span data-stu-id="89d8e-113">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="89d8e-114">응용 프로그램에 대해 SSL을 구성하려면 먼저 이 목적으로 인증서를 발급하는 신뢰할 수 있는 타사 CA(인증 기관)에서 서명한 SSL 인증서를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-114">To configure SSL for an application, you first need to get an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="89d8e-115">아직 없는 경우 SSL 인증서를 판매하는 회사에서 구입해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-115">If you do not already have one, you need to obtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="89d8e-116">인증서는 Azure의 SSL 인증서에 대한 다음 요구 사항을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-116">The certificate must meet the following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="89d8e-117">인증서에 개인 키가 포함되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-117">The certificate must contain a private key.</span></span>
* <span data-ttu-id="89d8e-118">개인 정보 교환(.pfx) 파일로 내보낼 수 있는 키 교환용 인증서를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-118">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="89d8e-119">인증서의 주체 이름은 클라우드 서비스 액세스에 사용되는 도메인과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-119">The certificate's subject name must match the domain used to access the cloud service.</span></span> <span data-ttu-id="89d8e-120">cloudapp.net 도메인에 사용되는 SSL 인증서는 CA(인증 기관)에서 얻을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-120">You cannot obtain an SSL certificate from a certificate authority (CA) for the cloudapp.net domain.</span></span> <span data-ttu-id="89d8e-121">서비스에 액세스할 때 사용할 사용자 지정 도메인 이름을 획득해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-121">You must acquire a custom domain name to use when access your service.</span></span> <span data-ttu-id="89d8e-122">CA에서 인증서를 요청하는 경우 인증서의 주체 이름이 응용 프로그램 액세스에 사용되는 사용자 지정 도메인 이름과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-122">When you request a certificate from a CA, the certificate's subject name must match the custom domain name used to access your application.</span></span> <span data-ttu-id="89d8e-123">예를 들어 사용자 지정 도메인 이름이 **contoso.com**인 경우 CA에서 ***.contoso.com** 또는 **www.contoso.com**에 대한 인증서를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-123">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="89d8e-124">인증서는 최소한 2048비트 암호화를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-124">The certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="89d8e-125">테스트용으로 자체 서명된 인증서를 [만들어](cloud-services-certs-create.md) 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-125">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="89d8e-126">자체 서명된 인증서는 CA를 통해 인증되지 않으며 cloudapp.net 도메인을 웹 사이트 URL로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-126">A self-signed certificate is not authenticated through a CA and can use the cloudapp.net domain as the website URL.</span></span> <span data-ttu-id="89d8e-127">예를 들어 다음 작업에서는 인증서에서 사용되는 CN(일반 이름)이 **sslexample.cloudapp.net**인 자체 서명된 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-127">For example, the following task uses a self-signed certificate in which the common name (CN) used in the certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="89d8e-128">다음으로 인증서에 대한 정보를 서비스 정의 및 서비스 구성 파일에 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-128">Next, you must include information about the certificate in your service definition and service configuration files.</span></span>

<span data-ttu-id="89d8e-129"><a name="modify"> </a></span><span class="sxs-lookup"><span data-stu-id="89d8e-129"><a name="modify"> </a></span></span>

## <a name="step-2-modify-the-service-definition-and-configuration-files"></a><span data-ttu-id="89d8e-130">2단계: 서비스 정의 및 구성 파일 수정</span><span class="sxs-lookup"><span data-stu-id="89d8e-130">Step 2: Modify the service definition and configuration files</span></span>
<span data-ttu-id="89d8e-131">인증서를 사용하도록 응용 프로그램을 구성하고 HTTPS 끝점을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-131">Your application must be configured to use the certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="89d8e-132">따라서 서비스 정의 및 서비스 구성 파일을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-132">As a result, the service definition and service configuration files need to be updated.</span></span>

1. <span data-ttu-id="89d8e-133">개발 환경에서 서비스 정의 파일(CSDEF)을 열고 **WebRole** 섹션 내에 **Certificates** 섹션을 추가한 후 인증서(및 중간 인증서)에 대한 다음 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-133">In your development environment, open the service definition file (CSDEF), add a **Certificates** section within the **WebRole** section, and include the following information about the certificate (and intermediate certificates):</span></span>

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Certificates>
            <Certificate name="SampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="My"
                        permissionLevel="limitedOrElevated" />
            <!-- IMPORTANT! Unless your certificate is either
            self-signed or signed directly by the CA root, you
            must include all the intermediate certificates
            here. You must list them here, even if they are
            not bound to any endpoints. Failing to list any of
            the intermediate certificates may cause hard-to-reproduce
            interoperability problems on some clients.-->
            <Certificate name="CAForSampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="CA"
                        permissionLevel="limitedOrElevated" />
        </Certificates>
    ...
    </WebRole>
    ```

   <span data-ttu-id="89d8e-134">**Certificates** 섹션에서는 인증서의 이름, 위치 및 인증서가 위치한 저장소의 이름을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-134">The **Certificates** section defines the name of our certificate, its location, and the name of the store where it is located.</span></span>

   <span data-ttu-id="89d8e-135">권한(`permisionLevel` 특성)은 다음 값 중 하나로 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-135">Permissions (`permisionLevel` attribute) can be set to one of the following values:</span></span>

   | <span data-ttu-id="89d8e-136">권한 값</span><span class="sxs-lookup"><span data-stu-id="89d8e-136">Permission Value</span></span> | <span data-ttu-id="89d8e-137">설명</span><span class="sxs-lookup"><span data-stu-id="89d8e-137">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="89d8e-138">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="89d8e-138">limitedOrElevated</span></span> |<span data-ttu-id="89d8e-139">**(기본값)** 모든 역할 프로세스는 개인 키에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-139">**(Default)** All role processes can access the private key.</span></span> |
   | <span data-ttu-id="89d8e-140">elevated</span><span class="sxs-lookup"><span data-stu-id="89d8e-140">elevated</span></span> |<span data-ttu-id="89d8e-141">승격된 프로세스만 개인 키에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-141">Only elevated processes can access the private key.</span></span> |

2. <span data-ttu-id="89d8e-142">서비스 정의 파일에서 **끝점** 섹션 내에 **InputEndpoint** 요소를 추가하여 HTTPS를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-142">In your service definition file, add an **InputEndpoint** element within the **Endpoints** section to enable HTTPS:</span></span>

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Endpoints>
            <InputEndpoint name="HttpsIn" protocol="https" port="443"
                certificate="SampleCertificate" />
        </Endpoints>
    ...
    </WebRole>
    ```

3. <span data-ttu-id="89d8e-143">서비스 정의 파일에서 **Sites** 섹션 내에 **Binding** 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-143">In your service definition file, add a **Binding** element within the **Sites** section.</span></span> <span data-ttu-id="89d8e-144">이 요소는 HTTPS 바인딩을 추가하여 끝점을 사이트에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-144">This element adds an HTTPS binding to map the endpoint to your site:</span></span>

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="HttpsIn" endpointName="HttpsIn" />
                </Bindings>
            </Site>
        </Sites>
    ...
    </WebRole>
    ```

   <span data-ttu-id="89d8e-145">서비스 정의 파일에서 필요한 사항은 모두 변경했지만 인증서 정보를 서비스 구성 파일에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-145">All the required changes to the service definition file have been completed; but, you still need to add the certificate information to the service configuration file.</span></span>
4. <span data-ttu-id="89d8e-146">서비스 구성 파일(CSCFG), ServiceConfiguration.Cloud.cscfg에서 사용 중인 인증서 값에 해당하는 **Certificates** 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-146">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** value with that of your certificate.</span></span> <span data-ttu-id="89d8e-147">다음 코드 예제에서는 지문 값을 제외한 **Certificates** 섹션의 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-147">The following code sample provides details of the **Certificates** section, except for the thumbprint value.</span></span>

   ```xml
    <Role name="Deployment">
    ...
        <Certificates>
            <Certificate name="SampleCertificate"
                thumbprint="9427befa18ec6865a9ebdc79d4c38de50e6316ff"
                thumbprintAlgorithm="sha1" />
            <Certificate name="CAForSampleCertificate"
                thumbprint="79d4c38de50e6316ff9427befa18ec6865a9ebdc"
                thumbprintAlgorithm="sha1" />
        </Certificates>
    ...
    </Role>
    ```

<span data-ttu-id="89d8e-148">이 예제에서는 지문 알고리즘에 **sha1**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-148">(This example uses **sha1** for the thumbprint algorithm.</span></span> <span data-ttu-id="89d8e-149">인증서의 지문 알고리즘에 적합한 값을 지정하세요.</span><span class="sxs-lookup"><span data-stu-id="89d8e-149">Specify the appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="89d8e-150">서비스 정의 및 서비스 구성 파일이 업데이트되었으므로 Azure에 업로드할 배포를 패키지합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-150">Now that the service definition and service configuration files have been updated, package your deployment for uploading to Azure.</span></span> <span data-ttu-id="89d8e-151">**cspack**를 사용하는 경우 **/generateConfigurationFile** 플래그를 사용하지 않도록 하세요. 이 플래그는 방금 삽입한 인증서 정보를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-151">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that will overwrite the certificate information you just inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="89d8e-152">3단계: 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="89d8e-152">Step 3: Upload a certificate</span></span>
<span data-ttu-id="89d8e-153">Azure Portal에 연결하고 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-153">Connect to the Azure portal and...</span></span>

1. <span data-ttu-id="89d8e-154">포털의 **모든 리소스** 섹션에서 클라우드 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-154">In the **All resources** section of the Portal, select your cloud service.</span></span>

    ![클라우드 서비스 게시](media/cloud-services-configure-ssl-certificate-portal/browse.png)

2. <span data-ttu-id="89d8e-156">**인증서**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-156">Click **Certificates**.</span></span>

    ![인증서 아이콘 클릭](media/cloud-services-configure-ssl-certificate-portal/certificate-item.png)

3. <span data-ttu-id="89d8e-158">인증서 영역 위쪽에서 **업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-158">Click **Upload** at the top of the certificates area.</span></span>

    ![업로드 메뉴 항목 클릭](media/cloud-services-configure-ssl-certificate-portal/Upload_menu.png)

4. <span data-ttu-id="89d8e-160">**파일**, **암호**를 입력하고 데이터 입력 영역 아래쪽의 **업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-160">Provide the **File**, **Password**, then click **Upload** at the bottom of the data entry area.</span></span>

## <a name="step-4-connect-to-the-role-instance-by-using-https"></a><span data-ttu-id="89d8e-161">4단계: HTTPS를 사용하여 역할 인스턴스에 연결</span><span class="sxs-lookup"><span data-stu-id="89d8e-161">Step 4: Connect to the role instance by using HTTPS</span></span>
<span data-ttu-id="89d8e-162">이제 Azure에서 배포가 실행되고 있으므로 HTTPS를 사용하여 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-162">Now that your deployment is up and running in Azure, you can connect to it using HTTPS.</span></span>

1. <span data-ttu-id="89d8e-163">**사이트 URL**을 클릭하여 웹 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-163">Click the **Site URL** to open up the web browser.</span></span>

   ![사이트 URL 클릭](media/cloud-services-configure-ssl-certificate-portal/navigate.png)

2. <span data-ttu-id="89d8e-165">웹 브라우저에서 **http** 대신 **https**를 사용하도록 링크를 수정한 다음 페이지를 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-165">In your web browser, modify the link to use **https** instead of **http**, and then visit the page.</span></span>

   > [!NOTE]
   > <span data-ttu-id="89d8e-166">자체 서명된 인증서를 사용하는 경우 자체 서명된 인증서와 연결된 HTTPS 끝점으로 이동하면 브라우저에 인증서오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-166">If you are using a self-signed certificate, when you browse to an HTTPS endpoint that's associated with the self-signed certificate you may see a certificate error in the browser.</span></span> <span data-ttu-id="89d8e-167">신뢰할 수 있는 인증 기관에서 서명한 인증서를 사용하면 이 문제가 해결되지만 이 오류는 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-167">Using a certificate signed by a trusted certification authority eliminates this problem; in the meantime, you can ignore the error.</span></span> <span data-ttu-id="89d8e-168">또 다른 옵션으로 사용자의 신뢰할 수 있는 인증 기관 인증서 저장소에 자체 서명된 인증서를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-168">(Another option is to add the self-signed certificate to the user's trusted certificate authority certificate store.)</span></span>
   >
   >

   ![사이트 미리 보기](media/cloud-services-configure-ssl-certificate-portal/show-site.png)

   > [!TIP]
   > <span data-ttu-id="89d8e-170">프로덕션 배포가 아닌 스테이징 배포에 SSL을 사용하려면 먼저 스테이징 배포에 사용된 URL을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-170">If you want to use SSL for a staging deployment instead of a production deployment, you'll first need to determine the URL used for the staging deployment.</span></span> <span data-ttu-id="89d8e-171">클라우드 서비스가 배포되면 `https://deployment-id.cloudapp.net/` 형식의 **배포 ID** GUID에 따라 스테이징 환경에 대한 URL이 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-171">Once your cloud service has been deployed, the URL to the staging environment is determined by the **Deployment ID** GUID in this format: `https://deployment-id.cloudapp.net/`</span></span>  
   >
   > <span data-ttu-id="89d8e-172">GUID 기반 URL과 같은 CN(일반 이름)으로 인증서를 만듭니다(예: **328187776e774ceda8fc57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="89d8e-172">Create a certificate with the common name (CN) equal to the GUID-based URL (for example, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="89d8e-173">스테이징된 클라우드 서비스에 인증서를 추가하려면 포털을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-173">Use the portal to add the certificate to your staged cloud service.</span></span> <span data-ttu-id="89d8e-174">그런 다음 인증서 정보를 CSDEF 및 CSCFG 파일에 추가하고 응용 프로그램을 다시 패키지하고 스테이징된 배포를 업데이트하여 새 패키지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-174">Then, add the certificate information to your CSDEF and CSCFG files, repackage your application, and update your staged deployment to use the new package.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="89d8e-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="89d8e-175">Next steps</span></span>
* <span data-ttu-id="89d8e-176">[클라우드 서비스의 일반 구성](cloud-services-how-to-configure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="89d8e-176">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="89d8e-177">[클라우드 서비스를 배포](cloud-services-how-to-create-deploy-portal.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-177">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="89d8e-178">[사용자 지정 도메인 이름](cloud-services-custom-domain-name-portal.md)을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="89d8e-178">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="89d8e-179">[클라우드 서비스를 관리합니다](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="89d8e-179">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
