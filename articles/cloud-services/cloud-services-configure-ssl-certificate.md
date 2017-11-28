---
title: "클라우드 서비스 (클래식)에 대 한 SSL aaaConfigure | Microsoft Docs"
description: "자세한 내용은 방법 toospecify 웹 역할 및 어떻게 tooupload SSL 인증서를 toosecure 응용 프로그램에 대 한 HTTPS 끝점입니다."
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
ms.openlocfilehash: a1ca031b98af49d371977a208ed24f6dc8ea2ac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="d2627-103">Azure에서 응용 프로그램에 대한 SSL 구성</span><span class="sxs-lookup"><span data-stu-id="d2627-103">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d2627-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="d2627-104">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="d2627-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="d2627-105">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
> 
> 

<span data-ttu-id="d2627-106">Secure Socket Layer (SSL) 암호화는 데이터 hello를 통해 전송 보안의 가장 일반적으로 사용 하는 hello 메서드 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-106">Secure Socket Layer (SSL) encryption is hello most commonly used method of securing data sent across hello internet.</span></span> <span data-ttu-id="d2627-107">이 작업에 설명 방법을 toospecify 웹 역할 및 어떻게 tooupload SSL 인증서를 toosecure 응용 프로그램에 대 한 HTTPS 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-107">This common task discusses how toospecify an HTTPS endpoint for a web role and how tooupload an SSL certificate toosecure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="d2627-108">이 작업의 절차에서는 hello 적용 tooAzure 클라우드 서비스 응용 프로그램 서비스에 대 한 참조 [이](../app-service-web/web-sites-configure-ssl-certificate.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="d2627-108">hello procedures in this task apply tooAzure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md) article.</span></span>
> 
> 

<span data-ttu-id="d2627-109">이 작업에서는 프로덕션 배포를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-109">This task uses a production deployment.</span></span> <span data-ttu-id="d2627-110">스테이징 배포를 사용 하는 방법은이 항목의 hello 끝에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-110">Information on using a staging deployment is provided at hello end of this topic.</span></span>

<span data-ttu-id="d2627-111">클라우드 서비스를 아직 만들지 않은 경우 먼저 [이](cloud-services-how-to-create-deploy.md) 문서를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="d2627-111">Read [this](cloud-services-how-to-create-deploy.md) article first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="d2627-112">1단계: SSL 인증서 다운로드</span><span class="sxs-lookup"><span data-stu-id="d2627-112">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="d2627-113">응용 프로그램에 대 한 SSL을 tooconfigure, 먼저 tooget는 인증 기관 (CA)에서이 목적을 위해 인증서를 발급 하는 신뢰할 수 있는 타사 서명 된 SSL 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-113">tooconfigure SSL for an application, you first need tooget an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="d2627-114">이미 않아도 하나, 하는 경우 SSL 인증서를 판매 하는 회사에서 tooobtain 하나 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-114">If you do not already have one, you need tooobtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="d2627-115">hello 인증서 hello Azure에서 SSL 인증서에 대 한 요구 사항을 준수를 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-115">hello certificate must meet hello following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="d2627-116">hello 인증서 개인 키를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-116">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="d2627-117">키 교환, 내보낼 수 있는 tooa 개인 정보 교환 (.pfx) 파일에 대 한 hello 인증서를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-117">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="d2627-118">hello 인증서의 주체 이름은 일치 해야 hello 사용 되는 도메인 tooaccess hello 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-118">hello certificate's subject name must match hello domain used tooaccess hello cloud service.</span></span> <span data-ttu-id="d2627-119">Hello cloudapp.net 도메인에 대 한 인증 기관 (CA)에서 SSL 인증서를 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-119">You cannot obtain an SSL certificate from a certificate authority (CA) for hello cloudapp.net domain.</span></span> <span data-ttu-id="d2627-120">사용자 지정 도메인 이름을 toouse 획득 해야 서비스에 액세스할 때.</span><span class="sxs-lookup"><span data-stu-id="d2627-120">You must acquire a custom domain name toouse when access your service.</span></span> <span data-ttu-id="d2627-121">CA에서 인증서를 요청한 응용 프로그램 hello 인증서의 주체 이름은 hello 사용자 지정 도메인 이름 사용 tooaccess 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-121">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name used tooaccess your application.</span></span> <span data-ttu-id="d2627-122">예를 들어 사용자 지정 도메인 이름이 **contoso.com**인 경우 CA에서 ***.contoso.com** 또는 **www.contoso.com**에 대한 인증서를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-122">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="d2627-123">hello 인증서 최소 2048 비트 암호화를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-123">hello certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="d2627-124">테스트용으로 자체 서명된 인증서를 [만들어](cloud-services-certs-create.md) 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-124">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="d2627-125">자체 서명 된 인증서가 CA를 통해 인증 되지 않은 및 hello cloudapp.net 도메인 hello 웹 사이트 URL로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-125">A self-signed certificate is not authenticated through a CA and can use hello cloudapp.net domain as hello website URL.</span></span> <span data-ttu-id="d2627-126">예를 들어 hello 다음 태스크에서 사용 하는 hello CN (일반 이름) hello 인증서에 사용 되는 자체 서명 된 인증서 **sslexample.cloudapp.net**합니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-126">For example, hello following task uses a self-signed certificate in which hello common name (CN) used in hello certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="d2627-127">다음으로, 서비스 정 및 서비스 구성 파일에 hello 인증서에 대 한 정보를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-127">Next, you must include information about hello certificate in your service definition and service configuration files.</span></span>

## <a name="step-2-modify-hello-service-definition-and-configuration-files"></a><span data-ttu-id="d2627-128">2 단계: hello 서비스 정 및 구성 파일 수정</span><span class="sxs-lookup"><span data-stu-id="d2627-128">Step 2: Modify hello service definition and configuration files</span></span>
<span data-ttu-id="d2627-129">응용 프로그램 구성된 toouse hello 인증서 및 HTTPS 끝점을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-129">Your application must be configured toouse hello certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="d2627-130">결과적으로, hello 서비스 정 및 서비스 구성 파일 필요한 toobe 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-130">As a result, hello service definition and service configuration files need toobe updated.</span></span>

1. <span data-ttu-id="d2627-131">개발 환경의 hello 서비스 정의 파일 (CSDEF)을 열고, 추가 **인증서** hello 내의 섹션 **WebRole** 섹션을 hello에 대 한 다음 정보를 포함 합니다.는 인증서 (및 중간 인증서):</span><span class="sxs-lookup"><span data-stu-id="d2627-131">In your development environment, open hello service definition file (CSDEF), add a **Certificates** section within hello **WebRole** section, and include hello following information about the certificate (and intermediate certificates):</span></span>
   
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
   
   <span data-ttu-id="d2627-132">hello **인증서** 섹션에는 인증서, 위치 및 위치한 hello 저장소의 hello 이름을의 hello 이름을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-132">hello **Certificates** section defines hello name of our certificate, its location, and hello name of hello store where it is located.</span></span>
   
   <span data-ttu-id="d2627-133">사용 권한 (`permisionLevel` 특성) 다음과 같은 값 사용의 hello 집합 tooone 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-133">Permissions (`permisionLevel` attribute) can be set tooone of hello following values:</span></span>
   
   | <span data-ttu-id="d2627-134">권한 값</span><span class="sxs-lookup"><span data-stu-id="d2627-134">Permission Value</span></span> | <span data-ttu-id="d2627-135">설명</span><span class="sxs-lookup"><span data-stu-id="d2627-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="d2627-136">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="d2627-136">limitedOrElevated</span></span> |<span data-ttu-id="d2627-137">**(기본값)**  모든 역할 프로세스가 개인 키 hello에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-137">**(Default)** All role processes can access hello private key.</span></span> |
   | <span data-ttu-id="d2627-138">elevated</span><span class="sxs-lookup"><span data-stu-id="d2627-138">elevated</span></span> |<span data-ttu-id="d2627-139">승격 된 프로세스만 개인 키 hello 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-139">Only elevated processes can access hello private key.</span></span> |
2. <span data-ttu-id="d2627-140">서비스 정의 파일에서 추가 된 **InputEndpoint** hello 내의 요소 **끝점** tooenable HTTPS 섹션:</span><span class="sxs-lookup"><span data-stu-id="d2627-140">In your service definition file, add an **InputEndpoint** element within hello **Endpoints** section tooenable HTTPS:</span></span>
   
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

3. <span data-ttu-id="d2627-141">서비스 정의 파일에서 추가 된 **바인딩** hello 내의 요소 **사이트** 섹션.</span><span class="sxs-lookup"><span data-stu-id="d2627-141">In your service definition file, add a **Binding** element within hello **Sites** section.</span></span> <span data-ttu-id="d2627-142">이 섹션에는 HTTPS 바인딩 toomap 끝점 tooyour 사이트 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-142">This section adds an HTTPS binding toomap the endpoint tooyour site:</span></span>
   
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
   
   <span data-ttu-id="d2627-143">Toohello 서비스 정의 파일에 대 한 모든의 hello 필요한 변경 작업을 완료 하지만 hello 서비스 구성 파일에 tooadd hello 인증서 정보를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-143">All hello required changes toohello service definition file have been completed, but you still need tooadd hello certificate information to hello service configuration file.</span></span>
4. <span data-ttu-id="d2627-144">서비스 구성 파일 (CSCFG) ServiceConfiguration.Cloud.cscfg에서는 추가 **인증서** hello 내의 섹션 **역할** 섹션에서 다음 hello 샘플 지문 값 바꾸기 인증서의 해당:</span><span class="sxs-lookup"><span data-stu-id="d2627-144">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** section within hello **Role** section, replacing hello sample thumbprint value shown below with that of your certificate:</span></span>
   
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

<span data-ttu-id="d2627-145">(앞에 사용 하 여 예제 hello **sha1** hello 지문 알고리즘에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-145">(hello preceding example uses **sha1** for hello thumbprint algorithm.</span></span> <span data-ttu-id="d2627-146">Hello 인증서의 지문 알고리즘에 대 한 적절 한 값을 지정 합니다.)</span><span class="sxs-lookup"><span data-stu-id="d2627-146">Specify hello appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="d2627-147">Hello 서비스 정 및 서비스 구성 파일을 업데이트 한 했으므로 tooAzure 업로드에 대 한 배포를 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-147">Now that hello service definition and service configuration files have been updated, package your deployment for uploading tooAzure.</span></span> <span data-ttu-id="d2627-148">**cspack**를 사용하는 경우 **/generateConfigurationFile** 플래그를 사용하지 않도록 하세요. 이 플래그는 방금 삽입한 인증서 정보를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-148">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that overwrites the certificate information you inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="d2627-149">3단계: 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="d2627-149">Step 3: Upload a certificate</span></span>
<span data-ttu-id="d2627-150">배포 패키지 업데이트 toouse hello 인증서 및 HTTPS 끝점이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-150">Your deployment package has been updated toouse hello certificate, and an HTTPS endpoint has been added.</span></span> <span data-ttu-id="d2627-151">이제 hello 패키지 및 인증서 tooAzure hello Azure 클래식 포털으로 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-151">Now you can upload hello package and certificate tooAzure with hello Azure classic portal.</span></span>

1. <span data-ttu-id="d2627-152">Toohello 로그인 [Azure 클래식 포털][Azure classic portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-152">Log in toohello [Azure classic portal][Azure classic portal].</span></span> 
2. <span data-ttu-id="d2627-153">클릭 **클라우드 서비스** hello 왼쪽 탐색 창에서.</span><span class="sxs-lookup"><span data-stu-id="d2627-153">Click **Cloud Services** on hello left-side navigation pane.</span></span>
3. <span data-ttu-id="d2627-154">원하는 hello 클라우드 서비스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-154">Click hello desired cloud service.</span></span>
4. <span data-ttu-id="d2627-155">Hello 클릭 **인증서** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-155">Click hello **Certificates** tab.</span></span>
   
    ![Hello 인증서 탭을 클릭 합니다.](./media/cloud-services-configure-ssl-certificate/click-cert.png)

5. <span data-ttu-id="d2627-157">Hello 클릭 **업로드** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-157">Click hello **Upload** button.</span></span>
   
    ![업로드](./media/cloud-services-configure-ssl-certificate/upload-button.png)
    
6. <span data-ttu-id="d2627-159">Hello 제공 **파일**, **암호**, 클릭 **완료** (확인 표시를 hello).</span><span class="sxs-lookup"><span data-stu-id="d2627-159">Provide hello **File**, **Password**, then click **Complete** (hello checkmark).</span></span>

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a><span data-ttu-id="d2627-160">4 단계: toohello 역할 인스턴스를 HTTPS를 사용 하 여 연결</span><span class="sxs-lookup"><span data-stu-id="d2627-160">Step 4: Connect toohello role instance by using HTTPS</span></span>
<span data-ttu-id="d2627-161">배포 실행 되 고 Azure에서, 했으므로 tooit HTTPS를 사용 하 여 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-161">Now that your deployment is up and running in Azure, you can connect tooit using HTTPS.</span></span>

1. <span data-ttu-id="d2627-162">에 Azure 클래식 포털 hello, 배포를 선택 하 고 아래 hello 링크를 클릭 **사이트 URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-162">In hello Azure classic portal, select your deployment, then click hello link under **Site URL**.</span></span>
   
   ![사이트 URL 확인][2]
2. <span data-ttu-id="d2627-164">웹 브라우저에서 hello 링크 toouse 수정 **https** 대신 **http**, hello 페이지를 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-164">In your web browser, modify hello link toouse **https** instead of **http**, and then visit hello page.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d2627-165">Hello 자체 서명 된 인증서와 관련 된 tooan HTTPS 끝점을 찾을 때에 자체 서명 된 인증서를 사용 하는 hello 브라우저에 인증서 오류가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-165">If you are using a self-signed certificate, when you browse tooan HTTPS endpoint that's associated with hello self-signed certificate you may see a certificate error in hello browser.</span></span> <span data-ttu-id="d2627-166">이 문제는 신뢰할 수 있는 인증 기관에서 서명한 인증서를 사용 하 여 제거 그 동안 hello에 hello 오류를 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-166">Using a certificate signed by a trusted certification authority eliminates this problem; in hello meantime, you can ignore hello error.</span></span> <span data-ttu-id="d2627-167">(또 다른 옵션은 tooadd hello 자체 서명 된 인증서 toohello 사용자의 신뢰할 수 있는 인증 기관 인증서 저장소.)</span><span class="sxs-lookup"><span data-stu-id="d2627-167">(Another option is tooadd hello self-signed certificate toohello user's trusted certificate authority certificate store.)</span></span>
   > 
   > 
   
   ![SSL 예제 웹 사이트][3]

<span data-ttu-id="d2627-169">프로덕션 배포 하는 대신 스테이징 배포에 대 한 SSL toouse 하려는 경우 먼저 toodetermine hello URL hello 스테이징 배포에 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-169">If you want toouse SSL for a staging deployment instead of a production deployment, you first need toodetermine hello URL used for hello staging deployment.</span></span> <span data-ttu-id="d2627-170">인증서 또는 인증서 정보를 포함 하지 않고 클라우드 서비스 toohello 준비 환경을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-170">Deploy your cloud service toohello staging environment without including a certificate or any certificate information.</span></span> <span data-ttu-id="d2627-171">배포 된 hello GUID 기반 URL을 hello Azure 클래식 포털의에 나열 된 결정할 수 있습니다 **사이트 URL** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-171">Once deployed, you can determine hello GUID-based URL, which is listed in hello Azure classic portal's **Site URL** field.</span></span> <span data-ttu-id="d2627-172">Hello 일반 이름 (CN) 같은 toohello GUID 기반 URL으로 인증서를 만듭니다 (예를 들어 **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="d2627-172">Create a certificate with hello common name (CN) equal toohello GUID-based URL (for example, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="d2627-173">사용 하 여 hello Azure 클래식 포털 tooadd hello 인증서 tooyour 클라우드 서비스를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-173">Use hello Azure classic portal tooadd hello certificate tooyour staged cloud service.</span></span> <span data-ttu-id="d2627-174">그런 다음 hello는 인증서 정보 tooyour CSDEF 및 CSCFG 파일을 추가 하 고 응용 프로그램을 다시 패키지 다음 준비 된 배포 toouse hello 새 패키지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-174">Then, add hello certificate information tooyour CSDEF and CSCFG files, repackage your application, and update your staged deployment toouse hello new package.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2627-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d2627-175">Next steps</span></span>
* <span data-ttu-id="d2627-176">[클라우드 서비스의 일반 구성](cloud-services-how-to-configure.md)</span><span class="sxs-lookup"><span data-stu-id="d2627-176">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="d2627-177">너무 방법에 대해 알아봅니다[클라우드 서비스 배포](cloud-services-how-to-create-deploy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2627-177">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="d2627-178">[사용자 지정 도메인 이름](cloud-services-custom-domain-name.md)구성</span><span class="sxs-lookup"><span data-stu-id="d2627-178">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="d2627-179">[클라우드 서비스를 관리합니다](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="d2627-179">[Manage your cloud service](cloud-services-how-to-manage.md).</span></span>

[Azure classic portal]: http://manage.windowsazure.com
[0]: ./media/cloud-services-configure-ssl-certificate/CreateCloudService.png
[1]: ./media/cloud-services-configure-ssl-certificate/AddCertificate.png
[2]: ./media/cloud-services-configure-ssl-certificate/CopyURL.png
[3]: ./media/cloud-services-configure-ssl-certificate/SSLCloudService.png
[4]: ./media/cloud-services-configure-ssl-certificate/AddCertificateComplete.png  
