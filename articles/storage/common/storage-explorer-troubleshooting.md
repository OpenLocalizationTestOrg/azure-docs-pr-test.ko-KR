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
# <a name="azure-storage-explorer-troubleshooting-guide"></a>Azure Storage 탐색기 문제 해결 가이드

## <a name="introduction"></a>소개

Microsoft Azure 저장소 탐색기 (미리 보기)는 Windows, macOS 및 Linux에서 데이터를 Azure 저장소 사용 tooeasily 작업 수 있는 독립 실행형 앱입니다. hello 앱 Azure, Sovereign 클라우드 및 Azure 스택에서 호스팅되는 toStorage 계정을 연결할 수 있습니다.

이 가이드에는 Storage 탐색기에 나타나는 일반적인 문제에 대한 솔루션이 요약되어 있습니다.

## <a name="sign-in-issues"></a>로그인 문제

계속 하기 전에 응용 프로그램을 다시 시도 하 고 hello 문제를 해결할 수 있는지 여부를 참조 하십시오.

### <a name="error-self-signed-certificate-in-certificate-chain"></a>오류: 인증서 체인의 자체 서명된 인증서

여러 가지 이유로 발생할 수 있습니다이 오류 이유와 hello 가장 일반적인 두 가지 이유는 다음과 같습니다.

1. hello 앱 "투명 프록시"를 통해 서버 (예: 회사 서버)의 HTTPS 트래픽을 차단, 암호 해독 고 자체 서명 된 인증서를 사용 하 여 암호화 한 다음 연결 되어 있습니다.

2. 바이러스 백신 소프트웨어를 삽입 하는 자체 서명 된 SSL 인증서를 수신 하는 hello HTTPS 메시지로 같은 응용 프로그램을 실행 하는 합니다.

저장소 탐색기 hello 문제를 발견 하면 수신 hello HTTPS 메시지는 변조 여부를 알고 더 이상 수 없습니다. Hello 자체 서명 된 인증서의 복사본을 사용 하는 경우 저장소 탐색기를 신뢰 하도록 할 수 있습니다. hello 인증서 삽입 하 게 잘 모를 경우 이러한 단계 toofind를 수행 하기:

1. OpenSSL을 설치합니다.

    - [Windows](https://slproweb.com/products/Win32OpenSSL.html) (hello 밝은 버전 중 하나 여야 함 충분)

    - Mac 및 Linux: 운영 체제에 포함되어야 합니다.

2. OpenSSL을 실행합니다.

    - Windows: hello 설치 디렉터리를 열고, 클릭 **/bin/**, 두 번 클릭 하 고 **openssl.exe**합니다.
    - Mac 및 Linux: 터미널에서 **openssl**을 실행합니다.

3. s_client -showcerts -connect microsoft.com :443을 실행합니다.

4. 자체 서명된 인증서를 찾습니다. 자체 서명 된 확실 하지 않은 경우 아무 곳 이나 hello 제목 ("s:")를 찾고 발급자 ("i:")는 동일 hello 됩니다.

5. 자체 서명 된 인증서를 찾은 면 각 하나에 대 한 복사 하 여 포함 하 여에서 모든 항목을 붙여 **---BEGIN 인증서---** 너무**---END 인증서---** tooa 새.cer 파일입니다.

6. 저장소 탐색기를 열고 **편집** > **SSL 인증서** > **가져오기 인증서**, 한 다음 사용 하 여 hello 파일 선택기 toofind, select, 만든 hello.cer 파일을 엽니다.

단계는 hello를 사용 하 여 자체 서명 된 인증서를 찾을 수 없는 경우 hello 피드백 도구에 대 한 자세한 도움말을 통해 문의.

### <a name="unable-tooretrieve-subscriptions"></a>없습니다 tooretrieve 구독

구독 한 후에 성공적으로 로그인 하는 없습니다 tooretrieve 인 경우 이러한 단계 tootroubleshoot이이 문제를 수행 합니다.

- Hello Azure 포털에 로그인 하 여 사용자 계정 액세스 toohello 구독에 있는지 확인 합니다.

- Hello 올바른 환경 (Azure, Azure 중국, 독일 Azure, Azure 미국 정부 또는 사용자 정의 환경/Azure 스택)를 사용 하 여 로그인 한 있는지 확인 합니다.

- 프록시 뒤에 있다면 hello 저장소 탐색기 프록시를 제대로 구성 했는지 확인 합니다.

- 제거 하 고 다시 추가 중 hello 계정 사용을 시도 합니다.

- 파일 루트 디렉터리 (즉, C:\Users\ContosoUser)에서 고 hello 계정을 다시 추가 hello를 삭제 해 보십시오.

    - .adalcache

    - .devaccounts

    - .extaccounts

- 조사식 hello 개발자 도구 콘솔 (f 12를 눌러) 경우 로그인 하는 모든 오류 메시지:

![개발자 도구](./media/storage-explorer-troubleshooting/4022501_en_2.png)

### <a name="unable-toosee-hello-authentication-page"></a>없습니다 toosee hello 인증 페이지

없습니다 toosee hello 인증 페이지 인 경우 이러한 단계 tootroubleshoot이이 문제를 수행 합니다.

- 연결의 hello 속도 따라 hello 로그인 페이지 tooload 시간이 오래 걸릴 수 있습니다, 그리고 hello 인증 대화 상자를 닫기 전에 적어도 1 분까지 기다려야 합니다.

- 프록시 뒤에 있다면 hello 저장소 탐색기 프록시를 제대로 구성 했는지 확인 합니다.

- Hello F12 키를 눌러 보기 hello 개발자 콘솔. Hello 응답 hello 개발자 콘솔에서 감시 하 고 이유에 대 한 모든 단서를 찾을 수 있는지 여부를 참조 하십시오. 인증 작동 하지 않습니다.

### <a name="cannot-remove-account"></a>계정을 제거할 수 없음

계정이 없습니다 tooremove 없거나 hello 다시 인증 링크 아무 작업도 수행 하지 않는 경우 이러한 단계 tootroubleshoot이이 문제를 따르십시오.

- 루트 디렉터리에서 파일을 따르고 다음 hello 계정에 다시 추가 중 hello를 삭제 해 보십시오.

    - .adalcache

    - .devaccounts

    - .extaccounts

- Tooremove SAS 저장소 리소스를 연결 하려면 다음 파일이 hello를 삭제 합니다.

    - Windows - %AppData%/StorageExplorer 폴더

    - Mac - Users/<your_name>/Library/Applicaiton SUpport/StorageExplorer

    - Linux - ~/.config/StorageExplorer

> [!NOTE]
>  나면 tooreenter 자격 증명 이러한 파일을 삭제 합니다.

## <a name="proxy-issues"></a>프록시 문제

먼저, 정보를 입력 한 다음 해당 hello 모두 정확한 지 확인:

- hello 프록시 URL과 포트 번호

- 사용자 이름 및 암호 hello 프록시에 필요한 경우

### <a name="common-solutions"></a>일반적인 솔루션

문제가 여전히 발생 하는 경우에 따라 이러한 단계 tootroubleshoot 해당:

- 프록시를 사용 하지 않고 toohello 인터넷에 연결할 수 있는, 경우에 저장소 탐색기 프록시 설정을 사용 하도록 설정 하지 않고 작동 하는지 확인 합니다. 상황에 hello 프록시 설정에 문제가 있을 수 있습니다. 프록시 관리자 tooidentify hello 문제를 사용 합니다.

- 다른 응용 프로그램 프록시 서버 hello를 사용 하 여 예상 대로 작동 하는지 확인 합니다.

- 웹 브라우저를 사용 하 여 toohello Microsoft Azure 포털에 연결할 수 있는지 확인 하십시오.

- 서비스 끝점에서 응답을 수신할 수 있는지 확인합니다. 끝점 URL 중 하나를 브라우저에 입력합니다. 연결할 수 있으면 InvalidQueryParameterValue 또는 유사한 XML 응답을 수신해야 합니다.

- 다른 사용자가 Storage 탐색기와 프록시 서버를 함께 사용하고 있는 경우 연결할 수 있는지 확인합니다. 연결할 수 있는 경우 toocontact 프록시 서버 관리자

### <a name="tools-for-diagnosing-issues"></a>문제를 진단하기 위한 도구

Windows 용 Fiddler와 같은 네트워킹 도구 경우 다음과 같이 수 toodiagnose hello 문제 수 있습니다.

- 프록시를 통해 toowork를 설정한 경우 hello 프록시를 통해 네트워킹 도구 tooconnect 프로그램 tooconfigure를 할 수 있습니다.

- 네트워킹 도구에서 사용 하는 hello 포트 번호를 확인 합니다.

- 저장소 탐색기의 프록시 설정으로 도구의 포트 번호를 네트워킹 hello와 hello 로컬 호스트 URL을 입력 합니다. 이 isdone 올바르게 네트워킹 도구 시작 저장소 탐색기 toomanagement 및 서비스 끝점에서 만든 네트워크 요청을 기록 합니다. 예를 들어 브라우저에서 blob 끝점 https://cawablobgrs.blob.core.windows.net/를 입력 하 고 응답을 받습니다. 액세스할 수 있지만 hello 리소스가 존재를 제안 하는 hello 다음 예제와 유사 합니다.

![코드 샘플](./media/storage-explorer-troubleshooting/4022502_en_2.png)

### <a name="contact-proxy-server-admin"></a>프록시 서버 관리자 문의

프록시 설정이 올바른지, 해야 toocontact 프록시 서버 관리자에 게 및

- 프록시 트래픽 tooAzure 관리 또는 리소스 끝점을 차단 하지 않습니다 있는지 확인 합니다.

- 프록시 서버에서 사용 하는 hello 인증 프로토콜을 확인 합니다. Storage 탐색기는 현재 NTLM 프록시를 지원하지 않습니다.

## <a name="unable-tooretrieve-children-error-message"></a>"없습니다 tooRetrieve 자식" 오류 메시지

프록시를 통해 연결 된 tooAzure 인 경우에 프록시 설정이 올바른지 확인 합니다. Hello 구독이 나 계정을의 hello 소유자 로부터 tooa 리소스 액세스를 부여 된 경우 확인 읽기 하거나 해당 리소스에 대 한 사용 권한을 나열 합니다.

### <a name="issues-with-sas-url"></a>SAS URL 문제
SAS URL을 사용 하 고이 오류를 발생 tooa 서비스 연결 하는 경우:

- Hello URL 제공 tooread 또는 목록 리소스 hello 필요한 권한이 있는지 확인 합니다.

- 해당 hello URL 만료 되지 않았는지 확인 합니다.

- Hello SAS URL 액세스 정책에 따르면 hello 액세스 정책을 취소 되지 않았는지를 확인 합니다.

## <a name="next-steps"></a>다음 단계

Hello 솔루션 중, 적합 한 경우 전자 메일 hello 피드백 도구를 통해 문제를 제출 하 고 연락을 드릴 수 있습니다 hello 문제를 해결 하기 위한 있도록 있습니다으로 포함 하는 hello 문제에 대 한 자세한 정보 수 있습니다.

toodo이를 클릭 하이 여 **도움말** 메뉴를 차례로 클릭 **사용자 의견 보내기**합니다.

![사용자 의견](./media/storage-explorer-troubleshooting/4022503_en_1.png)
