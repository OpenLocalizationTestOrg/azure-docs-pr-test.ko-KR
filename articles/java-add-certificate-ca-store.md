---
title: "Java CA 저장소에 인증서 추가 | Microsoft 문서"
description: "Java CA(인증 기관) 인증서(cacerts) 저장소에 Twilio 서비스 또는 Azure 서비스 버스용 CA 인증서를 추가하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 4f3ec837588c6e959e82108ca25ab4289e40d3f5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="adding-a-certificate-to-the-java-ca-certificates-store"></a><span data-ttu-id="710a3-103">Java CA 인증서 저장소에 인증서 추가</span><span class="sxs-lookup"><span data-stu-id="710a3-103">Adding a Certificate to the Java CA Certificates Store</span></span>
<span data-ttu-id="710a3-104">다음 단계는 Java CA 인증서(cacerts) 저장소에 CA(인증 기관) 인증서를 추가하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="710a3-104">The following steps show you how to add a certificate authority (CA) certificate to the Java CA certificate (cacerts) store.</span></span> <span data-ttu-id="710a3-105">사용된 예제는 Twilio 서비스에 필요한 CA 인증서용입니다.</span><span class="sxs-lookup"><span data-stu-id="710a3-105">The example used is for the CA certificate required by the Twilio service.</span></span> <span data-ttu-id="710a3-106">항목의 뒷부분에 제공된 정보는 Azure 서비스 버스용 CA 인증서를 설치하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="710a3-106">Information provided later in the topic describes how to install the CA certificate for the Azure Service Bus.</span></span> 

<span data-ttu-id="710a3-107">JDK를 압축하고 Azure 프로젝트의 **approot** 폴더에 추가하기 전에 keytool을 사용하여 CA 인증서를 추가하거나 keytool을 사용하여 인증서를 추가하는 Azure 시작 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="710a3-107">You can use keytool to add the CA certificate prior to zipping your JDK and adding it to your Azure project's **approot** folder, or you could run an Azure start-up task that uses keytool to add the certificate.</span></span> <span data-ttu-id="710a3-108">이 예제에서는 JDK를 압축하기 전에 CA 인증서를 추가한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="710a3-108">This example assumes you will add a CA certificate prior to the JDK being zipped.</span></span> <span data-ttu-id="710a3-109">또한 예제에서는 특정 CA 인증서가 사용되지만 다른 CA 인증서를 얻고 cacerts 저장소로 가져오는 단계도 이와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="710a3-109">Also, a specific CA certificate will be used in the example, but the steps of obtaining a different CA certificate and importing it into the cacerts store would be similar.</span></span>

## <a name="to-add-a-certificate-to-the-cacerts-store"></a><span data-ttu-id="710a3-110">cacerts 저장소에 인증서를 추가하려면</span><span class="sxs-lookup"><span data-stu-id="710a3-110">To add a certificate to the cacerts store</span></span>
1. <span data-ttu-id="710a3-111">JDK의 **jdk\jre\lib\security** 폴더로 설정된 명령 프롬프트에서 다음을 실행하여 설치된 인증서를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="710a3-111">At a command prompt that is set to your JDK's **jdk\jre\lib\security** folder, run the following to see what certificates are installed:</span></span>
   
    `keytool -list -keystore cacerts`
   
    <span data-ttu-id="710a3-112">저장소 암호를 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="710a3-112">You'll be prompted for the store password.</span></span> <span data-ttu-id="710a3-113">기본 암호는 **changeit**입니다.</span><span class="sxs-lookup"><span data-stu-id="710a3-113">The default password is **changeit**.</span></span> <span data-ttu-id="710a3-114">암호를 변경하려면 <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>에 있는 keytool 설명서를 참조하세요. 이 예제에서는 MD5 지문 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4가 포함된 인증서가 나열되지 않아서 해당 인증서를 가져오려 한다고 가정합니다(이 특정 인증서는 Twilio API 서비스에 필요함).</span><span class="sxs-lookup"><span data-stu-id="710a3-114">(If you want to change the password, see the keytool documentation at <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.) This example assumes that the certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 is not listed, and that you want to import it (this particular certificate is needed by the Twilio API service).</span></span>
2. <span data-ttu-id="710a3-115">[GeoTrust 루트 인증서](http://www.geotrust.com/resources/root-certificates/)(영문)에 나열된 인증서 목록에서 인증서를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="710a3-115">Obtain the certificate from the list of certificates listed at [GeoTrust Root Certificates](http://www.geotrust.com/resources/root-certificates/).</span></span> <span data-ttu-id="710a3-116">일련 번호가 35:DE:F4:CF인 인증서의 링크를 마우스 오른쪽 단추로 클릭하고 **jdk\jre\lib\security** 폴더에 해당 인증서를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="710a3-116">Right-click the link for the certificate with serial number 35:DE:F4:CF and save it to the **jdk\jre\lib\security** folder.</span></span> <span data-ttu-id="710a3-117">이 예제에서는 인증서가 **Equifax\_Secure\_Certificate\_Authority.cer**이라는 파일에 저장되었습니다.</span><span class="sxs-lookup"><span data-stu-id="710a3-117">For purposes of this example, it was saved to a file named **Equifax\_Secure\_Certificate\_Authority.cer**.</span></span>
3. <span data-ttu-id="710a3-118">다음 명령을 통해 인증서를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="710a3-118">Import the certificate via the following command:</span></span>
   
    `keytool -keystore cacerts -importcert -alias equifaxsecureca -file Equifax_Secure_Certificate_Authority.cer`
   
    <span data-ttu-id="710a3-119">이 인증서를 신뢰하라는 메시지가 표시될 경우 인증서에 MD5 지문 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4가 포함되어 있으면 **y**를 입력하여 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="710a3-119">When prompted to trust this certificate, if the certificate has MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4, respond by typing **y**.</span></span>
4. <span data-ttu-id="710a3-120">다음 명령을 실행하여 CA 인증서를 가져왔는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="710a3-120">Run the following command to ensure the CA certificate has been successfully imported:</span></span>
   
    `keytool -list -keystore cacerts`
5. <span data-ttu-id="710a3-121">JDK를 압축하고 Azure 프로젝트의 **approot** 폴더에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="710a3-121">Zip the JDK and add it to your Azure project's **approot** folder.</span></span>

<span data-ttu-id="710a3-122">keytool에 대한 자세한 내용은 <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="710a3-122">For information about keytool, see <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span></span>

## <a name="azure-root-certificates"></a><span data-ttu-id="710a3-123">Azure 루트 인증서</span><span class="sxs-lookup"><span data-stu-id="710a3-123">Azure Root Certificates</span></span>
<span data-ttu-id="710a3-124">Azure 서비스(예: Azure 서비스 버스)를 사용하는 응용 프로그램은 Baltimore CyberTrust Root 인증서를 신뢰해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="710a3-124">Your applications that use Azure services (such as Azure Service Bus) need to trust the Baltimore CyberTrust Root certificate.</span></span> <span data-ttu-id="710a3-125">2013년 4월 15일부터 Azure는 GTE CyberTrust Global Root에서 Baltimore CyberTrust Root로 마이그레이션을 시작했습니다.</span><span class="sxs-lookup"><span data-stu-id="710a3-125">(Beginning April 15, 2013, Azure began migrating from the GTE CyberTrust Global Root to the Baltimore CyberTrust Root.</span></span> <span data-ttu-id="710a3-126">이 마이그레이션을 완료하는 데 몇 달이 걸렸습니다.</span><span class="sxs-lookup"><span data-stu-id="710a3-126">This migration took several months to complete.)</span></span>

<span data-ttu-id="710a3-127">Baltimore 인증서가 cacerts 저장소에 이미 설치되어 있을 수도 있으므로 먼저 **keytool -list** 명령을 실행하여 인증서가 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="710a3-127">The Baltimore certificate might already be installed in your cacerts store, so remember to run the **keytool -list** command first to see if it already exists.</span></span>

<span data-ttu-id="710a3-128">Baltimore CyberTrust Root를 추가해야 하는 경우 일련 번호 02:00:00:b9 및 SHA1 지문 d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="710a3-128">If you need to add the Baltimore CyberTrust Root, it has serial number 02:00:00:b9 and SHA1 fingerprint d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74.</span></span> <span data-ttu-id="710a3-129"><https://cacert.omniroot.com/bc2025.crt>에서 다운로드하고 확장명이 **.cer**인 로컬 파일에 저장한 다음 위와 같이 **keytool**을 사용하여 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="710a3-129">It can be downloaded from <https://cacert.omniroot.com/bc2025.crt>, saved to a local file with extension **.cer**, and then imported using **keytool** as shown above.</span></span>

## <a name="next-steps"></a><span data-ttu-id="710a3-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="710a3-130">Next steps</span></span>
<span data-ttu-id="710a3-131">Azure에서 사용되는 루트 인증서에 대한 자세한 내용은 [Azure 루트 인증서 마이그레이션](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="710a3-131">For more information about the root certificates used by Azure, see [Azure Root Certificate Migration](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx).</span></span>

<span data-ttu-id="710a3-132">Java에 대한 자세한 내용은 [Java 개발자용 Azure](/java/azure)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="710a3-132">For more information about Java, see [Azure for Java developers](/java/azure).</span></span>

