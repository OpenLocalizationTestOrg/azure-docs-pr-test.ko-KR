---
title: "aaaConfiguring 및 Visual Studio와 함께 저장소 에뮬레이터를 hello를 사용 하 여 | Microsoft Docs"
description: "구성 및 Visual Studio와 함께 hello 저장소 에뮬레이터 사용"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: c8e7996f-6027-4762-806e-614b93131867
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/17/2017
ms.author: kraigb
ms.openlocfilehash: d590f21146c86bcb7bfa6b6164b92c6df5938d5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-and-using-hello-storage-emulator-with-visual-studio"></a>구성 및 Visual Studio와 함께 hello 저장소 에뮬레이터 사용
[!INCLUDE [storage-try-azure-tools](../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>개요
hello Azure SDK 개발 환경 hello 저장소 에뮬레이터, hello Blob, 큐 및 테이블 저장소 서비스 시뮬레이션 하 여 로컬 개발 컴퓨터에 Azure에서 제공 하는 유틸리티를 포함 합니다. hello Azure 저장소 서비스를 사용 하는 클라우드 서비스를 구축 또는 hello 저장소 서비스를 호출 하는 외부 응용 프로그램을 작성, 코드 hello 저장소 에뮬레이터에 대해 로컬로 테스트할 수 있습니다. hello Azure Tools for Microsoft Visual Studio는 Visual Studio로 hello 저장소 에뮬레이터의 관리를 통합 합니다. 처음 사용할 때 hello 저장소 에뮬레이터 데이터베이스를 초기화 하는 hello Azure 도구, 시작 hello 저장소 에뮬레이터 서비스를 실행 하거나 Visual Studio에서 코드를 디버깅 하 고 hello Azure 저장소 탐색기를 통해 toohello 저장소 에뮬레이터 데이터 읽기 전용 액세스를 제공 합니다.

시스템 요구 사항 및 사용자 지정 구성 지침을 포함 하는 hello 저장소 에뮬레이터에 대 한 자세한 내용은 참조 [개발 및 테스트에 Azure 저장소 에뮬레이터 사용 하 여 hello](storage/common/storage-use-emulator.md)합니다.

> [!NOTE]
> Hello 저장소 에뮬레이터 시뮬레이션과 hello Azure 저장소 서비스 간의 기능에서 차이가 있습니다. 참조 [차이점 hello 저장소 에뮬레이터와 Azure 저장소 서비스](storage/common/storage-use-emulator.md) hello hello 특정 차이점에 대 한 내용은 Azure SDK 설명서에에서 있습니다.
> 
> 

## <a name="configuring-a-connection-string-for-hello-storage-emulator"></a>Hello 저장소 에뮬레이터에 대 한 연결 문자열 구성
역할 내의 코드에서 tooaccess hello 저장소 에뮬레이터, tooconfigure 한 연결 문자열 해당 지점 toohello 저장소 에뮬레이터 및 변경 된 toopoint tooan Azure 저장소 계정을 나중에 일 수 있는 있습니다 해야 합니다. 연결 문자열은 사용자의 역할 런타임 tooconnect tooa 저장소 계정에서 읽을 수 있는 구성 설정입니다. 방법에 대 한 자세한 내용은 toocreate 연결 문자열 참조 [구성 hello Azure 응용 프로그램](https://msdn.microsoft.com/library/azure/2da5d6ce-f74d-45a9-bf6b-b3a60c5ef74e#BK_SettingsPage)합니다.

> [!NOTE]
> Hello를 사용 하 여 사용자 코드에서 참조 toohello 저장소 에뮬레이터 계정을 반환할 수 있습니다 **DevelopmentStorageAccount** 속성입니다. 이 접근 tooaccess hello 사용자 코드에서 저장소 에뮬레이터만 응용 프로그램 tooAzure toopublish 하려는 경우 Azure 저장소 계정 연결 문자열 tooaccess toocreate 필요를 코드 toouse 수정 해야 할 경우 제대로 작동 하는 게시 하기 전에 연결 문자열입니다. Hello 저장소 에뮬레이터 계정과 Azure 저장소 계정 사이 자주 전환할 연결 문자열은이 프로세스를 간소화 합니다.
> 
> 

## <a name="initializing-and-running-hello-storage-emulator"></a>Hello 저장소 에뮬레이터 초기화 및 실행
실행 하거나 Visual Studio에서 서비스를 디버깅할 때 Visual Studio 자동으로 시작 hello 저장소 에뮬레이터를 지정할 수 있습니다. 솔루션 탐색기에서 hello 바로 가기 메뉴를 열고 프로그램 **Azure** 프로젝트를 마우스 선택 **속성**합니다. Hello에 **개발** 탭 hello **Azure 저장소 에뮬레이터 시작** 목록에서 선택 **True** (toothat 값을 아직 설정 되지 않은) 하는 경우.

hello 처음으로 실행 하거나 Visual Studio, hello 저장소 에뮬레이터에서에서 서비스를 디버그 하는 초기화 프로세스를 시작 합니다. 이 프로세스는 hello 저장소 에뮬레이터에 대 한 로컬 포트를 예약 하 고 hello 저장소 에뮬레이터 데이터베이스를 만듭니다. 완료 되 면이 프로세스는 않아도 toorun 다시 hello 저장소 에뮬레이터 데이터베이스를 삭제 하지 않으면 됩니다.

> [!NOTE]
> Hello Azure Tools의 2012 년 6 월 릴리스를 hello 부터는 hello 저장소 에뮬레이터 실행, 기본적으로 SQL Express LocalDB에서 됩니다. SQL Express 2005 또는 2008 년의 기본 인스턴스에 대해 실행 hello 저장소 에뮬레이터의 hello Azure Tools의 이전 릴리스에서 hello Azure SDK를 설치 하기 전에 설치 해야 합니다. SQL Express 또는 명명 된의 명명 된 인스턴스 또는 Microsoft SQL Server의 기본 인스턴스에 대해 hello 저장소 에뮬레이터를 실행할 수 있습니다. Tooconfigure hello 저장소 에뮬레이터 toorun hello 기본 인스턴스가 아닌 인스턴스에 대해 필요한 경우 참조 [개발 및 테스트에 Azure 저장소 에뮬레이터 사용 하 여 hello](storage/common/storage-use-emulator.md)합니다.
> 
> 

hello 로컬 저장소 서비스의 사용자 인터페이스 tooview hello 상태를 제공 하는 hello 저장소 에뮬레이터 및 toostart, 중지 및 다시 설정 합니다. Hello 저장소 에뮬레이터 서비스가 시작 되 면 hello 사용자 인터페이스를 표시 하거나 시작할 수 있습니다 또는 hello 알림 영역 아이콘을 마우스 오른쪽 단추로 클릭 하 여 hello 서비스 중지 hello Windows 작업 표시줄에서 Microsoft Azure 에뮬레이터를 환영 합니다.

## <a name="viewing-storage-emulator-data-in-server-explorer"></a>서버 탐색기에서 저장소 에뮬레이터 데이터 보기
서버 탐색기에서 Azure 저장소 노드 hello를 사용 하면 blob에 대 한 데이터와 변경 설정을 tooview 및 테이블 데이터를 포함 하 여 저장소 계정의 저장소 에뮬레이터 hello 합니다. 자세한 내용은 [저장소 탐색기(미리 보기)를 사용하여 Azure Blob Storage 리소스 관리](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs)를 참조하세요.

