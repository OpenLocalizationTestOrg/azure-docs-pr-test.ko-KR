---
title: "aaaCreate 및 Azure 포털을 사용 하 여 MySQL server에 대 한 Azure 데이터베이스 관리 | Microsoft Docs"
description: "설명 신속 하 게 MySQL server에 대 한 새 Azure 데이터베이스를 만들 하는 방법을 hello Azure 포털을 사용 하 여 hello 서버를 관리 합니다."
services: mysql
author: v-chenyh
ms.author: nolanwu
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: c532df43b3d2124d7bd34875b32d52357f162af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a>Azure Portal을 사용한 MySQL용 Azure Database 서버 만들기 및 관리
설명 신속 하 게 MySQL server에 대 한 새 Azure 데이터베이스를 만들 하는 방법을 hello Azure 포털을 사용 하 여 hello 서버를 관리 합니다. 서버 관리 서버 세부 정보 및 데이터베이스 보기, 암호 다시 설정 및 서버 hello 삭제를 포함 합니다.

## <a name="log-in-toohello-azure-portal"></a>Azure 포털 toohello에 로그인
Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.

## <a name="create-an-azure-database-for-mysql-server"></a>Azure Database for MySQL 서버 만들기
이러한 단계 toocreate "mysqlserver4demo" 이라는 MySQL 서버에 대 한 Azure 데이터베이스를 수행 합니다.

원 클릭 **새로** 단추 hello 왼쪽 위 모서리의 hello Azure 포털에서 찾을 수 있습니다.

2 선택 **데이터베이스** hello 새 페이지 및 선택에서 **MySQL에 대 한 Azure 데이터베이스** hello 데이터베이스 페이지에서.

> MySQL용 Azure Database 서버는 일련의 정의된 [계산 및 저장소](./concepts-compute-unit-and-storage.md) 리소스를 사용하여 만들어집니다. MySQL server에 대 한 Azure 데이터베이스 및 Azure 리소스 그룹 내의 hello 데이터베이스가 생성 됩니다.

![create-new-server](./media/howto-create-manage-server-portal/create-new-server.png)

3-다음 정보는 hello로 MySQL 폼에 대 한 hello Azure 데이터베이스를 입력 합니다.

| **양식 필드** | **필드 설명** |
|----------------|-----------------------|
| *서버 이름* | azure-mysql(서버 이름은 전역적으로 고유함) |
| *구독* | MySQLaaS(드롭다운 목록에서 선택) |
| *리소스 그룹* | myresource(새 리소스 그룹을 만들거나 기존 그룹 선택) |
| *서버 관리자 로그인* | myadmin(관리자 계정 이름을 설정함) |
| *암호* | 암호 관리자 계정 암호 |
| *암호 확인* | 관리자 계정 암호를 확인합니다. |
| *위치*: | 북유럽(북유럽 및 미국 서부 중 선택) |
| *버전* | 5.6(MySQL용 Azure Database 서버 버전 선택) |

4 클릭 **가격 책정 계층** toospecify hello 서비스 계층과 성능 수준을 새 서버에 대 한 합니다. 계산 단위는 기본 계층 50에서 100 및 표준 계층 100에서 200 사이로 구성할 수 있으며, 저장소는 포함된 금액에 따라 추가할 수 있습니다. 이 방법 가이드에서는 계산 단위 50 및 50GB를 선택합니다. 클릭 **확인** toosave 선택 합니다.
![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)

5 클릭 **만들기** tooprovision hello 서버입니다. 프로비전하는 데 몇 분이 걸립니다.

> Hello 확인 **Pin toodashboard** 배포 옵션 tooallow 간편한 추적 합니다.
> [!NOTE]
> 기본 계층에서 too1000GB 및 표준에 10000 GB를 계층 지원이 제공 됩니다 저장소, 공개 미리 보기에 대 한 최대 저장소 hello 이지만 여전히 제한 too1000GB 일시적으로 있습니다. 
</Include>

## <a name="update-an-azure-database-for-mysql-server"></a>MySQL용 Azure Database 서버 업데이트
새 서버를 프로 비전 되 면 사용자에 게 2 옵션 tooedit 기존 서버: hello 계산 단위를 변경 하 여 관리자 암호 자릿수 또는 소수 위쪽/아래쪽 hello 서버를 다시 설정 합니다.

### <a name="change-hello-administrator-user-password"></a>Hello 관리자 사용자 암호 변경
1-hello 서버에서 **개요** 블레이드에서 클릭 **암호 재설정** toopopulate 암호 입력 및 확인 창이 있습니다.

2-새 암호를 입력 하 고 아래와 같이 hello 창의 hello 암호 확인: ![암호 재설정](./media/howto-create-manage-server-portal/reset-password.png)

3 번 클릭 **확인** toosave hello에 대 한 새 암호입니다.

### <a name="scale-updown-by-changing-compute-units"></a>계산 단위를 변경하여 강화/규모 축소

1-에 hello 서버 블레이드에서 아래 **설정**, 클릭 **가격 책정 계층** tooopen hello 가격 책정 계층 블레이드 MySQL server에 대 한 hello Azure 데이터베이스에 대 한 합니다.

다음 2 단계 4 **MySQL server 용 Azure 데이터베이스 만들기** toochange 계산 단위 가격 책정 계층을 동일한 hello 합니다.

## <a name="delete-an-azure-database-for-mysql-server"></a>MySQL용 Azure Database 서버 삭제

1-서버의 hello **개요** 블레이드에서 클릭 **삭제** 명령 단추 tooopen hello Deleting 확인 블레이드입니다.

2-형식 hello hello 블레이드 double 확인의 입력된 상자에 올바른 서버 이름입니다.

3 번 클릭 **삭제** 단추를 다시 tooconfirm 작업을 삭제 하 고 hello 알림 표시줄에 "성공 삭제" 팝업 때까지 대기 합니다.

## <a name="list-hello-azure-database-for-mysql-databases"></a>MySQL 데이터베이스에 대 한 목록 hello Azure 데이터베이스
Hello 서버의 **개요** 블레이드에서 hello 데이터베이스 나타날 때까지 아래로 스크롤하여 hello 아래쪽에 바둑판식으로 배열 합니다. 모든 hello 데이터베이스 hello 테이블에 나열 됩니다. 클릭 **삭제** 명령 단추 tooopen hello Deleting 확인 블레이드입니다.

![show-databases](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a>MySQL용 Azure Database 서버의 세부 정보 보기
클릭 **속성** 아래 **설정** hello 서버의 블레이드가 열리고 hello **속성** 블레이드입니다. 그런 다음 서버 hello에 대 한 모든 세부 정보를 볼 수 있습니다.

## <a name="next-steps"></a>다음 단계

[빠른 시작: Azure Portal을 사용한 MySQL용 Azure Database 서버 만들기 및 관리](./quickstart-create-mysql-server-database-using-azure-portal.md)
