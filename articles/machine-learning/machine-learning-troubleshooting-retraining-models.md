---
title: "웹 서비스는 Azure 컴퓨터 학습 클래식 재교육 aaaTroubleshoot | Microsoft Docs"
description: "식별 하 고는 Azure 기계 학습 웹 서비스에 대 한 hello 모델 재교육는 일반적인 문제 이름을으로 해결 합니다."
services: machine-learning
documentationcenter: 
author: VDonGlover
manager: raymondl
editor: 
ms.assetid: 75cac53c-185c-437d-863a-5d66d871921e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 2b6a78eaba161877106dccdc23437b5e454fca7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-retraining-of-an-azure-machine-learning-classic-web-service"></a>Hello 재교육 Azure 컴퓨터 학습 클래식 웹 서비스의 문제 해결
## <a name="retraining-overview"></a>재학습 개요
예측 실험을 점수 매기기 웹 서비스로 배포하는 경우 정적 모델입니다. 새 데이터를 사용할 수 있게 됨 또는 hello API의 hello 소비자가 데이터에 다시 학습 되도록 toobe hello 모델에 필요 합니다. 

Hello 재교육 클래식 웹 서비스의 프로세스는 전체 연습은 참조 [보존 하기 위해 컴퓨터 학습 모델 프로그래밍 방식으로](machine-learning-retrain-models-programmatically.md)합니다.

## <a name="retraining-process"></a>재학습 프로세스
Tooretrain hello 웹 서비스를 해야 하는 경우 일부 추가 항목을 추가 해야 합니다.

* Hello 학습 실험에서에서 배포 된 웹 서비스입니다. hello 실험 있어야는 **웹 서비스 출력** 모듈이 연결의 hello toohello 출력 **모델 학습** 모듈입니다.  
  
    ![Hello 웹 서비스 출력 toohello 학습 모델을 연결 합니다.][image1]
* 새 끝점 tooyour 웹 서비스 점수 매기기를 추가 합니다.  Hello 끝점을 프로그래밍 방식으로 추가할 수 있습니다 hello에서 참조 하는 hello 샘플 코드를 사용 하 여 다시 학습 기계 학습 모델 프로그래밍 방식으로 항목 또는 hello Azure 클래식 포털을 통해.

다음 샘플 C# 코드 hello hello 학습 웹 서비스의 API 도움말 페이지 tooretrain 모델에서 사용할 수 있습니다. Hello 결과 평가 하 여 만족 되 면, 웹 서비스 사용자가 추가한 hello 새 끝점을 사용 하 여 점수 매기기 hello 학습 된 모델을 업데이트 합니다.

모든 hello 작업으로 tooretrain hello 모델을 수행 해야 하는 hello 주요 단계는 다음과 같습니다.

1. Hello 학습 웹 서비스 호출: 요청 응답 서비스 (RR) 하지 hello, hello 호출은 toohello 일괄 처리 실행 서비스 (BES)입니다. Hello API 도움말 페이지 toomake hello 호출 hello 샘플 C# 코드를 사용할 수 있습니다. 
2. Hello에 대 한 hello 값을 찾을 *BaseLocation*, *RelativeLocation*, 및 *SasBlobToken*: hello 출력에 프로그램 호출 toohello 교육 웹에서에서 이러한 값이 반환 서비스입니다. 
   ![샘플 및 hello BaseLocation, RelativeLocation, 및 SasBlobToken 값 재교육 hello의 hello 출력을 표시 합니다.][image6]
3. 학습 된 모델에서 새 웹 서비스 hello와 점수 매기기 hello 끝점 업데이트 hello 추가: hello 보존 하기 위해 기계 학습에서에서 모델을 프로그래밍 방식으로 hello 새 끝점 업데이트 제공 hello 샘플 코드를 사용 하 여 추가한 toohello 새로 hello 사용 하 여 모델 점수 매기기 hello 학습 웹 서비스에서에서 학습 된 모델입니다.

## <a name="common-obstacles"></a>일반적인 장애물
### <a name="check-toosee-if-you-have-hello-correct-patch-url"></a>올바른 URL 패치 hello 있으면 toosee 확인
hello 패치 URL을 사용 하는 hello hello에 연결 되어 있어야 합니다. 새 점수 매기기 끝점용 추가한 toohello 웹 서비스를 평가 합니다. 다양 한 방법으로 tooobtain hello 패치 URL에는

**옵션 1: 프로그래밍 방식으로**

tooget hello 패치 URL을 수정 합니다.

1. Hello 실행 [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) 샘플 코드입니다.
2. Hello AddEndpoint의 출력에서 찾을 hello *HelpLocation* 값 및 hello URL을 복사 합니다.
   
   ![HelpLocation hello addEndpoint 샘플의 hello 출력에서 합니다.][image2]
3. Hello URL을 hello 웹 서비스에 대 한 도움말 링크를 제공 하는 브라우저 toonavigate tooa 페이지에 붙여 넣습니다.
4. Hello 클릭 **업데이트 리소스** 링크 tooopen hello 패치 도움말 페이지.

**옵션 2: hello Azure 클래식 포털 사용**

1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. 열기 hello 기계 학습 탭 합니다. ![Machine Leaning 탭.][image4]
3. 작업 영역 이름을 클릭한 후 **웹 서비스**를 클릭합니다.
4. 웹 서비스를 사용 하는 점수 매기기 hello를 클릭 합니다. (Hello 웹 서비스의 hello 기본 이름을 수정 하지 않은 경우 끝납니다 [점수 매기기 Exp].의 합니다.)
5. **끝점 추가**를 클릭합니다.
6. Hello 끝점 추가 되 면 hello 끝점 이름을 클릭 합니다. 클릭 **업데이트 리소스** tooopen hello 도움말 페이지를 패치 합니다.

> [!NOTE]
> Hello hello를 클릭할 때 다음 오류가 표시는 hello 예측 웹 서비스 대신 hello 끝점 toohello 학습 웹 서비스를 추가한 경우 **업데이트 리소스** 링크: 죄송 합니다. 하지만이 기능은 지원 되지 않는 또는 이 컨텍스트에서 사용할 수 있습니다. 이 웹 서비스에 업데이트할 수 있는 리소스가 없습니다. 이 워크플로 개선으로 작업 하 hello 불편을 했습니다.
> 
> 

![새 끝점 대시보드.][image3]

hello를 사용 해야 하는 패치 URL을 포함 하 고 예제 코드를 사용할 수 있습니다를 제공 하는 hello 패치 도움말 페이지 toocall 것입니다.

![패치 URL.][image5]

### <a name="check-toosee-that-you-are-updating-hello-correct-scoring-endpoint"></a>Toosee hello 올바른 점수 매기기 끝점을 업데이트 하 고 있는지 확인 합니다.
* Hello 학습 웹 서비스를 패치 하지 않습니다: 웹 서비스를 평가 하는 hello에서 hello 패치 작업을 수행 해야 합니다.
* 웹 서비스에 대 한 hello 기본 끝점을 패치 하지 않습니다: hello 패치 작업 hello 새로운 사용자가 추가한 웹 서비스 끝점 점수 매기기에서 수행 해야 합니다.

웹 서비스 hello 끝점으로 설정 되어 방문 hello Azure 클래식 포털을 확인할 수 있습니다. 

> [!NOTE]
> Hello 끝점 toohello 예측 웹 서비스, 하지 hello 학습 웹 서비스를 추가 하는 확인 해야 합니다. 학습 및 예측 웹 서비스를 모두 올바르게 배포한 경우 나열된 두 개의 별도 웹 서비스가 표시됩니다. hello 예측 웹 서비스 "[예측 내선 번호]"로 끝나야 합니다.
> 
> 

1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. 열기 hello 기계 학습 탭 합니다. ![Machine Learning 작업 영역 UI.][image4]
3. 작업 영역을 선택합니다.
4. **웹 서비스**를 클릭합니다.
5. 예측 웹 서비스를 선택합니다.
6. 새 끝점 추가 toohello 웹 서비스 되는지 확인 합니다.

### <a name="check-hello-workspace-that-your-web-service-is-in-tooensure-it-is-in-hello-correct-region"></a>웹 서비스에 tooensure은 hello 올바른 영역에 있는 hello 작업 영역 확인
1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. 기계 학습 hello 메뉴에서 선택 합니다.
   ![Machine Learning 하위 지역 UI.][image4]
3. 작업 영역의 hello 위치를 확인 합니다.

<!-- Image Links -->

[image1]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png
