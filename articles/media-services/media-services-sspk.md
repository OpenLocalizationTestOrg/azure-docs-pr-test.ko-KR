---
title: "Microsoft® 부드러운 스트리밍 클라이언트 이식 키트 aaaLicensing"
description: "Toolicensing Microsoft® 부드러운 스트리밍 클라이언트 이식 키트 hello 하는 방법에 대해 알아봅니다."
services: media-services
documentationcenter: 
author: xpouyat
manager: cfowler
editor: 
ms.assetid: e3b488e7-8428-4c10-a072-eb3af46c82ad
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: xpouyat
ms.openlocfilehash: 56c3dccda73dd02207bb4dbe8109ba6fda917a6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-microsoft-smooth-streaming-client-porting-kit"></a>Microsoft® 부드러운 스트리밍 클라이언트 이식 키트 라이선스
## <a name="overview"></a>개요
Microsoft 부드러운 스트리밍 클라이언트 이식 키트 (**SSPK** 줄여서)는 포함 된 최적화 된 toohelp 장치 제조업체, 케이블 및 모바일 사업자, 콘텐츠 서비스 공급자, 송수화기는 부드러운 스트리밍 클라이언트 구현 제조업체, 독립 소프트웨어 공급 업체 (Isv) 및 솔루션 공급자 toocreate 제품 및 서비스 부드러운 스트리밍 형식의 적응 스트리밍 콘텐츠를 합니다. SSPK는 정식 사용자 tooany 장치 hello 및 플랫폼으로 이식 될 수 있는 부드러운 스트리밍 클라이언트의 장치 및 플랫폼 독립적 구현입니다. 

아래에 포함 된 높은 수준의 아키텍처 이며 IIS 부드러운 스트리밍 이식 키트 상자는 Microsoft에서 제공 하는 hello 부드러운 스트리밍 클라이언트 구현 하며 부드러운 스트리밍 콘텐츠를 재생 하기 위한 모든 hello 핵심 논리를 포함 합니다. 그런 다음 파트너는 적절한 인터페이스를 구현하며 특정 장치 또는 플랫폼에 맞게 이식합니다. 

![SSPK](./media/media-services-sspk/sspk-arch.png)

## <a name="description"></a>설명
SSPK는 뛰어난 비즈니스 가치를 제공하는 조건으로 사용 허가됩니다. SSPK 라이선스와 hello 업계를 제공합니다.

* C++의 부드러운 스트리밍 이식 키트 소스 
  * 부드러운 스트리밍 클라이언트 기능 구현
  * 형식 구문 분석, 추론, 버퍼링 논리 등 추가
* 플레이어 응용 프로그램 API 
  * 미디어 플레이어 응용 프로그램과 상호 작용을 위한 프로그래밍 인터페이스
* PAL(플랫폼 추상화 계층) 인터페이스 
  * hello 운영 체제 (스레드, 소켓)와 상호 작용에 대 한 프로그래밍 인터페이스
* HAL(하드웨어 추상화 계층) 인터페이스 
  * 하드웨어 A/V 디코더(디코딩, 렌더링)와 상호 작용을 위한 프로그래밍 인터페이스
* DRM(디지털 권한 관리) 인터페이스 
  * DRM hello DRM DAL (추상화 계층)을 통해 처리 하기 위한 프로그래밍 인터페이스
  * Microsoft PlayReady 이식 키트는 별도로 제공되지만 이 인터페이스를 통해 통합됩니다. Microsoft PlayReady 장치 라이선스에 대한 자세한 내용을 보려면 [여기](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl)를 클릭하세요.
* 구현 샘플 
  * Linux용 샘플 PAL 구현
  * GStreamer용 샘플 HAL 구현

## <a name="licensing-options"></a>라이선스 옵션
Microsoft 부드러운 스트리밍 클라이언트 이식 키트는 두 개의 고유 사용권 계약에서 사용 가능한 toolicensees 이루어집니다: 부드러운 스트리밍 클라이언트 중간 제품 및 부드러운 스트리밍 클라이언트 최종 제품 버전에서는 tooend 사용자 배포 관리를 위한 개발에 대 한 합니다.

* 칩셋 제조업체, 시스템 통합 업체가 또는 독립 소프트웨어 공급 업체 (Isv 소스 코드 포팅 해야 하 는) 키트는 Microsoft 부드러운 스트리밍 클라이언트 이식 키트 toodevelop 중간 제품 **중간 제품 라이선스** 실행 되어야 합니다.
* 장치 제조업체 또는 부드러운 스트리밍 클라이언트 최종 제품 버전에서는 tooend 사용자에 대 한 배포 권한이 필요로 하는 Isv hello Microsoft 부드러운 스트리밍 클라이언트 이식 키트에 대 한 **최종 제품 라이선스** 실행 해야 합니다.

### <a name="microsoft-smooth-streaming-client-porting-kit-interim-product-license"></a>Microsoft 부드러운 스트리밍 클라이언트 이식 키트 중간 제품 라이선스
이 라이선스에 따라 Microsoft는 부드러운 스트리밍 클라이언트 이식 키트 제공 필요한 지적 재산권 권한 toodevelop hello 및 부드러운 스트리밍 클라이언트 중간 제품 tooother 부드러운 스트리밍 클라이언트 이식 키트 장치 라이선스 실시 권 자 배포 하는 부드러운 스트리밍 클라이언트 최종 제품 버전에서는 배포 합니다.

#### <a name="fee-structure"></a>요금 구조
미국 $ 50, 000 번 라이센스 요금은 액세스 toohello 부드러운 스트리밍 클라이언트 이식 키트를 제공합니다. 

### <a name="microsoft-smooth-streaming-client-porting-kit-final-product-license"></a>Microsoft 부드러운 스트리밍 클라이언트 이식 키트 최종 제품 라이선스
이 라이선스에 따라 Microsoft는 다른 부드러운 스트리밍 클라이언트 이식 키트용 라이선스 실시 권 자 및 회사 브랜드 부드러운 스트리밍 클라이언트 최종 toodistribute에서 필요한 모든 지적 재산권 권한 tooreceive 부드러운 스트리밍 클라이언트 중간 제품을 제공 제품 tooend 사용자입니다.

#### <a name="fee-structure"></a>요금 구조
여기에서는 스트리밍 되지 않은 부드러운 클라이언트 최종 제품 hello 아래으로 사용료 모델에서 제공 됩니다.

* 제공된 장치 구현당 0.10달러
* 각 연도 50, 000 달러에 hello 사용료는 제한
* 각 연도의 최초 10,000대의 장치 구현에 대해서는 사용료 없음 

## <a name="licensing-procedure-and-sspk-access"></a>라이선스 절차 및 SSPK 액세스
모든 라이선스 관련 문의는 [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) 로 문의하시기 바랍니다.

hello [SSPK 배포 포털](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) 는 액세스할 수 있는 tooregistered 중간 라이선스 실시 권 자입니다.

중간 및 마지막 SSPK 라이선스 실시 권 자 기술 관련 질문에 너무 제출할 수[smoothpk@microsoft.com](mailto:smoothpk@microsoft.com)합니다.

## <a name="microsoft-smooth-streaming-client-interim-product-agreement-licensees"></a>Microsoft 부드러운 스트리밍 클라이언트 중간 제품 계약 정식 사용자
* Adroit Business Solutions, Inc
* Advanced Digital Broadcast SA
* AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.
* Albis Technologies Ltd.
* Alticast Corporation
* Amazon Digital Services, Inc.
* Arion Technology, Inc.
* AVC Multimedia Software Co., Ltd.
* Cavium, Inc.
* EchoStar Purchasing Corporation
* Enseo, Inc.
* Fluendo S.A.
* HANDAN BroadInfoCom Co., Ltd.
* Infomir GMBH
* Irdeto USA Inc.
* iWEDIA S.A. 
* Liberty Global Services BV
* MediaTek Inc.
* MStar Co, Ltd
* Nintendo Co., Ltd.
* OpenTV, Inc.
* Saffron Digital Limited
* Sichuan Changhong Electric Co., Ltd
* SoftAtHome
* Sony Corporation
* Tatung Technology Inc.
* TCL Technoly Electronics (Huizhou) Co., Ltd.
* Top Victory Investments, Ltd.
* Vestel Elektronik Sanayi ve Ticaret A.S.
* VisualOn, Inc.
* ZTE Corporation

## <a name="microsoft-smooth-streaming-client-final-product-agreement-licensees"></a>Microsoft 부드러운 스트리밍 클라이언트 최종 제품 계약 정식 사용자
* Advanced Digital Broadcast SA
* AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.
* Albis Technologies Ltd.
* Amazon Digital Services, Inc.
* AmTRAN Technology Co., Ltd.
* Arcadyan Technology Corporation
* Arion Technology, Inc.
* ATMACA ELEKTRONİK SAN. VE TİC. A.Ş
* British Sky Broadcasting Limited
* CastPal Technology Inc., Shenzhen
* Compal Electronics, Inc.
* Dongguan Digital AV Technology Corp., Ltd.
* EchoStar Purchasing Corporation
* Enseo, Inc.
* Filmflex Movies Limited
* Fluendo S.A.
* Gibson Innovations Limited
* Haier Information Applicantion S.R.L
* HANDAN BroadInfoCom Co., Ltd.
* Hisense International Co., Ltd. 
* Homecast Co.,Ltd
* Hon Hai Precision Industry Co., Ltd.
* Infomir GMBH
* Kaonmedia Co., Ltd.
* KDDI Corporation
* Nintendo Co., Ltd.
* Orange SA
* Saffron Digital Limited
* Sagemcom Broadband SAS
* Shenzhen Coship Electronics CO., LTD
* Shenzhen Jiuzhou Electric Co.,Ltd
* Shenzhen Skyworth Digital Technology Co., Ltd
* Sichuan Changhong Electric Co., Ltd.
* Skardin Industrial Corp.
* Sky Deutschland Fernsehen GmbH & Co. KG
* SmarDTV S.A.
* SoftAtHome
* Sony Corporation
* TCL Overseas Marketing (Macao Commercial Offshore) Limited
* Technicolor Delivery Technologies, SAS
* Tongfang Global Ltd.
* Top Victory Investments, Ltd.
* Toshiba Lifestyle Products & Services Corporation
* Universal Media Corporation /Slovakia/ s.r.o.
* VIZIO, Inc.
* Wistron Corporation
* ZTE Corporation


## <a name="media-services-learning-paths"></a>Media Services 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

