---
title: "클라우드 서비스(클래식)에 대해 SSL 구성 | Microsoft Docs"
description: "웹 역할에 대해 HTTPS 끝점을 지정하는 방법 및 응용 프로그램 보안을 위해 SSL 인증서를 업로드하는 방법에 대해 알아봅니다."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 4cbb7f38-7994-454d-b4f0-7259b558c766
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/14/2016
ms.author: adegeo
ms.openlocfilehash: edb9aaf6dae11c9b8a171b22bc8a17003f80d86b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="4aeec-103">Azure에서 응용 프로그램에 대한 SSL 구성</span><span class="sxs-lookup"><span data-stu-id="4aeec-103">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4aeec-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="4aeec-104">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="4aeec-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="4aeec-105">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
> 
> 

<span data-ttu-id="4aeec-106">SSL(Secure Socket Layer) 암호화는 인터넷을 통해 전송되는 데이터 보호에 가장 일반적으로 사용되는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-106">Secure Socket Layer (SSL) encryption is the most commonly used method of securing data sent across the internet.</span></span> <span data-ttu-id="4aeec-107">이 일반 작업에서는 웹 역할에 대해 HTTPS 끝점을 지정하는 방법 및 응용 프로그램 보안을 위해 SSL 인증서를 업로드하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-107">This common task discusses how to specify an HTTPS endpoint for a web role and how to upload an SSL certificate to secure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="4aeec-108">이 작업의 절차는 Azure 클라우드 서비스에 적용됩니다. 앱 서비스에 대해서는 [이](../app-service-web/web-sites-configure-ssl-certificate.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4aeec-108">The procedures in this task apply to Azure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md) article.</span></span>
> 
> 

<span data-ttu-id="4aeec-109">이 작업에서는 프로덕션 배포를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-109">This task uses a production deployment.</span></span> <span data-ttu-id="4aeec-110">스테이징 배포에 대한 정보는 이 항목의 끝에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-110">Information on using a staging deployment is provided at the end of this topic.</span></span>

<span data-ttu-id="4aeec-111">클라우드 서비스를 아직 만들지 않은 경우 먼저 [이](cloud-services-how-to-create-deploy.md) 문서를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="4aeec-111">Read [this](cloud-services-how-to-create-deploy.md) article first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="4aeec-112">1단계: SSL 인증서 다운로드</span><span class="sxs-lookup"><span data-stu-id="4aeec-112">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="4aeec-113">응용 프로그램에 대해 SSL을 구성하려면 먼저 이 목적으로 인증서를 발급하는 신뢰할 수 있는 타사 CA(인증 기관)에서 서명한 SSL 인증서를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-113">To configure SSL for an application, you first need to get an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="4aeec-114">아직 없는 경우 SSL 인증서를 판매하는 회사에서 구입해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-114">If you do not already have one, you need to obtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="4aeec-115">인증서는 Azure의 SSL 인증서에 대한 다음 요구 사항을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-115">The certificate must meet the following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="4aeec-116">인증서에 개인 키가 포함되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-116">The certificate must contain a private key.</span></span>
* <span data-ttu-id="4aeec-117">개인 정보 교환(.pfx) 파일로 내보낼 수 있는 키 교환용 인증서를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-117">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="4aeec-118">인증서의 주체 이름은 클라우드 서비스 액세스에 사용되는 도메인과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-118">The certificate's subject name must match the domain used to access the cloud service.</span></span> <span data-ttu-id="4aeec-119">cloudapp.net 도메인에 사용되는 SSL 인증서는 CA(인증 기관)에서 얻을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-119">You cannot obtain an SSL certificate from a certificate authority (CA) for the cloudapp.net domain.</span></span> <span data-ttu-id="4aeec-120">서비스에 액세스할 때 사용할 사용자 지정 도메인 이름을 획득해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-120">You must acquire a custom domain name to use when access your service.</span></span> <span data-ttu-id="4aeec-121">CA에서 인증서를 요청하는 경우 인증서의 주체 이름이 응용 프로그램 액세스에 사용되는 사용자 지정 도메인 이름과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-121">When you request a certificate from a CA, the certificate's subject name must match the custom domain name used to access your application.</span></span> <span data-ttu-id="4aeec-122">예를 들어 사용자 지정 도메인 이름이 **contoso.com**인 경우 CA에서 ***.contoso.com** 또는 **www.contoso.com**에 대한 인증서를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-122">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="4aeec-123">인증서는 최소한 2048비트 암호화를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-123">The certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="4aeec-124">테스트용으로 자체 서명된 인증서를 [만들어](cloud-services-certs-create.md) 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-124">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="4aeec-125">자체 서명된 인증서는 CA를 통해 인증되지 않으며 cloudapp.net 도메인을 웹 사이트 URL로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-125">A self-signed certificate is not authenticated through a CA and can use the cloudapp.net domain as the website URL.</span></span> <span data-ttu-id="4aeec-126">예를 들어 다음 작업에서는 인증서에서 사용되는 CN(일반 이름)이 **sslexample.cloudapp.net**인 자체 서명된 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-126">For example, the following task uses a self-signed certificate in which the common name (CN) used in the certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="4aeec-127">다음으로 인증서에 대한 정보를 서비스 정의 및 서비스 구성 파일에 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-127">Next, you must include information about the certificate in your service definition and service configuration files.</span></span>

## <a name="step-2-modify-the-service-definition-and-configuration-files"></a><span data-ttu-id="4aeec-128">2단계: 서비스 정의 및 구성 파일 수정</span><span class="sxs-lookup"><span data-stu-id="4aeec-128">Step 2: Modify the service definition and configuration files</span></span>
<span data-ttu-id="4aeec-129">인증서를 사용하도록 응용 프로그램을 구성하고 HTTPS 끝점을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-129">Your application must be configured to use the certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="4aeec-130">따라서 서비스 정의 및 서비스 구성 파일을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-130">As a result, the service definition and service configuration files need to be updated.</span></span>

1. <span data-ttu-id="4aeec-131">개발 환경에서 서비스 정의 파일(CSDEF)을 열고 **WebRole** 섹션 내에 **Certificates** 섹션을 추가한 후 인증서(및 중간 인증서)에 대한 다음 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-131">In your development environment, open the service definition file (CSDEF), add a **Certificates** section within the **WebRole** section, and include the following information about the certificate (and intermediate certificates):</span></span>
   
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
   
   <span data-ttu-id="4aeec-132">**Certificates** 섹션에서는 인증서의 이름, 위치 및 인증서가 위치한 저장소의 이름을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-132">The **Certificates** section defines the name of our certificate, its location, and the name of the store where it is located.</span></span>
   
   <span data-ttu-id="4aeec-133">권한(`permisionLevel` 특성)은 다음 값 중 하나로 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-133">Permissions (`permisionLevel` attribute) can be set to one of the following values:</span></span>
   
   | <span data-ttu-id="4aeec-134">권한 값</span><span class="sxs-lookup"><span data-stu-id="4aeec-134">Permission Value</span></span> | <span data-ttu-id="4aeec-135">설명</span><span class="sxs-lookup"><span data-stu-id="4aeec-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="4aeec-136">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="4aeec-136">limitedOrElevated</span></span> |<span data-ttu-id="4aeec-137">**(기본값)** 모든 역할 프로세스는 개인 키에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-137">**(Default)** All role processes can access the private key.</span></span> |
   | <span data-ttu-id="4aeec-138">elevated</span><span class="sxs-lookup"><span data-stu-id="4aeec-138">elevated</span></span> |<span data-ttu-id="4aeec-139">승격된 프로세스만 개인 키에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-139">Only elevated processes can access the private key.</span></span> |
2. <span data-ttu-id="4aeec-140">서비스 정의 파일에서 **끝점** 섹션 내에 **InputEndpoint** 요소를 추가하여 HTTPS를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-140">In your service definition file, add an **InputEndpoint** element within the **Endpoints** section to enable HTTPS:</span></span>
   
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

3. <span data-ttu-id="4aeec-141">서비스 정의 파일에서 **Sites** 섹션 내에 **Binding** 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-141">In your service definition file, add a **Binding** element within the **Sites** section.</span></span> <span data-ttu-id="4aeec-142">이 섹션은 HTTPS 바인딩을 추가하여 끝점을 사이트에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-142">This section adds an HTTPS binding to map the endpoint to your site:</span></span>
   
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
   
   <span data-ttu-id="4aeec-143">서비스 정의 파일에서 필요한 사항은 모두 변경했지만 인증서 정보를 서비스 구성 파일에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-143">All the required changes to the service definition file have been completed, but you still need to add the certificate information to the service configuration file.</span></span>
4. <span data-ttu-id="4aeec-144">서비스 구성 파일(CSCFG), ServiceConfiguration.Cloud.cscfg에서 **Role** 섹션 내에 **Certificates** 섹션을 추가하여 아래에 표시된 샘플 지문 값을 인증서의 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-144">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** section within the **Role** section, replacing the sample thumbprint value shown below with that of your certificate:</span></span>
   
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

<span data-ttu-id="4aeec-145">이전 예제에서는 지문 알고리즘에 **sha1**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-145">(The preceding example uses **sha1** for the thumbprint algorithm.</span></span> <span data-ttu-id="4aeec-146">인증서의 지문 알고리즘에 적합한 값을 지정하세요.</span><span class="sxs-lookup"><span data-stu-id="4aeec-146">Specify the appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="4aeec-147">서비스 정의 및 서비스 구성 파일이 업데이트되었으므로 Azure에 업로드할 배포를 패키지합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-147">Now that the service definition and service configuration files have been updated, package your deployment for uploading to Azure.</span></span> <span data-ttu-id="4aeec-148">**cspack**를 사용하는 경우 **/generateConfigurationFile** 플래그를 사용하지 않도록 하세요. 이 플래그는 방금 삽입한 인증서 정보를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-148">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that overwrites the certificate information you inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="4aeec-149">3단계: 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="4aeec-149">Step 3: Upload a certificate</span></span>
<span data-ttu-id="4aeec-150">배포 패키지가 인증서를 사용하도록 업데이트되었으며 HTTPS 끝점이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-150">Your deployment package has been updated to use the certificate, and an HTTPS endpoint has been added.</span></span> <span data-ttu-id="4aeec-151">이제 Azure 클래식 포털을 사용하여 패키지 및 인증서를 Azure에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-151">Now you can upload the package and certificate to Azure with the Azure classic portal.</span></span>

1. <span data-ttu-id="4aeec-152">[Azure 클래식 포털][Azure classic portal]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-152">Log in to the [Azure classic portal][Azure classic portal].</span></span> 
2. <span data-ttu-id="4aeec-153">클릭할 왼쪽 탐색 모음 창의 **클라우드 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-153">Click **Cloud Services** on the left-side navigation pane.</span></span>
3. <span data-ttu-id="4aeec-154">원하는 클라우드 서비스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-154">Click the desired cloud service.</span></span>
4. <span data-ttu-id="4aeec-155">**인증서** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-155">Click the **Certificates** tab.</span></span>
   
    ![인증서 탭을 클릭합니다.](./media/cloud-services-configure-ssl-certificate/click-cert.png)

5. <span data-ttu-id="4aeec-157">**업로드** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-157">Click the **Upload** button.</span></span>
   
    ![업로드](./media/cloud-services-configure-ssl-certificate/upload-button.png)
    
6. <span data-ttu-id="4aeec-159">**파일**, **암호**를 제공한 후 **완료**를 클릭합니다(확인 표시).</span><span class="sxs-lookup"><span data-stu-id="4aeec-159">Provide the **File**, **Password**, then click **Complete** (the checkmark).</span></span>

## <a name="step-4-connect-to-the-role-instance-by-using-https"></a><span data-ttu-id="4aeec-160">4단계: HTTPS를 사용하여 역할 인스턴스에 연결</span><span class="sxs-lookup"><span data-stu-id="4aeec-160">Step 4: Connect to the role instance by using HTTPS</span></span>
<span data-ttu-id="4aeec-161">이제 Azure에서 배포가 실행되고 있으므로 HTTPS를 사용하여 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-161">Now that your deployment is up and running in Azure, you can connect to it using HTTPS.</span></span>

1. <span data-ttu-id="4aeec-162">Azure 클래식 포털에서 배포를 선택한 다음 **사이트 URL**아래의 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-162">In the Azure classic portal, select your deployment, then click the link under **Site URL**.</span></span>
   
   ![사이트 URL 확인][2]
2. <span data-ttu-id="4aeec-164">웹 브라우저에서 **http** 대신 **https**를 사용하도록 링크를 수정한 다음 페이지를 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-164">In your web browser, modify the link to use **https** instead of **http**, and then visit the page.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4aeec-165">자체 서명된 인증서를 사용하는 경우 자체 서명된 인증서와 연결된 HTTPS 끝점으로 이동하면 브라우저에 인증서오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-165">If you are using a self-signed certificate, when you browse to an HTTPS endpoint that's associated with the self-signed certificate you may see a certificate error in the browser.</span></span> <span data-ttu-id="4aeec-166">신뢰할 수 있는 인증 기관에서 서명한 인증서를 사용하면 이 문제가 해결되지만 이 오류는 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-166">Using a certificate signed by a trusted certification authority eliminates this problem; in the meantime, you can ignore the error.</span></span> <span data-ttu-id="4aeec-167">또 다른 옵션으로 사용자의 신뢰할 수 있는 인증 기관 인증서 저장소에 자체 서명된 인증서를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-167">(Another option is to add the self-signed certificate to the user's trusted certificate authority certificate store.)</span></span>
   > 
   > 
   
   ![SSL 예제 웹 사이트][3]

<span data-ttu-id="4aeec-169">프로덕션 배포가 아닌 스테이징 배포에 SSL을 사용하려면 먼저 스테이징 배포에 사용된 URL을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-169">If you want to use SSL for a staging deployment instead of a production deployment, you first need to determine the URL used for the staging deployment.</span></span> <span data-ttu-id="4aeec-170">인증서나 인증서 정보를 포함하지 않고도 스테이징 환경에 클라우드 서비스를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-170">Deploy your cloud service to the staging environment without including a certificate or any certificate information.</span></span> <span data-ttu-id="4aeec-171">배포된 다음에는 Azure 클래식 포털의 **사이트 URL** 필드에 나열되는 GUID 기반 URL을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-171">Once deployed, you can determine the GUID-based URL, which is listed in the Azure classic portal's **Site URL** field.</span></span> <span data-ttu-id="4aeec-172">GUID 기반 URL과 같은 CN(일반 이름)으로 인증서를 만듭니다(예: **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="4aeec-172">Create a certificate with the common name (CN) equal to the GUID-based URL (for example, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="4aeec-173">스테이징된 클라우드 서비스에 인증서를 추가하려면 Azure 클래식 포털을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-173">Use the Azure classic portal to add the certificate to your staged cloud service.</span></span> <span data-ttu-id="4aeec-174">그런 다음 인증서 정보를 CSDEF 및 CSCFG 파일에 추가하고 응용 프로그램을 다시 패키지하고 스테이징된 배포를 업데이트하여 새 패키지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-174">Then, add the certificate information to your CSDEF and CSCFG files, repackage your application, and update your staged deployment to use the new package.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4aeec-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4aeec-175">Next steps</span></span>
* <span data-ttu-id="4aeec-176">[클라우드 서비스의 일반 구성](cloud-services-how-to-configure.md)</span><span class="sxs-lookup"><span data-stu-id="4aeec-176">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="4aeec-177">[클라우드 서비스를 배포](cloud-services-how-to-create-deploy.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-177">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="4aeec-178">[사용자 지정 도메인 이름](cloud-services-custom-domain-name.md)을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4aeec-178">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="4aeec-179">[클라우드 서비스를 관리합니다](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="4aeec-179">[Manage your cloud service](cloud-services-how-to-manage.md).</span></span>

[Azure classic portal]: http://manage.windowsazure.com
[0]: ./media/cloud-services-configure-ssl-certificate/CreateCloudService.png
[1]: ./media/cloud-services-configure-ssl-certificate/AddCertificate.png
[2]: ./media/cloud-services-configure-ssl-certificate/CopyURL.png
[3]: ./media/cloud-services-configure-ssl-certificate/SSLCloudService.png
[4]: ./media/cloud-services-configure-ssl-certificate/AddCertificateComplete.png  
