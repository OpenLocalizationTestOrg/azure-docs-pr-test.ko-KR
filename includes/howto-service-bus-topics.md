## <a name="what-are-service-bus-topics-and-subscriptions"></a>서비스 버스 토픽 및 구독 정의
서비스 버스 토픽 및 구독은 *게시/구독* 메시징 통신 모델을 지원합니다. 토픽 및 구독을 사용하는 경우 분산 응용 프로그램의 구성 요소가 서로 직접 통신하지 않고 중간자 역할을 하는 토픽을 통해 메시지를 교환합니다.

![TopicConcepts](./media/howto-service-bus-topics/sb-topics-01.png)

각 메시지가 단일 소비자에 의해 처리되는 서비스 버스 큐와 반대로, 토픽과 구독은 게시/구독 패턴을 사용하여 "일 대 다" 형태의 통신을 제공합니다. 여러 구독 tooa 항목을 등록 하는 것이 불가능 합니다. 메시지 tooa 항목을 보낼 때 것은 다음 사용할 수 있는 tooeach 구독 toohandle/프로세스 독립적으로 수행 합니다.

구독 tooa 항목 toohello 항목 보낸 hello 메시지의 복사본을 받는 가상 큐와 유사 합니다. 필요에 따라 toofilter 사용할 수 있는 구독 당 기준 항목에 대 한 필터 규칙을 등록 하거나 항목 구독에서 받은 메시지 tooa 주제를 제한할 수 있습니다.

서비스 버스 항목 및 구독 tooscale를 사용 하 고 많은 사용자와 응용 프로그램에서 매우 많은 메시지를 처리 합니다.

## <a name="create-a-namespace"></a>네임스페이스 만들기
서비스 버스 항목 및 구독을 사용 하 여 Azure에서 toobegin 먼저 만들어야 합니다는 *서비스 네임 스페이스*합니다. 네임스페이스는 응용 프로그램 내에서 서비스 버스 리소스의 주소를 지정하기 위한 범위 컨테이너를 제공합니다.

toocreate 네임 스페이스:

1. Toohello 로그온 [Azure 포털][Azure portal]합니다.
2. Hello hello 포털의 왼쪽된 탐색 창에서 클릭 **새로**, 클릭 **엔터프라이즈 통합**, 클릭 하 고 **서비스 버스**합니다.
3. Hello에 **네임 스페이스 만들기** 대화 상자에서 네임 스페이스 이름을 입력 합니다. hello 시스템 hello 이름이 사용 가능한 경우 즉시 toosee를 확인 합니다.
4. 만드는 있는지 hello 네임 스페이스 이름을 사용할 수 있는 되 면 hello 가격 책정 계층 (Basic, Standard 또는 Premium)를 선택 합니다.
5. Hello에 **구독** 필드는 toocreate hello 네임 스페이스에는 Azure 구독을 선택 합니다.
6. Hello에 **리소스 그룹** 필드는 hello 네임 스페이스: 라이브, 하거나 새로 만들 기존 리소스 그룹을 선택 합니다.      
7. **위치**, hello 국가 또는 지역에서 네임 스페이스를 호스트를 선택 합니다.
   
    ![네임스페이스 만들기][create-namespace]
8. Hello 클릭 **만들기** 단추입니다. hello 시스템 이제 네임 스페이스 만들고 사용 하도록 설정 합니다. 사용자 계정에 대 한 hello 시스템 규정 자원으로 몇 분 정도 toowait를 할 수 있습니다.

### <a name="obtain-hello-credentials"></a>Hello 자격 증명을 가져옵니다
1. 네임 스페이스의 hello 목록에서 새로 생성 된 네임 스페이스 이름 hello를 클릭 합니다.
2. Hello에 **서비스 버스 네임 스페이스** 블레이드에서 클릭 **공유 액세스 정책을**합니다.
3. Hello에 **공유 액세스 정책을** 블레이드에서 클릭 **RootManageSharedAccessKey**합니다.
   
    ![connection-info][connection-info]
4. Hello에 **정책: RootManageSharedAccessKey** 블레이드에서 다음 너무 hello 복사 단추를 클릭**연결 문자열-기본 키**, toocopy hello 연결 문자열 tooyour 클립보드 나중에 사용할 수 있습니다.
   
    ![connection-string][connection-string]

[Azure portal]: https://portal.azure.com
[create-namespace]: ./media/howto-service-bus-topics/create-namespace.png
[connection-info]: ./media/howto-service-bus-topics/connection-info.png
[connection-string]: ./media/howto-service-bus-topics/connection-string.png


