---
title: "서버 탐색기에서 Azure 가상 컴퓨터 aaaAccessing | Microsoft Docs"
description: "Tooview 만들고 Visual Studio 서버 탐색기에서 Azure 가상 컴퓨터 (Vm) 관리에 대 한 개요를 가져옵니다."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: eb3afde6-ba90-4308-9ac1-3cc29da4ede0
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: f8326aed105a64ca558f766d712cc68701f82c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-azure-virtual-machines-from-server-explorer"></a>서버 탐색기에서 Azure 가상 컴퓨터 액세스(영문)
Visure Studio에서 서버 탐색기를 사용하여 Azure에서 호스팅되는 가상 컴퓨터에 대한 정보를 표시할 수 있습니다.

## <a name="accessing-virtual-machines-in-server-explorer"></a>서버 탐색기의 Azure 가상 컴퓨터 액세스
Azure에서 호스팅되는 가상 컴퓨터가 있는 경우 서버 탐색기에서 액세스할 수 있습니다. 먼저 로그인 해야 tooyour Azure 구독 tooview 모바일 서비스입니다. 에서는 toosign가 서버 탐색기에서 Azure 노드 hello에 대 한 hello 바로 가기 메뉴를 열고 선택 **tooMicrosoft Azure 연결**합니다.

### <a name="tooget-information-about-your-virtual-machines"></a>가상 컴퓨터에 대 한 tooget 정보
1. 서버 탐색기에서 가상 컴퓨터를 선택 하 고 hello F4 키 tooshow 고 속성 창을 선택 합니다.
   
    다음 표에 hello 속성을 보여 줍니다를 사용할 수 있지만 모든 읽기 전용입니다. toochange hello를 사용 하 여, [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)합니다.
   
   | 속성 | 설명 |
   | --- | --- |
   | DNS 이름 |hello 가상 컴퓨터의 인터넷 주소 hello로 hello URL입니다. |
   | Environment |가상 컴퓨터에 대 한이 속성의 hello 값은 항상 프로덕션입니다. |
   | 이름 |hello 가상 컴퓨터의 hello 이름입니다. |
   | 크기 |hello 양을 사용할 수 있는 메모리와 디스크 공간을 반영 하는 hello 가상 컴퓨터의 hello 크기입니다. 자세한 내용은 가상 컴퓨터 구성 방법을 참조하세요. |
   | 가동 상태 |값은 시작, 시작됨, 중지, 중지됨 및 상태 검색을 포함합니다. 상태 검색에 표시 되 면 hello 현재 상태를 알 없습니다. hello에 사용 되는 hello 값에서이 속성에 대 한 hello 값이 다른 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)합니다. |
   | 구독 ID |Azure 계정에 대 한 hello 구독 ID입니다. Hello에이 정보를 표시할 수 있습니다 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885) 구독에 대 한 hello 속성을 확인 하 여 합니다. |
2. 끝점 노드를 선택한 다음 hello 볼 **속성** 창.
3. hello 다음 표에서 설명 hello 끝점의 사용 가능한 속성이 있지만 읽기 전용입니다. 가상 컴퓨터에 대 한 hello 끝점 tooadd 또는 편집 hello를 사용 하 여 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)합니다. 
   
   | 속성 | 설명 |
   | --- | --- |
   | 이름 |Hello 끝점에 대 한 식별자입니다. |
   | 개인 포트 |네트워크 액세스에 대 한 내부 tooyour 응용 프로그램에 대 한 hello 포트입니다. |
   | 프로토콜 |TCP 또는 UDP hello 프로토콜 hello이 끝점에 대 한 전송 계층을 사용 합니다. |
   | 공용 포트 |공용 액세스 tooyour 응용 프로그램에 사용 되는 hello 포트입니다. |

## <a name="next-steps"></a>다음 단계
Visual Studio에서 Azure 역할 사용에 대 한 더 toolearn 참조 [Azure 역할과 함께 원격 데스크톱 사용 하 여](vs-azure-tools-remote-desktop-roles.md)합니다.

