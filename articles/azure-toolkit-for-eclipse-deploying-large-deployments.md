---
title: "aaaDeploying 대규모 배포"
description: "Toodeploy 대규모 배포를 사용 하 여 Azure Toolkit for Eclipse hello 하는 방법에 대해 알아봅니다."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5e18bace-5df0-4af8-ad86-6151ea8bd823
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 6b1d2a7a5e49c78154fc856a221e64ca8dcfbe9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-large-deployments"></a>대규모 배포
배포가 너무 커서 toobe hello 기본 approot 폴더에 포함 된 면으로 사용할 수 있습니다 로컬 저장소 리소스 hello 배포 루트 폴더에 jdk 및 응용 프로그램 서버.

## <a name="toouse-a-local-storage-resource-as-hello-deployment-root-folder-for-large-deployments"></a>toouse 대규모 배포에 대 한 hello 배포 루트 폴더와 로컬 저장소 리소스
1. 새 로컬 저장소 리소스를 만듭니다. hello 리소스의 hello 이름 중요 하지 않습니다. 저장소 리소스는 hello 역할 수준에서 정의 됩니다. hello 가장 빠른 방법은 tooaccess hello 로컬 저장소 구성 대화 상자에서 새 로컬 저장소 리소스를 만들 수 있습니다는 단계를 수행 하는 hello를 사용 하 여: hello에서 마우스 오른쪽 단추로 클릭 hello 역할 **프로젝트 탐색기** 보기 (확장 프로그램 Azure 프로젝트 노드 hello 역할 보이지 않는 경우)를 클릭 하 여 **Azure**, 클릭 하 고 **로컬 저장소**합니다. Hello 내 **로컬 저장소** 대화 상자를 클릭 하 여 **추가** toocreate 새 로컬 저장소 리소스입니다.

2. 집합 hello 원하는 크기 tooat 최소 2048MB (아무 것도 덜 hello 같은 파일 크기에서에서 문제가 발생할 수 발생 하는 것 처럼 hello approot).

3. 확인 **hello 내용을 hello 역할 인스턴스가 재활용 될 때 정리** 확인란이; 것을 방지할 hello 배포의 시작 논리 hello 리소스의 기존 파일과 충돌을 일으키지에서 때 역할 hello 인스턴스가 재활용 됩니다.

4. 해당 hello 확인 **배포 후 리소스의 디렉터리 경로 hello 환경 변수 저장** 값이 설정 toohello 문자열 **DEPLOYROOT**합니다. 로컬 저장소 리소스 대화 상자에는 비슷한 toohello 다음을 찾습니다.

   ![][ic667943]

또는 사용 하는 경우 **DEPLOYROOT** hello로 *이름* 로컬 리소스의 바뀌지 않는 hello 자동으로 생성 된 환경 변수 이름 (너무 설정 **DEPLOYROOT_PATH** 경우), 응용 프로그램 뿐이 적합 합니다.

로컬 저장소 리소스를 만드는 방법에 대한 추가 정보는 [로컬 저장소 속성][Local storage properties]에서 찾을 수 있습니다.

## <a name="see-also"></a>참고 항목
[Eclipse용 Azure 도구 키트][Azure Toolkit for Eclipse]

[Eclipse에서 Azure용 Hello World 응용 프로그램 만들기][Creating a Hello World Application for Azure in Eclipse]

[Hello Eclipse 용 Azure 도구 키트 설치][Installing hello Azure Toolkit for Eclipse] 

Java와 함께 Azure 사용에 대 한 자세한 내용은 참조 hello [Azure Java 개발자 센터][Azure Java Developer Center]합니다.

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: ./media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
