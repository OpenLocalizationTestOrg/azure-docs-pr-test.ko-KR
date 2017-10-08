---
title: "aaaCreate hello Azure 포털을 사용 하 여 MySQL 방화벽 규칙에 대 한 Azure 데이터베이스 관리 및 | Microsoft Docs"
description: "만들기 및 hello Azure 포털을 사용 하 여 MySQL 방화벽 규칙에 대 한 Azure 데이터베이스 관리"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 30dbdde4299df564fbf6581419e908186fe3b823
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-hello-azure-portal"></a>만들기 및 hello Azure 포털을 사용 하 여 MySQL 방화벽 규칙에 대 한 Azure 데이터베이스 관리
지정된 된 IP 주소 또는 IP 주소 범위에서 MySQL Server에 대 한 관리자 tooaccess Azure 데이터베이스를 사용 하는 서버 수준 방화벽 규칙입니다. 

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Hello Azure 포털에에서 서버 수준 방화벽 규칙을 만들려면

1. Hello MySQL 서버 블레이드의 설정에서 머리글을 클릭 하 여 **연결 보안** tooopen hello 연결 보안 블레이드 hello MySQL에 대 한 Azure 데이터베이스에 대 한 합니다.

   ![Azure Portal - 보안 연결 클릭](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. 클릭 **내 IP 추가** hello 도구 모음 toocreate hello Azure 시스템에서 인식 하는 대로 컴퓨터의 IP 주소 hello 사용 하는 규칙에 있습니다.

   ![Azure Portal - 내 IP 추가 클릭](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. Hello 구성 저장 하기 전에 IP 주소를 확인 합니다. 경우에 따라 Azure 포털을 살펴 hello IP 주소가 사용 된 hello IP 주소에서 다릅니다 때 인터넷 및 Azure 서버 hello에 액세스 합니다. 따라서 toochange hello IP 시작 및 끝 IP toomake hello 규칙 함수 예상 대로 할 수 있습니다.

   사용 하 여 검색 엔진 또는 다른 온라인 도구 toocheck 사용자의 IP 주소 ("란 내 IP 주소" 검색 등).

   ![내 IP 주소는 무엇입니까에 대한 Bing](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. 추가 주소 범위를 추가합니다. MySQL 방화벽에 대 한 hello Azure 데이터베이스에 대 한 hello 규칙에서 단일 IP 주소 또는 주소 범위를 지정할 수 있습니다. Toolimit hello 규칙 tooone 단일 IP 주소, 시작 IP 및 끝 IP 주소 hello 필드에 같게 형식 hello 하려면. Hello 방화벽을 열고 hello MySQL 서버 toowhich 올바른 자격 증명이 있는 모든 데이터베이스 관리자와 사용자 tooaccess 수 있습니다.

   ![Azure Portal - 방화벽 규칙 ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. 클릭 **저장** 에 hello 도구 모음 toosave이 서버 수준 방화벽 규칙입니다. Hello toohello 방화벽 규칙 업데이트 성공 했음을 hello 확인 될 때까지 기다립니다.

   ![Azure Portal - 저장 클릭](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a>Hello Azure 포털을 통해 기존 서버 수준 방화벽 규칙 관리
Hello 단계 toomanage hello 방화벽 규칙을 반복 합니다.
* tooadd hello 현재 컴퓨터를 클릭 하 여 **+ 내 IP 추가**합니다.
* hello에 tooadd 추가 IP 주소를 입력 **규칙 이름**, **시작 IP**, 및 **끝 IP**합니다.
* 기존 규칙을 toomodify hello 규칙의 hello 필드 중 하나를 클릭 하 고 수정 합니다.
* hello 줄임표 [...]를 클릭 하 고 클릭 하 여 기존 toodelete 규칙 **삭제**합니다.
* 클릭 **저장** toosave hello 변경 합니다.

## <a name="next-steps"></a>다음 단계
- Azure 데이터베이스 tooan MySQL server에 대 한 연결에 대 한 도움말을 참조 하십시오. [MySQL에 대 한 Azure 데이터베이스에 대 한 연결 라이브러리](./concepts-connection-libraries.md)
