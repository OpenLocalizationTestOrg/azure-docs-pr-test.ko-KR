---
title: "Azure 마켓플레이스 hello에 대 한 가상 컴퓨터 이미지를 만들기 위한 필수 구성 요소 aaaTechnical | Microsoft Docs"
description: "다른 사용자에 대 한 가상 컴퓨터 이미지 toohello Azure 마켓플레이스를 배포 하기 위한 hello 요구 사항을 이해 toopurchase 합니다."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 63c16966-0304-4b17-a715-368a0a5ccb2c
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: fcae4d9e052581e3c1dfe7962e6d50ec31040419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="technical-prerequisites-for-creating-a-virtual-machine-image-for-hello-azure-marketplace"></a>Azure 마켓플레이스 hello에 대 한 가상 컴퓨터 이미지를 만들기 위한 필수 구성 요소를 기술
Hello 프로세스 시작 하기 전에 철저 하 게 읽고 각 단계도 수행 하는 위치와 이유를 이해 합니다. 가능한 한 있습니다 해야 회사 정보 및 기타 데이터를 준비, 필요한 도구를 다운로드 및/또는 hello 제안 만들기 프로세스를 시작 하기 전에 기술 구성 요소를 만들어야 합니다. 이 문서를 검토하여 이러한 항목에 대해 명확히 알아야 합니다.  

## <a name="download-needed-tools--applications"></a>필요한 도구 및 응용 프로그램 다운로드
다음 항목 hello 프로세스를 시작 하기 전에 hello가 있어야 합니다.

* 운영 체제에 따라 대상으로 하는, 설치 hello [Azure PowerShell cmdlet](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) 또는 [Linux 명령줄 인터페이스 도구](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) hello에서 [Azure 다운로드](https://azure.microsoft.com/downloads/) 페이지입니다.
* CodePlex에서 Azure 저장소 탐색기를 설치합니다.
* 다운로드 하 여 Azure 인증에 대 한 hello 인증 테스트 도구를 설치 합니다.
  * [http://go.microsoft.com/fwlink/?LinkID=526913](http://go.microsoft.com/fwlink/?LinkID=526913). Windows 기반 컴퓨터 toorun hello 인증 도구가 필요 합니다. Windows 기반 컴퓨터를 사용할 수 없는 경우에 Windows 기반 VM을 사용 하 여 Azure의 hello 도구를 실행할 수 있습니다.

## <a name="platforms-supported"></a>지원되는 플랫폼
Windows 또는 Linux에서 Azure 기반 VM을 개발할 수 있습니다. Hello 게시 프로세스-는 Azure 호환 가상 하드 디스크 (VHD)-다른 도구를 사용 하 고 사용 중인 운영 체제에 따라 단계를 만드는 등의 일부 요소:  

* Linux를 사용 하는 경우의 hello toohello "(Linux 기반)는 Azure 호환 VHD 만들기" 섹션을 참조 하십시오. [가상 컴퓨터 이미지 게시 가이드](marketplace-publishing-vm-image-creation.md)합니다.
* Windows를 사용 하는 경우의 hello toohello "(Windows 기반)는 Azure 호환 VHD 만들기" 섹션을 참조 하십시오. [가상 컴퓨터 이미지 게시 가이드](marketplace-publishing-vm-image-creation.md)합니다.

> [!NOTE]
> Tooa Windows 기반 컴퓨터를 액세스 필요 합니다.
> 
> * Hello 인증 유효성 검사 도구를 실행 합니다.
> * VHD 인증을 제출 hello에 대 한 hello VHD 공유 액세스 서명 URL을 만듭니다.
> 
> 

## <a name="develop-your-vhd"></a>VHD 개발
Hello 클라우드 또는 온-프레미스에서 Azure Vhd를 개발할 수 있습니다.

* 클라우드 기반 개발에서는 모든 개발 단계를 Azure에 있는 VHD에서 원격으로 수행합니다.
* 온-프레미스 개발에서는 VHD를 다운로드하고 온-프레미스 인프라를 사용하여 VHD를 개발해야 합니다. 이 방법은 가능하지만 권장되지는 않습니다. Windows 또는 SQL에 대 한 개발 온-프레미스 키가 필요 하면 toohave hello 관련 온-프레미스 라이선스 note 합니다. VM을 만든 후에는 SQL Server를 포함하거나 설치할 수 없습니다. 자신의 구독을 기반 있습니다 hello Azure 포털에서에서 승인 된 SQL 이미지를 해야 합니다. Toodevelop 온-프레미스를 결정 한 경우 다르게 hello 클라우드에서 개발 하려는 경우 몇 가지 단계를 수행 해야 합니다. 관련 정보는 [온-프레미스 VM 이미지 만들기](marketplace-publishing-vm-image-creation-on-premise.md)를 참조하세요.

[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
