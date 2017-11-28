---
title: "인증서 toohello Java CA 저장소 aaaAdd | Microsoft Docs"
description: "Tooadd 인증 기관 (CA) 인증서 toohello Java CA 인증서 (cacerts) 저장 되는 방식과 Twilio 서비스 또는 Azure 서비스 버스에 대해 알아봅니다."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: d3699b0a-835c-43fb-844d-9c25344e5cda
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 030e43129580023942dee662e72d2f443167f308
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-a-certificate-toohello-java-ca-certificates-store"></a><span data-ttu-id="f4efc-103">인증서 toohello Java CA 인증서 저장소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f4efc-103">Adding a Certificate toohello Java CA Certificates Store</span></span>
<span data-ttu-id="f4efc-104">단계를 수행 하는 hello 인증 기관 (CA) 인증서 toohello Java CA 인증서 (cacerts) 저장 하는 tooadd 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f4efc-104">hello following steps show you how tooadd a certificate authority (CA) certificate toohello Java CA certificate (cacerts) store.</span></span> <span data-ttu-id="f4efc-105">hello CA 인증서에 대 한 사용 되는 hello 예제는 hello Twilio 서비스에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4efc-105">hello example used is for hello CA certificate required by hello Twilio service.</span></span> <span data-ttu-id="f4efc-106">Hello 항목의 뒷부분에 제공 된 정보는 hello Azure 서비스 버스에 대 한 tooinstall hello CA 인증서 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4efc-106">Information provided later in hello topic describes how tooinstall hello CA certificate for hello Azure Service Bus.</span></span> 

<span data-ttu-id="f4efc-107">JDK 및 tooyour Azure 프로젝트의 추가 keytool tooadd hello CA 인증서 이전 toozipping를 사용할 수 있습니다 **approot** 폴더 또는 있습니다 keytool tooadd hello 인증서를 사용 하는 Azure 시작 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4efc-107">You can use keytool tooadd hello CA certificate prior toozipping your JDK and adding it tooyour Azure project's **approot** folder, or you could run an Azure start-up task that uses keytool tooadd hello certificate.</span></span> <span data-ttu-id="f4efc-108">이 CA 인증서 이전 toohello JDK 압축 되 고 추가한 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4efc-108">This example assumes you will add a CA certificate prior toohello JDK being zipped.</span></span> <span data-ttu-id="f4efc-109">또한 hello 있지만, 다른 CA 인증서를 받는 hello 단계에서 특정 CA 인증서를 사용할 고 hello cacerts로 가져온 저장소 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4efc-109">Also, a specific CA certificate will be used in hello example, but hello steps of obtaining a different CA certificate and importing it into hello cacerts store would be similar.</span></span>

## <a name="tooadd-a-certificate-toohello-cacerts-store"></a><span data-ttu-id="f4efc-110">tooadd 인증서 toohello cacerts 저장</span><span class="sxs-lookup"><span data-stu-id="f4efc-110">tooadd a certificate toohello cacerts store</span></span>
1. <span data-ttu-id="f4efc-111">Tooyour JDK 설정 된 명령 프롬프트에서 **jdk\jre\lib\security** hello toosee 설치 된 인증서를 다음를 실행 하는 폴더:</span><span class="sxs-lookup"><span data-stu-id="f4efc-111">At a command prompt that is set tooyour JDK's **jdk\jre\lib\security** folder, run hello following toosee what certificates are installed:</span></span>
   
    `keytool -list -keystore cacerts`
   
    <span data-ttu-id="f4efc-112">암호를 저장 하는 hello 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4efc-112">You'll be prompted for hello store password.</span></span> <span data-ttu-id="f4efc-113">hello 기본 암호는 **changeit**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4efc-113">hello default password is **changeit**.</span></span> <span data-ttu-id="f4efc-114">(Hello keytool 설명서를 참조 하려는 경우 toochange hello 암호, <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.) 이 예에서는 가정 된 MD5 지문 67:CB:9 D hello 인증서: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 나열 되지 않으면 고 tooimport it (hello Twilio API 서비스에서이 인증서 필요).</span><span class="sxs-lookup"><span data-stu-id="f4efc-114">(If you want toochange hello password, see hello keytool documentation at <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.) This example assumes that hello certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 is not listed, and that you want tooimport it (this particular certificate is needed by hello Twilio API service).</span></span>
2. <span data-ttu-id="f4efc-115">Hello에 나열 된 인증서 목록에서 hello 인증서를 얻은 [GeoTrust 루트 인증서](http://www.geotrust.com/resources/root-certificates/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f4efc-115">Obtain hello certificate from hello list of certificates listed at [GeoTrust Root Certificates](http://www.geotrust.com/resources/root-certificates/).</span></span> <span data-ttu-id="f4efc-116">일련 번호 35:DE:F4:CF과 hello 인증서 hello 링크를 마우스 오른쪽 단추로 클릭 하 고 toohello 저장 **jdk\jre\lib\security** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f4efc-116">Right-click hello link for hello certificate with serial number 35:DE:F4:CF and save it toohello **jdk\jre\lib\security** folder.</span></span> <span data-ttu-id="f4efc-117">이 예에서는 라는 tooa 파일으로 저장 된 **Equifax\_Secure\_인증서\_Authority.cer**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4efc-117">For purposes of this example, it was saved tooa file named **Equifax\_Secure\_Certificate\_Authority.cer**.</span></span>
3. <span data-ttu-id="f4efc-118">다음 명령을 hello 통해 hello 인증서를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f4efc-118">Import hello certificate via hello following command:</span></span>
   
    `keytool -keystore cacerts -importcert -alias equifaxsecureca -file Equifax_Secure_Certificate_Authority.cer`
   
    <span data-ttu-id="f4efc-119">때 hello 인증서 MD5 지문을 67:CB:9 D에 있는 경우이 인증서를 tootrust 메시지가: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4를 입력 하 여 응답 **y**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4efc-119">When prompted tootrust this certificate, if hello certificate has MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4, respond by typing **y**.</span></span>
4. <span data-ttu-id="f4efc-120">명령 tooensure hello CA 인증서를 다음 실행된 hello가 성공적으로 가져왔는지 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f4efc-120">Run hello following command tooensure hello CA certificate has been successfully imported:</span></span>
   
    `keytool -list -keystore cacerts`
5. <span data-ttu-id="f4efc-121">Tooyour Azure 프로젝트의 추가 하 고 압축 하는 hello JDK **approot** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f4efc-121">Zip hello JDK and add it tooyour Azure project's **approot** folder.</span></span>

<span data-ttu-id="f4efc-122">keytool에 대한 자세한 내용은 <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4efc-122">For information about keytool, see <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span></span>

## <a name="azure-root-certificates"></a><span data-ttu-id="f4efc-123">Azure 루트 인증서</span><span class="sxs-lookup"><span data-stu-id="f4efc-123">Azure Root Certificates</span></span>
<span data-ttu-id="f4efc-124">Azure 서비스 (예: Azure 서비스 버스)를 사용 하는 응용 프로그램 tootrust hello Baltimore CyberTrust 루트 인증서를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4efc-124">Your applications that use Azure services (such as Azure Service Bus) need tootrust hello Baltimore CyberTrust Root certificate.</span></span> <span data-ttu-id="f4efc-125">(2013 년 4 월 15 일을 시작 하 고 Azure 시작 된 hello GTE CyberTrust 전역 루트 toohello Baltimore CyberTrust 루트에서에서 마이그레이션입니다.</span><span class="sxs-lookup"><span data-stu-id="f4efc-125">(Beginning April 15, 2013, Azure began migrating from hello GTE CyberTrust Global Root toohello Baltimore CyberTrust Root.</span></span> <span data-ttu-id="f4efc-126">이 마이그레이션 걸린 몇 개월 toocomplete입니다.)</span><span class="sxs-lookup"><span data-stu-id="f4efc-126">This migration took several months toocomplete.)</span></span>

<span data-ttu-id="f4efc-127">hello 인증서 cacerts 저장소에 이미 설치 될 수 있습니다 Baltimore 따라서 프로그램인 toorun hello **keytool-목록** 이미 존재 하는 경우 첫 번째 toosee 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="f4efc-127">hello Baltimore certificate might already be installed in your cacerts store, so remember toorun hello **keytool -list** command first toosee if it already exists.</span></span>

<span data-ttu-id="f4efc-128">Baltimore CyberTrust 루트 hello tooadd 해야 할 경우, 일련 번호 02:00:00:b9 있으며 SHA1 지문 d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2 c: 78:db:28:52:ca:e4:74 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4efc-128">If you need tooadd hello Baltimore CyberTrust Root, it has serial number 02:00:00:b9 and SHA1 fingerprint d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74.</span></span> <span data-ttu-id="f4efc-129">다운로드할 수 있습니다 <https://cacert.omniroot.com/bc2025.crt>, tooa 로컬 파일 확장명으로 저장 **.cer**를 사용 하 여 **keytool** 위와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4efc-129">It can be downloaded from <https://cacert.omniroot.com/bc2025.crt>, saved tooa local file with extension **.cer**, and then imported using **keytool** as shown above.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4efc-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f4efc-130">Next steps</span></span>
<span data-ttu-id="f4efc-131">Azure에서 사용 하는 hello 루트 인증서에 대 한 자세한 내용은 참조 [Azure 루트 인증서 마이그레이션](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="f4efc-131">For more information about hello root certificates used by Azure, see [Azure Root Certificate Migration](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx).</span></span>

<span data-ttu-id="f4efc-132">Java에 대한 자세한 내용은 [Java 개발자용 Azure](/java/azure)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4efc-132">For more information about Java, see [Azure for Java developers](/java/azure).</span></span>

