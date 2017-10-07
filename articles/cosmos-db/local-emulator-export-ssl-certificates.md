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
# <a name="export-hello-azure-cosmos-db-emulator-certificates-for-use-with-java-python-and-nodejs"></a>Java, Python 및 Node.js와 함께 사용할 hello Azure Cosmos DB 에뮬레이터 인증서 내보내기

[**에뮬레이터의 hello 다운로드**](https://aka.ms/cosmosdb-emulator)

hello Azure Cosmos DB 에뮬레이터 hello Azure Cosmos DB 서비스를 SSL 연결 사용을 포함 하 여 개발 목적으로 에뮬레이트하는 로컬 환경을 제공 합니다. 이 게시물 언어 및 hello 자체를 사용 하 여 Java와 같은 Windows 인증서 저장소와 통합 되지 않는 런타임에서 사용 하기 위해 tooexport hello SSL 인증서 하는 방법을 보여 줍니다. [인증서 저장소](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) 및 를사용하여Python[래퍼 소켓](https://docs.python.org/2/library/ssl.html) 및 사용 하 여 Node.js [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback)합니다. 자세한 내용은의 hello 에뮬레이터에 대 한 [개발 및 테스트에 사용 하 여 hello Azure Cosmos DB 에뮬레이터](./local-emulator.md)합니다.

이 자습서에서는 hello 다음 작업 방법을 배웁니다.

> [!div class="checklist"]
> * 인증서 순환
> * SSL 인증서 내보내기
> * Toouse Java, Python 및 Node.js에 인증서를 hello 하는 방법 학습

## <a name="certification-rotation"></a>인증 회전

Hello hello 에뮬레이터를 실행 하는 처음으로 생성 하는 Azure Cosmos DB 로컬 에뮬레이터는 hello에 있는 인증서. 두 개의 인증서가 있습니다. Toohello 로컬 에뮬레이터와 hello 에뮬레이터 내에서 암호 관리에 대해 각각 하나씩 연결 하는 데 사용 되는 하나입니다. tooexport hello 인증서는 hello 친숙 한 이름이 "DocumentDBEmulatorCertificate" hello 연결 인증서입니다.

두 인증서를 클릭 하 여 다시 생성할 수 있습니다 **재설정 데이터** 트레이 Windows hello에서 실행 하는 Azure Cosmos DB 에뮬레이터에서 다음과 같이 합니다. Hello 인증서가 다시 생성 하 고 hello Java 인증서 저장소에 설치 했거나 다른 위치에서 사용 되는 경우 tooupdate 이러한 응용 프로그램 toohello 로컬 에뮬레이터는 더 이상 연결 하는 그렇지 않은 경우.

![Azure Cosmos DB 로컬 에뮬레이터 데이터 다시 설정](./media/local-emulator-export-ssl-certificates/database-local-emulator-reset-data.png)

## <a name="how-tooexport-hello-azure-cosmos-db-ssl-certificate"></a>어떻게 tooexport hello Azure Cosmos DB SSL 인증서

1. Certlm.msc를 실행 하 여 hello Windows 인증서 관리자를 시작 하 고 탐색-> toohello 개인 인증서 폴더 및 hello 친숙 한 이름의 열기 hello 인증서 **DocumentDbEmulatorCertificate**합니다.

    ![Azure Cosmos DB 로컬 에뮬레이터 내보내기 1단계](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-1.png)

2. **세부 정보**를 클릭한 다음 **확인**을 클릭합니다.

    ![Azure Cosmos DB 로컬 에뮬레이터 내보내기 2단계](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-2.png)

3. 클릭 **tooFile 복사...** .

    ![Azure Cosmos DB 로컬 에뮬레이터 내보내기 3단계](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-3.png)

4. **다음**을 누릅니다.

    ![Azure Cosmos DB 로컬 에뮬레이터 내보내기 4단계](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-4.png)

5. **아니요, 개인 키를 내보내지 않습니다.**를 클릭한 후 **다음**을 클릭합니다.

    ![Azure Cosmos DB 로컬 에뮬레이터 내보내기 5단계](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-5.png)

6. **Base-64 encoded X.509 (.CER)**를 클릭한 후 **다음**을 클릭합니다.

    ![Azure Cosmos DB 로컬 에뮬레이터 내보내기 6단계](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-6.png)

7. Hello 인증서에 이름을 지정 합니다. 여기서는 **documentdbemulatorcert**이며, **다음**을 클릭합니다.

    ![Azure Cosmos DB 로컬 에뮬레이터 내보내기 7단계](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-7.png)

8. **Finish**를 클릭합니다.

    ![Azure Cosmos DB 로컬 에뮬레이터 내보내기 8단계](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-8.png)

## <a name="how-toouse-hello-certificate-in-java"></a>Toouse java에서 인증서 hello 하는 방법

전달 hello 보다 쉽게 tooinstall hello 인증서 hello Java 기본 인증서 저장소로 않은 경우가 많으므로 Java 응용 프로그램 또는 hello Java 클라이언트를 사용 하는 MongoDB 응용 프로그램을 실행 하는 경우 "-Djavax.net.ssl.trustStore=<keystore> - Djavax.net.ssl.trustStorePassword= "<password>" 플래그입니다. 포함 하는 hello 예를 들어 [Java 데모 응용 프로그램](https://localhost:8081/_explorer/index.html) hello 기본 인증서 저장소에 따라 달라 집니다.

Hello에 hello 지침에 따라 [Java CA 인증서를 저장 하는 인증서 toohello 추가](https://docs.microsoft.com/azure/java-add-certificate-ca-store) hello 기본 Java 인증서 저장소로 tooimport hello X.509 인증서입니다. 있습니다 수 작업 하는 hello % JAVA_HOME % 디렉터리 keytool를 실행 하는 경우.

한 번 "CosmosDBEmulatorCertificate" SSL hello 인증서가 설치 된 응용 프로그램 수 tooconnect 속해 있어야 하며 사용 하 여 hello 로컬 Azure Cosmos DB 에뮬레이터입니다. Toofollow hello 경우가 toohave 문제가 계속 되 면 [SSL/TLS 연결 디버깅](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) 문서. 매우 높습니다 hello 인증서가 hello %JAVA_HOME%/jre/lib/security/cacerts 저장소에 설치 되지 않습니다. 예를 들어 Java 응용 프로그램의 설치 된 버전을 여러 개 있는 경우 hello 업데이트 하나 보다 다른 cacerts 저장소 사용 될 수 있습니다.

## <a name="how-toouse-hello-certificate-in-python"></a>Toouse는 Python에서 인증서를 hello 하는 방법

기본 hello로 [Python SDK(version 2.0.0 or higher)](documentdb-sdk-python.md) hello에 대 한 DocumentDB API는 시도 없고 toohello 로컬 에뮬레이터를 연결할 때 hello SSL 인증서를 사용 합니다. Toouse SSL 유효성 검사를 원하는 뒤 hello에 hello 예제 [Python 소켓 래퍼](https://docs.python.org/2/library/ssl.html) 설명서입니다.

## <a name="how-toouse-hello-certificate-in-nodejs"></a>Toouse는 Node.js에 인증서를 hello 하는 방법

기본 hello로 [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) hello에 대 한 DocumentDB API는 시도 없고 toohello 로컬 에뮬레이터를 연결할 때 hello SSL 인증서를 사용 합니다. Toouse SSL 유효성 검사를 원하는 뒤 hello에 hello 예제 [Node.js 설명서](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback)합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 hello 다음 작업을 수행 하면:

> [!div class="checklist"]
> * 인증서를 순환했습니다.
> * 내보낸된 hello SSL 인증서
> * Toouse Java, Python 및 Node.js에 인증서를 hello 하는 방법을 배웠습니다.

이제 toohello Cosmos DB에 대 한 자세한 내용은 개념 섹션을 진행할 수 있습니다.

> [!div class="nextstepaction"]
> [글로벌 분포](distribute-data-globally.md) 
