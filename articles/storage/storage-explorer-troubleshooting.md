---
title: "Azure Storage 탐색기 문제 해결 가이드 | Microsoft Docs"
description: "Azure의 두 가지 디버깅 기능 개요"
services: virtual-machines
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: delhan
ms.openlocfilehash: e9b833b07556378f17d9aaff0912c7d73dff44eb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-storage-explorer-troubleshooting-guide"></a><span data-ttu-id="68297-103">Azure Storage 탐색기 문제 해결 가이드</span><span class="sxs-lookup"><span data-stu-id="68297-103">Azure Storage Explorer troubleshooting guide</span></span>

## <a name="introduction"></a><span data-ttu-id="68297-104">소개</span><span class="sxs-lookup"><span data-stu-id="68297-104">Introduction</span></span>

<span data-ttu-id="68297-105">Microsoft Azure Storage 탐색기(미리 보기)는 Windows, macOS 및 Linux에서 Azure Storage 데이터를 손쉽게 사용할 수 있는 독립 실행형 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="68297-105">Microsoft Azure Storage Explorer (Preview) is a stand-alone app that enables you to easily work with Azure Storage data on Windows, macOS and Linux.</span></span> <span data-ttu-id="68297-106">앱은 Azure, Sovereign Clouds 및 Azure Stack에서 호스트되는 저장소 계정에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68297-106">The app can connect toStorage accounts hosted on Azure, Sovereign Clouds, and Azure Stack.</span></span>

<span data-ttu-id="68297-107">이 가이드에는 Storage 탐색기에 나타나는 일반적인 문제에 대한 솔루션이 요약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68297-107">This guide summarizes solutions for common issues seen in Storage Explorer.</span></span>

## <a name="sign-in-issues"></a><span data-ttu-id="68297-108">로그인 문제</span><span class="sxs-lookup"><span data-stu-id="68297-108">Sign in issues</span></span>

<span data-ttu-id="68297-109">AAD(Azure Active Directory) 계정만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="68297-109">Only Azure Active Directory (AAD) accounts are supported.</span></span> <span data-ttu-id="68297-110">ADFS 계정을 사용하는 경우 Storage 탐색기에 대한 로그인은 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68297-110">If you use an ADFS account, it’s expected that signing in to Storage Explorer would not work.</span></span> <span data-ttu-id="68297-111">계속하기 전에 응용 프로그램을 다시 시작하고 문제가 해결될 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-111">Before you continue, try restarting your application and see whether the problems can be fixed.</span></span>

### <a name="error-self-signed-certificate-in-certificate-chain"></a><span data-ttu-id="68297-112">오류: 인증서 체인의 자체 서명된 인증서</span><span class="sxs-lookup"><span data-stu-id="68297-112">Error: Self-Signed Certificate in Certificate Chain</span></span>

<span data-ttu-id="68297-113">이 오류가 발생할 수 있는 몇 가지 이유가 있으며 가장 일반적인 두 가지 이유는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="68297-113">There are several reasons why you may encounter this error, and the most common two reasons are as follows:</span></span>

1. <span data-ttu-id="68297-114">앱이 "투명 프록시"를 통해 연결됩니다. 즉, 회사 서버와 같은 서버가 HTTPS 트래픽을 가로 채고 해독한 다음 자체 서명된 인증서를 사용하여 암호화하는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-114">The app is connected through a “transparent proxy”, which means a server (such as your company server) is intercepting HTTPS traffic, decrypting it, and then encrypting it using a self-signed certificate.</span></span>

2. <span data-ttu-id="68297-115">수신한 HTTPS 메시지에 자체 서명된 SSL 인증서를 삽입하는 바이러스 백신 소프트웨어와 같은 응용 프로그램을 실행하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68297-115">You are running an application, such as antivirus software, which is injecting a self-signed SSL certificate into the HTTPS messages that you receive.</span></span>

<span data-ttu-id="68297-116">Storage 탐색기에서 문제 중 하나를 발견하면 수신된 HTTPS 메시지가 변조되었는지 여부를 더 이상 알 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="68297-116">When Storage Explorer encounters one of the issues, it can no longer know whether the received HTTPS message is tampered.</span></span> <span data-ttu-id="68297-117">자체 서명된 인증서의 복사본이 있으면 Storage 탐색기에서 이를 신뢰하게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68297-117">If you have a copy of the self-signed certificate, you can let Storage Explorer trust it.</span></span> <span data-ttu-id="68297-118">누가 인증서를 삽입하고 있는지 확실하지 않은 경우 다음 단계를 수행하여 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="68297-118">If you are unsure of who is injecting the certificate, follow these steps to find it:</span></span>

1. <span data-ttu-id="68297-119">OpenSSL을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-119">Install Open SSL</span></span>

    - <span data-ttu-id="68297-120">[Windows](https://slproweb.com/products/Win32OpenSSL.html)(라이트 버전이면 충분함)</span><span class="sxs-lookup"><span data-stu-id="68297-120">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (any of the light versions should be sufficient)</span></span>

    - <span data-ttu-id="68297-121">Mac 및 Linux: 운영 체제에 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-121">Mac and Linux: should be included with your operating system</span></span>

2. <span data-ttu-id="68297-122">OpenSSL을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-122">Run Open SSL</span></span>

    - <span data-ttu-id="68297-123">Windows: 설치 디렉터리를 열고 **/bin/**을 클릭한 다음 **openssl.exe**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-123">Windows: open the installation directory, click **/bin/**, and then double-click **openssl.exe**.</span></span>
    - <span data-ttu-id="68297-124">Mac 및 Linux: 터미널에서 **openssl**을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-124">Mac and Linux: run **openssl** from a terminal.</span></span>

3. <span data-ttu-id="68297-125">s_client -showcerts -connect microsoft.com :443을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-125">Execute s_client -showcerts -connect microsoft.com:443</span></span>

4. <span data-ttu-id="68297-126">자체 서명된 인증서를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="68297-126">Look for self-signed certificates.</span></span> <span data-ttu-id="68297-127">어떤 인증서가 자체 서명된 것인지 확실하지 않은 경우 제목("s:")과 발급자("i:")가 같은 위치를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="68297-127">If you are unsure which are self-signed, look for anywhere the subject ("s:") and issuer ("i:") are the same.</span></span>

5. <span data-ttu-id="68297-128">자체 서명된 인증서를 찾았으면 각 인증서에 대해 **----- BEGIN CERTIFICATE -----**부터 **----- END CERTIFICATE -----**까지 모든 줄을 복사하여 새 .cer 파일에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="68297-128">When you have found any self-signed certificates, for each one, copy and paste everything from and including **-----BEGIN CERTIFICATE-----** to **-----END CERTIFICATE-----** to a new .cer file.</span></span>

6. <span data-ttu-id="68297-129">Storage 탐색기를 열고 **편집** > **SSL 인증서** > **인증서 가져오기**를 클릭한 다음 파일 선택기를 사용하여 만든 .cer 파일을 찾고 선택하고 엽니다.</span><span class="sxs-lookup"><span data-stu-id="68297-129">Open Storage Explorer, click **Edit** > **SSL Certificates** > **Import Certificates**, and then use the file picker to find, select, and open the .cer files that you created.</span></span>

<span data-ttu-id="68297-130">위의 단계를 사용하여 자체 서명된 인증서를 찾을 수 없는 경우 사용자 의견 도구를 통해 당사에 문의하여 도움을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="68297-130">If you cannot find any self-signed certificates using the above steps, contact us through the feedback tool for more help.</span></span>

### <a name="unable-to-retrieve-subscriptions"></a><span data-ttu-id="68297-131">구독을 검색할 수 없음</span><span class="sxs-lookup"><span data-stu-id="68297-131">Unable to retrieve subscriptions</span></span>

<span data-ttu-id="68297-132">성공적으로 로그인한 후 구독을 검색할 수 없는 경우 다음 단계에 따라 이 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-132">If you are unable to retrieve your subscriptions after you successfully sign in, follow these steps to troubleshoot this issue:</span></span>

- <span data-ttu-id="68297-133">Azure Portal에 로그인하여 계정이 구독에 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-133">Verify that your account has access to the subscriptions by signing into the Azure portal.</span></span>

- <span data-ttu-id="68297-134">올바른 환경(Azure, Azure China, Azure Germany, Azure US Government 또는 사용자 지정 환경/Azure Stack)을 사용하여 로그인했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-134">Make sure that you have signed in using the correct environment (Azure, Azure China, Azure Germany, Azure US Government, or Custom Environment/Azure Stack).</span></span>

- <span data-ttu-id="68297-135">프록시 뒤에 있는 경우 Storage 탐색기 프록시를 제대로 구성했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-135">If you are behind a proxy, make sure that you have configured the Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="68297-136">계정을 제거하고 다시 추가해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="68297-136">Try removing and readding the account.</span></span>

- <span data-ttu-id="68297-137">루트 디렉터리(즉, C:\Users\ContosoUser)에서 다음 파일을 삭제한 다음 계정을 다시 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-137">Try deleting the following files from your root directory (that is, C:\Users\ContosoUser), and then re-adding the account:</span></span>

    - <span data-ttu-id="68297-138">.adalcache</span><span class="sxs-lookup"><span data-stu-id="68297-138">.adalcache</span></span>

    - <span data-ttu-id="68297-139">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="68297-139">.devaccounts</span></span>

    - <span data-ttu-id="68297-140">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="68297-140">.extaccounts</span></span>

- <span data-ttu-id="68297-141">로그인할 때 F12 키를 눌러 개발자 도구 콘솔에서 오류 메시지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-141">Watch the developer tools console (by pressing F12) when you are signing in for any error messages:</span></span>

![개발자 도구](./media/storage-explorer-troubleshooting/4022501_en_2.png)

### <a name="unable-to-see-the-authentication-page"></a><span data-ttu-id="68297-143">인증 페이지를 볼 수 없음</span><span class="sxs-lookup"><span data-stu-id="68297-143">Unable to see the authentication page</span></span>

<span data-ttu-id="68297-144">인증 페이지를 볼 수 없는 경우 다음 단계에 따라 이 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-144">If you are unable to see the authentication page, follow these steps to troubleshoot this issue:</span></span>

- <span data-ttu-id="68297-145">연결 속도에 따라 로그인 페이지가 로드되는 데 시간이 걸릴 수 있으므로 인증 대화 상자를 닫기 전에 1분 이상 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="68297-145">Depending on the speed of your connection, it may take a while for the sign-in page to load, wait at least one minute before closing the authentication dialog box.</span></span>

- <span data-ttu-id="68297-146">프록시 뒤에 있는 경우 Storage 탐색기 프록시를 제대로 구성했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-146">If you are behind a proxy, make sure that you have configured the Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="68297-147">F12 키를 눌러 개발자 콘솔을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-147">View the developer console by pressing the F12 key.</span></span> <span data-ttu-id="68297-148">개발자 콘솔의 응답을 보고 인증이 작동하지 않는 이유에 대한 단서를 찾을 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-148">Watch the responses from the developer console and see whether you can find any clue for why authentication not working.</span></span>

### <a name="cannot-remove-account"></a><span data-ttu-id="68297-149">계정을 제거할 수 없음</span><span class="sxs-lookup"><span data-stu-id="68297-149">Cannot remove account</span></span>

<span data-ttu-id="68297-150">계정을 제거할 수 없거나 재인증 링크가 작동하지 않는 경우 다음 단계에 따라 이 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-150">If you are unable to remove an account, or if the reauthenticate link does not do anything, follow these steps to troubleshoot this issue:</span></span>

- <span data-ttu-id="68297-151">루트 디렉터리에서 다음 파일을 삭제한 다음 계정을 다시 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-151">Try deleting the following files from your root directory, and then readding the account:</span></span>

    - <span data-ttu-id="68297-152">.adalcache</span><span class="sxs-lookup"><span data-stu-id="68297-152">.adalcache</span></span>

    - <span data-ttu-id="68297-153">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="68297-153">.devaccounts</span></span>

    - <span data-ttu-id="68297-154">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="68297-154">.extaccounts</span></span>

- <span data-ttu-id="68297-155">SAS 연결 Storage 리소스를 제거하려면 다음 파일을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-155">If you want to remove SAS attached Storage resources, delete the following files:</span></span>

    - <span data-ttu-id="68297-156">Windows - %AppData%/StorageExplorer 폴더</span><span class="sxs-lookup"><span data-stu-id="68297-156">%AppData%/StorageExplorer folder for Windows</span></span>

    - <span data-ttu-id="68297-157">Mac - Users/<your_name>/Library/Applicaiton SUpport/StorageExplorer</span><span class="sxs-lookup"><span data-stu-id="68297-157">/Users/<your_name>/Library/Applicaiton SUpport/StorageExplorer for Mac</span></span>

    - <span data-ttu-id="68297-158">Linux - ~/.config/StorageExplorer</span><span class="sxs-lookup"><span data-stu-id="68297-158">~/.config/StorageExplorer for Linux</span></span>

> [!NOTE]
>  <span data-ttu-id="68297-159">이러한 파일을 삭제하면 모든 자격 증명을 다시 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-159">You will have to reenter all your credentials if you delete these files.</span></span>

## <a name="proxy-issues"></a><span data-ttu-id="68297-160">프록시 문제</span><span class="sxs-lookup"><span data-stu-id="68297-160">Proxy issues</span></span>

<span data-ttu-id="68297-161">먼저 입력한 다음 정보가 모두 올바른지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-161">First, make sure that the following information you entered are all correct:</span></span>

- <span data-ttu-id="68297-162">프록시 URL 및 포트 번호</span><span class="sxs-lookup"><span data-stu-id="68297-162">The proxy URL and port number</span></span>

- <span data-ttu-id="68297-163">프록시가 요구하는 경우 사용자 이름과 암호</span><span class="sxs-lookup"><span data-stu-id="68297-163">Username and password if required by the proxy</span></span>

### <a name="common-solutions"></a><span data-ttu-id="68297-164">일반적인 솔루션</span><span class="sxs-lookup"><span data-stu-id="68297-164">Common solutions</span></span>

<span data-ttu-id="68297-165">여전히 문제가 발생하는 경우 다음 단계에 따라 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-165">If you are still experiencing issues, follow these steps to troubleshoot them:</span></span>

- <span data-ttu-id="68297-166">프록시를 사용하지 않고 인터넷에 연결할 수 있으면 프록시 설정을 사용하지 않고 Storage 탐색기가 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-166">If you can connect to the Internet without using your proxy, verify that Storage Explorer works without proxy settings enabled.</span></span> <span data-ttu-id="68297-167">이 경우 프록시 설정에 문제가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68297-167">If this is the case, there may be an issue with your proxy settings.</span></span> <span data-ttu-id="68297-168">프록시 관리자와 함께 문제를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-168">Work with your proxy administrator to identify the problems.</span></span>

- <span data-ttu-id="68297-169">프록시 서버를 사용하는 다른 응용 프로그램이 예상대로 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-169">Verify that other applications using the proxy server work as expected.</span></span>

- <span data-ttu-id="68297-170">웹 브라우저를 사용하여 Microsoft Azure Portal에 연결할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-170">Verify that you can connect to the Microsoft Azure portal using your web browser</span></span>

- <span data-ttu-id="68297-171">서비스 끝점에서 응답을 수신할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-171">Verify that you can receive responses from your service endpoints.</span></span> <span data-ttu-id="68297-172">끝점 URL 중 하나를 브라우저에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-172">Enter one of your endpoint URLs into your browser.</span></span> <span data-ttu-id="68297-173">연결할 수 있으면 InvalidQueryParameterValue 또는 유사한 XML 응답을 수신해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-173">If you can connect, you should receive an InvalidQueryParameterValue or similar XML response.</span></span>

- <span data-ttu-id="68297-174">다른 사용자가 Storage 탐색기와 프록시 서버를 함께 사용하고 있는 경우 연결할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-174">If someone else is also using Storage Explorer with your proxy server, verify that they can connect.</span></span> <span data-ttu-id="68297-175">연결할 수 있다면 프록시 서버 관리자에게 문의해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68297-175">If they can connect, you may have to contact your proxy server admin.</span></span>

### <a name="tools-for-diagnosing-issues"></a><span data-ttu-id="68297-176">문제를 진단하기 위한 도구</span><span class="sxs-lookup"><span data-stu-id="68297-176">Tools for diagnosing issues</span></span>

<span data-ttu-id="68297-177">Windows용 Fiddler와 같은 네트워킹 도구가 있으면 다음과 같은 문제를 진단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68297-177">If you have networking tools, such as Fiddler for Windows, you may be able to diagnose the problems as follows:</span></span>

- <span data-ttu-id="68297-178">프록시를 통해 작업해야 하는 경우 프록시를 통해 연결하도록 네트워킹 도구를 구성해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68297-178">If you have to work through your proxy, you may have to configure your networking tool to connect through the proxy.</span></span>

- <span data-ttu-id="68297-179">네트워킹 도구에서 사용하는 포트 번호를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-179">Check the port number used by your networking tool.</span></span>

- <span data-ttu-id="68297-180">Storage 탐색기에 로컬 호스트 URL과 네트워킹 도구의 포트 번호를 프록시 설정으로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-180">Enter the local host URL and the networking tool's port number as proxy settings in Storage Explorer.</span></span> <span data-ttu-id="68297-181">올바르게 수행되면 네트워킹 도구가 Storage 탐색기에서 만든 네트워크 요청을 관리 및 서비스 끝점에 기록하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-181">If this is done correctly, your networking tool starts logging network requests made by Storage Explorer to management and service endpoints.</span></span> <span data-ttu-id="68297-182">예를 들어 브라우저에서 Blob 끝점에 대한 https://cawablobgrs.blob.core.windows.net/을 입력하면 다음과 유사한 응답이 수신됩니다. 이 응답을 통해 리소스에 액세스할 수는 없지만 리소스가 있음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68297-182">For example, enter https://cawablobgrs.blob.core.windows.net/ for your blob endpoint in a browser, and you will receive a response resembles the following, which suggests the resource exists, although you cannot access it.</span></span>

![코드 샘플](./media/storage-explorer-troubleshooting/4022502_en_2.png)

### <a name="contact-proxy-server-admin"></a><span data-ttu-id="68297-184">프록시 서버 관리자 문의</span><span class="sxs-lookup"><span data-stu-id="68297-184">Contact proxy server admin</span></span>

<span data-ttu-id="68297-185">프록시 설정이 올바른 경우 프록시 서버 관리자에게 문의해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68297-185">If your proxy settings are correct, you may have to contact your proxy server admin, and</span></span>

- <span data-ttu-id="68297-186">프록시가 Azure 관리 또는 리소스 끝점에 대한 트래픽을 차단하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-186">Make sure that your proxy does not block traffic to Azure management or resource endpoints.</span></span>

- <span data-ttu-id="68297-187">프록시 서버에서 사용하는 인증 프로토콜을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-187">Verify the authentication protocol used by your proxy server.</span></span> <span data-ttu-id="68297-188">Storage 탐색기는 현재 NTLM 프록시를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68297-188">Storage Explorer does not currently support NTLM proxies.</span></span>

## <a name="unable-to-retrieve-children-error-message"></a><span data-ttu-id="68297-189">"하위 항목을 검색할 수 없음" 오류 메시지</span><span class="sxs-lookup"><span data-stu-id="68297-189">"Unable to Retrieve Children" error message</span></span>

<span data-ttu-id="68297-190">프록시를 통해 Azure에 연결된 경우 프록시 설정이 올바른지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-190">If you are connected to Azure through a proxy, verify that your proxy settings are correct.</span></span> <span data-ttu-id="68297-191">구독 또는 계정 소유자로부터 리소스에 대한 액세스가 부여된 경우 해당 리소스에 대한 읽기 또는 목록 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-191">If you were granted access to a resource from the owner of the subscription or account, verify that you have read or list permissions for that resource.</span></span>

### <a name="issues-with-sas-url"></a><span data-ttu-id="68297-192">SAS URL 문제</span><span class="sxs-lookup"><span data-stu-id="68297-192">Issues with SAS URL</span></span>
<span data-ttu-id="68297-193">SAS URL을 사용하여 서비스에 연결하고 이 오류가 발생하는 경우:</span><span class="sxs-lookup"><span data-stu-id="68297-193">If you are connecting to a service using a SAS URL and experiencing this error:</span></span>

- <span data-ttu-id="68297-194">URL이 리소스를 읽거나 나열하는 데 필요한 권한을 제공하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-194">Verify that the URL provides the necessary permissions to read or list resources.</span></span>

- <span data-ttu-id="68297-195">URL이 만료되지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-195">Verify that the URL has not expired.</span></span>

- <span data-ttu-id="68297-196">SAS URL이 액세스 정책을 기반으로 하는 경우 액세스 정책이 철회되지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-196">If the SAS URL is based on an access policy, verify that the access policy has not been revoked.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68297-197">다음 단계</span><span class="sxs-lookup"><span data-stu-id="68297-197">Next steps</span></span>

<span data-ttu-id="68297-198">해결할 수 있는 솔루션이 없으면 당사에서 문제 해결을 위해 연락할 수 있도록 사용자 의견 도구를 통해 메일로 문제에 대한 자세한 내용을 최대한 포함하여 문제를 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-198">If none of the solutions work for you, submit your issue through the feedback tool with your email and as many details about the issue included as you can, so that we can contact you for fixing the issue.</span></span>

<span data-ttu-id="68297-199">이렇게 하려면 **도움말** 메뉴를 클릭한 다음 **피드백 보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68297-199">To do this, click **Help** menu, and then click **Send Feedback**.</span></span>

![사용자 의견](./media/storage-explorer-troubleshooting/4022503_en_1.png)
