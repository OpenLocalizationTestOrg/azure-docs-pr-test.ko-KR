---
title: "aaaAzure 저장소 탐색기 문제 해결 가이드 | Microsoft Docs"
description: "Azure의 hello 두 디버깅 기능 개요"
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
ms.date: 05/18/2017
ms.author: delhan
ms.openlocfilehash: 5152f70418707d65c0a4bce9a916336829956219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-explorer-troubleshooting-guide"></a><span data-ttu-id="b21d2-103">Azure Storage 탐색기 문제 해결 가이드</span><span class="sxs-lookup"><span data-stu-id="b21d2-103">Azure Storage Explorer troubleshooting guide</span></span>

## <a name="introduction"></a><span data-ttu-id="b21d2-104">소개</span><span class="sxs-lookup"><span data-stu-id="b21d2-104">Introduction</span></span>

<span data-ttu-id="b21d2-105">Microsoft Azure 저장소 탐색기 (미리 보기)는 Windows, macOS 및 Linux에서 데이터를 Azure 저장소 사용 tooeasily 작업 수 있는 독립 실행형 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-105">Microsoft Azure Storage Explorer (Preview) is a stand-alone app that enables you tooeasily work with Azure Storage data on Windows, macOS and Linux.</span></span> <span data-ttu-id="b21d2-106">hello 앱 Azure, Sovereign 클라우드 및 Azure 스택에서 호스팅되는 toStorage 계정을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-106">hello app can connect toStorage accounts hosted on Azure, Sovereign Clouds, and Azure Stack.</span></span>

<span data-ttu-id="b21d2-107">이 가이드에는 Storage 탐색기에 나타나는 일반적인 문제에 대한 솔루션이 요약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-107">This guide summarizes solutions for common issues seen in Storage Explorer.</span></span>

## <a name="sign-in-issues"></a><span data-ttu-id="b21d2-108">로그인 문제</span><span class="sxs-lookup"><span data-stu-id="b21d2-108">Sign in issues</span></span>

<span data-ttu-id="b21d2-109">계속 하기 전에 응용 프로그램을 다시 시도 하 고 hello 문제를 해결할 수 있는지 여부를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b21d2-109">Before you continue, try restarting your application and see whether hello problems can be fixed.</span></span>

### <a name="error-self-signed-certificate-in-certificate-chain"></a><span data-ttu-id="b21d2-110">오류: 인증서 체인의 자체 서명된 인증서</span><span class="sxs-lookup"><span data-stu-id="b21d2-110">Error: Self-Signed Certificate in Certificate Chain</span></span>

<span data-ttu-id="b21d2-111">여러 가지 이유로 발생할 수 있습니다이 오류 이유와 hello 가장 일반적인 두 가지 이유는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-111">There are several reasons why you may encounter this error, and hello most common two reasons are as follows:</span></span>

1. <span data-ttu-id="b21d2-112">hello 앱 "투명 프록시"를 통해 서버 (예: 회사 서버)의 HTTPS 트래픽을 차단, 암호 해독 고 자체 서명 된 인증서를 사용 하 여 암호화 한 다음 연결 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-112">hello app is connected through a “transparent proxy”, which means a server (such as your company server) is intercepting HTTPS traffic, decrypting it, and then encrypting it using a self-signed certificate.</span></span>

2. <span data-ttu-id="b21d2-113">바이러스 백신 소프트웨어를 삽입 하는 자체 서명 된 SSL 인증서를 수신 하는 hello HTTPS 메시지로 같은 응용 프로그램을 실행 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-113">You are running an application, such as antivirus software, which is injecting a self-signed SSL certificate into hello HTTPS messages that you receive.</span></span>

<span data-ttu-id="b21d2-114">저장소 탐색기 hello 문제를 발견 하면 수신 hello HTTPS 메시지는 변조 여부를 알고 더 이상 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-114">When Storage Explorer encounters one of hello issues, it can no longer know whether hello received HTTPS message is tampered.</span></span> <span data-ttu-id="b21d2-115">Hello 자체 서명 된 인증서의 복사본을 사용 하는 경우 저장소 탐색기를 신뢰 하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-115">If you have a copy of hello self-signed certificate, you can let Storage Explorer trust it.</span></span> <span data-ttu-id="b21d2-116">hello 인증서 삽입 하 게 잘 모를 경우 이러한 단계 toofind를 수행 하기:</span><span class="sxs-lookup"><span data-stu-id="b21d2-116">If you are unsure of who is injecting hello certificate, follow these steps toofind it:</span></span>

1. <span data-ttu-id="b21d2-117">OpenSSL을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-117">Install Open SSL</span></span>

    - <span data-ttu-id="b21d2-118">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (hello 밝은 버전 중 하나 여야 함 충분)</span><span class="sxs-lookup"><span data-stu-id="b21d2-118">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (any of hello light versions should be sufficient)</span></span>

    - <span data-ttu-id="b21d2-119">Mac 및 Linux: 운영 체제에 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-119">Mac and Linux: should be included with your operating system</span></span>

2. <span data-ttu-id="b21d2-120">OpenSSL을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-120">Run Open SSL</span></span>

    - <span data-ttu-id="b21d2-121">Windows: hello 설치 디렉터리를 열고, 클릭 **/bin/**, 두 번 클릭 하 고 **openssl.exe**합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-121">Windows: open hello installation directory, click **/bin/**, and then double-click **openssl.exe**.</span></span>
    - <span data-ttu-id="b21d2-122">Mac 및 Linux: 터미널에서 **openssl**을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-122">Mac and Linux: run **openssl** from a terminal.</span></span>

3. <span data-ttu-id="b21d2-123">s_client -showcerts -connect microsoft.com :443을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-123">Execute s_client -showcerts -connect microsoft.com:443</span></span>

4. <span data-ttu-id="b21d2-124">자체 서명된 인증서를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-124">Look for self-signed certificates.</span></span> <span data-ttu-id="b21d2-125">자체 서명 된 확실 하지 않은 경우 아무 곳 이나 hello 제목 ("s:")를 찾고 발급자 ("i:")는 동일 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-125">If you are unsure which are self-signed, look for anywhere hello subject ("s:") and issuer ("i:") are hello same.</span></span>

5. <span data-ttu-id="b21d2-126">자체 서명 된 인증서를 찾은 면 각 하나에 대 한 복사 하 여 포함 하 여에서 모든 항목을 붙여 **---BEGIN 인증서---** 너무**---END 인증서---** tooa 새.cer 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-126">When you have found any self-signed certificates, for each one, copy and paste everything from and including **-----BEGIN CERTIFICATE-----** too**-----END CERTIFICATE-----** tooa new .cer file.</span></span>

6. <span data-ttu-id="b21d2-127">저장소 탐색기를 열고 **편집** > **SSL 인증서** > **가져오기 인증서**, 한 다음 사용 하 여 hello 파일 선택기 toofind, select, 만든 hello.cer 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-127">Open Storage Explorer, click **Edit** > **SSL Certificates** > **Import Certificates**, and then use hello file picker toofind, select, and open hello .cer files that you created.</span></span>

<span data-ttu-id="b21d2-128">단계는 hello를 사용 하 여 자체 서명 된 인증서를 찾을 수 없는 경우 hello 피드백 도구에 대 한 자세한 도움말을 통해 문의.</span><span class="sxs-lookup"><span data-stu-id="b21d2-128">If you cannot find any self-signed certificates using hello above steps, contact us through hello feedback tool for more help.</span></span>

### <a name="unable-tooretrieve-subscriptions"></a><span data-ttu-id="b21d2-129">없습니다 tooretrieve 구독</span><span class="sxs-lookup"><span data-stu-id="b21d2-129">Unable tooretrieve subscriptions</span></span>

<span data-ttu-id="b21d2-130">구독 한 후에 성공적으로 로그인 하는 없습니다 tooretrieve 인 경우 이러한 단계 tootroubleshoot이이 문제를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-130">If you are unable tooretrieve your subscriptions after you successfully sign in, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="b21d2-131">Hello Azure 포털에 로그인 하 여 사용자 계정 액세스 toohello 구독에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-131">Verify that your account has access toohello subscriptions by signing into hello Azure Portal.</span></span>

- <span data-ttu-id="b21d2-132">Hello 올바른 환경 (Azure, Azure 중국, 독일 Azure, Azure 미국 정부 또는 사용자 정의 환경/Azure 스택)를 사용 하 여 로그인 한 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-132">Make sure that you have signed in using hello correct environment (Azure, Azure China, Azure Germany, Azure US Government, or Custom Environment/Azure Stack).</span></span>

- <span data-ttu-id="b21d2-133">프록시 뒤에 있다면 hello 저장소 탐색기 프록시를 제대로 구성 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-133">If you are behind a proxy, make sure that you have configured hello Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="b21d2-134">제거 하 고 다시 추가 중 hello 계정 사용을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-134">Try removing and readding hello account.</span></span>

- <span data-ttu-id="b21d2-135">파일 루트 디렉터리 (즉, C:\Users\ContosoUser)에서 고 hello 계정을 다시 추가 hello를 삭제 해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="b21d2-135">Try deleting hello following files from your root directory (that is, C:\Users\ContosoUser), and then re-adding hello account:</span></span>

    - <span data-ttu-id="b21d2-136">.adalcache</span><span class="sxs-lookup"><span data-stu-id="b21d2-136">.adalcache</span></span>

    - <span data-ttu-id="b21d2-137">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="b21d2-137">.devaccounts</span></span>

    - <span data-ttu-id="b21d2-138">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="b21d2-138">.extaccounts</span></span>

- <span data-ttu-id="b21d2-139">조사식 hello 개발자 도구 콘솔 (f 12를 눌러) 경우 로그인 하는 모든 오류 메시지:</span><span class="sxs-lookup"><span data-stu-id="b21d2-139">Watch hello developer tools console (by pressing F12) when you are signing in for any error messages:</span></span>

![개발자 도구](./media/storage-explorer-troubleshooting/4022501_en_2.png)

### <a name="unable-toosee-hello-authentication-page"></a><span data-ttu-id="b21d2-141">없습니다 toosee hello 인증 페이지</span><span class="sxs-lookup"><span data-stu-id="b21d2-141">Unable toosee hello authentication page</span></span>

<span data-ttu-id="b21d2-142">없습니다 toosee hello 인증 페이지 인 경우 이러한 단계 tootroubleshoot이이 문제를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-142">If you are unable toosee hello authentication page, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="b21d2-143">연결의 hello 속도 따라 hello 로그인 페이지 tooload 시간이 오래 걸릴 수 있습니다, 그리고 hello 인증 대화 상자를 닫기 전에 적어도 1 분까지 기다려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-143">Depending on hello speed of your connection, it may take a while for hello sign-in page tooload, wait at least one minute before closing hello authentication dialog box.</span></span>

- <span data-ttu-id="b21d2-144">프록시 뒤에 있다면 hello 저장소 탐색기 프록시를 제대로 구성 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-144">If you are behind a proxy, make sure that you have configured hello Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="b21d2-145">Hello F12 키를 눌러 보기 hello 개발자 콘솔.</span><span class="sxs-lookup"><span data-stu-id="b21d2-145">View hello developer console by pressing hello F12 key.</span></span> <span data-ttu-id="b21d2-146">Hello 응답 hello 개발자 콘솔에서 감시 하 고 이유에 대 한 모든 단서를 찾을 수 있는지 여부를 참조 하십시오. 인증 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-146">Watch hello responses from hello developer console and see whether you can find any clue for why authentication not working.</span></span>

### <a name="cannot-remove-account"></a><span data-ttu-id="b21d2-147">계정을 제거할 수 없음</span><span class="sxs-lookup"><span data-stu-id="b21d2-147">Cannot remove account</span></span>

<span data-ttu-id="b21d2-148">계정이 없습니다 tooremove 없거나 hello 다시 인증 링크 아무 작업도 수행 하지 않는 경우 이러한 단계 tootroubleshoot이이 문제를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="b21d2-148">If you are unable tooremove an account, or if hello reauthenticate link does not do anything, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="b21d2-149">루트 디렉터리에서 파일을 따르고 다음 hello 계정에 다시 추가 중 hello를 삭제 해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="b21d2-149">Try deleting hello following files from your root directory, and then readding hello account:</span></span>

    - <span data-ttu-id="b21d2-150">.adalcache</span><span class="sxs-lookup"><span data-stu-id="b21d2-150">.adalcache</span></span>

    - <span data-ttu-id="b21d2-151">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="b21d2-151">.devaccounts</span></span>

    - <span data-ttu-id="b21d2-152">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="b21d2-152">.extaccounts</span></span>

- <span data-ttu-id="b21d2-153">Tooremove SAS 저장소 리소스를 연결 하려면 다음 파일이 hello를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-153">If you want tooremove SAS attached Storage resources, delete hello following files:</span></span>

    - <span data-ttu-id="b21d2-154">Windows - %AppData%/StorageExplorer 폴더</span><span class="sxs-lookup"><span data-stu-id="b21d2-154">%AppData%/StorageExplorer folder for Windows</span></span>

    - <span data-ttu-id="b21d2-155">Mac - Users/<your_name>/Library/Applicaiton SUpport/StorageExplorer</span><span class="sxs-lookup"><span data-stu-id="b21d2-155">/Users/<your_name>/Library/Applicaiton SUpport/StorageExplorer for Mac</span></span>

    - <span data-ttu-id="b21d2-156">Linux - ~/.config/StorageExplorer</span><span class="sxs-lookup"><span data-stu-id="b21d2-156">~/.config/StorageExplorer for Linux</span></span>

> [!NOTE]
>  <span data-ttu-id="b21d2-157">나면 tooreenter 자격 증명 이러한 파일을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-157">You will have tooreenter all your credentials if you delete these files.</span></span>

## <a name="proxy-issues"></a><span data-ttu-id="b21d2-158">프록시 문제</span><span class="sxs-lookup"><span data-stu-id="b21d2-158">Proxy issues</span></span>

<span data-ttu-id="b21d2-159">먼저, 정보를 입력 한 다음 해당 hello 모두 정확한 지 확인:</span><span class="sxs-lookup"><span data-stu-id="b21d2-159">First, make sure that hello following information you entered are all correct:</span></span>

- <span data-ttu-id="b21d2-160">hello 프록시 URL과 포트 번호</span><span class="sxs-lookup"><span data-stu-id="b21d2-160">hello proxy URL and port number</span></span>

- <span data-ttu-id="b21d2-161">사용자 이름 및 암호 hello 프록시에 필요한 경우</span><span class="sxs-lookup"><span data-stu-id="b21d2-161">Username and password if required by hello proxy</span></span>

### <a name="common-solutions"></a><span data-ttu-id="b21d2-162">일반적인 솔루션</span><span class="sxs-lookup"><span data-stu-id="b21d2-162">Common solutions</span></span>

<span data-ttu-id="b21d2-163">문제가 여전히 발생 하는 경우에 따라 이러한 단계 tootroubleshoot 해당:</span><span class="sxs-lookup"><span data-stu-id="b21d2-163">If you are still experiencing issues, follow these steps tootroubleshoot them:</span></span>

- <span data-ttu-id="b21d2-164">프록시를 사용 하지 않고 toohello 인터넷에 연결할 수 있는, 경우에 저장소 탐색기 프록시 설정을 사용 하도록 설정 하지 않고 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-164">If you can connect toohello Internet without using your proxy, verify that Storage Explorer works without proxy settings enabled.</span></span> <span data-ttu-id="b21d2-165">상황에 hello 프록시 설정에 문제가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-165">If this is hello case, there may be an issue with your proxy settings.</span></span> <span data-ttu-id="b21d2-166">프록시 관리자 tooidentify hello 문제를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-166">Work with your proxy administrator tooidentify hello problems.</span></span>

- <span data-ttu-id="b21d2-167">다른 응용 프로그램 프록시 서버 hello를 사용 하 여 예상 대로 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-167">Verify that other applications using hello proxy server work as expected.</span></span>

- <span data-ttu-id="b21d2-168">웹 브라우저를 사용 하 여 toohello Microsoft Azure 포털에 연결할 수 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b21d2-168">Verify that you can connect toohello Microsoft Azure portal using your web browser</span></span>

- <span data-ttu-id="b21d2-169">서비스 끝점에서 응답을 수신할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-169">Verify that you can receive responses from your service endpoints.</span></span> <span data-ttu-id="b21d2-170">끝점 URL 중 하나를 브라우저에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-170">Enter one of your endpoint URLs into your browser.</span></span> <span data-ttu-id="b21d2-171">연결할 수 있으면 InvalidQueryParameterValue 또는 유사한 XML 응답을 수신해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-171">If you can connect, you should receive an InvalidQueryParameterValue or similar XML response.</span></span>

- <span data-ttu-id="b21d2-172">다른 사용자가 Storage 탐색기와 프록시 서버를 함께 사용하고 있는 경우 연결할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-172">If someone else is also using Storage Explorer with your proxy server, verify that they can connect.</span></span> <span data-ttu-id="b21d2-173">연결할 수 있는 경우 toocontact 프록시 서버 관리자</span><span class="sxs-lookup"><span data-stu-id="b21d2-173">If they can connect, you may have toocontact your proxy server admin.</span></span>

### <a name="tools-for-diagnosing-issues"></a><span data-ttu-id="b21d2-174">문제를 진단하기 위한 도구</span><span class="sxs-lookup"><span data-stu-id="b21d2-174">Tools for diagnosing issues</span></span>

<span data-ttu-id="b21d2-175">Windows 용 Fiddler와 같은 네트워킹 도구 경우 다음과 같이 수 toodiagnose hello 문제 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-175">If you have networking tools, such as Fiddler for Windows, you may be able toodiagnose hello problems as follows:</span></span>

- <span data-ttu-id="b21d2-176">프록시를 통해 toowork를 설정한 경우 hello 프록시를 통해 네트워킹 도구 tooconnect 프로그램 tooconfigure를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-176">If you have toowork through your proxy, you may have tooconfigure your networking tool tooconnect through hello proxy.</span></span>

- <span data-ttu-id="b21d2-177">네트워킹 도구에서 사용 하는 hello 포트 번호를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-177">Check hello port number used by your networking tool.</span></span>

- <span data-ttu-id="b21d2-178">저장소 탐색기의 프록시 설정으로 도구의 포트 번호를 네트워킹 hello와 hello 로컬 호스트 URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-178">Enter hello local host URL and hello networking tool's port number as proxy settings in Storage Explorer.</span></span> <span data-ttu-id="b21d2-179">이 isdone 올바르게 네트워킹 도구 시작 저장소 탐색기 toomanagement 및 서비스 끝점에서 만든 네트워크 요청을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-179">If this isdone correctly, your networking tool starts logging network requests made by Storage Explorer toomanagement and service endpoints.</span></span> <span data-ttu-id="b21d2-180">예를 들어 브라우저에서 blob 끝점 https://cawablobgrs.blob.core.windows.net/를 입력 하 고 응답을 받습니다. 액세스할 수 있지만 hello 리소스가 존재를 제안 하는 hello 다음 예제와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-180">For example, enter https://cawablobgrs.blob.core.windows.net/ for your blob endpoint in a browser, and you will receive a response resembles hello following, which suggests hello resource exists, although you cannot access it.</span></span>

![코드 샘플](./media/storage-explorer-troubleshooting/4022502_en_2.png)

### <a name="contact-proxy-server-admin"></a><span data-ttu-id="b21d2-182">프록시 서버 관리자 문의</span><span class="sxs-lookup"><span data-stu-id="b21d2-182">Contact proxy server admin</span></span>

<span data-ttu-id="b21d2-183">프록시 설정이 올바른지, 해야 toocontact 프록시 서버 관리자에 게 및</span><span class="sxs-lookup"><span data-stu-id="b21d2-183">If your proxy settings are correct, you may have toocontact your proxy server admin, and</span></span>

- <span data-ttu-id="b21d2-184">프록시 트래픽 tooAzure 관리 또는 리소스 끝점을 차단 하지 않습니다 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-184">Make sure that your proxy does not block traffic tooAzure management or resource endpoints.</span></span>

- <span data-ttu-id="b21d2-185">프록시 서버에서 사용 하는 hello 인증 프로토콜을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-185">Verify hello authentication protocol used by your proxy server.</span></span> <span data-ttu-id="b21d2-186">Storage 탐색기는 현재 NTLM 프록시를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-186">Storage Explorer does not currently support NTLM proxies.</span></span>

## <a name="unable-tooretrieve-children-error-message"></a><span data-ttu-id="b21d2-187">"없습니다 tooRetrieve 자식" 오류 메시지</span><span class="sxs-lookup"><span data-stu-id="b21d2-187">"Unable tooRetrieve Children" error message</span></span>

<span data-ttu-id="b21d2-188">프록시를 통해 연결 된 tooAzure 인 경우에 프록시 설정이 올바른지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-188">If you are connected tooAzure through a proxy, verify that your proxy settings are correct.</span></span> <span data-ttu-id="b21d2-189">Hello 구독이 나 계정을의 hello 소유자 로부터 tooa 리소스 액세스를 부여 된 경우 확인 읽기 하거나 해당 리소스에 대 한 사용 권한을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-189">If you were granted access tooa resource from hello owner of hello subscription or account, verify that you have read or list permissions for that resource.</span></span>

### <a name="issues-with-sas-url"></a><span data-ttu-id="b21d2-190">SAS URL 문제</span><span class="sxs-lookup"><span data-stu-id="b21d2-190">Issues with SAS URL</span></span>
<span data-ttu-id="b21d2-191">SAS URL을 사용 하 고이 오류를 발생 tooa 서비스 연결 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="b21d2-191">If you are connecting tooa service using a SAS URL and experiencing this error:</span></span>

- <span data-ttu-id="b21d2-192">Hello URL 제공 tooread 또는 목록 리소스 hello 필요한 권한이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-192">Verify that hello URL provides hello necessary permissions tooread or list resources.</span></span>

- <span data-ttu-id="b21d2-193">해당 hello URL 만료 되지 않았는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-193">Verify that hello URL has not expired.</span></span>

- <span data-ttu-id="b21d2-194">Hello SAS URL 액세스 정책에 따르면 hello 액세스 정책을 취소 되지 않았는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-194">If hello SAS URL is based on an access policy, verify that hello access policy has not been revoked.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b21d2-195">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b21d2-195">Next steps</span></span>

<span data-ttu-id="b21d2-196">Hello 솔루션 중, 적합 한 경우 전자 메일 hello 피드백 도구를 통해 문제를 제출 하 고 연락을 드릴 수 있습니다 hello 문제를 해결 하기 위한 있도록 있습니다으로 포함 하는 hello 문제에 대 한 자세한 정보 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-196">If none of hello solutions work for you, submit your issue through hello feedback tool with your email and as many details about hello issue included as you can, so that we can contact you for fixing hello issue.</span></span>

<span data-ttu-id="b21d2-197">toodo이를 클릭 하이 여 **도움말** 메뉴를 차례로 클릭 **사용자 의견 보내기**합니다.</span><span class="sxs-lookup"><span data-stu-id="b21d2-197">toodo this, click **Help** menu, and then click **Send Feedback**.</span></span>

![사용자 의견](./media/storage-explorer-troubleshooting/4022503_en_1.png)
