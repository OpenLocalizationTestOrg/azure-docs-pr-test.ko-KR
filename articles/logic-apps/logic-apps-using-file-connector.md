---
title: "aaaConnect tooon 온-프레미스 파일 시스템에서 Azure 논리 앱 | Microsoft Docs"
description: "온-프레미스 데이터 게이트웨이 hello와 파일 시스템 커넥터를 통해 논리 앱 워크플로에서 tooon 온-프레미스 파일 시스템 연결"
keywords: "파일 시스템"
services: logic-apps
author: derek1ee
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/27/2017
ms.author: LADocs; deli
ms.openlocfilehash: beb5565293def4aba81f63f19e77d7498aac38c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-file-systems-from-logic-apps-with-hello-file-system-connector"></a>Hello 파일 시스템 커넥터를 사용 하 여 논리 앱에서 tooon 온-프레미스 파일 시스템 연결

하이브리드 클라우드 연결 중앙 toologic 앱, 따라서 toomanage 데이터 하며 안전 하 게 액세스 온-프레미스 리소스, 논리 앱 hello 온-프레미스 데이터 게이트웨이 사용할 수 있습니다. 이 문서에서는 어떻게 tooconnect tooan 온-프레미스 파일 시스템 기본 시나리오를 보여 줍니다:는 업로드 된 tooDropbox tooa 파일 공유를 다음 전자 메일을 보낼 파일을 복사 합니다.

## <a name="prerequisites"></a>필수 조건

- 설치 하 고 최신 hello 구성 [온-프레미스 데이터 게이트웨이](https://www.microsoft.com/download/details.aspx?id=53127)합니다.
- 설치 hello 최신 온-프레미스 데이터 게이트웨이 1.15.6150.1 버전 이상. [Toohello 온-프레미스 데이터 게이트웨이 연결](http://aka.ms/logicapps-gateway) 목록 hello 단계입니다. hello 나머지 hello 단계를 계속 하기 전에 hello 게이트웨이 온-프레미스 컴퓨터에 설치 되어야 합니다.

## <a name="add-trigger-and-actions-for-connecting-tooyour-file-system"></a>트리거 및 tooyour 파일 시스템 연결에 대 한 작업 추가

1. 논리 앱을 만들고 Dropbox 트리거: **파일이 만들어진 경우**를 추가합니다. 
2. Hello 트리거 선택 **다음 단계** > **동작 추가**합니다. 
3. Hello 검색 상자에 입력 `file system` hello 파일 시스템 커넥터에 대 한 지원 되는 모든 작업을 볼 수 있도록 합니다.

   ![파일 커넥터 검색](media/logic-apps-using-file-connector/search-file-connector.png)

2. Hello 선택 **파일 만들기** 동작을 연결 tooyour 파일 시스템을 만듭니다.

   기존 연결 되지 않은 경우 하나 toocreate 메시지 표시 됩니다.

   1. **온-프레미스 데이터 게이트웨이를 통해 연결**을 선택합니다. 더 많은 속성이 표시됩니다.
   2. 파일 시스템에 대한 루트 폴더를 선택합니다.
      
       > [!NOTE]
       > hello 루트 폴더는 모든 파일 관련 작업에 대 한 상대 경로에 사용 되는 hello 기본 부모 폴더입니다. Hello 컴퓨터 hello 폴더 hello 컴퓨터는 네트워크 공유에 액세스할 수 있을 수 있습니다 또는 hello 온-프레미스 데이터 게이트웨이가 설치 된 위치에서 로컬 폴더를 지정할 수 있습니다.

   3. Hello 게이트웨이에 대 한 hello 사용자 이름 및 암호를 입력 합니다.
   4. 이전에 설치한 hello 게이트웨이 선택 합니다.

       ![연결 구성](media/logic-apps-using-file-connector/create-file.png)

3. Hello에 대 한 세부 정보를 모두 제공한 후 선택 **만들기**합니다. 

   논리 앱 구성 및 hello 연결이 제대로 작동 하는지 확인 하 여 연결을 테스트 합니다. 
   Hello 연결 올바르게 설치 되 면 이전에 선택한 hello 동작에 대 한 옵션이 표시 됩니다. 
   hello 파일 시스템 커넥터가 사용할 준비가 되었습니다.

4. 온-프레미스 파일 공유에 대 한 Dropbox toohello 루트 폴더에서 파일 toocopy 되도록 지정 합니다.

   ![파일 작업 만들기](media/logic-apps-using-file-connector/create-file-filled.png)

5. 논리 앱 복사본 hello 파일을 후 hello 새 파일에 대 한 관련 사용자를 확인할 수 있도록 전자 메일을 보내는 Outlook 동작을 추가 합니다. Hello 받는 사람, 제목 및 hello 전자 메일의 본문을 입력 합니다. 

   Hello 동적 콘텐츠 편집기 도구 모음에서 더 많은 세부 정보 toohello 전자 메일을 추가할 수 있도록 hello 파일 커넥터에서 데이터 출력 선택할 수 있습니다.

   ![전자 메일 보내기 작업](media/logic-apps-using-file-connector/send-email.png)

6. 논리 앱을 저장합니다. 파일 tooDropbox 업로드 하 여 응용 프로그램을 테스트 합니다. hello 파일을 복사한 toohello 온-프레미스 파일 공유를 얻어야 하 고 hello 작업에 대 한 전자 메일을 받게 됩니다.

   > [!TIP] 
   > 너무 방법에 대해 알아봅니다[논리 앱 모니터링](../logic-apps/logic-apps-monitor-your-logic-apps.md)합니다.

축, tooyour 온-프레미스 파일 시스템에 연결할 수 있는 작업 중인 논리 앱 생깁니다. 예를 들어 커넥터 제공 hello 다른 기능을 탐색 하십시오.

- 파일 만들기
- 폴더의 파일 나열
- 파일 첨부
- 파일 삭제
- 파일 콘텐츠 가져오기
- 경로를 사용하여 파일 콘텐츠 가져오기
- 파일 메타데이터 가져오기
- 경로를 사용하여 파일 메타데이터 가져오기
- 루트 폴더의 파일 나열
- 파일 업데이트

## <a name="view-hello-swagger"></a>Hello swagger 보기
Hello 참조 [세부 정보를 swagger](/connectors/fileconnector/)합니다. 

## <a name="get-help"></a>도움말 보기

tooask 질문 질문에 답변 하 고 다른 Azure 논리 앱을 수행 하는 사용자가 방문 hello 자세한 [Azure 논리 앱 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)합니다.

Azure 논리 앱 및 커넥터 향상, 투표 하거나 hello에서 아이디어 제출 toohelp [Azure 논리 앱 사용자 의견 사이트](http://aka.ms/logicapps-wish)합니다.

## <a name="next-steps"></a>다음 단계

- [Tooon 온-프레미스 데이터 연결](../logic-apps/logic-apps-gateway-connection.md) 논리 앱에서
- [엔터프라이즈 통합](../logic-apps/logic-apps-enterprise-integration-overview.md)에 대해 알아봅니다.
