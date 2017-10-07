---
title: "클라우드 서비스에 대 한 SSL aaaConfigure | Microsoft Docs"
description: "자세한 내용은 방법 toospecify 웹 역할 및 어떻게 tooupload SSL 인증서를 toosecure 응용 프로그램에 대 한 HTTPS 끝점입니다. 이러한 예제는 hello Azure 포털을 사용합니다."
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
ms.openlocfilehash: b19283bb7b0e95374f2ae9c3532eb1effc7d6a9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="f90ed-104">Azure에서 응용 프로그램에 대한 SSL 구성</span><span class="sxs-lookup"><span data-stu-id="f90ed-104">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f90ed-105">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="f90ed-105">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="f90ed-106">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="f90ed-106">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
>

<span data-ttu-id="f90ed-107">Secure Socket Layer (SSL) 암호화는 데이터 hello를 통해 전송 보안의 가장 일반적으로 사용 하는 hello 메서드 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-107">Secure Socket Layer (SSL) encryption is hello most commonly used method of securing data sent across hello internet.</span></span> <span data-ttu-id="f90ed-108">이 작업에 설명 방법을 toospecify 웹 역할 및 어떻게 tooupload SSL 인증서를 toosecure 응용 프로그램에 대 한 HTTPS 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-108">This common task discusses how toospecify an HTTPS endpoint for a web role and how tooupload an SSL certificate toosecure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="f90ed-109">이 작업의 절차에서는 hello 적용 tooAzure 클라우드 서비스 응용 프로그램 서비스에 대 한 참조 [이](../app-service-web/web-sites-configure-ssl-certificate.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-109">hello procedures in this task apply tooAzure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md).</span></span>
>

<span data-ttu-id="f90ed-110">이 작업에서는 프로덕션 배포를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-110">This task uses a production deployment.</span></span> <span data-ttu-id="f90ed-111">스테이징 배포를 사용 하는 방법은이 항목의 hello 끝에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-111">Information on using a staging deployment is provided at hello end of this topic.</span></span>

<span data-ttu-id="f90ed-112">클라우드 서비스를 아직 만들지 않은 경우 먼저 [이 문서를](cloud-services-how-to-create-deploy-portal.md) 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="f90ed-112">Read [this](cloud-services-how-to-create-deploy-portal.md) first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="f90ed-113">1단계: SSL 인증서 다운로드</span><span class="sxs-lookup"><span data-stu-id="f90ed-113">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="f90ed-114">응용 프로그램에 대 한 SSL을 tooconfigure, 먼저 tooget는 인증 기관 (CA)에서이 목적을 위해 인증서를 발급 하는 신뢰할 수 있는 타사 서명 된 SSL 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-114">tooconfigure SSL for an application, you first need tooget an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="f90ed-115">이미 않아도 하나, 하는 경우 SSL 인증서를 판매 하는 회사에서 tooobtain 하나 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-115">If you do not already have one, you need tooobtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="f90ed-116">hello 인증서 hello Azure에서 SSL 인증서에 대 한 요구 사항을 준수를 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-116">hello certificate must meet hello following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="f90ed-117">hello 인증서 개인 키를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-117">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="f90ed-118">키 교환, 내보낼 수 있는 tooa 개인 정보 교환 (.pfx) 파일에 대 한 hello 인증서를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-118">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="f90ed-119">hello 인증서의 주체 이름은 일치 해야 hello 사용 되는 도메인 tooaccess hello 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-119">hello certificate's subject name must match hello domain used tooaccess hello cloud service.</span></span> <span data-ttu-id="f90ed-120">Hello cloudapp.net 도메인에 대 한 인증 기관 (CA)에서 SSL 인증서를 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-120">You cannot obtain an SSL certificate from a certificate authority (CA) for hello cloudapp.net domain.</span></span> <span data-ttu-id="f90ed-121">사용자 지정 도메인 이름을 toouse 획득 해야 서비스에 액세스할 때.</span><span class="sxs-lookup"><span data-stu-id="f90ed-121">You must acquire a custom domain name toouse when access your service.</span></span> <span data-ttu-id="f90ed-122">CA에서 인증서를 요청한 응용 프로그램 hello 인증서의 주체 이름은 hello 사용자 지정 도메인 이름 사용 tooaccess 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-122">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name used tooaccess your application.</span></span> <span data-ttu-id="f90ed-123">예를 들어 사용자 지정 도메인 이름이 **contoso.com**인 경우 CA에서 ***.contoso.com** 또는 **www.contoso.com**에 대한 인증서를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-123">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="f90ed-124">hello 인증서 최소 2048 비트 암호화를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-124">hello certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="f90ed-125">테스트용으로 자체 서명된 인증서를 [만들어](cloud-services-certs-create.md) 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-125">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="f90ed-126">자체 서명 된 인증서가 CA를 통해 인증 되지 않은 및 hello cloudapp.net 도메인 hello 웹 사이트 URL로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-126">A self-signed certificate is not authenticated through a CA and can use hello cloudapp.net domain as hello website URL.</span></span> <span data-ttu-id="f90ed-127">예를 들어 hello 다음 태스크에서 사용 하는 hello CN (일반 이름) hello 인증서에 사용 되는 자체 서명 된 인증서 **sslexample.cloudapp.net**합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-127">For example, hello following task uses a self-signed certificate in which hello common name (CN) used in hello certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="f90ed-128">다음으로, 서비스 정 및 서비스 구성 파일에 hello 인증서에 대 한 정보를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-128">Next, you must include information about hello certificate in your service definition and service configuration files.</span></span>

<span data-ttu-id="f90ed-129"><a name="modify"> </a></span><span class="sxs-lookup"><span data-stu-id="f90ed-129"><a name="modify"> </a></span></span>

## <a name="step-2-modify-hello-service-definition-and-configuration-files"></a><span data-ttu-id="f90ed-130">2 단계: hello 서비스 정 및 구성 파일 수정</span><span class="sxs-lookup"><span data-stu-id="f90ed-130">Step 2: Modify hello service definition and configuration files</span></span>
<span data-ttu-id="f90ed-131">응용 프로그램 구성된 toouse hello 인증서 및 HTTPS 끝점을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-131">Your application must be configured toouse hello certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="f90ed-132">결과적으로, hello 서비스 정 및 서비스 구성 파일 필요한 toobe 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-132">As a result, hello service definition and service configuration files need toobe updated.</span></span>

1. <span data-ttu-id="f90ed-133">개발 환경의 hello 서비스 정의 파일 (CSDEF)을 열고, 추가 **인증서** hello 내의 섹션 **WebRole** 섹션을 hello에 대 한 다음 정보를 포함 합니다.는 인증서 (및 중간 인증서):</span><span class="sxs-lookup"><span data-stu-id="f90ed-133">In your development environment, open hello service definition file (CSDEF), add a **Certificates** section within hello **WebRole** section, and include hello following information about the certificate (and intermediate certificates):</span></span>

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Certificates>
            <Certificate name="SampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="My"
                        permissionLevel="limitedOrElevated" />
            <!-- IMPORTANT! Unless your certificate is either
            self-signed or signed directly by hello CA root, you
            must include all hello intermediate certificates
            here. You must list them here, even if they are
            not bound tooany endpoints. Failing toolist any of
            hello intermediate certificates may cause hard-to-reproduce
            interoperability problems on some clients.-->
            <Certificate name="CAForSampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="CA"
                        permissionLevel="limitedOrElevated" />
        </Certificates>
    ...
    </WebRole>
    ```

   <span data-ttu-id="f90ed-134">hello **인증서** 섹션에는 인증서, 위치 및 위치한 hello 저장소의 hello 이름을의 hello 이름을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-134">hello **Certificates** section defines hello name of our certificate, its location, and hello name of hello store where it is located.</span></span>

   <span data-ttu-id="f90ed-135">사용 권한 (`permisionLevel` 특성) 다음과 같은 값 사용의 hello 집합 tooone 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-135">Permissions (`permisionLevel` attribute) can be set tooone of hello following values:</span></span>

   | <span data-ttu-id="f90ed-136">권한 값</span><span class="sxs-lookup"><span data-stu-id="f90ed-136">Permission Value</span></span> | <span data-ttu-id="f90ed-137">설명</span><span class="sxs-lookup"><span data-stu-id="f90ed-137">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="f90ed-138">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="f90ed-138">limitedOrElevated</span></span> |<span data-ttu-id="f90ed-139">**(기본값)**  모든 역할 프로세스가 개인 키 hello에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-139">**(Default)** All role processes can access hello private key.</span></span> |
   | <span data-ttu-id="f90ed-140">elevated</span><span class="sxs-lookup"><span data-stu-id="f90ed-140">elevated</span></span> |<span data-ttu-id="f90ed-141">승격 된 프로세스만 개인 키 hello 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-141">Only elevated processes can access hello private key.</span></span> |

2. <span data-ttu-id="f90ed-142">서비스 정의 파일에서 추가 된 **InputEndpoint** hello 내의 요소 **끝점** tooenable HTTPS 섹션:</span><span class="sxs-lookup"><span data-stu-id="f90ed-142">In your service definition file, add an **InputEndpoint** element within hello **Endpoints** section tooenable HTTPS:</span></span>

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

3. <span data-ttu-id="f90ed-143">서비스 정의 파일에서 추가 된 **바인딩** hello 내의 요소 **사이트** 섹션.</span><span class="sxs-lookup"><span data-stu-id="f90ed-143">In your service definition file, add a **Binding** element within hello **Sites** section.</span></span> <span data-ttu-id="f90ed-144">이 요소는 HTTPS 바인딩 toomap 끝점 tooyour 사이트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-144">This element adds an HTTPS binding toomap the endpoint tooyour site:</span></span>

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

   <span data-ttu-id="f90ed-145">Toohello 서비스 정의 파일에 대 한 모든의 hello 필요한 변경을 완료 되었습니다. 하지만 hello 서비스 구성 파일에 tooadd hello 인증서 정보를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-145">All hello required changes toohello service definition file have been completed; but, you still need tooadd hello certificate information to hello service configuration file.</span></span>
4. <span data-ttu-id="f90ed-146">서비스 구성 파일(CSCFG), ServiceConfiguration.Cloud.cscfg에서 사용 중인 인증서 값에 해당하는 **Certificates** 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-146">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** value with that of your certificate.</span></span> <span data-ttu-id="f90ed-147">hello 다음 코드 샘플을 자세히 설명 hello **인증서** hello 지문 값을 제외한 섹션.</span><span class="sxs-lookup"><span data-stu-id="f90ed-147">hello following code sample provides details of hello **Certificates** section, except for hello thumbprint value.</span></span>

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

<span data-ttu-id="f90ed-148">(이 예에서는 **sha1** hello 지문 알고리즘에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-148">(This example uses **sha1** for hello thumbprint algorithm.</span></span> <span data-ttu-id="f90ed-149">Hello 인증서의 지문 알고리즘에 대 한 적절 한 값을 지정 합니다.)</span><span class="sxs-lookup"><span data-stu-id="f90ed-149">Specify hello appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="f90ed-150">Hello 서비스 정 및 서비스 구성 파일을 업데이트 한 했으므로 tooAzure 업로드에 대 한 배포를 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-150">Now that hello service definition and service configuration files have been updated, package your deployment for uploading tooAzure.</span></span> <span data-ttu-id="f90ed-151">**cspack**를 사용하는 경우 **/generateConfigurationFile** 플래그를 사용하지 않도록 하세요. 이 플래그는 방금 삽입한 인증서 정보를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-151">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that will overwrite the certificate information you just inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="f90ed-152">3단계: 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="f90ed-152">Step 3: Upload a certificate</span></span>
<span data-ttu-id="f90ed-153">Azure 포털 toohello 연결 및...</span><span class="sxs-lookup"><span data-stu-id="f90ed-153">Connect toohello Azure portal and...</span></span>

1. <span data-ttu-id="f90ed-154">Hello에 **모든 리소스** 섹션 hello 포털의 클라우드 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-154">In hello **All resources** section of hello Portal, select your cloud service.</span></span>

    ![클라우드 서비스 게시](media/cloud-services-configure-ssl-certificate-portal/browse.png)

2. <span data-ttu-id="f90ed-156">**인증서**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-156">Click **Certificates**.</span></span>

    ![Hello 인증서 아이콘을 클릭 합니다.](media/cloud-services-configure-ssl-certificate-portal/certificate-item.png)

3. <span data-ttu-id="f90ed-158">클릭 **업로드** hello hello 인증서 영역 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-158">Click **Upload** at hello top of hello certificates area.</span></span>

    ![Hello 업로드 메뉴 항목을 클릭 합니다.](media/cloud-services-configure-ssl-certificate-portal/Upload_menu.png)

4. <span data-ttu-id="f90ed-160">Hello 제공 **파일**, **암호**, 클릭 **업로드** hello hello 데이터 입력 영역 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-160">Provide hello **File**, **Password**, then click **Upload** at hello bottom of hello data entry area.</span></span>

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a><span data-ttu-id="f90ed-161">4 단계: toohello 역할 인스턴스를 HTTPS를 사용 하 여 연결</span><span class="sxs-lookup"><span data-stu-id="f90ed-161">Step 4: Connect toohello role instance by using HTTPS</span></span>
<span data-ttu-id="f90ed-162">배포 실행 되 고 Azure에서, 했으므로 tooit HTTPS를 사용 하 여 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-162">Now that your deployment is up and running in Azure, you can connect tooit using HTTPS.</span></span>

1. <span data-ttu-id="f90ed-163">Hello 클릭 **사이트 URL** tooopen hello 웹 브라우저를 합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-163">Click hello **Site URL** tooopen up hello web browser.</span></span>

   ![Hello 사이트 URL을 클릭 합니다.](media/cloud-services-configure-ssl-certificate-portal/navigate.png)

2. <span data-ttu-id="f90ed-165">웹 브라우저에서 hello 링크 toouse 수정 **https** 대신 **http**, hello 페이지를 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-165">In your web browser, modify hello link toouse **https** instead of **http**, and then visit hello page.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f90ed-166">Hello 자체 서명 된 인증서와 관련 된 tooan HTTPS 끝점을 찾을 때에 자체 서명 된 인증서를 사용 하는 hello 브라우저에 인증서 오류가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-166">If you are using a self-signed certificate, when you browse tooan HTTPS endpoint that's associated with hello self-signed certificate you may see a certificate error in hello browser.</span></span> <span data-ttu-id="f90ed-167">이 문제는 신뢰할 수 있는 인증 기관에서 서명한 인증서를 사용 하 여 제거 그 동안 hello에 hello 오류를 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-167">Using a certificate signed by a trusted certification authority eliminates this problem; in hello meantime, you can ignore hello error.</span></span> <span data-ttu-id="f90ed-168">(또 다른 옵션은 tooadd hello 자체 서명 된 인증서 toohello 사용자의 신뢰할 수 있는 인증 기관 인증서 저장소.)</span><span class="sxs-lookup"><span data-stu-id="f90ed-168">(Another option is tooadd hello self-signed certificate toohello user's trusted certificate authority certificate store.)</span></span>
   >
   >

   ![사이트 미리 보기](media/cloud-services-configure-ssl-certificate-portal/show-site.png)

   > [!TIP]
   > <span data-ttu-id="f90ed-170">프로덕션 배포 하는 대신 스테이징 배포에 대 한 SSL toouse 하려는 경우 먼저 hello 스테이징 배포에 사용 되는 toodetermine hello URL을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-170">If you want toouse SSL for a staging deployment instead of a production deployment, you'll first need toodetermine hello URL used for hello staging deployment.</span></span> <span data-ttu-id="f90ed-171">클라우드 서비스 배포 된 hello URL toohello 스테이징 환경 따라 사용자가 hello **배포 ID** 이 형식의 GUID:`https://deployment-id.cloudapp.net/`</span><span class="sxs-lookup"><span data-stu-id="f90ed-171">Once your cloud service has been deployed, hello URL toohello staging environment is determined by hello **Deployment ID** GUID in this format: `https://deployment-id.cloudapp.net/`</span></span>  
   >
   > <span data-ttu-id="f90ed-172">Hello 일반 이름 (CN) 같은 toohello GUID 기반 URL으로 인증서를 만듭니다 (예를 들어 **328187776e774ceda8fc57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="f90ed-172">Create a certificate with hello common name (CN) equal toohello GUID-based URL (for example, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="f90ed-173">사용 하 여 hello 포털 tooadd hello 인증서 tooyour 클라우드 서비스를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-173">Use hello portal tooadd hello certificate tooyour staged cloud service.</span></span> <span data-ttu-id="f90ed-174">그런 다음 hello는 인증서 정보 tooyour CSDEF 및 CSCFG 파일을 추가 하 고 응용 프로그램을 다시 패키지 다음 준비 된 배포 toouse hello 새 패키지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-174">Then, add hello certificate information tooyour CSDEF and CSCFG files, repackage your application, and update your staged deployment toouse hello new package.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="f90ed-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f90ed-175">Next steps</span></span>
* <span data-ttu-id="f90ed-176">[클라우드 서비스의 일반 구성](cloud-services-how-to-configure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="f90ed-176">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="f90ed-177">너무 방법에 대해 알아봅니다[클라우드 서비스 배포](cloud-services-how-to-create-deploy-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f90ed-177">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="f90ed-178">[사용자 지정 도메인 이름](cloud-services-custom-domain-name-portal.md)구성</span><span class="sxs-lookup"><span data-stu-id="f90ed-178">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="f90ed-179">[클라우드 서비스를 관리합니다](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f90ed-179">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
