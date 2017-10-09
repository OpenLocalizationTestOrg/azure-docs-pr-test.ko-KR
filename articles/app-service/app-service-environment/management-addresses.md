---
title: "aaaAzure 앱 서비스 환경 관리 주소"
description: "목록 hello 관리 주소가 toocommand 앱 서비스 환경 사용"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: a7738a24-89ef-43d3-bff1-77f43d5a3952
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: b34b6266dc3a35915421b14bf34eddc07c2825c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-management-addresses"></a>App Service Environment 관리 주소

앱 서비스 Environment(ASE) hello는 Azure 가상 네트워크 (VNet)에서 서브넷에 hello Azure 앱 서비스의 배포입니다.  관리할 수 있도록 hello ASE hello Azure 앱 서비스에서에서 액세스할 수 있어야 합니다.  이 ASE 관리 트래픽을 hello 사용자 제어 네트워크에서 이동 합니다.  Azure 앱 서비스 관리 서버 toohello 공용 VIP hello ASE 연관 된에서 제공 합니다.  Hello ASE에 대 한 자세한 내용은 종속성 네트워킹 읽을 [네트워킹 고려 사항 및 앱 서비스 환경 hello][networking]합니다.  Hello ASE에 대 한 일반적인 정보로 시작할 수 있습니다 [소개 toohello 앱 서비스 환경][intro]합니다.

이 문서에 대 한 관리 트래픽 toohello ASE hello 원본 Ip를 나열합니다. 이러한 주소 toocreate 네트워크 보안 그룹 toolock 들어오는 트래픽 다운을 사용 하거나 필요에 따라 경로 테이블에서 사용할 수 있습니다.  toouse toouse 필요한이 정보:

* 모든 지역에 대해 나열 된 hello IP 주소
* hello IP 주소 여 ASE에 배포 된 해당 일치 toohello 지역.

hello 들어오는 관리 트래픽에 이러한 IP 주소에서 tooports 454 및 455 있습니다.

| 지역 | 주소 |
|--------|-----------|
| 모든 지역 | 70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141 |
| 미국 중남부, 미국 중북부 | 23.102.188.65, 191.236.154.88 |
| 오스트레일리아 남동부, 오스트레일리아 동부 | 23.101.234.41, 104.210.90.65 |
| 미국 서부, 미국 동부 | 104.45.227.37, 191.236.60.72 |
| 서유럽, 북유럽 | 191.233.94.45, 191.237.222.191 |
| 미국 중서부, 미국 서부 2 | 13.78.148.75, 13.66.225.188 |
| 미국 중부, 미국 동부 2 | 104.43.165.73, 104.46.108.135 |
| 동아시아, 동남 아시아 | 23.99.115.5, 104.215.158.33 |
| 일본 동부, 일본 서부 | 104.41.185.116, 191.239.104.48 |
| 캐나다 중부, 캐나다 동부 | 40.85.230.101, 40.86.229.100 |
| 영국 서부, 영국 남부 | 51.141.8.34, 51.140.185.75 |
| 한국 남부, 한국 중부 | 52.231.200.177, 52.231.32.117 |
| 브라질 남부, 미국 중남부| 104.41.46.178, 23.102.188.65 |
| 인도 중부, 인도 남부 | 104.211.98.24, 104.211.225.66 |
| 인도 서부, 인도 남부 | 104.211.160.229, 104.211.225.66 |


<!-- LINKS -->
[networking]: ./network-info.md
[intro]: ./intro.md
