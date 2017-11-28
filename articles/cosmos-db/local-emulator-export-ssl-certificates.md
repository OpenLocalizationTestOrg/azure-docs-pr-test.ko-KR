---
title: "aaaExport hello Azure Cosmos DB 에뮬레이터 인증서 | Microsoft Docs"
description: "언어 및 런타임 hello Windows 인증서 저장소를 사용 하지 않는에서 개발할 때 필요한 tooexport 및 hello SSL 인증서를 관리 합니다. 이 게시물에서는 단계별 지침을 제공합니다."
services: cosmos-db
documentationcenter: 
keywords: "Azure Cosmos DB 에뮬레이터"
author: voellm
manager: jhubbard
editor: 
ms.assetid: ef43deda-c2e9-4193-99e2-7f6a88a0319f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: tvoellm
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: db56cda856fccf93d71ae5b21c4090ccb9aa40a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="export-hello-azure-cosmos-db-emulator-certificates-for-use-with-java-python-and-nodejs"></a><span data-ttu-id="83446-105">Java, Python 및 Node.js와 함께 사용할 hello Azure Cosmos DB 에뮬레이터 인증서 내보내기</span><span class="sxs-lookup"><span data-stu-id="83446-105">Export hello Azure Cosmos DB Emulator certificates for use with Java, Python, and Node.js</span></span>

[<span data-ttu-id="83446-106">**에뮬레이터의 hello 다운로드**</span><span class="sxs-lookup"><span data-stu-id="83446-106">**Download hello Emulator**</span></span>](https://aka.ms/cosmosdb-emulator)

<span data-ttu-id="83446-107">hello Azure Cosmos DB 에뮬레이터 hello Azure Cosmos DB 서비스를 SSL 연결 사용을 포함 하 여 개발 목적으로 에뮬레이트하는 로컬 환경을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="83446-107">hello Azure Cosmos DB Emulator provides a local environment that emulates hello Azure Cosmos DB service for development purposes including its use of SSL connections.</span></span> <span data-ttu-id="83446-108">이 게시물 언어 및 hello 자체를 사용 하 여 Java와 같은 Windows 인증서 저장소와 통합 되지 않는 런타임에서 사용 하기 위해 tooexport hello SSL 인증서 하는 방법을 보여 줍니다. [인증서 저장소](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) 및 를사용하여Python[래퍼 소켓](https://docs.python.org/2/library/ssl.html) 및 사용 하 여 Node.js [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback)합니다.</span><span class="sxs-lookup"><span data-stu-id="83446-108">This post demonstrates how tooexport hello SSL certificates for use in languages and runtimes that do not integrate with hello Windows Certificate Store such as Java which uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) and Python which uses [socket wrappers](https://docs.python.org/2/library/ssl.html) and Node.js which uses [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span></span> <span data-ttu-id="83446-109">자세한 내용은의 hello 에뮬레이터에 대 한 [개발 및 테스트에 사용 하 여 hello Azure Cosmos DB 에뮬레이터](./local-emulator.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="83446-109">You can read more about hello emulator in [Use hello Azure Cosmos DB Emulator for development and testing](./local-emulator.md).</span></span>

<span data-ttu-id="83446-110">이 자습서에서는 hello 다음 작업 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="83446-110">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="83446-111">인증서 순환</span><span class="sxs-lookup"><span data-stu-id="83446-111">Rotating certificates</span></span>
> * <span data-ttu-id="83446-112">SSL 인증서 내보내기</span><span class="sxs-lookup"><span data-stu-id="83446-112">Exporting SSL certificate</span></span>
> * <span data-ttu-id="83446-113">Toouse Java, Python 및 Node.js에 인증서를 hello 하는 방법 학습</span><span class="sxs-lookup"><span data-stu-id="83446-113">Learning how toouse hello certificate in Java, Python, and Node.js</span></span>

## <a name="certification-rotation"></a><span data-ttu-id="83446-114">인증 회전</span><span class="sxs-lookup"><span data-stu-id="83446-114">Certification rotation</span></span>

<span data-ttu-id="83446-115">Hello hello 에뮬레이터를 실행 하는 처음으로 생성 하는 Azure Cosmos DB 로컬 에뮬레이터는 hello에 있는 인증서.</span><span class="sxs-lookup"><span data-stu-id="83446-115">Certificates in hello Azure Cosmos DB Local Emulator are generated hello first time hello emulator is run.</span></span> <span data-ttu-id="83446-116">두 개의 인증서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83446-116">There are two certificates.</span></span> <span data-ttu-id="83446-117">Toohello 로컬 에뮬레이터와 hello 에뮬레이터 내에서 암호 관리에 대해 각각 하나씩 연결 하는 데 사용 되는 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="83446-117">One used for connecting toohello local emulator and one for managing secrets within hello emulator.</span></span> <span data-ttu-id="83446-118">tooexport hello 인증서는 hello 친숙 한 이름이 "DocumentDBEmulatorCertificate" hello 연결 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="83446-118">hello certificate you want tooexport is hello connection certificate with hello friendly name "DocumentDBEmulatorCertificate".</span></span>

<span data-ttu-id="83446-119">두 인증서를 클릭 하 여 다시 생성할 수 있습니다 **재설정 데이터** 트레이 Windows hello에서 실행 하는 Azure Cosmos DB 에뮬레이터에서 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="83446-119">Both certificates can be regenerated by clicking **Reset Data** as shown below from Azure Cosmos DB Emulator running in hello Windows Tray.</span></span> <span data-ttu-id="83446-120">Hello 인증서가 다시 생성 하 고 hello Java 인증서 저장소에 설치 했거나 다른 위치에서 사용 되는 경우 tooupdate 이러한 응용 프로그램 toohello 로컬 에뮬레이터는 더 이상 연결 하는 그렇지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="83446-120">If you regenerate hello certificates and have installed them into hello Java certificate store or used them elsewhere you will need tooupdate them, otherwise your application will no longer connect toohello local emulator.</span></span>

![Azure Cosmos DB 로컬 에뮬레이터 데이터 다시 설정](./media/local-emulator-export-ssl-certificates/database-local-emulator-reset-data.png)

## <a name="how-tooexport-hello-azure-cosmos-db-ssl-certificate"></a><span data-ttu-id="83446-122">어떻게 tooexport hello Azure Cosmos DB SSL 인증서</span><span class="sxs-lookup"><span data-stu-id="83446-122">How tooexport hello Azure Cosmos DB SSL certificate</span></span>

1. <span data-ttu-id="83446-123">Certlm.msc를 실행 하 여 hello Windows 인증서 관리자를 시작 하 고 탐색-> toohello 개인 인증서 폴더 및 hello 친숙 한 이름의 열기 hello 인증서 **DocumentDbEmulatorCertificate**합니다.</span><span class="sxs-lookup"><span data-stu-id="83446-123">Start hello Windows Certificate manager by running certlm.msc and navigate toohello Personal->Certificates folder and open hello certificate with hello friendly name **DocumentDbEmulatorCertificate**.</span></span>

    ![Azure Cosmos DB 로컬 에뮬레이터 내보내기 1단계](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-1.png)

2. <span data-ttu-id="83446-125">**세부 정보**를 클릭한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83446-125">Click on **Details** then **OK**.</span></span>

    ![Azure Cosmos DB 로컬 에뮬레이터 내보내기 2단계](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-2.png)

3. <span data-ttu-id="83446-127">클릭 **tooFile 복사...** .</span><span class="sxs-lookup"><span data-stu-id="83446-127">Click **Copy tooFile...**.</span></span>

    ![Azure Cosmos DB 로컬 에뮬레이터 내보내기 3단계](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-3.png)

4. <span data-ttu-id="83446-129">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="83446-129">Click **Next**.</span></span>

    ![Azure Cosmos DB 로컬 에뮬레이터 내보내기 4단계](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-4.png)

5. <span data-ttu-id="83446-131">**아니요, 개인 키를 내보내지 않습니다.**를 클릭한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83446-131">Click **No, do not export private key**, then click **Next**.</span></span>

    ![Azure Cosmos DB 로컬 에뮬레이터 내보내기 5단계](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-5.png)

6. <span data-ttu-id="83446-133">**Base-64 encoded X.509 (.CER)**를 클릭한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83446-133">Click on **Base-64 encoded X.509 (.CER)** and then **Next**.</span></span>

    ![Azure Cosmos DB 로컬 에뮬레이터 내보내기 6단계](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-6.png)

7. <span data-ttu-id="83446-135">Hello 인증서에 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="83446-135">Give hello certificate a name.</span></span> <span data-ttu-id="83446-136">여기서는 **documentdbemulatorcert**이며, **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83446-136">In this case **documentdbemulatorcert** and then click **Next**.</span></span>

    ![Azure Cosmos DB 로컬 에뮬레이터 내보내기 7단계](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-7.png)

8. <span data-ttu-id="83446-138">**Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83446-138">Click **Finish**.</span></span>

    ![Azure Cosmos DB 로컬 에뮬레이터 내보내기 8단계](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-8.png)

## <a name="how-toouse-hello-certificate-in-java"></a><span data-ttu-id="83446-140">Toouse java에서 인증서 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="83446-140">How toouse hello certificate in Java</span></span>

<span data-ttu-id="83446-141">전달 hello 보다 쉽게 tooinstall hello 인증서 hello Java 기본 인증서 저장소로 않은 경우가 많으므로 Java 응용 프로그램 또는 hello Java 클라이언트를 사용 하는 MongoDB 응용 프로그램을 실행 하는 경우 "-Djavax.net.ssl.trustStore=<keystore> - Djavax.net.ssl.trustStorePassword= "<password>" 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="83446-141">When running Java applications or MongoDB applications that use hello Java client it is easier tooinstall hello certificate into hello Java default certificate store than passing hello "-Djavax.net.ssl.trustStore=<keystore> -Djavax.net.ssl.trustStorePassword="<password>" flags.</span></span> <span data-ttu-id="83446-142">포함 하는 hello 예를 들어 [Java 데모 응용 프로그램](https://localhost:8081/_explorer/index.html) hello 기본 인증서 저장소에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="83446-142">For example hello included [Java Demo application](https://localhost:8081/_explorer/index.html) depends on hello default certificate store.</span></span>

<span data-ttu-id="83446-143">Hello에 hello 지침에 따라 [Java CA 인증서를 저장 하는 인증서 toohello 추가](https://docs.microsoft.com/azure/java-add-certificate-ca-store) hello 기본 Java 인증서 저장소로 tooimport hello X.509 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="83446-143">Follow hello instructions in hello [Adding a Certificate toohello Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store) tooimport hello X.509 certificate into hello default Java certificate store.</span></span> <span data-ttu-id="83446-144">있습니다 수 작업 하는 hello % JAVA_HOME % 디렉터리 keytool를 실행 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="83446-144">Keep in mind you will be working in hello %JAVA_HOME% directory when running keytool.</span></span>

<span data-ttu-id="83446-145">한 번 "CosmosDBEmulatorCertificate" SSL hello 인증서가 설치 된 응용 프로그램 수 tooconnect 속해 있어야 하며 사용 하 여 hello 로컬 Azure Cosmos DB 에뮬레이터입니다.</span><span class="sxs-lookup"><span data-stu-id="83446-145">Once hello "CosmosDBEmulatorCertificate" SSL certificate is installed your application should be able tooconnect and use hello local Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="83446-146">Toofollow hello 경우가 toohave 문제가 계속 되 면 [SSL/TLS 연결 디버깅](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) 문서.</span><span class="sxs-lookup"><span data-stu-id="83446-146">If you continue toohave trouble you may want toofollow hello [Debugging SSL/TLS Connections](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) article.</span></span> <span data-ttu-id="83446-147">매우 높습니다 hello 인증서가 hello %JAVA_HOME%/jre/lib/security/cacerts 저장소에 설치 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="83446-147">It is very likely hello certificate is not installed into hello %JAVA_HOME%/jre/lib/security/cacerts store.</span></span> <span data-ttu-id="83446-148">예를 들어 Java 응용 프로그램의 설치 된 버전을 여러 개 있는 경우 hello 업데이트 하나 보다 다른 cacerts 저장소 사용 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83446-148">For example if you have multiple installed versions of Java your application may be using a different cacerts store than hello one you updated.</span></span>

## <a name="how-toouse-hello-certificate-in-python"></a><span data-ttu-id="83446-149">Toouse는 Python에서 인증서를 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="83446-149">How toouse hello certificate in Python</span></span>

<span data-ttu-id="83446-150">기본 hello로 [Python SDK(version 2.0.0 or higher)](documentdb-sdk-python.md) hello에 대 한 DocumentDB API는 시도 없고 toohello 로컬 에뮬레이터를 연결할 때 hello SSL 인증서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="83446-150">By default hello [Python SDK(version 2.0.0 or higher)](documentdb-sdk-python.md) for hello DocumentDB API will not try and use hello SSL certificate when connecting toohello local emulator.</span></span> <span data-ttu-id="83446-151">Toouse SSL 유효성 검사를 원하는 뒤 hello에 hello 예제 [Python 소켓 래퍼](https://docs.python.org/2/library/ssl.html) 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="83446-151">If however you want toouse SSL validation you can follow hello examples in hello [Python socket wrappers](https://docs.python.org/2/library/ssl.html) documentation.</span></span>

## <a name="how-toouse-hello-certificate-in-nodejs"></a><span data-ttu-id="83446-152">Toouse는 Node.js에 인증서를 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="83446-152">How toouse hello certificate in Node.js</span></span>

<span data-ttu-id="83446-153">기본 hello로 [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) hello에 대 한 DocumentDB API는 시도 없고 toohello 로컬 에뮬레이터를 연결할 때 hello SSL 인증서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="83446-153">By default hello [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) for hello DocumentDB API will not try and use hello SSL certificate when connecting toohello local emulator.</span></span> <span data-ttu-id="83446-154">Toouse SSL 유효성 검사를 원하는 뒤 hello에 hello 예제 [Node.js 설명서](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback)합니다.</span><span class="sxs-lookup"><span data-stu-id="83446-154">If however you want toouse SSL validation you can follow hello examples in hello [Node.js documentation](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="83446-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="83446-155">Next steps</span></span>

<span data-ttu-id="83446-156">이 자습서에서는 hello 다음 작업을 수행 하면:</span><span class="sxs-lookup"><span data-stu-id="83446-156">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="83446-157">인증서를 순환했습니다.</span><span class="sxs-lookup"><span data-stu-id="83446-157">Rotated certificates</span></span>
> * <span data-ttu-id="83446-158">내보낸된 hello SSL 인증서</span><span class="sxs-lookup"><span data-stu-id="83446-158">Exported hello SSL certificate</span></span>
> * <span data-ttu-id="83446-159">Toouse Java, Python 및 Node.js에 인증서를 hello 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="83446-159">Learned how toouse hello certificate in Java, Python and Node.js</span></span>

<span data-ttu-id="83446-160">이제 toohello Cosmos DB에 대 한 자세한 내용은 개념 섹션을 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83446-160">You can now proceed toohello Concepts section for more information about Cosmos DB.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="83446-161">글로벌 분포</span><span class="sxs-lookup"><span data-stu-id="83446-161">Global distribution</span></span>](distribute-data-globally.md) 
