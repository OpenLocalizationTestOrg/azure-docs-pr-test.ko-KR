---
title: "시작 됨-Microsoft 위협 모델링 도구-Azure aaaGetting | Microsoft Docs"
description: "작업에 hello 위협 모델링 도구를 강조 표시에 대 한 깊은 개요입니다."
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 75ef139071e8abd0e743aa17b443a6e353f29372
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-threat-modeling-tool"></a>Hello 위협 모델링 도구를 시작 하기

hello 클라우드 및 엔터프라이즈 보안 도구 팀으로 무료 올해 초 hello 위협 모델링 도구 미리 보기를 출시  **[다운로드 하려면 클릭](https://aka.ms/tmtpreview)**합니다. 전달 메커니즘의 hello 변경을 통해 toopush hello 최신 향상 및 버그 수정 toocustomers toomaintain 쉽고 사용 하 여 hello 도구를 열 때마다 있습니다.
이 문서는 hello Microsoft SDL 위협 모델링 접근 시작 hello 과정을 안내 하 고 보안 프로세스의 핵심으로 toouse hello 도구 toodevelop 유용한 위협 모델링 하는 방법을 보여 줍니다.

이 문서 hello SDL 위협 모델링 접근의 기존 지식을 기반으로 합니다. 빠른 검토를 위해 참조 너무**[위협 모델링 웹 응용 프로그램](https://msdn.microsoft.com/library/ms978516.aspx)**  및 보관 된 버전의  **[보안 결함을 사용 하 여 확인할 hello 접근 방식을 STRIDE](https://docs.google.com/viewer?a=v&pid=sites&srcid=ZGVmYXVsdGRvbWFpbnxzZWN1cmVwcm9ncmFtbWluZ3xneDo0MTY1MmM0ZDI0ZjQ4ZDMy)**  2006의 MSDN 문서를 게시 합니다.

tooquickly 요약, hello 방법은 다이어그램을 만들어 위협을 식별을 완화 하 고 각 완화 유효성을 검사 하는 것입니다. 이 프로세스를 강조 표시하는 다이어그램은 다음과 같습니다.

![SDL 프로세스](./media/azure-security-threat-modeling-tool/sdlapproach.png)

## <a name="starting-hello-threat-modeling-process"></a>Hello 위협 모델링 프로세스를 시작 합니다.

Hello 위협 모델링 도구를 시작할 때 hello 그림에 표시 된 대로 몇 가지를 알 수 있습니다.

![빈 시작 페이지](./media/azure-security-threat-modeling-tool/tmtstart.png)

### <a name="threat-model-section"></a>위협 모델 섹션

| 구성 요소                                   | 세부 정보                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **피드백, 제안 및 문제 단추** | Hello 있습니다 하나  **[MSDN 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sdlprocess)**  SDL 모든 것에 대 한 합니다. 다른 사용자가 수행 하는 작업을 함께 해결 방법 및 권장 사항을 통해는 영업 기회 tooread를 제공 합니다. 원하는 항목 여전히 찾을 수 없는 경우 메일 tmtextsupport@microsoft.com 우리의 지원 팀 toohelp에 대 한 사용자                                                                                                                            |
| **모델 만들기**                          | 빈 캔버스 toodraw 있습니다에 대 한 다이어그램을 엽니다. 확인 되었는지 tooselect 템플릿을 원하는 toouse 모델에 대 한                                                                                                                                                                                                                                                                                                                                                                       |
| **새 모델에 대한 템플릿**                 | 모델을 만들기 전에 어떤 템플릿 toouse를 선택 해야 합니다. 우리의 기본 서식 파일에는 hello Azure 관련 스텐실, 위험, 완화 기능이 포함 된 Azure 위협 모델 템플릿을입니다. 일반 모델에 대 한 hello 드롭 다운 메뉴에서 hello SDL TM 기술 자료를 선택 합니다. Toocreate 서식 파일을 직접 아니면 모든 사용자에 대 한 새 제출 시겠습니까? 체크 아웃 우리의  **[템플릿 리포지토리](https://github.com/Microsoft/threat-modeling-templates)**  GitHub 페이지 toolearn 자세한                              |
| **모델 열기**                            | <p>이전에 저장된 위협 모델을 엽니다. hello 최근에 열린 모델 기능은 tooopen 가장 최근 파일을 해야 하는 경우 유용 합니다. Hello 선택 영역 위로 마우스를 가져가면 tooopen 모델에는 두 가지 방법 찾을 수 있습니다.</p><p><ul><li>이 컴퓨터에서 열기 - 로컬 저장소를 사용하여 파일을 여는 고전적인 방법</li><li>열기 OneDrive – 팀 OneDrive toosave에서 폴더를 사용 하 여 생산성을 높이고 단일 위치 toohelp 및 공동 작업에 자신의 모든 위협 모델을 공유 합니다.</li></ul></p> |
| **시작 가이드**                   | 엽니다 hello  **[Microsoft 위협 모델링 도구](./azure-security-threat-modeling-tool.md)**  기본 페이지                                                                                                                                                                                                                                                                                                                                                                                            |

### <a name="template-section"></a>템플릿 섹션

| 구성 요소               | 세부 정보                                                                                                                                                          |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **새 템플릿 만들기** | toobuild 하기 위한 빈 서식 파일을 엽니다. 템플릿을 새로 만드는 응용 프로그램 스트레스 없다면 권장 toobuild 기존 세션에서 |
| **템플릿 열기**       | 너무 toomake 변경에 대 한 서식 파일을 기존 열립니다.                                                                                                             |

hello 위협 모델링 도구 팀 tooimprove 도구 기능 및 환경을 지속적으로 작동 합니다. 약간의 차이가 hello 연도의 hello 과정을 통해 수행 될 수 있습니다 하지만 모든 주요 변경 hello 가이드에는 캡슐화 해야 합니다. Tooit 참조 hello 최신 공지를 얻게 tooensure 경우가 많습니다.

## <a name="building-a-model"></a>모델 작성

이 섹션에서는 다음을 따릅니다.

- Cristina(개발자)
- Ricardo(프로그램 관리자) 및
- Ashish(테스터)

첫 번째 위협 모델 개발의 hello 프로세스를 통해 있다는 것입니다.

> Ricardo: 안녕하세요 적신호, hello 위협 모델 다이어그램에 및 toomake 있는지 원하는 가져온 hello 세부 정보 오른쪽입니다. 살펴보는 데 도움을 주실 수 있으세요?
> Cristina: 물론입니다. 살펴보겠습니다.
> Ricardo는 hello 도구 열리고 적신호와 화면을 공유 합니다.

![기본 위협 모델](./media/azure-security-threat-modeling-tool/basictmt.png)

> Cristina: 네, 간단해 보이지만 단계별로 확인해 볼 수 있을까요?
> Ricardo: 물론입니다! Hello 분석 결과 다음과 같습니다.
> - 이 사용자는 엔터티 외부로 그려집니다. - 사각형
> - 명령을 tooour 웹 서버를 전송 하는-hello 원
> - hello 웹 서버는 데이터베이스 (두 개의 병렬 선)에 문의

Ricardo가 Cristina에게 보여준 것은 DFD, **[데이터 흐름 다이어그램](https://en.wikipedia.org/wiki/Data_flow_diagram)**의 짧은 버전입니다. hello 위협 모델링 도구에는 hello 빨간색 점선, 서로 다른 엔터티가 컨트롤에 있는 tooshow로 표시 된 사용자가 toospecify 신뢰 경계 수 있습니다. 예를 들어 IT 관리자가 Active Directory hello 제어할 이므로 Active Directory 시스템 인증을 위해 필요 합니다.

> 적신호: 오른쪽 toome를 찾습니다. Hello 위협 어떻습니까?
> Ricardo: 보여 드리겠습니다.

## <a name="analyzing-threats"></a>위협 분석

Hello 아이콘 메뉴 선택 항목에서 (파일 돋보기), tooa 목록이 생성 된 위협 hello 위협 모델링 도구가 hello 기본 템플릿을 기반으로 만들어지며 그 호출 hello SDL 접근 방식을 사용 하 여 hello 분석 보기를 클릭 한 후  **[ STRIDE (스푸핑, 변조, 정보 노출, 서비스 거부 및 권한 상승)](https://en.wikipedia.org/wiki/STRIDE_(security))**합니다. hello 개념은 소프트웨어 위협 6 이러한 범주를 사용 하 여 찾을 수 있는 예측 가능한 집합에서 제공 됨입니다.

이 방법은 달리 각 문을 실행 하 고 창 여 집 보안 잠금 메커니즘에에서 경보 시스템을 추가 하거나 hello 도둑 후 추적 합니다.

![기본 위협](./media/azure-security-threat-modeling-tool/basicthreats.png)

Ricardo는 hello hello 목록에서 첫 번째 항목을 선택 하 여 시작 합니다. 다음과 같은 상황이 발생합니다.

첫째, hello 두 스텐실 간의 상호 작용 hello 향상 되었으며

![상호 작용](./media/azure-security-threat-modeling-tool/interaction.png)

Hello 위협에 대 한 추가 정보를 두 번째 hello 위협 속성 창에 표시

![상호 작용 정보](./media/azure-security-threat-modeling-tool/interactioninfo.png)

생성 된 hello 위협 디자인의 잠재적 결함을 이해 하는 그 수 있습니다. hello STRIDE 분류를 통해 잠재적인 공격 벡터에 이해할 him, hello 하는 동안 추가 설명 알리는 정확히 어떤에 잘못 된 경우, 잠재적인 방법으로 toomitigate 함께 것입니다. Hello 근거 세부 정보에 편집 가능한 필드 toowrite 노트를 사용 하거나 기관의 저마다에 따라 우선 순위 등급을 변경할 수 그 합니다.

Azure 템플릿 뿐만 아니라 문제가 무엇 인지, 뿐만 아니라 방법을 이해 하는 추가 세부 정보 toohelp 사용자가 있는 toofix tooAzure 관련 문서를 설명, 예제 및 하이퍼링크를 추가 하 여 것입니다.

hello 설명 hello 중요성을 실제로 그 내용을 인증 메커니즘 tooprevent 사용자가 스푸핑 추가의 첫 번째 위협 toobe hello를 공개 작업 합니다. 몇 분 정도 적신호와 hello 토론에 이러한 원칙을 파악 hello 중요도 액세스 제어 및 역할을 구현 합니다. 구현 된 이러한 있는지 몇 가지 사항 toomake Ricardo 채워집니다.

정보 공개 아래 hello 위협에 Ricardo를, 그 hello 액세스 제어 계획 감사 및 보고서 생성에 대 한 일부 읽기 전용 계정이 필요한 실현 합니다. 그 궁금 있는지 여부를이 새 threat 야 하지만 그 hello 위험할을 그에 따라 표시 되므로 완화 된 hello hello 동일 합니다.
그 또한 조금 더 정보 공개 문제점에 대 한 생각 고 hello 백업 테이프 tooneed 암호화, hello 운영 팀에 대 한 작업을 진행 되 실현 합니다.

위협 tooexisting 완화 또는 보안 인해 적용 되지 않음 toohello 디자인에서는 너무 변경할 수 있습니다 hello 상태 드롭다운 목록에서에서 "해당 사항 없음"입니다. 다른 세 가지 선택 사항이: – 기본 선택 항목인 조사가 필요 – 시작 되지 기본값이 사용 toofollow 항목 및 완화 – 작업에 완벽 하 게 합니다.

## <a name="reports--sharing"></a>보고서 및 공유

Ricardo 적신호를 사용 하 여 hello 목록을 통해 이동 하 고 중요 한 참고 사항 추가 완화/근거, 우선 순위 및 상태 변경, 보고서에는 전체 보고서를 통해 toogo 그에 대 한 보고서를 출력 하는 좋은 보고서 저장-> 만들기-> 그 선택 동료 tooensure hello 적절 한 보안 작업 구현 됩니다.

![상호 작용 정보](./media/azure-security-threat-modeling-tool/report.png)

Ricardo tooshare hello 파일 대신 원하는 경우 그 쉽게 여 그렇게 할 수 기관의 OneDrive 계정에 저장 합니다. 그 hello 문서 링크를 복사 하 고 그의 동료와 공유할 수 그 합니다. 

## <a name="threat-modeling-meetings"></a>위협 모델링 회의

Ricardo OneDrive, Ashish, hello 테스터를 사용 하 여 위협 모델 toohis 서 보내면 underwhelmed 되었습니다. Ricardo와 Cristina가 쉽게 손상될 수 있는 몇 가지 중요한 특수한 사례를 놓친 것처럼 보였습니다. 그의 대처는 보수 toothreat 모델입니다.

이 시나리오에서는 Ashish hello 위협 모델 처리 후 그 라는 두 개의 위협 모델링 회의 대 한: 한 모임 toosynchronize hello 프로세스와 hello 다이어그램 및 위협 검토 및 승인에 대 한 두 번째 회의 안내 합니다.

Hello 첫 번째 회의에서 Ashish hello SDL 위협 모델링 프로세스를 통해 모든 사용자를 검색 하는 10 분 소요 됩니다. 그런 다음 hello 위협 모델 다이어그램을 끌어온 하 고 자세히 설명 하는 시작 합니다. 5분 이내에 누락된 중요한 구성 요소가 확인되었습니다.

몇 분 이상 Ashish 되며, Ricardo hello 웹 서버 작성 된 방식을 하는 확장 된 설명은로 가져왔습니다. 회의 tooproceed에 대 한 이상적인 방법 hello 되지 않았기 하지만 모든 사람이 결국 동의 합니다. 초기 hello 불일치 검색 toosave hello 미래에서 시간으로 이동 되었습니다.

두 번째 회의 연습을 통해 hello 위협 hello 팀 hello와 서명 된 몇 가지 방법으로 tooaddress에 설명 hello 위협 모델에서 해제 합니다. Hello 문서 소스 제어에 체크 인 하며 개발을 계속 합니다.

## <a name="thinking-about-assets"></a>자산에 대한 고려

위협을 모델링한 일부 독자는 자산에 대해 전혀 다루지 않은 것을 인지했을 것입니다. 많은 소프트웨어 엔지니어 소프트웨어 자산 hello 개념에 이해 하 고 있는 자산 공격자에 관심이 있을 수 보다 더 잘 이해 발견 했습니다.

Toothreat 거 집 모델, 패밀리, 대체할 수 없는 사진이 나 중요 한 아트 워크에 대해 생각 하면 시작할 수 있습니다. 아마도 게 손상 될 수 있습니다 및 hello 현재 보안 시스템에 대 한 생각 하면 시작할 수 있습니다. 또는 hello hello 풀 또는 hello 프런트 친구와 같은 물리적 기능을 고려 하 여 시작할 수 있습니다. 이들은 자산, 공격자의 목표가 또는 소프트웨어 디자인에 대 한 유사한 toothinking입니다. 이러한 세 가지 방법 중 하나라도 작동합니다.

여기에 설명 된 것 hello 접근 방식을 toothreat 모델링은 크게 지난 hello에서 수행 하는 Microsoft가 보다 더 간단 합니다. Hello 소프트웨어 디자인 방법은 대부분의 팀에 대해 제대로 작동 하는지 확인 했습니다. 사용자를 포함하길 바랍니다.

## <a name="next-steps"></a>다음 단계

질문, 의견 및 문제를 보내 tootmtextsupport@microsoft.com합니다. **[다운로드](https://aka.ms/tmtpreview)**  hello 위협 모델링 도구 tooget 시작 합니다.
