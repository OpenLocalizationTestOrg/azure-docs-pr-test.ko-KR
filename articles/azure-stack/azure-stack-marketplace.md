---
title: "Azure 스택 (클라우드 연산자)에서 사용자 지정 마켓플레이스 항목을 게시 | Microsoft Docs"
description: "Azure 스택 연산자 Azure 스택에 사용자 지정 마켓플레이스 항목을 게시 하는 방법에 설명 합니다."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 60871cbb-eed2-433c-a76d-d605c7aec06c
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: erikje
ms.openlocfilehash: 7b5f976eb2d51eb86761a2bd0be6adb45ca87681
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="the-azure-stack-marketplace-overview"></a>Azure 스택 마켓플레이스 개요

*적용 대상: Azure 스택 통합 시스템과 Azure 스택 개발 키트*

마켓플레이스는 서비스, 응용 프로그램 및 네트워크, 가상 컴퓨터, 저장소, 등과 같이 Azure 스택에 대 한 사용자 지정 리소스의 컬렉션입니다. 여기로 사용자와 새 리소스를 만들 새 응용 프로그램을 배포 합니다. 것으로 생각 하면 쇼핑 카탈로그 사용자 찾아볼 수도 있고 사용 하려는 항목을 선택 합니다. 마켓플레이스 항목을 사용 하려면 사용자가 항목에 대 한 액세스를 부여 하는 서비스를 구독 해야 합니다.

Azure 스택 연산자로 결정 추가할 항목을 마켓플레이스에 (게시). 데이터베이스, 응용 프로그램 서비스 등과 같은 항목을 게시할 수 있습니다. 따라서 하 여 모든 사용자에 게 표시 됩니다. 작성 한 사용자 지정 항목을 게시할 수 있습니다. 증가 하는 항목을 게시할 수도 있습니다 [Azure 마켓플레이스 항목 목록이](azure-stack-marketplace-azure-items.md)합니다. 마켓플레이스 항목을 게시할 때 사용자가 5 분 이내 볼 수 있습니다.

Marketplace를 열려면 **새로 만들기**를 클릭합니다.

![](media/azure-stack-publish-custom-marketplace-item/image1.png)

## <a name="marketplace-items"></a>Marketplace 항목
Azure 스택 마켓플레이스 항목 서비스, 응용 프로그램 또는 사용자가 다운로드 하 고 사용할 수 있는 리소스입니다. 모든 Azure 스택 마켓플레이스 항목이 모든 사용자에 게 표시 됩니다.

모든 Marketplace 항목은 다음이 있습니다.

* 리소스 프로비전을 위한 Azure 리소스 관리자 템플릿
* 문자열, 아이콘 및 기타 마케팅 참고 자료와 같은 메타데이터
* 포털에서 항목을 표시 하는 서식 지정 정보

Marketplace에 게시되는 모든 항목은 Azure 갤러리 패키지(azpkg)라는 서식을 사용합니다. 마켓플레이스 항목의 일부가 아니라 Azure 스택에 배포 또는 런타임 리소스 (예: 코드, 소프트웨어 또는 가상 컴퓨터 이미지와 zip 파일)를 개별적으로 추가 합니다. 

## <a name="next-steps"></a>다음 단계
[만들기 및 마켓플레이스 항목을 게시](azure-stack-create-and-publish-marketplace-item.md)

