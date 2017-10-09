---
title: "aaaMicrosoft Azure의 SAP 용 인증 | Microsoft Docs"
description: "현재 구성과 hello Azure 플랫폼에 sap 인증 목록을 업데이트 합니다."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2017
ms.author: rclaus
ms.custom: 
ms.openlocfilehash: 4001375b465b3abd27335064454b7fe8979f1530
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sap-certifications-and-configurations-running-on-microsoft-azure"></a>Microsoft Azure에서 실행되는 SAP 인증 및 구성

SAP와 Microsoft는 고객에게 상호 혜택을 주는 강력한 파트너 관계 속에서 장기간 함께 협력해 왔습니다. Microsoft 플랫폼과 지속적으로 업데이트 되 고 순서 tooensure Microsoft Azure에서에서 새 인증 세부 정보 tooSAP 제출 하는 hello에 어떤 toorun 지정 기능이 뛰어난 SAP 작업. hello 다음를 정리한 표 우리의 지원 되는 구성 및 인증 증가의 목록입니다. 

## <a name="sap-hana-certifications"></a>SAP HANA 인증

| SAP 제품 | 지원되는 OS | Azure 제품 |
| --- | --- | --- |
| SAP HANA Developer Edition (hello HANA 클라이언트 소프트웨어를 포함 하 여 이루어진 SQLODBC, ODBO Windows만, ODBC, JDBC 드라이버, HANA studio 및 HANA 데이터베이스) |Red Hat Enterprise Linux, SUSE Linux Enterprise | D 시리즈 VM 제품군 |
| HANA One |Red Hat Enterprise Linux, SUSE Linux Enterprise |DS14_v2(일반 공급 시) |
| SAP S/4 HANA |Red Hat Enterprise Linux, SUSE Linux Enterprise |GS5의 제어되는 가용성, Azure(큰 인스턴스)에서 SAP HANA 사용 |
| Suite on HANA, OLTP |Red Hat Enterprise Linux, SUSE Linux Enterprise |비프로덕션 시나리오를 위한 단일 노드 배포의 GS5, Azure(큰 인스턴스)에서 SAP HANA 사용 |
| HANA Enterprise for BW, OLAP |Red Hat Enterprise Linux, SUSE Linux Enterprise |단일 노드 배포의 GS5, Azure(큰 인스턴스)에서 SAP HANA 사용 |
| SAP BW/4 HANA |Red Hat Enterprise Linux, SUSE Linux Enterprise |단일 노드 배포의 GS5, Azure(큰 인스턴스)에서 SAP HANA 사용 |

## <a name="sap-netweaver-certifications"></a>SAP NetWeaver 인증
Microsoft Azure hello를 모두 지 원하는 Microsoft 및 SAP에서 SAP 제품 다음에 대 한 인증 합니다.

| SAP 제품 | 게스트 OS | RDBMS | 가상 컴퓨터 유형 |
| --- | --- | --- | --- |
| SAP Business Suite 소프트웨어 |Windows, SUSE Linux Enterprise, Red Hat Enterprise Linux, Oracle Linux |SQL Server, Oracle(Windows 및 Oracle Linux만 해당), DB2, SAP ASE |A5 tooA11, D11 tooD14, DS11 tooDS14, DS11_v2 tooDS15_v2, GS1 tooGS5 |
| SAP Business All-in-One |Windows, SUSE Linux Enterprise, Red Hat Enterprise Linux |SQL Server, Oracle(Windows 및 Oracle Linux만 해당), DB2, SAP ASE |A5 tooA11, D11 tooD14, DS11 tooDS14, DS11_v2 tooDS15_v2, GS1 tooGS5 |
| SAP BusinessObjects BI |Windows |해당 없음 |A5 tooA11, D11 tooD14, DS11 tooDS14, DS11_v2 tooDS15_v2, GS1 tooGS5 |
| SAP NetWeaver |Windows, SUSE Linux Enterprise, Red Hat Enterprise Linux |SQL Server, Oracle(Windows 및 Oracle Linux만 해당), DB2, SAP ASE |A5 tooA11, D11 tooD14, DS11 tooDS14, DS11_v2 tooDS15_v2, GS1 tooGS5 |
