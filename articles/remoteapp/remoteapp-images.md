---
title: "aaaWhat은 hello Azure RemoteApp 템플릿 이미지는? | Microsoft Docs"
description: "Azure RemoteApp과 함께 포함 된 hello 템플릿 이미지에 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7f8442b2-81da-421e-a453-aa53ba2066b7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: ea012cec8dc581a8bd4a5a138ce302de19d5c6af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-in-hello-azure-remoteapp-template-images"></a>Hello Azure RemoteApp 템플릿 이미지에는 무엇입니까?
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

Azure RemoteApp 구독에는 다음 세 개의 템플릿 이미지가 포함되어 있습니다.

* Windows Server 2012
* Microsoft Office 365 ProPlus(Office 365 구독 필요)
* Microsoft Office 2013 Professional Plus(평가판 전용)

> [!IMPORTANT]
> Azure RemoteApp 구독 toohello 소프트웨어 Office 365 ProPlus, 별도 구독을 요구 하 고 프로덕션 환경에서 사용할 수 없는 Office 2013의 hello 예외를 사용 하 여 hello 이미지에서 액세스 권한을 부여 합니다. 즉, 사용자와 hello 프로그램 또는 hello 템플릿 이미지에 앱을 공유할 수 있습니다. 예를 들어 hello Windows Server 2012 R2 이미지를 사용 하는 컬렉션을 만들면 RemoteApp 통해 사용자가 tooaccess에 대 한 System Center Endpoint Protection을 게시할 수 있습니다.
> 
> 체크 아웃 hello [세부 정보를 라이선스 하는 RemoteApp](remoteapp-licensing.md) 자세한 정보에 대 한 합니다. 및 [Azure RemoteApp과 함께 사용 하 여 Office](remoteapp-o365.md) hello Office 라이센스 정보에 대 한 합니다.
> 
> 

각 이미지에 포함된 항목에 대한 내용도 읽어보세요.

## <a name="windows-server-2012-r2--hello-vanilla-image"></a>Windows Server 2012 R2 ("hello 바닐라 이미지")
이 이미지는 Microsoft Windows Server 2012 R2 Datacenter 운영 체제에 따라 및 hello 다음 역할 및 기능 설치에 대 한 Azure RemoteApp 템플릿 이미지 toomeet hello 요구 사항:

* .NET Framework 4.5, 3.5.1, 3.5
* 데스크톱 경험
* 잉크 및 필기 서비스
* 미디어 파운데이션
* 원격 데스크톱 세션 호스트
* Windows PowerShell 4.0
* Windows PowerShell ISE
* WoW64 지원

이 이미지에는 다음 응용 프로그램을 설치 하는 hello에 있습니다.

* Adobe Flash Player
* Microsoft Silverlight
* Microsoft System Center 2012 Endpoint Protection
* Microsoft Windows Media Player

## <a name="microsoft-office-365-proplus-subscription-required"></a>Microsoft Office 365 ProPlus(구독 필요)
Office 365는 "custom" 이미지에 작성 된 toowork 하므로 가장 요청한 응용 프로그램을 hello 됩니다.

이 이미지는 hello 바닐라 이미지의 확장 및 hello Microsoft Office 365 ProPlus의 다음 구성 요소 설치 또한 hello Windows Server 2012 R2 이미지에서 설명 하는 toohello 구성 요소:

* Access
* Excel
* Lync
* OneNote
* 비즈니스용 OneDrive (참고: Azure RemoteApp과 함께 사용 하기 위해 해당 hello 동기화 에이전트를 사용할 수 없습니다)
* Outlook
* PowerPoint
* Word
* Microsoft Office 언어 교정 도구

hello 이미지에는 Visio Pro 및 Pro 프로젝트도 포함 됩니다.

및 응용 프로그램에도 다음 hello:

* SQL Native client
* ODBC 드라이버
* SQL Server 데이터 마이닝 클라이언트
* MasterDataServices 클라이언트
* Microsoft Publisher
* PowerQuery
* PowerMap

Office 365 ProPlus 계획이 있는 사용자만 Office 365 ProPlus 앱의 모든 기능을 사용할 수 있습니다. Hello Office 365 구독에 대 한 자세한 내용은 계획 참조 [Office 365 서비스 계획](http://technet.microsoft.com/library/office-365-plan-options.aspx)합니다. 질문이 있으십니까? 체크 아웃 hello [Office 365 + RemoteApp](remoteapp-o365.md) 정보입니다. Hello 새 문서를 확인해 [어떻게 toouse Azure RemoteApp과 함께 Office 365 구독](remoteapp-officesubscription.md)합니다.

자신의 라이선스를 사용할 구성 파일은 각각 할 toolicense Office 365 ProPlus, Visio Pro 및 프로젝트 Pro 별도로-참고 합니다.

## <a name="microsoft-office-2013-professional-plus-trial-only"></a>Microsoft Office 2013 Professional Plus(평가판 전용)
Hello 무료 평가 기간 중 hello Office 2013 이미지로 hello 서비스를 테스트할 수 있습니다.

이 이미지는 hello 바닐라 이미지의 확장 및 hello Microsoft Office 2013 Professional Plus의 다음 구성 요소 설치 또한 hello Windows Server 2012 R2 이미지에서 설명 하는 toohello 구성 요소:

* Access
* Excel
* Lync
* OneNote
* 비즈니스용 OneDrive (참고: Azure RemoteApp과 함께 사용 하기 위해 해당 hello 동기화 에이전트를 사용할 수 없습니다)
* Outlook
* PowerPoint
* Project
* Visio
* Word
* Microsoft Office 언어 교정 도구

> [!IMPORTANT]
> **법적 정보:** 이 이미지에는 Microsoft Office 라이선스를 포함하지 않으며 *프로덕션에 사용할 수 없습니다*. hello Office 2013 Professional 더하기 이미지 평가판에 사용이 됩니다. 프로덕션에 대 한 Azure RemoteApp에서 toouse 오피스 응용 프로그램을 원하는 경우 toouse hello Office 365 ProPlus 이미지를 해야 합니다. 라이선스 Office에 대한 자세한 내용은 [Azure RemoteApp과 함께 Office 365 사용](remoteapp-o365.md)
> 
> 

